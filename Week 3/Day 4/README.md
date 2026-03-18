# Claude Code — Week 3, Day 4: Complete Study Guide
### Agent Teams, Swarms, Orchestration, GSD & Building the FiNALLY Trading Platform

---

## Table of Contents

1. [Day 4 Overview — The Roller Coaster Peak](#1-day-4-overview--the-roller-coaster-peak)
2. [Swarms vs. Orchestration — The Spectrum](#2-swarms-vs-orchestration--the-spectrum)
3. [Agent Teams: What They Are and Why They're Different](#3-agent-teams-what-they-are-and-why-theyre-different)
4. [Sub-Agents vs. Agent Teams — Complete Comparison](#4-sub-agents-vs-agent-teams--complete-comparison)
5. [When to Use Agent Teams — Use Cases](#5-when-to-use-agent-teams--use-cases)
6. [Setting Up Claude Agent Teams — Step by Step](#6-setting-up-claude-agent-teams--step-by-step)
7. [Agent Teams in Action — Live Build of the FiNALLY Trading Platform](#7-agent-teams-in-action--live-build-of-the-finally-trading-platform)
8. [GSD: Spec-Driven Design Meets Multi-Agent Orchestration](#8-gsd-spec-driven-design-meets-multi-agent-orchestration)
9. [GSD Commands and Workflow](#9-gsd-commands-and-workflow)
10. [GSD in Action — Building the FiNALLY Platform (5-Hour Deep Dive)](#10-gsd-in-action--building-the-finally-platform-5-hour-deep-dive)
11. [GSD vs. Claude Agent Teams — Side-by-Side Comparison](#11-gsd-vs-claude-agent-teams--side-by-side-comparison)
12. [Day 4 Summary and Key Takeaways](#12-day-4-summary-and-key-takeaways)

---

## 1. Day 4 Overview — The Roller Coaster Peak

Day 4 of Week 3 is described as the "roller coaster peak" moment — the highest point of the entire three-week course before the final descent into the capstone project.

### What Today Covers

This is the day the course reaches **Stages 7 and 8** of Steve Yegge's eight-stage evolution of the coding agent programmer:

- **Stage 7 — Swarms**: Many agents running simultaneously. Everything is going at once. It feels chaotic, almost mad.
- **Stage 8 — Orchestration**: The realization that you can rein in the chaos by giving agents structure, hierarchy, and defined roles — having LLMs manage the coordination process.

The two approaches explored today:
1. **Claude Agent Teams** — Anthropic's experimental feature for coordinating multiple Claude Code instances
2. **GSD (Get Sh\*t Done)** — A community-built orchestration framework combining spec-driven design with multi-agent execution

Both approaches are used to build the same project — the **FiNALLY trading platform** — so you can see a direct side-by-side comparison of results.

---

## 2. Swarms vs. Orchestration — The Spectrum

Rather than being two distinct binary states, swarms and orchestration sit on a **continuum**. Your position on this spectrum depends on the choices you make and how much structure you impose.

### The Swarm End (Stage 7)
- Many agents all doing things at once
- Minimal structure or hierarchy
- Maximum parallelism and speed
- High chaos — hard to predict or control
- Best for: throwing raw power at a problem, early ideation, pure generation

### The Orchestration End (Stage 8)
- Agents with defined roles and responsibilities
- A lead agent manages coordination
- Structured task dependencies and communication channels
- More predictable outcomes, more methodical
- Best for: production-quality builds, projects requiring coherent integration, quality-sensitive work

### Where to Aim
Most real projects should sit **somewhere in the middle** — with enough structure to produce coherent output, but enough parallelism to benefit from having multiple agents working simultaneously.

> *"The different solutions will be looking at somewhere on that continuum between being a sort of wild swarm with no structure and extremely organized structured orchestration. Where you are on that continuum depends on the choices you make, how you set it up, and how crazy you want to go."*

---

## 3. Agent Teams: What They Are and Why They're Different

### What Are Claude Agent Teams?

Claude Agent Teams are an **experimental feature** in Claude Code (experimental at time of recording — may be fully live by the time you read this). They allow multiple Claude Code instances to be **coordinated as a team** to achieve a shared goal.

The key components of an agent team:

**The Team Lead**
- One Claude Code instance acts as the manager
- Its job is to assign tasks, manage collaboration, and coordinate toward the goal
- It tracks the overall task list and decides what gets worked on when

**The Teammates**
- The other Claude Code instances on the team
- They work independently on their assigned areas
- They can communicate directly with each other (not just through the lead)
- They can message the human directly too

### The Critical New Feature: Direct Communication Between Agents

This is the most important distinction from everything covered previously:

- In sub-agents, agents exist only to serve the main Claude Code. They complete a task and report back. They **cannot communicate with other agents**.
- In agent teams, teammates **can send messages to each other directly**. A frontend agent can ask the backend agent a question. A tester can report directly to both the frontend and backend agents.

This enables genuine collaboration, not just delegation.

### Persistence vs. Transience

| | Sub-Agents | Agent Team Members |
|---|---|---|
| **Lifespan** | Exists only for the duration of one task | Persists throughout the session |
| **Context** | Isolated, discarded after task | Maintained, long-running |
| **Communication** | One-way: back to main agent only | Bidirectional: to lead, to other teammates, to you |
| **Interaction** | Cannot receive messages from outside | Can receive messages from any teammate or human |

---

## 4. Sub-Agents vs. Agent Teams — Complete Comparison

Anthropic's documentation provides a clear comparison table. Here it is explained in full:

### Sub-Agents

| Characteristic | Detail |
|---|---|
| **Own context** | Yes — each sub-agent has its own isolated context window |
| **Returns to caller** | Yes — results are returned to whichever agent spawned it |
| **Communication** | One-way only: back to the main Claude Code that called it |
| **Management** | Main agent manages all the work; sub-agents just execute |
| **Task type** | Focused, well-defined single tasks |
| **Result handling** | Summarizes results back to main context |
| **Token efficiency** | Relatively efficient — work offloaded, but sub-agent itself uses tokens |
| **Best used when** | You need quick, focused workers that report back |

### Agent Teams

| Characteristic | Detail |
|---|---|
| **Own context** | Yes — each teammate has a full, completely independent context window |
| **Returns to caller** | No — results don't automatically return anywhere; teammates are persistent |
| **Communication** | Multi-directional: teammates can message each other, message lead, message human |
| **Management** | Shared task list managed by the lead; teammates coordinate among themselves |
| **Task type** | Complex, interrelated work requiring collaboration |
| **Result handling** | Ongoing — teammates update shared task list, communicate progress |
| **Token efficiency** | Can be expensive — multiple full context windows running simultaneously |
| **Best used when** | Teammates need to share findings, challenge each other, and coordinate on their own |

### The Golden Rule from Anthropic's Docs

> **Use sub-agents** when you need quick, focused workers that report back.
> **Use agent teams** when teammates need to share findings, challenge each other, and coordinate on their own.

---

## 5. When to Use Agent Teams — Use Cases

### Use Case 1: Parallel Research

When you need to research multiple sources simultaneously:
- Send one agent to Wikipedia
- Send another to Stack Overflow
- Send others to different documentation sites

Each agent researches independently, possibly exchanging information between themselves, then brings back consolidated results. This is something sub-agents can also do, but teams enable the agents to share what they find as they go rather than just at the end.

### Use Case 2: Vertical Division — Independent Modules

When you have a system with clear module boundaries and you want separate agents working on each:
- One agent on the authentication module
- One on the payment module
- One on the reporting module

They can work truly independently without stepping on each other, while still having a communication channel for interface questions.

Previously you might have done this with multiple open terminals, but that means communication relies on them reading and writing `.md` files — which works but is "a little bit flaky" since it depends on agents consistently writing and reading at the right times. Agent teams provide a proper communication channel.

### Use Case 3: Horizontal Division — Layer-Based Teams

When you divide by technical layer rather than feature area:
- Frontend engineer agent
- Backend engineer agent
- LLM/AI engineer agent
- Database engineer agent
- DevOps agent
- Integration tester agent

This mirrors how human software engineering teams are often organized. The important design principle is that each agent has **non-overlapping responsibilities** — they can work independently most of the time, but still benefit from the ability to communicate when needed.

### The Key Design Balance

> *"You're ideally looking to give separate responsibilities to Claude agents so that they can work independently, and still have some benefit from communication between the agents so they can collaborate, but not so much communication that they start to grind down and they're churning with lots of backwards and forwards."*

Too much collaboration between agents defeats the purpose. The goal is maximum independence with just enough communication to stay coherent.

---

## 6. Setting Up Claude Agent Teams — Step by Step

### Prerequisites: Clean Environment

Before starting, ensure your project is in a clean state:
- Check `.claude/` — verify `agents`, `commands`, `skills` folders
- Ensure `settings.json` is clean (no leftover hooks from Day 1-2)
- Check `settings.local.json` for permissions
- Disable sandbox if it's active (for a vanilla setup)
- Verify no conflicting plugins are installed (`/plugin` → Installed)

### Step 1: Enable the Experimental Flag in `settings.json`

Open `.claude/settings.json` and add:

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  },
  "teamMode": "in-process"
}
```

**`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS: "1"`** — Enables the agent teams feature. If the feature has been made fully live since this recording, you may not need this flag.

**`teamMode`** has two options:
- `"in-process"` — All agents share the same terminal screen; you flip between them using keyboard shortcuts. Works on all platforms (Mac, Windows, Linux). **Use this one to start.**
- `"tmux"` — The screen splits into panels showing each agent simultaneously. Looks cooler but requires `tmux` installed (Mac/Linux only) or the `iTerm2` terminal emulator.

### Step 2: Choose and Install Relevant Plugins

For the FiNALLY project build, carefully selected plugins were installed:

**Good plugins to add:**
- **Frontend Design** — Adds instructions for making production-grade frontends that avoid the typical LLM aesthetic. Works by adding information to context, no sub-agents spawned.
- **Context7** — Adds current API documentation. Again, informational only.
- **Playwright** — Allows agents to spawn a browser and run Playwright integration tests.

**Plugins to avoid when using Agent Teams:**
- Anything that **itself spawns sub-agents** (e.g., Code Simplifier, Feature Dev) — this creates confusion and loss of control because you'll have nested agent invocations that are hard to track.

> *"I want to avoid plugins that themselves spawn sub-agents, or we're going to lose control."*

After installing plugins, **restart Claude Code** for them to take effect.

### Step 3: Update `claude.md` for Multi-Agent Context

All agents load `claude.md` at startup. This is your opportunity to give every agent the same foundational information. Update it to include:

- What has already been built (reference documentation paths)
- What still needs to be built
- Where to find detailed documentation (use **links, not `@` embedding**)

Example update:
```markdown
The key document is plan.md included in full below.
The market data components are already completed.
A summary is in `planning/market-data-summary.md`.
Detailed docs are in `planning/market-data/`.
Consult these docs only when required.
The remainder of the platform is still to be developed.
```

**Why use links instead of `@` embedding?** Using `@planning/architecture.md` inserts the entire file contents into the context immediately — often wasteful. A path reference lets each agent decide whether it needs that information and load it progressively when required.

### Step 4: Create a Git Branch for Safety

Always work on a separate branch before running agent teams:

```bash
git checkout -b agent-teams
```

This lets you see exactly what was built, push it to GitHub for review, and switch back to `main` cleanly if you need to start over:

```bash
git checkout main   # instantly reverts everything to baseline
```

### Step 5: Check Your Usage Baseline

Before starting, run:
```
/usage
```

Note the percentages (today's quota, week's quota, by model). This lets you measure exactly how much was consumed by the agent team run — important since it can be significant.

### Step 6: Craft the Team-Creation Prompt

You can let Claude figure out the team composition, or specify it explicitly. Here is the team created for the FiNALLY project:

```
Create an agent team to build the entire project. 
Team members:
- A frontend engineer to work on the frontend
- A backend engineer for all backend code
- A database engineer for all database code
- An LLM engineer for the LLM calls (should use the Cerebrace skill)
- All engineers should write unit tests for their area
- An integration tester to test end-to-end functionality
- A DevOps engineer to handle the Docker container

Please wait for your teammates to complete their tasks before proceeding.
```

**Why these specific team members?**
- Each has a clear, non-overlapping domain
- The "integration tester last" design mirrors real engineering — you can't test integration until components exist
- DevOps at the end makes sense — Docker is built after the code is written
- The explicit instruction to "wait for teammates to complete tasks" prevents the lead from doing all the work itself (a common failure mode mentioned in Anthropic's docs)

**Note on code reviewer agent**: The instructor considered adding a code review agent to check quality and give feedback, but decided against it:
> *"That's going to introduce something which is going to require a conversation with every single agent and more backwards and forwards. I feel like that's going to just add more noise than we would like."*

### Step 7: Enable Auto-Accept and Launch

Press `Shift+Tab` to cycle through modes. Ensure **"Accept edits on"** is active before sending the team creation prompt.

### Key Keyboard Shortcuts for Agent Teams

| Shortcut | Action |
|---|---|
| `Shift + Tab` | Cycle through modes (accept edits, plan mode, etc.) |
| `Shift + ↑` | Move to next agent (scroll up through team) |
| `Shift + ↓` | Move to previous agent (scroll down through team) |
| `Ctrl + T` | Toggle the task list view on/off |
| `Ctrl + C` (twice) | Stop Claude Code |

### Step 8: Shutting Down the Team

When work is complete:
- Ask the lead to shut down specific teammates: *"Ask the [name] teammate to shut down"*
- Clean up everything: *"Clean up the team"* — stops all running agents

---

## 7. Agent Teams in Action — Live Build of the FiNALLY Trading Platform

### What Was Built

Using Claude Agent Teams on the FiNALLY (finance ally) trading platform project — building the entire full-stack application from the existing market data backend foundation.

### How the Build Unfolded

**Phase 1: Exploration and Planning (~5 minutes)**
- The team lead starts by exploring the project state, reading all planning documents
- It then creates the team structure and assigns tasks with dependencies
- Task list becomes visible: some tasks blocked by others (dependency chains shown in the UI)

**Phase 2: Database and Frontend Start in Parallel**
- Database engineer kicks off first: building the SQLite database layer
- Frontend engineer also starts simultaneously
- Backend, LLM, DevOps engineers wait — correctly identified as blocked by database completion

**Phase 3: Serial Execution with Dependency Respect**
- The execution was more serial than expected — agents respecting dependencies carefully
- Database engineer completes → backend engineer starts
- Back end delivers: **121 passing tests, all green**
- Back end completes → LLM engineer unblocked
- Front end, DevOps, and LLM engineers then run in parallel (first time 4 agents active simultaneously)

**Observation on Serialization:**
> *"It's interesting that it is a bit more serial than I was expecting... That is a more structured, organized way of doing it that probably leads to better outcomes — a bit less chaotic and more managed."*

This was actually positive — it shows the lead made intelligent decisions about dependencies rather than blindly parallelizing everything.

**Phase 4: Integration Testing**
- DevOps, frontend, and LLM engineers complete
- Integration tester is the final agent spawned
- Integration tester found **5 API response mismatches** causing frontend crashes
- Team lead responds: "Good catch" — the integration tester then fixes the issues itself
- All teammates shut down gracefully
- Final summary: **6 agents, 6 tasks, all complete**

**Docker Note:** The DevOps agent noticed Docker wasn't running and launched it autonomously — this is an example of the kind of intelligent proactive behavior that newer models (Opus 4.6) can handle that older models couldn't.

### Approving Commands During Agent Teams

Unlike YOLO/sandbox mode, agent teams still occasionally ask for approval. Key decisions made:
- `chmod` commands to make scripts executable: **Approve once** (recurring operation, safe)
- Running tests: **Always approve** (predictable, important to see each time)
- Docker build: **Always approve** (significant operation worth watching)

Making smart choices between "approve once" and "always approve" is important — you want oversight without creating approval fatigue.

### The Result: A Working Trading Dashboard

After the team completed, running `scripts/start_mac.sh` launched the application at `localhost:8000`:

**What worked perfectly (zero-shot):**
- Live market data watchlist with flashing price updates
- Portfolio heat map showing position weights
- Real-time cash and portfolio value tracking
- Buying stocks by ticker (JPM, Google, Visa) updates the heat map instantly
- AI assistant responding to natural language: "Add SPY to the watch list" → done
- AI assistant executing trades: "Buy one share of V" → executed and appeared on heat map
- AI assistant giving advice: "Your portfolio is cash-heavy, consider rebalancing"
- AI assistant autonomous trading: "Please do this for me" → sold JP Morgan shares
- Portfolio P&L chart updating in real time

**Minor issues noted (non-blocking):**
- Price chart section not filling in for some tickers
- Portfolio PNL line occasionally static
- CSS layer overlap (cosmetic only)

**Overall assessment:** "An impressive setup." Six agents, built in approximately **30 minutes**, zero-shot success.

### Usage After Agent Teams

```
/usage
```
Result: Usage went from **8% → 9% of weekly quota** — a very modest cost for building a full-stack application.

---

## 8. GSD: Spec-Driven Design Meets Multi-Agent Orchestration

### What is GSD?

**GSD stands for "Get Sh\*t Done"** — a community-built, open-source framework that combines spec-driven design (SDD) with multi-agent orchestration to produce high-quality, well-tested applications.

- **Author**: An EDM/electronic dance musician based in LA (showing the breadth of who is building in this space)
- **GitHub**: Available as an open-source repository with significant community following
- **Platforms supported**: Claude Code, Open Code, Gemini CLI — works with any of the three

### The Philosophy Behind GSD

GSD was born from a frustration with the "vibe coding" pattern:

> *"Vibe coding has a bad reputation: you describe what you want, agents code, you get inconsistent garbage that falls apart at scale."*

GSD is the counter to that. It describes itself as:

> *"The context engineering layer that makes Claude Code reliable. It's for people who can describe what they want and have it built correctly — without pretending they're running a 50-person engineering org."*

### What Problem Does GSD Solve?

The core problem GSD targets is **context rot** — the quality degradation that happens as the context window fills up during a long coding session. As context gets full:
- The model loses track of earlier decisions
- Code becomes inconsistent with itself
- The model starts contradicting its own previous work

GSD solves this through:
1. **Carefully engineered prompts** — not just clever prompting, but systematically pre-prompted agents tuned for software development
2. **Structured state tracking** — maintains progress in a fixed set of markdown files that all agents read and update
3. **Phase-by-phase execution** — breaks large projects into phases, clearing context at phase boundaries
4. **Parallel agent spawning** — uses sub-agents (not Claude Agent Teams) to parallelize specific tasks within each phase

### GSD vs. Claude Agent Teams — Conceptual Distinction

| Aspect | Claude Agent Teams | GSD |
|---|---|---|
| **Type** | First-party Claude Code feature | Community-built orchestration framework |
| **Agent model** | Long-running teammates with persistent context | Sub-agents spawned per phase, then discarded |
| **Structure** | Defined by the team creation prompt | Fixed opinionated workflow with specific phases |
| **Communication** | Agents can message each other | Agents communicate through structured state files |
| **Customizability** | High — you define the team | Fixed steps: new, discuss, plan, execute, verify |
| **Context management** | Managed by Claude's built-in handling | Explicitly managed through GSD's phase system |

GSD is described as "similar to the agent teams concept... but more opinionated. It's got more constructs designed to put you into a particular way of doing it."

---

## 9. GSD Commands and Workflow

### Installation

GSD installs via a single command (from the GSD GitHub repo):

```bash
# Run this command from your project directory
# Then choose: Claude Code runtime, project-local installation
```

After installation, GSD creates a set of folders and files inside `.claude/`:
- `agents/` — pre-built sub-agent definitions
- `commands/` — the GSD slash commands
- `hooks/` — any GSD-specific hooks

This is similar to what a plugin installation does — dropping a pre-configured set of capabilities into your project.

### The GSD Phase Workflow

GSD is designed as a structured, sequential workflow through phases:

```
/gsd:new-project    →    /gsd:discuss-phase    →    /gsd:plan-phase
        ↓                                                    ↓
/gsd:verify         ←    /gsd:execute          ←    (review plan)
        ↓
/gsd:new-milestone (if more phases remain)
```

**Each phase produces structured markdown files in a `.planning/` folder:**

| File | Purpose |
|---|---|
| `project.md` | High-level project overview |
| `research.md` | Research done during initialization |
| `requirements.md` | Detailed requirements with unique IDs |
| `roadmap.md` | Phase-by-phase roadmap |
| `state.md` | Current state of all tasks |
| `plan.md` | Current phase's execution plan |
| `summary.md` | Summary of completed work |
| `todo.md` | Outstanding items |

### The GSD Commands Explained

**`/gsd:new-project`** — The starting command
- Initializes the project
- Spawns parallel MAPA (Multi-Agent Parallel Analysis) agents to analyze the codebase
- Agents read all existing code, documentation, and planning files
- Asks clarifying questions about the project
- Creates `requirements.md` with all requirements given unique IDs

**`/gsd:settings`** — Configure GSD behavior
- Set model quality: **Quality** (most capable), **Balance** (recommended), **Budget** (cheapest)
- Enable/disable parallel agents: plan researcher, plan checker, execution verifier
- This is where you ensure GSD uses Opus instead of defaulting to Sonnet

**`/gsd:discuss-phase`** — Shape the implementation
- An interactive dialogue about how each phase should be approached
- Can be skipped if you want to go straight to planning

**`/gsd:plan-phase [number]`** — Plan a specific phase
- Agents create a detailed plan for executing this phase
- Produces a `plan.md` with all steps, dependencies, and verification criteria

**`/gsd:execute`** — Execute the current phase
- Runs the plan with sub-agents doing parallel work where possible
- Shows context usage climbing as work progresses

**`/gsd:verify`** — Verify the work done
- Runs tests and checks, marks phase complete
- The manual verification step before moving to the next phase

**`/gsd:audit-milestone`** / **`/gsd:complete-milestone`** / **`/gsd:new-milestone`** — Milestone management commands for larger projects

**Quick mode** — Runs all steps (new, discuss, plan, execute, verify) in one shot if you don't need the individual planning steps.

### GSD's Key Design Philosophy: Skip Permissions Mode

GSD recommends running Claude in "dangerously skip permissions" (YOLO) mode:

> *"They recommend skip permissions mode running Claude with this. It's how it's intended to be used. Stopping to approve git commits 50 times defeats the purpose."*

If you're not comfortable with full YOLO mode: run it inside a sandbox (native or Sprites.dev) so that permissions are irrelevant because the environment itself is isolated.

---

## 10. GSD in Action — Building the FiNALLY Platform (5-Hour Deep Dive)

### Setup

Before starting:
- Remove the agent teams experimental flag from `settings.json` (starting fresh)
- Delete the `frontend/` folder contents (to start completely from scratch)
- Create a new git branch: `git checkout -b finally-gsd`
- Configure GSD to use **Quality** model (Opus) — use `/gsd:settings` and select Quality tier

### The Interactive Initialization Process

**Step 1: Run `/gsd:new-project`**

GSD immediately asks clarifying questions:

*"How polished does the frontend need to be for a course demo?"*
→ Answer: "Production quality — not a demo, really great"

*"For the LLM chat — should it work out of the box without an API key (mock mode), or require a real key?"*
→ Answer: "It should need a real key"

*"Should I build the Docker file and stop/start scripts, or just focus on app code?"*
→ Answer: "Include Docker for sure"

This interactive approach is notably different from agent teams where you just describe the goal and let it figure out the details.

**Step 2: GSD presents `requirements.md` for approval**

After analysis, GSD generates a comprehensive `requirements.md` with:
- Unique IDs for each requirement (e.g., `DB-001`, `API-003`, `UI-007`)
- A checklist structure
- Items explicitly deferred to V2/future release (enhanced visualization, social features, Terraform)

This is a valuable checkpoint: review the requirements, ensure nothing important is missing, confirm scope is appropriate.

**Step 3: GSD proposes the Roadmap**

The proposed roadmap had **10 phases**:
1. Database foundation
2. Portfolio and trade execution
3. Watch list
4. App assembly
5. LLM chat integration
6. Frontend foundation
7. Watch list (frontend)
8. Portfolio (frontend)
9. Chat interface (frontend)
10. Packaging and testing

**Notable design choices:**
- UI deferred until phases 6-9 (after backend is solid) — the instructor noted this was a better approach than what Claude Agent Teams did (which started with the UI)
- Chat integration near the end — makes sense, it depends on everything else
- Packaging and testing last — clean finale

### The Build Process

**Parallelism in GSD:**
Rather than Claude Agent Teams (long-running parallel instances), GSD uses **sub-agents spawned in parallel within each phase**. At the start of `new-project`, it spawns "MAPA agents" in parallel to analyze different aspects of the codebase. Within phases, it similarly spawns parallel workers for specific tasks.

**Context management in action:**
As phases progress, the main context window fills up. GSD's phase system helps manage this: each phase completes, context is effectively "reset" to a new starting point for the next phase (summary of previous phase in state files, not full history).

**Token usage tracking:**

| Checkpoint | Weekly Token Usage |
|---|---|
| Before GSD started | 8% |
| After new-project + planning phase 1 | 18% (10% consumed just for planning!) |
| After full completion | ~17% of weekly quota (second week) + 24% of daily quota |

This is approximately **10x the token consumption** of the Claude Agent Teams run.

**Time taken:**
- Planned 10 phases with plan + execute + verify for each
- Total time: **approximately 5 hours**
- The agent teams run took: **approximately 30 minutes**

### The GSD Experience

The instructor was present but hands-off, watching the process:
- GSD works in highly methodical, thorough sweeps
- Backwards and forwards confirming, double-checking, triple-checking tests
- Going back to fix issues it found during verification
- Very disciplined, very thorough — but agonizingly slow to watch

> *"When I saw it go backwards and forwards over confirming and double-checking and triple-checking that the tests were passing, it was clearly very thorough indeed. I see why it works well. But it's a lot of time spent and a lot of tokens spent as well."*

The instructor noted it could have been left running overnight — set it going before bed, wake up to a completed project. In that context, the 5-hour duration doesn't matter.

### Code Quality Notes

When inspecting the generated code:
- GSD used the Cerebrace skill for LLM inference (as instructed)
- However, it used Cerebrace + LangChain rather than pure Cerebrace
- Interpretation: It likely read the Cerebrace skill, started implementing it, hit a bug, and rewrote using a hybrid approach it was more confident about
- This is a known pattern — when models hit bugs they sometimes pivot to approaches they know work

---

## 11. GSD vs. Claude Agent Teams — Side-by-Side Comparison

### The UI Results

Both approaches built the same FiNALLY trading platform. Here is what each produced, viewed side-by-side:

#### Claude Agent Teams Result (30 minutes)

**What worked well:**
- Very polished UI with professional color scheme
- Beautiful heat map with colored position boxes (red/green showing P&L)
- Smooth live price updates on the watchlist
- Functional AI assistant (natural language add/buy/sell commands)
- Clean, non-generic-LLM aesthetic (frontend design plugin helped)

**Issues found:**
- Could not get prices for tickers not already on the watchlist (bug when buying new stocks)
- Price chart section occasionally didn't fill in properly
- Some CSS layering issues (cosmetic)

#### GSD Result (5 hours)

**What worked well:**
- Also very polished and professional looking
- Functional watchlist with live prices
- Working AI assistant (add IBM, buy 1 IBM, sell 5 META — all executed correctly)
- Better buy flow — could buy any ticker even if not on watchlist
- Remembered portfolio data between sessions (persistent SQLite database working)

**Issues found:**
- Heat map not color-coded based on P&L (just shows sizes, not colors)
- Some chart displays empty in certain states
- Slightly less dramatic visual treatment than agent teams version

### The Comparison Verdict

| Criterion | Claude Agent Teams | GSD |
|---|---|---|
| **Time to complete** | ~30 minutes | ~5 hours |
| **Token consumption** | ~1% of weekly quota | ~10% of weekly quota |
| **UI polish** | Slightly better (colorful heat map) | Good but simpler |
| **Functional quality** | Very good (minor watchlist bug) | Slightly better (handles new tickers correctly) |
| **Code thoroughness** | Good | Very thorough — exhaustive testing |
| **Predictability** | Somewhat unpredictable | Very methodical, predictable steps |
| **Appropriate use case** | Fast iterations, demos, time-sensitive work | Big projects, production quality, overnight runs |

**Final verdict from the instructor:**

> *"I give Claude Agent Teams a slight one step ahead of this... Despite the defects — which I think I could tell it to fix pretty quickly — the fact that it got the whole thing done in half an hour already speaks volumes to me."*

But acknowledging GSD's strengths for longer projects:

> *"When it's taking on a really big project, especially if you're willing to run it in YOLO mode and just leave it be — then it's clearly very, very diligent. It's a lot of time spent and a lot of tokens spent, but the result is very thorough."*

### When to Choose Each Approach

| Situation | Better Approach |
|---|---|
| Time-sensitive — need results in 30 minutes | **Claude Agent Teams** |
| Big project you can leave running overnight | **GSD** |
| Production code requiring exhaustive testing | **GSD** |
| Demo or course project | **Claude Agent Teams** |
| When cost is a concern | **Claude Agent Teams** |
| When thoroughness trumps speed | **GSD** |
| You want to interact with the process as it goes | **GSD** (more checkpoints) |
| You want maximum autonomy | **Both work, set YOLO mode** |

---

## 12. Day 4 Summary and Key Takeaways

### What Was Covered

1. **Theory of Swarms vs. Orchestration** — The continuum from wild swarms to structured orchestration; both are valid, the right balance depends on your project

2. **Claude Agent Teams** — Anthropic's experimental feature for running multiple long-lived Claude Code instances that communicate with each other and share a task list; enabled via `settings.json` experimental flag

3. **Sub-Agents vs. Agent Teams** — Clear conceptual distinction: sub-agents are short-lived focused workers; agent teammates are persistent collaborators with independent context and bidirectional communication

4. **Agent Teams Setup** — 8-step setup process including enabling the flag, installing appropriate plugins (avoiding sub-agent-spawning ones), updating `claude.md`, creating a git branch, crafting the team prompt, and knowing the keyboard shortcuts

5. **Agent Teams Build** — 30-minute zero-shot build of the FiNALLY trading platform with 6 agents, resulting in a working AI-powered trading dashboard with live prices, portfolio heat map, and natural language trading

6. **GSD Framework** — Community-built spec-driven orchestration: structured phases (new-project → discuss → plan → execute → verify), MAPA parallel agents for analysis, state tracking through markdown files, designed to solve context rot

7. **GSD Build** — 5-hour build of the same platform using GSD's methodical approach; ~10x more tokens consumed but very thorough — exhaustive testing, complete documentation, disciplined phase-by-phase execution

8. **Side-by-side comparison** — Both produced impressive, working trading platforms; Agent Teams faster and flashier; GSD more thorough and better for overnight/unattended runs

### The Big Picture

Day 4 completes the journey to Stages 7 and 8 of the coding agent evolution spectrum. The two approaches represent two fundamentally different philosophies:

- **Claude Agent Teams** = Trust the model to figure out structure, prioritizing speed and dynamism
- **GSD** = Impose structure on the model, prioritizing thoroughness and reliability

Neither is universally better. The right tool depends on what you're building, how much time you have, and what quality bar you're aiming for.

### Course Progress

**93% complete** — only the capstone Day 5 remains.

---

## Quick Reference

### Agent Teams `settings.json` Configuration

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  },
  "teamMode": "in-process"
}
```

### Agent Teams Keyboard Shortcuts

| Key | Action |
|---|---|
| `Shift+Tab` | Cycle modes (accept edits, plan mode) |
| `Shift+↑` / `Shift+↓` | Flip between team agents |
| `Ctrl+T` | Toggle task list |

### GSD Command Sequence

```
/gsd:new-project    → Initialize, map codebase, create requirements
/gsd:settings       → Configure model quality and agent toggles
/gsd:discuss-phase  → (Optional) Shape implementation approach
/gsd:plan-phase N   → Plan phase N in detail
/gsd:execute        → Execute current phase
/gsd:verify         → Verify and close phase
/gsd:new-milestone  → Move to next set of phases
```

### Agent Team Shutdown Commands

```
# Shut down one teammate
"Ask the [frontend] teammate to shut down"

# Shut down the entire team
"Clean up the team"
```

---

## Key Concepts Glossary

| Term | Definition |
|---|---|
| **Swarm** | Many agents running simultaneously with minimal structure — Stage 7 of the coding agent evolution |
| **Orchestration** | Agents with defined structure, hierarchy, and managed coordination — Stage 8 |
| **Claude Agent Teams** | Anthropic's experimental feature for coordinating multiple Claude Code instances with bidirectional communication |
| **Team Lead** | The primary Claude Code instance in an agent team; manages task assignment and coordination |
| **Teammate** | A Claude Code instance in an agent team with persistent context and ability to communicate with other teammates |
| **MAPA Agents** | Multi-Agent Parallel Analysis agents spawned by GSD to analyze different aspects of a codebase simultaneously |
| **GSD** | "Get Sh*t Done" — a community-built orchestration framework combining spec-driven design with multi-agent execution |
| **Context Rot** | The quality degradation that occurs as a Claude Code session's context window fills up during long projects |
| **Spec-Driven Design (SDD)** | An approach that creates a detailed specification first, then executes precisely against that spec |
| **`teamMode: in-process`** | Agent team display mode where all agents share one terminal, navigated with keyboard shortcuts |
| **`teamMode: tmux`** | Agent team display mode where the screen splits to show each agent simultaneously (Mac/Linux only) |
| **`/gsd:settings`** | GSD command to configure model quality (Quality/Balance/Budget) and parallel agent toggles |
| **Zero-shot success** | When something works correctly on the very first attempt without any iteration |
| **Phase (GSD)** | A bounded unit of work with its own discuss, plan, execute, and verify cycle |
| **`.planning/` folder** | The GSD-created directory containing all state-tracking markdown files |
| **`requirements.md`** | GSD-generated document with uniquely identified requirements and a completion checklist |
| **`roadmap.md`** | GSD-generated phase-by-phase breakdown of the entire project |
| **`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS`** | Environment variable that enables the agent teams experimental feature |
| **Task list** | The shared list of tasks in an agent team, visible via `Ctrl+T`, showing status and dependencies |
| **Blocked task** | A task in the agent team's list that cannot start until a dependency completes |
| **Approval fatigue** | The risk of mindlessly approving every Claude request without reading it — countered by sandboxing |

---

*End of Day 4 Notes — Week 3 of the AI Codec Course*
