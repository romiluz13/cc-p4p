---
name: cc-p4p-router
description: |
  THE ONLY ENTRY POINT FOR CC-P4P. This skill MUST be activated for ANY product management task - never skip.

  Use this skill when: writing specs, synthesizing research, planning roadmaps, drafting stakeholder updates, defining metrics, or ANY PM request.

  Triggers: spec, prd, feature, requirement, user story, acceptance criteria, research, interview, feedback, survey, competitive, persona, insight, roadmap, priority, plan, timeline, rice, moscow, okr, quarter, update, status, stakeholder, announcement, launch, report, metric, kpi, dashboard, retention, conversion, north star, product, pm, brainstorm.

  CRITICAL: Execute workflow immediately. Never just describe capabilities.
---

# cc-p4p Router

**EXECUTION ENGINE.** When loaded: Detect intent -> Load memory -> Execute workflow -> Update memory.

**NEVER** list capabilities. **ALWAYS** execute.

## Decision Tree (FOLLOW IN ORDER)

| Priority | Signal | Keywords | Workflow |
|----------|--------|----------|----------|
| 1 | SPEC | spec, prd, feature, requirement, user story, acceptance criteria, "write a spec", "define requirements" | **SPEC** |
| 2 | RESEARCH | research, interview, feedback, survey, competitive, persona, insight, "synthesize", "analyze interviews" | **RESEARCH** |
| 3 | ROADMAP | roadmap, priority, plan, timeline, rice, moscow, okr, quarter, "prioritize", "what should we build next" | **ROADMAP** |
| 4 | COMMUNICATE | update, status, stakeholder, announcement, launch, report, "send update", "draft email" | **COMMUNICATE** |
| 5 | METRICS | metric, kpi, dashboard, retention, conversion, north star, "define metrics", "track success" | **METRICS** |
| 6 | DEFAULT | Everything else | **SPEC** |

**Conflict Resolution:** SPEC signals win over ROADMAP. "Plan the feature" = SPEC (not ROADMAP). "Plan the quarter" = ROADMAP.

**Disambiguation:** If intent is genuinely unclear, use AskUserQuestion:
"What would you like to do?"
- A. Write a feature spec/PRD
- B. Synthesize research findings
- C. Plan/prioritize a roadmap
- D. Draft a stakeholder communication

## Agent Chains

| Workflow | Agent | Type |
|----------|-------|------|
| SPEC | spec-writer | WRITE |
| RESEARCH | research-synthesizer | WRITE |
| ROADMAP | roadmap-planner | WRITE |
| COMMUNICATE | comms-drafter | READ-ONLY |
| METRICS | Router inline (no agent) | INLINE |

Each workflow = single agent + memory update. No parallel chains (v1 simplicity).

## Memory (PERMISSION-FREE)

**LOAD FIRST (Before routing):**

**Step 1 - Create directory (MUST complete before Step 2):**
```
Bash(command="mkdir -p .claude/cc-p4p")
```

**Step 2 - Load memory files (AFTER Step 1 completes):**
```
Read(file_path=".claude/cc-p4p/activeContext.md")
Read(file_path=".claude/cc-p4p/insights.md")
Read(file_path=".claude/cc-p4p/roadmap-state.md")
```

**IMPORTANT:** Do NOT run Step 1 and Step 2 in parallel. Wait for mkdir to complete before reading files.

If any memory file is missing:
- Create it with `Write(...)` using the templates from `cc-p4p:pm-memory` (include the contract comment + required headings).
- Then `Read(...)` it before continuing.

**TEMPLATE VALIDATION GATE (Auto-Heal):**

After loading memory files, ensure ALL required sections exist.

### activeContext.md - Required Sections
`## Current Focus`, `## Recent Work`, `## Decisions`, `## Open Questions`, `## References`, `## Last Updated`

### insights.md - Required Sections
`## User Research Insights`, `## Competitive Intelligence`, `## Customer Feedback Themes`, `## Personas`, `## Last Updated`

### roadmap-state.md - Required Sections
`## Current Priorities`, `## Shipped`, `## Dependencies`, `## Capacity Notes`, `## Last Updated`

**Auto-heal pattern (apply to EACH file, EACH missing section):**

activeContext.md example:
```
Edit(file_path=".claude/cc-p4p/activeContext.md",
     old_string="## Last Updated",
     new_string="## Open Questions\n- [None yet]\n\n## Last Updated")
Read(file_path=".claude/cc-p4p/activeContext.md")
```

insights.md example:
```
Edit(file_path=".claude/cc-p4p/insights.md",
     old_string="## Last Updated",
     new_string="## Personas\n- [None identified yet]\n\n## Last Updated")
Read(file_path=".claude/cc-p4p/insights.md")
```

roadmap-state.md example:
```
Edit(file_path=".claude/cc-p4p/roadmap-state.md",
     old_string="## Last Updated",
     new_string="## Capacity Notes\n- [Not yet assessed]\n\n## Last Updated")
Read(file_path=".claude/cc-p4p/roadmap-state.md")
```

**VERIFY:** After ALL auto-heals, Read each file once more and confirm every required section exists.

