---
title: Film Simulation jp
contributors:
  - Yz2house
---

<div class="pagetitle">

フィルムシミュレーション

</div>

<img src="/images/Rt_haldclut_london.jpg" title="Rt_haldclut_london.jpg"
width="900" alt="Rt_haldclut_london.jpg" /> 　
　フィルムシミュレーションは、クリック一回で編集画像の色彩を参照画像の色彩と一致させる機能です。この機能を利用するには、HaldCLUTパターンで構成されたPNG或いはTIFF形式の参照画像を使う必要があります。各HaldCLUTは一つの「色映り」に相当します。その「色映り」は任意の画像に適用できますが、参照画像の殆どは典型的なフィルム写真から集めたものなので、機能名をフィルムシミュレーションにしました。

　この機能を使うために、RawTherapeeがHaldCLUT画像を読み込む必要があります。フィルムシミュレーション集と呼ぶ私たちのコレクションをダウンロードして使う、または貴方自身でHald
CLUT画像を作成することも出来ます‐これについては後で説明します。この機能を使う時、初回だけRawTherapeeが参照画像の保存されているフォルダーの場所を聞いてきます。フォルダーに参照画像を保存した後、環境設定→画像編集タブ→ディレクトリと進み、“HaldCLUTディレクトリ”をそのフォルダーに指定して下さい。

## 起動時間

　プログラムを起動するたびにRawTherapeeは指定されたHaldCLUTフォルダーをスキャンします。従って、毎回無関係のファイルまで読み取るという無駄な動作を避けるため、HaldCLUTの参照画像だけが入っているフォルダーを作成しておくことが重要です。安全対策として、フォルダーの読み取りが始まって10秒が経過するとプログラムから警告が出ます。その場合は、ポップアップした警告表示の中のボタンをクリックして読み取りを中止し、″環境設定→画像処理→“ディレクトリ″と進み、どのフォルダーが指定されているか確認して下さい。そして、Hald
CLUT画像だけが保存されているフォルダーを指定するか、フィルムシミュレーション機能を使わないのであれば、空のフォルダーを指定して下さい。

　参考までに起動時間がどれくらい影響を受けるかと言うと、Hald
CLUTフォルダーに何も入っていない場合と500個のファイル（これはRawTherapeeフィルムシムレーションの中のファイル数より大きい数です）が入っている場合の起動時間の差はたったの0.1秒です。しかし、貴方が誤って、そのフォルダーにC:¥Program
Files(x86)などを指定したとすると、そこに属する全てのフォルダーをスキャンするのでプログラムの起動に数分かかる場合があります。Hald
CLUTだけが入っている専用フォルダーを指定すれば、こういった問題を避けられます。

## どの様に作用するのか

<figure>
<img src="/images/Hald_CLUT_Identity_12.png"
title="Hald_CLUT_Identity_12.png" />
<figcaption>Hald_CLUT_Identity_12.png</figcaption>
</figure>

　フィルムシミュレーション機能では、HaldCLUTパターンと呼ばれる特別に準備された画像を使います。“CLUT”は“Color
Look Up
Table”の略称ですが、Haldの由来は分かりません。HaldCLUT画像はマトリクスの中に様々な色相のグラデーションを並べたセットです。これら色相に変更が加えられていないニュートラルな画像を、“HaldCLUT
identity”と呼びます。HaldCLUT
identityを編集画像に適用しても、何も変わりません。目標とする“色映り”を反映させるためには、画像編集ソフトでHaldCLUT
identityを開き、全体の色調を調整します。例えば、レベルやカーブ、色相、彩度、などを使ってです。適用できるのはこれらの様な全体的調整で、トーンマッピングやノイズ低減、シャープ化のようなローカル調整はこの機能との互換性がないので使えません。肌の色を小麦色に変えたり、木の葉をいきいきした感じにさせたりするための機能です。

