---
layout: post
title: JekyllとGitHub Pagesでウェブサイトを立ち上げた
updated: 2017-07-30 12:00 
categories:
 - blog
---


それなりに技術的なメモが溜まってきたが，[Qiita](http://qiita.com/)に投稿するほどではない．これまでは[evernote](https://evernote.com/intl/jp/)で管理していたが，数式やソースコードを書きづらい．[はてなブログ](http://hatenablog.com/)等で[Markdown](https://ja.wikipedia.org/wiki/Markdown)を書いても良いが，手元にコンテンツが残らないのが嫌だし，`haltaro`ドメインが取れなかった．そこで，[Jekyll](https://jekyllrb-ja.github.io/)と[GitHub Pages](https://pages.github.com/)で，ウェブサイトを立ち上げた．

# 参考

`jekyll github pages`等でググると素晴らしい記事がたくさん出てきた．今回は，特に，以下を参考にした．

* [jekyll公式ドキュメント](https://jekyllrb-ja.github.io/docs/home/)
* [How to Set Up a Jekyll Development Site on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-jekyll-development-site-on-ubuntu-16-04)：Ubuntu 16.04を使ってJekyllでウェブサイトを立ち上げる全般について．
* [Windowsで游ゴシックが汚いのは、どう考えてもWebデザイナーが悪い？](https://www.cherrypieweb.com/weblog/technical/20160629025615.php)：`*-font-family`および`*-font-weight`の設定について．
* [HTMLやCSSのソースコードをそのままページに貼り付ける方法](http://fukafuka295.jp/hp/hp_no9.html)：Gistを使ってソースコードをページに埋め込む方法について．

gitやGitHubの使い方は，もともと知っていたので割愛．

# 手順

なお，Ubuntu 16.04を想定する．

## 1. GitHubアカウント取得

[GitHub](https://github.com/)に登録し，アカウントを取得．もともと持ってた．

## 2. haltaro.github.ioレポジトリ作成

`<アカウント名>.github.io`レポジトリを作成．これも，もともと持ってた．

## 3. Jekyllインストール

[How to Set Up a Jekyll Development Site on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-jekyll-development-site-on-ubuntu-16-04)を参考に，以下のコマンドを実行．

```bash
$ sudo apt-get install ruby ruby-dev make gcc
$ sudo gem install jekyll bundler
```

ついでに，ローカル保存用のディレクトリを作成して移動．

```bash
$ mkdir haltaro.github.io
$ cd haltaro.github.io
```

## 4. Jekyllテーマ選定

[Jekyll themes](http://jekyllthemes.org/)から，テーマを選んだ．シンプルさと，カテゴリ分類機能という条件を満たす[laobubu](https://github.com/laobubu)さんの[EasyBook](http://jekyllthemes.org/themes/easybook/)を使わせてもらうことにした．

ダウンロードするなりクローンしたファイル一式を，先程のローカルディレクトリに保存．

## 5. カスタマイズ

### 5.1 フォントの変更

デフォルトだと日本語フォントが気持ち悪いので，`/css/main.scss`を次のように変更した．

<script src="https://gist.github.com/haltaro/e33a9c4992e80ac8c0c1f8ae946efa57.js"></script>

流行りの[游ゴシック](http://www.jiyu-kobo.co.jp/library/ygf/)を使ってみた．`$*-font-familiy`および`$*-font-weight`については，[Windowsで游ゴシックが汚いのは、どう考えてもWebデザイナーが悪い？](https://www.cherrypieweb.com/weblog/technical/20160629025615.php)を参考にした．

### 5.2 連絡先の追加

連絡先に，`Qiita`と`Kaggle`を追加した．まず，`_includes/sidebar.html`に`Qiita`ボタンと`Kaggle`ボタンの設定を追記．

<script src="https://gist.github.com/haltaro/acaa8d617ea4fb598f6781ed1a8b916b.js"></script>


次に，`/_config.yml`に`qitta_username`と`kaggle_username`を追加した．

<script src="https://gist.github.com/haltaro/dbbefa944f0072eda07c405e0fdb9762.js"></script>

### 5.3 Projectsページの追加

業績をまとめたページを作りたかったので，`/projects.md`を追加した．フロントマターは，`/about.md`を参考に作った．

```markdown
---
layout: page
title: Projects
permalink: /projects/
public: true
---
```

### 5.4 Grabatarの取得

丸窓にアイコンを表示するためには，[Gravatar](https://en.gravatar.com/)を設定して，ハッシュ値を`_config.yml`に追記する必要がある．[アバター画像を設定！Gravatar(グラバター)の登録方法と使い方](http://zaitaku-hukugyo-net.com/1132.html)を参考にした．

## 6. ローカルテスト

下記コマンドで動作確認．いくつかエラーが出たので，その都度ググって解決した．
```
$ jekyll serve
```
ブラウザで`localhost:4000`にアクセスすると，動作確認ができた．．

## 7. アップロード

```bash
$ git remote add origin git@github.com:haltaro/haltaro.github.io # アカウント名等は適宜変更のこと．
$ git add . -A
$ git commit -m "First commit"
$ git push origin master
```

しばらく経ってから，`https://haltaro.github.io`にアクセスすると，サイトが出来上がっていた．

# 感想

htmlとかcssとか全然わからんが，なんとか形になった．今後は，[googleアナリティクス](https://www.google.com/intl/ja/analytics/#?modal_active=none)と連携させたい．

