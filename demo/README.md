# Ice Cream Vendor Portal - Demo Anleitung

Dieses Verzeichnis enthält einen interaktiven HTML-Mockup für das "Ice Cream Vendor Portal".

## 🚀 Starten der Website

Da die Website das **Tailwind CSS Play CDN** nutzt, benötigt sie eine aktive Internetverbindung für das Styling. Um die Navigation zwischen den Seiten korrekt zu testen und mögliche Browser-Sicherheitsbeschränkungen (CORS) zu vermeiden, wird empfohlen, einen einfachen lokalen Server zu verwenden.

### Option 1: Python (Empfohlen, keine Installation nötig)
Öffne ein Terminal in diesem Ordner und gib ein:
```bash
python3 -m http.server 8000
```
Öffne dann im Browser: `http://localhost:8000/login.html`

### Option 2: VS Code Live Server
Falls du VS Code nutzt, kannst du die Erweiterung "Live Server" installieren und unten rechts auf "Go Live" klicken.

### Option 3: Direktes Öffnen
Du kannst die `login.html` auch direkt per Doppelklick öffnen, allerdings funktionieren dann relative Pfade in manchen Browsern restriktiver.

---

## 💡 Kurze Einführung in Tailwind CSS

Tailwind CSS ist ein "Utility-First" CSS Framework. Anstatt Klassen wie `.button` oder `.card` zu schreiben, nutzt man kleine, vordefinierte Klassen direkt im HTML.

**Beispiel aus diesem Projekt:**
```html
<div class="bg-white rounded-2xl shadow-xl p-8">...</div>
```
- `bg-white`: Hintergrund weiß
- `rounded-2xl`: Stark abgerundete Ecken
- `shadow-xl`: Großer Schatten-Effekt
- `p-8`: Padding (Innenabstand) von 2rem

**Vorteile für deine Demo:**
- **Keine CSS-Dateien:** Alles ist direkt im HTML sichtbar.
- **Schnelles Design:** Änderungen am Layout sind sofort durch das Ändern einer Klasse erledigt.
- **Kein Build-Schritt:** Durch das Play-CDN im `<head>` wird das CSS im Browser generiert.

---

## 🛠 Struktur des Mockups

1.  **`login.html`**: Einstiegspunkt. Wähle zwischen "Kunde" oder "Großhändler".
2.  **`customer-dashboard.html`**: 
    - Produktkatalog mit Detail-Modals.
    - Interaktiver Preisrechner (JavaScript berechnet Menge * Preis + 19% MwSt).
3.  **`vendor-dashboard.html`**: 
    - Liste simulierter Bestellungen.
    - Lagerbestandsanzeige mit Warnfarben bei niedrigem Bestand.
4.  **`confirmation.html`**: Bestätigungsseite nach einer Bestellung.

Viel Erfolg bei deiner Zusatzqualifikation!
