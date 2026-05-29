---
title:  "Local, Isometric Invariant States"
date:   2026-05-30 06:53:53 +0200
categories: aqft lcaqft
---

This blog post introduces the notion of "local isometric invariant states" in Algebraic Quantum Field Theory (AQFT) in Minkowski spacetime (a theory defined in [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)) and also does the same for AQFT in Lorentzian spacetime (a theory defined in [Haag Kastler Axioms in Curved Spacetime](https://kellyjdavis.github.io/aqft/lcaqft/haag-kastler-axioms-curved-spacetime/)). Such "local isometric invariant states" capture the physics of quantum systems that are invariant under isometries of spacetime.

# Reveiw of Algebraic Quantum Field Theory
Instead of diving headlong into a definition of "local isometric invariant states", we will begin with a review of AQFT in Minkowski spacetime and AQFT in Lorentzian spacetime.

The reviews of AQFT in Minkowski and Lorentzian spacetime will not provide all details of the blog posts [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/) and [Haag Kastler Axioms in Curved Spacetime](https://kellyjdavis.github.io/aqft/lcaqft/haag-kastler-axioms-curved-spacetime/) where these theories were introduced. The AQFT reviews serve only as a refresher, making sure readers are clear on the various definitions and axioms used.

## Algebraic Quantum Field Theory in Minkowski Spacetime
Now, before introducing any axioms that codify AQFT in Minkowski Spacetime, we must define Minkowski spacetime itself, the arena upon which everything unfolds.

**Definition** *(Chronological Future and Past)*
Consider a point $$p$$ in a smooth manifold with a Minkowski metric and associated time orientation. The *chronological future* of $$p$$ is the set $$I^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like curve. Similarly, the *chronological past* of $$p$$ is the set $$I^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like curve.

**Definition** *(Minkowski Spacetime)*
*Minkowski spacetime is the standard, smooth manifold $$\mathbb{R}^4$$ equipped with the standard time orientation $$(1,0,0,0)$$, associated Minkowski metric, and associated Alexandrov topology. (Note the Alexandrov topology is the topology in which sets of the form $$I^+(p) \cap I^-(q)$$ form the basis.)*

That done we can introduce the first axiom of AQFT in Minkowski spacetime:

> **Axiom 1** *(Local Algebras)* For any basis element $$\mathbf{B}$$ of the Alexandrov topology on Minkowski spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$, there is a corresponding abstract C\*-algebra $$\mathfrak{U}(\mathbf{B})$$
>
> $$
> \mathbf{B} \longmapsto \mathfrak{U}(\mathbf{B}),
> $$
>
> and when $$\mathbf{B}$$ is the the empty set, we have the distinguished correspondence
>
> $$
> \emptyset \longmapsto \mathbb{C} \mathbf{1},
> $$
>
> where $$\mathbf{1}$$ is the multiplicative identity in the abstract C\*-algebra $$\mathbb{C} \mathbf{1}$$.

The second axiom takes the following form:

> **Axiom 2** *(Isotony)* Let $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ be any two basis elements of the Alexandrov topology on Minkowski spacetime, i.e. any two sets of the form $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$.
>
> If $$\mathbf{B}_1 \subset \mathbf{B}_2$$ then $$\mathfrak{U}(\mathbf{B}_1) \subset \mathfrak{U}(\mathbf{B}_2)$$, where inclusion is implemented by
>
> $$
> i : \mathfrak{U}(\mathbf{B}_1) \hookrightarrow \mathfrak{U}(\mathbf{B}_2),
> $$
>
> a unital \*-monomorphism.

Before stating the next axiom, we need to introduce some terminology that appears therein.

**Definition** *(Quasilocal Algebra)*
Consider the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$. As proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), this set-theoretic union is a normed \*-algebra. Also, as proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), its completion yields a C\*-algebra, denoted as $$\mathfrak{U}$$. This C\*-algebra $$\mathfrak{U}$$ is called the *quasilocal algebra*.

**Definition** *(Causal Future and Past)*
Consider a point $$p$$ in a Minkowski spacetime. The *causal future* of $$p$$ is the set $$J^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like or light-like curve. Similarly, the *causal past* of $$p$$ is the set $$J^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like or light-like curve.

**Definition** *(Spacelike Related)*
Consider two points $$p_1$$ and $$p_2$$ in a Minkowski spacetime. The points are said to be *spacelike related* if $$p_2 \notin J^+(p_1) \cup J^-(p_1)$$ or equivalently $$p_1 \notin J^+(p_2) \cup J^-(p_2)$$.

**Definition** *(Completely Spacelike)*
Consider two sets $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ in a Minkowski spacetime. $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ are said to be *completely spacelike* if every $$p_1$$ in $$\mathbf{O}_1$$ is spacelike related to every $$p_2$$ in $$\mathbf{O}_2$$ or equivalently if every $$p_2$$ in $$\mathbf{O}_2$$ is spacelike related to every $$p_1$$ in $$\mathbf{O}_1$$.

With all of these definitions in hand, we can now state the next axiom:

> **Axiom 3** *(Local Commutativity)* Let $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ be any two basis elements of the Alexandrov topology on Minkowski spacetime, i.e. any two sets of the form $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$.
>
> If $$\mathbf{B_1}$$ and $$\mathbf{B_2}$$ are completely spacelike, then $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ commute in the quasilocal algebra $$\mathfrak{U}$$, i.e. for any $$a_1$$ in $$\mathfrak{U}(\mathbf{B_1})$$ and $$a_2$$ in $$\mathfrak{U}(\mathbf{B_2})$$ it follows that
>
> $$
> a_1 a_2 - a_2 a_1 = 0
> $$
>
> in the quasilocal algebra $$\mathfrak{U}$$.

The definitions required in the next axiom make use of terminology introduced in the previous blog post [GNS Construction Theorem](https://kellyjdavis.github.io/aqft/gns-construction/). It's strongly recommended that the reader be familiar with the GNS Construction Theorem or read [GNS Construction Theorem](https://kellyjdavis.github.io/aqft/gns-construction/) before proceeding.

That said, to state the next axiom we make use of the following definition:

**Definition** *(Quasilocal Observable)*
The image $$\pi_\omega(a)$$ of a self-adjoint member $$a$$ of the quasilocal algebra $$\mathfrak{U}$$ under a GNS \*-homomorphism $$\pi_\omega$$ of state $$\omega$$ is self-adjoint and thus corresponds to an "observable". Any "observable" corresponding to such a self-adjoint $$\pi_\omega(a)$$ is called a *quasilocal observable*.

Using this definition we can then state the next axiom

> **Axiom 4** *(Quasilocal Algebra)* All "observables" are quasilocal observables.

Finally we can state the last axiom

> **Axiom 5** *(Lorentz Covariance)* Let $$\mathbf{B}$$ be any basis element of the Alexandrov topology on Minkowski spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$.
>
> A member $$L$$ of the inhomogeneous Lorentz group connected to the identity acts on $$\mathfrak{U}(\mathbf{B})$$ as follows
>
> $$
> \begin{align}
> \alpha_L : \mathfrak{U}(\mathbf{B}) &\longrightarrow \mathfrak{U}(\mathbf{LB}) \\
>                      a              &\longmapsto     \alpha_L(a)
> \end{align}
> $$
>
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital *-isomorphism generated by $$L$$ that for the Lorentz group identity $$\mathbf{1}$$ satisfies
>
> $$
> \alpha_{\mathbf{1}}(a) = a
> $$
>
> and for all appropriate $$a$$, $$L$$, and $$L'$$
>
> $$
> \alpha_{L' \cdot L}(a) = \alpha_{L'}(\alpha_{L}(a)).
> $$

## Algebraic Quantum Field Theory in Lorentzian Spacetime
The lightning review of AQFT in Minkowski spacetime complete, we now move onto a review of AQFT in Lorentzian spacetime.

As in the Minkowski case, before introducing any axioms that codify AQFT in Lorentzian spacetime, we need to specify exactly what Lorentzian spacetime is:

**Definition** *(Chronological Future and Past)*
Consider a point $$p$$ in a smooth manifold with a Lorentzian metric and associated time orientation. The *chronological future* of $$p$$ is the set $$I^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like curve. Similarly, the *chronological past* of $$p$$ is the set $$I^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like curve.

**Definition** *(Lorentzian Spacetime)*
A *Lorentzian spacetime* is a smooth, connected, four dimensional manifold equipped with a smooth, nowhere-vanishing global vector field $$t^a$$ and associated Lorentzian metric. In addition it is equipped with an associated Hausdorff Alexandrov topology.

That clarified, we can present the first axiom:

> **Axiom 1** *(Local Algebras)* For any basis element $$\mathbf{B}$$ of the Alexandrov topology on a Lorentzian spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$, there is a corresponding abstract C\*-algebra $$\mathfrak{U}(\mathbf{B})$$
>
> $$
> \mathbf{B} \longmapsto \mathfrak{U}(\mathbf{B}),
> $$
>
> and when $$\mathbf{B}$$ is the the empty set, we have the distinguished correspondence
>
> $$
> \emptyset \longmapsto \mathbb{C} \mathbf{1},
> $$
>
> where $$\mathbf{1}$$ is the multiplicative identity in the abstract C\*-algebra $$\mathbb{C} \mathbf{1}$$.

The second axiom can be immediately stated:

> **Axiom 2** *(Isotony)* Let $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ be any two basis elements of the Alexandrov topology on a Lorentzian spacetime, i.e. any two sets of the form $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$.
>
> If $$\mathbf{B}_1 \subset \mathbf{B}_2$$ then $$\mathfrak{U}(\mathbf{B}_1) \subset \mathfrak{U}(\mathbf{B}_2)$$, where inclusion is implemented by
>
> $$
> i : \mathfrak{U}(\mathbf{B}_1) \hookrightarrow \mathfrak{U}(\mathbf{B}_2),
> $$
>
> a unital \*-monomorphism.

The next axiom makes use of the following definitions:

**Definition** *(Causal Future and Past)*
Consider a point $$p$$ in a Lorentzian spacetime. The *causal future* of $$p$$ is the set $$J^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like or light-like curve. Similarly, the *causal past* of $$p$$ is the set $$J^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like or light-like curve.

**Definition** *(Spacelike Related)*
Consider two points $$p_1$$ and $$p_2$$ in a Lorentzian spacetime. The points are said to be *spacelike related* if $$p_2 \notin J^+(p_1) \cup J^-(p_1)$$ or equivalently $$p_1 \notin J^+(p_2) \cup J^-(p_2)$$.

**Definition** *(Completely Spacelike)*
Consider two sets $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ in a Lorentzian spacetime. $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ are said to be *completely spacelike* if every $$p_1$$ in $$\mathbf{O}_1$$ is spacelike related to every $$p_2$$ in $$\mathbf{O}_2$$ or equivalently if every $$p_2$$ in $$\mathbf{O}_2$$ is spacelike related to every $$p_1$$ in $$\mathbf{O}_1$$.

and can be stated as follows:

> **Axiom 3** *(Local Commutativity)* Let $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ be any two basis elements of the Alexandrov topology on a Lorentzian spacetime, i.e. any two sets of the form $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$.
>
> If $$\mathbf{B_1}$$ and $$\mathbf{B_2}$$ are completely spacelike and there exists a basis element $$\mathbf{B}$$ such that $$\mathbf{B_1}, \mathbf{B_2} \subseteq \mathbf{B}$$ then $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ commute in the C\*-algebra $$\mathfrak{U}(\mathbf{B})$$, i.e. for any $$a_1$$ in $$\mathfrak{U}(\mathbf{B_1})$$ and $$a_2$$ in $$\mathfrak{U}(\mathbf{B_2})$$ it follows that
>
> $$
> a_1 a_2 - a_2 a_1 = 0
> $$
>
> in the C\*-algebra $$\mathfrak{U}(\mathbf{B})$$.
>
> If no such $$\mathbf{B}$$ exists, then it simply doesn't make sense to consider if $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ commute as they are not in the same algebra.

Again, the definitions required for the next axiom use terminology introduced in the previous blog post [GNS Construction Theorem](https://kellyjdavis.github.io/aqft/gns-construction/). It's strongly recommended that the reader be familiar with the GNS Construction Theorem or read [GNS Construction Theorem](https://kellyjdavis.github.io/aqft/gns-construction/) before proceeding.

That being said, the next axiom has need of the following definition:

**Definition** *(Local Observable)*
For Lorentzian spacetime $$M$$ the image $$\pi_\omega(a)$$ of a self-adjoint member $$a$$ of the local algebra $$\mathfrak{U}(\mathbf{B})$$ under the GNS \*-homomorphism $$\pi_\omega$$ of a state $$\omega$$ on $$\mathfrak{U}(\mathbf{B})$$ is self-adjoint and thus corresponds to an "observable". Any "observable" corresponding to such a self-adjoint $$\pi_\omega(a)$$ is called a *local observable*.

and can be stated as follows:

> **Axiom 4** *(Local Algebra)* All "observables" are local observables.

The final axiom states:

> **Axiom 5** *(Isometric Covariance)* Let $$\mathbf{B}$$ be any basis element of the Alexandrov topology on a Lorentzian spacetime $$M$$, i.e. any set of the form $$I^+(p) \cap I^-(q)$$.
>
> A member $$\varphi$$ of the group of isometries of $$M$$ connected to the identity acts on $$\mathfrak{U}(\mathbf{B})$$ as follows
>
> $$
> \begin{align}
> \alpha_\varphi : \mathfrak{U}(\mathbf{B}) &\longrightarrow \mathfrak{U}(\varphi(\mathbf{B})) \\
>                            a              &\longmapsto     \alpha_\varphi(a)
> \end{align}
$$
>
> where $$\varphi(\mathbf{B})$$ is the image of the basis element $$\mathbf{B}$$ under the isometry $$\varphi$$ and $$\alpha_\varphi$$ is a unital *-isomorphism generated by $$\varphi$$ that for the identity isometry $$\mathbf{1}$$ satisfies
>
> $$
> \alpha_{\mathbf{1}}(a) = a
> $$
>
> and for all appropriate $$a$$, $$\varphi$$, and $$\varphi'$$
>
> $$
> \alpha_{\varphi' \cdot \varphi}(a) = \alpha_{\varphi'}(\alpha_{\varphi}(a)).
> $$

# Introduction to States
In this section we will examine various types of states with the goal of eventually introducing "local isometric invariant states" which are the states of most "physical relevance".

## Abstract C\*-Algebra States
Before introducting the various states associated with AQFT, we will take a moment to remind the reader of the definition of an abstract C\*-algebra state that was introduced in the blog post [GNS Construction Theorem](https://kellyjdavis.github.io/aqft/gns-construction/)

> **Definition** *(State)*
> Let $$\mathfrak{S}$$ be an abstract C\*-algebra. A *state* is an element $$\omega$$ of the dual space $$\mathfrak{S}^*$$ that is
>
> * *Positive* - for any $$a \in \mathfrak{S}$$ we have $$0 \le \omega(a^*a)$$ and
> * *Normalized* - the operator norm satisfies $$\| \omega \|=1$$.
>
> Furthermore, a state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{S}$$, it follows that $$0 < \omega(a^*a)$$.

This definition is critical; all subsequent notions of state associated with AQFT are built upon it.

## States of Algebraic Quantum Field Theory in Minkowski Spacetime
In this section we detail how some notions of state in AQFT in Minkowski spacetime follow "naturally" from the notion of state for an abstract C\*-algebra.

"Local states" in AQFT on Minkowski spacetime are simply abstract C\*-algebra states associated to a local algebra $$\mathfrak{U}(\mathbf{B})$$, where $$\mathbf{B}$$ is a basis element of the Alexandrov topology in Minkowski spacetime. Similarly, "global states" there are abstract C\*-algebra states associated to the quasilocal algebra $$\mathfrak{U}$$.

These are "simple" extensions of the notion of an abstract C\*-algebra state. These extensions start to become interesting only when we examine how they behave under isometries.

### Local States of Algebraic Quantum Field Theory in Minkowski Spacetime
Formally a "local state" of AQFT in Minkowski Spacetime is defined as follows

> **Definition** *(Local State)*
> Let $$\mathbf{B}$$ be any basis element of the Alexandrov topology in Minkowski spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$, and $$\mathfrak{U}(\mathbf{B})$$ its associated abstract C\*-algebra.
>
> A *local state* is an element $$\omega$$ of the dual space $$\mathfrak{U}(\mathbf{B})^*$$ that is
>
> * *Positive* - for any $$a \in \mathfrak{U}(\mathbf{B})$$ we have $$0 \le \omega(a^*a)$$ and
> * *Normalized* - the operator norm satisfies $$\| \omega \|=1$$.
>
> Furthermore, a local state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{U}(\mathbf{B})$$, it follows that $$0 < \omega(a^*a)$$.

Thus a local state is "simply" an abstract C\*-algebra state associated to a local algebra $$\mathfrak{U}(\mathbf{B})$$.

### Global States of Algebraic Quantum Field Theory in Minkowski Spacetime
Similarly, a "global state" of AQFT in Minkowski Spacetime is defined as follows

> **Definition** *(Global State)*
> Let $$\mathfrak{U}$$ be the quasilocal algebra associated with Minkowski spacetime.
>
> A *global state* is an element $$\omega$$ of the dual space $$\mathfrak{U}^*$$ that is
>
> * *Positive* - for any $$a \in \mathfrak{U}$$ we have $$0 \le \omega(a^*a)$$ and
> * *Normalized* - the operator norm satisfies $$\| \omega \|=1$$.
>
> Furthermore, a global state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{U}$$, it follows that $$0 < \omega(a^*a)$$.

So, a global state is just an abstract C\*-algebra state associated to the quasilocal algebra $$\mathfrak{U}$$.

## States of Algebraic Quantum Field Theory in Lorentzian Spacetime
The states associated to AQFT in Lorentzian spacetime also follow "naturally" from the definition of an abstract C\*-algebra state.

"Local states" are abstract C\*-algebra states associated to a local algebra. And in contrast to Minkowski spacetime, there exists no notion of "global states" in Lorentzian spacetime as there exists no quasilocal algebra associated with a general Lorentzian spacetime.

### Local States of Algebraic Quantum Field Theory in Lorentzian Spacetime
Formally a "local state" of AQFT in a Lorentzian spacetime is

> **Definition** *(Local State)*
> Let $$\mathbf{B}$$ be any basis element of the Alexandrov topology in a Lorentzian spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$, and $$\mathfrak{U}(\mathbf{B})$$ its associated abstract C\*-algebra.
>
> A *local state* is an element $$\omega$$ of the dual space $$\mathfrak{U}(\mathbf{B})^*$$ that is
>
> * *Positive* - for any $$a \in \mathfrak{U}(\mathbf{B})$$ we have $$0 \le \omega(a^*a)$$ and
> * *Normalized* - the operator norm satisfies $$\| \omega \|=1$$.
>
> Furthermore, a local state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{U}(\mathbf{B})$$, it follows that $$0 < \omega(a^*a)$$.

So a local state is just an abstract C\*-algebra state associated to a local algebra $$\mathfrak{U}(\mathbf{B})$$. Furthermore, as there exists no quasilocal algebra associated with a general Lorentzian spacetime, there is no such thing as a "global state" on a generic Lorentzian spacetime.

# Introduction to Isometric Invariant States
Finally, we've reached the "core" of this blog post, the study of "isometric invariant" states. As one might guess, "isometric invariant" states are local or global states that are "invariant" under spacetime isometries.

These states are interesting for many reasons. For example, they provide a canonical example of how one can create a state "invariant" under a given classical symmetry. Critically, "isometric invariant" states, with some additional properties, can also serve as AQFT vacua. In addition, they provide a laboratory in which to examine aspects of spontaneous symmetry breaking: e.g. Are the classical spacetime isometries broken by a quantum state?

With this as motivation, let's jump right in!

## Global, Isometric Invariant States in Minkowski Spacetime
We begin with global, "isometric invariant" states in Minkowski spacetime. They are, in some sense, the "simplest" "isometric invariant" states. However, a careful examination of such  global, "isometric invariant" states in Minkowski spacetime clarifies essentially all subtleties that arise in other cases.

### Isometries of the Quasilocal Algebra
"Morally", as the metric doesn't change under and isometry, an isometry $$L$$ of Minkowski spacetime, in particular a member  of the inhomogeneous Lorentz group connected to the identity, should generate an associated unital \*-automorphism $$\alpha_L$$ of the quasilocal algebra $$\mathfrak{U}$$

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

and a global, "isometric invariant" state should be a global state $$\omega$$ that is invariant with respect to this unital \*-automorphism

$$
\omega(a) = \omega(\alpha_L(a)).
$$

While "morally" this is indeed the case, the problem one immediately encounters is that Axiom 5 (Lorentz Covariance) states only

> **Axiom 5** *(Lorentz Covariance)* Let $$\mathbf{B}$$ be any basis element of the Alexandrov topology on Minkowski spacetime, i.e. any set of the form $$I^+(p) \cap I^-(q)$$.
>
> A member $$L$$ of the inhomogeneous Lorentz group connected to the identity acts on $$\mathfrak{U}(\mathbf{B})$$ as follows
>
> $$
> \begin{align}
> \alpha_L : \mathfrak{U}(\mathbf{B}) &\longrightarrow \mathfrak{U}(L\mathbf{B}) \\
>                      a              &\longmapsto     \alpha_L(a)
> \end{align}
> $$
>
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital *-isomorphism generated by $$L$$ that satisfies for the Lorentz group identity $$\mathbf{1}$$
>
> $$
> \alpha_{\mathbf{1}}(a) = a
> $$
>
> and for all appropriate $$a$$, $$L$$, and $$L'$$
>
> $$
> \alpha_{L' \cdot L}(a) = \alpha_{L'}(\alpha_{L}(a)).
> $$

So, the unital \*-automorphism

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

isn't defined by this axiom. Our first task, then, is to define this unital \*-automorphism.

This task begins by recounting the definition of the quasilocal algebra

**Definition** *(Quasilocal Algebra)*
Consider the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$. As proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), this set-theoretic union is a normed \*-algebra. Also, as proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), its completion yields a C\*-algebra, denoted as $$\mathfrak{U}$$. This C\*-algebra $$\mathfrak{U}$$ is called the *quasilocal algebra*.

This implies that the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$ is dense in $$\mathfrak{U}$$. Hence, if we can define $$\alpha_L$$ on this set-theoretic union, then we should be able to employ the Bounded Linear Transformation Theorem (Theorem A.36 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Theorem** *(Bounded Linear Transformation Theorem)*
> *Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.*

to extend $$\alpha_L$$ to the entire quasilocal algebra, the desired result. It is to this argument we now turn.

The first step in this argument is to prove the following theorem

> **Theorem**
> On Minkowski spacetime let $$L$$ be any member of the inhomogeneous Lorentz group that is connected to the identity. Then there exists a map
>
> $$
> \alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
> $$
>
> from the set theoretic union over a countable basis
>
> $$
> \{ \mathbf{B}_i \}_{i \in \mathbb{N}}
> $$
>
> of the Alexandrov topology to the quasilocal algebra $$\mathfrak{U}$$ such that: (1) The map $$\alpha_L$$ is linear; (2) The map $$\alpha_L$$ is bounded; and (3) The restriction of $$\alpha_L$$ to any $$\mathfrak{U}(\mathbf{B}_i)$$
>
> $$
> \begin{align}
> \left. \alpha_L\right|_{\mathfrak{U}(\mathbf{B}_i)} : \mathfrak{U}(\mathbf{B}_i) &\longrightarrow \mathfrak{U}(L\mathbf{B}_i) \\
>                                                  a              &\longmapsto     \left.\alpha_L\right|_{\mathfrak{U}(\mathbf{B}_i)}(a)
> \end{align}
> $$
>
> is the map that appears in Axiom 5 (Lorentz Covariance).

**Proof**
Let us start by proving the existence of a countable basis

$$
\{ \mathbf{B}_i \}_{i \in \mathbb{N}}
$$

of the Alexandrov topology. In other words, let us prove the lemma

> **Lemma**
> A countable basis $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ of the Alexandrov topology exists on Minkowski spacetime.

**Proof**
Let $$E_r(p)$$ be a Euclidian open ball in Minkowski spacetime centered at $$p$$ and with radius $$r$$. The set

$$
\{ E_r(p) : r \in \mathbb{Q} \text{ and } p \in \mathbb{Q}^4 \}
$$

is a countable basis $$\{ \mathbf{E}_i \}_{i \in \mathbb{N}}$$ of the Euclidian topology on Minkowski spacetime (Example 2.49 [Lee](https://doi.org/10.1007/978-1-4419-7940-7)). Thus, by definition, the Euclidian topology of Minkowski spacetime is second countable.

Sets of the form $$I^+(p) \cap I^{-}(q)$$ form an uncountable a basis $$\{ \mathbf{B}_{\iota} \}_{\iota \in \mathcal{I}}$$ of the Alexandrov topology (Definition 4.22 of [Penrose](https://doi.org/10.1137/1.9781611970609)). Furthermore, as proven by Penrose, the Alexandrov and Euclidian topology of Minkowski spacetime are equivalent (Paragraph 4.23 of [Penrose](https://doi.org/10.1137/1.9781611970609)). Hence, $$\{ \mathbf{B}_{\iota} \}_{\iota \in \mathcal{I}}$$ forms a basis for the Euclidian topology. Thus the definition of basis implies that for any given $$\mathbf{E}_i$$ one has

$$
\mathbf{E}_i = \bigcup\limits_{\mathbf{B}_\iota \in \mathbf{B}(\mathbf{E}_i)} \mathbf{B}_\iota,
$$

where $$\mathbf{B}(\mathbf{E}_i)$$ is the set of all $$\mathbf{B}_\iota$$ in $$\{ \mathbf{B}_{\iota} \}_{\iota \in \mathcal{I}}$$ that are subsets $$\mathbf{B}_\iota \subseteq \mathbf{E}_i$$ of $$\mathbf{E}_i$$.

Now any open subset $$U$$ of a second countable space $$X$$ is second countable, just discard all basis elements of $$X$$ not contained in $$U$$. Thus, $$\mathbf{E}_i$$ is second countable.

Now if we recall the standard theorem (Theorem 2.50 [Lee](https://doi.org/10.1007/978-1-4419-7940-7))

> **Theorem** *(Properties of Second Countable Spaces)*
> Suppose $$X$$ is a second countable space.
>
> 1. $$X$$ is first countable
> 2. $$X$$ contains a countable, dense subset.
> 3. Every open cover of $$X$$ has a countable subcover.

We see that the fact that $$\mathbf{E}_i$$ is second contable and $$\mathbf{B}(\mathbf{E}_i)$$ is an open cover of $$\mathbf{E}_i$$ imply that $$\mathbf{E}_i$$ has a countable subcover consisting of basis elements $$\mathbf{B}_\iota \in \mathbf{B}(\mathbf{E}_i)$$ of the Alexandrov topology.

As the basis $$\{ \mathbf{E}_i \}_{i \in \mathbb{N}}$$ is countable and each $$\mathbf{E}_i$$ admits a countable cover of basis elements of the Alexandrov topology, it follows that there is a countable $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ cover of the $$\{ \mathbf{E}_i \}_{i \in \mathbb{N}}$$.

Obviously every element $$\mathbf{B}_i$$ of $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ is open. Furthermore, as $$\{ \mathbf{E}_i \}_{i \in \mathbb{N}}$$ is a basis the definition of a basis implies that any open set is a union of elements of $$\{ \mathbf{E}_i \}_{i \in \mathbb{N}}$$. As each $$\mathbf{E}_i$$ is a union of elements of $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$, this implies that any open set is a union of elements of $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$.

These two facts (1) every element $$\mathbf{B}_i$$ of $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ is open and (2) any open set is a union of elements of $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$, imply that $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ is a countable basis of the Alexandrov topology, the desired result. $$\blacksquare$$

With that preliminary step completed, let us now move onto the first proper element of the proof. We will now prove by induction that there exists a linear map $$\alpha_L$$ of the desired form

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U},
$$

where the $$\mathbf{B}_i$$ are elements of the countable basis of the Alexandrov topology.

Let us start with the base case.

Let $$\mathbf{B}_1$$ be an element of the countable basis of the Alexandrov topology. As a result of Axiom 5 (Lorentz Covariance), for any member $$L$$ of the inhomogeneous Lorentz group that is connected to the identity we have the map

$$
\alpha_L : \mathfrak{U}(\mathbf{B}_1) \longrightarrow \mathfrak{U}(L\mathbf{B}_1)
$$

where $$\alpha_L$$ is a unital \*-isomorphism and is thus linear. The definition of the quasilocal algebra $$\mathfrak{U}$$ implies that $$\mathfrak{U}(L\mathbf{B}_1) \subseteq \mathfrak{U}$$. Hence, viewing the range $$\mathfrak{U}(L\mathbf{B}_1)$$ of $$\alpha_L$$ as a subset of $$\mathfrak{U}$$, we have a map

$$
\alpha_L : \bigcup\limits_{i \in \{1\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

of the desired form, i.e. linear and with the proper restriction.

Now let us prove the inductive case.

Assume that for $$n$$ in $$\mathbb{N}$$ there exists a map

$$
\alpha_L : \bigcup\limits_{i \in \{1,\ldots,n\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U},
$$

of the desired form, i.e. a linear map that restricts to the unital \*-isomorphisms that appear in Axiom 5 (Lorentz Covariance). We must prove that this implies that there exists a map

$$
\alpha_L : \bigcup\limits_{i \in \{1,\ldots,n+1\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

of the desired form.

Consider any element $$\mathbf{B}_{n+1}$$ of the countable basis of the Alexandrov topology that is different from the first $$n$$ we are already considering. As we are in Minkowski spacetime, there exists[^1] an element $$\mathbf{B}$$ in the uncountable a basis $$\{ \mathbf{B}_{\iota} \}_{\iota \in \mathcal{I}}$$ of the Alexandrov topology such that $$\mathbf{B}_1, \ldots, \mathbf{B}_{n+1} \subseteq \mathbf{B}$$. As a result of Axiom 5 (Lorentz Covariance) there exists a map

$$
\alpha_L : \mathfrak{U}(\mathbf{B}) \longrightarrow \mathfrak{U}(L\mathbf{B})
$$

where $$\alpha_L$$ is a unital \*-isomorphism and is thus linear. As $$\mathbf{B}_1, \ldots, \mathbf{B}_{n+1} \subseteq \mathbf{B}$$, Axiom 2 (Isotony) implies

$$
\bigcup\limits_{i \in \{1,\ldots,n+1\}} \mathfrak{U}(\mathbf{B}_i) \subseteq \mathfrak{U}(\mathbf{B}).
$$

Thus restriction of $$\alpha_L$$ to the above subdomain of $$\mathfrak{U}(\mathbf{B})$$ gives the map

$$
\alpha_L : \bigcup\limits_{i \in \{1,\ldots,n+1\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}(L\mathbf{B}).
$$

The definition of the quasilocal algebra $$\mathfrak{U}$$ implies that $$\mathfrak{U}(L\mathbf{B}) \subseteq \mathfrak{U}$$. Hence, as above, viewing $$\mathfrak{U}(L\mathbf{B})$$ as a subset of $$\mathfrak{U}$$ leads to the map

$$
\alpha_L : \bigcup\limits_{i \in \{1,\ldots,n+1\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

that obviously has the desired form, i.e. a linear map that restricts to the unital \*-isomorphism that appear in Axiom 5 (Lorentz Covariance). This completes the proof of the recursive case.

So with this we have proven that there exists a map

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U},
$$

of the desired form, where the $$\mathbf{B}_i$$ are elements of the countable basis of the Alexandrov topology.

Now let us prove that our map

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U},
$$

is bounded.

We begin this part of the proof by proving the following lemma

> **Lemma** *(Spectral Equivalence)*
> Let $$\mathfrak{U}_1$$ and $$\mathfrak{U}_2$$ be unital C\*-algebras, $$\alpha: \mathfrak{U} \rightarrow \mathfrak{U}_2$$ a unital \*-monomorphism where $$\mathfrak{U} \subseteq \mathfrak{U}_1$$, and $$a_1$$ an arbitrary element of $$\mathfrak{U}$$.
>
> Then it follows that
>
> $$
> \sigma(\alpha(a_1)) = \sigma(a_1).
> $$
>
> In other words, the specturm of $$\sigma(\alpha(a_1))$$ of $$\alpha(a_1)$$ in $$\mathfrak{U}_2$$ is equivalent to the specturm $$\sigma(a_1)$$ of $$a_1$$ in $$\mathfrak{U}_1$$.

**Proof**
Consider $$\lambda \notin \sigma(a_1)$$. The definition of spectrum then implies that  $$(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})$$ is invertible in $$\mathfrak{U}_1$$. Let $$(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}$$ be that inverse. As $$\alpha$$ is a unital \*-monomorphism

$$
\begin{align}
\alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})\right) \alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}\right)
  &= \alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}\right) \\
  &= \alpha(\mathbf{1}_{\mathfrak{U}_1}) \\
  &= \mathbf{1}_{\mathfrak{U}_2}.
\end{align}
$$

Similarly, as $$\alpha$$ is a unital \*-monomorphism

$$
\begin{align}
\alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})\right)
  &= \alpha(a_1) - \alpha(\lambda \mathbf{1}_{\mathfrak{U}_1}) \\
  &= \alpha(a_1) - \lambda \alpha(\mathbf{1}_{\mathfrak{U}_1}) \\
  &= \alpha(a_1) - \lambda \mathbf{1}_{\mathfrak{U}_2}.
\end{align}
$$

Combining the previous two derivations

$$
\left( \alpha(a_1) - \lambda \mathbf{1}_{\mathfrak{U}_2} \right) \alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}\right) = \mathbf{1}_{\mathfrak{U}_2}.
$$

Thus, $$(\alpha(a_1) - \lambda \mathbf{1}_{\mathfrak{U}_2})$$ is invertible in $$\mathfrak{U}_2$$, and thus $$\lambda \notin \sigma(\alpha(a_1))$$. This then implies

$$
\sigma(\alpha(a_1)) \subseteq \sigma(a_1).
$$

Now as $$\alpha$$ is a unital \*-monomorphism, it follows that when $$\alpha$$ is restricted to domain $$\mathfrak{U}$$ and range $$\alpha(\mathfrak{U})$$, it is invertible. Thus

$$
\alpha^{-1} : \alpha(\mathfrak{U}) \rightarrow \mathfrak{U}
$$

is well-defined. Thus,

$$
\alpha^{-1} : \alpha(\mathfrak{U}) \rightarrow \mathfrak{U}_1,$$

where $$\alpha(\mathfrak{U}) \subseteq \mathfrak{U}_2$$, is a unital \*-monomorphism. Hence, we can repeat the above argument using $$\alpha^{-1}$$ with domain $$\alpha(\mathfrak{U})$$ to conclude

$$
\sigma(a_1) \subseteq \sigma(\alpha(a_1)).
$$

So, we have proven that $$\sigma(\alpha(a_1)) \subseteq \sigma(a_1)$$ and that $$\sigma(a_1) \subseteq \sigma(\alpha(a_1))$$. Together these imply the desired result $$\sigma(\alpha(a_1)) = \sigma(a_1)$$. $$\blacksquare$$

The next result we need to establish on the road to proving that $$\alpha_L$$ is bounded is the following

> **Lemma**
> Let $$\mathfrak{U}_1$$ and $$\mathfrak{U}_2$$ be unital C\*-algebras, $$\alpha: \mathfrak{U} \rightarrow \mathfrak{U}_2$$ a unital \*-monomorphism where $$\mathfrak{U} \subseteq \mathfrak{U}_1$$, and $$a_1$$ an arbitrary self-adjoint element of $$\mathfrak{U}$$.
>
> Then it follows that
>
> $$
> \|\alpha(a_1)\| = \|a_1\|
> $$

**Proof**
Recall the followiing lemma (Lemma 8.1 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Lemma**
> If $$a$$ is a self-adjoint member of a unital C\*-algebra, then its norm $$\|a\|$$ is equivalent to its spectral radius $$r(a)$$, i.e.
>
> $$
> \|a\| = r(a).
> $$

Hence,

$$
\|a_1\| = r(a_1)
$$

as a result of this lemma.

As $$\alpha$$ is a unital \*-monomorphism and $$a_1$$ is self-adjoint

$$
\alpha(a_1) = \alpha(a_1^*) = \alpha(a_1)^*,
$$

i.e. $$\alpha(a_1)$$ is also self-adjoint. Hence, the previous lemma implies

$$
\|\alpha(a_1)\| = r(\alpha(a_1)).
$$

Now the definition of spectral radius along with our Spectral Equivalence Theorem imply

$$
r(\alpha(a_1)) \equiv \sup\{|\lambda| : \lambda \in \sigma(\alpha(a_1))\} = \sup\{|\lambda| : \lambda \in \sigma(a_1)\} \equiv r(a_0).
$$

Thus $$r(\alpha(a_1)) = r(a_0)$$. This along with $$\|\alpha(a_1)\| = r(\alpha(a_1))$$ and $$\|a_1\| = r(a_1)$$ imply

$$
\|\alpha(a_1)\| = \|a_1\|,
$$

the desired result. $$\blacksquare$$

As proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)) the quasilocal algebra $$\mathfrak{U}$$ is a C\*-algebra. Also, the definition of the quasilocal algebra $$\mathfrak{U}$$ implies

