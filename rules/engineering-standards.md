# Engineering Rules

These rules apply across all skills.

## Evidence before assumption
- Read the actual error, code, config, waveform, dataset, datasheet, or tool output before concluding.
- Mark unknowns. Do not fabricate pin mappings, register values, API signatures, metrics, or test results.

## Minimal change
- Fix the root cause with the smallest change that preserves intended behavior.
- Avoid unrelated refactors while debugging.

## Build warnings matter
- Treat warnings as diagnostic evidence. Explain which are harmless and which need fixes.

## Hardware safety
- Check voltage, current, pin mode, common ground, and actuator drive requirements before suggesting wiring changes.
- Do not confuse absolute maximum ratings with normal operating conditions.

## Embedded code
- Keep ISRs short.
- Avoid blocking timing-sensitive execution paths.
- Check integer width, overflow, shared-state access, and error returns.
- Prefer named constants/configuration over unexplained magic values.

## Verilog
- Blocking assignments for combinational procedural logic.
- Non-blocking assignments for sequential logic.
- No inferred latch unless explicitly intended.
- Verify signal width, reset polarity, enable polarity, and constraints.

## Data Science
- Split before fitting learned preprocessing.
- Check leakage.
- Use metrics appropriate to the actual class balance and operational decision.
- Keep experimental conclusions reproducible.

## Verification
A task is not "done" merely because code was written.
Report exactly what was:
- built;
- simulated;
- tested;
- run on hardware;
- not verified.
