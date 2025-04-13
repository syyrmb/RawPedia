---
title: The Image Editor Tab fr
contributors:
  - Lebarhon
  - Hombre
---

<div class="pagetitle">

L’Éditeur

</div>

<figure>
<img src="/images/Rt_55_trains.png" title="Rt_55_trains.png" />
<figcaption>Rt_55_trains.png</figcaption>
</figure>

## Introduction

L'onglet Editeur est l'endroit pour travailler ses photos. Rawtherapee
est par défaut en mode "*Editeur unique, onglets verticaux*" (ou SETM =
Single Editor Tab Mode), le mode qui utilise le plus efficacement la
mémoire et permet l'utilisation de la *Bande film* (décrite ci-dessous).
Vous pouvez basculer en "*Editeurs multiples*"(ou METM = Multiple Editor
Tabs Mode) en allant dans "*Préférences \> Général \> Habitudes de
travail*", cependant chaque onglet Editeur exige une certaine quantité
de mémoire RAM en fonction de la taille de l'image et des outils
utilisés, et aussi la *Bande film* est cachée dans ce mode, donc, nous
recommandons au moins d'essayer le mode SETM.

## Le panneau Aperçu

Le panneau central affiche un aperçu de votre photo. Il est généré à
partir des données raw et d'un calcul qui prend en compte les paramètres
soit donnés manuellement ou bien enregistrés dans le [profil de
traitement](Sidecar_Files_-_Processing_Profiles/fr.md) utilisé à
l'ouverture de la photo, tel que spécifié dans "*Préférences \>
Traitement de l'image \> Paramètres de traitement d'image par défaut*".
L'aperçu vous montre les effets de tous les ajustements que vous
apportez. Notez que les effets de certains outils ne sont visibles avec
précision que si l'image est zoomée à au moins 1:1 (100%). Ces outils
sont repérés dans l'interface par une icône ![Zoom
1:1](One-to-one-small.png "Zoom 1:1") juste après le nom de l'outil.

