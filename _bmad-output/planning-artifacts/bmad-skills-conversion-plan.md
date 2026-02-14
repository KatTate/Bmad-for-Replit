# BMAD Workflows to Replit Agent Skills — Conversion Plan

## Executive Summary

This plan outlines how to convert the BMAD Method's workflows, agents, and tasks into **Replit Agent Skills** — the open standard format that lives in `/.agents/skills/` and is automatically loaded by Replit Agent. The goal is to make BMAD workflows natively discoverable and enforceable by the agent without relying on `replit.md` routing hacks, giving us persistent, structured, and portable workflow enforcement that survives chat resets.

---

## 1. Understanding the Two Systems

### How BMAD Works Today (in Replit)

- A large routing table is injected into `replit.md` that maps natural language triggers to agent/workflow files
- The agent must pattern-match every user message against this routing table
- Workflows use a "step-file architecture" — each workflow has a `workflow.md` that loads sequential step files from a `steps/` directory
- Agent personas are defined in markdown/XML files that dictate persona, menu, and behavior
- A YAML-based workflow engine (`workflow.xml`) handles some Phase 4 workflows
- All output goes to `_bmad-output/planning-artifacts/` and `_bmad-output/implementation-artifacts/`
- Configuration lives in `_bmad/bmm/config.yaml`

### How Replit Agent Skills Work

- Skills live in `/.agents/skills/<skill-name>/SKILL.md`
- Each skill has YAML frontmatter (`name`, `description`) + markdown body with instructions
- The `description` field is loaded at startup for ALL skills (~100 tokens) — this is how the agent decides when to activate a skill
- When activated, the full `SKILL.md` body is loaded (recommended < 500 lines / ~5000 tokens)
- Optional subdirectories: `scripts/`, `references/`, `assets/` for supporting files
- Skills support progressive disclosure — heavy content goes in `references/` and is loaded on demand
- Skills persist across chat sessions and can be version-controlled

### Key Differences & Challenges

| Aspect | BMAD Today | Agent Skills Target |
|--------|-----------|-------------------|
| Discovery | `replit.md` routing table (fragile) | Automatic from `description` field (native) |
| Activation | Pattern matching + file loading | Agent natively activates matching skills |
| Step execution | Sequential step-file loading | Instructions in SKILL.md + references/ |
| Persona enforcement | XML agent definitions | Persona instructions in SKILL.md body |
| State tracking | Frontmatter in output files | Same approach works within skill instructions |
| Configuration | `_bmad/bmm/config.yaml` | Can reference via relative paths or a shared config skill |
| Token budget | Entire workflow.md + steps loaded sequentially | SKILL.md < 500 lines; overflow in references/ |

---

## 2. Conversion Architecture

### 2.1 Skill Organization Strategy

