<h1 align="center">Gann Stockmarket Control Skill</h1>

<p align="center"><a href="README.md">中文</a> | English</p>

An AI skill pack for immediate use — it distills the operating method in *Gann Stockmarket Control* ("read supply and demand first, locate the phase second, act only on a confirmed breakout, and stay alive with stop orders") into 16 capability cards arranged in workflow order, from pre-market preparation all the way to failure triage.

It is not a book summary, nor a reading response — it breaks the reusable methodology in the book into skill modules that can be triggered, executed and tested.

## What these skills solve

- You have read plenty of technical analysis and still do not know which step comes first when you actually place an order: this pack lays the 16 steps out as one pipeline and tells you which step you are on and what comes next
- Volume expands without price following, and you cannot tell distribution from ordinary turnover — without separating absolute volume from turnover measured against shares outstanding, every volume expansion looks like a signal
- You cannot say whether the market sits in a high-level distribution zone or a low-level accumulation zone: the same "heavy turnover, no price progress" means opposite things at the top and at the bottom, and without the location context you trade the signal backwards
- You trade dozens of times a year and burn out watching the screen, yet cannot say how often you should look at the tape, how many trades a year is too many, or when you must step away
- You can never bring yourself to place a stop, or you place one, cancel it, then widen it — and you have never computed how many losses your account can absorb
- After a loss you only say "bad luck": there is no symptom-driven triage table, and no clear line between averaging down and adding to a winner

## What was distilled

16 capability cards, organized in workflow order — prepare, diagnose, select, time, execute, hold and correct — one card per step:

- **Preparation and tape reading (steps 0–1)**: `readiness-gate` (entry readiness and tape-reading rhythm), `tape-reading-workflow` (tape-reading discipline and the monthly / weekly / daily three-chart system)
- **Supply, demand and location (steps 2–3)**: `volume-supply-diagnosis` (volume-based supply and demand diagnosis), `seven-zone-positioning` (seven-zone phase positioning and extreme reversal)
- **Selection and profiling (steps 4–6)**: `stock-type-filter` (instrument type filtering and rotation), `stock-habits-profile` (per-stock habit profile and safe location), `strength-weakness-ranking` (strength and weakness ranking with the annual list)
- **Tops, bottoms and special structures (steps 7–7b)**: `final-top-bottom` (final top and bottom determination), `low-price-accumulation` (life cycle of a low-priced accumulation stock)
- **Order entry and execution (steps 8–11)**: `pretrade-checklist` (the twelve pre-trade rules), `capital-stop-loss` (capital and stop-loss management), `breakout-execution` (breakout entry and exit execution), `pyramid-plan` (pyramid scaling-in plan that decreases with the trend)
- **Events, holding and correction (steps 12–14)**: `event-news-reaction` (news discounting and event reaction), `portfolio-annual-checkup` (annual portfolio checkup and selling on the first sign), `failure-mode-triage-skill` (failure-mode triage and comparison of operating methods)

## Two packaging modes: single and pack

The same 16 capability cards are compiled twice, at two granularities. The cards are identical; the difference is how the entry is named and how the manifests record ownership.

| | single (one entry) | pack (compact pack, source router) |
|---|---|---|
| Discoverable entries | **1**: `gann-stockmarket-control-skill` | **1**: `gann-stockmarket-control-skill-router` (a source router; this pack promotes no card to a standalone skill) |
| Where the 16 cards live | All inside the entry's `references/capabilities/`, loaded one at a time by the routing table, at most two when a task crosses domains | The same 16, inside the router's `references/capabilities/`; the pack root carries two manifests that record each card's owner |
| Triggering | The entry description states the situations directly (build a system / run the workflow / do a checkup / fix my setup) | The router description presents itself as a source router, then routes through the ownership table in `capability-destinations.json` to the same cards |
| Upgrades | Replace 1 directory | Replace 1 router directory and keep `BUILD_MANIFEST.json` and `capability-destinations.json` in sync |

No card in this pack was promoted to a standalone skill — all 16 are served by the router — so the two builds ship byte-identical cards and indexes; only the entry name, the description wording and the manifest files differ.

