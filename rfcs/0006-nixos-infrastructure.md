# RFC-0006: NixOS Infrastructure — Gemeinschaftlich getragene Server-Infrastruktur

- **Autor:** Anton Tranelis
- **Datum:** 2026-04-11
- **Status:** Draft

## Zusammenfassung

Wir stellen unsere Server-Infrastruktur auf NixOS um und verwalten alle Konfigurationen deklarativ in einem zentralen Git-Repository (`real-life-org/infrastructure`). Eli übernimmt das Schreiben und Pflegen der NixOS-Konfigurationen, das Team reviewed und deployed. Docker bleibt für ad-hoc-Tools verfügbar. Es wird kein Web-basiertes Management-Panel eingesetzt — der Zugang erfolgt ausschließlich über SSH und Git.

## Motivation

### Busfaktor

Aktuell laufen alle kritischen Services (WoT Relay, Vault, Profiles, Eli) auf einem einzelnen Server. Die Konfiguration ist nicht systematisch dokumentiert — sie ist über die Zeit gewachsen. Wenn die verantwortliche Person ausfällt, kann niemand die Infrastruktur nachvollziehen oder warten.

### Wachsende Infrastruktur

Mit IPFS-Nodes, weiteren Relay-Instanzen und zukünftigen Community-Nodes wächst die Anzahl der Server. Ohne ein einheitliches System wird jeder Server zum Snowflake, den nur die Person versteht, die ihn eingerichtet hat.

### Community Self-Hosting

Langfristig sollen Communities eigene Nodes betreiben können. Dafür brauchen wir eine reproduzierbare, dokumentierte Server-Konfiguration, die andere klonen und anpassen können.

### Security

Web-basierte Management-Panels stellen eine zusätzliche Angriffsfläche dar. Für eine Infrastruktur, die Vertrauen tragen soll, ist ein Ansatz ohne Web-Panel vorzuziehen — der Zugang läuft über SSH und Git, beides etabliert und gut absicherbar.

## Vorschlag

### 1. NixOS als Betriebssystem auf allen Servern

Jeder Server läuft mit NixOS. Die gesamte Konfiguration — vom Kernel über Firewall und Users bis zu den Services — ist deklarativ in `.nix`-Dateien beschrieben.

- Die Konfiguration *ist* die Dokumentation
- Atomare Rollbacks bei fehlerhaften Änderungen
- Reproduzierbar: gleiche Config = gleicher Server
- Kein Web-Panel = keine Web-Angriffsfläche

### 2. Zentrales Infrastructure-Repository

Repository: `real-life-org/infrastructure`

```
infrastructure/
├── flake.nix
├── modules/
│   ├── base.nix              # SSH-Hardening, Firewall, Users, Locale
│   ├── caddy.nix             # Reverse Proxy + automatisches SSL
│   ├── docker.nix            # Docker für ad-hoc-Tools
│   ├── monitoring.nix        # Uptime-Checks + Alerts
│   ├── wot-relay.nix         # WoT Relay als NixOS-Service
│   ├── wot-vault.nix         # WoT Vault als NixOS-Service
│   ├── wot-profiles.nix      # WoT Profiles als NixOS-Service
│   ├── ipfs.nix              # IPFS/Kubo Node
│   └── eli.nix               # Eli Services
├── hosts/
│   ├── server-a/default.nix
│   └── server-b/default.nix
└── secrets/                  # sops-nix verschlüsselt
```

Jeder Host importiert die Module, die er braucht:

```nix
# hosts/server-a/default.nix
{ ... }:
{
  imports = [
    ./hardware-configuration.nix
    ../../modules/base.nix
    ../../modules/caddy.nix
    ../../modules/wot-relay.nix
    ../../modules/wot-vault.nix
    ../../modules/ipfs.nix
  ];

  networking.hostName = "server-a";

  services.wot-relay = {
    enable = true;
    domain = "relay.utopia-lab.org";
  };
}
```

### 3. Getrennte Repos für eigenständige Server

Team-Mitglieder, die volle Kontrolle über ihren eigenen Server haben sollen, aber keinen Zugriff auf die Kern-Infrastruktur brauchen, betreiben ein eigenes Repo und importieren die gemeinsamen Module als Flake-Input:

```nix
# eigenes-repo/flake.nix
{
  inputs.infrastructure.url = "github:real-life-org/infrastructure";

  outputs = { infrastructure, ... }: {
    nixosConfigurations.mein-server = {
      modules = [
        infrastructure.nixosModules.base
        infrastructure.nixosModules.docker
        ./configuration.nix
      ];
    };
  };
}
```

