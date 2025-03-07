---
title: Negative de
contributors:
  - Fherb
---

Todo-List / State:

- Translation: open
- Content completely cleared: open
- Expression and didactics checked: open
- Spelling checked: open

Ready for publishing: no

------------------------------------------------------------------------

# Negativbilder

Vielleicht arbeitest du bei deinen Aufnahmen noch immer mit *analogem*
Filmmaterial. Oder du möchtest ältere Filme, die du eingescannt hast,
bearbeiten. Meist handelt es sich dabei um sogenannte Negative.
Bedeutet, helle Stellen im Bild werden dunkel wiedergegeben und dunkle
Stellen hell. Bei Farbnegativfilmen kommt noch eine zusätzliche
braun-orange Maskierung dazu und die Farben erscheinen auf den ersten
Blick genau so negativ gemischt.

RawTherapee besitzt keine unmittelbare Ein-Klick-Unterstützung für
Negativmaterial. Aus diesem Grund beschreibt diese Seite etwas
ausführlicher, wie solche Bilder trotzdem mit RawTherapee bearbeitet
werden können.

------------------------------------------------------------------------

Auf Grund der noch nicht übersetzen Seite "Filmsimulation", auf die hier
immer wieder verwiesen wird, übersetze ich den folgen Abschnit noch
nicht:

1.  Invert a diagonal [tone curve](Exposure#Tone_Curves.md)
    either in the Exposure tool, or all of the curves in the [RGB
    Curves](RGB_Curves.md) tool. In the Color Management tool
    select "[No profile](Color_Management#No_Profile.md)" as the
    input profile. The downside is that there are tonal shifts when
    doing this.
2.  Use a negative Hald CLUT via the [Film
    Simulation](Film_Simulation.md) tool. The "RawTherapee Film
    Simulation Collection" contains one, get it from the [Film
    Simulation](Film_Simulation.md) page. The downside is that
    some controls might operate in reverse, such as the Exposure slider,
    and you may experience clipping in the shadows and/or highlights as
    these tools are not designed to work with negatives.
3.  In addition to using the neutral negative Hald CLUT as described
    above, if you have a successful workflow of not only inverting
    negatives but also toning them to your liking in RawTherapee or in
    other software, you could [make your own negative Hald
    CLUT](Film_Simulation#Make_Your_Own.md) which reproduces the
    whole look including negative inversion. To do that, apply the same
    steps to the "identity Hald CLUT image" shipped with the RawTherapee
    Film Simulation Collection as you would to a photo negative, save it
    under a new name, then open a photo negative in RawTherapee and
    apply that new Hald CLUT image. This lets you instantly achieve not
    only negative inversion but also your own toning with the click of a
    button, leaving you only needing to expand the histogram by
    adjusting the Exposure slider or using curves.
4.  Currently the best method is to use the DCP (DNG Camera Profile) for
    your camera model but edited in DNG Profile Editor so that the
    diagonal tone curve is inverted, then manually loading this DCP in
    RawTherapee for all negative shots. Method outlined below.

------------------------------------------------------------------------

## Ein DCP für Negative erstellen

<figure>
<img src="DNG_Profile_Editor_inverted_tone_curve.png"
title="DNG_Profile_Editor_inverted_tone_curve.png" />
<figcaption>DNG_Profile_Editor_inverted_tone_curve.png</figcaption>
</figure>

<figure>
<img src="Rt_negative_dcp_l_curve.png"
title="Rt_negative_dcp_l_curve.png" />
<figcaption>Rt_negative_dcp_l_curve.png</figcaption>
</figure>

1.  Lade dir den [DNG Profile
    Editor](http://www.adobe.com/support/downloads/detail.jsp?ftpID=5494)
    herunter. Unter Linux arbeitet das Tool auch gut mittels
    [wine](https://www.winehq.org/).
2.  Konvertiere eins deiner Fotos, egal ob aus der Kamera oder gescannt,
    zu DNG. Lies hierzu die Anleitung "[Raw-Bilder zu DNG
    konvertieren](How_to_convert_raw_formats_to_DNG/de.md)".
3.  Öffne das DNG-Bild im DNG Profile Editor
4.  Prüfe in der Registerkarte *Color*, ob das Basisprofil "Adobe
    Standard (*<Dein Kameramodell>*) vorhanden ist. Wenn ja, wähle es
    aus. Wenn nein, wähle "Choose external profile" und suche das File
    mit der Bezeichnung "*<your camera model>* Adobe Standard.dcp". Die
    Anleitung "[Wie werden LCP- und DCP-Profile
    erstellt?](How_to_get_LCP_and_DCP_profiles/de.md)" erklärt,
    wie man zu diesem File kommt.
5.  Invertiere die Diagonale in der Registerkarte *Tone Curve* so, dass
    sie von links oben nach rechts unten geht.
6.  Auch noch in *Tone Curve* gibt es die Wahl zwischen drei *Base Tone
    Curves*. "Base Profile" und "Camera Raw Default" sind für gewöhnlich
    identisch und liefern mehr Kontrast, während "Linear" das Bild
    flacher wirken lässt. Zu empfehlen ist, ein DCP mit "Base Profile"
    und eins mit "Linear" abzuspeichern und in RawTherapee zu
    entscheiden, welche Variante dir besser geeignet scheint. Beide DCPs
    benötigen eine Überarbeitung mit RawTherapee, aber "Linear" benötigt
    eher mehr davon als "Base Curve". Wobei mit "Base Curve" die Farben
    auch schnell mal übersättigen könen. Also aufpassen.
7.  Um das DCP zu erstellen, klicke auf "File \> Export
    *<your camera model>* profile...". Zu empfehlen ist, wie im
    vorhergehenden Schritt angesprochen, zwei Versionen zu speichern.

Um nun dieses DCP für Negative zu verwenden, öffne das Negativ im Editor
von RawTherapee, gehe zu *Registerkarte Farbe \> Farbmanagement \>
Eingangsfarbprofil*, wähle *DCP/ICP-Profil* und suche dazu das neue
DCP-File heraus. Selektiere noch *DCP \> Tonwertkurve*.

Wenn du in RawTherapee Bilder unter Verwendung von DCPs bearbeitest,
denke daran, dass bei der Verwendung von Tonwertkurven, die mit den
RGB-Kanälen arbeiten (Tonwertkurve 1 und 2 im Werkzeug *Belichtung*),
nicht nur die Helligkeiten verändert werden, sondern auch die
Farbsättigung. Steuere entweder die Farbsättigung unter Verwendung der
Tonwertkurven-Modes "Gewichteter Standard" und "Sättigung und
Überlagerung" oder du vermeidest das Problem ganz, wenn du im
L\*a\*b-Farbraum arbeitest. Der Vorteil hierbei ist, dass die L\*-Kurve
zur Korrektur der Helligkeit nicht die Farben ändert. Korrigiere also
zuerst im Helligkeitsbereich mit der L\*-Kurve und danach die
Farbsättigung mit z.B. der CC-Kurve.
