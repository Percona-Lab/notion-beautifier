---
name: notion-beautifier
description: |
  Create beautifully formatted Notion pages with professional visual hierarchy using callouts, columns, colored headings, toggles, tables, and layered layouts. MANDATORY TRIGGERS: Use this skill whenever the user says "create notion page", "make a notion page", "build a notion page", "beautify" (followed by a Notion URL or page reference), or any variation involving creating or formatting content in Notion. Also trigger when the user asks to format, structure, lay out, or redesign a Notion page, or wants to turn content into a well-designed Notion page. The "beautify" command specifically means: fetch the existing page, preserve all content, and reformat it using the design system. This skill handles the formatting and structure — content instructions come separately from the user.
---

# Notion Page Creator

You create visually polished, professionally structured Notion pages. Your job is to apply a consistent design system that makes pages scannable, beautiful, and information-dense without feeling cluttered.

This skill focuses on **formatting and structure**. The user will provide the content or topic separately — your role is to make it look great in Notion using the Notion-flavored Markdown format that the Notion MCP tools accept.

## Before You Start

Before creating any page, fetch the Notion enhanced markdown spec to ensure you have the latest syntax:
```
notion-fetch: id = "notion://docs/enhanced-markdown-spec"
```

If this fails, use the reference patterns documented below — they are extracted from real, working Notion pages.

## Page Creation Defaults

- **Privacy**: Pages are created as **private** (no parent specified) unless the user specifies a location. If the user provides a parent page or database, use that.
- **Icons**: Always give the page an emoji icon that reflects its topic. Use a relevant emoji, not a generic one.
- **Title**: Use the user's provided title. Don't add emoji to the title itself — that's what the icon is for.

## The Design System

These patterns come from real production pages and create a consistent, professional look. The key insight: Notion's callout blocks are the primary structural element — they create visual containment, color coding, and hierarchy that plain headings can't achieve.

### 1. Intro Callout (Every Page Gets One)

Every page opens with a plain callout that establishes context. This orients the reader immediately.

```markdown
::: callout
	**Owner:** <mention-user url="user://..."/>
	**Purpose:** Brief description of what this page is and why it exists.
	*Additional context or notes in italics if needed.*
:::
```

If no owner is relevant, use the callout for a brief executive summary or page purpose statement instead.

### 2. Section Headers as Colored Callouts

Major sections use colored callout blocks as headers rather than plain headings. This creates strong visual separation between sections.

**Red callout headers** for primary sections (executive summaries, major topic areas):
```markdown
::: callout {color="red_bg"}
	### **Section Title**
:::
```

**Green callout headers** for positive/success sections (next steps, achievements, results):
```markdown
::: callout {color="green_bg"}
	### **Section Title**
:::
```

The content for each section goes in a **separate plain callout** immediately below the header callout. This creates a "header bar + content block" pattern:
```markdown
::: callout {color="red_bg"}
	### **The Problem**
:::
::: callout
	Description of the problem goes here in the content callout...
:::
```

### 3. Color Coding System

Colors have consistent semantic meaning:

| Color | Use For |
|-------|---------|
| `red_bg` | Section headers, critical warnings, key evidence |
| `blue_bg` | Key commitments, objectives, highlighted statements |
| `green_bg` | Success metrics, next steps, positive outcomes, download links |
| `yellow_bg` | Caution areas, security/governance, priority 2 items, table header rows |
| `orange_bg` | Priority 1 headings, phased labels |
| `purple_bg` | Innovation sections, advanced features, architecture layers |
| `gray_bg` | Reference tables, notes, context sections |

### 4. Colored Background Headings for Priority/Category Labels

When you need inline section markers (like priority levels), use headings with background colors:
```markdown
## Priority 1 Goals {color="orange_bg"}
## Priority 2 Goals {color="yellow_bg"}
```

### 5. Blue Blockquotes for Key Objectives

Inside callouts, use blockquotes with blue backgrounds to highlight the core objective or key statement:
```markdown
::: callout
	## **Section Title**
	> **Objective:** The main goal stated clearly and concisely. {color="blue_bg"}
:::
```

### 6. Columns for Side-by-Side Content

Use columns when you have parallel content — pillars, comparisons, paired sections (like Security + Next Steps, or Notes + To-Do):

```markdown
<columns>
	<column>
		::: callout {color="yellow_bg"}
			## **Left Section**
			Content here...
		:::
	</column>
	<column>
		::: callout {color="green_bg"}
			## **Right Section**
			Content here...
		:::
	</column>
</columns>
```

Two columns is the sweet spot. Three works for brief items. Don't exceed three.

### 7. Architecture/Layer Callouts

When showing layers, phases, or stacked concepts, use nested colored callouts to create a visual stack:

```markdown
::: callout
	## **Architecture**
	::: callout {color="yellow_bg"}
		**Layer 1** - Description of first layer.
	:::
	::: callout {color="green_bg"}
		**Layer 2** - Description of second layer.
	:::
	::: callout {color="purple_bg"}
		**Layer 3** - Description of third layer.
	:::
	::: callout {color="red_bg"}
		**Layer 4** - Description of fourth layer.
	:::
:::
```

### 8. Toggle Sections for Detail-Heavy Content

For content that's important but shouldn't dominate the page (goals with metrics, Jira tickets, reference data), use toggle/details blocks inside colored callouts:

