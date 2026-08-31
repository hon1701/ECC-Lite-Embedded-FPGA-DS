---
name: test-verifier
description: Verify a change after implementation using build, lint/static checks, simulation, targeted tests, hardware checks, and regression tests appropriate to firmware, FPGA, Python, or Data Science. Use after fixes/features, before commits/PRs, and whenever 'it works' needs evidence.
---

# Test Verifier

No completion claim without observable verification.

## Verification ladder
Run only applicable gates, in this order:

1. Configuration sanity
2. Build/compile/elaborate
3. Static warnings/lint
4. Unit/module test
5. Integration/simulation
6. Boundary/error test
7. Regression
8. Hardware/demo validation
9. Final evidence summary

Stop and fix a failed foundational gate before trusting later gates.

## Firmware verification
At minimum consider:
- clean build;
- warnings reviewed;
- boot log;
- nominal sensor/input;
- lower/upper threshold boundary;
- disconnected/invalid input when safe;
- repeated operation;
- reset/reboot;
- actuator safe state;
- timing if relevant.

For hardware, record:
`stimulus -> expected -> observed -> pass/fail`.

## FPGA verification
- syntax/elaboration;
- simulation;
- exhaustive combinations for small combinational blocks;
- reset and state transitions for sequential blocks;
- waveform check;
- synthesis warnings;
- constraint/top-port match;
- board test if hardware is available.

## Data Science verification
- notebook/script runs from a clean state;
- deterministic split where expected;
- assertions on shapes/schema;
- no train/test leakage;
- score sanity;
- metric recomputation;
- baseline comparison;
- results persisted/reported from the same run.

## Regression principle
A bug fix needs:
1. a test/experiment that fails before the fix when feasible;
2. the same check passing after the fix;
3. a nearby case to ensure the fix did not merely hard-code one input.

## Verification report
Use:

### Build
PASS/FAIL + command/tool + key result

### Tests
PASS/FAIL + cases executed

### Warnings
None / reviewed list

### Hardware or simulation
Stimulus and observed output

### Remaining gaps
Anything not tested

### Verdict
`verified`, `partially verified`, or `not verified`.

## Guardrails
- Do not treat successful compilation as proof of functional correctness.
- Do not hide warnings.
- Do not claim hardware verification if only simulation was performed.
- Do not claim full test coverage unless measured.

## Related skills
- `embedded-debugger`
- `verilog-reviewer`
- `data-science-reviewer`
- `code-reviewer`
