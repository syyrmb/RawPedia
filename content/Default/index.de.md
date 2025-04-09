---
title: Default de
contributors:
  - Fherb
---

Todo-List / State:

- Translation: completed
- Content completely cleared: yes
- Expression and didactics checked: completed
- Spelling checked: open

Ready for publishing: no

------------------------------------------------------------------------

# Das Default-Bearbeitungsprofil

In den Standardeinstellungen wird für Raw-Fotos das Profil *Default* als
Start-Profil verwendet, wenn ein bisher noch nicht bearbeitetes Raw-Bild
im Editor geöffnet wird. (Bei allen anderen Fotos wird hingegen das
*Neutral*-Profil verwendet.) Falls das nicht gewünscht ist, kannst du
das umstellen. Siehe hierzu auch:

- [Standard-Bildverarbeitungsparameter](Preferences/de#Standard-Bildverarbeitungsparameter.md)
- [Erstellung von Bearbeitungsprofilen für die allgemeine
  Verwendung](Creating_processing_profiles_for_general_use/de.md)

Während das alternativ auch übliche Standardprofil *Neutral* bei
Raw-Fotos nur das Demosaicing bestimmt und den Weißabgleich auf "Kamera"
stellt, wird mit dem Profil *Default* noch etwas mehr getan:

- Im Belichtungswerkzeug wird die Automatikfunktion *Auto* ausgeführt,
  um in den meisten Fällen einen etwas praktischeren Startwert für die
  weitere Bearbeitung der Belichtung vorzugeben.
- Das Schärfen wird mit moderaten Parametern eingeschaltet. (Wieder
  abschalten, falls du später die Rauschminderung zuschaltest!)
- Die automatische Korrektur von chromatischer Aberration unter den
  Raw-Werkzeugen wird aktiviert.
- Unter *RAW \> Vorverarbeitung* wird der Hot- und Dead-Pixel-Filter
  zugeschaltet.

Diese Einstellungen werden selbstverständlich **nicht** das liefern, was
die Kamera als JPEG entwickelt hat. Dazu gehört auch das im Raw
eingebettete JPEG der Kamera, dass standardmäßig in den Miniaturbildern
angezeigt wird, solange noch keine Einstellungen getroffen wurden.

Statt dessen soll das *Default*-Profil einen Startwert für die
Raw-Bearbeitung liefern, der dir die Bearbeitungszeit etwas verkürzt.

Verwendest du standardmäßig immer, zumindest ein wenig, das
Rauschminderungswerkzeug, ist das *Default*-Profil nicht ganz optimal:
Du musst die Schärfung sinnvollerweise wieder abstellen. Und die
Hot-/Dead-Pixel-Filterung übernimmt sozusagen als Nebeneffekt auch der
Impulsrauschminderungsfilter. Denke hier über den Einstz von [eigenen
Bearbeitungsprofilen](Creating_processing_profiles_for_general_use/de.md)
anstatt des Default-Profils nach.
