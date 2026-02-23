---
name: pm-verification
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Grep, Glob
---

# PM Verification

## Overview

Claiming PM work is complete without verification is dishonesty, not efficiency.

**Core principle:** Evidence of completeness before claims, always.

## The Iron Law

```
NO COMPLETION CLAIMS WITHOUT EVIDENCE OF COMPLETENESS
```

If you haven't checked the deliverable against criteria, you cannot claim it's done.

## The Gate Function

```
BEFORE claiming any status or expressing satisfaction:

1. IDENTIFY: What criteria prove this claim?
2. CHECK: Verify each criterion against the deliverable
3. SCORE: sections_present / sections_required
4. VERIFY: Does the score justify the claim?
   - If NO: State actual status with gaps
   - If YES: State claim WITH evidence
5. ONLY THEN: Make the claim

Skip any step = incomplete work
```

## Per-Workflow Checklists

### SPEC Verification
| Check | Criteria | Required? |
|-------|----------|-----------|
| Problem statement | Present, 2-3 sentences, evidence-grounded | YES |
| Goals | 3-5 measurable outcomes listed | YES |
| Non-goals | 3-5 explicit exclusions with rationale | YES |
| User stories | Standard format with specific user types | YES |
| P0 requirements | Must-haves clearly identified | YES |
| Success metrics | Leading + lagging with targets | YES |
| Open questions | Tagged with owner (eng/design/legal/data) | YES |
| Acceptance criteria | Given/When/Then or checklist format | RECOMMENDED |
| Timeline | Hard deadlines and phasing noted | OPTIONAL |

**Completeness score:** Count YES criteria present / total YES criteria required.
**Pass threshold:** 6/7 (all YES criteria) = SPEC_COMPLETE. Missing any = NEEDS_CLARIFICATION.

### RESEARCH Verification
| Check | Criteria | Required? |
|-------|----------|-----------|
| Sources cited | Each finding has named sources | YES |
| Evidence graded | Strong (3+) / Medium (1-2) / Weak (assumption) for each theme | YES |
| Themes triangulated | Multiple data points per theme | YES |
| Opportunities sized | Users affected x frequency x severity | YES |
| Methodology stated | How data was collected and analyzed | YES |
| Contradictions noted | Where sources disagree, documented | RECOMMENDED |
| Personas identified | If data supports, behavioral clusters described | OPTIONAL |

**Pass threshold:** 5/5 = SYNTHESIS_COMPLETE. Missing any = NEEDS_MORE_DATA.

### ROADMAP Verification
| Check | Criteria | Required? |
|-------|----------|-----------|
| Items scored | Each item scored with chosen framework | YES |
| Dependencies mapped | Owner + need-by date for each dependency | YES |
| Capacity considered | Items fit within team capacity constraints | YES |
| Strategy-aligned | Each item serves a stated goal/OKR | YES |
| Now/Next/Later clear | Clear differentiation between time horizons | YES |
| Shipped acknowledged | Recent completions documented | RECOMMENDED |

**Pass threshold:** 5/5 = ROADMAP_UPDATED. Missing any = NEEDS_CLARIFICATION.

### COMMUNICATE Verification
| Check | Criteria | Required? |
|-------|----------|-----------|
| Audience matched | Tone, detail level, format match audience | YES |
| No jargon leaks | Internal terms not in customer comms | YES |
| Actionable | Clear next steps or asks | YES |
| Status justified | Green/Yellow/Red backed by evidence | YES (if status update) |
| Length appropriate | Under limits (exec: 200 words, eng: flexible) | YES |

**Pass threshold:** 4/4 (or 5/5 for status updates) = DRAFT_READY.

## Evidence Grounding

For every claim in a PM deliverable, ask: **"What data supports this?"**

### Strong Evidence
- User research data (interviews, surveys, analytics)
- Competitive analysis with feature comparison
- Metrics with statistical significance
- Multiple independent sources agreeing

### Medium Evidence
- Expert opinion from domain SMEs
- Single data source (one survey, one analysis)
- Customer feedback from small sample
- Industry benchmarks

### Weak Evidence (Flag These)
- Assumptions without data
- "Common sense" claims
- Extrapolation from unrelated contexts
- Single anecdote

**Rule:** Every finding should state its evidence strength. Weak evidence must be flagged explicitly.

## Red Flags — STOP

If you find yourself using:
- "Seems fine" — What specifically is fine? Check the list.
- "Probably" — Based on what evidence?
- "Should work" — For whom? Verified how?
- "Users will love it" — What data supports this?
- "This is obvious" — Obvious to whom? Document it anyway.

**STOP. Check against the appropriate workflow checklist above.**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "It's good enough" | Check the completeness score. Is it really? |
| "We can refine later" | Ship complete, refine content. Don't ship incomplete structure. |
| "The PM will know" | Document explicitly. Context gets lost. |
| "Minor gaps don't matter" | Minor gaps become major confusion in implementation. |
| "I'm confident" | Confidence does not equal completeness. Check the list. |

## Completeness Scoring

```
COMPLETENESS = sections_present / sections_required

SPEC:      [X/7]  — Problem, Goals, Non-Goals, Stories, P0 Reqs, Metrics, Questions
RESEARCH:  [X/5]  — Sources, Grading, Triangulation, Sizing, Methodology
ROADMAP:   [X/5]  — Scored, Dependencies, Capacity, Strategy, Horizons
COMMS:     [X/4+] — Audience, Jargon, Actionable, Length (+Status if applicable)
```

## Self-Critique Gate (BEFORE Router Contract)

**MANDATORY: Check these BEFORE writing Router Contract:**

### Deliverable Quality
- [ ] Meets all required criteria for this workflow type?
- [ ] Evidence strength stated for key claims?
- [ ] No placeholder text or TODOs remaining?
- [ ] Saved to correct output location?

### Self-Critique Verdict
**PROCEED:** [YES/NO]
**CONFIDENCE:** [High/Medium/Low]
**COMPLETENESS:** [X/Y]

- If NO — Fix gaps before writing Router Contract
- If YES — Proceed to Router Contract

## Output Format

```markdown
## Verification Summary

### Workflow
[SPEC | RESEARCH | ROADMAP | COMMUNICATE]

### Criteria Checked
| Check | Status | Evidence |
|-------|--------|----------|
| [Criterion] | PASS/FAIL | [What was verified] |

### Completeness
[X/Y] criteria met

### Gaps (if any)
- [Missing element] — [Severity: Blocking/Non-blocking]

### Verdict
COMPLETE — All required criteria verified
```
