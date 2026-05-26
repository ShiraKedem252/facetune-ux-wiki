# Facetune UX Research & Competitive Analysis Wiki

A research repository and competitive intelligence hub for the Facetune UX team, built using the [Karpathy LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

The LLM builds and maintains a structured, interlinked wiki from raw sources. Shira (UX Researcher) curates sources, asks questions, and directs analysis. The LLM handles summarization, cross-referencing, filing, and bookkeeping. Anyone on the Facetune team (PMs, designers, data analysts, marketers) can query the wiki to find research findings and competitive intel.

**Primary interaction mode:** Cowork sessions. Drop files in `raw/`, ask to ingest, then query conversationally.

## Architecture

| Layer | Directory | Owner | Description |
|-------|-----------|-------|-------------|
| Raw sources | `raw/` | Shira | Immutable source documents - research reports, decks, exports, articles. The LLM reads but **never modifies** these. |
| Wiki | `wiki/` | LLM | Generated markdown pages - summaries, entities, concepts, comparisons, synthesis. |
| Schema | `CLAUDE.md` | Shira + LLM | This file. Conventions, workflows, and structure rules. |

## Directory Layout

```
raw/                 # Source documents - never modified by LLM
  assets/            # Downloaded images, PDFs, screenshots, data files
wiki/                # LLM-generated wiki pages
  index.md           # Content catalog (by category)
  log.md             # Chronological operation log (append-only)
.claude/skills/      # Wiki skills (auto-available in Claude Code and Cowork)
```

## Source File Types

The wiki accepts these raw source formats. The ingest workflow handles extraction from all of them:

| Format | Examples |
|--------|---------|
| `.md` / `.txt` | Research notes, Dovetail exports, discussion guides |
| `.pptx` | Research shareout decks, stakeholder presentations |
| `.pdf` | Published reports, exported research summaries |
| `.docx` | Research plans, written reports |
| `.csv` / `.xlsx` | Survey data exports, competitive feature matrices |
| `.html` | Saved web pages, competitor screenshots |

Files are placed in `raw/` as-is. The ingest skill extracts text content and creates wiki pages from them.

## Domain

This wiki covers **Facetune UX research** and the **competitive landscape** of consumer photo & video editing apps.

### In scope

- **UX research findings** - usability studies, user interviews, survey results, behavioral insights
- **Research methodology** - study designs, discussion guides, recruiting approaches, analysis frameworks
- **User segments** - personas, behavioral archetypes, needs and pain points across Facetune products
- **Product knowledge** - Facetune, Videoleap, Photoleap, Boosted features and user flows
- **Competitive analysis** - competitor products, features, pricing, UX patterns, market positioning
- **Industry trends** - photo/video editing market, creator economy, AI features in consumer apps
- **Stakeholder insights** - how research informs product, design, and marketing decisions

### Out of scope

- Internal engineering architecture or code
- LTX (B2B) product details (separate wiki exists for that)
- Financial or HR data

## Slash Commands

Four skills implement the wiki operations:

- `/wiki-research` - Research a topic online, save findings as raw source files in `raw/`
- `/wiki-ingest` - Process raw sources into wiki pages with cross-references
- `/wiki-query` - Answer questions from compiled wiki knowledge, optionally file answers
- `/wiki-lint` - Health-check the wiki (contradictions, orphans, broken links, gaps)

Typical flow: `/wiki-research` → `/wiki-ingest` → `/wiki-query` → `/wiki-lint`

## Page Format

Every wiki page uses this structure:

```markdown
---
title: Page Title
type: source | entity | concept | comparison | analysis | overview | finding | methodology | competitor | persona | product
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - raw/filename.md
tags:
  - tag1
---

# Page Title

Content here. Use [[wikilinks]] to link to other wiki pages.

## References

- [[source-summary]] - what was drawn from this source
```

### Page Types

| Type | Use for |
|------|---------|
| `source` | Summary of a raw source document |
| `entity` | A person, team, tool, or app (e.g. Facetune, Dovetail) |
| `concept` | A UX concept, framework, or methodology |
| `comparison` | Side-by-side analysis (e.g. Facetune vs Snapseed) |
| `analysis` | Synthesized insight across multiple sources |
| `overview` | High-level topic survey |
| `finding` | A specific research finding or insight |
| `methodology` | Research method, protocol, or study design |
| `competitor` | A competing product or company |
| `persona` | A user segment or behavioral archetype |
| `product` | A Facetune-family product page |

### Conventions

- Use `[[wikilinks]]` for internal wiki links (Obsidian-compatible).
- File names: lowercase, hyphenated (e.g. `wiki/mobile-editing-habits.md`).
- Citations: note inline (e.g. "According to [[source-name]], ...").
- One entity/concept per page. Split when a page grows beyond ~300 lines.
- Tag pages with relevant categories from the index.

## Workflows

### Ingest

1. **Read** the source document in full.
2. **Discuss** key takeaways with the user.
3. **Create a source summary page** in `wiki/` (type: source).
4. **Update existing pages** affected by the new source.
5. **Create new pages** for entities/concepts not yet covered.
6. **Update `wiki/index.md`** with new entries.
7. **Append to `wiki/log.md`** with date and pages touched.

### Query

1. **Read `wiki/index.md`** to identify relevant pages.
2. **Read the relevant wiki pages** (wiki is compiled knowledge; raw is ground truth).
3. **Synthesize an answer** with citations to wiki pages.
4. **Optionally file the answer** as a new wiki page if it's valuable synthesis.

### Lint

- [ ] **Broken wikilinks** - verify `[[wikilink]]` targets exist
- [ ] **Orphan pages** - no inbound `[[wikilinks]]`
- [ ] **Missing pages** - wikilinks pointing to non-existent pages
- [ ] **Contradictions** - conflicting claims across pages
- [ ] **Stale claims** - superseded by newer research or product changes
- [ ] **Missing cross-references** - related pages not linking to each other
- [ ] **Index drift** - `wiki/index.md` out of sync with actual pages
- [ ] **Data gaps** - important questions the wiki can't answer

### Index and Log Rules

**wiki/index.md** - catalog by category, `- [[page-name]] - one-line summary`, updated on every ingest.

**wiki/log.md** - append-only, `## [YYYY-MM-DD] verb | Subject`, parseable with grep.

## Audience Guidelines

The wiki serves the broader Facetune unit (~72 people). When generating wiki pages and query answers:

- Write findings in plain language - avoid jargon like "McNemar's test" or "thematic saturation" in headlines. Save methodology details for a separate section or footnote.
- Lead with the "so what" - what should a PM or designer take away from this finding?
- Always include: what was studied, key finding, sample size, date, and implications.
- For competitive analysis: note the observation date prominently. Competitor products change fast.

## Tips

- For large sources (decks with 30+ slides, long PDFs), read in sections.
- Prefer adding to existing pages over creating new ones until they get too long.
- Always check for existing pages before creating new ones.
- Research findings should cite their study methodology and sample size.
- Competitive analysis should note the date of observation.
- When ingesting research reports, extract both findings AND methodology details.
- When ingesting presentation decks, the headlines often ARE the findings (Shira's style). Extract them as the primary insights.
