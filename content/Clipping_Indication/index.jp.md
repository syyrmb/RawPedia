---
title: Clipping Indication jp
contributors:
  - Yz2house
---

　シャドウ部分のクリップ![<File:Warning-shadows.png>](Warning-shadows.png "File:Warning-shadows.png")とハイライト部分のクリップ![<File:Warning-highlights.png>](Warning-highlights.png "File:Warning-highlights.png")のインディケーター（警告）を使うことで、画像の中の暗すぎる部分と明るすぎる部分を簡単に見極めることが出来ます。

　これら2つのインディケーターのしきい値は環境設定＞一般タブで定義します。

　**シャドウ**部分のクリップインディケーターは、全ての色チャンネルが指定したシャドウのしきい値以下になっている部分を表示します。

　**ハイライト**のクリップインディケーターは、少なくとも色チャンネルの一つが指定したしきい値以上になっている部分を表示します。全てのチャンネルが飽和している部分だけを見たい場合は、ハイライトクリップインディケーターに加えて、輝度プレビューモードを有効にします。

　クリッピングは編集画面のメインプレビュー上部にある色域のプロファイルの種類を選択するボタン![<File:Gamut-hist.png>](Gamut-hist.png "File:Gamut-hist.png")によって計算が変わります。このボタンが押されていると、クリッピングの計算は作業プロファイルで、押されていなければガンマ補正された出力プロファイルで行われます。
