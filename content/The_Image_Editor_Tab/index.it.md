---
title: The Image Editor Tab it
contributors:
  - Andrea.romagnoli
---

<figure>
<img src="/images/Rt-5-misty1.jpg" title="Rt-5-misty1.jpg" />
<figcaption>Rt-5-misty1.jpg</figcaption>
</figure>

La scheda Editor Immagine serve per modificare le tue foto.
Nell'impostazione predefinita, RawTherapee è in modalità "Modalita
Scheda Singola, Schede Verticali" (SETM) che è più efficiente per la
memoria e consente di utilizzare la *Sequenza* (descritta di seguito).
Puoi passare a *Modalità a Schede Multiple*(METM) con l'opzione
*Preferenze\> Generale\> Disposizione*, tuttavia ogni scheda Editor
richiede una quantità specifica di RAM rispetto alla dimensione
dell'immagine e gli strumenti utilizzati, e anche la *Sequenza* è
nascosta in questa modalità, quindi ti consigliamo di iniziare a provare
la SETM.

## Il pannello di anteprima

Il pannello centrale contiene un'anteprima della tua foto. Questa
anteprima viene generata dai dati raw effettivi elaborandola in base
alle impostazioni impostate manualmente o quelle memorizzate nel file
[profilo di
sviluppo](Sidecar_Files_-_Processing_Profiles_/it.md) utilizzato
durante l'apertura della foto, come specificato in "*Preferenze\>
Elaborazione di immagini\> Profilo di elaborazione predefinito*".
L'anteprima mostrerà l'effetto di tutte le regolazioni fatte. Tieni
presente che gli effetti di alcuni strumenti sono solo visibili quando
si è ingranditi fino a 1:1 (100%) o più. Questi strumenti sono
contrassegnati nell'interfaccia con un'icona "1:1"
![Image:zoom-100-identifier.png](zoom-100-identifier.png "Image:zoom-100-identifier.png")
accanto al nome dell'utensile.

