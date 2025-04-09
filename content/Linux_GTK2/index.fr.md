---
title: Linux GTK2 fr
contributors:
  - Lebarhon
---

Cette page archivée détaille les instructions pour la compilation de la
version obsolète GTK2 de RawTherapee sur les vieux systèmes
**GNU/Linux**. La dernière version de RawTherapee à supporter GTK2 fut
celle labellisée `5.0-r1-gtk2` en février 2017.

## Dépendances

Pour compiler RawTherapee votre système nécessite un jeu d'outils et des
bibliothèques venues d'autres programmes. Ils sont appelés dépendances,
en voici la liste pour la version obsolète GTK2 de RawTherapee :

| Paquetage    | Version             | URL                                                                                |
|--------------|---------------------|------------------------------------------------------------------------------------|
| EXIV2        | exiv2\>=0.19        | <http://www.exiv2.org/>                                                            |
| EXPAT        | expat\>=2.1.0       | <http://expat.sourceforge.net/>                                                    |
| FFTW3        | fftw\>=3.2.2        | <http://fftw.org/>                                                                 |
| GCC          | gcc\>=4.9           | <http://gcc.gnu.org/>                                                              |
| GLIB2        | glib-2.0\>=2.24     | <http://www.gtk.org/>                                                              |
| GLIBMM       | glibmm-2.4\>=2.24   | <http://www.gtkmm.org>                                                             |
| GTK+         | gtk+-2.0\>=2.24.18  | <http://www.gtk.org/>                                                              |
| GTK2-Engines | gtk-engines-2.20.2  | <http://www.gtk.org/>                                                              |
| GTKMM        | gtkmm-2.4\>=2.22    | <http://www.gtkmm.org>                                                             |
| JPEG         | libjpeg\>=6b        | <http://libjpeg-turbo.virtualgl.org/> <http://jpegclub.org/> <http://www.ijg.org/> |
| LCMS2        | lcms\>=2.6          | <http://www.littlecms.com/>                                                        |
| LENSFUN      | lensfun\>=0.2       | <http://lensfun.sourceforge.net/>                                                  |
| LIBCANBERRA  | libcanberra\>=0.29  | <http://0pointer.de/lennart/projects/libcanberra/> (Linux only)                    |
| LIBIPTCDATA  | libiptcdata\>=1.0.2 | <http://libiptcdata.sourceforge.net>                                               |
| PNG          | libpng\>=1.2.44     | <http://www.libpng.org/>                                                           |
| SIGC         | sigc++-2.0          | <http://libsigc.sourceforge.net/>                                                  |
| TIFF         | libtiff\>=3.9.4     | <http://www.remotesensing.org/libtiff/>                                            |
| ZLIB         | zlib\>=1.2.3        | <http://www.zlib.net/>                                                             |

Dépendances pour RawTherapee:

Pour compiler la version 3 obsolète de RawTherapee, vous avez besoin de
:

| Paquetage | Version     | Gentoo          | Debian/Ubuntu | URL                         |
|-----------|-------------|-----------------|---------------|-----------------------------|
| LCMS1     | lcms\<=1.99 | media-libs/lcms | liblcms1-dev  | <http://www.littlecms.com/> |

Dépendances pour la version 3 obsoléte de RawTherapee :

Reportez vous à l'actuel article [Linux](Linux/fr.md) pour
obtenir les instructions de compilation et remplacez les dépendances de
GTK3 avec celles de GTK2 là où c'est nécessaire. Utilisez la branche
obsolète `5.0-r1-gtk2`, pas la branche `dev`.

### Debian/Ubuntu/Mint/elementary OS

#### Ubuntu 15.04, 14.10, 14.04 LTS

    sudo apt-get update
    sudo apt-get install build-essential cmake curl git libbz2-dev libcanberra-gtk-dev libexiv2-dev libexpat-dev libfftw3-dev libglibmm-2.4-dev libgtk2.0-dev libgtkmm-2.4-dev libiptcdata0-dev libjpeg8-dev liblcms2-dev libpng12-dev libsigc++-2.0-dev libtiff5-dev zlib1g-dev

RawTherapee exige une version de GCC égale ou supérieure à 4.9. Ubuntu
14.04 LTS est livré avec GCC version 4.8.2 ce qui est trop vieux. Pour
obtenir la version 4.9, suivre ces étapes :
<http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-on-ubuntu-14-04>

#### Ubuntu 13.10, 13.04, 12.10, 12.04 LTS, 11.10

Ces versions d'Ubuntu sont très dépassées. Le code ci-dessous fonctionne
habituellement mais cela peut s'arrêter à tout moment. Mettez votre
système d'exploitation à niveau.

Puisque ces versions d'Ubuntu ne supportent que GCC-4.8.1 ou plus vieux,
la dernière édition que vous pourrez compiler est [commit
b343b9a7](https://github.com/Beep6581/RawTherapee/commit/b343b9a7) du
29/12/2015. Les versions plus récentes ne sont pas compilables.

    sudo apt-get update
    sudo apt-get install build-essential cmake curl git libbz2-dev libcanberra-gtk-dev libexiv2-dev libexpat-dev libfftw3-dev libglibmm-2.4-dev libgtk2.0-dev libgtkmm-2.4-dev libiptcdata0-dev libjpeg8-dev liblcms2-dev libpng12-dev libsigc++-2.0-dev libtiff5-dev zlib1g-dev

#### Ubuntu 10.10 and 11.04

Ces versions d'Ubuntu sont très dépassées. Le code ci-dessous fonctionne
habituellement mais cela peut s'arrêter à tout moment. Mettez votre
système d'exploitation à niveau.

    sudo apt-add-repository ppa:dasprid/rawtherapee
    sudo apt-get update
    sudo apt-get install cmake curl git libbz2-dev libcanberra-gtk-dev libexiv2-dev libexpat-dev libglibmm-2.4-dev libgtk2.0-dev libgtkmm-2.4-dev libiptcdata0-dev libjpeg62 liblcms2-dev libnm-glib2 libpng12-dev libsigc++-2.0-dev libtiff4-dev zlib1g-dev
