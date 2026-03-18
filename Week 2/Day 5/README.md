# Day 5 — Pro Week: Building a Full SaaS Platform with Claude Code — Skills, claude.md & End-to-End Delivery

> **Overview:** Day 5 is the culmination of Week 2 — a full build day where everything learned across the week is applied together to ship a real SaaS product from scratch. The day covers writing a powerful global `claude.md`, creating a custom Skill for Cerebras fast inference, writing Jira tickets as proper product requirements, and then running Claude Code through four sequential feature tickets to build a complete, multi-user AI-powered legal document SaaS platform.

---

## Table of Contents

1. [Week 2 Recap — The Full Toolkit at a Glance](#1-week-2-recap--the-full-toolkit-at-a-glance)
2. [The Project — Pre-Legal SaaS Platform](#2-the-project--pre-legal-saas-platform)
3. [The Global claude.md — Your Personal AI Instruction File](#3-the-global-claudemd--your-personal-ai-instruction-file)
   - [What is the Global claude.md?](#what-is-the-global-claudemd)
   - [Where it Lives and How it Works](#where-it-lives-and-how-it-works)
   - [What to Put in Your Global claude.md](#what-to-put-in-your-global-claudemd)
   - [Example Global claude.md Content](#example-global-claudemd-content)
4. [Writing the Project claude.md](#4-writing-the-project-claudemd)
   - [The @ File Reference Trick](#the--file-reference-trick)
   - [What the Project claude.md Should Cover](#what-the-project-claudemd-should-cover)
   - [Example Project claude.md Structure](#example-project-claudemd-structure)
5. [Building a Custom Skill — The Cerebras Inference Skill](#5-building-a-custom-skill--the-cerebras-inference-skill)
   - [Why Build a Custom Skill?](#why-build-a-custom-skill)
   - [What is Cerebras and Why Use It?](#what-is-cerebras-and-why-use-it)
   - [Creating the Skill Folder Structure](#creating-the-skill-folder-structure)
   - [Writing the skill.md File](#writing-the-skillmd-file)
   - [The skill.md Metadata Format — Getting it Exactly Right](#the-skillmd-metadata-format--getting-it-exactly-right)
   - [Referencing the Skill in claude.md](#referencing-the-skill-in-claudemd)
6. [Setting Up the Environment File](#6-setting-up-the-environment-file)
7. [Writing Jira Tickets — The V1 Product Roadmap](#7-writing-jira-tickets--the-v1-product-roadmap)
   - [Good Ticket Writing Principles](#good-ticket-writing-principles)
   - [PL-4 — Build Foundation of V1 Product](#pl-4--build-foundation-of-v1-product)
   - [PL-5 — Add AI Chat Interface](#pl-5--add-ai-chat-interface)
   - [PL-6 — Expand to All Legal Document Types](#pl-6--expand-to-all-legal-document-types)
   - [PL-7 — Multiple Users and Final Polish](#pl-7--multiple-users-and-final-polish)
8. [Verifying Claude Code is Ready](#8-verifying-claude-code-is-ready)
9. [Building PL-4 — V1 Technical Foundation](#9-building-pl-4--v1-technical-foundation)
   - [The Command](#the-command)
   - [Architecture Review — A Key Human Checkpoint](#architecture-review--a-key-human-checkpoint)
   - [What Claude Built](#what-claude-built)
   - [After PL-4 — Context Management Before Next Ticket](#after-pl-4--context-management-before-next-ticket)
10. [Building PL-5 — AI Chat Interface with Cerebras](#10-building-pl-5--ai-chat-interface-with-cerebras)
    - [The Command](#the-command-1)
    - [Clarifying Questions from Feature Dev](#clarifying-questions-from-feature-dev)
    - [The Architecture Debate — Streaming vs Structured Output](#the-architecture-debate--streaming-vs-structured-output)
    - [Verifying the Skill Was Used Correctly](#verifying-the-skill-was-used-correctly)
    - [Testing PL-5 — The AI Chat Demo](#testing-pl-5--the-ai-chat-demo)
    - [Observed Issues (Feedback for Next Ticket)](#observed-issues-feedback-for-next-ticket)
11. [Building PL-6 — All Legal Document Types + Fixes](#11-building-pl-6--all-legal-document-types--fixes)
    - [The Command with Inline Fixes](#the-command-with-inline-fixes)
    - [Testing PL-6 — Cloud SaaS Agreement Demo](#testing-pl-6--cloud-saas-agreement-demo)
    - [The PR — What Was Built](#the-pr--what-was-built)
12. [Building PL-7 — Multi-User Auth and Final Polish](#12-building-pl-7--multi-user-auth-and-final-polish)
    - [The Command](#the-command-2)
    - [Testing PL-7 — The Full SaaS Demo](#testing-pl-7--the-full-saas-demo)
    - [Freemium Pattern — An Unasked-For Bonus](#freemium-pattern--an-unasked-for-bonus)
    - [What Was Missing — Honest Critique](#what-was-missing--honest-critique)
13. [Session Rhythm — The Context Management Loop](#13-session-rhythm--the-context-management-loop)
14. [The Complete Architecture of What Was Built](#14-the-complete-architecture-of-what-was-built)
15. [Final PR Merge and Project Closure](#15-final-pr-merge-and-project-closure)
16. [Week 2 Summary — What You've Learned to Do](#16-week-2-summary--what-youve-learned-to-do)
17. [Key Takeaways — Day 5 Principles](#17-key-takeaways--day-5-principles)

---

## 1. Week 2 Recap — The Full Toolkit at a Glance

Before the build begins, here is the complete picture of everything assembled through the week:

| Tool | What it Does | Pro | Con |
|---|---|---|---|
| **MCP** | Connects Claude Code to external tool processes via an open standard. | Enormous ecosystem; flexible; real-time data. | Can consume context window; complex; auth can be unreliable. |
| **Skills** | Markdown files that give Claude Code expertise via progressive disclosure. | Context-efficient; simple to build and share via Git. | Less powerful; less mature ecosystem. |
| **Plugins** | Bundles of MCP, skills, commands, and agents installed in one step. | Simplest to use; best of both. | Claude Code only; too many can degrade performance. |
| **Feature Dev Plugin** | Guides Claude Code through a 7-step disciplined development process. | Structured, asks clarifying questions, quality review built in. | Can skip steps; still needs human oversight. |
| **Atlassian MCP** | Reads and updates Jira issues. | Full Jira integration from inside Claude Code. | Loses authentication frequently — must re-authenticate often. |
| **GitHub MCP** | Creates commits, PRs, and merges on GitHub. | Complete git workflow from inside Claude Code. | Fine-grained token limits may block some operations (e.g., API merge). |

**The workflow from Day 4 in one line:**

```
Read Jira issue (Atlassian MCP) → Feature Dev 7-step process → Code → PR (GitHub MCP)
```

Triggered by a single command:
```
/feature-dev:feature-dev Please implement Jira issue PL-3 with a Next.js 
application in a directory called frontend. Then raise a PR when done.
```

---

## 2. The Project — Pre-Legal SaaS Platform

**Pre-Legal** is the SaaS product being built throughout Day 5. It is a platform for drafting legal agreements based on templates, powered by an AI chat interface.

**Core concept:**
- A user has a conversation with an AI.
- The AI asks questions to determine what legal document they need and gathers the specific field values (party names, dates, governing law, etc.).
- The platform fills in a legal document template with those values.
- The user can download the completed document as a PDF.
- Users can create accounts, save documents, and access prior documents.

**Why this is a good learning project:**
- It uses AI in a genuinely useful, commercially viable way.
- It has a clear data layer (templates), a backend API, and a frontend UI.
- It is complex enough to be realistic but well-contained enough to build in a single day.
- It demonstrates the entire lifecycle: data curation → prototype → V1 backend → AI chat → multi-user auth.

**The template data source:** Common Paper GitHub repository — legal document templates (mutual NDA, cloud SaaS agreement, pilot agreement, etc.) licensed under Creative Commons, meaning they can be freely used and modified.

---

## 3. The Global claude.md — Your Personal AI Instruction File

### What is the Global claude.md?

Most developers know about the `claude.md` file inside a project repository — it gives Claude project-specific context. But there is also a **global `claude.md`** that lives in your home directory, completely independent of any project.

This global file applies to **every single Claude Code session you ever start**, across all projects. It is your personal preferences and non-negotiables, expressed to Claude once and applied everywhere.

---

### Where it Lives and How it Works

| File | Location | Scope |
|---|---|---|
| **Global claude.md** | `~/.claude/claude.md` (your home directory) | Applies to ALL projects and sessions. |
| **Project claude.md** | `<project>/.claude.md` or `<project>/claude.md` | Applies only to that specific project. |

Both files are read by Claude Code at startup. Project-level instructions can build on, override, or add specificity to the global ones.

---

### What to Put in Your Global claude.md

The global `claude.md` should be **short, high-value, and personal**. Every token in this file is loaded into every context window you ever open, so make every word count.

**Good things to put in the global file:**
- Your coding style preferences (e.g., keep modules short, prefer clear variable names).
- Non-negotiables that consistently get ignored without reminders (e.g., no emojis in code, keep READMEs concise).
- Your preferred tools and package managers (e.g., always use `uv` instead of `pip`).
- Debugging philosophy (e.g., always find root cause, never apply workarounds).
- Short reminders you want repeated (repetition is okay here — if you really want something remembered, say it twice).

**What NOT to put in the global file:**
- Project-specific context (that goes in the project `claude.md`).
- Very long documents or reference material (use `@file-reference` for that).
- Boilerplate that Anthropic has already built into Opus by default.

> *"The key is to keep this super short and concise and make every word count, because every token counts — this goes in every single context that you ever have."*

---

### Example Global claude.md Content

```markdown
## Very Important
Be simple. Approach tasks in a simple incremental way.
Work incrementally — always small, simple steps.
Validate and check each increment before moving on.
Use latest APIs as of now.

## Mandatory Code Style
Do not overengineer.
Do not program defensively.
Use UV as the Python package manager.
  - Always `uv run`, never `python3`.
  - Always `uv add`, never `pip install`.
Favor clear concise docstring comments.
Be sparing with comments outside docstrings.
Favor short modules.
Never use emojis in code, print statements, or logging.
Keep README concise.
Clean up old files when no longer needed.

## Debugging (Important)
Always identify root cause before fixing.
Prove the problem first — don't guess.
Reproduce consistently.
One test at a time — be methodical.
Do not jump to conclusions.
Do not apply workarounds.
```

---

## 4. Writing the Project claude.md

The project-level `claude.md` is where you give Claude Code specific context about *this* project — the product, the architecture, the AI design decisions, and the development process to follow.

### The @ File Reference Trick

Claude.md supports `@filename` syntax to **dynamically include the contents of another file**. This is extremely useful for keeping the `claude.md` lean while ensuring Claude always has access to important reference data.

**Example:**
```markdown
The available documents are covered in catalog.json. 
Included here: @catalog.json
```

When Claude reads `claude.md`, it also reads the full contents of `catalog.json` at that point. This means you can maintain a separate data file and simply reference it — no copying needed.

**Other uses of `@` syntax:**
- `@docs/plan.md` — include a detailed plan file.
- `@agents.md` — point `claude.md` entirely to `agents.md` (single source of truth trick from Day 2).
- `@src/` — include a directory listing (not file contents, just names).

> **Caution:** The `@` reference inserts the entire file into context at startup. Only use it for files that are truly necessary every session and are not too long.

---

### What the Project claude.md Should Cover

A well-written project `claude.md` for a SaaS build should cover:

| Section | What to Include |
|---|---|
| **Project overview** | What the product is, who it is for, what it does. |
| **Current implementation status** | What has been built already, what state the project is in. |
| **Development process** | Remind it to use Jira tools, not skip steps, test thoroughly, submit PRs. |
| **AI design** | Which model to use, which skill to use, how to structure LLM calls. |
| **Technical design** | Backend framework, frontend framework, database, Docker setup, directory structure. |
| **Scripts** | How to start and stop the server. |
| **Style/branding** | Color scheme, UI guidelines if relevant. |

---

### Example Project claude.md Structure

```markdown
# Pre-Legal Project

## Overview
This is a SaaS product to allow users to draft legal agreements based on 
templates in the /templates directory. The user engages in a chat to 
establish what document they want and how to fill in the fields.

The available documents are covered in catalog.json:
@catalog.json

The initial implementation is a frontend-only prototype.

## Development Process
- Use your Atlassian tools to read feature instructions from Jira.
- Develop the feature — do not skip any steps.
- Thoroughly test with unit and integration tests.
- Fix any issues found during testing.
- Submit a PR using your GitHub tools.

## AI Design
When writing code that makes calls to LLMs:
- Use your cerebras skill.
- Use the `openai/gpt-4o-mini` model via OpenRouter.
- Use structured outputs so you can interpret results and populate 
  fields in the legal document.

## Technical Design
- Package everything into a Docker container.
- Backend: `backend/` — UV project using FastAPI.
- Frontend: `frontend/` — Next.js static export.
- Database: SQLite, created fresh each time the Docker container starts.
  Allows for a users table with sign-up and sign-in.
- Scripts:
  - Start: `scripts/start-mac.sh` (or `start-windows.sh`)
  - Stop:  `scripts/stop-mac.sh` (or `stop-windows.sh`)

## Color Scheme
Primary: #2D3748  
Accent: #4299E1  
Background: #F7FAFC
```

---

## 5. Building a Custom Skill — The Cerebras Inference Skill

### Why Build a Custom Skill?

Throughout the build, all LLM calls need to go through a very specific provider setup:
- **Model:** GPT-OSS 120B (open-source, extremely capable).
- **Router:** OpenRouter (as used throughout the course).
- **Inference provider:** Cerebras.

Cerebras is a specialized AI chip company that runs inference on their own silicon. When you route a request to Cerebras through OpenRouter, the response comes back **dramatically faster** than other providers — essentially instant for typical document question-and-answer exchanges. No streaming is needed because the full response arrives in one chunk almost immediately.

A Skill is the perfect way to encode this pattern because:
- It can include code snippets showing exactly how to make the API call.
- It uses progressive disclosure — it does not load the full code examples into context until Claude actually needs to make an LLM call.
- It can be committed to the repo so every team member automatically has it.
- It gives Claude a precise, project-specific pattern to follow, rather than letting it guess.

---

### What is Cerebras and Why Use It?

**Cerebras** is an AI hardware company that builds custom silicon (chips) specifically for AI inference. When you route requests through OpenRouter and specify Cerebras as the provider, you get:

- **Extremely fast response times** — entire responses arrive almost instantly.
- **No need for streaming** — the whole response comes as one chunk so fast that streaming adds complexity with no UX benefit.
- **Slightly higher cost** than standard providers — but still cheap in absolute terms for small API calls.

For a legal document application where users need immediate feedback as they fill in fields via chat, Cerebras makes the experience feel native and snappy rather than like waiting for an AI.

---

### Creating the Skill Folder Structure

Navigate to the project's `.claude` folder and create the skills structure:

```
<project>/
└── .claude/
    └── skills/
        └── cerebras/           ← Skill name folder
            └── skill.md        ← The skill file
```

**Steps:**
1. In VS Code Explorer, find the `.claude` folder in your project.
2. Create a new folder inside `.claude` called `skills`.
3. Inside `skills`, create a new folder called `cerebras`.
4. Inside `cerebras`, create a new file called `skill.md`.

---

### Writing the skill.md File

The `skill.md` file has two parts:
1. **YAML front matter** (metadata) — always loaded into context.
2. **Markdown instructions** — loaded only when Claude decides the skill is needed.

**Metadata block (YAML front matter):**

```markdown
---
name: cerebras
description: Use this to write code to call an LLM using LiteLLM and 
  OpenRouter with the Cerebras inference provider.
---
```

**Instructions body (everything below the `---`):**

```markdown
# Calling an LLM via Cerebras

These instructions allow you to write code to call an LLM with Cerebras 
specified as the inference provider.

## Setup

Install LiteLLM:
```bash
uv add litellm python-dotenv
```

Load your API key from `.env`:
```python
import os
from dotenv import load_dotenv
load_dotenv()
OPENROUTER_API_KEY = os.getenv("OPENROUTER_API_KEY")
```

## Code to Call Cerebras (Standard)

```python
import litellm

response = litellm.completion(
    model="openrouter/openai/gpt-4o-mini",
    messages=[{"role": "user", "content": prompt}],
    api_key=OPENROUTER_API_KEY,
    extra_body={
        "provider": {
            "order": ["Cerebras"],
            "allow_fallbacks": False
        }
    }
)
result = response.choices[0].message.content
```

## Code to Call Cerebras (Structured Outputs)

```python
from pydantic import BaseModel

class DocumentFields(BaseModel):
    party_name: str
    effective_date: str
    governing_law: str
    # ... other fields

response = litellm.completion(
    model="openrouter/openai/gpt-4o-mini",
    messages=[{"role": "user", "content": prompt}],
    api_key=OPENROUTER_API_KEY,
    response_format=DocumentFields,
    extra_body={
        "provider": {
            "order": ["Cerebras"],
            "allow_fallbacks": False
        }
    }
)
fields = DocumentFields.parse_raw(response.choices[0].message.content)
```
```

> **Critical:** The `extra_body` parameter specifying `"provider": {"order": ["Cerebras"]}` is what routes the request specifically through Cerebras. Without this, OpenRouter will use whatever provider it selects by default.

---

### The skill.md Metadata Format — Getting it Exactly Right

The YAML front matter at the top of `skill.md` must follow an **exact format**. If the format is wrong, the skill will not be recognised.

```
---                           ← Three hyphens, nothing else on this line
name: cerebras               ← Must be "name:", then the skill name
description: <description>   ← Must be "description:", then the description
---                           ← Three hyphens to close, nothing else on this line
```

**Common mistakes to avoid:**
- Extra spaces before `name:` or `description:`.
- Using different quote styles.
- Not closing with `---`.
- Putting anything else in the front matter block.

> *"It's a bit like API keys — you've got to get this format right. If you get it wrong, it won't work."*

---

### Referencing the Skill in claude.md

Once the skill exists, reference it explicitly in your project `claude.md` so Claude always knows to use it for LLM calls:

```markdown
## AI Design
When writing code to make calls to LLMs, use your cerebras skill.
Use LiteLLM via OpenRouter with the `openai/gpt-4o-mini` model.
Use Cerebras as the inference provider.
Use structured outputs so you can interpret results and populate fields 
in the legal document.
```

The phrase **"use your cerebras skill"** is the key instruction — it ensures Claude loads the skill when designing any LLM integration code.

---

## 6. Setting Up the Environment File

The project needs a `.env` file with the OpenRouter API key for Cerebras to work.

**Copy from an existing project:**

```bash
cp ../pm/.env .env
```

**Or create it manually:**

```
OPENROUTER_API_KEY=sk-or-your-key-here
```

**Verify the file:**
- Do NOT open it in a word processor (curly quotes will break it).
- Confirm the variable name matches exactly what the code expects.
- Confirm `.env` is in your `.gitignore` (it should be — Claude added it in Day 4).

**Reference it in claude.md** to make sure Claude always knows it exists:

```markdown
There is an OpenRouter API key in the .env file in the project root.
```

---

## 7. Writing Jira Tickets — The V1 Product Roadmap

The four Jira tickets created for Day 5 represent the **V1 product roadmap** — taking the application from a frontend-only prototype to a full, multi-user SaaS product.

### Good Ticket Writing Principles

Before looking at the specific tickets, here is what makes a good ticket for Claude Code to implement:

| Principle | Why it Matters |
|---|---|
| **Write in business/product language** | Claude is excellent at translating high-level requirements. Technical details constrain it unnecessarily. |
| **Be intentionally vague about implementation details** | Feature Dev will ask clarifying questions — leave room for that dialogue. |
| **Be clear about what NOT to do yet** | Explicitly saying "no authentication yet" or "placeholder only" prevents scope creep. |
| **Reference the relevant data files** | If the ticket needs existing data, name the files (e.g., "use the templates in `/templates`"). |
| **Include acceptance criteria** | What does "done" look like? Even one clear sentence helps enormously. |

---

### PL-4 — Build Foundation of V1 Product

**Title:** Build foundation of V1 product

**Description:**
```
Upgrade the prototype so that it has the proper technical foundation for 
the full V1 project, including frontend, backend, and temporary database 
with scripts to start and stop — but without updating the functionality yet.

For the frontend/backend interaction, keep the current NDA form functionality 
client-side.

For authentication: placeholder routes only — fake login screen, no real 
authentication. Just bring the user into the platform.
```

**What this ticket accomplishes:** Converts the Next.js frontend-only prototype into a proper full-stack architecture (FastAPI backend + Next.js frontend + SQLite database) inside a Docker container — without changing any user-facing functionality.

---

### PL-5 — Add AI Chat Interface

**Title:** Add AI chat, but still just mutual NDA

**Description:**
```
Change the way the platform interacts with a user. Instead of a series 
of questions (form), this should be a free-form chat with an AI.

The AI asks about the document, asks questions related to the fields, 
and populates the document based on the responses.
```

**Intentional vagueness:** The download format, chat vs form coexistence, and how conversation ends are all left open for Feature Dev's clarifying questions.

---

### PL-6 — Expand to All Legal Document Types

**Title:** Expand to all supported legal document types

**Description:**
```
Now expand the functionality so it supports all legal document types for 
which we have templates.

If the user asks for an unsupported document type, engage with them — 
explain we can't generate that, but offer the closest document we can generate.
```

---

### PL-7 — Multiple Users and Final Polish

**Title:** Support multiple users and final polish

**Description:**
```
Add a proper sign-in and sign-up screen. Let a user register and come back 
into the platform.

Store previously generated documents. Allow the user to look back at prior 
documents they have created.

The database can be temporary and reset every time the server restarts.

Add polish to all screens so they look like a professional SaaS application.

Add a disclaimer that the documents should be considered draft and subject 
to legal review.
```

---

## 8. Verifying Claude Code is Ready

Before starting the build, run these checks inside Claude Code:

### Check 1 — Verify the Cerebras Skill is Loaded

```
/context
```

In the context display, you should see: **"cerebras — project skill"** listed under skills. This confirms the skill was detected and its metadata is in context. It should use a very small number of tokens (just the metadata, not the full instructions).

### Check 2 — Verify MCP Servers and Plugins

The context display should also show:
- Atlassian MCP tools (from the Atlassian MCP server).
- GitHub MCP tools (from the GitHub MCP server).
- Feature Dev plugin.
- Any other installed plugins (Frontend Design, Code Simplifier, etc.).

### Check 3 — Re-authenticate Atlassian

Always do this before starting a new build session:

```
/mcp
```

Select `atlassian` → press Enter → select **Re-authenticate** → browser opens → Approve → Accept → return to Claude Code.

This prevents the silent hang that happens when the Atlassian auth token has expired.

---

## 9. Building PL-4 — V1 Technical Foundation

### The Command

```
/feature-dev:feature-dev Implement Jira ticket PL4 and make a PR.
```

---

### Architecture Review — A Key Human Checkpoint

Feature Dev's seven-step process includes an architecture design phase that **pauses and presents the proposed architecture for your review**. This is one of the most important moments in the entire workflow.

For PL-4, the proposed architecture was:

| Component | Decision | Reason |
|---|---|---|
| **Frontend** | Next.js static export | Standard, compatible with Docker. |
| **Backend** | FastAPI with UV | Fast, async, Python — matches project spec. |
| **Database** | SQLite | Simple, temporary, no external service needed. |
| **Authentication** | Placeholder routes only | Per ticket spec — no real auth yet. |
| **Containerisation** | Single Docker container, multi-stage build | Clean, portable, matches `claude.md` spec. |
| **Package config** | `pyproject.toml` (UV project) | Better than `requirements.txt` — proper dependency management. |

**What to do during the architecture review:**
- Read every decision point.
- Verify each matches what you specified in `claude.md` and the Jira ticket.
- Challenge anything that seems off.
- If you are not technical, ask Claude to explain any decision you don't understand — this is the right time to probe.

> *"Even if you're not from a technical background, you need to be the boss — be like the inquisitive manager that asks probing questions. This is your opportunity to challenge."*

After reviewing, press **1** (Yes, proceed) to start implementation.

---

### What Claude Built

- A `backend/` FastAPI application with proper UV project structure (`pyproject.toml`).
- A `frontend/` Next.js application (unchanged functionality from prototype).
- A `docker-compose.yml` and `Dockerfile` with multi-stage build.
- `scripts/start-mac.sh`, `scripts/stop-mac.sh`, `scripts/start-windows.sh`, `scripts/stop-windows.sh`.
- SQLite database setup with placeholder routes for future auth.
- 76 tests written and passing.
- Pull Request raised on GitHub.

**Testing manually:**

```bash
scripts/start-mac.sh
# → Server running at localhost:8000
```

The app looked identical to the prototype (correct — no functionality change was asked for), but was now running through the full FastAPI + Docker stack. PDF download still worked correctly.

---

### After PL-4 — Context Management Before Next Ticket

After a major ticket is complete, the context window is typically quite full. Before starting the next ticket:

**Step 1 — Update claude.md with current status**

```
Please update claude.md with concise details on what has been implemented.
Correct anything that is no longer accurate.
```

This ensures that after a `/clear`, Claude still knows what has been done and what state the project is in.

**Step 2 — Review the updated claude.md**

Open the file in VS Code (right-click → Open Preview) and verify:
- The overview still accurately describes the product.
- The development progress section reflects what was just built.
- The AI design section still references the Cerebras skill correctly.
- Nothing critical has been inadvertently removed or garbled.

**Step 3 — `/clear` the context**

```
/clear
```

This wipes the conversation history completely — starting fresh. Claude re-reads `claude.md` (which now contains updated status), so it has good context for the next ticket without carrying the accumulated weight of the last conversation.

**Step 4 — Re-authenticate Atlassian**

```
/mcp → atlassian → Re-authenticate
```

Do this every single time after a `/clear` or a session restart.

> **Why `/clear` instead of `/compact`?** Compaction tries to summarise the conversation but can selectively lose important information in the process. A clean `/clear` combined with a well-maintained `claude.md` is more reliable. The key is keeping `claude.md` up to date so that the "cold start" has all the information Claude needs.

---

## 10. Building PL-5 — AI Chat Interface with Cerebras

### The Command

```
/feature-dev:feature-dev Implement Jira ticket PL5 and make a PR.
```

---

### Clarifying Questions from Feature Dev

Feature Dev asked four key clarifying questions for PL-5:

| Question | Options | Choice | Reasoning |
|---|---|---|---|
| Should the chat UI completely replace the form or coexist with it? | (1) Replace form, (2) Coexist (switch between) | **1 — Replace** | A chat interface is the new paradigm; keeping the old form adds unnecessary complexity. |
| Should document preview update live or only after conversation ends? | (1) Live updates, (2) After conversation | **1 — Live updates** | Better UX — user sees the document forming in real time. |
| How should the AI conversation begin? | (1) AI greets and asks first question, (2) User initiates | **1 — AI greets first** | More natural, guided experience. |
| When all required fields are filled in, what should happen? | (1) AI confirms and shows download, (2) AI keeps asking | **1 — AI confirms and shows download** | Clear completion signal; avoids infinite loops. |

These are exactly the kinds of questions that would typically be answered by a product owner or UX designer. Feature Dev surfaces them upfront — before any code is written.

---

### The Architecture Debate — Streaming vs Structured Output

Feature Dev launched **three parallel architecture agents** for PL-5 and presented the options:

| Option | Description | Trade-offs |
|---|---|---|
| **Minimal** | Replace the NDA form with a chat interface; reuse everything else; stateless backend. | Simplest, lowest risk. |
| **Clean** | Full session management, database persistence, SSE streaming. | Richer but over-engineered for this use case. |
| **Pragmatic** | Streaming responses + parallel field extraction; stateless backend; clean separation. | Good balance — but includes streaming. |

**The decision and the reasoning:**

The correct choice for this project is **Minimal with structured outputs** — not any of the three options as presented. The key insight was:

> *"I don't particularly think we need streaming because we're using Cerebras, which is so fast that streaming is not going to be required. I'd rather we just have the structured extraction. One LLM call with structured outputs — including the response text AND the field data — is cleaner."*

**Why streaming is unnecessary with Cerebras:**
- Streaming is typically used to give users visual feedback while waiting for a slow response.
- Cerebras returns complete responses essentially instantly — the entire response arrives as one chunk.
- Streaming adds code complexity (SSE connections, chunked parsing) with zero UX benefit.
- A single structured output call returns both the conversational response AND the extracted field values simultaneously, which is cleaner architecturally.

**This is a great example of the human staying in the loop.** Feature Dev proposed reasonable options, but the developer's knowledge of Cerebras's speed characteristics led to a better architectural decision than any of the pre-generated options.

To make this choice, the developer typed a message in the architecture chat:

```
I'd like the simple backend — the pragmatic choice — except I only want one 
LLM call and no streaming because Cerebras is so fast that streaming isn't 
necessary. One LLM call with structured outputs — including both the response 
text and the extracted fields — is cleaner.
```

Feature Dev accepted this feedback and updated its implementation plan accordingly.

---

### Verifying the Skill Was Used Correctly

After implementation, check the Pull Request diff to confirm the Cerebras skill was followed correctly. Specifically, look for:

1. The `extra_body` parameter in LLM calls — this is the Cerebras provider routing instruction that was in the skill's code snippet:

```python
extra_body={
    "provider": {
        "order": ["Cerebras"],
        "allow_fallbacks": False
    }
}
```

2. The correct model string: `openrouter/openai/gpt-4o-mini` (or whatever model was specified in the skill).

3. Pydantic structured output objects for parsing field values from the LLM response.

If these are present, the skill was correctly applied. The fact that Claude extracted the exact `extra_body` pattern from the skill demonstrates that the skill's progressive disclosure mechanism worked — Claude loaded the code examples when it needed to write the LLM integration.

---

### Testing PL-5 — The AI Chat Demo

**Start the server:**
```bash
scripts/start-mac.sh
```

**Open:** `localhost:8000`

**The conversation flow (demo):**

| Turn | User Says | What Happens |
|---|---|---|
| - | App loads | AI greets: *"I'll help you create a mutual non-disclosure agreement. Let's start with the basics — what's the purpose?"* |
| 1 | "I'm evaluating a business relationship." | AI: *"When would you like the effective date?"* — Document preview starts updating. |
| 2 | "Today." | AI: *"How long should the agreement last?"* |
| 3 | "Three years." | Fields fill in on the right side of the screen in real time. |
| 4 | "Two years confidentiality period." | More fields fill in. |
| 5 | "New York." | AI: *"Perfect. I have what I need."* — **Download PDF** button appears. |

**Key observations:**
- The response speed is remarkable — essentially instant, no loading indicator needed.
- The document on the right updates live with each exchange.
- The PDF downloads correctly when clicked.

---

### Observed Issues (Feedback for Next Ticket)

After testing, two issues were identified to fix in PL-6:

1. **The UI focus does not return to the text input field** after submitting a message. The user has to click back to type their next message — jarring UX.
2. **The AI sometimes stops asking questions** mid-conversation rather than always asking the next question. The conversation can stall awkwardly.

These were noted and added to the PL-6 command as inline fixes.

---

## 11. Building PL-6 — All Legal Document Types + Fixes

### The Command with Inline Fixes

This illustrates an important pattern: you can combine a Jira ticket implementation with **specific fixes or enhancements** in the same command:

```
Implement Jira ticket PL6. Also please make a couple of fixes:
1. Ensure that after answering a question, the UI focus goes back 
   to the text input field.
2. Ensure that the AI always asks a follow-on question if it needs 
   more information.

When PL6 is done and these enhancements are done, please test and 
then make a PR.
```

This is efficient — rather than raising a separate ticket for each small fix, you can bundle related work together into a single Feature Dev run.

---

### Testing PL-6 — Cloud SaaS Agreement Demo

After PL-6 was implemented, the app now supports all document types from the templates catalog. Testing with a **Cloud SaaS Agreement** (a more complex document than an NDA):

**The conversation flow:**

| Turn | User Says | Observed Behaviour |
|---|---|---|
| - | App loads | AI: *"Hello, I'll help you create a legal agreement. What type of document do you need?"* |
| 1 | "A cloud SaaS agreement." | AI: *"Great, a Cloud Service Agreement. Let's start. What's the name of the provider company?"* |
| 2 | Placeholder company names | AI asks about start date. |
| 3 | "Today." | AI asks about governing state. |
| 4 | "New York." | *Document preview updates with "New York" in real time.* |
| 5 | (Subscription, support, pricing...) | AI keeps asking relevant questions. |
| 6 | "$10,000 per annum, invoice net 30." | AI: *"Thanks for the details. That all seems good."* — **Download PDF** appears. |

**Results:**
- ✅ Correct brand colors displayed.
- ✅ AI always asks follow-on questions (fix confirmed working).
- ✅ UI focus returns to text input after each message (fix confirmed working).
- ✅ Document preview updates live as fields are filled.
- ✅ PDF downloads successfully with correct content.

---

### The PR — What Was Built

The PL-6 Pull Request contained:
- **16 files changed**
- **~2,500 lines of code added**
- Support for all legal document types from the template catalog.
- Dynamic document type detection from user's opening message.
- Graceful handling of unsupported document requests (suggests closest available).
- The two UX fixes from the inline enhancement requests.
- Quality improvements from Feature Dev's built-in review phase.

---

## 12. Building PL-7 — Multi-User Auth and Final Polish

### The Command

After a `/clear` and Atlassian re-authentication:

```
/feature-dev:feature-dev Implement Jira ticket PL7, then test and 
submit a PR.
```

---

### Testing PL-7 — The Full SaaS Demo

After PL-7 was implemented and the server restarted:

**Open:** `localhost:8000`

**What appeared:** A professional landing screen offering both a sign-in option and the ability to use the app without logging in (a freemium pattern — see below).

**Creating an account:**
1. Click sign-up.
2. Enter email and password.
3. Submit → lands in the main platform interface.
4. User's email shown in the top corner with a **Sign Out** button.

**Creating and saving a document:**
1. Start a pilot agreement conversation through the AI chat.
2. Fill in all fields through the conversation.
3. Click **Save Document** — document is saved to the database.
4. Click **New Document** — returns to a blank chat.

**Verifying persistence (sign out and back in):**
1. Click **Sign Out**.
2. Click **Sign In** → enter credentials.
3. Click **My Documents**.
4. The previously saved pilot agreement appears.
5. Click **Open** — the document is fully restored.

**The full demo confirmed:**
- ✅ Sign-up and sign-in working.
- ✅ Session persistence — user stays logged in.
- ✅ Document saved to database.
- ✅ Document retrieved after logout and re-login.
- ✅ Professional polished UI throughout.
- ✅ Brand colors applied consistently.

---

### Freemium Pattern — An Unasked-For Bonus

Claude implemented something that was not in the Jira ticket: **a "freemium" or product-led growth (PLG) pattern**. The app allows users to:
- Use the document creation feature **without signing in**.
- Optionally sign up to save their documents and access previous ones.

This is a very common pattern in successful SaaS products — let users experience value before requiring commitment. Claude implemented it entirely on its own initiative.

> *"It's very clever. I guess it is a good, it's the freemium pattern that is very common — product-led growth (PLG). But it didn't ask me that question. It just did it, and I love it."*

This is an example of how powerful models like Opus 4.5 can now make sensible product decisions autonomously — not just implementation decisions.

---

### What Was Missing — Honest Critique

Even with Feature Dev's quality review, one item from the PL-7 ticket was missed:

> **Missing:** The legal disclaimer — *"documents should be considered draft and subject to legal review"* — was not visible anywhere in the UI.

This was explicitly in the Jira ticket description.

**Lesson:** Even with a seven-step process including a quality review phase, Claude is not perfect. The human must always do a final pass to check all acceptance criteria from the original ticket were met.

**How to fix it:**
```
Please add a disclaimer notice visible in the UI that states: 
"Documents generated by Pre-Legal are draft documents subject to 
legal review. Do not rely on them as final legal agreements."
Ensure this is visible on the document creation screen.
```

---

## 13. Session Rhythm — The Context Management Loop

Building four sequential tickets in a day requires a disciplined **session rhythm** — a repeatable pattern that keeps context clean between each ticket. Here is the complete loop used on Day 5:

```
┌─────────────────────────────────────────────────────┐
│  START OF EACH TICKET SESSION                       │
├─────────────────────────────────────────────────────┤
│  1. /context          ← Check context is clean      │
│  2. /mcp → atlassian  ← Re-authenticate Jira        │
│  3. Run the ticket command                          │
│  4. Answer Feature Dev clarifying questions         │
│  5. Review architecture proposal                    │
│  6. Monitor implementation                          │
│  7. Test the result manually                        │
│  8. Verify PR on GitHub                             │
│  9. Merge PR (or ask Claude to merge)               │
│ 10. Update claude.md with current status            │
│ 11. /context          ← Check how full context is   │
│ 12. /clear            ← Reset for next ticket       │
└─────────────────────────────────────────────────────┘
         ↓
    NEXT TICKET
```

**Why this rhythm matters:**
- **Re-authenticating Atlassian before every ticket** prevents silent hangs.
- **Updating claude.md before `/clear`** ensures the cold-start after clearing has all the right context.
- **Manual `/clear` instead of waiting for auto-compact** gives predictable, consistent behaviour.
- **Testing after every ticket** catches problems while the context is still warm.

---

## 14. The Complete Architecture of What Was Built

By the end of Day 5, Pre-Legal is a complete SaaS application with the following architecture:

```
┌─────────────────────────────────────────────┐
│               Docker Container              │
│                                             │
│  ┌────────────────┐  ┌─────────────────┐   │
│  │   Frontend     │  │    Backend      │   │
│  │  (Next.js)     │  │  (FastAPI/UV)   │   │
│  │                │  │                 │   │
│  │  - Chat UI     │  │  - /api/chat    │   │
│  │  - Live doc    │  │  - /api/docs    │   │
│  │    preview     │  │  - /api/users   │   │
│  │  - PDF export  │  │  - /api/auth    │   │
│  │  - My docs     │  │                 │   │
│  └───────┬────────┘  └────────┬────────┘   │
│          │                    │             │
│          └──────────┬─────────┘             │
│                     │                       │
│              ┌──────▼──────┐               │
│              │   SQLite    │               │
│              │  Database   │               │
│              │  - users    │               │
│              │  - documents│               │
│              └─────────────┘               │
└─────────────────────────────────────────────┘
                     │
         ┌───────────▼───────────┐
         │      OpenRouter       │
         │   (Cerebras provider) │
         │   GPT-OSS 120B model  │
         └───────────────────────┘
                     │
         ┌───────────▼───────────┐
         │   Legal Templates     │
         │   /templates/*.md     │
         │   catalog.json        │
         └───────────────────────┘
```

**Key technical stack:**
- **Frontend:** Next.js with Tailwind CSS.
- **Backend:** FastAPI, Python, UV package manager.
- **Database:** SQLite (temporary, resets on container restart).
- **AI:** LiteLLM → OpenRouter → Cerebras → GPT-OSS 120B.
- **LLM pattern:** Single structured output call returning both conversation reply and field values simultaneously.
- **Document generation:** Markdown templates filled with Pydantic-validated field values → converted to PDF.
- **Auth:** Email/password sign-up and sign-in with session management.
- **Container:** Docker multi-stage build.

---

## 15. Final PR Merge and Project Closure

After PL-7 testing:

```
Please merge the PR locally and then push and then switch the 
branch to main.
```

After merging:

```
Please update claude.md with the latest project status.
```

Then check the GitHub repository — the final PR shows:
- **22 files changed**
- **~1,500 lines of code added**
- Multi-user authentication, document persistence, and UI polish.

---

## 16. Week 2 Summary — What You've Learned to Do

By completing Day 5 and the full Week 2, you have learned to:

| Skill | Where Learned |
|---|---|
| Use Claude Code's CLI with full professional features | Day 1 |
| Manage sessions, checkpoints, and Git in a coherent workflow | Day 2 |
| Use YOLO mode and Ralph Loops for autonomous coding | Day 2 |
| Understand MCP, Skills, and Plugins conceptually | Day 3 |
| Install and use MCP servers (Atlassian, GitHub, Context7, Polygon) | Day 3 |
| Install and use Skills (Agent Browser, custom Cerebras skill) | Day 3, Day 5 |
| Install and use Plugins (Feature Dev, Code Simplifier, Frontend Design) | Day 3 |
| Connect Claude Code to Jira for end-to-end ticket-to-PR workflow | Day 4 |
| Use Feature Dev's 7-step process to build features with discipline | Day 4, Day 5 |
| Debug systematically with the 5-step debug process | Day 4 |
| Write a global `claude.md` that applies to all projects | Day 5 |
| Write a project `claude.md` with `@` file references | Day 5 |
| Build a custom Skill with YAML front matter and code examples | Day 5 |
| Run four sequential feature tickets to completion in a single session | Day 5 |
| Apply the session rhythm (context → auth → build → test → clear) | Day 5 |

---

## 17. Key Takeaways — Day 5 Principles

### The Global claude.md

Every developer should have one. Keep it short, personal, and opinionated. Every token counts — this file is loaded into every context you ever open. Put your non-negotiables in here (no emojis, always UV, always identify root cause before fixing).

### Skills Are Your Most Powerful Team Tool

A custom Skill committed to the repo is the most efficient way to share expertise across a team. One file, checked into Git, means every developer and every session automatically follows the same pattern — in this case, always using Cerebras for fast inference with the correct `extra_body` routing.

### Jira Tickets Are Your Spec

Write tickets in business language, not technical language. Be intentionally vague about implementation details where you want Feature Dev to ask clarifying questions. Be explicit about what NOT to build yet. Good tickets produce good features.

### The Session Rhythm is Non-Negotiable

```
Context check → Auth → Ticket → Test → Update claude.md → Clear → Repeat
```

Skipping any step creates problems: skip the auth re-check and Jira hangs; skip the claude.md update and the next ticket starts without context; skip the `/clear` and the full context degrades performance.

### Human in the Loop Matters Most at Two Points

1. **The architecture review** — this is your opportunity to catch structural problems before they are built. Read every decision. Challenge what seems wrong.
2. **The acceptance check** — after every ticket, manually verify every item in the original ticket description was implemented. Feature Dev is not perfect and occasionally skips items.

### The One-Command Pattern

```
/feature-dev:feature-dev Implement Jira ticket [ID] with [tech]. 
Make a PR when done.
```

Combined with Atlassian MCP (reads the ticket) and GitHub MCP (raises the PR), this single command orchestrates the entire development lifecycle. Four tickets. One day. One complete SaaS product.

---

*End of Day 5 — Pro Week Notes. Week 2 Complete.*
