---
title:  "Spectral Theorems"
date:   2026-07-06 07:43:42 +0200
categories: functional-analysis
---

Here we will state and prove two versions of the Spectral Theorem, one for bounded, self-adjoint operators and a second for unbounded, self-adjoint operators. Both sit at the core of much of AQFT. Extensive use of both will be made in subsequent work. 

Here, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

# Spectral Theorem: Bounded Self-Adjoint Operators
In this section we will state and prove the Spectral Theorem for bounded, self-adjoint operators. However, we must introduce "extensive machinary" before we are able to state and prove the theorem. To that end we begin by examining some properties of bounded operators.

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

As $$\epsilon$$ independent of $$\psi$$, this limit holds uniformly for all $$\psi \in \mathbf{H}$$ that satisfy $$\|\psi\| = 1$$. Thus we can take the supremum over such $$\psi$$ to obtain

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
In this section we will actually be able to state the Spectral Theorem. However, we will only be able to do so after introducing "substantial machinary" related to "projection-valued measures".

### Projection-Valued Measures
"Projection-valued measures" are "core" to the Spectral Theorem. Basically, they generalize the notion of a measure. A "projection-valued measure", instead of taking on positive, real-values as a standard measure does, takes on "bounded orthogonal projection" values. Formally, we define this by first introducing the notion of a "bounded orthogonal projection"

> **Definition** *(Resolvent and Spectrum)*
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
> 3. If $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$ are disjoint, then for all $$v \in \mathbf{H}$$, we have
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
* **Countable additivity** - For disjoint $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$ 

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

Finally let us prove countable additivity. Let $$E_1$$, $$E_2$$, $$E_3$$... in $$\Omega(X)$$ be disjoint. The definition of $$\mu_\psi$$ along with the definition of the projection-valued measure $$\mu$$ imply

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
>    where $$\| \cdot \|$$ is the Hilbert space norm on $$\mathbf{H}$$ and $$\mid \cdot \mid$$ is the norm on $$\mathbb{C}$$.
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

**Proof**
By hypothesis we have a projection-valued measure $$\mu$$. Consider any bounded, measurable, complex-valed function $$f$$ on $$X$$ and any $$\psi \in \mathbf{H}$$. With this, let us define a map $$Q_f : \mathbf{H} \rightarrow \mathbb{C}$$ by

$$
    Q_f(\psi) \equiv \int_X f \, d\mu_\psi,
$$

where $$\mu_\psi$$ is the positive real-valued measure of [**Theorem** *(Projection-Valued Measure’s Associated Measure)*](#thrm:projection-valued-measures-associated-measure). It turns out that such a $$Q_f(\psi)$$ is a bounded quadratic form which we now prove

> **Lemma**
<a name="lmm:lemma1-of-operator-valued-integration"></a>
<!--  \uses{def:projection-valued-measure} -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{thrm:projection-valued-measures-associated-measure} -->
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

where $$\alpha_i \in \mathbb{C}$$ and $$E_i \in \Omega(X)$$ are disjoint, also results in a bounded quadratic form $$Q_s$$.

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

Consider an arbitrary $$\phi \in \mathbf{H}$$ such that $$\|\phi\| \neq 0$$. As $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$ we have

$$
\begin{align}
    \frac{Q_f(\phi)}{\|\phi\|^2} &= \frac{1}{\|\phi\|^2} \int_X f d\mu_\phi \\
                                 &= \frac{1}{\|\phi\|^2} \int_X \lim\limits_{i \rightarrow \infty} s_i \, d\mu_\phi \\
                                 &= \frac{1}{\|\phi\|^2} \lim\limits_{i \rightarrow \infty} \int_X s_i \, d\mu_\phi \\
                                 &= \frac{1}{\|\phi\|^2} \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi) \\
                                 &= \lim\limits_{i \rightarrow \infty} \frac{Q_{s_i}(\phi)}{\|\phi\|^2},
\end{align}
$$

were we can pull the limit out of the integral as $$\{s_i\}_{i \in \mathbb{N}}$$ converges uniformly to $$f$$. Hence, we proved that

$$
    \frac{Q_f(\phi)}{\|\phi\|^2} = \lim\limits_{i \rightarrow \infty} \frac{Q_{s_i}(\phi)}{\|\phi\|^2}
$$

for all non-zero $$\phi \in \mathbf{H}$$.

Hence, for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i \ge N$$ one has

$$
    \left| \frac{Q_f(\phi)}{\|\phi\|^2} - \frac{Q_{s_i}(\phi)}{\|\phi\|^2} \right| < \frac{\epsilon}{2}
$$

for all non-zero $$\phi \in \mathbf{H}$$. Thus, for this same $$\epsilon > 0$$ and $$N$$ and for all $$i,j \ge N$$ and non-zero $$\phi \in \mathbf{H}$$ one has

$$
\begin{align}
    \left| \frac{Q_{s_i}(\phi)}{\|\phi\|^2} - \frac{Q_{s_j}(\phi)}{\|\phi\|^2} \right|
        &= \left| \left(\frac{Q_f(\phi)}{\|\phi\|^2} - \frac{Q_{s_j}(\phi)}{\|\phi\|^2} \right) - \left(\frac{Q_f(\phi)}{\|\phi\|^2} - \frac{Q_{s_i}(\phi)}{\|\phi\|^2} \right) \right| \\
        &\le \left| \frac{Q_f(\phi)}{\|\phi\|^2} - \frac{Q_{s_j}(\phi)}{\|\phi\|^2} \right| + \left| \frac{Q_f(\phi)}{\|\phi\|^2} - \frac{Q_{s_i}(\phi)}{\|\phi\|^2} \right| \\
        &< \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
        &= \epsilon,
