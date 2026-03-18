# Claude Code — Week 3, Day 5: Complete Study Guide
### Gastown, Codex Sub-Agents, Final Deployment, Best Practices & Course Wrap-Up

---

## Table of Contents

1. [Day 5 Overview — The Finale](#1-day-5-overview--the-finale)
2. [Day 4 Recap — What We Proved](#2-day-4-recap--what-we-proved)
3. [The Orchestration Spectrum — Three Approaches Compared](#3-the-orchestration-spectrum--three-approaches-compared)
4. [Gastown — The Radical Orchestration Framework](#4-gastown--the-radical-orchestration-framework)
5. [Gastown Vocabulary — The Complete Glossary](#5-gastown-vocabulary--the-complete-glossary)
6. [Installing and Setting Up Gastown](#6-installing-and-setting-up-gastown)
7. [Gastown in Action — Building the FiNALLY Platform](#7-gastown-in-action--building-the-finally-platform)
8. [Gastown Internal Architecture — What's Running Under the Hood](#8-gastown-internal-architecture--whats-running-under-the-hood)
9. [Gastown Build Result — Two Attempts](#9-gastown-build-result--two-attempts)
10. [Gastown vs. Claude Agent Teams vs. GSD — Full Comparison](#10-gastown-vs-claude-agent-teams-vs-gsd--full-comparison)
11. [Codex Sub-Agents — The Experimental Parallel Feature](#11-codex-sub-agents--the-experimental-parallel-feature)
12. [The Ultimate Four-Way UI Comparison](#12-the-ultimate-four-way-ui-comparison)
13. [Final Trader Workstation — With Live Market Data](#13-final-trader-workstation--with-live-market-data)
14. [Deploying to the Internet in 15 Minutes](#14-deploying-to-the-internet-in-15-minutes)
15. [Running Multiple Coding Agents Together (tmux Quad Setup)](#15-running-multiple-coding-agents-together-tmux-quad-setup)
16. [The Andrej Karpathy Tweet — Revisited](#16-the-andrej-karpathy-tweet--revisited)
17. [Course Best Practices — Final Summary](#17-course-best-practices--final-summary)
18. [The Progression: Vibe Coder → Vibe Engineer → Agentic Engineer](#18-the-progression-vibe-coder--vibe-engineer--agentic-engineer)
19. [Complete Course Recap — All Three Weeks](#19-complete-course-recap--all-three-weeks)
20. [Final Key Takeaways](#20-final-key-takeaways)

---

## 1. Day 5 Overview — The Finale

Day 5 of Week 3 is the **final day** of the entire three-week course — described as the "tearful finale." It is the moment the roller-coaster comes all the way down.

### What's Covered Today

The day is packed with content spanning multiple tools and a complete course wrap-up:

- **Gastown** — Steve Yegge's radical orchestration framework that pushes Stage 8 to an entirely new extreme
- **Codex Sub-Agents** — OpenAI's experimental parallel agent feature built into Codex
- **Four-way UI comparison** — GSD, Claude Agent Teams, Gastown, and Codex results shown side by side
- **Live market data integration** — Switching from simulated to real Polygon/Massive market data
- **Deployment to the internet** — Using Fly.io to deploy the containerized app in 15 minutes
- **tmux quad terminal setup** — Running multiple coding agents simultaneously
- **Best practices summary** — The complete "missing manual" for agentic engineering
- **Course recap and graduation** — From vibe coder to agentic engineer

---

## 2. Day 4 Recap — What We Proved

Before diving into Day 5, the instructor reviews what was achieved on Day 4 to set context for why Gastown matters.

### What Was Built on Day 4

Two complete builds of the FiNALLY trading platform were accomplished:

**Build 1 — Claude Agent Teams (30 minutes)**
- 6 agents working in sequence and then parallel
- Beautiful result with a colored heat map, live prices, AI assistant
- Minor bugs: pricing for new tickers not on watchlist
- Cost: approximately 1% of weekly token quota

**Build 2 — GSD (5 hours)**
- Methodical phase-by-phase execution
- Very thorough with exhaustive testing and documentation
- Slightly different but equally professional UI
- Better ticker handling than Agent Teams version
- Cost: approximately 10% of weekly token quota

### Key Insight from Day 4

> *"Remembering that both of these cases are zero shots. We didn't do any debugging ourselves. We didn't come back and say 'this is a bug.' Both of these are just the first time we brought it up after giving it all of those instructions. And they're huge amounts of code. It's extraordinary."*

Both outcomes were extraordinary given the complexity involved — full-stack applications with live data, AI chat, portfolio management, and Docker containers, all built in a single pass.

### The Eight Stages — Where We Landed

The course referenced Steve Yegge's eight-stage chart for coding agent evolution:

- **Stage 6**: Multi-agent workflows (where we spent most of Week 3)
- **Stage 7**: Swarms — many agents running at once (we skipped directly past manual management)
- **Stage 8**: Orchestration — LLMs managing the coordination between agents

The instructor notes: "We sort of jumped straight to Stage 8, which is the right way to do it." Rather than manually managing 10+ agents (Stage 7), the frameworks (Claude Agent Teams, GSD) manage the agents automatically.

And Steve Yegge built that eight-stage chart specifically to introduce **Gastown** — something that takes Stage 8 to a completely different extreme.

---

## 3. The Orchestration Spectrum — Three Approaches Compared

Before introducing Gastown, here is a clear mental model of where each approach sits on the spectrum:

```
Most Controlled & Slow ←————————————————————→ Most Chaotic & Fast

     GSD          Claude Agent Teams         Gastown
  (5 hours)          (30 minutes)           (~30 min)
Serial/careful    Semi-parallel          Fully parallel
Plan→Execute      Structured teams       8+ concurrent agents
→Verify each      Auto-coordinated       Merge queue system
```

### GSD (Most Controlled)
- Clear phases: new → discuss → plan → execute → verify
- Triple-checks everything before proceeding
- Uses markdown files for state tracking
- Most time-consuming, most thorough
- Ideal for: big projects, overnight runs, when thoroughness matters most

### Claude Agent Teams (Middle Ground)
- Long-lived agents with persistent context
- Structured team lead + teammates with communication channels
- Shared task list with dependency management
- Fast (~30 min) with good results
- Ideal for: most practical builds, demos, time-sensitive work

### Gastown (Most Chaotic)
- Potentially 20-30 agents running simultaneously
- Purpose-built role specialization (polecats, refinery, witness, mayor)
- True maximum parallelism — everything at once
- Faster than Claude Agent Teams in absolute terms
- Ideal for: complete fresh builds, when raw speed matters, when you're comfortable with controlled chaos

> *"If you've got GSD on one end and you've got agent teams here, well, then Gastown is like way over there by a mile."*

---

## 4. Gastown — The Radical Orchestration Framework

### What Is Gastown?

Gastown is an orchestration framework built by **Steve Yegge** — the same person who wrote the influential eight-stage blog post about coding agent evolution. It is his personal product built on top of an underlying infrastructure he also created called **Beads**.

Gastown describes itself as a **workspace manager** — but really it's a sophisticated set of wrappers around Claude Code (or any coding agent) that enables running 20+ agents simultaneously in an organized hierarchy.

Other descriptions it uses for itself:
- "A new IDE construct" — it's trying to replace the concept of an IDE
- "A fancy set of fabrics built around coding agents"
- A system for "controlled chaos when you have 20 agents"

### The Core Problem Gastown Solves

Just like GSD, Gastown is solving the problem of **context management and agent coordination at scale**. But where GSD solves it through careful serial execution, Gastown solves it through:

1. **A strict hierarchy** — mayor → polecats, each with defined roles
2. **A mailbox communication system** — agents communicate through managed mail rather than direct context sharing
3. **A merge queue** — handles the Git conflicts that inevitably arise when 8+ agents work on the same codebase simultaneously
4. **A witness monitor** — watches all agents and notifies the mayor if anything goes wrong
5. **A refinery** — a dedicated agent whose only job is processing merge requests

### Gastown Is Agent-Agnostic

Like GSD, Gastown is not tied to Claude Code. It can work with any coding agent CLI. Steve Yegge built it first around Claude Code but designed it to be portable.

### Who Should Use Gastown

The instructor is direct about this: Gastown is **optional** and comes with a warning:

> *"I recommend you watch me do it and use it as a way to get a sense of what this is all about. If you really wish to, then for sure you can replicate what I do. But be warned — it's a bit chaotic, it's a bit of madness. If it doesn't work out for you, then I would just move on."*

Prerequisites for using Gastown comfortably:
- Comfort with terminal/command-line tools
- Understanding of tmux (terminal multiplexer)
- Familiarity with Git merge requests/branches
- Tolerance for ambiguity and "controlled chaos"

---

## 5. Gastown Vocabulary — The Complete Glossary

Gastown has its own complete vocabulary. Understanding these terms is essential before working with it.

### Core Concepts

| Term | Definition |
|---|---|
| **Town** | Your entire Gastown workspace — the overarching environment where everything lives. Stored in a `~/GT` directory in your home folder. |
| **Rig** | A single project within Gastown. Each project you work on is a rig. Example: `fin` (short for FiNALLY). |
| **Crew** | A named workspace/identity within a rig. Like a developer's named workspace. Example: `ed` is a crew working in the `fin` rig. |
| **Mayor** | The primary Claude Code instance that you directly interact with. The mayor receives your instructions, coordinates the polecats, and manages the overall operation. You never talk to polecats directly — you talk to the mayor. |
| **Polecat** | A worker agent. Each polecat gets assigned specific tasks (beads) and works on them. You'll typically have 6-8+ polecats running simultaneously. Named automatically: chrome, rust, fury, guzzle, nitro, shiny, thunder, dust, etc. |
| **Bead** | A single unit of work — similar to a GitHub issue or JIRA ticket. Each bead has a unique ID and represents one task. Example: `fin-001`, `fin-002`. |
| **Convoy** | A bundle of beads (tasks) that gets "slung" to polecats to work on. A phase of work is organized as a convoy. |
| **Refinery** | A special dedicated agent responsible only for processing merge requests (MRs). It sits idle until a polecat completes work and submits an MR, then it merges the work into the main branch. |
| **Witness** | A monitoring agent that watches all running polecats and notifies the mayor if anything goes wrong. |
| **Merge Queue** | The queue of merge requests waiting to be processed by the refinery. When multiple polecats finish simultaneously, their MRs queue up here. |
| **Beads Ledger** | The underlying infrastructure (also built by Steve Yegge) that tracks all tasks/beads with IDs — similar to a GitHub Issues list but integrated into the Gastown workflow. |
| **Sling** | The verb used in Gastown for assigning work. "Sling the work to polecats" means distribute the tasks to the worker agents. |

### The Key Relationship

```
You (human)
    ↕ (natural language)
  Mayor  ←→  Mailbox  ←→  Polecats (chrome, rust, fury, guzzle...)
    ↓                          ↓
  Town/Rig                Merge Queue
    ↓                          ↓
  Beads Ledger            Refinery (merges work)
                               ↓
                          Witness (monitors all)
```

### In Plain Language

- You tell the **mayor** what you want to build
- The mayor creates **beads** (tasks) and a **convoy** (bundle of tasks)
- The mayor **slings** the convoy to multiple **polecats** (workers)
- All polecats work **in parallel** on their assigned beads
- As each polecat finishes, it submits an **MR** (merge request) to the **merge queue**
- The **refinery** processes the merge queue, resolving any conflicts
- The **witness** monitors everything and alerts the mayor if anything breaks

---

## 6. Installing and Setting Up Gastown

### Installation

**Mac:**
```bash
brew install gastown
```
This automatically installs Gastown plus the Beads infrastructure it depends on.

**PC (PowerShell):**
```powershell
# Command from the Gastown GitHub repo
# Run in PowerShell or WSL
```

For the best Windows experience, use **WSL** (Windows Subsystem for Linux) and run **tmux** inside it. The full Gastown experience requires tmux — without it you can still use Gastown but won't see all agents visually.

### Complete Setup Process

**Step 1: Initialize the Gastown workspace**
```bash
# Initialize in your home directory, using Git
gt init ~/GT --git
cd ~/GT
```
This creates the `~/GT` folder which becomes your "town" workspace.

**Step 2: Create a rig (project)**
```bash
gt rig add fin   # "fin" is the rig name (project name)
# You'll be prompted for a GitHub repo URL
# Example: github.com/yourusername/fin
```

**Step 3: Create a crew (workspace identity)**
```bash
gt crew add ed --rig fin   # "ed" is the crew name
```
Output confirms: crew `ed` is now working in rig `fin`.

**Step 4: Navigate to the crew directory**
```bash
cd ~/GT/fin/crew/ed
```
Inside this directory you'll find your GitHub repo has been cloned, plus a file called `spec` (the specification file).

**Step 5: Add your spec/plan**
The `spec` file is where Gastown reads your project specification. Copy your `plan.md` content into it:
```bash
# Copy your planning document to the spec file
cp /path/to/plan.md spec.md
```

**Step 6: Launch the mayor**
```bash
gt mayor attach
```
This launches Claude Code as your mayor. The terminal now looks like a normal Claude Code session, but it's running as the Gastown mayor.

On first launch, the mayor says: *"No homework, no mail, inbox is empty, waiting for instructions."*

---

## 7. Gastown in Action — Building the FiNALLY Platform

### The Challenge

Gastown was given a **harder challenge** than Day 4's builds:
- Day 4 builds started with the existing market data backend already in place
- Gastown was given **only the spec/plan.md** — a completely blank repo with just the specification
- This means building everything from absolute scratch, including the market data simulator

> *"The challenge we've given it, just the specification, is a bigger harder challenge than the challenges that we did yesterday because we haven't included the market data implementation. This is completely blank. We've really had to do everything from scratch to see whether it can pull it off."*

### How to Launch the Build

Once in Claude Code as the mayor, give the instruction in natural language:

```
Build the entire project as described by spec.md.
File the issues, create a convoy, and sling the work to polecats.
```

The terminology in this prompt is important — it tells the mayor exactly what Gastown workflow to follow: create beads (issues), bundle them into a convoy, and distribute to polecats.

The mayor then:
1. Reads the spec.md thoroughly
2. Creates individual beads for each task (you'll see `fin-001`, `fin-002`, etc.)
3. Groups beads into a convoy
4. Slings the convoy to polecats
5. Multiple polecats start running simultaneously

### What You See During the Build

The Gastown experience is deliberately chaotic-feeling:

- The mayor terminal shows minimal output while polecats run in the background
- You can check on polecats by pressing `Ctrl+B` then `W` (in tmux) to see all running sessions
- You'll see sessions named: `chrome`, `rust`, `fury`, `guzzle`, `nitro`, `shiny`, `thunder`, `witness`, `refinery`, etc.
- Each is a separate Claude Code instance doing its assigned work

**Asking the mayor for a status update:**
```
Check on the polecats
```

The mayor responds with something like:
> *"Backend foundation: closed, merged. Polecat rust: already done. fin-wmw is in the merge queue, status ready. Polecat chrome is done, pushed its branches, wrapping up, waiting to submit its MR to the merge queue."*

This is Gastown-speak for: some work is done, some is in the process of being merged, some is still running.

### Navigating tmux During the Build

Gastown requires tmux to see the full picture of what's happening:

```bash
# List all running tmux sessions
Ctrl+B then W      # Shows all sessions in a menu

# Navigate between sessions
Ctrl+B then arrow  # Move between split panes
```

What you'll see in tmux:
- Many sessions running simultaneously
- One session for each polecat (chrome, rust, fury, guzzle, etc.)
- Sessions for witness and refinery
- The mayor session (your main interface)

> *"The thing about Gastown is you just go with it. This is the most disruptive and chaotic of all of them, and you just kind of go with the flow."*

---

## 8. Gastown Internal Architecture — What's Running Under the Hood

### The Refinery — How Merge Conflicts Are Handled

When 8+ agents all work on the same codebase simultaneously, **merge conflicts are inevitable**. This is a classic software engineering problem that Gastown solves with the refinery:

**How it works:**
1. Each polecat works on its own Git branch
2. When a polecat finishes, it creates a merge request (MR) and adds it to the merge queue
3. The refinery watches the merge queue
4. When an MR appears, the refinery processes it — merging the branch into main and resolving any conflicts
5. The refinery then notifies the mayor that the merge is complete

**Why the refinery sits idle for long periods:**
The refinery has nothing to do until polecats start finishing. Early in the build, everything is in flight. The refinery only activates when MRs start arriving.

### The Witness — Monitoring System

The witness is a background monitoring agent with one job: watch all polecats and notify the mayor if anything goes wrong.

An error the instructor encountered — "decon session won't stay up" — was the witness/decon monitoring layer having an issue. The mayor confirmed:

> *"Minimal implications — the witness is still running. What we lose is the ability to watch multiple projects if they were running, but we only have one so it doesn't matter."*

This demonstrates Gastown's **graceful degradation** — even if monitoring components have issues, the actual work (polecats running, refinery merging) continues unaffected.

### The Gastown Dashboard

Gastown provides a visual dashboard showing all running processes:
- Each polecat shown with a colored indicator (green = running, red = stopped/error)
- Status of the refinery and witness
- Phase tracking

The instructor notes seeing: *"chrome, fury, guzzle, nitro, refinery, rust, shiny, thunder — all on the go... It's quite bewildering but I'm confident that work is happening."*

### Phase Structure in Gastown

Gastown organizes work into phases, similar to GSD:
- Phase 1 polecats run first
- When phase 1 polecats complete and their MRs are merged, phase 2 beads "unlock"
- The mayor then slingsphase 2 to new (or reused) polecats
- This continues until all phases are complete

The difference from GSD: phases in Gastown run their internal tasks **fully in parallel**, whereas GSD's phases are more sequential internally.

---

## 9. Gastown Build Result — Two Attempts

### First Attempt: Failed

The first attempt resulted in a blank page — "page cannot be displayed." The build appeared to complete but the application didn't run properly.

**Response:** Rather than diagnosing it manually, the instructor simply told the mayor:

```
There's nothing there. Please just go ahead and fix it.
Sling your tasks. Get the polecats involved. Let's make this happen.
```

The mayor immediately relaunched all the polecats, the entire build cycle ran again, and the second attempt worked.

### Second Attempt: Success

The second run produced a working trading platform. Key points:
- Built **from absolute scratch** (no market data foundation given)
- Despite having no prior code, it built a complete market data simulator plus the full trading platform
- The entire rebuild took approximately 30 minutes

### The Result

A working trading platform including:
- Watch list with live simulated prices for multiple tickers
- Click on a ticker → price chart appears on the right
- Buy stocks: "Apple, quantity 3, buy" → Apple appears in portfolio heat map
- Buy stocks: "Netflix, quantity 4, buy" → portfolio updates
- AI chat working: "Please buy three shares of JPM" → executes and JP Morgan appears green in portfolio

The AI chat response to a buy order:
> *"Sure, I will place an order. Bam, look at that. JP Morgan appears here, nice and green. The AI chat works. That's absolutely amazing."*

**Was it truly zero-shot?** Not exactly — it required two attempts. But:
- No human debugging was done between attempts
- No feedback about what went wrong was given
- Just "go fix it" — and it fixed itself completely
- Starting from a completely empty repo with just a spec

---

## 10. Gastown vs. Claude Agent Teams vs. GSD — Full Comparison

### The Three Orchestrators on a Single Spectrum

| Dimension | GSD | Claude Agent Teams | Gastown |
|---|---|---|---|
| **Philosophy** | Spec-driven design, structured phases | Persistent team members with communication | Maximum parallel chaos with hierarchy |
| **Speed** | Slowest (~5 hours) | Fast (~30 min) | Fastest (also ~30 min but built more) |
| **Parallelism** | Mostly serial (some overlap) | 2-4 agents concurrent max | 6-8+ agents fully concurrent |
| **Control** | Maximum — human checkpoints at each phase | Moderate — you can interact anytime | Minimum — you mostly watch and ask status |
| **Predictability** | High — step-by-step, auditable | Moderate — somewhat unpredictable | Low — you're going with the flow |
| **Token cost** | Highest (~10x Claude Agent Teams) | Moderate | Moderate (similar to Agent Teams) |
| **State tracking** | Structured markdown files in `.planning/` | Shared task list in Claude Code | Beads ledger + Git branches |
| **Conflict handling** | N/A (mostly serial) | Agent Lead manages conflicts | Dedicated refinery agent |
| **Communication** | Through state files | Bidirectional messages between teammates | Mayor ↔ polecats via mailbox system |
| **Merge management** | Manual | Handled by Claude Code | Dedicated refinery + merge queue |
| **Best for** | Big projects, quality-critical work | Most practical builds, demos | Fresh builds, maximum speed, raw power |
| **Works with** | All coding agent CLIs | Claude Code only | All coding agent CLIs |
| **Experience** | Methodical, reassuring | Exciting but somewhat controlled | Bewildering but impressively fast |

### The Instructor's Personal Rankings

**Favorite to work with:** Claude Agent Teams
> *"It was the one that gave me the experience of a lot of power without feeling like I was completely out of control."*

**Best final result (this day):** Codex (see next section)

**Best for big production projects:** GSD

**Most impressive raw capability:** Gastown

---

## 11. Codex Sub-Agents — The Experimental Parallel Feature

### What Are Codex Sub-Agents?

Parallel to Anthropic's experimental Claude Agent Teams feature, OpenAI has built an equivalent experimental feature into **Codex** called **sub-agents** — not to be confused with Claude Code's sub-agents (which are different).

The Codex sub-agents feature:
- Allows Codex to spawn multiple parallel agent instances to work on different parts of a task simultaneously
- Designed to "parallelize the work and win in efficiency" (as described in the feature toggle)
- Experimental — accessed through the `/experimental` slash command menu in Codex

### How to Enable Codex Sub-Agents

```bash
# Start Codex in YOLO mode (in a Sprites.dev sandbox)
codex --yolo

# Inside Codex, bring up the slash command menu
/

# Navigate to experimental features
/experimental

# Toggle on the sub-agents feature:
# "sub-agents: ask codex that spawn multiple agents to 
#  parallelize the work and win inefficiency"
```

### Important Notes About Codex

- **`--yolo` flag** in Codex is equivalent to Claude's `--dangerously-skip-permissions`
- Codex uses `agents.md` NOT `claude.md` — if you're switching from Claude Code to Codex, **rename `claude.md` to `agents.md`**
- The build was run inside a **Sprites.dev sandbox** (remote fly.io environment) for safe YOLO execution
- Port proxying from Sprites: `sprite -s finally-worker proxy 8003` maps the remote port to local

### The Codex Build

**Setup used:**
```bash
# Connect to Sprites.dev sandbox
sprite -s finally-worker console

# Navigate to the project
cd finally
git status   # Confirm on branch "codex"

# Start Codex in YOLO mode with sub-agents
codex --yolo
```

**The prompt:**
```
Check out plan.md and build the entire project.
```

**Result:**
- Build completed in approximately **15 minutes** — the fastest of all approaches
- Deployed to port 8003 on the Sprite

**To view the result locally:**
```bash
# On local machine
sprite -s finally-worker proxy 8003
# Now browse to localhost:8003
```

### Codex Sub-Agents Result

The Codex result was declared the surprise winner by the instructor:

> *"I've got to tell you that actually the Codex implementation, Codex 5.3, is perhaps my personal winner. A late-breaking surprise."*

**Why Codex won:**
- Built in just 15 minutes (fastest of any approach)
- Produced a noticeably different and improved UI
- Live portfolio P&L chart updated in real time (none of the Claude versions consistently did this)
- Sleek, professional look with a different aesthetic
- Dark mode + light mode toggle (Claude added this unprompted!)

**Notable difference:** Codex was the only build that didn't have access to the Cerebrace skill (the custom LLM inference skill). Yet it still figured out how to make everything work — it just used a different approach for LLM calls.

---

## 12. The Ultimate Four-Way UI Comparison

The instructor assembled all four trading platform UIs simultaneously to compare them:

### GSD Version (5 hours)
- **Appearance:** Professional, slightly less flashy
- **Functionality:** Working watchlist, AI chat executes trades correctly
- **Strength:** Handles new tickers being added to watchlist smoothly
- **Weakness:** Heat map not color-coded by P&L; some chart displays have issues
- **Notable:** More robust ticker handling than other versions

### Claude Agent Teams Version (30 minutes)
- **Appearance:** Visually dynamic, beautiful colored heat map, live price flashing
- **Functionality:** Working watchlist, AI assistant, portfolio tracking
- **Strength:** Most visually impressive of all Claude versions
- **Weakness:** Bug — couldn't price tickers not already on watchlist when buying
- **Notable:** The front-end design plugin made a visible difference in UI quality

### Gastown Version (~30 minutes, 2 iterations)
- **Appearance:** Very similar to Agent Teams result (same model, same spec)
- **Functionality:** Working watchlist, heat map, AI chat
- **Strength:** Built entirely from scratch with no foundation code
- **Weakness:** Standard implementation without unique differentiators
- **Notable:** The fact it built the full market data simulator from nothing is impressive

### Codex Sub-Agents Version (15 minutes) — The Winner
- **Appearance:** Different look — sleek, black, professional, with unique design touches
- **Functionality:** All features working; portfolio P&L updates live (unique!)
- **Strength:** Fastest build + live updating portfolio + light/dark mode toggle
- **Weakness:** One minor display issue with some stats
- **Notable:** Dark mode / light mode toggle added spontaneously by Codex

### Why They All Look Similar

An interesting observation: all four platforms look remarkably similar despite different orchestration approaches. The reason:

1. All used the same underlying model (Claude Opus 4.6 or similar)
2. All started from the same `plan.md` specification document
3. The spec was detailed enough to guide similar UI decisions
4. The model has strong internal priors about what a trading dashboard should look like

> *"It was Opus 4.6 building all of these — just orchestrated differently."*

---

## 13. Final Trader Workstation — With Live Market Data

### Switching from Simulated to Real Market Data

After the Codex build completed, the next step was connecting the application to real live market data using the **Polygon API** (referred to as "Massive" in the course).

**The challenge:** Simply adding the Polygon API key didn't work immediately because the code had a hardcoded key issue.

**The solution using Codex:**
```
Please fix the API key integration and connect to the real Polygon/Massive market data
```

Codex found the problem (hardcoded key in the wrong place), fixed it, and then proactively told the user:

> *"Codex told me: 'Hey, you realize it's after trading hours? So it's going to be a bit static. There'll be a bit of after-hours movement.' And of course Codex was exactly right."*

### What the Final Platform Shows

The completed FiNALLY Trader Workstation with live data:

**Watch List Panel (Left):**
- 60 real stock tickers organized by sector:
  - Tech (AAPL, MSFT, GOOGL, META, AMZN, NVDA, etc.)
  - Financials (JPM, GS, BAC, etc.)
  - Healthcare
  - Consumer
  - Industrials
  - Energy
- Live price updates from Polygon API during market hours
- After-hours shows occasional changes from after-hours trading activity

**Main Chart (Center):**
- Click any ticker → that ticker's live price chart appears
- Real-time price history display

**Portfolio Heat Map (Right):**
- Boxes sized by position dollar weight
- Color-coded by P&L (green = up, red = down)
- Updates live as market prices change

**Portfolio P&L (Bottom):**
- Real-time overall portfolio profit/loss
- Updates continuously

**AI Chat (Side panel):**
- Natural language trading: "Please buy 3 shares of JPM"
- Add to watchlist: "Add IBM to watch list"
- Portfolio analysis: "Give me trading advice"

**Dark/Light Mode Toggle:**
- Switch between dark (gamer-style) and light (Bloomberg-style professional) mode
- Added spontaneously by Codex — not requested

### The Scale of What Was Built

> *"If you had shown me this a couple of years ago and asked me how long it would take to build this — I probably would have said this would take me a month or two. I would have charged a fair amount of money for this."*

This is a real, functional financial application:
- Real-time market data integration
- Portfolio management with buy/sell
- AI-powered natural language trading interface
- Heat map visualization
- Professional-grade UI with light/dark modes
- Dockerized for easy deployment

The only things missing for true production:
- User authentication/login system
- Production security hardening

Both of which are straightforward additions at this point.

---

## 14. Deploying to the Internet in 15 Minutes

### The Deployment

After completing the build, a 15-minute conversation with Codex resulted in the application being deployed live on the internet.

**The conversation:**
```
What's the best place to deploy this on the internet?
```

Codex recommended **Fly.io** (the company behind Sprites.dev) as the ideal choice for deploying the existing Docker container as-is.

**What happened:**
1. Codex wrote a deployment script
2. The script was run in the terminal
3. Environment variables were configured correctly (Polygon API key, etc.)
4. Application deployed and running live

**The live URL:**
```
https://finally-ed.fly.dev
```

### What Was Live at That URL

The fully deployed application at `finally-ed.fly.dev`:
- AI chat working
- Portfolio management working
- Live market data updating
- All environment variables configured correctly
- Running as a Docker container on Fly.io infrastructure

### Deployment Taking 15 Minutes — What That Means

This used to require significant DevOps expertise:
- Setting up a cloud provider account
- Configuring infrastructure
- Writing deployment manifests
- Managing environment variables
- Handling container registries

Now: a 15-minute conversation with a coding agent handled all of it.

> *"Deploying a container is relatively easy. They'll walk you through the instructions and help you make any decisions you need to make about which vendor you use, and then you can have this live on the internet."*

---

## 15. Running Multiple Coding Agents Together (tmux Quad Setup)

### The Final Power Move

After all the orchestrated builds, the instructor revealed one more advanced technique: running multiple **different** coding agents simultaneously, each potentially with their own sub-agents.

### The tmux Quad Setup

Using Sprites.dev + tmux, a four-panel terminal was set up:

```bash
# Connect to Sprite
sprite -s finally-worker console

# Attach to the existing quad tmux session
tmux attach -t quad
```

**The four quadrants:**
```
┌─────────────────┬─────────────────┐
│  Codex (YOLO)   │  Claude (--dsp)  │
│  + sub-agents   │  + agent teams  │
│  Backend/Data   │  UI/Frontend    │
├─────────────────┼─────────────────┤
│  Codex (YOLO)   │  Git Terminal   │
│  (Second agent) │  (Version ctrl) │
└─────────────────┴─────────────────┘
```

**Navigation in tmux:**
```bash
Ctrl+B then →    # Move to right panel
Ctrl+B then ↓    # Move to bottom panel
Ctrl+B then ←    # Move to left panel
Ctrl+B then ↑    # Move to top panel
```

### How They Were Used Together

- **Top Left (Codex + sub-agents):** Backend work and market data integration
- **Top Right (Claude + agent teams or sub-agents):** UI/Frontend work
- **Bottom Left (Second Codex):** Additional backend/testing work
- **Bottom Right (Git terminal):** Version control, committing and tracking changes

### The Human's Role

The instructor acted as the coordinator/boss across all three coding agents:
- Gave each agent its task area
- Occasionally asked them to review each other's work
- Used markdown files to track state across all three
- Never dug into the code directly
- Just directed traffic

> *"I've always been the boss. I've just been telling them what to do. I've not dug into the code. I've just asked them to look at things and occasionally review each other's stuff too. So powerful."*

### The "10x Then Bugs" Reality Check

An important honest reflection from the instructor about multi-agent development:

**The experience often goes like this:**
1. Start a session → feeling like you're 10x productive
2. Progress feels amazing, agents are humming
3. Hit a bug → agents keep cycling on it, can't break through
4. Feel like time is being wasted
5. Eventually break through

**The mindset to maintain:**
> *"Even when you factor that in, the amount of time that it's taken me to make lots of progress in a couple of hours is still multiple times — two or three times faster than if I was writing all this myself. So never be surprised when that initial 10x then gets pulled back by some bugs. Keep in mind it's still a significant net positive."*

**The bug-debugging discipline:**
When agents get stuck on a bug, the right process is:
1. Carefully **reproduce** the issue (get it to consistently fail)
2. **Understand** the issue (not just try random fixes)
3. Write a **markdown file** explaining the issue precisely
4. **Fix** it
5. **Test and prove** you fixed it
6. Sometimes discover: "the problem is still there" → repeat

This process takes time. Expect it. Plan for it. It's part of the new way.

---

## 16. The Andrej Karpathy Tweet — Revisited

### The Tweet That Started the Course

The entire course was inspired by a tweet from **Andrej Karpathy** (former Tesla AI Director, OpenAI founding member):

> *"I've never felt this much behind as a programmer. Professions being refactored as the bits contributed by a programmer are becoming sparse. I could be 10 times more powerful if I could just string together everything has become available.*
>
> *There's a new layer of abstraction to master with agents, sub-agents, their prompts, context, memory, modes, permissions, tools, plug-ins, skills, hooks, MCP, LSPs, slash commands, workflows, IDEs and the need to build an all-encompassing mental model for the strengths and pitfalls of fundamentalistic, stochastic, fallible, unintelligible and changing entities.*
>
> *Clearly, a powerful alien tool was handed around except it comes with no manual and everyone has to figure out operated. While the resulting magnitude 9 earthquake is rocking the profession, roll up your sleeves to not fall behind."*

### What This Tweet Meant at the Start of the Course

At the beginning of the course, this tweet felt like a foreign language:
- What are agents, sub-agents, hooks, MCP, LSPs, skills?
- What are these "stochastic, fallible, unintelligible entities"?
- How do you build a mental model for all of this?

### What This Tweet Means at the End of the Course

By Day 5, every single term in this tweet has been learned, experienced, and practiced:

| Term in Tweet | What You Now Know |
|---|---|
| **Agents** | Claude Code instances doing autonomous work |
| **Sub-agents** | Focused worker instances that report back to main Claude |
| **Their prompts** | Crafting effective prompts, agents.md, claude.md |
| **Context** | Context window management, /context, /clear, context rot |
| **Memory** | agents.md, progressive documentation, state files |
| **Modes** | Plan mode, accept edits, YOLO, --dangerously-skip-permissions |
| **Permissions** | Approval workflows, sandboxing, YOLO mode |
| **Tools** | Read, Write, Edit, Bash, MCP tools |
| **Plug-ins** | Plugin marketplace, feature dev, code simplifier, frontend design |
| **Skills** | Markdown-based skill files for domain knowledge |
| **Hooks** | Event-triggered actions in settings.json |
| **MCP** | Model Context Protocol servers for external integrations |
| **LSPs** | Language Server Protocol support in coding agents |
| **Slash commands** | /context, /clear, /usage, /gsd, /skills, etc. |
| **Workflows** | GSD, Claude Agent Teams, Gastown orchestration |
| **IDEs** | Cursor, Copilot, VS Code with coding agents |
| **Mental model** | The 8-stage Steve Yegge spectrum |
| **Stochastic entities** | Understanding LLM unpredictability and working with it |

### Plus Things Karpathy Didn't Mention

The course covered additional things not even in the tweet:
- **Sandboxing** (native, managed cloud, Sprites.dev)
- **REPL loops** (infinite feedback loops for automation)
- **Spec-driven design** (GSD framework)
- **Multi-agent orchestration** (Claude Agent Teams, Gastown)
- **Live market data integration** (Polygon API)
- **Deployment** (Fly.io, containers)

---

## 17. Course Best Practices — Final Summary

These are the consolidated best practices from the entire course, distilled into a final checklist.

### 1. Pick the Right Tool for the Job

Use this decision framework:

| Situation | Recommended Approach |
|---|---|
| Mission-critical production code | Yellow row (markdown management, incremental, SDD/GSD) |
| Large existing codebases | GSD or top-row techniques |
| Code at the frontier (not in training data) | GSD — spec-driven with verification |
| MVPs, new builds, risk appetite | Purple row — YOLO in sandbox |
| Churning out boilerplate | YOLO + REPL loops + Claude on managed web |
| Multi-agent orchestration needed | Claude Agent Teams, GSD, or Gastown |
| Budget constraints | GSD with cheaper model; free models with more discipline |

### 2. Start with Plugins

Begin every new project by installing appropriate plugins:

**High-value plugins to consider:**
- **Feature Dev** — guided feature development workflow
- **Code Simplifier** — prevents code bloat and encourages clean code
- **Frontend Design** — production-grade frontends that avoid generic LLM aesthetic
- **Playwright** — integration testing with browser automation

**Plugin selection rule:** Pick the ones that match your project type. Don't install more than needed.

### 3. Build Project-Specific Skills

After plugins, add custom skills for your domain:
- Skills encode the "right way" to do things in your specific project
- Consistent use of the Cerebrace/OpenRouter skill for LLM inference
- Market data API usage patterns
- Framework-specific patterns (if you have them)
- Any domain knowledge that should be universal across all agent interactions

### 4. Maintain a Trial and Error Mindset

> *"There's not necessarily one right answer. The great thing about using these coding agents is you can kick it off, let it build something. If it all goes wrong, just simply start again, try it again with a different approach."*

- Embrace experimentation — it's low-risk with Git
- If something doesn't work, `git checkout main` and try again with different instructions
- Keep iterating on prompts and team compositions

### 5. Make Heavy Use of Git

Git is your most important safety net when using coding agents:
- Always work on branches, not main
- Commit before any major agent operation: `git commit -m "ready for agents"`
- Create specific branches: `git checkout -b agent-teams` or `git checkout -b gsd`
- Use `git checkout main` as your "escape hatch"
- This lets you compare results from different approaches side-by-side

### 6. Be Disciplined About Markdown Documentation

Maintain markdown files throughout every project:
- **agents.md / claude.md** — always kept current with latest state
- **plan.md** — the spec document that drives agent work
- **State tracking files** — what has been built, what's pending
- **Bug files** — when debugging, write down the issue precisely before trying to fix it

> *"Markdown is baked into some of these workflows. Use it as your way of tracking what's going on, just as we've been doing both in Weeks 2 and 3."*

### 7. Proactively Manage Context

Don't let context rot kill your work quality:

```bash
# Check context regularly
/context

# See what's consuming context
# Remove unnecessary items
# Write important state to files

# Clear and start fresh when context is full
/clear
```

**The right process:**
1. Run `/context` regularly to see what's loaded
2. Write key state to `agents.md` before clearing
3. Run `/clear` to start with clean context
4. Let agents reload from files as needed

> *"Don't wait for your context to compact. Manage it yourself. Write stuff out to markdown, write stuff to claude.md/agents.md, and then do a slash clear to start again and be fresh with your context."*

### 8. Own the Quality of Your Code

The most important mindset reminder:

> *"Remember — you own the quality of the code that you push. This is code that you stand behind. Don't let your coding agent build slop."*

Specific things to reject and push back on:
- **Unnecessary test files** that just test code paths, not real behavior
- **README files** that weren't asked for
- **Emojis** in code or documentation (unless specifically wanted)
- **Long, bloated files** that are hard to review
- **Over-mocked tests** that don't test real functionality
- **Defensive programming bloat** — excessive null checks, redundant validations

**The AIPR policy** (referenced from Jennifer in the course): treat your coding agent output with the same review rigor you'd apply to any code you're professionally responsible for.

---

## 18. The Progression: Vibe Coder → Vibe Engineer → Agentic Engineer

### The Three Levels

The course defines three levels of coding agent mastery, and you've now completed all three:

```
Level 1: Vibe Coder
├── Using AI assistants in IDEs (Cursor, Copilot)
├── Simple natural language coding
├── Building fun projects
└── Learning the basics of AI pair programming

        ↓ (Week 1-2)

Level 2: Vibe Engineer  
├── Professional-grade use of coding agents
├── Claude Code & Codex in CLI
├── Slash commands, REPL loops
├── Proper Git workflow integration
├── Commercial project delivery
└── Large codebase best practices

        ↓ (Week 3)

Level 3: Agentic Engineer
├── Sub-agents and agent teams
├── Multi-agent orchestration (GSD, Agent Teams, Gastown)
├── Sandboxing and remote execution
├── Plugins, skills, hooks, MCP
├── Swarm orchestration
└── Deploying production-ready containerized apps
```

### The Graduation

> *"By this point, I said that you are now vibe engineering. You've gone from vibe coding to vibe engineering as a professional. And now... you are no longer a vibe coder. You are no longer a vibe engineer. You are now officially an agentic engineer."*

---

## 19. Complete Course Recap — All Three Weeks

### Week 1 — Vibe Coding for Fun and Profit

**Topics covered:**
- Introduction to AI coding assistants and IDEs
- Cursor, GitHub Copilot, Codex, Cody/Gravity
- Plugins overview within IDEs
- First YOLO experience
- Built first commercial MVP project (unnamed project)
- Introduction to vibe coding concepts

**Projects built:**
- First-person shooter game (introductory/fun)
- Commercial MVP

### Week 2 — Professional Coding Agents

**Topics covered:**
- Claude Code and Open Code in CLI environments
- AMP (another coding agent CLI)
- Slash commands for the first time
- REPL loops for automation
- JIRA integration workflow (full cycle from ticket to git push)
- The full engineering workflow with version control

**Major project:**
- Legal SaaS platform (full commercial application with user authentication, contract management, multi-user support)
- This was Project 4 in the commercial project series

### Week 3 — Agentic Engineering

**Day 1 — Pro Features:**
- Slash commands and custom commands
- Skills (the new universal standard across all agents)
- Multi-agents (running multiple instances)
- Sub-agents (focused workers that report back)
- Agent teams preview (coming Day 4)
- Hooks (event-triggered automation)
- Plugins (bundled skills, commands, sub-agents, hooks)
- Plugin marketplace

**Day 2 — Sandboxing and Remote Execution:**
- Why sandboxing matters (approval fatigue, security risks)
- Native sandbox (`/sandbox`)
- Managed cloud (5 methods: ampersand prefix, `--remote`, web UI, mobile app, GitHub Issues `@Claude`)
- Sprites.dev (third-party cloud sandbox, Fly.io powered)
- Live Sprites.dev demo with zero-shot market data terminal

**Day 3 — Large Codebases and Spicy Extras:**
- 7 best practices for large team codebases
- Progressive documentation, link vs `@` embedding
- Consistent team workflows
- Project-specific skills
- Behavior-focused testing
- Human review culture
- Bite-sized chunks
- Bonus: Claude Agent SDK (programmatic control)
- Bonus: Claude Cowork (business users, receipts-to-Excel demo)
- Bonus: OpenClaw (personal AI sidekick via Telegram/WhatsApp)

**Day 4 — Orchestration Part 1:**
- Swarms vs. orchestration spectrum
- Claude Agent Teams (experimental, settings.json, 8 steps, keyboard shortcuts)
- Agent Teams vs Sub-Agents deep comparison
- FiNALLY platform built in 30 minutes (6 agents, zero-shot)
- GSD framework (spec-driven, phase workflow)
- FiNALLY platform built in 5 hours (10 phases, thorough testing)
- Side-by-side comparison

**Day 5 — Orchestration Part 2 + Finale:**
- Day 4 recap and zero-shot reflection
- Gastown framework (Steve Yegge's radical approach)
- Gastown vocabulary and setup
- Gastown live build from scratch (polecats, refinery, witness, mayor)
- Gastown vs. Claude Agent Teams vs. GSD comparison
- Codex sub-agents (experimental parallel feature)
- Four-way UI comparison
- Live market data integration (Polygon/Massive API)
- Deployment to Fly.io in 15 minutes
- tmux quad terminal with multiple coding agents
- Andrej Karpathy tweet revisited
- Best practices summary
- Course graduation: Agentic Engineer

### Total Projects Built

| # | Project | Week | Type |
|---|---|---|---|
| 1 | First-Person Shooter Game | 1 | Fun/demo |
| 2 | Space Invaders (via Claude Agent SDK) | 3 Day 3 | Fun/demo |
| 3 | Commercial MVP | 1 | Commercial |
| 4 | Legal SaaS Platform | 2 | Commercial |
| 5 | FiNALLY Trading Platform (multiple builds) | 3 Days 4-5 | Commercial capstone |

---

## 20. Final Key Takeaways

### The Three Core Realizations

**1. The alien tool has been domesticated**

Karpathy's "powerful alien tool handed around with no manual" now has a manual. You know:
- When to use each tool (IDE vs CLI vs orchestrator)
- How to manage context proactively
- How to structure documentation for agents
- How to test agent-generated code appropriately
- How to deploy the results

**2. Zero-shot is real, but bugs are part of it**

Multiple complex applications were built zero-shot (first attempt, no debugging). But:
- Zero-shot doesn't mean bug-free
- The 10x speedup is real but gets pulled back by debugging cycles
- Net result is still 2-3x faster than manual coding at minimum
- The right attitude is: expect bugs, have a process, keep going

**3. The landscape is moving and you're moving with it**

The course covered the landscape as it exists now. By the time you read this:
- Some features mentioned as "experimental" may be fully live
- New orchestration frameworks will have emerged
- The eight stages will have been redrawn
- Models will be stronger

The key is the **mindset and mental model** — not the specific tools. The mental model (when to use what, how to manage context, how to structure work for agents) is durable even as the specific tools change.

### The Single Most Important Thing

> *"The single most important thing is you need to be willing to experiment. There's not necessarily one right answer. The great thing about using these coding agents is you can kick it off, let it build something. If it all goes wrong, just simply start again, try it again with a different approach."*

Build. Experiment. Learn. Build again.

---

## Quick Reference — Day 5

### Gastown Commands

```bash
# Install
brew install gastown          # Mac
# (PowerShell command on GitHub repo for Windows)

# Setup
gt init ~/GT --git            # Initialize workspace
gt rig add [name]             # Create a project (rig)
gt crew add [name] --rig [rig] # Create a workspace (crew)
gt mayor attach               # Launch the mayor (Claude Code)

# Inside Claude Code (the mayor)
"Build the entire project as described by spec.md. 
 File the issues, create a convoy, and sling the work to polecats."

# tmux navigation
Ctrl+B then W                 # List all sessions
Ctrl+B then arrow             # Navigate between panes
```

### Codex Sub-Agents

```bash
# In Sprites.dev sandbox
codex --yolo                  # Launch Codex in YOLO mode
/experimental                 # Access experimental features toggle
# Enable: "sub-agents: spawn multiple agents to parallelize work"

# Note: rename claude.md to agents.md for Codex
mv claude.md agents.md
```

### Fly.io Deployment

```bash
# Ask Codex/Claude to handle deployment
"What's the best place to deploy this on the internet?
 Please write a deployment script for Fly.io"

# Run the generated script
# Set environment variables when prompted (API keys, etc.)
# App will be live at [appname].fly.dev
```

### tmux Quad Setup

```bash
# Attach to existing quad session
tmux attach -t quad

# Navigate between the 4 panes
Ctrl+B →    # Right
Ctrl+B ↓    # Down  
Ctrl+B ←    # Left
Ctrl+B ↑    # Up
```

---

## Final Glossary — All Gastown Terms

| Term | Definition |
|---|---|
| **Town** | The entire Gastown workspace (`~/GT`) |
| **Rig** | A single project within the town |
| **Crew** | A named workspace identity within a rig |
| **Mayor** | The primary Claude Code you interact with; the coordinator |
| **Polecat** | A worker agent assigned specific tasks (beads) |
| **Bead** | A single task/issue with a unique ID (like a GitHub issue) |
| **Convoy** | A bundle of beads assigned to polecats as a phase of work |
| **Refinery** | Dedicated agent that processes merge requests (MRs) |
| **Witness** | Monitoring agent that watches all polecats and alerts the mayor |
| **Merge Queue** | Queue of MRs waiting to be processed by the refinery |
| **Beads Ledger** | The underlying task-tracking infrastructure by Steve Yegge |
| **Sling** | The action of assigning/distributing work to polecats |
| **MR** | Merge Request — what a polecat creates when its work is done |
| **GT** | The Gastown command prefix (e.g., `gt rig add`, `gt mayor attach`) |
| **Decon session** | A monitoring/debugging process (can fail without major consequences) |

---

*End of Day 5 Notes — Week 3 of the AI Codec Course*

*Congratulations — you are now an Agentic Engineer.*
