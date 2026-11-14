# Data, sources, and attribution

This package contains original verification code and a methods-report draft. Its mathematical examples are elementary or established constructions. Re-encoding them is not a new solution of a named open conjecture.

| Artifact | Origin and scope |
| --- | --- |
| The 24 `D4` vectors | Explicit vectors with exactly two coordinates equal to ±1 and the others zero; a standard root-system construction. The package checks this finite list. |
| Four-dimensional kissing optimality | Established mathematical background, attributed to Oleg R. Musin, *The kissing number in four dimensions*, Annals of Mathematics 168 (2008), 1–32; [arXiv:math/0309430v3](https://arxiv.org/abs/math/0309430v3). The package does not reconstruct that upper-bound proof. |
| Integer squares modulo four | Elementary residue argument, proved directly in Lean. No claim of mathematical novelty. |
| Polynomial SOS example | Exact identity `(x-y)^2 + (x+1)^2/3`; a tutorial example also used by [Anaxia](https://github.com/creelie/Anaxia). |
| Domain-mismatch negative control | `x(x-1)` is nonnegative on integers but equals `-1/4` at `x=1/2`; an elementary example. |
| Lean trust and axioms | [Official Lean documentation](https://lean-lang.org/theorem_proving_in_lean4/Axioms-and-Computation/). Actual `#print axioms` output is retained with the validation report. |
| Julia exact rational arithmetic | [Official Julia manual](https://docs.julialang.org/en/v1/manual/complex-and-rational-numbers/). The script uses only standard libraries. |
| Submission preparation | [Preprints.org author instructions](https://www.preprints.org/instructions-for-authors), checked during draft preparation. No posting or acceptance has occurred. |

No arXiv article body, copyrighted paper, proprietary model weight, or scraped private dataset is redistributed. References identify existing results; reference links are not registrations of a new DOI for this package.

The original software and manuscript preparation were assisted by an AI coding assistant. Deep Bhattacharjee must review the mathematical statements, execution records, authorship details, licensing choice, and final manuscript before any submission.
