# 🤖 The Definitive AI Coder Course — Day 4 Complete Notes
### *YOLO Mode — Building a Personal Website with AI Digital Twin*

---

## Table of Contents

1. [Day 4 Overview — First Blue (Project) Day](#1-day-4-overview--first-blue-project-day)
2. [Recap — The Four IDEs & Their Models](#2-recap--the-four-ides--their-models)
3. [The Two Decisions Every Agentic Coder Must Make](#3-the-two-decisions-every-agentic-coder-must-make)
4. [Rules of Thumb for Choosing the Right LLM](#4-rules-of-thumb-for-choosing-the-right-llm)
5. [Five Principles for Successful Vibe Coding — Be the Boss](#5-five-principles-for-successful-vibe-coding--be-the-boss)
6. [Honest Productivity Assessment — What LLMs Actually Deliver](#6-honest-productivity-assessment--what-llms-actually-deliver)
7. [The Responsible YOLO — Important Warnings Before We Build](#7-the-responsible-yolo--important-warnings-before-we-build)
   - [The Anthropic Study on Junior Developers](#the-anthropic-study-on-junior-developers)
   - [The Jellyfin Open Source Policy](#the-jellyfin-open-source-policy)
8. [Today's Project — Personal Portfolio Website with AI Digital Twin](#8-todays-project--personal-portfolio-website-with-ai-digital-twin)
9. [Setting Up OpenRouter — API Access for Your App's AI](#9-setting-up-openrouter--api-access-for-your-apps-ai)
10. [Project Environment Setup](#10-project-environment-setup)
    - [Creating the Project Folder](#creating-the-project-folder)
    - [Creating the .env File](#creating-the-env-file)
    - [Creating the .gitignore File](#creating-the-gitignore-file)
    - [Preparing Your LinkedIn Profile PDF](#preparing-your-linkedin-profile-pdf)
    - [Configuring Cursor for YOLO Mode](#configuring-cursor-for-yolo-mode)
11. [Phase 1 — Building the Portfolio Website (YOLO)](#11-phase-1--building-the-portfolio-website-yolo)
12. [Phase 2 — Adding the AI Digital Twin Chat](#12-phase-2--adding-the-ai-digital-twin-chat)
13. [Checkpoint — Take a Backup](#13-checkpoint--take-a-backup)
14. [Iterating and Improving the Digital Twin](#14-iterating-and-improving-the-digital-twin)
15. [The "Get Unstuck" Technique — When to Start Fresh](#15-the-get-unstuck-technique--when-to-start-fresh)
16. [Advanced Technique — Having the AI Teach You Its Own Code](#16-advanced-technique--having-the-ai-teach-you-its-own-code)
17. [Cross-Model Collaboration — Using Opus for Code Review](#17-cross-model-collaboration--using-opus-for-code-review)
18. [Day 4 Wrap-Up & What's Next](#18-day-4-wrap-up--whats-next)

---

## 1. Day 4 Overview — First Blue (Project) Day

Day 4 is a **blue day** — the first real commercial project day of the course. Blue days are dedicated to building actual products with business relevance. After three days of setup, theory, and tool exploration, it's time to **build something real**.

### What We're Building

A **personal portfolio website** with a built-in **AI Digital Twin** — a chatbot that can answer questions about your career, background, and experience on your behalf. All of it built with a single YOLO-mode prompt, no agents.md, no step-by-step approval.

### Why This Project?

- It's **immediately useful** — a real website you could actually deploy and share
- It's **achievable in one session** with AI assistance
- It's **commercially relevant** — portfolio sites with AI interaction are increasingly expected for tech professionals
- It demonstrates **AI building AI** — the coding agent builds an app that itself calls an AI model

### Two Parts of Today

1. **Theory first:** Recap of IDEs/models, choosing models wisely, five principles of vibe coding, and a responsible warning about the downsides of YOLO
2. **Practice second:** Full hands-on YOLO build of the portfolio + digital twin, followed by iteration and advanced techniques

---

## 2. Recap — The Four IDEs & Their Models

Before diving into building, the instructor recaps the four tools from Day 3 and — critically — clarifies exactly which **AI model** was behind each one. This matters a lot for understanding why results differed.

### The Four IDEs Reviewed

| IDE | Type | Who Made It | Based On |
|---|---|---|---|
| **Cursor** | Standalone IDE | Anysphere | VS Code fork |
| **GitHub Copilot** | VS Code Extension | GitHub/Microsoft | VS Code plugin |
| **Codex** | VS Code Extension | OpenAI | VS Code plugin |
| **Antigravity** | Standalone IDE | Google | VS Code fork |

> **Key observation:** Three of the four tools are forks or extensions of VS Code. Microsoft open-sourced VS Code, making it the foundation of the entire AI coding IDE ecosystem.

---

### The Models Used Behind Each Tool

| Tool | Model Used | Model Type | Context Window |
|---|---|---|---|
| **Cursor** (Auto mode) | Composer (Anysphere's own model) | Fast frontier | 200,000 tokens |
| **GitHub Copilot** (Auto mode) | Claude Haiku 4.5 (likely) | Fast/small frontier | 200,000 tokens |
| **Codex** | GPT 5.2 Codex | Top frontier (coding-specialised) | 272,000 tokens |
| **Antigravity** | Gemini 3 Pro | Top frontier | 1,000,000 tokens |

### Model Category Definitions

Understanding model categories is essential for making smart decisions:

#### Fast Frontier Models (Small/Quick)
- Examples: **Composer** (Anysphere), **Claude Haiku 4.5**
- Fast, low-cost, good for simple tasks
- Generate code quickly
- Less reliable for complex or innovative tasks
- **Not recommended for YOLO mode on important work**

#### Top Frontier Models (Powerful)
- Examples: **GPT 5.2 Codex**, **Gemini 3 Pro**, **Claude Opus 4.5**
- Slower, more expensive
- Dramatically better output quality
- **Recommended for YOLO mode** on real projects
- The reason Codex's Kanban output on Day 3 was so impressive

---

## 3. The Two Decisions Every Agentic Coder Must Make

A crucial mental model introduced today: **there are two separate decisions** to make when using any AI coding tool, and most people only think about one of them.

```
┌─────────────────────────────────────────────────────┐
│            THE TWO DECISIONS                        │
│                                                     │
│  Decision 1: WHICH IDE / TOOL?                      │
│  ─────────────────────────────                      │
│  Cursor? Copilot? Codex? Antigravity?               │
│  → Mostly a matter of personal preference,          │
│    team conventions, and plan/pricing               │
│    They are fundamentally all doing the same thing: │
│    calling an LLM in a loop with tools to achieve   │
│    a goal. Minor differences in UX and features.    │
│                                                     │
│  Decision 2: WHICH LLM / MODEL?  ← The BIG one     │
│  ────────────────────────────────                   │
│  GPT 5.2 Codex? Claude Opus? Gemini 3 Pro?          │
│  → THIS is what actually determines output quality  │
│    This is where you spend your time and money      │
│    Most IDEs let you switch models freely           │
└─────────────────────────────────────────────────────┘
```

> *"The big decision is what LLM are you using to actually make the decisions. That is where you want to spend your time and choose your money wisely."*

Most of the IDEs (except Cursor with its proprietary Composer model) let you connect to any of the major frontier models. So the **tool** is less important than the **model**.

---

## 4. Rules of Thumb for Choosing the Right LLM

### Rule 1 — Favour Smart Over Fast

> *"I would personally always tend to favour a smart model over a fast model."*

It may seem more efficient to use a cheap, fast model. But in practice:
- A fast/cheap model makes more mistakes
- You spend time iterating to fix those mistakes
- The total time to a working result is often **longer** with a cheap model than a smart one

**Waiting for a smart model to think is almost always faster overall than debugging the output of a dumb model.**

---

### Rule 2 — Set a Budget, Then Pick the Best Model That Fits

Rather than starting with the cheapest option and upgrading when needed, do it the other way:

1. Decide how much you're willing to spend on a task
2. Pick the **most intelligent model** your budget allows
3. Stick to it

> *"I tried saving extra money by using a cheaper model. It usually ends up costing more because of the extra iterations and the time drain."*

---

### Rule 3 — Smaller Models Need More Precise Prompts

If you must use a smaller/cheaper model (free open-source models, etc.), compensate with:
- Much more detailed and precise prompts
- Think of it as writing a **formal specification** rather than a casual instruction
- Provide significantly more oversight — approve every step
- Do **not** use YOLO mode with small models on important work

---

### Rule 4 — YOLO Only with Top Frontier Models

This is the clearest and most direct rule:

| Model Tier | Recommended Workflow |
|---|---|
| **Top frontier** (GPT 5.2 Codex, Gemini 3 Pro, Claude Opus 4.5) | ✅ YOLO is viable — you can let it run and expect good results |
| **Fast frontier** (Composer, Claude Haiku) | ⚠️ Step-by-step only — baby steps, approve each change, watch every diff |
| **Small open-source** (free models) | ❌ YOLO is very risky — high chance of coming back to nonsense |

> *"If you're going to YOLO, the chances are so high with a smaller model that you'll let it go, come back later, and just have a pile of nonsense."*

---

## 5. Five Principles for Successful Vibe Coding — Be the Boss

This is one of the most important sections of the entire course — a framework for staying in control and getting the best out of agentic coding. The overarching theme: **you are always the boss**.

---

### Principle 1 — Write a Great agents.md

The single biggest lever you have for quality is your instructions. A great `agents.md` covers three things:

```
1. SPEC        → Exactly what needs to be built (clear, unambiguous)
2. STYLE       → How it should be built (coding standards, frameworks, UI approach)
3. SUCCESS     → How to know when it's done (criteria, tests, definition of done)
```

Keep it concise. Every word takes up context window space and should earn its place.

---

### Principle 2 — Start Simple

**Don't try to boil the ocean.** This applies at two levels:

#### Level 1 — Start with a simple agents.md
The first version of your project instructions should describe the simplest possible MVP. Not the full vision — just the core feature that proves the concept works.

#### Level 2 — Iterate incrementally
Once the simple version works, add complexity in layers:
- Build the basic version → verify it works
- Add feature 2 → verify it works
- Add feature 3 → verify it works
- Never move forward until the current step is confirmed working

> *"If you try and start by boiling the ocean with a super complicated application, you might go off track, off the rails, it might not work, and you'll just get stuck."*

---

### Principle 3 — Work Incrementally and Validate Constantly

At every step, before moving on:
- ✅ Test that the current step works
- ✅ Validate against your success criteria
- ✅ Only then allow the agent to move to the next step

This disciplined approach means you always know exactly where things stand. If something breaks, you know which step introduced the problem — making it easy to roll back.

---

### Principle 4 — Don't Get Lazy

This is the most psychologically important principle — and the easiest one to violate.

When early results are impressive (and they will be), there's a powerful temptation to:
- Stop checking every step
- Trust the agent completely
- Just keep pushing forward without validation

**Resist this.** The moment your guard comes down is the moment the agent will make a terrible assumption that cascades into a large problem — and you won't notice until you're many steps ahead.

#### The Danger Pattern
```
Agent declares: "Found the problem! Fixed it! ✅"
Reality: Agent guessed, didn't test, may have broken something else
Your response: Accept it and move on
Result: A hidden bug that surfaces much later
```

#### The Right Response Pattern
```
Agent declares: "Found the problem! Fixed it!"
Your response:
  → "Show me how you reproduced the bug"
  → "What was the root cause?"
  → "Show me the test results confirming it's fixed"
  → Only accept once evidence is provided
```

Always demand:
- Evidence of problem reproduction
- Root cause analysis (not guessing)
- Proof the fix works

---

### Principle 5 — Embrace the Frustration as Part of the Process

There will be moments of genuine frustration:
- The agent makes the same mistake repeatedly
- You add it to `agents.md` with "NEVER do this again" — and it does it again
- It gets stuck in a loop fixing one thing and breaking another
- You feel like yelling at it (the instructor admits to doing this)

**This is normal. It is part of the process.**

What to do when hitting these walls:
1. Recognise it's a limitation of the model
2. Find a way to work around it (different phrasing, different approach, different model)
3. Manage it with "style" — don't let frustration spiral into wasted time
4. Remember: these models give enormous advantages; the downsides are the price of admission

> *"Managing the downsides is the key path to success."*

---

### Guidance for Different Experience Levels

#### For Junior Engineers / Beginners
- **Use this as a learning opportunity** — don't let the AI do all the thinking
- Ask the LLM to explain what it just built
- Study the code it produces, even if you didn't write it
- Develop healthy skepticism — the AI is often overconfident and wrong
- Think of it as a very eager but sometimes misguided assistant
- **If you let the AI do everything, you won't grow** — and that will hurt you later

#### For Senior Engineers
- You're actually in the best position to use these tools — you can tell when something is wrong
- Keep in mind this is a productivity multiplier, not a replacement
- The joy of coding changes: less line-by-line satisfaction, more system-level building
- You gain new superpowers: front-end, DevOps, Terraform — things you couldn't do before
- Embrace the trade: some old joys replaced by new, bigger ones

---

## 6. Honest Productivity Assessment — What LLMs Actually Deliver

A grounded, non-hyped breakdown of when AI coding agents genuinely help and when they don't:

### Where LLMs Are Genuinely Transformative (10x+)

| Scenario | Impact |
|---|---|
| Building a **Kanban app** in Next.js from scratch | Days → Minutes. Demonstrably a 10x change |
| **Greenfield MVP** with lots of boilerplate | Very high multiplier |
| Front-end components with **well-understood patterns** | Enormous speedup |
| DevOps, Terraform, deployment scripts | Opens entire domains previously inaccessible |

### Where LLMs Are Incrementally Better (2x–5x)

| Scenario | Impact |
|---|---|
| Adding features to **existing large codebases** | More moderate — context is harder to manage |
| **Complex backend changes** in legacy systems | Reduced effectiveness |
| Integration work with established enterprise systems | Helpful but not transformative |

### Where LLMs Can Actually Slow You Down (<1x)

| Scenario | Impact |
|---|---|
| Cutting-edge technology not well represented in training data | Agent generates non-idiomatic, broken code |
| **Streamable HTTP servers**, very new protocols | Agent keeps getting it wrong; you'd be faster doing it yourself |
| Highly innovative architectural decisions | Agent defaults to patterns that may not fit |

### The Balanced Verdict

> *"As an aggregate, it is a multiplier — but it's not a 10x. How much more depends critically on the project."*

- **Always a positive** when using top coding agents — always speeds things up *somewhat*
- **How much** varies enormously based on task type, project size, skill match, and novelty
- **Small greenfield MVPs:** Very significant multiplier
- **Large legacy projects:** Moderate, incremental improvement
- **The key skill:** Quickly recognising which category a task falls into, so you set the right expectations

---

## 7. The Responsible YOLO — Important Warnings Before We Build

Before getting into YOLO mode, the instructor presents two sobering, real-world counterpoints that every agentic coder should internalise.

### The Anthropic Study on Junior Developers

**Source:** An Anthropic blog post on AI assistants and coding skill formation

**What they studied:** Two groups of junior developers:
- Group A: Using AI assistants to complete a coding task
- Group B: Completing the same task without AI assistance

**The result:**

| Group | Quiz Score on Underlying Technology |
|---|---|
| Used AI assistant | **50%** average |
| Did not use AI | **67%** average |

**The implication:** The AI-assisted group had a slightly higher productivity outcome on the immediate task — but they understood the technology significantly less. The learning was sacrificed for the short-term output.

> **Takeaway for learners:** Using AI is not an excuse to stop learning. Constantly ask the AI to explain what it built. Don't let it do all the thinking. The junior engineer who becomes dependent on AI without building understanding will hit a ceiling — and that ceiling will be painful.

---

### The Jellyfin Open Source Policy

**Who is Jellyfin?** A popular open-source media streaming platform with many community contributors.

**What they published:** A formal AI-assisted development policy for contributors who use AI to generate code.

Here are the key rules, quoted and explained:

#### On Communication (Issues, Comments, Pull Requests)

> LLM output is **prohibited** for direct communication — issues, comments, feature requests, pull request descriptions, forum posts.

Exception: translation (and you must note that you used AI for translation).

**Why this matters:** AI-generated PR descriptions and issue comments flood maintainers with verbose, low-signal noise. It shifts the burden of understanding from the person who wrote the code to the people who have to review it. That's not fair.

#### On Code — The Formal Policy

The Jellyfin policy states (paraphrased and condensed):

| Rule | Detail |
|---|---|
| **Contributions must be concise and focused** | If a PR targeting feature X is also touching unrelated Y and Z, it will be rejected |
| **PRs must use small, manageable commits** | No massive single-commit AI dumps |
| **Quality and formatting standards must be upheld** | LLM-generated slop will be rejected |
| **Do not commit LLM meta-files** | Don't include `.cursor` folders, `agents.md`, etc. in your PR |
| **You must be able to explain the code** | If you can't explain what changed and why — without AI help — the change is not welcome |
| **You must test it yourself** | You cannot just trust the AI's test claims |

#### The Golden Rule of the Jellyfin Policy

> *"Do not just let an LLM loose on the codebase with a vague vibe prompt and then commit the results as-is. This is lazy development and will always result in a poor-quality contribution from our perspective. We are not at all interested in such slop. Make an effort, or please do not bother."*

**Why this is highlighted in the course:**

> *"I think this is actually really well written. It is brave of them to be so upfront about it and put in writing what a lot of us feel — this sense of the asymmetry that it is so easy to generate tons of LLM code and then just submit it somewhere. The onus falls on the senior people to go through it and try to digest it. That's not fair."*

#### The Principle to Take Away

Whether or not you ever contribute to open source, this policy expresses a professional standard that applies everywhere:

- **You own the code** — regardless of who (or what) wrote it
- **You must understand the code** — "the AI wrote it" is not an explanation
- **You must be able to defend it** — in code review, in testing, in production
- **Quality is your responsibility** — not the AI's

---

## 8. Today's Project — Personal Portfolio Website with AI Digital Twin

### What We're Building

A **Next.js portfolio website** that:
1. Reads your **LinkedIn profile** and builds a professional "about me" site
2. Includes a **digital twin chat interface** — an AI chatbot that answers questions about you and your career
3. Has navigable sections: About Me, Career Journey, Portfolio (coming soon), Digital Twin Chat
4. Makes live API calls to an LLM via **OpenRouter** for the chat functionality

### The Prompt Used (Single YOLO Shot)

```
Please build me a professional website running locally.
My LinkedIn profile is in LinkedIn.pdf.
Make the website stunning — enterprise meets edgy.
It should include:
- About me
- My career journey
- Links to a portfolio (for future)
- A rate/contact section

Make it as slick and professional as possible.
Let me know when complete.
Use Next.js.
```

That's it. No `agents.md`. No step-by-step plan. Pure YOLO.

---

## 9. Setting Up OpenRouter — API Access for Your App's AI

### What is OpenRouter?

**OpenRouter** (openrouter.ai) is a service that acts as a **unified gateway** to multiple AI models from different providers:
- OpenAI (GPT models)
- Anthropic (Claude models)
- Google (Gemini models)
- Open-source models (Llama, Mistral, etc.)

#### The Problem it Solves

Without OpenRouter, to call multiple AI providers you'd need to:
- Create separate accounts with OpenAI, Anthropic, and Google
- Put money on each separately
- Maintain separate API keys
- Write different authentication code for each

OpenRouter consolidates all of this into **one account, one API key, one interface**.

#### Free vs. Paid Models

OpenRouter offers both:
- **Free models** — open-source models you can call at no cost (with some conditions)
- **Paid models** — frontier models like GPT 5.2, Claude Opus, Gemini Pro (pay per token)

---

### Creating an OpenRouter Account

1. Go to **openrouter.ai**
2. Click **Sign Up**
3. Use Google credentials or create an account
4. Answer any onboarding questions

---

### Creating an API Key

1. Click your **avatar/profile menu** (top right)
2. Select **Keys**
3. Click **Create API Key**
4. Give it a name (anything descriptive, e.g., "portfolio-site-key")
5. Optional: Set a **monthly spend limit** (e.g., $5 max per month) — recommended to avoid surprises
6. Optional: Set an **expiry date**
7. Click **Create**
8. **IMMEDIATELY copy the key** — it starts with `sk-or-` (secret key, open router)

> ⚠️ **Critical:** Copy the key exactly as shown, including the `sk-or-` prefix. A single wrong character will cause authentication failures. If you lose it or make an error, simply delete it and create a new one.

---

### Enabling Free Models (Optional)

If you want to use free open-source models through OpenRouter:

1. Go to **avatar menu → Settings**
2. Scroll to **Privacy and Guardrails**
3. Turn ON: **"Enable free endpoints that might train on inputs"**
4. Turn ON: **"Enable free endpoints that may publish your prompts"**

> **Important:** These settings acknowledge that free models may use your data for training and may share your prompts. Only enable this if you're comfortable with that trade-off and are not sending sensitive information.

---

### Adding Credits (For Paid Models)

If you want to use a paid frontier model for your digital twin:

1. Go to **avatar menu → Credits**
2. Add funds — OpenRouter's minimum top-up is approximately **$2** (much lower than OpenAI's $5 minimum)
3. This amount draws down as you use paid models

> For a personal portfolio digital twin with occasional use, $2–$5 is sufficient for many months of usage.

---

### Finding the Right Model Name

When you tell the coding agent which model to use, you need the **exact model identifier string**:

1. Go to **openrouter.ai/models** (in the main navigation)
2. Search for the model you want (e.g., type "free" to see free models, or search "GPT OSS")
3. Find the model and copy its **exact identifier string** (e.g., `openai/gpt-4o-mini-free`)
4. This string goes into your prompt when telling the agent which model to call

---

## 10. Project Environment Setup

### Creating the Project Folder

In Cursor:
1. Go to **File → New Window**
2. Press **Open Project**
3. Navigate to your `projects` folder
4. Create a **new folder** called `site`
5. Open it

You should now see `SITE` in block capitals in the top left — confirming you're in the right project.

---

### Creating the .env File

The `.env` file stores **environment variables** — configuration values that your app reads at runtime. Critically, API keys live here so they're never hard-coded into source code.

**Step 1:** Right-click in the file explorer → **New File**

**Step 2:** Name it exactly:
```
.env
```

**Step 3:** Inside the file, type:

```
OPENROUTER_API_KEY=paste-your-key-here
```

Replace `paste-your-key-here` with the OpenRouter key you copied earlier.

> If using OpenAI directly instead of OpenRouter, use:
> ```
> OPENAI_API_KEY=your-key-here
> ```

**Step 4:** Save with `Cmd+S` (Mac) or `Ctrl+S` (PC)

---

#### ⚠️ Why .env Files Are Critical Security

API keys in `.env` files are treated as **secrets**. They should:
- **Never** be committed to Git (version control)
- **Never** be shared publicly
- **Never** be hard-coded in source files that get checked in

A leaked API key means someone else can use your account and run up charges in your name.

---

### Creating the .gitignore File

A `.gitignore` file tells Git which files to **never include in the repository**.

**Step 1:** Right-click → **New File**

**Step 2:** Name it:
```
.gitignore
```

**Step 3:** Inside it, type:
```
.env
```

**Step 4:** Save

Now even if you later initialise this as a Git repository (which you should eventually do), the `.env` file will never accidentally get committed and pushed.

> This is always good best practice. Make `.env` the very first entry in every `.gitignore` you create.

---

### Preparing Your LinkedIn Profile PDF

The agent will use your LinkedIn profile as the source of truth for your website content.

**Option 1 — Export LinkedIn Profile as PDF**
1. Go to your LinkedIn profile page
2. Click **Resources** (top of profile)
3. Select **Save to PDF**
4. Move the downloaded PDF into your `site` project folder

**Option 2 — Copy/Paste (if PDF export is unavailable)**
- Copy all the text from your LinkedIn profile
- Paste it into a text file
- Save it in the `site` folder as `linkedin.txt`

**Option 3 — Use your CV/Resume**
- If you have an existing PDF CV/resume, use that instead

---

### Configuring Cursor for YOLO Mode

Open Cursor Settings:
- Mac: `Cmd+Shift+J`
- PC: `Ctrl+Shift+J`
- Or via the Settings menu

#### Settings to Configure

| Setting | Location | Value to Set |
|---|---|---|
| **Usage summary** | Agents section | Change from "Auto" to "Always" (shows context usage) |
| **Auto run / YOLO** | Agents → Auto Run | "Run everything unsandboxed" (for YOLO) |
| **Model selection** | Models tab | Turn on GPT 5.2 Codex Hi (or your preferred frontier model) |

> If you're not comfortable with full YOLO mode, leave Auto Run on "Ask every time" — you'll still see the full build happening, just with permission prompts.

---

## 11. Phase 1 — Building the Portfolio Website (YOLO)

### The Prompt

In the Cursor agent panel (right side), make sure:
- Model is set to **GPT 5.2 Codex Hi** (or your preferred frontier model)
- Auto run is on **Run everything unsandboxed**

Then paste this prompt and press Enter:

```
Please build me a professional website running locally.
My LinkedIn profile is in LinkedIn.pdf.
Make the website stunning — enterprise meets edgy.
It should include:
- About me
- My career journey
- Links to a portfolio (for future)

Make it as slick and professional as possible.
Let me know when complete.
Use Next.js.
```

### What the Agent Does

The agent:
1. Reads the LinkedIn PDF you provided
2. Plans the website structure
3. Creates a `web/` subdirectory (good practice — keeps the Next.js app isolated)
4. Builds the full Next.js application
5. Generates pages, components, and styling
6. Runs into errors, detects them, and self-corrects
7. Eventually signals completion

---

### Launching the Website

Open the terminal in Cursor (`Ctrl+Backtick` or `View → Terminal`):

```bash
cd web
npm run dev
```

Then open a browser and visit: `http://localhost:3000`

---

### What the Result Looks Like

The output was described as:

- **Beautiful dark-themed design** — professional and "enterprise meets edgy"
- **About Me section** — pulled directly from the LinkedIn profile
- **Career Journey section** — with dark/dramatic styling that gets darker as you scroll
- **Portfolio section** — placeholder (coming soon)
- **Navigation** — working links to sections (career, portfolio, contact)
- **Contact links** — real email address extracted from LinkedIn, LinkedIn profile link
- **Clever detail:** Detected the instructor's personal website from LinkedIn and linked to it

> *"First impression positive. I like this. I like it a lot. I think it does look quite enterprise meets edgy."*

---

### When Things Don't Work — YOLO Debugging

If the first run shows errors (which it likely will), the YOLO approach to debugging is:

1. Copy the **entire error message** from the terminal
2. Paste it directly into the agent chat
3. Press Enter — no explanation needed

```
[paste error here]
```

The agent reads the error and fixes it. No explanation required. Pure vibe.

> *"We are vibing. We are YOLOing. We're not going to even bother explaining ourselves. We just send it the error."*

---

## 12. Phase 2 — Adding the AI Digital Twin Chat

Once the base website is working, it's time to add the AI chatbot.

### The Prompt

```
That's great. Please now add the ability to have an AI chat with a 
digital twin which can answer questions about my career.

Please use OpenRouter.
My OpenRouter API key is in the .env file in the project root.
Please use the model named: [paste exact model identifier from OpenRouter]

Make the changes. Make sure it works. Let me know when ready for me.
```

> Replace `[paste exact model identifier]` with the model string you copied from openrouter.ai/models (e.g., `openai/gpt-4o-mini-free` or `openai/gpt-4.1-nano`).

---

### What Gets Built

The agent:
1. Creates an **API route** in Next.js (`/api/chat/route.ts`) — the server-side code that calls OpenRouter
2. Builds a **chat UI component** in the frontend
3. Wires the UI to the API route
4. Sets up the system prompt for the digital twin — telling it to answer as you, based on your profile
5. Reads the API key from the `.env` file

---

### How It Works Under the Hood

When you look at the generated code in `web/src/app/api/chat/route.ts`, you'll see:

```
Client (chat UI) 
    → POST /api/chat 
    → Next.js API route (server-side)
    → OpenRouter API (with your API key)
    → The LLM model you specified
    → Response streams back to the UI
```

The key thing to inspect here is the **system prompt** — the instructions telling the AI who it is and how to respond. The initial version may be very simple (just a few lines saying "You are [name]"). The system prompt should ideally include your full LinkedIn profile so the AI can give detailed, accurate answers.

---

### Testing the Digital Twin

Visit `http://localhost:3000` and scroll to the Digital Twin section.

Try questions like:
- *"Hi there"*
- *"What are you most proud of?"*
- *"Tell me about your career"*

If it's working, you'll get responses that sound like you — drawing on information from your LinkedIn profile.

---

## 13. Checkpoint — Take a Backup

At this point — before making further changes — **take a backup**.

### Why Backups Matter in YOLO Mode

When YOLOing, the agent has full permissions. A well-intentioned change can sometimes break multiple things at once. Having a backup means you can always restore to a working state.

### Simple Backup Method (No Git Knowledge Required)

```bash
# In your projects directory:
# Duplicate the entire "site" folder and rename it
# On Mac: just copy-paste the folder in Finder and rename it
# On PC: copy-paste in File Explorer
```

Name it something like `site_backup_working` so you know it's a good state.

### Proper Method — Git Commits

If you know Git:

```bash
cd site
git init
git add .
# First, make sure .gitignore has .env listed (which it does)
git commit -m "Working site with digital twin"
```

Now you have a committed checkpoint you can always return to.

> There's an existing `.git` folder inside the `web/` subdirectory (from Next.js scaffolding). If you want a single repo for the whole project, remove the nested `.git` and initialise one at the `site/` level. If Git is new to you, the simple folder-copy approach works fine for now.

---

## 14. Iterating and Improving the Digital Twin

After the initial build, there are typically several things to improve. Here's how to approach each type of issue:

### Problem 1 — The System Prompt Is Too Thin

The initial system prompt might only say something like:
> *"You are Ed Donner. Answer questions about Ed's career."*

This is too vague. The full LinkedIn profile should be embedded in the system prompt so the digital twin has all the context it needs for detailed, accurate responses.

**Fix prompt:**
```
Please improve the AI chat feature. The system prompt should include 
the full content of my LinkedIn profile so the AI can give detailed, 
accurate answers. Currently the system prompt is too vague.
```

### Problem 2 — Chat UI Looks Rough or Has Styling Issues

The initial chat interface may have formatting problems — wrong colors, awkward layout, elements that don't match the rest of the site.

**Fix prompt:**
```
The chat interface styling doesn't match the rest of the site. 
Please improve it — it should look polished and match the 
enterprise/edgy aesthetic of the main site.
```

### Problem 3 — Page Scrolls to the Wrong Section on Load

The page might automatically scroll to the chat section when it loads, which feels jarring.

**Fix prompt:**
```
When the page loads, it automatically scrolls down to the digital 
twin section. Please fix this — the page should load at the top.
```

### Problem 4 — Broken Navigation Links

Some navigation links may not work correctly.

**Fix prompt:**
```
The [section name] navigation link isn't working. Please debug and fix it.
```

---

## 15. The "Get Unstuck" Technique — When to Start Fresh

One of the most valuable practical techniques of the day: what to do when an agent gets stuck in a loop.

### The Pattern That Gets Stuck

```
You: "Please fix the chat colors — they look wrong."
Agent: Applies a fix
You: "Still wrong."
Agent: Applies a slightly different fix
You: "Still wrong — now it's worse."
Agent: Tries again, same category of fix
(repeat 4–5 times with no real progress)
```

This happens when:
- The agent has committed to one approach and keeps iterating within that dead end
- The original code has structural issues that can't be patched incrementally
- The model is going in circles and losing coherence with each iteration

### The Solution — Nuclear Reset

Instead of asking it to fix the same broken thing again, tell it to **start that component from scratch**:

```
"Don't try to fix the current chat interface. 
Remove it entirely and build a completely different one.
Start fresh — the current implementation is the problem."
```

**What this does:**
- Breaks the agent out of the iterative loop
- Forces a fresh approach with no baggage from the previous failed attempts
- Often produces a dramatically better result in one shot

> *"There comes a point when you get sort of stuck in a rut. You're asking the model to make a change and it's making the same mistake or it's just stuck. There's a point when you can just say, let's approach it differently. That might be easier than trying to figure out what's going wrong."*

---

## 16. Advanced Technique — Having the AI Teach You Its Own Code

One of the most powerful and underused techniques in agentic coding: **asking the agent to explain and document what it just built**.

### Why This Matters

Without this step, you have a working website but you don't understand it. That means:
- You can't maintain it
- You can't explain it in a code review
- You don't learn anything
- You violate the Jellyfin principle: "you must be able to explain the code"

### The Tutorial Prompt

After the build is complete, send this:

```
Please now write me a comprehensive tutorial in Markdown that is 
suitable for a complete beginner in front-end coding to walk me 
through what you've done here.

Include:
1. A summary of the technology stack used
2. A high-level walkthrough of the architecture
3. A detailed code review with code samples
4. The styling approach and how the UI works
5. The back-end API route and how it calls OpenRouter
6. How to run it locally
7. Five suggestions for how the code could be improved, based on a self-review
```

### What Gets Generated

The agent creates a `tutorial.md` file in your project containing:
- Technology stack summary (Next.js, React, TypeScript, Tailwind, etc.)
- Architecture overview
- Key code sections with explanations
- How the frontend and backend communicate
- How OpenRouter is called from the API route
- Numbered improvement suggestions

**To view it formatted:** Right-click `tutorial.md` → **Open Preview**

### How to Use the Tutorial

- **If you're a beginner:** Read it carefully. Use it to understand the structure. Ask follow-up questions to fill gaps.
- **If you're experienced:** Skim it quickly to verify the agent built things the way you'd expect.
- **Either way:** Use it as a checklist — does the code match the description?

> *"This is both the way to learn about it and a way to challenge and test your agent to make sure you're satisfied with the way it's done the work."*

---

## 17. Cross-Model Collaboration — Using Opus for Code Review

This is the **standout technique** of Day 4. Rather than having the same model review its own work, you can have a **different, more powerful model** do a code review — bringing a fresh perspective.

### The Concept

Each LLM has different strengths, different training, and different tendencies. Having one model write code and another model review it is like having two expert colleagues — their different perspectives catch different issues.

This is a foreshadowing of **multi-agent workflows** (covered in Week 3) — the same idea, but automated and running concurrently.

### The Cross-Model Code Review Prompt

In the Cursor agent panel, **switch the model** from GPT 5.2 Codex to **Claude Opus 4.5**:

```
Please do a comprehensive code review of this project and write 
the results to review.md.

Include:
- Overall code quality assessment
- Security concerns
- Performance issues
- Structural/architectural observations
- Remedial actions needed (listed as priority items)

Do NOT change any code — write the review only.
```

**Key detail:** Switch the model to Opus before sending this prompt. The same conversation context and codebase is now being reviewed by a completely different AI model.

---

### What Opus Produces

The code review in `review.md` typically includes:

- **Dependency analysis** — checking if library choices are appropriate
- **Security audit** — looking for issues like exposed API keys, injection risks
- **Performance observations** — identifying inefficient patterns
- **Structural review** — evaluating component organisation, separation of concerns
- **Prioritised remedial actions** — critical issues flagged at the top, minor suggestions at the bottom

> *"I just love Opus. We should have had Opus write the tutorial — it would have been this comprehensive."*

---

### How to Act on the Code Review

Once you have `review.md`, you have two options:

**Option A — Pass the review back to the original builder**
```
"Please read through review.md and implement all the remedial 
actions listed. If you disagree with any recommendation, explain 
why before changing it."
```

**Option B — Discuss and selectively implement**
- Read the review yourself first
- Decide which recommendations to action
- Prompt the agent to implement specific items

---

### Why This Matters Beyond the Code

This technique establishes a workflow pattern that scales to real enterprise development:

```
Builder Agent (GPT 5.2 Codex) → Creates the code
Reviewer Agent (Claude Opus)   → Reviews the code  
Builder Agent (GPT 5.2 Codex) → Implements fixes
```

In Week 3 of the course, this same pattern runs with **automated sub-agents** doing this concurrently in real time. Today's manual version is the foundation of that.

---

## 18. Day 4 Wrap-Up & What's Next

### What You Built Today

✅ A full **personal portfolio website** in Next.js, generated from your LinkedIn profile  
✅ An embedded **AI Digital Twin chatbot** that answers questions about your career  
✅ Live **OpenRouter API integration** using a `.env` file for secure key management  
✅ Used a single YOLO prompt — no agents.md, no step-by-step approval  
✅ Iterated on the output: improved chat UI, fixed navigation, improved the system prompt  
✅ Generated a **self-tutorial** — the AI explaining its own code  
✅ Performed a **cross-model code review** using Claude Opus as a second opinion  

**You are now 27% through the course! 🎉**

---

### Key Concepts Introduced Today

| Concept | Description |
|---|---|
| **Two decisions** | IDE choice vs. Model choice — model is what matters most |
| **Five principles of vibe coding** | agents.md quality, start simple, work incrementally, don't get lazy, embrace frustration |
| **Responsible YOLO** | YOLO is only safe/productive with top frontier models |
| **The .env file** | Secure storage for API keys; always listed in .gitignore |
| **OpenRouter** | Unified gateway to multiple AI providers — one account, one key |
| **Digital Twin** | An AI chatbot trained on your profile, answering as you |
| **Nuclear reset technique** | When stuck in a loop, ask the agent to rebuild from scratch |
| **Tutorial prompt** | Ask the AI to explain its own code — bridges the learning gap |
| **Cross-model collaboration** | Use different models for building and reviewing — different perspectives catch different issues |

---

### Critical Rules to Remember

```
1. Never commit .env to Git — ever
2. Smart model > fast model for YOLO
3. You own the code — "the AI wrote it" is not a defence
4. Be the boss — always demand evidence, not just assertions
5. When stuck in a loop → nuclear reset (rebuild from scratch)
6. Check your work — always test after every claim of "fixed"
```

---

### Coming Up Tomorrow — Day 5

Day 5 is the **second blue (project) day** — another commercial project, building on everything covered in Week 1.

> *"Tomorrow is another blue day as we build more projects. The first blue day was fantastic — and tomorrow's will be even better."*

---

*📝 Notes compiled from Day 4 lectures of the AI Coder Course — covering all 6 segments: YOLO Mode & LLM Choosing, Five Principles for Vibe Coding, Responsible YOLO & OpenRouter Setup, Building the Portfolio Website, Adding the AI Digital Twin, and Tutorials/Code Reviews with Cross-Model Collaboration.*
