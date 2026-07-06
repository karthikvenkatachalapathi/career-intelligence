---
name: career-intelligence
description: Use when evaluating career opportunities, job postings, referrals, recruiter conversations, interview preparation, or application artifacts. Helps classify the task, assess evidence-based fit, preserve decision context, and create truthful career materials only when justified.
version: 1.0.0
author: Community
license: MIT
metadata:
  hermes:
    tags: [career, jobs, resume, cover-letter, referrals, interview-prep, decision-support]
    related_skills: []
---

# Career Intelligence Skill

## Overview

This skill helps an AI agent support career decisions with structure, evidence, and judgment.

It is designed for people navigating complex career choices, including layoffs, reorganizations, slow hiring markets, referrals, interviews, and role comparisons. The goal is not to maximize application volume. The goal is to help a candidate decide which opportunities deserve time and how to pursue them honestly and effectively.

This skill can be adapted for any candidate. Replace the placeholders in this file with the candidate's real constraints, source materials, and career goals in a private workspace. Do not commit personal data to a public repository.

## Core principles

1. **Evidence before optimization**
   - Never invent experience, accomplishments, metrics, certifications, technologies, employers, dates, responsibilities, relationships, or referrals.
   - If a claim is unsupported, label it as missing, inferred, or unverified.
   - Strong positioning should come from better evidence selection, not fabrication.

2. **Decision quality over application volume**
   - Do not treat every job posting as an application task.
   - Classify the request into the narrowest workflow mode that satisfies it.
   - Escalate to full application artifacts only when the role clears the configured threshold or the user explicitly asks.

3. **Career trajectory matters more than keyword overlap**
   - A role can match keywords while being a poor strategic fit.
   - Evaluate level, scope, work model, compensation, domain, growth, and long-term direction.

4. **Context should be durable**
   - Serious opportunities should become structured packets.
   - Preserve source links, decision rationale, risks, questions, status, and artifacts so the candidate can resume later without starting over.

5. **Privacy by default**
   - Keep personal source documents private.
   - Use placeholders in public examples.
   - Do not expose recruiter names, referrer names, email addresses, private document IDs, local paths, or compensation details unless the user explicitly wants them in a private artifact.

## Required private configuration

Before using this skill, configure these values in the user's private workspace:

```yaml
candidate_profile:
  name: <CANDIDATE_NAME>
  target_role_families:
    - <TARGET_ROLE_FAMILY_1>
    - <TARGET_ROLE_FAMILY_2>
  preferred_industries:
    - <INDUSTRY_1>
  preferred_level: <LEVEL_OR_SCOPE>
  compensation_constraints: <PRIVATE_COMPENSATION_RULES>
  work_model_constraints: <REMOTE_HYBRID_ONSITE_RULES>
  location_constraints: <LOCATION_RULES>
  travel_constraints: <TRAVEL_RULES>

source_materials:
  master_resume: <PRIVATE_MASTER_RESUME_PATH_OR_DOC>
  master_cover_letter: <PRIVATE_MASTER_COVER_LETTER_PATH_OR_DOC>
  portfolio: <OPTIONAL_PRIVATE_OR_PUBLIC_PORTFOLIO>
  brag_document: <PRIVATE_BRAG_DOCUMENT>
  project_history: <PRIVATE_PROJECT_HISTORY>

storage:
  career_packet_root: <PRIVATE_CAREER_PACKET_ROOT>
  tracker: <OPTIONAL_TRACKER_URL_OR_PATH>
  docx_versions_root: <OPTIONAL_DOCX_ROOT>

thresholds:
  evaluate_only_below: 7.0
  tailor_materials_at_or_above: 7.0
  apply_immediately_at_or_above: 9.0
```

## Workflow modes

Before acting, classify the request into one mode.

| Mode | Trigger examples | Expected behavior |
|---|---|---|
| `scan` | "Find roles", "scan job boards", "what should I look at?" | Search high-signal boards or company pages, dedupe, shortlist only credible matches. |
| `evaluate` | A job link, job description, company page, or "is this worth it?" | Build or update fit analysis, role intelligence, employer context, risks, and next-step recommendation. Do not tailor materials unless threshold or user request justifies it. |
| `apply` | "Create a packet", "tailor resume", "move forward", "apply" | Generate full application artifacts from verified evidence, including change log and reviewer pass. |
| `prep` | Recruiter screen, hiring-manager call, panel, interview, referral call | Build interview prep, pitch, story bank, questions, red flags, and qualification wording. |
| `upskill` | "What gaps do I have?", "how do I prepare for these roles?" | Compare target roles against verified evidence and produce a development plan. |
| `status` | "Where does this stand?", "what is my status?" | Look up packet/tracker status only. Do not regenerate artifacts. |

