# Sonoff Salt Check — Forward Plan

> Derived from the T1 plan in [tests.md](./tests.md) and the pre-test data check in [README.md](./README.md). Update after T1 is run.

---

## Must-Fix

| # | Issue | Source |
|---|-------|--------|
| 1 | Sonoff stopped reporting from 2026-05-13 to 2026-10-09. The DHT22 correction can't be re-checked against the Sonoff over that period, and a silent dropout could recur | [README.md](./README.md#current-status) |
| 2 | Sonoff reports only on ~1-point changes, which limits the resolution of a settled reading taken from BigQuery | [setup.md](./setup.md#sonoff-reporting-behaviour) |

---

## Experiments to Run

| Experiment | Goal | Priority |
|------------|------|----------|
| T2 — Second reference point: saturated Mg(NO₃)₂ (~54 % RH) — **chosen 2026-10-12**; fallbacks K₂CO₃ (~43 %) or MgCl₂ (~33 %) | Separate an offset error from a gain (slope) error, so the DHT22 correction can be adjusted across its range and not just at 75 % | **Medium.** T1 gave \|e\| = 0.6 < U = 1.9, so there is no evidence of a problem at 75 %, but gain error at ~50 % is still unchecked |
| T3 — Repeat NaCl check | Detect Sonoff drift over time | Every 6–12 months, or after any suspicious reading |
| T4 — DHT22 directly over salt (if it can be removed from the home Pi) | Check the DHT22 against the physical reference directly, without going through the Sonoff | Low; only if the DHT22 can be moved without disturbing the long-term setup |

### Second Reference Point: Is It Worth It?

Probably yes. T1 found no significant error at 75 %, so this is about confirming the low end, not fixing a known problem:

- The correction was fitted over Sonoff readings of **~51–71 %** (5th–95th percentile, Oct 2025 – May 2026). NaCl at 75 % sits just above that range, so T1 checks the top end only.
- A gain error can't be ruled out with one point. A second point lets the Sonoff's own two-point correction (`true = a × Sonoff + b`) be chained into the DHT22 correction.
- **Chosen: magnesium nitrate, Mg(NO₃)₂ (~54 %).** It sits inside the fitted range (51–71 %), so it checks the Sonoff where the correction is actually used. With NaCl at 75 % it gives two points ~21 RH points apart.
- Fallbacks if Mg(NO₃)₂ is hard to get: **K₂CO₃ (~43 %)**, just below the range and easy to buy (baking supplies), or **MgCl₂ (~33 %)**, the bath flakes. It's further out of range but very temperature-stable.

#### T2 notes: magnesium nitrate

| Temperature | Equilibrium RH (Greenspan 1977) |
|-------------|---------------------------------|
| 15 °C | 55.87 % ± 0.27 |
| 20 °C | 54.38 % ± 0.23 |
| 25 °C | 52.89 % ± 0.22 |
| 30 °C | 51.40 % ± 0.24 |

- **Much more temperature-sensitive than NaCl:** about −0.3 points per °C, compared with −0.04 for NaCl. Record the enclosure temperature carefully and use the settled-window mean `T` for `R`. A 1 °C error in `T` gives ~0.3 points of reference error.
- Usually sold as the hexahydrate (fertiliser grade is fine). It is an oxidiser: keep it away from flammables and don't heat it. Make the slurry the same way as for NaCl (damp, with undissolved crystals).
- Use the same jar, desk location, and Sonoff placement as T1 so the two points are comparable. Allow 24–36 h; T1 took ~10 h to reach its final step.
- Analysis: with errors `e₁` (NaCl, −0.6) and `e₂` (Mg(NO₃)₂), the Sonoff's own correction is the line through the two points. If `e₂` ≈ `e₁` (within U), it's an offset only and the DHT22 correction stands. If not, chain the Sonoff line into the DHT22 correction to get a new slope and intercept.
- Unlike table salt, all three need buying. Other salts may settle more slowly than NaCl. T1 took ~10 h to reach its final step in this jar, so allow 24–36 h.

---

## Repeat Schedule for the DHT22

DHT22 sensors drift, especially at sustained high humidity. The correction depends on two links, DHT22 → Sonoff and Sonoff → reference. Check each at a different interval:

| Check | Method | Interval |
|-------|--------|----------|
| DHT22 vs Sonoff | Re-run the paired 10-minute regression on the latest 4–8 weeks and compare slope/intercept/RMSE with the current fit | Monthly, or a scheduled query |
| Live sanity check | Corrected DHT22 vs Sonoff spot reading (as on 2026-10-09: 64.8 vs 64.1) | Whenever looking at the data |
| Sonoff vs salt | Repeat T1 | 6–12 months |

Suggested alert threshold: if corrected-DHT22 minus Sonoff stays above **±2 points** (≈ 1.5 × the fit RMSE) as a 24-hour mean, re-fit the correction.

---

## Unknowns

- [ ] Can the Sonoff's humidity reporting threshold be lowered in Zigbee2MQTT?
- [ ] Why did the Sonoff stop reporting between 2026-05-13 and 2026-10-09 (battery, pairing, Zigbee2MQTT, or pipeline)?
- [ ] What is the Sonoff SNZB-02D's datasheet humidity accuracy? [TBC — check manufacturer spec] Compare it with the measured `e`.
- [ ] Is the Sonoff's error a constant offset or a gain error? (Needs T2.)
- [ ] Should the corrected DHT22 values be stored in BigQuery (e.g. a view), so other projects use the same correction?

---

## Design Principles

1. Every correction should trace back to a physical reference, not only to another low-cost sensor.
2. Change the correction only when the measured error exceeds its uncertainty.
3. Record correction versions with the date and evidence, so past analyses can say which correction they used.