```
.agents/skills/
├── bmad-core/                    # Core orchestrator & help system
│   ├── SKILL.md                  # Master routing, "what's next?", orientation
│   └── references/
│       ├── workflow-catalog.md   # Complete workflow reference
│       └── agent-roster.md      # All agent personas summary
│
├── bmad-brainstorm/              # Phase 1: Brainstorming
│   ├── SKILL.md
│   ├── references/
│   │   └── techniques.md
│   └── assets/
│       └── template.md
│
├── bmad-create-brief/            # Phase 1: Product Brief
│   ├── SKILL.md
│   └── references/
│       ├── step-vision.md
│       ├── step-users.md
│       ├── step-metrics.md
│       ├── step-scope.md
│       └── template.md
│
├── bmad-research/                # Phase 1: All three research types
│   ├── SKILL.md
│   └── references/
│       ├── market-research.md
│       ├── domain-research.md
│       ├── technical-research.md
│       └── template.md
│
├── bmad-create-prd/              # Phase 2: PRD Creation
│   ├── SKILL.md
│   └── references/
│       ├── step-discovery.md
│       ├── step-success.md
│       ├── step-journeys.md
│       ├── step-domain.md
│       ├── step-innovation.md
│       ├── step-scoping.md
│       ├── step-functional.md
│       ├── step-nonfunctional.md
│       ├── step-polish.md
│       └── prd-purpose.md
│
├── bmad-validate-prd/            # Phase 2: PRD Validation
│   ├── SKILL.md
│   └── references/
│       └── validation-steps.md
│
├── bmad-edit-prd/                # Phase 2: PRD Editing
│   ├── SKILL.md
│   └── references/
│       └── edit-steps.md
│
├── bmad-create-ux/               # Phase 2: UX Design
│   ├── SKILL.md
│   └── references/
│       └── ux-steps.md
│
├── bmad-create-architecture/     # Phase 3: Architecture
│   ├── SKILL.md
│   └── references/
│       ├── step-context.md
│       └── architecture-data.md
│
├── bmad-create-epics/            # Phase 3: Epics & Stories
│   ├── SKILL.md
│   └── references/
│       └── epic-steps.md
│
├── bmad-check-readiness/         # Phase 3: Implementation Readiness
│   ├── SKILL.md
│   └── references/
│       └── readiness-steps.md
│
├── bmad-sprint-planning/         # Phase 4: Sprint Planning
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       └── checklist.md
│
├── bmad-create-story/            # Phase 4: Story Creation
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       ├── checklist.md
│       └── template.md
│
├── bmad-dev-story/               # Phase 4: Story Development
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       └── checklist.md
│
├── bmad-code-review/             # Phase 4: Code Review
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       └── checklist.md
│
├── bmad-quick-spec/              # Anytime: Quick Spec
│   ├── SKILL.md
│   └── references/
│       └── spec-steps.md
│
├── bmad-quick-dev/               # Anytime: Quick Dev
│   ├── SKILL.md
│   └── references/
│       └── dev-steps.md
│
├── bmad-party-mode/              # Anytime: Multi-Agent Discussion
│   ├── SKILL.md
│   └── references/
│       └── orchestration.md
│
├── bmad-correct-course/          # Anytime: Course Correction
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       └── checklist.md
│
├── bmad-project-context/         # Anytime: Generate Project Context
│   ├── SKILL.md
│   └── references/
│       └── scan-steps.md
│
├── bmad-document-project/        # Anytime: Document Project
│   ├── SKILL.md
│   └── references/
│       └── doc-instructions.md
│
├── bmad-adversarial-review/      # Anytime: Adversarial Review
│   └── SKILL.md
│
├── bmad-tech-writer/             # Tech Writer tools (WD, MG, VD, EC, US)
│   ├── SKILL.md
│   └── references/
│       └── documentation-standards.md
│
├── bmad-qa-automation/           # QA: Test Automation
│   ├── SKILL.md
│   └── references/
│       ├── instructions.md
│       └── checklist.md
│
├── bmad-retrospective/           # Phase 4: Retrospective
│   ├── SKILL.md
│   └── references/
│       └── instructions.md
│
└── bmad-assess-project/          # Phase 0: Brownfield Assessment
    ├── SKILL.md
    └── references/
        └── assessment-steps.md
```

### 2.2 Naming Convention

All BMAD skills use the `bmad-` prefix to:
- Group them visually in the skills directory
- Avoid naming conflicts with non-BMAD skills
- Make it clear they belong to the BMAD Method framework

### 2.3 The `bmad-core` Skill — The Orchestrator

This is the most important skill. It replaces the routing table in `replit.md` and acts as the master coordinator:

