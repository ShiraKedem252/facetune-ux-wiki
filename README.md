# Facetune UX Research & Competitive Analysis Wiki

A living knowledge base for Facetune UX research findings and competitive intelligence. Built using the [Karpathy LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## What this is

An LLM-maintained wiki where:
- **Shira** (UX Researcher) adds raw source files — research reports, presentation decks, Dovetail exports, competitive analyses, articles
- **Claude** processes them into structured, cross-linked wiki pages with citations
- **Anyone on the Facetune team** can query the wiki to find research findings, user insights, and competitive intel

## Quick start

### In Cowork (recommended)

1. Open this folder in a Cowork session
2. Drop your research files into `raw/`
3. Say "ingest the new files in raw/" — Claude will extract content, summarize key findings, and create wiki pages
4. Ask questions like "what do we know about how users edit on mobile vs desktop?" — Claude will search the wiki and synthesize an answer

### In Claude Code

1. Open this folder in Claude Code (skills auto-detect)
2. Use slash commands:
   - `/wiki-ingest` — process new files in `raw/` into wiki pages
   - `/wiki-query "your question"` — search the wiki for answers
   - `/wiki-research "topic"` — research a topic online and save sources
   - `/wiki-lint` — health-check the wiki for broken links, stale content, gaps

## Folder structure

```
raw/                    # Your source files (never modified by the LLM)
  assets/               # Images, PDFs, data files
wiki/                   # LLM-generated wiki pages (markdown)
  index.md              # Table of contents by category
  log.md                # Chronological log of all operations
.claude/skills/         # Wiki commands
CLAUDE.md               # Schema and conventions
```

## What goes in `raw/`

Any file with knowledge you want in the wiki:

| File type | Examples |
|-----------|---------|
| `.pptx` | Research shareout decks, stakeholder presentations |
| `.pdf` | Published reports, exported research summaries |
| `.docx` | Research plans, written reports |
| `.md` / `.txt` | Dovetail exports, discussion guides, notes |
| `.csv` / `.xlsx` | Survey data, competitive feature matrices |

## How it works

1. **You add sources** to `raw/` — research reports, decks, competitive analyses, articles
2. **Claude ingests** — reads each source, extracts findings, creates wiki pages with cross-references
3. **Wiki grows** — each new source adds to and connects with existing knowledge
4. **You query** — ask questions in natural language; Claude synthesizes answers from compiled wiki knowledge
5. **You maintain** — periodic lint checks catch stale info, broken links, and coverage gaps

## Wiki categories

- **Research Findings** — insights from studies, usability tests, surveys
- **User Segments & Personas** — who our users are
- **Products** — Facetune, Videoleap, Photoleap, Boosted
- **Competitive Landscape** — competitors, features, positioning
- **Research Methodology** — study designs, protocols, guides
- **Industry & Trends** — market and creator economy trends
- **Concepts & Frameworks** — recurring UX themes and mental models

## Credits

Pattern: [Andrej Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Reference implementation: [Beckdotan/ltx-wiki](https://github.com/Beckdotan/ltx-wiki).
