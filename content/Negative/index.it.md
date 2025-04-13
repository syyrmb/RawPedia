---
title: Negative it
contributors:
  - Andrea.romagnoli
---

I negativi sono immagini con luminosità e colori invertiti, come quelli
prodotti dalle fotocamere a pellicola. RawTherapee non ha ancora una
soluzione impeccabile ad un solo clic per gestirli, quindi questa pagina
serve a informarti sulle possibili soluzioni di soluzione alternative:

1.  Inverti la diagonale della [curva di
    tono](Exposure_#_Tone_Curves.md) sia nello strumento
    Esposizione, sia in tutte le curve dello strumento [Curve
    RGB](RGB_Curves.md). Nello strumento Gestione colori
    selezionare "[Nessun
    profilo](Color_Management_#_No_Profile.md)" come profilo di
    input. Purtropo con questo metodo ci sono spostamenti tonali dei
    colori.
2.  Utilizza un Hald CLUT negativo tramite lo strumento [Simulazione
    Pellicola](Film_Simulation.md). La "Collezione di
    simulazione di pellicole RawTherapee" ne contiene uno, utilizzalo
    dalla pagina [Simulazione Pellicola](simulazione_film).
    L'inconveniente è che alcuni comandi potrebbero funzionare al
    contrario, come il cursore Esposizione, e si possono verificare
    ritagli nelle ombre e/o nelle alte luci poiché questi strumenti non
    sono progettati per funzionare con i negativi.
3.  Oltre a utilizzare un Hald CLUT negativo neutro come descritto in
    precedenza, se si dispone di un flusso di lavoro non solo invertendo
    i negativi, ma anche assegnando la giusta tonalità con RawTherapee o
    in un altro software, è possibile [Creare un Hald CLUT
    negativo](Film_Simulation_#_Make_Your_Own.md) che riproduce
    l'intero aspetto, tra cui inversione del negativo. A tale scopo,
    applica gli stessi passaggi di "identity Hald CLUT image" fornita
    con la Collezione di simulazione di pellicole di RawTherapee come
    faresti ad un negativo, salvala con un nuovo nome, quindi riapri il
    negativo in RawTherapee e applicare questa nuova Hald CLUT. Ciò
    consente di ottenere immediatamente non solo l'inversione negativa
    ma anche la propria correzione di tono con un solo clic, resta
    semmai una correzione dell'istogramma da fare regolando il cursore
    dell'Esposizione o utilizzando le curve.
4.  Attualmente il metodo migliore è quello di utilizzare il DCP (DNG
    Camera Profile) per il tuo modello di fotocamera ma modificato in
    Editor di profili DNG in modo che la curva di tono diagonale sia
    invertita, quindi caricare manualmente questo DCP in RawTherapee per
    tutti gli scatti negativi. Metodo descritto di seguito.

## Creazione di un DCP per Negativi

![](_DNG_Profile_Editor_inverted_tone_curve.png "_DNG_Profile_Editor_inverted_tone_curve.png")
![](Rt_negative_dcp_l_curve.png "Rt_negative_dcp_l_curve.png")

1.  Ottieni [Editor dei profili
    DNG](http://www.adobe.com/support/downloads/detail.jsp?ftpID=5494).
    Funziona bene in Linux attraverso [1](https://www.winehq.org/wine).
2.  Convertire una delle foto raw della fotocamera o dello scanner (può
    essere la foto del negativo) a DNG seguendo la guida "[Come
    convertire i formati raw in
    DNG](Come_convertire_i_formati_raw_in_DNG.md)".
3.  Aprire l'immagine DNG nell'editor del profilo DNG.
4.  Nella scheda Tabelle Colori, vedere se è disponibile il profilo base
    chiamato "Adobe Standard (*<il modello della tua fotocamera>*)". Se
    è così, selezionalo. In caso contrario, seleziona "Scegli il profilo
    esterno" e trova il file intitolato "*<modello di fotocamera>* Adobe
    Standard.dcp". La guida [come ottenere i profili LCP e
    DCP](come_ottenere_i_profili_LCP_e_DCP.md) spiega come
    ottenerli e dove trovarli.
5.  Nella scheda Curva di tono invertite la diagonale in modo da passare
    da alto a sinistra a basso a destra (spostare il punto superiore
    verso il basso).
6.  Nella scheda Curva di tono esistono tre "Curve di tono base" da
    scegliere. "Profilo di base" e "Camera Raw Default" sono
    generalmente identici e hanno più contrasto, mentre "Lineare" rende
    l'immagine piatta. Ti consigliamo di salvare un DCP che utilizza
    "Profilo Base" e un altro che utilizza "Lineare" e scopri quale è
    più adatto alle tue esigenze in RawTherapee. Entrambi i DCP
    richiederanno ulteriori modifiche dell'immagine in RawTherapee, ma
    la linea "lineare" richiederà più modifiche rispetto alla "Curva di
    Base", anche se quest'ultima potrebbe sovra saturare i colori - fai
    attenzione a questo.
7.  Per creare il DCP, fare clic su
    "File\>Esporta*<modello di fotocamera>* profilo ...". Come indicato
    nel passaggio precedente salvare due versioni.

Per utilizzare questo nuovo DCP per i Negativi, una volta che hai aperto
il tuo raw negativo in RawTherapee, vai alla scheda Colore\> Gestione
del colore\>Profilo di input e seleziona Personalizzato, quindi trova
questo nuovo file DCP. Abilita "Usa la curva di tono di DCP".

Quando si modificano le immagini in RawTherapee usando questi DCP,
ricordate si utilizzare le curve di tono che operano sui canali RGB
(curva di tono 1 e 2 nello strumento Esposizione) andando a cambiare non
solo la luminosità, ma anche la saturazione del colore, e questo in modo
evidente. È possibile controllare la saturazione dei colori utilizzando
le modalità "Standard ponderato" e "Saturazione e miscelazione valore",
oppure è possibile evitare il problema lavorando nello spazio L\*a\*b\*.
Il vantaggio di lavorare nello spazio L\*a\*b\* con la curva L\* è che i
colori non vengono modificati mentre si modifica la luminosità, è così
possibile poter correggere profondamente la luminosità dell'immagine
usando una curva L\* e poi fissare la saturazione del colore usando ad
esempio la curva CC.
