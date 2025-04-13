---
title: Wavelets es
contributors:
  - XavAL
---

<div class="pagetitle">

Niveles de Ondícula

</div>

## ¿Cómo está organizada esta herramienta?

La herramienta de Niveles de Ondícula es muy extensa y su funcionamiento
interno es francamente complejo. Salvo por algunas tareas como la
interpolación o la gestión del color, puedes llegar a procesar
completamente una fotografía solo con esta herramienta, aunque su mejor
virtud es su capacidad de completar y refinar el efecto de otras
herramientas.

La estructura general consiste en un bloque de ***configuración de la
herramienta**'', seguido de una serie de***módulos**'' (grupos de
opciones) que realizan tareas específicas. Podrás activar o desactivar
los módulos que desees, aunque si los desactivas todos conseguirás el
mismo efecto que desactivando la herramienta.

## ¿Qué son las Ondículas?

Una [Ondícula](https://es.wikipedia.org/wiki/Ondícula), o más
específicamente una [Transformada de
Ondícula](https://es.wikipedia.org/wiki/Transformada_ondícula), es una
función matemática compleja y muy útil en el procesamiento de imágenes,
ya que te permite dividirlas en varios niveles de detalle para que
puedas trabajar en el que te interese.

El término técnico de las ondículas fue introducido a principios de los
años 80 por los físicos franceses Jean Morlet y Alex Grossman:
utilizaron la palabra francesa *ondelette*, que significa *onda
pequeña*. Posteriormente, esta palabra fue adaptada al inglés cambiando
*onde* por *wave*, quedando *wavelet*. En español se emplea una
adaptación basada en el latín (*unda*=onda, *-ícula*=pequeña; y al
final, *ondícula*).

La *Transformada de Ondícula* es similar a una *Transformada de
Fourier*: se trata de representar los datos como combinaciones de ondas
conocidas y predefinidas (las frecuencias), de forma que el resultado
sea lo más parecido posible a los datos originales. A *grosso modo*, la
diferencia principal para imágenes de dos dimensiones es que en la
Transformada de Ondícula los datos que se están analizando se
representan como las frecuencias presentes en los puntos de la imagen,
mientras que en la Transformada de Fourier estándar sólo se representan
como las frecuencias presentes en la imagen completa. Por lo tanto,
utilizar ondículas ofrece más precisión a la hora de analizar los datos.
  <span style="font-size: 0.7em; font-style: italic;">\[Obviamente esta
es una explicación muy simplista y resumida: los matemáticos seguro que
tendrían mucho que decir aquí...\]</span>

![](Wavelet_daubechies20.png "Wavelet_daubechies20.png")RawTherapee
emplea las ondículas en varias herramientas y en ésta en concreto usa la
ondícula de
[Daubechies](https://en.wikipedia.org/wiki/Daubechies_wavelet)
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span>, con la que descompone los elementos de la imagen en
el [espacio de color
L\*a\*b\*](https://es.wikipedia.org/wiki/Espacio_de_color_Lab) (*L\**,
*a\** y *b\**).

Descomponer la imagen implica analizar mediante un
[algoritmo](https://es.wikipedia.org/wiki/Algoritmo) el contraste
«interno» de grupos de píxeles (2x2=4 píxeles en el primer nivel, 4x4=16
píxeles en el segundo nivel, ...) en tres direcciones: vertical,
horizontal y diagonal. Este análisis convierte los valores de esos
contrastes en conjuntos de ondículas con diferentes amplitudes e
intensidades y guarda sus características en matrices de coeficientes,
que indican cómo se deben combinar las ondículas para regenerar una
imagen lo más similar posible a la original.

Y cada vez que realizas modificaciones (contraste, tono, ruido, ...)
esta regeneración se realiza de forma automática e interactiva, de forma
que puedas ver inmediatamente el resultado de tus ajustes.

En este sentido, una vez descompuesta, la imagen gráfica deja de existir
y sólo quedan conjuntos de coeficientes (un conjunto por cada nivel) que
serán con los que trabajará la herramienta. Estos conjuntos representan
dos resultados diferentes:

- varios niveles de detalle: el primer nivel corresponde a detalles con
  un área de 2x2 píxeles; el décimo nivel corresponde a «detalles» con
  una área de 1024x1024 píxeles. La elección de cuántos usar depende de
  tus necesidades, sin embargo ten en cuenta que cuantos más niveles se
  extraigan, más tiempo de procesamiento y más memoria harán falta.

  
Por otro lado, como en cada nivel sólo se analizan las *variaciones*
(gradientes, o diferencias) del
[tono](https://es.wikipedia.org/wiki/Tono_(color)) o la
[luminancia](https://es.wikipedia.org/wiki/Luminancia), si una imagen es
absolutamente uniforme en luminancia y color, los niveles no contendrán
ninguna información. Es decir, las diferencias que se extraen en cada
nivel provienen del ruido digital y los cambios en el contraste (o
cromaticidad) debidos a efectos de borde, niebla u otros fenómenos
ópticos provenientes de la escena.

- una imagen residual: es el resultado de eliminar de la imagen original
  los detalles presentes en todos los niveles analizados, con la
  importante particularidad de que la modificación de las
  características de un nivel (contraste, cromaticidad, etc.) no tiene
  efecto sobre la imagen residual. Y viceversa.

Además, para cada nivel la herramienta tiene en cuenta el conjunto de
valores de los coeficientes y calcula su media aritmética (con lo que en
cada nivel la media será diferente) y la [desviación
típica](https://es.wikipedia.org/wiki/Desviación_típica). Añadiendo el
coeficiente máximo y el coeficiente mínimo a estos datos se genera una
curva de distribución que representa las características de cada nivel
(es de destacar que esta curva no es
[Gaussiana](https://es.wikipedia.org/wiki/Distribuci%C3%B3n_normal)).
Todo éllo se emplea de distintas formas en los algoritmos de la
herramienta.

## En la práctica

Tras la descomposición se pueden usar los niveles resultantes para
distintos propósitos: compresión de la imagen, reducción de ruido,
[marcas de agua
secretas](http://www.intechopen.com/books/discrete-wavelet-transforms-algorithms-and-applications/application-of-discrete-wavelet-transform-in-watermarking)
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span>, tratamiento específico de la imagen residual para
astronomía, etc.

Dependiendo de tus necesidades, tendrás que trabajar con un nivel de
detalle individual, con varios niveles de detalle (uno tras otro), con
la imagen residual, o con todos éllos combinados.

El tamaño de los detalles incluídos en cada nivel es:

<figure>
<img src="/images/Wavelet_detail_size.png" title="Wavelet_detail_size.png" />
<figcaption>Wavelet_detail_size.png</figcaption>
</figure>

  
  
**1 (Fino)**: 2x2 píxeles

**2**: 4x4 píxeles

**3**: 8x8 píxeles

**4**: 16x16 píxeles

**5**: 32x32 píxeles

**6**: 64x64 píxeles

**7**: 128x128 píxeles

**8**: 256x256 píxeles

**9** (Grueso): 512x512 píxeles

**Extra**: 1024x1024 píxeles

Si seleccionases 5 niveles de detalle, las modificaciones en los
distintos niveles se limitarían a los detalles con un tamaño de 32
píxeles o más pequeños. En este caso la imagen residual tendrá todos los
detalles de la imagen, excepto los que se hayan incluído en los niveles
del *1* al *5*. Y dado que los detalles eliminados son relativamente
pequeños, la imagen residual será bastante similar a la imagen original.

Por el contrario, si escogieses el *nivel 9* podrías cambiar los
detalles con un tamaño de 512 píxeles y de 1024 píxeles (*nivel Extra*).
En este caso la imagen residual será bastante diferente a la imagen
original, ya que los niveles del *1* al *Extra* contendrán todos los
detalles, por lo que lo que quedará será poco más que un fondo
emborronado.

En cualquier caso, la descomposición por ondículas separa tanto en la
imagen residual como en cada nivel la
*[luminosidad](https://es.wikipedia.org/wiki/Luminosidad_(color))* y los
canales de *[color](http://www.huevaluechroma.com/015.php)*
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span>
(\[<https://es.wikipedia.org/wiki/Espacio_de_color_Lab#El_espacio_de_color_CIE_1976_L>\*,_a\*,_b\*_CIELAB)
*a\** y *b\**\]). Gracias a ésto puedes aplicar diferentes ajustes a la
luminosidad y a los tonos de cada nivel, sin impedir que realices un
procesado completamente distinto en la imagen residual. Es decir, los
niveles y la imagen residual son independientes: la herramienta solo
realizará modificaciones en aquellos niveles en los que hagas cambios,
el resto permanecerán sin alterar y además la imagen residual seguirá
siendo lo que quede después de eliminar todos los detalles de todos los
niveles (se hayan modificado o no).

Es necesario destacar que si deseas usar las ondículas al mismo tiempo
que [la herramienta CIECAM](CIECAM02/es.md), es posible que te
encuentres con artefactos debidos a que el modelo de color CIECAM
utiliza valores específicos que son cercanos pero a la vez diferentes de
los valores del espacio de color Lab. Conforme está codificada la
herramienta estos artefactos son inevitables, pero su aparición
dependerá del procesado que realices.

#### La vista previa

El tamaño en pantalla de la imagen tiene un impacto directo en la
nitidez percibida y en la apreciación de los mínimos cambios realizados
en cada módulo: **los efectos de esta herramienta solo son visibles con
el zoom a tamaño real** (o más ampliado). En la práctica, ésto significa
que, [por razones de velocidad de
procesado](General_Comments_About_Some_Toolbox_Widgets/es#La_Vista_Previa.md),
debes tener previsto el tamaño final de la imagen y si va a ser
necesario reducirla (reducir su escala, no recortarla), entonces primero
la tendrás que exportar con el tamaño definitivo y luego procesarla con
las ondículas. Tenlo en cuenta porque de otro modo lo que veas en la
vista previa no será igual al resultado final después de exportar.

Por otro lado se presenta otra limitación: RawTherapee utiliza en la
vista previa todos los niveles que puede, ignorando aquellos niveles
cuyos detalles son más grandes que la porción de la imagen que ves en
pantalla. Pero aunque las modificaciones en los niveles ignorados no se
muestren en pantalla, sí que se aplicarán a la hora de procesar la
imagen para guardarla en disco.

**Ejemplos**

- **ejemplo 1**: la imagen es de **4096x2160** píxeles, la has ampliado
  (al 100% o más) y en la vista previa ves una zona de **1500x1200**
  píxeles a un tamaño similar al que tendrá en la imagen final. Este es
  el caso ideal y en pantalla podrás ver todas las modificaciones que
  realices en todos los niveles (hasta el *nivel Extra*). Además, los
  cambios que realices en todos los niveles se incluirán en la imagen
  final.
- **ejemplo 2**: la imagen es de **4096x2160** píxeles, pero la has
  ampliado y en la vista previa solo ves **300x200** píxeles, por lo
  cual en pantalla no podrás ver ninguna modificación en detalles más
  grandes que los del *nivel 7* (detalles de 128 píxeles), pero al
  guardarla los cambios que realices en los niveles *8*, *9* y *Extra*
  sí serán incluídos (porque la imagen es mayor que 1024x1024 píxeles).
- **ejemplo 3**: la imagen es de **720x480** píxeles y la has ampliado
  hasta que en la vista previa solo ves **300x200** píxeles, por lo cual
  en pantalla no podás ver ninguna modificación en detalles más grandes
  que los del *nivel 7* (detalles de 128 píxeles) ***y además*** al
  guardarla los cambios que realices en el *nivel 8* sí se incluirán
  (detalles de 256 píxeles), pero los niveles *9* y *Extra* **NO** serán
  incluídos.

Como todo esto es muy importante no olvidarlo, la propia herramienta te
informa de cuántos niveles se están usando para la vista previa, debajo
del último control deslizante del módulo de *Contraste*. En los ejemplos
2 y 3 anteriores verías: «**Máximo número de niveles empleados en la
vista previa = 7**».

#### Contraste por Niveles de detalle vs Niveles de Ondícula

Cabe mencionar que RawTherapee tiene una herramienta llamada *[Contraste
por Niveles de detalle](Contrast_by_Detail_Levels/es.md)* y
aunque se parece a la herramienta Niveles de Ondícula, hay varias
diferencias importantes entre éllas:

- el *Contraste por Niveles de detalle* tiene menos niveles (6, en lugar
  de hasta 10),
- el *Contraste por Niveles de detalle* solo permite ajustar la
  luminancia de cada nivel, mientras que los Niveles de Ondícula también
  te permiten ajustar la cromaticidad de cada nivel,
- el *Contraste por Niveles de detalle* ajusta por igual todas las
  luminancias (o cromaticidades) del nivel, mientras que los Niveles de
  Ondícula realizan un ajuste progresivo ([ésto se entenderá mejor en el
  capítulo de atenuación del
  contraste](#La_curva_de_atenuación.md)),
- el *Contraste por Niveles de detalle* no tiene imagen residual.

Dicho ésto, nadie te impide usar ambas herramientas a la vez, aunque ten
en cuenta que el *Contraste por Niveles de detalle* se aplica antes en
el [circuito de revelado](Toolchain_Pipeline/es.md), así que
según la intensidad de los ajustes realizados allí, podrían verse
afectados los detalles que se presentarán en los niveles del *1* al *6*.
Es decir, puesto que el contraste habrá cambiado con los ajustes del
*Contraste por Niveles de detalle*, el análisis por Niveles de Ondícula
podría descomponer la imagen de manera diferente, con lo que los
resultados serían distintos. En todo caso, si debes utilizar las dos
herramientas, es recomendable que ajustes en primer lugar el *Contraste
por Niveles de detalle* y después te dediques a ajustar los Niveles de
Ondícula.

## Configuración general de la herramienta

Una vez activada la herramienta, podrás realizar ajustes generales de su
comportamiento, que afectarán a todos los módulos.

### Intensidad

Con este control deslizante regularás la intensidad global de la
herramienta.

Se trata de imaginar que se mezclan dos imágenes superpuestas: la imagen
original estará debajo y sobre élla se superpone la imagen modificada
por esta herramienta, mientras que con este control modificarás la
opacidad (la transparencia) de la imagen superior para que el resultado
final sea más suave o gradual. Así se pueden hacer ajustes más
agresivos, que luego se integrarán mejor en la imagen original mediante
la transparencia.

### Niveles de Ondícula

Este control deslizante te permite decidir en cuántos niveles de detalle
se descompondrá la imagen. Podrás escoger cualquier nivel entre *4* y
*9* (el décimo nivel, que se llama *Extra*, aparece automáticamente
cuando seleccionas el *nivel 9* ). Cuanto más alto sea el número,
mayores serán las necesidades de tiempo de procesado y de memoria.

### Método de mosaico

Una lista desplegable te permite elegir entre:

- Imagen completa,
- [Teselas](https://es.wikipedia.org/wiki/Teselado_regular).

Siempre es preferible emplear la *Imagen completa*, ya que evita
problemas en la zona de transición entre teselas.

Sin embargo, si no tienes suficiente memoria RAM, o si estás procesando
imágenes muy grandes (por ejemplo, 50 Megapíxeles o más), es posible que
sí tengas que usar las teselas:

| Memoria necesaria, en bytes, con 9 niveles de detalle      |
|------------------------------------------------------------|
|                                                            |
| Megapíxeles (Mpx)                                          |
| Para abrir la imagen (todas las herramientas desactivadas) |
| Contraste, Cromaticidad o Protección de matiz activado     |
| \+ Evitar el Cambio de Color                               |
| Total                                                      |

### Comportamiento de los bordes

La descomposición de los componentes por el método de Daubechies puede
tener hasta 10 escalas de coeficiente, desde D2 (que corresponde a la
descomposición Haar) hasta D20. En RawTherapee se usan los coeficientes
*D2 (bajo), D4 (estándar), D6 (estándar plus), D10 (medio) y D14
(alto)*. Cuantos más coeficientes se usen, más detalles distinguirá la
ondícula y se producirá un ligero aumento en el tiempo de procesamiento
(muchas veces inapreciable).

Aunque no existe una relación directa entre la calidad resultante y el
número de coeficientes (dependiendo ésta de la imagen original), escoger
la cantidad de coeficientes correcta permitirá refinar la calidad de los
niveles inferiores, o la de la imagen residual:

- en algunos casos los mejores resultados para la detección de bordes se
  obtienen con D2
- en otros casos con D6 o D14

Este parámetro tiene un impacto bastante alto en la *[Detección de
bordes](#Detección_de_bordes.md)* y también en la descomposición
global (la relación entre la imagen residual y cada nivel).

### Vista previa

Este grupo de controles te servirán para ayudarte a entender cómo
trabajar con esta herramienta de ondículas y para ajustar con precisión
los parametros de los módulos (por ejemplo en la reducción de ruido).

Tienes cuatro listas desplegables en total, que te permiten adaptar lo
que verás en la vista previa.

El grupo se divide en dos listas desplegables principales (y dos más que
se activarán cuando realices ciertas selecciones en las listas
principales):

- la primera sirve para escoger un fondo para la vista previa
- la segunda permite escoger qué niveles se verán en la vista previa

#### El fondo

En la lista ***Fondo:*** puedes elegir entre 3 fondos posibles y el que
elijas será el que podrás ver detrás de todos los niveles: *Negro*,
*Gris* o *Imagen Residual*.

El histograma tendrá en cuenta estas opciones y te permitirá, por
ejemplo, ver los efectos de los ajustes en la imagen residual. Sin
embargo, ten en cuenta que si eliges los fondos negro o gris, no verás
la imagen residual (el fondo real) y puede que encuentres la imagen con
un aspecto extraño. Debes tener esto especialmente en cuenta si realizas
cambios en los niveles de detalle, ya que el efecto real no lo verás
hasta que vuelvas a poner como fondo la imagen residual. A pesar de
éllo, a veces es interesante ver los cambios sobre un fondo neutro para
juzgar mejor lo que está ocurriendo (por ejemplo en la reducción de
ruido).

#### Los niveles

En la lista ***Niveles:*** podrás seleccionar:

1.  *Un nivel*
2.  *Niveles con detalles finos, incluyendo el seleccionado*: todos los
    niveles **desde** el seleccionado hasta el *nivel 1*,
3.  *Niveles con detalles grandes, sin incluir el seleccionado*: todos
    los niveles hasta el *nivel Extra* (más la imagen residual), pero
    **sin incluir** el seleccionado
4.  *Todos los niveles en todas direcciones*

A modo de comparación con versiones anteriores del programa, la lista se
mostraba con diferentes títulos, aunque el significado era el mismo:

- Un nivel
- Por debajo o igual que el nivel: ahora *Niveles con detalles finos,
  incluyendo el seleccionado*
- Por encima del nivel: ahora *Niveles con detalles grandes, sin incluir
  el seleccionado*
- Todos los niveles en todas direcciones

Si seleccionas cualquiera de las tres primeras opciones, se activarán un
par de listas desplegables justo debajo de *Niveles:*

- en la lista de la izquierda decidirás cuál será el nivel al que hacen
  referencia las opciones anteriores (desde el *nivel 1* al *9*, el
  *nivel Extra*, o la *Imagen Residual*).
- en la lista de la derecha podrás escoger la dirección de
  descomposición de la ondícula (*Vertical, Horizontal, Diagonal, Todas
  las direcciones*).

En cambio, si seleccionaras la opción *Todos los niveles, en todas
direcciones*, entonces editarías los niveles directamente sobre la
imagen residual (las dos listas inferiores permanecerían desactivadas).
Esta opción es útil si ya tienes experiencia con la herramienta y vas
*directo al grano*, es decir, si prefieres estar viendo la imagen
completa mientras la modificas. Además es la opción que deberás
seleccionar antes de exportar. Ten en cuenta que lo que veas en la vista
previa será lo que se exporte en la imagen final y lo que se muestre en
el histograma: si has seleccionado *un nivel*, verás en pantalla solo un
nivel, el histograma reflejará los valores RGB de ese nivel y al
exportar solo se incluirá en la imagen final el nivel elegido. Así pues,
*'antes de exportar, asegúrate que has seleccionado*Todos los niveles,
en todas direcciones'''.

#### Sugerencias de uso

- puedes seleccionar *Un nivel* con un fondo gris para apreciar cómo ha
  descompuesto los detalles el coeficiente de Daubechies elegido (del D2
  al D14), e ir probando coeficientes diferentes para ver cual ofrece la
  separación de detalles más ajustada a lo que necesitas
- puedes seleccionar *Un nivel* para encontrar el nivel que tenga los
  detalles sobre los que quieres trabajar (como puede ser el nivel que
  haya extraído las manchas de la piel, pero no su textura)
- puedes seleccionar *Un nivel* y ver el efecto de los cambios de
  contraste en ese nivel concreto, o afinar en la reducción de ruido
- puedes seleccionar *Niveles con detalles grandes, sin incluir el
  seleccionado* y *8*, para ver la imagen residual junto con los
  detalles más grandes y apreciar mejor la acción de los distintos
  parámetros del módulo *Imagen Residual*
- puedes seleccionar *Niveles con detalles finos, incluyendo el
  seleccionado*, *4* y como fondo *Imagen Residual*, para ver en
  contexto las modificaciones en los detalles más finos, sin que los
  detalles más grandes enmascaren lo que estás haciendo.

### Ejemplo real (la vista previa)

A continuación tienes una imagen de ejemplo a la que se le ha realizado
un procesado mínimo. A su lado, de izquierda a derecha verás los
detalles de *nivel 2*, los detalles de *nivel 4* y la *imagen residual*.

En los dos ejemplos de detalles, la descomposición se ha realizado con
un ***Comportamiento de los bordes*** en *D6 (estándar plus)*, se ha
seleccionado como ***Fondo:*** el color *gris*. Además, para aislar el
detalle, en ***Niveles:*** se ha escogido *Un nivel*.

En cuanto a la *Imagen Residual*, es el resultado de eliminar todos los
detalles después de escoger *5 Niveles de ondícula*.

<span style="font-size: 0.7em; font-style: italic;">  ***Para ver las
imágenes un poco más grandes, deberás hacer clic en éllas y cuando se
cargue la nueva página, volver a hacer clic en la foto***. </span>

<div>

- <figure>
  <img src="/images/wavelet_pic.png" title="wavelet_pic.png" />
  <figcaption>wavelet_pic.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_L2.png" title="wavelet_config_L2.png" />
  <figcaption>wavelet_config_L2.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_L4.png" title="wavelet_config_L4.png" />
  <figcaption>wavelet_config_L4.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_config_RI.png" title="wavelet_config_RI.png" />
  <figcaption>wavelet_config_RI.png</figcaption>
  </figure>

</div>

## Módulo de Contraste

En este módulo podrás modificar el contraste de la luminosidad
(componente *L\**) de los detalles de cada nivel por separado, de manera
que podrás aumentar el contraste de los detalles más pequeños para dar
impresión de mayor nitidez, al tiempo que reducir el contraste de
detalles más grandes. Una utilidad práctica de esta forma de proceder es
que al reducir el contraste general (los detalles grandes), es necesario
aumentar en menor cuantía los detalles finos para notar un aumento de la
impresión de nitidez. Así es más fácil evitar introducir artefactos.

### La curva de atenuación

Tal como se comentó en otro capítulo, la herramienta calcula la media y
la desviación estándar en cada nivel de la descomposición, para
utilizarlas a lo largo de todos los módulos.

En el módulo de Contraste en concreto el primer paso es establecer el
valor de ajuste para todos los niveles de la descomposición que lo
necesiten, pero si solo realizaras esta acción, las variaciones del
contraste serían proporcionales al contraste original ([modificaciones
homotéticas, tal como ocurre en la herramienta *Contraste por Niveles de
Detalle*](https://es.wikipedia.org/w/index.php?title=Homotética)) y
sería bastante fácil generar artefactos.

Así pues, los contrastes de los detalles en cada nivel se analizan y
ordenan para recibir una modificación progresiva y atenuada, según una
curva similar a:

<figure>
<img src="/images/wavelet_beta.png" title="wavelet_beta.png" />
<figcaption>wavelet_beta.png</figcaption>
</figure>

A *grosso modo* y para cada nivel, este gráfico implica que:

- hacia la izquierda de la gráfica se sitúan los contrastes más suaves,
  mientras que hacia la derecha están los contrastes más intensos
- el valor establecido de contraste para cada nivel (*contrast* en el
  gráfico) será la modificación máxima a aplicar a los contrastes
  presentes en el nivel
- la modificación será máxima alrededor del valor de contraste medio de
  cada nivel (*mean*, en la gráfica)
- cuanto más distintos sean los valores de contraste del valor de
  contraste medio, menor modificación sufrirán
- tienen más atenuación los contrastes altos o fuertes que los bajos

Gracias a este comportamiento, los mayores cambios de contraste en cada
nivel se efectuarán en los valores medios de contraste, dejando a un
lado los valores extremos para evitar efectos excesivos o artefactos.
Sin embargo ten presentes dos puntos fundamentales:

1.  el valor de contraste medio es la media aritmética **de los valores
    de contraste presentes en el nivel**: si todos los contrastes
    presentes son altos (contrastes fuertes), la media será también
    alta, pero los contrastes extremos de ese nivel se modificarán menos
2.  cada nivel tiene su propio valor medio, dependiendo de los
    contrastes presentes en los detalles de ese nivel

### Niveles de Contraste

![](wavelet_contrast_buttons.png "wavelet_contrast_buttons.png") El
número de niveles mostrados viene definido por los ***Niveles de
Ondícula*** y podrás reducir o aumentar este número en la configuración
de la ondícula.

Los botones ***Contraste -*** y ***Contraste +*** facilitan la
modificación progresiva de los valores de cada nivel: más intensa en los
primeros niveles y más discreta en los últimos. Como puedes observar en
el ejemplo, la progresión es homogénea: empezando desde el *nivel
Extra*, que no modifica su contraste, en cada salto de nivel se añaden
31 unidades por cada nivel (la cantidad concreta dependerá de las veces
que hagas clic en los botones).

En general con estos botones se obtiene una progresión lógica del
[microcontraste](Edges_and_Microcontrast/es#Microcontraste.md):
mayor para los primeros niveles y menor para los últimos niveles. Sin
embargo no olvides que si un nivel es uniforme en contraste, la acción
del control deslizante de ese nivel será nula (si no hay detalles, no se
modifica nada).

Fíjate que la imagen residual no está incluida en este grupo de
controles porque no es un nivel: es lo que queda de la imagen original
tras quitar todos los detalles que se distribuyen entre los niveles.

### Atenuación y selectividad en el cambio de contrastes

Para poder ajustar a tus necesidades la curva explicada en el [análisis
de los contrastes de cada
nivel](#An.C3.A1lisis_de_los_contrastes_de_cada_nivel.md), verás
que dispones de 3 controles deslizantes:

1.  ***Atenuación***: al seleccionar valores positivos la parte superior
    de la curva se hace más amplia alrededor del contraste medio, aunque
    favoreciendo más a los contrastes altos. Por el contrario, al
    seleccionar valores negativos la curva se estrecha, por lo que se
    reduce el rango de contrastes que reciben una modificación notable.
    Gráficamente:
    <div>

    - <figure>
      <img src="/images/wavelet_beta+damper.png" title="wavelet_beta+damper.png" />
      <figcaption>wavelet_beta+damper.png</figcaption>
      </figure>

    - <figure>
      <img src="/images/wavelet_beta-damper.png" title="wavelet_beta-damper.png" />
      <figcaption>wavelet_beta-damper.png</figcaption>
      </figure>

    </div>
2.  ***Compensación***: desplaza la parte superior de la curva, de forma
    que los contrastes más intensamente modificados ya no sean los
    contrastes medios. Desplazando la curva a la derecha los contrastes
    más fuertes sufrirán una mayor variación, mientras que con valores
    negativos del deslizador los contrastes más suaves serán los que más
    se modifiquen. Gráficamente:
    ![](wavelet_beta+offset.png "wavelet_beta+offset.png")
3.  ***Umbral de mínimo contraste***: se trata del valor mínimo de
    contraste que deben tener los detalles del nivel de descomposición
    para que la herramienta los tenga en cuenta. Todos los contrastes
    más debiles, con un valor inferior al establecido aquí no se tendrán
    en cuenta al calcular la media de ese nivel, así como tampoco
    sufrirán ninguna variación, sean cuales sean los ajustes de los
    anteriores deslizadores. De esta forma podemos evitar resaltar el
    ruido o las texturas más finas y delicadas.

### Aplicar en

Este bloque de controles te permite decidir si los cambios en el
contraste de cada nivel se aplican a todos los detalles del nivel o solo
a los que tengan píxeles dentro de un rango determinado de
[luminancias](https://es.wikipedia.org/wiki/Luminancia). Gracias a ésto
podrás, por ejemplo, aumentar el contraste de los detalles finos que
tengan luminancia alta y reducir el contraste de detalles más grandes
con luminancia baja.

En la lista desplegable decidirás dónde aplicas los cambios de
contraste: en todo el rango de luminancias (es decir, en todos los
detalles del nivel) o solo en los detalles que tengan un determinado
valor de luminancia en la imagen.

#### Rangos de luminancias

Si has seleccionado el *Rango completo de luminancias*, todos los
detalles del nivel se verán modificados. En cambio al seleccionar *Rango
selectivo de luminancias*, los niveles afectados por estos rangos o
modificarán los detalles de las sombras, o modificarán los de las luces,
pero no ambos a la vez.

Además, tras seleccionar el *Rango selectivo de luminancias* aparecerán
varios controles para personalizar el resultado: un par de barras en
blanco y negro con puntos ajustables y una curva gráfica. A saber:

- **Rango de luminancias para los niveles con detalles finos**:
  - se trata de una pequeña área con un degradado en blanco y negro,
    donde se definen cuatro puntos que establecerán en qué luminancias
    será efectivo el cambio de contraste
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_contrast_highlight.png"
    title="wavelet_contrast_highlight.png" />
    <figcaption>wavelet_contrast_highlight.png</figcaption>
    </figure>

    </div>
  - si pasas el puntero del ratón por encima de élla, podrás ver en qué
    puntos se sitúan por defecto los límites: *Abajo-Izq: 50,
    Arriba-Izq: 75, Arriba-Der: 98, Abajo-Der: 100*. Se trata de un
    rango alrededor de las luces
  - estos valores son las luminancias que debe haber en la imagen para
    que a sus detalles se les aplique el cambio de contraste (más sobre
    ésto al explicar el siguiente control deslizante)
  - los valores por defecto se leerían así:
    - a los detalles con luminancia de 50 o inferior no se les aplicará
      cambio alguno
    - a los detalles con una luminancia a partir de 50 y hasta 75 se les
      irá aplicando cada vez una mayor cantidad de modificación
    - entre 75 y 98 se aplicará el 100% de la modificación
    - entre 98 y 100, se aplicará progresivamente menos cambio
  - para cambiar los valores de los puntos de la curva, tenemos dos
    opciones:
    - hacer clic y mover uno de los dos puntos de un lado (izquierda o
      derecha) y desplazaremos los dos puntos de ese lado, en bloque
    - presionar la tecla *mayúscula*, hacer clic en un punto y moverlo
      para desplazar únicamente ese punto
  - puedes modificar a voluntad los puntos de la curva y ajustar el
    rango deseado, pudiendo incluso seleccionar exclusivamente las
    luminancias más bajas (las sombras)

<!-- -->

- **Rango de luminancia para los niveles con detalles más grandes**
  - se presenta otra pequeña área con un degradado en blanco y negro,
    dónde se definen cuatro puntos que establecerán en qué luminancias
    será efectivo el cambio de contraste
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_contrast_shadow.png"
    title="wavelet_contrast_shadow.png" />
    <figcaption>wavelet_contrast_shadow.png</figcaption>
    </figure>

    </div>
  - de nuevo, pasando el puntero del ratón por encima de élla, verás en
    qué puntos alrededor de las sombras se sitúan por defecto los
    límites: *Abajo-Izq: 0, Arriba-Izq: 2, Arriba-Der: 25, Abajo-Der:
    50*
  - los niveles por defecto los leeríamos así:
    - a los detalles con luminancia entre 0 y 2 se les irá aplicando
      cada vez una mayor cantidad de cambio de contraste
    - entre 2 y 25 se aplicará el 100% de la modificación de contraste
    - entre 25 y 50, se aplicará progresivamente menos cambio
    - a partir de 50 no se aplicará cambio alguno
  - para cambiar los valores de los puntos de la curva, procederemos de
    igual forma que en la curva de los detalles finos, incluso llegando
    a seleccionar un rango exclusivamente para las luminancias más altas
    (las luces)

<!-- -->

- **Niveles con detalles Finos-Gruesos**:
  - es un área gráfica para establecer en qué niveles se cambiará el
    contraste de los detalles pertenecientes a zonas de la imagen con
    las luminancias exigidas anteriormente

  - la parte izquierda del gráfico corresponde a los niveles con los
    detalles más finos, siempre deberá situarse por encima del eje
    horizontal y por defecto termina en el *nivel 5*

  - la parte derecha del gráfico corresponde a los niveles con los
    detalles más gruesos, siempre deberá situarse por debajo del eje
    horizontal y por defecto comienza en el *nivel 6*

  - el gráfico se divide en 10 zonas verticales: de izquierda a derecha
    corresponden al *nivel 1*, hasta el *nivel Extra*. Desplazando la
    curva hacia arriba o abajo en cada zona modifica el efecto del
    módulo en esos niveles

  - <div class="parrpad">

    <figure>
    <img src="/images/wavelet_contrast_finercoarser.png"
    title="wavelet_contrast_finercoarser.png" />
    <figcaption>wavelet_contrast_finercoarser.png</figcaption>
    </figure>

    </div>

    en los niveles no comprendidos entre los establecidos en este
    gráfico los cambios se realizarán en el rango completo de
    luminancias. Por ejemplo, si la parte izquierda de la curva termina
    en la zona alrededor del *nivel 3* y la parte derecha empieza
    alrededor del *nivel 6*, los niveles *4* y *5* modificarán todos sus
    detalles sea cual sea la luminancia en la imagen'''''.

</br>

#### Casos prácticos

- estás usando 7 niveles y quieres que solo el *nivel 7* aplique cambios
  según el *Rango de luminancia para los niveles con detalles más
  grandes*: ajusta la parte derecha de la curva para que empiece
  alrededor de la zona donde está el *nivel 7* y desliza la curva hacia
  abajo para establecer la intensidad del cambio de contraste
- estás usando 7 niveles y solo quieres ser selectivo con los detalles
  más finos: ajusta el inicio de la parte derecha del gráfico. Mientras
  presionas la tecla mayúscula, desplaza el inicio de la zona hasta la
  derecha del todo, de manera que los detalles más grandes se
  modificarán en todo el rango de luminancias
- estás usando 7 niveles y quieres ser selectivo en los niveles *1* y
  *2*, al mismo tiempo que en los niveles *6* y *7*: ajusta el final de
  la parte izquierda alrededor del *nivel 2* y el inicio de la parte
  derecha alrededor del *nivel 6*. De esta forma los niveles *3*, *4* y
  *5* modificarán sus detalles sea cual sea la luminancia en la imagen

### Ejemplo real (modificando el contraste)

A continuación se vuelve a mostrar la imagen de ejemplo y a su lado, de
izquierda a derecha tienes varias posibilidades a la hora de aplicar un
aumento de contraste en todos los niveles, tras pulsar *15 veces* sobre
el botón ***Contraste +***.

En primer lugar se muestra el efecto sobre el ***Rango completo de
luminancias***, a su derecha el efecto si seleccionas el ***Rango
selectivo de luminancias**''. Por fin, un ejemplo de cómo puedes matizar
los cambios mediante el control***Intensidad**''.

Los controles no mencionados se han dejado en sus valores por defecto
(los puntos de las curvas, ...).

<div>

- <figure>
  <img src="/images/wavelet_pic.png" title="wavelet_pic.png" />
  <figcaption>wavelet_pic.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_WL.png"
  title="wavelet_contrast_15C+_WL.png" />
  <figcaption>wavelet_contrast_15C+_WL.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.png"
  title="wavelet_contrast_15C+_H3S6.png" />
  <figcaption>wavelet_contrast_15C+_H3S6.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6_Str50.png"
  title="wavelet_contrast_15C+_H3S6_Str50.png" />
  <figcaption>wavelet_contrast_15C+_H3S6_Str50.png</figcaption>
  </figure>

</div>

Y ahora la imagen original y la final, lado a lado para que aprecies
mejor las diferencias: puedes distinguir un aumento de nitidez de la
textura de los pétalos, sin arruinar el efecto global.

<div>

- <figure>
  <img src="/images/wavelet_pic.png" title="wavelet_pic.png" />
  <figcaption>wavelet_pic.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6_Str50.png"
  title="wavelet_contrast_15C+_H3S6_Str50.png" />
  <figcaption>wavelet_contrast_15C+_H3S6_Str50.png</figcaption>
  </figure>

</div>

## Módulo de Color

Este módulo funciona de manera similar al del contraste, aunque en este
caso la herramienta analiza el contraste de los colores (componentes
*a\** y *b\**).

En la lista desplegable ***Método de color:*** tienes las siguientes
opciones:

- *Rango completo de color*: con esta opción, cualquier cambio en
  cualquier nivel afectará al rango completo de tonos,
  independientemente de los valores en los niveles del *Módulo de
  contraste*.
- *Saturado/Pastel*: aquí modificarás dos rangos que actúan a la vez y
  limitan los tonos pastel y los tonos saturados, independientemente de
  los niveles del *Módulo de contraste*.
- *Enlazar con los niveles de contraste*: los cambios en cromaticidad
  estarán directamente relacionados con los que se hayan efectuado en
  cada nivel del *Módulo de contraste*.

Cuando selecciones *Rango completo de color* o *Saturado/Pastel* podrás
emplear el botón *Neutro*, que sirve para reiniciar todos los
deslizadores de los niveles al valor por defecto (0).

Por otra parte, en cualquiera de las 3 opciones tendrás a tu disposición
un deslizador de *Atenuación*, que actuará de la misma forma explicada
en el [capítulo sobre la atenuación del módulo de
Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md).

### Rango completo de color

Si seleccionas esta opción, se modifica el rango completo de tonos de la
imagen, independientemente de lo saturados que ya estén.

La misma observación que en el contraste se aplica aquí: para que hayan
modificaciones en el color, debe preexistir una variación de tonos en el
nivel. Si un nivel tiene un color uniforme, el control deslizante no
producirá ningún efecto.

Las modificaciones de cada nivel están limitadas al rango
*\[-100,+100\]*: el valor *-100* es el equivalente a desaturar
completamente el nivel, mientras que el valor *+100* incrementa la
tonalidad de cada detalle. Este método casi siempre introduce
artefactos, dado que a cada valor de color de los detalles se les aplica
una fórmula simple que no tiene en cuenta si se generan desviaciones del
tono inicial.

<div>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.png"
  title="wavelet_contrast_15C+_H3S6.png" />
  <figcaption>wavelet_contrast_15C+_H3S6.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_full.png"
  title="wavelet_chrom_WC_full.png" />
  <figcaption>wavelet_chrom_WC_full.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_L1L2full.png"
  title="wavelet_chrom_WC_L1L2full.png" />
  <figcaption>wavelet_chrom_WC_L1L2full.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_detail.png"
  title="wavelet_chrom_WC_detail.png" />
  <figcaption>wavelet_chrom_WC_detail.png</figcaption>
  </figure>

</div>

Los ejemplos anteriores vienen a decir que con esta opción deberías ser
muy sutil, ya que dependiendo del nivel y la intensidad del cambio en el
color es bastante fácil introducir artefactos muy visibles. Sin embargo,
si eres demasiado sutil, los cambios apenas serán perceptibles. En
cualquier caso el ruido de color (en inglés: *chroma noise*) se verá
afectado y aumentará de forma notable.

### Saturado/Pastel

Con esta opción los cambios del color en cada nivel se centran en los
tonos saturados de los niveles con detalles de menor tamaño y en los
tonos pastel del resto de niveles (con detalles más grandes).

Tras seleccionarla, aparecen varios controles para personalizar el
resultado: un control deslizante y un par de barras en blanco y negro
con curvas ajustables, tal como ocurría con el contraste.

- **Umbral de saturado/pastel**
  - con este control decides en qué nivel se pasa de modificar los tonos
    saturados a los tonos pastel
  - el valor por defecto es *5*, es decir, en los primeros 5 niveles se
    modificarán los tonos saturados y en el resto los tonos pastel (los
    niveles más altos)
  - ten en cuenta que si este valor es superior al número de niveles de
    la descomposición, sólo se modificarán los tonos saturados
  - por otro lado, si eliges *1*, dado que este nivel solo tiene los
    detalles más finos, en la práctica es como si solo modificaras los
    tonos pastel
- **Rango de tonos pastel**:
  - tal como ocurría en el contraste, se trata de una pequeña área con
    un degradado en blanco y negro, dónde se definen cuatro puntos que
    establecerán en qué nivel de saturación será efectivo el cambio de
    color
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_chrom_pastel.png" title="wavelet_chrom_pastel.png" />
    <figcaption>wavelet_chrom_pastel.png</figcaption>
    </figure>

    </div>
  - *debes entender que la zona oscura del degradado son tonos pastel y
    la zona más clara son tonos saturados (siguiendo [esta explicación
    de saturación](https://es.wikipedia.org/wiki/Saturación_(color)))*
  - pasando el puntero del ratón por encima de élla, podrás ver los
    límites: por defecto los valores presentados son *Abajo-Izq: 0,
    Arriba-Izq: 2, Arriba-Der: 20, Abajo-Der: 30*
  - los cambios en la curva se realizan de forma análoga a los
    realizados en las curvas de contraste
- **Rango de tonos saturados**
  - pasando el puntero del ratón por encima de élla, verás en qué puntos
    se sitúan los límites: por defecto los valores presentados son
    *Abajo-Izq: 30, Arriba-Izq: 45, Arriba-Der: 100, Abajo-Der: 130*
    <div style="overflow: hidden">

    <figure>
    <img src="/images/wavelet_chrom_chrom.png" title="wavelet_chrom_chrom.png" />
    <figcaption>wavelet_chrom_chrom.png</figcaption>
    </figure>

    </div>
  - si bien los valores de ambas curvas no se solapan, se puede ver en
    la interfaz que sí se solapan y de hecho en la práctica parece que
    alrededor del nivel umbral los cambios afectan tanto a los tonos
    saturados como a los pastel. Para poder ver una distinción clara
    entre que haya efecto o no según el tono sea pastel/saturado,
    tendremos que ir a valores muy saturados o muy *insaturados*
    (pastel)

Con todo, tal como ocurría al modificar el *Rango completo de color*,
los cambios son poco apreciables si no estás dispuesto a introducir
artefactos bastante visibles.

<div>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.png"
  title="wavelet_contrast_15C+_H3S6.png" />
  <figcaption>wavelet_contrast_15C+_H3S6.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_WC_L1L2full.png"
  title="wavelet_chrom_WC_L1L2full.png" />
  <figcaption>wavelet_chrom_WC_L1L2full.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_SP_L1L2full_L3_60.png"
  title="wavelet_chrom_SP_L1L2full_L3_60.png" />
  <figcaption>wavelet_chrom_SP_L1L2full_L3_60.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6.png"
  title="wavelet_contrast_15C+_H3S6.png" />
  <figcaption>wavelet_contrast_15C+_H3S6.png</figcaption>
  </figure>

</div>

Como puedes ver, a pesar de aplicar los cambios al 100% en algunos
niveles, las diferencias son sutiles, incluso inapreciables si no te
fijas: los cambios más visibles son las «venas» en los pétalos con una
coloración más intensa.

### Enlazar con los niveles de contraste

En esta opción empezamos a hablar de resultados interesantes: los
cambios en el tono están directamente relacionados con los que se hayan
efectuado en cada nivel del contraste.

La proporción entre los cambios en el contraste y el color la regulas
con el control deslizante ***Intensidad de la relación
Color/Contraste***: así, *0* hará que no haya efecto alguno en la
cromaticidad, mientras que *100* proporcionará el máximo efecto. Y este
efecto máximo es más intenso que en *Rango completo de cromaticidad*
(particularidad especialmente notable en el ruido de color).

Ten en cuenta que si aplicas cambios fuertes en los contrastes, asímismo
serán en la cromaticidad y con mucha probabilidad se presentarán
artefactos indeseables: tu mejor aliado siempre será el control
***Intensidad de la relación Color/Contraste***, para conseguir efectos
claramente visibles sin que los artefactos arruinen la foto.

### Ejemplo real (modificando el color)

<div>

- <figure>
  <img src="/images/wavelet_chrom_Link_100.png"
  title="wavelet_chrom_Link_100.png" />
  <figcaption>wavelet_chrom_Link_100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_Link_50.png"
  title="wavelet_chrom_Link_50.png" />
  <figcaption>wavelet_chrom_Link_50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_chrom_Link_50_Str50.png"
  title="wavelet_chrom_Link_50_Str50.png" />
  <figcaption>wavelet_chrom_Link_50_Str50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_contrast_15C+_H3S6_Str50.png"
  title="wavelet_contrast_15C+_H3S6_Str50.png" />
  <figcaption>wavelet_contrast_15C+_H3S6_Str50.png</figcaption>
  </figure>

</div>

Como las modificaciones en la imagen original se están haciendo *a
grosso modo* para que se vean suficientemente bien los resultados, en
esta última foto (con modificación de contraste y color aplicados) se
pueden ver bordes azulados en los pétalos, halos alrededor de las
anteras de los estambres y un fondo lleno de ruido, pero aún así, dado
lo agresivas que son las modificaciones, parece que la imagen no está
tan desastrosa. En este punto cabe resaltar la intensidad que ha tomado
el tono de las «venas» en los pétalos.

## Módulo del Rango de colores

Este módulo está vinculado a los módulos de
[Contraste](#Módulo_de_Contraste.md) y
[Color](#Módulo_de_Color.md), de manera que te ayuda a afinar
dónde se aplican sus efectos dependiendo del tono (color) que tengan los
detalles. Es decir, ya no sólo tendrás en cuenta el contraste de la
luminosidad (módulo de contraste) o el contraste de los tonos (módulo de
color) de los detalles en cada nivel, sinó que además decidirás en qué
rangos de colores de la imagen se aplicarán estas modificaciones.

### Reducción de Artefactos en el azul del cielo

Las imágenes digitales a menudo tienen un ruido moteado en el azul del
cielo y además el procesado por Niveles de Ondícula puede generar o
incrementar pequeños artefactos, ya que intensifica el contraste local.

Esta casilla de selección introduce un [filtro de
mediana](https://en.wikipedia.org/wiki/Median_filter)
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span> para reducir estos artefactos, a costa de pérdida de
detalles y generación de artefactos en las zonas de cambio de tono o
elevado contraste. Aunque es útil para procesados rápidos y sin muchas
exigencias, en realidad conseguirás mejores resultados con una
combinación juiciosa de la herramienta *[Reducción de
ruido](Noise_Reduction/es.md)* y la *[Reducción de ruido de las
ondículas](#Módulo_de_Reducción_de_Ruido.md)*.

<div>

- <figure>
  <img src="/images/wavelets_gamut_nosky.png" title="wavelets_gamut_nosky.png" />
  <figcaption>wavelets_gamut_nosky.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_sky.png" title="wavelets_gamut_sky.png" />
  <figcaption>wavelets_gamut_sky.png</figcaption>
  </figure>

</div>

### Rango de Tonos de piel

Aunque el título se refiera a *tonos de piel*, aquí puedes ajustar el
rango de los tonos que desees modificar, sean o no tonos de piel. El
rango seleccionado será el que gobernará los cambios realizados por el
resto de controles del módulo. A pesar de todo lo dicho, el rango por
defecto abarca los tonos habituales de piel.

Para los ejemplos que seguirán, se ha escogido el siguiente rango
(bastante restrictivo) de tonos rojos:

<figure>
<img src="/images/wavelets_gamut_skin_hue.png"
title="wavelets_gamut_skin_hue.png" />
<figcaption>wavelets_gamut_skin_hue.png</figcaption>
</figure>

### Protección/Selección del tono de piel

Aquí es dónde decidirás si vas a modificar o no el contraste y/o color
de los detalles que tengan tonos incluídos en el rango anterior:

- con el deslizador en *0* todos los tonos de la imagen se modifican por
  igual
- al seleccionar *-100* (deslizando hacia la izquierda) se centran los
  cambios de contraste y color **en el rango de tonos seleccionado**
- por el contrario, si seleccionas *100* (deslizando a la derecha) se
  modificarán los tonos que **no** coincidan con el rango seleccionado

En las posiciones intermedias entre *0* y *±100* los cambios van siendo
progresivamente más hacia el rango escogido, o hacia el resto de tonos.

<div>

- ![](wavelets_gamut_skin.png "wavelets_gamut_skin.png")\]

- <figure>
  <img src="/images/wavelets_gamut_skin_target0.png"
  title="wavelets_gamut_skin_target0.png" />
  <figcaption>wavelets_gamut_skin_target0.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_skin_target-100.png"
  title="wavelets_gamut_skin_target-100.png" />
  <figcaption>wavelets_gamut_skin_target-100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_skin_target+100.png"
  title="wavelets_gamut_skin_target+100.png" />
  <figcaption>wavelets_gamut_skin_target+100.png</figcaption>
  </figure>

</div>

Como puedes observar los tonos seleccionados no tienen unos límites tan
claros (los «rojos») y normalmente habrá ciertos tonos que serán
modificados tanto en una posición como en la otra, pero aún así, la
separación es bastante clara.

### Curva

Una vez ajustada la *Protección/Selección del tono* deseada, con este
gráfico puedes afinar más exactamente la variación del
contraste/cromaticidad según el tono: si desplazas un punto de control
hacia arriba, aumentarás la variación el efecto para ese tono, mientras
que si lo desplazas hacia abajo mitigarás los cambios para ese tono
(aunque no eliminarás el efecto del todo).

De todas formas, independientemente de los tonos modificados aquí, solo
se tendrán en cuenta los que estén dentro del rango seleccionado antes.

<div>

- <figure>
  <img src="/images/wavelets_gamut_curve_target100.png"
  title="wavelets_gamut_curve_target100.png" />
  <figcaption>wavelets_gamut_curve_target100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_gamut_curve.png" title="wavelets_gamut_curve.png" />
  <figcaption>wavelets_gamut_curve.png</figcaption>
  </figure>

</div>

### Evitar el Cambio de Color

Dado que el procesado por Niveles de Ondícula puede introducir notables
cambios de color (de tono), en especial cerca de los límites del rango
de colores del [espacio de color de
trabajo](Gestion_del_Color#Perfil_de_Trabajo.md) empleado, con
esta opción activada la herramienta realiza una serie de correcciones
para garantizar que los tonos están relacionados con el color inicial.

## Módulo de Viraje por niveles

Este módulo realiza un viraje de los tonos, pero dirigiendo las
modificaciones a niveles concretos de detalles, según tus necesidades.

Sin embargo, la realidad es que no se puede actuar directamente y con
exactitud en el color (matiz) en cada nivel, porque los componentes
*a\** y *b\** se han descompuesto y es muy difícil crear una relación
matemática precisa entre el matiz seleccionado y los componentes
descompuestos.

Aún así, se puede controlar en cierto modo qué tonos que se modificarán
y qué dominantes de color tomarán.

Además, tal y como se utiliza en otros módulos tienes a tu disposición
un deslizador de *Atenuación*, que actuará de la misma forma explicada
en el [capítulo sobre la atenuación del módulo de
Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md).

### Colores que no se modificarán

El gráfico de *Colores excluídos* se basa en una representación de la
distribución de colores a partir de las coordenadas cromáticas del
espacio de color L\*a\*b\*: el eje horizonal representa la componente
a\* (que va del verde al rojo) y el eje vertical representa la
componente b\* (que va del azul al amarillo).

Sin embargo, dado que representar en dos dimensiones la distribución
real de colores del espacio L\*a\*b\* es muy complicado, en la interfaz
este gráfico presenta unos tonos pastel que resultan bastante precisos
matemáticamente, pero no demasiado intuitivos a la vista, especialmente
al seleccionar tonos amarillos. Perceptualmente equivalen a un gráfico
como el siguiente:

<figure>
<img src="/images/Cielab_8x8.png" title="Cielab_8x8.png" />
<figcaption>Cielab_8x8.png</figcaption>
</figure>

En el centro del gráfico tienes un punto blanco que al arrastrarlo deja
ver otro punto negro. Ambos sirven para definir los centros de rangos de
colores que serán protegidos en mayor o menor grado de los virajes de
este módulo. Al situar el punto blanco en un color del gráfico, se
define el centro del primer rango. Al situar el punto negro se define el
centro del segundo rango. Si el punto negro no se mueve del centro,
entonces el segundo rango se ignora.

Con el deslizador *Rango a y b %* se crea una zona de influencia
alrededor del centro definido en el gráfico; zona que será más amplia
cuanto mayor sea el porcentaje establecido.

Con el deslizador *Protección* se disminuye el efecto del módulo sobre
los tonos escogidos (centro más rango), de forma que el valor
seleccionado será el porcentaje de disminución del efecto sobre el
centro de cada rango. A partir del centro, la protección (la disminución
del efecto del módulo) será cada vez menor, hasta llegar en el extremo
del rango (en la periferia de la zona de influencia) a una reducción
equivalente a la mitad del valor establecido.

Por ejemplo: *Protección=80* significa que el centro de cada rango solo
recibirá un 20% del viraje establecido en los ecualizadores del módulo
(explicados a continuación), mientras que a medida que nos alejamos de
los centros y hasta llegar al límite establecido por el *Rango a y b %*,
cada vez el viraje será más intenso, pero llegando únicamente a un 50%
del valor de *Protección*. En este caso sería 40, o sea, que en la
periferia los colores sufrirían un viraje de un 60%.

### Control del viraje

En este grupo de controles se presentan dos curvas:

- la ***Opacidad Rojo-Verde*** (la *curva a\**) actúa sobre los tonos
  rojos-verdes,
- la ***Opacidad Azul-Amarillo*** (la *curva b\**) actúa sobre los tonos
  azules-amarillos.

Pero no olvides que los colores finales de la foto serán una combinación
de los tonos de estas dos curvas. Por ejemplo: si modificas la *curva
a\** (***Opacidad Rojo-Verde*** ) hacia el rojo, todos los tonos del
nivel que estes modificando tomarán un tinte rojo/rojizo, pero no
necesariamente se convertirán en rojos (si también tuvieran una fuerte
componente azul, virarían hacia el magenta/violeta).

Desde un punto de vista práctico: el tono puede incrementar su
saturación, o sufrir una desaturación *hasta cierto punto* y al mismo
tiempo ir cambiando su matiz. Para visualizar mejor estos efectos,
échale un vistazo a esta [vista desde arriba del *espacio de color
L\*a\*b\**](https://upload.wikimedia.org/wikipedia/commons/0/06/CIELAB_color_space_top_view.png),
con *b\** como eje vertical y *a\** como eje horizontal. Y no dejes de
ver esta [vista desde el frente del *espacio de color
L\*a\*b\**](https://upload.wikimedia.org/wikipedia/commons/7/7d/CIELAB_color_space_front_view.png).
La parte inferior de la vista desde arriba coincide con la parte
delantera de la vista de frente.

En la interfaz encontrarás dos *tipos de curva:* *Lineal*
(![](wavelet_toning_linear.png "wavelet_toning_linear.png")) y
*Ecualizada* (![](wavelet_toning_curve.png "wavelet_toning_curve.png")).
Para elegir entre una u otra, deberás desplegar la lista con el pequeño
triángulo de la derecha.

La curva *lineal* sirve para cancelar el efecto del eje al que se
refiere: si la seleccionas en la ***Opacidad Rojo-Verde**'', no
realizarás ninguna acción sobre esos tonos. De forma análoga en
la***Opacidad Azul-Amarillo**''.

En cada curva *ecualizada* tienes un eje horizontal (o eje *x*) y un eje
vertical (o eje *y*):

- el eje *x* representa los 10 niveles posibles, ordenados de izquierda
  a derecha y repartidos uniformemente
- el eje *y* representa la intensidad de la modificación: cuando la
  curva sube por encima o baja por debajo de la línea media la
  cromaticidad se modifica hacia un extremo u otro del eje del
  componente que se esté modificando (*a\** o *b\**)
- en la ***Opacidad Rojo-Verde*** (la *curva a\**), al desplazar la
  curva hacia arriba se introduce un tinte rojizo, mientras que
  desplazarla hacia abajo introduce un tinte verdoso
- en la ***Opacidad Azul-Amarillo*** (la *curva b\**), al desplazar la
  curva hacia arriba se introduce un tinte amarillo, mientras que
  desplazarla hacia abajo introduce un tinte azulado

Por defecto, la curva es plana y se sitúa sobre la línea media. Para
hacerte una idea de cómo puedes interactuar con la curva, repasa las
explicaciones de las *[Curvas
Tonales](Exposure/es#Curvas_Tonales.md)*. Y recuerda que si al
final no te gustan las modificaciones que has realizado en la curva,
siempre puedes volver a empezar haciendo clic en la flecha de reinicio
de la herramienta
![<File:ResetButton.png>](ResetButton.png "File:ResetButton.png").

Siempre que existan previamente variaciones de contraste en el color de
la imagen original, con estas curvas tienes la posibilidad de variar de
forma diferenciada el tono de los detalles deseados, según dónde
coloques los puntos en la curva y la amplitud que tenga la modificación
(es decir, a cuántos niveles afecta). Sin embargo, cabe decir que se
hará todo «a ojo», puesto que no hay referencia de los niveles en el eje
*x* y será más probable que sepas lo que estás modificando mientras
miras en la vista previa que directamente en la curva.

Si utilizas menos de 10 niveles, los puntos que afecten a los niveles
que queden más a la derecha de los que utilices, simplemente se
ignorarán: si estás modificando la imagen con 4 niveles, los 6 de más a
la derecha (los de detalles de mayor tamaño) se ignorarán.

### Ejemplo real (aplicando viraje)

Si lo recuerdas, teníamos unos feos halos azules alrededor de algunas
zonas de la flor, así que vamos a intentar eliminarlos (o al menos
disimularlos) con el viraje. Aprovechamos que la mayor parte de la
imagen tiene una dominante roja y modificaremos la componente azul, sin
que se note demasiado en el resultado global. Para este ejemplo no se ha
excluído ningún color:

<div>

- <figure>
  <img src="/images/wavelet_chrom_Link_50_Str50.png"
  title="wavelet_chrom_Link_50_Str50.png" />
  <figcaption>wavelet_chrom_Link_50_Str50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBYfull.png"
  title="wavelet_toning_opBYfull.png" />
  <figcaption>wavelet_toning_opBYfull.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBYfull_curve.png"
  title="wavelet_toning_opBYfull_curve.png" />
  <figcaption>wavelet_toning_opBYfull_curve.png</figcaption>
  </figure>

</div>
<div>

- <figure>
  <img src="/images/wavelet_toning_opBY.png" title="wavelet_toning_opBY.png" />
  <figcaption>wavelet_toning_opBY.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBY_Str50.png"
  title="wavelet_toning_opBY_Str50.png" />
  <figcaption>wavelet_toning_opBY_Str50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_toning_opBY_curve.png"
  title="wavelet_toning_opBY_curve.png" />
  <figcaption>wavelet_toning_opBY_curve.png</figcaption>
  </figure>

</div>

Al final siguen quedando algunos restos de halos azules, pero más
disimulados, mientras que el aspecto general de la foto parece no haber
cambiado.

## Módulo de Reducción de Ruido

Este módulo viene a completar a la herramienta general de **[Reducción
de Ruido](Noise_Reduction/es.md)** (de la *pestaña Detalle*) y a
la **Nitidez de Bordes** (explicada en el siguiente apartado).

La gestión del ruido es un asunto complejo, ya que ¿dónde debe
realizarse? ¿Al principio del procesado o al final? ¿Sobre qué se debe
actuar y cómo hacerlo adecuadamente? En RawTherapee la reducción general
del ruido se sitúa al principio del procesado, para evitar que las
diferentes herramientas lo realcen a niveles inasumibles (es decir, para
mantener el ruido en niveles *soportables*). En la herramienta general
tienes las siguientes posibilidades:

- tratar la luminancia (con ondículas) como un bloque, es decir, sin
  diferencia entre los niveles de ondícula.
- procesar el ruido de color mediante un tratamiento diferente: ésto
  generalmente requiere un mayor número de niveles de ondícula (de 4
  a 7) y un procesamiento más complejo.
- añadir un tratamiento mediante *Transformada de Fourier* para refinar
  la luminosidad
- añadir una mediana

Aunque ésto pueda ser suficiente, la herramienta de Niveles de Ondícula
tiene las siguientes ventajas (a pesar de que emplea el mismo algoritmo
que la herramienta general):

- se encuentra al final del circuito de procesado, reduciendo así el
  impacto del ruido añadido por otras herramientas generales
  (*Exposición*, *Curvas*, ajuste de *Gama*, ...)
- actúa de forma separada e independiente en cada uno de los 4 primeros
  niveles, mientras que la reducción de ruido *estándar* tiene efecto
  sobre toda la imagen a la vez. Ésto es especialmente útil en imágenes
  de bajo ruido y en imágenes en las que con la heramienta general se ha
  hecho deliberadamente una reducción de ruido poco agresiva para
  preservar los detalles (es decir, reduciendo algo el ruido, pero no
  completamente)
- permite la reducción de la incidencia del ruido en el resto del
  procesado por niveles de ondícula, por ejemplo para procesar los
  cielos sin exagerar el ruido
- ajusta tanto el procesado del ruido como el grado de
  amplificación/reducción del contraste en cada nivel, útil por ejemplo
  para imágenes astronómicas

### Los controles

La reducción de ruido por niveles podrás ajustarla a tus necesidades con
el siguiente bloque de controles, con los que además de decidir sobre
qué ruido actuar, podrás vincular su efecto al módulo de *Nitidez de
Bordes* y a la reducción de ruido de color.

#### Enlazar con la Intensidad de la Nitidez de Bordes

Esta opción va a modificar el comportamiento del deslizador inferior de
cada nivel (explicado más abajo).

- si decides **no activarla**, el deslizador inferior de cada nivel (el
  de la **Intensidad**) tiene un efecto similar a los del módulo de
  Contraste cuando utilizas el *Rango completo de luminancias*
- si por el contrario sí que la activas, con el deslizador inferior
  podrás cambiar la distribución de la mejora de nitidez en los primeros
  niveles (ésto se explica con más detalle en el siguiente módulo, el de
  *Nitidez de Bordes*)

#### Nivelador de Reducción de Ruido Blanco-Negro

La visión humana es capaz de distinguir el ruido más fácilmente en zonas
claras que en zonas oscuras, a pesar de que con mediciones objetivas
haya más cantidad de ruido en las zonas oscuras (las sombras).

Mediante este deslizador, la reducción de ruido se intensifica más en
las sombras (con valores hacia la derecha) o en las luces (con valores
hacia la izquierda).

Para poder ajustar mejor el efecto es conveniente que escojas una zona
con areas claras y oscuras, de manera que puedas diferenciar el cambio
en ambos extremos.

#### Reducción de ruido e Intensidad

Estos deslizadores sirven para controlar el ruido en los 4 niveles con
detalles más finos de la imagen:

- el deslizador superior de cada nivel es el que realiza la **Reducción
  de ruido**
- el inferior, llamado **Intensidad**, modifica el contraste de los
  detalles del nivel, aunque no de una manera tan sofisticada como los
  deslizadores del módulo de Contraste

A pesar de que el deslizador de *Intensidad* pueda parecer superfluo o
duplicado, resulta bastante útil para recuperar el contraste que pierden
los detalles cuando se va aumentando la *Reducción de ruido*. De esta
forma no hace falta que saltes de un módulo a otro para ajustar
rápidamente la imagen. Además, recuerda que también sirve para modular
la distribución del efecto en los 4 primeros niveles de la *Nitidez de
Bordes*.

#### Reducción de ruido de color

Dentro de la herramienta *Reducción de Ruido* ya se realiza una
reducción global del ruido de color, así que ¿para qué puede servir lo
mismo dentro de la herramienta de *Niveles de Ondícula*?

Recordemos que esta herramienta está al final del circuito de procesado,
por lo que la reducción de ruido de color en este punto es muy útil para
eliminar los posibles restos que no se hayan eliminado al principio, o
el ruido que se haya generado en otras herramientas.

En este grupo de deslizadores encontrarás:

- el **Nivelador de Reducción de ruido Azul-Rojo**: el ruido de color
  suele presentarse en forma de puntos de color rojo o azul y con este
  deslizador puedes incrementar la reducción de los puntos azules (hacia
  la izquierda), o de los puntos rojos (hacia la derecha)
- el control deslizante **Color fino**: aquí reduciremos el ruido de
  color en los detalles más finos, es decir, en los niveles más bajos
- el control deslizante **Color grueso**: en este caso la reducción de
  ruido de color se realiza en los detalles más grandes, o sea, en los
  niveles altos. Este ruido se puede ver como areas de color que
  «ensucian» o «que no corresponden» a la imagen y que no se pueden
  eliminar con el anterior control deslizante precisamente por su tamaño

### Ejemplo real (reduciendo el ruido)

Para comprender mejor cuánto se puede mejorar el nivel de ruido, es
conveniente que lo estudies nivel por nivel, aprovechando que puedes ver
los detalles sobre un fondo neutro (como se explicó al tratar la *[Vista
previa](#Vista_previa.md)*). Para éllo puedes desactivar
*Enlazar con la Intensidad de la Nitidez de Bordes* y después
incrementar al máximo la intensidad del nivel que estés estudiando: el
ruido presente se hará muy evidente y podrás valorar cuánta reducción
necesitarás. Una vez tengas ajustada la reducción del ruido, mueve la
*Intensidad* al valor que mejor te convenga (incluso valores negativos)
y pasa al siguiente nivel.

<div>

- <figure>
  <img src="/images/wavelet_denoise_orig.png" title="wavelet_denoise_orig.png" />
  <figcaption>wavelet_denoise_orig.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d00s100.png"
  title="wavelet_denoise_L2d00s100.png" />
  <figcaption>wavelet_denoise_L2d00s100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d30s100.png"
  title="wavelet_denoise_L2d30s100.png" />
  <figcaption>wavelet_denoise_L2d30s100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L2d30s27.png"
  title="wavelet_denoise_L2d30s27.png" />
  <figcaption>wavelet_denoise_L2d30s27.png</figcaption>
  </figure>

</div>
<div>

- <figure>
  <img src="/images/wavelet_denoise_L1d00s00.png"
  title="wavelet_denoise_L1d00s00.png" />
  <figcaption>wavelet_denoise_L1d00s00.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d00s100.png"
  title="wavelet_denoise_L1d00s100.png" />
  <figcaption>wavelet_denoise_L1d00s100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d12s100.png"
  title="wavelet_denoise_L1d12s100.png" />
  <figcaption>wavelet_denoise_L1d12s100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_L1d12s-17.png"
  title="wavelet_denoise_L1d12s-17.png" />
  <figcaption>wavelet_denoise_L1d12s-17.png</figcaption>
  </figure>

</div>
<div>

- <figure>
  <img src="/images/wavelet_denoise_orig.png" title="wavelet_denoise_orig.png" />
  <figcaption>wavelet_denoise_orig.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_final.png"
  title="wavelet_denoise_final.png" />
  <figcaption>wavelet_denoise_final.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_orig100.png"
  title="wavelet_denoise_orig100.png" />
  <figcaption>wavelet_denoise_orig100.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_denoise_final100.png"
  title="wavelet_denoise_final100.png" />
  <figcaption>wavelet_denoise_final100.png</figcaption>
  </figure>

</div>

En general es interesante que no elimines completamente el ruido, sinó
que lo lleves a niveles bajos (contrastes bajos) para que sea apenas
visible y al mismo tiempo aumentar el contraste de los detalles del
nivel: amplificando la presencia de los detalles, cuando se vea la
imagen el ruido se ignorará, pero ayudará a rellenar la foto con una
textura ligera. El procedimiento sería como sigue:

1.  reduce el ruido de luminancia en la herramienta general: tan solo
    una ligera reducción, cuidando especialmente que no se pierda ningún
    detalle
2.  selecciona *un nivel*, *fondo gris* y el *nivel 1*
3.  haz zoom al 300-400% en una zona con fondo poco detallado (deben
    apreciarse detalles con buen contraste, pero no ser demasiados para
    no enmascarar el ruido)
4.  lleva la *intensidad del nivel 1* en la *reducción de ruido* hasta
    el máximo (o casi), sin perder de vista lo que son los detalles en
    lugar de ruido
5.  lleva el deslizador superior hasta un punto en que el contraste del
    ruido sea medio-bajo (no lo elimines completamente)
6.  tras la reducción de ruido los detalles habrán perdido algo de
    contraste: devuelve el deslizador inferior a un nivel de intensidad
    que recupere el contraste inicial de los detalles
7.  cambia al *nivel 2* y continúa con los puntos 4, 5 y 6, pero
    ajustando la *intensidad del nivel 2*
8.  continúa de la misma forma con los niveles *3* y *4*
9.  termina seleccionando *Todos los niveles en todas direcciones*

Si la imagen fuese poco ruidosa, puedes pasar directamente al punto 2.
En cambio si se trata de una imagen con mucho ruido es casi
imprescindible que en el punto 1 ajustes perfectamente la reducción de
ruido de luminancia: deberás jugar con el deslizador de luminancia y con
el de la *Gama*, para dirijir la reducción de ruido a las sombras o a
las luces. Cuanto mejor ajustes este paso, mejor se comportará la
reducción de ruido de las ondículas.

Para aumentar la presencia de los detalles puedes emplear los
deslizadores inferiores y aumentar la intensidad de cada nivel hasta
donde desees, pero es más recomendable emplear los controles del módulo
de Contraste, ya que ofrecen mucho más control y unos mejores resultados
con menos artefactos. Además, no olvides que en este ejemplo sólo se han
empleado los deslizadores de *Reducción de ruido* y de *Intensidad*,
pero si fuese necesario aún se podría afinar más el resultado con el
resto de deslizadores de este módulo.

No confundas esta reducción del ruido con la función **Umbral bajo
(ruido)** en la **Detección de Bordes** del siguiente módulo, que tiene
en cuenta el ruido (sin reducirlo), para no resaltarlo mientras se
analizan los bordes.

## Módulo de Nitidez de Bordes

Este módulo realiza un tipo de detección de contornos basado en los
detalles de cada nivel de ondícula.

A primera vista se parece a la **[Máscara de
Desenfoque](Sharpening/es#Máscara_de_Desenfoque.md)**, dado que
la descomposición por niveles de ondícula genera una *imagen residual*
que podría asemejarse a una máscara, pero ahí se acaban las similitudes.

Si deseas obtener resultados parecidos a la *Máscara de Desenfoque* o a
la
*[Deconvolución](https://es.wikipedia.org/wiki/Deconvolución#Óptica)*,
es casi obligatorio que selecciones la casilla *Detección de bordes* y
elijas un valor alto de *Sensibilidad de gradiente* (70 o más; por
defecto será 90). Además, es mejor no modificar los primeros niveles de
contraste en *Contraste por Niveles de Detalle*, ya que dificultarían el
buen funcionamiento del algoritmo (todas estas opciones se explican con
detalle a continuación).

Antes de explicar cómo usar el módulo y para evitar generar artefactos o
efectos excesivamente intensos, no olvides que tanto la configuración
del *[Comportamiento de los bordes (D2, D4 ...
D14)](#Comportamiento_de_los_bordes.md)* como la [intensidad de
cada nivel en la *Reducción de ruido*](#Reducción_de_ruido.md)
(cuando tienes activado *Enlazar con la Intensidad de la Nitidez de
Bordes*) tienen un efecto muy notable en la *Detección de Bordes*.
Deberás ajustar, valorar el resultado y reajustarlo todo en conjunto
para obtener una buena nitidez con el mínimo de artefactos.

En la interfaz tienes varios bloques de controles:

- la ***configuración***: este primer bloque te permite ajustar cómo
  intensifica los bordes la herramienta
- el ***contraste local***: en este bloque se decide cómo se aplican los
  cambios de contraste en los detalles, según la intensidad del
  contraste de cada detalle
- la ***detección de bordes***: para aumentar la nitidez en dónde más se
  necesita (es decir, en los bordes)

### Configuración

***Por el momento la*Detección de Bordes*permanecerá desactivada en todo
momento, ya que los resultados son distintos si se activa esa opción.***

Aquí tienes 4 controles deslizantes:

1.  **Intensidad**: es cuánto potencia la herramienta el contraste de
    los detalles. Su efecto es más enérgico en los niveles bajos y
    además, cuanto mayor sea el valor de la *Intensidad*, mayor será el
    cambio de contraste. La puesta a cero de este control deslizante
    anula cualquier modificación en el resto del módulo.
2.  **Atenuación**: de la misma forma que en el [capítulo sobre la
    atenuación del módulo de
    Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md),
    controla qué contrastes se intensificarán más o menos.
3.  **Radio**: genera una impresión de imagen tridimensional. La
    impresión podrá ser de más *volumen* en los detalles, o de una
    *textura* más pronunciada. Su acción no es nula si el cursor está en
    cero. Además, el efecto del *Radio* se ve modificado por el valor
    del *Detalle*.
4.  **Detalle**: hace que el contraste se distribuya de distintas formas
    entre los niveles. El efecto será más intenso en los 3 primeros
    niveles si el cursor se mueve a la derecha, mientras que si lo
    mueves a la izquierda (hacia valores negativos), prácticamente se
    anulará el cambio de contraste en esos 3 primeros niveles.

Puesto que los cambios en el contraste de cada nivel están íntimamente
relacionados con los valores del *Radio* y del *Detalle* y que los
efectos del *Radio* se modifican según el valor del *Detalle*, veamos
con detenimiento qué ocurre. Para éllo tendremos el *Primer nivel: Sin
Cambios* (que se explicará después) y *Enlazar con la Intensidad de la
Nitidez de Bordes* desactivada (que se encuentra en el módulo de
*Reducción de Ruido*).

- **la relación Radio-Contraste**: al modificar el valor del *Radio* se
  modifica el contraste de los detalles. En general, la mayor intensidad
  global de los cambios de contraste se observan entre los radios 40
  y 75. Por debajo de 40 se potencia el nivel 1 y por encima de 75 el
  nivel 3 y en menor medida los superiores (el efecto va siendo cada vez
  más suave y en los niveles *9* y *Extra* el efecto es inapreciable).
- **la relación Radio-Detalle**: dependiendo del valor que tenga
  *Detalle*, al modificar el *Radio* se intensifica más o menos el
  contraste de los detalles de unos niveles u otros.

  
Se entenderá mejor gráficamente:

<div>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_D-50.png"
  title="Wavelet_edge_sharpening_D-50.png" />
  <figcaption>Wavelet_edge_sharpening_D-50.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_unchanged.png"
  title="Wavelet_edge_sharpening_unchanged.png" />
  <figcaption>Wavelet_edge_sharpening_unchanged.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Wavelet_edge_sharpening_D100.png"
  title="Wavelet_edge_sharpening_D100.png" />
  <figcaption>Wavelet_edge_sharpening_D100.png</figcaption>
  </figure>

</div>

Justo debajo del control del *Detalle*, tienes una lista desplegable con
3 opciones para el **Primer nivel** de ondícula:

- *Intensificado*: se incrementa el efecto en el *nivel 1*.
- *Sin cambios*: la distribución del algoritmo no se modifica.
- *Reducido*: el *nivel 1* se modifica con menor intensidad.

Que aprecies o no diferencias entre estas tres opciones dependerá de la
cantidad de detalles finos de la imagen, lo contrastados que estén esos
detalles y los coeficientes empleados en la descomposición (*D2*, *D4*,
..., *D14*): en fotos nocturnas con puntos de luz sobreexpuestos
(farolas, ...) la opción *Reducido* suaviza el ruido muy contrastado del
primer nivel; pero en muchas ocasiones verás que el *nivel 1* apenas
contiene detalles relevantes, por lo que casi dará igual qué opción
escojas.

Además, si utilizas la opción *Reducido*, podrás observar un
comportamiento algo extraño para el *nivel 1*, o al menos «diferente»:
el contraste disminuye progresivamente desde un máximo en *Radio: 0*
hasta un difuminado casi total de los detalles en *Radio: 19*, para
saltar de golpe a otro máximo en *Radio: 20*. Después vuelve a ir
difuminándose lentamente hasta llegar a *Radio:100*. Gráficamente:

<figure>
<img src="/images/Wavelet_edge_sharpening_reduced.png"
title="Wavelet_edge_sharpening_reduced.png" />
<figcaption>Wavelet_edge_sharpening_reduced.png</figcaption>
</figure>

De todas formas, lo más recomendable será escoger *Sin Cambios*, porque
de esta forma al **Enlazar con la Intensidad de la Nitidez de Bordes**
los cambios serán más progresivos y controlables.

### Enlazar con la Intensidad de la Nitidez de Bordes

Todo lo anterior es válido mientras NO actives la opción *Enlazar con la
Intensidad de la Nitidez de Bordes* (de la *Reducción de Ruido*). En
este caso se realizarán cambios de contraste en función de los valores
de *Radio* y *Detalle*.

En cambio, si has activado la opción *Enlazar con la Intensidad de la
Nitidez de Bordes*, las intensidades de cada nivel de la *Reducción de
Ruido* serán las que regulen la intensidad del efecto en cada uno de los
cuatro primeros niveles de la *Nitidez de Bordes*. Gracias a ésto puedes
ajustar el aumento de nitidez sólo para determinados niveles y con
valores de incremento de contraste significativamente más altos que los
obtenidos con los 10 deslizadores de *Contraste*.

Por ejemplo, podrás:

- dejar sin cambios de contraste el *nivel 1*
- incrementar la intensidad máxima en el *nivel 2*
- reducir el contraste en el *nivel 4* (*Intensidad* negativa)

### Contraste local

Para cada nivel de descomposición, la herramienta calcula la
[media](https://es.wikipedia.org/wiki/Media_(matemáticas)) y la
[desviación típica](https://es.wikipedia.org/wiki/Desviación_típica) del
contraste interno (también llamado *contraste local*) de los detalles,
utilizando los resultados para modificarlo.

Recuerda que un «detalle» es en realidad un grupo de píxeles de la
imagen original, siendo más grande el grupo cuanto más alto es el nivel
(en el *nivel 1* es un grupo de 2x2=4 píxeles, en el *nivel 2* es un
grupo de 4x4=16 píxeles, etc). Como cada píxel tiene una luminancia
inicial distinta del resto de píxeles del detalle, se genera un
contraste interno entre píxeles que es analizado por la herramienta.

La modificación de estos contrastes internos o locales sigue un patrón
basado en la media de los contrastes del nivel y su desviación típica y
este patrón se aplica por igual en todos los niveles, sin importar si
los detalles de cada nivel tienen o no el mismo valor de contraste
medio.

Así pues, por ejemplo puedes:

- para los valores iniciales bajos de contraste (normalmente localizados
  en las sombras): reducir el contraste local para suavizar la
  apariencia de los detalles
- para los valores medios: aumentar el contraste local para realzarlos
- para los valores altos (normalmente localizados en las zonas con mucha
  luminosidad): reducir o incluso cancelar el contraste local, para
  evitar *quemar* las luces

Para realizar los ajustes puedes elegir entre 2 métodos gráficos:

1.  un gráfico en blanco y negro con cuatro puntos ajustables que
    representan (de izquierda a derecha) el contraste mínimo, la media,
    la media + la desviación típica y el contraste máximo.
2.  una curva, que por defecto es una curva de tipo gaussiano asimétrico
    y con las siguientes características:
    - el centro de la
      [abscisa](https://es.wikipedia.org/wiki/Coordenadas_cartesianas)
      corresponde al valor medio de los contrastes
    - desde el centro y a un tercio del ancho del gráfico a cada lado se
      encuentran los detalles con contrastes más altos y más bajos que
      la media, pero dentro del rango de valores establecido por la
      desviación típica

***LA CURVA CON CONTROLES DESLIZANTES***

<div class="parrpad">

<figure>
<img src="/images/wavelet_local_contrast_thresholds.png"
title="wavelet_local_contrast_thresholds.png" />
<figcaption>wavelet_local_contrast_thresholds.png</figcaption>
</figure>

</div>

Si escoges los puntos deslizantes, el fondo representa que mover un
punto a la derecha aumentará su contraste, mientras que moverlo a la
izquierda lo disminuirá (cuanto más blanco es el color del fondo, mayor
es el contraste, mientras que un fondo oscuro indica un contraste bajo).

Teniendo en cuenta que los puntos representan de izquierda a derecha el
contraste mínimo, la media, la media + la desviación típica y el
contraste máximo, por ejemplo, mover a la derecha el punto que
representa la media de los contrastes implicará que se aumentará el
contraste de los valores cercanos a la media. Y de igual forma ocurre en
el resto de puntos, es decir, la herramienta modifica cada grupo de
contrastes (media, desviación típica, mínimo y máximo) según los
desplazamientos de los puntos ajustables.

En la práctica:

- en general, con los valores por defecto el efecto con los deslizadores
  es más *natural* (o más *habitual*) a costa de brillos exagerados,
  especialmente los brillos especulares. Sin embargo, los detalles se
  realzan más naturalmente y con mayor definición que con la curva, sin
  resaltar en exceso el ruido o el grano
- en fotos diurnas con tonos medios (como en paisajes urbanos) resaltan
  los detalles sin forzar el contraste en las luces (pero marcando más
  los reflejos)
- sin embargo, en fotos con mucho contraste (fotos nocturnas con
  iluminación artificial, fotografía astronómica) tienen tendencia a
  exagerar los contrastes de los puntos de luz
- en fotos con mucho contraste (con mucho ruido contrastado), si has
  seleccionado *primer nivel: reducido* el efecto en el *nivel 1*
  disminuye y el ruido se suaviza bastante. Sin embargo, en fotos con
  contrastes moderados prácticamente no hay diferencias

***LA CURVA GAUSIANA***

<div class="parrpad">

<figure>
<img src="/images/wavelet_local_contrast_gauss.png"
title="wavelet_local_contrast_gauss.png" />
<figcaption>wavelet_local_contrast_gauss.png</figcaption>
</figure>

</div>

En este caso la forma de la curva te orienta sobre cómo se modificarán
los contrastes de los detalles. Recuerda que la desviación típica de los
contrastes se encuentran a un tercio a derecha e izquierda del centro
del gráfico.

Además, este gráfico es más completo, pues te permite modificar tanto
los contrastes locales afectados, como la intensidad del cambio: si
mueves un punto de la curva a derecha o izquierda, cambiarás los
contrastes afectados (como con los puntos deslizantes), mientras que
arriba o abajo aumenta o disminuye la intensidad de las modificaciones
en los detalles.

Con la forma por defecto de la curva (que puedes reiniciar con el botón
![<File:ResetButton.png>](ResetButton.png "File:ResetButton.png")) el
efecto conseguido es parecido a un
[HIRALOAM](https://fotografodigital.com/tutoriales-photoshop/tutorial-tecnica-de-super-enfoque/):
potencia los contrastes controlando las sombras, mientras que los
contrastes fuertes los resalta menos. Es como resaltar el volumen de
cada detalle, manteniendo controlados tanto el ruido en las sombras como
la sobreexposición en las luces y especialmente en los brillos
especulares. Sin embargo, el grano y el ruido de los contrastes medios
se resaltan excesivamente.

Si utilizas los valores por defecto en ambas curvas, según el resultado
que quieras lograr es mejor la curva que los deslizadores, o viceversa.
Pero al usar la curva, la *Intensidad* de la herramienta deberá ser baja
para no obtener resultados excesivos. Con los deslizadores puedes subir
bastante más la intensidad con resultados más *naturales*. De todas
formas, ajustando la curva puedes conseguir el mismo efecto que con los
deslizadores, con la ventaja añadida de poder variar los contrastes
incluso suavizándolos (con la curva por debajo de la línea horizontal).

<div>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_o.png"
  title="wavelet_local_contrast_curves_o.png" />
  <figcaption>wavelet_local_contrast_curves_o.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_t.png"
  title="wavelet_local_contrast_curves_t.png" />
  <figcaption>wavelet_local_contrast_curves_t.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_local_contrast_curves_g.png"
  title="wavelet_local_contrast_curves_g.png" />
  <figcaption>wavelet_local_contrast_curves_g.png</figcaption>
  </figure>

</div>

### Detección de bordes

Antes de comenzar a utilizar esta parte del módulo es necesario que
ajustes bien los parámetros anteriores, especialmente el contraste
local. Deberás actuar con sutileza, ya que es fácil generar efectos
exagerados y artefactos en la imagen.

Al activar la detección de bordes, el resultado obtenido será diferente
a los de los algoritmos tradicionales (máscara de desenfoque,
deconvolución...), pues la herramienta realiza una serie de operaciones
con los detalles de cada nivel de manera que se resalten los bordes sin
realzar el ruido. Para éllo intensifica los detalles de la
descomposición, los difumina para eliminar el ruido y selecciona
aquellos que pueden formar parte de un borde.

El proceso se basa en el algoritmo de Sobel-Canny, aunque personalizando
los cálculos para adecuarlos a los componentes de la descomposición y
reduciendo las variables necesarias a 3 deslizadores:

- **Sensibilidad de gradiente**: cuanto más muevas el cursor a la
  derecha, más se centrará el algoritmo de detección en los bordes
  nítidos y menos tendrá en cuenta el contraste local de las zonas
  pequeñas (como el ruido o los pequeños detalles). Por el contrario, si
  llevas el cursor a la izquierda se detectarán mejor todos los bordes,
  hasta los más pequeños, pero también se resaltará el ruido.
- **Umbral bajo (ruido)**: este control deslizante configura un [filtro
  gaussiano](https://es.wikipedia.org/wiki/Desenfoque_gaussiano) que no
  modifica directamente la imagen, sinó los coeficientes de la
  descomposición. A la izquierda actúa sobre una matriz de 3x3, mientras
  que a la derecha sobre una matriz más grande de 5x5. Al difuminar la
  imagen, tanto el ruido como los detalles más finos o con menor
  contraste se pierden o disimulan. Esto es bueno para mitigar el ruido,
  pero también provoca un menor acierto a la hora de detectar bordes.
  Cuanto más a la derecha esté el cursor mejor se mitigará el ruido,
  pero se detectarán menos bordes. Un valor alrededor de 3x3 es mejor
  para detectar líneas pequeñas, pero es más propenso a la contaminación
  por ruido. Un valor de 5x5 es mejor para bordes más amplios o más
  destacados, a costa de perder líneas pequeñas y que la detección sea
  más imprecisa.

  
Además, en un paso posterior del algoritmo, con este umbral se
eliminarán aquellos bordes que, aunque se hayan detectado, es poco
probable que sean realmente bordes. Cuanto más bajo sea este umbral, más
cantidad de bordes con contraste bajo se detectarán, pero también se
considerará más cantidad de ruido como probable borde.

- **Umbral alto (detección)**: una vez ya se han detectado los bordes de
  la imagen, con este control deslizante la herramienta analiza con qué
  fiabilidad se ha detectado cada borde (borde nítido o borde
  difuminado) y aplica una atenuación o intensificación en el cambio de
  contraste local dependiendo de lo nítido que sea el borde. Así pues,
  cuanto más a la derecha se sitúe el cursor, más se intensifica el
  cambio de contraste de los bordes nítidos, mientras que cuanto más a
  la izquierda, más se atenuarán los contrastes.

### Algoritmo mejorado

Al activar esta parte del módulo tendrás acceso a la configuración de
algunas partes del algoritmo de detección de bordes:

- Sensibilidad de borde: este valor permite descartar los detalles que
  no tengan un contraste mayor al establecido aquí. Cuanto más a la
  derecha, más contrastado debe ser el detalle para considerarlo como
  posible borde (y los bordes con poco contraste serán ignorados).
- Amplificación de base: con este control deslizante se intensifican los
  valores iniciales antes de comenzar los cálculos de forma que se
  puedan detectar mejor los bordes. Cuanto más a la derecha se sitúe,
  mejor será la distinción entre *borde* y *no borde*, pero mayor será
  el riesgo de que se produzcan artefactos.
- Píxeles vecinos: aquí decides qué influencia tienen en la detección de
  bordes los píxeles alrededor del detalle. Tienes 3 opciones:
  *ninguna*, *baja*, *alta*.

### Ejemplo real (modificando reducción de ruido y nitidez de bordes)

<div>

- 

<figure>
<img src="/images/wavelet_edge_sharpness.png"
title="wavelet_edge_sharpness.png" />
<figcaption>wavelet_edge_sharpness.png</figcaption>
</figure>

</li>
</ul>
</div>

## Difuminar niveles

Este módulo te permite difuminar («desenfocar») selectivamente los
detalles de los niveles que desees, aunque los resultados son más
adecuados en los niveles altos (del *nivel 7* hacia arriba). Es
especialmente útil en astrofotografía.

El deslizador de ***Atenuación*** actúa de la misma forma explicada en
el [capítulo sobre la atenuación del módulo de
Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md).

La curva para ***Difuminar por niveles*** modifica la luminancia de cada
nivel: se divide en 10 zonas, con el *nivel 1* a la izquierda y el
*Extra* a la derecha. Cuanto más alta esté la curva en la zona de un
nivel, más se desdibujarán los detalles en ese nivel.

El deslizador para ***Difuminar color*** funde los colores con sus
alrededores, creando manchas tenues. Su efecto se localiza en los mismos
niveles establecidos con la anterior curva.

## Módulo de Máscara de Nitidez y de Claridad

La función **Máscara de Nitidez** es una nueva forma de tratar la mejora
de la nitidez ya presente en RawTherapee (*Máscara de desenfoque*,
*Deconvolución* y *Nitidez de bordes en los Niveles de ondículas*), que
puede o no combinarse con estos otros tres métodos.

Tradicionalmente el método más empleado para acentuar los bordes y
aumentar la sensación de nitidez de las imágenes es la *Máscara de
desenfoque*: consiste en elaborar una máscara difusa de tipo Gaussiano
(para cada píxel y de forma recursiva se desdibujan los píxeles vecinos)
que luego se resta de la imagen original, lo que aporta un énfasis. En
esa herramienta los radios utilizados suelen ser pequeños (del orden de
menos de 1 a unos pocos píxeles).

Sin embargo en este módulo se utiliza una máscara que corresponde a una
parte de la descomposición de la ondícula. Esta máscara puede usarse de
dos formas:

- privilegiando los niveles más bajos mediante la **Máscara de
  nitidez**.
- favoreciendo los niveles altos mediante la **Claridad**, que
  incrementa la impresión de contraste local y la saturación local de la
  imagen.

Cuando activas el módulo la configuración general de la herramienta
cambiará automáticamente a:

|          | Máscara de nitidez         | Claridad                     |
|----------|----------------------------|------------------------------|
| Fondo:   | Imagen Residual            | Imagen Residual              |
| Niveles: | Niveles con detalles finos | Niveles con detalles grandes |
| Nivel:   | 3                          | 7                            |

En cualquiera de los dos casos podrás cambiar el *nivel* de referencia.
En el caso de la *Máscara de nitidez* el cambio del nivel se asemeja a
modificar el radio en la *Máscara de desenfoque* y puedes escoger
cualquier nivel entre el *1* y el *4*. Para la *Claridad* un cambio de
nivel implica un mayor o menor efecto de *volumen tridimensional* en la
imagen. En este caso puedes seleccionar los niveles del *5* al *Extra*.

Cuando desactivas el módulo los valores que hayas modificado no se
pierden (excepto el *Nivel*) y solo tendrás que volver a seleccionar el
nivel deseado al activarlo de nuevo.

La *combinación* en la *Máscara de nitidez* consiste en realzar los
detalles por debajo del nivel seleccionado y mezclar (combinar) el
resultado con los niveles restantes: si has seleccionado el *nivel 3*,
se resaltarán los detalles de los niveles *1*, *2* y *3* para después
combinarlos con los niveles 4 y superiores (incluyendo la imagen
residual). El deslizador de la combinación permite ajustar la mezcla
dando más o menos relevancia a los detalles resaltados respecto al resto
de la imagen.

De forma análoga, en el caso de la *Claridad* se resaltan los niveles
superiores y se combinan con el resto de la foto.

En ambos casos dispones de 3 controles deslizantes para ajustar los
cambios:

1.  **Combinar Luminosidad**: moviéndolo hacia la derecha (valores
    positivos) se realza el contraste de los detalles, mientras que con
    valores negativos la imagen se vuelve *borrosa, como de ensueño*.
2.  **Combinar Cromaticidad**: moviéndolo hacia la derecha (valores
    positivos) se realzan los tonos saturados, mientras que los tonos
    menos saturados (más pastel) se realzan menos. Con valores
    negativos, la imagen se vuelve menos vívida, mientras que los tonos
    pastel prácticamente no varían.
3.  **Radio de suavizado**: con valores de combinación elevados suelen
    aparecer halos alrededor de las zonas contrastadas. Con este control
    los puedes suavizar sin afectar demasiado a la imagen. Sin embargo
    tiene efectos secundarios: las zonas oscuras se vuelven más oscuras
    y cada vez más zonas se considerará que no tienen suficiente
    contraste para ser realzadas, por lo que permanecen sin modificar.

<div>

- ![](wavelet_smc_original.png "wavelet_smc_original.png")\]

- <figure>
  <img src="/images/wavelet_sharpm_ML60MC30.png"
  title="wavelet_sharpm_ML60MC30.png" />
  <figcaption>wavelet_sharpm_ML60MC30.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelet_clarity_ML60MC30.png"
  title="wavelet_clarity_ML60MC30.png" />
  <figcaption>wavelet_clarity_ML60MC30.png</figcaption>
  </figure>

</div>

Por último, debajo del *Radio de suavizado* tienes la opción de
**Mostrar la «máscara» de ondícula**, con la que podrás ver qué detalles
serán los que se realzarán:

- en el caso de la *Máscara de nitidez* se mostrará una imagen con fondo
  negro y los detalles que se resaltarán en blanco (si alguna vez has
  visto la máscara de una *Máscara de desenfoque*, la encontrarás
  bastante similar).
- sin embargo, con la *Claridad* nos encontraremos con un tipo de
  máscara diferente, basada en un [Guided Image
  Filtering](http://kaiminghe.com/eccv10/)
  <span style="font-size: 0.7em; font-style: italic;">(enlace a
  documento en inglés)</span> y con un aspecto poco intuitivo. A modo
  general, las zonas blancas (aunque difuminadas) son las que se
  resaltarán.

## Módulo de la Imagen Residual

Como recordatorio, la imagen residual corresponde a la diferencia entre
la imagen original y el conjunto de todos los detalles de los niveles
(las modificaciones realizadas en cada nivel no tienen efecto sobre la
imagen residual). Es decir, cuantos más niveles selecciones en la
configuración general de la herramienta, mayor será la diferencia entre
la imagen original y la residual. Además, cuando seleccionas más de 6
niveles casi se puede decir que la imagen residual está libre de ruido,
por lo que cambiar el contraste (global) o la cromaticidad de esta
imagen no tendrá casi ningún efecto sobre el ruido.

<div>

- ![](wavelets_residual_original.png "wavelets_residual_original.png")\]

- <figure>
  <img src="/images/wavelets_residual_L5.png" title="wavelets_residual_L5.png" />
  <figcaption>wavelets_residual_L5.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_L7.png" title="wavelets_residual_L7.png" />
  <figcaption>wavelets_residual_L7.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_L8.png" title="wavelets_residual_L8.png" />
  <figcaption>wavelets_residual_L8.png</figcaption>
  </figure>

</div>

Es importante tener en cuenta que si quieres evitar artefactos y tonos
fuera de la [gama de
colores](https://es.wikipedia.org/wiki/Gama_de_color) (el «gamut»),
debes controlar los cambios realizados en todos los niveles así como en
la imagen residual: si la imagen original ya tiene tonos cercanos a los
límites del espacio de color, el aumento significativo del contraste o
de la cromaticidad de los detalles resultará casi inevitablemente en
artefactos o tonos que se saldrán del rango de colores. En estos casos,
jugar con la imagen residual aumentando o disminuyendo su contraste y su
cromaticidad te permitirá mantener los colores dentro del rango definido
por el espacio de color.

Como puedes ver, modificar la imagen residual es un aspecto fundamental
del procesado por niveles de ondícula. Te permite:

- trabajar con las sombras y las luces independientemente de los
  detalles que contienen,
- reducir el contraste y la cromaticidad globales, para percibir mejor
  el micro-contraste,
- cambiar la cromaticidad para reducir los artefactos resultantes de una
  modificación excesiva en los niveles (por ejemplo en los cielos),
- etc

### Sombras/Luces de la imagen residual

El grupo comienza dando la opción de poder asignar valores negativos con
los deslizadores (***El algoritmo usa valores negativos***), aunque a
costa de anular el último deslizador, el del *Radio Sombras/Luces*.

En el caso de activar la anterior opción, mover los controles
deslizantes para las Sombras y las Luces hacia la derecha aumenta la
luminancia de esas zonas; hacia la izquieda (valores negativos), la
reduce. La utilidad de emplear este método es la de poder oscurecer aún
más las sombras y aumentar el brillo de las luces:

<div>

- <figure>
  <img src="/images/wavelets_residual_original.png"
  title="wavelets_residual_original.png" />
  <figcaption>wavelets_residual_original.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SH.png" title="wavelets_residual_SH.png" />
  <figcaption>wavelets_residual_SH.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SH-out.png"
  title="wavelets_residual_SH-out.png" />
  <figcaption>wavelets_residual_SH-out.png</figcaption>
  </figure>

</div>

El efecto de estos cambios está influenciado por los controles
deslizantes de umbral: en una escala de luminancia de *0* a *100*, para
las sombras las luminancias con valores inferiores al establecido son
las que sufrirán variaciones. De igual forma, para las luces el umbral
indica el valor a partir del cual habrán modificaciones.

Por otra parte, si decides desactivar la opción *El algoritmo usa
valores negativos*, los deslizadores de las sombras y las luces solo
podrán tener valores positivos, de forma que únicamente podrás
*recuperar* las sombras (aclarándolas) o las luces (oscureciéndolas). El
resultado es muy parecido al de la herramienta
[Sombras/Luces](Shadows/Highlights/es.md) de la pestaña
Exposición. Sin embargo ten en cuenta que esta herramienta no tiene
capacidad de [reconstruir las
luces](Exposure/es#Reconstrucción_de_Luces.md).

Además, debes tener en cuenta la diferencia en el comportamiento del
módulo según esté activada o no la opción:

- si la opción *El algoritmo usa valores negativos* está
  **desactivada**:
  - los valores negativos en los deslizadores se ignoran (se tratan como
    si fueran igual a *0*)
  - las luces pierden brillo
  - las sombras se aclaran
- si por el contrario se **activa** la opción *El algoritmo usa valores
  negativos*:
  - los valores negativos tienen un fuerte impacto en la imagen residual
  - las luces pierden brillo si se emplean valores negativos
  - las luces **ganan** brillo si se emplean valores positivos
  - las sombras **se oscurecen más** si se emplean valores negativos
  - las sombras se aclaran si se emplean valores positivos

<div>

- <figure>
  <img src="/images/wavelets_residual_SHneg_original.png"
  title="wavelets_residual_SHneg_original.png" />
  <figcaption>wavelets_residual_SHneg_original.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SHneg_old.png"
  title="wavelets_residual_SHneg_old.png" />
  <figcaption>wavelets_residual_SHneg_old.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_SHneg_new.png"
  title="wavelets_residual_SHneg_new.png" />
  <figcaption>wavelets_residual_SHneg_new.png</figcaption>
  </figure>

</div>

En las tres imágenes anteriores puedes apreciar el cambio drástico,
además de que cuando la opción está desactivada el valor negativo de las
sombras se ignora, así como que las luces se oscurecen.

La última opción de este grupo es el ***Radio Sombras/Luces***

Este radio aplica un filtro de tipo [Guided Image
Filtering](http://kaiminghe.com/eccv10/)
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span> que atenúa las desigualdades o efectos demasiado
súbitos en las sombras y las luces provocadas por los ajustes en los
controles anteriores: se trata del area de influencia del efecto
producido en las sombras y en las luces, de manera que se integren mejor
dichos cambios en el resto de la imagen.

En cualquier caso, para decidir mejor los valores de umbral correctos,
comprueba el valor de las luminancias que te interesan en el panel del
Navegador.

Puedes ajustar las sombras y luces para:

- añadir impacto a los objetos brillantes,
- evitar que las luces se saturen,
- mejorar las sombras,
- etc

### Compresión del Contraste de la imagen residual

Este es uno de los aspectos fundamentales del procesado por niveles de
ondícula: el deslizador ***Contraste*** te permite cambiar el contraste
de la imagen residual mientras por otro lado puedes ajustar de forma
distinta el contraste de los detalles.

Por ejemplo, reduciendo moderadamente el contraste de la imagen residual
conseguirás más diferencia visual con el contraste de cada nivel, con lo
que se incrementa la percepción de profundidad y relieve. Dicho de otra
manera: puedes realizar aumentos moderados del contraste de los detalles
para evitar generar artefactos y al mismo tiempo reducir el contraste de
la imagen residual, lo cual en conjunto generará una percepción
equivalente a un mayor aumento de contraste en los detalles.

En cambio, si realizas cambios drásticos en el contraste de la imagen
residual, dependiendo de la foto puedes conseguir efectos interesantes:

<div>

- <figure>
  <img src="/images/wavelets_residual_contrast-.png"
  title="wavelets_residual_contrast-.png" />
  <figcaption>wavelets_residual_contrast-.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_residual_contrast+.png"
  title="wavelets_residual_contrast+.png" />
  <figcaption>wavelets_residual_contrast+.png</figcaption>
  </figure>

</div>

Para ayudarte a controlar el efecto este módulo tiene un conjunto de
opciones que te permiten ajustar el rango dinámico de la imagen
residual. Estas opciones se agrupan en la *Compresión por Contraste* y
la *Compresión por Mapeo de Tonos*.

#### Método de Compresión: Contraste

Al cambiar únicamente el contraste se ven los efectos inmediatamente y
la variación es casi lineal dependiendo de la posición del cursor: hacia
la derecha disminuirá el contraste y hacia la izquierda aumentará. Todo
éllo con una gestión interna de límites para evitar artefactos.

La ***Intensidad de la Compresión*** modifica el rango dinámico de la
imagen residual: hacia la derecha lo reduce (las sombras se aclaran y
las luces se suavizan) y hacia la izquierda lo amplía (las sombras se
oscurecen y las luces se intensifican ligeramente).

Mientras tanto la ***Gama de la Compresión*** modifica el reparto de
luces y sombras, desplazando en la práctica el histograma hacia la
izquierda o la derecha.

Con estos controles podrás, por ejemplo, reducir los efectos de la
niebla o permitir representar una imagen altamente dinámica.

#### Método de Compresión: Mapeo de Tonos

En este caso el método de compresión empleado es el mismo que el de la
herramienta [Mapeo de Tonos](Tone_Mapping/es.md) y sus
deslizadores actúan de la misma manera, aunque aplicados únicamente a la
imagen residual. Así pues modificarás los contrastes en profundidad
(como hace el mapeo tonal) y resultará casi imprescindible que ajustes
bien los cambios en los niveles, de forma que el conjunto esté
equilibrado.

No olvides que estás aplicando un mapeo tonal a la imagen residual, pero
que ésto no impide que actives también la herramienta del *Mapeo de
Tonos* global, por lo que deberás tener especial cuidado de no generar
artefactos si empleas ambas herramientas a la vez.

### Difuminado

Este grupo de dos deslizadores puede parecer banal, pero puede ser una
interesante ayuda para mejorar el [<https://es.wikipedia.org/wiki/Bokeh>
bokeh](https://es.wikipedia.org/wiki/Bokeh_bokeh.md) de la
imagen, al difuminar la luminancia de la imagen residual (***Difuminar
luminancia**'') y su componente de color (***Difuminar color**'').

El resultado obtenido está íntimamente ligado a los valores escogidos,
pero también a los [niveles de
ondícula](#Niveles_de_Ondícula.md) que hayas establecido: para
obtener un buen bokeh necesitarás que la imagen tenga la cantidad justa
de detalles para que el fondo sea reconocible o no (dependiendo de
cuánto desees que se difumine el fondo).

Normalmente los mejores resultados los obtendrás con 7 niveles de
ondícula o más y con valores de difuminado modestos (alrededor de *50*),
ya que es fácil generar halos y artefactos con niveles inferiores o
valores excesivos.

### Cromaticidad de la imagen residual

El mismo principio que se acaba de manejar con el contraste se aplica a
la cromaticidad, pero cambiando la saturación de los tonos de la imagen
residual.

El control de ***Intensidad*** va ligado a los valores establecidos en
el rango y la protección del azul del cielo explicados a continuación.

#### Rango del Azul del Cielo

De la misma forma que ocurría en el módulo del *Rango de colores*,
aunque el título se refiera al *azul del cielo*, aquí se pueden ajustar
los tonos que se deseen modificar, sean o no azul del cielo. Como ya se
ha dicho, estos colores están vinculados al control de la *Intensidad*.

El rango por defecto abarca los tonos habituales del azul del cielo.

#### Protección/Selección del azul del cielo

Con este control decidirás si vas a modificar la cromaticidad de las
zonas con colores incluídos en el rango anterior o no:

- con el deslizador en *0* los cambios realizados en el control de la
  cromaticidad se aplicarán a todos los tonos de la imagen por igual
- al seleccionar *-100* (deslizando hacia la izquierda) se centran los
  cambios de cromaticidad en el rango de tonos seleccionado
- por el contrario, seleccionando *100* (deslizando a la derecha) se
  modificarán los tonos que **no** coincidan con el rango seleccionado.

En las posiciones intermedias entre *0* y *±100* los cambios van siendo
progresivamente más hacia el rango escogido, o hacia el resto de tonos.

Este control es muy útil para prevenir la sobresaturación del tono de la
piel humana, que da lugar a un «tono zanahoria» rápidamente detectado
por nuestros ojos.

### Curva de la imagen residual

Esta curva es independiente del *Rango del azul del cielo* y del control
de cromaticidad: con élla puedes modificar los tonos de forma que
adquieran una dominante de color, independientemente del resto de
controles del módulo.

El funcionamiento es como sigue: en el gráfico puedes ver unas líneas
verticales coloreadas con puntos deslizantes; si mueves un punto hacia
arriba, las zonas de la imagen con el color de esa línea adquirirán un
tinte o dominante del color de la línea inmediatamente a su derecha. Si
lo mueves hacia abajo, la dominante será del tono de la línea
inmediatamente a la izquierda. Por ejemplo: moviendo el punto de la
línea amarilla hacia arriba, las zonas amarillas de la imagen residual
tomarán un tinte verdoso (la línea a la derecha de la amarilla),
mientras que si mueves el punto hacia abajo, la dominante será
anaranjada (la línea a la izquierda de la amarilla).

Fíjate que si desplazas la línea hacia la izquierda o la derecha, su
color cambiará, indicando qué tonos de la imagen serán los que se
modificarán. Sin embargo, si desplazas las líneas de la izquierda o de
la derecha, el color de referencia no cambia, a pesar de que dichas
líneas representan ahora tonos distintos.

### Equilibrio de Matiz y Color

Al activar esta opción se presentan 3 pares de controles del tono, cada
par para las *Luces*, los *Tonos medios* y las *Sombras*,
respectivamente. Cualquiera de éllos introduce una dominante de color
sobre la imagen residual.

Los controles modifican las componentes *a\** y *b\** del Espacio de
color Lab, por lo que los cambios serán:

- para la componente *a\** = del verde al rojo (o maś bien magenta
  claro)
- para la componente *b\** = del azul al amarillo

Los resultados dependerán de la intensidad de los cambios:

- con valores altos se pueden crear efectos especiales, similares a los
  conseguidos con el *Módulo de Color* pero centrados en la imagen
  residual. Puedes utilizarlo en combinación con aquel módulo si lo
  deseas
- con valores moderados podrás corregir manualmente el balance de
  blancos: por ejemplo, imagina una escena con los detalles principales
  situados en una sombra con dominante azulada, mientras que el fondo
  está a plena luz del día, con una temperatura de color diferente. En
  este caso puedes ajustar el balance de blanco para los detalles (y
  eliminar la dominante azul) y a posteriori reajustar el fondo (la
  imagen residual) y darle un balance de blancos a medida para cada zona
  (luces, tonos medios y sombras)

Por último, puesto que lo controles de compresión del contraste de la
imagen residual te permiten modificar las luminancias de cada zona,
tendrán una influencia directa en los resultados conseguidos con esta
parte del módulo.

## Módulo de Retoque final

En este módulo puedes aplicar pequeños retoques sobre la imagen, aunque
a pesar de situarse al final de la herramienta, con modificaciones
importantes en sus controles los cambios pueden significar que tengas
que reajustar el resto de módulos.

### Contraste direccional

En general en toda la herramienta se respeta el equilibrio inicial entre
los 3 componentes direccionales de la descomposición de la imagen:
vertical, horizontal y diagonal. Sin embargo, con este módulo puedes
aumentar el peso de una sobre otras, para conseguir un resultado
distinto.

#### Método de Balance del Contraste

Este *balance* modifica el equilibrio entre la descomposición diagonal
por un lado y la descomposición vertical y horizontal por otro. Su
principio es similar al de la [descomposición preservadora de
bordes](http://www.cs.huji.ac.il/~danix/epd)
<span style="font-size: 0.7em; font-style: italic;">(enlace a documento
en inglés)</span> que se basa en la [Factorización de
Cholesky](https://es.wikipedia.org/wiki/Factorización_de_Cholesky) y
modifica linealmente las luminancias de la imagen.

Siempre que el módulo de contraste, el de cromaticidad o el mapeo tonal
de la imagen residual estén activos, con este módulo se podrán modificar
los efectos conseguidos.

Tienes dos opciones:

- Control deslizante: con esta opción aparece el control ***Balance
  d/v-h*** con el que modificarás los contrastes de la imagen. A la
  derecha intensificarás la apariencia del contraste global de la
  imagen, mientras que a la izquierda la suavizarás. Sin embargo no
  olvides que estás actuando sobre el equilibrio entre las diferentes
  direcciones de la descomposición, por lo que con valores extremos
  introducirás artefactos importantes.
- Curva: en este caso aparece la curva ***Balance d/v-h (curva)***, que
  actúa sobre el balance en función de la luminancia de la imagen. Por
  defecto, las áreas oscuras y las brillantes se reducen para evitar
  artefactos (sub y sobreexposiciones).

En cualquiera de los dos casos anteriores, existe un control adicional:
***Variación del equilibrio entre Niveles***. Con él situado en cero
(por defecto), todos los niveles de la descomposición tienen el mismo
tratamiento. Si se sitúa a la izquierda, se enfatizan los niveles
inferiores (los detalles finos) y se reducen los niveles superiores (los
que dan volumen). En cambio si se sitúa a la derecha los niveles
inferiores se reducen y se aumentan los superiores.

Por otra parte, tienes a tu disposición un deslizador de
***Atenuación***, que actuará de la misma forma explicada en el
[capítulo sobre la atenuación del módulo de
Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md).

Por último la opción ***Balance de Cromaticidad*** permite que también
se modifique el equilibrio d/v-h en los componentes cromáticos de la
descomposición. Esta modificación se realizará con el mismo control del
método de balance utilizado (control deslizante o curva).

### Contraste Local Final

Esta curva se localiza al final del tratamiento, justo antes de la
recomposición y actúa de forma no lineal sobre el contraste de los
niveles de la descomposición.

Ten en cuenta que esta curva no duplica a la anterior (*Balance del
Contraste*), ya que ésta actúa en función del contraste local inicial y
no de la luminancia.

En la gráfica el centro de la abscisa corresponde al valor medio del
contraste local y a un tercio a cada lado encontraremos el punto
correspondiente a la media más una desviación estándar de los valores de
contraste local. Al modificar la forma de la curva reducirás o
aumentarás los efectos del módulo de *Contraste*, la *Nitidez de los
Bordes*, el *Método de Balance* e incluso el principio mismo de la
descomposición - recomposición.

Por defecto la curva es *plana* (es decir, que no tiene efecto), aunque
la puedes modificar a tu gusto para por ejemplo reducir aún más el valor
del contraste local bajo y así suavizar la visibilidad del ruido, o
reducir también los valores de contrastes locales altos y evitar
artefactos.

Además, tienes de nuevo a tu disposición un deslizador de
***Atenuación***, que actuará de la misma forma explicada en el
[capítulo sobre la atenuación del módulo de
Contraste](#Atenuación_y_selectividad_en_el_cambio_de_contrastes.md).

### Curva de Contraste *Posterior*

Esta curva no está relacionada con las anteriores, se encuentra al final
del procesamiento de los niveles de ondícula, tras la recomposición de
los niveles más la imagen residual y permite modificar el contraste
global de la imagen.

Actúa sobre la luminancia y su uso es similar a las otras curvas tonales
encontradas en RawTherapee, aunque en este caso no verás un histograma
de fondo.

Por fin, también tienes un deslizador que controla el ***Radio de
suavizado*** con el que aplicarás un difuminado en las zonas afectadas
que permitirán integrarse mejor en la imagen.

## Comparación final

 

<div>

- <figure>
  <img src="/images/wavelets_original_big.png"
  title="wavelets_original_big.png" />
  <figcaption>wavelets_original_big.png</figcaption>
  </figure>

- <figure>
  <img src="/images/wavelets_final_big.png" title="wavelets_final_big.png" />
  <figcaption>wavelets_final_big.png</figcaption>
  </figure>

</div>
