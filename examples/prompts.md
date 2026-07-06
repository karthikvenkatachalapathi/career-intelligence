# Example Prompts

These examples are intentionally generic. Replace placeholders with private information only in your local workspace.

## Scan mode

```text
Use the Career Intelligence workflow in scan mode. Find high-signal roles matching <TARGET_ROLE_FAMILY> and <LOCATION_OR_WORK_MODEL_RULES>. Search my configured global sources, dedupe against my tracker, and return only opportunities that appear worth deeper evaluation.
```

## Scheduled discovery

```text
Use the Career Intelligence workflow in scan mode as my scheduled discovery run.
Scan my configured sources for any country or job board I listed.
Update my tracker with Company, Role, Country/Region, Location, Work Model, Source URL, Date Found, Last Checked, Fit Score, Next Action, and Artifact Status.
Create or update packets in my Career Intelligence workspace.
Do not auto-apply.
Report only new high-signal roles, blockers, or failures.
```

## Cron tracking check

```text
Use the Career Intelligence workflow in status mode. Check whether scheduled discovery is running correctly. Verify the latest log entry, tracker Last Checked values, and whether new or updated roles have matching packets.
```

## Evaluate mode

```text
Use the Career Intelligence workflow in evaluate mode for this job posting: <JOB_POSTING_URL>. Assess strategic fit, evidence, risks, gaps, country/location/work-model constraints, and the recommended next action. Do not generate application materials yet.
```

## Apply mode

```text
Use the Career Intelligence workflow in apply mode for this packet. Tailor the resume or CV and cover letter from verified source material only. Use the document convention expected for this country/market. Include ATS keyword analysis, a tailoring change log, and reviewer pass.
```

## Prep mode

```text
Use the Career Intelligence workflow in prep mode. I have a recruiter screen for <ROLE> at <COMPANY>. Create a 60-second pitch, must-ask questions, compensation/work-model qualification wording, likely risks, and do-not-overclaim boundaries.
```

## Referral blurb

```text
Use the Career Intelligence workflow to create a referrer talking blurb for <ROLE> at <COMPANY>. It should be factual, concise, role-specific, and written in language a referrer could credibly use.
```

## Upskill mode

```text
Use the Career Intelligence workflow in upskill mode. Compare my evidence base against these target roles and identify the highest-leverage gaps to close over the next 30 and 90 days.
```

## Status mode

```text
Use the Career Intelligence workflow in status mode. Tell me where <COMPANY> - <ROLE> stands, whether required artifacts exist for the current stage, and the next action. Do not regenerate artifacts.
```
