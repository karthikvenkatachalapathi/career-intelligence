---
name: career-intelligence
description: Use when evaluating career opportunities, job postings, referrals, recruiter conversations, interviews, offers, rejections, or application artifacts. Classifies the request, assesses evidence-based fit, preserves decision context, and creates truthful career materials only when justified.
version: 1.3.0
license: MIT
---

# Career Intelligence Workflow

## Purpose

Use this workflow to help a person make better career decisions with an AI agent.

It is platform-agnostic. It can run inside Claude, ChatGPT, Cursor, Codex, Hermes, OpenCode, a local agent, or any other system that can follow reusable instructions.

The goal is not to maximize job applications. The goal is to improve decision quality:

- Should this opportunity be pursued?
- Is the fit real or just keyword overlap?
- What evidence supports the candidate's fit?
- What risks or gaps should be clarified?
- What is the right next action?
- Which artifacts are actually needed?

## Core rules

1. **Classify before acting.**
   - Pick the narrowest workflow mode that satisfies the request.
   - Do not turn every request into resume or cover-letter generation.

2. **Use evidence before optimization.**
   - Use only verified candidate evidence.
   - Do not invent experience, accomplishments, metrics, certifications, technologies, employers, dates, responsibilities, relationships, or referrals.
   - If evidence is missing, say so.

3. **Treat fit as trajectory, not keywords.**
   - Evaluate level, scope, domain, compensation, location, work model, growth, and long-term direction.
   - Do not assume keyword overlap means strategic fit.

4. **Preserve decision context.**
   - For serious opportunities, create or update a durable packet.
   - The agent should create the packet automatically when a role is worth tracking; the user should only provide or correct evidence.
   - Capture source links, rationale, risks, status, questions, and next action.

5. **Generate artifacts only when justified.**
   - Resume, CV, cover-letter, referral, or interview artifacts should follow the mode and threshold.
   - If a role is weak or unclear, recommend research, qualification, or pass instead of generating polished documents.

6. **Scheduled discovery is part of the system.**
   - The complete workflow requires a scheduled scan plus a tracker.
   - Manual one-off evaluation is allowed, but label it as manual mode rather than the full Career Intelligence system.
   - The scheduled job must update tracker state, packet state, and last-run evidence.

## Workflow modes

Before doing anything else, classify the request into one mode.

| Mode | Trigger examples | Expected behavior |
|---|---|---|
| `scan` | “Find roles,” “scan job boards,” “what should I look at?” | Search high-signal global sources, dedupe, and shortlist only credible matches. |
| `evaluate` | Job link, JD, company page, “is this worth it?” | Build or update fit analysis, role intelligence, employer context, risks, and next-step recommendation. Do not tailor materials by default. |
| `apply` | “Create a packet,” “tailor resume,” “apply,” “move forward” | Create/update the opportunity packet and generate application artifacts from verified evidence, including change log and reviewer pass. |
| `prep` | Recruiter screen, hiring-manager call, referral call, interview | Build pitch, story bank, questions, qualification wording, red flags, and do-not-overclaim boundaries. |
| `upskill` | “What gaps do I have?” “How should I prepare for these roles?” | Compare target roles against evidence and produce a development plan. |
| `status` | “Where does this stand?” “What is the status?” | Report status and next action only. Do not regenerate artifacts. |

Default to the narrowest useful mode. Escalate only when the user asks or when the saved opportunity status requires it.

## Inputs

Possible inputs:

- job posting URL
- job description text
- company career page
- public job listing
- recruiter message
- referrer context
- role family without a formal job description
- resume or cover-letter source material
- portfolio or project history
- interview stage and interviewer context
- compensation, location, or work-model constraints
- existing packet or tracker status

For any-country jobs, normalize market context instead of assuming US defaults. Capture country/region, city, time zone if relevant, salary currency, work model, and visa/sponsorship information when visible.

If no formal job description exists, switch to qualification-first mode. Use verified company context and label all inferred role expectations clearly.

## Suggested private configuration

Adapt this in the user's private workspace:

