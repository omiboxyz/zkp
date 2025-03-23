# Interactive Oracle Proof (IOP)
There are two main components in an IOP that require explanation. Below is an informal overview; formal definitions will appear later.

1. **Interactive Proof**:  
   An *interactive proof* is a protocol between a prover and a verifier, where the prover attempts to convince the verifier of a public claim $x$. This protocol involves back-and-forth (“ping-pong”) exchanges of messages, and at the end, the verifier is convinced of the claim. The number of interactions must be a polynomial function of $\lvert x \rvert$ (the size of $x$).

2. **Oracle**: 
   An *oracle* is a mechanism enabling the verifier to query a function in a “black-box” manner. Specifically, the verifier can ask the oracle for the value of some function $f$ at a chosen input $r$, and the oracle responds with $f(r)$. The verifier learns only these specific outputs and nothing else about $f$.

An **Interactive Oracle Proof (IOP)** is an interactive proof where the verifier has access to one or more such oracles. In the preprocessing part, the:
- **Prover** knows (or can construct) certain functions $f_1, f_2, \dots$.
- **Verifier** initially gains black-box (oracle) access to these functions, denoted $\boxed{f_1}, \boxed{f_2}, \dots$.  


During the protocol:
1. The prover may generate new functions $q, r, \ldots$ on the fly.
2. The prover sends “oracles” (or in zkSNARKs, *commitments*) for these new functions to the verifier.
3. The verifier queries these oracles as needed.

In this chapter, we will describe various IOP protocols under the assumption that the verifier has black-box oracle access. The reported complexities focus on how many queries or checks the verifier makes, without assuming specifics about the underlying commitment scheme. Then, in a zkSNARK context, these oracles get instantiated with cryptographic commitments, and each oracle query becomes an evaluation proof within the scheme.


## IOPs vs. zkSNARKs

In a zkSNARK implementation:

- **Oracles** $\boxed{f}$ become *commitments* to $f$.  
- When the verifier “queries” $f(r)$, the prover provides $f(r)$ *plus a short proof* certifying the correctness of that value.  
- Interaction can sometimes be replaced or minimized (e.g., via Fiat–Shamir transforms) to yield non-interactive proofs in the random oracle model.
