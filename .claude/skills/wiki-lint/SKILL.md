description: Run a health check on the wiki. Use when the user says "lint", "check wiki health", "audit", "find issues", or after a large batch of ingests. Finds contradictions, stale claims, orphan pages, missing pages, broken wikilinks, missing cross-references, data gaps, and index drift.

---

# Wiki Lint

Systematic quality assurance for the wiki. Run this after major ingests or periodically to keep the wiki healthy.

**Working directory:** The wiki project root (contains `raw/`, `wiki/`, `CLAUDE.md`).

## Checks

### 1. Broken Wikilinks
Scan all wiki pages for `[[wikilinks]]` and verify each target file exists.
- **Fix:** Create missing pages or correct the link.

### 2. Orphan Pages
Find wiki pages with zero inbound `[[wikilinks]]` from other pages.
- **Fix:** Add links from related pages or from `wiki/index.md`.

### 3. Missing Pages
Find `[[wikilinks]]` that point to non-existent pages — concepts referenced but never documented.
- **Fix:** Create the page or remove the link.

### 4. Contradictions
Scan for conflicting claims across pages (e.g. different competitor pricing on two pages, conflicting user behavior stats).
- **Fix:** Reconcile by checking raw sources, note which is authoritative.

### 5. Stale Claims
Flag content that may be outdated:
- Competitor features/pricing older than 3 months
- Research findings older than 12 months without revalidation
- Product features that may have changed
- **Fix:** Mark as potentially stale, suggest `/wiki-research` to update.

### 6. Missing Cross-References
Find pages about related topics that don't link to each other.
- **Fix:** Add `[[wikilinks]]` between related pages.

### 7. Index Drift
Compare `wiki/index.md` entries against actual files in `wiki/`:
- Pages in index but not on disk
- Pages on disk but not in index
- **Fix:** Update index.

### 8. Format Compliance
Check all wiki pages for:
- Valid YAML frontmatter (title, type, created, updated, sources, tags)
- Correct page type (from allowed list)
- Lowercase hyphenated filename
- **Fix:** Correct formatting issues.

### 9. Data Gaps
Identify important questions the wiki can't answer:
- Competitor products mentioned but not fully documented
- User segments referenced but without dedicated persona pages
- Research areas with sparse coverage
- **Fix:** Suggest topics for `/wiki-research`.

## Output Format

```markdown
# Wiki Health Report — YYYY-MM-DD

## Critical
- [issue description and fix]

## Warning
- [issue description and fix]

## Info
- [observation or suggestion]

## Stats
- Total wiki pages: X
- Total raw sources: X
- Orphan pages: X
- Broken links: X
- Potentially stale pages: X
```

## Logging

Append to `wiki/log.md`:
```
## [YYYY-MM-DD] lint | Wiki health check
X issues found (Y critical, Z warning). [Summary of fixes applied.]
```

## Batch Mode (200+ pages)

For large wikis, delegate across 5 specialized subagents:
1. **Structural** — broken links, orphans, missing pages
2. **Content** — contradictions, stale claims
3. **Navigation** — index drift, missing cross-references
4. **Format** — frontmatter, naming, compliance
5. **Completeness** — data gaps, coverage analysis
