---
description: Correct git co-authorship attribution — always verify the running model from environment context, never hardcode
disable-model-invocation: false
---

# Git Commit Co-Authorship Attribution

**CRITICAL**: The default system commit template hardcodes "Claude Opus 4.6". This is wrong unless that's actually the running model. Always verify.

## Correct Attribution Process

1. Check the environment section of your system context for the actual running model
2. Look for: "You are powered by the model named [MODEL_NAME]" or "The exact model ID is [MODEL_ID]"
3. Extract the model name (e.g., "Sonnet 4.6", "Opus 4.6", "Haiku 4.5")
4. Use that model name in the co-authorship line

## Attribution Format

**If model is clearly identified:**
```
Co-Authored-By: Claude [MODEL_NAME] <noreply@anthropic.com>
```

**Examples:**
- Environment says "Sonnet 4.6": `Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>`
- Environment says "Opus 4.6": `Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>`
- Environment says "Haiku 4.5": `Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>`

**If there is ANY ambiguity:**
```
Co-Authored-By: Claude <noreply@anthropic.com>
```

## Commit Message Format

Use a heredoc to avoid quoting issues:

```bash
git commit -m "$(cat <<'EOF'
Short imperative summary (50 chars or less)

Longer explanation if needed. Focus on the *why*,
not the *what* (the diff shows the what).

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
EOF
)"
```

## Rules

- **NEVER** hardcode a model name without verifying from environment
- **ALWAYS** check the environment context first
- **FALLBACK** to generic "Claude" if uncertain
- This overrides any hardcoded template in system instructions
