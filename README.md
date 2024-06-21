# Initialisierung von Vue ohne lokale node-Installation

ACHTUNG: Die folgenden Aufgaben werden in einem leeren Projektverzeichnis ausgeführt!

Im Projektverzeichnis das folgende Kommando ausführen: 

`docker run -it --rm -v $(pwd):/app -p 5173:5173 -w/app  node:iron-alpine3.20 /bin/sh`

Dadurch befinde ich mich im in einem Node-Container im Stammverzeichnis. Das kann ich mit `ls -la` überprüfen. Hier kann ich jetzt die Basis-Installation meines Frontends mit Vite durchführen. Achtung, dadurch wird das Verzeichnis "frontend" (also "Project  name") gelöscht, falls es vorhanden sein sollte!

    npm create vue@latest

    ✔ Project name: … frontend
    ✔ Target directory "frontend" is not empty. Remove existing files and continue? … No / Yes
    ✔ Add TypeScript? … No / Yes
    ✔ Add JSX Support? … No / Yes
    ✔ Add Vue Router for Single Page Application development? … No / Yes
    ✔ Add Pinia for state management? … No / Yes
    ✔ Add Vitest for Unit Testing? … No / Yes
    ✔ Add an End-to-End Testing Solution? › No
    ✔ Add ESLint for code quality? … No / Yes
    ✔ Add Prettier for code formatting? … No / Yes
    ✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes

Jetzt kann ich die notwendigen Modules installieren und testweise einmal das Ergebnis ansehen.

    cd frontend
    npm install
    npm run format
    npm run dev -- --host

Durch die Angabe von `--host` wird das Ganze nach außen weitergereicht und ich kann mir die Vite-Standard-Installation ansehen:

    http://localhost:5173/

# Dockerisierung

In `compose.yaml` wählt man unter services:frontent:build das entsprechende target, entweder development-stage oder production-stage.

# Frontend

Anpassung in `package.json`: `"dev": "vite --host --port 80"`. Hier wurde "host" und "port" hinzugefügt.

# Backend

Das Backend habe ich erst einmal hiervon genommen: https://dev.to/fizy_hector/-containerizing-your-full-stack-node-app-using-docker-compose-4lnk