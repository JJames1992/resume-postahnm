# /outlook-sync - Sync Application Status from Outlook Email

You are scanning the user's Outlook email for status signals on tracked job applications (interview invites, assessment links, offers, rejections) and, once approved, writing the detected changes into `job_search_tracker.csv` and `documents/applications/<company>_<role>/outcome.md`.

This works identically to `/gmail-sync` but uses the Microsoft Graph API via the `graph.py` script in `~/AppData/Local/hermes/outlook/` instead of Gmail MCP.

## Prerequisites

Confirm Outlook Graph access is available:
- Token cache at `~/AppData/Local/hermes/outlook/token_cache.json`
- `graph.py mail` works (test: `python graph.py mail --limit 5`)
- Scopes include `Mail.Read`, `Mail.ReadWrite`, `Mail.Send`

## Step 1: Load State

1. Read `job_search_tracker.csv` — extract all tracked companies and role identifiers
2. Build lookup: company_name → [row_indices, job_title, status]

## Step 2: Search Email

Query Outlook inbox + Sent Items for messages from the last 21 days containing:
- Keywords: "application", "interview", "rejection", "offer", "assessment", "hired", "position"
- Sender domains from tracked companies (e.g., `pppl.gov`, `tektronix.com`)

For each message, extract:
- Sender (email + name)
- Subject
- Received date
- Body snippet (first 200 chars)

## Step 3: Classify

For each found message, classify the signal:

| Pattern in Subject/Body | Classification |
|---|---|
| "interview" + date/time | INTERVIEW_INVITE |
| "offer" or "congratulations" | OFFER |
| "not proceeding" / "no longer" / "rejection" | REJECTION |
| "application received" / "submitted" | APPLICATION_RECEIVED |
| "assessment" / "test" link | ASSESSMENT_REQUEST |
| "following up" / "checking in" | FOLLOW_UP |

## Step 4: Present Batch

Present all classified changes to the user as a table:
| Message | Classification | Confidence | Matched Company | Proposed Tracker Change |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

Do NOT write to tracker until user approves the batch.

## Step 5: Write Changes

After approval, update:
1. `job_search_tracker.csv` — update status column, applied_date, notes
2. `documents/applications/<company>_<role>/outcome.md` — append outcome entry with source email citation

## Step 6: Mark Email as Read

After processing, mark the relevant inbox emails as read to avoid re-processing.

## Notes

- If no Outlook access configured, tell the user to run the Microsoft 365 setup
- Never auto-reply to employer emails — flag for user review only
- If the tracker row doesn't exist for a matched company, create a new row with status "INBOX_HIT"
