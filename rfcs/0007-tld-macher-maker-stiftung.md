# RFC-0007: Top-Level-Domains `.macher` und `.maker` und Macher-Stiftung

- **Autor:** Timo Martin
- **Datum:** 2026-06-02
- **Status:** In Review

## Zusammenfassung

Die Real Life Organisation schlägt vor, dass Hornbach im Vorlauf zur Gründung einer gemeinnützigen **Macher-Stiftung** beim ICANN die Top-Level-Domains `.macher` (deutsch) und `.maker` (international) im Bewerbungsfenster 2026 beantragt. Nach Delegation (voraussichtlich 2028) gehen die Registry-Rechte über einen Registry Operator Change an die Macher-Stiftung über. Die Real Life Organisation übernimmt im Service-Vertrag den technischen Betrieb der Registry-Plattform.

## Motivation

Vier Gründe sprechen für diesen Schritt jetzt:

**1. Zeitfenster.** Das ICANN-Bewerbungsfenster für neue Top-Level-Domains läuft vom 30.04.2026 bis 12.08.2026, 23:59 UTC. Die nächste Runde öffnet erst 2029 oder 2030. Wer in diesem Fenster nicht antritt, verliert die Strings für mindestens drei Jahre. Eine einmal delegierte TLD ist nicht kopierbar und nicht kaufbar.

**2. Bewegung ohne festen digitalen Ort.** Die Macher-, Maker- und DIY-Bewegung in Deutschland (1.038.254 Handwerksbetriebe, 500 offene Werkstätten, 1.000+ Repair-Cafés, 8.000+ Festival-Besucher in Ferropolis pro Saison, 1,84 Mio Real-Life-Guys-Abonnenten) hat aktuell keinen gemeinsamen digitalen Anker. Eine eigene Endung schafft sichtbare Zugehörigkeit, ähnlich wie `.berlin` für die Stadt oder `.eco` für die Umwelt-Bewegung.

**3. Industrie sucht ein sauberes Format.** Werkzeug- und Industrie-Marken (Stanley Black & Decker als Hauptsponsor der Maker Faire Hannover 2026, weitere) engagieren sich heute über kommerzielle Sponsoring-Pakete. Die Maker-Szene reagiert zurückhaltend, weil das Modell nach Werbe-Fläche aussieht. Eine gemeinnützige Stiftungs-Trägerschaft setzt einen alternativen Standard.

**4. Anschluss an unsere bisherige Arbeit.** Real Life Network, Web of Trust, Real Life Stack sind die technische Grundlage, auf der eine Macher-Plattform mit `.macher`-Adressen aufsetzen kann. Vier Jahre Vorarbeit treffen auf einen Use-Case mit klarem Partner (Hornbach) und klarem Zeitdruck.

## Vorschlag

### Konstruktion in zwei Stiftungen

**Real Life Network Foundation** (global, gemeinnützig, in Gründung):
Trägerin des Real Life Network als Werk — Stack, Web of Trust, alle Module, alle Spaces. Beschäftigt das Kernteam der Real Life Organisation. Stifter: Anton Tranelis, Timo Martin (Gründerkreis). Hornbach kann als Förderer dazukommen, ohne Eigentum zu erwerben.

**Macher-Stiftung** (deutsch, gemeinnützig, in Gründung):
Hüterin der TLDs `.macher` und `.maker` nach Delegation. Förderin der Macher-Bewegung. Hauptstifter: Hornbach. Anker im Stiftungsrat: Hornbach und Real Life Network Foundation. Spätere Co-Stifter: Werkzeug-Familienunternehmen (Festool, Knipex, STIHL, Wera, Hazet).

Beide Stiftungen schließen einen Service-Vertrag: Die Macher-Stiftung beauftragt die Real Life Network Foundation mit dem technischen Betrieb der Registry-Plattform.

### Zeitlicher Ablauf

