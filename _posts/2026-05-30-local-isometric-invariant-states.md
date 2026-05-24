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
> a unital, injective \*-homomorphism.

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
> where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the transformation $$L$$ and $$\alpha_L$$ is a unital, bijective *-homomorphism generated by $$L$$.

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
> a unital, injective \*-homomorphism.

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

# Introduction to Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

## Local, Isometric Invariant States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometric Invariant States of Algebraic Quantum Field Theory in Minkowski Spacetime
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et dui nisl. Aliquam a erat eget metus commodo viverra et ut orci. Duis vitae leo ultricies purus feugiat rhoncus. In imperdiet, tortor quis tincidunt ultrices, orci diam aliquam sapien, eu laoreet erat dui id massa. Donec venenatis vitae velit malesuada euismod. Nunc euismod, turpis non gravida commodo, massa quam rutrum massa, sit amet venenatis tellus dui ac odio. Vestibulum ut porttitor ipsum. Nunc eget ultricies eros. Integer leo odio, vulputate ut sagittis at, vestibulum ac massa. In vulputate bibendum nisl, ut vestibulum lorem cursus et.

### Definition of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

### Existence of Local, Isometric Invariant States
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu placerat dolor. Integer dictum libero id lectus imperdiet, id semper orci interdum. Vestibulum sed nibh vel lorem ultricies egestas vitae sit amet mauris. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque pretium magna id facilisis laoreet. Quisque neque purus, ultrices nec placerat sed, porta ut quam. Quisque molestie ornare purus ac eleifend. Vestibulum lectus massa, malesuada rhoncus mi non, auctor tincidunt mauris. Phasellus accumsan lectus quis orci suscipit, laoreet consequat nunc rhoncus. In efficitur mauris in convallis bibendum. Duis nisi erat, porta id accumsan non, dignissim quis elit.

Nunc rhoncus, velit at rutrum bibendum, dolor est viverra sem, a vestibulum ex enim ut nulla. Maecenas iaculis hendrerit vulputate. Curabitur a condimentum dolor. In pharetra, arcu sit amet feugiat aliquet, nibh turpis maximus sem, sed vestibulum urna dui id mi. Sed at pretium ligula, nec efficitur odio. Aenean gravida purus et iaculis scelerisque. Morbi accumsan quis sapien eget luctus. Cras volutpat nunc et nulla interdum, eget consectetur orci porta. Nullam posuere diam nisi, eget ultricies dui molestie vel. Nam vitae dapibus mi. Morbi quis nibh leo. Nunc sagittis, mi sed fringilla pulvinar, felis justo sollicitudin ipsum, id fringilla felis massa venenatis dolor. Duis at ante a elit imperdiet tincidunt ut non mauris. Cras in aliquet nisl, id vehicula mi.

## Local, Isometric Invariant States of Algebraic Quantum Field Theory in Lorentzian Spacetime
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
