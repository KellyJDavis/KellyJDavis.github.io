---
title:  "Spectral Theorem for Bounded, Self-Adjoint Operators"
date:   2026-07-06 07:43:42 +0200
categories: functional-analysis
---

Here we will state and prove the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](#thrm:spectral-theorem-for-bounded-operators). This theorem sits at the core of much of AQFT, and extensive use of this theorem will be made in subsequent work.

Here, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

# Spectral Theorem: Bounded Self-Adjoint Operators
In this section we will state and prove the Spectral Theorem for bounded, self-adjoint operators. However, we must introduce "extensive machinery" before we are able to state and prove the theorem. To that end we begin by examining some properties of bounded operators.

## Elementary Properties of Bounded Operators
In this section we will introduce and prove some relatively "elementary" properties of bounded operators that will be of use when proving the Spectral Theorem for bounded, self-adjoint operators. We begin by introducing some notation

> **Definition** *(Bounded Operator Notation)*
<a name="def:bounded-operator-notation"></a>
> We notate the set of operators on a separable, complex Hilbert space $$\mathbf{H}$$ that are bounded with respect to the operator norm as $$\mathcal{B}(\mathbf{H})$$.

along with an "elementary" lemma that proves $$\mathcal{B}(\mathbf{H})$$ is a Banach space

> **Lemma** *(Bounded Operators form a Banach Space)*
<a name="lmm:bounded-operators-form-a-banach-space"></a>
<!--  \uses{def:bounded-operator-notation} -->
> $$\mathcal{B}(\mathbf{H})$$ forms a Banach space under the operator norm.

**Proof**
By definition a Banach space is a normed vector space that is complete with respect to the distance function associated to its norm. Hence, we must prove that $$\mathcal{B}(\mathbf{H})$$ is a normed vector space that is complete with respect to the distance function associated to its norm.

The norm we place on $$\mathcal{B}(\mathbf{H})$$ is the operator norm. The operator norm is indeed a norm. Hence, $$\mathcal{B}(\mathbf{H})$$ is normed.

Next we must prove that $$\mathcal{B}(\mathbf{H})$$ is a vector space. Consider $$A, B \in \mathcal{B}(\mathbf{H})$$ as well as $$\alpha, \beta \in \mathbb{C}$$. As the operator norm is a norm we have

$$
\begin{align}
    \|\alpha A + \beta B\| &\le \|\alpha A\| + \|\beta B\| \\
                           &=    |\alpha| \, \|A\| + |\beta| \, \|B\| \\
                           &< \infty,
\end{align}
$$

where the final step follows from the fact that $$A, B \in \mathcal{B}(\mathbf{H})$$ and thus $$\|A\|$$ and $$\|B\|$$ are bounded with respect to the operator norm. This implies that $$\alpha A + \beta B$$ is bounded and thus a member of $$\mathcal{B}(\mathbf{H})$$. This in turn implies that $$\mathcal{B}(\mathbf{H})$$ is a vector space.

Finally we must prove that $$\mathcal{B}(\mathbf{H})$$ is complete with respect to the distance function associated to the operator norm.

Consider a Cauchy sequence $$\{A_i\}_{i \in \mathbb{N}}$$ in $$\mathcal{B}(\mathbf{H})$$. The definition of Cauchy sequence implies that for any $$\epsilon > 0$$ there exists a $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

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

where the first line follows from linearity and the second line follows from the operator norm definition. As $$\{A_i\}_{i \in \mathbb{N}}$$ is a Cauchy sequence, for any $$\epsilon > 0$$ there exists a $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

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

As $$\mathbf{H}$$ is complete, this Cauchy sequence $$\{A_i\psi\}_{i \in \mathbb{N}}$$ converges to an element of $$\mathbf{H}$$. With this knowledge, we can define a map $$A : \mathbf{H} \rightarrow \mathbf{H}$$ point-wise as follows

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

If this fixed $$\psi$$ is such that $$\|\psi\| = 1$$, then for any $$\epsilon > 0$$ there exists a $$N \in \mathbb{N}$$ such that for all $$i,j \ge N$$ we have

$$
\begin{align}
    \|A_i\psi - A_j\psi\| &\le \|A_i - A_j\| \, \|\psi\| \\
                          &= \|A_i - A_j\| \\
                          &< \epsilon.
\end{align}
$$

Fixing an $$i \ge N$$ and taking the limit as $$j \rightarrow \infty$$ we have, as a result of continuity of the norm and our previous result

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
<!--  \uses{def:bounded-operator-notation} -->
> The *bounded inverse* of $$A \in \mathcal{B}(\mathbf{H})$$ is an element $$B \in \mathcal{B}(\mathbf{H})$$ such that $$AB = BA = \mathbf{1}$$, where $$\mathbf{1} \in \mathcal{B}(\mathbf{H})$$ is the multiplicative identity element.

This is required to define the "spectrum" of an operator, which is required by much of what follows

> **Definition** *(Resolvent and Spectrum)*
<a name="def:bounded-operator-resolvent-and-spectrum"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-inverse} -->
> For $$A \in \mathcal{B}(\mathbf{H})$$, the *resolvent set* of $$A$$, denoted as $$\rho(A)$$, is the set of all $$\lambda \in \mathbb{C}$$ such that the operator $$(A - \lambda \mathbf{1})$$ has a bounded inverse. The *spectrum* of $$A$$, denoted by $$\sigma(A)$$, is the complement of $$A$$'s resolvent set $$\rho(A)$$ in $$\mathbb{C}$$. For $$\lambda$$ in the resolvent set of $$A$$ the bounded inverse of $$(A - \lambda \mathbf{1})$$, which we notate as $$(A - \lambda \mathbf{1})^{-1}$$, is called the *resolvent* of $$A$$ at $$\lambda$$.

## Spectral Theorem for Bounded Self-Adjoint Operators
In this section we will actually be able to state the Spectral Theorem. However, we will only be able to do so after introducing "substantial machinery" related to "projection-valued measures".

### Projection-Valued Measures
"Projection-valued measures" are "core" to the Spectral Theorem. Basically, they generalize the notion of a measure. A "projection-valued measure", instead of taking on positive, real-values as a standard measure does, takes on "bounded orthogonal projection" values. Formally, we define this by first introducing the notion of a "bounded orthogonal projection"

> **Definition** *(Orthogonal Projection)*
<a name="def:bounded-orthogonal-projection"></a>
<!--  \uses{def:bounded-operator-notation} -->
> A *bounded orthogonal projection*, sometimes shortened to *orthogonal projection* or simply *projection*, is an element $$P \in \mathcal{B}(\mathbf{H})$$ such that $$P^2 = P$$ and $$P^* = P$$.

The notion of a bounded orthogonal projection can then be employed to define a "projection-valued measure"

> **Definition** *(Projection-Valued Measure)*
<a name="def:projection-valued-measure"></a>
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

Now, we can associate a positive, real-valued measure $$\mu_\psi$$ to a projection-valued measure $$\mu$$ and any $$\psi \in \mathbf{H}$$ as follows:

> **Theorem** *(Projection-Valued Measure's Associated Measure)*
<a name="thrm:projection-valued-measures-associated-measure"></a>
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

Next let us prove non-negativity, i.e. for all $$E \in \Omega(X)$$, it follows that $$\mu_\psi(E) \ge 0$$.  The definition of $$\mu_\psi$$, the projection-valued measure $$\mu$$, and of an orthogonal projection imply

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

where the third equality follows from the definition of an inner product. This implies

$$
    \mu_\psi \left( \bigcup_{j = 1}^{\infty} E_j \right) = \sum_{j = 1}^{\infty} \mu_\psi(E_j),
$$

which is the desired result.

Together these imply that $$\mu_\psi$$ defines a positive, real-valued measure $$\mu_\psi$$ on $$\Omega(X)$$. $$\blacksquare$$

Projection-valued measures give rise to a type of integration known as "operator-valued integration". The primary properties of "operator-valued integration" are described by the following theorem

> **Theorem** *(Operator-Valued Integration)*
<a name="thrm:operator-valued-integration"></a>
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{lmm:lemma1-of-operator-valued-integration} -->
<!--  \uses{lmm:lemma2-of-operator-valued-integration} -->
<!--  \uses{prpstn:hall-a.61} -->
<!--  \uses{prpstn:hall-a.63} -->
<!--  \uses{thrm:complex-valued-simple-approximation-theorem} -->
<!--  \uses{prpstn:hall-a.43} -->
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
> for all $$f$$ and $$\psi \in \mathbf{H}$$, where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure’s Associated Measure)*](#thrm:projection-valued-measures-associated-measure) and $$\left< \cdot, \cdot \right>$$ is the Hilbert space inner product on $$\mathbf{H}$$. This unique linear map has the following additional properties
>
> 1. For all $$E \in \Omega(X)$$, we have
>
>    $$
>        \int_X 1_E \, d\mu = \mu(E),
>    $$
>
>    where $$1_E$$ is the indicator function of $$E$$. In particular, the integral of the constant function $$1$$ is the multiplicative identity $$\mathbf{1}$$.
> 2. For all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have
>
>    $$
>        \left\| \, \int_X f \, d\mu \, \right\| \le \sup\limits_{\lambda \in X} \left| f(\lambda) \right|,
>    $$
>
>    where $$\| \cdot \|$$ is the operator norm and $$\mid \cdot \mid$$ is the norm on $$\mathbb{C}$$.
> 3. Integration is multiplicative: For all bounded, measurable, complex-valued functions $$f$$ and $$g$$ on $$X$$, we have
>
>    $$
>        \int_X fg \, d\mu = \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right).
>    $$
>
> 4. For all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have
>
>    $$
>        \int_X \overline{f} \, d\mu = \left( \int_X f \, d\mu \right)^*,
>    $$
>
>    where $$\overline{f}$$ is the complex conjugate of $$f$$ and the superscript $$*$$ denotes the adjoint on $$\mathcal{B}(\mathbf{H})$$ arising from the Hilbert space inner product. In particular, if $$f$$ is real-valued, then $$f = \overline{f}$$ and
>
>    $$
>        \left( \int_X f \, d\mu \right) = \left( \int_X \overline{f} \, d\mu \right) = \left( \int_X f \, d\mu \right)^*
>    $$
>
>    is self-adjoint.

**Proof**

To streamline the proof of this theorem, we will introduce a few new terms

