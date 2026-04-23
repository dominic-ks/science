# Onyx V2 — Project Approach

This file defines how the next stage of the Onyx project should be run. It is deliberately project-level: it is not a parts list, build log, or backlog.

The aim for V2 is to reduce uncontrolled iteration. Every task should make one unknown smaller, produce a recorded result, and leave the project easier to continue.

---

## Working Principles

### 1. Physical design leads

For a small underwater vehicle, the hard problems are sealing, buoyancy, balance, packaging, and power delivery. Firmware should support those decisions, not hide unresolved physical problems.

Before writing control logic for a behaviour, confirm that the physical system can perform that behaviour repeatably.

### 2. Test one variable at a time

Do not combine first-time tests. Avoid testing new seals, new electronics, new ballast, and new software in the same run.

A useful test should make it clear what passed or failed. If the result could have three unrelated causes, the test was too broad.

### 3. Validate the hull before installing electronics

The empty enclosure must pass a seal test before electronics go inside it.

Minimum sequence:

1. Dry fit.
2. Pressure or vacuum retention.
3. Static submersion.
4. Inspection for moisture.
5. Repeat after every hull modification.

### 4. Design for adjustment

Anything positional should be adjustable until the system is proven:

- Ballast location.
- Battery location.
- Chassis position.
- Trim weight.
- Tube routing.
- Sensor orientation.
- Motor alignment.

Fixed mounts are acceptable only after the adjustment range is known.

### 5. Lock orientation early

Orientation is a first-order constraint. Decide which side is up, where ballast sits, how the chassis is inserted, and how the vehicle should rest in water before detailed layout.

Changing orientation late invalidates too many downstream decisions.

### 6. Keep internal volume usable

A packed tube turns every change into a rebuild. V2 should leave clearance for insertion, wiring, ballast adjustment, inspection, and drying.

If a component makes the vehicle hard to assemble or service, treat that as a design problem rather than an inconvenience.

### 7. Use measured requirements

Avoid guessing where a quick measurement is possible.

Measure or estimate:

- Hull displacement.
- Required ballast volume.
- Centre of gravity.
- Motor current under load.
- Syringe actuation force.
- Battery runtime under representative use.
- Seal pressure or vacuum retention.

### 8. Record decisions when they are made

Notes should be written during the work, not reconstructed later. A useful entry states what was tried, what happened, what changed, and what decision follows.

Issues do not need a separate failure log. Record them in the build notes, test record, or V2 plan depending on where they affect the project.

---

## Task Pattern

Use this pattern for any V2 task:

1. State the question being answered.
2. Define the smallest test or build step that answers it.
3. Record the starting configuration.
4. Run the task.
5. Record the result.
6. Decide whether to keep, change, or discard the approach.
7. Update the relevant document before moving on.

If a task does not answer a concrete question or reduce a known risk, defer it.

---

## Documentation Rules

Use the documents this way:

| Document | Use |
|----------|-----|
| [build.md](./build.md) | V1 build record, component notes, and physical/electrical observations |
| [tests.md](./tests.md) | Submersion test history and future water-test protocol |
| [v2-plan.md](./v2-plan.md) | V2 requirements, blockers, experiments, and backlog |
| [approach.md](./approach.md) | Project-level working method for V2 |

Do not maintain a separate failure log. A failure should live where it is useful:

- A component or assembly failure belongs in `build.md`.
- A water-test failure belongs in `tests.md`.
- A future design requirement belongs in `v2-plan.md`.
- A repeated process lesson belongs in `approach.md`.

