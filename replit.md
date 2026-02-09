<!-- BMAD-METHOD-START -->
# BMad Method v6.0.0-Beta.7 — Replit Agent Configuration

## Overview

This project uses the **BMad Method** — an AI-driven agile development framework. It provides structured agent personas and workflows that guide projects from idea through implementation.

**How to use:** Just speak naturally. Say things like "act as the PM", "create a PRD", "what should I do next?", or use any 2-letter code (BP, CP, CA, etc.).

## Routing

When the user's message matches a BMAD trigger phrase, agent name, or workflow code below:

1. **Match the request** to an agent or workflow using the trigger phrases in the tables below
2. **Load the matched file** and follow its instructions
3. **For workflows:** Execute using `_bmad/core/tasks/workflow.xml` as the execution engine
4. **For agents:** Adopt the persona and present the agent's menu
5. **For "what's next?" or "help":** Execute `_bmad/core/tasks/help.md`

## Agent Routing

| Trigger Phrases | Agent | File |
|---|---|---|
| "act as analyst", "be the analyst", "I need Mary", "business analysis", "brainstorm" | Mary — 📊 Business Analyst | `_bmad/bmm/agents/analyst.md` |
| "act as PM", "be the PM", "I need John", "product manager", "create PRD", "product requirements" | John — 📋 Product Manager | `_bmad/bmm/agents/pm.md` |
| "act as architect", "be the architect", "I need Winston", "architecture", "technical design" | Winston — 🏗️ Architect | `_bmad/bmm/agents/architect.md` |
| "act as UX designer", "be the designer", "I need Sally", "UX design", "user experience" | Sally — 🎨 UX Designer | `_bmad/bmm/agents/ux-designer.md` |
| "act as dev", "be the developer", "I need Amelia", "implement story", "dev story" | Amelia — 💻 Developer Agent | `_bmad/bmm/agents/dev.md` |
| "act as QA", "be QA", "I need Quinn", "quality assurance", "test" | Quinn — 🧪 QA Engineer | `_bmad/bmm/agents/qa.md` |
| "act as scrum master", "be the SM", "I need Bob", "sprint planning", "sprint status" | Bob — 🏃 Scrum Master | `_bmad/bmm/agents/sm.md` |
| "act as tech writer", "be the writer", "I need Paige", "documentation", "write document" | Paige — 📚 Technical Writer | `_bmad/bmm/agents/tech-writer/tech-writer.md` |
| "act as quick flow dev", "quick flow", "I need Barry", "solo dev", "quick build" | Barry — 🚀 Quick Flow Solo Dev | `_bmad/bmm/agents/quick-flow-solo-dev.md` |
| "act as BMad", "BMad master", "start BMad", "begin", "initialize" | BMad Master | `_bmad/core/agents/bmad-master.md` |

## Workflow Routing — Phase 0: Assessment (Brownfield)

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "assess brownfield", "AB", "scan existing project", "brownfield assessment", "assess this project", "what do I have here?" | AB | Assess Brownfield | `_bmad/bmm/workflows/0-assess/assess-brownfield/workflow.md` |

## Workflow Routing — Phase 1: Analysis

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "brainstorm", "brainstorm project", "BP", "generate ideas" | BP | Brainstorm Project | `_bmad/core/workflows/brainstorming/workflow.md` |
| "market research", "MR", "competitive analysis", "market analysis" | MR | Market Research | `_bmad/bmm/workflows/1-analysis/research/workflow-market-research.md` |
| "domain research", "DR", "industry research", "domain deep dive" | DR | Domain Research | `_bmad/bmm/workflows/1-analysis/research/workflow-domain-research.md` |
| "technical research", "TR", "tech feasibility", "technology research" | TR | Technical Research | `_bmad/bmm/workflows/1-analysis/research/workflow-technical-research.md` |
| "create brief", "CB", "product brief", "project brief" | CB | Create Brief | `_bmad/bmm/workflows/1-analysis/create-product-brief/workflow.md` |

## Workflow Routing — Phase 2: Planning

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "create PRD", "CP", "product requirements", "requirements document" | CP | Create PRD | `_bmad/bmm/workflows/2-plan-workflows/create-prd/workflow-create-prd.md` |
| "validate PRD", "VP", "review PRD", "check PRD" | VP | Validate PRD | `_bmad/bmm/workflows/2-plan-workflows/create-prd/workflow-validate-prd.md` |
| "edit PRD", "EP", "update PRD", "modify PRD" | EP | Edit PRD | `_bmad/bmm/workflows/2-plan-workflows/create-prd/workflow-edit-prd.md` |
| "create UX", "CU", "UX design", "design the UX", "user experience design" | CU | Create UX | `_bmad/bmm/workflows/2-plan-workflows/create-ux-design/workflow.md` |

