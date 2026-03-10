# notion-beautifier

An opinionated formatter for Notion pages. Like Prettier, but for Notion.

## What it does

`notion-beautifier` is a Claude skill that transforms plain Notion pages into professionally structured documents with consistent visual hierarchy. It uses a design system built from real production pages — callout-based section headers, color-coded semantic meaning, columns, tables, and layered layouts.

Two commands:

- **"Create notion page"** — Builds a new page from scratch with the design system applied
- **"Beautify"** — Takes an existing Notion page URL, preserves all content, and reformats it

## Design System

The skill applies a consistent set of patterns:

- **Colored callout headers** — Red for major sections, green for next steps, blue for objectives
- **Intro callout** — Every page opens with context (owner, purpose, date)
- **Gray-wrapped tables** with yellow header rows
- **Columns** for parallel content (pillars, comparisons, paired sections)
- **Architecture layers** as stacked colored callouts
- **Blue blockquotes** for key objectives and statements
- **Colored text spans** for inline labels and status indicators

## Installation

### Claude Code / Cowork

Copy the `notion-beautifier` directory (containing `SKILL.md`) into your skills folder:

```bash
# Claude Code
cp -r notion-beautifier ~/.claude/skills/

# Or add to your project's .claude/skills/ directory
```

### Requirements

- Notion MCP connector must be connected
- Works with Claude Code, Cowork, or any Claude environment with Notion MCP access

## Usage

```
# Create a new page
Create notion page: MySQL Product Vision for 2026

# Beautify an existing page
Beautify https://www.notion.so/your-workspace/Your-Page-abc123
```

## Examples

The skill handles multiple page types:

- **Vision / Strategy docs** — Two-column pillars, synthesis sections, summary callouts
- **Proposals** — Red section headers, phased plans, comparison tables
- **Goals / Metrics** — Priority headings, toggle details, checkboxes
- **Architecture / Technical docs** — Code in gray callouts, layer diagrams, reference tables
- **Workspace plans** — Principles lists, scope controls, security + next steps columns

## Known Limitations

- Notion API doesn't support setting "full width" — toggle it manually after page creation
- `<details>` toggle blocks cannot contain code blocks (Notion strips the code). The skill uses blue_bg headings + gray callouts instead.
- Pages are created as private by default. Specify a parent page/database URL to place them elsewhere.

## License

MIT
