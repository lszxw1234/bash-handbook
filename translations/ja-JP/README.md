# bash-handbook-ja-JP 
[![CC 4.0][cc-image]][cc-url]
[![NPM version][npm-image]][npm-url]
[![Gitter][gitter-image]][gitter-url]

これは、あんまり深くBashを学びたい人のために書かれたファイルです。
> **Tip** このファイルを基にしたインタラクティブワークショップ[**learnyoubash**](https://git.io/learnyoubash)を試してください。

# Node Packaged Manuscript
`npm`を利用し、このファイルをインストールができます：
```
$ npm install -g bash-handbook
```

コマンドラインで`bash-handbook`を実行ができます。実行した後、あなたが選択した`$PAGER`のマニュアルが開きます。さもないと、ここで読み続けるでも可能です。

ソースはこちらで入手ですかす：<https://github.com/denysdovhan/bash-handbook>

# 通訳

現在、**bash-handbook**の通訳バージョンはこちらです：
- [Português (Brasil)](/translations/pt-BR/README.md)
- [简体中文 (中国)](/translations/zh-CN/README.md)
- [繁體中文（台灣）](/translations/zh-TW/README.md)
- [한국어 (한국)](/translations/ko-KR/README.md)
- [日本語](/translations/ja-JP/README.md)

[**別の通訳を要求する**][tr-request]

[tr-request]: https://github.com/denysdovhan/bash-handbook/issues/new?title=Translation%20Request:%20%5BPlease%20enter%20language%20here%5D&body=I%20am%20able%20to%20translate%20this%20language%20%5Byes/no%5D

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
# 目次

- [序論](#序論)
- [シェルとモード](#shells-and-modes)
  - [インタラクティブモード](#interactive-mode)
  - [非インタラクティブモード](#non-interactive-mode)
  - [終了コード](#exit-codes)
- [コメント](#comments)
- [変数](#variables)
  - [ローカル変数](#local-variables)
  - [環境変数](#environment-variables)
  - [位置パラメータ](#positional-parameters)
- [シェル展開](#shell-expansions)
  - [ブレース展開](#brace-expansion)
  - [コマンド置換](#command-substitution)
  - [算術展開](#arithmetic-expansion)
  - [二重引用符と一重引用符](#double-and-single-quotes)
- [配列](#arrays)
  - [配列宣言](#array-declaration)
  - [配列拡張](#array-expansion)
  - [配列スライス](#array-slice)
  - [配列に要素を追加する](#adding-elements-into-an-array)
  - [配列に要素を削除する](#deleting-elements-from-an-array)
- [ストリーム、パイプ、リスト](#streams-pipes-and-lists)
  - [ストリーム](#streams)
  - [パイプ](#pipes)
  - [コマンド一覧](#lists-of-commands)
- [条件文](#conditional-statements)
  - [一次式と結合式](#primary-and-combining-expressions)
  - [if文を使う](#using-an-if-statement)
  - [case文を使う](#using-a-case-statement)
- [ループ](#loops)
  - [`for` ループ](#for-loop)
  - [`while` ループ](#while-loop)
  - [`until` ループ](#until-loop)
  - [`select` ループ](#select-loop)
  - [ループ制御](#loop-control)
- [関数](#functions)
  - [デバッグ](#debugging)
- [後書き](#afterword)
- [もっと学びたいですか？](#want-to-learn-more)
- [その他のリソース](#other-resources)
- [ライセンス](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 序論
もし君が開発者、あなたが時間の価値を知っています。作業プロセスを最適化する、それは開発者の仕事の最も重要な１つです。

効率性と生産性への道は、私たちは時々次のような動作を何度も何度も繰り返されなければならない：
*スクリーンショットを撮ってサーバーにアップロードする
*さまざまな形や形式のテキストを処理する
*異なる形式間でのファイル変換
*プログラムの出力をパースする

私たちの救世主、**Bash**を利用してください。

BashはGNUプロジェクトのために[Brian Fox] []によって書かれた[Bourneシェル]（https://en.wikipedia.org/wiki/Bourne_shell）に代わるフリーソフトウェアとしてのUnixシェルです。
1989年にリリースされ、長い間LinuxとmacOSのデフォルトシェルとして配布されてきました。

[ブライアンフォックス]：https://en.wikipedia.org/wiki/Brian_Fox_(computer_programmer）
<!-- link this format, because some MD processors handle '()' in URLs poorly -->

では、なぜ３０年以上前に書かれたことを学ぶ必要があるの？答えは簡単です。
これは今日、全てのUnixベースのシステムに効率的なスクリプトを作成するための最も強力、そして移植性が高いのツールの１つです。
そしてそれはあなたがbashを学ぶべき理由です。

このハンドブックでは、bashで最も重要な概念を例を使って説明します。 
この概説がお役に立てば幸いです。
