# Reproducible Evidence Gates for Local-Model Mathematical Research

**Deep Bhattacharjee**
ORCID: https://orcid.org/0000-0003-0466-750X
Affiliation and corresponding-author contact: to be supplied by the author before submission.

**Working methods/software draft — human review required.** Prepared for possible consideration as a technical note; no submission or acceptance has occurred.

## Abstract

Mathematical research assistants can generate strategies whose claims exceed their evidence. We describe a reproducible software design that records model proposals, exact certificates, and kernel-checked statements. Eight Lean 4.34.1 theorems verify the geometry of a 24-vector `D4` construction and the universal obstruction to writing three as a sum of two integer squares. An independent Julia 1.10.13 replication passed 17 assertions using exact arithmetic. A changed polynomial coefficient and a rational counterexample test preservation of the statement and its domain. We report finite conjecture experiments and local model attempts with their recorded scopes. The evaluation yielded zero new global conjecture closures.

**Keywords:** mathematical software; formal verification; Lean; Julia; exact arithmetic; proof certificates; local language models; reproducibility.

## 1. Motivation and contribution

A mathematical suggestion and a mathematical proof are different artifacts. A model may give a plausible decomposition, infer a false universal claim from a finite sample, or silently change the domain. Repeated attempts do not resolve those problems unless the proposed evidence is checked against a fixed statement.

This methods package accompanies the Anaxia research workbench. Its contribution is the implementation of explicit evidence gates and a compact set of independently inspectable examples. A source record contains a link, identity, and capture context. A model proposal contains public strategy text. An exact checker accepts only supported evidence tied to an unchanged formal statement. A kernel-checked theorem additionally has an explicit logical statement and a retained trust audit. These artifacts have different evidential roles.

The examples are deliberately familiar. Their purpose is to test the boundaries of the software rather than to claim new mathematical discovery. In particular, checking a known `D4` configuration must be distinguished from proving a universal kissing-number upper bound, and from a separate reflexive-polytope descent question sharing the notation `D4`.

## 2. Evidence-gate protocol

The protocol has six stages: discover, formalize, propose, critique, verify, and record. Public metadata and abstracts produce review leads. A researcher reviews the literature and supplies the precise mathematical statement. A local or cloud model can suggest a strategy or a candidate certificate. Critique is recorded as advice; it cannot approve the mathematical status. The appropriate exact checker recomputes evidence against the original domain and coefficients. The result is then stored with source and statement hashes.

For polynomial nonnegativity, the certificate format is a rational weighted sum of squares. The verifier expands every factor and compares the resulting coefficient dictionary with the original polynomial. A changed constant, exponent, or domain is not accepted as a proof of the original task. For a counterexample, exact substitution must violate the original statement at a point in its domain.

For informal research targets, the campaign runner saves bounded public strategies and unresolved proof obligations. It never assigns a global closure status. Relevant source excerpts and previous model notes are treated as untrusted data, and no model-generated code is executed. Local and cloud model access is a configurable assistance layer, separate from the verifier.

Preparation of the software and manuscript used an AI coding assistant for implementation, drafting, and iterative checking. The assistant is not an author. The human author must review the mathematics, execution records, references, disclosures, and final text before submission.

## 3. Exact mathematical artifacts

### 3.1. A finite `D4` configuration

Let `R` be the vectors in `{-1,0,1}^4` with exactly two nonzero coordinates. Choosing two positions and two signs gives `|R| = 6·4 = 24`. The Lean file gives an explicit list and proves that it has length 24 and no duplicates. It also checks

\[
\|v\|^2=2\quad(v\in R),\qquad \|u-v\|^2\geq 2\quad(u\ne v\in R).
\]

A displayed pair attains squared distance two. There are 276 unordered pairs. The independent Julia construction generates the vectors by coordinate positions and signs; its expected exact squared-distance histogram is 96 pairs at 2, 72 at 4, 96 at 6, and 12 at 8.

For the standard Euclidean interpretation, scale the centers to `c = sqrt(2) v`. Each center is at distance two from the origin and distinct centers are at distance at least two. Unit spheres centered there therefore form a 24-sphere kissing configuration around the unit sphere at the origin. The Lean artifact verifies the integer statements underlying this scaling; it does not formalize a real-analytic sphere library.

This construction gives a lower-bound witness. The universal four-dimensional optimality result is established work of Musin [1], not a result of this package. No upper-bound or uniqueness proof is inferred from the finite list.

### 3.2. A universal modular impossibility

For every integer `n`, its square is zero or one modulo four. The Lean theorem `square_mod_four` proves this using the exhaustive possibilities for `n mod 4` and integer multiplication modulo four. Consequently, the sum of two integer squares can have residues zero, one, or two, and cannot equal three:

\[
\forall x,y\in\mathbb Z,\qquad x^2+y^2\ne 3.
\]

The theorem `no_integer_sum_squares_three` is universally quantified. Its validity does not depend on checking a large interval of integers. The Julia script separately enumerates the 16 residue assignments modulo four. A positive control verifies `1^2+1^2=2`. These are elementary existing facts, included to exercise soundness boundaries.

### 3.3. Coefficient equality and a domain control

The polynomial example uses the exact identity

\[
\frac43x^2-2xy+y^2+\frac23x+\frac13
=(x-y)^2+\frac13(x+1)^2.
\]

