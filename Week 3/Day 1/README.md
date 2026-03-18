# Claude Code — Week 3, Day 1: Complete Study Guide
### Pro Sub-Agents, Hooks, Swarms & Controlled Chaos

---

## Table of Contents

1. [Week Overview & Philosophy](#1-week-overview--philosophy)
2. [The Two Mindsets: Chaos vs. Control](#2-the-two-mindsets-chaos-vs-control)
3. [Controlled Chaos — The Core Principle](#3-controlled-chaos--the-core-principle)
4. [The FiNALLY Project — Setting Up the Multi-Agent Trading App](#4-the-finally-project--setting-up-the-multi-agent-trading-app)
5. [Custom Slash Commands](#5-custom-slash-commands)
6. [Agents and Sub-Agents](#6-agents-and-sub-agents)
7. [Subagents vs. Agent Teams](#7-subagents-vs-agent-teams)
8. [Hooks — Auto-Triggering Events and Reviews](#8-hooks--auto-triggering-events-and-reviews)
9. [Building Custom Plugins and Marketplaces](#9-building-custom-plugins-and-marketplaces)
10. [Pros and Cons of Sub-Agents — Final Summary](#10-pros-and-cons-of-sub-agents--final-summary)

---

## 1. Week Overview & Philosophy

### What This Week Covers

Week 3 is the "finale week" of the AI Codec Course. It focuses on the deeper, more powerful CLI (Command-Line Interface) features of Claude Code. The week is organized across four days:

| Day | Focus |
|-----|-------|
| Day 1 (Today) | Multi-agents, sub-agents, hooks, slash commands, plugins |
| Day 2 | Sandboxing — a critical safety and repeatability topic |
| Day 3 | Working successfully with large codebases |
| Day 4 | Swarms, orchestrators, advanced multi-agent architectures + capstone project |

### The 8 Stages of the Coding Agent Evolution

The course references **Steve Yegge's 8 stages** of how developers evolve as AI coding agent programmers:

- **Stage 5** (covered in Week 2): Deep use of the CLI, letting Claude work while you watch the diff scroll by, working in a "plan → execute → review → test" loop with a "trust but verify" mindset.
- **Stages 6, 7, and 8** (this week): Multi-agents → Swarms → Orchestrating agents. This is described as the "bigger deal" and comes with excitement but also a degree of chaos.

---

## 2. The Two Mindsets: Chaos vs. Control

The key conceptual framework for this week is understanding that pro techniques fall into **two opposing categories**:

### The Chaos Side (Positive Feedback)
These techniques *amplify* what is happening — they go big, go fast, and increase throughput at the cost of predictability:

- **YOLO Mode** — Just go for it. Let Claude make decisions without confirmation.
- **REPL/Ralph Loops** — Set it running and come back later (after lunch, overnight) to see results.
- **GSD (Get Stuff Done)** — A variation of letting the agent run autonomously.
- **Swarms** — Many agents running simultaneously, all working in parallel. Maximum chaos.

### The Control Side (Negative Feedback)
These techniques *rein things in* and keep quality high:

- **File System as Coordination Layer** — Having all agents read and write to shared files (architecture decisions, open questions, testing strategies) so they stay coordinated.
- **Self-Correcting Processes** — Agents whose job is to test, review code, and pull things back on track, acting as a brake on the chaos.
- **Sandboxes** — Running all the craziness inside an isolated environment you can destroy and restart. Gives repeatability.
- **Orchestration** — Having agents in a hierarchy with defined roles. One agent manages others. Structure is imposed.

---

## 3. Controlled Chaos — The Core Principle

> *"Think of it like a nuclear reactor. When you put the rods down to control, it's a controlled chain reaction."*

The goal of this week is not pure chaos and not pure control — it is **controlled chaos**: a deliberate balance between the two.

### How to Achieve It in Practice

1. **Start with more control**, not less. Begin a real project with close oversight.
2. **Gradually loosen your grip** as you see good results and build confidence.
3. **Pull back control** whenever things start going off the rails.
4. The right balance depends on:
   - Your risk appetite
   - Your team's comfort level
   - The nature of the project (mission-critical vs. experimental)

### Why This Balance Matters

- **Too much chaos** → Positive feedback loop → Things get bigger and bigger, harder to track, errors compound.
- **Too much control** → You lose the speed and parallelism advantages of multi-agent systems.
- **Balanced** → You amplify what you can do while still getting good, reliable results.

### A Key Reminder
You are always accountable for the code you deliver. The LLM coding agent is a tool to help you work more efficiently — not to replace your judgment. **You are the boss.**

---

## 4. The FiNALLY Project — Setting Up the Multi-Agent Trading App

### What is the FiNALLY Project?

The course capstone project is called **FiNALLY**, which has a double meaning:
- It is the **final week** of the course.
- The name stands for **FiN**ance **ALL**y — a finance ally application.

The project is a **live AI-powered trading workstation** — think of it as a modern Bloomberg Terminal with an AI co-pilot. It will:

- Stream **live (or simulated) market data**
- Allow users to trade in a **simulated portfolio**
- Integrate an **LLM assistant** that can analyze portfolios and execute trades on your behalf

The entire application will be built **by an army of agents** working in controlled chaos.

### Project Setup Steps

1. Clone the starter repo:
   ```bash
   git clone <finally-repo-url>
   cd finally
   ```
2. Open it as a new project in VS Code.
3. Explore the initial scaffolding.

### Project Structure

```
finally/
├── .claude/          # Claude configuration
├── planning/
│   └── plan.md       # The master business requirements document
├── backend/          # Empty — to be built by agents
├── db/               # Empty — to be built by agents
├── frontend/         # Empty — to be built by agents
├── tests/            # Empty — to be built by agents
├── .env              # API keys (OpenRouter, optional Massive/Polygon)
├── .gitignore
└── claude.md         # Project-level Claude instructions
```

### The Role of `claude.md`

The `claude.md` file is intentionally short and points to the `planning/` directory for all documentation. This is a deliberate architectural decision: **all agents converge on shared documentation**. The `plan.md` file is included via the `@` notation, which forces it into the context every single time — giving every agent a shared source of truth.

### The Master Plan Document (`plan.md`)

This is the heart of the project. It was created by having a conversation with Claude (the chat product) to flesh out the requirements. It contains:

- **Vision**: What the app is and why it matters.
- **User Experience**: Docker-based deployment, browser opens to localhost, streaming price data, portfolio monitoring, LLM chat assistant.
- **Architecture**: SQLite for the database (simple, lazy initialization), SSE (Server-Sent Events) for streaming market data to the UI (the same technology used for AI token streaming), a single Docker container (not multiple — keep it simple).
- **API Keys**: OpenRouter key (required), Massive/Polygon.io key (optional — the app includes a simulated market data mode).
- **LLM Integration**: Uses the Cerebrace skill (from Week 2), structured outputs so the LLM can make trading decisions and alter the UI.
- **Frontend Design**: Screen layout, color scheme.
- **Testing**: Unit tests and end-to-end tests.

### Key Design Principle: Boundary Clarity

When multiple agents work on different parts of a project, it is critical to clearly define **boundaries** between areas. Agents need to know:
- What they are responsible for
- How they interact with other agents' work

### Human Oversight Is Essential

Even when using AI to generate the plan document, human review is critical. For example, Claude initially suggested a multi-container Docker setup — which was overruled by the human instructor as unnecessarily complex. Always challenge the AI: *"Could this be simpler?"*

---

## 5. Custom Slash Commands

### What Are Slash Commands?

Slash commands are shortcuts you can type in the Claude Code prompt (using `/`) to trigger a pre-defined action. Claude Code ships with some built-in ones (like `/context`, `/hooks`, `/agents`, `/plugins`), but you can **create your own**.

### Two Ways to Create a Slash Command

#### Method 1: The `commands` Folder (Simple)

Inside your `.claude` directory (either project-level or in your home directory for global commands), create a folder called `commands`:

```
.claude/
└── commands/
    └── doc-review.md
```

The **filename** (without the `.md`) becomes the slash command name. The **contents** of the file is the prompt that runs when the command is used.

**Example — `doc-review.md`:**
```
Review the documentation file in the planning folder called $ARGUMENTS
and add questions, clarifications, or feedback to a new section at the end,
along with any opportunities to simplify.
```

The special variable **`$ARGUMENTS`** is replaced by whatever the user types after the slash command name.

**How to use it:**
```
/doc-review plan.md
```

This will prompt Claude to review `planning/plan.md` and append feedback.

#### Method 2: Skills (More Common in Practice)

Skills automatically create a slash command. Any skill you create (a folder inside `.claude` with its own markdown file) instantly becomes available as a slash command. This is actually the **more common modern approach** because skills can also include YAML front matter for metadata and can be more richly defined.

The `cerebrace-inference` skill created in Week 2, for example, appears automatically as `/cerebrace-inference` in the slash command menu.

### Important Distinction: Commands vs. Sub-Agents

A slash command runs within the **existing conversation context** — the interaction is part of your conversation history. A sub-agent, by contrast, runs in an **isolated context** — the work happens in a separate LLM call that doesn't pollute the main conversation. This distinction becomes very important as complexity grows.

### Sharing Slash Commands with Your Team

If you commit the `.claude/commands/` folder to Git, every team member who clones the repository automatically gets those same slash commands available to them. This makes it easy to standardize workflows across a team.

### Human Oversight During Reviews

After running a doc-review command, always critically evaluate the suggestions. In the example from the lesson, Claude suggested several simplifications (like dropping the Massive API integration and removing user IDs from all tables) that the instructor disagreed with and overruled. The AI's suggestions are a starting point — **you add value by being the decision-maker**.

---

## 6. Agents and Sub-Agents

### What Are Multi-Agents? (The Simple Definition)

The simplest definition of "multi-agent" is just: **running multiple instances of Claude Code at the same time**. You can open several terminal windows, each running `claude`, and have one build the frontend, one build the backend, and one write tests — all in parallel.

The challenge: this only works well if the plan document is detailed enough that each agent knows its exact scope and how its work connects with the others. Without that, you get chaos — agents making incompatible decisions and not even knowing other agents are at work.

### Using a Different Agent: Codex CLI

Claude Code isn't the only coding agent CLI. OpenAI's equivalent is the **Codex CLI**. It can be installed via npm:

```bash
npm install -g @openai/codex
```

And run with:
```bash
codex
```

Or used in non-interactive "execute" mode:
```bash
codex exec "please review the file planning/plan.md and write your feedback to planning/review.md"
```

This opens the door to **having different LLMs collaborate** — Claude can orchestrate a workflow where Codex (GPT-powered) handles specific tasks like code reviews.

### What Are Sub-Agents? (The Important Concept)

Sub-agents are a first-class feature of Claude Code. A sub-agent is a **separate LLM call** that:

1. **Takes on a specific task** delegated from the main Claude Code session.
2. **Runs in its own isolated context** — so the work of the sub-agent doesn't pollute the main conversation's context window.
3. **Returns its result** back to the main Claude Code.
4. Can **run in parallel** with other sub-agents.
5. Can optionally use **cheaper/faster models** (like Claude Haiku) for simpler tasks.

Claude Code comes with several built-in sub-agents (e.g., one for exploring file systems, one for planning), and you can see them firing with a different color in the output trace.

### Creating Your Own Sub-Agent

Sub-agents are defined as markdown files inside a special folder.

**Step 1:** Inside your `.claude` folder, create a folder called `agents`:

```
.claude/
├── commands/
├── skills/
└── agents/
    └── reviewer.md
```

**Step 2:** Write the agent definition file (`reviewer.md`):

```yaml
name: reviewer
description: Carry out a comprehensive review when requested.
```

Below the front matter, you write the instructions for what this agent does:

```
You review the file planning/plan.md and write your feedback to planning/review.md.
```

You can optionally specify:
- **`tools`**: Which tools the agent has access to (if not specified, it inherits from the parent)
- **`model`**: Which Claude model to use (e.g., `claude-haiku-4-5` for speed/cost efficiency)

**Step 3:** Verify the agent exists by running `/agents` inside Claude Code. Your `reviewer` agent will appear in the list.

**Step 4:** To trigger it, instruct Claude Code in natural language:
```
Use the reviewer sub-agent to carry out a review.
```

The keyword **"sub-agent"** helps Claude understand you want it to delegate the task rather than doing it inline.

### Where You Can Define Agents

Agents can be defined in several locations:

| Location | Scope |
|---|---|
| `.claude/agents/` in the project folder | Available in this project only |
| `~/.claude/agents/` in home directory | Available in all your projects |
| As part of a plugin | Distributed to anyone who installs the plugin |
| Via flags when launching `claude` | Specialized, not commonly used |

### Watching Sub-Agents Work: The Context Benefit

After a sub-agent completes, run `/context` in Claude Code. You'll see that the main conversation context is **clean and small** — the heavy work (reading files, analyzing, writing outputs) all happened in the sub-agent's isolated context. This is one of the biggest practical advantages.

### Example: A Codex-Powered Sub-Agent

You can create a sub-agent that *itself* calls Codex as an external process:

**`codex-reviewer.md`:**
```
name: codex-reviewer
description: Carry out a comprehensive review of plan.md when requested using Codex.

You are using a different AI agent to carry out a review of the document
planning/plan.md. You must execute the following shell command to carry
out the review. Do not review yourself.

Execute: codex exec "please review planning/plan.md and write feedback to planning/review.md"
```

This creates a powerful pattern: **Claude Code spawns a sub-agent, which in turn calls Codex**, giving you the opinions of two completely different AI models on the same work.

---

## 7. Subagents vs. Agent Teams

These are **two different things** and it's important to understand the distinction.

### Sub-Agents: The Simple Pattern

| Characteristic | Detail |
|---|---|
| **Relationship** | Always one main Claude Code that delegates to sub-agents |
| **Communication** | Sub-agent takes task → does work → returns result to main |
| **Context** | Isolated per sub-agent call |
| **Duration** | Short-lived — one task, one answer |
| **Memory** | Can optionally use project-level memory (configured in settings) |

Sub-agents are: **take a task → carry it out → return the answer**. Clean, simple, predictable.

### Agent Teams: The New Paradigm

Agent teams are an **experimental feature** in Claude Code that goes beyond the simple delegation model:

| Characteristic | Detail |
|---|---|
| **Relationship** | A whole group of Claude Code instances running collaboratively |
| **Communication** | Agents can communicate **directly with each other** — not just through the main Claude Code |
| **Context** | Each agent has a longer-running presence in the "team" |
| **Duration** | Long-running — agents persist throughout a session or longer |
| **Interaction** | Agents can challenge each other, test hypotheses, give feedback directly |

**Example of what an Agent Team enables:**
- A **tester agent** gives test feedback directly to a **frontend agent** and a **backend agent** simultaneously
- Agents can debate, challenge each other's decisions, and iterate together
- The whole team collaboratively produces a complex output

This is the foundation of the swarms and orchestration concepts coming on Day 4.

### When to Use Which

| Use Sub-Agents When... | Use Agent Teams When... |
|---|---|
| You have a well-defined, self-contained task | You need multiple agents collaborating on a complex, intertwined problem |
| You want to keep the main context clean | You want agents to have awareness of each other's work |
| You want speed and simplicity | You're ready for the more experimental, complex patterns |

---

## 8. Hooks — Auto-Triggering Events and Reviews

### What Is a Hook?

A **hook** is a mechanism that automatically triggers an action when a specific **event** occurs in Claude Code. Think of it as: *"Whenever X happens, automatically do Y."*

Hooks are a **pro feature** — most of the time you don't need them, but when you do, they're very powerful. You don't need to memorize all the details; just know they exist and consult the docs when needed.

### Events That Can Trigger a Hook

Claude Code defines several events:

| Event | When It Fires |
|---|---|
| `pre-tool-use` | Just before Claude is about to call a tool (e.g., run a shell command) |
| `post-tool-use` | Just after Claude finishes a tool call |
| `post-tool-use-failure` | After a tool call fails |
| `notification` | When Claude wants to send you a notification |
| `user-prompt-submit` | When you submit a new prompt |
| `session-start` | When a session begins |
| `stop` | When Claude finishes its work and is stopping |
| `sub-agent-start` | When a sub-agent begins |
| `sub-agent-stop` | When a sub-agent finishes |
| `pre-compact` | Just before Claude is about to compact the context window |
| `session-end` | When the entire session ends |

### Three Types of Hook Actions

When a hook fires, you can configure it to do one of three things:

1. **`command`**: Run a shell command. This is the most predictable and reliable option. Recommended for most use cases.
2. **`prompt`**: Send a new prompt to Claude. Can be used to give instructions, but has some permission constraints (e.g., cannot write files directly).
3. **`agent`**: Spawn a sub-agent to handle the response. Keeps the work off the main context, but takes some experimentation to configure robustly.

> **Best practice**: Start with `command` type hooks. They are bulletproof and easy to reason about.

### Practical Use Cases for Hooks

**Use case 1 — Fix a persistent bad habit:**
Claude keeps using `python` instead of `uv run`. Add a `pre-tool-use` hook that intercepts shell commands and replaces `python` with `uv run`.

**Use case 2 — Get notified when Claude is waiting:**
Claude sometimes stops and waits for your permission. Add a `notification` hook that sends you a desktop/phone notification so you can leave it running and return when needed.

**Use case 3 — Automatic code review on completion:**
The most common and powerful use case: add a `stop` hook so that every time Claude finishes a piece of work, a code review is automatically triggered.

> **Note**: The REPL/Ralph Loop pattern is implemented using a `stop` hook. When Claude finishes, a new prompt is sent ("I don't think you finished. Try again."), which causes it to loop.

### Where to Define Hooks

Hooks are defined in **`.claude/settings.json`**:

```
.claude/
└── settings.json
```

If this file doesn't exist, create it. Example structure:

```json
{
  "hooks": {
    "stop": [
      {
        "command": "codex exec \"review all changes since the last commit and write results to planning/review.md\""
      }
    ]
  }
}
```

### Exploring Hooks Interactively

You can also manage hooks through the Claude Code menu:

```
/hooks
```

This displays all configured hooks for each event type, and lets you add new ones interactively without editing JSON manually.

### The `matcha` Filter

You can optionally add a `matcha` property to a hook to specify conditions under which it should fire. For example, only trigger a pre-tool-use hook if the command contains the word `python`. Refer to the official Claude Code docs for the full syntax.

### Demo: Automatic Review on Stop

Here is the complete flow demonstrated in the lesson:

1. Run a normal Claude Code task: `please make a concise README.md for the project`
2. Claude writes the README and signals it is done.
3. The `stop` event fires.
4. The hook runs the command: `codex exec "review all changes since the last commit and write results to planning/review.md"`
5. Behind the scenes, Codex reads the git diff and writes a code review to `review.md`.
6. Claude Code's main context remains clean — it doesn't even know Codex came in and did a review.

---

## 9. Building Custom Plugins and Marketplaces

### Why Build a Plugin?

A **plugin** bundles together all the things you've learned — commands, skills, sub-agents, and hooks — into a single, installable, shareable package. This is useful when:

- You work in a **larger team** and want everyone to have the same tools.
- You want to build a **company-internal marketplace** of Claude Code tools.
- You want to **share your tools** with the wider community via GitHub.

### Plugin Directory Structure

Every plugin lives in its own folder and follows a specific structure:

```
independent-reviewer/         ← Your plugin's top-level folder
└── .claude-plugin/           ← Required special folder name
    ├── plugin.json           ← The manifest (required)
    ├── commands/             ← Optional: slash commands
    ├── skills/               ← Optional: skills
    ├── agents/               ← Optional: sub-agent definitions
    └── hooks/
        └── hooks.json        ← Optional: hook definitions
```

### Step-by-Step: Creating a Plugin

**Step 1: Create the plugin folder**

Create a directory for your plugin (can be inside an existing repo or in its own repo):

```
mkdir independent-reviewer
```

**Step 2: Create the `.claude-plugin` subfolder**

The name `.claude-plugin` is **fixed** — it must be exactly this.

```
mkdir independent-reviewer/.claude-plugin
```

**Step 3: Create `plugin.json` — the manifest**

Inside `.claude-plugin`, create a file called `plugin.json`:

```json
{
  "name": "independent-reviewer",
  "description": "Carries out an independent review of all changes since last commit.",
  "version": "1.0.0"
}
```

**Step 4: Add your hooks**

Create the `hooks` folder and a `hooks.json` file inside it. Move your hook definition here from `settings.json`:

```
independent-reviewer/
└── .claude-plugin/
    ├── plugin.json
    └── hooks/
        └── hooks.json
```

`hooks.json` contains the same JSON structure as what you would put in `settings.json`:

```json
{
  "hooks": {
    "stop": [
      {
        "command": "codex exec \"review all changes since the last commit and write results to planning/review.md\""
      }
    ]
  }
}
```

> **Important**: Remove the hook from `settings.json` once you've moved it to the plugin — you don't want the same hook running twice.

### Creating a Marketplace

Rather than referencing a single plugin file at launch time (which is inflexible), the recommended approach is to create a **marketplace** — a collection of plugins that can be browsed and installed through the Claude Code UI.

**Step 1: Create the marketplace folder**

At the root of your repository (the folder that will become the marketplace), create:

```
.claude-plugin/
└── marketplace.json
```

Note: `.claude-plugin` at the root level is the marketplace configuration folder, analogous to `.claude-plugin` inside a plugin folder.

**Step 2: Define the marketplace in `marketplace.json`**

```json
{
  "name": "EdTools",
  "author": "Ed",
  "email": "ed@example.com",
  "plugins": [
    {
      "name": "independent-reviewer",
      "description": "Carries out an independent review of all changes since last commit.",
      "path": "independent-reviewer"
    }
  ]
}
```

You can list as many plugins as you want. The `path` points to the relative directory of each plugin within the repository.

### Installing a Plugin from a Marketplace

**Step 1:** In Claude Code, run:
```
/plugin
```

**Step 2:** Navigate to **Marketplaces** → **Add marketplace**

**Step 3:** Provide the marketplace path. It can be:
- A **local path** (e.g., `./` for the current directory — great for testing)
- A **GitHub URL** (e.g., your company's internal marketplace repo)
- Any other URL pointing to a repository with a `marketplace.json`

**Step 4:** Browse the plugins from that marketplace and **select which ones to install**.

**Step 5:** Choose the **scope** of installation:
- **Project scope**: Installs for all collaborators on the repository (written to `.claude/settings.json` in the project)
- **User scope**: Installs just for you

**Step 6:** **Restart Claude Code** to load the new plugin.

After restarting, run `/plugin` → **Installed** to see your plugin listed and active.

### How It All Works Together

Once the plugin is installed with its hooks, the full automated workflow runs seamlessly:

1. You ask Claude to do some work (e.g., `write a README`)
2. Claude does the work
3. Claude signals it is done (`stop` event)
4. The plugin's hook fires automatically
5. The hook launches Codex (or any shell command) in the background
6. A `review.md` is written with a code review of all changes
7. Claude's main context is completely unaware this happened — it stays clean

This is the foundation of the **self-correcting, multi-agent workflow** that will be expanded upon throughout the week.

---

## 10. Pros and Cons of Sub-Agents — Final Summary

Before wrapping Day 1, here is a clear summary of when sub-agents add value and when they introduce risk.

### Advantages of Sub-Agents

| Advantage | Explanation |
|---|---|
| **Parallelism** | Multiple sub-agents can work simultaneously, dramatically increasing throughput |
| **Self-correction** | Reviewer/tester sub-agents can provide negative feedback loops, keeping work on track |
| **Context efficiency** | Heavy work (file reads, analysis, generation) happens off the main context, keeping it clean and available |
| **Specialization** | Each sub-agent can be fine-tuned with a perfect prompt for exactly one task |
| **Cost optimization** | Simpler sub-tasks can be run on cheaper, faster models (e.g., Claude Haiku) |

### Disadvantages of Sub-Agents

| Disadvantage | Explanation |
|---|---|
| **More moving parts** | Every additional process is something that can break in mysterious, hard-to-debug ways |
| **Boundary issues** | Errors at the interface between sub-agent and main agent can cause subtle, compounding mistakes |
| **Error amplification** | If something goes wrong early, multiple agents can diverge in different (wrong) directions simultaneously, making recovery hard |
| **Potential cost increase** | More activity = more tokens = higher costs, especially with self-correcting review loops |

### When to Reach for Sub-Agents

Reach for sub-agents when:
- You need to **keep the main context clean** (most common reason)
- You have a **well-defined, repeatable task** worth encapsulating
- You want **parallelism** and the plan document is solid enough to support it
- You want a **quality gate** (review, test, lint) that runs automatically

Avoid sub-agents when:
- The overhead of defining them outweighs the benefit for a one-off task
- The plan/spec isn't detailed enough to give agents clear, non-overlapping boundaries
- You're still early in a project and things are likely to change rapidly

---

## Quick Reference: Where Everything Lives

```
.claude/
├── claude.md                 # Project-level Claude instructions
├── settings.json             # Hooks configuration
├── commands/
│   └── doc-review.md         # Custom slash commands
├── agents/
│   ├── reviewer.md           # Sub-agent definitions
│   └── codex-reviewer.md     # Sub-agent that calls external CLIs
└── skills/
    └── cerebrace-inference/  # Skills (also become slash commands)

independent-reviewer/         # A standalone plugin
└── .claude-plugin/
    ├── plugin.json           # Plugin manifest
    ├── commands/
    ├── agents/
    ├── skills/
    └── hooks/
        └── hooks.json        # Hook definitions for this plugin

.claude-plugin/               # Marketplace root (at repo level)
└── marketplace.json          # Lists all plugins in this marketplace
```

---

## Key Concepts Glossary

| Term | Definition |
|---|---|
| **Controlled Chaos** | The philosophy of balancing chaotic speed/parallelism with stabilizing control mechanisms |
| **YOLO Mode** | Running Claude without confirmation prompts — high speed, high risk |
| **REPL/Ralph Loop** | A loop where Claude keeps working autonomously, triggered by hooks |
| **Swarm** | Many agents running simultaneously with minimal coordination |
| **Orchestration** | Agents in a defined hierarchy with roles — adds control to multi-agent systems |
| **Slash Command** | A `/keyword` shortcut that triggers a predefined prompt or action |
| **$ARGUMENTS** | Placeholder in a slash command file that gets replaced with what the user types |
| **Sub-Agent** | A separate LLM call, running in an isolated context, delegated a specific task |
| **Agent Team** | Multiple Claude Code instances that communicate with each other (experimental) |
| **Hook** | An auto-triggered action tied to a specific event in Claude Code |
| **Event** | A lifecycle moment in Claude Code (e.g., `stop`, `pre-tool-use`) that can trigger hooks |
| **Plugin** | A packaged bundle of commands, skills, agents, and hooks |
| **Marketplace** | A collection of plugins that can be browsed and installed via the Claude Code UI |
| **Context Window** | The "memory" available to Claude in a given conversation — must be managed carefully |
| **`plan.md`** | The master specification document that all agents in the FiNALLY project reference |
| **SSE** | Server-Sent Events — the technology used to stream market data (same as AI token streaming) |
| **Codex CLI** | OpenAI's equivalent of Claude Code — can be used as a sub-agent |

---

*End of Day 1 Notes — Week 3 of the AI Codec Course*