```yaml
candidate_profile:
  target_role_families:
    - <TARGET_ROLE_FAMILY_1>
    - <TARGET_ROLE_FAMILY_2>
  preferred_industries:
    - <INDUSTRY_1>
  preferred_level: <LEVEL_OR_SCOPE>
  compensation_constraints: <COMPENSATION_RULES>
  work_model_constraints: <REMOTE_HYBRID_ONSITE_RULES>
  location_constraints: <LOCATION_RULES>
  travel_constraints: <TRAVEL_RULES>

source_materials:
  master_resume: <MASTER_RESUME_PATH_OR_DOC>
  master_cover_letter: <MASTER_COVER_LETTER_PATH_OR_DOC>
  portfolio: <PORTFOLIO_OR_WEBSITE>
  brag_document: <BRAG_DOCUMENT>
  project_history: <PROJECT_HISTORY>

storage:
  career_packet_root: <CAREER_PACKET_ROOT>
  tracker: <TRACKER_URL_OR_PATH>

automation:
  scheduled_scan: <CRON_OR_SCHEDULED_AGENT>
  recommended_frequency: "daily at 8 AM; every 6 hours for active searches"
  approved_sources:
    - <JOB_BOARD_OR_COMPANY_CAREERS_SOURCE>
    - <COMPANY_CAREERS_PAGE>
    - <LINKEDIN_MCP_OR_LINKEDIN_JOB_SEARCH>
    - <COUNTRY_SPECIFIC_JOB_BOARD>
    - <REMOTE_WORK_BOARD>
  linkedin_mcp: <LINKEDIN_MCP_SERVER_NAME_IF_USED>
  tracker_sync: <SPREADSHEET_OR_DATABASE_SYNC>
  default_new_status: "01 - Not Reviewed"
  alert_policy: <WHEN_TO_NOTIFY_THE_USER>

thresholds:
  evaluate_only_below: 7.0
  tailor_materials_at_or_above: 7.0
  apply_immediately_at_or_above: 9.0
```

## Packet structure

Use any storage system: Markdown, Notion, Google Docs, a database, a spreadsheet, a project-management tool, or plain files.

Suggested status buckets:

```text
01 - Not Reviewed/
02 - Interested/
03 - Applied/
04 - Interview/
05 - Offers/
06 - On Hold/
99 - Not Interested/
100 - Rejected/
```

Suggested packet files:

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

Do not create every artifact for every role. Generate only what the mode and threshold require.

Artifact creation rules:

| Stage / status | Create these artifacts | Do not create yet |
|---|---|---|
| `01 - Not Reviewed` | `START HERE.md`, source posting, basic fit notes | Resume, CV, cover letter, interview prep |
| `02 - Interested` | Fit analysis, employer intelligence, role intelligence, gap analysis, application strategy | Final resume/CV unless applying soon |
| `03 - Applied` or active apply request | Job-specific resume or CV, cover letter, ATS keyword analysis, tailoring change log | Interview prep unless an interview is scheduled |
| Referral / recruiter screen | Referrer blurb, recruiter message, 60-second pitch, proof points | Full interview packet unless needed |
| `04 - Interview` | Interview prep packet, story bank, questions to ask, red flags to qualify | New resume rewrite unless the JD changed |
| `05 - Offers` | Offer comparison, negotiation notes, risk analysis | New application materials |
| `99 - Not Interested` / `100 - Rejected` | Status note only | Any new artifacts |

Simple global rule:

```text
Every job gets tracking.
Promising jobs get packets.
Apply-stage jobs get resume/CV + cover letter.
Interview-stage jobs get interview prep.
Closed jobs get no new artifacts.
```

Use `resume` or `CV` according to local market expectations. Do not force US terminology onto international roles.

## Required scheduled discovery layer

The workflow can be run manually for a single job, but the full Career Intelligence system requires a scheduled scan.

A cron job, scheduled agent, or workflow runner must:

1. scan approved job sources on a schedule,
2. extract company, role, URL, country/region, location, work model, compensation, currency, and source,
3. deduplicate against existing packets and tracker rows,
4. add new candidates to the review queue,
5. update a spreadsheet, database, or tracker with live status,
6. write a last-run timestamp and run summary,
7. notify only when a role needs attention or the job failed.

