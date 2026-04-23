# Scientific Project Documentation Standard

This document describes the documentation structure used in this project so it can be reused by another agent or collaborator on other experimental, scientific, or engineering projects.

The aim is to preserve the reasoning trail: what was built, what was tested, what happened, what was learned, and what that means for the next version.

---

## Core Principles

1. **Document the iteration, not just the result**
   - Record failed attempts, partial successes, constraints, and abandoned ideas.
   - Treat the documentation as part lab notebook, part build record, and part forward plan.

2. **Separate build facts from test facts**
   - Component choices, construction details, and observed design problems belong in the build record.
   - Experimental setup, observations, measurements, and conclusions belong in the test record.

3. **Make every test answer a question**
   - Each test should state the question it is trying to answer.
   - Avoid combining first-time tests unless the combined result will still be interpretable.

4. **Carry learning forward explicitly**
   - Every major issue should become either a future requirement, a planned experiment, or a design principle.
   - Do not leave lessons buried only in prose.

5. **Prefer measured unknowns over guessed conclusions**
   - If a quantity matters, record how it was measured or why it remains unknown.
   - Preserve assumptions separately from confirmed results.

---

## Recommended Repository Structure

Use a top-level repository README, one directory per project, and one subdirectory per major version, phase, or experimental build.

```text
README.md
approach.md
scientific-documentation-standard.md
projects/
  project-name/
    README.md
    project-v1/
      README.md
      build.md
      tests.md
      v2-plan.md
      approach.md
      images/
```

For non-versioned scientific work, replace `project-v1` with a phase, campaign, or experiment name:

```text
projects/
  project-name/
    experiment-2026-04/
    prototype-a/
    field-trial-1/
```

---

## Top-Level README

The root `README.md` gives repository-level orientation.

Include:

- Repository purpose.
- The working philosophy.
- A projects table.
- Links to shared documentation.
- A brief repository structure summary.

Recommended sections:

```markdown
# Scientific Experiments

Short description of the repository.

Brief note on preserving the reasoning trail.

## Projects

| Project | Status | Notes |
|---------|--------|-------|
| [Project Name](./projects/project-name/README.md) | Active | Short summary |

## Shared Documentation

- [Approach](./approach.md)
- [Scientific documentation standard](./scientific-documentation-standard.md)
```

---

## Project README

Each project gets a `README.md`. This gives project-level orientation before the reader enters a specific version or phase.

Include:

- Project name and one-paragraph description.
- What kind of project this is: prototype, experiment, field study, analysis, build log, etc.
- Inspiration or external references, if relevant.
- A versions/phases table.
- Current direction and links to active version/phase docs.

Recommended sections:

```markdown
# Project Name

Short description.

## Inspiration

Relevant external references or origin story.

## Versions

| Version / Phase | Status | Notes |
|-----------------|--------|-------|
| [V1](./project-v1/README.md) | Measurement / planning | Short summary |

## Current Direction

- Main unresolved problem.
- Next planned investigation.
- Important constraints.
```

---

## Version / Phase README

Each version or phase gets its own `README.md`. This is the narrative overview for that iteration.

Include:

- What this version or phase was meant to achieve.
- Objective table with status.
- Current or final status.
- What works.
- What does not work.
- Document index.
- Guidance on which file to use for which type of information.

Recommended sections:

```markdown
# Project V1

This directory records [version/phase].

## What Was V1?

Short narrative overview.

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Objective | ✅ / ⚠️ / ❌ status and note |

## Current Status

Plain-language summary of where this iteration stands.

## What Works

- Confirmed capability.

## What Doesn't

- Known limitation.

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | Build record and component notes |
| [tests.md](./tests.md) | Test history and planned tests |
| [v2-plan.md](./v2-plan.md) | Forward planning |
| [approach.md](./approach.md) | Working method |
```

Use careful status language. Avoid calling an experimental version a total failure if it can still answer useful measurement questions.

---

## Build Record

`build.md` records what exists physically or technically.

Use it for:

- System overview.
- Parts list.
- Construction details.
- Photos and captions.
- Subsystem notes.
- Component-level issues.
- Design limitations.
- Improvements for the next build.

Recommended structure:

```markdown
# Project V1 — Build Documentation

## System Overview

| Subsystem | Description |
|-----------|-------------|

## Parts List

Grouped by subsystem.

# Subsystem Name

## Overview

What this subsystem does and how it was built.

## Images

![Short image description](images/example.jpg)
*Caption explaining what the image shows and why it matters.*

## Issues

### Specific Issue Name

What happened, why it matters, and what remains unknown.

## Next Build — Subsystem Improvements

- [ ] Specific future improvement.
```

Guidelines:

- Put issues close to the subsystem they affect.
- Use photos as evidence, not decoration.
- Captions should explain what a future reader should notice.
- Record placeholders as `[TBC — specific missing fact]`, not just `[TBC]`.

---

## Test Record

`tests.md` records experiments, trials, measurements, and observations.

Use it for:

