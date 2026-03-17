# 🤖 The Definitive AI Coder Course — Day 1 Complete Notes
### *The Missing Manual for Agentic AI Coding*

---

## Table of Contents

1. [Welcome & Course Philosophy](#1-welcome--course-philosophy)
2. [Setting Up Cursor AI](#2-setting-up-cursor-ai)
3. [Cursor Interface Orientation](#3-cursor-interface-orientation)
4. [Hands-On Demo: Building a 3D First-Person Shooter Game](#4-hands-on-demo-building-a-3d-first-person-shooter-game)
5. [Iterating with Your AI Agent](#5-iterating-with-your-ai-agent)
6. [The Missing Manual — Andre Karpathy's Landmark Tweet](#6-the-missing-manual--andre-karpathys-landmark-tweet)
7. [Who Is This Course For?](#7-who-is-this-course-for)
8. [What You Will Achieve by the End](#8-what-you-will-achieve-by-the-end)
9. [Meet Your Instructor](#9-meet-your-instructor)
10. [The 3-Week Course Roadmap](#10-the-3-week-course-roadmap)
11. [Vibe Coding, Vibe Engineering & Agentic Coders — The Terminology](#11-vibe-coding-vibe-engineering--agentic-coders--the-terminology)
12. [Types of Coding Agent Platforms](#12-types-of-coding-agent-platforms)
13. [The 8 Stages of AI Coding (Steve Yegge's Framework)](#13-the-8-stages-of-ai-coding-steve-yegges-framework)
14. [AI Costs — What You Need to Know](#14-ai-costs--what-you-need-to-know)
15. [Wrapping Up Day 1 — Key Reminders](#15-wrapping-up-day-1--key-reminders)

---

## 1. Welcome & Course Philosophy

### The Big Picture

This is described as the **"definitive AI Coder course"** — the *missing manual* for agentic AI coding. The promise of the course is a 3-week journey that takes you from wherever you are today to being an **expert in agentic engineering**.

The course is not a conventional one. Most courses begin with:
- Objectives
- Instructor introduction
- Curriculum walkthrough
- Logistics

This course **does not follow that structure**. Instead, it begins with **instant gratification** — rolling up sleeves and building something immediately, because learning by doing is the core philosophy here.

### Core Teaching Philosophy

| Principle | Explanation |
|---|---|
| **Instant Gratification** | Start building right away, even before full explanations |
| **Business-First** | Projects should have real-world commercial impact |
| **Breadth + Depth** | Cover a wide range of tools, but go deep on the most important ones |
| **Hands-On** | Learn by building actual projects, not just watching theory |

> **One Exception:** Day 1 is the *only* day where we build something purely for fun (a game). Every other project from this point on is commercially relevant.

---

## 2. Setting Up Cursor AI

### What is Cursor?

**Cursor** is the first tool used in the course. It is:
- One of the most **popular** AI coding tools available
- Based on **VS Code** (so it will feel familiar if you've used VS Code before)
- Extremely **easy to use**
- Has a **free trial** for new users

> If you've already used up your Cursor free trial, you can either watch the instructor or follow along with any other AI coding product.

---

### How to Download and Install Cursor

#### Step 1 — Go to the Website
- Open your browser and navigate to **cursor.com**
- Cursor's tagline: *"Built to make you extraordinarily productive"*

#### Step 2 — Download for Your Platform
- The landing page automatically detects your OS and offers the right download
- Available for: **Mac**, **Windows**, and **Linux**
- The instructor is on a Mac (M1/ARM); there is also a Windows walkthrough shown

#### Step 3 — Install

**On Mac:**
1. Download the file
2. Drag the Cursor app into your **Applications** folder
3. Done ✅

**On Windows:**
1. Open the downloaded installer file
2. Accept the agreement
3. Press **Next** through the defaults (the "Add to PATH" option is important — keep it checked)
4. Press **Install**
5. Done ✅

---

### Creating Your Cursor Account

1. Launch Cursor after installation
2. You will be prompted to **Sign In** or **Sign Up**
3. If you don't see the prompt, go to **File → New Window**
4. Click **Sign In** → a browser window opens
5. Choose **"Don't have an account? Sign Up"**
6. Fill in your details and answer a few questions
7. The free trial lasts **a couple of weeks** — more than enough to get started

> If you already have a Cursor account, simply log in.

---

## 3. Cursor Interface Orientation

When you open Cursor with a project, you'll see **three main panes**:

```
┌─────────────────┬───────────────────────┬───────────────────────┐
│                 │                       │                       │
│   LEFT PANE     │    MIDDLE PANE        │    RIGHT PANE         │
│                 │                       │                       │
│  File Explorer  │   Code Editor         │   Agent / Chat        │
│                 │                       │                       │
│  Shows all      │   Where you see       │   Where you talk      │
│  files in       │   and edit code       │   to the AI agent     │
│  your project   │                       │                       │
│                 │                       │                       │
└─────────────────┴───────────────────────┴───────────────────────┘
```

> If you don't see all three panes, go to **View → Appearance** and toggle until all panes are visible.

### Opening a Project

A "project" in Cursor means selecting a **directory (folder)** on your computer. That folder will house all the files related to your project.

**Typical folder structure:**
```
Home Directory (e.g., /Users/ed/)
└── projects/
    └── instant/       ← your new project folder
```

**Steps:**
1. Press **Open Project** in Cursor
2. Navigate to your home directory
3. Open or create a `projects` folder
4. Create a **new folder** (e.g., `instant`) inside it
5. Click **Open** (or **Select Folder** on Windows)
6. You'll see the folder name in the top-left — that confirms you're in the right place

---

## 4. Hands-On Demo: Building a 3D First-Person Shooter Game

### Why a Game?

This is the **only non-business project** in the entire course. Day 1's goal is to immediately show the power of AI coding tools in the most fun way possible. A game is a great, visual, entertaining demonstration.

### The Prompt Used

In the **right-hand pane** (the Agent/Chat panel), the following prompt was entered:

> *"Please build a website for a 3D first-person shooter game in an arena against one computer opponent, controlled by arrow keys and space bar to shoot."*

### What Happened Next

- The agent immediately started **planning** its next moves
- It began **creating files** automatically
- A file called `index.html` was created (and potentially more)
- The agent worked through the task **without needing step-by-step approval**

### Model Selection

In Cursor, you can choose which **AI model** powers your agent:
- If you're on the free plan, it may be set to **Auto** (Cursor picks for you)
- On paid plans, you can manually select a model (e.g., **GPT 5.2 Codex**, described as one of the strongest available at the time)
- Different users may get different results depending on the model used

> **Key Insight:** Everyone's experience with AI coding tools will be slightly different. There is inherent unpredictability and variation — that is normal.

### The Result

After the agent finished, the files were saved in the `instant` project folder. Double-clicking `index.html` opened the game in a browser:

- 🎮 **"Neon Arena"** — a First-Person Shooter game
- Controls: **Arrow keys** to move/turn, **Spacebar** to shoot
- One AI opponent to fight against
- Fully playable — all from a single prompt with zero manual coding

---

## 5. Iterating with Your AI Agent

One of the most important skills in agentic coding is **iterating** — giving follow-up instructions to improve what was built.

### Iteration 1 — Improving the Enemy Appearance

After the initial game was created, the next prompt was:

> *"That's great. Please add some detail to the opponent so that it looks more like an enemy."*

- The agent edited the existing files
- The opponent was updated to look more visually detailed and interesting

### Iteration 2 — Adding a HUD and Increasing Difficulty

The next prompt:

> *"Please add a Heads-Up Display (HUD) and also make the difficulty harder."*

- A HUD was added (showing health, score, etc.)
- The enemy became harder to beat
- All done without writing a single line of code manually

### If Something Goes Wrong

AI agents don't always get things right on the first try. If the game didn't work:
1. Tell the agent what went wrong (describe the bug or issue)
2. The agent will attempt to fix it
3. If it's completely broken, **delete the project folder** and start fresh
4. Try a different model or rephrase your prompt

> This is not an important project — it's an experiment. There's no cost to failure here.

---

### The Advanced Demo — What's Possible with More Techniques

At the end of the demo, the instructor showed a **more advanced version** of the same game — built using a technique called a **"RALF Loop"** with **Claude Code**. This was a *zero-shot* build: one prompt, no feedback, one iteration.

The result was dramatically more impressive:
- 🔫 A detailed 3D gun model visible in-hand
- ❤️ Health display at the top of the screen
- 💀 Kill counter
- 🗺️ A mini-map in the bottom-right corner
- 💊 Health pickups in the arena

> This is a **teaser** of what you'll be capable of by the end of this course. The RALF Loop and Claude Code techniques will be covered in later sessions.

---

## 6. The Missing Manual — Andre Karpathy's Landmark Tweet

A major inspiration for this course came from a tweet by **Andre Karpathy** — one of the founding members of OpenAI, a former researcher at Tesla and Stanford, and the person who coined the term **"vibe coding"**.

### Karpathy's Tweet (Paraphrased)

Karpathy wrote that he had *never felt so behind as a programmer*. He described the profession as being "dramatically refactored" — where the bits contributed by human programmers are becoming increasingly sparse.

He described a new layer of abstraction now required for programmers — one that involves:

- Agents and sub-agents
- Prompts, context, memory, modes
- Permissions, tools, plugins, skills, hooks
- MCP (Model Context Protocol)
- LSP, slash commands, workflows
- IDE integrations

He described these as fundamentally **stochastic, fallible, unintelligible, and changing entities** now intermingled with traditional good-old-fashioned engineering.

He concluded: *"Clearly some powerful alien tool was handed around — except it comes with no manual, and everyone has to figure out how to hold it and operate it while the resulting magnitude-9 earthquake is rocking the profession."*

### Why This Matters

**This course is the missing manual Karpathy is talking about.**

The goal is that by the end of 3 weeks, you can read that tweet again and understand every single term in it — not just understand it, but know how they fit together, where they work well, where they don't, and how to navigate this new world of agentic AI coding.

---

## 7. Who Is This Course For?

### Two Primary Archetypes

This course is designed for **two types of people**:

#### 🟢 Aspiring Engineers (Beginners/Junior)
- You may be new to coding or have only written a little
- You don't yet consider yourself an expert
- **Goal:** Be able to build complete, large-scale products with confidence, assisted by AI agents

#### 🔵 Senior / Staff Engineers (Experienced)
- You are an experienced coder
- You may feel overwhelmed by how fast AI coding tools are evolving
- You feel a bit like Karpathy's tweet — there's too much, how do I navigate it all?
- **Goal:** Learn how to accelerate what you can do, maximize the potential of agentic tools, and continue enjoying engineering

### The Reality: It's For Everyone

In practice, there will be something for every experience level:
- **For beginners:** Some advanced content may feel challenging — that's okay. Get the gist and keep moving.
- **For experts:** Some setup content (like creating project directories) will be obvious. Speed through those at 2x and focus on the advanced material.
- The course connects the dots across the spectrum.

---

## 8. What You Will Achieve by the End

By the end of the 3-week program, you will be able to:

1. **Build, debug, troubleshoot, and enhance** software products at any scale — from a small game to a large enterprise repository
2. **Navigate the full agentic AI coding landscape** — you'll understand every term in Karpathy's tweet
3. **Meet modern job requirements** — increasingly, employers expect developers to use generative AI tools effectively; you'll have the skills (MCP, skills, hooks, RALF loops, etc.) to demonstrate that
4. **Deliver high-quality software fast** using a team of agents working for you

---

## 9. Meet Your Instructor

### Ed Donner

- **Co-founder and CTO** of an AI startup called **nebula.io**
- Former **Managing Director at JP Morgan** — led a team of ~300 technologists in software engineering, Python, and analytics
- Started career in London, moved to Tokyo, then settled in **New York City** (lives 1 block from Times Square)
- Founded an AI startup called **Untapped**, which was acquired in 2021 (celebrated with a Times Square billboard!)
- Speaks at conferences and live events about LLMs and agents
- Has **400,000+ students** across his various courses on Udemy
- Personally replies to all messages — *"It's really me, not an agent. Try me and I'll reply right away."*

### His Other Courses (and How This Fits In)

| Course | Focus |
|---|---|
| **AI Builder** | Building solutions with platforms like N8N, 11Labs, agents and voice agents |
| **AI Engineer – Core Track** | Writing code to build AI products |
| **AI Engineer – Agentic Track** | Building agentic AI systems |
| **AI Engineer – ML Ops Track** | Machine learning operations |
| **Leadership Briefing** | Delivering AI to production, roadmaps, business impact |
| **AI Coder (this course)** | Using AI agents to write code |

> **Key Distinction:** Most of his courses are about *using code to build AI*. This course is the reverse — *using AI to write code*. It's a different but highly complementary perspective.

### Course Design Strategy: Breadth + Depth

The course deliberately combines:
- **Breadth:** Exposure to many different AI coding tools across different environments and job settings
- **Depth:** Deep mastery of CLI-based coding (specifically Claude Code and similar tools)

---

## 10. The 3-Week Course Roadmap

### Three Session Types

Every session falls into one of three categories:

| Type | Color | Description |
|---|---|---|
| **Core Skills** | Purple | Foundational concepts — agents, context, memory, etc. |
| **Platforms & Tools** | Yellow | Hands-on with tools like Cursor, Codex, Claude Code |
| **Commercial Projects** | Green | Real-world projects with business impact |

---

### 📅 Week 1 — Vibe Coding for Fun and Profit

*Focus: Stages 1–4 of the AI coding journey*

| Day | Topic |
|---|---|
| **Day 1** | The Agentic Coding Landscape (today) |
| **Day 2** | Foundations — Agents, Context, the `agents.md` file |
| **Day 3** | Tooling Deep-Dive — Cursor, Copilot, Codex, Antigravity |
| **Day 4** | Project — Yellow (first commercial project) |
| **Day 5** | Project — Commercial MVP |

---

### 📅 Week 2 — Vibe Engineering

*Focus: Stage 5 — CLI-based agentic coding as a professional*

| Day | Topic |
|---|---|
| **Day 1** | Deep dive into CLI coding with Claude Code and Open Code |
| **Day 2** | Commands, checkpoints, and the **RALF Loop** |
| **Day 3** | MCP, skills, and plugins (hot topic in the community right now) |
| **Day 4** | Building workflows, working with a team, debugging |
| **Day 5** | Meaty Project — Build a full **SaaS Platform** together |

---

### 📅 Week 3 — Agentic Engineering as an Expert

*Focus: Stages 6–8 — Multi-agent orchestration and advanced workflows*

| Day | Topic |
|---|---|
| **Day 1** | Multi-agents — running many agents and sub-agents with hooks |
| **Day 2** | Sandboxing and advanced safety for agentic AI |
| **Day 3** | Working with large codebases — survival guide |
| **Day 4** | Agent swarms and orchestrators |
| **Day 5** | **Capstone Project** — the grand finale |

> By the end of Week 3: *"You will be able to say yes, I am now an expert agentic engineer."*

---

## 11. Vibe Coding, Vibe Engineering & Agentic Coders — The Terminology

The terminology in this space is still evolving and can mean different things in different contexts. Here's a clear breakdown:

### The Emotional Journey of AI Coding (2024–2025)

Most people who have worked with AI coding tools have gone through a recognizable emotional arc:

```
Surprise → Denial → Astonishment → Frustration → Anger → Acceptance → Mastery
```

1. **Surprise** — Amazed at what these tools could do
2. **Denial** — Pushed back, skeptical
3. **Astonishment** — Tried it themselves and were genuinely impressed
4. **Frustration** — Things sometimes didn't work, repeated mistakes were maddening
5. **Anger** — At times, so frustrated you might literally argue with the AI
6. **Acceptance** — Started to understand where it's strong and where it's weak
7. **Inflection Point (late 2025)** — Claude Sonnet/Opus 4.5, Gemini 3, GPT 5.2 dramatically improved things; less frustration, more capability

---

### Key Terms Defined

#### 🌊 Vibe Coding
- **Coined by:** Andre Karpathy
- **What it means:** Fully surrendering to the AI — you give in to the vibes, embrace the exponential capability, and don't even look at the underlying code. You ask, the AI builds, you see what happens.
- **Connotation:** Sometimes used to describe a more *casual or amateurish* approach — let it go, throw it away if it doesn't work, try again.
- **Also used as:** A general umbrella term for this entire field of AI-assisted coding.

#### 🔧 Vibe Engineering
- **Coined by:** Simon Willison (a prominent writer and developer in the AI space)
- **What it means:** The more *professional and disciplined* side of using AI agents to build real software. You're still leveraging AI, but you're doing it with the rigor and responsibility of an experienced software engineer.
- **Connotation:** More systematic, more production-ready, more accountable.

#### 🤖 Agentic Coder *(Two Meanings — Context Matters!)*
- **Meaning 1:** A *person* who uses AI agents to help them write code (what you and the instructor are doing together)
- **Meaning 2:** A *platform or tool* (like Cursor or Claude Code) that is itself an agent that writes code
- **Rule of thumb:** If in doubt, ask for clarification on which meaning is intended.

---

### Three Surfaces for Interacting with Coding Agents

There are **three different environments** where you can work with AI coding agents:

#### 1. 🖥️ IDE (Integrated Development Environment)
- A full application with windows, menus, and panes
- Example: **Cursor** — what we used in today's demo
- The agent lives in a sidebar panel
- Best for: Visual, structured, beginner-friendly workflow

#### 2. 🔌 Plugin / Extension
- An add-on bolted onto an existing IDE (usually VS Code)
- Example: **GitHub Copilot** — the most popular plugin
- Available as a VS Code extension
- Best for: Developers already using VS Code who want to add AI without switching tools

#### 3. ⌨️ CLI (Command Line Interface)
- A terminal/command-line based environment — retro-looking black screen with text
- Examples: **Claude Code**, Cursor CLI, Codex CLI, Gemini CLI, Open Code, AMP
- **Pioneered by Claude Code** (started as a side project and exploded in popularity)
- Best for: Power users, large codebases, multi-agent workflows, maximum productivity
- Surprisingly: This "retro" interface turned out to be one of the most powerful ways to work with agents

> **Note:** Claude Code also has a plugin for VS Code and Cursor — so the lines can blur. The primary mode, however, is CLI.

---

### Popular Tools by Category

| Category | Tool |
|---|---|
| **IDEs** | Cursor, Codex (OpenAI), Antigravity (Google), Windsurf |
| **Plugins/Extensions** | GitHub Copilot (for VS Code) |
| **CLI Tools** | Claude Code, Open Code, AMP, Cursor CLI, Codex CLI, Gemini CLI |

> ⚠️ This space moves extremely fast. New tools appear constantly. The key skill is **separating signal from noise** — don't chase every new announcement. Focus on tools with proven, lasting impact (like Claude Code).

---

## 12. Types of Coding Agent Platforms

This section expands on the practical landscape of tools you'll encounter.

### The Signal vs. Noise Problem

The AI coding space generates a tsunami of new announcements, tools, and excitement every single day. Social media feeds are full of it. The critical skill is:

- **Identifying true breakthroughs** (e.g., when Claude Code was first released)
- **Distinguishing them from hype** (e.g., a new tool that gets buzz for a week and then fades)

> When in doubt — ask the instructor. That's what he's there for.

### Important Note on Terminology Overlap

Tools don't always fit neatly into one category. For example:
- Claude Code is primarily a **CLI** tool
- But it also has **plugin extensions** for VS Code and Cursor

This overlap is normal in a fast-moving space. The categories above are useful mental models, not rigid boxes.

---

## 13. The 8 Stages of AI Coding (Steve Yegge's Framework)

**Steve Yegge**, author of a popular tool called **Gastown**, wrote an influential post describing the stages you go through as you use AI in increasingly advanced ways. This framework maps to the 3-week curriculum of this course.

---

### Stage 1 — Chat-Based AI Assistance
- Using ChatGPT or similar to ask coding questions
- Using AI autocomplete as a reference
- The AI is a helper you *refer to*, not one that acts independently
- **Status:** Assumed knowledge — most learners can already do this

---

### Stage 2 — Coding Agent in the IDE Sidebar (Ask Permission Mode)
- You have a coding agent in the sidebar of your IDE (like Cursor)
- The agent asks for **permission before every change**
- You check every suggestion step by step
- The agent offers suggestions and makes changes only with **your express consent**

---

### Stage 3 — IDE Sidebar Agent in YOLO Mode
- Same as Stage 2, but you've **stopped approving changes manually**
- **YOLO** = *"You Only Live Once"* — you trust the agent completely
- You say: *"I accept everything, go for it, do whatever you want"*
- The agent works autonomously; you just watch the output

---

### Stage 4 — Agent as the Main Window (Focus Shift)
- A conceptual change: the agent **expands to occupy your main focus**
- You're no longer staring at the code — you're watching the agent's reasoning and output
- Code diffs fly by; you glance at them but don't stop to approve each one
- You might walk away and let it run
- **Key distinction from Stage 3:** Your attention is on the *agent*, not the *code*

---

### Stage 5 — CLI-Based Coding (Terminal)
- You've moved from the IDE to the **command line / terminal**
- You're using a tool like **Claude Code** in YOLO mode
- Diffs scroll by in the terminal — you're not even watching them
- You might kick it off and come back when it's done

---

### Stage 6 — Multiple Agents Running Concurrently
- You've **spawned multiple agents** working at the same time on your project
- Think of it like having a small team: 3–5 agents all running in your CLI
- You're coordinating their work manually

---

### Stage 7 — Managing 10+ Agents
- You've scaled up dramatically — **10 or more agents** running concurrently
- You're manually coordinating and managing all of them
- You're hugely leveraged — enormous output with agents and sub-agents all building for you
- But it requires significant coordination effort on your part

---

### Stage 8 — Agent Orchestration (Agents Managing Agents)
- You have an **orchestrator agent** that manages the other agents
- You're no longer manually coordinating — agents coordinate *each other*
- Possible hierarchy:
  - 1 top-level orchestrator agent
  - Multiple manager agents beneath it
  - Multiple worker agents beneath those
  - Specialized teams (testing team, design team, etc.)
- This is the **most advanced stage** in Steve's progression

---

### How the Stages Map to the Course

| Week | Stages Covered | Focus |
|---|---|---|
| **Week 1** | Stages 2, 3, 4 | IDE-based agentic coding (Cursor, Copilot, etc.) |
| **Week 2** | Stage 5 | CLI-based coding with Claude Code |
| **Week 3** | Stages 6, 7, 8 | Multi-agent, orchestration, and expert workflows |

> **The Sweet Spot for Enterprise Use:** Stages 5 and 6. These are where you build the most bulletproof, reliable, and commercially valuable software. Stages 7 and 8 are powerful, but their suitability for enterprise production use is still an open question.

---

## 14. AI Costs — What You Need to Know

AI costs are a frequent question. Here's a clear breakdown of what to expect:

### You Can Take the Entire Course for Free
- It is **entirely possible** to complete this course without spending any money on API costs
- Most tools have free tiers or trials
- Where paid features are shown, the instructor will note it and suggest free alternatives in the resources

### But You Can Also Spend a Lot
- Running 20 agents building something enormous? They'll gladly consume your budget
- Easy to burn money if you're not careful
- Always know what you're signing up for before enabling paid tiers

### The Instructor's Recommended Minimum Spend

| Tool | Recommended Plan | Cost |
|---|---|---|
| **Cursor** | Free trial (use while eligible) | Free |
| **Claude Code** | Max plan | ~$20/month |
| Beyond that | Only if you want to go more intense | Varies |

### The Golden Rule: You Are In Charge of Your Costs

> *"I'll take responsibility for getting you to be able to answer the Andre Karpathy tweet at the end of three weeks — but I can't take responsibility for the API costs. You need to make the decisions about what you spend."*

- Monitor your costs on each platform
- Understand free trial limits before signing up
- Be aware that pricing varies by region and that offers change frequently
- Check the course resources for tips on using free models

### Why Do These Tools Cost Money?

Running AI models requires:
- **Hundreds of trillions of floating point calculations** per request
- Enormous amounts of compute and electricity
- The cost reflects real infrastructure — it's not arbitrary

The $20–$30/month feel uncomfortable, especially when you're signing up for multiple services. But it's worth reframing it: like the cost of a good laptop, this is the new cost of working with powerful modern technology.

---

## 15. Wrapping Up Day 1 — Key Reminders

### What You've Accomplished Today

- ✅ Installed and set up **Cursor**
- ✅ Built a **3D first-person shooter game** from a single prompt — no manual coding
- ✅ Iterated on the game using follow-up prompts
- ✅ Understood the **Karpathy tweet** and why this course is the missing manual
- ✅ Learned the **terminology** — vibe coding, vibe engineering, agentic coder
- ✅ Got familiar with the **three surfaces** for AI coding (IDE, Plugin, CLI)
- ✅ Understood **Steve Yegge's 8 stages** of AI coding
- ✅ Got clarity on **AI costs** and how to manage them

**You are now 7% complete with the course! 🎉**

---

### Important Mindset Notes

#### Embrace Inconsistency
- Every time you run an AI agent, you may get a **different result**
- Your results will differ from the instructor's — and that's perfectly normal
- This course is like a **"choose your own adventure"** — your journey will be unique
- New models are released every week; you might actually get *better* results than shown

#### Don't Get Distracted by Noise
- The AI space is flooded with new announcements every day
- Social media can make everything feel urgent
- Focus on proven, impactful tools and concepts
- When uncertain about a new tool or announcement, ask the instructor

#### This Course is Different from Others
- There is no single "right answer" that everyone will get
- Different users, different models, different results
- This makes things exciting but also introduces challenges — embrace both

---

### Stay Connected with the Instructor

- **Q&A on Udemy** — post questions anytime, the instructor personally replies
- **Email** — always gets a reply (check spam if no response)
- **LinkedIn** — connect and interact; tag the instructor in posts about your progress for amplification
- **Share your work** — posting about what you build is a great way to build visibility and demonstrate expertise

---

### What's Coming Tomorrow (Day 2)

Tomorrow covers the **foundations** — the bedrock concepts that underpin everything:

- What are agents, really?
- The `agents.md` file — the heart of agentic AI coding
- Context — what it is and why it matters so much
- How AI agents actually "think" and plan

> *"With that, let's celebrate the fact that you're already 7% complete with this course. There's 93% of a great journey left — starting tomorrow with the foundations. I'll see you then."*

---

*📝 Notes compiled from Day 1 lectures of the AI Coder Course — covering all 7 segments: Welcome, 3D Game Build, The Missing Manual, Instructor & Roadmap, Vibe Coding Terminology, The 8 Stages, and Wrap-Up.*