> **Definition** *((Bounded) Sesquilinear Form)*
<a name="def:bounded-sesquilinear-form"></a>
> A *sesquilinear form* on a Hilbert space $$\mathbf{H}$$ is a map $$L : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ that is conjugate linear in the first factor and linear in the second factor. A sesquilinear form  $$L$$ is a *bounded sesquilinear form* if there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi, \psi \in \mathbf{H}$$
>
> $$
>     |L(\phi, \psi)| \le C \|\phi\| \, \|\psi\|,
> $$
>
> where $$\mid\cdot\mid$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

> **Definition** *((Bounded) Quadratic Form)*
<a name="def:bounded-quadratic-form"></a>
<!--  \uses{def:bounded-sesquilinear-form} -->
> A *quadratic form* on a Hilbert space $$\mathbf{H}$$ is a map $$Q : \mathbf{H} \rightarrow \mathbb{C}$$ with the following properties:
>
> 1. $$Q(\lambda\psi) = \mid\lambda\mid^2 Q(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.
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
>     |Q(\phi)| \le C \|\phi\|^2,
> $$
>
> where $$\mid \cdot \mid$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

These will now let us begin the proof of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration)

By hypothesis we have a projection-valued measure $$\mu$$. Consider any bounded, measurable, complex-valued function $$f$$ on $$X$$ and any $$\psi \in \mathbf{H}$$. With this, let us define a map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure’s Associated Measure)*](#thrm:projection-valued-measures-associated-measure). It turns out that such a $$Q_f(\psi)$$ is a bounded quadratic form which we now prove

> **Lemma**
<a name="lmm:lemma1-of-operator-valued-integration"></a>
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
> where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure’s Associated Measure)*](#thrm:projection-valued-measures-associated-measure), is a bounded quadratic form.

**Proof**
To prove this result we will first prove the result for indicator functions, then for simple functions, and finally for bounded, measurable, complex-valued functions.

Let us start this proof by proving it is true for the case of indicator functions. Consider an arbitrary $$E \in \Omega(X)$$ and its indicator function $$1_E$$. In this case the definition of $$Q_{1_E}$$, standard properties of integration, and the definition of $$\mu_\psi$$ implies

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

1. $$Q_{1_E}(\lambda\psi) = \mid\lambda\mid^2 Q_{1_E}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$.
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
       |Q_{1_E}(\phi)| \le C \|\phi\|^2,
   $$

   where $$\mid \cdot \mid$$ is the norm on $$\mathbb{C}$$ and $$\|\cdot\|$$ is the norm on $$\mathbf{H}$$.

Let us first prove that $$Q_{1_E}(\lambda\psi) = \mid\lambda\mid^2 Q_{1_E}(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$. As a result of our previous derivation, the definition of an inner product, and the definition of the norm on $$\mathbb{C}$$ one has

$$
\begin{align}
  Q_{1_E}(\lambda\psi) &= \left< \lambda\psi, \mu(E) \lambda\psi \right> \\
                       &= \lambda^*\lambda \left< \psi, \mu(E) \psi \right> \\
                       &= \mid\lambda\mid^2 \left< \psi, \mu(E) \psi \right> \\
                       &= \mid\lambda\mid^2 Q_{1_E}(\psi),
\end{align}
$$

which proves $$Q_{1_E}(\lambda\psi) = \mid\lambda\mid^2 Q_{1_E}(\psi)$$, the desired result.

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
    |Q_{1_E}(\phi)| \le C \|\phi\|^2.
$$

Using the results of our previous derivation, the definition of an orthogonal projection, and standard properties of an inner product and its associated norm we have

$$
\begin{align}
    |Q_{1_E}(\phi)| &= | \left< \phi, \mu(E) \phi \right> | \\
                    &= | \left< \phi, \mu(E) \mu(E) \phi \right> | \\
                    &= | \left< \phi, \mu(E)^* \mu(E) \phi \right> | \\
                    &= | \left< \mu(E) \phi, \mu(E) \phi \right> | \\
                    &= | \|\mu(E) \phi\|^2 | \\
                    &= \|\mu(E) \phi\|^2 \\
                    &\le \|\phi\|^2,
\end{align}
$$

where the final inequality follows from the fact that $$\mu(E)$$ is an orthogonal projection. This proves that

$$
    |Q_{1_E}(\phi)| \le \|\phi\|^2,
$$

which implies that the constant required to prove that $$Q_{1_E}$$ is a bounded quadratic form is simply $$1$$. This concludes the proof of the indicator function result, $$Q_{1_E}$$ is a bounded quadratic form for any indicator function $$1_E$$.

Next we will prove that any simple function $$s$$, i.e. any finite linear combination of indicator functions

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

To prove that such a $$Q_s$$ is a bounded quadratic for we must prove the same three results.

First we must prove that $$Q_s(\lambda\psi) = \mid\lambda\mid^2 Q_s(\psi)$$. This follows from our indicator function result

$$
\begin{align}
    Q_s(\lambda\psi) &= \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\lambda\psi) \\
                     &= \sum_{i = 1}^n \alpha_i |\lambda|^2 Q_{1_{E_i}}(\psi) \\
                     &= |\lambda|^2 \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\psi) \\
                     &= |\lambda|^2 Q_s(\psi),
\end{align}
$$

giving the desired result $$Q_s(\lambda\psi) = \mid\lambda\mid^2 Q_s(\psi)$$.

Next we must prove the map $$L_s : \mathbf{H} \times \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
\begin{align}
    L_s(\phi, \psi) &= \frac{1}{2} \left[ Q_s(\phi + \psi) - Q_s(\phi) - Q_s(\psi) \right] \\
                    &-\frac{i}{2} \left[ Q_s(\phi + i\psi) - Q_s(\phi) - Q_s(i\psi) \right]
\end{align}
$$

is a sesquilinear form on $$\mathbf{H}$$. Basically this result follows from linearity and our indicator function result.

As

$$
    Q_s(\psi) = \sum_{i = 1}^n \alpha_i  Q_{1_{E_i}}(\psi)
$$

we have

$$
  L_s(\phi, \psi) = \sum_{i = 1}^n \alpha_i L_{1_{E_i}}(\phi, \psi).
$$

From our indicator function result we know that each $$L_{1_{E_i}}(\phi, \psi)$$ is conjugate linear in the first factor and linear in the second factor. Hence, $$L_s(\phi, \psi)$$ is conjugate linear in the first factor and linear in the second factor. Thus $$L_s(\phi, \psi)$$ is a sesquilinear form on $$\mathbf{H}$$, the desired result.

Finally, we must prove that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    |Q_s(\phi)| \le C \|\phi\|^2.
$$

This again follows from linearity and our indicator function result. We have

$$
\begin{align}
  |Q_s(\phi)| &= \left| \sum_{i = 1}^n \alpha_i Q_{1_{E_i}}(\phi) \right| \\
              &\le \sum_{i = 1}^n \left| \alpha_i Q_{1_{E_i}}(\phi) \right| \\
              &= \sum_{i = 1}^n \left|\alpha_i\right| \, \left| Q_{1_{E_i}}(\phi) \right| \\
              &\le \sum_{i = 1}^n \left|\alpha_i\right| \|\phi\|^2 \\
              &\le \left( \sum_{i = 1}^n \left|\alpha_i\right| \right) \|\phi\|^2.
\end{align}
$$

This gives the desired result

$$
    |Q_s(\phi)| \le C \|\phi\|^2
$$

for

$$
    C = \sum_{i = 1}^n \left|\alpha_i\right|.
$$

This completes the proof that $$Q_s$$ is a bounded quadratic form for any simple function $$s$$.

Next we will prove that for any bounded, measurable, complex-valued function $$f$$ the map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ defined by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

is a bounded quadratic form. This proof relies upon our previous simple function result along with the Complex-Valued Simple Approximation Theorem

> **Theorem** *(Complex-Valued Simple Approximation Theorem)*
<a name="thrm:complex-valued-simple-approximation-theorem"></a>
> Given any bounded, measurable, complex-valued function $$f$$ on a measurable set $$X$$, there exists a sequence of complex-valued simple functions $$\{s_i\}_{i \in \mathbb{N}}$$ on $$X$$ such that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ on $$X$$.

To wit we must first prove that $$Q_f(\lambda\psi) = \mid\lambda\mid^2 Q_f(\psi)$$. This follows from our simple function result and the Complex-Valued Simple Approximation Theorem. One has

$$
\begin{align}
    Q_f(\lambda\psi) &= \int_X f \, d\mu_{\lambda\psi} \\
                     &= \int_X \lim\limits_{i \rightarrow \infty} s_i \, d\mu_{\lambda\psi} \\
                     &= \lim\limits_{i \rightarrow \infty} \int_X s_i \, d\mu_{\lambda\psi} \\
                     &= \lim\limits_{i \rightarrow \infty} Q_{s_i}(\lambda\psi) \\
                     &= \lim\limits_{i \rightarrow \infty} \left|\lambda\right|^2 Q_{s_i}(\psi) \\
                     &= \left|\lambda\right|^2 \lim\limits_{i \rightarrow \infty} Q_{s_i}(\psi) \\
                     &= \left|\lambda\right|^2 Q_f(\psi),
\end{align}
$$

where the second equality follows from the Complex-Valued Simple Approximation Theorem, the third from the fact that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ and thus the limit can be pulled out of the integral, the fourth from the definition of $$Q_{s_i}$$, the fifth from our simple function result, and the final as before from uniform convergence and the Complex-Valued Simple Approximation Theorem. So in summary we have proven that

$$
    Q_f(\lambda\psi) = \left|\lambda\right|^2 Q_f(\psi),
$$

which is the first desired result.

A similar argument implies that $$L_f$$ defined by

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
    |Q_f(\phi)| \le C \|\phi\|^2.
$$

for all $$\phi \in \mathbf{H}$$. It is to this we now turn.

The definition of $$Q_f$$, triangle inequality for integrals, and the fact that $$f$$ is bounded imply

$$
\begin{align}
    \left| Q_f(\phi) \right| &= \left| \int_X f \, d\mu_\phi \right| \\
                             &\le \int_X \left| f \right| \, d\mu_\phi \\
                             &\le \int_X \left(  \sup\limits_{\lambda \in X} \left| f(\lambda) \right| \right) \, d\mu_\phi \\
                             &= \left( \sup\limits_{\lambda \in X} \left| f(\lambda) \right| \right) \int_X d\mu_\phi.
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
    \left| Q_f(\phi) \right| \le \left( \sup\limits_{\lambda \in X} \left| f(\lambda) \right| \right) \| \phi \|^2
$$

which, if we make the identification

$$
    C = \left( \sup\limits_{\lambda \in X} \left| f(\lambda) \right| \right),
$$

