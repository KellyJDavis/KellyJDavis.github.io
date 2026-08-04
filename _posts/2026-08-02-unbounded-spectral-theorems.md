---
title:  "Spectral Theorem for Unbounded, Self-Adjoint Operators"
date:   2026-08-02 19:30:00 +0200
categories: functional-analysis
---

Here we will state and prove the [**Spectral Theorem for Unbounded, Self-Adjoint Operators**](#thrm:hall-10.4). This theorem extends the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators) to the small handful of genuinely unbounded self-adjoint operators that do arise in AQFT — the momentum operator on Minkowski space is a standard example — even though the large majority of operators of interest there, local observables in particular, are bounded. It is a prerequisite for handling these unbounded operators within the rest of the AQFT work that motivated this series.

This post is a direct continuation of [Spectral Theorem for Bounded, Self-Adjoint Operators](../spectral-theorems), and depends on it: a number of the definitions, propositions, lemmas, and theorems proven there are reused here without repetition. Where this happens, we link directly to the relevant element in that post rather than restating it under a new name in this one.

As before, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

A note on conventions, extending the one given in the previous post. Results that are standard and whose proofs lie outside the scope of the development are, as before, stated in full but not proven, marked by the absence of an accompanying **Proof**. Every other result stated here — including everything below on unbounded operators — is proven in full, and every use of a prior result is made explicit, including a check that its hypotheses actually hold in the situation at hand. We do not assume the reader has already encountered unbounded operators: the relevant definitions are built up from scratch below, so that this post is self-contained modulo the previous one.

One more note, for a formalizer rather than a general reader: several proofs below pick a sequence, or a preimage, satisfying some property known only to exist (e.g. the approximating sequence in the [sequential characterization of a closure](#prpstn:closure-linearity-and-sequential-description), or a preimage $$\xi$$ with $$\eta = \mu(E)\xi$$ in the proof of [Lemma (Range Membership Concentrates the Associated Measure)](#lmm:range-membership-concentrates-measure)). These choices are all routine — nothing here needs a genuinely non-constructive selection principle beyond what dependent choice or `Classical.choice` already provides for sequences in a metric space — but they are choices, not constructions, and a formalizer should expect to reach for the corresponding Lean tactics rather than a constructive witness.

# Spectral Theorem: Unbounded Self-Adjoint Operators

We proceed in four stages. First, the basic theory of unbounded operators — adjoints, symmetry, self-adjointness, closedness, and the spectrum. Second, a theory of integrating an unbounded function against a projection-valued measure. Third, the spectral theorem for *bounded normal* operators. Finally, the Cayley transform, which lets us reduce the unbounded self-adjoint case to the bounded normal case and complete the proof.

## Unbounded Operators

### Adjoint and Closure of an Unbounded Operator

Recall from the [previous post](../spectral-theorems) that $$\mathbf{H}$$ denotes a separable, complex Hilbert space, and that $$\mathcal{B}(\mathbf{H})$$ denotes the set of bounded operators on $$\mathbf{H}$$. We now introduce operators that need not be bounded, and need not even be defined on all of $$\mathbf{H}$$; every definition and result below refers back to $$\mathbf{H}$$ in this fixed sense.

> **Definition** *(Unbounded Operator)*
<a name="def:hall-3.1"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> Let $$\mathbf{H}$$ be a separable, complex Hilbert space. An *unbounded operator* $$A$$ on $$\mathbf{H}$$ is a linear map $$A : \text{Dom}(A) \to \mathbf{H}$$, where $$\text{Dom}(A)$$, called the *domain* of $$A$$, is a dense subspace of $$\mathbf{H}$$. Here "unbounded" means "not necessarily bounded": we permit the case $$\text{Dom}(A) = \mathbf{H}$$ together with $$A \in \mathcal{B}(\mathbf{H})$$, the set of bounded operators on $$\mathbf{H}$$, but do not require it.

Before defining the adjoint of an unbounded operator, we record a small fact about dense subspaces that we will use repeatedly below — both to pin down the adjoint uniquely, and at several later points where we want to conclude that two vectors, or two operators, coincide from an equation that only holds on a dense subspace.

> **Lemma** *(Equality Testing on a Dense Subspace, First Slot)*
<a name="lmm:hall-dense-testing"></a>
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> Suppose $$\chi_1, \chi_2 \in \mathbf{H}$$ and $$D \subset \mathbf{H}$$ is a dense subset such that $$\left< \chi_1, \psi \right> = \left< \chi_2, \psi \right>$$ for all $$\psi \in D$$. Then $$\chi_1 = \chi_2$$.

**Proof**
Set $$\chi \equiv \chi_1 - \chi_2$$. For every $$\psi \in D$$, additivity of the inner product in its first argument (part of conjugate-linearity there) together with the hypothesis gives $$\left< \chi, \psi \right> = \left< \chi_1, \psi \right> - \left< \chi_2, \psi \right> = 0$$. Since $$D$$ is dense in $$\mathbf{H}$$, there is a sequence $$\{ \psi_n \}_{n \in \mathbb{N}}$$ in $$D$$ with $$\psi_n \to \chi$$. Fixing $$\chi$$ and applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) to this sequence,

$$
    \left< \chi, \chi \right> = \lim_{n \to \infty} \left< \chi, \psi_n \right> = \lim_{n \to \infty} 0 = 0.
$$

Since $$\mathbf{H}$$ is an inner product space, $$\left< \chi, \chi \right> = 0$$ forces $$\chi = 0$$, i.e. $$\chi_1 = \chi_2$$.$$\blacksquare$$

Several arguments below test equality of two vectors against a dense subset with the vectors sitting in the *second* slot of the inner product instead of the first — for instance, checking $$\left< \phi, \chi_1 \right> = \left< \phi, \chi_2 \right>$$ for all $$\phi$$ in some dense $$D$$. We record this as a second, separate lemma, bridged to the first by conjugate symmetry of the inner product.

> **Lemma** *(Equality Testing on a Dense Subspace, Second Slot)*
<a name="lmm:hall-dense-testing-second-slot"></a>
<!--  \uses{lmm:hall-dense-testing} -->
> Suppose $$\chi_1, \chi_2 \in \mathbf{H}$$ and $$D \subset \mathbf{H}$$ is a dense subset such that $$\left< \phi, \chi_1 \right> = \left< \phi, \chi_2 \right>$$ for all $$\phi \in D$$. Then $$\chi_1 = \chi_2$$.

**Proof**
Conjugating both sides of the hypothesis and using conjugate symmetry of the inner product, $$\left< \chi_1, \phi \right> = \overline{\left< \phi, \chi_1 \right>} = \overline{\left< \phi, \chi_2 \right>} = \left< \chi_2, \phi \right>$$ for all $$\phi \in D$$. This is exactly the hypothesis of [Lemma (Equality Testing on a Dense Subspace, First Slot)](#lmm:hall-dense-testing), which gives $$\chi_1 = \chi_2$$.$$\blacksquare$$

The construction of the adjoint below rests on the Hilbert-space self-duality theorem, distinct from the [**Riesz Representation Theorem**](../spectral-theorems/#thrm:riesz-representation) of the previous post (which represents positive linear functionals on $$C^0(X;\mathbb{R})$$, for $$X$$ a compact metric space, by a measure). The result we actually need is Hall's Theorem A.52, stated here for the first time in this series.

> **Theorem** *(Riesz Theorem)*
<a name="thrm:hall-a.52"></a>
> If $$\xi : \mathbf{H} \to \mathbb{C}$$ is a bounded linear functional, then there exists a unique $$\chi \in \mathbf{H}$$ such that
>
> $$
>     \xi(\psi) = \left< \chi, \psi \right>
> $$
>
> for all $$\psi \in \mathbf{H}$$. Furthermore, the operator norm of $$\xi$$ as a linear functional is equal to the norm of $$\chi$$ as an element of $$\mathbf{H}$$.

If $$A$$ happens to be a bounded operator on all of $$\mathbf{H}$$, then for any $$\phi \in \mathbf{H}$$ the linear functional $$\psi \mapsto \left< \phi, A\psi \right>$$ is automatically bounded, and the [**Riesz Theorem**](#thrm:hall-a.52) produces a unique $$\chi \in \mathbf{H}$$ with $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi$$; we then set $$A^*\phi \equiv \chi$$. If $$A$$ is genuinely unbounded, the functional $$\psi \mapsto \left< \phi, A\psi \right>$$ need not be bounded on $$\text{Dom}(A)$$ for every $$\phi$$ — but it may be bounded for *some* $$\phi$$, and it is exactly this set of $$\phi$$'s on which the adjoint gets defined.

> **Definition** *(Adjoint of an Unbounded Operator)*
<a name="def:hall-9.1"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{thrm:hall-a.52} -->
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

Now $$\tilde{T}$$ is a bounded linear functional on the Hilbert space $$\mathbf{H}$$, so the [**Riesz Theorem**](#thrm:hall-a.52) applies — its only hypothesis is exactly that $$\tilde{T}$$ be a bounded linear functional on a Hilbert space — and produces a unique $$\chi \in \mathbf{H}$$ with $$\tilde{T}\psi = \left< \chi, \psi \right>$$ for all $$\psi \in \mathbf{H}$$. In particular, restricting to $$\psi \in \text{Dom}(A)$$, where $$\tilde{T}$$ agrees with $$T$$,

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

Several proofs below establish $$\psi \in \text{Dom}(A^*)$$ by exhibiting a vector that represents $$\chi \mapsto \left< \psi, A\chi \right>$$ exactly, rather than checking boundedness directly against the definition. We record once, as a lemma, that this is a legitimate shortcut — the (easy) forward direction needs [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) to turn an exact representation into a boundedness statement — so that later proofs can cite it instead of silently re-deriving it.

> **Lemma** *(Characterizing Membership in the Adjoint's Domain)*
<a name="lmm:characterizing-adjoint-domain-membership"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$ and $$\psi \in \mathbf{H}$$. Then $$\psi \in \text{Dom}(A^*)$$ if and only if there exists $$\varphi \in \mathbf{H}$$ such that $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$; in that case, $$\varphi = A^*\psi$$.

**Proof**
If $$\psi \in \text{Dom}(A^*)$$, then $$\varphi = A^*\psi$$ satisfies the stated equation, directly by the [definition of the adjoint](#def:hall-9.1).

Conversely, suppose such a $$\varphi$$ exists. By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43), $$\lvert \left< \psi, A\chi \right> \rvert = \lvert \left< \varphi, \chi \right> \rvert \le \left\| \varphi \right\| \left\| \chi \right\|$$ for all $$\chi \in \text{Dom}(A)$$, so the map $$\chi \mapsto \left< \psi, A\chi \right>$$ is bounded, with bounding constant $$\left\| \varphi \right\|$$. By the [definition of the adjoint](#def:hall-9.1), this shows $$\psi \in \text{Dom}(A^*)$$; and, by uniqueness of the representing vector in that same definition, since $$\varphi$$ already satisfies the defining equation for $$A^*\psi$$, $$\varphi = A^*\psi$$.$$\blacksquare$$

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

The next two definitions let us make sense of the *closure* of an unbounded operator, which we will need almost immediately. First we fix the topology on $$\mathbf{H} \times \mathbf{H}$$: it is the Hilbert space with inner product $$\left< (\phi_1,\psi_1), (\phi_2,\psi_2) \right> \equiv \left< \phi_1,\phi_2 \right> + \left< \psi_1,\psi_2 \right>$$ and associated norm $$\left\| (\phi,\psi) \right\| \equiv \big( \left\| \phi \right\|^2 + \left\| \psi \right\|^2 \big)^{1/2}$$. Convergence in this norm is exactly componentwise convergence: if $$(\phi_n,\psi_n) \to (\phi,\psi)$$ then $$\left\| \phi_n - \phi \right\|^2 \le \left\| \phi_n-\phi \right\|^2 + \left\| \psi_n-\psi \right\|^2 = \left\| (\phi_n,\psi_n)-(\phi,\psi) \right\|^2 \to 0$$, so $$\phi_n \to \phi$$, and likewise $$\psi_n \to \psi$$; conversely, if $$\phi_n \to \phi$$ and $$\psi_n \to \psi$$ then $$\left\| (\phi_n,\psi_n)-(\phi,\psi) \right\|^2 = \left\| \phi_n-\phi \right\|^2 + \left\| \psi_n-\psi \right\|^2 \to 0$$. We also use the standard metric-space fact that a subset of $$\mathbf{H} \times \mathbf{H}$$ is closed exactly when it is sequentially closed (contains the limit of every convergent sequence of its own points), and that a point lies in the closure of a subset exactly when it is the limit of some sequence of points of that subset.

> **Definition** *(Closed and Closable Operators)*
<a name="def:hall-9.6"></a>
<!--  \uses{def:hall-3.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closed* if the graph of $$A$$ is a closed subset of $$\mathbf{H} \times \mathbf{H}$$. Equivalently — by sequential closedness, and componentwise convergence in $$\mathbf{H} \times \mathbf{H}$$, as just noted — $$A$$ is closed if and only if: whenever $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A)$$ and there exist $$\psi, \varphi \in \mathbf{H}$$ with $$\psi_n \to \psi$$ and $$A\psi_n \to \varphi$$, it follows that $$\psi \in \text{Dom}(A)$$ and $$A\psi = \varphi$$.
>
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closable* if the closure, in $$\mathbf{H} \times \mathbf{H}$$, of the graph of $$A$$ is again the graph of some operator. If $$A$$ is closable, the *closure* $$A^{\text{cl}}$$ of $$A$$ is the operator whose graph is the closure of the graph of $$A$$.

Two elementary facts about this closure — that it is automatically linear, and admits the same sequential description as $$A$$ itself — are needed repeatedly below, so we record and prove them immediately.

> **Proposition** *(Linearity and the Sequential Description of the Closure)*
<a name="prpstn:closure-linearity-and-sequential-description"></a>
<!--  \uses{def:hall-9.6} -->
> Suppose $$A$$ is a closable operator on $$\mathbf{H}$$.
>
> 1. $$A^{\text{cl}}$$ is linear, and $$\text{Dom}(A^{\text{cl}})$$ is a subspace of $$\mathbf{H}$$; in particular $$A^{\text{cl}}$$ is again an unbounded operator on $$\mathbf{H}$$ in the sense of [Definition (Unbounded Operator)](#def:hall-3.1).
> 2. For $$\xi \in \mathbf{H}$$: $$\xi \in \text{Dom}(A^{\text{cl}})$$ if and only if there is a sequence $$\{ \chi_n \}_{n \in \mathbb{N}}$$ in $$\text{Dom}(A)$$ with $$\chi_n \to \xi$$ and $$\{ A\chi_n \}_{n \in \mathbb{N}}$$ converging to some limit; in that case, the limit is $$A^{\text{cl}}\xi$$.
> 3. $$A^{\text{cl}}$$ is the smallest closed extension of $$A$$: it is itself a closed extension of $$A$$, and any closed extension of $$A$$ is in turn an extension of $$A^{\text{cl}}$$.

**Proof**
**Part 1.** The graph of $$A$$ is a linear subspace of $$\mathbf{H} \times \mathbf{H}$$: it contains $$(0,0) = (0, A0)$$, and for $$(\phi_1,A\phi_1), (\phi_2,A\phi_2)$$ in the graph and $$\alpha,\beta \in \mathbb{C}$$, linearity of $$A$$ gives $$\alpha(\phi_1,A\phi_1) + \beta(\phi_2,A\phi_2) = \big(\alpha\phi_1+\beta\phi_2,\ A(\alpha\phi_1+\beta\phi_2)\big)$$, again in the graph. The closure of a linear subspace of a normed vector space is again a linear subspace: if $$(\phi_1,\eta_1)$$ and $$(\phi_2,\eta_2)$$ are limits of sequences in the graph, then so is $$\alpha(\phi_1,\eta_1)+\beta(\phi_2,\eta_2)$$, being the limit of the corresponding linear combination of those sequences (using continuity of vector addition and scalar multiplication with respect to the norm — themselves immediate from the triangle inequality and homogeneity of the norm). So the graph of $$A^{\text{cl}}$$, being the closure of the graph of $$A$$, is a linear subspace of $$\mathbf{H} \times \mathbf{H}$$.

We now use this to show $$A^{\text{cl}}$$ is linear on a subspace domain. If $$\phi_1,\phi_2 \in \text{Dom}(A^{\text{cl}})$$ and $$\alpha,\beta \in \mathbb{C}$$, then $$(\phi_1,A^{\text{cl}}\phi_1)$$ and $$(\phi_2,A^{\text{cl}}\phi_2)$$ lie in the (linear) graph of $$A^{\text{cl}}$$, so $$\alpha(\phi_1,A^{\text{cl}}\phi_1) + \beta(\phi_2,A^{\text{cl}}\phi_2) = \big( \alpha\phi_1+\beta\phi_2,\ \alpha A^{\text{cl}}\phi_1 + \beta A^{\text{cl}}\phi_2 \big)$$ does too. This shows $$\alpha\phi_1+\beta\phi_2 \in \text{Dom}(A^{\text{cl}})$$ (so $$\text{Dom}(A^{\text{cl}})$$ is a subspace), and, since the graph of $$A^{\text{cl}}$$ is the graph of a *function* (by the [definition of closable](#def:hall-9.6), there is a unique second coordinate for each first coordinate), the second coordinate we just exhibited must be $$A^{\text{cl}}(\alpha\phi_1+\beta\phi_2)$$: that is, $$A^{\text{cl}}(\alpha\phi_1+\beta\phi_2) = \alpha A^{\text{cl}}\phi_1 + \beta A^{\text{cl}}\phi_2$$.

Finally, $$\text{Dom}(A^{\text{cl}})$$ is dense: the graph of $$A$$ is a subset of its own closure, i.e. of the graph of $$A^{\text{cl}}$$, so $$\text{Dom}(A) \subset \text{Dom}(A^{\text{cl}})$$; since $$\text{Dom}(A)$$ is already dense in $$\mathbf{H}$$ (by the [definition of an unbounded operator](#def:hall-3.1) applied to $$A$$), so is any superset of it, in particular $$\text{Dom}(A^{\text{cl}})$$. Together with linearity and the subspace domain just shown, this confirms $$A^{\text{cl}}$$ is again an unbounded operator on $$\mathbf{H}$$ in the sense of [Definition (Unbounded Operator)](#def:hall-3.1).

**Part 2.** By definition, the graph of $$A^{\text{cl}}$$ is the closure, in $$\mathbf{H} \times \mathbf{H}$$, of the graph of $$A$$. By the standard metric-space fact noted above, $$(\xi,\varphi)$$ lies in this closure exactly when it is the limit of a sequence $$\{ (\chi_n, A\chi_n) \}_{n\in\mathbb{N}}$$ of points of the graph of $$A$$ (i.e. $$\chi_n \in \text{Dom}(A)$$); by componentwise convergence in $$\mathbf{H}\times\mathbf{H}$$, also noted above, this means exactly $$\chi_n \to \xi$$ and $$A\chi_n \to \varphi$$. So $$\xi \in \text{Dom}(A^{\text{cl}})$$ (i.e. $$(\xi, A^{\text{cl}}\xi)$$ is in the graph of $$A^{\text{cl}}$$, for some — necessarily unique — value $$A^{\text{cl}}\xi$$) exactly when such a sequence exists, and in that case its limit $$\varphi$$ equals $$A^{\text{cl}}\xi$$.

**Part 3.** $$A^{\text{cl}}$$ is an extension of $$A$$: the graph of $$A$$ is a subset of its own closure, i.e. of the graph of $$A^{\text{cl}}$$. It is closed, since a closure is always a closed set. Suppose $$B$$ is any closed extension of $$A$$. Then the graph of $$B$$ is a closed set (as $$B$$ is closed) containing the graph of $$A$$ (as $$B$$ extends $$A$$), hence contains the closure of the graph of $$A$$, i.e. the graph of $$A^{\text{cl}}$$. This says exactly that $$B$$ is an extension of $$A^{\text{cl}}$$.$$\blacksquare$$

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

A remark on typing, before the first proposition of this section. [Definition (Unbounded Operator)](#def:hall-3.1) requires a dense domain, so strictly speaking, "closed" (as in [Definition (Closed and Closable Operators)](#def:hall-9.6)) is only defined for operators with dense domain. The adjoint $$A^*$$ of an unbounded operator $$A$$, however, need not itself have dense domain — nothing in [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1) guarantees this. The property of being closed — that the graph is a closed subset of $$\mathbf{H} \times \mathbf{H}$$ — is, on inspection, purely topological and makes sense for the graph of *any* linear map on *any* subspace of $$\mathbf{H}$$, dense or not; we use it below in exactly this more general sense whenever we ask whether $$A^*$$ is closed, without restating [Definition (Closed and Closable Operators)](#def:hall-9.6) for this broader class of objects. In every case where this document goes on to treat $$A^*$$ as a fully-fledged unbounded operator in its own right (in particular, taking a further adjoint $$(A^*)^*$$, which does require $$\text{Dom}(A^*)$$ to be dense), the operator $$A$$ in question is symmetric — so, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4) below, $$A^*$$ is an extension of $$A$$, and therefore automatically has dense domain (containing the already-dense $$\text{Dom}(A)$$). So the gap never bites in this post, though a fully general treatment would introduce two separate notions — linear maps on an arbitrary subspace, and the densely-defined ones among them — and track which results need which.

Our first observation is that the adjoint's graph is always closed, regardless of any hypothesis on $$A$$; from this, closability of symmetric operators follows immediately.

> **Proposition** *(Closedness of the Adjoint's Graph; Closability of Symmetric Operators)*
<a name="prpstn:hall-9.8"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> 1. If $$A$$ is an unbounded operator on $$\mathbf{H}$$, then the graph of $$A^*$$ (which may or may not be densely defined) is closed in $$\mathbf{H} \times \mathbf{H}$$.
> 2. A symmetric operator is always closable.

**Proof**
**Part 1:** Suppose $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A^*)$$ converging to some $$\psi \in \mathbf{H}$$, and suppose also that $$\{ A^*\psi_n \}_{n \in \mathbb{N}}$$ converges to some $$\varphi \in \mathbf{H}$$. By the [definition of the adjoint](#def:hall-9.1), $$\left< \psi_n, A\chi \right> = \left< A^*\psi_n, \chi \right>$$ for every $$\chi \in \text{Dom}(A)$$ and every $$n$$. Fix $$\chi \in \text{Dom}(A)$$. Applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — valid since $$\psi_n \to \psi$$ and $$A^*\psi_n \to \varphi$$ in $$\mathbf{H}$$ — to both sides of this equation,

$$
    \left< \psi, A\chi \right> = \lim_{n \to \infty} \left< \psi_n, A\chi \right> = \lim_{n \to \infty} \left< A^*\psi_n, \chi \right> = \left< \varphi, \chi \right>.
$$

As $$\chi \in \text{Dom}(A)$$ was arbitrary, this exhibits $$\varphi$$ as a vector with $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$, so [Lemma (Characterizing Membership in the Adjoint's Domain)](#lmm:characterizing-adjoint-domain-membership) gives $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = \varphi$$. By the [sequential characterization of closedness](#def:hall-9.6), this establishes that the graph of $$A^*$$ is closed, the desired **Part 1** result.

**Part 2:** Suppose $$A$$ is symmetric. By [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A^*$$ is an extension of $$A$$, so the graph of $$A$$ is a subset of the graph of $$A^*$$. By **Part 1**, the graph of $$A^*$$ is closed, so the closure of the graph of $$A$$ — being the smallest closed subset of $$\mathbf{H} \times \mathbf{H}$$ containing the graph of $$A$$ — is contained in the graph of $$A^*$$. A subset $$\Gamma$$ of the graph of a function is itself the graph of a function — namely, the restriction of that function to the projection of $$\Gamma$$ onto the first factor, since for each $$\phi$$ in that projection there is, by hypothesis $$\Gamma \subset \text{graph}(A^*)$$, exactly one $$\eta$$ with $$(\phi,\eta) \in \Gamma$$, namely $$\eta = A^*\phi$$. Applying this with $$\Gamma$$ the closure of the graph of $$A$$, that closure is the graph of a function (the restriction of $$A^*$$ to the projection of $$\Gamma$$ onto the first factor). By the [definition of closable](#def:hall-9.6), $$A$$ is closable, the desired **Part 2** result.$$\blacksquare$$

Having shown that closable operators are exactly those with a well-behaved closure, we record how the closure interacts with the adjoint: taking the adjoint of $$A$$ or of its closure $$A^{\text{cl}}$$ gives the same operator.

> **Proposition** *(The Adjoint of a Closure)*
<a name="prpstn:hall-9.10"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{prpstn:closure-linearity-and-sequential-description} -->
<!--  \uses{lmm:characterizing-adjoint-domain-membership} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> If $$A$$ is a closable operator on $$\mathbf{H}$$, then the adjoint of $$A^{\text{cl}}$$ coincides with the adjoint of $$A$$.

**Proof**
We prove $$\text{Dom}\big( (A^{\text{cl}})^* \big) \subset \text{Dom}(A^*)$$ and $$\text{Dom}(A^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big)$$ in turn, checking in each case that $$A^*$$ and $$(A^{\text{cl}})^*$$ agree.

**Part 1:** Suppose $$\psi \in \text{Dom}\big( (A^{\text{cl}})^* \big)$$, so that there is a $$\varphi \in \mathbf{H}$$ with $$\left< \psi, A^{\text{cl}}\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A^{\text{cl}})$$, by the [definition of the adjoint](#def:hall-9.1). Since $$A^{\text{cl}}$$ is an extension of $$A$$, in particular $$\text{Dom}(A) \subset \text{Dom}(A^{\text{cl}})$$ and $$A^{\text{cl}} = A$$ on $$\text{Dom}(A)$$, so this equation restricts to $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$. By [Lemma (Characterizing Membership in the Adjoint's Domain)](#lmm:characterizing-adjoint-domain-membership) applied to $$A$$, this shows $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = \varphi = (A^{\text{cl}})^*\psi$$.

**Part 2:** Suppose $$\psi \in \text{Dom}(A^*)$$, so that there is a $$\varphi \in \mathbf{H}$$ with $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$. Let $$\xi \in \text{Dom}(A^{\text{cl}})$$, with $$A^{\text{cl}}\xi = \eta$$. By Part 2 of [Proposition (Linearity and the Sequential Description of the Closure)](#prpstn:closure-linearity-and-sequential-description), there is a sequence $$\{ \chi_n \}_{n \in \mathbb{N}}$$ in $$\text{Dom}(A)$$ with $$\chi_n \to \xi$$ and $$A\chi_n \to \eta$$. For each $$n$$, $$\left< \psi, A\chi_n \right> = \left< \varphi, \chi_n \right>$$; letting $$n \to \infty$$ and applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — valid since $$\chi_n \to \xi$$ and $$A\chi_n \to \eta$$ — gives $$\left< \psi, \eta \right> = \left< \varphi, \xi \right>$$, i.e. $$\left< \psi, A^{\text{cl}}\xi \right> = \left< \varphi, \xi \right>$$. As $$\xi \in \text{Dom}(A^{\text{cl}})$$ was arbitrary, [Lemma (Characterizing Membership in the Adjoint's Domain)](#lmm:characterizing-adjoint-domain-membership) applied to $$A^{\text{cl}}$$ shows $$\psi \in \text{Dom}\big( (A^{\text{cl}})^* \big)$$ and $$(A^{\text{cl}})^*\psi = \varphi = A^*\psi$$.

Combining **Part 1** and **Part 2** gives $$\text{Dom}(A^*) = \text{Dom}\big( (A^{\text{cl}})^* \big)$$, with $$A^*$$ and $$(A^{\text{cl}})^*$$ agreeing on this common domain — the desired result.$$\blacksquare$$

When $$A$$ is essentially self-adjoint, its closure is not just *a* self-adjoint extension of $$A$$ — it is the *only* one, a fact we will use directly in the proof of [Proposition (Direct Sums of Bounded Self-Adjoint Operators)](#prpstn:hall-9.26) below.

The proof of the next proposition uses a general monotonicity fact about adjoints, worth recording separately since it recurs whenever comparing the adjoints of an operator and an extension of it.

> **Lemma** *(Extension Reverses Adjoint Domains)*
<a name="lmm:extension-reverses-adjoint-domains"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.3} -->
> If $$C_1$$ is an extension of $$C_2$$, then $$\text{Dom}(C_1^*) \subset \text{Dom}(C_2^*)$$, and $$C_1^*$$ and $$C_2^*$$ agree on $$\text{Dom}(C_1^*)$$.

**Proof**
Suppose $$\phi \in \text{Dom}(C_1^*)$$. By the [definition of the adjoint](#def:hall-9.1), the map $$\psi \mapsto \left< \phi, C_1\psi \right>$$ is bounded on $$\text{Dom}(C_1)$$, with some bounding constant $$K$$. Since $$C_1$$ is an extension of $$C_2$$, $$\text{Dom}(C_2) \subset \text{Dom}(C_1)$$ and $$C_1 = C_2$$ on $$\text{Dom}(C_2)$$, so the restriction of this map to $$\text{Dom}(C_2)$$ equals $$\psi \mapsto \left< \phi, C_2\psi \right>$$; being the restriction of a functional bounded on the larger set $$\text{Dom}(C_1)$$, it is bounded on the subset $$\text{Dom}(C_2)$$, with the same constant $$K$$. By the [definition of the adjoint](#def:hall-9.1) again, $$\phi \in \text{Dom}(C_2^*)$$.

Moreover, for such $$\phi$$, both $$C_1^*\phi$$ and $$C_2^*\phi$$ are, by the [definition of the adjoint](#def:hall-9.1), characterized as the unique vector $$\chi$$ with $$\left< \phi, C_i\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi \in \text{Dom}(C_i)$$; since $$C_1$$ and $$C_2$$ agree on $$\text{Dom}(C_2)$$, the defining equation for $$C_2^*\phi$$ is the restriction, to $$\text{Dom}(C_2) \subset \text{Dom}(C_1)$$, of the defining equation for $$C_1^*\phi$$, so both are satisfied by $$\chi = C_1^*\phi$$; by uniqueness in the definition applied to $$C_2$$, $$C_2^*\phi = C_1^*\phi$$.$$\blacksquare$$

> **Proposition** *(Uniqueness of the Self-Adjoint Extension of an Essentially Self-Adjoint Operator)*
<a name="prpstn:hall-9.11"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.3} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{prpstn:hall-9.8} -->
<!--  \uses{prpstn:closure-linearity-and-sequential-description} -->
<!--  \uses{lmm:extension-reverses-adjoint-domains} -->
> If $$A$$ is essentially self-adjoint, then $$A^{\text{cl}}$$ is the unique self-adjoint extension of $$A$$.

**Proof**
Suppose $$B$$ is a self-adjoint extension of $$A$$. Since $$B = B^*$$, [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8) shows $$B$$ is closed. As $$B$$ is a closed extension of $$A$$, Part 3 of [Proposition (Linearity and the Sequential Description of the Closure)](#prpstn:closure-linearity-and-sequential-description) shows it is an extension of $$A^{\text{cl}}$$; that is, $$\text{Dom}(A^{\text{cl}}) \subset \text{Dom}(B)$$.

Applying [Lemma (Extension Reverses Adjoint Domains)](#lmm:extension-reverses-adjoint-domains) with $$C_1 = B$$ and $$C_2 = A^{\text{cl}}$$ (recalling $$B$$ is an extension of $$A^{\text{cl}}$$) gives $$\text{Dom}(B^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big)$$. Thus we have

$$
    \text{Dom}(B^*) \subset \text{Dom}\big( (A^{\text{cl}})^* \big) \subset \text{Dom}(B),
$$

where the second containment is $$\text{Dom}(A^{\text{cl}}) \subset \text{Dom}(B)$$ from above, using that $$A$$ is essentially self-adjoint so $$(A^{\text{cl}})^* = A^{\text{cl}}$$. Since $$B$$ is self-adjoint, $$\text{Dom}(B^*) = \text{Dom}(B)$$, so all three sets above are equal:

$$
    \text{Dom}(B) = \text{Dom}(B^*) = \text{Dom}\big( (A^{\text{cl}})^* \big) = \text{Dom}(A^{\text{cl}}).
$$

As $$B$$ extends $$A^{\text{cl}}$$ and their domains coincide, $$B = A^{\text{cl}}$$.$$\blacksquare$$

We record next a description of $$\text{Ker}(A^*)$$ in terms of $$A$$ itself, generalizing the corresponding fact for bounded operators. First, since $$A$$ need not be defined on all of $$\mathbf{H}$$, we fix what $$\text{Range}(A)$$ means — and, since we are about to need orthogonal complements of subsets that are not the whole space, we fix that notion too, once and for all, rather than the informal shorthand $$\{\psi : \left<\psi,A\phi\right>=0 \text{ for all } \phi\}$$ sometimes used for bounded operators (where it happens to cause no harm, since there $$\text{Dom}(A) = \mathbf{H}$$, but would be wrong here, where $$\text{Dom}(A) \subsetneq \mathbf{H}$$ in general).

> **Definition** *(Orthogonal Complement)*
<a name="def:orthogonal-complement"></a>
> If $$V \subset \mathbf{H}$$ is any subset, its *orthogonal complement* is
>
> $$
>     V^\perp \equiv \{ \psi \in \mathbf{H} \mid \left< \psi, v \right> = 0 \text{ for all } v \in V \}.
> $$

> **Definition** *(Range of an Unbounded Operator)*
<a name="def:range-of-an-unbounded-operator"></a>
<!--  \uses{def:hall-3.1} -->
> If $$A$$ is an unbounded operator on $$\mathbf{H}$$, its *range* is $$\text{Range}(A) \equiv \{ A\psi \mid \psi \in \text{Dom}(A) \} \subset \mathbf{H}$$. Since $$\text{Dom}(A)$$ is a subspace of $$\mathbf{H}$$ and $$A$$ is linear, $$\text{Range}(A)$$ is again a subspace of $$\mathbf{H}$$: it contains $$0 = A0$$, and for $$A\psi_1, A\psi_2 \in \text{Range}(A)$$ and $$\alpha,\beta \in \mathbb{C}$$, linearity of $$A$$ gives $$\alpha A\psi_1 + \beta A\psi_2 = A(\alpha\psi_1+\beta\psi_2) \in \text{Range}(A)$$, as $$\alpha\psi_1+\beta\psi_2 \in \text{Dom}(A)$$. Unwinding [Definition (Orthogonal Complement)](#def:orthogonal-complement) for $$V = \text{Range}(A)$$: $$\left( \text{Range}(A) \right)^\perp = \{ \psi \in \mathbf{H} \mid \left< \psi, A\phi \right> = 0 \text{ for all } \phi \in \text{Dom}(A) \}$$ — the quantifier ranges over $$\text{Dom}(A)$$, not all of $$\mathbf{H}$$.

We will need two standard facts about closed subspaces of a Hilbert space at several points below, starting almost immediately; we import them together, as Hall does when he first needs them.

> **Proposition** *(Orthogonal Decomposition and the Double Complement)*
<a name="prpstn:hall-a.49"></a>
<!--  \uses{def:orthogonal-complement} -->
> 1. If $$V$$ is a closed subspace of $$\mathbf{H}$$, every $$\psi \in \mathbf{H}$$ decomposes uniquely as $$\psi = \psi_1 + \psi_2$$ with $$\psi_1 \in V$$ and $$\psi_2 \in V^\perp$$.
> 2. If $$V$$ is any subspace of $$\mathbf{H}$$, then $$(V^\perp)^\perp = \overline{V}$$, the closure of $$V$$. In particular, if $$V$$ is closed, $$(V^\perp)^\perp = V$$.

We record one immediate consequence of Part 2, in the form we will repeatedly need it: a subspace has trivial orthogonal complement exactly when it is dense.

> **Corollary** *(Trivial Complement Characterizes Density)*
<a name="crllr:trivial-complement-characterizes-density"></a>
<!--  \uses{prpstn:hall-a.49} -->
> A subspace $$V \subset \mathbf{H}$$ is dense in $$\mathbf{H}$$ if and only if $$V^\perp = \{0\}$$.

**Proof**
If $$V^\perp = \{0\}$$, then, by [Part 2 of **Proposition** *(hall-a.49)*](#prpstn:hall-a.49), $$\overline{V} = (V^\perp)^\perp = \{0\}^\perp = \mathbf{H}$$ — the last equality since $$\left< \psi, 0 \right> = 0$$ for every $$\psi \in \mathbf{H}$$, so every $$\psi$$ lies in $$\{0\}^\perp$$. Thus $$V$$ is dense.

Conversely, suppose $$V$$ is dense, i.e. $$\overline{V} = \mathbf{H}$$. Let $$\psi \in V^\perp$$, so $$\left< \psi, v \right> = 0$$ for all $$v \in V$$. Since $$\psi \in \mathbf{H} = \overline{V}$$, there is a sequence $$\{v_n\}$$ in $$V$$ with $$v_n \to \psi$$; by [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), $$\left< \psi, \psi \right> = \lim_n \left< \psi, v_n \right> = 0$$, so $$\psi = 0$$. Hence $$V^\perp = \{0\}$$.$$\blacksquare$$

> **Proposition** *(Orthogonal Complement of the Range)*
<a name="prpstn:hall-9.12"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:range-of-an-unbounded-operator} -->
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

The next proposition tells us how the adjoint interacts with adding a bounded operator, a computation we will need repeatedly below.

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

Applying the triangle inequality for complex numbers to the right-hand side, then [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) and boundedness of $$B$$ to the second term:

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

[Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) tells us how to add a bounded operator $$B$$ to $$A$$ and take the adjoint, but leaves $$B^*$$ itself as an unexplained ingredient whenever we specialize to $$B = \lambda\mathbf{1}$$ for a scalar $$\lambda \in \mathbb{C}$$ — a combination that will recur constantly (e.g. $$A - \lambda\mathbf{1}$$). We record the needed computation once.

> **Lemma** *(Adjoint of a Scalar Multiple of the Identity)*
<a name="lmm:adjoint-of-scalar-multiple-of-identity"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> For $$\lambda \in \mathbb{C}$$, the bounded operator $$\lambda\mathbf{1}$$ (defined on all of $$\mathbf{H}$$) has adjoint $$(\lambda\mathbf{1})^* = \overline{\lambda}\mathbf{1}$$.

**Proof**
For any $$\phi, \psi \in \mathbf{H}$$, using linearity of the inner product in its second argument,

$$
    \left< \phi, (\lambda\mathbf{1})\psi \right> = \left< \phi, \lambda\psi \right> = \lambda \left< \phi, \psi \right> = \left< \overline{\lambda}\phi, \psi \right>,
$$

the last equality by conjugate-linearity of the inner product in its first argument. As this holds for every $$\phi,\psi \in \mathbf{H} = \text{Dom}(\lambda\mathbf{1})$$, this is exactly the [definition of the adjoint](#def:hall-9.1): $$\text{Dom}\big((\lambda\mathbf{1})^*\big) = \mathbf{H}$$ and $$(\lambda\mathbf{1})^*\phi = \overline{\lambda}\phi$$ for every $$\phi$$, i.e. $$(\lambda\mathbf{1})^* = \overline{\lambda}\mathbf{1}$$.$$\blacksquare$$

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

We now come to a central result: the spectrum of a self-adjoint operator, bounded or not, is always contained in the real line. This is exactly the fact that will let us make sense of the Cayley transform, later in this post. The proof rests on an unbounded, merely-symmetric version of [**Lemma 7.8**](../spectral-theorems/#lmm:hall-7.8) of the previous post, which was stated and proved only for $$A \in \mathcal{B}(\mathbf{H})$$ self-adjoint. Its proof, in fact, only uses symmetry of $$A$$ — boundedness and the (stronger) self-adjointness hypothesis are never invoked beyond what symmetry already gives — but rather than reuse that result outside its stated hypotheses, we restate and reprove it here, for an unbounded symmetric operator, using the identical computation.

> **Lemma** *(The $$b^2$$ Inequality for Symmetric Operators)*
<a name="lmm:b-squared-inequality-symmetric"></a>
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> If $$A$$ is a symmetric operator on $$\mathbf{H}$$, then for all $$a, b \in \mathbb{R}$$ and associated $$\lambda \equiv a + ib \in \mathbb{C}$$,
>
> $$
>     \left< (A - \lambda\mathbf{1})\psi, (A - \lambda\mathbf{1})\psi \right> \ge b^2 \left< \psi, \psi \right>
> $$
>
> for all $$\psi \in \text{Dom}(A)$$.

**Proof**
Fix $$\psi \in \text{Dom}(A)$$. By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) with $$B = -a\mathbf{1}$$, $$A - a\mathbf{1}$$ has domain $$\text{Dom}(A)$$, and, since $$A$$ is symmetric and $$-a\mathbf{1}$$ is (trivially) symmetric with $$a$$ real, $$A - a\mathbf{1}$$ is again symmetric: for $$\phi, \chi \in \text{Dom}(A)$$, $$\left< \phi, (A-a\mathbf{1})\chi \right> = \left< \phi, A\chi \right> - a\left< \phi, \chi \right> = \left< A\phi, \chi \right> - a \left< \phi, \chi \right> = \left< (A-a\mathbf{1})\phi, \chi \right>$$, using symmetry of $$A$$ and reality of $$a$$. Applying this symmetry identity with $$\phi = \chi = \psi$$ gives, for our fixed $$\psi \in \text{Dom}(A)$$,

$$
    \left< \psi, (A-a\mathbf{1})\psi \right> = \left< (A-a\mathbf{1})\psi, \psi \right>.
$$

Writing $$(A - \lambda\mathbf{1})\psi = (A-a\mathbf{1})\psi - ib\psi$$ (immediate from $$\lambda = a+ib$$ and linearity), and expanding the inner product using linearity in the second argument and conjugate-linearity in the first,

$$
\begin{align}
    \left< (A-\lambda\mathbf{1})\psi, (A-\lambda\mathbf{1})\psi \right>
        &= \left< (A-a\mathbf{1})\psi - ib\psi,\ (A-a\mathbf{1})\psi - ib\psi \right> \\
        &= \left< (A-a\mathbf{1})\psi, (A-a\mathbf{1})\psi \right> - ib\left< \psi, (A-a\mathbf{1})\psi \right> + ib \left< (A-a\mathbf{1})\psi, \psi \right> + b^2 \left< \psi, \psi \right>.
\end{align}
$$

By the symmetry identity just established, the middle two terms cancel: $$-ib\left< \psi, (A-a\mathbf{1})\psi \right> + ib \left< (A-a\mathbf{1})\psi, \psi \right> = -ib\left< \psi, (A-a\mathbf{1})\psi \right> + ib \left< \psi, (A-a\mathbf{1})\psi \right> = 0$$. So

$$
    \left< (A-\lambda\mathbf{1})\psi, (A-\lambda\mathbf{1})\psi \right> = \left< (A-a\mathbf{1})\psi, (A-a\mathbf{1})\psi \right> + b^2 \left< \psi, \psi \right> \ge b^2 \left< \psi, \psi \right>,
$$

using positive-definiteness of the inner product for the last step.$$\blacksquare$$

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
<!--  \uses{lmm:b-squared-inequality-symmetric} -->
<!--  \uses{lmm:adjoint-of-scalar-multiple-of-identity} -->
<!--  \uses{crllr:trivial-complement-characterizes-density} -->
> If $$A$$ is an unbounded self-adjoint operator on $$\mathbf{H}$$, the spectrum of $$A$$ is contained in the real line.

**Proof**
Let $$\lambda = a + ib \in \mathbb{C}$$ with $$b \ne 0$$; we show $$\lambda$$ is in the resolvent set of $$A$$.

Since $$A$$ is [self-adjoint](#def:hall-9.5), $$A^*$$ is (trivially) an extension of $$A$$, so, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A$$ is symmetric. [**Lemma (The $$b^2$$ Inequality for Symmetric Operators)**](#lmm:b-squared-inequality-symmetric) gives

$$
    b^2 \left< \psi, \psi \right> \le \left< (A - \lambda \mathbf{1})\psi, (A - \lambda \mathbf{1})\psi \right> \tag{$\ast$}
$$

for all $$\psi \in \text{Dom}(A)$$. In particular, taking $$\psi \in \text{Dom}(A)$$ with $$(A - \lambda\mathbf{1})\psi = 0$$ forces $$b^2 \left< \psi, \psi \right> \le 0$$, hence $$\psi = 0$$ (as $$b \ne 0$$ and the inner product is positive definite); so $$A - \lambda \mathbf{1}$$ is injective.

Next we show $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$. By [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12) applied to $$A - \lambda \mathbf{1}$$,

$$
    \left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp = \text{Ker}\left( (A - \lambda \mathbf{1})^* \right).
$$

By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) with $$B = -\lambda \mathbf{1}$$ — a bounded operator on all of $$\mathbf{H}$$ — combined with [Lemma (Adjoint of a Scalar Multiple of the Identity)](#lmm:adjoint-of-scalar-multiple-of-identity) giving $$(-\lambda\mathbf{1})^* = -\overline{\lambda}\mathbf{1}$$, we get $$(A - \lambda\mathbf{1})^* = A^* + (-\lambda\mathbf{1})^* = A^* - \overline{\lambda}\mathbf{1} = A - \overline{\lambda}\mathbf{1}$$, using $$A^* = A$$. Since $$\overline{\lambda} = a - ib$$ also has $$b \ne 0$$ as its (negated) imaginary part, the argument of the previous paragraph applies verbatim with $$\overline{\lambda}$$ in place of $$\lambda$$ and shows $$A - \overline{\lambda}\mathbf{1}$$ is injective, i.e. $$\text{Ker}(A - \overline{\lambda}\mathbf{1}) = \{0\}$$. Hence

$$
    \left( \text{Range}(A - \lambda \mathbf{1}) \right)^\perp = \text{Ker}(A - \overline{\lambda}\mathbf{1}) = \{0\},
$$

so, by [Corollary (Trivial Complement Characterizes Density)](#crllr:trivial-complement-characterizes-density), $$\text{Range}(A - \lambda \mathbf{1})$$ is dense in $$\mathbf{H}$$.

Since $$A = A^*$$, [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8) shows $$A$$ is closed. Rewriting $$(\ast)$$ as $$\left\| (A - \lambda\mathbf{1})\psi \right\|^2 \ge b^2 \left\| \psi \right\|^2$$ and taking square roots, $$\lvert b \rvert \left\| \psi \right\| \le \left\| (A-\lambda\mathbf{1})\psi \right\|$$ for all $$\psi \in \text{Dom}(A)$$. This lets us apply [Proposition (Closedness of the Range from a Lower Bound)](#prpstn:hall-9.14) with $$\varepsilon = \lvert b \rvert$$, showing $$\text{Range}(A - \lambda\mathbf{1})$$ is closed. A subspace of $$\mathbf{H}$$ that is both dense and closed equals $$\mathbf{H}$$ (its closure is both itself, by closedness, and all of $$\mathbf{H}$$, by density), so $$\text{Range}(A - \lambda\mathbf{1}) = \mathbf{H}$$.

We have shown that $$A - \lambda \mathbf{1}$$ maps $$\text{Dom}(A)$$ bijectively onto $$\mathbf{H}$$ (injectively, from the first paragraph; onto $$\mathbf{H}$$, from $$\text{Range}(A-\lambda\mathbf{1}) = \mathbf{H}$$ just shown); let $$B : \mathbf{H} \to \text{Dom}(A)$$ denote its set-theoretic inverse, i.e. $$B\psi$$ is, for each $$\psi \in \mathbf{H}$$, the unique element of $$\text{Dom}(A)$$ with $$(A-\lambda\mathbf{1})(B\psi) = \psi$$.

We first check $$B$$ is linear. Fix $$\psi_1, \psi_2 \in \mathbf{H}$$ and $$\alpha, \beta \in \mathbb{C}$$, and set $$\chi_1 \equiv B\psi_1$$, $$\chi_2 \equiv B\psi_2 \in \text{Dom}(A)$$. Since $$\text{Dom}(A)$$ is a subspace, $$\alpha\chi_1 + \beta\chi_2 \in \text{Dom}(A)$$, and, by linearity of $$A - \lambda\mathbf{1}$$,

$$
    (A-\lambda\mathbf{1})(\alpha\chi_1+\beta\chi_2) = \alpha(A-\lambda\mathbf{1})\chi_1 + \beta(A-\lambda\mathbf{1})\chi_2 = \alpha\psi_1 + \beta\psi_2.
$$

By uniqueness of the preimage under the bijection $$A - \lambda\mathbf{1}$$, this identifies $$\alpha\chi_1+\beta\chi_2$$ as $$B(\alpha\psi_1+\beta\psi_2)$$, i.e. $$B(\alpha\psi_1+\beta\psi_2) = \alpha B\psi_1 + \beta B\psi_2$$. So $$B$$ is linear.

Next, for $$\psi \in \mathbf{H}$$, writing $$\psi = (A - \lambda\mathbf{1})\chi$$ for the unique $$\chi = B\psi \in \text{Dom}(A)$$, $$(\ast)$$ gives

$$
    \lvert b \rvert \left\| \chi \right\| \le \left\| (A - \lambda \mathbf{1})\chi \right\| = \left\| \psi \right\|,
$$

i.e. $$\lvert b \rvert \left\| B\psi \right\| \le \left\| \psi \right\|$$, so $$\left\| B\psi \right\| \le \tfrac{1}{\lvert b \rvert} \left\| \psi \right\|$$ for all $$\psi \in \mathbf{H}$$; combined with linearity just shown, $$B$$ is a bounded operator, with $$B \in \mathcal{B}(\mathbf{H})$$.

We now check $$B$$ satisfies both numbered conditions of the [definition of the resolvent set](#def:hall-9.16). For condition 1: for every $$\psi \in \mathbf{H}$$, $$B\psi \in \text{Dom}(A)$$ and $$(A-\lambda\mathbf{1})B\psi = \psi$$ — this is exactly how $$B\psi$$ was defined, as the (unique) element of $$\text{Dom}(A)$$ satisfying this equation. For condition 2: for $$\psi \in \text{Dom}(A)$$, we must check $$B(A-\lambda\mathbf{1})\psi = \psi$$. Since $$(A-\lambda\mathbf{1})\psi \in \mathbf{H}$$, $$B\big((A-\lambda\mathbf{1})\psi\big)$$ is, by definition of $$B$$, the unique element $$\chi \in \text{Dom}(A)$$ with $$(A-\lambda\mathbf{1})\chi = (A-\lambda\mathbf{1})\psi$$; since $$\psi \in \text{Dom}(A)$$ itself satisfies this equation, and $$A - \lambda\mathbf{1}$$ is injective (so the element $$\chi$$ with this property is unique), $$\chi = \psi$$, i.e. $$B(A-\lambda\mathbf{1})\psi = \psi$$. Both conditions hold, so $$\lambda$$ is in the resolvent set of $$A$$.

Since $$\lambda = a + ib$$ with $$b \ne 0$$ was an arbitrary non-real complex number, every non-real complex number lies in the resolvent set of $$A$$, so $$\sigma(A) \subset \mathbb{R}$$.$$\blacksquare$$

### Conditions for Self-Adjointness and Essential Self-Adjointness

We conclude this part of the development with a criterion for essential self-adjointness in terms of the density of two ranges — this is the tool that will let us verify, later on, that certain concretely-defined operators built out of bounded self-adjoint pieces are essentially self-adjoint.

> **Theorem** *(Essential Self-Adjointness via Dense Range)*
<a name="thrm:hall-9.21"></a>
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{thrm:hall-9.17} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.8} -->
<!--  \uses{prpstn:hall-9.10} -->
<!--  \uses{prpstn:hall-9.12} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{prpstn:hall-9.14} -->
<!--  \uses{prpstn:closure-linearity-and-sequential-description} -->
<!--  \uses{lmm:b-squared-inequality-symmetric} -->
<!--  \uses{lmm:adjoint-of-scalar-multiple-of-identity} -->
<!--  \uses{crllr:trivial-complement-characterizes-density} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> If $$A$$ is a symmetric operator on $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint if and only if $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense subspaces of $$\mathbf{H}$$.

**Proof**
We first prove the forward direction, i.e. that if $$A$$ is essentially self-adjoint, then $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense in $$\mathbf{H}$$. Since $$A$$ is essentially self-adjoint, $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$A^* = (A^{\text{cl}})^* = A^{\text{cl}}$$, the last equality because $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12) and [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) (with $$B = i\mathbf{1}$$, so $$B^* = -i\mathbf{1}$$ by [Lemma (Adjoint of a Scalar Multiple of the Identity)](#lmm:adjoint-of-scalar-multiple-of-identity)),

$$
    \left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \text{Ker}\left( (A - i\mathbf{1})^* \right) = \text{Ker}(A^* + i\mathbf{1}) = \text{Ker}(A^{\text{cl}} + i\mathbf{1}).
$$

Since $$A^{\text{cl}}$$ is self-adjoint, [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17) shows $$\sigma(A^{\text{cl}}) \subset \mathbb{R}$$, and since $$-i \notin \mathbb{R}$$, $$-i$$ is not in $$\sigma(A^{\text{cl}})$$, i.e. $$-i$$ is in the resolvent set of $$A^{\text{cl}}$$. By the [definition of the resolvent set](#def:hall-9.16), this gives a bounded two-sided inverse to $$A^{\text{cl}} + i\mathbf{1}$$, and an operator with a two-sided inverse is in particular injective, so $$\text{Ker}(A^{\text{cl}} + i\mathbf{1}) = \{0\}$$. Hence $$\left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \{0\}$$, so, by [Corollary (Trivial Complement Characterizes Density)](#crllr:trivial-complement-characterizes-density), $$\text{Range}(A - i\mathbf{1})$$ is dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ throughout shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$.

We now prove the reverse direction, i.e. that if $$A$$ is symmetric with $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ both dense in $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint. By [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), $$A$$ is closable, so $$A^{\text{cl}}$$ exists. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$(A^{\text{cl}})^* = A^*$$; and $$A^*$$ is a closed extension of the symmetric operator $$A$$ (closed by [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), an extension of $$A$$ by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4)), hence also an extension of the closure $$A^{\text{cl}}$$, by Part 3 of [Proposition (Linearity and the Sequential Description of the Closure)](#prpstn:closure-linearity-and-sequential-description). We check $$A^{\text{cl}}$$ is itself symmetric: for $$\xi, \eta \in \text{Dom}(A^{\text{cl}})$$, take sequences $$\{\xi_n\}, \{\eta_n\}$$ in $$\text{Dom}(A)$$ with $$\xi_n \to \xi$$, $$A\xi_n \to A^{\text{cl}}\xi$$ and $$\eta_n \to \eta$$, $$A\eta_n \to A^{\text{cl}}\eta$$, as furnished by Part 2 of the same proposition; symmetry of $$A$$ gives $$\left< \xi_n, A\eta_n \right> = \left< A\xi_n, \eta_n \right>$$ for every $$n$$, and [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — applicable since all four sequences $$\xi_n, A\xi_n, \eta_n, A\eta_n$$ converge — passes this to the limit, giving $$\left< \xi, A^{\text{cl}}\eta \right> = \left< A^{\text{cl}}\xi, \eta \right>$$, which is the [definition of symmetric](#def:hall-9.2) for $$A^{\text{cl}}$$.

Applying [**Lemma (The $$b^2$$ Inequality for Symmetric Operators)**](#lmm:b-squared-inequality-symmetric) — applicable since $$A^{\text{cl}}$$ is symmetric, shown above — with $$\lambda = i$$ (i.e. $$a=0$$, $$b=1$$) gives

$$
    \left\| \psi \right\|^2 \le \left\| (A^{\text{cl}} - i\mathbf{1})\psi \right\|^2 \tag{$\ast\ast$}
$$

for all $$\psi \in \text{Dom}(A^{\text{cl}})$$, so $$A^{\text{cl}} - i\mathbf{1}$$ is injective (by the same argument as in the proof of [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17)). Since $$A^{\text{cl}}$$ extends $$A$$, $$\text{Range}(A - i\mathbf{1}) \subset \text{Range}(A^{\text{cl}} - i\mathbf{1})$$; as the former is dense in $$\mathbf{H}$$, so is the latter. As $$A^{\text{cl}}$$ is closed, $$(\ast\ast)$$ lets us apply [Proposition (Closedness of the Range from a Lower Bound)](#prpstn:hall-9.14) with $$\varepsilon = 1$$, showing $$\text{Range}(A^{\text{cl}} - i\mathbf{1})$$ is closed; being both dense and closed, it equals $$\mathbf{H}$$. An identical argument, using density of $$\text{Range}(A + i\mathbf{1})$$, shows $$\text{Range}(A^{\text{cl}} + i\mathbf{1}) = \mathbf{H}$$ as well.

By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13), $$(A^{\text{cl}} - i\mathbf{1})^* = (A^{\text{cl}})^* + i\mathbf{1}$$; and since $$(A^{\text{cl}})^* = A^*$$ is an extension of $$A^{\text{cl}}$$, $$(A^{\text{cl}})^* + i\mathbf{1}$$ is an extension of $$A^{\text{cl}} + i\mathbf{1}$$. We claim this extension is not proper, i.e. that $$\text{Dom}\big( (A^{\text{cl}})^* + i\mathbf{1} \big) = \text{Dom}(A^{\text{cl}} + i\mathbf{1})$$. Suppose instead that $$\text{Dom}\big( (A^{\text{cl}})^* + i\mathbf{1} \big)$$ is strictly bigger. Since $$A^{\text{cl}} + i\mathbf{1}$$ already maps $$\text{Dom}(A^{\text{cl}})$$ onto $$\mathbf{H}$$ (shown above), for any $$\xi$$ in the strictly bigger domain but not in $$\text{Dom}(A^{\text{cl}})$$, surjectivity gives some $$\chi \in \text{Dom}(A^{\text{cl}})$$, necessarily $$\chi \ne \xi$$, with $$(A^{\text{cl}} + i\mathbf{1})\chi = \big( (A^{\text{cl}})^* + i\mathbf{1} \big)\xi$$; since $$(A^{\text{cl}})^* + i\mathbf{1}$$ agrees with $$A^{\text{cl}} + i\mathbf{1}$$ on $$\text{Dom}(A^{\text{cl}})$$, this reads $$\big( (A^{\text{cl}})^* + i\mathbf{1} \big)\chi = \big( (A^{\text{cl}})^* + i\mathbf{1} \big)\xi$$, so, by linearity, $$\big( (A^{\text{cl}})^* + i\mathbf{1} \big)(\xi - \chi) = 0$$ with $$\xi - \chi \ne 0$$. So $$(A^{\text{cl}})^* + i\mathbf{1}$$ has nontrivial kernel. But, by [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) once more,

$$
    (A^{\text{cl}})^* + i\mathbf{1} = A^* + i\mathbf{1} = (A - i\mathbf{1})^*.
$$

A nontrivial kernel for $$(A - i\mathbf{1})^*$$ means, by [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12), that $$\left( \text{Range}(A - i\mathbf{1}) \right)^\perp \ne \{0\}$$, contradicting density of $$\text{Range}(A - i\mathbf{1})$$ by [Corollary (Trivial Complement Characterizes Density)](#crllr:trivial-complement-characterizes-density).

We conclude $$(A^{\text{cl}})^* + i\mathbf{1} = A^{\text{cl}} + i\mathbf{1}$$, with equal domains. Equal domains means $$\text{Dom}\big((A^{\text{cl}})^*\big) = \text{Dom}(A^{\text{cl}})$$; and, writing $$D$$ for this common domain, equality of the two operators means $$(A^{\text{cl}})^*\psi + i\psi = A^{\text{cl}}\psi + i\psi$$ for every $$\psi \in D$$, directly from the pointwise definition of the sum of an operator with $$i\mathbf{1}$$. Subtracting $$i\psi$$ from both sides (ordinary vector subtraction in $$\mathbf{H}$$) gives $$(A^{\text{cl}})^*\psi = A^{\text{cl}}\psi$$ for every $$\psi \in D$$. Together with the equal domains just noted, this is exactly $$(A^{\text{cl}})^* = A^{\text{cl}}$$, i.e. $$A^{\text{cl}}$$ is self-adjoint. Since $$A$$ is symmetric and closable with $$A^{\text{cl}}$$ self-adjoint, $$A$$ is, by the [definition of essentially self-adjoint](#def:hall-9.7), essentially self-adjoint.$$\blacksquare$$

We close this section with a construction we will use directly in the proof of [Theorem 10.4](#thrm:hall-10.4): building an essentially self-adjoint operator on a Hilbert space direct sum out of bounded self-adjoint pieces on each summand. This uses the notion of a Hilbert space direct sum, which neither post has needed until now; we import it directly from Hall's appendix.

> **Definition** *(Hilbert Space Direct Sum)*
<a name="def:hall-a.45"></a>
> Suppose $$\{ \mathbf{H}_j \}_{j=1}^\infty$$ is a sequence of separable Hilbert spaces. Then the *Hilbert space direct sum*, denoted
>
> $$
>     \mathbf{H} \equiv \bigoplus_{j=1}^\infty \mathbf{H}_j,
> $$
>
> is the space of sequences $$\psi = (\psi_1, \psi_2, \psi_3, \ldots)$$ with $$\psi_j \in \mathbf{H}_j$$ and
>
> $$
>     \left\| \psi \right\|^2 \equiv \sum_{j=1}^\infty \left\| \psi_j \right\|_j^2 < \infty.
> $$
>
> The *finite direct sum* of the $$\mathbf{H}_j$$'s is the subspace of $$\psi = (\psi_1, \psi_2, \ldots)$$ with $$\psi_j = 0$$ for all but finitely many $$j$$. An inner product on $$\mathbf{H}$$ is defined by
>
> $$
>     \left< \phi, \psi \right> \equiv \sum_{j=1}^\infty \left< \phi_j, \psi_j \right>_j.
> $$
>
> This inner product is well defined, and $$\mathbf{H}$$ is complete with respect to it; hence $$\mathbf{H}$$, with this inner product, is itself a separable, complex Hilbert space. The finite direct sum is dense in $$\mathbf{H}$$: for $$\psi \in \mathbf{H}$$, the truncations $$\psi^{(N)} \equiv (\psi_1, \ldots, \psi_N, 0, 0, \ldots)$$ lie in the finite direct sum and satisfy $$\left\| \psi - \psi^{(N)} \right\|^2 = \sum_{j > N} \left\| \psi_j \right\|_j^2 \to 0$$ as $$N \to \infty$$, being the tail of the convergent series defining $$\left\| \psi \right\|^2$$.

The direct sum just defined is an *external* construction: its elements are sequences, and the summands $$\mathbf{H}_j$$ are separate spaces glued together. In practice we more often meet the *internal* situation: a single Hilbert space $$\mathbf{H}$$ together with a family of closed subspaces of $$\mathbf{H}$$ that decompose it. These are not literally the same object, so we record the notion and the identification between the two explicitly rather than passing between them silently.

> **Definition** *(Internal Orthogonal Decomposition)*
<a name="def:internal-orthogonal-decomposition"></a>
<!--  \uses{def:orthogonal-complement} -->
> A sequence $$\{ \mathbf{K}_n \}_{n=1}^\infty$$ of closed subspaces of $$\mathbf{H}$$ is an *internal orthogonal decomposition* of $$\mathbf{H}$$ if
>
> 1. the subspaces are pairwise orthogonal: $$\left< \eta, \zeta \right> = 0$$ whenever $$\eta \in \mathbf{K}_n$$, $$\zeta \in \mathbf{K}_m$$ with $$n \ne m$$; and
> 2. every $$\psi \in \mathbf{H}$$ can be written as $$\psi = \sum_{n=1}^\infty \psi_n$$ with $$\psi_n \in \mathbf{K}_n$$, the series converging in the norm of $$\mathbf{H}$$.

> **Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*
<a name="lmm:internal-decomposition-unitary"></a>
<!--  \uses{def:internal-orthogonal-decomposition} -->
<!--  \uses{def:hall-a.45} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> Suppose $$\{ \mathbf{K}_n \}_{n=1}^\infty$$ is an internal orthogonal decomposition of $$\mathbf{H}$$, with each $$\mathbf{K}_n$$ separable. Then:
>
> 1. The decomposition in Part 2 of [Definition (Internal Orthogonal Decomposition)](#def:internal-orthogonal-decomposition) is unique: if $$\sum_n \psi_n = \sum_n \psi_n'$$ with $$\psi_n, \psi_n' \in \mathbf{K}_n$$ (both series norm-convergent), then $$\psi_n = \psi_n'$$ for every $$n$$.
> 2. $$\left\| \psi \right\|^2 = \sum_{n=1}^\infty \left\| \psi_n \right\|^2$$ for every $$\psi \in \mathbf{H}$$, where $$\psi = \sum_n \psi_n$$ is its decomposition.
> 3. The map $$U : \mathbf{H} \to \bigoplus_{n=1}^\infty \mathbf{K}_n$$ (external direct sum, as in [Definition (Hilbert Space Direct Sum)](#def:hall-a.45)) given by $$U\psi \equiv (\psi_1, \psi_2, \ldots)$$ is a well-defined linear bijection preserving the inner product, i.e. a unitary map.

**Proof**
**Part 2 first.** Let $$\psi = \sum_n \psi_n$$ with $$\psi_n \in \mathbf{K}_n$$, and write $$\psi^{(N)} \equiv \sum_{n=1}^N \psi_n$$, so $$\psi^{(N)} \to \psi$$ in norm. By pairwise orthogonality (Part 1 of the definition), expanding the finite sum,

$$
    \left\| \psi^{(N)} \right\|^2 = \left< \sum_{n=1}^N \psi_n, \sum_{m=1}^N \psi_m \right> = \sum_{n=1}^N \sum_{m=1}^N \left< \psi_n, \psi_m \right> = \sum_{n=1}^N \left\| \psi_n \right\|^2,
$$

all cross terms ($$n\ne m$$) vanishing. Since $$\psi^{(N)} \to \psi$$, [continuity of the norm](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) gives $$\left\| \psi^{(N)} \right\|^2 \to \left\| \psi \right\|^2$$, so the partial sums $$\sum_{n=1}^N \left\| \psi_n \right\|^2$$ converge to $$\left\| \psi \right\|^2$$; that is, $$\sum_{n=1}^\infty \left\| \psi_n \right\|^2 = \left\| \psi \right\|^2$$.

**Part 1.** Suppose $$\sum_n \psi_n = \sum_n \psi_n'$$, both norm-convergent with $$n$$-th terms in $$\mathbf{K}_n$$. Set $$\chi_n \equiv \psi_n - \psi_n' \in \mathbf{K}_n$$ (a subspace); then $$\sum_n \chi_n = 0$$, norm-convergent, since the difference of two convergent series converges to the difference of their sums. Applying **Part 2** to the vector $$0$$ with this decomposition, $$0 = \left\| 0 \right\|^2 = \sum_n \left\| \chi_n \right\|^2$$, a sum of non-negative terms; hence $$\left\| \chi_n \right\| = 0$$, i.e. $$\psi_n = \psi_n'$$, for every $$n$$.

**Part 3.** *Well defined:* for $$\psi \in \mathbf{H}$$, Part 2 of the definition supplies a decomposition $$\psi = \sum_n \psi_n$$; **Part 1** shows it is unique, so $$U\psi = (\psi_1,\psi_2,\ldots)$$ is unambiguous. **Part 2** gives $$\sum_n \left\| \psi_n \right\|^2 = \left\| \psi \right\|^2 < \infty$$, so the sequence $$(\psi_1,\psi_2,\ldots)$$ does lie in the external direct sum, by [Definition (Hilbert Space Direct Sum)](#def:hall-a.45).

*Linear:* if $$\psi = \sum_n \psi_n$$ and $$\phi = \sum_n \phi_n$$ are the decompositions of $$\psi,\phi$$ and $$\alpha,\beta \in \mathbb{C}$$, then $$\alpha\psi + \beta\phi = \sum_n (\alpha\psi_n + \beta\phi_n)$$ (norm-convergent, as a linear combination of convergent series), with $$\alpha\psi_n+\beta\phi_n \in \mathbf{K}_n$$; by uniqueness (**Part 1**) this *is* the decomposition of $$\alpha\psi+\beta\phi$$, so $$U(\alpha\psi+\beta\phi) = \alpha U\psi + \beta U\phi$$.

*Injective:* if $$U\psi = 0$$ then every $$\psi_n = 0$$, so $$\psi = \sum_n \psi_n = 0$$.

*Surjective:* let $$(\eta_1,\eta_2,\ldots)$$ be an element of the external direct sum, so $$\eta_n \in \mathbf{K}_n$$ with $$\sum_n \left\| \eta_n \right\|^2 < \infty$$. The partial sums $$S_N \equiv \sum_{n=1}^N \eta_n$$ form a Cauchy sequence in $$\mathbf{H}$$: for $$N < M$$, pairwise orthogonality gives $$\left\| S_M - S_N \right\|^2 = \sum_{n=N+1}^M \left\| \eta_n \right\|^2$$, the tail of a convergent series, which tends to $$0$$ as $$N,M\to\infty$$. By completeness of $$\mathbf{H}$$, $$S_N \to \eta$$ for some $$\eta \in \mathbf{H}$$, i.e. $$\eta = \sum_n \eta_n$$ with $$\eta_n \in \mathbf{K}_n$$; by uniqueness this is the decomposition of $$\eta$$, so $$U\eta = (\eta_1,\eta_2,\ldots)$$.

*Inner-product preserving:* for $$\psi,\phi \in \mathbf{H}$$ with decompositions $$\sum_n\psi_n$$, $$\sum_n\phi_n$$, [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) applied to the partial sums, together with pairwise orthogonality killing all cross terms in each finite double sum, gives

$$
    \left< \psi, \phi \right> = \lim_{N\to\infty} \left< \sum_{n=1}^N \psi_n, \sum_{m=1}^N \phi_m \right> = \lim_{N\to\infty} \sum_{n=1}^N \left< \psi_n, \phi_n \right> = \sum_{n=1}^\infty \left< \psi_n, \phi_n \right> = \left< U\psi, U\phi \right>,
$$

the last equality being the definition of the inner product on the external direct sum. So $$U$$ is unitary.$$\blacksquare$$

With the identification in hand, we can restate [**Proposition** *(Direct Sums of Bounded Self-Adjoint Operators)*](#prpstn:hall-9.26) — which is phrased for the external direct sum — in the internal form in which we will actually apply it, transporting along $$U$$ rather than leaving the transport implicit. We state it here and prove it once [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) itself is available, immediately below.

> **Proposition** *(Direct Sums of Bounded Self-Adjoint Operators)*
<a name="prpstn:hall-9.26"></a>
<!--  \uses{def:hall-a.45} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.3} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.10} -->
<!--  \uses{prpstn:hall-9.11} -->
<!--  \uses{prpstn:closure-linearity-and-sequential-description} -->
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
> Suppose $$A$$ is a symmetric operator on $$\mathbf{H}$$ whose domain contains the finite direct sum $$W_0$$ of the $$\mathbf{H}_j$$'s (i.e. the sequences with only finitely many nonzero entries), and such that $$A \psi = (A_1 \psi_1, A_2 \psi_2, \ldots)$$ for $$\psi = (\psi_1, \psi_2, \ldots) \in W_0$$. Then $$A$$ is essentially self-adjoint, $$\text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = V$$, and
>
> $$
>     A^{\text{cl}}\psi = A^*\psi = (A_1 \psi_1, A_2 \psi_2, \ldots)
> $$
>
> for all $$\psi = (\psi_1, \psi_2, \ldots) \in V$$.

**Proof**
**Part 1: $$A$$ is essentially self-adjoint.** Fix $$j$$. Since $$A_j$$ is a bounded self-adjoint operator on $$\mathbf{H}_j$$, [Proposition (Spectrum of a Bounded Self-Adjoint Operator)](../spectral-theorems/#prpstn:hall-7.7) shows $$\sigma(A_j) \subset \mathbb{R}$$, so $$\pm i \notin \sigma(A_j)$$, i.e. $$\pm i$$ lie in the resolvent set of $$A_j$$: the bounded operators $$A_j \mp i\mathbf{1}$$ have bounded two-sided inverses, and an operator with a two-sided inverse is in particular surjective, so $$A_j \mp i\mathbf{1}$$ maps onto $$\mathbf{H}_j$$. Let $$\iota_j : \mathbf{H}_j \to \mathbf{H}$$ denote the isometric embedding of $$\mathbf{H}_j$$ as the $$j$$-th summand (all other coordinates zero); note $$\iota_j(\mathbf{H}_j) \subset W_0 \subset \text{Dom}(A)$$, and, by hypothesis on $$A$$, $$A \iota_j(\eta) = \iota_j(A_j \eta)$$ for $$\eta \in \mathbf{H}_j$$. Hence, by linearity of $$A$$,

$$
    (A - i\mathbf{1}) \iota_j(\eta) = A\iota_j(\eta) - i\iota_j(\eta) = \iota_j(A_j \eta) - i\iota_j(\eta) = \iota_j\big( (A_j - i\mathbf{1})\eta \big),
$$

using linearity of $$\iota_j$$ for the last step. So $$\iota_j\big( \text{Range}(A_j - i\mathbf{1}) \big) \subset \text{Range}(A - i\mathbf{1})$$; since $$A_j - i\mathbf{1}$$ is surjective onto $$\mathbf{H}_j$$, this reads $$\iota_j(\mathbf{H}_j) \subset \text{Range}(A - i\mathbf{1})$$. As this holds for every $$j$$, and $$\text{Range}(A - i\mathbf{1})$$ is a subspace (by linearity of $$A - i\mathbf{1}$$ on $$\text{Dom}(A)$$), $$\text{Range}(A - i\mathbf{1})$$ contains every finite sum of elements from the $$\iota_j(\mathbf{H}_j)$$'s, i.e. $$W_0 \subset \text{Range}(A - i\mathbf{1})$$. By the definition of the Hilbert space direct sum, $$W_0$$ is dense in $$\mathbf{H}$$, so $$\text{Range}(A - i\mathbf{1})$$ — being a superset of the dense subset $$W_0$$ — is itself dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$. Since $$A$$ is symmetric by hypothesis, [Theorem (Essential Self-Adjointness via Dense Range)](#thrm:hall-9.21) shows $$A$$ is essentially self-adjoint.

**Part 2: reduction to $$\text{Dom}(A) = W_0$$.** We first check $$A\vert_{W_0}$$ is itself a legitimate unbounded operator to which **Part 1**'s argument applies, and that it is symmetric. By [Definition (Hilbert Space Direct Sum)](#def:hall-a.45), the finite direct sum $$W_0$$ is dense in $$\mathbf{H}$$, so $$A\vert_{W_0}$$, with domain $$W_0$$, is an unbounded operator in the sense of [Definition (Unbounded Operator)](#def:hall-3.1). For symmetry: since $$W_0 \subset \text{Dom}(A)$$ and $$A\vert_{W_0} = A$$ on $$W_0$$, for $$\phi,\psi \in W_0$$, symmetry of $$A$$ gives $$\left< \phi, (A\vert_{W_0})\psi \right> = \left< \phi, A\psi \right> = \left< A\phi, \psi \right> = \left< (A\vert_{W_0})\phi, \psi \right>$$, which is the [definition of symmetric](#def:hall-9.2) for $$A\vert_{W_0}$$.

The argument of **Part 1**, applied verbatim to $$A\vert_{W_0}$$ in place of $$A$$ (it only used that $$\iota_j(\mathbf{H}_j) \subset W_0 = \text{Dom}(A\vert_{W_0})$$, that $$A\vert_{W_0}$$ agrees with $$A_j$$ there, and symmetry of $$A\vert_{W_0}$$, all just established), shows $$A\vert_{W_0}$$ is also essentially self-adjoint.

We now check $$A^{\text{cl}}$$ is a self-adjoint extension of $$A\vert_{W_0}$$. Essential self-adjointness of $$A$$, from **Part 1**, means exactly that $$A^{\text{cl}}$$ is self-adjoint; and, by Part 3 of [Proposition (Linearity and the Sequential Description of the Closure)](#prpstn:closure-linearity-and-sequential-description), $$A^{\text{cl}}$$ is an extension of $$A$$, which is in turn (trivially, by the [definition of extension](#def:hall-9.3)) an extension of $$A\vert_{W_0}$$. Extension is transitive: if $$\text{Dom}(A\vert_{W_0}) \subset \text{Dom}(A)$$ with $$A = A\vert_{W_0}$$ there, and $$\text{Dom}(A) \subset \text{Dom}(A^{\text{cl}})$$ with $$A^{\text{cl}} = A$$ there, then $$\text{Dom}(A\vert_{W_0}) \subset \text{Dom}(A^{\text{cl}})$$ and $$A^{\text{cl}} = A = A\vert_{W_0}$$ on $$\text{Dom}(A\vert_{W_0})$$. So $$A^{\text{cl}}$$ is a self-adjoint extension of $$A\vert_{W_0}$$. By [Proposition (Uniqueness of the Self-Adjoint Extension of an Essentially Self-Adjoint Operator)](#prpstn:hall-9.11) applied to the essentially self-adjoint operator $$A\vert_{W_0}$$, $$A^{\text{cl}}$$ must coincide with $$(A\vert_{W_0})^{\text{cl}}$$, the unique self-adjoint extension of $$A\vert_{W_0}$$:

$$
    A^{\text{cl}} = (A\vert_{W_0})^{\text{cl}}.
$$

By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10) applied to $$A$$, and separately to $$A\vert_{W_0}$$, together with self-adjointness of $$A^{\text{cl}}$$ and of $$(A\vert_{W_0})^{\text{cl}}$$ (both established in **Part 1**, applied to $$A$$ and to $$A\vert_{W_0}$$ respectively),

$$
    A^* = (A^{\text{cl}})^* = A^{\text{cl}} = (A\vert_{W_0})^{\text{cl}} = \big( (A\vert_{W_0})^{\text{cl}} \big)^* = (A\vert_{W_0})^*.
$$

So $$A^* = (A\vert_{W_0})^*$$, and it suffices to compute the adjoint of $$A\vert_{W_0}$$ — that is, we may assume without loss of generality that $$\text{Dom}(A) = W_0$$.

**Part 3: $$\text{Dom}(A^*) = V$$, with the stated formula.** Assume now $$\text{Dom}(A) = W_0$$. We first show $$V \subset \text{Dom}(A^*)$$. Let $$\phi = (\phi_1, \phi_2, \ldots) \in V$$, and let $$\psi = (\psi_1, \ldots, \psi_N, 0, 0, \ldots) \in W_0$$ be arbitrary. Since each $$A_j$$ is self-adjoint (hence symmetric, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4)) on $$\mathbf{H}_j$$, and using the definition of the inner product on the direct sum $$\mathbf{H}$$ as the sum of the componentwise inner products,

$$
    \left< \phi, A\psi \right> = \sum_{j=1}^N \left< \phi_j, A_j \psi_j \right> = \sum_{j=1}^N \left< A_j \phi_j, \psi_j \right> = \left< (A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots), \psi \right>.
$$

By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) applied in $$\mathbf{H}$$ — valid since both $$(A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots)$$ and $$\psi$$ are elements of $$\mathbf{H}$$ —

$$
    \lvert \left< \phi, A\psi \right> \rvert \le \left\| (A_1\phi_1, \ldots, A_N\phi_N, 0, \ldots) \right\| \left\| \psi \right\| = \left( \sum_{j=1}^N \left\| A_j \phi_j \right\|_j^2 \right)^{1/2} \left\| \psi \right\| \le \left( \sum_{j=1}^\infty \left\| A_j \phi_j \right\|_j^2 \right)^{1/2} \left\| \psi \right\|,
$$

and the right-most quantity is a finite constant since $$\phi \in V$$. Thus $$\psi \mapsto \left< \phi, A\psi \right>$$ is bounded on $$\text{Dom}(A) = W_0$$, so $$\phi \in \text{Dom}(A^*)$$ by the [definition of the adjoint](#def:hall-9.1). Moreover the computation above shows $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi \in W_0$$, where $$\chi = (A_1\phi_1, A_2\phi_2, \ldots)$$ — note $$\chi \in \mathbf{H}$$ since $$\sum_j \left\| A_j\phi_j \right\|_j^2 < \infty$$ — so, by uniqueness in the [definition of the adjoint](#def:hall-9.1), $$A^*\phi = \chi = (A_1\phi_1, A_2\phi_2, \ldots)$$, which is the claimed formula.

We now show $$\text{Dom}(A^*) \subset V$$. Let $$\phi = (\phi_1, \phi_2, \ldots) \in \text{Dom}(A^*)$$, so there is a constant $$C$$ with $$\lvert \left< \phi, A\psi \right> \rvert \le C \left\| \psi \right\|$$ for all $$\psi \in W_0$$. For each $$N$$, set $$\psi_N \equiv (A_1\phi_1, A_2\phi_2, \ldots, A_N\phi_N, 0, 0, \ldots) \in W_0$$ (a valid element of $$W_0$$ since each $$A_j\phi_j \in \mathbf{H}_j$$ and only finitely many entries are nonzero). Then, using self-adjointness of each $$A_j$$ as in the previous part,

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

We now record the internal-form version promised above.

> **Proposition** *(Direct Sums of Bounded Self-Adjoint Operators, Internal Form)*
<a name="prpstn:hall-9.26-internal"></a>
<!--  \uses{prpstn:hall-9.26} -->
<!--  \uses{lmm:internal-decomposition-unitary} -->
<!--  \uses{def:internal-orthogonal-decomposition} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.7} -->
<!--  \uses{def:hall-9.1} -->
> Suppose $$\{ \mathbf{K}_n \}_{n=1}^\infty$$ is an internal orthogonal decomposition of $$\mathbf{H}$$ into separable closed subspaces, and $$A_n$$ is a bounded, self-adjoint operator on $$\mathbf{K}_n$$ for each $$n$$. Define
>
> $$
>     V \equiv \left\{ \psi \in \mathbf{H} \;\middle|\; \sum_{n=1}^\infty \left( \left\| \psi_n \right\|^2 + \left\| A_n \psi_n \right\|^2 \right) < \infty \right\},
> $$
>
> where $$\psi = \sum_n \psi_n$$ is the (unique) decomposition of $$\psi$$. Suppose $$A$$ is a symmetric operator on $$\mathbf{H}$$ whose domain contains the algebraic span $$W_0$$ of the $$\mathbf{K}_n$$'s (finite sums $$\sum_{n=1}^N \eta_n$$, $$\eta_n \in \mathbf{K}_n$$), with $$A\eta = \sum_{n=1}^N A_n\eta_n$$ for $$\eta = \sum_{n=1}^N \eta_n \in W_0$$. Then $$A$$ is essentially self-adjoint, $$\text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = V$$, and
>
> $$
>     A^{\text{cl}}\psi = A^*\psi = \sum_{n=1}^\infty A_n \psi_n
> $$
>
> for all $$\psi \in V$$.

**Proof**
Let $$U : \mathbf{H} \to \bigoplus_n \mathbf{K}_n$$ be the unitary map of Part 3 of [**Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*](#lmm:internal-decomposition-unitary), $$U\psi = (\psi_1,\psi_2,\ldots)$$. Write $$\widetilde{\mathbf{H}} \equiv \bigoplus_n \mathbf{K}_n$$ for the external direct sum, and define $$\widetilde{A} \equiv UAU^{-1}$$, an operator on $$\widetilde{\mathbf{H}}$$ with $$\text{Dom}(\widetilde{A}) = U\big(\text{Dom}(A)\big)$$.

Since $$U$$ is a unitary bijection, it carries all the structure in the hypotheses across. Explicitly: $$U(W_0)$$ is exactly the finite direct sum of the $$\mathbf{K}_n$$'s (a finite sum $$\sum_{n=1}^N \eta_n$$ maps to the sequence with entries $$\eta_1,\ldots,\eta_N$$ and zeros beyond, and conversely), so $$\text{Dom}(\widetilde{A}) \supset U(W_0)$$ is the finite direct sum; and for such an element, $$\widetilde{A}(\eta_1,\ldots,\eta_N,0,\ldots) = U A \left( \sum_n \eta_n \right) = U\left( \sum_n A_n\eta_n \right) = (A_1\eta_1,\ldots,A_N\eta_N,0,\ldots)$$, matching the hypothesis of [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26). Moreover $$\widetilde{A}$$ is symmetric: for $$\widetilde\phi,\widetilde\psi \in \text{Dom}(\widetilde{A})$$, writing $$\phi = U^{-1}\widetilde\phi$$, $$\psi = U^{-1}\widetilde\psi \in \text{Dom}(A)$$, unitarity of $$U$$ (hence of $$U^{-1}$$) gives $$\left< \widetilde\phi, \widetilde{A}\widetilde\psi \right> = \left< \phi, A\psi \right> = \left< A\phi, \psi \right> = \left< \widetilde{A}\widetilde\phi, \widetilde\psi \right>$$, using symmetry of $$A$$ in the middle.

So [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) applies to $$\widetilde{A}$$ on $$\widetilde{\mathbf{H}}$$ and gives: $$\widetilde{A}$$ is essentially self-adjoint, with $$\text{Dom}(\widetilde{A}^{\text{cl}}) = \text{Dom}(\widetilde{A}^*) = \widetilde{V}$$, where $$\widetilde{V} = \{ (\psi_1,\psi_2,\ldots) \mid \sum_n ( \|\psi_n\|^2 + \|A_n\psi_n\|^2 ) < \infty \}$$, and $$\widetilde{A}^{\text{cl}}(\psi_1,\psi_2,\ldots) = (A_1\psi_1, A_2\psi_2,\ldots)$$ there.

Finally we transport back. A unitary $$U$$ intertwines adjoints and closures: $$(UAU^{-1})^* = U A^* U^{-1}$$ — since, for $$\widetilde\phi,\widetilde\psi$$, $$\left< \widetilde\phi, UAU^{-1}\widetilde\psi \right> = \left< U^{-1}\widetilde\phi, A U^{-1}\widetilde\psi \right>$$, so boundedness of $$\widetilde\psi \mapsto \left< \widetilde\phi, \widetilde{A}\widetilde\psi \right>$$ on $$\text{Dom}(\widetilde A)$$ is equivalent to boundedness of $$\psi \mapsto \left< U^{-1}\widetilde\phi, A\psi \right>$$ on $$\text{Dom}(A)$$, matching domains under $$U$$ by the [definition of the adjoint](#def:hall-9.1), with the values corresponding likewise — and $$(UAU^{-1})^{\text{cl}} = U A^{\text{cl}} U^{-1}$$, since $$U \times U$$ is a homeomorphism of $$\mathbf{H}\times\mathbf{H}$$ onto $$\widetilde{\mathbf{H}}\times\widetilde{\mathbf{H}}$$ (being unitary in each factor) and so carries the closure of the graph of $$A$$ onto the closure of the graph of $$\widetilde{A}$$. Hence $$A$$ is essentially self-adjoint (as $$A^{\text{cl}} = U^{-1}\widetilde{A}^{\text{cl}}U$$ is self-adjoint, $$\widetilde{A}^{\text{cl}}$$ being so), and

$$
    \text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = U^{-1}(\widetilde{V}) = V,
$$

the last equality because $$U\psi = (\psi_1,\psi_2,\ldots)$$, so the defining condition of $$\widetilde{V}$$ on $$U\psi$$ is verbatim the defining condition of $$V$$ on $$\psi$$. For $$\psi \in V$$, $$A^{\text{cl}}\psi = U^{-1}\widetilde{A}^{\text{cl}}U\psi = U^{-1}(A_1\psi_1,A_2\psi_2,\ldots) = \sum_n A_n\psi_n$$, the last step by the definition of $$U^{-1}$$ (the element of $$\mathbf{H}$$ whose decomposition has $$n$$-th entry $$A_n\psi_n$$, which is exactly the norm-convergent sum $$\sum_n A_n\psi_n$$).$$\blacksquare$$

## Integration Against a Projection-Valued Measure

The [previous post](../spectral-theorems) constructed, for a projection-valued measure $$\mu$$ on $$(X, \Omega(X))$$, an integral $$f \mapsto \int_X f \, d\mu$$ defined on *bounded* measurable functions $$f$$, landing in $$\mathcal{B}(\mathbf{H})$$. To state [Theorem 10.4](#thrm:hall-10.4), we need to make sense of $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ where the integrand $$\lambda \mapsto \lambda$$ is typically an *unbounded* function on $$\sigma(A)$$ — so the resulting integral will typically be an unbounded operator, and we need to say what its domain is. This section develops that theory in general, for an arbitrary (possibly unbounded) measurable function against an arbitrary projection-valued measure.

Recall that for $$\psi \in \mathbf{H}$$, $$\mu_\psi$$ denotes the [associated measure](../spectral-theorems/#thrm:projection-valued-measures-associated-measure) $$\mu_\psi(E) \equiv \left< \psi, \mu(E)\psi \right>$$, a positive, real-valued measure on $$(X, \Omega(X))$$. For a bounded measurable $$f$$, combining multiplicativity of the integral with the fact that integration intertwines complex conjugation and the adjoint — properties 3 and 4 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) — gives, for any $$\psi \in \mathbf{H}$$,

$$
\begin{align}
    \left\| \left( \int_X f \, d\mu \right) \psi \right\|^2 &= \left< \psi, \left( \int_X f \, d\mu \right)^* \left( \int_X f \, d\mu \right) \psi \right> \\
                                                             &= \left< \psi, \left( \int_X \overline{f} \, d\mu \right)\left( \int_X f \, d\mu \right) \psi \right> \\
                                                             &= \left< \psi, \left( \int_X \lvert f \rvert^2 \, d\mu \right) \psi \right> \\
                                                             &= \int_X \lvert f \rvert^2 \, d\mu_\psi, \tag{$\ast\ast\ast$}
\end{align}
$$

where the last equality is the defining property of the integral, applied to the bounded function $$\lvert f \rvert^2$$. If $$f$$ is *unbounded*, this suggests defining the domain of $$\int_X f \, d\mu$$ to be exactly the set of $$\psi$$ for which the right-hand side of $$(\ast\ast\ast)$$ is finite. Before making this precise, we need a version of the "quadratic form" and "sesquilinear form" machinery from the previous post that allows for a domain other than all of $$\mathbf{H}$$ — a subspace, not even necessarily dense, since we will want to apply this machinery to $$\mathbf{H}_n$$, a typically non-dense closed subspace, in the proof of [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3) below.

> **Definition** *(Sesquilinear Form on a Subspace)*
<a name="def:hall-sesquilinear-form-on-a-subspace"></a>
> Let $$D$$ be a subspace of $$\mathbf{H}$$. A *sesquilinear form on $$D$$* is a map $$L : D \times D \to \mathbb{C}$$ that is conjugate-linear in its first argument and linear in its second argument.

> **Definition** *(Quadratic Form on a Subspace)*
<a name="def:hall-quadratic-form-on-a-subspace"></a>
<!--  \uses{def:hall-sesquilinear-form-on-a-subspace} -->
> Let $$D$$ be a subspace of $$\mathbf{H}$$. A *quadratic form on $$D$$* is a map $$Q : D \to \mathbb{C}$$ with the following properties:
>
> 1. $$Q(\lambda\psi) = \lvert \lambda \rvert^2 Q(\psi)$$ for all $$\psi \in D$$ and $$\lambda \in \mathbb{C}$$.
> 2. The map $$L : D \times D \to \mathbb{C}$$ defined by
>
>    $$
>    \begin{align}
>        L(\phi, \psi) &\equiv \frac{1}{2} \left[ Q(\phi + \psi) - Q(\phi) - Q(\psi) \right] \\
>                      &-\frac{i}{2} \left[ Q(\phi + i\psi) - Q(\phi) - Q(i\psi) \right]
>    \end{align}
>    $$
>
>    is a sesquilinear form on $$D$$, called the *sesquilinear form associated to $$Q$$*.
>
> When $$D = \mathbf{H}$$, this recovers the notion of a (not necessarily bounded) quadratic form on $$\mathbf{H}$$ from the previous post.

Two elementary facts about quadratic forms on a subspace, generalizing [**Proposition** *(hall-a.61)*](../spectral-theorems/#prpstn:hall-a.61) of the previous post from $$D = \mathbf{H}$$ to a general subspace $$D$$, will be used repeatedly below. Since the proof of the bounded-case proposition is purely algebraic manipulation of the polarization formula — at no point using that $$D = \mathbf{H}$$, that $$D$$ is dense, or that the relevant vectors range over all of $$\mathbf{H}$$, only that $$D$$ is closed under the linear combinations $$\phi+\psi$$, $$\phi+i\psi$$, $$i\psi$$ appearing in the polarization formula — the same computation goes through verbatim on any subspace $$D$$; we record the two properties we need and reprove them directly, rather than merely asserting the analogy.

> **Proposition** *(Properties of Quadratic Forms on a Subspace)*
<a name="prpstn:quadratic-forms-on-a-subspace-properties"></a>
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
> Let $$D$$ be a subspace of $$\mathbf{H}$$, let $$Q$$ be a quadratic form on $$D$$, and let $$L$$ be its associated sesquilinear form.
>
> 1. If $$T : D \to \mathbf{H}$$ is linear and $$Q(\psi) = \left< \psi, T\psi \right>$$ for all $$\psi \in D$$, then $$L(\phi, \psi) = \left< \phi, T\psi \right>$$ for all $$\phi, \psi \in D$$.
> 2. If $$Q(\psi) \in \mathbb{R}$$ for all $$\psi \in D$$, then $$L(\phi, \psi) = \overline{L(\psi, \phi)}$$ for all $$\phi, \psi \in D$$.

**Proof**
**Part 1.** Fix $$\phi, \psi \in D$$; since $$D$$ is a subspace, $$\phi + \psi, \phi + i\psi, i\psi \in D$$ as well, so $$T$$ and $$Q$$ are defined at each. Expanding $$Q(\phi+\psi) = \left< \phi+\psi, T(\phi+\psi) \right>$$ using linearity of $$T$$ and of the inner product in its second argument, and additivity in its first,

$$
    Q(\phi+\psi) - Q(\phi) - Q(\psi) = \left< \phi, T\psi \right> + \left< \psi, T\phi \right>.
$$

Similarly, expanding $$Q(\phi + i\psi) = \left< \phi + i\psi, T(\phi + i\psi) \right>$$ and using $$\left< \phi, T(i\psi) \right> = i \left< \phi, T\psi \right>$$ and $$\left< i\psi, T\phi \right> = \overline{i} \left< \psi, T\phi \right> = -i \left< \psi, T\phi \right>$$ (conjugate-linearity in the first argument) and $$\left< i\psi, T(i\psi) \right> = \overline{i}\, i \left< \psi, T\psi \right> = \left< \psi, T\psi \right>$$,

$$
    Q(\phi+i\psi) - Q(\phi) - Q(i\psi) = i\left< \phi, T\psi \right> - i \left< \psi, T\phi \right>.
$$

Substituting both into the polarization formula defining $$L$$,

$$
\begin{align}
    L(\phi, \psi) &= \frac{1}{2}\Big[ \left< \phi, T\psi \right> + \left< \psi, T\phi \right> \Big] - \frac{i}{2}\Big[ i\left< \phi, T\psi \right> - i\left< \psi, T\phi \right> \Big] \\
                  &= \frac{1}{2}\Big[ \left< \phi, T\psi \right> + \left< \psi, T\phi \right> \Big] + \frac{1}{2}\Big[ \left< \phi, T\psi \right> - \left< \psi, T\phi \right> \Big] \\
                  &= \left< \phi, T\psi \right>,
\end{align}
$$

using $$-\tfrac{i}{2}\cdot i = \tfrac{1}{2}$$. This is the desired identity.

**Part 2.** Define $$M(\phi, \psi) \equiv \text{Re}\big[ L(\phi,\psi) \big]$$ for $$\phi, \psi \in D$$. Since $$Q$$ is real-valued, taking the real part of the polarization formula defining $$L$$ leaves only the first bracket (the second is multiplied by $$i$$):

$$
    M(\phi, \psi) = \frac{1}{2}\big[ Q(\phi+\psi) - Q(\phi) - Q(\psi) \big],
$$

which is manifestly symmetric, $$M(\phi,\psi) = M(\psi,\phi)$$. Since $$M = \text{Re}[L]$$ and $$L$$ is sesquilinear (property 2 of the [definition of a quadratic form](#def:hall-quadratic-form-on-a-subspace)), $$M$$ is real-bilinear: additive and $$\mathbb{R}$$-homogeneous in each argument. Also, using $$Q(\lambda\xi) = \lvert \lambda \rvert^2 Q(\xi)$$ (property 1 of the same definition) with $$\lambda = i$$,

$$
    M(i\phi, i\psi) = \frac{1}{2}\big[ Q(i\phi+i\psi) - Q(i\phi) - Q(i\psi) \big] = \frac{1}{2}\big[ \lvert i \rvert^2 Q(\phi+\psi) - Q(\phi) - Q(\psi) \big] = M(\phi, \psi),
$$

using $$i\phi + i\psi = i(\phi+\psi)$$ and $$\lvert i \rvert^2 = 1$$. Combining symmetry, real-bilinearity, and $$M(i\phi,i\psi) = M(\phi,\psi)$$ (applied with $$\phi \mapsto i\psi$$, $$\psi \mapsto \phi$$),

$$
    M(\phi, i\psi) = M(i\psi, \phi) = M\big( i(i\psi), i\phi \big) = M(-\psi, i\phi) = -M(\psi, i\phi).
$$

Comparing with the polarization formula, $$M(\phi,i\psi) = \tfrac{1}{2}\big[ Q(\phi+i\psi) - Q(\phi) - Q(i\psi) \big]$$ is exactly the bracket appearing in the second term of $$L(\phi,\psi)$$, so $$L(\phi,\psi) = M(\phi,\psi) - iM(\phi,i\psi)$$. Substituting $$M(\phi,i\psi) = -M(\psi,i\phi)$$ and then $$M(\phi,\psi) = M(\psi,\phi)$$,

$$
    L(\phi,\psi) = M(\phi,\psi) + iM(\psi,i\phi) = M(\psi,\phi) + iM(\psi,i\phi).
$$

Since $$M$$ is real-valued, this is exactly $$\overline{M(\psi,\phi) - iM(\psi,i\phi)} = \overline{L(\psi,\phi)}$$ (the same pattern applied to $$L(\psi,\phi)$$), giving $$L(\phi,\psi) = \overline{L(\psi,\phi)}$$.$$\blacksquare$$

The proof of Proposition (hall-10.2) below draws on three standard facts of Lebesgue integration that neither this post nor the previous one has needed until now. [Hall](https://doi.org/10.1007/978-1-4614-7116-5) explicitly assumes these as background (Appendix A.2: "we assume those parts of measure theory that are entirely standard: the monotone convergence and dominated convergence theorems, $$L^p$$ spaces, and Fubini's theorem"), so, exactly as with Cauchy–Schwarz or the Bounded Linear Transformation Theorem, we state them here without proof.

> **Theorem** *(Monotone Convergence Theorem, for Integrals)*
<a name="thrm:monotone-convergence-theorem-for-integrals"></a>
> Let $$(X, \Omega, \nu)$$ be a measure space, and let $$\{ g_n \}_{n \in \mathbb{N}}$$ be a sequence of nonnegative measurable functions on $$X$$ with $$g_n(x) \le g_{n+1}(x)$$ for all $$x \in X$$ and all $$n$$, converging pointwise to a function $$g$$. Then
>
> $$
>     \int_X g_n \, d\nu \longrightarrow \int_X g \, d\nu
> $$
>
> as $$n \to \infty$$ (an equality in $$[0, \infty]$$).

> **Proposition** *(Monotonicity of the Integral in the Measure)*
<a name="prpstn:monotonicity-of-the-integral-in-the-measure"></a>
> Let $$\nu, \nu'$$ be measures on $$(X, \Omega)$$ with $$\nu(E) \le \nu'(E)$$ for every $$E \in \Omega$$. Then $$\int_X g \, d\nu \le \int_X g \, d\nu'$$ for every nonnegative measurable $$g$$ on $$X$$.

> **Definition** *($$L^2$$ of a Measure Space)*
<a name="def:hall-a.46"></a>
> If $$(X, \mu)$$ is a measure space, define an inner product on $$L^2(X, \mu)$$ by the formula
>
> $$
>     \left< \phi, \psi \right> \equiv \int_X \overline{\phi(x)} \, \psi(x) \, d\mu(x).
> $$
>
> This integral is absolutely convergent for all $$\phi, \psi \in L^2(X, \mu)$$, $$\left< \cdot, \cdot \right>$$ is indeed an inner product, and $$L^2(X, \mu)$$ is complete with respect to the associated norm; thus $$L^2(X, \mu)$$, with this inner product, is a Hilbert space.

> **Proposition** *(Countable Additivity of the Integral over a Disjoint Cover)*
<a name="prpstn:countable-additivity-of-the-integral"></a>
> Let $$(X,\Omega,\nu)$$ be a measure space, $$g$$ a nonnegative measurable function on $$X$$, and $$\{ E_n \}_{n=1}^\infty$$ a pairwise disjoint sequence in $$\Omega$$ with $$\bigcup_n E_n = X$$. Then
>
> $$
>     \int_X g \, d\nu = \sum_{n=1}^\infty \int_{E_n} g \, d\nu
> $$
>
> (an equality in $$[0,\infty]$$).

> **Proposition** *(Integrals Agree when Measures Agree on a Set)*
<a name="prpstn:integrals-agree-when-measures-agree"></a>
> Let $$\nu, \nu'$$ be measures on $$(X,\Omega)$$ and $$E \in \Omega$$, and suppose $$\nu(S) = \nu'(S)$$ for every measurable $$S \subset E$$. Then $$\int_E g \, d\nu = \int_E g \, d\nu'$$ for every nonnegative measurable $$g$$ on $$X$$.

We record two more facts about projection-valued measures before the main proof, both used more than once below; extracting them now avoids re-deriving them, or worse, citing "the same argument as" a proof written for a different purpose.

> **Lemma** *(Range Membership Concentrates the Associated Measure)*
<a name="lmm:range-membership-concentrates-measure"></a>
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X,\Omega(X))$$ and $$\eta \in \text{Range}(\mu(E))$$ for some $$E \in \Omega(X)$$. Then $$\mu_\eta(E^c) = 0$$. Consequently, for any nonnegative measurable $$g$$ on $$X$$,
>
> $$
>     \int_X g \, d\mu_\eta = \int_E g \, d\mu_\eta.
> $$

**Proof**
Write $$\eta = \mu(E)\xi$$ for some $$\xi \in \mathbf{H}$$. Idempotency of $$\mu(E)$$ (part of being a [bounded orthogonal projection](../spectral-theorems/#def:bounded-orthogonal-projection)) gives $$\mu(E)\eta = \mu(E)^2\xi = \mu(E)\xi = \eta$$. Hence, using property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) and $$E^c \cap E = \emptyset$$,

$$
    \mu_\eta(E^c) = \left< \eta, \mu(E^c)\eta \right> = \left< \eta, \mu(E^c)\mu(E)\eta \right> = \left< \eta, \mu(E^c \cap E)\eta \right> = \left< \eta, \mu(\emptyset)\eta \right> = 0.
$$

For the consequence: since $$g \ge 0$$ and the measure of $$E^c$$ under $$\mu_\eta$$ is $$0$$, the portion of the integral over $$E^c$$ vanishes, and $$\int_X g\,d\mu_\eta = \int_E g\,d\mu_\eta + \int_{E^c} g\,d\mu_\eta = \int_E g\,d\mu_\eta + 0$$.$$\blacksquare$$

> **Lemma** *(Norm-Convergent Decomposition over a Disjoint Cover)*
<a name="lmm:norm-convergent-decomposition"></a>
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X,\Omega(X))$$, and $$\{F_n\}_{n\in\mathbb{N}}$$ is a pairwise disjoint sequence in $$\Omega(X)$$ with $$\bigcup_n F_n = X$$. Then for every $$\psi \in \mathbf{H}$$:
>
> 1. $$\psi = \sum_{n=1}^\infty \mu(F_n)\psi$$, convergent in the norm topology on $$\mathbf{H}$$.
> 2. For every $$N \in \mathbb{N}$$, $$\mu\big( \bigcup_{n=1}^N F_n \big)\psi = \sum_{n=1}^N \mu(F_n)\psi$$ — the $$N$$-th partial sum of the series in Part 1, so that $$\mu\big( \bigcup_{n=1}^N F_n \big)\psi \to \psi$$ as $$N \to \infty$$.

**Proof**
**Part 1.** Property 3 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure), applied to the pairwise disjoint sequence $$F_1, F_2, \ldots$$, gives $$\mu(X)\psi = \sum_{n=1}^\infty \mu(F_n)\psi$$, convergent in norm; since $$\mu(X) = \mathbf{1}$$ (property 2 of the same definition), this reads $$\psi = \sum_{n=1}^\infty \mu(F_n)\psi$$.

**Part 2.** Apply property 3 again, this time to the disjoint sequence $$F_1, \ldots, F_N, \emptyset, \emptyset, \ldots$$, whose union is $$\bigcup_{n=1}^N F_n$$, and whose infinitely many empty terms each contribute $$\mu(\emptyset)\psi = 0$$ (property 2): this gives $$\mu\big( \bigcup_{n=1}^N F_n \big)\psi = \sum_{n=1}^N \mu(F_n)\psi + \sum_{n>N} \mu(\emptyset)\psi = \sum_{n=1}^N \mu(F_n)\psi$$, exactly the $$N$$-th partial sum of the series in Part 1. By definition of convergence of that series to $$\psi$$, these partial sums converge to $$\psi$$ as $$N \to \infty$$.$$\blacksquare$$

One more standard fact is needed before we can even state that $$Q_f(\psi) \equiv \int_X f \, d\mu_\psi$$ is well defined (a finite complex number, not merely an integral of an integrable-in-modulus-squared function) for $$\psi \in W_f$$: on a finite measure space, an $$L^2$$ function is automatically $$L^1$$.

> **Lemma** *($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)*
<a name="lmm:l2-implies-l1"></a>
<!--  \uses{def:hall-a.46} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$\nu$$ is a finite measure on $$(X,\Omega)$$ and $$h \in L^2(X,\nu)$$. Then $$h \in L^1(X,\nu)$$, with $$\int_X \lvert h \rvert \, d\nu \le \nu(X)^{1/2} \left( \int_X \lvert h \rvert^2 \, d\nu \right)^{1/2}$$.

**Proof**
The constant function $$1$$ is in $$L^2(X,\nu)$$, since $$\int_X 1^2 \, d\nu = \nu(X) < \infty$$ ($$\nu$$ finite). By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43), applied in the inner product space $$L^2(X,\nu)$$ of [**Definition** *($$L^2$$ of a Measure Space)*](#def:hall-a.46) to $$\lvert h \rvert$$ and $$1$$,

$$
    \int_X \lvert h \rvert \, d\nu = \left< \lvert h \rvert, 1 \right>_{L^2(X,\nu)} \le \left\| h \right\|_{L^2(X,\nu)} \left\| 1 \right\|_{L^2(X,\nu)} = \left( \int_X \lvert h \rvert^2 \, d\nu \right)^{1/2} \nu(X)^{1/2},
$$

which is finite since $$h \in L^2(X,\nu)$$ and $$\nu(X) < \infty$$. So $$h \in L^1(X,\nu)$$, with the stated bound.$$\blacksquare$$

We can now state and prove the central technical result of this section. It is the unbounded analogue of the correspondence, from the previous post, between bounded operators and bounded quadratic forms.

> **Proposition**
<a name="prpstn:hall-10.2"></a>
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{thrm:monotone-convergence-theorem-for-integrals} -->
<!--  \uses{prpstn:monotonicity-of-the-integral-in-the-measure} -->
<!--  \uses{def:hall-a.46} -->
<!--  \uses{lmm:l2-implies-l1} -->
<!--  \uses{thrm:hall-a.52} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.62} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{lmm:norm-convergent-decomposition} -->
> Let $$\mu$$ be a projection-valued measure on $$(X, \Omega(X))$$ with values in $$\mathcal{B}(\mathbf{H})$$, and let $$f$$ be a measurable function on $$X$$, not necessarily bounded. Let
>
> $$
>     W_f \equiv \left\{ \psi \in \mathbf{H} \;\middle|\; \int_X \lvert f \rvert^2 \, d\mu_\psi < \infty \right\}.
> $$
>
> Then the following hold.
>
> 1. $$W_f$$ is a dense subspace of $$\mathbf{H}$$, and the map $$Q_f : W_f \to \mathbb{C}$$ given by $$Q_f(\psi) \equiv \int_X f \, d\mu_\psi$$ is a quadratic form on $$W_f$$.
> 2. If $$L_f$$ is the sesquilinear form on $$W_f$$ associated to $$Q_f$$, then
>
>    $$
>        \lvert L_f(\phi, \psi) \rvert \le \left\| \phi \right\| \, \left\| f \right\|_{L^2(X, \mu_\psi)}
>    $$
>
>    for all $$\phi, \psi \in W_f$$, where $$\left\| f \right\|_{L^2(X, \mu_\psi)} \equiv \left( \int_X \lvert f \rvert^2 \, d\mu_\psi \right)^{1/2}$$.
> 3. For each $$\psi \in W_f$$, there is a unique $$\chi \in \mathbf{H}$$ such that $$L_f(\phi, \psi) = \left< \phi, \chi \right>$$ for all $$\phi \in W_f$$. The map $$\psi \mapsto \chi$$ is linear on $$W_f$$, and for all $$\psi \in W_f$$,
>
>    $$
>        \left\| \chi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi.
>    $$

**Proof**
Before checking any properties of $$Q_f$$, we note it is well defined: for $$\psi \in W_f$$, $$\mu_\psi$$ is a finite measure ($$\mu_\psi(X) = \left\| \psi \right\|^2 < \infty$$) and $$f \in L^2(X,\mu_\psi)$$ (this is exactly the membership condition defining $$W_f$$), so [Lemma ($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)](#lmm:l2-implies-l1) gives $$f \in L^1(X,\mu_\psi)$$. Hence $$Q_f(\psi) = \int_X f \, d\mu_\psi$$ is a well-defined (finite) complex number for every $$\psi \in W_f$$, as required for $$Q_f$$ to be a map $$W_f \to \mathbb{C}$$ at all.

**Part 1.** We first check $$W_f$$ is a subspace. If $$\psi \in W_f$$ and $$\lambda \in \mathbb{C}$$, then, directly from the definition of $$\mu_{\lambda\psi}$$ and conjugate-linearity/linearity of the inner product in its two arguments,

$$
    \mu_{\lambda\psi}(E) = \left< \lambda\psi, \mu(E)\lambda\psi \right> = \overline{\lambda}\lambda \left< \psi, \mu(E)\psi \right> = \lvert \lambda \rvert^2 \mu_\psi(E)
$$

for every $$E \in \Omega(X)$$, so $$\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \mu_\psi$$ as measures on $$(X, \Omega(X))$$. Hence $$\int_X \lvert f \rvert^2 \, d\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \int_X \lvert f \rvert^2 \, d\mu_\psi$$, which is finite exactly when $$\int_X \lvert f \rvert^2 \, d\mu_\psi$$ is (trivially, if $$\lambda = 0$$ both integrals are $$0$$); so $$\lambda\psi \in W_f$$.

For closure under addition, fix $$\phi, \psi \in \mathbf{H}$$ and $$E \in \Omega(X)$$. Since $$\mu(E)$$ is a bounded orthogonal projection, and using the triangle inequality followed by the elementary inequality $$(x+y)^2 \le 2x^2 + 2y^2$$ for $$x, y \in \mathbb{R}$$,

$$
\begin{align}
    \mu_{\phi+\psi}(E) &= \left\| \mu(E)(\phi + \psi) \right\|^2 \\
                       &\le \left( \left\| \mu(E)\phi \right\| + \left\| \mu(E)\psi \right\| \right)^2 \\
                       &\le 2 \left\| \mu(E)\phi \right\|^2 + 2 \left\| \mu(E)\psi \right\|^2 \\
                       &= 2\mu_\phi(E) + 2\mu_\psi(E).
\end{align}
$$

As this holds for every $$E \in \Omega(X)$$, the measure $$\mu_{\phi+\psi}$$ is dominated by the finite measure $$2\mu_\phi + 2\mu_\psi$$, so by [**Monotonicity of the Integral in the Measure**](#prpstn:monotonicity-of-the-integral-in-the-measure), for any nonnegative measurable $$g$$ on $$X$$, $$\int_X g \, d\mu_{\phi+\psi} \le \int_X g \, d(2\mu_\phi + 2\mu_\psi) = 2\int_X g \, d\mu_\phi + 2\int_X g \, d\mu_\psi$$, applied with $$g = \lvert f \rvert^2$$. Thus, if $$\phi, \psi \in W_f$$, then $$\int_X \lvert f \rvert^2 \, d\mu_{\phi+\psi} \le 2\int_X \lvert f \rvert^2 \, d\mu_\phi + 2\int_X \lvert f \rvert^2 \, d\mu_\psi < \infty$$, so $$\phi + \psi \in W_f$$. Since also $$0 \in W_f$$ (as $$\mu_0 = 0$$, the zero measure), $$W_f$$ is a subspace of $$\mathbf{H}$$.

We next show $$W_f$$ is dense in $$\mathbf{H}$$. For $$n \in \mathbb{N} = \{1, 2, 3, \ldots\}$$ (throughout this post, indices of this kind start at $$1$$, never $$0$$), let $$E_n \equiv \{ x \in X \mid \lvert f(x) \rvert < n \}$$, so $$E_1 \subset E_2 \subset \cdots$$ and, since $$f$$ is finite-valued at every point of $$X$$, $$\bigcup_{n} E_n = X$$. Fix $$\psi \in \mathbf{H}$$, and let $$F_1 \equiv E_1$$ and $$F_n \equiv E_n \setminus E_{n-1}$$ for $$n \ge 2$$; the $$F_n$$ are pairwise disjoint, $$\bigcup_{j=1}^n F_j = E_n$$ for every $$n$$ (immediate by induction: true for $$n=1$$, and if $$\bigcup_{j=1}^{n-1} F_j = E_{n-1}$$ then $$\bigcup_{j=1}^n F_j = E_{n-1} \cup (E_n \setminus E_{n-1}) = E_n$$, the last step because $$E_{n-1} \subset E_n$$), and $$\bigcup_{j=1}^\infty F_j = \bigcup_n E_n = X$$. By [Lemma (Norm-Convergent Decomposition over a Disjoint Cover)](#lmm:norm-convergent-decomposition), applied to this sequence $$\{F_n\}$$, $$\mu(E_n)\psi = \mu\big(\bigcup_{j=1}^n F_j\big)\psi \to \psi$$ as $$n \to \infty$$.

For each $$n$$, $$\mu(E_n)\psi \in \text{Range}(\mu(E_n))$$; and for $$\eta \in \text{Range}(\mu(E_n))$$, [Lemma (Range Membership Concentrates the Associated Measure)](#lmm:range-membership-concentrates-measure) gives $$\int_X \lvert f \rvert^2\,d\mu_\eta = \int_{E_n} \lvert f \rvert^2\,d\mu_\eta \le n^2 \mu_\eta(E_n) \le n^2 \mu_\eta(X) = n^2 \left\| \eta \right\|^2 < \infty$$ — using $$\lvert f \rvert < n$$ on $$E_n$$, and $$\mu_\eta(X) = \left< \eta, \mu(X)\eta \right> = \left< \eta, \eta \right> = \left\| \eta \right\|^2$$. So $$\text{Range}(\mu(E_n)) \subset W_f$$ for every $$n$$. Since $$\mu(E_n)\psi \in \text{Range}(\mu(E_n)) \subset W_f$$ and $$\mu(E_n)\psi \to \psi$$, and $$\psi \in \mathbf{H}$$ was arbitrary, $$W_f$$ is dense in $$\mathbf{H}$$.

We now verify $$Q_f$$ satisfies the two properties required of a [quadratic form on $$W_f$$](#def:hall-quadratic-form-on-a-subspace). Property 1, $$Q_f(\lambda\psi) = \lvert \lambda \rvert^2 Q_f(\psi)$$, follows immediately from $$\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \mu_\psi$$ (shown above) and linearity of the integral in the measure. For property 2, we first establish a convergence fact we will reuse in **Part 2** below. Fix $$\psi \in W_f$$, and set $$f_n \equiv f \cdot 1_{E_n}$$, a bounded measurable function for each $$n$$ (as $$\lvert f_n \rvert \le n$$). Writing $$f = (f_+ - f_-) + i(g_+ - g_-)$$ in terms of the (nonnegative, measurable) positive and negative parts of the real and imaginary parts of $$f$$, each of $$f_+ 1_{E_n}, f_- 1_{E_n}, g_+ 1_{E_n}, g_- 1_{E_n}$$ is a nondecreasing (in $$n$$) sequence of nonnegative measurable functions converging pointwise to $$f_+, f_-, g_+, g_-$$ respectively, since $$E_n \uparrow X$$. By the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals) applied to $$\mu_\psi$$-integrals of each of these four sequences, $$\int_X f_\pm 1_{E_n} \, d\mu_\psi \to \int_X f_\pm \, d\mu_\psi$$ and $$\int_X g_\pm 1_{E_n} \, d\mu_\psi \to \int_X g_\pm \, d\mu_\psi$$; by [Lemma ($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)](#lmm:l2-implies-l1) — applicable since $$\psi \in W_f$$ ensures $$f \in L^2(X, \mu_\psi)$$ and $$\mu_\psi$$ is a finite measure ($$\mu_\psi(X) = \left\| \psi \right\|^2 < \infty$$) — $$f \in L^1(X,\mu_\psi)$$, so all four limiting integrals above are finite. Combining the four limits with appropriate signs,

$$
    Q_{f_n}(\psi) = \int_X f_n \, d\mu_\psi \longrightarrow \int_X f \, d\mu_\psi = Q_f(\psi). \tag{$\dagger$}
$$

More generally, the same argument, with $$\psi$$ replaced by an arbitrary $$\xi \in W_f$$ throughout (finiteness of $$\mu_\xi$$, membership of $$f$$ in $$L^2(X,\mu_\xi)$$ hence $$L^1(X,\mu_\xi)$$, and the Monotone Convergence Theorem applied to $$\mu_\xi$$-integrals), shows $$Q_{f_n}(\xi) \to Q_f(\xi)$$ for *every* $$\xi \in W_f$$, not just $$\xi = \psi$$ — indeed the same $$E_n$$'s work for every $$\xi \in W_f$$, since $$1_{E_n}$$ does not depend on $$\xi$$.

Now fix $$\phi, \psi \in W_f$$. Since $$W_f$$ is a subspace (shown above), $$\phi + \psi, \phi + i\psi, i\psi \in W_f$$, so by the previous paragraph, $$Q_{f_n}(\xi) \to Q_f(\xi)$$ for each of $$\xi \in \{ \phi + \psi, \phi, \psi, \phi + i\psi, i\psi \}$$. Each $$f_n$$ is bounded, so $$Q_{f_n}$$ is a genuine (bounded) quadratic form on all of $$\mathbf{H}$$ in the sense of the previous post — indeed $$Q_{f_n}(\xi) = \left< \xi, \left( \int_X f_n \, d\mu \right) \xi \right>$$ by the defining property of the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration), matching the construction of [**Proposition** *(hall-a.62)*](../spectral-theorems/#prpstn:hall-a.62) applied to the bounded operator $$\int_X f_n \, d\mu$$ — so its associated sesquilinear form $$L_{f_n}$$, given by the same polarization formula, is a genuine (bounded) sesquilinear form on $$\mathbf{H}$$, in particular conjugate-linear in its first argument and linear in its second. Taking $$n \to \infty$$ in the polarization formula defining $$L_{f_n}(\phi, \psi)$$ term by term, each $$Q_{f_n}$$-term converges to the corresponding $$Q_f$$-term by the previous paragraph, so

$$
    L_{f_n}(\phi, \psi) \longrightarrow L_f(\phi, \psi)
$$

for all $$\phi, \psi \in W_f$$, where $$L_f$$ is defined on $$W_f$$ by the same polarization formula applied to $$Q_f$$. Since each relation $$L_{f_n}(\alpha\phi_1 + \beta\phi_2, \psi) = \overline{\alpha} L_{f_n}(\phi_1, \psi) + \overline{\beta} L_{f_n}(\phi_2, \psi)$$ (and the analogous relation for linearity in the second argument) holds for every $$n$$ — with all terms in $$W_f$$, hence covered by the convergence just established — taking $$n \to \infty$$ on both sides shows the same relations hold for $$L_f$$. Thus $$L_f$$ is a sesquilinear form on $$W_f$$, verifying property 2, and completing the proof that $$Q_f$$ is a quadratic form on $$W_f$$.

**Part 2.** Fix $$\phi, \psi \in W_f$$, and retain $$f_n = f \cdot 1_{E_n}$$ from **Part 1**. Since $$f_n$$ is bounded, $$(\ast\ast\ast)$$ from the start of this section applies to $$f_n$$: $$\left\| \left( \int_X f_n \, d\mu \right) \eta \right\|^2 = \int_X \lvert f_n \rvert^2 \, d\mu_\eta$$ for all $$\eta \in \mathbf{H}$$. Combined with $$L_{f_n}(\phi, \psi) = \left< \phi, \left( \int_X f_n \, d\mu \right)\psi \right>$$ (noted in **Part 1**) and [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43),

$$
    \lvert L_{f_n}(\phi, \psi) \rvert \le \left\| \phi \right\| \left\| \left( \int_X f_n \, d\mu \right) \psi \right\| = \left\| \phi \right\| \left( \int_X \lvert f_n \rvert^2 \, d\mu_\psi \right)^{1/2}.
$$

By **Part 1**, $$L_{f_n}(\phi, \psi) \to L_f(\phi, \psi)$$ as $$n \to \infty$$. For the right-hand side, $$\lvert f_n \rvert^2 = \lvert f \rvert^2 1_{E_n}$$ is a nondecreasing sequence of nonnegative functions converging pointwise to $$\lvert f \rvert^2$$, so by the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals), $$\int_X \lvert f_n \rvert^2 \, d\mu_\psi \to \int_X \lvert f \rvert^2 \, d\mu_\psi = \left\| f \right\|_{L^2(X,\mu_\psi)}^2$$. Taking $$n \to \infty$$ in the displayed inequality gives $$\lvert L_f(\phi, \psi) \rvert \le \left\| \phi \right\| \left\| f \right\|_{L^2(X,\mu_\psi)}$$, the desired bound.

**Part 3.** Fix $$\psi \in W_f$$. By **Part 2**, the map $$\phi \mapsto L_f(\phi, \psi)$$ is bounded on $$W_f$$ with bound $$\left\| f \right\|_{L^2(X,\mu_\psi)}$$; since $$L_f$$ is conjugate-linear in $$\phi$$ (by **Part 1**), this map is a bounded conjugate-linear functional on $$W_f$$. Consider instead the map $$T : \phi \mapsto \overline{L_f(\phi, \psi)}$$, which is linear (conjugating a conjugate-linear map gives a linear map) and bounded with the same bound, on the dense subspace $$W_f$$ of $$\mathbf{H}$$. Exactly as in the justification following [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1) — $$\mathbf{H}$$ normed, $$\mathbb{C}$$ Banach, $$W_f$$ dense — the [**Bounded Linear Transformation Theorem**](../spectral-theorems/#thrm:bounded-linear-transformation-theorem) extends $$T$$ uniquely to a bounded linear functional $$\tilde{T}$$ on $$\mathbf{H}$$, and the [**Riesz Theorem**](#thrm:hall-a.52) produces a unique $$\chi \in \mathbf{H}$$ with $$\tilde{T}\phi = \left< \chi, \phi \right>$$ for all $$\phi \in \mathbf{H}$$; restricting to $$\phi \in W_f$$, where $$\tilde T$$ agrees with $$T$$, and conjugating both sides,

$$
    L_f(\phi, \psi) = \overline{T\phi} = \overline{\left< \chi, \phi \right>} = \left< \phi, \chi \right>
$$

for all $$\phi \in W_f$$. Uniqueness of $$\chi$$ with this property follows from [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot), exactly as in the uniqueness argument for the adjoint.

For linearity of $$\psi \mapsto \chi$$: writing $$\chi_\psi$$ for the vector associated to $$\psi \in W_f$$, fix $$\psi_1, \psi_2 \in W_f$$ and $$\alpha, \beta \in \mathbb{C}$$. Since $$L_f$$ is linear in its second argument, for all $$\phi \in W_f$$,

$$
    L_f(\phi, \alpha\psi_1 + \beta\psi_2) = \alpha L_f(\phi, \psi_1) + \beta L_f(\phi, \psi_2) = \alpha \left< \phi, \chi_{\psi_1} \right> + \beta \left< \phi, \chi_{\psi_2} \right> = \left< \phi, \alpha\chi_{\psi_1} + \beta\chi_{\psi_2} \right>,
$$

using linearity of the inner product in its second argument for the last step. By uniqueness (via [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) again), $$\chi_{\alpha\psi_1 + \beta\psi_2} = \alpha\chi_{\psi_1} + \beta\chi_{\psi_2}$$.

Finally, we derive the norm formula $$\left\| \chi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi$$. Retain $$f_n = f \cdot 1_{E_n}$$ from **Part 1**, and set $$\chi_n \equiv \left( \int_X f_n \, d\mu \right)\psi \in \mathbf{H}$$ — well defined since $$f_n$$ is bounded, so $$\int_X f_n \, d\mu \in \mathcal{B}(\mathbf{H})$$. For any $$\phi \in W_f$$, $$L_{f_n}(\phi,\psi) = \left< \phi, \chi_n \right>$$ (noted in **Part 1**) together with $$L_{f_n}(\phi,\psi) \to L_f(\phi,\psi) = \left< \phi, \chi \right>$$ (also **Part 1**) gives

$$
    \left< \phi, \chi_n \right> \longrightarrow \left< \phi, \chi \right> \quad \text{for every } \phi \in W_f. \tag{$\ddagger$}
$$

We show $$\{ \chi_n \}_{n \in \mathbb{N}}$$ is a Cauchy sequence in $$\mathbf{H}$$. For $$n < m$$, $$E_n \subset E_m$$ gives $$f_n - f_m = f \cdot 1_{E_n} - f \cdot 1_{E_m} = -f \cdot 1_{E_m \setminus E_n}$$, so, applying $$(\ast\ast\ast)$$ to the bounded function $$f_n - f_m$$ and using linearity of the bounded integral,

$$
    \left\| \chi_n - \chi_m \right\|^2 = \left\| \left( \int_X (f_n - f_m) \, d\mu \right)\psi \right\|^2 = \int_X \lvert f_n - f_m \rvert^2 \, d\mu_\psi = \int_{E_m \setminus E_n} \lvert f \rvert^2 \, d\mu_\psi = \int_X \lvert f_m \rvert^2 \, d\mu_\psi - \int_X \lvert f_n \rvert^2 \, d\mu_\psi,
$$

the last equality because $$E_n \subset E_m$$ splits $$\int_{E_m}$$ as $$\int_{E_n} + \int_{E_m \setminus E_n}$$. By **Part 2**'s argument, $$\int_X \lvert f_n \rvert^2 \, d\mu_\psi \to \int_X \lvert f \rvert^2 \, d\mu_\psi$$, a finite limit since $$\psi \in W_f$$; being also non-decreasing in $$n$$, this sequence of real numbers is Cauchy, so the right-hand side above tends to $$0$$ as $$n, m \to \infty$$. Thus $$\{ \chi_n \}_{n \in \mathbb{N}}$$ is Cauchy in $$\mathbf{H}$$, and, $$\mathbf{H}$$ being complete, converges to some $$\chi' \in \mathbf{H}$$.

By [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), $$\left< \phi, \chi' \right> = \lim_n \left< \phi, \chi_n \right> = \left< \phi, \chi \right>$$ for every $$\phi \in W_f$$, using $$(\ddagger)$$ — matching the defining property of $$\chi$$ exactly — so $$\chi' = \chi$$ by [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot). That is, $$\chi_n \to \chi$$ in norm, so, by continuity of the norm,

$$
    \left\| \chi \right\|^2 = \lim_{n \to \infty} \left\| \chi_n \right\|^2 = \lim_{n \to \infty} \int_X \lvert f_n \rvert^2 \, d\mu_\psi = \int_X \lvert f \rvert^2 \, d\mu_\psi,
$$

the desired formula.$$\blacksquare$$

The proof of Part 1 above showed, along the way, that $$\text{Range}(\mu(E_n)) \subset W_f$$ for the particular sets $$E_n$$ used there. We record the general fact as its own statement, since [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3) needs it below and should not have to reach inside another proof for it.

> **Lemma** *(Bounded on a Set Implies the Range Lies in the Domain)*
<a name="lmm:bounded-on-set-range-in-domain"></a>
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{prpstn:hall-10.2} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X,\Omega(X))$$, $$f$$ is measurable, and $$E \in \Omega(X)$$ is a set on which $$f$$ is bounded, say $$\lvert f \rvert \le c$$ on $$E$$. Then $$\text{Range}(\mu(E)) \subset W_f$$, and indeed $$\int_X \lvert f \rvert^2\,d\mu_\eta \le c^2 \left\| \eta \right\|^2$$ for every $$\eta \in \text{Range}(\mu(E))$$.

**Proof**
Let $$\eta \in \text{Range}(\mu(E))$$. By [**Lemma** *(Range Membership Concentrates the Associated Measure)*](#lmm:range-membership-concentrates-measure), $$\int_X \lvert f \rvert^2 \, d\mu_\eta = \int_E \lvert f \rvert^2 \, d\mu_\eta$$. Since $$\lvert f \rvert \le c$$ on $$E$$,

$$
    \int_E \lvert f \rvert^2 \, d\mu_\eta \le c^2 \mu_\eta(E) \le c^2 \mu_\eta(X) = c^2 \left< \eta, \mu(X)\eta \right> = c^2 \left< \eta,\eta \right> = c^2 \left\| \eta \right\|^2 < \infty,
$$

using $$\mu(X) = \mathbf{1}$$ (property 2 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure)). By the definition of $$W_f$$ in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2), $$\eta \in W_f$$.$$\blacksquare$$


With **Proposition** *(hall-10.2)* established, we can now give the definition and existence/uniqueness statement for the integral of an unbounded function against a projection-valued measure — this is the result we will actually invoke when discussing $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ in [Theorem 10.4](#thrm:hall-10.4).

> **Proposition**
<a name="prpstn:hall-10.1"></a>
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X, \Omega(X))$$ with values in $$\mathcal{B}(\mathbf{H})$$ and $$f : X \to \mathbb{C}$$ is a measurable function, not necessarily bounded. Let $$W_f$$, $$Q_f$$, and $$L_f$$ be as in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2). Then there exists a unique unbounded operator on $$\mathbf{H}$$, with domain $$W_f$$ — which we denote by $$\int_X f \, d\mu$$ — with the property that
>
> $$
>     \left< \phi, \left( \int_X f \, d\mu \right) \psi \right> = L_f(\phi, \psi)
> $$
>
> for all $$\phi, \psi \in W_f$$. In particular, taking $$\phi = \psi$$,
>
> $$
>     \left< \psi, \left( \int_X f \, d\mu \right) \psi \right> = Q_f(\psi) = \int_X f(\lambda) \, d\mu_\psi(\lambda)
> $$
>
> for all $$\psi \in W_f$$. Moreover, for every $$\psi \in W_f$$,
>
> $$
>     \left\| \left( \int_X f \, d\mu \right) \psi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi.
> $$

**Proof**
For $$\psi \in W_f$$, define $$\left( \int_X f \, d\mu \right) \psi \equiv \chi_\psi$$, the vector supplied by Part 3 of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2), satisfying $$L_f(\phi, \psi) = \left< \phi, \chi_\psi \right>$$ for all $$\phi \in W_f$$ — this is exactly the off-diagonal identity claimed. Part 3 shows this assignment is linear in $$\psi$$, so it defines an unbounded operator on $$\mathbf{H}$$ with domain $$W_f$$, which is dense by Part 1.

For the diagonal identity, we check directly that $$Q_f(\psi) = L_f(\psi,\psi)$$ for any quadratic form $$Q_f$$ on $$W_f$$: substituting $$\phi = \psi$$ into the polarization formula and using property 1 of the [definition of a quadratic form](#def:hall-quadratic-form-on-a-subspace) ($$Q_f(\lambda\psi) = \lvert\lambda\rvert^2 Q_f(\psi)$$) to evaluate $$Q_f(2\psi) = 4Q_f(\psi)$$ and $$Q_f\big((1+i)\psi\big) = \lvert 1+i \rvert^2 Q_f(\psi) = 2Q_f(\psi)$$,

$$
\begin{align}
    L_f(\psi,\psi) &= \frac{1}{2}\big[ Q_f(2\psi) - 2Q_f(\psi) \big] - \frac{i}{2}\big[ Q_f((1+i)\psi) - Q_f(\psi) - Q_f(i\psi) \big] \\
                   &= \frac{1}{2}\big[ 4Q_f(\psi) - 2Q_f(\psi) \big] - \frac{i}{2}\big[ 2Q_f(\psi) - Q_f(\psi) - Q_f(\psi) \big] \\
                   &= Q_f(\psi) - \frac{i}{2}\cdot 0 = Q_f(\psi).
\end{align}
$$

Taking $$\phi = \psi$$ in the just-established off-diagonal identity therefore gives $$\left< \psi, \chi_\psi \right> = L_f(\psi,\psi) = Q_f(\psi) = \int_X f \, d\mu_\psi$$, the diagonal identity. The norm formula is the formula $$\left\| \chi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi$$ from Part 3.

For uniqueness: if $$A_1$$ and $$A_2$$ are two unbounded operators with domain $$W_f$$ both satisfying $$\left< \psi, A_i \psi \right> = \int_X f \, d\mu_\psi$$ for all $$\psi \in W_f$$, then $$A_1$$ and $$A_2$$ induce the same quadratic form $$R(\psi) \equiv \left< \psi, A_i\psi \right>$$ on $$W_f$$ (the same for $$i=1,2$$, both equal to $$\int_X f\,d\mu_\psi$$). By Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties), applied once with $$T = A_1$$ and once with $$T = A_2$$, the sesquilinear form $$L_R$$ associated to $$R$$ satisfies both $$L_R(\phi,\psi) = \left< \phi, A_1\psi \right>$$ and $$L_R(\phi,\psi) = \left< \phi, A_2\psi \right>$$ for all $$\phi,\psi \in W_f$$ — the same $$L_R$$ in both cases, since it is defined purely in terms of $$R$$, which is common to both. Hence $$\left< \phi, A_1\psi \right> = \left< \phi, A_2 \psi \right>$$ for all $$\phi, \psi \in W_f$$. Fixing $$\psi$$, this says $$A_1\psi$$ and $$A_2\psi$$ agree in inner product against every $$\phi$$ in the dense subset $$W_f$$, so $$A_1\psi = A_2\psi$$ by [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot). As $$\psi \in W_f$$ was arbitrary, $$A_1 = A_2$$.$$\blacksquare$$

The next proposition records a natural compatibility check, confirming that [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) is a genuine extension of the previous post's construction rather than merely an analogue of it: for bounded $$f$$, the two constructions agree.

> **Proposition** *(Coincidence with the Bounded Integral)*
<a name="prpstn:coincidence-with-the-bounded-integral"></a>
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
> If $$f$$ is bounded, then $$W_f = \mathbf{H}$$, and the operator $$\int_X f \, d\mu$$ of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) coincides with the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration) $$\int_X f \, d\mu \in \mathcal{B}(\mathbf{H})$$ of the previous post.

**Proof**
If $$f$$ is bounded, $$\mu_\psi$$ is a finite measure for every $$\psi$$ (as always), so $$\int_X \lvert f \rvert^2 \, d\mu_\psi < \infty$$ automatically and $$W_f = \mathbf{H}$$. Writing $$A_1$$ for the operator of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) and $$A_2$$ for the bounded integral, both satisfy $$\left< \psi, A_i\psi \right> = \int_X f \, d\mu_\psi$$ for all $$\psi \in \mathbf{H}$$ — for $$A_1$$, this is the defining property of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1); for $$A_2$$, it is the defining property of the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration). The uniqueness argument just given (with $$W_f = \mathbf{H}$$ throughout) applies verbatim and gives $$A_1 = A_2$$.$$\blacksquare$$

We close this section with the fact we will actually need about $$\int_X f \, d\mu$$: when $$f$$ is real-valued, the resulting operator is self-adjoint. This is exactly what will let us conclude, in the proof of [Theorem 10.4](#thrm:hall-10.4), that the operator $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ we construct is self-adjoint (as it must be, to have any chance of equalling the self-adjoint operator $$A$$). The proof uses [Proposition (Orthogonal Decomposition and the Double Complement)](#prpstn:hall-a.49) from earlier.

> **Proposition**
<a name="prpstn:hall-10.3"></a>
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-a.45} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.26-internal} -->
<!--  \uses{prpstn:countable-additivity-of-the-integral} -->
<!--  \uses{prpstn:integrals-agree-when-measures-agree} -->
<!--  \uses{lmm:bounded-on-set-range-in-domain} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.62} -->
<!--  \uses{def:internal-orthogonal-decomposition} -->
<!--  \uses{lmm:internal-decomposition-unitary} -->
<!--  \uses{prpstn:hall-a.49} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{lmm:norm-convergent-decomposition} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> If $$f$$ is a real-valued, measurable function on $$X$$, then $$\int_X f \, d\mu$$ is self-adjoint on $$W_f$$.

**Proof**
Write $$A_f \equiv \int_X f \, d\mu$$. For $$n \in \mathbb{N} = \{1, 2, 3, \ldots\}$$, let $$F_n \equiv \{ x \in X \mid n - 1 \le \lvert f(x) \rvert < n \}$$, so the $$F_n$$ are pairwise disjoint with $$\bigcup_n F_n = X$$, and let $$\mathbf{H}_n \equiv \text{Range}(\mu(F_n))$$, a closed subspace of $$\mathbf{H}$$ (the range of a bounded orthogonal projection is always closed, being itself the kernel of the complementary projection $$\mathbf{1} - \mu(F_n)$$, which is bounded hence continuous), and hence itself a separable, complex Hilbert space with the inner product inherited from $$\mathbf{H}$$ (possibly $$\mathbf{H}_n = \{0\}$$, if $$F_n$$ happens to be a $$\mu$$-null set — this degenerate case is mathematically harmless throughout what follows, imposing no extra hypotheses, though a formalization should confirm the relevant library lemmas do not implicitly assume nontriviality). By [Lemma (Range Membership Concentrates the Associated Measure)](#lmm:range-membership-concentrates-measure), for any $$\eta \in \mathbf{H}_n$$, using $$\lvert f \rvert < n$$ on $$F_n$$,

$$
    \int_X \lvert f \rvert^2 \, d\mu_\eta = \int_{F_n} \lvert f \rvert^2 \, d\mu_\eta \le n^2 \mu_\eta(F_n) \le n^2 \mu_\eta(X) = n^2 \left\| \eta \right\|^2 < \infty.
$$

In particular $$\eta \in W_f$$, so, by the norm formula of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1), this reads $$\left\| A_f \eta \right\|^2 \le n^2 \left\| \eta \right\|^2$$, i.e. $$\left\| A_f \eta \right\| \le n \left\| \eta \right\|$$, for every $$\eta \in \mathbf{H}_n$$ — a bound on the size of $$A_f \eta$$ in $$\mathbf{H}$$, valid regardless of which subspace $$A_f \eta$$ actually lands in. By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) and the defining property of $$A_f$$, $$\lvert Q_f(\eta) \rvert = \lvert \left< \eta, A_f\eta \right> \rvert \le \left\| \eta \right\| \left\| A_f \eta \right\| \le n \left\| \eta \right\|^2$$, so $$Q_f$$, restricted to $$\mathbf{H}_n$$, is also a bounded quadratic form (bound $$n$$).

We first record a small fact about $$\mathbf{H}_n$$ that we will use twice: for $$\xi \in \mathbf{H}_n = \text{Range}(\mu(F_n))$$ and any $$E \in \Omega(X)$$, $$\mu(E)\xi \in \mathbf{H}_n$$. Since $$\xi \in \text{Range}(\mu(F_n))$$, idempotency gives $$\mu(F_n)\xi = \xi$$. Using this and property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure), we compute the two expressions

$$
    \mu(E)\xi = \mu(E)\mu(F_n)\xi = \mu(E \cap F_n)\xi
    \qquad\text{and}\qquad
    \mu(F_n)\mu(E)\xi = \mu(F_n \cap E)\xi.
$$

Since $$E \cap F_n = F_n \cap E$$, the right-hand sides agree, so $$\mu(F_n)\big[\mu(E)\xi\big] = \mu(E)\xi$$: that is, $$\mu(E)\xi$$ is fixed by $$\mu(F_n)$$, and hence $$\mu(E)\xi \in \text{Range}(\mu(F_n)) = \mathbf{H}_n$$.

Fix $$\psi \in \mathbf{H}_n$$, so $$\mu(F_n)\psi = \psi$$. Suppose first that $$\phi \in \mathbf{H}_n^\perp \cap W_f$$ (not yet all of $$\mathbf{H}_n^\perp$$ — see below). For any $$E \in \Omega(X)$$, the fact above gives $$\mu(E)\psi \in \mathbf{H}_n$$, so $$\left< \phi, \mu(E)\psi \right> = 0$$, as $$\phi \in \mathbf{H}_n^\perp$$; and, since $$\mu(E)$$ is self-adjoint, $$\left< \psi, \mu(E)\phi \right> = \overline{\left< \mu(E)\phi, \psi \right>} = \overline{\left< \phi, \mu(E)\psi \right>} = 0$$ as well. Hence

$$
    \mu_{\phi+\psi}(E) = \left< \phi + \psi, \mu(E)(\phi+\psi) \right> = \mu_\phi(E) + \mu_\psi(E) + \left< \phi, \mu(E)\psi \right> + \left< \psi, \mu(E)\phi \right> = \mu_\phi(E) + \mu_\psi(E)
$$

for every $$E \in \Omega(X)$$, i.e. $$\mu_{\phi+\psi} = \mu_\phi + \mu_\psi$$ as measures, so $$Q_f(\phi+\psi) = Q_f(\phi) + Q_f(\psi)$$. Since $$\phi \in W_f$$ and $$\psi \in \mathbf{H}_n \subset W_f$$, all of $$\phi, \psi, \phi+\psi, \phi+i\psi, i\psi$$ lie in $$W_f$$ (a subspace), and the identical argument with $$i\psi$$ in place of $$\psi$$ (still in $$\mathbf{H}_n$$, since $$\mathbf{H}_n$$ is a subspace) gives $$Q_f(\phi + i\psi) = Q_f(\phi) + Q_f(i\psi)$$. By the polarization formula defining $$L_f$$ in terms of $$Q_f$$, both differences $$Q_f(\phi+\psi) - Q_f(\phi) - Q_f(\psi)$$ and $$Q_f(\phi+i\psi) - Q_f(\phi) - Q_f(i\psi)$$ vanish, so $$L_f(\phi, \psi) = 0$$. By the defining property of $$A_f$$ from [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1), $$\left< \phi, A_f\psi \right> = L_f(\phi,\psi) = 0$$ for every $$\phi \in \mathbf{H}_n^\perp \cap W_f$$.

We now extend this to all of $$\mathbf{H}_n^\perp$$, using density. Let $$\phi \in \mathbf{H}_n^\perp$$ be arbitrary, and set $$E_m \equiv \{ x \in X \mid \lvert f(x) \rvert < m \}$$ for $$m \in \mathbb{N}$$. Since $$\lvert f \rvert \le m$$ on $$E_m$$, [**Lemma** *(Bounded on a Set Implies the Range Lies in the Domain)*](#lmm:bounded-on-set-range-in-domain) gives $$\mu(E_m)\phi \in \text{Range}(\mu(E_m)) \subset W_f$$ for every $$m$$; and, taking $$F_1 \equiv E_1$$, $$F_m \equiv E_m \setminus E_{m-1}$$ for $$m \ge 2$$ (pairwise disjoint with $$\bigcup_m F_m = \bigcup_m E_m = X$$, since $$f$$ is finite-valued, and with $$\bigcup_{j=1}^m F_j = E_m$$), Part 2 of [**Lemma** *(Norm-Convergent Decomposition over a Disjoint Cover)*](#lmm:norm-convergent-decomposition) gives $$\mu(E_m)\phi \to \phi$$ as $$m \to \infty$$. We claim, moreover, $$\mu(E_m)\phi \in \mathbf{H}_n^\perp$$: for any $$\eta \in \mathbf{H}_n$$, the fact established above (applied to $$\xi = \eta$$ and $$E = E_m$$) gives $$\mu(E_m)\eta \in \mathbf{H}_n$$, so, using self-adjointness of $$\mu(E_m)$$,

$$
    \left< \eta, \mu(E_m)\phi \right> = \left< \mu(E_m)\eta, \phi \right> = 0,
$$

the last equality because $$\mu(E_m)\eta \in \mathbf{H}_n$$ and $$\phi \in \mathbf{H}_n^\perp$$. As $$\eta \in \mathbf{H}_n$$ was arbitrary, $$\mu(E_m)\phi \in \mathbf{H}_n^\perp$$. So $$\mu(E_m)\phi \in \mathbf{H}_n^\perp \cap W_f$$ for every $$m$$, and $$\mu(E_m)\phi \to \phi$$: this shows $$\mathbf{H}_n^\perp \cap W_f$$ is dense in $$\mathbf{H}_n^\perp$$.

By the previous paragraph, $$\left< \mu(E_m)\phi, A_f\psi \right> = 0$$ for every $$m$$. By [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), letting $$m \to \infty$$,

$$
    \left< \phi, A_f\psi \right> = \lim_{m \to \infty} \left< \mu(E_m)\phi, A_f\psi \right> = 0.
$$

As $$\phi \in \mathbf{H}_n^\perp$$ was arbitrary, $$A_f\psi$$ is orthogonal to all of $$\mathbf{H}_n^\perp$$, i.e. $$A_f\psi \in \left( \mathbf{H}_n^\perp \right)^\perp$$. Since $$\mathbf{H}_n$$ is closed, [**Proposition** *(Orthogonal Decomposition and the Double Complement)*](#prpstn:hall-a.49) gives $$\left( \mathbf{H}_n^\perp \right)^\perp = \mathbf{H}_n$$, so $$A_f\psi \in \mathbf{H}_n$$.

So $$A_f$$ maps $$\mathbf{H}_n$$ into itself; let $$A_n$$ denote this restriction. Combined with the bound $$\left\| A_f \eta \right\| \le n \left\| \eta \right\|$$ established above (for $$\eta \in \mathbf{H}_n$$, where $$A_f\eta = A_n\eta \in \mathbf{H}_n$$), $$A_n$$ is a genuine bounded operator on $$\mathbf{H}_n$$, with operator norm at most $$n$$, and satisfies $$\left< \psi, A_n\psi \right> = \left< \psi, A_f\psi \right> = Q_f(\psi)$$ for all $$\psi \in \mathbf{H}_n$$. Since $$Q_f$$, restricted to $$\mathbf{H}_n$$, is a bounded quadratic form (shown above) that is real-valued (as $$f$$ is real-valued, so $$Q_f(\psi) = \int_X f \, d\mu_\psi \in \mathbb{R}$$, an integral of a real-valued function against a positive real measure), [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63), applied with $$\mathbf{H}_n$$ in place of $$\mathbf{H}$$, produces a *unique* bounded operator on $$\mathbf{H}_n$$ representing this quadratic form, and asserts that this unique operator is self-adjoint. As $$A_n$$ is itself a bounded operator on $$\mathbf{H}_n$$ representing $$Q_f$$, uniqueness forces $$A_n$$ to be that operator, so $$A_n$$ is self-adjoint on $$\mathbf{H}_n$$.

Now, $$\{ \mathbf{H}_n \}_{n=1}^\infty$$ is an *internal orthogonal decomposition* of $$\mathbf{H}$$ in the sense of [Definition (Internal Orthogonal Decomposition)](#def:internal-orthogonal-decomposition). We check its two conditions.

*Pairwise orthogonality.* The $$F_n$$ are pairwise disjoint, so for $$n \ne m$$, property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) gives $$\mu(F_n)\mu(F_m) = \mu(F_n \cap F_m) = \mu(\emptyset) = 0$$. Hence for $$\eta \in \mathbf{H}_n$$ and $$\zeta \in \mathbf{H}_m$$, using $$\mu(F_n)\eta = \eta$$ and $$\mu(F_m)\zeta = \zeta$$ (idempotency, as both lie in the respective ranges) and self-adjointness of $$\mu(F_n)$$,

$$
    \left< \eta, \zeta \right> = \left< \mu(F_n)\eta, \mu(F_m)\zeta \right> = \left< \eta, \mu(F_n)\mu(F_m)\zeta \right> = \left< \eta, 0 \right> = 0.
$$

*Decomposition.* By [Lemma (Norm-Convergent Decomposition over a Disjoint Cover)](#lmm:norm-convergent-decomposition) applied to $$\{F_n\}$$ (pairwise disjoint with union $$X$$), every $$\psi \in \mathbf{H}$$ satisfies $$\psi = \sum_{n=1}^\infty \mu(F_n)\psi$$, norm-convergent, with $$\mu(F_n)\psi \in \text{Range}(\mu(F_n)) = \mathbf{H}_n$$.

So $$\{\mathbf{H}_n\}$$ is an internal orthogonal decomposition of $$\mathbf{H}$$, each $$\mathbf{H}_n$$ being a separable closed subspace (shown at the start of this proof). Writing $$\psi_n \equiv \mu(F_n)\psi$$ for the components of $$\psi$$, Part 2 of [**Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*](#lmm:internal-decomposition-unitary) gives $$\left\| \psi \right\|^2 = \sum_n \left\| \psi_n \right\|^2$$, and Part 1 gives uniqueness of this decomposition — so the components $$\psi_n$$ referred to below are unambiguous.

Identifying $$\mathbf{H}$$ with sequences $$\psi = (\psi_1, \psi_2, \ldots)$$, $$\psi_n \in \mathbf{H}_n$$: for $$\psi \in \bigoplus_{n=1}^N \mathbf{H}_n$$ a finite sum (so $$\psi = \sum_{n=1}^N \psi_n \in W_f$$, since $$W_f$$ is a subspace and $$\mathbf{H}_n \subset W_f$$ for each $$n$$, shown above), linearity of $$A_f$$ on $$W_f$$ together with $$A_f$$ mapping each $$\mathbf{H}_n$$ to itself via $$A_n$$ gives $$A_f\psi = \sum_{n=1}^N A_n\psi_n$$, matching the formula in [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) on the finite direct sum. It remains to identify $$W_f$$ itself with the domain $$V$$ of that proposition. For any $$\psi = (\psi_1,\psi_2,\ldots) \in \mathbf{H}$$ (not assumed to lie in $$W_f$$ or to be a finite sum), countable additivity of $$\mu_\psi$$ over the pairwise disjoint $$F_n$$'s gives $$\mu_\psi(X) = \sum_n \mu_\psi(F_n)$$, and, more generally, restricting to any measurable $$E \subset X$$, $$\mu_\psi(E) = \sum_n \mu_\psi(E \cap F_n)$$; taking $$E \subset F_n$$ shows $$\mu_\psi$$ restricted to $$F_n$$ agrees with $$\mu_{\psi_n}$$ restricted to $$F_n$$ — indeed $$\mu_{\psi_n}(E) = \left< \mu(F_n)\psi, \mu(E)\mu(F_n)\psi \right> = \left< \psi, \mu(F_n)\mu(E)\mu(F_n)\psi \right> = \left< \psi, \mu(E \cap F_n)\psi \right> = \mu_\psi(E)$$ for $$E \subset F_n$$, using self-adjointness and idempotency of $$\mu(F_n)$$ and property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure). Hence

$$
    \int_X \lvert f \rvert^2 \, d\mu_\psi = \sum_n \int_{F_n} \lvert f \rvert^2 \, d\mu_\psi = \sum_n \int_{F_n} \lvert f \rvert^2 \, d\mu_{\psi_n} = \sum_n \int_X \lvert f \rvert^2 \, d\mu_{\psi_n} = \sum_n \left\| A_n \psi_n \right\|_n^2,
$$

where the first equality is countable additivity of the integral over the $$F_n$$'s (as for $$\mu_\psi$$ above), the third uses $$\mu_{\psi_n}(F_n^c) = 0$$ (shown at the start of this proof, applied to $$\eta = \psi_n$$), and the last is the norm formula of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) applied within $$\mathbf{H}_n$$. This holds for *every* $$\psi \in \mathbf{H}$$, with both sides possibly infinite, so it identifies

$$
    W_f = \left\{ \psi \in \mathbf{H} \mid \int_X \lvert f \rvert^2 \, d\mu_\psi < \infty \right\} = \left\{ \psi = (\psi_1,\psi_2,\ldots) \;\middle|\; \sum_n \left( \left\| \psi_n \right\|_n^2 + \left\| A_n\psi_n \right\|_n^2 \right) < \infty \right\},
$$

the second equality using that $$\psi \in \mathbf{H}$$ already forces $$\sum_n \left\| \psi_n \right\|_n^2 < \infty$$ (Parseval for the Hilbert space direct sum). This is exactly the domain $$V$$ in [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26).

We have shown: $$\{\mathbf{H}_n\}$$ is an internal orthogonal decomposition of $$\mathbf{H}$$ into separable closed subspaces, each $$A_n$$ is a bounded self-adjoint operator on $$\mathbf{H}_n$$, and $$A_f$$ is a symmetric operator (we check this directly: for $$\phi, \psi \in W_f$$, $$\left< \phi, A_f\psi \right> = L_f(\phi,\psi)$$ and $$\left< A_f\phi, \psi \right> = \overline{\left< \psi, A_f\phi \right>} = \overline{L_f(\psi,\phi)}$$; Part 2 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties), applicable since $$Q_f$$ is real-valued, gives $$L_f(\phi,\psi) = \overline{L_f(\psi,\phi)}$$, so $$\left< \phi, A_f\psi \right> = \left< A_f\phi, \psi \right>$$) whose domain contains the algebraic span $$W_0$$ of the $$\mathbf{H}_n$$'s (finite sums), and which acts as $$A_n$$ on each $$\mathbf{H}_n$$. This is exactly the hypothesis of [**Proposition** *(Direct Sums of Bounded Self-Adjoint Operators, Internal Form)*](#prpstn:hall-9.26-internal), which concludes that $$A_f$$ is essentially self-adjoint with $$\text{Dom}(A_f^{\text{cl}}) = \text{Dom}(A_f^*)$$ equal to the space $$V$$ identified there — which we showed above coincides with $$W_f = \text{Dom}(A_f)$$. Since $$A_f$$ is symmetric, [**Proposition** *(Symmetric Operators and the Adjoint)*](#prpstn:hall-9.4) shows $$A_f^*$$ is an extension of $$A_f$$, and having just shown $$\text{Dom}(A_f^*) = \text{Dom}(A_f)$$, this extension is trivial: $$A_f^* = A_f$$, i.e. $$A_f$$ is self-adjoint.$$\blacksquare$$

## The Spectral Theorem for Bounded Normal Operators

Every bounded self-adjoint operator is a special case of a broader, and for our purposes essential, class: the *normal* operators. The Cayley transform, developed in the next section, produces from a self-adjoint (possibly unbounded) operator a bounded operator that is generally not self-adjoint but is always normal — so to make the reduction work, we need the spectral theorem for bounded normal operators, not just bounded self-adjoint ones.

> **Definition** *(Normal Operator)*
<a name="def:hall-10.19"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> A bounded operator $$A$$ on $$\mathbf{H}$$ is *normal* if $$A$$ commutes with its adjoint: $$AA^* = A^*A$$.

Every bounded self-adjoint operator is normal (trivially, $$A A^* = A^2 = A^*A$$), but the class is genuinely larger — for instance every unitary operator is normal ($$UU^* = U^*U = \mathbf{1}$$), and unitary operators are generally not self-adjoint. Unlike the self-adjoint case, the spectrum of a normal operator need not lie on the real line at all.

Hall's proof that the bounded self-adjoint spectral theorem extends to normal operators proceeds in two stages, mirroring the two-stage proof of the self-adjoint case itself. The first stage builds a continuous functional calculus for $$A$$; the second turns that functional calculus into a projection-valued measure. Hall's own observation is that this second stage, once a continuous functional calculus is in hand, uses nothing about the operator beyond the functional calculus itself — not self-adjointness, not realness of the spectrum. Rather than treat this as license to say the self-adjoint case's construction "carries over unchanged" — citing one proof to justify another, exactly the pattern [**Lemma** *(The $$b^2$$ Inequality for Symmetric Operators)*](#lmm:b-squared-inequality-symmetric) and [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) were introduced earlier to avoid — when we reach that stage we will extract the construction as its own proposition, parameterized by an abstract continuous functional calculus on a compact metric space, so that the self-adjoint and normal cases each cite that one statement rather than one citing the other's proof. For now, our task is the first stage: building the continuous functional calculus for a normal operator.

For a self-adjoint operator, this calculus was built by approximating continuous *real-valued* functions on the (real) spectrum by real polynomials in $$\lambda$$, using the real Stone–Weierstrass theorem. For a normal operator, $$\sigma(A)$$ is a general compact subset of $$\mathbb{C}$$, and we need to approximate *complex-valued* functions; the complex-valued Stone–Weierstrass theorem requires an algebra of functions closed under complex conjugation, so plain polynomials in $$\lambda$$ no longer suffice — we need polynomials in $$\lambda$$ *and* $$\overline{\lambda}$$. On the operator side, the counterpart to conjugation is the adjoint, so a polynomial $$p(\lambda,\overline\lambda)$$ should correspond to the operator $$p(A,A^*)$$ obtained by substituting $$A$$ for $$\lambda$$ and $$A^*$$ for $$\overline\lambda$$. This substitution is where normality is essential: the polynomial ring $$\mathbb{C}[\lambda,\overline\lambda]$$ is commutative, so a given function $$p(\lambda,\overline\lambda)$$ has a unique representation as such a polynomial — but substituting $$\lambda \mapsto A$$, $$\overline\lambda \mapsto A^*$$ turns this into an expression in the generally *non*commutative algebra $$\mathcal{B}(\mathbf{H})$$, and the substitution is well defined as an algebra homomorphism only if it respects every relation that holds in the source ring — in particular $$\lambda\overline\lambda = \overline\lambda\lambda$$, which forces $$AA^* = A^*A$$. Without normality, there would be nothing to substitute *into*: no consistent way to assign a single operator to $$p(\lambda,\overline\lambda)$$ independent of how it is written.

The key technical result we are aiming for is a version of the spectral mapping theorem for this two-variable substitution: $$\sigma\big(p(A,A^*)\big) = \big\{ p(\lambda,\overline\lambda) \mid \lambda \in \sigma(A) \big\}$$. Unlike the ordinary (one-variable) spectral mapping theorem, this is genuinely harder to prove, and the route we follow — matching Hall's — uses the bounded self-adjoint spectral theorem itself, applied to an auxiliary self-adjoint operator, together with the notion of an *almost eigenvector*.

We start with a fact that will let us compute the norm of $$p(A,A^*)$$ once we know its spectrum: for normal operators, the operator norm equals the spectral radius, exactly as for self-adjoint operators. Proving this needs one general fact about spectral radii of commuting operators that is not yet available to us, and whose proof requires knowing that the powers of a bounded operator cannot grow faster than the spectral radius suggests.

We can establish the growth bound on powers of a bounded operator that Lemma 10.22 below will need using exactly the tools already assembled in the previous post's proof of the bounded self-adjoint case of norm-equals-spectral-radius — that proof, in fact, establishes a fact about *any* bounded operator (self-adjointness enters only in its final step, where it is used for a sharper conclusion we do not need here). We extract that general fact as its own lemma, citing the same tools directly, rather than repeating "self-adjoint" hypotheses we will not use. First, though, we need three facts about the resolvent that are established along the way in the previous post's proof of [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5), but do not appear in that proposition's own statement; we extract them here as their own citable facts.

> **Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*
<a name="prpstn:resolvent-holomorphy-and-neumann-series"></a>
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
<!--  \uses{../spectral-theorems/#lmm:hall-7.6} -->
> Suppose $$A \in \mathcal{B}(\mathbf{H})$$.
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
**Part 2.** By [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5), $$\lvert \lambda \rvert>\|A\|$$ implies $$\lambda$$ is in the resolvent set. For such $$\lambda$$, $$A - \lambda\mathbf{1} = -\lambda(\mathbf{1} - A/\lambda)$$ with $$\|A/\lambda\| < 1$$, so by the geometric series lemma [**Lemma** *(hall-7.6)*](../spectral-theorems/#lmm:hall-7.6), $$\mathbf{1} - A/\lambda$$ is invertible with $$(\mathbf{1}-A/\lambda)^{-1} = \sum_{m=0}^\infty (A/\lambda)^m$$, operator-norm convergent; hence $$(A-\lambda\mathbf{1})^{-1} = -\frac{1}{\lambda}\sum_{m=0}^\infty (A/\lambda)^m = -\sum_{m=0}^\infty A^m/\lambda^{m+1}$$.

**Part 1.** Openness of the resolvent set, and the local power series representation, both follow from the same algebraic factorization used to prove [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5) itself: for $$\lambda_0$$ in the resolvent set of $$A$$ and $$\lambda$$ with $$\lvert \lambda-\lambda_0 \rvert < 1/\|(A-\lambda_0\mathbf{1})^{-1}\|$$, writing $$A - \lambda\mathbf{1} = (A-\lambda_0\mathbf{1})\big(\mathbf{1} - (\lambda-\lambda_0)(A-\lambda_0\mathbf{1})^{-1}\big)$$ and applying [**Lemma** *(hall-7.6)*](../spectral-theorems/#lmm:hall-7.6) to the second factor (whose norm is less than $$1$$ by the bound on $$\lvert \lambda-\lambda_0 \rvert$$) shows $$\lambda$$ is again in the resolvent set — so the resolvent set is open — with

$$
    (A-\lambda\mathbf{1})^{-1} = \left( \sum_{m=0}^\infty (\lambda-\lambda_0)^m \big((A-\lambda_0\mathbf{1})^{-1}\big)^m \right)(A-\lambda_0\mathbf{1})^{-1},
$$

an operator-norm-convergent power series in $$(\lambda-\lambda_0)$$ with $$\mathcal{B}(\mathbf{H})$$ coefficients.$$\blacksquare$$

An operator-norm-convergent power series composed with any bounded linear functional gives a convergent scalar power series with the same radius of convergence, so Part 1 immediately gives: for any bounded linear functional $$\xi$$ on $$\mathcal{B}(\mathbf{H})$$, the scalar function $$\lambda \mapsto \xi\big( (A-\lambda\mathbf{1})^{-1} \big)$$ is holomorphic on the (open) resolvent set of $$A$$ — this is the fact [**Lemma** *(hall-8.1)*](../spectral-theorems/#lmm:hall-8.1) uses for a general such $$\xi$$, and the one we need below.

> **Lemma** *(Power Growth is Controlled by the Spectral Radius)*
<a name="lmm:power-growth-controlled-by-spectral-radius"></a>
<!--  \uses{../spectral-theorems/#def:spectral-radius} -->
<!--  \uses{prpstn:resolvent-holomorphy-and-neumann-series} -->
<!--  \uses{../spectral-theorems/#thrm:laurents-theorem} -->
<!--  \uses{../spectral-theorems/#lmm:nth-term-test} -->
<!--  \uses{../spectral-theorems/#thrm:hall-a.40} -->
<!--  \uses{../spectral-theorems/#thrm:theorem-on-completeness-of-the-dual} -->
<!--  \uses{../spectral-theorems/#lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{thrm:norm-via-dual-pairing} -->
<!--  \uses{../spectral-theorems/#crllr:crllr-1} -->
> Suppose $$A \in \mathcal{B}(\mathbf{H})$$ and $$T \in \mathbb{R}$$ with $$T > R(A)$$. Then
>
> $$
>     \lim_{m \to \infty} \frac{\|A^m\|}{T^m} = 0.
> $$

**Proof**
Fix $$\lambda_1 \in \mathbb{C}$$ with $$R(A) < \lvert \lambda_1 \rvert < T$$ (possible since $$R(A) < T$$). We first show there is a constant $$C < \infty$$ with $$\|A^m\| \le C\lvert \lambda_1 \rvert^{m+1}$$ for all $$m$$.

By Part 1 of [**Proposition** *(Operator-Norm Holomorphy and the Neumann Series of the Resolvent)*](#prpstn:resolvent-holomorphy-and-neumann-series), the resolvent set of $$A$$ is open and the resolvent is holomorphic (in the operator-norm sense) on it; this resolvent set contains $$\{ \lambda : \lvert \lambda \rvert > R(A) \}$$ (since $$\sigma(A) \subset \{ \lvert \lambda \rvert \le R(A) \}$$, by the [definition of the spectral radius](../spectral-theorems/#def:spectral-radius)), so the resolvent is holomorphic on all of the open annulus $$R(A) < \lvert \lambda \rvert$$. By Part 2 of the same proposition, for $$\lvert \lambda \rvert > \|A\|$$,

$$
    (A - \lambda\mathbf{1})^{-1} = -\sum_{m=0}^\infty \frac{A^m}{\lambda^{m+1}},
$$

convergent in operator norm.

Fix a bounded linear functional $$\xi$$ on $$\mathcal{B}(\mathbf{H})$$. As just noted, $$\lambda \mapsto \xi\big((A-\lambda\mathbf{1})^{-1}\big)$$ is holomorphic on the open annulus $$R(A) < \lvert \lambda \rvert$$, so by [**Laurent's Theorem**](../spectral-theorems/#thrm:laurents-theorem) it has a unique Laurent series expansion there, convergent throughout that annulus. Applying $$\xi$$ termwise to the operator-norm-convergent series above (valid for $$\lvert \lambda \rvert>\|A\|$$) gives a second expansion, $$-\sum_m \xi(A^m)/\lambda^{m+1}$$, which is a Laurent series (all terms of non-positive integer power) valid, a priori, only on the smaller annulus $$\|A\| < \lvert \lambda \rvert$$. On the overlap of the two annuli — which is exactly $$\|A\| < \lvert \lambda \rvert$$, since $$R(A) \le \|A\|$$ by [**Corollary**](../spectral-theorems/#crllr:crllr-1) — both expansions represent the same holomorphic function, so by the uniqueness clause of [**Laurent's Theorem**](../spectral-theorems/#thrm:laurents-theorem) (applied on that overlap), they are the same series: the coefficients agree. Hence the series $$-\sum_m \xi(A^m)/\lambda^{m+1}$$ *is* the unique Laurent series of $$\xi\big((A-\lambda\mathbf{1})^{-1}\big)$$ on the full annulus $$R(A) < \lvert \lambda \rvert$$ — and, Laurent's Theorem asserting convergence of that series throughout its annulus, it converges there, in particular at $$\lambda = \lambda_1$$.

By the [**Nth-Term Test**](../spectral-theorems/#lmm:nth-term-test), convergence of $$\sum_m \xi(A^m)/\lambda_1^{m+1}$$ forces its terms to tend to $$0$$, so in particular $$\{ \xi(A^m/\lambda_1^{m+1}) \}_m$$ is a bounded subset of $$\mathbb{C}$$, with some bound $$C_\xi$$ depending on $$\xi$$ (and on $$\lambda_1$$). As $$\xi$$ ranges over all bounded linear functionals on $$\mathcal{B}(\mathbf{H})$$ — a Banach space, by [**Lemma** *(Bounded Operators form a Banach Space)*](../spectral-theorems/#lmm:bounded-operators-form-a-banach-space), and so, by the [**Theorem on Completeness of the Dual**](../spectral-theorems/#thrm:theorem-on-completeness-of-the-dual), its dual $$\mathcal{B}(\mathbf{H})^*$$ is itself a Banach space — the [**Principle of Uniform Boundedness**](../spectral-theorems/#thrm:hall-a.40), applied with $$V_1 = \mathcal{B}(\mathbf{H})^*$$, $$V_2 = \mathbb{C}$$, and the family of evaluation maps $$\xi \mapsto \xi(A^m/\lambda_1^{m+1})$$ (each pointwise-bounded in $$m$$ by $$C_\xi$$, just shown), gives a constant $$C < \infty$$, independent of $$\xi$$, such that these evaluation maps have norm at most $$C$$ as elements of $$\mathcal{B}(\mathbf{H})^{**}$$: $$\lvert \xi(A^m/\lambda_1^{m+1}) \rvert \le C \left\| \xi \right\|$$ for every $$\xi \in \mathcal{B}(\mathbf{H})^*$$ and every $$m$$.

To convert this into a bound on $$\|A^m/\lambda_1^{m+1}\|$$ itself, we use the standard corollary of the Hahn–Banach theorem identifying the norm of an element of a normed space with the supremum of its image under unit-norm functionals.

> **Theorem** *(Norm via Dual Pairing)*
<a name="thrm:norm-via-dual-pairing"></a>
> If $$x$$ is an element of a normed vector space $$V$$, then
>
> $$
>     \|x\| = \sup \{ \lvert \xi(x) \rvert : \xi \in V^*,\ \|\xi\| \le 1 \}.
> $$

Applying [**Theorem** *(Norm via Dual Pairing)*](#thrm:norm-via-dual-pairing) with $$V = \mathcal{B}(\mathbf{H})$$ and $$x = A^m/\lambda_1^{m+1}$$: since $$\lvert \xi(A^m/\lambda_1^{m+1}) \rvert \le C\|\xi\|$$ for every $$\xi$$, taking the supremum over $$\|\xi\|\le 1$$ gives $$\|A^m/\lambda_1^{m+1}\| \le C$$, for every $$m$$. That is, $$\|A^m\| \le C\lvert \lambda_1 \rvert^{m+1}$$ for all $$m$$, as claimed.

Finally, since $$\lvert \lambda_1 \rvert < T$$,

$$
    \frac{\|A^m\|}{T^m} \le C\lvert \lambda_1 \rvert \left( \frac{\lvert \lambda_1 \rvert}{T} \right)^m \longrightarrow 0
$$

as $$m \to \infty$$, since $$\lvert \lambda_1 \rvert/T < 1$$. This is the desired result.$$\blacksquare$$

We now use this growth bound to establish submultiplicativity of the spectral radius for commuting operators.

> **Lemma**
<a name="lmm:hall-10.22"></a>
<!--  \uses{lmm:power-growth-controlled-by-spectral-radius} -->
<!--  \uses{../spectral-theorems/#def:spectral-radius} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
<!--  \uses{../spectral-theorems/#lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{../spectral-theorems/#crllr:crllr-1} -->
> If $$A$$ and $$B$$ are commuting elements of $$\mathcal{B}(\mathbf{H})$$, then
>
> $$
>     R(AB) \le R(A)R(B).
> $$

**Proof**
We first show: for *every* pair of real numbers $$S > R(A)$$ and $$T > R(B)$$,

$$
    \lim_{m \to \infty} \frac{\|(AB)^m\|}{S^mT^m} = 0. \tag{$\P$}
$$

Since $$A$$ and $$B$$ commute, $$(AB)^m = A^mB^m$$ for every $$m$$ (by induction: trivial for $$m=0,1$$, and if $$(AB)^m = A^mB^m$$ then $$(AB)^{m+1} = (AB)^mAB = A^mB^mAB = A^m(B^mA)B = A^m(AB^m)B = A^{m+1}B^{m+1}$$, using $$B^mA = AB^m$$, itself immediate by induction on $$m$$ from $$AB=BA$$). By submultiplicativity of the operator norm,

$$
    \frac{\|(AB)^m\|}{S^mT^m} = \frac{\|A^mB^m\|}{S^mT^m} \le \frac{\|A^m\|\|B^m\|}{S^mT^m} = \frac{\|A^m\|}{S^m}\cdot\frac{\|B^m\|}{T^m}.
$$

By [**Lemma** *(Power Growth is Controlled by the Spectral Radius)*](#lmm:power-growth-controlled-by-spectral-radius), applied to $$A$$ with $$T$$ there taken to be our $$S$$ (valid since $$S > R(A)$$), and to $$B$$ with $$T$$ there taken to be our $$T$$ (valid since $$T > R(B)$$), both factors on the right tend to $$0$$ as $$m \to \infty$$, giving $$(\P)$$.

Now fix real numbers $$S > R(A)$$ and $$T > R(B)$$ (for the remainder of the proof), and fix $$\lambda_1 \in \mathbb{C}$$ with $$\lvert \lambda_1 \rvert > ST$$, and $$\lambda_2$$ with $$\lvert \lambda_1 \rvert > \lvert \lambda_2 \rvert > ST$$. Applying $$(\P)$$ to the pair $$S' = S \cdot \lvert \lambda_2 \rvert/(ST)$$, $$T' = T$$ — so $$S'T' = \lvert \lambda_2 \rvert$$, and $$S' > R(A)$$ since $$\lvert \lambda_2 \rvert > ST$$ gives $$S' = S\lvert \lambda_2 \rvert/(ST) = \lvert \lambda_2 \rvert/T > S > R(A)$$, while $$T' = T > R(B)$$ trivially — the sequence $$\|(AB)^m\|/\lvert \lambda_2 \rvert^m$$ tends to $$0$$, so in particular is bounded: there is a constant $$C$$ with $$\|(AB)^m\| \le C\lvert \lambda_2 \rvert^m$$ for all $$m$$.

By [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5) applied to $$AB$$, for $$\lvert \lambda \rvert > \|AB\|$$,

$$
    (AB - \lambda\mathbf{1})^{-1} = -\sum_{m=0}^\infty \frac{(AB)^m}{\lambda^{m+1}}, \tag{$\P\P$}
$$

convergent in operator norm — but this alone only shows $$\lambda_1$$ is in the resolvent set of $$AB$$ when $$\lvert \lambda_1 \rvert > \|AB\|$$, which we do not know here ($$\lambda_1$$ was chosen only with $$\lvert \lambda_1 \rvert > ST \ge R(A)R(B)$$, and $$ST$$ may be far smaller than $$\|AB\|$$). Instead, we show directly that the series $$-\sum_m (AB)^m/\lambda_1^{m+1}$$, which converges in operator norm by the bound on $$\|(AB)^m\|$$ just derived — its terms have norm at most $$C\lvert \lambda_2 \rvert^m/\lvert \lambda_1 \rvert^{m+1}$$, dominated by a convergent geometric series since $$\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert<1$$, so the partial sums are Cauchy and converge by completeness of $$\mathcal{B}(\mathbf{H})$$ — defines a two-sided inverse of $$AB - \lambda_1\mathbf{1}$$.

Let $$S \equiv -\sum_{m=0}^\infty (AB)^m/\lambda_1^{m+1}$$ (the operator norm limit just established) and $$S_N \equiv -\sum_{m=0}^N (AB)^m/\lambda_1^{m+1}$$, so $$S_N \to S$$ as $$N \to \infty$$ by definition of the series' convergence. Expanding and re-indexing the first sum below with $$k=m+1$$,

$$
\begin{align}
    (AB-\lambda_1\mathbf{1})S_N &= (AB-\lambda_1\mathbf{1}) \left( -\sum_{m=0}^N \frac{(AB)^m}{\lambda_1^{m+1}} \right) \\
                                &= -\sum_{m=0}^N \frac{(AB)^{m+1}}{\lambda_1^{m+1}} + \sum_{m=0}^N \frac{(AB)^m}{\lambda_1^m} \\
                                &= -\sum_{k=1}^{N+1} \frac{(AB)^k}{\lambda_1^k} + \mathbf{1} + \sum_{m=1}^N \frac{(AB)^m}{\lambda_1^m} \\
                                &= \mathbf{1} - \frac{(AB)^{N+1}}{\lambda_1^{N+1}},
\end{align}
$$

the middle terms ($$k=m=1,\ldots,N$$) telescoping away. Since $$\|(AB)^{N+1}\|/\lvert \lambda_1 \rvert^{N+1} \le C\lvert \lambda_2 \rvert^{N+1}/\lvert \lambda_1 \rvert^{N+1} = C(\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert)^{N+1} \to 0$$ as $$N \to \infty$$ (using the same bound as above, with $$\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert<1$$), we get $$(AB-\lambda_1\mathbf{1})S_N \to \mathbf{1}$$. On the other hand, left multiplication by the fixed bounded operator $$AB - \lambda_1\mathbf{1}$$ is continuous in the operator norm (for any $$T_1,T_2 \in \mathcal{B}(\mathbf{H})$$, $$\|(AB-\lambda_1\mathbf{1})T_1 - (AB-\lambda_1\mathbf{1})T_2\| \le \|AB-\lambda_1\mathbf{1}\|\,\|T_1-T_2\|$$, by submultiplicativity), so $$(AB-\lambda_1\mathbf{1})S_N \to (AB-\lambda_1\mathbf{1})S$$ as well. By uniqueness of limits, $$(AB-\lambda_1\mathbf{1})S = \mathbf{1}$$. An identical computation — using that $$(AB)^m$$ commutes with $$AB-\lambda_1\mathbf{1}$$, being a power of $$AB$$ itself — gives $$S_N(AB-\lambda_1\mathbf{1}) = \mathbf{1} - (AB)^{N+1}/\lambda_1^{N+1} \to \mathbf{1}$$ and hence, by continuity of right multiplication by the fixed operator $$AB-\lambda_1\mathbf{1}$$, $$S(AB-\lambda_1\mathbf{1}) = \mathbf{1}$$. So $$S$$ is a two-sided inverse of $$AB - \lambda_1\mathbf{1}$$, and $$\lambda_1$$ is in the resolvent set of $$AB$$.

Since $$\lambda_1$$ with $$\lvert \lambda_1 \rvert > ST$$ was arbitrary, every such $$\lambda_1$$ is in the resolvent set of $$AB$$, so $$\sigma(AB) \subset \{ \lvert \lambda \rvert \le ST \}$$, giving $$R(AB) \le ST$$. As $$S > R(A)$$ and $$T > R(B)$$ were arbitrary, $$R(AB) \le R(A)R(B)$$.$$\blacksquare$$

We can now prove the equality of norm and spectral radius for normal operators, exactly as for self-adjoint operators. The proof needs two elementary properties of the adjoint of a bounded operator, neither yet available to us; we record them first.

> **Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*
<a name="lmm:adjoint-product-and-involution"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> For $$A, B \in \mathcal{B}(\mathbf{H})$$:
>
> 1. $$(AB)^* = B^*A^*$$.
> 2. $$(A^*)^* = A$$.

**Proof**
**Part 1.** For any $$\phi,\psi \in \mathbf{H}$$, applying the [definition of the adjoint](#def:hall-9.1) (for a bounded operator, with domain all of $$\mathbf{H}$$) to $$B$$ and then to $$A$$,

$$
    \left< \phi, (AB)\psi \right> = \left< \phi, A(B\psi) \right> = \left< A^*\phi, B\psi \right> = \left< B^*(A^*\phi), \psi \right> = \left< (B^*A^*)\phi, \psi \right>.
$$

As this holds for all $$\phi,\psi \in \mathbf{H}$$, this is exactly the defining property of $$(AB)^*$$, so $$(AB)^* = B^*A^*$$.

**Part 2.** For all $$\phi,\psi \in \mathbf{H}$$, using conjugate symmetry of the inner product twice and the [definition of the adjoint](#def:hall-9.1) applied to $$A$$ (in the form $$\left< A^*\psi,\phi\right> = \left<\psi,A\phi\right>$$, the conjugate-symmetric restatement of $$\left<\phi,A\psi\right>=\left<A^*\phi,\psi\right>$$ with $$\phi,\psi$$ swapped and both sides conjugated),

$$
    \left< \phi, A^*\psi \right> = \overline{\left< A^*\psi, \phi \right>} = \overline{\left< \psi, A\phi \right>} = \left< A\phi, \psi \right>.
$$

As this holds for all $$\phi,\psi\in\mathbf{H}$$, this is exactly the defining property of $$(A^*)^*$$ (applied to the operator $$A^*$$): it says $$A\phi$$ plays the role of $$(A^*)^*\phi$$ for every $$\phi$$, so $$(A^*)^*=A$$.$$\blacksquare$$

> **Proposition** *(Norm Equals Spectral Radius for Normal Operators)*
<a name="prpstn:hall-10.21"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{lmm:hall-10.22} -->
<!--  \uses{../spectral-theorems/#def:spectral-radius} -->
<!--  \uses{../spectral-theorems/#crllr:crllr-1} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-7.2} -->
<!--  \uses{../spectral-theorems/#lmm:hall-8.1} -->
<!--  \uses{lmm:adjoint-product-and-involution} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is normal, then $$\|A\| = R(A)$$.

**Proof**
By [**Corollary**](../spectral-theorems/#crllr:crllr-1), $$R(A) \le \|A\|$$ for any bounded operator. It remains to show $$\|A\| \le R(A)$$.

By [**Proposition** *(hall-7.2)*](../spectral-theorems/#prpstn:hall-7.2), $$\|A\|^2 = \|A^*A\|$$. Since $$A$$ is normal, $$A^*A = AA^*$$; note $$A^*A$$ is self-adjoint regardless of normality, since, by [**Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*](#lmm:adjoint-product-and-involution), $$(A^*A)^* = A^*(A^*)^* = A^*A$$ (Part 1 with the pair $$(A^*,A)$$, then Part 2 to simplify $$(A^*)^*=A$$). Since $$A$$ commutes with $$A^*$$ (normality), [**Lemma**](#lmm:hall-10.22) applies with the pair $$(A^*, A)$$ to give

$$
    R(A^*A) \le R(A^*)R(A).
$$

Also, since $$A^*A$$ is self-adjoint, [**Lemma** *(hall-8.1)*](../spectral-theorems/#lmm:hall-8.1) — the self-adjoint case of norm equals spectral radius, already established in the previous post — gives $$\|A^*A\| = R(A^*A)$$. Combining,

$$
    \|A\|^2 = \|A^*A\| = R(A^*A) \le R(A^*)R(A) \le \|A^*\|R(A) = \|A\|R(A),
$$

where the last equality is $$\|A^*\| = \|A\|$$, also from [**Proposition** *(hall-7.2)*](../spectral-theorems/#prpstn:hall-7.2), and $$R(A^*) \le \|A^*\|$$ is [**Corollary**](../spectral-theorems/#crllr:crllr-1) applied to $$A^*$$. If $$\|A\| \ne 0$$, dividing both sides by $$\|A\|$$ gives $$\|A\| \le R(A)$$, as desired; if $$\|A\| = 0$$ the inequality $$\|A\| \le R(A)$$ holds trivially, since $$R(A) \ge 0$$ always.$$\blacksquare$$