### Which one to install

Pick by the way you work, and **install only one**:

| How you work | Recommended | Why |
|---|---|---|
| You use DSH / Codex / Claude Code with a skills directory and want a clean list | single | Takes 1 slot and loses none of the 16 steps |
| You want manifests to audit which entry owns each card, or to distribute by ownership table to several agents | pack | `capability-destinations.json` records `served_by` and the card path for every card |
| You want to install once and maintain one directory | single | Upgrades replace a single directory |
| You want both the published hashes and the per-card ownership table for integrity checks | pack | Both manifests are present; single ships only `BUILD_MANIFEST.json` |

> Both builds come from the same bundle and carry identical capabilities. **Installing both will double-trigger**, so pick one.

## Examples

### Example 1: three weeks of heavy turnover with a two-point gain — should I sell?

**User question**

"This stock turned over 8%, 12% and 15% in three straight weeks, but the price is up only two points. Is the smart money distributing? Should I get out?"

**How the skill reasons**

- Enter `volume-supply-diagnosis`; the first step is not interpretation but **turnover calibration**: volume ÷ shares outstanding = turnover rate, so "heavy volume" is restated on a share-count basis. The card's input contract states that without shares outstanding no turnover conclusion may be given, and only the price structure can be used
- Run the four-quadrant volume/price walk: volume expanding while price stalls lands in the "distribution warning" quadrant — in the book's words, heavy turnover that cannot move the price means someone keeps supplying stock
- Overlay location: the same heavy-turnover stall is a distribution warning at a high level and may be active accumulation at a multi-year low; location comes from `seven-zone-positioning` and `final-top-bottom`
- Check for a record-volume day, and count range oscillations: 5%-level swings repeating 10–20 times inside one box whose edges hold means accumulation or distribution is still in progress
- The output is an evidence strength plus the next verification point, not a one-word "sell"

**Sample answer**

> Before asking whether to sell, restate it on a share-count basis: turnover = volume ÷ shares outstanding. Three weeks at 8% / 12% / 15% with the price up only 2% does land in the "heavy turnover, no progress" cell, and the reading is a **distribution warning** — heavy turnover that cannot move the price means someone keeps supplying stock. But that is an evidence strength, not a verdict: final confirmation of accumulation or distribution must wait for a range breakout, and the card explicitly forbids concluding from volume alone. Second, add location: the same pattern at a multi-year low may be active accumulation, so check which of the seven zones the price sits in and whether a historical top or bottom band hangs above. Third, check two things — whether a record-volume day has appeared recently (mark it as a suspected end of the move), and how many 5%-level swings this box has already produced. As for "how much turnover is abnormal": the 7% single-day alert line quoted in the card is an experienced rule of thumb from the book's commentary, and stocks differ widely (some correct hard at 7%, others keep rising at 15%), so it must be calibrated per instrument and never treated as a hard threshold. Conclusion: this is a distribution warning (directional, unconfirmed); the action is to trim and watch, then wait for the range to break, not to act on a single word.

### Example 2: a 200,000 CNY account — can I widen the stop to -20% to survive the shakeout?

**User question**

"I have 200,000 CNY and want to buy a 30 CNY stock with a -2.5% stop, but I am afraid of being shaken out. Can I just set the stop at -20% and sit through it?"

**How the skill reasons**

- Enter `capital-stop-loss`; the first step is not choosing a stop level but computing **how many losses the account can absorb** = capital ÷ maximum loss per trade, with a floor of 10
- 200,000 × 2.5% = 5,000 CNY per trade → 40 losses, which passes; at 20% the maximum loss per trade is 40,000 CNY → only 5 losses, far below 10, so the card's stop rule fails the trade outright (hand it to `pretrade-checklist`)
- Stop-order mechanics: placed together with the entry, G.T.C. (good till cancelled), filled at the best available price and therefore possibly worse than the trigger
- Five disciplines: every trade gets a stop; once placed it is not cancelled; it is not moved in the direction of a larger loss; the earlier the better; it is cancelled only on closing the position or on delivery
- Profit protection: at +3–4% (converted) move the stop to break-even, then follow `pyramid-plan`; after two or three consecutive losses, stand aside

