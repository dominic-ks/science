# Onyx V2 — Forward Plan

> Derived from the V1 build record, submersion testing, and unresolved problems. This is a living document — update it as planning progresses.

The next useful V1 work is a two-stage buoyancy validation recorded in [tests.md](./tests.md): T3 validates the hull-only ballast calculation, and T4 repeats the assessment with the chassis and electronics installed. These tests should feed directly into V2 ballast volume, ballast placement, chassis clearance, and centre-of-mass decisions.

---

## Must-Fix (Blockers for V2)

These are not optional. V2 cannot succeed without addressing these.

| # | Issue | Source |
|---|-------|--------|
| 1 | Waterproofing reliability | [build.md](./build.md), [tests.md](./tests.md) |
| 2 | Underwater communication method must be chosen before live submerged control design | [build.md](./build.md), [tests.md](./tests.md) |
| 3 | Buoyancy and balance must be stable before propulsion testing | [build.md](./build.md), [tests.md](./tests.md) |
| 4 | Ballast system must be measured and validated | [build.md](./build.md), [tests.md](./tests.md) |
| 5 | Seal validation protocol needed before electronics go in | [tests.md](./tests.md), [approach.md](./approach.md) |
| 6 | Internal orientation must be resolved before layout | [approach.md](./approach.md) |

---

## Improvements

Things that would significantly improve V2 but aren't hard blockers:

| Area | Improvement | Notes |
|------|-------------|-------|
| Enclosure | More internal volume if possible | Reduces layout friction |
| Ballast | Fully adjustable positioning | Not fixed-mount |
| Power | Profile actual current draw | Determine real runtime |
| Power | Larger LiPo if volume allows | ~300–500mAh target |
| Sealing | Redundant seal method | Glue + O-ring or gasket |
| Assembly | Document assembly sequence | Prevent rework loops |
| Testing | Run subsystem tests before integration | Bench → dry seal → wet seal → water |
| Communication | Replace Bluetooth only if live submerged control is required | Investigate low-frequency radio, tether, or acoustic methods before committing to real-time RC scope |

---

## Experiments to Run

These need structured test entries in [tests.md](./tests.md) when executed:

| Experiment | Goal |
|------------|------|
| Seal pressure test (empty enclosure) | Validate seal holds before electronics go in |
| V1 hull-only ballast validation | Validate displacement and required ballast before chassis effects are added |
| V1 chassis-installed buoyancy reassessment | Measure dry mass, syringe-water mass, trim, and practical ballast placement with the V1 chassis installed |
| Buoyancy profile (no ballast) | Understand baseline before adding ballast |
| Ballast range test | How much volume change is needed to submerge? |
| Power draw measurement | Real runtime under load |
| Stability test (ballast installed) | Can it hold a stable depth? |
| Underwater communication test | If V2 requires live submerged control, does the chosen communication method work at operating depth and range? |
| Orientation test | Confirm upside-down mount works mechanically |

---

## Unknowns

Things V2 will need to answer that V1 didn't:

- [ ] Does V2 require live submerged control, or is surface-commanded autonomous operation sufficient for the next test stage?
- [ ] If live control is required, what communication method will support the intended underwater control range?
- [ ] What is the minimum ballast volume change needed for meaningful depth control?
- [ ] What ballast mass is required for the V1 hull alone to reach neutral buoyancy?
- [ ] How much does the chassis-installed mass and centre of mass change the ballast requirement?
- [ ] How much water does the syringe actually bring onboard during a wet test?
- [ ] What is the actual power draw under full operation?
- [ ] Can the unit achieve neutral buoyancy with current weight budget?
- [ ] What seal method reliably holds at [target depth]?
- [ ] Is the syringe ballast mechanism reliable under pressure?
- [ ] What is the stability behaviour when propulsion is active?

---

## V2 Design Principles

Based on V1 experience, V2 should be designed around these rules:

1. **Orientation first** — lock the mounting orientation before anything else
2. **Seal before electronics** — validate the empty enclosure is watertight before installing components
3. **Adjustable over fixed** — every positional parameter should be adjustable
4. **Incremental testing** — bench → dry → static water → powered water
5. **Document as you go** — don't rely on memory

See [approach.md](./approach.md) for the project-level working method these principles come from.

---

## Backlog / Ideas

Low-priority items to consider for V2 or beyond:

- [ ] Active depth hold (PID control with pressure sensor)
- [ ] Camera integration
- [ ] Wired tether as interim control method
- [ ] Low-frequency radio communication research for untethered short-range control
- [ ] Acoustic communication research for untethered control
- [ ] 3D-printed custom enclosure
- [ ] External ballast weight system (removable lead/tungsten)
- [ ] LED status indicator (visible through enclosure)
