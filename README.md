# BINER

**Beautiful Intelligent Notion Enhancement & Reformatting**

An opinionated formatter for Notion pages. Like Prettier, but for Notion.

> **Why "BINER"?** In climbing, a *biner* (short for carabiner) is the essential link that connects everything on the wall — rope to harness, protection to anchor, climber to safety. BINER does the same for your Notion pages: it's the link between raw content and polished, professional structure. Part of the [Alpine toolkit](https://github.com/Percona-Lab) alongside [PACK](https://github.com/Percona-Lab/DK-PACK), [MYNAH](https://github.com/Percona-Lab/MYNAH), [IBEX](https://github.com/Percona-Lab/IBEX), and [SHERPA](https://github.com/Percona-Lab/SHERPA).

## What it does

BINER is a plugin for Claude that transforms plain Notion pages into professionally structured documents. It applies a consistent design system — colored section headers, structured layouts, tables, columns — so your pages look polished without manual formatting.

**Four commands:**

| Command | What it does |
|---------|-------------|
| **"Create notion page"** | Builds a new page from scratch with the design system applied |
| **"Beautify"** + a Notion URL | Reformats an existing page — preserves all your content, just makes it look great |
| **"Learn my Notion style"** + page URLs | Extracts your design preferences from sample pages and saves them |
| **"Forget my Notion style"** | Removes a saved design profile |

## Getting Started

### What you need

1. **Claude** — either [Claude Code](https://docs.claude.com/en/docs/claude-code) (terminal) or [Cowork](https://claude.ai) (desktop app)
2. **Notion connected** — Claude needs access to your Notion workspace via the Notion MCP connector

### How to install

#### One-liner (Claude Code or Cowork)

Open Claude and prompt:

```
Install this plugin: https://github.com/Percona-Lab/BINER
```

Claude will clone the repo, install the plugin to `~/.claude/plugins/biner/`, and clean up. Done.

#### ZIP upload (Cowork)

Download `biner-plugin.zip` from the
[latest release](https://github.com/Percona-Lab/BINER/releases/latest) and
upload it in Cowork under **Settings > Plugins > Upload**. This also works for
org-level installation: a team admin can upload the ZIP to make BINER available
to all members on Team or Enterprise plans.

#### Manual

1. Clone or download this repo
2. Copy the contents into `~/.claude/plugins/biner/`
3. Restart Claude (or reload plugins)

```bash
mkdir -p ~/.claude/plugins/biner
git clone https://github.com/Percona-Lab/BINER.git /tmp/biner
cp -r /tmp/biner/.claude-plugin /tmp/biner/skills ~/.claude/plugins/biner/
rm -rf /tmp/biner
```

### Verify it's installed

In Claude Code, run `/plugins` — you should see `biner` in the list. In Cowork, the plugin will appear automatically when you start a new session.

## Plugin Structure

```
biner/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata (name, version, author)
├── skills/
│   └── notion-beautifier/
│       ├── SKILL.md          # Formatting rules and design system
│       └── references/
│           ├── design-dimensions.md  # What to extract during LEARN mode
│           └── profile-schema.md     # Memory storage format for profiles
├── README.md
└── LICENSE
```

## Usage

Just tell Claude what you want:

```
Create notion page: Your Notion Page
```

```
Beautify https://www.notion.so/your-workspace/Your-Page-abc123
```

## Personalized Styles

BINER can learn your design preferences from existing Notion pages you love — similar to how [MYNAH](https://github.com/Percona-Lab/MYNAH) learns your writing voice.

```
Learn my Notion style from these pages: [URL1] [URL2] [URL3]
```

Optionally name the profile:

```
Learn my Notion style as "technical" from these pages: [URL1] [URL2] [URL3]
```

Once learned, all future Create and Beautify commands automatically apply your preferred patterns, colors, and formatting choices. Profiles are stored in your persistent memory ([PACK](https://github.com/Percona-Lab/DK-PACK) or equivalent) — not in the plugin itself. The default design system still applies if no profile exists.

## What it formats

BINER works with any type of Notion page:

- **Vision / Strategy docs** — Two-column pillars, synthesis sections, summary callouts
- **Proposals** — Colored section headers, phased plans, comparison tables
- **Goals / Metrics** — Priority headings, collapsible details, checkboxes
- **Architecture / Technical docs** — Code blocks in styled callouts, layer diagrams, reference tables
- **Workspace plans** — Principles lists, scope controls, paired columns

## Design System

BINER applies a consistent color language:

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
- **Toggle + code:** Notion's toggle blocks can't contain code blocks (the code gets stripped). BINER works around this with styled headings and callouts instead.
- **Privacy:** Pages are created as private by default. Tell Claude where to put the page if you want it somewhere specific.

## License

MIT