$$
\bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \subseteq \mathfrak{U}.
$$

Furthermore, Axiom 2 (Isotony), Axiom 5 (Lorentz Covariance), and our construction of the map

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

imply that this map $$\alpha_L$$ is a unital *-monomorphism. Hence, we can apply the previous lemma to an arbitrary self-adjoint element $$b$$

$$
b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i)
$$

to conclude that $$\|\alpha_L(b)\|=\|b\|$$.

However, not all elements we need to consider in this union are self-adjoint. But it turns out that every element $$a$$

$$
a \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i)
$$

in this union can be written as the sum of self-adjoint elements

$$
a = \left( \frac{a + a^*}{2} \right) + i \left( \frac{a - a^*}{2i} \right),
$$

where both

$$
\left( \frac{a + a^*}{2} \right) \text{ and } \left( \frac{a - a^*}{2i} \right)
$$

are self-adjoint. Our previous result, proving $$\alpha_L$$ is linear, then implies

$$
\alpha_L(a) = \alpha_L \left( \frac{a + a^*}{2} \right) + i \alpha_L\left( \frac{a - a^*}{2i} \right).
$$

Thus as a result of our previous lemma

$$
\begin{align}
\|\alpha_L(a)\|
  &= \left\| \alpha_L \left( \frac{a + a^*}{2} \right) + i \alpha_L\left( \frac{a - a^*}{2i} \right) \right\| \\
  &\le \left\| \alpha_L \left( \frac{a + a^*}{2} \right) \right\| + \left\| i \alpha_L\left( \frac{a - a^*}{2i} \right) \right\| \\
  &= \left\| \alpha_L \left( \frac{a + a^*}{2} \right) \right\| + \left\| \alpha_L\left( \frac{a - a^*}{2i} \right) \right\| \\
  &= \left\| \frac{a + a^*}{2} \right\| + \left\| \frac{a - a^*}{2i} \right\|.