Automation should not apply to jobs by default. It should reduce discovery and tracking effort while preserving the decision workflow.

Recommended frequency:

| Schedule | Use when |
|---|---|
| Daily at 8 AM | Default for most users. |
| Every 6 hours | Active search, fast-moving market, multiple countries/time zones. |
| Twice weekly | Passive monitoring. |

Tracking requirements:

- A log must show the latest run summary.
- The tracker must include `Last Checked` or equivalent.
- New or updated roles must have packet/tracker consistency.
- Failures must be visible; do not fail silently.

Default scheduled-scan behavior:

- New roles go to `01 - Not Reviewed` or an equivalent review queue.
- Existing roles are updated, not duplicated.
- LinkedIn, company career pages, and job boards are treated as first-class source channels when configured.
- LinkedIn MCP results should capture the LinkedIn job URL, company, role, location/work model, poster or recruiter context when available, and any verified direct company careers link.
- The tracker mirrors packet status, source links, fit signals, and next action.
- Alerts are reserved for new high-signal roles, blockers, or state changes.

## Phase 0 — Source collection

1. Capture the job posting or source text if accessible.
2. Capture the original URL and direct company careers URL if available.
3. Gather candidate evidence from approved source materials.
4. Separate facts, inferences, and missing evidence.
5. Normalize company name and role title.
6. Choose the workflow mode.
7. Create or update a packet only when durable storage is useful.

## Phase 1 — Employer intelligence

Create employer intelligence when company context affects the decision.

Include:

- company overview
- products and services
- business model
- market position
- size and headquarters when public
- public/private status
- likely org ownership when relevant
- strategic initiatives
- recent news
- why each item matters for this candidate
- interview talking points

If public employee sentiment is useful, summarize:

- sources reviewed
- evidence quality and access limits
- common praise
- common complaints
- repeated themes
- risks and opportunities
- candidate-specific implications

## Phase 2 — Role intelligence

Create role intelligence when evaluating a role.

Include:

- title
- function
- department or org if known
- location and work model
- employment type
- compensation range if posted
- likely seniority or level
- must-have responsibilities
- preferred responsibilities
- technical skills
- leadership skills
- domain skills
- interview predictions

If no formal JD exists, title the section `Probable Role Shape` and label inferred expectations clearly.

## Phase 3 — Fit analysis

Score configured dimensions from 0–10. Example dimensions:

- role-family alignment
- seniority alignment
- domain alignment
- technical alignment
- leadership alignment
- compensation alignment
- work-model fit
- location fit
- career trajectory fit

Provide:

- overall fit score
- recommendation
- strengths
- weaknesses
- risks
- opportunities
- assumptions
- missing evidence
- next best action

Suggested thresholds:

| Score | Interpretation | Default action |
|---|---|---|
| 9.0–10.0 | Excellent fit | Apply or pursue immediately. |
| 7.0–8.9 | Strong fit | Consider tailored materials or referral strategy. |
| 5.0–6.9 | Borderline | Clarify risks before investing deeply. |
| Below 5.0 | Weak fit | Usually do not pursue. Explain why. |

Apply hard penalties for configured non-negotiables such as relocation requirements, level mismatch, unacceptable travel, below-threshold compensation, or domain divergence.

## Phase 4 — Gap analysis and development plan

For each major requirement, include:

- requirement
- importance
- evidence of match
- gap
- risk level
- mitigation strategy

Then provide:

- critical gaps
- moderate gaps
- minor gaps
- immediate actions
- 30-day development plan
- 90-day development plan
- longer-term evidence-building plan

## Phase 5 — ATS keyword analysis

Use this when the user may apply.

Include:

- high-value keywords from the posting
- keywords already supported by evidence
- keywords that are missing but safely supportable
- unsafe keywords that should not be added
- current match estimate
- recommended truthful adjustments

Do not keyword-stuff. Do not add unsupported technologies or responsibilities.

## Phase 6 — Resume and cover-letter tailoring

Generate tailored materials only when:

- fit score meets the configured threshold,
- the opportunity is in an active application stage, or
- the user explicitly asks.