```markdown
---
name: bmad-core
description: >
  BMAD Method orchestrator — AI-driven agile development framework.
  Activates when user says "start BMad", "what's next?", "help",
  "BMad master", or any BMAD 2-letter workflow code (CB, CP, CA, CE, etc.).
  Routes to specialized BMAD workflow skills for structured project
  development from brainstorming through implementation.
---

# BMAD Core Orchestrator

You are the BMAD Method orchestrator. When activated, determine
what the user needs and guide them to the right workflow skill.

## Trigger Routing

When the user's message matches these patterns, tell them which
workflow to activate (the agent will auto-discover the matching skill):

| User Says | Workflow Skill | Phase |
|-----------|---------------|-------|
| "brainstorm", "BP" | bmad-brainstorm | 1-Analysis |
| "create brief", "CB" | bmad-create-brief | 1-Analysis |
| "create PRD", "CP" | bmad-create-prd | 2-Planning |
| ... (full table) | ... | ... |

## "What's Next?" Logic

See [references/workflow-catalog.md](references/workflow-catalog.md)
for the complete phase-sequenced guide.

(... abbreviated for plan purposes ...)
```

---

## 3. Conversion Strategy by Priority

### Tier 1 — Most Frequently Used (Convert First)

These are the workflows users reach for most often, and where drift causes the most pain:

| # | Skill Name | BMAD Source | Why Priority |
|---|-----------|-------------|-------------|
| 1 | `bmad-core` | `replit-routing.md` + `help.md` + `bmad-master.md` | Foundation — everything routes through here |
| 2 | `bmad-quick-spec` | `bmad-quick-flow/quick-spec/` | Most used "simple path" entry point |
| 3 | `bmad-quick-dev` | `bmad-quick-flow/quick-dev/` | Paired with quick-spec, high daily usage |
| 4 | `bmad-create-brief` | `1-analysis/create-product-brief/` | Primary "full path" entry point |
| 5 | `bmad-create-prd` | `2-plan-workflows/create-prd/` | Core planning workflow, complex + drift-prone |
| 6 | `bmad-create-architecture` | `3-solutioning/create-architecture/` | Critical solutioning workflow |
| 7 | `bmad-create-epics` | `3-solutioning/create-epics-and-stories/` | Bridge between planning and implementation |
| 8 | `bmad-dev-story` | `4-implementation/dev-story/` | Daily development loop |
| 9 | `bmad-code-review` | `4-implementation/code-review/` | Quality gate in story cycle |
| 10 | `bmad-party-mode` | `core/workflows/party-mode/` | Unique multi-agent feature, tricky to keep on track |

### Tier 2 — Supporting Workflows (Convert Second)

| # | Skill Name | BMAD Source |
|---|-----------|-------------|
| 11 | `bmad-create-story` | `4-implementation/create-story/` |
| 12 | `bmad-sprint-planning` | `4-implementation/sprint-planning/` |
| 13 | `bmad-check-readiness` | `3-solutioning/check-implementation-readiness/` |
| 14 | `bmad-brainstorm` | `core/workflows/brainstorming/` |
| 15 | `bmad-validate-prd` | `2-plan-workflows/create-prd/workflow-validate-prd.md` |
| 16 | `bmad-research` | `1-analysis/research/` (all 3 types) |
| 17 | `bmad-correct-course` | `4-implementation/correct-course/` |

### Tier 3 — Utility & Specialty (Convert Last)

| # | Skill Name | BMAD Source |
|---|-----------|-------------|
| 18 | `bmad-edit-prd` | `2-plan-workflows/create-prd/workflow-edit-prd.md` |
| 19 | `bmad-create-ux` | `2-plan-workflows/create-ux-design/` |
| 20 | `bmad-tech-writer` | `bmm/agents/tech-writer/` |
| 21 | `bmad-qa-automation` | `bmm/workflows/qa/automate/` |
| 22 | `bmad-retrospective` | `4-implementation/retrospective/` |
| 23 | `bmad-adversarial-review` | `core/tasks/review-adversarial-general.xml` |
| 24 | `bmad-assess-project` | `0-assess/assess-brownfield/` |
| 25 | `bmad-project-context` | `generate-project-context/` |
| 26 | `bmad-document-project` | `document-project/` |

---

## 4. Conversion Methodology — How to Transform Each Workflow