\end{align}
$$

Now, by definition

$$
\|\alpha_L\| \equiv \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \|\alpha_L(a)\|.
$$

Using the results of the last paragraph this becomes

$$
\begin{align}
\|\alpha_L\|
  &\equiv \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \|\alpha_L(a)\| \\
  &\le \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \left\| \frac{a + a^*}{2} \right\| + \left\| \frac{a - a^*}{2i} \right\| \\
  &\le \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \frac{\|a\| + \|a^*\|}{2} + \frac{\|a\| + \|a^*\|}{2} \\
  &= \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \|a\| + \|a^*\| \\
  &= \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} \|a\| + \|a\| \\
  &= \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} 2\|a\| \\
  &= \sup\limits_{a \in \{b \in \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) : \|b\| = 1\}} 2 \\
  &= 2.
\end{align}
$$

In other words $$\|\alpha_L\| \le 2$$ and thus $$\alpha_L$$ is bounded, the second desired result.

The final desired result---i.e. the restriction of $$\alpha_L$$ to any $$\mathfrak{U}(\mathbf{B}_i)$$

$$
\begin{align}
\left. \alpha_L\right|_{\mathfrak{U}(\mathbf{B}_i)} : \mathfrak{U}(\mathbf{B}_i) &\longrightarrow \mathfrak{U}(L\mathbf{B}_i) \\
                                                 a              &\longmapsto     \left.\alpha_L\right|_{\mathfrak{U}(\mathbf{B}_i)}(a)
