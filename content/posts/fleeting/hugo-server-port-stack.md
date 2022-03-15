---
title: "Hugo の localhost 番号が変わる現象"
date: 2022-03-14
tags: [Hugo]
aliases: ["Hugoのパスとの日付けについて"]
---

`hugo server` コマンドを使用した際にデフォルトで `localhost:1313` を使用して `http://localhost:1313/~` でプレビューを見られるはずだが、毎回ポート番号が変わってしまって開き直す必要があったので調べてみた。

次の記事が参考になった。

- [【Mac】占有portの調べ方と空け方](https://zenn.dev/json_hardcoder/articles/5925798786a07a)

```shell
❯ sudo lsof -P -i:1313
COMMAND   PID  USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
hugo    67762 roshi  254u  IPv4 0x2c5a9c113335d309      0t0  TCP localhost:1313 (LISTEN)
hugo    67762 roshi  255u  IPv4 0x2c5a9c11450548f1      0t0  TCP localhost:1313->localhost:49788 (CLOSED)
hugo    67762 roshi  256u  IPv4 0x2c5a9c113335f151      0t0  TCP localhost:1313->localhost:49789 (CLOSED)
hugo    67762 roshi  257u  IPv4 0x2c5a9c1144db2739      0t0  TCP localhost:1313->localhost:49794 (CLOSED)
hugo    67762 roshi  258u  IPv4 0x2c5a9c1143e56739      0t0  TCP localhost:1313->localhost:49797 (CLOSED)
hugo    67762 roshi  259u  IPv4 0x2c5a9c1145331d21      0t0  TCP localhost:1313->localhost:49798 (CLOSED)
hugo    67762 roshi  260u  IPv4 0x2c5a9c1143e13151      0t0  TCP localhost:1313->localhost:49804 (CLOSED)
hugo    67762 roshi  261u  IPv4 0x2c5a9c1141d0bb69      0t0  TCP localhost:1313->localhost:49802 (CLOSED)
```

- [sudo kill -9でプロセスを強制終了する - Qiita](https://qiita.com/nasuvitz/items/412a60b1e5e931cff24e)

PID を指定して `sudo kill -9` するとプロセスを強制終了できる。

```shell
❯ sudo kill -9 67762
```

上記のポートを専有しているっぽい `LISTEN` 状態のプロセスを `kill` することで `localhost:1313` が継続使用できるようになった。

```shell
❯ hugo server --minify --theme PaperMod
Start building sites …
hugo v0.94.2+extended darwin/arm64 BuildDate=unknown

                   | EN
-------------------+-----
  Pages            | 51
  Paginator pages  |  2
  Non-page files   | 87
  Static files     |  9
  Processed images |  0
  Aliases          | 26
  Sitemaps         |  1
  Cleaned          |  0

Built in 72 ms
Watching for changes in /Users/roshi/Documents/ALL-Repo/hugo-blog/hugo-repo/{archetypes,assets,content,data,layouts,package.json,static,themes}
Watching for config changes in /Users/roshi/Documents/ALL-Repo/hugo-blog/hugo-repo/config.yml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/anki-one/ (bind address 127.0.0.1)
```