# Guided setup

This repo is intentionally inert when cloned.

Cloning it does **not**:

- install an AI agent,
- configure a cron job,
- authenticate LinkedIn,
- create a spreadsheet or database,
- write to your private career workspace,
- apply to jobs.

That keeps the public repo safe and portable. The repo gives you the workflow; you decide which agent, tracker, and automation pieces to connect.

## Setup path

You can stop after Step 2 if you only want the manual workflow.

| Step | Required? | What it enables |
|---|---:|---|
| 1. Clone the repo | Yes | Local copy of the workflow. |
| 2. Add the workflow to your AI agent | Yes | Manual scan/evaluate/apply/prep/status workflow. |
| 3. Create a private workspace | Recommended | Durable opportunity packets. |
| 4. Add a tracker | Optional | Spreadsheet/database dashboard. |
| 5. Add LinkedIn MCP | Optional | LinkedIn as a first-class source. |
| 6. Add scheduled discovery | Optional | Automatic discovery + tracker updates. |

## 1. Clone the repo

```bash
git clone https://github.com/karthikvenkatachalapathi/career-intelligence.git
cd career-intelligence
```

## 2. Add the workflow to your AI agent

The canonical instruction file is:

```text
skills/career-intelligence/SKILL.md
```

Use it with any agent:

| Agent | Setup |
|---|---|
| Claude / ChatGPT | Upload or paste `skills/career-intelligence/SKILL.md` into a project or custom instructions. |
| Cursor / Codex / OpenCode | Keep the repo in your workspace and tell the agent to follow `skills/career-intelligence/SKILL.md`. |
| Hermes / skill-based agents | Copy `skills/career-intelligence/` into the agent's skills directory. |
| Other agents | Paste `SKILL.md` as reusable instructions. |

Test prompt:

```text
Use the Career Intelligence workflow in evaluate mode for this role: <JOB_URL>. Tell me whether it is worth pursuing, why, what risks exist, and the next action. Do not generate resume or cover-letter material yet.
```

## 3. Create your private workspace

Create a private folder outside this public repo:

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

When a role is worth tracking, the **agent should create the opportunity packet** using:

```text
templates/opportunity-packet-template.md
```

The user should not manually create every packet file. Normal flow:

```text
user or automation finds a role
  -> agent evaluates it
  -> agent creates <Company> - <Role>/START HERE.md
  -> agent creates only the additional artifacts required by the mode
  -> user reviews/corrects evidence
```

## 4. Add a tracker

A tracker is optional. It can be a spreadsheet, Airtable, Notion database, SQLite database, or project board.

Recommended columns:

```text
Company | Role | Status | Fit Score | Source URL | Company Careers URL | LinkedIn URL | Next Action | Last Updated
```

Rule of thumb:

- Packet = source of truth.
- Tracker = dashboard.

## 5. Add LinkedIn MCP as a first-class source

LinkedIn is optional. If you run a LinkedIn MCP server separately, treat it as a source channel in the `scan` pipeline.

Example MCP server config:

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

What happens after configuration depends on your agent runtime and the MCP server behavior.

Expect a separate authentication step the first time the LinkedIn server needs an authenticated session. That may involve browser login, cookies, or whatever flow the MCP server supports. This repo does not start that login automatically.

Use LinkedIn MCP to capture:

- LinkedIn job URL,
- company,
- role title,
- location / work model,
- posted date if available,
- recruiter or poster context when available,
- verified direct company careers link when possible.

Then route the role into `evaluate` mode.

## 6. Add scheduled discovery

Scheduled discovery is optional. It is not created automatically by this repo.

Use your scheduler of choice: cron, GitHub Actions, a local agent scheduler, Hermes cron, Airflow, a small script, or another workflow runner.

Recommended behavior:

```text
scheduled job
  -> scan approved sources, including LinkedIn MCP if configured
  -> extract company, role, URL, location, compensation, and source
  -> dedupe against existing packets and tracker rows
  -> create a packet in 01 - Not Reviewed only when worth tracking
  -> update the live tracker
  -> notify only for high-signal roles or required user decisions
```

Do **not** auto-apply by default.

The scheduled job should reduce discovery and tracking work. It should not make career decisions without review.

## Setup checklist

- [ ] Repo cloned.
- [ ] `skills/career-intelligence/SKILL.md` added to your agent.
- [ ] Private `Career Intelligence/` workspace created.
- [ ] Test `evaluate` prompt works on one job URL.
- [ ] Tracker created, if desired.
- [ ] LinkedIn MCP configured, if desired.
- [ ] LinkedIn authentication completed, if required by your MCP server.
- [ ] Scheduled discovery configured, if desired.
- [ ] Scheduled job tested with a dry run before enabling writes.

## Suggested first run

Use one job URL and ask:

```text
Use the Career Intelligence workflow in evaluate mode.
Use my private Career Intelligence workspace as the packet root.
Create an opportunity packet only if this role is worth tracking.
Do not create application materials yet.

Job URL: <JOB_URL>
```

Expected result:

- The agent classifies the role.
- If worth tracking, it creates or proposes a packet.
- It writes `START HERE.md` first.
- It recommends the next action.
- It does not generate a resume or cover letter unless the role clears the threshold and you ask for apply mode.
