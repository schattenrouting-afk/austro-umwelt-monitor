# austro-umwelt-monitor

Interaktive Österreich-Karte für Wetter-, Luft- und Pollenbelastung – **Bezirke + Städte**.  
Frontend läuft auf **GitHub Pages**, Daten kommen aus **Google Apps Script + Google Sheets** (JSONP) und ein **Bezirks-GeoJSON** wird on-the-fly aus Google Drive ausgeliefert.

## Live
- **Website:** https://schattenrouting-afk.github.io/austro-umwelt-monitor/

## Was kann die Karte?
- Bezirksflächen (Choropleth) basierend auf aktuellen Stadtwerten im Bezirk
- Städte als Marker mit Popup (Werte + Warnstufen + Maßnahmen)
- Umschaltbar zwischen Wetter-, Luft- und Pollenkennzahlen sowie Warnstufen
- Orts-/Stadtsuche (Zoom)
- Labels (Ortsnamen) erscheinen erst ab einer definierten Zoom-Stufe

## Datenquelle / Architektur
Dieses Repo enthält **nur das Frontend** (`index.html`).

Die Daten kommen aus einem Google Apps Script WebApp-Endpunkt (JSONP), u.a.:
- `action=meta` – verfügbare Felder
- `action=cache` – kompakte Datenzeilen für alle Städte (inkl. lat/lon)
- `action=cities` – Liste der Städte
- `action=measures` – Maßnahmen-Texte je Kategorie/Warnstufe
- `action=bezirke_geojson` – GeoJSON der österreichischen Bezirke (aus Google Drive)

**Warum GeoJSON über GAS?**  
Das Bezirks-GeoJSON ist zu groß für „einfaches Repo-Upload“ (Browser-Limit). Daher wird es aus Google Drive über Apps Script ausgeliefert und im Frontend geladen.

## Deployment
Deployment erfolgt automatisch über **GitHub Pages**:
- Branch: `hauptsächlich` (main)
- Ordner: `/ (Wurzel)`
- Entry Point: `index.html`

Änderungen am Frontend:
1. `index.html` im Repo bearbeiten oder neue Version hochladen
2. Commit ausführen
3. GitHub Pages baut automatisch neu (meist innerhalb von Sekunden)

## Lokale Nutzung
Du kannst `index.html` lokal öffnen (z.B. per Doppelklick).  
Empfohlen ist ein kleiner lokaler Server (z.B. VS Code Live Server), damit du konsistente Pfade/Loads testest.

## Konfiguration (im index.html)
Wichtige Stellen:
- `GAS_WEBAPP_URL` – URL der Google Apps Script WebApp
- `CITY_LABEL_MIN_ZOOM` – ab welcher Zoom-Stufe Ortslabels angezeigt werden

## Hinweise
- Die Flächenfarben pro Bezirk werden aus Stadtwerten innerhalb des Bezirks abgeleitet (z.B. Worst Case / Durchschnitt).
- In Gebirgs- und Tallagen kann es lokal zu Abweichungen kommen (Topografie).

## Tech-Stack
- Leaflet (Karten-Rendering)
- Turf.js (Point-in-Polygon / Geometrie)
- GitHub Pages (Hosting)
- Google Apps Script (JSONP API + GeoJSON-Auslieferung)
- Google Sheets (Cache/Measures als Datenspeicher)

## Lizenz
Private Nutzung / Prototyp (bei Bedarf hier anpassen).