\end{align}
$$

is the map that appears in Axiom 5 (Lorentz Covariance)---follows obviously from our construction of $$\alpha_L$$. $$\blacksquare$$

So, as we have established that our $$\alpha_L$$ is linear, bounded, and reduces to $$\alpha_L$$ from Axiom 5 (Lorentz Covariance) in the appropriate limit, we now want to apply the Bounded Linear Transformation Theorem (Theorem A.36 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Theorem** *(Bounded Linear Transformation Theorem)*
> *Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.*

to uniquely extend

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

to

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

as a unital *-automorphism.

In applying this theorem $$\mathfrak{U}$$, being a C\*-algebra and thus normed space, takes on the role of $$V_1$$. Similarly, $$\mathfrak{U}$$, being a C\*-algebra and thus Banach space, also takes on the role of $$V_2$$. In addition $$\alpha_L$$, being bounded and linear, takes on the role of $$T$$. Finally, we want

$$
\bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i)
$$

to take on the role of $$W$$. However, we haven't proven that it is dense in $$\mathfrak{U}$$. Let us prove that this is the case.

The definition of the quasilocal algebra $$\mathfrak{U}$$ implies that the union

$$
\bigcup\limits_{\iota \in \mathcal{I}} \mathfrak{U}(\mathbf{B}_\iota)
$$

