# Flutlicht Manager – App-Version

Saison 1994/95 mit allen Klubs der Bundesliga und 2. Bundesliga. Eigenständige Web-App: läuft offline, lässt sich auf Mac, iPhone und iPad wie eine App installieren.

## Inhalt

- `index.html` – das komplette Spiel
- `manifest.webmanifest` – Name, Farben, Symbole für die Installation
- `sw.js` – Offline-Cache
- `icons/` – App-Symbole

## Wichtig: HTTPS

Offline-Modus und Installation brauchen eine HTTPS-Adresse (Ausnahme: `localhost` auf demselben Rechner). Über `http://192.168.x.x` im WLAN läuft das Spiel zwar, aber nicht offline.

## Variante A: Mac mini mit Tailscale (empfohlen, privat)

Das Spiel enthält echte Vereins- und Spielernamen. Für den privaten Gebrauch ist das unproblematisch; eine öffentlich erreichbare Seite solltest du damit nicht betreiben.

Mac und iPhone im selben Tailnet:

```
cd ~/flutlicht-app
python3 -m http.server 8080
tailscale serve --bg 8080
```

`tailscale serve` zeigt die HTTPS-Adresse (`https://<macmini>.<tailnet>.ts.net/`), die nur in deinem Tailnet erreichbar ist. Nur auf dem Mac selbst reicht `http://localhost:8080`.

## Variante B: GitHub Pages

Achtung: GitHub-Pages-Seiten sind öffentlich, und die echten Namen stecken in `index.html` selbst (der Editor ändert nur deinen Spielstand). Für diese Variante besser die Version mit erfundenen Vereinen verwenden.

1. Neues Repository anlegen, z. B. `flutlicht`.
2. Den Inhalt dieses Ordners hochladen (`index.html` liegt im Hauptverzeichnis).
3. Settings → Pages → Branch `main`, Ordner `/ (root)` → Save.
4. Nach ein bis zwei Minuten: `https://<dein-name>.github.io/flutlicht/`

## Installieren

- **iPhone / iPad (Safari):** Teilen → „Zum Home-Bildschirm“.
- **Mac (Safari):** Ablage → „Zum Dock hinzufügen“.
- **Mac (Chrome):** Installieren-Symbol rechts in der Adresszeile.

Einmal online öffnen, danach läuft das Spiel offline.

## Spielstände

- Automatisch nach jedem Spieltag gespeichert, zusätzlich drei Speicherplätze unter **System**.
- Spielstände liegen pro Gerät. Zum Umziehen: **System → Als Datei sichern** (z. B. in iCloud Drive), auf dem anderen Gerät **Aus Datei laden**.
- Auf dem iPhone hat die installierte App einen eigenen Speicher, getrennt von Safari.

## Updates

Neue Version der Dateien hochladen und die App einmal online öffnen. Für ein sofortiges Update in `sw.js` die Zeile `const CACHE='flutlicht-v1'` hochzählen (`v2`, `v3` …).
