# Repository Guidelines

## Project Structure & Module Organization
This repository stores network rule lists for two clients:
- `QuantumultX/RuleSet/`: QuantumultX-formatted `.list` files
- `Surge/RuleSet/`: Surge-formatted `.list` files

Each rule topic should be maintained as a mirrored pair (same filename) in both directories, for example:
- `QuantumultX/RuleSet/Claude.list`
- `Surge/RuleSet/Claude.list`

Keep files focused by provider/app/topic (for example `Google.list`, `SummonersWar.list`).

## Build, Test, and Development Commands
There is no build pipeline in this repo; changes are plain-text edits.

- `git status`
Checks current changes before/after editing.
- `rg --files QuantumultX/RuleSet Surge/RuleSet`
Lists tracked rule files quickly.
- `comm -3 <(ls QuantumultX/RuleSet | sort) <(ls Surge/RuleSet | sort)`
Verifies filename parity between both clients.
- `grep -Ev '^\s*(#|$)' Surge/RuleSet/Claude.list | wc -l`
Counts active rules (useful for `# 规则统计` verification).

## Coding Style & Naming Conventions
- Use UTF-8 text, LF line endings, and one rule per line.
- Keep exactly one blank line between header and rules.
- Avoid trailing spaces (especially after commas).
- Use `PascalCase.list` filenames (example: `YunyiSecLocal.list`).
- Keep header format:
`# 规则名称: <Name>`
`# 规则统计: <N>`

Rule keyword mapping must stay client-correct:
- QuantumultX: `HOST`, `HOST-SUFFIX`, `HOST-KEYWORD`
- Surge: `DOMAIN`, `DOMAIN-SUFFIX`, `DOMAIN-KEYWORD`

For `IP-CIDR` in Surge, include `no-resolve` when applicable.

## Testing Guidelines
No automated test framework is configured. Validate changes manually:
- Confirm rule count in `# 规则统计` matches non-comment/non-empty lines.
- Confirm both client files exist for each topic and stay semantically aligned.
- Spot-check syntax compatibility per client before opening a PR.

## Commit & Pull Request Guidelines
Git history follows Conventional Commit style (for example `feat: add Google rules for Surge and QuantumultX`).

- Prefer `feat:` for new rules, `fix:` for corrections, `chore:` for non-rule maintenance.
- Keep each commit scoped to one logical rule update.
- PRs should include: what changed, why it changed, affected `.list` files, and any compatibility notes.
- Link related issues/tasks when available.
