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

Intuitively, consider \\( f(X) \in \mathbb{F}[X] \\) of degree \\( d \\). Since \\( f \\) can have at most \\( d \\) distinct roots, the probability that a random point \\( x \\in \mathbb{F} \\) makes \\( f(x) = 0 \\) is at most \\( d / \\lvert \mathbb{F} \\rvert \\). For very large \\( \\lvert \mathbb{F} \\rvert \\) (e.g., \\( 2^{256} \\)) and relatively small \\( d \\) (e.g., \\( 2^{30} \\)), this probability (\\( 2^{-226} \\) in the example) is negligible.

Therefore, if \\( f(X) \\) evaluates to 0 at a random point, we can conclude with high probability that \\( f(X) \\) is the zero polynomial, and we can safely ignore the small chance of error in our decision.