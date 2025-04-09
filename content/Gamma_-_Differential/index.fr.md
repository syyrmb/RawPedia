---
title: Gamma - Differential fr
contributors:
  - Jdc
  - Lebarhon
---

<div class="pagetitle">

Gamma - Différentiel

</div>

## Généralités

Les courbes tonales sont un des points clefs de tous les logiciels de
traitement d'image. RawTherapee n'échappe pas à la règle...et on peut
même dire que l'utilisateur est comblé (peut-être y en a-t-il trop ?)par
le nombre et le type de courbes présentes aussi bien en mode RGB,
L\*a\*b\*, CIECAM,...

Le débat est souvent de savoir - ainsi d'ailleurs que pour les profils
"Input" (matrice, ICC, DCP...) - que recherche-t-on et sur quoi agit-on
? Traditionnellement on agit sur la luminance L (L\* de L\*a\*b\*), ou Y
(Y de XYZ), ou L équivalent reconstruit à partir des valeurs RGB, etc.
Bien sûr les utilisateurs et programmeurs sentent bien qu'il y a un truc
! Il suffit de lire les débats sur les forums...Chacun essaie d'apporter
sa pierre à l'édifice, en proposant diverses options - combinant ou non
avec la composante couleur - comme par exemple l'introduction d'une
échelle logarithmique, ou un modèle d'apparence coloré.

### Proposition

- La gestion des couleurs (Color Management) - LCMS dans le cas de
  RawTherapee - met à disposition du programmeur, et de l'utilisateur,
  des outils performants pour manipuler les données.
- Ces outils sont utilisés :

1.  Au démarrage du processus par l'attribution d'un profil d'entrée
    (input) de type matrice, ICC ou DCP
2.  Lors de la conversion des valeurs enregistrées sur le capteur en
    données utilisables par le processus principal, dans un espace de
    travail (sRGB, Adobe, ...Prophoto), juste avant le processus de
    traitement de l'image
3.  En final pour convertir ces données à diverses fins (écran, Web,
    impression,...), vers un espace de sortie.

Bien sûr, 1 2 et 3 doivent faire l'objet d'améliorations pour rendre
Rawtherapee plus performant, mais l'objet de cette proposition est
nouveau par l'introduction de la gestion des couleurs au milieu du
processus afin de permettre:

- des modifications tonales qui prennent en compte la gestion des
  couleurs (primaires, gamma, TRC) et pas seulement les variations de
  luminance.
- une action différenciée à l'intérieur d'une partie du process afin de
  renforcer ou atténuer les actions s'attachant à la luminance, sans
  modifier globalement les traitements.

## Méthodes

Plusieurs méthodes sont à votre disposition:

### Standard (Relative ICC)

- Applique un profil ICC, au-dessus des paramètres en cours ("gamma
  sRGB" qui est le paramètre par défaut de Rawtherapee)
- Ce profil, utilise les primaires de l'espace de travail courant, et
  applique un gamma et une TRC sur les données RGB situées après la
  conversion RGB et la balance des blancs, pour chaque canal Rouge -
  Vert - Bleu. Ce qui induit un changement des valeurs RGB pris en
  compte dans les processus qui mettent en œuvre directement ces données
  ou dans les valeurs L\*a\*b\* qui en sont déduites
- Vous pouvez agir - de manière relative - sur le gamma de 0.5 à 3.0, et
  sur la pente (slope) de 0.0 à 20.0
- Tous les processus non-raw sont concernés. Sont donc exclus :
  Demosaicing, Raw Black et White points, Preprocessing, Chromatic
  aberration, Dark Frame, Flat field, Retinex, Noise Reduction, White
  Balance, Crop, Resize, Lens/Geometry, Distorsion, Vignetting,...

### Standard (Absolute ICC)

- Applique un profil ICC, sur des données desquelles a été "soustrait"
  le gamma original ("gamma sRGB")
- On pourrait penser que cette méthode est une sorte de "softproofing";
  c'est presque le cas...mais il y aura des différences, car la
  transformation est faite en début de processus et non à la fin.
- Ce profil, utilise les primaires de l'espace de travail courant (sauf
  si "use output profile instead of working" est cochée), et applique un
  gamma et une TRC sur les données RGB situées après la conversion RGB
  et la balance des blancs,pour chaque canal Rouge - Vert - Bleu. Ce qui
  induit un changement des valeurs RGB pris en compte dans les processus
  qui mettent en œuvre directement ces données ou dans les valeurs
  L\*a\*b\* qui en sont déduites
