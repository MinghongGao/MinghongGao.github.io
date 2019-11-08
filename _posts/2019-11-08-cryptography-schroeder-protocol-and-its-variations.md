---
layout: post
title: Cryptography Schroeder Protocol and its Variations
---
## Original

1. A$\to$KDC: $ID_A||ID_B||N_1$
2. KDC$\to$A: $E(K_a, [K_s||ID_B||N_1||E(K_b, [K_s||ID_A])])$
3. A$\to$B: $E(K_b, [K_s||ID_A])$
4. B$\to$A: $E(K_s, N_2)$
5. A$\to$B:$E(K_s, f(N_2))$

## Denning 81 Modification

1. A$\to$KDC: $ID_A||ID_B$
2. KDC$\to$A: $E(K_a, [K_s||ID_B||T||E(K_b, [K_s||ID_A||T])])$
3. A$\to$B: $E(K_b, [K_s||ID_A||T])$
4. B$\to$A: $E(K_s, N_1)$
5. A$\to$B:$E(K_s, f(N_1))$

Suppress Replay Attack

## Neuman 93 Modification

1. A$\to$B: $ID_A||N_a$
2. B$\to$KDC: $ID_B||N_b||E(K_b, [ID_A||N_a||T_b])$
3. KDC$\to$A: $E(K_a, [ID_B||N_a||K_s||T_b]) || E(K_b, [ID_A||K_s||T_b]) || N_b$
4. A$\to$B: $E(K_b, [ID_A||K_s||T_b]) || E(K_s, N_b)$

Solved the Suppress Replay Attack
