# cc-p4p: The Intelligent Orchestrator for Product Managers

## Auto-Activation

IMPORTANT: ALWAYS invoke cc-p4p-router on ANY product management task. First action, no exceptions.

**Skip cc-p4p ONLY when:**
- User EXPLICITLY says "don't use cc-p4p", "without cc-p4p", or "skip cc-p4p"
- No interpretation. No guessing. Only these exact opt-out phrases.

[CC-P4P]|entry: cc-p4p:cc-p4p-router

## What This Does

cc-p4p automatically routes PM requests to the right workflow:

| Signal | Keywords | Workflow |
|--------|----------|----------|
| SPEC | spec, prd, feature, requirement, user story | → spec-writer agent |
| RESEARCH | research, interview, feedback, survey, competitive | → research-synthesizer agent |
| ROADMAP | roadmap, priority, plan, timeline, rice, moscow | → roadmap-planner agent |
| COMMUNICATE | update, status, stakeholder, announcement, launch | → comms-drafter agent |
| METRICS | metric, kpi, dashboard, retention, conversion | → Router handles inline |

## Memory System

cc-p4p maintains persistent PM context across sessions in `.claude/cc-p4p/`:
- `activeContext.md` — Current focus, decisions, open questions
- `insights.md` — User research, competitive intel, customer themes
- `roadmap-state.md` — Now/Next/Later priorities, shipped items, dependencies

Memory survives conversation compaction. Every workflow loads and updates it.

## Works Alongside cc10x

cc-p4p uses `.claude/cc-p4p/` for memory (separate from cc10x's `.claude/cc10x/`).
Both can be installed simultaneously without conflict.

## Skills Index

[Skills Index]
|cc-p4p:{cc-p4p-router/SKILL.md,pm-memory/SKILL.md,pm-brainstorming/SKILL.md,pm-verification/SKILL.md,pm-spec-writing/SKILL.md,pm-roadmap-frameworks/SKILL.md,pm-research-patterns/SKILL.md,pm-communication-patterns/SKILL.md}
