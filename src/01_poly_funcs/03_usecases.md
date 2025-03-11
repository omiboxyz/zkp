# Zero Polynomial

Consider a nonzero $\ell$-variate polynomial function $f$ of total degree $d$ over $\mathbb{F}_p$. For a randomly chosen point $r \in \mathbb{F}_p^{\ell}$, we have

$$
\Pr[f(r) = 0] \le \frac{d}{|\mathbb{F}_p|}.
$$

For example, if $\mathbb{F}_p$ is such that $|\mathbb{F}_p| \approx 2^{256}$ and the total degree is $2^{20}$, then by the Schwartz-Zippel Lemma,

$$
\Pr[f(r) = 0] \le \frac{2^{20}}{2^{256}} = \frac{1}{2^{236}},
$$

which is an exceedingly small probability.

Consequently, if for a random $r$ we find that $f(r) = 0$, we can conclude—with overwhelming probability—that $f$ is the zero polynomial. Although there is a slight chance of error, it is negligible in practice.


# Equality of Polynomial Functions

Consider two multivariate polynomial functions $f(X)$ and $g(X)$, each having total degree at most $d$. By the Schwartz-Zippel Lemma, if a randomly chosen point $r$ satisfies $f(r) = g(r)$, then with high probability $f(X)$ and $g(X)$ are identical. To see this, define

$$
h(X) = f(X) - g(X).
$$

Then $h(X)$ has degree at most $d$, and if $f(r) = g(r)$, we have $h(r) = 0$. Since a nonzero polynomial of degree at most $d$ vanishes with probability at most $d/|\mathbb{F}|$, it follows that with high probability $h$ must be the zero polynomial. Hence, $f(X) = g(X)$.