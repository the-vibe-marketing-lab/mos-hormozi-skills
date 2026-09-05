# mos-hormozi-skills

The $100M chain for Claude Code: five skills that walk you from "who is this for" to a Grand Slam Offer, a lead plan, a money model, and a one-page go-to-market summary, one decision at a time.

Built by [The Vibe Marketing Lab](https://www.skool.com/the-vibe-marketing-lab) for the MarketingOS engine (`pipx install marketing-os`).

> These skills apply the frameworks from Alex Hormozi's *$100M Offers*, *$100M Leads* and *$100M Money Models*. They are independent implementations, not affiliated with or endorsed by the author. Read the books for the full argument; these skills are the build process, not a substitute for the source.

## What's in here

Run them in order. Each one reads the previous one's output from `outputs/`.

| # | Skill | What it does | Stops |
|---|-------|--------------|-------|
| 1 | `/mos-100m-avatar` | 10-section customer avatar from your business files. The rest of the chain reads this | — |
| 2 | `/mos-100m-offer` | Grand Slam Offer: market, pricing, value equation, bonuses, guarantee, naming | 12 |
| 3 | `/mos-100m-leads` | Lead magnet plus ONE advertising channel, with real activity maths | 10 |
| 4 | `/mos-100m-money-models` | Sequences attraction, upsell, downsell and continuity offers for 30-day payback | 6 |
| 5 | `/mos-100m-onepager` | Distils all of it into a one-page GTM summary (markdown, Word, HTML) | — |

The avatar is the only step that generates a document for you. The other four stop at every decision and make you choose. Slower, and much harder to end up with a plan you don't believe.

If you start at step 2 without an avatar, `/mos-100m-offer` will tell you and send you back to step 1. It never builds the avatar inline.

## Prerequisites

1. **Claude Code** with a Claude Pro or Max subscription (the parallel agents need the context).
2. **Business reference files** in the project you run the skills from. The skills read `reference/core/`:

   | File | What goes in it |
   |------|----------------|
   | `soul.md` | Your story: why you started, what drives you |
   | `offer.md` | What you sell: pricing, delivery model, who it's for |
   | `audience.md` | Who you serve: demographics, where they hang out, what they struggle with |
   | `voice.md` | How your brand speaks |

   Optional but powerful: `reference/proof/testimonials.md`. Real customer quotes make every output sharper.

   **Scaffolded with `mos onboard`?** The engine writes under `business/`; these skills currently read `reference/core/`. Copy or symlink across until the skills are aligned to the engine layout:

   | `mos onboard` writes | These skills read |
   |------|------|
   | `business/brand/brand.md`, `business/brand/voice.md` | `reference/core/soul.md`, `reference/core/voice.md` |
   | `business/audience/primary.md`, `business/offers/<slug>/offer.md` | `reference/core/audience.md`, `reference/core/offer.md` |
   | `business/proof/testimonials.md` | `reference/proof/testimonials.md` |

## Install

Skills live in `~/.claude/skills/`. This repo keeps them under version control and links them into place, so a `git pull` is all an update takes.

```bash
git clone https://github.com/the-vibe-marketing-lab/mos-hormozi-skills.git ~/Desktop/mos-hormozi-skills
cd ~/Desktop/mos-hormozi-skills
bash setup.sh
```

`setup.sh` links every skill folder in this repo into `~/.claude/skills/` (a symlink on macOS and Linux, a directory junction on Windows via Git Bash). Restart any open Claude Code session, then type `/mos-100m-avatar` to confirm it loads.

**Updating:** `cd ~/Desktop/mos-hormozi-skills && git pull`. The links point at the clone, so that's it. Updates are announced in the Skool community.

**Other packs:** this is one of the `mos-*-skills` packs that accompany the [MarketingOS engine](https://github.com/the-vibe-marketing-lab/marketing-os). The full list is in the [marketing-os-skills](https://github.com/the-vibe-marketing-lab/marketing-os-skills) README.

## How to use

Run these inside your MarketingOS repo with your business files in place.

### 1. `/mos-100m-avatar`

Reads your business files and builds a 10-section avatar: dream client, demographics, before state, dream outcome, top pains, top goals, buying questions, what they've tried, objections, stage of awareness. Generates an avatar image if `GOOGLE_API_KEY` is set (optional).

**Output:** `outputs/mos-100m-avatar-workbook.md`

### 2. `/mos-100m-offer`

Loads the avatar for the Chapter 2 market check, then walks the twelve chapters of *$100M Offers* one stop at a time: commit a price, build the value equation, divergent thinking, the five-step build, scarcity, urgency, bonuses, guarantee, and naming last.

**Output:** `outputs/mos-100m-offer-workbook-[slug].md`

### 3. `/mos-100m-leads`

Reads the offer and builds a lead magnet plus one advertising channel, with the activity maths that says how many of what per day.

**Output:** `outputs/mos-100m-leads-plan-[slug].md`

### 4. `/mos-100m-money-models`

Reads the offer and the leads plan and sequences the attraction, upsell, downsell and continuity offers so one customer pays for the next two inside 30 days.

**Output:** `outputs/mos-100m-money-model-[slug].md`

### 5. `/mos-100m-onepager`

Reads all of the above and writes the one-page GTM summary.

**Output:** `outputs/mos-100m-gtm-onepager-[slug].md`

All five share one `{{slug}}`, so each step finds the previous one's file:

```
outputs/
├── mos-100m-avatar-workbook.md
├── mos-100m-offer-workbook-[slug].md
├── mos-100m-leads-plan-[slug].md
├── mos-100m-money-model-[slug].md
└── mos-100m-gtm-onepager-[slug].md
```

## Tips

- **Better inputs, better outputs.** Real testimonials change everything; the AI uses your customers' language instead of guessing.
- **Don't skip the avatar.** The offer skill checks for it and stops if it's missing. That's the point: an offer with no customer language in it is a guess.
- **Re-run any step.** New testimonials, new pricing: run it again and the file is rewritten. Later steps pick up the change next time they run.
- **Read the workbooks in Obsidian.** They're markdown with cross-references.

## Troubleshooting

- **Skills don't show up:** the folders must be direct children of `~/.claude/skills/`. `ls ~/.claude/skills/ | grep mos-100m` should list all five. Restart Claude Code.
- **"I can't find an avatar workbook":** run `/mos-100m-avatar` first and check `outputs/`. Older runs saved it as `mos-avatar-workbook.md`; the offer skill still finds that name.
- **Avatar reads generic:** add real quotes to `reference/proof/testimonials.md`.
- **No avatar image:** `GOOGLE_API_KEY` isn't set. Optional; the skill works without it.
