# GitBook Custom Blocks — Full Reference

Complete syntax reference for all GitBook custom blocks. Load this file when you need detailed examples beyond the quick reference in SKILL.md.

---

## Tabs

Use for alternative content: different languages, platforms, or configuration approaches.

````markdown
{% tabs %}
{% tab title="JavaScript" %}
```javascript
const greeting = 'Hello World';
console.log(greeting);
```
{% endtab %}

{% tab title="Python" %}
```python
greeting = "Hello World"
print(greeting)
```
{% endtab %}
{% endtabs %}
````

---

## Stepper

Use for ordered, sequential processes — installation guides, tutorials, onboarding.

```markdown
{% stepper %}
{% step %}
## First step

Complete the initial setup by installing dependencies.
{% endstep %}

{% step %}
## Second step

Configure your environment variables.
{% endstep %}

{% step %}
## Third step

Run the application.
{% endstep %}
{% endstepper %}
```

---

## Hints

```markdown
{% hint style="info" %}
Informational hint with helpful context.
{% endhint %}

{% hint style="warning" %}
Be careful when running this in production.
{% endhint %}

{% hint style="danger" %}
This action cannot be undone. Make sure you have backups.
{% endhint %}

{% hint style="success" %}
Your configuration has been saved successfully.
{% endhint %}
```

---

## Expandable (details)

Use for optional deep-dives, advanced config, FAQ answers, or content that would clutter the main flow.

````markdown
<details>
<summary>Advanced Configuration Options</summary>

Here you can find detailed information about advanced settings.

```yaml
advanced:
  option1: value1
  option2: value2
```
</details>
````

---

## Columns

Two-column max. Use for side-by-side comparisons, before/after, pros/cons.

```markdown
{% columns %}
{% column %}
### Before

Old implementation that was inefficient.
{% endcolumn %}

{% column %}
### After

New optimized approach with better performance.
{% endcolumn %}
{% endcolumns %}
```

---

## Updates (changelog)

Use for product updates, release notes, changelogs.

```markdown
{% updates format="full" %}
{% update date="2024-01-15" %}
# Version 2.0 Released

Added dark mode and improved search.
{% endupdate %}

{% update date="2024-01-01" %}
# Bug Fixes

Fixed several community-reported issues.
{% endupdate %}
{% endupdates %}
```

---

## Cards

Visual navigation cards. Use for dashboards, feature overviews, linking to related pages.

```markdown
<table data-view="cards">
  <thead>
    <tr>
      <th>Title</th>
      <th data-card-target data-type="content-ref">Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Getting Started</td>
      <td><a href="getting-started/quickstart.md">Quick Start</a></td>
    </tr>
    <tr>
      <td>API Reference</td>
      <td><a href="api-reference/overview.md">API Docs</a></td>
    </tr>
  </tbody>
</table>
```

---

## Embeds

Embed external content: YouTube videos, CodePen, interactive demos.

```markdown
{% embed url="https://www.youtube.com/watch?v=example" %}

{% embed url="https://codepen.io/username/pen/example" %}
```

---

## Files (downloadable)

```markdown
{% file src="https://example.com/document.pdf" %}
Complete documentation in PDF format.
{% endfile %}
```

---

## Buttons

```markdown
<a href="https://example.com/download" class="button primary">Download Now</a>

<a href="https://docs.example.com" class="button secondary">View Documentation</a>

<!-- With icon (Font Awesome name without fa- prefix) -->
<a href="https://github.com/user/repo" class="button primary" data-icon="github">View on GitHub</a>
```

---

## Code blocks with titles

````markdown
{% code title="index.js" %}
```javascript
const foo = 'bar';
console.log(foo);
```
{% endcode %}
````

---

## Reusable content includes

Reusable blocks are created through the GitBook UI and exported to `.gitbook/includes/`. Reference them by their ID:

```markdown
{% include "/reusable-content/rc12345" %}
```

---

## OpenAPI

**Cannot be embedded directly in markdown.** Must be uploaded via API, CLI, or UI first. Once uploaded, reference with:

```markdown
{% openapi src="https://api.example.com/openapi.json" path="/users" method="get" %}
[OpenAPI spec](https://api.example.com/openapi.json)
{% endopenapi %}
```

---

## Nested markdown in custom blocks

Standard markdown works inside all custom block tags:

````markdown
{% tabs %}
{% tab title="Example" %}
This tab contains markdown:

- Bullet points work
  - Nested bullets too
- **Bold** and *italic*
- `inline code`

```javascript
// Code blocks work too
const example = true;
```
{% endtab %}
{% endtabs %}
````
