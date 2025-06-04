# Division Test
In the Division Test, a prover $\mathcal{P}$, who knows polynomial functions 
$$
f(X) \in \mathbb{F}^{(\leq d)}[X], g(X) \in \mathbb{F}^{(\leq d)}[X],
$$
tries to convince a verifier $\mathcal{V}$, who has oracle access or commitment to $f, g$ (denoted by $ \boxed{f}, \boxed{g}$), that
$$
\prod_{a \in \Omega} f(a)/g(a) = 1,
$$
where $ \Omega$ is a multiplicative subgroup of $\mathbb{F}$, where$ |\Omega| = k$:
$$
\Omega = \{ 1,\, w,\, w^2,\, \ldots,\, w^{k-1} \},
$$

---

A naive try by the verifier would be:
1. **Individual Queries**: The verifier queries the oracle for each $ a \in \Omega $. This results in $ \mathcal{O}(k) $ queries and a corresponding verification time of $ \mathcal{O}(k) $.

However, our goal is to achieve a constant number of queries (i.e., $ \mathcal{O}(1) $, independent of $ k $ and $ d $) and logarithmic verification time (i.e., $ \mathcal{O}(\log k) $).

We use the same set $\Omega$ from the zero test, i.e.,
$$
\Omega = \{1, w, w^2, \dots, w^{k-1}\},
$$
where $w$ is a primitive $k$th root of unity in $\mathbb{F}_p$.

---
## Auxiliary Polynomial $t(X)$

We define a polynomial $t(X)$ such that

$$
t(w \cdot x) \, g(w \cdot x) = t(x)\, f(w \cdot x) \quad \forall x \in \Omega.
$$

To understand this relationship, let us expand it over the points of $\Omega$:

- For $x = w^{k-1}$:  
  $$
  t(w^k) = \dfrac{f(w^k)}{g(w^k)} \, t(w^{k-1})
  \quad\Longrightarrow\quad
  t(1) = \dfrac{f(1)}{g(1)}\, t(w^{k-1}),
  $$
  since $w^k = 1$.

- For $x = w^{k-2}$:
  $$
  t(w^{k-1}) = \dfrac{f(w^{k-1})}{g(w^{k-1})}\, t(w^{k-2}).
  $$

- For $x = w^{k-3}$:
  $$
  t(w^{k-2}) = \dfrac{f(w^{k-2})}{g(w^{k-2})}\, t(w^{k-3})
  \quad\Longrightarrow\quad
  t(w^{k-1}) = \dfrac{f(w^{k-1})}{g(w^{k-1})}\, \dfrac{f(w^{k-2})}{g(w^{k-2})}\, t(w^{k-3}),
  $$

and so on, until eventually:

- For $x = w$:
  $$
  t(w^2) = \dfrac{f(w^2)}{g(w^2)}\, t(w),
  $$
- For $x = 1$:
  $$
  t(w) = \dfrac{f(w)}{g(w)}\, t(1).
  $$

Chaining these together, we get:

$$
t(w^{k-1}) 
= 
\dfrac{f(w^{k-1})}{g(w^{k-1})}\, \dfrac{f(w^{k-2})}{g(w^{k-2})} \,\dots\, \dfrac{f(w)}{g(w)}\, \dfrac{f(1)}{g(1)}\, t(w^{k-1}).
$$

If $t(w^{k-1}) \neq 0$ (i.e. $t(w^{k-1}) = 1$), we can divide both sides by $t(w^{k-1})$ and obtain

$$
1
=
\dfrac{f(w^{k-1})}{g(w^{k-1})}\, \dfrac{f(w^{k-2})}{g(w^{k-2})} \,\dots\, \dfrac{f(w)}{g(w)}\, \dfrac{f(1)}{g(1)}
$$

Thus, to show this relationship, the prover’s goal boils down to proving:

1. $t(w^{k-1}) = 1$.  
2. $t(w \cdot x) = \dfrac{f(w \cdot x)}{g(w \cdot x)}\, t(x)$ for all $x \in \Omega$.

---

## Protocol Overview
It is very similar to the product test. Therefore, I do not write the protocol for now.

---

## Time and Size Complexity
Let $p,\; d,\; k$ denote the field size, the degree of $f(X)$, and the size of $\Omega$ (respectively the degree of the vanishing polynomial $Z_{\Omega}(X)$).


1. **Prover**:  
   - The prover computes $t(X)$ (degree $k-1$) and $q(X)$ (degree $d-1$). This can be done in 
     $\mathcal{O}(d \log d)$ time (e.g., via FFT-based methods).  
   - The prover then:
     1. Commits to $t(X)$ and $q(X)$.
     2. Evaluates 
        $$
        q(r),\quad t(r),\quad t(wr),\quad f(wr), g(wr),\quad t(w^{k-1})
        $$
        at the random challenge $r$.
     3. Generates evaluation proofs that these values match the committed polynomials.


2. **Verifier**:  
   - Computes $Z_{\Omega}(r)$ in 
     $\mathcal{O}(\log k)$ time (e.g., by exponentiation for $(r^k - 1)$).  
   - Checks:
     1. The correctness of the commitments and their openings (depends on the underlying commitment scheme).
     2. The equality $t(w^{k-1}) \stackrel{?}{=} 1$.
     3. The equality 
        $$
        t(wr)g(wr) - t(r)\,f(wr) 
        \;\stackrel{?}{=}\; 
        q(r)\,\bigl(Z_{\Omega}(r)\bigr).
        $$

   In the KZG commitment scheme, these checks are constant time.

3. . **Proof Size**:  
   - The proof contains:
     1. Commitments to $q(X)$ and $t(X)$.
     2. The values 
        $$q(r),\; t(r),\; t(wr),\; f(wr), g(wr),\; t(w^{k-1}),$$ 
        plus the corresponding evaluation proofs.  
   - In a KZG scheme, all of these are of constant size, independent of $d$ or $k$.