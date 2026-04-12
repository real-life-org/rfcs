# RFC-0006: Gemeinschaftlich getragene Server-Infrastruktur

- **Autor:** Anton Tranelis
- **Datum:** 2026-04-11
- **Status:** Draft

## Zusammenfassung

Wir bauen eine Server-Infrastruktur auf, die gemeinschaftlich getragen, vollständig dokumentiert und reproduzierbar ist. Jede Server-Konfiguration liegt als Code in Git — transparent, versioniert, von mehreren Personen wartbar. Neue Server oder Community-Nodes lassen sich aus diesem Code aufsetzen. Es wird kein Web-basiertes Management-Panel eingesetzt — der Zugang erfolgt über SSH und Git.

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

### 1. Infrastructure as Code

Jede Server-Konfiguration — von Firewall und Users bis zu den Services — ist deklarativ als Code beschrieben und in Git versioniert. Als Werkzeug setzen wir NixOS ein, weil es den gesamten Server-Zustand deklarativ beschreibt und atomare Rollbacks ermöglicht.

- Die Konfiguration *ist* die Dokumentation
- Atomare Rollbacks bei fehlerhaften Änderungen
- Reproduzierbar: gleiche Config = gleicher Server

### 2. Zentrales Infrastructure-Repository

Alle Server-Konfigurationen und wiederverwendbare Module leben in einem gemeinsamen Repository: `real-life-org/infrastructure`

```
infrastructure/
├── flake.nix
├── modules/
│   ├── base.nix              # SSH-Hardening, Firewall, Users, Locale
│   ├── traefik.nix           # Reverse Proxy + automatisches SSL
│   ├── docker.nix            # Docker + Watchtower für App-Deployment
│   ├── monitoring.nix        # Uptime-Checks + Alerts
│   ├── wot-relay.nix         # WoT Relay
│   ├── wot-vault.nix         # WoT Vault
│   ├── wot-profiles.nix      # WoT Profiles
│   ├── ipfs.nix              # IPFS/Kubo Node
│   └── eli.nix               # Eli Services
├── hosts/
│   ├── server-a/default.nix
│   └── server-b/default.nix
└── secrets/                  # Verschlüsselt (sops-nix)
```

Jeder Host importiert die Module, die er braucht. Neuer Server? Neuen Ordner unter `hosts/`, Module auswählen, deployen.

### 3. Secrets Management

Secrets (API-Keys, Passwörter, Zertifikate) werden verschlüsselt im Repository gespeichert (sops-nix). Jeder Maintainer und jeder Server hat einen eigenen Schlüssel. So ist steuerbar, wer welche Secrets entschlüsseln kann.

### 4. Deployment

**Kern-Infrastruktur (kontrolliert):**
- Änderung → PR → Review → Merge → Deploy
- Nur Maintainer können deployen

**Eigenständige Server:**
- Pull-basiert: Server pullt das Repo und rebuilt automatisch
- Oder manuell angestoßen

### 5. Traefik als Reverse Proxy

Traefik als Reverse Proxy mit automatischem SSL via Let's Encrypt. Neue Docker-Container registrieren sich über Labels — kein manuelles Routing nötig.

### 6. App-Deployment via GitHub Actions + Watchtower

Docker bleibt auf allen Servern für Application-Deployments. Der Workflow:

1. Entwickler pusht Code auf GitHub
2. GitHub Action baut Docker Image und pushed zu ghcr.io
3. Watchtower auf dem Server erkennt das neue Image und aktualisiert den Container

Komplett pull-basiert, kein SSH-Zugang für CI nötig.

### 7. Hardware-Keys für privilegierte Zugänge

Root-Zugriff auf Server erfordert einen Hardware-Security-Key (z.B. Nitrokey 3, YubiKey). Der private Schlüssel existiert nur auf dem physischen Gerät und kann nicht extrahiert werden. Jede Verbindung erfordert physische Berührung des Sticks.

Hintergrund: Jeder im Team arbeitet mit AI-Tools, die als lokaler User laufen und grundsätzlich Zugriff auf alle Dateien haben — inklusive SSH Private Keys. Ein Hardware-Key schützt das Schlüsselmaterial für privilegierte Zugänge. Für eingeschränkte User (z.B. nur Docker-Rechte, kein sudo) ist ein Software-Key ausreichend.

### 8. Monitoring & Alerting

Uptime-Checks für alle kritischen Services. Benachrichtigung an mehrere Team-Mitglieder bei Ausfall.

### 9. Eli als Infrastructure-Maintainer

Eli schreibt und pflegt die Server-Konfigurationen. Das Team reviewed die Änderungen in Git-Diffs, ohne die Details der Konfigurationssprache kennen zu müssen.

## Alternativen

### Ansible + Debian/Ubuntu

Playbooks in YAML, idempotent, Git-versionierbar. Ansible beschreibt jedoch Schritte statt Zustand — Server können driften, kein atomisches Rollback, keine vollständige Reproduzierbarkeit.

### Web-basierte PaaS-Panels (Coolify, Dokploy, CapRover)

Einfach zu bedienen, Web-UI. Aber: zusätzliche Angriffsfläche, lösen nur Application-Deployment statt OS-Level-Konfiguration.

### Docker Compose + Git (Status Quo)

Pragmatisch, aber: nur Services sind beschrieben, das Host-OS bleibt undokumentiert. Kein Rollback auf OS-Ebene, keine Reproduzierbarkeit für neue Server.

## Stand

Dieses Setup wurde bereits beispielhaft für Timos Server umgesetzt. Der Server läuft mit NixOS, Traefik und Watchtower, die Konfiguration liegt im `real-life-org/infrastructure` Repo, und der End-to-End-Deploy-Workflow (git push → GitHub Action → ghcr.io → Watchtower → live) funktioniert.

## Offene Fragen

- **Migration:** Zeitplan und Reihenfolge für die Migration bestehender Server sind offen.
- **Monitoring-Stack:** Einfache HTTP-Checks + Telegram, oder vollständigeres Setup (Prometheus + Grafana)?
- **Domain-Ownership:** Sollten Domains auf die Org übertragen werden, um den Busfaktor zu reduzieren?
