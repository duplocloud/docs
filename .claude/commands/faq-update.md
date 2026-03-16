Update `docs/faqs.md` based on recent prospect and customer calls pulled from Slack.

## Steps

### 1. Get the last FAQ update date

Run this command and note the date:

```bash
git log -1 --format="%ci" docs/faqs.md
```

### 2. Search #momentum-ai-feedback for calls since that date

Search the `#momentum-ai-feedback` channel (channel ID: `C09A17N30S1`) for messages since the last FAQ update date. Convert the date to a Unix timestamp for the `oldest` parameter — subtract 19800 seconds to account for IST (UTC+5:30).

Collect the list of call names and dates mentioned.

### 3. Pull full call details from #sales-momentum-notifications and #cs-momentum-notifications

Use `slack_read_channel` (not search) on both the `#sales-momentum-notifications` channel (channel ID: `C07RBLTPA5Q`) and the `#cs-momentum-notifications` channel (channel ID: `C07R22S53BN`) with the `oldest` timestamp from step 2. Read through the messages to find each call. From the matching message extract:

- Call title and date
- Zoom recording link — this is the **full** preauthenticated URL embedded in the call title hyperlink in the parent message (e.g., `<https://duplocloud.zoom.us/rec/share/xxx?pwd=yyy|Call Title>`). The `?pwd=` query parameter is part of the authentication and **must not be truncated or omitted**.
- Attendee names

Then read the thread replies to extract:

- Full Momentum AI summary (questions asked, objections, next steps, direct quotes)

### 4. Search #ask-a-technical-question for recent questions

Search the `#ask-a-technical-question` channel (channel ID: `C0486SQ3RA5`) for messages since the last FAQ update date. For each question found, read the thread replies to capture any answers provided.

Collect the question, any answers, and the approximate date.

### 5. Present calls and questions to the user

Display each call clearly with its Zoom recording link, like this:

```
Found N call(s) since last FAQ update (YYYY-MM-DD):

1. [Call Title] — [Date]
   Attendees: [names]
   Zoom recording: [link]

2. [Call Title] — [Date]
   Attendees: [names]
   Zoom recording: [link]
```

Then display any questions from `#ask-a-technical-question`:

```
Found M question(s) from #ask-a-technical-question:

1. [Question summary] — [Date]
   Asked by: [name]
   Answer: [summary of thread replies, or "no answer yet"]
```

Then ask:

> If you'd like to include a transcript for any of these calls, click the Zoom link, download the VTT transcript file, and paste the local file path(s) below — one per line. Press Enter with no input to proceed with Slack summaries only.

Wait for the user to respond before continuing.

### 6. Read transcript files (if provided)

If the user provides any file paths, read each file. Match each transcript to its corresponding call by filename, date, or attendee names mentioned in the file. Use the transcript as additional context for that call alongside the Momentum summary.

### 7. Read the current FAQs

Read `docs/faqs.md` in full. Note the existing sections and what questions are already covered.

### 8. Gap analysis

Review all Momentum summaries, any transcripts, and the `#ask-a-technical-question` questions together. Identify questions, objections, or topics that:

- Are not covered at all in the current FAQs
- Are covered but incompletely or in a way the call suggests needs expanding

Focus on questions that would be useful to a broader audience — skip anything too company-specific or one-off. Generalise where appropriate (e.g. don't write an AWS-only answer if the answer applies to all cloud providers).

### 9. Draft FAQ entries

For each gap, write a new FAQ entry using the GitBook `<details>`/`<summary>` format:

```markdown
<details>

<summary>Question here?</summary>

Answer here.

</details>
```

For each proposed entry, show the user:
- The full draft entry
- Which existing section it belongs in (Security & Access / Pricing & Billing / Agents & Customisation / Operations & Reliability / Integration & Tooling / Getting Started)
- Where within that section it should be inserted (after which existing question)
- Which call(s) or question(s) it came from

### 10. Confirm before writing

Ask the user to confirm each proposed entry before writing. For each one, the user can:
- Approve as-is
- Request edits
- Skip

Do not write anything to the file until the user has reviewed all proposed entries.

### 11. Write approved entries to faqs.md

Insert each approved entry into `docs/faqs.md` at the correct position within the correct section.

### 12. Commit the changes

Stage and commit the updated file with a message summarising what was added, for example:

```
docs: add FAQs from [call names] ([date])
```
