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
  - [終了コード](#終了コード)
- [コメント](#コメント)
- [変数](#変数)
  - [ローカル変数](#ローカル変数)
  - [環境変数](#環境変数)
  - [位置パラメータ](#位置パラメータ)
- [シェル展開](#シェル展開)
  - [ブレース展開](#ブレース展開)
  - [コマンド置換](#コマンド置換)
  - [算術展開](#算術展開)
  - [二重引用符と一重引用符](#二重引用符と一重引用符)
- [配列](#配列)
  - [配列宣言](#配列宣言)
  - [配列拡張](#配列拡張)
  - [配列スライス](#配列スライス)
  - [配列に素子を追加する](#配列に要素を追加する)
  - [配列に素子を削除する](#配列に要素を削除する)
- [ストリーム、パイプ、リスト](#ストリーム、パイプ、リスト)
  - [ストリーム](#ストリーム)
  - [パイプ](#パイプ)
  - [コマンド一覧](#コマンド一覧)
- [条件語句](#条件語句)
  - [一次式と結合式](#一次式と結合式)
  - [ifを使う](#ifを使う)
  - [caseを使う](#caseを使う)
- [ループ](#ループ)
  - [`for` ループ](#for-ループ)
  - [`while` ループ](#while-ループ)
  - [`until` ループ](#until-ループ)
  - [`select` ループ](#select-ループ)
  - [ループ制御](#ループ制御)
- [関数](#関数)
  - [デバッグ](#デバッグ)
- [後書き](#後書き)
- [もっと学びたいですか？](#もっと学びたいですか？)
- [その他のリソース](#その他のリソース)
- [ライセンス](#ライセンス)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 序論
もし君が開発者、あなたが時間の価値を知っています。作業プロセスを最適化する、それは開発者の仕事の最も重要な１つです。

効率性と生産性への道は、私たちは時々次のような動作を何度も何度も繰り返されなければならない：
*スクリーンショットを撮ってサーバーにアップロードする
*さまざまな形や形式のテキストを処理する
*異なる形式間でのファイル変換
*プログラムの出力をパースする

私たちの救世主、**Bash**を利用してください。

BashはGNUプロジェクトのために[Brian Fox][]によって書かれた[Bourneシェル](https://en.wikipedia.org/wiki/Bourne_shell)に代わるフリーソフトウェアとしてのUnixシェルです。
1989年にリリースされ、長い間LinuxとmacOSのデフォルトシェルとして配布されてきました。

[Brian Fox]: https://en.wikipedia.org/wiki/Brian_Fox_(computer_programmer)
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

また、`bash`の代わりに` sh`を使いたければ、 `#!/bin/bash`を`#!/bin/sh`に変更してください。この `#!`の文字列は[shebang](http://en.wikipedia.org/wiki/Shebang_%28Unix%29)として知られています。これで、次のようにスクリプトを実行することができます。

/path/to/script.sh

上の例では、便利なトリック`echo`を使って端末の画面にテキストを表示することです。

shebang行を使用するもう１つの方法は次の通りです：

```bash
#!/usr/bin/env bash
echo "Hello, world!"
```


このshebang行の利点は、環境変数PATHに基づいてプログラム（この場合はbash）を検索することです。
ファイルシステム上のプログラムの場所を常に想定できるとは限らないので、これは上で示した最初の方法よりもしばしば好まれます。
これはシステム上の `PATH`変数がプログラムの代替バージョンを指すように設定されている場合にも便利です。例えば、元のバージョンを保持したまま新しいバージョンの `bash`をインストールし、新しいバージョンの場所を` PATH`変数に挿入することができます。`#!/bin/bash`を使うと元の` bash`を使うことになりますが、`#!/user/bin/env bash`は新しいバージョンを使います。

## 終了コード

全てのコマンドには**終了コード**(**戻りテータス**あるいは**終了ステータス**)を返します。
成功したコマンドは常に `0 `（ゼロコード）、失敗したコマンドはゼロ以外の値（エラーコード）を返します。失敗コードは、1から255までの正の整数でなければなりません。
スクリプトを書く時に使えるもう一つの便利なコマンドは `exit`です。このコマンドは、実行中のスクリプトを終了して終了コードをシェルに配信するために使用されます。
引数なしで`exit`コードを実行すると、実行中のスクリプトを終了させ、`exit`の前に実行された最後のコマンドの終了コードを返します。

プログラムが終了すると、シェルはその**終了コード**を`$?`環境変数に割り当てます。
だから、`$?`変数はスクリプトの実行を成功したかどうか使用されます。

スクリプトを終了するために `exit`を使うことができるのと同じ方法で、
関数を終了して呼び出し元に** exit code **を返すために` return`コマンドを使うことができます。
関数の中でも `exit`を使うことができます。これは関数を終了し、プログラムも終了します。

# コメント

スクリプトには_コメント_を含むかもしれません。コメントは`shell`インタプリタを無視された特別なステートメントです。
それらは`#`記号で始まり、行末まで続きます。

例えば：

```bash
#!/bin/bash
# このスクリプトはあなたのユーザー名を表示します.
whoami
```
> ** Tip **：あなたのスクリプトが何をするのか説明するためにコメントを使ってください。

#　変数

ほとんどのプログラミング言語と同じ、bashで変数を作成することもできます。

Bashはデータの型を知りません。変数には、数字、または１文字以上の文字列を含めることができます。
作成できる変数には、ローカル変数、環境変数、そして位置引数３種類があります。

## ローカル変数

**ローカル変数**は、単一のスクリプト内にのみ存在する変数です。
他のプログラムやスクリプトからこの変数へのアクセスでないです。

ローカル変数は`=`記号を使って宣言することができて(ルールで、変数の名前 `=`とその値の間にはスペースがあってはいけません)、
その値は`$`記号を使って検索できます。例えば：

```bash
username="denysdovhan"  # 変数を宣言する
echo $username          # 値を表示する
unset username          # 変数を削除する
```

`local`キーワードを使って単一の関数に対してローカル変数を宣言することもできます。
そうすると、関数が終了した時に変数が消えます。

```bash
local local_var="I'm a local value"
```

## 環境変数

**環境変数**は、現在のシェルセッションで実行されているプログラムまたはスクリプトからアクセス可能な変数です。
それらはローカル変数のように作成されますが、代わりに`export`キーワードを使用します。

```bash
export GLOBAL_VAR="I'm a global variable"
```

bashにはたくさんのグローバル変数があります。あなたはこれらの変数にかなり頻繁に見るでしょう、
それでここに最も実用的な変数を見てみましょう：

| 変数     	　| 説明                                                   			|
| :----------- | :------------------------------------------------------------ 	|
| `$HOME`      | 現在のユーザーのホームディレクトリ。                           |
| `$PATH`      | シェルがコマンドを探すディレクトリリスト、コロンで区別する。 	|
| `$PWD`       | 現在作業中のディレクトリ。                                		|
| `$RANDOM`    | 0から32767までのランダム整数。                           		|
| `$UID`       | 現在のユーザーの実数ユーザーID。            	|
| `$PS1`       | プライマリプロンプト文字列。                                 	|
| `$PS2`       | セコンドりプロンプト文字列。                                 	|

この [リンク](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html#sect_03_02_04) に従って、Bashの環境変数の拡張リストを確認してください。

## 位置パラメータ

**位置パラメータ**は、関数が実行する時に割り当てられた変数で、位置的に与えられます。
次の表は、位置パラメータ変数と他の特殊変数、及び関数内にいるときの意味を示します。

| パラメータ     | 説明                                                 		|
| :------------- | :---------------------------------------------------------- 	|
| `$0`           | スクリプトの名前。                                           |
| `$1 … $9`      | 1番目から9番目までのパラメータリスト素子              		|
| `${10} … ${N}` | 10番目からN番目までのパラメータリスト素子                    |
| `$*` or `$@`   | `$0`以外の全ての位置パラメータ                      			|
| `$#`           | パラメータの数、`$0`は含みません                 			|
| `$FUNCNAME`    | 関数名(関数内のみの値があります) 					    	|

以下の例では、位置パラメータは`$0='./script.sh'`、`$1='foo'`及び`$2='bar'`になります。

  ./script.sh foo bar
  
変数には_デフォルト_値もあります。次の語法を使用して、そのように定義できます。

```bash
 # 変数が空の場合は、それらにデフォルト値を割り当てます。
: ${VAR:='default'}
: ${$1:='first'}
# or
FOO=${FOO:-'default'}
```

# シェル展開

_展開_はコマンドラインが_トークン_に分割された後で実行されます。つまり、これらの展開は、
算術演算を計算し、コマンドの実行結果などを保存するためのメカニズムです。

興味のある方は、[シェル展開について]（https://www.gnu.org/software/bash/manual/bash.html#Shell-Expansions）を読んでください。

## ブレース展開

ブレース展開により、任意の文字列を生成することができます。これは_ファイル名展開_と似ています。例えば：

```bash
echo beg{i,a,u}n # begin began begun
```

また、範囲を作成するためにブレース展開を使用することもできます。これはループ内で繰り返されます。

```bash
echo {0..5} # 0 1 2 3 4 5
echo {00..8..2} # 00 02 04 06 08
```

## コマンド置換

コマンド置換により、コマンドを実行した時、その値を別のコマンドまたは変数に割り当てに代入できます。
コマンドが````````または`$()`で囲まれているときにコマンド置換が行われます。例えば、次のように使用できます。

```bash
now=`date +%T`
# または
now=$(date +%T)

echo $now # 19:08:26
```

## 算術展開

bashでは、算術演算は自由に行えます。しかし、式は`$(())`で囲まなれけばなりません。
算術展開の形式は次のとおりです。

```bash
result=$(( ((10 + 5*3) - 7) / 2 ))
echo $result # 9
```

算術展開内では、変数は一般的に`$`接頭辞なしで使われるべきです：

```bash
x=4
y=7
echo $(( x + y ))     # 11
echo $(( ++x + y++ )) # 12
echo $(( x + y ))     # 13
```

## 二重引用符と一重引用符

二重引用符と一重引用符の間には重要な違いがあります。
二重引用符内の変数またはコマンド置換は展開されています。
一重引用符の中にはありません。例えば：

```bash
echo "Your home: $HOME" # Your home: /Users/<username>
echo 'Your home: $HOME' # Your home: $HOME
```

スペースを含む可能性がある場合は、ローカル変数と環境変数を引用符で囲む展開するときは注意してください。
無害な例として、ユーザ入力を表示するために `echo`を使うことを考えてください：

```bash
INPUT="A string  with   strange    whitespace."
echo $INPUT   # A string with strange whitespace.
echo "$INPUT" # A string  with   strange    whitespace.
```

最初の`echo`は５この引数を呼び出されます。$INPUTは単語に分割され、`echo`はそれぞれの間にスペース１つで表示します。
２番目のケースは、`echo`は単一の引数(スペースを含む全体の$INPUT値)で呼び出されます。

より深刻な例を考えみましょう。

```bash
FILE="Favorite Things.txt"
cat $FILE   # ファイル２つを表示します: `Favorite` と `Things.txt`
cat "$FILE" # ファイル１つを表示します: `Favorite Things.txt`
```

この例の問題はFILEを`Favorite-Things.txt`に改名することで解決できますが、
環境変数、位置パラメータ、または他のコマンドの出力(` find`、 `cat`など)からの入力を考えしてください。
入力にスペースが含まれる可能性がある場合は、展開を引用符で囲むように注意してください。


# License

[![CC 4.0][cc-image]][cc-url]

&copy; [Denys Dovhan](http://denysdovhan.com)

[cc-url]: http://creativecommons.org/licenses/by/4.0/
[cc-image]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg?style=flat-square

[npm-url]: https://npmjs.org/package/bash-handbook
[npm-image]: https://img.shields.io/npm/v/bash-handbook.svg?style=flat-square

[gitter-url]: https://gitter.im/denysdovhan/bash-handbook
[gitter-image]: https://img.shields.io/gitter/room/nwjs/nw.js.svg?style=flat-square
