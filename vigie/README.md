# Vigie — ta voiture, en clair

Vigie est l'appli compagnon d'une voiture qui n'a pas d'appli constructeur. Elle lit la voiture avec un petit boîtier OBD2 Bluetooth BLE et dit en 3 secondes si tout va bien : autonomie, pneus, batterie, température, codes défaut, entretien, carnet de pleins et stations. L'assistant **Mécano** explique les voyants et les codes simplement.

Depuis la v0.13, Vigie a aussi un **mode autoradio** : l'interface 3D pour l'écran de la voiture décrite dans le business plan « Interface 3D et modernisation d'habitacle ».

## Ce qu'il y a dans ce dossier

| Fichier | Rôle |
|---|---|
| `index.html` | Toute l'appli (une seule page, sans étape de construction) |
| `changelog.json` | Les nouveautés, affichées dans Garage > Nouveautés |
| `roadmap.md` | La feuille de route et la carte du code |
| `manifest.webmanifest`, `sw.js`, `icon*.png`, `icon.svg` | L'appli installable et son mode hors ligne |
| `tests/check.py` | Le banc de test automatique |

## Mettre Vigie en ligne

1. Sur GitHub, ouvre **Settings > Pages** du dépôt.
2. Choisis la branche `main` et le dossier `/ (root)`, puis enregistre.
3. Après une minute, Vigie est à l'adresse `https://florentin2908.github.io/CV-BIONDI-Florentin-/vigie/`.

En ligne, tout ce que la page Claude bloque se met à marcher : ta position, la carte, les prix des carburants en direct, le boîtier Bluetooth (Chrome sur Android) et la caméra.

## L'installer comme une appli

- **Téléphone Android ou autoradio Android** : ouvre l'adresse dans Chrome, puis menu > « Installer l'appli ». Un appui long sur l'icône propose les raccourcis « Mode autoradio », « Ajouter un plein » et « Mécano ».
- **iPhone** : dans Safari, Partager > « Sur l'écran d'accueil ».
- Pour qu'un écran de voiture s'ouvre directement sur l'interface 3D : Garage > Écran de voiture > « Au démarrage de Vigie : ouvrir le mode autoradio », ou l'adresse `…/vigie/?mode=autoradio`.

## Le mode autoradio

- La voiture en 3D au centre (on la fait tourner du doigt), la vitesse et l'autonomie à gauche, les pneus, le moteur et la batterie à droite.
- De gros boutons : GPS (Google Maps), Waze, Spotify, téléphone, caméra de recul, stations ou bornes, bilan.
- Plein écran et écran gardé allumé quand le navigateur le permet.
- Sécurité : aucune vidéo, la caméra de recul se coupe dès que le boîtier voit la voiture rouler, et aucun bouton de verrouillage ou de climatisation (Vigie ne simule jamais une commande qu'elle ne peut pas faire).
- CarPlay et Android Auto restent des applis de l'écran : Vigie se place autour, jamais dedans.

## Tes données

Tout reste sur l'appareil (stockage du navigateur) : profil, pleins, carnet d'entretien, photo. Rien n'est envoyé ailleurs, sauf ta position aux services publics de prix des carburants quand tu ouvres la carte.

## Lancer le banc de test

```bash
npm install --prefix /tmp/vigie-deps three@0.160.0 leaflet@1.9.4
pip install playwright pillow
python3 tests/check.py . /tmp/vigie-out --deps /tmp/vigie-deps
```

Le banc démarre l'appli dans Chromium, remplit le premier lancement, note des pleins et des opérations d'entretien, change d'énergie et de scénario de démo, clique chaque bouton, ouvre le mode autoradio à plusieurs tailles d'écran et vérifie que rien ne déborde. Il écrit `report.json` et une planche de captures `contact.jpg`.

## Publier dans l'artefact Claude

La page Claude ajoute son propre squelette HTML. Avant de publier `index.html` dans l'artefact, retire la première ligne (`<!doctype html>…<body>`) et la dernière (`</body></html>`).
