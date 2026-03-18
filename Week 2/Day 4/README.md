# Day 4 — Pro Week: Building with Claude Code — Jira, MCP & Plugins Workflow + Debugging Strategies

> **Overview:** Day 4 is where everything from the week comes together in practice. After covering MCP, Skills, and Plugins on Day 3, this day puts them to work inside a real, end-to-end professional development workflow — from a Jira ticket all the way to a merged Pull Request on GitHub. The day also ends with a thorough, disciplined debugging strategy for when things go wrong.

---

## Table of Contents

1. [Day 3 Recap — The Three Extension Methods](#1-day-3-recap--the-three-extension-methods)
2. [Today's Goal — A Real Professional Workflow](#2-todays-goal--a-real-professional-workflow)
3. [The Project — Pre-Legal: A Legal Document Platform](#3-the-project--pre-legal-a-legal-document-platform)
4. [Setting Up Jira — The Starting Point of Every Feature](#4-setting-up-jira--the-starting-point-of-every-feature)
   - [What is Jira and Why Start Here?](#what-is-jira-and-why-start-here)
   - [Creating a Free Jira Account](#creating-a-free-jira-account)
   - [Creating Your Jira Space and First Issue](#creating-your-jira-space-and-first-issue)
5. [Connecting Claude Code to Jira via Atlassian MCP Server](#5-connecting-claude-code-to-jira-via-atlassian-mcp-server)
   - [Installing the Atlassian MCP Server](#installing-the-atlassian-mcp-server)
   - [OAuth Authentication with Jira](#oauth-authentication-with-jira)
   - [Dealing with Atlassian Re-Authentication (Known Issue)](#dealing-with-atlassian-re-authentication-known-issue)
   - [Testing the Jira Connection](#testing-the-jira-connection)
6. [Setting Up the GitHub Repository](#6-setting-up-the-github-repository)
   - [Creating the GitHub Repo](#creating-the-github-repo)
   - [Generating a Fine-Grained Personal Access Token](#generating-a-fine-grained-personal-access-token)
   - [Cloning the Repo Locally](#cloning-the-repo-locally)
7. [Connecting Claude Code to GitHub via MCP Server](#7-connecting-claude-code-to-github-via-mcp-server)
   - [Installing the GitHub MCP Server](#installing-the-github-mcp-server)
   - [Testing GitHub Integration — Creating an Issue and PR](#testing-github-integration--creating-an-issue-and-pr)
   - [Why Use MCP Servers Directly Instead of the Plugin?](#why-use-mcp-servers-directly-instead-of-the-plugin)
8. [Installing the Feature Dev Plugin](#8-installing-the-feature-dev-plugin)
   - [What is Feature Dev?](#what-is-feature-dev)
   - [Feature Dev vs Ralph Loops — The Spectrum of Autonomy](#feature-dev-vs-ralph-loops--the-spectrum-of-autonomy)
   - [How to Install Feature Dev](#how-to-install-feature-dev)
9. [Project Initialisation — Boilerplate and Git Ignore](#9-project-initialisation--boilerplate-and-git-ignore)
10. [The Full Workflow — Jira Ticket to Merged PR](#10-the-full-workflow--jira-ticket-to-merged-pr)
    - [Step 1 — Write a Good Jira Issue](#step-1--write-a-good-jira-issue)
    - [Step 2 — Task PL-2: Data Curation with Autonomous Problem-Solving](#step-2--task-pl-2-data-curation-with-autonomous-problem-solving)
    - [Step 3 — Task PL-3: Building the NDA Creator App with Feature Dev](#step-3--task-pl-3-building-the-nda-creator-app-with-feature-dev)
    - [The Single Command That Does It All](#the-single-command-that-does-it-all)
    - [The Feature Dev Seven-Step Process in Action](#the-feature-dev-seven-step-process-in-action)
    - [Results — What Claude Built](#results--what-claude-built)
11. [Closing the Loop — Tests, Code Review, and Merging](#11-closing-the-loop--tests-code-review-and-merging)
    - [Discovering a Skipped Step](#discovering-a-skipped-step)
    - [Triggering a Code Review and Tests](#triggering-a-code-review-and-tests)
    - [Final Merge and Jira Status Update](#final-merge-and-jira-status-update)
12. [Debugging Strategies — A Disciplined Approach](#12-debugging-strategies--a-disciplined-approach)
    - [Before You Debug — Take a Snapshot](#before-you-debug--take-a-snapshot)
    - [Mode 1 — Quick Interactive Approach (Copy-Paste Loop)](#mode-1--quick-interactive-approach-copy-paste-loop)
    - [Mode 2 — Disciplined Systematic Debugging](#mode-2--disciplined-systematic-debugging)
    - [The Five-Step Debugging Process](#the-five-step-debugging-process)
    - [Critical Warning — The "I Found It" Hallucination Trap](#critical-warning--the-i-found-it-hallucination-trap)
    - [Pro Tip — Use a Different LLM for Hard Problems](#pro-tip--use-a-different-llm-for-hard-problems)
    - [The Systematic Debugging Skill](#the-systematic-debugging-skill)
13. [Key Takeaways — Day 4 Summary](#13-key-takeaways--day-4-summary)

---

## 1. Day 3 Recap — The Three Extension Methods

Before diving into the workflow, a quick summary of where Day 4 starts from:

| Method | Core Idea | Big Pro | Big Con |
|---|---|---|---|
| **MCP** | Connect Claude Code to external tool processes using an open standard. | Enormous ecosystem of available tools. | Complex to set up; can consume context window (improved with lazy loading). |
| **Skills** | Package instructions and scripts as markdown files with progressive disclosure. | Context-efficient; simple to share via Git. | Less powerful than MCP; ecosystem still maturing. |
| **Plugins** | Bundle MCP servers, skills, commands, and agents into one-click installs. | Simplest to use; best of both MCP and skills. | Claude Code only; too many plugins can degrade performance. |

**The general rule for choosing:** Start with plugins → use MCP for specialized data/tools → use skills for team-shared knowledge.

---

## 2. Today's Goal — A Real Professional Workflow

Day 4 is about moving from *knowing* the tools to *using* them in a realistic, professional development process. The workflow being demonstrated covers the **entire feature development lifecycle**:

```
Jira Ticket → Claude Code → Feature Dev Plugin → GitHub PR → Merge → Jira Done
```

This is the kind of process that a development team might use day-to-day. It integrates:
- **Jira** (or GitHub Issues) as the source of work.
- **Claude Code** as the coding engine.
- **Atlassian MCP Server** to read and update Jira issues.
- **GitHub MCP Server** to create commits, PRs, and merges.
- **Feature Dev Plugin** to enforce a disciplined, seven-step development process.

The important thing to note is that **this is not one prescriptive path**. You can follow the exact same workflow but build something completely different. This is a workflow template — a choose-your-own-adventure where the process is fixed but the product is yours.

---

## 3. The Project — Pre-Legal: A Legal Document Platform

The product being built throughout Day 4 and Day 5 is called **Pre-Legal**.

**The concept:** A platform for drafting common legal documents (NDAs, client contracts, engagement letters, etc.) based on a repository of templates. The name "Pre-Legal" reflects that it is not meant to replace a lawyer — it is meant to do the *pre-work* so that a lawyer, paralegal, or attorney is best set up to finalise the document.

**Why this project:**
- It is a real product idea with genuine monetization potential.
- It naturally involves Gen AI (LLM-generated document filling).
- It requires both a data layer (template repository) and a UI layer (form-driven document generator).
- It is complex enough to be realistic but contained enough to build in a day.

---

## 4. Setting Up Jira — The Starting Point of Every Feature

### What is Jira and Why Start Here?

**Jira** is Atlassian's issue-tracking and project management tool. It is the industry standard for software development teams — used in the overwhelming majority of tech companies to manage work into tickets called "issues" (now called "work items" in newer versions).

The reason to start with Jira rather than just typing instructions into Claude Code is to simulate and practice the real-world flow:
- In a real company, requirements come from a product team or business sponsor.
- They get translated into Jira issues.
- Developers pick up those issues and implement them.
- Claude Code should fit into *that* workflow — not replace it with something new.

**Alternative:** If you do not want to use Jira, GitHub Issues is a valid and simpler alternative that achieves much the same result.

---

### Creating a Free Jira Account

Jira offers a free plan for up to 10 users — no credit card required.

1. Go to `atlassian.com/software/jira`.
2. Click **Get it free**.
3. Sign up with Google auth or email.
4. Choose a site name (this becomes your Jira URL).
5. You will land on a screen showing **Spaces** (the new name for Jira Projects).

> **Navigation note:** In the Jira UI, "Spaces" is the new name for what used to be called "Jira Projects." There is also a "Projects" menu item which is a different, higher-level project management feature — not the same thing.

---

### Creating Your Jira Space and First Issue

**Creating a Space:**
1. Click **Create Space**.
2. Choose a software development template — **Kanban** is a standard choice.
3. Name the space (e.g., `pre-legal`).
4. Set the key prefix — this becomes the prefix on all issue IDs (e.g., `PL` → issue IDs become `PL-1`, `PL-2`, etc.).
5. Set access: **Team managed**, open to anyone with access to the site.
6. Click Create.

**Creating the First Issue:**
1. Click **Create**.
2. Enter the issue title (e.g., "We need a simple website that describes the pre-legal company").
3. The issue is created and assigned an ID (e.g., `PL-1`).
4. Click into it to see the detail view — it shows as a **Task** (the lowest level of granularity in Jira).

---

## 5. Connecting Claude Code to Jira via Atlassian MCP Server

### Installing the Atlassian MCP Server

The Atlassian MCP server is a **remote MCP server** — it runs in Atlassian's cloud, not on your local machine.

**Run this command in a terminal** (outside Claude Code):

```bash
claude mcp add atlassian --transport http https://mcp.atlassian.com/v1/mcp
```

Breaking this down:
- `claude mcp add` — tells Claude Code to register a new MCP server.
- `atlassian` — the name you're giving this server (used to reference it later).
- `--transport http` — specifies this is an HTTP-based remote MCP server.
- `https://mcp.atlassian.com/v1/mcp` — the official Atlassian MCP server endpoint.

After running, you will see: `Added to local config.`

---

### OAuth Authentication with Jira

Unlike most MCP servers where you pass an API key in the install command, the Atlassian MCP server uses **OAuth2 authentication** — a proper authorization flow that lets you log in via your Atlassian account without ever sharing your password.

**Steps to authenticate:**

1. Launch Claude Code: `claude`
2. Run: `/mcp`
3. You will see `atlassian` listed with a status of **"needs authentication"**.
4. Use the arrow keys to select it and press **Enter**.
5. Claude Code asks: *"Authenticate or Disable?"* → Select **Authenticate**.
6. A browser window opens automatically with an Atlassian authorization screen.
7. Click **Approve** → scroll down → click **Accept**.
8. The browser shows: *"Authentication successful. Return to Claude Code."*
9. Close the browser, return to Claude Code.

The Atlassian server now shows as **Connected** in `/mcp`.

---

### Dealing with Atlassian Re-Authentication (Known Issue)

**This is a well-known community complaint:** The Atlassian MCP server frequently loses its authentication state. When this happens, Claude Code will appear to hang indefinitely when trying to use Jira tools — it just sits there doing nothing.

**How to recognise it:** Claude Code is "thinking" but not making progress — tools calls appear to be stuck.

**How to fix it:**
1. Press `Escape` to interrupt.
2. Run: `/mcp`
3. Select the Atlassian server.
4. Press **Enter** → choose **Re-authenticate**.
5. Go through the browser approval flow again.
6. Return to Claude Code and retry.

**Practical implication:** You will likely need to re-authenticate at the start of every new Claude Code session or before every significant new task. Build this into your workflow as a regular first step when using Jira integration.

---

### Testing the Jira Connection

Once authenticated, test that Claude Code can read Jira:

```
Please tell me about Jira issue PL-1.
```

Claude will use the Atlassian MCP tools to fetch the issue and return its details — title, description, status, and more. If it returns the correct issue details, the connection is working.

---

## 6. Setting Up the GitHub Repository

### Creating the GitHub Repo

1. Go to `github.com` and click **New** (or the `+` button → New repository).
2. Name the repository: `pre-legal`.
3. Add a description: *"A platform for drafting common legal agreements."*
4. Set visibility: **Private** (until the project is ready to share).
5. Add a **README file** (so the repo has at least one file to clone).
6. Choose a license: **MIT** is standard for open projects.
7. Click **Create repository**.

---

### Generating a Fine-Grained Personal Access Token

Claude Code needs a GitHub token to interact with the repository on your behalf. Always use **fine-grained tokens** with minimal permissions — not classic tokens with broad access.

**Navigation path:**
`Avatar menu → Settings → scroll to Developer Settings (bottom left) → Personal access tokens → Fine-grained tokens → Generate new token`

**Token settings:**

| Setting | Value | Reason |
|---|---|---|
| **Name** | `for-mcp-server` | A reminder of what this token is for. |
| **Expiration** | 30 days | Good security practice — forces regular rotation. |
| **Repository access** | Only selected repositories → tick `pre-legal` | Limits blast radius if the token is ever leaked. |
| **Contents** | Read only | Claude needs to read files. |
| **Issues** | Read and write | For reading and creating GitHub issues. |
| **Pull requests** | Read and write | For creating and merging PRs. |

Click **Generate token** → review the permissions summary → confirm.

> **Critical:** The token is shown **only once** on the next screen. Copy it immediately to a safe location (plain text file or password manager). Do not paste it into Word or any app that might change quote characters — this will break the token.

---

### Cloning the Repo Locally

Once the token is saved, clone the new repository:

```bash
cd ~/projects
git clone https://github.com/yourusername/pre-legal.git
cd pre-legal
ls
# → LICENSE  README.md
```

Then open the `pre-legal` folder in VS Code:
- File → Open Folder → navigate to `pre-legal` → Open.
- Trust the authors when prompted.

---

## 7. Connecting Claude Code to GitHub via MCP Server

### Installing the GitHub MCP Server

The GitHub MCP server is also a **remote HTTP MCP server** — run by GitHub/Microsoft in the cloud.

**Run this in a terminal** (outside Claude Code, inside the `pre-legal` project directory):

```bash
claude mcp add github \
  --transport http \
  https://api.githubcopilot.com/mcp \
  --header "Authorization: Bearer YOUR_GITHUB_TOKEN_HERE"
```

Replace `YOUR_GITHUB_TOKEN_HERE` with the exact token you copied from GitHub (no modifications, no extra spaces). The command is in the course resources.

After running: `Added to local config.`

Launch Claude Code: `claude`

Run `/context` to verify the GitHub tools are now loaded — you should see a range of GitHub-related MCP tools in the context overview.

---

### Testing GitHub Integration — Creating an Issue and PR

**Test 1 — Create a GitHub Issue:**
```
Please write an issue to GitHub saying the README needs to be updated.
```

Claude will use the `create-or-update-issue` GitHub tool. After approving the tool use, check your GitHub repository → Issues → you should see the new issue: *"Update README."*

**Test 2 — Update the README and Raise a PR:**
```
Please update the README to reflect that the project is in progress and 
will be completed in one week. Then raise a PR for this to be merged.
```

What Claude does:
1. Reads the current README file.
2. Makes edits locally.
3. Commits the changes using `git commit`.
4. Pushes the branch to GitHub with `git push`.
5. Uses the GitHub MCP tool to open a Pull Request.

The resulting PR will show up in GitHub → Pull Requests, with a message like: *"Add status section to README — indicates project is in progress. Generated with Claude Code."*

**Merging the PR:**
Click **Merge pull request** → **Confirm merge** in GitHub. Then return to the terminal and switch back to the main branch:

```bash
git checkout main
git status
```

---

### Why Use MCP Servers Directly Instead of the Plugin?

A valid question at this point is: "You said to start with plugins — why are we installing MCP servers directly?"

The answer has two parts:

1. **These are among the most important and widely-used MCP servers.** Jira and GitHub are near-universal in professional development. It is worth knowing how to install them directly.

2. **Authentication requires the direct approach.** Both the Atlassian and GitHub MCP servers use OAuth or token-based authentication that needs to be configured at install time. Going through the plugin route for these specific servers would add an extra layer of abstraction that makes the authentication steps harder to understand and manage.

For most other use cases, start with plugins. For these two specific servers, direct MCP installation is the cleaner approach.

---

## 8. Installing the Feature Dev Plugin

### What is Feature Dev?

**Feature Dev** is an official Anthropic plugin that guides Claude Code through a **disciplined, seven-step process** for building a new feature. It was built by Anthropic for their own internal software development and has been open-sourced as a plugin.

The seven-step process includes:
1. **Read and understand the requirements** (e.g., read the Jira issue).
2. **Explore the codebase** to understand existing structure and conventions.
3. **Clarify ambiguities** — ask the developer specific questions before building anything.
4. **Architecture design** — plan the approach before writing code.
5. **Implementation** — write the actual code.
6. **Quality review** — review the code for issues (can use a code reviewer sub-agent).
7. **Raise a Pull Request** — commit and push all changes.

---

### Feature Dev vs Ralph Loops — The Spectrum of Autonomy

Feature Dev and Ralph Loops represent **opposite ends of the autonomy spectrum**:

```
← MORE CONTROL                               MORE AUTONOMY →

Feature Dev ──────────────────────────────── Ralph Loop
7-step disciplined      YOLO mode        Iterative chaos,
process, clarifying                      run N times,
questions, quality                       no guardrails
review baked in
```

| Aspect | Feature Dev | Ralph Loop |
|---|---|---|
| **Approach** | Rigorous, disciplined, methodical | Autonomous, iterative, exploratory |
| **Asks questions** | Yes — clarifies before building | No — just builds |
| **Quality review** | Built into step 6 | None |
| **Best for** | Production features, business requirements | Prototypes, MVPs, experiments |
| **Predictability** | High — follows a defined process | Low — output varies |
| **Human involvement** | Active — answers clarifying questions | Minimal — can walk away |

---

### How to Install Feature Dev

1. Open Claude Code and run: `/plugin`
2. Navigate to the **Discover** tab.
3. Find **Feature Dev** (it may not be the first listing).
4. Press **Enter** to read the description: *"Comprehensive feature development workflow with specialised agents for codebase exploration, architecture design, and quality review."*
5. Choose the installation scope:
   - **User scope** — installs just for you.
   - **Project scope** — installs for all collaborators on this repo (recommended for teams).
6. Select **Project scope** → press **Enter** to install.

After installation, a `.claude` directory is created in your project root containing the plugin configuration. This should be committed to GitHub so all collaborators automatically get the plugin.

---

## 9. Project Initialisation — Boilerplate and Git Ignore

Before starting real feature development, do some housekeeping to get the repo into proper shape. Ask Claude to handle this:

```
Please create a boilerplate .gitignore for this new project for typical 
Python, FastAPI, Next.js web app development. Then commit and push to GitHub.
```

What Claude does:
1. Creates a comprehensive `.gitignore` file covering Python, Node.js, Next.js, and common environment files.
2. Runs `git status` to review changes.
3. Runs `git pull` to sync with any remote changes (important after merging the earlier PR).
4. Runs `git add .` and `git commit -m "..."`.
5. Runs `git push` to push to GitHub.

**Critical check:** After the `.gitignore` is created, verify it contains a `*.env` entry. This ensures your secrets file is never accidentally committed to GitHub.

After this step, the GitHub repository should contain:
- `README.md` (updated with project status)
- `LICENSE`
- `.gitignore` (new, covering Python + Node.js)
- `.claude/` (containing the Feature Dev plugin configuration)

---

## 10. The Full Workflow — Jira Ticket to Merged PR

### Step 1 — Write a Good Jira Issue

The quality of a Jira issue directly affects the quality of what Claude builds. A good issue should:

- Have a **clear, action-oriented title**.
- Include a **detailed description** that explains *what* needs to be done (not how).
- Reference any **external resources** or data sources Claude should use.
- Be written as if a **non-technical product manager** wrote it — high-level, human-readable, without implementation details.
- Leave **some intentional ambiguity** in areas where Claude should ask clarifying questions (especially when using Feature Dev).

**Example of a good issue description format:**

```
This task is a one-time data curation project to prepare data for the 
pre-legal project.

For context, the Common Paper GitHub account at [link] contains repos 
with legal agreement templates that can be copied and modified under a 
CC license. We will use this as the source of data.

For this task we will need to:
- Browse these repos
- Pull down the Markdown files into a directory called /templates
- Create a JSON catalog file to describe the different templates
- Add a license file to recognize the Creative Commons license
```

---

### Step 2 — Task PL-2: Data Curation with Autonomous Problem-Solving

**The Issue:** Create a dataset of legal document templates from the Common Paper GitHub repository.

**The instruction to Claude Code:**
```
Please carry out Jira issue PL-2 and raise a PR with your changes.
```

This single instruction triggered a remarkable demonstration of autonomous problem-solving:

**What happened (and why it was impressive):**

1. Claude read the Jira issue via the Atlassian MCP tools.
2. It understood it needed to download Markdown files from a public GitHub repository.
3. It initially tried to use the GitHub MCP tools to fetch files — but then realised this approach was going to be **too slow** (it would pull large files into its context window one by one).
4. Rather than continuing down the slow path, Claude **stopped and switched strategy** — it decided to run shell commands to download the files directly. This is faster and more context-efficient.
5. It asked permission to run those download commands.
6. After running them, all template files appeared in the `templates/` directory instantly.
7. Claude then created a `catalog.json` file (as requested in the Jira issue) describing each template.
8. It added a `license.txt` file crediting the Creative Commons license.
9. It raised a Pull Request using the GitHub MCP tools.
10. When the Atlassian tools hung (authentication expired), Claude recognised the hang, stopped, waited for re-authentication, and completed the Jira status update.
11. When it found it lacked GitHub permissions to merge via the API, it found an alternative: **merge locally and push to main**.

> *"I'm continually completely astonished by Claude Code. It hit a roadblock, figured out what was going on, and found a workaround that was actually smarter than the original plan."*

**Key takeaway:** This kind of adaptive problem-solving — recognising when a strategy is inefficient and switching to a better one mid-task — is an example of what changed at the Claude Opus 4.5 inflection point in November 2025.

---

### Step 3 — Task PL-3: Building the NDA Creator App with Feature Dev

**The Issue (`PL-3`):** Build a prototype mutual NDA creator.

**The Jira description (intentionally high-level):**
```
A web application to create a mutual NDA document for a user.
The user enters some key information in a form.
The website then displays the mutual NDA with the key information filled in.
The user can download the completed document locally.
```

> **Note:** The download format is intentionally left unspecified. What format? What framework? These are left deliberately vague to see how Feature Dev's clarifying questions handle ambiguity.

---

### The Single Command That Does It All

With the Atlassian MCP server, GitHub MCP server, and Feature Dev plugin all configured, the entire development cycle is triggered by **one command**:

```
/feature-dev:feature-dev Please implement Jira issue PL-3 with a Next.js 
application in a directory called frontend. Then raise a PR when done.
```

Breaking this down:
- `/feature-dev:feature-dev` — invokes the Feature Dev plugin directly using its command syntax (plugin name:command name).
- The rest is the natural language instruction.
- Claude Code does everything else: reads the Jira issue, asks clarifying questions, designs the architecture, builds the code, reviews it, and raises the PR.

---

### The Feature Dev Seven-Step Process in Action

After running the command, Feature Dev executes its structured process. Here is what each step looked like in practice:

**Step 1 — Read Requirements:**
Claude used the Atlassian MCP tools to fetch issue `PL-3` and read the full description.

**Step 2 — Explore Codebase:**
Claude scanned the repo structure — finding the `templates/` directory from PL-2, the `catalog.json`, and the license file. This context informed the implementation.

**Step 3 — Clarifying Questions:**
Feature Dev stopped and presented a series of multiple-choice questions:

| Question | Options | Choice Made |
|---|---|---|
| What download format should the completed NDA be in? | PDF (recommended), DOCX, Plain text | **PDF** |
| Should the app use a single-step wizard or single page form? | Single page (recommended), Multi-step wizard | **Single page** |
| How should the NDA preview be displayed? | Below the form, Side by side | **Side by side** |
| Simple prototype or styling polish? | Functional prototype (recommended), Polish design | **Polish design** |

After answering all questions, the user pressed **Submit Answers**.

**Step 4 — Architecture Design:**
Claude planned the Next.js application structure before writing a single line of code.

**Step 5 — Implementation:**
Claude created the `frontend/` directory and built the full Next.js application:
```bash
cd frontend
npm run dev  # → working at localhost:3000
```

**Step 6 — Quality Review (was skipped — see section 11):**
This step was not completed automatically. It required a follow-up prompt.

**Step 7 — Raise a Pull Request:**
Claude used the GitHub MCP tools to push the branch and create a PR with a detailed description, commit summary, and attribution note: *"Generated with Claude Code."*

---

### Results — What Claude Built

**The application built in a single session, from one Jira ticket:**

A complete, functioning mutual NDA creator with:
- A **live-updating preview** — as you type in the form fields on the left, the NDA document on the right updates in real time. No "generate" button needed.
- A **PDF download button** that generates a clean, properly formatted PDF document.
- The PDF uses the **Common Paper Markdown templates** from PL-2 as the base.
- **Responsive layout** — side-by-side view on desktop.
- **Polished styling** — not a bare-bones prototype.

**Testing the output:**
- Fill in company names, governing law, key dates.
- The preview updates live with each keystroke.
- Download PDF → the PDF is formatted correctly with all filled-in fields, cover sheet, CC BY 4.0 attribution at the bottom.
- All details were correct on first run without any manual intervention.

> *"I can't tell you how remarkable it is that we could have something like this appear zero-shot just with an instruction and a Jira ticket."*

---

## 11. Closing the Loop — Tests, Code Review, and Merging

### Discovering a Skipped Step

After the NDA creator was working, a useful introspective prompt revealed that Feature Dev had **skipped Step 6 (Quality Review)**:

```
Based on the process you followed, what quality review or testing 
have you already taken care of?
```

Claude's honest answer:
- ✅ Build verification (confirmed it compiles and runs).
- ❌ No automated tests written.
- ❌ No manual testing documented.
- ❌ No code reviewer agents used.
- ❌ PDF download not specifically tested.

**Lesson:** Even with a structured seven-step plugin, Claude does not always complete every step autonomously. Always ask about what was skipped — especially testing and code review — before signing off on a feature.

---

### Triggering a Code Review and Tests

Once the skipped steps were identified, a single follow-up prompt addressed all of them:

```
Yes to all three. Please add extensive automated tests and manual tests, 
and have the code reviewer agents do the review.
```

What happened:
- Claude ran for over 10 minutes.
- It built an extensive test suite: **76 tests across 5 suites**.
- The context window filled up during this process, triggering an **auto-compact**.
- After compaction, Claude appeared momentarily confused but recovered and completed the job.
- All 76 tests passed.
- The application continued to work correctly after the tests were added.

**Key observation about auto-compact:**
When the context fills up mid-task and auto-compaction triggers, there is a nail-biting moment where Claude temporarily loses its thread. In most cases it recovers. But this is why manual `/compact` at natural stopping points is recommended — to avoid auto-compact happening in the middle of complex work.

---

### Final Merge and Jira Status Update

```
Please merge the PR locally and push to main, switch the branch to main, 
and mark this issue PL-3 done in Jira.
```

What Claude did:
1. Re-authenticated with Atlassian (this was required again).
2. Attempted to merge via the GitHub API → failed (no merge permissions on the token).
3. Switched strategy: merged the branch locally using `git merge` and pushed `main` directly.
4. Marked `PL-3` as **Done** in Jira.
5. Switched back to the main branch.

After this step:
- Jira board shows `PL-3` in the **Done** column.
- GitHub `main` branch contains the complete NDA creator.
- All tests pass.
- The full lifecycle is complete.

---

## 12. Debugging Strategies — A Disciplined Approach

Even with excellent tools and powerful models, bugs happen. Day 4 concludes with a recommended debugging framework — a structured approach for when Claude Code gets stuck or goes off track.

### Before You Debug — Take a Snapshot

**Before doing anything else when a bug appears:**

```bash
git add .
git commit -m "before debugging: <brief description of the bug>"
```

**Why this is critical:**
- Debugging sessions can go badly wrong — Claude may make things worse.
- The `/rewind` checkpoint system only undoes Claude's direct file edits. It cannot reverse side effects from scripts, installed packages, or database changes.
- A Git commit gives you a clean restore point that you can always return to with `git checkout`.

> *"Do a Git commit to start with. Don't just trust the rewind functionality."*

---

### Mode 1 — Quick Interactive Approach (Copy-Paste Loop)

**When to use:** For small, isolated bugs — things that "just seem bashed up against" something.

**How it works:**
1. Run the application or test.
2. Copy the full error message or stack trace.
3. Paste it directly into Claude Code — no explanation needed.
4. Claude usually understands the context from the paste alone.
5. It attempts a fix.
6. Run again.
7. If still broken, copy the new error and paste again.
8. Repeat.

**Why it works:** For simple problems, Claude has enough context from the error message to identify and fix the issue quickly. No verbose explanation is needed — the error message is the explanation.

**When to stop:** If after several cycles the problem is getting worse, or Claude keeps applying superficial patches without addressing the root cause, switch to Mode 2.

---

### Mode 2 — Disciplined Systematic Debugging

**When to use:**
- The quick copy-paste loop is making things worse.
- The bug is non-obvious or deep-rooted.
- Claude keeps going off on tangents.

**First action:** Revert to your last Git commit — wipe all the bad patches Claude applied and start from a clean state.

```bash
git checkout .    # revert all uncommitted changes
# or
git stash         # stash changes temporarily
```

---

### The Five-Step Debugging Process

This is the structured approach to apply when quick fixes fail. Guide Claude through each step explicitly, using a dedicated `debug.md` file to document everything.

#### Step 1 — Reproduce Consistently

```
Reproduce this issue consistently and document exactly how to trigger it. 
Write the reproduction steps to debug.md.
```

**Why this step matters:** If you cannot reproduce the bug consistently, you cannot verify whether a fix actually works. Claude must be able to trigger the bug on demand before attempting any fix.

#### Step 2 — Investigate and Gather Information

```
Now investigate deeply. Look at all related logs. Add extra logging if needed. 
Gather all the information you can. Document your findings in debug.md.
Also search the web for whether others have encountered similar issues.
```

**What to watch for during this step:**
- Extra logging reveals where execution is actually going wrong.
- Web searches can surface known issues with specific library versions.
- Documentation of findings in `debug.md` ensures nothing is lost if the context is later compacted.

#### Step 3 — Form and Document Hypotheses

```
Based on your investigation, form hypotheses for what could be causing this. 
Document all hypotheses in debug.md, ranked by likelihood.
```

Claude should write out multiple possible causes, not just the most obvious one.

**Sanity-check all hypotheses before proceeding.** See the warning about the "I Found It" trap below.

#### Step 4 — Identify and Prove the Root Cause

```
Based on your hypotheses, identify the most likely root cause. 
Then prove it — demonstrate that this root cause consistently 
causes the issue. Document your proof in debug.md.
```

**This is the most critical step.** Do not skip straight to fixing. Make Claude demonstrate the causal chain between the root cause and the symptom. If it cannot prove causation, the hypothesis is wrong.

#### Step 5 — Fix, Verify, and Document Lessons Learned

```
Now fix the root cause. Then verify that your fix consistently 
resolves the issue using the reproduction steps you documented. 
Finally, document lessons learned in claude.md so we don't repeat this.
```

The final part — documenting in `claude.md` — is crucial. After a compact or a `/clear`, Claude loses memory of the debugging session. If the same issue can recur, document its cause and the fix in `claude.md` so it stays in Claude's persistent memory.

---

### Critical Warning — The "I Found It" Hallucination Trap

One of the most dangerous debugging patterns with LLMs is the **confident false identification**. It goes like this:

1. Claude searches the web for the error message.
2. It finds a Stack Overflow post or GitHub issue from several years ago where someone reported a vaguely similar problem.
3. Claude declares: **"I found it. This is a known issue with [library]. The fix is to install a prior version of [package]."**
4. Claude then begins a large-scale refactoring based on this finding.
5. You discover later that the original post was a single person's edge-case from three years ago, no one responded to it, and the "fix" has nothing to do with your actual problem.

**The warning signs:**
- Claude says "I found it" or "this is a known issue" after a web search.
- The cited source is old (more than 1-2 years).
- Only one or two people reported the issue.
- No official acknowledgement or fix from the library authors.
- The proposed fix involves major structural changes (e.g., downgrading packages, rewriting whole components).

**How to challenge it:**

```
You found one reported incident of this issue. Do you have evidence 
this is a common, well-documented problem? How many people reported it? 
Is there an official fix? Is it really the same situation we have?
```

Force Claude to justify the strength of the evidence before it acts on the hypothesis. A single GitHub issue from three years ago is very weak evidence.

> *"When it latches onto that and starts rebuilding things, you're like 'no.' That is the moment when you stop it, restore from your last commit, and tell it: this is not the problem. Try again."*

**Known example of this pattern:** A specific false finding that has recurred multiple times is Claude claiming: *"An LLM cannot both have tool use and structured outputs in the same API call — this is a known issue."* This is fictional. The claim is not true and is not a documented issue with any major LLM API. But Claude will state it with total confidence and begin rewriting everything.

---

### Pro Tip — Use a Different LLM for Hard Problems

When Claude Code is completely stuck on a bug and all systematic debugging has failed, **switch to a different AI tool** for a fresh perspective:

Recommended options:
- **Codex** (OpenAI) via the VS Code plugin.
- **Gemini** via the Anti-gravity IDE or Gemini CLI.
- **GPT-4.1** via GitHub Copilot.

**Why this works:**
- Different models have been trained on different data with different objectives.
- They have different internal "blind spots" — a problem that one model consistently misdiagnoses may be immediately obvious to another.
- It is the AI equivalent of getting a second opinion.
- Especially effective for: *complex architectural bugs, subtle logic errors, and problems related to how specific libraries behave*.

> *"There is every chance a different model will discover something Claude has missed. Having multiple different LLMs — totally different prompts and training — work on the same problem is a pro tip for sure, particularly with really hard problems."*

---

### The Systematic Debugging Skill

There is an official community skill specifically for debugging, available through the skills marketplace:

**Skill name:** `systematic-debugging`

Key features of this skill:
- A detailed, step-by-step debugging process similar to the five steps above.
- Emphasis on exhaustive web searching.
- Heavy focus on finding and proving the **root cause** — called the **"Iron Rule"**: do not attempt a fix until the root cause is proven.
- Guides Claude through logging, investigation, and documentation with much more thoroughness than ad hoc debugging.

**To find and install it:**
1. Search for `systematic-debugging` in a skills marketplace (skills.sh or Anthropic's GitHub skills repo).
2. Install it into your `.claude/skills/` directory.
3. Reference it in your debugging prompts: `use systematic-debugging to diagnose this issue.`

This skill is highly recommended for any non-trivial bug that resists the quick copy-paste approach.

---

## 13. Key Takeaways — Day 4 Summary

### The End-to-End Workflow

The complete workflow demonstrated today is:

```
1. Create Jira issue (product/business requirement)
         ↓
2. Claude Code reads Jira issue (Atlassian MCP)
         ↓
3. Feature Dev plugin guides seven-step process
         ↓
4. Claude asks clarifying questions before building
         ↓
5. Claude builds the feature (Next.js app)
         ↓
6. Code review and tests (when prompted)
         ↓
7. GitHub PR created (GitHub MCP)
         ↓
8. PR merged, Jira issue marked Done
```

### One Command to Run the Whole Pipeline

```
/feature-dev:feature-dev Please implement Jira issue PL-3 with a Next.js 
application in a directory called frontend. Then raise a PR when done.
```

This single command — combining an MCP server (Jira), a plugin (Feature Dev), and another MCP server (GitHub) — is what "using Claude Code to the max" looks like.

### MCP Authentication Quick Reference

| Server | Auth Method | Common Issue | Fix |
|---|---|---|---|
| **Atlassian (Jira)** | OAuth2 — browser flow | Loses auth frequently | Run `/mcp` → Re-authenticate before each major task |
| **GitHub** | Personal Access Token in header | Permission denied on merge | Use local merge + push instead |

### Debugging Decision Tree

```
Bug appears
    │
    ▼
Git commit (snapshot!)
    │
    ▼
Mode 1: Copy-paste error into Claude
    │
    ├─ Fixed? → Done ✅
    │
    └─ Getting worse? → Revert to git commit
                              │
                              ▼
                        Mode 2: Disciplined debugging
                        (reproduce → investigate → hypotheses
                         → prove root cause → fix → document)
                              │
                              ├─ Fixed? → Document in claude.md ✅
                              │
                              └─ Still stuck? → Try a different LLM
```

### Key Rules to Remember

- **Always re-authenticate Atlassian** before starting a new task.
- **Always commit before debugging** — never rely on checkpoint rewind alone.
- **Always ask Claude what it skipped** — especially testing and code review.
- **Challenge "I Found It" claims** — demand evidence before Claude acts on a web-search hypothesis.
- **Document lessons in `claude.md`** — this is the only thing that survives compaction and context resets.
- **Use a different LLM** when Claude is genuinely stuck — it often finds what Claude missed.
- **Feature Dev skipping steps** is normal — it is not fully autonomous. Monitor it and prompt it to complete any skipped phases.

### The Write-Once Prompt Pattern

The most powerful takeaway from Day 4 is how much leverage a single, well-crafted prompt gets you when all the pieces are in place:

```
/feature-dev:feature-dev Please implement Jira issue [ID] 
with a [framework] application in a directory called [dir]. 
Then raise a PR when done.
```

This pattern — combining a task source (Jira), a development framework (Feature Dev), and a delivery target (GitHub PR) — is the foundation of a repeatable, scalable professional development workflow with Claude Code.

---

*End of Day 4 — Pro Week Notes*
