<h1 align="center">Gann Stockmarket Control Skill</h1>

<p align="center"><a href="README.md">中文</a> | English</p>

An AI skill pack for immediate use — it distills the operating workflow in William D. Gann's *Truth of the Stock Tape* into 16 capability cards arranged by process stage: from market-entry readiness, tape-reading cadence and the three-chart system, all the way to the pre-trade gate, stop-loss execution, pyramiding, portfolio checkups and loss post-mortems.

It is not a book summary, nor a reading response — it breaks the reusable methodology in the book into skill modules that can be triggered, executed and tested.

## What these skills solve

- You stare at the screen until your nerves break and trade dozens of times a year, yet cannot say what cadence you should actually keep or how many trades a year is right
- "Heavy volume, no price gain" and "shrinking volume on the way down" are familiar words, but you cannot tell whether the volume is accumulation or distribution, nor what signal would confirm either
- You want to pick strong stocks but have only price change and gut feel — no reproducible strength test, and no way to turn "breaking last year's high" into an actual candidate list
- You cannot separate a "final top" from a "medium-term correction", and when a multi-year high breaks you do not know whether to chase, wait for a pullback, or suspect a false breakout
- There is no gate before you open a position: stops get cancelled on impulse, losing trades get averaged down, targets get raised — and afterwards you can only say "I should have followed the rules"
- You have held a position for two or three years and cannot name an objective signal for staying or leaving, so you wait for news or for someone else to call it

## What was distilled

16 capability cards, organized in the order "admission first, diagnosis second, execution last":

- **Entry and reading foundations**: `readiness-gate` (entry readiness and tape-reading cadence, stage 0), `tape-reading-workflow` (reading discipline and the monthly/weekly/daily three-chart system, stage 1)
- **Supply-demand and stage diagnosis**: `volume-supply-diagnosis` (volume-based supply/demand diagnosis, stage 2), `seven-zone-positioning` (seven-zone stage positioning and extreme reversals, stage 3)
- **Stock selection and location context**: `stock-type-filter` (instrument-type filtering and rotation, stage 4), `stock-habits-profile` (per-stock habit profile and safe price location, stage 5), `strength-weakness-ranking` (strength/weakness testing and annual lists, stage 6 — the core of selection)
- **Tops, bottoms and special structures**: `final-top-bottom` (final top and bottom determination, stage 7), `low-price-accumulation` (the low-price accumulation lifecycle, stage 7b — special structure)
- **Order entry and execution**: `pretrade-checklist` (the twelve-rule pre-trade gate, stage 8), `capital-stop-loss` (capital and stop-loss management, stage 9), `breakout-execution` (breakout buy/sell execution, stage 10), `pyramid-plan` (the decreasing pyramid add-on plan, stage 11)
- **Holding and correction**: `event-news-reaction` (news discounting and event reaction, stage 12), `portfolio-annual-checkup` (annual portfolio checkup and selling on the first sign of deterioration, stage 13), `failure-mode-triage-skill` (failure-mode triage and method comparison, stage 14 — the correction loop)

Importance across the 16 cards: 7 critical, 8 high, 1 medium. The full table (capability_id, slug, importance, destination, `also_read` dependencies) is in [INDEX.md](./INDEX.md).

## Two packaging modes: single and pack

The same 16 capability cards are compiled twice. The capability content is identical; the difference is the entry name and the directory shape.

| | single (one entry) | pack (compact pack, source router entry) |
|---|---|---|
| Discoverable entries | **1**: `gann-stockmarket-control-skill` | **1**: `gann-stockmarket-control-skill-router` |
| Where the 16 cards live | All inside the entry's `references/capabilities/`, loaded 1–2 at a time by the router table | Also all inside the router's `references/capabilities/` |
| Cards promoted to standalone skills | 0 (everything goes through the router table) | **0** — all 16 stayed inside the router in this build |
| Triggering | The entry description participates in matching; routing happens after entry | Same, except the router description is explicitly labelled as the "pack source router entry" |
| Upgrades | Replace 1 directory | Replace 1 directory |
| Bundled build metadata | `BUILD_MANIFEST.json` | `BUILD_MANIFEST.json` + `capability-destinations.json` |

