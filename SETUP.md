# Guided setup

This setup is written for anyone who wants a repeatable career-intelligence system for **any job, in any country, on any job board**.

The workflow has three required parts:

1. an AI agent that follows the Career Intelligence instructions,
2. a private workspace where job packets and artifacts are stored,
3. a scheduled discovery job that runs automatically and keeps a tracker current.

Cloning this repo does **not** install or connect those pieces automatically. The repo gives you the instructions and examples; your agent/runtime connects them.

## Mental model

```text
Scheduled discovery runs every day
  -> finds jobs from your approved sources
  -> removes duplicates
  -> creates/updates a job packet
  -> updates your tracker
  -> tells you what needs a decision

You review promising roles
  -> weak roles stay research-only or are marked pass
  -> strong roles get application artifacts
  -> interview-stage roles get prep artifacts
```

## Setup path

| Step | Required? | What it enables |
|---|---:|---|
| 1. Clone the repo | Yes | Local copy of the workflow. |
| 2. Add the workflow to your AI agent | Yes | Manual evaluation and artifact generation. |
| 3. Create a private workspace | Yes | Durable job packets and artifact storage. |
| 4. Create a tracker | Recommended | Simple dashboard for all jobs. |
| 5. Configure discovery sources | Yes | Any-country, any-job-board inputs. |
| 6. Add scheduled discovery | Recommended | Automatic scans and tracker updates. |
| 7. Add LinkedIn or other authenticated sources | Recommended | Better coverage where supported. |

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

When a role is worth tracking, the **agent creates the opportunity packet** using:

```text
templates/opportunity-packet-template.md
```

You should not manually create every packet file. Normal flow:

```text
scheduled discovery or user finds a role
  -> agent evaluates it
  -> agent creates <Company> - <Role>/START HERE.md
  -> agent creates only the additional artifacts required by the stage
  -> tracker is updated
  -> user reviews/corrects evidence
```

## 4. Create a tracker

A tracker is required because scheduled discovery needs a simple place to record what it found.

Use whatever you already understand:

- Google Sheets,
- Excel,
- Airtable,
- Notion database,
- SQLite,
- a Markdown table,
- a project board.

Minimum columns:

```text
Company | Role | Status | Fit Score | Country/Region | Location | Remote/Hybrid/Onsite | Source URL | Company Careers URL | Date Found | Last Checked | Next Action | Artifact Status
```

Recommended status values:

```text
Not Reviewed | Interested | Applied | Interview | Offer | On Hold | Not Interested | Rejected
```

Rule of thumb:

- Packet = source of truth.
- Tracker = easy dashboard.
- Scheduled discovery updates both.

## 5. Configure discovery sources

Scheduled discovery can work anywhere in the world if you define sources clearly.

Start with a small list. Add more later.

```text
sources:
  - LinkedIn job search URL for your target role/location
  - direct company careers page
  - Greenhouse / Lever / Workday / Ashby / SmartRecruiters board
  - local country-specific job board
  - remote-work board
  - recruiter newsletter or RSS feed
```

For global use, always capture:

```text
Country/Region | City | Time zone if relevant | Work model | Visa/sponsorship note if visible | Salary currency if posted
```

The workflow should not assume US-only job boards, US-only resumes, or one naming convention for CV/resume documents.

## 6. Add scheduled discovery

Scheduled discovery is **required** for this workflow. Without it, you still have useful prompts, but you do not have the full Career Intelligence system.

### Recommended frequency

Start here:

| Schedule | Use when |
|---|---|
| Every 6 hours | Active search, fast-moving market, multiple countries/time zones. |
| Daily at 8 AM | Normal default for most users. |
| Twice weekly | Passive monitoring. |

### What the scheduled job must do

```text
scheduled discovery job
  -> scan configured sources
  -> extract company, role, country, location, work model, compensation, URL, and source
  -> dedupe against existing packets and tracker rows
  -> create or update a packet in 01 - Not Reviewed
  -> update the tracker
  -> record when it ran
  -> report only new high-signal roles, blockers, or failures
```

Do **not** auto-apply by default.

The scheduled job should create or update folders under:

```text
Career Intelligence/01 - Not Reviewed/
```

If the tracker says a role exists but no packet exists, the job is incomplete.

## 7. Add LinkedIn or other authenticated sources

LinkedIn is optional as a source, but discovery itself is not optional.

If you run a LinkedIn MCP server separately, treat it as one source channel in the `scan` pipeline.

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

Expect a separate authentication step the first time the LinkedIn server needs an authenticated session. That may involve browser login, cookies, or whatever flow the MCP server supports. This repo does not start that login automatically.

## When artifacts are created

The workflow creates artifacts only when they are useful for the current stage.

| Stage / status | Create these artifacts | Do not create yet |
|---|---|---|
| Not Reviewed | `START HERE.md`, source posting, basic fit notes | Resume, cover letter, interview prep |
| Interested | Fit analysis, employer intelligence, role intelligence, gap analysis, application strategy | Final resume/CV unless applying soon |
| Applying / Applied | Job-specific resume or CV, cover letter, ATS keyword analysis, tailoring change log | Interview prep unless an interview is scheduled |
| Referral / recruiter screen | Referrer blurb, recruiter message, 60-second pitch, proof points | Full interview packet unless needed |
| Interview | Interview prep packet, story bank, questions to ask, red flags to qualify | New resume rewrite unless the JD changed |
| Offer | Offer comparison, negotiation notes, risk analysis | New application materials |
| Not Interested / Rejected | Status note only | Any new artifacts |

Simple rule:

```text
Every job gets tracking.
Promising jobs get packets.
Apply-stage jobs get resume/CV + cover letter.
Interview-stage jobs get interview prep.
Closed jobs get no new artifacts.
```

For international jobs:

- Use `resume` when that is expected by the market.
- Use `CV` when that is expected by the market.
- Preserve local conventions unless the user asks otherwise.
- Track salary currency, country, location, visa/sponsorship requirements, and work model.

## Setup checklist

- [ ] Repo cloned.
- [ ] `skills/career-intelligence/SKILL.md` added to your agent.
- [ ] Private `Career Intelligence/` workspace created.
- [ ] Tracker created.
- [ ] Discovery sources listed.
- [ ] Scheduled discovery configured.
- [ ] Scheduled discovery tested with a dry run before enabling writes.
- [ ] `discovery.log` created and readable.
- [ ] Tracker `Last Checked` updates after a scheduled run.
- [ ] Packets appear in `01 - Not Reviewed` when new roles are found.
- [ ] LinkedIn or other authenticated sources configured if desired.

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
- It does not generate a resume, CV, or cover letter unless the role clears the threshold and you ask for apply mode.