| Phase | Wann | Aktion |
|-------|------|--------|
| 0 | Juni 2026 | Real Life Network Foundation aufsetzen — unabhängig vom TLD-Strang |
| 1 | Juni–Juli 2026 | Hornbach beauftragt ICANN-Anwaltskanzlei (Phase 1, Marketing-Budget, ca. 50-100 TEUR). Markenrechts-Prüfung, Antragsschrift, Backend-Anbindung |
| 2 | bis 12.08.2026 | Antrag im Namen Hornbach Holding bei ICANN eingereicht |
| 3 | bis 19.08.2026 | Zahlung 454 TUSD Antragsgebühr (sieben Tage Puffer) |
| 4 | Q3 2026 — Q1 2027 | Macher-Stiftung wird in Ruhe gegründet (BGB-Stiftung, gemeinnützig) |
| 5 | 12-18 Monate ICANN-Prüfung | Parallel wachsen Bewegungs-Anbindungen, Festival 2027 wird vorbereitet |
| 6 | Ende 2027 | ICANN-Delegation |
| 7 | 2028 | Registry Operator Change zur Macher-Stiftung. TLDs live. Real Life Network Foundation übernimmt im Service-Vertrag den technischen Betrieb |

### Rolle der Real Life Organisation

Die Real Life Organisation tritt in drei Schichten auf:

1. **GbR Anton + Sebastian Stein + Timo** für die Konzeptphase mit Hornbach (Anton, Vertragsentwurf 28.05.2026)
2. **Real Life Network Foundation** als langfristige Trägerin des Werks und Service-Partner der Macher-Stiftung
3. **Stiftungsrat-Sitz** in der Macher-Stiftung — Vertretung durch Anton oder Timo

Tillmann Heigel pausiert operativ (Job-Belastung Flixtrain), bleibt aber im Bereich Infrastruktur & Qualität ansprechbar.

### Was die Macher-Stiftung tut

Die Stiftung fördert mit den Domain-Registrierungs-Einnahmen (10-20 EUR pro Domain pro Jahr, Wholesale-Anteil ca. 60 %):

- Aufbau und Erhalt offener Werkstätten (Verbund Offener Werkstätten als Partner)
- Förderung der Repair-Café- und Reparatur-Initiativen-Bewegung
- Maker-Spaces und Fab Labs in unterversorgten Regionen
- Sichtbarkeit für lokale Handwerksbetriebe — Adress-Förderung, Quest-Plattform, Mentor-Verzeichnis
- Werkzeug-Stipendien für junge Macher und Auszubildende im Handwerk
- Lokale DIY-, Macher- und Maker-Festivals (kleinere Formate)
- Internationaler Maker-Austausch DE-CZ-AT-NL-EU-USA

Erwartetes Förder-Volumen über 10 Jahre: 6-8 Mio EUR im realistischen Szenario (130.000 Adressen kumuliert), bis 15-20 Mio EUR im ambitionierten Szenario (350.000 Adressen).

### Antragstyp und ICANN-Konformität

`.macher` und `.maker` werden als **Generic TLD** beantragt (offen für alle Macher), **nicht als Brand-TLD**. Brand-TLDs (Specification 13) sind eingeschränkt — nur der Inhaber darf Subdomains nutzen. Das würde die Mission verfehlen.

Im Antrag wird transparent angegeben, dass die Übertragung an die Macher-Stiftung nach Delegation geplant ist. Der Registry Operator Change ist etabliertes ICANN-Verfahren (Beispiele: `.tube`, `.gay`).

### Backend-Operator

Vorgesehen: Auslagerung an einen etablierten Registry-Operator. Drei Optionen werden in der Anwaltskanzlei-Phase verglichen:

- **nic.at** (Wien) — Backend für `.berlin` und `.hamburg`, Erfahrung mit deutschen Geo-TLDs
- **CentralNic** (London) — international, breites Portfolio
- **Identity Digital** (USA, ehemals Donuts) — größter Backend-Operator weltweit

Auswahl erfolgt nach Kosten, technischer Eignung und Vertrags-Flexibilität.

## Alternativen

**A — Brand-TLD `.hornbach`.** Hornbach könnte eine eigene Brand-TLD analog zu `.obi` beantragen (OBI hat seit September 2015 die Endung). Verfehlt aber die Mission, weil Brand-TLDs für die Bewegung geschlossen wären.

**B — Marketing über klassische Domains.** `.com`, `.de` oder kreative Domain-Konstruktionen. Erfüllen den Identitäts-Marker-Effekt nicht, weil sie austauschbar bleiben.

**C — Warten auf nächste ICANN-Runde 2029/2030.** Verzögerung um drei bis vier Jahre. Risiko: Konkurrenz beantragt in der Zwischenzeit `.macher` oder `.maker` — der String ist dann verloren.

**D — Macher-Stiftung gründen ohne TLD.** Möglich, aber die Stiftung verliert ihre digitale Heimat. Der Identitäts-Marker bleibt aus.

