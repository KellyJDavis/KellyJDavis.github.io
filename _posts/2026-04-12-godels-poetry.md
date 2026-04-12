---
title: "Gödel's Poetry: AI, Lean4 Prover"
date: 2026-04-12
permalink: /posts/2026/04/godels-poetry/
tags:
  - automated theorem proving
  - formal verification
  - machine learning
  - Lean
---

[*Gödel's Poetry*](https://arxiv.org/abs/2512.14252) ([PDF](https://arxiv.org/pdf/2512.14252)) is a Lean 4 system that combines specialized language models for *proof generation* with *recursive decomposition* of difficult theorems into *simpler entailing propositions*, coordinated through a *multi-agent architecture* as in the [arXiv manuscript](https://arxiv.org/abs/2512.14252). *Proof verification* runs through the *Kimina Lean Server*; when *direct proof generation* (with *verifier-guided self-correction* in the style of *Goedel-Prover-V2*) does not yield a closed proof, the stack falls back to *RAG-based theorem retrieval*, *proof sketching* with `sorry` placeholders in explicit `have` obligations, *AST-based extraction* of those subgoals, recursive proof of each proposition, and finally *proof reconstruction* that substitutes verified sub-proofs back into the parent sketch.

The [*goedels-poetry*](https://github.com/KellyJDavis/goedels-poetry) repository (PyPI: `goedels-poetry`) remains authoritative for operational detail—supervisor routing, defaults, and harness semantics—while the arXiv PDF records motivation, ablations, and a frozen snapshot of benchmark numbers at submission time.

## Design stance

Many LLM+ATP setups stop at *verifier-guided self-correction*: the prover revises tactics using Lean diagnostics. That matches the direct-proving regime I report at *pass@32* on *miniF2F* without decomposition—*90.4%*, i.e. the same ceiling as Goedel-Prover-V2 under that protocol before the decomposition machinery activates. The additional design bet in Gödel's Poetry is *global* repair when local correction saturates: *RAG-based retrieval* of library facts (following the Hilbert-style pattern discussed in the paper), a *proof sketch* that states *entailing propositions* as named `have` lines closed with `sorry`, *sketch validation* in Kimina, then *AST extraction* so unproven leaves become first-class goals for recursion—not informal text the prover must reinterpret.

Orchestration uses *LangGraph* and *LangChain* as in the manuscript. A *supervisor* (omitted from the published figure for clarity) dispatches work to specialized agents; each role may use a different OpenAI-compatible endpoint.

## Pipeline (aligned with the Methods section)

*Autoformalization (when required).* Informal statements go through: (1) the *formalizer agent*; (2) *syntax validation* against Kimina; (3) *semantic validation*—an LLM-based check that the formal Lean statement preserves the informal problem, with veto power if the translation is wrong.

*Direct proof generation.* The *prover agent* (defaults to *Goedel-Prover-V2*) completes the theorem using *verifier-guided self-correction*: failed attempts return compiler errors to a *corrector agent* until Kimina accepts a proof or *self-correction* / *pass* limits are hit.

*Recursive decomposition (when direct proving fails).* This follows the POETRY-inspired pattern in the paper:

1. *Theorem retrieval:* the *query generation agent* emits natural-language descriptions of lemmas that might help; the *theorem lookup agent* queries a vector index (a *LeanExplore* variant in our deployment) over Mathlib.
2. *Proof sketching:* the *proof sketcher agent* produces a decomposition—high-level structure with named hypotheses and `have` subgoals ending in `sorry`, logically entailing the main statement.
3. *Sketch validation:* the *sketch checker* submits the sketch to Kimina so Lean can confirm syntax, well-formed `have` types, and that the `sorry`-backed obligations actually entail the target.
4. *AST-based extraction:* a *parser agent* requests the sketch’s AST from Kimina (the extended `/api/ast_code` endpoint); the *decomposition agent* traverses that tree to collect unproven `have` leaves and their statements (including context recovered from `sorries` metadata, as described in the paper).
5. *Recursive proving:* each extracted proposition re-enters the full pipeline—*direct proof generation* with fallback to further decomposition—under *depth* and *pass* limits, with *breadth-first* scheduling and *backtracking* to alternative decompositions when children fail validation or exceed depth.
6. *Proof reconstruction:* once subgoals verify, the implementation replaces each `sorry` with the corresponding verified tactic block so the enclosing theorem becomes a single *complete verified proof*—the *AST-based substitution* / reconstruction procedure in the paper’s Methods section.

## Architecture figure

The TikZ figure in the paper (and the PNG in the repo) labels nodes the same way: *Formalization & Validation*, *Proof Generation (Goedel-Prover-V2)*, *Verification (Kimina Lean Server)*, then on failure *Query Generation (Search Agent)*, *Theorem Lookup (Vector DB Agent)*, *Proof Sketch & Decomposition*, *Extract Subgoals (AST Parser)*, subgoal *Prove / Verify / Decompose* loops, and the dashed *Recurse* edge back to proof generation.

![High-level architecture of Gödel's Poetry: target theorem, formalization, proof generation, Kimina verification, and on failure query generation, vector retrieval, sketching, AST-based subgoal extraction, and recursive subgoal loops feeding back to the prover.](https://raw.githubusercontent.com/KellyJDavis/goedels-poetry/main/docs/images/goedels-poetry-architecture.png)

*Illustrative subgoal names denote dependency shape only, not claims about those problems on miniF2F.*

## Evaluation and contribution

*miniF2F* is the formal olympiad-level benchmark cited throughout the paper. *Pass rate* means the fraction of items closed with a machine-checked proof under the *pinned configuration* (commit, endpoints, timeouts, harness flags—see the repository for the executable definition).

Under the manuscript’s configuration: *90.4%* at *pass@32* *without* recursive decomposition (i.e. direct Goedel-Prover-V2-style proving only); *with* decomposition and RAG, the paper reports a significant improvement—re-run the harness after any code change to obtain fresh numbers. The PDF tabulates one frozen run.

The technical contribution emphasized in the paper—and implemented in Kimina—is *AST extraction* from Lean 4 sketches so that decomposition stays programmatic: the *proof sketcher* can propose structure, but *AST-based extraction* and *proof reconstruction* tie that structure to obligations Lean actually accepts.

## Reproducibility

Verification remains on *Kimina*; retrieval uses a *local LeanExplore* backend so indexed Mathlib matches the checker’s workspace. Agent backends are swappable via `config.ini` and `SECTION__OPTION` environment overrides; see `README.md` and `CONFIGURATION.md`.

## References and citation

- **arXiv abstract:** [https://arxiv.org/abs/2512.14252](https://arxiv.org/abs/2512.14252)  
- **PDF:** [https://arxiv.org/pdf/2512.14252](https://arxiv.org/pdf/2512.14252)  
- **Source:** [https://github.com/KellyJDavis/goedels-poetry](https://github.com/KellyJDavis/goedels-poetry)  
- **Documentation:** [https://KellyJDavis.github.io/goedels-poetry/](https://KellyJDavis.github.io/goedels-poetry/)

```bibtex
@misc{davis2025godelspoetry,
      title={G\"odel's Poetry},
      author={Kelly J. Davis},
      year={2025},
      eprint={2512.14252},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2512.14252},
}
```

Limitations and threat models for autoformalization are discussed in the manuscript; routing, retries, env vars, and driver behavior should always be checked against the repository revision you execute.

— Kelly J. Davis
