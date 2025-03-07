---
title: Image file formats and compression fr
contributors:
  - Lebarhon
---

<div class="pagetitle">

Formats de fichiers image et compression

</div>

## Obsolescence

Bien que les informations données ici peuvent présenter un intérêt,
notez qu'elles sont obsolètes. RawTherapee 5.4 utilise une stratégie de
compression rapide et efficace pour les deux formats TIFF et PNG, et ces
deux formats supportent les métadonnées.

## Format intermédiaire

Un fichier intermédiaire est un fichier utilisé uniquement pour
transférer l'image d'un programme à l'autre pendant le travail sur
celle-ci, par exemple de RawTherapee vers Gimp ou Photoshop.

Le fichier intermédiaire idéal est un format sans pertes de données ou
métadonnées et qui est rapide en lecture ou écriture. Cela impose
fortement à toujours utiliser comme format intermédiaire le TIFF 16-bits
non compressé. Point final.

## Format final

Certaines choses sont à considérer pour décider du format à utiliser
pour le stockage de fichiers non-intermediares, par exemple, des images
dont le traitement est terminé, du film scanné, des images à grande
gamme dynamique, etc. :

- JPEG est le plus largement supporté mais cause des pertes de données
  et est limité à 8 bits par canal, 24 bits par pixel, dans la majorité
  des implémentations.
- TIFF et JPEG supportent les métadonnées, pas PNG, en général.
- TIFF peut utiliser plusieurs méthodes de compression (y compris celle
  utilisée par PNG : DEFLATE, aussi appelée Zip). Zip est la méthode de
  compression la plus efficace pour les photos du monde réel supportées
  par TIFF.
- PNG est lent et inefficace.
- Les images peuvent être extérieurement converties en d'autres format
  plus efficaces, tels que JPEG-2000 ou OpenEXR en 16-bits.

## Comparaison de compressions sans pertes

Le fichier d'entrée est un panorama du monde réel de 10000x5000 pixels
en 16 bits.

Pour convertir les formats j'ai utilisé ImageMagick-6.8.8.10 sur un PC
x86_64 Intel(R) Core(TM) i7 CPU Q 820 @ 1.73GHz, et j'ai réalisé un
script des étapes dans Bash.

### TIFF 16-bit

`for c in RLE None LZW Zip; do time convert foo.tif[0] -monitor -depth 16 -compress "$c" "${c}_16.tif"; ls -lh "${c}_16.tif"; done`

| Format      | Compression | Taille \[Mo\] | Temps\[s\] |
|-------------|-------------|---------------|------------|
| TIFF 16-bit | Aucune      | 382           | 5          |
| TIFF 16-bit | RLE         | 385           | 5          |
| TIFF 16-bit | LZW         | 293           | 8          |
| TIFF 16-bit | Zip         | 243           | 61         |

Effectivement, la taille obtenue par RLE est supérieure à celle de
l'image non compressée.

### TIFF 12-bit

`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 12 -compress "$c" "${c}_12.tif"; ls -lh "${c}_12.tif"; done`

| Format      | Compression | Taille \[Mo\] | Temps\[s\] |
|-------------|-------------|---------------|------------|
| TIFF 12-bit | Aucune      | 287           | 4          |
| TIFF 12-bit | LZW         | 248           | 9          |
| TIFF 12-bit | Zip         | 210           | 44         |

GIMP-2.9 et RawTherapee-4.2 ne lisent pas les fichiers 12-bit TIFF.

### TIFF 8-bit

`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 8 -compress "$c" "${c}_8.tif"; ls -lh "${c}_8.tif"; done`

| Format     | Compression | Taille \[Mo\] | Temps\[s\] |
|------------|-------------|---------------|------------|
| TIFF 8-bit | Aucune      | 191           | 3          |
| TIFF 8-bit | LZW         | 51            | 4          |
| TIFF 8-bit | Zip         | 49            | 41         |

### TIFF 16-bit virgule flottante

`for c in None LZW Zip; do time convert foo.tif[0] -monitor -define quantum:format=floating-point -compress "$c" "${c}_fp.tif"; ls -lh "${c}_fp.tif"; done`

| Format                        | Compression | Taille \[Mo\] | Temps\[s\] \[s\] |
|-------------------------------|-------------|---------------|------------------|
| TIFF 16-bit virgule flottante | Aucune      | 382           | 6                |
| TIFF 16-bit virgule flottante | LZW         | 153           | 8                |
| TIFF 16-bit virgule flottante | Zip         | 133           | 72               |

### TIFF 64-bit double-précision virgule flottante

`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 64 -define quantum:format=floating-point -compress "$c" "${c}_64fp.tif"; ls -lh "${c}_64fp.tif"; done`

| Format                               | Compression | Taille \[Mo\] | Temps\[s\] |
|--------------------------------------|-------------|---------------|------------|
| TIFF 64-bit virgule flottante double | Aucune      | 1525          | 21         |
| TIFF 64-bit virgule flottante double | LZW         | 1016          | 36         |
| TIFF 64-bit virgule flottante double | Zip         | 551           | 104        |

### OpenEXR 16-bit virgule flottante

OpenEXR est un bon choix; il est moderne, efficace et largement
supporté.

`for c in None Zip PIZ; do time convert foo.tif[0] -monitor -depth 16 -compress "$c" "${c}_16.exr"; ls -lh "${c}_16.exr"; done`

| Format     | Compression | Taille \[Mo\] | Temps\[s\]\] |
|------------|-------------|---------------|--------------|
| EXR 16-bit | Aucune      | 382           | 13           |
| EXR 16-bit | Zip         | 106           | 21           |
| EXR 16-bit | PIZ         | 111           | 7            |

Pour convertir le format EXR vers le TIFF 16-bits, vous devez choisir
l'espace colorimétrique sRGB (le paramétrer, ne pas le transformer):

`convert Zip_16.exr -depth 16 -set colorspace sRGB suchwow.tif`

### PNG 16-bit

En fait, PNG. ImageMagick vous laisse paramétrer le niveau de
compression zlib de 1 à 9, ou utilise la compression Huffman si vous
paramétrez la première valeur à 0. La seconde valeur définit le filtre
d'encodage où 5=Adaptive, le meilleur pour les photos dans le monde
réel.

`for l in 0 6 9; do time foo.tif[0] -monitor -depth 16 -quality "${l}5" "${l}5_16.png"; ls -lh "${l}5_16.png"; done`

| Format     | Compression | Taille \[Mo\] | Temps\[s\] |
|------------|-------------|---------------|------------|
| PNG 16-bit | level 0     | 310           | 9          |
| PNG 16-bit | level 6     | 233           | 87         |
| PNG 16-bit | level 9     | 233           | 351        |

Remarquez la même taille de fichier pour les niveaux 6 et 9 malgré un
temps 4 fois plus long.

### PNG 8-bit

`for l in 0 6 9; do time foo.tif[0] -monitor -depth 8 -quality "${l}5" "${l}5_8.png"; ls -lh "${l}5_8.png"; done`

| Format    | Compression | Taille \[Mo\] | Temps\[s\] |
|-----------|-------------|---------------|------------|
| PNG 8-bit | level 0     | 137           | 10         |
| PNG 8-bit | level 6     | 49            | 40         |
| PNG 8-bit | level 9     | 46            | 341        |
