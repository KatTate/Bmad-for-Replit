# BMad Method — Replit Installation Guide

**Version:** 6.0.0-Beta.7

This guide covers two scenarios:

- **Scenario A** — Adding BMad to an existing Replit project (you already have code)
- **Scenario B** — Starting a brand-new project from scratch using BMad

---

## What You'll Need

- A Replit account (free or paid)
- The BMad Method zip file downloaded to your computer

---

## Scenario A: Add BMad to an Existing Project

This is the simplest path. Two steps.

### Step 1: Attach the Zip File

In your Replit project, click the **attachment button** (paperclip icon) in the Agent chat and attach the BMad zip file.

### Step 2: Tell the Agent to Install It

Type something like:

> "Unzip and install this file, then follow the instructions"

That's it. The agent handles everything — unzipping, running the installer, setting up the configuration. Your existing code and settings are preserved.

### After Installation

Start a **new chat** and say **"assess brownfield"** (or just **"AB"**). This scans your project and recommends the best starting point in the BMad workflow based on what you already have built.

---

## Scenario B: Start a New Project with BMad

When you go to create a new project on Replit, you'll see a screen asking "What do you want to make?" with several options. Here's what to pick:

### Step 1: Create the Project

1. On the Replit home screen, select the **App** tab (not Design)
2. Set the mode dropdown to **Build**
3. For the project type, select **Start from scratch**
4. In the description box, type something like:

> "Set up a blank project. Don't build anything yet."

5. Click **Start**

This gives you a clean, empty project with Agent ready to go.

### Step 2: Attach and Install BMad

Once the project opens:

1. Click the **attachment button** (paperclip icon) in the Agent chat and attach the BMad zip file
2. Tell the agent:

> "Unzip and install this file, then follow the instructions"

The agent will set everything up.

### After Installation

Start a **new chat** and say one of the following to get going:

- **"start BMad"** — Get oriented and learn what to do first
- **"brainstorm"** — Jump straight into generating ideas
- **"what should I do next?"** — Get a recommendation for your next step

---

## Quick Command Reference

Once installed, you can use any of these in the Agent chat:

### Workflows

| What to Say | What It Does |
|---|---|
| "start BMad" | Initialize and get oriented |
| "assess brownfield" or "AB" | Scan existing project, find best entry point |
| "brainstorm" or "BP" | Generate and explore ideas |
| "create brief" or "CB" | Nail down the product idea |
| "create PRD" or "CP" | Create product requirements document |
| "create architecture" or "CA" | Design the technical architecture |
| "create epics" or "CE" | Break work into epics and stories |
| "sprint planning" or "SP" | Plan the implementation sprint |
| "dev story" or "DS" | Implement a user story |
| "code review" or "CR" | Review implemented code |
| "what's next?" or "BH" | Get guidance on next steps |
| "quick spec" or "QS" | Fast technical spec (simple projects) |
| "quick dev" or "QD" | Fast implementation (simple projects) |

### Agents

You can also call agents by name:

| Say | Agent |
|---|---|
| "act as analyst" or "Mary" | Business Analyst |
| "act as PM" or "John" | Product Manager |
| "act as architect" or "Winston" | Architect |
| "act as UX designer" or "Sally" | UX Designer |
| "act as dev" or "Amelia" | Developer |
| "act as QA" or "Quinn" | QA Engineer |
| "act as SM" or "Bob" | Scrum Master |
| "act as tech writer" or "Paige" | Technical Writer |
| "quick flow" or "Barry" | Quick Flow Solo Dev |

---

## Recommended Workflow Order

### For New Projects

Full workflow:
```
brainstorm → create brief → create PRD → create architecture → create epics → sprint planning → dev story
```

Simplified path for small projects:
```
brainstorm → quick spec → quick dev
```

### For Existing Projects

```
assess brownfield → (follow the recommended entry point) → continue through the workflow
```

### Anytime You're Unsure

Just say **"what should I do next?"** and BMad will figure out where you are and tell you what comes next.

---

## Troubleshooting

### Agent doesn't respond to BMad commands

The agent reads the project configuration at the start of each conversation. If BMad commands aren't working:

1. Make sure the installation completed successfully
2. **Start a new chat** — the agent only picks up the configuration when a conversation begins

### The zip extracted into a subfolder

Sometimes the zip extracts into a nested folder (like `bmad-method-main/`) instead of putting files directly in the project root. If that happens, just tell the agent:

> "Move the contents of the bmad-method folder to the project root and run the install script"

### verify-bmad.sh shows unexpected results

You can optionally run `bash verify-bmad.sh` in the Shell to check the installation. Common messages:

- **FAIL about ".cursor directory":** Only relevant if migrating from Cursor IDE — safe to ignore
- **WARN about output directories:** Run the install script again to create them
- **WARN about help.md:** Cosmetic, doesn't affect anything
- **FAIL about missing files:** Re-upload and install the BMad package

---

## What Gets Installed

```
your-project/
├── _bmad/                          # BMad toolkit (don't modify)
├── _bmad-output/                   # Your generated documents go here
│   ├── planning-artifacts/         # Briefs, PRDs, architecture docs
│   └── implementation-artifacts/   # Sprint plans, stories, reviews
├── install-bmad.sh                 # Installer (safe to delete after install)
├── verify-bmad.sh                  # Verification (safe to delete after install)
├── replit.md                       # Project config (agent reads this)
└── (your existing project files)   # Untouched
```

---

## Tips

- **Always start a new chat** after installing BMad so the agent picks up the new configuration
- **You can re-run the installer** safely — it won't damage your existing content
- **The `_bmad-output/` folder** is where all your planning documents get saved
- **Configuration files** are in `_bmad/core/config.yaml` (your name, language) and `_bmad/bmm/config.yaml` (project settings) — the agent can update these for you if you ask