**Sample answer**

> Do not debate the 20% figure — do the arithmetic: losses the account can absorb = capital ÷ maximum loss per trade. With 200,000 and a 2.5% stop the maximum loss per trade is 5,000 CNY, so 40 losses, which passes. At 20% the maximum loss per trade is 40,000 CNY, so only 5 losses, and the trade fails outright — this is not a question of surviving a shakeout, the account structure does not allow it. One convention must be stated: the book's original parameter is a "3–5 point stop" (1 point = 1 USD of price), and converting it to 2.5%–5% is an adapter's patch for A-shares, not the book's own text, so the percentage still needs calibrating to the stock's volatility. A local risk belongs in the conclusion too: the book assumes a stop order always fills, and on A-shares a run of limit-down days or a liquidity freeze breaks that assumption, so the stop may not fill at all. As for the fear of being shaken out — the card's position is that "the stop was hit and then price reversed" is not a reason to cancel the stop; if you are stopped out repeatedly, the problem is entry location (back to the per-stock habit profile card), not the stop discipline. Operationally: buy at 30 and place the stop at 29.25 at the same time, move it to 30.05 for break-even once price reaches 31.1 (about +3.7%), then follow the pyramid card step by step.

## How these skills were generated

These skills were produced with the **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** RIA-TV++ pipeline, in six stages:

1. **Whole-book comprehension (Adler analysis)** — apply Mortimer Adler's analytical reading method to the book (structure, interpretation, criticism, application) and settle the distillation route: workflow-driven rather than capability-domain lookup
2. **Parallel extraction** — several specialized extractors (frameworks, principles, cases, counter-examples, terminology) mine candidate methodology units from the source text; this book yielded 347 candidates
3. **Triple verification** — every candidate must pass three checks: sufficient in-book sourcing (V1), a walkable input with an expected deliverable (V2), and real gain for the reader's task (V3); after merging and de-duplication, 16 capability units remained
4. **RIA++ construction** — structure each unit along R (quotation) / I (restatement in own words) / A1 (in-book case) / A2 (future trigger scenario) / E (executable steps) / B (boundaries and blind spots); every conversion of the book's point-based parameters into A-share percentages is labelled as an adapter's patch
5. **Zettelkasten linking** — number the 16 cards along the trading workflow (step 0 to step 14), mark each card's upstream and downstream neighbours plus "how it differs from the adjacent capability", and generate the capability index and routing table
6. **Trigger and output testing** — design trigger blind tests for the entry (including decoys: fire when they should, stay silent when they should not) and sample real outputs; failing entries go back for rework of the entry description and are re-verified afterwards

What is special about this book is the workflow framing: the same source text already has a sister skill for single-point capability lookups, so this distillation deliberately takes the end-to-end SOP route — it does not answer "what exactly is rule N", it walks with you through building a system, running the process, doing a checkup and fixing your own setup.

## Testing and verification

This repository publishes the test material from the generation process alongside the skills: `evals/test-prompts.json` holds the entry-level trigger and boundary cases, and `evals/test-results.md` is the item-by-item scoring log — including the failures and the rework, not just the passes.

- **Trigger blind tests**: 11 cases (5 should trigger, 3 decoys that should not, 3 boundary). Nine were correct on the first pass; cases 04 and 05 were mis-routed to the sister skill, fixed by rewriting the entry description (adding the "fix my rhythm / build a system" situation examples and sharpening the division of labour), and both routed correctly on re-test — 11 / 11 in the end
- **Decoy interception**: all three decoy types — cross-skill confusion (listing the twelve rules), out of domain (fundamental valuation), neighbouring school (Chan theory line drawing) — were correctly blocked or handed off, with no false trigger
- **Output sampling**: two representative tasks (volume diagnosis in a normal scenario, pre-trade checks with missing inputs) met their output contracts item by item; all three stop clauses — ask instead of guessing missing values, grade the evidence instead of calling a trade, never promise a price target — held, 2 / 2
- **Convention conflicts**: two disagreements found during sampling (weekly turnover versus the 7% single-day threshold, and two ways of accumulating turnover) were labelled explicitly in the record rather than silently resolved
- **Test environment**: the record states the test model and host were a GLM-5.3 subagent on the ZCode Agent tooling, not this repository's runtime

