# Project Documentation

## Overview

The BMad Method project provides a comprehensive, agent-driven framework for software development within the Replit environment. Its purpose is to guide users through the entire software development lifecycle—from analysis and planning to implementation and quality assurance—using specialized AI agents and predefined workflows. The project aims to streamline management, enhance collaboration, and accelerate development by automating routine tasks and offering expert guidance, leveraging Replit's platform intelligence for context-aware assistance.

## User Preferences

- QA workflow runs per epic completion (not per story) after retrospective, since tests cover full feature scope
- 3-session-per-story workflow cycle: Session 1 (Create Story + party mode review), Session 2 (Dev Story implementation), Session 3 (Code Review + Party Mode + Fix + Close)
- Prefers accessible terminology over technical jargon (e.g., "established projects" over "brownfield")

## System Architecture

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

## External Dependencies

- **Replit Platform:** Core execution environment, providing `$REPLIT_USER`, `$REPL_SLUG`, and `$LANG` environment variables for platform intelligence and context.
- **GitHub:** Used as the source repository for BMad updates (`KatTate/Bmad-for-Replit`) via the `update-bmad.sh` script.