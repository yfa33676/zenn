---
title: "自然変換の計算"
emoji: "🗣️"
topics:
  - "圏論"
  - "自然変換"
  - "関手"
  - "域"
type: tech
published: true
---

## 自然変換の定義

$F$ と $G$ を関手 $C \rightarrow D$ とします。このとき $\theta : F \Rightarrow G$ が自然変換であるとは、任意の $C$ の対象 $a$ について、$D$ の射 $\theta_a : Fa \rightarrow Ga$ が一意に定まり、次の**自然性**を満たすことをいう。

#### 自然性

任意の $C$ の射 $f : a \rightarrow b$ について図式

$$
\begin{CD}
Fa @>Ff>> Fb \\
@V\theta_aVV @VV\theta_bV\\
Ga @>Gf>> Gb
\end{CD}
$$

が可換になる。つまり、

$$
Gf \circ \theta_a = \theta_b \circ F f
$$

が成り立つ。

## 域と余域

射 $f$ が $a \rightarrow b$ であるとは、$f$ の**域**（domain）が対象 $a$ であり、**余域**（codomain）が対象 $b$ であるということです。このことを $\mathrm{dom}$ と $\mathrm{cod}$ で、

$$
\begin{align*}
\mathrm{dom}(f) &= a \\
\mathrm{cod}(f) &= b \\
\end{align*}
$$

と書くことがあります。この記法をここでは次のようにしましょう。

$$
\begin{align*}
f_0 &= a \\
f_1 &= b \\
\end{align*}
$$

つまり、$f : f_0 \rightarrow f_1$ です。自然変換 $\theta$ には域と余域に当てはまるものが関手 $F$、$G$ と圏 $C$ と $D$ があります。これは

$$
\begin{align*}
\theta_0 &= F \\
\theta_1 &= G \\
\theta^0 &= C \\
\theta^1 &= D \\
\end{align*}
$$

としましょう。

## 自然変換の定義の書き換え

さて、この記法にすれば自然変換の自然性は

$$
\theta_1f \circ \theta f_0 = \theta f_1 \circ \theta_0 f
$$

になります。いわば一つの**可換性**として見ることができます。図式にすると

$$
\begin{CD}
\theta_0 f_0 @>\theta_0 f>> \theta_0 f_1 \\
@V\theta f_0VV @VV\theta f_1V\\
\theta_1 f_0 @>\theta_1f>> \theta_1 f_1 \\
\end{CD}
$$

です。ただし自然変換 $\theta$ と対象 $a$ から定まる射は $\theta_a$ という添字の記法ではなく適用の記法 $\theta a$ で表しています。

## 関手と自然変換

関手 $F$ の域と余域は圏になります。これを $F^0$ と $F^1$ としましょう。つまり、$F : F^0 \rightarrow F^1$ です。

$\theta$ を自然変換とします。$F^1 = \theta^0$ のとき自然変換 $\theta F$ 、$F^0 = \theta^1$ のとき自然変換 $F \theta$ を定められます。

### 関手の左作用

$F^1 = \theta^0$ のとき自然変換 $\theta F$ が定まります。域・余域は

$$
\begin{align*}
(\theta F)_0 &= \theta_0 F\\
(\theta F)_1 &= \theta_1 F\\
(\theta F)^0 &= F^0 \\
(\theta F)^1 &= \theta^1 \\
\end{align*}
$$

となります。このとき圏 $(\theta F)^0 = F^0$ の対象 $a$ から定まる射 $(\theta F)a$ は

$$
(\theta F)a = \theta(F a)
$$

と定めます。自然性を満たすかを確かめましょう。

$f$ を圏 $(\theta F)^0 = F^0$ の任意の射とすると、

$$
\begin{align*}
& (\theta F)_1f \circ (\theta F) f_0 \\
=& (\theta_1 F)f \circ \theta (F f_0) \\
=& \theta_1 (Ff) \circ \theta (F f)_0 \\
=& \theta (Ff)_1 \circ \theta_0 (F f) \\
=& \theta (F f_1) \circ (\theta_0 F) f \\
=& (\theta F) f_1 \circ (\theta F)_0 f 
\end{align*}
$$

により、自然性

$$
(\theta F)_1f \circ (\theta F) f_0 = (\theta F) f_1 \circ (\theta F)_0 f 
$$

が成り立つことが分かります。

### 関手の右作用

$F^0 = \theta^1$ のとき自然変換 $F \theta$ が定まります。域・余域は

