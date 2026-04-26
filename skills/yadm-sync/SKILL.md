---
description: Synchronise yadm dotfiles — stage local changes, pull remote, resolve conflicts safely, and push
disable-model-invocation: false
---

# yadm Sync Workflow

yadm is a git-based dotfiles manager. Its tracked files live in `~/.local/share/yadm/repo.git` and check out directly into `$HOME`. Many files have class-based alternates (e.g. `settings.json##class.BlackDuck`, `settings.json##default`) — yadm selects the active alternate based on the configured class.

## Standard Sync Protocol

Run these checks first to understand state before touching anything:

```bash
yadm status
yadm fetch
yadm log origin/main..main --oneline   # local commits not on remote
yadm log main..origin/main --oneline   # remote commits not local
```

Then follow whichever branch applies:

### Branch A — Local changes only (remote is not ahead)

```bash
yadm add <specific files>   # never yadm add -A — avoid sweeping in unrelated files
GIT_AUTHOR_EMAIL="bolster@blackduck.com" GIT_AUTHOR_NAME="Andrew Bolster" \
GIT_COMMITTER_EMAIL="bolster@blackduck.com" GIT_COMMITTER_NAME="Andrew Bolster" \
yadm commit -m "$(cat <<'EOF'
Short imperative summary

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
EOF
)"
yadm push
```

### Branch B — Remote is ahead, local is clean

```bash
yadm pull --rebase
yadm push   # if local has unpushed commits
```

### Branch C — Remote is ahead AND local has changes (most common)

1. Stash or commit local changes first:
   ```bash
   yadm stash   # or commit with GIT_AUTHOR_* vars as above
   ```
2. Pull remote:
   ```bash
   yadm pull --rebase
   ```
3. Pop stash / cherry-pick if needed, then push.

## Identity Issues

`git config --global` may fail silently when `~/.gitconfig` is itself tracked by yadm and the working tree is locked. Use environment variables instead:

```bash
export GIT_AUTHOR_EMAIL="bolster@blackduck.com"
export GIT_AUTHOR_NAME="Andrew Bolster"
export GIT_COMMITTER_EMAIL="bolster@blackduck.com"
export GIT_COMMITTER_NAME="Andrew Bolster"
```

Set these before `yadm commit` or `yadm rebase --continue`.

## Rebase Conflict Rules

### Modify/delete conflicts (remote deleted a file we modified)

Occurs when remote refactored to class-based alternates and deleted the unclassed file, but our commit modified the old path.

Resolution:
```bash
yadm rm <conflicted-file>
yadm rebase --continue   # with GIT_AUTHOR_* vars exported
```

If `--continue` fails with identity errors after retries, use `yadm rebase --skip` as last resort — but **note that --skip discards the commit**. Recover content via reflog:
```bash
yadm reflog | head -20
yadm show <sha>:.claude/shared/data-science-reports.md > ~/.claude/shared/data-science-reports.md
```

### Merge conflicts in tracked files

Use standard git conflict markers. Edit the file to resolve, then:
```bash
yadm add <resolved-file>
yadm rebase --continue
```

## Class-Based Alternate Files

yadm selects alternates based on `yadm config local.class`. Common classes:
- `BlackDuck` → `##class.BlackDuck` suffix files are used
- `default` → `##default` suffix files are used

When remote introduces class-based alternates for a file that previously existed unclassed, the unclassed path is deleted on remote. This triggers a modify/delete conflict if you had local changes to the old path. Resolve by removing the old path (`yadm rm`) and re-applying changes to the new class-specific file.

## After a Successful Sync

Verify tracked alternates are correctly linked:
```bash
yadm alt   # regenerates symlinks/copies for active class
yadm status   # should be clean
```

## What NOT to Do

- **Never `yadm add -A`** — picks up scratch files, caches, secrets
- **Never `yadm rebase --skip` without checking reflog** — the skipped commit's content is recoverable but only if you act before GC
- **Never force-push** unless you know exactly what remote state you're overwriting
- **Never edit class-alternate files without knowing which class is active** — changes to `##class.BlackDuck` files only take effect on machines with `local.class = BlackDuck`
