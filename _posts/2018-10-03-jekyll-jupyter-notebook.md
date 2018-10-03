---
layout: post
title: JekyllにJupyter notebookを埋め込む
updated: 2018-10-03
cover:  "/assets/2018-10-03-blocks.jpg"
categories:
 - jekyll
 - python
#published: false
---

[red-data-tools/jekyll-jupyter-notebook - GitHub](https://github.com/red-data-tools/jekyll-jupyter-notebook)を使って，JekyllサイトにJupyter notebookを埋め込んでみた．

{::nomarkdown}
{% jupyter_notebook "/notebooks/2018-10-03-sample.ipynb" %}
{:/nomarkdown}


だめだ．どうやってもうまく表示されない．他の方法を試して見たほうが良いかもしれない．

このあたりを参考にするとか．

http://www.leeclemmer.com/2017/07/04/how-to-publish-jupyter-notebooks-to-your-jekyll-static-website.html