> Why does the pack have no promoted standalone skills? The bundle's promotion budget is 8, but the compile decision routed all 16 cards to the router (`promoted_count: 0`), so both builds expose the same number of discoverable entries. The pack's value is its distribution shape: it keeps `capability-destinations.json`, the per-card destination decision, which makes team-level splitting or later promotion easier.

### Which one to install

Pick by the way you work, and **install only one**:

| How you work | Recommended | Why |
|---|---|---|
| You use DSH / Codex / Claude Code with a skills directory and want a clean list | single | The most straightforward entry name; takes 1 slot |
| You want to audit why a card went to the router instead of becoming a standalone skill | pack | Ships `capability-destinations.json` with the destination decisions |
| You distribute to several agents or teammates and may promote cards later | pack | The directory shape matches the distribution convention and splits cleanly per card |
| You want to install once and maintain one directory | single | Upgrades replace a single directory |

> Both builds come from the same bundle and carry identical capabilities. **Installing both will double-trigger**, so pick one.

## Examples

### Example 1: three weeks of heavy turnover with no price gain — is it about to run?

**User question**

"This stock has 200 million shares outstanding. Weekly turnover over the last three weeks was 8%, 12% and 15%, yet the price rose only 2%. All that volume is piled up here — is it about to run?"

**How the skill reasons**

- Start with `volume-supply-diagnosis`: absolute volume means nothing; it must be converted to turnover (volume ÷ free float) and compared with this stock's own normal percentile
- Walk the four volume-price quadrants: heavy volume that cannot push the price up lands in "high-level heavy volume, stalled price", which reads as a distribution warning
- Overlay location: the same volume-price pattern at a high is a distribution warning, but at a multi-year low it may simply be active accumulation — that layer needs `seven-zone-positioning`, and this card does not conclude on its own
- Extreme-volume and range counting: about 17.5% cumulative turnover in three weeks; if price is still oscillating inside the same box with both edges intact, mark it "accumulation or distribution in progress"
- The output is an evidence strength, never a verdict; the confirming event is a range breakout

**Sample final answer**

> Convert it to turnover first: roughly 17.5% cumulative over three weeks is very heavy for a 200-million-share float, and the price moved only 2% — a classic "big turnover that cannot move price", which hits high-level heavy-volume-stalled-price and reads as a distribution warning. But note this is a **warning**, not a verdict: accumulation versus distribution is only confirmed by a range breakout, and volume alone cannot settle it. Two conventions need stating: single-day turnover above 7% should raise an eyebrow, but that is an experience figure quoted in the commentary — some stocks correct hard at 7%, others keep rising at 15%, so calibrate to your own name; and "8/12/15% weekly turnover" versus "7% single-day" are two different time bases, so do not mix them. The action is therefore not to chase. Mark the range edges and wait for the breakout side: only an upside break with volume supports entry, while a break down should be treated as distribution.

### Example 2: should this trade be taken at all?

**User question**

"I have 200,000 yuan. I want to buy 2,000 shares at 30 yuan. I'm already up 5%, so I plan to add straight to a full position. Is that fine?"

**How the skill reasons**

- Enter `pretrade-checklist` and check the input contract first: capital, instrument, size and entry price are present, but **no stop price** — fill the gap before passing the gate, never guess values
- Judge the twelve gates one by one, each binary: rule 1 capital (maximum loss per trade ≤ 3–5% of capital, i.e. 6,000–10,000 yuan, which cannot be computed without a stop); rule 2 stop preset (no stop price = fail); rule 4 profit protection (already up 5%, so the stop belongs at breakeven); rule 8 spreading (capital under 500k may be exempt per the commentary); rule 9 no target price (delete any intended exit and replace it with a trend-change exit); rule 10 the four selling questions
- The output is either "pass" or "fail plus remediation items" — there is no "partially passed"

**Sample final answer**

