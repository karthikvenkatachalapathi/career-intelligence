# Career Intelligence Skill

A platform-agnostic AI-agent workflow for helping people make better career decisions in a difficult tech market.

Use it with Claude, ChatGPT, Cursor, Codex, Hermes, OpenCode, local agents, or any system that supports reusable instructions. There is nothing platform-specific in the workflow: it is just structured operating guidance an agent can follow.

## Why this exists

A lot of AI job-search tooling focuses on speed:

- find more roles
- generate more resumes
- write more cover letters
- send more applications

That can help, but it is not always the highest-leverage problem.

In a market shaped by layoffs, reorganizations, slower hiring cycles, and unclear role expectations, many people need better judgment before they need more output.

The useful questions are often:

- Is this opportunity actually worth pursuing?
- Is the fit real, or just keyword overlap?
- What evidence supports the candidate's fit?
- What risks or gaps should be understood before investing time?
- Should this become a referral conversation, interview prep, application work, or a pass?
- How do you preserve the decision trail so you do not restart from zero every time?

This skill turns career planning into a repeatable intelligence workflow instead of an application factory.

## Credit and inspiration

This work was influenced by [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search), an open-source AI-powered job application framework built around Claude Code.

`ai-job-search` is strong at helping with the mechanics of applying: evaluating roles, tailoring CVs, writing cover letters, and preparing for interviews.

This skill operates one layer earlier and one layer wider.

The distinction:

> `ai-job-search` helps with the mechanics of applying.  
> Career Intelligence helps decide whether, why, and how to pursue an opportunity in the first place.

## What makes this different

| Layer | Application-oriented workflow | Career Intelligence workflow |
|---|---|---|
| Primary focus | Applying well | Deciding what deserves effort |
| Main question | “How do I apply?” | “Should I pursue this, and what is the right next step?” |
| Default behavior | Produce application materials | Classify the decision first, then act only as needed |
| Output | CV, cover letter, interview prep | Career packet: fit, evidence, employer context, risks, questions, referral strategy, status, and artifacts |
| Time horizon | Application moment | Full opportunity lifecycle |
| Differentiator | Execution speed | Judgment, gates, evidence, continuity |
| Automation layer | Usually user-initiated application work | Optional scheduled scans that find relevant job links, create review candidates, and update a live tracker/spreadsheet |

## Core idea

Not every opportunity should become an application.

Some deserve a quick screen.  
Some deserve deeper evaluation.  
Some deserve a referral qualification question.  
Some deserve interview prep.  
Some should be closed out quickly.

The skill routes work into the narrowest useful mode before generating artifacts.

## Workflow modes

| Mode | Use when | What the agent should do |
|---|---|---|
| `scan` | Looking for roles or market themes | Find high-signal opportunities, dedupe, and shortlist only credible matches. |
| `evaluate` | Deciding whether something is worth pursuing | Assess fit, evidence, risks, employer context, gaps, and next action. Do not create application materials by default. |
| `apply` | The opportunity clears the bar | Create tailored application artifacts from verified evidence only. |
| `prep` | A recruiter screen, referral conversation, hiring-manager call, or interview is coming up | Build pitch, story bank, questions, risks, and conversation guidance. |
| `upskill` | Comparing target roles against current evidence | Identify skill gaps and evidence-building priorities. |
| `status` | Checking where an opportunity stands | Report status and next action without regenerating artifacts. |

## What a career packet can include

For serious opportunities, the workflow creates or updates a structured career packet.

```text
START HERE.md
00 - Source Job Posting.md
01 - Job Fit Analysis.md
02 - Employer Intelligence.md
02A - Employee Sentiment.md
03 - Role Intelligence.md
04 - Gap Analysis and Development Plan.md
05 - ATS Keyword Analysis.md
06A - Tailoring Change Log.md
08 - Application Strategy.md
09 - Referral Screen Messages and ATS Resume.md
10 - Questions to Ask Employer.md
11 - Interview Prep Packet.md
```

Use any storage system you prefer: Markdown folders, Notion, Google Docs, a database, a spreadsheet, a project-management tool, or plain files.

