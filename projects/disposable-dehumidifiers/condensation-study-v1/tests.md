# Condensation Study V1 — Test Record

This file records the monitoring phases and later results for the disposable dehumidifier study.

---

## Summary

The study compares eaves storage temperature and humidity before and after disposable dehumidifiers are installed. OpenWeatherMap outside weather data should be collected for the same period so indoor changes can be compared against external temperature and humidity changes.

---

## Test Record

### S1 — Baseline Eaves Monitoring

**Date:** [In progress]

**Goal:**
Measure the normal temperature and humidity pattern in the eaves storage without disposable dehumidifiers installed.

**Setup:**
- Raspberry Pi Zero running `iot-nest-firmware`.
- DHT22 installed in the loft bedroom eaves storage.
- No disposable dehumidifiers installed in the test area.
- Outside temperature and humidity collected from OpenWeatherMap data.

**Duration:**
Minimum two weeks. Data collection may run longer, with a representative two-week analysis window selected later.

**Measurements to Record:**
- Eaves storage temperature.
- Eaves storage relative humidity.
- Outside temperature.
- Outside relative humidity.
- Sampling interval.
- Any changes to heating, ventilation, room use, windows, or access doors.

**Pass Condition:**
The baseline period produces enough continuous data to describe normal humidity variation and compare it with outside weather changes.

**Decision to Make After Test:**
Which two-week baseline window should be used for analysis, and whether the baseline is stable and complete enough to start the dehumidifier phase.

---

### S2 — Disposable Dehumidifier Monitoring

**Date:** [Planned]

**Goal:**
Measure whether adding disposable dehumidifiers changes eaves storage humidity relative to the baseline period and outside weather conditions.

**Setup:**
- Same sensor location and data-logging setup as S1.
- Disposable dehumidifiers installed in the eaves storage.
- Outside temperature and humidity collected from OpenWeatherMap data.

**Duration:**
TBC. Current working assumption is approximately two weeks, ideally comparable to S1.

**Measurements to Record:**
- Eaves storage temperature.
- Eaves storage relative humidity.
- Outside temperature.
- Outside relative humidity.
- Dehumidifier installation date and time.
- Number, brand, and size of dehumidifiers.
- Visible water collected, if practical to record.
- Any changes to heating, ventilation, room use, windows, or access doors.

**Pass Condition:**
The dehumidifier period produces enough continuous data to compare with S1 after accounting for outside weather changes.

**Decision to Make After Test:**
Whether disposable dehumidifiers produce a meaningful reduction in humidity for this location, and whether further tests should change the number, placement, or type of dehumidifier.

---

## Analysis Notes

Analysis should not rely only on relative humidity, because relative humidity changes with temperature. If possible, calculate dew point or absolute humidity from the DHT22 readings and compare those values before and after dehumidifiers are added.

Compare:

- S1 indoor humidity against S1 outside humidity.
- S2 indoor humidity against S2 outside humidity.
- S1 and S2 daily humidity profiles.
- Indoor/outdoor differences before and after dehumidifier installation.
- Any lag between outside weather changes and eaves storage changes.
