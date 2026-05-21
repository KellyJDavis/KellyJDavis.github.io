---
title:  "Local Isometrically Invariant States"
date:   2026-05-20 06:53:53 +0200
categories: aqft lcaqft
---

This blog post introduces the notion of "local, isometrically invariant states" of Algebraic Quantum Field Theory (AQFT) in Minkowski spacetime (a theory defined in [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)) and also does the same for AQFT in Lorentzian spacetime (a theory defined in [Haag Kastler Axioms in Curved Spacetime](https://kellyjdavis.github.io/aqft/lcaqft/haag-kastler-axioms-curved-spacetime/)). Such "local, isometrically invariant states" capture the physics of quantum systems that are invariant under isometries and that "reside" in bounded regions of spacetime.

# Reveiw of Algebraic Quantum Field Theory
Instead of diving headlong into a definition of "local, isometrically invariant states", we will begin with a review of the GNS construction, AQFT in Minkowski spacetime, and AQFT in Lorentzian spacetime.

We will provide a detailed review of the GNS construction as we will have need of these details here and in subsequent blog posts. However, the review of AQFT in Minkowski and Lorentzian spacetime will not provide all details of the blog posts [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/) and [Haag Kastler Axioms in Curved Spacetime](https://kellyjdavis.github.io/aqft/lcaqft/haag-kastler-axioms-curved-spacetime/) where these theories were introduced. The AQFT reviews serve only as a refresher, making sure readers are clear on the various definitions and axioms used in AQFT in Minkowski and Lorentzian spacetimes.

## GNS Construction
In the previous blog post [Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/), a sketch of the GNS construction was presented. However, the details and proof of these results were not provided. Here we rectify that situation, presenting all details of the GNS Construction and its proof following [Entanglement in Algebraic Quantum Field Theories](https://arxiv.org/abs/2410.16599).

### GNS Construction Theorem
In this section we will state the GNS Construction Theorem, which we prove in subsequent sections.

However, before stating the theorem we'll need to introduce some terminology that appears in the theorem's statement. We begin with the definition of "state" and some closely associated terms.

> **Definition** *(State)*
> Let $$\mathfrak{U}$$ be an abstract C\*-algebra[^1]. A *state* is an element $$\omega$$ of the dual space $$\mathfrak{U}^*$$ that is
> 
> * *Positive* - for any $$a \in \mathfrak{U}$$ we have $$0 \le \omega(a^*a)$$ and
> * *Normalized* - the operator norm satisfies $$\| \omega \|=1$$.
> 
> Furthermore, a state $$\omega$$ is said to be *faithful* if for any non-zero $$a$$ in $$\mathfrak{U}$$, it follows that $$0 < \omega(a^*a)$$.

We will also have need of the term "cyclic vector".

> **Definition** *(Cyclic Vector)*
> Let $$\mathcal{A}$$ be an algebra represented by the bounded operators $$\pi(\mathcal{A})$$ on the Hilbert space $$\mathcal{H}$$. A vector $$\Omega$$ in $$\mathcal{H}$$ is said to be a *cyclic vector* if the set
> 
> $$
> \{ A\Omega : A \in \pi(\mathcal{A}) \}
> $$
> 
> is dense in $$\mathcal{H}$$.

With this terminology we are then able to state the GNS Construction Theorem

> **Theorem** *(GNS Construction Theorem)*
> Let $$\omega$$ be a state over a unital C\*-algebra $$\mathfrak{U}$$. One can then construct a Hilbert space $$\mathcal{H}_\omega$$ and \*-representation $$\pi_\omega$$ of $$\mathfrak{U}$$ by bounded operators on $$\mathcal{H}_\omega$$ such that
>
> $$
> \pi_\omega(a^*) = \pi_\omega(a)^\dagger.
> $$
> 
> As $$\mathfrak{U}$$ is unital, there exists a cyclic vector $$\Omega$$ in $$\mathcal{H}_\omega$$ for the representation $$\pi_\omega$$ such that
> 
> $$
> \omega(a) = \left<\Omega, \pi_\omega(a)\Omega\right>_{\mathcal{H}_\omega}.
> $$
> 
> The triple $$(\mathcal{H}_\omega, \pi_\omega, \Omega)$$ is called the *GNS triple associated to $$(\mathfrak{U}, \omega)$$* or the *cyclic representation of $$(\mathfrak{U}, \omega)$$*. Furthermore, if $$\omega$$ is a faithful state, then the \*-representation $$\pi_\omega$$ is faithful. In addition the GNS triple associated to $$(\mathfrak{U}, \omega)$$ is unique up to unitary equivalence.

### Proof of the GNS Construction Theorem
With the GNS Construction Theorem stated, we can now commence with its proof.

This proof has four parts: (1) the construction of the GNS Hilbert space $$\mathcal{H}_\omega$$, (2) the construction of the \*-representation $$\pi_\omega$$, (3) the construction of the cyclic vector $$\Omega$$ in $$\mathcal{H}_\omega$$, and (4) the proof of uniqueness up to unitary equivalence. Each part corresponds to a subsequent subsection.

#### Construction of the GNS Hilbert Space
We'll construct the GNS Hilbert space $$\mathcal{H}_\omega$$ from the C\*-algebra $$\mathfrak{U}$$ itself, modifying $$\mathfrak{U}$$ as needed to obtain the desired $$\mathcal{H}_\omega$$.

Let's start by attemptiing to place an inner product on $$\mathfrak{U}$$. Naively one might hope the following defines an inner product

$$
\left< a, b \right> \equiv \omega(a^*b)
$$

on $$\mathfrak{U}$$. Unfortunately it doesn't. Let's examine why this fails.

Consider the set

$$
\mathcal{N} \equiv \{ n \in \mathfrak{U} : \omega(n^*n) = 0 \}.
$$

Generically $$\omega$$ isn't faithful. Thus $$\mathcal{N}$$ isn't empty and there exist non-zero $$n$$ in $$\mathcal{N}$$ such that $$\omega(n^*n) = 0$$. For such $$n$$ one has

$$
\left< n, n \right> \equiv \omega(n^*n) = 0.
$$

Hence, there are non-zero $$n$$ in $$\mathfrak{U}$$ such that $$\left< n, n \right> = 0$$. The existence of such $$n$$ proves that our naive inner product on $$\mathfrak{U}$$

$$
\left< a, b \right> \equiv \omega(a^*b)
$$

actually isn't an inner product. However, the form $$\mathcal{N}$$ takes gives us a hint as to how to repair this naive inner product.

In particular, if we quotient $$\mathfrak{U}$$ by $$\mathcal{N}$$ we would rid ourselves of the problem we encountered above and hopefully be able to construct an inner product on $$\mathfrak{U} / \mathcal{N}$$ and its completion. We'll see this plan actually works.


#### Construction of the GNS Representation
Lorem ipsum dolor sit amet, consectetur adipiscing elit. In eget mauris fringilla metus sollicitudin sagittis sollicitudin quis mi. Aliquam quis lacus sed eros tincidunt fermentum. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum in neque ac massa sagittis dapibus ut a nulla. Aenean fringilla finibus est, vel semper justo bibendum eu. Nulla quis nisl eget lacus tempor posuere dictum at ligula. Duis interdum nec metus quis eleifend. Sed eget lacinia erat, eget aliquet orci. Fusce convallis fringilla pellentesque. Aliquam nec luctus quam. Praesent nec feugiat risus. Nunc mattis volutpat efficitur. Pellentesque tempor aliquam ipsum vitae bibendum. Mauris eget sem auctor, pharetra sem at, varius urna. Praesent id quam vitae justo mattis rhoncus. Pellentesque tempor eros commodo convallis faucibus.

Vestibulum a egestas magna, sit amet molestie nisi. Sed a ex id mauris varius accumsan sed ut nulla. Donec non feugiat nulla. Cras ut erat a augue venenatis placerat. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras semper turpis in semper luctus. Ut vel nibh ut mauris lacinia fermentum nec nec odio. Donec a nunc ac odio placerat rhoncus. Nunc eget nunc ac massa tristique mollis vel quis lectus. Sed rutrum ante vitae dui faucibus auctor. Nullam ut rhoncus augue.

Duis a arcu sit amet arcu bibendum ultricies quis id lectus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Mauris sit amet felis in sem efficitur porta sit amet at eros. Nunc lectus nisl, hendrerit a massa ullamcorper, eleifend suscipit nisl. In nec ante ut ex bibendum posuere a vitae ex. Suspendisse id tincidunt eros. Donec nec libero posuere, euismod est et, posuere massa. Phasellus cursus mi nulla. Nunc at lacus elit. Praesent vel placerat lectus. Nam faucibus porta ipsum, sit amet rhoncus nulla. Nunc mattis erat non bibendum auctor. Aenean ornare urna justo, ut rutrum nibh viverra non. Nam urna augue, vehicula sed commodo eget, auctor ut quam. Donec porttitor lorem sit amet ornare hendrerit.

Vivamus accumsan velit mauris, id efficitur augue blandit ut. Duis iaculis efficitur eros, non volutpat turpis accumsan vitae. Maecenas tincidunt mauris vitae eros condimentum imperdiet ac tincidunt erat. Nam nibh nunc, faucibus vel commodo eu, fermentum in enim. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin scelerisque augue nec velit blandit, eu accumsan est tempus. Nunc consectetur, arcu sit amet porttitor vehicula, diam justo dictum arcu, eu dictum mauris enim et est. Nunc egestas congue malesuada. Cras pharetra faucibus mi, sed mollis tortor rhoncus id. Ut ornare ligula non mattis condimentum. Vestibulum tincidunt risus ac venenatis consequat. Etiam vitae arcu ante. Maecenas vel venenatis elit.

Fusce odio arcu, euismod eget erat eget, interdum feugiat lacus. Morbi porta turpis lorem, at lacinia arcu sagittis sed. Vestibulum cursus porta auctor. Curabitur porta risus sed ligula maximus, at accumsan nibh mattis. Sed aliquam neque dolor, commodo posuere arcu feugiat et. In vel molestie lorem. Phasellus sed tincidunt felis, ut euismod nibh. Integer a lacus ultrices, cursus purus eu, pulvinar nulla. Aenean sit amet enim ac mauris aliquet eleifend. Duis dictum cursus lacinia. Nunc metus ipsum, euismod vulputate auctor eu, feugiat ac tortor. Etiam pellentesque turpis sit amet aliquet ornare. Morbi interdum massa nec enim posuere, sed dignissim diam accumsan. Nullam tempus nisl lectus, lacinia consequat nibh posuere vitae. Maecenas et enim sed tellus efficitur euismod.

#### Construction of the Cyclic Vector 
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse sollicitudin placerat porttitor. Suspendisse iaculis condimentum mi, sed lobortis ex pharetra ac. Maecenas eget suscipit neque. In id porttitor ex, eget rhoncus nibh. Phasellus non libero semper, placerat urna quis, pellentesque nibh. Phasellus nec ex at dui rutrum sagittis. Etiam venenatis cursus felis. Vivamus tellus nulla, pellentesque ac mauris vel, faucibus eleifend metus. Sed ac tincidunt dui. Phasellus non tempor justo.

### Uniqueness up to Unitary Equivalence
Lorem ipsum dolor sit amet, consectetur adipiscing elit. In eget mauris fringilla metus sollicitudin sagittis sollicitudin quis mi. Aliquam quis lacus sed eros tincidunt fermentum. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum in neque ac massa sagittis dapibus ut a nulla. Aenean fringilla finibus est, vel semper justo bibendum eu. Nulla quis nisl eget lacus tempor posuere dictum at ligula. Duis interdum nec metus quis eleifend. Sed eget lacinia erat, eget aliquet orci. Fusce convallis fringilla pellentesque. Aliquam nec luctus quam. Praesent nec feugiat risus. Nunc mattis volutpat efficitur. Pellentesque tempor aliquam ipsum vitae bibendum. Mauris eget sem auctor, pharetra sem at, varius urna. Praesent id quam vitae justo mattis rhoncus. Pellentesque tempor eros commodo convallis faucibus.

Vestibulum a egestas magna, sit amet molestie nisi. Sed a ex id mauris varius accumsan sed ut nulla. Donec non feugiat nulla. Cras ut erat a augue venenatis placerat. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras semper turpis in semper luctus. Ut vel nibh ut mauris lacinia fermentum nec nec odio. Donec a nunc ac odio placerat rhoncus. Nunc eget nunc ac massa tristique mollis vel quis lectus. Sed rutrum ante vitae dui faucibus auctor. Nullam ut rhoncus augue.

Duis a arcu sit amet arcu bibendum ultricies quis id lectus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Mauris sit amet felis in sem efficitur porta sit amet at eros. Nunc lectus nisl, hendrerit a massa ullamcorper, eleifend suscipit nisl. In nec ante ut ex bibendum posuere a vitae ex. Suspendisse id tincidunt eros. Donec nec libero posuere, euismod est et, posuere massa. Phasellus cursus mi nulla. Nunc at lacus elit. Praesent vel placerat lectus. Nam faucibus porta ipsum, sit amet rhoncus nulla. Nunc mattis erat non bibendum auctor. Aenean ornare urna justo, ut rutrum nibh viverra non. Nam urna augue, vehicula sed commodo eget, auctor ut quam. Donec porttitor lorem sit amet ornare hendrerit.

## Algebraic Quantum Field Theory in Minkowski Spacetime
Now, before introducing any axioms that codify AQFT in Minkowski Spacetime, we must define Minkowski spacetime itself, the arena upon which everything unfolds.

**Definition** *(Chronological Future and Past)*
Consider a point $$p$$ in a smooth manifold with a Minkowski metric. The *chronological future* of $$p$$ is the set $$I^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like curve. Similarly, the *chronological past* of $$p$$ is the set $$I^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like curve.

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
> a unital, injective \*-homomorphism.

Before stating the next axiom, we need to introduce some terminology that appears in the axiom.

**Definition** *(Quasilocal Algebra)*
Consider the set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$. As proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), this set-theoretic union is a normed \*-algebra. Also, as proven in the blog post ([Unpacking the Haag Kastler Axioms](https://kellyjdavis.github.io/aqft/haag-kastler-axioms/)), its completion yields a C\*-algebra, denoted as $$\mathfrak{U}$$. This C\*-algebra $$\mathfrak{U}$$ is called the *quasilocal algebra*.

**Definition** *(Causal Future and Past)*
Consider a point $$p$$ in Minkowski spacetime. The *causal future* of $$p$$ is the set $$J^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like or light-like curve. Similarly, the *causal past* of $$p$$ is the set $$J^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like or light-like curve.

**Definition** *(Spacelike Related)*
Consider two points $$p_1$$ and $$p_2$$ in Minkowski spacetime. The points are said to be *spacelike related* if $$p_2 \notin J^+(p_1) \cup J^-(p_1)$$ or equivalently $$p_1 \notin J^+(p_2) \cup J^-(p_2)$$.

**Definition** *(Completely Spacelike)*
Consider two sets $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ in Minkowski spacetime. $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ are said to be *completely spacelike* if every $$p_1$$ in $$\mathbf{O}_1$$ is spacelike related to every $$p_2$$ in $$\mathbf{O}_2$$ or equivalently if every $$p_2$$ in $$\mathbf{O}_2$$ is spacelike related to every $$p_1$$ in $$\mathbf{O}_1$$.

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

To state the next axiom we make use of the following definition

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
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital, bijective *-homomorphism generated by $$L$$.

## Algebraic Quantum Field Theory in Lorentzian Spacetime
The lightning review of AQFT in Minkowski spacetime complete, we now move on to a review of AQFT in Lorentzian spacetime.

As in the Minkowski case, before introducing any axioms that codify AQFT in Lorentzian spacetime, we need to specify exactly what Lorentzian spacetime is:

**Definition** *(Chronological Future and Past)*
Consider a point $$p$$ in a smooth manifold with a Lorentzian metric. The *chronological future* of $$p$$ is the set $$I^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like curve. Similarly, the *chronological past* of $$p$$ is the set $$I^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like curve.

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
> a unital, injective \*-homomorphism.

The next axiom makes use of the following definitions:

**Definition** *(Causal Future and Past)*
Consider a point $$p$$ in Lorentzian spacetime. The *causal future* of $$p$$ is the set $$J^+(p)$$ of points reachable from $$p$$ via a future-directed, time-like or light-like curve. Similarly, the *causal past* of $$p$$ is the set $$J^-(p)$$ of all points that reach $$p$$ via a future-directed, time-like or light-like curve.

**Definition** *(Spacelike Related)*
Consider two points $$p_1$$ and $$p_2$$ in Lorentzian spacetime. The points are said to be *spacelike related* if $$p_2 \notin J^+(p_1) \cup J^-(p_1)$$ or equivalently $$p_1 \notin J^+(p_2) \cup J^-(p_2)$$.

**Definition** *(Completely Spacelike)*
Consider two sets $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ in Lorentzian spacetime. $$\mathbf{O}_1$$ and $$\mathbf{O}_2$$ are said to be *completely spacelike* if every $$p_1$$ in $$\mathbf{O}_1$$ is spacelike related to every $$p_2$$ in $$\mathbf{O}_2$$ or equivalently if every $$p_2$$ in $$\mathbf{O}_2$$ is spacelike related to every $$p_1$$ in $$\mathbf{O}_1$$.

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

The next axiom has need of the following definition

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
> where $$\varphi(\mathbf{B})$$ is the image of the basis element $$\mathbf{B}$$ under the isometry $$\varphi$$ and $$\alpha_\varphi$$ is a unital, bijective *-homomorphism generated by $$\varphi$$.

# Introduction to States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

## States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Local States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Global States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## States of Algebraic Quantum Field Theory in Lorentzian Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Local States of Algebraic Quantum Field Theory in Lorentzian Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Global States of Algebraic Quantum Field Theory
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

# Introduction to Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

## Local, Isometrically Invariant States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometrically Invariant States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometrically Invariant States of Algebraic Quantum Field Theory in Lorentzian Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometrically Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

# Summary
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas vitae quam sed ex gravida hendrerit. Curabitur ac ante fringilla, aliquet purus et, commodo justo. Nulla commodo consectetur nisl, eget cursus justo convallis non. Proin a consectetur libero. Proin placerat, turpis quis tristique porta, nibh orci laoreet dolor, non dignissim sem quam vel nisl. Cras metus ligula, mollis ut justo in, sollicitudin tincidunt magna. Nunc molestie pulvinar nibh, ac venenatis odio viverra vulputate. Nunc suscipit dignissim maximus. Ut consectetur condimentum sodales. Ut ultricies leo sed odio semper, a vehicula libero pellentesque.

Ut posuere convallis convallis. Cras fermentum lacinia blandit. Ut posuere ex sed neque porttitor condimentum. Sed ac felis luctus, bibendum velit vitae, sollicitudin dolor. Nunc tristique ante vitae ullamcorper lacinia. Mauris sodales dui at justo ornare porta. Nulla facilisi. Pellentesque vel eleifend risus, ac auctor sapien. Sed pellentesque finibus turpis, et ornare lectus auctor ut. Nulla ut dui tellus. Fusce risus augue, vehicula id convallis at, hendrerit sit amet orci.

Nunc ut imperdiet neque. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Maecenas aliquam nisi eget augue cursus, efficitur egestas ligula bibendum. Suspendisse fringilla mi dictum libero fermentum gravida. Mauris vehicula tortor ac orci aliquam dictum. Mauris ac enim enim. Suspendisse molestie eros et massa volutpat, non convallis arcu posuere. Sed id nunc in lectus tincidunt pellentesque. Nunc vestibulum facilisis ante, vitae vehicula ex. Donec maximus sem a tincidunt vulputate. Sed lacinia molestie mauris, et efficitur nisi dapibus eget. Aliquam vel elit quis dolor laoreet varius.

Nulla vel mollis neque. Proin vulputate nisi nec tellus consequat placerat. Etiam congue diam ante, in posuere sem eleifend vel. Suspendisse potenti. Duis tempus rhoncus mauris, ac dapibus mauris maximus in. Pellentesque finibus sagittis eros eu commodo. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque auctor nibh ut eros aliquam, vel rhoncus sem varius. Nam ac iaculis dolor, eu varius ligula. Sed vel tellus libero. Aenean vel diam at sem vulputate vehicula.

[^1]: Note $$\mathfrak{U}$$ is an abstract C\*-algebra and need not be a quasilocal algebra or in any way associated with an AQFT.
