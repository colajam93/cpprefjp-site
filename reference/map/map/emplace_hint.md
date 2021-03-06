# emplace_hint
* map[meta header]
* std[meta namespace]
* map[meta class]
* function[meta id-type]
* cpp11[meta cpp]

```cpp
template <class... Args>
iterator emplace_hint(const_iterator hint, Args&&... args);
```

## 概要
要素が配置されるべき場所を示唆するパラメータ `hint` を使って、コンテナに新しい要素を挿入する。要素は直接構築される（コピーもムーブもされない）。要素のコンストラクタはこの関数に渡された引数と同じ引数で呼ばれる。


## パラメータ
- `hint` : 新しい要素をどこへ挿入するかを示唆するために使われるイテレータ
- `args...` : 要素のコンストラクタへ転送される引数パック


## 戻り値
新たな要素が追加された場合、その追加された要素を指すイテレータ。新たな要素が追加されなかった場合、既にあった要素を指すイテレータ。


## 計算量
一般にコンテナのサイズについて対数時間だが、新しい要素が `hint` の前に挿入された場合は償却定数時間。


## 例
```cpp example
#include <iostream>
#include <map>
#include <utility>

int main()
{
  std::map<int, char> m;

  m.emplace( 1, 'A' );

  // キー2の要素が最後尾に追加されることが事前にわかっているので、m.end()をヒントとして与える
  m.emplace_hint( m.end(), 2, 'B' );

  for( const auto& pr : m ) {
    std::cout << std::get<0>( pr ) << " " << std::get<1>( pr ) << std::endl;
  }

  return 0;
}
```
* emplace_hint[color ff0000]
* m.emplace[link emplace.md]
* m.end()[link end.md]
* std::get[link /reference/utility/pair/get.md]

### 出力
```
1 A
2 B
```


## バージョン
### 言語
- C++11

### 処理系
- [Clang, C++11 mode](/implementation.md#clang): 3.2
- [GCC, C++11 mode](/implementation.md#gcc): 4.8.5
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 11.0


## 関連項目

| 名前 | 説明 |
|-----------------------------------------------------------------------------------------|-----------------------------|
| [`map::emplace`](/reference/map/map/emplace.md) | 要素を直接構築する |
| [`map::insert`](/reference/map/map/insert.md) | 要素を挿入する |


## 参照
- [N2680 Proposed Wording for Placement Insert (Revision 1)](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2680.pdf)