The Julia script expands the right-hand side using dictionaries of monomials with `Rational{BigInt}` coefficients. It compares coefficient dictionaries and rejects a copy with an altered constant term. This is an algebraic identity check, rather than a floating-point fit.

A second control evaluates `q(x)=x(x-1)` at `x=1/2`, obtaining `-1/4` exactly. Sampling the integer interval from -20 to 20 produces no negative value. The contrast demonstrates why evidence over a specified finite integer domain cannot silently become a proof over the real numbers.

## 4. Implementation and trust audit

The Lean source imports only `Std` under toolchain 4.34.1. The five finite geometric assertions and the positive-control equality are proved by ordinary decision procedures. The two modular statements use congruence rewriting and the `omega` procedure. The file declares no additional axioms and contains no proof placeholders, unsafe declarations, or native-evaluation proof shortcuts.

The actual `#print axioms` output shows no axiom dependencies for six theorems. The two modular theorems depend on the standard Lean principles `propext` and `Quot.sound`. These dependencies are disclosed rather than described as axiom-free. Lean's official documentation explains the role of its standard principles [2].

The Julia implementation uses standard libraries only. Arbitrary-precision integers avoid fixed-width overflow, and exact rational values avoid rounding in the polynomial and counterexample examples [3]. Its assertions remain computational checks, with a different trust boundary from kernel-checked Lean theorems.

The validator records runtime versions, source SHA-256 hashes, exit statuses, theorem names, and axiom dependencies. Logs are retained beside the report. The CI workflow sets up the pinned Lean toolchain and Julia 1.10 and requires both executions to succeed. No model inference is required for these proof-artifact checks.

## 5. Recorded evaluation

Lean 4.34.1 checked eight named theorems locally and on GitHub. Julia 1.10.13 passed all 17 assertions on GitHub. The saved verification record includes runtime versions and source hashes. [Verification run](https://github.com/creelie/Anaxia-Research/actions/runs/43609560559).

The companion Anaxia standard challenge snapshot contains the following exact finite experiments:

| Experiment | Recorded scope | Interpretation |
| --- | --- | --- |
| Collatz | Starting values 1 through 10,000 | Retained trajectories reach 1 within configured budgets. |
| Even Goldbach | 4,999 even values from 4 through 10,000 | Each value has a checked prime-pair witness. |
| Legendre | 500 consecutive-square intervals | A prime witness is checked in each stated interval. |
| Erdős–Straus | 199 values from 2 through 200 | Positive unit-fraction denominators satisfy the exact identity. |
| `D4` construction | 24 vectors and 276 pairs | Exact finite norms and separation. |

These are modest capability tests, not computational records or proofs of the general conjectures. Their companion snapshot reports zero new global conjecture closures. The source data are retained in `reports/companion-challenges.json`; the current workbench is available at [4].

A local llama.cpp CPU smoke test reused existing model weights and successfully exercised model discovery, one proposal, and a two-call reasoning round. The deterministic quadratic baseline had status `exact_sos_verified`; `model_evidence_verified` was false. Thus the working inference connection did not supply an additional accepted certificate. This distinction is preserved in `reports/companion-runtime.json`.

## 6. Limitations and next steps

The package does not prove Hodge, Yang–Mills existence and mass gap, the Riemann hypothesis, or the proposed reflexive-polytope descent bound. It does not establish a new error in an arXiv article. Finite tests, public model suggestions, and a known construction do not meet those proof obligations.

The evaluation is a small reproducibility study. It supplies no controlled comparison across model families or calibrated success-rate estimate. Formalizing an informal statement correctly remains a substantive human task. The manuscript's metadata and declarations require author review.

Future work can add independently validated formalization tasks, stronger certificate formats, adversarial tests, and controlled model comparisons. Every extension should preserve fixed statements, explicit domains, bounded resources, retained failures, and a checkable route from proposed evidence to the claimed conclusion.

## Data and code availability

The [companion repository](https://github.com/creelie/Anaxia-Research) contains Lean and Julia sources, validation scripts, source hashes, logs, and evaluation snapshots. Record the final revision and confirm reader access before submission. `DATA.md` records primary sources and attribution.

## Author declarations

**Author review:** The named author must approve the complete manuscript and supply affiliation and correspondence details.
**AI assistance:** An AI coding assistant assisted implementation and manuscript preparation. Human review and responsibility are required.
**Funding and competing interests:** To be completed by the author; no declaration is invented.
**Publication status:** Local methods/software draft. No external submission, new DOI registration, Zenodo deposit, or GitHub release has been performed.

## References

1. Musin, O. R. *The kissing number in four dimensions*. Annals of Mathematics 168 (2008), 1–32. [arXiv:math/0309430v3](https://arxiv.org/abs/math/0309430v3).
2. Lean project. *Theorem Proving in Lean 4: Axioms and Computation*. [Official documentation](https://lean-lang.org/theorem_proving_in_lean4/Axioms-and-Computation/).
3. Julia project. *The Julia Language: Complex and Rational Numbers*. [Official documentation](https://docs.julialang.org/en/v1/manual/complex-and-rational-numbers/).
4. Bhattacharjee, D. *Anaxia research workbench*. [Source repository](https://github.com/creelie/Anaxia). Final evaluated revision to be recorded before submission.
