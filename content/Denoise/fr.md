---
title: Denoise fr
contributors:
  - Jdc
---

<div class="pagetitle">

Comparaison des 3 outils Denoise de Rawtherapee

</div>

Comment fonctionnent et comment utiliser les divers outils « denoise »
de « Local adjustements »

## Préambule

Avant ces descriptions, il est important de rappeler comment est traité
le bruit dans « RT ». Il ne s'agit pas ici de remettre en cause la
documentation Rawpedia de « noise reduction » (detail tab) ou de l'outil
« denoise » dans « wavelet level », mais de la compléter par un
descriptif sommaire des algorithmes utilisés.

Dans RT on trouve plusieurs outils qui permettent de réduire le bruit :
Ceux situés dans la fonction initialement conçue par Emil Martinec en
2012 dans « Ftblockdn.cc »

- Wavelet en mode RGB
- Transformée de Fourier (DCT)

Et d'autres outils

- Guided Filter
- Medians
- Filtre Bilateral
- flous gaussien
- Dark Frame
- Hot Dead pixels

… Nous nous pencherons sur les 2 premiers ce cette liste : Wavelet,
Fourier.

## Le module original conçu par E.Martinec – 2008 – 2012

Il est composé de fonctions de base (Wavelet, DCT) qui peuvent être
appelées aussi d'autres programmes, c'est le cas pour « Wavelet level »
et « Local adjustments » Ces fonctions d'origine permettaient à
l'origine:

- le traitement « wavelet » :
  - agit de manière globale, c'est à dire identique pour tous les
    niveaux de décomposition, identique pour toute la plage de luminance
    ou de chroma
  - peut être utilisé en une ou deux passes (notion de « conservative »
    et « agressive » )
  - utilise une évaluation du bruit globale – par niveau de
    décomposition – se servant de « MAD » - « median absolute
    deviation »
- le traitement « Fourier » du bruit de luminance en utilisant la DCT
  (Discrete Cosinus Transform) pour traiter le bruit résiduel, égal à la
  différence entre l'image originale et l'image débruitée par wavelet

Ces 2 fonctions sont encadrées par un module général (Noise reduction –
detail tab) :

- - Utilisant la luminance et la chrominance de manière simple ; 1
    curseur pour chacun
  - Utilisant les « pavés » (tiles) de manière automatique aussi bien
    pour « wavelet » que « DCT » pour réduire les besoins en mémoire.

A noter que à l'origine (ainsi que dans Perfectraw...où je
« travaillais » avec E.Martinec et M.LLorens, le module « Denoise »
était en fin de processus.

## Les améliorations apportées aux fonctions d'origine – 2012 - 2020

Plusieurs améliorations ont été apportées par Ingo Weirich et Jacques
Desmis

1.  possibilité de débruiter par niveau de décomposition
2.  possibilité de débruiter au niveau de chaque pixel par la prise en
    compte de la luminance et de la chrominance
3.  possibilité d'étendre le traitement Fourier 'DCT' à la chrominance
4.  possibilité de mettre un seuil tenant compte de l'effet de bord à
    cette DCT (origine ART)

## Les améliorations apportées au module général (noise reduction – detail tab)

- calcul automatique des réglages de débruitage
- ajout de 2 courbes pour traiter plus finement les bruits de luminance
  et de chrominance – axe des 'y' amplitude, axe des 'x' intensité de la
  luminance ou de la chrominance
- possibilité d'utiliser le mode L\*a\*b\* au lieu du mode RGB
  - ajout du débruitage par medians

## L'ajout de "Debruitage par morceaux" - encore appelé "non-local means" (Local adjustments tab) - février 2021

