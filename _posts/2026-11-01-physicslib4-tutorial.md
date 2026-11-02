---
title:  "Tutorial for the Lean 4 Library physicslib4"
date:   2026-11-01 10:00:00 +0100
categories: aqft
---

<style>
.tutorial { --tut-accent: #0f766e; --tut-accent-bg: rgba(15, 118, 110, 0.06); --tut-output: #ca8a04; }
html[data-theme="dark"] .tutorial { --tut-accent: #5eead4; --tut-accent-bg: rgba(94, 234, 212, 0.07); --tut-output: #facc15; }
.tutorial .exercise { margin: 1.5em 0; padding: 1em 1.5em; border-left: 4px solid var(--tut-accent);
  background: var(--tut-accent-bg); border-radius: 0 6px 6px 0; }
.tutorial .exercise > :last-child { margin-bottom: 0; }
.tutorial .exercise-label { margin: 0 0 0.5em; font-weight: 700; color: var(--tut-accent); letter-spacing: 0.02em; }
.tutorial details.solution { margin-top: 0.75em; }
.tutorial details.solution > summary { cursor: pointer; font-weight: 600; color: var(--tut-accent); }
.tutorial details.solution[open] > summary { margin-bottom: 0.5em; }
.tutorial pre.lean-output { margin: 0 0 1em; padding: 0.5em 1em; border: none; border-left: 4px solid var(--tut-output);
  background: transparent; white-space: pre-wrap; overflow-wrap: anywhere; font-size: 0.8em; }
.tutorial .goals { position: relative; margin-bottom: 1em; padding: 1.25em 1.5em; background: var(--global-code-background-color);
  border: 1px solid var(--global-border-color); border-radius: 4px; box-shadow: 0 1px 1px rgba(0, 0, 0, 0.125); }
.tutorial .goals div.highlighter-rouge { margin: 0; padding: 0; background: transparent; border: none; box-shadow: none; }
.tutorial .goals div.highlighter-rouge::before { content: none; }
.tutorial .goals pre.highlight { margin: 0; }
.tutorial pre.tactic-state { margin: 0.35em 0 0.6em 2em; padding: 0.5em 0.75em; font-size: 0.72em; line-height: 1.45;
  border: 1px solid var(--global-border-color); border-left: 3px solid var(--tut-accent); border-radius: 4px;
  background: var(--global-bg-color); white-space: pre-wrap; overflow-wrap: anywhere; }
.tutorial .goals > pre.tactic-state:last-child { margin-bottom: 0; }
.tutorial .namedocs { margin: 1.5em 0; padding: 1em 1.25em; border: 1px solid var(--global-border-color);
  border-radius: 6px; font-size: 0.9em; }
.tutorial .namedocs pre { white-space: pre-wrap; overflow-wrap: anywhere; padding-left: 2em; text-indent: -2em;
  background: transparent; border: none; margin: 0.5em 0; font-size: 0.85em; }
.tutorial .namedocs-kind { font-style: italic; margin: 0; color: var(--global-fig-caption-color); }
.tutorial .namedocs-section { font-weight: 700; margin: 1em 0 0.25em; }
.tutorial .namedocs-fielddoc { margin: 0 0 0.75em 2em; }
.tutorial figure.tutorial-figure { margin: 2em auto; max-width: 420px; display: block; }
.tutorial figure.tutorial-figure figcaption { font-size: 0.85em; color: var(--global-fig-caption-color); text-align: center; margin-top: 0.5em; }
.tutorial .st-diagram { width: 100%; height: auto; display: block; }
.tutorial .st-big { fill: var(--tut-accent); fill-opacity: 0.07; stroke: var(--tut-accent); stroke-width: 2; }
.tutorial .st-small { fill: var(--tut-accent); fill-opacity: 0.3; stroke: var(--tut-accent); stroke-width: 2; }
.tutorial .st-cone { stroke: #64748b; stroke-width: 1.5; stroke-dasharray: 5 5; }
.tutorial .st-axis { stroke: #64748b; stroke-width: 1.5; }
.tutorial .st-arrowhead { fill: #64748b; }
.tutorial .st-label { fill: var(--global-text-color); font-size: 20px; font-weight: 600; }
.tutorial .st-label-small { font-size: 16px; }
.tutorial .st-axis-label { fill: #64748b; font-family: serif; font-style: italic; font-size: 16px; }
</style>

<div class="tutorial" markdown="1">

This tutorial introduces algebraic quantum field theory and its formalisation in Lean 4, through the
definitions and theorems of [physicslib4](https://github.com/physicslib/physicslib4). It is the single-page
version of the [physicslib4 tutorial](https://physicslib.github.io/physicslib4/tutorial/), and has four parts:

1. [AQFT in brief](#aqft-in-brief): nets of local algebras, the Haag–Kastler axioms, states and the GNS
   construction, for a reader who knows quantum mechanics and special relativity.
2. [Lean in brief](#lean-in-brief): enough Lean to read the library's definitions, statements and proofs.
3. [Worked examples](#worked-examples): four pieces of AQFT worked through in the library.
4. [Doing it yourself](#doing-it-yourself): setting up Lean, and going from a blueprint statement to a
   checked theorem of your own.

Every piece of Lean code below is checked against the library when the original tutorial is built. Where a
proof is shown with its proof states, the state after each tactic appears in a box beneath it. Exercises
appear throughout; click "Solution" to open a solution.

# 1. AQFT in brief {#aqft-in-brief}

Algebraic quantum field theory (AQFT) describes a relativistic quantum system by the observables
that can be measured in each region of spacetime, and by the relations between them that relativity
and quantum mechanics impose. This chapter introduces it to a reader who knows quantum mechanics and
special relativity. It covers nets of local algebras on causal diamonds, the Haag–Kastler axioms,
states and the GNS construction, and the points at which this project makes the 1964 axioms precise.
Lean appears from the next chapter on.

## 1.1 Why algebras

As you will recall from a first course in quantum field theory, a field such as the free scalar
field $$\phi$$ is not a function from spacetime to operators. The expression $$\phi(x)$$ makes sense
only inside an integral: the field is an operator-valued distribution, and the objects that act on
the Hilbert space are its smearings

$$
\phi(f) = \int f(x)\, \phi(x)\, d^4x,
$$

where $$f$$ is a smooth test function with compact support. If the support of $$f$$ lies in a region
$$\mathbf{B}$$ of spacetime, then $$\phi(f)$$ is something an experimenter confined to $$\mathbf{B}$$
can, at least in principle, control.

Fields are a convenient way to generate observables, but they are not observables themselves, and
they are far from unique. A Dirac field is not self-adjoint and anticommutes, rather than commutes,
at spacelike separation; it cannot be measured. A gauge potential changes under gauge
transformations that leave every measurable quantity untouched. Even for a scalar field, different
fields, such as the free field $$\phi$$ and $$\phi + {:}\phi^3{:}$$ with $${:}\phi^3{:}$$ the
Wick-ordered cube, commute with each other at spacelike separation. Such relatively local fields
belong to one _Borchers class_, and in an interacting theory any two fields of the class that create
the same particles give the same scattering matrix. The choice of field is a choice of coordinates
on the theory.

What does not depend on that choice is the answer to the question: _which observables can be
measured in which region of spacetime?_ Haag's idea is to take this assignment as the primary
object. To each region $$\mathbf{B}$$ one attaches an algebra $$\mathfrak{U}(\mathbf{B})$$ of
observables measurable in $$\mathbf{B}$$, generated, in a theory with a field, by bounded functions
of the smeared fields $$\phi(f)$$ with $$f$$ real and supported in $$\mathbf{B}$$. The physics is then
encoded in how these algebras sit inside one another and how they relate across spacetime. The
assignment $$\mathbf{B} \mapsto \mathfrak{U}(\mathbf{B})$$ is called a _net of local algebras_.

Two features of the approach matter from the start.

* The algebras consist of _bounded_ operators, or abstract versions of them. Unbounded operators
  such as $$\phi(f)$$ have domains, and their sums and products need not be defined. Bounded
  functions of them, such as $$e^{i\phi(f)}$$ or the spectral projections of $$\phi(f)$$, carry the
  same physical information without these difficulties.
* The algebras are _abstract_: no Hilbert space is fixed in advance. In quantum mechanics with
  finitely many degrees of freedom, the Stone–von Neumann theorem guarantees that the canonical
  commutation relations have, up to unitary equivalence, one irreducible representation (with the
  usual regularity assumptions). A field has infinitely many degrees of freedom, and the theorem
  fails: the same algebra has many inequivalent representations, describing, for instance, different
  thermal equilibria or different charge sectors. The algebraic approach keeps them all, and
  recovers a Hilbert space from a state, by the GNS construction, when it is needed.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$f$$ and $$g$$ be real test functions, and suppose that the smeared field satisfies the
commutation relation $$[\phi(f), \phi(g)] = i\Delta(f,g)\,\mathbf{1}$$ for a real number
$$\Delta(f,g)$$. Assuming that the formal manipulations are justified, show that the unitaries
$$W(f) = e^{i\phi(f)}$$ satisfy the Weyl relations

$$
W(f)\,W(g) = e^{-i\Delta(f,g)/2}\, W(f+g).
$$

What does this say about $$W(f)$$ and $$W(g)$$ when $$\Delta(f,g) = 0$$?

<details class="solution" markdown="1">
<summary>Solution</summary>

For operators $$A$$ and $$B$$ whose commutator is a multiple of the identity, the
Baker–Campbell–Hausdorff formula reduces to $$e^{A}e^{B} = e^{A+B}e^{[A,B]/2}$$. With $$A = i\phi(f)$$
and $$B = i\phi(g)$$, $$[A,B] = -[\phi(f),\phi(g)] = -i\Delta(f,g)\mathbf{1}$$, and linearity of the
smearing gives $$A + B = i\phi(f+g)$$. Hence $$W(f)W(g) = e^{-i\Delta(f,g)/2}\,W(f+g)$$. Exchanging
$$f$$ and $$g$$ changes the sign of $$\Delta$$, so $$W(f)W(g) = e^{-i\Delta(f,g)}W(g)W(f)$$. When
$$\Delta(f,g) = 0$$ the two unitaries commute. For the free field $$\Delta(f,g)$$ vanishes whenever
the supports of $$f$$ and $$g$$ are spacelike separated: a first sign of the locality axiom below.

</details>

</div>

**In the library:** the net, with its axioms, is the structure
`Physicslib4.AQFT.HaagKastler.HaagKastlerNet`.

## 1.2 Regions of spacetime

You will be familiar with Minkowski space: the set $$\mathbb{R}^4$$ of points
$$x = (x^0, x^1, x^2, x^3)$$, with time coordinate $$x^0$$ and the Minkowski form

$$
\eta(v, w) = -v^0 w^0 + v^1 w^1 + v^2 w^2 + v^3 w^3,
$$

of signature $$(-,+,+,+)$$, in units with $$c = 1$$. A nonzero vector $$v$$ is _timelike_ if
$$\eta(v,v) < 0$$, _null_ if $$\eta(v,v) = 0$$ and _spacelike_ if $$\eta(v,v) > 0$$; a timelike or null
vector is _causal_, and it is _future-directed_ if $$v^0 > 0$$. Two points are compared through their
difference:

* $$p \ll q$$, read "$$p$$ chronologically precedes $$q$$", if $$q - p$$ is timelike and
  future-directed;
* $$p \prec q$$, read "$$p$$ causally precedes $$q$$", if $$q - p$$ is causal and future-directed, or
  zero.

The _chronological future_ and _chronological past_ of a point are the open light cones

$$
I^+(p) = \{x : p \ll x\}, \qquad I^-(q) = \{x : x \ll q\},
$$

and the causal future and past $$J^{\pm}$$ are defined in the same way with $$\prec$$ in place of
$$\ll$$. Two points are _spacelike separated_ if neither causally precedes the other, and two sets
are _completely spacelike_ if every point of one is spacelike separated from every point of the
other.

### 1.2.1 Causal diamonds

Consider an experiment, carried out by an apparatus with mass, that starts at a spacetime point $$p$$
and ends at a point $$q$$. Every part of the apparatus moves on a timelike curve, so everything the
experiment touches lies to the future of $$p$$ and to the past of $$q$$. This is the region

$$
\mathbf{B} = I^+(p) \cap I^-(q),
$$

called the _causal diamond_ (also double cone, or Alexandrov set) of $$p$$ and $$q$$. It is open and
bounded, and it is nonempty exactly when $$p \ll q$$; when it is empty we still count it as a
diamond, the empty diamond. In the frame in which $$q - p$$ points along the time axis, $$\mathbf{B}$$
is the _domain of dependence_ of the open ball of radius $$(q^0 - p^0)/2$$ centred at the midpoint of
$$p$$ and $$q$$: every inextendible causal curve through $$\mathbf{B}$$ meets the ball, so initial data
on the ball fix a hyperbolically propagating field throughout $$\mathbf{B}$$.

<figure class="tutorial-figure">
<svg aria-labelledby="st-cones-title st-cones-desc" class="st-diagram" role="img" viewbox="0 0 400 420" xmlns="http://www.w3.org/2000/svg"><title id="st-cones-title">A causal diamond as the intersection of two light cones</title><desc id="st-cones-desc">A point p near the bottom and a point q near the top. Dashed lines at 45 degrees bound the chronological future of p, opening upwards, and the chronological past of q, opening downwards. Their intersection, shaded, is the diamond B.</desc><defs><marker id="st-cones-arrow" markerheight="7" markerwidth="7" orient="auto-start-reverse" refx="9" refy="5" viewbox="0 0 10 10"><path class="st-arrowhead" d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><line class="st-cone" x1="200" x2="20" y1="340" y2="160"></line><line class="st-cone" x1="200" x2="380" y1="340" y2="160"></line><line class="st-cone" x1="200" x2="20" y1="80" y2="260"></line><line class="st-cone" x1="200" x2="380" y1="80" y2="260"></line><polygon class="st-small" points="200,340 330,210 200,80 70,210"></polygon><circle class="st-arrowhead" cx="200" cy="340" r="4"></circle><circle class="st-arrowhead" cx="200" cy="80" r="4"></circle><text class="st-label st-label-small" text-anchor="middle" x="200" y="366">p</text><text class="st-label st-label-small" text-anchor="middle" x="200" y="66">q</text><text class="st-label" text-anchor="middle" x="200" y="217">B</text><text class="st-label st-label-small" text-anchor="middle" x="335" y="135">I⁺(p)</text><text class="st-label st-label-small" text-anchor="middle" x="335" y="300">I⁻(q)</text><line class="st-axis" marker-end="url(#st-cones-arrow)" x1="20" x2="20" y1="405" y2="345"></line><line class="st-axis" marker-end="url(#st-cones-arrow)" x1="20" x2="80" y1="405" y2="405"></line><text class="st-axis-label" x="28" y="352">t</text><text class="st-axis-label" x="76" y="398">x</text></svg>
<figcaption markdown="span">The diamond $$\mathbf{B} = I^+(p) \cap I^-(q)$$ in one space and one time dimension: the part of the
future cone of $$p$$ that lies in the past cone of $$q$$.</figcaption>
</figure>

Why chronological rather than causal cones? With $$J^\pm$$, the region $$J^+(p) \cap J^-(q)$$ is, when
nonempty, compact, so not open, and for $$q = p$$ it is the single point $$\{p\}$$; an operator-valued
distribution has no value at a point, so there is no algebra of observables at a point to assign.
The chronological cones, and every diamond, are open.

The 1964 axioms of [Haag and Kastler (1964)](https://doi.org/10.1063/1.1704187) attach algebras instead to all open sets with compact
closure. That phrase needs a topology on $$\mathbb{R}^4$$, which the axioms do not name. The natural
candidate is the one built from the causal structure itself.

The _Alexandrov topology_ is the topology whose open sets are the unions of causal diamonds. For
this to define a topology, the diamonds must form a basis: the intersection of two diamonds must be
a union of diamonds. In Minkowski space it is, and the Alexandrov topology coincides with the usual
Euclidean topology of $$\mathbb{R}^4$$, but it is defined by the light cones alone, without reference
to a Euclidean metric that has no physical meaning. In a curved spacetime the two topologies can
differ; they agree precisely when the spacetime is _strongly causal_.

So, in this project, _Minkowski spacetime_ is $$\mathbb{R}^4$$ with the form $$\eta$$, the time
orientation given by the vector $$(1,0,0,0)$$, and the Alexandrov topology, and the regions of the
net are its causal diamonds. One fact about them is used throughout: any two diamonds lie in a
common, larger diamond (the diamonds are _upward directed_ under inclusion).

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that $$I^+(p) \cap I^-(q)$$ is nonempty if and only if $$p \ll q$$.

<details class="solution" markdown="1">
<summary>Solution</summary>

If $$x$$ lies in the intersection, then $$p \ll x$$ and $$x \ll q$$. The sum of two future-directed
timelike vectors is future-directed timelike (both lie in the open forward cone, which is convex),
so $$q - p = (q - x) + (x - p)$$ is future-directed timelike, and $$p \ll q$$. Conversely, if
$$p \ll q$$, the midpoint $$m = (p+q)/2$$ satisfies $$m - p = q - m = (q-p)/2$$, which is
future-directed timelike, so $$m$$ lies in the intersection.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that any two diamonds $$I^+(p_1) \cap I^-(q_1)$$ and $$I^+(p_2) \cap I^-(q_2)$$ lie in a common
diamond.

<details class="solution" markdown="1">
<summary>Solution</summary>

Choose $$p = (t, 0, 0, 0)$$ with $$t$$ so negative that $$p_k^0 - t > \vert \mathbf{p}_k\vert $$ for $$k = 1, 2$$,
where $$\mathbf{p}_k$$ is the spatial part of $$p_k$$. Then $$p_k - p$$ is future-directed timelike, so
$$p \ll p_k$$, and by transitivity of $$\ll$$ (the convexity argument of the previous exercise)
$$I^+(p_k) \subseteq I^+(p)$$. Choose $$q$$ in the same way, far in the future, so that
$$I^-(q_k) \subseteq I^-(q)$$. Then both diamonds lie in $$I^+(p) \cap I^-(q)$$.

</details>

</div>

**In the library:** `Physicslib4.MinkowskiSpacetime`, with the Alexandrov topology
`Physicslib4.Spacetime.alexandrovTopology` and the diamonds
`Physicslib4.Spacetime.chronologicalDiamond`.

## 1.3 C\*-algebras of observables

Recall that a Hilbert space $$\mathcal{H}$$ is a complex vector space with an inner product
$$\langle \cdot, \cdot \rangle$$, linear in the second argument, that is complete in the norm
$$\Vert \psi\Vert  = \langle \psi, \psi \rangle^{1/2}$$. A linear operator $$A$$ on $$\mathcal{H}$$ is bounded
if its operator norm $$\Vert A\Vert  = \sup_{\Vert \psi\Vert  = 1} \Vert A\psi\Vert $$ is finite; the bounded operators form
an algebra $$\mathcal{B}(\mathcal{H})$$. Each bounded $$A$$ has an adjoint $$A^*$$, defined by
$$\langle \psi, A\chi \rangle = \langle A^*\psi, \chi \rangle$$, and the observables of quantum
mechanics are the self-adjoint operators, $$A = A^*$$, whose spectra are the possible outcomes of a
measurement. (Physicists often write $$A^\dagger$$; this chapter writes $$A^*$$, as mathematicians
do.)

One identity links the algebra $$\mathcal{B}(\mathcal{H})$$ to its norm:

$$
\Vert A^* A\Vert  = \Vert A\Vert ^2.
$$

(The bound $$\Vert A\Vert ^2 \le \Vert A^*A\Vert $$ follows from $$\Vert A\psi\Vert ^2 = \langle \psi, A^*A\psi \rangle$$, and
$$\Vert A^*A\Vert  \le \Vert A^*\Vert \,\Vert A\Vert  = \Vert A\Vert ^2$$, since $$\Vert A^*\Vert  = \Vert A\Vert $$ for bounded operators.) The
abstract counterpart of $$\mathcal{B}(\mathcal{H})$$ keeps these properties and forgets the Hilbert
space.

A _C\*-algebra_ is a complex algebra $$\mathfrak{A}$$ with

* a norm in which it is complete, with $$\Vert ab\Vert  \le \Vert a\Vert \,\Vert b\Vert $$ (a Banach algebra);
* an _involution_ $$a \mapsto a^*$$: antilinear, with $$(ab)^* = b^*a^*$$ and $$a^{**} = a$$;
* the _C\*-identity_ $$\Vert a^*a\Vert  = \Vert a\Vert ^2$$ for every $$a$$.

It is _unital_ if it has a unit $$\mathbf{1}$$, with $$\mathbf{1}a = a\mathbf{1} = a$$. All the
algebras of this chapter are unital. Examples are $$\mathcal{B}(\mathcal{H})$$ itself, any
norm-closed subalgebra of it that is closed under adjoints, the matrix algebras $$M_n(\mathbb{C})$$,
and, as a commutative example, the continuous complex functions on a compact space with the supremum
norm and complex conjugation as involution.

A _\*-homomorphism_ $$\pi : \mathfrak{A} \to \mathfrak{B}$$ is a linear map with
$$\pi(ab) = \pi(a)\pi(b)$$ and $$\pi(a^*) = \pi(a)^*$$; it is _unital_ if
$$\pi(\mathbf{1}) = \mathbf{1}$$. A \*-homomorphism between C\*-algebras is automatically continuous,
with $$\Vert \pi(a)\Vert  \le \Vert a\Vert $$, and if it is injective it is isometric, $$\Vert \pi(a)\Vert  = \Vert a\Vert $$: the
norm of a C\*-algebra is fixed by its algebraic structure. An injective \*-homomorphism is a
_\*-monomorphism_, and a bijective one a _\*-isomorphism_. A _representation_ of $$\mathfrak{A}$$ on
a Hilbert space $$\mathcal{H}$$ is a \*-homomorphism
$$\pi : \mathfrak{A} \to \mathcal{B}(\mathcal{H})$$.

Nothing is lost by the abstraction: by the Gelfand–Naimark theorem, every C\*-algebra is
\*-isomorphic to a norm-closed, adjoint-closed algebra of operators on some Hilbert space. What is
gained is that no particular Hilbert space is singled out.

The self-adjoint elements $$a = a^*$$ of a C\*-algebra are its _observables_. The possible results of
measuring $$a$$ are the points of its _spectrum_,

$$
\sigma(a) = \{\lambda \in \mathbb{C} : a - \lambda\mathbf{1} \text{ has no inverse in } \mathfrak{A}\},
$$

a nonempty compact subset of $$\mathbb{R}$$ when $$a$$ is self-adjoint. The definition refers to the
algebra in which inverses are sought. For C\*-algebras the choice does not matter: if
$$\mathfrak{A}$$ is a C\*-subalgebra of $$\mathfrak{B}$$ with the same unit, an element of
$$\mathfrak{A}$$ has the same spectrum in both. This _spectral permanence_ fails for general Banach
algebras, and it is one reason the axioms ask for C\*-algebras: an observable measured in a small
region is also an observable of any larger region, and its possible values must not depend on which
region we regard it as belonging to.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$\mathfrak{A}$$ be a nonzero unital C\*-algebra. Show that $$\Vert a^*\Vert  = \Vert a\Vert $$ for every $$a$$,
that $$\mathbf{1}^* = \mathbf{1}$$, and that $$\Vert \mathbf{1}\Vert  = 1$$.

<details class="solution" markdown="1">
<summary>Solution</summary>

For $$a \neq 0$$, $$\Vert a\Vert ^2 = \Vert a^*a\Vert  \le \Vert a^*\Vert \,\Vert a\Vert $$, so $$\Vert a\Vert  \le \Vert a^*\Vert $$. Applying this to
$$a^*$$ gives $$\Vert a^*\Vert  \le \Vert a^{**}\Vert  = \Vert a\Vert $$. Next, $$\mathbf{1}^* a = (a^*\mathbf{1})^* = a$$ and
likewise $$a\mathbf{1}^* = a$$, so $$\mathbf{1}^*$$ is a unit, and units are unique. Finally
$$\Vert \mathbf{1}\Vert  = \Vert \mathbf{1}^*\mathbf{1}\Vert  = \Vert \mathbf{1}\Vert ^2$$, so $$\Vert \mathbf{1}\Vert $$ is $$0$$ or
$$1$$, and it is not $$0$$ because $$\mathbf{1} \neq 0$$ in a nonzero algebra.

</details>

</div>

**In the library:** C\*-algebras are Mathlib's class `CStarAlgebra` (unital, complex); the net assigns
one to each diamond in `Physicslib4.AQFT.HaagKastler.LocalNet`.

## 1.4 The axioms

A theory, in the Haag–Kastler framework, is a net of C\*-algebras on the diamonds of Minkowski
spacetime, subject to a short list of axioms, each of which rules something out. They are stated
here in the form this project uses.

### 1.4.1 Axiom 1: local algebras

To every causal diamond $$\mathbf{B}$$ there is assigned a unital C\*-algebra
$$\mathfrak{U}(\mathbf{B})$$, the algebra of observables measurable in $$\mathbf{B}$$. The empty
diamond is assigned the one-dimensional algebra $$\mathbb{C}\mathbf{1}$$ of multiples of the unit.

This axiom makes a theory an assignment of algebras to regions, not a field, and rules out
observables attached to single points.

### 1.4.2 Axiom 2: isotony

An observable that can be measured in a diamond $$\mathbf{B}_1$$ can also be measured in any larger
diamond $$\mathbf{B}_2 \supseteq \mathbf{B}_1$$. Since the algebras are abstract, "is also an element
of" must be supplied by a map. Isotony provides, for each such pair, a unital \*-monomorphism

$$
i_{\mathbf{B}_1\mathbf{B}_2} : \mathfrak{U}(\mathbf{B}_1) \to \mathfrak{U}(\mathbf{B}_2),
$$

and requires these maps to be coherent:

$$
i_{\mathbf{B}\mathbf{B}} = \mathrm{id}, \qquad i_{\mathbf{B}_2\mathbf{B}_3} \circ i_{\mathbf{B}_1\mathbf{B}_2} = i_{\mathbf{B}_1\mathbf{B}_3} \quad\text{for } \mathbf{B}_1 \subseteq \mathbf{B}_2 \subseteq \mathbf{B}_3.
$$

Because the maps are unital, every local algebra shares the unit of
$$\mathfrak{U}(\emptyset) = \mathbb{C}\mathbf{1}$$, and $$\mathbf{1}$$ means the same thing in every
region. Because they are injective, they are isometric, and by spectral permanence an observable has
the same spectrum in every algebra it is embedded in.

Isotony rules out a theory in which enlarging the region of an experiment changes the observable
being measured.

### 1.4.3 Axiom 3: local commutativity

If $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ are completely spacelike, their observables commute. To
multiply an element of $$\mathfrak{U}(\mathbf{B}_1)$$ by one of $$\mathfrak{U}(\mathbf{B}_2)$$, both
must lie in one algebra. Isotony supplies one: the algebra of any diamond $$\mathbf{B}$$ containing
both regions, and in Minkowski spacetime such a diamond exists. The axiom states that for every such
$$\mathbf{B}$$,

$$
i_{\mathbf{B}_1\mathbf{B}}(a_1)\, i_{\mathbf{B}_2\mathbf{B}}(a_2) = i_{\mathbf{B}_2\mathbf{B}}(a_2)\, i_{\mathbf{B}_1\mathbf{B}}(a_1) \qquad\text{for all } a_1 \in \mathfrak{U}(\mathbf{B}_1),\ a_2 \in \mathfrak{U}(\mathbf{B}_2).
$$

<figure class="tutorial-figure">
<svg aria-labelledby="st-diagram-title st-diagram-desc" class="st-diagram" role="img" viewbox="0 0 400 420" xmlns="http://www.w3.org/2000/svg"><title id="st-diagram-title">Two spacelike-separated diamonds inside a causal diamond</title><desc id="st-diagram-desc">A large causal diamond B contains two smaller diamonds B1 and B2 side by side. Dashed light-cone lines at 45 degrees from B1 bound its causal future and past; B2 lies outside them, so B1 and B2 are spacelike separated.</desc><defs><marker id="st-arrow" markerheight="7" markerwidth="7" orient="auto-start-reverse" refx="9" refy="5" viewbox="0 0 10 10"><path class="st-arrowhead" d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><polygon class="st-big" points="200,30 370,200 200,370 30,200"></polygon><line class="st-cone" x1="130" x2="272.5" y1="245" y2="102.5"></line><line class="st-cone" x1="130" x2="57.5" y1="245" y2="172.5"></line><line class="st-cone" x1="130" x2="272.5" y1="155" y2="297.5"></line><line class="st-cone" x1="130" x2="57.5" y1="155" y2="227.5"></line><polygon class="st-small" points="130,155 175,200 130,245 85,200"></polygon><polygon class="st-small" points="270,155 315,200 270,245 225,200"></polygon><text class="st-label" text-anchor="middle" x="200" y="70">B</text><text class="st-label st-label-small" text-anchor="middle" x="130" y="207">B₁</text><text class="st-label st-label-small" text-anchor="middle" x="270" y="207">B₂</text><line class="st-axis" marker-end="url(#st-arrow)" x1="20" x2="20" y1="405" y2="345"></line><line class="st-axis" marker-end="url(#st-arrow)" x1="20" x2="80" y1="405" y2="405"></line><text class="st-axis-label" x="28" y="352">t</text><text class="st-axis-label" x="76" y="398">x</text></svg>
<figcaption markdown="span">Two completely spacelike diamonds $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ inside a diamond
$$\mathbf{B}$$. The dashed lines bound the causal future and past of $$\mathbf{B}_1$$, which
$$\mathbf{B}_2$$ avoids.</figcaption>
</figure>

This is _Einstein causality_. Commuting observables can be measured together, and measuring one does
not change the statistics of the other (see the exercise below), so the axiom rules out signalling
faster than light. It does not rule out correlations: the vacuum of a quantum field is entangled
across spacelike separation.

### 1.4.4 Axiom 4: the quasilocal algebra

The local algebras fit together into a single algebra. Take all the $$\mathfrak{U}(\mathbf{B})$$ and
identify each $$a \in \mathfrak{U}(\mathbf{B}_1)$$ with its images $$i_{\mathbf{B}_1\mathbf{B}_2}(a)$$
in the larger algebras. The result is the _inductive limit_ of the local algebras (in
category-theory language, the directed colimit). Elements from $$\mathfrak{U}(\mathbf{B}_1)$$ and
$$\mathfrak{U}(\mathbf{B}_2)$$ are added or multiplied in any diamond containing both, and the
coherence laws of isotony make the answer independent of the choice; the norm is inherited, since
the embeddings are isometric. This normed \*-algebra completes to a C\*-algebra $$\mathfrak{U}$$, the
_quasilocal algebra_. It comes with unital \*-monomorphisms
$$\iota_{\mathbf{B}} : \mathfrak{U}(\mathbf{B}) \to \mathfrak{U}$$, compatible with isotony:
$$\iota_{\mathbf{B}_2} \circ i_{\mathbf{B}_1\mathbf{B}_2} = \iota_{\mathbf{B}_1}$$.

An element of $$\mathfrak{U}$$ need not belong to any single diamond, but it is approximated
arbitrarily well, in norm, by elements that do: hence _quasilocal_. Local commutativity can equally
be stated in $$\mathfrak{U}$$: $$\iota_{\mathbf{B}_1}(a_1)$$ and $$\iota_{\mathbf{B}_2}(a_2)$$ commute.

The 1964 axiom adds that $$\mathfrak{U}$$ contains "all observables of interest". This is a claim
about physics, not mathematics: it says that every quantity that can actually be measured is
represented by a self-adjoint element of $$\mathfrak{U}$$. For a set $$S$$ of bounded operators, the
_commutant_ $$S'$$ is the set of bounded operators that commute with every element of $$S$$. In a
representation $$\pi$$, the bicommutant $$\pi(\mathfrak{U})'' = (\pi(\mathfrak{U})')'$$ is, by von
Neumann's bicommutant theorem, the closure of $$\pi(\mathfrak{U})$$ in the weak operator topology,
and it is in general larger than $$\pi(\mathfrak{U})$$. But by the von Neumann density theorem, for
every $$T \in \pi(\mathfrak{U})''$$, every finite set of vectors $$\psi_1, \dots, \psi_n$$ and every
$$\varepsilon > 0$$ there is an $$a \in \mathfrak{U}$$ with
$$\Vert \pi(a)\psi_k - T\psi_k\Vert  < \varepsilon$$ for all $$k$$, so no finite set of measurements
distinguishes them. What the principle rules out is a measurable quantity that cannot be
approximated by local observables.

### 1.4.5 Axiom 5: Lorentz covariance

As you will recall, the Poincaré group consists of the maps $$x \mapsto \Lambda x + a$$ with
$$a \in \mathbb{R}^4$$ and $$\Lambda$$ a Lorentz transformation,
$$\eta(\Lambda v, \Lambda w) = \eta(v, w)$$. (Haag and Kastler call it the inhomogeneous Lorentz
group, hence the name of the axiom.) It has four connected components. The component of the
identity, the proper orthochronous group, has $$\det\Lambda = 1$$ and $$\Lambda^0{}_0 \geq 1$$; the
other three are reached by space and time reflections, which are not symmetries of nature (the weak
interaction violates parity), so the axiom uses only the identity component. Its elements $$L$$
preserve $$\ll$$, and therefore map diamonds to diamonds:
$$L(I^+(p) \cap I^-(q)) = I^+(Lp) \cap I^-(Lq)$$.

The axiom provides, for each such $$L$$ and each diamond $$\mathbf{B}$$, a unital \*-isomorphism

$$
\alpha_L : \mathfrak{U}(\mathbf{B}) \to \mathfrak{U}(L\mathbf{B}),
$$

with $$\alpha_e = \mathrm{id}$$ for the identity $$e$$ of the group,
$$\alpha_{L'L} = \alpha_{L'} \circ \alpha_L$$, and compatibility with isotony,
$$\alpha_L \circ i_{\mathbf{B}_1\mathbf{B}_2} = i_{L\mathbf{B}_1\,L\mathbf{B}_2} \circ \alpha_L$$.
The maps then extend, by continuity, to automorphisms of $$\mathfrak{U}$$. The laws of physics are
thus the same at every place and in every inertial frame; the axiom rules out a preferred origin or
a preferred rest frame.

### 1.4.6 An aside: primitivity

The 1964 list has a sixth axiom: $$\mathfrak{U}$$ is _primitive_, that is, it has a representation
that is both faithful (injective) and irreducible (no closed subspace other than $$0$$ and the whole
space is invariant). Its physical motivation is thin, and Haag's later account in _Local Quantum
Physics_ omits it. This project omits it too. For orientation: a commutative C\*-algebra is
primitive only if it is $$\mathbb{C}\mathbf{1}$$, so the axiom excludes classical nets other than the
trivial one.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$\omega$$ be a state, a positive normalised expectation functional (defined in the next
section), and let $$P \in \mathfrak{U}(\mathbf{B}_1)$$ be a projection, $$P = P^* = P^2$$. A
measurement of $$P$$ whose result is not recorded changes the state to
$$\omega'(b) = \omega(PbP) + \omega((\mathbf{1}-P)\,b\,(\mathbf{1}-P))$$. Show that
$$\omega'(b) = \omega(b)$$ for every $$b$$ that commutes with $$P$$, in particular for every $$b$$ in a
completely spacelike region. What does this say about signalling?

<details class="solution" markdown="1">
<summary>Solution</summary>

If $$bP = Pb$$, then $$PbP = bP^2 = bP$$ and
$$(\mathbf{1}-P)b(\mathbf{1}-P) = b(\mathbf{1}-P)^2 = b(\mathbf{1}-P)$$, because $$\mathbf{1}-P$$ is
also a projection. The sum is $$bP + b - bP = b$$, so $$\omega'(b) = \omega(b)$$. By local
commutativity this holds for every observable $$b$$ of a region completely spacelike to
$$\mathbf{B}_1$$: an observer there sees the same expectation values whether or not the measurement
in $$\mathbf{B}_1$$ took place, so the measurement cannot be used to send a signal.

</details>

</div>

**In the library:** `Physicslib4.AQFT.HaagKastler.LocalNet`, `Physicslib4.AQFT.HaagKastler.Isotony`,
`Physicslib4.AQFT.HaagKastler.LocalCommutativity`, `Physicslib4.AQFT.HaagKastler.QuasilocalAlgebra`
and `Physicslib4.AQFT.HaagKastler.LorentzCovariance`.

## 1.5 States and the GNS construction

To make predictions, the axioms need a state: an assignment of expectation values to observables.

A _state_ on a unital C\*-algebra $$\mathfrak{A}$$ is a linear functional
$$\omega : \mathfrak{A} \to \mathbb{C}$$ that is

* _positive_: $$\omega(a^*a) \geq 0$$ for every $$a$$;
* _normalised_: $$\Vert \omega\Vert  = 1$$, which for a positive functional is the same as
  $$\omega(\mathbf{1}) = 1$$.

The number $$\omega(a)$$ is the expectation value of the observable $$a$$. The familiar states of
quantum mechanics are examples: for a representation $$\pi$$ on $$\mathcal{H}$$, a unit vector $$\psi$$
gives the vector state $$\omega(a) = \langle \psi, \pi(a)\psi \rangle$$, and a density matrix $$\rho$$
gives $$\omega(a) = \operatorname{tr}(\rho\,\pi(a))$$. The states form a convex set; its extreme
points, the states that are not mixtures of two others, are the _pure_ states. A state is _faithful_
if $$\omega(a^*a) > 0$$ whenever $$a \neq 0$$.

### 1.5.1 The GNS construction

A state determines a Hilbert space representation, uniquely up to unitary equivalence, by a theorem
of Gelfand, Naimark and Segal.

_Let $$\omega$$ be a state on a unital C\*-algebra $$\mathfrak{A}$$. There are a Hilbert space
$$\mathcal{H}_\omega$$, a representation $$\pi_\omega$$ of $$\mathfrak{A}$$ on it and a unit vector
$$\Omega_\omega$$ such that_

$$
\omega(a) = \langle \Omega_\omega, \pi_\omega(a)\,\Omega_\omega \rangle \quad\text{for all } a \in \mathfrak{A},
$$

_and $$\Omega_\omega$$ is cyclic: the vectors $$\pi_\omega(a)\Omega_\omega$$ are dense in
$$\mathcal{H}_\omega$$. Any two such triples are related by a unitary map. If $$\omega$$ is faithful,
so is $$\pi_\omega$$._

The proof builds the Hilbert space out of the algebra, in four steps.

1. **A semi-inner product.** Define $$\langle a, b \rangle = \omega(a^*b)$$ on $$\mathfrak{A}$$. It is
   linear in $$b$$, conjugate-linear in $$a$$, and $$\langle a, a \rangle \geq 0$$ by positivity, so it
   satisfies the Cauchy–Schwarz inequality $$\vert \omega(a^*b)\vert ^2 \le \omega(a^*a)\,\omega(b^*b)$$. It is
   not an inner product, because $$\omega(a^*a)$$ may vanish for $$a \neq 0$$.
2. **The null space.** Let $$\mathcal{N} = \{n : \omega(n^*n) = 0\}$$. By Cauchy–Schwarz,
   $$\mathcal{N}$$ is a subspace and a left ideal: $$an \in \mathcal{N}$$ for all $$a$$ and all
   $$n \in \mathcal{N}$$. On the quotient $$\mathfrak{A}/\mathcal{N}$$, the form
   $$\langle [a], [b] \rangle = \omega(a^*b)$$ is well defined and is an inner product.
3. **Completion and representation.** $$\mathcal{H}_\omega$$ is the completion of
   $$\mathfrak{A}/\mathcal{N}$$. The algebra acts by left multiplication, $$\pi_\omega(a)[b] = [ab]$$,
   which is well defined because $$\mathcal{N}$$ is a left ideal, and bounded,
   $$\Vert [ab]\Vert  \le \Vert a\Vert \,\Vert [b]\Vert $$, because $$b^*a^*ab \le \Vert a\Vert ^2\, b^*b$$. It extends to the
   completion, and $$\pi_\omega(a^*) = \pi_\omega(a)^*$$ follows from
   $$\omega((a^*b)^*c) = \omega(b^*(ac))$$.
4. **The cyclic vector.** $$\Omega_\omega = [\mathbf{1}]$$. Then $$\pi_\omega(a)\Omega_\omega = [a]$$,
   so these vectors are all of $$\mathfrak{A}/\mathcal{N}$$, which is dense, and
   $$\langle \Omega_\omega, \pi_\omega(a)\Omega_\omega \rangle = \omega(\mathbf{1}^*a) = \omega(a)$$.

Here the unit is used: without it there is no vector $$[\mathbf{1}]$$. Uniqueness comes from mapping
$$\pi_1(a)\Omega_1 \mapsto \pi_2(a)\Omega_2$$, which preserves inner products because both equal
$$\omega(a^*b)$$. Faithfulness: if $$\pi_\omega(a) = 0$$, then $$[a] = 0$$, so $$\omega(a^*a) = 0$$ and,
for faithful $$\omega$$, $$a = 0$$.

The GNS construction connects the abstract algebras to the Hilbert spaces of ordinary quantum
theory: applied to a state on $$\mathfrak{U}$$, it gives the Hilbert space of the theory in that
state, with $$\pi_\omega(a)$$ the operator of the observable $$a$$. The state is pure exactly when
$$\pi_\omega$$ is irreducible.

### 1.5.2 The vacuum

A _vacuum state_ is a state $$\omega$$ on $$\mathfrak{U}$$ that is invariant and has positive energy.

It is _invariant_ if $$\omega \circ \alpha_L = \omega$$ for every $$L$$ in the identity component of
the Poincaré group. Then $$U(L)\,\pi_\omega(a)\Omega_\omega = \pi_\omega(\alpha_L a)\Omega_\omega$$
defines unitaries on $$\mathcal{H}_\omega$$ that represent the group, leave $$\Omega_\omega$$ fixed
and implement the symmetry: $$U(L)\,\pi_\omega(a)\,U(L)^{-1} = \pi_\omega(\alpha_L a)$$ (see the
second exercise below).

Recall Stone's theorem: a strongly continuous one-parameter group of unitaries has the form
$$U(t) = e^{itH}$$ with a self-adjoint, in general unbounded, generator $$H$$. For the time
translations, $$H$$ is the Hamiltonian. _Positive energy_, or the _spectrum condition_, requires that
for every future-directed timelike vector $$a$$ the translations $$t \mapsto U(ta)$$ form such a group
with nonnegative generator; equivalently, the joint spectrum of the energy-momentum operators lies
in the closed forward light cone. This makes the vacuum a state of lowest energy.

### 1.5.3 Superselection sectors

Different states can give inequivalent representations of the same algebra $$\mathfrak{U}$$. Two
irreducible representations $$\pi_1$$ and $$\pi_2$$ are either unitarily equivalent or _disjoint_: no
nonzero bounded operator $$T$$ satisfies $$T\pi_1(a) = \pi_2(a)T$$ for all $$a$$. The equivalence
classes of the irreducible representations of physical interest are the _superselection sectors_ of
the theory, labelled by conserved charges such as electric charge. No observable in $$\mathfrak{U}$$
connects two sectors, so a superposition of state vectors from different sectors cannot be told
apart from the corresponding mixture: the relative phase is not measurable.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$\mathfrak{A} = M_2(\mathbb{C})$$ and $$\omega(a) = a_{11}$$, the state given by the unit vector
$$e_1$$. Find $$\mathcal{N}$$, $$\mathcal{H}_\omega$$, $$\pi_\omega$$ and $$\Omega_\omega$$. What changes
for the faithful state $$\omega(a) = \tfrac{1}{2}\operatorname{tr} a$$?

<details class="solution" markdown="1">
<summary>Solution</summary>

$$\omega(n^*n) = (n^*n)_{11} = \Vert n e_1\Vert ^2$$, so $$\mathcal{N}$$ is the set of matrices whose first
column is zero. The map $$[a] \mapsto a e_1$$ identifies $$\mathfrak{A}/\mathcal{N}$$ with
$$\mathbb{C}^2$$, preserving inner products since $$\omega(a^*b) = \langle a e_1, b e_1 \rangle$$.
Under it, $$\pi_\omega(a)$$ is the matrix $$a$$ acting on $$\mathbb{C}^2$$ and $$\Omega_\omega = e_1$$:
the GNS construction returns the defining representation. For
$$\omega = \tfrac12 \operatorname{tr}$$, $$\mathcal{N} = 0$$, and $$\mathcal{H}_\omega$$ is
$$M_2(\mathbb{C})$$ itself, four-dimensional, with
$$\langle a, b \rangle = \tfrac12 \operatorname{tr}(a^*b)$$. The algebra acts by left multiplication
and $$\Omega_\omega = \mathbf{1}$$. The representation is faithful but reducible: the two columns of
a matrix are invariant subspaces, each a copy of $$\mathbb{C}^2$$. This matches the facts that the
first state is pure and the second is a mixture.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that the operators $$U(L)$$ defined above for an invariant state are well defined and preserve
inner products.

<details class="solution" markdown="1">
<summary>Solution</summary>

For $$a, b \in \mathfrak{U}$$,

$$
\langle \pi_\omega(\alpha_L a)\Omega_\omega, \pi_\omega(\alpha_L b)\Omega_\omega \rangle = \omega(\alpha_L(a^*b)) = \omega(a^*b) = \langle \pi_\omega(a)\Omega_\omega, \pi_\omega(b)\Omega_\omega \rangle,
$$

using that $$\alpha_L$$ is a \*-homomorphism and that $$\omega$$ is invariant. So the map preserves
inner products on the dense set of vectors $$\pi_\omega(a)\Omega_\omega$$. In particular, if
$$\pi_\omega(a)\Omega_\omega = 0$$, its image has norm zero, so the map is well defined. It extends
by continuity to an isometry of $$\mathcal{H}_\omega$$, and it is onto because $$U(L^{-1})$$ inverts
it.

</details>

</div>

**In the library:** `Physicslib4.GNS.State`, `Physicslib4.GNS.gns_construction`, and for the vacuum
`Physicslib4.AQFT.HaagKastler.HaagKastlerNet.IsVacuumState`.

## 1.6 What this project sharpens

The axioms of [Haag and Kastler (1964)](https://doi.org/10.1063/1.1704187) leave open some details that a proof needs. The project's
blueprint fixes them, and the formal statements are checked against the blueprint. The forms above
differ from the 1964 text in these points.

* **Topology and regions.** Minkowski spacetime carries the Alexandrov topology, and the regions are
  the causal diamonds, including the empty one, rather than all open sets with compact closure in an
  unnamed topology.
* **The unit.** The 1964 isotony axiom allows the two algebras of each nested pair to have a common
  unit or neither to have one. Here all have one, fixed by
  $$\mathfrak{U}(\emptyset) = \mathbb{C}\mathbf{1}$$ and unital embeddings; the GNS construction
  needs it.
* **Isotony as data.** "$$\mathfrak{U}(\mathbf{B}_1) \subset \mathfrak{U}(\mathbf{B}_2)$$" becomes a
  chosen family of \*-monomorphisms with identity and composition laws, without which the union of
  the local algebras has no well-defined product.
* **Local commutativity in a containing diamond,** using only the net and isotony; in Minkowski
  spacetime this is equivalent to commutation in $$\mathfrak{U}$$.
* **The quasilocal algebra is constructed** from the local algebras and isotony, not assumed. The
  claim that it contains all observables of interest is kept apart as a physical principle.
* **The symmetry group.** Covariance uses the identity component of the Poincaré group, and the
  transported algebras must respect isotony.
* **Primitivity** is dropped.

The sharpened axioms carry over to a curved spacetime, a four-dimensional Lorentzian manifold used
as a fixed classical background, provided its Alexandrov topology is Hausdorff (equivalently, the
spacetime is strongly causal; the Alexandrov and manifold topologies then agree). The local algebras
and isotony are unchanged, and the Poincaré group is replaced by the isometries connected to the
identity.

One thing fails: two diamonds need not lie in a common diamond. In a Schwarzschild black hole, a
diamond just below the singularity and a diamond outside the horizon at sufficiently late times have
none: the top vertex of a common diamond would have to lie in the future of both, and inside the
hole the future of the first ends on the singularity before it meets the future of the second. Their
algebras then lie in no common algebra, and there is no quasilocal algebra. Local commutativity is
stated, as above, inside every diamond that contains both regions, and says nothing when there is
none: no experiment could compare the two. "All observables of interest" becomes a statement about
the local algebras.

This differs from the locally covariant framework of [Brunetti, Fredenhagen and Verch (2003)](https://doi.org/10.1007/s00220-003-0815-7), in
which a theory is a functor on a category of globally hyperbolic spacetimes; here it is a net on one
fixed spacetime. Later chapters develop both the Minkowski and the curved-spacetime axioms in Lean.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$M$$ be the strip $$-1 < x^0 < 1$$ of two-dimensional Minkowski space, with the causal structure
of Minkowski space. Show that two small diamonds centred at $$(0, 0)$$ and $$(0, 10)$$ lie in no
common diamond of $$M$$.

<details class="solution" markdown="1">
<summary>Solution</summary>

A diamond of $$M$$ is $$I^+(p) \cap I^-(q)$$ with $$p, q \in M$$, so $$q^0 - p^0 < 2$$. A point $$x$$ of
it satisfies $$\vert x^1 - p^1\vert  < x^0 - p^0$$ and $$\vert q^1 - x^1\vert  < q^0 - x^0$$. Adding the two inequalities,
$$\vert 2x^1 - p^1 - q^1\vert  < q^0 - p^0 < 2$$, so all points of the diamond have $$x^1$$ within $$1$$ of
$$(p^1 + q^1)/2$$. The two given diamonds contain points whose $$x^1$$ coordinates differ by almost
$$10$$, so no diamond of $$M$$ contains both.

</details>

</div>

**In the library:** the curved-spacetime net is `Physicslib4.AQFT.HaagKastlerCurved.HaagKastlerNet`,
and the physical principle of the quasilocal algebra is
`Physicslib4.AQFT.HaagKastler.ObservableCorrespondence`.

## 1.7 Further reading

* Rudolf Haag, [_Local Quantum Physics: Fields, Particles,
  Algebras_](https://doi.org/10.1007/978-3-642-61458-3), 2nd edition, Springer, 1996. The standard
  monograph.
* Rudolf Haag and Daniel Kastler, "[An algebraic approach to quantum field theory](https://doi.org/10.1063/1.1704187)", _Journal of Mathematical Physics_ 5(7), 848–861, 1964. The paper that introduced the axioms.
* Romeo Brunetti, Klaus Fredenhagen and Rainer Verch, "[The generally covariant locality principle: a new paradigm for local quantum field theory](https://doi.org/10.1007/s00220-003-0815-7)", _Communications in Mathematical Physics_ 237(1–2), 31–68, 2003. The locally covariant framework, on all globally
  hyperbolic spacetimes at once.
* Rafael Grossi, "[Entanglement in Algebraic Quantum Field Theories](https://arxiv.org/abs/2410.16599)", arXiv:2410.16599, 2024. A clear introduction to C\*-algebras, states, the GNS construction and
  nets, whose proof of the GNS theorem the blueprint follows.
* The [physicslib4 blueprint](https://physicslib.github.io/physicslib4/blueprint/). Chapters 1 to 9
  discuss each 1964 axiom and the choices made in sharpening it; Chapter 10 states the sharpened
  axioms and the results proved about them.

# 2. Lean in brief {#lean-in-brief}

This chapter teaches enough Lean to read the library: its definitions, its statements and its
proofs. It assumes no experience with a proof assistant. By the end you should be able to take a
declaration such as `LocalNet` or `LocalCommutativity`, say what it means in the language of
chapter 1, follow a short proof step by step, and write a small proof of your own. It does not
teach Lean in general; the books listed at the end do that.

Every piece of Lean code in this chapter is checked by Lean against the library when the tutorial
is built. Hover over a name to see its type. In a proof, click a tactic to show or hide the goal
that remains after it. The exercises can be read here, but not run: chapter 4 explains how to set up
Lean on your own machine and work with the library there.

## 2.1 What a proof assistant does {#lean-in-brief-checking}

A _proof assistant_ is a program that checks mathematical definitions and proofs written in a
formal language. Lean 4 is both a programming language and a proof assistant. You write
definitions, statements and proofs in a file; Lean reads each one, fills in the details you leave
implicit (types, coercions, routine arguments), and then checks the result. The final check is done
by a small program called the _kernel_, which knows only a few rules of logic. Everything else in
Lean, including the automation that finds proofs for you, produces a proof that the kernel must
accept. To trust a theorem you therefore trust the kernel, a few standard axioms, and the
statement itself: that it says what you mean.

A wrong proof is rejected. Here Lean is asked to prove $$2 + 2 = 5$$ by computation and refuses:

```lean
example : 2 + 2 = 5 := by
  rfl
```

<pre class="lean-output">Tactic `rfl` failed: The left-hand side
  2 + 2
is not definitionally equal to the right-hand side
  5

⊢ 2 + 2 = 5</pre>

The word `sorry` stands for a missing proof. Lean accepts a declaration that contains it, so that
you can work on the rest of a file, but warns that the declaration uses `sorry`. The exercises of
this chapter use it for the part you are to fill in.

```lean
example : 2 + 2 = 4 := by
  sorry
```

<pre class="lean-output">declaration uses `sorry`</pre>

Two words describe the state of this library.

* A definition or theorem is _formalised_ when it is a Lean declaration whose statement matches the
  blueprint. Matching the blueprint is checked by people, not by Lean: Lean checks that a proof
  proves the statement, not that the statement is the one intended.
* The library is _sorry-free_: no proof in it contains `sorry`.

The command `#print axioms` lists the axioms a theorem depends on, and it is how the second point
is checked. Here it is for the theorem that the algebra of the empty region is commutative, a
consequence of Axiom 1:

```lean
open Physicslib4.AQFT.HaagKastler in
#print axioms LocalNet.mul_comm_algebra_empty
```

<pre class="lean-output">&#x27;Physicslib4.AQFT.HaagKastler.LocalNet.mul_comm_algebra_empty&#x27; depends on axioms: [propext,
 Classical.choice,
 Quot.sound]</pre>

These three are the standard axioms of Lean's mathematics: propositional extensionality (two
equivalent statements are equal), the axiom of choice, and the soundness of quotients. A proof
with a gap would also list `sorryAx`.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Why does a theorem whose proof uses `sorry` prove nothing, even though Lean accepts the file? And
why can `#print axioms` not tell you whether a sorry-free theorem states the right thing?

<details class="solution" markdown="1">
<summary>Solution</summary>

`sorry` is elaborated as the axiom `sorryAx`, which produces a term of any type, so it "proves"
every statement, false ones included. `#print axioms` lists what a proof depends on; it says nothing
about the statement. A sorry-free proof of a statement that misrepresents the mathematics (a wrong
definition, a hypothesis that can never hold) is still a correct proof of that statement. This is
why the project checks each statement against the blueprint by reading it.

</details>

</div>

## 2.2 Types and terms {#lean-in-brief-types}

You will know that in ordinary mathematics everything is built from sets: a number, a function
and a Hilbert space are all sets, and $$x \in A$$ is a statement about two sets. Lean is built on a
different foundation, _type theory_. Every object has a _type_, and a _term_ of a type is an object
of that type. Writing `x : T` means "`x` is a term of type `T`". The type is part of what the object
is, not a property it may or may not have: a real number is a term of type `ℝ`, and the question
"is $$2 \in \mathbb{R}$$?" does not arise, because `(2 : ℝ)` and `(2 : ℂ)` are different terms of
different types.

The command `#check` shows the type of a term, and `#eval` computes the value of a term when it can
be computed:

```lean
#check (2 : ℝ)
```

<pre class="lean-output">2 : ℝ</pre>

```lean
#eval 2 + 3
```

<pre class="lean-output">5</pre>

A function from `X` to `Y` is a term of type `X → Y`. It is written with `fun`, and applied by
juxtaposition: `f x` rather than $$f(x)$$.

```lean
#check fun x : ℝ => x ^ 2
```

<pre class="lean-output">fun x =&gt; x ^ 2 : ℝ → ℝ</pre>

A function of two arguments is a function that returns a function: `X → Y → Z` means
`X → (Y → Z)`, and `g x y` means `(g x) y`. The subsets of a type `X` form a type `Set X`, written
with the familiar set-builder notation:

```lean
#check {x : ℝ | 0 < x}
```

<pre class="lean-output">{x | 0 &lt; x} : Set ℝ</pre>

Types are themselves terms: `ℝ` has type `Type`, the type of types, as do `Set ℝ` and `ℝ → ℝ`.

### 2.2.1 Points and regions

Minkowski spacetime is a term `StandardMinkowskiSpacetime` of type `Spacetime`, and the type of
its points is `StandardMinkowskiSpacetime.Carrier`, the field `Carrier` of the structure
`StandardMinkowskiSpacetime` ([section 5](#lean-in-brief-structures)). A region is a term of
type `Set StandardMinkowskiSpacetime.Carrier`. The library's names are long, because they are
organised in _namespaces_ ([section 7](#lean-in-brief-mathlib)); the command below makes the
short names available, and all the code that follows uses them.

```lean
open Physicslib4 Spacetime AQFT.HaagKastler
```

```lean
#check StandardMinkowskiSpacetime.Carrier
```

<pre class="lean-output">StandardMinkowskiSpacetime.Carrier : Type</pre>

The diamond $$I^+(p) \cap I^-(q)$$ of chapter 1 is, in the library, the _chronological diamond_
`chronologicalDiamond M t p q`, for a spacetime `M`, a time orientation `t` and two points `p` and
`q`. The library keeps the name `causalDiamond` for the closed version $$J^+(p) \cap J^-(q)$$, which
[section 4](#lean-in-brief-tactics) uses.

```lean
#check chronologicalDiamond
```

<pre class="lean-output">Physicslib4.Spacetime.chronologicalDiamond (M : Spacetime) (t : M.TimeOrientation) (p q : M.Carrier) : Set M.Carrier</pre>

This is the form in which the library writes its declarations: the name, then the arguments, each
in parentheses with its type, then a colon and the type of the result. Here the result is a set of
points of `M`.

### 2.2.2 Dependent functions

The arguments of `chronologicalDiamond` begin with `(M : Spacetime)`, and the types of the others
mention `M`: `t` is a time orientation _of `M`_, and `p` and `q` are points _of `M`_. As a type,
`chronologicalDiamond` is `(M : Spacetime) → M.TimeOrientation → M.Carrier → M.Carrier → Set
M.Carrier`. This is a _dependent function type_. The type of the output, or of later arguments,
depends on the value of an earlier argument. In mathematics such functions are common: a vector
field, a section of the tangent bundle, assigns to each point $$x$$ a vector in $$T_x M$$, a space
that changes with $$x$$. Lean writes the type of such a function as `(x : X) → T x`, or equivalently
`∀ x, T x`.

The net of chapter 1 is the central example. It assigns to each region $$\mathbf{B}$$ an algebra
$$\mathfrak{U}(\mathbf{B})$$, and an observable of the region is an element
$$a \in \mathfrak{U}(\mathbf{B})$$. In Lean, a net `U` has a function `U.algebra` from regions to
types, and an observable of `B` is a term `a : U.algebra B`, whose type depends on `B`. The notation
`U.algebra B` is short for `LocalNet.algebra U B`: when `U` has type `LocalNet`, Lean looks up
`algebra` in the namespace `LocalNet`. This "dot notation" is used throughout the library.

```lean
#check LocalNet.algebra
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastler.LocalNet.algebra.{u_1} (self : LocalNet) :
  Set StandardMinkowskiSpacetime.Carrier → Type u_1</pre>

(The `u_1` is a universe level; [section 5](#lean-in-brief-structures) explains it.)

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Replace `sorry` by the set of real numbers strictly between $$0$$ and $$1$$, and by an element of the
local algebra of a region `B`.

```lean
example : Set ℝ := sorry

example (U : LocalNet)
    (B : Set StandardMinkowskiSpacetime.Carrier) :
    U.algebra B := sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example : Set ℝ := {x | 0 < x ∧ x < 1}

example (U : LocalNet)
    (B : Set StandardMinkowskiSpacetime.Carrier) :
    U.algebra B := 1
```

Every local algebra is a unital C\*-algebra, so it has a unit `1` (and a zero `0`). Lean finds the
unit of `U.algebra B` by itself; [section 5](#lean-in-brief-structures) explains how.

</details>

</div>

## 2.3 Propositions and proofs {#lean-in-brief-propositions}

You will be used to building statements from a few connectives: "for all" ($$\forall$$), "there
exists" ($$\exists$$), "implies" ($$\Rightarrow$$), "and", "or", "not" and "if and only if". Lean
uses the same connectives, written `∀`, `∃`, `→`, `∧`, `∨`, `¬` and `↔`. A statement is a term of
the type `Prop`, the type of propositions:

```lean
#check 2 + 2 = 4
```

<pre class="lean-output">2 + 2 = 4 : Prop</pre>

### 2.3.1 Propositions as types

The step that makes Lean work is to treat each proposition as a type in its own right, whose terms
are its proofs. Writing `h : P` means "`h` is a proof of `P`". A true proposition has proofs, a
false one has none, and checking a proof means checking that a term has the type it claims. Each
connective then corresponds to a construction on types, and the proofs follow:

* A proof of `P → Q` is a function that turns any proof of `P` into a proof of `Q`. Using an
  implication `h : P → Q` on a proof `hp : P` is function application, `h hp`.
* A proof of `∀ x, P x` is a dependent function: for each `x`, a proof of `P x`. Applying it to a
  particular `a` gives `h a : P a`.
* A proof of `P ∧ Q` is a pair `⟨hp, hq⟩`; from `h : P ∧ Q`, the components are `h.1 : P` and
  `h.2 : Q`.
* A proof of `∃ x, P x` is a pair of a witness `a` and a proof of `P a`, written `⟨a, ha⟩`.
* `P ↔ Q` is a pair of implications, and `¬ P` is `P → False`.

### 2.3.2 Theorems and examples

A theorem is written `theorem name (arguments) : statement := proof`. The arguments are the
objects and hypotheses of the statement. Here is one from the library, as `#check` shows it:

```lean
#check causallyPrecedes_of_chronologicallyPrecedes
```

<pre class="lean-output">Physicslib4.Spacetime.causallyPrecedes_of_chronologicallyPrecedes (M : Spacetime) (t : M.TimeOrientation)
  {p q : M.Carrier} (h : p ≪[M, t] q) : p ≺[M, t] q</pre>

It says that chronological precedence implies causal precedence: if $$p \ll q$$, then
$$p \prec q$$. The library writes `p ≪[M, t] q` and `p ≺[M, t] q`, naming the spacetime and the
time orientation. Arguments in curly braces, like `{p q : M.Carrier}`, are _implicit_: you do not
supply them, because Lean can read them off the type of `h`. The hypothesis `h` is an argument like
any other, and the theorem itself is a function from proofs of `p ≪[M, t] q` to proofs of
`p ≺[M, t] q`.

As in chapter 1, `≺` is reflexive: `p ≺[M, t] p` always holds (`causallyPrecedes_refl`), the
trivial case `p = q`. The strict version, which asks for a genuine causal curve from `p` to `q`, is
`IsCausalTrip M t p q`:

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    (p q : M.Carrier) :
    (p ≺[M, t] q) ↔ p = q ∨ IsCausalTrip M t p q :=
  causallyPrecedes_iff_eq_or_isCausalTrip M t
```

An `example` is a theorem without a name, checked and then forgotten. Here the theorem above is
used as a function:

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q : M.Carrier} (h : p ≪[M, t] q) : p ≺[M, t] q :=
  causallyPrecedes_of_chronologicallyPrecedes M t h
```

The simplest proofs are by definition. `rfl` proves `a = a`, and more generally an equation whose
two sides are equal once the definitions are unfolded; `Iff.rfl` does the same for `↔`. A point lies
in the diamond $$I^+(p) \cap I^-(q)$$ exactly when $$p \ll x$$ and $$x \ll q$$, and in the library
this holds by definition, since an intersection is defined by "and" (the parentheses are needed
because of how the library's notation `≪[M, t]` parses):

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier} :
    x ∈ chronologicalDiamond M t p q ↔
      (p ≪[M, t] x) ∧ (x ≪[M, t] q) :=
  Iff.rfl
```

Since the two sides are the same proposition, a proof `h` of membership in the diamond is itself a
pair, and `h.1 : p ≪[M, t] x`.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Replace each `sorry` by a proof term. The first statement says that a point of a diamond lies in
the chronological future of its lower vertex; the second, that a nonempty diamond has
$$p \ll q$$. The library's theorem `chronologicallyPrecedes_trans M t` turns proofs of `p ≪[M, t] x`
and `x ≪[M, t] q` into a proof of `p ≪[M, t] q`.

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier}
    (h : x ∈ chronologicalDiamond M t p q) :
    p ≪[M, t] x :=
  sorry

example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier}
    (h : x ∈ chronologicalDiamond M t p q) :
    p ≪[M, t] q :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier}
    (h : x ∈ chronologicalDiamond M t p q) :
    p ≪[M, t] x :=
  h.1

example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier}
    (h : x ∈ chronologicalDiamond M t p q) :
    p ≪[M, t] q :=
  chronologicallyPrecedes_trans M t h.1 h.2
```

Membership in the diamond is, by definition, the conjunction `(p ≪[M, t] x) ∧ (x ≪[M, t] q)`, so
`h.1` and `h.2` are its two halves. This is the first half of the first exercise of chapter 1, in
Lean.

</details>

</div>

## 2.4 Tactic proofs {#lean-in-brief-tactics}

Longer proofs are written not as one term but, after `by`, as a sequence of _tactics_:
instructions that build the term step by step. At each step Lean
keeps a _proof state_: the hypotheses available, and the _goal_ that remains to be proved. It is
displayed as

```text
h₁ : hypothesis
h₂ : another hypothesis
⊢ goal
```

with the goal after the turnstile `⊢`. Each tactic changes the state, and the proof is finished
when no goals remain. Reading a tactic proof means following these states.

### 2.4.1 A small vocabulary

Most proofs in the library use a handful of tactics, each the counterpart of a phrase of written
mathematics:

* `intro x hx`: "let `x` be arbitrary and suppose `hx`." It applies to a goal `∀ x, …` or `P → Q`.
* `exact e`: "this follows from `e`." It closes the goal with a term `e` of exactly that type.
* `apply f`: "by `f`, it suffices to show …." It replaces the goal by the hypotheses of `f` that
  are still needed.
* `constructor`: splits a goal `P ∧ Q` (or `P ↔ Q`) into two goals.
* `rcases h with ⟨a, ha⟩` (or `obtain ⟨a, ha⟩ := h`): takes apart a hypothesis `h : ∃ x, P x` or
  `h : P ∧ Q`: "choose `a` with `ha`."
* `rw [e]`: rewrites the goal with an equation `e : a = b` or an equivalence `e : P ↔ Q`,
  replacing the left side by the right. `rw [e] at h` rewrites a hypothesis instead.
* `simp`: simplifies the goal with a large collection of lemmas, and closes it if it becomes
  trivial.
* `calc`: a chain of equalities or inequalities, each step with its own proof.
* `linarith`: closes goals that follow from the hypotheses by linear arithmetic over an ordered
  field such as `ℝ`.

As an example of `constructor`, a point lies in a diamond if it lies above the lower vertex and
below the upper one. The goal is a membership, but `constructor` sees through its definition to
the conjunction, as `Iff.rfl` showed in [section 3](#lean-in-brief-propositions). The two
goals it creates are each closed by `exact`; the dots `·` mark the proof of each goal.

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q x : M.Carrier}
    (hp : p ≪[M, t] x) (hq : x ≪[M, t] q) :
    x ∈ chronologicalDiamond M t p q := by
  constructor
  · exact hp
  · exact hq
```

Recall that a proof by cases splits a statement into finitely many cases that together cover all
possibilities. In Lean, `rcases h with h | h` splits a hypothesis `h : P ∨ Q` into the case `P` and
the case `Q`. Here $$x \cdot x \geq 0$$ is proved from the two cases $$x \geq 0$$ and
$$x \leq 0$$, using two of Mathlib's lemmas:

```lean
example (x : ℝ) : 0 ≤ x * x := by
  rcases le_total 0 x with h | h
  · exact mul_nonneg h h
  · exact mul_nonneg_of_nonpos_of_nonpos h h
```

Proof by induction is the tactic `induction`, which the library seldom needs. Finally, `calc` and
`linarith` handle routine algebra, and `simp` routine simplification:

```lean
example (a b c : ℝ) (h₁ : a = b + 1) (h₂ : b = 2 * c) :
    a = 2 * c + 1 := by
  calc a = b + 1 := h₁
    _ = 2 * c + 1 := by rw [h₂]

example (a b : ℝ) (hab : a < b) : a < (a + b) / 2 := by
  linarith

example (s : Set ℝ) : s ∩ s = s := by
  simp
```

### 2.4.2 Worked proof: the algebra of the empty region is commutative

Axiom 1 assigns to the empty region the algebra $$\mathfrak{U}(\emptyset) = \mathbb{C}\mathbf{1}$$.
In the library this is a \*-isomorphism `U.emptyEquivComplex` from `U.algebra ∅` to `ℂ`, and the
library proves that `U.algebra ∅` is commutative (`LocalNet.mul_comm_algebra_empty`). On paper:
let $$\varphi : \mathfrak{U}(\emptyset) \to \mathbb{C}$$ be the isomorphism. Since $$\varphi$$ is
injective, it suffices to show $$\varphi(ab) = \varphi(ba)$$. Since $$\varphi$$ is multiplicative,
this is $$\varphi(a)\varphi(b) = \varphi(b)\varphi(a)$$, which holds because $$\mathbb{C}$$ is
commutative.

The Lean proof has the same three steps (the library writes the first as
`U.emptyEquivComplex.injective`). Below, the state after each tactic is shown under it.

<div class="goals" markdown="1">

```lean
example (U : LocalNet) (a b : U.algebra ∅) :
    a * b = b * a := by
  apply EquivLike.injective U.emptyEquivComplex
```

<pre class="tactic-state">U : LocalNet
a : U.algebra ∅
b : U.algebra ∅
⊢ U.emptyEquivComplex (a * b) = U.emptyEquivComplex (b * a)</pre>

```lean
  rw [map_mul, map_mul]
```

<pre class="tactic-state">U : LocalNet
a : U.algebra ∅
b : U.algebra ∅
⊢ U.emptyEquivComplex a * U.emptyEquivComplex b = U.emptyEquivComplex b * U.emptyEquivComplex a</pre>

```lean
  exact mul_comm _ _
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `apply EquivLike.injective U.emptyEquivComplex`: injectivity says that `φ x = φ y` implies
  `x = y`, so applying it leaves the goal `φ (a * b) = φ (b * a)`, with `φ` written out as
  `U.emptyEquivComplex`.
* `rw [map_mul, map_mul]`: Mathlib's lemma `map_mul` states `f (x * y) = f x * f y` for any
  multiplicative map `f`. The first rewrite applies it on the left, the second on the right.
* `exact mul_comm _ _`: the goal is now the commutativity of multiplication in `ℂ`, Mathlib's
  `mul_comm`. Its two arguments are written `_`, which asks Lean to find them from the goal.

### 2.4.3 Worked proof: enlarging a causal diamond

The second exercise of chapter 1 enlarged a diamond by moving its vertices outwards. For the
library's causal diamonds $$J^+(p) \cap J^-(q)$$ (chapter 1 explains why the net does not use them),
the statement reads: if $$p' \prec p$$ and $$q \prec q'$$, then
$$J^+(p) \cap J^-(q) \subseteq J^+(p') \cap J^-(q')$$. On paper: let $$x$$ be a point of the first
diamond, so $$p \prec x$$ and $$x \prec q$$. By transitivity, $$p' \prec x$$ and $$x \prec q'$$, so
$$x$$ lies in the second.

The library states this for any spacetime as `causalDiamond_subset_of`. Here is its proof:

<div class="goals" markdown="1">

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p p' q q' : M.Carrier}
    (hp : p' ≺[M, t] p) (hq : q ≺[M, t] q') :
    causalDiamond M t p q ⊆ causalDiamond M t p' q' := by
  intro x hx
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
p&#x27; : M.Carrier
q : M.Carrier
q&#x27; : M.Carrier
hp : p&#x27; ≺[M, t] p
hq : q ≺[M, t] q&#x27;
x : M.Carrier
hx : x ∈ M.causalDiamond t p q
⊢ x ∈ M.causalDiamond t p&#x27; q&#x27;</pre>

```lean
  rw [mem_causalDiamond] at hx ⊢
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
p&#x27; : M.Carrier
q : M.Carrier
q&#x27; : M.Carrier
hp : p&#x27; ≺[M, t] p
hq : q ≺[M, t] q&#x27;
x : M.Carrier
hx : (p ≺[M, t] x) ∧ x ≺[M, t] q
⊢ (p&#x27; ≺[M, t] x) ∧ x ≺[M, t] q&#x27;</pre>

```lean
  rcases hx with ⟨hpx, hxq⟩
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
p&#x27; : M.Carrier
q : M.Carrier
q&#x27; : M.Carrier
hp : p&#x27; ≺[M, t] p
hq : q ≺[M, t] q&#x27;
x : M.Carrier
hpx : p ≺[M, t] x
hxq : x ≺[M, t] q
⊢ (p&#x27; ≺[M, t] x) ∧ x ≺[M, t] q&#x27;</pre>

```lean
  exact ⟨M.causallyPrecedes_trans t hp hpx,
    M.causallyPrecedes_trans t hxq hq⟩
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `intro x hx`: for sets, `A ⊆ B` is defined as `∀ x, x ∈ A → x ∈ B`, so `intro` applies. It adds
  the point `x` and the hypothesis `hx : x ∈ causalDiamond M t p q`, and the goal becomes
  `x ∈ causalDiamond M t p' q'`. (Lean displays `causalDiamond M t p q` as
  `M.causalDiamond t p q`, in dot notation; the two are the same term.)
* `rw [mem_causalDiamond] at hx ⊢`: the library's `mem_causalDiamond` says that
  `x ∈ causalDiamond M t p q` is equivalent to `(p ≺[M, t] x) ∧ (x ≺[M, t] q)`. The rewrite is
  done in `hx` and in the goal (written `⊢`).
* `rcases hx with ⟨hpx, hxq⟩`: splits the conjunction into `hpx : p ≺[M, t] x` and
  `hxq : x ≺[M, t] q`.
* `exact ⟨…, …⟩`: the goal is a conjunction, and `⟨…, …⟩` builds it from two proofs, each given
  by transitivity of `≺`, `causallyPrecedes_trans`.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Prove that a nonempty causal diamond has $$p \prec q$$. Recall that `s.Nonempty` means
`∃ x, x ∈ s`. (The library's version is `causallyPrecedes_of_causalDiamond_nonempty`.)

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q : M.Carrier}
    (h : (causalDiamond M t p q).Nonempty) :
    p ≺[M, t] q := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example (M : Spacetime) (t : M.TimeOrientation)
    {p q : M.Carrier}
    (h : (causalDiamond M t p q).Nonempty) :
    p ≺[M, t] q := by
  obtain ⟨x, hx⟩ := h
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
q : M.Carrier
x : M.Carrier
hx : x ∈ M.causalDiamond t p q
⊢ p ≺[M, t] q</pre>

```lean
  rw [mem_causalDiamond] at hx
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
q : M.Carrier
x : M.Carrier
hx : (p ≺[M, t] x) ∧ x ≺[M, t] q
⊢ p ≺[M, t] q</pre>

```lean
  rcases hx with ⟨hpx, hxq⟩
```

<pre class="tactic-state">M : Spacetime
t : M.TimeOrientation
p : M.Carrier
q : M.Carrier
x : M.Carrier
hpx : p ≺[M, t] x
hxq : x ≺[M, t] q
⊢ p ≺[M, t] q</pre>

```lean
  exact M.causallyPrecedes_trans t hpx hxq
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

`obtain` chooses a point `x` of the diamond; the rest is as in the worked proof.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

In a C\*-algebra `A`, prove that $$a^*a$$ is self-adjoint: $$(a^*a)^* = a^*a$$. Lean writes $$a^*$$
as `star a`, and `[CStarAlgebra A]` says that `A` is a C\*-algebra (the square brackets are
explained in [section 5](#lean-in-brief-structures)). Mathlib's lemmas `star_mul : star (x * y) = star y * star x` and
`star_star : star (star x) = x` are what you need.

```lean
example (A : Type) [CStarAlgebra A] (a : A) :
    star (star a * a) = star a * a := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example (A : Type) [CStarAlgebra A] (a : A) :
    star (star a * a) = star a * a := by
  rw [star_mul, star_star]
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

The first rewrite turns the left side into `star a * star (star a)`, the second into
`star a * a`. The two sides are then identical, and `rw` closes such a goal by itself.

</details>

</div>

## 2.5 Structures and type classes {#lean-in-brief-structures}

In algebra, a structure is a set together with some data and some axioms: a
group is a set with a multiplication, a unit and inverses, such that the group laws hold. Lean
represents such a thing as a `structure`: a type whose terms are records of named _fields_. Some
fields are data (a set, an operation, a map) and some are proofs (the axioms). To give a term of a
structure, you give every field; to use one, you read off its fields with dot notation.

### 2.5.1 The net of local algebras

Axiom 1 of chapter 1 assigns to each diamond a unital C\*-algebra, and to the empty diamond
$$\mathbb{C}\mathbf{1}$$. In the library this is the structure `LocalNet`. Here is its
declaration, without the documentation comments of the source:

```lean
structure LocalNet where
  algebra : Set StandardMinkowskiSpacetime.Carrier → Type*
  instCStarAlgebra : ∀ B, CStarAlgebra (algebra B)
  emptyEquivComplex : StarAlgEquiv ℂ (algebra ∅) ℂ
```

The three fields are the three parts of the axiom.

* `algebra` assigns to each region `B` a type `U.algebra B`, the algebra $$\mathfrak{U}(\mathbf{B})$$.
  (`Type*` means a type in some universe; see the aside below.) The family is indexed by all subsets
  of spacetime, for simplicity; only the diamonds (the empty one among them) are used, since the
  other axioms quantify over diamonds only.
* `instCStarAlgebra` gives, for each `B`, a C\*-algebra structure on `U.algebra B`: its addition,
  multiplication, norm, involution and the axioms relating them.
* `emptyEquivComplex` is a \*-isomorphism `U.algebra ∅ ≃⋆ₐ[ℂ] ℂ`: the normalisation
  $$\mathfrak{U}(\emptyset) = \mathbb{C}\mathbf{1}$$.

### 2.5.2 Isotony

Axiom 2 is a structure that takes the net as a parameter: `Isotony U` is the type of isotony data
for the net `U`. Its declaration, without documentation comments, and with the type
`Set StandardMinkowskiSpacetime.Carrier` of the regions written only once:

```lean
structure Isotony (U : LocalNet) where
  map : ∀ ⦃B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier⦄,
    IsAlexandrovBasisSet B₁ → IsAlexandrovBasisSet B₂ →
      B₁ ⊆ B₂ → StarAlgHom ℂ (U.algebra B₁) (U.algebra B₂)
  injective : ∀ ⦃B₁ B₂⦄ (h₁ : IsAlexandrovBasisSet B₁)
    (h₂ : IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂),
    Function.Injective (map h₁ h₂ h)
  map_self : ∀ ⦃B⦄ (h : IsAlexandrovBasisSet B),
    map h h (subset_refl B) = StarAlgHom.id ℂ (U.algebra B)
  map_comp : ∀ ⦃B₁ B₂ B₃⦄ (h₁ : IsAlexandrovBasisSet B₁)
    (h₂ : IsAlexandrovBasisSet B₂)
    (h₃ : IsAlexandrovBasisSet B₃)
    (h₁₂ : B₁ ⊆ B₂) (h₂₃ : B₂ ⊆ B₃),
    (map h₂ h₃ h₂₃).comp (map h₁ h₂ h₁₂) =
      map h₁ h₃ (h₁₂.trans h₂₃)
```

Read against chapter 1, field by field:

* `map` is the family of embeddings $$i_{\mathbf{B}_1\mathbf{B}_2}$$. Given two regions, proofs that
  both are diamonds (`IsAlexandrovBasisSet`, [section 6](#lean-in-brief-predicates)) and a proof of `B₁ ⊆ B₂`, it returns a
  \*-homomorphism `U.algebra B₁ →⋆ₐ[ℂ] U.algebra B₂`. Mathlib's \*-algebra homomorphisms
  preserve the unit, so these are unital. The proofs are arguments: the map exists only for nested
  diamonds.
* `injective` says that each embedding is injective, so the embeddings are \*-monomorphisms.
* `map_self` is the law $$i_{\mathbf{B}\mathbf{B}} = \mathrm{id}$$.
* `map_comp` is the law $$i_{\mathbf{B}_2\mathbf{B}_3} \circ i_{\mathbf{B}_1\mathbf{B}_2} =
  i_{\mathbf{B}_1\mathbf{B}_3}$$; `.comp` is composition, and `h₁₂.trans h₂₃` is the proof of
  `B₁ ⊆ B₃` obtained from the two inclusions.

The braces `⦃B₁ B₂⦄` mark _strict implicit_ arguments: like `{B₁ B₂}`, they are found by Lean, but
only once a later explicit argument, such as the proof `IsAlexandrovBasisSet B₁`, is supplied.

### 2.5.3 Type classes

The fields of `LocalNet` give each `U.algebra B` a C\*-algebra structure, but the proofs above
multiply, take adjoints and use the unit without ever mentioning `instCStarAlgebra`. This is the
work of _type classes_. A type class is a structure that Lean is allowed to find by itself. Mathlib
defines `CStarAlgebra A`, the class of unital complex C\*-algebras, by extending the classes of
normed rings, rings with an involution (`StarRing`), complete spaces, rings satisfying the
C\*-identity (`CStarRing`), normed algebras over `ℂ`, and star modules over `ℂ`
($$(\lambda a)^* = \bar\lambda a^*$$). A term of `CStarAlgebra A` is called an
_instance_.

An argument in square brackets, `[CStarAlgebra A]`, is an _instance argument_. It is not written
when the theorem is used: Lean searches its list of instances for one of the right type. The
library declares the field `instCStarAlgebra` to be an instance, so for every net `U` and region `B`
the search succeeds. `inferInstance` asks for that search explicitly:

```lean
example (U : LocalNet)
    (B : Set StandardMinkowskiSpacetime.Carrier) :
    CStarAlgebra (U.algebra B) :=
  inferInstance
```

Every theorem Mathlib proves for C\*-algebras therefore applies to every local algebra, such as the
C\*-identity $$\Vert a^*a\Vert  = \Vert a\Vert ^2$$ in $$\mathfrak{U}(\mathbf{B})$$, from Mathlib's
`CStarRing.norm_star_mul_self`:

```lean
example (U : LocalNet)
    (B : Set StandardMinkowskiSpacetime.Carrier)
    (a : U.algebra B) :
    ‖star a * a‖ = ‖a‖ * ‖a‖ :=
  CStarRing.norm_star_mul_self
```

### 2.5.4 The Haag–Kastler net

The structure `HaagKastlerNet` bundles the axioms. Without its documentation comments:

```lean
structure HaagKastlerNet where
  U : LocalNet.{u}
  isotony : Isotony U
  localCommutativity : LocalCommutativity U isotony
  lorentzCovariance : LorentzCovariance U isotony
```

A Haag–Kastler net is a local net `U`, isotony data for it, and proofs of local commutativity and
Lorentz covariance for that isotony. The type of each field depends on the earlier ones: this is
the dependent typing of [section 2](#lean-in-brief-types) at work. The quasilocal algebra of Axiom 4 is not a field. As
chapter 1 explains, it is constructed from the net (`HaagKastlerNet.quasilocal`), and the claim
that it contains all observables of interest is kept apart as a physical principle.

### 2.5.5 An aside on universes

`Type` is itself a term, of type `Type 1`, which has type `Type 2`, and so on. These levels,
called _universes_, avoid the paradox of a "type of all types", as set theory avoids a set of all
sets. A declaration can be stated for every universe at once by taking a _universe parameter_,
written `u` or `u_1`; `Type u` is then the universe at level `u`.

`LocalNet` has one: its field `algebra` returns types in `Type u_1`, so the algebras of a net may
live in any universe. A structure with such a field is one level higher:

```lean
#check LocalNet
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastler.LocalNet.{u_1} : Type (u_1 + 1)</pre>

`HaagKastlerNet` writes `LocalNet.{u}` for its field `U`, so that it, too, takes the universe as a
parameter rather than fixing it. In practice the algebras lie in `Type`, which is `Type 0`, and
`HaagKastlerNet.{0}` is the type of such nets. Most of the library can be read without thinking
about universes.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Use `map_self` to show that the embedding of a diamond in itself fixes every element. After
rewriting with `i.map_self hB`, the goal is `(StarAlgHom.id ℂ (U.algebra B)) a = a`, which holds
by definition.

```lean
example (U : LocalNet) (i : Isotony U)
    {B : Set StandardMinkowskiSpacetime.Carrier}
    (hB : IsAlexandrovBasisSet B) (a : U.algebra B) :
    i.map hB hB (subset_refl B) a = a := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example (U : LocalNet) (i : Isotony U)
    {B : Set StandardMinkowskiSpacetime.Carrier}
    (hB : IsAlexandrovBasisSet B) (a : U.algebra B) :
    i.map hB hB (subset_refl B) a = a := by
  rw [i.map_self hB]
```

<pre class="tactic-state">U : LocalNet
i : Isotony U
B : Set StandardMinkowskiSpacetime.Carrier
hB : IsAlexandrovBasisSet B
a : U.algebra B
⊢ (StarAlgHom.id ℂ (U.algebra B)) a = a</pre>

```lean
  rfl
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that every isotony embedding maps the unit to the unit. Mathlib's `map_one f` proves
`f 1 = 1` for any map `f` that preserves the unit.

```lean
example (U : LocalNet) (i : Isotony U)
    {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (h₁ : IsAlexandrovBasisSet B₁)
    (h₂ : IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂) :
    i.map h₁ h₂ h 1 = 1 :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (U : LocalNet) (i : Isotony U)
    {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (h₁ : IsAlexandrovBasisSet B₁)
    (h₂ : IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂) :
    i.map h₁ h₂ h 1 = 1 :=
  map_one _
```

This is why the unit $$\mathbf{1}$$ means the same thing in every region (chapter 1, Axiom 2): it
follows from the type of `map`, with no extra axiom.

</details>

</div>

## 2.6 Definitions that are propositions {#lean-in-brief-predicates}

A `def` gives a name to a term. When the term is a proposition, the definition is a _predicate_:
`def P (x : X) : Prop := …` defines, for each `x`, the statement `P x`. Axiom 3 is of this kind: a
property of a net and its isotony maps, not data. `HaagKastlerNet` has a field holding a proof of
it.

### 2.6.1 Diamonds

The simplest example is the predicate "is a diamond". Its signature, checked against the library:

```lean
def Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet
    (B : Set StandardMinkowskiSpacetime.Carrier) : Prop
```

Its value is membership in `Spacetime.alexandrovBasis`, the basis of the Alexandrov topology,
which is the set of all intersections $$I^+(p) \cap I^-(q)$$. Unfolding both definitions gives the
familiar statement, and `Iff.rfl` confirms that the two agree:

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier) :
    IsAlexandrovBasisSet B ↔
      ∃ p q, B = chronologicalFuture
          StandardMinkowskiSpacetime
          standardMinkowskiTimeOrientation p ∩
        chronologicalPast
          StandardMinkowskiSpacetime
          standardMinkowskiTimeOrientation q :=
  Iff.rfl
```

Nothing requires $$p \ll q$$, so the empty set is a diamond, as in chapter 1.

### 2.6.2 Local commutativity

The signature of Axiom 3 shows that it is a property of a net `U` together with isotony data `i`:

```lean
def Physicslib4.AQFT.HaagKastler.LocalCommutativity
    (U : LocalNet) (i : Isotony U) : Prop
```

The isotony maps are needed because, as chapter 1 explains, elements of
$$\mathfrak{U}(\mathbf{B}_1)$$ and $$\mathfrak{U}(\mathbf{B}_2)$$ can only be multiplied in a common
algebra $$\mathfrak{U}(\mathbf{B})$$. Here is the value of the definition, checked by `Iff.rfl`:

```lean
example (U : LocalNet) (i : Isotony U) :
    LocalCommutativity U i ↔
      ∀ ⦃B₁ B₂ B : Set StandardMinkowskiSpacetime.Carrier⦄
        (hB₁ : IsAlexandrovBasisSet B₁)
        (hB₂ : IsAlexandrovBasisSet B₂)
        (hB : IsAlexandrovBasisSet B),
        IsCompletelySpacelike StandardMinkowskiSpacetime
          standardMinkowskiTimeOrientation B₁ B₂ →
        (h₁ : B₁ ⊆ B) → (h₂ : B₂ ⊆ B) →
        ∀ (a : U.algebra B₁) (b : U.algebra B₂),
          Commute (i.map hB₁ hB h₁ a) (i.map hB₂ hB h₂ b) :=
  Iff.rfl
```

Read it line by line against Axiom 3:

1. for any three regions $$\mathbf{B}_1$$, $$\mathbf{B}_2$$ and $$\mathbf{B}$$,
2. that are diamonds,
3. such that $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ are completely spacelike,
4. and both lie in $$\mathbf{B}$$,
5. for all $$a_1 \in \mathfrak{U}(\mathbf{B}_1)$$ and $$a_2 \in \mathfrak{U}(\mathbf{B}_2)$$,
6. the images $$i_{\mathbf{B}_1\mathbf{B}}(a_1)$$ and $$i_{\mathbf{B}_2\mathbf{B}}(a_2)$$ commute.

Mathlib's `Commute x y` means `x * y = y * x`; a proof `h : Commute x y` gives the equation as
`h.eq`. Some hypotheses are named, like `(h₁ : B₁ ⊆ B) →`, because the last line uses them: the map
`i.map hB₁ hB h₁` needs the proof of the inclusion. A hypothesis is a term like any other, and
the statement may refer to it.

### 2.6.3 States

The library's notion of state, `Physicslib4.GNS.State`, is a structure built on another one. For a
type `A` with `[CStarAlgebra A]`, and without documentation comments:

```lean
structure State extends A →L[ℂ] ℂ where
  isPositive : ∀ a : A, 0 ≤ toContinuousLinearMap (star a * a)
  isNormalized : ‖toContinuousLinearMap‖ = 1
```

`structure State extends A →L[ℂ] ℂ` means that a state has all the fields of a continuous
$$\mathbb{C}$$-linear map $$A \to \mathbb{C}$$ (Mathlib's `A →L[ℂ] ℂ`), available as
`ω.toContinuousLinearMap`, and two more:

* `isPositive`: $$\omega(a^*a) \geq 0$$ for every `a`. The order on `ℂ` is Mathlib's: `0 ≤ z` holds
  when `z` is a nonnegative real number. It is made available by `open scoped ComplexOrder`.
* `isNormalized`: the operator norm of $$\omega$$ is $$1$$.

These are the two conditions of chapter 1. The library also lets you apply a state directly, `ω a`,
in place of `ω.toContinuousLinearMap a`.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Local commutativity states that `i.map hB₁ hB h₁ a` commutes with `i.map hB₂ hB h₂ b`. Derive the
equation in the other order, `i.map hB₂ hB h₂ b * i.map hB₁ hB h₁ a = i.map hB₁ hB h₁ a *
i.map hB₂ hB h₂ b`. Apply the hypothesis `hlc` to all its arguments, then use `.eq` and `.symm`
(which turns `x = y` into `y = x`).

```lean
example (U : LocalNet) (i : Isotony U)
    (hlc : LocalCommutativity U i)
    {B₁ B₂ B : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hB : IsAlexandrovBasisSet B)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (h₁ : B₁ ⊆ B) (h₂ : B₂ ⊆ B)
    (a : U.algebra B₁) (b : U.algebra B₂) :
    i.map hB₂ hB h₂ b * i.map hB₁ hB h₁ a =
      i.map hB₁ hB h₁ a * i.map hB₂ hB h₂ b :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (U : LocalNet) (i : Isotony U)
    (hlc : LocalCommutativity U i)
    {B₁ B₂ B : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hB : IsAlexandrovBasisSet B)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (h₁ : B₁ ⊆ B) (h₂ : B₂ ⊆ B)
    (a : U.algebra B₁) (b : U.algebra B₂) :
    i.map hB₂ hB h₂ b * i.map hB₁ hB h₁ a =
      i.map hB₁ hB h₁ a * i.map hB₂ hB h₂ b :=
  (hlc hB₁ hB₂ hB hs h₁ h₂ a b).eq.symm
```

The arguments `B₁`, `B₂` and `B` are strict implicit, so they are not written: Lean reads them off
`hB₁`, `hB₂` and `hB`. The proof term mirrors a sentence: "by local commutativity applied to these
regions and elements, the products agree; read the equation backwards."

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that a state takes a nonnegative value on every element of the form $$a^*a$$.

```lean
open scoped ComplexOrder in
example (A : Type) [CStarAlgebra A]
    (ω : GNS.State A) (a : A) :
    0 ≤ ω (star a * a) :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
open scoped ComplexOrder in
example (A : Type) [CStarAlgebra A]
    (ω : GNS.State A) (a : A) :
    0 ≤ ω (star a * a) :=
  ω.isPositive a
```

The field `isPositive` is a function that takes `a` and returns the proof. Its statement is about
`ω.toContinuousLinearMap (star a * a)`, and Lean accepts it for `ω (star a * a)` because the two
are equal by definition.

</details>

</div>

## 2.7 Mathlib and finding things {#lean-in-brief-mathlib}

_Mathlib_ is Lean's community library of mathematics, covering much of undergraduate and graduate
mathematics. From it this library takes the real and complex numbers, sets, topologies, normed and
Hilbert spaces, continuous linear maps, manifolds, C\*-algebras (`CStarAlgebra`) and their
\*-homomorphisms (`→⋆ₐ[ℂ]`). It adds what physics needs on top: spacetimes and their causal
structure, the Alexandrov topology, nets of local algebras and the Haag–Kastler axioms. Where
Mathlib lacks a notion, the library defines it: Mathlib has no packaged type of states on a
C\*-algebra, so the library introduces `GNS.State`.

### 2.7.1 Namespaces

Lean's names are hierarchical, like paths in a file system. The full name of the net is
`Physicslib4.AQFT.HaagKastler.LocalNet`: the declaration `LocalNet` in the _namespace_
`Physicslib4.AQFT.HaagKastler`. Source files open a namespace with `namespace … end`, and every
name declared inside receives the prefix. Three mechanisms keep the names short in use.

* `open Physicslib4 Spacetime AQFT.HaagKastler`, as in [section 2](#lean-in-brief-types), makes the names in those
  namespaces available without prefix, until the end of the file or section. `open … in` does the
  same for the next command only, as in the `#print axioms` example of [section 1](#lean-in-brief-checking).
* Dot notation, as in [section 2](#lean-in-brief-types): if `U : LocalNet`, then `U.algebra` means `LocalNet.algebra U`,
  and `i.map_self` means `Isotony.map_self i`. Lean looks the name up in the namespace of the type.
* `open scoped` makes available only the notation and instances of a namespace, such as the order
  on `ℂ` in `open scoped ComplexOrder`.

Mathlib's names follow a convention that this library also uses: a theorem is named after its
statement, the conclusion first and the hypotheses after `_of_`. So `map_mul` says that a map
preserves multiplication, and `causallyPrecedes_of_chronologicallyPrecedes` proves causal
precedence from chronological precedence. With practice you can guess a name before looking it up.

### 2.7.2 Searching

To find a theorem, there are four tools.

* [Loogle](https://loogle.lean-lang.org/) searches Mathlib by the shape of a statement. The query
  `‖star ?a * ?a‖` finds the theorems whose statement contains that expression, among them the
  C\*-identity `CStarRing.norm_star_mul_self`; `?a` stands for any term.
* The tactic `exact?`, used in place of a proof in your editor, searches for a theorem that
  closes the goal and suggests the proof it found.
* The API documentation lists every declaration with its signature and docstring, organised by
  namespace and file: [Mathlib's](https://leanprover-community.github.io/mathlib4_docs/) and
  [this library's](https://physicslib.github.io/physicslib4/docs/).
* The [blueprint](https://physicslib.github.io/physicslib4/blueprint/) states each definition and
  theorem of the project in ordinary mathematics. Each one names the Lean declarations that
  formalise it and links to their API documentation, and the dependency graph shows which are
  formalised. In the other direction, the docstrings in the library give the blueprint label.

Here is the documentation of `Isotony` as the API documentation shows it, with its docstring, the
blueprint label `def:isotony`, and the docstring of each field:

<div class="namedocs" markdown="0">
<p class="namedocs-kind">structure</p>
<pre class="namedocs-signature">Physicslib4.AQFT.HaagKastler.Isotony.{u_1} (U : Physicslib4.AQFT.HaagKastler.LocalNet) : Type u_1</pre>
<div class="namedocs-text">
<p>Axiom 2 (isotony): a chosen unital *-monomorphism 𝔘(B₁) → 𝔘(B₂) for each inclusion of diamonds.</p>
<p>An observable measurable in a diamond B₁ is also measurable in any larger diamond B₂ ⊇ B₁. Since
the local algebras are abstract, this is expressed by a map i(B₁, B₂) : 𝔘(B₁) → 𝔘(B₂), which is a
unital *-homomorphism and injective. The maps are coherent: i(B, B) is the identity, and
i(B₂, B₃) ∘ i(B₁, B₂) = i(B₁, B₃) for B₁ ⊆ B₂ ⊆ B₃. In other words B ↦ 𝔘(B) is a functor on the
diamonds ordered by inclusion.</p>
<p>The family is data, not an existence statement. The identity and composition laws are equations
between the maps themselves, so they can only be stated once the maps are fixed. They are required
rather than derived, since nothing about the spacetime constrains which monomorphism a net chooses.
They make the local algebras a directed system, which is what makes their directed colimit, and so
the quasilocal algebra (<code>exists_quasilocalAlgebra</code>), an algebra.</p>
<p>Implementation note: a unital *-homomorphism is Mathlib's <code>StarAlgHom</code>, which preserves the unit
because it is an algebra homomorphism.</p>
<p>Blueprint: def:isotony</p>
</div>
<p class="namedocs-section">Fields</p>
<pre class="namedocs-field">map : ⦃B₁ B₂ : Set Physicslib4.StandardMinkowskiSpacetime.Carrier⦄ →
  Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₁ →
    Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₂ → B₁ ⊆ B₂ → U.algebra B₁ →⋆ₐ[ℂ] U.algebra B₂</pre>
<p class="namedocs-fielddoc">The embedding i(B₁, B₂) : 𝔘(B₁) → 𝔘(B₂) of a diamond B₁ into a diamond B₂ ⊇ B₁.</p>
<pre class="namedocs-field">injective : ∀ ⦃B₁ B₂ : Set Physicslib4.StandardMinkowskiSpacetime.Carrier⦄
  (h₁ : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₁)
  (h₂ : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂), Function.Injective ⇑(self.map h₁ h₂ h)</pre>
<p class="namedocs-fielddoc">Each embedding is injective.</p>
<pre class="namedocs-field">map_self : ∀ ⦃B : Set Physicslib4.StandardMinkowskiSpacetime.Carrier⦄ (h : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B),
  self.map h h ⋯ = StarAlgHom.id ℂ (U.algebra B)</pre>
<p class="namedocs-fielddoc">The identity law: the embedding of a diamond in itself is the identity.</p>
<pre class="namedocs-field">map_comp : ∀ ⦃B₁ B₂ B₃ : Set Physicslib4.StandardMinkowskiSpacetime.Carrier⦄
  (h₁ : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₁)
  (h₂ : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₂)
  (h₃ : Physicslib4.AQFT.HaagKastler.IsAlexandrovBasisSet B₃) (h₁₂ : B₁ ⊆ B₂) (h₂₃ : B₂ ⊆ B₃),
  (self.map h₂ h₃ h₂₃).comp (self.map h₁ h₂ h₁₂) = self.map h₁ h₃ ⋯</pre>
<p class="namedocs-fielddoc">The composition law: for B₁ ⊆ B₂ ⊆ B₃, the embedding of B₁ in B₃ is the composite of the
embeddings of B₁ in B₂ and of B₂ in B₃.</p>
</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Mathlib proves that the involution of a C\*-algebra preserves the norm, $$\Vert a^*\Vert  = \Vert a\Vert $$
(chapter 1 proves it from the C\*-identity). Find the lemma, for instance with the Loogle query
`‖star ?a‖`, and use it.

```lean
example (A : Type) [CStarAlgebra A] (a : A) :
    ‖star a‖ = ‖a‖ :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (A : Type) [CStarAlgebra A] (a : A) :
    ‖star a‖ = ‖a‖ :=
  norm_star a
```

The lemma is `norm_star`. It holds in any normed group whose involution preserves the norm (the
class `NormedStarGroup`), and Lean finds by type class search that a C\*-algebra is one.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Using the naming convention, say what the library's theorem
`chronologicalFuture_subset_causalFuture` states, and check your answer with `#check`.

<details class="solution" markdown="1">
<summary>Solution</summary>

"The chronological future is a subset of the causal future": $$I^+(p) \subseteq J^+(p)$$.

```lean
#check chronologicalFuture_subset_causalFuture
```

<pre class="lean-output">Physicslib4.Spacetime.chronologicalFuture_subset_causalFuture (M : Spacetime) (t : M.TimeOrientation) (p : M.Carrier) :
  M.chronologicalFuture t p ⊆ M.causalFuture t p</pre>

</details>

</div>

## 2.8 Further reading

* [_Theorem Proving in Lean 4_](https://lean-lang.org/theorem_proving_in_lean4/), by Jeremy
  Avigad, Leonardo de Moura, Soonho Kong and Sebastian Ullrich. The systematic introduction to
  Lean's logic: dependent types, propositions as types, tactics, structures and type classes.
* [_Mathematics in Lean_](https://leanprover-community.github.io/mathematics_in_lean/), by Jeremy
  Avigad and Patrick Massot. Formalising mathematics with Mathlib, by worked examples and
  exercises; the natural next step after this chapter.
* [_Functional Programming in Lean_](https://lean-lang.org/functional_programming_in_lean/), by
  David Thrane Christiansen. Lean as a programming language, for readers who want to understand
  the language itself.
* [_The Lean Language Reference_](https://lean-lang.org/doc/reference/latest/). The precise
  description of the language, its syntax, its elaborator and its tactics.
* [Mathlib's documentation](https://leanprover-community.github.io/mathlib4_docs/), and the
  [Mathlib community pages](https://leanprover-community.github.io/), with installation
  instructions, an overview of the library and the Zulip chat where questions are answered.

# 3. Worked examples {#worked-examples}

[Chapter 1](#aqft-in-brief) gave the physics, and [chapter 2](#lean-in-brief) the Lean
needed to read it. This chapter puts the two together in four examples, each a piece of AQFT worked
through in the library: a net that satisfies every axiom, a state and its GNS representation,
local commutativity in a diamond, and the Lorentz invariance of causal precedence. Each example
follows the same pattern. A short reminder of the physics comes first, then the Lean statement,
read line by line, then a proof or construction with the goal shown after every step, and finally
one or two exercises.

As in chapter 2, every piece of Lean code on this page is checked against the library when the
tutorial is built, and the solutions to the exercises are checked too. Each example also names the
blueprint entry that it formalises, so that you can find the statement in ordinary mathematics.
All code below uses the short names made available by

```lean
open Physicslib4 Spacetime AQFT.HaagKastler
open scoped Pointwise
```

where `Pointwise` supplies the notation `L • B` for the image of a region under a Lorentz
transformation, used in the last example.

## 3.1 The trivial net {#worked-examples-trivial-net}

As you will recall from chapter 1, a theory in the Haag–Kastler framework is a net: a unital
C\*-algebra $$\mathfrak{U}(\mathbf{B})$$ for each diamond, unital \*-monomorphisms
$$i_{\mathbf{B}_1\mathbf{B}_2}$$ for nested diamonds, commutation at spacelike separation, and an
action $$\alpha_L$$ of the Poincaré group. First, can the conditions be met at all? If not, every
theorem about Haag–Kastler nets would hold vacuously.

The simplest candidate assigns the same algebra to every region: $$\mathfrak{U}(\mathbf{B}) =
\mathbb{C}$$ for every $$\mathbf{B}$$. Each axiom then holds for an elementary reason.

* **Axiom 1.** $$\mathbb{C}$$ is a unital C\*-algebra, with complex conjugation as involution and the
  modulus as norm, and $$\mathfrak{U}(\emptyset) = \mathbb{C} = \mathbb{C}\mathbf{1}$$.
* **Axiom 2.** Every embedding $$i_{\mathbf{B}_1\mathbf{B}_2}$$ is the identity of $$\mathbb{C}$$,
  which is injective, and identities compose to identities.
* **Axiom 3.** $$\mathbb{C}$$ is commutative, so any two of its elements commute, spacelike or not.
* **Axiom 4.** The quasilocal algebra is $$\mathbb{C}$$ again, up to isomorphism.
* **Axiom 5.** Every $$\alpha_L$$ is the identity of $$\mathbb{C}$$, which satisfies the group and
  isotony laws trivially.

### 3.1.1 The Lean statement

The library builds this net in stages, following the structures of
[chapter 2, section 5](#lean-in-brief-structures): a `LocalNet`, its `Isotony` data, a theorem
for each of Axioms 3 and 5, and the bundled `HaagKastlerNet`. The local net comes first. Its
source, without the documentation comment:

```lean
noncomputable def trivialLocalNet : LocalNet where
  algebra := fun _ => ℂ
  instCStarAlgebra := fun _ => inferInstance
  emptyEquivComplex := StarAlgEquiv.refl ℂ ℂ
```

Read it line by line against Axiom 1.

* `noncomputable def trivialLocalNet : LocalNet where` defines a term of the structure `LocalNet`
  by giving its fields. `noncomputable` tells Lean not to generate executable code: the real
  numbers, and with them the norm of `ℂ`, are not computable in Lean.
* `algebra := fun _ => ℂ` assigns to every region the type `ℂ`; the underscore marks a variable
  that is not used.
* `instCStarAlgebra := fun _ => inferInstance` gives each `ℂ` its C\*-algebra structure, found by
  type class search ([chapter 2, section 5](#lean-in-brief-structures)).
* `emptyEquivComplex := StarAlgEquiv.refl ℂ ℂ` is the normalisation
  $$\mathfrak{U}(\emptyset) \cong \mathbb{C}$$, here the identity \*-isomorphism of `ℂ`.

Its consequences hold by unfolding it, so `rfl` proves that every region gets `ℂ`:

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier) :
    trivialLocalNet.algebra B = ℂ :=
  rfl
```

The isotony data come next:

```lean
def trivialLocalNetIsotony : Isotony trivialLocalNet where
  map := fun _ _ _ _ _ => StarAlgHom.id ℂ ℂ
  injective := by
    intro B₁ B₂ h₁ h₂ h
    change Function.Injective (StarAlgHom.id ℂ ℂ)
    simpa using Function.injective_id
  map_self := by
    intro B h
    rfl
  map_comp := by
    intro B₁ B₂ B₃ h₁ h₂ h₃ h₁₂ h₂₃
    rfl
```

The field `map` takes five arguments, the two regions, the two proofs that they are diamonds and
the proof of `B₁ ⊆ B₂`, and ignores them all: every embedding is `StarAlgHom.id ℂ ℂ`. The three
laws are statements about the identity, proved by `simpa` with `Function.injective_id` and by
`rfl`. Lean confirms that each embedding fixes
every element:

```lean
example {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (h₁ : IsAlexandrovBasisSet B₁)
    (h₂ : IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂) (a : ℂ) :
    trivialLocalNetIsotony.map h₁ h₂ h a = a :=
  rfl
```

### 3.1.2 Worked proof: local commutativity

Axiom 3 for the trivial net is the theorem `trivialLocalNet_localCommutativity`. On paper: let
$$\mathbf{B}_1, \mathbf{B}_2 \subseteq \mathbf{B}$$ be diamonds and $$a, b \in \mathbb{C}$$. The
embeddings are identities, so the claim is $$ab = ba$$, which holds in $$\mathbb{C}$$. The spacelike
hypothesis is never used. Here is the proof in Lean, with the goal after each step:

<div class="goals" markdown="1">

```lean
example : LocalCommutativity trivialLocalNet
    trivialLocalNetIsotony := by
  intro B₁ B₂ B hB₁ hB₂ hB hs h₁ h₂ a b
```

<pre class="tactic-state">B₁ : Set StandardMinkowskiSpacetime.Carrier
B₂ : Set StandardMinkowskiSpacetime.Carrier
B : Set StandardMinkowskiSpacetime.Carrier
hB₁ : IsAlexandrovBasisSet B₁
hB₂ : IsAlexandrovBasisSet B₂
hB : IsAlexandrovBasisSet B
hs : StandardMinkowskiSpacetime.IsCompletelySpacelike standardMinkowskiTimeOrientation B₁ B₂
h₁ : B₁ ⊆ B
h₂ : B₂ ⊆ B
a : trivialLocalNet.algebra B₁
b : trivialLocalNet.algebra B₂
⊢ Commute ((trivialLocalNetIsotony.map hB₁ hB h₁) a) ((trivialLocalNetIsotony.map hB₂ hB h₂) b)</pre>

```lean
  exact mul_comm (G := ℂ) a b
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `intro B₁ B₂ B hB₁ hB₂ hB hs h₁ h₂ a b`: `LocalCommutativity` is a definition whose value is a
  chain of `∀` and `→` ([chapter 2, section 6](#lean-in-brief-predicates)), and `intro` sees
  through it. It introduces the three regions, the three proofs that they are diamonds, the
  spacelike hypothesis `hs`, the two inclusions and the two elements. The goal is the commutation of
  the two images in `trivialLocalNet.algebra B`.
* `exact mul_comm (G := ℂ) a b`: Mathlib's `mul_comm a b : a * b = b * a` holds in any commutative
  multiplication. `Commute x y` is by definition `x * y = y * x`, each `map … a` unfolds to `a`, and
  `trivialLocalNet.algebra B` unfolds to `ℂ`, so the goal is `mul_comm` in `ℂ`, up to definitions.
  The named argument `(G := ℂ)` tells Lean which type to use. Without it, Lean takes the type from
  `a`, which is `trivialLocalNet.algebra B`, and looks for a commutative multiplication on it. Type
  class search unfolds only definitions marked reducible, and `trivialLocalNet` is an ordinary
  `def`, so the search sees only the C\*-algebra instance supplied by the field `instCStarAlgebra`,
  which does not include commutativity. With `G := ℂ`, Lean instead checks, unfolding definitions,
  that `a` and `b` have type `ℂ` and that the two multiplications agree.

The library's proof is the same, written `exact @mul_comm ℂ _ _ _`.

### 3.1.3 Covariance, and the bundled net

Axiom 5 is the theorem `trivialLocalNet_lorentzCovariance`. Its proof supplies the identity
\*-isomorphism `StarAlgEquiv.refl ℂ ℂ` for every Lorentz transformation and every region, and checks
the three laws of `LorentzCovariance` by `rfl`.
The four pieces are then bundled:

```lean
noncomputable def trivialHaagKastlerNet : HaagKastlerNet where
  U := trivialLocalNet
  isotony := trivialLocalNetIsotony
  localCommutativity := trivialLocalNet_localCommutativity
  lorentzCovariance := trivialLocalNet_lorentzCovariance
```

The existence of this term is the theorem that the axioms are consistent:

```lean
#check nonempty_haagKastlerNet
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastler.nonempty_haagKastlerNet : Nonempty HaagKastlerNet</pre>

`Nonempty T` says that the type `T` has at least one term; the proof is `⟨trivialHaagKastlerNet⟩`.
The algebras of the trivial net lie in `Type`, so the theorem is stated for `HaagKastlerNet.{0}`
(Lean's display omits the universe; see the universe aside of
[chapter 2, section 5](#lean-in-brief-structures)).

The axioms can be satisfied, so theorems about `HaagKastlerNet` are not vacuous. But satisfying
them says nothing about physics. The
trivial net has a single observable up to scale, the unit, and every state assigns it the value
$$1$$. A model of physical interest needs non-commutative local algebras, such as the algebras
generated by the Weyl operators of chapter 1's first exercise, and constructing such a net in Lean
is a much larger task. The trivial net has no blueprint entry of its own; it is the library's
witness that `def:haag-kastler-net` is consistent.

### 3.1.4 An aside: the trivial net in curved spacetime

The curved-spacetime axioms of chapter 1 have their own trivial net,
`AQFT.HaagKastlerCurved.trivialHaagKastlerNet`:

```lean
#check AQFT.HaagKastlerCurved.trivialHaagKastlerNet
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastlerCurved.trivialHaagKastlerNet.{u} (M : AQFT.HaagKastlerCurved.LorentzianSpacetime) :
  AQFT.HaagKastlerCurved.HaagKastlerNet M</pre>

It takes as argument an interface, `HaagKastlerCurved.LorentzianSpacetime`, recording only what
the axioms use: points, diamonds, complete spacelike separation, and a group, standing for the
isometries connected to the identity, acting on the points. The net again assigns `ℂ` to every
region, and its proofs repeat those above. Two fields differ: `localAlgebra` (the curved Axiom 4,
which holds for every net by `HaagKastlerCurved.localAlgebra_of`) and `isometricCovariance`. A
one-point spacetime, `HaagKastlerCurved.trivialSpacetime`, gives the curved axioms a model.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that every local algebra of the trivial net is commutative. As in the worked proof, name the
type in which `mul_comm` is to be used.

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier)
    (a b : trivialHaagKastlerNet.algebra B) :
    a * b = b * a :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier)
    (a b : trivialHaagKastlerNet.algebra B) :
    a * b = b * a :=
  mul_comm (G := ℂ) a b
```

For a general net the library proves this only for the empty region
(`HaagKastlerNet.mul_comm_algebra_empty`, the worked proof of chapter 2).

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Every net has a one-dimensional algebra on the empty region (`HaagKastlerNet.finrank_algebra_empty`).
Show that in the trivial net every region has one. Mathlib's `Module.finrank_self ℂ` states
`Module.finrank ℂ ℂ = 1`.

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier) :
    Module.finrank ℂ
      (trivialHaagKastlerNet.algebra B) = 1 :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (B : Set StandardMinkowskiSpacetime.Carrier) :
    Module.finrank ℂ
      (trivialHaagKastlerNet.algebra B) = 1 :=
  Module.finrank_self ℂ
```

The algebra unfolds to `ℂ`, so the statement is `Module.finrank_self ℂ` up to definitions.

</details>

</div>

## 3.2 A state and its GNS representation {#worked-examples-gns}

Recall from chapter 1 that a state on a unital C\*-algebra $$\mathfrak{A}$$ is a linear functional
$$\omega$$ with $$\omega(a^*a) \geq 0$$ and $$\Vert \omega\Vert  = 1$$, and that the GNS construction turns it
into a Hilbert space $$\mathcal{H}_\omega$$, a representation $$\pi_\omega$$ and a cyclic unit vector
$$\Omega_\omega$$ with

$$
\omega(a) = \langle \Omega_\omega, \pi_\omega(a)\,\Omega_\omega \rangle \qquad\text{for all } a \in \mathfrak{A}.
$$

The smallest example is $$\mathfrak{A} = \mathbb{C}$$. A linear functional on $$\mathbb{C}$$ is
multiplication by the number $$\omega(1)$$. Positivity gives
$$\omega(1) = \omega(\bar 1 \cdot 1) \geq 0$$ and normalisation gives $$\vert \omega(1)\vert  = 1$$, so
$$\omega(1) = 1$$. So $$\mathbb{C}$$ has exactly one state, the identity $$\omega(z) = z$$. It is positive, since
$$\omega(\bar z z) = \vert z\vert ^2 \geq 0$$, and faithful, since $$\vert z\vert ^2 > 0$$ for $$z \neq 0$$. Its GNS space
is $$\mathbb{C}$$ itself: the null space $$\mathcal{N}$$ is $$\{0\}$$, the inner product is
$$\langle w, z \rangle = \bar w z$$, $$\pi(z)$$ is multiplication by $$z$$, and $$\Omega = 1$$. The
example is transparent enough that every step of the Lean version can be compared with this
calculation.

The library's notion of state is the structure `GNS.State` of
[chapter 2, section 6](#lean-in-brief-predicates), and its blueprint entry is `def:state`. The
code below needs the order on `ℂ`, for positivity, and the notation `⟪x, y⟫_ℂ` for the inner
product:

```lean
open scoped ComplexOrder InnerProductSpace
```

### 3.2.1 The Lean statement

The GNS theorem is `GNS.gns_construction`, the existence half of the blueprint's
`thrm:gns-construction-theorem`. Here is its statement, restated for an algebra in `Type` and
checked against the library by using the theorem as the proof:

```lean
example {A : Type} [CStarAlgebra A] (ω : GNS.State A) :
    ∃ (H : Type) (_ : NormedAddCommGroup H)
      (_ : InnerProductSpace ℂ H) (_ : CompleteSpace H)
      (π : A →⋆ₐ[ℂ] (H →L[ℂ] H)) (Ω : H),
        GNS.IsCyclicVector π Ω ∧
        (∀ a : A, ω a = ⟪Ω, π a Ω⟫_ℂ) ∧
        (ω.IsFaithful → Function.Injective π) :=
  GNS.gns_construction ω
```

Read it line by line.

1. For a C\*-algebra `A` and a state `ω` on it,
2. there are a type `H` and a norm on it,
3. making it a complex inner product space that is complete, that is, a Hilbert space;
4. a \*-homomorphism `π` from `A` to the bounded operators `H →L[ℂ] H`, which is a representation,
   and a vector `Ω`;
5. such that `Ω` is cyclic for `π`,
6. the reproducing formula holds,
7. and `π` is injective if `ω` is faithful.

Lines 2 and 3 quantify over structures. A Hilbert space is a type together with instances, and the
instances are data, so "there is a Hilbert space" becomes "there are a type and three instances".
The instances are written `(_ : …)`, without names, because Lean finds them by type class search
once they are in context. The library states the theorem for `A` in any universe `Type u`, with `H`
in the same universe. Uniqueness up to unitary equivalence is the separate theorem
`GNS.gns_unique`.

### 3.2.2 Worked construction: the identity state

A state is a structure, so a state is defined by giving its fields
([chapter 2, section 5](#lean-in-brief-structures)). The functional is Mathlib's identity map
`ContinuousLinearMap.id ℂ ℂ`, and the two proofs are short:

<div class="goals" markdown="1">

```lean
noncomputable def identityState : GNS.State ℂ where
  toContinuousLinearMap := ContinuousLinearMap.id ℂ ℂ
  isPositive := by
    intro a
```

<pre class="tactic-state">a : ℂ
⊢ 0 ≤ (ContinuousLinearMap.id ℂ ℂ) (star a * a)</pre>

```lean
    exact star_mul_self_nonneg a
```

<pre class="tactic-state">All goals completed! 🐙</pre>

```lean
  isNormalized := ContinuousLinearMap.norm_id
```

</div>

* `toContinuousLinearMap` is the field inherited from `A →L[ℂ] ℂ`
  ([chapter 2, section 6](#lean-in-brief-predicates)): here the identity of `ℂ`.
* `isPositive`: after `intro a` the goal is `0 ≤ (ContinuousLinearMap.id ℂ ℂ) (star a * a)`. The
  identity map unfolds, and Mathlib's `star_mul_self_nonneg a : 0 ≤ star a * a` closes the goal. It
  holds in any star-ordered ring, and `ℂ` with the order of `ComplexOrder` is one. On `ℂ`,
  `star a` is the complex conjugate.
* `isNormalized`: the operator norm of the identity is $$1$$, Mathlib's `ContinuousLinearMap.norm_id`.
  (It assumes the space is nonzero, which Lean confirms for `ℂ` by type class search.) The value
  of a field can be a proof term, as here, as well as a tactic proof.

Lean checks that the state is the identity, by definition:

```lean
example (a : ℂ) : identityState a = a :=
  rfl
```

### 3.2.3 Worked proof: running the GNS construction

The GNS theorem applies to any state, so to `identityState`. It returns an existential, which
`obtain` takes apart ([chapter 2, section 4](#lean-in-brief-tactics)). Here the reproducing
formula is extracted, with `identityState a` replaced by `a`:

<div class="goals" markdown="1">

```lean
example : ∃ (H : Type) (_ : NormedAddCommGroup H)
    (_ : InnerProductSpace ℂ H) (_ : CompleteSpace H)
    (π : ℂ →⋆ₐ[ℂ] (H →L[ℂ] H)) (Ω : H),
      ∀ a : ℂ, a = ⟪Ω, π a Ω⟫_ℂ := by
  obtain ⟨H, _, _, _, π, Ω, _, hrep, _⟩ :=
    GNS.gns_construction identityState
```

<pre class="tactic-state">H : Type
w✝² : NormedAddCommGroup H
w✝¹ : InnerProductSpace ℂ H
w✝ : CompleteSpace H
π : ℂ →⋆ₐ[ℂ] H →L[ℂ] H
Ω : H
left✝ : GNS.IsCyclicVector π Ω
hrep : ∀ (a : ℂ), identityState a = ⟪Ω, (π a) Ω⟫_ℂ
right✝ : identityState.IsFaithful → Function.Injective ⇑π
⊢ ∃ H x x_1, ∃ (x_2 : CompleteSpace H), ∃ π Ω, ∀ (a : ℂ), a = ⟪Ω, (π a) Ω⟫_ℂ</pre>

```lean
  exact ⟨H, _, _, _, π, Ω, hrep⟩
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `obtain ⟨H, _, _, _, π, Ω, _, hrep, _⟩ := GNS.gns_construction identityState`: the pattern
  follows the shape of the statement, a nested existential and then a conjunction of three. It puts
  the type `H`, its three instances, the representation `π` and the vector `Ω` into context, with
  `hrep : ∀ a, identityState a = ⟪Ω, π a Ω⟫_ℂ`. The cyclicity and faithfulness clauses are not
  needed and are discarded with `_`.
* `exact ⟨H, _, _, _, π, Ω, hrep⟩`: builds the existential from these witnesses. The goal asks for
  `a = ⟪Ω, π a Ω⟫_ℂ`, while `hrep` gives `identityState a = ⟪Ω, π a Ω⟫_ℂ`. The two are equal by
  definition, as the `rfl` above shows, so Lean accepts `hrep`.

What the proof does not tell you is what `H` is. The theorem asserts existence, and the proof in the
library builds `H` as Mathlib's `PositiveLinearMap.GNS`: the completion of $$\mathfrak{A}$$ with the
semi-inner product $$\omega(a^*b)$$, in which the null vectors are identified with $$0$$, steps 2 and
3 of chapter 1 at once. To identify it with the
$$\mathbb{C}$$ of the calculation above, one checks that $$\mathbb{C}$$, with $$\pi(z)w = zw$$ and
the vector $$1$$, is also a cyclic representation reproducing $$\omega$$, and applies
`GNS.gns_unique`, which gives a
unitary between the two spaces that intertwines the representations and maps one cyclic vector to
the other.

### 3.2.4 States of a net

For a net, the state of interest lives on the quasilocal algebra. For the trivial net of the
first example, that algebra is $$\mathbb{C}$$ up to isomorphism. Every net has a quasilocal algebra, by the
theorem `exists_quasilocalAlgebra`, and for the trivial net the library also writes one down,
`trivialQuasilocalAlgebra`, with carrier `ℂ`. The identity state is a state on it:

```lean
noncomputable example :
    GNS.State trivialQuasilocalAlgebra.carrier :=
  identityState
```

`trivialQuasilocalAlgebra` is a quasilocal algebra of the trivial net, but not the one
`trivialHaagKastlerNet.quasilocal` chosen by the library, and the predicates below are stated for
the chosen one. For a general net `N`, the quasilocal algebra is `N.quasilocal`, chosen once and
for all from the existence theorem by `Classical.choice`, and the vacuum is a property of a state on its carrier:

```lean
#check HaagKastlerNet.IsVacuumState
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastler.HaagKastlerNet.IsVacuumState.{u} (N : HaagKastlerNet)
  (ftl : (ℝ → InhomogeneousLorentzGroup) → Prop) (ω : GNS.State N.quasilocal.carrier) : Prop</pre>

The predicate `N.IsVacuumState ftl ω` has the two parts of chapter 1: `ω` is invariant under the
covariance action (`N.IsInvariantState ω`), and in some representation reproducing `ω`, with
unitaries implementing the action, the one-parameter groups of future timelike translations, those picked
out by `ftl`, have positive energy. `HaagKastlerNet.IsVacuumStateConcrete` fixes `ftl` to the
translations $$t \mapsto x + tn$$ with $$n$$ future timelike. The library constructs no vacuum state
for a concrete net. For the trivial net one would expect the unique state to be the vacuum, with a
one-dimensional GNS space on which every translation acts as the identity, but proving it means
first building a state on the chosen `N.quasilocal.carrier`, which is isomorphic to `ℂ` but not
literally `ℂ`. One route: show that every element is a scalar multiple of the unit, which gives a
unital \*-homomorphism to `ℂ`, and pull `identityState` back along it with the library's
`GNS.State.comp`. This is a natural project for chapter 4.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that `identityState` is faithful. Mathlib's `star_mul_self_pos_iff : 0 < star a * a ↔ a ≠ 0`
holds in `ℂ`. What does the third clause of the GNS theorem then give?

```lean
example : identityState.IsFaithful := by
  intro a ha
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example : identityState.IsFaithful := by
  intro a ha
```

<pre class="tactic-state">a : ℂ
ha : a ≠ 0
⊢ 0 &lt; identityState (star a * a)</pre>

```lean
  exact star_mul_self_pos_iff.mpr ha
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

After `intro a ha`, with `ha : a ≠ 0`, the goal is `0 < identityState (star a * a)`, which unfolds
to `0 < star a * a`. The GNS representation of `identityState` is therefore injective: no nonzero
element of `ℂ` acts as the zero operator, as for multiplication by $$z$$ on $$\mathbb{C}$$.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Let $$\Omega$$ be a unit vector in $$\mathbb{C}^n$$. Show that $$\omega(a) = \langle \Omega,
a\Omega \rangle$$ is a state on the algebra of bounded operators on $$\mathbb{C}^n$$. In Lean,
$$\mathbb{C}^n$$ is `EuclideanSpace ℂ (Fin n)`, abbreviated below as `Cn n`, and Mathlib makes
`Cn n →L[ℂ] Cn n` a C\*-algebra. The functional is built from two of Mathlib's continuous linear
maps, evaluation at `Ω` followed by the inner product with `Ω`:

```lean
abbrev Cn (n : ℕ) := EuclideanSpace ℂ (Fin n)

noncomputable def vectorFun {n : ℕ} (Ω : Cn n) :
    (Cn n →L[ℂ] Cn n) →L[ℂ] ℂ :=
  (innerSL ℂ Ω).comp
    (ContinuousLinearMap.apply ℂ (Cn n) Ω)

example {n : ℕ} (Ω : Cn n) (a : Cn n →L[ℂ] Cn n) :
    vectorFun Ω a = ⟪Ω, a Ω⟫_ℂ :=
  rfl
```

Prove positivity and normalisation.

```lean
example {n : ℕ} (Ω : Cn n) (a : Cn n →L[ℂ] Cn n) :
    0 ≤ vectorFun Ω (star a * a) := by
  sorry

example {n : ℕ} (Ω : Cn n) (hΩ : ‖Ω‖ = 1) :
    ‖vectorFun Ω‖ = 1 := by
  sorry
```

For positivity, rewrite $$\langle \Omega, a^*a\Omega \rangle$$ as $$\langle a\Omega, a\Omega \rangle$$
with `mul_apply_eq_comp`, `ContinuousLinearMap.star_eq_adjoint` and
`ContinuousLinearMap.adjoint_inner_right`, then use `inner_self_eq_norm_sq_to_K` and `positivity`.
For normalisation, prove $$\Vert \omega\Vert  \le 1$$ with `ContinuousLinearMap.opNorm_le_bound`, the
Cauchy–Schwarz inequality `norm_inner_le_norm` and `ContinuousLinearMap.le_opNorm`, and
$$\Vert \omega\Vert  \ge 1$$ from $$\omega(\mathbf{1}) = 1$$. The unit operator has norm $$1$$ only on a
nonzero space: first give Lean an instance `Nontrivial (Cn n)`, using $$\Omega \neq 0$$.

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
theorem vectorFun_nonneg {n : ℕ} (Ω : Cn n)
    (a : Cn n →L[ℂ] Cn n) :
    0 ≤ vectorFun Ω (star a * a) := by
  change 0 ≤ ⟪Ω, (star a * a) Ω⟫_ℂ
```

<pre class="tactic-state">n : ℕ
Ω : Cn n
a : Cn n →L[ℂ] Cn n
⊢ 0 ≤ ⟪Ω, (star a * a) Ω⟫_ℂ</pre>

```lean
  rw [mul_apply_eq_comp,
    ContinuousLinearMap.star_eq_adjoint,
    ContinuousLinearMap.adjoint_inner_right,
    inner_self_eq_norm_sq_to_K]
```

<pre class="tactic-state">n : ℕ
Ω : Cn n
a : Cn n →L[ℂ] Cn n
⊢ 0 ≤ ↑‖a Ω‖ ^ 2</pre>

```lean
  positivity
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

`change` unfolds `vectorFun`. The rewrites turn $$\langle \Omega, a^*(a\Omega) \rangle$$ into
$$\langle a\Omega, a\Omega \rangle$$ and then into $$\Vert a\Omega\Vert ^2$$, a nonnegative real number, which
`positivity` recognises.

```lean
theorem norm_vectorFun {n : ℕ} (Ω : Cn n)
    (hΩ : ‖Ω‖ = 1) : ‖vectorFun Ω‖ = 1 := by
  apply le_antisymm
  · apply ContinuousLinearMap.opNorm_le_bound _
      zero_le_one
    intro a
    calc ‖vectorFun Ω a‖ = ‖⟪Ω, a Ω⟫_ℂ‖ := rfl
      _ ≤ ‖Ω‖ * ‖a Ω‖ := norm_inner_le_norm _ _
      _ ≤ ‖Ω‖ * (‖a‖ * ‖Ω‖) := by
        gcongr
        exact a.le_opNorm Ω
      _ = 1 * ‖a‖ := by rw [hΩ]; ring
  · have : Nontrivial (Cn n) :=
      ⟨⟨Ω, 0, by intro h; simp [h] at hΩ⟩⟩
    have h1 : vectorFun Ω 1 = 1 := by
      change ⟪Ω, Ω⟫_ℂ = 1
      rw [inner_self_eq_norm_sq_to_K, hΩ]
      simp
    calc (1 : ℝ) = ‖vectorFun Ω 1‖ := by
          rw [h1, norm_one]
      _ ≤ ‖vectorFun Ω‖ * ‖(1 : Cn n →L[ℂ] Cn n)‖ :=
          (vectorFun Ω).le_opNorm 1
      _ = ‖vectorFun Ω‖ := by rw [norm_one, mul_one]

noncomputable def vectorState {n : ℕ} (Ω : Cn n)
    (hΩ : ‖Ω‖ = 1) : GNS.State (Cn n →L[ℂ] Cn n) :=
  ⟨vectorFun Ω, vectorFun_nonneg Ω, norm_vectorFun Ω hΩ⟩
```

The bound $$\Vert \omega\Vert  \le 1$$ is the chain
$$\vert \langle \Omega, a\Omega \rangle\vert  \le \Vert \Omega\Vert \,\Vert a\Omega\Vert  \le \Vert a\Vert $$. For the reverse, the
unit operator has norm $$1$$ once the space is nonzero (the `Nontrivial` instance, which holds
because $$\Omega \neq 0$$), and $$1 = \vert \omega(\mathbf{1})\vert  \le \Vert \omega\Vert \,\Vert \mathbf{1}\Vert $$. The last
line assembles the state. Its GNS representation is the defining one on $$\mathbb{C}^n$$, up to
unitary equivalence, since every vector of $$\mathbb{C}^n$$ is $$a\Omega$$ for some $$a$$, as in the
$$M_2(\mathbb{C})$$ exercise of chapter 1.

</details>

</div>

## 3.3 Local commutativity in a diamond {#worked-examples-locality}

You will remember Axiom 3 from chapter 1: if the diamonds $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ are
completely spacelike, their observables commute in the algebra of every diamond $$\mathbf{B}$$
containing both, and therefore also in the quasilocal algebra $$\mathfrak{U}$$. The second form is
the one used in practice, since $$\mathfrak{U}$$ holds the observables of all regions at once. This
example derives it from the first.

<figure class="tutorial-figure">
<svg aria-labelledby="st-diagram-title st-diagram-desc" class="st-diagram" role="img" viewbox="0 0 400 420" xmlns="http://www.w3.org/2000/svg"><title id="st-diagram-title">Two spacelike-separated diamonds inside a causal diamond</title><desc id="st-diagram-desc">A large causal diamond B contains two smaller diamonds B1 and B2 side by side. Dashed light-cone lines at 45 degrees from B1 bound its causal future and past; B2 lies outside them, so B1 and B2 are spacelike separated.</desc><defs><marker id="st-arrow" markerheight="7" markerwidth="7" orient="auto-start-reverse" refx="9" refy="5" viewbox="0 0 10 10"><path class="st-arrowhead" d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><polygon class="st-big" points="200,30 370,200 200,370 30,200"></polygon><line class="st-cone" x1="130" x2="272.5" y1="245" y2="102.5"></line><line class="st-cone" x1="130" x2="57.5" y1="245" y2="172.5"></line><line class="st-cone" x1="130" x2="272.5" y1="155" y2="297.5"></line><line class="st-cone" x1="130" x2="57.5" y1="155" y2="227.5"></line><polygon class="st-small" points="130,155 175,200 130,245 85,200"></polygon><polygon class="st-small" points="270,155 315,200 270,245 225,200"></polygon><text class="st-label" text-anchor="middle" x="200" y="70">B</text><text class="st-label st-label-small" text-anchor="middle" x="130" y="207">B₁</text><text class="st-label st-label-small" text-anchor="middle" x="270" y="207">B₂</text><line class="st-axis" marker-end="url(#st-arrow)" x1="20" x2="20" y1="405" y2="345"></line><line class="st-axis" marker-end="url(#st-arrow)" x1="20" x2="80" y1="405" y2="405"></line><text class="st-axis-label" x="28" y="352">t</text><text class="st-axis-label" x="76" y="398">x</text></svg>
<figcaption markdown="span">Two completely spacelike diamonds $$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ inside a diamond
$$\mathbf{B}$$.</figcaption>
</figure>

The argument uses one property of the embeddings $$\iota_{\mathbf{B}} : \mathfrak{U}(\mathbf{B})
\to \mathfrak{U}$$: they are compatible with isotony,
$$\iota_{\mathbf{B}} \circ i_{\mathbf{B}_1\mathbf{B}} = \iota_{\mathbf{B}_1}$$. Let
$$a \in \mathfrak{U}(\mathbf{B}_1)$$ and $$b \in \mathfrak{U}(\mathbf{B}_2)$$, and write
$$a' = i_{\mathbf{B}_1\mathbf{B}}(a)$$ and $$b' = i_{\mathbf{B}_2\mathbf{B}}(b)$$. Then

$$
\iota_{\mathbf{B}_1}(a)\,\iota_{\mathbf{B}_2}(b) = \iota_{\mathbf{B}}(a')\,\iota_{\mathbf{B}}(b') = \iota_{\mathbf{B}}(a'b') = \iota_{\mathbf{B}}(b'a') = \iota_{\mathbf{B}_2}(b)\,\iota_{\mathbf{B}_1}(a),
$$

using compatibility, that $$\iota_{\mathbf{B}}$$ is multiplicative, and Axiom 3 in
$$\mathfrak{U}(\mathbf{B})$$. In the library, Axiom 3 is `LocalCommutativity` (blueprint
`def:local-commutativity`), and the statement in $$\mathfrak{U}$$ is
`LocalCommutativity.commute_ι` (`lmm:local-commutativity-any-quasilocal`).

### 3.3.1 The Lean statement

For a Haag–Kastler net `N`, the quasilocal algebra is `N.quasilocal`, a structure
`QuasilocalAlgebra` whose fields include the carrier `N.quasilocal.carrier`, the embeddings
`N.quasilocal.ι hB`, one for each proof `hB` that `B` is a diamond, and the compatibility law
`N.quasilocal.ι_inclusion`. The law reads:

```lean
#check QuasilocalAlgebra.ι_inclusion
```

<pre class="lean-output">Physicslib4.AQFT.HaagKastler.QuasilocalAlgebra.ι_inclusion.{u} {U : LocalNet} {i : Isotony U}
  (self : QuasilocalAlgebra U i) ⦃B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier⦄ (hB₁ : IsAlexandrovBasisSet B₁)
  (hB₂ : IsAlexandrovBasisSet B₂) (h : B₁ ⊆ B₂) (a : U.algebra B₁) : (self.ι hB₂) ((i.map hB₁ hB₂ h) a) = (self.ι hB₁) a</pre>

It is the equation $$\iota_{\mathbf{B}_2}(i_{\mathbf{B}_1\mathbf{B}_2}(a)) = \iota_{\mathbf{B}_1}(a)$$,
for the net `U` with isotony `i`. For a Haag–Kastler net these are `N.U` and `N.isotony`. The
statement of the worked proof below says, in words:

1. for a Haag–Kastler net `N` and diamonds `B₁`, `B₂` and `B`,
2. with `B₁` and `B₂` completely spacelike, both inside `B`,
3. and for elements `a : N.algebra B₁` and `b : N.algebra B₂`,
4. the images `N.quasilocal.ι hB₁ a` and `N.quasilocal.ι hB₂ b` commute.

Here `N.algebra B` abbreviates `N.U.algebra B`, the algebra of `B` in the underlying local net.

### 3.3.2 Worked proof: from the common diamond to the quasilocal algebra

The Lean proof follows the calculation: it records Axiom 3 in the algebra of `B`, rewrites the
goal so that both elements pass through `B`, and maps the commutation into the quasilocal algebra.

<div class="goals" markdown="1">

```lean
example (N : HaagKastlerNet)
    {B₁ B₂ B : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hB : IsAlexandrovBasisSet B)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (h₁ : B₁ ⊆ B) (h₂ : B₂ ⊆ B)
    (a : N.algebra B₁) (b : N.algebra B₂) :
    Commute (N.quasilocal.ι hB₁ a)
      (N.quasilocal.ι hB₂ b) := by
  have hloc := N.localCommutativity hB₁ hB₂ hB hs h₁ h₂ a b
```

<pre class="tactic-state">N : HaagKastlerNet
B₁ : Set StandardMinkowskiSpacetime.Carrier
B₂ : Set StandardMinkowskiSpacetime.Carrier
B : Set StandardMinkowskiSpacetime.Carrier
hB₁ : IsAlexandrovBasisSet B₁
hB₂ : IsAlexandrovBasisSet B₂
hB : IsAlexandrovBasisSet B
hs : StandardMinkowskiSpacetime.IsCompletelySpacelike standardMinkowskiTimeOrientation B₁ B₂
h₁ : B₁ ⊆ B
h₂ : B₂ ⊆ B
a : N.algebra B₁
b : N.algebra B₂
hloc : Commute ((N.isotony.map hB₁ hB h₁) a) ((N.isotony.map hB₂ hB h₂) b)
⊢ Commute ((N.quasilocal.ι hB₁) a) ((N.quasilocal.ι hB₂) b)</pre>

```lean
  rw [← N.quasilocal.ι_inclusion hB₁ hB h₁ a,
    ← N.quasilocal.ι_inclusion hB₂ hB h₂ b]
```

<pre class="tactic-state">N : HaagKastlerNet
B₁ : Set StandardMinkowskiSpacetime.Carrier
B₂ : Set StandardMinkowskiSpacetime.Carrier
B : Set StandardMinkowskiSpacetime.Carrier
hB₁ : IsAlexandrovBasisSet B₁
hB₂ : IsAlexandrovBasisSet B₂
hB : IsAlexandrovBasisSet B
hs : StandardMinkowskiSpacetime.IsCompletelySpacelike standardMinkowskiTimeOrientation B₁ B₂
h₁ : B₁ ⊆ B
h₂ : B₂ ⊆ B
a : N.algebra B₁
b : N.algebra B₂
hloc : Commute ((N.isotony.map hB₁ hB h₁) a) ((N.isotony.map hB₂ hB h₂) b)
⊢ Commute ((N.quasilocal.ι hB) ((N.isotony.map hB₁ hB h₁) a)) ((N.quasilocal.ι hB) ((N.isotony.map hB₂ hB h₂) b))</pre>

```lean
  exact hloc.map (N.quasilocal.ι hB)
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `have hloc := N.localCommutativity hB₁ hB₂ hB hs h₁ h₂ a b`: the field `localCommutativity` of
  the net is a proof of Axiom 3, and applying it to all its arguments gives
  `hloc : Commute (N.isotony.map hB₁ hB h₁ a) (N.isotony.map hB₂ hB h₂ b)`, commutation in
  `N.algebra B`. The tactic `have` adds a new hypothesis, proved by the term after `:=`.
* `rw [← N.quasilocal.ι_inclusion hB₁ hB h₁ a, ← …]`: the arrow `←` rewrites from right to left,
  replacing `N.quasilocal.ι hB₁ a` by `N.quasilocal.ι hB (N.isotony.map hB₁ hB h₁ a)`, and likewise
  for `b`. Both elements now enter $$\mathfrak{U}$$ through the same embedding.
* `exact hloc.map (N.quasilocal.ι hB)`: Mathlib's `Commute.map` says that a multiplicative map
  sends commuting elements to commuting elements. Applied to `hloc` and the embedding of `B`, it is
  the goal.

The library's `LocalCommutativity.commute_ι` has the same proof, but needs no `B`: it obtains one
from `Spacetime.alexandrovBasis_directed`, the fact of chapter 1 that any two diamonds lie in a
common diamond. For a net the result is `HaagKastlerNet.commute_ι_of_spacelike`, whose hypotheses
are the two diamonds, the spacelike condition and the elements. The converse holds as well: by
`localCommutativity_iff_exists_commute_ι` (`lmm:local-commutativity-iff-quasilocal`), a net
satisfies Axiom 3 if and only if spacelike observables commute in some quasilocal algebra.

### 3.3.3 Einstein causality in a representation

The physical content is in Hilbert space: in any representation, spacelike observables are
commuting operators. That is `HaagKastlerNet.einstein_causality` (`thrm:einstein-causality`),
`Commute.map` once more, now along the representation `π`:

```lean
example (N : HaagKastlerNet) {H : Type*}
    [NormedAddCommGroup H] [InnerProductSpace ℂ H]
    [CompleteSpace H]
    (π : N.quasilocal.carrier →⋆ₐ[ℂ] (H →L[ℂ] H))
    {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (a : N.algebra B₁) (b : N.algebra B₂) :
    Commute (π (N.quasilocal.ι hB₁ a))
      (π (N.quasilocal.ι hB₂ b)) :=
  (N.commute_ι_of_spacelike hB₁ hB₂ hs a b).map π
```

Applied to the GNS representation of a state, this is
`HaagKastlerNet.exists_gns_einstein_causality`: for every state on $$\mathfrak{U}$$ there is a GNS
triple, as in the previous example, in which spacelike observables commute as operators on
$$\mathcal{H}_\omega$$.

One remark on the hypothesis. Since `≺` is reflexive, no point is spacelike to itself: the library's
`isSpacelikeRelated_irrefl` states `¬ IsSpacelikeRelated M t p p`. So two regions that share a point
are never completely spacelike, and Axiom 3 says nothing about them. This is as it should be: an
observable localised in a diamond inside the overlap embeds, by isotony, into both algebras, and
nothing makes it commute with the other observables of either.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that two regions with a common point `x` are not completely spacelike. A proof of
`IsCompletelySpacelike M t B₁ B₂` is a function: given a point of `B₁` with a proof of membership,
and a point of `B₂` with one, it returns a proof that they are spacelike related.

```lean
example {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    {x : StandardMinkowskiSpacetime.Carrier}
    (hx₁ : x ∈ B₁) (hx₂ : x ∈ B₂) :
    ¬ IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂ := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    {x : StandardMinkowskiSpacetime.Carrier}
    (hx₁ : x ∈ B₁) (hx₂ : x ∈ B₂) :
    ¬ IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂ := by
  intro hs
```

<pre class="tactic-state">B₁ : Set StandardMinkowskiSpacetime.Carrier
B₂ : Set StandardMinkowskiSpacetime.Carrier
x : StandardMinkowskiSpacetime.Carrier
hx₁ : x ∈ B₁
hx₂ : x ∈ B₂
hs : StandardMinkowskiSpacetime.IsCompletelySpacelike standardMinkowskiTimeOrientation B₁ B₂
⊢ False</pre>

```lean
  exact isSpacelikeRelated_irrefl _ _ x (hs x hx₁ x hx₂)
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

As in chapter 2, `¬ P` is `P → False`, so `intro hs` leaves the goal `False`. Then `hs x hx₁ x hx₂` says that `x` is
spacelike to itself, which `isSpacelikeRelated_irrefl` refutes. Its first two arguments, the
spacetime and the time orientation, are read off the type and written `_`.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Observables of smaller regions inherit the commutation: if `B₁' ⊆ B₁` and `B₂' ⊆ B₂`, and `B₁` and
`B₂` are completely spacelike, the observables of `B₁'` and `B₂'` commute in $$\mathfrak{U}$$. Use
`HaagKastlerNet.commute_ι_of_spacelike` and the library's `isCompletelySpacelike_mono`, which
states that complete spacelike separation survives shrinking either region.

```lean
example (N : HaagKastlerNet)
    {B₁ B₂ B₁' B₂' : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁' : IsAlexandrovBasisSet B₁')
    (hB₂' : IsAlexandrovBasisSet B₂')
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (h₁ : B₁' ⊆ B₁) (h₂ : B₂' ⊆ B₂)
    (a : N.algebra B₁') (b : N.algebra B₂') :
    Commute (N.quasilocal.ι hB₁' a)
      (N.quasilocal.ι hB₂' b) :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (N : HaagKastlerNet)
    {B₁ B₂ B₁' B₂' : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁' : IsAlexandrovBasisSet B₁')
    (hB₂' : IsAlexandrovBasisSet B₂')
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (h₁ : B₁' ⊆ B₁) (h₂ : B₂' ⊆ B₂)
    (a : N.algebra B₁') (b : N.algebra B₂') :
    Commute (N.quasilocal.ι hB₁' a)
      (N.quasilocal.ι hB₂' b) :=
  N.commute_ι_of_spacelike hB₁' hB₂'
    (isCompletelySpacelike_mono _ _ h₁ h₂ hs) a b
```

The regions `B₁` and `B₂` need not be diamonds: only the smaller regions carry algebras here, and
only their separation is used.

</details>

</div>

## 3.4 Lorentz invariance of causal precedence {#worked-examples-covariance}

Chapter 1 described the identity component of the Poincaré group: its elements are the maps
$$x \mapsto \Lambda x + a$$, where $$\Lambda$$ preserves the Minkowski form, has determinant $$1$$
and preserves the direction of time. On vectors, invariance of causal precedence is then immediate: the translation cancels in
$$(\Lambda q + a) - (\Lambda p + a) = \Lambda(q - p)$$, and $$\Lambda$$ maps a causal future-directed
vector to a causal future-directed vector. Axiom 5 rests on this. The covariance maps
$$\alpha_L : \mathfrak{U}(\mathbf{B}) \to \mathfrak{U}(L\mathbf{B})$$ make sense only if $$L$$
maps diamonds to diamonds, and they can respect locality only if $$L$$ maps spacelike pairs to
spacelike pairs.

The library defines $$\prec$$ not by vectors but by curves, as the blueprint does, so that the same
definition works in a curved spacetime. A _causal trip segment_ from $$p$$ to $$q$$ is a
future-oriented causal geodesic with past endpoint $$p$$ and future endpoint $$q$$, and
$$p \prec q$$ means that a chain of zero or more segments leads from $$p$$ to $$q$$. The empty chain
gives $$p \prec p$$. In Lean the one-segment relation is `CausalSegmentPrecedes`, and `≺` is its
reflexive-transitive closure, Mathlib's `Relation.ReflTransGen`; this is why `≺` is reflexive
([chapter 2, section 3](#lean-in-brief-propositions)). The proof of invariance therefore has
two layers: a Lorentz transformation maps each segment to a segment, and so it maps chains to
chains. This is the blueprint's `thrm:causal-precedence-lorentz-invariant`.

### 3.4.1 The Lean statement

An element of the group is a structure with five fields. Without the documentation comments:

```lean
structure InhomogeneousLorentzGroup where
  linear : StandardMinkowskiSpacetime.Carrier ≃ₗ[ℝ]
    StandardMinkowskiSpacetime.Carrier
  translation : StandardMinkowskiSpacetime.Carrier
  isLorentz : IsLorentz linear
  isProper : IsProper linear
  isOrthochronous : IsOrthochronous linear
```

The field `linear` is $$\Lambda$$, an invertible real-linear map (`≃ₗ[ℝ]`), and `translation` is
$$a$$. The three proofs say that $$\Lambda$$ preserves the Minkowski form, has determinant $$1$$ and
preserves the direction of time: together, that $$(\Lambda, a)$$ lies in the identity component. The
group acts on points, written `g • x`, by the affine map, as Lean confirms by `rfl`:

```lean
example (g : InhomogeneousLorentzGroup)
    (x : StandardMinkowskiSpacetime.Carrier) :
    g • x = g.linear x + g.translation :=
  rfl
```

The theorem `causallyPrecedes_smul_iff` reads:

```lean
example (g : InhomogeneousLorentzGroup)
    (p q : StandardMinkowskiSpacetime.Carrier) :
    (g • p ≺[StandardMinkowskiSpacetime,
        standardMinkowskiTimeOrientation] g • q) ↔
      (p ≺[StandardMinkowskiSpacetime,
        standardMinkowskiTimeOrientation] q) :=
  causallyPrecedes_smul_iff g p q
```

For every group element `g` and points `p` and `q`, the image of `p` causally precedes the image of
`q` exactly when `p` causally precedes `q`, with the standard time orientation throughout.

The segment layer is done by `lorentzPath g μ`, the image of a smooth path `μ` under `g`, the path
$$s \mapsto \Lambda\mu(s) + a$$. Its tangent at each parameter is $$\Lambda$$ applied to the tangent
of `μ` (`lorentzPath_mfderivWithin`), since the translation is constant. Five lemmas then transport
the five conditions of a causal trip segment: `lorentzPath_isCausal`,
`lorentzPath_isFutureOriented` and `lorentzPath_isGeodesic` for the curve, and
`lorentzPath_isPastEndpoint` and `lorentzPath_isFutureEndpoint` for its endpoints, which become
`g • p` and `g • q`. Together they give

```lean
#check causalSegmentPrecedes_smul
```

<pre class="lean-output">Physicslib4.causalSegmentPrecedes_smul (g : InhomogeneousLorentzGroup) {p q : StandardMinkowskiSpacetime.Carrier}
  (h : StandardMinkowskiSpacetime.CausalSegmentPrecedes standardMinkowskiTimeOrientation p q) :
  StandardMinkowskiSpacetime.CausalSegmentPrecedes standardMinkowskiTimeOrientation (g • p) (g • q)</pre>

### 3.4.2 Worked proof: from segments to causal precedence

The step from segments to chains is a case distinction. By
`causallyPrecedes_iff_eq_or_isCausalTrip` ([chapter 2,
section 3](#lean-in-brief-propositions)), either `p = q`, and then `g • p ≺ g • p` by reflexivity, or there is a causal trip, a
chain of one or more segments, and then `g` maps it segment by segment:

<div class="goals" markdown="1">

```lean
example (g : InhomogeneousLorentzGroup)
    {p q : StandardMinkowskiSpacetime.Carrier}
    (h : p ≺[StandardMinkowskiSpacetime,
      standardMinkowskiTimeOrientation] q) :
    g • p ≺[StandardMinkowskiSpacetime,
      standardMinkowskiTimeOrientation] g • q := by
  rcases (causallyPrecedes_iff_eq_or_isCausalTrip _ _).mp h
    with rfl | htrip
```

<pre class="tactic-state">case inl
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
h : p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] p
⊢ g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • p

case inr
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
h : p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q
htrip : StandardMinkowskiSpacetime.IsCausalTrip standardMinkowskiTimeOrientation p q
⊢ g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • q</pre>

```lean
  · exact causallyPrecedes_refl _ _ _
```

<pre class="tactic-state">All goals completed! 🐙</pre>

```lean
  · apply causallyPrecedes_of_isCausalTrip
```

<pre class="tactic-state">case inr
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
h : p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q
htrip : StandardMinkowskiSpacetime.IsCausalTrip standardMinkowskiTimeOrientation p q
⊢ StandardMinkowskiSpacetime.IsCausalTrip standardMinkowskiTimeOrientation (g • p) (g • q)</pre>

```lean
    exact Relation.TransGen.lift (fun x => g • x)
      (fun _ _ hs => causalSegmentPrecedes_smul g hs)
      _ _ htrip
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `rcases … with rfl | htrip`: `.mp` turns `h` into `p = q ∨ IsCausalTrip …`, and `rcases` splits
  the two cases; the two `_` are the spacetime and the time orientation. In the first case, the
  pattern `rfl` does more than name the equation: it substitutes `q := p` everywhere, so the goal
  becomes `g • p ≺ g • p`.
* `exact causallyPrecedes_refl _ _ _`: reflexivity of `≺`, applied to the spacetime, the time
  orientation and the point, all read off the goal.
* `apply causallyPrecedes_of_isCausalTrip`: in the second case it suffices to give a causal trip
  from `g • p` to `g • q`, since every causal trip gives causal precedence.
* `exact Relation.TransGen.lift …`: Mathlib's `Relation.TransGen.lift f` lifts a map `f` that
  preserves a relation to its transitive closure. Here `f` is `x ↦ g • x`, the relation is
  `CausalSegmentPrecedes`, which `causalSegmentPrecedes_smul` shows is preserved, and `htrip` is the
  chain to be transported. The two `_` are the endpoints `p` and `q`.

This direction is the library's `causallyPrecedes_smul`, proved in one line with
`Relation.ReflTransGen.lift`, which handles both cases at once. The converse comes from the inverse
group element:

<div class="goals" markdown="1">

```lean
example (g : InhomogeneousLorentzGroup)
    (p q : StandardMinkowskiSpacetime.Carrier) :
    (g • p ≺[StandardMinkowskiSpacetime,
        standardMinkowskiTimeOrientation] g • q) ↔
      (p ≺[StandardMinkowskiSpacetime,
        standardMinkowskiTimeOrientation] q) := by
  constructor
```

<pre class="tactic-state">case mp
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
⊢ (g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • q) →
p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q

case mpr
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
⊢ (p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q) →
g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • q</pre>

```lean
  · intro h
```

<pre class="tactic-state">case mp
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
h : g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • q
⊢ p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q</pre>

```lean
    have h' := causallyPrecedes_smul g⁻¹ h
```

<pre class="tactic-state">case mp
g : InhomogeneousLorentzGroup
p : StandardMinkowskiSpacetime.Carrier
q : StandardMinkowskiSpacetime.Carrier
h : g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g • q
h&#x27; : g⁻¹ • g • p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] g⁻¹ • g • q
⊢ p ≺[StandardMinkowskiSpacetime, standardMinkowskiTimeOrientation] q</pre>

```lean
    rwa [inv_smul_smul, inv_smul_smul] at h'
```

<pre class="tactic-state">All goals completed! 🐙</pre>

```lean
  · exact causallyPrecedes_smul g
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `constructor` splits the `↔` into its two implications.
* `have h' := causallyPrecedes_smul g⁻¹ h`: applying the forward direction with `g⁻¹` to
  `h : g • p ≺ g • q` gives `g⁻¹ • g • p ≺ g⁻¹ • g • q`.
* `rwa [inv_smul_smul, inv_smul_smul] at h'`: Mathlib's `inv_smul_smul` states
  `g⁻¹ • g • x = x` for any group action. After the two rewrites, `h'` is the goal `p ≺ q`; `rwa` is
  `rw` followed by closing the goal with a hypothesis.
* `exact causallyPrecedes_smul g`: the second implication is the forward direction itself.

### 3.4.3 Covariance of the net

Spacelike relatedness is defined from `≺` alone, so it is invariant too
(`isSpacelikeRelated_smul_iff`), and so is complete spacelike separation of two regions
(`isCompletelySpacelike_smul_iff`, and its one-directional form `isCompletelySpacelike_smul`).
The same argument for `≪` gives `chronologicallyPrecedes_smul_iff`, so a Lorentz transformation
maps diamonds to diamonds:
`isAlexandrovBasisSet_smul L hB` proves `IsAlexandrovBasisSet (L • B)` from
`hB : IsAlexandrovBasisSet B`.

These facts are what Axiom 5 needs. For a net `N`, the map $$\alpha_L$$ on the diamond `B` is
`N.covEquiv L B`, a \*-isomorphism from `N.algebra B` to `N.algebra (L • B)` chosen from the
existence statement of `LorentzCovariance`. It is compatible with isotony
(`HaagKastlerNet.covEquiv_isotony`), it preserves norms (`HaagKastlerNet.norm_covEquiv`), and it
preserves commutation within one algebra (`HaagKastlerNet.commute_covEquiv_iff`). With the
invariance of spacelike separation, the hypothesis of Axiom 3 is itself Lorentz invariant: if
$$\mathbf{B}_1$$ and $$\mathbf{B}_2$$ are completely spacelike diamonds, so are `L • B₁` and
`L • B₂`, and Axiom 3 applies to them. In particular the transported observables commute, as the
second exercise below shows; the proof needs nothing about `covEquiv` beyond its type.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that spacelike relatedness is Lorentz invariant. The library's
`isSpacelikeRelated_congr M t f hf p₁ p₂` proves
`IsSpacelikeRelated M t (f p₁) (f p₂) ↔ IsSpacelikeRelated M t p₁ p₂` for any map `f` with
`hf : ∀ p q, (f p ≺[M, t] f q) ↔ (p ≺[M, t] q)`.

```lean
example (g : InhomogeneousLorentzGroup)
    (p₁ p₂ : StandardMinkowskiSpacetime.Carrier) :
    IsSpacelikeRelated StandardMinkowskiSpacetime
        standardMinkowskiTimeOrientation (g • p₁) (g • p₂) ↔
      IsSpacelikeRelated StandardMinkowskiSpacetime
        standardMinkowskiTimeOrientation p₁ p₂ :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (g : InhomogeneousLorentzGroup)
    (p₁ p₂ : StandardMinkowskiSpacetime.Carrier) :
    IsSpacelikeRelated StandardMinkowskiSpacetime
        standardMinkowskiTimeOrientation (g • p₁) (g • p₂) ↔
      IsSpacelikeRelated StandardMinkowskiSpacetime
        standardMinkowskiTimeOrientation p₁ p₂ :=
  isSpacelikeRelated_congr _ _ (fun x => g • x)
    (causallyPrecedes_smul_iff g) p₁ p₂
```

`causallyPrecedes_smul_iff g` is a function of `p` and `q`, so it is exactly the hypothesis `hf`.
This is the library's proof of `isSpacelikeRelated_smul_iff`.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that transported observables of completely spacelike diamonds commute: if `B₁` and `B₂` are
completely spacelike, the transported observables `N.covEquiv L B₁ a` and `N.covEquiv L B₂ b`, which live in the algebras of
`L • B₁` and `L • B₂`, commute in $$\mathfrak{U}$$. Use `HaagKastlerNet.commute_ι_of_spacelike`,
`isAlexandrovBasisSet_smul` and `isCompletelySpacelike_smul`.

```lean
example (N : HaagKastlerNet) (L : InhomogeneousLorentzGroup)
    {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (a : N.algebra B₁) (b : N.algebra B₂) :
    Commute
      (N.quasilocal.ι (isAlexandrovBasisSet_smul L hB₁)
        (N.covEquiv L B₁ a))
      (N.quasilocal.ι (isAlexandrovBasisSet_smul L hB₂)
        (N.covEquiv L B₂ b)) :=
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (N : HaagKastlerNet) (L : InhomogeneousLorentzGroup)
    {B₁ B₂ : Set StandardMinkowskiSpacetime.Carrier}
    (hB₁ : IsAlexandrovBasisSet B₁)
    (hB₂ : IsAlexandrovBasisSet B₂)
    (hs : IsCompletelySpacelike StandardMinkowskiSpacetime
      standardMinkowskiTimeOrientation B₁ B₂)
    (a : N.algebra B₁) (b : N.algebra B₂) :
    Commute
      (N.quasilocal.ι (isAlexandrovBasisSet_smul L hB₁)
        (N.covEquiv L B₁ a))
      (N.quasilocal.ι (isAlexandrovBasisSet_smul L hB₂)
        (N.covEquiv L B₂ b)) :=
  N.commute_ι_of_spacelike _ _
    (isCompletelySpacelike_smul L hs) _ _
```

The images `L • B₁` and `L • B₂` are diamonds, by `isAlexandrovBasisSet_smul`, and completely
spacelike, by `isCompletelySpacelike_smul`, so Axiom 3 in $$\mathfrak{U}$$ applies to them. The four `_` are
the two diamond proofs and the two elements, which Lean reads off the goal. Commutation inside one
algebra is carried by `commute_covEquiv_iff` instead.

</details>

</div>

## 3.5 What the examples show {#worked-examples-summary}

The four examples share a method, and it is the method of the whole library.

* **Start from the blueprint.** The examples rest on blueprint entries: `def:haag-kastler-net` for
  the axioms, `def:state` and `thrm:gns-construction-theorem` for the state and its representation,
  `def:local-commutativity`, `lmm:local-commutativity-any-quasilocal` and `thrm:einstein-causality`
  for locality, and `thrm:causal-precedence-lorentz-invariant` for covariance. The blueprint gives
  the statement and a proof in ordinary mathematics; the Lean statement is reviewed against it.
* **Take the axioms as hypotheses.** A theorem about AQFT takes a net `N : HaagKastlerNet` as an
  argument and uses its fields: `N.localCommutativity` in the third example, `N.covEquiv` and the
  quasilocal algebra `N.quasilocal` in the fourth. Every result then holds for every net, the
  trivial one included, and for the nets of physical interest once they are built.
* **Build objects by their fields.** The trivial net, the identity state and the vector state are
  each defined by giving the data and proving the conditions, field by field, as for any structure.
* **Prove by the paper argument.** Each Lean proof is the paper proof with its steps made explicit:
  unfold a definition, split into cases, rewrite with a law such as the compatibility of the
  embeddings with isotony, and apply a general lemma such as `Commute.map` or
  `Relation.TransGen.lift`. The goal after each step is what a careful written proof would state.

The examples also show where the library stops. Its only concrete net is the trivial one, which
contains no quantum physics; the states of this chapter are states on single algebras, not on the
quasilocal algebra of a physical net; and the library constructs no vacuum state. A
free field, as a net of Weyl algebras with its Fock vacuum, would be the natural next model.

Chapter 4, "Doing it yourself", turns from reading to writing. It explains how to install Lean,
work with the library on your own machine, run the exercises of these chapters there, and go from
a blueprint statement to a checked Lean theorem of your own.

# 4. Doing it yourself {#doing-it-yourself}

The first three chapters are written to be read in the browser. This one moves you onto your own
machine. By its end you should be able to build the library, run and change the tutorial's examples,
state a new result in the blueprint and in Lean, find the API you need, prove the result, and open a
pull request that passes the project's checks. The chapter follows one small project from start to
finish: a state on the quasilocal algebra of the trivial net, the construction that
[chapter 3](#worked-examples-gns) left open.

Commands to type in a terminal are shown as plain code blocks; they are not run when the tutorial
is built. Lean code is checked against the library, as in chapters 2 and 3. The code below uses
the short names of chapter 3:

```lean
open Physicslib4 Spacetime AQFT.HaagKastler
open scoped ComplexOrder
```

## 4.1 Setting up {#doing-it-yourself-setup}

### 4.1.1 Installing Lean and building the library

Lean is installed through _elan_, which downloads and manages Lean versions. Each project names the
version it needs in a file `lean-toolchain` at its root, and elan fetches that version when you
first build the project, so you never install a Lean version by hand. The Lean community's
[installation guide](https://leanprover-community.github.io/get_started.html) covers each
operating system; on Linux and macOS it comes down to

```bash
curl https://elan.lean-lang.org/elan-init.sh -sSf | sh
```

and a new terminal. With `git` installed, fetch the library and build it:

```bash
git clone https://github.com/physicslib/physicslib4.git
cd physicslib4
lake exe cache get
lake build
```

_Lake_ is Lean's build tool, installed with elan. `lakefile.toml` names the project's dependencies,
Mathlib among them, and `lake-manifest.json` pins each to an exact commit.

* `lake exe cache get` downloads Mathlib's compiled files, several gigabytes: minutes on a fast
  connection, longer on a slow one. Without it, `lake build` would compile Mathlib itself, which
  takes hours. (`lake exe cache get!` downloads everything again, if a download was interrupted.)
* `lake build` then compiles the library's hundred-odd files. The first time takes a while (tens
  of minutes on a laptop is normal); later builds recompile only the files that changed and those
  that import them.

A build that ends without errors has checked every proof in the library.

### 4.1.2 The editor

The standard editor is [VS Code](https://code.visualstudio.com/) with the _Lean 4_ extension.
Open the folder `physicslib4` itself, so that the extension finds `lean-toolchain`, and then a
library file, say `Physicslib4/AQFT/HaagKastler/Net.lean`, the home of chapter 3's trivial net.
A Lean server starts, loads the file's imports (seconds, once `lake build` has run) and checks the
file as you type. Three things are then at hand.

* The _infoview_, a panel beside the file (the ∀ menu, "Toggle Infoview"). With the cursor in a
  tactic proof it shows the goal at that point, as the `goals` blocks of chapters 2 and 3 do for a
  whole proof. Step through `trivialLocalNet_localCommutativity` and watch the goal change.
* _Hovers_, as on these pages: the type and docstring of a name. Ctrl-click (Cmd-click on macOS)
  jumps to its definition, in the library or in Mathlib.
* _Errors_ and warnings, underlined in the file and listed in the infoview. Lean checks past an
  error, so one mistake does not hide the next.

A file sees changes to the files it imports once they are saved and its server is restarted
("Lean 4: Server: Restart File").

### 4.1.3 Running the tutorial's exercises

Create a file at the root of the repository, say `Playground.lean`, and start it with

```lean
import Physicslib4

open Physicslib4 Spacetime AQFT.HaagKastler
open scoped ComplexOrder InnerProductSpace
```

`import Physicslib4` loads the whole library, and Mathlib with it. Below, paste an exercise from
chapter 2 or 3, together with any definition from the text it uses, such as chapter 3's
`identityState`, and replace the `sorry` by a proof. The file is yours; do not commit it.

The tutorial itself is the Lean package in `web/`, one file per chapter: this one is
`web/Tutorial/DoingItYourself.lean`. Its Lean examples are checked when the package is built:

```bash
cd web
lake exe cache get
lake build
lake exe generate-tutorial --output _out/tutorial
```

The first `lake build` in `web/` compiles Verso, the tool that renders these pages, and the native
code of the modules it links, and takes a while. The last command writes the HTML to
`web/_out/tutorial/html-multi/`, and `web/README.md` explains how to view it. Change an example so
that it fails to check, and the build stops there.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

_Needs a local setup._ Build the library, open `Physicslib4/AQFT/HaagKastler/Net.lean`, and find
the proof of `trivialLocalNet_localCommutativity`. Put the cursor after `intro` and read the goal
in the infoview. Then replace `@mul_comm ℂ _ _ _` by `mul_comm` and read the error.

<details class="solution" markdown="1">
<summary>Solution</summary>

After the `intro` the goal is the commutation of the two embedded elements, as in the worked proof
of [chapter 3](#worked-examples-trivial-net). With plain `mul_comm`, the error is
`typeclass instance problem is stuck`, followed by `CommMagma ?m`: Lean needs a commutative
multiplication on some type, but the goal, a `Commute` statement about elements of
`trivialLocalNet.algebra B`, does not tell it which type, and it will not search for an instance on
an unknown one. Chapter 3 gave the fix: name the type, `@mul_comm ℂ _ _ _` or
`mul_comm (G := ℂ)`. Undo the change before going on.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

_Needs a local setup._ Create `Playground.lean` as above and run the first exercise of
[chapter 3, section 2](#worked-examples-gns): show that `identityState` is faithful.

<details class="solution" markdown="1">
<summary>Solution</summary>

Paste the definition of `identityState` from chapter 3, then the exercise, and complete it:

```lean
example : identityState.IsFaithful := by
  intro a ha
  exact star_mul_self_pos_iff.mpr ha
```

The infoview shows the goal `0 < identityState (star a * a)` after `intro a ha`. If the file reports
an unknown identifier, check the `open` lines at its top.

</details>

</div>

## 4.2 How the project is organised {#doing-it-yourself-organisation}

### 4.2.1 The blueprint is the specification

As you will recall from chapter 1, the project's starting point is the blueprint, a document in
ordinary mathematics that sharpens the 1964 axioms of [Haag and Kastler (1964)](https://doi.org/10.1063/1.1704187) where they are
under-specified. Its chapters 1 to 9 analyse the original axioms one by one and give the context;
only chapter 10 is formalised. Every definition and theorem of chapter 10 carries a label, such as
`def:state`, and names the Lean declarations that formalise it. A Lean statement is correct when it
says what its blueprint entry says, so it is checked against the blueprint, and not against the
1964 paper or a textbook. If you think the blueprint is wrong or imprecise, the fix starts there.

### 4.2.2 Where things are

The repository has four parts.

* `Physicslib4/`: the library, by subject. `Spacetime/` and `Geometry/` hold spacetimes, their
  causal structure and the Alexandrov topology; `GNS/` states and the GNS construction;
  `Spectral/` and `Operators/` the spectral theorems, Stone's theorem and operator algebra;
  `Analysis/` supporting analysis; `AQFT/HaagKastler/` and `AQFT/HaagKastlerCurved/` the axioms
  in Minkowski and in curved spacetime. The file `Physicslib4.lean` imports every file of the
  library.
* `blueprint/src/`: the blueprint's LaTeX source; chapter 10 is in `sections/sec10/`, one file per
  section.
* `web/`: the project's website, this tutorial and the reference manual, which follows the
  sections of chapter 10 and collects the library's conventions.

The published versions are linked from the header of this page: the blueprint, with its dependency
graph, and the API documentation, generated from the docstrings.

### 4.2.3 Conventions

A few rules keep the library and the blueprint in agreement.

* _Definitions are design decisions._ The topology on Minkowski space, the class of regions, and the
  fields of structures such as `LocalNet`, `Isotony` and `HaagKastlerNet` fix what the library
  means by a net. A change to them changes what every theorem says, so it is proposed and discussed
  in an issue before it is made. Theorems, lemmas and proofs can be added freely.
* _Restrictions are recorded._ When a declaration is deliberately less general than the blueprint
  intends, its docstring says so on a line starting `**Restriction:**`, naming the intended general
  form and what it is waiting on, in the form
  `**Restriction:** <restriction>; the intended form <general form>, and is waiting on <result>.`
  The line is removed when the general form is formalised.
* _Documentation is in the present tense._ Docstrings, comments, the blueprint and the home page
  describe what the project is, not how it came to be: no "previously" or "now". The history goes in
  `CHANGELOG.md`.
* _No `sorry`._ A `sorry` is useful while you work, as you will see, but the library contains none,
  and a contribution adds none.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Find Einstein causality, `thrm:einstein-causality`, in the blueprint (the theorem of chapter 3's
third example), and follow it to the Lean. Which declarations formalise it, in which file, and which
blueprint entries does it use?

<details class="solution" markdown="1">
<summary>Solution</summary>

The entry names two declarations, `HaagKastlerNet.einstein_causality` and
`HaagKastlerNet.exists_gns_einstein_causality`, both in the namespace
`Physicslib4.AQFT.HaagKastler` and in the file
`Physicslib4/AQFT/HaagKastler/EinsteinCausality.lean`.
It uses `def:haag-kastler-net`, `thrm:gns-construction-theorem` and `def:state`: the edges into
its node in the dependency graph.

</details>

</div>

## 4.3 From an idea to a statement {#doing-it-yourself-statement}

The project of this chapter comes from the end of [chapter 3, section 2](#worked-examples-gns).
Every net has a quasilocal algebra `N.quasilocal`, chosen once and for all, and for the trivial net
it is isomorphic to $$\mathbb{C}$$, but not literally `ℂ`. So `identityState` is not a state on it,
and the library constructs none. The claim to prove: _the quasilocal algebra of the
trivial net consists of the multiples of the unit, and has exactly one state,
$$\lambda\mathbf{1} \mapsto \lambda$$._

### 4.3.1 Start from the blueprint

A new result begins as a blueprint entry. In `blueprint/src/sections/sec10/haag-kastler-axioms.tex`,
next to the entries it depends on, it would read:

```latex
\begin{proposition}[The State of the Trivial Net]
    \label{prpstn:trivial-net-state}
    \uses{def:state, def:quasilocal-algebra}
    Let $\mathfrak{U}$ be the quasilocal algebra of the net that
    assigns $\mathbb{C}$ to every diamond. Every element of
    $\mathfrak{U}$ is a multiple $\lambda\mathbf{1}$ of the unit,
    and $\lambda\mathbf{1} \mapsto \lambda$ is the only state
    on $\mathfrak{U}$.
\end{proposition}
\begin{proof}
    \uses{def:quasilocal-algebra}
    Each local algebra is $\mathbb{C}$, so its image in $\mathfrak{U}$
    lies in $\mathbb{C}\mathbf{1}$. This subspace is finite-dimensional,
    hence closed, and the union of the images is dense, so
    $\mathfrak{U} = \mathbb{C}\mathbf{1}$. ...
\end{proof}
```

`\label` gives the entry its name. `\uses` lists the entries the statement, or the proof, depends
on; they become the edges of the dependency graph. Two more commands come later, once the Lean
exists: `\lean{…}`, with the full names of the declarations that formalise the entry (and
`\leanfile{…}`, this project's own addition, with their file), and `\leanok`, which marks the
statement as formalised when it is in the statement and the proof as formalised when it is in the
proof. The graph colours each node accordingly. Writing the proof on paper first is not a formality:
it tells you which lemmas the Lean proof needs.

### 4.3.2 Translate it into Lean

The statement goes in the library next to what it uses. Here that is a new file,
`Physicslib4/AQFT/HaagKastler/TrivialState.lean`, which imports the files that define the trivial
net and `GNS.State.comp`, opens `namespace Physicslib4.AQFT.HaagKastler` like its neighbours, and
is added to `Physicslib4.lean`. The two claims, with `sorry` for their proofs:

```lean
example (x : trivialHaagKastlerNet.quasilocal.carrier) :
    ∃ z : ℂ, algebraMap ℂ _ z = x := by
  sorry

example (ω : GNS.State
      trivialHaagKastlerNet.quasilocal.carrier)
    (z : ℂ) :
    ω (algebraMap ℂ _ z) = z := by
  sorry
```

`algebraMap ℂ A` is Mathlib's name for the map $$\lambda \mapsto \lambda\mathbf{1}$$ of a complex
algebra `A`, and the underscore lets Lean fill in `A` from the type of `x`. The first statement
says that every element is a multiple of the unit; the second that every state takes the value
$$\lambda$$ on $$\lambda\mathbf{1}$$, which, with the first, is uniqueness. Existence is a
construction, a term of type `GNS.State trivialHaagKastlerNet.quasilocal.carrier`, and
[section 6](#doing-it-yourself-project) builds it.

A `sorry` lets everything else be checked: Lean reports a warning, "declaration uses `sorry`", and
otherwise accepts the file. You can state all the lemmas of a proof this way, check that they fit
together, and fill them in one at a time.

### 4.3.3 Check what the statement says

A Lean statement can fail to mean what you intend, and a proof of the wrong statement is worth
nothing. Before proving, check it.

* _Read it back._ Hover over each name, or `#check` the statement, and read the result as
  mathematics. Is `trivialHaagKastlerNet.quasilocal.carrier` the algebra the blueprint means? It is:
  the quasilocal algebra that every predicate of the library, such as `IsVacuumState`, refers to.
* _Beware of statements that are too easy._ The library's `trivialQuasilocalAlgebra` is also a
  quasilocal algebra of the trivial net, with carrier `ℂ`, and a state on it is just
  `identityState`. Stated for it, the project would be a one-liner, and would say nothing about the
  algebra that matters.
* _Beware of hypotheses that cannot hold._ A theorem with contradictory hypotheses is true and
  useless. If you suspect this, try to prove `False` from them.
* _Test special cases._ Specialise the statement to a case you can check by hand, or try to prove a
  slightly stronger one and see where it fails.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

State in Lean that every state on the quasilocal algebra of every Haag–Kastler net takes the value
$$1$$ on the unit, and prove it with the library's `GNS.State.apply_one`.

<details class="solution" markdown="1">
<summary>Solution</summary>

```lean
example (N : HaagKastlerNet)
    (ω : GNS.State N.quasilocal.carrier) :
    ω 1 = 1 :=
  ω.apply_one
```

The net is an argument, as in chapter 3, so the statement holds for every net. The lemma holds for
a state on any C\*-algebra; dot notation finds it in the namespace `GNS.State`.

</details>

</div>

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Is the following a faithful translation of "the quasilocal algebra of the trivial net has a
state"? What is wrong with it?

```lean
example : Nonempty (GNS.State ℂ) :=
  ⟨identityState⟩
```

<details class="solution" markdown="1">
<summary>Solution</summary>

It is true, and proved, but it is a statement about `ℂ`, not about
`trivialHaagKastlerNet.quasilocal.carrier`. The two algebras are isomorphic, and the isomorphism
is precisely what the project has to construct. The faithful statement is
`Nonempty (GNS.State trivialHaagKastlerNet.quasilocal.carrier)`.

</details>

</div>

## 4.4 Finding the API {#doing-it-yourself-api}

Most of the work in a proof is finding what already exists. The paper proof of the last section
needs three facts: a unital \*-homomorphism sends $$\lambda\mathbf{1}$$ to $$\lambda\mathbf{1}$$; a
finite-dimensional subspace is closed; and a closed set that contains a set contains its closure.
All three are in Mathlib. Chapter 2 ([section 7](#lean-in-brief-mathlib)) listed several ways
to find them; here each is applied to one of the three.

### 4.4.1 Guessing a name, and `#check`

Mathlib's naming convention suggests where to look. A \*-homomorphism is in particular an algebra
homomorphism, and for these the property "commutes with `algebraMap`" is called `commutes`.
`#check` confirms the guess:

```lean
#check AlgHomClass.commutes
  (trivialHaagKastlerNet.quasilocal.ι
    isAlexandrovBasisSet_trivialBasisSet)
```

<pre class="lean-output">AlgHomClass.commutes
  (trivialHaagKastlerNet.quasilocal.ι
    isAlexandrovBasisSet_trivialBasisSet) : ∀ (r : ℂ),
  (trivialHaagKastlerNet.quasilocal.ι isAlexandrovBasisSet_trivialBasisSet)
      ((algebraMap ℂ (trivialHaagKastlerNet.U.algebra trivialBasisSet)) r) =
    (algebraMap ℂ trivialHaagKastlerNet.quasilocal.carrier) r</pre>

`AlgHomClass.commutes f r` holds for any algebra homomorphism `f`, \*-homomorphisms included,
and applying it to the embedding `ι` of one diamond (`trivialBasisSet`, the library's sample
diamond) shows what it says there: `ι` sends $$r\mathbf{1}$$ to $$r\mathbf{1}$$. Applying a lemma
to the objects at hand is often the quickest way to read it.

### 4.4.2 `exact?`, `apply?` and `rw?`

When the goal is a standard fact, let Lean search. `exact?` looks for a single lemma, applied to
hypotheses in context, that closes the goal:

```lean
example {X : Type} [TopologicalSpace X] (s t : Set X)
    (ht : IsClosed t) (h : s ⊆ t) : closure s ⊆ t := by
  exact?
```

<pre class="lean-output">Try this:
  [apply] exact (IsClosed.closure_subset_iff ht).mpr h</pre>

Replace `exact?` by the suggestion, which in the editor is one click. `apply?` lists lemmas whose
conclusion matches the goal, leaving their hypotheses as new goals, and `rw?` lists equations
that can rewrite it. These searches work well for small, general facts. They fail, or time out,
when the goal is large or the lemma needs an argument that is not in context, and they see the
goal as written: a goal phrased with the library's own definitions may need `change` or `unfold`
first.

### 4.4.3 Loogle

[Loogle](https://loogle.lean-lang.org/) searches Mathlib by the constants and patterns a statement
contains. The query `IsClosed, Submodule, FiniteDimensional` asks for statements that mention all
three, and among the first results is

```lean
Submodule.closed_of_finiteDimensional (s : Submodule 𝕜 E)
  [FiniteDimensional 𝕜 ↥s] : IsClosed ↑s
```

(with the hypotheses on the field `𝕜` and the space `E` omitted): a finite-dimensional subspace
of a Hausdorff topological vector space over a complete field is closed. Patterns with `?x` for
unknown terms, such as `closure ?s ⊆ ?t`, narrow the search further.

### 4.4.4 Documentation and sources

The [API documentation](https://physicslib.github.io/physicslib4/docs/) lists each declaration of
the library, and Mathlib's lists each of Mathlib's, with its docstring and a link to its source.
From the blueprint, each entry links to the documentation of its Lean declarations, so a concept
you know in mathematics leads to its Lean name. Finally, the sources are on your disk: Mathlib is
in `.lake/packages/mathlib/Mathlib/`, and a text search such as

```bash
grep -rn "closed_of_finiteDimensional" .lake/packages/mathlib/Mathlib
```

finds the declaration first, and its file, where the lemmas around it are often the ones you need
next.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

_Needs a local setup._ Use `exact?` to find the lemma that `algebraMap ℂ A` is injective when the
C\*-algebra `A` is nonzero:

```lean
example (A : Type) [CStarAlgebra A] [Nontrivial A] :
    Function.Injective (algebraMap ℂ A) := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

`exact?` suggests `exact FaithfulSMul.algebraMap_injective ℂ A`:

```lean
example (A : Type) [CStarAlgebra A] [Nontrivial A] :
    Function.Injective (algebraMap ℂ A) :=
  FaithfulSMul.algebraMap_injective ℂ A
```

The kernel of a ring homomorphism out of a field is an ideal without $$1$$, hence zero, so the map
is injective as soon as the target is nonzero. `(algebraMap ℂ A).injective` works as well.

</details>

</div>

## 4.5 Proving it {#doing-it-yourself-proving}

### 4.5.1 Working interactively

A Lean proof is written in a loop: read the goal in the infoview, take one step, read the new goal.
Each step should correspond to a sentence of the paper proof; if you cannot say which sentence, stop
and write it on paper first. Two habits help.

* _Keep the file checking._ Write `sorry` for whatever you have not done yet, so that Lean checks
  the rest and the infoview shows the goals that remain.
* _State intermediate facts._ `have h : P := by sorry` records a fact you will need, and you prove
  it once the main argument goes through. If the main argument does not go through, you have lost
  nothing.

### 4.5.2 Breaking a proof into lemmas

A long proof is a sequence of lemmas, each a short statement with a short proof. The paper proof of
[section 3](#doing-it-yourself-statement) has four steps, and the Lean has four lemmas:
local elements are scalars; the scalars form a closed set; therefore every element is a scalar; and
therefore $$\lambda \mapsto \lambda\mathbf{1}$$ is a bijection. Small lemmas are easier to prove,
easier to read, and often useful elsewhere. A rule of thumb: if a proof does not fit on a screen,
or a `have` is used twice, make it a lemma.

### 4.5.3 Common errors

Three kinds of error account for most of the time a beginner spends stuck. Each appeared, in a
mild form, in chapters 2 and 3.

_Type class problems._ Lean finds structure, such as a norm or a commutative multiplication, by type
class search ([chapter 2, section 5](#lean-in-brief-structures)). When the search fails, the
message says `failed to synthesize`; when Lean does not yet know the type to search on, it says
`typeclass instance problem is stuck`, as in the first exercise of
[section 1](#doing-it-yourself-setup). Another case: a `GNS.State` can be applied to an element,
like a function, but it is not registered as a linear map, so Mathlib's `map_smul` does not apply to
it:

```lean
example (ω : GNS.State ℂ) (z : ℂ) :
    ω (z • 1) = z • ω 1 := by
  rw [map_smul]
```

<pre class="lean-output">failed to synthesize instance of type class
  MulActionHomClass (GNS.State ℂ) ℂ ℂ ℂ

Hint: Type class instance resolution failures can be inspected with the `set_option trace.Meta.synthInstance true` command.</pre>

`MulActionHomClass` is the class of maps that commute with scalar multiplication, and Lean finds no
instance saying that states are such maps. (The second error, an unsolved goal of the same type,
is a consequence of the first.) The fix is to apply the lemma to the state's underlying continuous
linear map, `ω.toContinuousLinearMap`, as in the exercise below.

_Universe mismatches._ Recall the aside on universes in
[chapter 2, section 5](#lean-in-brief-structures): a structure such as `HaagKastlerNet.{u}` is
a family of types, one for each universe level.
The trivial net has its algebras in `Type`, so `nonempty_haagKastlerNet` is about level `0`, and
it cannot be used at level `1`:

```lean
example : Nonempty HaagKastlerNet.{1} :=
  nonempty_haagKastlerNet
```

<pre class="lean-output">Type mismatch
  nonempty_haagKastlerNet
has type
  Nonempty.{2} HaagKastlerNet
but is expected to have type
  Nonempty.{3} HaagKastlerNet</pre>

The levels in the message are those of `Nonempty`, which records where its argument lives:
`HaagKastlerNet.{0}` is a type in `Sort 2`, `HaagKastlerNet.{1}` one in `Sort 3`. Different levels,
different types. Lean's display omits the level of `HaagKastlerNet` itself, so a mismatch in which
two types print identically is often a universe mismatch; `set_option pp.universes true` shows
the levels. The fix is to state the result at the level where it holds, or to generalise the
construction.

_Coercions._ A state `ω` is applied to `a` through a coercion to a function, displayed `ω a`; its
field `ω.toContinuousLinearMap` is applied through another. The two are equal by definition, but
`rw` looks for a term as written, not up to definitions:

```lean
example (ω : GNS.State ℂ) :
    ω.toContinuousLinearMap 1 = 1 := by
  rw [ω.apply_one]
```

<pre class="lean-output">Tactic `rewrite` failed: Did not find an occurrence of the pattern
  ω 1
in the target expression
  ω.toContinuousLinearMap 1 = 1

ω : GNS.State ℂ
⊢ ω.toContinuousLinearMap 1 = 1</pre>

The fix is `change ω 1 = 1`, which replaces the goal by one equal to it by definition, followed by
the rewrite; or simply `exact ω.apply_one`, since `exact` does unfold definitions. Hover over the
terms in the infoview to see which coercion each uses.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Fix the first failing example above: prove `ω (z • 1) = z • ω 1` for a state on `ℂ`.

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example (ω : GNS.State ℂ) (z : ℂ) :
    ω (z • 1) = z • ω 1 := by
  change ω.toContinuousLinearMap (z • 1) =
    z • ω.toContinuousLinearMap 1
```

<pre class="tactic-state">ω : GNS.State ℂ
z : ℂ
⊢ ω.toContinuousLinearMap (z • 1) = z • ω.toContinuousLinearMap 1</pre>

```lean
  rw [map_smul]
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

`change` restates the goal in terms of the continuous linear map, to which it is equal by
definition. Then `rw [map_smul]` rewrites the left side to the right side, and `rw` closes the
goal by `rfl`.

</details>

</div>

## 4.6 The worked project {#doing-it-yourself-project}

This section carries out the project of [section 3](#doing-it-yourself-statement) in full,
with the lemmas found in [section 4](#doing-it-yourself-api). To keep the lines short, the
quasilocal algebra of the trivial net gets a local name:

```lean
noncomputable abbrev Q₀ :=
  trivialHaagKastlerNet.quasilocal
```

An `abbrev` is a definition that Lean unfolds freely, so type class search sees through `Q₀` to
the C\*-algebra structure of `trivialHaagKastlerNet.quasilocal.carrier`.

### 4.6.1 Local elements are scalars

The algebra of every diamond is `ℂ`, so an element `a` of it is a number, and `ι` sends it to
$$a\mathbf{1}$$. This is `AlgHomClass.commutes` applied to `ι`:

```lean
theorem trivial_ι_eq_algebraMap
    {B : Set StandardMinkowskiSpacetime.Carrier}
    (hB : IsAlexandrovBasisSet B)
    (a : trivialHaagKastlerNet.algebra B) :
    Q₀.ι hB a = algebraMap ℂ Q₀.carrier a :=
  AlgHomClass.commutes (Q₀.ι hB) a
```

The lemma's left side is `ι (algebraMap ℂ ℂ a)`, which is `ι a` by definition; on the right, Lean
accepts `a` as a complex number, although its type is the algebra of `B`, because the two types
are equal by definition.

### 4.6.2 The scalars are closed

The multiples of the unit form the range of `Algebra.linearMap ℂ A`, the map
$$\lambda \mapsto \lambda\mathbf{1}$$ as a linear map. Its range is a finite-dimensional subspace,
so `Submodule.closed_of_finiteDimensional` applies:

```lean
theorem isClosed_range_algebraMap {A : Type*}
    [CStarAlgebra A] :
    IsClosed (Set.range (algebraMap ℂ A)) := by
  have h := (LinearMap.range
    (Algebra.linearMap ℂ A)).closed_of_finiteDimensional
  rwa [LinearMap.coe_range] at h
```

`h` says that the range, as a subspace, is closed. `LinearMap.coe_range` turns the subspace into
the set `Set.range (Algebra.linearMap ℂ A)`, which is the goal up to definitions, and `rwa` closes
it. The finite-dimensionality is found by type class search: the range of a linear map out of a
finite-dimensional space is finite-dimensional. The lemma holds in every C\*-algebra, so it is
stated for every C\*-algebra.

### 4.6.3 Every element is a scalar

Now the paper argument: the union of the local images lies in the closed set of scalars, so its
closure does too, and the closure is everything.

<div class="goals" markdown="1">

```lean
theorem trivial_exists_scalar (x : Q₀.carrier) :
    ∃ z : ℂ, algebraMap ℂ Q₀.carrier z = x := by
  have hsub :
      (⋃ (B : Set StandardMinkowskiSpacetime.Carrier)
        (hB : IsAlexandrovBasisSet B),
          Set.range (Q₀.ι hB)) ⊆
      Set.range (algebraMap ℂ Q₀.carrier) := by
    simp only [Set.iUnion_subset_iff]
    rintro B hB _ ⟨a, rfl⟩
    exact ⟨a, (trivial_ι_eq_algebraMap hB a).symm⟩
  have hcl :=
    isClosed_range_algebraMap.closure_subset_iff.mpr hsub
```

<pre class="tactic-state">x : Q₀.carrier
hsub : ⋃ B, ⋃ (hB : IsAlexandrovBasisSet B), Set.range ⇑(Q₀.ι hB) ⊆ Set.range ⇑(algebraMap ℂ Q₀.carrier)
hcl : closure (⋃ B, ⋃ (hB : IsAlexandrovBasisSet B), Set.range ⇑(Q₀.ι hB)) ⊆ Set.range ⇑(algebraMap ℂ Q₀.carrier)
⊢ ∃ z, (algebraMap ℂ Q₀.carrier) z = x</pre>

```lean
  exact hcl (Q₀.dense_range x)
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `have hsub : … := by …` states the inclusion of the union of the images in the scalars. Its
  proof: `simp only [Set.iUnion_subset_iff]` turns "a union is contained in a set" into "each
  member is", and `rintro` introduces a diamond `B`, its proof `hB`, and an element of the range of
  `ι`, written `ι a` by the pattern `⟨a, rfl⟩`. Then `a` itself is the scalar.
* `have hcl := …` applies `IsClosed.closure_subset_iff`, found by `exact?` in section 4, to get
  the closure of the union inside the scalars.
* `exact hcl (Q₀.dense_range x)`: the field `dense_range` of a quasilocal algebra says that the
  union is dense, so `x` is in its closure, and hence a scalar.

### 4.6.4 The isomorphism, and the state

The map $$\lambda \mapsto \lambda\mathbf{1}$$ is Mathlib's `StarAlgHom.ofId ℂ Q₀.carrier`. It is
surjective by the last lemma, and injective because the algebra is nonzero: `ι` is injective and
$$1 \neq 0$$ in `ℂ`.

<div class="goals" markdown="1">

```lean
theorem trivial_bijective :
    Function.Bijective
      (StarAlgHom.ofId ℂ Q₀.carrier) := by
  refine ⟨?_, trivial_exists_scalar⟩
```

<pre class="tactic-state">⊢ Function.Injective ⇑(StarAlgHom.ofId ℂ Q₀.carrier)</pre>

```lean
  have hB := isAlexandrovBasisSet_trivialBasisSet
```

<pre class="tactic-state">hB : IsAlexandrovBasisSet trivialBasisSet
⊢ Function.Injective ⇑(StarAlgHom.ofId ℂ Q₀.carrier)</pre>

```lean
  have h10 : (1 : Q₀.carrier) ≠ 0 := by
    intro h
    have h' : Q₀.ι hB 1 = Q₀.ι hB 0 := by
      rw [map_one, map_zero]
      exact h
    exact one_ne_zero (α := ℂ) (Q₀.ι_injective hB h')
```

<pre class="tactic-state">hB : IsAlexandrovBasisSet trivialBasisSet
h10 : 1 ≠ 0
⊢ Function.Injective ⇑(StarAlgHom.ofId ℂ Q₀.carrier)</pre>

```lean
  have : Nontrivial Q₀.carrier := ⟨⟨1, 0, h10⟩⟩
```

<pre class="tactic-state">hB : IsAlexandrovBasisSet trivialBasisSet
h10 : 1 ≠ 0
this : Nontrivial Q₀.carrier
⊢ Function.Injective ⇑(StarAlgHom.ofId ℂ Q₀.carrier)</pre>

```lean
  exact FaithfulSMul.algebraMap_injective ℂ Q₀.carrier
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

* `refine ⟨?_, trivial_exists_scalar⟩`: a bijection is a pair, injective and surjective. The
  second is the last lemma; `?_` leaves the first as the goal.
* `h10` proves $$1 \neq 0$$ in `Q₀.carrier`: if $$1 = 0$$, then `ι 1 = ι 0` in the sample diamond,
  and injectivity of `ι` gives $$1 = 0$$ in its algebra, which is `ℂ`. Note `(α := ℂ)`, which
  names the type as in chapter 3: the algebra of the diamond is `ℂ` only by definition.
* `have : Nontrivial Q₀.carrier` puts the instance in context, and the lemma of the section 4
  exercise finishes.

A bijective \*-homomorphism is a \*-isomorphism (`StarAlgEquiv.ofBijective`). Its inverse is the
\*-homomorphism to `ℂ` the project needs, and the state is chapter 3's `identityState` pulled back
along it with `GNS.State.comp`:

```lean
noncomputable def trivialNetState :
    GNS.State Q₀.carrier :=
  identityState.comp
    (StarAlgEquiv.ofBijective _
      trivial_bijective).symm.toStarAlgHom

example (z : ℂ) :
    trivialNetState
      (algebraMap ℂ Q₀.carrier z) = z := by
  change identityState
    ((StarAlgEquiv.ofBijective _ trivial_bijective).symm
      (StarAlgEquiv.ofBijective _ trivial_bijective z))
    = z
  rw [StarAlgEquiv.symm_apply_apply]
  rfl
```

The check confirms that the state is $$\lambda\mathbf{1} \mapsto \lambda$$: `change` writes
$$\lambda\mathbf{1}$$ as the image of $$\lambda$$ under the isomorphism, the isomorphism and its
inverse cancel, and `identityState z = z` by definition.

### 4.6.5 Recording it

In the library the four lemmas and the definition go into the file of
[section 3](#doing-it-yourself-statement), each with a docstring giving the blueprint label.
The blueprint entry then gets its links and its marks:

```latex
\begin{proposition}[The State of the Trivial Net]
    \label{prpstn:trivial-net-state}
    \lean{Physicslib4.AQFT.HaagKastler.trivial_exists_scalar,
      Physicslib4.AQFT.HaagKastler.trivialNetState}
    \leanfile{Physicslib4/AQFT/HaagKastler/TrivialState.lean}
    \uses{def:state, def:quasilocal-algebra}
    \leanok
    ...
\end{proposition}
\begin{proof}
    \uses{def:quasilocal-algebra}
    \leanok
    ...
\end{proof}
```

The `\leanok` in the proof belongs there only once the whole proposition is proved in Lean,
uniqueness included, which is the exercise below; until then the proof carries none, and the
dependency graph shows the gap.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Prove uniqueness: every state on `Q₀.carrier` agrees with `trivialNetState`. Write `x` as a
scalar with `trivial_exists_scalar`, then use `Algebra.algebraMap_eq_smul_one`, linearity of the
underlying continuous linear maps, as in section 5, and `GNS.State.apply_one`.

```lean
example (ω : GNS.State Q₀.carrier) (x : Q₀.carrier) :
    ω x = trivialNetState x := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example (ω : GNS.State Q₀.carrier) (x : Q₀.carrier) :
    ω x = trivialNetState x := by
  obtain ⟨z, rfl⟩ := trivial_exists_scalar x
```

<pre class="tactic-state">ω : GNS.State Q₀.carrier
z : ℂ
⊢ ω ((algebraMap ℂ Q₀.carrier) z) = trivialNetState ((algebraMap ℂ Q₀.carrier) z)</pre>

```lean
  rw [Algebra.algebraMap_eq_smul_one]
```

<pre class="tactic-state">ω : GNS.State Q₀.carrier
z : ℂ
⊢ ω (z • 1) = trivialNetState (z • 1)</pre>

```lean
  change ω.toContinuousLinearMap (z • 1) =
    trivialNetState.toContinuousLinearMap (z • 1)
```

<pre class="tactic-state">ω : GNS.State Q₀.carrier
z : ℂ
⊢ ω.toContinuousLinearMap (z • 1) = trivialNetState.toContinuousLinearMap (z • 1)</pre>

```lean
  rw [map_smul, map_smul]
```

<pre class="tactic-state">ω : GNS.State Q₀.carrier
z : ℂ
⊢ z • ω.toContinuousLinearMap 1 = z • trivialNetState.toContinuousLinearMap 1</pre>

```lean
  change z • ω 1 = z • trivialNetState 1
```

<pre class="tactic-state">ω : GNS.State Q₀.carrier
z : ℂ
⊢ z • ω 1 = z • trivialNetState 1</pre>

```lean
  rw [ω.apply_one, trivialNetState.apply_one]
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

`obtain ⟨z, rfl⟩` replaces `x` by `algebraMap ℂ _ z` everywhere. After rewriting it as `z • 1`, the
two `change` steps move between a state and its continuous linear map, so that `map_smul` applies
and then `apply_one` does. The final goal `z • 1 = z • 1` is closed by `rw`. With `DFunLike.ext`
this gives `ω = trivialNetState`: $$\mathfrak{U}$$ has exactly one state.

</details>

</div>

## 4.7 Checking and contributing {#doing-it-yourself-checking}

### 4.7.1 What CI checks

Every push and every pull request runs the workflow `.github/workflows/lean_action_ci.yml` on
GitHub. It checks, in order:

* that the library builds (`lake build`);
* that it passes the linters of Mathlib's companion library Batteries (`lake lint`): every
  definition has a docstring, no argument is unused, `simp` lemmas are in the right form, and so
  on;
* that `Physicslib4.lean` imports every file of the library (`lake exe mk_all --check`), so a new
  file must be added there;
* that every Lean name in a blueprint `\lean{…}` exists (`checkdecls`, from the package of the
  same name);
* that the documentation is in the present tense (`scripts/check_temporal_wording.py`), as
  [section 2](#doing-it-yourself-organisation) asked;
* when `web/`, the library or the toolchain changes, that the website and this tutorial build, and
  that their pages use no root-relative links.

A second workflow, `.github/workflows/blueprint.yml`, runs on the `main` branch only. It builds the
blueprint's web and PDF versions, the API documentation, the website and the tutorial, and
publishes them.

### 4.7.2 Running the checks yourself

Run the checks before you push; it is faster than waiting for CI. From the root of the repository:

```bash
lake build
lake lint
lake exe mk_all --check
python3 scripts/check_temporal_wording.py
```

The blueprint needs `leanblueprint`, a Python package (`pip install leanblueprint`; it needs
Graphviz for the dependency graph and a LaTeX installation for the PDF; its README gives the
details per system). After a successful `lake build`,

```bash
leanblueprint web
leanblueprint pdf
leanblueprint checkdecls
```

build the blueprint into `blueprint/web/` and `blueprint/print/`, and then check the `\lean{…}`
names against the build (`checkdecls` reads the list of names that `leanblueprint web` writes). Open
`blueprint/web/index.html` and the dependency graph, and check that your entry and its edges look as
intended. For changes to the tutorial or the website, build them as in
[section 1](#doing-it-yourself-setup).

### 4.7.3 Pull requests

Contributions follow the usual GitHub process. Create a branch, commit your work to it, and open a
pull request against `main`. A pull request is merged when it passes all the checks above, has no
conflicts with `main`, and is approved by a reviewer. A notable change, such as a new result, a
changed definition or a new section of the blueprint, also gets a line in `CHANGELOG.md`, under
"Unreleased"; that file, not the documentation, is where the project's history is recorded. Keep a
pull request to one topic: a reviewer can check one new result with its blueprint entry far more
easily than five.

When you are stuck, ask. The [Lean Zulip chat](https://leanprover.zulipchat.com/), in particular
its "new members" and "Is there code for X?" channels, answers questions about Lean and Mathlib,
usually within hours; a question with a short complete example that shows the problem gets the
best answers. Questions and proposals about this project, including proposed changes to its
definitions, go to the
[repository's issues](https://github.com/physicslib/physicslib4/issues).

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

You add the file `Physicslib4/AQFT/HaagKastler/TrivialState.lean` of the worked project, with a
docstring on `trivialNetState` that reads "The state is now proved unique." You forget to add the
file to `Physicslib4.lean`. Which checks fail?

<details class="solution" markdown="1">
<summary>Solution</summary>

Two. `lake exe mk_all --check` fails, because `Physicslib4.lean` does not import the new file. And
`scripts/check_temporal_wording.py` fails on "now proved", which narrates history; the docstring
should say "The state is unique." Note that `lake build` passes: it builds only what
`Physicslib4.lean` imports, so the new file is not even compiled, and an error in it would go
unnoticed, which is one reason for the import check. If the blueprint entry of section 6 is
already in place, `checkdecls` fails too: its `\lean{…}` names are declared in a file that is not
built.

</details>

</div>

## 4.8 Where to go next {#doing-it-yourself-next}

The library formalises every entry of the blueprint's chapter 10, so new work extends the
blueprint as well as the Lean. Some directions, from small to large:

* _The vacuum of the trivial net._ Chapter 3 noted that the library constructs no vacuum state
  for any net. `trivialNetState` is the candidate for the trivial net: it is invariant (the
  exercise below), and the spectrum condition should hold in a one-dimensional GNS space where
  every translation acts as the identity.
* _A net with quantum physics in it._ The free scalar field, as a net of Weyl algebras with its
  Fock vacuum, would be the first model whose local algebras are not commutative.
* _Restrictions._ A declaration that is less general than intended says so in a
  `**Restriction:**` line, naming what it waits on; `grep -rn "Restriction:" Physicslib4` lists
  them, and each is a ready-made project. The search can come back empty, when every declaration
  has its intended general form.
* _Mathlib._ Results proved here that are not about physics, such as the extension of a
  \*-homomorphism from a dense \*-subalgebra (`exists_starAlgHom_extend_of_dense`), belong in
  Mathlib, where everyone can use them.

The reference manual, linked from the header, is in preparation. It is the companion to this
tutorial, meant to describe the library's definitions and theorems systematically where the
tutorial teaches by example. For Lean and Mathlib themselves, the further reading at the end of
[chapter 2](#lean-in-brief) is the place to continue, with _Mathematics in Lean_ first; for
the physics, the further reading at the end of [chapter 1](#aqft-in-brief), and the
blueprint.

<div class="exercise" markdown="1">
<p class="exercise-label">Exercise</p>

Show that `trivialNetState` is invariant under the covariance action of the trivial net, the first
half of the vacuum conditions. A \*-automorphism, like any algebra homomorphism, satisfies
`AlgHomClass.commutes`.

```lean
example : trivialHaagKastlerNet.IsInvariantState
    trivialNetState := by
  sorry
```

<details class="solution" markdown="1">
<summary>Solution</summary>

<div class="goals" markdown="1">

```lean
example : trivialHaagKastlerNet.IsInvariantState
    trivialNetState := by
  intro L a
```

<pre class="tactic-state">L : InhomogeneousLorentzGroup
a : trivialHaagKastlerNet.quasilocal.carrier
⊢ trivialNetState ((trivialHaagKastlerNet.action L) a) = trivialNetState a</pre>

```lean
  obtain ⟨z, rfl⟩ := trivial_exists_scalar a
```

<pre class="tactic-state">L : InhomogeneousLorentzGroup
z : ℂ
⊢ trivialNetState ((trivialHaagKastlerNet.action L) ((algebraMap ℂ Q₀.carrier) z)) =
trivialNetState ((algebraMap ℂ Q₀.carrier) z)</pre>

```lean
  rw [AlgHomClass.commutes]
```

<pre class="tactic-state">All goals completed! 🐙</pre>

</div>

After `intro L a` the goal is
`trivialNetState (trivialHaagKastlerNet.action L a) = trivialNetState a`. Writing `a` as
$$z\mathbf{1}$$, the action fixes it, since every unital \*-automorphism fixes the multiples of
the unit; `rw` rewrites the left side to the right and closes the goal. Every state
on this algebra is invariant, in fact, since there is only one.

</details>

</div>

</div>