**UPDATE (Final):**
- Do a workflow-final memory update after the agent completes.
- Use Edit tool on memory files (permission-free), then Read-back verify.

Memory update rules:
1. Use `Edit(...)` (not `Write`) to update existing `.claude/cc-p4p/*.md`.
2. Immediately `Read(...)` the edited file and confirm the expected text exists.
3. If the update did not apply, STOP and retry with a correct, exact `old_string` anchor.

## Check Active Workflow Tasks

**After loading memory, check for active tasks:**
```
TaskList()  # Check for pending/in-progress workflow tasks
```

**If active CC-P4P workflow task exists (subject starts with `CC-P4P `):**
- Resume from task state (use `TaskGet({ taskId })`)
- Skip workflow selection - continue execution from where it stopped
- Check `blockedBy` to determine which agent to run next

**If no active tasks:**
- Proceed with workflow selection below

---

## Task-Based Orchestration

**At workflow start, create task hierarchy using TaskCreate/TaskUpdate:**

### SPEC Workflow Tasks
```
TaskCreate({
  subject: "CC-P4P SPEC: {feature_summary}",
  description: "User request: {request}\n\nWorkflow: SPEC\nAgent: spec-writer",
  activeForm: "Writing spec for {feature}"
})
# Returns workflow_task_id

TaskCreate({
  subject: "CC-P4P spec-writer: Write spec for {feature}",
  description: "Write feature spec/PRD per user request",
  activeForm: "Writing feature spec"
})
# Returns agent_task_id

TaskCreate({
  subject: "CC-P4P Memory Update: Persist spec learnings",
  description: "REQUIRED: Collect Memory Notes from spec-writer and persist to memory files.\n\n**Instructions:**\n1. Find '### Memory Notes' section from agent output\n2. Update .claude/cc-p4p/activeContext.md with spec reference\n3. Use Read-Edit-Read pattern for each file.",
  activeForm: "Persisting spec learnings"
})
# Returns memory_task_id
TaskUpdate({ taskId: memory_task_id, addBlockedBy: [agent_task_id] })
```

### RESEARCH Workflow Tasks
```
TaskCreate({
  subject: "CC-P4P RESEARCH: {topic_summary}",
  description: "User request: {request}\n\nWorkflow: RESEARCH\nAgent: research-synthesizer",
  activeForm: "Synthesizing research on {topic}"
})

TaskCreate({
  subject: "CC-P4P research-synthesizer: Synthesize {topic}",
  description: "Synthesize research findings per user request",
  activeForm: "Synthesizing research"
})
# Returns agent_task_id

TaskCreate({
  subject: "CC-P4P Memory Update: Persist research insights",
  description: "REQUIRED: Persist insights to .claude/cc-p4p/insights.md.\n\nUse Read-Edit-Read pattern.",
  activeForm: "Persisting research insights"
})
# Returns memory_task_id
TaskUpdate({ taskId: memory_task_id, addBlockedBy: [agent_task_id] })
```

### ROADMAP Workflow Tasks
```
TaskCreate({
  subject: "CC-P4P ROADMAP: {scope_summary}",
  description: "User request: {request}\n\nWorkflow: ROADMAP\nAgent: roadmap-planner",
  activeForm: "Planning roadmap for {scope}"
})

TaskCreate({
  subject: "CC-P4P roadmap-planner: Plan {scope}",
  description: "Plan/prioritize roadmap per user request",
  activeForm: "Planning roadmap"
})
# Returns agent_task_id

TaskCreate({
  subject: "CC-P4P Memory Update: Persist roadmap state",
  description: "REQUIRED: Persist to .claude/cc-p4p/roadmap-state.md.\n\nUse Read-Edit-Read pattern.",
  activeForm: "Persisting roadmap state"
})
# Returns memory_task_id
TaskUpdate({ taskId: memory_task_id, addBlockedBy: [agent_task_id] })
```

### COMMUNICATE Workflow Tasks
```
TaskCreate({
  subject: "CC-P4P COMMUNICATE: {comm_summary}",
  description: "User request: {request}\n\nWorkflow: COMMUNICATE\nAgent: comms-drafter (READ-ONLY)",
  activeForm: "Drafting communication for {audience}"
})

TaskCreate({
  subject: "CC-P4P comms-drafter: Draft {comm_type}",
  description: "Draft communication. Agent is READ-ONLY -- outputs draft text.",
  activeForm: "Drafting communication"
})
# Returns agent_task_id

TaskCreate({
  subject: "CC-P4P Memory Update: Log communication",
  description: "REQUIRED: Log communication in activeContext.md ## Recent Work.\n\nNOTE: comms-drafter is READ-ONLY. Router persists if user approves draft.",
  activeForm: "Logging communication"
})
# Returns memory_task_id
TaskUpdate({ taskId: memory_task_id, addBlockedBy: [agent_task_id] })
```

### METRICS Workflow (Inline - No Agent)
```
TaskCreate({
  subject: "CC-P4P METRICS: {metric_summary}",
  description: "User request: {request}\n\nWorkflow: METRICS (inline)\nRouter handles directly using pm-roadmap-frameworks + pm-verification knowledge.",
  activeForm: "Defining metrics for {area}"
})
# Router handles this directly -- no agent spawned
```