- L'algorithme a pour origine Ipol (2014)
  [1](https://pdfs.semanticscholar.org/a262/269fa4b44b64d750c72fad3887f9d88817ce.pdf).
  Il a été porté sur ART par Albert Griggio, amélioré par Ingo Weirich.
  Jacques Desmis a assuré le portage sur Rawtherapee.
- Contrairement aux filtres habituels qui réalisent une moyenne des
  valeurs du groupe de pixels localisés autour d'un pixel cible afin de
  réduire le bruit, le filtre "non-local means" réalise une moyenne de
  la totalité des valeurs des pixels contenus dans l'image, pondérées en
  fonction de leur similarité avec le pixel cible. Le résultat d'un tel
  filtrage permet d’amoindrir la perte de détails au sein de l'image,
  comparé aux filtres réalisant des moyennes localement.

## Quelques remarques

Le débruitage est sujet à de nombreux débats souvent sujets aux
polémiques, ou querelles ou dogmes sur les méthodes et outils. Ma
position sur les sujets qui vont suivre est pragmatique...Ce qui est
important c'est le résultat final...

## Où situer le débruitage ?

Au début...ou à la fin du processus ? Chacun des modes à ses avantages
et inconvénients.

- Au début, le travail se fait en mode linéaire, mais ce mode ne tient
  pas compte des traitements postérieurs qui pourront faire croître le
  bruit ou son apparence (sharpening, exposition, saturation...) d'où
  une tendance à trop débruiter.
- A la fin, le travail se fait en mode non linéaire, il tient compte de
  tous les traitements...y compris des artefacts de bruit apparus avant
  ces traitements et amplifiés par ces traitements.
- L'idéal serait de combiner les 2 : un traitement « minimal » au
  « début », puis en final un traitement complémentaire.

## Mode RGB ou mode Lab ?

Chacune des méthodes a ses avantages et inconvénients là encore
pragmatisme.

- Le mode RGB linéaire « serait » supérieur notamment parce que
  l’évaluation du bruit « mad » serait meilleure...C'est oublier que
  notre œil, notre cerveau a pour le bruit les mêmes caractéristiques
  reprise que celles reprises dans les CAM (modèles d'apparence
  colorés) : le même niveau de bruit sera perçu différemment selon le
  fond noir, gris, blanc et sa coloration, sa saturation...
- Le mode « Lab » auquel il est nécessaire d'ajouter des outils de
  gestion du contraste et de la luminance (gamma, courbe, curseurs...)
  peut s'avérer dans de nombreux cas meilleur. De plus « Lab » semble
  plus discriminant pour le bruit de couleur.

## Combien de niveaux pour wavelet ?

- On dit souvent que seuls les 4 premiers niveaux sont utiles...Ceci est
  assez vrai pour le bruit de luminance en prenant en compte l'effet
  'CAM'
- Cependant si on agit pour la luminance sur les niveaux supérieurs on
  voit bien qu'il se passe quelque chose
- Pour le bruit de chrominance, les 4 premiers niveaux conviennent pour
  le bruit se traduisant par des pixels répartis colorés. Pour les
  paquets (blotches), ceux-ci ne pourront disparaître qu'en allant
  jusqu'au niveau 7

## Synthèse des outils

### Noise reduction (detail tab)

- pas de différentiation par niveau de décomposition
- différentiation par pixel au niveau de la luminance
- 5 niveaux de décomposition utilisés pour la luminance, 6 pour la
  chrominance
- DCT luminance seulement
- pas de seuil DCT
- Tiles automatique
- Possibilité de réglages automatiques

### Wavelet levels

- différentiation par niveau de décomposition pour Luminance et
  Chrominance (fine et coarse)
- différentiation par pixel au niveau de la luminance avec prise en
  compte de la teinte (hue)
- 6 niveaux de décomposition utilisés pour la luminance, 6 pour la
  chrominance
- différentiation utilisant le contraste local
- pas de DCT
- possibilités de tiles

### Local adjustements - et le débruitage par morceaux

- différentiation par niveau de décomposition pour Luminance et
  Chrominance (fine et coarse)
- différentiation par pixel au niveau de la luminance avec prise en
  compte de la teinte (hue)
- 7 niveaux de décomposition utilisés pour la luminance, 7 pour la
  chrominance
- DCT pour luminance et chrominance
- seuil DCT pour luminance et chrominance
- Récupération de tout ou partie de l'image originale non débruitée avec
  l'aide de masques
- Sélection différentielle « locale » (spot)
- utilisation du deltaE et des masques pour améliorer la sélection
  (spot).
- Utilisation des « excluding spot » pour « récupérer des zones
  bruitées »...(spot)
- pas de tiles : ceci a pour conséquence lorsqu'on travaille en « full
  image » et lorsque cette image est volumineuse 30Mb, 40Mb ou plus, de
  nécessiter plus de 8Gb de mémoire vive pour travailler sans plantage.
- à compter de février 2021 :Débruitage par morceaux.

## En final, quel module choisir entre « Noise reduction», « Wavelet levels », « Local adjustments denoise »

Il est très difficile de répondre à cette question, sinon pour « Local
adjustements » et débruiter seulement une partie de l'image. Néanmoins :

- avec les “vieux” raw…bruités ou les images très bruitées, “noise
  reduction” est indispensable…et simple
- avec les raws récents peu bruités, le mieux est « LA »… un peu
  complexe, mais et de loin le plus complet
- « wavelet level » a pour lui une interface facilitant une mise en
  œuvre conjointe avec les wavelets
- il n’y a aucun intérêt à utiliser les 3 ensemble. Par contre pour les
  images bruitées l'association de « noise reduction » et de un des
  autres modules est recommandée.

## Denoise avec « Local adjustments »

### Étapes du processus

(dans l'ordre où ils apparaissent dans le menu) Ces outils permettent
de:

- débruiter par niveau de détail
- différencier l'action sur les aplats et les structures

#### sélection  « agressive / conservative ». « Wavelet »

`Il n'est pas évident que « agressive soit plus destructeur que « conservative »...tout dépend de la force choisie aussi bien pour la luminance que la chrominance. Il est même probable que 2 passes de plus faible intensité aboutissent à un meilleur résultat. Par contre le temps de traitement sera nettement majoré`

#### « luminance denoise by level »: « Wavelet »

`cette courbe reprend en abscisse (axe des « x » )les niveaux de décomposition. Seuls les 3 premiers niveaux (0 1 2) sont différenciés par la courbe -  partie gauche. Pour les 4 niveaux supérieurs (3, 4, 5, 6) c'est le niveau de l'ordonnée  (axe des « y » - à droite de la courbe) qui est pris en compte. `

#### « Luminance detail recovery (DCT) » : « Fourier - Wavelet»

`ce curseur agit via la transformée de Fourier, sur la différence entre la composante L (Lab) de l'image débruitée par « wavelet » et l'image originale. Il est important que ce curseur ne soit pas à zéro (sinon de le vouloir), car cette transformée de Fourier va avoir un effet très fort sur le bruit et empêcher les 3 « equalizer » d'avoir une réelle action. Plus le curseur sera à droite, plus faible sera l'action DCT, plus les détails seront apparents.`

#### « Equalizer white black »: « Données avant wavelet »

`Ce curseur correspond en simplifié à la courbe luminance de « Noise reduction), il permet de choisir une action plus axée sur les tons sombres ou les tons clairs de l'image. L'action de la courbe ====« luminance denoise by level »===`  
`sera modulée en fonction de la position du curseur.`

#### « Denoise hue equalizer » : « Données avant wavelet ».

`Cette courbe permet d’accroître ou réduire par couleur (hue) de l'image, l'action de la courbe « luminance denoise by level »`

#### « Denoise based on luminance mask » : « Données avant wavelet »

- le masque dans « masque and modifications » (Blur & denoise ) doit
  être activé
- une des 2 courbes (ou les deux) L(L) - LC(H) doit être activée
- le curseur « dark area luminance threshold » permet de choisir le
  niveau de luminance en dessous duquel l'action de la courbe
  « luminance denoise by level » sera renforcée
- le curseur « light area luminance threshold » permet de choisir le
  niveau de luminance au dessus duquel l'action de la courbe « luminance
  denoise by level » sera renforcée
- entre les 2 valeurs, l'action de débruitage sera celle de la courbe.

#### « Reinforce denoise in dark and light areas »

`Tout dépend de chaque image et de la présence ou non d'aplats dans les tons sombres et/ou les tons clairs. Si l’image contient un aplat sombre presque parfait le fond du masque correspondant sera noir absolu (L =0). Si l'aplat est imparfait cette valeur sera variable. Le curseur accroîtra l'action de la courbe progressivement entre le niveau du seuil (dark ou light) et celui (variable) de l'aplat. Les valeurs inférieures à 1 diminuent l’action de la courbe.`

#### « Edge detection » - « Luminance and chroma detail threshold (DCT) » « Fourier - Wavelet » 

ce curseur essaye de prendre en compte l'effet de bord de l'image
originale afin de différencier l'action entre les aplats et les
structures. Deux algorithmes sont disponibles (tous deux sont issus de
ART..)

- « buildblendmask » - fonction similaire à celle utilisée notamment
  pour différencier le demosaicing
- « Laplacian »
- La première sera généralement plus progressive, la seconde plus
  sélective notamment lorsque le curseur est très proche du maximum.

#### Débruitage par morceaux

Peut être utilisé en conjonction avec wavelet et DCT ou seul. Il permet
un débruitage très performant de la luminance . Il va permettre
notamment une différentiation entre aplats et texture.

#### « Fine chroma » : « Wavelet »

`- ce curseur agit sur les 4 premiers niveaux de décomposition – en général va réduire ou supprimer les points colorés de bruit.`

#### « Coarse chroma » : « Wavelet »

`- ce curseur agit sur les 3 derniers niveaux de décomposition – en général va réduire ou supprimer les paquets colorés de bruit `

#### « Equalizer Blue-yellow / Red Green » : « Wavelet »

change la répartition du traitement du bruit coloré.

#### « Chroma detail recovery (DCT) » : « Fourier - Wavelet»

`ce curseur agit via la transformée de Fourier, sur la différence entre les  composantes  « a » et « b » (Lab) de l'image débruitée par « wavelet » et l'image originale. Il est important que ce curseur ne soit pas à zéro (sinon de le vouloir), car cette transformée de Fourier va avoir un effet très fort sur le bruit et empêcher les  « edge detection » d'avoir une réelle action. Plus le curseur sera à droite, plus faible sera l'action DCT, plus les détails colorés seront apparents.`

#### « Recovery based on luminance mask » - « Données avant et après débruitage »

Ce module agit sur la différence entre l’image originale bruitée et
l'image débruitée – bien sûr en prenant en compte l'ensemble des outils
ci-dessus. Ce sont les niveaux extrêmes de noir et de blanc du masque
qui vont permettre de maintenir le débruitage, où de conserver l'image
initiale non débruitée.

- le masque dans « masque and modifications » (Blur & denoise ) doit
  être activé
- une des 2 courbes (ou les deux) L(L) - LC(H) doit être activée
- le curseur « dark area luminance threshold » permet de choisir le
  niveau de luminance en dessous duquel l'action de « denoise » sera
  progressivement appliquée\*
- le curseur « light area luminance threshold » permet de choisir le
  niveau de luminance au dessus duquel l'action de « denoise » sera
  progressivement appliquée
- entre les 2 valeurs, l'image sera conservée sans débruitage, sauf si
  le curseur « Gray area denoise » est supérieur à 0 ; ce peut être
  utile par exemple pour atténuer un bruit chromatique disgracieux.
- Le curseur « Recovery threshold » permet de choisir le niveau
  d'application de « denoise » en dessous de « dark » et au dessus de
  « light »
- Le curseur « Decay » permet de choisir la « vitesse »
  d'affaiblissement ou d'amplification de l'application progressive.

### Note sur les masques

- Vous pouvez vous servir de « lockable color picker » (LCP) pour mieux
  cerner les zones de renforcement (ou d'affaiblissement). Attention
  pour que les informations du LCP corresponde aux valeurs des sliders
  il est nécessaire que dans « settings » - « background color for
  luminance and color masks » soit à zéro.
- Vous pouvez vous servir de l’ensemble des outils masque (en
  association avec les LCP), pour changer les zones grises et les rendre
  plus ou moins claires, conduisant à inclure ou exclure des aires
  différentes sur lesquelles l'action aura lieu ou non : structure mask,
  smooth radius, gamma, slope, shadows, courbe contrast L(L), courbe
  local contrast wavelet.

### Quelques rappels

Le module « Local adjustements » permet :

- de réaliser des ajustements locaux du bruit et donc par nature de
  différencier l'action selon les objets (par couleur, par luminance...)
- mais il permet aussi de traiter l'image entière et d'utiliser les
  fonctions spécifiques de « LA »
  - deltaE
  - Excluding spot
  - transitions
  - masques.

### Guided Filter

Cet outil – lorsque les valeurs du curseur « détail » sont négatives –
permet de générer un flou qui va masquer le bruit (luminance et
chrominance) et jouer le rôle de « denoise ».

- « Recovery based on luminance mask » fonctionne manière similaire à
  celui de « Denoise ».
