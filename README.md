# SAPM Monte Carlo — Credit Rating Agencies / Issuer-Pays Corruption Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Credit Rating Agencies (Issuer-Pays Corruption Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **11.21** |
| β_W mean | 11.26 |
| β_W std | 1.02 |
| **90% CI** | **[9.7, 13.0]** |
| 99% CI | [9.1, 13.8] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$123.3B/yr** |
| Π (revenue) | $11.0B/yr |

**β_W = 11.21** means the credit rating agencies industry destroys **$11.21 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-credit-rating.git
cd sapm-mc-credit-rating
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 11.21` and `ΔW median : $123.3B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_rating_inflation | $33.0B | [$25.9B, $42.0B] | Lognormal |
| C2_procyclical | $24.0B | [$19.2B, $30.0B] | Lognormal |
| C3_sovereign | $14.0B | [$12.3B, $16.0B] | Lognormal |
| C4_competition | $6.3B | [$4.9B, $8.0B] | Lognormal |
| C5_systemic | $36.5B | [$29.6B, $44.9B] | Lognormal |
| C6_democratic | $9.0B | [$6.8B, $12.0B] | Lognormal |
| **Total ΔW** | **$123.3B** | **[$106.3B, $143.2B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Credit Rating Agencies (Issuer-Pays Corruption Floor)*.
> GitHub: epostnieks/sapm-mc-credit-rating.
> https://github.com/epostnieks/sapm-mc-credit-rating
