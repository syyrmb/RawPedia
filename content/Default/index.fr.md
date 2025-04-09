---
title: Default fr
contributors:
  - Lebarhon
---

# Défaut

Lorsque vous ouvrez une photo raw que vous avez préalablement ouverte,
RawTherapee récupère évidemment les paramétrages précédemment définis
pour l'exposition, la netteté, le recadrage, etc. Cependant, la première
fois que vous ouvrez une photo, RawTherapee utilise le profil de
traitement "Default" (Défaut) (a moins que vous n'ayez changé le profil
de traitement par défaut des photo raw dans "Préférences \> Traitement
de l'image \> Paramètres de traitement d'image par défaut"). Ce profil
contient essentiellement des réglages neutres agrémentés de quelques
ajustements, ce qui devrait conduire à une photo plaisante que vous
pouvez continuer à peaufiner selon votre goût. En particulier, il
utilise Niveaux Auto pour obtenir une tonalité et une exposition
correctes, une Netteté modérée, une suppression automatique de
l'aberration chromatique et les pixels chauds/morts sont traités par
l'outil de pré-traitement. L'image produite n'aura pas le même aspect
que le JPEG sorti par l'appareil photo (ni le même que la vignette
originale que vous avez aperçue pour cette photo, puisqu'elle est
identique au JPEG sorti par l'appareil photo).

Lors de l'ouverture pour la première fois de fichiers non-raw (JPEG,
TIFF ou PNG), RawTherapee utilise un profil différent, le profil
"Neutral" (neutre) (a moins que vous n'ayez changé le profil de
traitement par défaut des photos non-raw dans "Préférences, comme décrit
ci-dessus). le profil "Neutral" n'applique aucun changement à l'image et
ainsi donne un point de départ qui est, eh bien, neutre !

RawTherapee est configuré pour utiliser le profil "Default" pour les
photos raw et le profil "Neutral" pour les photos non-raw, par défaut
après une nouvelle installation. Si cela ne vous donne pas satisfaction,
vous pouvez les changer dans "Préférences \> Traitement de l'image \>
Paramètres de traitement d'image par défaut". La page [Création de
profils de traitement d'usage
général](Creating_processing_profiles_for_general_use/fr.md)
vous aidera à créer de bons profils personnalisés.
