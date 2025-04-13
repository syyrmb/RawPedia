---
title: Saving it
contributors:
  - Andrea.romagnoli
---

Il file raw originale non verrà mai modificato da RawTherapee.

Ci sono diversi modi per salvare un'immagine dall' [Editor
Immagine](The_Image_Editor_Tab.md):

- ![Image:
  gtk-save-large.png](_gtk-save-large.png "Image: gtk-save-large.png")
  Salva immediatamente dalla scheda Editor,
- ![Image: processing.png](_processing.png "Image: processing.png")
  Salva tramite [Batch Queue](the_batch_queue),
- ![File: Image-editor.png](_Image-editor.png "File: Image-editor.png")
  "[Modifica immagine corrente in Editor
  esterno](Modifica_immagine_corrente_in_Editor_esterno.md)"
  (descritto nel proprio articolo).

## Salva immediatamente

Nella scheda Editor, fai clic sull'icona del piccolo disco rigido
![Image:
gtk-save-large.png](_gtk-save-large.png "Image: gtk-save-large.png") in
basso a sinistra dell'immagine di anteprima o premi il collegamento
**Ctrl + s** per "*Salvare immediatamente*". Questo funziona come una
finestra di dialogo "Salva con nome" standard. È possibile selezionare
il nome e la posizione del file di output (RawTherapee aggiunge
automaticamente l'estensione in base al formato scelto), scegliere un
formato JPEG, TIFF o PNG ([8 bit e 16 bit](8_bit_e_16_bit)
per TIFF e PNG) , impostare il rapporto di compressione, scegliere se si
desidera che il profilo di elaborazione sia salvato accanto all'immagine
di output ecc. L'ultima opzione consente di scegliere se si desidera
"*Salva immediatamente*" o "*Metti in testa/coda alla coda di
elaborazione*". Una scorciatoia per *OK* è **Ctrl + Enter**. Se si
sceglie "*Salva immediatamente*", RawTherapee sarà impegnato a salvare
la tua foto non appena si fa clic su "*OK*", quindi sarà meno sensibile
a qualsiasi regolazione che si potrebbe provare a fare mentre è
occupato, e impiegherà anche più tempo per aprire altre immagini finché
è occupato a salvare questo. Si consiglia generalmente di utilizzare la
coda se si lavora su più di un'immagine.

## Metti in testa / coda della coda di elaborazione

Se si fa clic sull'icona degli ingranaggi ![Image:
processing.png](_processing.png "Image: processing.png") o nella
finestra "*Salva*" scegli "*Mettere a testa/coda della coda di
elaborazione*", l'immagine verrà conservata in una coda di file da
elaborare, quindi RawTherapee sfrutterà al meglio la tua CPU e risulterà
più sensibile mentre si aggiusteranno altre foto. Una volta che finito
di aggiungere le immagini alla coda, mentre RawTherapee inizia
l'elaborazione della coda è possiile andare a godersi un buon tè. Il
vantaggio di utilizzare la coda usando la finestra "*Salva*" è che puoi
modificare individualmente il formato del file, il nome e la
destinazione di ciascuna immagine, mentre mettere le immagini nella coda
senza utilizzare il comando "*Salva*" utilizzerà le impostazioni dalla
scheda [Batch Queue](the_batch_queue/it)".

## Naming

Se il file originale raw è stato chiamato "photo_1000.raw", il nome del
file elaborato predefinito sarà "photo_1000.jpg" (o .tif o .png). Esiste
un'opzione nella finestra "*Salva immagine corrente*":"*Aggiunge
automaticamente un suffisso se il file esiste già*". Quando selezionato,
puoi creare versioni diverse di un raw, che verranno salvate come
"photo_1000.jpg", "photo_1000-1.jpg", "photo_1000-2.jpg", ecc. Lo stesso
vale quando si inviano versioni diverse della stessa immagine alla [coda
di sviluppo](The_Batch_Queue/it.md).
