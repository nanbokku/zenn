---
title: "UnityでVSCodeのインテリセンスが効かないときの対処法"
emoji: "⚙"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unity", "vscode", "intellisense"]
published: true
---

新しいPCを購入したのでUnityの環境構築を再度行う必要がありました．
その際にVSCodeでインテリセンスが効かなくなったので対処法を残しておきます．

:::message
他の多くの記事にも載っている情報と内容は同じです．新規的な情報はありません．  
自分用の備忘録として書いています．
:::

# 環境

- Unity2019.4.12f1
- VSCode 1.50.1

# インストールしたもの

- Mono
- .NET Core
- (.NET Framework 4.7.1)
- .NET Framework 4.7.1 Developer Pack ★

## .NET Framework 4.7.1 Developer Pack について

```
The reference assemblies for framework ".NETFramework,Version=v4.7.1" were not found.
```

[.NET Framework 4.7.1 Developer Pack](https://www.microsoft.com/ja-JP/download/details.aspx?id=56119) をインストールしていない状態では OmniSharp の上記エラーが出ました．  
インストールするバージョンはエラーメッセージに表示されているものを選べば間違いないと思います．

ちなみに`.NET Framework 4.7.1`に関しては`winget`でインストールこそしましたが意味はなかったです．  
これをインストールしなくてもインテリセンスは効くかと思われます．  

エラーメッセージをよく読んでからインストールしよう...と反省．