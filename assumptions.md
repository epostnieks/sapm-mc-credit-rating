# Monte Carlo Assumptions — Credit Rating Agencies / Issuer-Pays Corruption Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $11.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 11.21 | Confirmed by N=100,000 draws |
| ΔW median (result) | $123.3B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_rating_inflation` | lognormal | $24B | $33B | $42B | Capital misallocation from inflated ratings |
| `C2_procyclical` | lognormal | $18B | $24B | $30B | Cliff effects, forced selling, rating-triggered cascades |
| `C3_sovereign` | lognormal | $12B | $14B | $16B | Developing nation borrowing cost penalties |
| `C4_competition` | lognormal | $4.5B | $6.25B | $8.0B | NRSRO oligopoly, competition suppression |
| `C5_systemic` | lognormal | $28B | $36.5B | $45B | Systemic fragility, institutional lock-in |
| `C6_democratic` | lognormal | $6B | $9B | $12B | Democratic accountability deficit, austerity imposition |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.0) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 11.16 | 20% DC adj = 8.93 | 40% DC adj = 6.7

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $123B = 0.1% of world GDP ($106T) ✓
- **β_W range**: 11.21 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
