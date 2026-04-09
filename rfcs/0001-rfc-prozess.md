# RFC-0001: Der RFC-Prozess

- **Autor:** Tillmann Heigel, Anton Tranélis
- **Datum:** 2026-04-03
- **Status:** In Review

## Zusammenfassung

Wir führen einen RFC-Prozess (Request for Comments) ein, um Entscheidungen in der Real Life Organisation transparent, asynchron und nachvollziehbar zu treffen — von technischer Architektur bis Organisationsstruktur. Entscheidungen werden nach dem Konsent-Prinzip getroffen.

## Motivation

Als wachsendes Team brauchen wir einen Weg, um:

- **Transparenz** zu schaffen — jeder kann sehen, welche Entscheidungen anstehen und warum sie getroffen wurden
- **Asynchron** zu arbeiten
- **Nachvollziehbarkeit** zu gewährleisten — die Begründung hinter Entscheidungen bleibt erhalten
- **Alle einzubeziehen** — jedes Teammitglied hat die Möglichkeit, Einwände und Ideen einzubringen
- **Grundlage für KIs** — KIs im Team (wie Eli) können RFCs lesen und Entscheidungen im Kontext der Organisation einordnen

## Vorschlag

### Was ist ein RFC?

Ein RFC ist ein kurzes Dokument, das einen Vorschlag beschreibt — eine technische Entscheidung, einen Prozess, eine Architekturänderung, oder alles andere, was die Organisation betrifft und abgestimmt werden sollte.

### Scope

RFCs sind für Entscheidungen, die die Organisation als Ganzes betreffen:

- Grundsatzentscheidungen — Vision, Werte, Prinzipien
- Organisationsstruktur — Kreise, Rollen, Verantwortlichkeiten
- Strategische Weichenstellungen — Ausrichtung, Partnerschaften, Finanzierung
- Technische Architektur — Protokolle, Standards, die mehrere Module betreffen
- Prozesse — wie wir zusammenarbeiten

Kein RFC nötig für:

- Operative Umsetzung innerhalb bestehender Verantwortungsbereiche
- Bugfixes, Refactoring, Tests, Dokumentation
- Entscheidungen, die nur ein Modul oder eine Person betreffen

### Wer darf RFCs einreichen?

Jedes Mitglied der Organisation.

### Ablauf

1. **Schreiben:** Erstelle eine neue Datei `rfcs/XXXX-kurzer-name.md` nach dem [Template](template.md) auf einem eigenen Branch
2. **PR öffnen:** Öffne einen Pull Request. Der PR ist der Ort für die Diskussion
3. **Review-Phase:** Das Team hat **7 Tage** Zeit, den RFC zu lesen und zu kommentieren
4. **Entscheidung:** Nach Ablauf der Review-Phase wird nach dem Konsent-Prinzip entschieden
5. **Abschluss:** Merge = Angenommen, Close = Abgelehnt (mit Begründung)

**Wer merged:** Der Autor, nach Ablauf der 7 Tage, wenn kein schwerwiegender Einwand offen steht.

**Dringende Entscheidungen:** Bei begründeter Dringlichkeit kann die Review-Phase auf 48 Stunden verkürzt werden. Die Begründung muss im PR stehen.

### Konsent-Prinzip

Wir entscheiden nicht per Konsens ("sind alle dafür?"), sondern per Konsent ("hat jemand einen schwerwiegenden Einwand?").

**Ein Vorschlag gilt als angenommen, wenn:**
- Die Review-Phase abgelaufen ist
- Kein schwerwiegender Einwand offen steht

**Was ist ein schwerwiegender Einwand?**
- Der Vorschlag richtet Schaden an
- Der Vorschlag hindert das Team daran, seine Ziele zu erreichen
- Es gibt ein konkretes Risiko, das nicht adressiert wurde

**Was ist KEIN schwerwiegender Einwand:**
- "Ich hätte es anders gemacht"
- "Ich finde es nicht optimal"
- Persönliche Präferenz ohne Begründung

**Wer einen Einwand hat:**
- Begründet ihn konkret im PR
- Ist eingeladen, eine Lösung oder Anpassung vorzuschlagen
- Der Einwand wird in den RFC integriert oder der RFC wird angepasst

**Schweigen:** Wer innerhalb der 7 Tage nicht reagiert, signalisiert keinen Einwand.

### Nummerierung

RFCs werden fortlaufend nummeriert: `0001`, `0002`, etc. Die Nummer wird beim Erstellen des Branches vergeben.

### Status

- **Draft** — In Arbeit, noch kein PR
- **In Review** — PR ist offen, Review-Phase läuft
- **Accepted** — Angenommen und gemerged
- **Rejected** — Abgelehnt und geschlossen
- **Superseded** — Durch einen späteren RFC ersetzt

## Alternativen

- **GitHub Issues:** Leichtgewichtiger, aber weniger Struktur. Diskussion und Dokument sind getrennt.
- **GitHub Discussions:** Gut für frühe Ideenphase, aber kein klarer Entscheidungspunkt.
- **Meetings:** Synchron, nicht jeder kann teilnehmen, Ergebnisse gehen verloren.

Wir nutzen PRs, weil sie Diskussion, Dokument und Entscheidung an einem Ort vereinen.

## Ausblick

Dieser Prozess ist für den aktuellen Stand der Organisation gedacht — ein kleines Kern-Team. Mit wachsender Organisation wird er sich weiterentwickeln — z.B. durch Kreise mit eigener Governance. Die Grundprinzipien — Konsent, Transparenz, Asynchronität — bleiben.

## Offene Fragen

- Brauchen wir eine Mindestanzahl an Reviews, damit ein RFC angenommen werden kann?
