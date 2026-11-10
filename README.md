# Mises à jour en ligne de l'horloge à billes

Ce dossier est à publier tel quel sur un site statique en HTTPS. GitHub Pages convient et il est gratuit.
Chaque horloge lit `manifest.json` une fois par jour, et aussi quand on appuie sur « Vérifier maintenant » dans sa page de réglage.

## Adresse
Les horloges lisent : https://horlogef1.github.io/Horloge-billes/manifest.json
(GitHub Pages, branche `main`, dossier `/`). C'est la valeur de `MANIFESTE_USINE` dans `horloge_billes.ino`.

## Ajouter ou changer une carte pilote
- Mets le PNG de 240 × 240 dans `cartes/CODE.png`. Le code est celui des résultats officiels, en 3 lettres, par exemple `CAM.png`.
- Ajoute ou modifie sa ligne dans `cartes` avec `"v"` **augmenté de 1**. Une horloge ne télécharge une carte que si sa version augmente.
- Les cartes déjà intégrées au programme (photos_pilotes.h) n'ont pas besoin d'être listées. Le fichier en contient pourtant les 23 à la version 1 : c'est inoffensif (chaque horloge les télécharge une fois) et il suffit de passer à `"v": 2` pour remplacer l'une d'elles.

## Publier une nouvelle version du programme
1. Dans `horloge_billes.ino`, augmente `VERSION_PROGRAMME` (et `VERSION_TEXTE`).
2. Dans l'IDE Arduino : Croquis > Exporter les binaires compilés. Prends `horloge_billes.ino.bin`, **pas** le fichier `merged` ni `bootloader`.
3. Copie ce fichier dans `firmware/horloge_billes.bin`.
4. Dans `manifest.json`, mets `"version"` à la même valeur que `VERSION_PROGRAMME`.
5. Pousse. Les horloges qui ont « installer automatiquement » coché se mettent à jour d'elles-mêmes. Pour les autres, un bouton « Installer » apparaît sur leur page.

Avant de publier, teste toujours le .bin sur ta propre horloge : onglet Mises à jour > « Installer ce fichier ».
Un programme qui ne démarre plus ne peut pas se réparer à distance, il faudrait alors le câble USB.

## Si un service F1 change
Change `api_f1` ou `api_pilotes` (adresses en https://), puis pousse.
Si le nouveau service renvoie ses données dans un autre format, il faut aussi une nouvelle version du programme.
