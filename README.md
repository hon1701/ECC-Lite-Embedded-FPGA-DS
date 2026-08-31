# ECC Lite — Embedded / FPGA / Data Science

A compact skill pack adapted from workflow ideas in Everything Claude Code (ECC), specialized for:
- Embedded firmware (ESP32 / STM32 / AVR)
- Verilog / FPGA
- Python / Pandas / NumPy / classical ML
- Git / GitHub
- Planning, debugging, review, and verification

This pack intentionally excludes web/frontend/marketing/agent-orchestration material.

## Included skills

1. `project-planner`
2. `datasheet-researcher`
3. `embedded-debugger`
4. `verilog-reviewer`
5. `data-science-reviewer`
6. `code-reviewer`
7. `test-verifier`
8. `github-workflow`

Shared rule:
- `rules/engineering-standards.md`

## Recommended automatic workflow

For a new task:

`project-planner`
→ `datasheet-researcher` when technical facts are uncertain
→ implementation
→ domain reviewer/debugger
→ `test-verifier`
→ `code-reviewer`
→ `github-workflow`

### Embedded
`project-planner → datasheet-researcher → embedded-debugger → test-verifier → code-reviewer`

### FPGA
`project-planner → datasheet-researcher → verilog-reviewer → test-verifier → code-reviewer`

### Data Science
`project-planner → data-science-reviewer → test-verifier → code-reviewer`

## Claude Code installation

Project-level:
```bash
mkdir -p .claude/skills .claude/rules
cp -r skills/* .claude/skills/
cp rules/engineering-standards.md .claude/rules/
```

User-level:
```bash
mkdir -p ~/.claude/skills ~/.claude/rules
cp -r skills/* ~/.claude/skills/
cp rules/engineering-standards.md ~/.claude/rules/
```

On Windows PowerShell, copy the folders into:
- project: `.claude\skills\` and `.claude\rules\`
- user: `$HOME\.claude\skills\` and `$HOME\.claude\rules\`

Each skill uses a descriptive `description` field so a compatible harness can auto-select it from the task context. You can also explicitly request the skill by name when your harness supports that behavior.

## How to use effectively

Do not activate all eight at once. Use the smallest chain that fits the problem.

Examples:

**"ESP32 đọc DHT22 lúc được lúc không"**
- `embedded-debugger`
- `datasheet-researcher` if timing/electrical facts are uncertain
- `test-verifier` after the fix

**"Kiểm tra testbench decoder 3→8"**
- `verilog-reviewer`
- `test-verifier`

**"Notebook fraud detection của tôi có đúng không?"**
- `data-science-reviewer`
- `code-reviewer`
- `test-verifier`

**"Repo này tôi mới clone, bắt đầu ở đâu?"**
- `project-planner`
- `code-reviewer` (its reconnaissance/search phase)

## Design choices

The pack keeps several useful ECC principles:
- reconnaissance/search before reading an entire repository;
- evidence instead of guessing;
- explicit activation conditions;
- verification gates after implementation;
- review focused on correctness and risk;
- small, reviewable Git changes.

The implementation is rewritten and specialized rather than copied verbatim from ECC.

## Attribution

Workflow concepts were adapted from:
Everything Claude Code (ECC), `affaan-m/ECC`, MIT-licensed portions where applicable.

Reference:
https://github.com/affaan-m/ECC
