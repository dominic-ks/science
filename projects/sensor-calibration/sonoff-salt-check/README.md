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
| 1 | Prepare a sealed saturated-salt enclosure and confirm the Sonoff reports from inside it | ✅ Glass clip-top jar; Zigbee worked through the glass |
| 2 | Hold the Sonoff in the enclosure overnight and record start/end times and room conditions | ✅ Sealed 2026-10-11 13:21 BST, opened 2026-10-13 09:40 BST (~44 h, two nights) |
| 3 | Extract the settled Sonoff reading from BigQuery (and the on-device display) | ✅ 74.8 % (LCD and BigQuery agree) |
| 4 | Calculate the Sonoff error against the reference with an uncertainty budget | ✅ e = −0.6 ± 1.9 points |
| 5 | Keep or adjust the DHT22 calibration based on the decision rule in [tests.md](./tests.md) | ✅ Keep; error smaller than its uncertainty |
| 6 | Decide on a repeat interval and whether a second reference point is worth adding | ⚠️ See next-plan.md; T2 now medium priority |

---

## Current Status

**T1 run 2026-10-11/12.** The Sonoff read 74.8 % against a 75.4 % reference: −0.6 ± 1.9 points. Repeated on a second night with the same value, and the slurry still had plenty of undissolved crystals when opened (2026-10-13 09:40 BST). The hypothesis is supported, and the DHT22 correction stays as it is. Full record in [tests.md](./tests.md#result).

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
