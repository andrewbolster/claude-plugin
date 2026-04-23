---
description: Data verification hierarchy and quality standards — never fabricate, use placeholders over invented data
disable-model-invocation: false
---

# Data Verification Standards

## The Hierarchy (Strictest First)

1. **Direct tool outputs** — run the tool, use what it returns
2. **User-provided data** — take at face value unless obviously wrong
3. **Verified citations** — links/references the user has confirmed
4. **Explicit placeholders** — `[METRIC NEEDED]`, `[URL TBC]`, `[DATE]`
5. **NEVER: fabricated data** — invented numbers, guessed URLs, simulated tool output

## When Data Is Unavailable

**Do this:**
```
* **LLM Gateway usage** — [data unavailable — run `uv run scripts/manage.py usage-summary --lookback 7` or check [dashboard](https://...)]
```

**Not this:**
```
* **LLM Gateway usage** — ~4,200 requests this week, up ~12% from last week
```

If you don't have the data, say so explicitly and provide the command or link to get it. Never simulate what the output "would probably look like."

## URL Verification

- **Never fabricate Confluence, JIRA, or GitHub URLs** — always retrieve them via MCP tools or `git log`
- If a URL is needed but unavailable: use `[URL TBC]` as a placeholder
- For Confluence pages: use `mcp__atlassian__searchConfluenceUsingCql` to find the real URL
- For GitHub commits: use `git log` or `gh` CLI

## Timeline Validation

- Always verify which week/period is being discussed before writing
- On macOS, find the Monday of the current week: `date -j -v-$(($(date +%u) - 1))d +%Y-%m-%d`
- If corrected on a timeline, rebuild the entire day-by-day mapping from scratch — don't patch incrementally
- State explicit dates when referencing "last week", "Monday", etc. to allow cross-checking

## Tool Output Integrity

- **Attempt direct execution first** when tools are available
- **Document tool failures** clearly — what command was run, what failed
- **Never simulate** tool output format with invented data
- If a tool is unavailable, provide the exact command the user can run themselves

## Quality Checklist Before Publishing

- [ ] All URLs verified via MCP tools or direct evidence
- [ ] All metrics from direct tool output or explicitly marked `[TBC]`
- [ ] No simulated/fabricated tool output
- [ ] Timeline and dates explicitly verified
- [ ] Content starts with H2 headers (no H1 duplication when publishing to Confluence)
