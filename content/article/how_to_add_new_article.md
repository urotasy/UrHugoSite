---
title: "Hugo で新しいページを作成する方法"
date: 2025-02-16T16:00:46+09:00
tags: [ "Hugo", "software development" ]
categories: "Tips"
---

`hugo new` コマンドを使用して新しいファイルを追加する。

```
hugo new <path to new file>
```

ページの内容を編集し、 `hugot server` コマンドでテスト用のサーバを起動する。 `-D` オプションを指定することで、 draft: true のページも表示される。

```
hugo server -D
```

編集が完了したら作成された新規ファイルの draft: true を削除しておく。

最後に `hugo` コマンドを実行すると静的 HTML が生成される。