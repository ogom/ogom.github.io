---
layout: post
title:  第61回 Ruby/Rails勉強会に発表者で参加しました。
---

**[発表のスライド (Changelog on Blog)](http://ogom.github.io/slides/changelog_on_blog/slide.html)**

<div style="width: 50%">
<script async class="speakerdeck-embed" data-id="07a94fd0cd5f0131fa3126624a8aace7" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

## チェンジログを題材にRuby製のツールを紹介しました。

* Ruby製のおなじみのGitHubの`GitHub Pages`にチェンジログをホスティングします。
    * `Gitlab`もRuby製ですね。
* GitHub PagesnにはRuby製の静的サイトを生成ツールの`Jekyll`が利用できます。
    * Jekyllは`2系`がリリースされています。
* JekyllではRuby製のテンプレートエンジンの`Liquid`が使われています。
    * Ruby製のE-commerceの`Shopify`が開発をしています。


## nSumeを使ってデモをしました。

### サイトのジェネレート

Jekyllで`Bootswatch`のテーマが使える[nSume](http://nsume.org/)を利用します。

```
gem install nsume
mkdir example
cd example/
nsume init --site project
```

* 数回のコマンドで`Changelog`のサイトができます。
    * `Vagrant`っぽいサブコマンドにしています。

### チェンジログの追加

Jekyllは日付とタイトルの単位でファイルが作成されます。

```
nsume post 0.0.1
```

* `Markdown`で記述ができるのでカジュアルなチェンジログにしましょう。
    * Markdownは画像の表示にリンクも追加できます。さらに位置やサイズの調整が可能です。

<style>img[alt=octonsume] { display: block; margin-left: auto; margin-right: auto; width: 100px;} </style>
[![octonsume](https://raw.github.com/ogom/nsume/master/lib/generators/assets/img/octonsume.png)](http://nsume.org/)

### パブリックに公開

Githubに`example`のリポジトリを作ります。

```
git init
git checkout -b gh-pages
git add --all
git commit -m "Initial commit"
git remote add origin git@github.com:ogom/example.git
git push -u origin gh-pages
```

### ローカルでも確認

パブリックへの公開に`5分`もかかりませんが、ローカルでも確認できます。

```
nsume up
```

* `nsume up --provider=aws`で`s3`で公開する機能も実装できそうですね。


## チェンジログの書式

特に規定はありませんが、`git`のコミットメッセージのルールを統一するとログから生成できます。

```
git log --date=short --pretty=format:"%ad %an %s (#%h)"
```

## nSumeのおまけ

Railsで実装された`REST API`のドキュメントを生成します。

**[nSumeのサンプル](http://ogom.github.io/nsume-rails-example/docs/api/v1/products.html)**

* `RSpec`の結果からドキュメントを作成します。
* ステートマシン ダイアグラムを`Model`から生成します。
* エンティティ リレーションシップ ダイアグラムを`Schema`から生成します。

シーケンス ダイアグラム等は`PlantUML`から生成すればよいですね。

