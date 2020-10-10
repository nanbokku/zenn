---
title: 'Unityで視錐台を使って画面内外判定'
emoji: '💭'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['unity']
published: true
---

ある範囲をカメラが映しているかという判定を行ったので備忘録として残しておきます．

:::message
「ある `GameObject` を (あるいは 1 点を) カメラが映しているか」という判定方法はよく見かけますが，今回はあくまでも「**ある範囲**をカメラが映しているか」です．
:::

子要素の`GameObject`が画面内に表示されているかを知りたかったのですが，子要素が多すぎたため，全てを判定していくより親要素の空の`GameObject`で判定をした方が処理が重くならないなあと思ったのでトライ．
親要素は**空の`GameObject`なので描画されませんが，判定したい範囲は決まっていた**のでカメラの視錐台を使う方法でできました．

# コード

```csharp
// 視錐台の平面を取得
Plane[] planes = GeometryUtility.CalculateFrustumPlanes(camera);

// 視錐台の内側にあるか
bool isRendered = GeometryUtility.TestPlanesAABB(planes, bounds);
```

- `GeometryUtility.CalculateFrustumPlanes`で取得できる平面は，視錐台の

  > [0] = Left, [1] = Right, [2] = Down, [3] = Up, [4] = Near, [5] = Far

- `GeometryUtility.TestPlanesAABB`は`bounds`が`planes`の内側にある場合か，何れかの`planes`と交差する場合に`true`を返す．

# 参考文献

- [GeometryUtility.TestPlanesAABB](https://docs.unity3d.com/ja/current/ScriptReference/GeometryUtility.TestPlanesAABB.html)
- [GeometryUtility.CalculateFrustumPlanes](https://docs.unity3d.com/ja/current/ScriptReference/GeometryUtility.CalculateFrustumPlanes.html)
