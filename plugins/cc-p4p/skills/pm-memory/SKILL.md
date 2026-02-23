---
name: pm-memory
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Write, Edit, Bash
---

# PM Memory (MANDATORY)

## The Iron Law

```
EVERY WORKFLOW MUST:
1. LOAD memory at START (and before key decisions)
2. UPDATE memory at END (and after learnings/decisions)
```

**Brevity Rule:** Memory is an index, not a document. Be brief -- one line per item.

## What "Memory" Actually Is

cc-p4p memory is a **small, stable, permission-free Markdown database** used for:
- **Continuity:** survive compaction/session resets
- **Consistency:** avoid contradicting prior decisions
- **Compounding:** promote insights into reusable knowledge
- **Resumability:** recover where a workflow stopped

### Memory Surfaces (Types)

1. **Working Memory**: `.claude/cc-p4p/activeContext.md`
   - "What matters right now": focus, recent work, decisions, open questions
   - Links to durable artifacts (specs/research/roadmaps)
2. **Insights Memory**: `.claude/cc-p4p/insights.md`
   - User research insights, competitive intelligence, customer feedback themes, personas
3. **Roadmap Memory**: `.claude/cc-p4p/roadmap-state.md`
   - Now/Next/Later priorities, shipped items, dependencies, capacity
4. **Artifact Memory (Durable)**: `docs/specs/*`, `docs/research/*`, `docs/roadmap/*`
   - The details. Memory files are the index.
5. **Tasks (Execution State)**: Claude Code Tasks
   - Great for orchestration, survives across sessions.

### Promotion Ladder

Information "graduates" to more durable layers:
- **One-off observation** -> `activeContext.md` (Recent Work / Decisions)
- **Research finding** -> `insights.md` (User Research / Competitive / Themes)
- **Priority decision** -> `roadmap-state.md` (Current Priorities)
- **Needs detail** -> `docs/specs/*` or `docs/research/*` + link from activeContext

## Permission-Free Operations (CRITICAL)

**ALL memory operations are PERMISSION-FREE using the correct tools.**

