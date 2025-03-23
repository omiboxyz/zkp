# Polynomial Functions

**Definition**: A *polynomial function* $f$ of degree $d$ is a function of the form

$$
f(X) = c_0 + c_1 X + c_2 X^2 + \cdots + c_d X^d,
$$

where $c_d \neq 0 $. Each $c_i X^i$ is called a term or monomial.

**Example**: The function \\(f(X) = X^9 + 10X^6 + 3\\) is a polynomial function of degree 9.

**Definition (Zero Polynomial)**: A polynomial function \\(f\\) is called the *zero polynomial* if \\(f(x) = 0\\) for *all* inputs \\(x\\). Otherwise, \\(f\\) is a *non-zero polynomial*.

**Definition (Root)**: A value \\(x\\) is a *root* of a non-zero polynomial function \\(f\\) if \\(f(x) = 0\\). If \\(f\\) has degree \\(d\\), it has at most \\(d\\) *distinct* roots. 

However, note that some roots may be repeated. For example, in \\(f(X) = (X - 1)^2,\\) the degree is 2, but the only root is \\(x = 1\\).

## Polynomial Representation
There are two primary ways to represent a polynomial function \\(f(X)\\) of degree \\(d\\):
1. **Coefficients**: A degree \\(d\\) polynomial function can be represented uniquely by its \\(d+1\\) coefficients. For example, \\(f(X) = c_0 + c_1 X + c_2 X^2 + \cdots + c_d X^d.\\)
2. **Points**: A polynomial function of degree \\(d\\) can also be represented uniquely by \\(d+1\\) distinct points. For example, the set of points \\((0, -1), (2, 3), (-3, 8)\\) determines \\(f(X) = X^2 - 1\\) quadratic polynomial.

Converting from the coefficient-based representation to point values is straightforward. Conversely, one can recover the coefficients from the point-based representation via *polynomial interpolation*. A well-known method is *Lagrange interpolation*, which finds a degree-\\(d\\) polynomial passing through \\(d+1\\) points (see [1]). The naive approach has time complexity \\(\mathrm{O}(d^2)\\), but using the *Fast Fourier Transform (FFT)* can reduce this to \\(\mathrm{O}(d \log d)\\) [1].

## Factorization-Based Representation
Polynomials can also be represented by factoring out known roots. Consider a polynomial function \\(f(X)\\) of degree \\(d\\) that has \\(d'\\) *distinct* roots, denoted \\(x_1, x_2, \ldots, x_{d'}\\), where \\(0 \le d' \le d\\). Then there exists a polynomial function \\(q(X)\\) of degree \\(m = d - d'\\) such that
$$f(X) = q(X)\,(X - x_1)\,(X - x_2)\,\dots\,(X - x_{d'}).$$

If these roots \\(x_1, \ldots, x_{d'}\\) are known, one can compute \\(q(X)\\) by dividing \\(f(X)\\) by \\(\prod_{i=1}^{d'} (X - x_i)\\). A naive implementation of polynomial long division for each root yields \\(\mathrm{O}(d \cdot d')\\) complexity. However, more efficient methods (e.g., using FFT-based multiplication) can perform each division in \\(\mathrm{O}(d \log d')\\) time, potentially reducing the overall cost [1].  


## Polynomial Functions in Finite Fileds
A polynomial function $f(X) \in \mathbb{F}^{(\leq d)}[X]$ is said to be of degree at most $d$, where the coefficients are taken from the finite field $\mathbb{F}$.

In such a polynomial, all arithmetic operations—such as addition and multiplication—are performed in $\mathbb{F}$. For example, to compute the expression $c_0 + c_2 X^2$, one first computes $X^2 = X \cdot X$ in $\mathbb{F}$, then multiplies by $c_2$, and finally adds $c_0$, with each operation carried out in $\mathbb{F}$.

**Remark**: Polynomials that have no roots in the real numbers may possess roots in a finite field, and conversely, polynomials that have real roots may have no roots in a finite field [2].

## Multivariate Polynomial Functions

**Definition**: A *multivariate polynomial function* $f(X_1, X_2, \ldots, X_n)$ is a polynomial function in more than one variable. A polynomial function in a single variable is called *univariate*.

In a multivariate polynomial function with $\ell$ variables, each term (monomial) has the form

$$
c \, X_1^{d_1} X_2^{d_2} \cdots X_{\ell}^{d_{\ell}},
$$

and its degree is given by $d_1 + d_2 + \cdots + d_{\ell}$. The *total degree* of the polynomial is the maximum degree among all its monomials. Multivariate polynomial functions over a field $\mathbb{F}$ are commonly denoted either as $f(x_1, x_2, \ldots, x_{\ell})$, with each $x_i \in \mathbb{F}$, or as $f(x)$ where $x \in \mathbb{F}^{\ell}$.

## References

1. von zur Gathen, J., and Gerhard, J. **Modern Computer Algebra** (3rd ed.). Cambridge University Press, 2013.
2. https://www.rareskills.io/post/finite-fields