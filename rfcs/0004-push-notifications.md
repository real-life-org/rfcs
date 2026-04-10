# RFC-0004: Push Notifications mit UnifiedPush

- **Autor:** Anton Tranélis
- **Datum:** 2026-04-08
- **Status:** Draft

## Zusammenfassung

Push Notifications für die Web-of-Trust-App über UnifiedPush — einen offenen, dezentralen Standard der ohne Google-Abhängigkeit funktioniert. Ein Code-Pfad für F-Droid und Play Store. ntfy als selbst-gehosteter Push-Server. Push dient nur zum Wecken der App — Nachrichteninhalte bleiben Ende-zu-Ende verschlüsselt über das bestehende Relay.

## Motivation

Aktuell erfährt ein User erst von neuen Verifizierungen, Bestätigungen oder Space-Einladungen wenn er die App öffnet. Das Relay puffert Nachrichten zuverlässig, aber es gibt keinen Mechanismus um den User aktiv zu benachrichtigen.

Push Notifications lösen das — und sie sind Voraussetzung für zukünftige Features wie Chat in Spaces.

### Was Push auslöst

1. **Neue Verifizierung** — Jemand hat dich verifiziert
2. **Neue Bestätigung** — Jemand hat eine Attestation über dich erstellt
3. **Space-Einladung** — Du wurdest in einen verschlüsselten Space eingeladen
4. **Space-Aktivität** — Neue Inhalte in einem Space (opt-in pro Space)

### Warum nicht Google FCM?

- FCM ist proprietär und inkompatibel mit F-Droid
- FCM erfordert Google Play Services (nicht auf GrapheneOS, LineageOS etc.)
- Google sieht Metadaten (wer bekommt wann Push)
- Zwei Code-Pfade (FCM + Alternative) statt einem

## Vorschlag

### UnifiedPush als Standard

UnifiedPush ist ein offener Standard der Google als Mittelsmann ersetzt. Statt einer permanenten Verbindung zu Google hält ein **Distributor** auf dem Gerät die Verbindung zu einem Push-Server deiner Wahl.

### Architektur

```
Sender → Relay (WebSocket) → Empfänger offline?
                              → Queue (wie bisher)
                              → HTTP POST an Push-Endpoint
                              → ntfy Server
                              → Distributor auf dem Gerät
                              → App wacht auf
                              → App verbindet sich mit Relay
                              → Relay liefert verschlüsselte Nachrichten aus
```

### Komponenten

#### 1. ntfy als Push-Server

ntfy ist ein leichtgewichtiger, Open-Source Push-Server. Läuft als Docker-Container neben dem Relay auf unserem Server.

- Selbst-gehostet auf `ntfy.utopia-lab.org`
- Empfängt HTTP POST vom Relay
- Hält Verbindungen zu den Geräten
- Unterstützt das UnifiedPush-Protokoll

#### 2. Distributor auf dem Gerät

Der Distributor ist das Gegenstück zu Google Play Services — er hält die Verbindung zum Push-Server. Drei Optionen:

| Option | Beschreibung | Zielgruppe |
|--------|-------------|------------|
| **Embedded** | Die WoT-App verbindet sich direkt mit ntfy. Kein Extra-App nötig. | Alle User (einfachstes Onboarding) |
| **ntfy App** | User installiert die ntfy-App als Distributor. Batterie-effizienter. | Power-User, De-Googled Geräte |
| **gCompat-UP** | Distributor der intern FCM nutzt. Für Google-Geräte ohne Extra-App. | User auf Standard-Android |

Empfehlung: **Embedded als Default** (kein Onboarding-Overhead), mit Option für externe Distributoren.

#### 3. Relay-Erweiterung

Der Relay weiß bereits ob ein User offline ist (WebSocket-Connection Map + Offline Queue). Erweiterungen:

**Neues Schema:**
```sql
CREATE TABLE push_endpoints (
  did TEXT PRIMARY KEY,
  endpoint_url TEXT NOT NULL,
  registered_at TEXT NOT NULL,
  last_push_at TEXT
)
```

**Neue Message-Typen:**
- `push-register` — App sendet ihren Endpoint nach dem Login
- `push-unregister` — App löscht ihren Endpoint

**Push-Trigger:** Wenn eine Nachricht in die Offline-Queue geht und ein Endpoint registriert ist → HTTP POST an den Endpoint.

