# Scientific Work Approach

This document defines the general process to use across all projects in this repository.

Each project can add its own local `approach.md` when it needs project-specific rules, but those rules should build on this process rather than replace it.

---

## Working Principles

### 1. Start With the Question

Every build step, test, measurement, or analysis should answer a concrete question.

Good questions are specific enough that the result can change the next decision:

- How much ballast is required for neutral buoyancy?
- Does this material absorb more water than the control?
- Does this seal hold pressure for the target duration?

### 2. Separate Observation From Interpretation

Record what happened before explaining why it happened.

Observations should be direct:

- The vessel listed to port.
- The sample mass increased by 12g.
- Bubbles appeared at the lid joint.

Interpretation belongs in the conclusion:

- The ballast distribution was probably off-centre.
- The material absorbed moisture from the environment.
- The lid seal is a likely leak path.

### 3. Test One Main Variable at a Time

Avoid combining first-time changes unless the combined result will still be interpretable.

If a test changes the hardware, method, environment, and measurement tool at the same time, a failure will not explain which part was responsible.

### 4. Measure Before Optimising

Prefer measured values over intuition when a measurement is practical.

Record:

- Mass.
- Volume.
- Time.
- Temperature.
- Humidity.
- Current draw.
- Before/after states.
- Any other quantity that affects the conclusion.

If a value is estimated, label it as an estimate.

### 5. Preserve Useful Failures

A failed test is useful if it reduces uncertainty.

Do not hide failed attempts or overwrite them with only the later successful version. Record the configuration, result, likely cause, and decision that followed.

### 6. Carry Learning Forward

Every important finding should end up in one of three places:

- The test record, if it is an observation or result.
- The build record, if it affects physical or technical design.
- The forward plan, if it creates a future requirement, experiment, or unknown.

---

## Standard Task Pattern

Use this pattern for experimental work:

1. State the question being answered.
2. Define the smallest test or build step that can answer it.
3. Record the starting configuration.
4. Record the expected result or calculation, if there is one.
5. Run the test or build step.
6. Record measurements and observations.
7. Write the conclusion separately from the observations.
8. Decide what changes next.
9. Update the relevant documentation before moving on.

---

## Documentation Rules

Use the repository standard in [scientific-documentation-standard.md](./scientific-documentation-standard.md).

At minimum, every active project should have:

- A project `README.md`.
- One directory per version, phase, or experiment series.
- A build or method record.
- A test or measurement record.
- A forward plan when there are unresolved questions.

The root README is only an index. Project-specific evidence, photos, measurements, and decisions belong inside the relevant project directory.

---

## Agent Instructions

When an agent works in this repository, it should:

1. Read this file and the documentation standard first.
2. Inspect the relevant project directory before asking questions.
3. Preserve existing observations, measurements, and uncertainty.
4. Ask the human only for intent, missing experimental context, or ambiguous observations that cannot be inferred from the files.
5. Keep project-specific process notes inside the project, not in the root approach unless they apply across projects.
6. Update links whenever files are moved.
7. Run a Markdown/link sanity check when practical.
