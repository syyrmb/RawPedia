---
title: Saving de
contributors:
  - Fherb
  - McCap
---

Todo-List / State:

- Translation: completed and contend added
- Content completely cleared: yes
- Expression and didactics checked: completed
- Spelling checked: no

Ready for publishing: no

------------------------------------------------------------------------

# Speichern

Die original Bilddatei wird von Rawtherapee nie verändert. Beim
Speichern wird aus dem Original und den aktuellen Einstellungen bzw. des
Bearbeitungsprofils als Sidecar-File das Resultat berechnet und dann in
einem von dir gewählten Format gespeichert.

Es gibt verschiedene Arten ein Bild im
[Bild-Editor](The_Image_Editor_Tab/de.md) zu speichern:

- ![Image:gtk-save-large.png](gtk-save-large.png "Image:gtk-save-large.png")
  Sofort aus dem Editor speichern,
- ![Image:processing.png](processing.png "Image:processing.png") Über
  die [Warteschlange](The_Batch_Queue/de.md) speichern,
- ![<File:Image-editor.png>](Image-editor.png "File:Image-editor.png")
  "[Edit Current Image in External
  Editor](Edit_Current_Image_in_External_Editor.md)" (wird in
  eigenem Artikel beschrieben).

## Direkt speichern

Klickt man im Editor auf das kleine Festplattensymbol
![Image:gtk-save-large.png](gtk-save-large.png "Image:gtk-save-large.png")
links unterhalb des Vorschaubilds, oder drückt man **Ctrl+s**, so
speichert man direkt. Dies entspricht dem bekannten "Speichern unter"
Dialog in vielen Programmen. Du kannst nun den Namen der Ausgabedatei,
den Speicherort, das Ausgabeformat (JPEG, TIFF oder PNG), die Bitrate
für TIFF und PNG (8 oder 16) und die Kompression festlegen, und du
kannst enscheiden ob die Verarbeitungsparameter mit abgespeichert werden
sollen. Des Weiteren kannst du wählen ob du wirklich sofort speichern
willst oder ob du das Bild doch an den Anfang oder das Ende der
Warteschlange stellen willst. Das Tastenkürzel für den "OK" Knopf ist
**Ctrl+Enter**.

Schau dir die Optionen im Dialogfeld an: Wählst du "*Bild speichern*"
wird Rawtherapee dein Bild verarbeiten und speichern nachdem du den
"*OK*" Knopf gedrückt hast. Während des Speicherprozesses wird
Rawtherapee langsamer reagieren. Der Verarbeitungsvorgang inkl. Export
in das Dateiformat kann durchaus bis in den einstelligen Minutenbereich
dauern. Zu empfehlen ist deshalb die Warteschlange zu benutzen, falls du
nicht nur dieses eine Bild bearbeiten willst und falls du das Bild nicht
sofort benötigst, um weiterarbeiten zu können. Die Warteschlange kannst
du nach deiner getanen Arbeit laufen lassen. Kaffee trinken oder die
Nachtarbeit für dich beenden. Für die Warteschlange gibt es aber auch
einen schnelleren "Hinzufügen"-Button:

## Bild zur Warteschlange hinzufügen

Klickst du auf
![Image:processing.png](processing.png "Image:processing.png")
(alternativ die oben beschriebene "Direkt speichern"-Methode mit Auswahl
der Warteschlange), wird dein Bildentwicklungsauftrag nun tatsächlich
einem Stapel zugefügt. Und da bleibt er erstmal liegen und verbraucht
keine Prozessorleistung. Damit kannst du sofort die Bearbeitung weiterer
Bilder fortsetzen. Oder am gleichen Bild noch andere Einstellungen
tätigen. Zum Beispiel das Bild mit anderem Beschnitt oder anderer
Auflösung speichern.

### Dateiformat wählen

Hier gibt es nun den eigentlich entscheidenden Unterschied zwischen
beiden Speichermethoden:

- *Bild speichern*
  ![Image:gtk-save-large.png](gtk-save-large.png "Image:gtk-save-large.png")
  erlaubt dir, für dieses Bild das Dateiformat, gegebenenfalls die
  Farbauflösung und die Kompressionsstärke vorzugeben. Auch, wenn du es
  von hier aus in die Warteschlange einfügst.
- Legst du das Bild einfach nur in die Warteschlang
  (![Image:processing.png](processing.png "Image:processing.png")), wird
  das Zielformat und dessen Einstellungen verwendet, die in dem Register
  *Warteschlange* konfiguriert werden.

## Automatische Datei-Benennung

