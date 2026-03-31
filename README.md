# claude-cmt-plugin

A [Claude Code](https://claude.com/claude-code) plugin that analyses your git changes and creates conventional commits with gitmoji — with optional GPG signing.

## Features

- Auto-analyses staged and unstaged changes via `git status` + `git diff`
- Generates [Conventional Commits](https://www.conventionalcommits.org/) messages with [gitmoji](https://gitmoji.dev/)
- Optional GPG signing (pass your passphrase, or omit for unsigned commits)
- References recent commit history to match your project's style

## Install

Add to your project `.claude/settings.json` or global `~/.claude/settings.json`:

```json
{
  "plugins": [
    "https://github.com/yourname/claude-cmt-plugin"
  ]
}
```

## Usage

```
# Unsigned commit
/cmt

# GPG-signed commit
/cmt <your-gpg-passphrase>
```

## Commit format

```
<emoji> <type>(<scope>): <short description>
```

### Emoji mapping

| Type | Emoji | Type | Emoji |
|------|-------|------|-------|
| feat | ✨ | chore | 🔧 |
| fix | 🐛 | revert | ⏪ |
| docs | 📝 | wip | 🚧 |
| style | 💄 | breaking | 💥 |
| refactor | ♻️ | security | 🔒 |
| perf | ⚡️ | deps | ⬆️ |
| test | ✅ | remove | 🔥 |
| build | 📦 | move | 🚚 |
| ci | 👷 | release | 🔖 |

## License

MIT
