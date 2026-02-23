# cc-p4p: The Intelligent Orchestrator for Product Managers

**cc-p4p** applies the [cc10x](https://github.com/romiluz13/cc10x) orchestration pattern to Product Management workflows. Smart routing, persistent memory, evidence-based verification, and bundled PM domain expertise — zero external dependencies.

## How It Works

```
User Request
     │
     ▼
┌─────────────┐     ┌──────────────────────┐
│  cc-p4p     │────▶│  PM Memory           │
│  Router     │     │  .claude/cc-p4p/     │
│             │     │  ├─ activeContext.md  │
│  Detect     │     │  ├─ insights.md      │
│  Intent     │     │  └─ roadmap-state.md │
└──────┬──────┘     └──────────────────────┘
       │
       ├── SPEC ──────────▶ spec-writer agent
       │                    (PRDs, user stories, requirements)
       │
       ├── RESEARCH ──────▶ research-synthesizer agent
       │                    (themes, evidence grading, personas)
       │
       ├── ROADMAP ───────▶ roadmap-planner agent
       │                    (RICE, MoSCoW, Now/Next/Later)
       │
       ├── COMMUNICATE ───▶ comms-drafter agent (READ-ONLY)
       │                    (exec updates, eng updates, customer comms)
       │
       └── METRICS ───────▶ Router handles inline
                            (KPIs, dashboards, north star)
```

## The 5 Workflows

| Workflow | Signal Keywords | Agent | What It Does |
|----------|----------------|-------|--------------|
| **SPEC** | spec, prd, feature, requirement, user story | spec-writer | Brainstorms → drafts PRD → saves to `docs/specs/` |
| **RESEARCH** | research, interview, feedback, survey, competitive | research-synthesizer | Codes themes → grades evidence → saves to `docs/research/` |
| **ROADMAP** | roadmap, priority, plan, timeline, rice, moscow | roadmap-planner | Scores items → maps dependencies → saves to `docs/roadmap/` |
| **COMMUNICATE** | update, status, stakeholder, announcement | comms-drafter | Drafts audience-tailored comms → user approves → router saves |
| **METRICS** | metric, kpi, dashboard, retention, conversion | Router (inline) | Defines metrics, targets, measurement methods |

## Quick Start

### Install

```bash
# Clone the repository
git clone https://github.com/romiluz13/cc-p4p.git

# Add to your Claude Code plugins
# (Follow Claude Code plugin installation instructions)
```

### First Command

Just describe what you need. The router detects intent automatically:

```
"Write a spec for SSO support"          → SPEC workflow
"Synthesize these interview notes"      → RESEARCH workflow
"Prioritize Q2 roadmap using RICE"      → ROADMAP workflow
"Send weekly exec status update"        → COMMUNICATE workflow
"Define metrics for onboarding flow"    → METRICS workflow
```

## Architecture

### 4 Agents

| Agent | Type | Skills Preloaded | Output |
|-------|------|-----------------|--------|
| **spec-writer** | WRITE | pm-memory, pm-brainstorming, pm-spec-writing, pm-verification | PRD in `docs/specs/` |
| **research-synthesizer** | WRITE | pm-memory, pm-research-patterns, pm-verification | Synthesis in `docs/research/` |
| **roadmap-planner** | WRITE | pm-memory, pm-roadmap-frameworks, pm-verification | Roadmap in `docs/roadmap/` |
| **comms-drafter** | READ-ONLY | pm-memory, pm-communication-patterns, pm-verification | Draft text (user approves) |

### 8 Skills

| Skill | Purpose |
|-------|---------|
| **cc-p4p-router** | Intent detection, workflow routing, task orchestration, memory protocol |
| **pm-memory** | Memory load/save, file templates, Read-Edit-Verify pattern |
| **pm-brainstorming** | Product idea exploration, one-question-at-a-time dialogue |
| **pm-verification** | Per-workflow completeness checklists, evidence grounding |
| **pm-spec-writing** | PRD structure, user stories (INVEST), requirements (P0/P1/P2), success metrics |
| **pm-roadmap-frameworks** | RICE, MoSCoW, ICE, Now/Next/Later, OKR alignment, dependency mapping |
| **pm-research-patterns** | Thematic analysis, affinity mapping, triangulation, evidence grading, personas |
| **pm-communication-patterns** | Audience templates (exec/eng/customer), tone mapping, jargon detection, ROAM |

### Memory System

cc-p4p maintains persistent PM context across sessions:

```
.claude/cc-p4p/
├── activeContext.md    # Current focus, decisions, open questions, references
├── insights.md        # User research, competitive intel, customer themes, personas
└── roadmap-state.md   # Now/Next/Later priorities, shipped items, dependencies
```

**Key properties:**
- Survives conversation compaction
- Permission-free operations (Read/Edit tools)
- Stable anchors for reliable updates
- Read-Edit-Verify pattern prevents data loss
- Separate namespace from cc10x (`.claude/cc-p4p/` vs `.claude/cc10x/`)

## Project Structure

```
cc-p4p/
├── .claude-plugin/
│   └── marketplace.json            # Marketplace registration
├── plugins/
│   └── cc-p4p/
│       ├── .claude-plugin/
│       │   └── plugin.json         # Plugin metadata
│       ├── agents/
│       │   ├── spec-writer.md
│       │   ├── research-synthesizer.md
│       │   ├── roadmap-planner.md
│       │   └── comms-drafter.md
│       └── skills/
│           ├── cc-p4p-router/SKILL.md
│           ├── pm-memory/SKILL.md
│           ├── pm-brainstorming/SKILL.md
│           ├── pm-verification/SKILL.md
│           ├── pm-spec-writing/SKILL.md
│           ├── pm-roadmap-frameworks/SKILL.md
│           ├── pm-research-patterns/SKILL.md
│           └── pm-communication-patterns/SKILL.md
├── CLAUDE.md                       # Setup instructions
├── README.md                       # This file
├── LICENSE                         # MIT
└── .gitignore
```

## Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Fully self-contained** | Zero dependencies. All PM domain knowledge bundled in skills. |
| **4 agents, not 5** | METRICS handled inline — consultative, not artifact-producing. |
| **comms-drafter is READ-ONLY** | Communications are sensitive. Agent drafts, user reviews, router persists. |
| **Skills preloaded via frontmatter** | Self-contained agents. No external `Skill()` calls needed. |
| **Separate memory from cc10x** | `.claude/cc-p4p/` vs `.claude/cc10x/`. No conflicts. |
| **Single-agent chains** | v1 simplicity. Each workflow = one agent + memory update. |
| **Simplified Router Contract** | No remediation loops. PM reviews own work. Reports completeness + confidence. |

## Works Alongside cc10x

cc-p4p and cc10x use separate memory namespaces and separate routing. Install both simultaneously:

- **cc10x** handles development tasks (BUILD, DEBUG, REVIEW, PLAN)
- **cc-p4p** handles PM tasks (SPEC, RESEARCH, ROADMAP, COMMUNICATE, METRICS)

## Inspired By

[cc10x](https://github.com/romiluz13/cc10x) — The Intelligent Orchestrator for Claude Code (1 Router, 6 Agents, 12 Skills, 4 Workflows).

cc-p4p adapts the same orchestration pattern (router → agents → memory → verification) for Product Management workflows.

## Version History

- **v1.0.0** — Initial release. 4 agents, 8 skills, 5 workflows, persistent PM memory.

## License

MIT License. See [LICENSE](LICENSE) for details.

## Author

**Rom Iluz** — [GitHub](https://github.com/romiluz13)
