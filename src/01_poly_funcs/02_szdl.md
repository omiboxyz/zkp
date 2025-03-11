# SZDL Lemma

**Theorem**: Let $f(X) \in \mathbb{F}^{(\leq d)}[X]$ be a polynomial of degree at most $d$ over the finite field $\mathbb{F}$. Then $f(X)$ has at most $d$ distinct roots.

**Proof**: This is an informal proof. Assume for the sake of contradiction that $f(X)$ has $d+1$ distinct roots, say $x_1, x_2, \ldots, x_{d+1}$. Then $f(X)$ is divisible by

$$
(X - x_1)(X - x_2) \cdots (X - x_{d+1}),
$$

which is a polynomial of degree $d+1$. This contradicts the assumption that $f(X)$ is of degree at most $d$. Hence, $f(X)$ cannot have more than $d$ distinct roots.

**Lemma**: *Schwartz-Zippel Lemma*: Let $f(X_1, X_2, \ldots, X_{\ell}) \in \mathbb{F}[X_1, X_2, \ldots, X_{\ell}]$ be a nonzero multivariate polynomial with total degree $d$. If the variables $x_1, x_2, \ldots, x_{\ell}$ are chosen uniformly at random from $\mathbb{F}$, then

$$
\Pr[f(x_1, x_2, \ldots, x_{\ell}) = 0] \le \frac{d}{|\mathbb{F}|},
$$

where $|\mathbb{F}|$ denotes the size of the field.

The univariate case follows by setting $\ell = 1$.