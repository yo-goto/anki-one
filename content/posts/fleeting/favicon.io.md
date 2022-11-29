---
title: "favicon.io というサイト"
date: 2022-03-14
modified: 2022-11-02
tags: [Hugo, favicon, site]
aliases: 
description: "簡単にファビコンを作成できるサイト"
---

favicon って意外としっかりつくるのが面倒だったりするが、次のサイトを見つけた。

https://favicon.io

すごすぎる。

- image
- text
- emoji

から一瞬で favicon 用の画像を作成できる。ブログなどの簡単なサイトにはこれを使うようにしたい。

このブログの favicon にも emoji の犬を適用してみた。

Hugo の PaperMod テーマではダウンロードしたものを次の `static` ディレクトリにそのまま配置するだけで favicon を使用できる。

```shell
static
├── about.txt
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── apple-touch-icon.png
├── favicon-16x16.png
├── favicon-32x32.png
├── favicon.ico
└── site.webmanifest
```