## Repository layout

```text
gann-stockmarket-control-skill/
├── README.md                      ← Chinese version
├── README.en.md                   ← you are reading this
├── LICENSE                        ← MIT
├── BOOK_OVERVIEW.md               ← whole-book comprehension (Adler four-step, stage 0 output)
├── verified.md                    ← triple-verification conclusions for the 16 capability units
├── single/                        ← single-entry build
│   └── gann-stockmarket-control-skill/
│       ├── SKILL.md               ← entry: triggers + routing table + loading rules
│       ├── BUILD_MANIFEST.json    ← build manifest and file hashes
│       └── references/
│           ├── overview.md        ← whole-book overview
│           ├── capability-index.md  ← full intent and keyword index
│           ├── cheatsheet.md      ← decision-rule quick reference
│           ├── glossary.md        ← glossary
│           └── capabilities/      ← 16 capability cards
├── pack/                          ← multi-entry build (compact pack)
│   ├── BUILD_MANIFEST.json
│   ├── capability-destinations.json
│   └── gann-stockmarket-control-skill-router/
│       ├── SKILL.md               ← source router entry
│       └── references/            ← 16 cards + indexes, called by the router
└── evals/                         ← test material
    ├── test-results.md            ← item-by-item scoring and rework log
    └── test-prompts.json          ← entry-level trigger and boundary cases
```

## Usage

Clone the repository first:

```bash
git clone https://github.com/raphael-y7/gann-stockmarket-control-skill.git
```

### Install single (recommended first try)

```bash
# macOS / Linux
cp -r gann-stockmarket-control-skill/single/gann-stockmarket-control-skill ~/.agents/skills/
```

```powershell
# Windows
Copy-Item -Recurse .\gann-stockmarket-control-skill\single\gann-stockmarket-control-skill "$env:USERPROFILE\.agents\skills\"
```

### Install pack

Copy only the directory that contains a `SKILL.md`; do not copy the two JSON files under `pack/` into your skills directory:

```bash
# macOS / Linux
cd gann-stockmarket-control-skill/pack
cp -r gann-stockmarket-control-skill-router ~/.agents/skills/
```

```powershell
# Windows
$pack = ".\gann-stockmarket-control-skill\pack"
$dest = "$env:USERPROFILE\.agents\skills"
Copy-Item -Recurse -LiteralPath (Join-Path $pack 'gann-stockmarket-control-skill-router') -Destination $dest
```

> `~/.agents/skills` is the DSH skills directory; with another agent, use its own skills directory (for example `~/.claude/skills` for Claude Code).

### How to verify the install

Ask: "Walk this stock through Gann's method from start to finish." The agent should read the entry first and then load only one capability card from the routing table, rather than reading all 16 at once. Then ask: "My holdings are due for an annual checkup." It should route to `portfolio-annual-checkup` instead of giving generic long-term-holding advice.

## Sources

- *Gann Stockmarket Control*
- Distilled from the whole book, producing 16 capability cards

## Notice

This repository publishes distilled skills, indexes and rule quick references only. It contains no PDF, EPUB, OCR files, screenshots or full-book transcripts of the source book. Quotations that appear in the capability cards serve solely to attribute methodology and keep the material auditable.

The point-based parameters in the book (a 3–5 point stop, adds every 10 points, a 1–5 point first signal, and so on) are absolute 1920s US price levels; the percentages used in this repository are an adapter's patch, not the book's own text. Every criterion is a case- and experience-based rule without statistical backtesting; test it on your own instruments and declare the convention you use. Nothing in this repository is investment advice.

## License

[MIT](https://opensource.org/licenses/MIT)