over the uncountable basis elements $$\mathbf{B}_\iota$$ is dense in $$\mathfrak{U}$$. As each $$\mathbf{B}_\iota$$ is open the definition of a basis implies that

$$
\mathbf{B}_\iota = \bigcup_{\mathbf{B}_i \in \mathbf{B}(\mathbf{B}_\iota)} \mathbf{B}_i
$$

where $$\mathbf{B}(\mathbf{B}_\iota)$$ is the set of $$\mathbf{B}_i$$ in $$\{ \mathbf{B}_i \}_{i \in \mathbb{N}}$$ that are subsets $$\mathbf{B}_i \subseteq \mathbf{B}_\iota$$ of $$\mathbf{B}_\iota$$. Hence

$$
\bigcup\limits_{\iota \in \mathcal{I}} \mathfrak{U}(\mathbf{B}_\iota) = \bigcup\limits_{\iota \in \mathcal{I}} \left( \bigcup_{\mathbf{B}_i \in \mathbf{B}(\mathbf{B}_\iota)} \mathbf{B}_i \right) \subseteq \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i),
$$

where the final subset relation follows from the fact that the iterated union can at most contain all elements $$\mathbf{B}_i$$ of the countable basis. Hence, as

$$
\bigcup\limits_{\iota \in \mathcal{I}} \mathfrak{U}(\mathbf{B}_\iota)
$$

