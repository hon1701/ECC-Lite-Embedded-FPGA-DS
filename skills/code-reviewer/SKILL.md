---
name: code-reviewer
description: Review code changes or an unfamiliar repository for correctness, maintainability, safety, tests, and unintended behavior. Use for C/C++, Python, firmware, scripts, pull requests, or when the user asks whether code is correct. Search first, read selectively, and report issues in severity order.
---

# Code Reviewer

Review for defects, not style theater.

## Phase 1 — Understand before judging
Identify:
- task/requirement;
- changed files;
- entry points;
- callers/callees;
- build/test path.

For an unfamiliar repo, do reconnaissance first:
- list top-level structure;
- inspect build manifests/config;
- find main/top entry point;
- search symbols and references;
- read only the files needed to establish the flow.

Do not read every file.

## Phase 2 — Search impact
For every changed public function, module, pin mapping, schema, or interface:
- find references;
- identify consumers;
- check assumptions at boundaries.

## Phase 3 — Review by severity

### Critical
Could cause:
- hardware damage;
- credential exposure;
- data corruption;
- undefined behavior with serious impact;
- completely wrong model evaluation;
- unsafe merge/deployment.

### High
Likely functional bug:
- wrong condition;
- race/timing failure;
- buffer/index error;
- wrong register/API usage;
- latch/FSM error;
- data leakage.

### Medium
Maintainability/reliability problem:
- duplicated logic;
- unclear ownership;
- missing error handling;
- fragile hard-coded values;
- insufficient tests.

### Low
Clarity/style issue with limited behavioral impact.

## Embedded checks
- bounds and buffer sizes;
- `volatile` where hardware/ISR semantics require it;
- ISR-safe operations;
- blocking delays;
- timer arithmetic;
- integer width/overflow;
- shared state/concurrency;
- pin/peripheral ownership;
- error return handling.

## Python checks
- exception handling;
- path assumptions;
- mutability;
- dtype/index behavior;
- reproducibility;
- leakage in DS code.

## Review output
For each issue:
`[severity] file:line — problem`
- Why it matters
- Evidence/reproduction
- Minimal fix
- Test that proves the fix

Then:
- Open questions
- Positive/verified aspects
- Final verdict: `safe / safe with fixes / not safe yet`

## Guardrails
- Do not claim a bug without enough evidence.
- Prefer concrete defects over subjective formatting.
- Do not rewrite working code just to match personal taste.
- Verify repository conventions before enforcing them.

## Related skills
- `github-workflow`
- `test-verifier`
- `embedded-debugger`
- `verilog-reviewer`
- `data-science-reviewer`
