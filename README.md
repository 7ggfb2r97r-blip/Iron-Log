# Iron Log 🏋️

Ein Dark-Mode-Trainingstracker: Pläne erstellen, Workouts mit Gewicht/Sätzen/Wiederholungen/RIR loggen, Fortschritt pro Übung als Chart sehen, automatische Gewichts-Steigerungsvorschläge.

**Diese App ist eine einzige, komplett eigenständige `index.html`-Datei.** React, ReactDOM und der gesamte App-Code sind fest eingebettet — kein Build-Schritt, kein `npm install`, keine Internetverbindung zur Laufzeit nötig.

## Lokal öffnen

Einfach `index.html` doppelklicken bzw. mit dem Browser öffnen. Funktioniert auch offline (Flugmodus).

Deine Trainingsdaten werden im `localStorage` des jeweiligen Browsers gespeichert — sie bleiben also lokal auf dem Gerät/Browser, in dem du die Seite öffnest, und sind nicht mit anderen Geräten synchronisiert.

## Online über GitHub Pages bereitstellen

Damit du über eine Web-Adresse (z. B. von überall / vom iPhone) darauf zugreifen kannst:

### 1. Neues Repository auf GitHub anlegen
Auf [github.com/new](https://github.com/new) ein neues, leeres Repository erstellen (z. B. `iron-log`). **Kein** README/`.gitignore` mit anlegen lassen, da wir das schon lokal haben.

### 2. Dieses Projekt hochladen
Im Terminal, im Ordner mit `index.html` und dieser `README.md`:

```bash
git init
git add -A
git commit -m "Initial commit: Iron Log"
git branch -M main
git remote add origin https://github.com/DEIN-USERNAME/iron-log.git
git push -u origin main
```

(`DEIN-USERNAME` und den Repo-Namen entsprechend anpassen — die genaue Remote-URL zeigt dir GitHub direkt nach dem Anlegen des Repos an.)

### 3. GitHub Pages aktivieren
Im GitHub-Repo → **Settings** → **Pages** → unter „Build and deployment" als Source **„Deploy from a branch"** wählen → Branch **`main`**, Ordner **`/ (root)`** → **Save**.

Nach ein bis zwei Minuten ist die App erreichbar unter:
```
https://DEIN-USERNAME.github.io/iron-log/
```

Diese Adresse kannst du dann auf dem iPhone in Safari öffnen und per „Zum Home-Bildschirm" als App-Icon ablegen — ganz ohne AirDrop oder Dateien-App.

## Als echte PWA installieren (App-Icon, Splashscreen, sofortiges Offline-Laden)

Das Projekt enthält jetzt ein Manifest (`manifest.json`), eigene App-Icons (`icons/`, `apple-touch-icon.png`) und einen Service Worker (`sw.js`). Damit das funktioniert, **muss die App über HTTPS laufen** — Service Worker funktionieren aus Sicherheitsgründen nicht bei direkt geöffneten Dateien (`file://`). Das heißt: dieser Teil braucht die GitHub-Pages-URL aus Schritt 3 oben.

1. Die GitHub-Pages-URL (`https://DEIN-USERNAME.github.io/iron-log/`) **einmal mit Internetverbindung** in Safari öffnen. Dabei installiert sich der Service Worker im Hintergrund und cached die komplette App.
2. Teilen-Symbol → **„Zum Home-Bildschirm"**. Jetzt siehst du das eigene Plate-Icon (nicht mehr das Safari-Symbol) und beim Öffnen einen kurzen Splashscreen statt der Browser-Oberfläche.
3. Ab jetzt lädt die App beim Öffnen **sofort aus dem Cache**, auch ganz ohne Internet/im Flugmodus.

**Wichtig beim Aktualisieren:** Änderst du `index.html` künftig und pusht sie zu GitHub, merkt der Service Worker das automatisch beim nächsten Öffnen (im Hintergrund neu geladen, beim übernächsten Start aktiv). Falls eine Änderung partout nicht ankommt, in `sw.js` die Zahl in `CACHE_NAME` (z. B. `iron-log-v1` → `iron-log-v2`) hochzählen — das erzwingt einen kompletten Cache-Reset beim nächsten Laden.

⚠️ **Hinweis zu den Daten:** Da alles im `localStorage` des Browsers gespeichert wird, hat jede Kombination aus Browser + Gerät ihre eigene Historie. Öffnest du die GitHub-Pages-URL z. B. in Safari auf dem iPhone und später in Chrome am Mac, siehst du dort jeweils unterschiedliche Daten.

## Änderungen später aktualisieren

Nach jeder Anpassung an `index.html`:

```bash
git add -A
git commit -m "Beschreibung der Änderung"
git push
```

GitHub Pages aktualisiert sich danach automatisch (kurze Verzögerung von ein bis zwei Minuten).
