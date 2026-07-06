# Career Intelligence Workflow

This is the platform-agnostic version of the Career Intelligence skill.

Use it with any AI agent that can follow reusable instructions: Claude, ChatGPT, Cursor, Codex, Hermes, OpenCode, local agents, or a custom workflow runner.

The canonical instruction file is also available at:

```text
skills/career-intelligence/SKILL.md
```

Both files describe the same operating model. Use whichever shape your agent platform prefers.

---

## Short operating instruction

When a user gives you a career-related request, do not immediately generate application materials.

First classify the request as one of:

- `scan`
- `evaluate`
- `apply`
- `prep`
- `upskill`
- `status`

Then follow the matching workflow in `skills/career-intelligence/SKILL.md`.

Core rule:

> Treat career planning as an intelligence workflow, not just an application workflow.

A job posting is not automatically an application task. It may be a research task, a qualification task, a referral task, an interview-prep task, a status task, or a pass.

The workflow can also be paired with scheduled automation:

```text
cron / scheduled agent -> find relevant job links -> dedupe -> add to review queue -> update live tracker/spreadsheet
```

That automation should reduce discovery and tracking effort, not blindly apply to jobs.

---

For the full workflow, see `skills/career-intelligence/SKILL.md`.
