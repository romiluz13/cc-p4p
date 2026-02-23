---
name: pm-research-patterns
description: "Internal skill. Use cc-p4p-router for all PM tasks."
allowed-tools: Read, Write, Edit, Bash, AskUserQuestion, WebFetch
---

# PM Research Patterns

## Overview

Expert knowledge for synthesizing user research, competitive intelligence, and customer feedback into structured insights. Turns raw data into actionable product decisions.

## The Iron Law

```
NO SYNTHESIS WITHOUT EVIDENCE GRADING AND SOURCE TRIANGULATION
```

Every finding must state its evidence strength (Strong/Medium/Weak). Every theme must be checked against multiple sources. Research without grading is storytelling. Findings without triangulation are anecdotes.

## When to Use

- Synthesizing user interview notes
- Analyzing survey results
- Conducting competitive analysis
- Processing customer feedback at scale
- Building evidence-based personas
- Sizing opportunities from research data

## Thematic Analysis Methodology

The core method for synthesizing qualitative research:

1. **Familiarize**: Read through all data. Get a feel for the landscape before coding.
2. **Initial Coding**: Tag each observation, quote, or data point with descriptive codes. Be generous -- easier to merge than split.
3. **Theme Development**: Group related codes into candidate themes. A theme captures something important about the data in relation to the research question.
4. **Theme Review**: Check themes against data. Does each theme have sufficient evidence? Are themes distinct? Do they tell a coherent story?
5. **Theme Refinement**: Define and name each theme clearly. 1-2 sentence description of what each captures.
6. **Report**: Write up themes as findings with supporting evidence.

## Affinity Mapping

A collaborative method for grouping observations:

1. **Capture**: Write each distinct observation as a separate note
2. **Cluster**: Group related notes by similarity. Don't pre-define categories -- let them emerge.
3. **Label**: Give each cluster a descriptive name
4. **Organize**: Arrange clusters into higher-level groups if patterns emerge
5. **Identify themes**: Clusters and relationships reveal key themes

**Tips:**
- One observation per note
- Move notes between clusters freely
- Large clusters probably contain multiple themes -- split them
- Outliers are interesting -- don't force-fit

## Triangulation

Strengthen findings by combining sources:

| Type | Definition | Example |
|------|-----------|---------|
| **Methodological** | Same question, different methods | Interviews + survey + analytics |
| **Source** | Same method, different participants | Multiple user segments |
| **Temporal** | Same observation, different times | Q1 vs Q3 comparison |

Findings supported by multiple sources and methods are much stronger than single-source.
When sources disagree: that is a signal, not an error. May reveal segments or contexts.

## Evidence Strength Grading

| Grade | Definition | Criteria |
|-------|-----------|----------|
| **Strong** | High confidence | 3+ independent sources, multiple methods, behavioral data |
| **Medium** | Moderate confidence | 1-2 sources, single method, or stated preferences |
| **Weak** | Low confidence | Assumption, single anecdote, or extrapolation |

**Rule:** Every finding must state its evidence strength. Weak evidence must be flagged explicitly.

## Interview Note Processing

### Extracting Insights
For each interview, identify:

**Observations**: What did the participant describe doing, experiencing, feeling?
- Distinguish behaviors (what they do) from attitudes (what they think/feel)
- Note context: when, where, with whom, how often
- Flag workarounds -- these are unmet needs in disguise

**Direct Quotes**: Verbatim statements that illustrate a point
- Good quotes are specific and vivid, not generic
- Attribute to participant type, not name: "Enterprise admin, 200-person team"
- A quote is evidence, not a finding

**Behaviors vs Stated Preferences**: What people DO differs from what they SAY
- Behavioral observations are stronger evidence
- Note contradictions between stated and revealed preferences

**Signals of Intensity**: How much does this matter?
- Emotional language, frequency, workaround effort, impact of failure

### Cross-Interview Analysis
- Patterns: which observations appear across participants?
- Frequency: how many mentioned each theme?
- Segments: do different user types show different patterns?
- Contradictions: where do participants disagree?
- Surprises: what challenged assumptions?

## Competitive Analysis

### Identifying Competitors
| Level | Definition |
|-------|-----------|
| **Direct** | Same problem, same approach, same users |
| **Indirect** | Same problem, different approach |
| **Adjacent** | Could expand into your space |
| **Substitute** | Entirely different solution to same need |

### Feature Comparison Matrix
```
| Capability | Us | Competitor A | Competitor B |
|-----------|-----|-------------|-------------|
| [Feature] | Strong | Adequate | Absent |
```

Rating scale:
- **Strong**: Market-leading, deep, well-executed
- **Adequate**: Functional, gets job done, not differentiated
- **Weak**: Exists but limited, significant gaps
- **Absent**: Not available

### Win/Loss Patterns
Track reasons for wins and losses:
- Feature gaps, integration advantages, pricing structure
- Incumbent advantage, sales execution, brand/trust
- Segment by deal type, size, industry

## Opportunity Sizing

For each finding, estimate:
- **Addressable users**: How many could benefit?
- **Frequency**: How often encountered? (daily/weekly/monthly)
- **Severity**: Impact when it occurs? (blocker/friction/annoyance)
- **Willingness to pay**: Would it drive upgrades/retention?

**Scoring**: Impact = Users x Frequency x Severity