RawTherapee unterstützt dich bei der Benennung des gespeicherten Bildes.
Im Normalfall nimmt RawTherapee den Raw-Dateinamen, wirft die
Dateierweierung weg und hängt statt dessen die Erweiterung des
Zielformats an. Aus "Bild1.RAW" wird zum Beispiel "Bild1.jpg".

Dateien überschreiben geht schnell. Nutze deshalb vorzugsweise die
Option "Suffix anfügen, falls unter dem Namen bereits eine Datei
exisiert". Speicherst du nun das oben genannte Bild noch einmal, wird
die erste Variante nicht überschrieben, sondern ein Bild "Bild1-1.jpg"
erzeugt. RawTherapee zählt einfach hoch. Das Gleiche passiert, wenn du
das gleiche Raw mehrfach, z.B. mit unterschiedlichen Einstellungen, in
die \[\[The_Batch_Queue/de\|Warteschlange\] legst.

## Option *Verarbeitungsparameter mit dem Bild speichern*

Wenn du ein schon mal früher entwickeltes Foto noch einmal überarbeiten
willst, vielleicht für einen Posterdruck oder eine andere Auflösung im
Web, könnte es sein, dass das Bearbeitungsprofil, das dem Raw als
Sidecar-File beiligt, nicht mehr den Zustand hat, wie zum damaligen
Export des bereits entwickelten Fotos. Die Regel ist sowas sogar, wenn
du häufig von einer Aufnahme immer gleich mehrere Auflösungen
speicherst. Oder verschiedene Beschnitte. Das Sidecar-File steht dann
auf dem Stand der letzten Bearbeitung. Willst du aber ein bereits
entwickeltes Bild genau vom Zustand der Entwicklung aus noch einmal
bearbeiten, ist es eine feine Sache, wenn es zu dem Stand, wo du es
erzeugt hast, ein Bearbeitungsprofil gibt.

Wenn du die Bilder grundsätzlich mit dieser Option speicherst, bekommt
auch dein gespeichertes JPEG oder TIF oder PNG ein Sidecarfile mit.
Nämlich mit dem Stand zum Zeitpunkt der Entwicklung. Dann besitzt du
immer ein Parametersetting, mit dem du ganz genau dieses Bild noch
einmal aus dem Raw erzeugen kannst. Unabhängig von zwischenzeitlichen
Manipulationen am Bildverarbeitungsprofil, das dem Raw von RawTherapee
automatisch beigelegt wird.

## Eigenheiten der unterschiedlichen Bildformate

Ohne hier detailliert auf die Formate einzugehen, ein paar Stichpunkte,
die Du beachten kannst, je nach Weiterverwendung:

- JPEG ist grundsätzlich komprimiert. Ab 8x% ist die Qualtiät schon sehr
  akzeptabel. Geeignet für's Web auf alle Fälle. Mit 9x% ist die Qualtät
  exzellent. Helligkeitsmodulationen werden sehr gut aufgelöst.
  Allerdings ist die Detaillierung in den Farben immer noch begrenzt.
  Meist stört das nicht. Benötigst du aber den Erhalt von farbigem
  Restrauschen, um in einfarbigen schwach strukturierten und
  großflächigen Bereichen Stufung zu vermeiden (Dithering), solltest du
  auf 100% Qualität gehen.
- Mit JPEG kann nur in einer Farbtiefe von 8 Bit pro Kanal gespeichert
  werden. (Im Gegensatz zu JPEG2000, das derzeit nicht unterstützt
  wird.)
- TIFF wird verlustfrei komprimiert, wenn du die Kompression aktivierst.
  Allerdings sind viele Programme nicht in der Lage, komprimierte TIFFs
  einzulesen. Teste das und speichere für maximale Kompatibilität im
  unkomprimierten Modus.
- PNG wird auch verlustfrei komprimiert. Hier gibt es in der Regel keine
  Kompatibilitätsprobleme. Und es wird auch von den meisten
  Softwareprodukten unterstützt.
- TIFF und PNG werden auch mit 16 Bit Farbtiefe unterstützt. Beide
  Formate eignen sich demnach zur verlustfreien Übertragung in andere
  Software zur weiteren Bearbeitung.
- Die Kompressionsraten bei TIFF und PNG sind in der Fotografie nicht
  besonders groß. Wenn dein Bild auf 75% schrumpft, ist das schon ein
  seltenes Ereignis. Normal sind 5...15% Schrumpfgrad.
- PNG unterstützt die Foto-Metadaten
  ([Exif](https://de.wikipedia.org/wiki/Exchangeable_Image_File_Format))
  nicht. So sehr geeignet das ist, um die Aufnahmebedingungen sicher zu
  anonymisieren, so ungeeignet ist das, wenn Werkzeuge oder du selbst
  später diese Daten verwenden möchten.
