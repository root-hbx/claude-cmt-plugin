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
    "https://github.com/root-hbx/claude-cmt-plugin"
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

## Related Work

Compared with the built-in `/commit` command in Claude Code:

| Feature | `/commit` (built-in) | `/cmt` (this plugin) |
|---------|---------------------|----------------------|
| Gitmoji prefix | ❌ Not supported | ✅ 20+ types auto-mapped |
| Conventional Commits | ❌ Free-form, no enforced spec | ✅ Strict v1.0.0 compliance |
| Scope annotation | ❌ Not required | ✅ Always annotates change scope |
| GPG signing | ❌ Not supported | ✅ Optional, pass passphrase to enable |
| GPG agent warm-up | ❌ N/A | ✅ Auto warm-up, no interactive prompt |
| Co-Authored-By tag | ⚠️ Always added | ❌ Not added, cleaner commit history |
| Commit format consistency | ⚠️ Model-dependent, style may drift | ✅ Fixed template `<emoji> <type>(<scope>): <desc>` |

## License

MIT
