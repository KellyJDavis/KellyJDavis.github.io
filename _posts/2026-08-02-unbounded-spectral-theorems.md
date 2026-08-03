---
title:  "Spectral Theorem for Unbounded, Self-Adjoint Operators"
date:   2026-08-02 19:30:00 +0200
categories: functional-analysis
---

Here we will state and prove the [**Spectral Theorem for Unbounded, Self-Adjoint Operators**](#thrm:hall-10.4). This theorem extends the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators) to the unbounded self-adjoint operators that AQFT relies on throughout — field operators, and the self-adjoint operators built from them, are essentially never bounded — and is a prerequisite for the rest of the AQFT work that motivated this series.

This post is a direct continuation of [Spectral Theorem for Bounded, Self-Adjoint Operators](../spectral-theorems), and depends on it: a number of the definitions, propositions, lemmas, and theorems proven there are reused here without repetition. Where this happens, we link directly to the relevant element in that post rather than restating it under a new name in this one.

As before, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

A note on conventions, extending the one given in the previous post. Results that are standard and whose proofs lie outside the scope of the development are, as before, stated in full but not proven, marked by the absence of an accompanying **Proof**. Every other result stated here — including everything below drawn from Chap. 9 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5) on unbounded operators — is proven in full, and every use of a prior result is made explicit, including a check that its hypotheses actually hold in the situation at hand. We do not assume the reader has already encountered unbounded operators: the relevant definitions are built up from scratch below, so that this post is self-contained modulo the previous one.

# Spectral Theorem: Unbounded Self-Adjoint Operators

We proceed in four stages, mirroring Chaps. 9 and 10 of [Hall](https://doi.org/10.1007/978-1-4614-7116-5). First, the basic theory of unbounded operators — adjoints, symmetry, self-adjointness, closedness, and the spectrum (this section, mirroring Chap. 9). Second, a theory of integrating an unbounded function against a projection-valued measure (mirroring Sect. 10.1). Third, the spectral theorem for *bounded normal* operators (mirroring Sect. 10.3). Finally, the Cayley transform, which lets us reduce the unbounded self-adjoint case to the bounded normal case and complete the proof (mirroring Sect. 10.4).

## Unbounded Operators

### Adjoint and Closure of an Unbounded Operator

Recall from the [previous post](../spectral-theorems) that $$\mathbf{H}$$ denotes a separable, complex Hilbert space, and that $$\mathcal{B}(\mathbf{H})$$ denotes the set of bounded operators on $$\mathbf{H}$$. We now introduce operators that need not be bounded, and need not even be defined on all of $$\mathbf{H}$$; every definition and result below refers back to $$\mathbf{H}$$ in this fixed sense.

> **Definition** *(Unbounded Operator)*
<a name="def:hall-3.1"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> An *unbounded operator* $$A$$ on $$\mathbf{H}$$ is a linear map $$A : \text{Dom}(A) \to \mathbf{H}$$, where $$\text{Dom}(A)$$, called the *domain* of $$A$$, is a dense subspace of $$\mathbf{H}$$. Here "unbounded" means "not necessarily bounded": we permit the case $$\text{Dom}(A) = \mathbf{H}$$ together with $$A \in \mathcal{B}(\mathbf{H})$$, but do not require it.

Before defining the adjoint of an unbounded operator, we record a small fact about dense subspaces that we will use repeatedly below — both to pin down the adjoint uniquely, and at several later points where we want to conclude that two vectors, or two operators, coincide from an equation that only holds on a dense subspace.

> **Lemma** *(Equality Testing on a Dense Subspace)*
<a name="lmm:hall-dense-testing"></a>
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> Suppose $$\chi_1, \chi_2 \in \mathbf{H}$$ and $$D \subset \mathbf{H}$$ is a dense subset such that $$\left< \chi_1, \psi \right> = \left< \chi_2, \psi \right>$$ for all $$\psi \in D$$. Then $$\chi_1 = \chi_2$$.

**Proof**
Set $$\chi \equiv \chi_1 - \chi_2$$. For every $$\psi \in D$$, linearity of the inner product in its second argument together with the hypothesis gives $$\left< \chi, \psi \right> = \left< \chi_1, \psi \right> - \left< \chi_2, \psi \right> = 0$$. Since $$D$$ is dense in $$\mathbf{H}$$, there is a sequence $$\{ \psi_n \}_{n \in \mathbb{N}}$$ in $$D$$ with $$\psi_n \to \chi$$. Fixing $$\chi$$ and applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) to this sequence,

$$
    \left< \chi, \chi \right> = \lim_{n \to \infty} \left< \chi, \psi_n \right> = \lim_{n \to \infty} 0 = 0.
$$

Since $$\mathbf{H}$$ is an inner product space, $$\left< \chi, \chi \right> = 0$$ forces $$\chi = 0$$, i.e. $$\chi_1 = \chi_2$$.$$\blacksquare$$

