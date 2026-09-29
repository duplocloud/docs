---
name: product-updates
description: Use when the user asks for weekly product updates, weekly AI update summaries, or to "do the weekly updates". Covers fetching commits from GitHub, publishing the product updates changelog section, and then auditing and updating the product doc pages those updates affect (with screenshots via the Playwright skill where the UI changed).
---

# Product Update Workflow

Runs periodically (nominally weekly, but resumes from wherever the last run left off — see Step 1). Two phases, each ending in its own PR:

1. **Changelog** (Steps 1–3) — a new section appended to the public-facing product updates page.
2. **Docs** (Step 4) — for each published item, check whether the product docs need creating or correcting, and do it; screenshot-bearing pages go through the Playwright skill.

Phase 2 is part of the job, not an optional extra. Announcing a feature in the changelog while leaving its doc page stale or absent is the failure mode this skill exists to prevent.

---

## Fixed Config (never ask the user for these)

### GitHub Repos & Branches
| Repo | Branch |
|------|--------|
| `duplocloud-internal/duplo-ai-helpdesk` | `main` |
| `duplocloud-internal/duplo-ui` | `master` |
| `duplocloud-internal/claude-code-generic-ai-agent` | `main` (default) |
| `duplocloud-internal/helpdesk-helm` | `main` (default) |

---

## Step 1 — Determine the Date Range

There is no local state to read — this skill runs from inside the tracked `docs` repo and keeps no files of its own. The date range instead comes from **this skill's own past PRs on GitHub**, identified by a hidden marker (see Step 3b).

1. Find the docs repo's GitHub remote from the current directory: `gh repo view --json nameWithOwner -q .nameWithOwner` (do not hardcode an org/repo).
2. Search merged PRs on that repo for the marker, most recent first:
   ```bash
   gh pr list --repo <owner/repo> --state merged --search "product-updates-skill-marker in:body" \
     --json number,title,mergedAt,body --limit 5
   ```
3. Take the most recent result and extract the covered-through date from its hidden marker (format below) — this is the **start** of the new window.
4. If no marker is found anywhere (first run, or the marker was never added before), work out the last point of genuine **coverage** and propose it, then confirm with the user before using it.

   **Do not take the most recent PR that touched the changelog file.** Several kinds of PR touch `ai-helpdesk-v2/product-updates.md` without advancing coverage at all — doc-page passes that only add cross-links into existing entries, wording corrections, formatting fixes. The date that matters is when content was last *added*, not when the file was last edited.

   To find it: read the newest `##` section heading actually present in the file — that is the real watermark — and cross-check it against the PR that introduced that section (`git log -- ai-helpdesk-v2/product-updates.md`, looking for the commit that added the heading rather than ones that modified entries under it).

   Then propose a start date and say what you based it on. **If the watermark is ambiguous, ask the user rather than picking.** It frequently is: a heading like `## June–July 2026` names no end day, and the PR that added it may have merged before the month ended, so coverage could stop several days short of the heading's implied end. When in doubt prefer the earlier date — a duplicate item is visible in review and easy to drop, a silently missed feature is not.
5. The **end** of the window is always today (`currentDate` from the system prompt). This is a "since the last run" range, not a fixed weekly cadence — if it's been two days or two months since the last covered PR, cover exactly that gap.
6. Use `since=YYYY-MM-DD` and `until=YYYY-MM-DD` (today) when fetching commits.

