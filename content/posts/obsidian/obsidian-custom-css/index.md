---
title: "Custom CSS"
date: 2020-11-01
description: "Obsidianのスタイルを改造する"
tags: [" #obsidian "]
aliases: [記事_Obsidianのスタイルを改造する]
---

# Obsidianのスタイルを改造する
更新日 : 2020-11-09

こんにちは。パダワンです。今日も短めの記事をパンと出したいと思います。
今日は簡単ですがObsidianのカスタムCSSを改造する方法を紹介します。

Ankiを使っている方は、HTMLとCSSを自分で書いてカードのテンプレートを作成したことがあると思います。なのでAnkiを使ったことがある人はとっつきやすいと思います。かくゆう私もAnkiでHTMLとCSSの基礎を学んびました。Ankiを使いながらHTMLとCSSを学ぶのはかなりおすすめです。

この記事の前提知識としてHTMLとCSSの知識(クラスとプロパティ、DeveloperToolの使い方)の知識が少し必要です。

HTMLとCSSを全く触ったことの無い方にはサイト"サルワカ"がおすすめです。次の2つの記事を見れば今回なにをやってるのか大体わかるようになります。私もお世話になりました。かなり分かりやすいので参考にしてみてください。

- [初心者向けHTML入門：書き方の基本とタグの使い方](https://saruwakakun.com/html-css/basic/html)
- [初心者向けCSS（スタイルシート）入門：基本的な書き方を総まとめ！](https://saruwakakun.com/html-css/basic/css)


## 0. 全体の流れ
CSSファイルを改造するにあたっての全体の流れです。
全体として6つの工程があります。

1. 準備としてテキストエディタをインストール
2. Obsidianの設定画面を開き、 プラグインの項目から Custom CSS の設定をONにする
1. Community Themes で好きなテーマを選び、Useを押してCSSファイルをダウンロード
1. obsidian.cssがつくられるので、別名でそれのバックアップを作る
2. CSSファイルの中身を知る
1. Developer Toolで要素を調べる
1. CSSファイルを調整して実際の表示を確認しながら好きな見た目にする


## 1. 準備

まずObsidianのスタイルシートを改造するにあたって必要なのものがテキストエディタです。VSCodeやAtom等を入れてください。これでCSSのSyntax highlight(コードに色をつけて見やすくする)をすることができます。

- [Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)
- [Atom](https://atom.io/)

ちなみに最近はVS Codeがおすすめらしいです。


## 2. Custom CSSの設定をONにする

デフォルトでのスタイルではなく、Custom CSSを改造します。好きなテーマをインストールしてください。

設定の項目からプラグイン > Custom CSS と行き、ONにしてください。

![設定1](data/00002_customCSS.png)

## 3. Community Themesで好きなテーマを選ぶ

Community Themeから好きなテーマを選んでUseボタンをクリックしてください。そうすると`obsidian.css`というCSSファイルがVaultのディレクトリに作成されます。

![設定2](data/00009_customCSS.png)

## 4. obsidian.cssのバックアップを作る

`obsidian.css`ファイルは、Community Themeから新しいテーマを選択してUseするたびに上書きされるので、自分の改造したCSSファイルが上書きされないようにバックアップとしてファイルを複製します

まずは、ターミナルもしくはエクスプローラー/ファインダーからVaultとして選択してあるフォルダを開きます。そうするとそのフォルダ直下に`obsidian.css`ファイルが見つかります。

選択して、CSSファイルをデフォルトでテキストエディタで開けるように、情報の項目を開きます。デフォルトのappをテキストエディタにします。

![設定2 情報](data/00003_customCSS.png)
![設定3 情報](data/00004_customCSS.png)


次に隠しフォルダとして`.themes`という名でCSS専用のフォルダを作成します。その中にobsidian.cssをわかりやすい名前をつけて複製保存してください。

`テーマ名_日にち.css`とかで良いです。

これでCSSを改造するための準備が終わりました。今後、改造が終わる度にobsidian.cssの内容を`Cmd+A`で全選択してコピーし、バックアップファイルにペーストしてください。

## 5. CSSファイルの中身を知る

では`obsidian.css`ファイルをダブルクリックで開いてみてください。テキストエディタが立ち上がります。

CSSファイルを改造する際にテーマの更新がある場合があるので、どこに何を追加したか変更したかをファイル冒頭なのでにメモしておいてください。バグがあった場合に、テーマの更新をして治すのでその際に、自分の改造した部分がわかるようにしておきます。

コメントアウトして内容等を書いておいてください。

```css
/* 
2020/11/01 
- テキストカラーを変更
*/
```

### 5-1. CSSカスタムプロパティ

複数のテーマで、CSSカスタムプロパティが使われています。
CSSカスタムプロパティは、CSSのプロパティを変数として扱って、色などのプロパティをまとめた場所で管理できるようになります。

参考 : [CSS カスタムプロパティ (変数) の使用 - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/Using_CSS_custom_properties)

>複雑なウェブサイトには、膨大な量の CSS があり、しばしば同じ値が使われています。たとえば、同じ色が異なる場所で数百使われており、色を変更する場合、グローバルに検索し、置き換えをしなくてはなりません。カスタムプロパティを使えば、一ヶ所に値を保存しておき、複数の場所から参照することができます。更なるメリットとして、意味的な識別をしやすくなります。たとえば、 `--main-text-color` は `#00ff00` より、とりわけ同じ色がさまざまな文脈で使われる場合は理解しやすいでしょう。

CSSを扱う上ではわかりやすいので、なるべくカスタムプロパティを使っているテーマを選ぶといいです。

おすすめのカスタムCSSテーマ
- [kepano/obsidian-minimal](https://github.com/kepano/obsidian-minimal)
- [TriDiamond/Obsidian-Obsidianite](https://github.com/TriDiamond/Obsidian-Obsidianite)
- [nickmilo/Cybertron](https://github.com/nickmilo/Cybertron)



使い方としては、CSS変数を次のように`:root`疑似クラスのプロパティとして定義するか、もしくは`theme-light`クラスと`theme-dark`クラスのプロパティとして定義します。

```css
:root {
	/* ノードグラフのカラー   */
	--graph-color-fill:red;
	--graph-color-circle:red; 
	--graph-color-line:rgb(126, 126, 126);
	--graph-color-text:red;
	--graph-color-fill-highlight:white;
	--graph-color-line-highlight:rgb(255, 255, 255);
}

.theme-light {
	/* ライトテーマでの色   */
	--graph-color-fill:white;
}
.theme-dark {
	/* ダークテーマでの色  */
	--graph-color-fill:blue;
}
```

使うときは次のようにCSSの`var()`関数の引数としてCSS変数を入れて利用します。

```css
.graph-view.color-fill {
	color:var(--graph-color-fill);
}
```

参考 : [var() - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/var)


例えば、Obsidianiteのテーマでは`obsidian.css`ファイルの冒頭にこのようにかいてあります。

```css
.theme-dark {
  --background-primary: #100e17;
  --background-primary-alt: #0d0b12;
  --background-secondary: #191621;
  --background-secondary-alt: #0d0b12;
  --text-normal: #bebebe;
  --text-accent: #0db9d7;
~~中略
}
```

`--text-normal:`の後の色を`#bebebe`から例えば`#aaaaaa`に変更すると`var(-text-normal)`で参照されている部分の色が一度に変更されます。この場合はテキストカラーが`#aaaaaa`に変更されます。

ちなみにこの`#aaaaaa`というのはHexコードと言います。

参考: [色の分類（HSV・RGB・HEX） | ウェブ制作 | 葛飾区のホームページ制作ワイズ](https://web.wiis.info/web-development/classification-of-colors-hsv-rgb-and-hex/)

### 5-2. 例.ノードグラフの色

実際にイジる部分としてはテーマごとでわかりやすくカスタムプロパティで管理してくれている場合は簡単です。
そのCSS変数の値を書き換えるだけです。

ですが、そうでない場合は自分で次のようにクラスそのものを書き加える必要があります。

```css
.graph-view.color-fill {
	/* ノードの色   */
	color:var(--graph-color-fill);
}
.graph-view.color-circle {
	/* ノード縁の色   */
	color:var(--graph-color-circle);
}
.graph-view.color-line {
	/* エッジラインの色   */
	color:var(--graph-color-line);
}
.graph-view.color-text {
	/* タイトルテキストの色   */
	color:var(--text-normal);
}
.graph-view.color-fill-highlight {
	/* ノード選択時のノードの色   */
	color: var(--graph-color-fill-highlight);
}
.graph-view.color-line-highlight {
	/* ノード選択時のエッジラインの色   */
	color:var(--graph-color-line-highlight);
}
```

obsidian.cssファイル内でテキストエディタで `Cmd+F`を押して`.graph-view`を検索すると出てきます。

無い場合は自分でコードを作成します。
こんな感じで色付けがされます。

![ノードグラフ](data/00014_customCSS.png)

## 6. Developer Toolで要素を調べる

この部分の色を変えたいが、どこのcssプロパティをいじればいいのかわからないということがあると思います。

そんなときにDeveloper Toolを使います。
`View > Toggle Developer Tools `を開く、もしくは `Cmd + Alt + I`を押すとDeveloper Toolが開きます。

![DeveloperTool](data/00015_customCSS.png)

要するにブラウザの検証ツールと同じです。
Obsidian自体がHTMLとCSSでレンダリングされているので、要素をクリックするとその要素のクラスやプロパティがわかるようになっています。


Developer Tool画面の左上の
`Select an element in the page to inspect it` をクリックするとカーソルを合わせて部分のHTML部分をハイライトしてくれます。
変えたい部分にカーソルをあわせてクリックしてクラス名とプロパティを調べます。

![DeveloperTool](data/00006_customCSS.png)

ちなみに`app.css`にすべてのデフォルトのクラス名やプロパティ値が記載されています。Developer ToolのSourceから見ることができます。デフォルト値なので変えない方がいいですね。Custom CSSのファイル`obsidian.css`に記載されてないこともあるので、注意してください。`app.css`をみればどんなクラスがあるのかがわかります。

![app.css](data/00005_customCSS.png)

参考: [Getting comfortable with Obsidian CSS - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/getting-comfortable-with-obsidian-css/133)

## 7. CSSファイルを調整して実際の表示を確認しながら好きな見た目にする

Obsidianを開きながら、テキストエディタで`obsidian.css`の変更を保存するとすぐにObsidianのレンダリングが更新されます。

ここでは、参考にいくつか例をあげてCSSコードを紹介します。

### 7-1. 変更部分の概要
基本的にスタイル変更する部分は次の3つのスペースで

- UI部分(workspace)
- Editor画面
- Preview画面

![テキストカラー変更](data/00016_customCSS.png)

改造しやすいのがEditorとPreview画面ですね。

大雑把な目安として
Editorのクラスは`.cm-`から始まります。
Previewのクラスは`.markdown-preview-`から始まります。

例えば、`#` から始まる目次部分の色を変更したい場合はEditor画面なら`.cm-header`、Preview画面なら`.markdown-preview-view h1`です。

```css
  /* ========= editor画面の目次 ========= */
  .cm-header {
    color:var(--text-header-color) !important;
  } 
  
  /* ========= preview画面の目次 ========= */
  .markdown-preview-view h1, 
  .markdown-preview-view h2, 
  .markdown-preview-view h3, 
  .markdown-preview-view h4, 
  .markdown-preview-view h5, 
  .markdown-preview-view h6 {
    color:var(--text-header-color);
  }
```

こんな感じで`.cm-header`等を`cmd+F`で検索してその場所に記載されているコードを変更します。なければ自分で付け足します。

スタイルには優先度があるため、`!important`を記載しないと反映されないことがあるので、反映したいときは上のようにカスタムプロパティの後に`!important`を記載してください。

参考: [CSSでの表現の優先度](https://www.ankiyorihajimeyo.com/anki/font-and-textdecoration/#4-1-%E8%A1%A8%E7%8F%BE%E3%81%AE%E5%84%AA%E5%85%88%E5%BA%A6)


### 7-2. テキストカラーの変更

一例としてテキスト装飾の部分のコードを紹介します。
- `==`で囲まれるハイライト 
- `**`で囲まれるボールド
- `*`で囲まれるイタリック

の3つに関して色を変更します。

`.cm-` から始まるのがEditor画面
`.markdown-preview-` から始まるのがPreview画面のクラスです。
下のコードの例では、カンマを使ってEditorとPreviewの対応するクラスをまとめて変更しています。

```css
  /* ========= ハイライトカラーを変更========= */    
  .cm-s-obsidian .cm-highlight,
  .markdown-preview-view mark {
    color: var(--highlight-color-text) !important;
    background-color: var(--highlight-color-background) !important;
  }
  
  /* ========= ボールドに色を追加========= */    
  .cm-s-obsidian .cm-strong,
  .markdown-preview-view strong {
    color: var(--strong-color-text) !important;
  }
  
  /* ========= Preview画面だけボールドのフォントサイズ変更========= */    
  .markdown-preview-view strong {
    font-size: 1.3em;
  }
  
  /* ========= イタリックに色を追加========= */    
  .cm-s-obsidian .cm-em,
  .markdown-preview-view em {
    color: var(--italic-color-text) !important;
  }
```

カスタムプロパティで実際の色を指定してあげます。

```css
:root {
  --highlight-color-background: rgba(168, 14, 207, 0.56);
  --highlight-color-text: white;
  --strong-color-text:red;
  --italic-color-text:rgb(36, 193, 227);
}
```

そうすると以下のようになります。


![テキストカラー変更](data/00013_customCSS.png)

### 7-3. 選択時のテキストハイライト変更
テキストを選択時のハイライトの色を変更をします。

![選択時のハイライト](data/00012_customCSS.png)

```css
:root {
	--text-selection:red;
}

::selection { background:var(--text-selection); }
```


### 7-4. ドラッグゴーストの色を変更
タブをドラッグしたときのゴーストの色を変更します。

```css
.mod-drag {
  color: red;
  background-color: red;
} 

.drag-ghost {
  opacity:0.8;
  color: red;
  background-color: red;
} 
```


## CSS Common Hacks

Obsidianの公式Forumでの次のPostでおもしろい投稿があります。
CSSのハック方法が色々記載されています。

[Meta Post - Common CSS Hacks - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/meta-post-common-css-hacks/1978)

例えば、Dynalist風にListの表示にBullet pointをつけたりするためのコードなどが紹介されています。

```css
span.cm-formatting-list-ul {
  visibility: hidden !important;
 }
 span.cm-formatting-list-ul:after {
  content: '• ';
  margin-left: -14px;
  color: rgba(123, 108, 214); 
  visibility: visible !important;
 }
/* BULLET POINT RELATIONSHIP LINES */
.cm-hmd-list-indent .cm-tab,
ul ul {
  position: relative;
}
.cm-hmd-list-indent .cm-tab::before {
  left: 0;
  top: -5px;
  bottom: -4px;
}
ul ul::before {
  left: -13px;
  top: 0;
  bottom: 0;
}
.cm-hmd-list-indent .cm-tab,
ol ol {
  position: relative;
}
ol ol::before {
  left: -29px;
  top: 0;
  bottom: 0;
}
```

![bullet point](data/00011_customCSS.png)



カーソルをブロックに変更するなど

```css
/* Block Cursor */
.CodeMirror-cursor { 
  border-left-width: 0.5em;
  opacity: 0.75;
  background-color: red;
}
```

どんどん更新されているのでこまめにチェックしてみるとおもしろいと思います。


☟ Obsidianのカスタマイズについての次の記事です。合わせてお読みください。
[SCSS/SASS - ObsidianのスタイルをSCSSで作る| アンキヨリハジメヨ](https://www.ankiyorihajimeyo.com/obsidian/obsidian_scss/)