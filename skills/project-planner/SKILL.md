---
name: project-planner
description: Break an embedded, FPGA, data-science, or software task into a small implementation plan with acceptance criteria, dependencies, test points, and a safe execution order. Use before non-trivial implementation, project decomposition, team task assignment, or when requirements are vague.
---

# Project Planner

Turn a request into an implementation-ready plan. Prefer the smallest plan that can be verified.

## Activate when
- A feature spans multiple files/modules.
- A firmware/FPGA project needs module boundaries.
- A Data Science task needs a workflow from data to evaluation.
- The user asks what to do first, how to divide work, or how to assign tasks.
- Requirements are incomplete enough that implementation could drift.

## Workflow

### 1. State the target
Write one sentence:
`Build/change <thing> so that <observable outcome>.`

### 2. Extract constraints
Identify only constraints supported by the task or repository:
- target MCU/board/toolchain;
- timing/resource constraints;
- required libraries/frameworks;
- deliverables;
- test/demo requirements;
- explicit exclusions.

Do not invent hardware, cloud services, frameworks, or features.

### 3. Map modules
For embedded projects, prefer boundaries such as:
- `drivers/`: sensor/actuator/peripheral access;
- `services/`: application logic;
- `app/`: orchestration/state machine;
- `platform/`: board/RTOS/HAL adaptation;
- `tests/`: host or target tests.

For FPGA:
- datapath;
- control/FSM;
- interface modules;
- top;
- testbench.

For Data Science:
- data loading;
- cleaning;
- EDA;
- feature engineering;
- split;
- modeling;
- evaluation;
- reporting.

### 4. Define acceptance criteria
Each criterion must be observable.

Bad:
- "MQ-2 works."

Good:
- "When the sensor reading exceeds the configured threshold for N consecutive samples, the alarm state becomes active and the buzzer output is asserted."

### 5. Produce execution order
Use dependency order:
`inspect -> research -> implement smallest unit -> build/simulate -> test -> integrate -> verify`.

### 6. Identify risks
Keep only concrete risks:
- voltage/current mismatch;
- blocking delays;
- ISR misuse;
- race/resource conflict;
- clock/reset issue;
- latch or width mismatch;
- data leakage;
- wrong metric;
- train/test contamination.

## Output format
1. Goal
2. Current assumptions
3. Module map
4. Ordered implementation steps
5. Test/verification points
6. Risks
7. Definition of Done

## Guardrails
- Do not begin coding before interfaces and acceptance criteria are clear enough.
- Do not expand scope merely because an improvement is possible.
- Prefer 3–8 implementation steps over a huge backlog.
- Mark unknowns instead of guessing.

## Related skills
- `datasheet-researcher`
- `embedded-debugger`
- `test-verifier`
- `code-reviewer`
