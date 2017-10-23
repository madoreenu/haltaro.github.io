---
layout: post
title: Windows7でJekyll+GitHub Pages
updated: 2017-10-15 17:00
categories:
 - jekyll
outline: 船便でアメリカから送ったため，2ヶ月ほどLinuxが使えなくなった．そこで，手元のWindowsノートPC（Windows 7 Professional, Service Pack 1, 64 bit）にJekyll+GitHub Pages環境を構築した．
---

船便でアメリカから送ったため，2ヶ月ほどLinuxが使えなくなった．そこで，手元のWindowsノートPC（Windows 7 Professional, Service Pack 1, 64 bit）に[Jekyll](https://jekyllrb-ja.github.io/)+[GitHub Pages](https://pages.github.com/)環境を構築した．

![env]({{site.baseurl}}/images/2017-10-15-env.png)

# 参考

* [OPC Diary，私家版Git For Windowsのインストール手順](http://opcdiary.net/?page_id=27065)：WindowsにおけるGit環境構築．
* [Git for Windows](https://git-for-windows.github.io/)：Windows用Git環境．
* [posh-git](https://github.com/dahlbyk/posh-git)：PowerShellでgitコマンド補完を可能にするツール．
* [KaoriYa，Windowsでjekyll 3.0（github-pages）を使う](https://www.kaoriya.net/blog/2016/02/07/)：WindowsにおけるJekyll環境構築方法．
* [RubyInstaller](https://rubyinstaller.org/downloads/)：RubyおよびDevKitのインストール．
* [ATOM](https://atom.io/)：GitHubが開発したテキストエディタ．

# 手順

## 1. Gitのインストール

 [OPC Diary，私家版Git For Windowsのインストール手順](http://opcdiary.net/?page_id=27065)を参考にした．
 1. [Git for Windows](https://git-for-windows.github.io/)をダウンロード．
 2. インストーラを起動し，基本的にデフォルト設定を選択．ただし，改行設定（`Configuring the line ending conversions`）では，上記サイトのおすすめに従い，`Checkout as-is, commit as-is`を選択．

## 2. Gitのグローバル設定

`Git bash`を起動し，上記サイトを参考にグローバル設定した．

```bash
$ git config --global user.name "haltaro"
$ git config --global user.email "***@gmail.com"
$ git config --global core quotepath false
```

## 3. GitのSSHキー作成

引き続き上記サイトを参考に，SSHキーを作成した．

1. スタートメニューから`Git GUI`を起動．
2. `Help > Show SSH Key`を選択．
3. `Generate Key`をクリックし，適当にpassphraseを入力．
4. 公開鍵をコピーして，`GitHub`のアカウントに登録．

## 4. posh-gitのインストール

[posh-git](https://github.com/dahlbyk/posh-git)を使うと，PowerShellでgitコマンド補完してくれて便利なので，インストールした． [OPC Diary，私家版Git For Windowsのインストール手順](http://opcdiary.net/?page_id=27065)のPsGetを使った方法だと上手くいかなかったので，[公式GitHub](https://github.com/dahlbyk/posh-git)から直接クローンした．以下はその詳細である．

まずは，PowerShellで以下のコマンドを打ち，[公式GitHub](https://github.com/dahlbyk/posh-git)からクローンする．ディレクトリはどこでも良い．

```
> git clone git@github.dahlbyk/posh-git.git
```

PowerShellのセキュリティ設定を変更した．

```
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Confirm
```

上記ディレクトリに移動して，`install.ps1`を実行した．

```
> .\install.ps1
```

## 5. Rubyのインストール

[RubyInstaller](https://rubyinstaller.org/downloads/)から2017年10月15日現在の最新版である`Ruby 2.4.2-2(x64)`をダウンロードした．

## 6. DevKitのインストール

Rubyのパッケージ管理システム`RubyGems`のインストールに必要な`DevKit`をインストールした．以下はその詳細である．

まず，[RubyInstaller](https://rubyinstaller.org/downloads/)から，`DevKit-mingw64-32-4.7.2-20130224-1151-sfx.exe`をダウンロードした．以下では`C:\DevKit`に解凍したと想定する．

次に，PowerShellから以下のコマンドを実行した．

```
> cd C:\DevKit
> ruby dk.rb init
> ruby dk.rb install
```

## 7. 関連パッケージのインストール

`RubyGems`を使い，`github-pages`と`wdm`をインストールした．

```
> gem install github-pages wdm
```

## 8. ATOMのインストール
マークダウンエディタが欲しかったので，[ATOM](https://atom.io/)をインストールした．[公式ページ](https://atom.io/)からインストーラをダウンロードすれば簡単にできた．

## 9. まとめ

下図のような環境が完成した．

![env]({{site.baseurl}}/images/2017-10-15-env.png)

PowerShellで`jekyll serve`して，ブラウザで`http://127.0.0.1:4000`から出来栄えを確認しながら，ATOMでマークダウンを編集できる．

# EasyBook特有の問題

本サイトは，[laobubu](https://github.com/laobubu)さんの[EasyBook](http://jekyllthemes.org/themes/easybook/)をベースにカスタマイズしたものである．Windows上でJekyllを実行すると，Linuxとは違った問題が発生した．

## サマリに記事全文表示

![outline]({{site.baseurl}}/images/2017-10-15-outline.png)

これまでは，各記事の先頭行を自動抽出し，サマリとして表示していた．しかし，本環境で作成した[武井由紀子，ユーザ中心ウェブビジネス戦略](https://haltaro.github.io/2017/10/14/web-buisiness)に関しては，なぜか記事全文が表示された．

いろいろと調べてみたが，原因がよくわからなかった[^1]．そこで苦肉の策として，`post.outline`という変数を新たに追加し，各記事でサマリを直接編集できるようにした．

<script src="https://gist.github.com/haltaro/4e89092ad36d14c6f5a50639452e0137.js"></script>

[武井由紀子，ユーザ中心ウェブビジネス戦略](https://haltaro.github.io/2017/10/14/web-buisiness)のフロントマターでは，次のようにoutlineを指定した．

<script src="https://gist.github.com/haltaro/8254c80f168f8a06bde0591551a8d49b.js"></script>

[^1]: ちゃんとソースコード読めばわかると思うが，時間切れ．

# 感想
ATOMは本当に便利．Linuxが届いたらインストールしようと思う．サマリ問題については，根本的な問題を解決できなかったのが残念．
