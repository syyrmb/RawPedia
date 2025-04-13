---
title: Default it
contributors:
  - Andrea.romagnoli
---

Quando si apre una foto raw che hai precedentemente modificato,
RawTherapee ottiene ovviamente le impostazioni che hai precedentemente
deciso per l'esposizione, la nitidezza, il ritaglio ecc. Il primo
momento in cui apri una fotografia raw, però RawTherapee utilizza
l'elaborazione "predefinita" (a meno che non sia stato modificato il
profilo di elaborazione predefinito per le foto raw in "Preferenze\>
Elaborazione di immagini\> [Profilo di elaborazione
predefinito](Preferenze#Default_Processing_Profile.md)"). Questo
profilo contiene impostazioni in gran parte neutre e alcune modifiche
che dovrebbe far risultare la foto piacevole e che puoi continuare a
modificare secondo il tuo gusto. In particolare, utilizza [Livelli
automatici](Exposure#Auto_Levels.md) per ottenere i toni e
l'esposizione corretta, moderata [nitidezza](sharpening),
rimozione automatica [Aberrazione
cromatica](Chromatic_Aberration.md) e fissaggio dei pixel
caldi/morti usando lo strumento
[Pre-elaborazione](preprocessing). L'immagine prodotta non
sarà come il JPEG prodotto dalla camera (o come la miniatura originale
che hai visto per quella foto, identica al JPEG esterno).

Quando si apre i file non raw (JPEG, TIFF o PNG) per la prima volta,
RawTherapee utilizza un profilo diverso, il profilo "Neutral" (a meno
che non sia stato modificato il profilo di elaborazione predefinito per
le foto non raw in Preferenze, come sopra descritto). Il profilo
"Neutral" non modifica l'immagine e quindi dà un punto di partenza che è
neutro!

RawTherapee è impostato per utilizzare il profilo "Default" per le foto
raw e il profilo "Neutral" per le foto non raw per impostazione
predefinita dopo un'installazione pulita. Se non funzionano per voi,
puoi modificarli da "Preferenze\> Elaborazione di immagini\> [Profilo di
elaborazione
predefinito](Preferences#Default_Processing_Profile.md)". La
sezione "[Creazione di profili di elaborazione per uso
generale](Creating_processing_profiles_for_general_use.md)" ti
aiuterà a creare profili personalizzati.