**Rate Limiting:** Maximal ein Push alle 30 Sekunden pro DID. Verhindert Spam bei Nachrichtenschwemmen.

#### 4. Push-Payload

Minimaler Payload — kein Nachrichteninhalt, nur der Typ:

```json
{"wot": true, "t": "verification"}
```

Kein fromDid, kein Name, keine Details. Privacy bleibt gewahrt. Die App zeigt eine generische Notification: "Neue Verifizierung empfangen".

#### 5. App-Integration (Capacitor)

Neues natives Plugin `UnifiedPushPlugin` (analog zu BiometricKeystorePlugin):

- Android: `UnifiedPushReceiver` (BroadcastReceiver) + `UnifiedPushPlugin` (Capacitor Bridge)
- TypeScript: `PushService.ts` — `register()`, `unregister()`, `onPushReceived()`
- Registration nach Relay-Connect: Endpoint an Relay senden
- Bei Push-Empfang: Relay reconnecten → Nachrichten abholen

### iOS

UnifiedPush auf iOS funktioniert **nur** über einen APNs-Proxy. Apple erlaubt keine anderen Background-Push-Mechanismen.

ntfy kann als APNs-Gateway fungieren, erfordert aber:
- Apple Developer Account (99$/Jahr)
- APNs Push Certificate/Key
- Push Notifications Capability in Xcode

**Empfehlung:** iOS-Push als Phase 2. Für Phase 1 funktioniert iOS weiterhin mit Auto-Reconnect beim Öffnen der App.

### Space-Aktivität (Opt-In)

Für Push bei Space-Aktivität:
- Lokale Einstellung pro Space: "Benachrichtigungen für diesen Space"
- App sendet `push-subscribe-space` an Relay
- Relay speichert Space-Subscriptions
- Bei neuer Space-Nachricht: Push an alle Subscriber die offline sind

## Alternativen

### Google FCM

- Einfacher zu implementieren (Capacitor-Plugin existiert)
- Aber: proprietär, Google-Abhängigkeit, inkompatibel mit F-Droid, zwei Code-Pfade nötig
- Verworfen wegen Widerspruch zu unseren Werten (Dezentralität, Datensouveränität)

### WebSocket Keepalive

- App hält WebSocket zum Relay permanent offen
- Funktioniert nicht zuverlässig: Android Doze-Mode, Battery Optimization, iOS Background Restrictions
- Nur für Vordergrund-Nutzung geeignet (haben wir schon)

### Matrix Push

- Matrix hat ein eigenes Push-Gateway-Protokoll
- Wäre relevant wenn wir auf Matrix-Federation umsteigen
- Aktuell zu viel Overhead für unseren Anwendungsfall

### Polling

- App fragt regelmäßig den Relay: "Gibt es neue Nachrichten?"
- Batterie-intensiv, nicht echtzeitfähig
- Verworfen

## Offene Fragen

1. **Embedded vs. externe Distributor-App:** Embedded ist einfacher für User, aber hat höheren Batterieverbrauch. Sollen wir beides anbieten oder nur Embedded?

2. **Apple Developer Account:** Haben wir einen? Brauchen wir für iOS-Push und auch für den App Store. Wer registriert ihn?

3. **ntfy Server-Last:** Wie viele gleichzeitige Verbindungen kann ein ntfy-Container halten? Bei der aktuellen Nutzerzahl (10-100) kein Problem, aber skaliert es?

4. **Notification-UI:** Wie detailliert sollen Notifications sein? Nur "Neue Nachricht" oder "Neue Verifizierung von Anton"? Letzteres erfordert dass der Push den Absender-Namen enthält (Privacy-Tradeoff).

5. **Notification-Einstellungen:** Soll der User granular steuern können welche Push-Typen er bekommt? Oder erstmal alles-oder-nichts?

6. **Chat-Vorbereitung:** Push ist Voraussetzung für Chat in Spaces. Soll die Push-Architektur schon Chat-Nachrichten als Typ vorsehen?

## Implementierungsreihenfolge

1. **Server:** Relay-Erweiterung (push_endpoints Tabelle, push-register Handler, Push-Trigger)
2. **Server:** ntfy Deployment (Docker neben Relay)
3. **Android:** UnifiedPush Plugin + Receiver + PushService.ts
4. **Integration:** End-to-End Test
5. **iOS:** Phase 2 mit APNs (separater RFC oder Ergänzung)
