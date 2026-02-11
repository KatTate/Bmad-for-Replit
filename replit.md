# BMad Method v6.0.0-Beta.8 — Replit Agent Configuration

## Overview

The BMad Method project provides a comprehensive framework for software development, leveraging a structured, agent-driven approach within the Replit environment. It aims to guide users through the entire software development lifecycle, from initial analysis and planning to implementation and quality assurance, using a suite of specialized AI agents and predefined workflows. The core purpose is to streamline project management, enhance collaboration, and accelerate development by automating routine tasks and providing expert guidance at each stage. It integrates platform intelligence from Replit to provide context-aware assistance.

## User Preferences

- QA workflow runs per epic completion (not per story) after retrospective, since tests cover full feature scope
- 3-session-per-story workflow cycle: Session 1 (Create Story + party mode review), Session 2 (Dev Story implementation), Session 3 (Code Review + Party Mode + Fix + Close)
- Prefers accessible terminology over technical jargon (e.g., "established projects" over "brownfield")

## Recent Changes (Beta.8-replit.3)

- **Session management guidance**: Added fresh chat prompts to Create Story, Dev Story, and Code Review workflows at optimal session boundaries
- **workflow_path removal**: Replaced forbidden `workflow_path` variable with `installed_path` across 20 step files (quick-spec, quick-dev, create-epics-and-stories, check-implementation-readiness)
- **Technical research routing fix**: step-05 now correctly routes to step-06 with proper stepsCompleted values [1,2,3,4,5,6]
- **Verb standardization**: Replaced "invoke/run" with "load and follow" in brainstorming, help, and review workflows for clearer Replit agent file-following behavior
- **Terminology accessibility**: Renamed "brownfield" to "established project(s)" across user-facing text (routing, CSVs, templates, workflow steps) while preserving internal identifiers
- **QA workflow naming**: Standardized workflow file headers from "Quinn" to "QA" for consistency with agent id pattern

## System Architecture

The BMad Method operates on a modular architecture centered around specialized AI agents and predefined workflows.

**Core Principles:**
- **Agent-Driven Development:** Utilizes a team of 10 distinct AI agent personas (e.g., Business Analyst, Product Manager, Architect, Developer, QA Engineer, Scrum Master, UX Designer, Technical Writer, Quick Flow Solo Dev, BMad Master), each with a specific role and set of capabilities.
- **Workflow-Based Execution:** Development tasks are structured into sequential workflows, categorized into phases: Assessment (Established Projects), Analysis, Planning, Solutioning, and Implementation. Workflows ensure systematic progress and adherence to best practices.
- **Intent-Based Routing:** User commands are matched against a comprehensive routing table using intent recognition to activate specific agents or workflows. This allows for natural language interaction.
- **Execution Protocol:** Workflows are executed by a core engine (`_bmad/core/tasks/workflow.xml`), ensuring all steps are followed in order, with explicit wait points for user interaction.
- **Configuration Management:** Project-specific settings and agent behaviors are managed through `_bmad/bmm/config.yaml`, while help documentation is cataloged in `_bmad/_config/bmad-help.csv`.
- **UI/UX Decisions:** The system provides structured interactions, presenting agent menus and workflow steps clearly. UX Design workflows are integrated to guide the creation of user interfaces, including Replit preview instructions.
- **Platform Intelligence Integration:** Leverages Replit environment variables (`$REPLIT_USER`, `$REPL_SLUG`, `$LANG`) to personalize interactions and gather project context. This intelligence is integrated across multiple workflows, including retrospectives.
- **Output Management:** Generated artifacts (e.g., briefs, PRDs, architecture documents, sprint plans, code reviews) are systematically stored in the `_bmad-output/` directory, separated into `planning-artifacts/` and `implementation-artifacts/`.
- **Session Management:** Fresh chat boundaries are recommended at natural workflow breakpoints (after story creation and after implementation) to optimize agent context and performance.

**File Structure Overview:**
- `_bmad/`: Contains the core BMad engine, BMad Methodology Module (BMM) with agents and workflows, configuration files, and agent memory.
- `_bmad-output/`: Stores all generated project artifacts.

## External Dependencies

The BMad Method primarily operates within the Replit environment and relies on its integrated functionalities.

- **Replit Platform:** Core execution environment, providing `$REPLIT_USER`, `$REPL_SLUG`, and `$LANG` environment variables for platform intelligence and context.
- **GitHub:** Used as the source repository for BMad updates (`KatTate/Bmad-for-Replit`) via the `update-bmad.sh` script.
