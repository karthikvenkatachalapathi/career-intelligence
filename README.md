# Career Intelligence

A simple, platform-agnostic workflow for using an AI agent to decide which career opportunities are actually worth pursuing.

It works with Claude, ChatGPT, Cursor, Codex, Hermes, OpenCode, or any agent that can read a Markdown instruction file.

## Credit and relationship to `ai-job-search`

This repo was inspired by [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search).

The difference is the operating layer:

| Project | Primary job | Best for |
|---|---|---|
| `ai-job-search` | Application execution | Tailoring CVs, writing cover letters, preparing for interviews, and moving through application mechanics. |
| `career-intelligence` | Career decision intelligence | Deciding whether a role deserves effort, preserving fit rationale, tracking opportunities, qualifying referrals, and routing work into scan/evaluate/apply/prep/status modes. |

Put simply:

> `ai-job-search` helps you apply better once you know the role is worth pursuing.  
> `career-intelligence` helps you decide what is worth pursuing, why, and what the next action should be.

This repo also treats discovery and tracking as first-class workflow pieces: scheduled scans can find job links, LinkedIn MCP can be a native source, and a live tracker can mirror opportunity status.

## Start here

Cloning this repo does **not** automatically install cron jobs, authenticate LinkedIn, create trackers, or apply to jobs. It is a portable workflow package.

For a step-by-step onboarding path, use [SETUP.md](SETUP.md).

The one required workflow file is:

```text
skills/career-intelligence/SKILL.md
```

That is the canonical workflow. Give it to your AI agent and say:

```text
Use the Career Intelligence workflow. First classify my request as scan, evaluate, apply, prep, upskill, or status. Then follow that mode.
```

## 3-minute setup

### 1. Clone the repo

```bash
git clone https://github.com/karthikvenkatachalapathi/career-intelligence.git
cd career-intelligence
```

### 2. Add the workflow to your agent

Pick one:

| Agent | What to do |
|---|---|
| Claude / ChatGPT | Upload or paste `skills/career-intelligence/SKILL.md` into project/custom instructions. |
| Cursor / Codex / OpenCode | Keep the repo in your workspace and tell the agent to follow `skills/career-intelligence/SKILL.md`. |
| Hermes / skill-based agents | Copy `skills/career-intelligence/` into the agent's skills directory. |
| Any other agent | Paste `skills/career-intelligence/SKILL.md` as reusable instructions. |

### 3. Give it one of these prompts

```text
Use the Career Intelligence workflow in evaluate mode for this job: <JOB_URL>. Tell me if it is worth pursuing, why, what risks exist, and the next action. Do not create resume or cover-letter material yet.
```

```text
Use the Career Intelligence workflow in prep mode. I have a recruiter screen for <ROLE> at <COMPANY>. Build my pitch, likely questions, risks to clarify, and questions to ask.
```

```text
Use the Career Intelligence workflow in apply mode. Tailor materials only from verified evidence. Include a change log and do not invent experience.
```

## What it does

The workflow stops an AI agent from treating every job link as an application task.

It first chooses the right mode:

| Mode | Use it for |
|---|---|
| `scan` | Find promising roles. |
| `evaluate` | Decide whether a role is worth pursuing. |
| `apply` | Create truthful application materials after the role clears the bar. |
| `prep` | Prepare for recruiter calls, referrals, screens, or interviews. |
| `upskill` | Compare target roles against your current evidence. |
| `status` | Check where an opportunity stands. |

## Recommended workspace

Create a private folder outside this public repo for your actual job materials:

```text
Career Intelligence/
  01 - Not Reviewed/
  02 - Interested/
  03 - Applied/
  04 - Interview/
  05 - Offers/
  06 - On Hold/
  99 - Not Interested/
  100 - Rejected/
  DOCX Versions/
```

When a serious opportunity is worth tracking, the **agent should create the packet** using `templates/opportunity-packet-template.md`.

The user should not have to manually create every file. The normal flow is:

```text
user or scheduled scan finds a role
  -> agent evaluates whether it is worth tracking
  -> agent creates <Company> - <Role>/START HERE.md
  -> agent adds only the extra files required by the mode
```

Example packet:

```text
<Company> - <Role>/
  START HERE.md
  00 - Source Job Posting.md
  01 - Job Fit Analysis.md
  02 - Employer Intelligence.md
  ...only if needed
```

You do not need every file for every role. Generate only what the mode requires.

## Optional: live tracker

You can mirror packet status into a spreadsheet, Airtable, Notion database, or other tracker.

Recommended tracker columns:

```text
Company | Role | Status | Fit Score | Source URL | Company Careers URL | Next Action | Last Updated
```

The packet should remain the source of truth. The tracker is the dashboard.

## Optional: scheduled job discovery

This is not set up automatically. See [SETUP.md](SETUP.md) for the guided path.

Typical pipeline:

```text
cron / scheduled agent
  -> scan approved job sources
  -> extract company, role, URL, location, compensation, and source
  -> dedupe against existing packets and tracker rows
  -> add new roles to 01 - Not Reviewed
  -> update the live tracker
  -> alert only when something needs attention
```

This should not auto-apply. It should only reduce discovery and tracking work.

## Optional: LinkedIn as a first-class source

This is not authenticated automatically. If you run a LinkedIn MCP server separately, treat LinkedIn as a native source in the scan pipeline, alongside company career pages and job boards.

Example MCP config:

```json
{
  "linkedin": {
    "command": "uvx",
    "args": [
      "linkedin-scraper-mcp@latest",
      "--tool-timeout",
      "300"
    ],
    "env": {
      "UV_HTTP_TIMEOUT": "300",
      "LOG_LEVEL": "INFO"
    }
  }
}
```

Use it to capture:

- LinkedIn job URL
- company
- role title
- location / work model
- posted date if available
- recruiter or poster context when available
- direct company careers link when you can verify it

Then feed the result into `evaluate` mode. LinkedIn discovery should create review candidates, not automatic applications.

## Files in this repo

```text
README.md                                # Start here
SETUP.md                                 # Guided setup walkthrough
skills/career-intelligence/SKILL.md      # Canonical workflow instructions
examples/prompts.md                      # Copy/paste prompts
templates/opportunity-packet-template.md   # Agent-created packet starter template
CONTRIBUTING.md
LICENSE
```

## License

MIT License. See [LICENSE](LICENSE).
