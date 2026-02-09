# BMad Method v6.0.0-Beta.7 — Replit Agent Configuration

## Overview

This project uses the **BMad Method** — an AI-driven agile development framework. It provides structured agent personas and workflows that guide projects from idea through implementation.

**How to use:** Just speak naturally. Say things like "act as the PM", "create a PRD", "what should I do next?", or use any 2-letter code (BP, CP, CA, etc.).

## Routing

When the user's message matches a BMAD trigger phrase, agent name, or workflow code:

1. **Read the routing table:** `_bmad/replit-routing.md`
2. **Match the request** to an agent or workflow using the trigger phrases listed there
3. **Load the matched file** and follow its instructions
4. **For workflows:** Execute using `_bmad/core/tasks/workflow.xml` as the execution engine
5. **For agents:** Adopt the persona and present the agent's menu
6. **For "what's next?" or "help":** Execute `_bmad/core/tasks/help.md`

## Quick Reference — Agents

| Say | Agent | Role |
|---|---|---|
| "act as analyst" or "Mary" | 📊 Business Analyst | Brainstorming, research, briefs |
| "act as PM" or "John" | 📋 Product Manager | PRDs, epics, stories |
| "act as architect" or "Winston" | 🏗️ Architect | Technical architecture |
| "act as UX designer" or "Sally" | 🎨 UX Designer | User experience design |
| "act as dev" or "Amelia" | 💻 Developer | Story implementation |
| "act as QA" or "Quinn" | 🧪 QA Engineer | Testing and quality |
| "act as SM" or "Bob" | 🏃 Scrum Master | Sprint planning and management |
| "act as tech writer" or "Paige" | 📚 Technical Writer | Documentation |
| "quick flow" or "Barry" | 🚀 Quick Flow Solo Dev | Fast builds, simple projects |
| "start BMad" | BMad Master | Initialize and get oriented |

## Quick Reference — Key Workflows

| Say | Code | What It Does |
|---|---|---|
| "assess brownfield" | AB | Scan existing project, find best BMAD entry point |
| "brainstorm" | BP | Generate and explore ideas |
| "create brief" | CB | Nail down the product idea |
| "create PRD" | CP | Product requirements document |
| "create architecture" | CA | Technical architecture |
| "create epics" | CE | Break work into epics and stories |
| "sprint planning" | SP | Plan the implementation sprint |
| "dev story" | DS | Implement a story |
| "code review" | CR | Review implemented code |
| "what's next?" | BH | Get guidance on next steps |
| "quick spec" | QS | Fast technical spec (simple projects) |
| "quick dev" | QD | Fast implementation (simple projects) |

## Project State

- **Current Phase:** not started
- **Project Type:** greenfield
- **Completed Artifacts:** none yet

## File Structure

```
BMAD-README.md            # Complete guide to using BMad in Replit

_bmad/                    # BMad Method toolkit
├── README.md             # Source copy of BMAD-README.md (distributed on install/update)
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
└── replit-routing.md     # Trigger phrase → file routing table

_bmad-output/             # Generated artifacts go here
├── planning-artifacts/   # Briefs, PRDs, architecture, UX docs
└── implementation-artifacts/  # Sprint plans, stories, reviews
```

## Configuration

- **User config:** `_bmad/core/config.yaml` (user name, language)
- **Project config:** `_bmad/bmm/config.yaml` (project name, skill level, output paths)
- **Help catalog:** `_bmad/_config/bmad-help.csv` (phase-sequenced workflow guide)

## Installation (for dropping into other projects)

To install BMad into an existing Replit project:
1. Copy `_bmad/` folder and `install-bmad.sh` into the project root
2. Run: `bash install-bmad.sh`
3. The script auto-detects brownfield vs greenfield and safely merges with any existing `replit.md`

## Updating BMad in Installed Projects

Each installed project includes `update-bmad.sh`. Run `bash update-bmad.sh` to pull the latest version from the GitHub source repo (`KatTate/Bmad-for-Replit`). The script preserves user config files and `_bmad-output/`. Version tracking is in `_bmad/_config/version.txt`.

## Recent Changes

- 2026-02-09: Fixed user-facing story UI gap — added "User-Facing Story Principle" to epic/story creation (step-03), create-story instructions/checklist/template, and dev-story instructions/checklist. Stories for end users now require UI-focused ACs (no API specs), a UI/UX Deliverables section, frontend files in File Change Summary, and pre/post-implementation UI checks in the dev workflow. Prevents dev agents from delivering API-only implementations for user-facing features.
- 2026-02-09: Added BMAD-README.md — comprehensive Replit-specific guide covering all agents, workflows, story cycle, quick flow, and anytime tools; distributed via install and update scripts
- 2026-02-09: Completed implementation execution layer adaptation — dev agent persona, Quick Dev workflow (steps 3-6), Quick Spec (step 3 + template) all shifted from checkbox task scripts to AC-driven approach with architectural guidance; platform review tools replace custom adversarial review invocations
- 2026-02-09: Updated Code Review (CR) workflow to align with new story format — reviews verify against acceptance criteria and dev notes constraints instead of Tasks/Subtasks checkboxes, findings go to "Code Review Notes" section, removed forced minimum issue quota
- 2026-02-08: Adapted Create Story (CS) and Dev Story (DS) workflows for Replit Agent — stories are now intent-and-constraint context documents (not implementation scripts), dev workflow lets agent plan its own approach, dropped universal TDD mandate, uses platform's architect tool for review
- 2026-02-08: Added Replit preview instructions to UX Design workflow steps 8 and 9 for HTML visualizer files
- 2026-02-08: Added explanatory comment to tool-manifest.csv for Replit context
- 2026-02-08: Improved brownfield/greenfield detection — no longer triggered by Replit's default scaffolding (empty src/ dirs, bare package.json)
- 2026-02-08: Completed thorough upstream sync review (Beta.1-Beta.7) — confirmed only 3 content fixes apply; all other changes are CLI/IDE tooling, not methodology content
- 2026-02-08: Added update mechanism — `update-bmad.sh` pulls latest from GitHub, preserves user configs, reports version changes
- 2026-02-08: Synced upstream fixes — fixed help task path (7 files), added Party Mode return protocol, removed Claude Code-specific references
- 2026-02-06: Created install script for brownfield project integration
- 2026-02-06: Added brownfield assessment workflow (AB) for existing Replit projects
- 2026-02-06: Converted from Cursor IDE to Replit Agent (natural language triggers replace slash commands)
- 2026-02-06: Installed BMad Method v6.0.0-Beta.7

## User Preferences

- (Will be updated as user expresses preferences)
