---
title: "supressions file を用いて valgrind の一部のエラー検出を抑制する"
date: 2023-10-02T23:02:24+09:00
tags: [ "valgrind", "debug" ]
categories: "Tips"
---

この記事は主に Valgrind User Manual の [2. Using and understanding the Valgrind core](https://valgrind.org/docs/manual/manual-core.html) を元に作成しました。

# 概要

valgrind を利用してメモリリークなどエラーの検出をしていると、自分の開発しているもの以外のエラーを検出してしまうことがある。場合によっては関係のないエラーが多すぎて自分の開発しているものに由来するエラーが見つけられなくなってしまうことがある。

その場合、valgrind の `--suppressions` オプションの引数に特定の形式のテキストファイルを渡すことで対象のエラーを抑制することができる。引数に渡すテキストファイルを最も簡単に生成するには、`--gen-suppressions=yes` を指定して valgrind を実行すればよい。検出されたエラー毎にそのエラーを抑制するための文字列を出力するか否か選べるので、必要なものを suppressions file にコピーすればよい。検出されたエラーすべてを抑制したい場合には `--gen-suppressions=all` を実行するとすべてのエラー毎に抑制するための文字列を出力する。

また、複数の `--suppressions` オプションを指定することで、複数の suppressions file を使ってエラーを抑制することができる。

# suppressions file の詳細

具体例としては `/usr/lib/valgrind/default.supp` を見るとよい。
suppressions file は個別の抑制を `{` と `}` で囲んだ中に指定し、`{` と `}` で囲まれたものを列挙するという形式になっている。この `{` と `}` は行頭に書かねばならない。以降、`{` と `}` で囲んだ中の記述方法について説明する。

## 1 行目

suppressions file の名前を書く。valgrind のログの summary に出力されるだけ。

## 2 行目

カンマ区切りで suppression 対象のツール名と、 その後ろにコロンと suppression そのものの名前を書く。例えば `tool_name1,tool_name2:suppression_name` のような形式になる。対象のツールに関係のない suppression は無視されるだけなので、とりあえず全てのツール名を書いておいてよい。

## 3 行目
2 行目に対する付加情報を書くらしい。省略可能っぽいがよくわからない。

## 残りの行
抑制したいエラーの原因となるものを指定する。共有オブジェクト、関数、ソースコードの行の指定が可能になっており、それぞれ `obj:`、`fun:`、`src:` で指定する。オブジェクト名と関数名、ファイル名の指定にはワイルドカード `*` と `?` を利用することが可能である。ソースコードの行は `filename:lineno` の形式で指定する。この行は `...` を指定してもよく、その場合フレームレベルのワイルドカードとなる (その階層はあってもよいし、いくつあってもよい)。

C++ では関数名はマングリング済みでなければならない。`--gen-suppressions` を指定するとき同時に `--demangle=no` を指定すればマングリング済みの関数名を取得することができる。

# おまけ

- suppressions file の拡張子は .supp らしい
- suppressions file は `#` 始まりの行をコメントとして認識する