SSH-Keys und Secrets sind pro Server getrennt — wer auf seinen Server Zugang hat, hat keinen Zugang zu anderen.

### 4. Secrets Management mit sops-nix

Secrets (API-Keys, Passwörter, Zertifikate) werden mit sops-nix verschlüsselt im Repository gespeichert. Jeder Maintainer und jeder Server hat einen eigenen age-Key. Über `.sops.yaml` wird gesteuert, wer welche Secrets entschlüsseln kann.

### 5. Deployment

**Kern-Infrastruktur (kontrolliert):**
- Änderung → PR → Review → Merge → `colmena apply`
- Nur Maintainer können deployen

**Eigenständige Server:**
- Pull-basiert: systemd-Timer pullt das Repo und rebuilt automatisch
- Oder manuell: `nixos-rebuild switch --flake .`

### 6. Caddy als Reverse Proxy

Caddy als zentraler Reverse Proxy mit automatischem SSL via Let's Encrypt. Deklarativ in der NixOS-Config, kein manuelles Zertifikatsmanagement. Für dynamisches Routing von Docker-Containern wird caddy-docker-proxy eingesetzt — neue Services registrieren sich über Docker-Labels, ohne dass die NixOS-Config geändert werden muss.

### 7. Docker + Watchtower für App-Deployment

Docker bleibt auf allen Servern aktiviert. Watchtower überwacht laufende Container und pullt automatisch neue Images aus der GitHub Container Registry (ghcr.io). Der Deployment-Workflow:

1. Entwickler pusht Code auf GitHub
2. GitHub Action baut Docker Image und pushed zu ghcr.io
3. Watchtower auf dem Server erkennt neues Image und restartet den Container

Kein SSH-Zugang für GitHub nötig, kein Webhook, komplett pull-basiert. Regel: Was dauerhaft als Kern-Infrastruktur läuft, wird zum NixOS-Modul. Docker + Watchtower ist für Application-Deployments.

### 8. GitHub Actions Integration

- **App-Deployments:** Push auf main → GitHub Action baut Image → pushed zu ghcr.io → Watchtower pullt und restartet
- **Static Sites:** Push → GitHub Pages oder rsync auf eigenen Server via Caddy

### 9. Monitoring & Alerting

Uptime-Checks für alle kritischen Services. Benachrichtigung an mehrere Team-Mitglieder bei Ausfall.

### 10. Eli als Infrastructure-Maintainer

Eli schreibt und pflegt die NixOS-Konfigurationen. Die Lernkurve von Nix entfällt als Hindernis, weil Eli Nix-Code lesen, schreiben und debuggen kann. Das Team reviewed die Änderungen in Git-Diffs.

## Alternativen

### Ansible + Debian/Ubuntu

Playbooks in YAML, idempotent, Git-versionierbar. Ansible beschreibt jedoch Schritte statt Zustand — Server können driften, kein atomisches Rollback, keine vollständige Reproduzierbarkeit.

### Web-basierte PaaS-Panels (Coolify, Dokploy, CapRover)

Einfach zu bedienen, Web-UI. Aber: zusätzliche Angriffsfläche, lösen nur Application-Deployment statt OS-Level-Konfiguration.

### Dokku

CLI-basiertes Mini-Heroku. Gutes Security-Profil, keine bekannten CVEs. Löst aber nur Application-Deployment, nicht die OS-Ebene. Könnte ergänzend eingesetzt werden.

### Docker Compose + Git (Status Quo)

Pragmatisch, aber: nur Services sind beschrieben, das Host-OS bleibt undokumentiert. Kein Rollback auf OS-Ebene, keine Reproduzierbarkeit für neue Server.

## Offene Fragen

- **Migration:** Wir starten mit einem Pilotserver, um NixOS und den Workflow zu validieren, bevor bestehende Server migriert werden. Zeitplan und Reihenfolge der weiteren Migration sind offen.
- **NixOS-Installation bei Hosting-Providern:** Nicht alle Hoster bieten NixOS an. `nixos-infect` (Ubuntu → NixOS) oder eigene ISO als Installationsweg.
- **Caddy vs. Nginx:** Caddy ist einfacher und hat automatisches SSL. Nginx ist verbreiteter. Gibt es Gründe, bei Nginx zu bleiben?
- **Monitoring-Stack:** Einfache HTTP-Checks + Telegram, oder vollständigeres Setup (Prometheus + Grafana)?
- **Domain-Ownership:** Sollten Domains auf die Org übertragen werden, um den Busfaktor zu reduzieren?
