# The Lame-Duck's Revenge
**An experimental study of end-of-career policy sabotage**

> Why do politicians late in their careers make costly, seemingly retaliatory decisions that carry no strategic or financial benefit? This project tests a behavioral explanation: that spiteful social preferences are *state-dependent* — activated by *how* a person loses a position of power.

> **Status:** research prototype / work in progress. This repository implements an incentivized [oTree](https://www.otree.org/) experiment and its supporting design. The design is documented below; see [Project status & roadmap](#project-status--roadmap) for what is currently built versus planned.

---

## Overview

Standard political-economy models explain end-of-career "defections" as strategic moves to constrain a successor — for example, running up debt to limit a rival's fiscal space (Alesina & Tabellini, 1990; Persson & Svensson, 1989). They do not account for decisions that are *purely retaliatory*: costly to the actor, damaging to their own standing, and offering no strategic upside.

This project proposes and tests an alternative: the event that ends an agent's career changes their social preferences. Being **voted out by peers** ("betrayal") may activate spite in a way that reaching an **exogenous term limit** does not. The central research question:

> *Does the nature of an agent's exit from a privileged position — an endogenous "betrayal" versus an exogenous "term limit" — causally affect their willingness to pay a personal cost to sabotage their successors?*

The design isolates this by holding the *outcome* (the career ends) fixed while varying the *cause*, so that any choice to pay-to-harm can be attributed to a non-pecuniary, behavioral preference rather than to strategy.

## Theoretical framework

A removed or term-limited "Representative" who finished Stage 1 with earnings `E` makes a one-time terminal choice `a` from `{Harm, Help, Neutral}`. Utility combines the monetary payoff with a psychological payoff:

```
U(Neutral)    = E
U(Help)       = (E − Y) + α
U(Harm | k)   = (E − Y) + S_k
```

where `Y > 0` is the fixed personal cost of acting, `α ≥ 0` is an altruism ("warm-glow") parameter, and `S_k ≥ 0` is a **state-dependent spite** parameter that depends on *how* the career ended (state `k`). A purely self-interested agent always chooses Neutral; an agent chooses **Harm** if and only if `S_k > Y` **and** `S_k > α`.

Four terminal states define the spite parameters the design aims to measure:

| State `k` | Parameter | Triggered by |
|---|---|---|
| Betrayal | `S_B` | Voted out by peers (Treatment 3) |
| Indefinite term limit | `S_I` | Exogenous end, indefinite horizon (Treatment 5) — *baseline* |
| Survivor term limit | `S_S` | Survived accountability to a finite limit (Treatment 4) |
| No-vote term limit | `S_NV` | Reached the limit without ever facing a vote (Treatment 2) |

## Experimental design

**Stage 1 — Performance & Election.** The Representative completes a real-effort object-identification task (a visual-search paradigm in the spirit of Gneezy, Leonard & List, 2013). They earn a fixed salary for each round they survive; the Voters' shared pot grows with the Representative's performance. After each round, Voters privately and anonymously vote to retain or replace the Representative. All earnings and vote tallies are common knowledge, and the two sides cannot communicate across the Representative–Voter divide.

**Stage 2 — The Retaliation Decision.** When a career ends — by removal or by reaching a term limit — the Representative makes a one-time, private choice:

- **Harm** (red) — pay 50 tokens to reduce the Voters' pool by 50%
- **Help** (green) — pay 50 tokens to increase the Voters' pool by 50%
- **Neutral** (grey) — do nothing (the self-interested choice)

This is a costly-punishment / "joy of destruction" mechanism (Fehr & Gächter, 2000; Zizzo & Oswald, 2001): only a non-pecuniary preference can rationalize the red or green button.

## Treatments

| # | Name | Setup | Purpose |
|---|---|---|---|
| 1 | Principal-Agent Control | 1 Representative + 1 Voter | Effect of monitoring / group size on effort |
| 2 | No-Vote Term | 3 non-voting Voters, 3 rounds; Stage 2 at round 3 | Sabotage in the absence of accountability |
| 3 | **Betrayal** *(baseline)* | 1 Rep + 3 Voters; Stage 2 only if voted out | Spite from social rejection |
| 4 | Term Limit | Voting + replacement; Stage 2 at the finite limit; ends after the 20th rep-round | Finite-horizon baseline |
| 5 | Indefinite Horizon | Probabilistic stopping (≈80% continue / 20% end per round) | Spite from an exogenous career end |

## Hypotheses

1. **Activation of costly sabotage** — a non-trivial share choose Harm under Betrayal (T3) and under Indefinite Horizon (T5).
2. **The "Betrayal Effect"** — sabotage is higher under Betrayal than Indefinite (`S_B > S_I`).
3. **The "Survivor Effect"** — surviving accountability shifts sabotage (T4 vs T5).
4. **The Accountability Effect** — never facing a vote shifts sabotage (T2 vs T5).
5. **Group size & effort** — Representative effort is higher with one Voter (T1) than with three (T3).

## Pre-experimental personality battery

Before any roles are assigned, participants complete three incentivized one-shot games (paid for one, randomly chosen) that elicit a social-preference archetype, used as independent predictors of the Stage-2 choice:

| Task | Measures | Primary metric |
|---|---|---|
| Dictator Game (Forsythe et al., 1994) | Unconditional pro-sociality (altruism) | `Dictator_Send` (0–100) |
| Joy of Destruction (Zizzo & Oswald, 2001) | Baseline, unprovoked spite | `Destroy` (0/1) |
| Ultimatum, responder via strategy method (Güth et al., 1982) | Negative reciprocity / costly punishment | `MAO` (minimum acceptable offer) |

These classify participants into archetypes — Consistent Altruist, Fair-Minded Reciprocator, Purely Self-Interested, Spiteful/Demanding — and test whether baseline spite (`Destroy`) and negative reciprocity (`MAO`) predict pressing the red button, while pro-sociality (`Dictator_Send`) predicts the green.

## Repository structure

<!-- TODO: confirm the layout. The repo currently has "Code and Apps/" and "oTree/".
     Tell me which holds the runnable oTree app and what the other contains. -->

```
Lame_Duck-Concept/
├── oTree/              # TODO: the runnable oTree experiment app(s)?
├── Code and Apps/      # TODO: supporting code / earlier versions?
└── README.md
```

## Installation & running

<!-- TODO: confirm Python version, oTree version, and the exact commands you use. -->

```bash
# Requires Python <TODO> and oTree <TODO>
pip install otree                 # or: pip install -r requirements.txt
cd oTree                          # TODO: correct path to the app folder
otree devserver                   # then open http://localhost:8000
```

## Project status & roadmap

**Implemented:** <!-- TODO --> *(which treatments and/or the battery are coded, and what runs end-to-end today)*

**Planned:**
- **LM-agent pre-testing** — evaluating small, open-weight language models (e.g., Gemma) as simulated participants to pilot and stress-test the design before human deployment.
- **Human-subjects deployment** <!-- TODO: IRB status, if applicable -->.
- **Open design questions** flagged in the proposals — e.g., possible survivorship/selection effects in Treatment 4.

## Documents

The design is developed across four notes (commit them to the repo if you'd like them linked here):
the original concept note, the formal behavioral model, the main experimental proposal, and the personality-battery design.

## Selected references

- Alesina, A., & Tabellini, G. (1990). A Positive Theory of Fiscal Deficits and Government Debt. *Review of Economic Studies*, 57(3).
- Bauer, M., et al. (2024). Nastiness in Groups. *Journal of the European Economic Association*, 22(5).
- Dal Bó, P. (2005). Cooperation under the Shadow of the Future. *American Economic Review*, 95(5).
- Fehr, E., & Falk, A. (2002). Psychological Foundations of Incentives. *European Economic Review*, 46(4–5).
- Fehr, E., & Gächter, S. (2000). Cooperation and Punishment in Public Goods Experiments. *American Economic Review*, 90(4).
- Forsythe, R., et al. (1994). Fairness in Simple Bargaining Experiments. *Games and Economic Behavior*, 6(3).
- Güth, W., Schmittberger, R., & Schwarze, B. (1982). An Experimental Analysis of Ultimatum Bargaining. *JEBO*, 3(4).
- Herrmann, B., Thöni, C., & Gächter, S. (2008). Antisocial Punishment Across Societies. *Science*, 319(5868).
- Mas-Colell, A., Whinston, M. D., & Green, J. R. (1995). *Microeconomic Theory*. Oxford University Press.
- Strack, P., & Viefers, P. (2021). Too Proud to Stop: Regret in Dynamic Decisions. *JEEA*, 19(1).
- Zizzo, D. J., & Oswald, A. J. (2001). Are People Willing to Pay to Reduce Others' Incomes? *Annales d'Économie et de Statistique*.

*A complete bibliography appears in the proposal documents.*

## Author

Michael Manolakis — <!-- TODO: affiliation / website / contact; credit advisor if desired -->

## License

<!-- TODO: choose one. MIT is a common permissive default for research code; an academic /
     "all rights reserved" notice is also fine if you'd rather restrict reuse. -->
