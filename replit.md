

<!-- PROTECTION NOTE FOR REPLIT AGENT: The content between BMAD-METHOD-START and BMAD-METHOD-END markers is part of the BMad Method framework and MUST NOT be modified, overwritten, or removed during any replit.md updates. When updating this file, only modify the "Project Documentation" section AFTER the BMAD-METHOD-END marker. Always preserve both sections intact. -->

<!-- BMAD-METHOD-START -->
# BMad Method v6.0.0-beta.8-replit.4 — Agent Configuration

## IMPORTANT: How You Must Operate in This Project

This is a **BMad Method** project. BMAD workflows are activated through **Replit Agent Skills** installed in `.agents/skills/bmad-*/`. You MUST follow these rules in every conversation:

1. **BMAD skills handle workflow activation.** When a user's message matches a BMAD skill trigger (e.g., "create PRD", "code review", "party mode"), the skill will activate and provide instructions for loading the correct workflow files. Follow those instructions exactly.
2. **When a skill activates, load the referenced files and follow them.** Do not answer in your own words. Load the workflow or agent file specified in the skill and execute it.
3. **For workflows:** The skill will instruct you to either load `_bmad/core/tasks/workflow.xml` (the execution engine) with a workflow YAML config, or load a workflow markdown file directly. Execute ALL steps IN ORDER. When a step says WAIT for user input, STOP and WAIT.
4. **For agents:** Load the agent file, adopt that persona completely, and present the agent's menu.
5. **Never skip, summarize, or improvise** workflow steps. Never auto-proceed past WAIT points.
6. **If no skill activates,** respond normally but remain aware that this is a BMAD project. If the user seems to be asking about project planning, development, or process, suggest the relevant BMAD workflow. Say "help" or "BH" anytime for guidance.
7. **If unsure whether a BMAD workflow applies,** ask: "Would you like me to run the [workflow name] workflow for that?"

## BMad File Structure

```
_bmad/                    # BMad Method toolkit
├── core/                 # Core engine (workflow executor, help, brainstorming)
│   ├── agents/           # BMad Master agent
│   ├── tasks/            # Help, workflow engine, editorial tasks
│   └── workflows/        # Brainstorming, party mode, elicitation
├── bmm/                  # BMad Methodology Module
│   ├── agents/           # 9 specialist agent personas
│   ├── workflows/        # All phase workflows (analysis → implementation)
│   ├── data/             # Templates and context files
│   └── teams/            # Team configurations for party mode
├── _config/              # Manifests, help catalog, customization
└── _memory/              # Agent memory (tech writer standards)

.agents/skills/bmad-*/    # Replit Agent Skills (workflow activation)

_bmad-output/             # Generated artifacts go here
├── planning-artifacts/   # Briefs, PRDs, architecture, UX docs
└── implementation-artifacts/  # Sprint plans, stories, reviews
```

## BMad Configuration

- **BMAD config:** `_bmad/bmm/config.yaml` (skill level, output paths — BMAD-specific settings only)
- **Help catalog:** `_bmad/_config/bmad-help.csv` (phase-sequenced workflow guide)
- **Platform values:** User name, project name, and language are resolved automatically from Replit environment ($REPLIT_USER, $REPL_SLUG, $LANG)

**IMPORTANT:** Do NOT embed the contents of BMad config files (config.yaml, etc.) into this replit.md. Only reference them by file path above. Read them from disk when needed.
<!-- BMAD-METHOD-END -->

## Project Documentation

> This section is safe for the Replit agent to update. Add project-specific information below.

### Overview

The BMad Method project provides a comprehensive framework for software development, leveraging a structured, agent-driven approach within the Replit environment. It aims to guide users through the entire software development lifecycle, from initial analysis and planning to implementation and quality assurance, using a suite of specialized AI agents and predefined workflows. The core purpose is to streamline project management, enhance collaboration, and accelerate development by automating routine tasks and providing expert guidance at each stage. It integrates platform intelligence from Replit to provide context-aware assistance.

### User Preferences

- QA workflow runs per epic completion (not per story) after retrospective, since tests cover full feature scope
- 3-session-per-story workflow cycle: Session 1 (Create Story + party mode review), Session 2 (Dev Story implementation), Session 3 (Code Review + Party Mode + Fix + Close)
- Prefers accessible terminology over technical jargon (e.g., "established projects" over "brownfield")

### Recent Changes (Beta.8-replit.7)