| Operation | Tool | Permission |
|-----------|------|------------|
| Create memory directory | `Bash(command="mkdir -p .claude/cc-p4p")` | FREE |
| **Read memory files** | `Read(file_path=".claude/cc-p4p/activeContext.md")` | **FREE** |
| **Create NEW memory file** | `Write(file_path="...", content="...")` | **FREE** (file doesn't exist) |
| **Update EXISTING memory** | `Edit(file_path="...", old_string="...", new_string="...")` | **FREE** |
| Save spec/research files | `Write(file_path="docs/specs/...", content="...")` | FREE |

### CRITICAL: Write vs Edit

| Tool | Use For | Asks Permission? |
|------|---------|------------------|
| **Write** | Creating NEW files | NO (if file doesn't exist) |
| **Write** | Overwriting existing files | **YES** |
| **Edit** | Updating existing files | **NO - always permission-free** |

**RULE: Use Write for NEW files, Edit for UPDATES.**

### CRITICAL: Use Read Tool, NOT Bash(cat)

**NEVER use Bash compound commands** -- they ASK PERMISSION.
**ALWAYS use Read tool** for reading files -- it's PERMISSION-FREE.

## Memory Structure

```
.claude/
  cc-p4p/
    activeContext.md   # Current focus + decisions + open questions (MOST IMPORTANT)
    insights.md        # Research insights, competitive intel, customer themes
    roadmap-state.md   # Now/Next/Later priorities, shipped items, dependencies
```

## Who Reads/Writes Memory (Ownership)

### Read
- **Router (always):** loads all 3 files before workflow selection.
- **WRITE agents** (spec-writer, research-synthesizer, roadmap-planner): load memory at task start.
- **READ-ONLY agents** (comms-drafter): receive memory summary in prompt, do NOT load this skill.

### Write
- **WRITE agents:** update memory directly at task end using `Edit(...)` + `Read(...)` verify.
- **READ-ONLY agents:** output `### Memory Notes` section. Router persists via task-enforced Memory Update.

## Pre-Compaction Memory Safety

**Update memory IMMEDIATELY when you notice:**
- Extended brainstorming (5+ rounds)
- Long spec discussions
- Multi-topic research synthesis
- 30+ tool calls in session

**Checkpoint Pattern:**
```
Edit(file_path=".claude/cc-p4p/activeContext.md",
     old_string="## Current Focus",
     new_string="## Current Focus\n\n[Updated focus + key decisions]")
Read(file_path=".claude/cc-p4p/activeContext.md")  # Verify
```

## Memory File Templates

### activeContext.md (Read/Write EVERY session)

```markdown
# PM Active Context
<!-- CC-P4P: Do not rename headings. Used as Edit anchors. -->

## Current Focus
[Active work -- what PM task is in progress]

## Recent Work
- [Date] [What was done] - [artifact reference]

## Decisions
- [Decision]: [Choice] - [Why]

## Open Questions
- [Question] - [Who should answer] - [Blocking/Non-blocking]

## References
- Spec: `docs/specs/...` (or N/A)
- Research: `docs/research/...` (or N/A)
- Roadmap: `docs/roadmap/...` (or N/A)

## Last Updated
[timestamp]
```

### insights.md (Accumulates research findings)

```markdown
# PM Insights
<!-- CC-P4P: Do not rename headings. Used as Edit anchors. -->

## User Research Insights
- [Insight]: [Evidence] - [Source: interview/survey/analytics]

## Competitive Intelligence
- [Competitor]: [Finding] - [Implication for us]

## Customer Feedback Themes
- [Theme]: [Frequency] - [Severity] - [Example quote]

## Personas
- [Persona name]: [Brief description] - [Key need]

## Last Updated
[timestamp]
```

### roadmap-state.md (Tracks priorities)

```markdown
# PM Roadmap State
<!-- CC-P4P: Do not rename headings. Used as Edit anchors. -->

## Current Priorities

### Now (In Progress)
- [Item]: [Owner] - [Status]

### Next (Planned)
- [Item]: [Priority score] - [Dependencies]

### Later (Future)
- [Item]: [Strategic rationale]

## Shipped
- [Date] [Item] - [Impact/metrics]

## Dependencies
- [Dependency]: [Owner] - [Need-by date] - [Status]

## Capacity Notes
- [Team/resource considerations]

## Last Updated
[timestamp]
```

## Stable Anchors (ONLY use these)

| Anchor | File | Stability |
|--------|------|-----------|
| `## Recent Work` | activeContext | GUARANTEED |
| `## Decisions` | activeContext | GUARANTEED |
| `## Open Questions` | activeContext | GUARANTEED |
| `## References` | activeContext | GUARANTEED |
| `## Last Updated` | all files | GUARANTEED (fallback) |
| `## User Research Insights` | insights | GUARANTEED |
| `## Competitive Intelligence` | insights | GUARANTEED |
| `## Customer Feedback Themes` | insights | GUARANTEED |
| `## Current Priorities` | roadmap-state | GUARANTEED |
| `## Shipped` | roadmap-state | GUARANTEED |
| `## Dependencies` | roadmap-state | GUARANTEED |

**NEVER use as anchors:**
- Table headers (`| Col | Col |`)
- List item text (`- specific text`)
- Optional sections that may not exist

## Read-Edit-Verify (MANDATORY)

Every memory edit MUST follow this exact sequence:

### Step 1: READ
```
Read(file_path=".claude/cc-p4p/activeContext.md")
```

### Step 2: VERIFY ANCHOR
```
# Check if intended anchor exists in the content you just read
# If anchor not found -> use "## Last Updated" as fallback
```

### Step 3: EDIT
```
Edit(file_path=".claude/cc-p4p/activeContext.md",
     old_string="## Recent Work",
     new_string="## Recent Work\n- [New entry]\n")
```

### Step 4: VERIFY
```
Read(file_path=".claude/cc-p4p/activeContext.md")
# Confirm your change appears. If not -> STOP and retry.
```

## Memory File Contract (Never Break)

Hard rules:
- Do not rename the top-level headers (`# PM Active Context`, `# PM Insights`, `# PM Roadmap State`).
- Do not rename section headers (e.g., `## Current Focus`, `## Last Updated`).
- Only add content *inside* existing sections (append lists/rows).
- After every `Edit(...)`, **Read back** the file and confirm the intended change exists.

If an Edit does not apply cleanly:
- STOP (do not guess).
- Re-read the file and re-apply using a correct, exact `old_string` anchor.

## Mandatory Operations

### At Workflow START (REQUIRED)

```
# Step 1: Create directory
Bash(command="mkdir -p .claude/cc-p4p")

# Step 2: Load ALL 3 memory files
Read(file_path=".claude/cc-p4p/activeContext.md")
Read(file_path=".claude/cc-p4p/insights.md")
Read(file_path=".claude/cc-p4p/roadmap-state.md")
```

**If file doesn't exist:** Read tool returns an error -- that's fine, means starting fresh.

### At Workflow END (REQUIRED)

```
# Read existing content
Read(file_path=".claude/cc-p4p/activeContext.md")

# Add entry to Recent Work
Edit(file_path=".claude/cc-p4p/activeContext.md",
     old_string="## Recent Work",
     new_string="## Recent Work\n- [YYYY-MM-DD] [What was done] - [artifact path]\n")

# VERIFY
Read(file_path=".claude/cc-p4p/activeContext.md")
```

## Integration with Agents

**ALL agents MUST:**

1. **START**: Load memory files before any work
2. **DURING**: Note decisions and insights
3. **END**: Update memory files with new context

If an agent cannot safely update memory (e.g., no `Edit` tool -- comms-drafter):
- Include notes in `### Memory Notes` section
- Router persists those notes via task-enforced Memory Update

**Failure to update memory = incomplete work.**

## Red Flags -- STOP IMMEDIATELY

If you catch yourself:
- Starting work WITHOUT loading memory
- Making decisions WITHOUT checking Decisions section
- Completing work WITHOUT updating memory
- Saying "I'll remember" instead of writing to memory

**STOP. Load/update memory FIRST.**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "I know what we decided" | Check the Decisions section. |
| "Small task, no need" | Small tasks have context too. Always update. |
| "I'll remember" | You won't. Conversation compacts. Write it down. |
| "Memory is optional" | Memory is MANDATORY. No exceptions. |
