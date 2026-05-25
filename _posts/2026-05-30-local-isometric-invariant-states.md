---
title:  "Local, Isometric Invariant States"
date:   2026-05-30 06:53:53 +0200
categories: aqft lcaqft
---

This blog post introduces the notion of "local, isometric invariant states" in Algebraic Quantum Field Theory (AQFT) in Minkowski spacetime (a theory defined in [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)) and also does the same for AQFT in Lorentzian spacetime (a theory defined in [Haag Kastler Axioms in Curved Spacetime](https://kellyjdavis.github.io/aqft/lcaqft/haag-kastler-axioms-curved-spacetime/)). Such "local, isometric invariant states" capture the physics of quantum systems that are invariant under isometries and that "reside" in bounded regions of spacetime.

# Reveiw of Algebraic Quantum Field Theory
Instead of diving headlong into a definition of "local, isometric invariant states", we will begin with a review of AQFT in Minkowski spacetime and AQFT in Lorentzian spacetime.

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

That said, to state the next axiom we make use of the following definition

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
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital *-isomorphism generated by $$L$$.

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

> **Axiom 3** *(Local Commutativity)* Let $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ be any two basis elements of the Alexandrov topology on Lorentzian spacetime, i.e. any two sets of the form $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$.
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

That being said, the next axiom has need of the following definition

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
> where $$\varphi(\mathbf{B})$$ is the image of the basis element $$\mathbf{B}$$ under the isometry $$\varphi$$ and $$\alpha_\varphi$$ is a unital *-isomorphism generated by $$\varphi$$.

# Introduction to States
In this section we will examine various types of states with the goal of eventually introducing "local, isometric invariant states" which are the states of most "physical relevance".

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
Finally, we've reached the "core" of this blog post, the study of "isometric invariant states". As one might guess, "isometric invariant states" are local or global states that are "invariant" under isometries of the ambient spacetime.

These states are interesting for many reasons. For example, they are a canonical example of how to create a state "invariant" under a given classical symmetry. Critically, "isometric invariant states", with some additionaly properties, can also serve as AQFT vacua. In addition, they provide a laboratory in which to examine aspects of spontaneous symmetry breaking: e.g., Are the classical spacetime isometries broken by a quantum state?

With that as motivation, let us jump right in!

## Global, Isometric Invariant States in Minkowski Spacetime
We begin with global, "isometric invariant" states in Minkowski spacetime. They are, in some sense, the "simplest" "isometric invariant" states. However, a careful examination of such  global, "isometric invariant" states in Minkowski spacetime clarifies essentially all subtleties that arise in other cases.

### Quasilocal Algebra Automorphism of a Isometry
"Morally", an isometry $$L$$ of Minkowski spacetime should generate $$\alpha_L$$ an associated unital \*-automorphism of the quasilocal algebra $$\mathfrak{U}$$

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
> \alpha_L : \mathfrak{U}(\mathbf{B}) &\longrightarrow \mathfrak{U}(\mathbf{LB}) \\
>                      a              &\longmapsto     \alpha_L(a)
> \end{align}
> $$
> 
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital *-isomorphism generated by $$L$$.

So, the unital \*-automorphism

$$
\alpha_L : \mathfrak{U} \longrightarrow \mathfrak{U}
$$

isn't even defined. Out first task is thus defining this unital \*-automorphism.

This task begins with the quasilocal algebra definition

**Definition** *(Quasilocal Algebra)*
Consider the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$. As proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), this set-theoretic union is a normed \*-algebra. Also, as proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), its completion yields a C\*-algebra, denoted as $$\mathfrak{U}$$. This C\*-algebra $$\mathfrak{U}$$ is called the *quasilocal algebra*.

