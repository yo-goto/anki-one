---
title: "Github Pages に移行した"
date: 2022-03-14
description: "Github Pages で Hugo ブログをホストし、Github Actions で自動デプロイをやってみた"
tags: [Hugo, git/GitHub/pages, textlint]
---

「アンキヨリハジメヨ」のドメイン更新を忘れたため、個人ブログとして新しく作り直した。

記事もそこまで多くなかったので個人のミニブログとして新しく体裁を整えた。

Github Pages にした理由は、ドメインを意外といい感じにしてくるのが大きい。現時点でカスタムドメインにこだわっているわけではないのでリポジトリ名が最後につくだけでもよいかなと。

一応アーカイブとして記事もほぼ残したが、textlint などでリントしたり、記事も若干修正した。hugo の記事はリントしていなかったので、初めてやってみたが、誤字脱字・半角文字の使用など、まあひどかった。

## Hguo & Github Pages

構成は、Hugo のままだがテーマを変更して、ドメイン関連の管理を省略したかったので Netlify から Github Pages に変更した。

意外と簡単にいかなかったため、時間がかかってしまった。

Zenn や Qiita の記事を参考にしたが、変に応用したりしていたので、Hugo 公式ドキュメントと Github Actions のコードを作成した peaceiris さんの記事を見たら簡単にできた。

- [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/#build-hugo-with-github-action)
- [GitHub Actions による GitHub Pages への自動デプロイ](https://qiita.com/peaceiris/items/d401f2e5724fdcb0759d#user-and-organization-%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E5%A0%B4%E5%90%88)

デプロイキーやら ssh やら secret やらを結局作成せずに済んだのはシンプルな構成だったからかもしれない。

## Github Actions

Github Actions での自動デプロイを行うには次のファイル `.github/workflows/gh-pages.yml` をリポジトリに作成する。

- [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/#build-hugo-with-github-action)

```shell
$ mkdir -p .github/workflows/
$ touch .github/workflows/gh-pages.yml
```

次のコードを**そのまま**記載する(内容変更する必要ない)。

```yml:.github/workflows/gh-pages.yml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Github 側ではリポジトリの Settings > Pages の項目に移動して、 "Source" のところを `Branch: gh-pages` を選択して Save する。

- [簡単に Hugo サイトを GitHub Pages で（ 自動ビルドして ）公開する方法 - Qiita](https://qiita.com/normalsalt/items/406b31d2071db128bf0f)

これで終わり。`gh-pages` のブランチに公開用のファイルが生成されてプッシュのたびにデプロイできる。

## textlint

`textlint-rule-spellcheck-tech-word` はショートコード内のリントをしてしまうのでアンインストールした。また、「思う」などの弱い表現を指摘するルール `ja-technical-writing/ja-no-weak-phrase` はブログということもあって許可した。

```json:.textlintrc
{
  "rules": {
    "ja-technical-writing/ja-no-weak-phrase": false
  }
}
```

textlint については長い付き合いになりそうなので、今後も研究していきたいと思う。
