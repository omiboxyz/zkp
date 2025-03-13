# Proof Gadgets

In this section, we assume the existence of a polynomial commitment scheme. We then demonstrate how to prove specific properties of a polynomial function \\( f(X) \\) ove a designated set $\Omega$. Our approach ensures that the proof size remains constant relative to the proof size of the underlying commitment scheme. Additionally, the verification time is logarithmic in the size of the subset $\Omega$ from the filed.

For a polynomial function \\( f(X) \\), we use $ com_f $ to denote a commitment to \\( f \\) in the commitment scheme, and $\pi_{f, u, v}$ to denote the corresponding proof that \\( f(u) = v \\) in the commitment scheme.


The gadgets we will cover are:
- **Zero Test**
- **Product Check**
- **Permutation Check**
- **Prescribed Permutation Check**

## References
- ZKP MOOC 2023, *L5_Plonk Interactive Oracle Proofs (IOP).pdf*
