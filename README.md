# Zydeco

## Zydeco Scout — football opponent intelligence & game-plan builder

A product for coaching staffs that turns opponent film, audio and text into a
game plan: tendencies, tells, next-call probabilities, player vulnerabilities,
matchups, and an attack plan with the evidence behind every recommendation.

| File | What it is |
|---|---|
| [`docs/PRODUCT_SPEC.md`](docs/PRODUCT_SPEC.md) | Full product specification: data capture (video, audio, text), tagging dictionary, analytics engines, outputs, recommended process improvements, architecture, compliance, roadmap |
| [`docs/BUSINESS_PLAN.md`](docs/BUSINESS_PLAN.md) | Positioning, pricing hypotheses, go-to-market, the 15-minute sales demo, milestones |
| [`scout/index.html`](scout/index.html) | Working prototype (open in any browser; no install, no server) |

### Prototype

Open `scout/index.html` in a browser. It loads a **fictional** opponent
(4 games, ~370 tagged snaps, full rosters) so every screen is populated:

- **Overview**: KPIs, keys to victory, availability/position-fit watch
- **Tendencies**: filter by down, distance, field zone, hash, quarter, score, 2-minute, personnel, formation, game; one click turns any filter into a film cut-up
- **Tells**: pre-snap indicators with evidence thresholds (≥ 8 snaps, ≥ 20-point swing, strong only across 3+ games)
- **Next-Call Predictor**: similarity-weighted, recency-weighted probabilities with a hierarchical Bayesian prior and a confidence label
- **Situations**: 3rd down, red zone, two-minute, scripted openers, sudden change, 4th-down decisions, fatigue by quarter, halftime shifts
- **Personnel**: experience, technique/footwork/confidence grades, injuries, out-of-position flags, charted errors, vulnerability score
- **Matchups**: our players vs theirs, ranked advantages and risks
- **Attack Plan**: auto-generated advantages, disadvantages and how to attack, with evidence
- **Film Room**: load game film, tag snaps at timestamps, dictate notes, record audio notes, jump to clips
- **Intel**: articles, transcripts and notes with automatic player links and injury/depth-chart flags
- **Report**: printable scouting report (print or save as PDF)
- **Data**: JSON/CSV import and export, matchup pairings, reset

All data stays in the browser (localStorage).

## YouTube channel search (earlier utility)

`index.html` at the repo root is a separate single-page tool to search YouTube
channel names: open it, paste a free YouTube Data API v3 key (saved locally
only), and search.
