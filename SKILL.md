---
name: pm-dev-workflow
description: >-
  Use when a user asks to build, modify, or ship a software feature and benefits
  from product-manager-grade delivery discipline. Enforces a pragmatic PM-to-dev
  workflow: clarify intent, surface product/technical risks, define scope and
  success criteria, plan implementation, build, self-test, and hand off with
  clear validation steps. Trigger on requests like "build this feature",
  "make an app/system/tool", "add/modify a function", "turn this requirement
  into code", or "help me ship this".
---

# PM Dev Workflow

## Purpose

Turn vague product requests into shipped, tested work without skipping product thinking. Optimize for non-technical or semi-technical stakeholders who need the agent to make good technical decisions, explain tradeoffs clearly, and deliver something they can verify.

## Core Rules

- Do not jump straight into code for medium or large requests.
- Keep momentum: ask only blocking questions; otherwise state assumptions and proceed.
- Surface useful product and technical suggestions before implementation.
- Maintain durable context for medium/large work.
- Self-test before handoff.
- End with user-verifiable delivery steps.

## 0. Restore Existing Context

If `.dev-context.md` exists in the project root, read it before deciding next steps. Summarize current state in one sentence, then continue.

## 1. Classify Request Size

Classify quickly:

| Size | Examples | Workflow |
|---|---|---|
| Tiny | Copy, style, config, obvious one-line fix | Confirm understanding in one sentence, then implement. |
| Small | One isolated bug or simple UI/function change | Briefly state scope and implement. |
| Medium | New single feature, 1-2 modules, user-facing behavior | Clarify only blockers, propose approach, create/update context, plan, build, test. |
| Large | New app/system, database/auth/payment, multi-module workflow | Full workflow with explicit scope, milestones, risks, and confirmation before build. |

When unsure, choose the smaller workflow unless the change risks data loss, security, money, privacy, public release, or significant rework.

## 2. Product Clarification

For medium/large requests, first produce a short product framing:

- **Goal:** What user/business problem is being solved.
- **Primary user:** Who uses it and in what scenario.
- **MVP scope:** What must be in v1 and what should wait.
- **Success signal:** Metric, behavior, or acceptance condition.
- **Constraints:** Platform, data, auth, design, deadline, compliance, dependencies.

Ask at most 1-3 blocking questions. If answers are not required, state assumptions and continue.

## 3. Proactive Suggestions

Before implementation, provide 1-3 concrete suggestions that reduce rework or improve the product. Prefer specific observations:

- Hidden dependency: "This needs login state; I will use existing session handling if present."
- Data/metrics: "If this affects conversion, add events now instead of retrofitting later."
- Scope trim: "For v1, avoid admin roles and ship single-owner projects first."
- Technical risk: "Generating arbitrary HTML needs sandboxing."
- UX edge case: "Empty/error/loading states need explicit copy."

Avoid generic questions like "Do you have any other ideas?"

## 4. Durable Context for Medium/Large Work

Create or update `.dev-context.md` in the project root for medium/large tasks:

```markdown
# Project: [name]

## Original Request
[user request]

## Confirmed Scope
[what will be built now]

## Assumptions
- ...

## Technical Approach
[stack, architecture, key decisions]

## Product Requirements
- User:
- Goal:
- MVP:
- Success signal:
- Out of scope:

## Plan
- [ ] Step 1
- [ ] Step 2

## Decisions
| Decision | Reason |
|---|---|

## Risks / Open Questions
- ...

## Next Step
[current next action]
```

Update it after major decisions, completed milestones, scope changes, errors, and before long context transitions.

## 5. Implementation Plan

For medium/large requests, state the plan before editing:

- **Files/modules:** What will be created or changed.
- **Order:** What happens first and why.
- **Risk controls:** How regressions, security, data loss, or UX gaps will be avoided.
- **Test plan:** Automated and manual checks.

For large/high-risk work, wait for explicit confirmation before implementation. For medium work, proceed after stating the plan unless the user asked to approve first.

## 6. Build Discipline

During implementation:

- Prefer the existing project stack and patterns.
- Keep changes scoped to the confirmed goal.
- If a new decision materially changes scope, pause and ask.
- Add comments only where they clarify non-obvious logic.
- Update `.dev-context.md` as milestones complete.

## 7. Self-Test

Before delivery, run relevant checks:

- Build/typecheck/lint/tests when available.
- Manual smoke test for the core user path.
- Edge cases: empty data, invalid input, loading, error, permission/auth, mobile/responsive if UI.
- For generated UI/prototypes, verify the rendered page when practical.

If a check cannot be run, say why and note residual risk.

## 8. Handoff

Final response must include:

- **What changed:** Concise functional summary.
- **Where:** Key files or deliverables.
- **Verification:** Commands/tests run and result.
- **Manual test path:** 3-5 user-facing checks.
- **Known limits:** Anything intentionally out of scope or needing follow-up.

If the user is non-technical or asks for deployment help, include zero-assumption steps:

```text
1. Open Terminal.
2. Run: [command]
3. Wait until you see: [expected output]
4. Open: [URL/file]
5. Test: [specific path]
```

## 9. Post-Delivery Feedback

For substantial projects, ask one concise improvement question:

> Which part of this workflow should be faster or clearer next time?

Use the answer to improve future collaboration.
