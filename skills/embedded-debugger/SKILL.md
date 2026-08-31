---
name: embedded-debugger
description: Systematically debug C/C++ firmware and embedded behavior on ESP32, STM32, AVR, Arduino-class boards, sensors, buses, interrupts, timers, and RTOS code. Use when builds fail, peripherals misbehave, readings are wrong, resets occur, timing is unstable, or hardware and software disagree.
---

# Embedded Debugger

Use the loop:
`reproduce -> classify -> isolate -> measure -> hypothesize -> change one thing -> verify`.

## 1. Classify the failure
Choose the primary class:
- compile/link;
- flash/programming;
- boot/reset;
- GPIO;
- ADC/sensor;
- UART/I2C/SPI;
- timer/PWM;
- interrupt;
- RTOS/concurrency;
- memory;
- timing;
- power/electrical;
- logic/state machine.

## 2. Preserve evidence
Before editing, capture:
- exact error/warning;
- serial log;
- relevant code;
- pin map;
- expected behavior;
- observed behavior;
- reproducible steps.

Do not paraphrase away compiler diagnostics.

## 3. Reduce the system
Create the smallest failing path:
- one peripheral;
- one task;
- one input;
- fixed test value;
- no network/cloud/UI unless necessary.

## 4. Check layers in order
### Layer A — Build/toolchain
- correct target/board;
- correct headers/config;
- linker symbols;
- warnings;
- stale build artifacts.

### Layer B — Electrical
- common ground;
- supply voltage;
- logic level;
- pin direction;
- pull resistors;
- current demand;
- correct physical pin.

### Layer C — Peripheral configuration
- clock enabled;
- pin mux;
- mode;
- frequency;
- resolution;
- prescaler;
- address/baud;
- interrupt flags.

### Layer D — Application logic
- thresholds;
- state transitions;
- stale variables;
- integer truncation;
- overflow;
- blocking delay;
- race conditions.

## 5. Build hypotheses
Rank by evidence, not convenience. Test the cheapest/highest-probability hypothesis first.

## 6. Change one variable
Avoid large rewrites during diagnosis.

## 7. Verify
Re-run the same reproduction and at least one boundary/error case.

## ESP32 notes
- Check ESP-IDF target/config before changing code.
- Do not call non-ISR-safe APIs inside ISR context.
- Avoid long blocking work in callbacks/tasks that own timing-sensitive paths.
- Distinguish GPIO number from board silk-screen labels.

## AVR/STM32 notes
- Verify clock assumptions before timer/baud calculations.
- Inspect register bitfields against the exact MCU reference manual.
- Clear/handle interrupt flags as required by the peripheral.

## Output format
1. Symptom
2. Evidence
3. Most likely layer
4. Hypotheses ranked
5. Minimal experiment
6. Fix
7. Verification result
8. Remaining risk

## Related skills
- `datasheet-researcher`
- `test-verifier`
- `code-reviewer`
