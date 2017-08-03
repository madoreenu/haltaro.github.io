---
layout: post
title: Jekyll + GitHub Pagesでウェブサイトを立ち上げた
updated: 2017-07-30 12:00 
categories:
 - blog
 - draft
---

> 作成中

[Qiita](http://qiita.com/)に寄稿するほどではないけど，そこそこ技術的なメモが溜まってきた．これまでは[evernote](https://evernote.com/intl/jp/)を使ってきたが，数式やソースコードを書きづらい．[はてなブログ](http://hatenablog.com/)等で[Markdown](https://ja.wikipedia.org/wiki/Markdown)を書いても良いけど，手元にコンテンツが残らないのが嫌だったし，`haltaro`ドメインが取れなかった．ということで，[Jekyll](https://jekyllrb-ja.github.io/)と[GitHub Pages](https://pages.github.com/)で，ウェブサイトを自作することにした．

# 参考

ググればいくらでも記事が出て来る．特に，以下を参考にさせて頂いた:bow:

* [jekyll公式ドキュメント](https://jekyllrb-ja.github.io/docs/home/)
* [Windowsで游ゴシックが汚いのは、どう考えてもWebデザイナーが悪い？](https://www.cherrypieweb.com/weblog/technical/20160629025615.php)：`base-font-family`の指定について．

# 手順

## 1. GitHubアカウント取得

## 2. github.ioレポジトリ作成

## 3. Jekyllインストール

## 4. Jekyllテーマ選定

[Jekyll themes](http://jekyllthemes.org/)から，良さげなテーマを選ぶ．できるだけシンプルにしたかったことと，カテゴリ分類機能が欲しかったことから，[laobubu](https://github.com/laobubu)さんの[EasyBook](http://jekyllthemes.org/themes/easybook/)を使わせてもらうことにした．

## 5. カスタマイズ

### 5.1 フォントの変更

デフォルトだと日本語フォントが気持ち悪いので，`/css/main.scss`を次のように変更した．

```
$base-font-family: "Hiragino Maru Gothic W4 JIS2004", "游ゴシック", YuGothic, "ヒラギノ角ゴ ProN W3", "Hiragino Kaku Gothic ProN", "メイリオ", Meiryo, "Helvetica Neue", Helvetica, Arial, sans-serif;
$base-font-weight: 500;
$base-font-size:   16px;
$small-font-size:  $base-font-size * 0.875;
$base-line-height: 1.5;

$code-font-family:   Menlo, Monaco, Consolas, "DejaVu Sans Mono", "Liberation Mono", "Courier New", "Hiragino Maru Gothic W4 JIS2004", "游ゴシック", YuGothic, "ヒラギノ角ゴ ProN W3", "Hiragino Kaku Gothic ProN", "メイリオ", Meiryo, "Helvetica Neue", Helvetica, Arial, sans-serif;
$code-font-weight: 500; 
$code-font-size:     15px;
```

流行りの[游ゴシック](http://www.jiyu-kobo.co.jp/library/ygf/)なるものを使ってみた．`$*-font-familiy`および`$*-font-weight`については，[Windowsで游ゴシックが汚いのは、どう考えてもWebデザイナーが悪い？](https://www.cherrypieweb.com/weblog/technical/20160629025615.php)を参考にした．

### 5.2 連絡先の追加

連絡先に，`Qiita`と`Kaggle`を追加した．まず，`_includes/sidebar.html`に`Qiita`ボタンと`Kaggle`ボタンの設定を追記．

<script src="https://gist.github.com/haltaro/acaa8d617ea4fb598f6781ed1a8b916b.js"></script>

ちなみに，markdownにhtmlコードを直に書くと，ウェブサイト上では，自動変換されてソースコードが表示されない．上記では，[HTMLやCSSのソースコードをそのままページに貼り付ける方法](http://fukafuka295.jp/hp/hp_no9.html)を参考に，[Gist](https://gist.github.com/)を使って貼り付けた．

次に，`/_config.yml`に`qitta_username`と`kaggle_username`を追加した．

```yml
github_username: haltaro
qiita_username: haltaro #追加
kaggle_username: haltaro #追加
```

### 5.3 Projectページの追加

Projectをまとめたページを作りたかったので，`/project.md`を追加した．フロントマターは，`/about.md`を参考に作った．

```markdown
---
layout: page
title: Projects
permalink: /projects/
public: true
---

```

### 5.4 Gradatarの取得

## 6. 動作確認

## 7. アップロード

```bash
$ git add . -A
$ git commit -m "First commit"
$ git push origin master
```

# 感想

rubyとかcssとか全然わからんが，出来ないことは無かった[^1]．

[^1]: 結構ハマったけど．
