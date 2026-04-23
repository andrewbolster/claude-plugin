---
description: Kill processes holding a port using lsof — safe, targeted process management patterns
disable-model-invocation: false
---

# Port Process Management with lsof

## Kill Process on a Specific Port

```bash
lsof -ti:<PORT> -sTCP:LISTEN | xargs kill
```

Example — kill whatever is holding port 3001:
```bash
lsof -ti:3001 -sTCP:LISTEN | xargs kill
```

**Breakdown**:
- `-t` — output PIDs only (no headers)
- `-i:<PORT>` — filter by port number
- `-sTCP:LISTEN` — only processes in LISTEN state (avoids killing established connections)
- `| xargs kill` — send SIGTERM to each PID

## Graceful vs Force Kill

```bash
# Graceful (SIGTERM) — try this first
lsof -ti:3001 -sTCP:LISTEN | xargs kill

# Force (SIGKILL) — if process doesn't respond
lsof -ti:3001 -sTCP:LISTEN | xargs kill -9
```

## Find What's on a Port (Without Killing)

```bash
lsof -i:<PORT> -sTCP:LISTEN
```

## Multiple Ports

```bash
lsof -ti:3001,3002,8080 -sTCP:LISTEN | xargs kill
```

## Safe Usage Notes

- Always check with `lsof -i:<PORT>` first if unsure what's running
- Prefer SIGTERM before SIGKILL — give processes a chance to clean up
- This pattern works on macOS and Linux (BSD `lsof` included on macOS)
- On Linux, `fuser -k <PORT>/tcp` is an alternative but `lsof` is more portable
