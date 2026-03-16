# claude-notify

Give Claude Code the ability to send you push notifications via [ntfy.sh](https://ntfy.sh) so you can walk away from your computer and get pinged when Claude needs you.

## Why?

Some tasks take a while — reviewing a large codebase, running multiple subagents, planning an implementation and gathering questions. Instead of staring at the terminal, walk away and let Claude notify you when it's done or needs your input.

## Setup

### 1. Configure ntfy

Create `~/.claude-notify`:

```
server=https://ntfy.sh
topic=my-topic
# token=optional-bearer-token
```

- `server` — ntfy server URL (default: `https://ntfy.sh`)
- `topic` — ntfy topic name (required)
- `token` — Bearer token for authenticated servers (optional)

### 2. Install the script

```bash
ln -s /path/to/claude-notify/claude-notify ~/.local/bin/claude-notify
```

### 3. Add to your global CLAUDE.md

Add the following to `~/.claude/CLAUDE.md`:

```markdown
## Notifications

You have access to `claude-notify` to send push notifications to the user's phone/desktop.
Use it when:
- You've finished a task the user is likely waiting on (e.g. a multi-agent review, a large refactor, a lengthy analysis)
- You have questions or need input before you can continue
- You've hit a blocker and can't proceed without the user

Do NOT use it for routine intermediate steps. Only notify when the user would want to come back to the terminal.

Usage: `claude-notify -t "Title" "message"`
```

### 4. Allow the tool without prompting

Add to `~/.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(claude-notify *)"
    ]
  }
}
```

This lets Claude run `claude-notify` without asking for permission each time.

### 5. Subscribe to notifications

Install the [ntfy app](https://ntfy.sh) on your phone or desktop and subscribe to your topic.

## Usage

```bash
# Task complete
claude-notify -t "Review Ready" "Finished reviewing all 6 modules — report is in your conversation"

# Need user input
claude-notify -t "Questions Before Starting" "I have 3 questions about the auth module before I begin implementing"

# Hit a blocker
claude-notify -t "Blocked" "CI credentials are expired, can't run the integration tests"

# From stdin
echo "Refactor complete — 12 files changed, ready for your review" | claude-notify
```

## Requirements

- bash
- curl

## Disclaimer

This is a personal project and is not affiliated with, endorsed by, or supported by Anthropic. Claude Code is a product of Anthropic, but this tool is an independent community project.

## License

MIT