is dense in $$\mathfrak{U}$$ and

$$
\bigcup\limits_{\iota \in \mathcal{I}} \mathfrak{U}(\mathbf{B}_\iota) \subseteq \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i)
$$

it follows that

$$
\bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i)
$$

is dense in $$\mathfrak{U}$$ and can thus take on the role of $$W$$ in the theorem.

With this we can then apply the Bounded Linear Transformation Theorem and uniquely extend

$$
\alpha_L : \bigcup\limits_{i \in \mathbb{N}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

to

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

as a unital *-automorphism, the desired result of this section.

### Definition of Global, Isometric Invariant States
As we have established the definition of the unital *-automorphism

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

corresponding to any member $$L$$ of the inhomogeneous Lorentz group that is connected to the identity, we are now in the position to define a global "isometric invariant" states

> **Definition** *(Global Isometric Invariant State)*
> Let $$\mathfrak{U}$$ be the quasilocal algebra associated with Minkowski spacetime.
>
> A *global isometric invariant state* is global state $$\omega$$ such that for any $$a$$ in the quasilocal algebra $$\mathfrak{U}$$ and any $$L$$ in the inhomogeneous Lorentz group connected to the identity one has
>
> $$
> \omega(a) = \omega(\alpha_L(a))
> $$
>
> where $$\alpha_L$$ is the unital *-automorphism defined in the the previous section
>
> $$
> \alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
> $$
>
> corresponding to $$L$$.
>
> Furthermore, a global isometric invariant state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{U}$$, it follows that $$0 < \omega(a^*a)$$.

This is the "natural" definition that flows from everything up until this point. However, examining what this definition implies for a given "local" algebra $$\mathfrak{U}(\mathbf{B}_i)$$, where $$\mathbf{B}_i$$ is from the countable basis, aids in understanding subsequent definitions of local "isometric invariant" states.

So, to that end, consider an arbitrary element $$\mathbf{B}_i$$ from the countable basis of the Alexandrov topology. Axiom 1 (Local Algebras) associates to $$\mathbf{B}_i$$ the abstract C\*-algebra $$\mathfrak{U}(\mathbf{B}_i)$$. For any $$L$$ in the inhomogeneous Lorentz group connected to the identity Axiom 5 (Lorentz Covariance) defines the unital *-isomorphisim

$$
\alpha_L : \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}(L\mathbf{B}_i).
$$