Default to the narrowest mode. Do not escalate a status or evaluate request into apply mode unless the user explicitly asks.

## Inputs

Possible inputs:

- job posting URL
- job description text
- company career page
- LinkedIn or public job listing
- recruiter message
- referrer context
- role family without a formal job description
- resume or cover letter source documents
- portfolio or project materials
- interview stage and interviewer context
- compensation or work-model constraints

If the user does not have a formal job description yet, switch to referral or qualification-first mode. Use verified company context and label inferred role expectations clearly.

## Packet structure

For serious opportunities, create a packet under the configured private career packet root.

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

## Artifact standards

Every artifact should be:

- evidence-based
- concise but decision-useful
- explicit about uncertainty
- free of fabricated claims
- structured for fast rereading
- linked to source material when possible

Include source links when available:

- original job posting link
- direct company careers page link
- supporting company source links
- date captured
- confidence notes

## Phase 0 — Source collection

1. Capture the job posting or source text if accessible.
2. Capture the original URL and direct company careers URL if available.
3. Gather candidate evidence from approved private source materials.
4. Separate facts, inferences, and missing evidence.
5. Normalize company name and role title.
6. Choose the correct workflow mode.
7. Create or update the packet only when the task requires durable storage.

## Phase 1 — Employer intelligence

Create `02 - Employer Intelligence.md` when the mode requires company research.

Include:

- company overview
- products and services
- business model
- market position
- size and headquarters when public
- public/private status
- leadership and likely org ownership when relevant
- strategic initiatives
- recent news
- why each item matters for this candidate
- interview talking points

If public employee sentiment is useful, create `02A - Employee Sentiment.md` with:

- sources reviewed
- evidence quality and access limits
- common praise
- common complaints
- repeated themes
- risks and opportunities
- candidate-specific implications

## Phase 2 — Role intelligence

Create `03 - Role Intelligence.md` when evaluating a role.

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

Create `01 - Job Fit Analysis.md`.

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

Apply hard penalties for user-defined non-negotiables, such as relocation requirements, level mismatch, unacceptable travel, below-threshold compensation, or domain divergence.

## Phase 4 — Gap analysis and development plan

Create `04 - Gap Analysis and Development Plan.md` when useful.

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

Create `05 - ATS Keyword Analysis.md` when the user may apply.

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
- Preserve the candidate's voice.
- Change emphasis, ordering, summary language, and selected evidence.
- Do not invent facts.
- Do not redesign unless asked.
- Keep a change log in `06A - Tailoring Change Log.md`.
- Verify final outputs exist and are readable.

Recommended drafter-reviewer loop:

1. Draft role-specific material from verified sources.
2. Review against the JD, fit analysis, ATS analysis, and candidate evidence.
3. Flag unsupported claims, weak alignment, and formatting drift.
4. Revise only with grounded changes.
5. Verify rendered artifacts.

## Phase 7 — Referral and recruiter artifacts

Create `09 - Referral Screen Messages and ATS Resume.md` when referral, recruiter, or application-form support is needed.

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

Create `08 - Application Strategy.md` for serious opportunities.

Include:

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

Create `10 - Questions to Ask Employer.md` for recruiter screens, hiring-manager calls, interviews, or diligence.

Include:

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

Create `11 - Interview Prep Packet.md` when the user has an interview or screen.

Include:

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
2. Report status, next action, and any blockers.
3. Do not regenerate fit analysis, resume, cover letter, or prep artifacts.
4. Keep the response short.

## Rejection or not-interested cleanup

When the user says a role was rejected or should be closed:

1. Move or mark the packet in the correct status bucket.
2. Update `START HERE.md` with the current status and date.
3. Preserve historical notes.
4. Do not regenerate application artifacts.
5. Keep the response short.

## Final validation checklist

Before reporting completion, verify:

- [ ] Correct workflow mode was selected.
- [ ] No private data was written to public files.
- [ ] Original source link was captured when available.
- [ ] Direct company careers link was captured when available.
- [ ] Claims are supported by candidate evidence.
- [ ] Inferences are labeled.
- [ ] Unsupported claims were removed.
- [ ] Fit score and recommendation are explained.
- [ ] Resume/cover materials were generated only when justified.
- [ ] High-stakes artifacts received a reviewer pass.
- [ ] Final files exist and are readable.
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
   - Fix: preserve decision rationale in a packet.

7. **Publishing private examples**
   - Fix: keep public repos placeholder-only and store personal source material privately.