is nothing more than the statement that there exists a constant $$C$$ in $$\mathbb{R}$$ such that for all $$\phi$$ in $$\mathbf{H}$$

$$
    |Q_f(\phi)| \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$, the desired result.

This concludes our proof that for any bounded, measurable, complex-valued function $$f$$ on the set $$X$$ with $$\sigma$$-algebra $$\Omega(X)$$ the map $$Q_f$$ is a bounded quadratic form. $$\blacksquare$$

Our next step in the larger proof is establishing several propositions we will have need of later in our argument. To wit let us first prove the proposition (Proposition A.61 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Proposition**
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

The definition of a quadratic form along with standard properties of the norm $$\mid \cdot \mid$$ imply

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
        &-\frac{i}{2} \left[ Q((1 + i)\psi) - Q(\psi) - |i|^2 Q(\psi) \right]
    \end{aligned} \\
    &=
    \begin{aligned}[t]
        &\frac{1}{2} \left[ |2|^2Q(\psi) - 2Q(\psi) \right] \\
        &-\frac{i}{2} \left[ |1 + i|^2Q(\psi) - 2Q(\psi) \right]
    \end{aligned} \\
    &= Q(\psi),
\end{align}
$$

the desired result $$L(\psi, \psi) = Q(\psi)$$.

Let us next prove that if $$Q$$ is bounded, then $$L$$ is bounded.

In this case by hypothesis $$Q$$ is bounded. Hence, there exists a $$C$$ in $$\mathbb{R}$$ such that

$$
    \left| Q(\psi) \right| \le C \|\psi\|^2
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
                     &=    \|\phi\| + |i| \|\psi\| \\
                     &=    \|\phi\| + \|\psi\| \\
                     &=    2,
\end{align}
$$

which implies $$\|\phi + i\psi\| \le 2$$.

This, along with the definition of a norm and the fact that $$Q$$ is bounded, implies

$$
\begin{align}
    \left| L(\phi, \psi) \right| &= \left| \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] -\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right] \right| \\
    &\le \frac{1}{2} \left[ \left|Q(\phi + \psi)\right| + \left|Q(\phi)\right| + \left|Q(\psi)\right| + \left|Q(\phi + i\psi)\right| + \left|Q(\phi)\right| + \left|Q(i\psi)\right| \right] \\
    &\le C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + \|i\psi\|^2 \right] \\
    &=   C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + |i|^2 \, \|\psi\|^2 \right] \\
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
    \left|L(\phi, \psi)\right| = \|\phi\| \, \|\psi\| \, \left| L(\widehat{\phi}, \widehat{\psi}) \right| \le 6C \|\phi\| \, \|\psi\|,
$$

where the inequality follows from our previous result. This we have proven the second desired result

$$
    \left|L(\phi, \psi)\right| \le 6C \|\phi\| \, \|\psi\|,
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

Finally, as $$Q$$ is a quadratic form, and thus satisfies $$Q(\lambda\psi) = \mid\lambda\mid^2 Q(\psi)$$ for all $$\psi \in \mathbf{H}$$ and $$\lambda \in \mathbb{C}$$, one has