### 4.1 SKILL.md Structure Template

Every BMAD skill follows this structure:

```markdown
---
name: bmad-{workflow-name}
description: >
  {What it does}. Use when user says "{trigger phrases}",
  "{2-letter code}", or requests {natural language description}.
  Part of BMAD Method Phase {N}: {Phase Name}.
---

# {Workflow Title}

## Role
{Persona definition — extracted from agent .md file}

## Prerequisites
{What artifacts/documents must exist before starting}

## Workflow Steps

### Step 1: {Name}
{Condensed instructions from step-01-*.md}
- Key actions
- User interaction points (WAIT markers)
- Output expectations

### Step 2: {Name}
{Condensed from step-02-*.md}
...

## Critical Rules
{Anti-drift rules extracted from workflow.md "Critical Rules" section}

## Output
- **File:** `_bmad-output/{subfolder}/{filename}`
- **Format:** {description}

## What's Next
After completing this workflow, the next recommended step is:
{guidance from help.md catalog}
```

### 4.2 Handling the Step-File Architecture

The biggest conversion challenge. BMAD's step files are designed to be loaded one-at-a-time to combat context drift. In Agent Skills:

**Strategy: Progressive Disclosure via `references/`**

1. **SKILL.md** contains the workflow overview, critical rules, persona, and a condensed summary of all steps (< 500 lines)
2. **Each step's detailed instructions** move to `references/step-{N}-{name}.md`
3. **SKILL.md instructs the agent** to read each reference file sequentially as it progresses
4. **Anti-drift rules** are embedded prominently at the top of SKILL.md AND repeated in each reference file

Example pattern in SKILL.md:
```markdown
## Workflow Execution

Execute these steps IN ORDER. Load each step's reference file
when you reach it. NEVER load future steps ahead of time.

### Step 1: Initialization
Load and follow: [references/step-01-init.md](references/step-01-init.md)
Complete all instructions before proceeding.

### Step 2: Vision Discovery
WAIT for user confirmation before proceeding.
Load and follow: [references/step-02-vision.md](references/step-02-vision.md)
```

### 4.3 Handling Agent Personas

BMAD uses 10 agent personas. Rather than creating a skill per persona:

- **Embed persona instructions** in each workflow skill's SKILL.md under a "Role" section
- The persona relevant to that workflow gets its communication style, identity, and principles inlined
- This is more reliable than trying to maintain separate persona skills that must be co-activated

### 4.4 Handling YAML-Based Workflows (Phase 4)

The Phase 4 implementation workflows use a `workflow.yaml` + `instructions.xml` + `checklist.md` pattern. Conversion approach:

1. YAML config values → hardcoded paths in SKILL.md frontmatter or body
2. XML instructions → converted to markdown in SKILL.md body or references/
3. Checklist → moved to `references/checklist.md`
4. Template files → moved to `assets/template.md`

### 4.5 Configuration Handling

Create a lightweight shared config approach:
- Each skill references `_bmad/bmm/config.yaml` directly for output paths and settings
- Environment variables (`$REPLIT_USER`, `$REPL_SLUG`) are referenced in instructions
- No separate config skill needed — keep it simple

---

## 5. Anti-Drift Mechanisms

The primary goal is preventing the agent from "drifting off" BMAD workflows. Skills provide several enforcement mechanisms:

### 5.1 Description-Based Auto-Activation
The `description` field ensures the agent activates the right skill when it recognizes BMAD triggers — no routing table parsing needed.

### 5.2 Embedded Critical Rules
Every SKILL.md prominently displays:
```markdown
## CRITICAL RULES (NO EXCEPTIONS)
- NEVER skip steps or optimize the sequence
- NEVER auto-proceed past WAIT points
- NEVER generate content without user input at dialogue steps
- ALWAYS follow the exact instructions in each step
- ALWAYS save output to the specified file path
- ALWAYS present menus and wait for user selection
```

