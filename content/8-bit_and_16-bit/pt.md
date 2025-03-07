---
title: 8-bit and 16-bit pt
contributors:
  - DigitalPix
---

"8 bits" quando se refere a formatos de imagem normalmente significa que
o programa atribui 8 [bits](https://en.wikipedia.org/wiki/Bit) (oito "1"
ou "0" valores, que juntos fazem um
[byte](https://en.wikipedia.org/wiki/Byte), capaz de representar um
valor [integral](https://en.wikipedia.org/wiki/Integer) de 0
\[00000000\] até 255 \[11111111\]) para cada canal de cor do pixel, e
cada pixel nos arquivos que o RawTherapee salva tem três canais de cor -
vermelho, verde e azul.

A maioria das câmeras modernas com raw
[DSLR](https://en.wikipedia.org/wiki/DSLR) usa conversores
analógico-digital para gravar os dados do sensor de 12 ou 14 bits. Isso
significa que ao escolher um formato de saída de 8 bits por canal em sua
câmera, como JPEG, se perde algumas informações. Não é tão simples
quanto parece, câmeras registram dados linearmente (devido a limitações
no design de hardware) enquanto JPEG, TIFF e PNG usam [codificação
gama](https://en.wikipedia.org/wiki/Gamma_correction) nos seua dados, o
que significa que eles distribuem mais valores no intervalo de sombra e
menos nos realces que melhor combinam com a sensibilidade do olho. Isso
significa que um JPEG de 8 bits pode exibir tanto quanto
log2((1/2^8)^2.2) = 17.6 paradas de alcance dinâmico que excede de fato
as 14 paradas das melhores câmeras atuais, o que explica por que às
vezes podes ver o ruído de sombra de uma câmera num JPEG de 8 bits. No
entanto, devido aos poucos valores nos realces, perdemos precisão em
comparação com a câmera. Praticamente isso não é um problema quando o
arquivo de saída é o definitivo e não será mais processado, no entanto,
uma foto pode ser melhorada quando salva com dados raw e processada
usando um programa de processamento raw, como o seu - RawTherapee.

Depois de ter processado uma foto no RawTherapee, és confrontado com a
mesma escolha - para salvar a imagem com uma resolução de cor de 8 bits
por canal, ou 16 bits por canal (apenas
[TIFF](https://en.wikipedia.org/wiki/TIFF) e
[PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), não
[JPEG](https://en.wikipedia.org/wiki/JPEG)). Se planejas pós-processar
tuas fotos após o RawTherapee num programa de edição de imagens de 16
bits, é melhor salvá-las num formato de 16 bits sem perdas. TIFF não
compactado é sugerido como um formato intermediário, pois é rápido para
salvar e armazenar todos os metadados
([Exif](https://en.wikipedia.org/wiki/Exif),
[IPTC](https://en.wikipedia.org/wiki/IPTC_Information_Interchange_Model),
[XMP](https://en.wikipedia.org/wiki/Extensible_Metadata_Platform)) do
arquivo original (PNG geralmente descarta metadados!).

Há alguma confusão sobre a nomenclatura de arquivos de 8, 16, 24 e 32
bits. Aqui está um esclarecimento, mas fica confuso, então coloque seu
chapéu de folha de estanho. Realmente não precisas ler isso para usar
RawTherapee, é apenas conhecimento de fundo. Cada um dos canais
vermelho, verde e azul armazenados em um arquivo JPEG, PNG ou TIFF é, na
verdade, uma imagem incolor, mas ao combinar essas três imagens
incolores, você obtém uma imagem colorida. É assim que funciona toda a
representação digital de imagens - as imagens coloridas são sempre
decompostas em seus componentes de uma forma ou de outra. Dos formatos
de arquivo que o RawTherapee pode salvar em (JPG, PNG e TIFF), cada
pixel contém informações para três canais de cores - vermelho, verde e
azul. Dizemos "8 bits por canal" para deixar claro que esses 8 bits se
aplicam apenas a um canal de cor. A razão é que podes encontrar
referências a "imagens de 8 bits" e aqui fica confuso, porque a pessoa
que escreveu isso pode estar se referindo a um formato em escala de
cinza que armazena apenas um canal ou a um formato colorido que armazena
três canais, com precisão de 8 bits cada. Outra notação para as mesmas
imagens de "8 bits" que o RawTherapee salva é "24 bits". Woo, confuso.
Ou é? Cada pixel é feito de 3 canais e cada canal armazena 8 bits de
dados, então temos um total de 24 bits de dados por pixel. Fica pior.
Programas de edição de imagem também podem armazenar um quarto canal,
chamado "alfa". Para simplificar, alfa descreve o quão transparente é um
pixel. Esses canais alfa também possuem uma "resolução de cor" de 8
bits. Arquivos PNG e TIFF podem manipular alfa, JPEG não. Se tens uma
imagem de 8 bits por canal com um canal alfa, ela também pode ser
descrita como uma imagem de 32 bits; R (8) + G (8) + B (8) + alfa (8) =
32. O problema final é que também podes ter uma imagem que atribua até
32 bits por canal de cor. Essas imagens podem ser descritas como imagens
de "32 bits", bem como "imagens de 96 bits" (porque R (32) + G (32) + B
(32) = 96). Todos os arquivos HDR reais são armazenados em formatos de
imagem que atribuem pelo menos números de ponto flutuante de 16 bits
para cada pixel por canal de cor, como o formato EXR, ou os de 32 bits,
como o formato RGBE. Para resumir, uma imagem de "8 bits por canal" com
três canais (RGB) também pode ser chamada de imagem "24 bits por pixel",
e uma imagem "16 bits por canal" com três canais também pode ser chamada
de Imagem "48 bits por pixel". Em ambos os casos, use o primeiro (a
descrição completa do "x bit por canal", não diga apenas "x bit"!), Fica
mais claro o que queres dizer.