　HaldCLUT画像は色のグラデーションを並べたようなセットに見えますが、実はマトリクスの数値をグラフィックスで表現したものです。これらの数値は“出力”とか“結果”と呼ばれる値です。identity
を含むHaldCLUTファイルを扱える画像編集プログラムは、“入力”或いは“元”の値が何であるか認識しています。例えば、identity
ファイルの座標x=143、y=0に位置するピクセルは純色の赤、RGB＝（100％、0％、0％）、であることを知っています。貴方がこのidentity画像に調整を加え、その赤色のピクセルにオレンジの色味を加えたとしましょう。これでidentity画像が調整され、新しいHaldCLUTファイルが作られたことになります。

　RawTherapeeを使って編集画像にこのファイルを適用すると編集画像の純色の赤のピクセルが全部同じように調整されます。つまり、編集画像の赤色の部分にオレンジ色を加えるために数値を一つ一つ調整するような面倒な作業をせずとも、RawTherapeeやGIMPなどの編集プログラムでHaldCLUT
identity開いて赤色の部分を調整し（実践的に言えば、RGBカーブなどを使って赤色を全体的に調整する）、そのファイル保存しRawTherapeeを使って適用すれば同じ調整がどの編集画像にも簡単に適用できます。

　HaldCLUT画像にどの様なカラープロファイルを適用しても属性が変わることはありません。肝心なのはピクセルの値です、何故ならHaldCLUT画像は“出力”の値で作られているマトリクスだからです。カラープロファイルの”指定“はピクセルの値を変えることはありませんが、”適用“や”変換“は格納されているピクセルの値を変えてしまうので行ってはいけません。但し、カラープロファイルの指定が影響を与える可能性もあります。画像編集プログラムの中には指定されたカラープロファイルに応じて作業プロファイルを変えるものもあるからです。

　色の転換精度はHaldCLUT画像のレベル数（縦行の数）、そしてHaldCLUT画像を格納するビット深度で決まります。例えば、8‐ビットファイルに格納した12‐レベルのHaldCLUTを使って32‐ビット画像（或いは、32‐ビット空間にある任意のビット画像）を処理するなら、得られる色の精度は貴方の画像が持つ色の精度より落ちるでしょう。但し、これは問題とはなりません。不明な色の値は既知の値から補間されるので、ポスタリゼーションは起こりません。HaldCLUTを格納するために使う画像のビット深度はニーズに応じて選ぶもので、厳密にHaldCLUTのレベル数に合わせる必要はありません。一般的な写真であれば、8‐ビット空間で8‐レベルのHaldCLUT画像を格納していれば、それ以上のビット深度の画像を処理する場合でも十分です。

　更に詳しい情報が、Eskil SteenbergのHaldCLUTに関するページにあります:
<http://www.quelsolaar.com/technology/clut.html>

　ImageMagickを使って12‐レベルの16ビットHaldCLUT
identityを作成する場合は、以下のコマンドをコンソールから入力します：

　`convert hald:12 -depth 16 -colorspace sRGB hald12_16bit.tif`

## 注意

　もし貴方が自分のHaldCLUT
画像を作る時は、www.quelsolaar.comから入手したプログラムでHaldCLUT画像を作成しない方がいいでしょう。ハイライトに関係したバグがあるからです。ImageMagickかGraphicsMagickを使います。もちろんバグのない私たちのidentityファイルの利用に問題はありません。

## 自分のHald CLUT画像を作る

　この項では、特定のカラーレンダリングや明暗を再現するための独自のHaldCLUTファイルの作成方法を説明します。

1.  RawTherapee、或いは他の編集プログラムで画像を開き、好みの画像に仕上げます。その時、フィルムシムレーションが全体的な色彩の変更を再現する機能であることを思い出して下さい。つまりローカルな調整は行いませんーローカルコントラスト、トーンマッピング、などピクセルの値を変えるような調整のことですーシャープ化やノイズ低減も使いません。調整するのは、彩度の変更や、レベル調整、トーンカーブ、L\*a\*b\*調整です。それらの変更をサイドカーファイルに保存するか、変更内容を書き出しておいて下さい。次のステップで使います。
2.  HaldCLUT
    identityファイルを上記と同じ編集ソフトで開き、同じサイドカーファイルを適用するか、書き出しておいた調整を行います。
