---
title: Batch-Sync es
contributors:
  - XavAL
---

## Revelado por lotes

El ***revelado por lotes*** se diferencia con la ***sincronización*** en
que aquí procesas una imagen y después copias/pegas el perfil de
procesamiento en el resto de fotos, mientras que en la *sincronización*
se revelan todas las fotos a la vez. Esta opción quizá sea algo más
lenta que la *sincronización*, pero permite afinar mucho más el
procesado porque estás viendo la imagen con la ampliación que desees en
la *vista previa* del *Editor*.

El procedimiento general es seleccionar una imagen clave o
representativa del grupo a modificar y revelarla completamente según se
desee. A continuación, tras volver al *Explorador de archivos*, haz
sobre la imagen y dentro de ***Operaciones con el [perfil de
procesamiento](Sidecar_Files_-_Processing_Profiles/es.md)***,
haz en **Copiar**. Después, tras seleccionar las imágenes necesarias,
sobre una de éllas haz y dentro de *Operaciones con el perfil de
procesamiento*, haz en **Pegar** o en **Pegar - parcialmente**.

Copiar y pegar un perfil de procesamiento a una selección de imágenes es
una tarea muy común. Supongamos que has tomado una serie de fotos, por
ejemplo tomas de estudio, retratos de boda o fotos macro con apilado de
enfoque. Todas las imágenes van a ser muy similares: probablemente
usarán el mismo objetivo, la misma ISO, el mismo equilibrio de blancos,
y acabarán destinándose al mismo propósito. Esto significa que
probablemente todas necesitarán los mismos parámetros de procesamiento:
la misma reducción de ruido, la misma nitidez, corrección de la
distorsión del objetivo y así sucesivamente.

Además, RawTherapee te permite aplicar solamente una parte del perfil de
procesamiento copiado, por ejemplo solamente la herramienta
"Exposición". Para hacer ésto, usa la opción *Pegar - parcialmente*,
mientras que si quieres aplicar todos los ajustes en todas las fotos
seleccionadas, usa la opción *Pegar*.

## Sincronizar el procesado en varias imágenes

La ***sincronización*** se diferencia con el ***revelado por lotes*** en
que aquí procesas todas las imágenes a la vez, mientras que en el
*revelado por lotes* se procesa una imagen y después copias/pegas el
perfil de procesamiento en el resto de fotos. Esta opción quizá sea algo
más rápida que el *revelado por lotes* y es interesante para realizar
ajustes rápidos y no muy finos a las fotos, aunque no verás el resultado
final porque sólo verás la foto con el tamaño de las miniaturas.

Para *sincronizar* el procesado en varias fotos sólo tendrás que
seleccionarlas en la pestaña *Explorador de archivos* y acceder a las
*herramientas de sincronización* del panel *Revelar*, a la derecha.
Estas herramientas son las mismas que encontrarás en la pestaña del
*Editor*, pero sólo se usan para la *sincronización*.

Tus retoques pueden reemplazar los existentes (modo ***Establecer***), o
sumarlos (modo ***Añadir***). Por ejemplo, supongamos que seleccionas
dos fotos, una de las cuales ha sido retocada con **+1EV** de
*Compensación de exposición* y la otra sin retocar. Si en la herramienta
de sincronización *Exposición* ajustas la *Compensación de exposición* a
**+0.6EV**, entonces la foto que ya estaba editada tendría una
*Compensación de exposición* de **+1.6EV** en modo *Añadir* y sólo
**+0.6EV** en modo *Establecer*. La foto que no había sido previamente
retocada tendría **+0.6EV** en ambos modos.

Para decidir en qué modo debe funcionar cada herramienta de
sincronización, debes establecerlo en la [**pestaña Procesamiento por
lotes**](Preferences/es#Batch_Processing_Tab.md), de las
*Preferencias*.