Present with transparency:
- Show assumptions and confidence levels
- Use ranges, not false precision
- Compare opportunities against each other (relative ranking)

## Persona Development

Build evidence-based personas from research data:

1. Identify behavioral clusters across participants
2. Define distinguishing variables (company size, skill level, use case)
3. Create profiles (3-5 personas max):

```
[Persona Name] -- [One-line description]

Who: Role, company, experience
Goals: Primary jobs to be done
Pain points: Top 3 frustrations
Behaviors: Usage patterns, tools, frequency
Values: What matters most in a solution
Quote: Representative verbatim quote
```

**Avoid:** Demographic-only personas, too many personas (>5), fictional data, never updating.

## Survey Design Principles

### Question Types and When to Use
| Type | Best For | Watch Out For |
|------|----------|---------------|
| Multiple choice | Frequency, demographics, simple preferences | Forcing choices that don't reflect reality |
| Likert scale | Attitudes, satisfaction, agreement | Acquiescence bias (people tend to agree) |
| Open-ended | Exploring unknowns, getting language | Hard to analyze at scale |
| Ranking | Relative priorities | Cognitive load above 5-7 items |
| Matrix | Multiple items on same scale | Straight-lining (same answer for all) |

### Writing Good Questions
- One concept per question -- never double-barreled
- Avoid leading language ("Don't you agree that...")
- Offer "Not applicable" or "I don't know" options
- Randomize answer order where possible
- Test with 3-5 people before sending

### Sample Size Guidelines
| Confidence Level | Margin of Error | Sample Needed |
|-----------------|----------------|---------------|
| 95% | +/- 5% | ~385 |
| 95% | +/- 10% | ~97 |
| 90% | +/- 5% | ~271 |

For qualitative themes: 12-15 interviews typically reach saturation for a well-defined user segment.

## Jobs To Be Done (JTBD) Framework

### Core Structure
**When [situation], I want to [motivation], so I can [expected outcome].**

### Uncovering JTBD
Interview questions that reveal jobs:
- "Walk me through the last time you [did this task]."
- "What were you trying to accomplish?"
- "What did you try before this? Why did you switch?"
- "What would make you stop using this?"

### Job Map
Break a main job into process steps:

1. **Define**: How does the customer define what they need?
2. **Locate**: How do they find inputs?
3. **Prepare**: How do they set up?
4. **Confirm**: How do they verify readiness?
5. **Execute**: How do they do the core task?
6. **Monitor**: How do they track progress?
7. **Modify**: How do they adjust?
8. **Conclude**: How do they finish?

Each step is an opportunity for innovation.

## Research Synthesis Template

Save to: `docs/research/YYYY-MM-DD-<topic>-synthesis.md`

```markdown
# Research Synthesis: [Topic]

## Methodology
- Sources: [list with type]
- Methods: [interviews/survey/analytics/competitive]
- Sample: [size and composition]
- Period: [when conducted]

## Key Themes

### Theme 1: [Name]
**Evidence Strength:** Strong/Medium/Weak
**Sources:** [which sources]
**Finding:** [description]
**Key Quotes:** [1-2 representative]
**Implication:** [what this means for product]

## Opportunities
| Opportunity | Users | Frequency | Severity | Evidence | Score |
|------------|-------|-----------|----------|----------|-------|

## Personas
[If applicable]

## Recommendations
1. [Recommendation] -- [Evidence basis]

## Open Questions
- [Remaining unknowns]
```

## Red Flags — STOP

- Presenting findings without evidence strength grades → **STOP. Grade every finding Strong/Medium/Weak.**
- Single source supporting a "key theme" → **STOP. One anecdote is not a theme. Need 3+ for Strong.**
- Skipping triangulation → **STOP. Combine methods and sources before claiming confidence.**
- Synthesizing without methodology stated → **STOP. Document how you collected and analyzed.**
- Cherry-picking quotes that confirm hypothesis → **STOP. Present all themes including contradictory.**
- Research report with no recommendations → **STOP. Research without action is waste.**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "We only have one data source" | Then grade it Medium/Weak and say so. Don't present assumptions as findings. |
| "The quotes speak for themselves" | Quotes are evidence, not findings. Themes require interpretation and grading. |
| "We don't have time to triangulate" | Untriangulated findings lead to wrong decisions. Triangulation saves time long-term. |
| "Everyone agrees, so it must be true" | Unanimous agreement may mean you asked leading questions. Check methodology. |
| "The data is clear" | If clear, grading takes 30 seconds. If ambiguous, grading prevents overconfidence. |
| "We'll validate later" | Later means after you've built the wrong thing. Validate strength now. |
| "This user is very representative" | One user is N=1. Representative requires multiple participants showing same pattern. |
| "Outliers aren't important" | Outliers may represent edge cases, future segments, or broken assumptions. Document them. |

## Anti-Patterns to Avoid

| Anti-Pattern | Problem | Instead |
|-------------|---------|---------|
| Cherry-picking quotes | Confirmation bias | Present all themes, including contradictory |
| N=1 findings | Single anecdote masquerading as insight | Require 3+ sources for "strong" evidence |
| Asking "would you use X?" | Stated preference is unreliable | Ask about past behavior and current workarounds |
| Ignoring outliers | Missing edge cases and segments | Document outliers explicitly, investigate |
| Research without action | Waste of effort | Every synthesis must end with recommendations |
| Skipping triangulation | Fragile findings | Combine methods and sources |
