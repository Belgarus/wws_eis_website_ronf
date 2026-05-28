# 🍦 Eishändler-Portal — Prototyp

> Lokaler Klick-Prototyp für die Kundenpräsentation heute.
> Kein echtes Backend — reines Frontend mit Demo-Daten.

---

## Ziel

Der Prototyp soll zeigen wie die fertige Anwendung aussieht und sich anfühlt.
Alle vier Rollen sind durchklickbar. Daten sind hardcodiert.
Der Kunde soll durch jeden Flow navigieren können.

---

## Stack

| Schicht | Technologie | Warum |
|---|---|---|
| Framework | React + Vite | Schnellster Setup, HMR out of the box |
| Styling | Tailwind CSS + shadcn/ui | Moderne Komponenten, kein eigenes CSS schreiben |
| Routing | react-router-dom | Eine Route pro Rolle |
| Icons | lucide-react | Bereits in shadcn/ui integriert |
| Charts | recharts | Lagerbestand-Diagramm ohne Konfigurationsaufwand |
| Daten | Mock-Datei (JS) | Kein Backend nötig, alles lokal im Browser |

---

## Rollen & Routen

| Rolle | Route | Was diese Person sieht |
|---|---|---|
| Kunde | `/kunde` | Bestellmaske, Lagerbestand, Produktionsauftrag |
| Eishändlerin | `/admin` | Alle Bestellungen, Aktionen, CSV-Export, Telefonbestellung |
| Logistik | `/logistik` | Bestand je Standort, Bestandsaktualisierung, Lieferungen |
| Produktion | `/produktion` | Produktionsaufträge, Kapazität, Termine |

Der Login-Screen leitet je nach gewählter Rolle auf die passende Route weiter.
Es gibt keine echte Authentifizierung — ein Klick auf die Rolle reicht.

---

## Demo-Daten

Alle Daten leben in einer einzigen Mock-Datei im Projekt.
Sie enthält: Eissorten mit Preisen, Lagerbestände je Standort,
Bestellungen mit verschiedenen Statuswerten und die vier Demo-Nutzer.

Wichtig: Mindestens eine Eissorte hat Bestand 0 —
das löst im Demo den Produktionsauftrag-Flow aus.
Mindestens eine Bestellung hat den Status „in Produktion" —
das zeigt den vollständigen Lifecycle.

---

## Screens

### Login
Einstiegspunkt der Anwendung. Zeigt Logo und Appname.
Vier sichtbare Schnellzugriff-Buttons — einen pro Rolle.
Beim Klick wird die Rolle gespeichert und zur passenden Ansicht weitergeleitet.

### Kunden-Ansicht
Begrüßung mit Nutzername. Standort-Auswahl oben.
Tabelle aller Eissorten: Name, Preis, Lagerbestand als farbiges Badge,
Mengen-Eingabe pro Sorte. Darunter Datumswahl für den Liefertermin.
Absenden zeigt eine Erfolgsbenachrichtigung.
Sorten mit Bestand 0 sind gesperrt — dort erscheint stattdessen
ein Button zum Auslösen eines Produktionsauftrags.

### Admin-Ansicht (Eishändlerin)
Vier Kennzahl-Karten oben: Offene, Bestätigte, In Produktion, Gesamt.
Darunter die vollständige Bestelltabelle mit Status-Badge und Aktionen.
Aktionen pro Zeile: Bestellung bestätigen, CSV-Export auslösen.
Separater Button für Telefonbestellung — öffnet die komplette
Kunden-Bestellmaske als Modal, damit telefonische Bestellungen
direkt erfasst werden können.
Zweite Ansicht oder Tab: Balkendiagramm des Lagerbestands je Standort.

### Logistik-Ansicht
Standort-Selector oben — die Ansicht filtert sich entsprechend.
Bestandstabelle: Sorte, Menge, Status-Badge.
Pro Zeile: Button zum Aktualisieren des Bestands via Eingabe-Modal.
Zweite Karte: Anstehende Lieferungen für diesen Standort.

### Produktions-Ansicht
Liste aller Produktionsaufträge mit Status (angefragt / in Produktion / fertig).
Pro Auftrag: Sorte, Menge, Anfragedatum, Status.
Aktionen: Annehmen mit Datumsauswahl für den Fertigtermin, Ablehnen.
Darunter eine einfache Kapazitätstabelle für die nächsten vier Wochen.

### Geteiltes Layout
Feste Seitenleiste links mit Logo, rollenabhängiger Navigation und
Nutzerinformation unten. Auf der rechten Seite der Hauptinhalt.
Die Navigationspunkte passen sich automatisch an die eingeloggte Rolle an.

