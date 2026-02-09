# BMad Method v6.0.0-Beta.7 — Replit Agent Configuration

## Overview

The BMad Method project provides a comprehensive framework for software development, leveraging a structured, agent-driven approach within the Replit environment. It aims to guide users through the entire software development lifecycle, from initial analysis and planning to implementation and quality assurance, using a suite of specialized AI agents and predefined workflows. The core purpose is to streamline project management, enhance collaboration, and accelerate development by automating routine tasks and providing expert guidance at each stage. It integrates platform intelligence from Replit to provide context-aware assistance.

## User Preferences

- (Will be updated as user expresses preferences)

## System Architecture

The BMad Method operates on a modular architecture centered around specialized AI agents and predefined workflows.

**Core Principles:**
- **Agent-Driven Development:** Utilizes a team of 10 distinct AI agent personas (e.g., Business Analyst, Product Manager, Architect, Developer, QA Engineer, Scrum Master, UX Designer, Technical Writer, Quick Flow Solo Dev, BMad Master), each with a specific role and set of capabilities.
- **Workflow-Based Execution:** Development tasks are structured into sequential workflows, categorized into phases: Assessment (Brownfield), Analysis, Planning, Solutioning, and Implementation. Workflows ensure systematic progress and adherence to best practices.
- **Intent-Based Routing:** User commands are matched against a comprehensive routing table using intent recognition to activate specific agents or workflows. This allows for natural language interaction.
- **Execution Protocol:** Workflows are executed by a core engine (`_bmad/core/tasks/workflow.xml`), ensuring all steps are followed in order, with explicit wait points for user interaction.
- **Configuration Management:** Project-specific settings and agent behaviors are managed through `_bmad/bmm/config.yaml`, while help documentation is cataloged in `_bmad/_config/bmad-help.csv`.
- **UI/UX Decisions:** The system provides structured interactions, presenting agent menus and workflow steps clearly. UX Design workflows are integrated to guide the creation of user interfaces, including Replit preview instructions.
- **Platform Intelligence Integration:** Leverages Replit environment variables (`$REPLIT_USER`, `$REPL_SLUG`, `$LANG`) to personalize interactions and gather project context. This intelligence is integrated across multiple workflows, including retrospectives.
- **Output Management:** Generated artifacts (e.g., briefs, PRDs, architecture documents, sprint plans, code reviews) are systematically stored in the `_bmad-output/` directory, separated into `planning-artifacts/` and `implementation-artifacts/`.

**File Structure Overview:**
- `_bmad/`: Contains the core BMad engine, BMad Methodology Module (BMM) with agents and workflows, configuration files, and agent memory.
- `_bmad-output/`: Stores all generated project artifacts.

## External Dependencies

The BMad Method primarily operates within the Replit environment and relies on its integrated functionalities.

- **Replit Platform:** Core execution environment, providing `$REPLIT_USER`, `$REPL_SLUG`, and `$LANG` environment variables for platform intelligence and context.
- **GitHub:** Used as the source repository for BMad updates (`KatTate/Bmad-for-Replit`) via the `update-bmad.sh` script.