# Gadgets
In the subsequent sections, we define a few **claims**—referred to as *gadgets*—over the multiplicative subgroup $\Omega$. Each gadget comes with its own **Interactive Oracle Proof (IOP)** protocol, enabling a prover to convince a verifier of the claim's correctness efficiently. These gadgets lie at the heart of zkSNARK systems such as the Plonk proof framework.

---

## Overview

1. The prover knows some set of functions
   $f_1, f_2, \dots$
   (e.g., polynomials over $\mathbb{F}_p$).

2. The verifier has *oracle access* to these functions, denoted by
   $\boxed{f_1}, \boxed{f_2}, \dots$
   meaning the verifier can query $f_i(r)$ for any input $r\in \mathbb{F}_p$ and learn exactly $f_i(r)$. Each query costs 1 operation, so $\mathcal{O}(q)$ queries means $\mathcal{O}(q)$ time.

3. During the protocol, the prover may compute new functions $q_1,  q_2, \dots$ and *send oracles* (in zkSNARK terms, “commitments”) for these functions to the verifier. The verifier can then query $\boxed{q_i}$ as needed.

4. Both parties know a multiplicative subgroup
   $$
   \Omega = \{1, w, w^2, \ldots, w^{k-1}\} \;\subset\; \mathbb{F}_p,
   $$
   where $w^k = 1$. This subgroup has a *vanishing polynomial*:
   $$
   Z_{\Omega}(X) \;=\; X^k - 1.
   $$

---

## What Are “Gadgets”?

A *gadget* is simply a structured claim (or property) about one or more functions over $\Omega$. The prover wants to convince the verifier that the claim holds, with minimal query and computational costs. Examples include:

- **Zero Test**: Proving $f(a) = 0$ for all $a \in \Omega$.
- **Product Check**: Proving $\prod_{a \in \Omega} f(a) = 1$.
- **Permutation Check**: Proving two functions’ images $\{f(a)\}$ and $\{g(a)\}$ over $\Omega$ are permutations of each other.
- **Prescribed Permutation Check**: Proving $f(a) = g(\sigma(a))$ for a known permutation $\sigma$.

Each of these properties has a specialized protocol that leverages **oracle queries** and the **vanishing polynomial** $Z_{\Omega}$ to keep proofs succinct and the verifier’s workload low (often $\mathcal{O}(\log k)$ or $\mathcal{O}(1)$ queries).

We will see how each protocol ensures:

- **Completeness**: If the prover is honest and the claim is correct, the verifier accepts the claim with certainty.
- **Soundness**: A dishonest prover attempting to prove an incorrect claim cannot convince the verifier, except with negligible probability. More precisely, the cheating prover’s success probability is so small that, with very high confidence, the verifier rejects the false claim.
- **Low Query Complexity**: The verifier requires only a constant number of oracle queries (independent of the polynomial’s degree and the size of $\Omega$) and operates with logarithmic runtime, specifically $\mathcal{O}(\log |\Omega|)$, independent of the polynomial’s degree.

## References
- ZKP MOOC 2023, *L5_Plonk Interactive Oracle Proofs (IOP).pdf*
