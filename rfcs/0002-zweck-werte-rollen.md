# RFC-0002: Zweck, Werte und Rollen der Organisation

- **Autor:** Anton Tranélis
- **Datum:** 2026-04-04
- **Aktualisiert:** 2026-04-10
- **Status:** In Review

## Zusammenfassung

Dieses Dokument beschreibt den Zweck der Real Life Organisation, ihre Werte und die Rollen innerhalb des Kernteams.

## Motivation

Die Organisation ist das Kernteam, das die Werkzeuge baut — im Unterschied zum [Netzwerk](https://github.com/real-life-org/docs/blob/main/netzwerk.md), das dezentral und ohne feste Rollen funktioniert. Die Organisation braucht klare Zuständigkeiten: Wenn ein Bug im Core ist, muss klar sein, wer entscheidet. Wenn eine Architekturentscheidung ansteht, muss klar sein, wer sie trifft.

## Zweck

Die Organisation baut und pflegt die Werkzeuge, mit denen sich Menschen und Gemeinschaften verbinden, organisieren und Ressourcen teilen:

- **Web of Trust** — dezentrales Vertrauensprotokoll
- **Real Life Stack** — modulare Komponenten für Gemeinschafts-Apps
- **Real Life Map** — Karte zur Sichtbarmachung lokaler Initiativen
- **Server-Infrastruktur** — Relay, Vault, Profiles, F-Droid Repo

## Werte

**Open Source.** Alles was wir bauen ist offen — Code, Entscheidungen, Dokumentation.

**Souveränität.** Menschen und Gemeinschaften behalten die Kontrolle über ihre Daten, ihre Werkzeuge und ihre Entscheidungen.

**Dezentralität.** Keine zentrale Instanz kontrolliert das System — weder technisch noch organisatorisch.

**Vertrauen durch Begegnung.** Mitgliedschaft in der Organisation setzt echte persönliche Begegnung voraus (siehe RFC-0003).

**Sicherheit.** Alle Daten, die das Gerät verlassen, sind verschlüsselt und signiert.

## Rollen

Rollen definieren Zuständigkeiten. Wer eine Rolle hat, entscheidet eigenständig in seinem Bereich. Für Entscheidungen, die mehrere Bereiche betreffen, gilt der RFC-Prozess (RFC-0001).

### Architektur

**Zuständigkeit:** Technische Richtung, Protokolle, Datenstrukturen, Sicherheit, Code-Review

**Aktuell:** Anton

### Entwicklung & UX

**Zuständigkeit:** App-Entwicklung, Interface-Design, Nutzererfahrung, Mobile

**Aktuell:** Sebastian

### Infrastruktur & Qualität

**Zuständigkeit:** Server, CI/CD, Testing, Metriken, Logging, Releases

**Aktuell:** Tillmann

### Förderung

**Zuständigkeit:** Förderanträge, Stiftungskontakte, Mittelverwendung, Berichterstattung

**Aktuell:** *unbesetzt — wird gesucht*

## Rollen anpassen

Rollen werden per RFC angepasst, wenn:

- **Zu groß** — Eine Person schafft es nicht allein → Rolle aufteilen oder zweite Person dazu
- **Zu klein** — Kaum noch Aufgaben → mit einer anderen Rolle zusammenlegen
- **Falsch geschnitten** — Aufgaben landen regelmäßig bei der falschen Rolle → neu schneiden
- **Neue Verantwortung entsteht** → neue Rolle schaffen

## Rollen neu besetzen

Die Rolle gehört nicht der Person. Wenn eine Verantwortung dauerhaft nicht wahrgenommen wird:

1. **Gespräch** — die Spannung offen ansprechen
2. **Klärung** — Ist die Rolle zu groß? Fehlt Unterstützung? Gemeinsam eine Lösung suchen
3. **Neubesetzung** — per RFC neu vergeben

Die Person bleibt Teil der Organisation — nur die Verantwortung wechselt.

## Alternativen

**Keine formalen Rollen, alles fluid:** Wenn niemand klar zuständig ist, bleiben Bugs liegen und Architekturentscheidungen werden nicht getroffen.

**Holokratie mit Kreisen:** Für die aktuelle Teamgröße (4 Personen) zu viel Overhead. Kann später eingeführt werden.

## Offene Fragen

- Ab welcher Teamgröße brauchen wir Kreise statt flacher Rollen?
- Wer übernimmt die Rolle Förderung?
