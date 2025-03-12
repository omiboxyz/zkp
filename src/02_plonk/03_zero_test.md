# Zero Test

Assume a prover $P$ wants to prove to a verifier $V$ that 
$$
f(a) = 0 \quad \text{for all}\; a \in \Omega,
$$
and the verifier already holds a commitment $\text{com}_f$ to the polynomial $f$.
Let $\Omega \subset \mathbb{F}_p$ be a subset of size $|\Omega| = k$, and assume $\deg(f) \le d$.

The naive approaches for the verifier are:
1. The verifier directly evaluates $f$ on every point in $\Omega$ and checks if each evaluation is zero. 
   This requires $\mathcal{O}(k)$ polynomial evaluations, which is inefficient for large $k$.
2. The verifier queries the prover to prove correctness of $f(a)=0$ for each $a \in \Omega$. 
   This yields $\mathcal{O}(k)$ individual proofs, also inefficient.

By using an Interactive Oracle Proof (IOP) and a vanishing polynomial, we can reduce the complexity significantly. 
The key observation is:
$$
\text{If } f(a) = 0 \;\text{for all}\; a \in \Omega, 
\quad \text{then} \quad 
f(X) = q(X)\cdot Z_{\Omega}(X),
$$
where $Z_{\Omega}(X)$ is the vanishing polynomial over $\Omega$. 

### Protocol Overview

1. **Compute and Commit to $q$**:  
   The prover computes the polynomial $q(X)$ such that $f(X) = q(X)\,Z_{\Omega}(X)$. 
   Since $\deg(f) \le d$, we have $\deg(q) \le d$. 
   The prover sends a *commitment* to $q$ (denoted $\text{com}_q$) to the verifier.

2. **Random Challenge**:  
   The verifier samples a random challenge $r \in \mathbb{F}_p$ (public-coin protocol). 
   The verifier sends $r$ to the prover.

3. **Opening the Commitments**:  
   The prover returns:
   $$
   f(r), \quad q(r),
   $$
   along with proofs (in the polynomial commitment scheme) that these openings are consistent with the committed polynomials $f$ and $q$. 
   This ensures the prover cannot lie about the polynomial values.

4. **Check the Factorization**:  
   The verifier locally computes $Z_{\Omega}(r)$. 
   Then it checks the relation
   $$
   f(r) \stackrel{?}{=} q(r)\cdot Z_{\Omega}(r).
   $$
   If this holds, the verifier accepts; otherwise, it rejects.

**Proof (Informal Security Argument)**:  
If $f(X)$ truly vanishes on $\Omega$, then there is a valid $q(X)$ of degree at most $d$, and the relation $f(r) = q(r)\,Z_{\Omega}(r)$ holds for all $r$. The verifier accepts.

Conversely, define
$$
h(X) \;=\; f(X)\;-\;q(X)\,Z_{\Omega}(X).
$$
If $f(X)$ does *not* vanish on $\Omega$, then no polynomial $q(X)$ of degree at most $d$ can satisfy $f(X) = q(X)\,Z_{\Omega}(X)$. 
Consequently, $h(X)$ is a nonzero polynomial. 
A nonzero polynomial of degree $\deg(h)$ over $\mathbb{F}_p$ can have at most $\deg(h)$ roots. 
Hence, when the verifier selects a random $r\in \mathbb{F}_p$, the probability that $h(r) = 0$ is at most $\deg(h)/|\mathbb{F}_p|$. 
Therefore, except with negligible probability, the verifier's check
$$
f(r) \stackrel{?}{=} q(r)\,Z_{\Omega}(r)
$$
will fail, and the verifier will reject.

## References
<!-- List your references here -->
