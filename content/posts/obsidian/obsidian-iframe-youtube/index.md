---
title: "iFrame Youtube Link"
date: 2020-11-01
description: "ObsidianにYoutubeの動画を埋め込む方法"
tags: [" #obsidian "]
aliases: [記事_ObsidianにYoutubeの動画を埋め込む方法]
---

# ObsidianにYoutubeの動画を埋め込む方法

## 今日の記事

今日はとりあえず、使い方のTipsから紹介していきたいと思います。
まずObsidianのメモにYoutubeを埋め込む方法から紹介していきます。

	メモにYoutubeを埋め込むってなに?

という疑問が浮かぶと思いますので説明していきます。

Youtube、結構役に立つ動画とかあって、勉強に使うということもあると思います。
そんなとき、見てる動画についてメモを取りたいというときがありませんか?(僕はあります)

うーん、どこにメモをとるべきか???

僕の場合だと、いままではMwebでした(もっと前はEvernoteでした。)
たぶん皆さん何かしらのメモアプリをつかっていると思います。

そのとき、何の動画を見たかということもメモしていると思います。例えば、その動画のURLなど。

まあ、そこまでは普通ですね。

ですがメモを見返すときに何の動画だったかとか思い出すのにURLだけだと不便だとおもいませんか?
Youtube動画のサムネイル画像などが一発でみれたらわかりやすいですよね。 
というかメモ内で動画そのものを見れたらもっとよいと思いませんか?

｢動画で気になるところをもう一度みながら、新しく気づいてことをメモしたい｣
それをメモアプリ内で完結させることができたらかなり便利だとおもいませんか?


今日はその方法を紹介していきます。

## iframeを使用して埋め込む

はい、以前このサイトでも紹介しましたが、HTMLタグのiframeを使います。

[iframeによる画像検索窓で視覚的に単語を覚える -アンキヨリハジメヨ](https://www.ankiyorihajimeyo.com/anki/iframe_search_eventbtn/)

Obsidianはmarkdown形式(軽量なHTMLと考えもらってよいです)を採用しているのでHTMLタグを埋め込むことができます。つまりHTMLでできたことがmarkdownでもある程度再現できます。

markdownそものもがかなり便利なものなんですが、今回それの説明もおいておいて、動画の埋め込み方だけ紹介します。

といっても今回はかなり簡単に終わります。コードなんて全く書きません。Youtubeのサイトから埋め込む用のコードをコピーしてはるだけです。


はい、まずYoutubeにいきます。

[Why Obsidian Will Overtake Roam - YouTube](https://www.youtube.com/watch?v=_x54XJrECvk&ab_channel=LinkingYourThinking)

1. ｢共有｣ボタンをクリックします

![img2](data/02_obsidian_iframe_youtube.png)

2. ｢埋め込む｣ボタンをクリックします

![img3](data/03_obsidian_iframe_youtube.png)

3. iframeのコードが生成されるので｢コピー｣ボタンをクリックします

このとき動画の開始時間を入力するとその開始時間ではじまる動画のiframeコードがつくられるので、ここから始めたいという方は開始時間を入力してください。

![img7](data/07_obsidian_iframe_youtube.png)

4. Obsidianのノートにそのコードを貼り付けます

![img8](data/08_obsidian_iframe_youtube.png)

<br><br><br><br>





終わりです。

はい、以上で今日の内容は終わりです。
めちゃくちゃ簡単ですね(笑)


これでmarkdownのプレビュー画面を開いてみてください。Youtubeの動画がちゃんとあります。これがmarkdwonの良いところです。

これだけでYoutubeの動画を埋め込むことができます。


{{< youtube RqZSZz6Zixc >}}


## メモをつなげる

まあ、できることがこれだけだったらあまり驚かないんですけどね。他のmarkdownエディタでもyoutubeの埋め込みは出来ると思います。ここからがObsidianの本領の発揮です。
<br>

Obsididanはただのmarkdwonメモアプリではありません。

Obsidianは **Personal Knowledge Base (PKB)** としての使い方が真の姿です。

まずPKBってなによ?って感じだと思うんですが。これもまた少し長くなるので、簡単に言うと、｢個人の知識や参照したい情報をまとめたwiki的なもの｣ですね。


とにかく知識や情報を集めて、整理してそれらを繋げていき、新しいアイデアを創造したり、文章を書いたりするためのツールだと思ってください。

[Obsidian 公式サイト](https://obsidian.md/)

![img9](data/obisidian_secondbrain.png)

PKBという概念がなくとも、私達は普段から情報をまとめたり、整理したりしています。要するにそれを補助してくれるツールです。(PKBについてはまた別途で記事を書くつもりです。)

はい。では実演動画です。

{{< youtube vBZDUIjFM60 >}}


こういう感じですね。Youtubeの動画で勉強するときですが、一つの動画で知識が完結するということはあまり無いと思います。

むしろ様々な動画を見て、それらの情報をまとめたり、整理したりするはずです。

そんなときObsidianは役に立ちます。

そもそもYoutubeの動画のメモをつくる以前に、様々なメモを僕は作っています。技術系の参照情報や書籍に関する読書ノートなど。それら様々な情報とYoutubeの動画に関するメモを関連づけることができます。つまり、今まで学んできたことすべてとつなげることができます。

## iframeの大きさ調整

```HTML
<iframe width="560" height="315" src="https://www.youtube.com/embed/vBZDUIjFM60" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>
```

widthとheightでサイズを調整できます。
`width="100%"`にしておけばObsidianのタブの幅サイズに調整してくれます。

詳しくは上で紹介したAnkiでiframeを使う記事を参考にしてください。

[iframeによる画像検索窓で視覚的に単語を覚える -アンキヨリハジメヨ](https://www.ankiyorihajimeyo.com/anki/iframe_search_eventbtn/)

## 終わり

今後、Obsidianについての記事を上げていきますが、このサイトの記事も今はすべてObsidianを使ってmarkdown形式で書いています。

動画データを実際に埋め込んでいるわけではなく、**プレーンテキストでリンクをはっているだけなので、データは軽く、さらにmarkdwonファイルなのでシェアすることも、他のエディタでひらくことも簡単**です。

**軽快に情報や知識をつなぐことができるツール**。それがObsidianです。


ちなみに AnkiもPKB(Personal Knowledge Base)の一種だと考えられます。今後この分野はさらに色々なツールがでてきて面白いことになると思います。日本ではまだその勢いは感じられませんが、数年後はこのPKBという概念が一般化すると思います。
