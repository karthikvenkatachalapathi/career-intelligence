# Privacy and PII Checklist

Before publishing or contributing to this repository, confirm that no private data is present.

## Do not commit

- Real candidate names unless intentionally public
- Personal email addresses
- Phone numbers
- Home addresses
- Private compensation details
- Private recruiter/referrer names
- Private recruiter messages
- OAuth IDs
- Google Doc IDs or private document IDs
- API keys, tokens, cookies, or credentials
- Local filesystem paths
- Internal company documents
- Unpublished employment details
- Private tracker URLs
- Private interview notes

## Use placeholders

Use placeholders instead of personal values:

```text
<CANDIDATE_NAME>
<TARGET_ROLE_FAMILY>
<CAREER_PACKET_ROOT>
<MASTER_RESUME_PATH>
<MASTER_COVER_LETTER_PATH>
<TRACKER_URL>
<COMPENSATION_RULES>
<WORK_MODEL_RULES>
<LOCATION_RULES>
<REFERRER_NAME>
<RECRUITER_NAME>
```

## Suggested scan commands

Run these before publishing:

```bash
grep -RInE '(@|phone|address|token|secret|password|api[_-]?key|oauth|google_token|docid|/home/|Users/)' .
grep -RInE 'Karthik|Venkat|Meta|AWS|Deloitte|Oracle|Anthropic|Fluidstack' .
git status --short
```

The second command is intentionally conservative. Replace the names with private identifiers relevant to your own environment before publishing.
