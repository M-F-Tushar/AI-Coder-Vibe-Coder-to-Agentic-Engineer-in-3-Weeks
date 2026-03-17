# Day 2 — Pro Week: Claude Code Commands, Shortcuts, Sessions, Checkpoints, YOLO Mode & Ralph Loops

> **Overview:** Day 2 goes deeper into Claude Code — covering every important command, shortcut, and configuration option, then exploring the workflow management system (sessions, checkpoints, Git), and finally pushing into autonomous agentic coding with YOLO mode and Ralph Loops.

---

## Table of Contents

1. [The Coding Agent Landscape Recap](#1-the-coding-agent-landscape-recap)
2. [Claude Code Commands — Complete Reference](#2-claude-code-commands--complete-reference)
   - [How to Discover Commands](#how-to-discover-commands)
   - [Commands You Already Know](#commands-you-already-know)
   - [The Three "C" Commands — Context, Compact, Clear](#the-three-c-commands--context-compact-clear)
   - [Other Useful Commands](#other-useful-commands)
3. [Shortcut Keys in Claude Code](#3-shortcut-keys-in-claude-code)
4. [Configuration & Permissions](#4-configuration--permissions)
   - [The `.claude` Directory & Settings JSON](#the-claude-directory--settings-json)
   - [The `/permissions` Command](#the-permissions-command)
5. [The `@` Syntax — Referencing Files in Prompts](#5-the--syntax--referencing-files-in-prompts)
   - [Using `@` in Prompts](#using--in-prompts)
   - [Using `@` in Claude.md](#using--in-claudemd)
   - [The "Single Source of Truth" Trick](#the-single-source-of-truth-trick)
6. [Managing Your Workflow — Sessions, Checkpoints & Git](#6-managing-your-workflow--sessions-checkpoints--git)
   - [The Three Levels of State Management](#the-three-levels-of-state-management)
   - [Level 1 — Sessions (High-Level State)](#level-1--sessions-high-level-state)
   - [Level 2 — Checkpoints & Rewinding (Fine-Grained State)](#level-2--checkpoints--rewinding-fine-grained-state)
   - [Level 3 — Git (Code Snapshots)](#level-3--git-code-snapshots)
   - [How These Three Levels Fit Together](#how-these-three-levels-fit-together)
   - [The Instructor's Personal Workflow](#the-instructors-personal-workflow)
7. [Sessions in Practice — Naming & Resuming](#7-sessions-in-practice--naming--resuming)
   - [Naming a Session](#naming-a-session)
   - [Resuming a Named Session](#resuming-a-named-session)
8. [Checkpoints in Practice — Rewinding](#8-checkpoints-in-practice--rewinding)
   - [What is a Checkpoint?](#what-is-a-checkpoint)
   - [How to Rewind](#how-to-rewind)
   - [Rewind Options](#rewind-options)
   - [Limitations of Rewinding](#limitations-of-rewinding)
9. [YOLO Mode — Bypassing Permissions](#9-yolo-mode--bypassing-permissions)
   - [What is YOLO Mode?](#what-is-yolo-mode)
   - [YOLO Mode vs. Accept Edits Mode](#yolo-mode-vs-accept-edits-mode)
   - [How to Launch Claude Code in YOLO Mode](#how-to-launch-claude-code-in-yolo-mode)
   - [Risks & Warnings](#risks--warnings)
   - [YOLO Mode in Practice — UI Revamp Demo](#yolo-mode-in-practice--ui-revamp-demo)
   - [Best Practices for YOLO Mode](#best-practices-for-yolo-mode)
10. [Ralph Loops — Autonomous Agentic Coding on Autopilot](#10-ralph-loops--autonomous-agentic-coding-on-autopilot)
    - [What is a Ralph Loop?](#what-is-a-ralph-loop)
    - [The Origin of the Term](#the-origin-of-the-term)
    - [How Ralph Loops Work Technically](#how-ralph-loops-work-technically)
    - [Installing the Ralph Loop Plugin](#installing-the-ralph-loop-plugin)
    - [Running a Ralph Loop](#running-a-ralph-loop)
    - [Ralph Loop Demo — Results](#ralph-loop-demo--results)
    - [YOLO + Ralph Loop — The Ultimate Combination](#yolo--ralph-loop--the-ultimate-combination)
    - [When to Use Ralph Loops (and When Not To)](#when-to-use-ralph-loops-and-when-not-to)
11. [Key Takeaways — Day 2 Summary](#11-key-takeaways--day-2-summary)

---

## 1. The Coding Agent Landscape Recap

Before diving in, here is a quick map of where the tools covered in the course fit into the broader coding agent ecosystem:

### IDE-Based Tools
| Tool | Type | Notes |
|---|---|---|
| **Cursor** | IDE (full) | Full IDE experience, AI-first. |
| **Windsurf** | IDE (full) | Similar to Cursor; same underlying model. |
| **Anti-gravity** | IDE (full) | Gemini-based AI IDE. |
| **GitHub Copilot** | Plugin (VS Code) | AI assistant built into VS Code. |
| **Codex** | Plugin (VS Code) | OpenAI's agentic VS Code plugin. |

### CLI-Based Tools
| Tool | Provider | Notes |
|---|---|---|
| **Claude Code** | Anthropic | The original and most established. Covered in depth this week. |
| **Cursor CLI** | Cursor | Released in response to Claude Code's success. |
| **Codex CLI** | OpenAI | OpenAI's terminal equivalent. |
| **Gemini CLI** | Google | Terminal tool for Gemini models. |
| **OpenCode** | Open source | Covered on Day 1 — multi-model, free alternatives. |
| **AMP Code** | Independent | Covered on Day 1 — ad-funded free tier. |

> **Key point:** Claude Code started the CLI movement. Most other CLI tools came out because of Claude Code's success. The core concepts covered this week (checkpoints, YOLO mode, Ralph loops) apply in spirit to all CLI tools, even if the exact commands differ.

---

## 2. Claude Code Commands — Complete Reference

### How to Discover Commands

There are two easy ways to see all available commands:

**Method 1 — Browse with Down Arrow:**
Inside Claude Code, press `/` and then use the **down arrow key** to scroll through all commands with their descriptions. This is the quickest way to see everything available.

**Method 2 — Help Command:**
```
/help
```
Prints a summary of the most important commands plus a list of shortcut keys.

---

### Commands You Already Know

These were introduced on Day 1 and are worth reinforcing:

| Command | What it Does |
|---|---|
| `/init` | Scans the project and creates a `claude.md` file. Run once when starting on a new project. |
| `/model` | Shows the current active model and lets you switch to a different one. |
| `/status` | 3-page panel: current version, session ID, login method, active model, usage stats. |
| `/context` | Visual breakdown of context window usage — memory, messages, free space, buffer. |
| `/compact` | Manually triggers compaction — compresses conversation history into a summary. |

---

### The Three "C" Commands — Context, Compact, Clear

These three commands all relate to context management and are easy to confuse. Here is the distinction:

#### `/context` — View the Context Window
```
/context
```
Shows a visual bar chart of how much of the 200,000-token context window is currently used, broken into:
- **Memory** — Claude.md and other loaded files.
- **Messages** — Conversation history so far.
- **Free space** — Available tokens.
- **Buffer** — Reserved space for performing compaction.

Use this frequently. It is the equivalent of checking your fuel gauge. Never start a big task with a nearly-full context window.

---

#### `/compact` — Compress Context (Keep a Summary)
```
/compact
```
Triggers manual compaction — compresses the entire conversation history into a shorter summary, freeing up most of the context window while preserving key information.

Optional — you can add summarization instructions:
```
/compact keep the refactoring decisions and test results
```

**Best practice:** Run `/compact` yourself at the end of every major task — before starting the next. Do not let it auto-compact in the middle of an active task (e.g., while rewriting large amounts of code), as this can cause incoherence and off-the-rails behaviour.

**Important caveat:** After compaction, some details from the earlier conversation are lost. Claude may repeat mistakes it already made (e.g., incorrectly flagging a `.env` file as exposed in Git). The fix is to keep `claude.md` up to date with information you never want to lose.

---

#### `/clear` — Full Reset (Dangerous!)
```
/clear
```
This is a **destructive command**. It completely wipes the conversation history — equivalent to exiting Claude Code and launching it fresh. Claude.md is re-read, but everything in the current conversation is gone.

**When to use it:**
- When you want a completely clean slate with no accumulated context from prior conversations.
- When you prefer managing state via `claude.md` files rather than relying on accumulated conversation history.

**Alternative to `/clear`:** Press `Ctrl + C` twice to exit Claude Code, then type `claude` again to start fresh. The effect is the same.

> **Instructor's preference:** Keep `claude.md` meticulously up to date, then use `/clear` or restart to begin fresh. This gives a clean, human-readable understanding of where the project stands at all times.

---

### Other Useful Commands

| Command | What it Does |
|---|---|
| `/config` | Shows the configuration settings for the current session. Same as the second page of `/status`. |
| `/usage` | Shows token usage stats. Same as the third page of `/status`. |
| `/stats` | Displays a visual usage history — tokens per day, models used, over time. A fun dashboard to track your Claude Code usage. |
| `/permissions` | View, add, and remove what commands/actions Claude is allowed to run without asking for approval. |
| `/rename <name>` | Names the current session (see Sessions section below). |
| `/rewind` | Steps back through the conversation checkpoints (see Checkpoints section below). |
| `/plugin install <name>` | Installs a plugin into Claude Code (see Ralph Loops section). |

---

## 3. Shortcut Keys in Claude Code

These keyboard shortcuts work inside the Claude Code terminal interface:

| Shortcut | Action |
|---|---|
| `Ctrl + ` `` ` `` (backtick) | Open a new terminal in VS Code. |
| `Ctrl + Shift + ` `` ` `` | Open a *completely fresh* terminal (environment variables reset). |
| `Ctrl + C` twice | Exit Claude Code. |
| `Escape` | Exit from a slash-command picker or status screen. |
| `Shift + Tab` | Cycle through input modes: **Accept Edits On** → **Plan Mode On** → Normal. |
| `Ctrl + O` | Toggle **detailed transcript mode** — shows the full thinking trace of what Claude is doing at each step. Press again to turn off. |
| `Ctrl + E` | Expand all items in the detailed transcript. Press again to collapse. |
| `Ctrl + B` | Run Claude in **background mode** — Claude continues working while you type more commands. |

### Understanding `Shift + Tab` — The Three Modes

Pressing `Shift + Tab` cycles through these three modes:

| Mode | Behaviour |
|---|---|
| **Normal (default)** | Claude asks for approval before every file edit or command. |
| **Accept Edits On** | Claude automatically approves all file edits without asking. It still asks about running commands. This is NOT full YOLO mode. |
| **Plan Mode On** | Claude produces a plan and describes what it will do but does NOT act or make any changes. Use this to review intent before committing. |

> **Note on Plan Mode:** With more powerful models like Opus 4.5, Plan Mode is less commonly needed. The model is generally good at deciding on its own when to plan versus when to act. Plan Mode is more useful with weaker models that tend to jump straight into action without thinking.

### Understanding `Ctrl + O` — Detailed Transcript Mode

When you turn on detailed transcript mode, the terminal displays a full trace of everything Claude is doing internally:
- Every tool it is calling.
- Every file it is reading or writing.
- Its internal reasoning steps as it works.

This is extremely useful for:
- Debugging unexpected behaviour.
- Understanding what sub-agents are doing.
- Learning how Claude Code approaches complex problems.

---

## 4. Configuration & Permissions

### The `.claude` Directory & Settings JSON

As you use Claude Code, it creates a hidden `.claude` folder in your project root. Inside this folder is a **settings JSON file** that stores all the permissions you have granted.

Every time you press **`2`** in response to Claude asking *"Can I run this command?"* — it records that permission in this JSON file. Future sessions remember what you have allowed.

**Example — what the JSON file looks like:**
```json
{
  "allowedTools": [
    "docker build",
    "npm run test",
    "python -m pytest"
  ]
}
```

**Managing permissions directly:**
You can open this file in VS Code and:
- **Add** a permission manually by adding a line (instead of waiting for Claude to ask and pressing `2`).
- **Remove** a permission by deleting its line.

This gives you precise, human-readable control over what Claude is and isn't allowed to do autonomously.

---

### The `/permissions` Command

As an alternative to editing the JSON file directly:

```
/permissions
```

This opens an interactive panel inside Claude Code to:
- View all currently allowed actions.
- Add a new rule.
- Remove an existing rule.

Both methods (editing the JSON or using `/permissions`) achieve the same result.

---

## 5. The `@` Syntax — Referencing Files in Prompts

The `@` symbol is a powerful feature in Claude Code for bringing file contents directly into the context window.

### Using `@` in Prompts

You can use `@` followed by a file path directly in your chat prompt:

```
Please review @docs/plan.md and implement step 3.
```

This inserts the full contents of `docs/plan.md` into the prompt, making Claude read it as part of the current instruction.

**For directories:**
```
@src/
```
When you `@` a directory, Claude receives a *listing* of the files in that directory — not the full contents of every file. This is much lighter on context.

> **Use `@` with care.** Including large files via `@` can fill up your context window very quickly. Only use it for files that are truly necessary for the current task.

---

### Using `@` in Claude.md

The `@` syntax works inside `claude.md` as well, not just in prompts. This allows you to keep your memory file lean while dynamically pulling in other documents:

```markdown
# Project Plan

@docs/plan.md
```

This tells Claude: *whenever you read `claude.md`, also load the contents of `docs/plan.md`*. This keeps `claude.md` short while ensuring Claude always has the detailed plan in context.

---

### The "Single Source of Truth" Trick

A very useful trick for people who switch between different AI tools (e.g., both Claude Code and GitHub Copilot on the same project):

Both tools need an instruction file, but they use different filenames:
- Claude Code reads: `claude.md`
- GitHub Copilot reads: `agents.md`

Maintaining two separate files that say the same thing is wasteful and error-prone. The solution:

**Instead of writing a real `claude.md`, create a `claude.md` that contains only:**
```
@agents.md
```

This means `claude.md` simply *points to* `agents.md`. You only maintain one file (`agents.md`), and both tools read from it. No duplication, no drift.

---

## 6. Managing Your Workflow — Sessions, Checkpoints & Git

This is one of the most conceptually important — and most confusing — parts of Claude Code. There are **three different and overlapping systems** for tracking progress and going back in time. Understanding the distinction between them is essential.

---

### The Three Levels of State Management

```
┌──────────────────────────────────────────────────────────┐
│  SESSIONS                                                 │
│  (High-level — entire conversation context snapshots)     │
│                                                           │
│   ┌──────────────────────────────────────────────────┐   │
│   │  CHECKPOINTS                                      │   │
│   │  (Fine-grained — each prompt = one checkpoint)   │   │
│   │                                                   │   │
│   │   ┌──────────────────────────────────────────┐   │   │
│   │   │  GIT                                      │   │   │
│   │   │  (Code-level — independent of Claude)    │   │   │
│   │   └──────────────────────────────────────────┘   │   │
│   └──────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────┘
```

| System | What it Tracks | Granularity | Goes Back In |
|---|---|---|---|
| **Sessions** | The entire conversation context with Claude | High — full sessions | Conversation context only (not code) |
| **Checkpoints** | Each individual prompt in the current session | Fine — every single prompt | Conversation + optionally the code changes too |
| **Git** | The state of your codebase | Whatever you commit | Code only (not Claude's conversation context) |

---

### Level 1 — Sessions (High-Level State)

A **session** represents the complete state of your conversation with Claude — everything in the context window at a particular moment, including all prior messages and the instructions Claude has been given.

**Key facts about sessions:**
- You can give a session a **name** at any point using `/rename`.
- Naming a session records its current state — you can resume from that named state later.
- When you exit and re-enter Claude Code, you can **resume** any named session.
- Resuming a session restores the **conversation context only** — it does NOT revert your code to how it was at that point in time. The code remains as it currently is on disk.

**Use case:** "I want to go back to the conversation I had with Claude last Tuesday, where we had agreed on a specific architecture, and pick up from there."

---

### Level 2 — Checkpoints & Rewinding (Fine-Grained State)

**Checkpoints** operate at a much finer level than sessions. They apply to the **current session** only.

Every single prompt you send to Claude Code automatically becomes a checkpoint. This means if you send 20 prompts in a session, you have 20 checkpoints you can step back through.

**Rewinding** means going back to a specific checkpoint — stepping backward through your conversation history, step by step.

When rewinding, you have a choice:
- **Rewind just the conversation** — go back to what Claude knew at that point, but leave the code on disk as it currently is.
- **Rewind both conversation AND code** — undo all the file changes Claude made since that checkpoint, reverting the code to exactly how it was at that prompt.

**Use case:** "Claude just made a bunch of changes I don't like, and I want to undo the last 3 prompts worth of changes."

---

### Level 3 — Git (Code Snapshots)

Git is the most familiar and most robust of the three systems. It operates entirely on your **codebase** and is completely independent of Claude's conversation context.

**Key points:**
- Git commits capture the exact state of your code at any point.
- You can make many Git commits even within a single Claude conversation — it doesn't need to be at a "higher" level of granularity.
- Git is the **long-term, permanent record** of your code's evolution.
- Unlike checkpoints, Git does not know or care about what Claude was thinking or what context it had — it just stores the code.

**Use case:** "I want to go back to how the code was three days ago, before we started the refactoring sprint."

---

### How These Three Levels Fit Together

| Situation | Best Tool |
|---|---|
| "I need to undo the last prompt's file changes right now." | **Checkpoint rewind** (conversation + code) |
| "I want to pick up a conversation from last week with the same context." | **Session resume** |
| "I need to roll back the entire codebase to a known-good state from 3 days ago." | **Git revert/checkout** |
| "I want a permanent record of every significant state of the project." | **Git commits** |
| "Claude is about to do something risky — I want a save point." | **Git commit first**, then proceed |

---

### The Instructor's Personal Workflow

Every developer will find their own balance between these three systems. Here is the instructor's preferred approach:

1. **Heavy use of Git** — commit frequently during Claude work, with clear commit messages describing what Claude did.
2. **Markdown files for progress tracking** — `claude.md`, `plan.md`, and task-specific docs serve as the memory system. These are human-readable and survive context compaction.
3. **Occasional checkpoint rewind** — used reactively when something just went wrong.
4. **Rarely uses sessions to go back** — finds it confusing to try to resume an old conversation. Prefers to re-orient Claude using well-maintained markdown files.
5. **Frequent `/compact` or `/clear`** — keeps context clean and starts fresh regularly.

> *"I use markdown files as my way to track progress. It's quite boring and old school of me... I honestly recommend you do the same."*

---

## 7. Sessions in Practice — Naming & Resuming

### Naming a Session

At any point during a Claude Code conversation, you can give the current session a name:

```
/rename snarky-claude
```

This records a checkpoint of the current conversation state with that name. From this point forward, you can always come back to exactly this conversation state.

**Example use case:**
You've told Claude to be witty and snarky. You want to preserve this personality setting so you can return to it after other experiments.

---

### Resuming a Named Session

Exit Claude Code (`Ctrl + C` twice), then launch Claude with the resume flag:

```bash
claude --resume
```

You will see a list of recent sessions, numbered, showing:
- The session name (if you named it).
- The last prompt sent in that session (so you can identify it by content).

Use the **up/down arrow keys** to select the session you want, then press **Enter** to resume it.

**What happens on resume:**
- The full conversation context from that session is restored.
- Claude remembers everything that was discussed up to the point you named/saved the session.
- The code on disk is whatever it currently is — the code is NOT reverted.

**Demo result:** After naming "snarky-claude" and resuming, Claude responded to "Please summarize the project" in its previously established witty, snarky style — proving the personality/context was fully restored.

---

## 8. Checkpoints in Practice — Rewinding

### What is a Checkpoint?

Every single prompt you send in the current session is automatically a checkpoint. No setup required — this happens automatically.

Think of checkpoints as an **undo history** for your conversation with Claude.

---

### How to Rewind

```
/rewind
```

This opens an interactive list showing every prompt sent in the current session, from newest to oldest. Use the **up arrow** to go back in time:

```
→ [current] are you sure the API key is exposed?
  please do a code review and write results to review.md
  please summarize the project
```

Navigate to the prompt you want to rewind to and press **Enter**.

---

### Rewind Options

After selecting a checkpoint, Claude Code asks you what you want to restore:

| Option | What it Does |
|---|---|
| **Both** (conversation + code) | Restores Claude's conversation context AND reverts all file changes made since that checkpoint. |
| **Conversation only** | Restores what Claude knew at that checkpoint but leaves all file changes on disk as they are. |
| **Code only** | Reverts file changes but keeps the current conversation context. |
| **Cancel** | Do nothing — stay at the current state. |

**Demo result:** After rewinding to before the hint about the `.env` file, the `review.md` file was reverted to its earlier state (with the incorrect critical finding restored), confirming that both the conversation and the code were successfully wound back.

---

### Limitations of Rewinding

Checkpointing and rewinding has **one important limitation**: Claude can only undo changes it knows about. Specifically:

- If Claude ran a script, and that script made changes to files, Claude may not be able to undo those file changes — it only knows about the direct file edits it made itself.
- Claude does not take a full snapshot of your entire disk at each checkpoint. It tracks what it directly wrote/edited.
- Side effects from running commands (e.g., database changes, environment changes, installed packages) cannot be reverted by rewinding.

**Bottom line:** For anything important, rely on **Git commits** as your true safety net. Checkpoints are a convenient quick-undo for recent direct file edits — not a substitute for version control.

---

## 9. YOLO Mode — Bypassing Permissions

### What is YOLO Mode?

**YOLO mode** is the practice of running Claude Code without any permission prompts. Normally, Claude Code asks you to approve every file edit and every command before it runs them. In YOLO mode, all of these prompts are skipped — Claude just does everything without asking.

**Why "YOLO"?** It stands for *You Only Live Once* — you are taking a risk by giving an AI agent unrestricted access to your machine. The name captures the spirit of the decision.

---

### YOLO Mode vs. Accept Edits Mode

These two are easy to confuse — they are **not the same thing**:

| Mode | How to Enable | What it Bypasses |
|---|---|---|
| **Accept Edits On** (`Shift + Tab`) | Shortcut inside Claude Code | Only file edit approvals — Claude still asks before running terminal commands. |
| **YOLO Mode** (`--dangerously-skip-permissions`) | Flag when launching Claude | Everything — file edits AND terminal commands — nothing is prompted. |

YOLO mode is a much bigger deal than Accept Edits mode. It gives Claude permission to run *any* terminal command without asking.

---

### How to Launch Claude Code in YOLO Mode

```bash
claude --dangerously-skip-permissions
```

The flag is intentionally verbose and alarming — Anthropic want you to know exactly what you are doing.

**Warning message displayed on launch:**
```
⚠️  Claude Code running in bypass permissions mode.
Claude will not ask for approval before running potentially
dangerous commands. Only use in a sandbox container that has
restricted access and can be easily restored.
By proceeding you take all responsibility.
```

---

### Risks & Warnings

**Theoretical risks:**
- Claude could theoretically run destructive commands (e.g., `rm -rf /`) — there is a non-zero statistical probability of this.
- No well-publicized catastrophic incidents are known (as of recording), especially with frontier models like Opus.
- More capable models are generally *less* likely to do something destructive — they reason about consequences.

**Practical risk mitigation:**
- The safer way to use YOLO mode is inside a **sandboxed container** (covered in Week 3) — an isolated environment that can be wiped and restored without affecting your main machine.
- Always **commit your code to Git** before running in YOLO mode. If something goes wrong, you have a restore point.
- Keep instructions **scoped and specific** — don't tell it to "do everything"; give it a focused task.
- **Watch what it is doing**, at least periodically, especially for destructive operations.

---

### YOLO Mode in Practice — UI Revamp Demo

**Prompt given to YOLO mode Claude:**
```
Please improve the UI of this project. Make sure the horizontal layout 
looks better with icons instead of delete buttons, using the horizontal 
space properly. Make your changes, test everything, and let me know when done.
```

**What happened (with no human intervention, while the instructor read emails):**
- Claude ran for **7 minutes and 44 seconds** entirely autonomously.
- Completely revamped the front-end user interface.
- Made the layout responsive — mobile-friendly.
- Replaced text "Delete" buttons with clean icon buttons.
- Reorganized the horizontal layout into logical sections.
- Added responsive breakpoints so the layout adapts as the browser window resizes.
- All tests passed.

**Result:** The UI went from basic to genuinely polished and professional-looking without a single human approval click.

> *"You've got to hand it to it. That's really very nice indeed."*

---

### Best Practices for YOLO Mode

1. **Always Git commit before** you start a YOLO session — this is your safety net.
2. **Use a sandbox** for anything beyond small, scoped tasks (covered in Week 3).
3. **Keep the initial prompt focused** — don't ask it to "build the entire app."
4. **Check in afterwards** — run the app, run the tests, verify it did what you expected.
5. **Git commit after** if the result is good — lock in the YOLO work.

```bash
# Before YOLO — create a safety checkpoint
git add .
git commit -m "before YOLO UI revamp"

# Run YOLO mode
claude --dangerously-skip-permissions

# After YOLO — review and lock in
git add .
git commit -m "after YOLO UI revamp"
```

---

## 10. Ralph Loops — Autonomous Agentic Coding on Autopilot

### What is a Ralph Loop?

A **Ralph Loop** is an **outer loop** placed around Claude's existing inner agent loop, causing Claude to repeat and keep improving on a task autonomously — iteration after iteration — without any human intervention between cycles.

In simple terms: where a normal Claude Code session does one pass at a task and then stops and waits for you, a Ralph Loop sets it off doing that task again and again, each iteration building on and improving the previous one.

**Visual analogy:**
```
Normal Claude Code:
[Your Prompt] → [Claude works] → [Claude stops, waits for you]

Ralph Loop:
[Your Prompt] → [Claude works] → [Done? → Start again, improve] → 
                                 [Done? → Start again, improve] →
                                 [Done? → Start again, improve] → ... × N iterations
```

---

### The Origin of the Term

The Ralph Loop was conceived by **Jeffrey Huntley**, an Australian engineer described as a "luminary." The name is a tribute to **Ralph Wiggum from The Simpsons** — specifically the character's cheerful, oblivious persistence.

The core idea is giving the agent a kind of optimistic momentum: *"You've finished? Great — keep going. Do it better."*

---

### How Ralph Loops Work Technically

Under the hood, the Ralph Loop plugin works like this:

1. You give Claude a task.
2. Claude works through the task using its normal inner agent loop.
3. When Claude reaches the point where it would normally say *"I'm finished"* and wait for input...
4. The Ralph Loop intercepts this — instead of stopping, it prompts Claude to continue.
5. The context is kept from growing uncontrollably through automatic management.
6. Claude restarts the task from its current state, improving and expanding.
7. This repeats for the number of iterations you specify (e.g., `--max-iterations 10`).

The result is essentially: one human prompt → multiple full Claude work cycles → compounded output.

---

### Installing the Ralph Loop Plugin

Plugins in Claude Code are installed with the `/plugin install` command:

```
/plugin install ralph-loop@claude-plugins-official
```

This installs the official Anthropic-published Ralph Loop plugin. If it's already installed, Claude will say so.

> **Note:** Plugins will be covered in depth on Day 3. You don't need to fully understand how plugins work to use this one.

After installation, the plugin creates a file called `ralph-loop-local.md` inside the `.claude` directory.

---

### Running a Ralph Loop

The Ralph Loop adds a new slash command: `/ralph-loop:ralph-loop`

**Full command syntax:**
```
/ralph-loop:ralph-loop <your prompt here> --max-iterations <N>
```

**Example from the demo:**
```
/ralph-loop:ralph-loop Please significantly improve this project. 
Add user management, multiple Kanban boards per user, and other 
features to build out a comprehensive project management application. 
Test thoroughly as you go and maintain strong test coverage and good 
integration tests. --max-iterations 10
```

This tells Claude to run up to **10 full iterations** of attempting to improve the project, with each iteration building on the last.

---

### Ralph Loop Demo — Results

**Starting state:** A basic Kanban board app with hard-coded authentication and a single board.

**After running Ralph Loop (10 iterations max, ran for approximately 1 hour):**

| Metric | Value |
|---|---|
| Lines added | 1,311 |
| Lines removed | 170 |
| Run time | ~1 hour |
| Human interventions | Periodic approval clicks (not full YOLO) |

**Features built autonomously:**
- **Proper user authentication** — create account, log in, log out, session persistence.
- **Multiple Kanban boards per user** — create, name, and switch between boards.
- **Data persistence** — boards and cards saved to database, survive logout/login.
- **Responsive UI** — layout adapts to different screen sizes.
- **Clean separation of user data** — each user only sees their own boards.

**Verified behaviour after the loop:**
- Create a new account with username/password → works.
- Create a board → works.
- Add cards → works.
- Switch between multiple boards → works.
- Log out and log back in → session and boards are fully restored.

> *"It is astonishing to think that we built this whole thing just in a couple of hours... and really, most of this was done by the Ralph Loop."*

---

### YOLO + Ralph Loop — The Ultimate Combination

You can combine YOLO mode and Ralph Loops for the maximum level of autonomous coding:

```bash
# Step 1 — Start Claude in YOLO mode
claude --dangerously-skip-permissions

# Step 2 — Trigger a Ralph Loop inside the YOLO session
/ralph-loop:ralph-loop <your ambitious prompt> --max-iterations 10
```

**What this means:** Claude runs for N full iterations, making any file edits and running any terminal commands it wants, without ever asking for permission. You can walk away and come back to a transformed codebase.

**Why this is powerful:**
- Where a single YOLO session might take 7-8 minutes and produce one round of improvements...
- A YOLO + Ralph Loop with 10 iterations could run for an hour or more, compounding improvements one on top of another.
- You could set a large iteration count and let it run overnight.

**⚠️ Critical Warning:** YOLO + Ralph Loop without a sandbox is high risk. The combination means:
- No human approval on any action.
- Multiple full iterations of potentially large, broad changes.
- If something goes wrong in iteration 2, iterations 3–10 are building on top of broken code.

**Best practice:** Only use YOLO + Ralph Loops inside a **sandboxed environment** (covered in Week 3). This is not recommended on a live production machine unless you are closely monitoring the session throughout.

---

### When to Use Ralph Loops (and When Not To)

#### ✅ Ralph Loops are great for:
- **Prototyping and MVPs** — rapid feature-building where you want to see how far it can get.
- **Exploring what's possible** — letting Claude surprise you with what it builds.
- **Boilerplate-heavy work** — scaffolding out CRUD features, auth flows, UI components.
- **When you have risk appetite** — you're happy to review the output carefully before using it.
- **Overnight builds** — set a high iteration count, go to sleep, see what exists in the morning.

#### ❌ Ralph Loops are NOT appropriate for:
- **Mission-critical or production code** — where every change needs careful review and accountability.
- **Projects with complex existing architecture** — Ralph Loops might introduce inconsistencies across many files.
- **Without a sandbox** (for YOLO + Ralph Loop combinations) — unacceptable risk on a live machine.
- **When you need predictable, controlled outcomes** — Ralph Loops are inherently exploratory and unpredictable.

> *"If you need predictable reliable outcomes and you want to play a primary role in building this out, then you should stick with a process that is more regimented than just going for a Ralph loop. But for MVPs and prototyping, Ralph loops are terrific."*

---

## 11. Key Takeaways — Day 2 Summary

### Commands to Memorise
- `/context` — check your fuel gauge before starting any task.
- `/compact` — run this manually after every major task, before the next.
- `/clear` — nuclear reset. Use when you want a completely fresh start.
- `/rewind` — undo recent checkpoints, with or without reverting code.
- `/rename` — name your current session to return to it later.
- `claude --resume` — bring back a named session.
- `claude --dangerously-skip-permissions` — YOLO mode.

### Workflow Management Mental Model
- **Git** = code safety net. Always commit before major Claude tasks.
- **Checkpoints** = quick undo for the current conversation. Useful but limited.
- **Sessions** = returning to a past conversation context. Doesn't touch the code.
- **Markdown files** = the most reliable and human-readable way to maintain shared knowledge with Claude across sessions and compactions.

### Autonomy Dial
Think of Claude Code as having an "autonomy dial" from 0 to 100:

| Setting | Mode | Approval Required |
|---|---|---|
| 0 (default) | Normal | Every edit and command |
| 25 | Accept Edits On (`Shift + Tab`) | Commands only |
| 75 | YOLO mode | Nothing — fully autonomous |
| 100 | YOLO + Ralph Loop | Nothing, multiple iterations, unsupervised |

The further right you move the dial, the more you trade control for speed and autonomy. Move the dial right proportionally with your risk appetite, your trust in the model, and the presence of safety nets (Git commits, sandboxing).

### The `@` Syntax — Summary
```
@docs/plan.md       → includes file contents in context
@src/               → includes a directory listing (not file contents)
```
Inside `claude.md`:
```
@agents.md          → delegates everything to agents.md (single source of truth trick)
```

---

*End of Day 2 — Pro Week Notes*
