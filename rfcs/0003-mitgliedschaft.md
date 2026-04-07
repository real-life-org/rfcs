# RFC-0003: Mitgliedschaft in der Real Life Organisation

- **Autor:** Anton Tranélis
- **Datum:** 2026-04-06
- **Status:** Draft

## Zusammenfassung

Die Real Life Organisation bildet ihre Mitgliedschaft über einen Space im Real Life Stack ab. Wer dem Space beitritt, ist Mitglied. Voraussetzung: eine Web-of-Trust-Identität und mindestens drei Attestations durch bestehende Mitglieder aufgrund echter, persönlicher Begegnungen.

## Motivation

Die Organisation wächst, und es braucht eine klare Antwort auf die Frage: "Wie werde ich Teil davon?" Diese Antwort muss zu unseren Werten passen — dezentral, vertrauensbasiert, ohne zentrale Kontrollinstanz. Gleichzeitig muss sie das Netzwerk vor Missbrauch schützen.

## Vorschlag

### Der Organisations-Space

Die Mitgliedschaft wird über einen **Space im Real Life Stack** abgebildet. Der Space ist der Ort, an dem die Organisation lebt — mit geteilten Dokumenten, Entscheidungen und Kommunikation.

- **Beitreten** = Mitglied werden
- **Entfernt werden** = Mitgliedschaft verlieren
- Es gelten die bestehenden Space-Regeln: Alle Mitglieder können einladen, Space-Admins können entfernen

### Voraussetzungen für den Beitritt

Um in den Organisations-Space eingeladen zu werden, braucht es:

1. **Eine Web-of-Trust-Identität** — Eine selbst erstellte, dezentrale Identität
2. **Drei Attestations von bestehenden Mitgliedern** — Jede Attestation setzt eine echte, persönliche Begegnung voraus

Attestations sind ein Feature des Web of Trust und stehen jedem offen — man muss nicht Mitglied der Organisation sein, um andere zu attestieren. Aber um dem Organisations-Space beizutreten, braucht man drei Attestations von Personen, die bereits Mitglied sind.

Keine Bewerbung. Kein Aufnahmekomitee.

### Was "echte Begegnung" bedeutet

Eine Attestation darf nur nach einer persönlichen Begegnung im echten Leben ausgestellt werden. Nicht nach einem Videocall, nicht nach einem Chat, nicht nach einem Telefonat.

Warum: Vertrauen wächst durch Präsenz. Wer jemanden persönlich getroffen hat, kann einschätzen, ob diese Person zum Netzwerk passt. Das ist bewusst eine hohe Schwelle — und das ist gut so.

### Was Mitgliedschaft bedeutet

Mitglieder können:

- **RFCs einreichen** — Vorschläge für die Organisation machen
- **RFCs reviewen** — Einwände erheben oder Zustimmung signalisieren
- **Rollen übernehmen** — Verantwortung in einem Bereich tragen
- **Andere einladen** — Neue Menschen in den Space holen (sofern die Voraussetzungen erfüllt sind)

### Ausschluss

Wenn ein Mitglied das Netzwerk aktiv schädigt:

1. **Gespräch** — Die Spannung wird offen angesprochen
2. **Mediation** — Falls nötig, vermittelt eine dritte Person
3. **Entfernung aus dem Space** — Als letztes Mittel können Space-Admins ein Mitglied entfernen

Die Attestations bleiben bestehen — sie dokumentieren die echte Begegnung, die stattgefunden hat. Aber die Mitgliedschaft in der Organisation (= Space) kann beendet werden.

### Bootstrapping

Die Gründungsmitglieder — Anton, Timo, Tillmann, Sebastian — attestieren sich gegenseitig und bilden den initialen Space. Ab dann gilt die 3-Attestation-Regel für alle neuen Mitglieder.

## Alternativen

- **Einladung durch ein einzelnes Mitglied** — Zu niedrige Schwelle, ermöglicht schnelles unkontrolliertes Wachstum
- **Aufnahmekomitee oder Abstimmung** — Zentralisiert die Entscheidung, widerspricht der Dezentralität
- **Beitragsbasiert (Code, Zeit, Geld)** — Schließt Menschen aus die anders beitragen. Mitgliedschaft sollte auf Vertrauen basieren, nicht auf Leistung
- **Mitgliedschaft nur über Attestations (ohne Space)** — Kein Ausschlussmechanismus möglich, da Attestations nicht zurückgezogen werden können
- **Rein technisch (nur WoT-Identität)** — Kein Schutz vor Sybil-Attacken ohne die soziale Komponente der echten Begegnung

## Offene Fragen

- **Zustimmung zu Werten/Manifest:** Möglicherweise sollte der Beitritt auch eine formelle Zustimmung zu den Werten und dem Zweck der Organisation beinhalten (z.B. als Attestation). Das setzt voraus, dass diese Werte in einem eigenen RFC definiert werden. Sobald dieser RFC angenommen ist, werden die Beitrittsbedingungen entsprechend ergänzt.
- Soll es unterschiedliche Stufen der Mitgliedschaft geben (z.B. Beobachter vs. Vollmitglied)?
- Wie gehen wir mit Menschen um, die geografisch isoliert sind und schwer drei persönliche Begegnungen arrangieren können?
- Wer sind die initialen Space-Admins und wie werden neue Admins bestimmt?
- Braucht der Ausschluss eines Mitglieds einen RFC oder reicht die Entscheidung der Space-Admins?
