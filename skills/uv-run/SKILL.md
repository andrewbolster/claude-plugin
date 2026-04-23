---
description: Python script execution standards using uv — always use `uv run`, never bare python/python3
disable-model-invocation: false
---

# Python Script Execution with uv

**CRITICAL**: Always use `uv run` to execute Python scripts. Never use bare `python` or `python3`.

## Execution Rules

| Scenario | Command |
|----------|---------|
| Script with UV frontmatter (`# /// script` block) | `uv run <script.py>` |
| Script without frontmatter, with known deps | `uv run --with <dep1>,<dep2> <script.py>` |
| Inline/ad-hoc execution | `uvx <tool>` for tools, `uv run --with <dep> -c "..."` for snippets |

**Why**: Scripts may declare inline dependencies via `# /// script` blocks. Bypassing `uv run` misses these dependency declarations and breaks the script.

## New Script Template

When writing any new standalone Python script, use UV script format:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.11"
# dependencies = ["click", "requests"]
# ///
```

Adjust `requires-python` and `dependencies` as needed. Common deps: `click`, `requests`, `rich`, `httpx`, `pydantic`.

## Click CLI Pattern

For CLI tools, use Click:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.11"
# dependencies = ["click", "rich"]
# ///

import click
from rich.console import Console

console = Console()

@click.command()
@click.argument("target")
@click.option("--verbose", "-v", is_flag=True)
def main(target, verbose):
    """Brief description of what this does."""
    console.print(f"Processing {target}")

if __name__ == "__main__":
    main()
```

## Enforced Everywhere

This rule applies in ALL contexts:
- Shell commands typed manually
- Bash tool calls in Claude Code
- Command files and scripts
- Makefile targets that invoke Python
- Any other context where a Python script is invoked

**No exceptions.** If you find yourself writing `python script.py` or `python3 script.py`, stop and rewrite as `uv run script.py`.
