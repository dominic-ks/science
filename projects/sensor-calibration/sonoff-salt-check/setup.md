# Sonoff Salt Check — Setup

This file records the enclosure, reference, and sensor setup for the saturated-salt check.

---

## Reference: Saturated NaCl

Air in a sealed space over a saturated sodium chloride solution (a slurry with undissolved crystals present) reaches a fixed relative humidity that changes very little with temperature.

| Temperature | Equilibrium RH | Uncertainty |
|-------------|----------------|-------------|
| 15 °C | 75.61 % | ±0.18 |
| 20 °C | 75.47 % | ±0.14 |
| 25 °C | 75.29 % | ±0.12 |
| 30 °C | 75.09 % | ±0.11 |

*Source: Greenspan (1977), "Humidity Fixed Points of Binary Saturated Aqueous Solutions", J. Res. NBS 81A. Interpolate linearly for the recorded enclosure temperature. At typical room temperatures (18–23 °C) the reference is 75.4–75.5 %.*

The reference value itself is not the main source of error. Most of the error comes from the setup, mainly temperature differences inside the enclosure and incomplete settling.

---

## Equipment

| Item | Detail |
|------|--------|
| Sensor under test | Sonoff SNZB-02D |
| Enclosure | Airtight food container with a gasket lid. Clear, if possible, so the Sonoff's LCD can be read without opening it. [TBC — container type and approximate volume] |
| Salt | Plain table salt (NaCl). Iodised or anti-caking additives have a negligible effect at these quantities. [TBC — brand / type used] |
| Water | Tap or distilled. [TBC — which] |
| Dish | Small open dish or lid for the slurry |
| Stand | Something to hold the Sonoff above the slurry so it can't get wet (e.g. an upturned cup) |

---

## Preparation

1. Put a few tablespoons of salt in the dish. Add water a little at a time until it is a **damp slurry, like wet sand**: undissolved crystals must be visible, with a thin layer of brine around them. If all the salt dissolves, add more salt.
2. Place the dish in the container and the Sonoff on its stand next to it. The sensor must not touch the slurry or the brine.
3. Leave as much free air space as practical between slurry and sensor. A larger slurry surface relative to container volume settles faster.
4. Seal the lid. If the Sonoff's display is visible, note the reading and time.
5. Put the container somewhere with **stable temperature**: away from radiators, windows, direct sun, electronics, and draughts. A central shelf or cupboard in a room that is not heated overnight is ideal. Do not hold the container longer than needed; hand warmth affects the reading.

---

## Sensor Placement and Temperature Effects

Temperature differences inside the enclosure are the largest risk. If the sensor's air is warmer than the slurry surface, the sensor reads low: about **4.5 RH points per 1 °C** at 75 % RH. Keep the whole enclosure at one temperature:

- Do not place it near the Pi, a charger, or any other warm object.
- Avoid locations where one side of the container gets sun or radiator heat.
- Note the room temperature at start and end (the Sonoff and DHT22 both report it).

---

## Sonoff Reporting Behaviour

Observed in BigQuery on 2026-10-09, after the Sonoff reconnected at 17:53:

- Reports arrive only on change. Gaps between reports ranged from 4 s to 36 min (median ~2 min).
- Humidity values step by about 1.0 point between consecutive reports (e.g. 63.1 → 62.1 → 61.1 → 60.1), with occasional finer steps (63.6, 62.5).
- Temperature reports so far are 23.0, 23.2, and 22.2 °C. With only three values the temperature step size can't be confirmed yet; it may also be coarse.
- The first report after reconnecting was 75.4 % and then fell to ~65 % within a minute. It was probably a stale or start-up value, not a room reading.

**Implications for the test:**

- *Update, 2026-10-11 (T1):* the Sonoff also sends a repeat report every ~15–50 minutes when nothing has changed, so it never goes fully silent. That doesn't help resolution, though: changes smaller than 1 point still don't show up.
- Once the enclosure settles, the Sonoff may stop sending updates for long periods. The last reported value may then be up to about 1 point away from what the sensor currently reads. BigQuery alone then has about ±1 point resolution at the settled value.
- **Mitigation 1 (preferred):** read the Sonoff's own LCD through the container at the end of the test, or photograph it. Record the value in the field log.
- **Mitigation 2 (optional):** check in Zigbee2MQTT whether the humidity reporting threshold (reportable change) can be lowered for this device before the test. Record any change made and set it back afterwards if needed. [TBC — whether the SNZB-02D accepts a reporting config change]
- Ignore the first report after any reconnect or re-pair.

---

## Pre-Test Checks

- [ ] Sonoff is reporting to BigQuery (it reconnected 2026-10-09 after a gap from 2026-05-13).
- [ ] The Sonoff still reports from inside the closed container. A brief seal-and-check before the full run is enough.
- [ ] Slurry has visible undissolved crystals.
- [ ] Container lid seals fully. Check the gasket is seated.
- [ ] Location chosen away from heat sources and sun.
- [ ] Start time recorded in the [field log](./tests.md#field-log).
- [ ] Note: the Sonoff will not be measuring the room during the test. The DHT22 keeps logging as normal.
