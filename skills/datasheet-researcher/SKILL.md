---
name: datasheet-researcher
description: Research MCU, sensor, peripheral, protocol, FPGA, library, or API behavior from authoritative documentation before implementation. Use for register meanings, electrical limits, timing, pin functions, protocol details, ESP-IDF/HAL APIs, or any technical fact where guessing could break hardware or code.
---

# Datasheet Researcher

Evidence first. Prefer primary documentation over memory or random examples.

## Source priority
1. MCU/sensor/FPGA vendor datasheet.
2. Reference manual / technical reference manual.
3. Official SDK/framework documentation.
4. Official example repository.
5. Trusted secondary source only when primary sources are insufficient.

## Workflow

### 1. Form the exact question
Examples:
- What voltage range is valid for this pin?
- Which register controls Timer1 prescaler?
- Is this ESP-IDF API ISR-safe?
- What are setup/hold requirements?
- Is a signal active-high or active-low?

### 2. Identify the exact part/version
Do not mix:
- ESP32 vs ESP32-S3;
- ATmega328P vs another AVR;
- STM32F103 vs STM32F4;
- Vivado vs ISE behavior;
- ESP-IDF versions;
- sensor modules vs bare sensor ICs.

### 3. Extract only implementation-relevant facts
Capture:
- parameter/register/API;
- allowed values;
- units;
- reset/default state;
- timing/electrical limits;
- caveats;
- source section/page/link when available.

### 4. Cross-check contradictions
If a tutorial conflicts with the vendor manual, trust the vendor manual unless an erratum/version note explains the difference.

### 5. Convert evidence into action
Example:
`datasheet fact -> design implication -> code/test consequence`.

## Embedded checklist
- supply voltage;
- GPIO logic levels;
- current limits;
- pull-up/pull-down needs;
- ADC range/attenuation;
- clock/prescaler;
- interrupt constraints;
- peripheral pin mux;
- sensor warm-up/calibration;
- timing tolerances.

## FPGA checklist
- clock frequency/period;
- reset polarity/synchronicity;
- IO standard;
- active-low signals;
- width/signedness;
- device/package constraints.

## Guardrails
- Never invent register addresses, bit positions, pin mappings, or API signatures.
- Distinguish absolute maximum ratings from recommended operating conditions.
- Distinguish module-board specifications from the underlying IC.
- State uncertainty explicitly.

## Related skills
- `project-planner`
- `embedded-debugger`
- `verilog-reviewer`
