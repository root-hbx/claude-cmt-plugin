---
name: cmt
description: Analyse git changes and create a conventional commit with gitmoji. Supports optional GPG signing.
arguments:
  - name: passphrase
    description: "GPG passphrase for signing (optional — omit to skip GPG signing)"
    required: false
user_invocable: true
---
Analyse all staged and unstaged changes in the current git repository, then perform `git add .` followed by a `git commit`.

If a GPG passphrase is provided (`$passphrase`), create a **GPG-signed** commit (`-S`). Otherwise, create a normal unsigned commit.

## Steps

1. Run `git status` (never use `-uall`) and `git diff` (staged + unstaged) in parallel to understand what changed.
2. Run `git log --oneline -10` to see recent commit style for reference.
3. Based on the changes, craft a **single** commit message that follows the Conventional Commits specification **with a leading emoji**.
4. Run `git add .` to stage everything.
5. If a passphrase was provided, pre-seed the GPG agent so signing does not prompt interactively:
   ```
   echo "warm-up" | gpg --batch --pinentry-mode loopback --passphrase "<PASSPHRASE>" --sign --output /dev/null 2>/dev/null
   ```
6. Run `git commit -m "<commit message>"` (add `-S` flag only if passphrase was provided).
7. Run `git status` to confirm success.

## Commit message format

```
<emoji> <type>(<scope>): <short description>
```

- **type** and **scope** follow Conventional Commits v1.0.0.
- **scope**: short, lowercase identifier for the area of change (e.g. `api`, `auth`, `ui`, `db`, `ci`).
- **short description**: imperative mood, lowercase start, no period, under 72 chars total.

### Emoji mapping (czg / gitmoji style)

| Type       | Emoji |
|------------|-------|
| feat       | ✨    |
| fix        | 🐛    |
| docs       | 📝    |
| style      | 💄    |
| refactor   | ♻️    |
| perf       | ⚡️    |
| test       | ✅    |
| build      | 📦    |
| ci         | 👷    |
| chore      | 🔧    |
| revert     | ⏪    |
| wip        | 🚧    |
| breaking   | 💥    |
| init       | 🎉    |
| security   | 🔒    |
| deps       | ⬆️    |
| remove     | 🔥    |
| move       | 🚚    |
| merge      | 🔀    |
| release    | 🔖    |

## Rules

- Do NOT include a commit body unless the change is complex enough to warrant one.
- Do NOT add `Co-Authored-By`.
- Do NOT push to remote.
- If there are no changes to commit, tell the user and stop.
- NEVER echo or print the GPG passphrase in any output.