**E — Real Life Network Foundation beantragt allein.** Die RLN Foundation kann theoretisch selbst beantragen. Risiko: die 454 TUSD Antragsgebühr plus laufende Kosten sind für eine frische Foundation ohne Anker-Stifter schwer zu tragen. Hornbach als Antragsteller löst das Finanzkraft-Thema.

## Offene Fragen

1. **Förderung-Rolle in der Real Life Organisation** ist offen (siehe RFC-0002). Mit der Macher-Stiftung entsteht akuter Bedarf — Förderanträge, Stiftungskontakte, Mittelverwendung. Wer übernimmt das?
2. **Verhältnis zu RFC-0006** (Gemeinschaftlich getragene Server-Infrastruktur). Die Registry-Plattform der Macher-Stiftung ist eine Form von gemeinschaftlich getragener Infrastruktur. Wie greifen die beiden ineinander?
3. **Anwaltskanzlei-Auswahl.** Drei Kandidaten sind im Spiel (ComLaude, Lexsynergy, CSC Digital Brand Services). Wer entscheidet die Auswahl, mit welchen Kriterien?
4. **Stiftungsrechts-Anwalt für die Macher-Stiftung selbst.** Parallel zum ICANN-Anwalt brauchen wir einen Stiftungsrechts-Spezialisten in Deutschland für die BGB-Stiftungs-Gründung. Wer kennt einen?
5. **Verhältnis zur Real Life Network Foundation.** Diese Foundation ist parallel im Aufbau. Reihenfolge und Abhängigkeiten klären — was muss zuerst stehen, was kann parallel laufen?
6. **Macher-Festival 2027 als Verkündungs-Anlass.** Hornbach + Real Life Guys + Ferropolis. Wer trägt das ins Festival-Programm?

## Quellen

- ICANN New gTLD Program 2026 Round — [Übersicht](https://newgtldprogram.icann.org/en/application-rounds/round2), [Fee FAQ](https://newgtldprogram.icann.org/en/application-rounds/round2/2026-round-general/gtld-evaluation-fee/faqs/when-is-the-gtld-evaluation-fee-due), [Withdrawal/Refund Process](https://newgtlds.icann.org/en/applicants/global-support/withdrawal-refund)
- Hornbach Holding Geschäftsjahr 2024/25 — [EQS-News](https://www.eqs-news.com/news/corporate/hornbach-gruppe-erzielt-im-geschaeftsjahr-2024-25-solides-umsatz-und-ergebnisplus-und-steigert-weiter-marktanteile/5365b14d-5738-4930-80ab-2e5cacd6d5b1_de)
- ZDH Handwerks-Statistik 2024 — [Kennzahlen](https://www.zdh.de/daten-und-fakten/kennzahlen-des-handwerks/)
- Hauptdokument im Macher-Schule-Repo: [`docs/19-macher-universum-tld-vision.md`](https://github.com/lichtungooo/macher-schule/blob/master/docs/19-macher-universum-tld-vision.md) (volle Vision)
- Pitch-Dokument: [`docs/21-macher-universum-hornbach-pitch.md`](https://github.com/lichtungooo/macher-schule/blob/master/docs/21-macher-universum-hornbach-pitch.md)

## Bezug zu anderen RFCs

- **RFC-0001 (Prozess):** Dieser RFC nutzt den Konsent-Prozess wie in RFC-0001 beschrieben. 7 Tage Review-Phase, mindestens ein Approval, keine offenen Einwände.
- **RFC-0002 (Rollen):** Der RFC erzeugt Aufgaben in mehreren Rollen — Architektur (Anton, Registry-Plattform), UX (Sebastian Stein, Adress-Erlebnis), Bewegung & Außendarstellung (Timo, Partner-Kontakte), Förderung (offen). Eine Aktualisierung von RFC-0002 wird vorgeschlagen.
- **RFC-0003 (Mitgliedschaft):** Sobald die Macher-Stiftung steht, entstehen formale Mitgliedschafts-Verhältnisse (Stiftungsrat, Vorstand). Im Rahmen von RFC-0003 zu klären.
- **RFC-0006 (Gemeinschaftlich getragene Server-Infrastruktur):** Die Registry-Plattform der Macher-Stiftung ist ein Anwendungsfall der gemeinschaftlich getragenen Infrastruktur. Anschluss klären.
