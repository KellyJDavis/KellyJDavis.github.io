---
title:  "Spectral Theorem for Unbounded, Self-Adjoint Operators"
date:   2026-08-02 19:30:00 +0200
categories: functional-analysis
---

Here we will state and prove the [**Spectral Theorem for Unbounded, Self-Adjoint Operators**](#thrm:hall-10.4). This theorem extends the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators) to the small handful of genuinely unbounded self-adjoint operators that do arise in AQFT — the momentum operator on Minkowski space is a standard example — even though the large majority of operators of interest there, local observables in particular, are bounded. It is a prerequisite for handling these unbounded operators within the rest of the AQFT work that motivated this series.

This post is a direct continuation of [Spectral Theorem for Bounded, Self-Adjoint Operators](../spectral-theorems), and depends on it: a number of the definitions, propositions, lemmas, and theorems proven there are reused here without repetition. Where this happens, we link directly to the relevant element in that post rather than restating it under a new name in this one.

As before, we generally follow the clear, straightforward presentation of [Quantum Theory for Mathematicians](https://doi.org/10.1007/978-1-4614-7116-5).

A note on conventions, extending the one given in the previous post. Results that are standard and whose proofs lie outside the scope of the development are, as before, stated in full but not proven, marked by the absence of an accompanying **Proof**. Every other result stated here — including everything below on unbounded operators — is proven in full, and every use of a prior result is made explicit, including a check that its hypotheses actually hold in the situation at hand. We do not assume the reader has already encountered unbounded operators: the relevant definitions are built up from scratch below, so that this post is self-contained modulo the previous one.

One more note, for a formalizer rather than a general reader: several proofs below pick a sequence, or a preimage, satisfying some property known only to exist (e.g. the approximating sequence in the [sequential characterization of a closure](#prpstn:closure-linearity-and-sequential-description), or a preimage $$\xi$$ with $$\eta = P\xi$$ in the proof of [Lemma (The Range of a Projection is the Kernel of its Complement)](#lmm:range-of-projection-is-kernel)). These choices are all routine — nothing here needs a genuinely non-constructive selection principle beyond what dependent choice or `Classical.choice` already provides for sequences in a metric space — but they are choices, not constructions, and a formalizer should expect to reach for the corresponding Lean tactics rather than a constructive witness.

# Spectral Theorem: Unbounded Self-Adjoint Operators

We proceed in five stages. First, the basic theory of unbounded operators — adjoints, symmetry, self-adjointness, closedness, and the spectrum. Second, a theory of integrating an unbounded function against a projection-valued measure. Third, the continuous functional calculus for a *bounded normal* operator, built via a two-variable spectral mapping theorem. Fourth, an abstract construction turning any continuous functional calculus into a projection-valued measure — which, combined with the third stage, yields the spectral theorem for bounded normal operators. Finally, the Cayley transform, which lets us reduce the unbounded self-adjoint case to the bounded normal case and complete the proof.

## Unbounded Operators

### Adjoint and Closure of an Unbounded Operator

Recall from the [previous post](../spectral-theorems) that $$\mathbf{H}$$ denotes a separable, complex Hilbert space, and that $$\mathcal{B}(\mathbf{H})$$ denotes the set of bounded operators on $$\mathbf{H}$$. We now introduce operators that need not be bounded, and need not even be defined on all of $$\mathbf{H}$$; every definition and result below refers back to $$\mathbf{H}$$ in this fixed sense.

> **Definition** *(Unbounded Operator)*
<a name="def:hall-3.1"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> Let $$\mathbf{H}$$ be a separable, complex Hilbert space. An *unbounded operator* $$A$$ on $$\mathbf{H}$$ is a linear map $$A : \text{Dom}(A) \to \mathbf{H}$$, where $$\text{Dom}(A)$$, called the *domain* of $$A$$, is a dense subspace of $$\mathbf{H}$$. Here "unbounded" means "not necessarily bounded": we permit the case $$\text{Dom}(A) = \mathbf{H}$$ together with $$A \in \mathcal{B}(\mathbf{H})$$, the set of bounded operators on $$\mathbf{H}$$, but do not require it.

The identity operator $$\mathbf{1}$$ and indicator functions $$1_E$$ are as fixed in [Definition (The Identity Operator and Indicator Functions)](../spectral-theorems/#def:identity-and-indicator) of the previous post. One extension is needed here: when $$A$$ is an *unbounded* operator, $$A - \lambda\mathbf{1}$$ denotes the operator with domain $$\text{Dom}(A)$$ acting by $$\psi \mapsto A\psi - \lambda\psi$$ — its domain is that of $$A$$, since $$\lambda\mathbf{1}$$ is defined on all of $$\mathbf{H}$$.

Three standard facts about convergence of sequences and series are used at several points below. As with the other classical results imported here, we state them without proof.

> **Proposition** *(Convergence Facts for Sequences and Series)*
<a name="prpstn:convergence-facts"></a>
> 1. *(Monotone bounded sequences.)* A non-decreasing sequence $$\{ t_n \}_{n\in\mathbb{N}}$$ of real numbers that is bounded above converges, to $$\sup_n t_n$$.
> 2. *(Bolzano–Weierstrass.)* Every sequence in a closed, bounded subset $$K \subset \mathbb{C}$$ has a subsequence converging to a point of $$K$$. (Equivalently, such a $$K$$ is sequentially compact.)
> 3. *(Comparison test in a Banach space.)* Let $$\{a_n\}$$ be a sequence in a Banach space $$V$$ and $$\{t_n\}$$ non-negative reals with $$\left\| a_n \right\| \le t_n$$ for all $$n$$ and $$\sum_n t_n < \infty$$. Then $$\sum_n a_n$$ converges in $$V$$.
>
> We also use without further comment that limits in a metric space are unique, and that a convergent sequence is Cauchy.

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

The construction of the adjoint below rests on the Hilbert-space self-duality theorem, distinct from the [**Riesz Representation Theorem**](../spectral-theorems/#thrm:riesz-representation) of the previous post (which represents positive linear functionals on $$C^0(X;\mathbb{R})$$, for $$X$$ a compact metric space, by a measure). The result we actually need is Hall's Theorem A.52, which the previous post now states as a citable result: [**Theorem** *(Riesz Theorem)*](../spectral-theorems/#thrm:hall-a.52).

If $$A$$ happens to be a bounded operator on all of $$\mathbf{H}$$, then for any $$\phi \in \mathbf{H}$$ the linear functional $$\psi \mapsto \left< \phi, A\psi \right>$$ is automatically bounded, and the [**Riesz Theorem**](../spectral-theorems/#thrm:hall-a.52) produces a unique $$\chi \in \mathbf{H}$$ with $$\left< \phi, A\psi \right> = \left< \chi, \psi \right>$$ for all $$\psi$$; we then set $$A^*\phi \equiv \chi$$. If $$A$$ is genuinely unbounded, the functional $$\psi \mapsto \left< \phi, A\psi \right>$$ need not be bounded on $$\text{Dom}(A)$$ for every $$\phi$$ — but it may be bounded for *some* $$\phi$$, and it is exactly this set of $$\phi$$'s on which the adjoint gets defined.

> **Definition** *(Adjoint of an Unbounded Operator)*
<a name="def:hall-9.1"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{../spectral-theorems/#thrm:hall-a.52} -->
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

The definition just given is not self-evidently well posed: it declares $$A^*\phi$$ to be "the unique vector such that ...", which presupposes that such a vector exists and that there is only one. Neither is automatic once $$A$$ is merely densely defined, so we record the fact as a proposition — a formalization needs exactly this existence-and-uniqueness statement in order to define $$A^*$$ at all.

> **Proposition** *(The Adjoint is Well Defined)*
<a name="prpstn:adjoint-well-defined"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{../spectral-theorems/#thrm:hall-a.52} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
> Let $$A$$ be an unbounded operator on $$\mathbf{H}$$ and let $$\phi \in \text{Dom}(A^*)$$. Then there is exactly one $$\chi \in \mathbf{H}$$ with
>
> $$
>     \left< \phi, A\psi \right> = \left< \chi, \psi \right> \quad \text{for all } \psi \in \text{Dom}(A).
> $$

**Proof**
Fix $$\phi \in \text{Dom}(A^*)$$, and consider the map $$T : \text{Dom}(A) \to \mathbb{C}$$ given by $$T\psi \equiv \left< \phi, A\psi \right>$$. Since $$A$$ is linear (by the [definition of an unbounded operator](#def:hall-3.1)) and the inner product on $$\mathbf{H}$$ is linear in its second argument, $$T$$ is a linear map; by the defining property of $$\text{Dom}(A^*)$$ used above, $$T$$ is bounded on $$\text{Dom}(A)$$.

To apply the [**Bounded Linear Transformation Theorem**](../spectral-theorems/#thrm:bounded-linear-transformation-theorem) to $$T$$, we check its three hypotheses hold: it asks for a normed space $$V_1$$, a Banach space $$V_2$$, a dense subspace $$W \subset V_1$$, and a bounded linear map $$T : W \to V_2$$. Here $$\mathbf{H}$$, being a Hilbert space, is in particular a normed vector space with norm $$\left\| \cdot \right\|$$ induced by its inner product, so we may take $$V_1 = \mathbf{H}$$. The target space $$\mathbb{C}$$, with the usual absolute value as norm, is a Banach space, since every Cauchy sequence of complex numbers converges. By the [definition of an unbounded operator](#def:hall-3.1), $$\text{Dom}(A)$$ is a dense subspace of $$\mathbf{H}$$, so we may take $$W = \text{Dom}(A)$$. We have just checked $$T$$ is linear and bounded on $$W$$. All hypotheses being met, there is a unique bounded linear map $$\tilde{T} : \mathbf{H} \to \mathbb{C}$$ with $$\tilde{T} = T$$ on $$\text{Dom}(A)$$.

Now $$\tilde{T}$$ is a bounded linear functional on the Hilbert space $$\mathbf{H}$$, so the [**Riesz Theorem**](../spectral-theorems/#thrm:hall-a.52) applies — its only hypothesis is exactly that $$\tilde{T}$$ be a bounded linear functional on a Hilbert space — and produces a unique $$\chi \in \mathbf{H}$$ with $$\tilde{T}\psi = \left< \chi, \psi \right>$$ for all $$\psi \in \mathbf{H}$$. In particular, restricting to $$\psi \in \text{Dom}(A)$$, where $$\tilde{T}$$ agrees with $$T$$,

$$
    \left< \phi, A\psi \right> = T\psi = \tilde{T}\psi = \left< \chi, \psi \right> \quad \text{for all } \psi \in \text{Dom}(A).
$$

So $$\chi$$ satisfies the defining equation of $$A^*\phi$$ in [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1). For uniqueness: if $$\chi'$$ also satisfied $$\left< \phi, A\psi \right> = \left< \chi', \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$, then $$\chi$$ and $$\chi'$$ would agree in inner product against every element of the dense subset $$\text{Dom}(A)$$, so $$\chi = \chi'$$ by [Lemma (Equality Testing on a Dense Subspace, First Slot)](#lmm:hall-dense-testing). So $$\chi$$ is unique, and setting $$A^*\phi \equiv \chi$$ in [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1) is unambiguous.$$\blacksquare$$

Before proceeding, we check that $$A^*$$, as just constructed, is again a linear operator on its domain — a fact used implicitly throughout the rest of this post.

> **Proposition** *(Linearity of the Adjoint)*
<a name="prpstn:hall-linearity-of-the-adjoint"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:hall-dense-testing} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
<!--  \uses{prpstn:adjoint-well-defined} -->
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
<!--  \uses{prpstn:adjoint-well-defined} -->
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
<!--  \uses{def:hall-9.3} -->
<!--  \uses{prpstn:hall-9.4} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *self-adjoint* if $$\text{Dom}(A^*) = \text{Dom}(A)$$ and $$A^*\phi = A\phi$$ for all $$\phi \in \text{Dom}(A)$$. Equivalently, $$A$$ is self-adjoint if $$A^* = A$$, where equality of unbounded operators is understood to include equality of domains.

Indeed, if $$A$$ is self-adjoint then $$\text{Dom}(A^*) = \text{Dom}(A)$$ and $$A^* = A$$ on this common domain, which is exactly [Definition (Extension of an Operator)](#def:hall-9.3) applied with $$B = A$$: $$A^*$$ is (trivially) an extension of $$A$$, so by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4), $$A$$ is symmetric. Conversely, a symmetric operator $$A$$ is self-adjoint precisely when $$\text{Dom}(A^*)$$ is no bigger than $$\text{Dom}(A)$$, since symmetry already gives the reverse containment via [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4). This is usually the difficulty in showing a symmetric operator is self-adjoint: showing that the adjoint's domain does not overshoot.

The next two definitions let us make sense of the *closure* of an unbounded operator, which we will need almost immediately. They refer to the topology on $$\mathbf{H} \times \mathbf{H}$$, so we fix that first — as a definition and two supporting facts rather than as a remark, since every closedness argument below rests on them.

> **Definition** *(The Product Hilbert Space $$\mathbf{H} \times \mathbf{H}$$)*
<a name="def:product-hilbert-space"></a>
> $$\mathbf{H} \times \mathbf{H}$$ denotes the set of ordered pairs $$(\phi,\psi)$$ with $$\phi,\psi \in \mathbf{H}$$, made a complex vector space by componentwise operations and equipped with the inner product
>
> $$
>     \left< (\phi_1,\psi_1), (\phi_2,\psi_2) \right> \equiv \left< \phi_1,\phi_2 \right> + \left< \psi_1,\psi_2 \right>,
> $$
>
> whose associated norm is $$\left\| (\phi,\psi) \right\| = \big( \left\| \phi \right\|^2 + \left\| \psi \right\|^2 \big)^{1/2}$$. The inner-product axioms are inherited componentwise from those on $$\mathbf{H}$$, and completeness likewise: a sequence is Cauchy in $$\mathbf{H}\times\mathbf{H}$$ exactly when both component sequences are Cauchy in $$\mathbf{H}$$, by the same two inequalities used in [**Lemma** *(Convergence in $$\mathbf{H} \times \mathbf{H}$$ is Componentwise)*](#lmm:componentwise-convergence) below with $$(\phi_m,\psi_m)$$ in place of $$(\phi,\psi)$$. So $$\mathbf{H}\times\mathbf{H}$$ is again a separable, complex Hilbert space, and the topology on it is the one induced by this norm. (It is the two-summand case of [Definition (Hilbert Space Direct Sum)](#def:hall-a.45) further below, but is used well before that definition, so we give it directly here.)

> **Theorem** *(Sequential Characterization of Closed Sets and Closures)*
<a name="thrm:sequential-closedness"></a>
> Let $$M$$ be a metric space and $$S \subset M$$. Then $$S$$ is closed if and only if it is sequentially closed, i.e. contains the limit of every convergent sequence of its own points; and a point of $$M$$ lies in the closure $$\overline{S}$$ if and only if it is the limit of some sequence of points of $$S$$.

> **Lemma** *(Convergence in $$\mathbf{H} \times \mathbf{H}$$ is Componentwise)*
<a name="lmm:componentwise-convergence"></a>
<!--  \uses{def:product-hilbert-space} -->
> Let $$\{(\phi_n,\psi_n)\}_{n\in\mathbb{N}}$$ be a sequence in $$\mathbf{H}\times\mathbf{H}$$ and $$(\phi,\psi) \in \mathbf{H}\times\mathbf{H}$$. Then $$(\phi_n,\psi_n) \to (\phi,\psi)$$ in $$\mathbf{H}\times\mathbf{H}$$ if and only if $$\phi_n \to \phi$$ and $$\psi_n \to \psi$$ in $$\mathbf{H}$$.

**Proof**
Suppose $$(\phi_n,\psi_n) \to (\phi,\psi)$$. Then, by [Definition (The Product Hilbert Space $$\mathbf{H} \times \mathbf{H}$$)](#def:product-hilbert-space),

$$
    \left\| \phi_n - \phi \right\|^2 \le \left\| \phi_n-\phi \right\|^2 + \left\| \psi_n-\psi \right\|^2 = \left\| (\phi_n,\psi_n)-(\phi,\psi) \right\|^2 \longrightarrow 0,
$$

so $$\phi_n \to \phi$$; the same computation with the roles of the components exchanged gives $$\psi_n \to \psi$$.

Conversely, if $$\phi_n \to \phi$$ and $$\psi_n \to \psi$$ then

$$
    \left\| (\phi_n,\psi_n)-(\phi,\psi) \right\|^2 = \left\| \phi_n-\phi \right\|^2 + \left\| \psi_n-\psi \right\|^2 \longrightarrow 0,
$$

a sum of two sequences of non-negative reals each tending to $$0$$.$$\blacksquare$$

> **Definition** *(Closed and Closable Operators)*
<a name="def:hall-9.6"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{def:product-hilbert-space} -->
<!--  \uses{lmm:componentwise-convergence} -->
<!--  \uses{thrm:sequential-closedness} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closed* if the graph of $$A$$ is a closed subset of $$\mathbf{H} \times \mathbf{H}$$. Equivalently — by [**Theorem** *(Sequential Characterization of Closed Sets and Closures)*](#thrm:sequential-closedness) and [**Lemma** *(Convergence in $$\mathbf{H} \times \mathbf{H}$$ is Componentwise)*](#lmm:componentwise-convergence) — $$A$$ is closed if and only if: whenever $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A)$$ and there exist $$\psi, \varphi \in \mathbf{H}$$ with $$\psi_n \to \psi$$ and $$A\psi_n \to \varphi$$, it follows that $$\psi \in \text{Dom}(A)$$ and $$A\psi = \varphi$$.
>
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *closable* if the closure, in $$\mathbf{H} \times \mathbf{H}$$, of the graph of $$A$$ is again the graph of some operator. If $$A$$ is closable, the *closure* $$A^{\text{cl}}$$ of $$A$$ is the operator whose graph is the closure of the graph of $$A$$.

Two elementary facts about this closure — that it is automatically linear, and admits the same sequential description as $$A$$ itself — are needed repeatedly below, so we record and prove them immediately.

> **Proposition** *(Linearity and the Sequential Description of the Closure)*
<a name="prpstn:closure-linearity-and-sequential-description"></a>
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-3.1} -->
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
<!--  \uses{def:hall-9.1} -->
> An unbounded operator $$A$$ on $$\mathbf{H}$$ is *essentially self-adjoint* if $$A$$ is symmetric, $$A$$ is closable, and $$A^{\text{cl}}$$ is self-adjoint.

### Elementary Properties of Adjoints and Closed Operators

We record here some basic properties of adjoints and closures that we will draw on repeatedly below. Throughout, if we say two operators *coincide*, we mean they have the same domain and are equal on that common domain.

A remark on typing, before the first proposition of this section. [Definition (Unbounded Operator)](#def:hall-3.1) requires a dense domain, so [Definition (Closed and Closable Operators)](#def:hall-9.6), stated for unbounded operators in that sense, literally applies only to densely-defined operators. The adjoint $$A^*$$ of an unbounded operator $$A$$, however, need not itself have dense domain — nothing in [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1) guarantees this — so asking whether $$A^*$$ is *closed* is, strictly, asking a question the definition does not cover. Being closed is a purely topological property of the graph and makes sense for any linear map defined on any subspace, dense or not; rather than leave the mismatch implicit, we give the broader notion its own definition, so that there is a statement to cite.

> **Definition** *(Closed Linear Map on a Subspace)*
<a name="def:closed-linear-map-on-a-subspace"></a>
<!--  \uses{def:hall-9.6} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{prpstn:hall-9.4} -->
> Let $$D \subset \mathbf{H}$$ be a subspace, not necessarily dense, and $$T : D \to \mathbf{H}$$ a linear map. The *graph* of $$T$$ is $$\{ (\psi, T\psi) \mid \psi \in D \} \subset \mathbf{H} \times \mathbf{H}$$, and $$T$$ is *closed* if its graph is a closed subset of $$\mathbf{H} \times \mathbf{H}$$ (in the product topology fixed above). Equivalently, by sequential closedness and componentwise convergence exactly as in [Definition (Closed and Closable Operators)](#def:hall-9.6): $$T$$ is closed if and only if, whenever $$\{\psi_n\}$$ is a sequence in $$D$$ with $$\psi_n \to \psi$$ and $$T\psi_n \to \varphi$$ for some $$\psi,\varphi \in \mathbf{H}$$, it follows that $$\psi \in D$$ and $$T\psi = \varphi$$.
>
> When $$D$$ is dense — so that $$T$$ is an unbounded operator in the sense of [Definition (Unbounded Operator)](#def:hall-3.1) — this agrees with [Definition (Closed and Closable Operators)](#def:hall-9.6), the two conditions being verbatim the same.

It is in this sense that we ask below whether $$A^*$$ is closed. In every case where this document goes on to treat $$A^*$$ as a fully-fledged unbounded operator in its own right (in particular, taking a further adjoint $$(A^*)^*$$, which does require $$\text{Dom}(A^*)$$ to be dense), the operator $$A$$ in question is symmetric — so, by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4) below, $$A^*$$ is an extension of $$A$$, and therefore automatically has dense domain (containing the already-dense $$\text{Dom}(A)$$). So the gap never bites in this post.

Our first observation is that the adjoint's graph is always closed, regardless of any hypothesis on $$A$$; from this, closability of symmetric operators follows immediately.

> **Proposition** *(Closedness of the Adjoint's Graph; Closability of Symmetric Operators)*
<a name="prpstn:hall-9.8"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:characterizing-adjoint-domain-membership} -->
<!--  \uses{def:closed-linear-map-on-a-subspace} -->
<!--  \uses{def:hall-9.2} -->
<!--  \uses{def:hall-9.6} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{prpstn:hall-linearity-of-the-adjoint} -->
> 1. If $$A$$ is an unbounded operator on $$\mathbf{H}$$, then the graph of $$A^*$$ (which may or may not be densely defined) is closed in $$\mathbf{H} \times \mathbf{H}$$.
> 2. A symmetric operator is always closable.

**Proof**
**Part 1:** Suppose $$\{ \psi_n \}_{n \in \mathbb{N}}$$ is a sequence in $$\text{Dom}(A^*)$$ converging to some $$\psi \in \mathbf{H}$$, and suppose also that $$\{ A^*\psi_n \}_{n \in \mathbb{N}}$$ converges to some $$\varphi \in \mathbf{H}$$. By the [definition of the adjoint](#def:hall-9.1), $$\left< \psi_n, A\chi \right> = \left< A^*\psi_n, \chi \right>$$ for every $$\chi \in \text{Dom}(A)$$ and every $$n$$. Fix $$\chi \in \text{Dom}(A)$$. Applying [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — valid since $$\psi_n \to \psi$$ and $$A^*\psi_n \to \varphi$$ in $$\mathbf{H}$$ — to both sides of this equation,

$$
    \left< \psi, A\chi \right> = \lim_{n \to \infty} \left< \psi_n, A\chi \right> = \lim_{n \to \infty} \left< A^*\psi_n, \chi \right> = \left< \varphi, \chi \right>.
$$

As $$\chi \in \text{Dom}(A)$$ was arbitrary, this exhibits $$\varphi$$ as a vector with $$\left< \psi, A\chi \right> = \left< \varphi, \chi \right>$$ for all $$\chi \in \text{Dom}(A)$$, so [Lemma (Characterizing Membership in the Adjoint's Domain)](#lmm:characterizing-adjoint-domain-membership) gives $$\psi \in \text{Dom}(A^*)$$ and $$A^*\psi = \varphi$$. By the sequential characterization in [Definition (Closed Linear Map on a Subspace)](#def:closed-linear-map-on-a-subspace) — applicable to $$A^*$$ regardless of whether $$\text{Dom}(A^*)$$ is dense — this establishes that the graph of $$A^*$$ is closed, the desired **Part 1** result.

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

> **Definition** *(Kernel of an Unbounded Operator)*
<a name="def:kernel-of-an-unbounded-operator"></a>
<!--  \uses{def:hall-3.1} -->
> If $$A$$ is an unbounded operator on $$\mathbf{H}$$, its *kernel* is
>
> $$
>     \text{Ker}(A) \equiv \{ \psi \in \text{Dom}(A) \mid A\psi = 0 \} \subset \text{Dom}(A).
> $$
>
> As with the range, the domain restriction is part of the definition: a vector outside $$\text{Dom}(A)$$ is not in $$\text{Ker}(A)$$, regardless of any other property it may have. $$\text{Ker}(A)$$ is a subspace of $$\mathbf{H}$$: it contains $$0$$, and for $$\psi_1,\psi_2 \in \text{Ker}(A)$$ and $$\alpha,\beta \in \mathbb{C}$$ we have $$\alpha\psi_1+\beta\psi_2 \in \text{Dom}(A)$$ (a subspace) with $$A(\alpha\psi_1+\beta\psi_2) = \alpha A\psi_1 + \beta A\psi_2 = 0$$. Saying $$A$$ is *injective* is equivalent to $$\text{Ker}(A) = \{0\}$$, by linearity.

> **Definition** *(Range of an Unbounded Operator)*
<a name="def:range-of-an-unbounded-operator"></a>
<!--  \uses{def:hall-3.1} -->
<!--  \uses{../spectral-theorems/#def:orthogonal-complement} -->
> If $$A$$ is an unbounded operator on $$\mathbf{H}$$, its *range* is $$\text{Range}(A) \equiv \{ A\psi \mid \psi \in \text{Dom}(A) \} \subset \mathbf{H}$$. Since $$\text{Dom}(A)$$ is a subspace of $$\mathbf{H}$$ and $$A$$ is linear, $$\text{Range}(A)$$ is again a subspace of $$\mathbf{H}$$: it contains $$0 = A0$$, and for $$A\psi_1, A\psi_2 \in \text{Range}(A)$$ and $$\alpha,\beta \in \mathbb{C}$$, linearity of $$A$$ gives $$\alpha A\psi_1 + \beta A\psi_2 = A(\alpha\psi_1+\beta\psi_2) \in \text{Range}(A)$$, as $$\alpha\psi_1+\beta\psi_2 \in \text{Dom}(A)$$. Unwinding [Definition (Orthogonal Complement)](../spectral-theorems/#def:orthogonal-complement) for $$V = \text{Range}(A)$$: $$\left( \text{Range}(A) \right)^\perp = \{ \psi \in \mathbf{H} \mid \left< \psi, A\phi \right> = 0 \text{ for all } \phi \in \text{Dom}(A) \}$$ — the quantifier ranges over $$\text{Dom}(A)$$, not all of $$\mathbf{H}$$.

We will need two standard facts about closed subspaces of a Hilbert space at several points below, starting almost immediately; we import them together, as Hall does when he first needs them.

> **Proposition** *(Orthogonal Decomposition and the Double Complement)*
<a name="prpstn:hall-a.49"></a>
<!--  \uses{../spectral-theorems/#def:orthogonal-complement} -->
> 1. If $$V$$ is a closed subspace of $$\mathbf{H}$$, every $$\psi \in \mathbf{H}$$ decomposes uniquely as $$\psi = \psi_1 + \psi_2$$ with $$\psi_1 \in V$$ and $$\psi_2 \in V^\perp$$.
> 2. If $$V$$ is any subspace of $$\mathbf{H}$$, then $$(V^\perp)^\perp = \overline{V}$$, the closure of $$V$$. In particular, if $$V$$ is closed, $$(V^\perp)^\perp = V$$.

We record one immediate consequence of Part 2, in the form we will repeatedly need it: a subspace has trivial orthogonal complement exactly when it is dense.

> **Corollary** *(Trivial Complement Characterizes Density)*
<a name="crllr:trivial-complement-characterizes-density"></a>
<!--  \uses{prpstn:hall-a.49} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
> A subspace $$V \subset \mathbf{H}$$ is dense in $$\mathbf{H}$$ if and only if $$V^\perp = \{0\}$$.

**Proof**
If $$V^\perp = \{0\}$$, then, by [Part 2 of **Proposition** *(hall-a.49)*](#prpstn:hall-a.49), $$\overline{V} = (V^\perp)^\perp = \{0\}^\perp = \mathbf{H}$$ — the last equality since $$\left< \psi, 0 \right> = 0$$ for every $$\psi \in \mathbf{H}$$, so every $$\psi$$ lies in $$\{0\}^\perp$$. Thus $$V$$ is dense.

Conversely, suppose $$V$$ is dense, i.e. $$\overline{V} = \mathbf{H}$$. Let $$\psi \in V^\perp$$, so $$\left< \psi, v \right> = 0$$ for all $$v \in V$$. Since $$\psi \in \mathbf{H} = \overline{V}$$, there is a sequence $$\{v_n\}$$ in $$V$$ with $$v_n \to \psi$$; by [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), $$\left< \psi, \psi \right> = \lim_n \left< \psi, v_n \right> = 0$$, so $$\psi = 0$$. Hence $$V^\perp = \{0\}$$.$$\blacksquare$$

> **Proposition** *(Orthogonal Complement of the Range)*
<a name="prpstn:hall-9.12"></a>
<!--  \uses{def:hall-9.1} -->
<!--  \uses{../spectral-theorems/#def:orthogonal-complement} -->
<!--  \uses{lmm:characterizing-adjoint-domain-membership} -->
<!--  \uses{def:range-of-an-unbounded-operator} -->
<!--  \uses{def:kernel-of-an-unbounded-operator} -->
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
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{def:hall-3.1} -->
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

where the third equality used the [definition of the adjoint](#def:hall-9.1) applied to $$A$$ and, separately, applied to the everywhere-defined bounded operator $$B$$, and the last equality used linearity of the inner product in its second argument. So $$\left< (A+B)^*\phi, \psi \right> = \left< A^*\phi + B^*\phi, \psi \right>$$ for all $$\psi \in \text{Dom}(A)$$, a dense subset of $$\mathbf{H}$$ by the [definition of an unbounded operator](#def:hall-3.1); by [Lemma (Equality Testing on a Dense Subspace, First Slot)](#lmm:hall-dense-testing), $$(A+B)^*\phi = A^*\phi + B^*\phi$$.

Finally, suppose $$A$$ is self-adjoint and $$B$$ is bounded and self-adjoint on all of $$\mathbf{H}$$. Then $$\text{Dom}\big( (A+B)^* \big) = \text{Dom}(A^*) = \text{Dom}(A) = \text{Dom}(A+B)$$, using self-adjointness of $$A$$ for the middle equality; and for $$\psi$$ in this common domain, $$(A+B)^*\psi = A^*\psi + B^*\psi = A\psi + B\psi = (A+B)\psi$$, using self-adjointness of $$A$$ and of $$B$$. So $$A+B$$ is self-adjoint.$$\blacksquare$$

[Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) tells us how to add a bounded operator $$B$$ to $$A$$ and take the adjoint, but leaves $$B^*$$ itself as an unexplained ingredient whenever we specialize to $$B = \lambda\mathbf{1}$$ for a scalar $$\lambda \in \mathbb{C}$$ — a combination that will recur constantly (e.g. $$A - \lambda\mathbf{1}$$). We record the needed computation once.

> **Lemma** *(Adjoint of a Scalar Multiple of the Identity)*
<a name="lmm:adjoint-of-scalar-multiple-of-identity"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{def:hall-9.1} -->
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
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
> Suppose $$A$$ is an unbounded operator on $$\mathbf{H}$$. A number $$\lambda \in \mathbb{C}$$ belongs to the *resolvent set* of $$A$$ if there exists a bounded operator $$B \in \mathcal{B}(\mathbf{H})$$ with the following properties:
>
> 1. For all $$\psi \in \mathbf{H}$$, $$B\psi \in \text{Dom}(A)$$ and $$(A - \lambda \mathbf{1})B\psi = \psi$$; and
> 2. For all $$\psi \in \text{Dom}(A)$$, $$B(A - \lambda \mathbf{1})\psi = \psi$$.
>
> If no such bounded operator $$B$$ exists, then $$\lambda$$ belongs to the *spectrum* $$\sigma(A)$$ of $$A$$.

The operator $$B$$ in this definition is unique when it exists, which is what licenses the notation $$(A - \lambda\mathbf{1})^{-1}$$ used throughout below.

> **Lemma** *(Uniqueness of the Resolvent)*
<a name="lmm:uniqueness-of-resolvent"></a>
<!--  \uses{def:hall-9.16} -->
> Let $$A$$ be an unbounded operator on $$\mathbf{H}$$ and $$\lambda$$ a point of its resolvent set. Then there is exactly one $$B \in \mathcal{B}(\mathbf{H})$$ satisfying properties 1 and 2 of [Definition (Resolvent Set and Spectrum of an Unbounded Operator)](#def:hall-9.16). We denote it $$(A - \lambda\mathbf{1})^{-1}$$.

**Proof**
Suppose $$B_1, B_2 \in \mathcal{B}(\mathbf{H})$$ both satisfy properties 1 and 2, and let $$\psi \in \mathbf{H}$$. By property 1 for $$B_1$$, $$B_1\psi \in \text{Dom}(A)$$ and $$(A-\lambda\mathbf{1})B_1\psi = \psi$$. Applying $$B_2$$ to both sides of this last equation and using property 2 for $$B_2$$ with the vector $$B_1\psi \in \text{Dom}(A)$$,

$$
    B_1\psi = B_2(A - \lambda\mathbf{1})B_1\psi = B_2\psi.
$$

As $$\psi \in \mathbf{H}$$ was arbitrary, $$B_1 = B_2$$.$$\blacksquare$$

Two notions of resolvent set are now in play: the one just defined, for an unbounded operator, and the one from the previous post for a bounded operator, where $$\lambda$$ is in the resolvent set exactly when $$A - \lambda\mathbf{1}$$ has a bounded inverse. A bounded operator is in particular an unbounded operator with $$\text{Dom}(A) = \mathbf{H}$$, so both definitions apply to it, and we must know they agree before using results stated for one notion in a context governed by the other.

> **Lemma** *(The Two Notions of Spectrum Agree for Bounded Operators)*
<a name="lmm:spectrum-notions-agree"></a>
<!--  \uses{def:hall-9.16} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$, regarded also as an unbounded operator with $$\text{Dom}(A) = \mathbf{H}$$. Then $$\lambda \in \mathbb{C}$$ lies in the resolvent set of $$A$$ in the sense of [Definition (Resolvent Set and Spectrum of an Unbounded Operator)](#def:hall-9.16) if and only if it lies in the resolvent set in the sense of the [previous post's definition](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum). Consequently the two resulting spectra $$\sigma(A)$$ coincide.

**Proof**
Suppose first that $$\lambda$$ is in the resolvent set in the previous post's sense, so $$A - \lambda\mathbf{1}$$ has a bounded inverse $$B \in \mathcal{B}(\mathbf{H})$$, meaning $$(A-\lambda\mathbf{1})B = B(A-\lambda\mathbf{1}) = \mathbf{1}$$. Then for every $$\psi \in \mathbf{H}$$ we have $$B\psi \in \mathbf{H} = \text{Dom}(A)$$ and $$(A-\lambda\mathbf{1})B\psi = \psi$$, which is property 1 of [Definition (Resolvent Set and Spectrum of an Unbounded Operator)](#def:hall-9.16); and for every $$\psi \in \text{Dom}(A) = \mathbf{H}$$, $$B(A-\lambda\mathbf{1})\psi = \psi$$, which is property 2.

Conversely, suppose $$B \in \mathcal{B}(\mathbf{H})$$ satisfies properties 1 and 2 of that definition. Since $$\text{Dom}(A) = \mathbf{H}$$, property 1 says $$(A-\lambda\mathbf{1})B\psi = \psi$$ for all $$\psi \in \mathbf{H}$$ and property 2 says $$B(A-\lambda\mathbf{1})\psi = \psi$$ for all $$\psi \in \mathbf{H}$$; together, $$B$$ is a two-sided inverse of $$A - \lambda\mathbf{1}$$ lying in $$\mathcal{B}(\mathbf{H})$$, i.e. $$A - \lambda\mathbf{1}$$ has a bounded inverse.

So the two resolvent sets are equal, and the spectra — their complements in $$\mathbb{C}$$ — are equal too.$$\blacksquare$$

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
        &= \left< (A-a\mathbf{1})\psi, (A-a\mathbf{1})\psi \right> - ib\left< (A-a\mathbf{1})\psi, \psi \right> + ib \left< \psi, (A-a\mathbf{1})\psi \right> + b^2 \left< \psi, \psi \right>.
\end{align}
$$

Here the cross terms arise as follows: expanding the first argument by conjugate-linearity contributes $$\overline{(-ib)} = ib$$ to the $$\psi$$-term, and expanding the second by linearity contributes $$-ib$$; the final term is $$\overline{(-ib)}(-ib)\left< \psi,\psi \right> = (ib)(-ib)\left< \psi,\psi\right> = b^2\left<\psi,\psi\right>$$. By the symmetry identity just established, $$\left< (A-a\mathbf{1})\psi, \psi \right> = \left< \psi, (A-a\mathbf{1})\psi \right>$$, so the middle two terms cancel: $$-ib\left< (A-a\mathbf{1})\psi, \psi \right> + ib \left< \psi, (A-a\mathbf{1})\psi \right> = -ib\left< \psi, (A-a\mathbf{1})\psi \right> + ib \left< \psi, (A-a\mathbf{1})\psi \right> = 0$$. So

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
<!--  \uses{def:kernel-of-an-unbounded-operator} -->
<!--  \uses{lmm:uniqueness-of-resolvent} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
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

By [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) with $$B = -\lambda \mathbf{1}$$ — a bounded operator on all of $$\mathbf{H}$$ — combined with [Lemma (Adjoint of a Scalar Multiple of the Identity)](#lmm:adjoint-of-scalar-multiple-of-identity) giving $$(-\lambda\mathbf{1})^* = -\overline{\lambda}\mathbf{1}$$, we get $$(A - \lambda\mathbf{1})^* = A^* + (-\lambda\mathbf{1})^* = A^* - \overline{\lambda}\mathbf{1} = A - \overline{\lambda}\mathbf{1}$$, using $$A^* = A$$. Write $$\overline{\lambda} = a + i(-b)$$, so that [**Lemma (The $$b^2$$ Inequality for Symmetric Operators)**](#lmm:b-squared-inequality-symmetric), applied to the symmetric $$A$$ with the pair $$(a, -b)$$ in place of $$(a,b)$$, gives $$(-b)^2\left< \psi,\psi \right> \le \left< (A - \overline{\lambda}\mathbf{1})\psi, (A-\overline{\lambda}\mathbf{1})\psi \right>$$ for all $$\psi \in \text{Dom}(A)$$. Since $$(-b)^2 = b^2 \ne 0$$, the injectivity argument of the previous paragraph applies verbatim with $$\overline{\lambda}$$ in place of $$\lambda$$: $$\text{Ker}(A - \overline{\lambda}\mathbf{1}) = \{0\}$$. Hence

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
<!--  \uses{def:kernel-of-an-unbounded-operator} -->
> If $$A$$ is a symmetric operator on $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint if and only if $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense subspaces of $$\mathbf{H}$$.

**Proof**
We first prove the forward direction, i.e. that if $$A$$ is essentially self-adjoint, then $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ are dense in $$\mathbf{H}$$. Since $$A$$ is essentially self-adjoint, $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$A^* = (A^{\text{cl}})^* = A^{\text{cl}}$$, the last equality because $$A^{\text{cl}}$$ is self-adjoint. By [Proposition (Orthogonal Complement of the Range)](#prpstn:hall-9.12) and [Proposition (Adjoint of a Sum with a Bounded Operator)](#prpstn:hall-9.13) (applied to $$A - i\mathbf{1}$$, i.e. with $$B = -i\mathbf{1}$$, so that $$B^* = \overline{(-i)}\mathbf{1} = i\mathbf{1}$$ by [Lemma (Adjoint of a Scalar Multiple of the Identity)](#lmm:adjoint-of-scalar-multiple-of-identity)),

$$
    \left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \text{Ker}\left( (A - i\mathbf{1})^* \right) = \text{Ker}(A^* + i\mathbf{1}) = \text{Ker}(A^{\text{cl}} + i\mathbf{1}).
$$

Since $$A^{\text{cl}}$$ is self-adjoint, [Theorem (Spectrum of a Self-Adjoint Operator is Real)](#thrm:hall-9.17) shows $$\sigma(A^{\text{cl}}) \subset \mathbb{R}$$, and since $$-i \notin \mathbb{R}$$, $$-i$$ is not in $$\sigma(A^{\text{cl}})$$, i.e. $$-i$$ is in the resolvent set of $$A^{\text{cl}}$$. By the [definition of the resolvent set](#def:hall-9.16), this gives a bounded two-sided inverse to $$A^{\text{cl}} + i\mathbf{1}$$, and an operator with a two-sided inverse is in particular injective, so $$\text{Ker}(A^{\text{cl}} + i\mathbf{1}) = \{0\}$$. Hence $$\left( \text{Range}(A - i\mathbf{1}) \right)^\perp = \{0\}$$, so, by [Corollary (Trivial Complement Characterizes Density)](#crllr:trivial-complement-characterizes-density), $$\text{Range}(A - i\mathbf{1})$$ is dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ throughout shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$.

We now prove the reverse direction, i.e. that if $$A$$ is symmetric with $$\text{Range}(A - i\mathbf{1})$$ and $$\text{Range}(A + i\mathbf{1})$$ both dense in $$\mathbf{H}$$, then $$A$$ is essentially self-adjoint. By [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), $$A$$ is closable, so $$A^{\text{cl}}$$ exists. By [Proposition (The Adjoint of a Closure)](#prpstn:hall-9.10), $$(A^{\text{cl}})^* = A^*$$; and $$A^*$$ is a closed extension of the symmetric operator $$A$$ (closed by [Proposition (Closedness of the Adjoint's Graph)](#prpstn:hall-9.8), an extension of $$A$$ by [Proposition (Symmetric Operators and the Adjoint)](#prpstn:hall-9.4)), hence also an extension of the closure $$A^{\text{cl}}$$, by Part 3 of [Proposition (Linearity and the Sequential Description of the Closure)](#prpstn:closure-linearity-and-sequential-description). We check $$A^{\text{cl}}$$ is itself symmetric: for $$\xi, \eta \in \text{Dom}(A^{\text{cl}})$$, take sequences $$\{\xi_n\}, \{\eta_n\}$$ in $$\text{Dom}(A)$$ with $$\xi_n \to \xi$$, $$A\xi_n \to A^{\text{cl}}\xi$$ and $$\eta_n \to \eta$$, $$A\eta_n \to A^{\text{cl}}\eta$$, as furnished by Part 2 of the same proposition; symmetry of $$A$$ gives $$\left< \xi_n, A\eta_n \right> = \left< A\xi_n, \eta_n \right>$$ for every $$n$$, and [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product) — applicable since all four sequences $$\xi_n, A\xi_n, \eta_n, A\eta_n$$ converge — passes this to the limit, giving $$\left< \xi, A^{\text{cl}}\eta \right> = \left< A^{\text{cl}}\xi, \eta \right>$$, which is the [definition of symmetric](#def:hall-9.2) for $$A^{\text{cl}}$$.

Applying [**Lemma (The $$b^2$$ Inequality for Symmetric Operators)**](#lmm:b-squared-inequality-symmetric) — applicable since $$A^{\text{cl}}$$ is symmetric, shown above — with $$\lambda = i$$ (i.e. $$a=0$$, $$b=1$$) gives

$$
    \left\| \psi \right\|^2 \le \left\| (A^{\text{cl}} - i\mathbf{1})\psi \right\|^2 \tag{$\ast\ast$}
$$

for all $$\psi \in \text{Dom}(A^{\text{cl}})$$, so $$A^{\text{cl}} - i\mathbf{1}$$ is injective: if $$(A^{\text{cl}} - i\mathbf{1})\psi = 0$$ then $$(\ast\ast)$$ gives $$\left\| \psi \right\|^2 \le 0$$, forcing $$\psi = 0$$. Since $$A^{\text{cl}}$$ extends $$A$$, $$\text{Range}(A - i\mathbf{1}) \subset \text{Range}(A^{\text{cl}} - i\mathbf{1})$$; as the former is dense in $$\mathbf{H}$$, so is the latter. As $$A^{\text{cl}}$$ is closed, $$(\ast\ast)$$ lets us apply [Proposition (Closedness of the Range from a Lower Bound)](#prpstn:hall-9.14) with $$\varepsilon = 1$$, showing $$\text{Range}(A^{\text{cl}} - i\mathbf{1})$$ is closed; being both dense and closed, it equals $$\mathbf{H}$$. An identical argument, using density of $$\text{Range}(A + i\mathbf{1})$$, shows $$\text{Range}(A^{\text{cl}} + i\mathbf{1}) = \mathbf{H}$$ as well.

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
> This inner product is well defined, and $$\mathbf{H}$$ is complete with respect to it; hence $$\mathbf{H}$$, with this inner product, is itself a separable, complex Hilbert space.

The finite direct sum is dense in the full direct sum. This is used in the proof of [**Proposition** *(Direct Sums of Bounded Self-Adjoint Operators)*](#prpstn:hall-9.26) below, so we record it as a lemma rather than as part of the definition.

> **Lemma** *(The Finite Direct Sum is Dense)*
<a name="lmm:finite-direct-sum-dense"></a>
<!--  \uses{def:hall-a.45} -->
> With notation as in [Definition (Hilbert Space Direct Sum)](#def:hall-a.45), the finite direct sum — the set of sequences with only finitely many non-zero entries — is a dense subspace of $$\mathbf{H} = \bigoplus_j \mathbf{H}_j$$.

**Proof**
It is a subspace, being closed under componentwise linear combinations (a linear combination of two sequences each with finitely many non-zero entries again has finitely many). For density, let $$\psi = (\psi_1,\psi_2,\ldots) \in \mathbf{H}$$ and put $$\psi^{(N)} \equiv (\psi_1,\ldots,\psi_N,0,0,\ldots)$$, which lies in the finite direct sum. Then

$$
    \left\| \psi - \psi^{(N)} \right\|^2 = \sum_{j > N} \left\| \psi_j \right\|_j^2 \longrightarrow 0 \qquad (N \to \infty),
$$

being the tail of the series $$\sum_j \left\| \psi_j \right\|_j^2$$, which converges to $$\left\| \psi \right\|^2$$ by the definition of $$\mathbf{H}$$. So every $$\psi \in \mathbf{H}$$ is a norm limit of elements of the finite direct sum.$$\blacksquare$$

The direct sum just defined is an *external* construction: its elements are sequences, and the summands $$\mathbf{H}_j$$ are separate spaces glued together. In practice we more often meet the *internal* situation: a single Hilbert space $$\mathbf{H}$$ together with a family of closed subspaces of $$\mathbf{H}$$ that decompose it. These are not literally the same object, so we record the notion and the identification between the two explicitly rather than passing between them silently.

The identification below is by a *unitary* map, so we record that notion first; it is needed again, for a different purpose, in the Cayley transform of the final section.

> **Definition** *(Unitary Operator)*
<a name="def:unitary-operator"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> An operator $$U \in \mathcal{B}(\mathbf{H})$$ is *unitary* if it is a bijection of $$\mathbf{H}$$ onto $$\mathbf{H}$$ and preserves the inner product: $$\left< U\phi, U\psi \right> = \left< \phi,\psi \right>$$ for all $$\phi,\psi \in \mathbf{H}$$.

> **Definition** *(Internal Orthogonal Decomposition)*
<a name="def:internal-orthogonal-decomposition"></a>
<!--  \uses{../spectral-theorems/#def:orthogonal-complement} -->
> A sequence $$\{ \mathbf{K}_n \}_{n=1}^\infty$$ of closed subspaces of $$\mathbf{H}$$ is an *internal orthogonal decomposition* of $$\mathbf{H}$$ if
>
> 1. the subspaces are pairwise orthogonal: $$\left< \eta, \zeta \right> = 0$$ whenever $$\eta \in \mathbf{K}_n$$, $$\zeta \in \mathbf{K}_m$$ with $$n \ne m$$; and
> 2. every $$\psi \in \mathbf{H}$$ can be written as $$\psi = \sum_{n=1}^\infty \psi_n$$ with $$\psi_n \in \mathbf{K}_n$$, the series converging in the norm of $$\mathbf{H}$$.

A norm-preserving linear map automatically preserves the inner product, because the inner product is recoverable from the norm. We record the identity that makes this so, since it is what verifies unitarity of the Cayley transform in the final section.

> **Proposition** *(Polarization Identity for the Inner Product)*
<a name="prpstn:polarization-identity"></a>
> For all $$\phi,\psi \in \mathbf{H}$$,
>
> $$
>     \left< \phi, \psi \right> = \frac{1}{4}\Big( \left\| \phi+\psi \right\|^2 - \left\| \phi-\psi \right\|^2 \Big) - \frac{i}{4}\Big( \left\| \phi+i\psi \right\|^2 - \left\| \phi-i\psi \right\|^2 \Big).
> $$
>
> Consequently, if $$T : \mathbf{H} \to \mathbf{H}$$ is linear and norm-preserving, then $$T$$ preserves the inner product: $$\left< T\phi, T\psi \right> = \left< \phi,\psi \right>$$ for all $$\phi,\psi$$.

**Proof**
Expanding by conjugate-linearity in the first argument and linearity in the second,

$$
\begin{align}
    \left\| \phi \pm \psi \right\|^2 &= \left\| \phi \right\|^2 + \left\| \psi \right\|^2 \pm \left< \phi,\psi \right> \pm \left< \psi,\phi \right>, \\
    \left\| \phi \pm i\psi \right\|^2 &= \left\| \phi \right\|^2 + \left\| \psi \right\|^2 \pm i\left< \phi,\psi \right> \mp i\left< \psi,\phi \right>,
\end{align}
$$

the second line using $$\left< \phi, i\psi \right> = i\left< \phi,\psi \right>$$ and $$\left< i\psi, \phi \right> = -i\left< \psi,\phi \right>$$. Subtracting within each line,

$$
    \left\| \phi+\psi \right\|^2 - \left\| \phi-\psi \right\|^2 = 2\big( \left< \phi,\psi \right> + \left< \psi,\phi \right> \big), \qquad
    \left\| \phi+i\psi \right\|^2 - \left\| \phi-i\psi \right\|^2 = 2i\big( \left< \phi,\psi \right> - \left< \psi,\phi \right> \big).
$$

Multiplying the first by $$\tfrac14$$ and the second by $$-\tfrac{i}{4}$$ and adding, the $$\left< \psi,\phi \right>$$ terms cancel — $$\tfrac12\left< \psi,\phi \right>$$ from the first and $$-\tfrac{i}{4}\cdot(-2i)\left< \psi,\phi \right> = -\tfrac12\left< \psi,\phi \right>$$ from the second — while the $$\left< \phi,\psi \right>$$ terms combine to $$\tfrac12\left< \phi,\psi \right> + \tfrac12\left< \phi,\psi \right> = \left< \phi,\psi \right>$$. This is the stated identity.

For the consequence, suppose $$T$$ is linear with $$\left\| T\chi \right\| = \left\| \chi \right\|$$ for all $$\chi$$. Applying the identity to $$T\phi, T\psi$$ and using linearity of $$T$$ to write $$T\phi \pm T\psi = T(\phi\pm\psi)$$ and $$T\phi \pm iT\psi = T(\phi\pm i\psi)$$, each of the four norms equals the corresponding norm without $$T$$; so the right-hand sides agree and $$\left< T\phi,T\psi \right> = \left< \phi,\psi \right>$$.$$\blacksquare$$

> **Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*
<a name="lmm:internal-decomposition-unitary"></a>
<!--  \uses{def:internal-orthogonal-decomposition} -->
<!--  \uses{def:hall-a.45} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{def:unitary-operator} -->
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
<!--  \uses{lmm:finite-direct-sum-dense} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{prpstn:convergence-facts} -->
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
**Part 1: $$A$$ is essentially self-adjoint.** Fix $$j$$. We claim $$A_j \mp i\mathbf{1}$$ maps $$\mathbf{H}_j$$ onto $$\mathbf{H}_j$$.

If $$\mathbf{H}_j = \{0\}$$, this is immediate: the only operator on $$\{0\}$$ is the zero map, and it is trivially surjective onto $$\{0\}$$. (We treat this degenerate case separately because the route used below passes through [Proposition (Spectrum of a Bounded Self-Adjoint Operator)](../spectral-theorems/#prpstn:hall-7.7), whose statement asserts that $$\sigma(A_j)$$ is *non-empty* — which fails when $$\mathbf{H}_j = \{0\}$$, since then every $$\lambda$$ lies in the resolvent set and $$\sigma(A_j) = \emptyset$$. The conclusion we need is unaffected, but the cited route is unavailable, so we discharge the case directly.)

Suppose then $$\mathbf{H}_j \ne \{0\}$$. Since $$A_j$$ is a bounded self-adjoint operator on $$\mathbf{H}_j$$, [Proposition (Spectrum of a Bounded Self-Adjoint Operator)](../spectral-theorems/#prpstn:hall-7.7) shows $$\sigma(A_j) \subset \mathbb{R}$$, so $$\pm i \notin \sigma(A_j)$$, i.e. $$\pm i$$ lie in the resolvent set of $$A_j$$: the bounded operators $$A_j \mp i\mathbf{1}$$ have bounded two-sided inverses, and an operator with a two-sided inverse is in particular surjective, so $$A_j \mp i\mathbf{1}$$ maps onto $$\mathbf{H}_j$$. Let $$J_j : \mathbf{H}_j \to \mathbf{H}$$ denote the isometric embedding of $$\mathbf{H}_j$$ as the $$j$$-th summand (all other coordinates zero); note $$J_j(\mathbf{H}_j) \subset W_0 \subset \text{Dom}(A)$$, and, by hypothesis on $$A$$, $$A J_j(\eta) = J_j(A_j \eta)$$ for $$\eta \in \mathbf{H}_j$$. Hence, by linearity of $$A$$,

$$
    (A - i\mathbf{1}) J_j(\eta) = AJ_j(\eta) - iJ_j(\eta) = J_j(A_j \eta) - iJ_j(\eta) = J_j\big( (A_j - i\mathbf{1})\eta \big),
$$

using linearity of $$J_j$$ for the last step. So $$J_j\big( \text{Range}(A_j - i\mathbf{1}) \big) \subset \text{Range}(A - i\mathbf{1})$$; since $$A_j - i\mathbf{1}$$ is surjective onto $$\mathbf{H}_j$$, this reads $$J_j(\mathbf{H}_j) \subset \text{Range}(A - i\mathbf{1})$$. As this holds for every $$j$$, and $$\text{Range}(A - i\mathbf{1})$$ is a subspace (by linearity of $$A - i\mathbf{1}$$ on $$\text{Dom}(A)$$), $$\text{Range}(A - i\mathbf{1})$$ contains every finite sum of elements from the $$J_j(\mathbf{H}_j)$$'s, i.e. $$W_0 \subset \text{Range}(A - i\mathbf{1})$$. By [**Lemma** *(The Finite Direct Sum is Dense)*](#lmm:finite-direct-sum-dense), $$W_0$$ is dense in $$\mathbf{H}$$, so $$\text{Range}(A - i\mathbf{1})$$ — being a superset of the dense subset $$W_0$$ — is itself dense in $$\mathbf{H}$$. An identical argument with $$i$$ replaced by $$-i$$ shows $$\text{Range}(A + i\mathbf{1})$$ is dense in $$\mathbf{H}$$. Since $$A$$ is symmetric by hypothesis, [Theorem (Essential Self-Adjointness via Dense Range)](#thrm:hall-9.21) shows $$A$$ is essentially self-adjoint.

**Part 2: reduction to $$\text{Dom}(A) = W_0$$.** We first check $$A\vert_{W_0}$$ is itself a legitimate unbounded operator to which **Part 1**'s argument applies, and that it is symmetric. By [Definition (Hilbert Space Direct Sum)](#def:hall-a.45), the finite direct sum $$W_0$$ is dense in $$\mathbf{H}$$, so $$A\vert_{W_0}$$, with domain $$W_0$$, is an unbounded operator in the sense of [Definition (Unbounded Operator)](#def:hall-3.1). For symmetry: since $$W_0 \subset \text{Dom}(A)$$ and $$A\vert_{W_0} = A$$ on $$W_0$$, for $$\phi,\psi \in W_0$$, symmetry of $$A$$ gives $$\left< \phi, (A\vert_{W_0})\psi \right> = \left< \phi, A\psi \right> = \left< A\phi, \psi \right> = \left< (A\vert_{W_0})\phi, \psi \right>$$, which is the [definition of symmetric](#def:hall-9.2) for $$A\vert_{W_0}$$.

The argument of **Part 1**, applied verbatim to $$A\vert_{W_0}$$ in place of $$A$$ (it only used that $$J_j(\mathbf{H}_j) \subset W_0 = \text{Dom}(A\vert_{W_0})$$, that $$A\vert_{W_0}$$ agrees with $$A_j$$ there, and symmetry of $$A\vert_{W_0}$$, all just established), shows $$A\vert_{W_0}$$ is also essentially self-adjoint.

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

for every $$N$$. The partial sums $$\sum_{j=1}^N \left\| A_j\phi_j \right\|_j^2$$ are non-decreasing in $$N$$ and bounded above by $$C^2$$, so, by Part 1 of [**Proposition** *(Convergence Facts for Sequences and Series)*](#prpstn:convergence-facts), the sequence converges, giving $$\sum_{j=1}^\infty \left\| A_j\phi_j \right\|_j^2 < \infty$$. Since also $$\phi \in \mathbf{H} = \bigoplus_j \mathbf{H}_j$$ gives $$\sum_j \left\| \phi_j \right\|_j^2 < \infty$$ automatically, we conclude $$\phi \in V$$.

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
<!--  \uses{def:unitary-operator} -->
<!--  \uses{def:hall-3.1} -->
<!--  \uses{prpstn:hall-9.10} -->
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
Let $$U : \mathbf{H} \to \bigoplus_n \mathbf{K}_n$$ be the unitary map of Part 3 of [**Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*](#lmm:internal-decomposition-unitary), $$U\psi = (\psi_1,\psi_2,\ldots)$$. Write $$\widetilde{\mathbf{H}} \equiv \bigoplus_n \mathbf{K}_n$$ for the external direct sum, and define $$\widetilde{A} \equiv UAU^{-1}$$, an operator on $$\widetilde{\mathbf{H}}$$ with $$\text{Dom}(\widetilde{A}) = U\big(\text{Dom}(A)\big)$$. This is an unbounded operator in the sense of [Definition (Unbounded Operator)](#def:hall-3.1): it is linear, being a composition of linear maps, and its domain is dense, since $$U$$ is a surjective isometry — hence a homeomorphism — and $$\text{Dom}(A)$$ is dense in $$\mathbf{H}$$, so its image under $$U$$ is dense in $$\widetilde{\mathbf{H}}$$.

Since $$U$$ is a unitary bijection, it carries all the structure in the hypotheses across. Explicitly: $$U(W_0)$$ is exactly the finite direct sum of the $$\mathbf{K}_n$$'s (a finite sum $$\sum_{n=1}^N \eta_n$$ maps to the sequence with entries $$\eta_1,\ldots,\eta_N$$ and zeros beyond, and conversely), so $$\text{Dom}(\widetilde{A}) \supset U(W_0)$$ is the finite direct sum; and for such an element, $$\widetilde{A}(\eta_1,\ldots,\eta_N,0,\ldots) = U A \left( \sum_n \eta_n \right) = U\left( \sum_n A_n\eta_n \right) = (A_1\eta_1,\ldots,A_N\eta_N,0,\ldots)$$, matching the hypothesis of [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26). Moreover $$\widetilde{A}$$ is symmetric: for $$\widetilde\phi,\widetilde\psi \in \text{Dom}(\widetilde{A})$$, writing $$\phi = U^{-1}\widetilde\phi$$, $$\psi = U^{-1}\widetilde\psi \in \text{Dom}(A)$$, unitarity of $$U$$ (hence of $$U^{-1}$$) gives $$\left< \widetilde\phi, \widetilde{A}\widetilde\psi \right> = \left< \phi, A\psi \right> = \left< A\phi, \psi \right> = \left< \widetilde{A}\widetilde\phi, \widetilde\psi \right>$$, using symmetry of $$A$$ in the middle.

So [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) applies to $$\widetilde{A}$$ on $$\widetilde{\mathbf{H}}$$ and gives: $$\widetilde{A}$$ is essentially self-adjoint, with $$\text{Dom}(\widetilde{A}^{\text{cl}}) = \text{Dom}(\widetilde{A}^*) = \widetilde{V}$$, where $$\widetilde{V} = \{ (\psi_1,\psi_2,\ldots) \mid \sum_n ( \|\psi_n\|^2 + \|A_n\psi_n\|^2 ) < \infty \}$$, and $$\widetilde{A}^{\text{cl}}(\psi_1,\psi_2,\ldots) = (A_1\psi_1, A_2\psi_2,\ldots)$$ there.

Finally we transport back. A unitary $$U$$ intertwines adjoints and closures: $$(UAU^{-1})^* = U A^* U^{-1}$$ — since, for $$\widetilde\phi,\widetilde\psi$$, $$\left< \widetilde\phi, UAU^{-1}\widetilde\psi \right> = \left< U^{-1}\widetilde\phi, A U^{-1}\widetilde\psi \right>$$, so boundedness of $$\widetilde\psi \mapsto \left< \widetilde\phi, \widetilde{A}\widetilde\psi \right>$$ on $$\text{Dom}(\widetilde A)$$ is equivalent to boundedness of $$\psi \mapsto \left< U^{-1}\widetilde\phi, A\psi \right>$$ on $$\text{Dom}(A)$$, matching domains under $$U$$ by the [definition of the adjoint](#def:hall-9.1), with the values corresponding likewise — and $$(UAU^{-1})^{\text{cl}} = U A^{\text{cl}} U^{-1}$$, since $$U \times U$$ is a homeomorphism of $$\mathbf{H}\times\mathbf{H}$$ onto $$\widetilde{\mathbf{H}}\times\widetilde{\mathbf{H}}$$ (being unitary in each factor) and so carries the closure of the graph of $$A$$ onto the closure of the graph of $$\widetilde{A}$$. Hence $$A$$ is essentially self-adjoint (as $$A^{\text{cl}} = U^{-1}\widetilde{A}^{\text{cl}}U$$ is self-adjoint, $$\widetilde{A}^{\text{cl}}$$ being so), and

$$
    \text{Dom}(A^{\text{cl}}) = \text{Dom}(A^*) = U^{-1}(\widetilde{V}) = V,
$$

the last equality because $$U\psi = (\psi_1,\psi_2,\ldots)$$, so the defining condition of $$\widetilde{V}$$ on $$U\psi$$ is verbatim the defining condition of $$V$$ on $$\psi$$. For $$\psi \in V$$, $$A^{\text{cl}}\psi = U^{-1}\widetilde{A}^{\text{cl}}U\psi = U^{-1}(A_1\psi_1,A_2\psi_2,\ldots) = \sum_n A_n\psi_n$$, the second equality by the formula for $$\widetilde{A}^{\text{cl}}$$ above (applicable since $$U\psi \in \widetilde{V}$$) and the last by the definition of $$U^{-1}$$ — the element of $$\mathbf{H}$$ whose decomposition has $$n$$-th entry $$A_n\psi_n$$, which is exactly the norm-convergent sum $$\sum_n A_n\psi_n$$, this lying in $$\mathbf{H}$$ because $$\sum_n \left\| A_n\psi_n \right\|^2 < \infty$$ for $$\psi \in V$$.

Finally, the same formula holds for $$A^*$$: since $$A$$ is essentially self-adjoint, [**Proposition** *(The Adjoint of a Closure)*](#prpstn:hall-9.10) gives $$A^* = (A^{\text{cl}})^*$$, and $$A^{\text{cl}}$$ is self-adjoint, so $$(A^{\text{cl}})^* = A^{\text{cl}}$$; hence $$A^* = A^{\text{cl}}$$, with the same domain $$V$$ and the same action.$$\blacksquare$$

## Integration Against a Projection-Valued Measure

The [previous post](../spectral-theorems) constructed, for a projection-valued measure $$\mu$$ on $$(X, \Omega(X))$$, an integral $$f \mapsto \int_X f \, d\mu$$ defined on *bounded* measurable functions $$f$$, landing in $$\mathcal{B}(\mathbf{H})$$. To state [Theorem 10.4](#thrm:hall-10.4), we need to make sense of $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ where the integrand $$\lambda \mapsto \lambda$$ is typically an *unbounded* function on $$\sigma(A)$$ — so the resulting integral will typically be an unbounded operator, and we need to say what its domain is. This section develops that theory in general, for an arbitrary (possibly unbounded) measurable function against an arbitrary projection-valued measure.

Recall that for $$\psi \in \mathbf{H}$$, $$\mu_\psi$$ denotes the [associated measure](../spectral-theorems/#thrm:projection-valued-measures-associated-measure) $$\mu_\psi(E) \equiv \left< \psi, \mu(E)\psi \right>$$, a positive, real-valued measure on $$(X, \Omega(X))$$. The starting point is the following norm identity for the bounded integral, which is used at several points below and which motivates the definition of the domain in the unbounded case.

The associated measures are finite, with total mass determined by $$\psi$$. The previous post's [**Theorem** *(Associated Measure)*](../spectral-theorems/#thrm:projection-valued-measures-associated-measure) supplies only that $$\mu_\psi$$ is a positive real-valued measure, so we record the total mass separately; it is used repeatedly below, both to apply convergence theorems that need a finite measure and to bound integrals.

> **Convention** *(Standing Hypotheses for this Section)*
<a name="conv:section-integration"></a>
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
> Throughout this section, $$(X,\Omega(X))$$ denotes a measurable space and $$\mu$$ a projection-valued measure on $$\Omega(X)$$ with values in $$\mathcal{B}(\mathbf{H})$$; "measurable" means $$\Omega(X)$$-measurable. For $$\psi \in \mathbf{H}$$, $$\mu_\psi$$ denotes the associated measure $$E \mapsto \left< \psi, \mu(E)\psi \right>$$. Statements below that mention $$X$$, $$\Omega(X)$$, $$\mu$$ or $$\mu_\psi$$ without introducing them are to be read as carrying these as hypotheses; a formalization should take them as parameters of the corresponding result.

> **Lemma** *(The Associated Measure has Total Mass $$\left\| \psi \right\|^2$$)*
<a name="lmm:associated-measure-total-mass"></a>
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{conv:section-integration} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$ and $$\psi \in \mathbf{H}$$. Then
>
> $$
>     \mu_\psi(X) = \left\| \psi \right\|^2 < \infty;
> $$
>
> in particular $$\mu_\psi$$ is a finite measure, and $$\mu_\psi(E) \le \left\| \psi \right\|^2$$ for every $$E \in \Omega(X)$$.

**Proof**
By the definition of $$\mu_\psi$$ and property 2 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure), which gives $$\mu(X) = \mathbf{1}$$,

$$
    \mu_\psi(X) = \left< \psi, \mu(X)\psi \right> = \left< \psi, \mathbf{1}\psi \right> = \left< \psi,\psi \right> = \left\| \psi \right\|^2,
$$

finite since $$\psi \in \mathbf{H}$$. The final claim follows since $$\mu_\psi$$ is a positive measure, so is monotone: $$E \subset X$$ gives $$\mu_\psi(E) \le \mu_\psi(X)$$.$$\blacksquare$$

> **Lemma** *(Norm Identity for the Bounded Integral)*
<a name="lmm:norm-identity-bounded-integral"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-9.1} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$ and let $$f : X \to \mathbb{C}$$ be bounded and measurable. Then for every $$\psi \in \mathbf{H}$$,
>
> $$
>     \left\| \left( \int_X f \, d\mu \right) \psi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi.
> $$

**Proof**
Combining multiplicativity of the integral with the fact that integration intertwines complex conjugation and the adjoint — properties 3 and 4 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) — and using the [definition of the adjoint](#def:hall-9.1) for the first equality,

$$
\begin{align}
    \left\| \left( \int_X f \, d\mu \right) \psi \right\|^2 &= \left< \psi, \left( \int_X f \, d\mu \right)^* \left( \int_X f \, d\mu \right) \psi \right> \\
                                                             &= \left< \psi, \left( \int_X \overline{f} \, d\mu \right)\left( \int_X f \, d\mu \right) \psi \right> \\
                                                             &= \left< \psi, \left( \int_X \lvert f \rvert^2 \, d\mu \right) \psi \right> \\
                                                             &= \int_X \lvert f \rvert^2 \, d\mu_\psi,
\end{align}
$$

the last equality being the defining property of the integral, applied to the bounded function $$\lvert f \rvert^2 = \overline{f}f$$.$$\blacksquare$$

If $$f$$ is *unbounded*, this identity suggests defining the domain of $$\int_X f \, d\mu$$ to be exactly the set of $$\psi$$ for which $$\int_X \lvert f \rvert^2 \, d\mu_\psi$$ is finite. Before making this precise, we need a version of the "quadratic form" and "sesquilinear form" machinery from the previous post that allows for a domain other than all of $$\mathbf{H}$$ — a subspace, not even necessarily dense, since we will want to apply this machinery to $$\mathbf{H}_n$$, a typically non-dense closed subspace, in the proof of [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3) below.

> **Definition** *(Sesquilinear Form on a Subspace)*
<a name="def:hall-sesquilinear-form-on-a-subspace"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#def:bounded-sesquilinear-form} -->
> Let $$D$$ be a subspace of $$\mathbf{H}$$. A *sesquilinear form on $$D$$* is a map $$L : D \times D \to \mathbb{C}$$ that is conjugate-linear in its first argument and linear in its second argument. As with quadratic forms below, taking $$D = \mathbf{H}$$ recovers the previous post's [definition of a sesquilinear form](../spectral-theorems/#def:bounded-sesquilinear-form), and taking $$D$$ a closed subspace recovers that definition on the Hilbert space $$D$$.

> **Definition** *(Quadratic Form on a Subspace)*
<a name="def:hall-quadratic-form-on-a-subspace"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{def:hall-sesquilinear-form-on-a-subspace} -->
<!--  \uses{../spectral-theorems/#def:bounded-quadratic-form} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.61} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
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
> A quadratic form $$Q$$ on $$D$$ is *bounded* if there is a constant $$C \in \mathbb{R}$$ with $$\lvert Q(\psi) \rvert \le C\left\| \psi \right\|^2$$ for all $$\psi \in D$$.
>
> Two identifications with the previous post's notions will be used, and both are immediate from comparing the definitions rather than requiring proof. First, when $$D = \mathbf{H}$$, the conditions above are literally the previous post's [definition of a (bounded) quadratic form](../spectral-theorems/#def:bounded-quadratic-form) — the same two properties, the same polarization formula, and the same boundedness inequality. Second, and this is the form in which it is applied to $$\mathbf{H}_n$$ in [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3): if $$D$$ is a *closed* subspace of $$\mathbf{H}$$, then $$D$$ is itself a Hilbert space under the inherited inner product, and a (bounded) quadratic form on $$D$$ in the present sense is exactly a (bounded) quadratic form on the Hilbert space $$D$$ in the previous post's sense — the inherited norm on $$D$$ being the restriction of the norm on $$\mathbf{H}$$, so the two boundedness inequalities are the same inequality. This is what licenses applying results such as [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63) with $$D$$ in place of $$\mathbf{H}$$.

Two elementary facts about quadratic forms on a subspace, generalizing [**Proposition** *(hall-a.61)*](../spectral-theorems/#prpstn:hall-a.61) of the previous post from $$D = \mathbf{H}$$ to a general subspace $$D$$, will be used repeatedly below. Since the proof of the bounded-case proposition is purely algebraic manipulation of the polarization formula — at no point using that $$D = \mathbf{H}$$, that $$D$$ is dense, or that the relevant vectors range over all of $$\mathbf{H}$$, only that $$D$$ is closed under the linear combinations $$\phi+\psi$$, $$\phi+i\psi$$, $$i\psi$$ appearing in the polarization formula — the same computation goes through verbatim on any subspace $$D$$; we record the two properties we need and reprove them directly, rather than merely asserting the analogy.

> **Proposition** *(Properties of Quadratic Forms on a Subspace)*
<a name="prpstn:quadratic-forms-on-a-subspace-properties"></a>
<!--  \uses{conv:section-integration} -->
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

Since our forms are now defined on arbitrary subspaces, restriction to a smaller subspace is immediate; we record it, as it is exactly what lets us apply this machinery to $$\mathbf{H}_n$$ inside $$W_f$$ later.

> **Lemma** *(Restriction of a Quadratic Form to a Subspace)*
<a name="lmm:restriction-of-quadratic-form"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
> Let $$D' \subset D$$ be subspaces of $$\mathbf{H}$$ and $$Q$$ a quadratic form on $$D$$. Then $$Q\vert_{D'}$$ is a quadratic form on $$D'$$, and its associated sesquilinear form is the restriction to $$D' \times D'$$ of the sesquilinear form associated to $$Q$$.

**Proof**
Property 1 of the [definition of a quadratic form](#def:hall-quadratic-form-on-a-subspace) is inherited immediately: for $$\psi \in D' \subset D$$ and $$\lambda \in \mathbb{C}$$, $$\lambda\psi \in D'$$ ($$D'$$ being a subspace) and $$Q(\lambda\psi) = \lvert\lambda\rvert^2 Q(\psi)$$ holds because it holds in $$D$$. For property 2, note that the polarization formula defining the associated form involves only the values of $$Q$$ at $$\phi+\psi$$, $$\phi$$, $$\psi$$, $$\phi+i\psi$$, $$i\psi$$, all of which lie in $$D'$$ when $$\phi,\psi \in D'$$ ($$D'$$ being a subspace); so the form associated to $$Q\vert_{D'}$$ is given by the same formula with the same values, i.e. is the restriction $$L\vert_{D'\times D'}$$ of the form $$L$$ associated to $$Q$$. A restriction of a map that is conjugate-linear in its first and linear in its second argument, to a product of subspaces, retains those properties; so $$L\vert_{D'\times D'}$$ is a sesquilinear form on $$D'$$, verifying property 2.$$\blacksquare$$

The proofs of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2) and [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3) below draw on several standard facts of Lebesgue integration that neither this post nor the previous one has needed until now. [Hall](https://doi.org/10.1007/978-1-4614-7116-5) explicitly assumes these as background (Appendix A.2: "we assume those parts of measure theory that are entirely standard: the monotone convergence and dominated convergence theorems, $$L^p$$ spaces, and Fubini's theorem"), so, exactly as with Cauchy–Schwarz or the Bounded Linear Transformation Theorem, we state them here without proof.

> **Theorem** *(Monotone Convergence Theorem, for Integrals)*
<a name="thrm:monotone-convergence-theorem-for-integrals"></a>
<!--  \uses{conv:section-integration} -->
> Let $$(X, \Omega, \nu)$$ be a measure space, and let $$\{ g_n \}_{n \in \mathbb{N}}$$ be a sequence of nonnegative measurable functions on $$X$$ with $$g_n(x) \le g_{n+1}(x)$$ for all $$x \in X$$ and all $$n$$, converging pointwise to a function $$g$$. Then
>
> $$
>     \int_X g_n \, d\nu \longrightarrow \int_X g \, d\nu
> $$
>
> as $$n \to \infty$$ (an equality in $$[0, \infty]$$).

> **Theorem** *(Dominated Convergence Theorem)*
<a name="thrm:dominated-convergence-theorem"></a>
<!--  \uses{conv:section-integration} -->
> Let $$(X,\Omega,\nu)$$ be a measure space and $$\{g_n\}$$ measurable complex-valued functions on $$X$$ converging pointwise to $$g$$, with $$\lvert g_n \rvert \le G$$ for all $$n$$ and some $$\nu$$-integrable $$G$$. Then $$g$$ and each $$g_n$$ are $$\nu$$-integrable and $$\int_X g_n \, d\nu \to \int_X g \, d\nu$$.

> **Proposition** *(Linearity of the Integral in the Measure)*
<a name="prpstn:additivity-of-the-integral-in-the-measure"></a>
<!--  \uses{conv:section-integration} -->
> Let $$\nu, \nu'$$ be measures on $$(X,\Omega)$$, let $$c \ge 0$$ be a real constant, and let $$\nu + \nu'$$ and $$c\nu$$ denote the measures $$E \mapsto \nu(E)+\nu'(E)$$ and $$E \mapsto c\,\nu(E)$$ respectively. Then for every nonnegative measurable $$g$$ on $$X$$,
>
> $$
>     \int_X g \, d(\nu + \nu') = \int_X g \, d\nu + \int_X g \, d\nu'
>     \qquad\text{and}\qquad
>     \int_X g \, d(c\nu) = c\int_X g \, d\nu
> $$
>
> (equalities in $$[0,\infty]$$), and both hold for every $$g$$ integrable with respect to the measures involved. We refer to the first identity as *additivity* and the second as *homogeneity* in the measure.

> **Proposition** *(Monotonicity of the Integral in the Measure)*
<a name="prpstn:monotonicity-of-the-integral-in-the-measure"></a>
<!--  \uses{conv:section-integration} -->
> Let $$\nu, \nu'$$ be measures on $$(X, \Omega)$$ with $$\nu(E) \le \nu'(E)$$ for every $$E \in \Omega$$. Then $$\int_X g \, d\nu \le \int_X g \, d\nu'$$ for every nonnegative measurable $$g$$ on $$X$$.

> **Definition** *($$L^2$$ of a Measure Space)*
<a name="def:hall-a.46"></a>
<!--  \uses{conv:section-integration} -->
> Let $$(X,\Omega,\mu)$$ be a measure space and $$p \in \{1,2\}$$. Write
>
> $$
>     \mathcal{L}^p(X,\mu) \equiv \left\{ f : X \to \mathbb{C} \;\middle|\; f \text{ measurable and } \int_X \lvert f \rvert^p \, d\mu < \infty \right\},
> $$
>
> a complex vector space, and set $$\left\| f \right\|_{L^p(X,\mu)} \equiv \big( \int_X \lvert f \rvert^p \, d\mu \big)^{1/p}$$. Throughout this post the assertion "$$f \in L^p(X,\mu)$$" is shorthand for $$f \in \mathcal{L}^p(X,\mu)$$, i.e. for the integrability condition above; this is how the notation is used in every statement below.
>
> The quantity $$\left\| \cdot \right\|_{L^p(X,\mu)}$$ is a seminorm on $$\mathcal{L}^p(X,\mu)$$ but **not** a norm: a measurable $$f$$ that vanishes $$\mu$$-almost everywhere without being identically zero has $$\left\| f \right\|_{L^p(X,\mu)} = 0$$. To obtain a normed space one passes to the quotient
>
> $$
>     L^p(X,\mu) \equiv \mathcal{L}^p(X,\mu) \big/ \mathcal{N}, \qquad \mathcal{N} \equiv \{ f \text{ measurable} \mid f = 0 \ \mu\text{-almost everywhere} \},
> $$
>
> on which $$\left\| \cdot \right\|_{L^p(X,\mu)}$$ descends to a genuine norm. For $$p = 2$$ the formula
>
> $$
>     \left< \phi, \psi \right> \equiv \int_X \overline{\phi(x)} \, \psi(x) \, d\mu(x)
> $$
>
> is absolutely convergent for $$\phi,\psi \in \mathcal{L}^2(X,\mu)$$, descends to the quotient, and is there a genuine inner product inducing $$\left\| \cdot \right\|_{L^2(X,\mu)}$$; with it, $$L^2(X,\mu)$$ is complete, hence a Hilbert space. (The distinction matters for a formalization, where $$L^p$$ is a quotient type; it does not affect any argument below, all of which use only the seminorm and the integrability condition, never positive-definiteness.)

> **Proposition** *(Countable Additivity of the Integral over a Disjoint Cover)*
<a name="prpstn:countable-additivity-of-the-integral"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$(X,\Omega,\nu)$$ be a measure space, $$g$$ a nonnegative measurable function on $$X$$, and $$\{ E_n \}_{n=1}^\infty$$ a pairwise disjoint sequence in $$\Omega$$ with $$\bigcup_n E_n = X$$. Then
>
> $$
>     \int_X g \, d\nu = \sum_{n=1}^\infty \int_{E_n} g \, d\nu
> $$
>
> (an equality in $$[0,\infty]$$).

> **Proposition** *(Integrals Agree when Measures Agree on a Set)*
<a name="prpstn:integrals-agree-when-measures-agree"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$\nu, \nu'$$ be measures on $$(X,\Omega)$$ and $$E \in \Omega$$, and suppose $$\nu(S) = \nu'(S)$$ for every measurable $$S \subset E$$. Then $$\int_E g \, d\nu = \int_E g \, d\nu'$$ for every nonnegative measurable $$g$$ on $$X$$.

We record two more facts about projection-valued measures before the main proof, both used more than once below; extracting them now avoids re-deriving them, or worse, citing "the same argument as" a proof written for a different purpose. First, though, a fact about a single projection, used at several places to know that ranges of projections are closed subspaces.

> **Lemma** *(The Range of a Projection is the Kernel of its Complement)*
<a name="lmm:range-of-projection-is-kernel"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
> Let $$P \in \mathcal{B}(\mathbf{H})$$ be a bounded orthogonal projection. Then $$\text{Range}(P) = \text{Ker}(\mathbf{1} - P)$$, and this is a closed subspace of $$\mathbf{H}$$. Moreover $$\eta \in \text{Range}(P)$$ if and only if $$P\eta = \eta$$.

**Proof**
If $$\eta \in \text{Range}(P)$$, write $$\eta = P\xi$$; idempotency of $$P$$ (part of being a [bounded orthogonal projection](../spectral-theorems/#def:bounded-orthogonal-projection)) gives $$P\eta = P^2\xi = P\xi = \eta$$, so $$(\mathbf{1}-P)\eta = 0$$, i.e. $$\eta \in \text{Ker}(\mathbf{1}-P)$$. Conversely, if $$(\mathbf{1}-P)\eta = 0$$ then $$\eta = P\eta \in \text{Range}(P)$$. This proves both the set equality and the final characterization ($$\eta \in \text{Range}(P)$$ iff $$P\eta = \eta$$, the two conditions $$P\eta=\eta$$ and $$(\mathbf{1}-P)\eta=0$$ being the same equation).

For closedness: $$\mathbf{1} - P$$ is bounded, hence continuous, so $$\text{Ker}(\mathbf{1}-P) = (\mathbf{1}-P)^{-1}(\{0\})$$ is the preimage of the closed set $$\{0\}$$ under a continuous map, hence closed. It is a subspace by linearity of $$\mathbf{1}-P$$.$$\blacksquare$$


Closed subspaces recur as Hilbert spaces in their own right — the whole development is instantiated on them at several points — so we record that fact once.

> **Lemma** *(A Closed Subspace is a Separable Hilbert Space)*
<a name="lmm:closed-subspace-is-hilbert"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{thrm:sequential-closedness} -->
> Let $$V$$ be a closed subspace of $$\mathbf{H}$$. Then $$V$$, with the inner product inherited from $$\mathbf{H}$$, is itself a separable, complex Hilbert space, and its norm is the restriction of the norm of $$\mathbf{H}$$.

**Proof**
The inner-product axioms hold on $$V$$ because they hold on $$\mathbf{H}$$ and $$V \subset \mathbf{H}$$ is a complex subspace, so the restricted form is again an inner product; the associated norm is by construction the restriction of that of $$\mathbf{H}$$. For completeness, a Cauchy sequence in $$V$$ is Cauchy in $$\mathbf{H}$$, hence converges to some $$\psi \in \mathbf{H}$$ by completeness of $$\mathbf{H}$$; since $$V$$ is closed, $$\psi \in V$$ by [**Theorem** *(Sequential Characterization of Closed Sets and Closures)*](#thrm:sequential-closedness), and the convergence takes place in $$V$$. Separability is inherited: a subspace of a separable metric space is separable.$$\blacksquare$$

> **Lemma** *(Range Membership Concentrates the Associated Measure)*
<a name="lmm:range-membership-concentrates-measure"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X,\Omega(X))$$ and $$\eta \in \text{Range}(\mu(E))$$ for some $$E \in \Omega(X)$$. Then $$\mu_\eta(E^c) = 0$$. Consequently, for any nonnegative measurable $$g$$ on $$X$$,
>
> $$
>     \int_X g \, d\mu_\eta = \int_E g \, d\mu_\eta.
> $$

**Proof**
By [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel), applied to the bounded orthogonal projection $$\mu(E)$$ (property 1 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure)), $$\eta \in \text{Range}(\mu(E))$$ gives $$\mu(E)\eta = \eta$$. Hence, using property 4 of that definition together with $$E^c \cap E = \emptyset$$, and then property 2 ($$\mu(\emptyset) = 0$$),

$$
    \mu_\eta(E^c) = \left< \eta, \mu(E^c)\eta \right> = \left< \eta, \mu(E^c)\mu(E)\eta \right> = \left< \eta, \mu(E^c \cap E)\eta \right> = \left< \eta, \mu(\emptyset)\eta \right> = 0.
$$

For the consequence: since $$g \ge 0$$ and the measure of $$E^c$$ under $$\mu_\eta$$ is $$0$$, the portion of the integral over $$E^c$$ vanishes, and $$\int_X g\,d\mu_\eta = \int_E g\,d\mu_\eta + \int_{E^c} g\,d\mu_\eta = \int_E g\,d\mu_\eta + 0$$.$$\blacksquare$$

> **Lemma** *(Norm-Convergent Decomposition over a Disjoint Cover)*
<a name="lmm:norm-convergent-decomposition"></a>
<!--  \uses{conv:section-integration} -->
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
<!--  \uses{conv:section-integration} -->
<!--  \uses{def:hall-a.46} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
> Suppose $$\nu$$ is a finite measure on $$(X,\Omega)$$ and $$h \in L^2(X,\nu)$$. Then $$h \in L^1(X,\nu)$$, with $$\int_X \lvert h \rvert \, d\nu \le \nu(X)^{1/2} \left( \int_X \lvert h \rvert^2 \, d\nu \right)^{1/2}$$.

**Proof**
The constant function $$1$$ is square-integrable, since $$\int_X 1^2 \, d\nu = \nu(X) < \infty$$ ($$\nu$$ finite); and $$\lvert h \rvert$$ is square-integrable because $$h$$ is. So both lie in $$\mathcal{L}^2(X,\nu)$$ in the notation of [**Definition** *($$L^2$$ of a Measure Space)*](#def:hall-a.46).

[Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) is stated for a space carrying a genuine *inner* product, so we apply it not to the functions themselves — on which the form is only a semi-inner product — but to their classes $$[\lvert h \rvert], [1]$$ in the quotient $$L^2(X,\nu)$$, which is an inner product space by that definition. This changes none of the three quantities involved: for square-integrable $$\phi,\psi$$ the integrals $$\int_X \overline{\phi}\psi \, d\nu$$ and $$\int_X \lvert \phi \rvert^2 d\nu$$ depend only on the classes of $$\phi$$ and $$\psi$$, since altering a function on a $$\nu$$-null set changes no integral. Hence

$$
    \int_X \lvert h \rvert \, d\nu = \left< [\lvert h \rvert], [1] \right>_{L^2(X,\nu)} \le \left\| [\lvert h \rvert] \right\|_{L^2(X,\nu)} \left\| [1] \right\|_{L^2(X,\nu)} = \left( \int_X \lvert h \rvert^2 \, d\nu \right)^{1/2} \nu(X)^{1/2},
$$

the first equality because $$\overline{\lvert h \rvert}\cdot 1 = \lvert h \rvert$$ pointwise. The right-hand side is finite since $$h$$ is square-integrable and $$\nu(X) < \infty$$. So $$h \in L^1(X,\nu)$$, with the stated bound.$$\blacksquare$$

We can now state and prove the central technical result of this section. It is the unbounded analogue of the correspondence, from the previous post, between bounded operators and bounded quadratic forms.

> **Proposition**
<a name="prpstn:hall-10.2"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{thrm:monotone-convergence-theorem-for-integrals} -->
<!--  \uses{prpstn:monotonicity-of-the-integral-in-the-measure} -->
<!--  \uses{def:hall-a.46} -->
<!--  \uses{lmm:l2-implies-l1} -->
<!--  \uses{../spectral-theorems/#thrm:hall-a.52} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.62} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{lmm:norm-convergent-decomposition} -->
<!--  \uses{lmm:norm-identity-bounded-integral} -->
<!--  \uses{lmm:associated-measure-total-mass} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
<!--  \uses{prpstn:additivity-of-the-integral-in-the-measure} -->
> Let $$\mu$$ be a projection-valued measure on $$(X, \Omega(X))$$ with values in $$\mathcal{B}(\mathbf{H})$$, and let $$f : X \to \mathbb{C}$$ be a measurable function, not necessarily bounded (but everywhere finite-valued, since its values lie in $$\mathbb{C}$$ — this is used below, where the sets $$\{ \lvert f \rvert < n \}$$ are required to exhaust $$X$$). Let
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
Before checking any properties of $$Q_f$$, we note it is well defined: for $$\psi \in W_f$$, $$\mu_\psi$$ is a finite measure with $$\mu_\psi(X) = \left\| \psi \right\|^2 < \infty$$, by [**Lemma** *(The Associated Measure has Total Mass $$\left\| \psi \right\|^2$$)*](#lmm:associated-measure-total-mass), and $$f \in L^2(X,\mu_\psi)$$ (this is exactly the membership condition defining $$W_f$$), so [Lemma ($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)](#lmm:l2-implies-l1) gives $$f \in L^1(X,\mu_\psi)$$. Hence $$Q_f(\psi) = \int_X f \, d\mu_\psi$$ is a well-defined (finite) complex number for every $$\psi \in W_f$$, as required for $$Q_f$$ to be a map $$W_f \to \mathbb{C}$$ at all.

**Part 1.** We first check $$W_f$$ is a subspace. If $$\psi \in W_f$$ and $$\lambda \in \mathbb{C}$$, then, directly from the definition of $$\mu_{\lambda\psi}$$ and conjugate-linearity/linearity of the inner product in its two arguments,

$$
    \mu_{\lambda\psi}(E) = \left< \lambda\psi, \mu(E)\lambda\psi \right> = \overline{\lambda}\lambda \left< \psi, \mu(E)\psi \right> = \lvert \lambda \rvert^2 \mu_\psi(E)
$$

for every $$E \in \Omega(X)$$, so $$\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \mu_\psi$$ as measures on $$(X, \Omega(X))$$. Hence, by the homogeneity clause of [**Proposition** *(Linearity of the Integral in the Measure)*](#prpstn:additivity-of-the-integral-in-the-measure), $$\int_X \lvert f \rvert^2 \, d\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \int_X \lvert f \rvert^2 \, d\mu_\psi$$, which is finite exactly when $$\int_X \lvert f \rvert^2 \, d\mu_\psi$$ is (trivially, if $$\lambda = 0$$ both integrals are $$0$$); so $$\lambda\psi \in W_f$$.

For closure under addition, fix $$\phi, \psi \in \mathbf{H}$$ and $$E \in \Omega(X)$$. We first note that $$\mu_\eta(E) = \left\| \mu(E)\eta \right\|^2$$ for every $$\eta \in \mathbf{H}$$: since $$\mu(E)$$ is a [bounded orthogonal projection](../spectral-theorems/#def:bounded-orthogonal-projection), it is both self-adjoint and idempotent, so

$$
    \mu_\eta(E) = \left< \eta, \mu(E)\eta \right> = \left< \eta, \mu(E)^*\mu(E)\eta \right> = \left< \mu(E)\eta, \mu(E)\eta \right> = \left\| \mu(E)\eta \right\|^2,
$$

using idempotency ($$\mu(E) = \mu(E)^2 = \mu(E)^*\mu(E)$$, the last step by self-adjointness) for the second equality and the [definition of the adjoint](#def:hall-9.1) for the third. Applying this with $$\eta = \phi+\psi$$, and using the triangle inequality followed by the elementary inequality $$(x+y)^2 \le 2x^2 + 2y^2$$ for $$x, y \in \mathbb{R}$$,

$$
\begin{align}
    \mu_{\phi+\psi}(E) &= \left\| \mu(E)(\phi + \psi) \right\|^2 \\
                       &\le \left( \left\| \mu(E)\phi \right\| + \left\| \mu(E)\psi \right\| \right)^2 \\
                       &\le 2 \left\| \mu(E)\phi \right\|^2 + 2 \left\| \mu(E)\psi \right\|^2 \\
                       &= 2\mu_\phi(E) + 2\mu_\psi(E).
\end{align}
$$

As this holds for every $$E \in \Omega(X)$$, the measure $$\mu_{\phi+\psi}$$ is dominated by the finite measure $$2\mu_\phi + 2\mu_\psi$$, so by [**Monotonicity of the Integral in the Measure**](#prpstn:monotonicity-of-the-integral-in-the-measure), for any nonnegative measurable $$g$$ on $$X$$, $$\int_X g \, d\mu_{\phi+\psi} \le \int_X g \, d(2\mu_\phi + 2\mu_\psi) = 2\int_X g \, d\mu_\phi + 2\int_X g \, d\mu_\psi$$, applied with $$g = \lvert f \rvert^2$$. Thus, if $$\phi, \psi \in W_f$$, then $$\int_X \lvert f \rvert^2 \, d\mu_{\phi+\psi} \le 2\int_X \lvert f \rvert^2 \, d\mu_\phi + 2\int_X \lvert f \rvert^2 \, d\mu_\psi < \infty$$, so $$\phi + \psi \in W_f$$. Since also $$0 \in W_f$$ (as $$\mu_0 = 0$$, the zero measure), $$W_f$$ is a subspace of $$\mathbf{H}$$.

We next show $$W_f$$ is dense in $$\mathbf{H}$$. Here and throughout, $$\mathbb{N}$$ includes $$0$$, as fixed in [the previous post's notation conventions](../spectral-theorems/#def:identity-and-indicator); where an index must start at $$1$$ this is stated explicitly, as here. For each integer $$n \ge 1$$, let $$E_n \equiv \{ x \in X \mid \lvert f(x) \rvert < n \}$$, so $$E_1 \subset E_2 \subset \cdots$$ and, since $$f$$ is finite-valued at every point of $$X$$, $$\bigcup_{n} E_n = X$$. Fix $$\psi \in \mathbf{H}$$, and let $$F_1 \equiv E_1$$ and $$F_n \equiv E_n \setminus E_{n-1}$$ for $$n \ge 2$$; the $$F_n$$ are pairwise disjoint, $$\bigcup_{j=1}^n F_j = E_n$$ for every $$n$$ (immediate by induction: true for $$n=1$$, and if $$\bigcup_{j=1}^{n-1} F_j = E_{n-1}$$ then $$\bigcup_{j=1}^n F_j = E_{n-1} \cup (E_n \setminus E_{n-1}) = E_n$$, the last step because $$E_{n-1} \subset E_n$$), and $$\bigcup_{j=1}^\infty F_j = \bigcup_n E_n = X$$. By [Lemma (Norm-Convergent Decomposition over a Disjoint Cover)](#lmm:norm-convergent-decomposition), applied to this sequence $$\{F_n\}$$, $$\mu(E_n)\psi = \mu\big(\bigcup_{j=1}^n F_j\big)\psi \to \psi$$ as $$n \to \infty$$.

For each $$n$$, $$\mu(E_n)\psi \in \text{Range}(\mu(E_n))$$; and for $$\eta \in \text{Range}(\mu(E_n))$$, [Lemma (Range Membership Concentrates the Associated Measure)](#lmm:range-membership-concentrates-measure) gives $$\int_X \lvert f \rvert^2\,d\mu_\eta = \int_{E_n} \lvert f \rvert^2\,d\mu_\eta \le n^2 \mu_\eta(E_n) \le n^2 \mu_\eta(X) = n^2 \left\| \eta \right\|^2 < \infty$$ — using $$\lvert f \rvert < n$$ on $$E_n$$, and $$\mu_\eta(X) = \left\| \eta \right\|^2$$ by [**Lemma** *(The Associated Measure has Total Mass $$\left\| \psi \right\|^2$$)*](#lmm:associated-measure-total-mass). So $$\text{Range}(\mu(E_n)) \subset W_f$$ for every $$n$$. Since $$\mu(E_n)\psi \in \text{Range}(\mu(E_n)) \subset W_f$$ and $$\mu(E_n)\psi \to \psi$$, and $$\psi \in \mathbf{H}$$ was arbitrary, $$W_f$$ is dense in $$\mathbf{H}$$.

We now verify $$Q_f$$ satisfies the two properties required of a [quadratic form on $$W_f$$](#def:hall-quadratic-form-on-a-subspace). Property 1, $$Q_f(\lambda\psi) = \lvert \lambda \rvert^2 Q_f(\psi)$$, follows from $$\mu_{\lambda\psi} = \lvert \lambda \rvert^2 \mu_\psi$$ (shown above) together with the homogeneity clause of [**Proposition** *(Linearity of the Integral in the Measure)*](#prpstn:additivity-of-the-integral-in-the-measure), applied with $$c = \lvert \lambda \rvert^2 \ge 0$$: $$Q_f(\lambda\psi) = \int_X f \, d\mu_{\lambda\psi} = \int_X f \, d\big(\lvert\lambda\rvert^2\mu_\psi\big) = \lvert\lambda\rvert^2\int_X f\,d\mu_\psi = \lvert\lambda\rvert^2 Q_f(\psi)$$. For property 2, we first establish a convergence fact we will reuse in **Part 2** below. Fix $$\psi \in W_f$$, and set $$f_n \equiv f \cdot 1_{E_n}$$, a bounded measurable function for each $$n$$ (as $$\lvert f_n \rvert \le n$$). Writing $$f = (f_+ - f_-) + i(g_+ - g_-)$$ in terms of the (nonnegative, measurable) positive and negative parts of the real and imaginary parts of $$f$$, each of $$f_+ 1_{E_n}, f_- 1_{E_n}, g_+ 1_{E_n}, g_- 1_{E_n}$$ is a nondecreasing (in $$n$$) sequence of nonnegative measurable functions converging pointwise to $$f_+, f_-, g_+, g_-$$ respectively, since $$E_n \uparrow X$$. By the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals) applied to $$\mu_\psi$$-integrals of each of these four sequences, $$\int_X f_\pm 1_{E_n} \, d\mu_\psi \to \int_X f_\pm \, d\mu_\psi$$ and $$\int_X g_\pm 1_{E_n} \, d\mu_\psi \to \int_X g_\pm \, d\mu_\psi$$; by [Lemma ($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)](#lmm:l2-implies-l1) — applicable since $$\psi \in W_f$$ ensures $$f \in L^2(X, \mu_\psi)$$ and $$\mu_\psi$$ is a finite measure, by [**Lemma** *(The Associated Measure has Total Mass $$\left\| \psi \right\|^2$$)*](#lmm:associated-measure-total-mass) — $$f \in L^1(X,\mu_\psi)$$, so all four limiting integrals above are finite. Combining the four limits with appropriate signs,

$$
    Q_{f_n}(\psi) = \int_X f_n \, d\mu_\psi \longrightarrow \int_X f \, d\mu_\psi = Q_f(\psi). \tag{$\dagger$}
$$

More generally, the same argument, with $$\psi$$ replaced by an arbitrary $$\xi \in W_f$$ throughout (finiteness of $$\mu_\xi$$, membership of $$f$$ in $$L^2(X,\mu_\xi)$$ hence $$L^1(X,\mu_\xi)$$, and the Monotone Convergence Theorem applied to $$\mu_\xi$$-integrals), shows $$Q_{f_n}(\xi) \to Q_f(\xi)$$ for *every* $$\xi \in W_f$$, not just $$\xi = \psi$$ — indeed the same $$E_n$$'s work for every $$\xi \in W_f$$, since $$1_{E_n}$$ does not depend on $$\xi$$.

Now fix $$\phi, \psi \in W_f$$. Since $$W_f$$ is a subspace (shown above), $$\phi + \psi, \phi + i\psi, i\psi \in W_f$$, so by the previous paragraph, $$Q_{f_n}(\xi) \to Q_f(\xi)$$ for each of $$\xi \in \{ \phi + \psi, \phi, \psi, \phi + i\psi, i\psi \}$$. Each $$f_n$$ is bounded, so $$Q_{f_n}$$ is a genuine (bounded) quadratic form on all of $$\mathbf{H}$$ in the sense of the previous post — indeed $$Q_{f_n}(\xi) = \left< \xi, \left( \int_X f_n \, d\mu \right) \xi \right>$$ by the defining property of the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration), matching the construction of [**Proposition** *(hall-a.62)*](../spectral-theorems/#prpstn:hall-a.62) applied to the bounded operator $$\int_X f_n \, d\mu$$ — so its associated sesquilinear form $$L_{f_n}$$, given by the same polarization formula, is a genuine (bounded) sesquilinear form on $$\mathbf{H}$$, in particular conjugate-linear in its first argument and linear in its second.

We record explicitly the *off-diagonal* identity for $$L_{f_n}$$, used in **Part 2** below: applying Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) with $$D = \mathbf{H}$$, $$Q = Q_{f_n}$$ (a quadratic form on $$\mathbf{H}$$, just noted) and $$T = \int_X f_n \, d\mu \in \mathcal{B}(\mathbf{H})$$ (linear, and inducing $$Q_{f_n}$$ on the diagonal, also just noted),

$$
    L_{f_n}(\phi, \psi) = \left< \phi, \left( \int_X f_n \, d\mu \right) \psi \right> \qquad \text{for all } \phi, \psi \in \mathbf{H}. \tag{$\S$}
$$

Taking $$n \to \infty$$ in the polarization formula defining $$L_{f_n}(\phi, \psi)$$ term by term, each $$Q_{f_n}$$-term converges to the corresponding $$Q_f$$-term by the previous paragraph, so

$$
    L_{f_n}(\phi, \psi) \longrightarrow L_f(\phi, \psi)
$$

for all $$\phi, \psi \in W_f$$, where $$L_f$$ is defined on $$W_f$$ by the same polarization formula applied to $$Q_f$$. Since each relation $$L_{f_n}(\alpha\phi_1 + \beta\phi_2, \psi) = \overline{\alpha} L_{f_n}(\phi_1, \psi) + \overline{\beta} L_{f_n}(\phi_2, \psi)$$ (and the analogous relation for linearity in the second argument) holds for every $$n$$ — with all terms in $$W_f$$, hence covered by the convergence just established — taking $$n \to \infty$$ on both sides shows the same relations hold for $$L_f$$. Thus $$L_f$$ is a sesquilinear form on $$W_f$$, verifying property 2, and completing the proof that $$Q_f$$ is a quadratic form on $$W_f$$.

**Part 2.** Fix $$\phi, \psi \in W_f$$, and retain $$f_n = f \cdot 1_{E_n}$$ from **Part 1**. Since $$f_n$$ is bounded, [**Lemma** *(Norm Identity for the Bounded Integral)*](#lmm:norm-identity-bounded-integral) applies to $$f_n$$: $$\left\| \left( \int_X f_n \, d\mu \right) \eta \right\|^2 = \int_X \lvert f_n \rvert^2 \, d\mu_\eta$$ for all $$\eta \in \mathbf{H}$$. Combined with the off-diagonal identity $$(\S)$$ of **Part 1** and [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43),

$$
    \lvert L_{f_n}(\phi, \psi) \rvert \le \left\| \phi \right\| \left\| \left( \int_X f_n \, d\mu \right) \psi \right\| = \left\| \phi \right\| \left( \int_X \lvert f_n \rvert^2 \, d\mu_\psi \right)^{1/2}.
$$

By **Part 1**, $$L_{f_n}(\phi, \psi) \to L_f(\phi, \psi)$$ as $$n \to \infty$$. For the right-hand side, $$\lvert f_n \rvert^2 = \lvert f \rvert^2 1_{E_n}$$ is a nondecreasing sequence of nonnegative functions converging pointwise to $$\lvert f \rvert^2$$, so by the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals), $$\int_X \lvert f_n \rvert^2 \, d\mu_\psi \to \int_X \lvert f \rvert^2 \, d\mu_\psi = \left\| f \right\|_{L^2(X,\mu_\psi)}^2$$. Taking $$n \to \infty$$ in the displayed inequality gives $$\lvert L_f(\phi, \psi) \rvert \le \left\| \phi \right\| \left\| f \right\|_{L^2(X,\mu_\psi)}$$, the desired bound.

**Part 3.** Fix $$\psi \in W_f$$. By **Part 2**, the map $$\phi \mapsto L_f(\phi, \psi)$$ is bounded on $$W_f$$ with bound $$\left\| f \right\|_{L^2(X,\mu_\psi)}$$; since $$L_f$$ is conjugate-linear in $$\phi$$ (by **Part 1**), this map is a bounded conjugate-linear functional on $$W_f$$. Consider instead the map $$T : \phi \mapsto \overline{L_f(\phi, \psi)}$$, which is linear (conjugating a conjugate-linear map gives a linear map) and bounded with the same bound, on the dense subspace $$W_f$$ of $$\mathbf{H}$$. Exactly as in the justification following [Definition (Adjoint of an Unbounded Operator)](#def:hall-9.1) — $$\mathbf{H}$$ normed, $$\mathbb{C}$$ Banach, $$W_f$$ dense — the [**Bounded Linear Transformation Theorem**](../spectral-theorems/#thrm:bounded-linear-transformation-theorem) extends $$T$$ uniquely to a bounded linear functional $$\tilde{T}$$ on $$\mathbf{H}$$, and the [**Riesz Theorem**](../spectral-theorems/#thrm:hall-a.52) produces a unique $$\chi \in \mathbf{H}$$ with $$\tilde{T}\phi = \left< \chi, \phi \right>$$ for all $$\phi \in \mathbf{H}$$; restricting to $$\phi \in W_f$$, where $$\tilde T$$ agrees with $$T$$, and conjugating both sides,

$$
    L_f(\phi, \psi) = \overline{T\phi} = \overline{\left< \chi, \phi \right>} = \left< \phi, \chi \right>
$$

for all $$\phi \in W_f$$. Uniqueness of $$\chi$$ with this property follows from [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot), exactly as in the uniqueness argument for the adjoint.

For linearity of $$\psi \mapsto \chi$$: writing $$\chi_\psi$$ for the vector associated to $$\psi \in W_f$$, fix $$\psi_1, \psi_2 \in W_f$$ and $$\alpha, \beta \in \mathbb{C}$$. Since $$L_f$$ is linear in its second argument, for all $$\phi \in W_f$$,

$$
    L_f(\phi, \alpha\psi_1 + \beta\psi_2) = \alpha L_f(\phi, \psi_1) + \beta L_f(\phi, \psi_2) = \alpha \left< \phi, \chi_{\psi_1} \right> + \beta \left< \phi, \chi_{\psi_2} \right> = \left< \phi, \alpha\chi_{\psi_1} + \beta\chi_{\psi_2} \right>,
$$

using linearity of the inner product in its second argument for the last step. By uniqueness (via [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) again), $$\chi_{\alpha\psi_1 + \beta\psi_2} = \alpha\chi_{\psi_1} + \beta\chi_{\psi_2}$$.

Finally, we derive the norm formula $$\left\| \chi \right\|^2 = \int_X \lvert f \rvert^2 \, d\mu_\psi$$. Retain $$f_n = f \cdot 1_{E_n}$$ from **Part 1**, and set $$\chi_n \equiv \left( \int_X f_n \, d\mu \right)\psi \in \mathbf{H}$$ — well defined since $$f_n$$ is bounded, so $$\int_X f_n \, d\mu \in \mathcal{B}(\mathbf{H})$$. For any $$\phi \in W_f$$, the off-diagonal identity $$(\S)$$ of **Part 1** gives $$L_{f_n}(\phi,\psi) = \left< \phi, \chi_n \right>$$, which together with $$L_{f_n}(\phi,\psi) \to L_f(\phi,\psi) = \left< \phi, \chi \right>$$ (also **Part 1**) gives

$$
    \left< \phi, \chi_n \right> \longrightarrow \left< \phi, \chi \right> \quad \text{for every } \phi \in W_f. \tag{$\ddagger$}
$$

We show $$\{ \chi_n \}_{n \in \mathbb{N}}$$ is a Cauchy sequence in $$\mathbf{H}$$. For $$n < m$$, $$E_n \subset E_m$$ gives $$f_n - f_m = f \cdot 1_{E_n} - f \cdot 1_{E_m} = -f \cdot 1_{E_m \setminus E_n}$$, so, applying [**Lemma** *(Norm Identity for the Bounded Integral)*](#lmm:norm-identity-bounded-integral) to the bounded function $$f_n - f_m$$ and using linearity of the bounded integral,

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
<!--  \uses{conv:section-integration} -->
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{lmm:associated-measure-total-mass} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Suppose $$\mu$$ is a projection-valued measure on $$(X,\Omega(X))$$, $$f : X \to \mathbb{C}$$ is measurable, and $$E \in \Omega(X)$$ is a set on which $$f$$ is bounded, say $$\lvert f \rvert \le c$$ on $$E$$. Then $$\text{Range}(\mu(E)) \subset W_f$$, and indeed $$\int_X \lvert f \rvert^2\,d\mu_\eta \le c^2 \left\| \eta \right\|^2$$ for every $$\eta \in \text{Range}(\mu(E))$$.

**Proof**
Let $$\eta \in \text{Range}(\mu(E))$$. By [**Lemma** *(Range Membership Concentrates the Associated Measure)*](#lmm:range-membership-concentrates-measure), $$\int_X \lvert f \rvert^2 \, d\mu_\eta = \int_E \lvert f \rvert^2 \, d\mu_\eta$$. Since $$\lvert f \rvert \le c$$ on $$E$$,

$$
    \int_E \lvert f \rvert^2 \, d\mu_\eta \le c^2 \mu_\eta(E) \le c^2 \mu_\eta(X) = c^2 \left\| \eta \right\|^2 < \infty,
$$

using $$\mu(X) = \mathbf{1}$$ (property 2 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure)). By the definition of $$W_f$$ in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2), $$\eta \in W_f$$.$$\blacksquare$$


With **Proposition** *(hall-10.2)* established, we can now give the definition and existence/uniqueness statement for the integral of an unbounded function against a projection-valued measure — this is the result we will actually invoke when discussing $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ in [Theorem 10.4](#thrm:hall-10.4).

> **Proposition**
<a name="prpstn:hall-10.1"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
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
>
> The uniqueness holds in the following stronger form, which is what we will actually cite: if $$A$$ is *any* unbounded operator on $$\mathbf{H}$$ with domain $$W_f$$ satisfying merely the *diagonal* identity
>
> $$
>     \left< \psi, A\psi \right> = \int_X f \, d\mu_\psi \qquad \text{for all } \psi \in W_f,
> $$
>
> then $$A = \int_X f \, d\mu$$.

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

For the strengthened uniqueness clause: let $$A$$ be any unbounded operator on $$\mathbf{H}$$ with domain $$W_f$$ satisfying $$\left< \psi, A\psi \right> = \int_X f \, d\mu_\psi$$ for all $$\psi \in W_f$$, and write $$A_0 \equiv \int_X f \, d\mu$$ for the operator just constructed, which satisfies the same identity (the diagonal identity established above). So $$A$$ and $$A_0$$ induce the same function $$R : W_f \to \mathbb{C}$$, $$R(\psi) \equiv \left< \psi, A\psi \right> = \left< \psi, A_0\psi \right> = \int_X f\,d\mu_\psi$$. Note $$R = Q_f$$, which is a quadratic form on $$W_f$$ by Part 1 of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2) — this is needed because Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) requires its input to be a quadratic form. Applying that Part 1 once with $$T = A$$ and once with $$T = A_0$$ (both are linear maps $$W_f \to \mathbf{H}$$ inducing $$R$$), the sesquilinear form $$L_R$$ associated to $$R$$ satisfies both $$L_R(\phi,\psi) = \left< \phi, A\psi \right>$$ and $$L_R(\phi,\psi) = \left< \phi, A_0\psi \right>$$ for all $$\phi,\psi \in W_f$$ — the same $$L_R$$ in both cases, since it is defined purely in terms of $$R$$, which is common to both. Hence $$\left< \phi, A\psi \right> = \left< \phi, A_0\psi \right>$$ for all $$\phi, \psi \in W_f$$. Fixing $$\psi$$, this says $$A\psi$$ and $$A_0\psi$$ agree in inner product against every $$\phi$$ in the dense subset $$W_f$$, so $$A\psi = A_0\psi$$ by [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot). As $$\psi \in W_f$$ was arbitrary and the domains agree, $$A = A_0$$.$$\blacksquare$$

The next proposition records a natural compatibility check, confirming that [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) is a genuine extension of the previous post's construction rather than merely an analogue of it: for bounded $$f$$, the two constructions agree.

> **Proposition** *(Coincidence with the Bounded Integral)*
<a name="prpstn:coincidence-with-the-bounded-integral"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
> If $$f$$ is bounded, then $$W_f = \mathbf{H}$$, and the operator $$\int_X f \, d\mu$$ of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) coincides with the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration) $$\int_X f \, d\mu \in \mathcal{B}(\mathbf{H})$$ of the previous post.

**Proof**
If $$f$$ is bounded, $$\mu_\psi$$ is a finite measure for every $$\psi$$ (as always), so $$\int_X \lvert f \rvert^2 \, d\mu_\psi < \infty$$ automatically and $$W_f = \mathbf{H}$$. Let $$A_2$$ denote the [bounded integral](../spectral-theorems/#thrm:operator-valued-integration) of the previous post, an element of $$\mathcal{B}(\mathbf{H})$$, so in particular an unbounded operator on $$\mathbf{H}$$ with domain $$\mathbf{H} = W_f$$. Its defining property is exactly $$\left< \psi, A_2\psi \right> = \int_X f \, d\mu_\psi$$ for all $$\psi \in \mathbf{H}$$ — that is, $$A_2$$ satisfies the diagonal identity of the strengthened uniqueness clause of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1). That clause therefore gives $$A_2 = \int_X f \, d\mu$$ directly, which is the claim.$$\blacksquare$$

The integral is insensitive to changing the integrand on a set the projection-valued measure annihilates; we record this, as the Cayley transform below produces exactly such a situation (the function $$D$$ is undefined at one point, which carries no mass).

> **Lemma** *(The Integral Ignores Null Sets)*
<a name="lmm:integral-ignores-null-sets"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$ and let $$f, g : X \to \mathbb{C}$$ be measurable functions agreeing off a set $$N \in \Omega(X)$$ with $$\mu(N) = 0$$. Then $$W_f = W_g$$ and $$\int_X f \, d\mu = \int_X g \, d\mu$$ (as operators, with equal domains).

**Proof**
Since $$\mu(N) = 0$$, $$\mu_\psi(N) = \left< \psi, \mu(N)\psi \right> = 0$$ for every $$\psi \in \mathbf{H}$$; that is, $$N$$ is $$\mu_\psi$$-null for every $$\psi$$. Two measurable functions agreeing off a $$\nu$$-null set have the same $$\nu$$-integral whenever either is defined, and the same is true of their moduli squared. Hence, for every $$\psi$$,

$$
    \int_X \lvert f \rvert^2 \, d\mu_\psi = \int_X \lvert g \rvert^2 \, d\mu_\psi,
$$

so the defining condition of $$W_f$$ and of $$W_g$$ in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2) select the same set of $$\psi$$: $$W_f = W_g$$. Likewise $$\int_X f \, d\mu_\psi = \int_X g \, d\mu_\psi$$ for $$\psi$$ in this common domain, i.e. the two operators $$\int_X f \, d\mu$$ and $$\int_X g \, d\mu$$ have the same domain and satisfy the same diagonal identity. By the strengthened uniqueness clause of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1), they are equal.$$\blacksquare$$

Two further facts about the unbounded integral will be needed when we come to the Cayley transform. The first says that the operator may be computed as a norm limit of its bounded truncations; the second computes the associated measure of a vector in the image of the bounded calculus.

> **Lemma** *(Truncations Converge to the Unbounded Integral)*
<a name="lmm:truncations-converge"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{thrm:dominated-convergence-theorem} -->
<!--  \uses{lmm:l2-implies-l1} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{thrm:monotone-convergence-theorem-for-integrals} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{lmm:norm-identity-bounded-integral} -->
<!--  \uses{lmm:associated-measure-total-mass} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
<!--  \uses{prpstn:convergence-facts} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$, let $$f : X \to \mathbb{C}$$ be measurable, and let $$\psi \in W_f$$. Put $$E_n \equiv \{ x \in X \mid \lvert f(x) \rvert < n \}$$ and $$f_n \equiv f\cdot 1_{E_n}$$, a bounded measurable function. Then
>
> $$
>     \left( \int_X f_n \, d\mu \right)\psi \longrightarrow \left( \int_X f \, d\mu \right)\psi
> $$
>
> in the norm of $$\mathbf{H}$$ as $$n \to \infty$$.

**Proof**
Write $$\chi_n \equiv \left( \int_X f_n \, d\mu \right)\psi$$ — defined since $$f_n$$ is bounded — and $$\chi \equiv \left( \int_X f \, d\mu \right)\psi$$, defined since $$\psi \in W_f$$.

For $$n < m$$ we have $$E_n \subset E_m$$ and hence $$f_n - f_m = -f\cdot 1_{E_m \setminus E_n}$$, so, applying [**Lemma** *(Norm Identity for the Bounded Integral)*](#lmm:norm-identity-bounded-integral) to the bounded function $$f_n - f_m$$ and using linearity of the bounded integral,

$$
    \left\| \chi_n - \chi_m \right\|^2 = \int_X \lvert f_n - f_m \rvert^2 \, d\mu_\psi = \int_{E_m\setminus E_n} \lvert f \rvert^2 \, d\mu_\psi = \int_X \lvert f_m \rvert^2 \, d\mu_\psi - \int_X \lvert f_n \rvert^2 \, d\mu_\psi.
$$

Since $$\lvert f_n \rvert^2 = \lvert f \rvert^2 1_{E_n}$$ increases pointwise to $$\lvert f \rvert^2$$, the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals) gives $$\int_X \lvert f_n \rvert^2 \, d\mu_\psi \to \int_X \lvert f \rvert^2\,d\mu_\psi$$, a finite limit because $$\psi \in W_f$$; a convergent sequence of reals is Cauchy, so the right-hand side above tends to $$0$$ as $$n,m\to\infty$$, and $$\{\chi_n\}$$ is Cauchy in $$\mathbf{H}$$. By completeness, $$\chi_n \to \chi'$$ for some $$\chi' \in \mathbf{H}$$.

It remains to identify $$\chi' = \chi$$. Let $$\phi \in W_f$$. Since $$f_n$$ is bounded, $$W_{f_n} = \mathbf{H}$$ and $$Q_{f_n}$$ is a quadratic form on $$\mathbf{H}$$ by Part 1 of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2), induced on the diagonal by the bounded operator $$\int_X f_n\,d\mu$$; so Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties), applied with $$D = \mathbf{H}$$ and $$T = \int_X f_n\,d\mu$$, gives $$\left< \phi, \chi_n \right> = L_{f_n}(\phi,\psi)$$.

We check $$L_{f_n}(\phi,\psi) \to L_f(\phi,\psi)$$ directly. For any $$\xi \in W_f$$, the functions $$f_n$$ converge pointwise to $$f$$ and satisfy $$\lvert f_n \rvert \le \lvert f \rvert$$ with $$f$$ integrable against $$\mu_\xi$$ (by [**Lemma** *($$L^2$$ Implies $$L^1$$ on a Finite Measure Space)*](#lmm:l2-implies-l1), since $$\xi \in W_f$$ and $$\mu_\xi$$ is finite), so the [**Dominated Convergence Theorem**](#thrm:dominated-convergence-theorem) gives $$Q_{f_n}(\xi) = \int_X f_n\,d\mu_\xi \to \int_X f\,d\mu_\xi = Q_f(\xi)$$. By property 2 of the [definition of a quadratic form on a subspace](#def:hall-quadratic-form-on-a-subspace), $$L_{f_n}(\phi,\psi)$$ is a fixed finite linear combination — the same for every $$n$$ — of the five values $$Q_{f_n}$$ takes at $$\phi+\psi$$, $$\phi$$, $$\psi$$, $$\phi+i\psi$$, $$i\psi$$, all of which lie in the subspace $$W_f$$; each converges to the corresponding value for $$f$$, so $$L_{f_n}(\phi,\psi) \to L_f(\phi,\psi)$$.

Combining these with the defining property of $$\chi$$ in [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1),

$$
    \left< \phi, \chi' \right> = \lim_{n\to\infty}\left< \phi, \chi_n \right> = \lim_{n\to\infty} L_{f_n}(\phi,\psi) = L_f(\phi,\psi) = \left< \phi, \chi \right>,
$$

the first equality by [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product). As $$W_f$$ is dense in $$\mathbf{H}$$ (Part 1 of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2)), [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) gives $$\chi' = \chi$$.$$\blacksquare$$

> **Lemma** *(The Associated Measure of a Bounded-Calculus Image)*
<a name="lmm:associated-measure-of-image"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{thrm:monotone-convergence-theorem-for-integrals} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$, let $$h$$ be a bounded measurable function on $$X$$, and set $$T \equiv \int_X h \, d\mu \in \mathcal{B}(\mathbf{H})$$. Then for every $$\psi \in \mathbf{H}$$ and every $$E \in \Omega(X)$$,
>
> $$
>     \mu_{T\psi}(E) = \int_E \lvert h \rvert^2 \, d\mu_\psi;
> $$
>
> that is, $$d\mu_{T\psi} = \lvert h \rvert^2 \, d\mu_\psi$$. Consequently, for every nonnegative measurable $$g$$ on $$X$$,
>
> $$
>     \int_X g \, d\mu_{T\psi} = \int_X g\,\lvert h \rvert^2 \, d\mu_\psi.
> $$

**Proof**
Let $$E \in \Omega(X)$$. Using the [definition of the adjoint](#def:hall-9.1), then properties 3 and 4 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) — multiplicativity, and the fact that integration intertwines complex conjugation with the adjoint —

$$
\begin{align}
    \mu_{T\psi}(E) &= \left< T\psi, \mu(E)T\psi \right> \\
                   &= \left< \psi, T^*\mu(E)T\psi \right> \\
                   &= \left< \psi, \left( \int_X \overline{h}\,d\mu \right)\left( \int_X 1_E \, d\mu \right)\left( \int_X h \, d\mu \right)\psi \right> \\
                   &= \left< \psi, \left( \int_X \overline{h}\,1_E\,h \, d\mu \right)\psi \right> \\
                   &= \int_X 1_E \lvert h \rvert^2 \, d\mu_\psi \\
                   &= \int_E \lvert h \rvert^2 \, d\mu_\psi,
\end{align}
$$

the second-to-last equality by the defining property of the bounded integral. This is the stated identity of measures. The final claim is then the standard fact that integration against a measure with a density reduces to integration against the underlying measure weighted by that density — immediate for indicator functions by the identity just proved, hence for simple functions by linearity, hence for nonnegative measurable $$g$$ by the [**Monotone Convergence Theorem**](#thrm:monotone-convergence-theorem-for-integrals) applied to an increasing sequence of simple functions converging pointwise to $$g$$.$$\blacksquare$$

We now extract, as a standalone lemma, the fact that $$A_f$$ preserves the spectral subspace attached to any set on which $$f$$ is bounded. It is needed both here and, for a different projection-valued measure and a different family of sets, in the proof of [**Proposition** *(hall-10.29)*](#prpstn:hall-10.29) far below; stating it once, for a general such set, avoids re-deriving it there.

> **Lemma** *(The Integral Preserves Spectral Subspaces on which the Integrand is Bounded)*
<a name="lmm:integral-preserves-spectral-subspaces"></a>
<!--  \uses{conv:section-integration} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{lmm:bounded-on-set-range-in-domain} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{lmm:norm-convergent-decomposition} -->
<!--  \uses{prpstn:hall-a.49} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{lmm:associated-measure-total-mass} -->
<!--  \uses{prpstn:additivity-of-the-integral-in-the-measure} -->
> Let $$\mu$$ be a projection-valued measure on $$(X,\Omega(X))$$, let $$f : X \to \mathbb{C}$$ be measurable, and let $$E \in \Omega(X)$$ be a set on which $$f$$ is bounded. Write $$A_f \equiv \int_X f\,d\mu$$ and $$V_E \equiv \text{Range}(\mu(E))$$. Then $$V_E \subset W_f$$ and $$A_f(V_E) \subset V_E$$.

**Proof**
That $$V_E \subset W_f$$ is [**Lemma** *(Bounded on a Set Implies the Range Lies in the Domain)*](#lmm:bounded-on-set-range-in-domain).

*Step 1: $$\mu(S)$$ preserves $$V_E$$ for every $$S \in \Omega(X)$$.* Let $$\xi \in V_E$$ and $$S \in \Omega(X)$$. By [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel), $$\mu(E)\xi = \xi$$. Applying property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) twice,

$$
    \mu(E)\big[ \mu(S)\xi \big] = \mu(E)\mu(S)\xi = \mu(E \cap S)\xi
    \qquad\text{and}\qquad
    \mu(S)\xi = \mu(S)\mu(E)\xi = \mu(S \cap E)\xi,
$$

the second line using $$\mu(E)\xi = \xi$$. Since $$E \cap S = S \cap E$$, the two right-hand sides agree, so $$\mu(E)\big[\mu(S)\xi\big] = \mu(S)\xi$$; by the same lemma, $$\mu(S)\xi \in \text{Range}(\mu(E)) = V_E$$.

*Step 2: $$\left< \phi, A_f\psi \right> = 0$$ for $$\psi \in V_E$$ and $$\phi \in V_E^\perp \cap W_f$$.* Fix such $$\psi$$ and $$\phi$$, and let $$S \in \Omega(X)$$ be arbitrary. By **Step 1**, $$\mu(S)\psi \in V_E$$, so $$\left< \phi, \mu(S)\psi \right> = 0$$ since $$\phi \in V_E^\perp$$; and, since $$\mu(S)$$ is self-adjoint, $$\left< \psi, \mu(S)\phi \right> = \overline{\left< \mu(S)\phi, \psi \right>} = \overline{\left< \phi, \mu(S)\psi \right>} = 0$$ as well. Hence

$$
    \mu_{\phi+\psi}(S) = \left< \phi + \psi, \mu(S)(\phi+\psi) \right> = \mu_\phi(S) + \mu_\psi(S) + \left< \phi, \mu(S)\psi \right> + \left< \psi, \mu(S)\phi \right> = \mu_\phi(S) + \mu_\psi(S)
$$

for every $$S \in \Omega(X)$$, i.e. $$\mu_{\phi+\psi} = \mu_\phi + \mu_\psi$$ as measures. Hence, by [**Proposition** *(Additivity of the Integral in the Measure)*](#prpstn:additivity-of-the-integral-in-the-measure) — applicable since $$f$$ is integrable against each of $$\mu_\phi$$ and $$\mu_\psi$$, both $$\phi$$ and $$\psi$$ lying in $$W_f$$ —

$$
    Q_f(\phi+\psi) = \int_X f \, d\mu_{\phi+\psi} = \int_X f \, d\mu_\phi + \int_X f \, d\mu_\psi = Q_f(\phi) + Q_f(\psi).
$$
 Since $$\phi \in W_f$$ and $$\psi \in V_E \subset W_f$$, all of $$\phi, \psi, \phi+\psi, \phi+i\psi, i\psi$$ lie in $$W_f$$ (a subspace); and the identical argument with $$i\psi$$ in place of $$\psi$$ (still in $$V_E$$, a subspace) gives $$Q_f(\phi+i\psi) = Q_f(\phi) + Q_f(i\psi)$$. By the polarization formula defining $$L_f$$ from $$Q_f$$, both brackets $$Q_f(\phi+\psi) - Q_f(\phi) - Q_f(\psi)$$ and $$Q_f(\phi+i\psi) - Q_f(\phi) - Q_f(i\psi)$$ vanish, so $$L_f(\phi,\psi) = 0$$. By the off-diagonal identity of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1), $$\left< \phi, A_f\psi \right> = L_f(\phi,\psi) = 0$$.

*Step 3: extension to all of $$V_E^\perp$$ by density.* Let $$\phi \in V_E^\perp$$ be arbitrary and set $$E_m \equiv \{ x \in X \mid \lvert f(x) \rvert < m \}$$ for $$m \in \mathbb{N}$$. Since $$\lvert f \rvert < m$$ on $$E_m$$, [**Lemma** *(Bounded on a Set Implies the Range Lies in the Domain)*](#lmm:bounded-on-set-range-in-domain) gives $$\text{Range}(\mu(E_m)) \subset W_f$$, so $$\mu(E_m)\phi \in W_f$$. Putting $$G_1 \equiv E_1$$ and $$G_m \equiv E_m \setminus E_{m-1}$$ for $$m \ge 2$$, the $$G_m$$ are pairwise disjoint with $$\bigcup_{j=1}^m G_j = E_m$$ (induction, using $$E_{m-1} \subset E_m$$) and $$\bigcup_m G_m = \bigcup_m E_m = X$$ ($$f$$ being finite-valued); so Part 2 of [**Lemma** *(Norm-Convergent Decomposition over a Disjoint Cover)*](#lmm:norm-convergent-decomposition) gives $$\mu(E_m)\phi \to \phi$$ as $$m \to \infty$$.

Moreover $$\mu(E_m)\phi \in V_E^\perp$$: for any $$\eta \in V_E$$, **Step 1** gives $$\mu(E_m)\eta \in V_E$$, so, using self-adjointness of $$\mu(E_m)$$ — part of its being a bounded orthogonal projection, property 1 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) — $$\left< \eta, \mu(E_m)\phi \right> = \left< \mu(E_m)\eta, \phi \right> = 0$$, the last equality because $$\mu(E_m)\eta \in V_E$$ and $$\phi \in V_E^\perp$$. As $$\eta \in V_E$$ was arbitrary, $$\mu(E_m)\phi \in V_E^\perp$$.

So $$\mu(E_m)\phi \in V_E^\perp \cap W_f$$ for every $$m$$, with $$\mu(E_m)\phi \to \phi$$. Fix $$\psi \in V_E$$. By **Step 2**, $$\left< \mu(E_m)\phi, A_f\psi \right> = 0$$ for every $$m$$, so by [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), $$\left< \phi, A_f\psi \right> = \lim_m \left< \mu(E_m)\phi, A_f\psi \right> = 0$$.

*Conclusion.* For $$\psi \in V_E$$, $$A_f\psi$$ is orthogonal to every $$\phi \in V_E^\perp$$, i.e. $$A_f\psi \in \left( V_E^\perp \right)^\perp$$. Since $$V_E$$ is a closed subspace ([**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel)), Part 2 of [**Proposition** *(Orthogonal Decomposition and the Double Complement)*](#prpstn:hall-a.49) gives $$\left( V_E^\perp \right)^\perp = V_E$$, so $$A_f\psi \in V_E$$.$$\blacksquare$$

We close this section with the fact we will actually need about $$\int_X f \, d\mu$$: when $$f$$ is real-valued, the resulting operator is self-adjoint. This is exactly what will let us conclude, in the proof of [Theorem 10.4](#thrm:hall-10.4), that the operator $$\int_{\sigma(A)} \lambda \, d\mu_A(\lambda)$$ we construct is self-adjoint (as it must be, to have any chance of equalling the self-adjoint operator $$A$$). The proof uses [Proposition (Orthogonal Decomposition and the Double Complement)](#prpstn:hall-a.49) from earlier.

> **Proposition**
<a name="prpstn:hall-10.3"></a>
<!--  \uses{conv:section-integration} -->
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
<!--  \uses{lmm:restriction-of-quadratic-form} -->
<!--  \uses{lmm:closed-subspace-is-hilbert} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{lmm:associated-measure-total-mass} -->
<!--  \uses{lmm:integral-preserves-spectral-subspaces} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{prpstn:hall-9.26} -->
> If $$f$$ is a real-valued, measurable function on $$X$$, then $$\int_X f \, d\mu$$ is self-adjoint on $$W_f$$.

**Proof**
Write $$A_f \equiv \int_X f \, d\mu$$. For each integer $$n \ge 1$$, let $$F_n \equiv \{ x \in X \mid n - 1 \le \lvert f(x) \rvert < n \}$$, so the $$F_n$$ are pairwise disjoint with $$\bigcup_n F_n = X$$, and let $$\mathbf{H}_n \equiv \text{Range}(\mu(F_n))$$, a closed subspace of $$\mathbf{H}$$ by [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel), and hence itself a separable, complex Hilbert space with the inner product inherited from $$\mathbf{H}$$ (possibly $$\mathbf{H}_n = \{0\}$$, if $$F_n$$ happens to be a $$\mu$$-null set; this degenerate case is harmless: [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) is stated without excluding zero summands, and its proof discharges that case separately, since the route it otherwise takes passes through a result asserting non-emptiness of the spectrum). By [Lemma (Range Membership Concentrates the Associated Measure)](#lmm:range-membership-concentrates-measure), for any $$\eta \in \mathbf{H}_n$$, using $$\lvert f \rvert < n$$ on $$F_n$$,

$$
    \int_X \lvert f \rvert^2 \, d\mu_\eta = \int_{F_n} \lvert f \rvert^2 \, d\mu_\eta \le n^2 \mu_\eta(F_n) \le n^2 \mu_\eta(X) = n^2 \left\| \eta \right\|^2 < \infty.
$$

In particular $$\eta \in W_f$$, so, by the norm formula of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1), this reads $$\left\| A_f \eta \right\|^2 \le n^2 \left\| \eta \right\|^2$$, i.e. $$\left\| A_f \eta \right\| \le n \left\| \eta \right\|$$, for every $$\eta \in \mathbf{H}_n$$ — a bound on the size of $$A_f \eta$$ in $$\mathbf{H}$$, valid regardless of which subspace $$A_f \eta$$ actually lands in. By [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) and the defining property of $$A_f$$, $$\lvert Q_f(\eta) \rvert = \lvert \left< \eta, A_f\eta \right> \rvert \le \left\| \eta \right\| \left\| A_f \eta \right\| \le n \left\| \eta \right\|^2$$, so $$Q_f$$, restricted to $$\mathbf{H}_n$$, is also a bounded quadratic form (bound $$n$$).

By [**Lemma** *(The Integral Preserves Spectral Subspaces on which the Integrand is Bounded)*](#lmm:integral-preserves-spectral-subspaces), applied with $$E = F_n$$ (on which $$f$$ is bounded by $$n$$), $$A_f$$ maps $$\mathbf{H}_n$$ into $$\mathbf{H}_n$$.

So $$A_f$$ maps $$\mathbf{H}_n$$ into itself; let $$A_n$$ denote this restriction. Combined with the bound $$\left\| A_f \eta \right\| \le n \left\| \eta \right\|$$ established above (for $$\eta \in \mathbf{H}_n$$, where $$A_f\eta = A_n\eta \in \mathbf{H}_n$$), $$A_n$$ is a genuine bounded operator on $$\mathbf{H}_n$$, with operator norm at most $$n$$, and satisfies $$\left< \psi, A_n\psi \right> = \left< \psi, A_f\psi \right> = Q_f(\psi)$$ for all $$\psi \in \mathbf{H}_n$$. Since $$Q_f$$ is a quadratic form on $$W_f$$ (Part 1 of [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2)) and $$\mathbf{H}_n \subset W_f$$ is a subspace, [**Lemma** *(Restriction of a Quadratic Form to a Subspace)*](#lmm:restriction-of-quadratic-form) shows $$Q_f\vert_{\mathbf{H}_n}$$ is a quadratic form on $$\mathbf{H}_n$$; it is bounded (by the bound $$n$$ established above) and real-valued (as $$f$$ is real-valued, so $$Q_f(\psi) = \int_X f \, d\mu_\psi \in \mathbb{R}$$, an integral of a real-valued function against a positive real measure), [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63), applied with $$\mathbf{H}_n$$ in place of $$\mathbf{H}$$, produces a *unique* bounded operator on $$\mathbf{H}_n$$ representing this quadratic form, and asserts that this unique operator is self-adjoint. As $$A_n$$ is itself a bounded operator on $$\mathbf{H}_n$$ representing $$Q_f$$, uniqueness forces $$A_n$$ to be that operator, so $$A_n$$ is self-adjoint on $$\mathbf{H}_n$$.

Now, $$\{ \mathbf{H}_n \}_{n=1}^\infty$$ is an *internal orthogonal decomposition* of $$\mathbf{H}$$ in the sense of [Definition (Internal Orthogonal Decomposition)](#def:internal-orthogonal-decomposition). We check its two conditions.

*Pairwise orthogonality.* The $$F_n$$ are pairwise disjoint, so for $$n \ne m$$, property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) gives $$\mu(F_n)\mu(F_m) = \mu(F_n \cap F_m) = \mu(\emptyset) = 0$$. Hence for $$\eta \in \mathbf{H}_n$$ and $$\zeta \in \mathbf{H}_m$$, using $$\mu(F_n)\eta = \eta$$ and $$\mu(F_m)\zeta = \zeta$$ (idempotency, as both lie in the respective ranges) and self-adjointness of $$\mu(F_n)$$,

$$
    \left< \eta, \zeta \right> = \left< \mu(F_n)\eta, \mu(F_m)\zeta \right> = \left< \eta, \mu(F_n)\mu(F_m)\zeta \right> = \left< \eta, 0 \right> = 0.
$$

*Decomposition.* By [Lemma (Norm-Convergent Decomposition over a Disjoint Cover)](#lmm:norm-convergent-decomposition) applied to $$\{F_n\}$$ (pairwise disjoint with union $$X$$), every $$\psi \in \mathbf{H}$$ satisfies $$\psi = \sum_{n=1}^\infty \mu(F_n)\psi$$, norm-convergent, with $$\mu(F_n)\psi \in \text{Range}(\mu(F_n)) = \mathbf{H}_n$$.

So $$\{\mathbf{H}_n\}$$ is an internal orthogonal decomposition of $$\mathbf{H}$$, each $$\mathbf{H}_n$$ being a separable closed subspace (shown at the start of this proof). Writing $$\psi_n \equiv \mu(F_n)\psi$$ for the components of $$\psi$$, Part 2 of [**Lemma** *(Internal Decompositions are Unitarily External Direct Sums)*](#lmm:internal-decomposition-unitary) gives $$\left\| \psi \right\|^2 = \sum_n \left\| \psi_n \right\|^2$$, and Part 1 gives uniqueness of this decomposition — so the components $$\psi_n$$ referred to below are unambiguous.

Identifying $$\mathbf{H}$$ with sequences $$\psi = (\psi_1, \psi_2, \ldots)$$, $$\psi_n \in \mathbf{H}_n$$: for $$\psi \in \bigoplus_{n=1}^N \mathbf{H}_n$$ a finite sum (so $$\psi = \sum_{n=1}^N \psi_n \in W_f$$, since $$W_f$$ is a subspace and $$\mathbf{H}_n \subset W_f$$ for each $$n$$, shown above), linearity of $$A_f$$ on $$W_f$$ together with $$A_f$$ mapping each $$\mathbf{H}_n$$ to itself via $$A_n$$ gives $$A_f\psi = \sum_{n=1}^N A_n\psi_n$$, matching the formula in [**Proposition** *(hall-9.26)*](#prpstn:hall-9.26) on the finite direct sum. It remains to identify $$W_f$$ itself with the domain $$V$$ of that proposition. Let $$\psi \in \mathbf{H}$$ be arbitrary (not assumed to lie in $$W_f$$ or to be a finite sum), and write $$\psi_n \equiv \mu(F_n)\psi \in \mathbf{H}_n$$ for its components. We claim $$\mu_\psi$$ and $$\mu_{\psi_n}$$ agree on every measurable $$E \subset F_n$$. Indeed, for such $$E$$, using self-adjointness of $$\mu(F_n)$$ to move one factor across the inner product, then property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) twice, and finally $$E \cap F_n = E$$ (as $$E \subset F_n$$),

$$
    \mu_{\psi_n}(E) = \left< \mu(F_n)\psi, \mu(E)\mu(F_n)\psi \right> = \left< \psi, \mu(F_n)\mu(E)\mu(F_n)\psi \right> = \left< \psi, \mu(F_n \cap E \cap F_n)\psi \right> = \left< \psi, \mu(E)\psi \right> = \mu_\psi(E).
$$

Hence

$$
    \int_X \lvert f \rvert^2 \, d\mu_\psi = \sum_n \int_{F_n} \lvert f \rvert^2 \, d\mu_\psi = \sum_n \int_{F_n} \lvert f \rvert^2 \, d\mu_{\psi_n} = \sum_n \int_X \lvert f \rvert^2 \, d\mu_{\psi_n} = \sum_n \left\| A_n \psi_n \right\|_n^2,
$$

where: the first equality is [**Proposition** *(Countable Additivity of the Integral over a Disjoint Cover)*](#prpstn:countable-additivity-of-the-integral), applied to the nonnegative measurable function $$\lvert f \rvert^2$$, the measure $$\mu_\psi$$, and the disjoint cover $$\{F_n\}$$; the second is [**Proposition** *(Integrals Agree when Measures Agree on a Set)*](#prpstn:integrals-agree-when-measures-agree), applied with $$E = F_n$$ and the two measures $$\mu_\psi, \mu_{\psi_n}$$, which agree on all measurable subsets of $$F_n$$ (just shown); the third uses $$\mu_{\psi_n}(F_n^c) = 0$$ — which is [**Lemma** *(Range Membership Concentrates the Associated Measure)*](#lmm:range-membership-concentrates-measure) applied to $$\psi_n = \mu(F_n)\psi \in \text{Range}(\mu(F_n))$$ — to extend the integral from $$F_n$$ back to $$X$$; and the last is the norm formula of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) applied in $$\mathbf{H}$$ to the vector $$\psi_n$$ (which lies in $$W_f$$, since $$\mathbf{H}_n \subset W_f$$), giving $$\int_X \lvert f \rvert^2 d\mu_{\psi_n} = \left\| A_f\psi_n \right\|^2$$, together with $$A_f\psi_n = A_n\psi_n$$ and the fact that the $$\mathbf{H}_n$$-norm is the restriction of the $$\mathbf{H}$$-norm, so $$\left\| A_f\psi_n \right\| = \left\| A_n\psi_n \right\|_n$$. This holds for *every* $$\psi \in \mathbf{H}$$, with both sides possibly infinite, so it identifies

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

The class is genuinely larger than the self-adjoint operators — for instance every unitary operator is normal, by [**Lemma** *(Unitary Operators are Normal)*](#lmm:unitary-is-normal) below, and unitary operators are generally not self-adjoint. That every self-adjoint operator is itself normal is used below to apply normality-requiring results to $$B^*B$$, so we record it rather than leave it as a remark.

> **Lemma** *(Bounded Self-Adjoint Operators are Normal)*
<a name="lmm:self-adjoint-is-normal"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-9.5} -->
> If $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint, then $$A$$ is normal.

**Proof**
Self-adjointness gives $$A^* = A$$, so $$AA^* = AA = A^2$$ and $$A^*A = AA = A^2$$; the two agree, which is the [definition of normal](#def:hall-10.19).$$\blacksquare$$
 Unlike the self-adjoint case, the spectrum of a normal operator need not lie on the real line at all.

Hall's proof that the bounded self-adjoint spectral theorem extends to normal operators proceeds in two stages, mirroring the two-stage proof of the self-adjoint case itself. The first stage builds a continuous functional calculus for $$A$$; the second turns that functional calculus into a projection-valued measure. Hall's own observation is that this second stage, once a continuous functional calculus is in hand, uses nothing about the operator beyond the functional calculus itself — not self-adjointness, not realness of the spectrum. Rather than treat this as license to say the self-adjoint case's construction "carries over unchanged" — citing one proof to justify another, exactly the pattern [**Lemma** *(The $$b^2$$ Inequality for Symmetric Operators)*](#lmm:b-squared-inequality-symmetric) and [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) were introduced earlier to avoid — when we reach that stage we will extract the construction as its own proposition, parameterized by an abstract continuous functional calculus on a compact metric space, so that the self-adjoint and normal cases each cite that one statement rather than one citing the other's proof. For now, our task is the first stage: building the continuous functional calculus for a normal operator.

For a self-adjoint operator, this calculus was built by approximating continuous *real-valued* functions on the (real) spectrum by real polynomials in $$\lambda$$, using the real Stone–Weierstrass theorem. For a normal operator, $$\sigma(A)$$ is a general compact subset of $$\mathbb{C}$$, and we need to approximate *complex-valued* functions; the complex-valued Stone–Weierstrass theorem requires an algebra of functions closed under complex conjugation, so plain polynomials in $$\lambda$$ no longer suffice — we need polynomials in $$\lambda$$ *and* $$\overline{\lambda}$$. On the operator side, the counterpart to conjugation is the adjoint, so a polynomial $$p(\lambda,\overline\lambda)$$ should correspond to the operator $$p(A,A^*)$$ obtained by substituting $$A$$ for $$\lambda$$ and $$A^*$$ for $$\overline\lambda$$. This substitution is where normality is essential: the polynomial ring $$\mathbb{C}[\lambda,\overline\lambda]$$ is commutative, so a given function $$p(\lambda,\overline\lambda)$$ has a unique representation as such a polynomial — but substituting $$\lambda \mapsto A$$, $$\overline\lambda \mapsto A^*$$ turns this into an expression in the generally *non*commutative algebra $$\mathcal{B}(\mathbf{H})$$, and the substitution is well defined as an algebra homomorphism only if it respects every relation that holds in the source ring — in particular $$\lambda\overline\lambda = \overline\lambda\lambda$$, which forces $$AA^* = A^*A$$. Without normality, there would be nothing to substitute *into*: no consistent way to assign a single operator to $$p(\lambda,\overline\lambda)$$ independent of how it is written.

The key technical result we are aiming for is a version of the spectral mapping theorem for this two-variable substitution: $$\sigma\big(p(A,A^*)\big) = \big\{ p(\lambda,\overline\lambda) \mid \lambda \in \sigma(A) \big\}$$. Unlike the ordinary (one-variable) spectral mapping theorem, this is genuinely harder to prove, and the route we follow — matching Hall's — uses the bounded self-adjoint spectral theorem itself, applied to an auxiliary self-adjoint operator, together with the notion of an *almost eigenvector*.

We start with a fact that will let us compute the norm of $$p(A,A^*)$$ once we know its spectrum: for normal operators, the operator norm equals the spectral radius, exactly as for self-adjoint operators. Proving this needs one general fact about spectral radii of commuting operators that is not yet available to us, and whose proof requires knowing that the powers of a bounded operator cannot grow faster than the spectral radius suggests.

We will also need the standard corollary of the Hahn–Banach theorem identifying the norm of an element of a normed space with the supremum of its image under unit-norm functionals; like the other classical facts imported here, we state it without proof.

> **Theorem** *(Norm via Dual Pairing)*
<a name="thrm:norm-via-dual-pairing"></a>
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
> If $$x$$ is an element of a normed vector space $$V$$, then
>
> $$
>     \|x\| = \sup \{ \lvert \xi(x) \rvert : \xi \in V^*,\ \|\xi\| \le 1 \}.
> $$

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
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
> Suppose $$\mathbf{H} \ne \{0\}$$, $$A \in \mathcal{B}(\mathbf{H})$$, and $$T \in \mathbb{R}$$ with $$T > R(A)$$. (The hypothesis $$\mathbf{H} \ne \{0\}$$ is what makes $$R(A)$$ well defined: by [**Definition** *(Spectral Radius)*](../spectral-theorems/#def:spectral-radius) it is a supremum over $$\sigma(A)$$, and $$\sigma(A)$$ is non-empty only because of Part 1 of [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5), which fails on the zero space.) Then
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

By the [**Nth-Term Test**](../spectral-theorems/#lmm:nth-term-test), convergence of $$\sum_m \xi(A^m)/\lambda_1^{m+1}$$ forces its terms to tend to $$0$$, so in particular $$\{ \xi(A^m/\lambda_1^{m+1}) \}_m$$ is a bounded subset of $$\mathbb{C}$$, with some bound $$C_\xi$$ depending on $$\xi$$ (and on $$\lambda_1$$). As $$\xi$$ ranges over all bounded linear functionals on $$\mathcal{B}(\mathbf{H})$$ — a Banach space, by [**Lemma** *(Bounded Operators form a Banach Space)*](../spectral-theorems/#lmm:bounded-operators-form-a-banach-space), and so, by the [**Theorem on Completeness of the Dual**](../spectral-theorems/#thrm:theorem-on-completeness-of-the-dual), its dual $$\mathcal{B}(\mathbf{H})^*$$ is itself a Banach space — the [**Principle of Uniform Boundedness**](../spectral-theorems/#thrm:hall-a.40), applied with $$V_1 = \mathcal{B}(\mathbf{H})^*$$, $$V_2 = \mathbb{C}$$, and the family of evaluation maps $$T_m : \xi \mapsto \xi(A^m/\lambda_1^{m+1})$$. Its hypotheses hold: each $$T_m$$ is linear in $$\xi$$, and bounded, since $$\lvert T_m\xi \rvert = \lvert \xi(A^m/\lambda_1^{m+1}) \rvert \le \left\| \xi \right\| \left\| A^m/\lambda_1^{m+1} \right\|$$ by the definition of the dual norm — so $$T_m$$ is a bounded linear map $$\mathcal{B}(\mathbf{H})^* \to \mathbb{C}$$ — and for each fixed $$\xi$$ the family $$\{ T_m\xi \}_m$$ is bounded by $$C_\xi$$, just shown. The principle therefore gives a constant $$C < \infty$$, independent of $$\xi$$, such that these evaluation maps have norm at most $$C$$ as elements of $$\mathcal{B}(\mathbf{H})^{**}$$: $$\lvert \xi(A^m/\lambda_1^{m+1}) \rvert \le C \left\| \xi \right\|$$ for every $$\xi \in \mathcal{B}(\mathbf{H})^*$$ and every $$m$$.

To convert this into a bound on $$\|A^m/\lambda_1^{m+1}\|$$ itself, we use [**Theorem** *(Norm via Dual Pairing)*](#thrm:norm-via-dual-pairing).

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
<!--  \uses{../spectral-theorems/#lmm:lemma-2} -->
<!--  \uses{prpstn:convergence-facts} -->
> Suppose $$\mathbf{H} \ne \{0\}$$ (so that the spectral radii below are well defined, as in [**Lemma** *(Power Growth is Controlled by the Spectral Radius)*](#lmm:power-growth-controlled-by-spectral-radius)). If $$A$$ and $$B$$ are commuting elements of $$\mathcal{B}(\mathbf{H})$$, then
>
> $$
>     R(AB) \le R(A)R(B).
> $$

**Proof**
We first show: for *every* pair of real numbers $$S > R(A)$$ and $$T > R(B)$$,

$$
    \lim_{m \to \infty} \frac{\|(AB)^m\|}{S^mT^m} = 0. \tag{$\P$}
$$

Since $$A$$ and $$B$$ commute, $$(AB)^m = A^mB^m$$ for every $$m$$ (by induction: trivial for $$m=0,1$$, and if $$(AB)^m = A^mB^m$$ then $$(AB)^{m+1} = (AB)^mAB = A^mB^mAB = A^m(B^mA)B = A^m(AB^m)B = A^{m+1}B^{m+1}$$, using $$B^mA = AB^m$$, itself immediate by induction on $$m$$ from $$AB=BA$$). By [submultiplicativity of the operator norm](../spectral-theorems/#lmm:lemma-2),

$$
    \frac{\|(AB)^m\|}{S^mT^m} = \frac{\|A^mB^m\|}{S^mT^m} \le \frac{\|A^m\|\|B^m\|}{S^mT^m} = \frac{\|A^m\|}{S^m}\cdot\frac{\|B^m\|}{T^m}.
$$

By [**Lemma** *(Power Growth is Controlled by the Spectral Radius)*](#lmm:power-growth-controlled-by-spectral-radius), applied to $$A$$ with $$T$$ there taken to be our $$S$$ (valid since $$S > R(A)$$), and to $$B$$ with $$T$$ there taken to be our $$T$$ (valid since $$T > R(B)$$), both factors on the right tend to $$0$$ as $$m \to \infty$$, giving $$(\P)$$.

Now fix real numbers $$S > R(A)$$ and $$T > R(B)$$ (for the remainder of the proof), and fix $$\lambda_1 \in \mathbb{C}$$ with $$\lvert \lambda_1 \rvert > ST$$, and $$\lambda_2$$ with $$\lvert \lambda_1 \rvert > \lvert \lambda_2 \rvert > ST$$. Applying $$(\P)$$ to the pair $$S' = S \cdot \lvert \lambda_2 \rvert/(ST)$$, $$T' = T$$ — so $$S'T' = \lvert \lambda_2 \rvert$$, and $$S' > R(A)$$ since $$\lvert \lambda_2 \rvert > ST$$ gives $$S' = S\lvert \lambda_2 \rvert/(ST) = \lvert \lambda_2 \rvert/T > S > R(A)$$, while $$T' = T > R(B)$$ trivially — the sequence $$\|(AB)^m\|/\lvert \lambda_2 \rvert^m$$ tends to $$0$$, so in particular is bounded: there is a constant $$C$$ with $$\|(AB)^m\| \le C\lvert \lambda_2 \rvert^m$$ for all $$m$$.

By [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5) applied to $$AB$$, for $$\lvert \lambda \rvert > \|AB\|$$,

$$
    (AB - \lambda\mathbf{1})^{-1} = -\sum_{m=0}^\infty \frac{(AB)^m}{\lambda^{m+1}}, \tag{$\P\P$}
$$

convergent in operator norm — but this alone only shows $$\lambda_1$$ is in the resolvent set of $$AB$$ when $$\lvert \lambda_1 \rvert > \|AB\|$$, which we do not know here ($$\lambda_1$$ was chosen only with $$\lvert \lambda_1 \rvert > ST \ge R(A)R(B)$$, and $$ST$$ may be far smaller than $$\|AB\|$$). Instead, we show directly that the series $$-\sum_m (AB)^m/\lambda_1^{m+1}$$, which converges in operator norm by the bound on $$\|(AB)^m\|$$ just derived — its terms have norm at most $$C\lvert \lambda_2 \rvert^m/\lvert \lambda_1 \rvert^{m+1}$$, and $$\sum_m C\lvert \lambda_2 \rvert^m/\lvert \lambda_1 \rvert^{m+1}$$ is a convergent geometric series since $$\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert<1$$, so Part 3 of [**Proposition** *(Convergence Facts for Sequences and Series)*](#prpstn:convergence-facts), applied in the Banach space $$\mathcal{B}(\mathbf{H})$$, gives convergence — defines a two-sided inverse of $$AB - \lambda_1\mathbf{1}$$.

Let $$S \equiv -\sum_{m=0}^\infty (AB)^m/\lambda_1^{m+1}$$ (the operator norm limit just established) and $$S_N \equiv -\sum_{m=0}^N (AB)^m/\lambda_1^{m+1}$$, so $$S_N \to S$$ as $$N \to \infty$$ by definition of the series' convergence. Expanding and re-indexing the first sum below with $$k=m+1$$,

$$
\begin{align}
    (AB-\lambda_1\mathbf{1})S_N &= (AB-\lambda_1\mathbf{1}) \left( -\sum_{m=0}^N \frac{(AB)^m}{\lambda_1^{m+1}} \right) \\
                                &= -\sum_{m=0}^N \frac{(AB)^{m+1}}{\lambda_1^{m+1}} + \sum_{m=0}^N \frac{(AB)^m}{\lambda_1^m} \\
                                &= -\sum_{k=1}^{N+1} \frac{(AB)^k}{\lambda_1^k} + \mathbf{1} + \sum_{m=1}^N \frac{(AB)^m}{\lambda_1^m} \\
                                &= \mathbf{1} - \frac{(AB)^{N+1}}{\lambda_1^{N+1}},
\end{align}
$$

the middle terms ($$k=m=1,\ldots,N$$) telescoping away. Since $$\|(AB)^{N+1}\|/\lvert \lambda_1 \rvert^{N+1} \le C\lvert \lambda_2 \rvert^{N+1}/\lvert \lambda_1 \rvert^{N+1} = C(\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert)^{N+1} \to 0$$ as $$N \to \infty$$ (using the same bound as above, with $$\lvert \lambda_2 \rvert/\lvert \lambda_1 \rvert<1$$), we get $$(AB-\lambda_1\mathbf{1})S_N \to \mathbf{1}$$. On the other hand, left multiplication by the fixed bounded operator $$AB - \lambda_1\mathbf{1}$$ is continuous in the operator norm (for any $$T_1,T_2 \in \mathcal{B}(\mathbf{H})$$, $$\|(AB-\lambda_1\mathbf{1})T_1 - (AB-\lambda_1\mathbf{1})T_2\| \le \|AB-\lambda_1\mathbf{1}\|\,\|T_1-T_2\|$$, by [submultiplicativity](../spectral-theorems/#lmm:lemma-2)), so $$(AB-\lambda_1\mathbf{1})S_N \to (AB-\lambda_1\mathbf{1})S$$ as well. By uniqueness of limits, $$(AB-\lambda_1\mathbf{1})S = \mathbf{1}$$. An identical computation — using that $$(AB)^m$$ commutes with $$AB-\lambda_1\mathbf{1}$$, being a power of $$AB$$ itself — gives $$S_N(AB-\lambda_1\mathbf{1}) = \mathbf{1} - (AB)^{N+1}/\lambda_1^{N+1} \to \mathbf{1}$$ and hence, by continuity of right multiplication by the fixed operator $$AB-\lambda_1\mathbf{1}$$, $$S(AB-\lambda_1\mathbf{1}) = \mathbf{1}$$. So $$S$$ is a two-sided inverse of $$AB - \lambda_1\mathbf{1}$$, and $$\lambda_1$$ is in the resolvent set of $$AB$$.

Since $$\lambda_1$$ with $$\lvert \lambda_1 \rvert > ST$$ was arbitrary, every such $$\lambda_1$$ is in the resolvent set of $$AB$$, so $$\sigma(AB) \subset \{ \lvert \lambda \rvert \le ST \}$$, giving $$R(AB) \le ST$$. As $$S > R(A)$$ and $$T > R(B)$$ were arbitrary, $$R(AB) \le R(A)R(B)$$.$$\blacksquare$$

We can now prove the equality of norm and spectral radius for normal operators, exactly as for self-adjoint operators. The proof needs two elementary properties of the adjoint of a bounded operator, neither yet available to us; we record them first.

> **Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*
<a name="lmm:adjoint-product-and-involution"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
<!--  \uses{def:hall-9.1} -->
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
<!--  \uses{lmm:power-growth-controlled-by-spectral-radius} -->
> Suppose $$\mathbf{H} \ne \{0\}$$ (so that $$R(A)$$ is well defined, as in [**Lemma** *(Power Growth is Controlled by the Spectral Radius)*](#lmm:power-growth-controlled-by-spectral-radius)). If $$A \in \mathcal{B}(\mathbf{H})$$ is normal, then $$\|A\| = R(A)$$.

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

Several results below need to know that $$\sigma(A)$$ is a compact metric space carrying a Borel $$\sigma$$-algebra. The previous post established this, but only for *self-adjoint* $$A$$ — and its statement there includes $$\sigma(A) \subset \mathbb{R}$$, which fails for a general normal operator. The topological content holds for any bounded operator, so we record the version we actually need.

> **Lemma** *(The Spectrum of a Bounded Operator is a Compact Metric Measurable Space)*
<a name="lmm:spectrum-compact-general"></a>
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
<!--  \uses{../spectral-theorems/#thrm:heine–borel-theorem} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ with $$\mathbf{H} \ne \{0\}$$. Then $$\sigma(A)$$ is a non-empty compact subset of $$\mathbb{C}$$; it is a metric space under the metric $$d(z_1,z_2) \equiv \lvert z_1 - z_2 \rvert$$ inherited from $$\mathbb{C}$$, and a measurable space when equipped with the Borel $$\sigma$$-algebra of that metric topology. No self-adjointness or normality is assumed, and $$\sigma(A)$$ need not be contained in $$\mathbb{R}$$.

**Proof**
By Part 1 of [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5), which is stated for every $$A \in \mathcal{B}(\mathbf{H})$$, the spectrum $$\sigma(A)$$ is a closed, bounded, non-empty subset of $$\mathbb{C}$$. By the [**Heine–Borel Theorem**](../spectral-theorems/#thrm:heine–borel-theorem), a closed and bounded subset of $$\mathbb{C}$$ is compact, so $$\sigma(A)$$ is compact.

Any subset of $$\mathbb{C}$$ is a metric space under the inherited metric $$d$$, the metric axioms being inherited; and any metric space is a measurable space under the Borel $$\sigma$$-algebra generated by its open sets. This gives the remaining claims.$$\blacksquare$$

### Spectral Subspaces

The route to the two-variable spectral mapping theorem passes through *spectral subspaces*: the ranges of the projections $$\mu^A(E)$$ supplied by the bounded self-adjoint spectral theorem. These were not needed in the previous post, so we develop what we need here.

> **Definition** *(Spectral Subspaces)*
<a name="def:hall-7.14"></a>
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{lmm:closed-subspace-is-hilbert} -->
> Let $$\mu$$ be a projection-valued measure on a $$\sigma$$-algebra $$\Omega(Y)$$ over a set $$Y$$. For each $$E \in \Omega(Y)$$, the *spectral subspace* $$V_E$$ of $$\mathbf{H}$$ (relative to $$\mu$$) is
>
> $$
>     V_E \equiv \text{Range}\big( \mu(E) \big).
> $$
>
> When $$A \in \mathcal{B}(\mathbf{H})$$ is self-adjoint we take $$\mu = \mu^A$$, the projection-valued measure of the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators), extended to $$\mathbb{R}$$ by $$\mu^A(\mathbb{R}\setminus\sigma(A)) = 0$$, and speak of the spectral subspaces *of $$A$$*; when $$A$$ is normal we take $$\mu = \mu^A$$ from [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20) instead. The general definition covers both, and is the one used below.
>
> Each $$V_E$$ is a closed subspace of $$\mathbf{H}$$: it is the range of a bounded orthogonal projection $$\mu(E)$$ (property 1 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure)), and [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel) shows such a range is closed. Being a closed subspace of $$\mathbf{H}$$, $$V_E$$ is itself a separable Hilbert space under the inherited inner product, by [**Lemma** *(A Closed Subspace is a Separable Hilbert Space)*](#lmm:closed-subspace-is-hilbert): completeness because a closed subset of a complete space is complete, and separability because a subspace of a separable metric space is separable.

We need three properties of these subspaces. The first two follow directly from multiplicativity of the functional calculus; the third says the subspaces attached to neighbourhoods of spectral points are non-trivial.

> **Proposition** *(Properties of Spectral Subspaces)*
<a name="prpstn:hall-7.15"></a>
<!--  \uses{def:hall-7.14} -->
<!--  \uses{lmm:integral-ignores-null-sets} -->
<!--  \uses{prpstn:coincidence-with-the-bounded-integral} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{lmm:uniqueness-of-resolvent} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:spectrum-notions-agree} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$X \subset \mathbb{C}$$ be compact, let $$\mu$$ be a projection-valued measure on the Borel $$\sigma$$-algebra of $$X$$, and set $$A \equiv \int_X \iota \, d\mu$$ — a bounded operator, since $$\iota(\lambda) = \lambda$$ is bounded on the compact set $$X$$. Let $$V_E \equiv \text{Range}(\mu(E))$$ be the associated [spectral subspaces](#def:hall-7.14). Then:
>
> 1. Each $$V_E$$ is invariant under $$A$$: $$A(V_E) \subset V_E$$.
> 2. If $$E \subset \{ \lambda \in X \mid \lvert \lambda - \lambda_0 \rvert \le \varepsilon \}$$ for some $$\lambda_0 \in \mathbb{C}$$ and $$\varepsilon > 0$$, then $$\left\| (A - \lambda_0\mathbf{1})\psi \right\| \le \varepsilon \left\| \psi \right\|$$ for all $$\psi \in V_E$$.
> 3. If $$\lambda_0 \in \sigma(A)$$, then $$V_{U \cap X} \ne \{0\}$$ for every open $$U \subset \mathbb{C}$$ containing $$\lambda_0$$.
>
> Note that the statement is about an arbitrary projection-valued measure on a compact $$X \subset \mathbb{C}$$ and the operator $$A$$ it integrates to; it presupposes no spectral theorem, and its proof below uses none. It will be applied in two ways: with $$\mu = \mu^A$$ for a bounded *self-adjoint* $$A$$ (where $$X = \sigma(A) \subset \mathbb{R}$$, so the sets in Part 2 are real intervals), which is available now; and, later and only after that theorem has been proved by a route passing through this proposition, with $$\mu = \mu^U$$ for a bounded *normal* $$U$$. There is no circularity: the present proposition is logically prior to both.

**Proof**
Throughout we use multiplicativity of the bounded integral, property 3 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration), and write $$f(A) \equiv \int_X f\,d\mu$$ for bounded measurable $$f$$; note $$\iota(A) = A$$ by the definition of $$A$$, $$1(A) = \mathbf{1}$$ and $$1_E(A) = \mu(E)$$ by property 1 of the same theorem.

**Part 1.** Since $$\iota \cdot 1_E = 1_E \cdot \iota$$ as functions, multiplicativity gives $$A\,\mu(E) = (\iota 1_E)(A) = (1_E \iota)(A) = \mu(E)\,A$$. Hence for $$\psi = \mu(E)\phi \in V_E$$,

$$
    A\psi = A\mu(E)\phi = \mu(E)(A\phi) \in \text{Range}\big(\mu(E)\big) = V_E.
$$

**Part 2.** Let $$\psi \in V_E$$, so $$\mu(E)\psi = \psi$$ by [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel). With $$f \equiv \iota - \lambda_0$$, so that $$f(A) = A - \lambda_0\mathbf{1}$$ by linearity of the integral together with $$1(A) = \mathbf{1}$$, multiplicativity gives

$$
    (A - \lambda_0\mathbf{1})\psi = f(A)\,\mu(E)\psi = (f 1_E)(A)\psi.
$$

Since $$E \subset \{ \lvert \lambda - \lambda_0 \rvert \le \varepsilon \}$$, the function $$f 1_E$$ satisfies $$\lvert f(\lambda)1_E(\lambda) \rvert \le \varepsilon$$ for every $$\lambda \in X$$. By the norm bound, property 2 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration), $$\left\| (f1_E)(A) \right\| \le \varepsilon$$, so $$\left\| (A-\lambda_0\mathbf{1})\psi \right\| \le \varepsilon\left\| \psi \right\|$$.

**Part 3.** Suppose, for contradiction, that $$\lambda_0 \in \sigma(A)$$ but $$V_{U \cap X} = \{0\}$$ for some open $$U \subset \mathbb{C}$$ containing $$\lambda_0$$. Since $$U$$ is open, there is $$\varepsilon > 0$$ with $$\{ \lvert \lambda - \lambda_0 \rvert < \varepsilon \} \subset U$$; set $$N \equiv \{ \lambda \in X \mid \lvert \lambda - \lambda_0 \rvert < \varepsilon \}$$, so $$N \subset U \cap X$$. Then $$V_N \subset V_{U\cap X} = \{0\}$$: for $$E \subset F$$ measurable, property 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) gives $$\mu(F)\mu(E) = \mu(E \cap F) = \mu(E)$$, so every $$\eta = \mu(E)\xi$$ satisfies $$\mu(F)\eta = \eta$$ and hence lies in $$\text{Range}(\mu(F))$$ by [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel). So $$V_N = \{0\}$$, i.e. $$\mu(N) = 0$$ (a projection with trivial range is the zero operator).

Define the bounded measurable function

$$
    g(\lambda) \equiv \begin{cases} \dfrac{1}{\lambda-\lambda_0} & \lambda \in X \setminus N \\[4pt] 0 & \lambda \in N \end{cases}
$$

— bounded by $$1/\varepsilon$$, since $$\lvert \lambda - \lambda_0 \rvert \ge \varepsilon$$ off $$N$$. The function $$\lambda \mapsto g(\lambda)(\lambda-\lambda_0)$$ equals $$1$$ on $$X \setminus N$$ and $$0$$ on $$N$$, so it agrees with the constant function $$1$$ off $$N$$, and $$\mu(N) = 0$$; hence [**Lemma** *(The Integral Ignores Null Sets)*](#lmm:integral-ignores-null-sets) — transferred to the bounded integral by [**Proposition** *(Coincidence with the Bounded Integral)*](#prpstn:coincidence-with-the-bounded-integral) — gives $$\big( g\cdot(\iota-\lambda_0) \big)(A) = 1(A) = \mathbf{1}$$. By multiplicativity,

$$
    g(A)(A - \lambda_0\mathbf{1}) = (A-\lambda_0\mathbf{1})g(A) = \mathbf{1},
$$

exhibiting the bounded operator $$g(A)$$ as a two-sided inverse of $$A - \lambda_0\mathbf{1}$$. By the [definition of the resolvent set](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum), $$\lambda_0$$ therefore lies in the resolvent set of the bounded operator $$A$$ — equivalently, by [**Lemma** *(The Two Notions of Spectrum Agree for Bounded Operators)*](#lmm:spectrum-notions-agree), in its resolvent set in the unbounded sense, so that [**Lemma** *(Uniqueness of the Resolvent)*](#lmm:uniqueness-of-resolvent) identifies $$g(A)$$ as *the* inverse $$(A-\lambda_0\mathbf{1})^{-1}$$. Either way, $$\lambda_0$$ is in the resolvent set, contradicting $$\lambda_0 \in \sigma(A)$$.$$\blacksquare$$

The last property we need is that an operator commuting with $$A$$ preserves every spectral subspace of $$A$$. This rests on the fact that commuting with $$A$$ propagates through the whole functional calculus.

> **Proposition** *(Commuting Operators Preserve Spectral Subspaces)*
<a name="prpstn:hall-7.16"></a>
<!--  \uses{def:hall-7.14} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{../spectral-theorems/#def:functional-calculus} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-convergence-theorem} -->
<!--  \uses{../spectral-theorems/#thrm:stone–weierstrass-complex} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{../spectral-theorems/#lmm:hall-prblm-8.3.3c} -->
<!--  \uses{lmm:spectrum-compact-general} -->
<!--  \uses{../spectral-theorems/#lmm:lemma-2} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be self-adjoint and let $$B \in \mathcal{B}(\mathbf{H})$$ commute with $$A$$. Then
>
> 1. $$B$$ commutes with $$f(A)$$ for every bounded measurable $$f$$ on $$\sigma(A)$$; and
> 2. every spectral subspace $$V_E$$ of $$A$$ is invariant under $$B$$.

**Proof**
**Part 1.** Let $$\mathcal{F}$$ denote the set of bounded measurable $$f$$ on $$\sigma(A)$$ with $$Bf(A) = f(A)B$$. We show $$\mathcal{F}$$ contains all bounded measurable functions, in three steps.

*Polynomials.* $$B$$ commutes with $$A$$ by hypothesis, hence with $$A^m$$ for every $$m$$ (induction: $$BA^{m+1} = (BA^m)A = (A^mB)A = A^m(BA) = A^m(AB) = A^{m+1}B$$) and hence, by linearity, with $$p(A)$$ for every polynomial $$p$$. So $$\mathcal{F}$$ contains all polynomials.

*Continuous functions.* If $$f$$ is continuous on $$\sigma(A)$$, the [**Complex Stone–Weierstrass Theorem**](../spectral-theorems/#thrm:stone–weierstrass-complex) supplies polynomials $$p_n \to f$$ uniformly on $$\sigma(A)$$; the functional calculus is isometric on continuous functions, so $$p_n(A) \to f(A)$$ in operator norm. Since multiplication by the fixed bounded operator $$B$$ is continuous in the operator norm (on either side, by [submultiplicativity](../spectral-theorems/#lmm:lemma-2)), passing to the limit in $$Bp_n(A) = p_n(A)B$$ gives $$Bf(A) = f(A)B$$. So $$\mathcal{F}$$ contains $$C^0(\sigma(A);\mathbb{C})$$.

*Bounded measurable functions.* We show $$\mathcal{F}$$ is closed under uniformly bounded pointwise limits. The key is the following convergence fact, which we establish first: if $$\{f_i\}$$ are bounded measurable with $$\lvert f_i \rvert \le M$$ and $$f_i \to f$$ pointwise on $$\sigma(A)$$, then

$$
    \left< \phi, f_i(A)\psi \right> \longrightarrow \left< \phi, f(A)\psi \right> \qquad \text{for all } \phi,\psi \in \mathbf{H}. \tag{$\dagger\dagger$}
$$

Indeed, writing $$Q_g(\xi) \equiv \left< \xi, g(A)\xi \right> = \int_{\sigma(A)} g \, d\mu^A_\xi$$ for the quadratic form attached to a bounded measurable $$g$$ — the second equality being the defining property of the [functional calculus](../spectral-theorems/#def:functional-calculus) — the [**Bounded Convergence Theorem**](../spectral-theorems/#thrm:bounded-convergence-theorem) applies to each fixed $$\xi$$ (the measure $$\mu^A_\xi$$ being finite, with total mass $$\left\| \xi \right\|^2$$) and gives $$Q_{f_i}(\xi) \to Q_f(\xi)$$ for every $$\xi \in \mathbf{H}$$. By Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties), applied with $$D = \mathbf{H}$$ and $$T = g(A)$$, the sesquilinear form associated to $$Q_g$$ is $$(\phi,\psi) \mapsto \left< \phi, g(A)\psi \right>$$; and that form is given by the polarization formula as a fixed finite linear combination of the five values $$Q_g(\phi+\psi), Q_g(\phi), Q_g(\psi), Q_g(\phi+i\psi), Q_g(i\psi)$$. Each of those five converges as $$i \to \infty$$ by the previous sentence, so the linear combinations converge too, which is exactly $$(\dagger\dagger)$$.

Now let $$\{f_i\}$$ be as above with each $$f_i \in \mathcal{F}$$. For all $$\phi,\psi \in \mathbf{H}$$, applying $$(\dagger\dagger)$$ twice — once with the fixed vector $$B\psi$$ in the second slot, once with the fixed vector $$B^*\phi$$ in the first —

$$
    \left< \phi, f(A)B\psi \right> = \lim_{i\to\infty} \left< \phi, f_i(A)B\psi \right> = \lim_{i\to\infty} \left< \phi, Bf_i(A)\psi \right> = \lim_{i\to\infty} \left< B^*\phi, f_i(A)\psi \right> = \left< B^*\phi, f(A)\psi \right> = \left< \phi, Bf(A)\psi \right>,
$$

where the second equality used $$f_i \in \mathcal{F}$$ and the third and last used the [definition of the adjoint](#def:hall-9.1) for the bounded operator $$B$$. Since this holds for all $$\phi \in \mathbf{H}$$, [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) with $$D = \mathbf{H}$$ gives $$f(A)B\psi = Bf(A)\psi$$ for every $$\psi$$, i.e. $$f \in \mathcal{F}$$.

It remains to pass from continuous to bounded measurable $$f$$, and for this we appeal to [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c) rather than to a monotone-class argument. Its three hypotheses hold for $$\mathcal{F}$$:

1. *$$\mathcal{F}$$ is a complex vector space.* If $$f_1,f_2 \in \mathcal{F}$$ and $$\alpha_1,\alpha_2 \in \mathbb{C}$$, then, using linearity of the [functional calculus](../spectral-theorems/#def:functional-calculus) and of multiplication by the fixed operator $$B$$, $$B(\alpha_1f_1+\alpha_2f_2)(A) = \alpha_1Bf_1(A) + \alpha_2Bf_2(A) = \alpha_1f_1(A)B + \alpha_2f_2(A)B = (\alpha_1f_1+\alpha_2f_2)(A)B$$.
2. *$$\mathcal{F}$$ contains $$C^0(\sigma(A);\mathbb{R})$$.* This is the previous step, which established the stronger statement that $$\mathcal{F} \supset C^0(\sigma(A);\mathbb{C})$$.
3. *$$\mathcal{F}$$ is closed under pointwise limits of uniformly bounded sequences.* This is what was just shown.

Finally, $$\sigma(A)$$ is a compact metric measurable space, by [**Lemma** *(The Spectrum of a Bounded Operator is a Compact Metric Measurable Space)*](#lmm:spectrum-compact-general). So [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c) applies and gives that $$\mathcal{F}$$ consists of *all* bounded measurable complex-valued functions on $$\sigma(A)$$, which is **Part 1**.

**Part 2.** Let $$\psi \in V_E = \text{Range}(\mu^A(E))$$, so $$\mu^A(E)\psi = \psi$$. By **Part 1** applied to $$f = 1_E$$, $$B\mu^A(E) = \mu^A(E)B$$, so

$$
    B\psi = B\mu^A(E)\psi = \mu^A(E)(B\psi) \in \text{Range}\big(\mu^A(E)\big) = V_E,
$$

i.e. $$V_E$$ is invariant under $$B$$.$$\blacksquare$$

### Almost Eigenvectors

Recall the target: the two-variable spectral mapping theorem $$\sigma\big(p(A,A^*)\big) = \{ p(\lambda,\overline\lambda) \mid \lambda \in \sigma(A) \}$$ for normal $$A$$. For *matrices* the argument is short, because the spectrum consists exactly of eigenvalues; the substitute for an eigenvector in infinite dimensions is an *almost* eigenvector. We first record the identity that makes normality work for us throughout.

> **Lemma** *(Normality Balances the Two Norms)*
<a name="lmm:normality-balances-norms"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{lmm:adjoint-product-and-involution} -->
<!--  \uses{lmm:adjoint-of-scalar-multiple-of-identity} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{def:hall-9.1} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal and $$\lambda \in \mathbb{C}$$. Then for every $$\psi \in \mathbf{H}$$,
>
> $$
>     \left\| (A^* - \overline\lambda\mathbf{1})\psi \right\| = \left\| (A - \lambda\mathbf{1})\psi \right\|.
> $$

**Proof**
First note $$A - \lambda\mathbf{1}$$ is again normal. Its adjoint is $$A^* - \overline{\lambda}\mathbf{1}$$, by [**Proposition** *(Adjoint of a Sum with a Bounded Operator)*](#prpstn:hall-9.13) together with [**Lemma** *(Adjoint of a Scalar Multiple of the Identity)*](#lmm:adjoint-of-scalar-multiple-of-identity); and expanding both products, using $$AA^* = A^*A$$ (normality) and the fact that scalar multiples of $$\mathbf{1}$$ commute with everything,

$$
\begin{align}
    (A - \lambda\mathbf{1})(A^* - \overline\lambda\mathbf{1}) &= AA^* - \overline\lambda A - \lambda A^* + \lvert \lambda \rvert^2 \mathbf{1} \\
    (A^* - \overline\lambda\mathbf{1})(A - \lambda\mathbf{1}) &= A^*A - \lambda A^* - \overline\lambda A + \lvert \lambda \rvert^2 \mathbf{1},
\end{align}
$$

which agree. Now, for $$\psi \in \mathbf{H}$$, using the [definition of the adjoint](#def:hall-9.1) and [**Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*](#lmm:adjoint-product-and-involution) (to identify $$(A^* - \overline\lambda\mathbf{1})^* = A - \lambda\mathbf{1}$$),

$$
\begin{align}
    \left\| (A^* - \overline\lambda\mathbf{1})\psi \right\|^2
        &= \left< (A^* - \overline\lambda\mathbf{1})\psi, (A^* - \overline\lambda\mathbf{1})\psi \right> \\
        &= \left< \psi, (A - \lambda\mathbf{1})(A^* - \overline\lambda\mathbf{1})\psi \right> \\
        &= \left< \psi, (A^* - \overline\lambda\mathbf{1})(A - \lambda\mathbf{1})\psi \right> \\
        &= \left< (A - \lambda\mathbf{1})\psi, (A - \lambda\mathbf{1})\psi \right> \\
        &= \left\| (A - \lambda\mathbf{1})\psi \right\|^2,
\end{align}
$$

the middle equality being the commutation just verified. Taking square roots gives the result.$$\blacksquare$$

> **Definition** *($$\varepsilon$$-Almost Eigenvector)*
<a name="def:hall-10.24"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$, $$\lambda \in \mathbb{C}$$, and $$\varepsilon > 0$$. An *$$\varepsilon$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda$$* is a nonzero vector $$\psi \in \mathbf{H}$$ with
>
> $$
>     \left\| (A - \lambda\mathbf{1})\psi \right\| < \varepsilon \left\| \psi \right\|.
> $$

Note that, unlike the set of genuine eigenvectors for a fixed $$\lambda$$, the set of $$\varepsilon$$-almost eigenvectors is *not* a subspace — this is precisely the difficulty that spectral subspaces will be used to circumvent below.

> **Lemma**
<a name="lmm:hall-10.25"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-10.24} -->
<!--  \uses{lmm:normality-balances-norms} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{prpstn:hall-9.14} -->
<!--  \uses{prpstn:hall-9.12} -->
<!--  \uses{crllr:trivial-complement-characterizes-density} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{def:kernel-of-an-unbounded-operator} -->
<!--  \uses{thrm:hall-9.17} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal.
>
> 1. If $$\psi$$ is an $$\varepsilon$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda$$, then $$\psi$$ is an $$\varepsilon$$-almost eigenvector for $$A^*$$ with eigenvalue $$\overline\lambda$$.
> 2. $$\lambda \in \sigma(A)$$ if and only if, for every $$\varepsilon > 0$$, there exists an $$\varepsilon$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda$$.

**Proof**
**Part 1.** Immediate from [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms): $$\left\| (A^*-\overline\lambda\mathbf{1})\psi \right\| = \left\| (A-\lambda\mathbf{1})\psi \right\| < \varepsilon\left\| \psi \right\|$$, and $$\psi \ne 0$$.

**Part 2.** Suppose first that for every $$\varepsilon > 0$$ an $$\varepsilon$$-almost eigenvector $$\psi_\varepsilon$$ exists. If $$\lambda$$ were in the resolvent set, $$A - \lambda\mathbf{1}$$ would have a bounded inverse $$S$$, and then for every $$\varepsilon>0$$,

$$
    \left\| \psi_\varepsilon \right\| = \left\| S(A-\lambda\mathbf{1})\psi_\varepsilon \right\| \le \left\| S \right\| \left\| (A-\lambda\mathbf{1})\psi_\varepsilon \right\| < \left\| S \right\| \varepsilon \left\| \psi_\varepsilon \right\|.
$$

Since $$\psi_\varepsilon \ne 0$$, dividing by $$\left\| \psi_\varepsilon \right\|$$ gives $$1 < \left\| S \right\|\varepsilon$$ for every $$\varepsilon>0$$, which fails for $$\varepsilon < 1/\left\| S \right\|$$ (note $$\left\| S \right\| \neq 0$$, since $$S$$ is invertible and $$\mathbf{H} \ne \{0\}$$ whenever a nonzero $$\psi_\varepsilon$$ exists). So $$\lambda \in \sigma(A)$$.

Conversely, suppose that for some $$\varepsilon > 0$$ *no* $$\varepsilon$$-almost eigenvector with eigenvalue $$\lambda$$ exists. Then

$$
    \left\| (A - \lambda\mathbf{1})\psi \right\| \ge \varepsilon \left\| \psi \right\| \tag{$\natural$}
$$

for every $$\psi \in \mathbf{H}$$ — for nonzero $$\psi$$ because $$\psi$$ fails the defining inequality, and trivially for $$\psi = 0$$. In particular $$A - \lambda\mathbf{1}$$ is injective.

By [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms), $$(\natural)$$ holds equally with $$A - \lambda\mathbf{1}$$ replaced by $$A^* - \overline\lambda\mathbf{1}$$, so $$A^* - \overline\lambda\mathbf{1}$$ is injective too, i.e. $$\text{Ker}(A^* - \overline\lambda\mathbf{1}) = \{0\}$$. Since $$(A-\lambda\mathbf{1})^* = A^* - \overline\lambda\mathbf{1}$$ (as in the proof of [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms)), [**Proposition** *(Orthogonal Complement of the Range)*](#prpstn:hall-9.12) gives

$$
    \big( \text{Range}(A - \lambda\mathbf{1}) \big)^\perp = \text{Ker}\big( (A-\lambda\mathbf{1})^* \big) = \{0\},
$$

so by [**Corollary** *(Trivial Complement Characterizes Density)*](#crllr:trivial-complement-characterizes-density), $$\text{Range}(A-\lambda\mathbf{1})$$ is dense in $$\mathbf{H}$$. A bounded operator is in particular closed (its graph is closed: if $$\psi_n\to\psi$$ and $$(A-\lambda\mathbf{1})\psi_n \to \varphi$$ then continuity gives $$(A-\lambda\mathbf{1})\psi = \varphi$$, and $$\text{Dom} = \mathbf{H}$$ contains $$\psi$$), so $$(\natural)$$ lets us apply [**Proposition** *(Closedness of the Range from a Lower Bound)*](#prpstn:hall-9.14) to conclude $$\text{Range}(A-\lambda\mathbf{1})$$ is closed. Dense and closed, it is all of $$\mathbf{H}$$.

So $$A - \lambda\mathbf{1}$$ is a bijection of $$\mathbf{H}$$ onto $$\mathbf{H}$$; let $$S$$ be its inverse (linear, by the argument used in the proof of [**Theorem** *(Spectrum of a Self-Adjoint Operator is Real)*](#thrm:hall-9.17)). For $$\phi \in \mathbf{H}$$, applying $$(\natural)$$ with $$\psi = S\phi$$ gives $$\left\| \phi \right\| = \left\| (A-\lambda\mathbf{1})S\phi \right\| \ge \varepsilon\left\| S\phi \right\|$$, so $$\left\| S\phi \right\| \le \varepsilon^{-1}\left\| \phi \right\|$$ and $$S$$ is bounded. By the [definition of the resolvent set](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum), $$\lambda$$ is in the resolvent set of $$A$$, i.e. $$\lambda \notin \sigma(A)$$. This is the contrapositive of the remaining direction.$$\blacksquare$$

> **Lemma**
<a name="lmm:hall-10.26"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-10.24} -->
<!--  \uses{lmm:normality-balances-norms} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, $$p$$ a polynomial in two variables, and $$\lambda \in \mathbb{C}$$. Then there is a constant $$C$$ (depending on $$p$$, $$A$$, and $$\lambda$$, but not on $$\varepsilon$$ or $$\psi$$) such that: if $$\psi$$ is an $$\varepsilon$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda$$, then $$\psi$$ is a $$(C\varepsilon)$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$p(\lambda,\overline\lambda)$$.

**Proof**
Write $$p(\lambda,\overline\lambda) = \sum_{k,l} a_{kl}\lambda^k\overline\lambda^{\,l}$$, so that $$p(A,A^*) = \sum_{k,l} a_{kl}A^k(A^*)^l$$ (a well-defined expression, since $$A$$ and $$A^*$$ commute). Then

$$
    \big( p(A,A^*) - p(\lambda,\overline\lambda)\mathbf{1} \big)\psi = \sum_{k,l} a_{kl}\big( A^k(A^*)^l - \lambda^k\overline\lambda^{\,l}\mathbf{1} \big)\psi,
$$

so, by the triangle inequality, it suffices to bound $$\left\| \big( A^k(A^*)^l - \lambda^k\overline\lambda^{\,l}\mathbf{1} \big)\psi \right\|$$ by $$c_{kl}\varepsilon\left\| \psi \right\|$$ for each $$(k,l)$$. We then set

$$
    C \equiv 1 + \sum_{k,l} \lvert a_{kl} \rvert c_{kl},
$$

the added $$1$$ serving two purposes made precise at the end of the proof: it forces $$C > 0$$, and it converts the non-strict bound the induction produces into the *strict* inequality that [Definition ($$\varepsilon$$-Almost Eigenvector)](#def:hall-10.24) requires.

We prove the required bound by induction on $$k+l$$. For $$k+l = 0$$ the operator is $$\mathbf{1} - \mathbf{1} = 0$$ and $$c_{00}=0$$ works. For $$k=1, l=0$$, $$\left\| (A-\lambda\mathbf{1})\psi \right\| < \varepsilon\left\| \psi \right\|$$ by hypothesis, so $$c_{10}=1$$ works; for $$k=0,l=1$$, $$\left\| (A^*-\overline\lambda\mathbf{1})\psi \right\| = \left\| (A-\lambda\mathbf{1})\psi \right\| < \varepsilon\left\| \psi \right\|$$ by [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms), so $$c_{01}=1$$ works.

Suppose the bound holds for all pairs with $$k+l = N$$, and let $$k+l = N+1$$. If $$k > 0$$, the algebraic identity

$$
    \big( A^k(A^*)^l - \lambda^k\overline\lambda^{\,l}\mathbf{1} \big)\psi
      = A^{k-1}(A^*)^l (A - \lambda\mathbf{1})\psi
      + \lambda\big( A^{k-1}(A^*)^l - \lambda^{k-1}\overline\lambda^{\,l}\mathbf{1} \big)\psi
$$

holds. Indeed, expanding the right-hand side, the two $$\lambda A^{k-1}(A^*)^l\psi$$ terms cancel, leaving $$A^{k-1}(A^*)^lA\psi - \lambda^k\overline\lambda^{\,l}\psi$$; and $$A^{k-1}(A^*)^lA = A^k(A^*)^l$$, since $$A$$ commutes with $$A^*$$ by normality (so $$A$$ may be moved leftwards past each of the $$l$$ factors of $$A^*$$), giving the left-hand side. The first term has norm at most $$\left\| A \right\|^{k-1}\left\| A^* \right\|^l \left\| (A-\lambda\mathbf{1})\psi \right\| \le \left\| A \right\|^{k-1}\left\| A^* \right\|^l \varepsilon \left\| \psi \right\|$$, by [submultiplicativity of the operator norm](../spectral-theorems/#lmm:lemma-2) and the hypothesis on $$\psi$$. The second has norm at most $$\lvert \lambda \rvert c_{k-1,l}\varepsilon\left\| \psi \right\|$$, by the inductive hypothesis (applicable since $$(k-1)+l = N$$). So $$c_{kl} = \left\| A \right\|^{k-1}\left\| A^* \right\|^l + \lvert \lambda \rvert c_{k-1,l}$$ works. If $$k = 0$$, then $$l > 0$$, and the symmetric identity

$$
    \big( (A^*)^l - \overline\lambda^{\,l}\mathbf{1} \big)\psi
      = (A^*)^{l-1}(A^* - \overline\lambda\mathbf{1})\psi
      + \overline\lambda\big( (A^*)^{l-1} - \overline\lambda^{\,l-1}\mathbf{1} \big)\psi
$$

gives, in the same way (using [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms) to bound $$\left\| (A^*-\overline\lambda\mathbf{1})\psi \right\|$$ by $$\varepsilon\left\| \psi \right\|$$), $$c_{0l} = \left\| A^* \right\|^{l-1} + \lvert \lambda \rvert c_{0,l-1}$$.

Combining the per-term bounds with the triangle inequality gives the *non-strict* estimate

$$
    \left\| \big( p(A,A^*) - p(\lambda,\overline\lambda)\mathbf{1} \big)\psi \right\| \le \Big( \sum_{k,l} \lvert a_{kl} \rvert c_{kl} \Big)\varepsilon\left\| \psi \right\|.
$$

Since $$\psi \ne 0$$ by hypothesis and $$\varepsilon > 0$$, we have $$\varepsilon\left\| \psi \right\| > 0$$, so $$\big(\sum_{k,l}\lvert a_{kl}\rvert c_{kl}\big)\varepsilon\left\| \psi \right\| < C\varepsilon\left\| \psi \right\|$$ by the definition of $$C$$ (which exceeds that sum by $$1$$). Chaining, $$\left\| \big( p(A,A^*) - p(\lambda,\overline\lambda)\mathbf{1} \big)\psi \right\| < C\varepsilon\left\| \psi \right\|$$ — a strict inequality, as required — and $$\psi \ne 0$$, so $$\psi$$ is a $$(C\varepsilon)$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$p(\lambda,\overline\lambda)$$.$$\blacksquare$$

Two small structural facts are needed before the main construction: that polynomials in $$A$$ and $$A^*$$ are again normal, and that restricting a normal operator to a subspace invariant under both $$A$$ and $$A^*$$ leaves it normal.

> **Lemma** *(Polynomials in a Normal Operator are Normal)*
<a name="lmm:polynomials-in-normal-are-normal"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{lmm:adjoint-product-and-involution} -->
<!--  \uses{lmm:adjoint-of-scalar-multiple-of-identity} -->
<!--  \uses{prpstn:hall-9.13} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal and $$p$$ a polynomial in two variables, $$p(\lambda,\overline\lambda) = \sum_{k,l} a_{kl}\lambda^k\overline\lambda^{\,l}$$. Then $$p(A,A^*) \equiv \sum_{k,l} a_{kl}A^k(A^*)^l$$ satisfies
>
> $$
>     \big( p(A,A^*) \big)^* = \overline{p}(A,A^*), \qquad \text{where } \overline{p}(\lambda,\overline\lambda) \equiv \sum_{k,l} \overline{a_{kl}}\,\lambda^l\overline\lambda^{\,k},
> $$
>
> and $$p(A,A^*)$$ is normal. Moreover $$p(A,A^*)$$, and its adjoint, commute with both $$A$$ and $$A^*$$.

**Proof**
By [**Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*](#lmm:adjoint-product-and-involution), $$\big( A^k(A^*)^l \big)^* = \big((A^*)^l\big)^*\big(A^k\big)^* = A^l (A^*)^k$$, using Part 1 repeatedly to reverse each product and Part 2 to simplify $$(A^*)^* = A$$. Adjoints are conjugate-linear (by [**Proposition** *(Adjoint of a Sum with a Bounded Operator)*](#prpstn:hall-9.13) for additivity and [**Lemma** *(Adjoint of a Scalar Multiple of the Identity)*](#lmm:adjoint-of-scalar-multiple-of-identity) for scalars), so $$\big( p(A,A^*) \big)^* = \sum_{k,l}\overline{a_{kl}}A^l(A^*)^k = \overline{p}(A,A^*)$$.

Since $$A$$ commutes with $$A^*$$ (normality), any two words in the letters $$A$$ and $$A^*$$ commute: repeated application of $$AA^*=A^*A$$ lets one transpose adjacent letters, so any word can be rearranged into the normal form $$A^k(A^*)^l$$, and two such normal forms commute because $$A^k(A^*)^lA^{k'}(A^*)^{l'} = A^{k+k'}(A^*)^{l+l'} = A^{k'}(A^*)^{l'}A^k(A^*)^l$$. By bilinearity of the product, any two linear combinations of such words commute; in particular $$p(A,A^*)$$ commutes with $$\overline{p}(A,A^*) = \big(p(A,A^*)\big)^*$$, i.e. $$p(A,A^*)$$ is normal, and both commute with $$A$$ and with $$A^*$$ (themselves such words).$$\blacksquare$$

> **Lemma** *(Restriction of a Normal Operator to a Doubly Invariant Subspace)*
<a name="lmm:restriction-of-normal-operator"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:closed-subspace-is-hilbert} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal and let $$W \subset \mathbf{H}$$ be a nonzero closed subspace invariant under both $$A$$ and $$A^*$$. Then $$W$$ is a separable Hilbert space in the inherited inner product, $$A\vert_W \in \mathcal{B}(W)$$, its adjoint (computed in $$W$$) is $$A^*\vert_W$$, and $$A\vert_W$$ is normal.

**Proof**
$$W$$ is a closed subspace of $$\mathbf{H}$$, hence itself a separable Hilbert space by [**Lemma** *(A Closed Subspace is a Separable Hilbert Space)*](#lmm:closed-subspace-is-hilbert). Invariance means $$A\vert_W$$ maps $$W$$ into $$W$$, and $$\left\| A\vert_W\eta \right\| = \left\| A\eta \right\| \le \left\| A \right\|\left\| \eta \right\|$$, so $$A\vert_W \in \mathcal{B}(W)$$ with $$\left\| A\vert_W \right\| \le \left\| A \right\|$$.

For the adjoint: for $$\eta,\zeta \in W$$, $$\left< \eta, (A\vert_W)\zeta \right> = \left< \eta, A\zeta \right> = \left< A^*\eta, \zeta \right> = \left< (A^*\vert_W)\eta, \zeta \right>$$, the middle equality by the [definition of the adjoint](#def:hall-9.1) in $$\mathbf{H}$$ and the last because $$A^*\eta \in W$$ by invariance. As this holds for all $$\eta,\zeta \in W$$, the adjoint of $$A\vert_W$$ in $$\mathcal{B}(W)$$ is $$A^*\vert_W$$.

Normality: for $$\eta \in W$$, $$(A\vert_W)(A\vert_W)^*\eta = A A^*\eta = A^*A\eta = (A\vert_W)^*(A\vert_W)\eta$$, using invariance to keep every intermediate vector in $$W$$ and normality of $$A$$ in the middle.$$\blacksquare$$

We can now carry out the construction that replaces the matrix-case eigenspace argument.

> **Lemma**
<a name="lmm:hall-10.27"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-10.24} -->
<!--  \uses{def:hall-7.14} -->
<!--  \uses{prpstn:hall-7.15} -->
<!--  \uses{prpstn:hall-7.16} -->
<!--  \uses{lmm:hall-10.25} -->
<!--  \uses{lmm:hall-10.26} -->
<!--  \uses{lmm:polynomials-in-normal-are-normal} -->
<!--  \uses{lmm:adjoint-product-and-involution} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.43} -->
<!--  \uses{lmm:self-adjoint-is-normal} -->
<!--  \uses{../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:normality-balances-norms} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, $$p$$ a polynomial in two variables, and $$\mu \in \sigma\big( p(A,A^*) \big)$$. Then for every $$\varepsilon > 0$$ there is a nonzero closed subspace $$W^\varepsilon \subset \mathbf{H}$$, invariant under both $$A$$ and $$A^*$$, every nonzero element of which is an $$\varepsilon$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$\mu$$.

**Proof**
Fix $$\varepsilon > 0$$ and set $$B \equiv p(A,A^*) - \mu\mathbf{1}$$. By [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal), $$p(A,A^*)$$ is normal, and hence so is $$B$$ (the computation in the proof of [**Lemma** *(Normality Balances the Two Norms)*](#lmm:normality-balances-norms) shows that subtracting a scalar multiple of $$\mathbf{1}$$ preserves normality). Since $$\mu \in \sigma(p(A,A^*))$$, $$0 \in \sigma(B)$$ — for $$B - 0\cdot\mathbf{1} = p(A,A^*) - \mu\mathbf{1}$$ has a bounded two-sided inverse exactly when $$\mu$$ is in the resolvent set of $$p(A,A^*)$$.

*Step 1: $$0 \in \sigma(B^*B)$$.* The operator $$B^*B$$ is self-adjoint, by [**Lemma** *(Adjoint of a Product; the Adjoint is an Involution)*](#lmm:adjoint-product-and-involution): $$(B^*B)^* = B^*(B^*)^* = B^*B$$. Let $$\delta > 0$$. Apply [**Lemma** *(hall-10.26)*](#lmm:hall-10.26) to the normal operator $$B$$ with the polynomial $$q(\lambda,\overline\lambda) = \lambda\overline\lambda$$. Substituting gives $$q(B,B^*) = BB^*$$, which equals $$B^*B$$ because $$B$$ is normal; and $$q(0,\overline{0}) = 0$$. The lemma supplies a constant $$C_q$$, which satisfies $$C_q > 0$$ by its construction there, so the division by $$C_q$$ below is legitimate.

Since $$0 \in \sigma(B)$$ and $$B$$ is normal, Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25) gives, for the particular value $$\delta' \equiv \delta/C_q > 0$$, a $$\delta'$$-almost eigenvector $$\psi$$ for $$B$$ with eigenvalue $$0$$. By the lemma just applied, $$\psi$$ is then a $$(C_q\delta') = \delta$$-almost eigenvector for $$B^*B$$ with eigenvalue $$0$$. As $$\delta>0$$ was arbitrary, and $$B^*B$$ is normal by [**Lemma** *(Bounded Self-Adjoint Operators are Normal)*](#lmm:self-adjoint-is-normal) (it having been shown self-adjoint above), Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25) gives $$0 \in \sigma(B^*B)$$.

*Step 2: the spectral subspace.* Apply the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators) to $$B^*B$$ and let

$$
    W^\varepsilon \equiv V_{(-\varepsilon^2/4,\ \varepsilon^2/4)}
$$

be the spectral subspace of $$B^*B$$ for the interval $$(-\varepsilon^2/4, \varepsilon^2/4)$$, in the sense of [Definition (Spectral Subspaces)](#def:hall-7.14). It is a closed subspace, by that definition. Since $$0 \in \sigma(B^*B)$$ by **Step 1**, and the open disc $$\{ \lambda \in \mathbb{C} \mid \lvert \lambda \rvert < \varepsilon^2/4 \}$$ is an open neighbourhood of $$0$$ in $$\mathbb{C}$$ whose intersection with $$\sigma(B^*B) \subset \mathbb{R}$$ is exactly the interval $$(-\varepsilon^2/4,\varepsilon^2/4) \cap \sigma(B^*B)$$, Part 3 of [**Proposition** *(Properties of Spectral Subspaces)*](#prpstn:hall-7.15) — applied with $$X = \sigma(B^*B)$$ and $$\mu = \mu^{B^*B}$$, for which $$\int_X \iota\,d\mu = B^*B$$ by the [**Spectral Theorem for Bounded, Self-Adjoint Operators**](../spectral-theorems/#thrm:spectral-theorem-for-bounded-operators) — gives $$W^\varepsilon \ne \{0\}$$.

*Step 3: the almost-eigenvector bound.* Since every $$\lambda$$ in the defining set of $$W^\varepsilon$$ satisfies $$\lvert \lambda - 0 \rvert \le \varepsilon^2/4$$, Part 2 of [**Proposition** *(Properties of Spectral Subspaces)*](#prpstn:hall-7.15), applied with $$\lambda_0 = 0$$ and $$\varepsilon^2/4$$ in the role of $$\varepsilon$$ there, gives $$\left\| B^*B\psi \right\| \le (\varepsilon^2/4)\left\| \psi \right\|$$ for all $$\psi \in W^\varepsilon$$. Hence, by [Cauchy–Schwarz](../spectral-theorems/#prpstn:hall-a.43) and the [definition of the adjoint](#def:hall-9.1),

$$
    \left\| B\psi \right\|^2 = \left< B\psi, B\psi \right> = \left< \psi, B^*B\psi \right> \le \left\| \psi \right\| \left\| B^*B\psi \right\| \le \frac{\varepsilon^2}{4}\left\| \psi \right\|^2,
$$

so $$\left\| B\psi \right\| \le \tfrac{\varepsilon}{2}\left\| \psi \right\| < \varepsilon\left\| \psi \right\|$$ for every nonzero $$\psi \in W^\varepsilon$$. Since $$B = p(A,A^*) - \mu\mathbf{1}$$, this says exactly that every nonzero $$\psi \in W^\varepsilon$$ is an $$\varepsilon$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$\mu$$.

*Step 4: invariance.* By [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal), $$p(A,A^*)$$ and its adjoint commute with $$A$$ and with $$A^*$$; adding the scalar $$-\mu\mathbf{1}$$ (which commutes with everything) preserves this, so $$B$$ and $$B^*$$ commute with $$A$$ and $$A^*$$, and therefore so does the product $$B^*B$$. Applying Part 2 of [**Proposition** *(Commuting Operators Preserve Spectral Subspaces)*](#prpstn:hall-7.16) to the self-adjoint operator $$B^*B$$ and the commuting bounded operator $$A$$ shows $$W^\varepsilon$$ is invariant under $$A$$; the same with $$A^*$$ in place of $$A$$ gives invariance under $$A^*$$.$$\blacksquare$$

### The Two-Variable Spectral Mapping Theorem

> **Theorem** *(Spectral Mapping for Polynomials in $$A$$ and $$A^*$$)*
<a name="thrm:hall-10.23"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{def:hall-10.24} -->
<!--  \uses{lmm:hall-10.25} -->
<!--  \uses{lmm:hall-10.26} -->
<!--  \uses{lmm:hall-10.27} -->
<!--  \uses{lmm:polynomials-in-normal-are-normal} -->
<!--  \uses{lmm:restriction-of-normal-operator} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-7.5} -->
<!--  \uses{../spectral-theorems/#crllr:crllr-1} -->
<!--  \uses{prpstn:convergence-facts} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, with $$\mathbf{H} \ne \{0\}$$, and let $$p$$ be a polynomial in two variables. Then
>
> $$
>     \sigma\big( p(A,A^*) \big) = \big\{ p(\lambda,\overline\lambda) \;\mid\; \lambda \in \sigma(A) \big\}.
> $$

**Proof**
Before either inclusion, we record a uniformity remark about the constant $$C$$ of [**Lemma** *(hall-10.26)*](#lmm:hall-10.26). Inspecting the recursion there, $$C$$ is built from $$\left\| A \right\|$$, $$\left\| A^* \right\|$$, the coefficients of $$p$$, and $$\lvert \lambda \rvert$$, and is non-decreasing in $$\lvert \lambda \rvert$$. By [**Corollary**](../spectral-theorems/#crllr:crllr-1), every $$\lambda \in \sigma(A)$$ satisfies $$\lvert \lambda \rvert \le R(A) \le \left\| A \right\|$$; and, as we will see, every $$\lambda$$ arising below satisfies $$\lvert \lambda \rvert \le \left\| A \right\|$$ as well. So there is a single constant $$C$$, depending only on $$p$$ and $$A$$, valid for all $$\lambda$$ with $$\lvert\lambda\rvert \le \left\|A\right\|$$. The constant produced by [**Lemma** *(hall-10.26)*](#lmm:hall-10.26) already satisfies $$C > 0$$, by its construction there, so the divisions by $$C$$ below are legitimate; we fix such a $$C$$ once and for all.

**($$\supset$$).** Let $$\lambda \in \sigma(A)$$ and let $$\varepsilon > 0$$. By Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25), there is an $$(\varepsilon/C)$$-almost eigenvector $$\psi$$ for $$A$$ with eigenvalue $$\lambda$$. By [**Lemma** *(hall-10.26)*](#lmm:hall-10.26), $$\psi$$ is then a $$(C \cdot \varepsilon/C) = \varepsilon$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$p(\lambda,\overline\lambda)$$. As $$\varepsilon>0$$ was arbitrary and $$p(A,A^*)$$ is normal by [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal), Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25), applied to $$p(A,A^*)$$, gives $$p(\lambda,\overline\lambda) \in \sigma\big(p(A,A^*)\big)$$.

**($$\subset$$).** Let $$\mu \in \sigma\big(p(A,A^*)\big)$$. Fix $$n \in \mathbb{N}$$ and put $$\varepsilon_n \equiv 1/n$$. By [**Lemma** *(hall-10.27)*](#lmm:hall-10.27) there is a nonzero closed subspace $$W^{\varepsilon_n}$$, invariant under $$A$$ and $$A^*$$, every nonzero element of which is an $$\varepsilon_n$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$\mu$$.

By [**Lemma** *(Restriction of a Normal Operator to a Doubly Invariant Subspace)*](#lmm:restriction-of-normal-operator), $$A\vert_{W^{\varepsilon_n}}$$ is a normal element of $$\mathcal{B}(W^{\varepsilon_n})$$ with $$\left\| A\vert_{W^{\varepsilon_n}} \right\| \le \left\| A \right\|$$, and $$W^{\varepsilon_n} \ne \{0\}$$, so by [**Proposition** *(hall-7.5)*](../spectral-theorems/#prpstn:hall-7.5) its spectrum is non-empty. Choose $$\lambda_n \in \sigma\big( A\vert_{W^{\varepsilon_n}} \big)$$; then $$\lvert \lambda_n \rvert \le \left\| A\vert_{W^{\varepsilon_n}} \right\| \le \left\| A \right\|$$, by [**Corollary**](../spectral-theorems/#crllr:crllr-1), so the constant $$C$$ fixed above applies to $$\lambda_n$$.

By Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25) applied to the normal operator $$A\vert_{W^{\varepsilon_n}}$$ on the Hilbert space $$W^{\varepsilon_n}$$, there is an $$\varepsilon_n$$-almost eigenvector $$\psi_n \in W^{\varepsilon_n}$$ for $$A\vert_{W^{\varepsilon_n}}$$ with eigenvalue $$\lambda_n$$; since $$A\vert_{W^{\varepsilon_n}}\psi_n = A\psi_n$$ and the norms agree, $$\psi_n$$ is an $$\varepsilon_n$$-almost eigenvector for $$A$$ (on $$\mathbf{H}$$) with eigenvalue $$\lambda_n$$. By [**Lemma** *(hall-10.26)*](#lmm:hall-10.26), $$\psi_n$$ is a $$(C\varepsilon_n)$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$p(\lambda_n,\overline{\lambda_n})$$. On the other hand $$\psi_n$$ is a nonzero element of $$W^{\varepsilon_n}$$, hence an $$\varepsilon_n$$-almost eigenvector for $$p(A,A^*)$$ with eigenvalue $$\mu$$. Combining, and writing $$P \equiv p(A,A^*)$$,

$$
\begin{align}
    \big\lvert \mu - p(\lambda_n,\overline{\lambda_n}) \big\rvert \left\| \psi_n \right\|
        &= \left\| \big( \mu - p(\lambda_n,\overline{\lambda_n}) \big)\psi_n \right\| \\
        &= \left\| \big( P - p(\lambda_n,\overline{\lambda_n})\mathbf{1} \big)\psi_n - \big( P - \mu\mathbf{1} \big)\psi_n \right\| \\
        &\le \left\| \big( P - p(\lambda_n,\overline{\lambda_n})\mathbf{1} \big)\psi_n \right\| + \left\| \big( P - \mu\mathbf{1} \big)\psi_n \right\| \\
        &< C\varepsilon_n \left\| \psi_n \right\| + \varepsilon_n \left\| \psi_n \right\|.
\end{align}
$$

Dividing by $$\left\| \psi_n \right\| \ne 0$$,

$$
    \big\lvert \mu - p(\lambda_n,\overline{\lambda_n}) \big\rvert < (C+1)\varepsilon_n = \frac{C+1}{n}. \tag{$\flat$}
$$

The sequence $$\{\lambda_n\}$$ lies in the closed disc $$K \equiv \{ \lvert z \rvert \le \left\| A \right\| \}$$, which is closed and bounded in $$\mathbb{C}$$, so by Part 2 of [**Proposition** *(Convergence Facts for Sequences and Series)*](#prpstn:convergence-facts) it has a subsequence $$\lambda_{n_j} \to \lambda_\infty$$ with $$\lambda_\infty \in K$$, i.e. $$\lvert \lambda_\infty \rvert \le \left\| A \right\|$$.

We claim $$\lambda_\infty \in \sigma(A)$$. Let $$\delta > 0$$. For each $$j$$, using the triangle inequality and that $$\psi_{n_j}$$ is an $$\varepsilon_{n_j}$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda_{n_j}$$,

$$
    \left\| (A - \lambda_\infty\mathbf{1})\psi_{n_j} \right\|
      \le \left\| (A - \lambda_{n_j}\mathbf{1})\psi_{n_j} \right\| + \lvert \lambda_{n_j} - \lambda_\infty \rvert \left\| \psi_{n_j} \right\|
      < \big( \varepsilon_{n_j} + \lvert \lambda_{n_j} - \lambda_\infty \rvert \big) \left\| \psi_{n_j} \right\|.
$$

Choosing $$j$$ large enough that $$\varepsilon_{n_j} + \lvert \lambda_{n_j}-\lambda_\infty \rvert < \delta$$ (possible since both terms tend to $$0$$) exhibits $$\psi_{n_j}$$ as a $$\delta$$-almost eigenvector for $$A$$ with eigenvalue $$\lambda_\infty$$. As $$\delta>0$$ was arbitrary, Part 2 of [**Lemma** *(hall-10.25)*](#lmm:hall-10.25) gives $$\lambda_\infty \in \sigma(A)$$.

Finally, $$p$$ is a polynomial, hence continuous as a function of $$(\lambda,\overline\lambda)$$, so $$p(\lambda_{n_j},\overline{\lambda_{n_j}}) \to p(\lambda_\infty,\overline{\lambda_\infty})$$; and by $$(\flat)$$, $$p(\lambda_{n_j},\overline{\lambda_{n_j}}) \to \mu$$. By uniqueness of limits in $$\mathbb{C}$$, $$\mu = p(\lambda_\infty,\overline{\lambda_\infty})$$ with $$\lambda_\infty \in \sigma(A)$$, which is the required inclusion.$$\blacksquare$$

Combining [**Theorem** *(Spectral Mapping for Polynomials in $$A$$ and $$A^*$$)*](#thrm:hall-10.23) with [**Proposition** *(Norm Equals Spectral Radius for Normal Operators)*](#prpstn:hall-10.21) gives the norm identity that drives the construction of the functional calculus.

> **Corollary** *(Norm of a Polynomial in $$A$$ and $$A^*$$)*
<a name="crllr:norm-of-polynomial-in-a-astar"></a>
<!--  \uses{thrm:hall-10.23} -->
<!--  \uses{prpstn:hall-10.21} -->
<!--  \uses{lmm:polynomials-in-normal-are-normal} -->
<!--  \uses{../spectral-theorems/#def:spectral-radius} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, with $$\mathbf{H} \ne \{0\}$$, and $$p$$ a polynomial in two variables. Then
>
> $$
>     \left\| p(A,A^*) \right\| = \sup_{\lambda \in \sigma(A)} \big\lvert p(\lambda,\overline\lambda) \big\rvert.
> $$

**Proof**
By [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal), $$p(A,A^*)$$ is normal, so [**Proposition** *(Norm Equals Spectral Radius for Normal Operators)*](#prpstn:hall-10.21) gives $$\left\| p(A,A^*) \right\| = R\big( p(A,A^*) \big)$$. By the [definition of the spectral radius](../spectral-theorems/#def:spectral-radius) and [**Theorem** *(Spectral Mapping for Polynomials in $$A$$ and $$A^*$$)*](#thrm:hall-10.23),

$$
    R\big( p(A,A^*) \big) = \sup_{\nu \in \sigma(p(A,A^*))} \lvert \nu \rvert = \sup_{\lambda \in \sigma(A)} \big\lvert p(\lambda,\overline\lambda) \big\rvert,
$$

the last equality because the two sets over which the supremum is taken are equal.$$\blacksquare$$

### The Continuous Functional Calculus for a Normal Operator

With the norm identity in hand, extending $$p \mapsto p(A,A^*)$$ from polynomials to all continuous functions on $$\sigma(A)$$ is a routine density argument.

> **Theorem** *(Continuous Functional Calculus for a Normal Operator)*
<a name="thrm:continuous-functional-calculus-normal"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{crllr:norm-of-polynomial-in-a-astar} -->
<!--  \uses{lmm:polynomials-in-normal-are-normal} -->
<!--  \uses{../spectral-theorems/#thrm:stone–weierstrass-complex} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-linear-transformation-theorem} -->
<!--  \uses{lmm:spectrum-compact-general} -->
<!--  \uses{../spectral-theorems/#lmm:bounded-operators-form-a-banach-space} -->
<!--  \uses{../spectral-theorems/#lmm:lemma-2} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, with $$\mathbf{H} \ne \{0\}$$. There is a unique bounded linear map
>
> $$
>     \Phi_A : C^0\big( \sigma(A); \mathbb{C} \big) \longrightarrow \mathcal{B}(\mathbf{H})
> $$
>
> such that $$\Phi_A(p) = p(A,A^*)$$ for every polynomial $$p$$ in $$\lambda$$ and $$\overline\lambda$$. This map satisfies, for all $$f,g \in C^0(\sigma(A);\mathbb{C})$$ and $$\alpha,\beta \in \mathbb{C}$$:
>
> 1. $$\Phi_A(\alpha f + \beta g) = \alpha\Phi_A(f) + \beta\Phi_A(g)$$;
> 2. $$\Phi_A(fg) = \Phi_A(f)\Phi_A(g)$$;
> 3. $$\Phi_A(\overline{f}) = \Phi_A(f)^*$$;
> 4. $$\left\| \Phi_A(f) \right\| = \sup_{\lambda \in \sigma(A)} \lvert f(\lambda) \rvert$$, i.e. $$\Phi_A$$ is isometric;
> 5. $$\Phi_A(1) = \mathbf{1}$$ and $$\Phi_A(\iota) = A$$, where $$\iota(\lambda) = \lambda$$.
>
> In particular, if $$f$$ is real-valued on $$\sigma(A)$$ then $$\Phi_A(f)$$ is self-adjoint, and $$\Phi_A(f)$$ is normal for every $$f$$. We write $$f(A) \equiv \Phi_A(f)$$.

**Proof**
By [**Lemma** *(The Spectrum of a Bounded Operator is a Compact Metric Measurable Space)*](#lmm:spectrum-compact-general), $$\sigma(A)$$ is a compact metric space, so $$C^0(\sigma(A);\mathbb{C})$$ with the supremum norm is a normed vector space.

*The polynomials are dense.* Let $$\mathcal{P} \subset C^0(\sigma(A);\mathbb{C})$$ be the set of functions on $$\sigma(A)$$ of the form $$\lambda \mapsto p(\lambda,\overline\lambda)$$ for a polynomial $$p$$ in two variables. $$\mathcal{P}$$ is a subalgebra (products and linear combinations of such functions are again of this form), contains the constants (take $$p$$ constant), separates points of $$\sigma(A)$$ (the function $$\lambda\mapsto\lambda$$, i.e. $$p(\lambda,\overline\lambda)=\lambda$$, already does), and is closed under complex conjugation (the conjugate of $$p(\lambda,\overline\lambda)$$ is $$\overline{p}(\lambda,\overline\lambda)$$, again of the required form, with $$\overline p$$ as in [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal)). By the [**Complex Stone–Weierstrass Theorem**](../spectral-theorems/#thrm:stone–weierstrass-complex), $$\mathcal{P}$$ is dense in $$C^0(\sigma(A);\mathbb{C})$$.

*The map on polynomials is well defined and isometric.* Define $$\Phi_A^0 : \mathcal{P} \to \mathcal{B}(\mathbf{H})$$ by $$\Phi_A^0(p) = p(A,A^*)$$. This requires a check: two different polynomials $$p \ne q$$ (as formal expressions) may define the *same function* on $$\sigma(A)$$, and we need $$p(A,A^*) = q(A,A^*)$$ in that case. Indeed, if $$p$$ and $$q$$ agree as functions on $$\sigma(A)$$, then $$r \equiv p - q$$ vanishes identically on $$\sigma(A)$$, so by [**Corollary** *(Norm of a Polynomial in $$A$$ and $$A^*$$)*](#crllr:norm-of-polynomial-in-a-astar), $$\left\| r(A,A^*) \right\| = \sup_{\lambda\in\sigma(A)} \lvert r(\lambda,\overline\lambda) \rvert = 0$$, i.e. $$p(A,A^*) = q(A,A^*)$$. So $$\Phi_A^0$$ is well defined on $$\mathcal{P}$$, and the same corollary says exactly that it is isometric: $$\left\| \Phi_A^0(p) \right\| = \sup_{\lambda\in\sigma(A)}\lvert p(\lambda,\overline\lambda) \rvert = \left\| p \right\|_\infty$$. It is linear, since $$(\alpha p + \beta q)(A,A^*) = \alpha p(A,A^*) + \beta q(A,A^*)$$ directly from the definition of substitution.

*Extension.* $$\mathcal{P}$$ is a dense subspace of the normed space $$C^0(\sigma(A);\mathbb{C})$$, $$\mathcal{B}(\mathbf{H})$$ is a Banach space by [**Lemma** *(Bounded Operators form a Banach Space)*](../spectral-theorems/#lmm:bounded-operators-form-a-banach-space), and $$\Phi_A^0$$ is a bounded (indeed isometric, hence norm-$$1$$) linear map. By the [**Bounded Linear Transformation Theorem**](../spectral-theorems/#thrm:bounded-linear-transformation-theorem), $$\Phi_A^0$$ extends uniquely to a bounded linear map $$\Phi_A$$ on all of $$C^0(\sigma(A);\mathbb{C})$$, with the same norm; uniqueness of the extension is exactly the uniqueness claimed in the statement.

*The properties.* Property 1 is linearity, part of the extension. For properties 2, 3, and 4, each is an identity between continuous functions of $$f$$ (and $$g$$) that holds on the dense subspace $$\mathcal{P}$$ and whose two sides are continuous in $$f$$ (and $$g$$): for property 2, both $$(f,g)\mapsto\Phi_A(fg)$$ and $$(f,g)\mapsto\Phi_A(f)\Phi_A(g)$$ are continuous, the former because $$\left\| fg - f'g' \right\|_\infty \to 0$$ when $$f\to f'$$, $$g \to g'$$ uniformly (all functions being bounded on the compact $$\sigma(A)$$) and $$\Phi_A$$ is bounded, the latter by [submultiplicativity of the operator norm](../spectral-theorems/#lmm:lemma-2); on $$\mathcal{P}$$ the identity $$\Phi_A^0(pq) = \Phi_A^0(p)\Phi_A^0(q)$$ holds because substituting $$A$$ for $$\lambda$$ and $$A^*$$ for $$\overline\lambda$$ is multiplicative (the images commute, by [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal), which is what makes the substitution an algebra homomorphism). For property 3, $$f \mapsto \Phi_A(\overline f)$$ and $$f \mapsto \Phi_A(f)^*$$ are both continuous (the adjoint is isometric, so continuous), and agree on $$\mathcal{P}$$ by [**Lemma** *(Polynomials in a Normal Operator are Normal)*](#lmm:polynomials-in-normal-are-normal). Property 4 holds on $$\mathcal{P}$$ as shown, and both sides are continuous in $$f$$ (the left by boundedness of $$\Phi_A$$, the right because the supremum norm is continuous), so it holds throughout. Property 5 is immediate: the constant polynomial $$1$$ maps to $$\mathbf{1}$$ and $$p(\lambda,\overline\lambda)=\lambda$$ maps to $$A$$.

Finally, if $$f$$ is real-valued then $$\overline f = f$$, so property 3 gives $$\Phi_A(f)^* = \Phi_A(f)$$; and for general $$f$$, properties 2 and 3 give $$\Phi_A(f)\Phi_A(f)^* = \Phi_A(f\overline f) = \Phi_A(\overline f f) = \Phi_A(f)^*\Phi_A(f)$$, so $$\Phi_A(f)$$ is normal.$$\blacksquare$$

## From a Continuous Functional Calculus to a Projection-Valued Measure

We now carry out the second stage: manufacturing a projection-valued measure from a continuous functional calculus. As promised, we do this *abstractly* — the input is a compact metric space $$X$$ and an isometric $$*$$-homomorphism $$\Phi : C^0(X;\mathbb{C}) \to \mathcal{B}(\mathbf{H})$$, with no operator in sight — so that the bounded normal case below is an instance of a single statement rather than an appeal to the self-adjoint case's proof. The previous post's stage 2 is the same argument specialized to $$X = \sigma(A)$$ with $$A$$ bounded self-adjoint; we reproduce it here in the general setting.

Throughout this section, $$X$$ denotes a compact metric space, equipped with its Borel $$\sigma$$-algebra, so that "measurable" means "Borel-measurable"; this makes $$X$$ a compact metric measurable space in the sense used by the supporting lemmas of the previous post.

> **Convention** *(Standing Hypotheses for this Section)*
<a name="conv:section-abstract"></a>
> Throughout this section, $$X$$ denotes a compact metric space carrying its Borel $$\sigma$$-algebra, and — from [Definition (Abstract Continuous Functional Calculus)](#def:abstract-continuous-functional-calculus) onwards — $$\Phi$$ denotes an abstract continuous functional calculus on $$X$$, $$\mu_\psi$$ the measures it induces, and $$\widetilde\Phi$$ its extended calculus. Statements below that mention $$X$$, $$\Phi$$, $$\mu_\psi$$ or $$\widetilde\Phi$$ without introducing them are to be read as carrying these as hypotheses; a formalization should take them as parameters of the corresponding result.

> **Definition** *(Abstract Continuous Functional Calculus)*
<a name="def:abstract-continuous-functional-calculus"></a>
<!--  \uses{../spectral-theorems/#def:bounded-operator-notation} -->
<!--  \uses{thrm:continuous-functional-calculus-normal} -->
<!--  \uses{conv:section-abstract} -->
> Let $$X$$ be a compact metric space. An *abstract continuous functional calculus* on $$X$$ is a map $$\Phi : C^0(X;\mathbb{C}) \to \mathcal{B}(\mathbf{H})$$ satisfying, for all $$f,g \in C^0(X;\mathbb{C})$$ and $$\alpha,\beta\in\mathbb{C}$$:
>
> 1. $$\Phi(\alpha f + \beta g) = \alpha\Phi(f) + \beta\Phi(g)$$;
> 2. $$\Phi(fg) = \Phi(f)\Phi(g)$$;
> 3. $$\Phi(\overline f) = \Phi(f)^*$$;
> 4. $$\left\| \Phi(f) \right\| = \left\| f \right\|_\infty \equiv \sup_{x \in X}\lvert f(x) \rvert$$;
> 5. $$\Phi(1) = \mathbf{1}$$, where $$1$$ denotes the constant function with value $$1$$.

By [**Theorem** *(Continuous Functional Calculus for a Normal Operator)*](#thrm:continuous-functional-calculus-normal), a normal $$A \in \mathcal{B}(\mathbf{H})$$ with $$\mathbf{H}\ne\{0\}$$ supplies an abstract continuous functional calculus on $$X = \sigma(A)$$ — properties 1–5 there are literally properties 1–5 here.

Our first observation is that such a $$\Phi$$ takes non-negative functions to non-negative operators; this is what will let us feed it into the Riesz representation theorem.

> **Lemma** *(An Abstract Calculus is Non-Negative)*
<a name="lmm:abstract-calculus-non-negative"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{../spectral-theorems/#def:non-negative-operator} -->
<!--  \uses{def:hall-9.1} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$.
>
> 1. If $$f \in C^0(X;\mathbb{C})$$ is real-valued, then $$\Phi(f)$$ is self-adjoint, and $$\left< \psi, \Phi(f)\psi \right> \in \mathbb{R}$$ for every $$\psi \in \mathbf{H}$$.
> 2. If $$f \in C^0(X;\mathbb{C})$$ satisfies $$f(x) \ge 0$$ for all $$x \in X$$, then $$\left< \psi, \Phi(f)\psi \right> \ge 0$$ for every $$\psi \in \mathbf{H}$$.

**Proof**
**Part 1.** If $$f$$ is real-valued then $$\overline f = f$$, so property 3 gives $$\Phi(f)^* = \Phi(\overline f) = \Phi(f)$$. For self-adjoint $$T$$ and any $$\psi$$, $$\left< \psi, T\psi \right> = \left< T^*\psi, \psi \right> = \left< T\psi,\psi \right> = \overline{\left< \psi, T\psi \right>}$$, using the [definition of the adjoint](#def:hall-9.1) and conjugate symmetry; a complex number equal to its own conjugate is real.

**Part 2.** Let $$g \equiv \sqrt{f}$$, meaning $$g(x) = \sqrt{f(x)}$$ — well defined since $$f(x)\ge 0$$, real-valued, and continuous, since the square root is continuous on $$[0,\infty)$$ and $$f$$ is continuous. Then $$g^2 = f$$ pointwise, so by property 2, $$\Phi(f) = \Phi(g)\Phi(g)$$; and by **Part 1**, $$\Phi(g)^* = \Phi(g)$$. Hence, for any $$\psi \in \mathbf{H}$$,

$$
    \left< \psi, \Phi(f)\psi \right> = \left< \psi, \Phi(g)^*\Phi(g)\psi \right> = \left< \Phi(g)\psi, \Phi(g)\psi \right> = \left\| \Phi(g)\psi \right\|^2 \ge 0,
$$

using the [definition of the adjoint](#def:hall-9.1) for the middle equality.$$\blacksquare$$

Non-negativity is exactly the hypothesis of the Riesz representation theorem, which now produces, for each vector $$\psi$$, a measure on $$X$$.

> **Definition** *(The Measures Associated to an Abstract Calculus)*
<a name="def:abstract-associated-measures"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{lmm:abstract-calculus-non-negative} -->
<!--  \uses{../spectral-theorems/#thrm:riesz-representation} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$ and let $$\psi \in \mathbf{H}$$. Define $$\Lambda_\psi : C^0(X;\mathbb{R}) \to \mathbb{R}$$ by
>
> $$
>     \Lambda_\psi(f) \equiv \left< \psi, \Phi(f)\psi \right>.
> $$
>
> By Part 1 of [**Lemma** *(An Abstract Calculus is Non-Negative)*](#lmm:abstract-calculus-non-negative) this is real-valued; it is linear, by property 1 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus) together with linearity of the inner product in its second argument; and it is non-negative on non-negative $$f$$, by Part 2 of the same lemma. Since $$X$$ is a compact metric space, the [**Riesz Representation Theorem**](../spectral-theorems/#thrm:riesz-representation) therefore supplies a unique positive measure $$\mu_\psi$$ on the Borel $$\sigma$$-algebra of $$X$$ with
>
> $$
>     \left< \psi, \Phi(f)\psi \right> = \Lambda_\psi(f) = \int_X f \, d\mu_\psi \qquad \text{for all } f \in C^0(X;\mathbb{R}).
> $$
>
> We call $$\mu_\psi$$ the *measure associated to $$\psi$$* (relative to $$\Phi$$).

> **Lemma** *(The Abstract Associated Measures are Finite)*
<a name="lmm:abstract-associated-measures-finite"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-associated-measures} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with associated measures $$\mu_\psi$$. For every $$\psi \in \mathbf{H}$$, $$\mu_\psi(X) = \left\| \psi \right\|^2 < \infty$$. In particular $$\mu_\psi$$ is a finite measure.

**Proof**
Apply the defining property of $$\mu_\psi$$ to the constant function $$1 \in C^0(X;\mathbb{R})$$, and use property 5 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus):

$$
    \mu_\psi(X) = \int_X 1 \, d\mu_\psi = \left< \psi, \Phi(1)\psi \right> = \left< \psi, \mathbf{1}\psi \right> = \left< \psi,\psi \right> = \left\| \psi \right\|^2,
$$

which is finite since $$\psi \in \mathbf{H}$$.$$\blacksquare$$

The point of introducing the measures $$\mu_\psi$$ is that the right-hand side $$\int_X f \, d\mu_\psi$$ continues to make sense for *bounded measurable* $$f$$, well beyond the continuous functions on which $$\Phi$$ was defined. The next proposition shows that the resulting map of $$\psi$$ is always a bounded quadratic form, which is what lets us convert it back into an operator.

> **Proposition** *(The Extended Forms are Bounded Quadratic Forms)*
<a name="prpstn:abstract-extended-forms-are-bounded"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-associated-measures} -->
<!--  \uses{lmm:abstract-associated-measures-finite} -->
<!--  \uses{../spectral-theorems/#def:bounded-quadratic-form} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.62} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-convergence-theorem} -->
<!--  \uses{../spectral-theorems/#lmm:hall-prblm-8.3.3c} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.61} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$. For a bounded measurable $$f : X \to \mathbb{C}$$, define $$Q_f : \mathbf{H} \to \mathbb{C}$$ by
>
> $$
>     Q_f(\psi) \equiv \int_X f \, d\mu_\psi.
> $$
>
> Then $$Q_f$$ is a bounded quadratic form on $$\mathbf{H}$$, with $$\lvert Q_f(\psi) \rvert \le \left\| f \right\|_\infty \left\| \psi \right\|^2$$. Moreover $$Q_f(\psi) = \left< \psi, \Phi(f)\psi \right>$$ whenever $$f$$ is continuous.

**Proof**
Let $$\mathcal{F}$$ be the set of bounded measurable complex-valued $$f$$ on $$X$$ for which $$Q_f$$ is a bounded quadratic form. We verify the three hypotheses of [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c), which will then give that $$\mathcal{F}$$ is everything.

*$$\mathcal{F}$$ contains $$C^0(X;\mathbb{R})$$.* Let $$f \in C^0(X;\mathbb{R})$$. By the defining property of $$\mu_\psi$$ in [Definition (The Measures Associated to an Abstract Calculus)](#def:abstract-associated-measures), $$Q_f(\psi) = \int_X f \, d\mu_\psi = \left< \psi, \Phi(f)\psi \right>$$ for every $$\psi$$. So $$Q_f$$ is the quadratic form induced by the bounded operator $$\Phi(f)$$, which is a bounded quadratic form by [**Proposition** *(hall-a.62)*](../spectral-theorems/#prpstn:hall-a.62), with bound $$\left\| \Phi(f) \right\| = \left\| f \right\|_\infty$$ by property 4 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus). (The same computation, applied to a general continuous complex-valued $$f$$ by splitting into real and imaginary parts and using linearity of both $$\Phi$$ and the integral, gives the final claim of the proposition.)

*$$\mathcal{F}$$ is a complex vector space.* Let $$f,g \in \mathcal{F}$$ and $$\alpha,\beta\in\mathbb{C}$$. By linearity of the integral in the integrand, $$Q_{\alpha f + \beta g}(\psi) = \alpha Q_f(\psi) + \beta Q_g(\psi)$$ for every $$\psi$$. Property 1 of a quadratic form is preserved: $$Q_{\alpha f+\beta g}(\lambda\psi) = \alpha Q_f(\lambda\psi) + \beta Q_g(\lambda\psi) = \lvert \lambda \rvert^2\big( \alpha Q_f(\psi) + \beta Q_g(\psi) \big) = \lvert\lambda\rvert^2 Q_{\alpha f+\beta g}(\psi)$$. For property 2, the polarization formula is linear in the quadratic form, so the form associated to $$Q_{\alpha f + \beta g}$$ is $$\alpha L_f + \beta L_g$$, a linear combination of sesquilinear forms and hence sesquilinear. Boundedness likewise passes to linear combinations. So $$\alpha f + \beta g \in \mathcal{F}$$.

*$$\mathcal{F}$$ is closed under uniformly bounded pointwise limits.* Let $$\{f_i\}$$ be a sequence in $$\mathcal{F}$$ with $$\lvert f_i \rvert \le M$$ for all $$i$$ and $$f_i \to f$$ pointwise on $$X$$; $$f$$ is then bounded (by $$M$$) and measurable. Fix $$\psi$$. Since $$\mu_\psi$$ is a finite measure by [**Lemma** *(The Abstract Associated Measures are Finite)*](#lmm:abstract-associated-measures-finite), the [**Bounded Convergence Theorem**](../spectral-theorems/#thrm:bounded-convergence-theorem) applies and gives

$$
    Q_{f_i}(\psi) = \int_X f_i \, d\mu_\psi \longrightarrow \int_X f \, d\mu_\psi = Q_f(\psi).
$$

Property 1 passes to the limit: $$Q_f(\lambda\psi) = \lim_i Q_{f_i}(\lambda\psi) = \lim_i \lvert\lambda\rvert^2 Q_{f_i}(\psi) = \lvert\lambda\rvert^2 Q_f(\psi)$$. For property 2, the polarization formula expresses $$L_f(\phi,\psi)$$ as a fixed finite linear combination of values of $$Q_f$$, each of which is the limit of the corresponding values of $$Q_{f_i}$$; so $$L_{f_i}(\phi,\psi) \to L_f(\phi,\psi)$$ for all $$\phi,\psi$$, and each defining identity of sesquilinearity, holding for every $$f_i$$, passes to the limit. For boundedness, $$\lvert Q_f(\psi) \rvert = \lvert \int_X f \, d\mu_\psi \rvert \le M\mu_\psi(X) = M\left\| \psi \right\|^2$$, again by [**Lemma** *(The Abstract Associated Measures are Finite)*](#lmm:abstract-associated-measures-finite). So $$f \in \mathcal{F}$$.

By [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c), $$\mathcal{F}$$ consists of all bounded Borel-measurable functions on $$X$$. Finally, the stated bound holds for every bounded measurable $$f$$: $$\lvert Q_f(\psi) \rvert \le \int_X \lvert f \rvert \, d\mu_\psi \le \left\| f \right\|_\infty \mu_\psi(X) = \left\| f \right\|_\infty\left\| \psi \right\|^2$$.$$\blacksquare$$

With the forms in hand, converting them back to operators is immediate, and defines the extension of $$\Phi$$ to bounded measurable functions.

> **Definition** *(The Extended Calculus)*
<a name="def:abstract-extended-calculus"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{prpstn:abstract-extended-forms-are-bounded} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$ and let $$f : X \to \mathbb{C}$$ be bounded and measurable. By [**Proposition** *(The Extended Forms are Bounded Quadratic Forms)*](#prpstn:abstract-extended-forms-are-bounded), $$Q_f$$ is a bounded quadratic form, so by [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63) there is a unique $$\widetilde\Phi(f) \in \mathcal{B}(\mathbf{H})$$ with
>
> $$
>     \left< \psi, \widetilde\Phi(f)\psi \right> = Q_f(\psi) = \int_X f \, d\mu_\psi \qquad \text{for all } \psi \in \mathbf{H}.
> $$
>
> We call $$\widetilde\Phi$$ the *extended calculus*. By the final claim of that proposition, $$\widetilde\Phi(f) = \Phi(f)$$ for continuous $$f$$ — by uniqueness in [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63), since $$\Phi(f)$$ then induces the same quadratic form — so $$\widetilde\Phi$$ genuinely extends $$\Phi$$.

Before going further we record that $$\widetilde\Phi$$ is linear — used repeatedly below, and not automatic from the definition, which specifies $$\widetilde\Phi(f)$$ only one function at a time.

> **Lemma** *(The Extended Calculus is Linear)*
<a name="lmm:abstract-extended-linear"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{prpstn:abstract-extended-forms-are-bounded} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
<!--  \uses{../spectral-theorems/#prpstn:basic-integral-properties} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. For all bounded measurable $$f,g : X \to \mathbb{C}$$ and $$\alpha,\beta \in \mathbb{C}$$,
>
> $$
>     \widetilde\Phi(\alpha f + \beta g) = \alpha\widetilde\Phi(f) + \beta\widetilde\Phi(g).
> $$

**Proof**
The function $$\alpha f + \beta g$$ is again bounded and measurable, so $$\widetilde\Phi(\alpha f + \beta g)$$ is defined. For every $$\psi \in \mathbf{H}$$, linearity of the integral in the integrand gives

$$
    Q_{\alpha f+\beta g}(\psi) = \int_X (\alpha f + \beta g) \, d\mu_\psi = \alpha\int_X f\,d\mu_\psi + \beta\int_X g\,d\mu_\psi = \alpha Q_f(\psi) + \beta Q_g(\psi),
$$

and, by [Definition (The Extended Calculus)](#def:abstract-extended-calculus) applied to $$f$$ and to $$g$$ together with linearity of the inner product in its second argument, this equals $$\left< \psi, \big(\alpha\widetilde\Phi(f) + \beta\widetilde\Phi(g)\big)\psi \right>$$. So the bounded operator $$\alpha\widetilde\Phi(f)+\beta\widetilde\Phi(g)$$ induces the quadratic form $$Q_{\alpha f + \beta g}$$; since $$\widetilde\Phi(\alpha f+\beta g)$$ is by definition the *unique* bounded operator doing so — uniqueness being part of [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63) — the two coincide.$$\blacksquare$$

We isolate two facts about $$\widetilde\Phi$$ that the rest of this section uses repeatedly: an off-diagonal formula, and a continuity property under bounded pointwise limits of the integrand.

> **Lemma** *(Off-Diagonal Formula and Bounded Convergence for the Extended Calculus)*
<a name="lmm:abstract-extended-convergence"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{prpstn:abstract-extended-forms-are-bounded} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
<!--  \uses{lmm:abstract-associated-measures-finite} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-convergence-theorem} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. For bounded measurable $$h$$ let $$L_h$$ denote the sesquilinear form associated to $$Q_h$$. Then:
>
> 1. *(Off-diagonal formula.)* $$L_h(\phi,\psi) = \left< \phi, \widetilde\Phi(h)\psi \right>$$ for all $$\phi,\psi \in \mathbf{H}$$.
> 2. *(Convergence principle.)* If $$\{h_i\}$$ are bounded measurable with $$\lvert h_i \rvert \le M$$ for all $$i$$ and $$h_i \to h$$ pointwise on $$X$$, then
>
>    $$
>        \left< \phi, \widetilde\Phi(h_i)\psi \right> \longrightarrow \left< \phi, \widetilde\Phi(h)\psi \right> \qquad \text{for all } \phi,\psi \in \mathbf{H}.
>    $$

**Proof**
**Part 1.** Apply Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) with $$D = \mathbf{H}$$ and $$T = \widetilde\Phi(h)$$. Its hypotheses hold: $$Q_h$$ is a quadratic form on $$\mathbf{H}$$ by [**Proposition** *(The Extended Forms are Bounded Quadratic Forms)*](#prpstn:abstract-extended-forms-are-bounded), $$\widetilde\Phi(h)$$ is linear, and it induces $$Q_h$$ on the diagonal by [Definition (The Extended Calculus)](#def:abstract-extended-calculus).

**Part 2.** For each fixed $$\xi \in \mathbf{H}$$, the measure $$\mu_\xi$$ is finite by [**Lemma** *(The Abstract Associated Measures are Finite)*](#lmm:abstract-associated-measures-finite), so the [**Bounded Convergence Theorem**](../spectral-theorems/#thrm:bounded-convergence-theorem) gives

$$
    Q_{h_i}(\xi) = \int_X h_i \, d\mu_\xi \longrightarrow \int_X h \, d\mu_\xi = Q_h(\xi).
$$

By property 2 of the [definition of a quadratic form on a subspace](#def:hall-quadratic-form-on-a-subspace), $$L_{h_i}(\phi,\psi)$$ is a fixed finite linear combination of the five values $$Q_{h_i}(\phi+\psi)$$, $$Q_{h_i}(\phi)$$, $$Q_{h_i}(\psi)$$, $$Q_{h_i}(\phi+i\psi)$$, $$Q_{h_i}(i\psi)$$ — the same combination for every $$i$$, the polarization formula not depending on the function. Each of those five converges to the corresponding value for $$h$$ by the previous display, so $$L_{h_i}(\phi,\psi) \to L_h(\phi,\psi)$$. Combining with **Part 1** applied to each $$h_i$$ and to $$h$$ gives the claim.$$\blacksquare$$

The extended calculus inherits the algebraic properties of $$\Phi$$. Multiplicativity is the substantial one, and is proved in two passes of the same "vector space, contains the continuous functions, closed under bounded pointwise limits" argument — first fixing a continuous second factor, then letting both factors be measurable.

> **Lemma** *(Real Functions Give Self-Adjoint Operators)*
<a name="lmm:abstract-extended-real-self-adjoint"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$, and let $$f : X \to \mathbb{C}$$ be bounded, measurable, and real-valued. Then $$\widetilde\Phi(f)$$ is self-adjoint.

**Proof**
Since $$f$$ is real-valued and each $$\mu_\psi$$ is a positive real measure, $$Q_f(\psi) = \int_X f\,d\mu_\psi \in \mathbb{R}$$ for every $$\psi$$. By the second clause of [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63) — a bounded quadratic form taking only real values corresponds to a self-adjoint operator — $$\widetilde\Phi(f)$$ is self-adjoint.$$\blacksquare$$

> **Proposition** *(The Extended Calculus is Multiplicative)*
<a name="prpstn:abstract-extended-multiplicative"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{prpstn:abstract-extended-forms-are-bounded} -->
<!--  \uses{lmm:abstract-associated-measures-finite} -->
<!--  \uses{../spectral-theorems/#lmm:hall-prblm-8.3.3c} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-convergence-theorem} -->
<!--  \uses{def:hall-quadratic-form-on-a-subspace} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{lmm:abstract-extended-linear} -->
<!--  \uses{def:hall-9.1} -->
<!--  \uses{lmm:abstract-extended-convergence} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. For all bounded measurable $$f,g : X \to \mathbb{C}$$,
>
> $$
>     \widetilde\Phi(fg) = \widetilde\Phi(f)\widetilde\Phi(g).
> $$

**Proof**
Throughout we use [**Lemma** *(Off-Diagonal Formula and Bounded Convergence for the Extended Calculus)*](#lmm:abstract-extended-convergence); we refer to its Part 2 as the *convergence principle*.

**Pass 1: $$g$$ continuous.** Fix $$g \in C^0(X;\mathbb{R})$$ and let $$\mathcal{F}_1$$ be the set of bounded measurable $$f$$ with $$\widetilde\Phi(fg) = \widetilde\Phi(f)\widetilde\Phi(g)$$. We check the three hypotheses of [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c).

$$\mathcal{F}_1$$ *is a vector space*: for $$f_1,f_2 \in \mathcal{F}_1$$ and $$\alpha_1,\alpha_2 \in \mathbb{C}$$, using that $$(\alpha_1f_1+\alpha_2f_2)g = \alpha_1(f_1g)+\alpha_2(f_2g)$$ pointwise and [**Lemma** *(The Extended Calculus is Linear)*](#lmm:abstract-extended-linear),

$$
    \widetilde\Phi\big((\alpha_1f_1+\alpha_2f_2)g\big) = \alpha_1\widetilde\Phi(f_1g)+\alpha_2\widetilde\Phi(f_2g) = \big(\alpha_1\widetilde\Phi(f_1)+\alpha_2\widetilde\Phi(f_2)\big)\widetilde\Phi(g) = \widetilde\Phi(\alpha_1f_1+\alpha_2f_2)\widetilde\Phi(g).
$$

$$\mathcal{F}_1 \supset C^0(X;\mathbb{R})$$: for continuous $$f$$, $$fg$$ is continuous, and $$\widetilde\Phi$$ agrees with $$\Phi$$ on continuous functions ([Definition (The Extended Calculus)](#def:abstract-extended-calculus)), so the claim reduces to $$\Phi(fg) = \Phi(f)\Phi(g)$$, which is property 2 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus).

$$\mathcal{F}_1$$ *is closed under bounded pointwise limits*: let $$f_i \to f$$ pointwise with $$\lvert f_i \rvert \le M$$, all $$f_i \in \mathcal{F}_1$$. Then $$f_ig \to fg$$ pointwise with $$\lvert f_ig \rvert \le M\left\| g \right\|_\infty$$, so by the convergence principle, for all $$\phi,\psi$$,

$$
    \left< \phi, \widetilde\Phi(fg)\psi \right> = \lim_i \left< \phi, \widetilde\Phi(f_ig)\psi \right> = \lim_i \left< \phi, \widetilde\Phi(f_i)\widetilde\Phi(g)\psi \right> = \left< \phi, \widetilde\Phi(f)\widetilde\Phi(g)\psi \right>,
$$

the last step being the convergence principle applied with the fixed vector $$\widetilde\Phi(g)\psi$$ in place of $$\psi$$. By [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) with $$D = \mathbf{H}$$, $$\widetilde\Phi(fg)\psi = \widetilde\Phi(f)\widetilde\Phi(g)\psi$$ for every $$\psi$$, i.e. $$f \in \mathcal{F}_1$$.

By [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c), $$\mathcal{F}_1$$ contains every bounded measurable $$f$$. So $$\widetilde\Phi(fg) = \widetilde\Phi(f)\widetilde\Phi(g)$$ whenever $$f$$ is bounded measurable and $$g \in C^0(X;\mathbb{R})$$.

**Pass 2: $$g$$ measurable.** Fix a bounded measurable $$f$$ and let $$\mathcal{F}_2$$ be the set of bounded measurable $$g$$ with $$\widetilde\Phi(fg) = \widetilde\Phi(f)\widetilde\Phi(g)$$. That $$\mathcal{F}_2$$ is a vector space follows exactly as for $$\mathcal{F}_1$$; that $$\mathcal{F}_2 \supset C^0(X;\mathbb{R})$$ is precisely the conclusion of **Pass 1**; and closure under bounded pointwise limits follows by the same convergence-principle argument, with the roles of the two factors exchanged. Let $$g_i \to g$$ boundedly pointwise with each $$g_i \in \mathcal{F}_2$$, and fix $$\phi,\psi \in \mathbf{H}$$. Since $$\lvert g_i \rvert \le M$$ implies $$\lvert fg_i \rvert \le M\left\| f \right\|_\infty$$, and $$fg_i \to fg$$ pointwise, the convergence principle gives

$$
    \left< \phi, \widetilde\Phi(fg)\psi \right> = \lim_{i\to\infty} \left< \phi, \widetilde\Phi(fg_i)\psi \right> = \lim_{i\to\infty} \left< \phi, \widetilde\Phi(f)\widetilde\Phi(g_i)\psi \right>,
$$

the second equality because $$g_i \in \mathcal{F}_2$$. On the other hand, by the [definition of the adjoint](#def:hall-9.1) and the convergence principle applied with the fixed vector $$\widetilde\Phi(f)^*\phi$$ in the first slot,

$$
    \left< \phi, \widetilde\Phi(f)\widetilde\Phi(g_i)\psi \right> = \left< \widetilde\Phi(f)^*\phi, \widetilde\Phi(g_i)\psi \right> \longrightarrow \left< \widetilde\Phi(f)^*\phi, \widetilde\Phi(g)\psi \right> = \left< \phi, \widetilde\Phi(f)\widetilde\Phi(g)\psi \right>.
$$

By uniqueness of limits, $$\left< \phi, \widetilde\Phi(fg)\psi \right> = \left< \phi, \widetilde\Phi(f)\widetilde\Phi(g)\psi \right>$$ for all $$\phi,\psi \in \mathbf{H}$$; fixing $$\psi$$ and applying [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) with $$D = \mathbf{H}$$ gives $$\widetilde\Phi(fg)\psi = \widetilde\Phi(f)\widetilde\Phi(g)\psi$$ for every $$\psi$$, i.e. $$g \in \mathcal{F}_2$$. Again [**Lemma** *(hall-prblm-8.3.3c)*](../spectral-theorems/#lmm:hall-prblm-8.3.3c) gives $$\mathcal{F}_2$$ everything, which is the proposition.$$\blacksquare$$

> **Lemma** *(The Extended Calculus Respects Conjugation)*
<a name="lmm:abstract-extended-conjugation"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{lmm:abstract-extended-real-self-adjoint} -->
<!--  \uses{lmm:abstract-extended-linear} -->
<!--  \uses{../spectral-theorems/#thrm:hall-8.10} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. For every bounded measurable $$f : X \to \mathbb{C}$$, $$\widetilde\Phi(\overline f) = \widetilde\Phi(f)^*$$.

**Proof**
Write $$f = u + iv$$ with $$u = \tfrac{1}{2}(f+\overline f)$$ and $$v = \tfrac{1}{2i}(f - \overline f)$$ bounded, measurable, and real-valued. By [**Lemma** *(Real Functions Give Self-Adjoint Operators)*](#lmm:abstract-extended-real-self-adjoint), $$\widetilde\Phi(u)$$ and $$\widetilde\Phi(v)$$ are self-adjoint. By [**Lemma** *(The Extended Calculus is Linear)*](#lmm:abstract-extended-linear) and conjugate-linearity of the adjoint,

$$
    \widetilde\Phi(f)^* = \big( \widetilde\Phi(u) + i\widetilde\Phi(v) \big)^* = \widetilde\Phi(u)^* - i\widetilde\Phi(v)^* = \widetilde\Phi(u) - i\widetilde\Phi(v) = \widetilde\Phi(u - iv) = \widetilde\Phi(\overline f).\ \blacksquare
$$

We can now assemble the projection-valued measure. This is the abstract form of the previous post's [**Theorem** *(hall-8.10)*](../spectral-theorems/#thrm:hall-8.10).

> **Theorem** *(A Continuous Functional Calculus Yields a Projection-Valued Measure)*
<a name="thrm:abstract-calculus-yields-pvm"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{lmm:abstract-extended-convergence} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
<!--  \uses{../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{prpstn:abstract-extended-multiplicative} -->
<!--  \uses{lmm:abstract-extended-real-self-adjoint} -->
<!--  \uses{lmm:abstract-extended-conjugation} -->
<!--  \uses{lmm:abstract-associated-measures-finite} -->
<!--  \uses{prpstn:abstract-extended-forms-are-bounded} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#def:bounded-orthogonal-projection} -->
<!--  \uses{../spectral-theorems/#lmm:lemma-4} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{lmm:abstract-extended-linear} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
> Let $$X$$ be a compact metric space and $$\Phi$$ an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. Define, for each Borel set $$E \subset X$$,
>
> $$
>     \mu^\Phi(E) \equiv \widetilde\Phi(1_E).
> $$
>
> Then $$\mu^\Phi$$ is a projection-valued measure on $$X$$, and for every *bounded measurable* $$f$$ on $$X$$,
>
> $$
>     \int_X f \, d\mu^\Phi = \widetilde\Phi(f);
> $$
>
> in particular, for $$f \in C^0(X;\mathbb{C})$$, $$\int_X f \, d\mu^\Phi = \Phi(f)$$.

**Proof**
We verify the four properties of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) in turn, then the integral formula.

**Property 1: each $$\mu^\Phi(E)$$ is a bounded orthogonal projection.** $$\widetilde\Phi(1_E) \in \mathcal{B}(\mathbf{H})$$ by construction. Idempotency: $$1_E \cdot 1_E = 1_E$$ pointwise, so by [**Proposition** *(The Extended Calculus is Multiplicative)*](#prpstn:abstract-extended-multiplicative), $$\mu^\Phi(E)^2 = \widetilde\Phi(1_E)\widetilde\Phi(1_E) = \widetilde\Phi(1_E \cdot 1_E) = \widetilde\Phi(1_E) = \mu^\Phi(E)$$. Self-adjointness: $$1_E$$ is real-valued, so [**Lemma** *(Real Functions Give Self-Adjoint Operators)*](#lmm:abstract-extended-real-self-adjoint) applies. So $$\mu^\Phi(E)$$ is a [bounded orthogonal projection](../spectral-theorems/#def:bounded-orthogonal-projection).

**Property 2: $$\mu^\Phi(\emptyset) = 0$$ and $$\mu^\Phi(X) = \mathbf{1}$$.** We have $$1_\emptyset = 0$$, the zero function, and $$Q_0(\psi) = \int_X 0 \, d\mu_\psi = 0$$ for every $$\psi$$, so by uniqueness in [Definition (The Extended Calculus)](#def:abstract-extended-calculus), $$\widetilde\Phi(0) = 0$$. And $$1_X = 1$$, the constant function, which is continuous, so $$\widetilde\Phi(1_X) = \Phi(1) = \mathbf{1}$$ by property 5 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus).

**Property 4: $$\mu^\Phi(E_1 \cap E_2) = \mu^\Phi(E_1)\mu^\Phi(E_2)$$.** Immediate from multiplicativity, since $$1_{E_1 \cap E_2} = 1_{E_1}1_{E_2}$$ pointwise: $$\mu^\Phi(E_1\cap E_2) = \widetilde\Phi(1_{E_1}1_{E_2}) = \widetilde\Phi(1_{E_1})\widetilde\Phi(1_{E_2}) = \mu^\Phi(E_1)\mu^\Phi(E_2)$$.

**Property 3: countable additivity.** Let $$\{E_j\}_{j\in\mathbb{N}}$$ be pairwise disjoint Borel sets and $$E \equiv \bigcup_j E_j$$. By **Property 4** and disjointness, $$\mu^\Phi(E_i)\mu^\Phi(E_j) = \mu^\Phi(E_i\cap E_j) = \mu^\Phi(\emptyset) = 0$$ for $$i \ne j$$, so $$\{\mu^\Phi(E_j)\}$$ is a family of pairwise orthogonal bounded projections. By [**Lemma** *(lemma-4)*](../spectral-theorems/#lmm:lemma-4) — whose partial sums are indexed from $$0$$, so we apply it to the reindexed family $$P_i \equiv \mu^\Phi(E_{i+1})$$, still pairwise orthogonal — for each $$\psi$$ the partial sums $$\sum_{j=1}^n \mu^\Phi(E_j)\psi$$ converge in norm to $$P\psi$$, where $$P$$ is the orthogonal projection onto the smallest closed subspace containing all the ranges. It remains to identify $$P$$ with $$\mu^\Phi(E)$$.

Set $$h_n \equiv \sum_{j=1}^n 1_{E_j} = 1_{\bigcup_{j\le n}E_j}$$ (the equality by disjointness). Then $$h_n \to 1_E$$ pointwise on $$X$$ — for $$x \in E$$, $$x$$ lies in exactly one $$E_j$$, so $$h_n(x) = 1$$ for $$n \ge j$$; for $$x \notin E$$, $$h_n(x)=0$$ for all $$n$$ — and $$\lvert h_n \rvert \le 1$$. By Part 2 of [**Lemma** *(Off-Diagonal Formula and Bounded Convergence for the Extended Calculus)*](#lmm:abstract-extended-convergence), for all $$\phi,\psi \in \mathbf{H}$$,

$$
    \left< \phi, \widetilde\Phi(h_n)\psi \right> \longrightarrow \left< \phi, \widetilde\Phi(1_E)\psi \right> = \left< \phi, \mu^\Phi(E)\psi \right>.
$$

On the other hand $$\widetilde\Phi(h_n) = \sum_{j=1}^n \mu^\Phi(E_j)$$ by [**Lemma** *(The Extended Calculus is Linear)*](#lmm:abstract-extended-linear), and $$\sum_{j=1}^n\mu^\Phi(E_j)\psi \to P\psi$$ in norm, so by [continuity of the inner product](../spectral-theorems/#prpstn:continuity-of-norm-and-inner-product), $$\left< \phi, \widetilde\Phi(h_n)\psi \right> \to \left< \phi, P\psi \right>$$. By uniqueness of limits in $$\mathbb{C}$$, $$\left< \phi, \mu^\Phi(E)\psi \right> = \left< \phi, P\psi \right>$$ for all $$\phi,\psi$$; by [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) with $$D=\mathbf{H}$$, $$\mu^\Phi(E)\psi = P\psi$$ for every $$\psi$$. Hence $$\mu^\Phi(E)\psi = \lim_n \sum_{j=1}^n \mu^\Phi(E_j)\psi = \sum_{j=1}^\infty \mu^\Phi(E_j)\psi$$, which is Property 3.

**The integral formula.** By the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) applied to the projection-valued measure $$\mu^\Phi$$ just constructed, $$\int_X f\,d\mu^\Phi$$ is the unique bounded operator with $$\left< \psi, \left( \int_X f\,d\mu^\Phi \right)\psi \right> = \int_X f \, d\mu^\Phi_\psi$$ for all $$\psi$$, where $$\mu^\Phi_\psi(E) = \left< \psi, \mu^\Phi(E)\psi \right>$$. Now for any Borel $$E$$,

$$
    \mu^\Phi_\psi(E) = \left< \psi, \widetilde\Phi(1_E)\psi \right> = Q_{1_E}(\psi) = \int_X 1_E \, d\mu_\psi = \mu_\psi(E),
$$

using [Definition (The Extended Calculus)](#def:abstract-extended-calculus). So $$\mu^\Phi_\psi = \mu_\psi$$ as measures. Therefore, for *any* bounded measurable $$f$$,

$$
    \left< \psi, \left( \int_X f \, d\mu^\Phi \right)\psi \right> = \int_X f \, d\mu^\Phi_\psi = \int_X f \, d\mu_\psi = Q_f(\psi) = \left< \psi, \widetilde\Phi(f)\psi \right>,
$$

the last equality being [Definition (The Extended Calculus)](#def:abstract-extended-calculus). Two bounded operators inducing the same quadratic form are equal, by uniqueness in [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63); hence $$\int_X f \, d\mu^\Phi = \widetilde\Phi(f)$$. When $$f$$ is continuous, $$\widetilde\Phi(f) = \Phi(f)$$ (the final clause of [Definition (The Extended Calculus)](#def:abstract-extended-calculus)), giving the stated special case.$$\blacksquare$$

The extended calculus is norm-bounded by the supremum norm. This is *not* supplied by [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63), which yields existence, uniqueness and (for real forms) self-adjointness but no norm estimate; it comes instead from the identification just proved.

> **Corollary** *(The Extended Calculus is Norm-Bounded)*
<a name="crllr:abstract-extended-norm-bound"></a>
<!--  \uses{conv:section-abstract} -->
<!--  \uses{thrm:abstract-calculus-yields-pvm} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
> Let $$\Phi$$ be an abstract continuous functional calculus on $$X$$, with extended calculus $$\widetilde\Phi$$. Then for every bounded measurable $$f : X \to \mathbb{C}$$,
>
> $$
>     \left\| \widetilde\Phi(f) \right\| \le \left\| f \right\|_\infty.
> $$

**Proof**
By [**Theorem** *(A Continuous Functional Calculus Yields a Projection-Valued Measure)*](#thrm:abstract-calculus-yields-pvm), $$\widetilde\Phi(f) = \int_X f \, d\mu^\Phi$$ for every bounded measurable $$f$$. Property 2 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) bounds the operator norm of that integral by the supremum norm of the integrand, giving the claim.$$\blacksquare$$

### The Spectral Theorem for Bounded Normal Operators

Assembling the two stages gives the result this section was aiming at.

> **Theorem** *(Spectral Theorem for Bounded Normal Operators)*
<a name="thrm:hall-10.20"></a>
<!--  \uses{def:hall-10.19} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{../spectral-theorems/#thrm:riesz-representation} -->
<!--  \uses{../spectral-theorems/#thrm:stone–weierstrass-complex} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
<!--  \uses{lmm:polynomials-in-normal-are-normal} -->
<!--  \uses{thrm:continuous-functional-calculus-normal} -->
<!--  \uses{thrm:abstract-calculus-yields-pvm} -->
<!--  \uses{def:abstract-continuous-functional-calculus} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{lmm:spectrum-compact-general} -->
> Let $$A \in \mathcal{B}(\mathbf{H})$$ be normal, with $$\mathbf{H} \ne \{0\}$$. Then there is a *unique* projection-valued measure $$\mu^A$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$ with
>
> $$
>     \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = A.
> $$
>
> Uniqueness holds in the following stronger, *ambient* form, which is the one applied in [**Theorem** *(Spectral Theorem for Unbounded, Self-Adjoint Operators)*](#thrm:hall-10.4) below. Let $$X \subset \mathbb{C}$$ be compact with $$\sigma(A) \subset X$$, and let $$\nu$$ be a projection-valued measure on the Borel $$\sigma$$-algebra of $$X$$ with $$\int_X \lambda \, d\nu(\lambda) = A$$. Then
>
> $$
>     \nu(E) = \mu^A\big( E \cap \sigma(A) \big) \qquad \text{for every Borel } E \subset X;
> $$
>
> in particular $$\nu$$ assigns no mass to $$X \setminus \sigma(A)$$, so a measure representing $$A$$ on a larger space is automatically concentrated on $$\sigma(A)$$ and agrees there with $$\mu^A$$.

**Proof**
By [**Lemma** *(The Spectrum of a Bounded Operator is a Compact Metric Measurable Space)*](#lmm:spectrum-compact-general), $$X \equiv \sigma(A)$$ is a compact metric space. By [**Theorem** *(Continuous Functional Calculus for a Normal Operator)*](#thrm:continuous-functional-calculus-normal), the map $$\Phi_A$$ constructed there satisfies properties 1–5 of the [definition of an abstract continuous functional calculus](#def:abstract-continuous-functional-calculus), so it *is* an abstract continuous functional calculus on $$X$$.

Applying [**Theorem** *(A Continuous Functional Calculus Yields a Projection-Valued Measure)*](#thrm:abstract-calculus-yields-pvm) to $$\Phi_A$$ gives a projection-valued measure $$\mu^A \equiv \mu^{\Phi_A}$$ on the Borel $$\sigma$$-algebra of $$\sigma(A)$$ with $$\int_{\sigma(A)} f \, d\mu^A = \Phi_A(f)$$ for every continuous $$f$$ (and $$= \widetilde{\Phi_A}(f)$$ for every bounded measurable $$f$$). Taking $$f = \iota$$, the (continuous) function $$\iota(\lambda) = \lambda$$, and using property 5 of [**Theorem** *(Continuous Functional Calculus for a Normal Operator)*](#thrm:continuous-functional-calculus-normal), which gives $$\Phi_A(\iota) = A$$,

$$
    \int_{\sigma(A)} \lambda \, d\mu^A(\lambda) = \Phi_A(\iota) = A,
$$

which is existence.

*Uniqueness.* We prove the ambient form, which contains the plain one as the case $$X = \sigma(A)$$. So let $$X \subset \mathbb{C}$$ be compact with $$\sigma(A) \subset X$$, and let $$\nu$$ be a projection-valued measure on the Borel $$\sigma$$-algebra of $$X$$ with $$\int_X \iota \, d\nu = A$$, where $$\iota(\lambda) = \lambda$$ (a bounded function on the compact $$X$$, so this is the bounded integral). Write $$\Psi(f) \equiv \int_X f \, d\nu$$ for bounded measurable $$f$$ on $$X$$, and write $$\widetilde{\mu^A}$$ for the extension of $$\mu^A$$ to $$X$$ given by $$\widetilde{\mu^A}(E) \equiv \mu^A(E \cap \sigma(A))$$, a projection-valued measure on $$X$$ (the four properties transfer as in the corresponding extension in [**Theorem** *(hall-10.30)*](#thrm:hall-10.30), using $$\sigma(A) \subset X$$).

By property 4 of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) — integration intertwines complex conjugation with the adjoint — $$\Psi(\overline\iota) = \Psi(\iota)^* = A^*$$. By property 3 (multiplicativity) and linearity, it follows by induction on $$k+l$$ that $$\Psi(\iota^k\overline\iota^{\,l}) = A^k(A^*)^l$$ for all $$k,l \ge 0$$, and hence, by linearity again, $$\Psi(p) = p(A,A^*)$$ for every polynomial $$p$$ in $$\lambda$$ and $$\overline\lambda$$. The same identity holds for $$\Phi_A$$, by the defining property in [**Theorem** *(Continuous Functional Calculus for a Normal Operator)*](#thrm:continuous-functional-calculus-normal), and for the integral against $$\widetilde{\mu^A}$$, since $$\widetilde{\mu^A}$$ is concentrated on $$\sigma(A)$$ where it agrees with $$\mu^A$$. So all three agree on polynomial functions.

Now fix $$\psi \in \mathbf{H}$$ and consider the two finite positive Borel measures $$\nu_\psi$$ and $$\widetilde{\mu^A}_\psi$$ on $$X$$. Writing $$\mathcal{P}$$ for the algebra of functions on $$X$$ of the form $$\lambda \mapsto p(\lambda,\overline\lambda)$$, we have for $$p \in \mathcal{P}$$

$$
    \int_X p \, d\nu_\psi = \left< \psi, \Psi(p)\psi \right> = \left< \psi, p(A,A^*)\psi \right> = \left< \psi, \left( \int_X p \, d\widetilde{\mu^A} \right)\psi \right> = \int_X p \, d\widetilde{\mu^A}_\psi,
$$

using the defining property of each bounded integral at the two ends. Both sides are continuous in $$p$$ with respect to the supremum norm on $$X$$ (each is bounded in modulus by $$\left\| p \right\|_\infty$$ times the total mass $$\left\| \psi \right\|^2$$), and $$\mathcal{P}$$ is dense in $$C^0(X;\mathbb{C})$$ by the [**Complex Stone–Weierstrass Theorem**](../spectral-theorems/#thrm:stone–weierstrass-complex) — $$\mathcal{P}$$ being a subalgebra of $$C^0(X;\mathbb{C})$$ containing the constants, separating points, and closed under conjugation, exactly as verified for $$\sigma(A)$$ in the proof of [**Theorem** *(Continuous Functional Calculus for a Normal Operator)*](#thrm:continuous-functional-calculus-normal), the verification using nothing about the underlying compact set. Hence $$\int_X f \, d\nu_\psi = \int_X f \, d\widetilde{\mu^A}_\psi$$ for every $$f \in C^0(X;\mathbb{C})$$, in particular for every real-valued continuous $$f$$.

Two finite positive Borel measures on the compact metric space $$X$$ that assign the same integral to every $$f \in C^0(X;\mathbb{R})$$ are equal — this is exactly the uniqueness clause of the [**Riesz Representation Theorem**](../spectral-theorems/#thrm:riesz-representation), both measures representing the same positive linear functional. Hence $$\nu_\psi = \widetilde{\mu^A}_\psi$$, i.e. $$\left< \psi, \nu(E)\psi \right> = \left< \psi, \widetilde{\mu^A}(E)\psi \right>$$ for every Borel $$E \subset X$$ and every $$\psi \in \mathbf{H}$$. For fixed $$E$$, the two bounded operators therefore induce the same quadratic form, so are equal by uniqueness in [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63). As $$E$$ was arbitrary, $$\nu = \widetilde{\mu^A}$$, which is the ambient statement; taking $$X = \sigma(A)$$ gives $$\nu = \mu^A$$.$$\blacksquare$$

## The Cayley Transform

We can now prove the spectral theorem for an unbounded self-adjoint operator $$A$$, by manufacturing from $$A$$ a *bounded* operator to which the results of the previous section apply. The construction is guided by a scalar analogue: the map

$$
    C(x) \equiv \frac{x+i}{x-i}, \qquad x \in \mathbb{R},
$$

is about the simplest bounded injective function one can write down on $$\mathbb{R}$$. Substituting the operator $$A$$ for $$x$$ produces a bounded operator $$U$$ — the *Cayley transform* of $$A$$ — which turns out to be unitary, hence normal, hence subject to [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20). We then transport the resulting projection-valued measure back from the circle to $$\mathbb{R}$$ along $$C$$.

We will need one fact about unitary operators, from [Definition (Unitary Operator)](#def:unitary-operator) above.

> **Lemma** *(Unitary Operators are Normal)*
<a name="lmm:unitary-is-normal"></a>
<!--  \uses{def:unitary-operator} -->
<!--  \uses{def:hall-10.19} -->
<!--  \uses{lmm:hall-dense-testing-second-slot} -->
<!--  \uses{def:hall-9.1} -->
> If $$U \in \mathcal{B}(\mathbf{H})$$ is unitary, then $$U^*U = UU^* = \mathbf{1}$$; in particular $$U$$ is normal.

**Proof**
For all $$\phi,\psi \in \mathbf{H}$$, the [definition of the adjoint](#def:hall-9.1) and inner-product preservation give $$\left< \phi, U^*U\psi \right> = \left< U\phi, U\psi \right> = \left< \phi, \psi \right> = \left< \phi, \mathbf{1}\psi \right>$$. By [Lemma (Equality Testing on a Dense Subspace, Second Slot)](#lmm:hall-dense-testing-second-slot) with $$D = \mathbf{H}$$, $$U^*U\psi = \psi$$ for every $$\psi$$, i.e. $$U^*U = \mathbf{1}$$.

Since $$U$$ is a bijection, it has a set-theoretic inverse $$U^{-1}$$, and $$U^*U = \mathbf{1}$$ identifies $$U^* = U^*(UU^{-1}) = (U^*U)U^{-1} = U^{-1}$$. Hence $$UU^* = UU^{-1} = \mathbf{1}$$ as well, and $$U^*U = \mathbf{1} = UU^*$$ is exactly the [definition of normal](#def:hall-10.19).$$\blacksquare$$

The Cayley transform will be transported to a projection-valued measure on the unit circle, which presupposes that the spectrum of $$U$$ actually lies there. We record that.

> **Lemma** *(The Spectrum of a Unitary Operator Lies on the Unit Circle)*
<a name="lmm:unitary-spectrum-circle"></a>
<!--  \uses{def:unitary-operator} -->
<!--  \uses{../spectral-theorems/#crllr:crllr-1} -->
<!--  \uses{../spectral-theorems/#lmm:hall-7.6} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
> Let $$U \in \mathcal{B}(\mathbf{H})$$ be unitary, with $$\mathbf{H} \ne \{0\}$$. Then $$\sigma(U) \subset S^1 \equiv \{ z \in \mathbb{C} : \lvert z \rvert = 1 \}$$.

**Proof**
First, $$\left\| U \right\| = 1$$: unitarity gives $$\left\| U\psi \right\| = \left\| \psi \right\|$$ for all $$\psi$$ (take $$\phi = \psi$$ in the inner-product identity of [Definition (Unitary Operator)](#def:unitary-operator) and take square roots), so $$\left\| U \right\| = 1$$ since $$\mathbf{H} \ne \{0\}$$ provides a vector of norm $$1$$. The same computation applied to $$U^{-1}$$ gives $$\left\| U^{-1}\psi \right\| = \left\| U U^{-1}\psi \right\| = \left\| \psi \right\|$$, so $$\left\| U^{-1} \right\| = 1$$ as well.

Let $$\lambda \in \sigma(U)$$. By [**Corollary**](../spectral-theorems/#crllr:crllr-1), $$\lvert \lambda \rvert \le R(U) \le \left\| U \right\| = 1$$. Suppose, for contradiction, that $$\lvert \lambda \rvert < 1$$. Factor

$$
    U - \lambda\mathbf{1} = U\big( \mathbf{1} - \lambda U^{-1} \big).
$$

Since $$\left\| \lambda U^{-1} \right\| = \lvert \lambda \rvert \left\| U^{-1} \right\| = \lvert \lambda \rvert < 1$$, the geometric series [**Lemma** *(hall-7.6)*](../spectral-theorems/#lmm:hall-7.6) shows $$\mathbf{1} - \lambda U^{-1}$$ is invertible in $$\mathcal{B}(\mathbf{H})$$. As $$U$$ is invertible too (with bounded inverse $$U^{-1}$$), the product $$U(\mathbf{1}-\lambda U^{-1}) = U - \lambda\mathbf{1}$$ is invertible in $$\mathcal{B}(\mathbf{H})$$, with bounded inverse $$(\mathbf{1}-\lambda U^{-1})^{-1}U^{-1}$$. By the [definition of the resolvent set](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum), $$\lambda$$ lies in the resolvent set of $$U$$, contradicting $$\lambda \in \sigma(U)$$. Hence $$\lvert \lambda \rvert = 1$$.$$\blacksquare$$

We record the scalar maps and their elementary properties. Write $$S^1 \equiv \{ u \in \mathbb{C} : \lvert u \rvert = 1 \}$$ for the unit circle.

> **Lemma** *(The Cayley Map and its Inverse)*
<a name="lmm:cayley-map"></a>
> Define $$C : \mathbb{R} \to \mathbb{C}$$ and $$D : S^1\setminus\{1\} \to \mathbb{C}$$ by
>
> $$
>     C(x) \equiv \frac{x+i}{x-i}, \qquad D(u) \equiv i\,\frac{u+1}{u-1}.
> $$
>
> Then $$C$$ is a bijection of $$\mathbb{R}$$ onto $$S^1\setminus\{1\}$$, $$D$$ is its inverse, and both are continuous (hence Borel measurable) on their domains. Moreover $$D$$ is real-valued.

**Proof**
*Well defined and continuous.* For $$x \in \mathbb{R}$$, $$x - i \ne 0$$, so $$C(x)$$ is defined, and $$C$$ is continuous as a quotient of continuous functions with non-vanishing denominator. Also $$\lvert x+i \rvert = \sqrt{x^2+1} = \lvert x-i \rvert$$, so $$\lvert C(x) \rvert = 1$$, i.e. $$C(x) \in S^1$$; and $$C(x) = 1$$ would force $$x+i = x-i$$, i.e. $$i = -i$$, which is false, so $$C(x) \in S^1\setminus\{1\}$$. Similarly $$D$$ is defined and continuous on $$S^1\setminus\{1\}$$, where $$u - 1 \ne 0$$.

*$$D$$ is real-valued.* Let $$u \in S^1\setminus\{1\}$$, so $$\overline u = u^{-1}$$. Then

$$
    \overline{D(u)} = \overline{i\,\frac{u+1}{u-1}} = -i\,\frac{\overline u + 1}{\overline u - 1} = -i\,\frac{u^{-1}+1}{u^{-1}-1} = -i\,\frac{1 + u}{1 - u} = i\,\frac{u+1}{u-1} = D(u),
$$

multiplying numerator and denominator by $$u$$ in the middle step. A complex number equal to its conjugate is real.

*Mutually inverse.* For $$x \in \mathbb{R}$$, writing $$u = C(x) = (x+i)/(x-i)$$,

$$
    D(C(x)) = i\,\frac{\frac{x+i}{x-i} + 1}{\frac{x+i}{x-i} - 1} = i\,\frac{(x+i)+(x-i)}{(x+i)-(x-i)} = i\,\frac{2x}{2i} = x,
$$

multiplying numerator and denominator by $$x-i$$. Conversely, for $$u \in S^1\setminus\{1\}$$, writing $$x = D(u) = i(u+1)/(u-1)$$,

$$
    C(D(u)) = \frac{i\frac{u+1}{u-1} + i}{i\frac{u+1}{u-1} - i} = \frac{(u+1)+(u-1)}{(u+1)-(u-1)} = \frac{2u}{2} = u,
$$

multiplying numerator and denominator by $$(u-1)/i$$. So $$C$$ and $$D$$ are mutually inverse; in particular $$C$$ is injective (having a left inverse) and surjective onto $$S^1\setminus\{1\}$$ (having a right inverse), i.e. bijective.$$\blacksquare$$

We now construct the operator $$U$$. Recall from [**Theorem** *(Spectrum of a Self-Adjoint Operator is Real)*](#thrm:hall-9.17) that if $$A$$ is self-adjoint then $$\pm i$$ lie in the resolvent set of $$A$$, so $$(A \mp i\mathbf{1})^{-1}$$ exist as bounded operators on $$\mathbf{H}$$ in the sense of the [definition of the resolvent set](#def:hall-9.16).

> **Theorem** *(Cayley Transform)*
<a name="thrm:hall-10.28"></a>
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{def:unitary-operator} -->
<!--  \uses{thrm:hall-9.17} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:hall-9.13} -->
<!--  \uses{lmm:adjoint-of-scalar-multiple-of-identity} -->
<!--  \uses{def:range-of-an-unbounded-operator} -->
<!--  \uses{lmm:uniqueness-of-resolvent} -->
<!--  \uses{../spectral-theorems/#def:identity-and-indicator} -->
<!--  \uses{prpstn:polarization-identity} -->
> Let $$A$$ be a self-adjoint operator on $$\mathbf{H}$$ and define
>
> $$
>     U\psi \equiv (A + i\mathbf{1})(A - i\mathbf{1})^{-1}\psi, \qquad \psi \in \mathbf{H}.
> $$
>
> Then:
>
> 1. $$U$$ is a unitary operator on $$\mathbf{H}$$.
> 2. $$U - \mathbf{1}$$ is injective.
> 3. $$\text{Range}(U - \mathbf{1}) = \text{Dom}(A)$$, and for all $$\psi \in \text{Range}(U-\mathbf{1})$$,
>
>    $$
>        A\psi = i(U + \mathbf{1})(U - \mathbf{1})^{-1}\psi.
>    $$
> 4. $$U - \mathbf{1} = 2i\,(A - i\mathbf{1})^{-1}$$, and equivalently $$U = \mathbf{1} + 2i\,(A-i\mathbf{1})^{-1}$$.

Note that Point 2 and Point 3 together say that $$U - \mathbf{1}$$ is a bijection of $$\mathbf{H}$$ onto $$\text{Dom}(A)$$; the symbol $$(U-\mathbf{1})^{-1}$$ in Point 3 refers to the inverse of *that* bijection. We are *not* claiming $$1$$ lies in the resolvent set of $$U$$: the map $$(U-\mathbf{1})^{-1} : \text{Dom}(A) \to \mathbf{H}$$ is not bounded unless $$\text{Dom}(A) = \mathbf{H}$$, which happens only when $$A$$ is bounded.

**Proof**
*Preliminaries on the resolvents.* Since $$A$$ is self-adjoint, [**Theorem** *(Spectrum of a Self-Adjoint Operator is Real)*](#thrm:hall-9.17) gives $$\sigma(A) \subset \mathbb{R}$$, so $$\pm i$$ lie in the resolvent set. By the [definition of the resolvent set](#def:hall-9.16), there is a bounded $$(A-i\mathbf{1})^{-1} \in \mathcal{B}(\mathbf{H})$$ with: (i) $$(A-i\mathbf{1})^{-1}\psi \in \text{Dom}(A)$$ and $$(A-i\mathbf{1})(A-i\mathbf{1})^{-1}\psi = \psi$$ for all $$\psi \in \mathbf{H}$$; and (ii) $$(A-i\mathbf{1})^{-1}(A-i\mathbf{1})\psi = \psi$$ for all $$\psi \in \text{Dom}(A)$$.

From (i), $$(A-i\mathbf{1})^{-1}$$ is injective: if $$(A-i\mathbf{1})^{-1}\psi = 0$$ then $$\psi = (A-i\mathbf{1})0 = 0$$. From (ii), $$(A-i\mathbf{1})^{-1}$$ maps $$\mathbf{H}$$ *onto* $$\text{Dom}(A)$$: every $$\phi \in \text{Dom}(A)$$ equals $$(A-i\mathbf{1})^{-1}\chi$$ for $$\chi = (A-i\mathbf{1})\phi \in \mathbf{H}$$. Combining, $$(A-i\mathbf{1})^{-1}$$ is a bijection of $$\mathbf{H}$$ onto $$\text{Dom}(A)$$; and (i), (ii) show $$A - i\mathbf{1}$$ is the inverse bijection, from $$\text{Dom}(A)$$ onto $$\mathbf{H}$$. The identical reasoning with $$-i$$ in place of $$i$$ shows $$A + i\mathbf{1}$$ is a bijection of $$\text{Dom}(A)$$ onto $$\mathbf{H}$$.

**Part 1.** As a composition of a bijection $$\mathbf{H} \to \text{Dom}(A)$$ with a bijection $$\text{Dom}(A) \to \mathbf{H}$$, $$U$$ is a bijection of $$\mathbf{H}$$ onto $$\mathbf{H}$$. It is linear, being a composition of the linear maps $$(A-i\mathbf{1})^{-1}$$ and $$A+i\mathbf{1}$$. Boundedness will follow from the norm identity established next, so we turn to that first.

For the inner product, first note that $$A$$ is symmetric, by [**Proposition** *(Symmetric Operators and the Adjoint)*](#prpstn:hall-9.4) applied to the self-adjoint $$A$$. Hence for $$\phi \in \text{Dom}(A)$$, expanding and using symmetry to cancel the cross terms ($$\left< A\phi, i\phi \right> + \left< i\phi, A\phi \right> = i\left< A\phi,\phi \right> - i\left< \phi, A\phi \right> = 0$$),

$$
    \left< (A+i\mathbf{1})\phi, (A+i\mathbf{1})\phi \right> = \left< A\phi,A\phi \right> + \left< \phi,\phi \right> = \left< (A-i\mathbf{1})\phi, (A-i\mathbf{1})\phi \right>,
$$

the second equality by the same computation with $$i$$ replaced by $$-i$$ (the cross terms again cancelling). Applying this with $$\phi = (A-i\mathbf{1})^{-1}\psi \in \text{Dom}(A)$$, and using property (i) above,

$$
    \left\| U\psi \right\|^2 = \left< (A+i\mathbf{1})\phi, (A+i\mathbf{1})\phi \right> = \left< (A-i\mathbf{1})\phi, (A-i\mathbf{1})\phi \right> = \left< \psi,\psi \right> = \left\| \psi \right\|^2.
$$

So $$U$$ preserves norms, hence is bounded with $$\left\| U \right\| = 1$$ (as $$\mathbf{H} \ne \{0\}$$; if $$\mathbf{H} = \{0\}$$ everything is trivial). By the consequence clause of [**Proposition** *(Polarization Identity for the Inner Product)*](#prpstn:polarization-identity), a norm-preserving linear map preserves the inner product, so $$U$$ does. Being also a bijection, $$U$$ is unitary in the sense of [Definition (Unitary Operator)](#def:unitary-operator).

**Part 2.** For $$\psi \in \mathbf{H}$$, write $$A + i\mathbf{1} = (A - i\mathbf{1}) + 2i\mathbf{1}$$ and apply both sides to $$(A-i\mathbf{1})^{-1}\psi$$, using property (i):

$$
    U\psi = (A+i\mathbf{1})(A-i\mathbf{1})^{-1}\psi = (A-i\mathbf{1})(A-i\mathbf{1})^{-1}\psi + 2i(A-i\mathbf{1})^{-1}\psi = \psi + 2i(A-i\mathbf{1})^{-1}\psi,
$$

that is,

$$
    U - \mathbf{1} = 2i\,(A - i\mathbf{1})^{-1}, \tag{$\natural\natural$}
$$

which is **Part 4**. Since $$(A-i\mathbf{1})^{-1}$$ is injective (shown above) and $$2i \ne 0$$, $$U - \mathbf{1}$$ is injective, which is **Part 2**.

**Part 3.** By $$(\natural\natural)$$, $$\text{Range}(U-\mathbf{1}) = \text{Range}\big( 2i(A-i\mathbf{1})^{-1} \big) = \text{Range}\big( (A-i\mathbf{1})^{-1} \big) = \text{Dom}(A)$$, the last equality because $$(A-i\mathbf{1})^{-1}$$ maps $$\mathbf{H}$$ onto $$\text{Dom}(A)$$, as shown in the preliminaries.

For the formula, let $$\psi \in \text{Dom}(A) = \text{Range}(U - \mathbf{1})$$. By $$(\natural\natural)$$, $$(U-\mathbf{1})^{-1}\psi = \tfrac{1}{2i}(A-i\mathbf{1})\psi$$ — indeed applying $$U - \mathbf{1} = 2i(A-i\mathbf{1})^{-1}$$ to the right-hand side gives $$2i(A-i\mathbf{1})^{-1}\tfrac{1}{2i}(A-i\mathbf{1})\psi = \psi$$ by property (ii). Hence, using $$U = \mathbf{1} + 2i(A-i\mathbf{1})^{-1}$$ from $$(\natural\natural)$$ to write $$U + \mathbf{1} = 2\cdot\mathbf{1} + 2i(A-i\mathbf{1})^{-1}$$ and then property (i),

$$
\begin{align}
    i(U+\mathbf{1})(U-\mathbf{1})^{-1}\psi
        &= i(U+\mathbf{1})\,\frac{1}{2i}(A-i\mathbf{1})\psi \\
        &= \frac{1}{2}\Big( 2(A - i\mathbf{1})\psi + 2i(A-i\mathbf{1})^{-1}(A-i\mathbf{1})\psi \Big) \\
        &= \frac{1}{2}\Big( 2(A-i\mathbf{1})\psi + 2i\psi \Big) \\
        &= (A - i\mathbf{1})\psi + i\psi \\
        &= A\psi,
\end{align}
$$

which is the claimed identity.$$\blacksquare$$

The Cayley transform carries the spectrum of $$A$$ onto the spectrum of $$U$$, minus the point $$1$$. This is what will let us conclude that $$\mu^A$$ is concentrated on $$\sigma(A)$$, matching the form in which the spectral theorem is usually stated.

> **Lemma** *(Spectral Mapping for the Cayley Transform)*
<a name="lmm:cayley-spectral-mapping"></a>
<!--  \uses{thrm:hall-10.28} -->
<!--  \uses{lmm:cayley-map} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{lmm:spectrum-notions-agree} -->
<!--  \uses{lmm:uniqueness-of-resolvent} -->
<!--  \uses{../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum} -->
<!--  \uses{lmm:unitary-spectrum-circle} -->
> Let $$A$$ be a self-adjoint operator on $$\mathbf{H}$$, with $$\mathbf{H} \ne \{0\}$$, and let $$U$$ be its Cayley transform. Then for every $$\lambda \in \mathbb{R}$$,
>
> $$
>     \lambda \in \sigma(A) \iff C(\lambda) \in \sigma(U),
> $$
>
> and consequently $$C\big( \sigma(A) \big) = \sigma(U) \setminus \{1\}$$.

**Proof**
*The key factorization.* Fix $$\lambda \in \mathbb{R}$$, so $$\lambda \ne i$$ and $$C(\lambda) = (\lambda+i)/(\lambda-i)$$ is defined. Writing $$\mathbf{1} = (A-i\mathbf{1})(A-i\mathbf{1})^{-1}$$ and factoring,

$$
\begin{align}
    U - C(\lambda)\mathbf{1} &= \Big[ (A+i\mathbf{1}) - C(\lambda)(A - i\mathbf{1}) \Big](A-i\mathbf{1})^{-1} \\
                             &= \frac{1}{\lambda-i}\Big[ (\lambda-i)(A+i\mathbf{1}) - (\lambda+i)(A-i\mathbf{1}) \Big](A-i\mathbf{1})^{-1} \\
                             &= \frac{-2i}{\lambda-i}\,(A - \lambda\mathbf{1})(A-i\mathbf{1})^{-1},
\end{align}
$$

the last step because $$(\lambda-i)(A+i\mathbf{1}) - (\lambda+i)(A-i\mathbf{1}) = 2i\lambda\mathbf{1} - 2iA = -2i(A-\lambda\mathbf{1})$$, the terms $$\lambda A$$ and $$\mathbf{1}$$ cancelling. Note $$-2i/(\lambda-i) \ne 0$$.

*If $$\lambda$$ is in the resolvent set of $$A$$, so is $$C(\lambda)$$ for $$U$$.* Let $$B \equiv (A-\lambda\mathbf{1})^{-1} \in \mathcal{B}(\mathbf{H})$$, which maps $$\mathbf{H}$$ onto $$\text{Dom}(A)$$ and inverts $$A - \lambda\mathbf{1}$$ both ways. Put

$$
    S \equiv \frac{\lambda-i}{-2i}\,\big( \mathbf{1} + (\lambda-i)B \big),
$$

a bounded operator. Since $$(A - i\mathbf{1})B = \big[ (A-\lambda\mathbf{1}) + (\lambda-i)\mathbf{1} \big]B = \mathbf{1} + (\lambda-i)B$$ — the products being defined because $$B$$ lands in $$\text{Dom}(A)$$ — we have $$S = \frac{\lambda-i}{-2i}(A-i\mathbf{1})B$$. Hence, using the factorization and $$(A-i\mathbf{1})^{-1}(A-i\mathbf{1})\psi = \psi$$ on $$\text{Dom}(A)$$,

$$
    \big( U - C(\lambda)\mathbf{1} \big) S = \frac{-2i}{\lambda-i}(A-\lambda\mathbf{1})(A-i\mathbf{1})^{-1}\cdot\frac{\lambda-i}{-2i}(A-i\mathbf{1})B = (A-\lambda\mathbf{1})B = \mathbf{1},
$$

and symmetrically $$S\big( U - C(\lambda)\mathbf{1} \big) = \mathbf{1}$$, using $$B(A-\lambda\mathbf{1})\psi = \psi$$ on $$\text{Dom}(A)$$ together with the fact that $$(A-i\mathbf{1})^{-1}$$ maps $$\mathbf{H}$$ into $$\text{Dom}(A)$$. So $$U - C(\lambda)\mathbf{1}$$ has a bounded two-sided inverse, i.e. $$C(\lambda)$$ lies in the resolvent set of $$U$$ by the [definition of the resolvent set](../spectral-theorems/#def:bounded-operator-resolvent-and-spectrum).

*Conversely.* Suppose $$C(\lambda)$$ is in the resolvent set of $$U$$, with bounded inverse $$T \equiv (U - C(\lambda)\mathbf{1})^{-1}$$. Rearranging the factorization, and using that $$(A-i\mathbf{1})^{-1}$$ is a bijection of $$\mathbf{H}$$ onto $$\text{Dom}(A)$$ (established in the preliminaries of [**Theorem** *(Cayley Transform)*](#thrm:hall-10.28)),

$$
    (A - \lambda\mathbf{1}) = \frac{\lambda-i}{-2i}\big( U - C(\lambda)\mathbf{1} \big)(A - i\mathbf{1}) \qquad \text{on } \text{Dom}(A).
$$

Put $$R \equiv \frac{-2i}{\lambda-i}(A-i\mathbf{1})^{-1}T$$, a bounded operator mapping $$\mathbf{H}$$ into $$\text{Dom}(A)$$. For $$\psi \in \mathbf{H}$$, $$(A-\lambda\mathbf{1})R\psi = \frac{\lambda-i}{-2i}(U - C(\lambda)\mathbf{1})(A-i\mathbf{1})\cdot\frac{-2i}{\lambda-i}(A-i\mathbf{1})^{-1}T\psi = (U-C(\lambda)\mathbf{1})T\psi = \psi$$; and for $$\psi \in \text{Dom}(A)$$, $$R(A-\lambda\mathbf{1})\psi = \frac{-2i}{\lambda-i}(A-i\mathbf{1})^{-1}T\cdot\frac{\lambda-i}{-2i}(U-C(\lambda)\mathbf{1})(A-i\mathbf{1})\psi = (A-i\mathbf{1})^{-1}(A-i\mathbf{1})\psi = \psi$$. Both clauses of [Definition (Resolvent Set and Spectrum of an Unbounded Operator)](#def:hall-9.16) hold, so $$\lambda$$ is in the resolvent set of $$A$$.

*Conclusion.* Taking complements, $$\lambda \in \sigma(A) \iff C(\lambda) \in \sigma(U)$$ — the two notions of spectrum for the bounded operator $$U$$ agreeing by [**Lemma** *(The Two Notions of Spectrum Agree for Bounded Operators)*](#lmm:spectrum-notions-agree). Since $$C$$ is a bijection of $$\mathbb{R}$$ onto $$S^1\setminus\{1\}$$ by [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map), and $$\sigma(U) \subset S^1$$ by [**Lemma** *(The Spectrum of a Unitary Operator Lies on the Unit Circle)*](#lmm:unitary-spectrum-circle), the equivalence says exactly that $$C$$ maps $$\sigma(A)$$ onto $$\sigma(U) \cap (S^1\setminus\{1\}) = \sigma(U)\setminus\{1\}$$.$$\blacksquare$$

## Proof of the Spectral Theorem for Unbounded Self-Adjoint Operators

By [**Theorem** *(Cayley Transform)*](#thrm:hall-10.28) and [**Lemma** *(Unitary Operators are Normal)*](#lmm:unitary-is-normal), the operator $$U$$ is normal, so [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20) supplies a projection-valued measure $$\mu^U$$ on $$\sigma(U) \subset S^1$$ with $$\int_{\sigma(U)} u \, d\mu^U(u) = U$$. The plan is to recover $$A$$ from $$\mu^U$$ by integrating $$D$$, then transport $$\mu^U$$ to a measure on $$\mathbb{R}$$ along $$C$$.

We first record the measure-theoretic transport fact, standard and assumed here in the same spirit as the other imports.

> **Theorem** *(Change of Variables for a Pushforward Measure)*
<a name="thrm:change-of-variables"></a>
> Let $$(Y,\Omega(Y))$$ and $$(Z,\Omega(Z))$$ be measurable spaces, $$T : Y \to Z$$ a measurable bijection with measurable inverse, and $$\nu$$ a measure on $$\Omega(Y)$$. Define the *pushforward* $$T_*\nu$$ on $$\Omega(Z)$$ by $$(T_*\nu)(F) \equiv \nu\big(T^{-1}(F)\big)$$. Then for every measurable $$g : Z \to [0,\infty]$$, and for every $$g$$ integrable with respect to $$T_*\nu$$,
>
> $$
>     \int_Z g \, d(T_*\nu) = \int_Y (g \circ T) \, d\nu.
> $$

We also isolate the purely set-theoretic transport of a projection-valued measure along a Borel bijection, since we will need it twice: once to build $$\mu^A$$ from $$\mu^U$$, and once, in the reverse direction, in the uniqueness argument.

> **Lemma** *(A Borel Bijection Transports a Projection-Valued Measure)*
<a name="lmm:borel-bijection-transports-pvm"></a>
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{thrm:change-of-variables} -->
> Let $$(Y,\Omega(Y))$$ and $$(Z,\Omega(Z))$$ be measurable spaces.
>
> 1. *(Restriction.)* Let $$\mu$$ be a projection-valued measure on $$\Omega(Y)$$ and let $$Y_0 \in \Omega(Y)$$ satisfy $$\mu(Y\setminus Y_0) = 0$$. Then $$\Omega(Y_0) \equiv \{ E \in \Omega(Y) \mid E \subset Y_0 \}$$ is a $$\sigma$$-algebra on $$Y_0$$, and the restriction of $$\mu$$ to $$\Omega(Y_0)$$ is a projection-valued measure on $$Y_0$$.
> 2. *(Transport.)* Let $$T : Y \to Z$$ be a bijection such that both $$T$$ and $$T^{-1}$$ are measurable, and let $$\mu$$ be a projection-valued measure on $$\Omega(Y)$$. Then
>
>    $$
>        \nu(F) \equiv \mu\big( T^{-1}(F) \big), \qquad F \in \Omega(Z),
>    $$
>
>    defines a projection-valued measure on $$\Omega(Z)$$, and for every $$\psi \in \mathbf{H}$$ the associated scalar measures satisfy $$\nu_\psi = T_*\mu_\psi$$, the pushforward of $$\mu_\psi$$ along $$T$$.

**Proof**
**Part 1.** That $$\Omega(Y_0)$$ is a $$\sigma$$-algebra on $$Y_0$$ is immediate: it contains $$Y_0$$, is closed under countable unions (a countable union of subsets of $$Y_0$$ lies in $$Y_0$$), and is closed under complementation *within $$Y_0$$*, since $$Y_0 \setminus E = Y_0 \cap (Y\setminus E) \in \Omega(Y)$$ for $$E \in \Omega(Y_0)$$.

Properties 1, 3, and 4 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) are inherited verbatim, being conditions on sets that all lie in $$\Omega(Y_0) \subset \Omega(Y)$$. For property 2, $$\mu(\emptyset) = 0$$ is inherited, and for the total mass: $$Y = Y_0 \sqcup (Y\setminus Y_0)$$ is a disjoint decomposition, so property 3 applied to the sequence $$Y_0, Y\setminus Y_0, \emptyset, \emptyset, \ldots$$ gives $$\mathbf{1} = \mu(Y) = \mu(Y_0) + \mu(Y\setminus Y_0) = \mu(Y_0) + 0$$, i.e. $$\mu(Y_0) = \mathbf{1}$$.

**Part 2.** First, $$\nu$$ is well defined: $$T^{-1}(F) \in \Omega(Y)$$ for $$F \in \Omega(Z)$$, since $$T$$ is measurable.

*Property 1.* $$\nu(F) = \mu(T^{-1}(F))$$ is a bounded orthogonal projection, being a value of $$\mu$$.

*Property 2.* $$T^{-1}(\emptyset) = \emptyset$$ and $$T^{-1}(Z) = Y$$ (as $$T$$ is a bijection onto $$Z$$), so $$\nu(\emptyset) = \mu(\emptyset) = 0$$ and $$\nu(Z) = \mu(Y) = \mathbf{1}$$.

*Property 3.* Let $$\{F_j\}$$ be pairwise disjoint in $$\Omega(Z)$$ with union $$F$$. Preimages preserve disjointness and unions: $$T^{-1}(F_i) \cap T^{-1}(F_j) = T^{-1}(F_i \cap F_j) = T^{-1}(\emptyset) = \emptyset$$ for $$i \ne j$$, and $$T^{-1}(F) = \bigcup_j T^{-1}(F_j)$$. So property 3 for $$\mu$$ applied to $$\{T^{-1}(F_j)\}$$ gives, for every $$\psi$$,

$$
    \nu(F)\psi = \mu\big(T^{-1}(F)\big)\psi = \sum_{j=1}^\infty \mu\big(T^{-1}(F_j)\big)\psi = \sum_{j=1}^\infty \nu(F_j)\psi,
$$

convergent in the norm topology.

*Property 4.* $$T^{-1}(F_1 \cap F_2) = T^{-1}(F_1) \cap T^{-1}(F_2)$$, so $$\nu(F_1\cap F_2) = \mu\big(T^{-1}(F_1)\cap T^{-1}(F_2)\big) = \mu\big(T^{-1}(F_1)\big)\mu\big(T^{-1}(F_2)\big) = \nu(F_1)\nu(F_2)$$, by property 4 for $$\mu$$.

*The associated measures.* For $$\psi \in \mathbf{H}$$ and $$F \in \Omega(Z)$$, directly from the definitions,

$$
    \nu_\psi(F) = \left< \psi, \nu(F)\psi \right> = \left< \psi, \mu\big(T^{-1}(F)\big)\psi \right> = \mu_\psi\big( T^{-1}(F) \big) = (T_*\mu_\psi)(F),
$$

the last equality being the definition of the pushforward in [**Theorem** *(Change of Variables for a Pushforward Measure)*](#thrm:change-of-variables).$$\blacksquare$$

Note that $$T$$ being a *bijection* is used only for $$T^{-1}(Z) = Y$$ in property 2; the measurability of $$T^{-1}$$ is not needed for Part 2 at all, but is what guarantees, in our applications, that the transported measure can itself be transported back.

One more observation is needed: $$1$$ is never an atom of $$\mu^U$$, so $$D$$ — undefined at $$u=1$$ — is defined $$\mu^U_\psi$$-almost everywhere for every $$\psi$$, and integrating it is legitimate.

> **Lemma** *(The Cayley Transform Omits the Point $$1$$)*
<a name="lmm:cayley-omits-one"></a>
<!--  \uses{thrm:hall-10.28} -->
<!--  \uses{thrm:hall-10.20} -->
<!--  \uses{def:hall-7.14} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{prpstn:hall-7.15} -->
> Let $$A$$ be self-adjoint with Cayley transform $$U$$, and $$\mu^U$$ the projection-valued measure of $$U$$. Then $$\mu^U(\{1\}) = 0$$, and consequently $$\mu^U_\psi(\{1\}) = 0$$ for every $$\psi \in \mathbf{H}$$.

**Proof**
Let $$V \equiv \text{Range}\big(\mu^U(\{1\})\big)$$ be the corresponding spectral subspace and let $$\psi \in V$$. Apply Part 2 of [**Proposition** *(Properties of Spectral Subspaces)*](#prpstn:hall-7.15) with $$X = \sigma(U)$$ (compact, and contained in $$\mathbb{C}$$), $$\mu = \mu^U$$ — so that $$\int_X \iota\,d\mu^U = U$$ by [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20), making the operator called $$A$$ there equal to $$U$$ — together with $$\lambda_0 = 1$$ and $$E = \{1\} \cap \sigma(U)$$. For every $$\varepsilon > 0$$ we have $$E \subset \{ \lambda \in X \mid \lvert \lambda - 1 \rvert \le \varepsilon \}$$, since the only point of $$E$$ is $$1$$ itself, at distance $$0$$. Hence $$\left\| (U - \mathbf{1})\psi \right\| \le \varepsilon\left\| \psi \right\|$$ for every $$\varepsilon>0$$, forcing $$(U-\mathbf{1})\psi = 0$$. By Point 2 of [**Theorem** *(Cayley Transform)*](#thrm:hall-10.28), $$U - \mathbf{1}$$ is injective, so $$\psi = 0$$. Thus $$V = \{0\}$$, i.e. $$\mu^U(\{1\}) = 0$$ (a projection with trivial range is the zero operator, since $$P\xi \in \text{Range}(P) = \{0\}$$ for every $$\xi$$). Then $$\mu^U_\psi(\{1\}) = \left< \psi, \mu^U(\{1\})\psi \right> = 0$$ for every $$\psi$$.$$\blacksquare$$

The next proposition is the heart of the matter: $$A$$ is recovered from $$U$$ by the functional calculus applied to $$D$$.

> **Proposition**
<a name="prpstn:hall-10.29"></a>
<!--  \uses{thrm:hall-10.28} -->
<!--  \uses{lmm:integral-ignores-null-sets} -->
<!--  \uses{thrm:abstract-calculus-yields-pvm} -->
<!--  \uses{lmm:integral-preserves-spectral-subspaces} -->
<!--  \uses{lmm:range-of-projection-is-kernel} -->
<!--  \uses{thrm:hall-10.20} -->
<!--  \uses{lmm:cayley-map} -->
<!--  \uses{lmm:cayley-omits-one} -->
<!--  \uses{def:hall-7.14} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:hall-10.3} -->
<!--  \uses{prpstn:hall-9.26-internal} -->
<!--  \uses{def:internal-orthogonal-decomposition} -->
<!--  \uses{lmm:bounded-on-set-range-in-domain} -->
<!--  \uses{lmm:range-membership-concentrates-measure} -->
<!--  \uses{lmm:norm-convergent-decomposition} -->
<!--  \uses{prpstn:abstract-extended-multiplicative} -->
<!--  \uses{def:abstract-extended-calculus} -->
<!--  \uses{prpstn:hall-9.11} -->
<!--  \uses{lmm:unitary-is-normal} -->
<!--  \uses{crllr:abstract-extended-norm-bound} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{prpstn:hall-9.4} -->
<!--  \uses{prpstn:quadratic-forms-on-a-subspace-properties} -->
> Let $$A$$ be a self-adjoint operator on $$\mathbf{H}$$, with $$\mathbf{H} \ne \{0\}$$, let $$U$$ be its Cayley transform, and let $$D$$ be as in [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map). (The hypothesis $$\mathbf{H} \ne \{0\}$$ is needed because the projection-valued measure $$\mu^U$$ below is supplied by [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20), which assumes it.) Then
>
> $$
>     A = \int_{\sigma(U)} D(u) \, d\mu^U(u),
> $$
>
> with equality of domains, the right-hand side being the (generally unbounded) operator of [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1) with domain $$W_D$$.

**Proof**
Write $$\widehat{D} \equiv \int_{\sigma(U)} D \, d\mu^U$$, an unbounded operator with domain $$W_D$$ by [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1). Since $$D$$ is real-valued by [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map), and defined $$\mu^U_\psi$$-almost everywhere by [**Lemma** *(The Cayley Transform Omits the Point $$1$$)*](#lmm:cayley-omits-one), [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3) shows $$\widehat{D}$$ is self-adjoint on $$W_D$$.

*Step 1: a disjoint cover on which $$D$$ is bounded.* Recall from [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map) that $$D$$ is defined on $$S^1\setminus\{1\}$$. Extend it to all of $$S^1$$ by setting $$D(1) \equiv 0$$; since $$\mu^U(\{1\}) = 0$$ by [**Lemma** *(The Cayley Transform Omits the Point $$1$$)*](#lmm:cayley-omits-one), this modification changes no integral against any $$\mu^U_\psi$$, and it makes $$D$$ a measurable function defined everywhere on $$\sigma(U)$$, as required for $$\int_{\sigma(U)} D \, d\mu^U$$ to be given by [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1).

For $$n \ge 1$$ define

$$
    F_1 \equiv \big\{ u \in \sigma(U) \;\mid\; \lvert u-1 \rvert \ge 1 \big\} \cup \big( \{1\} \cap \sigma(U) \big),
    \qquad
    F_n \equiv \left\{ u \in \sigma(U) \;\middle|\; \frac{1}{n} \le \lvert u - 1 \rvert < \frac{1}{n-1} \right\} \ (n \ge 2).
$$

These are pairwise disjoint Borel subsets of $$\sigma(U)$$ with $$\bigcup_{n\ge1} F_n = \sigma(U)$$: every $$u \ne 1$$ has $$\lvert u-1\rvert > 0$$ and so lies in exactly one of the annuli, and $$u=1$$ has been placed in $$F_1$$.

On $$F_n$$ we have $$\lvert u-1 \rvert \ge 1/n$$ (for $$n=1$$ apart from the single point $$u=1$$, where $$D$$ has been set to $$0$$), so, using $$\lvert u+1 \rvert \le 2$$ for $$u \in S^1$$,

$$
    \lvert D(u) \rvert = \frac{\lvert u+1 \rvert}{\lvert u-1 \rvert} \le 2n \qquad \text{on } F_n
$$

(and $$\lvert D(1) \rvert = 0 \le 2n$$ as well), i.e. $$D$$ is bounded on each $$F_n$$. Let $$\mathbf{H}_n \equiv \text{Range}\big( \mu^U(F_n) \big)$$ be the corresponding [spectral subspaces](#def:hall-7.14).

*Step 2: $$\mathbf{H}_n \subset W_D$$, and $$\widehat{D}$$ agrees with $$A$$ there.* By [**Lemma** *(Bounded on a Set Implies the Range Lies in the Domain)*](#lmm:bounded-on-set-range-in-domain), applied with $$E = F_n$$ and $$c = 2n$$, $$\mathbf{H}_n \subset W_D$$.

Fix $$n$$ and let $$\psi \in \mathbf{H}_n$$. Let $$g \equiv 1_{F_n}\cdot D$$ and $$h \equiv 1_{F_n}\cdot (\iota - 1)$$, where $$\iota(u) = u$$; both are bounded measurable functions on $$\sigma(U)$$, so the extended calculus $$\widetilde\Phi$$ of [Definition (The Extended Calculus)](#def:abstract-extended-calculus) applies to them. Since $$D(u)(u-1) = i(u+1)$$ for $$u \ne 1$$, the functions $$g\,h$$ and $$1_{F_n}\cdot i(\iota+1)$$ agree at every point of $$\sigma(U)$$ except possibly $$u = 1$$ (where $$g(1)h(1) = 0$$ by our convention $$D(1) = 0$$, while the right-hand side need not vanish). Since $$\mu^U(\{1\}) = 0$$ by [**Lemma** *(The Cayley Transform Omits the Point $$1$$)*](#lmm:cayley-omits-one), [**Lemma** *(The Integral Ignores Null Sets)*](#lmm:integral-ignores-null-sets) — together with the identification $$\widetilde\Phi(\cdot) = \int_{\sigma(U)} \cdot \; d\mu^U$$ on bounded measurable functions from [**Theorem** *(A Continuous Functional Calculus Yields a Projection-Valued Measure)*](#thrm:abstract-calculus-yields-pvm) — gives $$\widetilde\Phi(g\,h) = \widetilde\Phi\big(1_{F_n}i(\iota+1)\big)$$. Hence, by [**Proposition** *(The Extended Calculus is Multiplicative)*](#prpstn:abstract-extended-multiplicative),

$$
    \widetilde\Phi(g)\,\widetilde\Phi(h) = \widetilde\Phi\big( 1_{F_n} i(\iota+1) \big) = i\,\widetilde\Phi\big(1_{F_n}(\iota+1)\big). \tag{$\smile$}
$$

Also $$h \cdot 1_{F_n} = h$$ and $$g \cdot 1_{F_n} = g$$, so multiplicativity gives $$\widetilde\Phi(h)\mu^U(F_n) = \widetilde\Phi(h)$$ and likewise for $$g$$; in particular $$\widetilde\Phi(h)\psi = \widetilde\Phi(h)\mu^U(F_n)\psi = \widetilde\Phi(h)\psi$$, consistent, and both $$\widetilde\Phi(g)\psi$$ and $$\widetilde\Phi(h)\psi$$ lie in $$\mathbf{H}_n$$ (as $$\mu^U(F_n)\widetilde\Phi(g) = \widetilde\Phi(1_{F_n}g) = \widetilde\Phi(g)$$, and similarly for $$h$$).

Now $$\widetilde\Phi(h) = \widetilde\Phi\big(1_{F_n}(\iota-1)\big) = (U - \mathbf{1})\mu^U(F_n)$$, by multiplicativity together with $$\widetilde\Phi(\iota) = U$$ and $$\widetilde\Phi(1) = \mathbf{1}$$. So for $$\psi \in \mathbf{H}_n$$, $$\widetilde\Phi(h)\psi = (U-\mathbf{1})\psi$$. By Point 3 of [**Theorem** *(Cayley Transform)*](#thrm:hall-10.28), $$(U-\mathbf{1})\psi \in \text{Range}(U-\mathbf{1}) = \text{Dom}(A)$$, and

$$
    A(U-\mathbf{1})\psi = i(U+\mathbf{1})(U-\mathbf{1})^{-1}(U-\mathbf{1})\psi = i(U+\mathbf{1})\psi.
$$

On the other hand, $$\widetilde\Phi\big(1_{F_n}(\iota+1)\big)\psi = (U+\mathbf{1})\psi$$ for $$\psi \in \mathbf{H}_n$$. Indeed, multiplicativity and linearity give $$\widetilde\Phi\big(1_{F_n}(\iota+1)\big) = \mu^U(F_n)(U+\mathbf{1})$$, and $$(U+\mathbf{1})\psi \in \mathbf{H}_n$$ — because $$U$$ commutes with $$\mu^U(F_n)$$ (multiplicativity again, $$\iota\cdot 1_{F_n} = 1_{F_n}\cdot\iota$$), so $$\mu^U(F_n)U\psi = U\mu^U(F_n)\psi = U\psi$$, while $$\mu^U(F_n)\psi = \psi$$ — so $$\mu^U(F_n)$$ acts as the identity on it. Hence, applying $$(\smile)$$ to $$\psi$$,

$$
    \widetilde\Phi(g)\,(U-\mathbf{1})\psi = \widetilde\Phi(g)\widetilde\Phi(h)\psi = i(U+\mathbf{1})\psi = A(U-\mathbf{1})\psi.
$$

We claim $$U - \mathbf{1}$$ maps $$\mathbf{H}_n$$ *onto* $$\mathbf{H}_n$$. On $$F_n$$ we have $$\lvert u - 1 \rvert \ge 1/n > 0$$, except at the single point $$u = 1$$, which lies in $$F_1$$ and where the reciprocal below is undefined; we set

$$
    k(u) \equiv \begin{cases} \dfrac{1}{u-1} & u \in F_n,\ u \ne 1 \\[4pt] 0 & \text{otherwise,} \end{cases}
$$

a bounded measurable function on $$\sigma(U)$$, bounded by $$n$$.

The functions $$k\,h$$ and $$1_{F_n}$$ agree at every point of $$\sigma(U)$$ except possibly $$u = 1$$: for $$u \in F_n$$ with $$u \ne 1$$ both equal $$1$$, off $$F_n$$ both vanish, and at $$u=1$$ (relevant only when $$n = 1$$) we have $$k(1)h(1) = 0$$ while $$1_{F_1}(1) = 1$$. The same holds for $$h\,k$$. Since $$\mu^U(\{1\}) = 0$$ by [**Lemma** *(The Cayley Transform Omits the Point $$1$$)*](#lmm:cayley-omits-one), [**Lemma** *(The Integral Ignores Null Sets)*](#lmm:integral-ignores-null-sets) — together with the identification $$\widetilde\Phi(\cdot) = \int_{\sigma(U)} \cdot \; d\mu^U$$ on bounded measurable functions from [**Theorem** *(A Continuous Functional Calculus Yields a Projection-Valued Measure)*](#thrm:abstract-calculus-yields-pvm) — gives $$\widetilde\Phi(k\,h) = \widetilde\Phi(1_{F_n}) = \widetilde\Phi(h\,k)$$. Hence by [**Proposition** *(The Extended Calculus is Multiplicative)*](#prpstn:abstract-extended-multiplicative),

$$
    \widetilde\Phi(k)\widetilde\Phi(h) = \widetilde\Phi(1_{F_n}) = \mu^U(F_n) = \widetilde\Phi(h)\widetilde\Phi(k).
$$

Since $$\mu^U(F_n)$$ acts as the identity on $$\mathbf{H}_n$$ (by [**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel)) and $$\widetilde\Phi(k)$$ maps $$\mathbf{H}_n$$ into $$\mathbf{H}_n$$ (as $$\mu^U(F_n)\widetilde\Phi(k) = \widetilde\Phi(1_{F_n}k) = \widetilde\Phi(k)$$ by multiplicativity), the restriction of $$\widetilde\Phi(k)$$ to $$\mathbf{H}_n$$ is a two-sided inverse of the restriction of $$\widetilde\Phi(h) = (U-\mathbf{1})\mu^U(F_n)$$ to $$\mathbf{H}_n$$ — which is just $$U - \mathbf{1}$$ there. So $$U-\mathbf{1}$$ maps $$\mathbf{H}_n$$ bijectively onto $$\mathbf{H}_n$$, and every $$\eta \in \mathbf{H}_n$$ is of the form $$(U-\mathbf{1})\psi$$ with $$\psi \in \mathbf{H}_n$$. Hence $$\widetilde\Phi(g)$$ and $$A$$ agree on all of $$\mathbf{H}_n$$, and $$\mathbf{H}_n \subset \text{Dom}(A)$$.

Finally, $$\widehat{D}$$ agrees with $$\widetilde\Phi(g)$$ on $$\mathbf{H}_n$$: for $$\psi \in \mathbf{H}_n$$, [**Lemma** *(Range Membership Concentrates the Associated Measure)*](#lmm:range-membership-concentrates-measure) gives $$\mu^U_\psi(F_n^c) = 0$$, so $$\int_{\sigma(U)} D \, d\mu^U_\psi = \int_{\sigma(U)} g \, d\mu^U_\psi$$, i.e. the two operators induce the same diagonal quadratic form on $$\mathbf{H}_n$$; since both map $$\mathbf{H}_n$$ into $$\mathbf{H}_n$$ — for $$\widehat{D}$$ by [**Lemma** *(The Integral Preserves Spectral Subspaces on which the Integrand is Bounded)*](#lmm:integral-preserves-spectral-subspaces), applied to the measure $$\mu^U$$, the function $$D$$, and the set $$F_n$$ on which $$D$$ is bounded; for $$\widetilde\Phi(g)$$ because $$\mu^U(F_n)\widetilde\Phi(g) = \widetilde\Phi(1_{F_n}g) = \widetilde\Phi(g)$$ by multiplicativity —, Part 1 of [**Proposition** *(Properties of Quadratic Forms on a Subspace)*](#prpstn:quadratic-forms-on-a-subspace-properties) applied on the subspace $$\mathbf{H}_n$$ gives equality of the two restrictions. So $$\widehat{D}$$ and $$A$$ agree on $$\mathbf{H}_n$$, for every $$n$$.

*Step 3: conclusion by essential self-adjointness.* We check $$\{\mathbf{H}_n\}$$ is an [internal orthogonal decomposition](#def:internal-orthogonal-decomposition) of $$\mathbf{H}$$. For pairwise orthogonality: the $$F_n$$ are pairwise disjoint, so for $$n \ne m$$, properties 4 and 2 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) give $$\mu^U(F_n)\mu^U(F_m) = \mu^U(F_n \cap F_m) = \mu^U(\emptyset) = 0$$; hence for $$\eta \in \mathbf{H}_n$$ and $$\zeta \in \mathbf{H}_m$$, using $$\mu^U(F_n)\eta = \eta$$ and $$\mu^U(F_m)\zeta = \zeta$$ ([**Lemma** *(The Range of a Projection is the Kernel of its Complement)*](#lmm:range-of-projection-is-kernel)) and self-adjointness of $$\mu^U(F_n)$$, $$\left< \eta,\zeta \right> = \left< \mu^U(F_n)\eta, \mu^U(F_m)\zeta \right> = \left< \eta, \mu^U(F_n)\mu^U(F_m)\zeta \right> = 0$$. For the decomposition: [**Lemma** *(Norm-Convergent Decomposition over a Disjoint Cover)*](#lmm:norm-convergent-decomposition) applied to $$\{F_n\}$$ (pairwise disjoint with union $$\sigma(U)$$) gives $$\psi = \sum_n \mu^U(F_n)\psi$$ for every $$\psi \in \mathbf{H}$$, norm-convergent, with $$\mu^U(F_n)\psi \in \mathbf{H}_n$$. Let $$W_0$$ be the algebraic span of the $$\mathbf{H}_n$$'s. By **Step 2**, $$W_0 \subset \text{Dom}(A) \cap W_D$$ and $$A = \widehat{D}$$ on $$W_0$$.

Let $$A_n$$ denote the common restriction of $$A$$ and $$\widehat D$$ to $$\mathbf{H}_n$$, a bounded operator (it equals $$\widetilde\Phi(g)\vert_{\mathbf{H}_n}$$, and $$\left\| \widetilde\Phi(g) \right\| \le \left\| g \right\|_\infty \le 2n$$ by [**Corollary** *(The Extended Calculus is Norm-Bounded)*](#crllr:abstract-extended-norm-bound), since $$\lvert g \rvert = \lvert 1_{F_n} D \rvert \le 2n$$ by **Step 1**) which is self-adjoint on $$\mathbf{H}_n$$: by [**Lemma** *(The Integral Preserves Spectral Subspaces on which the Integrand is Bounded)*](#lmm:integral-preserves-spectral-subspaces), $$\widehat{D}$$ maps $$\mathbf{H}_n$$ into itself, and for $$\eta,\zeta \in \mathbf{H}_n \subset W_D$$ the symmetry of $$\widehat D$$ (it being self-adjoint, hence symmetric by [**Proposition** *(Symmetric Operators and the Adjoint)*](#prpstn:hall-9.4)) gives $$\left< \eta, A_n\zeta \right> = \left< \eta, \widehat D\zeta \right> = \left< \widehat D\eta, \zeta \right> = \left< A_n\eta, \zeta \right>$$; a bounded symmetric operator defined on all of the Hilbert space $$\mathbf{H}_n$$ is self-adjoint there, since its adjoint is then defined on all of $$\mathbf{H}_n$$ and agrees with it. Both $$A\vert_{W_0}$$ and $$\widehat{D}\vert_{W_0}$$ are then symmetric operators on $$\mathbf{H}$$ with domain $$W_0$$ acting as $$A_n$$ on each $$\mathbf{H}_n$$ — and they are the *same* operator, by **Step 2**. By [**Proposition** *(Direct Sums of Bounded Self-Adjoint Operators, Internal Form)*](#prpstn:hall-9.26-internal), this common restriction is essentially self-adjoint.

Now $$A$$ and $$\widehat{D}$$ are both self-adjoint operators extending it: $$A$$ by hypothesis, $$\widehat{D}$$ by [**Proposition** *(hall-10.3)*](#prpstn:hall-10.3), and both extend $$A\vert_{W_0} = \widehat D\vert_{W_0}$$ since $$W_0 \subset \text{Dom}(A)\cap W_D$$ with agreement there. By [**Proposition** *(Uniqueness of the Self-Adjoint Extension of an Essentially Self-Adjoint Operator)*](#prpstn:hall-9.11), an essentially self-adjoint operator has exactly one self-adjoint extension; hence $$A = \widehat{D}$$, with equality of domains.$$\blacksquare$$

Transporting the measure along $$C$$ now gives the projection-valued measure for $$A$$.

> **Theorem**
<a name="thrm:hall-10.30"></a>
<!--  \uses{lmm:borel-bijection-transports-pvm} -->
<!--  \uses{prpstn:hall-10.29} -->
<!--  \uses{lmm:cayley-map} -->
<!--  \uses{lmm:cayley-omits-one} -->
<!--  \uses{thrm:change-of-variables} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:projection-valued-measures-associated-measure} -->
<!--  \uses{lmm:unitary-spectrum-circle} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{thrm:hall-10.20} -->
> Let $$A$$ be a self-adjoint operator on $$\mathbf{H}$$, with $$\mathbf{H} \ne \{0\}$$, let $$U$$ be its Cayley transform, and let $$\mu^U$$ be the projection-valued measure of $$U$$ supplied by [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20). Define, for each Borel set $$E \subset \mathbb{R}$$,
>
> $$
>     \mu^A(E) \equiv \mu^U\big( C(E) \big).
> $$
>
> Then $$\mu^A$$ is a projection-valued measure on $$\mathbb{R}$$ and
>
> $$
>     A = \int_{\mathbb{R}} \lambda \, d\mu^A(\lambda).
> $$

**Proof**
*$$\mu^A$$ is well defined and a projection-valued measure.* By [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map), $$C : \mathbb{R} \to S^1\setminus\{1\}$$ is a bijection with inverse $$D$$, both continuous and hence Borel measurable.

We first put $$\mu^U$$ on the right space. Extend $$\mu^U$$ from $$\sigma(U)$$ to all of $$S^1$$ by $$\mu^U(F) \equiv \mu^U(F \cap \sigma(U))$$; this is again a projection-valued measure, the four properties being inherited from those on $$\sigma(U)$$ since $$F \mapsto F\cap\sigma(U)$$ preserves the relevant set operations and sends $$S^1$$ to $$S^1 \cap \sigma(U) = \sigma(U)$$, the last equality by [**Lemma** *(The Spectrum of a Unitary Operator Lies on the Unit Circle)*](#lmm:unitary-spectrum-circle). By [**Lemma** *(The Cayley Transform Omits the Point $$1$$)*](#lmm:cayley-omits-one), $$\mu^U(\{1\}) = 0$$, so Part 1 of [**Lemma** *(A Borel Bijection Transports a Projection-Valued Measure)*](#lmm:borel-bijection-transports-pvm), applied with $$Y = S^1$$ and $$Y_0 = S^1\setminus\{1\}$$, shows the restriction of $$\mu^U$$ to the Borel subsets of $$S^1\setminus\{1\}$$ is a projection-valued measure on $$S^1\setminus\{1\}$$.

Now apply Part 2 of the same lemma with $$Y = S^1\setminus\{1\}$$, $$Z = \mathbb{R}$$, and $$T = D$$ (a bijection with $$T^{-1} = C$$, both measurable). Since $$D^{-1}(E) = C(E)$$, the transported measure is exactly

$$
    \mu^A(E) = \mu^U\big( C(E) \big) = \mu^U\big( D^{-1}(E) \big),
$$

so $$\mu^A$$ is a projection-valued measure on $$\mathbb{R}$$, and the lemma further gives $$\mu^A_\psi = D_*\mu^U_\psi$$ for every $$\psi$$.

*The associated scalar measures.* As just noted, $$\mu^A_\psi = D_*\mu^U_\psi$$, the pushforward of $$\mu^U_\psi$$ along $$D$$, in the sense of [**Theorem** *(Change of Variables for a Pushforward Measure)*](#thrm:change-of-variables).

*Equality of domains.* By that change-of-variables theorem applied with $$T = D$$ and $$g(\lambda) = \lvert \lambda \rvert^2$$,

$$
    \int_{\mathbb{R}} \lvert \lambda \rvert^2 \, d\mu^A_\psi(\lambda) = \int_{\sigma(U)} \lvert D(u) \rvert^2 \, d\mu^U_\psi(u).
$$

The left side is finite exactly when $$\psi$$ lies in the domain $$W_\iota$$ of $$\int_{\mathbb{R}}\lambda\,d\mu^A(\lambda)$$, and the right side exactly when $$\psi \in W_D$$, by the definition of those domains in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2). So the two operators have the same domain, namely $$W_D = \text{Dom}(A)$$, the last equality by [**Proposition** *(hall-10.29)*](#prpstn:hall-10.29).

*Equality of the operators.* Applying the change-of-variables theorem again, this time with $$g(\lambda) = \lambda$$ (integrable against $$\mu^A_\psi$$ for $$\psi$$ in the common domain), for every such $$\psi$$,

$$
    \left< \psi, \left( \int_{\mathbb{R}} \lambda \, d\mu^A(\lambda) \right)\psi \right> = \int_{\mathbb{R}} \lambda \, d\mu^A_\psi(\lambda) = \int_{\sigma(U)} D(u) \, d\mu^U_\psi(u) = \left< \psi, \left( \int_{\sigma(U)} D \, d\mu^U \right)\psi \right>,
$$

the outer equalities by the defining property of the unbounded integral in [**Proposition** *(hall-10.1)*](#prpstn:hall-10.1). By the strengthened uniqueness clause of that proposition — an operator on the common domain is determined by its diagonal quadratic form — the two operators are equal. By [**Proposition** *(hall-10.29)*](#prpstn:hall-10.29), $$\int_{\sigma(U)}D\,d\mu^U = A$$, so $$\int_{\mathbb{R}}\lambda\,d\mu^A(\lambda) = A$$.$$\blacksquare$$

We can finally state and prove the theorem this post set out to establish.

> **Theorem** *(Spectral Theorem for Unbounded, Self-Adjoint Operators)*
<a name="thrm:hall-10.4"></a>
<!--  \uses{lmm:borel-bijection-transports-pvm} -->
<!--  \uses{def:hall-9.5} -->
<!--  \uses{def:hall-9.16} -->
<!--  \uses{thrm:hall-9.17} -->
<!--  \uses{thrm:hall-10.30} -->
<!--  \uses{thrm:hall-10.28} -->
<!--  \uses{thrm:hall-10.20} -->
<!--  \uses{prpstn:hall-10.1} -->
<!--  \uses{prpstn:hall-10.2} -->
<!--  \uses{lmm:cayley-map} -->
<!--  \uses{lmm:truncations-converge} -->
<!--  \uses{lmm:associated-measure-of-image} -->
<!--  \uses{thrm:change-of-variables} -->
<!--  \uses{../spectral-theorems/#def:projection-valued-measure} -->
<!--  \uses{../spectral-theorems/#thrm:operator-valued-integration} -->
<!--  \uses{../spectral-theorems/#thrm:bounded-convergence-theorem} -->
<!--  \uses{../spectral-theorems/#prpstn:hall-a.63} -->
<!--  \uses{lmm:uniqueness-of-resolvent} -->
<!--  \uses{lmm:norm-identity-bounded-integral} -->
<!--  \uses{lmm:integral-ignores-null-sets} -->
<!--  \uses{lmm:unitary-spectrum-circle} -->
<!--  \uses{lmm:cayley-spectral-mapping} -->
> If $$A$$ is an unbounded self-adjoint operator on $$\mathbf{H}$$, there is a unique projection-valued measure $$\mu^A$$ on the Borel $$\sigma$$-algebra of $$\mathbb{R}$$ such that
>
> $$
>     \int_{\mathbb{R}} \lambda \, d\mu^A(\lambda) = A.
> $$
>
> Moreover $$\mu^A$$ is *concentrated on the spectrum*: $$\mu^A(\mathbb{R}\setminus\sigma(A)) = 0$$, equivalently $$\mu^A(E) = \mu^A(E \cap \sigma(A))$$ for every Borel $$E \subset \mathbb{R}$$. Restricting $$\mu^A$$ to the Borel subsets of $$\sigma(A)$$ therefore gives a projection-valued measure on $$\sigma(A)$$ with $$\int_{\sigma(A)}\lambda\,d\mu^A(\lambda) = A$$, which is the form in which the theorem is usually stated; the two formulations correspond under extension by zero.

**Proof**
*The degenerate case.* If $$\mathbf{H} = \{0\}$$ the statement is immediate: the only linear map on $$\{0\}$$ is the zero map, which is also the identity $$\mathbf{1}$$, so the only candidate assignment $$E \mapsto \mu^A(E) \equiv 0$$ satisfies all four properties of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) (in particular $$\mu^A(\mathbb{R}) = 0 = \mathbf{1}$$), it is the unique such assignment, and $$\int_{\mathbb{R}}\lambda\,d\mu^A(\lambda) = 0 = A$$. So assume from now on that $$\mathbf{H} \ne \{0\}$$, as required by the results invoked below.

*Existence* is [**Theorem** *(hall-10.30)*](#thrm:hall-10.30).

*Uniqueness.* Suppose $$\nu$$ is a projection-valued measure on $$\mathbb{R}$$ with $$\int_{\mathbb{R}} \lambda \, d\nu(\lambda) = A$$; we must show $$\nu = \mu^A$$. Write $$\iota(\lambda) = \lambda$$, so the hypothesis reads $$\int_{\mathbb{R}} \iota \, d\nu = A$$, and in particular $$W_\iota = \text{Dom}(A)$$, where $$W_\iota$$ is the domain supplied by [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2) for the measure $$\nu$$.

*Step 1: the resolvent of $$A$$ is given by integrating $$r$$.* Define

$$
    r(\lambda) \equiv \frac{1}{\lambda - i}, \qquad \lambda \in \mathbb{R},
$$

a continuous function on $$\mathbb{R}$$ satisfying $$\lvert r(\lambda) \rvert = (\lambda^2+1)^{-1/2} \le 1$$, hence bounded and measurable; so $$B \equiv \int_{\mathbb{R}} r \, d\nu$$ is a *bounded* operator defined on all of $$\mathbf{H}$$. We claim $$B = (A - i\mathbf{1})^{-1}$$, the bounded inverse supplied by [**Theorem** *(Spectrum of a Self-Adjoint Operator is Real)*](#thrm:hall-9.17) and the [definition of the resolvent set](#def:hall-9.16).

First, $$B\psi \in \text{Dom}(A)$$ for every $$\psi \in \mathbf{H}$$. By [**Lemma** *(The Associated Measure of a Bounded-Calculus Image)*](#lmm:associated-measure-of-image) applied with $$h = r$$, and then using $$\lvert \iota r \rvert^2 = \lambda^2/(\lambda^2+1) \le 1$$,

$$
    \int_{\mathbb{R}} \lvert \iota \rvert^2 \, d\nu_{B\psi} = \int_{\mathbb{R}} \lvert \iota \rvert^2 \lvert r \rvert^2 \, d\nu_\psi \le \int_{\mathbb{R}} 1 \, d\nu_\psi = \nu_\psi(\mathbb{R}) = \left\| \psi \right\|^2 < \infty,
$$

so $$B\psi \in W_\iota = \text{Dom}(A)$$, by the definition of $$W_\iota$$ in [**Proposition** *(hall-10.2)*](#prpstn:hall-10.2).

Next, $$(A - i\mathbf{1})B\psi = \psi$$. Put $$E_n \equiv \{ \lambda \in \mathbb{R} \mid \lvert \lambda \rvert < n \}$$ and $$\iota_n \equiv \iota\cdot 1_{E_n}$$, a bounded measurable function. Since $$\iota_n$$ and $$r$$ are both bounded, property 3 (multiplicativity) of the [**Theorem** *(Operator-Valued Integration)*](../spectral-theorems/#thrm:operator-valued-integration) gives

$$
    \left( \int_{\mathbb{R}} \iota_n \, d\nu \right) B = \left( \int_{\mathbb{R}} \iota_n \, d\nu \right)\left( \int_{\mathbb{R}} r \, d\nu \right) = \int_{\mathbb{R}} \iota_n r \, d\nu.
$$

Apply both sides to $$\psi$$ and let $$n \to \infty$$. On the left, $$B\psi \in W_\iota$$ (just shown), so [**Lemma** *(Truncations Converge to the Unbounded Integral)*](#lmm:truncations-converge), applied to $$f = \iota$$ and the vector $$B\psi$$, gives $$\left( \int \iota_n \, d\nu \right)B\psi \to \left( \int \iota \, d\nu \right)B\psi = A B\psi$$ in norm. On the right, $$\iota_n r \to \iota r$$ pointwise with $$\lvert \iota_n r \rvert \le \lvert \iota r \rvert \le 1$$, so by [**Lemma** *(Norm Identity for the Bounded Integral)*](#lmm:norm-identity-bounded-integral) applied to the bounded function $$\iota_n r - \iota r$$, together with linearity of the bounded integral,

$$
    \left\| \left( \int_{\mathbb{R}} \iota_n r \, d\nu \right)\psi - \left( \int_{\mathbb{R}} \iota r \, d\nu \right)\psi \right\|^2 = \int_{\mathbb{R}} \lvert \iota_n r - \iota r \rvert^2 \, d\nu_\psi \longrightarrow 0,
$$

by the [**Bounded Convergence Theorem**](../spectral-theorems/#thrm:bounded-convergence-theorem) — applicable since $$\nu_\psi$$ is a finite measure and the integrands are bounded by $$4$$ and tend to $$0$$ pointwise. Hence

$$
    A B\psi = \left( \int_{\mathbb{R}} \iota r \, d\nu \right)\psi.
$$

Now $$\iota r$$ simplifies: $$\dfrac{\lambda}{\lambda-i} = \dfrac{(\lambda - i) + i}{\lambda - i} = 1 + i\,r(\lambda)$$. So, by linearity of the bounded integral and $$\int_{\mathbb{R}} 1 \, d\nu = \mathbf{1}$$ (property 2 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure) together with the defining property of the integral),

$$
    A B\psi = \left( \int_{\mathbb{R}} (1 + ir) \, d\nu \right)\psi = \psi + i B\psi,
$$

that is, $$(A - i\mathbf{1})B\psi = \psi$$, for every $$\psi \in \mathbf{H}$$.

Finally, $$B(A-i\mathbf{1})\psi = \psi$$ for $$\psi \in \text{Dom}(A)$$: set $$\chi \equiv (A-i\mathbf{1})\psi \in \mathbf{H}$$. By what we have just shown, $$(A-i\mathbf{1})B\chi = \chi = (A - i\mathbf{1})\psi$$, with both $$B\chi$$ and $$\psi$$ in $$\text{Dom}(A)$$. Since $$i$$ lies in the resolvent set of $$A$$, $$A - i\mathbf{1}$$ is injective on $$\text{Dom}(A)$$, so $$B\chi = \psi$$, i.e. $$B(A-i\mathbf{1})\psi = \psi$$. Both clauses of the [definition of the resolvent set](#def:hall-9.16) hold, so $$B = (A-i\mathbf{1})^{-1}$$.

*Step 2: $$\nu$$ determines $$U$$.* By [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map), $$C$$ is bounded ($$\lvert C \rvert = 1$$) and continuous, hence measurable, so $$\int_{\mathbb{R}} C \, d\nu$$ is a bounded operator. The pointwise identity

$$
    C(\lambda) = \frac{\lambda+i}{\lambda-i} = \frac{(\lambda - i) + 2i}{\lambda-i} = 1 + 2i\,r(\lambda)
$$

together with linearity of the bounded integral and **Step 1** gives

$$
    \int_{\mathbb{R}} C \, d\nu = \mathbf{1} + 2i\,B = \mathbf{1} + 2i\,(A-i\mathbf{1})^{-1} = U,
$$

the last equality being Point 4 of [**Theorem** *(Cayley Transform)*](#thrm:hall-10.28).

*Step 3: transporting to the circle.* Apply Part 2 of [**Lemma** *(A Borel Bijection Transports a Projection-Valued Measure)*](#lmm:borel-bijection-transports-pvm) with $$Y = \mathbb{R}$$, $$Z = S^1\setminus\{1\}$$, $$T = C$$ (a bijection with $$T^{-1} = D$$, both measurable, by [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map)), and the projection-valued measure $$\nu$$. This gives a projection-valued measure

$$
    \nu^U(F) \equiv \nu\big( C^{-1}(F) \big) = \nu\big( D(F) \big), \qquad F \subset S^1\setminus\{1\} \text{ Borel},
$$

on $$S^1\setminus\{1\}$$, with $$\nu^U_\psi = C_*\nu_\psi$$ for every $$\psi$$. Extend $$\nu^U$$ to all of $$S^1$$ by $$\nu^U(F) \equiv \nu^U(F\setminus\{1\})$$; this assigns $$\{1\}$$ no mass and is again a projection-valued measure, exactly as in the corresponding extension in the proof of [**Theorem** *(hall-10.30)*](#thrm:hall-10.30).

By [**Theorem** *(Change of Variables for a Pushforward Measure)*](#thrm:change-of-variables) with $$T = C$$ and $$g(u) = u$$ (bounded on $$S^1$$), for every $$\psi \in \mathbf{H}$$,

$$
    \left< \psi, \left( \int_{S^1} u \, d\nu^U(u) \right)\psi \right> = \int_{S^1} u \, d\nu^U_\psi(u) = \int_{\mathbb{R}} C(\lambda)\,d\nu_\psi(\lambda) = \left< \psi, \left( \int_{\mathbb{R}} C \, d\nu \right)\psi \right>,
$$

so, two bounded operators inducing the same quadratic form being equal by uniqueness in [**Proposition** *(hall-a.63)*](../spectral-theorems/#prpstn:hall-a.63), and by **Step 2**,

$$
    \int_{S^1} u \, d\nu^U(u) = \int_{\mathbb{R}} C \, d\nu = U.
$$

*Step 4: conclusion.* The projection-valued measure $$\mu^U$$ of $$U$$ also satisfies $$\int_{S^1} u \, d\mu^U(u) = U$$, by [**Theorem** *(Spectral Theorem for Bounded Normal Operators)*](#thrm:hall-10.20). Now $$\nu^U$$ is a projection-valued measure on $$S^1$$, not a priori on $$\sigma(U)$$, so the plain uniqueness clause does not apply directly; but $$S^1$$ is compact and contains $$\sigma(U)$$ by [**Lemma** *(The Spectrum of a Unitary Operator Lies on the Unit Circle)*](#lmm:unitary-spectrum-circle), and $$\int_{S^1} u \, d\nu^U(u) = U$$ was just shown, so the *ambient* uniqueness clause of that theorem applies with $$X = S^1$$ and gives $$\nu^U(F) = \mu^U(F \cap \sigma(U))$$ for every Borel $$F \subset S^1$$ — that is, $$\nu^U$$ equals the extension of $$\mu^U$$ to $$S^1$$ used throughout, which we continue to denote $$\mu^U$$.

Hence, for every Borel $$E \subset \mathbb{R}$$, using $$C^{-1}(C(E)) = E$$ (injectivity of $$C$$, from [**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map)) and the definition of $$\mu^A$$ in [**Theorem** *(hall-10.30)*](#thrm:hall-10.30),

$$
    \nu(E) = \nu\big( C^{-1}(C(E)) \big) = \nu^U\big( C(E) \big) = \mu^U\big( C(E) \big) = \mu^A(E).
$$

So $$\nu = \mu^A$$, establishing uniqueness.

*Concentration on the spectrum.* By the definition of $$\mu^A$$ in [**Theorem** *(hall-10.30)*](#thrm:hall-10.30), $$\mu^A(\mathbb{R}\setminus\sigma(A)) = \mu^U\big( C(\mathbb{R}\setminus\sigma(A)) \big)$$. Since $$C$$ is injective with image $$S^1\setminus\{1\}$$ ([**Lemma** *(The Cayley Map and its Inverse)*](#lmm:cayley-map)) and $$C(\sigma(A)) = \sigma(U)\setminus\{1\}$$ ([**Lemma** *(Spectral Mapping for the Cayley Transform)*](#lmm:cayley-spectral-mapping)),

$$
    C\big( \mathbb{R}\setminus\sigma(A) \big) = \big( S^1\setminus\{1\} \big) \setminus \big( \sigma(U)\setminus\{1\} \big) = \big( S^1 \setminus \sigma(U) \big) \setminus \{1\} \subset S^1\setminus\sigma(U),
$$

using injectivity for the first equality. The extension of $$\mu^U$$ to $$S^1$$ assigns no mass off $$\sigma(U)$$, by its definition $$\mu^U(F) = \mu^U(F\cap\sigma(U))$$ in the proof of [**Theorem** *(hall-10.30)*](#thrm:hall-10.30). Hence $$\mu^A(\mathbb{R}\setminus\sigma(A)) = 0$$, and for any Borel $$E$$, countable additivity (property 3 of the [definition of a projection-valued measure](../spectral-theorems/#def:projection-valued-measure)) applied to the disjoint decomposition $$E = (E\cap\sigma(A)) \sqcup (E\setminus\sigma(A))$$ gives $$\mu^A(E) = \mu^A(E\cap\sigma(A)) + 0$$.

Finally, the restriction of $$\mu^A$$ to Borel subsets of $$\sigma(A)$$ is a projection-valued measure on $$\sigma(A)$$, by Part 1 of [**Lemma** *(A Borel Bijection Transports a Projection-Valued Measure)*](#lmm:borel-bijection-transports-pvm) applied with $$Y = \mathbb{R}$$ and $$Y_0 = \sigma(A)$$ (legitimate since $$\mu^A(\mathbb{R}\setminus\sigma(A)) = 0$$); and $$\int_{\sigma(A)}\lambda\,d\mu^A(\lambda) = \int_{\mathbb{R}}\lambda\,d\mu^A(\lambda) = A$$, the integrals agreeing because the two measures $$\mu^A_\psi$$ involved differ only on the $$\mu^A_\psi$$-null set $$\mathbb{R}\setminus\sigma(A)$$, so [**Lemma** *(The Integral Ignores Null Sets)*](#lmm:integral-ignores-null-sets) applies.$$\blacksquare$$
