# 🤖 The Definitive AI Coder Course — Day 5 Complete Notes
### *Week 1 Finale — Building a Commercial MVP: Full-Stack Kanban App with AI Assistant*

---

## Table of Contents

1. [Day 5 Overview — Week 1 Conclusion](#1-day-5-overview--week-1-conclusion)
2. [Karpathy's Tweet Timeline — The Evolution of Vibe Coding](#2-karpathys-tweet-timeline--the-evolution-of-vibe-coding)
3. [Rules Recap — Be the Boss (Second Pass)](#3-rules-recap--be-the-boss-second-pass)
4. [Web Apps 101 — Front-End, Back-End & APIs Explained](#4-web-apps-101--front-end-back-end--apis-explained)
5. [Docker Explained — Computers Within Computers](#5-docker-explained--computers-within-computers)
6. [Installing Docker Desktop](#6-installing-docker-desktop)
7. [Today's Project — The Full-Stack Kanban PM App](#7-todays-project--the-full-stack-kanban-pm-app)
8. [Setting Up the Project — The PM Repository](#8-setting-up-the-project--the-pm-repository)
9. [Deep Dive into agents.md — The PM App Version](#9-deep-dive-into-agentsmd--the-pm-app-version)
10. [The 10-Part Build Plan — plan.md](#10-the-10-part-build-plan--planmd)
11. [Part 1 — Planning & Enrichment](#11-part-1--planning--enrichment)
12. [Part 2 — Scaffolding (Docker + FastAPI Backend)](#12-part-2--scaffolding-docker--fastapi-backend)
13. [Part 3 — Adding the Front-End](#13-part-3--adding-the-front-end)
14. [Part 4 — Fake User Sign-In](#14-part-4--fake-user-sign-in)
15. [Part 5 — Database Schema Design](#15-part-5--database-schema-design)
16. [Part 6 — Backend API Routes](#16-part-6--backend-api-routes)
17. [Part 7 — Wiring Front-End to Back-End](#17-part-7--wiring-front-end-to-back-end)
18. [Context Window Management — Resetting the Chat](#18-context-window-management--resetting-the-chat)
19. [Part 8 — AI Connectivity (OpenRouter)](#19-part-8--ai-connectivity-openrouter)
20. [Part 9 — AI Understands the Kanban Board](#20-part-9--ai-understands-the-kanban-board)
21. [Part 10 — Full AI Chat Interface](#21-part-10--full-ai-chat-interface)
22. [Git Checkpointing — The Discipline of Snapshots](#22-git-checkpointing--the-discipline-of-snapshots)
23. [Lessons Learned from the Full Build](#23-lessons-learned-from-the-full-build)
24. [Week 1 Wrap-Up & Assignment](#24-week-1-wrap-up--assignment)

---

## 1. Day 5 Overview — Week 1 Conclusion

Day 5 is the **second blue (commercial project) day** and the **finale of Week 1**. Week 1's theme was "Vibe Coding for Fun and Profit" — Day 5 is the **profit** side. Everything built so far has been warmup.

### What's Different Today vs. Day 4

| Day 4 | Day 5 |
|---|---|
| Pure YOLO — no agents.md, no plan | Structured approach — proper agents.md + detailed plan |
| Single-shot prompts | Step-by-step incremental build |
| Front-end only | **Full-stack**: front-end + back-end + database + Docker |
| JavaScript API routes | **Python FastAPI** back-end |
| No persistence | **SQLite database** — data survives restarts |
| No authentication | **User sign-in** experience |
| No AI in the app | **AI assistant chat** built into the app |

### The Rule Violated on Day 4, Fixed Today

Day 4 deliberately broke all the "be the boss" rules — pure YOLO mode with no oversight. Day 5 **follows the rules** to show what disciplined, incremental building looks like and why it produces better results.

---

## 2. Karpathy's Tweet Timeline — The Evolution of Vibe Coding

The instructor walks through three key Andre Karpathy tweets in chronological order, showing how the conversation around AI coding has evolved.

### Tweet 1 — The Birth of Vibe Coding (February 2025)

Karpathy coined the term "vibe coding":

> *"There's a new kind of coding where you give in fully to the vibes, embrace the exponentials, forget that the code even exists."*

This was a light-hearted, optimistic take. It referred specifically to tools like Cursor Composer and Claude Sonnet.

---

### Tweet 2 — The Missing Manual (December 2025)

This is the tweet that inspired the entire course — Karpathy's explosion of everything happening in the agentic coding space:

> *"I've never felt this much behind as a programmer... involving agents, sub-agents, prompts, contacts, memory modes, permissions, tools, plugins, skills, hooks, MCP, LSP, workflows, IDE integrations..."*

We've covered many of these in Week 1. By the end of three weeks, all of them will be covered.

---

### Tweet 3 — A Train-of-Thought Deep Dive (Late January 2026)

This is a long, candid reflection. The instructor walks through each section:

#### Section 1 — Coding Workflow Shift
Karpathy describes his personal shift:
- **Before:** 80% manual autocomplete, 20% agents
- **After:** 80% agents, 20% edits and touch-ups

This is the trajectory the course is taking students on.

#### Section 2 — Agent Swarm Hype
> *"The 'no need for IDE anymore' hype and agent swarm hype is too much for me right now. The models definitely make mistakes. If you have any code you actually care about, I would watch them like a hawk."*

This directly validates the "be the boss" philosophy. Even Karpathy — the person who coined vibe coding — recommends watching agents like a hawk on serious code.

#### Section 3 — Tenacity
Karpathy observes that agents work **relentlessly** — they never get tired, never get demoralised, they just keep going. This is one of their most powerful attributes.

#### Section 4 — Speed-Up is Hard to Measure
He avoids giving a specific multiplier like "10x". Instead, he describes the effect as:
- Not purely a speed increase
- More of an **expansion** — he does a lot *more* than he planned to do
- The leverage is about reaching bigger goals, not just reaching the same goals faster

#### Section 5 — The Fun Factor (Surprising)
> *"He didn't anticipate that agent programming feels more fun."*

Agents handle the drudgery — getting stuck, bashing against walls. This frees up the engineer to focus on building. His hypothesis: this splits engineers into two camps — those who loved the act of *coding* (typing, running) and those who loved the act of *building* (creating systems). The latter group tends to enjoy vibe coding more.

#### Section 6 — Atrophy (Warning)
Karpathy honestly admits he's **starting to lose his technical acumen** from letting agents do too much. He's falling out of practice writing code directly.

> This is the same point made earlier about the Anthropic study — constant AI use without deliberate learning causes skill atrophy. Be aware of it.

#### Section 7 — The Slop Apocalypse
Karpathy coins "slop apocalypse" — bracing for the year when LLM-generated slop floods the internet and codebases. The backlash is coming, and it will demand concise, quality code, not emoji-filled verbose output.

---

## 3. Rules Recap — Be the Boss (Second Pass)

The five principles from Day 4 are revisited — quickly but with emphasis, because today they will be followed:

### The Five Principles (Quick Reference)

| Principle | What It Means |
|---|---|
| **1. Write a great agents.md** | Spec + Style + Success criteria. Concise but complete |
| **2. Start simple** | Begin with the most basic MVP, not the full vision |
| **3. Work incrementally** | Test and validate at every step before moving forward |
| **4. Don't get lazy** | Watch like a hawk. Demand evidence, not just claims |
| **5. Embrace frustration** | Hitting walls is part of the process — manage it, don't fight it |

### The Manager Analogy for Junior Engineers

Think of yourself as a **non-technical manager** in charge of an enthusiastic but sometimes misguided team:
- You may not have the technical depth of the agent
- But you can ask the challenging questions: *"Show me the evidence"*, *"Have you thought about this?"*, *"Explain this to me"*
- You can play the "this might be a silly question, but..." card — and often those questions cut right to the heart of a real problem
- Your role is **probing management**, not passive acceptance

### The Senior Engineer's Shift

For senior engineers, the new craft is:
- Less line-by-line coding satisfaction
- More system-level building (Andre's "less coding, more building")
- Finding the groove where agents handle the mundane, freeing you for higher-order work
- Leveraging your expertise to catch what the agent gets wrong

---

## 4. Web Apps 101 — Front-End, Back-End & APIs Explained

This section is a concise primer for anyone who isn't already familiar with how web applications are structured. Experienced engineers can skim.

### The Basic Architecture

A **web application** is accessed through a browser. Most web apps have two parts:

```
┌─────────────────────────────────────────────────────────┐
│                    WEB APPLICATION                      │
│                                                         │
│  ┌─────────────────┐        ┌────────────────────────┐ │
│  │   FRONT-END     │◄──────►│     BACK-END           │ │
│  │                 │  APIs  │                        │ │
│  │ Runs in the     │        │ Runs on a server       │ │
│  │ user's browser  │        │                        │ │
│  │                 │        │ • Business logic       │ │
│  │ • HTML          │        │ • Database access      │ │
│  │ • CSS           │        │ • LLM calls            │ │
│  │ • JavaScript    │        │ • Secrets (.env file)  │ │
│  └─────────────────┘        └────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

---

### The Front-End

The **front-end** is everything that runs inside the user's web browser:
- **HTML** — the structure and content of the page
- **CSS** — the styling (colors, layout, fonts, spacing)
- **JavaScript** — the interactivity and dynamic behaviour

#### Front-End Technology Progression

| Technology | Description |
|---|---|
| **Vanilla HTML/CSS/JS** | Basic web pages. What Day 1's FPS game used |
| **Libraries (jQuery)** | Simple, low-level helpers for common JS operations |
| **Frameworks (React, Vue, Angular, Svelte)** | Build UIs out of reusable components that update automatically |
| **Next.js** | Higher-level framework built on React. Handles routing, data fetching, server vs. client rendering. Made by Vercel. What we've been using |

#### Single Page Applications (SPAs)
With modern frameworks, the **entire front-end loads as one request**. After that, individual components make separate API calls to update themselves. This is called a **Single Page Application (SPA)** — very common in modern web development.

> **Note on LLM-generated front-ends:** LLMs are very strong at building front-ends. But they often produce a recognisable "LLM look" — similar layouts, that purple hue, three icons, generic structure. A skilled UX/UI person adds value by ensuring the design is unique, communicates well, and serves the actual users.

---

### The Back-End

The **back-end** runs on a server (or locally during development). It handles:
- **Business logic** — the rules and processing that make the app work
- **Database access** — reading and writing persistent data
- **LLM calls** — connecting to AI models (API keys live here, securely)
- **Secrets** — passwords, API keys (in `.env` files) — never on the front-end

#### Projects Built This Week: Front-End vs. Back-End

| Day | Project | Architecture |
|---|---|---|
| Day 1 | FPS Game | Front-end only (vanilla HTML/JS) |
| Day 3 | Kanban Board (all four tools) | Front-end only (Next.js) |
| Day 4 | Portfolio + Digital Twin | Front-end + back-end (both in JavaScript/Next.js) |
| **Day 5** | **PM App** | **Front-end (Next.js) + Back-end (Python FastAPI)** |

---

### APIs — How Front-End and Back-End Talk

**API** stands for Application Programming Interface. In web apps, the front-end makes **API calls** (HTTP requests) to the back-end to:
- Retrieve data (e.g., load the Kanban board cards)
- Submit changes (e.g., move a card to a new column)
- Trigger actions (e.g., ask the AI assistant a question)

The back-end processes the request, does whatever work is needed (database query, LLM call, etc.), and sends back a response.

---

### Why Python for the Back-End Today?

For the Day 5 project, the back-end is written in **Python**, not JavaScript. Reasons:
- Python is the **most common back-end language** for AI-connected apps
- The instructor knows Python well and has strong opinions on it
- The framework used — **FastAPI** — is excellent for building APIs with Python
- Python is the dominant language for working with LLMs, data science, and ML

---

## 5. Docker Explained — Computers Within Computers

### What is Docker?

Docker gives you a **computer within your computer** — a ring-fenced, isolated environment running on your machine that is separate from everything else.

> *"The easiest way to describe Docker is that it gives you a computer within your computer."*

If you know about **virtual machines**, Docker is a lighter-weight alternative that achieves a similar goal.

---

### Why Developers Love Docker

| Benefit | Explanation |
|---|---|
| **Isolation** | Everything inside the Docker environment can't damage the outside world — great for agentic coding safety |
| **Portability** | Build it once on your laptop, run it anywhere — another server, a cloud provider, a colleague's machine |
| **Reproducibility** | The exact same environment every time — no "works on my machine" problems |
| **Containerised deployment** | Once in a container, deploying to AWS, GCP, Vercel, etc. is dramatically simpler |

---

### Three Core Docker Concepts

Understanding these three terms is enough to work with Docker effectively:

#### 1. Dockerfile — The Recipe
A **Dockerfile** is a text file containing **step-by-step instructions** for setting up an environment:
- Which operating system to use
- Which software to install
- Which files to copy in
- How to configure everything

Think of it as a **recipe** for creating a consistent environment.

```dockerfile
# Example snippet of what a Dockerfile looks like:
FROM python:3.12-slim
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

#### 2. Docker Image — The Blueprint/Snapshot
A **Docker image** is built from a Dockerfile. It's a **snapshot** of a ready-to-use environment — everything installed and configured, ready to go.

- Created FROM a Dockerfile
- Static — it doesn't run, it just exists
- Can be reused to create many containers
- Think of it as a **blueprint**

#### 3. Docker Container — The Live Running Environment
A **Docker container** is created FROM an image. It's the actual **live, running environment** — the box within your box.

- Created from an image
- Actually running, actively processing
- You can have multiple containers from the same image
- Each is isolated from the others and from your main system

```
Dockerfile → (build) → Image → (run) → Container (live!)
```

**Example:** One image for your Python FastAPI back-end could spin up ten containers running simultaneously — each serving a different user.

---

### Additional Docker Concepts (Brief)

- **Volumes:** Ring-fenced storage space that containers can use. Allows data to persist even when a container stops
- **Docker Compose:** A tool for running multiple containers together (e.g., your back-end + your database, both in containers)

---

## 6. Installing Docker Desktop

**Docker Desktop** is the GUI (Graphical User Interface) application that manages all your Docker containers, images, and volumes from a visual dashboard.

### Installation Steps

1. Go to **docker.com**
2. Click **Download Docker Desktop**
3. Choose your platform (Mac, Windows, Linux)
4. Download and run the installer

#### On Windows:
- The installer will likely prompt you to use **WSL** (Windows Subsystem for Linux) — **accept this and follow the defaults**
- There will be multiple things to install — go through all of them
- A **computer restart** may be required to update PATH variables

#### On Mac:
- Download the `.dmg` file
- Drag Docker to Applications
- Launch it

### What You'll See After Installation

When Docker Desktop is open, you'll see a dashboard with:
- **Containers** — all currently running containers
- **Images** — all images built on your system (the blueprints)
- **Volumes** — storage areas used by containers

Everything will be empty initially. As you build projects, these will populate.

---

## 7. Today's Project — The Full-Stack Kanban PM App

### What We're Building

A **full-stack Project Management application** — a real, commercially-viable product with:

| Component | Technology | Description |
|---|---|---|
| **Front-End** | Next.js (React) | The Kanban board UI — the excellent one built by Codex on Day 3 |
| **Back-End** | Python FastAPI | REST API serving the front-end, handling business logic |
| **Database** | SQLite (local) | Persistent storage — cards and boards survive restarts |
| **Authentication** | Basic hardcoded user | Single user sign-in (expandable to multi-user) |
| **AI Feature** | OpenRouter | AI assistant chat within the app |
| **Packaging** | Docker | Everything runs in a container |

### The "AI Building AI" Aspect

Today's build is doubly interesting:
1. A **coding agent** (GitHub Copilot / Codex) is **writing the code**
2. The code it writes **itself calls an AI** (via OpenRouter)

An AI building an app that contains an AI.

### The Inheritance Model

Rather than starting from nothing, the project **inherits the Kanban front-end** built by Codex on Day 3. The premise: "imagine this was built by another team, and we're adding the back-end."

This introduces a real-world pattern:
- Starting with **inherited legacy code** (even if only a few days old)
- Building new functionality around it
- Integrating components that didn't previously know about each other

---

## 8. Setting Up the Project — The PM Repository

### Cloning the Repository

The course provides a GitHub repository called **PM** containing:
- The existing Kanban front-end (from Codex Day 3)
- An `agents.md` file (pre-written)
- A `docs/plan.md` file (10-part build plan)
- An empty `backend/` directory
- An empty `scripts/` directory
- A `.env` file (copy your OpenRouter key here)
- A `.gitignore` file (pre-configured to exclude `.env`)

```bash
# In the terminal inside VS Code:
cd projects
git clone [URL from course resources]
cd pm
```

Open the `pm` folder in VS Code as your project.

### Checking Your GitHub Copilot Usage

Before starting:
1. Go to your GitHub profile (github.com)
2. Avatar menu → **Copilot settings**
3. Check:
   - Which plan you're on (Free vs. Pro)
   - How many premium requests you've used
   - When your quota resets

This tells you how much runway you have for today's build.

### Choosing Your Model

In the GitHub Copilot agent panel (VS Code, right side):
- Click the model selector
- Choose **GPT 5.2 Codex** for best results (if available on your plan)
- The "manage models" button shows all available models, including options to run **local models** (e.g., Ollama) for free if your machine is powerful enough

---

## 9. Deep Dive into agents.md — The PM App Version

This `agents.md` is more sophisticated than the Kanban one from Day 3. Let's walk through each section.

### Section 1 — Business Requirements

```markdown
# Project Management MVP

## Business Requirements

- User should be able to sign in
- When signed in, they see a Kanban board representing their project
- Fixed columns that can be renamed
- Cards can be moved between columns
- AI chat feature in the sidebar
- The AI is able to create, edit or move one or more cards

## MVP Limitations

- Single user sign-in — hardcoded username and password
- Database should support multiple users for the future (just not the UI)
- One Kanban board per signed-in user
- Runs locally in a Docker container for MVP
```

**Key design decisions explained:**
- **Single hardcoded user** — simplifies auth for MVP while leaving the door open for multi-user later
- **Docker from the start** — even though it's local-only, running in Docker from day one means deployment is easy when the time comes
- **AI can modify cards** — this is the ambitious feature that makes the app genuinely useful

---

### Section 2 — Technical Decisions

```markdown
## Technical Decisions

- Frontend: Next.js (using the existing Kanban MVP in /frontend)
- Backend: Python FastAPI
- Packaging: Docker container
- Package manager: UV (Python)
- AI calls: OpenRouter (API key in .env file in project root)
- Model: [specified model name]
- Database: SQLite (local, simple)
```

**Why these choices?**
- **FastAPI** — the instructor's preferred Python API framework: fast, modern, excellent auto-documentation
- **UV** — a faster, more modern Python package manager than pip (personal preference of the instructor)
- **SQLite** — simplest possible database: a single file, no server needed, perfect for local MVPs
- **OpenRouter** — already familiar from Day 4; allows free and paid model access

> **You don't need to know these answers yourself** — you can always ask the agent to recommend a technical stack, then approve or modify its suggestions.

---

### Section 3 — Starting Point

```markdown
## Starting Point

A working MVP of the front-end is already in the /frontend directory.
This is NOT yet designed for the Docker setup.
It is a pure front-end-only demo.
```

This tells the agent about the existing code it will be working with, preventing it from rebuilding something that already exists.

---

### Section 4 — Coding Standards

```markdown
## Coding Standards

- Use latest library versions; idiomatic approaches
- Keep it simple — never over-engineer
- IMPORTANT: When hitting issues, always identify root cause
  Do NOT guess. Prove with evidence. Then fix the root cause.
- Be concise; keep READMEs minimal
- No emojis ever
```

The root cause rule is **critical** for a complex multi-part build where silent failures compound over time.

---

### Section 5 — Working Documentation

```markdown
## Working Documentation

All documents for planning and executing this project will be in the /docs directory.
Please review docs/plan.md before proceeding.
```

This is a powerful pattern: telling the agent to maintain its own working documentation. The plan file becomes a shared source of truth between you and the agent.

---

## 10. The 10-Part Build Plan — plan.md

Rather than asking the agent to come up with the entire plan, the instructor wrote a **high-level 10-step plan** in `docs/plan.md`. The agent is then asked to **enrich** this plan with details, sub-steps, and success criteria.

This approach gives you control over the architecture while letting the agent handle the implementation specifics.

### The 10 Parts

| Part | Name | What Gets Built |
|---|---|---|
| **1** | Planning & Enrichment | Agent enriches this document with detailed sub-steps, tests, and success criteria |
| **2** | Scaffolding | Docker infrastructure, FastAPI "hello world", start/stop scripts |
| **3** | Front-End Integration | Serve the existing Kanban front-end through the Docker setup |
| **4** | Fake User Sign-In | Simple login screen with hardcoded credentials |
| **5** | Database Schema | Design and document the database tables |
| **6** | Backend API Routes | CRUD endpoints for reading/writing the Kanban board |
| **7** | Front-End ↔ Back-End Wiring | Connect the UI to the API so board changes persist |
| **8** | AI Connectivity | Back-end can make OpenRouter API calls — tested with "2+2" |
| **9** | AI Understands the Board | Send the board state to the AI, receive structured responses |
| **10** | Full AI Chat UI | Beautiful chat widget in the sidebar with AI card management |

### Why This Plan Structure Works

Each part is:
- **Small enough** to be verifiable — you can confirm it works before moving on
- **Independent enough** — if it fails, it's clear which component broke
- **Progressive** — each part builds on the last, nothing is skipped
- **Testable** — you can run the server and manually verify each part

> *"The thing I have in my mind always is that if any one of these steps doesn't work, then I have a really good sense of how to dig in and figure out why."*

---

## 11. Part 1 — Planning & Enrichment

### The First Prompt Pattern

The very first message to the agent is deliberately designed **not to do any work yet**:

```
Please review agents.md and the plan, and let me know if you have 
any questions before we start.

Do NOT do any work yet.
```

**Why "do not do any work yet"?**
- Forces the agent to read and understand the brief before acting
- Surfaces any ambiguities or misunderstandings before they become code
- Gives you a chance to course-correct before the agent invests effort
- The agent asking questions is a sign of intelligence, not incompetence

### The Questions the Agent Asked

1. *"Do you want me to enrich plan.md with detailed checklists, tests and success criteria?"* → Yes
2. *"Should I create the front-end agents.md as part of the plan enrichment or only after?"* → Create it right away
3. *"Do you have a minimum test coverage target or specific test types you want prioritised?"* → 80% unit test coverage minimum, robust integration testing

### What Part 1 Produces

After enrichment, `plan.md` contains:
- **Checkboxes** for every sub-step (agent tracks progress by ticking these)
- **Success criteria** for each part (specific, testable conditions)
- A `frontend/agents.md` describing the inherited front-end codebase

---

## 12. Part 2 — Scaffolding (Docker + FastAPI Backend)

### What "Scaffolding" Means

Scaffolding is building the **structural skeleton** of the application — the infrastructure and plumbing that everything else sits on. No real features yet; just confirming the basic architecture works.

**Goal for Part 2:**
- Docker container builds and runs
- FastAPI serves a simple "hello world" response
- Start and stop scripts work
- A basic health check endpoint passes

### The Key Lesson: Always Make Agents Prove Their Work

After the agent declared Part 2 "done", it was challenged:

```
Did you actually test this yourself? 
Please run tests thoroughly. Bring up the server. 
Make sure it works. Check all routes. 
Bring it down. Let me know when you are confident.
```

**The agent's honest response:** *"No, I did not run the tests."*

This is a recurring pattern — agents often declare completion without actually verifying. **You must push back**.

### The Dockerfile

The generated Dockerfile included:
- `FROM python:3.12-slim` — using Python 3.12 (sensible, stable choice)
- Installing UV as the package manager
- Copying `requirements.txt` and installing dependencies
- Setting up the FastAPI server startup command

> The agent used `requirements.txt` rather than a UV project structure, but still used UV to run installs. This is slightly non-standard but functional — a pragmatic compromise.

### Manual Verification

After forcing the agent to test, the instructor also manually verified:

```bash
# In VS Code terminal:
bash scripts/start_mac.sh
```

Then in a browser:
- `http://localhost:8000/` — basic server response
- `http://localhost:8000/health` — `{"status": "ok"}`
- `http://localhost:8000/api/hello` — `"Hello from FastAPI"`

All working. ✅

### The 80% Coverage Trap

A warning caught during Part 2: the agent was spending most of its time trying to hit 80% test coverage by **adding pointless tests** — testing things that don't matter, just to tick the coverage percentage box.

This is a classic LLM failure mode: following the **letter** of a rule rather than its **spirit**. 

**Correction given after Part 3:**
```
Going forwards, please only achieve 80% test coverage if it's 
sensible to do so. Avoid adding unnecessary tests just to hit 80%.
Focus on valuable, meaningful tests. Not hitting 80% is okay.
```

---

## 13. Part 3 — Adding the Front-End

**Goal:** The existing Kanban front-end is now **served through the Docker setup** — not just running standalone, but integrated with the back-end infrastructure.

### What Changes
- The Next.js front-end is reconfigured to be served through the Docker container
- Both front-end and back-end now run from the same `start` script
- Visiting `localhost:8000` shows the Kanban board

### Reviewing Diffs
GitHub Copilot shows a **diff panel** — green lines are additions, red lines are removals. This is where you can review exactly what the agent changed.

Two approaches:
1. **Review each diff individually** — more thorough, slower
2. **Press "Keep All"** — accept everything, move faster (used here for low-risk changes)

The instructor recommends reviewing diffs carefully for sensitive changes (authentication, database schema, AI connectivity) but accepting quickly for low-risk scaffolding work.

### Result

Running `bash scripts/start_mac.sh` and visiting `localhost:8000` shows:
- The Kanban Studio UI (the beautiful Codex-built one)
- Drag and drop working
- Looking exactly as it did on Day 3

✅ Part 3 complete.

---

## 14. Part 4 — Fake User Sign-In

**Goal:** A login screen appears before the Kanban board. Users enter credentials to access their board.

### MVP Authentication Design

For the MVP:
- **One hardcoded user:** username = `user`, password = `password`
- Database schema designed to support multiple users in the future
- Simple session management (no OAuth, no JWT complexity for now)

### Result

Running the start script and visiting `localhost:8000`:
- A **login page** appears: "Sign in to continue to your Kanban board"
- Demo credentials shown on screen: `user` / `password`
- After login: full Kanban board
- **Logout button** in the top corner
- Logging out and back in: session works correctly

✅ Part 4 complete.

---

## 15. Part 5 — Database Schema Design

**Goal:** Design and document the database structure. Get human sign-off before building.

### Why Sign-Off Matters Here

Database schema is one of the few places where it's **very important to review before the agent builds it**. A bad schema is expensive to fix later — everything built on top of it may need to change.

### The Schema the Agent Proposed

```
Tables:
- users        (id, username, password_hash, created_at)
- boards       (id, user_id, title, created_at)  
- columns      (id, board_id, title, position, created_at)
- cards        (id, column_id, title, description, position, created_at)

Design notes:
- Title stored for future multi-board expansion
- Ordering handled via position field (enables drag-and-drop reordering)
- Migration approach documented
```

The instructor had considered storing board state as a JSON blob (simpler), but the agent's relational approach is **actually better**:
- More flexible for future features
- Easier to query and manipulate individual cards
- Better performance at scale
- Cleaner separation of concerns

> *"I probably would have done it differently, but then my way might have been a little bit more hacky. This is perhaps a better way of doing it."*

This is an important lesson: **sometimes the agent's design is better than yours**. Be open to it.

✅ Schema approved. Proceed to Part 6.

---

## 16. Part 6 — Backend API Routes

**Goal:** Build all the API endpoints the front-end will call to read and modify Kanban data.

### What Gets Built

Python FastAPI endpoints including:
- `GET /api/boards/{user_id}` — retrieve the user's board
- `POST /api/cards` — create a new card
- `PUT /api/cards/{card_id}` — update a card (title, description, position, column)
- `DELETE /api/cards/{card_id}` — delete a card
- `PUT /api/columns/{column_id}` — rename a column

### Verification

After Part 6, the server still runs cleanly. Nothing is broken. The back-end API exists but isn't yet connected to the front-end (that's Part 7).

✅ Git checkpoint taken. Proceed to Part 7.

---

## 17. Part 7 — Wiring Front-End to Back-End

**Goal:** Connect the Next.js front-end to the FastAPI back-end so that:
- Moving a card updates the database
- Renaming a column updates the database
- Logging out and back in shows the same board state

This is the **most significant change** of the whole build. The front-end needed substantial rewriting to make API calls instead of managing state locally.

### The Drag-and-Drop Bug

After Part 7, drag-and-drop mostly worked but had a bug: cards would be dragged, the target column would highlight correctly, but when the mouse was released, the card snapped back to its original position.

**Debugging approach:**

```
The persistence is working. But drag and drop seems to only work 
occasionally. Most of the time I drag a card, the next column 
highlights, but when I release the card goes back to its 
original position.

Please:
1. Reproduce the problem
2. Fix it  
3. Confirm it is fixed
```

### The Bizarre Resolution

The agent spent **30 minutes** in a loop trying to fix drag-and-drop. It kept jumping to conclusions, guessing at causes, applying fixes without proving them.

Then — unexpectedly — when the instructor went in to manually test... **it was already working**. The agent had actually fixed it earlier in the loop but then kept running failing automated tests and concluding the fix hadn't worked.

**The key insight:** The agent's **automated tests were wrong** — they were testing drag-and-drop in a way that didn't reflect actual browser behaviour. The fix was correct; the test was misleading the agent.

**Resolution:** The instructor manually verified the fix worked, then stopped the agent from continuing to thrash.

> *"Human involvement was needed to check and confirm that actually it's working fine."*

This is a perfect example of why you must keep your hands on the wheel — even in plan-execute mode.

### Final Verification of Part 7

```
1. Start the server
2. Login as user/password
3. Drag a card to a new column ✅
4. Open a new browser tab → go to localhost:8000
5. Login again
6. Card is still in the new column ✅ (persisted to database)
```

✅ Part 7 complete. Git snapshot taken.

---

## 18. Context Window Management — Resetting the Chat

After completing Parts 1–7, a critical context window management step was performed.

### The Problem

After many messages back and forth across 7 parts of the build, the conversation history is **enormous**. Even with compacting, the context is cluttered with:
- Old debugging sessions about drag-and-drop
- Superseded design decisions
- Test failure cycles that were eventually resolved
- Lots of old information that's no longer relevant

This cluttered context degrades the agent's performance on upcoming work (Parts 8–10).

### The Solution — Context Reset

**Step 1:** Update the plan to reflect everything done so far

```
Please confirm that plan.md is up to date with all the latest, 
including any design decisions that you made.
Let me know when ready.
```

**Step 2:** Take a git snapshot

```bash
git status
git add .
git commit -m "final updates after part 7"
```

**Step 3:** Start a completely new chat

In GitHub Copilot: right-click on the agent panel → **New Chat**

**Step 4:** First message in the new chat

```
Please read agents.md, then read the plan. 
Let me know any questions before we start part 8.
```

### Why This Works

By resetting the chat and pointing the fresh context to `plan.md`:
- The context window is **near-empty** — maximum efficiency
- The agent has all the relevant context from the plan document
- None of the old noise from debugging sessions
- It feels almost like the agent "decluttered its brain"

### The Trade-Off

After the reset, the agent briefly forgot the correct way to start the server and spent 5 minutes figuring it out again (it had learned this earlier in the conversation, which is now gone).

**Fix:** Ask it to update `plan.md` with the start command so it's always available in future resets.

> This is the balance: fresh context improves quality but occasionally requires re-teaching small things. The net effect is strongly positive.

---

## 19. Part 8 — AI Connectivity (OpenRouter)

**Goal:** The back-end can make API calls to OpenRouter. Verified with a simple "2+2" math test before any complex AI logic is added.

### The First AI Prompt to the New Chat

In the fresh chat context, with `agents.md` and `plan.md` loaded:

The agent asked clarifying questions about Part 8:
1. *"Should the '2+2' integration test be fully mocked or hit the actual OpenRouter endpoint?"*
2. *"Should this go under /api/ai or /api/chat?"*
3. *"Should the OpenRouter base URL be configurable or hardcoded?"*

**Answers given:**
- Test should hit **real OpenRouter** — no mocking — we need to confirm real connectivity
- Use `/api/chat` endpoint name
- Hardcoded base URL is fine for now

> The decision to test against **real OpenRouter** rather than mocking is deliberate. You can have tests that mock the API call, but you also need at least one test that confirms the actual connection works — otherwise you won't know until it's in production.

### What Part 8 Produces

- A `/api/chat` endpoint in FastAPI
- Reads the OpenRouter API key from `.env`
- Makes a real HTTP call to OpenRouter with a test prompt ("what is 2+2")
- Returns the response
- Integration test verifies a real response comes back

✅ Part 8 complete. Git snapshot taken.

---

## 20. Part 9 — AI Understands the Kanban Board

**Goal:** Extend the AI endpoint so it receives the current state of the Kanban board in its context, and can return structured responses that include both a text answer and instructions for card changes.

### What This Enables

When a user asks the AI "please summarise my project", the AI:
1. Receives the full board state (all columns and cards) as part of its prompt
2. Generates a text response based on that context
3. Optionally returns structured JSON describing card changes to make

### The System Prompt Design

The AI's system prompt for this feature:

```
You are an AI assistant for a project management application.
The user's Kanban board state is provided below.
You can answer questions about the project and suggest or make changes to cards.
When making changes, respond with valid JSON describing the changes needed.

[Board state injected here]
```

### Testing

The mock tests were replaced with real OpenRouter calls, confirming:
- The board state is correctly passed to the AI
- The AI understands and can reference the board content
- Structured card-change responses are correctly formatted

✅ Part 9 complete. Git snapshot taken.

---

## 21. Part 10 — Full AI Chat Interface

**Goal:** Build the polished AI chat widget in the sidebar of the Kanban app.

### What Gets Built

A chat interface embedded in the right sidebar of the Kanban board:
- **Message input** at the bottom
- **Conversation history** showing above
- Responses stream back from the AI
- When the AI decides to move a card, the board updates in real time
- "Hello, how can I help you with your board today?" initial message

### The Final Test

```
User: "Hi there"
AI: "Hello! How can I help you with your board today?"

User: "Please summarise my project"
AI: "Your project spans five columns: Backlog, To Do, In Progress, Review 
     and Done. [detailed summary follows]"

User: "Please move the 'Gather customer signals' card from Backlog to Done"
AI: [processes the instruction]
    [board updates in real time — the card moves]
```

**The card moved.** 🎉

### Persistence Verification

Open a new browser tab → `localhost:8000` → login → board loads → card is still in the Done column.

The change persisted to the database. ✅

---

## 22. Git Checkpointing — The Discipline of Snapshots

Throughout the build, git commits were taken at the end of every part. Here's the complete command pattern used:

```bash
# After completing each part:
git status                          # See all changed files
git add .                           # Stage all changes
git commit -m "part [N] complete"   # Commit with a descriptive message

# If you want to push to GitHub remote:
git push origin main
```

### Why This Is Essential

| Benefit | Explanation |
|---|---|
| **Rollback** | If Part 7 breaks something from Part 5, you can restore to the Part 5 snapshot |
| **Audit trail** | You know exactly what changed in each part |
| **Collaboration** | Others can see your progress and contribute |
| **Safety net for YOLO** | If the agent goes off the rails, you have a clean restore point |

### Git Commands Cheat Sheet for This Workflow

```bash
git status          # See what's changed
git add .           # Stage all changes (or: git add [filename] for specific files)
git commit -m "msg" # Commit with message
git log --oneline   # See commit history
git checkout [hash] # Restore to a previous commit
git diff            # See exactly what changed (before staging)
```

> *"I said I was going to do this at every step and I didn't always. But now we're getting to databases and it's more serious. This is a good point to be careful."*

---

## 23. Lessons Learned from the Full Build

### Lesson 1 — Step-by-Step Beats YOLO for Complex Projects

Yesterday's YOLO approach produced a beautiful but brittle single-file portfolio. Today's step-by-step approach produced a **real application** with proper architecture, persistence, and AI integration.

The trade-off: step-by-step takes longer and requires more engagement. But for anything that needs to actually work reliably, it's the right approach.

### Lesson 2 — The Agent Doesn't Always Test Its Own Work

**Multiple times** during this build, the agent declared a part "done" without actually running the server or executing the tests. This is one of the most common and costly failure patterns.

**Mitigation:** Always explicitly ask *"Did you test this yourself? Run the tests and confirm."*

### Lesson 3 — Sometimes the Agent's Design Is Better Than Yours

The database schema the agent proposed was more robust than what the instructor had in mind (JSON blob vs. relational tables). 

**Lesson:** Don't automatically override the agent's technical decisions. Evaluate them. Sometimes the agent knows better.

### Lesson 4 — Automated Tests Can Lie

The drag-and-drop was fixed but the agent's own tests kept failing — leading it to spend 30 minutes trying to fix something that wasn't broken. Manual testing by a human resolved this in seconds.

**Lesson:** Automated tests are valuable but not infallible. Human verification at key checkpoints is irreplaceable.

### Lesson 5 — Reset the Context Window on Long Builds

On a multi-part build spanning hours, the context window fills with stale, irrelevant information. A strategic reset — pointing the fresh context to a well-maintained `plan.md` — dramatically improves agent performance.

**Pattern:**
```
Long build → Context fills up → Quality degrades
→ Update plan.md with current state
→ Take a git snapshot
→ Start new chat
→ Point agent to plan.md
→ Quality recovers ✅
```

### Lesson 6 — Code Review Is Necessary Even When It Works

The final `main.py` was described as "a bit of a mess" — everything crammed into one Python module with no separation of concerns. The app works, but the code quality is poor.

**What to do next:** Ask a code review agent (e.g., Claude Opus) to audit the codebase and produce a remediation plan, exactly as was done on Day 4.

---

## 24. Week 1 Wrap-Up & Assignment

### Everything Built in Week 1

| Day | Project | Key Concept |
|---|---|---|
| Day 1 | 3D First-Person Shooter game | First contact with AI coding agents |
| Day 3 | Kanban board × 4 tools | Comparing Cursor, Copilot, Codex, Antigravity |
| Day 4 | Portfolio website + AI Digital Twin | YOLO mode, OpenRouter, cross-model review |
| Day 5 | Full-stack PM app with AI assistant | Structured build, Docker, FastAPI, SQLite |

### The Week 1 Assignment

Take the PM app and extend it. Suggested directions:

| Extension | Difficulty | How to Do It |
|---|---|---|
| **Refactor `main.py`** | Medium | Ask agent to restructure into proper modules |
| **Add multiple users** | Medium | The database already supports it — add the UI |
| **Multiple boards per user** | Medium | Schema already has this foundation |
| **Better chat UI** | Easy | Iterate on the chat widget appearance |
| **Response streaming** | Medium | Show the AI thinking in real time |
| **Remote database** | Medium | Replace SQLite with Supabase |
| **Deploy to production** | Hard | Ask agent for step-by-step Vercel/Railway/AWS instructions |

> *"Ask your model to build you a tutorial for how to deploy it to something like Vercel. It will tell you how to do it — it will actually deploy it for you."*

### Karpathy's Closing Words (from the same tweet series)

> *"LLM agent capabilities like Claude and Codex have crossed some kind of threshold of coherence around December of last year. We're causing a phase shift in software engineering. The intelligence part suddenly feels quite a bit ahead of all the rest of it... this is going to be a high-energy year as the industry figures out how to bring together this new capability."*

---

### Week 2 Preview — Vibe Engineering

Week 2 transitions from **Vibe Coding** to **Vibe Engineering** — the professional-grade approach. The big shift:

| Week 1 | Week 2 |
|---|---|
| IDE-based agents (Cursor, Copilot, Codex) | **CLI-based agents (Claude Code, Open Code)** |
| Plan mode in a sidebar | Terminal-native workflow |
| Approve diffs visually | Work in the command line like a pro |
| Simple projects | **Enterprise-grade development patterns** |

> *"Week two is huge. We make the transition from vibe coding to vibe engineering. We're going to be using Claude Code in anger and I love Claude Code and I can't wait to show it to you."*

**You are now 33% of the way through the course. Congratulations on completing Week 1! 🎉**

---

*📝 Notes compiled from Day 5 lectures of the AI Coder Course — covering all 7 segments: Karpathy's Tweet Timeline, Rules Recap, Web Apps 101, Docker Explained, Project Setup & agents.md, The 10-Part Build Plan (Parts 1–4), and the Full Build Completion (Parts 5–10 + Week 1 Wrap).*