- **Dev Story workflow restructured (11 steps)**: Restored the official BMAD multi-step structure to fix agents consistently skipping later steps (story doc updates, sprint status updates). The previous Replit adaptation had collapsed the workflow into 6 steps with a massive "Plan and implement" step, causing agents to lose track after implementation. Now uses 11 bounded steps: load → context → review detection → sprint status → plan → implement → test → verify ACs → platform checks → update docs → communicate completion. Replit adaptations preserved (agent-driven planning, LSP diagnostics, git status, screenshots).
- **SKILL.md enhanced**: Now includes explicit 11-step summary and highlights steps 10-11 as commonly missed, providing structural reinforcement for agent compliance.
- **Checklist.md expanded**: Restored comprehensive validation sections from official BMAD (Context Validation, AC Verification, Testing, User-Facing Delivery, Documentation & Traceability) plus Replit-specific Platform Verification section.
- **Variable alignment fix**: Corrected `story_path` → `story_file` mismatch between instructions.xml and workflow.yaml that could block story loading.

### Previous Changes (Beta.8-replit.6)

- **Skills-only activation**: Removed routing table from replit.md — BMAD workflows now activate exclusively through Replit Agent Skills (`.agents/skills/bmad-*/`). The replit.md BMAD section is now a slim awareness block that tells the agent "this is a BMAD project, skills handle activation."
- **Install/update script overhaul**: Both `install-bmad.sh` and `update-bmad.sh` now copy skills during install/update and generate the slim awareness block instead of inlining the routing table. Scripts bumped to v6.0.0-Beta.8.
- **No dual activation**: Routing table removed — skills are the single activation mechanism.

### Previous Changes (Beta.8-replit.5)

- **Skills conversion (28 total)**: Converted all 26 BMAD workflows + 2 utility tasks into Replit Agent Skills format (`.agents/skills/bmad-*/SKILL.md`). Skills use the "thin wrapper/pointer" approach — each SKILL.md contains activation logic, critical rules, and file pointers to existing `_bmad/` workflows. Zero content duplication. Skills enable native Replit Agent discovery and prevent agent drift across chat sessions.
- **Skill naming**: All skills use `bmad-` prefix for namespace grouping (e.g., `bmad-create-prd`, `bmad-dev-story`)

### Previous Changes (Beta.8-replit.4)

- **replit.md protection**: Added BMAD-METHOD-START/END markers with protective HTML comment to prevent Replit agent from overwriting BMad configuration during project updates
- **Session management guidance**: Added fresh chat prompts to Create Story, Dev Story, and Code Review workflows at optimal session boundaries
- **workflow_path removal**: Replaced forbidden `workflow_path` variable with `installed_path` across 20 step files (quick-spec, quick-dev, create-epics-and-stories, check-implementation-readiness)
- **Technical research routing fix**: step-05 now correctly routes to step-06 with proper stepsCompleted values [1,2,3,4,5,6]
- **Verb standardization**: Replaced "invoke/run" with "load and follow" in brainstorming, help, and review workflows for clearer Replit agent file-following behavior
- **Terminology accessibility**: Renamed "brownfield" to "established project(s)" across user-facing text (routing, CSVs, templates, workflow steps) while preserving internal identifiers
- **QA workflow naming**: Standardized workflow file headers from "Quinn" to "QA" for consistency with agent id pattern

### System Architecture

The BMad Method operates on a modular architecture centered around specialized AI agents and predefined workflows.

**Core Principles:**
- **Agent-Driven Development:** Utilizes a team of 10 distinct AI agent personas (e.g., Business Analyst, Product Manager, Architect, Developer, QA Engineer, Scrum Master, UX Designer, Technical Writer, Quick Flow Solo Dev, BMad Master), each with a specific role and set of capabilities.
- **Workflow-Based Execution:** Development tasks are structured into sequential workflows, categorized into phases: Assessment (Established Projects), Analysis, Planning, Solutioning, and Implementation. Workflows ensure systematic progress and adherence to best practices.
- **Skills-Based Activation:** BMAD workflows are activated through Replit Agent Skills (`.agents/skills/bmad-*/`), which provide native platform discovery and persistent instructions across chat sessions.
- **Execution Protocol:** Workflows are executed by a core engine (`_bmad/core/tasks/workflow.xml`), ensuring all steps are followed in order, with explicit wait points for user interaction.
- **Configuration Management:** Project-specific settings and agent behaviors are managed through `_bmad/bmm/config.yaml`, while help documentation is cataloged in `_bmad/_config/bmad-help.csv`.
- **Platform Intelligence Integration:** Leverages Replit environment variables (`$REPLIT_USER`, `$REPL_SLUG`, `$LANG`) to personalize interactions and gather project context.
- **Output Management:** Generated artifacts are systematically stored in the `_bmad-output/` directory, separated into `planning-artifacts/` and `implementation-artifacts/`.
- **Session Management:** Fresh chat boundaries are recommended at natural workflow breakpoints (after story creation and after implementation) to optimize agent context and performance.

### External Dependencies

- **Replit Platform:** Core execution environment, providing `$REPLIT_USER`, `$REPL_SLUG`, and `$LANG` environment variables for platform intelligence and context.
- **GitHub:** Used as the source repository for BMad updates (`KatTate/Bmad-for-Replit`) via the `update-bmad.sh` script.
