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

### 3. Pull full call details from #sales-momentum-notifications

For each call found, search the `#sales-momentum-notifications` channel (channel ID: `C07RBLTPA5Q`) to find the matching message and its thread. Read the thread replies to extract:

- Call title and date
- Zoom recording link
- Attendee names
- Full Momentum AI summary (questions asked, objections, next steps, direct quotes)

### 4. Present calls to the user

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

Then ask:

> If you'd like to include a transcript for any of these calls, click the Zoom link, download the VTT transcript file, and paste the local file path(s) below — one per line. Press Enter with no input to proceed with Slack summaries only.

Wait for the user to respond before continuing.

### 5. Read transcript files (if provided)

If the user provides any file paths, read each file. Match each transcript to its corresponding call by filename, date, or attendee names mentioned in the file. Use the transcript as additional context for that call alongside the Momentum summary.

### 6. Read the current FAQs

Read `docs/faqs.md` in full. Note the existing sections and what questions are already covered.

### 7. Gap analysis

Review all Momentum summaries and any transcripts together. Identify questions, objections, or topics that:

- Are not covered at all in the current FAQs
- Are covered but incompletely or in a way the call suggests needs expanding

Focus on questions that would be useful to a broader audience — skip anything too company-specific or one-off. Generalise where appropriate (e.g. don't write an AWS-only answer if the answer applies to all cloud providers).

### 8. Draft FAQ entries

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
- Which call(s) it came from

### 9. Confirm before writing

Ask the user to confirm each proposed entry before writing. For each one, the user can:
- Approve as-is
- Request edits
- Skip

Do not write anything to the file until the user has reviewed all proposed entries.

### 10. Write approved entries to faqs.md

Insert each approved entry into `docs/faqs.md` at the correct position within the correct section.

### 11. Commit the changes

Stage and commit the updated file with a message summarising what was added, for example:

```
docs: add FAQs from [call names] ([date])
```
