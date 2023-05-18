---
title: "モノイドについて～pointwiseとpointfree～"
emoji: "💨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

## モノイド
モノイドとは、

* **台集合**（underlying set）： 集合 $M$
* **乗法**（multiplication）： 二項演算子 $(\_) \cdot (\_) : M \times M \rightarrow M$
* **単位元**（unit）： 定数 $e \in M$

与えられたものです。合わせて $\langle M, (\_) \cdot (\_), e \rangle$ と表すことがあります。

### 乗法
乗法という場合には、**結合法則**（associative law）を満たしている二項演算を指します。結合法則とは、任意の $x, y, z \in M$ について、

$$
(x \cdot y) \cdot z = x \cdot (y \cdot z)
$$

が成り立つ、ということです。

さて、乗法を**カリー化**（currying）します。カリー化には左右がありえます。ここで、$\sigma^{(\_)}$, $\sigma_{(\_)} : M \rightarrow M^M$ を次のように定義します。ただし、$M^M$ は自己写像 $M \rightarrow M$ 全体の集合とします。

つまり、任意の $x \in M$ について $\sigma^{(\_)}$, $\sigma_{(\_)} : M \rightarrow M^M$ を次のように定めます。

$$
\begin{align*}
\sigma^x (y) &= x \cdot y \\
\sigma_x (y) &= y \cdot x
\end{align*}
$$

この定義から結合法則の等式は次のように書き換えられます。

$$
\begin{align*}
\sigma^{x \cdot y} (z) &= \sigma^x (\sigma^y (z)) \\
\sigma^{y \cdot z} (x) &= \sigma_z (\sigma_y (x)) 
\end{align*}
$$

もう少し書き換えましょう。右辺は関数合成の形にすれば、関数の等式になります。

$$
\begin{align*}
\sigma^{x \cdot y} &= \sigma^x \circ \sigma^y \\
\sigma_{y \cdot z} &= \sigma_z \circ \sigma_y \\
\end{align*}
$$


### 単位元
$e \in M$ が単位元であるとは、任意の $x \in M$ について、**単位元則**（unit law）つまり、

* **左単位元則**： $e \cdot x = x$
* **右単位元則**： $x \cdot e = x$


が成り立つ、ということです。

この等式を $\sigma$ で書き換えると次の二つの等式になります。

* **左単位元則**： $\sigma^e = \mathrm{id}_M$
* **右単位元則**： $\sigma_e = \mathrm{id}_M$

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
    @VV1 + \sigma^{(\_)} \times \sigma^{(\_)} V @VV \sigma^{(\_)} V \\
    1 + M^M \times M^M @> \lbrack \mathrm{id}_M , (\_) \circ (\_) \rbrack >> M^M
\end{CD}
$$