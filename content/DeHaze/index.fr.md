---
title: DeHaze fr
contributors:
  - Jdc
---

# Généralités

Alors que l'œil est capable de voir correctement les couleurs dans des
conditions de faible éclairage ou d'ambiance colorée ou de voile
atmosphérique, les appareils photo réussissent mal dans ces conditions.
C'est en s'inspirant des mécanismes biologiques de l'œil pour s'adapter
à ces conditions que l'algorithme MSR (MultiScale Retinex) a été
élaboré. Outre la photographie numérique, l'algorithme Retinex (Retinex
est la contraction de Rétine+cortex) est utilisé en astronomie pour
rendre visible l'information contenu dans les photographies
astronomiques, en médecine pour détecter des structures peu visibles
dans les radiographies et les tomodensitométries. De nombreuses théories
et algorithmes ont été mis au point depuis plus de 20 ans. La première
expérimentation a été proposée par Rahman en 1996. L'approche s'inspire
de la perception visuelle humaine et de la fonction rétinienne d'Edwin
Land. D'une certaine manière cette approche est assez « semblable » à
CIECAM. Cette fonction et plus particulièrement sa forme générale est
similaire à une différence de gaussienne \[DOG (Difference of Gaussian)
\]. L'idée consiste à caractériser l'information lumineuse d'un point à
partir de son intensité et celles de ses voisins. Ceci étant cette
approche ne repose sur aucun fondements scientifiques et s'appuie sur
l'expérience et diverses constantes empiriques. Au fil des ans de
nombreuses améliorations ont été apportées, mais de mon point de vue
aucune n'est parfaitement satisfaisante. Je me suis appuyé sur deux
documents:

- "Automatic Image Haze Removal Based on Luminance Component" (Fan Guo,
  Zixing Cai, Bin Xie, Jin
  Tang"[1](http://www.mcs.csueastbay.edu/~grewe/pubs/DistSensorNetworkBook2011/Atmosphere/HazeREmoval_SingleImage_Luminance.pdf)
- "Retinex Algorithm on Changing Scales for Haze Removal with Depth Map"
  (Weixing Wang, Lian
  Xu)"[2](http://www.sersc.org/journals/IJHIT/vol7_no4_2014/30.pdf)
- et de quelques astuces de programmation inspirées de "2003 Fabien
  Pelisson \<Fabien.Pelisson@inrialpes.fr\>"

# Les limitations imposées par Rawtherapee

L'algorithme de base impose une référence à l'image entière, et non à un
« crop » ou une réduction de l'image comme dans le processus de RT.
Cette limitation imposée par la fonction Gaussienne amène 3
conséquences :

- Le traitement a été décalé de sa place dédiée – qui aurait du être
  proche de « Lab adjustements » - vers le début du processus de RT –
  qui est obligatoirement (sauf si quelqu'un a une idée pour faire
  autrement) un process Raw. Ceci a pour conséquence que les fichiers
  non raw (TIF, JPG, etc.) ne peuvent être traités par cet algorithme.
- La deuxième conséquence de ce positionnement est que les
  caractéristiques des données Raw situées juste après interpolation
  (demosaicing) sont très différentes de celles situées en aval : pas de
  gamma, pas de limitation de gamut, par de balance des blancs, pas de
  conversion RGB....donc il faut s'attendre à des artefacts et des
  rendus luminance et couleurs peu performants.
- La troisième conséquence est le temps de réponse du système qui impose
  à chaque changement de réglages de réactualiser l'ensemble du
  processus.

Néanmoins, malgré ces handicaps, comme nous le verrons plus loin, les
résultats sont plus que satisfaisants aussi bien en temps de traitement
que en rendu des contrastes et couleurs notamment en conjurant l'action
de Retinex avec celle de Ondelettes.

# Le principe de l'algorithme

Pour de plus amples informations, lire les documents « pdf » situés en
généralités.

## Élaborer un fichier « transmission map » obtenu

- en faisant la différence, pour la luminance seulement, entre le
  logarithme de chaque pixel de l'image originale et le logarithme de la
  gaussienne correspondante des pixels voisins. L'écart-type (fonction
  gaussienne) ici utilisé est très élevé – usuellement dans RT des
  valeurs de sigma de 0.5 à 5 sont courantes – ici les valeurs se
  situent entre 10 et 280 (Single Scale Retinex) -au choix de
  l'utilisateur .
