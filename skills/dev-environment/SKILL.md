---
description: Andrew Bolster's development environment — toolchain, aliases, shell setup, and key patterns
disable-model-invocation: false
---

# Development Environment Reference

## Core Toolchain

| Tool | Role | Notes |
|------|------|-------|
| **yadm** | Dotfiles manager | `yadm status`, `yadm add`, `yadm push` |
| **zsh + Oh My Zsh** | Shell | Starship prompt; aliases in `~/.config/zsh/aliases.zsh` |
| **Neovim (LazyVim)** | Editor | `nv` or `vim` alias; LazyVim config |
| **tmux / byobu** | Terminal multiplexer | Ctrl-A prefix; `byo`, `byos`, `byoa` aliases |
| **mamba/miniforge3** | Python env manager | macOS: `~/miniforge3`; Linux: `~/miniconda3` |
| **bun** | Node.js package manager | `~/.bun/bin` in PATH |
| **uv** | Python tool/script runner | Always use `uv run` — see uv-run skill |
| **bob** | Neovim version manager | `~/.local/share/bob/nvim-bin` in PATH |

## Shell Aliases (Key Ones)

```zsh
# Git
gs='git status'    ga='git add'     gc='git commit'
gp='git push'      gl='git log --oneline --graph'

# Yadm (dotfiles)
ys='yadm status'   ya='yadm add'    yc='yadm commit'   yp='yadm push'

# Dev
nv='nvim'          vim='nvim'       py='python3'

# Claude
claude='claude-titled --dangerously-skip-permissions'

# Byobu
byo='byobu'        byos='byobu new-session'   byoa='byobu attach'

# Safety (confirm before destructive ops)
rm='rm -i'         cp='cp -i'       mv='mv -i'
```

## PATH Order (macOS)

```
$HOME/bin
$HOME/.local/bin
$HOME/.cargo/bin
/usr/local/bin
$HOME/.claude/local        # Claude Code local bin
$HOME/.local/share/bob/nvim-bin
$HOME/.bun/bin
/opt/homebrew/opt/ruby/bin
```

## File Search Anti-Patterns

When searching with filesystem tools, **never search the entire home directory** — it can trigger security systems. Restrict searches to:
- `~/scratch` and subdirectories
- Specific project directories (e.g., `~/src/<project>`)
- Known config locations (e.g., `~/.claude/`)

## Google Cloud SDK

Loaded from `~/google-cloud-sdk/` if present. Completion available for zsh.

## macOS-Specific

- Homebrew completions at `/opt/homebrew/share/zsh/site-functions`
- Ruby from `/opt/homebrew/opt/ruby/bin` if installed
- Docker completions at `~/.docker/completions`
