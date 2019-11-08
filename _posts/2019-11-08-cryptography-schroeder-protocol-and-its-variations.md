---
layout: post
title: Cryptography Schroeder Protocol and its Variations
---
## Original
1. A$\to$KDC: $ID_A \parallel ID_B \parallel N_1$
2. KDC$\to$A: $E(K_a, [K_s \parallel ID_B \parallel N_1 \parallel E(K_b, [K_s \parallel ID_A])])$
3. A$\to$B: $E(K_b, [K_s \parallel ID_A])$
4. B$\to$A: $E(K_s, N_2)$
5. A$\to$B:$E(K_s, f(N_2))$

## Denning 81 Modification

1. A$\to$KDC: $ID_A \parallel ID_B$
2. KDC$\to$A: $E(K_a, [K_s \parallel ID_B \parallel T \parallel E(K_b, [K_s \parallel ID_A \parallel T])])$
3. A$\to$B: $E(K_b, [K_s \parallel ID_A \parallel T])$
4. B$\to$A: $E(K_s, N_1)$
5. A$\to$B:$E(K_s, f(N_1))$

Suppress Replay Attack

## Neuman 93 Modification

1. A$\to$B: $ID_A \parallel N_a$
2. B$\to$KDC: $ID_B \parallel N_b \parallel E(K_b, [ID_A \parallel N_a \parallel T_b])$
3. KDC$\to$A: $E(K_a, [ID_B \parallel N_a \parallel K_s \parallel T_b])  \parallel  E(K_b, [ID_A \parallel K_s \parallel T_b])  \parallel  N_b$
4. A$\to$B: $E(K_b, [ID_A \parallel K_s \parallel T_b])  \parallel  E(K_s, N_b)$

Solved the Suppress Replay Attack