```markdown
::: callout {color="gray_bg"}
	<details>
	<summary>**Goal 1: Descriptive Title** </summary>
		Explanation of the goal.
		- **Signal:** What indicates progress.
			- **Metric:** How you measure it specifically.
			- **Metric:** Another measurement.
	</details>
:::
```

For top-level collapsible sections, use toggle headings:
```markdown
## Section That Can Collapse {toggle="true"}
```

### 9. Tables

Wrap tables in gray callouts for visual containment. Use colored header rows:

```markdown
::: callout {color="gray_bg"}
	<table header-row="true">
	<tr color="yellow_bg">
	<td>**Column 1**</td>
	<td>**Column 2**</td>
	<td>**Column 3**</td>
	</tr>
	<tr>
	<td>Data</td>
	<td>Data</td>
	<td>Data</td>
	</tr>
	</table>
:::
```

### 10. Colored Text for Inline Emphasis

Use colored spans for labels and inline emphasis:
```markdown
<span color="brown">**Label:**</span> Description follows the label.
<span color="blue">*Italic blue for vision/aspiration statements.*</span>
<span color="red">*Red italic for important warnings or notes.*</span>
<span color="gray">*Gray italic for subtitles and supplementary context.*</span>
<span color="green">Green for positive status indicators.</span>
```

### 11. Labeled Steps with Background Colors

For phased plans or numbered steps, use background-colored labels inline:
```markdown
::: callout
	Step 1: Adopt the Technology {color="green_bg"}
	Description of step 1...

	Step 2: Build the Partnership {color="yellow_bg"}
	Description of step 2...

	Step 3: Define the Value Proposition {color="blue_bg"}
	Description of step 3...
:::
```

### 12. Bottom Navigation / Link Blocks

For linking to related pages, use small colored callouts in columns:
```markdown
<columns>
	<column>
		::: callout {color="red_bg"}
			<page url="https://...">Key Evidence</page>
		:::
	</column>
	<column>
		::: callout {color="green_bg"}
			<page url="https://...">Strategic Plan</page>
		:::
	</column>
</columns>
```

## Page Type Templates

Choose the template that best fits the user's content, then adapt as needed.

### Vision / Strategy Document
1. Intro callout (owner, purpose)
2. Two-column layout for core pillars (blue_bg + purple_bg callout headers)
3. Balance/synthesis callout (yellow_bg header)
4. Summary callout (blue_bg header with icon)
5. Link blocks at bottom

### Proposal Document
1. Title heading + gray subtitle
2. Red callout section headers: Executive Summary → Problem → Solution → Rationale → Resource Plan → Next Steps
3. Each section: colored header callout + content callout below it
4. Steps within solution use green_bg/yellow_bg/blue_bg labels
5. Phased plan callouts

### Goals / Metrics Document
1. Two main columns (e.g., "Download Stats" vs "Activation Stats")
2. Green callout column headers
3. Priority headings with orange_bg / yellow_bg
4. Toggle/details blocks for each goal inside colored callouts
5. Bottom section: columns with Notes + To-Do (checkboxes)
6. Collapsible Jira/ticket sections

### Workspace / Plan Document
1. Intro callout with owner, purpose, and colored italic note
2. Goal callout with blue blockquote
3. Principles callout with emoji bullets
4. Gray callout wrapping a reference table
5. Architecture section with layered colored callouts
6. Scope/privacy controls as nested callouts per platform
7. Two-column footer: Security + Next Steps

## Commands

### "Create notion page" — Build a new page from scratch
1. **Read the user's content instructions** — they'll tell you what the page is about.
2. **Pick the closest template** from the Page Type Templates section and adapt it.
3. **Use `notion-create-pages`** to create the page. Set no parent (private) unless told otherwise.
4. **Apply the design system consistently** — every section should use the callout patterns, not bare markdown headings.
5. **Don't over-format** — if a section is short, a simple callout is fine. The patterns above are tools, not mandates. A page with 3 well-chosen patterns beats one that uses all 12 for no reason.

### "Beautify" — Reformat an existing Notion page
When the user says "beautify" followed by a Notion URL or page reference:
1. **Fetch the page** using `notion-fetch` to get the current content.
2. **Preserve all content exactly** — don't add, remove, or rewrite any text, code, or data. This is a formatting operation, not an editing one.
3. **Apply the design system** — restructure the page using callout patterns, colored section headers, tables in gray callouts, columns where parallel content exists, and the full visual hierarchy.
4. **Use `notion-update-page` with `replace_content`** to apply the new formatting.
5. **Understand the content type** — an architecture doc with code should show code inline (not hidden in toggles). A strategy doc should use pillars and columns. Match the formatting to what the content actually is.

## Common Mistakes to Avoid

- **Bare headings without callouts**: Plain `## Heading` looks weak in Notion. Wrap sections in callouts or use colored heading backgrounds.
- **Too many nested levels**: One level of nesting (callout inside callout) is great. Two levels is the max. Beyond that, restructure.
- **Inconsistent colors**: Pick 3-4 colors per page and use them consistently. Don't rainbow every section.
- **Forgetting the intro callout**: Every page needs one. It's the first thing readers see.
- **Giant walls of text in callouts**: Break up long content with sub-callouts, toggles, or columns.
- **NEVER put code blocks inside `<details>` toggles**: Notion strips code from inside `<details><summary>` blocks — the toggle renders but the code disappears. Instead, use a blue_bg heading above a gray callout containing the code block directly.
- **Don't hide important content in toggles**: Toggles are useful for truly supplementary info, but if the content is the point of the page (like code in an architecture doc), show it inline.
