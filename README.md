# Écran de salle, Au Fût et à Mesure

Boucle d'affichage pour la salle du bar (Salon-de-Provence). Cinq panneaux qui tournent
en continu, douze secondes chacun, à la charte relevée sur ses affiches.

Item 14 du catalogue du projet « Vendre de l'automatisation aux commerçants locaux ».
Le contexte, la faisabilité et les décisions vivent dans la note du coffre personnel,
`1 PROJETS/Vendre de l'automatisation aux commerçants locaux/Ecran du bar - Au Fut/`.

## Les deux fichiers

- `index.html` : la page. Aucune dépendance à installer, un navigateur suffit.
- `evenements.json` : **les données, et le seul fichier à toucher.**

La page relit `evenements.json` toutes les dix minutes et remonte ses panneaux sans rechargement. Mettre à jour la prog du bar
se fait donc en éditant ce seul fichier, sans toucher ni à la page ni à l'écran du bar.

## Mettre à jour la prog

Éditer `evenements.json`, committer, pousser. L'écran suit dans les dix minutes.

- `matchs` : les matchs diffusés. Mêmes données que le lot d'affiches « jour de match ».
- `soirees` : les soirées du bar. `exemple: true` affiche le marqueur « Exemple » sur
  la page, à retirer quand la date est confirmée.
- `classement` : la ligue de fléchettes. `exemple: true` tant qu'il n'est pas lu
  depuis la source réelle.
- `inscription` : la destination du QR.

**Ce qui n'est pas sourcé porte `exemple: true` et s'affiche comme tel.** Les 9 matchs
sont réels, recoupés le 23/10/2026 sur L'Équipe, Footamax et la billetterie de l'OM.
Les familles de soirées sont réelles, relevées sur sa production de février à octobre
2026, mais leurs dates sont des emplacements tant que sa prog du mois n'est pas relevée.

## Comment ça tourne au bar

Un boîtier HDMI derrière une de ses TV, piloté par un logiciel d'affichage qui ouvre
cette URL en plein écran, la rafraîchit, allume et éteint l'écran aux horaires voulus,
et sait basculer la source HDMI entre cette boucle et le décodeur les soirs de match.
Le détail du montage et son coût sont dans la note de livraison du coffre.

## Tester en local

    python -m http.server 8731
    # puis http://127.0.0.1:8731/

Un simple double-clic sur `index.html` ne suffit pas : le navigateur refuse de lire
`evenements.json` depuis `file://`. Il faut le servir en HTTP.
