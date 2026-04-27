# Air Portsmouth AQ V2 — Forward Plan

> Derived from the V1 device architecture, observed limitations, and the missing validation work. This is a living document.

V1 showed that low-cost AQ hardware can probably be deployed. V2 should focus on turning that into credible local data through calibration, environmental correction, and clearer separation between core and test measurements.

---

## Must-Fix

| # | Issue |
|---|-------|
| 1 | No PM calibration |
| 2 | No environmental correction |
| 3 | DHT22 needs replacing |
| 4 | No controlled enclosure / airflow |
| 5 | No defined test methodology |

---

## Improvements

| Area | Improvement | Notes |
|------|-------------|-------|
| Environmental sensing | Replace DHT22 with BME280 | Better humidity and temperature context for correction work |
| Gas sensing | Remove MQ-135 from the core system | Needs a constrained model before it can support serious interpretation |
| Gas sensing | Keep MICS6814 as a test channel | Do not treat it as a trusted pollutant value until calibration and interpretation are proven |
| Sampling design | Standardise enclosure and airflow path | Improve repeatability between devices |
| Documentation | Define a validation protocol before deployment | Make future results comparable |

---

## Experiments to Run

These should become structured entries in `tests.md` when executed.

| Experiment | Goal |
|------------|------|
| Co-location with official local sensors for 2-4 weeks | Establish whether PMS5003 tracks an official local baseline well enough to justify correction work |
| PM vs humidity correction study | Quantify the humidity effect and test whether a correction model is viable |
| Baseline drift test | Measure how outputs shift over time without any claimed environmental change |
| Multi-location comparison | Determine whether device-to-device and site-to-site comparisons are interpretable |

---

## Unknowns

- [ ] How accurate PMS5003 is in local Portsmouth conditions
- [ ] How strong the humidity effect is in real deployments
- [ ] Whether a practical correction model is viable
- [ ] What enclosure and airflow design is required for consistent sampling
- [ ] What sensor suite belongs in the more capable V2 device
- [ ] Whether all V2 sensors can be calibrated well enough to produce credible data

---

## V2 Design Principles

1. **Separate data collection from data confidence** — collecting a value does not mean it is ready for interpretation.
2. **Keep core and test measurements separate** — early-stage signals should not be confused with stronger ones.
3. **Prefer consistency over theoretical accuracy** — a stable, well-characterised system is more useful than a noisy sensor stack making bigger claims.
4. **Calibration is a core experiment** — not a cleanup task to defer until later.
5. **Record environmental context every time** — humidity, temperature, location, and placement all matter.
6. **Use V2 to broaden credibility** — the more capable device should be designed so every retained sensor has a practical calibration path.

See [approach.md](./approach.md) for the project-level working method behind these principles.
