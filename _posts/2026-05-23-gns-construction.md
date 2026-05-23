---
title:  "GNS Construction Theorem"
date:   2026-05-23 07:43:42 +0200
categories: aqft
---

In this blog post we will state and prove the GNS Construction Theorem, which we make extensive use of in subsequent blog posts.

In this blog post generally we follow the clear, straightforward presentation in [Entanglement in Algebraic Quantum Field Theories](https://arxiv.org/abs/2410.16599).

# GNS Construction Theorem
In this section we will state the GNS Construction Theorem, which we prove in subsequent sections.

Before stating the theorem we'll need to introduce terminology that appears in the theorem's statement. We begin with the definition of "state" and some closely associated terms.

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

# Proof of the GNS Construction Theorem
With the GNS Construction Theorem stated, we can now commence with its proof.

This proof has five parts: (1) the construction of the GNS Hilbert space $$\mathcal{H}_\omega$$, (2) the construction of the \*-representation $$\pi_\omega$$, (3) the construction of the cyclic vector $$\Omega$$ in $$\mathcal{H}_\omega$$, (4) the proof that the \*-representation $$\pi_\omega$$ is faithful, and (5) the proof of uniqueness up to unitary equivalence. Each part corresponds to a subsequent subsection.

## Construction of the GNS Hilbert Space
We'll construct the GNS Hilbert space $$\mathcal{H}_\omega$$ from the C\*-algebra $$\mathfrak{U}$$ itself, modifying $$\mathfrak{U}$$ as needed to obtain the desired $$\mathcal{H}_\omega$$.

Let's start by attempting to place an inner product on $$\mathfrak{U}$$. Naively one might hope the following defines an inner product

$$
\left< a, b \right> \equiv \omega(a^*b)
$$

on $$\mathfrak{U}$$. Unfortunately it doesn't. Let's examine why this fails.

Consider the set

$$
\mathcal{N} \equiv \{ n \in \mathfrak{U} : \omega(n^*n) = 0 \}.
$$

Generically $$\omega$$ isn't faithful. Thus in $$\mathcal{N}$$ there exist non-zero $$n$$. For such $$n$$ one has

$$
\left< n, n \right> \equiv \omega(n^*n) = 0.
$$

Hence, there are non-zero $$n$$ in $$\mathfrak{U}$$ such that $$\left< n, n \right> = 0$$. The existence of such $$n$$ proves that our naive inner product on $$\mathfrak{U}$$

$$
\left< a, b \right> \equiv \omega(a^*b)
$$

actually isn't an inner product. However, the form $$\mathcal{N}$$ takes gives us a hint as to how to repair this naive inner product.

In particular, if we quotient $$\mathfrak{U}$$ by $$\mathcal{N}$$ we may rid ourselves of the problem we encountered above and hopefully be able to construct an inner product on $$\mathfrak{U} / \mathcal{N}$$ and its completion. We'll see this plan actually works.

However, before being able to see this plan through we'll need to take a quick detour and prove a few needed results.

The most famous of these results is the Cauchy-Schwarz Inequality

> **Lemma** *(Cauchy-Schwarz Inequality)*
> Let $$\mathcal{A}$$ be a \*-algebra and $$\omega$$ a *positive* element of the dual space $$\mathcal{A}^*$$, i.e. $$\omega$$ is an element of the dual space $$\mathcal{A}^*$$ such that for any $$a \in \mathcal{A}$$ one has $$0 \le \omega(a^*a)$$. Then
> 
> $$
> \begin{align}
> \omega(a^*b) &= \overline{\omega(b^*a)} \\
> |\omega(a^*b)|^2 &\le \omega(a^*a) \omega(b^*b)
> \end{align}
> $$
> 
> for all $$a$$ and $$b$$ in $$\mathcal{A}$$.

**Proof**
Positivity of $$\omega$$ implies that for any $$a$$ and $$b$$ in $$\mathcal{A}$$ and $$\lambda \in \mathbb{C}$$ one has

$$
0 \le \omega\left((\lambda a + b)^*(\lambda a + b)\right).
$$

As $$\omega$$ is an element of the dual space $$\mathcal{A}^*$$ and thus linear, this implies

$$
0 \le |\lambda|^2\omega(a^*a) + \overline{\lambda}\omega(a^*b) + \lambda\omega(b^*a) + \omega(b^*b).
$$

This inequality then implies both desired results,

$$
\begin{align}
\omega(a^*b) &= \overline{\omega(b^*a)} \\
|\omega(a^*b)|^2 &\le \omega(a^*a) \omega(b^*b).
\end{align}
$$

We will prove these one-by-one. Let us first prove this inequality implies $$\omega(a^*b) = \overline{\omega(b^*a)}$$.

Notice that the inequality is between two real numbers, $$0$$ and the righthand side. As $$\omega$$ is positive, the first and last summands on the righthand side are obviously real. This then implies

$$
\overline{\lambda}\omega(a^*b) + \lambda\omega(b^*a) \in \mathbb{R}.
$$

As $$\lambda$$ is arbitrary, we are free to choose it to be real, which implies the imaginary parts of $$\omega(a^*b)$$ and $$\omega(b^*a)$$ are equal but have the opposite signs.

Similarly, we are free to choose $$\lambda$$ to be imaginary, which implies that the real parts of $$\omega(a^*b)$$ and $$\omega(b^*a)$$ are equal. Together these facts imply the first result

$$
\omega(a^*b) = \overline{\omega(b^*a)}.
$$

Let us next prove that our inequality

$$
0 \le |\lambda|^2\omega(a^*a) + \overline{\lambda}\omega(a^*b) + \lambda\omega(b^*a) + \omega(b^*b)
$$

implies $$\lvert \omega(a^*b) \rvert^2 \le \omega(a^*a) \omega(b^*b)$$.

Again, as $$\lambda$$ is arbitrary, we are free to choose it to extreemize the righthand side of the inequality. Extremizing the righthand of this inequality with respect to $$\overline{\lambda}$$ one finds at the extrema

$$
\lambda = - \frac{\omega(a^*b)}{\omega(a^*a)}.
$$

Substituting this into the inequality, multiplying by $$\omega(a^*a)$$ while using the fact that $$\omega$$ is positive, and using $$\omega(a^*b) = \overline{\omega(b^*a)}$$, then one obtains

$$
0 \le \lvert \omega(a^*b) \rvert^2 - \lvert \omega(a^*b) \rvert^2 - \lvert \omega(a^*b) \rvert^2 + \omega(a^*a) \omega(b^*b)
$$

which implies

$$
\lvert \omega(a^*b) \rvert^2 \le \omega(a^*a) \omega(b^*b),
$$

the second desired result. $$\blacksquare$$

The next result we need to prove is:

> **Lemma**
> Let $$\omega$$ be a state over a unital C\*-algebra $$\mathfrak{U}$$. Then the set $$\mathcal{N}_1$$ defined by
> 
> $$
> \mathcal{N}_1 \equiv \{ n \in \mathfrak{U} : \omega(b^*n) = 0 \;\; \forall \, b \in \mathfrak{U} \}
> $$
> 
> is equivalent to the set $$\mathcal{N}$$ defined by
> 
> $$
> \mathcal{N} \equiv \{ n \in \mathfrak{U} : \omega(n^*n) = 0 \}.
> $$

**Proof**
We will first prove that $$\mathcal{N} \subseteq \mathcal{N}_1$$. Then we will prove $$\mathcal{N}_1 \subseteq \mathcal{N}$$. Together these imply $$\mathcal{N} = \mathcal{N}_1$$, the final desired result.

Let us begin by proving $$\mathcal{N} \subseteq \mathcal{N}_1$$.

$$\mathfrak{U}$$ is a C\*-algebra and thus a \*-algebra. In addition $$\omega$$ is a state and thus a positive element of the dual space $$\mathfrak{U}^*$$. Thus, for arbitrary $$b$$ and $$n$$ in $$\mathfrak{U}$$ we can apply the Cauchy-Schwarz inequality to obtain

$$
\lvert \omega(b^*n) \rvert^2 \le \omega(b^*b) \omega(n^*n). 
$$

Thus if $$n$$ is in $$\mathcal{N}$$, and thus satisfies $$\omega(n^*n) = 0$$, then this inequality implies $$\omega(b^*n) = 0$$ for all $$b$$ in $$\mathfrak{U}$$. This then implies $$n$$ is in $$\mathcal{N}_1$$. As $$n$$ was an arbitrary element of $$\mathcal{N}$$, this in turn implies that $$\mathcal{N} \subseteq \mathcal{N}_1$$, the first desired result.

Next let us prove that $$\mathcal{N}_1 \subseteq \mathcal{N}$$.

Consider an arbitrary $$n_1$$ in $$\mathcal{N}_1$$. By definition $$\omega(b^*n_1) = 0$$ for any $$b$$ in $$\mathfrak{U}$$. In particular we can select $$b=n_1$$. Doing so we have $$\omega(n_1^*n_1) = 0$$. This then implies $$n_1$$ is in $$\mathcal{N}$$. As $$n_1$$ was an arbitrary element of $$\mathcal{N}_1$$ this further implies $$\mathcal{N}_1 \subseteq \mathcal{N}$$, the second desired result.

We have thus proven $$\mathcal{N} \subseteq \mathcal{N}_1$$ and $$\mathcal{N}_1 \subseteq \mathcal{N}$$ which together imply $$\mathcal{N} = \mathcal{N}_1$$, the final desired result. $$\blacksquare$$

Next we will prove $$\mathcal{N}$$ is a closed, linear subspace of $$\mathfrak{U}$$. Establishing this will allow us to take the quotient of $$\mathfrak{U}$$ by $$\mathcal{N}$$.

> **Lemma**
> Let $$\omega$$ be a state over a unital C\*-algebra $$\mathfrak{U}$$. Then the set $$\mathcal{N}$$ defined by
> 
> $$
> \mathcal{N} \equiv \{ n \in \mathfrak{U} : \omega(n^*n) = 0 \}.
> $$
> 
> is a closed, linear subspace of $$\mathfrak{U}$$.

**Proof**
First let us prove that $$\mathcal{N}$$ is a linear subspace of $$\mathfrak{U}$$.

Consider arbitrary $$n,m \in \mathcal{N}$$ and arbitrary $$\lambda, \mu \in \mathbb{C}$$. As proven above $$\mathcal{N} = \mathcal{N}_1$$, thus for arbitrary $$b \in \mathfrak{U}$$, one has

$$
\begin{align}
\omega(b^*n) &= 0 \\
\omega(b^*m) &= 0.
\end{align}
$$

Hence, the linearity of $$\omega$$ then implies

$$
\omega(b^*(\lambda n + \mu m)) = \lambda \omega(b^*n) + \mu \omega(b^*m) = 0.
$$

As $$b \in \mathfrak{U}$$ was arbitrary, this implies that $$(\lambda n + \mu m) \in \mathcal{N}_1$$. As we previously proved $$\mathcal{N} = \mathcal{N}_1$$, this in turn implies $$(\lambda n + \mu m) \in \mathcal{N}$$. Hence $$\mathcal{N}$$ is a linear subspace of $$\mathfrak{U}$$, the first desired result.

Next let us prove that $$\mathcal{N}$$ is a closed subspace of $$\mathfrak{U}$$.

First, let us note that as $$\omega$$ is a state, it is by definition a linear, normalized operator on $$\mathfrak{U}$$. Hence, it is a linear, bounded operator on $$\mathfrak{U}$$, a normed space. Thus, as a result of the standard theorem (Theorem B.2.4 of [Entanglement in Algebraic Quantum Field Theories](https://arxiv.org/abs/2410.16599))

> **Theorem**
> Let $$X$$ and $$Y$$ be normed spaces and $$T: \mathcal{D}(T) \rightarrow Y$$ be a linear operator where $$\mathcal{D}(T) \subseteq X$$. Then $$T$$ is continuous if and only if it is bounded. 

along with the fact that $$\mathbb{C}$$ is a normed space, it follows that $$\omega$$ is continuous.

With the continuity of $$\omega$$ in hand, consider a sequence $$(n_i)_{i \in \mathbb{N}}$$ in $$\mathcal{N}$$ that converges to $$n$$ in $$\mathfrak{U}$$. As $$\omega$$ is continuous, for any $$b$$ in $$\mathfrak{U}$$ one has

$$
\omega\left(b^*n\right) = \omega\left(b^*(\lim\limits_{i \rightarrow \infty} n_i)\right) = \lim\limits_{i \rightarrow \infty} \omega(b^*n_i) = 0,
$$

where the final equality follows from our previous result $$\mathcal{N} = \mathcal{N}_1$$. This proves that $$n$$ is an element of $$\mathcal{N}_1$$ and thus, as a consequence of our previous result $$\mathcal{N}_1 = \mathcal{N}$$, that $$n$$ is an element of $$\mathcal{N}$$. This establishes that $$\mathcal{N}$$ is closed, proving the second and final desired result, $$\mathcal{N}$$ is a closed subspace of $$\mathfrak{U}$$. $$\blacksquare$$

As we have established that $$\mathcal{N}$$ is a closed, linear subspace of $$\mathfrak{U}$$, we can now take the quotient of $$\mathfrak{U}$$ by $$\mathcal{N}$$. Elements of thie quotient $$\mathfrak{U} / \mathcal{N}$$ are equivalence classes of the form

$$
[a] \equiv \{ a + n : n \in \mathcal{N} \}
$$

with the zero vector in $$\mathfrak{U} / \mathcal{N}$$ given by

$$
[0] \equiv \{ n : n \in \mathcal{N} \}.
$$

On $$\mathfrak{U} / \mathcal{N}$$ we can introduce an inner product

$$
\left<[a], [b]\right> \equiv \omega(a^*b)
$$

motivated by our naive attempt at placing an inner product on $$\mathfrak{U}$$. This inner product is well-defined on $$\mathfrak{U} / \mathcal{N}$$ as one can see from its invariance under $$a \rightarrow a + n$$ where $$n$$ is in $$\mathcal{N}$$,

$$
\omega((a + n)^*b) = \omega(a^*b) + \omega(n^*b) = \omega(a^*b) + \overline{\omega(b^*n)} = \omega(a^*b).
$$

In this the first equality follows from $$\omega$$ being linear, the second from our previous result $$\omega(n^*b) = \overline{\omega(b^*n)}$$, and the final from our previous result $$\mathcal{N} = \mathcal{N}_1$$.

Furthermore, the inner product

$$
\left<[a], [b]\right> \equiv \omega(a^*b)
$$

on $$\mathfrak{U} / \mathcal{N}$$ doesn't suffer from the same problem of our naive inner product on $$\mathfrak{U}$$ did. In particular, one can easilly prove

$$
\left<[a], [a]\right> = 0
$$

if and only if $$[a] = [0]$$. This is essentially by construction.

The final step in going from $$\mathfrak{U} / \mathcal{N}$$ to the Hilbert space $$\mathcal{H}_\omega$$ consists of completing $$\mathfrak{U} / \mathcal{N}$$ in the norm defined by the inner product above. As this is standard, we will not present the details here. The completion of $$\mathfrak{U} / \mathcal{N}$$ in this norm is the Hilbert space $$\mathcal{H}_\omega$$ of the GNS Construction Theorem.

## Construction of the GNS Representation
Next we will construct $$\pi_\omega$$ the \*-representation of $$\mathfrak{U}$$ by bounded operators on $$\mathcal{H}_\omega$$. This will be much easier than the construction of $$\mathcal{H}_\omega$$.

By construction we can consider $$\mathfrak{U} / \mathcal{N}$$ as dense in $$\mathcal{H}_\omega$$. On this dense subset we define the action of $$\pi_\omega$$ the \*-representation of $$\mathfrak{U}$$ on $$\mathfrak{U} / \mathcal{N}$$ as follows

$$
\pi_\omega(a)[z] \equiv [az]
$$

where $$[z]$$ is an arbitrary element of $$\mathfrak{U} / \mathcal{N}$$.

This definition of $$\pi_\omega$$ on $$\mathfrak{U} / \mathcal{N}$$ is well-defined as for any other member of the equivalence class $$[z]$$ of the form $$[z + n]$$ one has

$$
\pi_\omega(a)[z + n] = [az + an] = [az],
$$

where the second equality follows from our previous result $$\mathcal{N}_1 = \mathcal{N}$$. In other words, $$\pi_\omega$$ is well-defined as $$\mathcal{N}$$ is a left-ideal in $$\mathfrak{U}$$.

Furthermore, it trivially follows from the definition of $$\pi_\omega$$ that it is linear and an algebraic morphism. So it remains to prove that $$\pi_\omega$$ is bounded and also a \*-morphism. 

Let us first prove that $$\pi_\omega$$ is bounded.

Consider a non-zero $$[z]$$ in $$\mathfrak{U} / \mathcal{N}$$. Simply applying definitions one has 

$$
\begin{align}
\|\pi_\omega(a)[z]\|^2 &= \|[az]\|^2 \\
                       &= \left<[az], [az]\right> \\
                       &= \omega((az)^*(az)) \\
                       &= \omega(z^*(a^*a)z) \\
                       &= \frac{\omega(z^*(a^*a)z)}{\omega(z^*z)} \omega(z^*z) \\
                       &= \frac{\omega(z^*(a^*a)z)}{\omega(z^*z)} \|[z]\|^2. 
\end{align}
$$

With that last equation in mind let us define the map $$\phi$$ acting on $$\mathfrak{U}$$ by

$$
\phi(a) \equiv \frac{\omega(z^*az)}{\omega(z^*z)}.
$$

One can easilly check that $$\phi$$ defines a state on $$\mathfrak{U}$$ as it is linear, positive

$$
\phi(c^*c) = \frac{\omega(z^*(c^*c)z)}{\omega(z^*z)} = \frac{\omega((cz)^*(cz))}{\omega(z^*z)} \ge 0
$$

as $$\omega$$ is positive, and normalized

$$
\|\phi\| \equiv \sup\limits_{a \in \{b \in \mathfrak{U} : \|b\| = 1\}} |\phi(a)| = \sup\limits_{a \in \{b \in \mathfrak{U} : \|b\| = 1\}} \left| \frac{\omega(z^*az)}{\omega(z^*z)} \right| = 1,
$$

where the final equality follows from the fact that $$\phi$$ divides by $$\omega(z^*z)$$ and $$\|a\|=1$$ and so the supremum is achieved at $$a=\mathbf{1}$$.

Now as $$\phi$$ is normalized and thus $$\|\phi\|=1$$, the definition of the norm $$\|\phi\|$$ implies

$$
\|\phi(c)\| \le \|\phi\| \, \|c\| = \|c\|.
$$

This along with our previous derivation gives

$$
\begin{align}
\|\pi_\omega(a)[z]\|^2 &= \phi(a^*a) \|[z]\|^2 \\
                       &\le \|\phi\| \, \|a^*a\| \, \|[z]\|^2 \\
                       &=  \|a^*a\| \, \|[z]\|^2 \\
                       &= \|a\|^2 \, \|[z]\|^2.
\end{align}
$$

Using the definition of the norm $$\|\pi_\omega(a)\|$$ this equation then implies

$$
\|\pi_\omega(a)\| \le \|a\|
$$

which is the statement that $$\pi_\omega(a)$$ is a bounded operator on $$\mathfrak{U} / \mathcal{N}$$.

Thus using the following standard theorem (Theorem A.36 [Hall](https://doi.org/10.1007/978-1-4614-7116-5)) 

> **Theorem** *(Bounded Linear Transformation Theorem)*
> *Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.*

one can extend $$\pi_\omega$$ from the dense subset $$\mathfrak{U} / \mathcal{N}$$ of $$\mathcal{H}_\omega$$ to all of $$\mathcal{H}_\omega$$. We do so and use the same notation $$\pi_\omega$$ for this extension.

Finally we need to prove that $$\pi_\omega$$ is not only an algebraic morphism but is a \*-morphism. Thankfully this is relatively simple.

For $$[x]$$ and $$[y]$$ in $$\mathfrak{U} / \mathcal{N}$$ and $$a$$ in $$\mathfrak{U}$$, we have

$$
\begin{align}
\left<[x], \pi_\omega(a^*)[y]\right> &= \left<[x], [a^*y]\right> \\
                                     &= \omega(x^*a^*y) \\
                                     &= \omega((ax)^*y) \\
                                     &= \left<[ax], [y]\right> \\
                                     &= \left<\pi_\omega(a)[x], [y]\right> \\
                                     &= \left<[x], \pi_\omega(a)^\dagger [y]\right>
\end{align}
$$

Hence, $$\pi_\omega(a^*) = \pi_\omega(a)^\dagger$$ and $$\pi_\omega$$ is a \*-morphism.

## Construction of the Cyclic Vector
Our next task is to construct the cyclic vector $$\Omega$$. This is relatively straightforward.

As $$\mathfrak{U}$$ is unital we can make the definition

$$
\Omega \equiv [\mathbf{1}].
$$

Tracing definitions we have

$$
\{\pi_\omega(a)\Omega : a \in \mathfrak{U}\} = \{[a] : a \in \mathfrak{U}\} = \mathfrak{U} / \mathcal{N}.
$$

As $$\mathfrak{U} / \mathcal{N}$$ is dense in $$\mathcal{H}_\omega$$, this implies that $$\Omega$$ is a cyclic vector in $$\mathcal{H}_\omega$$ for the representation $$\pi_\omega$$, the property claimed of $$\Omega$$ in the GNS Construction Theorem.

In addition tracing definitions gives

$$
\left<\Omega, \pi_\omega(a)\Omega\right> = \left<[\mathbf{1}], \pi_\omega(a)[\mathbf{1}]\right> = \left<[\mathbf{1}], [a]\right> = \omega(\mathbf{1}a) = \omega(a)
$$

which proves another relation

$$
\omega(a) = \left<\Omega, \pi_\omega(a)\Omega\right>
$$

claimed in the GNS Construction Theorem.

## Faithfullness of the GNS Representation
Now we are going to prove the \*-representation $$\pi_\omega$$ is faithful if $$\omega$$ is a faithful state.

For this section of the proof, assume that $$\omega$$ is a faithful state.

To prove that $$\pi_\omega$$ is faithful representation, we must prove that $$\ker \pi_\omega = \{0\}$$. In other words, we must prove that $$\pi_\omega(a) = 0$$ implies that $$a=0$$.

Assume that $$\pi_\omega(a) = 0$$. Thus we have

$$
0 = \left<\pi_\omega(a)\Omega, \pi_\omega(a)\Omega\right> = \omega(a^*a).
$$

As $$\omega$$ is assumed faithful in this section of the proof, this implies that $$a^*a=0$$. Hence,

$$
0 = \|a^*a\| = \|a\|^2,
$$

where we have employed the C\*-norm property. This in turn implies $$\|a\|=0$$ which implies $$a=0$$. This in turn implies $$\ker \pi_\omega = \{0\}$$, which proves that if $$\omega$$ is faithful, then $$\pi_\omega$$ is faithful, the desired result.

## Uniqueness up to Unitary Equivalence
Finally to complete the proof of the GNS Construction Theorem we now prove that the GNS triple associated to $$(\mathfrak{U}, \omega)$$ is is unique up to unitary equivalence.

To that end let $$(\mathcal{H}_\omega', \pi_\omega', \Omega')$$ be a second GNS triple associated to $$(\mathfrak{U}, \omega)$$. (This implies, in particular, that the inner product on $$\mathcal{H}_\omega'$$ is given by $$\omega$$.) Then define an operator $$U$$ by

$$
U\pi_\omega(a)\Omega \equiv \pi_\omega(a)'\Omega'.
$$

The operator $$U$$ is obviously linear. Furthermore, as $$\Omega$$ and $$\Omega'$$ are cyclic, the domain of $$U$$ is dense in $$\mathcal{H}_\omega$$ and its range is dense in $$\mathcal{H}_\omega'$$ . Now, as a result of chasing definitions

$$
\begin{align}
\left< U\pi_\omega(a)\Omega, U\pi_\omega(b)\Omega \right>' &= \left<\pi_\omega(a)'\Omega', \pi_\omega(b)'\Omega'\right>' \\
                                                           &= \omega(a^*b) \\
                                                           &= \left<\pi_\omega(a)\Omega, \pi_\omega(b)\Omega\right>
\end{align}
$$

we find that $$U$$ preserves the inner product and is thus bounded. Furthermore, as $$U$$ preserves the inner product on its dense domain and dense range, it's also unitary there.

As $$U$$ is bounded on its dense domain, the Bounded Linear Transformation Theorem (Theorem A.36 [Hall](https://doi.org/10.1007/978-1-4614-7116-5))

> **Theorem** *(Bounded Linear Transformation Theorem)*
> *Let $$V_1$$ be a normed space and $$V_2$$ a Banach space. Suppose $$W$$ is a dense subspace of $$V_1$$ and $$T: W \rightarrow V_2$$ is a bounded linear map. Then there exists a unique bounded linear map $$\widetilde{T}: V_1 \rightarrow V_2$$ such that $$\widetilde{T}|_W = T$$. Furthermore, the norm of $$\widetilde{T}$$ equals the norm of $$T$$.*

can be used to extend the domain of $$U$$ to all of $$\mathcal{H}_\omega$$. This gives a well-defined, unitary map from $$\mathcal{H}_\omega$$ to $$\mathcal{H}_\omega'$$ that we also denote by $$U : \mathcal{H}_\omega \rightarrow \mathcal{H}_\omega'$$.

Now, the definition of $$U$$

$$
U\pi_\omega(a)\Omega = \pi_\omega(a)'\Omega'.
$$

gives for the case $$a = \mathbf{1}$$

$$
U\Omega = \Omega'.
$$

Hence, the fact that $$U$$ is unitary and thus $$U^{-1}$$ is well-defined gives

$$
\begin{align}
\left< U\pi_\omega(a)\Omega, U\pi_\omega(b)\Omega \right>' &= \left< U\pi_\omega(a)U^{-1}U\Omega, U\pi_\omega(b)\Omega \right>' \\
                                                           &= \left< U\pi_\omega(a)U^{-1}U\Omega, \pi_\omega(b)'\Omega' \right>' \\
                                                           &= \left< U\pi_\omega(a)U^{-1}\Omega', \pi_\omega(b)'\Omega' \right>'. 
\end{align}
$$

However, the definition of $$U$$ implies

$$
\left< U\pi_\omega(a)\Omega, U\pi_\omega(b)\Omega \right>' = \left<\pi_\omega(a)'\Omega', \pi_\omega(b)'\Omega'\right>'.
$$ 

Thus the previous two equations imply

$$
\left< U\pi_\omega(a)U^{-1}\Omega', \pi_\omega(b)'\Omega' \right>' = \left<\pi_\omega(a)'\Omega', \pi_\omega(b)'\Omega'\right>'
$$

which implies

$$
\pi_\omega(a)' = U\pi_\omega(a)U^{-1},
$$

proving that two GNS triples associated to $$(\mathfrak{U}, \omega)$$ can differ at most by a unitary transformation, completing our proof of the GNS Construction Theorem. $$\blacksquare$$

# Summary
This concludes the proof of the GNS Construction Theorem, 

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

The reason we provided such detail is that we will have need not only of the theorem, but also of the details of the theorem's proof in subsequent blogs posts.

[^1]: Note $$\mathfrak{U}$$ is an abstract C\*-algebra and need not be a quasilocal algebra or in any way associated with an AQFT.
