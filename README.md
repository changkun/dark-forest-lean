# dark-forest-lean

Machine-checked claims for the essay
[Dark Forest Theory: A Formal Derivation](https://changkun.de/blog/posts/dark-forest-theory/).

What is checked is the mathematics of the model: its utilities, thresholds,
equilibrium conditions and recurrences. Whether the axioms describe any real
universe is not something a proof assistant can settle.

Every theorem depends only on Lean's standard axioms (`propext`,
`Classical.choice`, `Quot.sound`); none uses `sorry`.

What the proofs do not settle is set out in Section 8.7 of the essay. In
short:

- Beyond any proof: whether the axioms describe any universe; whether each
  Lean statement says what the essay's sentence says (check this by reading
  the statements); the modelling choices built in, such as counting a
  capable civilization as a willing one, two civilizations only, and A2
  never entering the model; the simulation of Section 9; the analogies of
  Section 7.
- Not proved here, though they could be: the general theorems cited, of
  which the file checks the case this model needs (Carlsson and van Damme,
  1993, for this game; Kandori, Mailath and Rob, 1993, for best-reply
  dynamics; grim trigger rather than the Folk theorem); that B1-B5 are
  minimal or independent; that the noisy game has an equilibrium under a
  proper prior; the informal arguments on costly signals and on many
  civilizations.

| Claim in the essay | Theorem |
|---|---|
| Axiom A1: with survival taking two values, the lexicographic order has a real-valued utility | `lex_representable` |
| ... unlike the lexicographic order on pairs of reals, which has none | `lex_real_not_representable` |
| Axiom A1: the additive utility respects the order if other gains are bounded and `M` exceeds twice the bound, and fails for every finite `M` if they are not | `additive_lex_of_bounded`, `additive_not_lex_of_unbounded` |
| Proposition 0 (a): once goodwill is verified, waiting is strictly better than striking, and with no hostile share revealing beats hiding | `prop0_verified`, `prop0_verified_reveal` |
| Proposition 0 (b): an enforcer that destroys violators with probability at least `q²` makes waiting strictly better whatever the other side does | `prop0_enforced` |
| Proposition 0 (c): a strike that never succeeds is strictly worse than waiting | `prop0_no_preemption_when_strikes_fail` |
| Proposition 0 (d): against grim trigger, restraint is a best reply iff `δ ≥ (g - w)/(g - p)`, a threshold below 1; with delay `τ` and discount rate `r`, iff `rτ ≤ log((g - p)/(g - w))` | `grim_sustains`, `restraint_pay`, `grim_threshold_lt_one`, `grim_delay` |
| Section 4.2: the base threat `π = 1 - (1 - p)(1 - γ)` is a probability, positive whenever `γ` is | `basePi_pos` |
| B4 and Section 4.2: with a Gaussian random term every capability level is reached with positive probability, so `γ > 0`; a bounded random term need not reach it | `explosion_possible`, `explosion_needs_reach` |
| Section 8.2: with a random term of mean zero, `γ ≤ σ²/c²`, and the base threat lies between `p` and `p + γ` | `explosion_rare`, `basePi_between` |
| Proposition 1: under B2 the threat believed after any signal is the prior, strictly between 0 and 1 | `prop1_posterior_is_prior`, `prop1_cheap_talk` |
| Proposition 2: the original recurrence has closed form `1 - (1 - π)^(n+1)` and tends to 1 | `linearChain_closed`, `linearChain_tendsto_one` |
| Proposition 2: that recurrence is the case of thresholds spread uniformly over `[0, 1]` | `linear_is_uniform` |
| Proposition 2: identical civilizations, the chain stops at `π` or reaches 1 in one step | `chain_stops`, `chain_unravels` |
| Proposition 2: the chain never passes a resting point | `chain_le_resting_point`, `chain_below_one_of_resting_point` |
| Proposition 3: striking first beats waiting iff `r > 1 - q + K/(qM)` | `prop3_threshold` |
| Proposition 3: as `M` grows, the threshold falls to `1 - q`, not to 0 | `threshold_tendsto` |
| Proposition 3: mutual restraint and mutual striking as equilibria | `wait_equilibrium_iff`, `strike_equilibrium_iff` |
| Proposition 3 and the Theorem: mutual striking is an equilibrium iff `K < q²M`, the only one when `π > r*`, and below that there are exactly the three equilibria of a stag hunt | `threshold_lt_one_iff`, `only_striking`, `stag_hunt_equilibria` |
| Proposition 3: striking is risk-dominant iff `q > (1 - π)/2` | `strike_risk_dominant_iff`, `strike_risk_dominant_iff_q` |
| Proposition 3, global game: with a noisy signal of `q` and a flat prior, in every equilibrium, symmetric or not, both sides strike above `(1 - π)/2` and wait below it, and the threshold strategy is an equilibrium | `global_game_pair`, `global_game_unique`, `threshold_is_equilibrium`, `selected_is_risk_dominant` |
| Proposition 3, global game: two i.i.d. noises that do not tie are each as likely to be the larger, and any atomless noise law gives the beliefs the argument needs | `noise_half`, `flatNoise` |
| Proposition 3, global game: under a uniform prior on an interval, a signal away from its ends carries no information about the noises, so the belief and the posterior mean are the flat prior's | `interior_signal`, `belief_is_conditional`, `posterior_is_signal_minus_noise`, `posterior_mean` |
| Proposition 3, global game: under that prior, with noise of mean zero bounded by `σ`, selection holds at every noise level once the prior extends `2σ` into both dominance regions | `uniform_prior_selects` |
| Proposition 3, global game: beliefs within `η` of the uniform prior's move the switch by at most `(2 - π)η` | `global_game` |
| Proposition 3, global game: under a prior with a density, Bayes' rule gives the posterior law of the noises given one's signal | `joint_law_density`, `signal_law_density`, `conditional_of_density` |
| Proposition 3, global game: if the density is at least `m` and `L`-Lipschitz, beliefs stay within `max(σ, 2Lσ/(m - Lσ))` of the flat prior's, and the switch closes on `(1 - π)/2` as the noise shrinks, whatever its law | `post_near`, `post_mean_near`, `smooth_prior_selects`, `smooth_prior_limit` |
| Proposition 4: hiding beats revealing iff `(λR - λH)(ρD - ρ0)M > B + C` | `prop4_hide_iff` |
| Proposition 4: detection is dangerous as soon as any hostile share exists, and a large `M` then makes hiding better | `rhoD_pos`, `silence_for_large_M` |
| Theorem, backward induction: one `M` makes hiding better whichever equilibrium follows detection | `silence_whatever_follows` |
| Theorem: for identical civilizations, the Dark Forest state holds for all large `M` iff `q > (1 - π)/2` | `dark_forest_state_iff` |
| Theorem, system level: under the replicator dynamics, the share that broadcasts tends to 0 whenever hiding is fitter | `repShare_closed`, `silence_spreads` |
| Theorem, system level: striking is bistable, taking over above an edge and dying out below it | `striking_takes_over`, `striking_dies_out` |
| Theorem, system level: striking has the larger basin exactly when it is risk-dominant | `larger_basin_iff_risk_dominant` |
| Theorem, system level: under best replies with mutation rate `ε`, every stationary distribution gives striking the share `α/(α + β)` of the two tipping chances, and one exists | `kmr_stationary`, `kmr_exists_stationary` |
| Theorem, system level: as mutations become rare, a large population spends almost all its time striking if striking is risk-dominant, and almost none if restraint is | `kmr_limit`, `kmr_limit_zero`, `kmr_selects_risk_dominant`, `kmr_selects_restraint` |

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