$$
\begin{align}
    M(i\phi, i\psi) &= \frac{1}{2} \left[ Q(i\phi + i\psi) - Q(i\phi) - Q(i\psi) \right] \\
                    &= \frac{1}{2} \left[ Q(i(\phi + \psi)) - |i|^2Q(\phi) - |i|^2Q(\psi) \right] \\
                    &= \frac{1}{2} \left[ |i|^2Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
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

The next in the set of "helper" propositions that we will prove is the proposition (Proposition A.63 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Proposition**
<a name="prpstn:hall-a.63"></a>
<!--  \uses{def:bounded-quadratic-form} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-a.61} -->
> If $$Q$$ is a bounded quadratic form on $$\mathbf{H}$$, there is a unique $$A \in \mathcal{B}(\mathbf{H})$$ such that $$Q(\psi) = \left< \psi, A\psi \right>$$ for all $$\psi \in \mathbf{H}$$. If $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then the operator $$A$$ is self-adjoint.

**Proof**
By hypothesis $$Q$$ is a bounded quadratic form. Hence, as a result of the [**Proposition**](#prpstn:hall-a.61) we just proved, the sesquilinear form associated to $$Q$$ is bounded. This implies that there exists a constant $$C$$ in $$\mathbb{R}$$ such that

$$
    \left| L(\phi, \psi) \right| \le C \|\phi\| \, \|\psi\|,
$$

for all $$\phi, \psi \in \mathbf{H}$$.

Hence, for any fixed $$\phi \in \mathbf{H}$$, the operator norm of the linear map $$\psi \mapsto L(\phi, \psi)$$ is bounded, with operator norm at most $$C \|\phi\|$$.

Explicitly, $$\psi \mapsto L(\phi, \psi)$$ is linear as a result of $$Q$$ being a quadratic form, which implies $$L$$ is a sesquilinear form, which in turn implies that $$\psi \mapsto L(\phi, \psi)$$ is linear in $$\psi$$.

Furthermore, the definition of operator norm implies

$$
    \|L(\phi, \cdot)\| \equiv \sup\limits_{\|\psi\| = 1} |L(\phi, \psi)|.
$$

The fact that $$L$$ is bounded as a sesquilinear form implies

$$
    \left| L(\phi, \psi) \right| \le C \|\phi\| \, \|\psi\|,
$$

for our fixed $$\phi$$ and any $$\psi \in \mathbf{H}$$. So for any $$\psi$$ such that $$\|\psi\| = 1$$

$$
    \left| L(\phi, \psi) \right| \le C \|\phi\|.
$$

Hence, these together imply

$$
    \|L(\phi, \cdot)\| \equiv \sup\limits_{\|\psi\| = 1} |L(\phi, \psi)| \le C \|\phi\|,
$$

the desired result.

Now as one will recall the Riesz Theorem (Theorem A.52 (Riesz Theorem) of [Hall](https://doi.org/10.1007/978-1-4614-7116-5)) states

> **Theorem** *(Riesz Theorem)*
> If $$\xi : \mathbf{H} \rightarrow \mathbb{C}$$ is a bounded linear functional on the Hilbert space $$\mathbf{H}$$, then there exists a unique $$\chi \in \mathbf{H}$$ such that
>
> $$
>     \xi(\psi) = \left< \chi, \psi \right>
> $$
>
> for all $$\psi \in \mathbf{H}$$. Furthermore, the operator norm of $$\xi$$ as a bounded linear functional is equal to the norm of $$\chi$$ as an element of $$\mathbf{H}$$.

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
    L(\alpha_1 \phi_1 + \alpha_2 \phi_1 , \psi) = \left< B(\alpha_1 \phi_1 + \alpha_2 \phi_1), \psi \right>.
$$

As $$L$$ is a sesquilinear form and thus conjugate-linear in its first argument

$$
    L(\alpha_1\phi_1 + \alpha_2\phi_2, \psi) = \overline{\alpha_1} L(\phi_1, \psi) + \overline{\alpha_2} L(\phi_2, \psi).
$$

Hence, for any $$\psi \in \mathbf{H}$$

$$
    \left< B(\alpha_1 \phi_1 + \alpha_2 \phi_1), \psi \right> = \overline{\alpha_1} \left< B\phi_1, \psi \right> + \overline{\alpha_2}  \left< B\phi_2, \psi \right> = \left< \alpha_1 B\phi_1 + \alpha_2 B\phi_2, \psi \right>
$$

where the final equality uses the fact that the inner product is conjugate-linear in its first argument. As this is true for any $$\psi \in \mathbf{H}$$ it implies

$$
    B(\alpha_1 \phi_1 + \alpha_2 \phi_1) =  \alpha_1 B\phi_1 + \alpha_2 B\phi_2,
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

for all $$\psi \in \mathbf{H}$$. We then define the operator valued integral of $$f$$ as follows

$$
    f \longmapsto \int_X f d\mu \equiv A_f.
$$

By construction it is a map from the space of bounded, measurable, complex-valued functions to $$\mathcal{B}(\mathbf{H})$$, as required.

**Property 0:** Tracing definitions it is obvious that this satisfies the required property

$$
    \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = \int_X f d\mu_\psi
$$

of an operator valued integral. Explicitly, the definition of the operator valued integral along with the definition of $$Q_f$$ imply

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

**Property 1:** Next we must prove that for all $$E \in \Omega(X)$$, we have

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

for all $$\psi \in \mathbf{H}$$. Hence, $$A_{1_E} = \mu(E)$$. Thus the definition of the operator valued integral implies

$$
    \int_X 1_E \, d\mu = \mu(E),
$$

which is the desired result.

**Property 2:** The next result we must prove is that for all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have

$$
    \left\| \, \int_X f \, d\mu \, \right\| \le \sup\limits_{\lambda \in X} \left| f(\lambda) \right|,
$$

where $$\| \cdot \|$$ is the operator norm and $$\mid \cdot \mid$$ is the norm on $$\mathbb{C}$$.

To prove this we will first prove a "utility" lemma that will aid our argument.

> **Lemma**
> <a name="lmm:lemma2-of-operator-valued-integration"></a>
> <!--  \uses{def:projection-valued-measure} -->
> <!--  \uses{def:bounded-operator-notation} -->
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

> **Lemma**
<a name="lmm:lemma-1"></a>
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

In this case the definition of a norm implies $$\|\psi\| = 0$$. Similarly, for all $$\chi \in \mathbf{H}$$ we have $$\lvert \left< \chi, 0 \right> \rvert = 0$$. Thus we have the trivial equality in this case, both the lefthand and righthand side of the desired equation are zero.

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
    \left| \left< \chi_0, \psi \right> \right| &= \left| \left< \frac{\psi}{\|\psi\|}, \psi \right> \right| \\
                                            &= \left| \frac{1}{\|\psi\|} \left< \psi, \psi \right> \right| \\
                                            &= \frac{1}{\|\psi\|} \left| \left< \psi, \psi \right> \right| \\
                                            &= \frac{1}{\|\psi\|} \left| \|\psi\|^2 \right| \\
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

Now as this point we have proven that

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

With this lemma proven, we can once again continue on with our main argument.

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

Now using the definition of a norm and applying [**Cauchy–Schwarz**](#prpstn:hall-a.43)

> **Proposition** *(Cauchy–Schwarz Inequality)*
<a name="prpstn:hall-a.43"></a>
> If $$V$$ is a space with an inner product, then for all $$\phi, \psi \in V$$, we have the *Cauchy–Schwarz inequality*
>
> $$
>     \lvert \left< \phi, \psi \right> \rvert^2 \le \left< \phi, \phi \right> \left< \psi, \psi \right>.
> $$

twice, first to each summand and then across the sum (viewing $$\|\mu(E_i) \phi\|$$ and $$\|\mu(E_i) \psi\|$$ as vectors in $$\mathbb{R}^n$$), one obtains

$$
\begin{align}
    \left| \left< \phi, A_s \psi \right> \right| &= \left| \sum_{i = 1}^n c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right| \\
                                                 &\le \sum_{i = 1}^n \left| c_i \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right| \\
                                                 &= \sum_{i = 1}^n \left| c_i \right| \, \left| \left< \mu(E_i) \phi, \mu(E_i) \psi \right> \right| \\
                                                 &\le \sum_{i = 1}^n \left| c_i \right| \left\| \mu(E_i) \phi \right\| \left\| \mu(E_i) \psi \right\| \\
                                                 &\le \left( \max_i \left| c_i \right| \right)  \sum_{i = 1}^n \left\| \mu(E_i) \phi \right\| \left\| \mu(E_i) \psi \right\| \\
                                                 &\le \left( \max_i \left| c_i \right| \right) \left( \sum_{i = 1}^n \left\| \mu(E_i) \phi \right\|^2 \right)^{1/2} \left( \sum_{i = 1}^n \left\| \mu(E_i) \psi \right\|^2 \right)^{1/2} \\
                                                 &= \left( \max_i \left| c_i \right| \right) \|\phi\| \, \|\psi\|,
\end{align}
$$

where in the final step we employed the second result of [**Lemma**](#lmm:lemma2-of-operator-valued-integration). So in summary

$$
    \left| \left< \phi, A_s \psi \right> \right| \le \left( \max_i \left| c_i \right| \right) \|\phi\| \, \|\psi\|
$$

for all $$\phi, \psi \in \mathbf{H}$$.

Now another way one can write the operator norm of $$A_s$$, or really any element of $$\mathcal{B}(\mathbf{H})$$, is as follows

$$
    \|A_s\| = \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left| \left< \phi, A_s \psi \right> \right|.
$$

Hence, our result implies

$$
\begin{align}
    \|A_s\| &= \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left| \left< \phi, A_s \psi \right> \right| \\
            &\le \sup_{\|\phi\| = 1 \text{ } \|\psi\| = 1} \left( \max_i \left| c_i \right| \right) \|\phi\| \, \|\psi\| \\
            &= \left( \max_i \left| c_i \right| \right).
\end{align}
$$

Obviously

$$
    \sup_{\lambda \in X} | s(\lambda) | = \max_i \left| c_i \right|.
$$

Hence, we have proven the desired result

$$
    \|A_s\|  \le \sup_{\lambda \in X} | s(\lambda) |
$$

for our simple function $$s$$. What remains to do is to generalize this to a bounded, measurable, complex-valued function $$f$$.

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
    \|A_{s_i - s_j}\| \le \sup_{\lambda \in X} | s_i(\lambda) - s_j(\lambda) |.
$$

This in turn implies

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &= \|A_{s_i - s_j}\| \\
                          &\le \sup_{\lambda \in X} | s_i(\lambda) - s_j(\lambda) |.
\end{align}
$$

However, the definition of a norm implies

$$
\begin{align}
    | s_i(\lambda) - s_j(\lambda) | &=   | (f(\lambda) - s_j(\lambda)) - (f(\lambda) - s_i(\lambda))| \\
                                    &\le | f(\lambda) - s_j(\lambda) | + | f(\lambda) - s_i(\lambda) |.
\end{align}
$$

Hence, we can continue our derivation

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &= \|A_{s_i - s_j}\| \\
                          &\le \sup_{\lambda \in X} | s_i(\lambda) - s_j(\lambda) | \\
                          &\le \sup_{\lambda \in X} \left( | f(\lambda) - s_j(\lambda) | + | f(\lambda) - s_i(\lambda) | \right) \\
                          &\le \sup_{\lambda \in X} | f(\lambda) - s_j(\lambda) | + \sup_{\lambda \in X} | f(\lambda) - s_i(\lambda) |.
\end{align}
$$

However, as the sequence $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$k \ge N$$

$$
    \sup_{\lambda \in X}  | f(\lambda) - s_k(\lambda) | < \frac{\epsilon}{2}.
$$

This along with our previous derivation allows us to conclude that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i, j \ge N$$ we have

$$
\begin{align}
    \|A_{s_i} - A_{s_j}\| &\le \sup_{\lambda \in X} | f(\lambda) - s_j(\lambda) | + \sup_{\lambda \in X} | f(\lambda) - s_i(\lambda) | \\
                          &< \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
                          &= \epsilon.
\end{align}
$$

This is nothing more than the statement that $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ is a Cauchy sequence.

By construction each $$A_{s_i}$$ is an element of $$\mathcal{B}(\mathbf{H})$$. Hence, $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ is a sequence in $$\mathcal{B}(\mathbf{H})$$. As we proved in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space) $$\mathcal{B}(\mathbf{H})$$ is a Banach space. So, in particular, $$\mathcal{B}(\mathbf{H})$$ is complete. Thus there exists an operator $$A_s$$ in $$\mathcal{B}(\mathbf{H})$$ that is the limit of the sequence $$\{A_{s_i}\}_{i \in \mathbb{N}}$$ relative to the operator norm on $$\mathcal{B}(\mathbf{H})$$.

As the sequence $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$k \ge N$$

$$
    \sup_{\lambda \in X}  | f(\lambda) - s_k(\lambda) | < \epsilon.
$$

Hence, using the definition of a norm, we can conclude that for all $$k \ge N$$

$$
\begin{align}
    \sup_{\lambda \in X} | s_k(\lambda) | &=   \sup_{\lambda \in X} | f(\lambda) - (f(\lambda) - s_k(\lambda)) | \\
                                          &\le \sup_{\lambda \in X} | f(\lambda) | + | f(\lambda) - s_k(\lambda) | \\
                                          &\le \sup_{\lambda \in X} | f(\lambda) | + \sup_{\lambda \in X} | f(\lambda) - s_k(\lambda) | \\
                                          &< \sup_{\lambda \in X} | f(\lambda) | + \epsilon.
\end{align}
$$

This implies

$$
    \lim_{i \rightarrow \infty} \sup_{\lambda \in X} | s_i(\lambda) | \le \sup_{\lambda \in X} | f(\lambda) |.
$$

We can also create a similar derivation switching the roles of $$s_k$$ and $$f$$ as follows

$$
\begin{align}
    \sup_{\lambda \in X} | f(\lambda) | &= \sup_{\lambda \in X} | (f(\lambda) - s_k(\lambda)) + s_k(\lambda) | \\
                                        &\le \sup_{\lambda \in X} | f(\lambda) - s_k(\lambda) | +  | s_k(\lambda) | \\
                                        &\le \sup_{\lambda \in X} | f(\lambda) - s_k(\lambda) | +  \sup_{\lambda \in X} | s_k(\lambda) | \\
                                        &< \epsilon +  \sup_{\lambda \in X} | s_k(\lambda) |.
\end{align}
$$

This implies

$$
    \sup_{\lambda \in X} | f(\lambda) | \le \lim_{i \rightarrow \infty} \sup_{\lambda \in X} | s_i(\lambda) |.
$$

The last two conclusions imply

$$
    \lim_{i \rightarrow \infty} \sup_{\lambda \in X} | s_i(\lambda) | = \sup_{\lambda \in X} | f(\lambda) |.
$$

Now tying the last results together

$$
\begin{align}
    \|A_s\| &=   \lim_{i \rightarrow \infty} \| A_{s_i} \| \\
            &\le \lim_{i \rightarrow \infty} \sup_{\lambda \in X} | s_i(\lambda) | \\
            &= \lim_{i \rightarrow \infty} \sup_{\lambda \in X} | f(\lambda) | \\
            &= \sup_{\lambda \in X} | f(\lambda) |.
\end{align}
$$

In other words

$$
    \|A_s\| \le \sup_{\lambda \in X} | f(\lambda) |.
$$

As

$$
    \int_X f \, d\mu \equiv A_f,
$$

this is almost the desired result

$$
    \left\| \int_X f \, d\mu \right\| \le \sup_{\lambda \in X} | f(\lambda) |.
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

and thus the desired relation

$$
    \left\| \int_X f \, d\mu \right\| \le \sup_{\lambda \in X} | f(\lambda) |,
$$

is proven.

**Property 3:** Next we must prove that integration is multiplicative. In other words for all bounded, measurable, complex-valued functions $$f$$ and $$g$$ on $$X$$, we have

$$
    \int_X fg \, d\mu = \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right).
$$

As in other proofs, we will first prove this result for indicator functions, then simple functions, then finally for bounded, measurable, complex-valued functions.

Let us begin with indicator functions. Consider $$E_1, E_2 \in \Omega(X)$$. Property 1, which we have already proved, along with the projection-valued measure definition imply

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

Let us next prove the result for simple functions. This result follows from the indicator function result and linearity.

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

Hence, using linearity and our previous indicator function result we have

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

the desired simple function result.

Let us next prove the result for bounded, measurable, complex-valued functions.

As one will recall [**Theorem** *(Complex-Valued Simple Approximation Theorem)*](#thrm:complex-valued-simple-approximation-theorem) implies that there exist sequences of complex-valued simple functions $$\{s_i\}_{i \in \mathbb{N}}$$ and $$\{r_j\}_{j \in \mathbb{N}}$$ on $$X$$ such that $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to a bounded, measurable, complex-valued function $$f$$ on $$X$$ and similarly $$\{r_j\}_{j \in \mathbb{N}}$$ to $$g$$.

This along with linearity of operator-valued integration implies for any $$s_i$$

$$
\begin{align}
    \left\| \left( \int_X f \, d\mu \right) - \left( \int_X s_i \, d\mu \right) \right\|
    &= \left\| \int_X ( f - s_i ) \, d\mu \right\| \\
    &\le \sup\limits_{\lambda \in X} | f(\lambda) - s_i(\lambda) |,
\end{align}
$$

where in the final step we employed our **Property 2** result. As $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$, this implies that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i \ge N$$ one has

$$
    \left\| \left( \int_X f \, d\mu \right) - \left( \int_X s_i \, d\mu \right) \right\| < \epsilon,
$$

in other words the operator-valued integral of $$s_i$$ converges to the operator-valued integral of $$f$$. One can establish using similar logic that the operator-valued integral of $$r_i$$ converges to the operator-valued integral of $$g$$.

Similarly, uniform convergence along with linearity imply for any $$s_i$$ and $$r_j$$

$$
\begin{align}
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_j \, d\mu \right) \right\|
    &= \left\| \int_X (fg - s_i r_j) \, d\mu \right\| \\
    &\le \sup\limits_{\lambda \in X} | f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) |
\end{align}
$$

where in the final step we employed our **Property 2** result. Looking at this result and our previous similar result, one concludes that if we can prove that given any $$\epsilon > 0$$, there exists a natural number $$N$$ such that for all $$i,j \ge N$$ one has

$$
    \sup\limits_{\lambda \in X} | f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) | < \epsilon,
$$

then we can conclude that the operator-valued integral of $$s_ir_j$$ converges to the operator-valued integral of $$fg$$.

One can prove this desired convergence as follows. Consider any $$s_i$$ and $$r_j$$. One has

$$
\begin{align}
    |s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda)| &=   |s_i(\lambda)r_j(\lambda) - f(\lambda)r_j(\lambda) + f(\lambda)r_j(\lambda) - f(\lambda)g(\lambda)| \\
                                                      &\le |s_i(\lambda)r_j(\lambda) - f(\lambda)r_j(\lambda)| + |f(\lambda)r_j(\lambda) - f(\lambda)g(\lambda)| \\
                                                      &\le |r_j(\lambda)| \, |s_i(\lambda) - f(\lambda)| + |f(\lambda)| \, |r_j(\lambda) - g(\lambda)|.
\end{align}
$$

As $$f$$ is bounded and $$r_j$$ is a simple function, their suprema are finite numbers. This allows us to continue this derivation as follows

$$
    |s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda)| \le \left( \sup\limits_{\lambda \in X} |r_j(\lambda)| \right) |s_i(\lambda) - f(\lambda)| + \left( \sup\limits_{\lambda \in X} |f(\lambda)| \right) |r_j(\lambda) - g(\lambda)|.
