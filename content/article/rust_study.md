---
title: "Rust お勉強記録"
date: 2025-02-19T22:28:29+09:00
tags: [ "Rust", "software development" ]
categories: "Programming"
---

作ってみたい Windows GUI アプリケーションがあり、ちょっと調べたところ Rust がよさそう。

全く触ってみたことがないので、チュートリアル代わりに https://doc.rust-jp.rs/book-ja/title-page.html を読んでやってみる。

どうも `rustc` というのがコンパイラで C における `gcc` みたいな立ち位置らしい。さらに `cargo` というビルドシステム兼パッケージマネージャや `rustfmt` というフォーマッタも標準でついているらしい。

`cargo new <name>` を実行すると、最初のコードである main.rs やパッケージ (クレート？) の設定情報である Cargo.toml などの生成と (デフォルトでは) git repository の初期化が実行される。Git を使うか否か、代わりになんのバージョン管理システムを使うかなどは `cargo new --vcs <VCS> <name>` で設定できる。

Cargo で作成したディレクトリ内には Cargo.lock というファイルが生成される。このファイルはプロジェクト内の依存関係の正確なバージョンを記録しているらしい。ファイル内にも書かれているが、これは Cargo によって自動生成されるものなので、自分で触る必要はない。

TODO: https://doc.rust-jp.rs/book-ja/ch01-03-hello-cargo.html#cargo%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%82%92%E3%83%93%E3%83%AB%E3%83%89%E3%81%97%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B から続きを読む。