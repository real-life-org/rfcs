# RFC-0005: Cross-Space Items

- **Autor:** Anton Tranélis
- **Datum:** 2026-04-09
- **Status:** Draft

## Zusammenfassung

Items können in mehreren Spaces referenziert werden, ohne dupliziert zu werden. Ein Item hat einen Heim-Space, in dem es lebt, und eine globale ID, über die andere Spaces es referenzieren können. Owner-Rechte sind an das Item gebunden, nicht an einen einzelnen Space.

## Motivation

Das Real Life Network verbindet bestehende Initiativen miteinander. In der Praxis heißt das:

- Agnes legt die "Transition Town Stuttgart" als Item auf der Karte an — in ihrem Space
- Die Transition Town Stuttgart hat auch einen eigenen Space und will das gleiche Item dort pflegen
- Der Real Life Circle Stuttgart will das Item ebenfalls auf seiner Karte zeigen
- Das bundesweite Transition-Netzwerk will alle lokalen Transition Towns sehen

Aktuell lebt ein Item in genau einem Y.Doc in genau einem Space. Es gibt keinen Mechanismus, ein Item über Space-Grenzen hinweg sichtbar oder bearbeitbar zu machen. Das verhindert die Vernetzung, die das Netzwerk ermöglichen soll.

### Szenarien

**Reisende Vernetzer:** Agnes und Jonathan fahren durch Europa und legen überall Items an. Sie wollen Ownership an lokale Menschen übergeben, die in anderen Spaces aktiv sind.

**Initiative mit eigenem Space:** Eine Lebensgemeinschaft hat ein Item auf der öffentlichen Karte UND einen eigenen Space. Das Item sollte in beiden sichtbar und konsistent sein.

**Regionale Aggregation:** Ein regionaler Space will alle öffentlichen Items aus der Region zeigen — ohne sie manuell zu duplizieren.

## Vorschlag

### Globale Item-ID

Jedes Item bekommt eine **globale ID**, die unabhängig vom Space ist. Diese ID ist stabil und ändert sich nicht, auch wenn das Item in anderen Spaces referenziert wird.

Format: Die bestehende Item-ID (UUID) wird zur globalen ID. Keine neue ID-Schicht nötig.

### Heim-Space

Jedes Item hat genau einen **Heim-Space**. Das ist der Space, in dessen Y.Doc das Item lebt — die Single Source of Truth. Alle Daten (Name, Beschreibung, Ort, Relationen) werden im Heim-Space gepflegt.

### Referenzen

Andere Spaces können ein Item **referenzieren**. Eine Referenz ist ein leichtgewichtiger Eintrag im Y.Doc des referenzierenden Spaces, der auf die globale ID und den Heim-Space verweist.

```
// Im Y.Doc von Space B
{
  type: "item-ref",
  itemId: "uuid-des-items",
  homeSpaceId: "space-a-id",
}
```

Der referenzierende Space zeigt das Item an, indem er die Daten aus dem Heim-Space liest. Änderungen im Heim-Space sind automatisch in allen Referenzen sichtbar.

### Multi-Owner

Ein Item kann **mehrere Owner** haben. Owner werden am Item selbst gespeichert (im Heim-Space Y.Doc), nicht am Space.

```
// Im Y.Doc von Space A (Heim-Space)
{
  id: "uuid-des-items",
  owners: ["did:key:agnes", "did:key:michaela", "did:key:markus"],
  // ... weitere Item-Daten
}
```

- Jeder Owner kann das Item bearbeiten, unabhängig davon in welchem Space er aktiv ist
- Owner können andere Owner einladen
- Der ursprüngliche Ersteller kann Owner entfernen

### Sichtbarkeit

Items haben ein Sichtbarkeits-Flag:

- **privat** — nur im Heim-Space sichtbar, nur für Space-Mitglieder
- **space** — nur im Heim-Space sichtbar, für alle Space-Mitglieder
- **öffentlich** — kann von anderen Spaces referenziert und auf der öffentlichen Karte angezeigt werden

Nur öffentliche Items können von anderen Spaces referenziert werden.

### Discovery

Öffentliche Items werden über den bestehenden **Profiles-Service** auffindbar gemacht. Jeder Space kann seine öffentlichen Items dort registrieren. Andere Spaces können nach Items in einer Region, einer Kategorie oder einem Stichwort suchen.

