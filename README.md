# Comparateur de traces GPX — application installable

Cet outil (comparaison altimétrique, carte, météo, transports pour 2 traces GPX) est packagé en
**Progressive Web App (PWA)** : une fois déployé sur GitHub Pages, Chrome sur Android proposera
de l'installer comme une application, avec icône sur l'écran d'accueil et ouverture en plein écran
(sans barre d'adresse).

## Contenu du dossier

```
index.html          → l'outil (page principale)
manifest.json        → métadonnées de l'application (nom, icônes, couleurs)
sw.js                → service worker (rend l'app installable + cache l'interface)
icons/icon-192.png
icons/icon-512.png
icons/icon-maskable-192.png
icons/icon-maskable-512.png
```

## 1. Déployer sur GitHub Pages

1. Créez un nouveau dépôt sur GitHub (public), par ex. `gpx-comparateur`.
2. Ajoutez-y tous les fichiers de ce dossier **en conservant la structure** (le dossier `icons/`
   doit rester un sous-dossier à la racine, à côté de `index.html`).
   - Via l'interface web GitHub : "Add file" → "Upload files", glissez tout le contenu du dossier.
   - Ou en ligne de commande :
     ```
     git init
     git add .
     git commit -m "Comparateur GPX — première version"
     git branch -M main
     git remote add origin https://github.com/<votre-utilisateur>/gpx-comparateur.git
     git push -u origin main
     ```
3. Dans le dépôt GitHub : **Settings → Pages**.
   - Source : "Deploy from a branch"
   - Branch : `main`, dossier `/ (root)`
   - Enregistrez.
4. Attendez 1 à 2 minutes. L'outil sera accessible à :
   `https://<votre-utilisateur>.github.io/gpx-comparateur/`

## 2. Installer l'application sur Android (Chrome)

1. Ouvrez l'URL ci-dessus dans **Chrome** sur votre téléphone Android.
2. Chrome propose normalement automatiquement une bannière **"Ajouter à l'écran d'accueil"** /
   **"Installer l'application"**. Si elle n'apparaît pas :
   - Menu ⋮ (trois points en haut à droite) → **"Installer l'application"** (ou "Ajouter à
     l'écran d'accueil").
3. L'icône apparaît sur l'écran d'accueil et ouvre l'outil en plein écran, sans barre Chrome.

## À savoir

- L'outil reste **entièrement client** : aucune donnée n'est envoyée à un serveur autre que les
  API tierces déjà utilisées dans le navigateur (Open-Meteo pour la météo, Overpass/OpenStreetMap
  pour les transports, tuiles CARTO pour la carte).
- Le service worker met en cache l'interface (HTML/icônes) pour un démarrage rapide et une
  disponibilité minimale hors-ligne, mais la météo, les transports et la carte nécessitent une
  connexion internet active pour se charger.
- Pour mettre à jour l'application après une modification, changez le numéro de version dans
  `sw.js` (`CACHE_NAME = 'gpx-compare-v2'`, etc.) afin que les appareils déjà installés récupèrent
  la nouvelle version.
