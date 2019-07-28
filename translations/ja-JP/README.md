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
- [シェルとモード](#シェルとモード)
  - [対話型モード](#対話型モード)
  - [非対話型モード](#非対話型モード)
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

#序論
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

# シェルとモード

ユーザーbashシェルは、対話型と非対話型２つのモートで動作します。

## 対話型モード

Ubuntuを使用している場合は、７つの仮想端末を利用できます。
デスクトップ環境は７番目の仮想端末で行われるので、`Ctrl-Alt-F7`キーバインディングを使って、わかりやすいGUIに戻ることができます。

`Ctrl-Alt-F1`キーバインドを使って、シェルを開きます。その後、GUIが消え、仮想端末の１つが表示されます。

このような何かを見るとき、インタラクティブモードで動いています：
user@host:~$

ここで、`ls`、` grep`、 `cd`、` mkdir`、 `rm`のような様々なUnixコマンドを入力して、それらの実行結果を見ることができます。

ユーザーと直接対話するので、対話型シェルと呼びます。

仮想端末を使うのはあまり便利ではありません。例えば、ファイルを編集して別のコマンドを同時に実行したい場合、次のよううな仮想端末エミュレータを使用することをお勤めします。

- [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal)
- [Terminator](https://en.wikipedia.org/wiki/Terminator_(terminal_emulator))
- [iTerm2](https://en.wikipedia.org/wiki/ITerm2)
- [ConEmu](https://en.wikipedia.org/wiki/ConEmu)

## 非対話型モード

非対話型モードでは、シェルはファイルまたはパイプからコマンドを読み取り、そしてそれらを実行します。インタプリタがファイルの終わりに達すると、シェルプロセスはこのセッションを終了して、親プロセスに戻ります。

	sh /path/to/script.sh
    bash /path/to/script.sh

上の例では、`script.sh`はシェルインタプリタが実行できるコマンドからなる通常のテキストファイルで、
`sh`や`bash`はシェルのインタプリタプログラムです。お好きなテキストエディタ（例：vim、nano、Sublime Text、Atomなど）を使って `script.sh`を作成できます。

`chmod`をコマンドを使ってスクリプトを簡単に実行可能なファイルに変更もできます：

	chmod +x /path/to/script.sh
	
さらに、スクリプトの最初の１行には、このファイルを実行使用するプログラムを指定する必要があります。

```bash
#!/bin/bash
echo "Hello, world!"
```

また、`bash`の代わりに` sh`を使いたければ、 `#!/bin/bash`を`#!/bin/sh`に変更してください。この `#!`の文字列は[shebang]（http://en.wikipedia.org/wiki/Shebang_%28Unix%29）として知られています。これで、次のようにスクリプトを実行することができます。

/path/to/script.sh

上の例では、便利なトリック`echo`を使って端末の画面にテキストを表示することです。

shebang行を使用するもう１つの方法は次の通りです：

```bash
#!/usr/bin/env bash
echo "Hello, world!"
```

このshebang行の利点は、環境変数PATHに基づいてプログラム（この場合はbash）を検索することです。
ファイルシステム上のプログラムの場所を常に想定できるとは限らないので、これは上で示した最初の方法よりもしばしば好まれます。これはシステム上の `PATH`変数がプログラムの代替バージョンを指すように設定されている場合にも便利です。例えば、元のバージョンを保持したまま新しいバージョンの `bash`をインストールし、新しいバージョンの場所を` PATH`変数に挿入することができます。 `＃！/ bin / bash`を使うと元の` bash`を使うことになりますが、 `＃！/ usr / bin / env bash`は新しいバージョンを使います。
