---
name: pm-roadmap-frameworks
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Write, Edit, Bash, AskUserQuestion
---

# PM Roadmap Frameworks

## Overview

Expert knowledge for product roadmap planning, prioritization, and communication. Provides frameworks for building roadmaps that are strategic, realistic, and actionable.

## Roadmap Formats

### Now / Next / Later
The simplest and often most effective format:

- **Now** (current sprint/month): Committed work. High confidence. Team is actively building.
- **Next** (1-3 months): Planned work. Good confidence in what, less in exactly when.
- **Later** (3-6+ months): Directional. Strategic bets, flexible scope and timing.

**When to use:** Most teams, most of the time. Avoids false precision on dates. Good for external/leadership communication.

### Quarterly Themes
Organize around 2-3 themes per quarter:

- Each theme = strategic investment area (e.g., "Enterprise readiness", "Activation improvements")
- Under each theme, list specific initiatives
- Themes map to company/team OKRs
- Makes it easy to explain WHY you're building what you're building

**When to use:** Showing strategic alignment. Planning meetings. Executive communication.

### OKR-Aligned Roadmap
Map items directly to Objectives and Key Results:

- Start with team's OKRs
- Under each Key Result, list initiatives that move that metric
- Include expected impact per initiative
- Creates clear accountability

**When to use:** OKR-driven organizations. Ensuring every initiative has measurable "why".

### Timeline / Gantt View
Calendar-based with start dates, end dates, durations:

- Shows parallelism and sequencing
- Good for identifying resource conflicts and dependencies
- NOT good for external communication (creates false precision)

**When to use:** Execution planning with engineering. Scheduling conflicts. Never for external comms.

## Prioritization Frameworks

### RICE Score
**RICE = (Reach x Impact x Confidence) / Effort**

| Dimension | Definition | Scale |
|-----------|-----------|-------|
| **Reach** | Users affected in time period | Concrete number (e.g., 500/quarter) |
| **Impact** | Needle movement per user | 3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal |
| **Confidence** | Estimate reliability | 100%=data-backed, 80%=some evidence, 50%=gut feel |
| **Effort** | Person-months of work | Include eng, design, all functions |

**When to use:** Quantitative, defensible prioritization. Large backlogs. Less good for strategic bets where impact is hard to estimate.

### MoSCoW
| Category | Definition | Rule |
|----------|-----------|------|
| **Must** | Non-negotiable. Roadmap fails without these. | Would we not ship without this? |
| **Should** | Important but not critical for launch. | High-priority fast follows. |
| **Could** | Desirable if capacity allows. | Won't delay if cut. |
| **Won't** | Explicitly out of scope this period. | Important for clarity. |

**When to use:** Scoping a release/quarter. Forcing prioritization conversations with stakeholders.

### ICE Score
**ICE = Impact x Confidence x Ease** (each scored 1-10)

| Dimension | Definition |
|-----------|-----------|
| **Impact** | How much will this move the target metric? |
| **Confidence** | How sure are we about the impact? |
| **Ease** | How easy to implement? (inverse of effort -- higher=easier) |

**When to use:** Quick prioritization. Early-stage products. Not enough data for RICE.

### Value vs Effort Matrix
Plot on 2x2:

| | Low Effort | High Effort |
|---|-----------|------------|
| **High Value** | Quick Wins -- Do first | Big Bets -- Plan carefully |
| **Low Value** | Fill-ins -- Spare capacity | Money Pits -- Don't do |

**When to use:** Visual prioritization in team sessions. Building shared understanding.

## Dependency Mapping

### Identifying Dependencies
| Type | Example |
|------|---------|
| Technical | Feature B requires infrastructure from Feature A |
| Team | Needs work from another team (design, platform, data) |
| External | Waiting on vendor, partner, or third-party |
| Knowledge | Need research results before starting |
| Sequential | Must ship A before starting B |

### Managing Dependencies
- List all dependencies explicitly in roadmap
- Assign owner to each
- Set "need by" date
- Build buffer -- dependencies are highest-risk items
- Flag cross-team dependencies early
- Have contingency plan for slips

### Reducing Dependencies
- Build simpler version that avoids the dependency
- Parallelize using interface contracts or mocks
- Sequence differently to move dependency earlier
- Absorb work into your team to remove coordination

## Capacity Planning

### Estimating Capacity
- Start with team size x time period
- Subtract overhead: meetings, on-call, interviews, PTO
- Rule of thumb: 60-70% time on planned feature work
- Factor ramp time for new members

### Healthy Allocation
| Category | % | Description |
|----------|---|-------------|
| Planned features | 70% | Roadmap items advancing strategic goals |
| Technical health | 20% | Tech debt, reliability, performance |
| Unplanned | 10% | Buffer for urgent issues, quick wins |

Adjust based on context:
- New product: more features, less tech debt
- Mature product: more tech debt investment
- Post-incident: more reliability
- Rapid growth: more scalability

### Capacity vs Ambition
- If roadmap exceeds capacity: cut scope, don't pretend people can do more
- When adding: ask "What comes off?"
- Commit to fewer things and deliver reliably

## Communicating Changes

### When Roadmap Changes
- New strategic priority from leadership
- Customer feedback changes priorities
- Technical discovery changes estimates
- Dependency slip from another team
- Resource change (team grows/shrinks)

### How to Communicate
1. Acknowledge the change directly
2. Explain the reason (new information)
3. Show the tradeoff (what was deprioritized)
4. Show the new plan
5. Acknowledge impact on affected stakeholders

### Avoiding Whiplash
- Don't change for every new input -- have threshold
- Batch updates at natural cadences unless truly urgent
- Distinguish "strategic reprioritization" from "normal execution refinement"
- Track change frequency -- frequent changes may signal unclear strategy
