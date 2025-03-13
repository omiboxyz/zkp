# SZDL Lemma

**Theorem**: Let \\( f(X) \in \mathbb{F}^{(\leq d)}[X] \\) be a nonzero polynomial of degree at most \\( d \\) over the finite field \\( \mathbb{F} \\). Then \\( f(X) \\) has at most \\( d \\) distinct roots.

**Proof** (Informal): Assume, for contradiction, that \\( f(X) \\) has \\( d+1 \\) distinct roots \\( x_1, x_2, \ldots, x_{d+1} \\). Then \\( f(X) \\) is divisible by

\\[
(X - x_1)(X - x_2)\cdots(X - x_{d+1}),
\\]

which is a polynomial of degree \\( d+1 \\). This contradicts the assumption that \\( f(X) \\) has degree at most \\( d \\). Hence, \\( f(X) \\) cannot have more than \\( d \\) distinct roots.

---

**The Schwartz-Zippel Lemma**: Let \\( f(X_1, X_2, \ldots, X_{\ell}) \in \mathbb{F}[X_1, X_2, \ldots, X_{\ell}] \\) be a nonzero multivariate polynomial with total degree \\( d \\). For values \\( x_1, x_2, \ldots, x_{\ell} \\) chosen uniformly at random from \\( \mathbb{F} \\),

\\[
\Pr\\bigl[f(x_1, x_2, \ldots, x_{\ell}) = 0\\bigr] \le \frac{d}{\\lvert \mathbb{F} \\rvert},
\\]

where \\( \\lvert \mathbb{F} \\rvert \\) denotes the size of the field. The *univariate* case follows by setting \\( \ell = 1 \\).


### Zero Polynomial

Consider a nonzero $\ell$-variate polynomial function $ f(X_1, X_2, \ldots, X_{\ell}) \in \mathbb{F}_{p}^{(\le d)}[X_1, X_2, \ldots, X_{\ell}] $. For a randomly chosen point $r \in \mathbb{F}_p^{\ell}$, we have

$$
\Pr[f(r) = 0] \le \frac{d}{|\mathbb{F}_p|}.
$$

For example, if $\mathbb{F}_p$ is such that $|\mathbb{F}_p| \approx 2^{256}$ and the total degree is $2^{20}$, then by the Schwartz-Zippel Lemma,

$$
\Pr[f(r) = 0] \le \frac{2^{20}}{2^{256}} = \frac{1}{2^{236}},
$$

which is an exceedingly small probability.

Consequently, if for a random $r$ we find that $f(r) = 0$, we can conclude—with overwhelming probability—that $f$ is the zero polynomial. Although there is a slight chance of error, it is negligible in practice.


### Equality of Polynomial Functions

Consider two multivariate polynomial functions $f(X)$ and $g(X)$, each having total degree at most $d$. By the Schwartz-Zippel Lemma, if a randomly chosen point $r$ satisfies $f(r) = g(r)$, then with high probability $f(X)$ and $g(X)$ are identical. To see this, define

$$
h(X) = f(X) - g(X).
$$

Then $h(X)$ has degree at most $d$, and if $f(r) = g(r)$, we have $h(r) = 0$. Since a nonzero polynomial of degree at most $d$ vanishes with probability at most $d/|\mathbb{F}|$, it follows that with high probability $h$ must be the zero polynomial. Hence, $f(X) = g(X)$.

## References

1. https://courses.cs.washington.edu/courses/cse521/17wi/521-lecture-7.pdf