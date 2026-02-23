# Build Patterns
<!-- CC-P4P BUILD: Do not rename headings. Used as Edit anchors. -->

## Naming Conventions
- Skills: `pm-{domain}/SKILL.md` (prefix with pm-)
- Agents: `{role}.md` (descriptive name, no prefix)
- Memory files: `activeContext.md`, `insights.md`, `roadmap-state.md`

## Frontmatter Format
- Agents: name, description, model, color, context, tools, skills
- Skills: name, description, allowed-tools

## Adaptation Rules
- cc10x pattern → cc-p4p: Replace dev workflows with PM workflows
- Router: BUILD/DEBUG/REVIEW/PLAN → SPEC/RESEARCH/ROADMAP/COMMUNICATE/METRICS
- Memory: activeContext/patterns/progress → activeContext/insights/roadmap-state
- Agents: component-builder/code-reviewer → spec-writer/research-synthesizer
- Verification: test evidence → PM completeness checklists

## Common Gotchas
- Router must handle METRICS inline (no agent)
- comms-drafter has no Edit/Write tools (READ-ONLY)
- Skills preloaded via frontmatter — no external Skill() calls from agents
- Memory anchors must be stable (## headings never renamed)
