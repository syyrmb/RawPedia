---
title: IPTC Tab
contributors:
  - DrSlony
  - XavAL
  - Lebarhon
---

<div class="pagetitle">

IPTC Tab

</div>

[IPTC](https://en.wikipedia.org/wiki/IPTC_Information_Interchange_Model)
values are metadata, as they are stored in the image files but do not
affect the actual image. Basically the metadata summarized as IPTC
contains additional information about your image. As this information is
saved within the image file it cannot get lost. This eases the workflow
a lot as you don't have to care about other files when backing up or
sorting your images.

IPTC is usually used to describe the image in detail. There are a lot
image database software that use the (IPTC) information saved in images
to e.g. fill their descriptive fields. For example you can also use IPTC
fields when you try to sell your images. Most online image-selling
companies support IPTC tags and read them when you upload your images to
their databases, thus you have less work. Adding keywords to your images
on your home computer once while developing the photo is much more
comfortable and efficient than doing so through the web browser every
time you share an image. Multiple "Keywords" and "Suppl. Categories"
(Supplemental Categories) can be added/removed using the plus
[image:List-add-small.png](image:List-add-small.png.md) and
minus
[image:List-remove-red-small.png](image:List-remove-red-small.png.md)
signs next to them.

There are three buttons:

- "[image:Gtk-undo-ltr.png](image:Gtk-undo-ltr.png.md) Reset"
  resets the IPTC values to those saved in your current processing
  profile.
- "[image:Gtk-copy.png](image:Gtk-copy.png.md)" copies your
  current IPTC setting to the clipboard. This is especially useful when
  you you want to apply the same IPTC values to multiple images.
- "[image:Gtk-paste.png](image:Gtk-paste.png.md)" pastes the
  formerly copied IPTC settings from the clipboard to your current
  image.

## Technical Details

IPTC strings are handled by `libiptcdata`. When saving strings, RT sets
`IPTC_TAG_CHARACTER_SET` to UTF-8.
