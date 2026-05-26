description: Research a topic online and save findings as raw source files. Use when the user says "research", "find info about", "look up", "what's out there on", or wants to add external knowledge about competitors, UX patterns, market trends, or industry benchmarks.

---

# Wiki Research

Research topics online and save findings as raw markdown source files in `raw/` for later ingestion into the wiki.

**Working directory:** The wiki project root (contains `raw/`, `wiki/`, `CLAUDE.md`).

## Arguments

`$ARGUMENTS` — The topic or question to research.

## Workflow

### 1. Scope the Research

Based on `$ARGUMENTS`, define 3-10 specific research areas. Present them to the user in a table:

| # | Research Area | What we're looking for |
|---|--------------|----------------------|
| 1 | ... | ... |

Ask the user to confirm, add, or remove areas before proceeding.

### 2. Check Existing Wiki

Read `wiki/index.md` to see what the wiki already covers on this topic. Avoid duplicating existing knowledge — focus on gaps.

### 3. Research and Save

For each research area:

- Use WebSearch to find relevant sources (articles, app store pages, reviews, blog posts, research papers, competitor websites)
- Use WebFetch to retrieve full content from the best sources
- Save each source as a markdown file in `raw/`

**File naming:** Use specific, descriptive names with prefixes:
- `competitor-` for competitor analysis (e.g. `raw/competitor-snapseed-features-apr-2026.md`)
- `trend-` for industry trends (e.g. `raw/trend-ai-photo-editing-2026.md`)
- `review-` for app reviews or user feedback (e.g. `raw/review-facetune-app-store-apr-2026.md`)
- `article-` for blog posts or news (e.g. `raw/article-creator-economy-tools-2026.md`)
- `study-` for research papers or studies (e.g. `raw/study-mobile-photo-editing-habits.md`)
- `ux-pattern-` for UX pattern references (e.g. `raw/ux-pattern-onboarding-flows.md`)

**File format:**
```markdown
---
source_url: https://...
retrieved: YYYY-MM-DD
type: article | competitor-page | app-review | research-paper | blog | documentation
---

# Title

[Full content here — actual text, not just links]
```

### 4. Report Results

Summarize what was found:
- Total files saved
- Files per research area
- Key findings and surprises
- Gaps that need further research
- Suggest running `/wiki-ingest` next

## Guidelines

- One topic per file — the wiki will synthesize across sources
- Include actual content, not just links
- Note the date — competitor features and market data go stale fast
- For competitor analysis, capture: features, pricing, target audience, UX strengths/weaknesses, recent changes
- For UX patterns, capture: the pattern, where it's used, pros/cons, examples
- Check existing `raw/` files to avoid saving duplicates

## Scaling

- 1-3 research areas → work sequentially
- 4-10 research areas → use subagents (one per area) in parallel
- 10+ research areas → batch into thematic groups, run parallel batches
