---
name: pm-spec-writing
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Write, Edit, Bash, AskUserQuestion
---

# PM Spec Writing

## Overview

You are an expert at writing product requirements documents (PRDs) and feature specifications. This skill provides the structure, formats, and best practices for producing complete, actionable specs.

## The Iron Law

```
NO SPEC WITHOUT A CLEAR PROBLEM STATEMENT AND MEASURABLE SUCCESS CRITERIA
```

Every PRD must start with a concrete user problem grounded in evidence. Every PRD must end with metrics that prove whether it worked. Specs without these are opinions, not requirements.

## When to Use

- Writing a new feature spec or PRD
- Defining requirements for an existing feature enhancement
- Structuring user stories with acceptance criteria
- Documenting P0/P1/P2 requirements with tradeoffs

## PRD Template

A well-structured PRD follows this structure:

### 1. Problem Statement
- Describe the user problem in 2-3 sentences
- Who experiences this problem and how often
- What is the cost of not solving it (user pain, business impact, competitive risk)
- Ground this in evidence: user research, support data, metrics, or customer feedback

### 2. Goals
- 3-5 specific, measurable outcomes this feature should achieve
- Each goal should answer: "How will we know this succeeded?"
- Distinguish between user goals (what users get) and business goals (what the company gets)
- Goals should be outcomes, not outputs ("reduce time to first value by 50%" not "build onboarding wizard")

### 3. Non-Goals
- 3-5 things this feature explicitly will NOT do
- Adjacent capabilities that are out of scope for this version
- For each non-goal, briefly explain why it is out of scope
- Non-goals prevent scope creep and set stakeholder expectations

### 4. User Stories
Format: "As a [specific user type], I want [capability] so that [benefit]"

Guidelines:
- User type should be specific ("enterprise admin" not just "user")
- Capability describes what they accomplish, not how
- Benefit explains the "why" — what value this delivers
- Include edge cases: error states, empty states, boundary conditions
- Include different user types if feature serves multiple personas
- Order by priority — most important stories first

Good user stories are INVEST:
- **I**ndependent: Can be developed alone
- **N**egotiable: Details can be discussed
- **V**aluable: Delivers value to the user
- **E**stimable: Team can estimate effort
- **S**mall: Completable in one sprint
- **T**estable: Clear way to verify

### 5. Requirements

**P0 — Must Have**: Feature cannot ship without these. Non-negotiable.
Ask: "If we cut this, does the feature still solve the core problem?" If no, it is P0.

**P1 — Nice to Have**: Significantly improves experience but core works without them.
These often become fast follow-ups after launch.

**P2 — Future Considerations**: Out of scope for v1 but design should support them later.
These prevent accidental architectural decisions that make them hard.

For each requirement:
- Clear, unambiguous description of expected behavior
- Acceptance criteria (Given/When/Then or checklist)
- Technical considerations or constraints
- Dependencies on other teams or systems

**Categorization tips:**
- Be ruthless about P0s. Tighter must-have list = faster ship and learn.
- If everything is P0, nothing is P0.
- P1s should be things you're confident you'll build soon, not a wish list.
- P2s are architectural insurance.

### 6. Success Metrics

**Leading Indicators** (change in days-weeks):
- Adoption rate: % of eligible users who try the feature
- Activation rate: % who complete the core action
- Task completion rate: % who accomplish their goal
- Time to complete: how long the workflow takes
- Error rate: how often users hit dead ends

**Lagging Indicators** (change in weeks-months):
- Retention impact: does feature improve retention?
- Revenue impact: does it drive upgrades or expansion?
- NPS/CSAT change: does it improve satisfaction?
- Support ticket reduction: does it reduce load?

**Setting targets:**
- Specific: "50% adoption within 30 days" not "high adoption"
- Based on comparable features, benchmarks, or hypotheses
- Set "success" threshold and "stretch" target
- Define measurement method: what tool, what query, what time window
- Specify when you'll evaluate: 1 week, 1 month, 1 quarter

### 7. Open Questions
- Questions needing answers before or during implementation
- Tag each with who should answer (engineering, design, legal, data)
- Distinguish blocking (must answer before starting) vs non-blocking

### 8. Timeline Considerations (Optional)
- Hard deadlines (contractual, events, compliance)
- Dependencies on other teams
- Suggested phasing if too large for one release