## Workflow Routing — Phase 3: Solutioning

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "create architecture", "CA", "architect the solution", "technical architecture" | CA | Create Architecture | `_bmad/bmm/workflows/3-solutioning/create-architecture/workflow.md` |
| "create epics", "CE", "epics and stories", "create stories", "break into stories" | CE | Create Epics and Stories | `_bmad/bmm/workflows/3-solutioning/create-epics-and-stories/workflow.md` |
| "check readiness", "IR", "implementation readiness", "ready to implement?" | IR | Check Implementation Readiness | `_bmad/bmm/workflows/3-solutioning/check-implementation-readiness/workflow.md` |

## Workflow Routing — Phase 4: Implementation

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "sprint planning", "SP", "plan the sprint", "create sprint plan" | SP | Sprint Planning | `_bmad/bmm/workflows/4-implementation/sprint-planning/workflow.yaml` |
| "sprint status", "SS", "where are we?", "what's the sprint status?" | SS | Sprint Status | `_bmad/bmm/workflows/4-implementation/sprint-status/workflow.yaml` |
| "create story", "CS", "prepare next story", "next story" | CS | Create Story | `_bmad/bmm/workflows/4-implementation/create-story/workflow.yaml` |
| "validate story", "VS", "check story", "story ready?" | VS | Validate Story | `_bmad/bmm/workflows/4-implementation/create-story/workflow.yaml` |
| "dev story", "DS", "implement story", "build the story", "code the story" | DS | Dev Story | `_bmad/bmm/workflows/4-implementation/dev-story/workflow.yaml` |
| "QA test", "QA", "automate tests", "create tests", "test automation" | QA | QA Automation Test | `_bmad/bmm/workflows/qa/automate/workflow.yaml` |
| "code review", "CR", "review code", "review my code" | CR | Code Review | `_bmad/bmm/workflows/4-implementation/code-review/workflow.yaml` |
| "retrospective", "ER", "epic retro", "what went well?" | ER | Retrospective | `_bmad/bmm/workflows/4-implementation/retrospective/workflow.yaml` |

## Workflow Routing — Anytime

| Trigger Phrases | Code | Workflow | File |
|---|---|---|---|
| "document project", "DP", "analyze codebase", "scan project" | DP | Document Project | `_bmad/bmm/workflows/document-project/workflow.yaml` |
| "generate project context", "GPC", "project context", "scan codebase for context" | GPC | Generate Project Context | `_bmad/bmm/workflows/generate-project-context/workflow.md` |
| "quick spec", "QS", "quick architecture", "fast spec" | QS | Quick Spec | `_bmad/bmm/workflows/bmad-quick-flow/quick-spec/workflow.md` |
| "quick dev", "QD", "quick build", "just build it", "quick implementation" | QD | Quick Dev | `_bmad/bmm/workflows/bmad-quick-flow/quick-dev/workflow.md` |
| "correct course", "CC", "change direction", "pivot", "we need to change" | CC | Correct Course | `_bmad/bmm/workflows/4-implementation/correct-course/workflow.yaml` |
| "write document", "WD", "create document", "draft document" | WD | Write Document | `_bmad/bmm/agents/tech-writer/tech-writer.agent.yaml` |
| "update standards", "US", "documentation standards", "update writing rules" | US | Update Standards | `_bmad/bmm/agents/tech-writer/tech-writer.agent.yaml` |
| "mermaid", "MG", "create diagram", "generate diagram" | MG | Mermaid Generate | `_bmad/bmm/agents/tech-writer/tech-writer.agent.yaml` |
| "validate document", "VD", "review document", "check document quality" | VD | Validate Document | `_bmad/bmm/agents/tech-writer/tech-writer.agent.yaml` |
| "explain concept", "EC", "explain this", "break it down" | EC | Explain Concept | `_bmad/bmm/agents/tech-writer/tech-writer.agent.yaml` |
| "party mode", "PM", "multi-agent", "agent discussion", "group review" | PM | Party Mode | `_bmad/core/workflows/party-mode/workflow.md` |
| "what should I do next?", "help", "BH", "what's next?", "I'm stuck" | BH | BMad Help | `_bmad/core/tasks/help.md` |
| "index docs", "ID", "create index", "index documents" | ID | Index Docs | `_bmad/core/tasks/index-docs.xml` |
| "shard document", "SD", "split document", "break up document" | SD | Shard Document | `_bmad/core/tasks/shard-doc.xml` |
| "editorial review prose", "review prose", "polish writing" | — | Editorial Review - Prose | `_bmad/core/tasks/editorial-review-prose.xml` |
| "editorial review structure", "review structure", "reorganize document" | — | Editorial Review - Structure | `_bmad/core/tasks/editorial-review-structure.xml` |
| "adversarial review", "AR", "critical review", "find weaknesses" | AR | Adversarial Review | `_bmad/core/tasks/review-adversarial-general.xml` |

