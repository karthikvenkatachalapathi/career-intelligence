# Opportunity packet template

This is a starter template for one tracked opportunity.

The user does **not** need to create every packet by hand.

Recommended behavior:

- The user creates or chooses a private `Career Intelligence/` workspace once.
- The agent creates a new opportunity packet automatically when a role is worth tracking.
- The agent uses this template to keep every packet consistent.
- The user reviews, corrects, and adds private evidence when needed.

Do not fill this public template with private career data.

## Workspace structure

Create this once in your private workspace:

```text
<CAREER_PACKET_ROOT>/
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

## Packet creation rule

When a new role is found manually or through scheduled discovery, the agent should create:

```text
<CAREER_PACKET_ROOT>/<STATUS>/<COMPANY> - <ROLE>/
  START HERE.md
```

Default status for new discovered roles:

```text
01 - Not Reviewed
```

Only create additional artifact files when the workflow mode requires them.

## START HERE.md template

```markdown
# <COMPANY> - <ROLE>

## Current status

- Status: <STATUS>
- Priority: <PRIORITY>
- Fit score: <SCORE>/10
- Recommendation: <RECOMMENDATION>
- Next action: <NEXT_ACTION>

## Source links

- Job link: <JOB_POSTING_URL>
- Company careers link: <COMPANY_CAREERS_URL>
- LinkedIn job link: <LINKEDIN_JOB_URL>
- Date captured: <DATE>

## Why this might fit

- <EVIDENCE_BASED_POINT_1>
- <EVIDENCE_BASED_POINT_2>
- <EVIDENCE_BASED_POINT_3>

## Key risks

- <RISK_1>
- <RISK_2>
- <RISK_3>

## Next action

<NEXT_ACTION_DETAIL>

## Artifacts

- [ ] 00 - Source Job Posting.md
- [ ] 01 - Job Fit Analysis.md
- [ ] 02 - Employer Intelligence.md
- [ ] 02A - Employee Sentiment.md
- [ ] 03 - Role Intelligence.md
- [ ] 04 - Gap Analysis and Development Plan.md
- [ ] 05 - ATS Keyword Analysis.md
- [ ] 06A - Tailoring Change Log.md
- [ ] 08 - Application Strategy.md
- [ ] 09 - Referral Screen Messages and ATS Resume.md
- [ ] 10 - Questions to Ask Employer.md
- [ ] 11 - Interview Prep Packet.md
```
