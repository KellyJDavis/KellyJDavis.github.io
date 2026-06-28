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
<!--  \label{def:bounded-operator-notation} -->
> We notate the set of operators on a separable, complex Hilbert space $$\mathbf{H}$$ that are bounded with respect to the operator norm as $$\mathcal{B}(\mathbf{H})$$.

along with an "elementary" lemma that proves $$\mathcal{B}(\mathbf{H})$$ is a Banach space

> **Lemma** *(Bounded Operators form a Banach Space)*
<!--  \label{lmm:bounded-operators-form-a-banach-space} -->
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
<!--  \label{def:bounded-inverse} -->
<!--  \uses{def:bounded-operator-notation} -->
> The *bounded inverse* of $$A \in \mathcal{B}(\mathbf{H})$$ is an element $$B \in \mathcal{B}(\mathbf{H})$$ such that $$AB = BA = \mathbf{1}$$, where $$\mathbf{1} \in \mathcal{B}(\mathbf{H})$$ is the multiplicative identity element.

This is required to define the "spectrum" of an operator, which is required by much of what follows

> **Definition** *(Resolvent and Spectrum)*
<!--  \label{def:bounded-operator-resolvent-and-spectrum} % Hall Definition 7.4 -->
<!--  \uses{def:bounded-operator-notation} -->
<!--  \uses{def:bounded-inverse} -->
> For $$A \in \mathcal{B}(\mathbf{H})$$, the *resolvent set* of $$A$$, denoted as $$\rho(A)$$, is the set of all $$\lambda \in \mathbb{C}$$ such that the operator $$(A - \lambda \mathbf{1})$$ has a bounded inverse. The *spectrum* of $$A$$, denoted by $$\sigma(A)$$, is the complement of $$A$$'s resolvent set $$\rho(A)$$ in $$\mathbb{C}$$. For $$\lambda$$ in the resolvent set of $$A$$ the bounded inverse of $$(A - \lambda \mathbf{1})$$, which we notate as $$(A - \lambda \mathbf{1})^{-1}$$, is called the *resolvent* of $$A$$ at $$\lambda$$.

## Spectral Theorem for Bounded Self-Adjoint Operators
In this section we will actually be able to state the Spectral Theorem. However, we will only be able to do so after introducing "substantial machinary" related to "projection-valued measures".

### Projection-Valued Measures
"Projection-valued measures" are "core" to the Spectral Theorem. Basically, they generalize the notion of a measure. A "projection-valued measure", instead of taking on positive real-values as a standard measure does, takes on "bounded orthogonal projection" values. Formally, we define this by first introducing the notion of a "bounded orthogonal projection"

> **Definition** *(Resolvent and Spectrum)*
<!--  \label{def:bounded-orthogonal-projection} -->
<!--  \uses{def:bounded-operator-notation} -->
> A *bounded orthogonal projection*, sometimes shortened to *orthogonal projection* or simply *projection*, is an element $$P \in \mathcal{B}(\mathbf{H})$$ such that $$P^2 = P$$ and $$P^* = P$$.

The notion of a bounded orthogonal projection can then be employed to define a "projection-valued measure"

> **Definition** *(Projection-Valued Measure)*
<!--  \label{def:projection-valued-measure} % Hall Definition 7.10 -->
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

Now, we can associate a positive real-valued measure $$\mu_\psi$$ to a projection-valued measure $$\mu$$ and any $$\psi \in \mathbf{H}$$ as follows:

> **Theorem** *(Projection-Valued Measure's Associated Measure)*
<!--  \label{thrm:projection-valued-measures-associated-measure} % Hall bottom of page 138 -->
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
> defines a positive real-valued measure $$\mu_\psi$$ on $$\Omega(X)$$.