$$

Now as $$s_j$$ converges uniformly to $$f$$, for any $$\epsilon > 0$$ there exists an $$N$$ such that for all $$i \ge N$$ one has

$$
    \sup\limits_{\lambda \in X} |s_i(\lambda) - f(\lambda)| < \left( \epsilon \left/ 2 \sup\limits_{\lambda \in X} |r_j(\lambda)| \right) \right. .
$$

Similarly, as $$r_j$$ converges uniformly to $$g$$, for this same $$\epsilon > 0$$ there exists an $$M$$ such that for all $$j \ge M$$ one has

$$
    \sup\limits_{\lambda \in X} |r_j(\lambda) - g(\lambda)| < \left( \epsilon \left/ 2 \sup\limits_{\lambda \in X} |f(\lambda)| \right) \right. .
$$

This implies that for all $$i,j \ge \max(N,M)$$ we have

$$
\begin{align}
    |s_i(\lambda)r_j(\lambda) - f(\lambda)g(\lambda)|
    &\le \left( \sup\limits_{\lambda \in X} |r_j(\lambda)| \right) |s_i(\lambda) - f(\lambda)| + \left( \sup\limits_{\lambda \in X} |f(\lambda)| \right) |r_j(\lambda) - g(\lambda)| \\
    &\le \left( \sup\limits_{\lambda \in X} |r_j(\lambda)| \right) \left( \frac{\epsilon}{2 \sup\limits_{\lambda \in X} |r_j(\lambda)|} \right)  + \left( \sup\limits_{\lambda \in X} |f(\lambda)| \right) \left( \frac{\epsilon}{2 \sup\limits_{\lambda \in X} |f(\lambda)|} \right) \\
    &< \frac{\epsilon}{2} +  \frac{\epsilon}{2} \\
    &= \epsilon.
\end{align}
$$

This implies that for any $$\epsilon > 0$$ there exists a natural number $$L$$ such that for all $$i,j \ge L$$ we have

$$
    \sup\limits_{\lambda \in X} |f(\lambda)g(\lambda) - s_i(\lambda)r_j(\lambda)| < \epsilon.
$$

This along with our previous result

$$
    \left\| \left( \int_X fg \, d\mu \right) - \left( \int_X s_i r_j \, d\mu \right) \right\| \le \sup\limits_{\lambda \in X} | f(\lambda) g(\lambda) - s_i(\lambda) r_j(\lambda) |
$$

this implies that the operator-valued integral of $$s_ir_j$$ converges to the operator-valued integral of $$fg$$.

Combining all of these results together we find

$$
\begin{align}
    \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right)
    &=  \left( \lim\limits_{i \rightarrow \infty} \int_X s_i \, d\mu \right) \left( \lim\limits_{j \rightarrow \infty} \int_x r_j \, d\mu \right)   \\
    &= \lim\limits_{i \rightarrow \infty} \lim\limits_{j \rightarrow \infty}  \left( \int_X s_i \, d\mu \right) \left( \int_x r_j \, d\mu \right)   \\
    &= \lim\limits_{i \rightarrow \infty} \lim\limits_{j \rightarrow \infty}  \int_X s_i r_j \, d\mu   \\
    &=  \int_X f g \, d\mu.
\end{align}
$$

This leads to the desired result

$$
    \left( \int_X f \, d\mu \right) \left( \int_X g \, d\mu \right) = \int_X f g \, d\mu
$$

for bounded, measurable, complex-valued functions $$f$$ and $$g$$.

**Property 4:** Finally we must prove that for all bounded, measurable, complex-valued functions $$f$$ on $$X$$, we have

$$
    \int_X \overline{f} \, d\mu = \left( \int_X f \, d\mu \right)^*,
$$

where $$\overline{f}$$ is the complex conjugate of $$f$$ and the superscript $$*$$ denotes the adjoint on $$\mathcal{B}(\mathbf{H})$$ arising from the Hilbert space inner product.

Let us start by considering the case in which $$f$$ is real. The definition of $$Q_f$$ states

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

for any bounded, measurable, complex-valued function $$f$$. This also completes the proof of [**Theorem** *(Operator-Valued Integration)*](#thrm:operator-valued-integration).$$\blacksquare$$

### The Spectral Theorem

Now we are finally in the position to state the spectral theorem for bounded operators.

> **Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*
<a name="thrm:spectral-theorem-for-bounded-operators"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:bounded-orthogonal-projection} -->
<!--  \uses{thrm:operator-valued-integration} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then there exists a unique projection-valued measure $$\mu^A$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$, the spectrum of $$A$$, with values in orthogonal projections on $$\mathbf{H}$$ such that
>
> $$
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
> $$

**Proof**
To facilitate the proof of this theorem, we first introduce the useful notion of "Functional Calculus".

> **Definition** *(Functional Calculus)*
<a name="def:functional-calculus"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:spectral-theorem-for-bounded-operators} -->
<!--  \uses{thrm:operator-valued-integration} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint and $$f : \sigma(A) \rightarrow \mathbb{C}$$ is a bounded measurable function on the spectrum $$\sigma(A)$$ of $$A$$, *functional calculus* defines an operator $$f(A)$$ by
>
> $$
>     f(A) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda),
> $$
>
> where $$\mu^A$$ is the unique projection-valued measure of [**Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*](#thrm:spectral-theorem-for-bounded-operators) associated to $$A$$.

With functional calculus defined, we can now outline the proof of [**Theorem** *(Spectral Theorem for Bounded, Self-Adjoint Operators)*](#thrm:spectral-theorem-for-bounded-operators). This proof consists of two main stages.

*Stage 1:* In the first stage any self-adjoint $$A \in \mathcal{B}(\mathbf{H})$$ is used to construct a "continuous functional calculus" that associates to each continuous function $$f$$ on $$\sigma(A)$$ an operator $$f(A)$$.

This association is such that for any natural number $$m$$ the function $$f(\lambda) = \lambda^m$$ is associated with the operator $$f(A)=A^m$$. The full "continuous functional calculus" is then constructed by approximating arbitrary continuous functions $$f$$ on $$\sigma(A)$$ by polynomials.

The [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass) implies that polynomials are dense in the space of continuous functions on $$\sigma(A)$$. Hence, for any continuous function $$f$$ on $$\sigma(A)$$ there exists a sequence of polynomials $$\{p_i\}_{i \in \mathbb{N}}$$ that converge uniformly to $$f$$ on $$\sigma(A)$$. The final step of stage 1 then proves that the sequence of operators $$\{p_i(A)\}_{i \in \mathbb{N}}$$ converge to an operator denoted as $$f(A)$$.

*Stage 2:* The second stage of the proof shows that for a continuous function $$f$$ on $$\sigma(A)$$ the operator $$f(A)$$ of the first stage can be represented as integration against a projection-valued measure. This amounts to an operator-valued version of the [**Riesz Representation Theorem**](#thrm:riesz-representation) from measure theory.

**Stage 1: The Continuous Functional Calculus**

We begin this stage of the proof with "utility" lemmas and propositions that we will have need of later in this stage.

> **Lemma**
<a name="lmm:hall-7.6"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-inverse} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
> Suppose $$X \in \mathcal{B}(\mathbf{H})$$ satisfies $$\|X\| < 1$$, where $$\|X\|$$ is the operator norm of $$X$$. Then the operator $$I - X$$ has a bounded inverse $$(I - X)^{-1}$$ in $$\mathcal{B}(\mathbf{H})$$; and this bounded inverse is given by the following series
>
> $$
>     (I - X)^{-1} = \mathbf{1} + X + X^2 + X^3 + \cdots
> $$
>
> that is convergent in $$\mathcal{B}(\mathbf{H})$$ with respect to the operator norm.

**Proof**
As the product of operators $$A,B \in \mathcal{B}(\mathbf{H})$$ is submultiplicative,

$$
    \|AB\| \le \|A\| \, \|B\|,
$$

for an arbitrary natural number $$m$$ one has

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

Finally, recalling the fact established in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space) that $$\mathcal{B}(\mathbf{H})$$ is a Banach space with respect to the operator norm, one can from the following proposition

> **Proposition**
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

conclude that the series $$\{X^m\}_{m \in \mathbb{N}}$$ converges in $$\mathcal{B}(\mathbf{H})$$ with respect to the operator norm. In other words the series

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

proving

$$
    (\mathbf{1} - X)^{-1} = \mathbf{1} + X + X^2 + X^3 + \cdots,
$$

the final desired result.$$\blacksquare$$

> **Proposition**
<a name="prpstn:hall-7.5"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-7.6} -->
<!--  \uses{thrm:analytic-equivalence-theorem} -->
<!--  \uses{thrm:maximum-modulus-principle} -->
> For all $$A \in \mathcal{B}(\mathbf{H})$$, the following results hold.
>
> 1. The spectrum $$\sigma(A)$$ of $$A$$ is a closed, bounded, and nonempty subset of $$\mathbb{C}$$.
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