This implies that the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$ is dense in $$\mathfrak{U}$$. Hence, if we can define $$\alpha_L$$ on this set-theoretic union, then we should be able to employ the Bounded Linear Transformation Theorem (Theorem A.36 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Theorem** *(Bounded Linear Transformation Theorem)*
> *Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.*

to extend $$\alpha_L$$ to the entire quasilocal algebra, the desired result. It is to this argument we now turn.

As a result of Axiom 5 (Lorentz Covariance), for any two basis element $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ of the Alexandrov topology on Minkowski spacetime we have

$$
\begin{align}
\alpha_L : \mathfrak{U}(\mathbf{B}_1) &\longrightarrow \mathfrak{U}(\mathbf{LB}_1) \\
\alpha_L : \mathfrak{U}(\mathbf{B}_2) &\longrightarrow \mathfrak{U}(\mathbf{LB}_1) 
\end{align}
$$

where $$\alpha_L$$ is a unital \*-isomorphism.

As $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ are basis elements of the Alexandrov topology on Minkowski spacetime, there exists[^1] a basis element $$\mathbf{B}$$ such that $$\mathbf{B}_1, \mathbf{B}_2 \subset \mathbf{B}$$, where again Axiom 5 (Lorentz Covariance) implies

$$
\alpha_L : \mathfrak{U}(\mathbf{B}) \longrightarrow \mathfrak{U}(\mathbf{LB}).
$$

Furthermore, as a result of Axiom 2 (Isotony) $$\mathfrak{U}(\mathbf{B}_1), \mathfrak{U}(\mathbf{B}_2) \subset \mathfrak{U}(\mathbf{B})$$. As a result of continuity of the isometry $$L$$ we have $$\mathbf{LB}_1, \mathbf{LB}_2 \subset \mathbf{LB}$$ and thus as a result of  Axiom 2 (Isotony) $$\mathfrak{U}(\mathbf{LB}_1), \mathfrak{U}(\mathbf{LB}_2) \subset \mathfrak{U}(\mathbf{LB})$$.

So as a result of all this, the unital \*-isomorphism

$$
\alpha_L : \mathfrak{U}(\mathbf{B}) \longrightarrow \mathfrak{U}(\mathbf{LB})
$$

through restriction defines a linear map

$$
\alpha_L : \bigcup_{i \in \{1,2\}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}(\mathbf{LB}).
$$

This general construction can be repeated a finite number of times, defining a linear map

$$
\alpha_L : \bigcup_{i \in \mathcal{T}} \mathfrak{U}(\mathbf{B}_i) \longrightarrow \mathfrak{U}
$$

where $$\mathcal{T}$$ indexes all basis elements of the Alexandrov topology. This extends $$\alpha_L$$ to a linear map on the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$. To apply the Bounded Linear Transformation Theorem to such an $$\alpha_L$$ we must further prove that $$\alpha_L$$ is bounded. It is to this we now turn.

We begin this by proving the followiing result

> **Theorem** *(Spectral Contraction)*
> Let $$\mathfrak{U}_1$$ and $$\mathfrak{U}_2$$ be unital C\*-algebras, $$\alpha: \mathfrak{U}_1 \rightarrow \mathfrak{U}_2$$ a unital \*-morphism, and $$a_1$$ an arbitrary element of $$\mathfrak{U}_1$$.
> 
> Then it follows that
>
> $$
> \sigma(\alpha(a_1)) \subseteq \sigma(a_1).
> $$
>
> In other words, the specturm of $$\sigma(\alpha(a_1))$$ of $$\alpha(a_1)$$ in $$\mathfrak{U}_2$$ is a subset of the specturm $$\sigma(a_1)$$ of $$a_1$$ in $$\mathfrak{U}_1$$.

**Proof**
Consider $$\lambda \notin \sigma(a_1)$$. The definition of spectrum then implies that  $$(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})$$ is invertible in $$\mathfrak{U}_1$$. Let $$(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}$$ be than inverse. As $$\alpha$$ is a unital \*-morphism

$$
\begin{align}
\alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})\right) \alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}\right)
  &= \alpha\left((a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})(a_1 - \lambda \mathbf{1}_{\mathfrak{U}_1})^{-1}\right) \\
  &= \alpha(\mathbf{1}_{\mathfrak{U}_1}) \\
  &= \mathbf{1}_{\mathfrak{U}_2}.
\end{align}
$$

Similarly, as $$\alpha$$ is a unital \*-morphism

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

Thus, $$(\alpha(a_1) - \lambda \mathbf{1}_{\mathfrak{U}_2})$$ is invertible in $$\mathfrak{U}_2$$, and thus $$\lambda \notin \sigma(\alpha(a_1))$$. This then implies the desired result $$\sigma(\alpha(a_1)) \subseteq \sigma(a_1)$$. $$\blacksquare$$

The next result we need to establish on the road to proving that $$\alpha_L$$ is bounded is the following

