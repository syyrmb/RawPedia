---
title: Negative jp
contributors:
  - Yz2house
---

<span style="color: #000000; background: none; overflow: hidden; page-break-after: avoid; font-size: 2.0em; font-family: Georgia,Times,serif; margin-top: 1em; margin-bottom: 0.25em; line-height: 1.3; padding: 0; border-bottom: 1px solid #AAAAAA;">ネガ
</span>

　フィルムカメラで撮影された、明暗と色が反転しているような画像のことをネガと呼びますが、今のところRawTherapeeは、手間のかからないワンクリックで画像をネガへ変換することが出来ません。以下に、現在のバージョンでネガに変換する方法を紹介します：

1.  　露光補正セクションの[トーンカーブを](exposure/jp#トーンカーブ)反転させる、或いは[RGBカーブカーブ](rgb_curves/jp)機能で、全てのカーブを反転させます。欠点：トーンが変化します。
2.  　[フィルムシムレーションで](film_simulation/jp)、“RawTherapeeフィルムシミュレーション集”の中から“negative”のHaldCLUTを選んで適用します。欠点：幾つかの設定値、例えば露光量補正スライダーの値が逆向きに作用し、ハイライトやシャドウが飛んだり潰れたりするかもしれません（機能自体がネガを扱うように設計されていないため）。
3.  　上記で説明したニュートラルなHaldCLUTのネガティブを使うだけでなく、既に貴方がネガティブへの変換だけでなく、RawTherapeeや他のソフトを使って好みの色調も調整出来るのであれば、独自のネガティブHaldCLUTを作成し、編集に適用することが出来ます。そうすれば画像を簡単にネガティブ変換するだけでなく、自分の好みに合わせた色調も同時に得られます。後は露光量補正や他のカーブでヒストグラムを拡大するだけで済みます。
4.  　現状、ベストと思われる方法は、貴方のカメラのDCP（DNG Camera
    Profile）を使う方法です。DNG Profile
    Editorでそのトーンカーブを反転させ、その編集したDCPを手動でネガに適用します。方法を以下に説明します。自分でネガ用のトーンカーブを作りたくなければ、次のリンクからネガ用のDCPのサンプルをダウンロード出来ます：[Linear
    inverted.dcp](:File:Linear_inverted.dcp.md)

## ネガ用のDCPを作成する

![](DNG_Profile_Editor_inverted_tone_curve.png "DNG_Profile_Editor_inverted_tone_curve.png")
![](Rt_negative_dcp_l_curve.png "Rt_negative_dcp_l_curve.png")

1.  \[<https://helpx.adobe.com/jp/photoshop/digital-negative.html>　 DNG
    Profile
    Editor\]を手に入れます。[wine　wine](https://www.winehq.org/)（英語）を使えばLinuxでも問題なく動作します。
2.  貴方のカメラ或いはスキャナーのraw画像（ネガの写真でも可能です）の形式を、“[Rawファイルの形式をDNGに変換する](how_to_convert_raw_formats_to_dng/jp)”の説明を参考に、DNGに変換します。
3.  DNG Profile EditorでそのDNG形式の画像を開きます。
4.  カラーテーブルタブの中で、“Adobe
    Standard（<your camera model>）”と呼ぶベースプロファイルを探します。あればそれを使いますが、無ければ“Choose
    external profile”を選択し、“<your camera model>Adobe Standard
    dcp”と名付けられたファイルを探します。“[LCPとDCPプロファイルを取得する方法](how_to_get_lcp_and_dcp_profiles/jp)”に、入手方法と探し方が説明されています。
5.  トーンカーブタブの中のトーンカーブを反転させます。つまり、最上点を左に移動し、最下点を右に移動します。
6.  同じトーンカーブタブの中に、3種類の“Base Tone
    Curve”があります。うち“Base Profile”と“Camera Raw
    Default”は通常同一のカーブで、画像にコントラストを与えます。もう一つのカーブは“Linear”で、画像の印象をフラットにします。DCPは、“Base
    Profile”と“Linear”で2つ保存することを奨めます。RawTherapeeで編集を行う際に、どちらのプロファイルが適しているか選べるからです。どちらのDCPもRawTherapeeで更なる調整が必要ですが、“Linear”で保存したDCPの方が、“Base
    Profile”で保存したDCPより、多くの調整が必要です。しかし、後者のDCPは彩度が飽和してしまう場合があるのです。
7.  DCPを作成するには、“ファイルをクリックして、<your camera model>を書き出します。先ほど推奨したように、2つのDCPを作成します。

　ネガ用にこの新しいDCPを使うには、raw画像を開き、カラータブのカラーマネジメントに表示されている入力プロファイルで、カスタムを選択し、そのDCPを検索します。“DCPのトーンカーブを使う”は有効にします。

　これらDCPを使って、RawTherapeeで画像を編集しますが、RGBチャンネル（露光補正パネルの2つのカーブ）の調整は、明るさを変えるだけでなく、彩度に対しては貴方のカーブより強く影響することを覚えておいて下さい。場合によって、カーブのモードを“加重平均”や“彩度と明度のブレンド”にして調整します。或いは、L\*a\*b\*色空間で調節し、彩度の問題を回避することも出来ます。明るさが色と切り離されているので、明度の調整が色に影響を与えません。ですから、L\*カーブで明度を調整した後、CCカーブなどで彩度を調節出来ます。
