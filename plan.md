## Ausgangssituation

Ein Eishändler wickelt Bestellungen bisher telefonisch und manuell ab.
Ein bestehendes Warenwirtschaftssystem (WWS) verwaltet Kunden und Aufträge —
hat aber **keine Verbindung** zu Lagerstandorten oder Produktion.

**Ziel:** Webanwendung, über die Kunden selbst bestellen können,
mit Echtzeit-Lagerblick und automatischer WWS-Übergabe.

---

## Rollen & Zugriff

| Rolle | Zugriff |
|---|---|
| **Kunde** | Bestellungen aufgeben, Lagerbestand einsehen, Produktionsauftrag auslösen |
| **Eishändlerin** | Admin-Vollzugriff + Bestellübersicht + WWS-Import + Telefonbestellung erfassen |
| **Logistik / Lager** | Eigene Bestände lesen, Bestandsänderungen melden |
| **Produktion** | Eingehende Aufträge sehen, Kapazität melden, Fertigtermin setzen |

---

## Anforderungen

### MUSS

- `LF-01` Kunde gibt Bedarfe ein
- `LF-02` Kunde löst Bestellung aus
- `LF-03` Bestellung auf definierten Liefertermin
- `LF-05` Produktionsauftrag bei Nullbestand auslösbar
- `LF-06` Eishändler erstellt Angebot manuell
- `LF-08` Bestand / Kapazität wird bei Eingang geprüft
- `LF-09` Eishändler-Login (interner Bereich)
- `LF-10` Übersicht aller offenen Bestellungen
- `LF-11` Import in WWS per Exportfunktion (CSV)
- `LF-14` Lieferbestätigung + Rechnung per Mail (automatisch)
- `LF-15` Angebot per Mail bei Produktionsauftrag (automatisch)

### SOLL

- `LF-04` Lagerbestand je Sorte und Standort sichtbar
- `LF-12` Telefonische Bestellungen direkt erfassbar (Direktmodus)
- `LF-13` Echtzeit-Verfügbarkeitsabfrage aus Lager und Produktion

### KANN

- `LF-07` Automatische Preiskalkulation (Folgeversion)

---

## Architektur

```
Browser (React)
    │
    ▼
REST API (Node.js / FastAPI)
    │
    ├── PostgreSQL (simuliert WWS + Bestellungen + Nutzer)
    │
    ├── Mock: Lagerstandorte (eigener Service / Tabelle)
    │
    ├── Mock: Produktion (eigener Service / Tabelle)
    │
    └── Mail-Dienst (SMTP / SendGrid)
```

> Das WWS wird nicht direkt angebunden.
> Ein CSV-Export simuliert den Import in ein echtes Warenwirtschaftssystem.

### Datenbankschema (vereinfacht)

| Tabelle | Inhalt |
|---|---|
| `users` | Kunden, Eishändler, Logistik, Produktion (mit Rolle) |
| `ice_types` | Eissorten mit Basispreis |
| `stock` | Bestand je Sorte und Standort |
| `production_capacity` | Kapazität je Sorte und Woche |
| `orders` | Bestellkopf (Kunde, Termin, Status) |
| `order_items` | Positionen (Sorte, Menge, Preis) |
| `production_orders` | Produktionsaufträge mit Termin und Status |

---

## Umsetzungsplan

### Phase 1 — Grundgerüst (Woche 1–2)

- [ ] Projekt aufsetzen (Repo, Linter, CI)
- [ ] Datenbankschema anlegen und mit Testdaten befüllen
- [ ] Authentifizierung mit Rollentrennung (JWT)
- [ ] Basis-API: Nutzer, Eissorten, Lagerbestand

### Phase 2 — Kernfunktionen (Woche 3–5)

- [ ] Bestellmaske für Kunden (`LF-01`, `LF-02`, `LF-03`)
- [ ] Lagerbestandsanzeige je Standort (`LF-04`, `LF-13`)
- [ ] Produktionsauftrag bei Nullbestand (`LF-05`)
- [ ] Admin-Bestellübersicht (`LF-10`)
- [ ] Bestandsprüfung bei Eingang (`LF-08`)

### Phase 3 — Integration & Kommunikation (Woche 6–7)

- [ ] Automatischer Mailversand: Bestätigung + Rechnung (`LF-14`, `LF-15`)
- [ ] Angebotserstellung durch Eishändler (`LF-06`)
- [ ] CSV-Export / WWS-Importfunktion (`LF-11`)
- [ ] Telefonischer Direktmodus (Erfassung in Kundenansicht) (`LF-12`)

### Phase 4 — Test & Abnahme (Woche 8–9)

- [ ] Funktionale Tests je Rolle
- [ ] Integrationstests (Lager → Bestellung → Mail)
- [ ] Abnahme mit Testprotokoll

### Phase 5 — Präsentation (Woche 10)

- [ ] Demo-Daten vorbereiten
- [ ] Rollendemo: Kunde → Eishändler → Logistik → Produktion
- [ ] Dokumentation finalisieren

---

## Testkriterien

| TC | Testfall | Erwartetes Ergebnis |
|---|---|---|
| TC-01 | Kunde bestellt vorrätige Sorte | Bestätigung gespeichert, Mail raus |
| TC-02 | Lagerbestand anzeigen | Korrekte Mengen je Standort |
| TC-03 | Sorte nicht verfügbar | Produktionsauftrag auslösbar |
| TC-04 | Eishändler-Login | Bestellübersicht sichtbar |
| TC-05 | WWS-Export | Vollständige CSV aller offenen Bestellungen |
| TC-06 | Telefonbestellung | Erfassung in Kundenansicht möglich |
| TC-07 | Lagerstandort offline | Fehlermeldung, kein Absturz |

---

## Offene Fragen

- [ ] Schnittstellenformat Lagerstandorte (REST? CSV-Polling?)
- [ ] Wer erstellt die Rechnung — API oder WWS?
- [ ] Mindest- / Maximalbestellmengen je Sorte?
- [ ] SLA: Reaktionszeit Eishändler auf neue Bestellungen?
- [ ] DSGVO: Datenschutzbeauftragter und Einwilligungskonzept?

---

## Stack (Vorschlag)

```
Frontend    React + Tailwind CSS
Backend     Node.js (Express) oder Python (FastAPI)
Datenbank   PostgreSQL
Auth        JWT + Rollentrennung
Mail        Nodemailer / SendGrid
Export      CSV-Generierung serverseitig
Hosting     Docker Compose (lokal) → ggf. Railway / Render
```

---

*Übungsprojekt · AFBB-fA Anforderungsmanagement · Stand Mai 2026*