## Workflow Execution

### SPEC
1. Load memory -> Check for existing specs in References
2. **Clarify scope** -> AskUserQuestion if vague
3. Create task hierarchy
4. Invoke agent:
   ```
   Task(subagent_type="cc-p4p:spec-writer", prompt="
   ## Task Context
   - **Task ID:** {taskId}

   ## User Request
   {request}

   ## Memory Summary
   {brief summary from activeContext.md}

   ## Existing Context
   {relevant insights from insights.md}

   ## SKILL_HINTS (conditional skills if triggered)
   {detected skills from CLAUDE.md Complementary Skills table, otherwise 'None'}

   ---
   IMPORTANT:
   - **NEVER call `EnterPlanMode`.** This is an execution agent.
   - Update `.claude/cc-p4p/{activeContext,insights,roadmap-state}.md` at the end per `cc-p4p:pm-memory`.
   - Include Router Contract in output.

   Execute the task and include 'Task {TASK_ID}: COMPLETED' in your output when done.
   ")
   ```
5. Validate Router Contract
6. Update memory (task-enforced)

### RESEARCH
1. Load memory -> Check insights.md for related themes
2. **Clarify scope** -> AskUserQuestion: Users? Market? Competitive? All?
3. Create task hierarchy
4. Invoke research-synthesizer agent (same pattern as SPEC)
5. Validate Router Contract
6. Update memory (persist to insights.md)

### ROADMAP
1. Load memory -> Load roadmap-state.md (current priorities)
2. **Clarify format** -> AskUserQuestion: Now/Next/Later? RICE scoring? Quarterly?
3. Create task hierarchy
4. Invoke roadmap-planner agent
5. Validate Router Contract
6. Update memory (persist to roadmap-state.md)

### COMMUNICATE
1. Load memory -> Get full context from all 3 files
2. **Clarify audience + cadence** -> AskUserQuestion: Executive? Engineering? Customer? Weekly/monthly?
3. Create task hierarchy
4. Invoke comms-drafter agent (READ-ONLY)
5. Present draft to user
6. **If user approves:** Router persists to file and updates memory
7. **If user requests changes:** Re-invoke with feedback

### METRICS (Inline)
1. Load memory
2. Identify metric area from request
3. Apply PM knowledge directly:
   - North Star metric definition
   - Leading vs lagging indicators
   - Measurement methods
   - Dashboard recommendations
4. Output metric definitions
5. Update memory with metric decisions

## Router Contract Validation

After agent completes, check for Router Contract:

```
Look for "### Router Contract (MACHINE-READABLE)" section in agent output.
If found -> Parse and validate.
If NOT found -> Non-compliant. Ask user to review output manually.
```

**Parse and Validate Contract:**
```
CONTRACT FIELDS:
- STATUS: Agent's self-reported status
- CONFIDENCE: 0-100 score
- BLOCKING: true/false
- MEMORY_NOTES: Structured notes for persistence

VALIDATION:
1. If contract.BLOCKING == true:
   -> Present issues to user via AskUserQuestion
   -> Options: Fix / Skip / Abort
2. Collect contract.MEMORY_NOTES for workflow-final persistence
3. If none of above triggered -> Workflow complete
```

## Agent Invocation Template

**Pass task ID, context, and conditional skills to each agent:**
```
Task(subagent_type="cc-p4p:{agent_name}", prompt="
## Task Context
- **Task ID:** {taskId}

## User Request
{request}

## Memory Summary
{brief summary from activeContext.md}

## PM Context
{relevant context from insights.md and roadmap-state.md}

## SKILL_HINTS (conditional skills if triggered)
{detected skills from CLAUDE.md Complementary Skills table, otherwise 'None'}
**If skills listed:** Call `Skill(skill="{skill-name}")` after memory load. If unavailable, note in Memory Notes and continue.

---
IMPORTANT:
- **NEVER call `EnterPlanMode`.** This is an execution agent.
- If your tools include `Edit`, update `.claude/cc-p4p/*.md` at the end.
- If your tools do NOT include `Edit`, include a `### Memory Notes` section.
- Include Router Contract in your output.

Execute the task and include 'Task {TASK_ID}: COMPLETED' in your output when done.
")
```

## Workflow-Final Memory Persistence (Task-Enforced)

When the Memory Update task becomes available:
1. Review agent output for `### Memory Notes` section
2. Follow the task description to persist learnings
3. Use Read-Edit-Read pattern for each memory file
4. Mark task completed

**Why task-enforced:**
- Tasks survive context compaction
- Visible in TaskList() -- can't be forgotten
- Workflow isn't complete until Memory Update task is done

## Gates (Must Pass)

1. **MEMORY_LOADED** - Before routing
2. **TASKS_CHECKED** - Check TaskList() for active workflow
3. **INTENT_CLARIFIED** - User intent is unambiguous
4. **TASKS_CREATED** - Workflow task hierarchy created
5. **ALL_TASKS_COMPLETED** - All workflow tasks completed
6. **MEMORY_UPDATED** - Before marking done
