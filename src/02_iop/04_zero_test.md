# Zero Test
In the Zero Test, a prover $\mathcal{P}$, who knows a polynomial function 
$$
f(X) \in \mathbb{F}^{(\leq d)}[X],
$$
tries to convince a verifier $\mathcal{V}$, who has oracle access or commitment to $f$ (denoted by $ \boxed{f}$), that
$$
f(a) = 0 \quad \text{for all}\; a \in \Omega,
$$
where $ \Omega \subseteq \mathbb{F}_p $ and $ |\Omega| = k $. (The definition of $ \Omega $ is provided in the previous section.)

---

A naive try by the verifier would be:
1. **Individual Queries**: The verifier queries the oracle for each $ a \in \Omega $. This results in $ \mathcal{O}(k) $ queries and a corresponding verification time of $ \mathcal{O}(k) $.

However, our goal is to achieve a constant number of queries (i.e., $ \mathcal{O}(1) $, independent of $ k $ and $ d $) and logarithmic verification time (i.e., $ \mathcal{O}(\log k) $).


The key observation is that if $f(a) = 0 \  \text{for all}\; a \in \Omega,$
then
$$
f(X) = q(X)\,\cdot Z_{\Omega}(X),
$$
where $ Z_{\Omega}(X) $ is the vanishing polynomial over $ \Omega $. The reasoning is that if $ f(x) = 0 $ for all $ x \in \Omega $, then every element of $ \Omega $ is a root of $ f(X) $, and hence the vanishing polynomial $ Z_{\Omega}(X) $ divides $ f(X) $.

---

### Protocol Overview

![Zero Test Protocol](./diagrams/zero_test.png)

In this protocol, the prover knows the function $ f $ and the verifier has oracle access to $ f $ (in zkSNARKs, where oracles are replaced by function commitments, the verifier sends an input $ x $ to the prover, and the prover responds with $ f(x) $ along with a proof of correct evaluation).

1. The prover computes the polynomial $ q(X) $ such that 
   $$
   f(X) = q(X)\,Z_{\Omega}(X).
   $$
   Since $ f $ is zero on $ \Omega $, $ Z_{\Omega}(X) $ divides $ f(X) $ and such a $ q(X) $ exists. The prover then sends a *commitment* to $ q(X) $ (denoted by $ \boxed{q} $) to the verifier.


2.    The verifier samples a random challenge $r \in \mathbb{F}_p$ (a public-coin protocol) and sends $r$ to the prover.

3. The prover returns $f(r) \  \text{and} \  q(r),$
   along with proofs that these values are consistent with the committed polynomials $ f $ and $ q $. This ensures that the prover cannot lie about the polynomial evaluations.


4. The verifier locally computes $ Z_{\Omega}(r) $ and then checks:
   $$
   f(r) \stackrel{?}{=} q(r)\,Z_{\Omega}(r).
   $$
   If this equality holds, the verifier accepts; otherwise, it rejects.

### Informal Security Proof
- **Completeness**: If the prover follows the protocol honestly and $f(X)$ truly vanishes on $\Omega$, then there is a valid $q(X)$ of degree at most $\deg(f) - \deg(Z) = d - k$ such that $f(X) = q(X)\,Z_{\Omega}(X)$ for all $X$. Hence, for any challenge $r$, $f(r) = q(r)\,Z_{\Omega}(r),$ and the verifier accepts.

- **Soundness**: We show that a malicious prover cannot fool the verifier into accepting unless $f(X)$ actually vanishes on $\Omega$. The main cases are:
   1. We assume the underlying commitment scheme is secure; thus, a malicious prover cannot cheat when revealing $ f(r) $ or $ q(r) $ in Step 3.
   2. Suppose $ f(X) $ does *not* vanish on $ \Omega $. Then, there exists no polynomial $ q(X) $ of degree at most $ d - k $ such that $f(X) = q(X)\,Z_{\Omega}(X).$
   In other words, we can write
   $$
   f(X) \;=\; q(X)\,Z_{\Omega}(X) \;+\; R(X),
   $$
   where $ R(X) $ is a nonzero polynomial. A nonzero polynomial of degree $ \deg(R) $ over $ \mathbb{F}_p $ has at most $ \deg(R) $ roots. Thus, if the verifier picks a random $ r \in \mathbb{F}_p $, the probability that 
   $$
   R(r) = 0 \quad \text{(i.e., } f(r) = q(r)\,Z_{\Omega}(r)\text{)}
   $$
   is at most
   $$
   \frac{\deg(R)}{| \mathbb{F}_p |}.
   $$
   Therefore, except with negligible probability (assuming $ (d-k)/p $ is negligible), the verifier’s check will fail, and the verifier will reject.

---

## Time and Size Complexity
Let $p, d, k$ denote the field size, the degree of $f(X)$, and the size of $\Omega$ (respectively the degree of the vanishing polynomial $Z_\Omega(X)$).

1. **Prover**:  
   - The prover must compute $q(X)$ such that $f(X) = q(X) Z_\Omega(X)$. This can be done in 
     $\mathcal{O}(k\,d)$ via naive polynomial multiplication/division or in 
     $\mathcal{O}(d \log d)$ using the Fast Fourier Transform (FFT).  
   - Additionally, the prover needs to:
     - Commit to $q(X)$.
     - Evaluate both $f(r)$ and $q(r)$ at the random challenge $r$.
     - Generate correct evaluation proofs for $f(r)$ and $q(r)$ in the commitment scheme.

2. **Verifier**:  
   - The verifier computes the vanishing polynomial $Z_\Omega(X)$ in 
     $\mathcal{O}(\log k)$ time (e.g., via exponentiation by squaring for $X^k - 1$).  
   - The verifier checks:
     1. The correctness of the committed evaluations ($f(r)$ and $q(r)$) — this cost depends on the underlying commitment scheme.
     2. One equality check $f(r) \stackrel{?}{=} q(r)\,Z_\Omega(r)$.  
   - In the KZG commitment scheme, both the proof verification and equality check take constant time, independent of $d$ or $p$.

3. **Proof Size**:  
   - The proof consists of:
     1. A commitment to $q(X)$.
     2. The values $f(r)$ and $q(r)$ and the evaluation proofs showing these values match the committed polynomials.  
   - In KZG, all of these elements are of constant size, yielding a proof size that does not grow with $d$