---
name: verilog-reviewer
description: Review and debug Verilog RTL and testbenches for combinational/sequential correctness, simulation behavior, synthesis safety, widths, reset/clock logic, case completeness, and FPGA constraints. Use for Xilinx ISE/ISim or similar FPGA coursework and RTL projects.
---

# Verilog Reviewer

Review RTL by separating:
`specification -> RTL -> testbench -> waveform -> constraints`.

## 1. Reconstruct the specification
Determine:
- inputs/outputs and widths;
- active-high/active-low behavior;
- combinational vs sequential;
- truth table/state transitions;
- clock/reset behavior.

If the specification is unclear, do not infer functionality from faulty RTL alone.

## 2. Syntax and elaboration checks
Inspect:
- missing `;`, `end`, `endcase`;
- port-name/case mismatches;
- wrong module instance ports;
- `wire` vs `reg` in Verilog;
- undeclared signals;
- width truncation/extension.

## 3. Combinational logic checks
For `always @(*)`:
- assign every output on every path;
- use blocking `=`;
- provide default assignments where needed;
- ensure `case` covers required values;
- avoid unintended latches.

`default` is not mandatory when all input combinations are covered and outputs are assigned, but it is often useful for defensive handling of X/Z or future changes.

## 4. Sequential logic checks
For clocked blocks:
- use non-blocking `<=`;
- confirm edge (`posedge`/`negedge`);
- confirm reset polarity;
- avoid assigning the same register from multiple procedural blocks;
- separate next-state logic when an FSM becomes complex.

## 5. Width and signedness
Check every literal and expression:
- `2'b11` fits 2 bits;
- assigning `3'b111` to 2 bits truncates;
- unsized integer literals can change expression width;
- signed/unsigned comparisons can surprise.

## 6. Testbench review
A good TB should:
- initialize every driven input;
- wait deterministically;
- cover every truth-table/state case;
- include enable/reset cases;
- include boundary/invalid cases where relevant;
- make expected results easy to compare.

For small combinational circuits, exhaustive enumeration is preferred.

## 7. Waveform interpretation
Read in this order:
1. time axis;
2. stimulus inputs;
3. enable/reset;
4. outputs;
5. transition boundaries.

Compare each stable input interval against the truth table, not against visual intuition.

## 8. FPGA constraints
Verify:
- exact top-level port names;
- device/package;
- UCF/XDC syntax;
- LOC mapping;
- pull-up/pull-down;
- active-low board LEDs/buttons.

## Output format
- Spec summary
- RTL issues
- TB issues
- Constraint issues
- Exact fix
- Expected waveform behavior
- Verification checklist

## Related skills
- `project-planner`
- `test-verifier`
- `code-reviewer`
