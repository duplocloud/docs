---
name: gitbook-docs
description: Edit, write, and review GitBook documentation files. Use when creating or updating markdown pages, managing SUMMARY.md navigation, applying GitBook syntax (hints, tabs, steppers, expandable blocks, cards, columns, embeds), configuring .gitbook.yaml, working with variables and expressions, or auditing documentation structure in a GitBook-synced repository.
license: Proprietary. See https://policies.gitbook.com/terms-of-service for GitBook terms.
compatibility: Designed for Claude Code. Requires access to a GitBook-synced Git repository.
metadata:
  source: https://gitbook.com/docs/skill.md
  version: "1.0"
---

# GitBook Documentation Skill

Use this skill when writing, editing, reviewing, or restructuring any GitBook documentation page.

---

## Working with existing content

When starting work on an existing GitBook space:

1. **Read `SUMMARY.md` first** — it defines the complete navigation tree, page hierarchy, and relative paths to every file.
2. **Check `.gitbook.yaml`** — confirms the root directory, custom readme/summary paths, and any redirects.
3. **Check `.gitbook/vars.yaml`** — lists space-level variables referenced across pages.
4. **Explore `.gitbook/assets/`** — all uploaded images live here; reference them as `../.gitbook/assets/filename.png`.

---

## File structure

```
/
  .gitbook/
    assets/        # GitBook-managed images and files
    includes/      # Reusable content blocks (each exported as a .md file)
    vars.yaml      # Space-level variables
  .gitbook.yaml    # Space configuration
  README.md        # Homepage
  SUMMARY.md       # Table of contents / navigation
  section-name/
    README.md      # Section index
    page.md
```

---

## Page format

Every page must begin with YAML frontmatter, then a level-1 heading:

```markdown
---
description: One sentence used for SEO and navigation previews. Keep under 160 characters.
---

# Page Title
```

**Available frontmatter fields:**

```yaml
---
description: Page description
icon: book-open
hidden: true
vars:
  my_var: value
layout:
  width: default        # or 'wide'
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---
```

---

## SUMMARY.md rules

`SUMMARY.md` controls the GitBook sidebar. Every page must appear here; every entry must point to an existing file.

```markdown
# Summary

## Section heading

* [Page title](path/to/page.md)
  * [Child page](path/to/child.md)

## Another section

* [Another page](another.md)
```

- Use `##` headings for section groups (visible as sidebar section labels).
- Use `*` unordered list items for page links.
- Indent with spaces (not tabs) for nesting.
- Paths are relative to the repo root (or the `root:` set in `.gitbook.yaml`).
- Do not reference the same file twice.

When adding a page: create the file, then add the SUMMARY.md entry.
When removing a page: delete the file, remove the SUMMARY.md entry, update any cross-links.

---

## Essential custom blocks

For full syntax details, see [references/blocks.md](references/blocks.md).

### Hints

```markdown
{% hint style="info" %}
Informational context. Use this by default.
{% endhint %}

{% hint style="warning" %}
Something to be aware of before proceeding.
{% endhint %}

{% hint style="danger" %}
Irreversible or destructive action.
{% endhint %}

{% hint style="success" %}
Positive outcome or confirmation.
{% endhint %}
```

### Tabs

```markdown
{% tabs %}
{% tab title="Tab One" %}
Content here.
{% endtab %}
{% tab title="Tab Two" %}
Content here.
{% endtab %}
{% endtabs %}
```

### Stepper (sequential instructions)

```markdown
{% stepper %}
{% step %}
## Step title
Step content.
{% endstep %}
{% step %}
## Next step
Content.
{% endstep %}
{% endstepper %}
```

### Expandable

```markdown
<details>
<summary>Optional detail heading</summary>

Content shown when expanded.

</details>
```

### Columns (2-column max)

```markdown
{% columns %}
{% column %}
Left content.
{% endcolumn %}
{% column %}
Right content.
{% endcolumn %}
{% endcolumns %}
```

### Reusable content

```markdown
{% include "/reusable-content/rc12345" %}
```

---

## Variables and expressions

**Space-level** — defined in `/.gitbook/vars.yaml`:
```yaml
latest_version: v3.0.4
product_name: DuploCloud
```

**Page-level** — defined in page frontmatter:
```yaml
vars:
  section_version: v2.1
```

**Usage in content:**
```markdown
<code class="expression">space.vars.latest_version</code>
<code class="expression">page.vars.section_version</code>
```

---

## Links

- **Internal pages**: use relative file paths — `[text](page.md)`, `[text](../folder/page.md)`
- **External**: `[text](https://example.com)`
- **Never** use absolute paths for internal pages.

---

## When to use which block

| Need | Block |
|---|---|
| Sequential instructions | `{% stepper %}` |
| Alternative options | `{% tabs %}` |
| Optional/advanced detail | `<details>` |
| Important warnings or tips | `{% hint %}` |
| Side-by-side comparison | `{% columns %}` |
| Changelog / release notes | `{% updates %}` |
| Visual navigation cards | `<table data-view="cards">` |
| Downloadable file | `{% file %}` |
| Call-to-action link | `<a class="button">` |
| Repeated content across pages | `{% include %}` |
| Dynamic variable display | `<code class="expression">` |

---

## Common pitfalls

- Do not reference the same markdown file twice in `SUMMARY.md`.
- Always close custom blocks (`{% endtab %}`, `{% endhint %}`, `{% endstepper %}`, etc.).
- OpenAPI specs **cannot** be embedded directly in markdown — they must be uploaded via the GitBook API, CLI, or UI, then referenced with `{% openapi src="..." %}`.
- When using Git Sync, manage `README.md` only through your repository to avoid conflicts.
- Avoid deeply nested lists in `SUMMARY.md` — keep hierarchy shallow and clear.

---

## Git Sync best practices

- Make structural changes (navigation order, new sections) via `SUMMARY.md` in Git.
- Make content changes consistently in one place — either Git or the GitBook UI.
- Use branch-based workflows for significant updates.
- Resolve merge conflicts in Git, not the GitBook UI.
