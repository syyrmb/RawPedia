---
title: Clipping Indication fr
contributors:
  - Lebarhon
---

Les indicateurs ombres
![<File:Warning-shadows.png>](Warning-shadows.png "File:Warning-shadows.png")
ou
![<File:Warning-highlights.png>](Warning-highlights.png "File:Warning-highlights.png")
hautes lumières hors domaine dans l'onglet Editeur permettent de
facilement repérer les zones de l'image qui sont trop sombres ou trop
claires. Les zones mises en évidence sont grisées en proportion du
dépassement du seuil.

Les seuils de ces indicateurs sont définis dans Préférences \> Général.

L'indicateur **ombres** hors domaine met en évidence les zones où les
trois canaux sont égaux ou en-dessous du seuil pour le dépassement de
domaine inférieur spécifié.

L'indicateur **hautes lumières** hors domaine met en évidence les zones
où au moins un canal est égal ou au-dessus du seuil supérieur de
dépassement de domaine spécifié. Si vous ne désirez voir que les
endroits où tous les canaux sont hors domaine, activez le mode aperçu de
la luminosité en plus de l'indicateur des hautes lumières hors domaine.
Voir [Modes
d'aperçu](The_Image_Editor_Tab/fr#Modes_d'aperçu.md).

Le dépassement est calculé a l'aide des données qui dépendent de l'état
du bouton gamut
![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png") situé
au-dessus de l'aperçu principal dans l'onglet Editeur. Lorsque ce bouton
est activé le profil de travail est utilisé, sinon est utilisé le profil
de sortie corrigé par le gamma.
