---
date: 2022-06-07
aliases: []
tags: [" #type/hugo  "]
---

## 概要
「アンキヨリハジメヨ」のドメイン更新を忘れたため、個人ブログとして新しく作り直した。記事もそこまで多くなかったので個人のミニブログとしての体裁にした。一応アーカイブとして記事もほぼ残したが、textlint などでリントしたり、若干修正もした。

構成は、Hugo のままだがテーマを変更して、ドメイン関連の管理を省略したかったので Netlify から Github Pages に変更した。

## textlint
`textlint-rule-spellcheck-tech-word` はショートコード内のリントをしてしまうのでアンインストールした。また、「思う」などの弱い表現は `ja-technical-writing/ja-no-weak-phrase` ブログなので許可した。

```json:.textlintrc
{
    "rules": {
        "ja-technical-writing/ja-no-weak-phrase": false
    }
}
```

