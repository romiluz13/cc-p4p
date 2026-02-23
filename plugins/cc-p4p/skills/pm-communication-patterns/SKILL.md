---
name: pm-communication-patterns
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Grep, Glob, AskUserQuestion
---

# PM Communication Patterns

## Overview

Expert knowledge for stakeholder communications -- status updates, risk communication, decision documentation, and audience-adapted messaging. Every communication should be tailored to its audience.

## Audience Templates

### Executive / Leadership
**Executives want:** Strategic context, progress against goals, risks needing help, decisions needing input.

```
Status: [Green / Yellow / Red]

TL;DR: [One sentence -- the most important thing to know]

Progress:
- [Outcome achieved, tied to goal/OKR]
- [Milestone reached, with impact]
- [Key metric movement]

Risks:
- [Risk]: [Mitigation plan]. [Ask if needed].

Decisions needed:
- [Decision]: [Options with recommendation]. Need by [date].

Next milestones:
- [Milestone] -- [Date]
```

**Tips:**
- Lead with conclusion, not journey. "We shipped X and it moved Y metric."
- Keep under 200 words
- Status color = YOUR genuine assessment. Yellow = good risk management.
- Only include risks you want help with
- Asks must be specific: "Decision on X by Friday" not "support needed"

### Engineering Team
**Engineers want:** Clear priorities, technical context, blockers resolved, decisions affecting their work.

```
Shipped:
- [Feature/fix] -- [Link]. [Impact if notable].

In progress:
- [Item] -- [Owner]. [Expected completion]. [Blockers].

Decisions:
- [Made]: [Rationale]. [Link to ADR if exists].
- [Needed]: [Context]. [Options]. [Recommendation].

Priority changes:
- [What changed and why]

Coming up:
- [Next items] -- [Why these are next]
```

**Tips:**
- Link to tickets, PRs, documents -- engineers click through
- When priorities change, explain why
- Be explicit about blockers and what you're doing to unblock
- Don't waste time with irrelevant info

### Cross-Functional Partners
**Partners want:** What's coming that affects them, what they need to prepare, how to give input.

```
What's coming:
- [Feature/launch] -- [Date]. [What this means for your team].

What we need from you:
- [Specific ask] -- [Context]. By [date].

Decisions made:
- [Decision] -- [How it affects your team].

Open for input:
- [Topic] -- [How to provide feedback].
```

### Customer / External
**Customers want:** What's new, what's coming, how it benefits them, how to get started.

```
What's new:
- [Feature] -- [Benefit in customer terms]. [How to use it].

Coming soon:
- [Feature] -- [Expected timing]. [Why it matters to you].

Known issues:
- [Issue] -- [Status]. [Workaround if available].

Feedback:
- [How to share feedback]
```

**Tips:**
- No internal jargon. No ticket numbers. No technical details.
- Frame as what customer can now DO, not what you built
- Be honest about timelines -- "later this quarter" beats a missed date
- Only mention issues if customer-impacting with resolution plan

## Tone Mapping Matrix

| Audience | Tone | Format | Length |
|----------|------|--------|--------|
| Executive | Concise, strategic, decisive | Bullet points, status colors | Under 200 words |
| Engineering | Direct, technical, specific | Structured lists with links | Flexible |
| Cross-functional | Collaborative, clear, action-oriented | Action items + context | Under 300 words |
| Customer | Friendly, benefit-focused, jargon-free | Short paragraphs | Under 250 words |

## Status Framework (Green / Yellow / Red)

| Status | Definition | When to Use |
|--------|-----------|-------------|
| **Green** | On track. No significant risks. Meeting commitments. | Things genuinely going well |
| **Yellow** | At risk. Progress slower or risk materialized. May miss without intervention. | FIRST sign of risk (early!) |
| **Red** | Off track. Major blocker. Will miss without significant help. | Need escalation |

**Rules:**
- Move to Yellow at FIRST sign of risk, not when sure things are bad
- Move to Red when you've exhausted own options
- Move back to Green only when risk genuinely resolved
- Document what changed: "Moved to Yellow because [reason]"

## Jargon Detection

Internal terms that should NOT appear in customer/external communications:

| Internal Term | Customer-Friendly Alternative |
|--------------|------------------------------|
| Sprint/iteration | "upcoming release" or "next update" |
| Backlog | "planned improvements" |
| Technical debt | [don't mention -- irrelevant to customer] |
| Regression | "issue we're fixing" |
| Deploy/ship | "release" or "update" |
| Standup/retro | [don't mention] |
| OKR/KPI | "our goals" or "what we're measuring" |
| P0/P1/P2 | "high priority" or "important" |
| Blocker | "delay" or "issue" |

**Rule:** Before sending customer comms, scan for internal terms and replace.

## ROAM Risk Framework

| Status | Definition | Action |
|--------|-----------|--------|
| **Resolved** | No longer a concern | Document how resolved |
| **Owned** | Someone actively managing it | State owner + mitigation plan |
| **Accepted** | Known, proceeding without mitigation | Document rationale |
| **Mitigated** | Actions reduced risk to acceptable level | Document what was done |

## Risk Communication

1. **State clearly:** "There is a risk that [thing] happens because [reason]"
2. **Quantify impact:** "If this happens, the consequence is [impact]"
3. **State likelihood:** "[likely/possible/unlikely] because [evidence]"
4. **Present mitigation:** "We are managing this by [actions]"
5. **Make the ask:** "We need [specific help] to reduce this risk"

## Decision Documentation (ADR Format)

### Architecture Decision Record -- Adapted for PM
```
# ADR-[number]: [Decision Title]

## Status
[Proposed / Accepted / Deprecated / Superseded by ADR-X]

## Context
[What is the situation? What forces are at play?]

## Decision
[What did we decide?]

## Options Considered
| Option | Pros | Cons |
|--------|------|------|
| A | ... | ... |
| B | ... | ... |

## Rationale
[Why this option? What tipped the balance?]

## Consequences
- [Expected positive outcomes]
- [Expected negative outcomes or tradeoffs]
- [What we'll monitor]
```

**When to write an ADR:** Any decision that is hard to reverse, affects multiple teams, or will be questioned later.

## Channel Recommendations

| Situation | Channel | Why |
|-----------|---------|-----|
| Urgent blocker | Slack DM / call | Immediate attention needed |
| Weekly status | Email or shared doc | Async, reference-able |
| Decision needed | Meeting with follow-up doc | Real-time discussion + record |
| Launch announcement | Email + Slack broadcast | Reach + visibility |
| Risk escalation | Meeting then email summary | Discussion + paper trail |

## Review Checklist

Before sending ANY communication:
- [ ] Audience identified and appropriate
- [ ] Tone matches audience expectations
- [ ] No jargon leaks (especially in customer comms)
- [ ] Actionable -- clear next steps or asks
- [ ] Length appropriate for audience
- [ ] Status/color justified by evidence (if applicable)
- [ ] Links included where relevant
- [ ] Reviewed for accuracy against latest data
