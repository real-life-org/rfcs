# RFC-0002: Zweck, Werte und Rollen der Organisation

- **Autor:** Anton Tranélis
- **Datum:** 2026-04-04
- **Aktualisiert:** 2026-04-10
- **Status:** In Review

## Zusammenfassung

Dieses Dokument beschreibt den Zweck der Real Life **Organisation**, ihre Werte und die Rollen innerhalb des Kernteams. Es grenzt die Organisation klar vom Netzwerk ab.

## Motivation

Real Life besteht aus zwei Ebenen:

- Die **Organisation** (real-life.org) — das Kernteam, das Werkzeuge baut und Infrastruktur pflegt
- Das **Netzwerk** (real-life.network) — alle Menschen und Initiativen, die sich verbinden

Das Netzwerk ist dezentral, gehört niemandem und funktioniert ohne feste Rollen (siehe [netzwerk.md](https://github.com/real-life-org/docs/blob/main/netzwerk.md)). Die Organisation dagegen braucht klare Zuständigkeiten: Wenn ein Bug im Core ist, muss klar sein, wer entscheidet. Wenn eine Architekturentscheidung ansteht, muss klar sein, wer sie trifft.

Dieses Dokument definiert, wie die Organisation arbeitet — nicht wie das Netzwerk funktioniert.

## Zweck

Die Organisation dient dem Netzwerk. Sie baut und pflegt die Werkzeuge, mit denen sich Menschen und Gemeinschaften verbinden, organisieren und Ressourcen teilen.

Konkret:
- **Web of Trust** — dezentrales Vertrauensprotokoll
- **Real Life Stack** — modulare Komponenten für Gemeinschafts-Apps
- **Real Life Map** — Karte zur Sichtbarmachung lokaler Initiativen
- **Server-Infrastruktur** — Relay, Vault, Profiles, F-Droid Repo

Die Organisation kontrolliert nicht das Netzwerk. Sie stellt Infrastruktur zur Verfügung, die jede Gemeinschaft frei nutzen, anpassen und selbst betreiben kann.

## Werte

**Open Source.** Alles was wir bauen ist offen — Code, Entscheidungen, Dokumentation.

**Souveränität.** Menschen und Gemeinschaften behalten die Kontrolle über ihre Daten, ihre Werkzeuge und ihre Entscheidungen.

**Dezentralität.** Keine zentrale Instanz kontrolliert das System — weder technisch noch organisatorisch.

**Vertrauen durch Begegnung.** Mitgliedschaft in der Organisation setzt echte persönliche Begegnung voraus (siehe RFC-0003).

**Sicherheit.** Alle Daten, die das Gerät verlassen, sind verschlüsselt und signiert.

## Rollen

Rollen definieren klare Zuständigkeiten innerhalb der Organisation. Wer eine Rolle hat, entscheidet eigenständig in seinem Bereich. Für Entscheidungen, die mehrere Bereiche betreffen, gilt der RFC-Prozess (siehe RFC-0001).

Rollen sind keine Hierarchie. Sie beschreiben, wer wofür Verantwortung übernimmt.

### Architektur & Entwicklung

**Zuständigkeit:** Technische Architektur, Core-Entwicklung (Web of Trust, Real Life Stack), Code-Qualität, Sicherheit

**Aktuell:** Anton

### Vision & Outreach

**Zuständigkeit:** Die größere Vision tragen, neue Menschen und Gemeinschaften einladen, Brücken bauen zu bestehenden Bewegungen, Kommunikation nach außen

**Aktuell:** Timo

### Prozesse & Infrastruktur

**Zuständigkeit:** CI/CD, Metriken, Logging, Integrationstests, Server-Infrastruktur

**Aktuell:** Tillmann

### UX & Mobile

**Zuständigkeit:** Benutzererfahrung, Mobile Apps, Interface-Design, Nutzerforschung

**Aktuell:** Sebastian

## Rollen vs. Netzwerk-Focalization

In der Organisation gibt es **Rollen** mit klarer Zuständigkeit und Entscheidungsgewalt.

Im Netzwerk gibt es **keine festen Rollen**. Stattdessen bringt jeder das ein, was ihm liegt — Begegnung, Verbindung, Sichtbarkeit, Logistik, Werkzeuge, Wachstum. Diese Tätigkeiten sind in [netzwerk.md](https://github.com/real-life-org/docs/blob/main/netzwerk.md) und im [Handbuch](https://github.com/real-life-org/docs/blob/main/handbuch.md) beschrieben.

Die Menschen in der Organisation sind gleichzeitig Teil des Netzwerks und bringen sich dort ein wie alle anderen auch — aber ihre Org-Rolle gibt ihnen zusätzlich Entscheidungsgewalt über technische und strategische Fragen.

## Rollen anpassen

Rollen werden per RFC angepasst, wenn:

- **Zu groß** — Eine Person schafft es nicht allein → Rolle aufteilen oder zweite Person dazu
- **Zu klein** — Kaum noch Aufgaben → mit einer anderen Rolle zusammenlegen
- **Falsch geschnitten** — Aufgaben landen regelmäßig bei der falschen Rolle → Verantwortungsbereiche neu schneiden
- **Neue Verantwortung entsteht** → neue Rolle schaffen

## Rollen neu besetzen

Die Rolle gehört nicht der Person. Wenn eine Verantwortung dauerhaft nicht wahrgenommen wird:

1. **Gespräch** — Das Team spricht die Spannung offen an
2. **Klärung** — Ist die Rolle zu groß? Fehlt Unterstützung? Gemeinsam eine Lösung suchen
3. **Neubesetzung** — Wenn sich nichts ändert, wird die Rolle per RFC neu vergeben

Die Person bleibt Teil der Organisation — nur die Verantwortung wechselt.

## Alternativen

**Keine formalen Rollen, alles fluid:** Funktioniert im Netzwerk, aber nicht für die Kernentwicklung. Wenn niemand klar zuständig ist, bleiben Bugs liegen und Architekturentscheidungen werden nicht getroffen.

**Holokratie mit Kreisen:** Für die aktuelle Teamgröße (4 Personen) zu viel Overhead. Kann später eingeführt werden, wenn die Organisation wächst.

## Offene Fragen

- Soll es eine Rolle für Finanzen/Fundraising geben?
- Ab welcher Teamgröße brauchen wir Kreise statt flacher Rollen?
