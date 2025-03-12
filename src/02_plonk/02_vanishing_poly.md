# Vanishing Polynomial

Let $\mathbb{F}_p$ be a field of large prime order $p$, and let $\Omega \subseteq \mathbb{F}_p$ be a subset with $|\Omega| = k$.  
In the following sections, we define efficient polynomial IOPs (Interactive Oracle Proofs) for various tasks over $\Omega$. 

**Remark**: Using a specific subset $\Omega$ rather than the entire field $\mathbb{F}_p$ allows us to work with a manageable set of evaluation points. If the entire field were used, the corresponding vanishing polynomial would have degree $p$, which is impractical for computation.

**Definition (Vanishing Polynomial)**: The *vanishing polynomial* of $\Omega$, denoted by $Z_{\Omega}(X)$, is the unique polynomial that evaluates to zero at every point in $\Omega$. Thus, we have

$$
Z_{\Omega}(X) = \prod_{a \in \Omega} (X - a),
$$

which implies that the degree of $Z_{\Omega}(X)$ is $|\Omega|$.

For the specific case where $w$ is a primitive $k$th root of unity (i.e., $w^k = 1$) and 

$$
\Omega = \{1, w, w^2, \ldots, w^{k-1}\} \subset \mathbb{F}_p,
$$

the vanishing polynomial simplifies to

$$
Z_{\Omega}(X) = X^k - 1.
$$

**Remark**: In the case where $\Omega = \{1, w, w^2, \ldots, w^{k-1}\}$, the vanishing polynomial can be evaluated efficiently using exponentiation by squaring, which requires approximately $\log_2 k$ multiplications; when counting both squaring and multiplication steps, the total comes to roughly $2\log k$ operations. In contrast, for a general subset $\Omega$, directly computing

$$
Z_{\Omega}(X) = \prod_{a \in \Omega} (X - a)
$$

would require $k-1$ multiplications, making it much less efficient for large $k$.

This significant speedup is why, in the subsequent sections, we restrict ourselves to the case

$$
\Omega = \{1, w, w^2, \ldots, w^{k-1}\}.
$$

## References
<!-- List your references here -->
