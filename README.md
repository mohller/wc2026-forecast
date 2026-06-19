# WC 2026 Forecast

A probabilistic forecast for the 2026 FIFA World Cup, updated automatically as group-stage results come in.

**Live site:** https://leonel-morejon.org/wc2026-forecast/

---

## What it shows

- **Win probabilities** for all 48 teams, ranked and updated after each match
- **Projected knockout bracket** — the most frequent complete path from quarter-finals to the final across all simulations
- **Probability trend sparklines** showing how each team's chances have evolved over recent updates of the model and matches

---

## How it works

The backend runs a Monte Carlo simulation of the remaining tournament tens of thousands of times, producing probability estimates from the distribution of outcomes.

Two match models are available:

**Poisson model** — each team's expected goals in a match are derived from their attack and defence rates relative to the tournament average. Goals are drawn from independent Poisson distributions. Fast; default for high simulation counts.

**Event model** — the same expected-goals formula, but played out as 90 independent Bernoulli trials (one per minute). After each goal, a tactical mode multiplier adjusts both teams' scoring rates — a team that falls behind becomes more aggressive, one that leads becomes more conservative. Slower but captures in-game momentum shifts.

Both models use a Bayesian prior seeded from FIFA ranking-derived estimates (attack and defence rates per team), blended with observed WC 2026 group-stage results as they accumulate. Weather conditions at each venue are factored in via Open-Meteo forecasts.

The projected bracket is chosen as the most self-consistent outcome: the combination of quarter-final, semi-final and final results that appeared most frequently as a complete, coherent sequence across all simulations.

---

## Data sources

- Match data: [football-data.org](https://www.football-data.org/) (free tier)
- Weather forecasts: [Open-Meteo](https://open-meteo.com/)
