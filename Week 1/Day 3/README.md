# 🤖 The Definitive AI Coder Course — Day 3 Complete Notes
### *Hands-On with Cursor, Copilot, Codex & Antigravity — Building a Kanban App*

---

## Table of Contents

1. [Day 3 Overview — First Yellow (Tools) Day](#1-day-3-overview--first-yellow-tools-day)
2. [Key Principles for Today](#2-key-principles-for-today)
3. [Environment Setup — Installing Node.js](#3-environment-setup--installing-nodejs)
4. [Terminal Basics for Beginners](#4-terminal-basics-for-beginners)
5. [Setting Up the Kanban Project](#5-setting-up-the-kanban-project)
6. [Deep Dive into agents.md — The Kanban Version](#6-deep-dive-into-agentsmd--the-kanban-version)
7. [Cursor — YOLO Mode Build](#7-cursor--yolo-mode-build)
8. [GitHub Copilot in VS Code — Full Walkthrough](#8-github-copilot-in-vs-code--full-walkthrough)
9. [OpenAI Codex — VS Code Extension Build](#9-openai-codex--vs-code-extension-build)
10. [Antigravity (Google) — Gemini-Powered Build](#10-antigravity-google--gemini-powered-build)
11. [Final Verdict — Cursor vs Copilot vs Codex vs Antigravity](#11-final-verdict--cursor-vs-copilot-vs-codex-vs-antigravity)
12. [Critical Lessons from Day 3](#12-critical-lessons-from-day-3)
13. [Day 3 Wrap-Up & What's Next](#13-day-3-wrap-up--whats-next)

---

## 1. Day 3 Overview — First Yellow (Tools) Day

Day 3 is the **first "yellow day"** in the course — yellow days are about tools, products, and hands-on building. After two days of setup and theory, this is where things get practical.

### What Happens Today

- A side-by-side comparison of **four major agentic coding IDEs**:
  - **Cursor** (the one used on Day 1)
  - **GitHub Copilot** in VS Code
  - **OpenAI Codex** as a VS Code extension
  - **Antigravity** (Google's AI-powered IDE)

- All four tools build the **exact same project**: a Kanban board application
- This makes for a fair, direct, apples-to-apples comparison

### The Project: A Kanban Board

A **Kanban board** is a project management tool (similar to Trello or Jira) where:
- Tasks are represented as **cards**
- Cards live in **columns** that represent stages of work (e.g., Backlog → In Progress → Done)
- You can **drag and drop** cards between columns

Building the same app across all four tools lets you clearly see the differences in quality, workflow, and output.

---

## 2. Key Principles for Today

Before diving in, the instructor sets expectations with three guiding principles:

### Principle 1 — Everything Is Optional

You do **not** need to use all four tools. Options include:
- Watch and observe the differences without installing everything
- Pick the one that suits you and follow along with only that
- Use whichever tool you prefer (Cursor, Copilot, Claude Code, etc.) throughout the course

> *"You don't need to do them all. And that can be the one that you stick with."*

### Principle 2 — Your Results Will Vary

- Different plans give access to different models
- Free plans use lower-tier models; paid plans use stronger models
- Model differences directly affect output quality
- This is expected — embrace it as part of the experience

### Principle 3 — Don't Get Frustrated. Simplify.

If things don't work:
1. **Be patient** — resist the urge to panic
2. **Give feedback** — tell the agent what's wrong
3. **Simplify** — reduce the scope, get *something* working, then build up
4. **Delete and restart** — it's perfectly fine to wipe and start fresh
5. **Skip and move on** — if one tool doesn't cooperate, move to the next

> **The golden debugging mantra for today:** *Simplify, simplify, simplify.*

---

## 3. Environment Setup — Installing Node.js

### What is Node.js and Why Do We Need It?

**Node.js** is a JavaScript runtime that lets you run JavaScript code on your computer (outside of a browser). It's required for running modern JavaScript/TypeScript web apps — including the Next.js framework that the Kanban app will use.

### How to Check if You Already Have It

Open a terminal in Cursor (View menu → Terminal) and type:

```bash
node --version
```

If you get back a version number like `v22.x.x`, you're good. **Anything v22 or above is great.**

---

### How to Install Node.js

Go to **nodejs.org** and click **Download**.

#### On Mac (using terminal commands)
The download page provides terminal commands specific to your Mac. Copy and paste them into your terminal.

#### On Windows
Two options:
1. **Using Chocolatey** (if you have it): use the provided Chocolatey install command
2. **Standard Windows Installer**: scroll to the Windows section, choose the x64 version, and run the installer like any normal Windows app

#### Opening the Terminal in Cursor

If you need to run terminal commands while inside Cursor:

```
View Menu → Terminal
```

A terminal panel opens at the bottom of the screen. This is where you run all command-line instructions.

> If you have problems, check the course resources or send a message to the instructor.

---

## 4. Terminal Basics for Beginners

For those new to the terminal, here are the essential commands used throughout today:

### Essential Commands

| Command | What It Does | Example |
|---|---|---|
| `pwd` | Print Working Directory — shows you where you are | `pwd` → `/Users/ed/projects` |
| `cd [folder]` | Change Directory — move into a folder | `cd projects` |
| `cd ..` | Go up one directory level (to the parent folder) | `cd ..` |
| `git clone [url]` | Download a GitHub repository to your computer | `git clone https://github.com/...` |
| `mv [old] [new]` | Move / Rename a file or folder | `mv kanban cursor_kanban` |
| `npm run dev` | Start the development server for a Node.js app | `npm run dev` |
| `node --version` | Check which version of Node.js is installed | `node --version` |

### The Reset Pattern (Used Multiple Times Today)

Because we're building the same project 4 times with different tools, there's a repeated pattern for resetting between each tool:

```bash
# Step 1: Go to the projects directory
cd ..          # (go up to projects if you're inside a project folder)

# Step 2: Rename the current kanban folder (to save it, not delete it)
mv kanban cursor_kanban     # renames "kanban" to "cursor_kanban"

# Step 3: Clone a fresh copy of the kanban starter project
git clone https://github.com/ed-donner/kanban.git

# Now you have a fresh "kanban" folder with just the agents.md file
```

This preserves each tool's output under a new name while giving you a clean slate for the next one.

---

## 5. Setting Up the Kanban Project

### Getting the Starter Repository

The course provides a GitHub repository that contains just one file — the pre-written `agents.md`. This is all the agent needs to get started.

```bash
# Clone the starter repo
git clone https://github.com/ed-donner/kanban.git

# Open it in Cursor
# File → New Window → Open Project → navigate to "kanban" folder
```

Once open in Cursor, you'll see:
- **Left pane:** File explorer showing the project — just one file: `agents.md`
- **Middle pane:** Code editor
- **Right pane:** Agent chat panel

---

## 6. Deep Dive into agents.md — The Kanban Version

The instructor **hand-wrote** (not generated) the `agents.md` for this project. Let's walk through each section carefully.

### Viewing the File

In Cursor, you can:
- **Click** the file to see the raw markdown source
- **Right-click → Open Preview** to see it rendered (formatted) — this is essentially how the agent "sees" it

---

### Section 1 — Business Requirements

```markdown
# Business Requirements — Kanban Project

- MVP (Minimum Viable Product): A Kanban-style project management web app
- One board only — keep it simple
- Fixed five columns that can be renamed
- Each card: title and details only
- Drag and drop interface to move cards between columns
- Add a card
- Delete an existing card
- NO archive, NO search and filter — keep it simple
- Priority: slick, professional, gorgeous UI with very simple features
- Should open with dummy data
```

**Why write it this way?**
- **Precise and unambiguous** — no room for interpretation
- **Focused on positives** — tells the agent what to build, not what to avoid
- **Simple scope** — starts with the minimum; complexity comes later
- **UI priority stated explicitly** — tells the agent aesthetics matter

---

### Section 2 — Technical Details

```markdown
## Technical Details

- Next.js app
- In a subdirectory called "frontend"
- No persistence (no database)
- No user login
- Use popular libraries, as simple as possible, but with an elegant UI
```

**Key decisions explained:**
- **Next.js:** A popular React-based framework for building web applications
- **Subdirectory structure:** Keeps the project organised
- **No persistence:** Simplifies the MVP — data lives in memory only
- **No login:** Removes complexity that isn't needed for a prototype

---

### Section 3 — Color Scheme

```markdown
## Color Scheme

[Instructor's preferred hex codes for colors]
```

This is optional. You can:
- Use the instructor's colors (copy from the repo)
- Use your own hex codes
- Remove this section entirely and let the agent choose its own colors

---

### Section 4 — Strategy

```markdown
## Strategy

- Write a plan with success criteria for each phase to be checked off
- Include project scaffolding
- Rigorous unit testing
- Execute the plan
- Carry out extensive integration testing with Playwright or similar, fixing defects
- Only complete when the MVP is finished and tested, with the server running and ready for the user
```

**What this does:**
- Forces the agent to **plan before building**
- Demands **success criteria** for each phase
- Requires **automated testing** (unit tests + integration tests using Playwright)
- Sets a clear **definition of done**: server running, MVP complete, tested

> **Note:** In 2026, modern agents increasingly follow this kind of strategy by default. You may not need to spell it out as explicitly anymore — but there's no harm in including it.

---

### Section 5 — Coding Standards

```markdown
## Coding Standards

- Use latest versions of libraries; idiomatic approaches as of today
- Keep it simple — never over-engineer
- Always simplify; no unnecessary defensive programming
- No extra features; focus on simplicity
- Be concise; keep READMEs minimal
- IMPORTANT: No emojis ever
```

**Why each rule matters:**

| Rule | Reason |
|---|---|
| **Latest library versions** | LLMs can default to older patterns; this keeps it current |
| **Keep it simple / Never over-engineer** | LLMs love complexity — this fights that tendency |
| **No unnecessary defensive programming** | Avoids excessive try/catch blocks everywhere |
| **Concise READMEs** | LLMs generate bloated READMEs by default — this prevents it |
| **IMPORTANT: No emojis** | LLMs love emojis; they can also cause rendering issues on Windows |

---

### agents.md Best Practices Summarised

Based on the walkthrough, here are the principles applied when writing this file:

```
1. BE PRECISE — No ambiguity. Say exactly what you want.
2. BE CONCISE — Every word costs context window space.
3. FOCUS ON POSITIVES — What should it do (not just what it shouldn't)
4. REPEAT THE IMPORTANT STUFF — Repetition for critical requirements is fine.
5. USE "IMPORTANT" IN CAPS — Empirically gets better adherence
6. MAKE IT A LIVING DOCUMENT — Iterate and refine it as you go
7. START SIMPLE — You can always add more requirements later
```

> You can use the instructor's `agents.md` as a starting point template and update the requirements section for whatever you're building.

---

## 7. Cursor — YOLO Mode Build

### Setup

#### Cursor Shortcut Keys
Before starting, these keyboard shortcuts help you navigate:

| Action | Mac | Windows/PC |
|---|---|---|
| Toggle left sidebar (file explorer) | `Cmd + B` | `Ctrl + B` |
| Toggle right sidebar (agent chat) | `Cmd + Option + B` | `Ctrl + Option + B` |

#### Checking Context Usage
In the agent panel, a **circular indicator** shows how much of the context window has been used so far. Watch this as the build progresses — it's a live readout of context consumption.

---

### Configuring YOLO Mode in Cursor

Go to: **Settings → Agents → Auto Run section**

Three permission options:

| Mode | Description | Best For |
|---|---|---|
| **Ask every time** | Agent pauses and asks permission before every action | Beginners learning what's happening |
| **Auto run (sandboxed)** | Agent runs in a safe environment; some restrictions apply | Middle ground |
| **Run everything unsandboxed (YOLO)** | Agent does whatever it wants, no questions asked | Experienced users comfortable with the risks |

> **Instructor's choice:** YOLO mode (`run everything unsandboxed`). He knows what's happening and accepts the risk for a low-stakes project like this.
>
> **Recommendation for newcomers:** Start with "Ask every time" to watch what the agent does at each step. Move to YOLO when you're comfortable.

---

### The Build Process

#### Step 1 — Set to Plan Mode
In the agent drop-down selector (top of the right panel), select **Plan** mode.

Then send a simple prompt:
> *"Go ahead and plan."*

The agent already knows what to build because it automatically loads `agents.md` into its context.

**What you'll see:**
- Agent reads `agents.md` — confirmed in the "active rules" display
- Context usage ticks up (e.g., 6.4% used)
- A full implementation plan document is generated — multiple phases, architecture overview, success criteria, scope definition, execution order

#### Step 2 — Switch to Build Mode
Press the **Build** button (or equivalent "start implementation" option).

> The instructor doesn't read the plan — he just trusts it and presses Go. For a real project, you'd review and give feedback before proceeding.

**What you'll see happening in real time:**
- Files being created one by one (`.gitignore`, `frontend/` directory, component files, etc.)
- Context usage percentage climbing (went from 10.7% → 28.8% during the build)
- Tests running — some failing — agent detecting the failure and self-correcting
- This is **the agent definition in action**: LLM running tools (file creation, code execution) in a loop to achieve a goal

#### Step 3 — View the Result

The agent may:
- **Automatically launch** the server and open the browser (happened for the instructor)
- **Give you instructions** to launch it yourself: `cd frontend && npm run dev`

Then visit: `http://localhost:3000`

---

### The Result

The Cursor agent produced a working Kanban board:
- **Columns:** Backlog, To Do, In Progress, Review, Done
- **Drag and drop:** Working (with drag handles visible)
- **Add card:** Working
- **Delete card:** Working
- **Rename columns:** Working
- **Visual style:** Clean layout with basic styling

**What wasn't perfect:**
- A Next.js error symbol appeared at the bottom of the screen
- Drag and drop was "a bit janky"
- Cards couldn't be reordered within a column

---

### Iteration — Giving Feedback

After the initial build, this feedback prompt was sent:

> *"It's mostly working nicely. But Next.js is showing one error (red symbol at the bottom). Also the drag and drop is a bit janky and it's not possible to reorder within a column. Can this be made more slick? Also it would be nice to have more yellow and purple on the screen."*

**What improved after iteration:**
- ✅ Colors updated with more purple and yellow
- ✅ Cards can now be reordered within a column
- ✅ Drag and drop feels smoother
- ❌ The original Next.js error remained (the agent briefly fixed it but seemed to reintroduce it)

**Overall verdict for Cursor:** Good. Not perfect, but demonstrated the complete workflow of plan → build → test → iterate effectively.

---

## 8. GitHub Copilot in VS Code — Full Walkthrough

### About GitHub Copilot

- One of the **most widely used** AI coding assistants in the world
- Available as an extension inside **VS Code** (the open-source code editor that Cursor itself is based on)
- Has a **free tier** with a monthly request allowance — no credit card needed to start
- Also available via CLI and web, but IDE extension is the most popular usage mode

---

### Installing VS Code

Go to **code.visualstudio.com** and download for your platform.

If you already have it: check for updates to ensure you have the latest version.

VS Code looks very similar to Cursor — because Cursor is literally a fork (a modified version) of VS Code. The familiarity is intentional.

---

### Installing GitHub Copilot Extension

1. Open VS Code
2. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (PC) — or go to **View → Extensions**
3. In the search box, type: `GitHub Copilot`
4. Find the one from **GitHub.com** (verified tick) — currently has 69M+ downloads
5. Press the blue **Install** button
6. Restart VS Code if prompted

---

### Signing Into GitHub

In the **bottom-left corner** of VS Code, click the account/avatar icon. Sign in to your GitHub account. GitHub Copilot uses your GitHub account for authentication and usage tracking.

---

### Opening the Copilot Agent Panel

Press `Cmd+Shift+I` (Mac) or `Ctrl+Shift+I` (PC) — or go to **View → Chat**

A sidebar appears on the right labeled **"Build with Agent"**. This is very similar to Cursor's agent panel.

**Key elements of the panel:**
- **Message input:** Where you send prompts
- **Plan mode dropdown:** Switch between planning and execution mode
- **Model selector:** Choose which AI model powers the agent — includes free models on the lower tier
- **Usage bar:** Hover over it to see your monthly request usage vs. your plan's allowance

---

### Setting Up the Project

```bash
# Reset: rename the Cursor build, clone fresh copy
mv kanban cursor_kanban
git clone https://github.com/ed-donner/kanban.git

# In VS Code: File → New Window → Open → navigate to "kanban" folder
```

---

### The Build Process

#### Step 1 — Plan Mode

Put the agent in **Plan mode** and send:
> *"Please plan the task at hand."*

The agent picks up `agents.md` automatically and generates a comprehensive plan.

#### Step 2 — Start Implementation

Press **"Start Implementation"** button. The agent will begin running.

**Permission prompts:** Unlike Cursor in YOLO mode, GitHub Copilot asks for permission before certain actions. Options:
- Allow this once
- **Always allow** — puts it into a session-level YOLO mode
- Approve step by step — safer for beginners

**What happened during the build:**
- A lot of file creation and coding
- Agent started the server in the wrong directory — caught the error, fixed it
- Started the server again in the correct directory
- Then appeared to "hang" — got stuck waiting without realising the server was already up

#### Step 3 — Dealing with the Hang

The agent got stuck in a loop waiting for a server response that never came back to it. Solution:
- **Cancel / interrupt** the agent
- Manually run `npm run dev` from the `frontend` directory

```bash
cd frontend
npm run dev
```

Then visit: `http://localhost:3000`

---

### The Result

Despite the awkward finish, the output was **surprisingly impressive**:
- Clean layout with a nice column design
- Drag and drop worked smoothly
- Column renaming worked
- **No error symbols** — cleaner than Cursor's output
- **Bug found:** Delete card functionality was broken

> The model used was **Claude Haiku 4.5** — a small, fast, lower-cost model. Despite being smaller, it produced a clean result.

---

### The Critical Debug Lesson

When the delete button didn't work, the agent was asked to fix it. The agent immediately:
1. Guessed what the problem might be
2. Applied a fix
3. Claimed "it's fixed"

**Without testing. Without proving the root cause.**

The instructor tested it — still broken.

This is a **classic bad behaviour pattern** from coding agents:
> "Guess → Fix → Claim victory" — without proving anything

#### The Correct Debugging Instruction

When asking an agent to fix a bug, always use this formula:

```
"Please:
1. Reproduce the problem — prove you've reproduced it
2. Find the root cause
3. Fix it
4. Prove you've fixed it — demonstrate the fix works"
```

**Result after this structured instruction:** The agent actually reproduced the problem, found the real root cause, fixed it, and verified it worked. Delete was now functional. ✅

> **Key insight:** You must be the boss of the debugging process. Push back and demand rigour, especially from smaller models. Accepting "I've fixed it" without proof is dangerous.

---

## 9. OpenAI Codex — VS Code Extension Build

### What is Codex?

OpenAI's **Codex** is primarily a **CLI tool** (similar to Claude Code — covered in Week 2), but it also exists as a **VS Code extension**. Since Day 3 is IDE-focused, the extension version is used here.

> Codex CLI will be covered in depth in Week 2.

---

### Installing the Codex Extension

1. Open VS Code
2. `Cmd+Shift+X` / `Ctrl+Shift+X` → Extensions marketplace
3. Search for: `Codex`
4. Find the official **OpenAI Coding Assistant** from OpenAI (tick verified)
5. Press **Install**
6. Restart VS Code

The Codex icon appears in the **left sidebar** (unlike Cursor/Copilot which use the right side).

---

### Authentication

Codex requires an **OpenAI/ChatGPT account** with an active subscription. It is **not available on a free tier** (as of the time of recording — verify current status).

Go to the settings icon within the Codex panel and log in with your OpenAI account.

---

### Codex Panel Controls

| Control | What It Does |
|---|---|
| **Agent Full Access** | YOLO mode — agent can do whatever it wants |
| **Model selector** | Choose the GPT model to use |
| **Reasoning effort** | Controls how deeply the model "thinks" before responding |

#### About Reasoning Effort

The **reasoning effort** slider controls how much the model invests in step-by-step thinking (Trick 2 from Day 2):

| Setting | Effect |
|---|---|
| Low | Faster, lighter thinking — good for simple tasks |
| Medium | Balanced |
| High | Deep reasoning — better quality but slower; can sometimes **overthink** |

> Important nuance: High reasoning is not always better. Sometimes models "agonize" over decisions in a way that's counterproductive — overthinking simple problems. **Medium-High is often the sweet spot.** The instructor chose High for this build.

**Note:** Codex does **not have a built-in plan mode** in the IDE extension. However, the `agents.md` file already instructs it to plan first, so this is handled through the context.

---

### The Build Process

#### Reset and Setup

```bash
mv kanban copilot_kanban     # rename previous build
git clone https://github.com/ed-donner/kanban.git  # fresh clone
```

Open the fresh `kanban` folder in VS Code, then switch to the Codex panel.

#### Running the Build

Send the simple prompt:
> *"Please go ahead."*

The agent:
- Identifies `agents.md` to read
- Reads it into context
- Begins planning and executing autonomously

**Build stats:**
- Ran for approximately **15 minutes**
- Created **74 different files**
- Context window usage: 16% (42,258 tokens used)
- Dev server launched and running automatically
- Agent provided a summary of all changes made

---

### The Result

This was described as the **best result of the day**:

```
"Kanban Studio — One board, five columns, zero clutter"
```

- Beautiful, polished UI design
- Drag and drop: fully working
- Card reordering within columns: working
- Card deletion: working
- Column renaming: working — live updates visible in real time
- **Zero errors**
- Professional aesthetic out of the box

> *"I'm blown away by that. This is really awesome."*

**Why did Codex do so well?**
The key factor: **the model**. Codex was running **GPT 5.2 Codex on High reasoning** — the strongest available model at the time. Strong model = strong results. The other tools were using smaller/cheaper models.

---

### The "I Don't Know React" Confession

The instructor made an important admission during the Codex demo:

> *"The secret is I don't know how to write this kind of front-end code either. I'm a lousy React developer... but this is doable. Even if you don't know how to write front-end code, you can act like the manager. You can give feedback."*

This is a profound point for beginners:

- You do **not** need to understand every line of code the agent generates
- You act as the **product manager and reviewer** — describe what you want, evaluate what you get, give feedback
- The agent handles the implementation details
- You bring the **judgment, requirements, and quality standards**; the agent brings the code

> As projects grow in complexity and scale, deeper technical understanding becomes increasingly important. But for MVPs and prototypes, this is genuinely viable.

---

## 10. Antigravity (Google) — Gemini-Powered Build

### What is Antigravity?

**Antigravity** is Google's AI-powered IDE. Key facts:
- Website: **antigravity.google**
- Tagline: *"Experience liftoff with the next generation IDE"*
- Like Cursor and VS Code, it is **also a VS Code fork** — so the interface will look familiar
- Powered by **Google's Gemini** models
- Supports a **1 million token context window** (largest of any major model family)
- Interestingly, also offers **Anthropic models** and **open-source GPT** as options within the IDE

---

### Installing Antigravity

1. Go to **antigravity.google**
2. Download for your platform (Mac, Windows, Linux)
3. On Mac: drag the icon to Applications
4. On Windows: run the installer wizard
5. **During setup:** stick with all defaults, pick your preferred color scheme
6. Sign in with your **Google account** (required)

---

### The Interface

When you open Antigravity, it looks almost identical to VS Code and Cursor. That's because it is, fundamentally, the same editor. The agent panel is on the **right side**.

---

### Configuring Antigravity Settings

Click the **Settings icon** at the bottom of the screen:

| Setting | Options | Recommended |
|---|---|---|
| **Agent autofix lints** | On / Off | **On** — automatically fixes code quality errors |
| **Permissions / YOLO control** | Request reviews / Agent decides / Always proceed | Start with "Request reviews"; switch to "Always proceed" when comfortable |

The **"Agent decides"** option is a nice middle ground — the agent chooses when to ask for permission based on the risk of the action.

---

### Unique Feature: `.agent/rules/` Directory

This is where Antigravity differs from the other tools. Instead of using `agents.md` in the project root, **Antigravity uses a special hidden folder structure**:

```
project-root/
└── .agent/
    └── rules/
        └── strategy.md    ← your instructions go here
```

#### How to Set It Up

1. **Copy the contents** of `agents.md` (select all, copy)
2. **Delete** `agents.md` from the project root (to avoid confusion)
3. **Right-click** anywhere in the file explorer → **New Folder**
4. Name it: `.agent`
5. Inside `.agent`, create another folder: `rules`
6. Inside `rules`, create a new file: `strategy.md` (or any name you like)
7. **Paste** the copied content into `strategy.md`
8. At the top of the file, set the **activation mode** to `always on`

#### Activation Mode Options

| Mode | Meaning |
|---|---|
| **Always on** | This file is always included in the agent's context |
| **Manual** | Only loaded when you explicitly tell the agent to load it |
| **Model decision** | The model decides whether to include it |

> Always use **"always on"** for your main strategy/rules file.

---

### The Build Process

#### Setup

```bash
mv kanban codex_kanban     # rename Codex build
git clone https://github.com/ed-donner/kanban.git  # fresh clone
```

Set up the `.agent/rules/strategy.md` file as described above.

Put the agent in **Planning mode** and send:
> *"Please go ahead."*

**Model used:** Gemini 3 Pro (High) — Google's strongest model

---

### What Made This Build Special

Antigravity did something none of the others did: it **tested the app visually while building it**:

1. **Launched a browser** during the build to check screens looked correct
2. **Ran Playwright** (browser automation testing) — drove a real browser through a series of automated tests
3. **Detected failing tests**, fixed them, and re-ran until they passed
4. **Generated a screen recording** of the running app as evidence of completion

> The completion summary included an animated GIF/recording showing the Kanban board in action — Antigravity actually captured a visual of its own work.

---

### The Result

Clean, fresh, professional-looking Kanban board:
- Drag and drop: working ✅
- Card reordering: working ✅
- Column renaming: working ✅
- Delete: working ✅
- Add card: **partially working** — used a basic JavaScript browser pop-up instead of a proper modal form (felt simplistic)

---

### Iteration — Improving the "Add Card" Experience

Feedback prompt:
> *"It looks good, but creating a new card isn't great. There's a simplistic JavaScript pop-up for the name and no way to add a description. This does not look professional. Can it be improved?"*

The agent's response was telling — it mentioned it had actually been "wrestling with a better UI for card creation" during the build, showing it had already considered the problem.

**After iteration:**
- A proper **modal dialog** appeared when clicking "Add Card"
- The modal had fields for title and description
- Clean, professional design

> *"I like this. This is better."*

**Final verdict for Antigravity:** Strong performance, competitive with Codex, especially with the self-testing behaviour.

---

## 11. Final Verdict — Cursor vs Copilot vs Codex vs Antigravity

### Summary Table

| Tool | Model Used | Output Quality | Unique Feature | Weakness |
|---|---|---|---|---|
| **Cursor** | Auto (likely Cursor Composer — internal model) | Good | Fast iteration, familiar interface, strong YOLO mode | Minor drag-and-drop issues, one persistent error |
| **GitHub Copilot** | Claude Haiku 4.5 (small model) | Good for the model size | Free tier available, massive adoption | Agent "hung" at end, delete bug needed extra prompting |
| **OpenAI Codex** | GPT 5.2 Codex (High reasoning) | Excellent — best visual result | Strongest model = best output quality, 74 files created | Requires paid OpenAI subscription |
| **Antigravity** | Gemini 3 Pro (High) | Excellent — best automated testing | Self-launches browser tests, generates screen recordings, Playwright integration | Slightly less polished "Add Card" UX initially |

---

### The Instructor's Ranking

1. 🥇 **Codex** — Best visual result, most impressive out-of-the-box quality
2. 🥈 **Antigravity** — Very close second, especially impressive for its self-testing behaviour
3. 🥉 **Cursor** — Solid, familiar, great workflow
4. 4️⃣ **GitHub Copilot** — Respectable, especially given the small model used

**Important caveat from the instructor:**

> *"The reason Codex did so well is because we are using the absolute frontier model — GPT 5.2 Codex on High reasoning. Cursor was using its internal Composer model, and Copilot was on Claude Haiku. Strong model = strong results."*

The ranking reflects **model choice as much as tool quality.** If Cursor had been set to GPT 5.2 Codex, it might have produced equally impressive results.

---

### The Real Takeaway: They're All Quite Similar

> *"The overall takeaway is that they all look quite similar when you use IDE-based agents. They often have a sidebar (left or right) that you can make larger. They often come with plan mode and execute mode. They're mostly driven by agents.md. You get very familiar with this and which one you pick depends on which plan you've paid for, which one you like, or what the rest of your team are using."*

All four tools share the same fundamental structure:
- **Agent chat panel** (sidebar, left or right)
- **Plan mode + Execution mode**
- **`agents.md` or equivalent** for persistent instructions
- **Context window display** showing usage
- **YOLO mode option** for hands-free operation

The differentiators are:
- **Model quality** (the biggest factor in output quality)
- **Ecosystem/integration** (GitHub for Copilot, Google for Antigravity, OpenAI for Codex)
- **Price and plan structure**
- **Team conventions** (what your colleagues use)

---

## 12. Critical Lessons from Day 3

### Lesson 1 — Model Quality Is the Biggest Variable

The quality difference between the Cursor (small model) and Codex (GPT 5.2 Codex) outputs was substantial. Before worrying about which IDE to use, **understand which model you're actually running on** and whether you're getting the best available option for your plan.

---

### Lesson 2 — The agents.md Is Your Most Important Input

All four tools produced dramatically different results depending on how well-specified the `agents.md` was. A vague brief produces vague results. **Your instructions are your biggest lever for quality control.**

Key qualities of a good `agents.md`:
- Precise requirements
- Clear success criteria
- Explicit coding standards
- Positive framing (what to do, not just what not to do)

---

### Lesson 3 — The Debugging Discipline

Never accept "I've fixed it" from an agent without proof. The correct debugging cycle is:

```
1. Reproduce the problem — demonstrate you can trigger the bug
2. Find the root cause — not a guess, a diagnosis
3. Fix it
4. Prove it's fixed — test and demonstrate the fix works
```

This protocol should become second nature when working with coding agents. It applies regardless of which tool or model you're using.

---

### Lesson 4 — Simplify When Stuck

If the agent starts producing garbage, the instinct is to give more detailed instructions. Often the better move is to **reduce scope** — ask for something smaller, get it working, then build up incrementally.

---

### Lesson 5 — You Don't Need to Know Every Technology

Particularly for front-end work, you can function effectively as the **manager/reviewer** even without deep knowledge of the specific framework. You need to:
- Know enough to evaluate the output
- Know how to run the app (`npm run dev`)
- Know how to give clear feedback
- Know when something doesn't look or feel right

Deeper technical mastery matters more as projects grow in complexity — but for MVPs, this level of oversight is genuinely viable.

---

### Lesson 6 — Iterating is Normal, Not a Sign of Failure

Not one of the four tools produced a perfect result on the first pass. Every build needed at least one round of feedback and iteration. This is normal. The agent is a collaborator, not a magic oracle.

**Embrace the loop:**
> Build → Evaluate → Give specific feedback → Rebuild → Evaluate again

---

## 13. Day 3 Wrap-Up & What's Next

### What You Accomplished Today

✅ Installed and configured Node.js  
✅ Learned essential terminal commands  
✅ Wrote and understood a real `agents.md` file  
✅ Built a Kanban board with **Cursor** in YOLO mode  
✅ Built the same Kanban board with **GitHub Copilot** in VS Code  
✅ Built it again with **OpenAI Codex** as a VS Code extension  
✅ Built it a fourth time with **Antigravity** (Google/Gemini)  
✅ Compared all four tools side by side  
✅ Learned the correct debugging discipline  
✅ Understood that model quality is the #1 factor in output quality  

**You are now 20% through the course! 🎉**

---

### Key Mindset Shifts from Today

```
Before Day 3: "I need to pick the perfect tool"
After Day 3:  "The tools are very similar; the model and my instructions matter more"

Before Day 3: "The agent fixed it → it must be fixed"
After Day 3:  "Reproduce → Root cause → Fix → Prove it → Only then trust it"

Before Day 3: "I need to know the technology to build with it"
After Day 3:  "I can direct and review; the agent implements"
```

---

### Coming Up — Day 4 (The YOLO Project)

Day 4 is a **green day** — a commercial project day. You'll be going into full YOLO mode on a real, business-relevant project.

> *"I hope you feel brave as we go into YOLO mode. It's going to be so much fun starting with YOLO tomorrow."*

The first two days gave you the theory. Day 3 gave you the tools. Day 4 puts it all together on something that matters commercially.

---

*📝 Notes compiled from Day 3 lectures of the AI Coder Course — covering all 7 segments: Introduction & Setup, agents.md Deep Dive, Cursor YOLO Build, GitHub Copilot Build, OpenAI Codex Build, Antigravity Build, and the Final Verdict comparison.*