---

## Umsetzungsreihenfolge

Die Reihenfolge ist wichtig — spätere Screens bauen auf früheren auf.

**Schritt 1 — Projekt aufsetzen**
Neues Vite-React-Projekt erstellen, Tailwind und shadcn/ui initialisieren,
react-router-dom und lucide-react installieren.
Danach einmal starten und prüfen ob alles läuft.

**Schritt 2 — Mock-Daten anlegen**
Eine einzige Datei mit allen Demo-Daten erstellen: Eissorten, Standorte,
Lagerbestände, Bestellungen, Nutzer. Diese Datei ist der Ausgangspunkt
für alle weiteren Screens — sie muss zuerst fertig sein.

**Schritt 3 — Auth-Context**
Einen globalen React-Context für die aktuelle Rolle anlegen.
Kein echtes Login — nur ein State der speichert welche Rolle aktiv ist
und die Navigation entsprechend steuert.

**Schritt 4 — App-Layout und Router**
Das geteilte Layout mit Sidebar bauen und alle Routen verdrahten.
Noch ohne fertige Inhalte — die Seiten können erstmal leer sein.
Danach: Login-Screen mit den vier Schnellzugriff-Buttons.

**Schritt 5 — Kunden-Ansicht**
Die Bestellmaske ist der wichtigste Screen für die Demo.
Mit Lagerbestand-Badges, Mengen-Eingabe, Datumswahl und
dem Produktionsauftrag-Flow bei Nullbestand.

**Schritt 6 — Admin-Ansicht**
Kennzahl-Karten, Bestelltabelle mit Status-Aktionen, CSV-Export,
Telefonbestellung-Modal (wiederverwendet die Bestellmaske aus Schritt 5),
Lagerbestand-Diagramm.

**Schritt 7 — Logistik-Ansicht**
Standort-Filter, Bestandstabelle, Aktualisierungs-Modal,
Lieferungsübersicht.

**Schritt 8 — Produktions-Ansicht**
Auftragsübersicht, Annehmen/Ablehnen-Logik, Kapazitätstabelle.

**Schritt 9 — Feinschliff**
Farben vereinheitlichen, Übergänge prüfen, Demo-Flow einmal
komplett durchklicken und sicherstellen dass alle Status-Wechsel sichtbar sind.

---

## Design

Sauber und modern — passend zu einem professionellen B2B-Portal.

- Hintergrund hell, Karten weiß mit leichtem Schatten und abgerundeten Ecken
- Primärfarbe Teal (blau-grün) — passt zum Eisthema
- Status-Badges: grün für bestätigt, gelb/orange für offen, blau für in Produktion, rot für abgelehnt
- Lagerbestand-Badges: grün für ausreichend, gelb für niedrig, rot für kritisch, grau für Nullbestand
- Einheitliche Schrift, großzügige Abstände, keine überladenen Seiten

---

## Demo-Flow für die Präsentation

Diesen Flow beim Zeigen durchlaufen — etwa 5 Minuten, alle Kernfunktionen sichtbar:

1. Login-Screen öffnen — alle vier Rollen erklären
2. Als Kunde einloggen — Bestellmaske zeigen, Lagerbestände erklären
3. Bestellung aufgeben — Sorte wählen, Menge, Termin, absenden, Toast zeigen
4. Sorte mit Nullbestand anklicken — Produktionsauftrag-Button erklären
5. Zur Admin-Ansicht wechseln — neue Bestellung erscheint in der Tabelle
6. Bestellung bestätigen — Status-Wechsel zeigen
7. CSV-Export — Datei lädt herunter, WWS-Import erklären
8. Telefonbestellung — Modal öffnet, Direktmodus erklären
9. Zur Logistik wechseln — Bestand für einen Standort aktualisieren
10. Zur Produktion wechseln — Produktionsauftrag annehmen, Termin setzen

---

## Abgrenzung

Was der Prototyp zeigt aber nicht wirklich tut:

- Kein Mailversand — eine Erfolgsbenachrichtigung im Browser simuliert die Mail
- Kein echter CSV-Export — eine generierte Dummy-Datei reicht für die Demo
- Kein Datenbankzugriff — alle Zustandsänderungen leben nur im Browser-Memory
- Kein echter Login — Rollenwechsel per Klick

Was trotzdem echt wirkt:

- Alle Status-Wechsel sind live sichtbar
- Die Bestellmaske verhält sich wie die echte Anwendung
- Der Lagerbestand reagiert auf Eingaben
- Die Rollentrennung ist vollständig umgesetzt

---

*Prototyp · AFBB-fA Anforderungsmanagement · Mai 2026*
