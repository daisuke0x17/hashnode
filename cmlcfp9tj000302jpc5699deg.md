---
title: "Overleaf で日本語を使えるようにする"
datePublished: Sat Feb 07 2026 14:53:26 GMT+0000 (Coordinated Universal Time)
cuid: cmlcfp9tj000302jpc5699deg
slug: overleaf-setup-japanese-support
tags: overleaf

---

## **結論**

1. 左上メニューからコンパイラを`LaTeX`に設定する
    
2. プロジェクトのルートディレクトリに`latexmkrc`ファイル（**拡張子不要**）を作成し、下記を記述する
    

```plaintext
$latex = 'platex';
$bibtex = 'pbibtex';
$dvipdf = 'dvipdfmx %O -o %D %S';
$makeindex = 'mendex %O -o %D %S';
```

## **はじめに**

私が所属している研究室では、論文執筆に [Overleaf](https://ja.overleaf.com/) を利用しています。Overleaf はインストール不要で LaTeX が使えるオンラインエディタです。しかし！デフォルトの設定では日本語入力ができません😅  
本記事では、Overleaf で日本語入力ができるようになるまでの手順をまとめました。

## **日本語入力に必要な設定**

プロジェクト開始時の状態では日本語を入力してもコンパルできません。  
以下の4つ（主に最初の3つ！）を設定して日本語入力ができるようにしましょう💪

### **1\. 左上メニューからコンパイラを**`LaTeX`に設定する

![](https://res.cloudinary.com/zenn/image/fetch/s--fO4SsM53--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/0bb8edf19cdb1e84d412a216.jpg%3Fsha%3D84460ff385e986952a0afaf5f2bc19640ff36738 align="left")

![](https://res.cloudinary.com/zenn/image/fetch/s--iQSSPyl_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/8438a465b9369304f06925dd.png%3Fsha%3Da94e30aa1500e98c2a9580fd6210c4b95a05fe47 align="left")

### **2\. プロジェクトのルートディレクトリに** `latexmkrc` というファイルを作成する

ルートディレクトリに`latexmkrc`というファイルを作成してください。  
**拡張子は不要**ですのでご注意ください。

![](https://res.cloudinary.com/zenn/image/fetch/s--mzDaYrk4--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/aa1adda07db1128be71338b1.png%3Fsha%3D2100be6c7ae95325d7ae72f2be5e0032888d5427 align="left")

### **3\.** `latexmkrc` ファイルに下記をコピペする

一旦無心でコピペしましょう。詳細については後ほど解説します。

```plaintext
$latex = 'platex';
$bibtex = 'pbibtex';
$dvipdf = 'dvipdfmx %O -o %D %S';
$makeindex = 'mendex %O -o %D %S';
```

### **4\.** `\documentclass{}`を確認する

学会のテンプレートでは既に設定されいると思いますが、念の為確認しておきましょう。文章クラスの種類については[こちら](https://medemanabu.net/latex/documentclass/)にまとまっていました。和文のクラスであれば問題ないです。

参考：[https://ja.overleaf.com/learn/latex/Japanese](https://ja.overleaf.com/learn/latex/Japanese)

## **latexmkrc の中身が知りたい**

これで日本語は入力できるようになりました。しかし、`latexmkrc` の中身を理解せずに使うのはムズムズしますよね。自分なりにですが何を設定しているのか調べてみました。間違っている箇所があればご指摘ください🙇‍♂️

* `$latex`  
    `.tex` ファイルをコンパイルする際のコマンドを指定します。日本語をコンパイルする際は `platex` を指定する。
    
* `$bibtex`  
    `.bib` ファイルをコンパイルする際のコマンドを指定します。日本語をコンパイルする際は `pbibtex` を指定する。
    
* `$dvipdf`  
    `latex` が出力した`DVI` ファイルを PDF に変換するコマンドを指定します。日本語を変換する際は `dvipdfmx` を指定する。
    
* `$makeindex`  
    索引を作成するコマンドを指定します。 `\usepackage{makeindex}` 利用時に必要になる。
    

参考：[https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=latex:latexmk%E3%81%AE%E8%A8%AD%E5%AE%9A](https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=latex:latexmk%E3%81%AE%E8%A8%AD%E5%AE%9A)

## **おわりに**

本記事では Overleaf で日本語入力ができるようになるまでの手順をまとめました。日本語入力の設定は、論文執筆のはじめの一歩になると思います。この記事が誰かのお役に立てば幸いです🙇‍♂️  
皆様の論文執筆が少しでも快適になりますように🤞