- Test history.
- Planned tests.
- Measurements.
- Observations.
- Conclusions.
- Decisions made after tests.
- Future test protocols.

Recommended structure:

```markdown
# Project V1 — Testing Record

This file records tests performed during V1 and observations that carry forward.

## Summary

Short synthesis of the main experimental outcomes.

## Test Record

### T1 — Test Name

**Date:** [YYYY-MM-DD, time if useful]

**Goal:**
The question this test answers.

**Setup:**
- Exact hardware/software/material configuration.
- Environment.
- Measurement tools.

**Measurements to Record:**
- Quantities that must be captured.

**Result:**
What happened.

**Observations:**
- Direct observations.

**Conclusion:**
Interpretation of the result.

**Issues to Carry Forward:**
- Requirement, redesign need, or planned follow-up.

**Decision Made After Test:**
What changes because of this test.
```

For planned tests, include:

- Pass condition.
- Out-of-scope items.
- Decision to make after the test.

This prevents a planned test from becoming an uncontrolled trial.

---

## Forward Plan

Use `v2-plan.md`, `next-plan.md`, or equivalent to convert lessons into future work.

Include:

- Blockers that must be solved.
- Improvements that are useful but not blockers.
- Experiments to run.
- Unknowns.
- Design principles.
- Backlog ideas.

Recommended structure:

```markdown
# Project V2 — Forward Plan

> Derived from the previous build record, test record, and unresolved problems.

## Must-Fix

| # | Issue | Source |
|---|-------|--------|

## Improvements

| Area | Improvement | Notes |
|------|-------------|-------|

## Experiments to Run

| Experiment | Goal |
|------------|------|

## Unknowns

- [ ] Question that needs answering.

## Design Principles

1. Principle derived from evidence.

## Backlog / Ideas

- [ ] Lower-priority future idea.
```

Each blocker should cite where it came from, usually `build.md` or `tests.md`.

---

## Approach Document

`approach.md` records the working method. It should be project-level, not a task list.

Use it for:

- Testing philosophy.
- Design principles.
- Measurement rules.
- Documentation rules.
- The standard task pattern.

Recommended sections:

```markdown
# Project V2 — Project Approach

## Working Principles

### 1. Principle Name

Short explanation.

## Task Pattern

1. State the question being answered.
2. Define the smallest test or build step that answers it.
3. Record the starting configuration.
4. Run the task.
5. Record the result.
6. Decide whether to keep, change, or discard the approach.
7. Update the relevant document before moving on.

## Documentation Rules

| Document | Use |
|----------|-----|
```

---

## Image Handling

Store images inside the relevant project phase directory:

```text
projects/project-name/project-v1/images/
```

Rules:

- Use relative links from Markdown files.
- Give every image a meaningful alt text.
- Add a caption under every image.
- Captions should identify the component, viewpoint, state, and reason the image matters.
- Prefer original photos for physical projects.

Example:

```markdown
![Internal chassis side profile](images/chassis-side.jpg)
*Side view of the internal chassis removed from the hull. The actuator is visible on the left, with the power system mounted below the main frame.*
```

---

## Writing Style

- Be factual and specific.
- Distinguish observations from conclusions.
- Say when something is unknown.
- Do not over-polish away useful uncertainty.
- Prefer short sections with clear headings.
- Use tables for status, parts, blockers, and experiment lists.
- Use checkboxes for unresolved work.
- Avoid vague issue names like "Problem" or "Failure"; name the actual failure mode.

Good:

```markdown
### Seal Compression — Insufficient at Lid Joint
```

Less useful:

```markdown
### Problem With Seal
```

---

## Agent Workflow

When another agent applies this structure to a project, it should work in this order:

1. Read the root README and existing docs.
2. Inventory files, images, test notes, and any build artifacts.
3. Identify the project phases or versions.
4. Create or update the root README.
5. Create or update the phase README.
6. Build the `build.md` from physical/technical facts.
7. Build the `tests.md` from experiments and observations.
8. Convert unresolved issues into the forward plan.
9. Capture project-level working rules in `approach.md`.
10. Cross-check links, terminology, statuses, and repeated claims.

The agent should ask the human only for information that cannot be discovered from the repo or artifacts, such as:

- Why a decision was made.
- What happened during an undocumented test.
- Whether a planned test is still intended.
- The meaning of ambiguous images or measurements.

---

## Completion Checklist

Use this checklist before considering the documentation complete:

- [ ] Root README explains the project and links to the active docs.
- [ ] Each version or phase has an overview README.
- [ ] Build facts are separated from test facts.
- [ ] Every major test has goal, setup, result, observations, conclusion, and decision.
- [ ] Planned tests include pass conditions and out-of-scope items.
- [ ] Every major unresolved problem appears in the forward plan.
- [ ] Blockers cite their source docs.
- [ ] Images have useful alt text and captions.
- [ ] Unknowns are explicitly marked.
- [ ] Terminology is consistent across files.
- [ ] Links work.
- [ ] The docs explain what to do next.