> Stop here: you gave no stop price, and "no stop price" fails gate 2 outright — there is no special case. Add the stop and we continue. Meanwhile run rule 1: maximum loss per trade must stay within 6,000–10,000 yuan (3–5% of capital — this is the compiler's conversion of the book's 3–5 points into A-share terms, not the book's own wording). At 30 yuan for 2,000 shares the position is 60,000 yuan, so the stop distance can be at most 5–8%; beyond that you cut size, you do not widen the stop. Second, "add straight to a full position" has to be rejected: rule 8 is about equal spreading, not about maxing one name, and with a 5% gain the correct move is to lift the stop to breakeven rather than add. Adding belongs to `pyramid-plan`, which only allows decreasing add-ons in the direction of open profit and forbids adding inside accumulation/distribution zones or within 10% of tops and bottoms. Third, under A-share T+1 a same-day stop is not executable, so the risk budget must be widened for next-day gaps. The conclusion is fail: supply the stop price, cut size into the risk budget, lift the stop to breakeven, then run the gate again.

## How these skills were generated

This skill set was generated with the RIA-TV++ pipeline of **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)**, in six stages:

1. **Whole-book understanding (Adler analysis)** — apply Mortimer Adler's analytical reading method to the book in four steps (structural, interpretive, critical, applied) and produce `BOOK_OVERVIEW.md`
2. **Parallel extraction** — run several specialised extractors at once (frameworks, principles, cases, counter-examples, glossary) to pull candidate methodology units out of the source text
3. **Three-fold verification** — every candidate must pass three checks: at least two independent in-book corroborations (V1 source sufficiency), a path to executable steps (V2 executability), and real task gain (V3 task utility)
4. **RIA++ construction** — structure each unit across six dimensions: R (source quote) / I (rewritten in our own words) / A1 (in-book case) / A2 (future trigger scenario) / E (executable steps) / B (boundaries and blind spots)
5. **Zettelkasten linking** — map dependencies, contrasts and combinations between cards, and generate the capability index and router table
6. **Trigger and output testing** — design trigger blind tests for the entry (including decoys: trigger when it should, stay silent or route away when it should not) plus output spot checks; failures go back for rework and are then regression-tested

One constraint shaped this distillation: the book is a different Chinese translation of the same original as the already-published *Gann Stock Market Trend Theory*, with 32 chapters mapping one to one and identical case numbers. This pack is therefore deliberately organized as an "end-to-end operating SOP" that advances by process stage, distinct from that earlier "capability-domain lookup" toolbox; the two serve as near-neighbour negative examples — "what are the twelve rules?" routes to the other skill, while "check this trade for me" enters this one.

## Testing and verification

The repository ships the generation-time test material as well: `evals/test-prompts.json` holds the entry-level trigger and boundary cases, and `evals/test-results.md` holds the item-by-item scoring record — including the failures and the rework that fixed them, not only the passing rows.

- **Trigger blind tests**: 11 cases (5 should_trigger, 3 should_not_trigger, 3 edge), final result 11 / 11 PASS
- **Decoy tolerance**: all 3 decoys (cross-skill confusion, neighbouring school, out-of-domain) were correctly blocked or routed, none falsely triggering this entry
- **Fix record**: cases 04 (cadence remediation) and 05 (building a reading system) were first mis-routed to the sister skill because the entry description lacked scenario phrasings and overlapped literally with that skill's "reading and review workflow". The fix rewrote the entry description (adding the scenario examples and sharpening the division of labour: "what is a given rule or criterion" goes there; "build a system, walk the process, run a checkup, fix my own situation" comes here), and both cases re-tested correctly. The fix landed in section A2 (description) without touching the rule body (E / B), so no rework of stage 2 was needed
- **Output spot checks**: 2 representative tasks (the volume-diagnosis card and the pre-trade card) both passed; all three stop conditions held — ask instead of guessing missing inputs, grade evidence instead of calling a trade, and state convention differences explicitly

## Repository structure

