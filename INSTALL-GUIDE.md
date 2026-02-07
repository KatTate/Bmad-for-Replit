# BMad Method — Replit Installation Guide

**Version:** 6.0.0-Beta.7

This guide covers two scenarios:

- **Scenario A** — Installing BMad into an existing Replit project (you already have code)
- **Scenario B** — Creating a brand-new Replit project using BMad (starting from scratch)

---

## What You'll Need

- A Replit account (free or paid)
- The BMad Method zip file downloaded to your computer
- A few minutes of your time

---

## Scenario A: Install BMad into an Existing Replit Project

Use this when you already have a Replit project with code in it and you want to add the BMad planning and development framework on top of it.

### Step 1: Open Your Existing Project

Open the Replit project where you want to install BMad.

### Step 2: Upload the Zip File

1. In the **Files** panel on the left side of Replit, click the three-dot menu (⋯) at the top
2. Select **Upload file**
3. Choose the BMad zip file from your computer
4. Wait for the upload to finish — you should see the zip file appear in your file list

### Step 3: Unzip the File

1. Open the **Shell** tab at the bottom of Replit (if you don't see it, click the "+" tab and choose "Shell")
2. Type the following command and press Enter:

```bash
unzip bmad-method*.zip
```

> **Note:** If your zip file has a different name, replace `bmad-method*.zip` with the actual filename. You can check by typing `ls *.zip` first.

3. You should now see these items in your file list:
   - `_bmad/` folder (the toolkit)
   - `install-bmad.sh` (the installer script)
   - `verify-bmad.sh` (optional verification script)

### Step 4: Run the Installer

In the Shell, type:

```bash
bash install-bmad.sh
```

The installer will:
- Detect that this is a **brownfield** project (meaning it has existing code)
- Create the `_bmad-output/` folders for generated documents
- Safely add the BMad configuration to your `replit.md` file **without overwriting** any of your existing content

You should see output like:

```
==========================================
 BMad Method 6.0.0-Beta.7 — Replit Installer
==========================================

[1/5] Found _bmad/ toolkit directory
[2/5] Created _bmad-output/ directories
[3/5] Detected BROWNFIELD project (X existing indicators found)
[4/5] Appending BMAD section to existing replit.md...
[5/5] Installation complete!
```

### Step 5: Verify the Installation (Optional)

Run the verification script to make sure everything is in place:

```bash
bash verify-bmad.sh
```

All checks should show **OK**. If any show **FAIL**, see the Troubleshooting section below.

### Step 6: Clean Up

Remove the zip file to keep your project tidy:

```bash
rm bmad-method*.zip
```

### Step 7: Start Using BMad

1. **Start a new chat** with the Replit Agent (this ensures the agent reads the updated `replit.md`)
2. Say: **"assess brownfield"** or just type **"AB"**
   - This will scan your existing project and figure out where you are in the development process
   - It recommends the best entry point into the BMad workflow based on what you already have

---

## Scenario B: Create a New Replit Project with BMad

Use this when you're starting a brand-new project from scratch and want to use BMad from the very beginning.

### Step 1: Create a New Replit

1. Go to [replit.com](https://replit.com) and click **Create Repl** (or **+** button)
2. Choose any template — a blank **Bash** or **HTML/CSS/JS** Repl works fine, but any language is OK
3. Give your project a name and click **Create Repl**

### Step 2: Upload the Zip File

1. In the **Files** panel on the left, click the three-dot menu (⋯)
2. Select **Upload file**
3. Choose the BMad zip file from your computer

### Step 3: Unzip the File

1. Open the **Shell** tab
2. Run:

```bash
unzip bmad-method*.zip
```

3. Confirm you see the `_bmad/` folder and `install-bmad.sh` in your file list

### Step 4: Run the Installer

```bash
bash install-bmad.sh
```

The installer will:
- Detect that this is a **greenfield** project (no existing code)
- Create the output directories
- Create a fresh `replit.md` with all the BMad configuration

You should see output like:

```
==========================================
 BMad Method 6.0.0-Beta.7 — Replit Installer
==========================================

[1/5] Found _bmad/ toolkit directory
[2/5] Created _bmad-output/ directories
[3/5] Detected GREENFIELD project (no existing project files found)
[4/5] Creating new replit.md...
[5/5] Installation complete!
```

### Step 5: Verify the Installation (Optional)

```bash
bash verify-bmad.sh
```

### Step 6: Clean Up

```bash
rm bmad-method*.zip
```

### Step 7: Start Using BMad

1. **Start a new chat** with the Replit Agent
2. Say one of the following to get going:
   - **"start BMad"** — The BMad Master will introduce you and help you get oriented
   - **"brainstorm"** or **"BP"** — Jump straight into brainstorming ideas
   - **"what should I do next?"** — Get guidance on the recommended next step

---

## Quick Command Reference

Once installed, you can use these commands in any Replit Agent chat:

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

## Troubleshooting

### "ERROR: _bmad/ directory not found"

The `_bmad/` folder needs to be in the project root (the top level). This usually means the zip file extracted into a subfolder. Check:

```bash
ls
```

If you see a folder like `bmad-method-main/` instead of `_bmad/` at the top level, move the contents up:

```bash
mv bmad-method-main/* .
mv bmad-method-main/.* . 2>/dev/null
rmdir bmad-method-main
```

Then run `bash install-bmad.sh` again.

### Agent doesn't respond to BMad commands

The Replit Agent reads `replit.md` at the start of each conversation. If BMad commands aren't working:

1. Check that `replit.md` exists and contains the BMad section (look for the "BMad Method" heading)
2. **Start a new chat** — the agent only reads `replit.md` when a conversation begins
3. Run `bash verify-bmad.sh` to confirm all files are in place

### Zip file won't upload

- Make sure the file is under Replit's upload size limit
- Try refreshing the Replit page and uploading again
- As an alternative, you can drag and drop the zip file directly onto the Files panel

### verify-bmad.sh shows warnings or unexpected results

- **FAIL about ".cursor directory":** This check is only relevant if you migrated from Cursor IDE. If you've never used Cursor, you can safely ignore this message
- **WARN about output directories:** Just run `bash install-bmad.sh` again — it will create them
- **WARN about help.md:** This is cosmetic and won't affect functionality
- **FAIL about missing files:** These indicate missing toolkit files — re-upload and unzip the BMad package

---

## Recommended Workflow

### For New Projects (Greenfield)

```
brainstorm → create brief → create PRD → create architecture → create epics → sprint planning → dev story
```

Or use the simplified path for small projects:

```
brainstorm → quick spec → quick dev
```

### For Existing Projects (Brownfield)

```
assess brownfield → (follow the recommended entry point) → continue through the workflow
```

### Anytime You're Unsure

Just say **"what should I do next?"** and BMad will analyze where you are and recommend the next step.

---

## Project Structure After Installation

```
your-project/
├── _bmad/                          # BMad toolkit (don't modify)
│   ├── core/                       # Core engine
│   ├── bmm/                        # Methodology module
│   ├── _config/                    # Configuration files
│   ├── _memory/                    # Agent memory
│   └── replit-routing.md           # Command routing table
├── _bmad-output/                   # Your generated documents appear here
│   ├── planning-artifacts/         # Briefs, PRDs, architecture docs
│   └── implementation-artifacts/   # Sprint plans, stories, reviews
├── install-bmad.sh                 # Installer (can delete after install)
├── verify-bmad.sh                  # Verification (can delete after install)
├── replit.md                       # Project config (agent reads this)
└── (your project files...)         # Your existing code stays untouched
```

---

## Tips

- **Always start a new chat** after installing BMad so the agent picks up the configuration
- **You can re-run the installer** safely at any time — it won't damage your existing content
- **The `_bmad/` folder** contains the toolkit itself — you generally don't need to edit anything in there
- **The `_bmad-output/` folder** is where all your planning documents and artifacts get saved
- **Configuration files** are in `_bmad/core/config.yaml` (your name, language) and `_bmad/bmm/config.yaml` (project settings)