Alternativ: Ein neuer Discovery-Endpunkt, der öffentliche Items aggregiert. Das ist eine Implementierungsentscheidung, kein Architektur-Thema.

### Relationen

Item-Relationen (z.B. Projekt → Events) funktionieren innerhalb des Heim-Space wie bisher. Cross-Space-Relationen (ein Item in Space A hat ein Event in Space B) sind explizit **nicht Teil dieses RFC** — das ist eine zukünftige Erweiterung.

## Beispiel-Flow

1. Agnes erstellt das Item "Transition Town Stuttgart" in ihrem Space (= Heim-Space)
2. Agnes setzt Sichtbarkeit auf "öffentlich"
3. Agnes lädt Michaela als Owner ein
4. Michaela akzeptiert — sie kann das Item jetzt bearbeiten
5. Die Transition Town Stuttgart gründet einen eigenen Space
6. In diesem Space erstellen sie eine Referenz auf das Item
7. Das Item erscheint in beiden Spaces — eine Quelle, keine Kopie
8. Michaela ändert die Beschreibung → sichtbar überall
9. Der Real Life Circle Stuttgart referenziert das Item ebenfalls → drei Spaces, ein Item

## Technische Überlegungen

### Y.Doc Zugriff über Space-Grenzen

Wenn Space B ein Item aus Space A referenziert, muss Space B die Daten lesen können. Optionen:

**A) Direkter Y.Doc Zugriff:** Space B bekommt Lesezugriff auf das Y.Doc von Space A (oder einen Teil davon). Problem: Granularität — man müsste einzelne Items freigeben, nicht das ganze Doc.

**B) Sync-Schicht:** Öffentliche Items werden in ein separates Y.Doc oder einen REST-Endpunkt gespiegelt. Referenzierende Spaces lesen von dort. Entkopplung von der internen Space-Struktur.

**C) Profiles-Service erweitern:** Der bestehende Profiles-Service hält öffentliche Item-Daten vor. Referenzen lesen von dort. Einfachste Lösung, aber Latenz bei Updates.

**Empfehlung:** Option B oder C als MVP, Option A als langfristige Lösung. Die Entscheidung ist eine Implementierungsdetail und kann separat getroffen werden.

### Owner-Berechtigungen

Owner müssen schreibend auf das Y.Doc des Heim-Space zugreifen können, auch wenn sie nicht Mitglied des Heim-Space sind. Das erfordert eine Änderung am Berechtigungsmodell: Item-Level-Zugriff zusätzlich zu Space-Level-Zugriff.

### Performance

Bei tausenden öffentlichen Items braucht die Karte Pagination, Clustering und Lazy Loading. Der CrossSpaceIndex ist ein Anfang, muss aber für diese Größenordnung skaliert werden.

## Alternativen

### Item-Kopien statt Referenzen

Jeder Space hält eine eigene Kopie des Items. Sync per CRDT oder manuell.

Verworfen weil: Inkonsistenz bei Änderungen, kein klarer Owner, Konflikte bei gleichzeitiger Bearbeitung in verschiedenen Spaces.

### Kein Heim-Space — Item lebt global

Items existieren außerhalb von Spaces in einem globalen Pool.

Verworfen weil: Widerspricht der Space-als-Grundeinheit-Architektur. Unklar wer das globale Doc pflegt. Berechtigungen werden komplex.

### Nur über Profiles-Service

Items existieren nur im Profiles-Service, Spaces zeigen sie nur an.

Verworfen weil: Zentralisiert die Datenhaltung. Offline nicht verfügbar. Widerspricht Local-First-Prinzip.

## Offene Fragen

1. **Heim-Space wechseln:** Kann ein Item seinen Heim-Space wechseln? Z.B. wenn die Transition Town einen eigenen Space gründet und das Item "zu sich holen" will?

2. **Referenz-Berechtigung:** Kann jeder ein öffentliches Item referenzieren? Oder muss der Owner zustimmen?

3. **Löschung:** Was passiert mit Referenzen, wenn das Item im Heim-Space gelöscht wird?

4. **Offline:** Wie funktionieren Referenzen offline? Wird ein Cache vorgehalten?

5. **Migration:** Wie werden bestehende Items migriert? Braucht es einen Migrationspfad?
