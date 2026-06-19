# Air Portsmouth AQ V2 — Test Record

This file records planned and completed tests for V2.

The V2 test programme was derived from the missing tests and minimum validation sequence identified at the end of V1. See [aq-v1/tests.md](../aq-v1/tests.md) for V1 test history.

The programme is structured in three phases:

- **Phase 1** — validate the V2 sensor platform on the original mains/WiFi architecture.
- **Phase 2** — modify the device to use LoRa and battery power, and validate the new architecture.
- **Phase 3** — co-location calibration against official sensors.

---

## Summary

### Phase 1 — V2 Sensor Platform Validation

| # | Test | Status |
|---|------|--------|
| T1.1 | Bench validation | ✅ Done |
| T1.2 | MICS6814 dropout investigation | ✅ Done |
| T1.3 | Home deployment — reliability | 🟡 Ongoing |

### Phase 2 — LoRa / Battery Architecture

| # | Test | Status |
|---|------|--------|
| T2.1 | LoRa/battery architecture — research and design | ⬜ Not started |
| T2.2 | LoRa range test — co-location site | ⬜ Not started |
| T2.3 | LoRa/battery deployment — home longevity | ⬜ Not started |
| T2.4 | BME680 fixed-temperature fault investigation | ⬜ Not started |
| T2.5 | Passive radiation shield / external environmental sensor test | ⬜ Not started |

### Phase 3 — Co-location Calibration

| # | Test | Status |
|---|------|--------|
| T3.1 | Co-location with official local sensors | ⬜ Not started |
| T3.2 | PM vs humidity correlation | ⬜ Not started |
| T3.3 | Baseline drift | ⬜ Not started |
| T3.4 | Multi-device or multi-deployment repeatability | ⬜ Not started |

---

## Test Records

### T1.1 — Bench Validation

**Date:** 22/05/2026

**Goal:**
Confirm all sensors are producing stable output before deployment.

**Setup:**
1. Take down the current deployed unit.
2. Replace sensors as required to bring the unit to V2 spec (DHT22 → BME680, MQ-135 removed).
3. Bench validate all sensors — confirm stable output before redeployment.

Enclosure note: may need to order a spare enclosure or additional lid to allow swapping without leaving the unit exposed. Confirm whether a second lid is required before starting.

**Result:**
 - Sensors removed and added, moving to test connectivity to the sensors directly with the Pi Pico.
 - Retested the PMS5003 and MICS6814 after the sensor swap, and both are working as expected.
 - First run of BME680 worked perfectly, with the code written in advance with Copilot. 0 issues so far.
 - Development for Pi Zero firmware and backend functions completed.
 - Device end to end test successful, with all sensors reporting data to Grafana as expected. Ready for redeployment.

---

### T1.2 — MICS6814 Dropout Investigation

**Date:** 22/05/2026

**Goal:**
Identify why the MICS6814 stopped reporting data during V1 and never recovered, and determine whether the sensor is usable in V2. Run concurrently with T1.1 during the bench phase.

**Setup:**
 - AQ device taken down and opened for bench testing.
 - Connected Pi Zero to power and am monitoring measures via Grafana.

**Result:**
 - Oberved that all sensors stopped reporting at approx 0947 on 20/05/2026.
 - All sensors except MICS6814 recovered after a power cycle. 
 - After confirming that the MICS6814 was still not reporting after power cycling, I checked the cable in order to rule out a loose connection. Strangely, the sensor was not connected to the ground, with no obvious reason as to why, or how the sensor was operating previously.
 - Reconnected the ground and the sensor started reporting data again, with no obvious issues.

---

### T1.3 — Home Deployment — Reliability

**Date:** 22/05/2026 - ongoing

**Goal:**
Validate that the unit reliably collects and uploads data over an extended period in a real deployment environment. Confirm there are no connectivity dropouts, sensor failures, or data loss issues before moving to Phase 2.

**Setup:**
Deploy unit at home on existing mains power and WiFi. Monitor data continuity and sensor output over time.

**Result:**
 - V2 device deployed at home on 22/05/2026. Initial data looks good, with all sensors reporting as expected. Will monitor over time to confirm reliability before moving to Phase 2.
 - As always the PMS is taking some time to warm up. We'll need to monitor this over time to confirm it stabilises as expected.

---

### T2.1 — LoRa / Battery Architecture — Research and Design

**Goal:**
Research, select, and build a LoRa/battery architecture suitable for temporary co-location deployments where mains power and home WiFi are not available.

**Setup:**
Desk research and feasibility assessment. Select hardware. Define field node and gateway architecture. Plan power management strategy including PMS5003 duty cycling.

Planned field node hardware:
- Raspberry Pi Pico
- PMS5003, BME680, MICS6814 (optional, pending power budget)
- Adafruit RFM95W LoRa breakout (868 MHz)
- LiPo battery + Adafruit bq25185 charger/boost board

Planned gateway hardware:
- LilyGO TTGO LoRa32 (868 MHz) USB-connected to Raspberry Pi Zero

Planned duty cycle: wake → enable PMS5003 → stabilise → read sensors → transmit LoRa packet → sleep.

Note: 868 MHz (UK/EU band) only.

**Result:**
[TBC]

---

### T2.2 — LoRa Range Test — Co-location Site

**Goal:**
Validate LoRa connectivity between the field node at the target co-location site and the gateway at home. Establish whether the link is viable before committing to a co-location deployment.

