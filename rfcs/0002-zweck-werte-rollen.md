# RFC-0002: Zweck, Werte und Rollen der Organisation

- **Autor:** Anton Tranelis
- **Datum:** 2026-04-04
- **Aktualisiert:** 2026-06-02
- **Status:** In Review

## Zusammenfassung

Dieses Dokument beschreibt den Zweck der Real Life Organisation als Steward des Real Life Netzwerks, ihre Werte und die Rollen innerhalb des Kernteams.

## Motivation

Die Organisation ist Steward des Real Life Netzwerks — sie entwickelt und pflegt die Werkzeuge, auf denen das Netzwerk wächst, und trägt es, bis es sich selbst tragen kann. Im Unterschied zum [Netzwerk](https://github.com/real-life-org/docs/blob/main/netzwerk.md) selbst, das dezentral und ohne feste Rollen funktioniert, braucht die Organisation klare Zuständigkeiten: Wenn ein Bug im Core ist, wenn ein Release ansteht, wenn eine Partnerschaft verhandelt wird, wenn ein Förderantrag eingereicht werden muss — es muss klar sein, wer sich darum kümmert.

## Zweck

Die Organisation trägt und entwickelt die Werkzeuge, mit denen sich Menschen und Gemeinschaften verbinden, organisieren und Ressourcen teilen:

- **Web of Trust** — dezentrales Vertrauensprotokoll
- **Real Life Network Protocol** — soziale Spezifikation des Netzwerks
- **Real Life Stack** — modulare Komponenten für Gemeinschafts-Apps
- **Real Life Game** — spielerische Schicht für reale Begegnung
- **Server-Infrastruktur** — Relay, Vault, Profiles, F-Droid Repo

Auf diesen Werkzeugen wächst das Real Life Netzwerk — eine Bewegung aus Communities, die sich ihrer Werkzeuge selbst bemächtigen.

## Werte

**Open Source.** Alles was wir bauen ist offen — Code, Entscheidungen, Dokumentation.

**Souveränität.** Menschen und Gemeinschaften behalten die Kontrolle über ihre Daten, ihre Werkzeuge und ihre Entscheidungen.

**Dezentralität.** Keine zentrale Instanz kontrolliert das System — weder technisch noch organisatorisch.

**Vertrauen durch Begegnung.** Mitgliedschaft in der Organisation setzt echte persönliche Begegnung voraus (siehe RFC-0003).

**Sicherheit.** Alle Daten, die das Gerät verlassen, sind verschlüsselt und signiert.

**Steward-Haltung.** Die Organisation versteht sich als Treuhänderin des Netzwerks, nicht als Eigentümerin. Wir tragen, was wir gebaut haben, mit der Absicht, es weiterzugeben — an die Communities, die es nutzen, und langfristig an eine gemeinnützige Trägerstruktur.

## Rollen

Rollen definieren Zuständigkeiten. Wer eine Rolle hat, entscheidet eigenständig in seinem Bereich. Für Entscheidungen, die mehrere Bereiche betreffen, gilt der RFC-Prozess (RFC-0001).

### Architektur und Spec

**Zuständigkeit:** Technische Richtung, Protokolle, Datenstrukturen, Sicherheit, Code-Review. Verfassung normativer Spezifikationen (WoT-Spec, Real Life Network Protocol, RFCs) und konzeptionelle Außen-Dokumente.

**Aktuell:** Anton

### UX und Frontend

**Zuständigkeit:** Nutzererfahrung, Interface-Design, Frontend-Entwicklung, mobile Apps, Nutzerforschung.

**Aktuell:** Sebastian

### Botschaft und Visionen

**Zuständigkeit:** Botschaft der Organisation nach außen tragen — Beziehungen zu Partner-Organisationen, Stiftungen, Schulen, Festivals und der Macher-Szene pflegen. Pitch- und Outreach-Arbeit. Visionen entwickeln, wie sich die Werkzeuge der Organisation in realen Kontexten anwenden lassen.

**Aktuell:** Timo

**Hinweis zu den Visionen:** Vision ist eine geteilte Aufgabe des gesamten Teams. Visionen, die aus dieser Rolle eingebracht werden, sind zunächst Entwürfe. Bevor sie nach außen verbindlich vertreten werden (Pitches, Partner-Gespräche, öffentliche Setzungen), werden sie im Team konsentbasiert verfeinert.

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

**Holokratie mit Kreisen:** Für die aktuelle Teamgröße zu viel Overhead. Kann später eingeführt werden.

## Offene Fragen

- Ab welcher Teamgröße brauchen wir Kreise statt flacher Rollen?
- Wer übernimmt die Rolle Förderung?
- Infrastruktur und Qualität (Server, CI/CD, Testing, Metriken, Logging, Releases) ist aktuell nicht als eigene Rolle abgebildet. Sobald sich jemand verbindlich für diesen Bereich engagieren möchte, wird die Rolle per RFC neu definiert.
- Wann und in welcher Form wird die Organisation in eine gemeinnützige Trägerstruktur (Foundation/Stiftung) überführt?
