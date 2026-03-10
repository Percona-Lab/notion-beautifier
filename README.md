# notion-beautifier

An opinionated formatter for Notion pages. Like Prettier, but for Notion.

## What it does

notion-beautifier is a skill for Claude that transforms plain Notion pages into professionally structured documents. It applies a consistent design system — colored section headers, structured layouts, tables, columns — so your pages look polished without manual formatting.

**Two commands:**

| Command | What it does |
|---------|-------------|
| **"Create notion page"** | Builds a new page from scratch with the design system applied |
| **"Beautify"** + a Notion URL | Reformats an existing page — preserves all your content, just makes it look great |

## Getting Started

### What you need

1. **Claude** — either [Claude Code](https://docs.claude.com/en/docs/claude-code) (terminal) or [Cowork](https://claude.ai) (desktop app)
2. **Notion connected** — Claude needs access to your Notion workspace via the Notion MCP connector

### How to install

#### One-liner (Claude Code)

Open Claude Code and prompt:

```
Install this skill: https://github.com/Percona-Lab/notion-beautifier
```

Claude will clone the repo, copy the skill files to `~/.claude/skills/notion-beautifier/`, and clean up. Done.

#### Manual

1. Clone or download this repo
2. Copy `SKILL.md` into `~/.claude/skills/notion-beautifier/`
3. Restart Claude (or reload skills)

```bash
mkdir -p ~/.claude/skills/notion-beautifier
git clone https://github.com/Percona-Lab/notion-beautifier.git /tmp/notion-beautifier
cp /tmp/notion-beautifier/SKILL.md ~/.claude/skills/notion-beautifier/
rm -rf /tmp/notion-beautifier
```

### Verify it's installed

In Claude Code, run `/skills` — you should see `notion-beautifier` in the list. In Cowork, the skill will appear automatically when you start a new session.

## Usage

Just tell Claude what you want:

```
Create notion page: Your Notion Page
```

```
Beautify https://www.notion.so/your-workspace/Your-Page-abc123
```

## What it formats

The skill works with any type of Notion page:

- **Vision / Strategy docs** — Two-column pillars, synthesis sections, summary callouts
- **Proposals** — Colored section headers, phased plans, comparison tables
- **Goals / Metrics** — Priority headings, collapsible details, checkboxes
- **Architecture / Technical docs** — Code blocks in styled callouts, layer diagrams, reference tables
- **Workspace plans** — Principles lists, scope controls, paired columns

## Design System

The skill applies a consistent color language:

| Color | Meaning |
|-------|---------|
| Red | Major section headers, critical warnings |
| Blue | Key objectives, commitments, highlighted statements |
| Green | Next steps, success metrics, positive outcomes |
| Yellow | Caution areas, table header rows, security/governance |
| Purple | Innovation sections, advanced features |
| Orange | Priority 1 items, phased labels |
| Gray | Reference tables, notes, supplementary context |

## Known Limitations

- **Full width:** The Notion API doesn't support setting pages to full width — toggle it manually after creation.
- **Toggle + code:** Notion's toggle blocks can't contain code blocks (the code gets stripped). The skill works around this with styled headings and callouts instead.
- **Privacy:** Pages are created as private by default. Tell Claude where to put the page if you want it somewhere specific.

## License

MIT