## Acceptance Criteria Format

**Given/When/Then:**
- Given [precondition or context]
- When [action the user takes]
- Then [expected outcome]

**Checklist format:**
- [ ] [Specific testable behavior]
- [ ] [Error case handled]
- [ ] [Edge case covered]

**Tips:**
- Cover happy path, error cases, and edge cases
- Be specific about expected behavior, not implementation
- Include negative test cases (what should NOT happen)
- Each criterion should be independently testable
- Avoid ambiguous words: "fast", "user-friendly" — define concretely

## Scope Management

### Recognizing Scope Creep
- Requirements keep getting added after spec approved
- "Small" additions accumulate into larger project
- Building features no user asked for ("while we're at it...")
- Launch date keeps moving without re-scoping

### Preventing Scope Creep
- Write explicit non-goals in every spec
- Any scope addition requires a scope removal or timeline extension
- Separate v1 from v2 clearly
- Review spec against original problem statement
- Time-box investigations: "If we can't figure out X in 2 days, cut it"
- Create a "parking lot" for good ideas not in scope

## Anti-Patterns

| Anti-Pattern | Problem | Fix |
|-------------|---------|-----|
| Vague goals | "Make it better" — unmeasurable | Specific metric + target |
| Missing non-goals | Scope creeps unchecked | List 3-5 explicit exclusions |
| Solution-prescriptive stories | "Add a dropdown" — prescribes UI | Describe need, not widget |
| Unmeasurable metrics | "Users are happy" — untestable | Define measurement method |
| Everything is P0 | No prioritization happened | Force-rank, ask "would we not ship?" |
| No open questions | False certainty | List unknowns honestly |

## Red Flags — STOP

- Writing requirements before problem is defined → **STOP. Write problem statement first.**
- All requirements marked P0 → **STOP. Force-rank. If everything is P0, nothing is.**
- No success metrics or metrics are unmeasurable → **STOP. Define how you'll know it succeeded.**
- User stories use generic "user" not specific persona → **STOP. Identify who this is for.**
- Non-goals section empty or missing → **STOP. Scope creep is guaranteed without boundaries.**
- Spec has no open questions → **STOP. False certainty. List unknowns honestly.**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "The problem is obvious, skip it" | If obvious, writing 2 sentences costs nothing. If wrong, saves weeks. |
| "We don't need non-goals" | Scope will creep. Non-goals are your defense. |
| "We'll figure out metrics later" | Without metrics, you can't know if you succeeded. Define now. |
| "Everything is P0 for launch" | If everything is P0, you haven't prioritized. Cut harder. |
| "User stories slow us down" | Stories ensure you build for real users, not assumptions. |
| "Acceptance criteria are engineering's job" | PM defines WHAT, eng defines HOW. Criteria are WHAT. |
| "The timeline is flexible" | Hard deadlines exist even if unspoken. Surface them now. |
| "Open questions will resolve themselves" | Unresolved questions become launch blockers. Tag owners now. |

## Spec File Location

Save specs to: `docs/specs/YYYY-MM-DD-<feature>-spec.md`

## Spec File Template

```markdown
# [Feature Name] — Product Requirements Document

## Status
Draft | In Review | Approved | Shipped

## Problem Statement
[2-3 sentences, evidence-grounded]

## Goals
1. [Measurable outcome 1]
2. [Measurable outcome 2]
3. [Measurable outcome 3]

## Non-Goals
1. [Exclusion 1] — [why out of scope]
2. [Exclusion 2] — [why out of scope]
3. [Exclusion 3] — [why out of scope]

## User Stories
- As a [user type], I want [capability] so that [benefit]
- As a [user type], I want [capability] so that [benefit]

## Requirements

### P0 — Must Have
- [Requirement]: [Description]
  - Acceptance: [Given/When/Then]

### P1 — Nice to Have
- [Requirement]: [Description]

### P2 — Future Considerations
- [Requirement]: [Why we're noting it now]

## Success Metrics
| Metric | Type | Target | Measurement | Evaluate At |
|--------|------|--------|-------------|-------------|
| [Metric] | Leading | [target] | [how measured] | [when] |

## Open Questions
- [ ] [Question] — [Owner: eng/design/legal] — [Blocking/Non-blocking]

## Timeline
- [Hard deadlines, dependencies, phasing]
```