Rules:

- Use the candidate's approved source resume and cover letter as the foundation.
- Preserve the candidate's voice unless the user asks for a rewrite.
- Change emphasis, ordering, summary language, and selected evidence.
- Do not invent facts.
- Do not redesign unless asked.
- Keep a change log.
- Verify final outputs exist and are readable.

Drafter-reviewer loop:

1. Draft role-specific material from verified sources.
2. Review against the JD, fit analysis, ATS analysis, and candidate evidence.
3. Flag unsupported claims, weak alignment, and formatting drift.
4. Revise only with grounded changes.
5. Verify the final artifact.

## Phase 7 — Referral and recruiter artifacts

Create referral/recruiter artifacts when referral, recruiter, or application-form support is needed.

Include some or all of:

- referral ask message
- referrer talking blurb
- recruiter outreach note
- recruiter screen positioning
- plain-text ATS-safe resume block
- role-specific proof points

### Referrer talking blurb rules

The referrer blurb should be:

- 1–2 concise paragraphs
- role-specific
- company/team-aware where evidence supports it
- factual and warm
- written in language a referrer could credibly use
- grounded only in verified candidate evidence

Never imply that the referrer has worked with the candidate, directly observed performance, or has inside knowledge unless that is explicitly true.

## Phase 8 — Application strategy

For serious opportunities, include:

- fit score
- recommendation
- interview probability estimate
- positioning strategy
- networking or referral strategy
- what to clarify first
- risks to manage
- likely interview themes
- next actions

For qualification-first opportunities, emphasize what must be learned before applying.

## Phase 9 — Questions to ask employer

For recruiter screens, hiring-manager calls, interviews, or diligence, include:

- top 12 must-ask questions
- recruiter questions
- hiring-manager questions
- peer/panel questions
- success metrics questions
- team/scope questions
- work-model and travel questions
- compensation/equity questions when appropriate
- culture and operating-model questions
- questions to avoid
- stage-by-stage usage guide

Questions should be specific to the role and company, not generic interview filler.

## Phase 10 — Interview prep

When the user has an interview or screen, include:

- 60-second pitch
- role-specific positioning
- likely questions
- story bank
- leadership examples
- technical/program examples
- red flags to qualify
- questions to ask
- compensation/work-model wording
- do-not-overclaim boundaries
- final pre-call checklist

If interviewer names are available, include only information that changes positioning or questions. Avoid generic small talk research unless requested.

## Status-only workflow

For status requests:

1. Look up the packet or tracker.
2. Report status, next action, and blockers.
3. Do not regenerate fit analysis, resume, cover letter, or prep artifacts.
4. Keep the response short.

## Rejection or not-interested cleanup

When the user says a role was rejected or should be closed:

1. Move or mark the packet in the correct status bucket.
2. Update the current status and date.
3. Preserve historical notes.
4. Do not regenerate application artifacts.
5. Keep the response short.

## Final validation checklist

Before reporting completion, verify:

- [ ] Correct workflow mode was selected.
- [ ] Original source link was captured when available.
- [ ] Direct company careers link was captured when available.
- [ ] Claims are supported by candidate evidence.
- [ ] Inferences are labeled.
- [ ] Unsupported claims were removed.
- [ ] Fit score and recommendation are explained.
- [ ] Resume/cover materials were generated only when justified.
- [ ] High-stakes artifacts received a reviewer pass.
- [ ] Final files exist and are readable when files were requested.
- [ ] Tracker or packet status is consistent.
- [ ] Next action is clear.

## Common pitfalls

1. **Treating every job as apply mode**
   - Fix: classify the request first.

2. **Optimizing a weak-fit role**
   - Fix: evaluate strategic fit before creating materials.

3. **Mistaking keyword overlap for fit**
   - Fix: score level, scope, domain, compensation, work model, and trajectory.

4. **Inventing candidate strength**
   - Fix: use only verified evidence and label gaps honestly.

5. **Writing generic referral language**
   - Fix: make the blurb role-specific and credible for the referrer.

6. **Losing context across conversations**
   - Fix: preserve decision rationale in a packet or tracker.
