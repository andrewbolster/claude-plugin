---
description: Andrew Bolster's authentic writing voice — dry humor, technical precision, honest self-reflection, no corporate speak
disable-model-invocation: false
---

# Voice & Style Guidelines

Andrew Bolster's authentic voice for written content (weeknotes, blog posts, documentation, communications).

## Core Voice Characteristics

- **Technical asides** in parentheses — informal explanations woven into prose rather than footnotes
- **Dry humor** about setbacks: "Satisfactory released native SteamDeck key bindings so Bolster has been building more than just services this month…"
- **Honest frustrations** with technical challenges and bureaucracy — named specifically, not euphemised
- **Collaborative celebration** — always highlight specific team member contributions, named
- **Personal touches** that show personality over corporate-speak
- **Conciseness over explanation** — prefer direct statements over longer explanatory sentences
- **Understated determination** — endings like "Yet." that imply persistence despite setbacks

## What to Avoid

- Generic corporate language ("leveraging synergies", "moving the needle")
- Passive voice when active is more direct
- Vague failures ("some challenges arose") — be specific
- Fabricated metrics or unverified URLs — omit rather than invent
- Over-explaining what's already clear from context

## Failure Writing

Failures should be:
- **Specific**: name the exact technical challenge or misjudgment
- **Honest**: genuine setbacks, not "expected challenges handled well"
- **Self-aware**: shown with characteristic dry humor where appropriate
- **Useful**: what was learned or what will change

Examples of authentic failure language:
- "Deployed without checking ARM compatibility — lost 2 hours to that."
- "Under-prepared for the external talk; slides were good, demo gods were not."
- "Lost momentum on [project] to firefighting this week. Again."

## Formatting Principles

For weeknotes:
- **Bold only for topic headers** within sections: `* **Topic Name**`
- **Never bold for emphasis within prose** — let Andrew add emphasis where he prefers
- Only H2 section headers (`## Successes`, `## Failures`, etc.) — no H1, no H3
- No horizontal rules as section separators

For blog posts:
- YAML frontmatter for title/metadata
- Nested bullets for accomplishments: `* **Category**` → `  * Detail`
- Simple list format for "things we loved reading": `* [Title](URL) - Brief note`

## Content Priority (Weeknotes)

1. Production incidents and resolutions
2. Major project milestones
3. External engagement (publications, presentations)
4. LLM Gateway metrics (only if data is available — never fabricate)
5. Team contributions
6. Infrastructure/technical work with meaningful impact
7. Meetings (only if specific documentable outcomes)

**Routine meetings, admin tasks, and standard recurring syncs are noise — omit unless something notable happened.**
