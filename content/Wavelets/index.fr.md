---
title: Wavelets fr
contributors:
  - Jdc
  - Lebarhon
  - DrSlony
---

<div class="pagetitle">

Ondelettes

</div>

<figure>
<img src="/images/Daffodil_split.jpg" title="Daffodil_split.jpg" />
<figcaption>Daffodil_split.jpg</figcaption>
</figure>

__TOC__

## Remerciements et mise à jour

- Mise à jour : 23/08/2022
- Merci à Javier Bartol notamment pour la construction de cette page
  Rawpedia, particuièrement adaptée aux Ondelettes, et pour le long
  travail en commun.
- Merci à Wayne Sutton et Andy Astbury, pour le travail en commun, et la
  réalisation d'une version Anglaise de grande qualité.

## Comment cet outil est-il organisé?

L'outil Niveaux d'ondelettes est vaste et ses algorithmes sous-jacents
sont complexes. Il dispose de la plupart des fonctions nécessaires au
traitement des photographies du début à la fin, à l'exception de
certaines tâches telles que l'interpolation ou la gestion des couleurs.
Cependant, il est surtout utile lorsqu'il est utilisé pour compléter ou
affiner les opérations de traitement effectuées dans d'autres parties de
RawTherapee. Il vous permet de travailler sur différents niveaux de
détail pour produire des effets différentiés de contraste et de couleur,
de supprimer le bruit ou les défauts de l'image sans sacrifier le détail
global, ou de travailler sur la couleur et la luminance de l'image sans
introduire d'artefacts

Il peut être utilisé pour tout type d'image mais ses capacités uniques
le rendent particulièrement adapté aux portraits, à la
macrophotographie, à l'astrophotographie, etc., où le contrôle sélectif
des détails fins est important. Il peut également être utilisé avec
beaucoup d'efficacité en photographie de paysage pour supprimer le bruit
dans les ciels, compresser la gamme dynamique tout en préservant les
détails, réduire le bruit, supprimer les artefacts de couleur dans les
ombres et créer des effets de luminosité intéressants. Les possibilités
sont presque illimitées, mais vous ne pourrez les utiliser correctement
que si vous avez une bonne compréhension des principes sous-jacents et
du fonctionnement des différents outils.

L'outil est organisé autour d'un module général **Réglages des
ondelettes** suivi d'une série de modules qui peuvent être activés ou
désactivés pour effectuer des tâches spécifiques.

## Qu'est-ce qu'une Ondelette ? Application à RawTherapee