**Setup:**
Initial testing should use simplified packet transmitters before integrating the full AQ payload stack. This separates RF link problems from AQ sensor problems and avoids ambiguous failures.

Initial validation packets:
- Incrementing counters
- Timestamps
- Battery voltage

Deploy gateway at home (loft, roofline, or external antenna). Take field node to target co-location site (~2.2 km, no direct line of sight). The 2.2 km home gateway link is considered experimental — it may not be viable due to terrain, urban density, and lack of line of sight. Record RSSI, SNR, and packet loss. Also test the fallback gateway site (~800 m, first-floor placement only), which is the more likely viable option.

**Result:**
[TBC]

---

### T2.3 — LoRa / Battery Deployment — Home Longevity

**Goal:**
Validate that the LoRa/battery field node sustains reliable operation over an extended period running on battery with duty-cycled power management. Confirm battery life and data continuity are sufficient for a co-location deployment.

**Setup:**
Deploy field node at home on battery with LoRa uplink to home gateway. Run full duty-cycle operation. Monitor data continuity, packet loss, and battery voltage over time.

**Result:**
[TBC]

---

### T2.4 — BME680 Fixed-Temperature Fault Investigation

**Observed issue:**
The BME680 temperature channel has been reporting a flat **34.7 deg C** since **2026-06-15 03:32:29**. The sensor then stopped reporting from **2026-06-17 02:27:30** for approximately 36 hours. When reporting resumed, the temperature value was still fixed at **34.7 deg C**. Restarting the unit had no effect.

**Goal:**
Identify whether the fault is caused by the BME680 sensor, wiring, Pico firmware, serial payload handling, or backend ingestion/display. Decide whether the BME680 should be replaced before Phase 2 field-node work continues.

**Setup:**
[TBC]

Initial checks to run:
- Confirm whether humidity, pressure, and gas resistance changed while temperature remained fixed.
- Check raw Pico serial output before the Pi Zero upload path.
- Inspect BME680 wiring and connector seating.
- Test the BME680 directly on the bench with a minimal read script.
- Swap in a known-good BME680 if available.
- Confirm backend ingestion is not reusing a stale temperature value.

**Result:**
[TBC]

---

### T2.5 — Passive Radiation Shield / External Environmental Sensor Test

**Background:**
Temperature readings from the AQ unit have appeared higher than nearby weather stations, especially during sunny periods. The likely cause is solar heating of the enclosure and limited airflow around the environmental sensor, causing the BME680 to measure warmed enclosure air rather than true ambient air.

The PMS5003 particulate sensor does not appear to be affected in the same way. The main data-quality risk is therefore temperature, with humidity affected to a lesser extent.

**Goal:**
Design and test a simple passive radiation shield or external sensor arrangement so the environmental sensor measures ambient air temperature and humidity more accurately.

Expected benefits:
- Reduce daytime temperature spikes caused by direct or indirect solar heating.
- Improve agreement with nearby weather stations.
- Improve humidity readings used for particulate correction work.
- Decide whether future AQ nodes should use a permanent shielded external environmental sensor.

**Planned design:**
Use a plumbing part as a simple passive shield:
- White plastic body.
- Sloped upward side holes drilled for ventilation while reducing rain ingress.
- Insect net blocking the bottom opening.
- BME680 mounted inside the shield.
- Sensor wired back to the main AQ unit.

This is a data-quality improvement rather than a core AQ requirement. Particulate readings are already reasonably protected; the environmental readings stand to gain the most.

**Comparison method:**
Compare:
- Current internal / enclosure-adjacent sensor configuration.
- Shielded external BME680 configuration.
- Nearby weather station data.

**Result:**
[TBC]

---

### T3.1 — Co-location With Official Local Sensors

**Goal:**
Establish whether PMS5003 tracks an official local baseline closely enough to justify correction work. Target duration: 2–4 weeks.

**Setup:**
[TBC]

**Result:**
[TBC]

---

### T3.2 — PM vs Humidity Correlation

**Goal:**
Quantify the humidity effect on PMS5003 readings and test whether a correction model is viable.

**Setup:**
[TBC]

**Result:**
[TBC]

---

### T3.3 — Baseline Drift

**Goal:**
Measure how sensor outputs shift over time without any claimed environmental change.

**Setup:**
[TBC]

**Result:**
[TBC]

---

### T3.4 — Multi-Device or Multi-Deployment Repeatability

**Goal:**
Determine whether device-to-device and site-to-site comparisons are interpretable.

**Setup:**
[TBC]

**Result:**
[TBC]

---

## Minimum V2 Validation Sequence

**Phase 1 — Sensor platform validation:**
1. Bench validation — confirm all sensors produce stable output (T1.1).
2. MICS6814 dropout investigation — run concurrently with bench phase (T1.2).
3. Home deployment — validate reliable data collection over time (T1.3).

**Phase 2 — LoRa/battery architecture:**
4. LoRa/battery architecture research, design, and build (T2.1).
5. LoRa range test at target co-location site (T2.2).
6. LoRa/battery home longevity deployment (T2.3).
7. Investigate and resolve the BME680 fixed-temperature fault before relying on environmental correction values (T2.4).
8. Test passive radiation shield / external environmental sensor arrangement before co-location calibration (T2.5).

**Phase 3 — Co-location calibration:**
9. Co-location with official local sensors for an extended period (T3.1).
10. Environmental correlation analysis — humidity vs PM response (T3.2).
11. Baseline drift check across a meaningful deployment window (T3.3).
12. Repeatability checks across more than one device or deployment cycle (T3.4).
