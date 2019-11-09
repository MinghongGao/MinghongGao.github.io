---
layout: post
title: Cryptograpy - ElGamal Scheme
---
## Problems
1. Discrete Logarithm Problem
2. Computational Diffie Hellman Problem

**Alice:** 
Private Key: $x_A$
Public Key: $(a,q,y_A)$
> Key Generation Step: 
> 
> A primitive element: $a$
> Prime Field:  $GF(q)$
> 1. Select a private key:  $x_A, 1 \le x_A \le q-1$
> 2. Generate a public key:  $y_A, y_A=a^{x_A} \mod  q$

**Bob:**
Alice's Public Key: $y_A$

## Encryption


### Encryption Step - Bob

Message: $M$

1. Select random $k$, where $1 \le k \le q-1$
2. Calculate $K = y_A^k \mod q$
3. $C_1 = a^k \mod q$ 
4. $C_2 = KM$
5. Cipher: $C = (C_1,C_2)$

### Decryption Step - Alice
Cipher text: $C = (C_1,C_2)$
1.  Recoverying key $K =C_1^{x_A}$
2. Calculate $K^{-1}$
3. Recovery Message $M =C_2K^{-1}$

> The importance of uniqueness of k:
> If Adversary knows $M_1$, he can then recover $M_2$ using Known Plaintext Attack
> Recovery Step:
> Attacker knows: 
> $C_1 = (C_{1_A}, C_{1_B})$
> $C_2 = (C_{2_A}, C_{2_B})$
> $M_1$
> Because $M_1 = C_{1_B} K^{-1} \mod q$
> He can recover $K^{-1}$
> Finally, $M_2 = C_2K^{-1}$
## Signature
### Signing Step - Alice

Message: $M$
Hash: $m=H(M), 0 \le m \le (q-1)$

1. Select random $k$, where $1 \le k \le q-1,GCD(k, q-1)=1$
2. Calculate $S_1 = a^k \mod q$
3. Calculate $k^{-1}  \mod q-1$ 
4. Calculate $S_2 = k^{-1} (m-x_AS_1) \mod q-1$
5. Signature: $S = (S_1,S_2)$

### Verification Step- Bob
Signature: $S = (S_1,S_2)$
Hash value of $M$: $m$
1.  $V_1 =a^m \mod q$
2. $V_2 = y_a^{S_1}S_1^{S_2} \mod q$
3. Signature is valid if  $V_1=V_2$
