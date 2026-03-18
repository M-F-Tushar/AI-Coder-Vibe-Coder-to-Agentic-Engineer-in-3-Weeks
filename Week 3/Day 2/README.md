# Claude Code — Week 3, Day 2: Complete Study Guide
### Sandboxing, Remote Execution & Cloud Environments

---

## Table of Contents

1. [Day 1 Recap & What Really Matters](#1-day-1-recap--what-really-matters)
2. [Plugin Deep-Dive: MCP Servers and LSP Files](#2-plugin-deep-dive-mcp-servers-and-lsp-files)
3. [What is Sandboxing and Why Does It Matter?](#3-what-is-sandboxing-and-why-does-it-matter)
4. [The Three Approaches to Sandboxing & Remote Execution](#4-the-three-approaches-to-sandboxing--remote-execution)
5. [Approach 1 — Native Sandbox (Built Into Claude Code)](#5-approach-1--native-sandbox-built-into-claude-code)
6. [Approach 2 — Managed Cloud Sandbox (Claude Code on the Web)](#6-approach-2--managed-cloud-sandbox-claude-code-on-the-web)
7. [GitHub Integration Setup — Step by Step](#7-github-integration-setup--step-by-step)
8. [5 Ways to Run Claude Code Remotely](#8-5-ways-to-run-claude-code-remotely)
9. [Approach 3 — Third-Party Cloud Sandbox (Sprites.dev)](#9-approach-3--third-party-cloud-sandbox-spritesdev)
10. [YOLO Mode in a Sandbox — The Best of Both Worlds](#10-yolo-mode-in-a-sandbox--the-best-of-both-worlds)
11. [Complete Day 2 Summary & Comparison of All Approaches](#11-complete-day-2-summary--comparison-of-all-approaches)

---

## 1. Day 1 Recap & What Really Matters

Before diving into sandboxing, the instructor walks through which Day 1 features actually matter in practice versus which are rarely used. This helps prioritize where to spend your energy.

### Practical Priority Guide for Day 1 Topics

| Feature | How Often You'll Use It | Key Point |
|---|---|---|
| **Slash Commands** | Rarely standalone | Almost entirely replaced by **Skills** now |
| **Skills** | Very frequently | The de facto standard — used everywhere, even outside Claude Code |
| **Sub-Agents** | Frequently | Primary use case: freeing up the main context window |
| **Agent Teams** | Occasionally (later this week) | More experimental; covered on Day 4 |
| **Hooks** | When you have a specific need | Know they exist; look up docs when needed |
| **Plugins** | Team/enterprise contexts | Good to know; most daily work is skills + sub-agents |

### Skills Are Universal

Skills have become the **de facto standard** across the AI coding agent ecosystem — not just Claude Code. They were originally popularized by the AMP project and are now used in Codex, Open Code, AMP, and others. Even if your preferred tool is not Claude Code today, skills will likely be relevant to it soon.

### The Primary Reason to Use Sub-Agents

Out of all the advantages of sub-agents, the **most important one** is freeing up context. When work happens in a sub-agent's isolated context, the main conversation stays clean and has more room. This is why you'll reach for sub-agents most often.

---

## 2. Plugin Deep-Dive: MCP Servers and LSP Files

Day 1 covered the core four sub-directories of a plugin (`commands`, `skills`, `agents`, `hooks`). There are two more optional files worth knowing about:

### `.mcp.json` — MCP Servers in a Plugin

A plugin can include **MCP (Model Context Protocol) servers** as part of its package. You define them in a file called `.mcp.json` inside the plugin's `.claude-plugin` folder.

```
my-plugin/
└── .claude-plugin/
    ├── plugin.json
    ├── .mcp.json         ← Defines MCP servers bundled with this plugin
    └── hooks/
        └── hooks.json
```

This means that when someone installs your plugin, they also get any MCP server connections you've configured. This is powerful for distributing pre-configured integrations to a team.

### `.lsp.json` — Language Server Protocol

LSP stands for **Language Server Protocol**. It is a standard that describes the syntax rules and validation behavior of a programming language so that tools can understand code written in that language.

Claude Code already knows about all the common programming languages (Python, JavaScript, etc.). However, if you're working with a **custom or obscure programming language** that Claude isn't already trained on, you can describe it to Claude using an LSP configuration file.

**How to use it:**

1. Create a file called `.lsp.json` inside the `.claude-plugin` folder of your plugin.
2. Configure it to describe the language rules.
3. When the plugin is installed, Claude Code will understand that language for that project.

**When would you actually need this?** Almost never for typical developers. It was mentioned because it appeared in Andrej Karpathy's influential tweet about Claude Code features — so it's good to know where it lives, even if you'll rarely use it.

---

## 3. What is Sandboxing and Why Does It Matter?

Sandboxing is about **constraining what Claude Code can do** — ring-fencing its access to your system so that it can only reach what you explicitly permit.

### The Core Idea

Without sandboxing, Claude Code can:
- Read and write any file on your computer
- Access any website
- Run any shell command

With sandboxing, you can say things like:
- "You can read and write files, but **only within this project directory**"
- "You can use the network, but **only to these 10 approved websites**"
- "You can run bash scripts, but **you cannot call external APIs**"

### Three Benefits of Sandboxing

**Benefit 1 — Security:** You're protecting your system from accidental or runaway actions. Claude can't reach outside the sandbox even if it tries.

**Benefit 2 — Increased Productivity (YOLO without the risk):** Because the sandbox protects you, you can be more aggressive. You can let Claude work without constant permission prompts, knowing that the worst case is still contained.

**Benefit 3 — Solving Approval Fatigue:** This is subtle but important. Without a sandbox, Claude asks you to approve every shell command and file change. You press `1` or `2` to approve each action. But over time, your brain goes on autopilot and you just keep pressing `1` without reading what you're approving. This is called **approval fatigue** — you're pretending to supervise but actually just rubber-stamping everything.

A sandbox is actually *more* secure than manual approvals in this scenario, because the fence is real — it doesn't depend on your attention.

---

## 4. The Three Approaches to Sandboxing & Remote Execution

The course introduces **three distinct approaches**, which together cover local and remote execution. They are color-coded for reference throughout the day:

| Color | Name | Description | Runs On |
|---|---|---|---|
| 🔵 Blue | **Native Sandbox** | Built into Claude Code — lightweight OS-level isolation | Your own machine |
| 🟣 Purple | **Managed Cloud Sandbox** | Anthropic-hosted remote execution (Claude Code on the Web) | Anthropic's servers |
| 🟡 Yellow | **Third-Party Cloud Sandbox** | Independent cloud providers (e.g., Sprites.dev) | Provider's servers |

Each approach has different trade-offs in terms of setup complexity, cost, security, and flexibility.

> **Note on Docker/Dev Containers:** Docker and VS Code Dev Containers are the "old way" of doing this. They're still valid options if you know them, but the three approaches above are newer and better in most cases. Everything covered today supersedes the Docker approach.

---

## 5. Approach 1 — Native Sandbox (Built Into Claude Code)

### What It Is

This is a **sandbox mode baked directly into Claude Code**. It uses OS-level isolation (not a full Docker container) to create a lightweight, controlled environment around Claude's operations. It's faster and simpler than Docker because it runs at the operating system level rather than in a full virtual machine.

### Platform Availability

| Platform | Status |
|---|---|
| **Mac** | Fully supported |
| **Linux** | Fully supported |
| **Windows** | Requires WSL (Windows Subsystem for Linux); native Windows support coming soon |

If you're on Windows and don't know what WSL is, skip to Approach 2 or 3 for now.

### How to Enable It

Inside Claude Code, type:
```
/sandbox
```

You'll see the current sandbox status and a menu with options.

### Sandbox Options

**Option 1 — Sandboxed YOLO (Recommended for most use cases)**

Commands automatically run inside the sandbox. Attempts to do things outside the sandbox gracefully fall back to asking for permissions. You can add explicit deny rules for anything you never want allowed. This is essentially YOLO mode but with guardrails — you get the speed and productivity of not being asked for approvals on every little thing, while the sandbox prevents anything from escaping the project environment.

**Option 2 — Regular Sandbox**

A sandbox that still allows bash/shell scripts to run with regular (non-elevated) permissions. Less automatic — still asks before some operations.

### What Claude Can Do Inside the Sandbox

Once the sandbox is active:
- **Automatically allowed** (no prompt needed): Read files, write files, run bash/shell scripts
- **Still requires your approval**: Web searches (first time accessing a new domain)
- **Can be overridden**: You can add explicit allow or deny rules in the Overrides section

### Configuring the Sandbox

After enabling it, you can navigate to:
- **Overrides**: Choose whether attempts to go outside the sandbox fall back to normal permissions (permissive) or fail completely (strict)
- **Config**: See what is currently allowed and denied — you might find some things already in the denied list

### Practical Demo Result

The instructor asked Claude to carry out comprehensive research and write three planning documents to the planning directory — all without being asked for permission on every step. Claude completed the entire multi-step task (including using the Context7 plugin for research) with only web search requests requiring a first-time approval.

> **Best Practice**: Read the Claude Code sandbox documentation for full details on granular configuration — for example, allowing web searches to specific domains only. There are important security considerations described there as well.

---

## 6. Approach 2 — Managed Cloud Sandbox (Claude Code on the Web)

### What It Is

This is the "juicy" part that makes sandboxing genuinely exciting. Instead of running Claude Code on your local machine, **Anthropic runs it for you in the cloud** — in an isolated, sandboxed environment.

This goes by several names in different contexts:
- **Claude Code on the Web** (official Anthropic name)
- **Remote Execution**
- **Codex on the Web** (OpenAI's equivalent for Codex)
- **Managed Cloud Sandbox** (most descriptive technical name)

### What Makes It Remarkable

The core concept is a shift in where computation happens:

**Before (local):**
Your computer → Claude Code runs here → modifies your files

**After (remote/cloud):**
Your computer → sends instruction → Anthropic's servers → Claude Code runs there → commits to GitHub → you review PR

Everything still ends up in your GitHub repository, but the actual execution — all the CPU cycles, file reads, writes, tests — happens on Anthropic's infrastructure, not your machine.

### The "Teleport" Feature

While Claude Code is running a task remotely, you can **"teleport" into that session** — connecting your local terminal directly to the remote session that's running in the cloud. It's like SSH-ing into a remote server, except the remote server is an actively running Claude Code session.

Use `/tasks` to see all currently running remote sessions, then select one to teleport into it.

---

## 7. GitHub Integration Setup — Step by Step

The Managed Cloud Sandbox is tightly integrated with GitHub. All of your code must be in a GitHub repository because the cloud instance will clone your repo, do the work, and then push a branch and open a PR for your review.

### Prerequisites

Before you can use remote execution, you need:
- A GitHub account with your project repo pushed
- Everything committed (working tree clean)
- The GitHub CLI installed and authenticated
- The Claude GitHub App installed in your repo

### Step 1: Connect Claude to GitHub (via the web)

1. Open a browser and go to `claude.ai/code`
2. You'll see the "Code with Claude anywhere" landing page
3. Click **Connect to GitHub**
4. Authorize Claude to access your GitHub account
5. Click **Connect Repositories**

### Step 2: Install the Claude Code GitHub App in Your Repo

1. From the connect screen, click **Install Claude into repos**
2. Choose **Only selected repositories** and pick your project repo (or choose all repositories)
3. Click **Install and Authorize**

### Step 3: Install the GitHub CLI on Your Machine

Inside Claude Code, run:
```
/install-github-app
```

Claude will tell you if the GitHub CLI (`gh`) is not installed and provide the exact install command for your OS:

**Mac:**
```bash
brew install gh
```

**Windows:**
```bash
winget install --id GitHub.cli
```

**Linux:** Refer to the docs link Claude provides.

### Step 4: Log In to the GitHub CLI

```bash
gh auth login
```

This opens a browser window for OAuth. You'll enter a code displayed in your terminal and authorize the connection. Once done, you're logged into the GitHub CLI.

### Step 5: Run the Install GitHub App Command Again

Back in Claude Code:
```
/install-github-app
```

This time, it should find everything installed. Follow the prompts:
1. **Select your repository** from the list
2. **Select GitHub Workflows to install** — you'll see two workflow options; tick both with the Space bar and press Enter
3. **Choose token type** — select the long-lived token that comes with your Claude subscription
4. **Authorize** Claude Code to connect to your Claude chat account via the browser

### Step 6: Review and Merge the Setup Pull Request

At this point, Claude Code automatically opens GitHub in your browser. A **Pull Request** has been created — this PR adds GitHub workflow YAML files to your repo (in `.github/workflows/`). These files are what give Claude the ability to respond to GitHub Issues.

1. Click **Create Pull Request**
2. Click **Merge Pull Request**
3. Click **Confirm Merge**

### What Was Just Set Up?

Your repo now has these files:
```
.github/
└── workflows/
    ├── claude.yaml                ← Triggers when @Claude is mentioned in issues/PRs
    └── claude-code-review.yaml   ← Triggers for automated code review on PRs
```

These GitHub Actions workflows are the bridge between GitHub events (issues, PRs) and Claude Code running in Anthropic's cloud.

---

## 8. Five Ways to Run Claude Code Remotely

Now that everything is set up, here are the **five different ways** to trigger remote execution:

### Way 1 — The Ampersand Prefix (Inside Claude Code)

**How it works:** While inside a Claude Code session, prefix any message with `&` (ampersand). The task runs remotely on Anthropic's servers instead of your local machine.

**Example:**
```
& please rewrite the README and create a new document
```

**Key detail:** When you kick off a remote task this way, the **full current conversation context** is sent to the cloud. So Claude can continue seamlessly where you left off, now running remotely.

**Monitoring:** Use `/tasks` to see all tasks currently running in the cloud. You can kick off multiple tasks from the same session and have them all running in parallel in the cloud, just as you could open multiple terminals locally with the `+` button.

### Way 2 — `claude --remote` from the Terminal

**How it works:** Instead of running `claude` normally, run `claude --remote` followed by your instruction — entirely from your operating system's terminal, not inside a Claude Code session.

```bash
claude --remote "please build the complete market data backend with full unit tests"
```

This spins up a remote Claude Code instance, does the work, pushes a branch to GitHub, and finishes. You then review and merge the PR.

### Way 3 — Claude.ai/code Web Interface

**How it works:** Go to `claude.ai/code` in any browser (no terminal needed at all). You get a browser-based interface that looks like a simplified Claude Code.

**First-time setup:** When you first visit, you'll be asked to configure your "cloud environment" — specifically the network access level:
- **None** — no network access from the remote instance
- **Trusted** — access to trusted/known websites *(recommended for most use cases)*
- **Full** — unrestricted network access

**Using it:**
1. Select your repository from the list
2. Type any instruction in the prompt box
3. Hit Enter — Claude Code spins up in the cloud, does the work
4. The results appear as a PR in your GitHub repo

**What happens on your machine:** Absolutely nothing. Your machine is completely idle. All computation happens on Anthropic's servers.

**Caveats at time of recording:** Labeled as "research preview" — somewhat slower than local execution; can be slightly flaky (may stop and need to be prompted again); will improve over time.

**Practical demo result:** Asking Claude to design the market data backend and write a detailed planning document took about 10 minutes, produced a 1,490-line document, and pushed it as a PR in GitHub.

### Way 4 — The Claude Mobile App

**How it works:** On your phone (iOS or Android), open the Claude mobile app. The bottom navigation bar includes a **"Code"** section alongside Chats, Projects, and Artifacts.

Tap **"Code"** → you see the same list of sessions as `claude.ai/code` → tap **"New Session"** → give your instruction → submit.

**What you can do from your phone:**
- Kick off new coding tasks
- Run multiple sessions in parallel
- Come back later and find a PR ready for review in GitHub
- Approve and merge entirely from your phone

This creates a genuine mobile development workflow: you could be at dinner, kick off three features from your phone, and by the time you're back at your computer, review the PRs.

### Way 5 — GitHub Issues Tagged with @Claude

This is the most remarkable method — it requires no terminal, no browser IDE, no app. Just GitHub.

**How it works:**
1. Go to your GitHub repository
2. Click **Issues** → **New Issue**
3. Write your task as the issue description (be as detailed as needed)
4. In the issue body or title, **mention `@Claude`**
5. Click **Create**

Within seconds, Claude Code automatically:
- Detects the `@claude` tag via the GitHub workflow you installed
- Spins up a remote instance in Anthropic's cloud
- Clones your repository
- Reads your planning docs and context
- Does the work (builds, tests, fixes)
- Creates a branch and pushes it to GitHub
- Posts a comment on the issue with a to-do checklist showing progress
- Opens a Pull Request for your review

**You did nothing after pressing Create.** The GitHub workflow handles everything.

**Practical demo result:** Creating an issue titled "Build complete market data backend" with detailed instructions and `@Claude` resulted in: 21 files changed, 1,600+ lines of code written, 90+ tests created, all in about 7 minutes — with a PR ready to review and merge.

> **Pro tip:** Think of this like the Jira/GitHub ticket workflow from Week 2 — but now Claude picks up the issue autonomously and does all the work without you ever opening a terminal. You can create many issues at once and have multiple Claude instances working on all of them in parallel.

---

## 9. Approach 3 — Third-Party Cloud Sandbox (Sprites.dev)

### What It Is

This is the "yellow" approach — using a cloud sandbox from a company that is **neither Anthropic nor the creator of your AI coding tool**. It is an independent, general-purpose cloud execution environment designed specifically for coding agents.

The specific product demonstrated is **[Sprites.dev](https://sprites.dev)**, made by the team at **Fly.io** (a well-regarded cloud hosting platform).

### Why Would You Use This Instead of Anthropic's Cloud?

- You're using **Codex, Open Code, or any non-Claude agent** and want a sandboxed environment
- You want more **control over the hardware and network** than Anthropic's managed environment gives you
- You prefer **not to have your code go through Anthropic's infrastructure** for any reason
- You want the ability to **checkpoint and restore** a sandbox environment (a unique Sprites feature)
- You want faster instance creation or different pricing

> **Important**: Third-party cloud sandboxes like Sprites.dev work with **any coding agent** — Claude Code, Codex, Open Code, or any other. This approach is completely agent-agnostic.

### Key Features of Sprites.dev

- **Hardware-isolated execution environment** — genuine hardware isolation, not just container emulation
- **Persistent Linux computer** — acts like a full Linux machine in the cloud; your environment persists across sessions
- **Checkpoint and restore** — you can save the state of a sandbox and rewind to a previous point in time
- **Extremely fast spin-up** — a new instance is created in under a second (0.6 seconds in the demo)
- **Claude Code pre-installed** — Claude Code comes pre-installed on every instance and auto-updates when relaunched
- **Automatic YOLO mode** — Claude Code starts in bypass permissions mode because it's already sandboxed at the hardware level

### Setup Walkthrough

**Step 1: Create an account at sprites.dev**

Note: A credit card is required even for the free trial credits. As of recording, $30 in free credits is provided (roughly 500 Sprite instances).

**Step 2: Install the Sprite CLI**

After signing up, the dashboard shows you an install command that contains your API key embedded in it. Copy and paste it into your terminal exactly as shown:

```bash
# The command shown on the dashboard includes your key — copy exactly as shown
curl -fsSL https://sprites.dev/install | sh -s YOUR_KEY_HERE
```

**Step 3: Log in**

```bash
sprite login
```

This opens a browser window for authentication.

**Step 4: Create a Sprite (cloud instance)**

```bash
sprite create finally-worker
```

This creates a new isolated Linux machine in the cloud. Named `finally-worker` in the demo. Creation takes **0.6 seconds** — extremely fast server spin-up is a core fly.io/Sprites.dev selling point.

The terminal prompt changes to show `sprite@sprite` indicating you are now connected to the remote machine.

**Step 5: Clone your repository**

Since the remote box is empty, clone your project onto it:

```bash
git clone <your-repo-url>
cd finally
ls  # Verify everything is there
```

**Step 6: Launch Claude Code**

```bash
claude
```

Claude Code is **pre-installed** on every Sprite. On first launch:
- It asks setup questions (choose theme, etc.)
- It asks you to log in to Claude
- The **browser window for login opens on your local machine** even though the process is running in the cloud — Sprites.dev handles this browser-forwarding automatically
- You authorize in the browser → logged in on the remote box

**Step 7: Update Claude Code (if needed)**

The first launch may run an older version. Exit Claude Code (`Ctrl+C`) and re-run `claude` — it auto-updates to the latest version on restart.

**Step 8: Accept Bypass Permissions Mode**

You'll see a warning:
```
Warning: Claude Code running in bypass permissions mode
```

This is **intentional and safe** because:
- The Sprite is isolated hardware — it cannot reach your local machine
- The worst Claude can do is affect files within the Sprite — which you can delete and recreate in 0.6 seconds
- Bypass permissions mode is **automatically configured** by Sprites.dev to maximize Claude productivity inside the sandbox

Claude is now running on a remote cloud machine, in full YOLO mode, completely sandboxed. You interact with it through your VS Code terminal as if it were local — but everything is happening on Fly.io's hardware in the cloud.

### Logging Into GitHub from a Sprite

When you want Claude to push code to GitHub from a Sprite, you need to authenticate the GitHub CLI on the remote box:

```bash
# Exit Claude Code first (Ctrl+C twice)

# Log in to GitHub CLI on the remote box
gh auth login
```

The browser that opens for the GitHub OAuth flow opens **on your local machine** (Sprites.dev handles this forwarding), even though the process is running on a remote server. Enter the code shown in the terminal, authorize, and you're logged into GitHub from the remote box.

### Resuming After Interruptions

If you restart Claude Code on the Sprite (e.g., to update it or after a login step), you can resume the previous conversation exactly where it left off:

```
/resume
```

This picks up the previous conversation — just like the `/resume` command covered in Week 2.

---

## 10. YOLO Mode in a Sandbox — The Best of Both Worlds

The combination of a sandbox and YOLO mode represents the highest-productivity approach available. The sandbox removes the risk that made YOLO scary in the first place.

### Why This Combination Is Powerful

| Factor | Without Sandbox + YOLO | With Sandbox + YOLO |
|---|---|---|
| **Permission prompts** | None (risky) | None (safe) |
| **Access to your machine** | Full | None — isolated |
| **Damage potential** | High (your files at risk) | Zero (contained environment) |
| **Productivity** | Maximum | Maximum |
| **Peace of mind** | Low | High |

You get **all of the speed** of YOLO mode — no interruptions, no approval buttons — while **all of the safety** comes from the sandbox isolating Claude from anything you care about.

### The Workflow in Practice (Sprites.dev Demo)

The instructor ran a full workflow on Sprites.dev that demonstrates this combination end-to-end:

1. Instructed Claude (in YOLO mode on the Sprite) to review the code, run all tests, and write findings to a review file
2. Claude ran all tests without asking permission — some passed, some failed; it correctly reported both
3. Asked Claude to push changes to GitHub → failed (not logged in to GitHub yet on the Sprite)
4. Exited Claude Code, ran `gh auth login` (browser opened locally for auth), logged in
5. Re-entered Claude Code, used `/resume` to pick up the previous conversation
6. Claude created a branch, pushed it, and told us a PR was ready
7. Reviewed and merged the PR in GitHub
8. Gave Claude a comprehensive follow-up task: pull the latest main branch, carry out all the fixes and improvements documented in the review file, keep working until all tests pass, then push a new branch to GitHub
9. Claude worked fully autonomously — fixing bugs one by one, rerunning tests, refining code — with zero approvals needed throughout
10. Created a new PR with all improvements; instructor reviewed and merged

The experience was described as:

> "It's been the most amazing experience sitting here watching this happening. I haven't approved anything. It's been working and working, fixing bugs one by one, rerunning the tests, more passing, reporting on problems, and then at the end it created a branch, submitted the push — everything just happening."

And the key insight:

> "It's so efficient because there's no more of this permissions approval nonsense. It's all running. It's going to do its thing... it's super productive, and lots are going on, and yet it's also secure. It's happening in a way that it's totally sandboxed. So it really feels like I've got the best of both."

---

## 11. Complete Day 2 Summary & Comparison of All Approaches

### Three Approaches — At a Glance

#### 🔵 Approach 1: Native Sandbox (Blue)

Activation: `/sandbox` → Option 1 (Sandboxed YOLO) inside Claude Code

| Attribute | Detail |
|---|---|
| **Where it runs** | Your own machine |
| **Cost** | Free (part of Claude Code) |
| **Platform** | Mac & Linux (Windows: requires WSL) |
| **Isolation type** | OS-level (lighter and faster than Docker) |
| **Permission prompts** | Auto-approved for files/bash; web requires first-time approval |
| **Best for** | Most everyday development tasks where you want YOLO speed locally |
| **Limitations** | Still on your machine; doesn't give you true remote/cloud execution |

#### 🟣 Approach 2: Managed Cloud Sandbox (Purple)

Activation: `claude.ai/code` → or → `@Claude` in GitHub Issues → or → `&` prefix → or → `claude --remote` → or → Mobile App

| Attribute | Detail |
|---|---|
| **Where it runs** | Anthropic's cloud servers |
| **Cost** | Included with Claude Pro/Team subscription |
| **Platform** | Any (it's in the cloud — your OS doesn't matter) |
| **Isolation type** | Fully managed cloud sandbox |
| **Permission prompts** | None (completely automated) |
| **Best for** | Long-running tasks, mobile coding, parallel tasks via GitHub Issues |
| **Limitations** | Slightly slower than local; requires GitHub integration; labeled "research preview" |

#### 🟡 Approach 3: Third-Party Cloud Sandbox (Yellow)

Activation: `sprite create my-box` → `git clone` → `claude` → YOLO mode auto-configured

| Attribute | Detail |
|---|---|
| **Where it runs** | Third-party provider's servers (e.g., Sprites.dev / Fly.io) |
| **Cost** | Provider charges (~$30 free credits on Sprites.dev, pay per use after) |
| **Platform** | Any (remote Linux box — your OS doesn't matter) |
| **Isolation type** | Hardware-isolated Linux machine |
| **Permission prompts** | None (YOLO mode auto-configured) |
| **Best for** | Agent-agnostic use; checkpointing; maximum control; non-Claude agents |
| **Limitations** | Requires account setup with credit card; extra setup steps |

### Key GitHub Integration Points

For both Approaches 2 and 3, the GitHub workflow is central to how results are delivered:

```
You create issue / make request
         ↓
Claude Code runs in cloud (on Anthropic or Sprite)
         ↓
Claude reads your planning docs and context
         ↓
Claude writes code, runs tests, fixes bugs
         ↓
Claude pushes branch to GitHub
         ↓
Claude opens Pull Request with summary
         ↓
You review → Merge → Done
```

### When to Use Each Approach

| Situation | Best Approach |
|---|---|
| Normal local development with reduced interruptions | Native Sandbox (Blue) |
| Long-running task you want to run while away from your desk | Managed Cloud (Purple) — web or mobile |
| Kicking off many parallel tasks like a task board | GitHub Issues with @Claude (Purple) |
| Using Codex, Open Code, or any non-Claude agent | Third-Party Sandbox (Yellow) |
| Want maximum control over the execution environment | Third-Party Sandbox (Yellow) |
| Don't want your code going through Anthropic's servers | Third-Party Sandbox (Yellow) |
| Testing code on a clean Linux environment | Third-Party Sandbox (Yellow) |

### The Course Progress at This Point

At this point in the course, you are approximately **80% complete**:

- ✅ **Day 1 complete** — Pro features (slash commands, sub-agents, hooks, plugins)
- ✅ **Day 2 complete** — Sandboxing + remote execution (all 3 approaches, all 5 remote methods)
- 🔜 **Day 3** — Working with large codebases (context management at scale)
- 🔜 **Day 4** — Swarms and orchestrators (the most advanced multi-agent patterns)
- 🔜 **Day 5** — Capstone project (FiNALLY trading app — built entirely by agents)

---

## Quick Reference: Commands Introduced in Day 2

| Command | Where | What It Does |
|---|---|---|
| `/sandbox` | Claude Code | Configure and toggle the native sandbox |
| `/tasks` | Claude Code | List all currently running remote sessions |
| `/install-github-app` | Claude Code | Set up the GitHub App for remote execution |
| `/resume` | Claude Code | Resume a previous conversation (works on remote boxes too) |
| `& <instruction>` | Claude Code prompt | Run a task remotely on Anthropic's cloud |
| `claude --remote "<task>"` | Terminal | Launch a remote Claude Code session from the terminal |
| `gh auth login` | Terminal | Log in to the GitHub CLI (needed for remote box pushes) |
| `sprite create <name>` | Terminal | Create a new Sprites.dev cloud instance |
| `sprite login` | Terminal | Authenticate with Sprites.dev |
| `@Claude` in GitHub Issues | GitHub | Tag Claude to autonomously pick up and complete a task |

---

## Key Concepts Glossary

| Term | Definition |
|---|---|
| **Sandbox** | An isolated execution environment that restricts what code (including Claude) can access |
| **Approval Fatigue** | The tendency to blindly approve every Claude request after repeated use, undermining real security |
| **Remote Execution** | Running Claude Code on servers other than your own local machine |
| **Claude Code on the Web** | Anthropic's official term for managed cloud execution of Claude Code |
| **Teleport** | A Claude Code feature that lets you attach your terminal session to a remotely running Claude Code instance |
| **`/tasks`** | Claude Code command to see all remote sessions currently running in the cloud |
| **GitHub Workflow** | A YAML file in `.github/workflows/` that defines automated CI/CD actions; used here to trigger Claude on issues |
| **`@Claude` in GitHub** | Mentioning Claude in a GitHub issue or PR triggers a remote Claude Code instance to handle it |
| **Sprites.dev** | A third-party cloud sandbox product by Fly.io, designed for running coding agents in isolated environments |
| **Checkpoint & Restore** | A Sprites.dev feature that lets you save the exact state of a sandbox and rewind to it later |
| **YOLO Mode** | Running Claude with all permission prompts bypassed — safe in a sandbox, risky without one |
| **Bypass Permissions** | The technical term for YOLO mode in Claude Code — all approval prompts skipped |
| **WSL** | Windows Subsystem for Linux — a way to run a Linux environment on Windows, required for native sandboxing on Windows |
| **Native Sandbox** | OS-level sandboxing built into Claude Code, activated with `/sandbox` — lighter than Docker |
| **LSP** | Language Server Protocol — a standard for describing programming language rules to development tools |
| **MCP** | Model Context Protocol — a standard for connecting AI models to external data sources and tools |
| **Pull Request (PR)** | A GitHub mechanism to propose and review code changes before merging them into the main branch |
| **`gh auth login`** | GitHub CLI command to authenticate your machine (or remote box) with your GitHub account |
| **`.github/workflows/`** | Directory in a GitHub repo containing YAML files that define automated GitHub Actions workflows |

---

*End of Day 2 Notes — Week 3 of the AI Codec Course*