This establishes that if $$\lvert \lambda \rvert > \|A\|$$, then $$\lambda$$ is in the resolvent set of $$A$$, which is the desired result of Point 2 of the proposition.

Furthermore, as $$\lvert \lambda \rvert > \|A\|$$ implies that $$\lambda$$ is in the resolvent set of $$A$$ and the spectrum $$\sigma(A)$$ is the complement of the resolvent set in $$\mathbb{C}$$, this also proves that the spectrum $$\sigma(A)$$ of $$A$$ is bounded. This is one of the desired results of Point 1 of the proposition.

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

can be expressed as a locally convergent power series with coefficients in $$\mathbb{C}$$. In other words it is an analytic function on the resolvent set of $$A$$ which, as we have proven, is open. Thus, as a result of the [**Analytic Equivalence Theorem**](#thrm:analytic-equivalence-theorem)

> **Theorem** *(Analytic Equivalence Theorem)*
<a name="thrm:analytic-equivalence-theorem"></a>
> Let $$U$$ be an open subset of $$\mathbb{C}$$ and let $$f: U \rightarrow \mathbb{C}$$ be a function. Then $$f$$ is analytic on $$U$$ if and only if it is holomorphic on $$U$$.

this function is holomorphic on the resolvent set of $$A$$.

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

Now let us assume the spectrum $$\sigma(A)$$ of $$A$$ is the empty set. Then the resolvent set of $$A$$, the complement of $$\sigma(A)$$ in $$\mathbb{C}$$,  would be all of $$\mathbb{C}$$. This would then imply that the holomorphic function $$\lambda \mapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ is holomorphic on all of $$\mathbb{C}$$. In other words it is an entire function.

Hence, by evaluating the entire function $$\lambda \mapsto \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ on ever larger closed disks $$\overline{B}$$, the [**Maximum Modulus Principle**](#thrm:maximum-modulus-principle)

> **Theorem** *(Maximum Modulus Principle)*
<a name="thrm:maximum-modulus-principle"></a>
> Let $$B$$ be a bounded, nonempty, connected open subset of $$\mathbb{C}$$. Let $$\overline{B}$$ be the closure of $$B$$. Suppose $$f : \overline{B} \rightarrow \mathbb{C}$$ is a continuous function that is holomorphic on $$B$$. Then $$\lvert f(z) \rvert$$ attains its maximum at some point on the boundary of $$B$$.

implies that the maximum of $$\lvert \left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right> \rvert$$ is zero. As a result of the definition of a norm, this in turn implies that $$\left< \phi, (A - \lambda \mathbf{1})^{-1} \psi \right>$$ is identically zero.

As this is true for any $$\phi, \psi \in \mathbf{H}$$, it implies that $$(A - \lambda \mathbf{1})^{-1}$$ has operator norm zero and is thus the zero operator. However, we know that $$(A - \lambda \mathbf{1})(A - \lambda \mathbf{1})^{-1} = \mathbf{1}$$. Thus, $$(A - \lambda \mathbf{1})^{-1}$$ can not be the zero operator, and we have arrived at a contradiction.

Hence, our assumption that the spectrum $$\sigma(A)$$ of $$A$$ is the empty set is false. The spectrum $$\sigma(A)$$ is non-empty. This is the final desired result of Part 1.$$\blacksquare$$

Another proposition we will have need of is

> **Proposition**
<a name="prpstn:hall-7.3"></a>
<!--  \uses{def:bounded-operator-notation} -->
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

> **Lemma**
<a name="lmm:hall-7.8"></a>
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

Now we move onto the result

> **Proposition**
<a name="prpstn:hall-7.7"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-7.8} -->
<!--  \uses{prpstn:hall-7.3} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$.

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
    \| (A - \lambda \mathbf{1}) \psi_j - (A - \lambda \mathbf{1}) \psi_i \| < \epsilon b.
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

Now as $$A \in \mathcal{B}(\mathbf{H})$$ it is a bounded linear operator from the normed space $$\mathbf{H}$$ to the normed space $$\mathbf{H}$$. Thus, as a result of the standard proposition

> **Proposition** *(Bounded Operators are Continuous)*
> A linear operator between normed spaces is bounded if and only if it is continuous.

$$A$$ is continuous. As $$A$$ is continuous our definitions imply

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

Hence, we have proven that for any $$a,b \in \mathbb{R}$$ with $$b \neq 0$$ and $$\lambda$$ defined by $$\lambda \equiv a  + ib$$, then it follows that $$\lambda$$ is in the resolvent set of a self-adjoint $$A$$. This is then equivalent to the statement that if $$A$$ is self-adjoint, then the spectrum $$\sigma(A)$$ of $$A$$ is in $$\mathbb{R}$$.$$\blacksquare$$


> **Definition** *(Spectral Radius)*
<a name="def:spectral-radius"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{prpstn:hall-7.5} -->
> For any $$A \in \mathcal{B}(\mathbf{H})$$ the *spectral radius* $$R(A)$$ of $$A$$ is defined by
>
> $$
>     R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} |\lambda|.
> $$
>
> Note that as a result of [**Proposition**](#prpstn:hall-7.5), $$\sigma(A)$$ is a closed, bounded, and nonempty subset $$\mathbb{C}$$. Hence, $$R(A)$$ is a finite real number.

The first property that one can easily ascertain of the spectral radius is the following corollary:

> **Corollary**
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
    R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} |\lambda| \le \|A\|,
$$

the desired result.$$\blacksquare$$

The next "utility" proposition we will require details properties of the operator norm on $$\mathcal{B}(\mathbf{H})$$.

> **Proposition**
<a name="prpstn:hall-7.2"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-a.43} -->
<!--  \uses{lmm:lemma-1} -->
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

Now let us begin the proof of the second desired result $$\|A^*A\| = \|A\|^2$$ by proving that operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative,

$$
    \|AB\| \le \|A\| \, \|B\|
$$

for any $$A,B \in \mathcal{B}(\mathbf{H})$$.

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

the desired result, operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative.

Now as operator multiplication in $$\mathcal{B}(\mathbf{H})$$ is submultiplicative we have for an arbitrary $$A \in \mathcal{B}(\mathbf{H})$$

$$
    \|A^*A\| \le \|A^*\| \, \|A\| = \|A\|^2,
$$

where the equality uses the first result $$\|A^*\| = \|A\|$$ proved in this proposition.

However, using the alternative means of expressing the operator norm we derived in the first part of this proposition one has

$$
\begin{align}
    \|A^*A\| &= \sup\limits_{\|\phi\| = \|\psi\| = 1} \left| \left< \phi, A^*A\psi \right> \right| \\
             &= \sup\limits_{\|\phi\| = \|\psi\| = 1} \left| \left< A\phi, A\psi \right> \right| \\
             &\ge \sup\limits_{\|\psi\| = 1} \left| \left< A\psi, A\psi \right> \right| \\
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

> **Lemma**
<a name="lmm:hall-8.1"></a>
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

