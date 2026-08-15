---
title:  "Spectral Theorem for Bounded, Self-Adjoint Operators"
date:   2026-08-02 11:20:00 +0200
categories: functional-analysis
---

Here we will state and prove the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators). This theorem sits at the core of much of AQFT, and extensive use of this theorem will be made in subsequent work.

Here, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

A note on conventions. Throughout this post, results that are standard and whose proofs lie outside the scope of the development---for instance the [**Heine–Borel Theorem**](#thrm:heine–borel-theorem), the [**Riesz Representation Theorem**](#thrm:riesz-representation), the [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass-real), and the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem)---are stated in full but not proven. They are marked as such by the absence of an accompanying **Proof**. Every other result stated here is proven in full.

# Spectral Theorem: Bounded Self-Adjoint Operators
In this section we will state and prove the Spectral Theorem for bounded, self-adjoint operators. However, we must introduce "extensive machinery" before we are able to state and prove the theorem. To that end we begin by examining some properties of bounded operators.

## Elementary Properties of Bounded Operators
In this section we will introduce and prove some relatively "elementary" properties of bounded operators that will be of use when proving the Spectral Theorem for bounded, self-adjoint operators. We begin by introducing some notation

> **Definition** *(Inner Product)*
<a name="def:inner-product"></a>
> An *inner product* on a complex vector space $$V$$ is a map $$\left< \cdot, \cdot \right> : V \times V \rightarrow \mathbb{C}$$ satisfying, for all $$\phi, \psi, \chi \in V$$ and $$c \in \mathbb{C}$$:
>
> 1. *(Conjugate symmetry.)* $$\left< \psi, \phi \right> = \overline{\left< \phi, \psi \right>}$$.
> 2. *(Positive definiteness.)* $$\left< \phi, \phi \right>$$ is real and non-negative, and $$\left< \phi, \phi \right> = 0$$ only if $$\phi = 0$$.
> 3. *(Conjugate-linear in the first argument, linear in the second.)* $$\left< c\phi, \psi \right> = \overline{c} \left< \phi, \psi \right>$$ and $$\left< \phi, c\psi \right> = c \left< \phi, \psi \right>$$.
> 4. *(Additivity.)* $$\left< \phi + \psi, \chi \right> = \left< \phi, \chi \right> + \left< \psi, \chi \right>$$ and $$\left< \phi, \psi + \chi \right> = \left< \phi, \psi \right> + \left< \phi, \chi \right>$$.
>
> Point 3 fixes the *physics* convention — the conjugate is taken on the **first** factor. This choice is load-bearing rather than cosmetic: several expansions below, the polarization formula and the $$b^2$$ inequality among them, change sign under the opposite convention. It is the convention used throughout this post and its sequel.

> **Definition** *(Norm Induced by an Inner Product)*
<a name="def:induced-norm"></a>
<!--  \uses{def:inner-product} -->
> Let $$V$$ be a complex vector space with an inner product. The *induced norm* is
>
> $$
>     \left\| \psi \right\| \equiv \sqrt{\left< \psi, \psi \right>},
> $$
>
> which is well defined by point 2 of [Definition (Inner Product)](#def:inner-product).

> **Definition** *(Bounded Operator Notation)*
<a name="def:bounded-operator-notation"></a>
<!--  \uses{def:inner-product} -->
<!--  \uses{def:induced-norm} -->
> Throughout, $$\mathbf{H}$$ denotes a separable, complex Hilbert space — a complex vector space with an inner product, complete with respect to the induced norm.
>
> A linear map $$A : \mathbf{H} \rightarrow \mathbf{H}$$ is *bounded* if there is a constant $$C \in \mathbb{R}$$ with $$\left\| A\psi \right\| \le C \left\| \psi \right\|$$ for all $$\psi \in \mathbf{H}$$. For such an $$A$$ the *operator norm* is the least such constant,
>
> $$
>     \left\| A \right\| \equiv \sup\limits_{\psi \ne 0} \frac{\left\| A\psi \right\|}{\left\| \psi \right\|} = \sup\limits_{\left\| \psi \right\| = 1} \left\| A\psi \right\|,
> $$
>
> the two suprema agreeing by homogeneity, and both being finite exactly when $$A$$ is bounded. It satisfies $$\left\| A\psi \right\| \le \left\| A \right\| \left\| \psi \right\|$$ for every $$\psi$$.
>
> We notate the set of bounded linear operators on $$\mathbf{H}$$ as $$\mathcal{B}(\mathbf{H})$$.

> **Convention** *(The Hilbert Space is Non-Zero)*
<a name="conv:nonzero-hilbert-space"></a>
<!--  \uses{def:bounded-operator-notation} -->
> Throughout this post $$\mathbf{H} \ne \{0\}$$.
>
> This is needed wherever non-emptiness of the spectrum is used: on the zero space the only operator is $$0$$, and $$A - \lambda\mathbf{1} = 0$$ is a bijection of $$\{0\}$$ onto itself with bounded inverse for every $$\lambda$$, so $$\sigma(A) = \emptyset$$ and the spectral radius would be a supremum over the empty set. Nothing is lost: on the zero space every statement below is vacuous.

### Preliminaries: Notation

Two pieces of notation are used pervasively throughout this post and are fixed here. We also fix that $$\mathbb{N} = \{0, 1, 2, \ldots\}$$ **includes** $$0$$, matching the convention of Lean and Mathlib; wherever an index must start at $$1$$ this is stated explicitly rather than left to the convention.

> **Definition** *(The Identity Operator)*
<a name="def:identity-operator"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{conv:nonzero-hilbert-space} -->
> $$\mathbf{1}$$ denotes the *identity operator* on $$\mathbf{H}$$, that is, the map $$\mathbf{1}\psi \equiv \psi$$ for every $$\psi \in \mathbf{H}$$. It is linear and bounded with $$\left\| \mathbf{1} \right\| = 1$$, so $$\mathbf{1} \in \mathcal{B}(\mathbf{H})$$. For $$\lambda \in \mathbb{C}$$, $$\lambda\mathbf{1}$$ denotes the operator $$\psi \mapsto \lambda\psi$$, and for $$A \in \mathcal{B}(\mathbf{H})$$ the operator $$A - \lambda\mathbf{1}$$ is $$\psi \mapsto A\psi - \lambda\psi$$, again an element of $$\mathcal{B}(\mathbf{H})$$.

> **Definition** *(Indicator Function)*
<a name="def:indicator-function"></a>
> If $$(X,\Omega(X))$$ is a measurable space and $$E \in \Omega(X)$$, the *indicator function* $$1_E : X \to \mathbb{C}$$ is defined by $$1_E(x) \equiv 1$$ for $$x \in E$$ and $$1_E(x) \equiv 0$$ for $$x \notin E$$. It is measurable, since $$1_E^{-1}(S) \in \{ \emptyset, E, X\setminus E, X\}$$ for every $$S \subset \mathbb{C}$$, and bounded by $$1$$. It satisfies $$1_E 1_F = 1_{E \cap F}$$ pointwise, and $$1_E + 1_F = 1_{E \cup F}$$ when $$E \cap F = \emptyset$$.

> **Definition** *(The Identity Operator and Indicator Functions)*
<a name="def:identity-and-indicator"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
> Retained as a compound reference to [Definition (The Identity Operator)](#def:identity-operator) and [Definition (Indicator Function)](#def:indicator-function), which now state these two unrelated notations separately. Citations of this anchor remain valid; new citations should prefer whichever of the two is actually needed.

We also fix the notation for the orthogonal complement of a subset, and record the basic properties of the Lebesgue integral that are used throughout — including the meaning of $$\int_E g \, d\nu$$, which appears repeatedly below.

> **Definition** *(Orthogonal Complement)*
<a name="def:orthogonal-complement"></a>
> If $$V \subset \mathbf{H}$$ is any subset, its *orthogonal complement* is
>
> $$
>     V^\perp \equiv \{ \psi \in \mathbf{H} \mid \left< \psi, v \right> = 0 \text{ for all } v \in V \}.
> $$

> **Proposition** *(Basic Properties of the Integral, and Integration over a Subset)*
<a name="prpstn:basic-integral-properties"></a>
<!--  \uses{def:indicator-function} -->
> Let $$(X,\Omega,\nu)$$ be a measure space.
>
> 1. *(Integration over a subset.)* For $$E \in \Omega$$ and $$g$$ measurable, $$\int_E g \, d\nu \equiv \int_X 1_E\,g \, d\nu$$, whenever the right-hand side is defined. This is the meaning of the notation $$\int_E g\,d\nu$$ throughout.
> 2. *(Linearity in the integrand.)* If $$g,h$$ are $$\nu$$-integrable and $$\alpha,\beta\in\mathbb{C}$$, then $$\alpha g + \beta h$$ is $$\nu$$-integrable and $$\int_X (\alpha g + \beta h)\,d\nu = \alpha\int_X g\,d\nu + \beta\int_X h\,d\nu$$. The same identity holds for nonnegative measurable $$g,h$$ and $$\alpha,\beta \ge 0$$, as an equality in $$[0,\infty]$$.
> 3. *(Monotonicity in the integrand.)* If $$g,h$$ are measurable with $$0 \le g \le h$$ pointwise, then $$\int_X g\,d\nu \le \int_X h\,d\nu$$ in $$[0,\infty]$$. In particular, if $$0 \le g \le c$$ on $$E$$ for a constant $$c$$, then $$\int_E g\,d\nu \le c\,\nu(E)$$.
> 4. *(Triangle inequality.)* If $$g$$ is $$\nu$$-integrable then $$\lvert \int_X g\,d\nu \rvert \le \int_X \lvert g \rvert\,d\nu$$.


Before proceeding we record two elementary continuity properties of the Hilbert space norm and inner product. Both are used repeatedly throughout this post, and so we state them once here rather than re-deriving them at each point of use. Their proofs rest on two standard inequalities, which we state first.

> **Proposition** *(Cauchy–Schwarz Inequality)*
<a name="prpstn:hall-a.43"></a>
> If $$V$$ is a space with an inner product, then for all $$\phi, \psi \in V$$, we have the *Cauchy–Schwarz inequality*
>
> $$
>     \lvert \left< \phi, \psi \right> \rvert^2 \le \left< \phi, \phi \right> \left< \psi, \psi \right>.
> $$
>
> Equivalently, writing $$\left\| \phi \right\| \equiv \sqrt{\left< \phi, \phi \right>}$$ for the norm induced by the inner product, one has
>
> $$
>     \lvert \left< \phi, \psi \right> \rvert \le \left\| \phi \right\| \left\| \psi \right\|.
> $$

> **Proposition** *(Reverse Triangle Inequality)*
<a name="prpstn:reverse-triangle-inequality"></a>
> Let $$V$$ be a normed space. Then for all $$\phi, \psi \in V$$
>
> $$
>     \left\lvert \left\| \phi \right\| - \left\| \psi \right\| \right\rvert \le \left\| \phi - \psi \right\|.
> $$

With these stated, we turn to the continuity properties themselves.

> **Proposition** *(Continuity of the Norm and Inner Product)*
<a name="prpstn:continuity-of-norm-and-inner-product"></a>
<!--  \uses{prpstn:hall-a.43} -->
<!--  \uses{prpstn:reverse-triangle-inequality} -->
> Let $$\mathbf{H}$$ be a Hilbert space and let $$\{ \psi_n \}_{n \in \mathbb{N}}$$ be a sequence in $$\mathbf{H}$$ converging to $$\psi \in \mathbf{H}$$. Then
>
> 1. *(Continuity of the norm)* $$\left\| \psi \right\| = \lim\limits_{n \rightarrow \infty} \left\| \psi_n \right\|$$.
> 2. *(Continuity of the inner product)* For any fixed $$\phi \in \mathbf{H}$$, $$\left< \psi, \phi \right> = \lim\limits_{n \rightarrow \infty} \left< \psi_n, \phi \right>$$ and $$\left< \phi, \psi \right> = \lim\limits_{n \rightarrow \infty} \left< \phi, \psi_n \right>$$.

**Proof**
**Part 1:** By the [**Reverse Triangle Inequality**](#prpstn:reverse-triangle-inequality), for any $$n \in \mathbb{N}$$

$$
    \left\lvert \left\| \psi_n \right\| - \left\| \psi \right\| \right\rvert \le \left\| \psi_n - \psi \right\|.
$$

As $$\psi_n \rightarrow \psi$$ the righthand side tends to $$0$$, and hence $$\left\| \psi_n \right\| \rightarrow \left\| \psi \right\|$$, the desired **Part 1** result.

**Part 2:** By the [**Cauchy–Schwarz Inequality**](#prpstn:hall-a.43), for any $$n \in \mathbb{N}$$

$$
    \left\lvert \left< \psi_n, \phi \right> - \left< \psi, \phi \right> \right\rvert = \left\lvert \left< \psi_n - \psi, \phi \right> \right\rvert \le \left\| \psi_n - \psi \right\| \left\| \phi \right\|,
$$

where we have used the additivity of the inner product in its first argument. As $$\psi_n \rightarrow \psi$$ and $$\left\| \phi \right\|$$ is a fixed finite real number, the righthand side tends to $$0$$, giving the first claim. An identical argument, using additivity in the second argument, gives the second claim. This is the desired **Part 2** result.

Combining **Part 1** and **Part 2** gives the desired result.$$\blacksquare$$

With that stated, we now give an "elementary" lemma that proves $$\mathcal{B}(\mathbf{H})$$ is a Banach space

> **Lemma** *(Bounded Operators form a Banach Space)*
<a name="lmm:bounded-operators-form-a-banach-space"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
> $$\mathcal{B}(\mathbf{H})$$ forms a Banach space under the operator norm.

**Proof**
By definition a Banach space is a normed vector space that is complete with respect to the distance function associated to its norm. Hence, we must prove that $$\mathcal{B}(\mathbf{H})$$ is a normed vector space that is complete with respect to the distance function associated to its norm.

The norm we place on $$\mathcal{B}(\mathbf{H})$$ is the operator norm. The operator norm is indeed a norm. Hence, $$\mathcal{B}(\mathbf{H})$$ is normed.

Next we must prove that $$\mathcal{B}(\mathbf{H})$$ is a vector space. Consider $$A, B \in \mathcal{B}(\mathbf{H})$$ as well as $$\alpha, \beta \in \mathbb{C}$$. As the operator norm is a norm we have

$$
\begin{align}
    \|\alpha A + \beta B\| &\le \|\alpha A\| + \|\beta B\| \\
                           &=    \lvert \alpha \rvert \, \|A\| + \lvert \beta \rvert \, \|B\| \\
                           &< \infty,
\end{align}
$$

where the final step follows from the fact that $$A, B \in \mathcal{B}(\mathbf{H})$$ and thus $$\|A\|$$ and $$\|B\|$$ are bounded with respect to the operator norm. This implies that $$\alpha A + \beta B$$ is bounded and thus a member of $$\mathcal{B}(\mathbf{H})$$. This in turn implies that $$\mathcal{B}(\mathbf{H})$$ is a vector space.

Finally we must prove that $$\mathcal{B}(\mathbf{H})$$ is complete with respect to the distance function associated to the operator norm.

Consider a Cauchy sequence $$\{A_i\}_{i \in \mathbb{N}}$$ in $$\mathcal{B}(\mathbf{H})$$. The definition of Cauchy sequence implies that for any $$\epsilon > 0$$ there exists an $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

$$
    \|A_i - A_j\| < \epsilon.
$$

Fix an arbitrary $$\psi \in \mathbf{H}$$. With this fixed $$\psi \in \mathbf{H}$$ consider the sequence $$\{A_i\psi\}_{i \in \mathbb{N}}$$ in $$\mathbf{H}$$. For any $$i,j \in \mathbb{N}$$ we have

$$
\begin{align}
    \|A_i\psi - A_j\psi\| &= \|(A_i - A_j)\psi\| \\
                          &\le \|A_i - A_j\| \, \|\psi\|,
\end{align}
$$

where the first line follows from linearity and the second line follows from the operator norm definition. As $$\{A_i\}_{i \in \mathbb{N}}$$ is a Cauchy sequence, for any $$\epsilon > 0$$ there exists an $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

$$
    \|A_i - A_j\| < \epsilon.
$$

Thus for such $$\epsilon$$, $$i$$, and $$j$$ we have

$$
    \|A_i\psi - A_j\psi\| < \epsilon \|\psi\|.
$$

This implies that $$\{A_i\psi\}_{i \in \mathbb{N}}$$ is a Cauchy sequence in $$\mathbf{H}$$.

In particular for the case $$\|\psi\| \neq 0$$ we can choose the $$\epsilon$$ to be $$\epsilon = \epsilon' / \|\psi\|$$, where $$\epsilon' > 0$$ is arbitrary. Using this the previous equation takes the form

$$
\begin{align}
    \|A_i\psi - A_j\psi\| &< \frac{\epsilon'}{\|\psi\|} \|\psi\| \\
                          &= \epsilon',
\end{align}
$$

proving that for an arbitrary $$\epsilon' > 0$$ there exists an $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

$$
    \|A_i\psi - A_j\psi\| < \epsilon'.
$$

In other words for $$\|\psi\| \neq 0$$ the sequence $$\{A_i\psi\}_{i \in \mathbb{N}}$$ is a Cauchy sequence in $$\mathbf{H}$$.

In the case $$\|\psi\| = 0$$ the sequence $$\{A_i\psi\}_{i \in \mathbb{N}}$$ consists only of zeros. Hence, it's trivially a Cauchy sequence.

As $$\mathbf{H}$$ is complete, this Cauchy sequence $$\{A_i\psi\}_{i \in \mathbb{N}}$$ converges to an element of $$\mathbf{H}$$. With this knowledge, we can define a map $$A : \mathbf{H} \rightarrow \mathbf{H}$$ pointwise as follows

$$
    A\psi \equiv \lim\limits_{i \rightarrow \infty} A_i\psi.
$$

As we have just proven, the fact that $$\{A_i\psi\}_{i \in \mathbb{N}}$$ is a Cauchy sequence implies this map is well-defined.

Linearity of $$A$$ follows from the fact that each $$\{A_i\}_{i \in \mathbb{N}}$$ is linear. In more detail, given $$\psi,\phi \in \mathbf{H}$$ and $$\alpha,\beta \in \mathbb{C}$$ we have

$$
\begin{align}
    A(\alpha\psi + \beta\phi) &\equiv \lim\limits_{i \rightarrow \infty} A_i (\alpha\psi + \beta\phi) \\
                              &= \lim\limits_{i \rightarrow \infty} \alpha A_i\psi + \beta A_i\phi \\
                              &= \lim\limits_{i \rightarrow \infty} \alpha A_i\psi + \lim\limits_{i \rightarrow \infty} \beta A_i\phi \\
                              &= \alpha \lim\limits_{i \rightarrow \infty} A_i\psi + \beta \lim\limits_{i \rightarrow \infty} A_i\phi \\
                              &= \alpha A\psi + \beta A\phi,
\end{align}
$$

proving $$A$$ is linear.

Next let us prove that $$\{A_i\psi\}_{i \in \mathbb{N}}$$ converges to $$A$$ in the operator norm.

As we previously established, for a fixed $$\psi \in \mathbf{H}$$ and any $$i,j \in \mathbb{N}$$ we have

$$
\begin{align}
    \|A_i\psi - A_j\psi\| &= \|(A_i - A_j)\psi\| \\
                          &\le \|A_i - A_j\| \, \|\psi\|.
\end{align}
$$

If this fixed $$\psi$$ is such that $$\|\psi\| = 1$$, then for any $$\epsilon > 0$$ there exists an $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

$$
\begin{align}
    \|A_i\psi - A_j\psi\| &\le \|A_i - A_j\| \, \|\psi\| \\
                          &= \|A_i - A_j\| \\
                          &< \epsilon.
\end{align}
$$

Fixing an $$i \ge N$$, recall that $$A$$ was defined pointwise by $$A\psi \equiv \lim\limits_{j \rightarrow \infty} A_j\psi$$, so that the sequence $$\{ A_i\psi - A_j\psi \}_{j \in \mathbb{N}}$$ converges in $$\mathbf{H}$$ to $$A_i\psi - A\psi$$. Hence, taking the limit as $$j \rightarrow \infty$$ we have, as a result of Part 1 of [**Proposition** *(Continuity of the Norm and Inner Product)*](#prpstn:continuity-of-norm-and-inner-product) and our previous result

$$
    \lim\limits_{j \rightarrow \infty} \|A_i\psi - A_j\psi\| = \|A_i\psi - A\psi\| \le \epsilon.
$$

As $$\epsilon$$ is independent of $$\psi$$, this limit holds uniformly for all $$\psi \in \mathbf{H}$$ that satisfy $$\|\psi\| = 1$$. Thus we can take the supremum over such $$\psi$$ to obtain

$$
    \|A_i - A\| \equiv \sup\limits_{\|\psi\| = 1} \|A_i\psi - A\psi\| \le \epsilon.
$$

This proves that $$\{A_i\}_{i \in \mathbb{N}}$$ converges to $$A$$ in the operator norm.

Finally let us prove that $$A$$ is bounded. For fixed $$i \ge N$$ we have

$$
\begin{align}
    \|A\| &=   \|A - A_i + A_i\| \\
          &\le \|A - A_i\| + \|A_i\| \\
          &\le \epsilon + \|A_i\| \\
          &< \infty,
\end{align}
$$

where the second line follows from the definition of a norm, the third from the fact that $$\{A_i\}_{i \in \mathbb{N}}$$ converges to $$A$$ in the operator norm, and the final from the fact that $$A_i$$ is an element of $$\mathcal{B}(\mathbf{H})$$ and is thus bounded. So we conclude that $$\|A\| < \infty$$ and thus $$A$$ is bounded.

So in conclusion every Cauchy sequence $$\{A_i\}_{i \in \mathbb{N}}$$ in $$\mathcal{B}(\mathbf{H})$$ converges in the operator norm to an operator $$A$$ that is linear and bounded, and thus $$A$$ is an element of $$\mathcal{B}(\mathbf{H})$$. This implies that $$\mathcal{B}(\mathbf{H})$$ is complete with respect to the distance function associated to the operator norm, the desired result.

So in summary we have proven that $$\mathcal{B}(\mathbf{H})$$ is a normed vector space that is complete with respect to the operator norm. Thus $$\mathcal{B}(\mathbf{H})$$ is a Banach space, the desired result. $$\blacksquare$$

With this first, elementary result out of the way, our next step is the introduction of several definitions required by the Spectral Theorem. The first of these is the notion of "bounded inverse"

> **Definition** *(Bounded Inverse)*
<a name="def:bounded-inverse"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
> The *bounded inverse* of $$A \in \mathcal{B}(\mathbf{H})$$ is an element $$B \in \mathcal{B}(\mathbf{H})$$ such that $$AB = BA = \mathbf{1}$$, where $$\mathbf{1} \in \mathcal{B}(\mathbf{H})$$ is the multiplicative identity element.

This is required to define the "spectrum" of an operator, which is required by much of what follows

> **Definition** *(Resolvent and Spectrum)*
<a name="def:bounded-operator-resolvent-and-spectrum"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-inverse} -->
> For $$A \in \mathcal{B}(\mathbf{H})$$, the *resolvent set* of $$A$$, denoted as $$\rho(A)$$, is the set of all $$\lambda \in \mathbb{C}$$ such that the operator $$(A - \lambda \mathbf{1})$$ has a bounded inverse. The *spectrum* of $$A$$, denoted by $$\sigma(A)$$, is the complement of $$A$$'s resolvent set $$\rho(A)$$ in $$\mathbb{C}$$. For $$\lambda$$ in the resolvent set of $$A$$ the bounded inverse of $$(A - \lambda \mathbf{1})$$, which we notate as $$(A - \lambda \mathbf{1})^{-1}$$, is called the *resolvent* of $$A$$ at $$\lambda$$.

## Spectral Theorem for Bounded Self-Adjoint Operators
In this section we will actually be able to state the Spectral Theorem. However, we will only be able to do so after introducing "substantial machinery" related to "projection-valued measures".

### Projection-Valued Measures
"Projection-valued measures" are "core" to the Spectral Theorem. Basically, they generalize the notion of a measure. A "projection-valued measure", instead of taking on positive, real-values as a standard measure does, takes on "bounded orthogonal projection" values. Formally, we define this by first introducing the notion of a "bounded orthogonal projection"

The adjoint is used from here onward; we fix it and its basic algebra before the first use.

> **Definition** *(Adjoint of a Bounded Operator)*
<a name="def:adjoint-bounded"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:inner-product} -->
<!--  \uses{thrm:hall-a.52} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$. For each $$\phi \in \mathbf{H}$$ the map $$\psi \mapsto \left< \phi, A\psi \right>$$ is a bounded linear functional on $$\mathbf{H}$$, so by [**Theorem** *(hall-a.52)*](#thrm:hall-a.52) there is a unique $$\chi \in \mathbf{H}$$ with $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi$$. The *adjoint* $$A^*$$ of $$A$$ is the map $$\phi \mapsto \chi$$, so that
>
> $$
>     \left< \phi, A\psi \right> = \left< A^*\phi, \psi \right> \qquad \text{for all } \phi, \psi \in \mathbf{H}.
> $$
>
> An operator $$A \in \mathcal{B}(\mathbf{H})$$ is *self-adjoint* if $$A^* = A$$, that is, if $$\left< \phi, A\psi \right> = \left< A\phi, \psi \right>$$ for all $$\phi, \psi \in \mathbf{H}$$.

> **Lemma** *(Algebraic Properties of the Adjoint)*
<a name="lmm:adjoint-algebra"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
> For all $$A, B \in \mathcal{B}(\mathbf{H})$$ and $$c \in \mathbb{C}$$:
>
> 1. $$(A + B)^* = A^* + B^*$$.
> 2. $$(cA)^* = \overline{c}\,A^*$$.
> 3. $$(AB)^* = B^*A^*$$, and hence $$(A^k)^* = (A^*)^k$$ for every integer $$k \ge 0$$.
> 4. $$(A^*)^* = A$$.
> 5. $$\mathbf{1}^* = \mathbf{1}$$.

**Proof**
Each part follows from uniqueness in [Definition (Adjoint of a Bounded Operator)](#def:adjoint-bounded): it suffices to exhibit an operator satisfying the defining identity.

*Part 1.* $$\left< \phi, (A+B)\psi \right> = \left< \phi, A\psi \right> + \left< \phi, B\psi \right> = \left< A^*\phi, \psi \right> + \left< B^*\phi, \psi \right> = \left< (A^*+B^*)\phi, \psi \right>$$.

*Part 2.* $$\left< \phi, cA\psi \right> = c\left< \phi, A\psi \right> = c\left< A^*\phi, \psi \right> = \left< \overline{c}A^*\phi, \psi \right>$$, the last step because the inner product is conjugate-linear in its first argument.

*Part 3.* $$\left< \phi, AB\psi \right> = \left< A^*\phi, B\psi \right> = \left< B^*A^*\phi, \psi \right>$$. Induction on $$k$$ then gives $$(A^k)^* = (A^*)^k$$, the case $$k=0$$ being Part 5.

*Part 4.* $$\left< \phi, A^*\psi \right> = \overline{\left< A^*\psi, \phi \right>} = \overline{\left< \psi, A\phi \right>} = \left< A\phi, \psi \right>$$, using conjugate symmetry twice.

*Part 5.* $$\left< \phi, \mathbf{1}\psi \right> = \left< \phi, \psi \right> = \left< \mathbf{1}\phi, \psi \right>$$.$$\blacksquare$$

> **Definition** *(Orthogonal Projection)*
<a name="def:bounded-orthogonal-projection"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-operator-notation} -->
> A *bounded orthogonal projection*, sometimes shortened to *orthogonal projection* or simply *projection*, is an element $$P \in \mathcal{B}(\mathbf{H})$$ such that $$P^2 = P$$ and $$P^* = P$$.

Orthogonal projections are norm-decreasing, a fact used repeatedly below.

> **Lemma** *(Orthogonal Projections are Norm-Decreasing)*
<a name="lmm:projection-norm-decreasing"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{prpstn:hall-a.43} -->
> Let $$P \in \mathcal{B}(\mathbf{H})$$ be a bounded orthogonal projection. Then $$\left\| P\psi \right\| \le \left\| \psi \right\|$$ for every $$\psi \in \mathbf{H}$$.

**Proof**
Using $$P^* = P$$ and $$P^2 = P$$ from the [definition of an orthogonal projection](#def:bounded-orthogonal-projection), and then [**Cauchy–Schwarz**](#prpstn:hall-a.43),

$$
    \left\| P\psi \right\|^2 = \left< P\psi, P\psi \right> = \left< \psi, P^*P\psi \right> = \left< \psi, P\psi \right> \le \left\| \psi \right\| \left\| P\psi \right\|.
$$

If $$\left\| P\psi \right\| = 0$$ the claim is immediate; otherwise divide both sides by $$\left\| P\psi \right\| > 0$$ to obtain $$\left\| P\psi \right\| \le \left\| \psi \right\|$$.$$\blacksquare$$

The notion of a bounded orthogonal projection can then be employed to define a "projection-valued measure"

> **Definition** *(Projection-Valued Measure)*
<a name="def:projection-valued-measure"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
> Let $$X$$ be a set and $$\Omega(X)$$ a $$\sigma$$-algebra on $$X$$. A map $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ is called a *projection-valued measure* if the following properties are satisfied:
> 1. For each $$E \in \Omega(X)$$, it follows that $$\mu(E)$$ is a bounded orthogonal projection.
> 2. $$\mu(\emptyset) = 0$$, where $$\emptyset \in \Omega(X)$$ is the empty set, and $$\mu(X) = \mathbf{1}$$, where $$\mathbf{1}$$ is the multiplicative identity element.
> 3. If $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$ are pairwise disjoint, then for all $$v \in \mathbf{H}$$, we have
>
>    $$
>        \mu \left( \bigcup_{j = 1}^{\infty} E_j \right) v = \sum_{j = 1}^{\infty} \mu(E_j)v,
>    $$
>
>    where the convergence of the sum is in the norm topology on $$\mathbf{H}$$.
> 4. For all $$E_1, E_2 \in \Omega(X)$$, we have $$\mu(E_1 \cap E_2) = \mu(E_1) \mu(E_2)$$.
>
> Two projection-valued measures $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ and $$\nu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ are said to be *equivalent* if $$\mu(E) = \nu(E)$$ for all $$E \in \Omega(X)$$.

Now, we can associate a positive, real-valued measure $$\mu_\psi$$ to a projection-valued measure $$\mu$$ and any $$\psi \in \mathbf{H}$$ as follows:

> **Theorem** *(Projection-Valued Measure's Associated Measure)*
<a name="thrm:projection-valued-measures-associated-measure"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
> Given a projection-valued measure $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ and any $$\psi \in \mathbf{H}$$ the map $$\mu_\psi$$ defined by
>
> $$
> \begin{align}
>     \mu_\psi : \Omega(X) &\longrightarrow \mathbb{R} \\
>                       E  &\longmapsto \mu_\psi(E) \equiv \left< \psi, \mu(E) \psi \right>
> \end{align}
> $$
>
> defines a positive, real-valued measure $$\mu_\psi$$ on $$\Omega(X)$$.

**Proof**
To prove that $$\mu_\psi$$ defines a positive, real-valued measure on $$X$$ with $$\sigma$$-algebra $$\Omega(X)$$ we must prove
* **Empty set is of measure zero** - $$\mu_\psi(\emptyset) = 0$$, where $$\emptyset$$ is the empty set.
* **Non-negativity** - For all $$E \in \Omega(X)$$, it follows that $$\mu_\psi(E) \ge 0$$.
* **Countable additivity** - For pairwise disjoint $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$

$$
    \mu_\psi \left( \bigcup_{j = 1}^{\infty} E_j \right) = \sum_{j = 1}^{\infty} \mu_\psi(E_j).
$$

Let us first prove the empty set is of measure zero, i.e. $$\mu_\psi(\emptyset) = 0$$. The definition of $$\mu_\psi$$ along with the definition of the projection-valued measure $$\mu$$ imply

$$
\begin{align}
    \mu_\psi(\emptyset) &= \left< \psi, \mu(\emptyset) \psi \right> \\
                        &= \left< \psi, 0 \psi \right> \\
                        &= 0 \left< \psi, \psi \right> \\
                        &= 0.
\end{align}
$$

Hence, the empty set is of measure zero $$\mu_\psi(\emptyset) = 0$$ as desired.

Next let us prove non-negativity, i.e. for all $$E \in \Omega(X)$$, it follows that $$\mu_\psi(E) \ge 0$$. The definition of $$\mu_\psi$$, the projection-valued measure $$\mu$$, and of an orthogonal projection imply

$$
\begin{align}
    \mu_\psi(E) &= \left< \psi, \mu(E) \psi \right> \\
                &= \left< \psi, \mu(E) \mu(E) \psi \right>  \\
                &= \left< \psi, \mu(E)^* \mu(E) \psi \right>  \\
                &= \left< \mu(E) \psi, \mu(E) \psi \right>  \\
                &\ge 0,
\end{align}
$$

where the final step follows from the definition of an inner product. Thus, $$\mu_\psi(E) \ge 0$$ as desired.

Finally let us prove countable additivity. Let $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$ be pairwise disjoint. The definition of $$\mu_\psi$$ along with the definition of the projection-valued measure $$\mu$$ imply

$$
\begin{align}
    \mu_\psi \left( \bigcup_{j = 1}^{\infty} E_j \right) &= \left< \psi, \mu \left( \bigcup_{j = 1}^{\infty} E_j \right) \psi \right>  \\
                                                         &= \left< \psi, \sum_{j = 1}^{\infty} \mu(E_j) \psi \right>  \\
                                                         &= \sum_{j = 1}^{\infty} \left< \psi, \mu(E_j) \psi \right>  \\
                                                         &= \sum_{j = 1}^{\infty} \mu_\psi(E_j),
\end{align}
$$

where the third equality requires care: the sum $$\sum_{j=1}^\infty \mu(E_j)\psi$$ is a limit of partial sums in the norm topology, so linearity of the inner product alone gives only the *finite* case. Writing $$S_N \equiv \sum_{j=1}^N \mu(E_j)\psi$$, linearity gives $$\left< \psi, S_N \right> = \sum_{j=1}^N \left< \psi, \mu(E_j)\psi \right>$$ for each $$N$$, and $$S_N \to \sum_{j=1}^\infty \mu(E_j)\psi$$ in norm by property 3 of the [definition of a projection-valued measure](#def:projection-valued-measure); [**Proposition** *(Continuity of the Norm and Inner Product)*](#prpstn:continuity-of-norm-and-inner-product) then lets us pass to the limit in the second argument, giving the displayed equality. This implies

$$
    \mu_\psi \left( \bigcup_{j = 1}^{\infty} E_j \right) = \sum_{j = 1}^{\infty} \mu_\psi(E_j),
$$

which is the desired result.

Together these imply that $$\mu_\psi$$ defines a positive, real-valued measure $$\mu_\psi$$ on $$\Omega(X)$$. $$\blacksquare$$

Projection-valued measures give rise to a type of integration known as "operator-valued integration". The primary properties of "operator-valued integration" are described by the following theorem

> **Theorem** *(Operator-Valued Integration)*
<a name="thrm:operator-valued-integration"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{prpstn:Q-indicator-bounded-form} -->
<!--  \uses{prpstn:Q-measurable-bounded-form} -->
<!--  \uses{prpstn:Q-simple-bounded-form} -->
<!--  \uses{thrm:hall-a.52} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{lmm:lemma1-of-operator-valued-integration} -->
<!--  \uses{lmm:lemma2-of-operator-valued-integration} -->
<!--  \uses{prpstn:hall-a.61} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{lmm:lemma-1} -->
> Let $$\Omega(X)$$ be a $$\sigma$$-algebra on a set $$X$$ and let $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ be a projection-valued measure. Then there exists a unique linear map, denoted by
>
> $$
>     f \longmapsto \int_X f \, d\mu,
> $$
>
> from the space of bounded, measurable, complex-valued functions on $$X$$ into $$\mathcal{B}(\mathbf{H})$$ such that
>
> $$
>     \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f d\mu_\psi,
> $$
>
> for all $$f$$ and $$\psi \in \mathbf{H}$$, where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure's Associated Measure)*](#thrm:projection-valued-measures-associated-measure) and $$\left< \cdot, \cdot \right>$$ is the Hilbert space inner product on $$\mathbf{H}$$. 
>
> Its four basic properties — the integral of an indicator, the norm bound, multiplicativity, and the interaction with conjugation — are established separately in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), [**Proposition** *(Norm Bound for the Operator-Valued Integral)*](#prpstn:integral-norm-bound), [**Proposition** *(Operator-Valued Integration is Multiplicative)*](#prpstn:integral-multiplicative) and [**Proposition** *(Operator-Valued Integration Intertwines Conjugation and the Adjoint)*](#prpstn:integral-conjugation) below.

**Proof**

To streamline the proof of this theorem, we will introduce a few new terms

> **Definition** *((Bounded) Sesquilinear Form)*
<a name="def:bounded-sesquilinear-form"></a>
> A *sesquilinear form* on a Hilbert space $$\mathbf{H}$$ is a map $$L : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ that is conjugate linear in the first factor and linear in the second factor. A sesquilinear form $$L$$ is a *bounded sesquilinear form* if there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi, \psi \in \mathbf{H}$$
>
> $$
>     \lvert L(\phi, \psi) \rvert \le C \|\phi\| \, \|\psi\|,
> $$
>
> where $$\lvert\cdot\rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

> **Definition** *((Bounded) Quadratic Form)*
<a name="def:bounded-quadratic-form"></a>
<!--  \uses{def:bounded-sesquilinear-form} -->
> A *quadratic form* on a Hilbert space $$\mathbf{H}$$ is a map $$Q : \mathbf{H} \rightarrow \mathbb{C}$$ with the following properties:
>
> 1. $$Q(\lambda\psi) = \lvert\lambda\rvert^2 Q(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.
> 2. The map $$L : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by
>
>    $$
>    \begin{align}
>        L(\phi, \psi) &\equiv \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
>                      &-\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right]
>    \end{align}
>    $$
>
>    is a sesquilinear form on $$\mathbf{H}$$.
>
> A quadratic form $$Q$$ is a *bounded quadratic form* if there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$
>
> $$
>     \lvert Q(\phi) \rvert \le C \|\phi\|^2,
> $$
>
> where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

These will now let us begin the proof of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration).

By hypothesis we have a projection-valued measure $$\mu$$. Consider any bounded, measurable, complex-valued function $$f$$ on $$X$$ and any $$\psi \in \mathbf{H}$$. With this, let us define a map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

The next lemma uses the Complex-Valued Simple Approximation Theorem, which we state first.

> **Theorem** *(Complex-Valued Simple Approximation Theorem)*
<a name="thrm:complex-valued-simple-approximation-theorem"></a>
<!--  \uses{def:indicator-function} -->
> Let $$X$$ be a measurable space, i.e. a set equipped with a $$\sigma$$-algebra $$\Omega(X)$$. Given any bounded, measurable, complex-valued function $$f$$ on $$X$$, there exists a sequence of complex-valued simple functions $$\{s_i\}_{i \in \mathbb{N}}$$ on $$X$$---i.e. functions of the form $$s_i = \sum_{j = 1}^{n_i} \alpha_{ij} 1_{E_{ij}}$$ with $$\alpha_{ij} \in \mathbb{C}$$ and $$E_{ij} \in \Omega(X)$$ pairwise disjoint---such that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ on $$X$$.

where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure's Associated Measure)*](#thrm:projection-valued-measures-associated-measure). It turns out that such a $$Q_f(\psi)$$ is a bounded quadratic form which we now prove

> **Lemma** *(The Quadratic Form of a Bounded Measurable Function)*
<a name="lmm:lemma1-of-operator-valued-integration"></a>
<!--  \uses{prpstn:Q-indicator-bounded-form} -->
<!--  \uses{prpstn:Q-measurable-bounded-form} -->
<!--  \uses{prpstn:Q-simple-bounded-form} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
> Let $$\Omega(X)$$ be a $$\sigma$$-algebra on a set $$X$$ and let $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ be a projection-valued measure. For any bounded, measurable, complex-valued function $$f$$ on $$X$$ and any $$\psi \in \mathbf{H}$$ the map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ defined by
>
> $$
>     Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
> $$
>
> where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure's Associated Measure)*](#thrm:projection-valued-measures-associated-measure), is a bounded quadratic form.

**Proof**
The result is proved in three stages, each resting on the previous: for indicator functions in [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form), for simple functions in [**Proposition** *(The Quadratic Form of a Simple Function is Bounded)*](#prpstn:Q-simple-bounded-form), and for general bounded, measurable, complex-valued functions in [**Proposition** *(The Quadratic Form of a Bounded Measurable Function is Bounded)*](#prpstn:Q-measurable-bounded-form). The last of these is the statement of this lemma.$$\blacksquare$$

> **Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*
<a name="prpstn:Q-indicator-bounded-form"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
> Let $$\Omega(X)$$ be a $$\sigma$$-algebra on a set $$X$$ and let $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ be a projection-valued measure. For any $$E \in \Omega(X)$$ the map $$Q_{1_E} : \mathbf{H} \rightarrow \mathbb{C}$$, $$Q_{1_E}(\psi) \equiv \int_X 1_E \, d\mu_\psi$$, is a bounded quadratic form, with constant $$1$$.

**Proof**
Consider an arbitrary $$E \in \Omega(X)$$ and its indicator function $$1_E$$. In this case the definition of $$Q_{1_E}$$, standard properties of integration, and the definition of $$\mu_\psi$$ implies

$$
\begin{align}
    Q_{1_E}(\psi) &= \int_X 1_E \, d\mu_\psi \\
                  &= \int_E d\mu_\psi \\
                  &= \mu_\psi(E) \\
                  &= \left< \psi, \mu(E) \psi \right>.
\end{align}
$$

So, $$Q_{1_E}(\psi) = \left< \psi, \mu(E) \psi \right>$$.

To prove that this $$Q_{1_E}$$ is a bounded quadratic form we must prove that

1. $$Q_{1_E}(\lambda\psi) = \lvert\lambda\rvert^2 Q_{1_E}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.
2. The map $$L_{1_E} : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by

   $$
   \begin{align}
       L_{1_E}(\phi, \psi) &\equiv \frac{1}{2} \left[ Q_{1_E}(\phi + \psi) - Q_{1_E}(\phi) - Q_{1_E}(\psi) \right] \\
                           &-\frac{i}{2} \left[ Q_{1_E}(\phi + i\psi) - Q_{1_E}(\phi) - Q_{1_E}(i\psi) \right]
   \end{align}
   $$

   is a sesquilinear form on $$\mathbf{H}$$.

3. There exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

   $$
       \lvert Q_{1_E}(\phi) \rvert \le C \|\phi\|^2,
   $$

   where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

Let us first prove that $$Q_{1_E}(\lambda\psi) = \lvert\lambda\rvert^2 Q_{1_E}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$. As a result of our previous derivation, the definition of an inner product, and the definition of the norm on $$\mathbb{C}$$ one has

$$
\begin{align}
  Q_{1_E}(\lambda\psi) &= \left< \lambda\psi, \mu(E) \lambda\psi \right> \\
                       &= \lambda^*\lambda \left< \psi, \mu(E) \psi \right> \\
                       &= \lvert\lambda\rvert^2 \left< \psi, \mu(E) \psi \right> \\
                       &= \lvert\lambda\rvert^2 Q_{1_E}(\psi),
\end{align}
$$

which proves $$Q_{1_E}(\lambda\psi) = \lvert\lambda\rvert^2 Q_{1_E}(\psi)$$, the desired result.

Next let us prove the map $$L_{1_E} : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined above is a sesquilinear form on $$\mathbf{H}$$. As a result of our previous derivation and the definition of $$L_{1_E}$$ we have

$$
\begin{align}
    L_{1_E}(\phi, \psi) &= \frac{1}{2} \left[ \left< (\phi + \psi), \mu(E) (\phi + \psi) \right> - \left< \phi, \mu(E) \phi \right> - \left< \psi, \mu(E) \psi \right> \right] \\
                        &-\frac{i}{2} \left[ \left< (\phi + i\psi), \mu(E) (\phi + i\psi) \right> - \left< \phi, \mu(E) \phi \right> - \left< i\psi, \mu(E) i\psi \right> \right]
\end{align}
$$

for all $$\phi, \psi \in \mathbf{H}$$. Using the definition of an inner product, this simplifies as follows

$$
\begin{align}
    L_{1_E}(\phi, \psi) &= \frac{1}{2} \left[ \left< \phi, \mu(E) \psi \right> + \left< \psi, \mu(E) \phi \right> \right] - \frac{i}{2} \left[ \left< \phi, \mu(E) i\psi \right> + \left< i\psi, \mu(E) \phi \right> \right] \\
                        &= \frac{1}{2} \left[ \left< \phi, \mu(E) \psi \right> + \left< \psi, \mu(E) \phi \right> \right] + \frac{1}{2} \left[ \left< \phi, \mu(E) \psi \right> - \left< \psi, \mu(E) \phi \right> \right] \\
                        &= \left< \phi, \mu(E) \psi \right>,
\end{align}
$$

which implies

$$
     L_{1_E}(\phi, \psi) = \left< \phi, \mu(E) \psi \right>.
$$

The definition of an inner product then implies that $$L_{1_E}(\phi, \psi)$$ is conjugate linear in the first factor and linear in the second factor. Thus $$L_{1_E}(\phi, \psi)$$ is a sesquilinear form, the desired result. The results up until this point prove that $$Q_{1_E}$$ is a quadratic form.

Finally, to prove that $$Q_{1_E}$$ isn't only a quadratic form but is a bounded quadratic form we must prove that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_{1_E}(\phi) \rvert \le C \|\phi\|^2.
$$

Using the results of our previous derivation, the definition of an orthogonal projection, and standard properties of an inner product and its associated norm we have

$$
\begin{align}
    \lvert Q_{1_E}(\phi) \rvert &= \lvert \left< \phi, \mu(E) \phi \right> \rvert \\
                    &= \lvert \left< \phi, \mu(E) \mu(E) \phi \right> \rvert \\
                    &= \lvert \left< \phi, \mu(E)^* \mu(E) \phi \right> \rvert \\
                    &= \lvert \left< \mu(E) \phi, \mu(E) \phi \right> \rvert \\
                    &= \lvert \|\mu(E) \phi\|^2 \rvert \\
                    &= \|\mu(E) \phi\|^2 \\
                    &\le \|\phi\|^2,
\end{align}
$$

where the final inequality is [**Lemma** *(Orthogonal Projections are Norm-Decreasing)*](#lmm:projection-norm-decreasing), applicable since $$\mu(E)$$ is an orthogonal projection by property 1 of the [definition of a projection-valued measure](#def:projection-valued-measure). This proves that

$$
    \lvert Q_{1_E}(\phi) \rvert \le \|\phi\|^2,
$$

which implies that the constant required to prove that $$Q_{1_E}$$ is a bounded quadratic form is simply $$1$$. This concludes the proof: $$Q_{1_E}$$ is a bounded quadratic form for any indicator function $$1_E$$.
$$\blacksquare$$

> **Proposition** *(The Quadratic Form of a Simple Function is Bounded)*
<a name="prpstn:Q-simple-bounded-form"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{prpstn:Q-indicator-bounded-form} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{lmm:sesquilinear-linear-combination} -->
<!--  \uses{lmm:bqf-linear-combination} -->
> With notation as in [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form), let $$s = \sum_{i} c_i 1_{E_i}$$ be a simple function on $$X$$. Then $$Q_s : \mathbf{H} \rightarrow \mathbb{C}$$, $$Q_s(\psi) \equiv \int_X s \, d\mu_\psi$$, is a bounded quadratic form.

**Proof**
Let $$s$$ be a simple function, i.e. a finite linear combination of indicator functions

$$
  s = \sum_{i = 1}^n \alpha_i 1_{E_i}
$$

where $$\alpha_i \in \mathbb{C}$$ and $$E_i \in \Omega(X)$$ are pairwise disjoint, also results in a bounded quadratic form $$Q_s$$.

In this case, following a logic similar to the indicator function case, we have

$$
\begin{align}
    Q_s(\psi) &= \int_X \left( \sum_{i = 1}^n \alpha_i 1_{E_i} \right) d\mu_\psi \\
              &= \sum_{i = 1}^n \int_X \alpha_i 1_{E_i} d\mu_\psi \\
              &= \sum_{i = 1}^n \alpha_i  \int_X 1_{E_i} d\mu_\psi \\
              &= \sum_{i = 1}^n \alpha_i  \left< \psi, \mu(E_i) \psi \right> \\
              &= \sum_{i = 1}^n \alpha_i  Q_{1_{E_i}}(\psi)
\end{align}
$$

So in summary

$$
    Q_s(\psi) = \sum_{i = 1}^n \alpha_i  Q_{1_{E_i}}(\psi)
$$

Each $$Q_{1_{E_i}}$$ is a bounded quadratic form by [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form), so [**Lemma** *(Linear Combinations of Bounded Quadratic Forms are Bounded Quadratic Forms)*](#lmm:bqf-linear-combination) gives at once that $$Q_s$$ is a bounded quadratic form. For completeness we record the three conditions explicitly.

First we must prove that $$Q_s(\lambda\psi) = \lvert\lambda\rvert^2 Q_s(\psi)$$. This follows from [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form)

$$
\begin{align}
    Q_s(\lambda\psi) &= \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\lambda\psi) \\
                     &= \sum_{i = 1}^n \alpha_i \lvert \lambda \rvert^2 Q_{1_{E_i}}(\psi) \\
                     &= \lvert \lambda \rvert^2 \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\psi) \\
                     &= \lvert \lambda \rvert^2 Q_s(\psi),
\end{align}
$$

giving the desired result $$Q_s(\lambda\psi) = \lvert\lambda\rvert^2 Q_s(\psi)$$.

Next we must prove the map $$L_s : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
\begin{align}
    L_s(\phi, \psi) &= \frac{1}{2} \left[ Q_s(\phi + \psi) - Q_s(\phi) - Q_s(\psi) \right] \\
                    &-\frac{i}{2} \left[ Q_s(\phi + i\psi) - Q_s(\phi) - Q_s(i\psi) \right]
\end{align}
$$

is a sesquilinear form on $$\mathbf{H}$$. This result follows from linearity together with [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form).

As

$$
    Q_s(\psi) = \sum_{i = 1}^n \alpha_i  Q_{1_{E_i}}(\psi)
$$

we have

$$
  L_s(\phi, \psi) = \sum_{i = 1}^n \alpha_i L_{1_{E_i}}(\phi, \psi).
$$

From [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form) each $$L_{1_{E_i}}$$ is a sesquilinear form, so [**Lemma** *(Linear Combinations of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-linear-combination) gives that $$L_s$$ is a sesquilinear form on $$\mathbf{H}$$, as required.

Finally, we must prove that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_s(\phi) \rvert \le C \|\phi\|^2.
$$

This again follows from linearity together with [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form). We have

$$
\begin{align}
  \lvert Q_s(\phi) \rvert &= \left\lvert \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\phi) \right\rvert \\
              &\le \sum_{i = 1}^n \left\lvert \alpha_i Q_{1_{E_i}}(\phi) \right\rvert \\
              &= \sum_{i = 1}^n \left\lvert\alpha_i\right\rvert \, \left\lvert Q_{1_{E_i}}(\phi) \right\rvert \\
              &\le \sum_{i = 1}^n \left\lvert\alpha_i\right\rvert \|\phi\|^2 \\
              &\le \left( \sum_{i = 1}^n \left\lvert\alpha_i\right\rvert \right) \|\phi\|^2.
\end{align}
$$

This gives the desired result

$$
    \lvert Q_s(\phi) \rvert \le C \|\phi\|^2
$$

for

$$
    C = \sum_{i = 1}^n \left\lvert\alpha_i\right\rvert.
$$

This completes the proof that $$Q_s$$ is a bounded quadratic form for any simple function $$s$$.
$$\blacksquare$$

> **Proposition** *(The Quadratic Form of a Bounded Measurable Function is Bounded)*
<a name="prpstn:Q-measurable-bounded-form"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{prpstn:Q-indicator-bounded-form} -->
<!--  \uses{prpstn:Q-simple-bounded-form} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{lmm:sesquilinear-pointwise-limit} -->
<!--  \uses{lmm:bqf-pointwise-limit} -->
> With notation as in [**Proposition** *(The Quadratic Form of an Indicator Function is Bounded)*](#prpstn:Q-indicator-bounded-form), let $$f$$ be a bounded, measurable, complex-valued function on $$X$$. Then $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$, $$Q_f(\psi) \equiv \int_X f \, d\mu_\psi$$, is a bounded quadratic form.

**Proof**
Consider the map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

is a bounded quadratic form. The route is: approximate $$f$$ uniformly by simple functions $$s_i$$, note that each $$Q_{s_i}$$ is a bounded quadratic form by [**Proposition** *(The Quadratic Form of a Simple Function is Bounded)*](#prpstn:Q-simple-bounded-form) with a bound uniform in $$i$$, and apply [**Lemma** *(Uniformly Bounded Pointwise Limits of Bounded Quadratic Forms)*](#lmm:bqf-pointwise-limit). We give the three conditions explicitly below.

To wit we must first prove that $$Q_f(\lambda\psi) = \lvert\lambda\rvert^2 Q_f(\psi)$$. This follows from [**Proposition** *(The Quadratic Form of a Simple Function is Bounded)*](#prpstn:Q-simple-bounded-form) and the Complex-Valued Simple Approximation Theorem. One has

$$
\begin{align}
    Q_f(\lambda\psi) &= \int_X f \, d\mu_{\lambda\psi} \\
                     &= \int_X \lim\limits_{i \rightarrow \infty} s_i \, d\mu_{\lambda\psi} \\
                     &= \lim\limits_{i \rightarrow \infty} \int_X s_i \, d\mu_{\lambda\psi} \\
                     &= \lim\limits_{i \rightarrow \infty} Q_{s_i}(\lambda\psi) \\
                     &= \lim\limits_{i \rightarrow \infty} \left\lvert\lambda\right\rvert^2 Q_{s_i}(\psi) \\
                     &= \left\lvert\lambda\right\rvert^2 \lim\limits_{i \rightarrow \infty} Q_{s_i}(\psi) \\
                     &= \left\lvert\lambda\right\rvert^2 Q_f(\psi),
\end{align}
$$

where the second equality follows from the Complex-Valued Simple Approximation Theorem, the third from the fact that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ and thus the limit can be pulled out of the integral, the fourth from the definition of $$Q_{s_i}$$, the fifth from [**Proposition** *(The Quadratic Form of a Simple Function is Bounded)*](#prpstn:Q-simple-bounded-form), and the final as before from uniform convergence and the Complex-Valued Simple Approximation Theorem. So in summary we have proven that

$$
    Q_f(\lambda\psi) = \left\lvert\lambda\right\rvert^2 Q_f(\psi),
$$

which is the first desired result.

By [**Lemma** *(Pointwise Limits of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-pointwise-limit), applied to the sesquilinear forms $$L_{s_i}$$ whose pointwise limit it is, the map $$L_f$$ defined by

$$
\begin{align}
    L_f(\phi, \psi) &= \frac{1}{2} \left[ Q_f(\phi + \psi) - Q_f(\phi) - Q_f(\psi) \right] \\
                    &-\frac{i}{2} \left[ Q_f(\phi + i\psi) - Q_f(\phi) - Q_f(i\psi) \right]
\end{align}
$$

is a sesquilinear form on $$\mathbf{H}$$. In particular, using the same argument as above but for $$\lambda = 1$$ we have

$$
\begin{align}
    Q_f(\psi) &= \int_X f \, d\mu_{\psi} \\
              &= \int_X \lim\limits_{i \rightarrow \infty} s_i \, d\mu_{\psi} \\
              &= \lim\limits_{i \rightarrow \infty} \int_X s_i \, d\mu_{\psi} \\
              &= \lim\limits_{i \rightarrow \infty} Q_{s_i}(\psi).
\end{align}
$$

Hence,

$$
\begin{align}
    L_f(\phi, \psi) &=
    \begin{aligned}[t]
        &\frac{1}{2} \left[ \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi + \psi) - \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi) - \lim\limits_{i \rightarrow \infty} Q_{s_i}(\psi) \right] \\
       -&\frac{i}{2} \left[ \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi + i\psi) - \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi) - \lim\limits_{i \rightarrow \infty} Q_{s_i}(i\psi) \right]
    \end{aligned} \\
    &=
    \begin{aligned}[t]
        \lim\limits_{i \rightarrow \infty} &\left( \frac{1}{2} \left[ Q_{s_i}(\phi + \psi) - Q_{s_i}(\phi) - Q_{s_i}(\psi) \right] \right. \\
        &-\left. \frac{i}{2} \left[ Q_{s_i}(\phi + i\psi) - Q_{s_i}(\phi) - Q_{s_i}(i\psi) \right] \right)
    \end{aligned} \\
    &= \lim\limits_{i \rightarrow \infty} L_{s_i}(\phi, \psi).
\end{align}
$$

This implies

$$
    L_f(\phi, \psi) = \lim\limits_{i \rightarrow \infty} L_{s_i}(\phi, \psi),
$$

which---as a result of our simple function proof that $$L_{s_i}(\phi, \psi)$$ is conjugate linear in the first factor and linear in the second factor---implies that $$L_f(\phi, \psi)$$ is conjugate linear in the first factor and linear in the second factor, and thus a sesquilinear form on $$\mathbf{H}$$.

Finally, we must prove that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_f(\phi) \rvert \le C \|\phi\|^2.
$$

for all $$\phi \in \mathbf{H}$$. It is to this we now turn.

The definition of $$Q_f$$, triangle inequality for integrals, and the fact that $$f$$ is bounded imply

$$
\begin{align}
    \left\lvert Q_f(\phi) \right\rvert &= \left\lvert \int_X f \, d\mu_\phi \right\rvert \\
                             &\le \int_X \left\lvert f \right\rvert \, d\mu_\phi \\
                             &\le \int_X \left(  \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert \right) \, d\mu_\phi \\
                             &= \left( \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert \right) \int_X d\mu_\phi.
\end{align}
$$

However, the definitions of $$\mu_\phi$$ and $$\mu$$ imply

$$
\begin{align}
    \int_X d\mu_\phi &= \left< \phi, \mu(X) \phi \right> \\
                     &= \left< \phi, \mathbf{1} \phi \right> \\
                     &= \left< \phi, \phi \right> \\
                     &= \| \phi \|^2,
\end{align}
$$

where the final step uses the definition of the Hilbert space norm in terms of the Hilbert space inner product.

The previous two results together imply

$$
    \left\lvert Q_f(\phi) \right\rvert \le \left( \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert \right) \| \phi \|^2
$$

which, if we make the identification

$$
    C = \left( \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert \right),
$$

is nothing more than the statement that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_f(\phi) \rvert \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$, the desired result.

This concludes our proof that for any bounded, measurable, complex-valued function $$f$$ on the set $$X$$ with $$\sigma$$-algebra $$\Omega(X)$$ the map $$Q_f$$ is a bounded quadratic form. $$\blacksquare$$


Our next step in the larger proof is establishing several propositions we will have need of later in our argument. To wit let us first prove the proposition (Proposition A.61 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Proposition** *(Properties of the Sesquilinear Form Associated to a Quadratic Form)*
<a name="prpstn:hall-a.61"></a>
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:bounded-sesquilinear-form} -->
> If $$Q$$ is a quadratic form on $$\mathbf{H}$$ and $$L$$ is the associated sesquilinear form
>
> $$
> \begin{align}
>     L(\phi, \psi) &\equiv \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
>                   &-\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right],
> \end{align}
> $$
>
> then we have the following results
>
> 1. For all $$\psi \in \mathbf{H}$$, we have $$Q(\psi) = L(\psi, \psi)$$.
> 2. If $$Q$$ is bounded, then $$L$$ is bounded.
> 3. If $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then $$L$$ is conjugate symmetric, that is
>
>    $$
>        L(\phi, \psi) = \overline{L(\psi, \phi)}
>    $$
>
>    for all $$\phi, \psi \in \mathbf{H}$$

**Proof**
Let us first prove for all $$\psi \in \mathbf{H}$$, we have $$Q(\psi) = L(\psi, \psi)$$.

The definition of a quadratic form along with standard properties of the norm $$\lvert \cdot \rvert$$ imply

$$
\begin{align}
    L(\psi, \psi) &=
    \begin{aligned}[t]
        &\frac{1}{2} \left[ Q(\psi + \psi) - Q(\psi) - Q(\psi) \right] \\
        &-\frac{i}{2} \left[ Q(\psi + i\psi) - Q(\psi) - Q(i\psi) \right]
    \end{aligned} \\
    &=
    \begin{aligned}[t]
        &\frac{1}{2} \left[ Q(2\psi) - 2Q(\psi) \right] \\
        &-\frac{i}{2} \left[ Q((1 + i)\psi) - Q(\psi) - \lvert i \rvert^2 Q(\psi) \right]
    \end{aligned} \\
    &=
    \begin{aligned}[t]
        &\frac{1}{2} \left[ \lvert 2 \rvert^2Q(\psi) - 2Q(\psi) \right] \\
        &-\frac{i}{2} \left[ \lvert 1 + i \rvert^2Q(\psi) - 2Q(\psi) \right]
    \end{aligned} \\
    &= Q(\psi),
\end{align}
$$

the desired result $$L(\psi, \psi) = Q(\psi)$$.

Let us next prove that if $$Q$$ is bounded, then $$L$$ is bounded.

In this case by hypothesis $$Q$$ is bounded. Hence, there exists a $$C$$ in $$\mathbb{R}$$ such that

$$
    \left\lvert Q(\psi) \right\rvert \le C \|\psi\|^2
$$

for all $$\psi \in \mathbf{H}$$.

Consider for the moment $$\phi, \psi \in \mathbf{H}$$ such that $$\|\phi\| = 1$$ and $$\|\psi\| = 1$$. The definition of a norm then implies

$$
    \|\phi + \psi\| \le \|\phi\| + \|\psi\| = 2,
$$

which implies $$\|\phi + \psi\| \le 2$$ as well as

$$
\begin{align}
    \|\phi + i\psi\| &\le \|\phi\| + \|i\psi\| \\
                     &=    \|\phi\| + \lvert i \rvert \|\psi\| \\
                     &=    \|\phi\| + \|\psi\| \\
                     &=    2,
\end{align}
$$

which implies $$\|\phi + i\psi\| \le 2$$.

This, along with the definition of a norm and the fact that $$Q$$ is bounded, implies

$$
\begin{align}
    \left\lvert L(\phi, \psi) \right\rvert &= \left\lvert \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] -\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right] \right\rvert \\
    &\le \frac{1}{2} \left[ \left\lvert Q(\phi + \psi)\right\rvert + \left\lvert Q(\phi)\right\rvert + \left\lvert Q(\psi)\right\rvert + \left\lvert Q(\phi + i\psi)\right\rvert + \left\lvert Q(\phi)\right\rvert + \left\lvert Q(i\psi)\right\rvert \right] \\
    &\le C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + \|i\psi\|^2 \right] \\
    &=   C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + \lvert i \rvert^2 \, \|\psi\|^2 \right] \\
    &=   C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + \|\psi\|^2 \right] \\
    &\le C \frac{1}{2} \left[ 4 + 1 + 1 + 4 + 1 + 1 \right] \\
    &=   6C.
\end{align}
$$

Now for arbitrary $$\phi, \psi \in \mathbf{H}$$ that need not satisfy $$\|\phi\| = 1$$ and $$\|\psi\| = 1$$, we can obviously always find unit vectors $$\widehat{\phi}$$ and $$\widehat{\psi}$$ in $$\mathbf{H}$$ such that

$$
\begin{align}
    \phi &= \|\phi\| \widehat{\phi} \\
    \psi &= \|\psi\| \widehat{\psi}.
\end{align}
$$

As the definition of a quadratic form implies that $$L$$ is sesquilinear, we thus have for these arbitrary $$\phi, \psi \in \mathbf{H}$$

$$
    \left\lvert L(\phi, \psi)\right\rvert = \|\phi\| \, \|\psi\| \, \left\lvert L(\widehat{\phi}, \widehat{\psi}) \right\rvert \le 6C \|\phi\| \, \|\psi\|,
$$

where the inequality follows from our previous result. Thus we have proven the second desired result

$$
    \left\lvert L(\phi, \psi)\right\rvert \le 6C \|\phi\| \, \|\psi\|,
$$

that $$L$$ is bounded.

Finally, we will prove that if $$Q(\psi)$$ is valued in $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then $$L$$ is conjugate symmetric.

In this case, by hypothesis $$Q(\psi)$$ is valued in $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$. This implies that for arbitrary $$\phi, \psi \in \mathbf{H}$$

$$
\begin{align}
    \text{Re} \left[ L(\phi, \psi) \right]
        &= \text{Re} \left[ \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] -\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right] \right] \\
        &= \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right].
\end{align}
$$

If we define $$M(\phi, \psi) \equiv \text{Re} \left[ L(\phi, \psi) \right]$$, then we have shown

$$
    M(\phi, \psi) = \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right].
$$

Now let us derive several basic properties of $$M$$.

First one can note that by inspection of

$$
    M(\phi, \psi) = \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right]
$$

that $$M(\phi, \psi)$$ is symmetric, i.e. $$M(\phi, \psi) = M(\psi, \phi)$$.

Second, as $$M(\phi, \psi) \equiv \text{Re} \left[ L(\phi, \psi) \right]$$ and $$L$$ is a sesquilinear form, and thus conjugate linear in the first factor and linear in the second factor, it follows that $$M$$ is linear in both factors, i.e. real-bilinear.

Finally, as $$Q$$ is a quadratic form, and thus satisfies $$Q(\lambda\psi) = \lvert\lambda\rvert^2 Q(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$, one has

$$
\begin{align}
    M(i\phi, i\psi) &= \frac{1}{2} \left[ Q(i\phi + i\psi) - Q(i\phi) - Q(i\psi) \right] \\
                    &= \frac{1}{2} \left[ Q(i(\phi + \psi)) - \lvert i \rvert^2Q(\phi) - \lvert i \rvert^2Q(\psi) \right] \\
                    &= \frac{1}{2} \left[ \lvert i \rvert^2Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
                    &= \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
                    &= M(\phi, \psi),
\end{align}
$$

which implies $$M(i\phi, i\psi) = M(\phi, \psi)$$.

Together these basic properties of $$M$$ imply

$$
\begin{align}
    M(\phi, i\psi) &= M(i\psi, \phi) \\
                   &= M(i^2\psi, i\phi) \\
                   &= M(-\psi, i\phi) \\
                   &= -M(\psi, i\phi),
\end{align}
$$

which implies $$M(\phi, i\psi) = -M(\psi, i\phi)$$.

Now noting that

$$
    M(\phi, i\psi) = \frac{1}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right],
$$

we have

$$
\begin{align}
    L(\phi, \psi)
        &= \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] -\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right] \\
        &= M(\phi, \psi) - iM(\phi, i\psi) \\
        &= M(\phi, \psi) + iM(\psi, i\phi) \\
        &= M(\psi, \phi) + iM(\psi, i\phi), \\
\end{align}
$$

where the second to last step follows from our previous result $$M(\phi, i\psi) = -M(\psi, i\phi)$$ and the last from the symmetry of $$M$$. As $$M$$ is real this derivation can be continued as

$$
\begin{align}
    L(\phi, \psi)
        &= M(\phi, \psi) - iM(\phi, i\psi) \\
        &= M(\phi, \psi) + iM(\psi, i\phi) \\
        &= M(\psi, \phi) + iM(\psi, i\phi) \\
        &= \overline{L(\psi, \phi)},
\end{align}
$$

proving that $$L(\phi, \psi) = \overline{L(\psi, \phi)}$$, the desired result, i.e. if $$Q$$ is real, then $$L$$ is conjugate symmetric.$$\blacksquare$$


Two closure properties of sesquilinear forms are used repeatedly below; we record them once here.

> **Lemma** *(Linear Combinations of Sesquilinear Forms are Sesquilinear)*
<a name="lmm:sesquilinear-linear-combination"></a>
<!--  \uses{def:bounded-sesquilinear-form} -->
> Let $$L_1, \ldots, L_n$$ be sesquilinear forms on $$\mathbf{H}$$ and let $$\alpha_1, \ldots, \alpha_n \in \mathbb{C}$$. Then
>
> $$
>     L(\phi,\psi) \equiv \sum_{k=1}^n \alpha_k L_k(\phi,\psi)
> $$
>
> is a sesquilinear form on $$\mathbf{H}$$.

**Proof**
Fix $$\psi$$. Each $$L_k$$ is conjugate-linear in its first argument, so for $$\phi, \chi \in \mathbf{H}$$ and $$c \in \mathbb{C}$$,

$$
\begin{align}
    L(c\phi + \chi, \psi) &= \sum_k \alpha_k L_k(c\phi+\chi,\psi) \\
                &= \sum_k \alpha_k \left( \overline{c} L_k(\phi,\psi) + L_k(\chi,\psi) \right) \\
                &= \overline{c} L(\phi,\psi) + L(\chi,\psi),
\end{align}
$$

using that finite sums may be rearranged. The same computation with linearity in the second argument gives $$L(\phi, c\psi + \chi) = c L(\phi,\psi) + L(\phi,\chi)$$. So $$L$$ is conjugate-linear in the first argument and linear in the second, hence sesquilinear.$$\blacksquare$$

> **Lemma** *(Pointwise Limits of Sesquilinear Forms are Sesquilinear)*
<a name="lmm:sesquilinear-pointwise-limit"></a>
<!--  \uses{def:bounded-sesquilinear-form} -->
> Let $$\{L_i\}_{i \in \mathbb{N}}$$ be sesquilinear forms on $$\mathbf{H}$$ such that $$L(\phi,\psi) \equiv \lim_{i \rightarrow \infty} L_i(\phi,\psi)$$ exists for all $$\phi,\psi \in \mathbf{H}$$. Then $$L$$ is a sesquilinear form on $$\mathbf{H}$$.

**Proof**
For $$\phi,\chi,\psi \in \mathbf{H}$$ and $$c \in \mathbb{C}$$, each $$L_i$$ satisfies $$L_i(c\phi+\chi,\psi) = \overline{c}L_i(\phi,\psi) + L_i(\chi,\psi)$$. All three limits exist by hypothesis, and the limit of a sum is the sum of the limits while the limit of a scalar multiple is that multiple of the limit, so

$$
    L(c\phi+\chi,\psi) = \lim_{i \rightarrow \infty} \left( \overline{c}L_i(\phi,\psi) + L_i(\chi,\psi) \right) = \overline{c}L(\phi,\psi) + L(\chi,\psi).
$$

The same argument in the second argument gives linearity there. Hence $$L$$ is sesquilinear.$$\blacksquare$$


The same two closure properties hold for bounded quadratic forms, and it is in that form that they are used.

> **Lemma** *(Linear Combinations of Bounded Quadratic Forms are Bounded Quadratic Forms)*
<a name="lmm:bqf-linear-combination"></a>
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{lmm:sesquilinear-linear-combination} -->
> Let $$Q_1, \ldots, Q_n$$ be bounded quadratic forms on $$\mathbf{H}$$ and let $$\alpha_1, \ldots, \alpha_n \in \mathbb{C}$$. Then $$Q \equiv \sum_{k=1}^n \alpha_k Q_k$$ is a bounded quadratic form on $$\mathbf{H}$$.

**Proof**
*Homogeneity.* For $$\lambda \in \mathbb{C}$$ and $$\psi \in \mathbf{H}$$,

$$
    Q(\lambda\psi) = \sum_k \alpha_k Q_k(\lambda\psi) = \sum_k \alpha_k \lvert \lambda \rvert^2 Q_k(\psi) = \lvert \lambda \rvert^2 Q(\psi).
$$

*Sesquilinearity of the associated form.* The polarization formula is linear in $$Q$$, so the form associated to $$Q$$ is $$\sum_k \alpha_k L_k$$ where $$L_k$$ is the form associated to $$Q_k$$; each $$L_k$$ is sesquilinear, so [**Lemma** *(Linear Combinations of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-linear-combination) applies.

*Boundedness.* Choose $$C_k$$ with $$\lvert Q_k(\phi) \rvert \le C_k \lVert \phi \rVert^2$$. Then $$\lvert Q(\phi) \rvert \le \sum_k \lvert \alpha_k \rvert C_k \lVert \phi \rVert^2$$, so $$C \equiv \sum_k \lvert \alpha_k \rvert C_k$$ works.$$\blacksquare$$

> **Lemma** *(Uniformly Bounded Pointwise Limits of Bounded Quadratic Forms)*
<a name="lmm:bqf-pointwise-limit"></a>
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{lmm:sesquilinear-pointwise-limit} -->
> Let $$\{Q_i\}_{i \in \mathbb{N}}$$ be bounded quadratic forms on $$\mathbf{H}$$ such that $$Q(\psi) \equiv \lim_{i \rightarrow \infty} Q_i(\psi)$$ exists for every $$\psi \in \mathbf{H}$$, and suppose there is a single constant $$C$$ with $$\lvert Q_i(\phi) \rvert \le C \lVert \phi \rVert^2$$ for all $$i$$ and all $$\phi$$. Then $$Q$$ is a bounded quadratic form on $$\mathbf{H}$$, with the same constant $$C$$.
>
> The *uniformity* of the bound is required: a pointwise limit of quadratic forms whose individual bounds grow without limit need not be bounded.

**Proof**
*Homogeneity.* $$Q(\lambda\psi) = \lim_i Q_i(\lambda\psi) = \lim_i \lvert \lambda \rvert^2 Q_i(\psi) = \lvert \lambda \rvert^2 Q(\psi)$$.

*Sesquilinearity of the associated form.* The polarization formula expresses the associated form as a fixed finite combination of values of $$Q$$, so the form associated to $$Q$$ is the pointwise limit of the forms associated to the $$Q_i$$; [**Lemma** *(Pointwise Limits of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-pointwise-limit) applies.

*Boundedness.* For each $$\phi$$, $$\lvert Q(\phi) \rvert = \lim_i \lvert Q_i(\phi) \rvert \le C \lVert \phi \rVert^2$$, the inequality passing to the limit because it holds for every $$i$$ with the *same* $$C$$.$$\blacksquare$$

The next result requires the Hilbert-space self-duality theorem, which we state first.

> **Theorem** *(Riesz Theorem)*
<a name="thrm:hall-a.52"></a>
<!--  \uses{def:bounded-operator-notation} -->
> If $$\xi : \mathbf{H} \rightarrow \mathbb{C}$$ is a bounded linear functional on the Hilbert space $$\mathbf{H}$$, then there exists a unique $$\chi \in \mathbf{H}$$ such that
>
> $$
>     \xi(\psi) = \left< \chi, \psi \right>
> $$
>
> for all $$\psi \in \mathbf{H}$$. Furthermore, the operator norm of $$\xi$$ as a bounded linear functional is equal to the norm of $$\chi$$ as an element of $$\mathbf{H}$$.

The next in the set of "helper" propositions that we will prove is the proposition (Proposition A.63 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Proposition** *(A Bounded Quadratic Form Determines a Unique Bounded Operator)*
<a name="prpstn:hall-a.63"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:hall-a.52} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-a.61} -->
> If $$Q$$ is a bounded quadratic form on $$\mathbf{H}$$, there is a unique $$A \in \mathcal{B}(\mathbf{H})$$ such that $$Q(\psi) = \left< \psi, A\psi \right>$$ for all $$\psi \in \mathbf{H}$$. If $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then the operator $$A$$ is self-adjoint.

**Proof**
By hypothesis $$Q$$ is a bounded quadratic form. Hence, as a result of the [**Proposition**](#prpstn:hall-a.61) we just proved, the sesquilinear form associated to $$Q$$ is bounded. This implies that there exists a constant $$C$$ in $$\mathbb{R}$$ such that

$$
    \left\lvert L(\phi, \psi) \right\rvert \le C \|\phi\| \, \|\psi\|,
$$

for all $$\phi, \psi \in \mathbf{H}$$.

Hence, for any fixed $$\phi \in \mathbf{H}$$, the operator norm of the linear map $$\psi \mapsto L(\phi, \psi)$$ is bounded, with operator norm at most $$C \|\phi\|$$.

Explicitly, $$\psi \mapsto L(\phi, \psi)$$ is linear as a result of $$Q$$ being a quadratic form, which implies $$L$$ is a sesquilinear form, which in turn implies that $$\psi \mapsto L(\phi, \psi)$$ is linear in $$\psi$$.

Furthermore, the definition of operator norm implies

$$
    \|L(\phi, \cdot)\| \equiv \sup\limits_{\|\psi\| = 1} \lvert L(\phi, \psi) \rvert.
$$

The fact that $$L$$ is bounded as a sesquilinear form implies

$$
    \left\lvert L(\phi, \psi) \right\rvert \le C \|\phi\| \, \|\psi\|,
$$

for our fixed $$\phi$$ and any $$\psi \in \mathbf{H}$$. So for any $$\psi$$ such that $$\|\psi\| = 1$$

$$
    \left\lvert L(\phi, \psi) \right\rvert \le C \|\phi\|.
$$

Hence, these together imply

$$
    \|L(\phi, \cdot)\| \equiv \sup\limits_{\|\psi\| = 1} \lvert L(\phi, \psi) \rvert \le C \|\phi\|,
$$

the desired result.

Now recall the [**Riesz Theorem**](#thrm:hall-a.52) stated above: a bounded linear functional $$\xi$$ on $$\mathbf{H}$$ is represented by a unique $$\chi \in \mathbf{H}$$ via $$\xi(\psi) = \left< \chi, \psi \right>$$, with $$\left\| \chi \right\| = \left\| \xi \right\|$$.

As a result of the Riesz Theorem, for any fixed $$\phi$$ there exists a $$\chi$$ in $$\mathbf{H}$$ such that $$L(\phi, \psi) = \left< \chi, \psi \right>$$. In addition, the "operator norm conclusion" of the Riesz Theorem and our finding that the operator norm of $$\psi \mapsto L(\phi, \psi)$$ is bounded for any fixed $$\phi$$ imply that

$$
    \|\chi\| \le C \|\phi\|.
$$

As this is true for any $$\phi$$, we can use it to define a map $$B : \mathbf{H} \rightarrow \mathbf{H}$$ by $$B\phi \equiv \chi$$. It turns out that $$B$$ is linear and bounded relative to the operator norm.

Boundedness of $$B$$ relative to the operator norm follows from

$$
    \|\chi\| \le C \|\phi\|
$$

along with $$B\phi = \chi$$. These imply

$$
    \|B\phi\| \le C \|\phi\|.
$$

This is simply the statement that $$B$$ is bounded in the operator norm.

Linearity of $$B$$ follows from explicit calculation. For $$\phi_1, \phi_2 \in \mathbf{H}$$ we have by definition

$$
\begin{align}
    L(\phi_1, \psi) &= \left< B\phi_1, \psi \right> \\
    L(\phi_2, \psi) &= \left< B\phi_2, \psi \right>,
\end{align}
$$

for any $$\psi \in \mathbf{H}$$. Similarly, for any $$\alpha_1, \alpha_2 \in \mathbb{C}$$ we have by definition

$$
    L(\alpha_1 \phi_1 + \alpha_2 \phi_2 , \psi) = \left< B(\alpha_1 \phi_1 + \alpha_2 \phi_2), \psi \right>.
$$

As $$L$$ is a sesquilinear form and thus conjugate-linear in its first argument

$$
    L(\alpha_1\phi_1 + \alpha_2\phi_2, \psi) = \overline{\alpha_1} L(\phi_1, \psi) + \overline{\alpha_2} L(\phi_2, \psi).
$$

Hence, for any $$\psi \in \mathbf{H}$$

$$
    \left< B(\alpha_1 \phi_1 + \alpha_2 \phi_2), \psi \right> = \overline{\alpha_1} \left< B\phi_1, \psi \right> + \overline{\alpha_2}  \left< B\phi_2, \psi \right> = \left< \alpha_1 B\phi_1 + \alpha_2 B\phi_2, \psi \right>
$$

where the final equality uses the fact that the inner product is conjugate-linear in its first argument. As this is true for any $$\psi \in \mathbf{H}$$ it implies

$$
    B(\alpha_1 \phi_1 + \alpha_2 \phi_2) =  \alpha_1 B\phi_1 + \alpha_2 B\phi_2,
$$

which is none other than the statement of linearity.

It turns out that the unique operator $$A \in \mathcal{B}(\mathbf{H})$$ of the proposition, i.e. the operator satisfying $$Q(\psi) = \left< \psi, A \psi \right>$$, is given by $$A \equiv B^*$$. Let us prove that this is the case.

As a result of the last [**Proposition**](#prpstn:hall-a.61) we proved,

$$
    Q(\psi) = L(\psi, \psi)
$$

for all $$\psi \in \mathbf{H}$$. The definition of $$B$$ implies that

$$
    L(\psi, \psi) = \left< B\psi, \psi \right>.
$$

Together these imply

$$
    Q(\psi) = L(\psi, \psi) = \left< B\psi, \psi \right> = \left< \psi, B^*\psi \right>,
$$

which implies $$Q(\psi) = \left< \psi, B^*\psi \right>$$. This in turn implies that $$A \equiv B^*$$ is indeed the appropriate definition.

Uniqueness of $$A \equiv B^*$$ follows from the uniqueness of the Riesz Theorem. Explicitly, as a result of the Riesz Theorem, for any fixed $$\phi$$ there exists a unique $$\chi$$ in $$\mathbf{H}$$ such that $$L(\phi, \psi) = \left< \chi, \psi \right>$$. We then defined the map $$B$$ by $$B\phi \equiv \chi$$ and the map $$A$$ by $$A \equiv B^*$$. As $$\chi$$ is unique, any other possible $$B'$$ one could choose would have to satisfy $$B'\phi = \chi$$ too. Hence, $$(B - B')\phi = 0$$ for all $$\phi \in \mathbf{H}$$. This then implies that $$B - B'$$ is the zero operator, and thus $$B = B'$$, i.e. $$B$$ and thus $$A \equiv B^*$$ is unique.

Finally we must prove that if $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then the operator $$A$$ is self-adjoint.

Assuming that $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, the last [**Proposition**](#prpstn:hall-a.61) we proved implies that $$L$$ is conjugate symmetric,

$$
    L(\phi, \psi) = \overline{L(\psi, \phi)}
$$

for all $$\phi, \psi \in \mathbf{H}$$. This along with our definition of $$B$$ and $$A \equiv B^*$$ imply

$$
  \left< \phi, A\psi \right> = L(\phi, \psi) = \overline{L(\psi, \phi)} = \overline{\left< \psi, A\phi \right>} = \left< A\phi, \psi \right>,
$$

for all $$\phi, \psi \in \mathbf{H}$$, where the final step used the definition of an inner product. This implies

$$
    \left< \phi, A\psi \right> = \left< A\phi, \psi \right>
$$

for all $$\phi, \psi \in \mathbf{H}$$, which is simply the statement that $$A$$ is self-adjoint.$$\blacksquare$$

With these two "helper" propositions proven, we can now join the main thread of the [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration).

As one will recall we had established that for any bounded, measurable, complex-valued function $$f$$ the map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

is a bounded quadratic form. Hence, [**Proposition**](#prpstn:hall-a.63) implies that there is a unique, bounded operator $$A_f \in \mathcal{B}(\mathbf{H})$$ such that

$$
    Q_f(\psi) = \left< \psi, A_f\psi \right>
$$

for all $$\psi \in \mathbf{H}$$. We then define the operator-valued integral of $$f$$ as follows

$$
    f \longmapsto \int_X f d\mu \equiv A_f.
$$

By construction it is a map from the space of bounded, measurable, complex-valued functions to $$\mathcal{B}(\mathbf{H})$$, as required.

*The defining identity.* Tracing definitions it is obvious that this satisfies the required property

$$
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f d\mu_\psi
$$

of an operator-valued integral. Explicitly, the definition of the operator-valued integral along with the definition of $$Q_f$$ imply

$$
\begin{align}
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> &= \left< \psi, A_f \psi \right> \\
                                                              &= Q_f(\psi) \\
                                                              &= \int_X f \, d\mu_\psi,
\end{align}
$$

giving

$$
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f \, d\mu_\psi,
$$

the desired result.

for any bounded, measurable, complex-valued function $$f$$.$$\blacksquare$$

We now establish, one at a time, the four properties asserted by the theorem.

> **Proposition** *(Integral of an Indicator Function)*
<a name="prpstn:integral-of-indicator"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:operator-valued-integration} -->
> Let $$\Omega(X)$$ be a $$\sigma$$-algebra on a set $$X$$, let $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ be a projection-valued measure, and let $$f \mapsto \int_X f \, d\mu$$ be the map of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration). Then for all $$E \in \Omega(X)$$,
>
> $$
>     \int_X 1_E \, d\mu = \mu(E),
> $$
>
> where $$1_E$$ is the indicator function of $$E$$. In particular, the integral of the constant function $$1$$ is the multiplicative identity $$\mathbf{1}$$.

**Proof**
Next we must prove that for all $$E \in \Omega(X)$$, we have

$$
    \int_X 1_E \, d\mu = \mu(E),
$$

where $$1_E$$ is the indicator function of $$E$$.

Consider then the case $$f = 1_E$$. The definition of $$Q_{1_E}$$ and that of the measure $$\mu_\psi$$ imply

$$
    Q_{1_E}(\psi) = \int_X 1_E \, d\mu_\psi = \mu_\psi(E) = \left< \psi, \mu(E) \psi \right>.
$$

So, $$Q_{1_E}(\psi) = \left< \psi, \mu(E) \psi \right>$$.

As we proved, [**Proposition**](#prpstn:hall-a.63) implies that there is a unique, bounded operator $$A_{1_E} \in \mathcal{B}(\mathbf{H})$$ such that

$$
    Q_{1_E}(\psi) = \left< \psi, A_{1_E}\psi \right>
$$

for all $$\psi \in \mathbf{H}$$. Hence, $$A_{1_E} = \mu(E)$$. Thus the definition of the operator-valued integral implies

$$
    \int_X 1_E \, d\mu = \mu(E),
$$

which is the desired result.
$$\blacksquare$$

> **Proposition** *(Norm Bound for the Operator-Valued Integral)*
<a name="prpstn:integral-norm-bound"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{prpstn:hall-a.43} -->
<!--  \uses{prpstn:integral-as-limit-of-simple} -->
<!--  \uses{prpstn:integral-norm-bound-simple} -->
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{thrm:operator-valued-integration} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all bounded, measurable, complex-valued functions $$f$$ on $$X$$,
>
> $$
>     \left\| \, \int_X f \, d\mu \, \right\| \le \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert,
> $$
>
> where $$\| \cdot \|$$ is the operator norm and $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$.

**Proof**
The next result we must prove is that for all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have

$$
    \left\| \, \int_X f \, d\mu \, \right\| \le \sup\limits_{\lambda \in X} \left\lvert f(\lambda) \right\rvert,
$$

where $$\| \cdot \|$$ is the operator norm and $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$.

To prove this we will first prove a "utility" lemma that will aid our argument.

> **Lemma** *(Orthogonality of Spectral Projections on a Disjoint Cover)*
<a name="lmm:lemma2-of-operator-valued-integration"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
> Let $$X$$ be a set with $$\sigma$$-algebra $$\Omega(X)$$, and let $$\mu : \Omega(X) \rightarrow \mathcal{B}(\mathbf{H})$$ be a projection-valued measure. If $$E_1, E_2, \ldots, E_n \in \Omega(X)$$ are a finite set of elements that are pairwise disjoint and satisfy
>
> $$
>     X = \bigcup\limits_{i = 1}^n E_i,
> $$
>
> then for any $$\psi \in \mathbf{H}$$
>
> 1. The vectors $$\mu(E_1)\psi, \mu(E_2)\psi, \ldots, \mu(E_n)\psi$$ in $$\mathbf{H}$$ are pairwise orthogonal.
> 2. The norm $$\|\psi\|$$ of $$\psi$$ can be written as follows
>
>    $$
>        \|\psi\|^2 = \sum_{i = 1}^n \|\mu(E_i)\psi\|^2.
>    $$

**Proof**
Let us first prove that the vectors $$\mu(E_1)\psi, \mu(E_2)\psi, \ldots, \mu(E_n)\psi$$ in $$\mathbf{H}$$ are pairwise orthogonal.

Let $$i \neq j$$ be indices of the elements $$E_1, E_2, \ldots, E_n$$. The projection-valued measure definition along with the definitions of inner product and orthogonal projection imply

$$
\begin{align}
    \left< \mu(E_i)\psi, \mu(E_j)\psi \right> &= \left< \psi, \mu(E_i)^* \mu(E_j)\psi \right> \\
                                              &= \left< \psi, \mu(E_i) \mu(E_j)\psi \right> \\
                                              &= \left< \psi, \mu(E_i \cap E_j)\psi \right> \\
                                              &= \left< \psi, \mu(\emptyset)\psi \right> \\
                                              &= \left< \psi, 0\psi \right> \\
                                              &= 0,
\end{align}
$$

proving that $$\left< \mu(E_i)\psi, \mu(E_j)\psi \right> = 0$$, the desired pairwise orthogonality.

Next let us prove that the norm $$\|\psi\|$$ of $$\psi$$ can be written as follows

$$
    \|\psi\|^2 = \sum_{i = 1}^n \|\mu(E_i)\psi\|^2.
$$

The definition of a projection-valued measure implies

$$
\begin{align}
    \sum_{i = 1}^n \mu(E_i) \psi &= \mu \left( \bigcup_{i = 1}^n E_i \right) \psi \\
                                 &= \mu \left( X  \right) \psi \\
                                 &= \mathbf{1} \psi \\
                                 &= \psi,
\end{align}
$$

which implies

$$
     \psi = \sum_{i = 1}^n \mu(E_i) \psi.
$$

As we just proved, these summands are pairwise orthogonal; hence

$$
\begin{align}
    \| \psi \|^2 &= \left< \psi, \psi \right> \\
                 &= \left< \sum_{i = 1}^n \mu(E_i) \psi, \sum_{j = 1}^n \mu(E_j) \psi \right> \\
                 &= \sum_{i = 1}^n \sum_{j = 1}^n \left< \mu(E_i) \psi, \mu(E_j) \psi \right> \\
                 &= \sum_{i = 1}^n \left< \mu(E_i) \psi, \mu(E_i) \psi \right> \\
                 &= \sum_{i = 1}^n \|\mu(E_i) \psi\|^2,
\end{align}
$$

giving

$$
    \| \psi \|^2 = \sum_{i = 1}^n \|\mu(E_i) \psi\|^2,
$$

the desired result and completing the proof of our "utility" lemma.$$\blacksquare$$

One more "utility" lemma we will require is

> **Lemma** *(Operator Norm via the Inner Product)*
<a name="lmm:lemma-1"></a>
<!--  \uses{prpstn:hall-a.43} -->
<!--  \uses{def:bounded-operator-notation} -->
> Let $$\mathcal{B}(\mathbf{H})$$ be the set of operators on a separable, complex Hilbert space $$\mathbf{H}$$ that are bounded with respect to the operator norm as $$\mathcal{B}(\mathbf{H})$$. For any $$A$$ in $$\mathcal{B}(\mathbf{H})$$ we can write the operator norm $$\|A\|$$ of $$A$$ as follows
> 
> $$
>     \|A\| = \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< \chi, A \psi \right> \rvert
> $$ 
> 
> where $$\chi, \psi \in \mathbf{H}$$.

**Proof**
Let us begin this proof by deriving an alternative means of writing the norm of an element $$\psi \in \mathbf{H}$$ as

$$
    \|\psi\| = \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert.
$$

First let us prove this is true for the case $$\psi = 0$$.

In this case the definition of a norm implies $$\|\psi\| = 0$$. Similarly, for all $$\chi \in \mathbf{H}$$ we have $$\lvert \left< \chi, 0 \right> \rvert = 0$$. Thus we have the trivial equality in this case: both the lefthand and righthand sides of the desired equation are zero.

Now we can safely assume that $$\psi \neq 0$$.

Consider an arbitrary $$\psi \in \mathbf{H}$$ and an arbitrary $$\chi \in \mathbf{H}$$ such that $$\|\chi\| = 1$$. The [**Cauchy–Schwarz Inequality**](#prpstn:hall-a.43) implies that

$$
    \lvert \left< \chi, \psi \right> \rvert^2 \le \left< \chi, \chi \right> \left< \psi, \psi \right> = \|\chi\|^2 \left< \psi, \psi \right> = \left< \psi, \psi \right>.
$$

Hence, we have

$$
    \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert \le \|\psi\|.
$$

Alternatively, as $$\psi \neq 0$$ we can consider a particular $$\chi_0$$ of the form

$$
    \chi_0 = \frac{\psi}{\|\psi\|}.
$$

Obviously $$\|\chi_0\| = 1$$. With this form for $$\chi_0$$ the definitions of norm and inner product imply

$$
\begin{align}
    \left\lvert \left< \chi_0, \psi \right> \right\rvert &= \left\lvert \left< \frac{\psi}{\|\psi\|}, \psi \right> \right\rvert \\
                                            &= \left\lvert \frac{1}{\|\psi\|} \left< \psi, \psi \right> \right\rvert \\
                                            &= \frac{1}{\|\psi\|} \left\lvert \left< \psi, \psi \right> \right\rvert \\
                                            &= \frac{1}{\|\psi\|} \left\lvert \|\psi\|^2 \right\rvert \\
                                            &= \frac{1}{\|\psi\|} \|\psi\|^2 \\
                                            &= \|\psi\|.
\end{align}
$$

Hence, the previous bound we derived

$$
    \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert \le \|\psi\|
$$

is actually attained for this specific $$\chi_0$$. Thus it must be the case that

$$
    \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert \ge \lvert \left< \chi_0, \psi \right> \rvert = \|\psi\|.
$$

Now at this point we have proven that

$$
\begin{align}
    \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert &\le \|\psi\| \\
    \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert &\ge \|\psi\|.
\end{align}
$$

Together these imply the desired result

$$
    \|\psi\| = \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, \psi \right> \rvert.
$$

Now, the definition of the operator norm implies

$$
    \|A\| = \sup\limits_{\|\psi\| = 1} \|A\psi\|.
$$

Our recent result allows us to re-write the norm $$\|A\psi\|$$ as

$$
    \|A\psi\| = \sup\limits_{\|\chi\| = 1} \lvert \left< \chi, A\psi \right> \rvert.
$$

Hence,

$$
    \|A\| = \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< \chi, A\psi \right> \rvert.
$$

This is the final desired result of this lemma.$$\blacksquare$$

Let $$f$$ be a bounded, measurable, complex-valued function on $$X$$. By the [**Complex-Valued Simple Approximation Theorem**](#thrm:complex-valued-simple-approximation-theorem) there is a sequence $$\{s_i\}_{i \in \mathbb{N}}$$ of simple functions converging uniformly to $$f$$.

By [**Proposition** *(The Integral as a Limit of Integrals of Simple Functions)*](#prpstn:integral-as-limit-of-simple), the operators $$A_{s_i}$$ converge in the operator norm to $$\int_X f \, d\mu$$. By [**Proposition** *(Norm Bound for the Integral of a Simple Function)*](#prpstn:integral-norm-bound-simple), each satisfies $$\left\| A_{s_i} \right\| \le \sup_\lambda \lvert s_i(\lambda) \rvert$$.

Fix $$\epsilon > 0$$ and choose $$N$$ with $$\sup_\lambda \lvert f(\lambda) - s_i(\lambda) \rvert < \epsilon$$ for all $$i \ge N$$. Then for such $$i$$, the triangle inequality for the supremum norm gives $$\sup_\lambda \lvert s_i(\lambda) \rvert \le \sup_\lambda \lvert f(\lambda) \rvert + \epsilon$$, so $$\left\| A_{s_i} \right\| \le \sup_\lambda \lvert f(\lambda) \rvert + \epsilon$$. Since $$A_{s_i} \to \int_X f \, d\mu$$ in the operator norm and the norm is continuous, letting $$i \to \infty$$ yields $$\left\| \int_X f \, d\mu \right\| \le \sup_\lambda \lvert f(\lambda) \rvert + \epsilon$$. As $$\epsilon > 0$$ was arbitrary,

$$
    \left\| \int_X f \, d\mu \right\| \le \sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert,
$$

as required.$$\blacksquare$$

> **Proposition** *(Norm Bound for the Integral of a Simple Function)*
<a name="prpstn:integral-norm-bound-simple"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{lmm:lemma2-of-operator-valued-integration} -->
<!--  \uses{lmm:lemma-1} -->
<!--  \uses{prpstn:hall-a.43} -->
> With notation as in [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration), let $$E_1, E_2, \ldots, E_n \in \Omega(X)$$ be pairwise disjoint with $$X = \bigcup_{i=1}^n E_i$$, let $$c_1, \ldots, c_n \in \mathbb{C}$$, and let
>
> $$
>     s \equiv \sum_{i=1}^n c_i 1_{E_i}
> $$
>
> be the associated simple function, with $$A_s \equiv \int_X s \, d\mu$$. Then
>
> $$
>     \left\| A_s \right\| \le \sup\limits_{\lambda \in X} \lvert s(\lambda) \rvert.
> $$

**Proof**
Consider, as in the lemma, a finite set of elements $$E_1, E_2, \ldots, E_n \in \Omega(X)$$ that are pairwise disjoint and satisfy

$$
    X = \bigcup\limits_{i = 1}^n E_i.
$$

If we are given in addition a set of complex numbers $$c_1, c_2, \ldots, c_n \in \mathbb{C}$$, we can define a simple function $$s$$ by

$$
    s \equiv \sum_{i = 1}^n c_i 1_{E_i}.
$$

As we have already proven,

$$
    \int_X 1_{E_i} = \mu(E_i).
$$

Linearity of the map

$$
    f \longmapsto \int_X f d\mu
$$

then implies that

$$
    \int_X s \, d\mu \equiv A_s = \sum_{i = 1}^n c_i \mu(E_i).
$$

Hence, for any $$\phi, \psi \in \mathbf{H}$$ we have

$$
\begin{align}
    \left< \phi, A_s \psi \right> &= \left< \phi, \left(  \sum_{i = 1}^n c_i \mu(E_i) \right) \psi \right> \\
                                  &= \sum_{i = 1}^n c_i \left< \phi, \mu(E_i) \psi \right> \\
                                  &= \sum_{i = 1}^n c_i \left< \phi, \mu(E_i) \mu(E_i) \psi \right> \\
                                  &= \sum_{i = 1}^n c_i \left< \phi, \mu(E_i)^* \mu(E_i) \psi \right> \\
                                  &= \sum_{i = 1}^n c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right>,
\end{align}
$$

where we have used our previous equation for $$A_s$$, the definition of an inner product, definition of a projection-valued measure, and the definition of an orthogonal projection to conclude

$$
    \left< \phi, A_s \psi \right> = \sum_{i = 1}^n c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right>.
$$

Now using the definition of a norm and applying [**Cauchy–Schwarz**](#prpstn:hall-a.43) twice, first to each summand and then across the sum (viewing $$\|\mu(E_i) \phi\|$$ and $$\|\mu(E_i) \psi\|$$ as vectors in $$\mathbb{R}^n$$), one obtains

$$
\begin{align}
    \left\lvert \left< \phi, A_s \psi \right> \right\rvert &= \left\lvert \sum_{i = 1}^n c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right\rvert \\
                                                 &\le \sum_{i = 1}^n \left\lvert c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right\rvert \\
                                                 &= \sum_{i = 1}^n \left\lvert c_i \right\rvert \, \left\lvert \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right\rvert \\
                                                 &\le \sum_{i = 1}^n \left\lvert c_i \right\rvert \left\| \mu(E_i) \phi \right\| \left\| \mu(E_i) \psi \right\| \\
                                                 &\le \left( \max_i \left\lvert c_i \right\rvert \right)  \sum_{i = 1}^n \left\| \mu(E_i) \phi \right\| \left\| \mu(E_i) \psi \right\| \\
                                                 &\le \left( \max_i \left\lvert c_i \right\rvert \right) \left( \sum_{i = 1}^n \left\| \mu(E_i) \phi \right\|^2 \right)^{1/2} \left( \sum_{i = 1}^n \left\| \mu(E_i) \psi \right\|^2 \right)^{1/2} \\
                                                 &= \left( \max_i \left\lvert c_i \right\rvert \right) \|\phi\| \, \|\psi\|,
\end{align}
$$

where in the final step we employed the second result of [**Lemma**](#lmm:lemma2-of-operator-valued-integration). So in summary

$$
    \left\lvert \left< \phi, A_s \psi \right> \right\rvert \le \left( \max_i \left\lvert c_i \right\rvert \right) \|\phi\| \, \|\psi\|
$$

for all $$\phi, \psi \in \mathbf{H}$$.

As a result of [**Lemma**](#lmm:lemma-1) we can write the operator norm of $$A_s$$ as follows

$$
    \|A_s\| = \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left\lvert \left< \phi, A_s \psi \right> \right\rvert.
$$

Hence, our result implies

$$
\begin{align}
    \|A_s\| &= \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left\lvert \left< \phi, A_s \psi \right> \right\rvert \\
            &\le \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left( \max_i \left\lvert c_i \right\rvert \right) \|\phi\| \, \|\psi\| \\
            &= \left( \max_i \left\lvert c_i \right\rvert \right).
\end{align}
$$

Obviously

$$
    \sup_{\lambda \in X} \lvert s(\lambda) \rvert = \max_i \left\lvert c_i \right\rvert.
$$

Hence, we have proven the desired result

$$
    \|A_s\|  \le \sup_{\lambda \in X} \lvert s(\lambda) \rvert
$$

for our simple function $$s$$.$$\blacksquare$$

> **Proposition** *(The Integral as a Limit of Integrals of Simple Functions)*
<a name="prpstn:integral-as-limit-of-simple"></a>
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:integral-norm-bound-simple} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
> With notation as in [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration), let $$f$$ be a bounded, measurable, complex-valued function on $$X$$ and let $$\{s_i\}_{i \in \mathbb{N}}$$ be a sequence of simple functions converging uniformly to $$f$$. Then $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ is Cauchy in $$\mathcal{B}(\mathbf{H})$$, hence converges in the operator norm to some $$A_s \in \mathcal{B}(\mathbf{H})$$, and
>
> $$
>     A_s = \int_X f \, d\mu.
> $$
>
> That is, the limit operator is the integral already constructed in that theorem. (The identification is what makes the limit construction useful: it is obtained by showing $$\left< \psi, A_s\psi \right> = \int_X f \, d\mu_\psi$$ for all $$\psi$$, and then appealing to the *uniqueness* clause of that theorem.)

**Proof**
This generalization relies upon the [**Theorem** *(Complex-Valued Simple Approximation Theorem)*](#thrm:complex-valued-simple-approximation-theorem). This theorem implies that a sequence of complex-valued simple functions $$\{s_i\}_{i \in \mathbb{N}}$$ on $$X$$ exists such that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ on $$X$$.

Now for any two simple functions $$s_i$$ and $$s_j$$ in this sequence, their difference $$s_i - s_j$$ is also a simple function. Furthermore, linearity of the map

$$
    f \longmapsto \int_X f d\mu
$$

implies

$$
    A_{s_i - s_j} = A_{s_i} - A_{s_j},
$$

and thus

$$
    \|A_{s_i - s_j}\| = \|A_{s_i} - A_{s_j}\|.
$$

However, the result we just proved for simple functions implies

$$
    \|A_{s_i - s_j}\| \le \sup_{\lambda \in X} \lvert s_i(\lambda) - s_j(\lambda) \rvert.
$$

This in turn implies

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &= \|A_{s_i - s_j}\| \\
                          &\le \sup_{\lambda \in X} \lvert s_i(\lambda) - s_j(\lambda) \rvert.
\end{align}
$$

However, the definition of a norm implies

$$
\begin{align}
    \lvert s_i(\lambda) - s_j(\lambda) \rvert &=   \lvert (f(\lambda) - s_j(\lambda)) - (f(\lambda) - s_i(\lambda)) \rvert \\
                                    &\le \lvert f(\lambda) - s_j(\lambda) \rvert + \lvert f(\lambda) - s_i(\lambda) \rvert.
\end{align}
$$

Hence, we can continue our derivation

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &= \|A_{s_i - s_j}\| \\
                          &\le \sup_{\lambda \in X} \lvert s_i(\lambda) - s_j(\lambda) \rvert \\
                          &\le \sup_{\lambda \in X} \left( \lvert f(\lambda) - s_j(\lambda) \rvert + \lvert f(\lambda) - s_i(\lambda) \rvert \right) \\
                          &\le \sup_{\lambda \in X} \lvert f(\lambda) - s_j(\lambda) \rvert + \sup_{\lambda \in X} \lvert f(\lambda) - s_i(\lambda) \rvert.
\end{align}
$$

However, as the sequence $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$k \ge N$$

$$
    \sup_{\lambda \in X}  \lvert f(\lambda) - s_k(\lambda) \rvert < \frac{\epsilon}{2}.
$$

This along with our previous derivation allows us to conclude that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i, j \ge N$$ we have

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &\le \sup_{\lambda \in X} \lvert f(\lambda) - s_j(\lambda) \rvert + \sup_{\lambda \in X} \lvert f(\lambda) - s_i(\lambda) \rvert \\
                          &< \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
                          &= \epsilon.
\end{align}
$$

This is nothing more than the statement that $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ is a Cauchy sequence.

By construction each $$A_{s_i}$$ is an element of $$\mathcal{B}(\mathbf{H})$$. Hence, $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ is a sequence in $$\mathcal{B}(\mathbf{H})$$. As we proved in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space) $$\mathcal{B}(\mathbf{H})$$ is a Banach space. So, in particular, $$\mathcal{B}(\mathbf{H})$$ is complete. Thus there exists an operator $$A_s$$ in $$\mathcal{B}(\mathbf{H})$$ that is the limit of the sequence $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ relative to the operator norm on $$\mathcal{B}(\mathbf{H})$$.

As the sequence $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$k \ge N$$

$$
    \sup_{\lambda \in X}  \lvert f(\lambda) - s_k(\lambda) \rvert < \epsilon.
$$

Hence, using the definition of a norm, we can conclude that for all $$k \ge N$$

$$
\begin{align}
    \sup_{\lambda \in X} \lvert s_k(\lambda) \rvert &=   \sup_{\lambda \in X} \lvert f(\lambda) - (f(\lambda) - s_k(\lambda)) \rvert \\
                                          &\le \sup_{\lambda \in X} \lvert f(\lambda) \rvert + \lvert f(\lambda) - s_k(\lambda) \rvert \\
                                          &\le \sup_{\lambda \in X} \lvert f(\lambda) \rvert + \sup_{\lambda \in X} \lvert f(\lambda) - s_k(\lambda) \rvert \\
                                          &< \sup_{\lambda \in X} \lvert f(\lambda) \rvert + \epsilon.
\end{align}
$$

This implies

$$
    \lim_{i \rightarrow \infty} \sup_{\lambda \in X} \lvert s_i(\lambda) \rvert \le \sup_{\lambda \in X} \lvert f(\lambda) \rvert.
$$

We can also create a similar derivation switching the roles of $$s_k$$ and $$f$$ as follows

$$
\begin{align}
    \sup_{\lambda \in X} \lvert f(\lambda) \rvert &= \sup_{\lambda \in X} \lvert (f(\lambda) - s_k(\lambda)) + s_k(\lambda) \rvert \\
                                        &\le \sup_{\lambda \in X} \lvert f(\lambda) - s_k(\lambda) \rvert +  \lvert s_k(\lambda) \rvert \\
                                        &\le \sup_{\lambda \in X} \lvert f(\lambda) - s_k(\lambda) \rvert +  \sup_{\lambda \in X} \lvert s_k(\lambda) \rvert \\
                                        &< \epsilon +  \sup_{\lambda \in X} \lvert s_k(\lambda) \rvert.
\end{align}
$$

This implies

$$
    \sup_{\lambda \in X} \lvert f(\lambda) \rvert \le \lim_{i \rightarrow \infty} \sup_{\lambda \in X} \lvert s_i(\lambda) \rvert.
$$

The last two conclusions imply

$$
    \lim_{i \rightarrow \infty} \sup_{\lambda \in X} \lvert s_i(\lambda) \rvert = \sup_{\lambda \in X} \lvert f(\lambda) \rvert.
$$

Now tying the last results together

$$
\begin{align}
    \|A_s\| &=   \lim_{i \rightarrow \infty} \| A_{s_i} \| \\
            &\le \lim_{i \rightarrow \infty} \sup_{\lambda \in X} \lvert s_i(\lambda) \rvert \\
            &= \lim_{i \rightarrow \infty} \sup_{\lambda \in X} \lvert f(\lambda) \rvert \\
            &= \sup_{\lambda \in X} \lvert f(\lambda) \rvert.
\end{align}
$$

In other words

$$
    \|A_s\| \le \sup_{\lambda \in X} \lvert f(\lambda) \rvert.
$$

As

$$
    \int_X f \, d\mu \equiv A_f,
$$

this is almost the desired result

$$
    \left\| \int_X f \, d\mu \right\| \le \sup_{\lambda \in X} \lvert f(\lambda) \rvert.
$$

We simply need to identify $$A_f$$ with $$A_s$$ and we will have completed the proof. It is to this we now turn.

We previously proved

$$
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f \, d\mu_\psi
$$

for any $$\psi \in \mathbf{H}$$. So in particular as

$$
    \int_X s_i \, d\mu \equiv A_{s_i},
$$

for any $$s_i$$ of our sequence, our result implies

$$
    \left< \psi, A_{s_i} \psi \right> = \int_X s_i \, d\mu_\psi.
$$

Using this along with the fact that $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ converges uniformly to $$A_s$$ in the operator norm

$$
\begin{align}
    \left< \psi, A_s\psi \right> &= \lim_{i \rightarrow \infty} \left< \psi, A_{s_i} \psi \right> \\
                                 &= \lim_{i \rightarrow \infty} \int_X s_i \, d\mu_\psi \\
                                 &= \int_X \lim_{i \rightarrow \infty} s_i \, d\mu_\psi \\
                                 &= \int_X f \, d\mu_\psi,
\end{align}
$$

where the fact that the convergence is uniform allows us to bring the limit under the integral. Hence,

$$
    \left< \psi, A_s\psi \right> = \int_X f \, d\mu_\psi.
$$

Now previously we proved that there is a unique linear map

$$
    f \longrightarrow \int_X f \, d\mu
$$

such that

$$
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f \, d\mu_\psi.
$$

As this map is unique and

$$
    \left< \psi, A_s\psi \right> = \int_X f \, d\mu_\psi,
$$

it follows that

$$
    A_s = \int_X f \, d\mu
$$

This is the desired identification.$$\blacksquare$$

> **Proposition** *(Operator-Valued Integration is Multiplicative)*
<a name="prpstn:integral-multiplicative"></a>
<!--  \uses{prpstn:integral-mult-indicator} -->
<!--  \uses{prpstn:integral-mult-measurable} -->
<!--  \uses{prpstn:integral-mult-simple} -->
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{prpstn:integral-norm-bound} -->
<!--  \uses{thrm:operator-valued-integration} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all bounded, measurable, complex-valued functions $$f$$ and $$g$$ on $$X$$,
>
> $$
>     \int_X fg \, d\mu = \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right).
> $$

**Proof**
The result is proved in three stages, each resting on the previous: for indicator functions in [**Proposition** *(Multiplicativity of the Integral for Indicator Functions)*](#prpstn:integral-mult-indicator), for simple functions in [**Proposition** *(Multiplicativity of the Integral for Simple Functions)*](#prpstn:integral-mult-simple), and for general bounded, measurable, complex-valued functions in [**Proposition** *(Multiplicativity of the Integral for Bounded Measurable Functions)*](#prpstn:integral-mult-measurable). The last of these is the statement of this proposition.$$\blacksquare$$

> **Proposition** *(Multiplicativity of the Integral for Indicator Functions)*
<a name="prpstn:integral-mult-indicator"></a>
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:indicator-function} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all $$E_1, E_2 \in \Omega(X)$$,
>
> $$
>     \int_X 1_{E_1} 1_{E_2} \, d\mu = \left( \int_X 1_{E_1} \, d\mu \right) \left( \int_X 1_{E_2} \, d\mu \right).
> $$

**Proof**
Consider $$E_1, E_2 \in \Omega(X)$$. [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), along with the projection-valued measure definition imply

$$
\begin{align}
    \left( \int_X 1_{E_1} \, d\mu \right) \left( \int_X 1_{E_2} \, d\mu \right) &= \mu(E_1) \mu(E_2) \\
                                                                                &= \mu(E_1 \cap E_2) \\
                                                                                &= \int_X 1_{E_1 \cap E_2} \, d\mu \\
                                                                                &= \int_X 1_{E_1} 1_{E_2} \, d\mu,
\end{align}
$$

which gives the desired result

$$
    \left( \int_X 1_{E_1} \, d\mu \right) \left( \int_X 1_{E_2} \, d\mu \right) = \int_X 1_{E_1} 1_{E_2} \, d\mu
$$

for indicator functions.
$$\blacksquare$$

> **Proposition** *(Multiplicativity of the Integral for Simple Functions)*
<a name="prpstn:integral-mult-simple"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{prpstn:integral-mult-indicator} -->
<!--  \uses{thrm:operator-valued-integration} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all simple functions $$s_1, s_2$$ on $$X$$,
>
> $$
>     \int_X s_1 s_2 \, d\mu = \left( \int_X s_1 \, d\mu \right) \left( \int_X s_2 \, d\mu \right).
> $$

**Proof**
This result follows from [**Proposition** *(Multiplicativity of the Integral for Indicator Functions)*](#prpstn:integral-mult-indicator) and linearity.

To wit, consider two simple functions $$s_1$$ and $$s_2$$

$$
\begin{align}
    s_1 &= \sum_{i = 1}^n \alpha_i 1_{E_i} \\
    s_2 &= \sum_{j = 1}^m \beta_j 1_{F_j},
\end{align}
$$

where $$\alpha_i, \beta_j \in \mathbb{C}$$ and $$E_i, F_j \in \Omega(X)$$. Linearity implies

$$
\begin{align}
    \int_X s_1 \, d\mu &= \sum_{i = 1}^n \alpha_i \int_X 1_{E_i} \, d\mu \\
    \int_X s_2 \, d\mu &= \sum_{j = 1}^m \beta_j \int_X 1_{F_j} \, d\mu.
\end{align}
$$

Hence, using linearity and [**Proposition** *(Multiplicativity of the Integral for Indicator Functions)*](#prpstn:integral-mult-indicator) we have

$$
\begin{align}
    \left( \int_X s_1 \, d\mu \right) \left( \int_X s_2 \, d\mu \right)
    &= \left( \sum_{i = 1}^n \alpha_i \int_X 1_{E_i} \, d\mu \right) \left( \sum_{j = 1}^m \beta_j \int_X 1_{F_j} \, d\mu \right) \\
    &= \sum_{i = 1}^n \sum_{j = 1}^m \alpha_i \beta_j \left( \int_X 1_{E_i} \, d\mu \right) \left( \int_X 1_{F_j} \, d\mu \right) \\
    &= \sum_{i = 1}^n \sum_{j = 1}^m \alpha_i \beta_j \int_X 1_{E_i} 1_{F_j} \, d\mu \\
    &= \int_X \sum_{i = 1}^n \sum_{j = 1}^m \alpha_i \beta_j 1_{E_i} 1_{F_j} \, d\mu \\
    &= \int_X s_1 s_2 \, d\mu,
\end{align}
$$

proving

$$
    \left( \int_X s_1 \, d\mu \right) \left( \int_X s_2 \, d\mu \right) = \int_X s_1 s_2 \, d\mu,
$$

> **Proposition** *(Products of Uniform Approximants Converge Uniformly)*
<a name="prpstn:products-converge-uniformly"></a>
<!--  \uses{prpstn:basic-integral-properties} -->
> Let $$f, g$$ be bounded, complex-valued functions on a set $$X$$, and let $$\{s_i\}$$ and $$\{r_j\}$$ be sequences of complex-valued functions converging uniformly to $$f$$ and $$g$$ respectively, with each $$r_j$$ bounded. Then $$s_i r_j \rightarrow fg$$ uniformly as $$i, j \rightarrow \infty$$: for every $$\epsilon > 0$$ there is an $$N$$ with
>
> $$
>     \sup\limits_{\lambda \in X} \lvert f(\lambda)g(\lambda) - s_i(\lambda)r_j(\lambda) \rvert < \epsilon
> $$
>
> for all $$i, j \ge N$$.

**Proof**
Consider any $$s_i$$ and $$r_j$$. One has

$$
\begin{align}
    \lvert s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda) \rvert &=   \lvert s_i(\lambda)r_j(\lambda) - f(\lambda)r_j(\lambda) + f(\lambda)r_j(\lambda) - f(\lambda)g(\lambda) \rvert \\
                                                      &\le \lvert s_i(\lambda)r_j(\lambda) - f(\lambda)r_j(\lambda) \rvert + \lvert f(\lambda)r_j(\lambda) - f(\lambda)g(\lambda) \rvert \\
                                                      &= \lvert r_j(\lambda) \rvert \, \lvert s_i(\lambda) - f(\lambda) \rvert + \lvert f(\lambda) \rvert \, \lvert r_j(\lambda) - g(\lambda) \rvert.
\end{align}
$$

As $$f$$ is bounded and $$r_j$$ is a simple function, their suprema are finite numbers. This allows us to continue this derivation as follows

$$
    \lvert s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda) \rvert \le \left( \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert \right) \lvert s_i(\lambda) - f(\lambda) \rvert + \left( \sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert \right) \lvert r_j(\lambda) - g(\lambda) \rvert.
$$

Now as $$g$$ is bounded there exists a real constant $$M_g$$ such that

$$
    \sup\limits_{\lambda \in X} \lvert g(\lambda) \rvert \le M_g.
$$

As $$r_j \rightarrow g$$ uniformly, for $$\epsilon = 1$$ there exists an integer $$N_1$$ such that for all $$j \ge N_1$$ and all $$\lambda \in X$$ one has

$$
    \lvert r_j(\lambda) - g(\lambda) \rvert < 1.
$$

The definition of a norm and our previous results then imply that for all $$j \ge N_1$$ and all $$\lambda \in X$$ one has

$$
\begin{align}
    \lvert r_j(\lambda) \rvert &= \lvert r_j(\lambda) - g(\lambda) + g(\lambda) \rvert \\
                               &\le \lvert r_j(\lambda) - g(\lambda) \rvert + \lvert g(\lambda) \rvert \\
                               &< 1 + M_g.
\end{align}
$$

Taking the supremum while still requiring $$j \ge N_1$$ gives

$$
    \sup\limits_{j \ge N_1} \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert < 1 + M_g.
$$

Noting that the $$r_j$$ are simple functions and thus bounded we can define the real constant $$C$$ by

$$
    C \equiv \max \left\{ \sup\limits_{\lambda \in X} \lvert r_1(\lambda) \rvert, \ldots, \sup\limits_{\lambda \in X} \lvert r_{N_1 - 1} (\lambda) \rvert, 1 + M_g \right\},
$$

then it obviously follows that

$$
    \sup\limits_{j \in \mathbb{N}} \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert \le C.
$$

In other words there is a bound $$C$$ on the $$r_j$$ that holds uniformly for all $$\lambda \in X$$ and all $$j$$.
    
Now as $$s_i$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists an $$N$$ such that for all $$i \ge N$$ one has

$$
    \sup\limits_{\lambda \in X} \lvert s_i(\lambda) - f(\lambda) \rvert < \left( \frac{\epsilon}{2 C} \right).
$$

Similarly, set $$M_f \equiv 1 + \sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert$$, which is finite since $$f$$ is bounded and satisfies $$M_f > 0$$ and $$\sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert \le M_f$$ — the added $$1$$ is what keeps $$M_f$$ non-zero in the degenerate case $$f \equiv 0$$, so that the division below is always legitimate. As $$r_j$$ converges uniformly to $$g$$, for this same $$\epsilon > 0$$ there exists an $$M$$ such that for all $$j \ge M$$ one has

$$
    \sup\limits_{\lambda \in X} \lvert r_j(\lambda) - g(\lambda) \rvert < \frac{\epsilon}{2 M_f}.
$$

This implies that for all $$i,j \ge \max(N,M)$$ we have

$$
\begin{align}
    \lvert s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda) \rvert
    &\le \left( \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert \right) \lvert s_i(\lambda) - f(\lambda) \rvert + \left( \sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert \right) \lvert r_j(\lambda) - g(\lambda) \rvert \\
    &<   \left( \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert \right) \left( \frac{\epsilon}{2 C} \right) + \left( \sup\limits_{\lambda \in X} \lvert f(\lambda) \rvert \right) \left( \frac{\epsilon}{2 M_f} \right) \\
    &\le \frac{\epsilon}{2} +  \frac{\epsilon}{2} \\
    &= \epsilon,
\end{align}
$$

where the third line follows from our previous result

$$
    \sup\limits_{j \in \mathbb{N}} \sup\limits_{\lambda \in X} \lvert r_j(\lambda) \rvert \le C.
$$ 

This implies that for any $$\epsilon > 0$$ there exists a natural number $$L$$ such that for all $$i,j \ge L$$ we have

$$
    \sup\limits_{\lambda \in X} \lvert f(\lambda)g(\lambda) - s_i(\lambda)r_j(\lambda) \rvert < \epsilon.
$$

This along with our previous result

$$
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_j \, d\mu \right) \right\| \le \sup\limits_{\lambda \in X} \lvert f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) \rvert
$$

implies that for any $$\epsilon > 0$$ there exists a natural number $$L$$ such that for all $$i,j \ge L$$ we have

$$
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_j \, d\mu \right) \right\| < \epsilon.
$$
$$\blacksquare$$

as required.
$$\blacksquare$$

> **Proposition** *(Multiplicativity of the Integral for Bounded Measurable Functions)*
<a name="prpstn:integral-mult-measurable"></a>
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{prpstn:products-converge-uniformly} -->
<!--  \uses{prpstn:integral-mult-simple} -->
<!--  \uses{prpstn:integral-norm-bound} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{prpstn:integral-as-limit-of-simple} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all bounded, measurable, complex-valued functions $$f, g$$ on $$X$$,
>
> $$
>     \int_X fg \, d\mu = \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right).
> $$

**Proof**

As one will recall [**Theorem** *(Complex-Valued Simple Approximation Theorem)*](#thrm:complex-valued-simple-approximation-theorem) implies that there exist sequences of complex-valued simple functions $$\{s_i\}_{i \in \mathbb{N}}$$ and $$\{r_j\}_{j \in \mathbb{N}}$$ on $$X$$ such that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to a bounded, measurable, complex-valued function $$f$$ on $$X$$ and similarly $$\{r_j\}_{j \in \mathbb{N}}$$ to $$g$$.

By [**Proposition** *(The Integral as a Limit of Integrals of Simple Functions)*](#prpstn:integral-as-limit-of-simple), applied to $$\{s_i\}$$ and to $$\{r_j\}$$ in turn,

$$
    \int_X s_i \, d\mu \longrightarrow \int_X f \, d\mu
    \qquad\text{and}\qquad
    \int_X r_j \, d\mu \longrightarrow \int_X g \, d\mu
$$

in the operator norm.

Similarly, uniform convergence along with linearity imply for any $$s_i$$ and $$r_j$$

$$
\begin{align}
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_j \, d\mu \right) \right\|
    &= \left\| \int_X (fg - s_i r_j) \, d\mu \right\| \\
    &\le \sup\limits_{\lambda \in X} \lvert f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) \rvert
\end{align}
$$

where in the final step we employed [**Proposition** *(Norm Bound for the Operator-Valued Integral)*](#prpstn:integral-norm-bound). Looking at this bound, one concludes that if we can prove that given any $$\epsilon > 0$$, there exists a natural number $$N$$ such that for all $$i,j \ge N$$ one has

$$
    \sup\limits_{\lambda \in X} \lvert f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) \rvert < \epsilon,
$$

then we can conclude that the operator-valued integral of $$s_ir_j$$ converges to the operator-valued integral of $$fg$$.

That supremum bound is [**Proposition** *(Products of Uniform Approximants Converge Uniformly)*](#prpstn:products-converge-uniformly) above, applied to $$\{s_i\}$$ and $$\{r_j\}$$; it holds for all $$i,j \ge N$$, and hence the operator-valued integral of $$s_i r_j$$ converges to that of $$fg$$.

In particular, this holds when $$j = i$$: for any $$\epsilon > 0$$ there exists a natural number $$L$$ such that for all $$i \ge L$$ we have

$$
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_i \, d\mu \right) \right\| < \epsilon.
$$

In other words, the single-indexed sequence of operator-valued integrals of $$s_i r_i$$ converges, in the operator norm, to the operator-valued integral of $$fg$$

$$
    \int_X s_i r_i \, d\mu \longrightarrow \int_X fg \, d\mu.
$$

Now recall from [**Proposition** *(Multiplicativity of the Integral for Simple Functions)*](#prpstn:integral-mult-simple) that for every $$i$$, as $$s_i$$ and $$r_i$$ are both simple functions,

$$
    \left( \int_X s_i \, d\mu \right) \left( \int_X r_i \, d\mu \right) = \int_X s_i r_i \, d\mu
$$

exactly, with no limit involved. Combining this exact identity with the convergence just established gives

$$
    \left( \int_X s_i \, d\mu \right) \left( \int_X r_i \, d\mu \right) \longrightarrow \int_X fg \, d\mu
$$

as $$i \rightarrow \infty$$.

On the other hand, as we established earlier in this proof,

$$
\begin{align}
    \int_X s_i \, d\mu &\rightarrow \int_X f \, d\mu \\
    \int_X r_i \, d\mu &\rightarrow \int_X g \, d\mu
\end{align}
$$

in the operator norm. Operator multiplication is jointly continuous with respect to the operator norm: for any $$X_i \rightarrow X$$ and $$Y_i \rightarrow Y$$ in $$\mathcal{B}(\mathbf{H})$$, submultiplicativity gives

$$
\begin{align}
    \left\| X_iY_i - XY \right\| &=   \left\| X_i(Y_i - Y) + (X_i - X)Y \right\| \\
                                 &\le \left\| X_i \right\| \left\| Y_i - Y \right\| + \left\| X_i - X \right\| \left\| Y \right\| \longrightarrow 0,
\end{align}
$$

where we have used that $$\{ \|X_i\| \}_{i \in \mathbb{N}}$$ is bounded, being a convergent sequence of real numbers. Applying this with

$$
\begin{align}
    X_i = \int_X s_i \, d\mu &\qquad \qquad X   = \int_X f \, d\mu \\
    Y_i = \int_X r_i \, d\mu &\qquad \qquad Y   = \int_X g \, d\mu
\end{align}
$$

gives

$$
    \left( \int_X s_i \, d\mu \right) \left( \int_X r_i \, d\mu \right) \longrightarrow \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right)
$$

as $$i \rightarrow \infty$$.

We have thus shown that the single sequence

$$
    \left\{ \left( \int_X s_i \, d\mu \right) \left( \int_X r_i \, d\mu \right) \right\}_{i \in \mathbb{N}}
$$

converges, in the operator norm, to both

$$
    \int_X fg \, d\mu
$$

and

$$
    \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right).
$$

As limits in $$\mathcal{B}(\mathbf{H})$$ with respect to the operator norm are unique, this implies

$$
    \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right) = \int_X fg \, d\mu,
$$

the desired result, integration is multiplicative for bounded, measurable, complex-valued functions $$f$$ and $$g$$.
$$\blacksquare$$


> **Proposition** *(Operator-Valued Integration Intertwines Conjugation and the Adjoint)*
<a name="prpstn:integral-conjugation"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{thrm:operator-valued-integration} -->
> With notation as in [**Proposition** *(Integral of an Indicator Function)*](#prpstn:integral-of-indicator), for all bounded, measurable, complex-valued functions $$f$$ on $$X$$,
>
> $$
>     \int_X \overline{f} \, d\mu = \left( \int_X f \, d\mu \right)^*,
> $$
>
> where $$\overline{f}$$ is the complex conjugate of $$f$$ and the superscript $$*$$ denotes the adjoint on $$\mathcal{B}(\mathbf{H})$$. In particular, if $$f$$ is real-valued then $$f = \overline{f}$$ and $$\int_X f \, d\mu$$ is self-adjoint.

**Proof**
Finally we must prove that for all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have

$$
    \int_X \overline{f} \, d\mu = \left( \int_X f \, d\mu \right)^*,
$$

where $$\overline{f}$$ is the complex conjugate of $$f$$ and the superscript $$*$$ denotes the adjoint on $$\mathcal{B}(\mathbf{H})$$ arising from the Hilbert space inner product.

Let us start by considering the case in which $$f$$ is real. The map $$Q_f$$ introduced in the construction of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) is given by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi.
$$

for all $$\psi \in \mathbf{H}$$. As $$f$$ is real, this implies that $$Q_f(\psi)$$ is real. As $$Q_f(\psi)$$ is real, the [**Proposition**](#prpstn:hall-a.63) we previously proved along with the definition of $$A_f$$

$$
    Q_f(\psi) = \left< \psi, A_f \psi \right>
$$

imply that $$A_f$$ is self-adjoint. As $$A_f$$ is self-adjoint, it implies that

$$
    \int_X f \, d\mu \equiv A_f
$$

is also self-adjoint.

Consider now the case in which $$f$$ is complex. This implies that $$f$$ can be written as

$$
    f = f_1 + if_2,
$$

where both $$f_1$$ and $$f_2$$ are real. Linearity then implies

$$
\begin{align}
    \int_X \overline{f} \, d\mu &= \int_X \overline{(f_1 + if_2)} \, d\mu \\
                                &= \int_X (f_1 - if_2) \, d\mu \\
                                &= \int_X f_1 \, d\mu - i \int_X f_2 \, d\mu \\
                                &= \left( \int_X f_1 \, d\mu + i \int_X f_2 \, d\mu \right)^* \\
                                &= \left( \int_X (f_1 + i f_2) \, d\mu \right)^* \\
                                &= \left( \int_X f \, d\mu \right)^*,
\end{align}
$$

where when taking the adjoint we have also used our previous result that $$A_{f_i} = A_{f_i}^*$$ when $$f_i$$ is real. This proves the desired result

$$
    \int_X \overline{f} \, d\mu = \left( \int_X f \, d\mu \right)^*
$$
$$\blacksquare$$

### The Spectral Theorem
The development below constructs, for a self-adjoint $$A \in \mathcal{B}(\mathbf{H})$$, a continuous functional calculus, extends it to bounded Borel functions, and reads off from it a projection-valued measure. The spectral theorem itself is stated and proved at the end of this section, once those pieces are in place.

Throughout, we speak informally of a *functional calculus* — an association $$f \mapsto f(A)$$ — but no definition is needed yet: the two constructions actually used are given, where they are needed, by [**Proposition**](#prpstn:hall-8.3) for continuous $$f$$ and [**Definition**](#def:hall-8.8) for bounded measurable $$f$$, and the notion is named normatively only once the theorem is proved, in [**Definition** *(Functional Calculus)*](#def:functional-calculus).

Together the two stages establish [**Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*](#thrm:spectral-theorem-for-bounded-operators), stated and proved at the end of this section.

*Stage 1:* In the first stage any self-adjoint $$A \in \mathcal{B}(\mathbf{H})$$ is used to construct a "continuous functional calculus" that associates to each continuous function $$f$$ on $$\sigma(A)$$ an operator $$f(A)$$.

This association is such that for any natural number $$m$$ the function $$f(\lambda) = \lambda^m$$ is associated with the operator $$f(A)=A^m$$. The full "continuous functional calculus" is then constructed by approximating arbitrary continuous functions $$f$$ on $$\sigma(A)$$ by polynomials.

The [**Stone–Weierstrass Theorem for Real Numbers**](#thrm:stone–weierstrass-real) implies that polynomials are dense in the space of continuous functions on $$\sigma(A)$$. Hence, for any continuous function $$f$$ on $$\sigma(A)$$ there exists a sequence of polynomials $$\{p_i\}_{i \in \mathbb{N}}$$ that converge uniformly to $$f$$ on $$\sigma(A)$$. The final step of stage 1 then proves that the sequence of operators $$\{p_i(A)\}_{i \in \mathbb{N}}$$ converge to an operator denoted as $$f(A)$$.

*Stage 2:* The second stage shows that for a continuous function $$f$$ on $$\sigma(A)$$ the operator $$f(A)$$ of the first stage can be represented as integration against a projection-valued measure. This amounts to an operator-valued version of the [**Riesz Representation Theorem**](#thrm:riesz-representation) from measure theory.

**Stage 1: The Continuous Functional Calculus**

We begin this stage with "utility" lemmas and propositions that we will have need of later in this stage.

#### Stage 1: The Continuous Functional Calculus

> **Lemma** *(Bounded Operator Product is Submultiplicative)*
<a name="lmm:lemma-2"></a>
<!--  \uses{def:bounded-operator-notation} -->
> Let $$A, B \in \mathcal{B}(\mathbf{H})$$, then the operator product is *submultiplicative*
> 
> $$
>     \|AB\| \le \|A\| \, \|B\|.
> $$

**Proof**
Consider arbitrary $$A$$ and $$B$$ in $$\mathcal{B}(\mathbf{H})$$ and an arbitrary element $$\psi$$ in $$\mathbf{H}$$ such that $$\|\psi\| = 1$$.

Let us first consider the case in which $$B\psi \neq 0$$. As $$B\psi \neq 0$$ it follows that $$\|B\psi\| \neq 0$$. Hence,

$$
\begin{align}
    \|AB\psi\| &= \left\| A \left( \frac{\|B\psi\|}{\|B\psi\|} \right) B\psi \right\| \\
               &= \|B\psi\| \left\| A \left( \frac{B\psi}{\|B\psi\|} \right) \right\|.
\end{align}
$$

Obviously,

$$
    \left( \frac{B\psi}{\|B\psi\|} \right)
$$

has norm $$1$$. Furthermore, by definition

$$
\begin{align}
    \|A\| &= \sup\limits_{\|\phi\| = 1} \|A\phi\| \\
    \|B\| &= \sup\limits_{\|\phi\| = 1} \|B\phi\|.
\end{align}
$$

Hence, as $$\|\psi\| = 1$$ the previous derivation can proceed as follows

$$
\begin{align}
    \|AB\psi\| &= \left\| A \left( \frac{\|B\psi\|}{\|B\psi\|} \right) B\psi \right\| \\
               &= \|B\psi\| \left\| A \left( \frac{B\psi}{\|B\psi\|} \right) \right\| \\
               &\le \|B\| \, \|A\|.
\end{align}
$$

In other words for $$\|\psi\| = 1$$ such that $$B\psi \neq 0$$

$$
    \|AB\psi\| \le \|B\| \, \|A\|.
$$

Taking the supremum of the lefthand side this gives

$$
    \sup\limits_{\|\psi\| = 1 \text{ and } B\psi \neq 0} \|AB\psi\| \le \|B\| \, \|A\|,
$$

which as

$$
    \|AB\| = \sup\limits_{\|\psi\| = 1} \|AB\psi\|
$$

is almost the desired equation $$\|AB\| \le \|A\| \,\|B\|$$. We just need to prove it holds for $$B\psi = 0$$.

If $$\|\psi\| = 1$$ and $$B\psi = 0$$, then $$AB\psi = 0$$, and thus $$\|AB\psi\| = 0$$. Hence, the supremum of $$\|AB\psi\|$$ over such $$\psi$$ is $$0$$. As the supremum over such $$\psi$$ is zero, this supremum is always less than or equal to $$\|B\| \, \|A\|$$. Hence, the bound above

$$
    \sup\limits_{\|\psi\| = 1 \text{ and } B\psi \neq 0} \|AB\psi\| \le \|B\| \, \|A\|,
$$

is also satisfied for $$\psi$$ that satisfy $$B\psi = 0$$.

Hence, we have proven that

$$
    \sup\limits_{\|\psi\| = 1} \|AB\psi\| \le \|B\| \, \|A\|,
$$

which as a result of the definition of operator norm implies

$$
    \|AB\| \le \|A\| \, \|B\|,
$$

the desired result, operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative.$$\blacksquare$$

The next lemma uses the following standard fact about absolutely convergent series in a Banach space, which we state first.

> **Proposition** *(Absolute Convergence Implies Convergence in a Banach Space)*
<a name="prpstn:hall-a.34"></a>
> If $$V$$ is a Banach space, then absolute convergence implies convergence in $$V$$. That is, if $$\{\psi_i\}_{i \in \mathbb{N}}$$ is a sequence in $$V$$ and
>
> $$
>     \sum\limits_{i \in \mathbb{N}} \|\psi_i\| < \infty,
> $$
>
> then
>
> $$
>     \sum\limits_{i \in \mathbb{N}} \psi_i
> $$
>
> converges in $$V$$.

The next "utility" lemma we must prove is the following

> **Lemma** *(Neumann Series for a Contraction)*
<a name="lmm:hall-7.6"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-inverse} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{lmm:lemma-2} -->
<!--  \uses{prpstn:hall-a.34} -->
> Suppose $$X \in \mathcal{B}(\mathbf{H})$$ satisfies $$\|X\| < 1$$, where $$\|X\|$$ is the operator norm of $$X$$. Then the operator $$I - X$$ has a bounded inverse $$(I - X)^{-1}$$ in $$\mathcal{B}(\mathbf{H})$$; and this bounded inverse is given by the following series
>
> $$
>     (I - X)^{-1} = \mathbf{1} + X + X^2 + X^3 + \cdots
> $$
>
> that is convergent in $$\mathcal{B}(\mathbf{H})$$ with respect to the operator norm.

**Proof**
As a result of [**Lemma** *(Bounded Operator Product is Submultiplicative)*](#lmm:lemma-2) the product of operators $$A,B \in \mathcal{B}(\mathbf{H})$$ is submultiplicative,

$$
    \|AB\| \le \|A\| \, \|B\|,
$$

thus for an arbitrary natural number $$m$$ one has

$$
    \|X^m\| \le \|X^{m - 1}\| \, \|X\| \le \|X^{m-2}\| \, \|X\|^2 \le \cdots \le \|X\|^m.
$$

In other words $$\|X^m\| \le \|X\|^m$$.

Now the hypothesis $$\|X\| < 1$$ implies that the geometric series $$\{\|X\|^m\}_{m \in \mathbb{N}}$$ converges

$$
    \sum\limits_{m \in \mathbb{N}} \|X\|^m < \infty.
$$

Furthermore, as $$\|X^m\| \le \|X\|^m$$ this further implies the series $$\{\|X^m\|\}_{m \in \mathbb{N}}$$ also converges

$$
    \sum\limits_{m \in \mathbb{N}} \|X^m\| < \infty.
$$

Explicitly this follows from the definition of norm, $$\|X^m\| \le \|X\|^m$$, and convergence of the series $$\{\|X\|^m\}_{m \in \mathbb{N}}$$ together implying

$$
    0 \le \sum\limits_{m \in \mathbb{N}} \|X^m\| \le \sum\limits_{m \in \mathbb{N}} \|X\|^m < \infty.
$$

Finally, recalling the fact established in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space) that $$\mathcal{B}(\mathbf{H})$$ is a Banach space with respect to the operator norm, one can use the [**Proposition**](#prpstn:hall-a.34) to conclude that the series $$\{X^m\}_{m \in \mathbb{N}}$$ converges in $$\mathcal{B}(\mathbf{H})$$ with respect to the operator norm. In other words the series

$$
    \mathbf{1} + X + X^2 + X^3 + \cdots
$$

of the hypothesis converges in $$\mathcal{B}(\mathbf{H})$$, one of the desired results.

Now if we consider this convergent series of the hypothesis

$$
    \mathbf{1} + X + X^2 + X^3 + \cdots
$$

and multiply by $$(\mathbf{1} - X)$$ we find

$$
\begin{align}
    (\mathbf{1} - X) \left( \mathbf{1} + X + X^2 + \cdots \right) &= (\mathbf{1} - X) + (X - X^2) + (X^2 - X^3) + (X^3 - \cdots) + \cdots \\
                                                                  &= \mathbf{1} + (- X + X) + (- X^2 + X^2) + (-X^3 + X^3) + \cdots \\
                                                                  &= \mathbf{1},
\end{align}
$$

proving the right inverse is given by

$$
    (\mathbf{1} - X)^{-1} = \mathbf{1} + X + X^2 + X^3 + \cdots.
$$

A similar computation also proves

$$
   \left( \mathbf{1} + X + X^2 + \cdots \right) (\mathbf{1} - X) = \mathbf{1},
$$

establishing that the left inverse is given by the same expression

$$
    (\mathbf{1} - X)^{-1} = \mathbf{1} + X + X^2 + X^3 + \cdots.
$$

The proof of the next proposition draws on two standard results from complex analysis, which we state first.

> **Theorem** *(Analytic Equivalence Theorem)*
<a name="thrm:analytic-equivalence-theorem"></a>
> Let $$U$$ be an open subset of $$\mathbb{C}$$ and let $$f: U \rightarrow \mathbb{C}$$ be a function. Then $$f$$ is analytic on $$U$$ if and only if it is holomorphic on $$U$$.

> **Theorem** *(Maximum Modulus Principle)*
<a name="thrm:maximum-modulus-principle"></a>
> Let $$B$$ be a bounded, non-empty, connected open subset of $$\mathbb{C}$$. Let $$\overline{B}$$ be the closure of $$B$$. Suppose $$f : \overline{B} \rightarrow \mathbb{C}$$ is a continuous function that is holomorphic on $$B$$. Then $$\lvert f(z) \rvert$$ attains its maximum at some point on the boundary of $$B$$.

Together these imply the final desired result.$$\blacksquare$$

> **Proposition** *(The Spectrum is Closed, Bounded and Non-Empty)*
<a name="prpstn:hall-7.5"></a>
<!--  \uses{conv:nonzero-hilbert-space} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-7.6} -->
<!--  \uses{thrm:analytic-equivalence-theorem} -->
<!--  \uses{thrm:maximum-modulus-principle} -->
> Suppose $$\mathbf{H} \ne \{0\}$$. For all $$A \in \mathcal{B}(\mathbf{H})$$, the following results hold.
>
> 1. The spectrum $$\sigma(A)$$ of $$A$$ is a closed, bounded, and non-empty subset of $$\mathbb{C}$$.
>
>    The hypothesis $$\mathbf{H} \ne \{0\}$$ is needed only for non-emptiness: on the zero space the only operator is $$0$$, and $$A - \lambda\mathbf{1} = 0$$ is a bijection of $$\{0\}$$ onto itself with bounded inverse for every $$\lambda$$, so every $$\lambda$$ lies in the resolvent set and $$\sigma(A) = \emptyset$$. Closedness and boundedness hold regardless.
> 2. If $$\lvert \lambda \rvert > \|A\|$$, where $$\|A\|$$ is the operator norm of $$A$$, then $$\lambda$$ is in the resolvent set of $$A$$.

**Proof**
For any non-zero $$\lambda \in \mathbb{C}$$ and $$A$$ from our hypothesis, consider the operator

$$
    A - \lambda \mathbf{1} = -\lambda \left( \mathbf{1} - \frac{A}{\lambda} \right).
$$

If $$\lvert \lambda \rvert > \|A\|$$, then $$\|A / \lambda\| < 1$$ and as a result of the [**Lemma**](#lmm:hall-7.6) we just proved $$(\mathbf{1} - A / \lambda)$$ is invertible. As a result of the previous equation and $$\lambda \neq 0$$, this then implies that $$A - \lambda \mathbf{1}$$ is also invertible, with inverse given by

$$
    (A - \lambda \mathbf{1})^{-1} = - \frac{1}{\lambda} \left( \mathbf{1} + \frac{A}{\lambda} + \frac{A^2}{\lambda^2} + \frac{A^3}{\lambda^3} + \cdots \right).
$$

Hence, $$\lambda$$ is in the resolvent set of $$A$$.

This establishes that if $$\lvert \lambda \rvert > \|A\|$$, then $$\lambda$$ is in the resolvent set of $$A$$, which is the desired result of Part 2 of the proposition.

Furthermore, as $$\lvert \lambda \rvert > \|A\|$$ implies that $$\lambda$$ is in the resolvent set of $$A$$ and the spectrum $$\sigma(A)$$ is the complement of the resolvent set in $$\mathbb{C}$$, this also proves that the spectrum $$\sigma(A)$$ of $$A$$ is bounded. This is one of the desired results of Part 1 of the proposition.

Suppose now that $$\lambda_0 \in \mathbb{C}$$ is in the resolvent set of $$A$$. For any other $$\lambda \in \mathbb{C}$$ one has

$$
\begin{align}
    A - \lambda \mathbf{1} &= A - \lambda_0 \mathbf{1} - (\lambda - \lambda_0) \mathbf{1} \\
                           &= (A - \lambda_0 \mathbf{1}) (\mathbf{1} - (\lambda - \lambda_0) (A - \lambda_0 \mathbf{1})^{-1} ),
\end{align}
$$

where in the second line we have used the fact that $$\lambda_0$$ is in the resolvent set of $$A$$ to factor out $$(A - \lambda_0 \mathbf{1})$$.

Looking at the previous equation along with the [**Lemma**](#lmm:hall-7.6) we just proved, we can conclude that if

$$
    \lvert \lambda - \lambda_0 \rvert < \frac{1}{\|(A - \lambda_0 \mathbf{1})^{-1}\|},
$$

then both factors on the righthand side of the previous equation are invertible, and thus $$A - \lambda \mathbf{1}$$ would also be invertible. This implies that the resolvent set of $$A$$ is open and thus the spectrum $$\sigma(A)$$ of $$A$$, the complement of the resolvent set in $$\mathbb{C}$$, is closed. This is another one of the desired results of Part 1 of the proposition.

The final result that needs to be proven in the proposition is that the spectrum $$\sigma(A)$$ is non-empty, which is in Part 1 of the proposition.

Continuing on with the previous calculation where $$\lambda_0$$ is in the resolvent set of $$A$$ but now under the additional assumption that

$$
    \lvert \lambda - \lambda_0 \rvert < \frac{1}{\|(A - \lambda_0 \mathbf{1})^{-1}\|},
$$

we see that the righthand side of

$$
    A - \lambda \mathbf{1} = (A - \lambda_0 \mathbf{1})(\mathbf{1} - (\lambda - \lambda_0) (A - \lambda_0 \mathbf{1})^{-1} ),
$$

is invertible. This gives

$$
\begin{align}
    (A - \lambda \mathbf{1})^{-1} &= (\mathbf{1} - (\lambda - \lambda_0) (A - \lambda_0 \mathbf{1})^{-1} )^{-1} (A - \lambda_0 \mathbf{1})^{-1} \\
                                  &= \left( \sum_{m \in \mathbb{N}} (\lambda - \lambda_0)^m ((A - \lambda_0 \mathbf{1})^{-1})^m \right) (A - \lambda_0 \mathbf{1})^{-1},
\end{align}
$$

where the second equality follows from the [**Lemma**](#lmm:hall-7.6) we just proved.

This implies that in the neighborhood of any point $$\lambda_0$$ in the resolvent set of $$A$$ the resolvent $$(A - \lambda \mathbf{1})^{-1}$$ can be expressed by this locally convergent series in powers of $$(\lambda - \lambda_0)$$ with coefficients of these powers being elements of $$\mathcal{B}(\mathbf{H})$$.

Hence, for any $$\phi, \psi \in \mathbf{H}$$ the map

$$
    \lambda \longmapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>
$$

can be expressed as a locally convergent power series with coefficients in $$\mathbb{C}$$. In other words it is an analytic function on the resolvent set of $$A$$ which, as we have proven, is open. Thus, as a result of the [**Analytic Equivalence Theorem**](#thrm:analytic-equivalence-theorem) this function is holomorphic on the resolvent set of $$A$$.

Now, as we proved earlier, for $$\lambda$$ in the resolvent set of $$A$$ we can also write $$(A - \lambda \mathbf{1})^{-1}$$ as

$$
    (A - \lambda \mathbf{1})^{-1} = - \frac{1}{\lambda} \left( \mathbf{1} + \frac{A}{\lambda} + \frac{A^2}{\lambda^2} + \frac{A^3}{\lambda^3} + \cdots \right).
$$

This manner of writing $$(A - \lambda \mathbf{1})^{-1}$$ makes it clear that $$\|(A - \lambda \mathbf{1})^{-1}\|$$ tends to zero as $$\lvert \lambda \rvert$$ tends to infinity. Hence, the righthand side of our other expression for $$\| (A - \lambda \mathbf{1})^{-1} \|$$

$$
    \left\| (A - \lambda \mathbf{1})^{-1} \right\| = \left\| \left( \sum_{m \in \mathbb{N}} (\lambda - \lambda_0)^m ((A - \lambda_0 \mathbf{1})^{-1})^m \right) (A - \lambda_0 \mathbf{1})^{-1} \right\|,
$$

also tends to zero as $$\lvert \lambda \rvert$$ tends to infinity. And thus so does the holomorphic function

$$
    \lambda \longmapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>
$$

in the same limit.

Now let us assume the spectrum $$\sigma(A)$$ of $$A$$ is the empty set. Then the resolvent set of $$A$$, the complement of $$\sigma(A)$$ in $$\mathbb{C}$$, would be all of $$\mathbb{C}$$. This would then imply that the holomorphic function $$\lambda \mapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ is holomorphic on all of $$\mathbb{C}$$. In other words it is an entire function.

Hence, by evaluating the entire function $$\lambda \mapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ on ever larger closed disks $$\overline{B}$$, the [**Maximum Modulus Principle**](#thrm:maximum-modulus-principle) implies that the maximum of $$\lvert \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right> \rvert$$ is zero. As a result of the definition of a norm, this in turn implies that $$\left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ is identically zero.

As this is true for any $$\phi, \psi \in \mathbf{H}$$, it implies that $$(A - \lambda \mathbf{1})^{-1}$$ has operator norm zero and is thus the zero operator. However, we know that $$(A - \lambda \mathbf{1})(A - \lambda \mathbf{1})^{-1} = \mathbf{1}$$. Thus, $$(A - \lambda \mathbf{1})^{-1}$$ can not be the zero operator, and we have arrived at a contradiction.

Hence, our assumption that the spectrum $$\sigma(A)$$ of $$A$$ is the empty set is false. The spectrum $$\sigma(A)$$ is non-empty. This is the final desired result of Part 1.$$\blacksquare$$


The proof of the preceding proposition establishes two facts about the resolvent that later arguments use directly. We record them as a separate result rather than reaching into that proof.

> **Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*
<a name="prpstn:resolvent-holomorphy-and-neumann-series"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{conv:nonzero-hilbert-space} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{lmm:hall-7.6} -->
> Suppose $$\mathbf{H} \ne \{0\}$$ and $$A \in \mathcal{B}(\mathbf{H})$$.
>
> 1. The resolvent set of $$A$$ is open, and near every point $$\lambda_0$$ in it, the resolvent $$\lambda \mapsto (A-\lambda\mathbf{1})^{-1}$$ is given by an operator-norm-convergent power series in $$(\lambda - \lambda_0)$$ with coefficients in $$\mathcal{B}(\mathbf{H})$$.
> 2. For $$\lvert \lambda \rvert > \|A\|$$, $$\lambda$$ is in the resolvent set of $$A$$, and
>
>    $$
>        (A - \lambda\mathbf{1})^{-1} = -\sum_{m=0}^\infty \frac{A^m}{\lambda^{m+1}},
>    $$
>
>    convergent in operator norm.

**Proof**
**Part 2.** By [**Proposition** *(hall-7.5)*](#prpstn:hall-7.5), $$\lvert \lambda \rvert>\|A\|$$ implies $$\lambda$$ is in the resolvent set. For such $$\lambda$$, $$A - \lambda\mathbf{1} = -\lambda(\mathbf{1} - A/\lambda)$$ with $$\|A/\lambda\| < 1$$, so by the geometric series lemma [**Lemma** *(hall-7.6)*](#lmm:hall-7.6), $$\mathbf{1} - A/\lambda$$ is invertible with $$(\mathbf{1}-A/\lambda)^{-1} = \sum_{m=0}^\infty (A/\lambda)^m$$, operator-norm convergent; hence $$(A-\lambda\mathbf{1})^{-1} = -\frac{1}{\lambda}\sum_{m=0}^\infty (A/\lambda)^m = -\sum_{m=0}^\infty A^m/\lambda^{m+1}$$.

**Part 1.** Openness of the resolvent set, and the local power series representation, both follow from the same algebraic factorization used to prove [**Proposition** *(hall-7.5)*](#prpstn:hall-7.5) itself: for $$\lambda_0$$ in the resolvent set of $$A$$ and $$\lambda$$ with $$\lvert \lambda-\lambda_0 \rvert < 1/\|(A-\lambda_0\mathbf{1})^{-1}\|$$, writing $$A - \lambda\mathbf{1} = (A-\lambda_0\mathbf{1})\big(\mathbf{1} - (\lambda-\lambda_0)(A-\lambda_0\mathbf{1})^{-1}\big)$$ and applying [**Lemma** *(hall-7.6)*](#lmm:hall-7.6) to the second factor (whose norm is less than $$1$$ by the bound on $$\lvert \lambda-\lambda_0 \rvert$$) shows $$\lambda$$ is again in the resolvent set — so the resolvent set is open — with

$$
    (A-\lambda\mathbf{1})^{-1} = \left( \sum_{m=0}^\infty (\lambda-\lambda_0)^m \big((A-\lambda_0\mathbf{1})^{-1}\big)^m \right)(A-\lambda_0\mathbf{1})^{-1},
$$

an operator-norm-convergent power series in $$(\lambda-\lambda_0)$$ with $$\mathcal{B}(\mathbf{H})$$ coefficients.$$\blacksquare$$



Another proposition we will have need of is

> **Proposition** *(The Orthogonal Complement of the Range is the Kernel of the Adjoint)*
<a name="prpstn:hall-7.3"></a>
<!--  \uses{def:orthogonal-complement} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:adjoint-bounded} -->
> For any $$A \in \mathcal{B}(\mathbf{H})$$, we have
>
> $$
>     \left( \text{Range}(A) \right)^\perp = \text{Ker}(A^*)
> $$
>
> where $$\text{Ker}(A^*)$$ is the kernel of $$A^*$$, $$\text{Range}(A)$$ is the range of $$A$$, and $$\left( \text{Range}(A) \right)^\perp \equiv \{ \psi \in \mathbf{H} : \left< \psi, A\phi \right> = 0 \text{ for all } \phi \in \mathbf{H} \}$$.

**Proof**
Assume that $$\psi \in \left( \text{Range}(A) \right)^\perp$$. Hence, for all $$\phi \in \mathbf{H}$$

$$
\begin{align}
    0 &= \left< \psi, A\phi \right> \\
      &= \left< A^*\psi, \phi \right>.
\end{align}
$$

As this is true for all $$\phi \in \mathbf{H}$$, it implies that $$A^*\psi = 0$$ and thus $$\psi \in \text{Ker}(A^*)$$. Hence, we have proven that $$\left( \text{Range}(A) \right)^\perp \subseteq \text{Ker}(A^*)$$.

Assume now that $$\psi \in \text{Ker}(A^*)$$. Hence, $$A^*\psi = 0$$. Thus for all $$\phi \in \mathbf{H}$$

$$
\begin{align}
    0 &= \left< A^*\psi, \phi \right>  \\
      &= \left< \psi, A\phi \right>.
\end{align}
$$

As this is true for all $$\phi \in \mathbf{H}$$, it implies that $$\psi \in \left( \text{Range}(A) \right)^\perp$$. Hence, we have proven that $$\text{Ker}(A^*) \subseteq \left( \text{Range}(A) \right)^\perp$$.

As we have proven that $$\left( \text{Range}(A) \right)^\perp \subseteq \text{Ker}(A^*)$$ and that $$\text{Ker}(A^*) \subseteq \left( \text{Range}(A) \right)^\perp$$ it follows that

$$
    \left( \text{Range}(A) \right)^\perp = \text{Ker}(A^*),
$$

which is the desired result.$$\blacksquare$$

Another result we will require is

> **Lemma** *(The $$b^2$$ Inequality for a Self-Adjoint Operator)*
<a name="lmm:hall-7.8"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then for all $$a,b \in \mathbb{R}$$ and associated $$\lambda \equiv a + ib$$ in $$\mathbb{C}$$, we have
>
> $$
>     \left< (A - \lambda \mathbf{1}) \psi, (A - \lambda \mathbf{1}) \psi \right> \ge b^2 \left< \psi, \psi \right>
> $$
>
> for all $$\psi \in \mathbf{H}$$.

**Proof**
The definition of $$\lambda$$ in terms of $$a,b \in \mathbb{R}$$ along with the definition of an inner product imply that for any $$\psi \in \mathbf{H}$$

$$
\begin{align}
    &\left< (A - \lambda \mathbf{1}) \psi, (A - \lambda \mathbf{1}) \psi \right> \\
    &= \left< (A - (a + ib) \mathbf{1}) \psi, (A - (a + ib) \mathbf{1}) \psi \right> \\
    &= \left< (A - a\mathbf{1}) \psi, (A - a\mathbf{1}) \psi \right> + ib \left< \psi, (A - a\mathbf{1}) \psi \right> - ib \left< (A - a\mathbf{1}) \psi, \psi \right> + b^2 \left< \psi, \psi \right>.
\end{align}
$$

Now by hypothesis $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint and $$a \in \mathbb{R}$$, hence $$(A - a\mathbf{1})$$ is self-adjoint. Thus

$$
    \left< \psi, (A - a\mathbf{1}) \psi \right> = \left< (A - a\mathbf{1}) \psi, \psi \right>.
$$

Thus the second and third summands of the righthand side of our previous equation cancel leaving us with

$$
    \left< (A - \lambda \mathbf{1}) \psi, (A - \lambda \mathbf{1}) \psi \right> = \left< (A - a\mathbf{1}) \psi, (A - a\mathbf{1}) \psi \right> + b^2 \left< \psi, \psi \right>.
$$

The definition of inner product implies

$$
    0 \le \left< (A - a\mathbf{1}) \psi, (A - a\mathbf{1}) \psi \right>.
$$

Hence, the previous equation implies

$$
    \left< (A - \lambda \mathbf{1}) \psi, (A - \lambda \mathbf{1}) \psi \right> \ge b^2 \left< \psi, \psi \right>,
$$

which is the desired result.$$\blacksquare$$

The next proposition uses the following elementary fact, which we state first.

> **Proposition** *(Bounded Operators are Continuous)*
<a name="prpstn:bounded-operators-are-continuous"></a>
> A linear operator between normed spaces is bounded if and only if it is continuous.

Now we move onto the result

> **Proposition** *(The Spectrum of a Self-Adjoint Operator is Real)*
<a name="prpstn:hall-7.7"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:orthogonal-complement} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-7.8} -->
<!--  \uses{prpstn:hall-7.3} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$.
>
> Hall's Proposition 7.7 pairs this with a second clause characterising membership of the spectrum by the existence of almost-eigenvectors; that clause is not needed in this post and is omitted here. Its analogue for normal operators is proved in the sequel.

**Proof**
A statement obviously equivalent to that of this proposition is the following: For $$a,b \in \mathbb{R}$$ and $$\lambda \equiv a + ib$$ it follows that if $$b \neq 0$$, then $$\lambda$$ is in the resolvent set of $$A$$. We will prove this equivalent statement.

Now the [**Lemma**](#lmm:hall-7.8) we just proved implies that

$$
    \left< (A - \lambda \mathbf{1}) \psi, (A - \lambda \mathbf{1}) \psi \right> \ge b^2 \left< \psi, \psi \right>
$$

for arbitrary $$\psi \in \mathbf{H}$$. By hypothesis $$b \neq 0$$; this along with the previous inequality and the inner product definition imply that if $$\psi \neq 0$$, then $$(A - \lambda \mathbf{1}) \psi \ne 0$$. In other words $$(A - \lambda \mathbf{1})$$ is one-to-one.

As $$\overline{\lambda}$$ also has a non-zero imaginary part the previous argument also applies to $$(A - \overline{\lambda} \mathbf{1})$$ and thus $$(A - \overline{\lambda} \mathbf{1})$$ is also one-to-one.

Recall that as a result of the [**Proposition**](#prpstn:hall-7.3) we just proved we have

$$
\begin{align}
    \left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp &= \text{Ker}((A - \lambda \mathbf{1})^*) \\
    \                                                         &= \text{Ker}(A - \overline{\lambda} \mathbf{1}),
\end{align}
$$

where the second equality follows from the hypothesis that $$A$$ is self-adjoint. As $$(A - \overline{\lambda} \mathbf{1})$$ is one-to-one, $$\text{Ker}(A - \overline{\lambda} \mathbf{1})$$ consists of the zero vector $$\psi = 0$$. Hence, the previous equation implies $$\left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp$$ consists of the zero vector. This in turn implies that $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$.

Next we will prove that $$\text{Range}(A - \lambda \mathbf{1})$$ is not only dense in $$\mathbf{H}$$ but is in fact all of $$\mathbf{H}$$.

Consider any $$\phi \in \mathbf{H}$$. As $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$, there exists a sequence $$\{ \phi_i \equiv (A - \lambda \mathbf{1}) \psi_i \}_{i \in \mathbb{N}}$$ in $$\text{Range}(A - \lambda \mathbf{1})$$ such that $$\{ \phi_i \}_{i \in \mathbb{N}}$$ converges to $$\phi$$.

The [**Lemma**](#lmm:hall-7.8) we just proved implies that for any natural numbers $$i$$ and $$j$$ we have

$$
    \left< (A - \lambda \mathbf{1}) (\psi_j - \psi_i), (A - \lambda \mathbf{1}) (\psi_j - \psi_i) \right> \ge b^2 \left< (\psi_j - \psi_i), (\psi_j - \psi_i) \right>.
$$

As a result of the fact that $$\{ \phi_i \}_{i \in \mathbb{N}}$$ converges to $$\phi$$ it follows that $$\{ \phi_i \}_{i \in \mathbb{N}}$$ is a Cauchy sequence. As $$\{ \phi_i \}_{i \in \mathbb{N}}$$ is a Cauchy sequence $$\{ (A - \lambda \mathbf{1}) \psi_i \}_{i \in \mathbb{N}}$$ is a Cauchy sequence.

Hence, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i,j \ge N$$ one has

$$
    \| (A - \lambda \mathbf{1}) \psi_j - (A - \lambda \mathbf{1}) \psi_i \| < \epsilon \lvert b \rvert.
$$

As a result of the previous inequality involving $$b^2$$ this, along with the definition of the norm on $$\mathbf{H}$$, implies that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i,j \ge N$$ one has


$$
    \epsilon^2 b^2 > \| (A - \lambda \mathbf{1}) (\psi_j - \psi_i) \|^2 \ge b^2 \|\psi_j - \psi_i\|^2.
$$

This in turn implies that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i,j \ge N$$ one has

$$
    \|\psi_j - \psi_i\| < \epsilon.
$$

In other words $$\{ \psi_i \}_{i \in \mathbb{N}}$$ is a Cauchy sequence. Furthermore, as $$\{ \psi_i \}_{i \in \mathbb{N}}$$ is a Cauchy sequence and $$\mathbf{H}$$ is complete, there exists a $$\psi \in \mathbf{H}$$ such that $$\{ \psi_i \}_{i \in \mathbb{N}}$$ converges to $$\psi$$.

Now as $$A \in \mathcal{B}(\mathbf{H})$$ it is a bounded linear operator from the normed space $$\mathbf{H}$$ to the normed space $$\mathbf{H}$$. Thus, as a result of the standard proposition [**Bounded Operators are Continuous**](#prpstn:bounded-operators-are-continuous), $$A$$ is continuous.

As $$A$$ is continuous our definitions imply

$$
    (A - \lambda \mathbf{1}) \psi = \lim\limits_{i \rightarrow \infty} (A - \lambda \mathbf{1}) \psi_i = \lim\limits_{i \rightarrow \infty} \phi_i = \phi.
$$

As $$\phi \in \mathbf{H}$$ was arbitrary, this implies that an arbitrary $$\phi \in \mathbf{H}$$ is in $$\text{Range}(A - \lambda \mathbf{1})$$, and thus $$\text{Range}(A - \lambda \mathbf{1})$$ is all of $$\mathbf{H}$$, the desired result.

Hence, we have proven that $$(A - \lambda \mathbf{1})$$ is one-to-one and onto. There is one remaining result required to show that $$\lambda$$ is in the resolvent set of $$A$$. It remains to prove that $$(A - \lambda \mathbf{1})^{-1}$$ is bounded.

As we just proved, for an arbitrary $$\phi \in \mathbf{H}$$ there exists a $$\psi \in \mathbf{H}$$ such that $$(A - \lambda \mathbf{1}) \psi = \phi$$. In this case [**Lemma**](#lmm:hall-7.8) and the definition of norm on $$\mathbf{H}$$ imply

$$
\begin{align}
    b^2 \| (A - \lambda \mathbf{1})^{-1}\phi \|^2 &\le \| (A - \lambda \mathbf{1}) (A - \lambda \mathbf{1})^{-1}\phi \|^2 \\
                                                &=   \| \phi \|^2 \\
                                                &<   \infty,
\end{align}
$$

which proves that $$(A - \lambda \mathbf{1})^{-1}$$ is bounded.

Hence, we have proven that for any $$a,b \in \mathbb{R}$$ with $$b \neq 0$$ and $$\lambda$$ defined by $$\lambda \equiv a  + ib$$, it follows that $$\lambda$$ is in the resolvent set of a self-adjoint $$A$$. This is then equivalent to the statement that if $$A$$ is self-adjoint, then the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$.$$\blacksquare$$

Before proceeding, let us consolidate several structural facts about the spectrum $$\sigma(A)$$ of a self-adjoint operator $$A$$ into a single lemma. These facts are used repeatedly throughout the remainder of this post---in particular as the standing hypothesis "$$\sigma(A)$$ is a compact metric measurable space" required by several later results---and collecting them here allows us to cite them once rather than re-deriving them at each point of use.

However, in consolidating these facts we will have need of the [**Heine–Borel Theorem**](#thrm:heine–borel-theorem) which states

> **Theorem** *(Heine–Borel Theorem)*
<a name="thrm:heine–borel-theorem"></a>
> For any positive, natural number $$n$$, any subset of $$\mathbb{C}^n$$ is compact if and only if it is closed and bounded.

with that stated let us begin the consolidation.

> **Lemma** *(The Spectrum is a Compact Metric Measurable Space)*
<a name="lmm:spectrum-is-compact-metric-measurable"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{conv:nonzero-hilbert-space} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{thrm:heine–borel-theorem} -->
> Suppose $$\mathbf{H} \ne \{0\}$$ and let $$A \in \mathcal{B}(\mathbf{H})$$. Then the spectrum $$\sigma(A)$$ of $$A$$ satisfies the following.
>
> 1. $$\sigma(A)$$ is a non-empty subset of $$\mathbb{C}$$.
> 2. $$\sigma(A)$$ is compact.
> 3. $$\sigma(A)$$ is a metric space under the metric $$d(z_1, z_2) \equiv \lvert z_1 - z_2 \rvert$$ inherited from $$\mathbb{C}$$.
> 4. $$\sigma(A)$$ is a measurable space when equipped with its Borel $$\sigma$$-algebra, i.e. the smallest $$\sigma$$-algebra containing the open sets of $$\sigma(A)$$ in the topology induced by the metric of (3).
>
> No self-adjointness is assumed: parts (1)–(4) hold for every $$A \in \mathcal{B}(\mathbf{H})$$, and in particular $$\sigma(A)$$ need not be contained in $$\mathbb{R}$$. When $$A$$ *is* self-adjoint one has in addition $$\sigma(A) \subset \mathbb{R}$$, which is [**Proposition** *(hall-7.7)*](#prpstn:hall-7.7) and is stated separately there, since the topological content above does not depend on it.
>
> In particular, $$\sigma(A)$$ is a non-empty, compact metric measurable space. Throughout the remainder of this post, whenever $$\sigma(A)$$ is described as measurable, or a subset of $$\sigma(A)$$ is described as measurable, it is with respect to this Borel $$\sigma$$-algebra. Consequently, on $$\sigma(A)$$ the terms "measurable" and "Borel-measurable" are synonymous, both for sets and for functions.

**Proof**
**Part 1:** Part 1 of [**Proposition**](#prpstn:hall-7.5) implies that $$\sigma(A)$$ is non-empty. This is the desired **Part 1** result.

**Part 2:** Part 1 of [**Proposition**](#prpstn:hall-7.5) implies that $$\sigma(A)$$ is a closed and bounded subset of $$\mathbb{C}$$. The [**Heine–Borel Theorem**](#thrm:heine–borel-theorem) then implies that $$\sigma(A)$$ is compact, the desired **Part 2** result.

**Part 3:** As the norm $$\lvert \cdot \rvert$$ on $$\mathbb{C}$$ defines a metric

$$
  d(z_1, z_2) \equiv \lvert z_1 - z_2 \rvert
$$

on $$\mathbb{C}$$, and as the restriction of a metric to a subset is again a metric on that subset, the subset $$\sigma(A)$$ of $$\mathbb{C}$$ is a metric space by way of this inherited metric. This is the desired **Part 3** result.

**Part 4:** By **Part 3** the set $$\sigma(A)$$ carries a metric, and hence a topology generated by the open balls of that metric. The Borel $$\sigma$$-algebra of $$\sigma(A)$$ is by definition the smallest $$\sigma$$-algebra containing the open sets of this topology, and a set equipped with a $$\sigma$$-algebra is by definition a measurable space. Hence $$\sigma(A)$$, equipped with its Borel $$\sigma$$-algebra, is a measurable space, the desired **Part 4** result.

Combining **Part 1** through **Part 4**, $$\sigma(A)$$ is a non-empty, compact metric measurable space, the desired result.$$\blacksquare$$


> **Definition** *(Spectral Radius)*
<a name="def:spectral-radius"></a>
<!--  \uses{conv:nonzero-hilbert-space} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{prpstn:hall-7.5} -->
> Suppose $$\mathbf{H} \ne \{0\}$$. For any $$A \in \mathcal{B}(\mathbf{H})$$ the *spectral radius* $$R(A)$$ of $$A$$ is defined by
>
> $$
>     R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert \lambda \rvert.
> $$
>
> Note that as a result of [**Proposition**](#prpstn:hall-7.5), $$\sigma(A)$$ is a closed, bounded, and non-empty subset $$\mathbb{C}$$. Hence, $$R(A)$$ is a finite real number.

The first property that one can easily ascertain of the spectral radius is the following corollary:

> **Corollary** *(The Spectral Radius is at Most the Operator Norm)*
<a name="crllr:crllr-1"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:spectral-radius} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ then the spectral radius $$R(A)$$ of $$A$$ is less than or equal to the operator norm $$\|A\|$$ of $$A$$,
>
> $$
>     R(A) \le \|A\|
> $$

**Proof**
[**Proposition**](#prpstn:hall-7.5) Part 2 implies that if $$\lvert \lambda \rvert > \|A\|$$, then $$\lambda$$ is in the resolvent set of $$A$$. The contrapositive of this statement is: if $$\lambda$$ is not in the resolvent set of $$A$$, then $$\lvert \lambda \rvert \le \|A\|$$.

By definition the spectrum $$\sigma(A)$$ of $$A$$ is the complement of the resolvent set of $$A$$ in $$\mathbb{C}$$. Hence, our contrapositive is equivalent to the statement: if $$\lambda$$ is in the spectrum $$\sigma(A)$$ of $$A$$, then $$\lvert \lambda \rvert \le \|A\|$$.

Hence, for all $$\lambda \in \sigma(A)$$ it follows that $$\lvert \lambda \rvert \le \|A\|$$. This then implies

$$
    R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert \lambda \rvert \le \|A\|,
$$

the desired result.$$\blacksquare$$

The next "utility" proposition we will require details properties of the operator norm on $$\mathcal{B}(\mathbf{H})$$.

> **Proposition** *(The Adjoint Preserves the Operator Norm)*
<a name="prpstn:hall-7.2"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-a.43} -->
<!--  \uses{lmm:lemma-1} -->
<!--  \uses{lmm:lemma-2} -->
> For any $$A \in \mathcal{B}(\mathbf{H})$$ the operator norm satisfies
>
> $$
>     \|A\| = \|A^*\|
> $$
>
> along with
>
> $$
>     \|A^*A\| = \|A\|^2.
> $$
>
> In particular if $$A$$ is self-adjoint, it satisfies $$\|A^2\| = \|A\|^2$$.

**Proof**
Let us begin the proof of the first result $$\|A\| = \|A^*\|$$ by noting that as a result of our previous [**Lemma**](#lmm:lemma-1) we can write the operator norm of any $$A \in \mathcal{B}(\mathbf{H})$$ as

$$
    \|A\| = \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< \chi, A \psi \right> \rvert.
$$ 

This also allows us to write the operator norm of $$A^*$$ as

$$
\begin{align}
    \|A^*\| &= \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< \chi, A^*\psi \right> \rvert \\
            &= \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< A\chi, \psi \right> \rvert \\
            &= \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \overline{\left< \psi, A\chi \right>} \rvert \\
            &= \sup\limits_{\|\chi\| = \|\psi\| = 1} \lvert \left< \psi, A\chi \right> \rvert \\
            &= \|A\|,
\end{align}
$$

where we have used the definition of $$A^*$$ as well as the definition of norm and inner product. This gives us

$$
    \|A^*\| = \|A\|,
$$

the first desired result.

Now let us begin the proof of the second desired result $$\|A^*A\| = \|A\|^2$$ by recalling that as a result of [**Lemma** *(Bounded Operator Product is Submultiplicative)*](#lmm:lemma-2) operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative,

$$
    \|AB\| \le \|A\| \, \|B\|
$$

for any $$A,B \in \mathcal{B}(\mathbf{H})$$. Hence, for an arbitrary $$A \in \mathcal{B}(\mathbf{H})$$ we have

$$
    \|A^*A\| \le \|A^*\| \, \|A\| = \|A\|^2,
$$

where the equality uses the first result $$\|A^*\| = \|A\|$$ proved in this proposition.

Using the alternative means of expressing the operator norm derived in [**Lemma**](#lmm:lemma-1) one has

$$
\begin{align}
    \|A^*A\| &= \sup\limits_{\|\phi\| = \|\psi\| = 1} \left\lvert \left< \phi, A^*A\psi \right> \right\rvert \\
             &= \sup\limits_{\|\phi\| = \|\psi\| = 1} \left\lvert \left< A\phi, A\psi \right> \right\rvert \\
             &\ge \sup\limits_{\|\psi\| = 1} \left\lvert \left< A\psi, A\psi \right> \right\rvert \\
             &= \sup\limits_{\|\psi\| = 1} \left\| A\psi \right\|^2 \\
             &= \|A\|^2,
\end{align}
$$

where we used the definition of $$A^*$$, standard supremum properties, the norm definition, and the operator norm definition. So in summary this implies

$$
    \|A^*A\| \ge \|A\|^2.
$$

However, we have already proven

$$
    \|A^*A\| \le \|A\|^2.
$$

Together these imply

$$
    \|A^*A\| = \|A\|^2,
$$

the final desired result.$$\blacksquare$$

As a consequence of the first result of the [**Proposition**](#prpstn:hall-7.2) just proven, we record the following continuity property of the adjoint, which we will have need of later.

> **Proposition** *(Continuity of the Adjoint)*
<a name="prpstn:continuity-of-the-adjoint"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-7.2} -->
> Let $$\mathbf{H}$$ be a Hilbert space and let $$\{ B_n \}_{n \in \mathbb{N}}$$ be a sequence in $$\mathcal{B}(\mathbf{H})$$ converging in the operator norm to $$B \in \mathcal{B}(\mathbf{H})$$. Then $$\{ B_n^* \}_{n \in \mathbb{N}}$$ converges in the operator norm to $$B^*$$, i.e.
>
> $$
>     B^* = \lim\limits_{n \rightarrow \infty} B_n^*.
> $$

**Proof**
Let us first prove that the adjoint is additive, i.e. that $$(C - D)^* = C^* - D^*$$ for any $$C, D \in \mathcal{B}(\mathbf{H})$$. For any $$\chi, \psi \in \mathbf{H}$$ one has

$$
\begin{align}
    \left< \chi, (C - D)^* \psi \right> &= \left< (C - D)\chi, \psi \right> \\
                                        &= \left< C\chi, \psi \right> - \left< D\chi, \psi \right> \\
                                        &= \left< \chi, C^* \psi \right> - \left< \chi, D^* \psi \right> \\
                                        &= \left< \chi, (C^* - D^*) \psi \right>,
\end{align}
$$

where the first and third lines follow from the definition of the adjoint and the second and fourth from the additivity of the inner product. As this holds for all $$\chi \in \mathbf{H}$$, it follows that $$(C - D)^* \psi = (C^* - D^*)\psi$$ for all $$\psi \in \mathbf{H}$$, and hence $$(C - D)^* = C^* - D^*$$.

Now, as a result of the first result of [**Proposition**](#prpstn:hall-7.2), the operator norm satisfies $$\|C\| = \|C^*\|$$ for any $$C \in \mathcal{B}(\mathbf{H})$$. Combining this with the additivity just proven gives, for any $$n \in \mathbb{N}$$,

$$
    \left\| B_n^* - B^* \right\| = \left\| (B_n - B)^* \right\| = \left\| B_n - B \right\|.
$$

The proof of the next lemma draws on four standard results — one about series, two from complex and functional analysis, and the Principle of Uniform Boundedness — which we state first.

> **Lemma** *(Nth-Term Test)*
<a name="lmm:nth-term-test"></a>
> Let $$\{a_i\}_{i \in \mathbb{N}}$$ be a sequence in a normed vector space. If $$\left\| a_i \right\|$$ does **not** converge to $$0$$ — either because the limit exists and is non-zero, or because it fails to exist — then the series $$\sum_i a_i$$ does not converge.
>
> Equivalently, in contrapositive form: if $$\sum_i a_i$$ converges then $$\left\| a_i \right\| \rightarrow 0$$.

> **Theorem** *(Laurent's Theorem)*
<a name="thrm:laurents-theorem"></a>
> Any function holomorphic on an open annulus in $$\mathbb{C}$$ can be expanded uniquely as a Laurent series on that open annulus.

> **Theorem** *(Theorem on Completeness of the Dual)*
<a name="thrm:theorem-on-completeness-of-the-dual"></a>
<!--  \uses{def:adjoint-bounded} -->
> If $$V$$ is a Banach space, then its dual $$V^*$$ is also a Banach space.

> **Theorem** *(Principle of Uniform Boundedness)*
<a name="thrm:hall-a.40"></a>
> Suppose $$\{ T_m \}$$ is any family of bounded linear maps from a Banach space $$V_1$$ to a normed space $$V_2$$. Suppose that for each $$\xi \in V_1$$, there is a real constant $$C_\xi$$ such that
> 
> $$
>     \| T_m \xi \| \le C_\xi
> $$
> 
> for all $$m$$. Then there exists a real constant $$C$$ such that for all $$m$$
> 
> $$
>     \|T_m\| \le C,
> $$
> 
> where $$\|T_m\|$$ is the operator norm of $$T_m$$.

As $$B_n \rightarrow B$$ in the operator norm the righthand side tends to $$0$$, and hence $$B_n^* \rightarrow B^*$$ in the operator norm, the desired result.$$\blacksquare$$

> **Lemma** *(The Norm of a Self-Adjoint Operator is its Spectral Radius)*
<a name="lmm:hall-8.1"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:resolvent-holomorphy-and-neumann-series} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:spectral-radius} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:nth-term-test} -->
<!--  \uses{prpstn:hall-7.2} -->
<!--  \uses{thrm:analytic-equivalence-theorem} -->
<!--  \uses{thrm:laurents-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{thrm:theorem-on-completeness-of-the-dual} -->
<!--  \uses{thrm:hall-a.40} -->
<!--  \uses{crllr:crllr-1} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then the operator norm $$\|A\|$$ of $$A$$ is equal to the spectral radius $$R(A)$$ of $$A$$,
>
> $$
>     \|A\| = R(A)
> $$

**Proof**
Before diving in to the details, let's present an outline of the proof. At core, the proof consists of 4 steps:

1. Prove that if $$\lvert \lambda \rvert > \|A\|$$, then $$(A - \lambda \mathbf{1})^{-1}$$ can be expressed as a series convergent in the operator norm topology.
2. Prove that if $$\lvert \lambda \rvert \le \|A\|$$, then this series doesn't converge in the operator norm topology.
3. Prove that if $$\lvert \lambda \rvert > R(A)$$, then this series converges in the operator norm topology.
4. Conclude that a contradiction arises if $$R(A) < \|A\|$$, and thus $$R(A) = \|A\|$$.

Let us first (1) prove that if $$\lvert \lambda \rvert > \|A\|$$, then $$(A - \lambda \mathbf{1})^{-1}$$ can be expressed as a series convergent in the operator norm topology.

This first result is Part 2 of [**Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*](#prpstn:resolvent-holomorphy-and-neumann-series), which gives that for $$\lvert \lambda \rvert > \|A\|$$, the following series is convergent in the operator norm topology

$$
    - \frac{1}{\lambda} \left( \mathbf{1} + \frac{A}{\lambda} + \frac{A^2}{\lambda^2} + \frac{A^3}{\lambda^3} + \cdots \right) = - \sum_{m = 0}^\infty \frac{A^m}{\lambda^{m + 1}},
$$

and in fact is equivalent to $$(A - \lambda \mathbf{1})^{-1}$$

$$
    (A - \lambda \mathbf{1})^{-1} = - \sum_{m = 0}^\infty \frac{A^m}{\lambda^{m + 1}}.
$$

This is the first desired result.

Next let us (2) prove that if $$\lvert \lambda \rvert \le \|A\|$$, then this series doesn't converge in the operator norm topology.

The first step in this proof is to derive a useful identity expressing $$\|A^{2^n}\|$$ in terms of $$\|A\|^{2^n}$$. For self-adjoint $$A$$ [**Proposition**](#prpstn:hall-7.2) states

$$
    \|A^2\| = \|A\|^2.
$$

For natural number $$n$$ iterating this identity gives

$$
    \|A^{2^n}\| = \|A\|^{2^n}.
$$

This identity will be of use when we prove our series doesn't converge in the operator norm topology. In particular we will prove this using the [**Nth-Term Test**](#lmm:nth-term-test).

Consider the limit

$$
\begin{align}
    \lim\limits_{n \rightarrow \infty} \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\|
    &= \lim\limits_{n \rightarrow \infty} \left\lvert \frac{1}{\lambda^{2^n + 1}} \right\rvert \left\| A^{2^n} \right\| \\
    &= \lim\limits_{n \rightarrow \infty} \left\lvert \frac{1}{\lambda^{2^n + 1}} \right\rvert \left\| A \right\|^{2^n}  \\
    &= \lim\limits_{n \rightarrow \infty} \frac{1}{\lvert \lambda \rvert}  \left( \frac{\left\| A \right\|}{\left\lvert \lambda \right\rvert} \right)^{2^n} \\
    &= \frac{1}{\lvert \lambda \rvert} \lim\limits_{n \rightarrow \infty} \left( \frac{\left\| A \right\|}{\left\lvert \lambda \right\rvert} \right)^{2^n}.
\end{align}
$$

By hypothesis $$\lvert \lambda \rvert \le \|A\|$$. Hence

$$
    1 \le \frac{\left\| A \right\|}{\left\lvert \lambda \right\rvert}.
$$

This implies that our derivation continues as follows

$$
    \lim\limits_{n \rightarrow \infty} \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\|
    = \frac{1}{\lvert \lambda \rvert} \lim\limits_{n \rightarrow \infty} \left( \frac{\left\| A \right\|}{\left\lvert \lambda \right\rvert} \right)^{2^n}
    \neq 0.
$$

Hence, the [**Nth-Term Test**](#lmm:nth-term-test) implies that the series does not converge.

With that we have proven the desired result: if $$\lvert \lambda \rvert \le \|A\|$$, then our series doesn't converge in the operator norm topology.

Now let us (3) prove that if $$\lvert \lambda \rvert > R(A)$$, then this series converges in the operator norm topology.

Recall from Part 1 of [**Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*](#prpstn:resolvent-holomorphy-and-neumann-series) that if $$\lambda_0$$ is in the resolvent set of $$A$$ and $$\lambda \in \mathbb{C}$$ satisfies

$$
    \lvert \lambda - \lambda_0 \rvert < \frac{1}{\|(A - \lambda_0 \mathbf{1})^{-1}\|}
$$

then $$(A - \lambda \mathbf{1})^{-1}$$ exists in $$\mathcal{B}(\mathbf{H})$$ and is expressible as the following locally convergent power series in $$ (\lambda - \lambda_0)$$

$$
    (A - \lambda \mathbf{1})^{-1} = \left( \sum_{m \in \mathbb{N}} (\lambda - \lambda_0)^m ((A - \lambda_0 \mathbf{1})^{-1})^m \right) (A - \lambda_0 \mathbf{1})^{-1},
$$

that converges in the operator norm topology. Furthermore, as $$(A - \lambda \mathbf{1})^{-1}$$ exists in $$\mathcal{B}(\mathbf{H})$$ this implies that $$\lambda$$ is also in the resolvent set of $$A$$.

Consider now any element $$\xi$$ in the dual space of $$\mathcal{B}(\mathbf{H})$$. Using $$\xi$$ and the above convergent series, the map

$$
    \lambda \longmapsto \xi (A - \lambda \mathbf{1})^{-1}
$$

can be expressed as a locally convergent power series with coefficients in $$\mathbb{C}$$. Hence, it is an analytic function on the resolvent set of $$A$$, which is open by Part 1 of [**Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*](#prpstn:resolvent-holomorphy-and-neumann-series). Hence, the [**Analytic Equivalence Theorem**](#thrm:analytic-equivalence-theorem) implies that this function is holomorphic on the resolvent set of $$A$$.

Now, as mentioned in [**Definition** *(Spectral Radius)*](#def:spectral-radius), the spectral radius

$$
    R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert \lambda \rvert
$$

of $$A$$ is a finite real number. Explicitly, [**Proposition**](#prpstn:hall-7.5) implies that $$\sigma(A)$$ is a closed, bounded, and non-empty subset $$\mathbb{C}$$. Hence, $$R(A)$$ is a finite real number.

The spectrum $$\sigma(A)$$ of $$A$$ is defined as the complement of the resolvent set of $$A$$ in $$\mathbb{C}$$. Hence, all $$\lambda \in \mathbb{C}$$ such that $$\lvert \lambda \rvert > R(A)$$ are in the resolvent set of $$A$$. Thus, the function

$$
    \lambda \longmapsto \xi (A - \lambda \mathbf{1})^{-1}
$$

is holomorphic on the (unbounded) open annulus $$R(A) < \lvert \lambda \rvert$$.

Now recall [**Laurent's Theorem**](#thrm:laurents-theorem) stated above: a function holomorphic on an annulus admits there a Laurent expansion, convergent on that annulus, whose coefficients are uniquely determined.

Hence, the function

$$
    \lambda \longmapsto \xi (A - \lambda \mathbf{1})^{-1}
$$

can be expanded uniquely into a convergent Laurent series on the (unbounded) open annulus $$R(A) < \lvert \lambda \rvert$$.

Now in Part 1 of this proof we established that if $$\lvert \lambda \rvert > \|A\|$$, then $$(A - \lambda \mathbf{1})^{-1}$$ can be expressed as the series

$$
    (A - \lambda \mathbf{1})^{-1} = - \sum_{m = 0}^\infty \frac{A^m}{\lambda^{m + 1}}.
$$

that is convergent in the operator norm topology. Acting on this series with $$\xi$$ we obtain the convergent Laurent series

$$
    \lambda \longmapsto \xi  (A - \lambda \mathbf{1})^{-1} = - \sum_{m = 0}^\infty \frac{\xi A^m}{\lambda^{m + 1}},
$$

on the (unbounded) open annulus $$\lvert \lambda \rvert > \|A\|$$.

Hence, we have two convergent Laurent series expansions of $$(A - \lambda \mathbf{1})^{-1}$$ on the (unbounded) open annulus $$\max(R(A), \|A\|) < \lvert \lambda \rvert$$. The first resulting from the initial application of [**Laurent's Theorem**](#thrm:laurents-theorem) and the second from the result from Part 1 of this proof. The uniqueness of [**Laurent's Theorem**](#thrm:laurents-theorem) implies that these convergent Laurent series expansions must be identical. Hence, we can write the convergent Laurent series expansion in both cases as

$$
    \lambda \longmapsto - \sum_{m = 0}^\infty \frac{\xi A^m}{\lambda^{m + 1}},
$$

which converges for $$R(A) < \lvert \lambda \rvert$$. This completes the proof of Part 3.

Next let us (4) conclude that a contradiction arises if $$R(A) < \|A\|$$, and thus $$R(A) = \|A\|$$.

Recall we already established in [**Corollary**](#crllr:crllr-1) that $$R(A) \le \|A\|$$. We will now establish that $$R(A) = \|A\|$$ using proof by contradiction.

Let us for the moment assume that $$R(A) < \|A\|$$. Then it is possible to select a $$\lambda$$ such that $$R(A) < \lvert \lambda \rvert < \|A\|$$. Let us fix this $$\lambda$$ for the remainder of the proof.

The unique Laurent series from Part 3, evaluated at this fixed $$\lambda$$, converges. This implies that all of its summands are bounded. In other words, for each $$\xi$$ in the dual space of $$\mathcal{B}(\mathbf{H})$$ there exists a $$C_\xi \in \mathbb{R}$$---which may depend on $$\xi$$ and on our now-fixed $$\lambda$$---such that for any natural number $$m$$

$$
    \left\lvert \frac{\xi A^m}{\lambda^{m + 1}} \right\rvert < C_\xi.
$$

Now, as we established in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space), $$\mathcal{B}(\mathbf{H})$$ forms a Banach space under the operator norm. Recalling the [**Theorem on Completeness of the Dual**](#thrm:theorem-on-completeness-of-the-dual) we can conclude that the dual $$\mathcal{B}(\mathbf{H})^*$$ of $$\mathcal{B}(\mathbf{H})$$ is also a Banach space.

As both $$\mathcal{B}(\mathbf{H})$$ and $$\mathcal{B}(\mathbf{H})^*$$ are Banach spaces and we have a set of bounded summands we can apply the [**Principle of Uniform Boundedness**](#thrm:hall-a.40) by identifying $$V_1$$ with $$\mathcal{B}(\mathbf{H})^*$$, $$V_2$$ with $$\mathbb{C}$$, the operators $$\{ T_m \}$$ with the operators

$$
    \left\{ \frac{A^m}{\lambda^{m + 1}} \right\},
$$

evaluated at our fixed $$\lambda$$, and the bounds we derived previously

$$
    \left\lvert \frac{\xi A^m}{\lambda^{m + 1}} \right\rvert < C_\xi
$$

with those in this theorem. Doing so we find that there exists a real number $$C$$---which may depend on our fixed $$\lambda$$---such that for all natural numbers $$m$$

$$
    \left\| \frac{A^m}{\lambda^{m + 1}} \right\| \le C,
$$

where here the operator norm is used.

Now, as one will recall, in Part 2 of this proof we established that for any natural number $$n$$

$$
    \left\| A^{2^n} \right\| = \left\| A \right\|^{2^n}.
$$

Applying this to the bound we just derived, at our fixed $$\lambda$$, gives

$$
    \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\| = \frac{\left\| A^{2^n} \right\|}{\left\lvert \lambda \right\rvert^{2^n + 1}} = \frac{\left\| A \right\|^{2^n} }{\left\lvert \lambda \right\rvert^{2^n + 1}} \le C.
$$

Now, as $$R(A) < \lvert \lambda \rvert < \|A\|$$, we have

$$
    1 < \frac{\|A\|}{\lvert \lambda \rvert}.
$$

Hence, it is possible to select an $$n$$ large enough to violate the above inequality

$$
    \frac{1}{\left\lvert \lambda \right\rvert} \left( \frac{\left\| A \right\|}{\left\lvert \lambda \right\rvert} \right)^{2^n} = \frac{\left\| A \right\|^{2^n} }{\left\lvert \lambda \right\rvert^{2^n + 1}} \le C.
$$

So it can not be the case that $$R(A) < \|A\|$$. As we know $$R(A) \le \|A\|$$, the only option left is $$R(A) = \|A\|$$, the desired result.$$\blacksquare$$

The next step in this **Stage 1: The Continuous Functional Calculus** is to understand how the spectrum $$\sigma(A)$$ of an operator $$A \in \mathcal{B}(\mathbf{H})$$ is related to the spectrum $$\sigma(p(A))$$ of a polynomial $$p(A)$$ in $$A$$. The relation between $$\sigma(A)$$ and $$\sigma(p(A))$$ is "straightforward" and described by the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem).

However, to prove the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) we will first have to prove this utility lemma

> **Lemma** *(A Product with a Non-Invertible Commuting Factor is Non-Invertible)*
<a name="lmm:hall-ex-8.3.1"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
> If $$A,B \in \mathcal{B}(\mathbf{H})$$ commute and $$A$$ is not invertible, then $$AB$$ is not invertible.

**Proof**
We will prove this result using proof by contradiction. We will assume that $$(AB)$$ is invertible, then derive a contradiction.

Assuming $$(AB)$$ is invertible implies that there exists a $$(AB)^{-1}$$ such that

$$
    (AB)(AB)^{-1} = \mathbf{1}.
$$

This implies that

$$
\begin{align}
    \mathbf{1} &= (AB)(AB)^{-1} \\
               &= A(B(AB)^{-1}).
\end{align}
$$

This is simply the statement that $$A$$ has a right inverse $$(B(AB)^{-1})$$.

Similarly, under the assumption that $$(AB)$$ has an inverse, $$(AB)^{-1}$$ exists and satisfies

$$
    (AB)^{-1}(AB) = \mathbf{1}.
$$

As $$A$$ commutes with $$B$$ this implies

$$
\begin{align}
    \mathbf{1} &= (AB)^{-1}(AB) \\
               &= (AB)^{-1}(BA) \\
               &= ((AB)^{-1}B)A.
\end{align}
$$

This is simply the statement that $$A$$ has a left inverse $$((AB)^{-1}B)$$.

Now if we let the right inverse $$(B(AB)^{-1})$$ act on the right of $$((AB)^{-1}B)A = \mathbf{1}$$, we have

$$
    ((AB)^{-1}B)A(B(AB)^{-1}) = (B(AB)^{-1}).
$$

However, $$(B(AB)^{-1})$$ is the right inverse of $$A$$; so

$$
    A(B(AB)^{-1}) = \mathbf{1}.
$$

The last two equations then imply

$$
    ((AB)^{-1}B) = (B(AB)^{-1}).
$$

In other words the left inverse $$((AB)^{-1}B)$$ and the right inverse $$(B(AB)^{-1})$$ agree and there is a single unique inverse of $$A^{-1}$$.

However, by hypothesis $$A$$ is not invertible. Thus our assumption that $$AB$$ is invertible is false, and $$AB$$ is not invertible. This is the desired result.$$\blacksquare$$

The proof of the Spectral Mapping Theorem uses the Fundamental Theorem of Algebra, which we state first.

> **Theorem** *(Fundamental Theorem of Algebra)*
<a name="thrm:fundamental-theorem-of-algebra"></a>
> The field of complex numbers is algebraically closed.

With this lemma complete we may now move on to the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem).

> **Lemma** *(Spectral Mapping Theorem)*
<a name="lmm:spectral-mapping-theorem"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-ex-8.3.1} -->
<!--  \uses{thrm:fundamental-theorem-of-algebra} -->
<!--  \uses{conv:nonzero-hilbert-space} -->
> For all $$A$$ in $$\mathcal{B}(\mathbf{H})$$ and any polynomial $$p(\lambda)$$ of degree $$m$$ on the spectrum $$\sigma(A)$$ of $$A$$
>
> $$
>     p(\lambda) = \alpha_0 + \alpha_1 \lambda + \alpha_2 \lambda^2 + \cdots + \alpha_{m - 1} \lambda^{m - 1} + \alpha_m \lambda^m
> $$
>
> with $$\mathbb{C}$$ valued coefficients $$\alpha_i$$, let us define a map $$p \mapsto p(A)$$ from such polynomials to elements of $$\mathcal{B}(\mathbf{H})$$ by
>
> $$
>     p \longmapsto p(A) \equiv \alpha_0 \mathbf{1} + \alpha_1 A + \alpha_2 A^2 + \cdots + \alpha_{m - 1} A^{m - 1} + \alpha_m A^m.
> $$
>
> Then the spectrum $$\sigma(p(A))$$ of $$p(A)$$ is given by
>
> $$
>     \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}.
> $$
>
> Note that in an abuse of notation this is often written as $$\sigma(p(A)) = p(\sigma(A))$$, despite the fact that $$p(\sigma(A))$$ is ill-defined.


**Proof**
Before getting into the details, let us present an outline of the 4-step proof.

1. Prove that the desired result

   $$
       \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}
   $$

   holds for a constant polynomial $$p(\lambda) = \alpha_0$$.
2. Prove that

   $$
       \{ p(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(p(A))
   $$

   for a generic polynomial $$p$$ of positive degree.
3. Prove that

   $$
       \sigma(p(A)) \subseteq \{ p(\lambda) : \lambda \in \sigma(A) \}
   $$

   for a generic polynomial $$p$$ of positive degree.
4. Conclude that

   $$
       \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}
   $$

   as a result of the proofs of Parts 1-3.

Let us begin by (1) proving that the desired result

$$
    \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

holds for a constant polynomial $$p(\lambda) = \alpha_0$$.

The resolvent set of $$p(A) = \alpha_0 \mathbf{1}$$ is defined as the set of $$\lambda \in \mathbb{C}$$ such that $$\alpha_0 \mathbf{1} - \lambda \mathbf{1}$$ has a bounded inverse in $$\mathcal{B}(\mathbf{H})$$. The resolvent set of $$p(A)$$ in this case is $$\mathbb{C} \setminus \{\alpha_0\}$$. Indeed $$\alpha_0\mathbf{1} - \lambda\mathbf{1} = (\alpha_0 - \lambda)\mathbf{1}$$, so for $$\lambda \ne \alpha_0$$ the operator $$(\alpha_0 - \lambda)^{-1}\mathbf{1}$$ is a bounded two-sided inverse, putting $$\lambda$$ in the resolvent set; while for $$\lambda = \alpha_0$$ the operator is $$0$$, which has no inverse because $$\mathbf{H} \ne \{0\}$$ by the [standing convention](#conv:nonzero-hilbert-space) — there is a non-zero $$\psi$$ with $$0\psi = 0$$, so $$0$$ is not injective. The spectrum $$\sigma(p(A))$$ of $$p(A)$$ is defined as the complement of the resolvent set of $$p(A)$$ in $$\mathbb{C}$$. Hence, $$\sigma(p(A)) = \{ \alpha_0 \}$$.

On the other hand, by definition the spectrum $$\sigma(A)$$ is some subset of $$\mathbb{C}$$. In addition, for any $$\lambda$$ in $$\mathbb{C}$$ we have $$p(\lambda) = \alpha_0$$. Hence,

$$
    \{ p(\lambda) : \lambda \in \sigma(A) \} = \{ \alpha_0 : \lambda \in \sigma(A) \} = \{ \alpha_0 \}.
$$

Thus we have proven that if $$p$$ is a constant polynomial $$p(\lambda) = \alpha_0$$, then

$$
    \sigma(p(A)) = \{ \alpha_0 \} = \{ p(\lambda) : \lambda \in \sigma(A) \},
$$

which implies $$\sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}$$, the first desired result.

Next let us (2) prove that

$$
    \{ p(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(p(A))
$$

for a generic polynomial $$p$$ of positive degree.

Consider an arbitrary $$\lambda$$ in the spectrum $$\sigma(A)$$ of $$A$$. Linearity implies

$$
    p(A) - p(\lambda) \mathbf{1} = \alpha_0 (\mathbf{1} - \mathbf{1}) + \cdots + \alpha_{m-1} (A^{m - 1} - \lambda^{m - 1} \mathbf{1}) + \alpha_m (A^m - \lambda^m \mathbf{1}).
$$

However,

$$
    A^k - \lambda^k \mathbf{1} = (A - \lambda \mathbf{1}) (A^{k-1} + \lambda A^{k-2} + \lambda^2 A^{k-3} + \cdots + \lambda^{k-1} \mathbf{1}).
$$

This allows us to pull out a $$(A - \lambda \mathbf{1})$$ factor from each summand in our expression for $$p(A) - p(\lambda) \mathbf{1}$$ giving

$$
    p(A) - p(\lambda) \mathbf{1} = (A - \lambda \mathbf{1}) q(A),
$$

where $$q(A)$$ is a $$\lambda$$ dependent polynomial.

Now as $$\lambda$$ is in $$\sigma(A)$$, by definition $$(A - \lambda \mathbf{1})$$ is not invertible in $$\mathcal{B}(\mathbf{H})$$. Furthermore, by construction $$(A - \lambda \mathbf{1})$$ commutes with $$q(A)$$. Hence, as a result of [**Lemma**](#lmm:hall-ex-8.3.1) the lefthand side $$(A - \lambda \mathbf{1}) q(A)$$ of the previous equation isn't invertible. Hence, $$p(A) - p(\lambda) \mathbf{1}$$ isn't invertible, and thus $$p(\lambda)$$ is an element of the spectrum $$\sigma(p(A))$$ of $$p(A)$$. In other words

$$
    \{ p(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(p(A)),
$$

the second desired result.

Next let us (3) prove that

$$
    \sigma(p(A)) \subseteq \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

for a generic polynomial $$p$$ of positive degree.

Consider an arbitrary $$\gamma$$ in the spectrum $$\sigma(p(A))$$ of $$p(A)$$. As a result of the [**Fundamental Theorem of Algebra**](#thrm:fundamental-theorem-of-algebra) we can factor the polynomial $$p(z) - \gamma$$ as a function of $$z$$ as follows

$$
    p(z) - \gamma = c (z - b_1)(z - b_2)\cdots(z - b_m),
$$

where $$c, b_i\in \mathbb{C}$$. Thus, as $$A$$ commutes with itself and $$\mathbf{1}$$, we also have

$$
    p(A) - \gamma \mathbf{1} = c (A - b_1 \mathbf{1} )(A - b_2 \mathbf{1} )\cdots(A - b_m \mathbf{1} ).
$$

Now as $$\gamma \in \sigma(p(A))$$ it follows that $$p(A) - \gamma \mathbf{1}$$ is not invertible. Thus there must exist some $$j$$ such that $$(A - b_j \mathbf{1})$$ is not invertible. If no such $$j$$ existed, then all the terms on the righthand side of this equation would be invertible which would imply that $$p(A) - \gamma \mathbf{1}$$ is invertible, which we already know is not the case.

Now as $$(A - b_j \mathbf{1})$$ is not invertible, this implies that $$b_j$$ is an element in the spectrum $$\sigma(A)$$ of $$A$$. However, from our equation for $$p(z)$$ we know that $$p(z)$$ evaluated at this $$b_j$$ satisfies

$$
    p(b_j) - \gamma = c (b_j - b_1)(b_j - b_2)\cdots(b_j -  b_j)\cdots(b_j - b_m) = 0.
$$

This implies that

$$
    \gamma = p(b_j),
$$

which is none other than the statement that an arbitrary $$\gamma$$ in the spectrum $$\sigma(p(A))$$ of $$p(A)$$ is of the form $$p(\lambda)$$ for a $$\lambda$$ in $$\sigma(A)$$. This is exactly the third desired result

$$
    \sigma(p(A)) \subseteq \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

for a generic polynomial $$p(\lambda)$$ of positive degree.

Finally we (4) conclude that

$$
    \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

as a result of the proofs of Parts 1-3.

Part 1 establishes this result for a constant polynomial. Part 2 establishes that

$$
    \{ p(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(p(A))
$$

for a generic polynomial of positive degree while Part 3 establishes that

$$
    \sigma(p(A)) \subseteq \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

also for a generic polynomial of positive degree. So Part 2 and Part 3 imply that

$$
    \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

for a generic polynomial of positive degree, while Part 1 establishes the result for a polynomial of degree zero. This establishes the desired result for a generic polynomial of arbitrary finite degree.$$\blacksquare$$

We record separately a fact used both in constructing the continuous functional calculus and in establishing its self-adjointness.

> **Lemma** *(A Real Polynomial in a Self-Adjoint Operator is Self-Adjoint)*
<a name="lmm:real-polynomial-self-adjoint"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{lmm:adjoint-algebra} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$p$$ be a polynomial with real coefficients, so that
>
> $$
>     p(A) = c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_m A^m, \qquad c_0, \ldots, c_m \in \mathbb{R}.
> $$
>
> Then $$p(A)$$ is self-adjoint.

**Proof**
By [**Lemma** *(Algebraic Properties of the Adjoint)*](#lmm:adjoint-algebra) the adjoint is additive and conjugate-homogeneous, and $$(A^k)^* = (A^*)^k$$ for every $$k \ge 0$$, so

$$
\begin{align}
    p(A)^* &= \left( c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_m A^m \right)^* \\
           &= (c_0 \mathbf{1})^* + (c_1 A)^* + (c_2 A^2)^* + \cdots + (c_m A^m)^* \\
           &= \overline{c_0} \mathbf{1}^* + \overline{c_1} A^* + \overline{c_2} (A^*)^2 + \cdots + \overline{c_m} (A^*)^m \\
           &= c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_m A^m \\
           &= p(A),
\end{align}
$$

the fourth line using that $$A^* = A$$, that $$\mathbf{1}^* = \mathbf{1}$$, and that each $$c_k$$ is real so $$\overline{c_k} = c_k$$.$$\blacksquare$$


The last step in **Stage 1: The Continuous Functional Calculus** is to generalize the map of the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem)

$$
    p \longmapsto p(A),
$$

taking complex-valued polynomials on $$\sigma(A)$$ to elements of $$\mathcal{B}(\mathbf{H})$$, to take real-valued, continuous functions $$f$$ on $$\sigma(A)$$ to elements $$f(A)$$ of $$\mathcal{B}(\mathbf{H})$$.

We will do so using the [**Stone–Weierstrass Theorem for Real Numbers**](#thrm:stone–weierstrass-real) to prove that the set of polynomials on $$\sigma(A)$$ is dense in $$C^0(\sigma(A); \mathbb{R})$$---the space of continuous, real-valued functions on $$\sigma(A)$$. Then we will use this fact along with the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem) to extend the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) map $$ p \mapsto p(A)$$ to all of $$C^0(\sigma(A); \mathbb{R})$$

$$
    f \longmapsto f(A).
$$

The construction in the next proposition draws on four standard results, which we state first: a definition from the theory of algebras of functions, the Stone–Weierstrass Theorem, the Boundedness Theorem, and the Bounded Linear Transformation Theorem.

> **Definition** *(Separates Points)*
<a name="def:separates-points"></a>
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. The algebra $$\mathcal{A}$$ is said to *separate points* if for any $$x,y \in X$$ such that $$x \neq y$$ there exists an $$f \in \mathcal{A}$$ such that $$f(x) \neq f(y)$$.

> **Theorem** *(Stone–Weierstrass for Real Numbers)*
<a name="thrm:stone–weierstrass-real"></a>
<!--  \uses{def:separates-points} -->
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. If $$\mathcal{A}$$ contains the constant functions and separates points, then $$\mathcal{A}$$ is dense in $$C^0(X; \mathbb{R})$$ with respect to the supremum norm.

> **Theorem** *(Boundedness Theorem)*
<a name="thrm:boundedness-theorem"></a>
> A continuous real-valued function on a non-empty compact set $$C$$ is bounded on $$C$$.

> **Theorem** *(Bounded Linear Transformation Theorem)*
<a name="thrm:bounded-linear-transformation-theorem"></a>
> Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}\vert_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.

Let's get started.

> **Proposition** *(The Continuous Functional Calculus)*
<a name="prpstn:hall-8.3"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:stone–weierstrass-real} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:hall-8.1} -->
<!--  \uses{def:spectral-radius} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{lmm:real-polynomial-self-adjoint} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. Then there exists a unique bounded linear map from $$C^0(\sigma(A); \mathbb{R})$$---the space of continuous, real-valued functions on the spectrum $$\sigma(A)$$ of $$A$$---to $$\mathcal{B}(\mathbf{H})$$
>
> $$
>     f \longmapsto f(A)
> $$
>
> such that when restricted to real-valued polynomials on $$\sigma(A)$$ it agrees with the restriction of the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) map $$p \mapsto p(A)$$. This map $$f \mapsto f(A)$$ is called the *(real-valued) functional calculus* for $$A$$.

**Proof**
Consider a real-valued polynomial on $$\sigma(A)$$ the spectrum of $$A$$. The map 

$$
    p \longmapsto p(A)
$$

of the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) results in

$$
    p(A) = c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_{m - 1} A^{m - 1} + c_m A^m,
$$

with $$\mathbb{R}$$ valued coefficients $$c_i$$. By [**Lemma** *(A Real Polynomial in a Self-Adjoint Operator is Self-Adjoint)*](#lmm:real-polynomial-self-adjoint), $$p(A)$$ is self-adjoint.

Now we can apply the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) to this real-valued polynomial to conclude that

$$
    \sigma(p(A)) = \{ p(\lambda) : \lambda \in \sigma(A) \}.
$$

Furthermore, as $$p(A)$$ is self-adjoint, we can apply the [**Lemma**](#lmm:hall-8.1) to conclude that

$$
    \|p(A)\| = R(p(A)).
$$

The definition of [spectral radius](#def:spectral-radius), however, implies that

$$
    R(p(A)) = \sup\limits_{\gamma \in \sigma(p(A))} \lvert \gamma \rvert.
$$

Putting this all together we conclude that

$$
\begin{align}
    \|p(A)\| &= R(p(A)) \\
             &= \sup\limits_{\gamma \in \sigma(p(A))} \lvert \gamma \rvert \\
             &= \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert,
\end{align}
$$

proving that

$$
    \|p(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert,
$$

which is simply the statement that the map $$p \mapsto p(A)$$ is isometric.

Explicitly, the map $$p \mapsto p(A)$$ from the set of real-valued polynomials on $$\sigma(A)$$ equipped with the supremum norm into $$\mathcal{B}(\mathbf{H})$$ equipped with the operator norm, is isometric. This map is also linear; for real-valued polynomials $$p$$ and $$q$$ we have $$(p + q) \mapsto (p + q)(A) = p(A) + q(A)$$.

Before proceeding, we pause to address a subtlety in the definition of this map. The map $$p \mapsto p(A)$$ has been described as a map on the set of real-valued polynomials *on* $$\sigma(A)$$, i.e. on polynomial *functions* with domain $$\sigma(A)$$, whereas the operator

$$
    p(A) = c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_{m - 1} A^{m - 1} + c_m A^m
$$

is computed from the *coefficients* $$c_0, c_1, \ldots, c_m$$. These are not the same datum: distinct coefficient tuples can determine the same function on $$\sigma(A)$$. For instance, if $$\sigma(A) = \{ 0, 1 \}$$, then the polynomials $$p(\lambda) = \lambda$$ and $$q(\lambda) = \lambda^2$$ agree at every point of $$\sigma(A)$$ while having different coefficients. For the map $$p \mapsto p(A)$$ to be well-defined on polynomial functions we must therefore verify that whenever two real-valued polynomials $$p$$ and $$q$$ agree at every point of $$\sigma(A)$$, the operators $$p(A)$$ and $$q(A)$$ coincide.

This follows from the isometry just established. Let $$p$$ and $$q$$ be real-valued polynomials with $$p(\lambda) = q(\lambda)$$ for all $$\lambda \in \sigma(A)$$. Then $$p - q$$ is a real-valued polynomial satisfying $$(p - q)(\lambda) = 0$$ for all $$\lambda \in \sigma(A)$$. Applying the isometry to $$p - q$$ and using the linearity of the map noted above gives

$$
\begin{align}
    \left\| p(A) - q(A) \right\| &= \left\| (p - q)(A) \right\| \\
                                 &= \sup\limits_{\lambda \in \sigma(A)} \lvert (p - q)(\lambda) \rvert \\
                                 &= \sup\limits_{\lambda \in \sigma(A)} 0 \\
                                 &= 0.
\end{align}
$$

As $$\| \cdot \|$$ is a norm on $$\mathcal{B}(\mathbf{H})$$, the fact that $$\left\| p(A) - q(A) \right\| = 0$$ implies $$p(A) - q(A)$$ is the zero operator, i.e.

$$
    p(A) = q(A).
$$

Hence, the operator $$p(A)$$ depends only on the function $$p$$ restricted to $$\sigma(A)$$, and not on the particular choice of coefficients representing it. Thus the map $$p \mapsto p(A)$$ is well-defined as a map on the set of real-valued polynomial functions on $$\sigma(A)$$.

Now in preparation for the application of the [**Stone–Weierstrass Theorem for Real Numbers**](#thrm:stone–weierstrass-real) let us examine explicitly some of the properties of the objects we are currently considering.

As one will recall, [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable) established that the spectrum $$\sigma(A)$$ of $$A$$ is a non-empty, compact metric measurable space.

In addition, any element $$p$$ in the algebra of real-valued polynomials on $$\sigma(A)$$ is continuous. Hence, the algebra of real-valued polynomials on $$\sigma(A)$$ is an algebra in $$C^0(\sigma(A); \mathbb{R})$$, the space of continuous, real-valued functions on $$\sigma(A)$$.

Obviously the algebra of real-valued polynomials on $$\sigma(A)$$ contains the constant functions

$$
    p(\lambda) = c_0.
$$

In addition this algebra [separates points](#def:separates-points). Explicitly, let $$x$$ and $$y$$ be any elements in $$\sigma(A)$$ such that $$x \neq y$$. Note that [**Proposition**](#prpstn:hall-7.7) along with the hypothesis that $$A$$ is self-adjoint, imply that $$x,y \in \sigma(A) \subset \mathbb{R}$$. Hence, the polynomial

$$
    p_s(\lambda) = (\lambda - x)
$$

on $$\sigma(A)$$ is a real-valued polynomial. Evaluating $$p_s$$ at $$x$$ and $$y$$ gives

$$
\begin{align}
    p_s(x) &= (x - x) = 0 \\
    p_s(y) &= (y - x) \neq 0,
\end{align}
$$

where the final $$\neq$$ follows from the fact that $$x \neq y$$. Hence, the real-valued polynomials on $$\sigma(A)$$ separate points.

With all of this in-hand we can apply the [**Stone–Weierstrass Theorem for Real Numbers**](#thrm:stone–weierstrass-real) to the current situation. Identifying $$X$$ with $$\sigma(A)$$ and $$\mathcal{A}$$ with the real-valued polynomials on $$\sigma(A)$$, the [**Stone–Weierstrass Theorem for Real Numbers**](#thrm:stone–weierstrass-real) allows us to conclude that real-valued polynomials on $$\sigma(A)$$ are dense in $$C^0(\sigma(A); \mathbb{R})$$.

Next we must prepare for the application of the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem). To do so, we must establish some relatively straightforward properties of objects we are currently considering. 

Consider $$C^0(\sigma(A); \mathbb{R})$$, the space of continuous, real-valued functions on $$\sigma(A)$$. As $$\sigma(A)$$ is compact the [**Boundedness Theorem**](#thrm:boundedness-theorem) implies that any element of $$C^0(\sigma(A); \mathbb{R})$$ is bounded. Hence, the supremum norm

$$
    \|f\| \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert
$$

on $$C^0(\sigma(A); \mathbb{R})$$ is finite. Furthermore, as a result of the fact that $$\lvert \cdot \rvert$$ defines a norm on $$\mathbb{R}$$, this supremum norm defines a norm on $$C^0(\sigma(A); \mathbb{R})$$. In other words $$C^0(\sigma(A); \mathbb{R})$$ is a normed space.

Recall, as proven in the [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space), $$\mathcal{B}(\mathbf{H})$$ is a Banach space under the operator norm.

Also recall we proved that the map $$p \mapsto p(A)$$ from the real-valued polynomials on $$\sigma(A)$$ into $$\mathcal{B}(\mathbf{H})$$ is linear and isometric satisfying

$$
    \|p(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert. 
$$

This implies

$$
    \|p(A)\| \le 1 \cdot \|p\| \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert, 
$$

which is none other than the statement that the linear map $$p \mapsto p(A)$$ is bounded using constant $$1$$.

With all of this in hand we can apply the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem) to the current situation. Identifying $$V_1$$ with $$C^0(\sigma(A); \mathbb{R})$$, $$V_2$$ with $$\mathcal{B}(\mathbf{H})$$, $$W$$ the real-valued polynomials on $$\sigma(A)$$, and $$T$$ with our map $$p \mapsto p(A)$$ allows us to conclude that there exists a unique, bounded, linear map

$$
    f \longmapsto f(A)
$$

from $$C^0(\sigma(A); \mathbb{R})$$ to $$\mathcal{B}(\mathbf{H})$$ that when restricted to real-valued polynomials agrees with our map $$p \mapsto p(A)$$ and that has the same norm of our map $$p \mapsto p(A)$$.

This map $$f \mapsto f(A)$$ is the desired result of this proposition and is known as the *(real-valued) functional calculus* for $$A$$.$$\blacksquare$$

As a final step in **Stage 1: The Continuous Functional Calculus**, we will derive some basic properties of the (real-valued) functional calculus of a self-adjoint operator $$A$$ in $$\mathcal{B}(\mathbf{H})$$. These properties require the following definition

> **Definition** *(Non-Negative Bounded Operator)*
<a name="def:non-negative-operator"></a>
> <!--  \uses{def:bounded-operator-notation} -->
> An operator $$A \in \mathcal{B}(\mathbf{H})$$ is called a *non-negative bounded operator* if
> 
> $$
>     0 \le \left< \psi, A\psi \right>
> $$
> 
> for all $$\psi \in \mathbf{H}$$.

as well as the following lemma

> **Lemma** *(Invertibility is an Open Condition)*
<a name="lmm:hall-prblm-7.4.8"></a>
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{lmm:lemma-2} -->
<!--  \uses{lmm:hall-7.6} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is invertible in $$\mathcal{B}(\mathbf{H})$$, then there exists an $$\epsilon > 0$$ such that for all $$B \in \mathcal{B}(\mathbf{H})$$ that satisfy
> 
> $$
>     \|B - A\| < \epsilon
> $$
> 
> $$B$$ is also invertible in $$\mathcal{B}(\mathbf{H})$$.

**Proof**
We start this proof by noting that as $$A$$ is by hypothesis invertible we have

$$
\begin{align}
    B &= A - (A - B) \\
      &= A (\mathbf{1} - A^{-1}(A - B)),
\end{align}
$$

where the final equation follows from factoring out a common $$A$$ at the expense of introducing $$A^{-1}$$.

Now, as a result of [**Lemma**](#lmm:hall-7.6), if

$$
    \|A^{-1}(A - B)\| < 1,
$$

then $$(\mathbf{1} - A^{-1}(A - B))$$ is invertible in $$\mathcal{B}(\mathbf{H})$$. As $$A$$ is also invertible in $$\mathcal{B}(\mathbf{H})$$, this condition implies that as $$B$$ is given by

$$
    B = A (\mathbf{1} - A^{-1}(A - B))
$$

it is invertible in $$\mathcal{B}(\mathbf{H})$$.

As a result of [**Lemma**](#lmm:lemma-2) operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative. This along with the norm definition imply

$$
\begin{align}
    \|A^{-1}(A - B)\| &= \|A^{-1}(B - A)\| \\
                      &\le \|A^{-1}\| \, \|B - A\|.
\end{align}
$$

Note first that $$\left\| A^{-1} \right\| \ne 0$$, so that division by it is legitimate: if $$A^{-1}$$ were the zero operator then $$\mathbf{1} = AA^{-1} = 0$$, forcing $$\mathbf{H} = \{0\}$$, which is excluded by the standing assumption of this post. Now if we define the $$\epsilon$$ of the hypothesis by

$$
    \epsilon \equiv \frac{1}{\|A^{-1}\|},
$$

then if

$$
    \|B - A\| < \epsilon
$$

it follows that

$$
    \|B - A\| < \frac{1}{\|A^{-1}\|}
$$

and thus

$$
    \|B - A\| \, \|A^{-1}\| < 1.
$$

However, from submultiplicativity we already established that

$$
    \|A^{-1}(A - B)\| \le \|A^{-1}\| \, \|B - A\|.
$$

Hence, we have

$$
    \|A^{-1}(A - B)\| \le \|A^{-1}\| \, \|B - A\| < 1.
$$

This is none other than the condition

$$
    \|A^{-1}(A - B)\| < 1
$$

which we previously found is the condition required for $$B$$ to be invertible.$$\blacksquare$$

The next proposition uses the following elementary fact about continuity, which we state first.

> **Theorem** *(Composition Theorem)*
<a name="thrm:composition-theorem"></a>
> If a function $$f$$ is continuous at $$c$$ and a function $$h$$ is continuous at $$f(c)$$, then the composition $$h \circ f$$ is continuous at $$c$$.

The properties of the (real-valued) functional calculus are captured in the following proposition

> **Proposition** *(Properties of the Continuous Functional Calculus)*
<a name="prpstn:hall-8.4"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:cfc-non-negative} -->
<!--  \uses{prpstn:cfc-norm} -->
<!--  \uses{prpstn:cfc-self-adjoint} -->
<!--  \uses{prpstn:cfc-spectral-mapping} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{def:non-negative-operator} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{thrm:composition-theorem} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{lmm:hall-prblm-7.4.8} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{prpstn:continuity-of-the-adjoint} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, the (real-valued) functional calculus for $$A$$, mapping $$C^0(\sigma(A); \mathbb{R})$$ into $$\mathcal{B}(\mathbf{H})$$, has the following properties
> 
> 1. **Multiplicativity:** For all $$f,g \in C^0(\sigma(A); \mathbb{R})$$, we have
> 
>    $$
>        (fg)(A) = f(A)g(A),
>    $$
> 
>    where $$(fg)$$ denotes the pointwise product of $$f$$ and $$g$$, i.e. $$(fg)(\lambda) \equiv f(\lambda)g(\lambda)$$.
> 2. **Self-adjointness:** For any $$f \in C^0(\sigma(A); \mathbb{R})$$, the operator $$f(A)$$ is self-adjoint.
> 3. **Non-negativity:** For any $$f \in C^0(\sigma(A); \mathbb{R})$$ such that $$f$$ is non-negative, it follows that $$f(A)$$ is a non-negative bounded operator.
> 4. **Norm and spectrum properties:** For any $$f \in C^0(\sigma(A); \mathbb{R})$$, we have
> 
>    $$
>        \|f(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert,
>    $$
> 
>    where $$\|f(A)\|$$ is the operator norm of $$f(A)$$ and $$\sigma(A)$$ is the spectrum of $$A$$, and
> 
>    $$
>        \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \},
>    $$
> 
>    where $$\sigma(f(A))$$ is the spectrum of $$f(A)$$.

**Proof**
Each of the four properties is established separately below: multiplicativity in [**Proposition** *(The Continuous Functional Calculus is Multiplicative)*](#prpstn:cfc-multiplicative), self-adjointness in [**Proposition** *(The Continuous Functional Calculus Yields Self-Adjoint Operators)*](#prpstn:cfc-self-adjoint), non-negativity in [**Proposition** *(The Continuous Functional Calculus Preserves Non-Negativity)*](#prpstn:cfc-non-negative), and the two norm-and-spectrum identities in [**Proposition** *(Norm of an Operator from the Continuous Functional Calculus)*](#prpstn:cfc-norm) and [**Proposition** *(Spectral Mapping for the Continuous Functional Calculus)*](#prpstn:cfc-spectral-mapping) respectively.$$\blacksquare$$

> **Proposition** *(The Continuous Functional Calculus is Multiplicative)*
<a name="prpstn:cfc-multiplicative"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{thrm:composition-theorem} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{prpstn:products-converge-uniformly} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$f \mapsto f(A)$$ be the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3). Then for all $$f,g \in C^0(\sigma(A); \mathbb{R})$$,
>
> $$
>     (fg)(A) = f(A)g(A),
> $$
>
> where $$(fg)(\lambda) \equiv f(\lambda)g(\lambda)$$.

**Proof**
for all $$f,g \in C^0(\sigma(A); \mathbb{R})$$, we have

$$
    (fg)(A) = f(A)g(A),
$$

where $$(fg)$$ denotes the pointwise product of $$f$$ and $$g$$, i.e. $$(fg)(\lambda) \equiv f(\lambda)g(\lambda)$$.

As a result of the proof of [**Proposition**](#prpstn:hall-8.3) we know the real-valued polynomials on the spectrum $$\sigma(A)$$ of $$A$$ are dense in $$C^0(\sigma(A); \mathbb{R})$$ with respect to the supremum norm. Hence, there exists a sequence $$\{ s_i \}_{i \in \mathbb{N}}$$ in the set of real-valued polynomials on $$\sigma(A)$$ such that $$s_i \rightarrow f$$ uniformly. Similarly, there exists a sequence $$\{ r_j \}_{j \in \mathbb{N}}$$ in the set of real-valued polynomials on $$\sigma(A)$$ such that $$r_j \rightarrow g$$ uniformly.

Recall that by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a non-empty, compact metric measurable space. Thus as a result of the [**Boundedness Theorem**](#thrm:boundedness-theorem) $$f$$, $$g$$, and all the $$s_i$$ and $$r_j$$ are bounded.

This setup will now allow us to prove that $$s_i r_i \rightarrow fg$$ uniformly.

Each $$r_j$$ is bounded, and $$f$$ and $$g$$ are bounded on the compact set $$\sigma(A)$$, by the [**Boundedness Theorem**](#thrm:boundedness-theorem) — these are exactly the hypotheses of the proposition below, which derives the uniform bound on the $$r_j$$ itself. So [**Proposition** *(Products of Uniform Approximants Converge Uniformly)*](#prpstn:products-converge-uniformly), applied on $$X = \sigma(A)$$ to the sequences $$\{s_i\}$$ and $$\{r_j\}$$, gives: for every $$\epsilon > 0$$ there is an $$L$$ with

$$
    \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda)g(\lambda) - s_i(\lambda)r_j(\lambda) \rvert < \epsilon
$$

for all $$i,j \ge L$$.
As this applies for all $$i,j \ge L$$ it implies in particular if $$j = i$$ and $$i \ge L$$. So, for any $$\epsilon > 0$$ there exists a natural number $$L$$ such that for all $$i \ge L$$ we have 

$$
    \lvert f(\lambda)g(\lambda) - s_i(\lambda)r_i(\lambda) \rvert < \epsilon
$$

for all $$\lambda \in \sigma(A)$$. In other words $$s_ir_i \rightarrow fg$$ uniformly.

Hence, we have

$$
\begin{align}
    (fg)(A) &= (\lim_{i \rightarrow \infty} s_ir_i)(A) \\
            &= \lim_{i \rightarrow \infty} (s_ir_i)(A) \\
            &= \lim_{i \rightarrow \infty} s_i(A) r_i(A) \\
            &= f(A) g(A),
\end{align}
$$

where the first equality follows from our previous derivation, the second equality from [**Proposition**](#prpstn:hall-8.3) proving that for real-valued polynomials $$p$$ the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) map $$p \rightarrow p(A)$$ is isometric, the third equality from $$(s_ir_i)(\lambda) \equiv s_i(\lambda)r_i(\lambda)$$, and the fourth equality follows from [**Proposition**](#prpstn:hall-8.3) which proved $$s_i(A)r_i(A) \rightarrow f(A)g(A)$$ relative to the operator norm.


In summary this proves the desired multiplicativity result, $$(fg)(A) = f(A) g(A)$$.
$$\blacksquare$$

> **Proposition** *(The Continuous Functional Calculus Yields Self-Adjoint Operators)*
<a name="prpstn:cfc-self-adjoint"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:continuity-of-the-adjoint} -->
<!--  \uses{lmm:real-polynomial-self-adjoint} -->
> With notation as in [**Proposition** *(The Continuous Functional Calculus is Multiplicative)*](#prpstn:cfc-multiplicative), for any $$f \in C^0(\sigma(A); \mathbb{R})$$ the operator $$f(A)$$ is self-adjoint.

**Proof**
for any $$f \in C^0(\sigma(A); \mathbb{R})$$, the operator $$f(A)$$ is self-adjoint.

By [**Proposition**](#prpstn:hall-8.3) there exists a sequence $$\{ s_i \}_{i \in \mathbb{N}}$$ in the set of real-valued polynomials on $$\sigma(A)$$ such that $$s_i \rightarrow f$$ uniformly.

Furthermore, as any $$s_i$$ is a real-valued polynomial, the map $$s_i \mapsto s_i(A)$$ of the [**Lemma** *(Spectral Mapping Theorem)*](#lmm:spectral-mapping-theorem) gives

$$
    s_i(A) = c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_{m - 1} A^{m - 1} + c_m A^m,
$$

with $$\mathbb{R}$$ valued coefficients $$c_i$$. By [**Lemma** *(A Real Polynomial in a Self-Adjoint Operator is Self-Adjoint)*](#lmm:real-polynomial-self-adjoint), each $$s_i(A)$$ is self-adjoint.

This then implies, using [**Proposition** *(Continuity of the Adjoint)*](#prpstn:continuity-of-the-adjoint) to exchange the adjoint with the limit,

$$
\begin{align}
    f(A)^* &= \left( \lim_{i \rightarrow \infty} s_i(A) \right)^* \\
           &= \lim_{i \rightarrow \infty} s_i(A)^* \\
           &= \lim_{i \rightarrow \infty} s_i(A) \\
           &= f(A),
\end{align}
$$

proving that $$f(A)^* = f(A)$$ and thus that $$f(A)$$ is self-adjoint, the desired self-adjointness result.
$$\blacksquare$$

> **Proposition** *(The Continuous Functional Calculus Preserves Non-Negativity)*
<a name="prpstn:cfc-non-negative"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:composition-theorem} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{def:non-negative-operator} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:cfc-self-adjoint} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$f \mapsto f(A)$$ the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3), if $$f \in C^0(\sigma(A); \mathbb{R})$$ is non-negative then $$f(A)$$ is a non-negative bounded operator.

**Proof**
for any $$f \in C^0(\sigma(A); \mathbb{R})$$ such that $$f$$ is non-negative, it follows that $$f(A)$$ is a non-negative bounded operator.

If $$f \in C^0(\sigma(A); \mathbb{R})$$ is non-negative, then there exists a continuous function $$g$$ in $$C^0(\sigma(A); \mathbb{R})$$ such that $$g = \sqrt{f}$$. This follows from the fact that $$f$$ is by hypothesis continuous and the square root function

$$
\begin{align}
    h : [0, \infty) &\longrightarrow [0, \infty) \\ 
             t      &\longmapsto h(t) \equiv \sqrt{t}
\end{align}
$$

is continuous. Hence, as a result of the [**Composition Theorem**](#thrm:composition-theorem) we know $$h \circ f = \sqrt{f}$$ is continuous on $$\sigma(A)$$ and thus an element of $$C^0(\sigma(A); \mathbb{R})$$.

With $$g \equiv \sqrt{f}$$ it follows that $$f = g^2$$. Applying [**Proposition** *(The Continuous Functional Calculus is Multiplicative)*](#prpstn:cfc-multiplicative) we have $$f(A) = g(A)g(A)$$. Applying [**Proposition** *(The Continuous Functional Calculus Yields Self-Adjoint Operators)*](#prpstn:cfc-self-adjoint) we know that $$g(A)$$ is self-adjoint. Hence, for any $$\psi \in \mathbf{H}$$ we have

$$
\begin{align}
    \left< \psi, f(A)\psi \right> &= \left< \psi, g(A)g(A)\psi \right> \\
                                  &= \left< \psi, g(A)^*g(A)\psi \right> \\
                                  &= \left< g(A)\psi, g(A)\psi \right> \\
                                  &\ge 0,
\end{align}
$$

where the final inequality follows from the definition of an inner product. This implies that for any $$\psi \in \mathbf{H}$$ we have

$$
    0 \le \left< \psi, f(A)\psi \right>.
$$

As $$f(A)$$ is bounded as a result of [**Proposition**](#prpstn:hall-8.3), this is none other than the statement that $$f(A)$$ is a non-negative bounded operator, the desired result.
$$\blacksquare$$

> **Proposition** *(Norm of an Operator from the Continuous Functional Calculus)*
<a name="prpstn:cfc-norm"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$f \mapsto f(A)$$ the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3), for any $$f \in C^0(\sigma(A); \mathbb{R})$$,
>
> $$
>     \|f(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert,
> $$
>
> where $$\|f(A)\|$$ is the operator norm of $$f(A)$$.

**Proof**
for any $$f \in C^0(\sigma(A); \mathbb{R})$$, we have

$$
    \|f(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert,
$$

where $$\|f(A)\|$$ is the operator norm of $$f(A)$$ and $$\sigma(A)$$ is the spectrum of $$A$$, and

$$
    \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \},
$$

where $$\sigma(f(A))$$ is the spectrum of $$f(A)$$.

Let us first prove that

$$
    \|f(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert.
$$

By [**Proposition**](#prpstn:hall-8.3) there exists a sequence $$\{ s_i \}_{i \in \mathbb{N}}$$ in the set of real-valued polynomials on $$\sigma(A)$$ such that $$s_i \rightarrow f$$ uniformly.

As proven in [**Proposition**](#prpstn:hall-8.3) for a real-valued polynomials $$p$$ on $$\sigma(A)$$ the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) map $$p \rightarrow p(A)$$ is isometric

$$
    \|p(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert.
$$

This implies

$$
\begin{align}
    \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert
    &= \sup\limits_{\lambda \in \sigma(A)} \lvert \lim_{i \rightarrow \infty} s_i (\lambda) \rvert \\
    &= \lim_{i \rightarrow \infty} \sup\limits_{\lambda \in \sigma(A)} \lvert s_i (\lambda) \rvert \\
    &= \lim_{i \rightarrow \infty} \| s_i(A) \| \\
    &= \| f(A) \|,
\end{align}
$$

where the first equality follows from the fact that $$s_i \rightarrow f$$, the second from the fact that this convergence is uniform, the third equation from the fact that $$p \rightarrow p(A)$$ is isometric, and the final from [**Proposition**](#prpstn:hall-8.3) which proved $$s_i(A) \rightarrow f(A)$$ relative to the operator norm. So with this we have proven the first, desired result

$$
   \| f(A) \| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert
$$ 

as required.$$\blacksquare$$

> **Proposition** *(Spectral Mapping for the Continuous Functional Calculus)*
<a name="prpstn:cfc-spectral-mapping"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{prpstn:cfc-self-adjoint} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{lmm:hall-prblm-7.4.8} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:hall-7.5} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$f \mapsto f(A)$$ the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3), for any $$f \in C^0(\sigma(A); \mathbb{R})$$,
>
> $$
>     \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \},
> $$
>
> where $$\sigma(f(A))$$ is the spectrum of $$f(A)$$.

**Proof**
We prove the two inclusions in turn.

$$
    \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \},
$$

where $$\sigma(f(A))$$ is the spectrum of $$f(A)$$ and $$\sigma(A)$$ is the spectrum of $$A$$.

We will prove this by first proving that $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$. We will then prove $$\{ f(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(f(A)$$. Together this will entail the desired result 

$$
    \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \}.
$$

We start by proving $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$ by proving its contrapositive. In other words we will prove that any element of $$\mathbb{C}$$ not in $$\{ f(\lambda) : \lambda \in \sigma(A) \}$$ is not in $$\sigma(f(A)$$.

To that end consider an arbitrary element $$\lambda_0 \in \mathbb{C}$$ such that $$\lambda_0$$ is not in $$\{ f(\lambda) : \lambda \in \sigma(A) \}$$. In other words, there exists no $$\mu \in \sigma(A)$$ such that $$f(\mu) = \lambda_0$$.

Such a $$\lambda_0$$ could lie in the complement of $$\mathbb{R}$$ in $$\mathbb{C}$$ or it could lie in $$\mathbb{R}$$ in $$\mathbb{C}$$. We will deal with these two cases separately.

Assume first that $$\lambda_0$$ is in the complement of $$\mathbb{R}$$ in $$\mathbb{C}$$. This in particular implies that the imaginary component of $$\lambda_0$$ is non-zero.

Now, by [**Proposition** *(The Continuous Functional Calculus Yields Self-Adjoint Operators)*](#prpstn:cfc-self-adjoint), $$f(A)$$ is self-adjoint. As $$f(A)$$ is self-adjoint, [**Proposition**](#prpstn:hall-7.7) implies that $$\sigma(f(A))$$ is a subset of $$\mathbb{R}$$ in $$\mathbb{C}$$.

However, as the imaginary component of $$\lambda_0$$ is non-zero this implies that $$\lambda_0$$ is not in $$\sigma(f(A))$$.

This proves the contrapositive of $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$ holds when $$\lambda_0$$ is in the complement of $$\mathbb{R}$$ in $$\mathbb{C}$$, and thus proves $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$ holds in this case.

Now let us assume that $$\lambda_0$$ lies in $$\mathbb{R}$$ in $$\mathbb{C}$$. This implies that $$\lambda_0$$ is real-valued.

For this case, consider then the function $$g$$ on $$\sigma(A)$$ defined by

$$
    g(\lambda) \equiv \frac{1}{f(\lambda) - \lambda_0}.
$$

As $$f$$ is continuous and $$f(\mu) \neq \lambda_0$$ for all $$\mu \in \sigma(A)$$, it follows that $$g$$ is continuous. Furthermore, as $$f$$ is real-valued and $$\lambda_0$$ lies in $$\mathbb{R}$$ in $$\mathbb{C}$$, it follows that $$g$$ is real-valued. So $$g$$ is an element of $$C^0(\sigma(A); \mathbb{R})$$.
 
Now obviously for all $$\lambda \in \sigma(A)$$ we have

$$
    1 = (f(\lambda) - \lambda_0) \left( \frac{1}{f(\lambda) - \lambda_0} \right) = (f(\lambda) - \lambda_0) g(\lambda).
$$

By [**Proposition** *(The Continuous Functional Calculus is Multiplicative)*](#prpstn:cfc-multiplicative) this implies

$$
    \mathbf{1} = (f(A) - \lambda_0 \mathbf{1}) g(A).
$$

A similar argument using $$1 = g(\lambda) (f(\lambda) - \lambda_0)$$ implies

$$
    \mathbf{1} = g(A) (f(A) - \lambda_0 \mathbf{1}).
$$

In both cases $$g(A)$$ is bounded as a result of [**Proposition**](#prpstn:hall-8.3). This implies that the bounded operator $$g(A)$$ is the inverse of $$(f(A) - \lambda_0 \mathbf{1})$$. This in turn implies that $$\lambda_0$$ is not in the spectrum $$\sigma(f(A))$$ of $$f(A)$$.

This proves the contrapositive of $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$ holds when $$\lambda_0$$ is in $$\mathbb{R}$$ in $$\mathbb{C}$$, and thus proves $$\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}$$ holds in this case.

Next let us prove that $$\{ f(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(f(A)$$.

Assume that there exists some $$\lambda_0$$ such that $$\lambda_0 = f(\mu)$$ for some $$\mu$$ in the spectrum $$\sigma(A)$$ of $$A$$. Our goal is then to prove that $$f(\mu)$$ is in $$\sigma(f(A))$$. We will do so using proof by contradiction, assuming $$f(\mu)$$ is not in $$\sigma(f(A))$$ and proving this leads to a contradiction.

To that end, assume that $$f(\mu)$$ is in the resolvent set of $$A$$. Hence, $$f(A) - f(\mu) \mathbf{1}$$ is invertible in $$\mathcal{B}(\mathbf{H})$$.

By [**Proposition**](#prpstn:hall-8.3) there exists a sequence $$\{ s_i \}_{i \in \mathbb{N}}$$ in the set of real-valued polynomials on $$\sigma(A)$$ such that $$s_i \rightarrow f$$ uniformly.

As $$s_i \rightarrow f$$ uniformly [**Proposition**](#prpstn:hall-8.3) implies that $$s_i(A) \rightarrow f(A)$$ relative to the operator norm. Hence, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i \ge N$$ one has

$$
    \|f(A) - s_i(A)\| < \epsilon.
$$

As a result of $$s_i \rightarrow f$$ uniformly and $$s_i(A) \rightarrow f(A)$$ relative to the operator norm, one can conclude that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i \ge N$$ one has

$$
    \|(f(A) - f(\mu)\mathbf{1}) - (s_i(A) - s_i(\mu)\mathbf{1})\| < \epsilon.
$$

Now by assumption $$f(A) - f(\mu)\mathbf{1}$$ is invertible. Thus as a result of [**Lemma**](#lmm:hall-prblm-7.4.8) we can select $$\epsilon$$ so small that for the associated $$N$$ and $$i \ge N$$ one forces $$s_i(A) - s_i(\mu)\mathbf{1}$$ to invertible. However, this contradicts the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem).

For the polynomial $$s_i$$ the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) states

$$
    \sigma(s_i(A)) = \{ s_i(\mu) : \mu \in \sigma(A) \}.
$$

This implies that $$s_i(\mu)$$ should be in the spectrum of $$s_i(A)$$ which implies $$s_i(A) - s_i(\mu)\mathbf{1}$$ is not invertible. However, we just proved that under the assumption $$f(\mu)$$ is not in $$\sigma(f(A))$$ it follows that $$s_i(A) - s_i(\mu)\mathbf{1}$$ is invertible. Hence, our assumption that $$f(\mu)$$ is not in $$\sigma(f(A))$$ is false and $$f(\mu)$$ is in $$\sigma(f(A))$$.

Hence, we have proven the second desired result $$\{ f(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(f(A)$$.

Now we have proven

$$
\begin{align}
    &\{ f(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(f(A) \\
    &\sigma(f(A) \subseteq \{ f(\lambda) : \lambda \in \sigma(A) \}.
\end{align}
$$

Together these imply

$$
    \sigma(f(A) = \{ f(\lambda) : \lambda \in \sigma(A) \},
$$

the final desired result.$$\blacksquare$$


**Stage 2: An Operator-Valued Riesz Representation Theorem**

We are finally in a position to kick off Stage 2. In this stage we will prove that for a real-valued, continuous function $$f$$ on the spectrum $$\sigma(A)$$ of $$A$$, the operator $$f(A)$$ derived using real-valued functional calculus can be represented as integration against a projection-valued measure. This will essentially amount to an operator-valued version of the [**Riesz Representation Theorem**](#thrm:riesz-representation).

> **Theorem** *(Riesz Representation)*
<a name="thrm:riesz-representation"></a>
> Let $$X$$ be a compact metric space and let $$C^0(X; \mathbb{R})$$ be the space of continuous, real-valued functions on $$X$$. Suppose $$\Lambda : C^0(X; \mathbb{R}) \rightarrow \mathbb{R}$$ is a linear function with the property that $$\Lambda(f)$$ is non-negative whenever all the values of $$f$$ are non-negative. Then there exists a unique, real-valued, positive measure $$\mu$$ on the Borel $$\sigma$$-algebra of $$X$$ for which
>
> $$
>     \Lambda(f) = \int_X f \, d\mu
> $$
>
> for all $$f \in C^0(X; \mathbb{R})$$.

However, before considering an operator-valued version, let us consider how we can apply the non-operator-valued version to the situation at hand.

The hypothesis of the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators) presents us with an element $$A \in \mathcal{B}(\mathbf{H})$$ that is self-adjoint. For any continuous, real-valued function $$f$$ on the spectrum $$\sigma(A)$$ of $$A$$, i.e. any $$f \in C^0(\sigma(A) ; \mathbb{R})$$, the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3) defines a linear map $$f \mapsto f(A)$$ from $$C^0(\sigma(A) ; \mathbb{R})$$ into $$\mathcal{B}(\mathbf{H})$$. Furthermore, if $$f$$ is non-negative, then as a result of Part 3 of [**Proposition**](#prpstn:hall-8.4), it follows that $$f(A)$$ is a non-negative bounded operator, i.e. $$0 \le \left< \psi, f(A)\psi \right>$$ for all $$\psi \in \mathbf{H}$$.

Before defining our candidate functional, let us verify that the quantity $$\left< \psi, f(A) \psi \right>$$ is in fact a real number for any $$f \in C^0(\sigma(A) ; \mathbb{R})$$ and any $$\psi \in \mathbf{H}$$. As a result of Part 2 of [**Proposition**](#prpstn:hall-8.4), for any $$f \in C^0(\sigma(A) ; \mathbb{R})$$ the operator $$f(A)$$ is self-adjoint, i.e. $$f(A)^* = f(A)$$. Hence, for any $$\psi \in \mathbf{H}$$

$$
\begin{align}
    \overline{\left< \psi, f(A) \psi \right>} &= \left< f(A) \psi, \psi \right> \\
                                              &= \left< \psi, f(A)^* \psi \right> \\
                                              &= \left< \psi, f(A) \psi \right>,
\end{align}
$$

where the first line follows from the conjugate symmetry of the Hilbert space inner product, the second from the definition of the adjoint, and the third from the self-adjointness of $$f(A)$$. As a complex number equal to its own complex conjugate is real, we conclude

$$
    \left< \psi, f(A) \psi \right> \in \mathbb{R}
$$

for all $$f \in C^0(\sigma(A) ; \mathbb{R})$$ and all $$\psi \in \mathbf{H}$$.

Hence, for any $$\psi \in \mathbf{H}$$ the function $$\Lambda_\psi : C^0(\sigma(A) ; \mathbb{R}) \rightarrow \mathbb{R}$$ defined by

$$
    \Lambda_\psi(f) \equiv \left< \psi, f(A) \psi \right>
$$


#### Stage 2: From the Calculus to a Measure

is well-defined, in the sense that it does indeed take values in $$\mathbb{R}$$, and satisfies the hypotheses required by the [**Riesz Representation Theorem**](#thrm:riesz-representation). It is linear, as $$f \mapsto f(A)$$ is linear by [**Proposition**](#prpstn:hall-8.3) and the inner product is linear in its second argument, and it is non-negative whenever all the values of $$f$$ are non-negative, as established in the first paragraph above. Hence, we can apply the [**Riesz Representation Theorem**](#thrm:riesz-representation), which yields the following.

<a name="eqtn:hall-8.8"></a>
> **Proposition** *(The Measures Associated to a Self-Adjoint Operator)*
<a name="prpstn:associated-measures-self-adjoint"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{def:bounded-operator-notation} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. For every $$\psi \in \mathbf{H}$$ there is a unique positive, real-valued measure $$\mu_\psi$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$ such that
>
> $$
>     \left< \psi, f(A) \psi \right> = \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda)
> $$
>
> for all $$f \in C^0(\sigma(A) ; \mathbb{R})$$.

**Proof**
The functional $$\Lambda_\psi$$ is well defined, linear and non-negative, as established in the preceding paragraphs, so the [**Riesz Representation Theorem**](#thrm:riesz-representation) applies to it and supplies a unique positive measure $$\mu_\psi$$ representing it; unwinding the definition $$\Lambda_\psi(f) = \left< \psi, f(A)\psi \right>$$ gives the displayed identity.$$\blacksquare$$ Note how similar this is to the equality

$$
    \left< \psi, \left( \int_{\sigma(A)} f \, d\mu \right) \psi \right> = \int_{\sigma(A)} f(\lambda) d\mu_\psi(\lambda).
$$

that appears when [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) is formulated on $$X \equiv \sigma(A)$$. This will turn out to be more than a similarity. The remainder of Stage 2 will be dedicated to proving that these are indeed the same equation.  
 
To that end let us make the following definition

> **Definition** *(The Quadratic Form Associated to a Bounded Measurable Function)*
<a name="def:hall-8.6"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:hall-8.4} -->
> Let $$A$$ in $$\mathcal{B}(\mathbf{H})$$ be self-adjoint. For any bounded, measurable, complex-valued function $$f$$ on the spectrum $$\sigma(A)$$ of $$A$$ let us define a map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ by
> 
> $$
>     Q_f(\psi) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda),
> $$
> 
> where $$\mu_\psi$$ is the measure on $$\sigma(A)$$ derived from our map $$\Lambda_\psi$$ and the [**Riesz Representation Theorem**](#thrm:riesz-representation).

Before proceeding, let us record a basic property of the measures $$\mu_\psi$$ just defined. This property is used repeatedly in what follows---in particular it is the hypothesis required to apply the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem) to $$\mu_\psi$$---and so we isolate it here rather than re-deriving it at each point of use.

> **Lemma** *(The Associated Measures are Finite)*
<a name="lmm:associated-measures-are-finite"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:hall-8.3} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and, for any $$\psi \in \mathbf{H}$$, let $$\mu_\psi$$ be the measure on $$\sigma(A)$$ of [**Definition**](#def:hall-8.6). Then
>
> $$
>     \mu_\psi(\sigma(A)) = \left\| \psi \right\|^2.
> $$
>
> In particular $$\mu_\psi(\sigma(A)) < \infty$$, i.e. $$\mu_\psi$$ is a finite measure on $$\sigma(A)$$.

**Proof**
Recall from [**Definition**](#def:hall-8.6) that for any $$f \in C^0(\sigma(A); \mathbb{R})$$ one has

$$
    Q_f(\psi) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) = \left< \psi, f(A)\psi \right>.
$$

The constant function $$f(\lambda) = 1$$ is continuous and real-valued on $$\sigma(A)$$, and so is an element of $$C^0(\sigma(A); \mathbb{R})$$. Furthermore, viewing $$f(\lambda) = 1$$ as the constant polynomial $$p(\lambda) = 1$$, the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3) gives $$f(A) = \mathbf{1}$$, the identity operator on $$\mathbf{H}$$. Hence, one has

$$
\begin{align}
    \mu_\psi(\sigma(A)) &\equiv \int_{\sigma(A)} d\mu_\psi(\lambda) \\
                        &= \int_{\sigma(A)} 1 \, d\mu_\psi(\lambda) \\
                        &= Q_1(\psi) \\
                        &= \left< \psi, \mathbf{1} \psi \right> \\
                        &= \left< \psi, \psi \right> \\
                        &= \left\| \psi \right\|^2,
\end{align}
$$

where the final line follows from the definition of the norm on $$\mathbf{H}$$. As $$\psi$$ is an element of the Hilbert space $$\mathbf{H}$$, its norm $$\left\| \psi \right\|$$ is a finite real number, and thus

$$
    \mu_\psi(\sigma(A)) = \left\| \psi \right\|^2 < \infty,
$$

i.e. $$\mu_\psi$$ is a finite measure on $$\sigma(A)$$, the desired result.$$\blacksquare$$

It turns out that $$Q_f$$ is a bounded quadratic form, as proven in the following [**Proposition**](#prpstn:hall-8.7)

> **Proposition** *(The Associated Quadratic Form is Bounded)*
<a name="prpstn:hall-8.7"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:F-class} -->
<!--  \uses{prpstn:F-bounded} -->
<!--  \uses{prpstn:F-closed-under-limits} -->
<!--  \uses{prpstn:F-contains-continuous} -->
<!--  \uses{prpstn:F-homogeneous} -->
<!--  \uses{prpstn:F-sesquilinear} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:bounded-sesquilinear-form} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:hall-a.62} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
> Let $$A$$ in $$\mathcal{B}(\mathbf{H})$$ be self-adjoint. For any bounded, measurable, complex-valued function $$f$$ on the spectrum $$\sigma(A)$$ of $$A$$, let $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ be its associated map
> 
> $$
>     Q_f(\psi) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda),
> $$ 
> 
> via [**Definition**](#def:hall-8.6). This map $$Q_f$$ is a bounded quadratic form.

**Proof**
Let $$\mathcal{F}$$ be as in [Definition *(The Class of Functions with Bounded Quadratic Form)*](#def:F-class). We verify the three hypotheses of [**Lemma** *(hall-prblm-8.3.3c)*](#lmm:hall-prblm-8.3.3c).

$$\mathcal{F}$$ is a complex vector space by [**Proposition** *(Homogeneity of the Quadratic Form of a Linear Combination)*](#prpstn:F-homogeneous), [**Proposition** *(The Associated Form of a Linear Combination is Sesquilinear)*](#prpstn:F-sesquilinear) and [**Proposition** *(The Quadratic Form of a Linear Combination is Bounded)*](#prpstn:F-bounded), which together show that $$Q_{\alpha f + \beta g}$$ is a bounded quadratic form whenever $$f,g \in \mathcal{F}$$. It contains $$C^0(\sigma(A);\mathbb{R})$$ by [**Proposition** *(The Class Contains the Continuous Functions)*](#prpstn:F-contains-continuous), and is closed under uniformly bounded pointwise limits by [**Proposition** *(The Class is Closed under Bounded Pointwise Limits)*](#prpstn:F-closed-under-limits).

Since $$\sigma(A)$$ is a compact metric measurable space by [**Lemma**](#lmm:spectrum-is-compact-metric-measurable), [**Lemma** *(hall-prblm-8.3.3c)*](#lmm:hall-prblm-8.3.3c) applies and gives that $$\mathcal{F}$$ is the set of *all* bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$. That is, $$Q_f$$ is a bounded quadratic form for every such $$f$$, as required.$$\blacksquare$$

> **Definition** *(The Class of Functions with Bounded Quadratic Form)*
<a name="def:F-class"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. Write $$\mathcal{F}$$ for the set of all bounded, Borel-measurable, complex-valued functions $$f$$ on $$\sigma(A)$$ such that the associated map $$Q_f$$ of [**Definition**](#def:hall-8.6) is a bounded quadratic form on $$\mathbf{H}$$.

> **Proposition** *(The Map $$f \mapsto Q_f$$ is Linear)*
<a name="prpstn:Q-is-linear"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:F-class} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:basic-integral-properties} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint, let $$f,g$$ be bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$, and let $$\alpha,\beta \in \mathbb{C}$$. Then
>
> $$
>     Q_{\alpha f + \beta g} = \alpha Q_f + \beta Q_g.
> $$

**Proof**
For any $$\psi \in \mathbf{H}$$, using the [definition of $$Q_f$$](#def:hall-8.6) and linearity of the integral in the integrand — part 2 of [**Proposition** *(Basic Properties of the Integral, and Integration over a Subset)*](#prpstn:basic-integral-properties) —

$$
\begin{align}
    Q_{\alpha f + \beta g}(\psi) &= \int_{\sigma(A)} (\alpha f + \beta g)(\lambda) \, d\mu_\psi(\lambda) \\
                                 &= \int_{\sigma(A)} \alpha f(\lambda) + \beta g(\lambda) \, d\mu_\psi(\lambda) \\
                                 &= \alpha \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) + \beta \int_{\sigma(A)} g(\lambda) \, d\mu_\psi(\lambda) \\
                                 &= \alpha Q_f(\psi) + \beta Q_g(\psi).
\end{align}
$$

As $$\psi$$ was arbitrary, $$Q_{\alpha f + \beta g} = \alpha Q_f + \beta Q_g$$.$$\blacksquare$$

> **Proposition** *(Homogeneity of the Quadratic Form of a Linear Combination)*
<a name="prpstn:F-homogeneous"></a>
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:Q-is-linear} -->
<!--  \uses{def:F-class} -->
<!--  \uses{def:bounded-quadratic-form} -->
> Let $$f,g \in \mathcal{F}$$ and $$\alpha,\beta \in \mathbb{C}$$, with $$\mathcal{F}$$ as in [Definition (The Class of Functions with Bounded Quadratic Form)](#def:F-class). Then $$Q_{\alpha f + \beta g}(\lambda\psi) = \lvert \lambda \rvert^2 Q_{\alpha f + \beta g}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.

**Proof**
$$Q_{\alpha f + \beta g}(\lambda\psi) = \lvert\lambda \rvert^2 Q_{\alpha f + \beta g}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.

This follows from the fact that $$f$$ and $$g$$ are in $$\mathcal{F}$$ and thus $$Q_f$$ and $$Q_g$$ are bounded quadratic forms. Explicitly,

$$
\begin{align}
    Q_{\alpha f + \beta g}(\lambda\psi) &= \alpha Q_f(\lambda\psi) + \beta Q_g(\lambda\psi) \\
                                        &= \lvert \lambda \rvert^2 \alpha Q_f(\psi) + \lvert \lambda \rvert^2 \beta Q_g(\psi) \\
                                        &= \lvert \lambda \rvert^2 \left( \alpha Q_f(\psi) + \beta Q_g(\psi) \right) \\
                                        &= \lvert \lambda \rvert^2 Q_{\alpha f + \beta g}(\psi),
\end{align}
$$

which implies

$$
    Q_{\alpha f + \beta g}(\lambda\psi) = \lvert\lambda \rvert^2 Q_{\alpha f + \beta g}(\psi),
$$

the first desired result.
$$\blacksquare$$

> **Proposition** *(The Associated Form of a Linear Combination is Sesquilinear)*
<a name="prpstn:F-sesquilinear"></a>
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:Q-is-linear} -->
<!--  \uses{def:F-class} -->
<!--  \uses{def:bounded-sesquilinear-form} -->
<!--  \uses{prpstn:F-homogeneous} -->
<!--  \uses{lmm:sesquilinear-linear-combination} -->
> With $$f,g,\alpha,\beta$$ as in [**Proposition** *(Homogeneity of the Quadratic Form of a Linear Combination)*](#prpstn:F-homogeneous), the map $$L_{\alpha f + \beta g} : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by
>
> $$
> \begin{align}
>     L_{\alpha f + \beta g}(\phi, \psi) &\equiv \frac{1}{2} \left[ Q_{\alpha f + \beta g}(\phi + \psi) - Q_{\alpha f + \beta g}(\phi) - Q_{\alpha f + \beta g}(\psi) \right] \\
>                                        &-\frac{i}{2} \left[ Q_{\alpha f + \beta g}(\phi + i\psi) - Q_{\alpha f + \beta g}(\phi) - Q_{\alpha f + \beta g}(i\psi) \right]
> \end{align}
> $$
>
> is a sesquilinear form on $$\mathbf{H}$$.

**Proof**
the map $$L_{\alpha f + \beta g} : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
\begin{align}
    L_{\alpha f + \beta g}(\phi, \psi) &\equiv \frac{1}{2} \left[ Q_{\alpha f + \beta g}(\phi + \psi) - Q_{\alpha f + \beta g}(\phi) - Q_{\alpha f + \beta g}(\psi) \right] \\
                                       &-\frac{i}{2} \left[ Q_{\alpha f + \beta g}(\phi + i\psi) - Q_{\alpha f + \beta g}(\phi) - Q_{\alpha f + \beta g}(i\psi) \right]
\end{align}
$$

is a sesquilinear form on $$\mathbf{H}$$.

Again this follows from the fact that $$f$$ and $$g$$ are in $$\mathcal{F}$$ and thus $$Q_f$$ and $$Q_g$$ are bounded quadratic forms. Explicitly, linearity implies

$$
   L_{\alpha f + \beta g}(\phi, \psi) = \alpha L_f(\phi, \psi) + \beta L_g(\phi, \psi),
$$

with the obvious definitions of $$L_f$$ in terms of $$Q_f$$ and $$L_g$$ in terms of $$Q_g$$.

Now as $$Q_f$$ and $$Q_g$$ are bounded quadratic forms, $$L_f$$ and $$L_g$$ are sesquilinear forms. Hence [**Lemma** *(Linear Combinations of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-linear-combination) gives that $$L_{\alpha f + \beta g} = \alpha L_f + \beta L_g$$ is a sesquilinear form, as required.
$$\blacksquare$$

> **Proposition** *(The Quadratic Form of a Linear Combination is Bounded)*
<a name="prpstn:F-bounded"></a>
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:Q-is-linear} -->
<!--  \uses{def:F-class} -->
<!--  \uses{prpstn:F-homogeneous} -->
<!--  \uses{prpstn:F-sesquilinear} -->
> With $$f,g,\alpha,\beta$$ as in [**Proposition** *(Homogeneity of the Quadratic Form of a Linear Combination)*](#prpstn:F-homogeneous), there is a constant $$C \in \mathbb{R}$$ with $$\lvert Q_{\alpha f + \beta g}(\phi) \rvert \le C \|\phi\|^2$$ for all $$\phi \in \mathbf{H}$$. Consequently $$\mathcal{F}$$ is a complex vector space.

**Proof**
there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_{\alpha f + \beta g}(\phi) \rvert \le C \|\phi\|^2,
$$

where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$. 

Again this follows from the fact that $$f$$ and $$g$$ are in $$\mathcal{F}$$ and thus $$Q_f$$ and $$Q_g$$ are bounded quadratic forms. Explicitly, the norm definition and linearity imply


$$
\begin{align}
    \lvert Q_{\alpha f + \beta g}(\phi) \rvert &=   \lvert \alpha Q_f(\phi) + \beta Q_g(\phi) \rvert \\
                                               &\le \lvert \alpha Q_f(\phi) \rvert + \lvert \beta Q_g(\phi) \rvert \\
                                               &=   \lvert \alpha \rvert \, \lvert Q_f(\phi) \rvert + \lvert \beta \rvert \, \lvert Q_g(\phi) \rvert \\
                                               &\le C_f \lvert \alpha \rvert \, \| \phi \|^2 + C_g \lvert \beta \rvert \, \| \phi \|^2 \\
                                               &=   \left( C_f \lvert \alpha \rvert + C_g \lvert \beta \rvert \right) \| \phi \|^2 \\
                                               &=   C \| \phi \|^2, 
\end{align}
$$

where we have used the fact that $$Q_f$$ and $$Q_g$$ are bounded quadratic forms to infer that there exist constants $$C_f$$ and $$C_g$$ in $$\mathbb{R}$$ such that

$$
\begin{align}
    \lvert Q_f(\phi) \rvert &\le C_f \| \phi \|^2 \\
    \lvert Q_g(\phi) \rvert &\le C_g \| \phi \|^2
\end{align}
$$

along with the definition

$$
    C \equiv C_f \lvert \alpha \rvert + C_g \lvert \beta \rvert.
$$

This implies

$$
    \lvert Q_{\alpha f + \beta g}(\phi) \rvert \le C \| \phi \|^2,
$$

the final desired result. This completes the proof that $$Q_{\alpha f + \beta g}$$ is a bounded quadratic form. This in turn implies that $$\alpha f + \beta g$$ is an element of $$\mathcal{F}$$ which in turn implies $$\mathcal{F}$$ is a vector space.
$$\blacksquare$$

> **Proposition** *(The Class Contains the Continuous Functions)*
<a name="prpstn:F-contains-continuous"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{def:F-class} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:hall-a.62} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mathcal{F}$$ as in [Definition (The Class of Functions with Bounded Quadratic Form)](#def:F-class), $$C^0(\sigma(A); \mathbb{R}) \subseteq \mathcal{F}$$.

**Proof**
$$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$\mathcal{F}$$.

By definition $$\mathcal{F}$$ is a subset of the set of bounded, Borel-measurable, complex-valued functions on the spectrum $$\sigma(A)$$ of $$A$$, where $$A$$ is self-adjoint. So, let us first prove that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of this set of bounded, Borel-measurable, complex-valued functions.

Recall that by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a non-empty, compact metric measurable space, and is a subset of $$\mathbb{R} \subset \mathbb{C}$$. In addition, the [**Boundedness Theorem**](#thrm:boundedness-theorem) implies that any element of $$C^0(\sigma(A); \mathbb{R})$$ is bounded.

As $$C^0(\sigma(A); \mathbb{R})$$ is continuous, for any $$f$$ in $$C^0(\sigma(A); \mathbb{R})$$ the pre-image of any open set in $$\mathbb{R}$$ is open in $$\sigma(A)$$. As $$\mathbb{R} \subset \mathbb{C}$$ has the subset topology, for any $$f$$ in $$C^0(\sigma(A); \mathbb{R})$$ the pre-image of any open set in $$\mathbb{C}$$ is open in $$\sigma(A)$$. Hence, any element of $$C^0(\sigma(A); \mathbb{R})$$ is Borel-measurable when considered as a complex-valued function on the spectrum $$\sigma(A)$$ of $$A$$.

So with that we have proven that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of the set of bounded, Borel-measurable, complex-valued functions on the spectrum $$\sigma(A)$$ of $$A$$.

The final step to prove $$C^0(\sigma(A); \mathbb{R}) \subset \mathcal{F}$$ is to prove that any $$f$$ in $$C^0(\sigma(A); \mathbb{R})$$ results in a bounded quadratic form $$Q_f$$.

Now tracing definitions we find that for any $$f$$ in $$C^0(\sigma(A); \mathbb{R})$$ one has

$$
    Q_f(\psi) = \left< \psi, f(A)\psi \right>,
$$

where bounded operator $$f(A)$$ is the image of $$f$$ under the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3). Thus as a result of [**Proposition**](#prpstn:hall-a.62)

> **Proposition** *(The Quadratic Form of a Bounded Operator)*
<a name="prpstn:hall-a.62"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:bounded-sesquilinear-form} -->
<!-- Hall states this as Example A.62; we record it as a proposition since later results cite it. -->
> If $$A \in \mathcal{B}(\mathbf{H})$$, one can construct a bounded quadratic form $$Q_A$$ on $$\mathbf{H}$$ by setting
> 
> $$
>     Q_A(\psi) \equiv \left< \psi, A\psi \right>
> $$
> 
> for all $$\psi$$ in $$\mathbf{H}$$. The associated sesquilinear form $$L_A$$ is then given by
> 
> $$
>     L_A(\phi, \psi) = \left< \phi, A\psi \right>
> $$
> 
> for all $$\phi$$ and $$\psi$$ in $$\mathbf{H}$$.

From this we can conclude that $$Q_f(\psi) = \left< \psi, f(A)\psi \right>$$ is a bounded quadratic form, the final desired result required to prove that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$\mathcal{F}$$.

Our next step is to prove that $$\mathcal{F}$$ is closed under uniformly bounded pointwise limits. This essentially is a result of the fact that $$Q_f(\psi)$$ is continuous with respect to such limits.

Explicitly, consider a sequence $$\{ f_i \}_{i \in \mathbb{N}}$$ of elements in $$\mathcal{F}$$ that are uniformly bounded, i.e. there exists a real-valued constant $$M$$ such that

$$
    \lvert f_i(\lambda) \rvert \le M
$$

for all $$i \in \mathbb{N}$$ and all $$\lambda \in \sigma(A)$$, and that converge pointwise, i.e. there exists a map $$f : \sigma(A) \rightarrow \mathbb{C}$$ that satisfies

$$
    \lim\limits_{i \rightarrow \infty} f_i(\lambda) = f(\lambda)
$$

pointwise for each $$\lambda \in \sigma(A)$$ relative to the standard norm $$\lvert \cdot \rvert$$ on $$\mathbb{C}$$. Our goal is then to prove that $$f$$ is in $$\mathcal{F}$$.

As $$\mathcal{F}$$ is a subset of the set of all bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$, our first task is to prove that $$f$$ is a bounded, Borel-measurable, complex-valued function.

Each $$f_i$$ is an element of $$\mathcal{F}$$, and thus a bounded, Borel-measurable, complex-valued function on $$\sigma(A)$$. By [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a compact metric measurable space. Hence, identifying $$X$$ with $$\sigma(A)$$, the sequence $$\{ f_i \}_{i \in \mathbb{N}}$$ and its pointwise limit $$f$$ satisfy the hypotheses of [**Lemma** *(Pointwise Limits of Uniformly Bounded, Borel-Measurable Functions)*](#lmm:pointwise-limits-of-borel-measurable-functions). That [**Lemma**](#lmm:pointwise-limits-of-borel-measurable-functions) directly implies that $$f$$ is bounded and Borel-measurable, the desired result.
$$\blacksquare$$

> **Proposition** *(The Class is Closed under Bounded Pointwise Limits)*
<a name="prpstn:F-closed-under-limits"></a>
<!--  \uses{def:hall-8.6} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:F-class} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
<!--  \uses{prpstn:F-bounded} -->
<!--  \uses{lmm:sesquilinear-pointwise-limit} -->
> With $$\mathcal{F}$$ as in [Definition (The Class of Functions with Bounded Quadratic Form)](#def:F-class), if $$\{f_n\}$$ is a sequence in $$\mathcal{F}$$, uniformly bounded and converging pointwise to $$f$$, then $$f \in \mathcal{F}$$.

**Proof**
$$f$$ is in $$\mathcal{F}$$. The definition of $$\mathcal{F}$$ implies that this is equivalent to proving that $$Q_f$$ is a bounded quadratic form.

To prove that $$Q_f$$ is a bounded quadratic form we must prove that

1. $$Q_f(\lambda\psi) = \lvert\lambda \rvert^2 Q_f(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.
2. The map $$L_f : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by

   $$
   \begin{align}
       L_f(\phi, \psi) &\equiv \frac{1}{2} \left[ Q_f(\phi + \psi) - Q_f(\phi) - Q_f(\psi) \right] \\
                                                       &-\frac{i}{2} \left[ Q_f(\phi + i\psi) - Q_f(\phi) - Q_f(i\psi) \right]
   \end{align}
   $$

   is a sesquilinear form on $$\mathbf{H}$$.

3. That there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

   $$
       \lvert Q_f(\phi) \rvert \le C \|\phi\|^2,
   $$

   where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

The key "engine" in proving the $$Q_f$$ is a bounded quadratic form is the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem)

> **Theorem** *(Bounded Convergence Theorem)*
<a name="thrm:bounded-convergence-theorem"></a>
> Let $$X$$ be a set with finite measure $$\mu(X) < \infty$$ and $$\{ f_i \}_{i \in \mathbb{N}}$$ a sequence of uniformly bounded, complex valued functions on $$X$$ that converge pointwise to $$f$$, then
> 
> $$
>     \int_X f \, d\mu = \lim\limits_{i \rightarrow \infty} \int_X f_i \, d\mu.
> $$

To apply this to the sequence $$\{ f_i \}_{i \in \mathbb{N}}$$ at hand in order to prove

$$
    \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) = \lim\limits_{i \rightarrow \infty} \int_{\sigma(A)} f_i(\lambda) \, d\mu_\psi(\lambda)
$$

we must prove that

$$
    \mu_\psi(\sigma(A)) \equiv \int_{\sigma(A)} d\mu_\psi(\lambda) < \infty.
$$

This is precisely the content of [**Lemma** *(The Associated Measures are Finite)*](#lmm:associated-measures-are-finite), which gives $$\mu_\psi(\sigma(A)) = \left\| \psi \right\|^2 < \infty$$. In other words $$\sigma(A)$$ has a finite measure $$\mu_\psi(\sigma(A))$$.

That established we can apply the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem) to conclude that

$$
    \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) = \lim\limits_{i \rightarrow \infty} \int_{\sigma(A)} f_i(\lambda) \, d\mu_\psi(\lambda).
$$

This implies

$$
\begin{align}
    Q_f(\psi) &= \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) \\
              &= \lim\limits_{i \rightarrow \infty} \int_{\sigma(A)} f_i(\lambda) \, d\mu_\psi(\lambda \\
              &= \lim\limits_{i \rightarrow \infty} Q_{f_i}(\psi),
\end{align}
$$

and it is this relation

$$
    Q_f(\psi) = \lim\limits_{i \rightarrow \infty} Q_{f_i}(\psi)
$$

that will allow us to prove that $$Q_f$$ is a bounded quadratic form.

To wit, first let us prove $$Q_f(\lambda\psi) = \lvert\lambda \rvert^2 Q_f(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.

This follows from our previous result along with the fact that the $$Q_{f_i}(\psi)$$ are bounded quadratic forms. We have

$$
\begin{align}
    Q_f(\lambda\psi) &= \lim\limits_{i \rightarrow \infty} Q_{f_i}(\lambda\psi) \\
                     &= \lim\limits_{i \rightarrow \infty} \lvert\lambda \rvert^2 Q_{f_i}(\psi) \\
                     &= \lvert\lambda \rvert^2 \left( \lim\limits_{i \rightarrow \infty} Q_{f_i}(\psi) \right) \\
                     &= \lvert\lambda \rvert^2 Q_f(\psi),
\end{align}
$$

which is the desired result.

Now let us prove the map $$L_f : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by
   
$$
\begin{align}
    L_f(\phi, \psi) &\equiv \frac{1}{2} \left[ Q_f(\phi + \psi) - Q_f(\phi) - Q_f(\psi) \right] \\
                                                    &-\frac{i}{2} \left[ Q_f(\phi + i\psi) - Q_f(\phi) - Q_f(i\psi) \right]
\end{align}
$$

is a sesquilinear form on $$\mathbf{H}$$.

Linearity implies

$$
    L_f(\phi, \psi) = \lim\limits_{i \rightarrow \infty} L_{f_i}(\phi, \psi).
$$

As each $$L_{f_i}$$ is a sesquilinear form and this limit exists for all $$\phi,\psi$$, [**Lemma** *(Pointwise Limits of Sesquilinear Forms are Sesquilinear)*](#lmm:sesquilinear-pointwise-limit) gives that $$L_f$$ is a sesquilinear form on $$\mathbf{H}$$, as required.

Finally, let us prove that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    \lvert Q_f(\phi) \rvert \le C \|\phi\|^2,
$$

where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$. 

This follows from [**Lemma** *(The Associated Measures are Finite)*](#lmm:associated-measures-are-finite), which gives

$$
   \mu_\phi(\sigma(A)) = \|\phi\|^2
$$

for any $$\phi \in \mathbf{H}$$, together with the fact that $$f$$ is bounded. Together these imply

$$
\begin{align}
    \lvert Q_f(\phi) \rvert &=   \left\lvert \int_{\sigma(A)} f(\lambda) \, d\mu_\phi(\lambda) \right\rvert \\
                            &\le \int_{\sigma(A)} \left\lvert f(\lambda) \right\rvert \, d\mu_\phi(\lambda) \\
                            &\le \int_{\sigma(A)} \left( \sup\limits_{\lambda' \in \sigma(A)} \left\lvert f(\lambda') \right\rvert \right) \, d\mu_\phi(\lambda) \\
                            &=   \left( \sup\limits_{\lambda' \in \sigma(A)} \left\lvert f(\lambda') \right\rvert \right) \int_{\sigma(A)} \, d\mu_\phi(\lambda) \\
                            &=   \sup\limits_{\lambda' \in \sigma(A)} \left\lvert f(\lambda') \right\rvert \|\phi\|^2 \\
\end{align}
$$

which gives the desired result, there exists a real constant

$$
    C \equiv \sup\limits_{\lambda' \in \sigma(A)} \left\lvert f(\lambda') \right\rvert
$$

such that for all $$\phi$$ in $$\mathbf{H}$$ one has

$$
    \lvert Q_f(\phi) \rvert \le C \|\phi\|^2.
$$

This completes our proof that $$f$$ is in $$\mathcal{F}$$ and thus our proof that $$\mathcal{F}$$ is closed under uniformly bounded pointwise limits.

Finally to complete the proof of [**Proposition**](#prpstn:hall-8.7) we will prove that $$\mathcal{F}$$ is the space of all bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$.
$$\blacksquare$$

The next lemma refers to an algebra of sets and to the Archimedean Property; we state both first.

> **Definition** *(Algebra of Sets)*
<a name="def:algebra-of-sets"></a>
> Given a set $$S$$ and a set of subsets $$\mathcal{S}$$ of $$S$$, the set of subsets $$\mathcal{S}$$ is an *algebra of sets* if it
> 
> 1. Contains the empty set, i.e. $$\emptyset \in \mathcal{S}$$.
> 2. Closed under complements, i.e. if $$s \in \mathcal{S}$$, then $$(S \backslash s) \in \mathcal{S}$$.
> 3. Closed under finite union, i.e. if $$r,s \in \mathcal{S}$$, then $$s \cup r \in \mathcal{S}$$.

> **Theorem** *(Archimedean Property)*
<a name="thrm:archimedean-property"></a>
> For any real number $$\epsilon > 0$$ there exists a natural number $$N \ge 1$$ such that for all natural numbers $$n \ge N$$ one has $$1/n < \epsilon$$. (The requirement $$N \ge 1$$ matters because $$\mathbb{N}$$ includes $$0$$ here, and $$1/n$$ is undefined at $$n = 0$$.)

Our proof of this result requires that we first prove some "utility" lemmas as stepping stones. The first of these "utility" lemmas is the following:

> **Lemma** *(The Class $$\mathcal{L}_0$$ is an Algebra Containing the Open Sets)*
<a name="lmm:hall-prblm-8.3.3a"></a>
<!--  \uses{def:L0-class} -->
<!--  \uses{prpstn:L0-complement} -->
<!--  \uses{prpstn:L0-contains-closed} -->
<!--  \uses{prpstn:L0-contains-empty} -->
<!--  \uses{prpstn:L0-union} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:algebra-of-sets} -->
<!--  \uses{thrm:archimedean-property} -->
<!--  \uses{def:bump-function} -->
<!--  \uses{thrm:existence-of-bump-functions} -->
> Let $$X$$ be a compact metric measurable space with a measure $$\mu_X$$. Let $$\mathcal{L}_0$$ be as in [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class) below: the measurable subsets $$E \subseteq X$$ whose indicator function $$1_E$$ is the *pointwise* limit of a uniformly bounded sequence of continuous functions. Then $$\mathcal{L}_0$$ is an algebra and contains all open sets in $$X$$.

**Proof**
That $$\mathcal{L}_0$$ is an algebra of sets is the conjunction of the three conditions of [**Definition** *(Algebra of Sets)*](#def:algebra-of-sets): it contains $$\emptyset$$ by [**Proposition** *(The Empty Set Lies in $$\mathcal{L}_0$$)*](#prpstn:L0-contains-empty), is closed under complements by [**Proposition** *($$\mathcal{L}_0$$ is Closed under Complements)*](#prpstn:L0-complement), and is closed under finite unions by [**Proposition** *($$\mathcal{L}_0$$ is Closed under Finite Unions)*](#prpstn:L0-union).

For the open sets: every closed subset of $$X$$ lies in $$\mathcal{L}_0$$ by [**Proposition** *($$\mathcal{L}_0$$ Contains all Closed Sets)*](#prpstn:L0-contains-closed). If $$U \subseteq X$$ is open then $$U^c$$ is closed, hence $$U^c \in \mathcal{L}_0$$, and so $$U = (U^c)^c \in \mathcal{L}_0$$ by closure under complements. Thus $$\mathcal{L}_0$$ contains all open sets in $$X$$, as required.$$\blacksquare$$

> **Definition** *(The Class $$\mathcal{L}_0$$)*
<a name="def:L0-class"></a>
<!--  \uses{def:indicator-function} -->
> Let $$X$$ be a compact metric measurable space. Write $$\mathcal{L}_0$$ for the set of all measurable subsets $$E \subseteq X$$ whose indicator function $$1_E$$ is the *pointwise* limit of a uniformly bounded sequence of continuous functions: that is, there are $$\{f_n\} \subset C^0(X;\mathbb{R})$$ and a constant $$C$$ with $$\lvert f_n(x) \rvert \le C$$ for all $$n$$ and all $$x$$, such that **for each $$x \in X$$** and each $$\epsilon > 0$$ there is an $$N$$ — depending on $$x$$ as well as on $$\epsilon$$ — with $$\lvert f_n(x) - 1_E(x) \rvert < \epsilon$$ for all $$n \ge N$$.
>
> The dependence of $$N$$ on $$x$$ is essential: uniform convergence of continuous functions would force $$1_E$$ to be continuous, which holds only for clopen $$E$$ and would make [**Lemma** *(hall-prblm-8.3.3a)*](#lmm:hall-prblm-8.3.3a) false.

> **Proposition** *(The Empty Set Lies in $$\mathcal{L}_0$$)*
<a name="prpstn:L0-contains-empty"></a>
<!--  \uses{thrm:archimedean-property} -->
<!--  \uses{def:L0-class} -->
> With $$\mathcal{L}_0$$ as in [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class), $$\emptyset \in \mathcal{L}_0$$.

**Proof**
$$\emptyset \in \mathcal{L}_0$$. To prove this we must prove **Property 1.1:** that $$\emptyset$$ is measurable and **Property 1.2:** that $$1_\emptyset$$ is the pointwise limit of a sequence of uniformly bounded continuous functions.

**Property 1.1:** Let us first prove that $$\emptyset$$ is measurable.

The definition of a $$\sigma$$-algebra requires that the empty set $$\emptyset$$ is an element of any $$\sigma$$-algebra, in particular the empty set $$\emptyset$$ is an element of the $$\sigma$$-algebra of $$X$$.

The definition of a measure implies that $$\mu_X$$ maps the $$\sigma$$-algebra of $$X$$ to the extended real numbers.

These facts together imply that $$\mu_X(\emptyset)$$ is defined, which is none other than the desired result, $$\emptyset$$ is measurable.

**Property 1.2:** Let us now prove that $$1_\emptyset$$ is the pointwise limit of a sequence of uniformly bounded continuous functions.

To prove that $$1_\emptyset$$ is the pointwise limit of a sequence of uniformly bounded continuous functions, we must prove that **Property 1.2.1:** there exists a sequence of function $$\{ f_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$C$$ such that

$$
    \lvert f_n(x) \rvert \le C
$$

for all $$x \in X$$ and all $$n \in \mathbb{N}$$; and **Property 1.2.2:** for any real number $$\epsilon > 0$$ there exist a natural number $$N$$ such that for all $$n \ge N$$ one has

$$
    \lvert f_n(x) - 1_\emptyset(x) \rvert < \epsilon
$$

for all $$x \in X$$.

Below we will prove that the set of constant functions

$$
    f_n(x) \equiv \frac{1}{n + 1}
$$

on $$X$$ has all these desired properties.

**Property 1.2.1:** Let us next prove that the sequence of functions $$\{ f_n \}_{n \in \mathbb{N}}$$ above is in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$C$$ exists such that

$$
    \lvert f_n(x) \rvert \le C
$$

for all $$x \in X$$ and all $$n \in \mathbb{N}$$.

We begin with the obvious result that the constant functions

$$
    f_n(x) \equiv \frac{1}{n + 1}
$$

on $$X$$ are elements of $$C^0(X; \mathbb{R})$$.

Also a moment's thought reveals that if we take $$C = 1$$, then we have

$$
    \lvert f_n(x) \rvert = \left\lvert \frac{1}{n + 1} \right\rvert \le C
$$

for all $$x \in X$$ and all $$n \in \mathbb{N}$$. Hence, the sequence satisfies all the desired properties required by **Property 1.2.1**.

**Property 1.2.2:** Let us now prove that for each $$x \in X$$ and any real number $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$n \ge N$$ one has

$$
    \lvert f_n(x) - 1_\emptyset(x) \rvert < \epsilon.
$$

Recall that the definition of an indicator function implies that

$$
    1_\emptyset(x) = 0
$$

for all $$x \in X$$. Hence, we must prove that for each $$x \in X$$ and any real number $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$n \ge N$$ one has

$$
    \lvert f_n(x) \rvert < \epsilon.
$$ As $$f_n(x) \equiv 1 / (n + 1)$$, this is true as a result of the [**Archimedean Property**](#thrm:archimedean-property). Hence, the sequence $$f_n(x) \equiv 1 / (n + 1)$$ satisfies all the desired properties required by **Property 1.2.2**. This completes the proof.
$$\blacksquare$$

> **Proposition** *($$\mathcal{L}_0$$ is Closed under Complements)*
<a name="prpstn:L0-complement"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:L0-class} -->
> With $$\mathcal{L}_0$$ as in [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class), if $$E \in \mathcal{L}_0$$ then $$E^c \in \mathcal{L}_0$$.

**Proof**
$$\mathcal{L}_0$$ is closed under complements. In other words if $$E \in \mathcal{L}_0$$, then $$E^c \equiv (X \backslash E) \in \mathcal{L}_0$$. To prove this we must prove **Property 2.1:** that $$E^c$$ is measurable, and **Property 2.2:** that $$1_{E^c}$$ is a pointwise limit of a sequence of uniformly bounded continuous functions.

**Property 2.1:** Let us prove that if $$E \in \mathcal{L}_0$$, then $$E^c$$ is measurable

By hypothesis $$E \in \mathcal{L}_0$$. The definition of $$\mathcal{L}_0$$ then implies that $$E$$ is measurable and thus in the $$\sigma$$-algebra of $$X$$. As $$E$$ is in the $$\sigma$$-algebra of $$X$$, the $$\sigma$$-algebra definition implies that $$E^c$$ is also in the $$\sigma$$-algebra of $$X$$. Hence, the definition of a measure and the fact that we have a measure $$\mu$$ on $$X$$ imply that $$E^c$$ is measurable, the desired result. 

**Property 2.2:** Now let us prove that $$1_{E^c}$$ is a pointwise limit of a sequence of uniformly bounded continuous functions.

By hypothesis $$E \in \mathcal{L}_0$$. Hence, (1) the definition of $$\mathcal{L}_0$$ implies that there exists a sequence of functions $$\{ f_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$C$$ such that

$$
    \left\lvert f_n(x) \right\rvert \le C
$$

for all $$x \in X$$ and $$n \in \mathbb{N}$$ and (2) for each $$x \in X$$ and every real number $$\epsilon > 0$$ there exists a natural number $$N$$ (depending on $$x$$ and $$\epsilon$$) such that for all $$n \ge N$$ one has

$$
    \left\lvert f_n(x) - 1_E(x) \right\rvert < \epsilon.
$$

Let us define a sequence of functions $$\{ g_n \}_{n \in \mathbb{N}}$$ on $$X$$ by

$$
   g_n(x) \equiv (1 - f_n(x)). 
$$

Obviously, the $$g_n$$ are in $$C^0(X; \mathbb{R})$$. The definition of the $$g_n$$, the properties of the $$f_n$$, and the norm definition imply

$$
\begin{align}
    \left\lvert g_n(x) \right\rvert &=   \left\lvert 1 - f_n(x) \right\rvert \\
                          &\le \left\lvert 1 \right\rvert + \left\lvert f_n(x) \right\rvert \\
                          &\le 1 + C \\
                          &=   D,  \\
\end{align}
$$

where we have made the definition $$D \equiv 1 + C$$. Thus we have proven that there exists a sequence of functions $$\{ g_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$D$$ such that

$$
    \left\lvert g_n(x) \right\rvert \le D
$$

for all $$x \in X$$ and all $$n \in \mathbb{N}$$. In other words our sequence $$\{ g_n \}_{n \in \mathbb{N}}$$ is a sequence of uniformly bounded continuous functions.

Let $$\epsilon > 0$$ be an arbitrary real number and consider if we can find a natural number $$N$$ such that

$$
    \left\lvert g_n(x) - 1_{E^c}(x) \right\rvert < \epsilon
$$

for all $$x \in X$$ and all $$n \ge N$$.

To this end for an arbitrary $$g_n$$ and arbitrary $$x \in X$$ consider

$$
\begin{align}
    \left\lvert g_n(x) - 1_{E^c}(x) \right\rvert &= \left\lvert (1 - f_n(x)) - 1_{E^c}(x) \right\rvert \\
                                       &= \left\lvert (1 - f_n(x)) - (1 - 1_{E}(x)) \right\rvert \\
                                       &= \left\lvert 1_{E}(x) - f_n(x) \right\rvert \\
                                       &= \left\lvert f_n(x) - 1_{E}(x) \right\rvert,
\end{align}
$$

where in the second line we used $$1_{E^c}(x) = 1 - 1_{E}(x)$$ which follows easily from the definitions of the indicator function and the sets $$E$$ and $$E^c$$.

However, as $$E \in \mathcal{L}_0$$ the definition of $$\mathcal{L}_0$$ implies that for each $$x \in X$$ and each real-valued number $$\epsilon > 0$$ there exists a natural number $$N$$ (depending on $$x$$ and $$\epsilon$$) such that for all $$n \ge N$$ one has

$$
    \left\lvert f_n(x) - 1_{E}(x) \right\rvert < \epsilon.
$$

However, as we have proven that

$$
    \left\lvert g_n(x) - 1_{E^c}(x) \right\rvert = \left\lvert f_n(x) - 1_{E}(x) \right\rvert
$$

for an arbitrary $$n \in \mathbb{N}$$ and arbitrary $$x \in X$$, then it follows that for each $$x \in X$$ and each real-valued number $$\epsilon > 0$$ there exists a natural number $$N$$ (the same one supplied by the hypothesis at that $$x$$) such that for all $$n \ge N$$ one has

$$
    \left\lvert g_n(x) - 1_{E^c}(x) \right\rvert < \epsilon.
$$

Thus with this we have proven that $$1_{E^c}$$ is the pointwise limit of a sequence of uniformly bounded functions, the desired **Property 2.2** result.

Having proven both parts we conclude that $$\mathcal{L}_0$$ is closed under complements, the desired result.
$$\blacksquare$$

> **Proposition** *($$\mathcal{L}_0$$ is Closed under Finite Unions)*
<a name="prpstn:L0-union"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:L0-class} -->
> With $$\mathcal{L}_0$$ as in [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class), if $$E_1, E_2 \in \mathcal{L}_0$$ then $$E_1 \cup E_2 \in \mathcal{L}_0$$.

**Proof**
$$\mathcal{L}_0$$ is closed under finite union, i.e. if $$E_1,E_2 \in \mathcal{L}_0$$, then $$E_1 \cup E_2 \in \mathcal{L}_0$$. Proving this is tantamount to proving **Property 3.1:** that $$E_1 \cup E_2$$ is measurable and **Property 3.2:** that $$1_{E_1 \cup E_2}$$ is a pointwise limit of a sequence of uniformly bounded continuous functions.

**Property 3.1:** Let us next prove that $$E_1 \cup E_2$$ is measurable.

By hypothesis $$E_1,E_2 \in \mathcal{L}_0$$. The definition of $$\mathcal{L}_0$$ implies that both $$E_1$$ and $$E_2$$ are measurable and thus in the $$\sigma$$-algebra of $$X$$. As $$E_1$$ and $$E_2$$ are in the $$\sigma$$-algebra of $$X$$, the $$\sigma$$-algebra definition implies that $$E_1 \cup E_2$$ is also in the $$\sigma$$-algebra of $$X$$. Hence, the definition of a measure and the fact that we have a measure $$\mu$$ on $$X$$ imply that $$E_1 \cup E_2$$ is also measurable, the desired result.

**Property 3.2:** Finally let us prove that $$1_{E_1 \cup E_2}$$ is a pointwise limit of a sequence of uniformly bounded continuous functions.

By hypothesis $$E_1,E_2 \in \mathcal{L}_0$$. The definition of $$\mathcal{L}_0$$ implies that (1) there for each $$E_i$$ exists a sequence $$\{ f^i_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$C_i$$ such that

$$
    \left\lvert f^i_n(x) \right\rvert \le C_i
$$

for all $$n \in \mathbb{N}$$ and all $$x \in X$$ and (2) for each $$E_i$$, each $$x \in X$$ and any real number $$\epsilon_i > 0$$ there exists a natural number $$N_i$$ (depending on $$x$$ and $$\epsilon_i$$) such that for all $$n \ge N_i$$ we have

$$
    \left\lvert f^i_n(x) - 1_{E_i}(x) \right\rvert < \epsilon_i.
$$

With the easily verifiable fact

$$
    1_{E_1 \cup E_2}(x) = 1_{E_1}(x) + 1_{E_2}(x) - 1_{E_1}(x) 1_{E_2}(x)
$$

in mind, let us define the sequence of functions $$\{ g_n \}_{n \in \mathbb{N}}$$ on $$X$$ by

$$
    g_n(x) = f^1_n(x) + f^2_n(x) - f^1_n(x) f^2_n(x).
$$

As the $$f^i_n$$ are in $$C^0(X; \mathbb{R})$$, it obviously follows that the $$g_n$$ are also in $$C^0(X; \mathbb{R})$$.

The norm definition along with the fact that the $$f^i_n$$ are bounded implies

$$
\begin{align}
    \left\lvert g_n(x) \right\rvert &=   \left\lvert f^1_n(x) + f^2_n(x) - f^1_n(x) f^2_n(x) \right\rvert \\
                          &\le \left\lvert f^1_n(x) \right\rvert + \left\lvert f^2_n(x) \right\rvert + \left\lvert f^1_n(x) f^2_n(x) \right\rvert \\
                          &=   \left\lvert f^1_n(x) \right\rvert + \left\lvert f^2_n(x) \right\rvert + \left\lvert f^1_n(x) \right\rvert \, \left\lvert f^2_n(x) \right\rvert \\
                          &\le C_1 + C_2 + C_1 C_2 \\
                          &=   D,
\end{align}
$$

where we have defined $$D \equiv C_1 + C_2 + C_1 C_2$$.

Thus we have proven that there exists a sequence of functions $$\{ g_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$ and a real-valued constant $$D$$ such that

$$
    \left\lvert g_n(x) \right\rvert \le D
$$

for all $$x \in X$$ and all $$n \in \mathbb{N}$$. In other words the $$g_n$$ are a sequence of uniformly bounded continuous functions.

Let $$\epsilon > 0$$ be an arbitrary real number and consider if we can find a natural number $$N$$ such that

$$
    \left\lvert g_n(x) - 1_{E_1 \cup E_2}(x) \right\rvert < \epsilon
$$

for all $$x \in X$$ and all $$n \ge N$$.

This is always possible as for all $$x \in X$$ the limit $$f^1_n(x) \rightarrow 1_{E_1}(x)$$ and the limit $$f^2_n \rightarrow 1_{E_2}$$ exist as real finite numbers. Hence,

$$
\begin{align}
    \lim_{n \rightarrow \infty} g_n(x) &= \lim_{n \rightarrow \infty} \left( f^1_n(x) + f^2_n(x) - f^1_n(x) f^2_n(x) \right) \\ 
                                       &= \lim_{n \rightarrow \infty} f^1_n(x) + \lim_{n \rightarrow \infty} f^2_n(x) - \lim_{n \rightarrow \infty} f^1_n(x) f^2_n(x) \\ 
                                       &= \lim_{n \rightarrow \infty} f^1_n(x) + \lim_{n \rightarrow \infty} f^2_n(x) - \left( \lim_{n \rightarrow \infty} f^1_n(x) \right) \left( \lim_{n \rightarrow \infty} f^2_n(x) \right) \\ 
                                       &= 1_{E_1}(x) + 1_{E_2}(x) - 1_{E_1}(x) 1_{E_2}(x) \\
                                       &= 1_{E_1 \cup E_2}(x)
\end{align}
$$

for each $$x \in X$$. That is, for each $$x \in X$$ and each real number $$\epsilon > 0$$ there exists a natural number $$N$$ (depending on $$x$$ and $$\epsilon$$ — one may take $$N = \max(N_1,N_2)$$ for the indices supplied by the two hypotheses at that $$x$$) such that for all $$n \ge N$$ one has

$$
    \left\lvert g_n(x) - 1_{E_1 \cup E_2}(x) \right\rvert < \epsilon.
$$

This completes the proof of **Property 3.2**, and with it the proposition.

Let us next prove **Part 2**, that $$\mathcal{L}_0$$ contains all open sets in $$X$$.

We will prove that $$\mathcal{L}_0$$ contains all open sets in $$X$$ by **Step 1:** proving that $$\mathcal{L}_0$$ contains all closed sets in $$X$$, then **Step 2:** relying on the fact that any open set is the complement of a closed set along with the fact that we proved that $$\mathcal{L}_0$$ is closed under complements.
$$\blacksquare$$

> **Proposition** *($$\mathcal{L}_0$$ Contains all Closed Sets)*
<a name="prpstn:L0-contains-closed"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:L0-class} -->
<!--  \uses{def:bump-function} -->
<!--  \uses{thrm:existence-of-bump-functions} -->
> With $$\mathcal{L}_0$$ as in [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class), every closed subset of $$X$$ lies in $$\mathcal{L}_0$$.

**Proof**
$$\mathcal{L}_0$$ contains all closed sets in $$X$$. To prove that $$\mathcal{L}_0$$ contains all closed sets in $$X$$ we must **Step 1.1:** prove that any closed set $$\overline{E}$$ in $$X$$ is measurable and **Step 1.2:** prove that $$1_{\overline{E}}$$ is the pointwise limit of a sequence of uniformly bounded continuous functions.

**Step 1.1:** Let us first prove that any closed set $$\overline{E}$$ in $$X$$ is measurable.

Note that by hypothesis $$X$$ is a metric measurable space. By definition this implies that $$X$$ is a measure space with a Borel regular measure. By definition a Borel regular measure is a measure in which any Borel set is measurable. By definition a Borel set is any set in a topological space that can be formed from open sets through the operations of countable union, countable intersection, and complement.

As any closed set $$\overline{E}$$ in $$X$$ is, by definition, the complement of an open set, and all open sets are Borel sets, it follows that any closed set $$\overline{E}$$ is a Borel set and thus measurable, the desired **Step 1.1** result.

**Step 1.2:** Let us next prove that $$1_{\overline{E}}$$ is the pointwise limit of a sequence of uniformly bounded continuous functions.

To this end let us review a definition we will require, that of a "bump function"

> **Definition** *(Bump Function)*
<a name="def:bump-function"></a>
> Given a topological manifold $$X$$, a closed subset $$\overline{E}$$ of $$X$$, and an open subset $$U$$ of $$X$$ that contains $$\overline{E}$$, i.e. $$\overline{E} \subset U$$, then a function $$f$$ in $$C^0(X; \mathbb{R})$$ is called a *bump function* for $$\overline{E}$$ supported in $$U$$ if
> 
> 1. For every $$x \in X$$ one has $$0 \le f(x) \le 1$$.
> 2. For every $$x \in \overline{E}$$ one has $$f(x) = 1$$.
> 3. $$f$$ is supported on $$U$$.

The existence of a bump function is guaranteed by the following theorem

> **Theorem** *(Existence of Bump Functions)*
<a name="thrm:existence-of-bump-functions"></a>
> Let $$X$$ be a normal topological space. For any closed set $$\overline{E}$$ in $$X$$ and any open set $$U$$ containing $$\overline{E}$$, there exists a bump function for $$\overline{E}$$ supported in $$U$$.

With this in mind consider our $$\overline{E}$$. One can always arrange for the existence of a sequence of open sets $$\{ U_i \}_{i \in \mathbb{N}}$$ in $$X$$ such that $$U_{i + 1} \subset U_{i}$$ and $$\overline{E} \subset U_i$$ for all $$i \in \mathbb{N}$$. By way of [**Existence of Bump Functions**](#thrm:existence-of-bump-functions) we are guaranteed the existence of a sequence of bump functions $$\{ f_i \}_{i \in \mathbb{N}}$$ with $$f_i$$ being a bump function for $$\overline{E}$$ supported in $$U_i$$.

The definition of a bump function implies that for $$C \equiv 1$$ we have

$$
    \left\lvert f_i(x) \right\rvert \le C
$$

for all $$x \in X$$ and all $$i \in \mathbb{N}$$. Thus the sequence $$\{ f_i \}_{i \in \mathbb{N}}$$ is uniformly bounded.

Furthermore, $$f_i \to 1_{\overline{E}}$$ pointwise. Fix $$x \in X$$ and $$\epsilon > 0$$. If $$x \in \overline{E}$$ then $$f_i(x) = 1 = 1_{\overline{E}}(x)$$ for every $$i$$, by the first defining property of a bump function, and any $$N$$ will do. If $$x \notin \overline{E}$$ then, since $$\bigcap_i U_i = \overline{E}$$, there is an index $$N$$ — depending on $$x$$ — with $$x \notin U_N$$; as $$f_N$$ is supported in $$U_N$$ and the $$U_i$$ are decreasing, $$f_i(x) = 0 = 1_{\overline{E}}(x)$$ for all $$i \ge N$$. In either case

$$
    \left\lvert f_i(x) - 1_{\overline{E}}(x) \right\rvert < \epsilon \qquad \text{for all } i \ge N.
$$

The dependence of $$N$$ on $$x$$ is essential and cannot be removed: the convergence is *not* uniform, since a uniform limit of continuous functions would be continuous and $$1_{\overline{E}}$$ is not, for $$\overline{E}$$ closed but not open. So $$1_{\overline{E}}$$ is the pointwise limit of a uniformly bounded sequence of continuous functions, as required.
$$\blacksquare$$


The next lemma uses the Monotone Class Theorem, which we state first.

> **Theorem** *(Monotone Class Theorem)*
<a name="thrm:monotone-class-theorem"></a>
> Let $$\mathcal{A}$$ be an algebra of subsets of a set $$X$$, and let $$\mathcal{M}$$ be a monotone class, i.e. a collection of subsets of $$X$$ closed under countable increasing unions and countable decreasing intersections, such that $$\mathcal{A} \subseteq \mathcal{M}$$. Then $$\sigma(\mathcal{A}) \subseteq \mathcal{M}$$, where $$\sigma(\mathcal{A})$$ is the smallest $$\sigma$$-algebra containing $$\mathcal{A}$$.

The next of these "utility" lemmas is the following:

> **Lemma** *(Extension from an Algebra to the Generated $$\sigma$$-Algebra)*
<a name="lmm:hall-prblm-8.3.3b"></a>
<!--  \uses{def:L0-class} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{lmm:hall-prblm-8.3.3a} -->
<!--  \uses{thrm:monotone-class-theorem} -->
> Let $$X$$ be a compact metric measurable space and $$C^0(X; \mathbb{R})$$ the set of continuous real-valued functions on $$X$$. Let $$\mathcal{C}$$ be the set of bounded, measurable, complex-valued functions on $$X$$ such that (1) $$\mathcal{C}$$ is a complex vector space, (2) $$\mathcal{C}$$ contains $$C^0(X; \mathbb{R})$$, and (3) $$\mathcal{C}$$ is closed under pointwise limits of uniformly bounded sequences. Finally let $$\mathcal{L}_1$$ be the set of all measurable sets $$E$$ in $$X$$ such that the indicator function $$1_E$$ belongs to $$\mathcal{C}$$. Then $$\mathcal{L}_1$$ contains all Borel sets in $$X$$.

**Proof**
By [Definition (The Class $$\mathcal{L}_0$$)](#def:L0-class), $$\mathcal{L}_0$$ is the set of all measurable subsets $$E$$ of $$X$$ whose indicator function $$1_E$$ is the *pointwise* limit of a uniformly bounded sequence of continuous, real-valued functions on $$X$$.

Let us first prove that $$\mathcal{L}_0 \subseteq \mathcal{L}_1$$. Consider any $$E$$ in $$\mathcal{L}_0$$. Then there exists a sequence $$\{ f_n \}_{n \in \mathbb{N}}$$ in $$C^0(X; \mathbb{R})$$, uniformly bounded, that converges pointwise to $$1_E$$. By hypothesis $$C^0(X; \mathbb{R})$$ is a subset of $$\mathcal{C}$$, so each $$f_n$$ is in $$\mathcal{C}$$. By hypothesis $$\mathcal{C}$$ is closed under pointwise limits of uniformly bounded sequences, so $$1_E$$, being such a limit, is in $$\mathcal{C}$$. Hence $$E$$ is in $$\mathcal{L}_1$$, the desired result $$\mathcal{L}_0 \subseteq \mathcal{L}_1$$.

Next let us prove that $$\mathcal{L}_1$$ is a monotone class, i.e. that $$\mathcal{L}_1$$ is closed under countable increasing unions and countable decreasing intersections.

Let $$\{ E_n \}_{n \in \mathbb{N}}$$ be an increasing sequence of sets in $$\mathcal{L}_1$$, i.e. $$E_0 \subseteq E_1 \subseteq \cdots$$ with each $$1_{E_n} \in \mathcal{C}$$, and let $$E \equiv \bigcup_{n \in \mathbb{N}} E_n$$. For any $$x \in X$$, if $$x \in E$$ then $$x \in E_{n_0}$$ for some $$n_0$$, and since the $$E_n$$ are increasing, $$1_{E_n}(x) = 1$$ for all $$n \ge n_0$$; if $$x \notin E$$ then $$1_{E_n}(x) = 0$$ for all $$n$$. Hence $$1_{E_n}(x) \rightarrow 1_E(x)$$ for every $$x \in X$$, i.e. $$1_{E_n} \rightarrow 1_E$$ pointwise. Furthermore this convergence is uniformly bounded, as $$\lvert 1_{E_n}(x) \rvert \le 1$$ for all $$n$$ and $$x$$. As $$\mathcal{C}$$ is closed under uniformly bounded pointwise limits (property (3) of $$\mathcal{C}$$), we conclude $$1_E \in \mathcal{C}$$, i.e. $$E \in \mathcal{L}_1$$.

An entirely analogous argument applies to a decreasing sequence $$\{ E_n \}_{n \in \mathbb{N}}$$ in $$\mathcal{L}_1$$, i.e. $$E_0 \supseteq E_1 \supseteq \cdots$$: with $$E \equiv \bigcap_{n \in \mathbb{N}} E_n$$, one again has $$1_{E_n} \rightarrow 1_E$$ pointwise and uniformly bounded by $$1$$, so property (3) of $$\mathcal{C}$$ gives $$1_E \in \mathcal{C}$$, i.e. $$E \in \mathcal{L}_1$$.

Together these prove that $$\mathcal{L}_1$$ is a monotone class.

With this established, we can apply the [**Monotone Class Theorem**](#thrm:monotone-class-theorem). Identifying $$\mathcal{A}$$ with $$\mathcal{L}_0$$---an algebra, as established in [**Lemma**](#lmm:hall-prblm-8.3.3a)---and $$\mathcal{M}$$ with $$\mathcal{L}_1$$---a monotone class containing $$\mathcal{L}_0$$, as we just proved---the [**Monotone Class Theorem**](#thrm:monotone-class-theorem) implies

$$
    \sigma(\mathcal{L}_0) \subseteq \mathcal{L}_1,
$$

where $$\sigma(\mathcal{L}_0)$$ is the smallest $$\sigma$$-algebra containing $$\mathcal{L}_0$$.

However, as $$\mathcal{L}_0$$ contains all open sets in $$X$$ ([**Lemma**](#lmm:hall-prblm-8.3.3a)), and the Borel $$\sigma$$-algebra of $$X$$ is by definition the smallest $$\sigma$$-algebra containing all open sets in $$X$$, it follows that the Borel $$\sigma$$-algebra of $$X$$ is contained in $$\sigma(\mathcal{L}_0)$$. Combined with our previous result this gives

$$
    \text{(Borel sets of } X\text{)} \subseteq \sigma(\mathcal{L}_0) \subseteq \mathcal{L}_1.
$$

Hence, $$\mathcal{L}_1$$ contains all Borel sets, the desired result.$$\blacksquare$$

The next lemma uses the following form of the Monotone Convergence Theorem, which we state first.

> **Theorem** *(Monotone Convergence Theorem, Non-Increasing Case)*
<a name="thrm:monotone-convergence-theorem-nonincreasing"></a>
> Let $$\{ a_i \}_{i \in \mathbb{N}}$$ be a non-increasing sequence of real numbers, i.e. $$a_i \ge a_{i + 1}$$ for all $$i \in \mathbb{N}$$, and suppose it is **bounded below**. Then it converges, and
>
> $$
>     \lim\limits_{i \rightarrow \infty} a_i = \inf_{i \in \mathbb{N}} a_i.
> $$
>
> The boundedness hypothesis is needed: without it $$\inf_i a_i = -\infty$$ and the sequence has no limit in $$\mathbb{R}$$. Compare [**Theorem** *(Monotone Convergence Theorem)*](#thrm:monotone-convergence-theorem), which states the two-sided version with the same hypothesis.

Before proving the final of these "utility" lemmas, we isolate the following elementary fact about pointwise limits of Borel-measurable functions, which we will have need of shortly.

> **Lemma** *(Pointwise Limits of Uniformly Bounded, Borel-Measurable Functions)*
<a name="lmm:pointwise-limits-of-borel-measurable-functions"></a>
<!--  \uses{thrm:monotone-convergence-theorem-nonincreasing} -->
> Let $$X$$ be a compact metric measurable space. Let $$\{ f_i \}_{i \in \mathbb{N}}$$ be a sequence of bounded, Borel-measurable, complex-valued functions on $$X$$ that are uniformly bounded, i.e. there exists a real-valued constant $$M$$ such that
>
> $$
>     \lvert f_i(x) \rvert \le M
> $$
>
> for all $$i \in \mathbb{N}$$ and all $$x \in X$$, and that converge pointwise to a function $$f : X \rightarrow \mathbb{C}$$. Then $$f$$ is bounded and Borel-measurable.

**Proof**
Let us first prove that $$f$$ is bounded. For any $$x \in X$$ we have

$$
\begin{align}
    \lvert f(x) \rvert &= \lim\limits_{i \rightarrow \infty} \lvert f(x) - f_i(x) + f_i(x) \rvert \\
                        &\le \lim\limits_{i \rightarrow \infty} \lvert f(x) - f_i(x) \rvert + \lvert f_i(x) \rvert \\
                        &=   \lim\limits_{i \rightarrow \infty} \lvert f(x) - f_i(x) \rvert + \lim\limits_{i \rightarrow \infty} \lvert f_i(x) \rvert \\
                        &=   \lim\limits_{i \rightarrow \infty} \lvert f_i(x) \rvert \\
                        &\le \lim\limits_{i \rightarrow \infty} M \\
                        &=   M,
\end{align}
$$

where we have used that $$f_i(x) \rightarrow f(x)$$ and the definition of a norm. This proves $$\lvert f(x) \rvert \le M$$ for all $$x \in X$$, i.e. $$f$$ is bounded.

Next let us prove that $$f$$ is Borel-measurable.

As $$\{ f_i \}_{i \in \mathbb{N}}$$ converges to $$f$$ pointwise, and as taking real and imaginary parts is continuous, the real-valued sequences $$\{ \text{Re}(f_i) \}_{i \in \mathbb{N}}$$ and $$\{ \text{Im}(f_i) \}_{i \in \mathbb{N}}$$ converge pointwise to $$\text{Re}(f)$$ and $$\text{Im}(f)$$ respectively. Explicitly, for any $$x \in X$$,

$$
    \lvert \text{Re}(f(x)) - \text{Re}(f_i(x)) \rvert \le \lvert f(x) - f_i(x) \rvert \rightarrow 0
$$

as $$i \rightarrow \infty$$, and similarly

$$
    \lvert \text{Im}(f(x)) - \text{Im}(f_i(x)) \rvert \le \lvert f(x) - f_i(x) \rvert \rightarrow 0.
$$

As $$\{ f_i \}_{i \in \mathbb{N}}$$ is uniformly bounded by $$M$$, so too are $$\{ \text{Re}(f_i) \}_{i \in \mathbb{N}}$$ and $$\{ \text{Im}(f_i) \}_{i \in \mathbb{N}}$$, since $$\lvert \text{Re}(f_i(x)) \rvert \le \lvert f_i(x) \rvert \le M$$ and likewise for the imaginary part. This allows us to define, for each $$i \in \mathbb{N}$$, the real numbers

$$
    g_i(x) \equiv \sup\limits_{n \ge i} \text{Re}(f_n(x)), \qquad h_i(x) \equiv \sup\limits_{n \ge i} \text{Im}(f_n(x)),
$$

both of which are well-defined, as suprema of bounded sets of real numbers.

By an identical argument to before---now applied to the real-valued sequence $$\{ \text{Re}(f_n(x)) \}_{n \in \mathbb{N}}$$ converging to $$\text{Re}(f(x))$$---for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for $$i \ge N$$ one has

$$
    \lvert \text{Re}(f(x)) - g_i(x) \rvert < \epsilon,
$$

which implies

$$
    \text{Re}(f(x)) = \lim\limits_{i \rightarrow \infty} g_i(x).
$$

An identical argument applied to the real-valued sequence $$\{ \text{Im}(f_n(x)) \}_{n \in \mathbb{N}}$$ converging to $$\text{Im}(f(x))$$ gives

$$
    \text{Im}(f(x)) = \lim\limits_{i \rightarrow \infty} h_i(x).
$$

Now looking at the sequences

$$
    \left\{  g_i(x) \right\}_{i \in \mathbb{N}} \quad \text{and} \quad \left\{  h_i(x) \right\}_{i \in \mathbb{N}}
$$

we see that both are non-increasing, since each is a supremum taken over a shrinking set of indices $$\{ n : n \ge i \}$$ as $$i$$ increases. Both are also bounded below: the $$f_n$$ are uniformly bounded, say $$\lvert f_n(x) \rvert \le M$$ for all $$n$$ and $$x$$, so $$g_i(x) \ge \text{Re}(f_i(x)) \ge -M$$ and likewise $$h_i(x) \ge -M$$. Hence, we can apply the [**Monotone Convergence Theorem (Non-Increasing Case)**](#thrm:monotone-convergence-theorem-nonincreasing) to each of these sequences, giving

$$
\begin{align}
    \text{Re}(f(x)) &= \lim\limits_{i \rightarrow \infty} g_i(x) \\
                &= \inf_{i \in \mathbb{N}} g_i(x), \qquad \text{Im}(f(x)) \\
                &= \lim\limits_{i \rightarrow \infty} h_i(x) \\
                &= \inf_{i \in \mathbb{N}} h_i(x).
\end{align}
$$

We will next prove that $$g_i$$ and $$h_i$$ are Borel-measurable, and use this and the two equations above to prove that $$\text{Re}(f)$$ and $$\text{Im}(f)$$---and hence $$f$$ itself---are Borel-measurable.

Note that a real-valued function is Borel-measurable if the preimage of any set of the form $$(a, \infty)$$ is a Borel set. With that in mind consider the preimage of $$(a, \infty)$$ under $$g_i$$

$$
    \left\{ x \in X : g_i(x) > a \right\} = \left\{ x \in X : \sup\limits_{n \ge i} \text{Re}(f_n(x)) > a \right\}.
$$

The supremum of a set of numbers is strictly greater than $$a$$ if and only if at least one of the numbers in the sequence is strictly greater than $$a$$. Hence,

$$
    \left\{ x \in X : \sup\limits_{n \ge i} \text{Re}(f_n(x)) > a \right\} = \bigcup_{n=i}^\infty  \left\{ x \in X : \text{Re}( f_n(x) ) > a \right\}.
$$

As each $$f_n$$ is by hypothesis Borel measurable, and the Borel $$\sigma$$-algebra on $$\mathbb{C}$$ is generated by the Cartesian product of Borel sets on $$\mathbb{R}$$, each $$\text{Re}( f_n(x) )$$ is Borel measurable. Hence, sets of the form

$$
    \left\{ x \in X : \text{Re}( f_n(x) ) > a \right\}
$$

are Borel measurable sets. As the $$\sigma$$-algebra of Borel sets is closed under countable unions, it then follows that

$$
    \bigcup_{n=i}^\infty  \left\{ x \in X : \text{Re}( f_n(x) ) > a \right\}
$$

is a Borel measurable set. Hence, the preimage of any set of the form $$(a, \infty)$$ under $$g_i$$ is a Borel measurable set, and thus $$g_i$$ is Borel measurable. An identical argument, with $$\text{Im}(f_n)$$ in place of $$\text{Re}(f_n)$$, proves that $$h_i$$ is Borel measurable.

Now let us prove that $$\text{Re}(f)$$ and $$\text{Im}(f)$$ are Borel measurable.

Recall that a real-valued function is Borel measurable if the preimage of any set of the form $$(-\infty, a)$$ is a Borel set. With this in mind consider the preimage of $$(-\infty, a)$$ under $$\text{Re}(f)$$

$$
    \left\{ x \in X : \text{Re}(f(x)) < a \right\} = \left\{ x \in X : \inf_{i \in \mathbb{N}} g_i(x) < a \right\}.
$$

Now the infimum of a sequence is strictly less than $$a$$ if and only if at least one term in the sequence is strictly less than $$a$$. Hence,

$$
    \left\{ x \in X : \inf_{i \in \mathbb{N}} g_i(x) < a \right\} = \bigcup_{i \in \mathbb{N}}  \left\{ x \in X : g_i(x) < a \right\}.
$$

However, we proved that $$g_i$$ is Borel measurable. Thus

$$
    \left\{ x \in X : g_i(x) < a \right\}
$$

are Borel measurable sets. As the $$\sigma$$-algebra of Borel sets is closed under countable unions, it then follows that

$$
    \bigcup_{i \in \mathbb{N}}  \left\{ x \in X : g_i(x) < a \right\}
$$

is a Borel measurable set. Hence, the preimage of any set of the form $$(-\infty, a)$$ under $$\text{Re}(f)$$ is a Borel measurable set, and thus $$\text{Re}(f(x))$$ is Borel measurable. An identical argument, with $$h_i$$ in place of $$g_i$$, proves that $$\text{Im}(f(x))$$ is Borel measurable.

As the Borel $$\sigma$$-algebra on $$\mathbb{C}$$ is generated by the Cartesian product of Borel sets on $$\mathbb{R}$$, a complex valued function is Borel-measurable if and only if both its real part and its imaginary part are real-valued Borel measurable functions. As we have just shown $$\text{Re}(f)$$ and $$\text{Im}(f)$$ are both real-valued Borel measurable functions, it follows that $$f$$ is Borel-measurable.

Together, boundedness and Borel-measurability of $$f$$ give the desired result.$$\blacksquare$$

The final of these "utility" lemmas is the following:

> **Lemma** *(A Class Containing the Continuous Functions and Closed under Bounded Limits is Everything)*
<a name="lmm:hall-prblm-8.3.3c"></a>
<!--  \uses{def:indicator-function} -->
<!--  \uses{lmm:hall-prblm-8.3.3b} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$X$$ be a compact metric measurable space and $$C^0(X; \mathbb{R})$$ the set of continuous real-valued functions on $$X$$. Let $$\mathcal{C}$$ be the set of bounded, measurable, complex-valued functions on $$X$$ such that (1) $$\mathcal{C}$$ is a complex vector space, (2) $$\mathcal{C}$$ contains $$C^0(X; \mathbb{R})$$, and (3) $$\mathcal{C}$$ is closed under pointwise limits of uniformly bounded sequences. Then $$\mathcal{C}$$ consists of all bounded, Borel-measurable functions on $$X$$.

**Proof**
By hypothesis $$\mathcal{C}$$ is the set of bounded, measurable, complex-valued functions on $$X$$ such that (1) $$\mathcal{C}$$ is a complex vector space, (2) $$\mathcal{C}$$ contains $$C^0(X; \mathbb{R})$$, and (3) $$\mathcal{C}$$ is closed under pointwise limits of uniformly bounded sequences.

Let us first prove that any function $$f$$ in $$\mathcal{C}$$ is bounded and Borel-measurable.

For any $$f \in \mathcal{C}$$, the definition of $$\mathcal{C}$$ implies that $$f$$ is bounded and measurable. As $$X$$ is a metric measurable space, its measure is a Borel regular measure. A Borel regular measure is a measure in which any Borel set is measurable. Hence, in the definition of $$\mathcal{C}$$ when we state that $$f$$ is measurable we mean that $$f$$ is Borel-measurable. Thus, any $$f \in \mathcal{C}$$ is bounded and Borel-measurable.

Let us now prove that any bounded, Borel-measurable, complex-valued function $$f$$ on $$X$$ is in $$\mathcal{C}$$.

By [**Lemma**](#lmm:hall-prblm-8.3.3b), the set $$\mathcal{L}_1 \equiv \{ E \subseteq X \text{ measurable} : 1_E \in \mathcal{C} \}$$ contains all Borel sets of $$X$$. As noted above, on $$X$$ "measurable" and "Borel-measurable" coincide; hence every measurable set of $$X$$ is a Borel set, and so for any measurable set $$E$$ of $$X$$, $$1_E \in \mathcal{C}$$.

Consider now an arbitrary simple function $$s$$ on $$X$$, i.e.

$$
    s = \sum_{i = 1}^n \alpha_i 1_{E_i},
$$

where $$\alpha_i \in \mathbb{C}$$ and the $$E_i$$ are pairwise disjoint measurable sets of $$X$$. By the previous paragraph, each $$1_{E_i}$$ is in $$\mathcal{C}$$. As $$\mathcal{C}$$ is by hypothesis a complex vector space, it is closed under finite linear combinations, so $$s \in \mathcal{C}$$. Hence every simple function on $$X$$ is in $$\mathcal{C}$$.

Now consider our arbitrary bounded, Borel-measurable, complex-valued function $$f$$ on $$X$$. By the [**Complex-Valued Simple Approximation Theorem**](#thrm:complex-valued-simple-approximation-theorem), there exists a sequence $$\{ s_i \}_{i \in \mathbb{N}}$$ of complex-valued simple functions on $$X$$ that converges uniformly to $$f$$ on $$X$$. By the previous paragraph, each $$s_i$$ is in $$\mathcal{C}$$.

We claim the $$s_i$$ are uniformly bounded. As $$f$$ is bounded, there exists $$M_f \in \mathbb{R}$$ such that $$\lvert f(x) \rvert \le M_f$$ for all $$x \in X$$. As $$s_i \rightarrow f$$ uniformly, there exists $$N \in \mathbb{N}$$ such that for all $$i \ge N$$ and all $$x \in X$$

$$
    \lvert s_i(x) - f(x) \rvert < 1,
$$

so that $$\lvert s_i(x) \rvert < M_f + 1$$ for all $$i \ge N$$ and all $$x \in X$$. Each of the finitely many remaining $$s_1, \ldots, s_{N-1}$$ is individually a simple function, hence bounded. Setting

$$
    M \equiv \max \left\{ \sup_{x \in X} \lvert s_1(x) \rvert, \ldots, \sup_{x \in X} \lvert s_{N-1}(x) \rvert, M_f + 1 \right\},
$$

we have $$\lvert s_i(x) \rvert \le M$$ for all $$i \in \mathbb{N}$$ and all $$x \in X$$, i.e. the $$s_i$$ are uniformly bounded.

As $$s_i \rightarrow f$$ uniformly, in particular $$s_i \rightarrow f$$ pointwise. Thus $$\{ s_i \}_{i \in \mathbb{N}}$$ is a uniformly bounded sequence in $$\mathcal{C}$$ that converges pointwise to $$f$$. As $$\mathcal{C}$$ is by hypothesis closed under pointwise limits of uniformly bounded sequences, $$f \in \mathcal{C}$$.

Thus, any bounded, Borel-measurable, complex-valued function $$f$$ on $$X$$ is in $$\mathcal{C}$$.

So we've proven that any function $$f$$ in $$\mathcal{C}$$ is bounded and Borel-measurable and we've proven that any bounded, Borel-measurable, complex-valued function $$f$$ on $$X$$ is in $$\mathcal{C}$$. Thus, $$\mathcal{C}$$ is the set of bounded, Borel-measurable, complex-valued functions on $$X$$, the desired result.$$\blacksquare$$


#### The Bounded Borel Functional Calculus

With [**Proposition** *(hall-8.7)*](#prpstn:hall-8.7) established, let us introduce another definition that will be of use later. It essentially amounts to a means of defining an operator $$f(A)$$ from a bounded measurable function $$f$$ on $$\sigma(A)$$; this is in contrast to the identically notated operator $$f(A)$$ defined in [**Proposition**](#prpstn:hall-8.3) which requires $$f$$ be an element of $$C^0(\sigma(A); \mathbb{R})$$.

> **Definition** *(The Bounded Borel Functional Calculus)*
<a name="def:hall-8.8"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:hall-a.63} -->
> Let $$A$$ in $$\mathcal{B}(\mathbf{H})$$ be self-adjoint. For a bounded, measurable, complex-valued function $$f$$ on the spectrum $$\sigma(A)$$ of $$A$$, let $$f(A)$$ be the operator associated to the quadratic form $$Q_f$$ of [**Definition**](#def:hall-8.6) by [**Proposition**](#prpstn:hall-a.63). This means that $$f(A)$$ is the unique operator such that
> 
> $$
>     \left< \psi, f(A)\psi \right> = Q_f(\psi) = \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda)
> $$
> 
> for all $$\psi \in \mathbf{H}$$.

As a first use of this definition we can prove the following lemma

> **Lemma** *(The Operator of a Real-Valued Function is Self-Adjoint)*
<a name="lmm:lemma-3"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{prpstn:hall-8.7} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A$$ in $$\mathcal{B}(\mathbf{H})$$ be self-adjoint, $$f$$ a bounded, measurable, complex-valued function on the spectrum $$\sigma(A)$$ of $$A$$, and $$f(A)$$ the operator associated to $$f$$ by way of the previous [**Definition**](#def:hall-8.8). If $$f$$ is real-valued, then $$f(A)$$ is self-adjoint.

**Proof**
By hypothesis $$f$$ is a bounded, measurable, real-valued function on the spectrum $$\sigma(A)$$ of $$A$$. By definition $$Q_f$$ acting on an arbitrary $$\psi \in \mathbf{H}$$ is given by

$$
    Q_f(\psi) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda),
$$

where, as stated in [**Definition**](#def:hall-8.8), the measure $$\mu_\psi$$ is the measure on $$\sigma(A)$$ derived from the [**Riesz Representation Theorem**](#thrm:riesz-representation). As a result of the [**Proposition**](#prpstn:hall-8.7) we just proved, $$Q_f$$ is a bounded quadratic form.

Now, as $$\mu_\psi$$ is the measure derived from the [**Riesz Representation Theorem**](#thrm:riesz-representation), it is a real-valued, positive measure on the Borel $$\sigma$$-algebra of $$\sigma(A)$$.

Furthermore, by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable) the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$.

Thus, $$f$$ being real-valued, $$\mu_\psi$$ being real-valued, and the spectrum $$\sigma(A)$$ of $$A$$ being a subset of $$\mathbb{R}$$ together imply that the integral defining $$Q_f(\psi)$$

$$
    Q_f(\psi) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda),
$$

and thus $$Q_f(\psi)$$ is real-valued for any $$\psi \in \mathbf{H}$$.

As $$Q_f(\psi)$$ is real-valued for all $$\psi \in \mathbf{H}$$, [**Proposition**](#prpstn:hall-a.63) implies that $$f(A)$$ is self-adjoint, the desired result.$$\blacksquare$$

The next proposition uses the Polarization Identity, which we state first.

> **Proposition** *(Polarization Identity)*
<a name="prpstn:hall-a.59"></a>
<!--  \uses{def:bounded-sesquilinear-form} -->
> If $$L$$ is a sesquilinear form on the Hilbert space $$\mathbf{H}$$, then for any $$\phi, \psi \in \mathbf{H}$$ the value of $$L(\phi, \psi)$$ can be determined from the values of $$L$$ "on the diagonal" (i.e. the values of $$L(\xi, \xi)$$ for various $$\xi \in \mathbf{H}$$) as follows:
> 
> $$
> \begin{align}
>     L(\phi, \psi) &= \frac{1}{2} \left[ L(\phi + \psi, \phi + \psi) - L(\phi, \phi) - L(\psi, \psi) \right] \\
>                   &-\frac{i}{2} \left[ L(\phi + i\psi, \phi + i\psi) - L(\phi, \phi) - L(i\psi, i\psi) \right]. 
> \end{align}
> $$

The next proposition proves the analog of multiplicativity from [**Proposition**](#prpstn:hall-8.4) for operators $$(fg)(A)$$, $$f(A)$$, and $$g(A)$$ that arise from bounded measurable functions $$f$$ and $$g$$ by way of [**Definition**](#def:hall-8.8).

> **Proposition** *(The Bounded Borel Functional Calculus is Multiplicative)*
<a name="prpstn:hall-8.9"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:F1-closed-under-limits} -->
<!--  \uses{prpstn:F1-vector-space} -->
<!--  \uses{prpstn:F2-is-everything} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{prpstn:associated-measures-self-adjoint} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:hall-8.7} -->
<!--  \uses{prpstn:hall-a.59} -->
<!--  \uses{def:bounded-sesquilinear-form} -->
<!--  \uses{prpstn:hall-a.61} -->
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and $$f$$ and $$g$$ be bounded, measurable, complex-valued functions on the spectrum $$\sigma(A)$$ of $$A$$, then
> 
> $$
>     (fg)(A) = f(A) g(A),
> $$
> 
> where $$(fg)(A)$$, $$f(A)$$, and $$g(A)$$ are operators that arise respectively from $$(fg)$$, $$f$$, and $$g$$ by way of [**Definition**](#def:hall-8.8).

**Proof**
The result is obtained by applying [**Lemma** *(hall-prblm-8.3.3c)*](#lmm:hall-prblm-8.3.3c) twice. The first pass, through [**Proposition** *($$\mathcal{F}_1$$ is a Vector Space)*](#prpstn:F1-vector-space) and [**Proposition** *($$\mathcal{F}_1$$ is Closed under Bounded Pointwise Limits)*](#prpstn:F1-closed-under-limits), gives multiplicativity for an arbitrary bounded Borel $$f$$ paired with a *continuous* $$g$$. The second pass, [**Proposition** *($$\mathcal{F}_2$$ Contains all Bounded Borel Functions)*](#prpstn:F2-is-everything), lifts the second argument to bounded Borel functions as well, which is the statement of this proposition.$$\blacksquare$$

> **Definition** *(The Classes $$\mathcal{F}_1$$ and $$\mathcal{F}_2$$)*
<a name="def:F1-F2-classes"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:F-class} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint, and let $$f \mapsto f(A)$$ be the bounded Borel functional calculus of [**Definition**](#def:hall-8.8). Write
>
> $$
> \begin{align}
>     \mathcal{F}_1 &\equiv \{ f \text{ bounded, Borel-measurable on } \sigma(A) \mid (fg)(A) = f(A)g(A) \text{ for all } g \in C^0(\sigma(A); \mathbb{R}) \}, \\
>     \mathcal{F}_2 &\equiv \{ g \text{ bounded, Borel-measurable on } \sigma(A) \mid (fg)(A) = f(A)g(A) \text{ for all bounded, Borel-measurable } f \}.
> \end{align}
> $$
>
> These are distinct from the class $$\mathcal{F}$$ of [Definition (The Class of Functions with Bounded Quadratic Form)](#def:F-class): the subscripted classes concern *multiplicativity* of the functional calculus, not boundedness of a quadratic form.

> **Proposition** *($$\mathcal{F}_1$$ is a Vector Space)*
<a name="prpstn:F1-vector-space"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:F1-F2-classes} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:associated-measures-self-adjoint} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mathcal{F}_1$$ as in [Definition (The Classes $$\mathcal{F}_1$$ and $$\mathcal{F}_2$$)](#def:F1-F2-classes), $$\mathcal{F}_1$$ is a complex vector space containing $$C^0(\sigma(A); \mathbb{R})$$.

**Proof**
We first show $$\mathcal{F}_1$$ is a complex vector space. To prove this consider any $$f_1$$ and $$f_2$$ in $$\mathcal{F}_1$$ and any $$\alpha_1$$ and $$\alpha_2$$ in $$\mathbb{C}$$. Then one has

$$
\begin{align}
    ((\alpha_1f_1 + \alpha_2f_2)g)(A) &= (\alpha_1(f_1g) + \alpha_2(f_2g))(A) \\
                                      &= \alpha_1(f_1g)(A) + \alpha_2(f_2g)(A) \\
                                      &= \alpha_1f_1(A)g(A) + \alpha_2f_2(A)g(A) \\
                                      &= (\alpha_1f_1(A) + \alpha_2f_2(A))g(A),
\end{align}
$$

where the first line is the distributive property over functions, the second from linearity of the integral in [**Definition**](#def:hall-8.8), the third from properties of $$\mathcal{F}_1$$ along with the fact $$f_1, f_2 \in \mathcal{F}_1$$ and $$g \in C^0(\sigma(A); \mathbb{R})$$, and the final is the distributive property over operators. These imply

$$
\begin{align}
    ((\alpha_1f_1 + \alpha_2f_2)g)(A) &= (\alpha_1f_1(A) + \alpha_2f_2(A))g(A) \\
                                      &= (\alpha_1f_1 + \alpha_2f_2)(A)g(A),
\end{align}
$$

where the second equality follows from linearity. This implies

$$
    ((\alpha_1f_1 + \alpha_2f_2)g)(A) = (\alpha_1f_1 + \alpha_2f_2)(A)g(A)
$$

which is nothing more than the statement that $$\mathcal{F}_1$$ is a complex vector space.

We further claim that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$\mathcal{F}_1$$. To prove this consider arbitrary $$f$$ and $$g$$ in $$C^0(\sigma(A); \mathbb{R})$$. If $$f(A)$$ and $$g(A)$$ were the operators defined by [**Proposition**](#prpstn:hall-8.3) then the desired property

$$
    (fg)(A) = f(A)g(A)
$$

would follow from the multiplicativity property of [**Proposition**](#prpstn:hall-8.3). So if we can prove that in the case $$f,g \in C^0(\sigma(A); \mathbb{R})$$, the operators $$f(A)$$ and $$g(A)$$ defined by [**Definition**](#def:hall-8.8) are the same as those defined by [**Proposition**](#prpstn:hall-8.3), then we will have proven the claim.

If $$f,g \in C^0(\sigma(A); \mathbb{R})$$, the operators $$f(A)$$ and $$g(A)$$ defined by [**Definition**](#def:hall-8.8) are the unique operators $$f(A)$$ and $$g(A)$$ such that

$$
\begin{align}
    \left< \psi, f(A)\psi \right> &= \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) \\
    \left< \psi, g(A)\psi \right> &= \int_{\sigma(A)} g(\lambda) \, d\mu_\psi(\lambda), 
\end{align}
$$

for all $$\psi \in \mathbf{H}$$. If $$f,g \in C^0(\sigma(A); \mathbb{R})$$, the operators $$f(A)$$ and $$g(A)$$ defined by [**Proposition**](#prpstn:hall-8.3) are the unique operators $$f(A)$$ and $$g(A)$$ such that

$$
\begin{align}
    \left< \psi, f(A)\psi \right> &= \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) \\
    \left< \psi, g(A)\psi \right> &= \int_{\sigma(A)} g(\lambda) \, d\mu_\psi(\lambda), 
\end{align}
$$

for all $$\psi \in \mathbf{H}$$. Note here we have used [**Proposition** *(The Measures Associated to a Self-Adjoint Operator)*](#prpstn:associated-measures-self-adjoint) to write these operators in a form similar to that above. Hence, in both cases the operators $$f(A)$$ and $$g(A)$$ are the same. This then proves the claim that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$\mathcal{F}_1$$.
$$\blacksquare$$

> **Proposition** *(The Quadratic Form is Continuous under Bounded Pointwise Limits)*
<a name="prpstn:Q-continuous-under-limits"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:F1-F2-classes} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{prpstn:hall-8.7} -->
<!--  \uses{prpstn:hall-a.59} -->
<!--  \uses{prpstn:hall-a.61} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and $$\psi \in \mathbf{H}$$. If $$\{f_i\}$$ are bounded, Borel-measurable, uniformly bounded and converge pointwise to $$f$$ on $$\sigma(A)$$, then $$Q_{f_i}(\psi) \rightarrow Q_f(\psi)$$, and likewise for the associated sesquilinear forms.

**Proof**
We show that the map $$f \mapsto Q_f(\psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\psi \in \mathbf{H}$$. It turns out we actually proved this as part of our [**Proposition**](#prpstn:hall-8.7) proof.

In [**Proposition**](#prpstn:hall-8.7) we proved that $$\mathcal{F}$$ the space of all bounded, Borel-measurable, complex-valued functions $$f$$ such that $$Q_f$$ is a quadratic form is closed under uniformly bounded pointwise limits and that $$\mathcal{F}$$ is the space of all bounded, Borel-measurable, complex-valued functions. Hence, $$f \mapsto Q_f(\psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\psi \in \mathbf{H}$$ when $$f$$ is a bounded, Borel-measurable, complex-valued function, the desired result.

Now recall the [**Polarization Identity**](#prpstn:hall-a.59) stated above, which expresses the sesquilinear form $$L$$ associated to a quadratic form $$Q$$ in terms of the values of $$Q$$ alone.

This result---along with the [**Proposition**](#prpstn:hall-a.61) which for quadratic form $$Q$$ expresses its sesquilinear form $$L$$ on the diagonal in terms of the quadratic form itself as follows

$$
   L(\psi, \psi) = Q(\psi)
$$

for all $$\psi \in \mathbf{H}$$---allows us to write a quadratic form's sesquilinear form "off the diagonal" purely in terms of the quadratic form itself.

So, as [**Proposition**](#prpstn:hall-8.7) proves $$Q_f$$ is a bounded, quadratic form for any bounded, Borel-measurable, complex-valued function $$f$$, we can write the sesquilinear form $$L_f$$ associated to $$Q_f$$ purely in terms of $$Q_f$$.

As we can express $$L_f$$ purely in terms of $$Q_f$$ it follows from our previous result that the map $$f \mapsto L_f(\phi, \psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\phi,\psi \in \mathbf{H}$$ when $$f$$ is a bounded, Borel-measurable, complex-valued function.

Now by definition for any $$f \in \mathcal{F}_1$$ and any $$g \in C^0(\sigma(A); \mathbb{R})$$ we have

$$
    (fg)(A) = f(A)g(A).
$$

This implies that for any $$\psi \in \mathbf{H}$$ we have

$$
    \left< \psi, (fg)(A)\psi \right> = \left< \psi, f(A)g(A)\psi \right>.
$$

Now the [**Definition**](#def:hall-8.8) implies that the operator $$(fg)(A)$$ satisfies

$$
    Q_{fg}(\psi) = \left< \psi, (fg)(A)\psi \right>
$$

for all $$\psi \in \mathbf{H}$$.

In addition the [**Definition**](#def:hall-8.8) and the previous result allowing us to express $$L_f$$ in terms of $$Q_f$$ gives

$$
    L_f(\phi, \psi) = \left< \phi, f(A)\psi\right>.
$$

Hence, we have 

$$
    \left< \psi, f(A)g(A)\psi \right> = L_f(\psi, g(A)\psi).
$$

Thus $$\left< \psi, (fg)(A)\psi \right> = \left< \psi, f(A)g(A)\psi \right>$$ implies

$$
    Q_{fg}(\psi) = L_f(\psi, g(A)\psi)
$$

for all $$\psi \in \mathbf{H}$$, all $$f \in \mathcal{F}_1$$, and all $$g \in C^0(\sigma(A); \mathbb{R})$$.
$$\blacksquare$$

> **Proposition** *($$\mathcal{F}_1$$ is Closed under Bounded Pointwise Limits)*
<a name="prpstn:F1-closed-under-limits"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{def:F1-F2-classes} -->
<!--  \uses{prpstn:F1-vector-space} -->
<!--  \uses{prpstn:Q-continuous-under-limits} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mathcal{F}_1$$ as in [Definition (The Classes $$\mathcal{F}_1$$ and $$\mathcal{F}_2$$)](#def:F1-F2-classes), if $$\{f_i\}$$ is a uniformly bounded sequence in $$\mathcal{F}_1$$ converging pointwise to $$f$$, then $$f \in \mathcal{F}_1$$. Consequently, by [**Lemma** *(hall-prblm-8.3.3c)*](#lmm:hall-prblm-8.3.3c), $$\mathcal{F}_1$$ is the set of *all* bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$ — that is, $$(fg)(A) = f(A)g(A)$$ for every bounded Borel $$f$$ and every continuous $$g$$.

**Proof**
We show that $$\mathcal{F}_1$$ is closed under pointwise limits of uniformly bounded sequences.

To this end let $$\{ f_i \}_{i \in \mathbb{N}}$$ be a sequence in $$\mathcal{F}_1$$, uniformly bounded by some $$M \in \mathbb{R}$$, that converges pointwise to a function $$f$$ on $$\sigma(A)$$. By [**Lemma** *(Pointwise Limits of Uniformly Bounded, Borel-Measurable Functions)*](#lmm:pointwise-limits-of-borel-measurable-functions), $$f$$ is itself a bounded, Borel-measurable, complex-valued function on $$\sigma(A)$$, and so is a candidate for membership in $$\mathcal{F}_1$$. Let $$g \in C^0(\sigma(A); \mathbb{R})$$ and $$\psi \in \mathbf{H}$$ be arbitrary.

As each $$f_i$$ belongs to $$\mathcal{F}_1$$, the identity established above gives

$$
    Q_{f_i g}(\psi) = L_{f_i}(\psi, g(A)\psi)
$$

for every $$i \in \mathbb{N}$$. We now take the limit $$i \rightarrow \infty$$ of each side separately.

For the lefthand side, note first that as $$\sigma(A)$$ is compact by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable) and $$g$$ is continuous, the [**Boundedness Theorem**](#thrm:boundedness-theorem) implies $$g$$ is bounded, say by $$M_g \in \mathbb{R}$$. As $$f_i \rightarrow f$$ pointwise we have $$f_i g \rightarrow fg$$ pointwise, and

$$
    \lvert f_i(\lambda) g(\lambda) \rvert \le M M_g
$$

for all $$i \in \mathbb{N}$$ and all $$\lambda \in \sigma(A)$$, so the sequence $$\{ f_i g \}_{i \in \mathbb{N}}$$ is uniformly bounded. Hence, the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem), applied to the measure $$\mu_\psi$$, which is finite by [**Lemma** *(The Associated Measures are Finite)*](#lmm:associated-measures-are-finite), gives 

$$
    Q_{f_i g}(\psi) = \int_{\sigma(A)} f_i g \, d\mu_\psi \longrightarrow \int_{\sigma(A)} fg \, d\mu_\psi = Q_{fg}(\psi).
$$

For the righthand side, recall we proved above that the map $$h \mapsto L_h(\phi, \psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\phi, \psi \in \mathbf{H}$$. Applying this to the uniformly bounded sequence $$\{ f_i \}_{i \in \mathbb{N}}$$ converging pointwise to $$f$$, with the fixed vectors $$\psi$$ and $$g(A)\psi$$, gives

$$
    L_{f_i}(\psi, g(A)\psi) \longrightarrow L_f(\psi, g(A)\psi).
$$

As a sequence in $$\mathbb{C}$$ has at most one limit, these two computations give

$$
    Q_{fg}(\psi) = L_f(\psi, g(A)\psi).
$$

Now, by [**Definition**](#def:hall-8.8) the lefthand side satisfies $$Q_{fg}(\psi) = \left< \psi, (fg)(A)\psi \right>$$, while the righthand side satisfies $$L_f(\psi, g(A)\psi) = \left< \psi, f(A)g(A)\psi \right>$$ by the expression for $$L_f$$ obtained above. Hence,

$$
    \left< \psi, (fg)(A)\psi \right> = \left< \psi, f(A)g(A)\psi \right>
$$

for all $$\psi \in \mathbf{H}$$. As both $$(fg)(A)$$ and $$f(A)g(A)$$ are elements of $$\mathcal{B}(\mathbf{H})$$, the uniqueness clause of [**Proposition**](#prpstn:hall-a.63), applied to the bounded quadratic form $$Q_{fg}$$, implies

$$
    (fg)(A) = f(A)g(A).
$$

As $$g$$ was an arbitrary element of $$C^0(\sigma(A); \mathbb{R})$$, this is precisely the statement that $$f \in \mathcal{F}_1$$. Thus $$\mathcal{F}_1$$ is closed under pointwise limits of uniformly bounded sequences.

As $$\sigma(A)$$ is a compact metric measurable space by [**Lemma**](#lmm:spectrum-is-compact-metric-measurable) and $$\mathcal{F}_1$$ (1) is a vector space, (2) contains $$C^0(\sigma(A); \mathbb{R})$$, and (3) is closed under uniformly bounded pointwise limits, we can apply [**Lemma**](#lmm:hall-prblm-8.3.3c) to conclude that $$\mathcal{F}_1$$ consists of all bounded, Borel-measurable functions on $$\sigma(A)$$.
$$\blacksquare$$

> **Proposition** *($$\mathcal{F}_2$$ Contains all Bounded Borel Functions)*
<a name="prpstn:F2-is-everything"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{def:F1-F2-classes} -->
<!--  \uses{prpstn:F1-closed-under-limits} -->
<!--  \uses{prpstn:Q-continuous-under-limits} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mathcal{F}_2$$ as in [Definition (The Classes $$\mathcal{F}_1$$ and $$\mathcal{F}_2$$)](#def:F1-F2-classes), $$\mathcal{F}_2$$ is a complex vector space, contains $$C^0(\sigma(A); \mathbb{R})$$, and is closed under bounded pointwise limits; hence it is the set of *all* bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$.

**Proof**
By [**Proposition** *($$\mathcal{F}_1$$ is Closed under Bounded Pointwise Limits)*](#prpstn:F1-closed-under-limits), we have multiplicativity for an arbitrary bounded, Borel-measurable $$f$$ paired with a *continuous* $$g$$. To obtain the full result we must also allow $$g$$ to be an arbitrary bounded, Borel-measurable function. To this end recall $$\mathcal{F}_2$$ from [Definition (The Classes $$\mathcal{F}_1$$ and $$\mathcal{F}_2$$)](#def:F1-F2-classes) — note that there it is the *second* argument that varies. We will prove that $$\mathcal{F}_2$$ (1) is a complex vector space, (2) contains $$C^0(\sigma(A); \mathbb{R})$$, and (3) is closed under pointwise limits of uniformly bounded sequences, so that [**Lemma**](#lmm:hall-prblm-8.3.3c) applies.

**(1)** Consider any $$g_1$$ and $$g_2$$ in $$\mathcal{F}_2$$, any $$\alpha_1$$ and $$\alpha_2$$ in $$\mathbb{C}$$, and any bounded, Borel-measurable $$f$$. Then

$$
\begin{align}
    (f(\alpha_1g_1 + \alpha_2g_2))(A) &= (\alpha_1(fg_1) + \alpha_2(fg_2))(A) \\
                                      &= \alpha_1(fg_1)(A) + \alpha_2(fg_2)(A) \\
                                      &= \alpha_1f(A)g_1(A) + \alpha_2f(A)g_2(A) \\
                                      &= f(A)\left( \alpha_1g_1(A) + \alpha_2g_2(A) \right) \\
                                      &= f(A)(\alpha_1g_1 + \alpha_2g_2)(A),
\end{align}
$$

where the first line is the distributive property over functions, the second and fifth follow from linearity of the map of [**Definition**](#def:hall-8.8), the third from $$g_1, g_2 \in \mathcal{F}_2$$, and the fourth is the distributive property over operators. Hence $$\alpha_1g_1 + \alpha_2g_2 \in \mathcal{F}_2$$, i.e. $$\mathcal{F}_2$$ is a complex vector space.

**(2)** Let $$g \in C^0(\sigma(A); \mathbb{R})$$. Membership of $$g$$ in $$\mathcal{F}_2$$ requires that $$(fg)(A) = f(A)g(A)$$ for every bounded, Borel-measurable $$f$$. This is precisely the statement that every such $$f$$ belongs to $$\mathcal{F}_1$$, which we established above. Hence $$C^0(\sigma(A); \mathbb{R}) \subseteq \mathcal{F}_2$$.

**(3)** Let $$\{ g_i \}_{i \in \mathbb{N}}$$ be a sequence in $$\mathcal{F}_2$$, uniformly bounded by some $$M \in \mathbb{R}$$, converging pointwise to $$g$$. Let $$f$$ be an arbitrary bounded, Borel-measurable, complex-valued function on $$\sigma(A)$$, bounded by $$M_f \in \mathbb{R}$$, and let $$\psi \in \mathbf{H}$$ be arbitrary.

As $$g_i \rightarrow g$$ pointwise, we have $$fg_i \rightarrow fg$$ pointwise, and

$$
    \lvert f(\lambda)g_i(\lambda) \rvert \le M_f M
$$

for all $$i \in \mathbb{N}$$ and all $$\lambda \in \sigma(A)$$, so the sequence $$\{ fg_i \}_{i \in \mathbb{N}}$$ is uniformly bounded. Hence, the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem), applied to the measure $$\mu_\psi$$, which is finite by [**Lemma** *(The Associated Measures are Finite)*](#lmm:associated-measures-are-finite), gives 

$$
\begin{align}
    \left< \psi, (fg_i)(A)\psi \right> &= Q_{fg_i}(\psi) \\
                &= \int_{\sigma(A)} fg_i \, d\mu_\psi \longrightarrow \int_{\sigma(A)} fg \, d\mu_\psi \\
                &= Q_{fg}(\psi) \\
                &= \left< \psi, (fg)(A)\psi \right>.
\end{align}
$$

On the other hand, as each $$g_i$$ is in $$\mathcal{F}_2$$ we have $$(fg_i)(A) = f(A)g_i(A)$$, and thus

$$
    \left< \psi, (fg_i)(A)\psi \right> = \left< \psi, f(A)g_i(A)\psi \right> = \left< f(A)^*\psi, g_i(A)\psi \right>,
$$

where $$f(A)^*$$ is the adjoint of the bounded operator $$f(A)$$. Recall we established above that for any bounded, Borel-measurable, complex-valued function $$h$$ the sesquilinear form $$L_h$$ associated to $$Q_h$$ satisfies $$L_h(\phi, \psi) = \left< \phi, h(A)\psi \right>$$, and that the map $$h \mapsto L_h(\phi, \psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\phi, \psi \in \mathbf{H}$$. Applying this with $$\phi = f(A)^*\psi$$ to the uniformly bounded sequence $$\{ g_i \}_{i \in \mathbb{N}}$$ converging pointwise to $$g$$ gives

$$
\begin{align}
    \left< f(A)^*\psi, g_i(A)\psi \right> &= L_{g_i}(f(A)^*\psi, \psi) \longrightarrow L_g(f(A)^*\psi, \psi) \\
                &= \left< f(A)^*\psi, g(A)\psi \right> \\
                &= \left< \psi, f(A)g(A)\psi \right>.
\end{align}
$$

As a sequence in $$\mathbb{C}$$ has at most one limit, the two computations give

$$
    \left< \psi, (fg)(A)\psi \right> = \left< \psi, f(A)g(A)\psi \right>
$$

for all $$\psi \in \mathbf{H}$$. Both $$(fg)(A)$$ and $$f(A)g(A)$$ are elements of $$\mathcal{B}(\mathbf{H})$$, so by the uniqueness clause of [**Proposition**](#prpstn:hall-a.63) applied to the bounded quadratic form $$Q_{fg}$$ we conclude

$$
    (fg)(A) = f(A)g(A).
$$

As $$f$$ was arbitrary, $$g \in \mathcal{F}_2$$, and thus $$\mathcal{F}_2$$ is closed under pointwise limits of uniformly bounded sequences.

As $$\sigma(A)$$ is a compact metric measurable space by [**Lemma**](#lmm:spectrum-is-compact-metric-measurable) and $$\mathcal{F}_2$$ (1) is a vector space, (2) contains $$C^0(\sigma(A); \mathbb{R})$$, and (3) is closed under uniformly bounded pointwise limits, we can apply [**Lemma**](#lmm:hall-prblm-8.3.3c) to conclude that $$\mathcal{F}_2$$ consists of all bounded, Borel-measurable, complex-valued functions on $$\sigma(A)$$. This is none other than the desired result

$$
    (fg)(A) = f(A)g(A)
$$

for all bounded, Borel-measurable, complex-valued functions $$f$$ and $$g$$ on $$\sigma(A)$$.$$\blacksquare$$



#### The Spectral Measure

In what is the penultimate result required to prove the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators) we present the following theorem that covers all of the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators) except uniqueness of the projection-valued measure $$\mu^A$$.

> **Theorem** *(The Spectral Measure of a Self-Adjoint Operator)*
<a name="thrm:hall-8.10"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:Q-continuous-under-limits} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{prpstn:integral-multiplicative} -->
<!--  \uses{prpstn:integral-norm-bound} -->
<!--  \uses{prpstn:mua-countably-additive} -->
<!--  \uses{prpstn:mua-empty-and-whole} -->
<!--  \uses{prpstn:mua-integrates-to-A} -->
<!--  \uses{prpstn:mua-multiplicative} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{prpstn:orthogonal-sum-converges} -->
<!--  \uses{prpstn:orthogonal-sum-is-projection} -->
<!--  \uses{prpstn:orthogonal-sum-range} -->
<!--  \uses{prpstn:pvm-agree-on-continuous} -->
<!--  \uses{prpstn:pvm-agree-on-measurable} -->
<!--  \uses{prpstn:pvm-agree-on-polynomials} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{thrm:hall-prblm-8.3.4} -->
<!--  \uses{thrm:monotone-convergence-theorem} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{lmm:lemma-3} -->
<!--  \uses{prpstn:hall-8.9} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{lmm:lemma-4} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Suppose $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint. For any measurable subset $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$, define the operator $$\mu^A(E)$$ by
> 
> $$
>     \mu^A(E) \equiv 1_E(A),
> $$
> 
> where $$1_E(A)$$ is the operator associated to the indicator function $$1_E$$ on $$\sigma(A)$$ by way of [**Definition**](#def:hall-8.8). Then $$\mu^A$$ is a projection-valued measure on $$\sigma(A)$$ and satisfies
> 
> $$
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
> $$

**Proof**
This proof broadly consists of two parts **Part 1:** prove that $$\mu^A$$ is a projection valued measure on $$\sigma(A)$$ and **Part 2:** prove that $$\mu^A$$ satisfies

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
$$
**Proof**
That $$\mu^A$$ is a projection-valued measure is the conjunction of the four axioms of the [definition](#def:projection-valued-measure), established in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), [**Proposition** *(Spectral Projections Multiply to the Intersection)*](#prpstn:mua-multiplicative), [**Proposition** *(Spectral Projections of the Empty Set and the Whole Spectrum)*](#prpstn:mua-empty-and-whole) and [**Proposition** *(Spectral Projections are Countably Additive)*](#prpstn:mua-countably-additive). The integral identity is [**Proposition** *(The Spectral Measure Integrates to the Operator)*](#prpstn:mua-integrates-to-A).$$\blacksquare$$

> **Proposition** *(Each Spectral Projection is an Orthogonal Projection)*
<a name="prpstn:mua-projection"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{lmm:lemma-3} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{prpstn:hall-8.9} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and, for measurable $$E \subseteq \sigma(A)$$, define $$\mu^A(E) \equiv 1_E(A)$$, where $$1_E(A)$$ is given by [**Definition**](#def:hall-8.8). Then $$\mu^A(E)$$ is a bounded orthogonal projection.

**Proof**
for each measurable set $$E$$ on $$\sigma(A)$$ it follows that $$\mu^A(E)$$ is a bounded orthogonal projection.

To this end, first let us note that as a result of [**Lemma**](#lmm:lemma-3) for any measurable subset $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$ the fact that $$1_E$$ is a bounded, Borel-measurable, real-valued function on $$\sigma(A)$$ allows us to conclude that $$1_E(A)$$ is self-adjoint.

Next note that the fact that $$1_E 1_E = 1_E$$ allows us to conclude that

$$
    (1_E1_E)(A) = 1_E(A).
$$

At the same time the [**Proposition**](#prpstn:hall-8.9) implies

$$
    (1_E1_E)(A) = 1_E(A)1_E(A).
$$

Together these imply

$$
    1_E(A)1_E(A) = 1_E(A).
$$

By way of the orthogonal projection [**Definition**](#def:bounded-orthogonal-projection) the fact that $$1_E(A)$$ is a bounded, self-adjoint operator that satisfies $$1_E(A)1_E(A) = 1_E(A)$$ implies that $$1_E(A)$$ is an orthogonal projection. Hence,

$$
    \mu^A(E) \equiv 1_E(A)
$$

is also an orthogonal projection for any measurable subset $$E$$ of the spectrum $$\sigma(A)$$, as required.
$$\blacksquare$$

> **Proposition** *(Spectral Projections Multiply to the Intersection)*
<a name="prpstn:mua-multiplicative"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{prpstn:hall-8.9} -->
<!--  \uses{def:indicator-function} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), for any measurable $$E_1, E_2 \subseteq \sigma(A)$$,
>
> $$
>     \mu^A(E_1)\mu^A(E_2) = \mu^A(E_1 \cap E_2).
> $$

**Proof**
for any measurable sets $$E_1$$ and $$E_2$$ on $$\sigma(A)$$ that $$\mu^A(E_1 \cap E_2) = \mu^A(E_1) \mu^A(E_2)$$.

So to this end, consider any two measurable subsets $$E_1$$ and $$E_2$$ of the spectrum $$\sigma(A)$$. Tracing definitions one has

$$
    1_{E_1 \cap E_2} = 1_{E_1} 1_{E_2}.
$$

Using the definition of $$\mu^A$$ this implies

$$
\begin{align}
    \mu^A(E_1 \cap E_2) &\equiv 1_{E_1 \cap E_2}(A) \\
                         &=      (1_{E_1} 1_{E_2})(A) \\
                         &=      1_{E_1}(A) 1_{E_2}(A) \\
                         &=      \mu^A(E_1) \mu^A(E_2),
\end{align}
$$

where the second line follows from the previous equation, the third from [**Proposition**](#prpstn:hall-8.9), and the final from the definition of $$\mu^A$$. Hence,

$$
    \mu^A(E_1 \cap E_2) = \mu^A(E_1) \mu^A(E_2),
$$

as required.
$$\blacksquare$$

> **Proposition** *(Spectral Projections of the Empty Set and the Whole Spectrum)*
<a name="prpstn:mua-empty-and-whole"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{prpstn:hall-8.9} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), 
>
> $$
>     \mu^A(\emptyset) = 0 \qquad\text{and}\qquad \mu^A(\sigma(A)) = \mathbf{1}.
> $$

**Proof**
$$\mu^A(\emptyset) = 0$$, where $$\emptyset$$ is the empty set, and $$\mu^A(\sigma(A)) = \mathbf{1}$$, where $$\mathbf{1}$$ is the multiplicative identity element.

To this end, consider the empty set $$\emptyset$$ which is a measurable subset of the spectrum $$\sigma(A)$$. Tracing definitions one has

$$
    1_\emptyset = 0.
$$

[**Definition**](#def:hall-8.8) then implies

$$
\begin{align}
    \left< \psi, 1_\emptyset(A)\psi \right> &= \int_{\sigma(A)} 1_\emptyset(\lambda) \, d\mu_\psi(\lambda) \\
                                            &= \int_{\sigma(A)} 0 \, d\mu_\psi(\lambda) \\
                                            &= 0,
\end{align}
$$

for all $$\psi \in \mathbf{H}$$. So as

$$
    \left< \psi, 1_\emptyset(A)\psi \right> = 0
$$

is true for any $$\psi$$ in $$\mathbf{H}$$ we conclude that $$1_\emptyset(A)$$ is the zero operator.

However, by definition

$$
    \mu^A(\emptyset) \equiv 1_\emptyset(A).
$$

Thus, $$\mu^A(\emptyset)$$ is the zero operator, the first of the two desired results.

Now consider the measurable set $$\sigma(A)$$, the entire spectrum. Tracing definitions

$$
    1_{\sigma(A)} = 1.
$$

[**Definition**](#def:hall-8.8) then implies for all $$\psi \in \mathbf{H}$$ that

$$
\begin{align}
    \left< \psi, 1_{\sigma(A)}(A)\psi \right> &= \int_{\sigma(A)} 1_{\sigma(A)}(\lambda) \, d\mu_\psi(\lambda) \\
                                              &= \int_{\sigma(A)} 1 \, d\mu_\psi(\lambda) \\
                                              &= \mu_\psi(\sigma(A)) \\
                                              &= \Lambda_\psi(\mathbf{1}) \\
                                              &= \left< \psi, \psi \right>,
\end{align}
$$

where the fourth line follows from the definition of $$\mu_\psi$$ in terms of our map $$\Lambda_\psi$$ by way of the [**Riesz Representation Theorem**](#thrm:riesz-representation) and the final line follows from the definition of $$\Lambda_\psi$$. So for any $$\psi \in \mathbf{H}$$ we have

$$
    \left< \psi, 1_{\sigma(A)}(A)\psi \right> = \left< \psi, \psi \right>,
$$

which implies that

$$
    1_{\sigma(A)}(A) = \mathbf{1}.
$$ 

By definition

$$
    \mu^A(\sigma(A)) \equiv 1_{\sigma(A)}(A).
$$

Hence, we have proven

$$
    \mu^A(\sigma(A)) = \mathbf{1},
$$

the second, as required.
$$\blacksquare$$

> **Proposition** *(Spectral Projections are Countably Additive)*
<a name="prpstn:mua-countably-additive"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:Q-continuous-under-limits} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{prpstn:orthogonal-sum-converges} -->
<!--  \uses{prpstn:orthogonal-sum-is-projection} -->
<!--  \uses{prpstn:orthogonal-sum-range} -->
<!--  \uses{thrm:monotone-convergence-theorem} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{prpstn:mua-multiplicative} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{lmm:lemma-4} -->
<!--  \uses{prpstn:hall-8.9} -->
<!--  \uses{prpstn:mua-empty-and-whole} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), for pairwise disjoint measurable sets $$\{E_j\}$$ in $$\sigma(A)$$ and any $$\psi \in \mathbf{H}$$,
>
> $$
>     \mu^A\left( \bigcup_{j=1}^{\infty} E_j \right)\psi = \sum_{j=1}^{\infty} \mu^A(E_j)\psi,
> $$
>
> the sum converging in the norm topology on $$\mathbf{H}$$.

**Proof**
for pairwise disjoint measurable sets $$\{ E_i \}_{i \in \mathbb{N}}$$ on $$\sigma(A)$$ and any $$\psi \in \mathbf{H}$$ we have

$$
    \mu^A \left( \bigcup_{j = 1}^{\infty} E_j \right) \psi = \sum_{j = 1}^{\infty} \mu(E_j)\psi,
$$

where the convergence of the sum is in the norm topology on $$\mathbf{H}$$.

In order to prove this, consider now any two disjoint measurable subsets $$E_1$$ and $$E_2$$ of the spectrum $$\sigma(A)$$. The definition of $$\mu^A$$ along with [**Proposition** *(Spectral Projections of the Empty Set and the Whole Spectrum)*](#prpstn:mua-empty-and-whole) implies

$$
\begin{align}
    \mu^A(E_1 \cap E_2) &= \mu^A(\emptyset) \\
                        &\equiv 1_\emptyset(A) \\
                        &= 0,
\end{align}
$$

where the first line follows from the fact that $$E_1$$ and $$E_2$$ are disjoint and the final line follows from [**Proposition** *(Spectral Projections of the Empty Set and the Whole Spectrum)*](#prpstn:mua-empty-and-whole), which gives that $$1_\emptyset(A)$$ is the zero operator.

However, by [**Proposition** *(Spectral Projections Multiply to the Intersection)*](#prpstn:mua-multiplicative), for arbitrary measurable subsets $$E_1$$ and $$E_2$$ of the spectrum $$\sigma(A)$$ of $$A$$

$$
    \mu^A(E_1) \mu^A(E_2) = \mu^A(E_1 \cap E_2).
$$

So if $$E_1$$ and $$E_2$$ are disjoint, this result along with the last result imply

$$
    \mu^A(E_1) \mu^A(E_2) = \mu^A(E_1 \cap E_2) = \mu^A(\emptyset) = 0.
$$

So if $$E_1$$ and $$E_2$$ are disjoint, then

$$
    \mu^A(E_1) \mu^A(E_2) = 0.
$$

As $$\mu^A(E_1)$$ is self-adjoint, this implies that for arbitrary $$\phi$$ and $$\psi$$ in $$\mathbf{H}$$ one has

$$
\begin{align}
    0 &= \left< \phi, \mu^A(E_1) \mu^A(E_2)\psi \right> \\
      &= \left< \phi, \mu^A(E_1)^* \mu^A(E_2)\psi \right> \\
      &= \left< \mu^A(E_1)\phi, \mu^A(E_2)\psi \right>,
\end{align}
$$

which is nothing more than the statement that for disjoint $$E_1$$ and $$E_2$$ and arbitrary $$\phi$$ and $$\psi$$ in $$\mathbf{H}$$ we have

$$
    \left< \mu^A(E_1)\phi, \mu^A(E_2)\psi \right> = 0,
$$

i.e. the ranges of $$\mu^A(E_1)$$ and $$\mu^A(E_2)$$ are orthogonal.

The next lemma uses the Monotone Convergence Theorem for real sequences, which we state first.

> **Theorem** *(Monotone Convergence Theorem)*
<a name="thrm:monotone-convergence-theorem"></a>
> Let $$\{ a_n \}_{n \in \mathbb{N}}$$ be a monotone sequence of real numbers (either $$a_n \le a_{n+1}$$ or $$a_n \ge a_{n+1}$$ for all $$n$$). Then the sequence $$\{ a_n \}_{n \in \mathbb{N}}$$ has a finite limit in $$\mathbb{R}$$ if and only if $$\{ a_n \}_{n \in \mathbb{N}}$$ is bounded.

With this result as motivation, let us prove the following "utility" lemma

> **Lemma** *(Sums of Pairwise Orthogonal Projections)*
<a name="lmm:lemma-4"></a>
<!--  \uses{prpstn:orthogonal-sum-converges} -->
<!--  \uses{prpstn:orthogonal-sum-is-projection} -->
<!--  \uses{prpstn:orthogonal-sum-range} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{thrm:monotone-convergence-theorem} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
> Let $$\{ P_i \}_{i \in \mathbb{N}}$$ be a set of bounded orthogonal projections on a separable, complex Hilbert space $$\mathbf{H}$$ that satisfy $$P_iP_j = 0$$ for $$i \neq j$$. Then for all $$\psi \in \mathbf{H}$$ the sequence of partial sums
> 
> $$
>     S_n\psi \equiv \sum_{i = 0}^n P_i\psi
> $$
> 
> converges to $$P\psi$$ where $$P$$ is a bounded orthogonal projection onto the smallest closed subspace containing the range of the $$P_i$$.

**Proof**
Convergence of the partial sums is [**Proposition** *(Partial Sums of Pairwise Orthogonal Projections Converge)*](#prpstn:orthogonal-sum-converges); that the limit map $$P$$ is a bounded orthogonal projection is [**Proposition** *(The Limit of the Partial Sums is a Bounded Orthogonal Projection)*](#prpstn:orthogonal-sum-is-projection); and that its range is the smallest closed subspace containing the ranges of the $$P_i$$ is [**Proposition** *(The Range of the Limit Projection)*](#prpstn:orthogonal-sum-range).$$\blacksquare$$

> **Proposition** *(Partial Sums of Pairwise Orthogonal Projections Converge)*
<a name="prpstn:orthogonal-sum-converges"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{lmm:projection-norm-decreasing} -->
<!--  \uses{thrm:monotone-convergence-theorem} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
> Let $$\{ P_i \}_{i \in \mathbb{N}}$$ be bounded orthogonal projections on a separable, complex Hilbert space $$\mathbf{H}$$ with $$P_iP_j = 0$$ for $$i \ne j$$. Then for every $$\psi \in \mathbf{H}$$ the sequence of partial sums $$S_n\psi \equiv \sum_{i=0}^n P_i\psi$$ converges in $$\mathbf{H}$$. We write $$P\psi$$ for its limit.

**Proof**
the sequence of partial sums $$S_n\psi$$ converges.

To this end for an arbitrary $$\psi \in \mathbf{H}$$ let us first examine the norm of the partial sum $$S_n\psi$$

$$
\begin{align}
    \left\| S_n\psi \right\|^2 &= \left\| \sum_{i = 0}^n P_i\psi \right\|^2 \\
                               &= \left< \sum_{i = 0}^n P_i\psi, \sum_{j = 0}^n P_j\psi \right> \\
                               &= \sum_{i = 0}^n \left< P_i\psi, P_i\psi \right> \\
                               &= \sum_{i = 0}^n \left\| P_i\psi \right\|^2,
\end{align}
$$

where on the third line we made use of the fact that $$P_iP_j = 0$$ if $$i \neq j$$. So we have proven

$$
    \left\| S_n\psi \right\|^2 = \sum_{i = 0}^n \left\| P_i\psi \right\|^2.
$$

Next we bound $$\left\| S_n\psi \right\|$$ by $$\left\| \psi \right\|$$. This is not immediate from $$P_iP_j = 0$$ alone; it follows because the operator $$S_n \equiv \sum_{i=0}^n P_i$$ is itself a bounded orthogonal projection. Indeed, $$S_n$$ is a finite sum of elements of $$\mathcal{B}(\mathbf{H})$$ and so lies in $$\mathcal{B}(\mathbf{H})$$; it is self-adjoint, since

$$
    S_n^* = \left( \sum_{i=0}^n P_i \right)^* = \sum_{i=0}^n P_i^* = \sum_{i=0}^n P_i = S_n,
$$

each $$P_i$$ being self-adjoint by the [definition of an orthogonal projection](#def:bounded-orthogonal-projection); and it is idempotent, since

$$
    S_n^2 = \sum_{i=0}^n \sum_{j=0}^n P_iP_j = \sum_{i=0}^n P_i^2 = \sum_{i=0}^n P_i = S_n,
$$

where the cross terms vanish by the hypothesis $$P_iP_j = 0$$ for $$i \ne j$$ and the diagonal terms satisfy $$P_i^2 = P_i$$ by that same definition. So $$S_n$$ is a bounded orthogonal projection, and [**Lemma** *(Orthogonal Projections are Norm-Decreasing)*](#lmm:projection-norm-decreasing) gives

$$
    \left\| S_n\psi \right\|^2 \le \|\psi\|^2.
$$

These last two results then imply

$$
    \sum_{i = 0}^n \left\| P_i\psi \right\|^2 = \left\| S_n\psi \right\|^2 \le \|\psi\|^2.
$$

Which implies

$$
    \sum_{i = 0}^n \left\| P_i\psi \right\|^2 \le \|\psi\|^2.
$$

As $$\|\psi\|^2 < \infty$$ and $$0 \le \|P_i\psi\|^2$$ for all $$i \in \mathbb{N}$$, this implies that for any $$\psi \in \mathbf{H}$$ the sequence $$\{ a_n(\psi) \}_{n \in \mathbb{N}}$$ where $$a_n(\psi)$$ is defined by

$$
    a_n(\psi) \equiv \sum_{i = 0}^n \left\| P_i\psi \right\|^2
$$

in a bounded, monotonically increasing sequence of real numbers. Thus the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem) implies that the bounded, monotonically increasing sequence of real numbers

$$
    a_n(\psi) \equiv \sum_{i = 0}^n \left\| P_i\psi \right\|^2
$$

has a finite limit in $$\mathbb{R}$$ for any $$\psi \in \mathbf{H}$$.

For an arbitrary $$\psi \in \mathbf{H}$$ consider again the sequence 

$$
    S_n\psi \equiv \sum_{i = 0}^n P_i\psi.
$$

Using the result we just established, we will now prove that this sequence converges, which is the assertion of this proposition.

We will do so by employing the fact that $$\mathbf{H}$$ being a Hilbert space implies that $$\mathbf{H}$$ is also a Banach space. Thus, a Cauchy sequence in $$\mathbf{H}$$ converges in $$\mathbf{H}$$. So, if we can prove the sequence $$S_n\psi$$ is a Cauchy sequence, then we can conclude it converges.

To that end, consider $$n, m \in \mathbb{N}$$ and without loss of generality assume that $$n > m$$. One has

$$
    \left\| S_n\psi - S_m \psi \right\|^2 = \left\| \sum_{i=m+1}^n P_i\psi \right\|^2 = \sum_{i = m+1}^n \|P_i\psi\|^2,
$$

where the final equality follows from $$P_iP_j = 0$$ when $$i \neq j$$. Now as we proved the sequence

$$
    a_n(\psi) \equiv \sum_{i = 0}^n \left\| P_i\psi \right\|^2
$$

converges, it follows that as $$n,m \rightarrow \infty$$ the tail sum goes to zero

$$
    \sum_{i = m+1}^n \|P_i\psi\|^2 \rightarrow 0.
$$

This then implies that as $$n,m \rightarrow \infty$$ one has

$$
    \left\| S_n\psi - S_m \psi \right\| \rightarrow 0.
$$

In other words $$S_n\psi$$ is a Cauchy sequence.

As $$S_n\psi$$ is a Cauchy sequence and $$\mathbf{H}$$ is a Hilbert, and thus a Banach space, this implies that $$S_n\psi$$ converges to some element in $$\mathbf{H}$$. This and linearity allows us to define a linear operator $$P$$ by

$$
    P\psi \equiv \lim\limits_{n \rightarrow \infty} S_n\psi.
$$
$$\blacksquare$$

> **Proposition** *(The Limit of the Partial Sums is a Bounded Orthogonal Projection)*
<a name="prpstn:orthogonal-sum-is-projection"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:orthogonal-sum-converges} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:continuity-of-norm-and-inner-product} -->
> With $$\{P_i\}$$ and $$P$$ as in [**Proposition** *(Partial Sums of Pairwise Orthogonal Projections Converge)*](#prpstn:orthogonal-sum-converges), the map $$\psi \mapsto P\psi$$ is a bounded orthogonal projection on $$\mathbf{H}$$: it lies in $$\mathcal{B}(\mathbf{H})$$, is self-adjoint, and satisfies $$PP = P$$.

**Proof**
the sequence limit $$P\psi$$ defines a bounded orthogonal projection operator $$P$$. To prove that $$P$$ is a bounded orthogonal projection operator we must **Part 2.1:** prove that $$P$$ is an element of $$\mathcal{B}(\mathbf{H})$$, **Part 2.2:** prove that $$P$$ is self-adjoint, and **Part 2.3:** prove that $$PP=P$$.

**Part 2.1:** Next let us prove that $$P$$ is an element of $$\mathcal{B}(\mathbf{H})$$.

By definition

$$
    P\psi = \lim\limits_{n \rightarrow \infty} S_n\psi = \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n P_i\psi.
$$

As the $$P_i$$ are elements in $$\mathcal{B}(\mathbf{H})$$ they are linear. This then implies that $$P$$ is linear.

Recall we previously proved that for any $$n$$ in $$\mathbb{N}$$ one has

$$
    \left\| \sum_{i = 0}^n P_i\psi \right\|^2 \le \|\psi\|^2.
$$

Thus for any unit norm $$\psi$$, i.e. $$\psi$$ such that $$\|\psi\| = 1$$, we have

$$
    \left\| \sum_{i = 0}^n P_i\psi \right\|^2  \le 1
$$

and thus

$$
    \left\| \sum_{i = 0}^n P_i\psi \right\|  \le 1.
$$

for arbitrary $$n \in \mathbb{N}$$.

Now the operator norm $$\|P\|$$ of $$P$$ is defined by

$$
    \|P\| \equiv \sup\limits_{\|\psi\| = 1} \|P\psi\|.
$$

Hence, the definition of $$P$$ along with our previous result and Part 1 of [**Proposition** *(Continuity of the Norm and Inner Product)*](#prpstn:continuity-of-norm-and-inner-product), which permits the exchange of the norm with the limit, implies

$$
\begin{align}
    \|P\| &=   \sup\limits_{\|\psi\| = 1} \left\|P\psi\right\| \\
          &=   \sup\limits_{\|\psi\| = 1} \left\|\lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n P_i\psi\right\| \\
          &=   \sup\limits_{\|\psi\| = 1} \lim\limits_{n \rightarrow \infty} \left\|\sum_{i = 0}^n P_i\psi\right\| \\
          &\le \sup\limits_{\|\psi\| = 1} \lim\limits_{n \rightarrow \infty} 1 \\
          &=   1.
\end{align}
$$

Thus $$\|P\| \le 1$$, proving that $$P$$ is bounded and thus an element of $$\mathcal{B}(\mathbf{H})$$, as required.

**Part 2.2:** Next let us prove that $$P$$ is self-adjoint. It turns out this follows directly from the fact that each of the $$P_i$$ is self-adjoint.

Tracing definitions, and using Part 2 of [**Proposition** *(Continuity of the Norm and Inner Product)*](#prpstn:continuity-of-norm-and-inner-product) to exchange the inner product with the limit, one has for arbitrary $$\phi, \psi \in \mathbf{H}$$

$$
\begin{align}
    \left< P\phi, \psi \right> &= \left< \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n P_i\phi, \psi \right> \\
                               &= \lim\limits_{n \rightarrow \infty} \left< \sum_{i = 0}^n P_i\phi, \psi \right> \\
                               &= \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n \left< P_i\phi, \psi \right> \\
                               &= \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n \left< P_i^*\phi, \psi \right> \\
                               &= \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n \left< \phi, P_i\psi \right> \\
                               &= \lim\limits_{n \rightarrow \infty} \left< \phi, \sum_{i = 0}^n P_i\psi \right> \\
                               &= \left< \phi, \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n P_i\psi \right> \\
                               &= \left< \phi, P\psi \right>,
\end{align}
$$

proving

$$
    \left< P\phi, \psi \right> = \left< \phi, P\psi \right>
$$

for arbitrary $$\phi, \psi \in \mathbf{H}$$. In other words $$P$$ is self-adjoint, the desired result of **Part 2.2**.

**Part 2.3:** Now let us prove that $$P$$ satisfies $$PP=P$$. Again it turns out this follows directly from the fact that for each of the linear, bounded operators $$P_i$$ we have $$P_iP_i = P_i$$ and $$P_iP_j = 0$$ if $$i \neq j$$.


Tracing definitions one has for arbitrary $$\psi \in \mathbf{H}$$

$$
\begin{align}
    PP\psi &= \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n P_i \left( \lim\limits_{m \rightarrow \infty} \sum_{j = 0}^m P_j\psi \right) \\
           &= \lim\limits_{n \rightarrow \infty}  \lim\limits_{m \rightarrow \infty} \sum_{i = 0}^n P_i \left( \sum_{j = 0}^m P_j\psi \right) \\
           &= \lim\limits_{n \rightarrow \infty}  \lim\limits_{m \rightarrow \infty} \left( \sum_{i = 0}^n \sum_{j = 0}^m P_i P_j\psi \right) \\
           &= \lim\limits_{n \rightarrow \infty}  \sum_{i = 0}^n P_i P_i\psi \\
           &= \lim\limits_{n \rightarrow \infty}  \sum_{i = 0}^n P_i\psi \\
           &= P\psi.
\end{align}
$$

Proving

$$
    PP\psi = P\psi
$$

for arbitrary $$\psi \in \mathbf{H}$$, the third and final condition, so $$P$$ is a bounded orthogonal projection.
$$\blacksquare$$

> **Proposition** *(The Range of the Limit Projection)*
<a name="prpstn:orthogonal-sum-range"></a>
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:orthogonal-sum-converges} -->
<!--  \uses{prpstn:orthogonal-sum-is-projection} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
> With $$\{P_i\}$$ and $$P$$ as in [**Proposition** *(Partial Sums of Pairwise Orthogonal Projections Converge)*](#prpstn:orthogonal-sum-converges), the range of $$P$$ is the smallest closed subspace of $$\mathbf{H}$$ containing the ranges of all the $$P_i$$.

**Proof**
the range of $$P$$ is the smallest closed subspace containing the range of the $$P_i$$. Proving this will require two parts **Part 3.1:** prove that the closed subspace containing the range of the $$P_i$$ is a subset of the range of $$P$$ and **Part 3.2:** prove that the range of $$P$$ is a subset of the closed subspace containing the range of the $$P_i$$.

**Part 3.1:** Let us begin by proving that the closed subspace containing the range of the $$P_i$$ is a subset of the range of $$P$$.

To facilitate this, let us define the notation

$$
    M \equiv \text{Range}(P)
$$

for the range of $$P$$. Similarly, let us define the notation

$$
    V \equiv \overline{\text{Span} \left( \bigcup_{i = 0}^\infty \text{Range}(P_i) \right)}
$$

for the closure of the subspace containing the range of the $$P_i$$.

With this notation in hand, let us first prove that $$M$$ is closed.

Let $$\{ \psi_i \}_{i \in \mathbb{N}}$$ be a sequence in $$M$$ that converges to $$\psi$$ in $$\mathbf{H}$$. As the $$\psi_i$$ are in $$M \equiv \text{Range}(P)$$, the fact that $$P$$ is a bounded orthogonal projection operator implies that $$P\psi_i = \psi_i$$ for all $$i \in \mathbb{N}$$.

Now, as we proved that $$P$$ is bounded the standard proposition [**Bounded Operators are Continuous**](#prpstn:bounded-operators-are-continuous) proves that $$P$$ is continuous. As $$P$$ is continuous, we can pull $$P$$ through limits; this implies

$$
\begin{align}
    P\psi &= P \left( \lim_{i \rightarrow \infty} \psi_i \right) \\
          &= \lim_{i \rightarrow \infty} P \psi_i \\
          &= \lim_{i \rightarrow \infty} \psi_i \\
          &= \psi.
\end{align}
$$

This implies

$$
    P\psi = \psi,
$$

which implies that $$\psi$$ is in the range of $$P$$ and thus in $$M \equiv \text{Range}(P)$$, proving $$M$$ is closed.

To complete the proof of **Part 3.1** we must prove that $$V \subseteq M$$.

As $$P_iP_i = P_i$$ and $$P_iP_j = 0$$ for $$i \neq j$$, for any $$\psi_i$$ in $$\text{Range}(P_i)$$ we have $$P_i\psi_i = \psi_i$$ and $$P_j\psi_i = 0$$ for $$i \neq j$$. As a result we have

$$
    P\psi_i = \lim\limits_{n \rightarrow \infty} \sum_{j = 0}^n P_j\psi_i = P_i\psi_i = \psi_i.
$$

This implies $$P\psi_i = \psi_i$$ which in turn implies that $$\psi_i$$ is in $$M \equiv \text{Range}(P)$$. However, as $$\psi_i$$ is an arbitrary element in $$\text{Range}(P_i)$$, this implies that $$\text{Range}(P_i) \subseteq M$$. But, as the index $$i$$ we used was arbitrary this implies that

$$
   \bigcup_{i = 0}^\infty \text{Range}(P_i) \subseteq M.
$$ 

However, as we proved, $$M$$ is closed. Thus it must contain the closed linear span of all these ranges

$$
   \overline{\text{Span} \left( \bigcup_{i = 0}^\infty \text{Range}(P_i) \right)} \subseteq M,
$$ 

which is none other than the desired result $$V \subseteq M$$ of **Part 3.1**.

**Part 3.2:** Next let us prove that the range of $$P$$ is a subset of the closed subspace containing the range of the $$P_i$$.

Consider an arbitrary $$\psi \in \mathbf{H}$$. The partial sum

$$
    S_n\psi \equiv \sum_{i = 0}^n P_i\psi
$$

is a linear combination of a finite number of vectors $$P_i\psi$$ in

$$
    \bigcup_{i = 0}^n \text{Range}(P_i).
$$

Obviously, $$S_n\psi \in V$$. As $$V$$ is by construction closed and $$S_n\psi \rightarrow P\psi$$ relative to the norm on $$\mathbf{H}$$, the limit $$P\psi$$ must also live in $$V$$. Thus, $$M \subseteq V$$, as required.

This completes the proof of [**Lemma**](#lmm:lemma-4).$$\blacksquare$$


With the lemma in hand we return to the countable-additivity argument, consider a series $$\{ E_i \}_{i \in \mathbb{N}}$$ of disjoint measurable subsets of the spectrum $$\sigma(A)$$ of $$A$$. We proved that the $$\mu^A(E_i)$$ are bounded orthogonal projections on the separable, complex Hilbert space $$\mathbf{H}$$ and that $$\mu^A(E_i)\mu^A(E_j) = 0$$ if $$i \neq j$$.

Hence, we can apply the [**Lemma**](#lmm:lemma-4) we just proved to conclude that for any $$\psi \in \mathbf{H}$$ the sequence of partial sums

$$
    S_n\psi \equiv \sum_{i = 0}^n \mu^A(E_i)\psi
$$

converges to $$P\psi$$ where $$P$$ is a bounded orthogonal projection onto the smallest closed subspace containing the range of the $$\mu^A(E_i)$$.

Now with this same series $$\{ E_i \}_{i \in \mathbb{N}}$$ let us define $$E$$ by

$$
    E \equiv \bigcup_{i = 0}^\infty E_i.
$$

As the $$E_i$$ are disjoint, the sequence

$$
    f_n \equiv \sum_{i = 0}^n 1_{E_i}
$$

is uniformly bounded by $$1$$, and converges pointwise to $$1_E$$.

As both the $$1_{E_i}$$ and $$1_E$$ are bounded measurable functions on the spectrum $$\sigma(A)$$ of $$A$$, we can associate by way of the [**Definition**](#def:hall-8.8) the operators $$1_{E_i}(A)$$ and $$1_E(A)$$ to them.

As the sequence $$f_n$$ is uniformly bounded and converges pointwise to $$1_E$$, we can use [**Proposition** *(The Quadratic Form is Continuous under Bounded Pointwise Limits)*](#prpstn:Q-continuous-under-limits), which gives that the map $$f \mapsto Q_f(\psi)$$ is continuous under uniformly bounded pointwise convergence for any $$\psi \in \mathbf{H}$$ to conclude that the convergence of $$f_n$$ along with [**Definition**](#def:hall-8.8) imply

$$
\begin{align}
   \left< \psi, 1_E(A)\psi \right> &= \left< \psi, \left( \lim\limits_{n \rightarrow \infty} \sum_{i = 0}^n 1_{E_i}(A) \right) \psi \right> \\
                                   &= \lim\limits_{n \rightarrow \infty} \left< \psi, \left( \sum_{i = 0}^n 1_{E_i}(A) \right) \psi \right>.
\end{align}
$$

However, by definition $$\mu^A(E) \equiv 1_E(A)$$ and $$\mu^A(E_i) \equiv 1_{E_i}(A)$$, thus the previous equation implies

$$
     \left< \psi, \mu^A\left( \bigcup_{i = 0}^\infty E_i \right) \psi \right> = \lim\limits_{n \rightarrow \infty} \left< \psi, \left( \sum_{i = 0}^n \mu^A(E_i) \right) \psi \right>,
$$

for arbitrary $$\psi \in \mathbf{H}$$. This is nothing more than the statement that $$\mu^A$$ is countable additive, as required.
$$\blacksquare$$

> **Proposition** *(Spectral Projections are the Integrals of their Indicators)*
<a name="prpstn:mua-indicator-integral"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:integral-of-indicator} -->
<!--  \uses{def:hall-8.8} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), and given that $$\mu^A$$ is a projection-valued measure, for every measurable $$E \subseteq \sigma(A)$$,
>
> $$
>     \mu^A(E) = \int_{\sigma(A)} 1_E(\lambda) \, d\mu^A(\lambda).
> $$

**Proof**
$$\mu^A$$ satisfies

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
$$

To this end, consider the measurable set $$E$$ on $$\sigma(A)$$ and its bounded, measurable indicator function $$1_E$$. As a result of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) we have the unique linear map

$$
    1_E \longmapsto \int_{\sigma(A)} 1_E(\lambda) \, d\mu^A(\lambda)
$$

from the space of bounded, measurable, complex-valued functions on $$\sigma(A)$$ into $$\mathcal{B}(\mathbf{H})$$. By definition

$$
    \mu^A(E) \equiv \int_{\sigma(A)} 1_E(\lambda) \, d\mu^A(\lambda),
$$

and by definition

$$
    \mu^A(E) \equiv 1_E(A).
$$

Hence, we have the unique linear map

$$
    1_E \longmapsto 1_E(A).
$$

Consider now any simple function $$s$$ on $$\sigma(A)$$, i.e. any finite linear combination of indicator functions $$1_{E_i}$$ on $$\sigma(A)$$

$$
    s = \sum_{i = 1}^n \alpha_i 1_{E_i},
$$

where the $$E_i$$ are pairwise disjoint measurable sets on $$\sigma(A)$$ and the $$\alpha_i$$ are in $$\mathbb{C}$$. As the map

$$
    1_E \longmapsto 1_E(A)
$$

is linear we have for the arbitrary simple function $$s$$

$$
    s \longmapsto s(A) \equiv \sum_{i = 1}^n \alpha_i 1_{E_i}(A).
$$
    
Now, by taking limits of such simple functions this map extends to all bounded, Borel-measurable functions $$f$$ as follows

$$
    f \longmapsto f(A).
$$

In particular, $$\sigma(A)$$ is compact as a result of [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), thus the function $$f(\lambda) = \lambda$$ on $$\sigma(A)$$ is a bounded and obviously Borel-measurable function on $$\sigma(A)$$. Hence, we can apply the map above to $$f(\lambda) = \lambda$$.

We claim that the integral of $$f(\lambda) = \lambda$$ against $$\mu^A$$ is $$A$$.

Proving this claim explicitly follows from (1) proving that the measures $$\mu^A_\psi$$ and $$\mu_\psi$$ agree, (2) proving that the operator $$f(A)$$ of [**Definition**](#def:hall-8.8) agrees with the projection-valued integral of $$f$$ with respect to $$\mu^A$$, (3) proving that for continuous $$g$$ the operator $$g(A)$$ of [**Definition**](#def:hall-8.8) agrees with the operator $$g(A)$$ of [**Proposition**](#prpstn:hall-8.3), and (4) finally specializing to the continuous function $$f(\lambda) = \lambda$$ for the final result.

To (1) prove that the measures $$\mu^A_\psi$$ and $$\mu_\psi$$ agree we can unroll definitions. For any measurable $$E$$ on $$\sigma(A)$$ we have

$$
\begin{align}
    \mu^A_\psi(E) &\equiv \left< \psi, \mu^A(E) \psi \right> \\
                  &=      \left< \psi, 1_E(A) \psi \right> \\
                  &=      Q_{1_E}(\psi) \\
                  &=      \int_{\sigma(A)} 1_E(\lambda) \, d\mu_\psi(\lambda) \\
                  &=      \mu_\psi(E),
\end{align}
$$

where the first equality follows from the definition of $$\mu^A_\psi$$ in [**Theorem** *(Projection-Valued Measure's Associated Measure)*](#thrm:projection-valued-measures-associated-measure), the second from the definition of the operator $$\mu^A(E)$$, the third from the characterization of $$1_E(A)$$ in [**Definition**](#def:hall-8.8), and the fourth from the [**Definition**](#def:hall-8.6) of $$Q_{1_E}(\psi)$$. This implies

$$
    \mu^A_\psi(E) = \mu_\psi(E)
$$

which, as $$E$$ is arbitrary, is none other than the statement that the measures $$\mu^A_\psi$$ and $$\mu_\psi$$ agree.
$$\blacksquare$$

> **Proposition** *(The Two Bounded Functional Calculi Agree)*
<a name="prpstn:mua-bounded-calculus-agrees"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:mua-indicator-integral} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{prpstn:hall-a.63} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), for every bounded, Borel-measurable, complex-valued $$f$$ on $$\sigma(A)$$ the operator $$f(A)$$ of [**Definition**](#def:hall-8.8) coincides with the projection-valued integral of $$f$$ against $$\mu^A$$:
>
> $$
>     f(A) = \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda).
> $$

**Proof**
We show that the operator $$f(A)$$ of [**Definition**](#def:hall-8.8) agrees with the projection-valued integral of $$f$$ with respect to $$\mu^A$$.

For any bounded, Borel-measurable, complex-valued function $$f$$ on $$\sigma(A)$$ as a result of [**Definition**](#def:hall-8.8) and [**Definition**](#def:hall-8.6) we have

$$
    \left< \psi, f(A) \psi \right> = Q_f(\psi) = \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) 
$$

for any $$\psi$$ in $$\mathbf{H}$$. Also, as a result of the defining property of a projection-valued measure $$\mu^A$$, we have

$$
    \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right) \psi \right> = \int_{\sigma(A)} f(\lambda) \, d\mu^A_\psi(\lambda)
$$

from [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration). However, we just proved the measures $$\mu^A_\psi$$ and $$\mu_\psi$$ agree. Thus

$$
    \int_{\sigma(A)} f(\lambda) \, d\mu_\psi(\lambda) = \int_{\sigma(A)} f(\lambda) \, d\mu^A_\psi(\lambda).
$$ 

From our previous equations, this implies that the operators

$$
    f(A) \quad \text{and} \quad \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda)
$$

both represent the same bounded quadratic form $$Q_f$$.

However, by the uniqueness clause of [**Proposition**](#prpstn:hall-a.63) the operator representing a given bounded quadratic form $$Q_f$$ is unique. Thus

$$
    f(A) = \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda).
$$
$$\blacksquare$$

> **Proposition** *(The Spectral Measure Integrates to the Operator)*
<a name="prpstn:mua-integrates-to-A"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{prpstn:mua-projection} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{prpstn:mua-bounded-calculus-agrees} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{def:hall-8.6} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint. With $$\mu^A(E) \equiv 1_E(A)$$ as in [**Proposition** *(Each Spectral Projection is an Orthogonal Projection)*](#prpstn:mua-projection), 
>
> $$
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
> $$

**Proof**
We show that for continuous $$g$$ in $$C^0(\sigma(A); \mathbb{R})$$ the operator $$g(A)$$ of [**Definition**](#def:hall-8.8) agrees with the operator $$g(A)$$ of [**Proposition**](#prpstn:hall-8.3).

Directly before the statement of [**Definition**](#def:hall-8.6) we established that for any $$\psi$$ in $$\mathbf{H}$$ we can construct a map $$\Lambda_\psi : C^0(\sigma(A); \mathbb{R}) \rightarrow \mathbb{R}$$ defined by

$$
   \Lambda_\psi(g) \equiv \left< \psi, g(A)\psi \right>,
$$

where $$g(A)$$ arises from the real-valued functional calculus of [**Proposition**](#prpstn:hall-8.3), such that the application of [**Theorem** *(Riesz Representation)*](#thrm:riesz-representation) implies

$$
    \Lambda_\psi(g) \equiv \left< \psi, g(A)\psi \right> = \int_{\sigma(A)} g(\lambda) \, d\mu_\psi(\lambda) = Q_g(\psi),
$$

where the measure $$\mu_\psi$$ arises from the [**Theorem** *(Riesz Representation)*](#thrm:riesz-representation) and $$Q_g(\psi)$$ arises from [**Definition**](#def:hall-8.6).

However, the $$g(A)$$ from [**Definition**](#def:hall-8.8) satisfies

$$
    \left< \psi, g(A)\psi \right> = Q_g(\psi) = \int_{\sigma(A)} g(\lambda) \, d\mu_\psi(\lambda).
$$

So both the $$g(A)$$ from [**Proposition**](#prpstn:hall-8.3) and the $$g(A)$$ from [**Definition**](#def:hall-8.8) both give rise to the same bounded quadratic form $$Q_g$$. However, by the uniqueness clause of [**Proposition**](#prpstn:hall-a.63), the operator representing a given bounded quadratic form $$Q_g$$ is unique. Thus, for $$g$$ in $$C^0(\sigma(A); \mathbb{R})$$ the $$g(A)$$ from [**Proposition**](#prpstn:hall-8.3) agrees with the $$g(A)$$ from [**Definition**](#def:hall-8.8), the desired result.

Finally, let us (4) prove that specializing to the continuous function $$f(\lambda) = \lambda$$ we obtain the desired result, that the integral of $$f(\lambda) = \lambda$$ against $$\mu^A$$ is $$A$$.

Recall that [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable) implies that $$\sigma(A)$$ is a subset of $$\mathbb{R}$$. Thus, $$f(\lambda) = \lambda$$ is real-valued. Furthermore, as $$f(\lambda) = \lambda$$ is a polynomial it is continuous. Also note that the same [**Lemma**](#lmm:spectrum-is-compact-metric-measurable) implies $$\sigma(A)$$ is compact. Hence, as a result of [**Theorem** *(Boundedness Theorem)*](#thrm:boundedness-theorem), $$f(\lambda) = \lambda$$ is bounded.

So the result of the last section on continuous functions applies to $$f(\lambda) = \lambda$$ and the $$f(A)$$ from [**Proposition**](#prpstn:hall-8.3) agrees with the $$f(A)$$ from [**Definition**](#def:hall-8.8).

Now by way of the map defined in the [**Lemma** *(Spectral Mapping Theorem)*](#lmm:spectral-mapping-theorem) the polynomial $$f(\lambda) = \lambda$$ is mapped to the operator $$f(A) = A$$. Recall also that the $$f(A)$$ of [**Proposition**](#prpstn:hall-8.3) is constructed such that when $$f$$ is a polynomial it agrees with the $$f(A)$$ of [**Lemma** *(Spectral Mapping Theorem)*](#lmm:spectral-mapping-theorem). Hence, as $$f(\lambda) = \lambda$$ is a polynomial the $$f(A)$$ of [**Proposition**](#prpstn:hall-8.3) is given by $$f(A) = A$$.

So putting this all together we have from our second step that

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = f(A),
$$

where $$f(A)$$ is the $$f(A)$$ of [**Definition**](#def:hall-8.8). Now using the results of this step we know that for $$f(\lambda) = \lambda$$ the $$f(A)$$ of [**Definition**](#def:hall-8.8) is equal to the $$f(A)$$ of [**Proposition**](#prpstn:hall-8.3) and the $$f(A)$$ of [**Proposition**](#prpstn:hall-8.3) is equal to $$A$$, giving in full

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = f(A) = A,
$$

the desired result.

So in summary we have proven that

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A,
$$

as required.$$\blacksquare$$



#### Uniqueness of the Spectral Measure

The final result we need to prove to complete our proof of the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators) is to prove that the projection-valued measure $$\mu^A$$ of [**Theorem**](#thrm:hall-8.10) is unique. It is to this we turn.

> **Theorem** *(Uniqueness of the Spectral Measure)*
<a name="thrm:hall-prblm-8.3.4"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:pvm-agree-on-continuous} -->
<!--  \uses{prpstn:pvm-agree-on-measurable} -->
<!--  \uses{prpstn:pvm-agree-on-polynomials} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{lmm:lemma-5} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$\mu^A$$ and $$\nu^A$$ be two projection-valued measures on the spectrum $$\sigma(A)$$ of $$A$$ such that
> 
> $$
> \begin{align}
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) &= A \\
>     \int_{\sigma(A)} \lambda \, d\nu^A(\lambda) &= A.
> \end{align}
> $$
> 
> Then $$\mu^A(E) = \nu^A(E)$$ for all measurable subsets $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$, i.e. $$\mu^A$$ and $$\nu^A$$ are equivalent projection-valued measures.

**Proof**
The proof is a ladder of increasing function classes: the two integrals agree on polynomials by [**Proposition** *(Two Spectral Measures Agree on Polynomials)*](#prpstn:pvm-agree-on-polynomials), on continuous functions by [**Proposition** *(Two Spectral Measures Agree on Continuous Functions)*](#prpstn:pvm-agree-on-continuous), and on bounded Borel-measurable functions by [**Proposition** *(Two Spectral Measures Agree on Bounded Measurable Functions)*](#prpstn:pvm-agree-on-measurable). It remains to specialise to indicator functions.

We now prove that $$\mu^A(E) = \nu^A(E)$$ for all measurable subsets $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$.

Consider any measurable subset $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$ along with its indicator function $$1_E$$. As a result of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) we have

$$
\begin{align}
    \mu^A(E) &= \int_{\sigma(A)} 1_E(\lambda) \, d\mu^A(\lambda) \\
    \nu^A(E) &= \int_{\sigma(A)} 1_E(\lambda) \, d\nu^A(\lambda). 
\end{align}
$$

Now the indicator function $$1_E$$ is obviously bounded, as

$$
    \lvert 1_E(\lambda) \rvert \le 1
$$

for all $$\lambda$$ in $$\sigma(A)$$; measurable, as the inverse image of any measurable set in $$\mathbb{C}$$ is either the empty set or $$E$$; and also complex-valued, as $$\mathbb{R}$$ is a subset of $$\mathbb{C}$$. Hence, the indicator function $$1_E$$ is a bounded, Borel-measurable function on $$\sigma(A)$$.

Now, by [**Proposition** *(Two Spectral Measures Agree on Bounded Measurable Functions)*](#prpstn:pvm-agree-on-measurable), operator-valued integration with respect to $$\mu^A$$ agrees with the same with respect to $$\nu^A$$ on all bounded, Borel-measurable functions on $$\sigma(A)$$. So in the case of $$1_E$$ this implies that

$$
    \int_{\sigma(A)} 1_E(\lambda) \, d\mu^A(\lambda) = \int_{\sigma(A)} 1_E(\lambda) \, d\nu^A(\lambda).
$$

This along with our previous expressions for $$\mu^A(E)$$ and $$\nu^A(E)$$ then imply

$$
    \mu^A(E) = \nu^A(E),
$$

the desired result of this final part.
$$\blacksquare$$

> **Proposition** *(Two Spectral Measures Agree on Polynomials)*
<a name="prpstn:pvm-agree-on-polynomials"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:integral-multiplicative} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{prpstn:integral-mult-measurable} -->
<!--  \uses{prpstn:integral-of-indicator} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$\mu^A, \nu^A$$ be projection-valued measures on $$\sigma(A)$$ with $$\int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A = \int_{\sigma(A)} \lambda \, d\nu^A(\lambda)$$. Then for every polynomial $$p$$ on $$\sigma(A)$$,
>
> $$
>     \int_{\sigma(A)} p \, d\mu^A = \int_{\sigma(A)} p \, d\nu^A.
> $$

**Proof**
operator-valued integration with respect to $$\mu^A$$ agrees with that with respect to $$\nu^A$$ on complex-valued polynomials.

Consider an arbitrary complex valued polynomial $$p$$ on $$\sigma(A)$$ with $$\mathbb{C}$$ valued coefficients. Generically $$p$$ has the form

$$
    p(\lambda) = \sum_{i=0}^n a_i\lambda^i
$$

where the $$a_i$$ take values in $$\mathbb{C}$$. Operator-valued integration with respect to $$\mu^A$$ gives

$$
\begin{align}
    \int_{\sigma(A)} p(\lambda) \, d\mu^A(\lambda) &=  \int_{\sigma(A)} \left( \sum_{i=0}^n a_i\lambda^i \right) \, d\mu^A(\lambda) \\
                                                   &=  \sum_{i=0}^n a_i \left( \int_{\sigma(A)} \lambda^i \, d\mu^A(\lambda) \right) \\
                                                   &=  \sum_{i=0}^n a_i \left( \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) \right)^i \\
                                                   &=  \sum_{i=0}^n a_i A^i,
\end{align}
$$

where the first equality made use of the definition of $$p$$, the second equality made use of linearity of operator-valued integration following from [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration), the third equality made use of multiplicativity of operator-valued integration, [**Proposition** *(Operator-Valued Integration is Multiplicative)*](#prpstn:integral-multiplicative), and the final equality made use of the hypothesis of this theorem.

Using the same logic, operator-valued integration with respect to $$\nu^A$$ gives

$$
\begin{align}
    \int_{\sigma(A)} p(\lambda) \, d\nu^A(\lambda) &=  \int_{\sigma(A)} \left( \sum_{i=0}^n a_i\lambda^i \right) \, d\nu^A(\lambda) \\
                                                   &=  \sum_{i=0}^n a_i \left( \int_{\sigma(A)} \lambda^i \, d\nu^A(\lambda) \right) \\
                                                   &=  \sum_{i=0}^n a_i \left( \int_{\sigma(A)} \lambda \, d\nu^A(\lambda) \right)^i \\
                                                   &=  \sum_{i=0}^n a_i A^i.
\end{align}
$$

Hence, we have proven the desired result

$$
    \int_{\sigma(A)} p(\lambda) \, d\mu^A(\lambda) = \int_{\sigma(A)} p(\lambda) \, d\nu^A(\lambda),
$$

operator-valued integration with respect to $$\mu^A$$ agrees with that with respect to $$\nu^A$$ on complex-valued polynomials.
$$\blacksquare$$

> **Proposition** *(Two Spectral Measures Agree on Continuous Functions)*
<a name="prpstn:pvm-agree-on-continuous"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{prpstn:integral-norm-bound} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:pvm-agree-on-polynomials} -->
<!--  \uses{lmm:lemma-5} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$\mu^A, \nu^A$$ be projection-valued measures on $$\sigma(A)$$ with $$\int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A = \int_{\sigma(A)} \lambda \, d\nu^A(\lambda)$$. Then for every continuous, complex-valued $$g$$ on $$\sigma(A)$$,
>
> $$
>     \int_{\sigma(A)} g \, d\mu^A = \int_{\sigma(A)} g \, d\nu^A.
> $$

**Proof**
operator-valued integration with respect to $$\mu^A$$ agrees with that with respect to $$\nu^A$$ on the set of continuous, complex-valued functions on $$\sigma(A)$$.

The next lemma uses the complex-valued Stone–Weierstrass Theorem, which we state first.

> **Theorem** *(Stone–Weierstrass for Complex Numbers)*
<a name="thrm:stone–weierstrass-complex"></a>
<!--  \uses{def:separates-points} -->
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{C})$$, the space of continuous, complex-valued functions on $$X$$. If $$\mathcal{A}$$ contains the constant functions, separates points, and is closed under complex conjugation, then $$\mathcal{A}$$ is dense in $$C^0(X; \mathbb{C})$$ with respect to the supremum norm.

We will have need of the fact that the set of complex-valued polynomials on $$\sigma(A)$$ is dense in the set of continuous, complex-valued functions on $$\sigma(A)$$ with respect to the supremum norm. So we begin by proving this fact.

> **Lemma** *(Polynomials are Dense in the Continuous Functions on the Spectrum)*
<a name="lmm:lemma-5"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{thrm:stone–weierstrass-complex} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint, then the set of complex-valued polynomials on $$\sigma(A)$$ is dense in the set of continuous, complex-valued functions on $$\sigma(A)$$ with respect to the supremum norm.

**Proof**
By [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a non-empty, compact metric measurable space.

As $$\sigma(A)$$ is a subset of $$\mathbb{C}$$, we can restrict the standard metric on $$\mathbb{C}$$

$$
    d(\lambda_1, \lambda_2) \equiv \lvert \lambda_2 - \lambda_1 \rvert,
$$

where $$\lvert \cdot \rvert$$ is the norm on $$\mathbb{C}$$, to $$\sigma(A)$$ making $$\sigma(A)$$ a metric space.

Consider now $$\mathcal{P}(\sigma(A); \mathbb{C})$$ the set of complex-valued polynomials on $$\sigma(A)$$ and $$C^0(\sigma(A); \mathbb{C})$$ the set of continuous, complex-valued functions on $$\sigma(A)$$. Obviously, $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is a subset of $$C^0(\sigma(A); \mathbb{C})$$ as all complex-valued polynomials on $$\sigma(A)$$ are continuous.

Furthermore, $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is obviously an algebra as it has the required vector space properties, e.g. closure under addition, as well as the required bilinear product properties, e.g. left distributivity.

In addition it is also obvious that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ [separates points](#def:separates-points). Explicitly, consider any two distinct points $$\lambda_1, \lambda_2 \in \sigma(A)$$. There exists a polynomial $$p$$ in $$\mathcal{P}(\sigma(A); \mathbb{C})$$ such that $$p(\lambda_1) \neq p(\lambda_2)$$. For example the polynomial

$$
    p(\lambda) = (\lambda - \lambda_1)
$$

would suffice as $$p(\lambda_1) \neq p(\lambda_2)$$ follows from the fact that $$\lambda_1$$ and $$\lambda_2$$ are distinct.

Another obvious point we will have need of is the fact that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ contains constant functions. Explicitly the constant function

$$
    p(\lambda) = a_0,
$$

where $$a_0 \in \mathbb{C}$$, is an element of $$\mathcal{P}(\sigma(A); \mathbb{C})$$.

The final point we will have need of is the fact that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is closed under complex conjugation, i.e. if $$p(\lambda)$$ is in $$\mathcal{P}(\sigma(A); \mathbb{C})$$, then $$\overline{p(\lambda)}$$ is also in $$\mathcal{P}(\sigma(A); \mathbb{C})$$. This follows from noting that [**Proposition**](#prpstn:hall-7.7) implies that the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$. Hence, a generic $$p$$ in $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is of the form

$$
    p(\lambda) = \sum_{i=0}^n a_i \lambda^i,
$$

where the $$a_i$$ are complex-valued and $$\lambda$$ is real, and this implies

$$
\begin{align}
    \overline{p(\lambda)} &= \overline{\sum_{i=0}^n a_i \lambda^i} \\
                          &= \sum_{i=0}^n \overline{a_i} \lambda^i.
\end{align}
$$

Now as the $$\overline{a_i}$$ are also in $$\mathbb{C}$$, this implies that

$$
    \overline{p(\lambda)} = \sum_{i=0}^n \overline{a_i} \lambda^i
$$

is an element in $$\mathcal{P}(\sigma(A); \mathbb{C})$$, proving that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is closed under complex conjugation.

With all of this in place we are in a position to apply the [**Theorem** *(Stone–Weierstrass for Complex Numbers)*](#thrm:stone–weierstrass-complex) and conclude that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is dense in $$C^0(\sigma(A); \mathbb{C})$$ with respect to the supremum norm, the desired result.$$\blacksquare$$

Our next long term goal is to apply the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem) to prove that operator-valued integration with respect to $$\mu^A$$ agrees with the same with respect to $$\nu^A$$ when the integrand is an element of $$C^0(\sigma(A); \mathbb{C})$$. In other words to prove

$$
    \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) = \int_{\sigma(A)} f(\lambda) \, d\nu^A(\lambda),
$$

for an arbitrary $$f$$ in $$C^0(\sigma(A); \mathbb{C})$$. Let's begin.

First, as mentioned after our application of the [**Theorem** *(Stone–Weierstrass for Complex Numbers)*](#thrm:stone–weierstrass-complex), $$C^0(\sigma(A); \mathbb{C})$$ is equipped with a norm, the supremum norm, and is thus a normed space.

Second, recall that as a result of [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space) we know that $$\mathcal{B}(\mathbf{H})$$ is a Banach space with respect to the operator norm.

Now recall that [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) implies that the maps

$$
\begin{align}
    I_{\mu^A} : p \longmapsto \int_{\sigma(A)} p(\lambda) \, d\mu^A(\lambda) \\
    I_{\nu^A} : p \longmapsto \int_{\sigma(A)} p(\lambda) \, d\nu^A(\lambda)
\end{align}
$$

from the set of bounded, measurable complex-valued functions on $$\sigma(A)$$ to $$\mathcal{B}(\mathbf{H})$$ are linear. We want to prove $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is a subset of the domain of $$I_{\mu^A}$$ and $$I_{\nu^A}$$.

Recall that by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a non-empty, compact metric measurable space.

Also recall that any complex-valued polynomial $$p$$ on $$\sigma(A)$$ is continuous, i.e. $$\mathcal{P}(\sigma(A); \mathbb{C}) \subset C^0(\sigma(A); \mathbb{C})$$. Thus the norm $$\lvert p \rvert$$ of any element of $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is a continuous real-valued function on $$\sigma(A)$$. Hence, as a result of [**Theorem** *(Boundedness Theorem)*](#thrm:boundedness-theorem), $$\lvert p \rvert$$ is bounded on $$\sigma(A)$$. This is none other than the statement that $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is bounded on $$\sigma(A)$$.

Finally, note that as $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is continuous and the $$\sigma$$-algebra on $$\sigma(A)$$ is the Borel $$\sigma$$-algebra, it follows that any element of $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is measurable.

Hence, elements of $$\mathcal{P}(\sigma(A); \mathbb{C})$$ are bounded, measurable, complex-valued functions on $$\sigma(A)$$. Thus, $$\mathcal{P}(\sigma(A); \mathbb{C})$$ is in the domain of the $$I_{\mu^A}$$ and $$I_{\nu^A}$$.

Furthermore, [**Proposition** *(Norm Bound for the Operator-Valued Integral)*](#prpstn:integral-norm-bound) implies that for any bounded, measurable, complex-valued function $$f$$ on $$\sigma(A)$$

$$
    \left\| \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right\| \le \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert,
$$

and similarly with $$\mu^A$$ replaced by $$\nu^A$$. Applying this to an arbitrary $$p$$ in $$\mathcal{P}(\sigma(A); \mathbb{C})$$, which we have just shown is bounded and measurable, gives

$$
    \| I_{\mu^A}(p) \| \le \sup\limits_{\lambda \in \sigma(A)} \lvert p(\lambda) \rvert \equiv \|p\|,
$$

and similarly $$\| I_{\nu^A}(p) \| \le \|p\|$$, where $$\|p\|$$ denotes the supremum norm of $$p$$. This is none other than the statement that the linear maps $$I_{\mu^A}$$ and $$I_{\nu^A}$$, restricted to $$\mathcal{P}(\sigma(A); \mathbb{C})$$, are bounded using constant $$1$$.

With that established, let us restrict the domain of $$I_{\mu^A}$$ and $$I_{\nu^A}$$ to be $$\mathcal{P}(\sigma(A); \mathbb{C})$$ and only $$\mathcal{P}(\sigma(A); \mathbb{C})$$ while retaining the same notation $$I_{\mu^A}$$ and $$I_{\nu^A}$$. Hopefully this is not too confusing.

Finally, we may make use of the [**Theorem** *(Bounded Linear Transformation Theorem)*](#thrm:bounded-linear-transformation-theorem) to uniquely extend the domain of $$I_{\mu^A}$$ and $$I_{\nu^A}$$ from $$\mathcal{P}(\sigma(A); \mathbb{C})$$ to all of $$C^0(\sigma(A); \mathbb{C})$$. (Note we will still use the same notation $$I_{\mu^A}$$ and $$I_{\nu^A}$$ for these extended maps.) As $$I_{\mu^A}$$ and $$I_{\nu^A}$$ are extensions, $$I_{\mu^A}$$ agrees on $$\mathcal{P}(\sigma(A); \mathbb{C})$$ with its non-extended version, and a similar statement is true of $$I_{\nu^A}$$.

However, by [**Proposition** *(Two Spectral Measures Agree on Polynomials)*](#prpstn:pvm-agree-on-polynomials) the maps $$I_{\mu^A}$$ and $$I_{\nu^A}$$ agree when restricted to $$\mathcal{P}(\sigma(A); \mathbb{C})$$. Thus, as the extensions $$I_{\mu^A}$$ and $$I_{\nu^A}$$ obtained from [**Theorem** *(Bounded Linear Transformation Theorem)*](#thrm:bounded-linear-transformation-theorem) are unique, this implies that the extensions $$I_{\mu^A}$$ and $$I_{\nu^A}$$ agree everywhere on the domain $$C^0(\sigma(A); \mathbb{C})$$. 

Hence, we have proven as required: operator-valued integration with respect to $$\mu^A$$ agrees with that with respect to $$\nu^A$$ on the set of continuous, complex-valued functions on $$\sigma(A)$$.
$$\blacksquare$$

> **Proposition** *(Two Spectral Measures Agree on Bounded Measurable Functions)*
<a name="prpstn:pvm-agree-on-measurable"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{prpstn:pvm-agree-on-polynomials} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:pvm-agree-on-continuous} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$\mu^A, \nu^A$$ be projection-valued measures on $$\sigma(A)$$ with $$\int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A = \int_{\sigma(A)} \lambda \, d\nu^A(\lambda)$$. Then for every bounded, Borel-measurable, complex-valued $$f$$ on $$\sigma(A)$$,
>
> $$
>     \int_{\sigma(A)} f \, d\mu^A = \int_{\sigma(A)} f \, d\nu^A.
> $$

**Proof**
operator-valued integration with respect to $$\mu^A$$ agrees with that with respect to $$\nu^A$$ on the set of bounded, measurable complex-valued functions.

Let $$\mathcal{G}$$ be the set of bounded, measurable, complex-valued functions on $$\sigma(A)$$ such that operator-valued integration with respect to $$\mu^A$$ agrees with the same with respect to $$\nu^A$$.

Recall from [**Proposition** *(Two Spectral Measures Agree on Continuous Functions)*](#prpstn:pvm-agree-on-continuous) that $$C^0(\sigma(A); \mathbb{C})$$ is a subset of $$\mathcal{G}$$. Now, as $$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$C^0(\sigma(A); \mathbb{C})$$, it obviously follows that $$C^0(\sigma(A); \mathbb{R})$$ is a subset of $$\mathcal{G}$$ too.

Also note that as a result of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) the maps $$I_{\mu^A}$$ and $$I_{\nu^A}$$---now viewed as having domain consisting of all bounded, measurable, complex-valued functions on $$\sigma(A)$$---are linear. This implies that $$\mathcal{G}$$ is a vector space over $$\mathbb{C}$$. Explicitly, consider arbitrary $$f_1,f_2 \in \mathcal{G}$$ and arbitrary $$\alpha_1, \alpha_2 \in \mathbb{C}$$. Linearity of $$I_{\mu^A}$$ implies

$$
    \int_{\sigma(A)} \left( \alpha_1 f_1(\lambda) + \alpha_2 f_2(\lambda) \right) \, d\mu^A(\lambda) =  
    \alpha_1 \int_{\sigma(A)} f_1(\lambda) \, d\mu^A(\lambda) + \alpha_2 \int_{\sigma(A)} f_2(\lambda) \, d\mu^A(\lambda).
$$

Similarly linearity of $$I_{\nu^A}$$ implies

$$
    \int_{\sigma(A)} \left( \alpha_1 f_1(\lambda) + \alpha_2 f_2(\lambda) \right) \, d\nu^A(\lambda) =  
    \alpha_1 \int_{\sigma(A)} f_1(\lambda) \, d\nu^A(\lambda) + \alpha_2 \int_{\sigma(A)} f_2(\lambda) \, d\nu^A(\lambda).
$$

However, as $$f_1,f_2 \in \mathcal{G}$$ the definition of $$\mathcal{G}$$ implies

$$
\begin{align}
    \int_{\sigma(A)} f_1(\lambda) \, d\mu^A(\lambda) &= \int_{\sigma(A)} f_1(\lambda) \, d\nu^A(\lambda) \\
    \int_{\sigma(A)} f_2(\lambda) \, d\mu^A(\lambda) &= \int_{\sigma(A)} f_2(\lambda) \, d\nu^A(\lambda). 
\end{align}
$$

Hence, the last four equations imply

$$
    \int_{\sigma(A)} \left( \alpha_1 f_1(\lambda) + \alpha_2 f_2(\lambda) \right) \, d\mu^A(\lambda) = 
    \int_{\sigma(A)} \left( \alpha_1 f_1(\lambda) + \alpha_2 f_2(\lambda) \right) \, d\nu^A(\lambda).
$$

This implies that $$\alpha_1 f_1(\lambda) + \alpha_2 f_2(\lambda)$$ is in element $$\mathcal{G}$$ and thus $$\mathcal{G}$$ is a vector space over $$\mathbb{C}$$.

Next we want to prove that $$\mathcal{G}$$ is closed under pointwise limits of uniformly bounded sequences.

To this end let $$\{ f_i \}_{i \in \mathbb{N}}$$ be a sequence in $$\mathcal{G}$$, uniformly bounded by some $$M \in \mathbb{R}$$, that converges pointwise to a function $$f$$ on $$\sigma(A)$$. By [**Lemma** *(Pointwise Limits of Uniformly Bounded, Borel-Measurable Functions)*](#lmm:pointwise-limits-of-borel-measurable-functions), $$f$$ is itself a bounded, Borel-measurable, complex-valued function on $$\sigma(A)$$, and so is a candidate for membership in $$\mathcal{G}$$. Let $$\psi \in \mathbf{H}$$ be arbitrary.

By the defining property of the map of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration), applied to the projection-valued measure $$\mu^A$$, we have for every $$i \in \mathbb{N}$$

$$
    \left< \psi, \left( \int_{\sigma(A)} f_i(\lambda) \, d\mu^A(\lambda) \right) \psi \right> = \int_{\sigma(A)} f_i(\lambda) \, d(\mu^A)_\psi(\lambda),
$$

where $$(\mu^A)_\psi$$ is the positive real-valued measure associated to $$\mu^A$$ and $$\psi$$ by way of [**Theorem** *(Projection-Valued Measure's Associated Measure)*](#thrm:projection-valued-measures-associated-measure). Note that $$(\mu^A)_\psi$$ is a finite measure, as

$$
    (\mu^A)_\psi(\sigma(A)) = \left< \psi, \mu^A(\sigma(A)) \psi \right> = \left< \psi, \mathbf{1} \psi \right> = \|\psi\|^2 < \infty.
$$

As $$f_i \rightarrow f$$ pointwise with $$\lvert f_i(\lambda) \rvert \le M$$ for all $$i \in \mathbb{N}$$ and all $$\lambda \in \sigma(A)$$, the [**Bounded Convergence Theorem**](#thrm:bounded-convergence-theorem), applied to the finite measure $$(\mu^A)_\psi$$, gives

$$
    \int_{\sigma(A)} f_i(\lambda) \, d(\mu^A)_\psi(\lambda) \longrightarrow \int_{\sigma(A)} f(\lambda) \, d(\mu^A)_\psi(\lambda) = \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right) \psi \right>.
$$

Combining the last two results we obtain

$$
    \left< \psi, \left( \int_{\sigma(A)} f_i(\lambda) \, d\mu^A(\lambda) \right) \psi \right> \longrightarrow \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right) \psi \right>.
$$

An entirely identical argument, with $$\mu^A$$ replaced by $$\nu^A$$ throughout, gives

$$
    \left< \psi, \left( \int_{\sigma(A)} f_i(\lambda) \, d\nu^A(\lambda) \right) \psi \right> \longrightarrow \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\nu^A(\lambda) \right) \psi \right>.
$$

However, as each $$f_i$$ is an element of $$\mathcal{G}$$, the definition of $$\mathcal{G}$$ gives

$$
    \int_{\sigma(A)} f_i(\lambda) \, d\mu^A(\lambda) = \int_{\sigma(A)} f_i(\lambda) \, d\nu^A(\lambda)
$$

for every $$i \in \mathbb{N}$$, and hence

$$
    \left< \psi, \left( \int_{\sigma(A)} f_i(\lambda) \, d\mu^A(\lambda) \right) \psi \right> = \left< \psi, \left( \int_{\sigma(A)} f_i(\lambda) \, d\nu^A(\lambda) \right) \psi \right>
$$

for every $$i \in \mathbb{N}$$. So the two convergent sequences displayed above are in fact the same sequence of complex numbers. As a sequence in $$\mathbb{C}$$ has at most one limit, their limits coincide, giving

$$
    \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right) \psi \right> = \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\nu^A(\lambda) \right) \psi \right>
$$

for all $$\psi \in \mathbf{H}$$.

Now, as $$f$$ is a bounded, Borel-measurable, complex-valued function on $$\sigma(A)$$, [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration) implies that both $$\int_{\sigma(A)} f \, d\mu^A$$ and $$\int_{\sigma(A)} f \, d\nu^A$$ are elements of $$\mathcal{B}(\mathbf{H})$$. Hence the map

$$
    Q(\psi) \equiv \left< \psi, \left( \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) \right) \psi \right>
$$

is a bounded quadratic form on $$\mathbf{H}$$, and the equation above states that both $$\int_{\sigma(A)} f \, d\mu^A$$ and $$\int_{\sigma(A)} f \, d\nu^A$$ represent $$Q$$. Thus, the uniqueness clause of [**Proposition**](#prpstn:hall-a.63) implies

$$
    \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda) = \int_{\sigma(A)} f(\lambda) \, d\nu^A(\lambda),
$$

which is precisely the statement that $$f \in \mathcal{G}$$. Thus $$\mathcal{G}$$ is closed under pointwise limits of uniformly bounded sequences, the desired result.

Recall that by [**Lemma** *(The Spectrum is a Compact Metric Measurable Space)*](#lmm:spectrum-is-compact-metric-measurable), $$\sigma(A)$$ is a non-empty, compact metric measurable space.

Furthermore, as $$\sigma(A)$$ is a subset of $$\mathbb{C}$$ it inherits the metric from $$\mathbb{C}$$. Thus $$\sigma(A)$$ is also a metric space.

Finally recall, as we have noted many times, $$\sigma(A)$$ is also a measurable space as it is equipped with the Borel $$\sigma$$-algebra.

So we have $$\sigma(A)$$ a compact metric measurable space by [**Lemma**](#lmm:spectrum-is-compact-metric-measurable), $$\mathcal{G}$$ a set of bounded, measurable, complex-valued functions on $$\sigma(A)$$ such that (1) $$\mathcal{G}$$ is a complex vector space, (2) $$\mathcal{G}$$ contains $$C^0(\sigma(A); \mathbb{R})$$, and (3) $$\mathcal{G}$$ is closed under pointwise limits of uniformly bounded sequences. These are the exact conditions we require to apply the [**Lemma**](#lmm:hall-prblm-8.3.3c) we previously proved.

Applying this [**Lemma**](#lmm:hall-prblm-8.3.3c) to the case at hand, we can conclude that $$\mathcal{G}$$ consists of all bounded, Borel-measurable functions on $$\sigma(A)$$. However, by definition $$\mathcal{G}$$ is the set of bounded, measurable, complex-valued functions on $$\sigma(A)$$ such that operator-valued integration with respect to $$\mu^A$$ agrees with the same with respect to $$\nu^A$$. Thus, these last two facts imply that operator-valued integration with respect to $$\mu^A$$ agrees with the same with respect to $$\nu^A$$ on all bounded, Borel-measurable functions on $$\sigma(A)$$, as required.
$$\blacksquare$$

So with this we have proven that under the hypotheses of the [**Theorem**](#thrm:hall-prblm-8.3.4) $$\mu^A(E) = \nu^A(E)$$ for all measurable subsets $$E$$ of the spectrum $$\sigma(A)$$ of $$A$$, i.e. $$\mu^A$$ and $$\nu^A$$ are equivalent projection-valued measures.$$\blacksquare$$


> **Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*
<a name="thrm:spectral-theorem-for-bounded-operators"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:resolvent-holomorphy-and-neumann-series} -->
<!--  \uses{crllr:crllr-1} -->
<!--  \uses{def:F-class} -->
<!--  \uses{def:L0-class} -->
<!--  \uses{def:algebra-of-sets} -->
<!--  \uses{def:hall-8.6} -->
<!--  \uses{def:hall-8.8} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{def:spectral-radius} -->
<!--  \uses{lmm:associated-measures-are-finite} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{lmm:hall-7.6} -->
<!--  \uses{lmm:hall-7.8} -->
<!--  \uses{lmm:hall-8.1} -->
<!--  \uses{lmm:hall-ex-8.3.1} -->
<!--  \uses{lmm:hall-prblm-7.4.8} -->
<!--  \uses{lmm:hall-prblm-8.3.3a} -->
<!--  \uses{lmm:hall-prblm-8.3.3b} -->
<!--  \uses{lmm:hall-prblm-8.3.3c} -->
<!--  \uses{lmm:lemma-1} -->
<!--  \uses{lmm:lemma-2} -->
<!--  \uses{lmm:nth-term-test} -->
<!--  \uses{lmm:pointwise-limits-of-borel-measurable-functions} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:spectrum-is-compact-metric-measurable} -->
<!--  \uses{prpstn:F-bounded} -->
<!--  \uses{prpstn:F-closed-under-limits} -->
<!--  \uses{prpstn:F-contains-continuous} -->
<!--  \uses{prpstn:F-homogeneous} -->
<!--  \uses{prpstn:F-sesquilinear} -->
<!--  \uses{prpstn:L0-complement} -->
<!--  \uses{prpstn:L0-contains-closed} -->
<!--  \uses{prpstn:L0-contains-empty} -->
<!--  \uses{prpstn:L0-union} -->
<!--  \uses{prpstn:bounded-operators-are-continuous} -->
<!--  \uses{prpstn:cfc-multiplicative} -->
<!--  \uses{prpstn:cfc-non-negative} -->
<!--  \uses{prpstn:cfc-norm} -->
<!--  \uses{prpstn:cfc-self-adjoint} -->
<!--  \uses{prpstn:cfc-spectral-mapping} -->
<!--  \uses{prpstn:continuity-of-the-adjoint} -->
<!--  \uses{prpstn:hall-7.2} -->
<!--  \uses{prpstn:hall-7.3} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{prpstn:hall-7.7} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{prpstn:hall-8.4} -->
<!--  \uses{prpstn:hall-8.7} -->
<!--  \uses{prpstn:hall-a.34} -->
<!--  \uses{prpstn:hall-a.62} -->
<!--  \uses{thrm:analytic-equivalence-theorem} -->
<!--  \uses{thrm:archimedean-property} -->
<!--  \uses{thrm:bounded-convergence-theorem} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{thrm:composition-theorem} -->
<!--  \uses{thrm:existence-of-bump-functions} -->
<!--  \uses{thrm:fundamental-theorem-of-algebra} -->
<!--  \uses{thrm:hall-a.40} -->
<!--  \uses{thrm:laurents-theorem} -->
<!--  \uses{thrm:maximum-modulus-principle} -->
<!--  \uses{thrm:monotone-class-theorem} -->
<!--  \uses{thrm:monotone-convergence-theorem-nonincreasing} -->
<!--  \uses{thrm:riesz-representation} -->
<!--  \uses{thrm:theorem-on-completeness-of-the-dual} -->
<!--  \uses{def:identity-operator} -->
<!--  \uses{def:indicator-function} -->
<!--  \uses{def:orthogonal-complement} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{thrm:hall-8.10} -->
<!--  \uses{thrm:hall-prblm-8.3.4} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then there exists a unique projection-valued measure $$\mu^A$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$, the spectrum of $$A$$, with values in orthogonal projections on $$\mathbf{H}$$ such that
>
> $$
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
> $$

**Proof**
*Existence.* [**Theorem** *(The Spectral Measure of a Self-Adjoint Operator)*](#thrm:hall-8.10) constructs a projection-valued measure $$\mu^A$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$, with values in orthogonal projections on $$\mathbf{H}$$, and establishes

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
$$

*Uniqueness.* [**Theorem** *(Uniqueness of the Spectral Measure)*](#thrm:hall-prblm-8.3.4) shows that any two projection-valued measures on $$\sigma(A)$$ satisfying that identity agree on every measurable set. Together these give existence and uniqueness as asserted.$$\blacksquare$$

With the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators) proof complete, we can conclude by finally introducing the normative definition of the "functional calculus"

> **Definition** *(Functional Calculus)*
<a name="def:functional-calculus"></a>
<!--  \uses{def:adjoint-bounded} -->
<!--  \uses{prpstn:basic-integral-properties} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:spectral-theorem-for-bounded-operators} -->
<!--  \uses{thrm:operator-valued-integration} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{prpstn:mua-bounded-calculus-agrees} -->
<!--  \uses{def:hall-8.8} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint and $$f : \sigma(A) \rightarrow \mathbb{C}$$ is a bounded measurable function on the spectrum $$\sigma(A)$$ of $$A$$, *functional calculus* defines an operator $$f(A)$$ by
>
> $$
>     f(A) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda),
> $$
>
> where $$\mu^A$$ is the unique projection-valued measure of [**Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*](#thrm:spectral-theorem-for-bounded-operators) associated to $$A$$.
>
> This is the *second* construction of an operator written $$f(A)$$ in this post. The first, [**Definition**](#def:hall-8.8), obtains $$f(A)$$ from the quadratic form $$Q_f$$ via [**Proposition** *(hall-a.63)*](#prpstn:hall-a.63), without reference to any projection-valued measure. **The two agree**: that is the content of [**Proposition** *(The Two Bounded Functional Calculi Agree)*](#prpstn:mua-bounded-calculus-agrees), which shows $$f(A) = \int_{\sigma(A)} f \, d\mu^A$$ for every bounded, Borel-measurable $$f$$. The notation $$f(A)$$ is therefore unambiguous, and either construction may be used.

a tool which will often be used.
