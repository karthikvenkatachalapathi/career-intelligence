# Career Intelligence Skill

A reusable AI-agent skill for helping people navigate career decisions with structure, evidence, and judgment — especially in a difficult tech market shaped by layoffs, reorganizations, and slower hiring cycles.

This repository is intentionally **PII-free**. It contains a generalized version of a Career Intelligence workflow that anyone can adapt for their own background, target roles, constraints, and preferred tools.

## Why this exists

Many career tools optimize for volume:

- more job postings
- more applications
- more resume variants
- more cover letters

In a tough market, volume is not always the advantage. The bigger advantage is decision quality:

- Which opportunities are actually worth pursuing?
- Is the role strategically aligned, or just keyword-adjacent?
- What evidence supports the candidate's fit?
- What gaps or risks should be understood up front?
- What should be clarified before investing more time?
- When should tailored materials be created — and when should they be skipped?

The Career Intelligence Skill turns career exploration into a repeatable AI-assisted workflow. It is designed to help someone think clearly, preserve context, and create high-quality artifacts only when justified.

## Inspiration and credit

This work was influenced by [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search), an open-source AI-powered job application framework built around Claude Code.

That project demonstrates how AI can help evaluate jobs, tailor CVs, write cover letters, and prepare for interviews. This skill borrows the useful discipline of structured command modes and agent-assisted career workflows, while taking a different direction: a broader **career decision system** focused on evidence, fit, risk, and durable context rather than application volume.

## What makes this skill different

### 1. Decision quality over application volume

The skill is not designed to apply everywhere. It is designed to decide what deserves attention.

It separates quick screening, deeper evaluation, application artifact creation, interview preparation, and status tracking into distinct modes.

### 2. Evidence before optimization

The skill explicitly prohibits inventing:

- experience
- accomplishments
- metrics
- certifications
- technologies
- employers
- dates
- relationships
- referrals

If a claim is not supported by the candidate's source material, it should not appear in the output.

### 3. Fit is based on trajectory, not keywords

Keyword overlap is not the same as career fit. The workflow evaluates opportunities across dimensions such as:

- seniority alignment
- domain fit
- leadership scope
- technical relevance
- compensation assumptions
- work model
- location constraints
- long-term career direction

### 4. Career packets preserve context

The skill encourages each serious opportunity to become a structured packet containing fit analysis, employer intelligence, gap analysis, strategy, questions, referral language, and interview prep.

That makes the process durable. A person should be able to return to an opportunity later without reconstructing the decision from scattered chats, notes, browser tabs, or recruiter messages.

### 5. Referrals are treated thoughtfully

The skill includes a dedicated referrer-talking-blurb artifact. The goal is to help a referrer explain a candidate's fit credibly and specifically, without overstating the relationship or fabricating inside knowledge.

### 6. High-stakes artifacts get a reviewer pass

For resumes, cover letters, and other high-stakes materials, the skill uses a drafter-reviewer pattern:

1. Draft from verified evidence.
2. Review for unsupported claims, weak positioning, missing evidence, and formatting drift.
3. Revise only with grounded improvements.
4. Verify the final artifact exists and is usable.

## Workflow modes

| Mode | Use when | Expected behavior |
|---|---|---|
| `scan` | Looking for opportunities or themes | Find high-signal roles, dedupe, shortlist only credible matches. |
| `evaluate` | Deciding whether a role is worth pursuing | Build fit analysis, employer intelligence, risks, and next-step recommendation. |
| `apply` | The opportunity clears the bar | Generate tailored resume/cover/referral artifacts from verified evidence. |
| `prep` | A recruiter screen, hiring-manager call, or interview is coming up | Produce interview prep, story bank, questions, and positioning guidance. |
| `upskill` | Comparing target roles to current evidence | Identify gaps, learning priorities, and evidence-building opportunities. |
| `status` | Checking where an opportunity stands | Look up status from the packet/tracker without regenerating artifacts. |

## Suggested repository structure after installing

You can adapt this to any note system, document system, or tracker. One common structure is:

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

Each opportunity packet can contain:

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

## Installation

### Option A — Use with Hermes Agent skills

Copy the skill folder into your Hermes profile skills directory:

```bash
mkdir -p ~/.hermes/profiles/<profile-name>/skills/productivity/
cp -R skills/career-intelligence ~/.hermes/profiles/<profile-name>/skills/productivity/career-intelligence
```

Start a new Hermes session so the skill loader can pick it up.

### Option B — Use as a prompt/workflow in another agent

If your agent system does not support Hermes-style skills, copy the contents of:

```text
skills/career-intelligence/SKILL.md
```

into your agent's system prompt, project instructions, or reusable workflow library.

## Configuration checklist

Before using this skill, customize the placeholders in `skills/career-intelligence/SKILL.md`:

- target role families
- preferred industries
- level/seniority targets
- compensation constraints
- work-model constraints
- location constraints
- source documents to trust
- packet storage location
- tracker fields
- artifact naming conventions
- apply/tailoring threshold

## Recommended source materials

The skill works best when the agent has access to a clean evidence base:

- master resume
- master cover letter
- portfolio or personal website
- project history
- brag document
- performance review excerpts
- case studies
- writing samples
- certifications
- target role examples

Do not add private information to this public repository. Keep personal source documents in your private workspace.

## Safety and privacy

This repository should not contain:

- names of private individuals
- personal email addresses
- phone numbers
- home addresses
- private compensation details
- private recruiter or referrer names
- private auth IDs or document IDs
- credentials or access keys
- local filesystem paths
- unpublished employment history
- private company documents

Use placeholders such as:

```text
<CANDIDATE_NAME>
<TARGET_ROLE_FAMILY>
<CAREER_PACKET_ROOT>
<MASTER_RESUME_PATH>
<TRACKER_URL>
<COMPENSATION_FLOOR>
```

## Example prompts

### Evaluate a role

```text
Use the Career Intelligence skill in evaluate mode for this job posting. Tell me whether it is worth pursuing, what evidence supports the fit, what risks exist, and what I should clarify before investing more time.
```

### Prepare for a recruiter screen

```text
Use the Career Intelligence skill in prep mode. Build a recruiter-screen prep packet with a 60-second pitch, must-ask questions, compensation/work-model clarification wording, and risks to qualify.
```

### Create application artifacts

```text
Use the Career Intelligence skill in apply mode. Generate tailored application artifacts only from verified source material. Include a change log and reviewer pass.
```

### Build a referral blurb

```text
Use the Career Intelligence skill to create a referrer talking blurb for this role. Keep it factual, role-specific, and written in language a referrer could credibly use.
```

## Contributing

Contributions are welcome if they preserve the core principles:

- evidence before optimization
- no fabricated candidate claims
- decision quality over volume
- explicit uncertainty labeling
- reusable packet structure
- privacy by default

Please avoid adding real candidate data, real recruiter messages, private documents, or company-confidential material.

## License

MIT License. See [LICENSE](LICENSE).