- Vous pouvez agir - de manière absolue - sur le gamma de 0.5 à 3.0, et
  sur la pente (slope) de 0.0 à 20.0 et ainsi cerner des rendus
  spécifiques
  - Linéaire : gamma=1.0
  - BT-709 : gamma=2.22 slope=4.5
  - sRGB: gamma=2.4 slope=12.92
  - Adobe : gamma=2.2 slope=0.0
  - Prophoto : gamma=1.8 slope=0.0
  - etc.
- Tous les processus non-raw sont concernés (identique à Relative ICC)

<!-- -->

- Si vous activez "use output profile instead of working", le profil de
  sortie sera appliqué - les curseurs gamma et slope sont désactivés -
  (attention seule l'option "Output profile" avec Output gamma = default
  et Free gamma non activé est prise en compte)

===Standard (Absolute ICC g=1 + end)===

- on soustrait aux données le gamma original ("gamma sRGB") tout au
  début du processus RGB.
- puis on applique un profil ICC, à la fin du processus RT...juste avant
  la conversion vers TIFF/JPG.
- Si vous choisissez un gamma=2.40 et slope=12.92, ceci revient à ce que
  l'ensemble du processus RGB + L\*a\*b\* est traité en mode linéaire
  (sans gamma).Remarque : on aboutit au même résultat avec "RGB +
  L\*a\*b\* differential (ICC)" et gamma=0.417 slope=12.92.
- Tous les processus non-raw sont concernés (identique à Relative ICC)
- mêmes options et remarques que "Absolute ICC".

### RGB differential (Only gamma)

- Applique un gamma, au-dessus des paramètres en cours pour une partie
  du process RGB, puis à la fin de ce process applique un gamma inverse
- amène une action différenciée à l'intérieur d'une partie du
  process(ici RGB) afin de renforcer ou atténuer les actions s'attachant
  à la luminance, sans modifier globalement les traitements.
- J'ai mis en place ce mode en partie à des fins pédagogiques pour
  montrer la différence entre une application d'un gamma et son inverse,
  avec la méthode suivante (RGB + L\*a\*b\* differential ICC). La
  méthode "RGB differential Only gamma" peut introduire des artefacts
  lors d'actions importantes sur les curseurs.
- Si tous les réglages du process RGB sont à zéro (ou neutre) ou les
  courbes non activées, cette double conversion est sans effet. Par
  contre si un réglage est activé, il sera amplifié ou réduit selon les
  réglages choisis de gamma et de pente (slope)
- Vous pouvez agir - de manière différentielle - sur la gamma de 0.5 à
  3.0 (des valeurs réduites vers 0.7 et 2.5 sont recommandées afin de
  limiter les artefacts) et la pente.
- les processus suivants sont concernés : Exposure, Channel Mixer, HSV
  equalizer, RGB Curves, Color Toning

### RGB + L\*a\*b\* differential (ICC)

- Applique un profil ICC, au-dessus des paramètres en cours et applique
  un profil ICC inverse à la fin du processus général de Rawtherapee,
  juste avant la conversion vers le profil de sortie (sortie TIFF,
  JPG,...)
- amène une action différenciée à l'intérieur d'une partie du process
  (ici RGB + L\*a\*b\*) afin de renforcer ou atténuer les actions
  s'attachant à la luminance, sans modifier globalement les traitements.
- Ce profil, utilise les primaires de l'espace de travail courant, et
  applique un gamma et une TRC sur les données RGB situées après la
  conversion RGB et la balance des blancs, pour chaque canal Rouge -
  Vert - Bleu et un dispositif inverse à la fin du processus général. Ce
  qui induit un changement des valeurs RGB et L\*a\*b\* pris en compte
  dans les processus qui mettent en œuvre ces données.
- Ce processus présente l’inconvénient, par rapport à "RGB
  differential", d'accroître notablement les temps de traitement, mais
  dans les cas extrêmes il produira moins d'artefacts.
- Si tous les réglages du process RGB et L\*a\*b sont à zéro (ou neutre)
  ou les courbes non activées, cette double conversion est sans effet.
  Par contre si un réglage est activé, il sera amplifié ou réduit selon
  les réglages choisis de gamma et de pente (slope).
- On pourra ainsi différencier profondément le traitement de l'image
  selon la gamma choisi, renforcer un traitement pour les ombres, ou les
  hautes lumières, etc.
- Tous les processus non-raw sont concernés (identique à Relative ICC)
