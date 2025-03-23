# Vanishing Polynomial
Let $\mathbb{F}_p$ be a field of large prime order $p$, and let $\Omega \subseteq \mathbb{F}_p$ be a subgroup of $\mathbb{F}_p$ with $\lvert \Omega \rvert = k$. In many practical protocols, $\Omega$ is a *multiplicative* subgroup of $\mathbb{F}_p^\times$. This chapter explains the notion of a vanishing polynomial over $\Omega$ and why restricting $\Omega$ to a cyclic subgroup can be highly efficient.


---

## 1. Vanishing Polynomial
A *vanishing polynomial* of $\Omega$, denoted $Z_{\Omega}(X)$, is the unique polynomial that evaluates to zero at every point in $\Omega$. In symbols:
$$
Z_{\Omega}(X) \;=\; \prod_{a \in \Omega} (X - a),
$$
which immediately implies $\deg\!\bigl(Z_{\Omega}\bigr) = \lvert \Omega \rvert = k$.

**Remark**: Using a specific subset $\Omega$ (rather than the entire field $\mathbb{F}_p$) lets us work with a smaller, more manageable set of evaluation points. If we took $\Omega$ to be all of $\mathbb{F}_p\setminus\{0\}$, the resulting polynomial would have degree $p-1$, which is impractical to handle in many protocols.

#### Example (Computing a Vanishing Polynomial in a Small Field)
Consider the small field $\mathbb{F}_7$ and let $\Omega = \{1, 3, 5\} \subset \mathbb{F}_7$. Then:
$$
Z_{\Omega}(X) 
= (X - 1)(X - 3)(X - 5).
$$
Expanding over $\mathbb{F}_7$:
$$
(X - 1)(X - 3) = X^2 - 4X + 3 \equiv X^2 + 3X + 3
$$
(since $-4 \equiv 3 \pmod{7}$). Next:
$$
(X^2 + 3X + 3)(X - 5) 
= X^3 - 5X^2 + 3X^2 - 15X + 3X - 15
$$
$$
= X^3 - 2X^2 - 12X - 15 
\equiv X^3 + 5X^2 + 2X + 6 \pmod{7},
$$
as $-2 \equiv 5 \mod 7$, $-12 \equiv 2 \mod 7$, and $-15 \equiv 6 \mod 7$.  

Thus,
$$
Z_{\Omega}(X) 
\;=\; X^3 + 5X^2 + 2X + 6 \;\;\text{in}\;\mathbb{F}_7.
$$
Indeed, substituting $X \in \{1,3,5\}$ into this cubic yields zero modulo 7.

---

## 2. Multiplicative Subgroup

The multiplicative group of a finite field $\mathbb{F}_p$, denoted $\mathbb{F}_p^\times$, is the set of all *non-zero* elements of the field under multiplication. 

**Lemma:** Every finite subgroup of the multiplicative group of a field is *cyclic*. [Proof reference.](https://math.mit.edu/classes/18.783/2019/LectureNotes3.pdf)

Hence, the multiplicative subgroup $\Omega$ can be written as:
$$
\Omega = \{ 1,\, w,\, w^2,\, \ldots,\, w^{k-1} \},
$$
where $w$ is a generator (also called a *primitive root of unity* when $w^k=1$).

*Example:* In $\mathbb{F}_7$, one nontrivial subgroup is $\{1, 2, 4\}$. We can check:
- $2^2 = 4$, $2^3 = 8 \equiv 1\pmod{7}$, so $\{1,2,4\}$ is closed under multiplication, includes the identity 1, and has inverses within itself.  
- The element $2$ acts as a generator here since powers of $2$ cycle through $\{1,2,4\}$.  
Hence, $\Omega = \{1,2,4\}$ is a cyclic subgroup of $\mathbb{F}_7^\times$ of size 3.

---

## 3. Specialized Case: $ \Omega = \langle w \rangle = \{1, w, w^2, \ldots, w^{k-1}\} $

When $\Omega$ is multiplicative subgroup, 
$$
Z_{\Omega}(X) 
= \prod_{a \in \Omega}(X - a) 
= \prod_{i=0}^{k-1} (X - w^i).
$$

If $w^k = 1$, we get:
$$
Z_{\Omega}(X) = X^k - 1.
$$
This form is far easier to evaluate than the product form.

**Remark**:  
1. Evaluating $X^k - 1$ at a point $r$ can be done in $\mathcal{O}(\log k)$ time via fast exponentiation (“exponentiation by squaring”).  
2. For a general subset $\Omega$ without a known structure, computing $\prod_{a \in \Omega}(r - a)$ is $\mathcal{O}(k)$. If $k$ is large, $\mathcal{O}(k)$ might be impractical.

---

## Conclusions and Usage

By focusing on a *multiplicative cyclic subgroup* of size $k$, we can represent its vanishing polynomial succinctly as $X^k-1$. This form allows:

1. **Fast Evaluation**: $\mathcal{O}(\log k)$ multiplications to compute $r^k$.  
2. **Compact Representation**: A single exponent and subtraction.  

In many cryptographic protocols (including those used in zkSNARKs), this structure is central because it keeps polynomials—and hence proofs—much more efficient. For this reason, subsequent sections **assume**:
$$
\Omega = \{1,\, w,\, w^2,\, \dots,\, w^{k-1}\} \subset \mathbb{F}_p \quad\text{with}\quad w^k = 1.
$$

This choice enables a significant speedup in all the polynomial operations we will discuss.