L'immagine visualizzata nell'anteprima viene prelevata dallo spazio
colore del profilo di lavoro e convertito nello spazio colore del
profilo del monitor, se viene caricato un profilo di monitor o in sRGB
se non lo è. Non tiene conto del "[Profilo di
Uscita](Color_Management/it#Output_Profile.md)" dello strumento
"[Gestione del Colore](Color_Management/it.md)".

### Eek! La mia foto raw sembra diversa rispetto alla fotocamera JPEG

Dopo aver aperto una foto raws i noterà che sembra diversa, spesso
peggio - più scura, meno nitida, più opaca, mancante di contrasto, più
rumorosa - rispetto all'immagine JPEG della tua fotocamera o della
stessa foto raw se viene visualizzata in un altro software. Che cosa dà?
Streghe, alieni, opossum o è voluto?

Ci sono tre cose che devi sapere prima per capire cosa sta succedendo:

1.  La fotocamera non ti mostra i dati veri e propri quando si scatta le
    foto raw. Processa l'immagine raw in molti modi prima di presentarvi
    l'istogramma e l'anteprima sul display digitale della fotocamera.
    Anche se impostate tutte le funzioni di elaborazione, il firmware
    della tua fotocamera consente di modificare le posizioni "0"
    neutrali, ciò che vedete non è ancora un'immagine non elaborata.
    Esattamente ciò che viene applicato dipende dalle scelte effettuate
    dagli ingegneri e dalla gestione della tua macchina fotografica, ma
    di solito questa include una curva personalizzata del tono,
    l'aumento della saturazione, la risoluzione e la riduzione del
    rumore. Alcune fotocamere, in particolare quelli a basso livello e
    [Micro Four Thirds
    system](http://en.wikipedia.org/wiki/Micro_Four_Thirds_system),
    possono anche applicare la correzione della distorsione
    dell'obiettivo non solo per correggere la distorsione [barrel and
    pincushion
    distortion](http://en.wikipedia.org/wiki/Distortion_(optics)#Radial_distortion)
    ma anche per nascondere la vignettatura
    [vignetting](http://en.wikipedia.org/wiki/Vignetting). La maggior
    parte delle fotocamere sottoespone ogni foto scattata da -0,3EV a
    -1,3EV o più, per evitare di bruciare le alte luci. Quando la
    fotocamera (o altro software) elabora il file raw, aumenta la
    compensazione dell'esposizione della stessa quantità, rendendo la
    luminosità corretta cercando così di recuperare le alte luci.
    RawTherapee mostra i veri dati raw e questo spiega come mai le tue
    foto appaiono scure, quindi dipende da voi se applicate l'aumento
    dell'esposizione desiderato, utilizzando il cursore Compensazione
    dell'esposizione o una delle diverse curve di tono . L'aumento della
    compensazione dell'esposizione rende il rumore più evidente
    indipendentemente dal fatto che sia la tua macchina fotografica o
    RawTherapee che lo fa, ma diverso da questo \[RawTherapee non
    "aggiunge rumore"\] Molte fotocamere applicano la riduzione del
    rumore ai JPEG (senza ammetterlo) per abbassare il livello di
    rumorosità dopo aver aumentato la compensazione dell'esposizione,
    quindi si dovrebbe aspettarsi che vi sia una differenza tra
    l'immagine JPEG e l'immagine RawTherapee se la riduzione del rumore
    in RawTherapee non è abilitata.
2.  Ogni file raw DSLR contiene un'immagine JPEG elaborata. La maggior
    parte dei file raw contengono un'immagine JPEG della stessa
    risoluzione completa che la fotocamera può sparare e alcuni file raw
    contengono ben tre immagini JPEG che si differenziano solo in
    risoluzione. Quando si apre i file raw in altri software, ciò che di
    solito si vede è "*non*" i dati raw, ma l'immagine JPEG incorporata
    e elaborata. Esempi di software che sono incapaci o che nelle loro
    impostazioni predefinite non ti mostrano i dati reali:
    [IrfanView](http://en.wikipedia.org/wiki/IrfanView), [/ wiki /
    XnView XnView](http://en.wikipedia.org),
    [Gwenview](http://it.wikipedia.org/wiki/Gwenview),
    [Geeqie](http://it.wikipedia.org/wiki/Geeqie), \[http:
    //en.wikipedia. org / wiki / Eye_of_GNOME Occhio di GNOME\],
    [F-Spot](http://it.wikipedia.org/wiki/F-Spot),
    [Shotwell](http://it.wikipedia.org/wiki/Shotwell_(software)) ,
    [gThumb](http://en.wikipedia.org/wiki/GThumb), ecc Vale la pena
    ricordare a questo punto che se si scatta in modalità "RAW + JPEG",
    in realtà stai perdendo spazio su disco e non guadagni nulla in
    quanto i file raw contengono già i file JPEG incorporati che è
    possibile visualizzare utilizzando i programmi elencati. Il JPEG
    incorporato può differire da quello "esterno" salvato utilizzando la
    modalità "RAW + JPEG" in compressione.
3.  La maggior parte dei programmi di sviluppo raw (programmi che
    leggono i veri dati raw anziché la semplice lettura del JPEG
    incorporato) applicano una elaborazione all'immagine, ad esempio una
    curva di tonalità base, anche alle impostazioni più neutrali,
    rendendo così impossibile per gli utenti di vedere il contenuto
    reale e incontaminato delle loro foto raw. Adobe Lightroom è un
    esempio. Confrontando la vera immagine neutra di RawTherapee con una
    quasi-neutrale di questi altri programmi si evincono le differenze.

RawTherapee, d'altra parte, è progettato per mostrare l'immagine reale
reale nell'anteprima principale, lasciando il modo in cui si desidera
che questi dati vengono elaborati. Quando si utilizza il profilo di
elaborazione "Neutrale" si vedrà l'immagine demo-tagliata con il
bilanciamento del bianco della fotocamera nello spazio colore di lavoro
senza altre modifiche. Risulta possibile vedere anche l'immagine non
domosaicizzata impostando l'opzione
[demosaicizzazione](demosaicing/it.md) su "Nessuno". Per offrire
un punto di partenza esteticamente più piacevole, è stata aggiunta una
collezione di profili di elaborazione con RawTherapee. Dopo
l'installazione di RawTherapee, il profilo predefinito per
l'elaborazione delle foto raw è chiamato in modo omonimo "Default".
Consigliamo anche i profili "Default ISO Medium" e "Default ISO High",
progettati per fornire un buon punto di partenza per immagini
rispettivamente di rumore medio e rumoroso.

Nessuno dei profili inseriti (almeno nessuno di quelli spediti in
RawTherapee 5.0) è stato progettato per imitare l'aspetto della tua
fotocamera. Perchè no? Ogni fotocamera è diversa. La qualità
dell'immagine della mia fotocamera a ISO1600 potrebbe essere più
rumorosa di quella della tua fotocamera. La risposta della mia
fotocamera ai colori è diversa da quella della tua. Anche la stessa
fotocamera può comportarsi in modo diverso in varie impostazioni. Per
fornire tali profili, avremmo bisogno di accedere a file raw per ogni
modello di fotocamera supportato, spesso più file raw in varie modalità
di scatto per una singola fotocamera e innumerevoli
[person-hours](http://en.wikipedia.org/wiki/Man-hour). Questo può essere
possibile come uno sforzo di comunità, ma non è un lavoro per una
piccola squadra. Anche se fosse, quale sarebbe lo scopo di RawTherapee
se finisse per riprodurre l'aspetto JPEG della fotocamera?

È molto più ragionevole imparare a utilizzare gli strumenti potenti che
RawTherapee offre per ottenere il massimo dal tuo raw, per superare
l'aspetto della fotocamera.

A partire da settembre 2015 stiamo iniziando a trasportare i profili di
input DCP fatti utilizzando
[DCamProf](http://www.ludd.ltu.se/~torger/dcamprof.html) che includono
una [/~torger/dcamprof.html#dcp_tone curva di tonalità
opzionale](http://www.ludd.ltu.se). Questa curva è modellata dopo la
curva di pellicola predefinita di Adobe Camera Raw e rende un risultato
simile al tuo "look fotocamera". Il motivo per cui includiamo la curva
nei nuovi profili DCP è perché fa un buon punto di partenza vibrante (al
contrario dell'aspetto piatto dell'utilizzo del profilo di elaborazione
"Neutral") senza dover utilizzare [Livelli
automatici](Exposure/it#Auto_Levels.md) e senza toccare nessuno
degli altri strumenti, ed è completamente opzionale. Leggere l'articolo
su [profili di ingresso](Color_Management/it#Input_Profile.md).
Se è presente un DCP per il tuo modello di fotocamera che include la
curva di tono, la casella di controllo "curva di tono" in *Gestione del
colore\> Profilo di input\> DCP* sarà cliccabile. Applicare il profilo
di elaborazione (Neutro) disattiverà la curva di tono. Mentre il profilo
di colore dell'ingresso viene applicato nelle prime fasi della
[toolchain pipeline](Toolchain_Pipeline/it.md), la curva del
tono DCP viene applicata in un secondo momento dopo lo strumento
Esposizione.

È possibile creare un profilo di elaborazione idealmente adattato alla
combinazione di fotocamere e lenti e impostare RawTherapee per
utilizzarlo per impostazione predefinita sulle tue foto raw. Vedere la
sezione [Creare profilo di sviluppo per uso
generale](Creating_processing_profiles_for_general_use/it.md)
per apprendere come.

### Modalità Anteprima

Oltre all'originale anteprima, RawTherapee supporta numerose altre
modalità di anteprima per aiutarti a modificare le tue foto. Le modalità
di anteprima sono controllate tramite i pulsanti nella barra degli
strumenti *Editor* o tramite [scorciatoie da
tastiera](Keyboard_Shortcuts_/it.md). Può essere attivata una
sola modalità di anteprima alla volta.

<div style="float: right">

<table>
<caption>align="bottom" | * The preview is returned to normal by
deselecting any other mode.</caption>
<thead>
<tr class="header">
<th><p>Preview Mode</p></th>
<th><p>Shortcut</p></th>
<th><p>Button</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="padding:10px;"><p>Regular*</p></td>
<td></td>
<td><figure>
<img src="/images/preview_mode_1_regular.png"
title="Image:preview mode 1 regular.png" />
<figcaption>Image:preview mode 1 regular.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Red channel</p></td>
<td style="text-align: center;"><p>r</p></td>
<td><figure>
<img src="/images/preview_mode_2_red.png"
title="Image:preview mode 2 red.png" />
<figcaption>Image:preview mode 2 red.png</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td style="padding:10px;"><p>Green channel</p></td>
<td style="text-align: center;"><p>g</p></td>
<td><figure>
<img src="/images/preview_mode_3_green.png"
title="Image:preview mode 3 green.png" />
<figcaption>Image:preview mode 3 green.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Blue channel</p></td>
<td style="text-align: center;"><p>b</p></td>
<td><figure>
<img src="/images/preview_mode_4_blue.png"
title="Image:preview mode 4 blue.png" />
<figcaption>Image:preview mode 4 blue.png</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td style="padding:10px;"><p>Luminance channel</p></td>
<td style="text-align: center;"><p>v</p></td>
<td><figure>
<img src="/images/preview_mode_5_luminance.png"
title="Image:preview mode 5 luminance.png" />
<figcaption>Image:preview mode 5 luminance.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td style="padding:10px;"><p>Focus Mask</p></td>
<td style="text-align: center;"><p>Shift+f</p></td>
<td><figure>
<img src="/images/preview_mode_6_focus.png"
title="Image:preview mode 6 focus.png" />
<figcaption>Image:preview mode 6 focus.png</figcaption>
</figure></td>
</tr>
</tbody>
</table>

align="bottom" \| \* The preview is returned to normal by deselecting
any other mode.

</div>

Sono supportati anche i seguenti modi anteprima:

- Red channel,
- Green channel,
- Blue channel,
- Luminosity, which is calculated as 0.299\*R + 0.587\*G + 0.114\*B,
- Focus mask, per vedere quale area risulta a fuoco

Image:Preview_1_regular.jpg\|Regular Image:Preview_2_red.jpg\|Red
Image:Preview_3_green.jpg\|Green Image:Preview_4_blue.jpg\|Blue
Image:Preview_5_luminosity.jpg\|Luminosity
Image:Preview_6_focus.jpg\|Focus Mask

#### Modalità di anteprima rossa, verde, blu e luminosità

Quando gli indicatori di ritaglio sono attivati ​​nei modi di anteprima
RGBL, le aree con ombreggiatura sono indicate in un colore blu e le alte
luci bruciate sono indicate in rosso. Come durante l'anteprima normale,
la luminosità delle alte luci bruciate è indicativa del grado di
bruciatura (clipping).

L'anteprima dei singoli canali può essere utile quando si modifica le
curve RGB, per previsualizzare la conversioen in bianco e nero
utilizzando il mixer di canali, per la valutazione del rumore
dell'immagine ecc. L'anteprima di luminosità è utile per visualizzare
immediatamente l'immagine in bianco e nero senza modificare i parametri
di sviluppo. per vedere quale canale è bruciatoi o per motivi estetici.

#### Maschera di messa a fuoco

![Maschera di messa a fuoco che evidenzia il piano a
fuoco](Preview_6_focus_2.jpg "Maschera di messa a fuoco che evidenzia il piano a fuoco")
La maschera di messa a fuoco è progettata per evidenziare le aree
dell'immagine messe a fuoco. Naturalmente, le aree focalizzate sono più
nitide, per cui le aree nitide vengono evidenziate. La maschera di messa
a fuoco è più accurata nelle immagini con una profondità di campo
ridotta, con bassa rumorosità e se riprese con focali lunghe. Per
migliorare l'accuratezza della rilevazione per immagini rumorose, si
valuta con uno zoom più piccolo, intorno al range di 10-30%. Si noti che
l'anteprima viene eseguita più lentamente quando la maschera di messa a
fuoco è abilitata.

L'implementazione attuale analizza l'immagine di anteprima che viene
ridimensionata dall'immagine originale. Questo processo di
ridimensionamento riduce il rumore ed è utile per identificare i
dettagli veramente più nitidi, piuttosto che il rumore stesso che può
anche contenere micro texture. Allo stesso tempo, il ridimensionamento
dell'immagine originale alle dimensioni di anteprima comprime i dettagli
di grandi dimensioni in una dimensione minore e può introdurre aliasing
artifacts, entrambi gli effetti possono portare a falsi positivi. È
possibile aumentare la tua fiducia guardando la maschera a vari livelli
di zoom. Non è sempre controprova, ma può essere utile in molti casi.

**Avviso** : Assicuratevi di duplicare le proprie immagini se decidete
di eliminarle in base alla maschera di messa a fuoco.

### Colore di sfondo dell'anteprima

Il colore di sfondo del pannello di anteprima che circonda l'area
dell'immagine può essere modificato per facilitare l'anteprima
dell'immagine durante la modifica e per visualizzare meglio la ritaglio
dell'immagine. Una pila verticale di tre bottoni sottili nella barra
degli strumenti Modalità di anteprima sopra il pannello di anteprima
dell'immagine consente di impostare il colore di sfondo dell'area
attorno all'anteprima della foto.

<div align="center">

<table>
<thead>
<tr class="header">
<th><p>Preview<br />
Background</p></th>
<th><p>Shortcut</p></th>
<th><p>Button</p></th>
<th><p>Preview Background<br />
and Crop Visualization</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Theme-based</p></td>
<td style="text-align: center;"><p>8</p></td>
<td><figure>
<img src="/images/Previewback_7_theme.png"
title="Image:Previewback_7_theme.png" />
<figcaption>Image:Previewback_7_theme.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_theme.png"
title="Previewback_flower_theme.png" width="180" />
<figcaption>Previewback_flower_theme.png</figcaption>
</figure></td>
<td><p>L'area ritagliata dell'immagine viene mascherata con un colore
tematico. La visibilità dell'area ritagliata si basa sul colore della
maschera e sulla trasparenza impostata "<em>Preferenze &gt; Tema
Predefinito &gt; Colore /trasparenza della maschera di
ritaglio</em>".</p></td>
</tr>
<tr class="even">
<td><p>Black</p></td>
<td style="text-align: center;"><p>9</p></td>
<td><figure>
<img src="/images/Previewback_8_black.png"
title="Image:Previewback_8_black.png" />
<figcaption>Image:Previewback_8_black.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_white.png"
title="Previewback_flower_white.png" />
<figcaption>Previewback_flower_white.png</figcaption>
</figure></td>
<td><p>L'area ritagliata dell'immagine viene mascherata con il
nero.</p></td>
</tr>
<tr class="odd">
<td><p>White</p></td>
<td style="text-align: center;"><p>0</p></td>
<td><figure>
<img src="/images/Previewback_9_white.png"
title="Image:Previewback_9_white.png" />
<figcaption>Image:Previewback_9_white.png</figcaption>
</figure></td>
<td><figure>
<img src="/images/Previewback_flower_black.png"
title="Previewback_flower_black.png" />
<figcaption>Previewback_flower_black.png</figcaption>
</figure></td>
<td><p>L'area ritagliata dell'immagine viene mascherata con il
bianco.</p></td>
</tr>
</tbody>
</table>

</div>

### Dettaglio finestra

Il pulsante "Nuova finestra di dettaglio"
![Image:new-detail-window.png](new-detail-window.png "Image:new-detail-window.png"),
situato sotto l'anteprima principale accanto ai pulsanti di zoom, apre
una nuova visualizzazione nell'anteprima principale di una dimensione
regolabile e con zoom regolabile. Ciò consente di lavorare sulla foto
zoomata durante l'esame di diverse aree di interesse con uno zoom del
100% (o ancora di più). Il vantaggio di utilizzare questa funzionalità è
particolarmente importante per gli utenti con macchine più lente,
sebbene non solo, poiché l'anteprima principale zoomata richiede un
minor tempo di aggiornamento rispetto a quanto lo si desidera per lo
zoom al 100% perché lo zoom a livelli inferiori al 100% esclude alcuni
strumenti lenti, come la riduzione del rumore, mentre le piccole
finestre dettagliate ingrandite al 100% includono tutti gli strumenti ma
sono veloci da aggiornare date le loro piccola dimensione. Ciò consente
di utilizzare l'anteprima principale per le modifiche dell'esposizione
generale in cui è necessario vedere l'intera immagine e una o più
finestre di dettaglio per ottenere la risoluzione e/o la riduzione del
rumore corretti.

### Visualizzazione del ritardo di aggiornamento

La modifica dei parametri di uno strumento invia un segnale per
l'aggiornamento dell'immagine di anteprima. Immagina cosa succederebbe
se non ci fosse un "periodo di ritardo" e si trascina, ad esempio, il
cursore di esposizione da 0,00 a +0,60. Sarà inviato un segnale per
aggiornare l'anteprima di ogni singola modifica di tale valore - per
+0.01, +0.02, ... +0.59, +0.60. L'aggiornamento dell'anteprima di 60
volte sarebbe completamente inutile e in realtà richiederebbe più tempo
di quanto ti serve per spostare il cursore. Ciò è particolarmente vero
per gli strumenti più complicati, come la riduzione del rumore, in cui
un aggiornamento di anteprima può richiedere anche un secondo (a seconda
della CPU e della dimensione dell'anteprima). La soluzione è introdurre
un ritardo molto breve durante il quale le modifiche dei parametri
vengono ignorate e il segnale per aggiornare l'anteprima viene inviato
solo dopo che non è stata registrata qualche modifica dei parametri dopo
questo tempo.

Abbiamo introdotto due di questi parametri:

AdjusterMinDelay  
Valore predefinito = 100ms.

Questo è il tempo minimo da attendere prima che l'anteprima venga
aggiornata.

AdjusterMaxDelay  
Valore predefinito = 200ms.

Questo è il tempo massimo da attendere prima che l'anteprima venga
aggiornata. Se continui a modificare un parametro, RawTherapee non
aspetterà più di questo periodo di tempo breve prima di attivare un
aggiornamento di anteprima. Mentre il ritardo minimo è previsto per
impedire il sovraccarico della CPU con aggiornamenti inutili
dell'anteprima, questo ritardo è quello di garantire che si può vedere
cosa succede all'immagine mentre modifichi lentamente un determinato
parametro.

È possibile regolare entrambi questi valori nel file delle opzioni nella
[config folder](File_Paths/it.md).

## Il pannello sinistro

A sinistra è un pannello che facoltativamente mostra l'istogramma
principale ("" "Preferenze\> Generale\> Layout\> Istogramma nel pannello
di sinistra" ") e mostra sempre i" 'Navigator' ',' 'History' 'e'
'Snapshots ''. Puoi nascondere questo pannello usando l'icona ![Hide
left panel icon](panel-to-left.png/it "Hide left panel icon") o la
relativa [scorciatoie da tastiera](Keyboard_Shortcuts/it.md).

### Principale istogramma

![](Rt_histogram_crop_scale-off.png "Rt_histogram_crop_scale-off.png")
![](Rt_histogram_crop_scale-on.png "Rt_histogram_crop_scale-on.png")
![](Rt_histogram_raw.png "Rt_histogram_raw.png")
![](Rt_histogram_rgbindicator.png "Rt_histogram_rgbindicator.png")

L'istogramma principale può mostrare gli istogrammi della
![](histRed.png/it "histRed.png/it"), verde
![](histGreen.png/it "histGreen.png/it"), blu
![](histBlue.png/it "histBlue.png/it"), CIELab Luminance
![](histValue.png/it "histValue.png/it") e
[Chromaticity](http://en.wikipedia.org/wiki/Cromatica)
![](histChro.png/it "histChro.png/it") i canali della foto come sarebbe
sembrato se l'hai salvato. Utilizza queste informazioni per impedire il
taglio del risultato finale. Se l'immagine grezzo non ha un ritaglio ma
il risultato finale è possibile identificare facilmente i canali
necessari per eseguire la regolazione e adottare le misure necessarie
per prevenirlo se non è indesiderabile.

Può mostrare l'istogramma dei dati grezzi
![](histRaw.png/it "histRaw.png/it") prima che vengano applicate tutte
le trasformazioni come demosaicing. Utilizza queste informazioni per
vedere se c'è un ritaglio nell'immagine grezzo. I dati grezzi ritagliati
non possono essere recuperati. Alcuni highlight evidenziati possono
essere [](Exposure/it#Highlight_Reconstruction "wikilink").

Quando esiste una zona sproporzionatamente luminosa rispetto al resto
dell'immagine, questo verrà visualizzato come un picco nell'istogramma.
Se vuoi mostrare questo su un istogramma lineare, non scalato nell'asse
y, sacrificerai vedendo i livelli bassi per mostrare completamente il
picco. È possibile cambiare la scala dell'istogramma nell'asse y
![](histFull.png/it "histFull.png/it") per contribuire a far fronte a
questo, quindi i valori elevati verranno ridimensionati in modo da poter
vedere meglio il resto dell'istogramma.

È possibile mostrare o nascondere la barra di indicazione RGB
![](histBar.png/it "histBar.png/it"), che si trova sotto l'istogramma e
mostra l'esatto posto dell'istogramma dei valori R, G, B o L del pixel
che il cursore è attualmente si è spostato nell'anteprima principale.

L'istogramma può essere spostato nel pannello sinistro / destro di ""
"Preferenze\> Generale\> Layout\> Istogramma nel pannello di sinistra"
".

I valori che mostrano l'istogramma principale e il pannello Navigatore
sono quelli del profilo di lavoro o del profilo di uscita corretto da
gamma. Puoi scegliere quello che preferisci in '' '[Preferences \>
General](Preferences/it#General_Tab.md)\> Utilizza il profilo di
lavoro per l'istogramma principale e Navigator' '".

### Navigatore

Il pannello *Navigatore* mostra una miniatura dell'immagine attualmente
aperta e dei valori RGB, HSV e Lab del pixel sul quale il cursore è in
corso.

I valori che mostrano l'istogramma principale e il pannello Navigatore
sono quelli del profilo di lavoro o del profilo di uscita corretto da
gamma. Puoi scegliere quello che preferisci in '' '[Preferences \>
General](Preferences/it#General_Tab.md)\> Utilizza il profilo di
lavoro per l'istogramma principale e Navigator' '".

Facendo clic sui valori nel Navigatore è possibile passare tra questi
tre formati:

- \[0-255\]
- \[0-1\]
- \[%\]

RawTherapee 5.1 in avanti può mostrare i valori reali di photosite
grezzi. Per vederli, impostare il Navigatore per utilizzare l'intervallo
\[0-255\], applicare il profilo [Neutri](Neutral/it.md) [profilo
di sviluppo](Sidecar_Files_-_Processing_Profiles/it.md), quindi
impostare il metodo [Demosaicizzazione](Demosaicing/it.md) su
"Nessuno". Il Navigatore mostrerà i valori reali di photosite privi dopo
la sottrazione di livello nero nell'ambito dei dati grezzi originali.

<div style = "clear: entrambi">

\</ div\>

### storia

Sotto il *Navigator* è il pannello *Storia*. Durante la modifica di una
foto, tutte le tue azioni vengono registrate in questo pannello
*Storia*. Facendo clic sulle diverse voci, puoi passare avanti e
indietro attraverso le diverse fasi del tuo lavoro.

### Snapshots

Sotto il pannello *Storia* è un pannello chiamato *Snapshots*. Il suo
uso è quello di salvare un'immagine istantanea della foto con tutte le
regolazioni fino a quel momento nel tempo e quindi continuare a
modificare ulteriormente la tua foto per dare un aspetto diverso,
salvando nuove istantanee in ogni momento in cui ritenete di avere ha
raggiunto una versione della tua foto vale la pena di risparmiare. Una
volta che hai due o più istantanee, puoi semplicemente cliccare su di
loro per scorrere le varie versioni e attenersi a quello che ti piace di
più. In futuro, le istantanee verranno salvate nel file sidecar PP3. Per
ora, la storia e le istantanee vengono perse quando si carica una nuova
foto nell'Editor di immagini '' o chiudi RawTherapee.

## Il pannello destro

A destra è un pannello che mostra in opzione l'istogramma principale e
il selettore "'Profili di elaborazione' '(' *Preferenze\> Generale\>
Layout\> Istogramma nel pannello di sinistra*) e mostra sempre
[Strumenti](Toolbox/it.md). Puoi nascondere questo pannello
usando l'icona ![Hide right panel
icon](panel-to-right.png/it "Hide right panel icon") o la relativa
[scorciatoie da tastiera](Keyboard_Shortcuts/it.md).

### Selezione del profilo di elaborazione

L'elenco a discesa *Profili di elaborazione* consente di applicare in
bundle o personalizzate [profilo di
sviluppo](Sidecar_Files_-_Processing_Profiles_/it.md). Vedere
l'articolo [Percorsi File](File_Paths/it.md) per informazioni su
dove questi profili di elaborazione risiedono nel sistema.

Prestare attenzione al pulsante "*Modalità di riempimento del profilo di
elaborazione*"!

Modo "Riempimento" [image:Profile-filled.png](image:Profile-filled.png.md)  
Quando il pulsante è attivato e si apre un profilo parziale, i valori
mancanti saranno sostituiti con i valori predefiniti di RawTherapee.

Ad esempio, se si applica un profilo parziale che contiene solo
impostazioni di affilatura, tutti gli altri strumenti (come
l'esposizione, la mappatura del suono, la riduzione del rumore, la
ridimensionamento, ecc.) Verranno visualizzati nelle posizioni
predefinite.

Modalità "Preservare" [image:Profile-partial.png](image:Profile-partial.png.md)  
Se il pulsante è disattivato e si apre un profilo parziale, verranno
applicati solo i valori nel profilo e quelli mancanti rimangono
invariati.

Ad esempio se si applica un profilo parziale che contiene solo
impostazioni di affilatura, vengono applicate solo quelle impostazioni
di affilatura e gli altri strumenti rimangono invariati.

Lo stato di questo pulsante non farà differenza se si applica un profilo
completo, ma la maggior parte dei profili in bundle con RawTherapee sono
parziali (per buona ragione).

### Toolbox

La *Toolbox*, nel riquadro destro, contiene tutti gli strumenti
utilizzati per modificare le tue foto. Ogni strumento ha un proprio
articolo RawPedia.

## Modifiche modulo editor

RawTherapee consente di lavorare su foto in due modi:

- *Single Editor Mod Tab* (SETM), dove si lavora solo su una foto alla
  volta e ogni foto viene aperta nella stessa scheda *Editor*. Esiste un
  pannello orizzontale denominato
  *[Filmstrip](The_Image_Editor_Tab/it#The_Filmstrip.md)* nella
  parte superiore del
  *[editor](The_Image_Editor_Tab/it#The_Filmstrip.md)* che
  mostra le altre foto in quella cartella per un facile accesso. Nella
  barra degli strumenti inferiore (e
  ![<File:Nav-prev.png>](Nav-prev.png "File:Nav-prev.png")
  ![<File:Nav-next.png>](Nav-next.png "File:Nav-next.png")\] per passare
  all'immagine precedente / successiva.
- *Multiple Module Module Editor* (METM), dove ogni foto viene aperta
  nel proprio
  *[editor](The_Image_Editor_Tab/it#The_Filmstrip.md)*. Il
  *[Filmstrip](The_Image_Editor_Tab/it#The_Filmstrip.md)* è
  nascosto in questa modalità e non ci sono pulsanti precedenti /
  successivi. Avere più foto aperte allo stesso tempo richiede più RAM.

Prova entrambe le modalità e vedi quale ti si adatta meglio. Per fare
ciò, clicca sull'icona *Preferenze* ![Preferences
icon](Gtk-preferences.png/it "Preferences icon") nell'angolo in basso a
sinistra o in alto a destra della finestra RT, scegli "*Generale\>
Layout '* e impostare *Editor Layout* nella tua scelta preferita.

Utilizza questa finestra *Preferenze* per selezionare una lingua diversa
per l'interfaccia utente, per scegliere un diverso tema a colori,
modificare la dimensione del carattere, ecc.

È anche possibile avviare RawTherapee in modalità No-File-Browser (senza
la scheda 'File Browser') specificando RawTherapee per aprire
un'immagine dal browser del file del sistema operativo (in altre parole,
fare clic con il pulsante destro del mouse su una foto e seleziona
"*Open With\> RawTherapee*") oppure usa il nome del file immagine come
argomento quando inizia RawTherapee dalla riga di comando (<code>
rawtherapee /path/to/some/photo.raw \</ code\>) . Questa modalità è
stata introdotta per le persone con scarsa RAM in quanto non avendo una
scheda *File Browser* significa che RawTherapee utilizza un po 'meno
memoria, ma in pratica la quantità di memoria salvata è scarsa e il
costo di usabilità supera il piccolo vantaggio, quindi è probabilmente
sarà rimosso in futuro (vedi [numero
2254](https://code.google.com/p/rawtherapee/issues/detail?id=2254)).

## La Filmstrip

![](Rt_filmstrip_21_toolbar-visible.jpg "Rt_filmstrip_21_toolbar-visible.jpg")
![](Rt_filmstrip_21_toolbar-hidden.jpg "Rt_filmstrip_21_toolbar-hidden.jpg")

Se si utilizza la modalità 'Single Editor Tab Mode' (*'Preferenze\>
Generale\> Layout' '), è possibile visualizzare un pannello orizzontale
sopra l'anteprima, chiamato' 'Filmstrip' '. Contiene miniature di tutte
le immagini nell'album attualmente aperto e viene sincronizzato con
l'immagine attualmente aperta in modo da poter usare [scorciatoie da
tastiera](Keyboard_Shortcuts/it.md) o precedente ![Open previous
image icon](nav-prev.png/it "Open previous image icon") e successive
![Open next image icon](nav-next.png/it "Open next image icon") pulsanti
immagine per aprire l'immagine precedente / successiva senza necessità
di tornare alla* [Navigatoreile](The_File_Browser_Tab/it.md)
Browser File \| File Browser\] '' tab.

A partire da RawTherapee versione 4.2.10, è possibile nascondere la
barra degli strumenti di Filmstrip per salvare lo spazio dello schermo.
Ci sono due modi per farlo: un solo modo consente di attivare /
disattivare la barra degli strumenti senza ridimensionare la pellicola
alla nuova altezza e, altrimenti, lo stesso ma ridimensiona
automaticamente l'altezza della pellicola. Entrambi vengono richiamati
solo tramite [scorciatoie da
tastiera](Keyboard_Shortcuts/it.md). Come ridimensionare
l'altezza della pellicola innescherà un aggiornamento dell'anteprima
dell'immagine e questo potrebbe richiedere un po 'se utilizza attrezzi
affamati da CPU come la riduzione del rumore mentre è ingrandita al
100%, la modalità che non viene ridimensionata è stata implementata per
utenti con macchine lente . Gli utenti con macchine veloci troveranno la
modalità di ridimensionamento più utile.

  
== Monitor profilo e Soft-Proofing == I widget sotto l'anteprima
principale in RawTherapee 5 consentono di applicare un profilo di colore
del monitor all'immagine di anteprima. Ciò consente agli utenti che
hanno calibrato e profilato i loro monitor per ottenere un'anteprima
immediata e precisa del loro lavoro, sia che siate a sRGB o che lavorano
in una vasta gamma. Nota: gli utenti di OS X sono limitati a sRGB e non
ottengono un'anteprima precisa altrimenti ([vedi
discussione](https://discuss.pixls.us/t/wide-gamut-preview-in-os-x/2481)),
mentre gli utenti di Linux e Windows avranno un'accuratezza corretta a
larga scala.

Vai a Preferenze\> [Gestione del
Colore](Preferences/it#Color_Management_Tab.md) e indica la
"Directory contenente i profili di colore" nella cartella in cui è stato
salvato il monitor e il profilo ICC della stampante. Riavviate
RawTherapee per avere effetto le modifiche. Ora potrai selezionare il
profilo di colore del monitor nella combinazione di sotto l'anteprima.
Utilizza l'intenzione di rendering "Colorimetric Relative" a meno che tu
non abbia una buona ragione altrimenti.

Può anche consentire l'impermeabilizzazione dell'anteprima. Ciò mostrerà
ciò che apparirà la tua immagine una volta che viene trasformata dal
profilo della stampante impostato in Preferenze\> [Gestione del
Colore](Preferences/it#Color_Management_Tab.md). Se si desidera
regolare un'immagine per la stampa e si dispone di un profilo ICC per la
combinazione di carta stampante, è possibile impostare come profilo di
output abilitare "Black point compensation" in Preferenze in modo che il
più nero nero della tua immagine corrisponda al più nero nero la
combinazione di stampanti-carta è in grado di riprodurre, quindi
abilitare la protezione morbida. Vedrai quale sia la tua immagine, se lo
stamperai. Ciò consente di eseguire delle regolazioni e di ottenere
un'anteprima istantanea del risultato, risparmiando tempo e inchiostro
sulle stampe di prova.

L'icona con il segno di esclamazione accanto al pulsante soft-proof
indurirà aree che non possono essere riprodotte dalla stampante, vale a
dire aree in cui si perdono i dettagli.

È necessario disporre di un monitor calibrato e profilato in modo che
l'anteprima di prova non sia corretta.

Le voci visualizzate nella combinazione di profilo del monitor (sotto
l'anteprima principale) e nel combinatore di comandi della stampante (in
Preferenze\> [Gestione del
Colore](Preferences/it#Color_Management_Tab.md) sono i file ICC
situati in una cartella in cui è possibile puntare RawTherapee per
andare a "[Preferenze](Preferences/it.md)\> [Gestione del
Colore](Preferences/it#Color_Management_Tab.md)\> Directory
contenente profili di colore".