L'image affichée dans l'aperçu utilise l'espace colorimétrique de
travail puis est convertie dans l'espace colorimétrique de l'écran si un
tel espace est installé, ou bien dans un espace sRVB dans le cas
contraire. Il ne prend pas en compte le [Profil de
sortie](Color_Management/fr#Profil_de_sortie.md)" de l'outil
"[Gestion de la couleur (ICM)](color_management/fr)".

### Oups! Ma photo raw n'a pas le même aspect que le JPEG de l'appareil photo

Après l'ouverture d'une photo raw vous remarquerez qu'elle semble
différente (souvent moins bien, plus sombre, moins piquée, plus terne,
manquant de contraste) de la photo JPEG de l'appareil, ou de la même
photo raw affichée par un autre logiciel. Qui est la cause ?
Sorcellerie, les aliens, les opposums ou la conception ?

Il y a trois choses que vous devez connaître pour comprendre ce qui se
passe ici :

1.  Votre appareil ne vous montre pas les vraies données raw lors des
    prises de vues. Il traite l'image raw de nombreuses façons avant de
    vous la présenter avec l'histogramme et l'aperçu sur l'afficheur
    numérique au dos de l'appareil. Même si vous avez réglé sur la
    position neutre, "0", tous les paramètres de traitement que le
    firmware de votre appareil permet de modifier, ce que vous voyez
    n'est pas une image non traitée. En fait, ce qui est affiché dépend
    des choix faits par les ingénieurs et managers qui ont développé
    votre appareil, ce qui comprend habituellement un courbe tonale
    personnalisée et un renforcement du contraste, de la netteté et de
    la réduction du bruit. Certains appareils, surtout les bas de gamme
    et les [systèmes micro quatre
    tiers](http://fr.wikipedia.org/wiki/Syst%C3%A8me_Micro_Four_Thirds),
    peuvent aussi appliquer une correction de la distorsion de
    l'objectif pour non seulement corriger la [distorsion en barillet et
    en coussin](http://fr.wikipedia.org/wiki/Distorsion_%28optique%29),
    mais aussi pour cacher de sévères problèmes de
    [vignettage](http://fr.wikipedia.org/wiki/Vignettage). Beaucoup
    d'appareils sous-exposent aussi vos photos de -0,3IL jusqu'à -1,3IL
    voire plus, dans le but de gagner de la place dans les hautes
    lumières. Au moment du traitement de l'image raw par l'appareil
    photo (ou un autre logiciel), la compensation d'exposition est
    accrue du même montant, faisant apparaître une luminosité correcte
    avec l'espoir dans le même coup de récupérer des hautes lumières.
    RawTherapee vous montre les vraies données raw, ce qui peut vous
    faire apparaitre vos photos foncées, il vous appartient de décider
    l'application de la correction d'exposition et de la façon de le
    faire, soit en utilisant le curseur Compensation d'exposition ou
    bien l'une des diverses courbes tonales. Augmenter la Compensation
    d'exposition rend le bruit plus apparent, indifféremment du fait
    qu'il soit réalisé par l'appareil photo ou bien RawTherapee, mais en
    dehors de cela **RawTherapee n'ajoute pas de bruit !** Beaucoup
    d'appareils appliquent une réduction du bruit aux images JPEG (dans
    votre dos) pour diminuer le niveau de bruit après l'augmentation de
    la compensation d'exposition, ainsi vous pouvez vous attendre à une
    différence entre votre image JPEG sortie de l'appareil et l'image
    sortie de RawTherapee si la réduction du bruit n'est pas utilisée.
2.  Chaque fichier raw DSLR contient une image traitée JPEG. La plupart
    des fichiers raw contiennent une image JPEG de la même résolution
    maximum dont est capable votre appareil, et certains fichiers raw
    contiennent jusqu'à trois images JPEG ne différant que par leur
    résolution. Quand vous ouvrez des fichiers raw dans un autre
    logiciel, ce que vous voyez en général ne sont **pas** les données
    raw, mais l'image JPEG traitée et intégrée. Exemples de logiciels
    qui soit sont incapables de présenter les vraies données raw ou qui
    ne le font pas de par leur configuration par défaut :
    [IrfanView](http://fr.wikipedia.org/wiki/IrfanView),
    [XnView](http://fr.wikipedia.org/wiki/XnView),
    [Gwenview](http://fr.wikipedia.org/wiki/Gwenview),
    [Geeqie](http://en.wikipedia.org/wiki/Geeqie), [Eye of
    GNOME](http://fr.wikipedia.org/wiki/Eye_of_GNOME),
    [F-Spot](http://fr.wikipedia.org/wiki/F-Spot),
    [Shotwell](http://fr.wikipedia.org/wiki/Shotwell),
    [gThumb](http://fr.wikipedia.org/wiki/GThumb), etc. Il est
    intéressant de mentionner maintenant que si vous prenez vos photos
    en mode "RAW+JPEG", vous gaspillez de la place disque pour rien car
    vos fichiers raw contiennent déjà les fichiers JPEG intégrés que
    vous pouvez voir en utilisant le programme listé. L'image JPEG
    intégrée peut différer d'une "externe" enregistrée en utilisant le
    mode "RAW+JPEG" pour la compression.
3.  La plupart des programmes de développement raw (ceux qui lisent
    vraiment les données raw réelles au lieu de se contenter du fichier
    JPEG intégré) y appliquent un traitement, tel qu'une courbe tonale
    basique, même si le paramétrage est au plus neutre possible, rendant
    ainsi impossible pour l'utilisateur le visionnage des données
    réelles, non modifiées contenues dans la photo raw. Adobe Lightroom
    en est un exemple. Comparer l'image réellement neutre de RawTherapee
    à une autre quasi neutre en provenance de ces autres programmes met
    en évidence les différences.

RawTherapee, d'un autre côté est conçu pour vous montrer la véritable
image raw dans l'aperçu principal, vous laissant maître de la façon dont
vous voulez traiter ces données. Lorsque vous utilisez le profil de
traitement "Neutre" vous voyez l'image dématricée avec la balance des
blancs de l'appareil dans votre espace colorimétrique de travail et
aucune autre modification. Vous pouvez même voir l'image non dématricée
et réglant l'option [dématriçage](demosaicing/fr) sur "None"
(Aucune). Pour vous fournir un point de départ plus agréable
esthétiquement, nous fournissons une collection de profils de traitement
avec RawTherapee. Après l'installation de ce dernier, le profile de
traitement par défaut des fichiers raw est appelé de façon éponyme
"Default". Nous fournissons aussi les profils "Default ISO Medium" (ISO
moyen par défaut) et "Default ISO High" (ISO élevés par défaut) qui sont
conçus pour donner un bon point de départ pour les images respectivement
modérément bruitées oet très bruitées.

Aucun des profils fournis (du moins aucun de ceux fournis avec
RawTherapee 5.0) n'est conçu pour imiter le rendu de l'appareil photo.
Pourquoi cela ? Chaque appareil est différent. La qualité des images de
mon appareil à 1600 ISO peuvent être beaucoup plus bruitées que celles
de votre appareil. La réponse aux couleurs de mon appareil diffère de
celle du votre. Même un appareil identique peut répondre différemment
aux divers réglages. Pour fournir de tels profils, il faudrait que l'on
accède aux fichiers raw pour chaque modèle d'appareil photo supporté,
souvent même, à de multiples fichiers raw réalisés dans différents modes
de prise de vue pour chaque appareil, plus d'infinies heures de travail.
Cela est peut-être possible pour une communauté, mais pas pour une
petite équipe. Et puis même, quel serait l'intérêt de RawTherapee si
c'est pour finir avec un rendu de JPEG d'appareil photo ?

Il est bien plus raisonnable que vous appreniez l'utilisation des outils
puissants fournis par RawTherapee afin d'obtenir le meilleur de vos
photos, de dépasser les rendu de l'appareil.

A partir de septembre 2015 nous fournirons des profils d'entrée DCP
fabriqués avec [DCamProf](http://www.ludd.ltu.se/~torger/dcamprof.html)
qui comprend une [courbe tonale
optionnelle](http://www.ludd.ltu.se/~torger/dcamprof.html#dcp_tone).
Cette courbe est réalisée d'après la courbe pour film par défaut du
logiciel Camera Raw d'Adobe et donne un résultat similaire au rendu de
votre appareil photo. La raison pour laquelle nous intégrons la courbe
dans les nouveaux profils DCP est que cela donne un bon départ plein de
vie (par opposition à l'aspect terne donné par le profil de traitement
"Neutre") sans avoir à utiliser [Niveaux
Auto](Exposure/fr#Niveaux_Auto.md) et sans avoir à toucher à
aucun des autres outils, et c'est entièrement optionnel. Lisez l'article
sur les [Profils
d'entrée](Color_Management/fr#Profil_d'entrée.md). Si nous
fournissons un DCP pour le modèle de votre appareil photo qui comprend
une courbe tonale, la case à cocher "Utiliser la courbe tonale du profil
DCP" dans ICM \> Profil d'entrée \> DCP sera cliquable. Appliquer le
profil de traitement Neutre désactivera la courbe tonale. Alors que le
profil couleur d'entrée est appliqué dès les premières étapes de la
[Succession des outils dans le
pipeline](Toolchain_Pipeline/fr.md), la courbe tonale DCP est
appliquée plus tard dans le pipeline peu après l'outil Exposition.

Vous pouvez créer un profil de traitement sur mesure, parfait pour
l'ensemble appareil et objectif, et régler RawTherapee pour l'utiliser
par défaut sur toutes vos photos raw. Voir la page [Création de profils
de traitement d'usage
général](http://50.87.144.65/~rt/w/index.phptitle=Creating_processing_profiles_for_general_use/fr.md)
pour découvrir comment.

### Défilement de la barre d'outils

La barre d'outils au-dessus et au-dessous l'aperçu principal contient un
certain nombre de boutons et autres widgets qui peuvent ne pas pouvoir
être affichés sur un écran de trop basse définition.

### Modes d'aperçu

En plus de l'aperçu normal, RawTherapee supporte plusieurs autres modes
d'aperçu pour aider au peaufinage des photos. Les modes d'aperçu sont
contrôlés soit avec des boutons situés dans la barre d'outils de
l*'Editeur* soit avec des [raccourcis
clavier](Keyboard_Shortcuts/fr.md). Un seul mode d'aperçu
peut-être utilisé à la fois.

<div style="float: right">

<table>
<caption>align="bottom" | * L'aperçu revient en mode normal en
désélectionnant tout autre mode.</caption>
<thead>
<tr class="header">
<th><p>Mode d'aperçu</p></th>
<th><p>Raccourci</p></th>
<th><p>Boutons</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="padding:10px;"><p>Normal*</p></td>
<td></td>
<td><figure>
<img src="/images/preview_mode_1_regular.png"
title="Image:preview mode 1 regular.png" />
<figcaption>Image:preview mode 1 regular.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Canal rouge</p></td>
<td style="text-align: center;"><p>r</p></td>
<td><figure>
<img src="/images/preview_mode_2_red.png"
title="Image:preview mode 2 red.png" />
<figcaption>Image:preview mode 2 red.png</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td style="padding:10px;"><p>Canal vert</p></td>
<td style="text-align: center;"><p>g</p></td>
<td><figure>
<img src="/images/preview_mode_3_green.png"
title="Image:preview mode 3 green.png" />
<figcaption>Image:preview mode 3 green.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Canal bleu</p></td>
<td style="text-align: center;"><p>b</p></td>
<td><figure>
<img src="/images/preview_mode_4_blue.png"
title="Image:preview mode 4 blue.png" />
<figcaption>Image:preview mode 4 blue.png</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td style="padding:10px;"><p>Luminance</p></td>
<td style="text-align: center;"><p>v</p></td>
<td><figure>
<img src="/images/preview_mode_5_luminance.png"
title="Image:preview mode 5 luminance.png" />
<figcaption>Image:preview mode 5 luminance.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Masque du focus</p></td>
<td style="text-align: center;"><p>Shift+f</p></td>
<td><figure>
<img src="/images/preview_mode_6_focus.png"
title="Image:preview mode 6 focus.png" />
<figcaption>Image:preview mode 6 focus.png</figcaption>
</figure></td>
</tr>
</tbody>
</table>

align="bottom" \| \* L'aperçu revient en mode normal en désélectionnant
tout autre mode.

</div>

Les modes d'aperçu suivants sont actuellement possibles :

- Le canal rouge,
- Le canal vert,
- Le canal bleu,
- La luminosité, qui est calculée avec la formule 0.299\*R + 0.587\*V +
  0.114\*B,
- Le masque du focus, pour voir les zones de mise au point

Image:Preview_1_regular.jpg\|Aperçu normal
Image:Preview_2_red.jpg\|Canal rouge Image:Preview_3_green.jpg\|Canal
vert Image:Preview_4_blue.jpg\|Canal bleu
Image:Preview_5_luminosity.jpg\|Luminosité
Image:Preview_6_focus.jpg\|Masque du focus

#### Modes d'aperçu Rouge, Vert, Bleu et Luminosité

L'aperçu sur différents canaux peut être utile lors de l'édition des
courbes RVB, en cas de projet d'une conversion en noir et blanc en
utilisant le mixage de canaux, pour évaluer le bruit dans l'image, etc.
L'aperçu Luminosité est utile pour avoir instantanément une vision de
l'image en noir et blanc sans modifier les paramètres de développement,
pour voir quel canal peut présenter une zone hors domaine, ou pour des
raisons d'esthétisme.

#### Masque du focus

![Masque du focus révélant le plan de mise au
point](Preview_6_focus_2.jpg "Masque du focus révélant le plan de mise au point")
Le Masque du focus est conçu pour mettre en évidence les zones de
l'image sur lesquelles s'est faite la mise au point. Bien sûr ces zones
sont plus nettes, ainsi les zones nettes seront mises en évidence. Le
Masque du focus est plus précis sur les images à faible profondeur de
champ, faible bruit et à niveaux de zoom importants. Pour améliorer la
précision de détection sur les images bruitées, opérer avec un faible
zoom, autour de 10 à 30 %. Noter que l'aperçu est affiché plus lentement
quand le Masque du focus est activé.

L'implémentation actuelle analyse l'image de l'aperçu qui est une
diminution d'échelle de l'image originale. Ce procédé de changement
d'échelle diminue le bruit et facilite l'identification des détails
réellement plus nets plutôt que le bruit qui peut aussi contenir une
micro texture. En même temps, réduire l'image originale vers l'aperçu
compresse les détails de plus grande échelle vers une taille plus petite
et cela peut introduire un effet de crénelage, ce qui dans les deux cas
peut provoquer de faux positifs. Il est possible d'augmenter sa
confiance en observant le masque a différents niveaux de zoom, ce n'est
pas toujours exempt d'erreurs mais peut aider dans bien des cas.

**Attention :** Assurez vous d'avoir vérifié deux fois vos photos si
vous décidez de les détruire suite aux résultats donnés par le Masque du
focus.

### Couleur d'arrière plan de l'aperçu de l'éditeur

La couleur d'arrière plan du panneau d'aperçu entourant l'image peut
-être changée pour faciliter l'observation de l'image pendant l'édition
et mieux voir le recadrage de l'image. Une pile verticale de trois fins
boutons dans la barre d'outils des modes d'aperçu au-dessus du panneau
d'aperçu de l'image, permet de sélectionner la couleur d'arrière plan de
la zone autour de l'aperçu.

<div align="center">

<table>
<colgroup>
<col style="width: 17%" />
<col style="width: 17%" />
<col style="width: 17%" />
<col style="width: 30%" />
<col style="width: 17%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Couleur d'arrière<br />
plan de l'aperçu</p></th>
<th><p>Raccourci</p></th>
<th><p>Boutons</p></th>
<th width="30%"><p>Comportement de l'aperçu &amp;<br />
Visualisation du recadrage</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dépendant du thème</p></td>
<td style="text-align: center;"><p>8</p></td>
<td><figure>
<img src="/images/Previewback_7_theme.png"
title="Image:Previewback_7_theme.png" />
<figcaption>Image:Previewback_7_theme.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_theme.png"
title="Previewback_flower_theme.png" width="180" />
<figcaption>Previewback_flower_theme.png</figcaption>
</figure></td>
<td><p>La zone rognée de l'image est masquée par la couleur du thème. Sa
visibilité est donnée par le Masque de recadrage &amp; l'Opacité tels
que définis dans les "<em>Préférences &gt; Général &gt; Théme par défaut
&gt; Masque de recadrage</em>".</p></td>
</tr>
<tr class="even">
<td><p>Noir</p></td>
<td style="text-align: center;"><p>9</p></td>
<td><figure>
<img src="/images/Previewback_8_black.png"
title="Image:Previewback_8_black.png" />
<figcaption>Image:Previewback_8_black.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_white.png"
title="Previewback_flower_white.png" />
<figcaption>Previewback_flower_white.png</figcaption>
</figure></td>
<td><p>La zone rognée de l'image est masquée par la couleur
noire.</p></td>
</tr>
<tr class="odd">
<td><p>Blanc</p></td>
<td style="text-align: center;"><p>0</p></td>
<td><figure>
<img src="/images/Previewback_9_white.png"
title="Image:Previewback_9_white.png" />
<figcaption>Image:Previewback_9_white.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_black.png"
title="Previewback_flower_black.png" />
<figcaption>Previewback_flower_black.png</figcaption>
</figure></td>
<td><p>La zone rognée de l'image est masquée par la couleur
blanche.</p></td>
</tr>
</tbody>
</table>

</div>

### Vue détaillée

Le bouton "(nouvelle) vue détaillée"
![<File:Window-add.png>](Window-add.png "File:Window-add.png"), situé
sous l'aperçu principal à coté des boutons de zoom, ouvre par-dessus
l'aperçu principal, une nouvelle vue d'une taille et d'un niveau de zoom
réglables. Cela vous permet de travailler sur une photo zoomée selon le
besoin tout en examinant plusieurs détails grossis à 100 % (ou même
plus). Le bénéfice de cette fonctionnalité est particulièrement
important pour les utilisateurs d'un ordinateur assez lent, mais pas
seulement, car le zoom arrière de l'aperçu principal prend moins de
temps à se rafraîchir que si vous zoomiez à 100% car en travaillant à un
niveau de zoom inférieur à 100% cela exclue certains outils trop lents
tels que la réduction de bruit, alors que les petites vues détaillées
zoomées à 100% incluent effectivement tous les outils mais restent
rapides à se rafraîchir en raison de leur petite taille. Cela permet par
exemple d'utiliser l'aperçu principal pour régler l'exposition générale,
là où il est nécessaire de voir toute l'image, et de créer une ou
plusieurs vues détaillées pour apprécier la qualité de la netteté et/ou
de la réduction du bruit.

### Délai de rafraîchissement de l'aperçu

Toute modification des paramètres des outils envoie un signal destiné au
rafraîchissement en conséquence de l'aperçu. Imaginez ce qui arriverait
s'il n'y avait pas de "temps de retard", alors que vous venez, par
exemple, de pousser le curseur compensation d'exposition de 0.00 à
+0.60. Un signal est envoyé pour mettre à jour l'aperçu après chaque
modification minime de la valeur, +0.01, +0.02, ... +0.59, +0.60. Mettre
l'aperçu à jour 60 fois serait complètement inutile en prendrait en fait
plus de temps que le déplacement du curseur. Cela est plus
particulièrement vrai pour les outils les plus compliqués, tels que la
réduction du bruit, où la mise à jour peut prendre jusqu'à une seconde
(selon votre CPU et la taille de l'aperçu). La solution est pour
RawTherapee d'attendre un instant très court à partir du moment où vous
avez arrêté de bouger un curseur (vous n'avez pas besoin de le lâcher,
une pause dans le mouvement est suffisante) jusqu’au moment où il envoie
un signal pour le rafraîchissement de l'aperçu.

Nous avons introduit deux paramètres qui contrôlent le temps de cette
attente :

AdjusterMinDelay  
Valeur par défaut = 100ms.

Ceci est utilisé pour les outils ayant un temps de réponse très court,
par exemple le curseur de compensation d'exposition.

AdjusterMaxDelay  
Valeur par défaut = 200ms.

Ceci est utilisé pour les outils ayant un temps de réponse assez long,
par exemple les curseurs CIECAM02.

Ces deux valeurs sont modifiables dans le fichier Options du dossier
[Config](file_paths/fr).

## Le panneau de gauche

Sur votre gauche, il y a un panneau qui affiche optionnellement
l'histogramme principal ("*Préférences \> Général \> Habitudes de
travail \> Histogramme dans le panneau de gauche*"), et en permanence le
*Navigateur de fichiers*, l*'Historique* et les *Captures*. Vous pouvez
cacher ce panneau en utilisant l'icône Montrer/Cacher ![Hide left panel
icon](panel-to-left.png "Hide left panel icon") ou le [raccourci
clavier](Keyboard_Shortcuts/fr.md).

### Histogramme

<figure>
<img src="/images/Rt57_histogram_wide_labeled.png"
title="Rt57_histogram_wide_labeled.png" />
<figcaption>Rt57_histogram_wide_labeled.png</figcaption>
</figure>

<figure>
<img src="/images/RT57_histogram_ani.gif" title="RT57_histogram_ani.gif" />
<figcaption>RT57_histogram_ani.gif</figcaption>
</figure>

<figure>
<img src="/images/Rt_histogram_rgbindicator.png"
title="Rt_histogram_rgbindicator.png" />
<figcaption>Rt_histogram_rgbindicator.png</figcaption>
</figure>

Un histogramme, en photographie, est une représentation graphique du
nombre de pixels ayant une valeur donnée. Typiquement, l'axe horizontal
représente la gamme des valeurs possibles et l'axe verticale représente
le nombre de pixels ayant cette valeur. Les axes ne sont pas
nécessairement linéaires, RawTherapee peut aussi représenter un
histogramme logarithmique.

Indépendamment du nombre de bits utilisés pour la profondeur de la
photo, l'histogramme proprement dit possède une précision de 256
intervalles d’échantillonnage. Pour comprendre cela, prenons l'exemple
d'une image de précision 16 bits en nombres entiers. La gamme des
valeurs possibles s'étend depuis 0 jusqu'à 65535 (2^16 = 65536 valeurs
possibles, et puisque 0 est la valeur minimale autorisée, alors la
valeur maximale est 65535). Vouloir dessiner un histogramme exploitant
une précision de 16 bits signifierait qu'il devrait avoir une largeur de
65535 pixels pour représenter toutes les données fidèlement, or aucun
écran aujourd'hui n'appproche cette largeur. En conséquence, tous les
pixels ayant une valeur comprise entre 0 et 255 (65535/256\*1) sont
regroupés dans le premier "intervalle". Le second intervalle contient le
compte de tous les pixels ayant une valeur comprise entre 256 et 511
(65535/256\*2). Le troisième intervalle représente les valeurs de 512 à
767 (65535/256\*3), et ainsi de suite jusqu'à l'intervalle 256. Cela se
passe ainsi indépendamment de la profondeur de l'immage d'entrée et
d'ailleurs le moteur de RawTherapee utilise une précision de 32 bits en
virgule flottante

L'histogramme principal peut présenter un ou simultanément plusieurs des
éléments suivants :

- ![<File:Histogram-red-on-small.svg>](Histogram-red-on-small.svg "File:Histogram-red-on-small.svg")
  le canal rouge,
- ![<File:Histogram-green-on-small.svg>](Histogram-green-on-small.svg "File:Histogram-green-on-small.svg")
  le canal vert,
- ![<File:Histogram-blue-on-small.svg>](Histogram-blue-on-small.svg "File:Histogram-blue-on-small.svg")
  le canal bleu,
- ![<File:Histogram-silver-on-small.svg>](Histogram-silver-on-small.svg "File:Histogram-silver-on-small.svg")
  la luminance CIELab,
- ![<File:Histogram-gold-on-small.svg>](Histogram-gold-on-small.svg "File:Histogram-gold-on-small.svg")
  [chromaticité](http://en.wikipedia.org/wiki/Chromaticity).
- ![<File:Histogram-bayer-on-small.svg>](Histogram-bayer-on-small.svg "File:Histogram-bayer-on-small.svg")
  les canaux rouge, vert et bleu de l'image source en raw avant le
  dématriçage.

L'histogramme présente les canaux listés ci-dessus en utilisant le
profil de sortie corrigé gamma lorsque le bouton
gamut![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png") est
désactivé (par défaut), ou en utilisant le profil de travail lorsque le
bouton est activé. L'état de ce bouton affecte aussi les valeurs
présentées dans le panneau Navigateur, ainsi que les indicateurs Ombres
hors domaine
![<File:Warning-shadows.png>](Warning-shadows.png "File:Warning-shadows.png")
et Hautes lumières hors domaine
![<File:Warning-highlights.png>](Warning-highlights.png "File:Warning-highlights.png").
Il n'affecte pas l'histogramme raw.

Comme l'eau dans un tuyau, les données de l'image cheminent emportées
par RawTherapee depuis le fichier d'entrée à travers diverses étapes, la
plupart étant contrôlables par l'utilisateur, jusqu'à la sortie.
Celle-ci peut être l'image enregistrée dans un fichier, ou affichée sur
votre écran. Chaque étape impacte les données de couleur. L'histogramme
permet de visualiser ces données aux différentes étapes. Par défaut,
l'histogramme montre les données de couleur telles qu'elles apparaîtront
si vous enregistrez l'image de sortie, y compris le traitement fait à
toutes les étapes intermédiaires. En activant le bouton gamut
![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png") vous
pouvez accéder aux données lors des étapes précoces où elles sont
converties dans l'espace colorimétrique de travail. Vous pouvez même
voir les données raw avant que toute transformation ou dématriçage ne
soit appliqué.

Examinons l'exemple donné par le large histogramme ci-dessus. Bien qu'il
présente en fait quatre histogrammes (rouge, vert, bleu et luminance),
concentrez vous sur un seul à la fois. L'axe horizontal représente les
valeurs possibles où "A" sont les valeurs les plus sombres possibles,
"C" les tons moyens, et "E" les valeurs les plus claires possibles. La
position de la ligne de l'histogramme sur l'axe vertical varie en
fonction du nombre de pixels qui possèdent cette valeur. On voit qu'il
n'y a pas de pixels dans le canal rouge ayant une valeur proche de "A"
(depuis 0 jusqu'au très foncé), car la ligne de l'histogramme est proche
du bas. Il y a un nombre significatifs de pixels où le canal rouge est
foncé (entre A et B), et aussi un nombre significatifs ou il est clair
(autour de D). Enfin, point important, il y a un pic à l'extrémité
droite de l'histogramme, sur E, il indique qu'un grand nombre de pixels
ont une valeur de rouge maximale, ils sont hors domaine.

D'une façon générale, vous devez vous inquiéter lorsque des pixels hors
domaine apparaissent sur de la peau, mais ne pas vous en soucier
lorsqu'ils sont dus à une [lumière
spéculaire](https://fr.wikipedia.org/wiki/Lumi%C3%A8re_sp%C3%A9culaire).
Si l'histogramme présente des pixels hors domaine et que les endroits où
ils apparaissent vous soucient, commencez par établir à quel moment cela
arrive. Consultez l'histogramme raw, y a t-il des canaux présentant du
hors domaine ? Si oui, alors aidez vous de la [reconstruction des hautes
lumières](Exposure/fr#Reconstruction_des_hautes_lumières.md). Si
non, alors toute l'information nécessaire est intacte, et les pixels
hors domaine sont dus à certaines étapes dans le pipeline. Assurez vous
que le gamut de l'espace de travail est suffisamment large en activant
le bouton gamut
![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png") pour voir
l'histogramme au niveau du profil de travail dans le pipeline. Il peut
être utile d'appliquer temporairement le profil
[Neutre](neutre) afin de désactiver tous les outils pendant
la vérification, puis rétablir comme à l'origine. Si l'espace de travail
n'est pas la cause du problème (l'espace de travail par défaut est
ProPhoto qui est énorme), alors c'est probablement vos réglages qui le
sont. Réduisez l’exposition, soyez modéré avec les courbes, utilisez la
[Compression de Plage
Dynamique](Dynamic_Range_Compression/fr.md) si nécessaire.

Savoir lire un histogramme est une compétence de base indispensable car
cela permet d'identifier des problèmes sur l'image indépendamment du
fait que l'écran puisse être trop foncé ou mal calibré.

Pour vous aider à visualiser les données, l'histogramme (à partir de
RawTherapee 5.5) propose trois échelles de calibrage des données selon
les axes x et y :

- ![<File:Histogram-mode-linear-small.png>](Histogram-mode-linear-small.png "File:Histogram-mode-linear-small.png")
  Mode linéaire-linéaire. Affiche des lignes de grille à mi-hauteur, au
  quart, au huitième et au seizième selon la taille de l'histogramme.
- ![<File:Histogram-mode-logx-small.png>](Histogram-mode-logx-small.png "File:Histogram-mode-logx-small.png")
  Mode linéaire-log. L'axe x est linéaire, l'axe y et les lignes de
  grille horizontales sont selon une échelle logarithmique. La position
  des lignes de grille correspond toujours à la mi-hauteur, le quart,
  etc.
- ![<File:Histogram-mode-logxy-small.png>](Histogram-mode-logxy-small.png "File:Histogram-mode-logxy-small.png")
  Mode Log-log. Les deux axes, x et y sont selon une échelle
  logarithmique. Les lignes de grille ne sont pas selon une échelle
  logarithmique mais correspondent aux [indices de
  lumination](https://fr.wikipedia.org/wiki/Indice_de_lumination) - à
  chaque ligne de grille, la valeur double, il y a donc une ligne pour
  les valeurs 1, 3, 7, 15, 31, 63, et 127 (`pow(2.0,i) - 1)`).

En présence d'une zone brillante disproportionnée par rapport au reste
de l'image, elle apparaîtra dans l'histogramme sous la forme d'un pic.
Pour montrer cela dans un histogramme avec un axe y linéaire, le pic
risque de pousser les valeurs moindres au pied de l'axe y, les rendant
difficiles à voir. Passez dans l'un des modes logarithmiques pour
changer les données d'échelle et ainsi vous permettre d'avoir une
meilleure vue d'ensemble de toutes les valeurs.

L'histogramme peut être placé dans le panneau de droite ou de gauche
("*Préférences \> Général \> Habitudes de travail \> Histogramme dans le
panneau de gauche*").

#### Histogramme raw

Les fichiers raw contiennent un grand nombre de données capturées par le
capteur et numérisées par le convertisseur analogique/numérique. Le
fichier raw en tant que conteneur possède une profondeur de couleur qui
lui est propre, typiquement 16 bits, alors que les données qu'il
contient peuvent avoir une profondeur plus faible, typiquement 12 bits
(0-4096) ou 14 bits (0-16384). Afin d'afficher les données d'un fichier
raw sous forme d'image, parmi les éléments d'information clés exigés
pour traiter les données correctement, il y a les niveaux du noir et du
blanc. Le niveau du noir n'est pas nécessairement 0, car le capteur et
l'électronique de l'appareil photo produisent du bruit numérique, donc
le plancher du bruit peut être par exemple à 512. Le niveau du blanc
n'est pas obligatoirement 16384; il dépend aussi de diverses choses, et
peut se situer par exemple à 16300. Pour plus d'information, consulter
les articles [Dématriçage](demosaicing/fr) et [Ajouter la
prise en charge de nouveaux formats
raw](Adding_Support_for_New_Raw_Formats/fr.md) (principalement
l'en-tête du fichier `camconst.json`). Les valeurs des niveaux du noir
et du blanc utilisés par RawTherapee sont hiérarchiquement établies en
consultant plusieurs endroits : dans `dcraw.c`, à l'intérieur des
métadonnées du fichier raw, et dans `camconst.json` (le dernier en
premier). Ensuite, l'utilisateur peut peaufiner les niveaux raw
[noir](raw_black_points/fr) et
[blanc](raw_white_points/fr) depuis RawTherapee.

Les histogrammes raw présentent les données après la soustraction du
niveau du noir. L'extrémité droite de l'histogramme est ancrée sur le
niveau du blanc. Les histogrammes raw sont impactés par les niveaux du
noir et du blanc détectés ainsi que par les ajustements du niveau du
noir et du blanc réalisés par l'utilisateur.

Lors de l'examen de l'histogramme raw, vous pouvez aussi régler la
méthode de dématriçage sur "aucune". Cela révélera le motif du capteur
dans l'aperçu, et aussi fera afficher les valeurs RVB du pixel
actuellement survolé par la souris dans le panneau
[Navigateur](the_image_editor_tab/fr#navigateur). Ces valeurs
sont impactées par les niveaux détectés du noir et du blanc ainsi que
par les ajustements du niveau du noir réalisés par l'utilisateur dans
RawTherapee, mais ils ne sont pas impactés par les ajustements du niveau
du blanc ("correction du point blanc") réalisés par l'utilisateur dans
RawTherapee.

### Navigateur

Le panneau *Navigateur* affiche une vignette (en entier) de l'image en
cours d'édition, et les valeurs RVB, TSV et Lab du pixel se trouvant
sous le curseur de la souris.

Les valeurs montrées par l'histogramme principal et le panneau
navigateur sont soit celles du profil de travail ou bien celles
corrigées en gamma du profil de sortie, cela dépend de la position du
bouton gamut
![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png") situé
dans la barre d'outils au-dessus de l'aperçu principal. Lorsque le
bouton gamut est activé, le profil de travail est utilisé, sinon c'est
le profil de travail de sortie gamma-corrigé qui est utilisé.

En cliquant sur les valeurs dans le panneau Navigateur vous commutez en
boucle entre ces trois formats :

- \[0-255\]
- \[0-1\]
- \[%\]

RawTherapee 5.1 et suivants peuvent indiquer les valeurs raw réelles des
photosites. Pour cela, paramétrer le Navigateur dans le format
\[0-255\], appliquer le [profil de
traitement](Sidecar_Files_-_Processing_Profiles/fr.md) neutre,
puis régler la méthode de [Dématriçage](demosaicing/fr) à
"Aucune". Le Navigateur indiquera la valeur raw réelle des photosites
après la soustraction du niveau noir à l'intérieur de la gamme des
données raw originales.

<div style="clear: both">
</div>

### Historique

Le panneau Historique contient une série d'entrées qui représentent
chacune de vos actions d'édition. En cliquant sur les différentes
entrées, vous pouvez vous déplacer en avant ou en arrière au travers des
différentes étapes de votre travail.

Une entrée est ajoutée à chaque action sur un outil *différent*, les
éditions répétées avec le même outil sont enregistrées en une seule
entrée. Par exemple, ajuster le curseur de compensation d'exposition de
"0" à "0.3" puis à "0.6" aboutira à n'enregistrer qu'une seule entrée
ayant une valeur finale de "0.6". De même, en ajustant une courbe, tous
les réglages de points de contrôle individuels sont regroupés en une
seule entrée dans l'historique. Si vous désirez enregistrer les
ajustements en deux entrées (ou plus), vous devez les séparer en
agissant sur un autre outil. Par exemple, supposons une courbe en mode
"Simulation de film" que vous désirez conserver dans ce mode, ajustez
plusieurs points de contrôle, puis basculez le mode de "Simulation de
film" en "Standard", puis à nouveau en "Simulation de film" pour créer
une nouvelle entrée dans l'historique et continuer les ajustements de la
courbe.

L'historique n'est pas enregistré, il est perdu aussitôt après la
fermeture de l'onglet Éditeur. Cependant, aucun des ajustements n'est
perdu car l'état final de tous les outils est enregistré dans le [le
fichier accolé](Sidecar_Files_-_Processing_Profiles/fr.md), prêt
à être utilisé la fois suivante où vous ouvrirez cette image.

### Captures

Sous le panneau *Historique* se trouve la panneau *Captures*. Sa raison
d'être est de permettre la sauvegarde de la photo avec tous les
ajustements réalisés jusqu'alors, puis de continuer les modifications
pour donner une apparence différente à la photo, tout en sauvegardant de
nouvelles captures à chaque fois que vous avez le sentiment d'avoir
atteint une version de la photo qui mérite une sauvegarde. Dès que vous
avez deux captures ou plus, il suffit de cliquer dessus pour visionner
les différentes versions et ne conserver que la préférée. Dans le futur,
les captures seront sauvegardées dans le fichier accolé PP3. Pour
l'instant, l'historique et les captures sont perdus lorsqu'une nouvelle
photo est chargée dans l*'Editeur* ou à la fermeture de RawTherapee.

## Le panneau de droite

Le panneau de droite affiche optionnellement l'histogramme principal et
le sélecteur de *Profils de traitement* ("*Préférences \> Général \>
Habitudes de travail \> Histogramme dans le panneau de gauche/Affiche le
sélecteur de profils*"), et en permanence la [boite à
outils](Toolbox/fr.md). Vous pouvez cacher ce panneau en
utilisant l'icône Montrer/Cacher ![Hide right panel
icon](panel-to-right.png "Hide right panel icon") ou le [raccourci
clavier](Keyboard_Shortcuts/fr.md).

### Sélecteur de profil de traitement

La liste déroulante *Profils de traitement* permet d'appliquer des
[profils de
traitement](Sidecar_Files_-_Processing_Profiles/fr.md) fournis
ou personnalisés. Voir l'article [Où sont les
fichiers](File_Paths/fr.md) pour savoir où ces profils de
traitement sont enregistrés sur votre système. Faire attention au bouton
"*Mode de complètement des profils de traitement*"

Bouton pressé [image:Profile-filled.png](image:profile-filled.png)  
Quand le bouton est activé et que vous ouvrez un profil partiel, les
valeurs manquantes seront remplacées par les valeurs par défaut
programmées dans RawTherapee.

Par exemple si vous appliquez un profil partiel qui ne contient que le
paramétrage de la netteté, tous les autres outils (Exposition,
Compression tonale, Réduction du bruit, redimensionnement, etc.)
prendront leur position par défaut.

Bouton relevé [image:Profile-partial.png](image:profile-partial.png)  
Quand le bouton est désactivé et que vous ouvrez un profil partiel,
seulement ces valeurs du profil seront appliquées, et les autres
resteront inchangées.

Par exemple si vous appliquez un profil partiel qui ne contient que le
paramétrage de la netteté, ce paramétrage sera seul appliqué et les
autres outils restent inchangés.

La position de ce bouton ne fait aucune différence si vous appliquez un
profil complet, mais la plupart des profils fournis avec RawTherapee
sont partiels (pour une bonne raison).

### Boite à outils

La *Boite à outils*, dans le panneau de droite, contient tous les outils
nécessaires au peaufinage de vos photos. Chaque outil possède sa propre
page dans RawPedia.

## Modes de l'onglet Editeur

RawTherapee dispose de deux modes pour travailler les photos :

- *Editeur unique* (ou SETM pour Single Editor Tab Mode), avec lequel
  vous ne travaillez que sur une seule photo à la fois, et chaque photo
  est ouverte dans le même onglet *Editeur*. Il y a un panneau
  horizontal appelé *[bande
  film](The_Image_Editor_Tab/fr#La_bande_film.md)* en haut de
  l'onglet *[Editeur](the_image_editor_tab/fr#la_bande_film)*
  affichant les autres photos du répertoire pour y accéder facilement.
  Il y a aussi des boutons *Image précédente* et *Image suivante*
  ![<File:Nav-prev.png>](Nav-prev.png "File:Nav-prev.png")
  ![<File:Nav-next.png>](Nav-next.png "File:Nav-next.png") dans la barre
  d'outils du bas (et des [raccourcis
  clavier](Keyboard_Shortcuts/fr.md) équivalents) pour basculer
  vers l'image précédente/suivante.
- *Editeur multiple* (ou METM pour Multiple Editor Tabs Mode), avec
  lequel chaque photo est ouverte dans son propre onglet
  *[Editeur](the_image_editor_tab/fr#la_bande_film)*. La
  *[bande film](the_image_editor_tab/fr#la_bande_film)* est
  cachée dans ce mode et il n'y a pas de boutons précédent/suivant.
  Avoir plusieurs photos ouvertes en même temps requière plus de RAM.

Essayez les deux modes et voyez lequel vous convient le mieux. Pour
cela, cliquer sur l'icône *Préférences* [Preferences
icon](image:preferences.png.md) située en bas à gauche ou en
haut à droite de la fenêtre de RawTherapee, choisir "*Général \>
Habitudes de travail \> Disposition de l'éditeur*" et sélectionnez votre
préférence.

Utilisez aussi cette fenêtre *Préférences* pour sélectionner une autre
langue a utiliser dans l'interface utilisateur, pour choisir un autre
thème de couleurs, pour changer la taille de police, etc.

Il est aussi possible de démarrer RawTherapee en mode sans Navigateur de
fichiers (sans l'onglet *Navigateur de fichiers*) en spécifiant à
RawTherapee d'ouvrir une image depuis le gestionnaire de fichiers de
votre système d'exploitation (en d'autres termes, cliquez droit sur une
photo et cliquez sur "*Ouvrir avec... \> RawTherapee*") ou en donnant le
nom de l'image en argument au lancement de RawTherapee en ligne de
commande (`rawtherapee /chemin/vers/une/photo.raw`). Ce mode fut
introduit pour ceux qui ont peu de RAM, car l'absence du *Navigateur de
fichiers* fait que RawTherapee utilise un peu moins de mémoire.
Cependant, en pratique la quantité de mémoire économisée est faible et
les inconvénients à l'usage ne compensent pas le faible bénéfice, il est
donc probable que ce mode soit supprimé dans le future (voir [issue
2254](https://code.google.com/p/rawtherapee/issues/detail?id=2254)).

## La bande film

<figure>
<img src="/images/Rt_filmstrip_21_toolbar-visible.jpg"
title="Rt_filmstrip_21_toolbar-visible.jpg" />
<figcaption>Rt_filmstrip_21_toolbar-visible.jpg</figcaption>
</figure>

<figure>
<img src="/images/Rt_filmstrip_21_toolbar-hidden.jpg"
title="Rt_filmstrip_21_toolbar-hidden.jpg" />
<figcaption>Rt_filmstrip_21_toolbar-hidden.jpg</figcaption>
</figure>

Si vous utilisez le mode "Editeur unique" ("*Préférences \> Général \>
Habitudes de travail*") vous pouvez afficher un panneau horizontal
au-dessus de l'aperçu, cela s’appelle la *Bande film* (ou Pellicule
d'image). Elle contient une vignette de toutes les images présentes dans
l'album actuellement ouvert, et elle est synchronisée avec l'image
actuellement ouverte si bien que vous pouvez utiliser les [raccourcis
clavier](Keyboard_Shortcuts/fr.md) et les boutons image
précédente ![Open previous image
icon](nav-prev.png "Open previous image icon") et image suivante ![Open
next image icon](nav-next.png "Open next image icon") pour ouvrir les
images précédentes/suivantes sans avoir besoin de retourner dans
l'onglet *[Navigateur de fichiers](the_file_browser_tab/fr)*

A partir de la version 4.2.10 de RawTherapee, on peut cacher la barre
d'outils de la bande film pour économiser l'espace à l'écran. Il y a
deux façon de procéder : une qui ne fait que basculer la barre d'outils
en mode affiché/caché sans redimensionner la bande film dans la hauteur,
l'autre agit de même mais en plus redimensionne automatiquement la
hauteur de la bande film. Les deux ne sont commandées que via les
[raccourcis clavier](keyboard_shortcuts/fr). Vu que le
redimensionnement de la bande film déclenche le rafraîchissement de
l'aperçu et que cela peut prendre du temps si des outils gourmands en
temps processeur comme la réduction du bruit d'une image zoomée à 100%,
le mode qui ne redimensionne pas a été implanté à l'intention des
utilisateurs ayant de faibles machines. Ceux qui en utilisent de rapides
préféreront le mode avec redimensionnement automatique.

## Profil de l'écran et épreuvage à l'écran

Les widgets sous l'aperçu principal dans RawTherapee 5 vous permet
d'appliquer un profil couleur d'écran sur l'image dans l'aperçu. Cela
apporte un aperçu immédiat et précis de leur travail aux utilisateurs
qui ont calibré et profilé leur écran, que ce soit avec sRGB ou un gamut
étendu. A noter que les utilisateurs de OS X sont limités au sRGB et ne
pourront obtenir un aperçu optimum ([voir la
discussion](https://discuss.pixls.us/t/wide-gamut-preview-in-os-x/2481)),
alors que les utilisateurs de Linux ou de Windows obtiendront un aperçu
correct avec un gamut étendu.

Allez dans Préférences \> [Gestion des
couleurs](Preferences/fr#L'onglet_Gestion_des_couleurs.md) et
indiquez au "Dossier des profils ICC" le répertoire dans lequel vous
avez enregistré les profils ICC de vos écran et imprimante. Redémarrer
RawTherapee pour la prise en compte des modifications. Maintenant vous
pouvez sélectionner le profil couleur de votre écran dans la liste
déroulante sous l'aperçu. Utiliser la "Colorimétrie relative" dans
l'Intention de rendu, à moins que vous n'ayez une bonne raison de
choisir autre chose.

Il est possible aussi de valider l'épreuvage à l'écran de l'aperçu. Cela
vous présentera l'image telle qu'elle apparaîtra une fois transformée
par le profil de l'imprimante indiqué dans Préférences \> [Gestion des
couleurs](Preferences/fr#L'onglet_Gestion_des_couleurs.md). Si
vous désirez ajuster une image pour l'impression et que vous disposez du
profil ICC du couple imprimante/papier, vous pouvez le définir comme
étant votre profil de sortie, cocher "Compensation du point noir" dans
Préférences, afin que le point le plus noir de votre image corresponde
au point le plus noir dont votre couple imprimante/papier est capable,
puis activer Epreuvage écran. Vous apercevez alors votre image telle
qu'elle serait si vous l'imprimiez. Cela permet de réaliser des réglages
et d'obtenir un aperçu immédiat du résultat, vous économisant le temps
et l'encre des épreuves imprimées.

L’icône avec un point d'exclamation auprès de l'épreuvage à l'écran
grise les zones qui ne sont pas reproductibles par l'imprimante, par
exemple les zones où des détails seront perdus.

Afin d'avoir un aperçu d'épreuvage à l'écran de qualité, vous devez
disposer d'un écran calibré et profilé.

Les entrées visibles dans la liste déroulante (sous l'aperçu principal)
et dans la liste déroulante des profils de l'imprimante (Préférences \>
[Gestion des
couleurs](Preferences/fr#L'onglet_Gestion_des_couleurs.md) sont
les fichiers ICC placés dans un répertoire que vous devez désigner à
RawTherapee en allant dans [Préférences](preferences/fr) \>
[Gestion des
couleurs](Preferences/fr#L'onglet_Gestion_des_couleurs.md) \>
Dossier des profils ICC.