Before fetching any commits, state the inferred range and its source PR to the user and confirm it looks right (a PR from another workflow — e.g. a docs backfill — could theoretically carry similar text; the marker's exact key below avoids that, but a sanity check is still cheap insurance).

---

## Step 2 — Fetch Commits

Use `mcp__plugin_github_github__list_commits` (NOT `mcp__github__list_commits` — that tool has auth issues).

Fetch all 4 repos **in parallel** (single message, four tool calls):
```
owner: duplocloud-internal
repo: [each repo]
sha: [branch per table above]
since: YYYY-MM-DD  (start of week)
until: YYYY-MM-DD  (end of week)
perPage: 100
```

### An item ships only when its WHOLE stack has shipped

A frontend change reaching production does not mean the feature has. Many features need a backend half, and the two repos release independently — so UI can be live for a capability the server cannot yet fulfil. **Announcing that tells the customer they can do something they cannot.**

This is not hypothetical here. `duplo-ai-helpdesk` releases only from `main` (`rc.yaml` checks out `ref: main`; `promote.yaml` promotes that RC to production; every GitHub release targets `main`). Day-to-day backend work lands on `dev`, and `dev` → `main` release merges have been rare — at the time of writing, none since 2025-08-29, leaving hundreds of backend commits unreleased. So a `duplo-ui` feature whose server side sits on `dev` is **not** available to end users, however complete the UI looks.

For every candidate item, establish that its backend dependency has actually shipped:

1. **Does it need a backend at all?** Pure presentation — layout, navigation, validation, display formatting — does not. Anything that reads or writes data, enforces a policy, or calls an endpoint does.
2. **Which backend?** See "Two products, one UI" below. Ticket prefixes (`DUPLOAI-` vs `DUPLO-`/`CUST-`) are a weak hint that has been **wrong repeatedly** — never classify on prefix alone.
3. **Has that backend shipped?** For `duplo-ai-helpdesk`, the test is whether the supporting code is on **`main`**, not merely on `dev`:
   ```bash
   gh api repos/duplocloud-internal/duplo-ai-helpdesk/contents/<path>?ref=main   # present on main?
   gh api "repos/duplocloud-internal/duplo-ai-helpdesk/commits?sha=main&path=<path>"
   ```
   Comparing `main...dev` shows what is still unreleased.
4. **Not yet shipped → hold the item.** Do not publish it, and do not soften it into a vaguer entry. Say in the draft review which items were held and why, so the user can overrule if they know a release is imminent. A held item is picked up by a later run once its backend lands — which is exactly what the resume-from-marker mechanism is for.

When a dependency genuinely can't be determined from the code, ask rather than assuming it shipped. The asymmetry matters: a deferred item is published a month late, a wrongly-published one tells customers a feature exists when it doesn't.

### Two products, one UI — and the field-level test

`duplo-ui` is a **shared frontend serving two separate products**:

- **AI product** — backend in `duplo-ai-helpdesk`. In scope.
- **Core platform** (the older DuploCloud platform) — backend in `duplocloud-internal/duplo`, documented under `automation-platform/` in this repo. **Out of scope** for this changelog, and its docs are not touched in Step 4.

Both products manage overlapping cloud resources (RDS, EKS node groups, EFS, SQS, EC2 hosts, ElastiCache …), and `ai-helpdesk` has its **own independent implementations** of many of them — not a passthrough to the core platform. It provisions directly via the AWS SDK (`AwsPassThroughServiceBase`, `AzurePassThroughServiceBase`, `K8sPassthroughServiceBase`) with its own MongoDB-backed resource model. So "this is an AWS resource" says nothing about which product shipped it.

**Two signals, applied in order. Neither alone is sufficient.**

**Signal 1 — which UI surface?** Check the changed file paths on the `duplo-ui` PR:
```bash
gh api repos/duplocloud-internal/duplo-ui/pulls/<PR>/files --jq '.[].filename'
```
- `portal/ai-studio/…` → AI Studio (AI product surface)
- `portal/src/…` → legacy core portal → **out of scope**
- `portal/common-lib/…` → shared; judge by what else the PR touches

**Signal 2 — the field-level test (this is the one that matters).** A resource type existing in `ai-helpdesk` does **not** mean this cycle's specific new capability exists there. Repeatedly, the resource was present while the announced field was not — the UI change was surfacing a *core-platform* field through the shared frontend.

So check for the **specific field, action, or endpoint the item announces**, not the resource type:
```bash
# does the resource exist at all?
gh api "repos/duplocloud-internal/duplo-ai-helpdesk/git/trees/main?recursive=1" --jq '.tree[].path' | grep -i <resource>
# then: does THIS capability exist in its spec/model/controller?
gh api "repos/duplocloud-internal/duplo-ai-helpdesk/contents/<SpecFile>.cs?ref=main" --jq '.content' | base64 -d | grep -i <field>
```

Worked examples from a real run — same resource, opposite answers:

| Announced item | Resource in `ai-helpdesk`? | Field present? | Verdict |
|---|---|---|---|
| RDS Performance Insights | yes | `EnablePerformanceInsights` ✅ | **in scope** |
| RDS subnet group selection | yes | `DbSubnetGroupName` ✅ | **in scope** |
| EKS node group autoscaler / custom AMI / disk encryption | yes | no such fields ❌ | core platform — **exclude** |
| SQS dead letter queue | yes | no DLQ field in spec ❌ | core platform — **exclude** |
| EFS automatic backups | yes | no backup field ❌ | core platform — **exclude** |
| EC2 host AMI create/snapshot/share | yes | no such actions ❌ | core platform — **exclude** |
| AppRunner, OpenSearch, Amazon MQ, Azure VM | no controller at all ❌ | — | core platform — **exclude** |

The pattern to internalise: **resource-type presence is necessary but not sufficient.** Always confirm the specific capability. When the field isn't there, the feature belongs to the core platform and does not go in this changelog, however prominent the UI work was.

**Filter out noise commits** — skip anything that looks like:
- Version bumps (`Bump version from X to Y`)
- Image tag updates (`Update container image tags`, `Update DuploAgent image tag`)
- Merge branch commits (`Merge branch 'main' into feature/...`)
- Build/CI-only changes unless there's a meaningful feature in the message
- Fixing tests, fixing build issues (unless the underlying change is notable)

Group remaining commits by feature/PR — multi-commit PRs count as one item.

---

## Step 3 — Draft & Approve the Update List

### Step 3a — Present the draft for review

Before writing any file, present the full list of updates **in the exact `.md` format** (see format below) directly in the chat for the user to review. Do not write the file yet.

**Rules for the draft:**
- **No `Bug` items** — skip anything that is purely a bug fix
- Label each item as exactly one of: `` `Feature` `` or `` `Enhancement` ``
  - `Feature` = new capability that didn't exist before
  - `Enhancement` = improvement to an existing capability
- Each item: numbered, label tag, bold title, one-liner, 3 bullet points (fewer if genuinely only 2 noteworthy points), `Changes in:` line
- `Changes in:` uses backtick labels — pick from: `` `Backend` `` `` `Frontend` `` `` `Agent` `` `` `Helm` ``
- **Up to 25 items per section — a hard ceiling, with no floor.** At the current roughly-monthly cadence a full month of AI-product work has run to about 10–12 items once core-platform work is correctly excluded (see the field-level test in Step 2), so a section in that range is normal and needs no explanation. Merge minor related commits into one item.
- **If the list exceeds 25, the bar for inclusion is too low — raise it.** Do not publish an over-length section and flag it; fix it. In order:
  1. **Cut** the items that aren't really product news — small validation tweaks, field-level additions, copy and layout adjustments, consistency passes, internal refactors surfaced in the UI. If a reader wouldn't change what they do on learning it, it doesn't earn a numbered entry.
  2. **Merge** what remains into the capability it belongs to. Several changes to one feature area are one item with bullets, not three items.
  3. Only then check the count again.
- **Never pad to reach a number.** Do not split one capability across several items, and never promote excluded work (bug fixes, internal changes, reverted features, anything whose backend hasn't shipped) to make a section look fuller. A short section is a correct section when the period was quiet or most of the work was out of scope.
- When in doubt about a borderline item, leave it out — the changelog is a highlights document, not a complete record of every merge.
- **No technical implementation details** — this is a customer-facing document. Describe *what* changed and *why it matters*, not *how* it was built. No mention of internal class names, API endpoints, database fields, test counts, or code-level specifics.

### Format (copy exactly)

The heading below is a placeholder — the actual section heading is agreed with the user in Step 3b. What must be copied exactly is the *item* format beneath it.

```markdown
## {section heading — see Step 3b}

---

**1.** `Feature` — **Title Here**
One-sentence description of what changed and why it matters to the user.
- What users can now do (capability-first)
- What this replaces or improves
- Any notable scope or constraint worth knowing

Changes in: `Backend` `Frontend`

---
```

After presenting the draft, ask: **"Does this look right? Any changes before I write the file?"**

---

### Step 3b — Sync, write, and publish (after approval)

Once the user approves (or requests edits and approves the revision):

**1. Pull latest from the docs repo first** — before touching any files:
```bash
cd "/Users/amal/Documents/github/duplocloud/docs"
git fetch origin && git pull origin <current-branch>
```

**2. Insert the section into the public-facing product updates doc**

**Additional rule:** Keep all bullet points at the capability/outcome level. If a bullet sounds like it belongs in a pull request description, rewrite it as a user benefit.

**Ask the user how to head the section(s) — do not assume.** The right granularity depends on how often updates are being run, which changes over time:
- Roughly monthly or less often → month-only headings are usually enough (`## August 2026`).
- More frequent than monthly → headings need dates to stay distinguishable (`## August 4–18, 2026`).

Propose the format that fits the range you just covered, show the exact heading(s) you intend to use, and let the user confirm or change it. Match whatever style the existing sections in the file already use unless the user says otherwise.

Place newest first, directly after the `# Product Updates` heading.

**If a section with that heading already exists, append into it — do not create a second one.** A run covering part of a period will often be followed by another run covering the rest; the later run adds its items to the bottom of the existing section and continues its numbering, rather than opening a duplicate heading.

If the range spans more than one period, split the items into one section per period by the date the work landed.

**When one run produces several sections, order those newest-first too.** The whole page reads newest-first, and that applies within a single insert as much as between inserts — a run covering August and September writes **September above August**, not in chronological order. This is easy to get wrong: the natural way to draft is oldest-first, and inserting that block at the top leaves the newest section buried underneath. Check the final heading order before committing.

**3. Commit, push, and create a PR**

Stage only `ai-helpdesk-v2/product-updates.md`:
```bash
git add ai-helpdesk-v2/product-updates.md
git commit -m "Add product updates for {section period}"
git push origin <current-branch>
```

**The PR body must carry the checkpoint marker** — this is what Step 1 reads on the *next* run to find where to resume, so it must be present on every PR this skill creates, with no exceptions. Write the body to a file first (avoids shell-quoting issues with the HTML comment) and pass it via `--body-file`:

```bash
cat > /tmp/pr-body.md << 'EOF'
## Summary

{list all items covered, grouped by label (Features / Enhancements)}

---
_Generated by the `product-updates` skill. This was the last update produced by this skill — covering commits through {until-date, YYYY-MM-DD}. The next run resumes from that date._
<!-- product-updates-skill-marker: covered_through={until-date, YYYY-MM-DD} -->
EOF

gh pr create --title "Product updates: {section period}" --body-file /tmp/pr-body.md
```

- `{until-date}` is the **end** of the range fetched in Step 1/2 (today's date at the time of the run), in `YYYY-MM-DD` — not the start, so the next run picks up exactly where this one left off with no gap or overlap.
- The HTML comment is invisible when the PR renders on GitHub; the italic line above it is the human-visible equivalent, so anyone reading the PR (not just the skill) can see it's the checkpoint.
- Do not alter the exact key `product-updates-skill-marker:` — Step 1's search depends on it.

Do not stop here. The changelog entry announces a feature; Step 4 makes sure the docs actually describe it.

---

## Step 4 — Audit the Product Docs for Each Update

A product update entry is an announcement, not documentation. Every item published in Step 3 may also need its own doc page created or corrected, and the changelog entry cross-linked to it (the established pattern — see the existing entries that link out, e.g. `[**HelpDesk Audit Trail**](../armor/helpdesk/audit-trail.md)`).

### Step 4a — Work out what each item needs

For every item in the section just published, determine one of three outcomes. **Verify against the actual docs and the actual product code — do not infer from the commit message alone.**

1. **No doc change** — the feature is internal plumbing, or an existing page already describes it accurately.
2. **Doc change, no screenshots** — text-only. Typical when the feature is deployment/env-var driven, backend-configured, or a wording/accuracy correction to existing prose.
3. **Doc change, screenshots needed** — there is new or changed **UI** a reader has to see: a new page, new form, new fields, a new tab, a changed workflow.

To decide, for each item:
- Search the docs repo for existing coverage: `grep -ril "<feature keywords>" --include=*.md .`
- Read the page that would own it and check whether it is actually accurate, not merely adjacent — an existing page mentioning the feature name is not the same as documenting the new behaviour.
- Where the distinction matters, check the product source for whether the feature has admin UI at all. A feature with no UI surface is category 2 even if it sounds visual. Conversely, if the UI shipped but the described control doesn't exist in `main`, say so rather than documenting a draft that never shipped.

Then present the full audit to the user as a table, and wait for approval before changing anything:

| # | Update | Needs doc? | Target page | Screenshots? |
|---|--------|-----------|-------------|--------------|
| 1 | Feature name | Yes — new page | `armor/<section>/<page>.md` | No |
| 2 | Feature name | Yes — correction | `armor/<existing>.md` | Yes |
| 3 | Feature name | No — internal only | — | — |

State the reasoning for every "No", and for every "Yes" say whether it's a new page or an edit to an existing one. The user may reclassify any row — a "No" can become a "Yes", and a screenshot call can go either way. Respect the reclassification rather than re-arguing it.

### Step 4b — Text-only updates (no screenshots)

Handle these first — they're self-contained and don't need a browser.

Same draft-then-approve rhythm as Step 3, **per page**:
1. Show the user the proposed content for that page, and say exactly where it goes (new file at path X, or inserted into existing page Y under heading Z).
2. Get approval for that page.
3. Write it.

Batch the drafts into one message where several pages are small, but keep each page's destination explicit. Do not write any file before its draft is approved.

For each page written:
- Add the cross-link from the changelog entry in `ai-helpdesk-v2/product-updates.md` to the new/updated page, matching the existing link style.
- If a new page is added, update `SUMMARY.md` to place it in the nav under the right parent.
- If a new sub-page needs to nest under a currently-flat section, convert the section first (`git mv armor/x.md armor/x/README.md`) and fix that file's image paths for the new depth — see §17 of the Playwright skill, which documents this repo's unusual "one extra `../`" convention.

### Step 4c — Updates that need screenshots

These require driving the real product in a browser. **Use the Playwright documentation skill** for each one.

That skill lives at `/Users/amal/Documents/github/duplocloud/Playwright-Documentation/.claude/skill_playwright_documentation.md`. It is a plain file, not a registered skill — read it with the `Read` tool; do not try to invoke it via the `Skill` tool.

Work through screenshot items **one feature at a time**, not in parallel — each needs a live browser session and per-screenshot review.

For each:
1. Read the Playwright skill first and follow it as written. The parts that matter most here: probe before writing the full test (§1), the interactive review loop showing each PNG for approval (§1), present the script before running anything that creates or modifies real data (§12), and the sensitivity review before publishing any screenshot of real content (§15).
2. Draft in `Playwright-Documentation/Docs/<section>/` as that skill directs, then move the approved page into this repo following its §17 checklist (file layout, image-path depth, `SUMMARY.md`, copying only the referenced assets).
3. Cross-link the changelog entry to the finished page, same as 4b.

If the live product isn't reachable, or a capture session can't be completed now, do not fake it or write the page without the screenshots. Report which items are still outstanding and leave them for a follow-up run — a text page that promises screenshots it doesn't have is worse than a deferred item.

### Step 4d — Ship the doc updates

The doc work is a **separate PR** from the changelog PR in Step 3. Keeping them apart means the changelog can merge on its own cadence while doc pages go through their own review, which is how PRs #152/#153 were handled against the #150 changelog.

Title it for the coverage, e.g. `docs: cover N {Month} product updates across {area}`. Body should list each page added or changed and what it documents.

Do **not** put the `product-updates-skill-marker` comment in this PR — the marker belongs only on the Step 3 changelog PR, which is what defines the covered-through date. A second marker would create an ambiguous checkpoint.

Stage deliberately: only the doc pages, `SUMMARY.md`, and the `.gitbook/assets/` images this change actually references. Never `git add -A` — this repo's working tree routinely carries unrelated untracked files (`.DS_Store`, editor settings, stray backups).

---

## Summary of All Outputs

| # | Output | Where |
|---|--------|--------|
| 1 | Changelog section (Step 3, own PR — carries the marker) | `ai-helpdesk-v2/product-updates.md` |
| 2 | New/updated doc pages + nav + assets (Step 4, separate PR) | `armor/...`, `SUMMARY.md`, `.gitbook/assets/` |