Un [Wavelet](https://en.wikipedia.org/wiki/Wavelet), ou plus précisément
[Wavelet Transform](https://en.wikipedia.org/wiki/Wavelet_transform),
est une fonction mathématique complexe qui est très utile dans le
traitement des images. Elle vous permet de diviser les images en
différents niveaux de détail afin de pouvoir travailler sur le niveau
qui vous intéresse.

Le terme ondelettes a été introduit au début des années 1980 par les
physiciens français Jean Morlet et Alex Grossman : ils ont utilisé le
mot français *ondelette*, qui signifie *petite vague*. Plus tard, ce mot
a été adapté à l'anglais en remplaçant *onde* par *wave*, ce qui a donné
*wavelet*.

La *transformée en ondelettes*, qui est similaire à une *transformée de
Fourier*, représente les données comme des combinaisons d'ondes connues
et prédéfinies (les fréquences), de sorte que le résultat soit aussi
proche que possible des données d'origine. D'une manière générale, la
principale différence pour les images bidimensionnelles est que dans la
transformée en ondelettes, les données analysées sont représentées comme
les fréquences présentes au niveau du pixel de l'image, alors que dans
la transformée de Fourier standard, les données représentent les
fréquences présentes dans le plein image. Par conséquent, l'utilisation
d'ondelettes offre plus de précision lors de l'analyse des données. .  
<span style="font-size: 0.7em; font-style: italic;">\[C'est évidemment
une explication très simpliste : les mathématiciens auraient sûrement
beaucoup à dire ici...\]</span>

![](Wavelet_daubechies20.jpg "Wavelet_daubechies20.jpg") RawTherapee
utilise des ondelettes dans divers outils, et dans celui-ci en
particulier il utilise
l'ondelette[Daubechies](https://en.wikipedia.org/wiki/Daubechies_wavelet)
pour décomposer les éléments de l'image en composants de l'image
[L\*a\*b\* color
space](https://en.wikipedia.org/wiki/CIELAB_color_space) (*L\**, *a\**
and *b\**).

La décomposition de l'image est réalisée à l'aide d'un
[algorithm](https://en.wikipedia.org/wiki/Algorithm) pour analyser le
contraste « interne » des groupes de pixels (2x2=4 pixels au premier
niveau, 4x4=16 pixels au deuxième niveau, ...) dans trois directions :
verticale, horizontale et diagonale. Cette analyse convertit ces valeurs
de contraste en ensembles d'ondelettes d'amplitudes et d'intensités
différentes et stocke leurs caractéristiques dans des matrices de
coefficients, qui indiquent comment les ondelettes doivent être
combinées pour régénérer une image aussi proche que possible de
l'originale.

A chaque fois que vous faites des modifications (contraste, tonalité,
bruit, ...) cette régénération se fait automatiquement, vous pouvez
ainsi voir immédiatement le résultat de vos réglages. En effet dès que
l'image est décomposée, elle cesse d'exister, ne laissant que des
ensembles de coefficients (un ensemble pour chaque niveau) qui seront
utilisés ultérieurement par l'outil. Ces ensembles de coefficients
peuvent être utilisés pour caractériser l'image des deux manières
suivantes : \* Plusieurs niveaux de détail : le premier niveau
correspond à des détails d'une surface de 2x2 pixels ; le dixième niveau
correspond aux "détails" d'une surface de 1024x1024 pixels. Le choix du
nombre que vous utilisez dépend de vos besoins, mais gardez à l'esprit
que le temps de traitement et les besoins en mémoire augmenteront avec
le nombre de niveaux.

  
Parce que seulement les *variations* (gradients, ou differences) dans
[hue](https://en.wikipedia.org/wiki/Hue) or
[luminance](https://en.wikipedia.org/wiki/Luminance) sont analysées à
chaque niveau, les niveaux ne contiendront aucune information si une
image est absolument uniforme en luminance et en couleur. Dans ce cas,
toutes les différences extraites des niveaux individuels proviendront du
bruit numérique et des changements de contraste (ou de chromaticité) dus
aux effets de bord, au brouillard ou à d'autres phénomènes optiques liés
à la scène.

- Une image résiduelle : résultat de la suppression des détails de tous
  les niveaux décomposés de l'image d'origine. Par conséquent, toute
  modification (contraste, chromaticité, etc.) effectuée à l'intérieur
  d'un niveau particulier n'aura aucun effet sur l'image résiduelle et
  vice versa.

[standard deviation](https://en.wikipedia.org/wiki/Standard_deviation).
En ajoutant les coefficients maximum et minimum à ces données, une
courbe de distribution caractéristique est générée pour chaque niveau
(il convient de noter que cette courbe n'est pas
[Gaussian](https://en.wikipedia.org/wiki/Normal_distribution)). Cette
information est utilisée de différentes manières dans les différents
algorithmes utilisés par l'outil des niveaux d'ondelettes.

## En pratique

Après décomposition, les niveaux obtenus peuvent être utilisés à
différentes fins : compression d'image, réduction de bruit, [tatouage
secret par transformation en ondelettes en
filigrane](http://www.intechopen.com/books/discrete-wavelet-transforms-algorithms-and-applications/application-of-discrete-),
traitement d'image résiduelle spécifique pour l'astronomie, etc.

Selon vos besoins, vous pouvez travailler soit avec un niveau de détail
individuel, soit avec plusieurs niveaux de détail (les uns après les
autres), soit avec l'image résiduelle, soit avec tous ces niveaux
combinés.

La taille des détails inclus dans chaque niveau est :

<figure>
<img src="/images/Wavelet_detail_size.jpg" title="Wavelet_detail_size.jpg" />
<figcaption>Wavelet_detail_size.jpg</figcaption>
</figure>

  
  
**1 (le plus fin)** : 2x2 pixels

**2** : 4x4 pixels

**3** : 8x8 pixels

**4** : 16x16 pixels

**5** : 32x32 pixels

**6** : 64x64 pixels

**7** : 128x128 pixels

**8** : 256x256 pixels

**9 (Le plus grossier)** : 512x512 pixels

**Extra** : 1024x1024 pixels

Si vous deviez sélectionner 5 niveaux de détail, les changements dans
les différents niveaux seraient limités aux détails de 32 pixels ou
moins. Dans ce cas l'image résiduelle aurait tous les détails de
l'image, sauf ceux inclus dans les niveaux *1* à *5*. Et comme les
détails qui ont été supprimés sont relativement petits, l'image
résiduelle serait similaire à l'image d'origine.

Par contre, si vous choisissez le *niveau 9* vous pourrez modifier les
détails avec une taille de 512 pixels et 1024 pixels (*niveau Extra*).
Dans ce cas, l'image résiduelle serait assez différente de l'image
d'origine, car les niveaux de *1* à *Extra* contiendraient tous les
détails, ne laissant guère plus qu'un arrière-plan flou.

La décomposition en ondelettes sépare les niveaux
*[lightness](https://en.wikipedia.org/wiki/Lightness)* et
*[chroma](http://www.huevaluechroma.com/015.php)* (\[https
://en.wikipedia.org/wiki/CIELAB_color_space#CIELAB *a\** et *b\**\])
dans l'image résiduelle et dans chacun des niveaux. Cela vous permet
d'appliquer différents réglages à la luminosité et aux tons de chaque
niveau et d'effectuer des traitements complètement différents sur
l'image résiduelle. Cela signifie que les niveaux et l'image résiduelle
sont indépendants et que l'outil ne modifiera que les niveaux où des
modifications ont été apportées. Le reste restera intact et l'image
résiduelle continuera d'être ce qui reste après que les détails de
chacun des niveaux ont été supprimés (qu'ils aient été modifiés ou non).

Notez que si vous souhaitez utiliser l'outil Niveaux d'ondelettes en
même temps que [l'outil CIECAM](CIECAM02/fr.md), vous pouvez
obtenir des artefacts dus au fait que le modèle colorimétrique CIECAM
utilise des valeurs spécifiques proches, mais différentes des valeurs de
l'espace colorimétrique Lab. Du fait du codage de l'outil, ces artefacts
sont inévitables, mais leur apparition dépendra des traitements
effectués.

#### L'apercu

La taille de l'image à l'écran a un impact direct sur la netteté perçue
et sur la capacité à voir les petits changements introduits par les
différents modules : **les effets de cet outil ne sont visibles qu'en
taille réelle** (ou plus grande).

En pratique, cela signifie que, [pour des raisons de vitesses du
processus](General_Comments_About_Some_Toolbox_Widgets/fr#La_zone_d.27aper.C3.A7u.md),
vous devez avoir à l'esprit la taille finale de l'image. S'il est prévu
de réduire la taille de l'image (la réduire, pas la recadrer), alors il
est conseillé de l'exporter d'abord avec sa taille finale et de la
traiter ensuite avec des ondelettes. Gardez cela à l'esprit car sinon ce
que vous voyez dans l'aperçu ne sera pas le même que le résultat final
exporté.

Il existe également une autre limitation : RawTherapee utilise tous les
niveaux possibles dans l'aperçu et ignore les niveaux dont les détails
sont plus grands que la partie de l'image que vous voyez à l'écran.
Cependant, si les modifications apportées aux niveaux ignorés ne
s'affichent pas à l'écran, elles seront appliquées lors de
l'enregistrement de l'image sur le disque.

**Exemples**

- ***Exemple 1*** : l'image fait **4096x2160** pixels, vous l'avez
  agrandie (à 100% ou plus) et dans l'aperçu vous voyez un *'1500x1200*
  ' zone de pixels de taille similaire à l'image finale. C'est le cas
  idéal car sur l'écran vous pouvez voir toutes les modifications dans
  tous les niveaux (jusqu'au *niveau Extra*). De plus, toute
  modification apportée à l'un des niveaux sera incluse dans l'image
  finale.
- ***Exemple 2*** : l'image fait **4096x2160** pixels, mais vous l'avez
  agrandie et ne pouvez voir que **300x200** pixels dans l'aperçu. Sur
  l'écran, vous ne pourrez voir aucun changement dans les détails
  supérieurs au *niveau 7* (détails de 128 pixels), mais lorsque vous
  l'enregistrerez, les modifications que vous avez apportées aux niveaux
  *8*, *9* et *Extra* seront inclus (car l'image est plus grande que
  1024x1024 pixels).
- ***Exemple 3*** : l'image fait **720x480** pixels et vous l'avez
  agrandie jusqu'à ne plus voir que **300x200** pixels dans l'aperçu.
  Sur l'écran vous ne pourrez voir aucune modification dans les détails
  plus gros que ceux du *niveau 7* (détails de 128 pixels). Lors de
  l'enregistrement, les modifications que vous avez apportées au *niveau
  8* seront incluses (détails de 256 pixels), mais les niveaux *9* et
  *Extra* **NE SERONT PAS** inclus.

Pour aider à garder cette information importante à l'esprit, l'outil
indique combien de niveaux sont utilisés pour l'aperçu (sous le dernier
curseur du module *Contraste*). Dans les exemples 2 et 3 il indiquerait
: « **Aperçu des niveaux maximum possibles = 7** ».

#### Contrast by Detail Levels vs Wavelet Levels (Niveaux ondelettes)

Il convient de mentionner que RawTherapee a un outil appelé *[Contrast
by Detail Levels](Contrast_by_Detail_Levels/fr.md)* et bien
qu'il ressemble à l'outil Wavelet Levels, il existe plusieurs
différences importantes entre eux :

- *Contraste par niveaux de détail* a moins de niveaux (6, au lieu de
  10),
- *Contrast by Detail Levels* vous permet uniquement de régler la
  luminance de chaque niveau, tandis que Wavelet Levels vous permet
  également de régler la chrominance de chaque niveau,
- *Contrast by Detail Levels* ajuste de manière égale toutes les valeurs
  de luminance (ou chroma) présentes dans le niveau, tandis que Wavelet
  Levels effectue un ajustement progressif ([cela est expliqué plus loin
  dans la section atténuation du
  contraste](#Le_concept_"Attenuation_curve".md)),
- *Contraste par niveaux de détail* n'a pas d'image résiduelle.

Cela dit, il est possible d'utiliser les deux outils en même temps. Il
convient de noter cependant que le *Contraste par niveaux de détail* est
appliqué plus tôt dans le [Pipeline de
traitement](Toolchain_Pipeline/fr.md), donc en fonction de
l'intensité des ajustements qui y sont effectués, les détails présentés
dans les niveaux à partir de *1* à *6* peuvent être affectés. En
d'autres termes, puisque le contraste aura changé avec les paramètres
*Contraste par Niveaux de Détail*, l'analyse par Niveaux d'Ondelettes
pourrait décomposer l'image d'une manière différente, donc les résultats
seraient différents. Dans tous les cas, si vous devez utiliser les deux
outils, il est recommandé d'ajuster d'abord le contraste par niveaux de
détail, puis d'ajuster les niveaux d'ondelettes.

## Configuration générale de l'outil

Lorsque cet outil est activé, tout ajustement affectera tous les modules
suivants.

### Force

Avec ce curseur, vous pouvez régler l'intensité globale de l'outil. Il
fonctionne sur un principe similaire au curseur d'opacité utilisé pour
mélanger les calques dans GIMP : tous les ajustements effectués dans
l'outil Niveaux d'ondelettes peuvent être mélangés dans l'image
d'origine à l'aide du curseur Intensité. Cela vous permet de faire des
ajustements assez agressifs, puis d'ajuster l'intensité globale pour
obtenir le résultat souhaité.

### Niveaux d'ondelettes

Ce curseur vous permet de décider en combien de niveaux de détail
l'image sera décomposée. Vous pouvez choisir n'importe quel niveau entre
*4* et *9* (le 10ème niveau, appelé *Extra*, apparaît automatiquement
lorsque vous sélectionnez *niveau 9*). Plus le nombre est élevé, plus le
temps de traitement et la mémoire nécessaires seront importants.

### Méthode avec pavés (Tiles)

Une liste déroulante vous permet de choisir parmi :

- Image complète,
- [Pavés](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons).

Il est toujours préférable d'utiliser *Image complète*, car cela évite
les problèmes dans la zone de transition entre les pavés (tiles).

Cependant, si vous n'avez pas assez de RAM, ou si vous traitez des
images très volumineuses (par exemple, 50 mégapixels ou plus), vous
devrez peut-être utiliser les tuiles :

| Mémoire requise, en octets, avec 9 niveaux de détail       |
|------------------------------------------------------------|
|                                                            |
| Mégapixels (Mpx)                                           |
| Pour ouvrir l'image (tous les outils désactivés)           |
| Contraste, chromaticité ou protection de la teinte activés |
| \+ Éviter le changement de couleur                         |
| Total                                                      |

### Performances des bords (Edge)

Une image qui a été décomposée en ses composantes par la méthode de
Daubechies peut avoir jusqu'à 10 échelles de coefficients allant de D2
(qui correspond à la décomposition de Haar) à D20. Dans RawTherapee les
coefficients *D2 (faible), D4 (standard), D6 (standard plus), D10
(moyen)* et *D14 (élevé)* sont utilisés. Plus il y a de coefficients,
plus l'ondelette distinguera de détails, mais avec une légère
augmentation du temps de traitement (souvent négligeable).

Bien qu'il n'y ait pas de relation directe entre la qualité résultante
et le nombre de coefficients (selon l'image d'origine), choisir le bon
nombre de coefficients permettra d'affiner la qualité des niveaux
inférieurs, ou celle de l'image résiduelle :

- dans certains cas, les meilleurs résultats pour la détection des
  contours sont obtenus avec D2
- dans les autres cas avec D6 ou D14

Ce paramètre a un impact assez fort sur *[Détection des
bords](#Détection_des_bords.md)* et aussi sur la décomposition
globale (la relation entre l'image résiduelle et chaque niveau).

### Aperçu

Ce groupe de commandes vous aidera à comprendre comment travailler avec
l'outil d'ondelettes et à affiner les paramètres des différents modules
(par exemple, la réduction du bruit).

Vous avez un total de quatre listes déroulantes, vous permettant de
personnaliser ce que vous voyez dans l'aperçu.

Le groupe est divisé en deux listes déroulantes principales (et
plusieurs autres qui seront activées lorsque vous effectuerez certaines
sélections dans les listes principales) :

- le premier vous permet de choisir l'arrière-plan de l'aperçu
- le second vous permet de choisir quels niveaux seront affichés dans
  l'aperçu

#### Arrière-plan

Dans la liste ***Arrière-plan***, vous pouvez choisir entre 3
arrière-plans possibles : *Noir*, *Gris* ou *Image résiduelle*, qui sera
utilisé lors de la visualisation de l'un des niveaux.

L'histogramme tiendra compte de ces options et vous permettra par
exemple de voir les effets des réglages sur l'image résiduelle. Notez
cependant que si vous choisissez le fond noir ou gris, vous ne verrez
pas l'image résiduelle (le vrai fond) et vous pourrez trouver que
l'image a un aspect étrange. Vous devez être particulièrement conscient
de cela si vous apportez des modifications aux niveaux de détail, car
l'effet réel ne sera pas visible tant que vous n'aurez pas remis l'image
résiduelle en arrière-plan. Malgré cela, il est parfois intéressant de
voir les changements sur fond neutre pour mieux juger de ce qui se passe
(par exemple en réduction de bruit).

#### Niveaux de processus

Dans la liste ***Processus*** vous pouvez sélectionner :

1.  *Un niveau*
2.  *Niveaux de détails plus fins, avec niveau sélectionné* : tous les
    niveaux **depuis** le niveau sélectionné jusqu'au *niveau 1*,
3.  *Niveaux de détails plus grossiers, sans niveau sélectionné* : tous
    les niveaux jusqu'au *niveau Extra* (plus l'image résiduelle), **à
    l'exception** du niveau sélectionné
4.  *Tous niveaux, dans tous les sens*

Dans les versions précédentes du programme, la liste était affichée avec
des étiquettes différentes, mais le comportement des curseurs reste
inchangé :

- Un niveau
- Inférieur ou égal au niveau : maintenant *Niveaux de détails plus
  fins, avec le niveau sélectionné*
- Au-dessus du niveau : désormais **Niveaux de détails plus grossiers,
  sans niveau sélectionné**
- Tous niveaux, dans toutes les directions

Si vous sélectionnez l'une des trois premières options, deux listes
déroulantes seront activées juste en dessous de *Traiter :*.

- dans la liste de gauche vous pouvez décider à quel niveau se réfèrent
  les options précédentes (du *niveau 1* à *9*, le *niveau Extra*, ou
  l*'Image Résiduelle*).
- dans la liste de droite vous pouvez choisir le sens de décomposition
  des ondelettes (*Vertical, Horizontal, Diagonal, All directions*).

Si vous sélectionnez l'option *Tous les niveaux, dans toutes les
directions*, vous pouvez éditer les niveaux directement sur l'image
résiduelle (les deux listes du bas resteraient désactivées). Cette
option est utile si vous avez déjà de l'expérience avec l'outil et que
vous préférez afficher l'intégralité de l'image lors de sa modification.
C'est également l'option que vous devez sélectionner avant d'exporter.
Gardez à l'esprit que ce que vous voyez dans l'aperçu sera ce qui est
exporté dans l'image finale et qui apparaît dans l'histogramme : si vous
avez sélectionné *Un niveau*, vous ne verrez qu'un seul niveau à l'écran
et l'histogramme reflètent les valeurs RVB de ce niveau particulier.
Lorsque vous exportez l'image, seul le niveau choisi sera inclus dans
l'image finale. *'Avant d'exporter, assurez-vous de sélectionner*Tous
les niveaux, dans toutes les directions'''

Vous trouverez ci-dessous un exemple d'image avec un traitement minimal
qui sera utilisé dans tous les exemples suivants. A côté, de gauche à
droite, vous verrez les détails *niveau 2*, les détails *niveau 4* et
l*'image résiduelle*.

Dans les deux exemples montrant les détails, la décomposition a été
faite avec ***Edge performance***réglé sur*D6 - standard plus*, la
couleur*gris*a été sélectionnée comme***Arrière plan***. De plus, pour
isoler le détail,*Un niveau'' a été sélectionné dans***Traitement**''.

L*'image résiduelle* est le résultat de la suppression de tous les
détails après avoir choisi *5 niveaux d'ondelettes*.

<span style="font-size: 0.7em; font-style: italic;">  ***Pour agrandir
les images, cliquez dessus et lorsque la nouvelle page se charge,
cliquez une seconde fois sur l'image***. </span>

#### Suggestions d'utilisation

- vous pouvez sélectionner *Un niveau* avec un fond gris pour voir
  comment le coefficient de Daubechies sélectionné (de D2 à D14) a
  décomposé les détails, puis essayer différents coefficients pour voir
  lequel offre la séparation des détails la plus précise
- vous pouvez sélectionner *Un niveau* pour trouver le niveau qui
  contient les détails sur lesquels vous souhaitez travailler (comme le
  niveau qui a extrait les imperfections de la peau, mais pas sa
  texture)
- vous pouvez sélectionner *Un niveau* et voir l'effet des changements
  de contraste sur ce niveau particulier, ou affiner la réduction du
  bruit
- vous pouvez sélectionner *Niveaux de détails plus grossiers, sans
  niveau sélectionné* et *8*, pour voir l'image résiduelle avec les
  détails les plus larges et mieux apprécier l'action des différents
  paramètres du module *Image résiduelle*
- vous pouvez sélectionner *Niveaux de détails plus fins, avec le niveau
  4 sélectionné* et comme arrière-plan *Image résiduelle*, pour voir les
  modifications dans les détails les plus fins dans leur contexte, sans
  que les détails plus grands ne masquent ce que vous faites

### Exemple (aperçu)

Vous trouverez ci-dessous un exemple d'image avec un traitement minimal
qui sera utilisé dans tous les exemples suivants. A côté, de gauche à
droite, vous verrez les détails *niveau 2*, les détails *niveau 4* et
l*'image résiduelle*.

Dans les deux exemples montrant les détails, la décomposition a été
faite avec ***Edge performance***réglé sur*D6 - standard plus*, la
couleur*gris*a été sélectionnée comme***Arrière plan***. De plus, pour
isoler le détail,*Un niveau'' a été sélectionné dans***Traitement**''.

L*'image résiduelle* est le résultat de la suppression de tous les
détails après avoir choisi *5 niveaux d'ondelettes*.

<span style="font-size: 0.7em; font-style: italic;">  ***Pour agrandir
les images, cliquez dessus et lorsque la nouvelle page se charge,
cliquez une seconde fois sur l'image***. </span>

<div>

- <figure>
  <img src="/images/wavelet_pic.jpg" title="wavelet_pic.jpg" />
  <figcaption>wavelet_pic.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_L2.jpg" title="wavelet_config_L2.jpg" />
  <figcaption>wavelet_config_L2.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_L4.jpg" title="wavelet_config_L4.jpg" />
  <figcaption>wavelet_config_L4.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_RI.jpg" title="wavelet_config_RI.jpg" />
  <figcaption>wavelet_config_RI.jpg</figcaption>
  </figure>

</div>

## Contraste

Dans ce module, vous pouvez modifier le contraste de luminosité
(composante *L\** de la décomposition) des détails de chaque niveau
indépendamment. Cela vous permet d'augmenter le contraste des détails
plus petits pour donner une impression de plus grande netteté, tout en
réduisant le contraste des détails plus grands. Un avantage pratique de
cette approche est qu'en réduisant le contraste global (les gros
détails), vous n'avez pas besoin d'augmenter autant les détails fins
pour obtenir une impression de netteté. Cela permet d'éviter plus
facilement l'introduction d'artefacts.

### Le concept "Attenuation curve"

Comme indiqué dans un chapitre précédent, l'outil d'ondelettes calcule
la moyenne et l'écart type (même si cette valeur à peu de sens du fait
que la distribution n'est pas Gaussienne, mais c'est une modélisation)
pour chaque niveau de décomposition et chaque direction (verticale,
horizontale, diagonale), pour les valeurs positives et négatives, et
utilisera ces valeurs dans tous les modules.

En réalité selon les images la valeur moyenne est aux environs de 300 ou
400, l'écart-type vers 500 à 700 et le maximum peut atteindre 11000. Ce
qui amène de nécessaires adaptation de l'algorithme, en particulier pour
les valeurs inférieures à la moyenne.

Dans le cas du module Contraste, la première étape consiste à définir
les valeurs du curseur de contraste pour chaque niveau décomposé en
fonction de l'effet requis. Cependant, si vous n'effectuez que cette
action, les variations de contraste seraient proportionnelles au
contraste d'origine ([modifications
homothétiques](https://en.wikipedia.org/wiki/Homothetic_transformation),
comme dans l'outil *Contraste par niveaux de détail* ) et il serait
facile de générer des artefacts.

Pour pallier ce problème, les valeurs de contraste des détails de chacun
des niveaux sont analysées et triées avant d'être modifiées et
progressivement atténuées selon la courbe suivante :

<figure>
<img src="/images/wavelet_beta.png" title="wavelet_beta.png" />
<figcaption>wavelet_beta.png</figcaption>
</figure>

De manière générale et pour chaque niveau, le graphique montre que :

- les valeurs de contraste les plus faibles sont à gauche et les valeurs
  de contraste les plus élevées à droite (attention le graphique est lui
  aussi une modélisation, car la partie droite est beaucoup plus
  étendue)
- la valeur de contraste fixée pour chaque niveau et direction
  (*contraste* dans le graphique) définit la modification maximale qui
  sera appliquée aux valeurs de contraste présentes dans le niveau
- la modification sera maximale autour de la valeur de contraste moyenne
  de chaque niveau (la valeur *moyenne* sur le graphique)
- plus les valeurs de contraste s'écartent de la valeur de contraste
  moyenne, moins elles seront modifiées
- les valeurs de contraste élevées ou fortes sont plus atténuées que les
  faibles

Cela signifie que pour chaque niveau, les changements de contraste les
plus importants seront apportés aux valeurs de contraste moyen tout en
évitant les valeurs extrêmes pour éviter des effets excessifs ou des
artefacts. Cependant, gardez à l'esprit deux points fondamentaux :

1.  la valeur de contraste moyenne est la moyenne arithmétique **des
    valeurs de contraste présentes dans le niveau** : si toutes les
    valeurs de contraste sont élevées (forts contrastes), la valeur
    moyenne sera également élevée et les contrastes extrêmes dans ce
    niveau particulier le niveau sera moins modifié
2.  chaque niveau a sa propre valeur moyenne, qui dépend des valeurs de
    contraste présentes dans les détails de ce niveau particulier

### Niveaux de contraste

![](wavelet_contrast_buttons.jpg "wavelet_contrast_buttons.jpg") Le
nombre de niveaux affichés est défini par les ***Niveaux d'ondelettes***
et vous pouvez réduire ou augmenter ce nombre dans les paramètres de
configuration des ondelettes.

Les boutons ***Contraste -*** et ***Contraste +*** facilitent le
changement progressif des valeurs de chaque niveau : plus fort dans les
premiers niveaux et plus discret dans les derniers . Comme vous pouvez
le voir dans l'exemple, la progression est homogène : à partir du
*Niveau Extra*, qui n'a pas été modifié, chaque niveau a été augmenté de
31 unités par rapport au niveau précédent (le montant réel dépendra de
le nombre de fois que vous avez cliqué sur les boutons Contraste+ ou
Contraste-).

En général ces boutons permettent de définir une progression logique des
valeurs de
[microcontrast](Edges_and_Microcontrast/fr#Microcontrast.md) :
plus haut pour les premiers niveaux et plus bas pour les derniers
niveaux.

N'oubliez pas que si un niveau a un contraste uniforme, l'action du
curseur pour ce niveau n'aura aucun effet (s'il n'y a pas de détails,
rien n'est changé).

Notez que l'image résiduelle n'est pas incluse dans ce groupe de champs
car ce n'est pas un niveau : c'est ce qui reste de l'image d'origine
après suppression de tous les détails répartis sur tous les niveaux.

### Attenuation et sélectivité des niveaux de contraste

Il y a 3 curseurs qui vous permettent d'ajuster la courbe pour chaque
niveau (et direction)

1.  ***Réponse d'atténuation*** : en sélectionnant des valeurs
    positives, la partie supérieure de la courbe s'élargit autour de la
    zone de contraste moyen et est pondérée vers les contrastes les plus
    élevés. A l'inverse, la sélection de valeurs négatives rétrécit la
    courbe, réduisant ainsi la plage des contrastes qui subissent toute
    modification notable. Graphiquement:
    <div>

    - <figure>
      <img src="/images/wavelet_beta+damper.png" title="wavelet_beta+damper.png" />
      <figcaption>wavelet_beta+damper.png</figcaption>
      </figure>

    - <figure>
      <img src="/images/wavelet_beta-damper.png" title="wavelet_beta-damper.png" />
      <figcaption>wavelet_beta-damper.png</figcaption>
      </figure>

    </div>
2.  ***Offset*** : décale le haut de la courbe, pour que les
    modifications de contraste les plus fortes ne soient plus apportées
    aux contrastes moyens. En déplaçant la courbe vers la droite, les
    valeurs de contraste les plus élevées varieront davantage, alors
    qu'avec des valeurs de curseur négatives, les valeurs de contraste
    les plus faibles seront davantage modifiées. Graphiquement:
    ![](wavelet_beta+offset.png "wavelet_beta+offset.png")
3.  ***Seuil de faible contraste*** : il s'agit de la valeur de
    contraste minimum que doivent avoir les détails du niveau de
    décomposition pour qu'ils soient pris en compte. Les valeurs de
    contraste inférieures, qui ont une valeur inférieure à la valeur
    minimale, ne seront pas prises en compte lors du calcul de la
    moyenne de ce niveau, ni ne subiront de variation, quel que soit le
    réglage du curseur. De cette façon, nous pouvons éviter de mettre en
    évidence le bruit ou des textures plus fines et plus délicates.

### Application

Ce bloc de contrôle vous permet de décider si les changements de
contraste dans les niveaux individuels s'appliquent à tous les détails
ou uniquement aux détails dont les pixels se situent dans une plage
donnée de [luminance](https://en.wikipedia.org/wiki/Luminance). Cela
vous permet, par exemple, d'augmenter le contraste des détails fins avec
une luminance élevée et de réduire le contraste des détails plus grands
avec une luminance faible.

Dans la liste déroulante, vous décidez où appliquer les changements de
contraste : sur toute la plage de valeurs de luminance (c'est-à-dire à
tous les détails de chaque niveau) ou uniquement aux détails qui ont une
certaine valeur de luminance.

#### Plage de Luminance

Si vous avez sélectionné la *Plage entière de luminance*, la
modification s'appliquera à tous les détails de chacun des niveaux.
Cependant, si vous choisissez *Plage de luminance sélective*, vous
pouvez décider quels détails seront modifiés dans quels niveaux.

De plus, après avoir sélectionné la *Plage de luminance sélective* deux
courbes de seuil et deux curseurs apparaîtront vous permettant de
personnaliser le résultat. c'est à dire.:

- **Plage de luminance des niveaux plus fins** :
  - il s'agit d'une petite zone avec un dégradé noir et blanc et quatre
    points qui définissent la plage des valeurs de luminance qui seront
    affectées par le changement de contraste
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_contrast_highlight.jpg" title="gauche" />
    <figcaption>gauche</figcaption>
    </figure>

    </div>
  - Si vous déplacez votre souris dessus, vous verrez où sont les
    limites par défaut : *Bottom-Left : 50, Top-Left : 75, Top-Right :
    98, Bottom-Right : 100*. Cette gamme couvre les points forts
  - ce sont les valeurs de luminance qui doivent être dans l'image pour
    que le changement de contraste soit appliqué aux détails (voir
    l'explication suivante du curseur)
  - les valeurs par défaut sont les suivantes :
    - les détails avec une luminance de 50 ou moins ne seront pas
      modifiés
    - les détails avec une luminance de 50 à 75 seront soumis à un
      nombre croissant de modifications
    - entre 75 et 98, 100% de la modification sera appliquée
    - entre 98 et 100, progressivement moins de changement sera appliqué
  - pour changer les valeurs des points sur la courbe, nous avons deux
    options :
    - cliquez et déplacez l'un des deux points d'un côté (gauche ou
      droite) et faites glisser les deux points ensemble
    - appuyez sur la touche *shift*, cliquez sur un point et faites-le
      glisser pour déplacer uniquement ce point
  - les valeurs par défaut sont définies pour les hautes lumières, mais
    vous pouvez modifier les points pour couvrir n'importe quelle partie
    de la plage, des ombres aux hautes lumières, selon vos besoins.

<!-- -->

- **Niveaux plus fins** : seuls les niveaux à partir de la valeur
  sélectionnée et en dessous seront affectés par la courbe de seuil
  *Plage de luminance des niveaux plus fins*.

<!-- -->

- **Plage de luminance des niveaux plus grossiers** :
  - une autre petite zone avec un dégradé noir et blanc et quatre points
    qui définissent la plage des valeurs de luminance qui seront
    affectées par le changement de contraste
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_contrast_shadow.jpg"
    title="wavelet_contrast_shadow.jpg" />
    <figcaption>wavelet_contrast_shadow.jpg</figcaption>
    </figure>

    </div>
  - encore une fois, en passant votre souris dessus, vous verrez où se
    trouvent les limites par défaut autour des ombres : *Bottom-Left: 0,
    Top-Left: 2, Top-Right: 25, Bottom-Right: 50*
  - les niveaux par défaut sont :
    - les détails avec une luminance entre 0 et 2 seront soumis à une
      quantité croissante de changement de contraste
    - entre 2 et 25, une modification de contraste de 100% sera
      appliquée
    - entre 25 et 50, progressivement moins de changement sera appliqué
    - à partir de 50 aucun changement ne sera appliqué
  - les valeurs par défaut sont définies pour les ombres, mais vous
    pouvez modifier les points pour couvrir n'importe quelle partie de
    la plage, des ombres aux hautes lumières, selon vos besoins.

<!-- -->

- **Niveaux plus grossiers** : seuls les niveaux compris entre la valeur
  définie avec ce curseur et le nombre sélectionné de *niveaux
  d'ondelettes* seront affectés par la courbe de seuil *Plage de
  luminance des niveaux plus grossiers*.

Aucune modification ne sera apportée à un niveau qui n'est pas inclus
dans une sélection *Niveaux plus fins* ou *Niveaux plus grossiers*,
quelles que soient les valeurs définies avec les curseurs Contraste.
Pour ces niveaux, le résultat final sera le même qu'en définissant une
valeur de curseur de contraste de *0*. </br>

#### Études de cas

- vous utilisez 7 niveaux et souhaitez uniquement modifier le *niveau 7*
  dans la plage définie par la courbe de seuil *Plage de luminance des
  niveaux plus grossiers* : réglez le curseur de *Niveaux plus
  grossiers* sur *7*
- vous utilisez 7 niveaux et souhaitez uniquement modifier sélectivement
  les détails les plus fins : réglez les *Niveaux plus fins* sur le
  niveau le plus élevé que vous souhaitez modifier et réglez les
  curseurs Contraste pour le reste des niveaux sur *0*
- vous utilisez 7 niveaux et vous souhaitez régler sélectivement les
  niveaux *1* et *2* en fonction des valeurs de luminance définies dans
  la courbe de seuil pour *Plage de luminance des niveaux plus fins* et
  ajuster les niveaux *6* et *7* en fonction des valeurs de luminance
  définies dans la courbe de seuil pour la *Plage de luminance des
  niveaux plus grossiers* : réglez le curseur *Niveaux plus fins* sur
  *2* et le curseur *Niveaux plus grossiers*. niveaux*sur*6*. Cela
  modifiera sélectivement les niveaux*1*,*2*et*6*,*7*en fonction des
  paramètres de la courbe de seuil correspondante et des détails des
  niveaux*3*,*4 *et*5'' resteront inchangés

## Chroma

Ce module fonctionne de manière similaire au module de contraste, sauf
que dans ce cas, l'outil analyse le contraste des couleurs (composantes
*a\** et *b\**).

Dans la liste déroulante ***Méthode de chrominance*** vous avez les
options suivantes :

- *Whole chroma range* : avec cette option, tout changement dans
  n'importe quel niveau affectera toute la gamme de chroma, quelles que
  soient les valeurs qui ont été définies dans les niveaux du *Module de
  contraste*.
- *Saturé/pastel* : vous pouvez modifier ici deux courbes de seuil qui
  agissent simultanément et limitent les tons pastel et saturés, quelles
  que soient les valeurs des niveaux *Module Contraste*.
- *Lier les niveaux de contraste* : les changements de chrominance
  seront directement liés à ceux effectués à chaque niveau du *Module
  Contraste*.

Lorsque vous sélectionnez *Whole chroma range* ou *Saturated/pastel*,
vous pouvez utiliser le bouton *Neutral* pour réinitialiser tous les
curseurs de niveau à leur valeur par défaut (0).

De plus, il y a un curseur *Réponse d'atténuation* pour les 3 options,
qui agira de la même manière que décrit dans la [Concept
Attenuation](#Le_concept_"Attenuation_curve".md).

### All Chroma

Si vous choisissez cette option, toute la plage de chrominance de
l'image est modifiée, quelle que soit la saturation de chaque couleur.

La même remarque que pour le contraste s'applique ici : pour qu'il y ait
des changements de couleur, il faut qu'il y ait une variation de couleur
préexistante dans le niveau. Si un niveau a une couleur uniforme, le
curseur n'aura aucun effet.

Les modifications à chaque niveau sont limitées à la plage
*\[-100,+100\]* : la valeur *-100* équivaut à désaturer complètement le
niveau, tandis que la valeur *+100* augmente la chroma de chaque détail.
Cette méthode introduit presque toujours des artefacts car la formule
appliquée à la valeur de couleur pour chaque détail ne prend pas en
compte s'il existe des écarts par rapport à la valeur initiale.

<div>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.jpg"
  title="wavelet_contrast_15C+_H3S6.jpg" />
  <figcaption>wavelet_contrast_15C+_H3S6.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_full.jpg"
  title="wavelet_chrom_WC_full.jpg" />
  <figcaption>wavelet_chrom_WC_full.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_L1L2full.jpg"
  title="wavelet_chrom_WC_L1L2full.jpg" />
  <figcaption>wavelet_chrom_WC_L1L2full.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_detail.jpg"
  title="wavelet_chrom_WC_detail.jpg" />
  <figcaption>wavelet_chrom_WC_detail.jpg</figcaption>
  </figure>

</div>

Les exemples ci-dessus signifient que vous ne devez apporter que des
modifications subtiles avec cette option car, selon le niveau et la
force du changement, il est très facile d'introduire des artefacts très
visibles. Cependant, si les changements sont trop subtils, ils seront à
peine perceptibles. Dans tous les cas, le bruit de chrominance sera
affecté et augmentera de manière significative

### Pastel - Saturated

Avec cette option, les changements de couleur dans chaque niveau se
concentrent sur les tons saturés des niveaux avec des détails plus fins
et sur les tons pastel des autres niveaux (avec des détails plus
grossiers).

Après avoir sélectionné cette option, un curseur de seuil et deux
courbes de seuil apparaîtront, qui fonctionnent de la même manière que
les courbes de seuil de contraste ci-dessus.

- **Seuil de saturation/pastel**
  - avec ce contrôle vous décidez à partir de quel niveau passer des
    tons saturés aux tons pastel
  - la valeur par défaut est *5*, c'est-à-dire que dans les 5 premiers
    niveaux, les tons saturés seront modifiés, et dans les niveaux
    supérieurs, les tons pastel seront modifiés
  - veuillez noter que si cette valeur est supérieure au nombre de
    niveaux de la décomposition en ondelettes, seuls les tons saturés
    seront modifiés
  - par contre, si vous choisissez *1* (le niveau avec seulement les
    détails les plus fins), c'est comme si vous ne modifiiez que les
    tons pastels
- **Gamme de chrominance pastel** :
  - la courbe de seuil est la même que pour le contraste. Les points
    définissent le niveau de saturation pour lequel un changement de
    couleur sera effectif
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_chrom_pastel.jpg" title="wavelet_chrom_pastel.jpg" />
    <figcaption>wavelet_chrom_pastel.jpg</figcaption>
    </figure>

    </div>
  - *il est à noter que la zone sombre du dégradé correspond aux tons
    pastel et la zone plus claire correspond aux tons saturés (suite
    [cette explication de la
    saturation](https://en.wikipedia.org/wiki/Colorfulness) )*
  - en passant la souris dessus, vous pouvez voir les limites : par
    défaut les valeurs présentées sont *Bottom-Left : 0, Top-Left : 2,
    Top-Right : 20, Bottom-Right : 30*.
  - les modifications de la courbe sont effectuées de manière similaire
    à celles apportées aux courbes de contraste
- **Gamme de chrominance saturée**
  - en passant la souris dessus, vous verrez où sont les limites : par
    défaut les valeurs affichées sont *Bottom-Left : 30, Top-Left : 45,
    Top-Right : 100, Bottom-Right : 130* \< div style="overflow :
    caché"\>![](wavelet_chrom_chrom.jpg "wavelet_chrom_chrom.jpg")
    </div>
  - Bien que les valeurs des deux courbes ne se chevauchent pas, vous
    pouvez voir un chevauchement sur l'interface graphique. Et dans la
    pratique, il semble que les changements autour du niveau de seuil
    affectent à la fois les tons saturés et pastel. Pour pouvoir voir
    clairement s'il y a un effet ou non (selon que le ton est pastel ou
    saturé), il faut utiliser des valeurs très saturées ou très
    *désaturées* (pastel).

Néanmoins, comme avec l'option *Whole chroma range*, les changements ne
sont pas perceptibles à moins que vous ne vouliez introduire des
artefacts assez visibles.

<div>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.jpg"
  title="wavelet_contrast_15C+_H3S6.jpg" />
  <figcaption>wavelet_contrast_15C+_H3S6.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_L1L2full.jpg"
  title="wavelet_chrom_WC_L1L2full.jpg" />
  <figcaption>wavelet_chrom_WC_L1L2full.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_SP_L1L2full_L3_60.jpg"
  title="wavelet_chrom_SP_L1L2full_L3_60.jpg" />
  <figcaption>wavelet_chrom_SP_L1L2full_L3_60.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.jpg"
  title="wavelet_contrast_15C+_H3S6.jpg" />
  <figcaption>wavelet_contrast_15C+_H3S6.jpg</figcaption>
  </figure>

</div>

Comme vous pouvez le voir, malgré l'application de changements de 100 %
à certains niveaux, les différences sont subtiles et peuvent sembler
négligeables si vous ne regardez pas de près. Les changements les plus
visibles sont les « nervures » plus intensément colorées des pétales.

### Link contrast levels

Cette option est intéressante car les changements de chrominance sont
directement liés à ceux apportés à chacun des niveaux de contraste.

Le rapport entre les changements de contraste et de couleur est ajusté
avec le curseur ***Force du lien chroma-contrast*** : ainsi *0* n'aura
aucun effet sur la chrominance, tandis que *100* fournit le maximum
d'effet, et est plus intense que pour l'option *Whole chroma range*
(particulièrement perceptible en *chroma noise*).

Gardez à l'esprit que si vous appliquez de forts changements aux niveaux
de contraste, ils apparaîtront également dans la chrominance et
généreront très probablement des artefacts indésirables : votre meilleur
allié sera toujours le '**'Force du lien Chroma-contrast**' ', pour
obtenir des effets clairement visibles sans produire d'artefacts qui
gâcheraient la photo.

### Exemple (changement de chrominance)

<div>

- <figure>
  <img src="/images/wavelet_chrom_Link_100.jpg"
  title="wavelet_chrom_Link_100.jpg" />
  <figcaption>wavelet_chrom_Link_100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_Link_50.jpg"
  title="wavelet_chrom_Link_50.jpg" />
  <figcaption>wavelet_chrom_Link_50.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_Link_50_Str50.jpg"
  title="wavelet_chrom_Link_50_Str50.jpg" />
  <figcaption>wavelet_chrom_Link_50_Str50.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6_Str50.jpg"
  title="wavelet_contrast_15C+_H3S6_Str50.jpg" />
  <figcaption>wavelet_contrast_15C+_H3S6_Str50.jpg</figcaption>
  </figure>

</div>

Les modifications apportées à l'image originale ont été exagérées afin
que les résultats soient clairement visibles. Par conséquent, les
modifications de contraste et de couleur apportées à la dernière photo
ont introduit des liserés bleus sur les pétales, des auréoles autour des
anthères des étamines et un fond bruité. Malgré cela, l'image n'est pas
un désastre complet compte tenu de l'agressivité des modifications. À ce
stade, il convient de noter l'intensité de la couleur dans les «veines»
des pétales.

## Gamut (contrôle)

Ce module est lié aux modules [Contraste](#Contraste.md) et
[Chroma](#Chroma.md), afin que les ajustements puissent être
ciblés en fonction de la chrominance dans les détails. En d'autres
termes, pour les détails dans chacun des niveaux d'ondelettes, vous
pouvez non seulement prendre en compte le contraste de la luminance
(module contraste) ou le contraste des tons (module chroma), vous pouvez
également choisir la gamme de couleurs que ces modifications seront
appliquées.

### Réduire les artefacts dans le ciel bleu

Les images numériques présentent souvent un bruit "moucheté" dans les
couleurs bleues du ciel. Le traitement par ondelettes peut accentuer ce
bruit ou générer de petits artefacts car il augmente le contraste local.

Cette case à cocher introduit un [filtre
médian](https://en.wikipedia.org/wiki/Median_filter) pour réduire ces
artefacts, au détriment de la perte de détails et de la génération
d'artefacts dans les zones où il y a des changements de ton ou qui ont
un contraste élevé . Bien qu'utile pour un traitement rapide et peu
exigeant, vous obtiendrez en fait de meilleurs résultats avec une
combinaison judicieuse de l'outil *[Réduction du
bruit](Noise_Reduction/fr.md)* de l'onglet Détail et du *[Module
Débruitage et ajustements](#Débruitage_et_ajustements.md)* dans
cet outil.

<div>

- <figure>
  <img src="/images/wavelets_gamut_nosky.jpg" title="wavelets_gamut_nosky.jpg" />
  <figcaption>wavelets_gamut_nosky.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_sky.jpg" title="wavelets_gamut_sky.jpg" />
  <figcaption>wavelets_gamut_sky.jpg</figcaption>
  </figure>

</div>

### Teinte de peau

Bien que le titre fasse référence aux *teintes de peau*, le réglage ne
se limite pas à celles-ci et vous pouvez spécifier la gamme de tons que
vous souhaitez modifier. La plage sélectionnée régira les modifications
apportées par les autres contrôles du module. Cependant, la plage par
défaut concerne les tons de peau habituels.

Pour les exemples qui suivent, la gamme suivante (plutôt restrictive) de
tons rouges a été choisie :

<figure>
<img src="/images/wavelets_gamut_skin_hue.jpg"
title="wavelets_gamut_skin_hue.jpg" />
<figcaption>wavelets_gamut_skin_hue.jpg</figcaption>
</figure>

### Ciblage/protection de la peau

Cela vous permet de modifier le contraste et/ou la couleur des détails
dont les couleurs sont incluses dans la gamme ci-dessus :

- avec le curseur à *0* toutes les couleurs de l'image sont modifiées de
  la même manière
- la sélection de *-100* (glissement vers la gauche) centre le contraste
  et les changements de couleur **dans la gamme de couleurs
  sélectionnée**
- au contraire, si vous sélectionnez *100* (en glissant vers la droite)
  les couleurs qui **ne coïncident pas** avec la plage sélectionnée
  seront modifiées

Dans les positions intermédiaires entre *0* et *±100* les changements
augmentent progressivement soit vers la gamme choisie, soit vers le
reste des couleurs.

<div>

- ![](wavelets_gamut_skin.jpg "wavelets_gamut_skin.jpg")\]

- <figure>
  <img src="/images/wavelets_gamut_skin_target0.jpg"
  title="wavelets_gamut_skin_target0.jpg" />
  <figcaption>wavelets_gamut_skin_target0.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_skin_target-100.jpg"
  title="wavelets_gamut_skin_target-100.jpg" />
  <figcaption>wavelets_gamut_skin_target-100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_skin_target+100.jpg"
  title="wavelets_gamut_skin_target+100.jpg" />
  <figcaption>wavelets_gamut_skin_target+100.jpg</figcaption>
  </figure>

</div>

### Courbe

Une fois que vous avez défini le "ciblage/protection de la peau"
souhaité, vous pouvez utiliser ce graphique pour affiner la variation de
contraste/chromaticité pour chaque couleur : déplacer un point de
contrôle vers le haut augmentera la variation pour cette couleur, tout
en le déplaçant vers le bas atténuera les changements pour cette couleur
particulière (bien qu'il n'éliminera pas complètement l'effet).

Cependant, seules les couleurs comprises dans la gamme sélectionnée
ci-dessus seront prises en compte quelles que soient les couleurs
modifiées avec la courbe.

<div>

- <figure>
  <img src="/images/wavelets_gamut_curve_target100.jpg"
  title="wavelets_gamut_curve_target100.jpg" />
  <figcaption>wavelets_gamut_curve_target100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_curve.jpg" title="wavelets_gamut_curve.jpg" />
  <figcaption>wavelets_gamut_curve.jpg</figcaption>
  </figure>

</div>

### Éviter le changement de couleur (Avoid color shift)

Le traitement par niveaux d'ondelettes peut introduire des changements
de teinte importants, en particulier près des limites de la gamme de
couleurs de l'[Espace colorimétrique de
travail](Color_Management/fr#Profil_de_travail.md). L'activation
de cette option effectue une série de corrections pour s'assurer que la
teinte résultante est liée à la couleur initiale.

## Virage partiel

Ce module peut être utilisé pour colorer des niveaux de détail
spécifiques selon les besoins.

Cependant, il n'est pas possible d'agir directement et précisément sur
la teinte à chaque niveau individuel car les composantes *a\** et *b\**
ont été décomposées et il est très difficile de créer une relation
mathématique précise entre les teinte sélectionnée et les composants
décomposés.

Néanmoins, vous pouvez contrôler dans une certaine mesure les teintes
qui seront modifiées et décider des dominantes de couleur qu'elles
prendront.

Comme pour les autres modules, il y a un curseur *Attenuation Response*,
qui agira de la même manière que décrit dans le [chapitre sur
l'atténuation dans le module
Contraste](#Attenuation_and_selectivity_in_contrast_changes.md).

### Couleurs exclues

Le graphique ***Couleurs exclues*** est basé sur la répartition des
couleurs des coordonnées chromatiques utilisées pour l'espace
colorimétrique L\*a\*b\* : l'axe horizontal représente la composante a\*
(allant du vert au rouge ) et l'axe vertical représente la composante
b\* (allant du bleu au jaune).

Cependant, comme il est compliqué de représenter la distribution réelle
des couleurs de l'espace L\*a\*b\* en deux dimensions, les teintes
pastel telles qu'elles sont présentées dans l'interface, tout en étant
mathématiquement précises, ne sont pas visuellement intuitives, en
particulier lors de la sélection de tons jaunes. Perceptuellement, ils
sont équivalents à un graphique tel que celui ci-dessous :

<figure>
<img src="/images/Cielab_8x8.jpg" title="Cielab_8x8.jpg" />
<figcaption>Cielab_8x8.jpg</figcaption>
</figure>

Au centre du graphique, il y a un point blanc qui, lorsqu'il est
déplacé, produira un deuxième point noir. Ces deux points définissent
les centres des gammes de couleurs qui seront plus ou moins protégées
par les éventuels réglages de tonification effectués ultérieurement dans
ce module. Placer le point blanc sur une couleur particulière du
graphique définit le centre de la première gamme de couleurs. De même,
la position du point noir définit le centre de la deuxième gamme de
couleurs. Si le point noir n'est pas déplacé de la position initiale au
centre, la deuxième plage est ignorée.

Avec le curseur ***Plage a et b %*** une zone d'influence est créée
autour du centre tel que défini par la position du point sur le
graphique et le curseur % détermine la taille de la zone.

Avec le curseur ***Protection***, l'effet des éventuels ajustements sur
les couleurs sélectionnées est réduit dans la zone d'influence (centre
plus plage). La valeur du curseur de protection correspond au % de
l'effet de protection et diminuera à mesure que vous vous éloignez du
centre, jusqu'à ce qu'en fin de plage (à la périphérie de la zone
d'influence) la réduction soit équivalente à la moitié de la valeur
établie.

Par exemple : *Protection=80* signifie que la protection est de 80% et
donc le centre de chaque plage ne recevra que 20% des valeurs de
tonification définies dans les modules d'égaliseur (expliqué
ci-dessous). Au fur et à mesure que l'on s'éloigne du centre et jusqu'à
ce que l'on atteigne la limite fixée par *Plage a et b %*, la
tonification s'intensifiera progressivement jusqu'à atteindre au maximum
la moitié de la valeur de *Protection*. Dans ce cas ce serait 40 ce qui
signifie que les couleurs en périphérie subiraient 60% de la valeur de
consigne.

### Virage - contrôles

Dans ce groupe, deux courbes sont présentées :

- la ***Opacity Red-Green*** (la *a\*-curve*) qui agit sur les tons
  rouge-vert
- la ***Opacity Blue-Yellow*** (la *b\*-curve*) qui agit sur les tons
  bleu-jaune

Mais n'oubliez pas que les couleurs finales de la photo seront une
combinaison des tons de ces deux courbes. Par exemple : si vous modifiez
la courbe *a\** (***Red-Green Opacity***) en rouge, tous les tons du
niveau que vous modifiez prendront un ton rouge/rougeâtre , mais ne
deviendront pas nécessairement rouges (s'ils avaient aussi une forte
composante bleue, ils tourneraient vers le magenta/violet).

D'un point de vue pratique : un ton peut devenir plus ou moins saturé
"jusqu'à une certaine limite" et en même temps subir un changement de
teinte. Pour mieux visualiser ces effets, jetez un œil à cette [vue du
dessus de *L\*a\*b\* color
space*](https://upload.wikimedia.org/wikipedia/commons/0/06/CIELAB_color_space_top_view.png)
, avec *b\** comme axe vertical et *a\** comme axe horizontal. Et ne
manquez pas cette [vue de face de l*'espace colorimétrique
L\*a\*b\**](https://upload.wikimedia.org/wikipedia/commons/7/7d/CIELAB_color_space_front_view.png).
Le bas de la vue de dessus correspond à l'avant de la vue de face.

Dans l'interface vous trouverez deux *types de courbe :* *Linéaire*
(![](wavelet_toning_linear.jpg "wavelet_toning_linear.jpg")) et
*Equalizer* (![sans cadre](wavelet_toning_curve.jpg "sans cadre")). Pour
choisir entre l'un ou l'autre, cliquez sur le petit triangle à droite.

La courbe *linéaire* annule l'effet de l'axe auquel elle se réfère : si
vous la sélectionnez dans ***Opacité Rouge-Vert**'', vous n'effectuerez
aucune action sur ces tons. De même avec le***Opacité bleu-jaune**''.

Dans chaque courbe *égaliseur* il y a un axe horizontal (ou axe *x*) et
un axe vertical (ou axe *y*) :

- l'axe *x* représente les 10 niveaux possibles, dans l'ordre croissant
  de gauche à droite et uniformément répartis
- l'axe *y* représente l'intensité de la modification : lorsque la
  courbe monte ou descend au-dessus de la ligne médiane la couleur est
  modifiée vers une extrémité ou l'autre de l'axe de la composante en
  cours de modification (*a\** ou *b\**)
- dans la ***Opacité rouge-vert*** (la *courbe a\**), déplacer la courbe
  vers le haut introduit une teinte rougeâtre, tandis que la déplacer
  vers le bas introduit une teinte verdâtre
- dans la ***Opacité Bleu-Jaune*** (la *b\*-courbe*), déplacer la courbe
  vers le haut introduit une teinte jaune, tandis que la déplacer vers
  le bas introduit une teinte bleutée

Par défaut, la courbe est plate et se trouve sur la ligne médiane. Pour
avoir une idée de la façon dont vous pouvez interagir avec la courbe,
consultez les explications de *[Tone
Curves](Exposure#Tone_Curves.md)*. Et rappelez-vous que si vous
n'aimez pas les modifications que vous avez apportées à la courbe, vous
pouvez toujours recommencer en cliquant sur la flèche de
réinitialisation
![<File:ResetButton.png>](ResetButton.png "File:ResetButton.png").

Tant qu'il y a des variations de contraste dans la couleur de l'image
d'origine, ces courbes vous permettront de faire varier sélectivement la
tonalité des détails souhaités. Les changements qui en résultent
dépendent de l'endroit où vous placez les points dans la courbe et de
l'amplitude de la modification (c'est-à-dire du nombre de niveaux
qu'elle affecte). Tout doit être fait «à l'œil», car il n'y a pas de
référence aux niveaux sur l'axe *x*, cependant vous pouvez voir l'effet
de la modification en regardant l'aperçu.

Si vous utilisez moins de 10 niveaux, les points affectant les niveaux
les plus à droite seront simplement ignorés : si vous modifiez une image
à 4 niveaux, les 6 les plus à droite (ceux avec les plus gros détails)
seront ignorés.

### Exemple (application de virages partiels)

Vous vous souviendrez que nous avions de vilains halos bleus autour de
certaines parties de la fleur, alors essayons de les éliminer (ou au
moins de les cacher) avec les commandes de tonification. On profite du
fait que la majeure partie de l'image a une dominante rouge pour pouvoir
modifier la composante bleue, sans que cela soit trop perceptible dans
le résultat global. Pour cet exemple, aucune des couleurs n'a été
exclue :

<div>

- <figure>
  <img src="/images/wavelet_chrom_Link_50_Str50.jpg"
  title="wavelet_chrom_Link_50_Str50.jpg" />
  <figcaption>wavelet_chrom_Link_50_Str50.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBYfull.jpg"
  title="wavelet_toning_opBYfull.jpg" />
  <figcaption>wavelet_toning_opBYfull.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBYfull_curve.jpg"
  title="wavelet_toning_opBYfull_curve.jpg" />
  <figcaption>wavelet_toning_opBYfull_curve.jpg</figcaption>
  </figure>

</div>
<div>

- ![](wavelet_toning_opBY.jpg "wavelet_toning_opBY.jpg") \</ li\>

- <figure>
  <img src="/images/wavelet_toning_opBY_Str50.jpg"
  title="wavelet_toning_opBY_Str50.jpg" />
  <figcaption>wavelet_toning_opBY_Str50.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBY_curve.jpg"
  title="wavelet_toning_opBY_curve.jpg" />
  <figcaption>wavelet_toning_opBY_curve.jpg</figcaption>
  </figure>

</div>

Il y a encore quelques traces de halos bleus dans le résultat final bien
qu'ils ne soient pas aussi visibles, et l'aspect général de la photo
semble être le même.

## Débruitage et ajustements

Ce module complète l'outil général **[Réduction du
bruit](Noise_Reduction/fr.md)** (dans l**onglet Détail'')
et**Bords netteté''' (expliqué dans la section suivante).

La gestion du bruit est une question complexe car il faut décider où
cela doit être fait dans le pipeline de traitement (par exemple au début
ou à la fin), ce qui doit être fait et comment.

Dans RawTherapee, l'outil général de réduction du bruit est placé au
début du pipeline de traitement pour empêcher les outils suivants
d'augmenter le bruit à des niveaux inacceptables. Dans l'outil
*Réduction du bruit* de l'onglet Détail vous avez les possibilités
suivantes :

- traiter la luminance (également basée sur les ondelettes) comme un
  bloc, c'est-à-dire sans distinction entre les niveaux d'ondelettes
- traiter le bruit de couleur selon une méthode différente : cela
  nécessite généralement un nombre de niveaux d'ondelettes plus élevé (4
  à 7) et un traitement plus complexe
- ajouter un traitement *Fourier Transform* pour affiner la luminosité
- ajouter un filtre médian

Bien que cela puisse être suffisant, l'utilisation de l'outil Niveaux
d'ondelettes peut apporter des avantages supplémentaires (même s'il
utilise le même algorithme que l'outil général) :

- il est à la fin du pipeline de traitement, réduisant ainsi l'impact du
  bruit ajouté par d'autres outils généraux (*Exposition*, *Courbes*,
  *Plage dynamique*, etc.)
- il agit séparément et indépendamment sur chacun des 4 premiers
  niveaux, alors que la réduction de bruit *standard* a un effet sur
  l'ensemble de l'image. Ceci est particulièrement utile pour les images
  à faible bruit et pour les images où l'outil général a été utilisé
  avec parcimonie pour préserver les détails (c'est-à-dire pour réduire
  plutôt que pour éliminer le bruit)
- il réduit l'incidence du bruit dans les autres modules de traitement
  des ondelettes, par ex. vous permettant de traiter le ciel sans
  exagérer le bruit
- il ajuste à la fois le traitement du bruit et le degré
  d'amplification/réduction du contraste à chaque niveau, ce qui est
  utile par exemple pour les images astronomiques

### Les contrôles

Vous pouvez ajuster la réduction du bruit par niveaux selon vos besoins
avec l'ensemble de commandes suivant, qui non seulement décident sur
quel bruit agir, mais lient également son effet au module *Edge
Sharpness* et au chroma denoise.

#### Lien avec la force de la netteté des bords (Edge sharpness)

Cette option modifiera le comportement du curseur inférieur de chaque
niveau (expliqué ci-dessous).

- si vous choisissez de **ne pas l'activer**, alors le curseur inférieur
  de chaque niveau (le curseur **Force**) aura un effet similaire au
  module Contraste lorsqu'il est utilisé sur le *Toute la gamme de
  luminance*
- si vous l'activez, vous pouvez modifier la distribution de
  l'amélioration de la netteté dans les premiers niveaux avec le curseur
  inférieur (ceci est expliqué plus en détail dans le module suivant,
  *Netteté des contours*)

#### Denoise égaliseur Blanc-Noir

La vision humaine est capable de distinguer plus facilement le bruit
dans les zones claires que dans les zones sombres, même lorsqu'il y a
plus de bruit dans les zones sombres (les ombres).

Avec ce curseur, la réduction du bruit peut être augmentée soit dans les
ombres (avec des valeurs à droite), soit dans les hautes lumières (avec
des valeurs à gauche).

Il est plus facile de régler si vous choisissez une zone avec à la fois
des zones claires et sombres, de sorte que vous puissiez voir la
différence entre les niveaux de bruit dans les ombres et dans les hautes
lumières.

#### Denoise (Débruitage) et force

Ces curseurs sont utilisés pour contrôler le bruit dans les 4 niveaux de
détail plus fins de l'image :

- le curseur supérieur de chaque niveau effectue le **Denoise**.
- celui du bas, appelé **Force**, modifie le contraste des détails pour
  ce niveau particulier. Il convient de noter que ce réglage n'est pas
  aussi sophistiqué que les réglages effectués dans le module Contraste

Bien que le curseur *Strength* puisse sembler redondant, il est très
utile pour récupérer le contraste perdu dans les détails lorsque des
valeurs plus élevées de *Denoise* ont été appliquées. De cette façon,
vous n'avez pas à sauter d'un module à l'autre pour ajuster rapidement
l'image. Il sert également à moduler la répartition de l'effet sur les 4
premiers niveaux du *Edge Sharpness*.

#### Denoise chrominance

Le chroma denoise est complémentaire de l'outil *Noise Reduction* de
l'onglet Detail.

Étant donné que le débruitage de la chrominance des ondelettes se trouve
à la fin du pipeline de traitement, il est utile pour supprimer tout
bruit de chrominance qui n'a pas été supprimé lors de l'utilisation de
la réduction du bruit dans l'onglet Détails, ou le bruit qui a été
généré par d'autres outils.

Dans ce groupe de curseurs, vous trouverez :

- le **Denoise Equalizer Blue-Red** : le bruit de chrominance se
  présente généralement sous la forme de points rouges ou bleus et avec
  ce curseur vous pouvez augmenter la réduction des points bleus (à
  gauche), ou des points rouges ( À droite)
- le curseur **Chrominance Fine** : réduit le bruit de chrominance dans
  les détails les plus fins, c'est-à-dire aux niveaux les plus bas
- le curseur **Chrominance Coarse** : réduit le bruit de chrominance
  dans les détails les plus grossiers, c'est-à-dire aux niveaux les plus
  élevés. Ce bruit peut être vu comme des taches de couleur qui semblent
  «sales» ou «n'appartiennent pas» à l'image et qui ne peuvent pas être
  supprimées avec le curseur *Chrominance Fine* en raison de leur taille

### Exemple (application de débruitage)

Pour mieux comprendre dans quelle mesure les niveaux de bruit peuvent
être améliorés, il est utile de procéder niveau par niveau, en profitant
du fait que vous pouvez visualiser le détail de chaque niveau individuel
sur un fond neutre (comme expliqué à propos de
*[Preview](#The_preview.md)*). Désactivez *Lien avec Edge
Sharpness' Strength* puis augmentez le curseur *Strength* du niveau sur
lequel vous travaillez au maximum : le bruit deviendra évident et vous
pourrez évaluer la quantité de bruit nécessaire . Une fois que vous avez
ajusté le curseur *Denoise*, déplacez le curseur *Strength* sur la
valeur qui vous convient le mieux (des valeurs négatives peuvent
également être utilisées) et passez au niveau suivant.

<div>

- <figure>
  <img src="/images/wavelet_denoise_orig.jpg" title="wavelet_denoise_orig.jpg" />
  <figcaption>wavelet_denoise_orig.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d00s100.jpg"
  title="wavelet_denoise_L2d00s100.jpg" />
  <figcaption>wavelet_denoise_L2d00s100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d30s100.jpg"
  title="wavelet_denoise_L2d30s100.jpg" />
  <figcaption>wavelet_denoise_L2d30s100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d30s27.jpg"
  title="wavelet_denoise_L2d30s27.jpg" />
  <figcaption>wavelet_denoise_L2d30s27.jpg</figcaption>
  </figure>

</div>
<div>

- <figure>
  <img src="/images/wavelet_denoise_L1d00s00.jpg"
  title="wavelet_denoise_L1d00s00.jpg" />
  <figcaption>wavelet_denoise_L1d00s00.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d00s100.jpg"
  title="wavelet_denoise_L1d00s100.jpg" />
  <figcaption>wavelet_denoise_L1d00s100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d12s100.jpg"
  title="wavelet_denoise_L1d12s100.jpg" />
  <figcaption>wavelet_denoise_L1d12s100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d12s-17.jpg"
  title="wavelet_denoise_L1d12s-17.jpg" />
  <figcaption>wavelet_denoise_L1d12s-17.jpg</figcaption>
  </figure>

</div>
<div>

- <figure>
  <img src="/images/wavelet_denoise_orig.jpg" title="wavelet_denoise_orig.jpg" />
  <figcaption>wavelet_denoise_orig.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_final.jpg"
  title="wavelet_denoise_final.jpg" />
  <figcaption>wavelet_denoise_final.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_orig100.jpg"
  title="wavelet_denoise_orig100.jpg" />
  <figcaption>wavelet_denoise_orig100.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_final100.jpg"
  title="wavelet_denoise_final100.jpg" />
  <figcaption>wavelet_denoise_final100.jpg</figcaption>
  </figure>

</div>

En règle générale, il est préférable de ne pas éliminer complètement le
bruit, mais simplement de le réduire afin qu'il soit à peine visible et
en même temps, d'augmenter le contraste des détails à ce niveau
particulier. En amplifiant la présence des détails, le bruit sera ignoré
lors de la visualisation de l'image et la photo aura un aspect
légèrement texturé. La procédure est la suivante :

1.  réduisez légèrement le bruit de luminance à l'aide de l'outil
    *Réduction du bruit* dans l'onglet détail, en faisant
    particulièrement attention à ne perdre aucun détail
2.  sélectionnez *un niveau*, *fond gris* et *niveau 1*
3.  zoomez à 300-400 % sur une zone avec des détails d'arrière-plan
    médiocres (il doit y avoir suffisamment de détails avec un bon
    contraste, mais pas au point de masquer le bruit)
4.  déplacer le curseur *niveau 1 force* dans *Denoise* au maximum (ou
    presque), en s'assurant que les détails peuvent toujours être
    distingués du bruit
5.  déplacez le curseur supérieur vers un point où la réduction du bruit
    est moyennement faible (ne supprimez pas complètement le bruit),
    puis remettez le curseur de force inférieure dans sa position
    d'origine.
6.  le réglage de la réduction du bruit entraînera une perte de
    contraste dans les détails. Pour y remédier, augmentez le curseur
    inférieur à un niveau de force qui vous permet de récupérer le
    contraste initial des détails
7.  passez au *niveau 2* et continuez avec les points 4, 5 et 6, en
    ajustant cette fois la *force* du *niveau 2*
8.  continuer de la même manière avec les niveaux *3* et *4*
9.  terminez le processus en sélectionnant *Tous les niveaux dans toutes
    les directions*

Si l'image est peu bruitée, vous pouvez passer directement à l'étape 2.
Cependant, si l'image est très bruitée, il est important de régler la
réduction du bruit de luminance à l'étape 1 : il faut jouer avec le
débruitage *Luminance* et le curseur *Gamma* (dans l'outil Réduction du
bruit), pour diriger la réduction du bruit vers les ombres ou les hautes
lumières. Plus vous prendrez soin de cette étape, meilleur sera le
résultat final.

Pour augmenter la présence de détails, vous pouvez utiliser les curseurs
inférieurs et augmenter la force de chaque niveau autant que vous le
souhaitez, mais il est préférable d'utiliser les curseurs du module
Contraste, car ils offrent plus de contrôle et donnent de meilleurs
résultats avec moins d'artefacts. . N'oubliez pas non plus que dans cet
exemple seuls les curseurs *Denoise* et *Force* ont été utilisés, mais
le résultat peut être encore affiné si nécessaire avec les autres
curseurs de ce module.

Ne pas confondre le débruitage de ce module avec la fonction **Seuil bas
(bruit)** utilisée pour la **Détection des contours** dans le module
*Netteté des contours*, qui prend en compte le bruit (sans réduire it)
pour éviter de le mettre en évidence lors de l'analyse des bords

## Bords Netteté (luminance) et Clarté

Ce module applique une forme de détection de contour sur les détails
dans chacun des niveaux d'ondelettes.

À première vue, cela ressemble à un **[Masque
flou](Sharpening/fr#Masque_Flou.md)**, car la décomposition par
niveaux d'ondelettes génère une *image résiduelle* qui ressemble un peu
à un masque, mais c'est là que les similitudes fin.

Si vous voulez des résultats similaires au *Masque flou* ou
*[Deconvolution](https://en.wikipedia.org/wiki/Deconvolution#Optics_and_other_imaging)*,
alors vous devrez sélectionner le *Détection des contours* et choisissez
une valeur élevée de *Sensibilité au dégradé* (70 ou plus ; par défaut,
ce sera 90). Il est préférable de ne pas modifier les premiers niveaux
de contraste dans *Contraste par niveaux de détail*, car ils peuvent
nuire au fonctionnement de l'algorithme (toutes ces options sont
expliquées en détail ci-dessous).

Avant d'expliquer comment utiliser le module, gardez à l'esprit ce qui
suit pour éviter de générer des artefacts ou des effets trop forts : à
la fois la configuration de *[Performance des bords (D2, D4 ...
D14)](#Performances_des_bords_(Edge) "wikilink")* et le [force de chaque
niveau dans *Débruitage et
ajustements*](#D.C3.A9bruitage_et_ajustements.md) (lorsque vous
avez activé *Lien avec Edge Sharpness' Strength*) a un effet notable sur
*Edge detection*. A chaque réglage, il faut évaluer le résultat et tout
réajuster pour obtenir une bonne netteté avec le minimum d'artefacts.

Dans l'interface vous avez plusieurs blocs de contrôle :

- ***paramètres*** : ce premier bloc permet de régler la façon dont
  l'outil détecte les bords
- ***contraste local*** : dans ce bloc, vous pouvez décider comment les
  changements de contraste sont appliqués aux détails en fonction de
  leurs valeurs de contraste initiales.
- ***détection des contours*** : pour augmenter la netteté là où elle
  est le plus nécessaire (c'est-à-dire sur les bords)

### Configuration

***Pour le moment, n'activez pas la*Détection des bords*, car les
résultats seront différents si cette option est activée.***

Il y a 4 curseurs :

1.  **Force** : est la quantité d'amélioration du contraste appliquée
    aux détails. Plus la valeur *Strength* est élevée, plus le
    changement de contraste est important. Son effet est plus fort à des
    niveaux plus fins et la réinitialisation de ce curseur annule tout
    changement dans le reste du module.
2.  **Attenuation Response** : il fonctionne de la même manière que le
    contrôle d'atténuation décrit dans le [chapitre traitant de
    l'atténuation du module
    Contraste](#Attenuation_and_selectivity_in_contrast_changes.md).
    Il contrôle dans quelle mesure les valeurs de contraste seront
    modifiées.
3.  **Rayon** : génère un effet d'image en trois dimensions et peut
    donner l'impression de plus de *volume* dans les détails, ou de
    *texture* plus prononcée et a une influence même si le curseur est
    réglé à zéro. A noter également que l'effet du *Rayon* est modifié
    par la valeur du *Détail*.
4.  **Détail** : change la façon dont le contraste est réparti entre les
    niveaux. L'effet sera plus fort dans les 3 premiers niveaux si le
    curseur est déplacé vers la droite, alors que si vous le déplacez
    vers la gauche (vers des valeurs négatives), les changements de
    contraste dans les 3 premiers niveaux seront pratiquement annulés.

L'exemple suivant vous permet de voir à quel point les changements de
contraste dans chacun des niveaux sont liés aux valeurs des curseurs
*Rayon* et *Détail*, et comment les effets du *Rayon* curseur sont
modifiés en fonction de la valeur du curseur *Détail*. Pour illustrer
cela, nous avons défini *Premier niveau : Inchangé* (qui sera expliqué
plus tard) et *Lien avec la force de la netteté des bords* désactivé
(dans le module *Denoise and Refine*).

- **le rapport Rayon-Contraste** : changer la valeur du *Rayon* modifie
  le contraste des détails. En général, les changements de contraste les
  plus forts sont observés entre les rayons 40 et 75. En dessous de 40,
  le niveau 1 est renforcé et au-dessus de 75, le niveau 3 et dans une
  moindre mesure les niveaux supérieurs (l'effet devient d'autant plus
  doux que le niveau est élevé et aux niveaux ' '9*et*Extra'' l'effet
  est négligeable).
- **Relation Rayon-Détail** : selon la valeur de *Détail*, modifier le
  *Rayon* augmente plus ou moins le contraste des détails d'un niveau ou
  d'un autre.

Ce qui suit est un résumé des principaux points. La représentation
graphique facilite la compréhension :

<div>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_D-50.png"
  title="Wavelet_edge_sharpening_D-50.png" />
  <figcaption>Wavelet_edge_sharpening_D-50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_unchanged.png"
  title="Wavelet_edge_sharpening_unchanged.png" />
  <figcaption>Wavelet_edge_sharpening_unchanged.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_D100.png"
  title="Wavelet_edge_sharpening_D100.png" />
  <figcaption>Wavelet_edge_sharpening_D100.png</figcaption>
  </figure>

</div>

Juste sous le champ *Détail*, vous avez une liste déroulante avec 3
options pour le **Premier (ondelette) niveau** :

- *Renforcé* : l'effet est augmenté au *niveau 1*.
- *Inchangé* : la distribution de l'algorithme est inchangée.
- *Réduit* : la modification est réduite pour le *niveau 1*.

La possibilité de voir les différences entre ces trois options dépendra
de la quantité de détails fins dans l'image, du contraste des détails et
du choix des coefficients utilisés pour la décomposition (*D2*, *D4' ',
...,*D14*) : dans les photos de nuit avec des points lumineux surexposés
(par exemple, des réverbères, etc.), l'option*Réduit*atténuera tout
bruit de contraste élevé au premier niveau. Souvent cependant, il n'y a
pratiquement pas de détails pertinents dans le*niveau 1'', donc l'option
que vous choisissez n'aura probablement pas d'importance.

De plus, si vous utilisez l'option *Réduit*, vous constaterez peut-être
un comportement un peu étrange ou du moins «différent» pour le *niveau
1* : le contraste diminue progressivement à partir d'un maximum au
*Rayon : 0* à un floutage quasi total des détails au *Rayon : 19* puis
saute à un autre maximum au *Rayon : 20*. Il redescend ensuite lentement
jusqu'à *Rayon:100*. Graphiquement:

\[[des contrastes dans les niveaux de *1* à *3*, au fur et à mesure que
le *Rayon* augmente. Regardez les changements dans le *niveau 1*, en
particulier autour de *Rayon : 20*. Le ***Premier niveau :
Réduit***.](File:Wavelet_edge_sharpening_reduced.png%7Cthumb%7C450px%7Ccenter%7CVariation)

### Lien vers la force de la netteté des bords

Tout ce qui précède est valable tant que vous n'activez PAS l'option
*Lier à la force de la netteté des bords* (dans *Denoise and Refine*).
Ne pas l'activer signifie que des changements de contraste seront
effectués en fonction des valeurs de *Rayon* et *Détail*.

Cependant, si vous avez activé l'option *Lier à la force de la netteté
des bords*, les paramètres de force pour chaque niveau de *Denoise*
réguleront la force de l'effet dans chacun des quatre premiers niveaux
de *Netteté des bords* '. Cela vous permet d'ajuster la netteté pour
certains niveaux uniquement et d'utiliser des augmentations de contraste
nettement plus élevées que celles pouvant être obtenues avec les 10
curseurs *Contraste*.

Par exemple, vous pouvez :

- laisser le contraste *niveau 1* inchangé
- augmenter la force maximale au *niveau 2*
- réduire le contraste au *niveau 4* (*Force* négatif)

### Contraste local

Pour chaque niveau de décomposition, l'outil calcule la
[mean](https://en.wikipedia.org/wiki/Mean) et [standard
deviation](https://en.wikipedia.org/wiki/Standard_deviation) du
contraste interne du détails (aussi appelé *contraste local*) et utilise
ensuite les résultats pour des modifications ultérieures.

Rappelez-vous qu'un « détail » est en fait un groupe de pixels dans
l'image d'origine. Plus le niveau d'ondelettes est élevé, plus le groupe
est grand (au *niveau 1* un groupe est composé de 2x2=4 pixels, au
*niveau 2* 4x4=16 pixels, etc). Étant donné que chaque pixel a une
luminance initiale différente du reste des pixels dans le détail,
l'outil peut dériver et analyser le contraste interne entre les pixels.

Toute modification de ces valeurs de contraste interne ou local est
basée sur un motif (ou courbe) dérivé de la moyenne des valeurs de
contraste local dans le niveau et de leur écart type. Il est appliqué
aux valeurs locales de contraste de la même manière dans chacun des
niveaux. c'est-à-dire centré autour des valeurs moyennes de contraste.

Ainsi, par exemple, vous pouvez :

- pour des valeurs de contraste initiales faibles (généralement situées
  dans l'ombre) : réduire le contraste local pour adoucir le détail
- pour les valeurs moyennes : valorisez-les en augmentant le contraste
  local
- pour des valeurs élevées (généralement situées dans des zones très
  lumineuses) : réduire voire supprimer le contraste local, pour éviter
  de *clipper* les hautes lumières

Vous pouvez choisir entre deux commandes graphiques pour définir les
paramètres :

1.  une courbe de seuil avec quatre points mobiles qui représentent (de
    gauche à droite) le contraste minimum, la moyenne, la moyenne +
    écart-type et le contraste maximum
2.  une courbe, qui par défaut est une courbe de type gaussienne
    asymétrique, avec les caractéristiques suivantes
    - le centre de
      l'[abscissa](https://en.wikipedia.org/wiki/Cartesian_coordinate_system)
      correspond à la valeur moyenne des valeurs de contraste
    - la zone à partir du centre couvrant un tiers de la largeur du
      graphique de chaque côté correspond aux détails dont les valeurs
      de contraste sont supérieures ou inférieures à la valeur moyenne
      et se situent dans la plage de valeurs définie par l'écart type

***LA COURBE GAUSSIENNE***

<div class="parrpad">

<figure>
<img src="/images/wavelet_local_contrast_gauss.jpg"
title="wavelet_local_contrast_gauss.jpg" />
<figcaption>wavelet_local_contrast_gauss.jpg</figcaption>
</figure>

</div>

Dans ce cas, la forme de la courbe sert de guide visuel lors de la
modification des valeurs de contraste des détails. N'oubliez pas que
l'écart type des valeurs de contraste est d'un tiers à droite et d'un
tiers à gauche du centre du graphique.

Par rapport à la courbe de seuil, ce graphique permet non seulement de
modifier la plage des valeurs de contraste locales qui seront affectées
mais également l'intensité de la modification : si vous déplacez un
point de la courbe vers la droite ou vers la gauche, vous modifierez la
gamme de valeurs de contraste qui sera affectée (comme avec les points
du curseur), tandis que le déplacer vers le haut ou vers le bas
augmentera ou diminuera la force des changements de détail.

Avec la forme de courbe par défaut (que vous pouvez réinitialiser avec
le bouton
![<File:ResetButton.png>](ResetButton.png "File:ResetButton.png")),
l'effet obtenu est similaire à un
[HIRALOAM](https://www.ledet.com/margulis/Makeready/MA69-Life_on_the_Edge.pdf) :
il améliore les valeurs de contraste en contrôlant les ombres, tout en
atténuant les contrastes forts. C'est comme mettre en évidence le volume
de chaque détail, en gardant à la fois le bruit dans les ombres et la
surexposition dans les hautes lumières sous contrôle (en particulier
avec les hautes lumières spéculaires). Cependant, le grain et le bruit
des valeurs de contraste moyennes sont excessivement améliorés.

La courbe de seuil et les courbes gaussiennes donneront des résultats
différents avec leurs valeurs par défaut respectives, donc le choix
dépend de ce que vous essayez d'atteindre. Cependant, lors de
l'utilisation de la courbe gaussienne, la "force" de l'outil doit être
maintenue faible pour éviter des résultats trop exagérés. Avec la courbe
de seuil, vous pouvez utiliser des valeurs de force plus élevées tout en
obtenant des résultats « naturels ». Cependant, vous pouvez obtenir le
même effet en ajustant la courbe gaussienne, avec l'avantage
supplémentaire de pouvoir faire varier les valeurs de contraste pour les
augmenter ou les réduire, ou même les aplatir complètement en déplaçant
la courbe sous la ligne horizontale).

<div>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_o.jpg"
  title="wavelet_local_contrast_curves_o.jpg" />
  <figcaption>wavelet_local_contrast_curves_o.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_t.jpg"
  title="wavelet_local_contrast_curves_t.jpg" />
  <figcaption>wavelet_local_contrast_curves_t.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_g.jpg"
  title="wavelet_local_contrast_curves_g.jpg" />
  <figcaption>wavelet_local_contrast_curves_g.jpg</figcaption>
  </figure>

</div>

### Détection des bords

Avant de commencer à utiliser cette partie du module, vous devez ajuster
soigneusement les paramètres ci-dessus, en particulier le contraste
local. Vous ne devez apporter que des modifications subtiles, car il est
facile de générer des effets exagérés et des artefacts dans l'image.

En activant la détection des contours, le résultat obtenu sera différent
de ceux des algorithmes traditionnels (masque flou, déconvolution...),
car l'outil effectue une série d'opérations sur les détails de chaque
niveau pour mettre en évidence les contours sans accentuer le bruit : il
intensifie les détails de la décomposition, les floute pour supprimer le
bruit et sélectionne les détails considérés comme faisant partie d'un
bord.

Le processus est basé sur l'algorithme Sobel-Canny, personnalisé pour
s'adapter aux composants de la décomposition et réduire les variables
nécessaires à 3 curseurs :

- **Sensibilité au gradient** : plus vous déplacez le curseur vers la
  droite, plus l'algorithme de détection se concentrera sur les arêtes
  vives et moins il prendra en compte les valeurs de contraste locales
  des petites zones (comme le bruit ou petits détails). A l'inverse,
  déplacer le curseur vers la gauche détectera plus d'arêtes, même les
  plus petites, mais cela mettra également en évidence le bruit.
- **Seuil bas (bruit)** : ce curseur configure un [filtre
  gaussien](https://en.wikipedia.org/wiki/Gaussian_blur) qui ne modifie
  pas directement l'image, mais plutôt les coefficients de
  décomposition. À gauche, il agit sur une matrice 3x3, tandis qu'à
  droite, il agit sur une matrice 5x5 plus grande. En rendant l'image
  floue, le bruit et les détails de contraste plus fins ou plus faibles
  sont perdus ou obscurcis. C'est bon pour atténuer le bruit, mais cela
  entraîne également une détection des contours moins précise. Plus le
  curseur est à droite, mieux le bruit sera atténué, mais moins de
  contours seront détectés. Une valeur autour de 3x3 est meilleure pour
  détecter les bords fins, mais est plus sujette aux interférences dues
  au bruit. Une valeur de 5x5 est préférable pour les bords plus larges
  ou plus proéminents, au prix de la perte des bords plus fins et de la
  détection moins précise.

De plus, dans une étape ultérieure de l'algorithme, ce seuil supprimera
les bords qui, bien que détectés, sont peu susceptibles d'être de vrais
bords. Plus ce seuil est bas, plus il détectera les bords à faible
contraste. Cependant, il sera également plus susceptible d'interpréter
le bruit comme un bord probable.

- **Seuil haut (détection)** : une fois les contours de l'image
  détectés, ce curseur permet à l'outil d'analyser la fiabilité de la
  détection des contours (c'est-à-dire s'il s'agit d'un contour net ou
  flou) puis soit atténuer ou améliorer les changements de contraste
  locaux en fonction de la netteté du bord. Déplacer le curseur vers la
  droite augmentera le contraste des arêtes vives et le déplacer vers la
  gauche l'atténuera.

### Algorithme amélioré

L'activation de cette partie du module vous permet de configurer
certains aspects de l'algorithme de détection des contours :

- Sensibilité des bords : cette valeur vous permet d'ignorer les détails
  qui n'ont pas un contraste supérieur à la valeur définie par le
  curseur. Plus le curseur est déplacé vers la droite, plus le contraste
  des détails doit être élevé pour qu'ils soient considérés comme un
  bord possible (les bords à faible contraste seront ignorés).
- Amplification de base : ce curseur intensifie les valeurs initiales
  avant de commencer les calculs pour améliorer la détection des
  contours. Plus on est à droite, meilleure est la distinction entre
  *edge* et *non-edge*, mais plus le risque d'artefacts est grand.
- Pixels voisins : vous décidez ici de l'influence que les pixels
  entourant le détail auront sur la détection des contours. Vous avez 3
  options : *Aucun*, *Bas*, *Elevé*.

### Exemple (modification de la réduction du bruit et de la netteté des contours)

<div>

- 

<figure>
<img src="/images/wavelet_edge_sharpness.jpg"
title="wavelet_edge_sharpness.jpg" />
<figcaption>wavelet_edge_sharpness.jpg</figcaption>
</figure>

</li>
</ul>
</div>

## Module Niveaux de flou (Blur)

Ce module permet de flouter sélectivement (« défocaliser ») les détails
des niveaux sélectionnés. Le résultat est plus fort dans les niveaux
supérieurs (à partir du *niveau 7*) et est particulièrement utile en
astrophotographie.

Le curseur ***Réponse d'atténuation*** agit comme décrit dans le
[chapitre sur l'atténuation du module
Contraste](#Le_concept_"Attenuation_curve".md).

La courbe ***Flou par niveaux*** modifie la luminance de chaque niveau :
elle est divisée en 10 zones, avec *niveau 1* à gauche et *Extra* à
droite. Augmenter la courbe dans la zone d'un niveau augmentera le flou
pour ce niveau particulier.

Le curseur ***Blur Chroma*** mélange les couleurs avec leur
environnement, créant un effet de bavure subtil. Elle agit sur les mêmes
niveaux définis par la courbe précédente.

## Module Sharp-mask et Clarity

La fonction *Sharp mask* est une nouvelle façon d'améliorer la netteté
aux côtés des autres méthodes disponibles dans RawTherapee (c'est-à-dire
*Unsharp Mask*, *Deconvolution* et *Wavelet Levels Edge Sharpness*). Il
peut être utilisé en conjonction avec eux ou seul.

Le *Unsharp mask* est la méthode traditionnellement utilisée pour
accentuer les bords et augmenter l'impression de netteté d'une image :
elle repose sur la création d'un masque flou de type Gaussien généré en
prenant chaque pixel et en brouillant récursivement le voisin pixels. Ce
masque est ensuite soustrait de l'image d'origine pour accentuer les
bords. Les rayons utilisés avec cette méthode sont généralement petits
(de l'ordre de moins de 1 à quelques pixels).

Le masque de ce module est basé sur une partie de la décomposition en
ondelettes et peut être utilisé de deux manières :

- amélioration des niveaux plus fins à l'aide de l'option **Sharp
  mask**.
- amélioration des niveaux plus grossiers à l'aide de l'option
  **Clarté**, qui augmente l'impression de contraste local et de
  saturation locale dans l'image.

Lorsque vous activez le module, la configuration générale de l'outil
passe automatiquement à :

|               | Sharp Mask                    | Clarté                             |
|---------------|-------------------------------|------------------------------------|
| Arrière plan: | Image résiduelle              | Image résiduelle                   |
| Niveaux:      | Niveaux avec des détails fins | Niveaux avec des détails grossiers |
| Niveau:       | 3                             | sept                               |

Dans les deux cas, vous pouvez modifier le *niveau* de référence. Dans
le cas du *Sharp Mask*, le changement de niveau est similaire au
changement de rayon dans le *Unsharp Mask* et vous pouvez choisir
n'importe quel niveau entre *1* et *4*. Pour *Clarté* un changement de
niveau se traduit par un effet *volume tridimensionnel* plus ou moins
important sur l'image. Dans ce cas, vous pouvez sélectionner les niveaux
de *5* à *Extra*.

Lorsque vous désactivez le module, les valeurs de *fusion* ne sont pas
perdues et vous n'aurez qu'à re-sélectionner le *niveau* souhaité
lorsque vous réactivez le module.

La *fusion* dans le *Sharp Mask* consiste à rehausser les détails sous
le niveau sélectionné et à fusionner (mélange) le résultat avec les
niveaux restants : si vous avez sélectionné *niveau 3*, les détails des
niveaux *1*, *2* et *3* seront améliorés puis fusionnés avec les niveaux
4 et supérieurs (y compris l'image résiduelle). Le curseur *merge* vous
permet d'ajuster le mix, en donnant plus ou moins de pertinence aux
détails améliorés par rapport au reste de l'image.

De même, dans le cas de *Clarté*, les niveaux les plus grossiers sont
améliorés et fusionnés avec le reste de la photo.

Dans les deux cas vous avez 3 curseurs pour ajuster les changements :

1.  *Merge Luma* : en le déplaçant vers la droite (valeurs positives) le
    contraste des détails est renforcé, tandis qu'avec des valeurs
    négatives l'image devient *floue, comme dans un rêve*.
2.  *Merge Chroma* : en le déplaçant vers la droite (valeurs positives)
    les tons saturés sont plus rehaussés que les tons moins saturés
    (pastel). Avec des valeurs négatives, l'image devient moins vive et
    les tons pastel restent pratiquement inchangés.
3.  *Soft Radius* : des valeurs de fusion élevées peuvent générer des
    halos autour des zones contrastées. Avec ce contrôle, vous pouvez
    les lisser sans trop affecter l'image. Cependant, il a des effets
    secondaires : les zones sombres deviennent plus sombres et de plus
    en plus de zones seront considérées comme n'ayant pas suffisamment
    de contraste pour être rehaussées, elles resteront donc inchangées.

<div>

- ![](wavelet_smc_original.jpg "wavelet_smc_original.jpg")\]

- <figure>
  <img src="/images/wavelet_sharpm_ML60MC30.jpg"
  title="wavelet_sharpm_ML60MC30.jpg" />
  <figcaption>wavelet_sharpm_ML60MC30.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_clarity_ML60MC30.jpg"
  title="wavelet_clarity_ML60MC30.jpg" />
  <figcaption>wavelet_clarity_ML60MC30.jpg</figcaption>
  </figure>

</div>

Enfin, sous le *Soft Radius* vous avez l'option *Show wavelet 'mask*',
ce qui vous permet de voir quels détails seront améliorés :

- dans le cas du *Sharp Mask*, une image s'affichera avec un fond noir
  et les détails seront surlignés en blanc (si vous avez déjà vu un
  *Unsharp Mask*, vous le trouverez similaire) .
- cependant, avec l'option *Clarté*, le masque est différent et est basé
  sur [Guided Image Filtering](http://kaiminghe.com/eccv10/) et est
  moins intuitif. En général, ce sont les zones blanches (bien que
  floues) qui seront mises en valeur.

## Image résiduelle

L'image résiduelle correspond à l'image d'origine moins les détails qui
ont été extraits dans les niveaux. Toute modification apportée aux
niveaux n'aura donc aucun effet sur l'image résiduelle et plus vous
sélectionnez de niveaux dans les paramètres généraux de l'outil, plus la
différence entre l'original et l'image résiduelle est importante. De
plus, lorsque vous sélectionnez plus de 6 niveaux, l'image résiduelle ne
contiendra presque pas de bruit, donc la modification du contraste
global ou de la chromaticité dans l'image résiduelle n'aura presque
aucun effet sur le bruit.

<div>

- ![](wavelets_residual_original.jpg "wavelets_residual_original.jpg")\]

- <figure>
  <img src="/images/wavelets_residual_L5.jpg" title="wavelets_residual_L5.jpg" />
  <figcaption>wavelets_residual_L5.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_L7.jpg" title="wavelets_residual_L7.jpg" />
  <figcaption>wavelets_residual_L7.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_L8.jpg" title="wavelets_residual_L8.jpg" />
  <figcaption>wavelets_residual_L8.jpg</figcaption>
  </figure>

</div>

Il est important de noter que pour éviter les artefacts et les tons hors
[gamut](https://en.wikipedia.org/wiki/Gamut), vous devrez observer de
près les ajustements que vous faites sur chacun des niveaux et sur
l'image résiduelle : si l'image d'origine a déjà des tons proches des
limites de l'espace colorimétrique, une augmentation significative du
contraste ou de la chromaticité du détail entraînera presque
inévitablement des artefacts ou des tons en dehors de la gamme de
couleurs. Dans ce cas, augmenter ou diminuer le contraste et la
chromaticité résiduels de l'image vous permettra de conserver les
couleurs dans la plage définie par l'espace colorimétrique.

Comme vous pouvez le voir, les ajustements d'image résiduelle sont un
aspect fondamental du traitement au niveau des ondelettes. Ils vous
permettent de :

- travailler avec les ombres et les hautes lumières quels que soient les
  détails qu'elles contiennent,
- réduire le contraste global et la chromaticité, pour mieux percevoir
  le micro-contraste,
- modifier la chromaticité pour réduire les artefacts résultant de
  modifications excessives des niveaux (par exemple dans le ciel)
- etc

### Ombres/lumières de l'image résiduelle

Le déplacement des curseurs des ombres et des hautes lumières vers la
droite augmente la luminance de ces zones ; vers la gauche (valeurs
négatives), il le réduit. Cela peut être utilisé pour assombrir
davantage les ombres et augmenter la luminosité des hautes lumières :

<div>

- <figure>
  <img src="/images/wavelets_residual_original.jpg"
  title="wavelets_residual_original.jpg" />
  <figcaption>wavelets_residual_original.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SH.jpg" title="wavelets_residual_SH.jpg" />
  <figcaption>wavelets_residual_SH.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SH-out.jpg"
  title="wavelets_residual_SH-out.jpg" />
  <figcaption>wavelets_residual_SH-out.jpg</figcaption>
  </figure>

</div>

L'effet de ces changements est influencé par les curseurs de seuil, qui
ont une échelle de luminance allant de *0* à *100* : pour les ombres,
déplacer le curseur de seuil vers la gauche limitera progressivement
l'action du curseur aux valeurs de luminance les plus sombres. De même
pour les hautes lumières, déplacer le curseur de seuil vers la droite
limitera progressivement l'action du curseur de hautes lumières aux
valeurs de luminance les plus élevées. Pour vous aider à décider des
valeurs de seuil à utiliser, vous pouvez vérifier les valeurs de
luminance en passant la souris sur la zone pertinente de l'image et en
lisant la valeur de luminance L\* dans le panneau Navigateur. Ces
valeurs correspondent directement à l'échelle utilisée pour les curseurs
de seuil.

- les valeurs négatives ont un fort impact sur l'image résiduelle
- les surbrillances sont assombries si des valeurs négatives sont
  utilisées
- les surbrillances sont éclaircies si des valeurs positives sont
  utilisées
- les ombres sont assombries si des valeurs négatives sont utilisées
- les ombres deviennent plus claires si des valeurs positives sont
  utilisées

<div>

- <figure>
  <img src="/images/wavelets_residual_SHneg_original.jpg"
  title="wavelets_residual_SHneg_original.jpg" />
  <figcaption>wavelets_residual_SHneg_original.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SHneg_old.jpg"
  title="wavelets_residual_SHneg_old.jpg" />
  <figcaption>wavelets_residual_SHneg_old.jpg</figcaption>
  </figure>

- ![](wavelets_residual_SHneg_new.jpg "wavelets_residual_SHneg_new.jpg")
  \</ li\>

</div>

La dernière option de ce groupe est le *Radius Shadows/Highlights*.
Remarque : ce curseur sera masqué lorsque l'option *Algorithme utilisant
des valeurs négatives* est activée.

Ce curseur applique [Guided Image
Filtering](http://kaiminghe.com/eccv10/) qui atténue les transitions
dans les ombres et les hautes lumières causées par les ajustements
précédents. Il contrôle la zone d'influence des ajustements effectués
dans les ombres et les hautes lumières pour améliorer leur intégration
dans le reste de l'image.

Vous pouvez ajuster les ombres et les hautes lumières pour :

- ajouter de l'impact aux objets brillants,
- éviter que les hautes lumières ne saturent,
- lever les ombres,
- etc

### Compression du contraste de l'image résiduelle

C'est l'un des aspects clés du traitement au niveau des ondelettes : le
curseur ***Contraste*** vous permet de modifier le contraste de l'image
résiduelle séparément des changements de contraste des détails dans les
niveaux.

Des réductions modérées du contraste résiduel de l'image feront
ressortir plus clairement le contraste des détails et donneront une plus
grande impression de profondeur et de relief. Cela vous permet de
limiter les augmentations de contraste pour les détails afin d'éviter de
générer des artefacts et en même temps, de produire un effet
visuellement équivalent à une augmentation plus importante.

Cependant pour certaines images, des changements drastiques dans le
contraste de l'image résiduelle vous permettront d'obtenir des effets
intéressants :

<div>

- <figure>
  <img src="/images/wavelets_residual_contrast-.jpg"
  title="wavelets_residual_contrast-.jpg" />
  <figcaption>wavelets_residual_contrast-.jpg</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_contrast+.jpg"
  title="wavelets_residual_contrast+.jpg" />
  <figcaption>wavelets_residual_contrast+.jpg</figcaption>
  </figure>

</div>

Pour vous aider à contrôler l'effet de ce module, il existe un ensemble
d'options qui vous permettent d'ajuster la plage dynamique de l'image
résiduelle. Ces options sont regroupées en *Compression du contraste* et
*Compression du mappage des tons*.

#### Méthode de compression : Contraste

Les effets du curseur de contraste sont immédiatement visibles et
varient presque linéairement en fonction de la position du curseur :
vers la droite le contraste augmentera et vers la gauche il diminuera.
L'action du curseur est limitée en interne pour éviter les artefacts.

La **Force de compression** modifie la plage dynamique de l'image
résiduelle : déplacer le curseur vers la droite la réduit (les ombres
sont éclaircies et les hautes lumières sont réduites) et vers la gauche,
l'augmente (les ombres sont assombries et les hautes lumières sont
légèrement intensifié).

La **Compression gamma** modifie la répartition de la lumière et de
l'ombre, déplaçant efficacement l'histogramme vers la gauche ou la
droite.

Avec ces commandes, vous pouvez, par exemple, réduire les effets de
brouillard ou compresser la plage dynamique des images à plage dynamique
élevée.

#### Méthode de compression : Tone Mapping

Dans ce cas, la méthode de compression utilisée est la même que celle de
l'outil [Tone Mapping](Tone_Mapping.md) et ses curseurs agissent
de la même manière. Il n'agit que sur l'image résiduelle et va modifier
en profondeur le contraste (à la manière du Tone Mapping). Pour cette
raison, vous devrez très probablement également réajuster tout
changement de niveau pour vous assurer que l'image globale reste
équilibrée.

Bien que vous appliquiez le tone mapping à l'image résiduelle, cela ne
vous empêche pas d'activer également l'outil global *Tone Mapping*. Dans
ce cas, il faut faire attention car l'utilisation simultanée des deux
outils peut générer des artefacts.

### Flou

Ce groupe de deux curseurs peut sembler anodin, mais il peut être une
aide intéressante pour améliorer le
[bokeh](https://en.wikipedia.org/wiki/Bokeh) de l'image, en floutant la
luminance de l'image résiduelle (***Blur Luminance***) et sa composante
de couleur (***Blur Chroma***).

Le résultat est étroitement lié aux valeurs et au nombre de [Niveaux
d'ondelettes](#Niveaux_d'ondelettes.md) : pour obtenir un bon
bokeh, il faut pouvoir ajuster la quantité de détails dans l'image selon
que l'on veut que l'arrière-plan être partiellement reconnaissable ou
complètement flou.

Normalement, les meilleurs résultats seront obtenus avec 7 niveaux
d'ondelettes ou plus et avec des valeurs de flou modestes (autour de
*50*), car il est facile de générer des halos et des artefacts avec des
niveaux inférieurs ou des valeurs extrêmes.

#### Teinte du ciel

Le titre fait référence à la *teinte du ciel*, mais vous n'êtes pas
limité aux couleurs du ciel et pouvez ajuster les tons de couleur sans
limitation. Comme mentionné précédemment, les couleurs sont liées au
contrôle *Intensité*.

La plage par défaut couvre les nuances habituelles de bleu dans le ciel.

#### Ciblage/protection du ciel

Avec ce contrôle vous pouvez décider si vous souhaitez modifier, la
chrominance des zones contenant des couleurs définies dans la gamme
précédente :

- avec le curseur sur *0*, les modifications apportées au contrôle de la
  chrominance seront appliquées de la même manière à tous les tons de
  l'image
- la sélection de *-100* (glissant vers la gauche) centre les
  changements de chrominance dans la gamme tonale sélectionnée
- au contraire, sélectionner *100* (coulissant vers la droite) modifiera
  les tonalités qui *ne* correspondent pas à la plage sélectionnée.

Dans les positions intermédiaires entre *0* et *±100* les changements se
font progressivement vers la gamme choisie, ou vers le reste des
tonalités.

Ce contrôle est très utile pour éviter la sursaturation des tons de peau
humaine, ce qui se traduit par un «look carotte» immédiatement
perceptible.

### Courbe d'image résiduelle

Il s'agit d'une courbe plate avec des lignes verticales colorées et des
points coulissants et est indépendante de la *gamme de teintes du ciel*
et du contrôle d'intensité de chrominance : vous pouvez l'utiliser pour
modifier les tons afin qu'ils prennent une couleur dominante,
indépendamment de la reste des commandes du module.

Cela fonctionne comme suit : si vous déplacez un point vers le haut, les
zones de l'image avec la couleur de cette ligne particulière prendront
la teinte de la ligne immédiatement à droite. Si vous le déplacez vers
le bas, la dominante sera la couleur de la ligne immédiatement à gauche.
Par exemple : en déplaçant le point du trait jaune vers le haut, les
zones jaunes de l'image résiduelle prendront une teinte verdâtre (le
trait à droite du jaune), alors que si vous déplacez le point vers le
bas, la dominante sera orange (la ligne à gauche du jaune). En savoir
plus sur ce texte sourceVous devez indiquer le texte source pour obtenir
des informations supplémentaires Envoyer des commentaires Panneaux
latéraux

### Toning et équilibre des couleurs

L'activation de cette option présente 3 paires de commandes de tonalité
pour *Highlights*, *Midtones* et *Shadows*, respectivement, qui peuvent
être utilisées pour colorer l'image résiduelle.

Les contrôles modifient les composants *a\** et *b\** de l'espace
colorimétrique Lab, donc les changements seront :

- pour le composant *a\** = du vert au magenta
- pour le composant *b\** = du bleu au jaune

Les résultats dépendront de l'intensité des changements :

- avec des valeurs élevées, vous pouvez créer des effets spéciaux,
  similaires à ceux obtenus avec le *Module Chroma*, mais axés sur
  l'image résiduelle. Vous pouvez l'utiliser en combinaison avec ce
  module si vous le souhaitez
- avec des valeurs modérées, vous pouvez corriger manuellement la
  balance des blancs : par exemple, imaginez une scène où les principaux
  détails sont dans une zone ombragée qui a une dominante de couleur
  bleue et l'arrière-plan est en plein jour et a une température de
  couleur différente. Dans ce cas, vous pouvez ajuster la balance des
  blancs pour les détails (et supprimer la dominante bleue) puis
  réajuster le fond (l'image résiduelle) et personnaliser la balance des
  blancs pour chaque zone (hautes lumières, demi-teintes et ombres)

Notez que les contrôles de compression du contraste résiduel de l'image,
qui modifient les valeurs de luminance de chaque zone, auront une
influence directe sur les résultats obtenus avec cette partie du module.
En savoir plus sur ce texte sourceVous devez indiquer le texte source
pour obtenir des informations supplémentaires Envoyer des commentaires
Panneaux latéraux

## Retouche finale

Dans ce module, vous pouvez appliquer de petits ajustements de retouche
à l'image. Cependant, comme il est situé à la fin de l'outil Niveaux
d'ondelettes, toute modification importante effectuée ici peut
nécessiter un réajustement du reste des modules.

### Contraste directionnel

En général, l'équilibre initial entre les 3 composantes directionnelles
de la décomposition de l'image est respecté dans l'ensemble de l'outil :
verticale, horizontale et diagonale. Cependant, avec ce module, vous
pouvez augmenter le poids de l'un par rapport à l'autre, pour obtenir un
résultat différent.

#### Méthode d'équilibre du contraste

Ce contrôle *balance* modifie l'équilibre entre la décomposition
diagonale d'une part et la décomposition verticale et horizontale
d'autre part. Son principe est similaire à celui de la [edge-preserving
decomposition](http://www.cs.huji.ac.il/~danix/epd) qui se base sur la
[Factorisation de
Cholesky](https://fr.wikipedia.org/wiki/Factorisation_de_Cholesky#:~:text=La%20factorisation%20de%20Cholesky%2C%20nomm%C3%A9e,%C2%AB%20racine%20carr%C3%A9e%20%C2%BB%20de%20A..md)
et modifie linéairement les valeurs de luminance de l'image.

Ce module vous permet de modifier les effets des modules suivants :
Contraste, Chroma et Residual Image Tone Mapping.

Vous avez deux choix :

- Curseur : avec cette option, le contrôle ***Balance du contraste
  d/v-h*** apparaît vous permettant de modifier les valeurs de contraste
  dans l'image. Le déplacer vers la droite intensifie le contraste
  global de l'image, tandis que le déplacer vers la gauche réduit le
  contraste. Gardez à l'esprit que vous agissez sur l'équilibre entre
  les différentes directions de décomposition, donc avec des valeurs
  extrêmes, vous introduirez des artefacts importants.
- Courbe : Dans ce cas apparaît la courbe ***Courbe de balance contraste
  d/v-h*** qui agit sur la balance des valeurs de luminance de l'image.

Dans les deux cas, il y a un contrôle supplémentaire : **Niveaux
d'équilibre delta**. Lorsqu'il est défini sur zéro (par défaut), tous
les niveaux de la décomposition sont traités de la même manière. S'il
est placé à gauche, les niveaux inférieurs sont accentués (les détails
fins) et les niveaux supérieurs sont réduits (ceux qui donnent du volume
à l'image). En revanche, s'il est placé à droite, les niveaux inférieurs
sont réduits et les niveaux supérieurs sont augmentés.

Vous avez également à votre disposition un curseur ***Attenuation
Response***, qui agira comme décrit dans le [chapitre sur l'atténuation
du module Contraste](#Le_concept_"Attenuation_curve".md).

Enfin l'option ***Balance chrominance*** permet de modifier la balance
d/v-h des composantes chromatiques de la décomposition en utilisant les
mêmes contrôles que ci-dessus (curseur ou courbe).

### Contraste local final

Cette courbe est située à la fin du pipeline de traitement, juste avant
la recomposition et agit de manière non linéaire sur le contraste des
niveaux de décomposition.

A noter que cette courbe, qui agit sur le contraste local initial et non
sur la luminance, ne fait pas double emploi avec la précédente
(*Contrast balance*).

Sur le graphique, le centre de l'abscisse correspond à la valeur moyenne
du contraste local et au tiers de chaque côté se trouve un point
correspondant à la moyenne plus un écart-type des valeurs de contraste
local. En changeant la forme de la courbe vous diminuerez ou augmenterez
les effets du module de *Contraste*, de la *Netteté des contours*, de la
*Méthode Balance* et même du principe même de décomposition -
recomposition.

Par défaut, la courbe est *plate* (c'est-à-dire qu'elle n'a aucun
effet), bien que vous puissiez la modifier à votre guise, par ex.
réduire davantage la valeur des contrastes locaux faibles et ainsi
adoucir la visibilité du bruit, ou réduire les valeurs des contrastes
locaux élevés et éviter les artefacts.

De plus, il y a aussi un curseur ***Attenuation Response***, qui agira
de la même manière expliquée dans le [chapitre sur l'atténuation du
module Contraste](#Le_concept_"Attenuation_curve".md).

### *Après* Courbe de Contraste

Cette courbe n'est pas liée aux courbes précédentes. Il se situe à la
fin du pipeline de traitement des niveaux d'ondelettes, après la
recomposition des niveaux plus l'image résiduelle, et permet de modifier
le contraste global de l'image.

Elle agit sur la luminance et son utilisation est similaire aux autres
courbes tonales trouvées dans RawTherapee, bien que dans ce cas vous ne
verrez pas d'histogramme de fond.

Enfin, vous disposez également d'un curseur ***Rayon doux*** qui vous
permet d'appliquer un flou aux zones sélectionnées afin qu'elles se
fondent mieux dans l'image.

## Questions - Réponses

### Une autre lecture de Rawpedia

Je propose au lecteur une autre manière de lire les paragraphes
précédents avec une logique différente, probablement autant, voire plus
technique, mais plus proche de l'utilisation.

#### Les ondelettes quel intérêt pour la photographie ?

A quoi cela sert ? c'est quoi ? c'est difficilement compréhensible !
Lorsqu'on agit sur un curseur selon le cas il ne se passe rien ou alors
des artefacts apparaissent, etc. etc. Telles sont les commentaires qu'on
retrouve à propos de Rawtherapee Wavelet ! Alors effectivement c'est
quoi ?

1.  en imagerie traditionnelle, tout est en 2 dimensions (largeur -
    hauteur), chaque pixel / zone est caractérisée d'une part par ses
    coordonnées et d'autre part par des données RGB ou Lab qui
    conditionnent directement luminance, contraste, saturation. Bien sûr
    il existe pour certains logiciels des possibilités de modifications
    locales via ou non par des calques, mais quelque soit le nombre de
    calques ou leurs caractéristiques on intervient toujours de manière
    globale (même si la zone est petite) en 2 dimensions.
2.  avec les ondelettes c'est totalement différent...on peut parler de
    pseudo-3D. Bien sûr on conserve les coordonnées (on ne voit pas
    comment on pourrait s'en passer!), mais au lieu d'avoir une
    description linéaire, on obtient par décomposition une
    représentation avec, d'une part, une image résiduelle (aux
    caractéristiques proches de l'image originale en tant que support)
    et, d'autre part, autant de niveaux que l'image peut en contenir.
    Ces différences qui se traduisent dans chaque niveau (contraste et
    chroma) proviennent : a) du bruit numérique ; b) des différences de
    contrastes (chroma) dues aux effets de bords; c) des différences de
    contraste (chroma) dues à la brume ou autres phénomènes optiques dus
    à la scène.

Alors bien sûr la logique de traitement sera différente...c'est
évident...Ce n'est ni plus, ni moins complexe - sinon le degré de
complexité due à la 3ème (pseudo) dimension - qu'une imagerie
traditionnelle. Mais évidemment les algorithmes seront spécifiques,
différents de l'imagerie traditionnelle, et bien sûr nécessitent un
apprentissage. Ici on intervient sur chaque niveau, sachant qu'un niveau
n'a des informations que si et seulement si, il y a des variations de
luminance / chroma. Une zone d'aplats donnera toujours 0 au niveau de la
décomposition.

On voit immédiatement l’intérêt (ou non) de cette décomposition : la
possibilité d'intervenir séparément sur la zone de contraste (chroma)
globale (image résiduelle) et chacun des niveaux. L'action (plus
habituelle) sur les niveaux va permettre par exemple de réduire le
bruit, ou accroître de manière différenciée le contraste pour aboutir à
des effets de relief ou de perspective...

Dans le cas de Rawtherapee nous nous servons d'un algorithme de
décomposition performant (Daubechies) qui permet notamment pour chaque
pixel et chaque niveau l'utilisation de 3 directions (horizontale -
verticale - diagonale). Cette 3ème dimension fera souvent la différence
avec d'autres logiciels utilisant les ondelettes. De plus, les
algorithmes utilisés ne se limitent pas - comme dans beaucoup de
logiciels 'wavelet' - aux curseurs de modifications du contraste (et/ou
chroma), mais permettent des actions différenciées :

1.  à l'intérieur de chaque niveau
2.  entre les niveaux
3.  pour l'image résiduelle
4.  pour le traitement global de l'image

Afin d’acquérir des possibilités en termes de "tone-mapping", "réduction
des effets de brume", accentuation, etc.

Alors, bien sûr, on pourra dire que cela ajoute de la complexité...C'est
vrai, mais pourquoi se priver de fonctionnalités qui vont amener de
nouvelles possibilités logicielles !

#### Les ondelettes est-ce complexe ? Cela va-t-il changer nos habitudes ?

Est-ce complexe ? : oui et non...

1.  oui : car cela change nos habitudes et oblige à penser 3D
2.  non : car une fois qu'on a compris le principe, ce n'est pas plus
    complexe (et je pense - moins complexe) que par exemple les calques
    de Photoshop.

Alors bien sûr cela va changer nos habitudes...Mais rappelez vous il y a
quelques années vos premières retouches avec un logiciel de traitement
d'image : qu'est-ce que c'est que ce truc..le mode RGB, le mode Lab, les
pixels, etc. Celui qui me dit que Photoshop est simple et que la
création - gestion des calques est évident...pourra très facilement
s'adapter aux fonctionnalités des ondelettes.

Tout est question d'apprentissage et d'habitudes, sachant que dans ce
cas, on introduit de nouvelles données!

Alors ? que faire ?

1.  travailler par essais-erreurs ? pourquoi pas, mais de manière
    limitée afin d'enrichir une démarche 'logique'
2.  il y a des principes de base à connaître développés dans Rawpedia et
    dans ce complément qui doivent guider l'action et limiter ces
    essais-erreurs aux premières expérimentations ou à certaines
    améliorations.

#### Quels sont les ondelettes utilisées par Rawtherapee, incidences des réglages ?

Rawtherapee, utilise la décomposition en ondelettes discrètes selon la
méthode de Daubechies, qui permet notamment la décomposition en 3
directions. Ce que ne permet pas la méthode (plus simple) du chapeau
Mexicain utilisée par une majorité de logiciels du marché.
Actuellement - tant qu'un processus de retouche locale performant ne
sera pas implanté dans Rawtherapee - la méthode de Kingsbury, nettement
plus performante au niveau des détails, mais considérablement plus
exigeante en ressources, ne sera pas implémentée.

Rawtherapee, permet de choisir :

1.  le nombre de niveaux de décomposition : de 2 à 10. Plus le nombre
    est petit et plus l'image résiduelle sera "proche" de
    l'originale...et plus les réglages seront intuitifs, par contre plus
    les possibilités liées aux ondelettes seront peu utilisées. Plus le
    nombre sera grand, plus importantes seront les retouches possibles
    (jusque des détails de 1024\*1024 pixels), notamment pour déboucher
    des ombres...
2.  le niveau ondelettes Daubechies : par défaut il est à 4 (D4) ce qui
    doit convenir dans la majorité des cas. Modifier ce niveau va
    permettre - sans que j'ai pu trouver une corrélation évidente -
    d'affiner la qualité des niveaux faibles (la littérature
    universitaire affirme que le meilleur rendu des détails est obtenu
    avec D2), ou celle de l'image résiduelle.

#### Peut-on avoir un idée de ce qui est contenu dans chaque niveau de décomposition ?

Bien sûr et c'est très simple, il suffit d'entrer dans la rubrique
"Wavelet settings" et de sélectionner selon son souhait. Par exemple
sélectionner Background : grey (pour mieux percevoir les détails, car la
réalité de la décomposition est un fond noir)et Process : below or
equal, et level 3, permettra de visualiser le contenu des niveaux 1, 2
et 3. Attention, les choix faits ici se répercutent sur la
prévisualisation (ce que l'on voit dans l’aperçu) mais aussi sur l'image
de sortie et sur l'histogramme.

Cet histogramme va permettre de guider les actions notamment l'incidence
des ajustements sur l'image résiduelle.

#### Avec une décomposition en ondelettes lorsqu'on parle de contraste, c'est quoi ?

Comme dirait quelqu'un : "c'est une très bonne question et je vous
remercie de l'avoir posée"...

En imagerie traditionnelle, le contraste est toujours global (même au
niveau élémentaire), l'action du contraste va modifier les
caractéristiques des valeurs RGB (ou Lab) des pixels concernés ou
avoisinants.

Ici, en ondelettes, c'est différent et même totalement différent :

1.  chaque niveau de décomposition (pour 2x2 pixels..jusque 1024x1024)
    contient les valeurs de contraste local pour chaque pixel. Si il n'y
    a pas de contraste le niveau est à zéro, si le contraste est faible
    ou moyen (par exemple pour du bruit de luminance), on aura des
    valeurs (si on parle en valeurs L\*a\*b\* utilisée dans
    Rawtherapee - valeurs réelles comprises entre 0 et 32768 pour L) aux
    environs de 100 à 400. La valeur moyenne, qui bien sûr dépend de
    chaque image et de chaque niveau sera souvent comprise vers des
    valeurs de 400 à 600. Les valeurs maximales seront souvent aux
    environ de 5000 à 10000. Le spectre de ces valeurs est constituées
    de données négatives et positives et chaque 'groupe' est traité
    séparément dans les algorithmes.
2.  Lorsqu'on agit sur le curseur d'un niveau on accroitra les valeurs
    de chaque niveau de manière homothétique. Par exemple une valeur
    faible située à 100 avant action sur le curseur passera à 150, la
    valeur moyenne située à 500 passera à 750, la valeur maxi qui était
    à 6000 passera à 9000. On voit immédiatement les limites de cette
    action - même si dans une majorité de cas elle est pertinente - les
    valeurs faibles souvent liées au bruit seront amplifiées...d'où
    accroissement du bruit visible, les valeurs très élevées (souvent
    liées aux bords) seront trop accentuées, d'où apparition
    d'artefacts.
3.  Il apparaît à l'évidence, 2 modifications possibles des algorithmes
    : a) en fonction de la luminance de l'image initiale, pour cibler
    l'action sur une plage de luminance; b) en fonction du contraste
    local initialement présent, pour différencier l'action selon le
    contraste initial (celui qui précède l'action en cours) et permettre
    ainsi d'accroître le contraste local, sans ajouter de bruit ou
    d'artefacts.

Ces modifications sont possibles :

- pour la luminance dans le menu "Contrast" avec les curseurs "Highlight
  luminance range" et "Shadow luminance range"
- pour la luminance dans le menu "Final Touchup" pour l'image recomposée
  (niveaux + résiduelle) avec la courbe "Final contrast"
- pour le contraste local dans le menu "Edge sharpness" avec la courbe
  ou le curseur "Local contrast"
- pour le contraste local dans le menu "Final Touchup" avec la courbe
  "Final contrast". Dans ce cas à titre d'exemple les valeurs reprises
  ci-dessus 150 pourra devenir 50, la valeur moyenne de 750 pourra
  devenir 1000, et la valeur maxi pourra passer de 9000 à 7000.

Il est également important de signaler que le contraste de l'image
recomposée (finale) sera la somme (même si ce n'est pas une somme
arithmétique exacte) entre la valeur des contrastes locaux pour chaque
niveau et le contraste global de l'image résiduelle. Il semble évident
que dans une majorité de cas, afin d'éviter les artefacts et les
dépassements de gamut, lorsqu'on augmente significativement les
contrastes locaux par les curseurs niveaux, il faut corrélativement
abaisser le contraste de l'image résiduelle (et réciproquement). On peut
le vérifier, en partie, avec l'histogramme général et celui de l'image
résiduelle.

#### Avec une décomposition en ondelettes lorsqu'on parle de chroma, c'est quoi ?

On peut faire ici exactement les mêmes remarques, commentaires à propos
de la chroma qui devient 3D, exactement comme le contraste, pas de
différences sinon qu'au lieu d'utiliser L\* on utilise sqrt(a\*a +
b\*b).

Par contre il n'y a pas de courbes :

- de correction de la chroma en fonction de la chroma locale (équivalent
  de la courbe de edge-sharpness), pas plus que celle de "Final touchup"
- de correction de la chroma de l'image reconstituée dans "Final
  touchup".

Bien sûr, il est possible, si les utilisateurs le souhaitent, de les
ajouter...mais cela accroît la complexité!

#### Pourquoi est-il difficile voire impossible de passer des réglages d'une image à une autre ?

Il n'est pas impossible de passer les paramètres via un pp3
(partialpaste, etc.), mais ils ne produiront pas les mêmes effets. En
effet comme expliqué plus haut, les structures du contraste et de la
chroma ne sont pas les mêmes qu'en imagerie traditionnelle, et donc tout
va dépendre de l'image...Je ne pense pas qu'il y ait de différences
profondes liées au type de fichiers (NEF, CR2, PEF, etc.)

La différence va provenir pour l'essentiel de l'éclairage de la scène au
moment de la prise de vue :

- y-a-t-il du voile atmosphérique: celui-ci va modifier la répartition
  entre l'avant plan et l'arrière plan, réduisant le contraste des
  sujets lointains, en accentuant l'écart avec l'avant plan ,
- y-a-t-il des différences d'illuminants ou d'exposition qui a leur tour
  vont changer les rapports entre les divers plans ?
- y-a-t-il des zones où la détection des bords va être amplifiée...par
  la nature des teintes, par exemple un paysage avec de grosses zones de
  tons neutres avec de forts contrastes ?
- etc.

Bien sûr il y aura des moyens pour réduire ou accroitre ces écarts, mais
ils ne permettront pas une portabilité facile

#### Pourquoi voit-on apparaître des artefacts dans certains cas avec une utilisation conjointe de CIECAM?

Le code de CIECAM utilise des données spécifiques : J (lightness), Q
(brightness), etc. qui sont proches mais différentes des valeurs Lab.

Si on souhaite considérablement réduire les artefacts, il faudra (comme
d'ailleurs pour CBDL ou Tone-mapping) écrire une version spécifique de
Wavelet, utilisant les données CIECAM plutôt que Lab...beaucoup de
travail en perspective.

#### Le panel image résiduelle – quel usage ?

J'ai déjà beaucoup écrit sur le panel "image résiduelle", néanmoins une
redite ne fait pas de mal.

Comme son nom l'indique l'image résiduelle est la "différence" entre
l'image originale et la "somme" des niveaux de décomposition.

Lorsqu'on choisit plus de 6 niveaux, on peut quasiment dire que l'image
résiduelle est exempte de bruit. Donc, modifier le contraste (global) de
cette image, ou la chroma n'aura quasiment aucune incidence sur le
bruit.

Il est important de noter, que si on veut éviter les artefacts et les
sorties de gamut, il faut maîtriser la "somme" niveaux + image
résiduelle; Si l'image originale est déjà proche des limites, accroître
de manière significative le contraste ou la chroma des niveaux, va
aboutir quasi inévitablement à des artefacts ou à des hors gamut. Jouer
sur l'image résiduelle, en accroissant ou diminuant contraste et chroma
va permettre de rester dans les limites.

Pour modifier le contraste vous pouvez utiliser 3 méthodes, inclues dans
"Image résiduelle" :

1.  changer le contraste seul, vous voyez immédiatement les incidences,
    la variation de contraste est quasi linéaire - avec bien sûr une
    gestion des limites - en fonction de la position du curseur.
2.  utiliser la méthode de compression "contrast", on est un peu dans le
    même cas que précédemment, sinon que la variation du contraste est
    une combinaison logarithme-exponentielle, modifiant plus en
    profondeur le contraste des valeurs extrêmes en maintenant les
    valeurs centrales. Le curseur compression gamma, va permettre de
    recentrer s'il le faut l'histogramme (certes cela semble complexe,
    mais pas tant que cela !)
3.  utiliser la méthode de compression "tone-mapping". Ici, c'est
    différent, on va agir sur l'image résiduelle en modifiant les
    contrastes en profondeur (comme le fait tone-mapping), il est quasi
    indispensable, afin de ne pas aboutir à des images laides, de
    modifier en profondeur les niveaux.

Cette image résiduelle pourra par exemple, permettre de réduire les
effets de brume, ou autoriser une action différentielle sur ombre et
lumière pour remettre une image à forte dynamique dans le rang.

#### Le traitement du bruit : pourquoi 2 traitements ?

Dans Rawtherapee, il y a 2 processus de traitement du bruit.

- le premier appelé "Noise reduction" se situe en début de processus de
  RT, juste avant la conversion colorimétrique. Il s'appuie:
  - sur un traitement par ondelettes, pour le bruit de luminance et de
    chrominance. Ce traitement utilise les premiers niveaux de
    décomposition pour le bruit de luminance, et sur les niveaux plus
    élevés pour le bruit de chrominance. Dans tous les cas, il n'y a pas
    de différenciation accessible à l'utilisateur selon les niveaux; le
    traitement différencié du bruit repose sur l'analyse de l'importance
    du bruit pour chaque niveau.
  - sur un traitement par la méthode de Fourrier, qui complète le
    traitement luminance
  - sur un traitement par median

<!-- -->

- le second qui se situe en fin de processus de RT, et utilise l'outil
  "Niveaux d'ondelettes". Dans ce cas seuls sont accessibles les 4
  premiers niveaux de décomposition.
  - ce traitement va permettre de compléter "Noise reduction" ou traiter
    le bruit des actions postérieures à "Noise reduction"
  - ce traitement est différencié selon les niveaux, de manière
    accessible à l'utilisateur.
  - il utilise pour la luminance le même algorithme que "Noise reduction
    (wavelet)"

Il n'y a donc pas incompatibilité entre les deux traitements, mais
complémentarité. Ils utilisent tous les deux les ondelettes, mais de
manière différente, et chacun à une extrémité du processus de traitement
RT.

#### Les réglages sont-ils interdépendants, par exemple lors de l'utilisation de "denoise" et "edge sharpness" ?

Oui et Non !

Bien sûr en première approche c'est vrai...et évident! Si on accroît
"edge sharpness" sans précautions, le bruit va croître. De plus la
reconstruction après décomposition prendra en compte ce changement!

Mais, car il y a de nombreux mais :

- si on souhaite utiliser edge-sharpness pour créer quelque chose de
  semblable à 'unsharp mask', il est indispensable d'activer 'edge
  detection" et utiliser les réglages proches de 'defaut' pour 'gradient
  sensitivity'...et accroître 'Threshold low (noise)' pour prendre en
  compte le bruit et éviter d'augmenter la force pour ces zones,
  etc...ceci est affaire de goût!
- si l'image est assez bruitée ou fortement bruitée il est recommandé de
  traiter au préalable avec 'noise reduction'; on peut compléter on non
  le traitement du bruit par "denoise and refine'
- il est évident que les effets de 'contrast by details levels' et de
  'wavelet levels' se cumulent pour la luminance et les niveaux
  jusque 5. En effet CBDL est très proche de 'wavelet levels" sinon
  qu'il n'intègre pas la dimension diagonale et qu'il utilise la méthode
  de Haar équivalent de "D2 low" pour wavelet.
- si on utilise "edge sharpness" avec "detection", il semble évident -
  sauf si on souhaite des effets spéciaux de ne pas activer les premiers
  niveaux de 'contrast levels', par contre il est possible (si Link est
  activé) d'utiliser "refine" de "denoise and refine" pour modifier la
  répartition des niveaux de 'edge sharpness'.
- on est libre ou non d'utiliser 'chroma levels"...attention dans
  certains cas ceci peut amener des halos colorés.
- on est libre ou non d'utiliser les niveaux élevés de 'contrast levels'
  (par exemple 5 à 9)...
- on est libre ou non d'utiliser les propriétés de l'image
  résiduelle...qui à partir du niveau 6 ou 7 n'est pas bruitée...on peut
  donc accroître ou réduire son contraste sans risque...sinon ceux d'une
  non maîtrise (excès ou insuffisance de contraste, etc.)!!
- on est libre ou non d'utiliser les propriétés de 'Final Touchup' qui
  vont permettre de modifier le contraste :
  - pour les niveaux (local) : a) contrast balance method; b) final
    local contrast.
  - pour le global : Final contrast curve.

Donc, en résumé, il y a bien une certaine interdépendance pour les
premiers niveaux de contraste, mais la marge de manoeuvre est très
importante pour les autres paramètres.

### Quelques trucs et tours de main

#### Pourquoi et quand regarder l'histogramme de l'image résiduelle ?

Dès qu'une image présente une faible ou un très fort contraste global,
l'utilisation de l'image résiduelle et de son histogramme, va permettre
de guider l'action.

- faut-il réduire ou accroitre le contraste ou la chroma ?
- cherche-t-on des effets spéciaux (tone-mapping, perspective, etc.)
- souhaite-t-on réduire le voile atmosphérique ?
- les images sont-elle à forte dynamique ?
- souhaite-t-on (module en cours)différencier la balance des blancs pour
  l'avant plan et l'arrière plan ?
- etc.

#### Comment réduire le voile atmosphérique ?

Bien sûr, il y a d'autres moyens qui peuvent être utilisés en
conjugaison ou non avec "wavelets" (Retinex exposure...dont c'est une
des finalités, point noir, courbes RGB, etc.). La correction du point
noir semble incontournable (onglet exposition)

Ce que je propose ne peut égaler les outils spécialisés (quoique !!)
pour traiter le voile atmosphérique, mais apporte un plus non
négligeable.

Ici, en observant l'histogramme de l'image résiduelle, on verra que cet
histogramme est amputé des parties basses lumières et hautes lumières.
Il est évident que le nombre de niveaux aura une incidence...affaire de
goût!

Agir sur le contraste de l'image résiduelle soit par :

- le curseur contraste afin de l'accroître
- la méthode de compression contraste, conjointement si c'est
  nécessaire, à compression gamma
- soit par conjugaison de ces 2 méthodes

Va permettre (ces 2 algorithmes donnent des résultats différents), en
conjonction - si c'est nécessaire avec un changement du contraste des
niveaux:

- soit par "edge sharpness"
- soit par "Contraste niveaux"
- soit les deux

On peut également si nécessaire modifier la chroma de l'image résiduelle
et des niveaux, selon l'image et l'effet recherché.

On peut aussi, modifier le chroma de l'image globale, par une courbe Lab
CC:.

On peut aussi, avec l'outil wavelet, agir sur le menu "Final Touchup" et
selon goût agir sur un à trois des paramètres :

- Final local contrast (le plus efficient me semble-t-il !)
- Contrast balance - mais qui peut amener des effets "tone-mapping" pas
  toujours souhaitables !
- et si nécessaire - de mon point de vue le moins efficace ici - "Final
  contrast curve"

#### Pourquoi certaines images ont un aspect tone-mapping ?

A partir du moment où on modifie substantiellement les contrastes des
niveaux, on verra apparaître une notion de perspective ou de relief.

Attention aux artefacts dus à de trop fortes valeurs.

Vous pouvez réduire l'action à l'aide de :

- la courbe "edge sharpness"
- la courbe "final contrast"
- etc.

#### Comment accentuer-réduire l'aspect tone-mapping ?

Vous disposez de plusieurs méthodes qui peuvent se combiner :

- accroître les niveaux de manière différenciée, en conjugaison avec un
  travail sur l'image résiduelle
- utiliser modérément "edge sharpness : local contrast", l'action sur la
  courbe va permettre de contenir les artefacts dus à de trop fortes
  valeurs
- utiliser Retinex in wavelet, ou Retinex Exposure en conjonction avec
  l'outil Wavelet
- utiliser "Final Touchup : contrat balance méthode". Ici l'action sera
  nettement accrue en jouant sur la combinaison des 3 directions
  horizontale - verticale et diagonale, en contrôlant l'action sur la
  diagonale.
- agir sur "Final Touchup : final local contrast" qui va permettre de
  réduire le contraste local pour les faibles valeurs de contraste local
  (et ainsi éviter la montée du bruit), ainsi que pour les hautes
  valeurs et prévenir les artefacts.

#### Le bruit numérique, comment le prendre en compte ?

Il y a plusieurs manière de traiter le bruit:

1.  à l'aide du module "Noise Reduction" qui utilise pour sa part
    essentielle lui aussi des ondelettes (ce module utilise également
    une transformée de Fourier pour la luminance" et un filtre
    "median"). Au niveau du traitement en ondelettes tous les niveaux
    sont traités avec la même amplitude, avec bien sûr un traitement en
    interne différencié en fonction du bruit réel.
2.  à l'aide du module "Wavelet" - "Denoise and refine". Dans ce cas
    seul est traité, le bruit de luminance et uniquement pour les 4
    premiers niveaux, ce qui devrait convenir dans une majorité de cas.

Plusieurs cas peuvent se produire:

1.  l'image originale est fortement bruitée en luminance et chrominance.
    Dans cette situation il faut privilégier l'usage du module "Noise
    reduction", et ramener le bruit de luminance au minimum acceptable
    si on veut continuer par un traitement en ondelettes avec "wavelet
    levels".
2.  l'image originale est peu ou pas bruitée...Le bruit risque d'être
    apporté par le traitement en ondelettes qui risque dans certains cas
    d'accroître le bruit. Dans ce cas, on pourra utiliser "Denoise and
    refine" pour éliminer le bruit restant (accentué ou non par le
    traitement en ondelettes). On pourra par exemple réduire le bruit du
    niveau 2 et amplifier légèrement (refine) l'action sur les niveaux.

#### Quel traitement pour les images « astro » ?

Bien sûr tout dépend du niveau de bruit de l'image "astro", mais en
règle générale :

1.  on pourra réduire le bruit des étoiles en agissant sur les 3
    curseurs "Denoise and Refine"
2.  amplifier le contraste local par action sur les curseurs inférieurs
3.  réduire ou accroître le contraste de l'image résiduelle (ciel
    profond)

#### Les portraits ?

Ici, le processus sera équivalent à celui de CBDL...

1.  On réglera l'image générale par les niveaux d'ondelletes, l'image
    résiduelle, et "edge sharpness"?... selon le cas
2.  puis on pourra soit cibler l'action sur la peau de manière directe
    (protection) ou indirecte (cible : targetting)

Les 2 méthodes présentent chacune des avantages et sont plus liées à des
souhaits photographique! Est-ce qu'on souhaite détacher le portrait sur
une arrière plan moins contrasté, ou l'inverse. Là encore l'action sur
l'image résiduelle pourra venir compléter l'action.
