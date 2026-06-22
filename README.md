# WC 2026 Forecast

A probabilistic forecast for the 2026 FIFA World Cup, updated automatically as group-stage results come in.

---

## What it shows

- **Win probabilities** for all 48 teams, ranked and updated after each match
- **Projected knockout bracket** — the most likely coherent path from quarter-finals through to the final
- **Probability trend sparklines** showing how each team's chances have evolved over time

---

## How it works

The backend runs a Monte Carlo simulation of the remaining tournament, producing probability estimates from the distribution of outcomes.

Two match models are available:

**Poisson model** — each team's expected goals in a match are derived from their attack and defence rates relative to the tournament average. Goals are drawn from independent Poisson distributions. Fast; default for high simulation counts.

**Event model** — the same expected-goals formula, but played out as 90 independent Bernoulli trials (one per minute). After each goal, a tactical mode multiplier adjusts both teams' scoring rates — a team that falls behind becomes more aggressive, one that leads becomes more conservative. Slower but captures in-game momentum shifts.

Both models use a Bayesian prior blended from hand-crafted FIFA-ranking estimates, ~4 years of historical international results (weighted by recency and competition importance), and observed WC 2026 group-stage results as they accumulate. Weather conditions at each venue are factored in via Open-Meteo forecasts.

The projected bracket is built as a coherent conditional chain: the quarter-final winner at each position is the team that advances there most often across all simulations; the semi-final matchups are drawn only from simulations where both QF winners actually met; the final is drawn only from simulations where both SF winners met. This guarantees the bracket is self-consistent — every team shown advancing in one round appears as a participant in the next.

---

## Data sources

- Match data: [football-data.org](https://www.football-data.org/) (free tier)
- Weather forecasts: [Open-Meteo](https://open-meteo.com/)