> **Theorem**
> Let $$\mathfrak{U}_1$$ and $$\mathfrak{U}_2$$ be unital C\*-algebras, $$\alpha: \mathfrak{U}_1 \rightarrow \mathfrak{U}_2$$ a unital \*-morphism, and $$a_1$$ an arbitrary self-adjoint element of $$\mathfrak{U}_1$$.
> 
> Then it follows that
> 
> $$
> \|\alpha(a_1)\| \le \|a_1\|
> $$ 

**Proof**
Recall the followiing lemma (Lemma 8.1 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Lemma**
> If $$a_1$$ is a self-adjoint member of a C\*-algebra, then its norm $$\|a_1\|$$ is equivalent to its spectral radius $$r(a_1)$$, i.e.
> 
> $$
> \|a_1\| = r(a_1)
> $$

Hence,

$$
\|a_1\| = r(a_1)
$$

as a result of this lemma.

As $$\alpha$$ is a \*-morphism and $$a_1$$ is self-adjoint

$$
\alpha(a_1) = \alpha(a_1^*) = \alpha(a_1)^*,
$$

i.e. $$\alpha(a_1)$$ is also self-adjoint. Hence, the previous lemma implies

$$
\|\alpha(a_1)\| = r(\alpha(a_1)).
$$

Now the definition of spectral radius along with our Spectral Contraction Theorem imply

$$
r(\alpha(a_1)) \equiv \sup\{|\lambda| : \lambda \in \sigma(\alpha(a_1))\} \le \sup\{|\lambda| : \lambda \in \sigma(a_1)\} \equiv r(a_0).
$$

Thus $$r(\alpha(a_1)) \le r(a_0)$$. This along with $$\|\alpha(a_1)\| = r(\alpha(a_1))$$ and $$\|a_1\| = r(a_1)$$ implies

$$
\|\alpha(a_1)\| \le \|a_1\|,
$$

the desired result. $$\blacksquare$$


### Definition of Global, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Global, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometric Invariant States in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometric Invariant States in Lorentzian Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

# Summary
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas vitae quam sed ex gravida hendrerit. Curabitur ac ante fringilla, aliquet purus et, commodo justo. Nulla commodo consectetur nisl, eget cursus justo convallis non. Proin a consectetur libero. Proin placerat, turpis quis tristique porta, nibh orci laoreet dolor, non dignissim sem quam vel nisl. Cras metus ligula, mollis ut justo in, sollicitudin tincidunt magna. Nunc molestie pulvinar nibh, ac venenatis odio viverra vulputate. Nunc suscipit dignissim maximus. Ut consectetur condimentum sodales. Ut ultricies leo sed odio semper, a vehicula libero pellentesque.

Ut posuere convallis convallis. Cras fermentum lacinia blandit. Ut posuere ex sed neque porttitor condimentum. Sed ac felis luctus, bibendum velit vitae, sollicitudin dolor. Nunc tristique ante vitae ullamcorper lacinia. Mauris sodales dui at justo ornare porta. Nulla facilisi. Pellentesque vel eleifend risus, ac auctor sapien. Sed pellentesque finibus turpis, et ornare lectus auctor ut. Nulla ut dui tellus. Fusce risus augue, vehicula id convallis at, hendrerit sit amet orci.

Nunc ut imperdiet neque. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Maecenas aliquam nisi eget augue cursus, efficitur egestas ligula bibendum. Suspendisse fringilla mi dictum libero fermentum gravida. Mauris vehicula tortor ac orci aliquam dictum. Mauris ac enim enim. Suspendisse molestie eros et massa volutpat, non convallis arcu posuere. Sed id nunc in lectus tincidunt pellentesque. Nunc vestibulum facilisis ante, vitae vehicula ex. Donec maximus sem a tincidunt vulputate. Sed lacinia molestie mauris, et efficitur nisi dapibus eget. Aliquam vel elit quis dolor laoreet varius.

Nulla vel mollis neque. Proin vulputate nisi nec tellus consequat placerat. Etiam congue diam ante, in posuere sem eleifend vel. Suspendisse potenti. Duis tempus rhoncus mauris, ac dapibus mauris maximus in. Pellentesque finibus sagittis eros eu commodo. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque auctor nibh ut eros aliquam, vel rhoncus sem varius. Nam ac iaculis dolor, eu varius ligula. Sed vel tellus libero. Aenean vel diam at sem vulputate vehicula.

[^1]: Note such a $$\mathbf{B}$$ need not exist on a general Lorentzian spacetime. This is special to Minkowski spacetime.
