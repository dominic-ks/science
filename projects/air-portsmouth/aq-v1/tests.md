# Air Portsmouth AQ V1 — Test Record

This file records what V1 testing appears to have achieved and, equally importantly, what it did not.

V1 should not be described as formally validated. The available understanding is that data was collected, but scientific validation was not completed.

---

## Summary

- No formal test protocol is recorded for V1
- Data appears to have been collected
- That data was not validated against a defensible reference process

The main result is therefore technical rather than scientific: the system produced data, but the trustworthiness of that data remains unresolved.

---

## Test Record

### T1 — Initial Data Collection

**Date:** [TBC — specific deployment or collection date]

**Goal:**
Verify that the sensor stack and device-side host path produce data in a real deployment.

**Setup:**
- AQ V1 hardware with PMS5003, gas sensors, and DHT22 connected through the Pico + Pi Zero architecture
- Pi Zero host path enabled
- Deployment environment: [TBC — specific location and conditions]

**Result:**
- Data was produced
- No formal validation is recorded

**Observations:**
- The system appears to have generated a usable data stream
- PMS5003 output appears more promising than the gas sensors
- Environmental context was available but limited by DHT22 quality
- No documented calibration, co-location, or correction procedure accompanies the dataset

**Conclusion:**
V1 appears to work technically as a data-producing device, but not scientifically as a validated measurement instrument.

**Issues to Carry Forward:**
- A device that produces data is not the same as a device producing trusted AQ measurements
- Calibration and test design must become first-order tasks in V2

---

## Missing Tests

These are important tests that appear necessary but are not recorded as completed in V1.

### Co-location With Reference Station

**Question:**
How closely does PMS5003 track a trusted local reference over time?

**Status:**
Not recorded as completed.

### PM vs Humidity Correlation

**Question:**
How strongly are the particulate readings being shifted by humidity in local deployment conditions?

**Status:**
Not recorded as completed.

### Sensor Drift Over Time

**Question:**
Do PMS5003, MICS6814, and DHT22 outputs remain stable enough over time to support comparison?

**Status:**
Not recorded as completed.

### Cross-Sensor Comparison

**Question:**
Do multiple V1 devices or repeated sensor assemblies agree closely enough to support comparative deployment?

**Status:**
Not recorded as completed.

---

## Minimum V2 Validation Sequence

The next phase should document at least:

1. Bench validation that all sensors are producing stable output.
2. Co-location with a reference station for an extended period.
3. Environmental correlation analysis, especially humidity vs PM response.
4. Repeatability checks across more than one device or more than one deployment cycle.
5. Clear separation between raw data, corrected data, and interpreted results.