If $$A$$ happens to be a bounded operator on all of $$\mathbf{H}$$, then for any $$\phi \in \mathbf{H}$$ the linear functional $$\psi \mapsto \left< \phi, A\psi \right>$$ is automatically bounded, and the [**Riesz Theorem**](../spectral-theorems/#thrm:riesz-representation) produces a unique $$\chi \in \mathbf{H}$$ with $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi$$; we then set $$A^*\phi \equiv \chi$$. If $$A$$ is genuinely unbounded, the functional $$\psi \mapsto \left< \phi, A\psi \right>$$ need not be bounded on $$\text{Dom}(A)$$ for every $$\phi$$ — but it may be bounded for *some* $$\phi$$, and it is exactly this set of $$\phi$$'s on which the adjoint gets defined.

> **Definition** *(Adjoint of an Unbounded Operator)*
<a name="def:hall-9.1"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{../spectral-theorems/#thrm:riesz-representation} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$. Let $$\text{Dom}(A^*)$$ be the space of all $$\phi \in \mathbf{H}$$ for which the linear functional
>
> $$
>     \psi \longmapsto \left< \phi, A\psi \right>, \qquad \psi \in \text{Dom}(A),
> $$
>
> is *bounded*, i.e. for which there is a constant $$C \in \mathbb{R}$$ such that $$\lvert \left< \phi, A\psi \right> \rvert \le C \left\| \psi \right\|$$ for all $$\psi \in \text{Dom}(A)$$. For $$\phi \in \text{Dom}(A^*)$$, define $$A^*\phi$$ to be the unique vector such that
>
> $$
>     \left< \phi, A\psi \right> = \left< A^*\phi, \psi \right> \quad \text{for all } \psi \in \text{Dom}(A).
> $$
>
> The operator $$A^*$$, with domain $$\text{Dom}(A^*)$$, is called the *adjoint* of $$A$$.

We now justify that $$A^*\phi$$, as described in this definition, actually exists and is unique for each $$\phi \in \text{Dom}(A^*)$$ — this is not automatic once $$A$$ is only densely defined, and we spell out exactly which prior results make it work. Fix $$\phi \in \text{Dom}(A^*)$$, and consider the map $$T : \text{Dom}(A) \to \mathbb{C}$$ given by $$T\psi \equiv \left< \phi, A\psi \right>$$. Since $$A$$ is linear (by the [definition of an unbounded operator](#def:hall-3.1)) and the inner product on $$\mathbf{H}$$ is linear in its second argument, $$T$$ is a linear map; by the defining property of $$\text{Dom}(A^*)$$ used above, $$T$$ is bounded on $$\text{Dom}(A)$$.

To apply the [**Bounded Linear Transformation Theorem**](../spectral-theorems/#thrm:bounded-linear-transformation-theorem) to $$T$$, we check its three hypotheses hold: it asks for a normed space $$V_1$$, a Banach space $$V_2$$, a dense subspace $$W \subset V_1$$, and a bounded linear map $$T : W \to V_2$$. Here $$\mathbf{H}$$, being a Hilbert space, is in particular a normed vector space with norm $$\left\| \cdot \right\|$$ induced by its inner product, so we may take $$V_1 = \mathbf{H}$$. The target space $$\mathbb{C}$$, with the usual absolute value as norm, is a Banach space, since every Cauchy sequence of complex numbers converges. By the [definition of an unbounded operator](#def:hall-3.1), $$\text{Dom}(A)$$ is a dense subspace of $$\mathbf{H}$$, so we may take $$W = \text{Dom}(A)$$. We have just checked $$T$$ is linear and bounded on $$W$$. All hypotheses being met, there is a unique bounded linear map $$\tilde{T} : \mathbf{H} \to \mathbb{C}$$ with $$\tilde{T} = T$$ on $$\text{Dom}(A)$$.

Now $$\tilde{T}$$ is a bounded linear functional on the Hilbert space $$\mathbf{H}$$, so the [**Riesz Theorem**](../spectral-theorems/#thrm:riesz-representation) applies — its only hypothesis is exactly that $$\tilde{T}$$ be a bounded linear functional on a Hilbert space — and produces a unique $$\chi \in \mathbf{H}$$ with $$\tilde{T}\psi = \left< \chi, \psi \right>$$ for all $$\psi \in \mathbf{H}$$. In particular, restricting to $$\psi \in \text{Dom}(A)$$, where $$\tilde{T}$$ agrees with $$T$$,

$$
    \left< \phi, A\psi \right> = T\psi = \tilde{T}\psi = \left< \chi, \psi \right> \quad \text{for all } \psi \in \text{Dom}(A).
$$

So $$\chi$$ satisfies the defining equation of $$A^*\phi$$ in [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1). For uniqueness: if $$\chi'$$ also satisfied $$\left< \phi, A\psi \right> = \left< \chi', \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$, then $$\chi$$ and $$\chi'$$ would agree in inner product against every element of the dense subset $$\text{Dom}(A)$$, so $$\chi = \chi'$$ by [Lemma (Equality Testing on a Dense Subspace)](#lmm:hall-dense-testing). We may therefore unambiguously set $$A^*\phi \equiv \chi$$.

Before proceeding, we check that $$A^*$$, as just constructed, is again a linear operator on its domain — a fact used implicitly throughout the rest of this post.

> **Proposition** *(Linearity of the Adjoint)*
<a name="prpstn:hall-linearity-of-the-adjoint"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$. Then $$A^*$$ is linear on $$\text{Dom}(A^*)$$: for all $$\phi_1, \phi_2 \in \text{Dom}(A^*)$$ and $$\alpha, \beta \in \mathbb{C}$$, we have $$\alpha\phi_1 + \beta\phi_2 \in \text{Dom}(A^*)$$, and
>
> $$
>     A^*(\alpha\phi_1 + \beta\phi_2) = \alpha A^*\phi_1 + \beta A^*\phi_2.
> $$

**Proof**
Fix $$\phi_1, \phi_2 \in \text{Dom}(A^*)$$ and $$\alpha, \beta \in \mathbb{C}$$. For every $$\psi \in \text{Dom}(A)$$, using that the inner product on $$\mathbf{H}$$ is conjugate-linear in its first argument, and the [definition of the adjoint](#def:hall-9.1) applied to $$\phi_1$$ and to $$\phi_2$$ separately,

$$
\begin{align}
    \left< \alpha\phi_1 + \beta\phi_2, A\psi \right> &= \overline{\alpha} \left< \phi_1, A\psi \right> + \overline{\beta} \left< \phi_2, A\psi \right> \\
                                                       &= \overline{\alpha} \left< A^*\phi_1, \psi \right> + \overline{\beta} \left< A^*\phi_2, \psi \right> \\
                                                       &= \left< \alpha A^*\phi_1 + \beta A^*\phi_2, \psi \right>,
\end{align}
$$

where the last line again used conjugate-linearity of the inner product in its first argument, this time read right to left. By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43), $$\psi \mapsto \left< \alpha A^*\phi_1 + \beta A^*\phi_2, \psi \right>$$ is bounded on $$\mathbf{H}$$, with bounding constant $$\left\| \alpha A^*\phi_1 + \beta A^*\phi_2 \right\|$$; by the equality just derived, the functional $$\psi \mapsto \left< \alpha\phi_1 + \beta\phi_2, A\psi \right>$$ is therefore bounded on $$\text{Dom}(A)$$, with the same constant. By the [definition of the adjoint](#def:hall-9.1), this shows $$\alpha\phi_1 + \beta\phi_2 \in \text{Dom}(A^*)$$.

Moreover, the equality derived above states precisely that $$\left< \alpha\phi_1 + \beta\phi_2, A\psi \right> = \left< \alpha A^*\phi_1 + \beta A^*\phi_2, \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$; by uniqueness in the [definition of the adjoint](#def:hall-9.1), $$A^*(\alpha\phi_1 + \beta\phi_2) = \alpha A^*\phi_1 + \beta A^*\phi_2$$.$$\blacksquare$$

Among unbounded operators, the ones of central interest to us are those whose adjoint interacts with them in a controlled way. The simplest such condition asks that the defining equation of the adjoint hold with $$A$$ in place of $$A^*$$.

> **Definition** *(Symmetric Operator)*
<a name="def:hall-9.2"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{def:hall-9.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *symmetric* if
>
> $$
>     \left< \phi, A\psi \right> = \left< A\phi, \psi \right>
> $$
>
> for all $$\phi, \psi \in \text{Dom}(A)$$.

To make the relationship between a symmetric operator $$A$$ and its adjoint $$A^*$$ precise, we need the notion of one operator extending another.

> **Definition** *(Extension of an Operator)*
<a name="def:hall-9.3"></a>
<!--  \uses{def:hall-3.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is an *extension* of an unbounded operator $$B$$ on $$\mathbf{H}$$ if $$\text{Dom}(B) \subset \text{Dom}(A)$$ and $$A\psi = B\psi$$ for all $$\psi \in \text{Dom}(B)$$. In this situation we also say $$B$$ is a *restriction* of $$A$$ to $$\text{Dom}(B)$$, and, for a subspace $$W \subset \text{Dom}(A)$$, write $$A\vert_W$$ for the restriction of $$A$$ with domain $$W$$.

If $$A$$ is symmetric, it turns out that $$A^*$$ is always an extension of $$A$$ in the sense just defined — this is the content of the next proposition, and is the beginning of why symmetric operators are of interest at all.

> **Proposition** *(Symmetric Operators and the Adjoint)*
<a name="prpstn:hall-9.4"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.3} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> An unbounded operator $$A$$ is symmetric if and only if $$A^*$$ is an extension of $$A$$.

**Proof**
We first prove the forward direction, i.e. that if $$A$$ is symmetric, then $$A^*$$ is an extension of $$A$$. Fix $$\phi \in \text{Dom}(A)$$. By the [definition of symmetric](#def:hall-9.2), $$\left< \phi, A\psi \right> = \left< A\phi, \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$. Hence, by the [**Cauchy–Schwarz Inequality**](../spectral-theorems/#prpstn:hall-a.43) — applicable since $$\mathbf{H}$$ is an inner product space and $$A\phi, \psi \in \mathbf{H}$$ —

$$
    \lvert \left< \phi, A\psi \right> \rvert = \lvert \left< A\phi, \psi \right> \rvert \le \left\| A\phi \right\| \left\| \psi \right\|
$$

for all $$\psi \in \text{Dom}(A)$$, which is precisely the statement that $$\psi \mapsto \left< \phi, A\psi \right>$$ is bounded, with bounding constant $$C = \left\| A\phi \right\|$$. By the [definition of the adjoint](#def:hall-9.1), this shows $$\phi \in \text{Dom}(A^*)$$.

By the same [definition](#def:hall-9.1), $$A^*\phi$$ is the unique vector $$\chi$$ satisfying $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$. We have just observed that $$\chi = A\phi$$ satisfies exactly this equation, by symmetry of $$A$$; by this uniqueness, $$A^*\phi = A\phi$$.

As $$\phi \in \text{Dom}(A)$$ was arbitrary, we have shown $$\text{Dom}(A) \subset \text{Dom}(A^*)$$ and that $$A^*$$ agrees with $$A$$ on $$\text{Dom}(A)$$. By the [definition of extension](#def:hall-9.3), this is precisely the statement that $$A^*$$ is an extension of $$A$$.

We now prove the reverse direction, i.e. that if $$A^*$$ is an extension of $$A$$, then $$A$$ is symmetric. By the [definition of extension](#def:hall-9.3), $$\text{Dom}(A) \subset \text{Dom}(A^*)$$ and $$A^*\phi = A\phi$$ for all $$\phi \in \text{Dom}(A)$$. Fix $$\phi, \psi \in \text{Dom}(A)$$. By the [definition of the adjoint](#def:hall-9.1),

$$
    \left< \phi, A\psi \right> = \left< A^*\phi, \psi \right> = \left< A\phi, \psi \right>,
$$

where the final equality used $$A^*\phi = A\phi$$. As $$\phi, \psi \in \text{Dom}(A)$$ were arbitrary, this is precisely the [definition of symmetric](#def:hall-9.2) for $$A$$.$$\blacksquare$$

We now come to the key definition of this post: that of self-adjointness. Every self-adjoint operator is symmetric, as we will see falls immediately out of [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), but symmetry alone only gives $$A^*$$ as an extension of $$A$$ — self-adjointness demands equality.

> **Definition** *(Self-Adjoint Operator)*
<a name="def:hall-9.5"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{def:hall-9.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *self-adjoint* if $$\text{Dom}(A^*) = \text{Dom}(A)$$ and $$A^*\phi = A\phi$$ for all $$\phi \in \text{Dom}(A)$$. Equivalently, $$A$$ is self-adjoint if $$A^* = A$$, where equality of unbounded operators is understood to include equality of domains.

Indeed, if $$A$$ is self-adjoint then $$\text{Dom}(A^*) = \text{Dom}(A)$$ and $$A^* = A$$ on this common domain, which is exactly [Definition (Extension of an Operator)](#def:hall-9.3) applied with $$B = A$$: $$A^*$$ is (trivially) an extension of $$A$$, so by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A$$ is symmetric. Conversely, a symmetric operator $$A$$ is self-adjoint precisely when $$\text{Dom}(A^*)$$ is no bigger than $$\text{Dom}(A)$$, since symmetry already gives the reverse containment via [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4). This is usually the difficulty in showing a symmetric operator is self-adjoint: showing that the adjoint's domain does not overshoot.

The next two definitions let us make sense of the *closure* of an unbounded operator, which we will need almost immediately.

> **Definition** *(Closed and Closable Operators)*
<a name="def:hall-9.6"></a>
<!--  \uses{def:hall-3.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closed* if the graph of $$A$$ is a closed subset of $$\mathbf{H} \times \mathbf{H}$$. Equivalently — unwinding what it means for a subset of $$\mathbf{H} \times \mathbf{H}$$ to be closed — $$A$$ is closed if and only if: whenever $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A)$$ and there exist $$\psi, \varphi \in \mathbf{H}$$ with $$\psi_n \to \psi$$ and $$A\psi_n \to \varphi$$, it follows that $$\psi \in \text{Dom}(A)$$ and $$A\psi = \varphi$$.
>
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closable* if the closure, in $$\mathbf{H} \times \mathbf{H}$$, of the graph of $$A$$ is again the graph of some (necessarily linear) operator. If $$A$$ is closable, the *closure* $$A^{\text{cl}}$$ of $$A$$ is the operator whose graph is the closure of the graph of $$A$$. Equivalently, $$A^{\text{cl}}$$ is the smallest closed extension of $$A$$: it is itself a closed extension of $$A$$, and any closed extension of $$A$$ is in turn an extension of $$A^{\text{cl}}$$.

With self-adjointness, symmetry, and closure all in hand, we can state the last definition of this subsection.

> **Definition** *(Essentially Self-Adjoint Operator)*
<a name="def:hall-9.7"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.6} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *essentially self-adjoint* if $$A$$ is symmetric, $$A$$ is closable, and $$A^{\text{cl}}$$ is self-adjoint.

### Elementary Properties of Adjoints and Closed Operators

We record here some basic properties of adjoints and closures that we will draw on repeatedly below. Throughout, if we say two operators *coincide*, we mean they have the same domain and are equal on that common domain.

Our first observation is that the adjoint's graph is always closed, regardless of any hypothesis on $$A$$; from this, closability of symmetric operators follows immediately.

> **Proposition** *(Closedness of the Adjoint's Graph; Closability of Symmetric Operators)*
<a name="prpstn:hall-9.8"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{prpstn:hall-9.4} -->
> 1. If $$A$$ is an unbounded operator on $$\mathbf{H}$$, then the graph of $$A^*$$ (which may or may not be densely defined) is closed in $$\mathbf{H} \times \mathbf{H}$$.
> 2. A symmetric operator is always closable.

**Proof**
**Part 1:** Suppose $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A^*)$$ converging to some $$\psi \in \mathbf{H}$$, and suppose also that $$\{ A^*\psi_n \}_{n \in \mathbb{N}}$$ converges to some $$\varphi \in \mathbf{H}$$. By the [definition of the adjoint](#def:hall-9.1), $$\left< \psi_n, A\chi \right> = \left< A^*\psi_n, \chi \right>$$ for every $$\chi \in \text{Dom}(A)$$ and every $$n$$. Fix $$\chi \in \text{Dom}(A)$$. Applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — valid since $$\psi_n \to \psi$$ and $$A^*\psi_n \to \varphi$$ in $$\mathbf{H}$$ — to both sides of this equation,

$$
    \left< \psi, A\chi \right> = \lim_{n \to \infty} \left< \psi_n, A\chi \right> = \lim_{n \to \infty} \left< A^*\psi_n, \chi \right> = \left< \varphi, \chi \right>.
$$

As $$\chi \in \text{Dom}(A)$$ was arbitrary, this shows $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = \varphi$$, by the [definition of the adjoint](#def:hall-9.1). By the [sequential characterization of closedness](#def:hall-9.6), this establishes that the graph of $$A^*$$ is closed, the desired **Part 1** result.

**Part 2:** Suppose $$A$$ is symmetric. By [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A^*$$ is an extension of $$A$$, so the graph of $$A$$ is a subset of the graph of $$A^*$$. By **Part 1**, the graph of $$A^*$$ is closed, so the closure of the graph of $$A$$ — being the smallest closed subset of $$\mathbf{H} \times \mathbf{H}$$ containing the graph of $$A$$ — is contained in the graph of $$A^*$$. In particular, the closure of the graph of $$A$$ is a subset of the graph of a function (namely $$A^*$$), and is therefore itself the graph of a function. By the [definition of closable](#def:hall-9.6), $$A$$ is closable, the desired **Part 2** result.$$\blacksquare$$

Having shown that closable operators are exactly those with a well-behaved closure, we record how the closure interacts with the adjoint: taking the adjoint of $$A$$ or of its closure $$A^{\text{cl}}$$ gives the same operator.

> **Proposition** *(The Adjoint of a Closure)*
<a name="prpstn:hall-9.10"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.6} -->
> If $$A$$ is a closable operator on $$\mathbf{H}$$, then the adjoint of $$A^{\text{cl}}$$ coincides with the adjoint of $$A$$.

**Proof**
We prove $$\text{Dom}\big( (A^{\text{cl}})^* \big) \subset \text{Dom}(A^*)$$ and $$\text{Dom}(A^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big)$$ in turn, checking in each case that $$A^*$$ and $$(A^{\text{cl}})^*$$ agree.

**Part 1:** Suppose $$\psi \in \text{Dom}\big( (A^{\text{cl}})^* \big)$$, so that there is a $$\varphi \in \mathbf{H}$$ with $$\left< \psi, A^{\text{cl}}\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A^{\text{cl}})$$, by the [definition of the adjoint](#def:hall-9.1). Since $$A^{\text{cl}}$$ is an extension of $$A$$, in particular $$\text{Dom}(A) \subset \text{Dom}(A^{\text{cl}})$$ and $$A^{\text{cl}} = A$$ on $$\text{Dom}(A)$$, so this equation restricts to $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$. By the [definition of the adjoint](#def:hall-9.1) applied to $$A$$, this shows $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = \varphi = (A^{\text{cl}})^*\psi$$.

**Part 2:** Suppose $$\psi \in \text{Dom}(A^*)$$, so that there is a $$\varphi \in \mathbf{H}$$ with $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$. Let $$\xi \in \text{Dom}(A^{\text{cl}})$$, with $$A^{\text{cl}}\xi = \eta$$. By the [definition of closure](#def:hall-9.6), there is a sequence $$\{ \chi_n \}_{n \in \mathbb{N}}$$ in $$\text{Dom}(A)$$ with $$\chi_n \to \xi$$ and $$A\chi_n \to \eta$$. For each $$n$$, $$\left< \psi, A\chi_n \right> = \left< \varphi, \chi_n \right>$$; letting $$n \to \infty$$ and applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — valid since $$\chi_n \to \xi$$ and $$A\chi_n \to \eta$$ — gives $$\left< \psi, \eta \right> = \left< \varphi, \xi \right>$$, i.e. $$\left< \psi, A^{\text{cl}}\xi \right> = \left< \varphi, \xi \right>$$. As $$\xi \in \text{Dom}(A^{\text{cl}})$$ was arbitrary, this shows $$\psi \in \text{Dom}\big( (A^{\text{cl}})^* \big)$$ and $$(A^{\text{cl}})^*\psi = \varphi = A^*\psi$$.

Combining **Part 1** and **Part 2** gives $$\text{Dom}(A^*) = \text{Dom}\big( (A^{\text{cl}})^* \big)$$, with $$A^*$$ and $$(A^{\text{cl}})^*$$ agreeing on this common domain — the desired result.$$\blacksquare$$

When $$A$$ is essentially self-adjoint, its closure is not just *a* self-adjoint extension of $$A$$ — it is the *only* one, a fact we will use directly in the proof of [Proposition (Direct Sums of Bounded Self-Adjoint Operators)](#prpstn:hall-9.26) below.

> **Proposition** *(Uniqueness of the Self-Adjoint Extension of an Essentially Self-Adjoint Operator)*
<a name="prpstn:hall-9.11"></a>
<!--  \uses{def:hall-9.3} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{prpstn:hall-9.8} -->
> If $$A$$ is essentially self-adjoint, then $$A^{\text{cl}}$$ is the unique self-adjoint extension of $$A$$.

**Proof**
Suppose $$B$$ is a self-adjoint extension of $$A$$. Since $$B = B^*$$, [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8) shows $$B$$ is closed. As $$B$$ is a closed extension of $$A$$, it is, by the [definition of closure](#def:hall-9.6) as the smallest closed extension, an extension of $$A^{\text{cl}}$$; that is, $$\text{Dom}(A^{\text{cl}}) \subset \text{Dom}(B)$$.

We next check that, quite generally, if $$C_1$$ is an extension of $$C_2$$ then $$\text{Dom}(C_1^*) \subset \text{Dom}(C_2^*)$$. Indeed, if $$\phi \in \text{Dom}(C_1^*)$$, then $$\psi \mapsto \left< \phi, C_1\psi \right>$$ is bounded on $$\text{Dom}(C_1)$$, by the [definition of the adjoint](#def:hall-9.1); since $$C_1$$ agrees with $$C_2$$ on the subset $$\text{Dom}(C_2) \subset \text{Dom}(C_1)$$, the same functional, restricted to $$\text{Dom}(C_2)$$, equals $$\psi \mapsto \left< \phi, C_2\psi \right>$$, and a functional bounded on a set is bounded on any subset of it with the same constant; so $$\phi \in \text{Dom}(C_2^*)$$, by the [definition of the adjoint](#def:hall-9.1) again. Applying this with $$C_1 = B$$ and $$C_2 = A^{\text{cl}}$$ (recalling $$B$$ is an extension of $$A^{\text{cl}}$$) gives $$\text{Dom}(B^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big)$$. Thus we have

$$
    \text{Dom}(B^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big) \subset \text{Dom}(B),
$$

where the second containment is $$\text{Dom}(A^{\text{cl}}) \subset \text{Dom}(B)$$ from above, using that $$A$$ is essentially self-adjoint so $$(A^{\text{cl}})^* = A^{\text{cl}}$$. Since $$B$$ is self-adjoint, $$\text{Dom}(B^*) = \text{Dom}(B)$$, so all three sets above are equal:

$$
    \text{Dom}(B) = \text{Dom}(B^*) = \text{Dom}\big( (A^{\text{cl}})^* \big) = \text{Dom}(A^{\text{cl}}).
$$

As $$B$$ extends $$A^{\text{cl}}$$ and their domains coincide, $$B = A^{\text{cl}}$$.$$\blacksquare$$

We record next a description of $$\text{Ker}(A^*)$$ in terms of $$A$$ itself, generalizing the corresponding fact for bounded operators.

> **Proposition** *(Orthogonal Complement of the Range)*
<a name="prpstn:hall-9.12"></a>
<!--  \uses{def:hall-9.1} -->
> If $$A$$ is an unbounded operator on $$\mathbf{H}$$, then
>
> $$
>     \left( \text{Range}(A) \right)^\perp = \text{Ker}(A^*).
> $$

**Proof**
We prove the two containments $$\left( \text{Range}(A) \right)^\perp \subset \text{Ker}(A^*)$$ and $$\text{Ker}(A^*) \subset \left( \text{Range}(A) \right)^\perp$$ in turn.

Suppose $$\psi \in \left( \text{Range}(A) \right)^\perp$$. Then for all $$\phi \in \text{Dom}(A)$$ we have $$\left< \psi, A\phi \right> = 0$$. That is, the linear functional $$\psi' \mapsto \left< \psi, A\psi' \right>$$ is bounded on $$\text{Dom}(A)$$ — it is identically zero, with bounding constant $$C = 0$$. By the [definition of the adjoint](#def:hall-9.1), this shows $$\psi \in \text{Dom}(A^*)$$ with $$A^*\psi = 0$$, i.e. $$\psi \in \text{Ker}(A^*)$$.

Conversely, suppose $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = 0$$. By the [definition of the adjoint](#def:hall-9.1), $$\left< \psi, A\phi \right> = \left< A^*\psi, \phi \right> = 0$$ for all $$\phi \in \text{Dom}(A)$$. Thus $$\psi$$ is orthogonal to every element of $$\text{Range}(A)$$, i.e. $$\psi \in \left( \text{Range}(A) \right)^\perp$$.

Combining both containments gives the desired equality.$$\blacksquare$$

The next proposition tells us how the adjoint interacts with adding a bounded operator, a computation we will need repeatedly below. We follow the proof strategy of Kelly's solution to Problem 9.11.3 of the exercises to Chap. 9, with one correction noted in the proof.

> **Proposition** *(Adjoint of a Sum with a Bounded Operator)*
<a name="prpstn:hall-9.13"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$ and $$B \in \mathcal{B}(\mathbf{H})$$ is a bounded operator defined on all of $$\mathbf{H}$$. Let $$A + B$$ denote the operator with $$\text{Dom}(A+B) = \text{Dom}(A)$$, given by $$(A+B)\psi = A\psi + B\psi$$ for all $$\psi \in \text{Dom}(A)$$. Then $$(A+B)^*$$ has the same domain as $$A^*$$, and
>
> $$
>     (A+B)^*\psi = A^*\psi + B^*\psi \quad \text{for all } \psi \in \text{Dom}(A^*).
> $$
>
> In particular, the sum of an unbounded self-adjoint operator and a bounded self-adjoint operator (defined on all of $$\mathbf{H}$$) is self-adjoint on the domain of the unbounded operator.

**Proof**
We prove $$\text{Dom}\big( (A+B)^* \big) \subset \text{Dom}(A^*)$$ and $$\text{Dom}(A^*) \subset \text{Dom}\big( (A+B)^* \big)$$ in turn, and then the stated formula.

**Part 1: $$\text{Dom}\big( (A+B)^* \big) \subset \text{Dom}(A^*)$$.** Suppose $$\phi \in \text{Dom}\big( (A+B)^* \big)$$, i.e. there is a constant $$C$$ with $$\lvert \left< \phi, (A+B)\psi \right> \rvert \le C \left\| \psi \right\|$$ for all $$\psi \in \text{Dom}(A) = \text{Dom}(A+B)$$. Since $$\left< \phi, (A+B)\psi \right> = \left< \phi, A\psi \right> + \left< \phi, B\psi \right>$$ by linearity of the inner product in its second argument and the given formula for $$(A+B)\psi$$, we may isolate the $$A$$-term:

$$
    \left< \phi, A\psi \right> = \left< \phi, (A+B)\psi \right> - \left< \phi, B\psi \right>.
$$

(This is the point where we depart from Kelly's original derivation, which attempted to isolate $$\left< \phi, A\psi \right>$$ by an algebraic manipulation of the inequality $$\lvert \left< \phi, A\psi \right> \rvert \le \lvert \left< \phi, (A+B)\psi \right> \rvert + \left\| \phi \right\| \left\| B \right\| \left\| \psi \right\|$$ that does not follow from it; isolating the exact identity above and then bounding is the cleaner route to the same conclusion.) Applying the triangle inequality for complex numbers to the right-hand side, then [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) and boundedness of $$B$$ to the second term:

$$
\begin{align}
    \lvert \left< \phi, A\psi \right> \rvert &\le \lvert \left< \phi, (A+B)\psi \right> \rvert + \lvert \left< \phi, B\psi \right> \rvert \\
                                               &\le C \left\| \psi \right\| + \left\| \phi \right\| \left\| B\psi \right\| \\
                                               &\le C \left\| \psi \right\| + \left\| \phi \right\| \left\| B \right\| \left\| \psi \right\| \\
                                               &= \left( C + \left\| \phi \right\| \left\| B \right\| \right) \left\| \psi \right\|.
\end{align}
$$

Since $$C$$, $$\left\| \phi \right\|$$, and $$\left\| B \right\|$$ are all finite real numbers, $$C' \equiv C + \left\| \phi \right\| \left\| B \right\|$$ is a finite constant, and we have shown $$\lvert \left< \phi, A\psi \right> \rvert \le C' \left\| \psi \right\|$$ for all $$\psi \in \text{Dom}(A)$$. By the [definition of the adjoint](#def:hall-9.1), $$\phi \in \text{Dom}(A^*)$$.

**Part 2: $$\text{Dom}(A^*) \subset \text{Dom}\big( (A+B)^* \big)$$.** Suppose $$\phi \in \text{Dom}(A^*)$$, so there is a constant $$C_A$$ with $$\lvert \left< \phi, A\psi \right> \rvert \le C_A \left\| \psi \right\|$$ for all $$\psi \in \text{Dom}(A)$$. Since $$B$$ is bounded and defined on all of $$\mathbf{H}$$, [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) gives $$\lvert \left< \phi, B\psi \right> \rvert \le \left\| \phi \right\| \left\| B\psi \right\| \le \left\| \phi \right\| \left\| B \right\| \left\| \psi \right\| \equiv C_B \left\| \psi \right\|$$ for all $$\psi \in \mathbf{H}$$, where $$C_B$$ is a finite constant since $$\phi \in \mathbf{H}$$ and $$B \in \mathcal{B}(\mathbf{H})$$. Hence, for all $$\psi \in \text{Dom}(A) = \text{Dom}(A+B)$$, using the triangle inequality for complex numbers,

$$
    \lvert \left< \phi, (A+B)\psi \right> \rvert = \lvert \left< \phi, A\psi \right> + \left< \phi, B\psi \right> \rvert \le \lvert \left< \phi, A\psi \right> \rvert + \lvert \left< \phi, B\psi \right> \rvert \le (C_A + C_B) \left\| \psi \right\|,
$$

where $$C_A + C_B$$ is a finite constant. By the [definition of the adjoint](#def:hall-9.1), $$\phi \in \text{Dom}\big( (A+B)^* \big)$$.

Combining **Part 1** and **Part 2**, $$\text{Dom}(A^*) = \text{Dom}\big( (A+B)^* \big)$$.

**Part 3: the formula.** By the [definition of the adjoint](#def:hall-9.1), for any $$\phi \in \text{Dom}(A^*) = \text{Dom}\big( (A+B)^* \big)$$ and any $$\psi \in \text{Dom}(A) = \text{Dom}(A+B)$$,

$$
\begin{align}
    \left< (A+B)^*\phi, \psi \right> &= \left< \phi, (A+B)\psi \right> \\
                                     &= \left< \phi, A\psi \right> + \left< \phi, B\psi \right> \\
                                     &= \left< A^*\phi, \psi \right> + \left< B^*\phi, \psi \right> \\
                                     &= \left< A^*\phi + B^*\phi, \psi \right>,
\end{align}
$$

where the third equality used the [definition of the adjoint](#def:hall-9.1) applied to $$A$$ and, separately, applied to the everywhere-defined bounded operator $$B$$, and the last equality used linearity of the inner product in its second argument. So $$\left< (A+B)^*\phi, \psi \right> = \left< A^*\phi + B^*\phi, \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$, a dense subset of $$\mathbf{H}$$ by the [definition of an unbounded operator](#def:hall-3.1); by [Lemma (Equality Testing on a Dense Subspace)](#lmm:hall-dense-testing), $$(A+B)^*\phi = A^*\phi + B^*\phi$$.

Finally, suppose $$A$$ is self-adjoint and $$B$$ is bounded and self-adjoint on all of $$\mathbf{H}$$. Then $$\text{Dom}\big( (A+B)^* \big) = \text{Dom}(A^*) = \text{Dom}(A) = \text{Dom}(A+B)$$, using self-adjointness of $$A$$ for the middle equality; and for $$\psi$$ in this common domain, $$(A+B)^*\psi = A^*\psi + B^*\psi = A\psi + B\psi = (A+B)\psi$$, using self-adjointness of $$A$$ and of $$B$$. So $$A+B$$ is self-adjoint.$$\blacksquare$$

We record one more elementary fact about closed operators before turning to the spectrum: a uniform lower bound on $$\left\| (A - \lambda \mathbf{1})\psi \right\|$$ forces the range of $$A - \lambda \mathbf{1}$$ to be closed.

> **Proposition** *(Closedness of the Range from a Lower Bound)*
<a name="prpstn:hall-9.14"></a>
<!--  \uses{def:hall-9.6} -->
<!--  \uses{prpstn:hall-9.13} -->
> Let $$A$$ be a closed operator on $$\mathbf{H}$$ and $$\lambda \in \mathbb{C}$$. Suppose there exists $$\varepsilon > 0$$ such that
>
> $$
>     \varepsilon \left\| \psi \right\| \le \left\| (A - \lambda \mathbf{1})\psi \right\| \qquad \text{for all } \psi \in \text{Dom}(A).
> $$
>
> Then the range of $$A - \lambda \mathbf{1}$$ is a closed subspace of $$\mathbf{H}$$. (Here $$\text{Dom}(A - \lambda \mathbf{1}) \equiv \text{Dom}(A)$$, as in [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) with $$B = -\lambda \mathbf{1}$$.)

**Proof**
Let $$\{ \varphi_n \}_{n \in \mathbb{N}}$$ be a sequence in $$\text{Range}(A - \lambda \mathbf{1})$$ converging to some $$\varphi \in \mathbf{H}$$; we must show $$\varphi \in \text{Range}(A - \lambda \mathbf{1})$$. Write $$\varphi_n = (A - \lambda \mathbf{1})\psi_n$$ for some sequence $$\{ \psi_n \}_{n \in \mathbb{N}}$$ in $$\text{Dom}(A)$$. Applying the hypothesis with $$\psi = \psi_n - \psi_m$$, and using linearity of $$A - \lambda\mathbf{1}$$ on $$\text{Dom}(A)$$,

$$
    \varepsilon \left\| \psi_n - \psi_m \right\| \le \left\| (A - \lambda \mathbf{1})(\psi_n - \psi_m) \right\| = \left\| \varphi_n - \varphi_m \right\|,
$$

so $$\left\| \psi_n - \psi_m \right\| \le \tfrac{1}{\varepsilon} \left\| \varphi_n - \varphi_m \right\|$$. Since $$\{ \varphi_n \}_{n \in \mathbb{N}}$$ converges, it is a Cauchy sequence, so the right-hand side tends to $$0$$ as $$n, m \to \infty$$; hence $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a Cauchy sequence in $$\mathbf{H}$$, and, $$\mathbf{H}$$ being complete, converges to some $$\psi \in \mathbf{H}$$. Since $$\psi_n \to \psi$$ and $$(A - \lambda\mathbf{1})\psi_n = \varphi_n \to \varphi$$, we have

$$
    A\psi_n = \lambda \psi_n + \varphi_n \longrightarrow \lambda \psi + \varphi.
$$

By the [sequential characterization of closedness](#def:hall-9.6) applied to $$A$$ — using $$\psi_n \to \psi$$ and $$A\psi_n \to \lambda\psi + \varphi$$ — we conclude $$\psi \in \text{Dom}(A)$$ and $$A\psi = \lambda \psi + \varphi$$, i.e. $$(A - \lambda \mathbf{1})\psi = \varphi$$. Thus $$\varphi \in \text{Range}(A - \lambda \mathbf{1})$$, and the range of $$A - \lambda \mathbf{1}$$ is closed.$$\blacksquare$$

### The Spectrum of an Unbounded Operator

Recall that for a bounded operator, a number $$\lambda \in \mathbb{C}$$ belongs to the [resolvent set](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum) if $$A - \lambda \mathbf{1}$$ has a bounded inverse, and to the spectrum otherwise. For an unbounded operator $$A$$, we again want $$\lambda$$ to be in the resolvent set precisely when $$A - \lambda \mathbf{1}$$ has a bounded inverse — but since $$A$$ itself is only defined on $$\text{Dom}(A)$$, we have to be careful about what "bounded inverse" means: it should be a bounded operator, defined on all of $$\mathbf{H}$$, landing in $$\text{Dom}(A)$$, that inverts $$A - \lambda \mathbf{1}$$ on both sides.

> **Definition** *(Resolvent Set and Spectrum of an Unbounded Operator)*
<a name="def:hall-9.16"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$. A number $$\lambda \in \mathbb{C}$$ belongs to the *resolvent set* of $$A$$ if there exists a bounded operator $$B \in \mathcal{B}(\mathbf{H})$$ with the following properties:
>
> 1. For all $$\psi \in \mathbf{H}$$, $$B\psi \in \text{Dom}(A)$$ and $$(A - \lambda \mathbf{1})B\psi = \psi$$; and
> 2. For all $$\psi \in \text{Dom}(A)$$, $$B(A - \lambda \mathbf{1})\psi = \psi$$.
>
> If no such bounded operator $$B$$ exists, then $$\lambda$$ belongs to the *spectrum* $$\sigma(A)$$ of $$A$$.

As in the bounded case, even if $$A$$ is self-adjoint, a point $$\lambda \in \sigma(A)$$ need not be an eigenvalue. On the other hand, if $$A\psi = \lambda\psi$$ for some nonzero $$\psi \in \text{Dom}(A)$$, then $$A - \lambda\mathbf{1}$$ is not injective, so it certainly cannot have a two-sided bounded inverse — thus $$\lambda \in \sigma(A)$$.

We now come to a central result: the spectrum of a self-adjoint operator, bounded or not, is always contained in the real line. This is exactly the fact that will let us make sense of the Cayley transform, later in this post.

> **Theorem** *(Spectrum of a Self-Adjoint Operator is Real)*
<a name="thrm:hall-9.17"></a>
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.8} -->
<!--  \uses{prpstn:hall-9.12} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{prpstn:hall-9.14} -->
<!--  \uses{../spectral-theorems/#lmm:hall-7.8} -->
> If $$A$$ is an unbounded self-adjoint operator on $$\mathbf{H}$$, the spectrum of $$A$$ is contained in the real line.

**Proof**
Let $$\lambda = a + ib \in \mathbb{C}$$ with $$b \ne 0$$; we show $$\lambda$$ is in the resolvent set of $$A$$.

Since $$A$$ is [self-adjoint](#def:hall-9.5), $$A^*$$ is (trivially) an extension of $$A$$, so, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A$$ is symmetric. [**Lemma 7.8**](../spectral-theorems/#lmm:hall-7.8) is stated for bounded operators, but its proof only uses symmetry of the operator, together with the algebraic identity $$(A - \lambda\mathbf{1})\psi = (A - a\mathbf{1})\psi - ib\psi$$ and expansion of the resulting inner product — nothing in that argument uses boundedness. It therefore applies here verbatim to our unbounded, symmetric $$A$$, giving

$$
    b^2 \left< \psi, \psi \right> \le \left< (A - \lambda \mathbf{1})\psi, (A - \lambda \mathbf{1})\psi \right> \tag{$\ast$}
$$

for all $$\psi \in \text{Dom}(A)$$. In particular, taking $$\psi \in \text{Dom}(A)$$ with $$(A - \lambda\mathbf{1})\psi = 0$$ forces $$b^2 \left< \psi, \psi \right> \le 0$$, hence $$\psi = 0$$ (as $$b \ne 0$$ and the inner product is positive definite); so $$A - \lambda \mathbf{1}$$ is injective.

Next we show $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$. By [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12) applied to $$A - \lambda \mathbf{1}$$,

$$
    \left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp = \text{Ker}\left( (A - \lambda \mathbf{1})^* \right).
$$

By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) with $$B = -\lambda \mathbf{1}$$ — a bounded operator on all of $$\mathbf{H}$$ — $$(A - \lambda\mathbf{1})^* = A^* - \overline{\lambda}\mathbf{1} = A - \overline{\lambda}\mathbf{1}$$, using $$A^* = A$$. Since $$\overline{\lambda} = a - ib$$ also has $$b \ne 0$$ as its (negated) imaginary part, the argument of the previous paragraph applies verbatim with $$\overline{\lambda}$$ in place of $$\lambda$$ and shows $$A - \overline{\lambda}\mathbf{1}$$ is injective, i.e. $$\text{Ker}(A - \overline{\lambda}\mathbf{1}) = \{0\}$$. Hence

$$
    \left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp = \text{Ker}(A - \overline{\lambda}\mathbf{1}) = \{0\},
$$

so $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$.

Since $$A = A^*$$, [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8) shows $$A$$ is closed. Rewriting $$(\ast)$$ as $$\left\| (A - \lambda\mathbf{1})\psi \right\|^2 \ge b^2 \left\| \psi \right\|^2$$ and taking square roots, $$\lvert b \rvert \left\| \psi \right\| \le \left\| (A-\lambda\mathbf{1})\psi \right\|$$ for all $$\psi \in \text{Dom}(A)$$. This lets us apply [Proposition (Closedness of the Range from a Lower Bound)](#prpstn:hall-9.14) with $$\varepsilon = \lvert b \rvert$$, showing $$\text{Range}(A - \lambda\mathbf{1})$$ is closed. A subspace of $$\mathbf{H}$$ that is both dense and closed equals $$\mathbf{H}$$ (its closure is both itself, by closedness, and all of $$\mathbf{H}$$, by density), so $$\text{Range}(A - \lambda\mathbf{1}) = \mathbf{H}$$.

We have shown that $$A - \lambda \mathbf{1}$$ maps $$\text{Dom}(A)$$ injectively onto $$\mathbf{H}$$; let $$B: \mathbf{H} \to \text{Dom}(A)$$ denote its (two-sided) inverse. For $$\psi \in \mathbf{H}$$, writing $$\psi = (A - \lambda\mathbf{1})\chi$$ for the unique $$\chi = B\psi \in \text{Dom}(A)$$, $$(\ast)$$ gives

$$
    \lvert b \rvert \left\| \chi \right\| \le \left\| (A - \lambda \mathbf{1})\chi \right\| = \left\| \psi \right\|,
$$

i.e. $$\lvert b \rvert \left\| B\psi \right\| \le \left\| \psi \right\|$$, so $$\left\| B\psi \right\| \le \tfrac{1}{\lvert b \rvert} \left\| \psi \right\|$$ for all $$\psi \in \mathbf{H}$$; that is, $$B$$ is a bounded operator, with $$B \in \mathcal{B}(\mathbf{H})$$. As $$B$$ is a bounded, everywhere-defined, two-sided inverse to $$A - \lambda \mathbf{1}$$, it satisfies both properties required by the [definition of the resolvent set](#def:hall-9.16), so $$\lambda$$ is in the resolvent set of $$A$$.

Since $$\lambda = a + ib$$ with $$b \ne 0$$ was an arbitrary non-real complex number, every non-real complex number lies in the resolvent set of $$A$$, so $$\sigma(A) \subset \mathbb{R}$$.$$\blacksquare$$

### Conditions for Self-Adjointness and Essential Self-Adjointness

We conclude the Chapter 9 scaffold with a criterion for essential self-adjointness in terms of the density of two ranges — this is the tool that will let us verify, later on, that certain concretely-defined operators built out of bounded self-adjoint pieces are essentially self-adjoint.

> **Theorem** *(Essential Self-Adjointness via Dense Range)*
<a name="thrm:hall-9.21"></a>
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{thrm:hall-9.17} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.8} -->
<!--  \uses{prpstn:hall-9.10} -->
<!--  \uses{prpstn:hall-9.12} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{prpstn:hall-9.14} -->
<!--  \uses{../spectral-theorems/#lmm:hall-7.8} -->
> If $$A$$ is a symmetric operator on $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint if and only if $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense subspaces of $$\mathbf{H}$$.

**Proof**
We first prove the forward direction, i.e. that if $$A$$ is essentially self-adjoint, then $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense in $$\mathbf{H}$$. Since $$A$$ is essentially self-adjoint, $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$A^* = (A^{\text{cl}})^* = A^{\text{cl}}$$, the last equality because $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12) and [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) (with $$B = i\mathbf{1}$$),

$$
    \left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \text{Ker}\left( (A - i\mathbf{1})^* \right) = \text{Ker}(A^* + i\mathbf{1}) = \text{Ker}(A^{\text{cl}} + i\mathbf{1}).
$$

Since $$A^{\text{cl}}$$ is self-adjoint, [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17) shows $$\sigma(A^{\text{cl}}) \subset \mathbb{R}$$, and since $$-i \notin \mathbb{R}$$, $$-i$$ is not in $$\sigma(A^{\text{cl}})$$, i.e. $$-i$$ is in the resolvent set of $$A^{\text{cl}}$$. By the [definition of the resolvent set](#def:hall-9.16), this gives a bounded two-sided inverse to $$A^{\text{cl}} + i\mathbf{1}$$, and an operator with a two-sided inverse is in particular injective, so $$\text{Ker}(A^{\text{cl}} + i\mathbf{1}) = \{0\}$$. Hence $$\left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \{0\}$$, i.e. $$\text{Range}(A - i\mathbf{1})$$ is dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ throughout shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$.

We now prove the reverse direction, i.e. that if $$A$$ is symmetric with $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ both dense in $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint. By [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), $$A$$ is closable, so $$A^{\text{cl}}$$ exists. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$(A^{\text{cl}})^* = A^*$$; and $$A^*$$ is a closed extension of the symmetric operator $$A$$ (closed by [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), an extension of $$A$$ by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4)), hence also an extension of the closure $$A^{\text{cl}}$$, by the [definition of closure](#def:hall-9.6) as the smallest closed extension. We check $$A^{\text{cl}}$$ is itself symmetric: for $$\xi, \eta \in \text{Dom}(A^{\text{cl}})$$, take sequences $$\{\xi_n\}, \{\eta_n\}$$ in $$\text{Dom}(A)$$ with $$\xi_n \to \xi$$, $$A\xi_n \to A^{\text{cl}}\xi$$ and $$\eta_n \to \eta$$, $$A\eta_n \to A^{\text{cl}}\eta$$, as furnished by the [definition of closure](#def:hall-9.6); symmetry of $$A$$ gives $$\left< \xi_n, A\eta_n \right> = \left< A\xi_n, \eta_n \right>$$ for every $$n$$, and [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — applicable since all four sequences $$\xi_n, A\xi_n, \eta_n, A\eta_n$$ converge — passes this to the limit, giving $$\left< \xi, A^{\text{cl}}\eta \right> = \left< A^{\text{cl}}\xi, \eta \right>$$, which is the [definition of symmetric](#def:hall-9.2) for $$A^{\text{cl}}$$.

Applying [**Lemma 7.8**](../spectral-theorems/#lmm:hall-7.8) — valid here for the same reason given in the proof of [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17), namely that its proof uses only symmetry — to $$A^{\text{cl}}$$ with $$\lambda = i$$ gives

$$
    \left\| \psi \right\|^2 \le \left\| (A^{\text{cl}} - i\mathbf{1})\psi \right\|^2 \tag{$\ast\ast$}
$$

for all $$\psi \in \text{Dom}(A^{\text{cl}})$$, so $$A^{\text{cl}} - i\mathbf{1}$$ is injective (by the same argument as in the proof of [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17)). Since $$A^{\text{cl}}$$ extends $$A$$, $$\text{Range}(A - i\mathbf{1}) \subset \text{Range}(A^{\text{cl}} - i\mathbf{1})$$; as the former is dense in $$\mathbf{H}$$, so is the latter. As $$A^{\text{cl}}$$ is closed, $$(\ast\ast)$$ lets us apply [Proposition (Closedness of the Range from a Lower Bound)](#prpstn:hall-9.14) with $$\varepsilon = 1$$, showing $$\text{Range}(A^{\text{cl}} - i\mathbf{1})$$ is closed; being both dense and closed, it equals $$\mathbf{H}$$. An identical argument, using density of $$\text{Range}(A + i\mathbf{1})$$, shows $$\text{Range}(A^{\text{cl}} + i\mathbf{1}) = \mathbf{H}$$ as well.

By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13), $$(A^{\text{cl}} - i\mathbf{1})^* = (A^{\text{cl}})^* + i\mathbf{1}$$; and since $$(A^{\text{cl}})^* = A^*$$ is an extension of $$A^{\text{cl}}$$, $$(A^{\text{cl}})^* + i\mathbf{1}$$ is an extension of $$A^{\text{cl}} + i\mathbf{1}$$. We claim this extension is not proper, i.e. that $$\text{Dom}\big( (A^{\text{cl}})^* + i\mathbf{1} \big) = \text{Dom}(A^{\text{cl}} + i\mathbf{1})$$. Suppose instead that $$\text{Dom}\big( (A^{\text{cl}})^* + i\mathbf{1} \big)$$ is strictly bigger. Since $$A^{\text{cl}} + i\mathbf{1}$$ already maps $$\text{Dom}(A^{\text{cl}})$$ onto $$\mathbf{H}$$ (shown above), for any $$\xi$$ in the strictly bigger domain but not in $$\text{Dom}(A^{\text{cl}})$$, surjectivity gives some $$\chi \in \text{Dom}(A^{\text{cl}})$$, necessarily $$\chi \ne \xi$$, with $$(A^{\text{cl}} + i\mathbf{1})\chi = \big( (A^{\text{cl}})^* + i\mathbf{1} \big)\xi$$; since $$(A^{\text{cl}})^* + i\mathbf{1}$$ agrees with $$A^{\text{cl}} + i\mathbf{1}$$ on $$\text{Dom}(A^{\text{cl}})$$, this reads $$\big( (A^{\text{cl}})^* + i\mathbf{1} \big)\chi = \big( (A^{\text{cl}})^* + i\mathbf{1} \big)\xi$$, so, by linearity, $$\big( (A^{\text{cl}})^* + i\mathbf{1} \big)(\xi - \chi) = 0$$ with $$\xi - \chi \ne 0$$. So $$(A^{\text{cl}})^* + i\mathbf{1}$$ has nontrivial kernel. But, by [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) once more,

$$
    (A^{\text{cl}})^* + i\mathbf{1} = A^* + i\mathbf{1} = (A - i\mathbf{1})^*.
$$

A nontrivial kernel for $$(A - i\mathbf{1})^*$$ means, by [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12), that $$\left( \text{Range}(A - i\mathbf{1}) \right)^\perp \ne \{0\}$$, contradicting density of $$\text{Range}(A - i\mathbf{1})$$.

We conclude $$(A^{\text{cl}})^* + i\mathbf{1} = A^{\text{cl}} + i\mathbf{1}$$, with equal domains. By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13), subtracting $$i\mathbf{1}$$ from both sides gives $$(A^{\text{cl}})^* = A^{\text{cl}}$$, with equal domains, i.e. $$A^{\text{cl}}$$ is self-adjoint. Since $$A$$ is symmetric and closable with $$A^{\text{cl}}$$ self-adjoint, $$A$$ is, by the [definition of essentially self-adjoint](#def:hall-9.7), essentially self-adjoint.$$\blacksquare$$

We close this section with a construction we will use directly in the proof of [Theorem 10.4](#thrm:hall-10.4): building an essentially self-adjoint operator on a Hilbert space direct sum out of bounded self-adjoint pieces on each summand.

> **Proposition** *(Direct Sums of Bounded Self-Adjoint Operators)*
<a name="prpstn:hall-9.26"></a>
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{prpstn:hall-9.10} -->
<!--  \uses{prpstn:hall-9.11} -->
<!--  \uses{thrm:hall-9.21} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-7.7} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$\mathbf{H}$$ is a Hilbert space direct sum of a sequence of separable Hilbert spaces $$\mathbf{H}_j$$:
>
> $$
>     \mathbf{H} = \bigoplus_{j=1}^\infty \mathbf{H}_j.
> $$
>
> Suppose $$A_j$$ is a bounded, [self-adjoint](#def:hall-9.5) operator on $$\mathbf{H}_j$$ for each $$j$$. Define a subspace $$V$$ of $$\mathbf{H}$$ by
>
> $$
>     V = \left\{ \psi = (\psi_1, \psi_2, \ldots) \;\middle|\; \sum_{j=1}^\infty \left( \left\| \psi_j \right\|_j^2 + \left\| A_j \psi_j \right\|_j^2 \right) < \infty \right\}.
> $$
>
> Suppose $$A$$ is a symmetric operator on $$\mathbf{H}$$ whose domain contains the finite direct sum $$W$$ of the $$\mathbf{H}_j$$'s (i.e. the sequences with only finitely many nonzero entries), and such that $$A \psi = (A_1 \psi_1, A_2 \psi_2, \ldots)$$ for $$\psi = (\psi_1, \psi_2, \ldots) \in W$$. Then $$A$$ is essentially self-adjoint, $$\text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = V$$, and
>
> $$
>     A^{\text{cl}}\psi = A^*\psi = (A_1 \psi_1, A_2 \psi_2, \ldots)
> $$
>
> for all $$\psi = (\psi_1, \psi_2, \ldots) \in V$$.

**Proof**
**Part 1: $$A$$ is essentially self-adjoint.** Fix $$j$$. Since $$A_j$$ is a bounded self-adjoint operator on $$\mathbf{H}_j$$, [Proposition (Spectrum of a Bounded Self-Adjoint Operator)](../spectral-theorems/#prpstn:hall-7.7) shows $$\sigma(A_j) \subset \mathbb{R}$$, so $$\pm i \notin \sigma(A_j)$$, i.e. $$\pm i$$ lie in the resolvent set of $$A_j$$: the bounded operators $$A_j \mp i\mathbf{1}$$ have bounded two-sided inverses, and an operator with a two-sided inverse is in particular surjective, so $$A_j \mp i\mathbf{1}$$ maps onto $$\mathbf{H}_j$$. Let $$\iota_j : \mathbf{H}_j \to \mathbf{H}$$ denote the isometric embedding of $$\mathbf{H}_j$$ as the $$j$$-th summand (all other coordinates zero); note $$\iota_j(\mathbf{H}_j) \subset W \subset \text{Dom}(A)$$, and, by hypothesis on $$A$$, $$A \iota_j(\eta) = \iota_j(A_j \eta)$$ for $$\eta \in \mathbf{H}_j$$. Hence, by linearity of $$A$$,

$$
    (A - i\mathbf{1}) \iota_j(\eta) = A\iota_j(\eta) - i\iota_j(\eta) = \iota_j(A_j \eta) - i\iota_j(\eta) = \iota_j\big( (A_j - i\mathbf{1})\eta \big),
$$

using linearity of $$\iota_j$$ for the last step. So $$\iota_j\big( \text{Range}(A_j - i\mathbf{1}) \big) \subset \text{Range}(A - i\mathbf{1})$$; since $$A_j - i\mathbf{1}$$ is surjective onto $$\mathbf{H}_j$$, this reads $$\iota_j(\mathbf{H}_j) \subset \text{Range}(A - i\mathbf{1})$$. As this holds for every $$j$$, and $$\text{Range}(A - i\mathbf{1})$$ is a subspace (by linearity of $$A - i\mathbf{1}$$ on $$\text{Dom}(A)$$), $$\text{Range}(A - i\mathbf{1})$$ contains every finite sum of elements from the $$\iota_j(\mathbf{H}_j)$$'s, i.e. $$W \subset \text{Range}(A - i\mathbf{1})$$. By the definition of the Hilbert space direct sum, $$W$$ is dense in $$\mathbf{H}$$, so $$\text{Range}(A - i\mathbf{1})$$ — being a superset of the dense subset $$W$$ — is itself dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$. Since $$A$$ is symmetric by hypothesis, [Theorem (Essential Self-Adjointness via Dense Range)](#thrm:hall-9.21) shows $$A$$ is essentially self-adjoint.

**Part 2: reduction to $$\text{Dom}(A) = W$$.** The argument of **Part 1**, applied verbatim to $$A\vert_W$$ in place of $$A$$ (it only used that $$\iota_j(\mathbf{H}_j) \subset W = \text{Dom}(A\vert_W)$$ and that $$A$$, hence $$A\vert_W$$, agrees with $$A_j$$ there), shows $$A\vert_W$$ is also essentially self-adjoint. Since $$A^{\text{cl}}$$ is a self-adjoint extension of $$A$$ (essential self-adjointness of $$A$$, from **Part 1**, means exactly that $$A^{\text{cl}}$$ is self-adjoint, and $$A^{\text{cl}}$$ extends $$A$$ by the [definition of closure](#def:hall-9.6)), and $$A$$ extends $$A\vert_W$$, so does $$A^{\text{cl}}$$; that is, $$A^{\text{cl}}$$ is a self-adjoint extension of $$A\vert_W$$. By [Proposition (Uniqueness of the Self-Adjoint Extension of an Essentially Self-Adjoint Operator)](#prpstn:hall-9.11) applied to the essentially self-adjoint operator $$A\vert_W$$, $$A^{\text{cl}}$$ must coincide with $$(A\vert_W)^{\text{cl}}$$, the unique self-adjoint extension of $$A\vert_W$$:

$$
    A^{\text{cl}} = (A\vert_W)^{\text{cl}}.
$$

By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10) applied to $$A$$, and separately to $$A\vert_W$$, together with self-adjointness of $$A^{\text{cl}}$$ and of $$(A\vert_W)^{\text{cl}}$$ (both established in **Part 1**, applied to $$A$$ and to $$A\vert_W$$ respectively),

$$
    A^* = (A^{\text{cl}})^* = A^{\text{cl}} = (A\vert_W)^{\text{cl}} = \big( (A\vert_W)^{\text{cl}} \big)^* = (A\vert_W)^*.
$$

So $$A^* = (A\vert_W)^*$$, and it suffices to compute the adjoint of $$A\vert_W$$ — that is, we may assume without loss of generality that $$\text{Dom}(A) = W$$.

**Part 3: $$\text{Dom}(A^*) = V$$, with the stated formula.** Assume now $$\text{Dom}(A) = W$$. We first show $$V \subset \text{Dom}(A^*)$$. Let $$\phi = (\phi_1, \phi_2, \ldots) \in V$$, and let $$\psi = (\psi_1, \ldots, \psi_N, 0, 0, \ldots) \in W$$ be arbitrary. Since each $$A_j$$ is self-adjoint (hence symmetric, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4)) on $$\mathbf{H}_j$$, and using the definition of the inner product on the direct sum $$\mathbf{H}$$ as the sum of the componentwise inner products,

$$
    \left< \phi, A\psi \right> = \sum_{j=1}^N \left< \phi_j, A_j \psi_j \right> = \sum_{j=1}^N \left< A_j \phi_j, \psi_j \right> = \left< (A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots), \psi \right>.
$$

By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) applied in $$\mathbf{H}$$ — valid since both $$(A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots)$$ and $$\psi$$ are elements of $$\mathbf{H}$$ —

$$
    \lvert \left< \phi, A\psi \right> \rvert \le \left\| (A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots) \right\| \left\| \psi \right\| = \left( \sum_{j=1}^N \left\| A_j \phi_j \right\|_j^2 \right)^{1/2} \left\| \psi \right\| \le \left( \sum_{j=1}^\infty \left\| A_j \phi_j \right\|_j^2 \right)^{1/2} \left\| \psi \right\|,
$$

and the right-most quantity is a finite constant since $$\phi \in V$$. Thus $$\psi \mapsto \left< \phi, A\psi \right>$$ is bounded on $$\text{Dom}(A) = W$$, so $$\phi \in \text{Dom}(A^*)$$ by the [definition of the adjoint](#def:hall-9.1). Moreover the computation above shows $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi \in W$$, where $$\chi = (A_1\phi_1, A_2\phi_2, \ldots)$$ — note $$\chi \in \mathbf{H}$$ since $$\sum_j \left\| A_j\phi_j \right\|_j^2 < \infty$$ — so, by uniqueness in the [definition of the adjoint](#def:hall-9.1), $$A^*\phi = \chi = (A_1\phi_1, A_2\phi_2, \ldots)$$, which is the claimed formula.

We now show $$\text{Dom}(A^*) \subset V$$. Let $$\phi = (\phi_1, \phi_2, \ldots) \in \text{Dom}(A^*)$$, so there is a constant $$C$$ with $$\lvert \left< \phi, A\psi \right> \rvert \le C \left\| \psi \right\|$$ for all $$\psi \in W$$. For each $$N$$, set $$\psi_N \equiv (A_1\phi_1, A_2\phi_2, \ldots, A_N\phi_N, 0, 0, \ldots) \in W$$ (a valid element of $$W$$ since each $$A_j\phi_j \in \mathbf{H}_j$$ and only finitely many entries are nonzero). Then, using self-adjointness of each $$A_j$$ as in the previous part,

$$
    \left< \phi, A\psi_N \right> = \sum_{j=1}^N \left< \phi_j, A_j(A_j\phi_j) \right> = \sum_{j=1}^N \left< A_j\phi_j, A_j\phi_j \right> = \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2,
$$

while $$\left\| \psi_N \right\| = \left( \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2 \right)^{1/2}$$. Boundedness of $$\psi \mapsto \left< \phi, A\psi \right>$$ gives

$$
    \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2 = \lvert \left< \phi, A\psi_N \right> \rvert \le C \left\| \psi_N \right\| = C \left( \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2 \right)^{1/2},
$$

so, dividing both sides by $$\left( \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2 \right)^{1/2}$$ when it is nonzero (the desired inequality below is trivial otherwise),

$$
    \left( \sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2 \right)^{1/2} \le C
$$

for every $$N$$. The partial sums $$\sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2$$ are non-decreasing in $$N$$ and bounded above by $$C^2$$, so a non-decreasing sequence of real numbers bounded above converges, giving $$\sum_{j=1}^\infty \left\| A_j\phi_j \right\|_j^2 < \infty$$. Since also $$\phi \in \mathbf{H} = \bigoplus_j \mathbf{H}_j$$ gives $$\sum_j \left\| \phi_j \right\|_j^2 < \infty$$ automatically, we conclude $$\phi \in V$$.

Combining both containments, $$\text{Dom}(A^*) = V$$, with $$A^*$$ given by the stated formula on $$V$$.

**Conclusion.** By **Part 2**, $$A^{\text{cl}} = A^*$$ (with equality of domains); by **Part 3**, $$\text{Dom}(A^*) = V$$ with $$A^*\psi = (A_1\psi_1, A_2\psi_2, \ldots)$$. Hence $$\text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = V$$ and $$A^{\text{cl}}\psi = A^*\psi = (A_1\psi_1, A_2\psi_2, \ldots)$$ for all $$\psi \in V$$, the desired result.$$\blacksquare$$