As we've proven above, $$\alpha_L$$ acting on the quasilocal algebra $$\mathfrak{U}$$ restricts to this "local" $$\alpha_L$$.

Let $$\omega$$ be a global isometric invariant state. By restriction $$\omega$$ defines elements

$$
\begin{align}
\omega|_{\mathfrak{U}(\mathbf{B}_i)} \quad \text{and} \quad \omega|_{\mathfrak{U}(L\mathbf{B}_i)}
\end{align}
$$

of the dual spaces of $$\mathfrak{U}(\mathbf{B}_i)^*$$ and $$\mathfrak{U}(L\mathbf{B}_i)^*$$ respectively. Using the unital *-isomorphisim

$$
\alpha_L : \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}(L\mathbf{B}_i)
$$

we can pull-back to $$\mathfrak{U}(\mathbf{B}_i)$$ the restriction of $$\omega$$ to $$\mathfrak{U}(L\mathbf{B}_i)$$ as follows

$$
\left( \omega|_{\mathfrak{U}(L\mathbf{B}_i)} \right)^*(a) \equiv \omega|_{\mathfrak{U}(L\mathbf{B}_i)}(\alpha_L(a)),
$$

where $$a$$ is an arbitrary element of $$\mathfrak{U}(\mathbf{B}_i)$$. As $$\omega$$ is a global isometric invariant state, it follows that

