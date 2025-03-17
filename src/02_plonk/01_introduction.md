# Polynomial Interactive Oracle Proof (poly-IOP)
There are three components in a poly-IOP that require explanation. Here, I provide an informal overview; formal definitions should be added later.

1. **Interactive Proof**:  
   An interactive proof is a protocol between a prover and a verifier, where the prover attempts to convince the verifier of a public claim $x$. The protocol features a back-and-forth (or "ping-pong") interaction—messages are exchanged between the prover and the verifier, and at the end of the interaction, the verifier is convinced of the claim.

2. **Polynomial Interactive Proof**:  
   In a polynomial interactive proof, the number of interaction messages is a polynomial function of the size of the claim $x$.

3. **Oracle**:  
   An oracle is a mechanism that allows the verifier to query a property—typically, the output of a function on input $r$—and learn its value.

Overall, a **Polynomial Interactive Oracle Proof (poly-IOP)** refers to a polynomial interactive protocol where the verifier has access to one or more oracles.

In this chapter, we define various claims and present protocols in which the prover convinces the verifier of the correctness of a claim using a poly-IOP framework, with the verifier having access to certain given oracles.

Note that in zkSNARKs, the prover provides oracles to the verifier via function commitment schemes such as KZG or FRI. Therefore, in our discussion, the prover sends oracles to the verifier (in zkSNARKs, the prover sends a commitment to the function), the verifier sends its query to the prover, and the prover provides the oracle output on that input (in zkSNARKs, the prover sends the output of the committed function, together with a proof of correctness).


 In our discussion, the analysis is independent of the underlying commitment scheme, and the reported sizes and times are generic to the commitment scheme used.
