# ECC Lite — Embedded / FPGA / Data Science

A compact skill pack adapted from workflow ideas in Everything Claude Code (ECC), specialized for:
- Embedded firmware (ESP32 / STM32 / AVR)
- Verilog / FPGA
- Python / Pandas / NumPy / classical ML
- Git / GitHub
- Planning, debugging, review, and verification

This pack intentionally excludes web/frontend/marketing/agent-orchestration material.

## Quick use in ChatGPT

Use this short convention:

`@GitHub ECC Lite: <your request>`

Examples:

`@GitHub ECC Lite: kiểm tra project ESP32 này và tìm nguyên nhân cảm biến đọc sai`

`@GitHub ECC Lite: xem testbench decoder 3-to-8 này có đúng không`

`@GitHub ECC Lite: review notebook fraud detection và kiểm tra leakage`

`@GitHub ECC Lite: sửa xong rồi kiểm tra và commit lên GitHub`

The `ecc-lite-router` skill is the dispatcher. It selects the smallest useful skill chain, so you do not need to remember every skill name.

Important: storing this repository on GitHub does not globally install the skills into ChatGPT. The `@GitHub ECC Lite: ...` convention tells the assistant to consult this repository/router when the task uses GitHub-connected data. In environments that support local skill discovery, install the `skills/` folder so the skill descriptions can be discovered automatically.

## Included skills

Router:
- `ecc-lite-router` — classify the request and choose the required skills.

Domain/workflow skills:
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

The router follows this principle:

`understand task → choose primary skill → add only needed support skills → verify → Git if requested`

### Embedded
`project-planner? → datasheet-researcher? → embedded-debugger → test-verifier → code-reviewer? → github-workflow?`

### FPGA
`project-planner? → datasheet-researcher? → verilog-reviewer → test-verifier → github-workflow?`

### Data Science
`project-planner? → data-science-reviewer → test-verifier → code-reviewer? → github-workflow?`

`?` means optional. The router should not activate every skill automatically.

## Routing examples

| Request | Skills selected |
|---|---|
| ESP32 sensor behaves intermittently | `embedded-debugger`, optionally `datasheet-researcher`, then `test-verifier` |
| STM32 timer/interrupt issue | `embedded-debugger`, `datasheet-researcher`, `test-verifier` |
| Verilog RTL/testbench issue | `verilog-reviewer`, `test-verifier` |
| Fraud Detection notebook review | `data-science-reviewer`, optionally `code-reviewer`, `test-verifier` |
| Unfamiliar repository | `code-reviewer`, optionally `project-planner` |
| Commit/push/PR after a fix | domain skill, `test-verifier`, `github-workflow` |

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

Do not activate all skills at once. Use the smallest chain that fits the problem.

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
- `code-reviewer` when code-level impact needs inspection
- `test-verifier`

**"Repo này tôi mới clone, bắt đầu ở đâu?"**
- `code-reviewer` reconnaissance
- `project-planner` when an implementation plan is needed

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
