# mos-hormozi-skills — Public Shared Repo

This repo is shared with The Vibe Marketing Lab community members. It is PUBLIC.

Offer-building skills: the interactive $100M chain, avatar first. This pack sits alongside the MarketingOS engine (`pipx install marketing-os`) and the other `mos-*-skills` packs.

---

## Security Rules (CRITICAL)

Every commit is visible to community members.

- **NEVER commit API keys, tokens, secrets, passwords, or credentials** — not in code, not in comments, not in examples
- **NEVER commit hardcoded file paths** containing usernames or machine-specific paths (e.g. `/mnt/c/Users/<name>/...`, `/Users/<name>/...`)
- **NEVER reference `.env` files with real values** — only env var NAMES as setup instructions (e.g. "set `GOOGLE_API_KEY` in your environment")
- **NEVER commit personal data** — emails, member lists, client info, business details
- **NEVER reference private repos** by path or content

**Before every commit, verify:**
1. `grep -r "API_KEY\|TOKEN\|SECRET\|PASSWORD\|sk-\|AIza" --include="*.md"` returns only env var name references, never values
2. `grep -r "/mnt/c/Users\|/Users/" --include="*.md"` returns zero results
3. No `.env`, `.env.*`, or credential files are staged

---

## What This Repo Contains

**The $100M chain, in order:**
1. `mos-100m-avatar` — 10-section customer avatar workbook (Step 1; the offer skill refuses to start without it)
2. `mos-100m-offer` — Grand Slam Offer, 12 stops
3. `mos-100m-leads` — lead magnet + one channel, 10 stops
4. `mos-100m-money-models` — offer sequencing for 30-day payback, 6 stops
5. `mos-100m-onepager` — GTM one-pager capstone

The avatar writes `outputs/mos-100m-avatar-workbook.md`; the other four read and write `outputs/mos-100m-*-{{slug}}.md`, sharing one slug so each step finds the previous one's output. The older `mos-offer` and `mos-money-models` workbook skills were retired from this pack on 2026-09-05.

Each skill is a flat top-level folder with a `SKILL.md` (the skill prompt) and, where needed, `references/` (frameworks) or `scripts/` (deterministic tools). `setup.sh` links every top-level skill folder into `~/.claude/skills/`.

## Editing Rules

- Skills must work on any machine — relative paths and env var references only
- Skills sit at the top level of this repo; a nested skill folder is invisible to Claude Code
- Keep README.md current when adding or renaming a skill, then re-run `setup.sh`
- Test every skill without any private infrastructure before pushing

> **Third-party framework rule.** These skills apply frameworks from published books by Alex Hormozi. They are independent implementations, not affiliated with or endorsed by the author, and every SKILL.md carries that attribution. Do NOT add verbatim extracts, scanned material, or redistributable "cheat sheets" derived from the source texts. The `references/` files must stay operational summaries written for the build process.
