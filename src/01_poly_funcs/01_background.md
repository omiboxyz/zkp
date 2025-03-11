# Polynomial Functions

**Definition**: A *polynomial function* $f$ of degree $d$ is a function of the form

$$
f(X) = c_0 + c_1 X + c_2 X^2 + \cdots + c_d X^d,
$$

where $c_d \neq 0 $. Each $c_i X^i$ is called a term or monomial.

A polynomial function $f(X) \in \mathbb{F}^{(\leq d)}[X]$ is said to be of degree at most $d$, where the coefficients are taken from the finite field $\mathbb{F}$.

In such a polynomial, all arithmetic operations—such as addition and multiplication—are performed in $\mathbb{F}$. For example, to compute the expression $c_0 + c_2 X^2$, one first computes $X^2 = X \cdot X$ in $\mathbb{F}$, then multiplies by $c_2$, and finally adds $c_0$, with each operation carried out in $\mathbb{F}$.

**Remark**: Polynomials that have no roots in the real numbers may possess roots in a finite field, and conversely, polynomials that have real roots may have no roots in a finite field [rareskills_finitefields].

# Multivariate Polynomial Functions

**Definition**: A *multivariate polynomial function* $f(X_1, X_2, \ldots, X_n)$ is a polynomial function in more than one variable. A polynomial function in a single variable is called *univariate*.

In a multivariate polynomial function with $\ell$ variables, each term (monomial) has the form

$$
c \, X_1^{d_1} X_2^{d_2} \cdots X_{\ell}^{d_{\ell}},
$$

and its degree is given by $d_1 + d_2 + \cdots + d_{\ell}$. The *total degree* of the polynomial is the maximum degree among all its monomials. Multivariate polynomial functions over a field $\mathbb{F}$ are commonly denoted either as $f(x_1, x_2, \ldots, x_{\ell})$, with each $x_i \in \mathbb{F}$, or as $f(x)$ where $x \in \mathbb{F}^{\ell}$.

**Definition**: In a polynomial function $f(X)$, an element $x$ is called a *root* (or *zero*) of $f$ if $f(x) = 0$.