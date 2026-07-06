---
title:  "Spectral Theorems"
date:   2026-07-06 07:43:42 +0200
categories: functional-analysis
---

Here we will state and prove two versions of the Spectral Theorem, one for bounded, self-adjoint operators and a second for unbounded, self-adjoint operators. Both sit at the core of much of AQFT. Extensive use of both will be made in subsequent work.

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
> for all $$f$$ and $$\psi \in \mathbf{H}$$, where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure’s Associated Measure)*](#thrm:projection-valued-measures-associated-measure) $$\left< \cdot, \cdot \right>$$ is the Hilbert space inner product on $$\mathbf{H}$$. This unique linear map has the following additional properties
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

Finally we must prove that it $$Q(\psi)$$ belongs to $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then the operator $$A$$ is self-adjoint.

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

Now using the definition of a norm and applying Cauchy–Schwarz twice, first to each summand and then across the sum (viewing $$\|\mu(E_i) \phi\|$$ and $$\|\mu(E_i) \psi\|$$ as vectors in $$\mathbb{R}^n$$), one obtains

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

in other words operator-valued integral of $$s_i$$ converges to the operator-valued integral of $$f$$. One can establish using similar logic that the operator-valued integral of $$r_i$$ converges to the operator-valued integral of $$g$$.

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

> **Theorem** *(Spectral Theorem for Bounded Operators)*
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
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint and $$f : \sigma(A) \rightarrow \mathbb{C}$$ is a bounded measurable function on the the spectrum $$\sigma(A)$$ of $$A$$, *functional calculus* defines an operator $$f(A)$$ by
>
> $$
>     f(A) \equiv \int_{\sigma(A)} f(\lambda) \, d\mu^A(\lambda),
> $$
>
> where $$\mu^A$$ is the unique projection-valued measure of [**Theorem** *(Spectral Theorem for Bounded Operators)*](#thrm:spectral-theorem-for-bounded-operators) associated to $$A$$.

With functional calculus defined, we can now outline the proof of [**Theorem** *(Spectral Theorem for Bounded Operators)*](#thrm:spectral-theorem-for-bounded-operators). This proof consists of two main stages.

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
> Suppose $$X \in \mathcal{B}(\mathbf{H})$$ satisfies $$\|X\| < 1$$, where $$\|X\|$$ is the operator norm of $$X$$. Then the operator $$I - X$$ has a bounded inverse $$(I - X)^{-1}$$ in $$\mathcal{B}(\mathbf{H})$$; and this bounded inverse given by the following series
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
> For all $$A \in \mathcal{B}(\mathbf{H})$$, the following results hold.
>
> 1. The spectrum $$\sigma(A)$$ of $$A$$ is a closed, bounded, and nonempty subset of $$\mathbb{C}$$.
> 2. If $$\lvert \lambda \rvert > \|A\|$$, where $$\|A\|$$ is the operator norm of $$A$$, then $$\lambda$$ is in the resolvent set of $$A$$.

**Proof**
TODO!

> **Proposition**
<a name="prpstn:hall-7.7"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then the spectrum $$\sigma(A)$$ of $$A$$ is contained in $$\mathbb{R}$$.

**Proof**
TODO!


> **Definition** *(Spectral Radius)*
<a name="def:spectral-radius"></a>
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{prpstn:hall-7.5} -->
<!--  \uses{prpstn:hall-7.7} -->
> For any $$A \in \mathcal{B}(\mathbf{H})$$ the *spectral radius* $$R(A)$$ of $$A$$ is defined by
>
> $$
>     R(A) \equiv \sup\limits_{\lambda \in \sigma(A)} |\lambda|.
> $$
>
> As a result of the proved previously [**Proposition**](#prpstn:hall-7.5) and [**Proposition**](#prpstn:hall-7.7), $$\sigma(A)$$ is a nonempty, bounded subset of $$\mathbb{R}$$. Hence, $$R(A)$$ is well-defined.






> **Definition** *(Separates Points)*
<a name="def:separates-points"></a>
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. The algebra $$\mathcal{A}$$ is said to *separate points* if for any $$x,y \in X$$ such that $$x \neq y$$ there exists a $$f \in \mathcal{A}$$ such that $$f(x) \neq f(y)$$.

> **Theorem** *(Stone–Weierstrass)*
<a name="thrm:stone–weierstrass"></a>
<!--  \uses{def:separates-points} -->
> Let $$X$$ be a compact metric space and let $$\mathcal{A}$$ be an algebra in $$C^0(X; \mathbb{R})$$, the space of continuous, real-valued functions on $$X$$. If $$\mathcal{A}$$ contains the constant functions and separates points, then $$\mathcal{A}$$ is dense in $$C^0(X; \mathbb{R})$$ with respect to the supremum norm.

#### Stage 2: An Operator-Valued Riesz Representation Theorem

> **Theorem** *(Riesz Representation)*
<a name="thrm:riesz-representation"></a>
> Let $$X$$ be a compact metric space and let $$C^0(X; \mathbb{R})$$ be the space of continuous, real-valued functions on $$X$$. Suppose $$\Lambda : C^0(X; \mathbb{R}) \rightarrow \mathbb{R}$$ is a linear function with the property that $$\Lambda(f)$$ is non-negative whenever all the values of $$f$$ are non-negative. Then there exists a unique, real-valued, positive measure $$\mu$$ on the Borel $$\sigma$$-algebra of $$X$$ for which
>
> $$
>     \Lambda(f) = \int_X f \, d\mu
> $$
>
> for all $$f \in C^0(X; \mathbb{R})$$.
