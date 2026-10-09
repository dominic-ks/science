# Sonoff Salt Check — Test Record

This file records the saturated-salt test of the Sonoff SNZB-02D and the resulting DHT22 calibration decision.

---

## Summary

Not yet run. T1 places the Sonoff in a sealed enclosure over saturated NaCl overnight. It compares the settled reading with the ~75.4 % reference and uses the error to keep or adjust the DHT22 correction.

---

## Test Record

### T1 — Sonoff vs Saturated NaCl, Overnight

**Date:** [TBC — run date]

**Goal:**
Measure the Sonoff's humidity error at ~75 % RH against a saturated-salt reference, and decide whether the DHT22 correction (`true RH ≈ 0.483 × DHT22 + 26.36`) needs adjusting.

**Hypothesis:**
The Sonoff's settled reading is within ±3 points of the reference.

**Setup:**
- Enclosure, salt, and placement as in [setup.md](./setup.md).
- Sonoff SNZB-02D (`0x3425b4fffe149e16`) reporting via Zigbee2MQTT on device-003 to BigQuery `SNZB_02D`.
- Minimum duration: overnight, ideally **≥ 8 hours** sealed. Longer is better; do not open the container during the run.

**Measurements to Record:**
- Seal (start) and unseal (end) times, local time.
- Sonoff LCD humidity and temperature at start and just before opening. Photograph if possible.
- Room temperature at start and end, plus anything that changed overnight (heating on/off, window open, sun on container).
- Sonoff humidity and temperature reports from BigQuery for the whole run.
- Any reporting-threshold change made in Zigbee2MQTT.

**Pass Condition (hypothesis supported):**
The settled reading is within ±3.0 points of the temperature-adjusted reference.

**Validity Conditions (test is usable at all):**
- Undissolved salt still visible in the slurry at the end.
- Reading has **settled**: the time-weighted mean over the final 2 hours differs from the previous 2 hours by **≤ 0.5 points**, and is not still trending.
- Enclosure temperature range over the settled window is ≤ 1 °C.
- The Sonoff reported at least once during the final 2 hours, or the LCD reading was recorded at the end.

If a validity condition fails, record the run as a useful failure with its cause and repeat. Do not stretch the analysis to fit.

**Out of Scope:**
- Checking the Sonoff's slope or linearity. One reference point can only check the error at ~75 %. See [next-plan.md](./next-plan.md).
- Checking temperature accuracy.
- Putting the DHT22 itself in the enclosure.
- Re-fitting the DHT22 correction from new paired data.

**Decision to Make After Test:**
Keep the current DHT22 correction, or shift it using the decision rule below.

---

## Field Log

Record times in local time (BST until 2026-10-25). **BigQuery `datetime` values are UTC.** Subtract 1 hour from BST times when filtering queries. This was confirmed on 2026-10-09: the newest rows were stamped 19:32 when local time was ~20:34 BST.

| Event | Local time | UTC | Sonoff LCD RH | Sonoff LCD temp | Room temp | Notes |
|-------|------------|-----|---------------|-----------------|-----------|-------|
| Container sealed | | | | | | |
| Check (optional) | | | | | | |
| Just before opening | | | | | | |
| Container opened | | | | | | |

Observations (reference by event, e.g. "sealed: condensation on lid"):

- 

---

## Analysis Method

### 1. Settling Profile

Hourly time-weighted mean of the Sonoff's reported humidity. Each report stays in force until the next report. Replace the two times with the run's **UTC** seal and open times.

```sql
WITH p AS (
  SELECT DATETIME '2026-10-09 21:00:00' AS start_dt,   -- seal time, UTC
         DATETIME '2026-10-10 07:00:00' AS end_dt      -- open time, UTC
),
r AS (
  SELECT s.datetime AS t0,
         LEAST(COALESCE(LEAD(s.datetime) OVER (ORDER BY s.datetime), p.end_dt), p.end_dt) AS t1,
         s.humidity, s.temperature
  FROM `iot-projects-309015.iot_device_data.SNZB_02D` s, p
  WHERE s.datetime >= p.start_dt AND s.datetime < p.end_dt
)
SELECT DATETIME_TRUNC(t0, HOUR) AS hour_utc,
       COUNT(*) AS reports,
       ROUND(SUM(humidity * DATETIME_DIFF(t1, t0, SECOND)) / NULLIF(SUM(DATETIME_DIFF(t1, t0, SECOND)), 0), 2) AS tw_rh,
       MIN(humidity) AS min_rh, MAX(humidity) AS max_rh,
       MIN(temperature) AS min_t, MAX(temperature) AS max_t
FROM r
GROUP BY hour_utc
ORDER BY hour_utc;
```