3.  この画像を8‐ビットsRGB
    TIFFかPNGでRawTherapeeが読み込むHaldCLUTフォルダーに保存します。これで準備完了です。あとはプログラムを再起動すればHaldCLUTフォルダーの中に新しく作成したHaldCLUTファイルがあるはずです。

　新しく作成したHaldCLUT画像の色の精度が8‐ビットであっても、足りない色情報は補間されますのでポスタリゼーションは起こりません。つまり、画像の質は維持されるので、作成には12‐レベルのidentityファイルを使うことをお勧めします。たとえ8‐レベルのもので作成しても、各色チャンネル8‐ビットのPNGやTIFFファイルで保存すればいいでしょう。

　保存したHaldCLUT画像にカラープロファイルを割り当てることは問題ではありません。重要なのは、画像のピクセル値です。GIMPやPhotoshopの利用者なら、“カラープロファイルの割り当て”と“カラープロファイルへの転換”という用語を知っていると思いますが、カラープロファイルを割り当てることに問題はありません、何故ならそれはピクセル値に影響しないからです。しかし、カラープロファイルに転換することは問題です、何故ならピクセル値が変わるからです。RawTherapeeでHaldCLUT画像を編集する際、[出力カラープロファイルの](color_management/jp#output_profile)選択には注意が必要です。何故なら保存画像のピクセル値を変えてしまうかもしれないからです。私たちから提供された、或いは私たちの設計従って作成されたidentity画像はsRGBのプライマリー色度を使っています。従って色を維持するには画像を保存する際にRTv2_sRGB、或いはRTv4_sRGBを使います。

　作成したHaldCLUTをRawTherapeeの中にある画像に適用した時、画像の明るさが予想外に著しく暗くなることがあります。これはプログラムの動作がガンマに何らかの影響を与えていると思われます。解決するにはプログラムが行う動作を無効にする必要があります。この場合、12‐レベルのHaldCLUTの作成時に、色空間にsRGB”ではなく単なる“RGB”を使って下さい。

### 高度な手法ーDNG identity

これはまだ試験的な方法で、常に機能するとは限りません。
編集プログラムの中にはTIFF画像が開けないものがあります。しかし、そのプログラムがDNGファイルとデモザイクした画像（Adobe
DNG
Converterで言うところの“線形（デモザイク）”）を処理できるなら、以下の手法が使えます。ImageMagickとExif
Toolで以下のコマンドラインを使います。DNGが一種のTIFF形式であることを利用します。HaldCLUT
identityをDNG形式で作成するのです：

`convert hald:12 -depth 16 -colorspace RGB -gravity NorthWest -splice 4x4 -gravity SouthEast -splice 4x4 foo.tif`
`exiftool -DNGVersion=1.4.0.0 -PhotometricInterpretation='Linear Raw' foo.tif mv -v foo.tif Hald_CLUT_Identity_12.dng`

　上記の手法を使うにあたって一つ注意があります。Raw編集プログラムは、デモザイク処理を行う過程で技術的な理由から画像の外郭部分で一定の数のピクセルを削除しています。どれだけのピクセルが削除されるかは、そのプログラム次第なので自分自身で調べるしかありません。12‐レベルのHaldCLUT
identity画像は1728x1728ピクセルで構成されています。CLUT画像を処理する場合、その色情報を模倣するためには保存する画像の方も正確に1728x1728ピクセルの画像でなければなりません。プログラムにraw画像を処理しているかのように見せかけるため、そして画像の外郭部分で数ピクセルが削除されるという理由から、保存する画像に追加しなければならないピクセルの行と列の数を正確に把握しておく必要があります。RawTherapeeはデモザイクされたDNGファイルを読み込む際に外郭部分の4ピクセルを削除しています。従って上記のコマンドラインで画像の底辺と右の縁に4ピクセル追加し、それからもう4ピクセル上辺と左の縁に追加するように記述しています。使用する編集プログラムでこの画像を開き、各縁を拡大し、ピクセルを更に追加（或いは削除）する必要があるかどうか判断します。

　外郭のピクセル処理が済めば、あとは“自分のHaldCLUTを作る”項で説明されている手順にしたが追うだけです。

## RawTherapeeの中の閲覧

　私たちが集めたHaldCLUT画像は沢山あります。それら全てを試してみたいと思う人もいるでしょう。でも各画像を一つ一つマウスでクリックする必要はありません。収集された全ての画像一つ一つを、マウスを使わずに簡単にチェックする方法があります。RawTherapeeにHaldCLUTフォルダーを読み込ませる、編集予定の画像が既に開かれている、フィルムシムレーション機能の使用準備も整っているとしましょう。あとはコンボボックスの中の任意のHaldCLUT画像を選び、キーボードの“↑”と“↓”キーで前と次を適用します。この方法を使えば、サブフォルダーを飛び越えることも出来ますー例えば白黒画像のサブフォルダーからカラー画像のサブフォルダーへと移動することが出来ます。

　幾つか特定のHaldCLUT画像の効果を比較したいが、それらが別々な位置に収納されている場合は、HaldCLUTを適用した画像を[スナップショット機能で](the_image_editor_tab/jp#スナップショット)一時保存し、それらスナップショットをクリックして比較します。

## RawTherapeeのフィルムシムレーション集

　このアーカイブにはフィルム写真の映りを模倣したHaldCLUTが集められていて、貴方の画像の色を即座に特定のフィルム調に変えることが出来ます。ファイルネームの中に断わりがない限り、画像の色空間はsRGBで、各色チャンネル8‐ビットのPNG形式の画像です。殆どの画像が様々なフィルム写真の映りー現像時の増感や減感、映りの経時的変化ーを模倣するようにデザインされています。

　ファイル名に付いている、＋、＋＋、＋＋＋、－、－－、は現像時の増感或いは減感の強さ（但し、＋＋が＋の倍という関係ではありません）を意味しています、“generic”は一般に販売されているフィルムの再生版です。

[ダウンロード](http://rawtherapee.com/shared/HaldCLUT.zip) (ファイルサイズは402MBあります)  

<!-- -->

ログの変更  
2015‐9‐20  
“CreativePack-1”というカラー収集を追加

TIFF形式画像を全てPNG形式に変換（identityファイルを除く）

2015-3-25  
IdentityCLUTにハイライトのシアンカラーにバグがあることを発見し、このバグを修正。

減感・増感で、ファイルの並びを修正

2014-08-25  
最初の公式リリース

カラーと白黒のフォルダーで、ブランドごとにサブフォルダ―に入れる

2014-08-15  
README.txtを拡張し、免責事項を加える

2014-07-05  
最初の内部リリース

全ての画像を最大非損失圧縮で再圧縮

　Hald CLUTについてもっと知りたい方は以下のリンクからどうぞ（英語）:

  
<http://www.quelsolaar.com/technology/clut.html>

<http://blog.patdavid.net/2013/08/film-emulation-presets-in-gmic-gimp.html>

<http://blog.patdavid.net/2013/09/film-emulation-presets-in-gmic-gimp.html>

貢献者:

  
Pat David - <https://discuss.pixls.us/u/patdavid>

Pavlov Dmitry

Michael Ezra - <https://discuss.pixls.us/u/michaelezra>

免責事項:

  
Hald
CLUT画像の多くのファイル名に見られる商標権のある名前は、情報目的のためだけです。プログラムのユーザーに提供されHaldCLUT画像が、どのフィルムストックに類似したものであるかという情報を示すだけです。名前を使用する以外に、この情報を譲渡・移転することは決してありませんので、私達はこうした名前の利用は公正であると考えます。本文の発行人も著者も、これら商標権を持つ企業に所属しておらず、承認も受けてはおりません。
