---
title: "Hugo のポストの日付"
date: 2022-03-14
description: "Hugo のビルド時に未来の日付は認識されない"
tags: [Hugo, yaml]
aliases: [Hugoのパスとの日付けについて]
---

Hugo では未来の日付はポストとして認識されないっぽい。テーマの問題ではなく。

次のように記事のフロントマターに未来の日付を書いてしまうと、`hugo server --minify --theme PaperMod` などでプレビューしようとしてもこの記事は表示されない。従って、日付を一日前に戻しておく必要がある。

```diff yml:この記事のYAMLフロントマター
---
title: "Hugo のポストの日付"
- date: 2022-03-15
+ date: 2022-03-14
description: "Hugo のビルド時に未来の日付は認識されない"
tags: [Hugo]
aliases: ["Hugoのパスとの日付けについて"]
---
```

