# Quantitative Evidence Rules

## Hard constraints (never traded away for performance)

Data integrity, absence of leakage, honest out-of-sample evidence, drawdown
compliance, execution fidelity, and live-trading safety are hard constraints.
Profit is an optimisation objective inside them. Never improve an apparent
performance result by weakening an evidence or safety standard.

## Honesty rules

- Never promise profitability or claim a backtest guarantees live results.
- Translate "high accuracy" / "high profitability" into measurable definitions,
  confidence intervals, degradation tolerances, acceptance thresholds, and stop
  conditions for Jacob to approve.
- Report uncertainty and degradation alongside every performance figure.
- A valid research outcome may be "no suitable strategy" or "no suitable
  book". Never force a result to exist.

## Leakage and holdout

- Each data period serves development/selection **or** untouched testing,
  never both. Maintain the data-period ledger
  (`docs/05-research-and-validation/LEAKAGE_AND_HOLDOUT_POLICY.md`).
- A final holdout must be locked, selection-untouched, and tested only after
  the book and pass/fail thresholds are pre-registered.
- If no credible untouched holdout remains, say so and design prospective
  shadow/paper validation. Never relabel touched data as unseen.
- Track every strategy/configuration attempted so multiple-testing risk cannot
  be hidden. Research breadth is part of the evidence.

## Validation standards

- Nested time-aware validation where hyperparameters or features are selected.
- Purging/embargo, walk-forward, regime segmentation, block/bootstrap methods,
  parameter stability, perturbation, and adversarial costs are evaluated per
  the statistical validation plan.
- Multiple-testing corrections (PBO, Deflated Sharpe, Reality Check, SPA) are
  candidates to research, with limitations stated — no single statistic is a
  magic gate.
- Crisis validation uses measured historical episodes; synthetic stresses
  complement, never replace, them. Crisis periods are chosen before seeing
  candidate outcomes.

## Research standard (for every deep-research brief)

1. State the decision the research supports.
2. Define question, scope, exclusions, freshness date, and acceptance standard
   before searching.
3. Prioritise primary/official sources; multiple independent sources for
   consequential claims.
4. Label facts, calculations, inferences, opinions, unknowns, recommendations.
5. Record contradictory evidence and its effect on confidence.
6. Cite material claims close to the claim; retain retrieval metadata.
7. Run a sceptical verification pass that tries to disprove the conclusion.
8. State limitations, gaps, licensing constraints, and what evidence would
   change the recommendation.
9. Jacob approves before research changes any specification, backlog, book,
   live control, or content claim.