The key is not the tool. The key is preserving the reasoning, evidence, and next action.

## Optional automation layer

This workflow also supports scheduled automation.

A lightweight cron job or scheduled agent can run without manual prompting to:

1. search selected sources for relevant job links,
2. deduplicate roles already seen,
3. add promising roles to a review queue,
4. create starter packets when useful,
5. update a live spreadsheet or tracker with status, links, fit signals, and next actions.

The automation should not blindly apply to jobs. Its job is to reduce discovery and tracking friction:

> find relevant links automatically, preserve them in the workflow, and keep the live tracker current.

The human or agent can then evaluate, apply, prep, or pass using the same Career Intelligence modes.

Typical scheduled setup:

```text
cron / scheduled agent
  -> scan approved job sources
  -> extract company, role, URL, location, compensation, and source
  -> dedupe against existing packets and tracker rows
  -> add new candidates to Not Reviewed
  -> update spreadsheet / tracker live view
  -> alert only when something needs attention
```

This makes the tracker an operational dashboard rather than a manually maintained spreadsheet.

## How to use it with any AI agent

### Claude Projects / Claude Desktop / Claude Code

Add `career-intelligence-workflow.md` or `skills/career-intelligence/SKILL.md` to your project knowledge or skill folder. Tell Claude:

```text
Use the Career Intelligence workflow. First classify the request as scan, evaluate, apply, prep, upskill, or status. Then follow that mode.
```

### ChatGPT / custom GPTs

Paste the workflow into custom instructions or a project file. Use prompts such as:

```text
Use the Career Intelligence workflow in evaluate mode for this role. Do not generate resume or cover-letter content unless the fit clears the threshold.
```

### Cursor / Codex / OpenCode / other coding agents

Keep the workflow file in the repository and reference it in your agent instructions:

```text
Follow career-intelligence-workflow.md for all career-opportunity analysis. Default to decision quality over application volume.
```

### Hermes or other skill-based agents

Copy the `skills/career-intelligence/` folder into the agent's skill directory, or paste the workflow into the agent's reusable instruction system.

## Quick-start prompts

### Evaluate a role

```text
Use the Career Intelligence workflow in evaluate mode for this job posting. Assess whether it is worth pursuing, what evidence supports the fit, what risks exist, and what should be clarified before investing more time.
```

### Prepare for a recruiter screen

```text
Use the Career Intelligence workflow in prep mode. Build a recruiter-screen prep packet with a 60-second pitch, must-ask questions, compensation/work-model clarification wording, and risks to qualify.
```

### Create application artifacts

```text
Use the Career Intelligence workflow in apply mode. Tailor materials only from verified evidence. Include a change log and reviewer pass.
```

### Build a referral blurb

```text
Use the Career Intelligence workflow to create a referrer talking blurb for this role. Keep it factual, concise, role-specific, and written in language a referrer could credibly use.
```

## What to customize

Before using it seriously, customize:

1. **Target lanes** — role families, functions, industries, or stages that matter.
2. **Hard filters** — compensation, work model, location, travel, level, company stage, or other non-negotiables.
3. **Evidence base** — resume, project history, portfolio, writing samples, performance notes, or case studies.
4. **Decision thresholds** — what score or conditions justify deeper research, referral effort, tailored materials, or interview prep.
5. **Packet structure** — where the agent should save analysis, status, questions, and artifacts.

## Design principles

- Evidence before optimization.
- Decision quality over application volume.
- Career trajectory over keyword matching.
- Generate only the artifacts that are actually needed.
- Label uncertainty clearly.
- Do not invent accomplishments, metrics, relationships, technologies, dates, or credentials.
- Preserve context so the process can continue over time.

## Repository contents

```text
README.md
career-intelligence-workflow.md
skills/career-intelligence/SKILL.md
examples/prompts.md
templates/career-packet-template.md
CONTRIBUTING.md
LICENSE
```

`career-intelligence-workflow.md` and `skills/career-intelligence/SKILL.md` contain the same core workflow. The duplicate path exists so different agent platforms can consume whichever shape is easiest.

## License

MIT License. See [LICENSE](LICENSE).
