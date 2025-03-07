---
title: Dynamic processing profiles fr
contributors:
  - Lebarhon
---

<div class="pagetitle">

Profils de traitement dynamiques

</div>

<figure>
<img src="dynamic-profile-rules-screenshot.png"
title="dynamic-profile-rules-screenshot.png" />
<figcaption>dynamic-profile-rules-screenshot.png</figcaption>
</figure>

Quelques fois un simple profil de traitement "statique" n'est pas
suffisant pour couvrir tous les cas d'utilisation. Par exemple, la
quantité de réduction du bruit qui doit être appliquée varie selon
l’appareil photo et le réglage ISO utilisés. Un autre exemple est la
nature et la quantité de la correction de l'objectif nécessaires, ce qui
est de toute évidence dépendant de l'objectif utilisé.

Pour traiter de tels cas, RawTherapee fournit une fonctionnalité qui
permet de créer un profil de traitement par défaut "dynamiquement", basé
sur les métadonnées de l'image en cours de taritement (telles que le nom
de l'appareil et de l'objectif, vitesse de l'obturateur, valeur ISO, et
autres)

Cela se réalise en définissant un jeu de "règles de profil dynamique".
Chaque règle possède un [profil de traitement
(partiel)](Creating_processing_profiles_for_general_use/fr.md)
qui lui est attaché, plus certaines conditions sur les métadonnées de
l'image qui définissent si la règle est applicable. Lorsque qu'une image
est éditée pour la première fois, la liste des règles est scannée et
tous les profils qui correspondent sont combinés (dans un ordre donné,
ainsi les règles suivantes peuvent écraser les premières) pour produire
le profil de traitement initial.

Pour activer la fonctionnalité, le [paramètres de traitement d'image par
défaut](Preferences/fr#Paramètres_de_traitement_d'image_par_défaut.md)
doit être paramétré sur "(Dynamic)". Les règles sont définies dans
l'onglet [Règles du profil
dynamique](Preferences/fr#L'onglet_Règles_du_profil_dynamique.md)
de la fenêtre Préférences.

Dans le but d'invoquer la chaîne du profil de traitement dynamique dans
un traitement par lots, après avoir configuré les règles du profil
dynamique et avoir défini à "(Dynamique)" le profil par défaut pour les
photos raw/non-raw, sélectionner plusieurs photos dans le Navigateur de
Fichiers, cliquer droit sur n'importe quelle photo sélectionnée et
cliquer sur "Opérations sur les profils \> Réinitialiser au traitement
par défaut" dans le menu contextuel qui apparaît.

Les règles du profil dynamique fonctionnent sur les métadonnées
suivantes de l'image :

Appareil photo  
le nom de l'appareil (y compris la marque) comme indiqué en
surimpression en haut de l'aperçu de
[l'éditeur](The_Image_Editor_Tab/fr.md) (non présent sur l'image
visible dans ce lien). Si activée, par défaut cette entrée appliquera la
règle à toutes les images réalisées uniquement avec l'appareil spécifié
(le nom est sensible à la casse). Cependant, si l'entrée commence par le
préfixe `re:`, alors la suite de la chaîne de caractères sera
interprétée comme étant une [expression
rationnelle](https://fr.wikipedia.org/wiki/Expression_rationnelle) à
utiliser pour la recherche de correspondance. Par exemple, une règle
avec une entrée d'appareil photo notée `re:SONY ILCE-[56].00`
s'appliquera à tous les appareils Sony Alpha a5xxx and a6xxx.

<!-- -->

Objectifs  
Le nom complet de l'objectif. Come ci-dessus, une expression rationnelle
peut être utilisée en commençant par le préfixe `re:`.

<!-- -->

ISO  
La gamme des valeurs ISO.

<!-- -->

Ouverture  
La gamme des ouvertures de l'objectif, mesurés en [nombre
d'ouverture](https://fr.wikipedia.org/wiki/Ouverture_(photographie)).

<!-- -->

Distance focale  
La gamme des longueurs focales utilisées, en mm.

<!-- -->

Obturateur  
La gamme des vitesses d'obturation, en secondes. Par exemple, entrer
0.03 pour une vitesse de 1/30".

<!-- -->

Compensation d'exposition  
La gamme des compensations d'exposition, en pas.
