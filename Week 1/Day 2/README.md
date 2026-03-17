# 🤖 The Definitive AI Coder Course — Day 2 Complete Notes
### *Foundations: How LLMs Work, Agents, Context Engineering & Workflows*

---

## Table of Contents

1. [Day 2 Overview — What to Expect](#1-day-2-overview--what-to-expect)
2. [What is an LLM? The Core Mechanics](#2-what-is-an-llm-the-core-mechanics)
3. [LLM vs. AI Application — A Critical Distinction](#3-llm-vs-ai-application--a-critical-distinction)
4. [The 4 Tricks That Make LLMs Powerful](#4-the-4-tricks-that-make-llms-powerful)
   - [Trick 1 — The Illusion of Memory](#trick-1--the-illusion-of-memory)
   - [Trick 2 — Reasoning / Thinking](#trick-2--reasoning--thinking)
   - [Trick 3 — Tools](#trick-3--tools)
   - [Trick 4 — The Loop](#trick-4--the-loop)
5. [Defining an AI Agent](#5-defining-an-ai-agent)
6. [Context Engineering — The Most Important Concept](#6-context-engineering--the-most-important-concept)
   - [What is Context?](#what-is-context)
   - [The 5 Components of Context](#the-5-components-of-context)
   - [The Context Window](#the-context-window)
   - [Context Window Sizes of Major Models](#context-window-sizes-of-major-models)
   - [Context Compacting](#context-compacting)
7. [The agents.md File — Your Agent's Brain](#7-the-agentsmd-file--your-agents-brain)
   - [What is agents.md?](#what-is-agentsmd)
   - [How the Hierarchy Works](#how-the-hierarchy-works)
   - [Tool Names by Platform](#tool-names-by-platform)
   - [What to Put in agents.md](#what-to-put-in-agentsmd)
   - [Best Practices for Writing agents.md](#best-practices-for-writing-agentsmd)
   - [The 2025 vs. 2026 Mindset on agents.md](#the-2025-vs-2026-mindset-on-agentsmd)
8. [The Evolution of AI Coding Workflows](#8-the-evolution-of-ai-coding-workflows)
   - [Workflow 1 — Micromanagement](#workflow-1--micromanagement)
   - [Workflow 2 — Plan → Execute → Review → Test](#workflow-2--plan--execute--review--test)
   - [Workflow 3 — Spec-Driven Development (SDD)](#workflow-3--spec-driven-development-sdd)
   - [Workflow 4 — YOLO Mode](#workflow-4--yolo-mode)
   - [Workflow 5 — RALF Loops](#workflow-5--ralf-loops)
   - [Workflow 6 — Multi-Agent Orchestration](#workflow-6--multi-agent-orchestration)
   - [Which Workflow to Use?](#which-workflow-to-use)
9. [The Reality of LLMs — Avoiding the Hype](#9-the-reality-of-llms--avoiding-the-hype)
10. [Comparing LLMs — ArtificialAnalysis.ai](#10-comparing-llms--artificialanalysisai)
11. [Day 2 Wrap-Up & What's Next](#11-day-2-wrap-up--whats-next)

---

## 1. Day 2 Overview — What to Expect

Day 2 is a **theory/foundations day** (marked as a "purple day" in the curriculum). It covers the conceptual bedrock that everything else in the course builds upon. Two key notes going in:

- **More talking, less building** — unlike most days, this one is content-heavy
- **Some of this may be familiar** — if you already know how LLMs work, feel free to speed through sections. There will still be interesting insights, especially around `agents.md`, workflows, and model comparisons.

The core topics today are:

| Topic | Why It Matters |
|---|---|
| How LLMs actually work | You can't use a tool well without understanding it |
| The 4 tricks behind AI apps | Explains how chatbots, agents, and coding tools work under the hood |
| What an AI agent really is | A precise definition used throughout the course |
| Context engineering | The single most impactful skill in agentic coding |
| The `agents.md` file | How to give your coding agent the right instructions |
| Workflow evolution | The different ways to work with coding agents — from micromanagement to multi-agent orchestration |
| LLM comparison tools | How to evaluate and choose the right model for your task |

---

## 2. What is an LLM? The Core Mechanics

### The Simple Definition

A **Large Language Model (LLM)** — such as GPT from OpenAI — is a system designed to do one thing:

> **Predict what text (what tokens) should come after a given input.**

It's sometimes described as *"autocomplete on steroids"* — the same concept as your phone's predictive text, but vastly more powerful and trained on an enormous amount of data.

---

### How It Actually Works

Under the hood, an LLM is a **massive pattern-matching statistical engine**:

1. It was fed enormous amounts of training data — text from the internet and far beyond
2. It learned patterns in that data
3. Given some input text, it can predict what should come next

```
Input:  "The capital of France is..."
Output: "Paris" (high probability)
        "bananas" (very low probability)
```

---

### Tokens — Not Words

LLMs don't actually operate on words. They operate on **tokens**.

- A **token** is a chunk of a few letters — often a whole word, but sometimes part of a word
- The input to an LLM is a **sequence of tokens**
- The output is not the single most likely next word — it's the **probability of every possible next token**

This is an important distinction:
- Input: sequence of tokens
- Output: probability distribution over all possible next tokens

The LLM picks (or samples from) that probability distribution to generate the next token.

---

### Token-by-Token Generation

LLMs generate output **one token at a time**, in a loop:

```
Step 1: Input = "What is the capital of France?"
        Output = "The" (most likely next token)

Step 2: Input = "What is the capital of France? The"
        Output = "capital"

Step 3: Input = "What is the capital of France? The capital"
        Output = "of"

... and so on until: "The capital of France is Paris."
```

Each time, the **entire input so far + all tokens generated so far** is passed back in to predict the next token. This process is called **inference**.

---

## 3. LLM vs. AI Application — A Critical Distinction

This is a distinction many people blur, and it matters:

| Concept | What It Is | Example |
|---|---|---|
| **LLM** | The model itself. A statistical engine that takes tokens in and outputs the probability of the next token. | GPT (the model) |
| **AI Application / AI Product** | Software built *around* calling an LLM. It wraps the LLM with extra functionality like memory, web search, a user interface, etc. | ChatGPT (the product) |

### Real-World Examples of AI Applications

- **ChatGPT** — wraps GPT with a chat interface, memory, web search, image generation, etc.
- **Cursor Agent** — wraps an LLM with a code editor, file system access, and project context
- **Duolingo Max** — wraps an LLM into a language-learning conversation feature
- **Atlassian Rovo** — Gen AI built into Jira, Confluence, and other Atlassian products

> **Key Insight:** When you're "talking to ChatGPT," you are not talking directly to the raw GPT model. You are using a *product* that has code, memory management, tool connections, and other software wrapped around that model.

Keeping these two concepts clearly separate will help you understand everything else in this course.

---

## 4. The 4 Tricks That Make LLMs Powerful

A raw LLM is "just" a next-token predictor. But four clever techniques, implemented in the *software layer* around the LLM, are what allow us to get from basic autocomplete to fully autonomous coding agents.

---

### Trick 1 — The Illusion of Memory

#### The Reality

An LLM is **completely stateless**. Every time you call it with an input sequence, it has **zero knowledge of any previous calls**. Each call is independent.

**If you called the raw GPT model directly:**
```
Call 1 → Input:  "I'm Ed."
         Output: "Hello, Ed!"

Call 2 → Input:  "Who am I?"
         Output: "I don't know. I don't have that information."
```

The model has no idea who "Ed" is, because it has no memory of Call 1.

#### The Trick

The software layer (the AI application) solves this by **passing the entire conversation history** on every call:

```
Call 2 → Input:  "I'm Ed." + "Hello, Ed!" + "Who am I?"
         Output: "You're Ed — you just told me!"
```

Every message sent to the LLM includes **all prior messages and all prior responses**. This creates the *illusion* that the LLM "remembers" the conversation.

> **This is not a feature of the LLM — it's a feature of the software wrapper around it.**

This is exactly how ChatGPT works. Every time you type a message, the application sends your entire conversation thread to the model, not just your latest message.

---

### Trick 2 — Reasoning / Thinking

#### The Discovery

Researchers noticed something surprising: if you add the phrase **"Please think step by step"** to the end of a prompt, you often get significantly better answers. This led to a whole new approach to training models.

#### How It Works

Models can be trained to **generate "thinking tokens"** before giving an answer — they output a description of *how they're going to approach the problem* before actually solving it.

As a side effect of generating these reasoning tokens, the model tends to arrive at better, more accurate answers.

#### Example — The Coin Puzzle

**Question:** "You toss two coins. One of them is heads. What's the probability the other is tails?"

| Approach | Output | Correct? |
|---|---|---|
| Without reasoning | 1/2 (50%) | ❌ Wrong |
| With step-by-step reasoning | 2/3 (66.7%) | ✅ Correct |

The intuitive answer is 50%, but the correct answer is 2/3 (because you're not told *which* coin is heads — there are three equally likely scenarios where at least one coin is heads: HH, HT, TH — and in two of those three, the other coin is tails).

With reasoning enabled, the model first says *"this is probably a trick question, let me think this through carefully"* and then arrives at the right answer.

> **Key Insight:** Generating tokens to describe its own thinking process causes the model to produce better outputs. It sounds counterintuitive, but it consistently works.

---

### Trick 3 — Tools

#### The Concept

Tools are about realizing that the **tokens an LLM generates don't have to be just text responses** — they can also be **instructions to perform actions**.

The idea: include in the input (the prompt) a description of actions the LLM is allowed to request. When the LLM wants to perform one of those actions, it generates special tokens that say so. The software layer reads those tokens, performs the action, and calls the LLM again with the result.

#### The Flow

```
1. User prompt sent to LLM → includes list of available tools

2. LLM generates output:
   → Either a text response, OR
   → "I want to call the [tool name] with these parameters"

3. Software layer executes the tool

4. Software layer calls LLM again with the tool's result

5. LLM continues generating its response
```

#### Real Example — Python Code Execution

A prompt like:

> *"You can respond with Python: followed by a Python expression if you'd like to calculate something. What is the square root of π?"*

The LLM doesn't just answer "1.7724..." — instead, it outputs:

```python
Python: import math; print(math.sqrt(math.pi))
```

It decided to use the Python tool rather than guessing the answer. The software runs that code and returns the result.

#### Important Reality Check

> **The LLM itself never actually runs any code or searches the internet.** It just generates tokens that *say* it wants to do those things. It's the software wrapper around the LLM that actually executes the tools and returns the results.

The LLM is always and only a statistical token generator. Tools are a clever trick to make it *coordinate* with real-world actions.

---

### Trick 4 — The Loop

#### The Concept

What if, instead of calling an LLM once and getting one response, you called it **multiple times in a loop** until some goal is met?

```
Call LLM → Get output → Check: Is goal achieved?
   → No: Add output to context, call LLM again
   → Yes: Done
```

This simple loop idea unlocks the ability to achieve **much bigger, more complex goals** than a single LLM call ever could.

#### Why It's So Powerful

A single call might generate one function. A loop can:
- Generate a file
- Check if it runs correctly
- Fix errors
- Add features
- Write tests
- ... all iteratively, in sequence

> **This loop idea is the backbone of every coding agent.** When you watched Cursor Agent building the FPS game in Day 1, you were watching this trick in action — the LLM was called dozens of times in a loop.

---

### Putting It All Together

These four tricks, layered on top of a basic next-token predictor, are what give us everything from ChatGPT to fully autonomous coding agents:

```
Raw LLM
  + Trick 1 (Illusion of Memory)     → Conversational AI
  + Trick 2 (Reasoning/Thinking)     → More accurate, thoughtful responses
  + Trick 3 (Tools)                  → AI that can act on the world
  + Trick 4 (Loop)                   → AI that can achieve complex, long-horizon goals
  = AI Agent
```

---

## 5. Defining an AI Agent

The term "AI agent" has been used loosely and has evolved over time. Here's a clear historical progression of its definitions:

---

### Definition 1 — OpenAI's Early Definition (circa 2023)

> **"AI systems that can do work for you independently."**

The clearest example: a product (formerly called Operator, now GPT Agent) that can open a browser, search for restaurants, check availability, make a reservation — all while you watch. There's a sense of *something autonomously doing work on your behalf*.

---

### Definition 2 — Hugging Face / Anthropic (early 2025)

> **"AI systems where an LLM controls the workflow."**

The LLM's output tokens don't just provide answers — they *orchestrate what happens next*. The LLM decides what steps to take, when to call tools, and how to sequence actions toward a goal.

Anthropic reinforced this with their seminal blog post *"Building Effective Agents."*

---

### Definition 3 — The Current Winning Definition (Simon Willison, late 2025)

> **"An LLM that runs tools in a loop to achieve a goal."**

This is the definition used throughout this course. It ties together Tricks 3 and 4 directly:

```
AI Agent = LLM + Tools + Loop + Goal
```

This maps exactly to what you saw with the Cursor Agent in Day 1:
- **Goal:** Build a 3D first-person shooter game in a web page
- **Loop:** The agent was called many times in sequence
- **Tools:** It had tools to create files, write code, and run checks
- **Result:** It achieved the goal autonomously

---

## 6. Context Engineering — The Most Important Concept

### What is Context?

**Context** refers to the entire input that gets passed to an LLM for a given call.

Because an LLM is stateless — it has no memory between calls — everything the LLM needs to know must be passed in *every single time* as part of this input package. This input is called the **context**.

> **"The output of an LLM is based entirely on the input. Getting that input right is everything — it's all the LLM has."**

**Prompt Engineering** (the older term) has evolved into the broader concept of **Context Engineering** — because it's not just about the prompt text. It's about everything that gets packed into the context: system prompts, tools, memory, conversation history, special files, and more.

---

### The 5 Components of Context

Here is a breakdown of everything that gets packed into a single LLM call:

```
┌─────────────────────────────────────────────────────────────┐
│                        CONTEXT                              │
│                                                             │
│  1. SYSTEM PROMPT                                           │
│     The overall framing — role, tone, approach, objective   │
│                                                             │
│  2. TOOL DESCRIPTIONS                                       │
│     Descriptions of every tool the LLM can call            │
│                                                             │
│  3. MEMORY                                                  │
│     Persisted information across conversations              │
│                                                             │
│  4. agents.md (or Claude.md / Gemini.md)                    │
│     Special project-specific file for coding agents         │
│                                                             │
│  5. CONVERSATION HISTORY                                    │
│     Every message sent + every reply received so far,       │
│     including reasoning tokens, generated code,             │
│     tool calls, and tool results                            │
└─────────────────────────────────────────────────────────────┘
```

#### 1. System Prompt
The **system prompt** is the most fundamental part of the context. It's the overall framing that tells the LLM:
- What role it is playing (e.g., "You are a coding agent responsible for writing Python code")
- What its overall job is
- The tone it should take (formal, casual, etc.)
- General approach and constraints

This is usually placed at the very beginning of the context.

#### 2. Tool Descriptions
This section lists all the **tools the LLM can request to use**. Each tool needs a description so the LLM understands what it does and when to use it. The more tools you give the LLM, the more space this takes up in the context.

Some people consider tool descriptions to be part of the system prompt — the distinction is mostly semantic and doesn't affect how the system works.

#### 3. Memory
**Memory** is information that persists across multiple conversations — things you'd want the LLM to always have access to, regardless of which conversation it's in. This is sometimes called long-term or medium-term memory.

#### 4. agents.md
A special file (covered in detail in Section 7) that is particular to **coding agents**. It contains project-specific information: coding standards, project goals, known constraints, etc. It gets injected into the context automatically.

#### 5. Conversation History
Because of the "illusion of memory" trick (Trick 1), the **entire conversation** must be included in the context every single time:
- Every message the user has sent
- Every response the LLM has generated
- Any reasoning tokens the LLM generated to "think" through problems
- Any tool calls the LLM requested
- The results returned by those tool calls
- Any code generated so far

All of this must be squeezed into the context window every time the LLM is called.

---

### The Context Window

Every LLM has a maximum number of tokens it can accept as input. This is called the **context window** (or context window limit).

> If you try to pass in more tokens than the maximum context window size, the call will fail with an error.

#### Less is More — Even Before You Hit the Limit

This is a critical insight that's often overlooked:

> **Even if you haven't reached the context window limit, having too much in the context can degrade the quality of the LLM's outputs.**

As you fill up the context:
- The LLM may start to "lose coherence"
- It may begin forgetting things mentioned earlier
- The quality, accuracy, and relevance of responses may decrease

Conversely: the **best performance** typically comes at the *very start* of a fresh conversation, when the context is nearly empty and the LLM has very little to process.

**Takeaway:** Don't just worry about hitting the limit — actively aim to keep the context as lean as possible.

---

### Context Window Sizes of Major Models

| Model | Provider | Context Window |
|---|---|---|
| **Gemini 3 / Antigravity** | Google | 1,000,000 tokens |
| **GPT 5.2 / GPT 5.2 Codex** | OpenAI | 400,000 tokens |
| **Claude Sonnet 4.5 / Opus 4.5** | Anthropic | 200,000 tokens |

> **Note:** Bigger context windows don't necessarily mean better performance. As stated above, performance degrades as the context fills up — regardless of the limit. Keep contexts lean for best results.

---

### Context Compacting

**What is compacting?**
When the context window starts to fill up, tools like Claude Code have a built-in feature called **compacting** (also called context compaction). Instead of failing with an error, the system:

1. Detects that the context window is almost full
2. Looks back at the entire conversation history
3. Summarizes it into a compact version
4. Replaces the full history with the summary, freeing up context space

#### Why People Fear the Compactor

Compacting is an automated summarization — and summarization means decisions are made about what's important and what's not. The risk:

- The LLM doing the summarization might miss something important
- Critical instructions or decisions from earlier in the conversation might be dropped
- The agent might then make the same mistake twice, or forget a constraint you gave it — which is deeply frustrating

#### The Old Guard Approach (2025 mindset)
Many experienced developers, including the instructor, would rather:
1. Stop the agent before it compacts
2. Manually review what's happened
3. Rewrite `agents.md` to capture the important bits
4. Start a completely fresh context

This gives you full control over what gets preserved.

#### The Current Reality (2026)
Compacting has **significantly improved**. Modern compactors do a genuinely good job of summarizing conversations and retaining what matters.

> **Recommendation for new learners:** Start by trusting the compactor. Let it do its thing. It will often work well. You can always develop your own judgment about when to intervene as you get more experience.

---

## 7. The agents.md File — Your Agent's Brain

### What is agents.md?

`agents.md` is a special **Markdown file** that you create in your project and that gets injected into the context of your coding agent. Think of it as a persistent set of instructions and project knowledge that your agent always has access to.

#### Why Markdown?

Markdown is a lightweight text format that:
- Is simple to write (hash for headings, hyphens for bullets, etc.)
- Is highly readable for humans
- Is loved by LLMs — they've been trained on enormous amounts of markdown, so they read and generate it fluently

```markdown
# Project Summary

## Goals
- Build a SaaS invoicing platform
- Support multi-tenant architecture

## Coding Standards
- Use Python 3.12+
- Always use UV for package management
- Keep functions under 50 lines
```

---

### How the Hierarchy Works

You can have `agents.md` files at **multiple levels** of your project directory:

```
project-root/
│
├── agents.md          ← Always loaded (root-level)
│
├── backend/
│   ├── agents.md      ← Loaded when agent works on backend files
│   └── ...
│
└── frontend/
    ├── agents.md      ← Loaded when agent works on frontend files
    └── components/
        ├── agents.md  ← Loaded when agent works on components
        └── ...
```

**Rules:**
- The **root-level** `agents.md` is always loaded into the context
- **Subdirectory** `agents.md` files are only loaded when the agent is working on files in that subdirectory (or deeper)
- **Inner directory files override outer directory files** — if there's a conflict, the more specific (deeper) file wins
- When working in a subdirectory, the agent loads all relevant `agents.md` files working **upward through the tree** to the root

This gives you the ability to have **general project rules at the top** and **specific overrides deeper in the directory structure**.

---

### Tool Names by Platform

The file is called different things on different platforms, but it's the same concept:

| Platform | File Name |
|---|---|
| Cursor | `agents.md` |
| Codex | `agents.md` |
| GitHub Copilot | `agents.md` |
| Claude Code | `claude.md` |
| Antigravity (Google) | `gemini.md` |

> Cursor and GitHub Copilot also support other special files (like Cursor Rules), but the trend across the industry is converging on `agents.md` as the de facto standard.

---

### What to Put in agents.md

Here are the key categories of information to include:

#### 1. Project Goals & Success Criteria
- What is this project trying to achieve?
- What does "done" look like?
- Include a checklist the agent can check items off as it progresses

#### 2. Links to Supporting Documents
- Reference other relevant files the agent can load when needed
- Design docs, API specs, architecture diagrams

#### 3. Coding Standards
- Language versions (e.g., "Use Python 3.12+")
- Frameworks to use or avoid
- File/function length limits
- Testing requirements

#### 4. Known Anti-Patterns to Avoid
- Things this agent has gotten wrong before
- Specific bad habits of LLMs that apply to your project

#### 5. Tooling Preferences
- Specific package managers (e.g., "Always use UV, never `python3` directly")
- Build tools, formatters, linters

---

### Best Practices for Writing agents.md

#### ✅ Do These

| Practice | Reason |
|---|---|
| **Be concise** | Every word costs context window space — make it count |
| **Be specific** | Vague instructions get vague results |
| **Use natural language** | Write it like a prompt — assertive, clear, minimal ambiguity |
| **Focus on what it SHOULD do** | LLMs respond better to positive instructions than negative ones |
| **Use IMPORTANT in block caps** | Empirically, writing `IMPORTANT:` before a critical rule increases adherence |
| **Use backticks for code** | Single backtick for inline code, triple backticks for code blocks |
| **Keep READMEs short** | Explicitly tell the agent "keep READMEs concise" — LLMs love generating bloated READMEs |
| **No emojis** | Explicitly say "no emojis" if you don't want them |

#### ❌ Avoid These

| Anti-Pattern | Reason |
|---|---|
| **Verbose text** | Wastes precious context space |
| **Too many "do not" rules** | LLMs are less coherent at remembering prohibitions than permissions |
| **Over-complicated structure** | Keep it readable and scannable |
| **Stale information** | Regularly prune outdated rules and instructions |
| **Long wordy READMEs** | LLMs default to generating verbose READMEs — tell them not to |

#### A Note on Negatives

LLMs are noticeably *less reliable* at remembering things they're told *not* to do, compared to things they're told *to* do. You can use a few "never" rules, but don't rely on them heavily. Instead, frame things positively:

- ❌ *"Never use try/except around everything"*
- ✅ *"Only catch exceptions when they are genuinely expected and meaningful to handle"*

---

### The 2025 vs. 2026 Mindset on agents.md

There are two schools of thought, representing how the field has evolved:

#### The 2025 Mindset — Meticulous Context Management

- Invest significant time crafting an excellent `agents.md`
- Have multiple `agents.md` files at different directory levels
- Continually rewrite and prune as the project evolves
- Stop the agent regularly, update the file, restart fresh
- Have the LLM rewrite its own `agents.md` under your direction
- Treat every line as precious

#### The 2026 Mindset — Let It Go

- Focus on the end goal, not the detailed instructions
- Trust the agent more, give it more autonomy
- Use newer features (skills, sub-agents, agent swarms) rather than relying on a perfectly crafted `agents.md`
- Let the agent self-correct
- Less micromanagement, more high-level direction

#### The Instructor's Honest Take

> *"I hate to say it, but I'm still of the 2025 school of thought — at least for mission-critical projects. For toy projects or new greenfield MVPs, I'll use the 2026 approach. But for production-grade work on large codebases? I'm still all over the context window."*

The right approach depends on:

| Factor | Lean Toward |
|---|---|
| Mission-critical / production software | 2025 mindset (careful context management) |
| Large or complex codebases | 2025 mindset |
| Highly innovative code (e.g., MCP integrations) | 2025 mindset |
| New greenfield MVP / prototype | 2026 mindset |
| Boilerplate-heavy work (React frontend, etc.) | 2026 mindset |
| You have risk appetite / are experimenting | 2026 mindset |

---

## 8. The Evolution of AI Coding Workflows

A **workflow** describes *how you organize your activities* when working with a coding agent. This has evolved dramatically as models and tooling have improved.

There are six distinct workflow levels — the first three represent the **2025 mindset**, and the last three represent the **2026 mindset**:

---

### Workflow 1 — Micromanagement

**Trust Level:** Very Low  
**Speed:** Slow  
**Control:** Very High

This was how most people started using coding agents in 2025:

- Write very specific instructions in `agents.md`
- **Approve every change** the agent proposes
- **Frequently stop** the agent mid-task
- Go back, rewrite `agents.md`, then run it again
- Check everything at each step

**When to use:** Learning the tool, highly sensitive code, debugging a specific known issue.

---

### Workflow 2 — Plan → Execute → Review → Test

**Trust Level:** Low-Medium  
**Speed:** Moderate  
**Control:** High

This introduces a two-phase approach:

**Phase A — Planning Mode:**
- Put the agent in "plan mode" (available in most tools)
- The agent produces a to-do list / documentation of what it plans to do
- You review and agree on the plan together

**Phase B — Execution Mode:**
- Tell the agent to proceed
- Execute in phases — the agent builds one piece at a time
- After each phase: code review → test → mark complete → next phase

**The cycle for each phase:**
```
Agent builds → You review code → Agent tests → You validate → Mark complete → Next phase
```

**When to use:** Production features, team environments, any work where you want oversight but not total control.

---

### Workflow 3 — Spec-Driven Development (SDD)

**Trust Level:** Medium  
**Speed:** Faster  
**Control:** Medium

Also called **"Trust but Verify"**:

- You write a detailed specification of what needs to be built
- Some tools support formal spec languages for very precise descriptions
- The agent goes off and builds against that spec autonomously
- You come back at the end and verify the outputs meet the spec
- No step-by-step code review during the process

**When to use:** Well-understood requirements, feature additions to existing codebases, when you have strong specs and test suites.

---

### Workflow 4 — YOLO Mode

**Trust Level:** High  
**Speed:** Fast  
**Control:** Low

**YOLO** = *"You Only Live Once"*

- The agent has **full autonomy** — no permission prompts, no approval gates
- You set it going and let it run without interruption
- You can leave it running over dinner and come back to the results
- All decisions are made by the agent

**When to use:** Building MVPs from scratch, boilerplate-heavy work (React frontends, CRUD APIs), hobby projects, experimentation.

> YOLO mode has been around most of 2025, but is only now being used seriously for real projects, not just toys — which is why it's categorized as a "2026 mindset" workflow.

---

### Workflow 5 — RALF Loops

**Trust Level:** Very High  
**Speed:** Very Fast (runs for hours)  
**Control:** Minimal

**Invented by:** Australian developer Jeffrey Huntley  
**Named after:** Ralph Wiggum from The Simpsons — a naive, optimistic character

#### What is a RALF Loop?

An agent already runs an LLM in a loop to achieve a goal (that's the definition of an agent). A RALF Loop **wraps that entire agent loop inside an even bigger outer loop**:

```
OUTER LOOP (runs up to ~10 times):
  ├── Run full inner agent loop → Produces output
  ├── Automated test: "Is the goal fully achieved? Is this as good as it can be?"
  ├── If NO: Generate feedback about the gaps
  │         Add feedback to objectives
  │         Loop back → Run the inner agent loop again
  └── If YES: Done
```

#### Key Properties

- The **feedback mechanism is automated** — an LLM evaluates its own output and generates the feedback
- You don't intervene between iterations
- This can run **overnight** and produce an enormous amount of high-quality work
- It was used to produce the impressive FPS demo shown in Day 1 — one prompt, no human feedback, just RALF Loops running autonomously

> **RALF Loop vs. YOLO:** YOLO runs for maybe an hour. RALF Loops run for multiple hours, sometimes overnight. YOLO is a single long run; RALF is nested loops with self-generated feedback.

**When to use:** Large new features from scratch, complete greenfield applications, when you want the highest-quality autonomous output and have time to let it run.

---

### Workflow 6 — Multi-Agent Orchestration

**Trust Level:** Complete  
**Speed:** Extreme  
**Control:** Architectural only

This is the most advanced workflow — the culmination of the entire course:

- **Multiple agents** running simultaneously, each with a specific role
- Possible roles: coding agent, testing agent, feedback agent, code review agent
- Agents organized in a **hierarchy** with manager agents and worker agents
- An **orchestrator agent** manages all other agents — you don't manually coordinate
- Can involve **agent swarms** (many agents spawned dynamically)

This maps to **Stage 7 and Stage 8** from Steve Yegge's framework (covered in Day 1).

**When to use:** Large-scale builds, complex multi-part systems, when maximum throughput and coverage are needed.

---

### Which Workflow to Use?

The answer is: **it depends on the project**.

```
┌─────────────────────────────────────────────────────────────────┐
│                    CHOOSING A WORKFLOW                          │
│                                                                 │
│  ┌─────────────────────────────┐  ┌───────────────────────────┐ │
│  │   MISSION CRITICAL          │  │   EXPLORATORY / MVP       │ │
│  │                             │  │                           │ │
│  │ • Production software       │  │ • New prototype           │ │
│  │ • Large codebases           │  │ • Greenfield project      │ │
│  │ • Innovative/novel code     │  │ • Boilerplate-heavy work  │ │
│  │ • Enterprise environments   │  │ • You have risk appetite  │ │
│  │ • MCP integrations          │  │ • Hobby projects          │ │
│  │                             │  │                           │ │
│  │ → Workflows 1, 2, or 3      │  │ → Workflows 4, 5, or 6   │ │
│  │   (2025 mindset)            │  │   (2026 mindset)          │ │
│  └─────────────────────────────┘  └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

### A Final, Critical Reminder

> **You are accountable for the code you deliver, regardless of whether an LLM wrote it.**

This is especially important for people early in their careers:

- Using an LLM does not transfer responsibility for code quality
- "The LLM wrote it" is not an excuse for bugs, security holes, or bad architecture
- It is always your job to **check, validate, and take ownership** of the output
- Choose the workflow that matches the level of risk appropriate for the task

LLMs are a powerful tool that allow you to do more — but the professional standard of code quality remains your responsibility.

---

## 9. The Reality of LLMs — Avoiding the Hype

An honest, grounded assessment of where LLMs genuinely excel and where they still fall short:

### Where LLMs Are Transformative

| Scenario | Impact |
|---|---|
| **Boilerplate-heavy frontend work** (e.g., a React app with lots of UI components) | Days → Minutes. Genuinely order-of-magnitude improvement |
| **New greenfield projects** from scratch | Very high impact — LLMs can crank out foundational code very fast |
| **Cookie-cutter backend** (CRUD APIs, standard patterns) | Very high impact |

**Example:** A boilerplate React frontend that might take a great frontend developer one day, and the instructor several weeks, can be produced by an LLM in minutes.

### Where LLMs Are Only Incrementally Better

| Scenario | Impact |
|---|---|
| **Large, complex, existing codebases** | More limited — the LLM has to understand a large context first |
| **Highly innovative / novel code** | Reduced — LLMs don't have training examples for truly new patterns |
| **MCP server integrations** | Difficult — too new, not enough training data, tends to produce non-idiomatic code |
| **Subtle logic bugs** | Sometimes LLMs introduce very subtle mistakes that take longer to find than writing it correctly would have |

### The Honest Aggregate Assessment

> *"As an aggregate for me, LLMs are a multiplier — but it's not a 10x. How much more you can achieve depends critically on the project."*

There is a growing **anti-AI movement** among some developers who became frustrated by overhyped promises and bad experiences. This is understandable — but the right response is not rejection. It's:

1. Learn how to use these tools properly
2. Know where they genuinely help and where they don't
3. Set realistic expectations
4. Be able to articulate both the pros and the cons accurately

Both extreme positions — "LLMs will replace all programmers" and "LLMs are useless toys" — are wrong. The truth is nuanced, tool-dependent, and project-dependent.

---

## 10. Comparing LLMs — ArtificialAnalysis.ai

### The Site

**Website:** [artificialanalysis.ai](https://artificialanalysis.ai)

This is described as the single most important bookmark you should have if you work in this space. It is a comprehensive, regularly updated resource for comparing LLMs across multiple dimensions.

> *"I only have one bookmark. It should be artificialanalysis.ai."*

---

### What You'll Find There

#### Intelligence Index
A single composite score representing overall model intelligence. As of the time of recording, the top models (in order) were:

| Model | Provider | Notes |
|---|---|---|
| **GPT 5.2** | OpenAI | Top of the intelligence index |
| **Claude Opus 4.5** | Anthropic | Instructor's personal model of choice (especially within Claude Code) |
| **GPT 5.2 Codex** | OpenAI | Variant of GPT 5.2 optimized specifically for coding |
| **Gemini 3 Pro** | Google | Strong performer, especially for long context |

> **Important:** By the time you read this, there will likely be newer, stronger models — models get released every week. Your results will likely be better than what was shown in the course.

#### The Inflection Point — November 2025

The charts on ArtificialAnalysis show a dramatic jump in model intelligence around **November 2025**. This was when:
- New reasoning techniques matured
- Models like Claude Sonnet/Opus 4.5, Gemini 3, and GPT 5.2 launched
- The frustration and anger phase of the emotional journey (from Day 1) largely gave way to acceptance and mastery

Some developers still have "scar tissue" from the pre-November 2025 era — they gave up on LLMs after too many bad experiences. The recommendation: *encourage them to try again, because so much has changed.*

#### Other Dimensions Available

Beyond intelligence, the site lets you compare models on:
- **Speed** (tokens per second, latency)
- **Price** (cost per million tokens)
- **Coding benchmarks** (specific performance on coding tasks)
- **Tool use** (ability to correctly call and use tools)
- **Context window size**
- **Frontier model intelligence over time** (historical chart)

#### An Interesting Finding

One of the top performers in the **tool use** benchmark is **GLM-4 (GLM47)** from **Zhiyi (智谱AI)** — a Chinese AI startup. It scores very highly on tool-calling ability, which is a critical skill for coding agents. This is a reminder that strong AI models are being developed globally, not just by OpenAI, Anthropic, and Google.

---

### How to Use This Resource

- Visit regularly — models change fast
- Before starting a major project, check the current top models for coding performance
- Use the coding-specific benchmarks when choosing a model for development work
- Check the tool use benchmarks if your project involves heavy agent tooling
- Don't just look at intelligence — consider speed and price for your specific use case

---

## 11. Day 2 Wrap-Up & What's Next

### What You've Covered Today

✅ How LLMs actually work — tokens, inference, statelessness  
✅ The difference between an LLM and an AI application  
✅ The 4 tricks that power modern AI apps (memory, reasoning, tools, loops)  
✅ The precise definition of an AI agent: *"an LLM that runs tools in a loop to achieve a goal"*  
✅ Context engineering — the components of a context, the context window, and compacting  
✅ The `agents.md` file — what it is, how it works, how to write a great one  
✅ The 6 workflows — from micromanagement to multi-agent orchestration  
✅ The reality of LLMs — where they genuinely help and where they don't  
✅ ArtificialAnalysis.ai — how to compare models effectively  

**You are now 13% complete with the course! 🎉**

---

### Key Mental Models to Take Forward

```
1. LLM = stateless next-token predictor
2. AI Application = LLM + memory trick + reasoning + tools + loops
3. AI Agent = LLM + tools + loop + goal
4. Context = everything the LLM knows for this call
5. agents.md = your agent's persistent brain for a project
6. Workflow = your strategy for collaborating with the agent
```

---

### Coming Up Tomorrow — Day 3

**Day 3 is a tools day (yellow day):**
- A hands-on look at the major coding agent tools
- Cursor deep-dive
- GitHub Copilot
- Codex (OpenAI)
- Antigravity (Google)

> *"Tomorrow we look at tools, tools, tools. It's going to be really fun. I can't wait to show you all of that."*

---

*📝 Notes compiled from Day 2 lectures of the AI Coder Course — covering all 6 segments: How LLMs Work (Tokens, Memory, Reasoning), Tools & Loops & Agent Definition, Context Engineering, agents.md Mastery, Workflow Evolution (YOLO to RALF Loops), and LLM Comparison on ArtificialAnalysis.*
