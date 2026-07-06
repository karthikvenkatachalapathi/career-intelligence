# Career Intelligence

A platform-agnostic AI-agent workflow for making better career decisions — not just producing more applications.

Career Intelligence helps an agent answer the strategic question first:

> Is this opportunity worth pursuing, and what is the right next action?

It works with Claude, ChatGPT, Cursor, Codex, Hermes, OpenCode, or any agent that can follow a Markdown instruction file.

## What this is for

Most AI job-search tools start too late in the process: they assume the job is worth applying to and begin generating materials.

This workflow adds the missing decision layer before application execution:

- identify promising roles,
- evaluate real fit beyond keyword overlap,
- preserve why a role is or is not worth pursuing,
- create opportunity packets only when useful,
- prepare for referrals, recruiter screens, and interviews,
- keep a tracker or scheduled discovery loop aligned with the underlying evidence.

The goal is **better career judgment**, not more application volume.

## Relationship to `ai-job-search`

Inspired by [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search).

| Project | Primary layer | Outcome |
|---|---|---|
| `ai-job-search` | Application execution | Helps tailor CVs, write cover letters, and move through application mechanics. |
| `career-intelligence` | Decision intelligence | Helps decide whether, why, and how to pursue an opportunity before generating artifacts. |

In short:

> `ai-job-search` helps you apply better once a role is worth pursuing.  
> `career-intelligence` helps decide what deserves pursuit in the first place.

## Core workflow modes

The agent classifies each request before acting:

| Mode | Outcome |
|---|---|
| `scan` | Find credible opportunities from approved sources. |
| `evaluate` | Decide whether a role is worth pursuing and why. |
| `apply` | Create truthful application materials after the role clears the bar. |
| `prep` | Prepare for recruiter calls, referrals, screens, and interviews. |
| `upskill` | Compare target roles against current evidence and gaps. |
| `status` | Report where an opportunity stands and the next action. |

This prevents every job link from becoming a resume-generation task.

## What it produces

Depending on the mode, the workflow can produce:

- a fit recommendation,
- a role/company risk assessment,
- an opportunity packet,
- source-link capture,
- referral or recruiter-screen prep,
- ATS/resume/cover-letter artifacts when justified,
- tracker updates,
- scheduled discovery candidates.

Opportunity packets are created by the agent using:

```text
templates/opportunity-packet-template.md
```

The user should not manually create every packet file. The agent creates only what the mode requires.

## Automation philosophy

Cloning this repo does **not** install cron jobs, authenticate LinkedIn, create trackers, or apply to jobs.

Those are optional integrations.

When added, automation should support judgment rather than replace it:

```text
scheduled discovery
  -> find candidate roles
  -> dedupe against existing packets/tracker rows
  -> create review candidates
  -> update tracker
  -> notify only when attention is needed
```

It should not auto-apply by default.

## Quick start

For the guided setup, use:

[SETUP.md](SETUP.md)

The one required workflow file is:

```text
skills/career-intelligence/SKILL.md
```

Give it to your agent and say:

```text
Use the Career Intelligence workflow. First classify my request as scan, evaluate, apply, prep, upskill, or status. Then follow that mode.
```

Example first prompt:

```text
Use the Career Intelligence workflow in evaluate mode for this role: <JOB_URL>. Tell me whether it is worth pursuing, why, what risks exist, and the next action. Do not generate resume or cover-letter material yet.
```

## Files

```text
README.md                                # Strategy and outcome overview
SETUP.md                                 # Guided implementation walkthrough
skills/career-intelligence/SKILL.md      # Canonical agent workflow
examples/prompts.md                      # Copy/paste prompts
templates/opportunity-packet-template.md # Agent-created packet starter
CONTRIBUTING.md
LICENSE
```

## License

MIT License. See [LICENSE](LICENSE).