```text
gann-stockmarket-control-skill/
├── README.md                      ← the Chinese version
├── README.en.md                   ← you are reading this
├── LICENSE                        ← MIT
├── BOOK_OVERVIEW.md               ← whole-book understanding (Adler four-step, stage 0 output)
├── verified.md                    ← three-fold verification results for the 16 units
├── INDEX.md                       ← skill map: capability table + dependencies + load order
├── CANGJIE_ADAPTATION.md          ← Cangjie adaptation note: text status / goals / evidence rules / boundaries
├── TEST_SUMMARY.md                ← stage 4 stress-test summary (scope / structure check / results)
├── candidates/                    ← raw candidate pool from the five stage-1 extractors (347 items, auditable)
│   ├── frameworks.md              ← 50 framework candidates
│   ├── principles.md              ← 148 principle candidates
│   ├── cases.md                   ← 89 case candidates
│   ├── counter-examples.md        ← 39 counter-example candidates
│   └── glossary.md                ← 21 glossary candidates
├── bundle/                        ← distillation intermediates (the auditable source)
│   ├── verified.yaml              ← the canonical definition of the 16 cards (single source of truth)
│   ├── book/
│   │   ├── overview.md            ← whole-book overview
│   │   └── glossary.md            ← glossary
│   └── cards/                     ← the 16 capability cards (R / I / A1 / A2 / E / B)
├── single/                        ← one-entry mode
│   └── gann-stockmarket-control-skill/
│       ├── SKILL.md               ← entry: trigger conditions + router table + load rules
│       ├── BUILD_MANIFEST.json    ← build manifest and file hashes
│       ├── test-prompts.json      ← entry-level trigger and boundary cases (11 items, same source as evals/)
│       └── references/
│           ├── overview.md        ← whole-book overview
│           ├── capability-index.md  ← full intent and keyword index
│           ├── cheatsheet.md      ← decision-rule cheat sheet
│           ├── glossary.md        ← glossary
│           └── capabilities/      ← the 16 capability cards
├── pack/                          ← compact pack (source router entry)
│   ├── BUILD_MANIFEST.json
│   ├── capability-destinations.json
│   └── gann-stockmarket-control-skill-router/
│       ├── SKILL.md               ← source router entry
│       └── references/            ← the 16 cards + indexes, called internally by the router
└── evals/                          ← generation-time test material
    ├── test-prompts.json           ← entry-level trigger and boundary cases
    └── test-results.md             ← item-by-item scoring and fix record
```

## How to use

Clone the repository first:

```bash
git clone https://github.com/raphael-y7/gann-stockmarket-control-skill.git
```

### Install single (try this first)

```bash
# macOS / Linux
cp -r gann-stockmarket-control-skill/single/gann-stockmarket-control-skill ~/.agents/skills/
```

```powershell
# Windows
Copy-Item -Recurse .\gann-stockmarket-control-skill\single\gann-stockmarket-control-skill "$env:USERPROFILE\.agents\skills\"
```

### Install pack

Copy only the directory that contains `SKILL.md`; do not copy the two json files under `pack/` into your skills directory:

```bash
# macOS / Linux
cd gann-stockmarket-control-skill/pack
cp -r gann-stockmarket-control-skill-router ~/.agents/skills/
```

```powershell
# Windows
$pack = ".\gann-stockmarket-control-skill\pack"
$dest = "$env:USERPROFILE\.agents\skills"
Copy-Item -Recurse -LiteralPath (Join-Path $pack "gann-stockmarket-control-skill-router") -Destination $dest
```

> `~/.agents/skills` is DSH's skills directory; with another agent, use its own directory (Claude Code uses `~/.claude/skills`).

### How to confirm it works

After installing, ask "check this trade against Gann's twelve rules for me" and see whether the agent enters the twelve-gate judgment directly (capital, stop preset, frequency, breakeven…) instead of returning generic risk talk. With single installed it reads the entry first and then routes to the `pretrade-checklist` card; with pack installed the router entry does the same.

## Source

- *Truth of the Stock Tape* by William D. Gann
- 32 chapters distilled into 16 capability cards

## Disclaimer

This repository publishes only the distilled skills, indexes and rule cheat sheets. It does not contain the original PDF, EPUB, OCR files, screenshots or a full transcript of the book. Quotations that appear inside capability cards serve only to attribute the methodology and keep the material auditable.

Every numeric criterion in the book (3–5 points per trade, 7% turnover, the 100→50→30→20→10 pyramid, the 3-point stop beyond the range, and so on) is a case-based or experiential generalisation; the book offers no statistical backtest, and most of these figures are 1920s US absolute price points that must be converted into percentage or volatility terms before use on A shares, with the convention stated at the time of use. Nothing in this repository constitutes investment advice.

## License

[MIT](./LICENSE)
