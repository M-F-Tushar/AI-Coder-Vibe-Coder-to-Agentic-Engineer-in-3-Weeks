# Day 3 — Pro Week: MCP, Skills & Plugins — The Big Three Building Blocks of Claude Code

> **Overview:** Day 3 is the conceptual centrepiece of the course — passing the halfway point and what the instructor calls an "inflection point." This day covers the three most important architectural building blocks for extending Claude Code's capabilities: **MCP (Model Context Protocol)**, **Skills**, and **Plugins**. Each has its own strengths, weaknesses, and appropriate use cases.

---

## Table of Contents

1. [The Big Picture — Why Claude Code Needs Extensions](#1-the-big-picture--why-claude-code-needs-extensions)
2. [The Foundation — Tools: The Real Innovation](#2-the-foundation--tools-the-real-innovation)
3. [MCP — Model Context Protocol](#3-mcp--model-context-protocol)
   - [What is MCP?](#what-is-mcp)
   - [The USB-C Port Analogy](#the-usb-c-port-analogy)
   - [Why MCP Became a Big Deal](#why-mcp-became-a-big-deal)
   - [The Correct Way to Think About MCP](#the-correct-way-to-think-about-mcp)
   - [MCP Technical Architecture — Hosts, Clients & Servers](#mcp-technical-architecture--hosts-clients--servers)
   - [MCP Transport Modes — Local vs Remote](#mcp-transport-modes--local-vs-remote)
   - [Common Misconceptions About Local MCP Servers](#common-misconceptions-about-local-mcp-servers)
4. [Discovering MCP Servers — Marketplaces & Registries](#4-discovering-mcp-servers--marketplaces--registries)
   - [Official MCP Registry](#official-mcp-registry)
   - [Anthropic's Reference MCP Servers on GitHub](#anthropics-reference-mcp-servers-on-github)
   - [MCP Marketplace Sites](#mcp-marketplace-sites)
   - [How to Verify an MCP Server is Legitimate](#how-to-verify-an-mcp-server-is-legitimate)
5. [Adding MCP Servers to Claude Code — Hands-On](#5-adding-mcp-servers-to-claude-code--hands-on)
   - [Installing Context7 — Live API Documentation](#installing-context7--live-api-documentation)
   - [Using Context7 in Claude Code](#using-context7-in-claude-code)
   - [Installing Polygon IO — Market Data](#installing-polygon-io--market-data)
   - [Context Window Efficiency — The New Lazy Loading Behaviour](#context-window-efficiency--the-new-lazy-loading-behaviour)
   - [Removing MCP Servers](#removing-mcp-servers)
6. [MCP Pros and Cons — Summary](#6-mcp-pros-and-cons--summary)
7. [Skills — Claude Code's Simpler Way to Add Abilities](#7-skills--claude-codes-simpler-way-to-add-abilities)
   - [What are Skills?](#what-are-skills)
   - [Key Advantages of Skills Over MCP](#key-advantages-of-skills-over-mcp)
   - [Progressive Disclosure — The Core Concept](#progressive-disclosure--the-core-concept)
   - [The Three Levels of Progressive Disclosure](#the-three-levels-of-progressive-disclosure)
   - [File System Architecture — How Skills are Structured](#file-system-architecture--how-skills-are-structured)
   - [The skill.md File Format](#the-skillmd-file-format)
   - [Global vs Project-Level Skills](#global-vs-project-level-skills)
   - [Sharing Skills with Your Team](#sharing-skills-with-your-team)
   - [How Scripts Work in Skills](#how-scripts-work-in-skills)
8. [Skills Marketplaces — Where to Find Skills](#8-skills-marketplaces--where-to-find-skills)
   - [Anthropic's Official GitHub Skills Repo](#anthropics-official-github-skills-repo)
   - [skills.sh — The Vercel Curated Marketplace](#skillssh--the-vercel-curated-marketplace)
   - [Installing the Agent Browser Skill Step-by-Step](#installing-the-agent-browser-skill-step-by-step)
   - [Agent Browser in Action](#agent-browser-in-action)
9. [Skills Pros and Cons — Summary](#9-skills-pros-and-cons--summary)
10. [Plugins — The Highest-Level Building Block](#10-plugins--the-highest-level-building-block)
    - [What are Plugins?](#what-are-plugins)
    - [What Can a Plugin Bundle Together?](#what-can-a-plugin-bundle-together)
    - [The Plugins Marketplace — Inside Claude Code](#the-plugins-marketplace--inside-claude-code)
    - [Installing Plugins Step-by-Step](#installing-plugins-step-by-step)
    - [Top Plugins to Know About](#top-plugins-to-know-about)
    - [Using a Plugin — Code Simplifier Demo](#using-a-plugin--code-simplifier-demo)
    - [Adding External or Team Marketplaces](#adding-external-or-team-marketplaces)
11. [Plugins Pros and Cons — Summary](#11-plugins-pros-and-cons--summary)
12. [MCP vs Skills vs Plugins — The Complete Comparison](#12-mcp-vs-skills-vs-plugins--the-complete-comparison)
13. [Decision Framework — Which One Do You Use?](#13-decision-framework--which-one-do-you-use)
14. [Key Takeaways — Day 3 Summary](#14-key-takeaways--day-3-summary)

---

## 1. The Big Picture — Why Claude Code Needs Extensions

Out of the box, Claude Code is powerful — but its power is limited to what Anthropic has built into it. The real game-changer is the ability to **extend** Claude Code with tools, expertise, and abilities written by other people.

This is the problem that **MCP**, **Skills**, and **Plugins** all solve — each in a different way, each with different trade-offs.

The reason this feels confusing at first is that all three of them can:
- Be installed and uninstalled independently.
- Add new capabilities to Claude Code.
- Overlap in what they can accomplish.

The goal of Day 3 is to understand each one clearly and know when to use which.

---

## 2. The Foundation — Tools: The Real Innovation

Before understanding MCP, Skills, and Plugins, you need to understand **what makes all of them possible** in the first place: the concept of **Tools**.

### What is a "Tool" in the Context of LLMs?

A standard LLM does one thing: it generates tokens. It predicts the next word, then the next, and so on. That is it — no actions, just content generation.

**Tools** change this fundamentally. Here is how a tool works:
1. As part of generating tokens, the LLM produces a special kind of output that says: *"I want to take this specific action."*
2. The system surrounding the LLM interprets that output and actually executes the action.
3. The result of the action is fed back to the LLM as new input.
4. The LLM continues generating, now informed by the result.

This is what transforms a token-predictor into something that can **actually do things in the world**.

### Tools Already Built Into Claude Code

Anthropic has baked several tools directly into Claude Code:

| Built-in Tool | What it Does |
|---|---|
| **To-do list manager** | Lets Claude add tasks, check them off, and track progress. This is why you see Claude "checking things off" as it works. |
| **File manager** | Lets Claude read, write, create, and edit files in your project. |
| **Internet search** | Lets Claude search the web for current information. |
| **Shell command runner** | Lets Claude execute terminal commands (subject to your permissions). |

### Why This Matters for MCP, Skills, and Plugins

The entire point of MCP, Skills, and Plugins is to give Claude Code access to **more tools** — tools written by other people, for specialized purposes. Everything in this lesson is ultimately about bolting more tools onto Claude Code so it can do more things.

> **The key insight:** MCP, Skills, and Plugins are all ultimately about tools. Tools are the real innovation. The others are just different ways of *delivering* tools to Claude Code.

---

## 3. MCP — Model Context Protocol

### What is MCP?

**MCP (Model Context Protocol)** is an **open standard** — a protocol — for connecting AI applications like Claude Code to tools written by other people.

The key word is *protocol*. MCP is not:
- A library of tools.
- A specific implementation.
- A piece of software you run.

MCP **is**:
- An agreed standard that tells developers *how* to package their tools so that any AI application can use them.
- A universal interface between AI applications (Claude Code, ChatGPT, etc.) and external tool sets.
- Open source and now governed by the **Linux Foundation** — Anthropic donated it to ensure open governance.

### The USB-C Port Analogy

Anthropic described MCP as *"the USB-C port for AI applications."*

Think of it this way:
- **USB-C** is a standard connector that any device can implement. Once you implement it, you can plug in any USB-C accessory — regardless of brand.
- **MCP** is the same idea for AI tools. Once an AI application implements MCP, it can use any MCP-compatible tool set — regardless of who wrote it or what it does.

This is what allows a single one-line command to give Claude Code an entirely new ability it did not have before.

### Why MCP Became a Big Deal

MCP was announced in **late 2024**, around the same time Claude Code was being developed. The key insight was:

> *If you could bolt any tool into Claude Code with a single command, and anyone could write tools using the same standard, you could unlock virtually unlimited capabilities.*

Before MCP, other frameworks like LangChain existed that connected tools to LLMs — but they required developers to write code using those specific frameworks. MCP is different because:
- It is a **standard**, not a framework.
- It is **widely adopted** — by Claude Code, ChatGPT, Cursor, and virtually every major AI tool.
- It has a **massive ecosystem** — tens of thousands of MCP servers have been written.
- As of early 2026, MCP has **100 million downloads per month**.

The reason people get so excited is simple: *one command → new ability*. That is the real magic.

### The Correct Way to Think About MCP

MCP is great, but it is important to keep it in perspective:

**What to be excited about:**
- The *tools themselves* — a tool that fetches live stock prices, or reads the latest API documentation, is genuinely valuable.
- The *one-line install* — you can add any tool with a single terminal command.
- The *ecosystem* — tens of thousands of tools are available.

**What NOT to confuse:**
- MCP itself is just the *connective tissue* — the interface standard. It is not the tools. The value is in what the tools *do*, not in MCP itself.
- MCP can still fill your context window — adding too many MCP servers loads tool descriptions into Claude's context. This has improved significantly with lazy-loading in 2026, but it remains something to manage.

---

### MCP Technical Architecture — Hosts, Clients & Servers

There are three components in the MCP architecture. You do not need to build any of these — but knowing the terms helps you read documentation and understand discussions.

| Term | What it Is | Examples |
|---|---|---|
| **MCP Host** | The overall AI application that needs to call tools. | Claude Code, ChatGPT, a custom agent app. |
| **MCP Client** | Code running *inside* the host — one per tool set being used. Handles the communication protocol. | Built into Claude Code, handled automatically. |
| **MCP Server** | The thing you actually care about. Manages a specific set of tools written by somebody else. | Context7 (API docs), Polygon/Massive (stock prices), GitHub, Slack, etc. |

> **In everyday conversation:** When someone says "I'm using this MCP," they almost always mean "I'm using this MCP *server*." The host and client are invisible plumbing.

---

### MCP Transport Modes — Local vs Remote

MCP servers can run in two different physical locations, called **transports**:

| Transport | Where the Server Runs | Example |
|---|---|---|
| **Local (stdio)** | On your own computer, as a local process. | Most MCP servers — installed via npm or pip and run locally. |
| **Remote (SSE / Streamable HTTP)** | On a cloud server, operated by the tool's creator. | Atlassian running Jira tools, GitHub running their own server. |

Two remote transport protocols exist:
- **SSE (Server-Sent Events)** — the original standard, now deprecated but still supported.
- **Streamable HTTP** — the new, preferred standard.

Both achieve the same result. The difference is only in the transport mechanism.

> **The vast majority of MCP servers are local.** They get installed on your machine (via npm or pip) and run as local processes.

---

### Common Misconceptions About Local MCP Servers

**Misconception 1: "A local MCP server isn't real MCP."**

Reality: A local MCP server is completely legitimate. The code was written by someone else and shared publicly. You installed it locally, but it is still shared code with all the benefits of MCP.

**Misconception 2: "If the MCP server runs locally, it doesn't connect to the internet."**

Reality: Where the MCP server *runs* has nothing to do with whether it makes network calls. A local MCP server for stock prices runs *on your computer*, but it absolutely makes web requests to fetch the stock data. The local/remote distinction is only about where the MCP server *process* runs — not about what it does internally.

---

## 4. Discovering MCP Servers — Marketplaces & Registries

One acknowledged weakness of MCP is that there is no single, universally adopted place to discover MCP servers. It is described as "a bit of a wild west." Here are the main options:

### Official MCP Registry

**URL:** `registry.modelcontextprotocol.io`

- The official website for the MCP standard.
- Has a registry of available servers.
- Tends to be quiet and not very active in practice.
- Useful for reference but not the best discovery experience.

---

### Anthropic's Reference MCP Servers on GitHub

Anthropic maintains a curated GitHub repository of reference MCP servers — some written by Anthropic in the early days, some by trusted third parties that have been "blessed" by Anthropic. This is a reliable starting point for commonly needed tools.

---

### MCP Marketplace Sites

These are the most active and useful places to discover MCP servers:

#### 1. MCP.so
- **URL:** `mcp.so`
- Lists approximately **17,000 MCP servers**.
- Searchable with keywords and tags.
- Includes comment sections (often empty).
- Contains significant noise — unofficial clones, duplicates, low-quality entries.

#### 2. Glamour.ai (Preferred)
- **URL:** `glamour.ai`
- Lists approximately **16,000 MCP servers**.
- Includes **quality ratings** (e.g., triple-A rated servers), download counts, and favourites.
- More curated and easier to evaluate quality.
- Provides direct links to GitHub repos for verification.
- Considered the more mature and trustworthy marketplace.

---

### How to Verify an MCP Server is Legitimate

Since marketplaces contain noise and unofficial clones, always verify before installing:

1. **Find the GitHub repository.** Every legitimate MCP server has a public GitHub repo. Find the link from the marketplace listing.
2. **Check the star count.** A high star count (e.g., 40,000+) is a strong signal of quality and adoption.
3. **Check recent activity.** If the repo has not been updated in two years, be cautious.
4. **Read open issues.** This gives a sense of whether the server is actively maintained and what known problems exist.
5. **Read the README.** Good MCP servers have clear documentation including specific Claude Code install instructions.

> **Example:** For Context7, the correct server is from **Upstash** (`upstash/context7`). The GitHub repo has 40,000+ stars and is updated regularly — clear signals of a trustworthy, well-maintained server.

---

## 5. Adding MCP Servers to Claude Code — Hands-On

### Installing Context7 — Live API Documentation

**What Context7 does:** Solves a common problem where Claude Code provides outdated API information based on its training cutoff. Context7 lets Claude look up *current* documentation for any library in real time.

**Step 1 — Find the install command**

From Glamour.ai or the GitHub repo (`upstash/context7`), find the Claude Code install command:

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

This command is run **outside Claude Code** in a regular terminal.

**Step 2 — Run the install command**

Exit Claude Code if running, paste the command into your terminal, and run it. Output will confirm:

```
Added to local config.
```

**Step 3 — Verify installation**

Start Claude Code and run `/context`. You should now see two new MCP tools listed:
- `resolve-library-id` — finds the ID for a given library name.
- `query-docs` — fetches the latest documentation using that ID.

These two tools use approximately **1,000 tokens** combined in the context window.

---

### Using Context7 in Claude Code

**Explicit use (recommended when you want to be certain):**
```
Use context7 to summarize the correct way to use the OpenAI Agents SDK 
with a model other than OpenAI's.
```

Using the word **`use`** followed by the MCP server name reliably tells Claude to use that specific server.

**What happens internally:**
1. Claude recognises it should use the `resolve-library-id` tool first.
2. It asks permission (unless you have auto-approved it).
3. It finds the correct library ID (e.g., "openai-agents-python").
4. It then uses `query-docs` to fetch the latest documentation.
5. It responds with accurate, up-to-date instructions.

**Implicit use (Claude figures it out on its own):**

In many cases, Claude will use Context7 automatically without being told:
```
How do I turn off telemetry with Crew AI?
```

If Context7 is installed and Claude recognises this as an API question, it will often use the server automatically. The `use` keyword is a reliable way to force this when needed.

---

### Installing Polygon IO — Market Data

**What Polygon IO (now rebranded as Massive) does:** Provides real-time and historical stock market data, futures, analysis, and much more.

**Requirement:** A free API key from polygon.io (free tier provides somewhat delayed data).

**Install command:**
```bash
claude mcp add massive -- npx @polygon-io/mcp MASSIVE_API_KEY=your_api_key_here
```

**After installation**, running `/context` shows a large number of new tools under "massive" covering stock snapshots, historical data, futures, and market analysis.

**Using it:**
```
What's the current share price of Apple?
```

Claude automatically selects the correct tool (`get-snapshot-ticker`), calls out to the Polygon cloud service, and returns the live share price — all within the Claude Code terminal.

---

### Context Window Efficiency — The New Lazy Loading Behaviour

A significant concern with MCP in its early days was context window pollution: installing many MCP servers loaded all their tool descriptions into context immediately, consuming thousands of tokens before any work was done.

**In 2026, Claude Code introduced lazy loading for MCP tools:**
- Claude Code only loads MCP tool descriptions into context *when it actually needs to use them*.
- All other tools remain "available but not loaded" — shown in `/context` as dark grey (available) vs. bright white (actively loaded).
- In the Massive demo, only the single tool Claude actually used was loaded: **156 tokens** instead of potentially thousands.

This makes MCP significantly more context-efficient than before, though being selective about which MCP servers you install remains good practice.

---

### Removing MCP Servers

```bash
# Remove Context7
claude mcp remove context7

# Remove Massive/Polygon
claude mcp remove massive
```

Run these from a regular terminal (outside Claude Code). Relaunch Claude Code and run `/mcp` to confirm:

```
/mcp
```

This shows all currently configured MCP servers. An empty list confirms successful removal.

---

## 6. MCP Pros and Cons — Summary

| Pros | Cons |
|---|---|
| Enormous ecosystem — tens of thousands of tools | Discovery is messy — multiple noisy marketplaces |
| Very flexible — tools can do virtually anything | Complex setup compared to Skills and Plugins |
| Widely adopted across all AI tools (universal standard) | Can still consume significant context window space |
| One-line install once you know the right server | Requires research to find the right, trustworthy server |
| Works for specialized, live-data tasks | Spawning separate server processes adds infrastructure overhead |

---

## 7. Skills — Claude Code's Simpler Way to Add Abilities

### What are Skills?

**Skills** are a newer, simpler alternative to MCP for extending Claude Code's capabilities. While MCP is about connecting to someone else's *running tool processes*, skills are about providing Claude Code with *instructions and scripts* packaged as plain markdown files.

The core idea: **just like `claude.md` gives Claude instructions about your project, a skill file gives Claude instructions about how to do a specific thing** — but you can have many of them, each self-contained.

### Key Advantages of Skills Over MCP

| Advantage | Explanation |
|---|---|
| **Simple to build** | Anyone can create a skill — just markdown files and optional shell scripts. No coding required. |
| **Context-efficient** | Uses *progressive disclosure* — only loads what is relevant, when it is relevant. |
| **Easy to share** | Just check the skill folder into your Git repo — teammates get the skill automatically when they pull. |
| **Clean and elegant** | No separate server processes, no complex infrastructure plumbing. Just files. |
| **Can run scripts** | Skills can include shell scripts that Claude can execute, giving them tool-like capabilities at a higher abstraction level. |

> *"When skills first came out, there was this collective sigh of relief — it just feels right."*

---

### Progressive Disclosure — The Core Concept

**Progressive disclosure** is the mechanism that makes skills context-efficient. The idea is simple:

Instead of loading the entire skill into context at once, Claude Code only loads each part of a skill *if it decides that part is relevant to the current task*.

Think of it as three nested levels:

```
┌──────────────────────────────────────────────┐
│  LEVEL 1: Metadata  (always loaded)          │
│  Name + one-line description (~tiny)         │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  LEVEL 2: Instructions (on demand)    │  │
│  │  Full workflow, guidance, snippets    │  │
│  │                                       │  │
│  │  ┌──────────────────────────────────┐ │  │
│  │  │  LEVEL 3: Resources & Scripts   │ │  │
│  │  │  (only if explicitly needed)    │ │  │
│  │  └──────────────────────────────────┘ │  │
│  └────────────────────────────────────────┘  │
└──────────────────────────────────────────────┘
```

At each level, Claude decides: *"Do I need to go deeper?"* If not, it stops — saving context space.

---

### The Three Levels of Progressive Disclosure

#### Level 1 — Metadata (Always Loaded)
- Just the **name** of the skill and a short **description** (one or two sentences).
- This tiny snippet is loaded for *every* skill at startup.
- Claude reads all metadata and decides: *"Is this skill relevant to what I'm being asked to do?"*
- If not relevant, it stops here and uses almost no context.
- Example: `name: juggling` / `description: This skill teaches how to juggle safely.`

#### Level 2 — Instructions (Loaded on Demand)
- The full instructions for the skill: workflows, guidance, code snippets, examples, step-by-step processes.
- Only loaded if Claude decides the skill is relevant to the current task.
- This is the main body of the `skill.md` file.
- Can reference Level 3 resources that Claude may also optionally load.

#### Level 3 — Resources and Scripts (Loaded on Further Demand)
- Separate files (additional markdown, reference documents, data files) and shell scripts.
- Referenced within the Level 2 instructions.
- Only loaded or run if Claude determines it specifically needs them.
- Scripts are particularly powerful here — they run as a separate process outside Claude's context. Only the output comes back, making them very context-efficient.

---

### File System Architecture — How Skills are Structured

Skills use a simple, convention-based folder structure. The term "file system architecture" just means *the naming convention that makes everything work automatically*.

#### Location of Skills

| Location | Effect |
|---|---|
| `~/.claude/skills/` (home directory) | **Global** — available across all your projects. |
| `<your-project>/.claude/skills/` (project directory) | **Local** — only available in this specific project. |

#### The Required Folder Structure

```
.claude/
└── skills/                        ← Must be named exactly "skills"
    ├── agent-browser/             ← One subfolder per skill
    │   ├── skill.md               ← Required: metadata + instructions
    │   ├── additional-docs.md     ← Optional: extra reference material
    │   └── scripts/               ← Optional: runnable scripts
    │       ├── browse.py
    │       └── screenshot.sh
    └── pdf-generator/             ← Another skill
        └── skill.md
```

**The rules:**
- The folder must be named **exactly `skills`** — no variations.
- Each subfolder is one skill.
- Each skill subfolder must contain a file named **`skill.md`**.
- All other files and subfolders are optional and only referenced if Claude decides it needs them.

---

### The skill.md File Format

The `skill.md` file uses **YAML front matter** (metadata at the top, between `---` delimiters) followed by standard **markdown instructions** below:

```markdown
---
name: my-skill-name
description: A brief description that Claude reads to decide if this skill is relevant.
version: 1.0.0
---

# My Skill — Full Instructions

## When to Use This Skill
Describe what this skill is for and when Claude should apply it.

## Step-by-Step Workflow
1. First, do this...
2. Then, do that...

## Additional Resources
- See [extra-docs.md](extra-docs.md) for more reference material.
- Run [scripts/process.py](scripts/process.py) for live data processing.
```

The YAML block is **Level 1** (metadata). Everything below it is **Level 2** (instructions). The referenced files are **Level 3** (resources and scripts).

---

### Global vs Project-Level Skills

| Scenario | Where to Install |
|---|---|
| A skill that applies to all your projects (e.g., "write good commit messages") | `~/.claude/skills/` — global |
| A skill specific to one project's workflow or architecture | `<project>/.claude/skills/` — local |
| A shared team skill everyone on the project should have | `<project>/.claude/skills/` — committed to Git |

---

### Sharing Skills with Your Team

This is one of the most compelling advantages of skills over MCP:

**To share a skill with your entire team, simply check the `.claude/skills/` folder into your Git repository.**

Every teammate who clones or pulls the repo immediately has the same skills available in their Claude Code — with zero additional setup required. There is nothing to install, no API key to configure, no command to run.

Compare this to MCP, where every team member must manually run the install command and potentially configure an API key.

---

### How Scripts Work in Skills

When Claude Code runs a script that is part of a skill:

1. Claude issues a shell command to execute the script.
2. The script runs as a separate process on your machine.
3. All the processing that happens *inside* the script stays completely **outside** Claude's context window.
4. Only the **final output** (what the script prints to stdout) is returned to Claude.

This is highly context-efficient: the script could perform 1,000 lines of computation, but only a few lines of output come back into Claude's context. This is described as *"off-boarding processing to the script itself."*

---

## 8. Skills Marketplaces — Where to Find Skills

The skills ecosystem is newer and less mature than MCP's. There are two good starting points:

### Anthropic's Official GitHub Skills Repo

Anthropic maintains an official GitHub repository of example and reference skills. Notable examples include:

| Skill | What it Does |
|---|---|
| **Skill Creator** | Helps you build new skills — a meta-skill for building skills. |
| **PPTX (PowerPoint)** | Enables Claude to create PowerPoint presentations. |
| **PDF Generation** | Enables Claude to generate PDF documents. |
| **Agent Browser** | Gives Claude the ability to launch and control a headless web browser. |

Each skill folder contains the `skill.md` file with YAML metadata, full markdown instructions, and supporting scripts.

---

### skills.sh — The Vercel Curated Marketplace

**URL:** `skills.sh`

A curated community skills marketplace built by Vercel. Allows you to discover and install skills with a single `npx` command. More polished and curated than a raw GitHub search — think of it as the Glamour.ai equivalent for skills.

---

### Installing the Agent Browser Skill Step-by-Step

The **Agent Browser** skill gives Claude Code the ability to launch and control a real web browser — automating navigation, clicking, form-filling, and data extraction.

**Step 1 — Find the skill on skills.sh**

Visit `skills.sh`, search for "Agent Browser," and copy the install command.

**Step 2 — Run the Vercel NPX installer**

```bash
npx skills@latest install
```

The interactive installer prompts:
1. **Which agent?** → Select `Claude Code`.
2. **Installation scope?** → Choose `project` (installs into `.claude/skills/` in the current project) or `global` (installs into your home directory).

**Step 3 — Files are created automatically**

```
.claude/
└── skills/
    └── agent-browser/
        ├── skill.md          ← Browser control instructions
        └── scripts/
            ├── browse.py     ← Python browser automation script
            └── ...
```

**Step 4 — Install browser dependencies**

```bash
pip install playwright
playwright install chromium
```

**Step 5 — Verify in Claude Code**

Launch Claude Code and run:
```
/skills
```

You should see `agent-browser` listed. The skill occupies only **68 tokens** at Level 1 — just the metadata. Extremely efficient.

---

### Agent Browser in Action

With Agent Browser installed, Claude Code can navigate the web autonomously:

```
Use agent-browser to search Resy and OpenTable for restaurant reservations 
for 2 people this Saturday downtown.
```

Claude will:
1. Recognise the browser skill is needed.
2. Load the full skill instructions (Level 2).
3. Run the browser script (Level 3).
4. Launch a headless Chromium browser instance.
5. Navigate to the requested sites, perform searches, and extract availability.
6. Return a summary of results to you in the terminal.

All of this happens without any browser window appearing on screen (headless mode).

---

## 9. Skills Pros and Cons — Summary

| Pros | Cons |
|---|---|
| Extremely context-efficient — progressive disclosure | Less flexible than full MCP tool calling |
| Simple to create — just markdown and optional scripts | Discovery is even less mature than MCP |
| Simple to share — just commit the folder to Git | Relies on Claude's language matching the skill metadata |
| Clean and elegant — no server infrastructure | Can be "hand-wavy" — sometimes Claude doesn't pick up the skill |
| Scripts run entirely outside context — highly efficient | Still an evolving ecosystem |
| Scoped globally or per-project | Not as precise as proper JSON function-calling tools |

---

## 10. Plugins — The Highest-Level Building Block

### What are Plugins?

**Plugins** are the newest and highest-level of the three building blocks. A plugin is a **pre-packaged bundle** that can contain any combination of:
- MCP servers
- Skills
- Slash commands
- Hooks (automated triggers — covered separately)
- Agents (standalone sub-agents with their own roles)
- And more

Think of a plugin as a complete, ready-to-use "feature expansion" for Claude Code — all decisions about what to use internally (MCP vs skills, etc.) have already been made by the plugin author. You just install it and use it.

**Introduced:** October 2025

**Important limitation:** Plugins currently only work with **Claude Code specifically** — not ChatGPT, Cursor, or other AI tools.

---

### What Can a Plugin Bundle Together?

| Component | Description |
|---|---|
| **MCP servers** | Full MCP tool sets, pre-configured and ready to use. |
| **Skills** | Markdown-based instruction packages for specific workflows. |
| **Commands** | New `/slash-commands` you can type to trigger specific behaviour. |
| **Hooks** | Automated triggers that fire on certain events (e.g., after Claude completes a task). |
| **Agents** | Standalone sub-agents with specialised roles (e.g., a dedicated code review agent). |

**You have already used a plugin:** The **Ralph Loop** from Day 2 was a plugin — it bundled a slash command (`/ralph-loop:ralph-loop`) along with the logic to run iterative autonomous coding loops.

---

### The Plugins Marketplace — Inside Claude Code

Access the plugins interface directly from within Claude Code:

```
/plugin
```

This opens a UI with three tabs:

| Tab | Purpose |
|---|---|
| **Discover** | Browse available plugins from all active marketplaces, sorted by install count (most popular first). |
| **Installed** | See which plugins are currently installed. Enable or disable them individually. |
| **Marketplaces** | Manage which marketplaces are active. By default, only the official Anthropic marketplace is linked. |

The **official Anthropic marketplace** is a GitHub repository (`claude-plugins-official` in Anthropic's GitHub). It contains:
- **Bundled plugins** — written and maintained by Anthropic.
- **External plugins** — written by trusted third parties and listed in the official repo.

---

### Installing Plugins Step-by-Step

1. Open Claude Code and run `/plugin`.
2. Navigate to the **Discover** tab.
3. Browse the list (sorted by most installs).
4. Press **Spacebar** to select or deselect plugins you want.
5. Press **`I`** to install all selected plugins.
6. Exit Claude Code: `Ctrl + C` twice.
7. Restart: type `claude` again.
8. New plugins are now active.

---

### Top Plugins to Know About

| Plugin | Install Count | What it Does |
|---|---|---|
| **Frontend Design** | Most popular | Creates distinctive, production-grade frontend interfaces. Widely praised by the community. |
| **Context7** | Very high | Wraps the Upstash Context7 MCP server for live API documentation lookup. Easier way to get Context7 than installing the MCP server directly. |
| **Code Review** | High | Anthropic's official agent for reviewing pull requests and code quality. |
| **GitHub** | High | Installs the official GitHub MCP server for interacting with GitHub issues, PRs, and repositories. |
| **Code Simplifier** | 51,000+ installs | Anthropic's *own internal* code simplification agent — the same tool used inside Anthropic. Removes "LLM slop" (overly complex or redundant code), improves clarity and maintainability. |
| **Ralph Loop** | Very high | The iterative autonomous coding loop plugin from Day 2. |

---

### Using a Plugin — Code Simplifier Demo

After installing the Code Simplifier plugin, invoke it with natural language:

```
Please use the code simplifier agent to simplify the entire code base.
```

**What Claude does:**
1. Recognises this maps to the `code-simplifier:code-simplifier` agent command.
2. Launches the Code Simplifier agent.
3. The agent runs for approximately 6 minutes across the entire codebase.
4. Makes targeted changes to reduce complexity and remove unnecessary constructs.
5. Runs all tests to verify nothing is broken.
6. Reports a summary of all changes made.

**Result:** A cleaner, more maintainable codebase with all tests still passing. The remarkable part: this is Anthropic's *own internal* tool — the same one they use themselves — now available as a public plugin.

> *"We don't even know how to install agents ourselves yet — but we know how to use plugins, and plugins can install agents for us."*

---

### Adding External or Team Marketplaces

You can add additional marketplaces beyond the default official one via the `/plugin` → Marketplaces tab:

- Provide a GitHub repository address containing a plugin manifest.
- Plugins from that source immediately appear in your Discover tab.

**Use cases:**
- **Company internal marketplace** — your organisation maintains private plugins for all developers.
- **Team marketplace** — a small team shares specialised plugins via a shared GitHub repo.
- **Trusted community marketplaces** — verified third-party plugin collections you want to add.

This system makes it straightforward to distribute tooling standards across a team — everyone can have an identical Claude Code setup.

---

## 11. Plugins Pros and Cons — Summary

| Pros | Cons |
|---|---|
| Simplest to install and use — browse, select, install | Only works with Claude Code (not other AI tools) |
| Bundles everything together — one install, multiple capabilities | Less control over exactly what gets installed internally |
| Explicit commands reduce uncertainty about whether Claude will use them | Broad brush — you install the whole package or nothing |
| Supports agents, hooks, and commands (beyond just tools) | Overuse can complicate your Claude Code setup |
| Proper in-app marketplace with ratings and discovery | Marketplace is relatively new — fewer options than raw MCP |
| Supports team and company private marketplaces | |

---

## 12. MCP vs Skills vs Plugins — The Complete Comparison

| Dimension | MCP | Skills | Plugins |
|---|---|---|---|
| **What it is** | A protocol for connecting to external tool processes | Markdown-based instructions and optional scripts | A bundled package of MCP servers, skills, commands, agents |
| **Introduced** | Late 2024 | Mid 2025 | October 2025 |
| **Works with** | Any AI tool (universal standard) | Started as Claude Code; now broader | Claude Code only |
| **Setup complexity** | Medium — one command, but research needed | Low — just create files and folders | Very low — browse and press install |
| **Context efficiency** | Medium — improved with lazy loading | High — progressive disclosure | Depends on what it bundles |
| **Flexibility** | High — tools can do virtually anything | Medium — limited to markdown and scripts | Low — pre-decided by plugin author |
| **Discovery** | Messy — noisy marketplaces | Even less mature than MCP | Clean — official in-app marketplace |
| **Sharing with team** | Manual — each person installs separately | Automatic — just commit the folder to Git | Automatic — everyone installs same plugin |
| **Can bundle agents?** | No | No | Yes |
| **Can run shell scripts?** | Via tool calls | Yes natively | Depends on contents |
| **Best for** | Specialized, live-data, granular tool needs | Team knowledge and workflow sharing | Everyday features, getting started quickly |

---

## 13. Decision Framework — Which One Do You Use?

Follow this priority order:

### Step 1 — Always Start with Plugins

> *"If there's a plugin that works for you, just use it. That is the simplest way."*

Check the `/plugin` discover tab first. If a plugin solves your need, install it. You do not need to worry about whether it uses MCP or skills internally — the plugin author made those decisions.

### Step 2 — Use MCP Directly When...
- You need a **specialized, live-data tool** (e.g., real-time stock prices, Jira tickets, GitHub API).
- The tool is **not available as a plugin**.
- You need the **full power and flexibility** of the specific tool's complete API.
- Example: The Polygon/Massive stock data server — likely no plugin equivalent; install the MCP server directly.

### Step 3 — Use Skills Directly When...
- You want to **share a custom workflow or knowledge base** with your team via Git.
- You find a skill in a marketplace (like skills.sh) that is not available as a plugin.
- You want to create your own skill — it is just markdown files, so anyone can do it.
- Example: The Agent Browser skill from skills.sh.

### The Decision Rule in One Line

```
Plugin available?          → Use the Plugin
No plugin, need tools?     → Use MCP directly
No plugin, need knowledge? → Use Skills directly
```

---

## 14. Key Takeaways — Day 3 Summary

### Conceptual Foundations
- **Tools are the real innovation** — everything else (MCP, Skills, Plugins) is just a delivery mechanism for tools.
- **MCP = protocol** — it is the interface standard, not the tools themselves. The value is in the specific tool sets.
- **Skills = files** — instructions and scripts packaged as a folder. Simpler than MCP, more efficient, easier to share.
- **Plugins = bundles** — the highest-level, simplest, Claude Code-specific way to add new capabilities.

### Command Quick Reference

| Action | Command |
|---|---|
| Browse plugins | `/plugin` → Discover tab |
| See installed plugins | `/plugin` → Installed tab |
| Add MCP server | `claude mcp add <name> -- <command>` (outside Claude) |
| Remove MCP server | `claude mcp remove <name>` (outside Claude) |
| See active MCP servers | `/mcp` (inside Claude) |
| See active skills | `/skills` (inside Claude) |
| Uninstall a skill | Delete its folder from `.claude/skills/` |
| Install plugin | `/plugin` → Discover → Spacebar to select → `I` to install |

### The Context Window Mindset
- **MCP** used to be a context hog — greatly improved with lazy loading but still worth managing.
- **Skills** are the most efficient — almost nothing is loaded until specifically needed.
- **Plugins** depend entirely on what they contain.
- Always run `/context` after installing new capabilities to see the impact on available context space.

### Team Collaboration Quick Guide
- **Skills in Git** → commit `.claude/skills/` → team gets the skill automatically on pull.
- **Plugins** → everyone installs the same plugin list → consistent Claude Code setup.
- **Custom marketplace** → add a team GitHub repo as a private plugin marketplace.

### The skill.md Structure — Quick Reference
```markdown
---
name: skill-name
description: One-line description Claude reads to decide relevance.
---

# Full Instructions
Everything Claude needs to know about this skill.

## Resources
See [extra.md](extra.md) for additional detail.
Run [scripts/process.py](scripts/process.py) for live output.
```

The YAML block = Level 1 (always loaded, tiny). Everything below = Level 2 (loaded on demand). Referenced files and scripts = Level 3 (loaded only when explicitly needed).

---

*End of Day 3 — Pro Week Notes*
