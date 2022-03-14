---
title: "Prism.js"
date: 2021-09-15
description: "Anki に prism.js を入れる"
cover:
    image: "data/prism-0-view.png" # サムネイル画像画像 path/url
    alt: "prism.js image" # alt text
    caption: "prism.jsを入れる" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
tags: [" #anki ", " #prism "]
---

[Prism.js](https://prismjs.com/index.html)を利用してAnkiで次のようなコードハイライトを実現する。

![](data/prism-0-view.png)

[Prism](https://prismjs.com/index.html)の公式サイトにアクセスして｢Download｣ボタンを押す。

![prism-1](data/prism-1.png)


次に利用する言語やテーマ、プラグインの選択を行う。

![](data/prism-2_選択画面.png)


- Compression level : Minified versionをチェック
- Themes : 好きなハイライトテーマを選択
- Languages : Select/unselect all をチェックしてすべての言語のチェックを入れる

![](data/prism-3_plugin.png)


好きなプラグインにチェックを入れる。自分の場合には次のプラグインにチェックした。
- Line Numbers
- Autolinker
- Show Language
- Normalizze White-space
- Autoloader
- Toolbar
- Copy to Clipboard
- Dif Highlight
- Treeview
- Match Braces

![](data/prism-4_download.png)

｢DOWNLOAD JS｣と｢DOWNLOAD CSS｣をクリックして`prism.js`と`prism.css`をダウンロードする。

Ankiにデータを消されないように名前の頭にアンダーバーをつけて`_prisim.js`、`_prism.css`とリネームする。

Ankiを閉じた状態で`/Users/User_Name/Library/Application Support/Anki2/Profile_Name/collection.media`にその2つのファイルをペーストする。

![](data/prism-5_files.png)

Ankiを起動して使用するノートタイプを編集する。

カードタイプの編集画面で次のコードを適当な場所に追記する。これでコードハイライトが実現する。

```html:
<link type="text/css" href="_prism.css" rel="stylesheet" />
<script async type="text/javascript" src="_prism.js" charset="utf-8"></script>
```

![](data/prism-7_code.png)

フィールドに次のコードを書く。`language-xxxx`のxxxxにはなんの言語か指定する。JavaScriptなら`language-js`とする。

```html:
<pre class="language-xxxx"><code>
コード
</code></pre>
```

![](data/prism-6_code.png)

xxxxの部分は[次から確認できる](https://prismjs.com/index.html)

![](data/prism-8_lang.png)


