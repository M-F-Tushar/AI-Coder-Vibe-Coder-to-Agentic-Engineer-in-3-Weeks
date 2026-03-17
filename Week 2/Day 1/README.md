# Day 1 — Pro Week: From Vibe Coding to Vibe Engineering & Claude Code

> **Course Overview:** This is Week 2 ("Pro Week") of an AI-assisted coding course. The focus shifts from casual AI coding to professional, accountable, production-grade development using Claude Code and related CLI tools.

---

## Table of Contents

1. [Welcome to Pro Week — The Mindset Shift](#1-welcome-to-pro-week--the-mindset-shift)
2. [The 8 Stages of AI Coding Evolution](#2-the-8-stages-of-ai-coding-evolution)
3. [Three Types of Coding Workflows](#3-three-types-of-coding-workflows)
4. [From Vibe Coding to Vibe Engineering](#4-from-vibe-coding-to-vibe-engineering)
5. [What Vibe Engineering Demands — Simon Willison's Key Points](#5-what-vibe-engineering-demands--simon-willisons-key-points)
6. [The Rise of Claude Code — History & Timeline](#6-the-rise-of-claude-code--history--timeline)
7. [Claude Code Pricing & Plans](#7-claude-code-pricing--plans)
8. [Installing Claude Code](#8-installing-claude-code)
9. [Claude Code in VS Code — Two Modes Explained](#9-claude-code-in-vs-code--two-modes-explained)
10. [Getting Started with Claude Code CLI](#10-getting-started-with-claude-code-cli)
    - [Launching Claude Code](#launching-claude-code)
    - [The `/login` Command](#the-login-command)
    - [The `/init` Command — Setting Up Claude.md](#the-init-command--setting-up-claudemd)
    - [The `/context` Command — Monitoring Context Window](#the-context-command--monitoring-context-window)
    - [Context Compaction — `/compact`](#context-compaction--compact)
    - [The `/status` Command](#the-status-command)
11. [Running Tests with Claude Code](#11-running-tests-with-claude-code)
12. [Code Review with Claude Code](#12-code-review-with-claude-code)
    - [Triggering a Code Review](#triggering-a-code-review)
    - [Understanding Claude's Hallucinations — A Critical Warning](#understanding-claudes-hallucinations--a-critical-warning)
    - [Acting on the Code Review](#acting-on-the-code-review)
    - [Refactoring a Monolithic File](#refactoring-a-monolithic-file)
13. [OpenCode — Free Model Alternative to Claude Code](#13-opencode--free-model-alternative-to-claude-code)
    - [What is OpenCode?](#what-is-opencode)
    - [Installing OpenCode](#installing-opencode)
    - [Switching Models in OpenCode](#switching-models-in-opencode)
    - [Free Open-Source Models Available](#free-open-source-models-available)
    - [Connecting to Other Providers](#connecting-to-other-providers)
    - [Plan Mode vs Build Mode](#plan-mode-vs-build-mode)
14. [AMP Code — Ads-Funded Free CLI Agent](#14-amp-code--ads-funded-free-cli-agent)
    - [What is AMP?](#what-is-amp)
    - [Installing and Logging In](#installing-and-logging-in)
    - [AMP's Unique Features](#amps-unique-features)
    - [AMP Free Plan — Cost Breakdown](#amp-free-plan--cost-breakdown)
15. [Claude Code with OpenRouter (Custom Provider Setup)](#15-claude-code-with-openrouter-custom-provider-setup)
    - [Why Use OpenRouter with Claude Code?](#why-use-openrouter-with-claude-code)
    - [Environment Variables to Configure](#environment-variables-to-configure)
    - [Launching Claude Code with a Custom Model](#launching-claude-code-with-a-custom-model)
16. [Claude Code with Ollama (Running Models Locally)](#16-claude-code-with-ollama-running-models-locally)
    - [Requirements for Local Models](#requirements-for-local-models)
    - [Setting Up Claude Code + Ollama](#setting-up-claude-code--ollama)
17. [Tool Comparison Summary](#17-tool-comparison-summary)
18. [Key Takeaways & Best Practices](#18-key-takeaways--best-practices)

---

## 1. Welcome to Pro Week — The Mindset Shift

Week 2 is called **"Pro Week"** — a deliberate step up in depth, discipline, and professionalism compared to Week 1.

- Week 1 was about learning the fundamentals of AI-assisted coding — using AI like a power user.
- Week 2 is about becoming a **Vibe Engineer** — someone who is highly productive with AI tools but remains **fully accountable** for the code they ship.

The central theme of the entire week is **Claude Code**, which will also remain a major focus in Week 3. Other tools like OpenCode and AMP Code are also introduced as alternatives.

---

## 2. The 8 Stages of AI Coding Evolution

The course references **Steve Yegge's 8-stage model** describing how developers evolve in their use of AI for coding:

| Stage Range | Description |
|---|---|
| Stages 1–4 | The basics — using tools like ChatGPT for coding help. This was the focus of **Week 1**. |
| **Stage 5** | The main focus of **Week 2** — disciplined, agentic coding with professional oversight. |
| Stages 6–8 | Advanced orchestration — multi-agent systems, parallel workloads, automation pipelines. The focus of **Week 3**. |

> **Key idea:** You are not just trying to use the most powerful tool possible. You are trying to move through these stages deliberately, learning what each level of maturity demands from you as an engineer.

---

## 3. Three Types of Coding Workflows

Three major workflows were identified based on risk tolerance, project type, and the kind of code being written:

### Workflow 1 — Mission-Critical / Professional (Plan → Execute → Review → Test)
- Used for: large codebases, highly innovative code, latest libraries, production systems.
- Approach: write a detailed spec first, drive the process carefully, trust but verify every change.
- Mindset: slow, deliberate, accountable.

### Workflow 2 — MVP / Rapid Build (YOLO / Ralph Loops)
- Used for: new projects, boilerplate front-end, low-risk experiments, MVPs with risk appetite.
- Approach: be bold, move fast, automate heavily.
- Mindset: iterate quickly, accept imperfection early.

### Workflow 3 — Multi-Agent Orchestration
- Used for: very complex workflows that require multiple agents working in parallel.
- Focus of **Week 3**.

> **The Responsibility Principle:** Regardless of the workflow, *you* are accountable for the code you deliver. Using an LLM does not transfer responsibility. You must verify, test, and own every line of code that ships.

---

## 4. From Vibe Coding to Vibe Engineering

### What is Vibe Coding?
"Vibe coding" is a term for the **fast, loose, irresponsible** way of building software with AI — prompt-driven development where you don't pay attention to how the code actually works. You just prompt and accept results.

### What is Vibe Engineering?
The term **"Vibe Engineering"** was coined by **Simon Willison** (AI engineer and writer) to describe the *other end of the spectrum*:

> *What do we call it when seasoned professionals accelerate their work with LLMs whilst proudly and confidently staying accountable for the software they produce?*

He proposes: **Vibe Engineering.**

It is:
- Highly productive and effective.
- Making full use of AI to dramatically expand capability.
- But maintaining **full accountability** for code quality.
- Bulletproof in process — not sloppy or reckless.

This is the professional standard the course is now targeting.

---

## 5. What Vibe Engineering Demands — Simon Willison's Key Points

From Willison's blog post (recommended reading — link in course resources), these are the skills and practices that separate vibe engineering from vibe coding:

### Technical Practices
- **Automated testing** — Build testing into the process from the start, not as an afterthought.
- **Planning in advance** — Write specs and plan steps before running the agent.
- **Comprehensive documentation** — Keep docs up-to-date as code evolves.
- **Good version control habits** — Use Git checkpoints frequently.
- **Highly effective automation** — Use agentic loops and automation wherever reliable.

### Oversight & Review Practices
- **Code review culture** — Always have the LLM review its own work. This is described as *so powerful* and something the course has already practiced.
- **Really good manual QA** — Automated tests are not enough; manual spot-checking matters.

### Soft Skills & Judgment
- **Strong research skills** — When you hit a blocker, step back and try a completely different approach rather than bashing against a wall.
- **Ability to ship a preview** — Know when something is good enough to present.
- **Instinct for what to delegate to AI and what not to** — For example: front-end code is highly AI-delegatable; back-end logic and LLM integration often needs more human oversight.
- **Realistic project estimation** — AI tools make some tasks feel incredibly fast, creating a false sense of speed. Then you hit a wall and lose hours. Factor both into estimates.

### The "Weird Management" Problem
Getting good results from coding agents *feels uncomfortably close to managing a human collaborator* — but with key differences. The agent *will cheat* (take shortcuts, hallucinate, skip steps) if given the chance. Much time must be spent on code review.

> *"If you're going to really exploit these capabilities, you need to be at the top of your game."* — Simon Willison

---

## 6. The Rise of Claude Code — History & Timeline

| Date | Event |
|---|---|
| **Late 2024** | **Boris Cherny**, an engineer at Anthropic, starts a side project originally called *Claude CLI* to drive coding with Claude in an agent loop. |
| **February 2025** | Claude Code becomes available to most users for the first time. |
| **April 2025** | Anthropic officially releases Claude Code — the **first CLI coding agent tool that truly took hold** in the industry. |
| **Mid-2025** | Claude Code ecosystem expands rapidly during the year. |
| **September 2025** | **V2** is released, bringing a robust, mature ecosystem including: checkpointing, sub-agents, hooks, skills, background tasks, and the Claude Code SDK. |
| **November 2025** | Anthropic releases **Claude Opus 4.5** — widely seen as an **inflection point** in agentic coding. Many engineers reported that reliability improved so much they no longer needed to check every diff. |
| **Late 2025** | Google releases **Gemini 3 Pro** and OpenAI releases **GPT-5.2 Codex** — both entering the same elite tier as Opus 4.5. |
| **~Late 2025** | Anthropic passes **$1 billion ARR** from Claude Code — a major commercial milestone. |
| **January 2026** | Anthropic releases **Code Work** — extending the Claude Code concept beyond coding to other types of work. |
| **Early 2026** | Heavy hype around **OpenClaw** — an open-source co-working tool inspired by Claude Code's general approach. |

### MCP (Model Context Protocol) — A Parallel Revolution
- MCP was launched in late 2024 alongside Claude Code.
- It now has **100 million downloads per month**.
- MCP is a core part of the Claude Code ecosystem and will be covered in depth later in the course.

---

## 7. Claude Code Pricing & Plans

Claude Code runs on top of a **Claude.ai subscription**. There are several tiers:

| Plan | Monthly Cost | What it Includes |
|---|---|---|
| **Free** | $0 | Basic Claude chat — does NOT include Claude Code. |
| **Pro** | ~$20/month | Access to Claude Code in the web and in the terminal. Recommended entry point. |
| **Max** | $100/month | Higher usage limits with Claude Code. |
| **Max (Heavy)** | $200/month | Maximum limits — for power users who run Claude Code all day. The instructor uses this plan. |

> **Note:** You do NOT have to pay. Free and cheap alternatives (OpenCode, AMP Code, OpenRouter) are covered later in this lesson. However, the **paid Claude experience is noticeably better** in terms of model quality and reliability. If there's one investment to consider for this course, the Pro plan at $20/month is suggested as a strong value.

---

## 8. Installing Claude Code

### Step 1 — Create a Claude Account
1. Go to [claude.ai](https://claude.ai).
2. Click "Start Free" or "Try Claude."
3. Sign up with Google credentials or email.
4. Upgrade to a Pro plan if desired.

### Step 2 — Get the Install Command
1. Go to [code.claude.com](https://code.claude.com) — this redirects to the Claude Code website.
2. The website detects your OS and shows the correct installation command.
3. Copy the command to your clipboard.
4. For full documentation, click the docs link on the same page.

### Step 3 — Run the Install Command
1. Open **VS Code**.
2. Open a terminal: `Ctrl + `` `` ` (backtick) on Windows/Linux, or `Cmd + J` / `Ctrl + J`.
3. Paste the install command and press Enter.
4. Claude Code will install. You should see a success message with the version number (e.g., `v2.1.29`).

> **Windows Permission Note:** If you get a permissions error about running scripts, Google "allow PowerShell scripts Windows" — this is a standard, safe Windows setting to adjust.

### Step 4 — Install the VS Code Extension (Optional but Recommended)
1. Open Extensions: `Ctrl + Shift + X` (Windows) / `Cmd + Shift + X` (Mac).
2. Search for **"Claude Code"**.
3. Install the extension from Anthropic (verified with a checkmark).

---

## 9. Claude Code in VS Code — Two Modes Explained

Once installed, there are **two different ways** to use Claude Code inside VS Code:

### Mode 1 — Sidebar Extension (Beginner-Friendly)
- Access: Click the **Claude icon** in the VS Code sidebar.
- Experience: Similar to GitHub Copilot Chat or Codex — a visual chat panel baked into the IDE.
- Controls VS Code well (can open files, navigate tabs, etc.).
- **Limitation:** A more packaged, constrained experience. Not all pro features are available.
- Best for: Week 1 style of working — conversational, guided.

### Mode 2 — Terminal CLI (Pro / Full-Featured) ✅ *Used in this course*
- Access: Open a VS Code terminal and type `claude`.
- Experience: An intentionally retro, raw, text-based CLI interface.
- Has access to **all pro features** of Claude Code.
- Still aware it's running inside VS Code, so it can drive file changes and show diffs in the editor.
- Best for: Vibe Engineers — the full professional experience.

> **Why the terminal?** The CLI version is the complete, unpackaged tool. It gives you checkpoints, sub-agents, hooks, compaction, and all advanced features. The sidebar is essentially a beginner wrapper around a subset of these capabilities.

---

## 10. Getting Started with Claude Code CLI

### Launching Claude Code
In a VS Code terminal, navigate to your project folder and type:

```bash
claude
```

This launches the Claude Code CLI. You'll see a retro text-based interface — this is intentional. The raw, old-school aesthetic reflects its philosophy: direct, native LLM interaction.

---

### The `/login` Command

If this is your first time using Claude Code, you need to authenticate:

```
/login
```

This opens a web browser for you to log in with your Anthropic account credentials. After logging in, you return to the terminal — you are now authenticated.

> If you plan to use free models instead, skip this for now and continue to the OpenCode/AMP sections.

---

### The `/init` Command — Setting Up Claude.md

Claude Code does not use the `agents.md` file used in Week 1. It uses its own file called **`claude.md`**.

To let Claude set itself up automatically:

```
/init
```

**What happens:**
- Claude scans your entire project directory.
- It reads any existing agent documentation files (like `agents.md`).
- It generates a `claude.md` file with a project overview, commands, and development guidelines.
- It shows you a diff of the file it wants to create in VS Code.
- You choose to accept or reject:
  - `1` — Yes, apply this edit.
  - `2` — Yes, and allow all edits for this session (shortcut: `Shift + Tab`).
  - `3` — No, reject this edit.
  - `Tab` — Accept but add comments/modifications.

> **⚠️ Important Recommendation:** Do NOT rely solely on `/init` to write your `claude.md`. Just as with `agents.md`, it is **your job** to write this file carefully. You can use `/init` to generate a first draft and then improve it manually. The `claude.md` file is the most critical human-supervised element for getting good results.

---

### The `/context` Command — Monitoring Context Window

```
/context
```

This shows a **visual breakdown** of how much of Claude Code's context window is being used:

| Segment | Meaning |
|---|---|
| **Memory (purple-ish)** | Space used by `claude.md` and other loaded files. |
| **Messages (purple)** | Space used by the conversation history so far. |
| **Free space** | What's available for more interactions. |
| **Buffer** | Reserved space Claude keeps to perform compaction smoothly. |

**Key fact:** Claude Code has a **200,000 token context window**. This fills up faster than you might expect — just a few commands can consume a meaningful portion.

> **Pro tip:** Run `/context` regularly to keep a healthy eye on usage. Start a big task only when you have plenty of room.

---

### Context Compaction — `/compact`

When context fills up, Claude Code performs **compaction** — compressing the conversation history into a shorter summary while keeping the most important information.

**Auto compaction:** Claude will do this automatically when it approaches the buffer zone. However, it might happen mid-task (e.g., while rewriting code), which can cause interruptions.

**Manual compaction (recommended):**

```
/compact
```

Optional — add instructions for how to summarize:

```
/compact focus on the refactoring decisions and test results
```

**Best practice:** Run `/compact` manually at the end of a major task, before you start the next one. This ensures:
- You have a clean, empty context.
- Compaction doesn't interrupt ongoing work.
- You are in control of what gets summarized.

> **Warning:** After compaction, some details from earlier conversation are lost. Claude may repeat mistakes it already made (e.g., incorrectly claiming a `.env` file is exposed in Git). To mitigate this, update `claude.md` with any crucial information you don't want forgotten.

---

### The `/status` Command

```
/status
```

Shows a 3-page status panel (navigate with left/right arrow keys):

| Page | Contents |
|---|---|
| **Status** | Version, session ID, login method, active model. |
| **Config** | Configuration settings for the session. |
| **Usage** | How much of your daily/weekly token allowance you've used (e.g., "7% of daily allowance"). |

Press `Escape` to exit the status screen.

---

## 11. Running Tests with Claude Code

Once Claude Code is set up and `claude.md` is in place, a good first command is to have Claude run all your tests:

```
Please run all tests to confirm everything is working. Bring up the server as needed and bring it down at the end.
```

**What Claude does:**
- Asks for permission before running commands like `docker build` (you choose `1` for yes once, or `2` for yes and don't ask again for this type of command).
- Detects if required services aren't running (e.g., Docker) and attempts to start them automatically.
- Runs backend and front-end tests.
- Reports results with a summary table in the terminal.

> **Observation:** More powerful models (like Opus 4.5) handle edge cases like launching Docker Desktop automatically — something earlier, weaker models like Sonnet struggled with.

---

## 12. Code Review with Claude Code

### Triggering a Code Review

To get a comprehensive code review of the entire project:

```
Please carry out a comprehensive code review of the entire repo and write a report with actions to code-review.md in the docs folder.
```

**What Claude does:**
- Spawns **multiple parallel sub-agents** — e.g., a "Backend Code Quality" agent, a "Front-End" agent, and an "Infrastructure & Config" agent — running simultaneously.
- Each agent reads and analyzes different parts of the codebase.
- Results are compiled into a structured markdown report.

---

### Understanding Claude's Hallucinations — A Critical Warning

During the code review demo, Claude reported a **critical false positive**:

> *"Rotate OpenRouter API key — it's exposed in Git. Remove `.env` from Git history."*

This was **completely false**. The `.env` file was properly included in `.gitignore` and was never committed.

**What happened:**
- One of Claude's exploration sub-agents read the `.env` file locally on disk.
- It incorrectly concluded the file was tracked by Git.
- It reported this finding with extreme confidence in strongly worded language.

**The response and correction:**
- The instructor pushed back: *"How is `.env` in Git? It's clearly in `.gitignore`."*
- Claude immediately acknowledged the error: *"You're right. Let me verify. The file exists locally but is properly Git-ignored. I'll correct the review."*

**Lesson: The Hallucination Pattern**
- LLMs can state false information with full confidence using authoritative language.
- This is dangerous because readers (including other developers) may accept it without questioning.
- The telltale sign is overly confident, strongly worded statements — especially about things that are easy to verify.
- **Always verify critical findings before acting on them.**
- **You are the human supervisor. Your job is to catch these.**

> *"Everything has to be checked."* — This is the most important lesson from the code review section.

---

### Acting on the Code Review

After reviewing the code review report, you can instruct Claude to fix everything:

```
Please go ahead and address all the critical, high, and medium priority issues. Retest everything and let me know when everything is remediated and tests pass.
```

**Example findings Claude may identify:**

| Priority | Issue |
|---|---|
| Critical | Unpinned backend dependencies |
| High | Playwright test hard-coded to Mac only |
| High | Potential SQL injection risk |
| High | Missing input validation |
| High | Monolithic Python module (everything in one file) |
| Medium | Docker health check missing |
| Medium | Docker runs as root |
| Low | Missing docstrings |
| Low | No-doc strings on SQL functions |

Claude will fix these and re-run all tests, reporting a pass/fail summary.

---

### Refactoring a Monolithic File

In one interesting case, Claude decided **on its own** to defer restructuring the monolithic `main.py` file — judging that the cost-benefit ratio didn't justify the change given the amount of refactoring required.

This is a double-edged behaviour:
- On one hand, it shows intelligence and autonomy — it's not blindly following instructions.
- On the other hand, it's disobeying you, and you may genuinely want that refactoring done.

**The right response:** Come back and be explicit:

```
I really want to remediate the monolithic Python module. Please fix main.py now, organize it into modules and packages as appropriate, and retest everything.
```

**Result of refactoring `main.py`:**
- A lightweight, clean `main.py` entry point.
- Separate modules for: `config`, `models`, `database`, `AI`, `dependencies`.
- Individual route files for each area of the API.
- All 23 backend tests passed. All front-end tests passed.
- Documentation was updated automatically without being asked.

**After finishing — commit your changes:**

```bash
git add .
git commit -m "Claude code code review fixes"
```

---

## 13. OpenCode — Free Model Alternative to Claude Code

### What is OpenCode?

**OpenCode** ([opencode.ai](https://opencode.ai)) is an **open-source competitor** to Claude Code. Key characteristics:
- Not affiliated with any specific AI provider.
- Can connect to free models, paid models, or local models.
- Supports Claude, GPT, Gemini, and many others.
- Great option for people who don't want to pay for Anthropic's subscription.

---

### Installing OpenCode

OpenCode is installed via **npm** (Node.js package manager):

```bash
# macOS / Linux
curl [install command from opencode.ai]

# Windows (with Chocolatey)
choco install opencode

# Universal (npm)
npm install -g opencode
```

After installation, navigate to your project folder and type:

```bash
opencode
```

---

### Switching Models in OpenCode

Use the slash command:

```
/models
```

This opens a model picker showing all models available from connected providers. You can scroll through and select the model you want.

---

### Free Open-Source Models Available

OpenCode provides access to several powerful **free open-source models** through their "OpenCode Zen" set:

| Model | Origin | Notes |
|---|---|---|
| **GLM 4.7** | Zhipu AI (China) | Highly capable open-source model; very popular in the community. |
| **Kimi K2 / K2.5** | Moonshot AI (China) | Considered one of the most powerful open-source models available at the time of recording. |
| **MiniMax** | MiniMax AI | Another strong open-source contender. |

> **Free model limitations:** There is no hard quota, but heavy usage may trigger **rate limiting** — requests may slow down or fail with an error. Availability of free models may change over time.

---

### Connecting to Other Providers

Use the command:

```
/connect
```

This shows all the providers you can connect to:

- **OpenCode Zen** — Default free models (already connected).
- **OpenAI** — Automatically detected if you have an OpenAI subscription.
- **Anthropic** — Connect via Claude Max subscription or API key.
- **GitHub Copilot** — Connect via your GitHub credentials.
- **Google** — Connect via your Google account.
- **OpenRouter** — Provide your OpenRouter API key.
- **Azure / AWS Bedrock** — Enterprise cloud options.
- **LM Studio / Ollama** — For running models locally on your own machine.

---

### Plan Mode vs Build Mode

OpenCode has two agent modes, toggled with the **`Tab`** key:

| Mode | Behaviour |
|---|---|
| **Plan Mode** | Claude thinks and produces a plan but does NOT write or edit any files. Use this to review intentions before acting. |
| **Build Mode** | Claude acts — writes code, edits files, runs commands. |

**Best practice workflow:**
1. Start in **Plan Mode** — review what the agent intends to do.
2. Switch to **Build Mode** — let it execute once you're satisfied with the plan.

---

## 14. AMP Code — Ads-Funded Free CLI Agent

### What is AMP?

**AMP** ([amp.dev](https://amp.dev) / [ampcode.com](https://ampcode.com)) is another agentic coding CLI tool that:
- Works similarly to Claude Code and OpenCode.
- Is **not affiliated with any specific AI provider**.
- Available as a terminal CLI and as extensions for VS Code, Cursor, and Windsurf.
- Offers a unique **ads-funded free tier**.

---

### Installing and Logging In

```bash
# Install (paste command from ampcode.com)
[curl or npm install command]

# Launch
amp
```

**First-time login:**
1. AMP prompts you to log in.
2. A browser window opens — sign up with email/password or Google/GitHub OAuth.
3. Return to the terminal — you are now logged in and AMP is ready.

---

### AMP's Unique Features

#### Ads at the Top
AMP displays an **ad at the top of the interface** — this is how you "pay" for your free usage. The tech community initially reacted strongly against this, but the general assessment is that it's a reasonable trade-off for $10 of free model credits per day.

#### Model Selection is Automatic
Unlike Claude Code and OpenCode, **you don't choose your model** in AMP. AMP selects the best available model for the task behind the scenes. Based on context window sizes visible in the interface, AMP appears to use high-end frontier models (likely OpenAI models).

#### Reasoning Modes
Toggle with `Ctrl + S`:

| Mode | Description |
|---|---|
| **Smart** | Standard mode — balanced speed and reasoning. |
| **Deep** | Slower, more thorough thinking. Recommended for complex tasks. |
| **Rush** | Fast, lighter thinking. Best for simple quick tasks. |

---

### AMP Free Plan — Cost Breakdown

- You receive **$10 of model credit per day** in exchange for viewing ads.
- Credits reset daily.
- You can see your remaining balance at: `ampcode.com → Avatar → Settings`.
- Example from demo: A full project code review cost approximately **$0.42** out of the $10 daily allowance.
- You can also **purchase additional credits** or set up automatic top-ups from the Settings page.
- GitHub credentials can be connected for authentication.

---

## 15. Claude Code with OpenRouter (Custom Provider Setup)

### Why Use OpenRouter with Claude Code?

By default, Claude Code sends all requests to **Anthropic's API** (Claude models). However, you can **redirect** these calls to **OpenRouter** instead, allowing you to use different models (including free or cheaper ones) through the same Claude Code interface.

> **⚠️ Important Caveat:** This is **not** the experience Anthropic designed Claude Code for. The tooling is optimized for Claude models. Expect a **"janky" experience** — some things will work well, others may not. **For open-source models, OpenCode or AMP are generally recommended instead.** This setup is for experimentation only.

---

### Environment Variables to Configure

Before launching Claude Code, set these environment variables in your terminal:

```bash
# Load your .env file (macOS)
source .env

# Set all three model tiers to your chosen model
export ANTHROPIC_DEFAULT_HAIKU_MODEL="moonshotai/kimi-k2"
export ANTHROPIC_DEFAULT_SONNET_MODEL="moonshotai/kimi-k2"
export ANTHROPIC_DEFAULT_OPUS_MODEL="moonshotai/kimi-k2"

# Redirect Anthropic's base URL to OpenRouter
export ANTHROPIC_BASE_URL="https://openrouter.ai/api"

# Use your OpenRouter API key instead of Anthropic's
export ANTHROPIC_AUTH_TOKEN="your_openrouter_api_key_here"

# Clear the Anthropic key so it doesn't get used
export ANTHROPIC_API_KEY=""
```

> **Why set all three tiers to the same model?** If you only set one tier, Claude Code may fall back to using an actual Claude model for the other tiers. Setting all three to the same model ensures everything goes through OpenRouter.

---

### Launching Claude Code with a Custom Model

```bash
claude --model moonshotai/kimi-k2
```

Use the exact model string from OpenRouter's model listing.

**Verifying it worked:**
- Inside Claude Code, type `/model` to see the active model.
- You can also check your **OpenRouter Activity page** (avatar → Activity) to see recent API calls and confirm the model being used.

---

## 16. Claude Code with Ollama (Running Models Locally)

### Requirements for Local Models

Running a model locally via Ollama requires **significant hardware**:

| Requirement | Details |
|---|---|
| **Minimum RAM** | 64 GB GPU RAM (or 64 GB unified RAM on Apple Silicon Macs). |
| **Recommended model size** | At minimum a model equivalent to GPT-style 120B+ parameters. A 20B model is not powerful enough for real coding tasks. |
| **Software** | Ollama must be installed and running on your local machine. |

> Most consumer laptops and desktops do not meet these requirements. If you don't have the hardware, use OpenRouter for cheap/free cloud models instead.

---

### Setting Up Claude Code + Ollama

```bash
# Set model tiers to a local model (e.g., GPT OSS running via Ollama)
export ANTHROPIC_DEFAULT_HAIKU_MODEL="gpt-oss"
export ANTHROPIC_DEFAULT_SONNET_MODEL="gpt-oss"
export ANTHROPIC_DEFAULT_OPUS_MODEL="gpt-oss"

# Point to local Ollama server
export ANTHROPIC_BASE_URL="http://localhost:11434"
```

Launch Claude Code:

```bash
claude --model gpt-oss
```

**Verifying local model usage:**
- Type `/model` inside Claude Code to confirm the active model.
- Monitor your GPU usage — you should see it running at or near 100% while the model generates a response.

**Resetting to default (Claude + Anthropic):**
Simply close the terminal and open a new one — environment variables are cleared when the session ends. Claude Code will revert to using Anthropic's models.

---

## 17. Tool Comparison Summary

| Feature | Claude Code | OpenCode | AMP Code |
|---|---|---|---|
| **Provider** | Anthropic (official) | Open source / any provider | Independent / any provider |
| **Best model quality** | ⭐⭐⭐⭐⭐ (Opus 4.5) | ⭐⭐⭐ (depends on model) | ⭐⭐⭐⭐ (auto-selected frontier) |
| **Cost** | $20–$200/month (Claude subscription) | Free (with free models) | Free ($10/day with ads) |
| **Free models** | No (unless custom setup) | Yes (GLM 4.7, Kimi K2, MiniMax) | Yes (auto-selected, ad-supported) |
| **Model switching** | No (Claude only, unless custom) | Yes (easy `/models` command) | No (automatic) |
| **Context window tracking** | `/context` command | Shown in UI (%) | Shown in UI (%) |
| **Compaction** | `/compact` command | Built-in | Built-in |
| **Plan/Build mode** | No explicit toggle | Yes (`Tab` key) | Implicit (Deep/Smart/Rush modes) |
| **Sub-agents / parallel** | Yes (built-in) | Depends on model | Depends on model |
| **Best for** | Professional daily use | Free/flexible experimentation | Quick free experiments |
| **Recommended by instructor** | ✅ Primary tool | ✅ Alternative | ✅ For free experimentation |

---

## 18. Key Takeaways & Best Practices

### On Mindset
- You are a **vibe engineer**, not a vibe coder. The difference is accountability.
- AI expands your capability — it does not replace your judgment.
- You are responsible for every line of code that ships.

### On Claude Code Setup
- Always write your own `claude.md` — don't fully delegate it to `/init`.
- Run `/context` regularly to avoid running out of context mid-task.
- Use `/compact` manually at the end of major tasks, not in the middle.
- Use `/status` to check model, version, and daily usage limits.

### On Code Review
- Always run a code review before and after major changes.
- **Never blindly trust the results.** Always verify critical findings (especially security-related ones).
- Hallucinations happen with great confidence. The human eye is the last line of defense.
- Push back when something seems wrong — Claude will acknowledge and correct errors.

### On Model Choice
- For professional work: **Claude Code + Opus 4.5** is the gold standard.
- For free experimentation: **OpenCode with GLM 4.7 or Kimi K2** is the best starting point.
- For ads-funded free tier with frontier-quality models: **AMP Code**.
- For custom model routing: Use environment variables to redirect Claude Code to OpenRouter or Ollama.

### On Estimation and Hype
- AI can produce boilerplate very fast — creating a **false sense of speed**.
- Complex or novel problems can still take hours to solve.
- Don't get swept up in "10X productivity" hype — factor in the walls you'll inevitably hit.
- The efficiency gain is real and significant, but it is not magic.

### Git Hygiene
- Always run `git add . && git commit -m "..."` after a major Claude-assisted change.
- Claude will not commit for you by default — that's your job.
- Use commit messages that describe what Claude did (e.g., `"Claude code code review fixes"`).

---

*End of Day 1 — Pro Week Notes*
