---
name: ecc-lite-router
description: Route a user request to the smallest useful set of ECC Lite skills for Embedded, FPGA/Verilog, Data Science, code review, testing, and Git/GitHub work. Use whenever the user says "ECC Lite", asks to use this skill pack, or gives a mixed engineering task that spans more than one domain.
---

# ECC Lite Router

Act as the dispatcher for the ECC Lite skill pack.

The goal is not to activate every skill. Select the smallest chain that can solve and verify the task.

## Core rule

Use:
`understand task -> classify domain -> choose primary skill -> add support skills only when needed -> verify -> optionally Git`

## Available skills

### project-planner
Use when:
- the task is multi-step;
- a project/module needs decomposition;
- requirements or team responsibilities need structure;
- implementation order is unclear.

### datasheet-researcher
Use when:
- hardware facts are uncertain;
- register, pin, timing, voltage, protocol, API, or SDK behavior matters;
- the answer should be grounded in vendor/official documentation.

### embedded-debugger
Use when:
- ESP32/STM32/AVR/Arduino-class firmware fails;
- sensor readings are wrong;
- UART/I2C/SPI/ADC/timer/interrupt/RTOS behavior is incorrect;
- build, boot, reset, timing, memory, power, or GPIO issues appear.

### verilog-reviewer
Use when:
- the task involves Verilog, RTL, FPGA, testbench, waveform, FSM, synthesis, UCF/XDC, Xilinx ISE/ISim;
- width, reset, enable polarity, latch, blocking/non-blocking, or constraints may be wrong.

### data-science-reviewer
Use when:
- the task involves Python/Pandas/NumPy, EDA, preprocessing, ML evaluation, fraud detection, leakage, class imbalance, thresholds, Top-k, ROC/PR/F1;
- notebook code runs but correctness of the analysis is uncertain.

### code-reviewer
Use when:
- the user asks whether code/repo changes are correct;
- impact across files/functions must be assessed;
- defects should be ranked by severity;
- an unfamiliar repo needs reconnaissance before editing.

### test-verifier
Use after implementation/fix when:
- claims need evidence;
- build/simulation/test/hardware checks are required;
- regression or boundary cases should be verified.

### github-workflow
Use when:
- cloning, branch, commit, push, pull, merge, conflict, PR, repository hygiene, or Git history is part of the task;
- changes are ready to save/share.

## Routing table

| Request pattern | Primary | Support |
|---|---|---|
| New embedded project | project-planner | datasheet-researcher, embedded-debugger, test-verifier |
| ESP32/STM32/AVR bug | embedded-debugger | datasheet-researcher, test-verifier |
| Sensor/peripheral/API question | datasheet-researcher | embedded-debugger |
| Verilog/FPGA RTL or TB issue | verilog-reviewer | test-verifier |
| Data Science notebook/model review | data-science-reviewer | code-reviewer, test-verifier |
| General code review | code-reviewer | test-verifier |
| Unfamiliar repository | code-reviewer | project-planner |
| Save/share changes on GitHub | github-workflow | test-verifier |
| Mixed project request | project-planner | choose only relevant domain skills |

## Default chains

### Embedded
`project-planner? -> datasheet-researcher? -> embedded-debugger/implementation -> test-verifier -> code-reviewer? -> github-workflow?`

### FPGA
`project-planner? -> datasheet-researcher? -> verilog-reviewer -> test-verifier -> github-workflow?`

### Data Science
`project-planner? -> data-science-reviewer -> test-verifier -> code-reviewer? -> github-workflow?`

`?` means optional, not automatic.

## Decision rules

1. Choose one primary skill first.
2. Do not activate `project-planner` for trivial one-step questions.
3. Do not activate `datasheet-researcher` for facts already verified from the actual project/tool output unless external documentation is needed.
4. Add `test-verifier` whenever code/config/RTL is changed or a fix is claimed.
5. Add `github-workflow` only when repository operations are requested or the user wants changes saved/shared.
6. Prefer domain reviewers over generic `code-reviewer` when the defect is domain-specific.
7. If a task mixes domains, sequence skills by dependency rather than running all of them conceptually at once.

## ChatGPT usage convention

When the user writes:

`@GitHub ECC Lite: <request>`

Treat it as:
1. read/use this router;
2. select the relevant skill(s) from this repository;
3. inspect the target repository/files through GitHub when the request depends on them;
4. execute the task;
5. state which ECC Lite skills were actually used when that helps the user understand the workflow.

Do not require the user to memorize individual skill names.

## Examples

`@GitHub ECC Lite: ESP32 của tôi đọc DHT22 lúc được lúc không`
→ `embedded-debugger + datasheet-researcher + test-verifier`

`@GitHub ECC Lite: kiểm tra testbench decoder 3-to-8`
→ `verilog-reviewer + test-verifier`

`@GitHub ECC Lite: xem notebook fraud detection này có leakage không`
→ `data-science-reviewer + code-reviewer`

`@GitHub ECC Lite: repo này mới clone, chỉ tôi bắt đầu từ đâu`
→ `code-reviewer + project-planner`

`@GitHub ECC Lite: sửa xong rồi commit lên GitHub`
→ relevant domain skill + `test-verifier + github-workflow`

## Guardrails

- Do not claim a skill was used unless its instructions were actually consulted/applied.
- Do not substitute GitHub access for domain verification.
- Do not invent repository contents.
- Do not activate extra skills merely to make the workflow look more sophisticated.
- Evidence and verification take priority over number of skills used.
