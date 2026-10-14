<!-- solve-problem:a69fd2ec-bbb4-4f98-a0a8-8e0b7cdda2e8 -->
# Does P ≠ NP imply one-way functions?

A [Tangle Solve problem](https://solve.tangle.tools/problems/a69fd2ec-bbb4-4f98-a0a8-8e0b7cdda2e8).

## What is the problem?

Question: Does P ≠ NP imply the existence of one-way functions (OWFs)?

Formal setting. A function f : {0,1}* → {0,1}* is computable in polynomial time. f is a **one-way function** if for every probabilistic polynomial-time (PPT) adversary A, for all sufficiently large n,

Pr[f(A(f(x), 1^n)) ∈ f⁻¹(f(x))] ≤ 1/poly(n) — more standardly, A fails to find a preimage with probability ≥ 1 − negl(n), over x uniform on {0,1}^n and A's coins. This is an **average-case** hardness condition: inversion must fail on random inputs.

The question asks whether the worst-case separation P ≠ NP entails such an f exists. Known equivalences sharpen the target: OWFs exist iff there is no PPT algorithm solving SAT on average with noticeable success (i.e.,AvgP ≠ DistNP in the sense of Impagliazzo's worlds); iff pseudorandom generators exist (HILL); iff computationally secure commitments exist. So the question is precisely: **does worst-case NP-hardness of some language in NP force average-case hardness of some distributional problem?**

Ambiguity note: the census phrase "establish a precise obstruction" opens a second acceptable outcome — proving a relativized/black-box world where P ≠ NP yet OWFs fail to exist (or a natural-proof-style barrier), showing no "black-box" proof can work.

## Why does it matters?

Resolving it either way reshapes cryptography's foundations. A positive answer would base all of modern cryptography on the single central conjecture of complexity theory; a negative answer (P ≠ NP with no OWFs) means "Heuristica": SAT is hard in the worst case but easy on average, so cryptography and much of learning-theoretic hardness collapse despite P ≠ NP. It also decides the weak-vs-strong hardness question underlying derandomization (OWFs ⟹ PRGs ⟹ BPP=P heuristically). Any proof technique that settles it must circumvent known barriers, and thus would likely introduce new non-black-box machinery of independent value.

## What's already known?

- **Impagliazzo's five worlds** (1995) frames the landscape: P ≠ NP is consistent with Heuristica (no OWFs) or Cryptomania; the question is exactly which worlds P ≠ NP alone rules out.
- **Oracle separations**: There is an oracle relative to which P ≠ NP but OWFs do not exist (in an appropriately relativized sense) — attributed to work in the 1990s (verify exact attribution; often cited via Impagliazzo–Rudich-style barrier discussions and Gasarch's surveys). Hence any proof must be non-relativizing.
- **Worst-case→average-case reductions fail generically**: Feigenbaum–Fortnow showed average-case reductions from SAT to itself under non-adaptive random reductions collapse the polynomial hierarchy (verify statement strength); Bogdanov–Trevisan (2006) prove that non-adaptive reductions from NP-hard worst-case problems to average-case problems in NP collapse PH to Σ₃^p. So the naive route — "reduce SAT to inverting f on average" — provably cannot work with standard techniques.
- **Partial positives**: OWFs follow from stronger average-case assumptions, e.g., hardness of specific distributions on SAT (under non-uniform or circuit assumptions), from hardness of specific problems (lattice problems give worst-case→average-case connections, Ajtai 1998; Regev), and OWFs exist iff worst-case hardness of some time-hierarchy-type function exists (Levin's construction from any problem requiring 2^n time on almost all input lengths — this is worst-case hardness of an exponential-time problem, not NP).
- **Lattice caveat**: Ajtai/Regev worst-case-to-average-case results hold for worst-case problems in NP ∩ coNP, not NP-complete ones — consistent with the barriers above.

## What would count as solving it?

Any one of:
1. **Positive**: A proof that P ≠ NP ⟹ OWFs exist, i.e., construct (non-constructively) f from the assumption, or reduce inverting f on average to solving SAT on some input. Must evade the Bogdanov–Trevisan barrier (adaptive reductions, non-relativizing techniques).
2. **Negative**: An oracle world (or algebrization/barrier formalization) where P ≠ NP yet no OWFs exist, **plus** an argument that all "standard" proof techniques relativize — a true barrier theorem, not just one oracle.
3. **Structural**: A proof that the implication is independent of, say, relativizing + naturalizing techniques (analogous to Baker–Gill–Solovov / Aaronson–Wigderson).

A referee accepts: a complete proof of one direction, or a rigorous barrier capturing all known techniques. Partial results (implication under mild extra assumptions like PH not collapsing) are incremental progress, not solutions.

## How to start

1. Read Impagliazzo (1995) for the five-worlds taxonomy; then Bogdanov–Trevisan (2006), which contains the sharpest known barrier on worst-case-to-average-case reductions — internalize exactly why the standard reduction template fails.
2. Study Levin's observation that OWFs ⟺ near-worst-case hardness of some exponential-time computable function; ask what the analogous statement for NP fails to capture — the gap is the crux.
3. Try to weaken Bogdanov–Trevisan: their result covers non-adaptive reductions; adaptive or non-uniform reductions are less understood (some extensions exist — verify current frontier). A proof using adaptive reductions is the most plausible escape hatch.
4. Alternatively, attempt an oracle construction separating "P ≠ NP" from "no OWFs" beyond the known one (e.g., relative to a random oracle plus clever alterations), checking it against known results that OWFs exist relative to random oracles.

Main obstacle: all known techniques are relativizing; the required proof must break this.

## Key references

- R. Impagliazzo, "A Personal View of Average-Case Complexity," 1995 (Structures in Complexity Theory). Taxonomy of five worlds; positions the OWF question as Heuristica-vs-Cryptomania. https://ieeexplore.ieee.org/document/514853
- O. Goldreich, *Foundations of Cryptography, Vol. I*, 2001, Ch. 2. Definitions of OWFs and the full equivalence web (OWFs ⟺ PRGs ⟺ commitments). https://www.wisdom.weizmann.ac.il/~oded/foc-vol1.html
- A. Bogdanov, L. Trevisan, "On Worst-Case to Average-Case Reductions for NP Problems," FOCS 2006 / SIAM J. Comput. Proves non-adaptive reductions from NP-hard problems to average-case NP problems collapse PH — the central barrier. https://arxiv.org/abs/cs/0506063
- J. Håstad, R. Impagliazzo, L. Levin, M. Luby, "A Pseudorandom Generator from any One-Way Function," SIAM J. Comput., 1999. The HILL theorem: OWF ⟺ PRG, formalizing what a positive answer would yield.
- M. Ajtai, "Generating Hard Instances of Lattice Problems," STOC 1998. Worst-case-to-average-case connection for lattices — the known positive template, but for NP ∩ coNP, not NP-complete. (verify link) https://dl.acm.org/doi/10.1145/276698.276705

## Warnings

- The oracle separation "P ≠ NP but no OWFs" is folklore-adjacent; verify its exact provenance before citing — several claimed versions differ in how OWFs relativize.
- Do not conflate "no OWFs" with "P = NP": the gap between them is exactly Heuristica vs Algorithmica, and conflating them is the most common error in attempted proofs.
- Any proof reducing SAT to average-case inversion must handle Bogdanov–Trevisan: check early whether your reduction is non-adaptive.
- "OWF exists iff some function is hard on average for polynomial time" is true but vacuous unless the hardness assumption is weaker than what you're trying to prove.

---
*`ALGO-000199` · flagged for review*

## Acceptance guidance

Any one of:
1. **Positive**: A proof that P ≠ NP ⟹ OWFs exist, i.e., construct (non-constructively) f from the assumption, or reduce inverting f on average to solving SAT on some input. Must evade the Bogdanov–Trevisan barrier (adaptive reductions, non-relativizing techniques).
2. **Negative**: An oracle world (or algebrization/barrier formalization) where P ≠ NP yet no OWFs exist, **plus** an argument that all "standard" proof techniques relativize — a true barrier theorem, not just one oracle.
3. **Structural**: A proof that the implication is independent of, say, relativizing + naturalizing techniques (analogous to Baker–Gill–Solovov / Aaronson–Wigderson).

A referee accepts: a complete proof of one direction, or a rigorous barrier capturing all known techniques. Partial results (implication under mild extra assumptions like PH not collapsing) are incremental progress, not solutions.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/a69fd2ec-bbb4-4f98-a0a8-8e0b7cdda2e8?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000199.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000199)
