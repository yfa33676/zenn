---
title: "モノイドについて～pointwiseとpointfree～"
emoji: "🗣️"
type: "tech"
topics:
  - "圏論"
  - "モノイド"
  - "カリー化"
  - "関数型プログラミング"
  - "随伴"
published: true
---

## モノイド
モノイドとは、

* **台集合**（underlying set）： 集合 $M$
* **乗法**（multiplication）： 二項演算子 $(\_) \cdot (\_) : M \times M \rightarrow M$
* **単位元**（unit）： 定数 $e \in M$

与えられたものです。合わせて $\langle M, (\_) \cdot (\_), e \rangle$ と表すことがあります。

### 乗法
乗法という場合は、**結合法則**（associative law）を満たしている二項演算を指す場合が多いです。結合法則とは、任意の $x, y, z \in M$ について、

$$
(x \cdot y) \cdot z = x \cdot (y \cdot z)
$$

が成り立つ、ということです。つまり、演算の順序が任意です。そのため、括弧で順序を強制する必要がありません。

乗法を**カリー化**（currying）しましょう。つまり、任意の $x \in M$ について、$\sigma^x : M \rightarrow M$ を次のように定義します。

$$
\sigma^x (y) = x \cdot y
$$

さて、$\sigma$ で結合法則は次の関数等式に書き換えられます。

$$
\sigma^{x \cdot y} = \sigma^x \circ \sigma^y
$$

確かめてみましょう。左辺に $z \in M$ を与えると、

$$
\sigma^{x \cdot y} (z) = (x \cdot y) \cdot z
$$

です。一方で、右辺に $z \in M$ を与えると、

$$
\sigma^x \circ \sigma^y (z) = \sigma^x (\sigma^y (z)) = x \cdot (y \cdot z)
$$

となります。たしかに、結合法則です。

### 単位元
$e \in M$ が単位元であるとは、任意の $x \in M$ について、**単位元則**（unit law）つまり、

* **左単位元則**： $e \cdot x = x$
* **右単位元則**： $x \cdot e = x$


が成り立つ、ということです。

左単位元則は $\sigma$ で書くと次のようになります。

* **左単位元則**： $\sigma^e = \mathrm{id}_M$

右単位元則はそうはいきません。右単位元則を表すためには、カリー化の定義を左右入れ替える必要があります。つまり、$\sigma^x : M \rightarrow M$ を、

$$
\sigma^x (y) = y \cdot x
$$

と定義するわけです。すると、$\sigma^e = \mathrm{id}_M$ は右単位元則 $e \cdot x = x$ を表します。

## 自己写像モノイド

任意の集合 $X$ について自己写像全体にもモノイドを与えられます。つまり、

* **台集合**（underlying set）： 集合 $X^X = \{f | f : X \rightarrow X\}$
* **乗法**（multiplication）： 関数合成 $(\_) \circ (\_) : X^X \times X^X \rightarrow X^X$
* **単位元**（unit）： 恒等写像 $\mathrm{id}_X \in X^X$

です。

さて、結合法則と左単位元則は $\sigma$ が $M$ から $M^M$ への**準同型**（morphism）であることと同じです。つまり、

$$
\begin{align*}
\sigma^{x \cdot y} &= \sigma^x \circ \sigma^y \\
\sigma^e &= \mathrm{id}_M
\end{align*}
$$

上記等式を可換図式で表しましょう。

$$
\begin{CD}
    1 + M \times M @> \lbrack e, (\_) \cdot (\_) \rbrack >> M \\
    @VV \mathrm{id}_1 + \sigma^{(\_)} \times \sigma^{(\_)} V @VV \sigma^{(\_)} V \\
    1 + M^M \times M^M @> \lbrack \mathrm{id}_M , (\_) \circ (\_) \rbrack >> M^M
\end{CD}
$$

上記可換図式は、直和 $+$ と直和の普遍射 $\lbrack \cdots \rbrack$ の記法に従っている。詳しくは記事「[場合分けと排他的論理和](https://zenn.dev/e_do_kiriko/articles/c7098e6300ec4f)」を見ていただければと思います。

図式を展開すれば、

$$
\begin{align*}
\sigma^{(\_)} \circ e &= \mathrm{id}_M \circ \mathrm{id}_1 \\
\sigma^{(\_)} \circ (\_) \cdot (\_) &= ((\_) \circ (\_)) \circ \sigma^{(\_)} \times \sigma^{(\_)}
\end{align*}
$$

となります。

## おわりに ～pint-freeとpoint-wise～
二項演算をあえてカリー化して、結合法則や単位元則を書き換えました。たとえば、

$$
(x \cdot y) \cdot z = x \cdot (y \cdot z)
$$

が

$$
\sigma^{(\_)} \circ (\_) \cdot (\_) = ((\_) \circ (\_)) \circ \sigma^{(\_)} \times \sigma^{(\_)}
$$

になります。カリー化によって得られるのは $x, y, z \in M$ ではなく、すべてを $1 \rightarrow M$ や $M \times M \rightarrow M$ などの写像の合成で表したものです。**要素**（point）に依存しないということで、**point-free** と言ったりします。その反対に従来的な記法は **point-wise** と言ったりします。

**関数型**プログラミング（**functional** programming）というのも、こういう側面があります。カリー化も関数型プログラミングの概念のひとつと言っていいでしょう。

カリー化は圏論では次のような随伴関係です。

$$
X \times Y \rightarrow Z \iff X \rightarrow Z^Y
$$

ここでは二項演算についての随伴ですので、

$$
M \times M \rightarrow M \iff M \rightarrow M^M
$$

として現れていました。左辺は二項演算で右辺はモノイドからモノイドへの写像です。もし、二項演算に結合法則や単位元の概念を与えると、右辺では準同型になる。このような視点の切り替えを可能にします。

今回は左から右へ視点を切り替えましたが、別の記事で書く予定の**始代数**を考える場合は右から左へ視点を移すことになります。つまり、**非カリー化**（uncurrying）です。

たとえば、自然数の**後者関数**（sucsessor）$\sigma : \mathbb{N} \rightarrow \mathbb{N}$ はカリー化すると $\sigma : 1 \rightarrow \mathbb{N}^\mathbb{N}$ になり、それを**拡張**すると $\sigma : \mathbb{N} \rightarrow \mathbb{N}^\mathbb{N}$ になります。これを非カリー化して得られるのが加法 $+ : \mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N}$ になります。

つまり、

$$
\mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N} \iff \mathbb{N} \rightarrow \mathbb{N}^\mathbb{N} \iff 1 \rightarrow \mathbb{N}^\mathbb{N} \iff \mathbb{N} \rightarrow \mathbb{N}
$$

という切り替えです。後者関数と加法の関係を表しています。より一般的には文字列上の連接とconsの関係を表しています。

$$
\Sigma^{*} \times \Sigma^{*} \rightarrow \Sigma^{*} \iff \Sigma^{*} \rightarrow \Sigma^{*^{\Sigma^{*}}} \iff \Sigma \rightarrow \Sigma^{*^{\Sigma^{*}}} \iff \Sigma \times \Sigma^{*} \rightarrow \Sigma^{*}
$$

詳しくは別の記事で書きます。