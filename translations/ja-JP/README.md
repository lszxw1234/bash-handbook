# bash-handbook-ja-JP 
[![CC 4.0][cc-image]][cc-url]
[![NPM version][npm-image]][npm-url]
[![Gitter][gitter-image]][gitter-url]

これは、あんまり深くBashを学びたい人のために書かれたファイルです。
> **Tip** このファイルを基にしたインタラクティブワークショップ[**learnyoubash**](https://git.io/learnyoubash)を試してください。

# Node Packaged Manuscript
`npm`を利用して、このファイルをインストールができます：
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

# 目次

- [序論](#introduction)
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