## Routing Priority

1. **Exact code match** — If user types a 2-letter code (BP, CP, CA, etc.), route directly to that workflow
2. **Agent name match** — If user mentions an agent by name (Mary, John, Winston, etc.), load that agent
3. **Keyword match** — Match against trigger phrases in the tables above
4. **Ambiguous request** — If unclear, ask the user to clarify or suggest the most likely match
5. **"What's next?" / "help"** — Always route to `_bmad/core/tasks/help.md`

## Execution Protocol

When a route is matched:
1. Read the target file
2. For agents: adopt the persona and present their menu
3. For workflows: execute following `_bmad/core/tasks/workflow.xml` execution engine
4. For tasks: execute the task directly
5. Load relevant config from `_bmad/bmm/config.yaml` and `_bmad/core/config.yaml`

## Project State

- **Current Phase:** not started
- **Project Type:** greenfield
- **Completed Artifacts:** none yet

## File Structure

```
BMAD-README.md            # Complete guide to using BMad in Replit

_bmad/                    # BMad Method toolkit
├── README.md             # Source copy of BMAD-README.md
├── core/                 # Core engine (workflow executor, help, brainstorming)
│   ├── agents/           # BMad Master agent
│   ├── tasks/            # Help, workflow engine, editorial tasks
│   └── workflows/        # Brainstorming, party mode, elicitation
├── bmm/                  # BMad Methodology Module
│   ├── agents/           # 10 specialist agent personas
│   ├── workflows/        # All phase workflows (analysis → implementation)
│   ├── data/             # Templates and context files
│   └── teams/            # Team configurations for party mode
├── _config/              # Manifests, help catalog, customization
├── _memory/              # Agent memory (tech writer standards)
└── replit-routing.md     # Routing source (auto-inlined into replit.md on install)

_bmad-output/             # Generated artifacts go here
├── planning-artifacts/   # Briefs, PRDs, architecture, UX docs
└── implementation-artifacts/  # Sprint plans, stories, reviews
```

## Configuration

- **User config:** `_bmad/core/config.yaml` (user name, language)
- **Project config:** `_bmad/bmm/config.yaml` (project name, skill level, output paths)
- **Help catalog:** `_bmad/_config/bmad-help.csv` (phase-sequenced workflow guide)
<!-- BMAD-METHOD-END -->

## Installation (for dropping into other projects)

To install BMad into an existing Replit project:
1. Copy `_bmad/` folder and `install-bmad.sh` into the project root
2. Run: `bash install-bmad.sh`
3. The script auto-detects brownfield vs greenfield and safely merges with any existing `replit.md`
4. The full routing table is automatically inlined into `replit.md` so the agent can route without reading external files

## Updating BMad in Installed Projects

Each installed project includes `update-bmad.sh`. Run `bash update-bmad.sh` to pull the latest version from the GitHub source repo (`KatTate/Bmad-for-Replit`). The script preserves user config files and `_bmad-output/`, and re-inlines the routing table into `replit.md`. Version tracking is in `_bmad/_config/version.txt`.

## Recent Changes

- 2026-02-09: Auto-inline routing table into replit.md — install and update scripts now embed the full routing table directly into replit.md instead of referencing an external file
- 2026-02-09: Comprehensive platform intelligence integration across 7 workflows
- 2026-02-09: Enhanced retrospective workflow with Replit platform intelligence
- 2026-02-09: Added Sub-Agent Party Mode
- 2026-02-09: Fixed user-facing story UI gap
- 2026-02-09: Added BMAD-README.md
- 2026-02-09: Completed implementation execution layer adaptation
- 2026-02-09: Updated Code Review (CR) workflow to align with new story format
- 2026-02-08: Adapted Create Story (CS) and Dev Story (DS) workflows for Replit Agent
- 2026-02-08: Added Replit preview instructions to UX Design workflow
- 2026-02-08: Improved brownfield/greenfield detection
- 2026-02-08: Completed thorough upstream sync review (Beta.1-Beta.7)
- 2026-02-08: Added update mechanism
- 2026-02-08: Synced upstream fixes
- 2026-02-06: Created install script for brownfield project integration
- 2026-02-06: Added brownfield assessment workflow (AB)
- 2026-02-06: Converted from Cursor IDE to Replit Agent
- 2026-02-06: Installed BMad Method v6.0.0-Beta.7

## User Preferences

- (Will be updated as user expresses preferences)
