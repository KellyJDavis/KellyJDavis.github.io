---
title: "Gödel's Poetry"
collection: publications
category: manuscripts
permalink: /publication/2025-goedels-poetry
excerpt: 'Formal, automated theorem proving using specialized language models for Lean4 proof generation combined with recursive decomposition of difficult theorems into simpler entailing propositions.'
date: 2025-01-01
venue: 'arXiv Pre-print'
paperurl: 'https://arxiv.org/abs/2512.14252'
citation: 'Kelly Davis. (2025). &quot;Gödel&apos;s Poetry.&quot; <i>arXiv Pre-print</i>.'
---

We introduce a new approach to computer theorem proving, employing specialized language models for Lean4 proof generation combined with recursive decomposition of difficult theorems into simpler entailing propositions. These models are coordinated through a multi-agent architecture that orchestrates autoformalization (if required), proof generation, decomposition, and recursive proof. Without decomposition, we achieve a 90.4% pass rate on miniF2F; with decomposition, this is significantly improved. A key technical contribution is our extension of the Kimina Lean Server with AST parsing capabilities for automated, recursive proof decomposition. The system is available on PyPI as *goedels-poetry* and open-source at [KellyJDavis/goedels-poetry](https://github.com/KellyJDavis/goedels-poetry).
