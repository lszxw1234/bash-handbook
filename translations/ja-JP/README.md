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

- [Introduction](#introduction)
- [Shells and modes](#shells-and-modes)
  - [Interactive mode](#interactive-mode)
  - [Non-interactive mode](#non-interactive-mode)
  - [Exit codes](#exit-codes)
- [Comments](#comments)
- [Variables](#variables)
  - [Local variables](#local-variables)
  - [Environment variables](#environment-variables)
  - [Positional parameters](#positional-parameters)
- [Shell expansions](#shell-expansions)
  - [Brace expansion](#brace-expansion)
  - [Command substitution](#command-substitution)
  - [Arithmetic expansion](#arithmetic-expansion)
  - [Double and single quotes](#double-and-single-quotes)
- [Arrays](#arrays)
  - [Array declaration](#array-declaration)
  - [Array expansion](#array-expansion)
  - [Array slice](#array-slice)
  - [Adding elements into an array](#adding-elements-into-an-array)
  - [Deleting elements from an array](#deleting-elements-from-an-array)
- [Streams, pipes and lists](#streams-pipes-and-lists)
  - [Streams](#streams)
  - [Pipes](#pipes)
  - [Lists of commands](#lists-of-commands)
- [Conditional statements](#conditional-statements)
  - [Primary and combining expressions](#primary-and-combining-expressions)
  - [Using an `if` statement](#using-an-if-statement)
  - [Using a `case` statement](#using-a-case-statement)
- [Loops](#loops)
  - [`for` loop](#for-loop)
  - [`while` loop](#while-loop)
  - [`until` loop](#until-loop)
  - [`select` loop](#select-loop)
  - [Loop control](#loop-control)
- [Functions](#functions)
  - [Debugging](#debugging)
- [Afterword](#afterword)
- [Want to learn more?](#want-to-learn-more)
- [Other resources](#other-resources)
- [License](#license)