This first result was established in the proof of [**Proposition**](#prpstn:hall-7.5). There we established that for $$\lvert \lambda \rvert > \|A\|$$, the following series is convergent in the operator norm topology

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

This identity will be of use when we prove our series doesn't converge in the operator norm topology. In particular we will prove this using the [**Nth-Term Test**](#lmm:nth-term-test)

> **Lemma** *(Nth-Term Test)*
<a name="lmm:nth-term-test"></a>
> Let $$\{a_i\}_{i \in \mathbb{N}}$$ be a series in a normed vector space. If
>
> $$
>     \lim\limits_{i \rightarrow \infty} \| a_i \| \neq 0,
> $$
>
> then this series does not converge.

Consider the limit

$$
\begin{align}
    \lim\limits_{n \rightarrow \infty} \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\|
    &= \lim\limits_{n \rightarrow \infty} \left| \frac{1}{\lambda^{2^n + 1}} \right| \left\| A^{2^n} \right\| \\
    &= \lim\limits_{n \rightarrow \infty} \left| \frac{1}{\lambda^{2^n + 1}} \right| \left\| A \right\|^{2^n}  \\
    &= \lim\limits_{n \rightarrow \infty} \frac{1}{| \lambda |}  \left( \frac{\left\| A \right\|}{\left| \lambda \right|} \right)^{2^n} \\
    &= \frac{1}{| \lambda |} \lim\limits_{n \rightarrow \infty} \left( \frac{\left\| A \right\|}{\left| \lambda \right|} \right)^{2^n}.
\end{align}
$$

By hypothesis $$\lvert \lambda \rvert \le \|A\|$$. Hence

$$
    1 \le \frac{\left\| A \right\|}{\left| \lambda \right|}.
$$

This implies that our derivation continues as follows

$$
    \lim\limits_{n \rightarrow \infty} \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\|
    = \frac{1}{| \lambda |} \lim\limits_{n \rightarrow \infty} \left( \frac{\left\| A \right\|}{\left| \lambda \right|} \right)^{2^n}
    \neq 0.
$$

Hence, the [**Nth-Term Test**](#lmm:nth-term-test) implies that the series does not converge.

With that we have proven the desired result: if $$\lvert \lambda \rvert \le \|A\|$$, then our series doesn't converge in the operator norm topology.

Now let us (3) prove that if $$\lvert \lambda \rvert > R(A)$$, then this series converges in the operator norm topology.

Recall that in the proof of [**Proposition**](#prpstn:hall-7.5) we showed that if $$\lambda_0$$ is in the resolvent set of $$A$$ and $$\lambda \in \mathbb{C}$$ satisfies

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

can be expressed as a locally convergent power series with coefficients in $$\mathbb{C}$$. Hence, it is an analytic function on the resolvent set of $$A$$, which as shown in the proof of [**Proposition**](#prpstn:hall-7.5) is open. Hence, the [**Analytic Equivalence Theorem**](#thrm:analytic-equivalence-theorem) implies that this function is holomorphic on the resolvent set of $$A$$.

Now, as mentioned in [**Definition** *(Spectral Radius)*](#def:spectral-radius), the spectral radius

$$
    R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} \lvert \lambda \rvert
$$

of $$A$$ is a finite real number. Explicitly, [**Proposition**](#prpstn:hall-7.5) implies that $$\sigma(A)$$ is a closed, bounded, and nonempty subset $$\mathbb{C}$$. Hence, $$R(A)$$ is a finite real number.

The spectrum $$\sigma(A)$$ of $$A$$ is defined as the complement of the resolvent set of $$A$$ in $$\mathbb{C}$$. Hence, all $$\lambda \in \mathbb{C}$$ such that $$\lvert \lambda \rvert > R(A)$$ are in the resolvent set of $$A$$. Thus, the function

$$
    \lambda \longmapsto \xi (A - \lambda \mathbf{1})^{-1}
$$

is holomorphic on the (unbounded) open annulus $$R(A) < \lvert \lambda \rvert$$.

Now recall that [**Laurent's Theorem**](#thrm:laurents-theorem) states

> **Theorem** *(Laurent's Theorem)*
<a name="thrm:laurents-theorem"></a>
> Any function holomorphic on an open annulus in $$\mathbb{C}$$ can be expanded uniquely as a Laurent series on that open annulus.

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

The unique Laurent series from Part 3 converges. This implies that all of its summands are bounded. In other words, for each $$\xi$$ in the dual space of $$\mathcal{B}(\mathbf{H})$$ there exists a $$C_\xi \in \mathbb{R}$$ such that for any natural number $$m$$

$$
    \left| \frac{\xi A^m}{\lambda^{m + 1}} \right| < C_\xi
$$

for all complex $$\lambda$$ that satisfy $$R(A) < \lvert \lambda \rvert$$.

Now, as we established in [**Lemma** *(Bounded Operators form a Banach Space)*](#lmm:bounded-operators-form-a-banach-space), $$\mathcal{B}(\mathbf{H})$$ forms a Banach space under the operator norm. Recalling the [**Theorem on Completeness of the Dual**](#thrm:theorem-on-completeness-of-the-dual)

> **Theorem** *(Theorem on Completeness of the Dual)*
<a name="thrm:theorem-on-completeness-of-the-dual"></a>
> If $$V$$ is a Banach space, then its dual $$V^*$$ is also a Banach space.

we can conclude that the dual $$\mathcal{B}(\mathbf{H})^*$$ of $$\mathcal{B}(\mathbf{H})$$ is also a Banach space.

As both $$\mathcal{B}(\mathbf{H})$$ and $$\mathcal{B}(\mathbf{H})^*$$ are Banach spaces and we have a set of bounded summands we can apply the [**Principle of Uniform Boundedness**](#thrm:hall-a.40)

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

by identifying $$V_1$$ with $$\mathcal{B}(\mathbf{H})^*$$, $$V_2$$ with $$\mathbb{C}$$, the operators $$\{ T_m \}$$ with the operators

$$
    \left\{ \frac{A^m}{\lambda^{m + 1}} \right\},
$$

and the bounds we derived previously

$$
    \left| \frac{\xi A^m}{\lambda^{m + 1}} \right| < C_\xi
$$

with those in this theorem. Doing so we find that there exists a real number $$C$$ such that for all natural numbers $$m$$

$$
    \left\| \frac{A^m}{\lambda^{m + 1}} \right\| \le C
$$

for all complex $$\lambda$$ that satisfy $$R(A) < \lvert \lambda \rvert$$, where here the operator norm is used.

Now, as one will recall, in Part 2 of this proof we established that for any natural number $$n$$

$$
    \left\| A^{2^n} \right\| = \left\| A \right\|^{2^n}.
$$

This implies of the bound we just derived

$$
    \left\| \frac{A^{2^n}}{\lambda^{2^n + 1}} \right\| = \frac{\left\| A^{2^n} \right\|}{\left| \lambda \right|^{2^n + 1}} = \frac{\left\| A \right\|^{2^n} }{\left| \lambda \right|^{2^n + 1}} \le C
$$

for all complex $$\lambda$$ that satisfy $$R(A) < \lvert \lambda \rvert$$.

Recall we already established in [**Corollary**](#crllr:crllr-1) that $$R(A) \le \|A\|$$. We will now establish that $$R(A) = \|A\|$$ using proof by contradiction.

Let us for the moment assume that $$R(A) < \|A\|$$, then it is possible to select a $$\lambda$$ such that $$R(A) < \lvert \lambda \rvert < \|A\|$$. This implies that

$$
    1 < \frac{\|A\|}{\lvert \lambda \rvert}.
$$

Hence, it is possible to select an $$n$$ large enough to violate the above inequality

$$
    \frac{1}{\left| \lambda \right|} \left( \frac{\left\| A \right\|}{\left| \lambda \right|} \right)^{2^n} = \frac{\left\| A \right\|^{2^n} }{\left| \lambda \right|^{2^n + 1}} \le C.
$$

So it can not be the case that  $$R(A) < \|A\|$$. As we know $$R(A) \le \|A\|$$, the only option left is $$R(A) = \|A\|$$, the desired result.$$\blacksquare$$

The next step in this **Stage 1: The Continuous Functional Calculus** is to understand how the spectrum $$\sigma(A)$$ of an operator $$A \in \mathcal{B}(\mathbf{H})$$ is related to the spectrum $$\sigma(p(A))$$ of a polynomial $$p(A)$$ in $$A$$. The relation between $$\sigma(A)$$ and $$\sigma(p(A))$$ is "straightforward" and described by the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem).

However, to prove the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) we will first have to prove this utility lemma

> **Lemma**
<a name="lmm:hall-ex-8.3.1"></a>
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

This is simply the statement that $$A$$ has a right inverse $$A_r$$ defined by

$$
    (A_r)^{-1} = (B(AB)^{-1}).
$$

Similarly, under the assumption that $$(AB)$$ has an inverse,$$(AB)^{-1}$$ exists and satisfies

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

This is simply the statement that $$A$$ has a left inverse $$A_l$$ defined by

$$
    (A_l)^{-1} = ((AB)^{-1}B).
$$

Now if we let $$(A_r)^{-1}$$ act on the right of $$(A_l)^{-1}A = \mathbf{1}$$, we have

$$
    (A_l)^{-1}A(A_r)^{-1} = (A_r)^{-1}.
$$

However, $$(A_r)^{-1}$$ is the right inverse of $$A$$; so

$$
    A(A_r)^{-1} = \mathbf{1}.
$$

The last two equations then imply

$$
    (A_l)^{-1} = (A_r)^{-1}.
$$

In other words there is a single unique inverse

$$
    A^{-1} = (A_l)^{-1} = (A_r)^{-1}
$$

of $$A$$.

However, by hypothesis $$A$$ is not invertible. Thus our assumption that $$AB$$ is invertible is false, and  $$AB$$ is not invertible. This is the desired result.$$\blacksquare$$

With this lemma complete we may now move on to the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem).

> **Lemma** *(Spectral Mapping Theorem)*
<a name="lmm:spectral-mapping-theorem"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:hall-ex-8.3.1} -->
<!--  \uses{thrm:fundamental-theorem-of-algebra} -->
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
Before getting into the details, let us present an outline of the 4 step proof.

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

The resolvent set of $$p(A) = \alpha_0 \mathbf{1}$$ is defined as the set of $$\lambda \in \mathbb{C}$$ such that $$\alpha_0 \mathbf{1} - \lambda \mathbf{1}$$ has a bounded inverse in $$\mathcal{B}(\mathbf{H})$$. Obviously the resolvent set of $$p(A)$$ in this case is $$(\mathbb{C} - \alpha_0)$$, the set of all elements in $$\mathbb{C}$$ not equal to $$\alpha_0$$. The spectrum $$\sigma(p(A))$$ of $$p(A)$$ is defined as the complement of the resolvent set of $$p(A)$$ in $$\mathbb{C}$$. Hence, $$\sigma(p(A)) = \{ \alpha_0 \}$$.

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

Now as $$\lambda$$ is in $$\sigma(A)$$, by definition $$(A - \lambda \mathbf{1})$$ is not invertible in $$\mathcal{B}(\mathbf{H})$$. Furthermore, by construction $$(A - \lambda \mathbf{1})$$ commutes with $$q(A)$$. Hence, as a result of [**Lemma**](#lmm:hall-ex-8.3.1) the left hand side $$(A - \lambda \mathbf{1}) q(A)$$ of the previous equation isn't invertible. Hence, $$p(A) - p(\lambda) \mathbf{1}$$ isn't invertible, and thus $$p(\lambda)$$ is an element of the spectrum $$\sigma(p(A))$$ of $$p(A)$$.  In other words

$$
    \{ p(\lambda) : \lambda \in \sigma(A) \} \subseteq \sigma(p(A)),
$$

the second desired result.

Next let us (3) prove that

$$
    \sigma(p(A)) \subseteq \{ p(\lambda) : \lambda \in \sigma(A) \}
$$

for a generic polynomial $$p$$ of positive degree.

Consider an arbitrary $$\gamma$$ in the spectrum $$\sigma(p(A))$$ of $$p(A)$$. As a result of the [**Fundamental Theorem of Algebra**](#thrm:fundamental-theorem-of-algebra)

> **Theorem** *(Fundamental Theorem of Algebra)*
<a name="thrm:fundamental-theorem-of-algebra"></a>
> The field of complex numbers is algebraically closed.

we can factor the polynomial $$p(z) - \gamma$$ as a function of $$z$$ as follows

$$
    p(z) - \gamma = c (z - b_1)(z - b_2)\cdots(z - b_m),
$$

where $$c, b_i\in \mathbb{C}$$. Thus, as $$A$$ commutes with itself and $$\mathbf{1}$$, we also have

$$
    p(A) - \gamma \mathbf{1} = c (A - b_1 \mathbf{1} )(A - b_2 \mathbf{1} )\cdots(A - b_m \mathbf{1} ).
$$

Now as $$\gamma \in \sigma(p(A))$$ it follows that $$p(A) - \gamma \mathbf{1}$$ is not invertible. Thus there must exist some $$j$$ such that $$(A - b_j \mathbf{1})$$ is not invertible. If no such $$j$$ existed, then all the terms on the right hand side of this equation would be invertible which would imply that $$p(A) - \gamma \mathbf{1}$$ is invertible, which we already know is not the case.

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

The last step in **Stage 1: The Continuous Functional Calculus** is to generalize the map of the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem)

$$
    p \longmapsto p(A),
$$

taking complex-valued polynomials on $$\sigma(A)$$ to elements of $$\mathcal{B}(\mathbf{H})$$, to take real-valued, continuous functions $$f$$ on $$\sigma(A)$$ to elements $$f(A)$$ of $$\mathcal{B}(\mathbf{H})$$.

We will do so using the [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass) to prove that the set of polynomials on $$\sigma(A)$$ is dense in $$C^0(\sigma(A); \mathbb{R})$$---the space of continuous, real-valued functions on $$\sigma(A)$$. Then we will use this fact along with the [**Bounded Linear Transform Theorem**](#thrm:bounded-linear-transformation-theorem) to extend the [**Spectral Mapping Theorem**](#lmm:spectral-mapping-theorem) map $$ p \mapsto p(A)$$ to all of $$C^0(\sigma(A); \mathbb{R})$$

$$
    f \longmapsto f(A).
$$

Let's get started.

> **Proposition**
<a name="prpstn:hall-8.3"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{thrm:stone–weierstrass} -->
<!--  \uses{thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:spectral-mapping-theorem} -->
<!--  \uses{lmm:hall-8.1} -->
<!--  \uses{def:spectral-radius} -->
<!--  \uses{thrm:heine–borel-theorem} -->
<!--  \uses{def:separates-points} -->
<!--  \uses{thrm:boundedness-theorem} -->
<!--  \uses{lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{prpstn:hall-7.5} -->
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

with $$\mathbb{R}$$ valued coefficients $$c_i$$. If $$A$$ is self-adjoint, then $$p(A)$$ is also self-adjoint. Explicitly,

$$
\begin{align}
    p(A)^* &= \left( c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_{m - 1} A^{m - 1} + c_m A^m \right)^* \\
           &= (c_0 \mathbf{1})^* + (c_1 A)^* + (c_2 A^2)^* + \cdots + (c_{m - 1} A^{m - 1})^* + (c_m A^m)^* \\
           &= c_0^* \mathbf{1}^* + c_1^* A^* + c_2^* (A^2)^* + \cdots + c_{m - 1}^* (A^{m - 1})^* + c_m^* (A^m)^* \\
           &= c_0 \mathbf{1} + c_1 A + c_2 A^2 + \cdots + c_{m - 1} A^{m - 1} + c_m A^m \\
           &= p(A),
\end{align}
$$

where we employed the fact that $$A$$ is self-adjoint, the definition of the involution $$B \mapsto B^*$$, and the fact that the $$c_i$$ are real-valued.

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
    R(p(A)) = \sup\limits_{\gamma \in \sigma(p(A))} |\gamma|.
$$

Putting this all together we conclude that

$$
\begin{align}
    \|p(A)\| &= R(p(A)) \\
             &= \sup\limits_{\gamma \in \sigma(p(A))} |\gamma| \\
             &= \sup\limits_{\lambda \in \sigma(A)} | p(\lambda) |.
\end{align}
$$

Proving that

$$
    \|p(A)\| = \sup\limits_{\lambda \in \sigma(A)} | p(\lambda) |,
$$

which is simply the statement that the map $$p \mapsto p(A)$$ is isometric.

Explicitly, the map $$p \mapsto p(A)$$ from the set of real-valued polynomials on $$\sigma(A)$$ equipped with the supremum norm into $$\mathcal{B}(\mathbf{H})$$ equipped with the operator norm, is isometric. This map is also linear; for real-valued polynomials $$p$$ and $$q$$ we have $$(p + q) \mapsto (p + q)(A) = p(A) + q(A)$$.

Now in preparation for the application of the [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass) let us examine explicitly some of the properties of the objects we are currently considering.

As one will recall, [**Proposition**](#prpstn:hall-7.5) established that the spectrum $$\sigma(A)$$ of $$A$$ is a closed and bounded subset of $$\mathbb{C}$$. The [**Heine–Borel Theorem**](#thrm:heine–borel-theorem)

> **Theorem** *(Heine–Borel Theorem)*
<a name="thrm:heine–borel-theorem"></a>
> For any positive, natural number $$n$$, any subset of $$\mathbb{C}^n$$ is compact if and only if it is closed and bounded.

then implies that $$\sigma(A)$$ is compact. Furthermore, as the norm $$\lvert \cdot \rvert$$ on $$\mathbb{C}$$ defines a metric

$$
  d(z_1, z_2) \equiv \lvert z_1 - z_2 \rvert
$$ 

on $$\mathbb{C}$$, the subset $$\sigma(A)$$ of $$\mathbb{C}$$ is a metric space by way of this inherited metric. Thus, $$\sigma(A)$$ is a compact metric space.

In addition, any element $$p$$ in the algebra of real-valued polynomials on $$\sigma(A)$$ is continuous. Hence, the algebra of real-valued polynomials on $$\sigma(A)$$ is an algebra in $$C^0(\sigma(A); \mathbb{R})$$, the space of continuous, real-valued functions on $$\sigma(A)$$.

Obviously the algebra of real-valued polynomials on $$\sigma(A)$$ contains the constant functions

$$
    p(\lambda) = c_0.
$$

In addition this algebra [separates-points](#def:separates-points)

> **Definition** *(Separates Points)*
<a name="def:separates-points"></a>
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. The algebra $$\mathcal{A}$$ is said to *separate points* if for any $$x,y \in X$$ such that $$x \neq y$$ there exists a $$f \in \mathcal{A}$$ such that $$f(x) \neq f(y)$$.

Explicitly, let $$x$$ and $$y$$ be any elements in $$\sigma(A)$$ such that $$x \neq y$$. Note that [**Proposition**](#prpstn:hall-7.7) along with the hypothesis that $$A$$ is self-adjoint, imply that $$x,y \in \sigma(A) \subset \mathbb{R}$$. Hence, the polynomial

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

where the final $$\neq$$ follows from the fact that $$x \neq y$$. Hence, the real-valued polynomials on $$\sigma(A)$$ separates-points.

With all of this in-hand we can apply the [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass)

> **Theorem** *(Stone–Weierstrass)*
<a name="thrm:stone–weierstrass"></a>
<!--  \uses{def:separates-points} -->
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. If $$\mathcal{A}$$ contains the constant functions and separates points, then $$\mathcal{A}$$ is dense in $$C^0(X; \mathbb{R})$$ with respect to the supremum norm.

to the current situation. Identifying $$X$$ with $$\sigma(A)$$ and $$\mathcal{A}$$ with the real-valued polynomials on $$\sigma(A)$$, the [**Stone–Weierstrass Theorem**](#thrm:stone–weierstrass) allows us to conclude that real-valued polynomials on $$\sigma(A)$$ are dense in $$C^0(\sigma(A); \mathbb{R})$$.

Next we must prepare for the application of the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem). To do so, we must establish some relatively straightforward properties of objects we are currently considering. 

Consider $$C^0(\sigma(A); \mathbb{R})$$, the space of continuous, real-valued functions on $$\sigma(A)$$. As $$\sigma(A)$$ is compact the [**Boundedness Theorem**](#thrm:boundedness-theorem)

> **Theorem** *(Boundedness Theorem)*
<a name="thrm:boundedness-theorem"></a>
> A continuous real-valued function on a compact subset $$C$$ of $$\mathbf{R}$$ is bounded on $$C$$.

implies that any element of $$C^0(\sigma(A); \mathbb{R})$$ is bounded. Hence, the supremum norm

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

With all of this in hand we can apply the [**Bounded Linear Transformation Theorem**](#thrm:bounded-linear-transformation-theorem) 

> **Theorem** *(Bounded Linear Transformation Theorem)*
<a name="thrm:bounded-linear-transformation-theorem"></a>
> Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.

to the current situation. Identifying $$V_1$$ with $$C^0(\sigma(A); \mathbb{R})$$, $$V_2$$ with $$\mathcal{B}(\mathbf{H})$$, $$W$$ the real-valued polynomials on $$\sigma(A)$$, and $$T$$ with our map $$p \mapsto p(A)$$ allows us to conclude that there exists a unique, bounded, linear map

$$
    f \longmapsto f(A)
$$

from $$C^0(\sigma(A); \mathbb{R})$$ to $$\mathcal{B}(\mathbf{H})$$ that when restricted to real-valued polynomials agrees with our map $$p \mapsto p(A)$$ and that has the same norm of our map $$p \mapsto p(A)$$.

This map $$f \mapsto f(A)$$ is the desired result of this proposition and is known as the *(real-valued) functional calculus* for $$A$$.$$\blacksquare$$

As a final step in **Stage 1: The Continuous Functional Calculus**, we will derive some basic properties of the (real-valued) functional calculus of a self-adjoint operator $$A$$ in $$\mathcal{B}(\mathbf{H})$$. These properties require the following definition

> **Definition** *(Non-Negative (Bounded) Operator)*
<a name="def:non-negative-operator"></a>
> <!--  \uses{def:bounded-operator-notation} -->
> An operator $$A \in \mathcal{B}(\mathbf{H})$$ is called a *non-negative (bounded) operator* if
> 
> $$
>     0 \le \left< \psi, A\psi \right>
> $$
> 
> for all $$\psi \in \mathbf{H}$$.

and are captured in the following proposition

> **Proposition**
<a name="prpstn:hall-8.4"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{prpstn:hall-8.3} -->
<!--  \uses{def:non-negative-operator} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
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
> 3. **Non-negativity:** For any $$f \in C^0(\sigma(A); \mathbb{R})$$ such that $$f$$ is non-negative, $$f(A)$$ is a non-negative (bounded) operator.
> 4. **Norm and spectrum properties:** For any $$f \in C^0(\sigma(A); \mathbb{R})$$, we have
> 
>    $$
>        \|f(A)\| = \sup\limits_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert,
>    $$
> 
>    where $$\|f(A)\|$$ is the operator norm of $$f(A)$$ and $$\sigma(A)$$ is the specturm of $$A$$, and
> 
>    $$
>        \sigma(f(A)) = \{ f(\lambda) : \lambda \in \sigma(A) \},
>    $$
> 
>    where $$\sigma(f(A))$$ is the spectrum of $$f(A)$$.




**Stage 2: An Operator-Valued Riesz Representation Theorem**

> **Theorem** *(Riesz Representation)*
<a name="thrm:riesz-representation"></a>
> Let $$X$$ be a compact metric space and let $$C^0(X; \mathbb{R})$$ be the space of continuous, real-valued functions on $$X$$. Suppose $$\Lambda : C^0(X; \mathbb{R}) \rightarrow \mathbb{R}$$ is a linear function with the property that $$\Lambda(f)$$ is non-negative whenever all the values of $$f$$ are non-negative. Then there exists a unique, real-valued, positive measure $$\mu$$ on the Borel $$\sigma$$-algebra of $$X$$ for which
>
> $$
>     \Lambda(f) = \int_X f \, d\mu
> $$
>
> for all $$f \in C^0(X; \mathbb{R})$$.
