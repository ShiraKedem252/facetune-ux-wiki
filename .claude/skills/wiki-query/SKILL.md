description: Answer questions by reading the compiled wiki. Use when the user asks a question about research findings, competitors, user behavior, product features, or anything the wiki might know. Also use for "what do we know about", "summarize", "compare", or "what's missing".

---

# Wiki Query

Answer questions by reading the compiled wiki — not raw sources. The wiki is the compiled knowledge; raw sources are the ground truth only when deeper detail is needed.

**Working directory:** The wiki project root (contains `raw/`, `wiki/`, `CLAUDE.md`).

## Arguments

`$ARGUMENTS` — The question or topic to investigate.

## Workflow

### 1. Read the Index

Start by reading `wiki/index.md` to identify relevant pages. This is the primary navigation tool.

### 2. Read Relevant Pages

Read the wiki pages identified from the index. Follow `[[wikilinks]]` to discover related pages. Read as many as needed to build a complete answer.

If wiki pages are insufficient, read the referenced `raw/` sources for deeper detail.

### 3. Synthesize an Answer

Compose an answer that:
- **Cites wiki pages** - reference specific pages by name (e.g. "According to [[mobile-editing-habits]], 72% of users edit on their phone")
- **Synthesizes across pages** - don't just summarize one page; connect information from multiple pages
- **Notes confidence** - flag where information might be incomplete or contradictory
- **Is concise** - answer the question directly, then provide supporting detail
- **Notes dates** - flag when findings might be stale (competitive landscape changes fast)

### 4. Optionally File the Answer

If the answer represents valuable synthesis — a comparison, analysis, connection, or insight that doesn't exist in the wiki yet — ask the user:

> "This answer synthesizes information from multiple pages. Want me to save it as a new wiki page?"

If yes:
- Create a new wiki page (type: `analysis` or `comparison`)
- Add it to `wiki/index.md`
- Append to `wiki/log.md`: `## [YYYY-MM-DD] query | Question summary`

## Output Formats

Adapt the answer format to the question type:

- **Factual question** → direct answer with citations
- **"What do we know about X"** → structured summary with sections
- **Competitor comparison** → markdown table with citations
- **"What's missing"** → gap analysis with suggestions for sources to research
- **Research finding** → finding + methodology + sample size + confidence
- **User behavior question** → insight + supporting data points + user quotes if available
- **"How should we study X"** → methodology recommendations from wiki knowledge

## Audience Awareness

The wiki serves the entire Facetune unit — not just researchers. Adapt your language:
- For PMs asking about user behavior → lead with the actionable insight, then the evidence
- For designers asking about UX patterns → focus on what users do and why, include competitor examples
- For marketers asking about segments → describe the user in their language (demographics, motivations, behaviors)
- For anyone → avoid research jargon in the main answer. Put methodology details in a footnote or "Study details" section.

## Tips

- The wiki is the first source of truth — it contains compiled, cross-referenced knowledge
- If the wiki can't answer the question, say so and suggest what sources to look for (or suggest `/wiki-research`)
- Good queries compound: file valuable answers back into the wiki
- For broad questions, read more pages; for specific questions, grep for keywords
- Pay attention to dates — a competitor analysis from 6 months ago may be outdated
- When queried in Cowork, respond conversationally — the user can't run slash commands, so offer to do follow-up actions yourself
