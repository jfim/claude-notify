# claude-notify

A bash script that lets Claude Code send push notifications to the user via ntfy.sh when long-running tasks complete.

## Structure

- `claude-notify` — the main script (bash + curl)
- `~/.claude-notify` — user config file (server, topic, token)

## Config format

Simple `key=value` file. Lines starting with `#` are comments.
Supported keys: `server`, `topic`, `token`.
