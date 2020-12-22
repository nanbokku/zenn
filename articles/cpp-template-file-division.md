---
title: "C++ テンプレートのファイル分割"
emoji: "📄"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "テンプレート"]
published: true
---

C++ のテンプレートクラスのファイル分割についての自分用メモです．

# 基本

C++ のテンプレートは、基本的にヘッダファイルで宣言・定義しなければならない。
ヘッダファイルとソースファイルでファイル分割したい場合は、明示的に宣言をする必要がある。

```cpp:test_template.h
template <class T>
class TestTemplate
{
    public:
        TestTemplate() = default;

        T Add(T a, T b);
}
```
```cpp:test_template.cpp
#include "test_template.h"

template <class T>
T TestTemplate<T>::Add(T a, T b)
{
    return a + b;
}

// 明示的に宣言
template class TestTemplate<double>;
```
```cpp:main.cpp
#include "test_template.h"

int main()
{
    TestTemplate<double> test_template;
    double result = test_template.Add(1, 2);

    return 0;
}
```

しかし、テンプレートクラスに内部クラスや`typedef`宣言があった場合は、それについても明示する必要がある。

# 内部クラスや`typedef`宣言がテンプレートクラス内にある場合

```cpp:test_template2.h
template <class T>
class TestTemplate2
{
    public:
        struct InnerStruct
        {
            T member;
        }

        TestTemplate2() = default;

        void setMember(const InnerStruct& s);
        InnerStruct getMember() const;

    private:
        InnerStruct inner_;
}
```
```cpp:test_template2.cpp
#include "test_template2.h"

template <class T>
void TestTemplate2<T>::setMember(const InnerStruct& s)
{
    inner_ = s;
}

// typename が必要
template <class T>
typename TestTemplate2<T>::InnerStruct TestTemplate2<T>::getMember() const
{
    return inner_;
}

// 明示的に宣言
template class TestTemplate2<double>;
```

テンプレートは、テンプレート引数が確定するまで実体化されない。
そのため、コンパイラは`TestTemplate2<T>`を未知のクラスとして扱う。
そうなると、`TestTemlate2<T>::InnerStruct`はクラス名、メンバ変数のどちらに該当するかコンパイラはわからない。
このとき、**特に指定しないと、コンパイラはメンバ変数として取り扱う**ので、`InnerStruct`が型名であることを明示的に示すために、`typename`を指定する。

# 参考サイト

ありがとうございました．

https://teratail.com/questions/123776