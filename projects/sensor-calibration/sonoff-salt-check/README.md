# Sensor Calibration — Sonoff Salt Check

This phase checks the Sonoff SNZB-02D against a physical humidity standard. Air sealed over a saturated sodium chloride (table salt) slurry settles at a known relative humidity (~75.3–75.5 % at room temperature).

---

## Question

How far is the Sonoff from the true humidity at a known point (~75 % RH), and does that error change the DHT22 calibration we should use?

## Hypothesis

The Sonoff reads within ±3 points of the saturated-salt reference in a sealed enclosure, so the existing DHT22 calibration (`true RH ≈ 0.483 × DHT22 + 26.36`) can stand.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Prepare a sealed saturated-salt enclosure and confirm the Sonoff reports from inside it | Planned |
| 2 | Hold the Sonoff in the enclosure overnight and record start/end times and room conditions | Planned |
| 3 | Extract the settled Sonoff reading from BigQuery (and the on-device display) | Planned |
| 4 | Calculate the Sonoff error against the reference with an uncertainty budget | Planned |
| 5 | Keep or adjust the DHT22 calibration based on the decision rule in [tests.md](./tests.md) | Planned |
| 6 | Decide on a repeat interval and whether a second reference point is worth adding | Planned |

---

## Current Status

Setup and analysis method are written. The physical test has not been run yet.

Pre-test data check (2026-10-09):

- The Sonoff stopped reporting to BigQuery on **2026-05-13 12:40** and started again on **2026-10-09 17:53**. There is no Sonoff data for the summer.
- Since reconnecting, the Sonoff reports **only when a reading changes** (gaps from a few seconds to 36 minutes in the first two hours). Humidity values step by about 1 point between reports. Temperature reports so far are 23.0, 23.2, then 22.2 °C. That suggests coarse reporting thresholds, which matter for reading a steady value. See [setup.md](./setup.md#sonoff-reporting-behaviour).
- At 19:32 on 2026-10-09 the raw DHT22 read 75.0 % (corrected: 62.6 %) and the Sonoff read 63.2 %. The correction still tracks after the gap.

---

## Document Index

| File | Purpose |
|------|---------|
| [setup.md](./setup.md) | Enclosure, salt preparation, sensor placement, reference values, and pre-test checks |
| [tests.md](./tests.md) | T1 test plan, field log, analysis queries, uncertainty budget, and decision rule |
| [next-plan.md](./next-plan.md) | Repeat checks, second reference point, and open questions |
