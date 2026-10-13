# Flutlicht Manager – App-Version

Saison 1994/95 mit allen Klubs der Bundesliga und 2. Bundesliga. Eigenständige Web-App: läuft offline, lässt sich auf Mac, iPhone und iPad wie eine App installieren.

## Inhalt

- `index.html` – das komplette Spiel
- `manifest.webmanifest` – Name, Farben, Symbole für die Installation
- `sw.js` – Offline-Cache
- `icons/` – App-Symbole

## Wichtig: HTTPS

Offline-Modus und Installation brauchen eine HTTPS-Adresse (Ausnahme: `localhost` auf demselben Rechner). Über `http://192.168.x.x` im WLAN läuft das Spiel zwar, aber nicht offline.

## Hosting auf dem Mac mini (Tailscale)

Tailscale läuft dort schon für andere Apps. Damit deren Freigabe auf Port 443 erhalten bleibt, bekommt Flutlicht einen eigenen HTTPS-Port:

```
tailscale serve status
tailscale serve --bg --https=8443 ~/flutlicht-app
```

Danach: `https://<macmini>.<tailnet>.ts.net:8443/`. Mit `--bg` bleibt die Freigabe auch nach einem Neustart aktiv. Ist 8443 belegt, nimm 10000.

Das Spiel enthält echte Vereins- und Spielernamen. Für den privaten Gebrauch im Tailnet ist das unproblematisch; eine öffentliche Seite (z. B. GitHub Pages bei einem öffentlichen Repo) solltest du damit nicht betreiben.

## Installieren

- **iPhone / iPad (Safari):** Teilen → „Zum Home-Bildschirm“.
- **Mac (Safari):** Ablage → „Zum Dock hinzufügen“.
- **Mac (Chrome):** Installieren-Symbol rechts in der Adresszeile.

Einmal online öffnen, danach läuft das Spiel offline.

## Ton

Im Menü läuft eigene Chiptune-Musik, während der Spiele Stadionatmosphäre mit Gesängen, Klatschen, Torjubel und Schiedsrichterpfiff. Alles wird im Browser erzeugt, es gibt keine Audiodateien. Der Ton startet beim ersten Tippen (Browser-Vorgabe). ♪ oben rechts schaltet stumm.

## Spielstände

- Automatisch nach jedem Spieltag gespeichert, zusätzlich drei Speicherplätze unter **System**.
- Spielstände liegen pro Gerät. Zum Umziehen: **System → Als Datei sichern** (z. B. in iCloud Drive), auf dem anderen Gerät **Aus Datei laden**.
- Auf dem iPhone hat die installierte App einen eigenen Speicher, getrennt von Safari.

## Updates

Neue Version der Dateien hochladen und die App einmal online öffnen. Für ein sofortiges Update in `sw.js` die Zeile `const CACHE='flutlicht-v15'` hochzählen.
