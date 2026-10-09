# Sensor Calibration

This project checks how much the low-cost temperature and humidity sensors used across the other projects can be trusted, and records the corrections applied to them.

It is a measurement-support project. Other projects use DHT22 and Zigbee sensor humidity readings as evidence, so those readings need a documented link back to something more trustworthy than another low-cost sensor.

---

## Background

device-003 (home Pi) has a DHT22 that over-reads humidity. Using a Sonoff SNZB-02D Zigbee sensor next to it as the reference, a linear correction was fitted:

```text
true RH ≈ 0.483 × DHT22 RH + 26.36
```

| Fit detail | Value |
|------------|-------|
| Data | ~15k paired 10-minute averages, Oct 2025 – May 2026 |
| Correlation | r = 0.97 |
| RMSE | 1.2 RH points |
| Sonoff RH range during fit | 51–71 % for the middle 90 % of readings (median 62 %) |
| Live spot check, 2026-10-09 | Corrected DHT22 64.8 % vs Sonoff 64.1 %; a desktop monitor read 67.7 % around the same time |

That correction is only as good as the Sonoff. Nothing yet links the Sonoff to a physical standard.

---

## Devices

| Device | Role | Data |
|--------|------|------|
| Sonoff SNZB-02D (Zigbee ID `0x3425b4fffe149e16`) | Transfer reference for the DHT22 | Zigbee2MQTT on device-003 → BigQuery `iot-projects-309015.iot_device_data.SNZB_02D` |
| DHT22 on device-003 | Sensor being corrected | BigQuery `iot-projects-309015.iot_device_data.dht22`, `id = 9f37db1b-cceb-4ecd-be09-b1df3d8bdfc8` |

---

## Phases

| Phase | Status | Purpose |
|-------|--------|---------|
| [Sonoff Salt Check](./sonoff-salt-check/README.md) | Planned (setup ready) | Check the Sonoff against saturated table salt (~75.3 % RH) and decide whether the DHT22 correction needs adjusting |

---

## Current Direction

- Run the saturated-salt check on the Sonoff overnight.
- Use the result to keep or adjust the DHT22 correction.
- Decide whether a second reference point and a repeat schedule are worth setting up. See [next-plan.md](./sonoff-salt-check/next-plan.md).
