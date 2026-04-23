# Disposable Dehumidifiers — Condensation Study V1

This measurement campaign tests whether disposable dehumidifiers produce a measurable reduction in humidity in the loft bedroom eaves storage.

The study starts with passive monitoring only. Dehumidifiers are added only after a baseline period has been recorded.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Record baseline temperature and humidity in the eaves storage with no dehumidifiers installed | In progress |
| 2 | Compare eaves readings with outside temperature and humidity from OpenWeatherMap data | Planned |
| 3 | Add disposable dehumidifiers and monitor the same location over a comparable period | Planned |
| 4 | Determine whether any observed humidity reduction is larger than normal weather-driven variation | Planned |
| 5 | Decide whether disposable dehumidifiers are useful enough to keep using in this location | Planned |

---

## Working Hypothesis

Disposable dehumidifiers may reduce local moisture levels, but the effect could be small or temporary if moisture is replenished from outside air, adjacent rooms, or the building fabric.

The experiment should therefore compare both absolute values and trends before and after dehumidifiers are added, rather than relying only on the amount of water collected by the dehumidifier.

---

## Phase Plan

| Phase | Intervention | Duration | Question |
|-------|--------------|----------|----------|
| S1 — Baseline monitoring | No disposable dehumidifiers | Minimum two weeks; may run longer, with a two-week analysis window selected later | What are the normal temperature and humidity patterns in the eaves storage? |
| S2 — Dehumidifier monitoring | Disposable dehumidifiers installed | TBC, likely around two weeks | Do the readings change after dehumidifiers are added? |

The baseline phase is already collecting data. The exact analysis window should be selected later from the available baseline data. If the weather changes substantially between phases, the outside weather data should be used to interpret whether the indoor change is likely to be caused by the dehumidifiers.

---

## Data to Capture

- Timestamp.
- Eaves storage temperature.
- Eaves storage relative humidity.
- Outside temperature.
- Outside relative humidity.
- Disposable dehumidifier installation date and time.
- Number, brand, and size of disposable dehumidifiers used.
- Any changes to room use, ventilation, heating, windows, or access doors.

Derived values to consider during analysis:

- Dew point.
- Absolute humidity.
- Difference between inside and outside humidity.
- Daily minimum, maximum, and average humidity.
- Lag between outside weather changes and eaves storage changes.

---

## Document Index

| File | Purpose |
|------|---------|
| [setup.md](./setup.md) | Measurement setup, sensor location, firmware, and data sources |
| [tests.md](./tests.md) | Baseline and dehumidifier monitoring plan |
