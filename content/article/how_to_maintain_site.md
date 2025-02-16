---
title: "このサイトのメンテナンス方法"
date: 2025-02-16T19:54:24+09:00
tags: [ "Hugo", "GitHub Pages", "software development" ]
categories: "Tips"
---

久しぶりにこのサイトの記事を更新しようとしたところ、やり方を完全に忘れてしまっていた。

まったく記憶に残っていないが、 https://github.com/urotasy/UrHugoSite に Hugo site が置かれており、そこから生成された HTML を https://github.com/urotasy/urotasy.github.io に commit して GitHub Pages でホスティングしている。 GitHub Pages で Hugo による HTML 生成を行う方法もあるようだが、現状では手動で `hugo` を実行して生成した HTML を commit, push している。以下、その手順を記録しておく。

1. https://github.com/urotasy/UrHugoSite を clone したレポジトリで `hugo new <new_page_path>` を実行して新しいページを作成して編集する。
2. `hugo server -D` などでテスト後、 `hugo` コマンドで public 以下のファイルを更新する
3. public 以下は https://github.com/urotasy/urotasy.github.io の submodule になっているので、まずそちらを commit, push する。そうすると https://urotasy.github.io/ が更新されるので、内容を確認する (少し時間がかかる場合がある)
4. UrHugoSite レポジトリで変更を commit, push する。このとき、 public 以下を更新するために `git submodule update --remote` を実行する (このあたりの順が正しいかまだ怪しい)