$$
\begin{align*}
(F \theta)_0 &= F \theta_0\\
(F \theta)_1 &= F \theta_1\\
(F \theta)^0 &= \theta^0 \\
(F \theta)^1 &= F^1 \\
\end{align*}
$$

となります。このとき圏 $(F \theta)^0 = \theta^0$ の対象 $a$ から定まる射 $(F \theta)a$ は

$$
(F \theta)a = F (\theta a)
$$

と定めます。自然性を満たすかを確かめましょう。

$f$ を圏 $(F \theta)^0 = \theta^0$ の任意の射とすると、

$$
\begin{align*}
& (F \theta)_1f \circ (F \theta) f_0 \\
=& ( F\theta_1)f \circ F (\theta f_0) \\
=& F(\theta_1 f \circ \theta f_0) \\
=& F(\theta f_1 \circ \theta_0 f) \\
=& (F\theta) f_1 \circ (F\theta_0) f \\
=& (F\theta) f_1 \circ (F\theta)_0 f \\
\end{align*}
$$

により、自然性

$$
(F \theta)_1f \circ (F \theta) f_0 = (F\theta) f_1 \circ (F\theta)_0 f 
$$

が成り立つことが分かります。

### 自然変換の垂直合成

$\theta$、$\sigma$ を

$$
\begin{align*}
\theta_1 &= \sigma_0 \\
\theta^0 &= \sigma^0 \\
\theta^1 &= \sigma^1 
\end{align*}$$

が成り立つ自然変換とします。このとき自然変換 $\sigma \circ \theta$ が定められます。域・余域は

$$
\begin{align*}
(\sigma \circ \theta)_0 &= \theta_0\\
(\sigma \circ \theta)_1 &= \sigma_1\\
(\sigma \circ \theta)^0 &= \theta^0 = \sigma^0 \\
(\sigma \circ \theta)^1 &= \theta^1 = \sigma^1 \\
\end{align*}
$$

となります。このとき圏 $(\sigma \circ \theta)^0$ の対象 $a$ から定まる射 $(\sigma \circ \theta)a$ は

$$
(\sigma \circ \theta)a = \sigma a \circ \theta a
$$

と定めます。自然性を満たすかを確かめましょう。

$f$ を圏 $(\sigma \circ \theta)^0$ の任意の射とすると、

$$
\begin{align*}
& (\sigma \circ \theta)_1f \circ (\sigma \circ \theta) f_0 \\
=& \sigma_1 f \circ \sigma f_0 \circ \theta f_0 \\
=& \sigma f_1 \circ \sigma_0 f \circ \theta f_0 \\
=& \sigma f_1 \circ \theta_1 f \circ \theta f_0 \\
=& \sigma f_1 \circ \theta f_1 \circ \theta_0 f \\
=& (\sigma \circ \theta) f_1 \circ (\sigma \circ \theta) _0 f \\
\end{align*}
$$

により、自然性

$$
(\sigma \circ \theta)_1f \circ (\sigma \circ \theta) f_0 = (\sigma \circ \theta) f_1 \circ (\sigma \circ \theta) _0 f 
$$

が成り立つことが分かります。

### 自然変換の水平合成

$\theta$、$\sigma$ を

$$
\begin{align*}
\theta^1 &= \sigma^0 
\end{align*}
$$

が成り立つ自然変換とします。このとき、次が成り立ちます。

$$
\begin{align*}
\sigma \theta_1 \circ \sigma_0 \theta = \sigma_1 \theta \circ \sigma \theta_0
\end{align*}
$$

自然性と形式的には同じですが、関手と自然変換についての可換性という意味では違うものとなっています。

$a$ を $(\sigma \theta_1 \circ \sigma_0 \theta)^0$ の任意の対象として $(\sigma \theta_1 \circ \sigma_0 \theta)a$ を考えます。

$$
\begin{align*}
&(\sigma \theta_1 \circ \sigma_0 \theta)a \\
=&(\sigma \theta_1)a \circ (\sigma_0 \theta)a \\
=&\sigma (\theta_1 a) \circ \sigma_0 (\theta a) \\
=&\sigma (\theta a)_1 \circ \sigma_0 (\theta a) \\
=&\sigma_1 (\theta a) \circ \sigma (\theta a)_0 \\
=&(\sigma_1 \theta) a \circ (\sigma \theta_0) a \\
=&(\sigma_1 \theta \circ \sigma \theta_0) a \\
\end{align*}
$$

よって、

$$
\begin{align*}
\sigma \theta_1 \circ \sigma_0 \theta = \sigma_1 \theta \circ \sigma \theta_0
\end{align*}
$$

が成り立ちます。

