---
title: Image file formats and compression jp
contributors:
  - Yz2house
---

<div class="pagetitle">

画像ファイルの形式とその圧縮

</div>

## 中間ファイルの形式

　中間ファイルとは、編集途中にある画像データを、例えばRawTherapeeからGIMPなど他のプログラムに移動させる時のファイルのことを指します。

　この場合の理想的な形式は、画像データやメタデータの損失がなく、且つ読み込み・書き込みが簡単なものです。このことから、中間ファイルの形式としては、常に非圧縮16bitTIFFを使うべきでしょう。

## 最終ファイルの形式

　中間ではないファイル、つまり、最終編集画像やフィルムをスキャンした画像、HDR画像などを保存する場合は幾つか考慮する点があると思います：

- JPEGは最も幅広くサポートされている形式ですが、データ損失があります。殆どのJPEG形式は8bit／チャンネル、24bit／ピクセルのデータです。
- TIFF形式とJPEG形式はメタデータをサポートしていますが、PNG形式はしていません。
- TIFF形式は様々な圧縮方法が使えます（PNG形式で使う一つのDEFLATE、所謂Zipを含め）。ZipはTIFFをサポートしているRealWorldPhotosの画像を圧縮するのに最も効率の良い方法です。
- PNGは動作が遅く、効率は良くありません。
- 保存する画像は外部エディターを使ってもっと効率の良い、16bit JPEG
  2000やOpen EXRなどに変換することも出来ます。

## 損失のない圧縮法の比較をする

　比較のための入力ファイルには16bit 10000ｘ5000ピクセルのReal
Worldパノラマ画像を使いました。

　形式の変換に使ったのは、ImageMagic6.8.8.10、演算に使われたCPUは、x86_64(R)Core™i7
CPU Q820 1.73Ghzです。作業手順はBashで入力しました。

### TIFF 16-bit

　`for c in RLE None LZW Zip; do time convert foo.tif[0] -monitor -depth 16 -compress "$c" "${c}_16.tif"; ls -lh "${c}_16.tif"; done`

| 形式        | 圧縮法   | サイズ \[MB\] | 時間 \[秒\] |
|-------------|----------|---------------|-------------|
| TIFF 16-bit | 圧縮なし | 382           | 5           |
| TIFF 16-bit | RLE      | 385           | 5           |
| TIFF 16-bit | LZW      | 293           | 8           |
| TIFF 16-bit | Zip      | 243           | 61          |

　備考：妙なことに、RLEで圧縮を行ったファイルのサイズは、圧縮をしなかったファイルより大きくなりました。

### TIFF 12-bit

　`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 12 -compress "$c" "${c}_12.tif"; ls -lh "${c}_12.tif"; done`

| 形式        | 圧縮法   | サイズ \[MB\] | 時間（秒） |
|-------------|----------|---------------|------------|
| TIFF 12-bit | 圧縮なし | 287           | 4          |
| TIFF 12-bit | LZW      | 248           | 9          |
| TIFF 12-bit | Zip      | 210           | 44         |

　備考：GIMP-2.9と RawTherapee-4.2 は 12-bit
TIFFファイルをサポートしていません。

### TIFF 8-bit

　`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 8 -compress "$c" "${c}_8.tif"; ls -lh "${c}_8.tif"; done`

| 形式       | 圧縮法   | サイズ \[MB\] | 時間（秒） |
|------------|----------|---------------|------------|
| TIFF 8-bit | 圧縮なし | 191           | 3          |
| TIFF 8-bit | LZW      | 51            | 4          |
| TIFF 8-bit | Zip      | 49            | 41         |

### TIFF 16-bit浮動小数点

　`for c in None LZW Zip; do time convert foo.tif[0] -monitor -define quantum:format=floating-point -compress "$c" "${c}_fp.tif"; ls -lh "${c}_fp.tif"; done`

| 形式                   | 圧縮法   | サイズ \[MB\] | 時間（秒） |
|------------------------|----------|---------------|------------|
| TIFF 16-bit 浮動小数点 | 圧縮なし | 382           | 6          |
| TIFF 16-bit 浮動小数点 | LZW      | 153           | 8          |
| TIFF 16-bit 浮動小数点 | Zip      | 133           | 72         |

### TIFF 64-bit倍精度浮動小数点

　`for c in None LZW Zip; do time convert foo.tif[0] -monitor -depth 64 -define quantum:format=floating-point -compress "$c" "${c}_64fp.tif"; ls -lh "${c}_64fp.tif"; done`

| 形式                         | 圧縮法   | サイズ \[MB\] | 時間（秒） |
|------------------------------|----------|---------------|------------|
| TIFF 64-bit 倍精度浮動小数点 | 圧縮なし | 1525          | 21         |
| TIFF 64-bit 倍精度浮動小数点 | LZW      | 1016          | 36         |
| TIFF 64-bit 倍精度浮動小数点 | Zip      | 551           | 104        |

### OpenEXR 16-bit浮動小数点

OpenEXRは悪くないオプションです。最近の圧縮法で、効率も良く幅広くサポートされています。

　`for c in None Zip PIZ; do time convert foo.tif[0] -monitor -depth 16 -compress "$c" "${c}_16.exr"; ls -lh "${c}_16.exr"; done`

| 形式       | 圧縮法   | サイズ \[MB\] | 時間（秒） |
|------------|----------|---------------|------------|
| EXR 16-bit | 圧縮なし | 382           | 13         |
| EXR 16-bit | Zip      | 106           | 21         |
| EXR 16-bit | PIZ      | 111           | 7          |

　EXRを16bitTIFFに変換する際は、色空間をsRGBに設定します（設定するだけで、それに変換する訳ではありません）：

　`convert Zip_16.exr -depth 16 -set colorspace sRGB suchwow.tif`

### PNG 16-bit

　最後にPNG形式の結果です。ImageMagickではZLIBの圧縮率1～9を自分で入力します、或いは最初の値を0に設定した場合は、ハフマン圧縮を使います。2番目の値で、エンコーディングフィルターの時間を入力します、5=AdaptiveがRealWorldPhotosに最適です。

　`for l in 0 6 9; do time foo.tif[0] -monitor -depth 16 -quality "${l}5" "${l}5_16.png"; ls -lh "${l}5_16.png"; done`

| 形式       | 圧縮法  | サイズ \[MB\] | 時間（秒） |
|------------|---------|---------------|------------|
| PNG 16-bit | level 0 | 310           | 9          |
| PNG 16-bit | level 6 | 233           | 87         |
| PNG 16-bit | level 9 | 233           | 351        |

　備考：レベル6とレベル9のファイルサイズは変わらないのに、演算時間は4倍になりました。

### PNG 8-bit

　`for l in 0 6 9; do time foo.tif[0] -monitor -depth 8 -quality "${l}5" "${l}5_8.png"; ls -lh "${l}5_8.png"; done`

| 形式      | 圧縮法  | サイズ \[MB\] | 時間（秒） |
|-----------|---------|---------------|------------|
| PNG 8-bit | level 0 | 137           | 10         |
| PNG 8-bit | level 6 | 49            | 40         |
| PNG 8-bit | level 9 | 46            | 341        |
