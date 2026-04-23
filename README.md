# bolster plugin

Personal best practices, development environment standards, voice/style guidelines, and tooling patterns for Andrew Bolster's Claude Code sessions.

These skills are non-work-specific and safe to use in any context.

## Skills

### `uv-run`

Python script execution standards. Enforces `uv run` over bare `python`/`python3` everywhere — Bash tool calls, Makefiles, command files. Includes the UV script frontmatter template and a Click CLI scaffold.

```
/bolster:uv-run
```

### `markitdown`

Convert files (PDF, DOCX, PPTX, XLSX, email) to markdown using `markitdown` via `uvx`. Covers supported formats, when to use it, and output conventions.

```
/bolster:markitdown
```

### `lsof-patterns`

Find and kill processes by port. One-liner patterns for graceful and force-kill, multiple ports, and safe port-reuse in dev workflows.

```
/bolster:lsof-patterns
```

### `git-attribution`

Correct Claude co-authorship attribution in git commits. Check the running model name from environment context, never hardcode it. Covers heredoc commit message format and fallback to generic "Claude" when uncertain.

```
/bolster:git-attribution
```

### `dev-environment`

Full development toolchain reference: yadm, zsh/Oh My Zsh/Starship, Neovim/LazyVim, tmux/byobu, mamba/miniforge3, bun, uv, bob. Key aliases, PATH order on macOS, and anti-patterns (never search the whole home directory).

```
/bolster:dev-environment
```

### `voice-style`

Andrew Bolster's authentic writing voice — dry humor, technical precision, honest self-reflection, no corporate speak. Covers formatting principles for weeknotes and blog posts, content priority order, and failure writing guidelines.

```
/bolster:voice-style
```

### `data-verification`

Data quality hierarchy and verification standards before publishing any content. Tool outputs > user-provided > verified citations > placeholders > never fabricate. URL and timeline verification patterns, quality checklist.

```
/bolster:data-verification
```

## Validation

```bash
cd plugins/bolster
claude plugin validate .
```