### 5.3 Step-Boundary Enforcement
Each reference file ends with:
```markdown
## STEP COMPLETE
Update frontmatter stepsCompleted. STOP and WAIT for user
to confirm before loading the next step reference.
```

### 5.4 Output Verification
Each skill specifies exact output file paths and formats, making it easy to verify the agent produced the right artifacts.

### 5.5 Cross-Skill Navigation
The `bmad-core` skill provides "what's next?" logic that checks which artifacts exist and guides users to the right next skill — preventing workflow sequence drift.

---

## 6. Migration Path

### Phase A: Parallel Operation (Recommended First Step)
1. Create all Tier 1 skills in `.agents/skills/`
2. Keep `replit.md` routing table intact as fallback
3. Test that skills activate correctly alongside existing BMAD setup
4. Verify workflows execute identically through skills vs. direct file loading

### Phase B: Validation & Refinement
1. Run each converted skill through its full workflow
2. Compare output quality and step adherence against the original
3. Tune `description` fields for reliable activation
4. Add/remove reference files based on context budget testing

### Phase C: Cutover
1. Convert Tier 2 and Tier 3 skills
2. Simplify `replit.md` to reference skills instead of raw routing
3. Eventually remove the routing table from `replit.md` entirely
4. `_bmad/` directory remains as the source-of-truth content library

### Phase D: Portability
1. Skills in `/.agents/skills/` can be installed in any Replit project via `npx skills`
2. Consider publishing to the skills.sh ecosystem for community use
3. Skills are compatible with other agents (Claude Code, Cursor, etc.) via the open standard

---

## 7. Estimated Effort

| Tier | Skills | Est. Hours per Skill | Total |
|------|--------|---------------------|-------|
| Tier 1 (10 skills) | Core + top workflows | 2-4 hours | 20-40 hours |
| Tier 2 (7 skills) | Supporting workflows | 1.5-3 hours | 10-21 hours |
| Tier 3 (9 skills) | Utility & specialty | 1-2 hours | 9-18 hours |
| Testing & tuning | All 26 skills | 0.5-1 hour each | 13-26 hours |
| **Total** | **26 skills** | | **52-105 hours** |

Most of the work is careful condensation of step files into the skill format while preserving exact behavior. The content already exists — it's a translation and restructuring effort, not a creation effort.

---

## 8. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|-----------|
| SKILL.md too large (> 500 lines) for complex workflows like Create PRD | Agent may not load fully | Aggressive use of references/ for step details; keep SKILL.md as overview + rules only |
| Description field doesn't trigger reliably for all BMAD codes | Workflows not activated | Test all trigger phrases; use very specific keywords in descriptions; keep bmad-core as catch-all |
| Step-file sequential enforcement weaker without explicit file loading | Agent may skip steps | Embed numbered checklists with explicit WAIT/STOP markers; add completion verification |
| Agent loads multiple skills simultaneously | Persona conflicts | Ensure each skill is self-contained with its own persona section |
| Keeping skills in sync with upstream BMAD updates | Version drift | Create an update script that regenerates skills from `_bmad/` source files |
| Token budget exceeded with many skills' descriptions loaded | Slower agent startup | Keep descriptions concise (< 200 chars ideally); use specific trigger words |

---

## 9. Recommendation

**Start with Tier 1, specifically `bmad-core`, `bmad-quick-spec`, and `bmad-quick-dev`.** These three skills cover the "simple path" that most users hit daily. They're also relatively self-contained and will validate the entire conversion approach before tackling the more complex multi-step planning workflows.

Once those three work reliably, move to `bmad-create-brief` and `bmad-create-prd` which are the most complex conversions due to their 10+ step sequences. Success with these proves the progressive disclosure pattern works at scale.

The key insight is that Agent Skills give us **native discovery** (no more routing table fragility) and **persistent instructions** (survives chat resets) — both of which directly address the two biggest sources of BMAD drift in the current setup.
