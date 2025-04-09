---
title: How to get Nikon ICM profiles fr
contributors:
  - Lebarhon
---

<div class="pagetitle">

Comment obtenir des profils Nikon ICM

</div>

Capture NX-D, Capture NX 2 et ViewNX-i sont des logiciels propriétaires
pour Windows fournis pour les appareils photo Nikon et sont capables de
développer avec précision des images raw en accord avec le rendu de
l'appareil photo. En arrière plan, ces programmes génèrent des profils
ICC qui incorporent des recettes pour les changements de tonalité en
fonction des réglages. Ces profils peuvent être utilisés par RawTherapee
comme profils d'entrée pour arriver à un rendu presque identique, en
suivant la même recette. Les profils ICC d'entrée de Nikon sont des
programmes propriétaires et ne peuvent pas être distribués.
Heureusement, ce logiciel extrait et génère les profils d'entrée à la
volée dans un répertoire temporaire au cours de son exécution. Veuillez
utiliser ces profils dans le respect de la licence des logiciels Nikon.
Ce procédé fonctionne avec les versions enregistrées et les versions
d'essai de ces programmes.

1.  Vous devez d'abord installer l'un de ces programmes.
2.  Ouvrez le fichier NEF dedans et regardez dans ce répertoire caché :
      
    `%APPDATA%\Local\Temp\Nkn`<random strings>`.tmp`

    Les profils ICC temporaires seront créés dans ce répertoire, ils
    ressemblent à cela :

    `Nkx_D90_962_1_03_0_00_10_00_00_00_05_00_0200_0_0_476.icm`

    Sous Windows XP, le chemin est différent :

    `%TEMP%\Nkn`<random string>`.tmp`
3.  Sous "Contrôle de l'image" (Picture Control), cliquer sur le bouton
    "Lancer l'utilitaire" (Launch Utility). Pendant que l'utilitaire
    fonctionne, les profils apparaîtront temporairement dans les
    répertoires indiqués ci-dessus. Ils apparaissent ici car Nikon
    applique des profils génériques à vos images, ils sont appelés
    paramètres de "contrôle de l'image" ("picture control” settings).
    Par exemple, Capture NX 2 possède les profils "neutral", "standard"
    et "monochrome". Pour les utiliser avec RawTherapee, vous devez
    savoir que Nikon génère différents profils ICM avec chaque
    paramétrage différent. Pour faciliter les choix, les paramètres
    "neutral", "standard", "vivid" et "paysage" sembles similaires,
    excepté l'augmentation de la saturation et du contraste. Vous
    devriez être capable d'ajuster les courbes tonales de RawTherapee et
    donc de vous satisfaire du profil "neutral" comme point de départ.

**Note**: D'autre paramètres peuvent aussi générer de nouveaux fichiers
ICM ! Vous devez être particulièrement conscient que les photos prises
en lumière artificielle ont un profil différent, et utiliser de tels
profils pour des photos prises en lumière du jour conduira à des
couleurs dominantes. D-lighting modifie considérablement le contraste.
En cas de doute, ouvrez l'image particulière pour laquelle vous désirez
le profil de couleur dans l'un de ces programmes Nikon, et utilisez ce
profil dans RawTherapee. Le plus souvent, un profil de couleur générique
sera suffisant.