*A report that spans an hour boundary is credited to the hour it started in. That is fine for checking settling, but use step 2 for the final value.*

### 2. Settled Value

- **Settled window:** the final 2 hours before opening, provided step 1 shows the curve has flattened.
- **Settled reading (`S`):** time-weighted mean RH over the settled window. Also note the last reported value and the LCD reading. If the LCD and BigQuery disagree by more than the reporting step, prefer the LCD and record why.
- **Enclosure temperature (`T`):** mean Sonoff temperature over the settled window.
- **Reference (`R`):** interpolate from the Greenspan table in [setup.md](./setup.md#reference-saturated-nacl) at `T`. For 18–23 °C this is 75.4–75.5 %.
- **Error:** `e = S − R`.

### 3. Uncertainty Budget

Estimate each term from the run itself, and replace the provisional values with measured ones.

| Source | How estimated | Provisional (±, RH points) |
|--------|---------------|----------------------------|
| Reference value (Greenspan) | Published uncertainty | 0.15 |
| Reference temperature (`T` uncertain by ~1 °C) | Table slope ≈ 0.03 points/°C | 0.03 |
| Temperature gradient inside the enclosure | ~4.5 points per 1 °C; assume ≤ 0.2 °C gradient in a stable location | 0.9 |
| Incomplete settling | Difference between last two 2-hour means | [TBC — from data, target ≤ 0.5] |
| Reporting threshold / resolution | Half the observed reporting step (~1 point), or 0.05 if read from the LCD | 0.5 (BigQuery) / 0.05 (LCD) |
| Short-term noise | Std. dev. of reports in settled window | [TBC — from data] |

Combined standard uncertainty `u` = root-sum-square of the rows. Use **U = 2u** (≈95 %) for decisions. With the provisional values, U ≈ 2.1–2.5 points if read from BigQuery, ≈ 1.8–2.1 if read from the LCD.

The temperature-gradient term dominates. A stable location matters more than anything else in the setup.

### 4. Decision Rule

The DHT22 correction maps the DHT22 onto the Sonoff's scale. If the Sonoff has an error `e` at ~75 %, and that error is assumed to be a **constant offset** across 50–75 % (the range the correction was fitted over), then:

```text
true RH ≈ 0.483 × DHT22 + (26.36 − e)
```

The slope is unchanged. Only the intercept moves.

| Outcome | Interpretation | Action |
|---------|----------------|--------|
| \|e\| ≤ U | Sonoff error not distinguishable from zero | **Keep** current correction. Record `e ± U` as the Sonoff's verified accuracy at 75 %. |
| U < \|e\| ≤ 3 | Hypothesis supported, but a real offset is likely | Keep the correction for now. Note the offset-adjusted intercept as an option. Prioritise a second reference point before changing anything. |
| \|e\| > 3 | Hypothesis rejected | **Adjust** the intercept to `26.36 − e`. Flag that the slope is unverified until a second reference point is run. |

Worked example: if `S = 77.4` and `R = 75.4`, then `e = +2.0`. The Sonoff over-reads by 2 points at 75 %. An offset-adjusted correction would be `0.483 × DHT22 + 24.36`.

Caveat: a single point cannot tell an offset from a gain error. If the Sonoff's error grows with humidity, a constant-offset shift would over-correct at the low end of the fitted range (~50 %). The offset assumption is the main limitation of this test.

---

## Result

**Result:** [TBC — after run]

| Quantity | Value |
|----------|-------|
| Seal → open (UTC) | |
| Settled window (UTC) | |
| Enclosure temperature `T` | |
| Reference `R` | |
| Settled reading `S` (BigQuery TW mean) | |
| Sonoff LCD at end | |
| Error `e` | |
| Expanded uncertainty `U` | |

**Observations:**

- 

**Conclusion:**
[TBC]

**Issues to Carry Forward:**

- 

**Decision Made After Test:**
[TBC — keep / adjust; adjusted intercept if applicable]
