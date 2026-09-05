# mos-hormozi-skills

Offer-building skills for Claude Code. Two ways to get from "I have a business" to "I have an offer, a lead plan and a money model I believe in": a fast workbook chain, and a slow interactive chain that stops at every decision.

Built by [The Vibe Marketing Lab](https://www.skool.com/the-vibe-marketing-lab) for the MarketingOS engine (`pipx install marketing-os`).

> These skills apply the frameworks from Alex Hormozi's *$100M Offers*, *$100M Leads* and *$100M Money Models*. They are independent implementations, not affiliated with or endorsed by the author. Read the books for the full argument; these skills are the build process, not a substitute for the source.

## What's in here

**The workbook chain — build your offer from your business files:**

| # | Skill | What it does | Time |
|---|-------|--------------|------|
| 1 | `/mos-avatar` | 10-section customer avatar from your business files | ~3-5 min |
| 2 | `/mos-offer` | Structured offer with value stack, pricing, guarantees and packaging | ~5-8 min |
| 3 | `/mos-money-models` | Full offer sequence (attraction, upsell, downsell, continuity) with 30-day payback maths | ~5-8 min |

**The $100M chain — the same jobs, one decision at a time:**

| # | Skill | What it does | Stops |
|---|-------|--------------|-------|
| 2a | `/mos-100m-offer` | Grand Slam Offer: market, pricing, value equation, bonuses, guarantee, naming | 12 |
| 2b | `/mos-100m-leads` | Lead magnet plus ONE advertising channel, with real activity maths | 10 |
| 2c | `/mos-100m-money-models` | Sequences attraction, upsell, downsell and continuity offers for 30-day payback | 6 |
| 2d | `/mos-100m-onepager` | Distils all three into a one-page GTM summary (markdown, Word, HTML) | — |

Run `/mos-avatar` first either way. Then pick one chain: the workbook chain generates documents for you to review; the $100M chain makes you choose at every step. Slower, and much harder to end up with a plan you don't believe. Running both gives you two competing offers.

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
git clone https://github.com/reapzyau/mos-hormozi-skills.git ~/Desktop/mos-hormozi-skills
cd ~/Desktop/mos-hormozi-skills
bash setup.sh
```

`setup.sh` links every skill folder in this repo into `~/.claude/skills/` (a symlink on macOS and Linux, a directory junction on Windows via Git Bash). Restart any open Claude Code session, then type `/mos-avatar` to confirm it loads.

**Updating:** `cd ~/Desktop/mos-hormozi-skills && git pull`. The links point at the clone, so that's it. Updates are announced in the Skool community.

**Other packs:** this is one of the `mos-*-skills` packs that accompany the [MarketingOS engine](https://github.com/reapzyau/marketing-os). The full list is in the [marketing-os-skills](https://github.com/reapzyau/marketing-os-skills) README.

## How to use

Run these inside your MarketingOS repo with your business files in place.

### 1. `/mos-avatar`

Reads your business files and builds a 10-section avatar: dream client, demographics, before state, dream outcome, top pains, top goals, buying questions, what they've tried, objections, stage of awareness. Generates an avatar image if `GOOGLE_API_KEY` is set (optional).

**Output:** `outputs/mos-avatar-workbook.md`

### 2. `/mos-offer`

Reads the avatar and builds the offer: problem universe, solution matrix, value stack, enhancement levers (scarcity, urgency, bonuses, guarantee), packaging, pricing with value-to-price ratio, the CUB test (Confusing? Unbelievable? Boring?), and competitor research.

**Output:** `outputs/mos-offer-workbook-[name].md`

### 3. `/mos-money-models`

Reads the offer and designs the sequence: attraction offer, core, upsell, continuity, downsell, 30-day payback maths, LTV at 1/3/6/12 months, and the customer journey map.

**Output:** `outputs/mos-money-model-[name].md`

### The $100M chain

Run `/mos-100m-offer`, `/mos-100m-leads`, `/mos-100m-money-models`, then `/mos-100m-onepager`, in order. Each reads the previous one's output from `outputs/` and they all share one `{{slug}}`:

```
outputs/
├── mos-avatar-workbook.md
├── mos-100m-offer-workbook-[slug].md
├── mos-100m-leads-plan-[slug].md
├── mos-100m-money-model-[slug].md
└── mos-100m-gtm-onepager-[slug].md
```

## Tips

- **Better inputs, better outputs.** Real testimonials change everything; the AI uses your customers' language instead of guessing.
- **Run them in order.** Skipping the avatar means the offer has no customer language to draw from.
- **Re-run any skill.** New testimonials, new pricing: run it again and the workbook is rewritten.
- **Read the workbooks in Obsidian.** They're markdown with cross-references.

## Troubleshooting

- **Skills don't show up:** the folders must be direct children of `~/.claude/skills/`. `ls ~/.claude/skills/ | grep mos-` should list them. Restart Claude Code.
- **Avatar reads generic:** add real quotes to `reference/proof/testimonials.md`.
- **"Avatar workbook not found":** run `/mos-avatar` first and check `outputs/`.
- **Offer validation flags issues:** that's the point. The validation agent stress-tests the offer; review the flags and decide.
- **No avatar image:** `GOOGLE_API_KEY` isn't set. Optional; the skill works without it.
