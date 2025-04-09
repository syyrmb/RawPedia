---
title: Supported Cameras fr
contributors:
  - Lebarhon
---

# Appareils photo supportés

Cette liste est en mise à jour permanente, si vous remarquez une erreur,
faites le nous savoir. Même si votre appareil photo n'est pas dans cette
liste, il peut être quand même supporté. Nous n'avons pas la possibilité
de tester tous les formats raw des différents modèles d'appareils photo.
Le meilleur moyen de vérifier est d'installer RawTherapee et d'essayer
d'ouvrir un fichier. Même si un fichier n'est pas supporté, dans bien
des cas il s'ouvrira tout de même car RawTherapee possède des décodeurs
de format pour la plupart des formats connus. Cependant, comme certains
formats propriétaires manquent d'informations disponibles concernant la
matrice des couleurs et le capteur, vous risquez d'observer des couleurs
délavées ou fausses et/ou un encadrement de pixels noirs ou décolorés.
Cela signifie que l'appareil photo n'est pas supporté mais peut assez
facilement le devenir en ajoutant quelques constantes soit dans le code
source ou bien dans le fichier texte
[camconst.json](http://50.87.144.65/~rt/w/index.php?title=Adding_Support_for_New_Raw_Formats/fr)

Si la colonne "Notes" ne détaille pas un support partiel, le support
complet est implicite. Si un fichier raw non supporté provoque le
plantage de RawTherapee, cela est indiqué par une coche dans la colonne
"Crash" (plantage). Si un appareil photo n'est pas listé, faites un
essai de RawTherapee et dites nous sur [notre page Google
Code](https://code.google.com/p/rawtherapee/issues/list) ou [notre
forum](http://rawtherapee.com/forum/) s'il fonctionne pour votre format
raw.

La plupart de ces appareils photo sont supportés depuis longtemps, mais
comme nous venons d'ajouter la colonne "Supported from" (supporté
depuis) seulement maintenant, cela pendrait trop de temps pour
rechercher quelle version a été la première à supporter tel appareil,
aussi la dernière version a été notée.

Le support des appareils Fujifilm avec le capteur X-Trans a commencé
avec RawTherapee version 4.2. Charger ces images avec des versions plus
anciennes mènera sans doute au plantage. Si pour une raison quelconque
vous ne pouvez pas mettre à jour vers 4.2, vous pouvez quand même les
traiter dans une version plus ancienne de RawTherapee en [les
convertissant en DNG
linéaire](How_to_convert_raw_formats_to_DNG/fr.md) avec la
dernière version de Adobe DNG Converter. Choisir le mode de
compatibilité "DNG 1.4" et "Linear (demosaiced)" (Linéaire (dématricé)).

| Fabricant et modèle | Extension(s) | Notes | Supportés depuis | Plantage |
|---------------------|--------------|-------|------------------|----------|
|                     |              |       |                  |          |

Liste de tous les appareil photos connus pour être supportés \|+
style="font-weight: normal; text-align: left;" \|

Note: Veuillez utiliser la [version
anglaise](Supported_Cameras.md) pour consultation et mise à jour
du tableau.

Note: Be kind enough to use [the English
version](Supported_Cameras.md) for board consultating and update
