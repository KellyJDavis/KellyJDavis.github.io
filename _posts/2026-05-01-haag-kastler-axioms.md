---
title:  "Haag Kastler Axioms"
date:   2025-06-21 14:37:53 +0200
categories: aqft
---

# Algebraic Quantum Field Theory 
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

# Original Haag Kastler Axioms
The original [Haag Kastler Axioms](https://doi.org/10.1063/1.1704187) state:

**Axiom 1** *(Local Algebras)* The "regions" $$\mathbf{B}$$ for which the correspondence

   $$\mathbf{B} \rightarrow \mathfrak{U}(\mathbf{B})$$

   is defined shall be the open sets with compact closure in Minkowski space, the algebras $$\mathfrak{U}(\mathbf{B})$$ shall be (abstract) C\*-algebras.

**Axiom 2** *(Isotony)* If $$\mathbf{B_1} \subset \mathbf{B_2}$$ then $$\mathfrak{U}(\mathbf{B_1}) \subset \mathfrak{U}(\mathbf{B_2})$$. We assume in addition that one of the two following situations prevails. Either $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ have a common unit element, or neither of them has a unit. The first situation can be obtained from the second by formal adjunction of a unit.

**Axiom 3** *(Local Commutativity)* If $$\mathbf{B_1}$$ and $$\mathbf{B_2}$$ are completely spacelike with respect to each other, then $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ commute.

**Axiom 4** *(Quasilocal Algebra)* The set-theoretic union of all $$\mathfrak{U}(\mathbf{B})$$ is a normed \*-algebra. Taking its completion we get a C\*-algebra which we denote by $$\mathfrak{U}$$ and call the *algebra of quasilocal observables*. We maintain that $$\mathfrak{U}$$ contains all observables of interest.

**Axiom 5** *(Lorentz Covariance)* The inhomogeneous Lorentz group is represented by automorphisms $$A \in \mathfrak{U} \rightarrow A^L \in \mathfrak{U}$$ such that

$$\mathfrak{U}(\mathbf{B})^L = \mathfrak{U}(\mathbf{LB})$$

where $$L\mathbf{B}$$ is the image of the region $$\mathbf{B}$$ under the Lorentz transformation $$L$$.

**Axiom 6** *(Primitivity)* $$\mathfrak{U}$$ is primitive.

# Axiom 0 (Minkowski Space)
"Minkowski space" is referred to, directly or indirectly, in most of these axioms. However, a crisp, mathematical definition of "Minkowski space" is never given in Haag and Kastler's [original work](https://doi.org/10.1063/1.1704187). So, to clarify the axioms, we should provide one.

Normally this level of pedanticism isn't warranted. But, for example, **Axiom 1** *(Local Algebras)* refers to the $$\mathbf{B}$$ as *"open sets with compact closure in Minkowski space"*. So, the topology of "Minkowski space" *is* relavent, and not all topologies may yield "physical" results.

All that being said, to ensure that the axioms are built on a solid foundation, we need a formal definition of "Minkowski space" to build them on.

## Standard Topology on Minkowski Space
Physicists usually think of Minkowski space as $$\mathbb{R}^4$$ equipped with the [Euclidean topology](https://ncatlab.org/nlab/show/Euclidean+topology), a [Minkowski metric](https://ncatlab.org/nlab/show/Minkowski+metric), and the "standard" time-orientation. The "standard" time-orientation in this context is simply the non-vanishing vector $$(1,0,0,0)$$ in the standard coordinate system on $$\mathbb{R}^4$$.

This may be what Haag and Kastler mean by "Minkowski space", but then again it may not. As they don't explicitly define the term "Minkowski space", it's uncertain what they mean. Let's consider some alternatives.

## Indiscrete Topology on Minkowski Space
Other topologies are possible on $$\mathbb{R}^4$$, and as Haag and Kastler don't explicitly specify a topology, we can explore other possibilities.

For example, one can equip $$\mathbb{R}^4$$ with the [indiscrete topology](https://ncatlab.org/nlab/show/discrete+and+indiscrete+topology). The indiscrete topology is the topology in which the only open sets are the empty set and $$\mathbb{R}^4$$ itself.

In this case, as we require our $$\mathbf{B}$$ to be an open, proper subset of $$\mathbb{R}^4$$, the only possible value that $$\mathbf{B}$$ can take on is the empty set. (Note, we require $$\mathbf{B}$$ to be a proper subset instead of just a subset to avoid the inclusion of global observables. See Section I Paragraph 5 of [Haag Kastler](https://doi.org/10.1063/1.1704187).) As $$\mathbf{B}$$ is intended to be a region in which one performs a "measurement", requiring $$\mathbf{B}$$ be the empty set doesn't capture that intention at all. The empty set is too "small".  So, we can assume that the indiscrete topology isn't implicitly being used.

But this leaves open the question: Exactly which topology *is* being used? The Euclidean topology?

## Euclidean Topology on Minkowski Space
If the Euclidean topology is being used, then this raises another question: Why use the $$\mathbf{B}$$, open sets with compact closure, based off a topology derived from a *Euclidian* metric on $$\mathbb{R}^4$$?  *Euclidian* metrics have *nothing* to do with physics which is determined by a Minkowski metric. A more "natural" thing to do would be to base $$\mathbf{B}$$ off a "topology derived from a Minkowski metric", whatever that might mean.

## Alexandrov Topology on Minkowski Space 
To consider what that might mean let $$p$$ and $$q$$ be any two points in what physicists think of as Minkowski space. With these two points, one can define two natural sets: $$I^+(p)$$, the chronological future of $$p$$ (i.e. the set of points reachable from $$p$$ via a future-directed, time-like curve), and $$I^-(q)$$, the chronological past of $$q$$ (i.e. the set of all points that reach $$q$$ via a future-directed, time-like curve).

It turns out that $$I^+(p)$$ is an open set in the Euclidean topology for any $$p$$ in what physicists think of as Minkowski space (Proposition 2.8 of [Penrose](https://doi.org/10.1137/1.9781611970609)). Similarly, the time-reversed version of Proposition 2.8 of [Penrose](https://doi.org/10.1137/1.9781611970609) implies that $$I^-(q)$$ is an open set in that same topology. Hence, $$I^+(p) \cap I^-(q)$$ is also open in that topology.

This suggests that sets of the form $$I^+(p) \cap I^-(q)$$ might be able to be used as the [basis](https://ncatlab.org/nlab/show/topological+base) of a new topology on $$\mathbb{R}^4$$. As it so happens, sets of this form *can* be used as the basis for a topology on $$\mathbb{R}^4$$.

Sets $$I^+(p) \cap I^-(q)$$ with $$p,q \in \mathbb{R}^4$$ form the basis for what's known as the Alexandrov topology of $$\mathbb{R}^4$$ (Definition 4.22 of [Penrose](https://doi.org/10.1137/1.9781611970609)). Furthermore, it turns out that the Alexandrov topology of $$\mathbb{R}^4$$ agrees with the Euclidean topology of $$\mathbb{R}^4$$ (Paragraph 4.23 of [Penrose](https://doi.org/10.1137/1.9781611970609)), a welcome happenstance that "explains" why physicists had not confronted this earlier.

All that being said, we will equip $$\mathbb{R}^4$$ with the Alexandrov topology as it is the "natural" topology of relativity.  So for us *Minkowski space* is $$\mathbb{R}^4$$ with the Alexandrov topology, the Minkowski metric, and standard time-orientation.

In this case the Euclidean topology and the Alexandrov topology agree, but on other manifolds this need not be the case.

# Axiom 1 (Local Algebras)
Next let us consider Axiom 1 (Local Algebras) which states

**Axiom 1** *(Local Algebras)* The "regions" $$\mathbf{B}$$ for which the correspondence

   $$\mathbf{B} \rightarrow \mathfrak{U}(\mathbf{B})$$

   is defined shall be the open sets with compact closure in Minkowski space, the algebras $$\mathfrak{U}(\mathbf{B})$$ shall be (abstract) C\*-algebras.

## Regions of Measurement
In **Axiom 1** *(Local Algebras)*, the regions $$\mathbf{B}$$ are open sets with compact closure in Minkowski space, assumingly equipped with a Euclidean topology though Haag and Kastler were silent on this point.

In Haag and Kastler's original [work](https://doi.org/10.1063/1.1704187), these $$\mathbf{B}$$ are regions in which one "measures" an "observable". Let us focus on such open sets with compact closure and see if they do indeed represent regions in which one "measures" an "observable", or if they require modification.

### Measurement
The topic of "measurement" is a fraught topic within quantum mechanics and, by extension, quantum field theory. What is "measurement"? What role do "observers" play in "measurement"? Does "measurement" collapse the wavefunction? The questions are myriad and won't be settled here.

However, despite having no idea what "measurement" is, with just a two "plausible" assumptions we can make progress in defining properties of the regions  $$\mathbf{B}$$ in which a "measurement" can occur.

The first "plausible" assumption is that the "process of measurement" starts at some point $$p$$ in Minkowski space.

The second "plausible" assumption is that the "process of measurement" stops at some point $$q$$ in Minkowski space.

### Regions of Measurement
With these "plausible" assumptions, we reach the "plausible" conclusion that a "measurement", whatever that may be, when done by a massive entity like us, occurs within regions of the form $$I^+(p) \cap I^-(q)$$, where $$I^+(p)$$ is the chronological future of $$p$$ and $$I^-(q)$$ is the chronological past of $$q$$.

The choice $$I^+(p) \cap I^-(q)$$ makes sense as, due to the constraints of special relativity, a massive "observer", such as ourselves, can only perform a "measurement", whatever that is, in the region $$I^+(p) \cap I^-(q)$$.

This then implies that all our regions $$\mathbf{B}$$ should all be of the form $$I^+(p) \cap I^-(q)$$ for appropriate $$p$$ and $$q$$ denoting the start and stop of the associated "measurement".


### Criticisms
While requiring $$\mathbf{B}$$ to be of the form $$I^+(p) \cap I^-(q)$$ is more "natural" than just requiring $$\mathbf{B}$$ be an open set with compact closure, it's still not without its problems.

#### Infinite Recursion
Consider the point $$p$$ at which the “process of measurement” starts. This point has a set of spacetime coordinates $$x_p$$. These coordinates must also be "measured", e.g. by looking at a watch and checking GPS.

However, this seemingly leads to a infinite recursion. To "measure" the coordinates of $$p$$ one must "measure" the coordinates of two other points $$p_p$$ and $$q_p$$ to determine the region $$I^+(p_p) \cap I^-(q_p)$$ in which $$p$$ is "measured", then one has to do the same for $$p_p$$ and $$q_p$$...

The resolution to this problem is the simple observation that in Algebraic Quantum Field Theory (AQFT) Minkowski space is treated classically. Hence, coordinates of the point $$p$$ and those of the point $$q$$ can be measured in the sense of classical mechanics without having to worry about regions of the form $$I^+(p_p) \cap I^-(q_p)$$, for example.

#### Casual Regions of Measurement 
We chose regions $$\mathbf{B}$$ of the form $$I^+(p) \cap I^-(q)$$ under the assumption that "observers" were massive like ourselves. Without any real justification this excludes massless "observers". We could have also considered massive and massless "observers" and utilized casual instead of chronological regions.

In other words we could have required our regions $$\mathbf{B}$$ to be of the form $$J^+(p) \cap J^-(q)$$, where $$J^+(p)$$ is the casual future of $$p$$ (i.e. the set of points reachable from $$p$$ via a future-directed, time-like or light-like curve) and $$J^-(q)$$ is the casual past of $$q$$ (i.e. the set of all points that reach $$q$$ via a future-directed, time-like or light-like curve). This, then, would allow for massless "observers".

Requiring our regions $$\mathbf{B}$$ to be of the form $$J^+(p) \cap J^-(q)$$, however, leads to problems. In particular, as the zero vector is light-like, the point $$\{p\}$$ is a light-like curve. Hence, the point $$\{p\}=J^+(p) \cap J^-(p)$$ would be an allowable form for a region $$\mathbf{B}$$ in this scenario.

With a $$\mathbf{B}$$ of the form $$\{p\}$$ we can then use Axiom 1 to assign an (abstract) C*-algebra $$\mathfrak{U}(\{p\})$$ to the point $$\{p\}$$. This, while seemingly harmless, runs into problems, running afoul of the initial motivation for AQFT.

In standard quantum field theory a field is an operator valued distribution. (See Section 3.10 of [Talagrand](https://doi.org/10.1017/9781108225144).) So, as it is a distribution, it is defined almost everywhere. This means that there may exist points $$p$$ in Minkowski space at which it is not defined.

Traditionlly (See Section II.4.1 of [Haag](https://doi.org/10.1007/978-3-642-61458-3)) AQFT motivates the passage from a standard field, i.e. an operator valued distribution $$\Phi$$, to the algebra $$\mathfrak{U}(\mathbf{B})$$ on an open, bounded set $$\mathbf{B}$$ by constructing the algebra $$\mathfrak{U}(\mathbf{B})$$ from *smearings* of $$\Phi$$ over $$\mathbf{B}$$, i.e. an element $$a$$ of $$\mathfrak{U}(\mathbf{B})$$ would be defined as follows

$$
a \equiv \int_{\mathbf{B}} f(x) \Phi(x) \, d^4x,
$$

where $$f(x)$$ is a *test function*, a smooth function with support in $$\mathbf{B}$$.

Trying to generalize this to $$\mathfrak{U}(\{p\})$$ immediately runs into problems. Naively an element $$b$$ in $$\mathfrak{U}(\{p\})$$ would be of the form 

$$
b \equiv \int_{\{p\}} f(x) \Phi(x) \, d^4x.
$$

However, this doesn't make any sense. $$\Phi$$ is a operator valued distribution and may not even be defined at $$p$$. Hence, $$b$$ isn't defined, which in turn implies $$\mathfrak{U}(\{p\})$$ isn't defined.

So, all of this implies that our original choice requiring regions $$\mathbf{B}$$ to be of the form $$I^+(p) \cap I^-(q)$$, and not of the form $$J^+(p) \cap J^-(q)$$, was the right one.


# Axiom 2 (Isotony)
Now let us consider Axiom 2 (Isotony) which states

**Axiom 2** *(Isotony)* If $$\mathbf{B_1} \subset \mathbf{B_2}$$ then $$\mathfrak{U}(\mathbf{B_1}) \subset \mathfrak{U}(\mathbf{B_2})$$. We assume in addition that one of the two following situations prevails. Either $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ have a common unit element, or neither of them has a unit. The first situation can be obtained from the second by formal adjunction of a unit.

## Isotony
Isotony, along with the requirement that $$\mathfrak{U}(\mathbf{B})$$ be a C*-algebra, turns out to be "natural" physically.

Simplifying things slightly[^1], "observables" in a region $$\mathbf{B}_1$$ correspond to self-adjoint elements of $$\mathfrak{U}(\mathbf{B}_1)$$. And, like in quantum mechanics, the possible values one can obtain when "measuring" the "observable" corresponding to a self-adjoint $$a \in \mathfrak{U}(\mathbf{B}_1)$$ are the values in the specturm $$\sigma_{\mathfrak{U}(\mathbf{B}_1)}(a)$$ of the operator $$a$$ when it is viewed as a element of $$\mathfrak{U}_1$$.

Isotony, implies that if $$\mathbf{B_1} \subset \mathbf{B_2}$$ then $$\mathfrak{U}(\mathbf{B_1}) \subset \mathfrak{U}(\mathbf{B_2})$$. So a self-adjoint $$a \in \mathfrak{U}(\mathbf{B_1})$$ may also be viewed as an element of $$\mathfrak{U}(\mathbf{B_2})$$.

The obvious question this raises is this: For $$\mathbf{B_1} \subset \mathbf{B_2}$$ and thus $$\mathfrak{U}(\mathbf{B_1}) \subset \mathfrak{U}(\mathbf{B_2})$$, given a self-adjoint $$a \in \mathfrak{U}(\mathbf{B_1})$$ we may also view $$a$$ as in $$\mathfrak{U}(\mathbf{B_2})$$. So the values one can obtain "measuring" the "observable" corresponding to $$a$$ are $$\sigma_{\mathfrak{U}(\mathbf{B}_1)}(a)$$, if one views $$a$$ as an element of $$\mathfrak{U}(\mathbf{B_1})$$, and $$\sigma_{\mathfrak{U}(\mathbf{B}_2)}(a)$$, if one views it as an element of $$\mathfrak{U}(\mathbf{B_2})$$. How does $$\sigma_{\mathfrak{U}(\mathbf{B}_1)}(a)$$ relate to $$\sigma_{\mathfrak{U}(\mathbf{B}_2)}(a)$$?

They actually relate in a "natural" manner when the $$\mathfrak{U}(\mathbf{B}_1)$$ and $$\mathfrak{U}(\mathbf{B}_2)$$  are C\*-algebras.

For C*-algebras we have the following theorem (Proposition 2.2.7 of [Bratteli and Robinson](https://doi.org/10.1007/978-3-662-02520-8))

**Theorem** *(C\*-Spectrum is Invariant Under Inclusion)*
*Let $$\mathfrak{U}_1$$ be a C\*-subalgebra of the C\*-algebra $$\mathfrak{U}_2$$. If $$a$$ is an element of $$\mathfrak{U}_1$$, then the spectrum $$\sigma_{\mathfrak{U}_1}(a)$$ of $$a$$ when viewed as a element of $$\mathfrak{U}_1$$ is the same as the spectrum $$\sigma_{\mathfrak{U}_2}(a)$$ of $$a$$ when viewed as a element of $$\mathfrak{U}_2$$*

$$
\sigma_{\mathfrak{U}_1}(a) = \sigma_{\mathfrak{U}_2}(a).
$$

*This allows us drop the subscript from $$\sigma_{\mathfrak{U}_1}(a)$$ and $$\sigma_{\mathfrak{U}_2}(a)$$ and to write $$\sigma(a)$$ unambiguously.*

As a result of this C\*-algebra specific theorem, **Axiom 2** *(Isotony)* is "natural" in that it doesn't lead to the "un-physical" situation in which the set of possible experimenal results can differ dependent on whether you consider your experiment as occuring in the city Cambridge, Massachusetts or in the state Massachusetts.

## Common Unit
The isotony axiom also contains this rather odd addendum:

> We assume in addition that one of the two following situations prevails. Either $$\mathfrak{U}(\mathbf{B_1})$$ and $$\mathfrak{U}(\mathbf{B_2})$$ have a common unit element, or neither of them has a unit. The first situation can be obtained from the second by formal adjunction of a unit.

If, as suggested, it is always possible, through formal adjunction, to add a unit, then why even consider the case in which there is no unit?

For example, to define the specturm of an element $$a$$ in an algebra $$\mathfrak{U}(\mathbf{B})$$ that doesn't have a unit, one has to, through formal adjunction, add a unit to $$\mathfrak{U}(\mathbf{B})$$, then compute the specturm of $$a$$ in this larger algebra. So the possible experimental values $$\sigma(a)$$ will appear as if $$\mathfrak{U}(\mathbf{B})$$ has a unit.

As the possible experimental values when a unit is not present are identical to the case in which a unit is present, we will simply assume that all such $$\mathfrak{U}(\mathbf{B})$$ contain a unit.

One convenient way to include a unit, and the one we adopt, is to assume that the empty set $$\emptyset$$ is assigned the C\*-algebra $$\mathbb{C} \mathbf{1}$$ generated by the unit operator $$\mathbf{1}$$

$$
\emptyset \rightarrow \mathbb{C} \mathbf{1}.
$$

As the empty set $$\emptyset$$ is a member of any $$\mathbf{B}$$, isotony, i.e. $$\emptyset \subset \mathbf{B}$$ implying $$\mathfrak{U}(\emptyset) \subset \mathfrak{U}(\mathbf{B})$$, then implies that all $$\mathfrak{U}(\mathbf{B})$$ contain a unit.

# Axiom 3 (Local Commutativity)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

# Axiom 4 (Quasilocal Algebra)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

# Axiom 5 (Lorentz Covariance)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

# Axioms 6 (Primitivity)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

# Haag Kastler Axioms Clarified

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed suscipit libero suscipit neque molestie fermentum. Duis in velit sed nulla ullamcorper egestas. Mauris eu dui a ligula dictum placerat. Aliquam erat volutpat. Aenean at sem laoreet, dictum lacus eget, faucibus nisl. Donec tellus dolor, mattis eget lectus vitae, pretium ultrices dolor. Nullam id faucibus libero. Donec a mollis urna, ac viverra turpis. Vivamus vel purus a elit viverra posuere. Mauris viverra ex ac sem congue, eget sagittis ligula elementum. Aenean sollicitudin consectetur nunc quis tincidunt.

Morbi sit amet sodales quam. Fusce tincidunt nisl eu justo ultrices volutpat. Pellentesque congue mi eget nisl feugiat, ac pulvinar urna sagittis. Integer efficitur pretium metus, vitae pharetra lacus. Phasellus sed leo diam. Fusce ut interdum magna. Curabitur semper faucibus semper. Suspendisse sed fermentum tortor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse nec ex sit amet quam varius feugiat.

Integer fermentum id diam id eleifend. Nulla et interdum elit, quis ornare est. Sed eget pretium nisi. Donec nec pharetra odio. Morbi pretium eget sem eget ultrices. Nam arcu mauris, lacinia quis magna sit amet, lacinia efficitur augue. Sed ac odio id ligula gravida vulputate.

[^1]: In reality one has to introduce a state $$\omega$$ and use that state in the GNS construction to create a representation $$\pi_\omega(\mathfrak{U}(\mathbf{B}))$$ of $$\mathfrak{U}(\mathbf{B})$$ on the GNS Hilbert space $$\mathcal{H}_\omega$$. Self-adjoint elements of this representation correspond to "observables". However, as $$\pi_\omega$$ is a representation, self-adjoint elements of $$\mathfrak{U}(\mathbf{B})$$ are mapped to self-adjoint elements of  $$\pi_\omega(\mathfrak{U}(\mathbf{B}))$$ under $$\pi_\omega$$.
