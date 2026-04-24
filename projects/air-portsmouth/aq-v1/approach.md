# Air Portsmouth AQ V2 — Project Approach

This file defines how the next stage of the Air Portsmouth device work should be run. It builds on the repository-wide [approach](../../../approach.md) and adapts it for low-cost air quality monitoring.

The main aim is to reduce over-interpretation. Future work should distinguish clearly between a device that produces numbers and a device that supports defensible claims.

---

## Working Principles

### 1. Treat calibration as a core experiment

Calibration is not a finishing step. For this device, calibration and co-location are central experiments that determine whether stronger interpretation is justified.

If a sensor cannot be calibrated or characterised well enough for its intended use, reduce the claim rather than stretching the evidence.

### 2. Separate raw, corrected, and interpreted data

Do not collapse all outputs into a single implied truth.

Keep these categories distinct:

- raw data
- corrected data
- interpreted data

Each stage should state what assumptions were applied and what remains uncertain.

### 3. Always record environmental conditions

AQ readings are strongly affected by context. Every meaningful test or deployment should record:

- temperature
- humidity
- placement
- airflow conditions
- duration
- nearby activity or obvious disturbances where known

If a relevant condition is not known, record it as unknown rather than ignoring it.

### 4. Prefer long-term observation over short tests

Short spot checks are useful for confirming that a sensor is alive. They are weak evidence for calibration, drift, or stronger interpretation.

When possible, prefer longer deployments that show:

- repeatability
- day-to-day consistency
- weather sensitivity
- drift behaviour

### 5. Keep experimental channels separate from core readings

If a signal is exploratory, label it that way.

In particular:

- PMS5003 may support cautious trend reporting before full absolute trust is established
- MICS6814 should remain experimental unless a specific interpretation method is validated
- MQ-135 should not drive core device conclusions

### 6. Preserve uncertainty explicitly

Unknowns should remain visible in the documentation. Use `[TBC — specific missing detail]` where evidence is missing.

Do not claim:

- regulatory accuracy
- pollutant-specific certainty from cross-sensitive gas sensors
- precision that has not been demonstrated

---

## Task Pattern

Use this pattern for AQ device work:

1. State the question being answered.
2. Define the smallest deployment, test, or analysis that can answer it.
3. Record the starting hardware and environmental conditions.
4. Run the test or deployment.
5. Record observations before interpretation.
6. State what can now be claimed, and what still cannot.
7. Update the relevant document before moving on.

If a task increases the amount of data but does not reduce uncertainty, reconsider whether it is the right next step.

---

## Documentation Rules

Use the documents this way:

| Document | Use |
|----------|-----|
| [build.md](./build.md) | Hardware architecture, sensor choices, and design limitations |
| [tests.md](./tests.md) | Validation history, missing tests, and future test records |
| [v2-plan.md](./v2-plan.md) | Must-fix issues, experiments, and design principles for V2 |
| [approach.md](./approach.md) | Project-specific process rules for AQ work |

Do not hide weak evidence inside strong wording. If a result is only good enough for exploratory trend use, document it that way.