$$
\omega|_{\mathfrak{U}(\mathbf{B}_i)}(a) = \left( \omega|_{\mathfrak{U}(L\mathbf{B}_i)} \right)^*(a)
$$

for an arbitrary element $$a$$ of $$\mathfrak{U}(\mathbf{B}_i)$$. This is a "local" manifestation of isometric invariance of $$\omega$$, and, as we shall see, it is this condition that plays a key role in defining local "isometric invariant" states.

## Local, Isometric Invariant States in Minkowski Spacetime
Global isometric invariant states in Minkowski spacetime defined, we can proceed to define local "isometric invariant" states in Minkowski spacetime. Our careful examination of implications global isometric invariant states had for "local" algebras will pay dividends in this section, simplifying and clarifying definitions and the presentation.

### Definition of Local, Isometric Invariant States
Let's jump right in with the definition

> **Definition** *(Local Isometric Invariant State)*
> Let $$\mathbf{B}$$ be an arbitrary basis element of the Alexandrov topology on Minkowski spacetime and $$\mathfrak{U}(\mathbf{B})$$ the abstract C\*-algebra associated with $$\mathbf{B}$$ via Axiom 1 (Local Algebras).
>
> A *local isometric invariant state* on $$\mathbf{B}$$ is a local state $$\omega$$ on $$\mathbf{B}$$ such that for any $$a$$ in $$\mathfrak{U}(\mathbf{B})$$ and any pair $$(L, \mathbf{B}_\iota)$$ where $$L$$ is in the inhomogeneous Lorentz group connected to the identity and $$\mathbf{B}_\iota$$ is a basis element of the Alexandrov topology such that $$\mathbf{B}_\iota, L\mathbf{B}_\iota \subseteq \mathbf{B}$$, one has
>
> $$
> \omega|_{\mathfrak{U}(\mathbf{B}_\iota)}(a) = \left( \omega|_{\mathfrak{U}(L\mathbf{B}_\iota)} \right)^*(a),
> $$
>
> where
>
> $$
> \begin{align}
> \omega|_{\mathfrak{U}(\mathbf{B}_\iota)} \quad \text{and} \quad \omega|_{\mathfrak{U}(L\mathbf{B}_\iota)}
> \end{align}
> $$
>
> are the restrictions of $$\omega$$ and
>
> $$
> \left( \omega|_{\mathfrak{U}(L\mathbf{B}_\iota)} \right)^*(a) \equiv \omega|_{\mathfrak{U}(L\mathbf{B}_\iota)}(\alpha_L(a))
> $$
>
> is the pull-back via the unital \*-isomorphism $$\alpha_L$$ of Axiom 5 (Lorentz Covariance).

In light of our examination of the implications global isometric invariant states had on "local" algebras, this is exactly what would one expect as a definition. It treats $$\mathbf{B}$$ in the same manner as the entire Minkowski spacetime was treated in the global case.

## Local, Isometric Invariant States in Lorentzian Spacetime
As there is no quasilocal algebra associated with a generic Lorentzian spacetime, we begin not by defining global "isometric invariant" states but by defining local "isometric invariant" states.

### Definition of Local, Isometric Invariant States
A Minkowski spacetime is a Lorentzian spacetime, one with far more symmetries than a generic Lorentzian spacetime but none-the-less a Lorentzian spacetime.

So, whatever definition is put forward for a local "isometric invariant" state in Lorentzian spacetime, it should reduce to the definition of a local isometric invariant state in Minkowski spacetime in the proper limit.

This alone is enough for us to introduce the following

> **Definition** *(Local Isometric Invariant State)*
> Let $$\mathbf{B}$$ be an arbitrary basis element of the Alexandrov topology in a Lorentzian spacetime $$M$$ and $$\mathfrak{U}(\mathbf{B})$$ the abstract C\*-algebra associated with $$\mathbf{B}$$ via Axiom 1 (Local Algebras).
>
> A *local isometric invariant state* on $$\mathbf{B}$$ is a local state $$\omega$$ on $$\mathbf{B}$$ such that for any $$a$$ in $$\mathfrak{U}(\mathbf{B})$$ and any pair $$(\varphi, \mathbf{B}_\iota)$$ where $$\varphi$$ is a member of the group of isometries of $$M$$ connected to the identity and $$\mathbf{B}_\iota$$ is a basis element of the Alexandrov topology such that $$\mathbf{B}_\iota, \varphi(\mathbf{B}_\iota) \subseteq \mathbf{B}$$, one has
>
> $$
> \omega|_{\mathfrak{U}(\mathbf{B}_\iota)}(a) = \left( \omega|_{\mathfrak{U}(\varphi(\mathbf{B}_\iota))} \right)^*(a),
> $$
>
> where
>
> $$
> \begin{align}
> \omega|_{\mathfrak{U}(\mathbf{B}_\iota)} \quad \text{and} \quad \omega|_{\mathfrak{U}(\varphi(\mathbf{B}_\iota))}
> \end{align}
> $$
>
> are the restrictions of $$\omega$$ and
>
> $$
> \left( \omega|_{\mathfrak{U}(\varphi(\mathbf{B}_\iota))} \right)^*(a) \equiv \omega|_{\mathfrak{U}(\varphi(\mathbf{B}_\iota))}(\alpha_\varphi(a))
> $$
>
> is the pull-back via the unital \*-isomorphism $$\alpha_\varphi$$ of Axiom 5 (Isometric Covariance).

Obviously, this reduces to a local isometric invariant state in Minkowski spacetime in the proper limit. Hence, it seems like the "natural" generalization to Lorentzian spacetime.

# Summary
We've covered alot of ground.

We've introduced the notion of states on abstract C\*-algebras. Then, using many key results from the AQFT axioms, we were able to generalize such states to global and local states on Minkowski spacetime and global and local isometric invariant states also on Minkowski spacetime.

Motivated by the Minkowski case, we also introduced the notion of local states and local isometric invariant states on Lorentzian spacetime. (As there is no quasilocal algebra on a generic Lorentzian spacetime, there is no analog of a global state or a global isometric invariant state there.)

What we haven't done here however is prove if global and/or local isometric invariant states on Minkowski spacetime exist. Similarly, we didn't prove local isometric invariant states on Lorentzian spacetime exist either.

Unfortunately, such existence questions are relatively complex and would have made this blog post unbearably long. So we reserve these existence questions for a future blog post.

[^1]: Note such a $$\mathbf{B}$$ need not exist on a general Lorentzian spacetime. This is special to Minkowski spacetime.
