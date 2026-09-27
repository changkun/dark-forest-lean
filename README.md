# dark-forest-lean

Machine-checked claims for the essay
[Dark Forest Theory: A Formal Derivation](https://changkun.de/blog/posts/dark-forest-theory/).

What is checked is the mathematics of the model: its utilities, thresholds,
equilibrium conditions and recurrences. Whether the axioms describe any real
universe is not something a proof assistant can settle.

Every theorem depends only on Lean's standard axioms (`propext`,
`Classical.choice`, `Quot.sound`); none uses `sorry`.

Not checked: the informal cases of Proposition 0; the general
equilibrium-selection theorem of Carlsson and van Damme (1993), for
asymmetric equilibria and other priors, of which the file checks the
symmetric, uniform-prior version for this game (the step from a uniform
prior to the one-half belief is assumed, and the underlying fact about
i.i.d. noise is proved); and the long-run selection result of Kandori,
Mailath and Rob (1993), which the essay cites alongside the replicator
theorems.

| Claim in the essay | Theorem |
|---|---|
| Axiom A1: with survival taking two values, the lexicographic order has a real-valued utility | `lex_representable` |
| ... unlike the lexicographic order on pairs of reals, which has none | `lex_real_not_representable` |
| Axiom A1: the additive utility respects the order if other gains are bounded and `M` exceeds twice the bound, and fails for every finite `M` if they are not | `additive_lex_of_bounded`, `additive_not_lex_of_unbounded` |
| Proposition 0 (c): a strike that never succeeds is strictly worse than waiting | `prop0_no_preemption_when_strikes_fail` |
| Section 4.2: the base threat `π = 1 - (1 - p)(1 - γ)` is a probability, positive whenever `γ` is | `basePi_pos` |
| Proposition 1: under B2 the threat believed after any signal is the prior, strictly between 0 and 1 | `prop1_posterior_is_prior`, `prop1_cheap_talk` |
| Proposition 2: the original recurrence has closed form `1 - (1 - π)^(n+1)` and tends to 1 | `linearChain_closed`, `linearChain_tendsto_one` |
| Proposition 2: that recurrence is the case of thresholds spread uniformly over `[0, 1]` | `linear_is_uniform` |
| Proposition 2: identical civilizations, the chain stops at `π` or reaches 1 in one step | `chain_stops`, `chain_unravels` |
| Proposition 2: the chain never passes a resting point | `chain_le_resting_point`, `chain_below_one_of_resting_point` |
| Proposition 3: striking first beats waiting iff `r > 1 - q + K/(qM)` | `prop3_threshold` |
| Proposition 3: as `M` grows, the threshold falls to `1 - q`, not to 0 | `threshold_tendsto` |
| Proposition 3: mutual restraint and mutual striking as equilibria | `wait_equilibrium_iff`, `strike_equilibrium_iff` |
| Proposition 3: striking is risk-dominant iff `q > (1 - π)/2` | `strike_risk_dominant_iff`, `strike_risk_dominant_iff_q` |
| Proposition 3, global game: with a noisy signal of `q`, every symmetric equilibrium strikes exactly above `(1 - π)/2`, and that threshold is an equilibrium | `global_game_unique`, `threshold_is_equilibrium`, `selected_is_risk_dominant` |
| Proposition 3, global game: two i.i.d. noises that do not tie are each as likely to be the larger, the one-half belief at the threshold | `noise_half` |
| Proposition 4: hiding beats revealing iff `(λR - λH)(ρD - ρ0)M > B + C` | `prop4_hide_iff` |
| Proposition 4: detection is dangerous as soon as any hostile share exists, and a large `M` then makes hiding better | `rhoD_pos`, `silence_for_large_M` |
| Theorem, system level: under the replicator dynamics, the share that broadcasts tends to 0 whenever hiding is fitter | `repShare_closed`, `silence_spreads` |
| Theorem, system level: striking is bistable, taking over above an edge and dying out below it | `striking_takes_over`, `striking_dies_out` |
| Theorem, system level: striking has the larger basin exactly when it is risk-dominant | `larger_basin_iff_risk_dominant` |

## Checking it

With [elan](https://github.com/leanprover/elan) installed:

```sh
lake exe cache get   # fetch Mathlib's prebuilt files
lake build
```

To see the axioms a theorem rests on, add `#print axioms DarkForest.prop3_threshold`
(or any other name) to the end of `DarkForest.lean` and build again.

Built with Lean `v4.35.0-rc3` and Mathlib at commit
`c55e6e786f49471c72fbddbec5415808896aec1e`, as pinned in `lake-manifest.json`.
