# Gadgets
In the subsequent sections, we will define a few claims (gadgets) over the set $\Omega$, with their corresponding poly-IOP protocols where the prover can convince the verifier of the correctness of these claims. These gadgets lie at the heart of zkSNARKs such as the Plonk proof system.

In all of these sections, we assume the **prover** knows the function
$$
f \in \mathbb{F}_p^{(\leq d)}[x],
$$
where $d$ is the maximum degree of the function $f$ and $p$ is a prime number representing the size of the field.

On the other hand, the **verifier** has only oracle access to the function $f$. This means that the verifier can query the oracle at any point $x$ and learn the value $f(x)$. Each query incurs a cost of 1 operation; therefore, for $q$ queries, the runtime complexity is $\mathcal{O}(q).$

In addition, both the prover and the verifier know
$$
Z_{\Omega}(X) = X^k - 1,
$$
which is the vanishing polynomial of the set
$$
\Omega = \{1, w, w^2, \ldots, w^{k-1}\} \subset \mathbb{F}_p,
$$
where $w$ is a primitive $k$th root of unity (i.e., $w^k = 1$).

We use $\boxed{f}$ to represent oracle access to a function $f$. In zkSNARKs, this access is realized through a prover who has committed to $f$ via a commitment scheme. Thus, in what follows, the verifier will send oracle queries to the prover, and the prover will provide the oracle responses to the verifier.

The gadgets we will cover are:
- **Zero Test**
- **Product Check**
- **Permutation Check**
- **Prescribed Permutation Check**

## References
- ZKP MOOC 2023, *L5_Plonk Interactive Oracle Proofs (IOP).pdf*
