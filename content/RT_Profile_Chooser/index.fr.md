---
title: RT Profile Chooser fr
contributors:
  - Lebarhon
---

# Sélecteur de profil pour RT

Si vous possédez plusieurs appareils photo et divers objectifs, le
script **RT Profile Chooser (Sélecteur de profil pour RT)** peut vous
aider dans l'attribution des profils personnalisés sur la base des
combinaisons *boitier + objectif + type d'image et ISO*. Ce script en
python est un script qui valide la possibilité d'exécuter des programmes
extérieurs depuis Rawtherapee pour manipuler les profils des images. Une
fois paramétré, le script est lancé avec la première ouverture d'une
image, il applique un profil de votre choix (un nouveau ou un de ceux
livrés avec RawTherapee) à l'image ouverte. Cela donne un point de
départ qui peut alors être ajusté manuellement en utilisant les outils
de RawTherapee pour atteindre le résultat désiré.

Par exemple, lorsque RawTherapee est utilisé sans aucun paramétrage
("out of the box") un profil d'image est attribué au profil 'default'.
Avec **RT Profile Chooser**, vous pouvez attribuer un autre profil à
l'image, ou même attribuer le profil fourni 'Default ISO High' (défaut
pour ISO élevés) quand la valeur des ISO enregistrée dans les
métadonnées de l'image est contenue dans un interval donné, disons
au-delà de 800 ISO. Ce script fournit un moyen de gérer quels profils
sont utilisés pour quelle image.

Vous pouvez le télécharger sur
[GitHub](https://github.com/SimonChristopherCropper/RT_ChooseProfile.git).
Il y a aussi un
[tutorial](http://www.fossworkflowguides.com/scripting/tutorials/00017/pdf/00017.pdf)
très utile sur la façon de configurer et d'utiliser le script.