\end{align}
$$

where we had used the definition of a norm in the second line and our previous result in the third line.

So we have proven that for any $$\epsilon > 0$$ there exists a natural number $$N$$ such that for all $$i,j \ge N$$ 

$$
     \left| \frac{Q_{s_i}(\phi)}{\|\phi\|^2} - \frac{Q_{s_j}(\phi)}{\|\phi\|^2} \right| < \epsilon
$$

for all non-zero $$\phi \in \mathbf{H}$$.

That being the case consider $$\epsilon = 1$$. Thus, there exists a natural number $$N_1$$ such that for all $$i_1,j_1 \ge N_1$$ one has

$$
     \left| \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} - \frac{Q_{s_{j_1}}(\phi)}{\|\phi\|^2} \right| < 1
$$

for all non-zero $$\phi \in \mathbf{H}$$. In particular one may set $$j_1 = N_1$$ to obtain

$$
     \left| \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} - \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right| < 1
$$

for all non-zero $$\phi \in \mathbf{H}$$. Hence, the definition of a norm along with this result implies

$$
\begin{align}
    \left| \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} \right|
        &= \left| \left( \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} - \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right) + \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right| \\
        &\le \left| \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} - \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right| + \left| \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right| \\
        &< 1 + \left| \frac{Q_{s_{N_1}}(\phi)}{\|\phi\|^2} \right| \\
        &\le 1 + C_{N_1},
\end{align}
$$

where in the final step we employed our simple function result

$$
    \left| Q_{s_{N_1}}(\phi) \right| \le C_{N_1} \|\phi\|^2.
$$

So in summary we have shown that for $$i_1 \ge N_1$$ one has

$$
    \left| \frac{Q_{s_{i_1}}(\phi)}{\|\phi\|^2} \right| < 1 + C_{N_1},
$$

which implies

$$
    \left| Q_{s_{i_1}}(\phi) \right| < \left( 1 + C_{N_1} \right) \|\phi\|^2,
$$

for all non-zero $$\phi \in \mathbf{H}$$.

Now as $$N_1$$ is just some finite natural number, we have a finite set of natural numbers $$\{1,2,\ldots,(N_1 - 1)\}$$. And as a result of our simple function result, for any $$j \in \{1,2,\ldots, (N_1 - 1)\}$$ we have

$$
    \left| Q_{s_j}(\phi) \right| \le C_j \|\phi\|^2.
$$

So if we define $$C$$ by

$$
    C \equiv \max \{C_1, C_1,\ldots, C_{(N_1 - 1)}, (1 + C_{N_1}) \},
$$

then for $$j < N_1$$ we have

$$
    \left| Q_{s_j}(\phi) \right| \le C \|\phi\|^2
$$

and for $$i \ge N_1$$ we have

$$
    \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2.
$$

So, for for any natural number $$i$$ we have proven that

$$
    \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2
$$

for all non-zero $$\phi \in \mathbf{H}$$. This result also is true for $$\phi = 0$$.

Explicitly, for $$\phi = 0$$, the associated measure $$\mu_\phi$$ assigns zero measure to all $$E \in \Omega(X)$$ as

$$
    \mu_0(E) = \left< 0, \mu(E) 0 \right> = 0.
$$

Hence, $$Q_{s_i}(0) = 0$$ and thus for $$\phi = 0$$ the inequality 

$$
    \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2
$$

reduces to $$\mid 0 \mid \le 0$$, which is trivially true.

So we have proven that for any natural number $$i$$

$$
    \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$.

Now consider taking the $$i \rightarrow \infty$$ limit of

$$
    \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2.
$$

As $$i$$ does not appear on the right-hand side of this inequality, one has

$$
    \lim\limits_{i \rightarrow \infty} \left| Q_{s_i}(\phi) \right| \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$. As we have previously proven that

$$
    Q_f(\phi) = \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi),
$$

we can pull the limit through $$\mid \cdot \mid$$ to obtain

$$
    \lim\limits_{i \rightarrow \infty} \left| Q_{s_i}(\phi) \right| = \left| \lim\limits_{i \rightarrow \infty} Q_{s_i}(\phi) \right| = \left| Q_f(\phi) \right| \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$. So we have proven that

$$
    \left| Q_f(\phi) \right| \le C \|\phi\|^2
$$

for all $$\phi \in \mathbf{H}$$, the desired result.

This concludes our proof that for any bounded, measurable, complex-valued function $$f$$ on the set $$X$$ with $$\sigma$$-algebra $$\Omega(X)$$ the map $$Q_f$$ is a bounded quadratic form. $$\blacksquare$$

Our next step in the larger proof is establishing some propositions we will have need of later in our argument. To wit let us first prove the proposition (Proposition A.61 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Proposition**
> <a name="prpstn:hall-a.61"></a>
> <!--  \uses{def:bounded-quadratic-form} -->
> <!--  \uses{def:bounded-sesquilinear-form} -->
> <!--  \uses{def:bounded-operator-notation} -->
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
    &=   C \frac{1}{2} \left[ \|\phi + \psi\|^2 + \|\phi\|^2 + \|\psi\|^2 + \|\phi + i\psi\|^2 + \|\phi\|^2 + |i| \, \|\psi\|^2 \right] \\
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
    \left|L(\phi, \psi)\right| \le 6C \|\phi\| \, \|\psi\|
$$

that $$L$$ is bounded.

Finally, we will prove that if $$Q(\psi)$$ is valued in $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$, then $$L$$ is conjugate symmetric.

In this case, by hypothesis $$Q(\psi)$$ is valued in $$\mathbb{R}$$ for all $$\psi \in \mathbf{H}$$.
