# Claude Code — Week 3, Day 3: Complete Study Guide
### Large Codebases, Best Practices, Claude Agent SDK, Cowork & OpenClaw

---

## Table of Contents

1. [Day 3 Overview & Structure](#1-day-3-overview--structure)
2. [Full Recap: All Pro Features Covered So Far](#2-full-recap-all-pro-features-covered-so-far)
3. [Day 2 Recap: Sandboxing & Remote Execution](#3-day-2-recap-sandboxing--remote-execution)
4. [Live Demo: Zero-Shot Market Data Terminal App](#4-live-demo-zero-shot-market-data-terminal-app)
5. [Best Practices for Large Team Codebases](#5-best-practices-for-large-team-codebases)
6. [The Spicy Part — Three Bonus Topics](#6-the-spicy-part--three-bonus-topics)
7. [Spicy #1 — Claude Agent SDK: Driving Claude Code Programmatically](#7-spicy-1--claude-agent-sdk-driving-claude-code-programmatically)
8. [Spicy #2 — Claude Cowork: Agentic AI for Everyday Tasks](#8-spicy-2--claude-cowork-agentic-ai-for-everyday-tasks)
9. [Spicy #3 — OpenClaw: Your Personal AI Sidekick](#9-spicy-3--openclaw-your-personal-ai-sidekick)
10. [Day 3 Summary & What's Next](#10-day-3-summary--whats-next)

---

## 1. Day 3 Overview & Structure

Day 3 of Week 3 is a "crescendo" day — a bridge between the foundational pro-feature content of Days 1 and 2 and the advanced swarm/orchestration content of Day 4. It is structured in two halves:

**The Vegetables (the important, practical stuff):**
- Recapping all the pro features and cloud execution capabilities covered earlier in the week
- A real-world demo showing the fruits of all that work
- Best practices for using coding agents on large, team-based codebases

**The Spice (the exciting bonus material):**
- Three demonstrations of related tools that extend the Claude Code ecosystem beyond the terminal
- These are not deeply covered — they are intentional "sizzle" demos to broaden your awareness

The instructor notes that originally the entire day was going to be about large codebases — but since all the underlying concepts had already been covered throughout the course, the large-codebase material could be summarized quickly, leaving room for the spicy bonus content.

---

## 2. Full Recap: All Pro Features Covered So Far

Before diving into new material, here is a complete summary of every pro feature covered in Week 3, Day 1:

### Slash Commands
- Built into Claude Code for triggering predefined actions
- You can create your own slash commands by putting markdown files in `.claude/commands/`
- **Modern approach**: Most people now just use Skills instead, which automatically create slash commands

### Skills
- The **de facto standard** across the entire coding agent ecosystem (Claude Code, Codex, AMP, Open Code, and others)
- Describe reusable behaviors or integrations as markdown files in a dedicated skills folder
- Shared across Claude Code and Codex, making them universally applicable
- Taking over from MCP as the preferred way to add specialized functionality to coding agents

### Multi-Agents
- The concept of running multiple Claude Code (or Codex) instances simultaneously
- Can be achieved by opening multiple terminal windows locally
- OR by kicking off multiple GitHub Issues tagged with `@Claude` — each spawns a separate cloud instance
- OR by running multiple instances on Sprites.dev cloud sandboxes
- All of these approaches constitute "multi-agents" in the broad sense

### Sub-Agents
- More contained than multi-agents — you delegate **one specific task** to an isolated Claude Code instance
- The sub-agent handles just that task in its own context window, then returns the result
- Built-in sub-agents in Claude Code include an "explore" sub-agent that reads lots of files, summarizes them, and reports back — keeping those file reads out of the main context
- You can create your own sub-agents as markdown files in `.claude/agents/`
- **Primary use case**: Offloading work to keep the main conversation context clean

### Agent Teams
- Covered conceptually but not used hands-on yet — coming up on Day 4
- Multiple agents collaborating together (swarms, orchestration)
- The "kooky" end of the multi-agent spectrum

### Hooks
- Tie specific Claude Code events (tool use, stopping, session start, etc.) to automated actions
- Actions can be: shell commands, prompts to Claude, or spawned sub-agents
- Used only occasionally but very powerful when needed
- Often come pre-packaged inside plugins

### Plugins
- Bundle together commands, skills, sub-agents, hooks, MCP servers, and LSP configs
- Distribute them through a marketplace
- Others with Claude Code can add your marketplace and pick which plugins to install
- A great way to standardize tools and workflows across a team

---

## 3. Day 2 Recap: Sandboxing & Remote Execution

A quick summary of the three approaches to sandboxing covered on Day 2:

### 🔵 Native Sandbox (`/sandbox`)
- Built directly into Claude Code
- Lightweight OS-level isolation running on your own machine
- Activates a "sandboxed YOLO" mode: auto-approves file reads, writes, and bash scripts, but prevents escape beyond the sandbox
- Eliminates "approval fatigue" — the real risk of blindly rubber-stamping every permission request

### 🟣 Managed Cloud Sandbox (Claude Code on the Web)
- Anthropic spins up remote Claude Code instances on their servers
- Five ways to trigger it:
  - Prefix any Claude Code message with `&` (ampersand)
  - Run `claude --remote "your instruction"` from the terminal
  - Use the web interface at `claude.ai/code`
  - Use the Claude mobile app (Code tab)
  - Create a GitHub Issue tagged with `@Claude`
- The GitHub Issue method is particularly powerful — Claude picks up the issue, does the work, and opens a PR, all automatically

### 🟡 Third-Party Cloud Sandbox (Sprites.dev)
- Independent, agent-agnostic cloud environment made by Fly.io
- Instant spin-up (under 1 second), persistent state, checkpoint-and-restore capability
- Claude Code comes pre-installed and auto-configures itself in YOLO (bypass permissions) mode
- Ideal when you want full control, don't want code going through Anthropic's infrastructure, or are using a non-Claude coding agent

---

## 4. Live Demo: Zero-Shot Market Data Terminal App

As a demonstration of what was built using Sprites.dev, the instructor continued work on the FiNALLY project overnight on the remote Sprite box. After all the remote work was done, the results were pulled to the local machine with `git pull`.

The instructor asked Claude (running on the Sprite) to:
1. Consolidate all the planning documentation into one summary document
2. Build a **market data demo** — a terminal-based program that visually demonstrates the market data simulator is actually working

### What the Demo Produced

Running `cd backend && uv run market_data_demo` in the local terminal revealed a live terminal display showing:

- **Stock tickers** with real-time simulated prices
- **Color-coded price changes** — red for down, green for up
- **Spark lines** — text-based ASCII graphs showing price movement history for each ticker
- All updating live in the terminal

### Why This Is Impressive

This was described as "zero-shot" — meaning the demo worked exactly as requested the **very first time**, with no iteration or debugging needed. Claude built it on a remote Sprite box, pushed it to GitHub, and the instructor pulled it down to their local machine and ran it immediately.

> **Key takeaway**: The combination of a remote sandbox (Sprites.dev), YOLO mode, and a well-specified planning document allowed fully autonomous, high-quality work to happen while the instructor was away. The stateful nature of Sprites.dev means you can come back to a remote box and it is exactly where you left it.

---

## 5. Best Practices for Large Team Codebases

### Context: The Historical Criticism

Coding agents like Claude Code have historically been criticized for struggling with large, existing codebases. They work brilliantly on small, greenfield projects where they can define the architecture themselves. The challenge was always: **what happens when you hand it a codebase with hundreds of thousands of lines of code that someone else wrote?**

The good news: as of late 2024/early 2025, models have become dramatically better at handling large codebases. But there are still clear best practices that determine success vs. failure.

### Best Practice 1: Invest Heavily in Your `agents.md` / `claude.md`

The `agents.md` (or `claude.md`) file is the primary way you communicate with coding agents about your project. For large codebases, this needs to be **excellent**.

Key principles for effective agent documentation:

- **Progressive disclosure by subdirectory**: Don't put all documentation at the root level. Each subdirectory should have its own `agents.md` that explains what an agent needs to know to work in that specific folder — without having to read all the files.
- **Interface-level descriptions**: Document what functions, APIs, or modules exist at each level so agents call the right things without reading source code.
- **Right level of detail**: Too much detail wastes context window space. Too little means agents make wrong assumptions. The goal is the minimum information needed to make correct decisions.
- **Generate, then review**: Let Claude Code write the documentation first, then carefully eyeball it and refine it. Do several rounds of review — this investment pays huge dividends.
- **Keep it current**: Make "update the agents.md" a required step any time code changes. Stale documentation misleads agents.

### Best Practice 2: Structure Documents for Agent Navigation

There is an important distinction between two ways of referencing other documents:

**Using `@` notation (not recommended as a default):**
```markdown
@planning/architecture.md
```
This inserts the *entire contents* of that file directly into the current document at load time. This is often wasteful — it puts a lot of context into the context window that may not be needed.

**Using links with descriptions (recommended):**
```markdown
For architecture details, see [architecture.md](planning/architecture.md) — describes 
the database schema, API endpoints, and component boundaries.
```
This tells the agent the document *exists* and what it *contains*, but lets the agent decide whether to actually read it. This is much more efficient. Agents will only read documents they determine are relevant to the current task.

**The principle**: Structure your documentation like a summarized index that points to more detailed resources. Agents can navigate progressively rather than loading everything upfront.

### Best Practice 3: Have a Consistent Team Strategy

If everyone on a team uses coding agents differently, the result is chaos. Define and agree on:

- **Which workflow to use**: If you decide to use GitHub Issues tagged with `@Claude`, that should be *the* process — not one option among many.
- **Which plugins to use**: Agree on a set of standard plugins (e.g., code simplifier, featured dev) that everyone installs and uses. This gives everyone the same capabilities and the same quality controls.
- **How new features get built**: When anyone wants a new feature, they should know exactly what process to follow — create a GitHub Issue, write a plan.md, open a terminal session, etc.
- **Avoiding muddle**: Mixed approaches (some people using JIRA, some using GitHub Issues, some just running Claude locally) make it impossible to track what's happening.

### Best Practice 4: Build Project-Specific Skills

Beyond the standard plugins available to everyone, invest in building **domain-specific skills** for your project. These encode how things should be done *in your codebase*:

**Examples of good project-specific skills:**
- A skill that explains how to use your specific market data API across the project
- A skill that describes the framework patterns your team uses (e.g., "in this project we always use the repository pattern for database access")
- A skill for how to run tests, how to deploy, how to write migrations

**Why this matters**: Skills ensure that every coding agent interaction follows the standards you've set. Instead of hoping each agent invocation will figure out your conventions, you encode them once and every future agent automatically follows them.

### Best Practice 5: Maintain a Robust Test Suite (With Caveats)

Having comprehensive tests is important for any large project — with coding agents, it becomes even more critical because:
- Agents need to know when their changes break something
- Tests are the feedback loop that tells an agent whether its work is correct

**However**, there is an important nuance about what makes a *good* test when using AI coding agents:

**What LLMs tend to do wrong (and you should push back on):**
- Write tests that achieve high **percentage coverage** by testing trivial paths through the code
- Create **over-mocked tests** that mock out everything except the specific line being tested
- Write **brittle tests** that break when you refactor but the logic is unchanged

**What you actually want:**
- Tests that verify the **behavior and logic** of your system — if the logic breaks, the test breaks; if you refactor without changing behavior, the test passes
- Tests that represent real user scenarios, not just code paths
- Tests that are worth maintaining

> "Make sure you give feedback on the testing strategy — maybe as part of your `agents.md`. Always push back if you see a ton of tests getting put in there just for the sake of testing."

### Best Practice 6: Human Review Accountability

The most important best practice of all: **humans are still accountable for the code produced**.

Key points:
- Establish a clear culture that a human reviews all agent-generated code
- The human's job is to **reject "coding agent slop"** — overly long files, defensive programming, unnecessary complexity, over-mocked tests
- The asymmetry problem is growing: it's becoming trivially easy to generate enormous amounts of code, but reviewing all that code is genuinely hard work
- Push back on and refuse code that overwhelms the reviewer with its length or complexity
- Coding agents should be instructed to write **succinct, reviewable code**

### Best Practice 7: Work in Bite-Sized Chunks

On a massive project with a large team, you **cannot** say "refactor the whole codebase." That is a recipe for disaster.

Instead:
- Divide large pieces of work into **small, independently specifiable tasks**
- Each task should be something that can be: clearly specified, independently tested, and reviewed by one human in a reasonable time
- Use Claude to help you divide a big task into smaller ones if needed, then assign the small tasks to coding agents
- This keeps each interaction bounded, reviewable, and correctable

> **Anti-test exercise**: As a learning experiment, try telling Claude "refactor the whole codebase and simplify everything" on a large open-source project. Put it in a REPL loop for 10 iterations. The result will show you exactly why bite-sized chunks matter — it probably won't be pretty.

### Summary Table: Large Codebase Best Practices

| Practice | Why It Matters |
|---|---|
| Invest in `agents.md` at every directory level | Agents navigate without reading all source files |
| Use links + descriptions, not `@` embedding | Avoids bloating context with irrelevant docs |
| Consistent team workflow | Prevents fragmentation; keeps quality predictable |
| Build project-specific skills | Encodes your standards into every agent interaction |
| Good tests (behavior-focused, not coverage-focused) | Provides real feedback without brittle mocks |
| Human review culture + reject slop | Humans remain accountable; code stays maintainable |
| Bite-sized chunks | Each task is specifiable, testable, and reviewable |

---

## 6. The Spicy Part — Three Bonus Topics

The remainder of Day 3 covers three "sizzle" topics — demos of tools related to the Claude Code ecosystem that extend its capabilities beyond the standard terminal workflow. These are not fully covered on the course but are demonstrated to broaden awareness:

1. **Claude Agent SDK** — Driving Claude Code programmatically using Python code
2. **Claude Cowork** — Claude Code's agentic capabilities applied to everyday business tasks
3. **OpenClaw** — A personal AI sidekick controlled via Telegram or WhatsApp

---

## 7. Spicy #1 — Claude Agent SDK: Driving Claude Code Programmatically

### What It Is (and What It Isn't)

Despite the name, the **Claude Agent SDK** is **not** a general-purpose agent framework (like LangChain, LlamaIndex, or similar tools). The name can be misleading.

What it actually is: **a Python library that lets you programmatically drive Claude Code** — the same Claude Code you use in the terminal — but instead of typing prompts interactively, you write Python code that sends prompts and receives results.

Think of it as: Claude Code, but called from code instead of from a keyboard.

> **Note on naming**: It was previously called the "Claude Code SDK" and was renamed to "Claude Agent SDK" (singular: agent, not agents). The package name is `claude-agent-sdk`.

### When Would You Use It?

You would use the Claude Agent SDK when:
- You want to **integrate Claude Code into a larger application**
- You want to use all the Claude Code ecosystem features (skills, plugins, sub-agents, MCP servers) but **triggered programmatically**
- You want **Claude Code to build things automatically** without a human at the keyboard
- You're building a product *on top of* Claude Code's capabilities

### Setup: Creating a New Project

The demo starts from a completely empty directory called `space` (named after what it will build — a Space Invaders game).

**Step 1: Create a bare UV project**
```bash
uv init --bare
uv python pin 3.13
```

**Step 2: Install dependencies**
```bash
uv add python-dotenv requests claude-agent-sdk
```

The three dependencies are:
- `python-dotenv` — to load API keys from a `.env` file
- `requests` — general HTTP library
- `claude-agent-sdk` — the SDK itself

**Step 3: Set up the environment file**

Create a `.env` file with your Anthropic API key:
```
ANTHROPIC_API_KEY=your_key_here
```

Create a `.gitignore` file to exclude it from version control (good practice even without a git repo):
```
.env
.venv/
```

### Writing the Code

Create a `main.py` file. Here is the complete structure:

```python
import asyncio
from dotenv import load_dotenv
from claude_agent_sdk import query, ClaudeAgentOptions

# Load environment variables (override any system-level settings)
load_dotenv(override=True)

# Define what you want Claude Code to do
prompt = """Make a vanilla HTML + JS + CSS website for a game of 
Space Invaders. Write the code to files in the current directory,
including index.html."""

# Define which tools Claude Code is allowed to use
tools = ["Read", "Write", "Edit"]  # file read, write, and edit tools

async def main():
    # Configure the agent options
    options = ClaudeAgentOptions(
        allowed_tools=tools,
        model="claude-opus-4-6"    # Specify model (use cheaper models in production!)
    )
    
    # Drive Claude Code programmatically
    async for message in query(prompt=prompt, options=options):
        print(message)

# Run the async main function
asyncio.run(main())
```

**Run it:**
```bash
uv run main.py
```

### Key API Concepts

**`ClaudeAgentOptions`**: The configuration object for your Claude Code session. Parameters include:
- `allowed_tools` — which tools Claude is permitted to use (Read, Write, Edit, Bash, etc.)
- `model` — which Claude model to use
- `permission_mode` — can configure sandboxing/permission behavior
- `mcp_servers` — any MCP servers to make available
- And many more options visible via IDE autocomplete

**`query(prompt, options)`**: An async generator that streams back messages as Claude Code works. Each iteration of the `async for` loop gives you a message object representing one piece of Claude's progress (tool calls, tool results, text output, etc.).

### Important Note on Model Choice

The demo uses `claude-opus-4-6` for entertainment purposes only. In any real use case, **especially in a loop**, you should use a cheaper, faster model:

> "You should use a cheap model. I'm splashing out for your entertainment. It doesn't mean that you should. Please don't do this, especially if it's a tight loop like this. Not a good idea unless you are crazy."

Use `claude-haiku-4-5` or similar lightweight models for programmatic loops.

### Demo Result: Space Invaders Game

After running `uv run main.py` for a couple of minutes, Claude Code (driven via the SDK) created an `index.html` file. Opening it in a browser revealed:

- A fully playable Space Invaders game
- Arrow key controls (Claude inferred these without being told)
- Score display
- Sound effects
- Proper alien graphics at the top
- Correct color theming

This entire game was produced from just a one-sentence prompt with no iteration required — pure zero-shot generation.

### When to Use the SDK vs Terminal

| Use Case | Better Approach |
|---|---|
| Exploring / prototyping a project | Terminal (interactive Claude Code) |
| Building an app on top of Claude Code's capabilities | Claude Agent SDK |
| Scheduled or automated tasks | Claude Agent SDK |
| Want to use skills + plugins programmatically | Claude Agent SDK |
| Need to integrate with other Python code | Claude Agent SDK |
| One-time manual task | Terminal |

---

## 8. Spicy #2 — Claude Cowork: Agentic AI for Everyday Tasks

### What Cowork Is

**Claude Cowork** is an Anthropic product that takes the same agentic power that Claude Code gives to developers and makes it available to **non-developers for everyday professional tasks**.

It uses the same underlying technology as Claude Code — the ability to read files, run processes, use tools, orchestrate tasks — but exposes it through a user-friendly interface designed for business workflows rather than coding.

> "It is basically taking Claude Code and that whole agentic experience that developers get to have, and offering it to business people, or to anyone that wants to use Claude Code's magic for things other than coding."

At the time of recording, Cowork was an early "research preview." By the time you read this, it may have been updated significantly.

### Where to Find It

1. Go to `claude.com/product/co-work`
2. Download the Claude desktop app (same app as the standard Claude desktop client)
3. If you already have the Claude desktop app installed, you already have access

### The Interface: Three Tabs

When you open the Claude desktop app after enabling Cowork, you'll see three tabs:

**Chat tab** — Standard Claude conversation interface, identical to `claude.ai`

**Code tab** — Claude Code on the Web interface, the same browser-based coding environment from Day 2. This connects to the managed cloud execution service.

**Cowork tab** — The new addition. This is where you set up tasks for Claude to execute on your local filesystem.

### What Cowork Can Do

Cowork uses the same plugin marketplace model as Claude Code. Available capabilities include:

- **File management**: Reorganize, rename, move files based on natural language instructions
- **Image processing**: Analyze and work with image files
- **Spreadsheet creation**: Generate formatted Excel files
- **Legal tasks**: Contract review, NDA triage, document analysis
- **Data analysis**: Dig through data files and produce summaries or reports
- **General document processing**: Read, process, and transform any kind of document

The plugin marketplace has an official Anthropic section plus community plugins, organized the same way as Claude Code's marketplace. You can build custom plugins for Cowork using the same `.claude-plugin` format.

### Demo: Processing Receipts into an Expenses Report

**The scenario**: A folder on the desktop containing 12 PDF receipts (from various purchases like audio equipment, software subscriptions, etc.).

**The task**: "Please review these receipts and make me an expenses report as an Excel file — expenses.xlsx"

**How to set it up:**
1. Click **"Work in a folder"** button in the Cowork interface
2. Navigate to the receipts folder on your desktop
3. Click **Allow** to grant Cowork access to modify files in that folder
4. Type your instruction in the chat box
5. Press Enter

**What Cowork does automatically:**
1. Reads the Excel skill documentation (it has skills just like Claude Code)
2. Lists the 12 PDF receipts in the folder
3. Processes each PDF in turn — realizes they contain images, uses vision to read them
4. Extracts expense data from each one
5. Creates `expenses.xlsx` with a nicely formatted table

**The output**: A properly formatted Excel spreadsheet containing all 12 receipts with columns for date, vendor, category (audio, equipment, subscriptions, etc.), amount, and a total — ready for submission.

**The significance**: This is the kind of task that is genuinely tedious for humans but straightforward for Claude Cowork. The receipts-to-Excel workflow that would take 30+ minutes manually took Cowork 5-10 minutes completely autonomously.

### Cowork vs Claude Code

| Aspect | Claude Code | Claude Cowork |
|---|---|---|
| **Target user** | Developers | Everyone (business users, etc.) |
| **Primary focus** | Building and modifying code | Everyday file and document tasks |
| **Interface** | Terminal CLI | Desktop app GUI |
| **Task types** | Software development | File management, document processing |
| **Underlying tech** | Same | Same (Claude Code capabilities) |

---

## 9. Spicy #3 — OpenClaw: Your Personal AI Sidekick

### What OpenClaw Is

**OpenClaw** is a community-built (not Anthropic-made), open-source project that turns Claude Code-style agentic AI into a **personal sidekick** you can interact with through everyday messaging apps like Telegram or WhatsApp.

**The core concept**: Instead of opening a terminal or a browser, you just open WhatsApp or Telegram on your phone, and your AI assistant is right there — ready to take actions on your computer, look things up, play music, control your smart home, etc.

**History of the name:**
1. Originally called **Claudebot** (CLAD-bot) — received a letter from Anthropic
2. Renamed to **Multbot** — hard to say, didn't stick
3. Renamed to **OpenClaw** — the current name (as of recording)

### Security Warning (Read This First)

OpenClaw is **inherently more risky** than other tools covered in this course:

- It runs directly on your computer with access to your files, applications, browser, and system
- You typically give it access to everything — that's what makes it powerful
- A malicious or cleverly crafted prompt could potentially trick it into doing something unsafe
- The OpenClaw installer itself shows a security advisory before first use: "It's a hobby project still in beta. Expect sharp edges. A bad prompt can trick it to doing unsafe things. You must read the security stuff."

**Who should use it**: People who understand what's running on their computer, are comfortable with the risks, and know enough about security to exercise appropriate judgment.

**Mitigation**: One way to reduce risk is to run OpenClaw inside a sandbox (as covered on Day 2).

### Key Features

- **Runs locally on your computer** — not a cloud service
- **Chat-first interface** — designed to be used through messaging apps, not a dedicated UI
- **Memory** — remembers context and previous interactions
- **Browser control** — can open and interact with web browsers
- **Computer control** — can interact with applications on your machine (Spotify, files, etc.)
- **Plugin ecosystem** — extensive range of skills/plugins to extend its capabilities
- **Multi-provider** — supports Anthropic (Claude), OpenAI (GPT), and others

### Installation

**Mac:**
```bash
# One-liner from the OpenClaw website
curl -fsSL https://openclaw.ai/install.sh | sh
```

**Windows (PowerShell):**
```powershell
# Command shown on OpenClaw website
iwr -useb https://openclaw.ai/install.ps1 | iex
```

The install script shows a post-install message: *"I'm the reason your shell history looks like a hacker movie montage."* And upon successful installation: *"The Lobster has landed. Your terminal will never be the same."*

### First-Time Setup Flow

**Step 1: Security acknowledgment**
The first screen shows security notices and asks you to confirm you understand the risks. Default answer is **No** — you must actively choose **Yes** to proceed.

**Step 2: Quick start or full setup**
Select **Quick Start** for a streamlined setup experience.

**Step 3: Choose model provider**
OpenClaw supports multiple AI providers. Options include:
- Anthropic (Claude models)
- OpenAI (GPT / Codex models)
- Others

The demo selects **OpenAI** and uses OAuth (browser-based login) rather than an API key.

**Step 4: Select default model**
After logging in, choose the default model. The demo uses `gpt-5.3-codex`.

**Step 5: Select communication channel**
OpenClaw can connect to:
- Telegram
- WhatsApp
- Others

The demo selects **Telegram**.

**Step 6: Create a Telegram bot**

To connect OpenClaw to Telegram, you need a Telegram bot token:
1. Open Telegram
2. Search for `@BotFather`
3. Type `/newbot`
4. Follow the prompts to name your bot
5. BotFather gives you an API token — copy and paste it into OpenClaw's setup

**Step 7: Install skills**

OpenClaw has a rich skills marketplace. During setup, you choose which skills to install. Examples available:
- **OpenAI Whisper** — speech-to-text (no API key needed)
- **Spotify control** — control music playback
- **Smart home** — control lights and devices
- **Web search** — look things up on the internet
- **File management** — interact with files
- And many more

**Step 8: Personalize your sidekick**
OpenClaw asks for:
- **Name**: What to call your sidekick (the demo uses "Sidekick")
- **Vibe**: A personality description
- **Emoji**: A personality icon

After completing setup, OpenClaw is running in your terminal and connected to Telegram. You can now chat with it from your Telegram app on your phone or computer.

### Demo: Tesla Stock → Music

**The task given via Telegram:**
```
Please look up Tesla stock price.
If it went up today, please play me something upbeat.
Otherwise, something depressing.
```

**What OpenClaw did:**
1. Received the message in Telegram
2. Performed a web search for Tesla's stock price
3. Determined that Tesla went up that day
4. Decided "upbeat" was the appropriate response
5. Chose the song "Upside Down" by Diana Ross
6. Activated Spotify on the computer
7. Started playing the song

**The result**: Music started playing through Spotify without any human interaction beyond the initial Telegram message.

This demonstrates the power of OpenClaw: it interpreted an ambiguous instruction (what counts as "upbeat"?), took multiple steps autonomously (web search → decision → music selection → app control), and produced a tangible real-world result.

### OpenClaw vs Cowork: Key Differences

| Aspect | Claude Cowork | OpenClaw |
|---|---|---|
| **Made by** | Anthropic (official) | Community (open-source) |
| **Target use** | Professional business tasks | Personal life / general AI sidekick |
| **Interface** | Desktop app GUI | Chat apps (Telegram, WhatsApp) |
| **Access level** | Controlled (folder-by-folder) | Full computer access |
| **Risk level** | Lower | Higher |
| **Security** | Managed, sandboxed | Needs careful personal configuration |
| **Interaction** | Open the app, work in a folder | Message from anywhere |
| **Availability** | claude.com/product/co-work | openclaw.ai |

### The Bigger Picture Both Represent

Both Cowork and OpenClaw represent the same idea: the agentic power that coding agents like Claude Code give to engineers is now being extended to everyone.

> "It really brings the power of Claude and the CLI tools that we use as engineers, and it brings them to people personally as their personal sidekick."

The direction of travel is clear: AI agents that can take real actions in the real world, not just generate text, are becoming available to everyone — not just developers who use terminals.

---

## 10. Day 3 Summary & What's Next

### What Was Covered Today

**The main course (vegetables):**
- Full recap of all Week 3 Day 1 pro features and Day 2 sandboxing/remote execution
- Live demo showing zero-shot market data terminal app built autonomously on Sprites.dev
- Comprehensive best practices for using coding agents on large, team-based codebases

**The spicy bonus demos:**
- Claude Agent SDK: programmatic control of Claude Code from Python code
- Claude Cowork: agentic AI for everyday professional tasks (receipts-to-Excel demo)
- OpenClaw: personal AI sidekick accessible via Telegram/WhatsApp (Tesla stock → music demo)

### Key Takeaways

The three spicy demos collectively illustrate a broader truth: the same underlying agentic capability — the ability to read context, make decisions, use tools, and take actions — is being applied in increasingly varied ways:

| Layer | Tool | Who Uses It | How |
|---|---|---|---|
| Programmatic control | Claude Agent SDK | Developers building apps | Python code |
| Professional tasks | Claude Cowork | Business professionals | Desktop app |
| Personal AI | OpenClaw | Individuals | Telegram / WhatsApp |

### Course Progress

**87% complete** — two big days remaining:

- **Day 4** (next): Swarms, agent teams, orchestration — the most advanced multi-agent patterns; the capstone project begins
- **Day 5**: Capstone completion, final recap, ecosystem overview

---

## Quick Reference

### Best Practices Checklist for Large Codebases

- [ ] `agents.md` exists at every directory level with interface-level documentation
- [ ] Documents use links + descriptions rather than `@` embedding
- [ ] Team has agreed on one consistent workflow (GitHub Issues, or JIRA tickets, not both)
- [ ] Standard plugins installed and agreed upon by all team members
- [ ] Project-specific skills built for domain conventions and frameworks
- [ ] Test suite focuses on behavior verification, not coverage percentages
- [ ] Human review process is established and non-negotiable
- [ ] Coding agents are instructed to write succinct, reviewable code
- [ ] New features are broken into bite-sized, independently testable tasks

### Claude Agent SDK — Minimal Code Template

```python
import asyncio
from dotenv import load_dotenv
from claude_agent_sdk import query, ClaudeAgentOptions

load_dotenv(override=True)

prompt = "Your instruction here"
tools = ["Read", "Write", "Edit"]

async def main():
    options = ClaudeAgentOptions(
        allowed_tools=tools,
        model="claude-haiku-4-5"  # Use cheap models in production!
    )
    async for message in query(prompt=prompt, options=options):
        print(message)

asyncio.run(main())
```

### Three Spicy Tools — At a Glance

| Tool | Install | Best For | Risk |
|---|---|---|---|
| **Claude Agent SDK** | `uv add claude-agent-sdk` | Building apps on top of Claude Code | Low |
| **Claude Cowork** | claude.com/product/co-work | Professional file/doc tasks | Low |
| **OpenClaw** | openclaw.ai | Personal AI sidekick | High (full computer access) |

---

## Key Concepts Glossary

| Term | Definition |
|---|---|
| **Progressive Documentation Disclosure** | The practice of putting documentation in each subdirectory, so agents only load context relevant to where they are working |
| **@ notation** | In `claude.md`, embedding a file with `@filename` inserts its entire contents — useful sometimes but often wasteful of context |
| **Link-based documentation** | Describing what a document contains + a link, so agents can choose whether to read it — more context-efficient than `@` embedding |
| **Coding Agent Slop** | Low-quality, bloated code generated by AI that passes tests but is hard to read, review, or maintain (overly long files, excessive mocking, defensive patterns) |
| **Behavior-focused tests** | Tests that break when logic changes but not when code is refactored — the gold standard over coverage-percentage tests |
| **Over-mocked tests** | Tests that mock out so much that they only test the test itself, not real functionality — a common AI coding agent failure mode |
| **Claude Agent SDK** | Python library that lets you drive Claude Code programmatically instead of interactively |
| **`ClaudeAgentOptions`** | The configuration object in the Claude Agent SDK specifying allowed tools, model, MCP servers, etc. |
| **`query()`** | The async generator function in the Claude Agent SDK that sends a prompt to Claude Code and streams back messages |
| **Claude Cowork** | Anthropic's product that applies Claude Code's agentic capabilities to everyday professional/business tasks |
| **OpenClaw** | Community-built open-source personal AI sidekick that connects to Telegram/WhatsApp and can control your computer |
| **@BotFather** | The official Telegram bot for creating new Telegram bots — used to generate the bot token needed for OpenClaw |
| **Bite-sized chunks** | Breaking large development tasks into independently specifiable, testable, reviewable units before assigning to coding agents |
| **Zero-shot** | A task succeeding exactly as requested on the very first attempt, with no iteration or debugging required |

---

*End of Day 3 Notes — Week 3 of the AI Codec Course*