- en appliquant plusieurs fois (scale) – au choix de l'utilisateur - cet
  algorithme avec une sommation à partir de coefficients empiriques
  (Multi Scale Retinex). De faibles valeurs de scale accroissent le
  contraste apparent, mais donnent à l'image un aspect perspective, de
  fortes valeurs rendent l'image plus naturelle, mais ont tendance à
  accroître le bruit.
- en faisant varier au choix de l'utilisateur, MSR en fonction de
  l'effet souhaité (Uniforme, Bas, Haut) :
  - Uniforme : Tend à traiter les intensités faibles et les intensités
    fortes de manière équilibrée.
  - Bas : améliore les zones de faibles intensités
  - Haut : améliore le rendu des zones les plus claires

On obtient ainsi une distribution logarithmique (Transmission Map) qu'on
pourra ensuite « retrancher » de l'image originale, pour obtenir une
image en théorie dépourvue de brume ou d'effet de voile. Cette
distribution a approximativement une représentation gaussienne, avec un
minimum (minT) aux alentours, selon les images ; plus élevées pour les
images avec voile ; de -10 à -40, une moyenne proche de -1 à +2, un
écart-type souvent aux environs de 2 à 6, et un maximum (maxT) aux
alentours de 10 à 40. Les valeurs négatives traduisent les faibles
intensités et les positives les fortes intensités. Attention ces valeurs
sont des coefficients logarithmiques qui traduisent de très fortes
valeurs (log 1000 = 6.9) (exp 10 \# 22000)...(exp 20) \# 500.000.000 En
théorie, il faudrait utiliser de fortes valeurs de « scale » et de
Gaussienne dans les zones proches de la camera (celles où l'incidence du
voile est plus faible) et de faibles valeurs dans les zones distantes
(celles où l'incidence du voile est forte).

## Traiter le fichier « Transmission map »

Le traitement de base principal consiste à partir de la moyenne et de
l'écart-type de « transmission map » à appliquer une transformation de
type :

- newT = (oldT – mini) / maxi-mini.
- avec mini = moyenne – k \* ecart-type
- avec maxi = moyenne + k \* écart-type

Le choix de k – accessible à l'utilisateur - est déterminant dans le
rendu de l'image : de faibles valeurs vont accroître le contraste
apparent, de fortes valeurs vont rendre l'image plus naturelle avec
moins d'artefacts et halos.

j'ai ajouté trois composantes à ce traitement de base :

- un seuil – accessible à l'utilisateur – qui va permettre de réduire
  les valeurs maximum (maxT) et minimum (minT) en intégrant les valeurs
  écrêtées à la nouvelle distribution. Par exemple si le seuil choisi
  est 10, toutes les valeurs inférieures à -10 deviendront -10, toutes
  les valeurs supérieures à +10 deviendront +10. Cette action va
  accroître les contrastes, mais peut amener des artefacts.
- Une courbe (flatcurve) – accessible à l'utilisateur – pour agir
  directement sur la distribution, en remplaçant la théorie par la
  pratique...C'est en agissant sur la distribution que l'utilisateur
  pourra par exemple réduire les valeurs négatives et accroître les
  positives, (ou l'inverse) pour améliorer le rendu en temps réel.
- Un median 3x3 – accessible à l'utilisateur – qui agit sur les
  irrégularités de la distribution, afin de réduire les artefacts

## Élaborer le fichier « Image Haze-free »

Ce fichier s'obtient par "différence" entre l'image source et le fichier
"Transmission map".

On utilisera ici deux paramètres supplémentaires, Gain et Offset : Ces 2
paramètres vont permettre d'intégrer le fichier « Transmission map » à
une image exploitable. En effet sans précautions, l'image restaurée peut
se situer complètement en dehors des limites habituelles de luminance,
comprises entre 0 et 32768.

- « Gain » va jouer sur l'amplitude globale en la réduisant ou
  l'accroissant et par exemple réduire le nombre de pixels complètement
  noirs.
- « Offset » va permettre de rétablir la luminance après l'action de
  « gain »

Afin d'apporter une aide à l'utilisateur, j'ai intégré au GUI un
affichage des valeurs minimum de l'image « haze-free ». On peut agir sur
« Gain » et « Offset », mais également sur tous les autres paramètres
notamment ; « variance » et la courbe « transmission map ». L'idéal est
d'amener les valeurs Min au plus proche de 0, et Max au plus proche de
32768, par exemple -44230 + 76000

# Les différents réglages

## Réglages accessibles dans tous les cas

Vous disposez de 3 réglages :

- Dehaze method : avec "Low" "Uniform" "High"
  - Low :améliore les zones de faibles intensités
  - Uniforme : Tend à traiter les intensités faibles et les intensités
    fortes de manière équilibrée.
  - High : améliore le rendu des zones les plus claires

<!-- -->

- Strength : combine l'image "Haze-free" avec l'image originale.
  Strength=0 n'apporte aucun traitement "Dehaze" à l'image. Strength=100
  amène un traitement total, seule l'image "Haze-free" est affichée. Des
  valeurs inférieures à 50 sont recommandées.

<!-- -->

- Neigboring pixels : prend en compte les pixels voisins par un
  algorithme "Différence de Gaussien", plus les valeurs sont fortes,
  plus l'avant plan sera affecté. Plus les valeurs sont faibles plus les
  zones distantes seront affectées.

## Réglages accessibles avec 'Complete Retinex Algoritm"

- Histogram Equalizer:Cette courbe est un pis-aller...car elle vise à
  elle seule à rétablir, le gamma, la conversion RGB, le profil input
  icc, la balance des blancs...dont le manque est du à la position de
  "Dehaze" dans le process, qui est placée en Raw afin de travailler sur
  l'image complète. En l'absence de cette courbe, les données de
  "Transmission Map" sont généralement mauvaises et amènent d'important
  artefacts.

<!-- -->

- Scales: Cette valeur comprise entre 1 et 8, conditionne l’aspect de
  l'image, plus les valeurs sont faibles plus l'impression de contraste
  est grande, plus l'impression de perspective est importante. Plus la
  valeur est élevée, plus l'image paraîtra naturelle, mais plus le bruit
  aura tendance à croître.

<!-- -->

- Gain et Offset: Utilisés en conjugaison, ils permettent de positionner
  correctement l'image "haze-free". Vous pouvez vous aider des
  information contenues dans le GUI, et situer Min proche de zéro et Max
  proche de 32768.

<!-- -->

- Variance : ce coefficient pondère la moyenne et l'écart-type de
  "Transmission map". C'est un facteur clef de rendu de l'image. Il agit
  sur les seuils haut et bas de contraste du fichier "Transmission Map",
  plus les valeurs sont faibles plus l'image sera contrastée, plus les
  valeurs sont élevées plus l'image sera naturelle et les artefacts
  réduits.

<!-- -->

- Threshold : ce coefficient agit sur les valeurs maximales et minimales
  de "Transmission map"

<!-- -->

- Transmission Map : cette courbe permet d'interagir avec le fichier
  "Transmission map", l'abscisse de la courbe représente la base de
  distributiion de "Transmission map" (MinT, moyenne, MaxT). Abaisser la
  partie gauche va réduire les valeurs minimales (celles relatives à
  l'avant plan) et réciproquement, abaisser la partie droite va réduire
  les valeurs maximales (celles relatives à l'arrière plan) et
  réciproquement. Cette courbe est un point clef de régulation de la
  qualité perçue de l'image.

<!-- -->

- Transmission median filter : réduit les artefacts dues aux trop fortes
  variations locales de "Transmission map"
