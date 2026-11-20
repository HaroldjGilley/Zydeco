# Zydeco Scout — Opponent Intelligence & Game-Plan Platform

**Product specification, v1.0** · Working product name: *Zydeco Scout* (run a trademark search before launch)

---

## 1. Executive summary

Coaching staffs at every level spend 20–40 staff-hours a week breaking down an
opponent: watching film, tagging plays in spreadsheets, building tendency
charts, writing scouting reports, drawing scout-team cards, and arguing about
what the opponent will call on 3rd & 6. Most of that work is manual, it
lives in separate tools, and the hardest-won insights (a young corner who
panics against double moves, a tackle playing out of position because the
starter is hurt, a coordinator who always runs the same play after a
turnover) live in one coach's head.

**Zydeco Scout** turns film, audio, and text about an opponent into one
structured, searchable intelligence picture, and then into a game plan:

1. **Capture everything.** Video (game film, all-22, end zone, broadcast),
   audio (coach dictation, broadcast commentary, press conferences, radio
   shows) and text (box scores, play-by-play, depth charts, injury reports,
   news, notes) in one place, every item linked to the play, player, and
   situation it describes.
2. **Structure it.** A standard tagging system for every snap (situation,
   personnel, formation, alignment, concept, result) and every player
   (experience, technique, footwork, engagement wins, confidence, injury,
   position fit). AI does the first pass and coaches confirm or correct it.
3. **Find the edges.** A tendency engine, tell (giveaway) detection,
   next-call probabilities with honest confidence levels, situational and
   clock analysis, and player-vs-player matchups.
4. **Deliver the plan.** An auto-built scouting report, an attack plan
   ("how to beat them" by position and by player), call-sheet suggestions by
   situation, scout-team cards, player-specific cut-ups sent to phones, and a
   halftime and post-game accuracy review.

The goal of the product is **more correct decisions in less staff time**.
Every recommendation shows its evidence (the clips and the sample size), so
coaches trust it, can check it, and stay in charge.

---

## 2. Customers and users

### 2.1 Market segments

| Segment | Staff size | Current tools | Primary pain | Willingness to pay |
|---|---|---|---|---|
| High school (varsity) | 4–12 coaches, mostly part-time | Hudl film exchange, spreadsheets, whiteboards | No time; teachers coaching at night | Moderate; booster-funded |
| Small college (NAIA / D-III / D-II / JUCO) | 6–12, few or no analysts | Hudl or XOS, Excel | Limited analyst staff | Moderate–high |
| FCS / FBS | 10 coaches + 10–40 support/analysts | XOS, DVSport, Catapult, PFF, in-house tools | Too much data, not enough synthesis | High, but slow procurement |
| Semi-pro, arena, international, 7-on-7 | Small | Ad hoc | No tooling at all | Low–moderate |
| Youth associations (12U+) | Volunteers | Nothing | Simplicity | Low (freemium funnel) |

**Beachhead:** varsity high school and small college programs. They have the
most manual work, the fewest analysts, short buying cycles (often one head
coach plus an athletic director) and strong word-of-mouth through clinics and
coaching associations.

### 2.2 Personas and what each one needs

| Persona | Primary questions | Key screens |
|---|---|---|
| **Head coach** | "What wins this game? Where are we at risk? What's our 4th-down/2-pt plan?" | Executive game-plan summary, keys to victory, decision charts |
| **Offensive coordinator** | "What coverage/pressure will I see by down & distance and field zone? Who do I attack?" | Defensive tendencies, blitz/coverage maps, matchup board, call-sheet suggestions |
| **Defensive coordinator** | "What do they run from each formation/personnel? What are their tells?" | Offensive tendencies, tell board, next-call predictor, scout cards |
| **Special-teams coordinator** | "Hang times, operation times, return lanes, fake indicators" | ST module |
| **Position coach** | "How do I beat *this* player? What does my guy see?" | Player cards, footwork/technique notes, one-on-one cut-ups |
| **Quality control / analyst** | "Tag fast, keep data clean, build the reports" | Film tagger, bulk import, data QA, report builder |
| **Athletic trainer / strength coach** | Own-team load and injury (internal only) | Snap counts, load, availability |
| **Players** | "What do I need to know about my matchup?" | Mobile player packet, cut-ups, quizzes |
| **Athletic director** | "Is this worth it? Is it compliant and secure?" | Usage, time saved, compliance settings |

---

## 3. The game week, and where the product fits

| Day (Saturday game) | Typical staff activity | Zydeco Scout role |
|---|---|---|
| **Sat night / Sun AM** | Grade own game, exchange film | Auto-import own film + opponent's last 3–4 games; AI pre-tags formations, personnel, down/distance (from scoreboard OCR), result |
| **Sunday** | Breakdown, tendency charts, first game-plan ideas | QC confirms tags; tendency, tell and matchup engines run; draft scouting report generated; self-scout report shows *our* tendencies the opponent will see |
| **Monday** | Install plan, scout cards | Scout-team cards auto-drawn from the opponent's most frequent plays per situation; player packets pushed to phones |
| **Tue–Wed** | Practice, situational periods | Practice script suggestions (3rd down, red zone, 2-minute) weighted by what the opponent actually does; "tendency breaker" alerts |
| **Thursday** | Finalize call sheet | Call-sheet builder ranks our plays by situation vs. their expected look; 4th-down/2-pt decision chart |
| **Friday / game day** | Walk-through, final reminders | Printable one-page "keys" sheet; sideline tablet mode (only where rules allow) |
| **In game** | Adjustments | Press-box live tracker updates tendencies in real time (where allowed); halftime report: what changed vs. scouting |
| **Post-game** | Review | Prediction accuracy report: what we called right, what surprised us, and model calibration |

---

## 4. Data capture

### 4.1 Video

| Source | Ingest method | What we extract |
|---|---|---|
| Opponent game film (sideline + end zone) | Upload, film-exchange export (e.g. Hudl/XOS exports), shared link | Every snap, cut into clips automatically |
| All-22 / tight end-zone | Upload | Full alignment and assignment detail |
| Broadcast / streaming replays | Upload or link (respect copyright and licensing) | Supplemental angles, crowd noise, clock |
| Own practice film | Upload, camera integration | Self-scout and scout-team accuracy |
| Drone / practice cameras | Upload | Formation and spacing |

**Automatic processing pipeline (phased; see roadmap):**
1. **Snap detection** splits a full game into play clips (motion onset + audio whistle + scoreboard changes).
2. **Scoreboard OCR** reads quarter, clock, score, down, distance, ball spot when a scoreboard or broadcast graphic is visible.
3. **Field registration** maps video pixels to field coordinates using yard lines and hashes (homography), giving ball spot, hash and player positions in yards.
4. **Player detection and tracking** (object detection plus multi-object tracking) and **jersey-number recognition** to identify players.
5. **Formation and personnel classification**: counts RB/TE/WR by alignment, labels the formation (Trips, Doubles, Empty, I, Pistol, Bunch…), backfield set, strength, splits and depths.
6. **Pre-snap motion and shift detection**, and **tempo** (seconds from ball-ready to snap).
7. **Play-type and concept suggestion**: run/pass/RPO/screen, run scheme (zone/gap/power/counter/trap), pass concept (stick, mesh, smash, verticals…), coverage shell (MOFC vs MOFO) and rotation, pressure count and source.
8. **Pose estimation** for technique metrics: stance, first-step direction/length, false steps, pad level, hip-flip timing, QB drop depth and base width, hand placement on engagements.
9. **Speed and effort metrics**: top speed, closing speed, pursuit angle, time-to-throw, time-to-pressure, yards after contact.

Every AI tag carries a **confidence value**. Anything below a threshold goes to
a QC queue. Coaches always confirm or correct, and corrections retrain the
models for that customer (and, with consent, the shared models).

### 4.2 Audio

| Source | Use |
|---|---|
| **Coach dictation** while watching film ("#54 false-steps on every pass set, left side") | Speech-to-text attaches the note to the current clip, timestamp and player number |
| **Broadcast commentary** | Transcribed; mentions of injuries, player names, scheme notes, crowd/noise context |
| **Opponent coach press conferences, radio and podcast shows (public)** | Transcribed and summarized: injury hints, depth-chart changes, philosophy, "we need to run the ball better" type signals |
| **Stadium noise level** | Decibel profile for planning silent counts on the road |
| **QB cadence (from public film audio)** | Cadence patterns and hard-count frequency, used to plan defensive snap anticipation |

> **Hard line:** the product never captures or decodes an opponent's live
> sideline signals by electronic means, and never records audio or video at an
> opponent's practice. Doing either violates NCAA rules and most state
> association rules, and is unsportsmanlike at every level. Only lawfully
> obtained film and public audio are ingested. See §11.

### 4.3 Text and structured data

- Box scores, play-by-play logs, season stats (state association sites, team sites, league sites)
- Rosters (height, weight, class, position, number) and depth charts
- Injury reports, news articles, local beat writers, public team social media
- Recruiting profiles (verified speed, offers, measurables)
- **Coaching staff history**: a new OC or DC brings their old system, so we import tendencies from the coach's previous school
- **Officiating crew** assignments and that crew's penalty tendencies (holding, DPI, false start rates)
- **Weather and field**: forecast, wind, turf vs grass, altitude, kickoff time
- **Travel and rest**: short weeks, bye weeks, travel distance
- Free-text coach notes, with `#number` and `@position` mentions auto-linked to player records

### 4.4 Own-team data (self-scout and availability)

- Our own tagged plays, so we see the tendencies *opponents* see in us
- Player availability, snap counts, practice participation, GPS load (from Catapult/STATSports-type wearables where available)
- Our players' measurables and grades, which drive the matchup engine

---

## 5. Data dictionary (what we tag)

### 5.1 Every snap: situation

| Field | Values / notes |
|---|---|
| Game, opponent, date, home/away, surface, weather | |
| Quarter, game clock, play clock at snap | Clock drives 2-minute and 4-minute logic |
| Score differential (from the team's view) | Buckets: down 9+, down 1–8, tied, up 1–8, up 9+ |
| Timeouts remaining (both teams) | |
| Down, distance | Distance buckets: 1–2 short, 3–6 medium, 7–10 long, 11+ very long |
| Ball spot (yards to goal) | Zones: backed up (−1 to −10), own territory, midfield, plus territory (opponent 40–21), red zone (20–11), high red (10–4), goal line (3–1) |
| Hash | L / M / R; also derived *boundary vs field* |
| Drive context | Play # of drive, after turnover (sudden change), after explosive play, after penalty, first play of half, opening script (plays 1–15) |
| Tempo | Huddle / no-huddle / hurry-up / milk-clock |

### 5.2 Offense

Personnel (RB-TE count: 10, 11, 12, 13, 20, 21, 22, jumbo), formation family,
strength, backfield set (gun, pistol, under center, offset), receiver splits,
TE alignment (in-line, wing, flex), motion/shift type, play type
(run / pass / RPO / screen / play-action / QB run / trick), run scheme (inside
zone, outside zone, power, counter, duo, trap, iso, sweep, jet, option),
direction and gap, pass concept, protection (5/6/7-man, slide direction),
primary target, ball carrier, QB drop/launch point, time-to-throw, result
yards, outcome (1st down, TD, turnover, sack, penalty, incomplete), explosive
(run ≥ 12, pass ≥ 16).

### 5.3 Defense

Front (4-3 over/under, 3-4, tite/mint, 4-2-5, 3-3-stack, bear), technique
alignment of each DL, LB depth, coverage shell pre-snap and post-snap
(Cover 0, 1, 2, 2-man, Tampa 2, 3, quarters/4, 6, match variations),
rotation direction, pressure (4-man, 5-man, 6+, simulated pressure,
creeper), blitzer source (Mike, Will, Sam, nickel, corner, safety),
stunts/games, CB technique (press/off/bail), defensive substitution
by offensive personnel, disguise rate (pre-snap shell ≠ post-snap coverage).

### 5.4 Special teams

Kickoff (depth, hang time, direction, onside indicators), kick return
(scheme, return lane), punt (operation time, hang time, directional,
punter steps, rugby-style), punt return (hold-up vs return vs block), FG/PAT
(operation time, range, block weaknesses at specific gaps), fakes, two-point
plays.

### 5.5 Per-player observations (per snap or per game)

| Category | Measures | How captured |
|---|---|---|
| **Experience** | Class/age, career starts, snaps this season, years in system, position change history | Roster + snap counts |
| **Engagement results** | Won/lost/neutral each rep (OL/DL/TE/LB/DB block and shed); pressures allowed; tackles, missed tackles, broken tackles | Tagging + CV |
| **Technique & footwork** | Stance tells (weight forward = run), first step quality, false steps, base width, pad level, hand placement, backpedal and hip-flip, QB drop and reset, eye discipline (peeking into the backfield) | Pose estimation + coach rubric |
| **Speed & effort** | Top speed, pursuit angle quality, loafs, effort grade by quarter | Tracking + rubric |
| **Assignment** | Correct / bust / blown coverage; communication breakdowns | Coach grade |
| **Confidence & composure** | Body-language rubric (see §15.2): reaction after a bad play, hesitation pre-snap, glances to sideline, penalty after frustration | Coach rubric, standardized |
| **Ball skills** | Drops, contested catch rate, fumbles, ball security (carry side, high-and-tight) | Tagging |
| **Discipline** | Penalties by type, pre-snap penalties under crowd noise | Tagging |
| **Health / availability** | Public injury status; *observed* signs (limping, a brace or wrap that is new, missed series, reduced snap share, avoiding contact on one side) | Text + observation; always labeled "observed, unconfirmed" |
| **Position fit** | Natural position vs current position; backups forced into starting roles; a player playing two ways (fatigue risk) | Roster + depth chart + snap data |
| **Fatigue** | Performance by quarter and by drive length, snaps per game, two-way players | Derived |

---

## 6. Analytics engines

### 6.1 Tendency engine

- Cross-tab any tag by any other: e.g. *run % by personnel × field zone*,
  *blitz % by down × distance bucket*, *coverage by formation into the
  boundary*.
- **Every percentage shows its sample size** ("72% run, n = 18") and is
  colored by confidence. Fewer than 5 plays is shown as "insufficient".
- **Recency weighting**: last game counts more than the one 4 weeks ago
  (configurable half-life, default 2 games).
- **Opponent quality adjustment**: tendencies against teams with our
  personality (e.g. odd fronts, spread offenses) are weighted up.
- **Game-script filter**: remove garbage time (win probability > 95% or
  < 5%) so blowouts don't skew results.

### 6.2 Tell (giveaway) detection

The engine scans every pre-snap feature for an outsized link to the play
call, and only promotes a tell when it holds across **≥ 3 games** and **≥ 8
snaps**:

- Formation, personnel, back alignment (offset toward the play side), RB depth
- OL stance and weight (heavy hand down = run), split width (wider = pass)
- TE alignment and motion type (jet motion → sweep or fake?)
- QB under center vs gun by situation
- Receiver splits (tight split = crack or a breaking route)
- Defensive tells: safety depth/width, corner leverage, LB walk-up, DL
  alignment shift → pressure or coverage indicators; late rotation habits
- Personnel substitution patterns (a specific player in = a specific play)

Output: *"Pistol with RB offset left: 89% run left (n = 19, 3 games). Tell
strength: high."*

### 6.3 Next-call predictor

Given a situation (down, distance, field zone, hash, score, time, personnel,
formation if known), return a probability distribution:

```
3rd & 6, opp 38, left hash, Q3, up 3, 11 personnel, Trips Rt
  Pass          71%  ███████████████
    Stick/Snag  24%
    Mesh        18%
    Smash       12%
  Run           18%  ████   (QB draw 9%, Inside zone 6%)
  Screen        11%  ██
  Confidence: MEDIUM (effective sample = 23 similar plays)
  Top target: #2 slot (41% of 3rd-down targets)
```

**Method (MVP, explainable):** similarity-weighted frequencies (plays
weighted by how closely they match the situation) blended with a Bayesian
prior from the opponent's overall tendency, so small samples never produce
false certainty. Recency weighting is applied as well.

**Method (v2+):** gradient-boosted trees or a calibrated multinomial model
trained on the opponent's own history, the coordinator's history at previous
jobs, and league-wide priors for that level.

**Calibration is published.** After every game the product checks its own
predictions (Brier score, top-1 hit rate, reliability curve), and the coach
sees how trustworthy the model has been for this opponent and for the season.
A model that claims 70% must be right about 70% of the time.

### 6.4 Situational and clock analytics

- **3rd down** by distance bucket: play type, concepts, targets, pressure faced/sent
- **Red zone and goal line**: favorite plays, personnel, fade/back-shoulder rate, QB runs
- **Two-minute and end of half**: tempo, sideline routes, timeout use, spike/clock habits
- **Four-minute (protecting a lead)**: run rate, formation tightening
- **Backed up**: conservative vs aggressive, punt-formation risk
- **4th down**: their go/punt/kick decisions by field zone and distance, compared with an
  expected-points model, plus *our* recommended decision chart for this
  opponent (adjusted for their offense/defense strength and weather)
- **2-point attempts**: tendencies and favorite plays; our 2-pt chart
- **Opening script**: their first 10–15 plays across games (often scripted, highly predictable)
- **Sudden change**: play call after a turnover; after explosive plays; after a sack
- **Halftime adjustments**: first-half vs second-half tendency shifts
- **Score state**: how aggressive they get when trailing

### 6.5 Player evaluation and matchups

- **Player card** for every opponent starter and key backup: experience,
  measurables, grades, technique notes, tells, injury flags, position fit,
  fatigue profile, best clips and worst clips.
- **Vulnerability score** (0–100) built from: low grades, youth/inexperience,
  out of natural position, observed injury, high missed-tackle/bust rate,
  low confidence score, fatigue drop-off.
- **Matchup engine**: our player vs their player at every natural pairing
  (WR vs CB, slot vs nickel/LB, OT vs DE, G vs DT, TE vs LB/S, RB vs LB in
  protection), comparing size, speed, experience and grades. Output is a
  ranked **mismatch board**: the 5 matchups to attack and the 3 to protect.

### 6.6 Attack-plan generator

Rule-based plus model-driven recommendations, each with evidence clips:

| Observation | Recommended attack |
|---|---|
| CB false-steps / bites on stems; inexperienced | Double moves (sluggo, stop-and-go), back-shoulder, PA shots at him |
| CB plays press but loses at the line | Quick fades, slants; stack/bunch to avoid press |
| Safety with poor eye discipline (peeks at the backfield) | Play-action posts, seams; flood his side |
| Aggressive downhill LB | Play-action, counter, screens behind him, RB angle routes |
| Slow-reacting / heavy LB in coverage | Isolate with RB/TE, option routes, mesh |
| DE crashes hard on every run | Bootleg, QB keep, reverse, read option on him |
| DE who rushes upfield wide | Trap, draws, inside zone into the vacated lane |
| Young OT on a short edge / backup OT | Speed rush, games/twists on his side, overload pressure |
| OL that struggles with stunts | T-E and E-T games, twist on long downs |
| Injured / limited player (observed) | Make him move laterally, run at him, increase tempo |
| Heavy blitz on 3rd & medium | Screens, quick game, hot routes, max protection with shot plays |
| Single-high on early downs | Boundary runs vs the box count, seam routes, play-action |
| Two-high, light box | Run the ball; the numbers favor you |
| Disguise-heavy defense | Tempo to freeze disguise, motion to reveal man vs zone |
| QB with poor footwork under pressure | Interior pressure, contain rush, simulated pressure to confuse |
| QB locks onto first read | Robber/lurk defender in the throwing lane, pattern-match |
| Offensive tell (formation/alignment) | Specific defensive check called from the tell |
| Special-teams slow operation time | Punt-block or FG-block pressure from the weak side |
| Fatigue drop-off in Q4 | Tempo late, deep shots in Q4, rotate our DL to stay fresh |

Output: **advantages, disadvantages, keys to victory, and how to attack**
grouped by position group and by player, plus a "how they will attack *us*"
section built from our self-scout.

### 6.7 Special teams, officials, weather

- ST: hang time / operation charts; return lanes; coverage lane gaps; fake indicators
- Officials: crew penalty profile ("this crew calls 1.8× more holding than average", "tight on DPI") feeds coaching points on press technique and OL hands
- Weather: wind direction by quarter → which direction to take, kicking range adjustments, ball security emphasis in rain

---

## 7. Outputs and deliverables

1. **Scouting report (auto-built, editable)**: executive summary, personnel, tendencies, tells, situational breakdown, player cards, ST, keys to victory. Export to PDF and print.
2. **Attack plan**: advantages, disadvantages, mismatch board, how to attack each position group.
3. **Call-sheet assistant**: our plays ranked by situation against the expected opponent look (e.g. "vs their 3rd & medium Cover 1 pressure: Mesh, Slant-Flat, RB screen").
4. **Scout-team cards**: auto-drawn diagrams of the opponent's most frequent plays per situation, sequenced into a practice script.
5. **Cut-up playlists**: one click, e.g. "all 3rd & long vs Trips", "every rep of #24", "every red-zone pass".
6. **Player packets**: on phones; 5-minute matchup video and 3 coaching points per player; quiz to confirm they watched (with view tracking).
7. **One-page game-day keys sheet** for the head coach.
8. **Live game tracker** (press box): tendencies update by quarter, with a halftime report: "They have used 12 personnel 40% more than scouted, mostly on early downs."
9. **Post-game accuracy review**: predictions vs reality, surprises, what to add to the model.

---

## 8. Recommended improvements to the scouting process

These are changes we recommend to the way most staffs scout today, and the product builds each one in.

1. **One shared tagging dictionary.** Most staffs disagree on what "Trips" or "Cover 3" means across coaches. Lock definitions (with diagrams) so data is consistent week to week and season to season.
2. **Always show the sample size.** "80% run" on 5 plays is noise. Show *n*, a confidence level, and stop showing anything below n = 5.
3. **Use a three-game rule for tells.** A tell only counts if it shows up in at least 3 games. That kills false tells from one odd game.
4. **Self-scout every week.** Your next opponent is running the same report on you. Find and break your own tendencies first with "tendency breaker" plays.
5. **Weight recent games and the right opponents.** Tendencies against teams that look like you matter more than tendencies against the triple-option team they played in week 2.
6. **Scout the coordinator, not just the team.** A new OC or DC brings their old system. Pull their prior-school data in week 1.
7. **Remove garbage time.** Plays in blowouts distort tendencies.
8. **Track the accuracy of your scouting.** After each game, grade the report itself: what did we predict, what happened? Staffs that measure this get better quickly.
9. **Standardize intangibles.** "Confidence" and "toughness" are useful but subjective. Use a defined rubric (§15.2) with observable behaviors, so two coaches grade the same player the same way.
10. **Put evidence behind every claim.** Every bullet in the report links to the clips that prove it. Coaches and players trust what they can see.
11. **Push less, but personalized, film to players.** A 5-minute cut-up of *their* matchup beats a 2-hour full game no one watches. Track that they watched it.
12. **Script the opponent's opening plays.** Openers are scripted and repeatable across games; prepare for their top 15.
13. **Plan decisions before the game.** Build the 4th-down, 2-point and timeout charts on Thursday, adjusted for this opponent and the weather, not on the sideline.
14. **Watch the officiating crew.** Penalty tendencies change how aggressively you press, hold, and rush.
15. **Use fatigue and depth.** Find two-way players, thin position groups and Q4 drop-offs; plan tempo and rotation around them.
16. **Track injuries ethically.** Use public reports and observed, on-field indicators only; label anything unconfirmed as such.
17. **Run a halftime data check.** 10 minutes of first-half tendency data beats memory and gut feel at halftime.
18. **Keep institutional memory.** Store every season's data, so when you meet a team again (or a coach changes jobs) the work isn't lost.
19. **Separate "what they do" from "what we do about it."** Tendencies are facts; the plan is a decision. The product keeps them apart, so the staff debates the decision, not the data.
20. **Measure staff time.** Track hours saved per week; reinvest them in teaching.

---

## 9. Product experience

### 9.1 Core screens

| Screen | Purpose |
|---|---|
| **Opponent home** | Record, schedule, key players, injuries, data coverage (how many games and plays tagged), report status |
| **Film room** | Video player with tagging panel, keyboard shortcuts, dictation, AI suggestions to accept/reject, playlist builder |
| **Tendencies** | Filter bar (down, distance, zone, hash, quarter, score, personnel, formation) driving every chart |
| **Tells** | Ranked list of indicators with strength, sample and clips |
| **Predictor** | Situation picker → probability distribution, confidence and similar-play clips |
| **Situations** | 3rd down, red zone, 2-minute, 4th down, openers, sudden change dashboards |
| **Personnel** | Opponent roster cards with grades, experience, injuries, position fit, vulnerability score |
| **Matchups** | Mismatch board: our players vs theirs |
| **Attack plan** | Advantages, disadvantages, keys to victory, how to attack each group |
| **Intel** | Text, articles, transcripts, notes, auto-linked to players |
| **Report builder** | Drag sections, edit narrative, export PDF/print, push to players |
| **Self-scout** | Same engines run on our own data |

### 9.2 Design principles

- **Speed of tagging matters most.** Keyboard-first tagging with hotkeys, carry-forward of situation fields, AI pre-fill. Target: < 8 seconds per play for manual QC.
- **Plain language.** "They run 78% to the field from Trips" instead of statistical jargon.
- **Evidence one click away.** Every number opens the clips behind it.
- **Works offline.** Stadiums and buses have bad connectivity; reports and film cache locally.
- **Tablet and phone first for players, desktop for analysts.**
- **Print-friendly.** Many coaches still want paper on the sideline.

---

## 10. Technology architecture

```
 Ingest                 Processing                    Intelligence             Delivery
 ───────                ──────────                    ────────────             ────────
 Video upload  ──┐      Snap detection / clipping     Tendency engine          Web app (staff)
 Film exchange ──┤      Scoreboard OCR                Tell detection           Tablet (sideline*)
 Audio / ASR   ──┼──▶   Field registration       ──▶  Next-call predictor ──▶  Mobile (players)
 Text / web    ──┤      Detection + tracking          Matchup engine           PDF / print
 Stats / CSV   ──┘      Pose estimation               Attack-plan rules        Exports (CSV/XML)
                        Speech-to-text, NLP           LLM narrative writer
                        Coach QC queue                Calibration monitor
                                 ▲                                          * where rules allow
                                 └─────── coach corrections retrain models
```

- **Storage:** object storage for video (tiered: hot for current opponent, cold archive), relational database for plays/players/tags, search index for notes and transcripts.
- **Computer vision:** player detection and tracking, jersey OCR, pose estimation, field homography, running on GPU workers; batch overnight after film upload.
- **Speech and language:** speech-to-text for dictation and transcripts; a large language model (LLM) for summarizing articles/transcripts and drafting report narrative, always grounded in the tagged data and citing the plays it uses. The LLM never invents statistics; numbers come only from the analytics engine.
- **Analytics:** Python services (pandas, scikit-learn/gradient boosting, Bayesian smoothing) exposing a REST/GraphQL API.
- **Apps:** a web app (React or similar), installable as an offline-capable PWA; a native tablet/phone app later.
- **Integrations:** film exchange platforms (via exports/partner APIs where available), wearable/GPS vendors, stats sites, calendar, and SSO (Google/Microsoft for schools).
- **Security:** per-program tenants, role-based access (head coach, coordinator, position coach, analyst, player, trainer), encryption at rest and in transit, audit logs, SOC 2 roadmap for college customers.

The included prototype (`/scout/index.html`) demonstrates the tendency
engine, tell detection, predictor, matchup board, attack-plan generator,
film tagging with video and dictation, the intel board, and the printable
report, all in the browser with sample data.

---

## 11. Compliance, ethics, and trust

- **Scouting rules.** NCAA rules prohibit in-person scouting of future opponents in the same season and prohibit using electronic equipment to record an opponent's signals. State high school associations and other leagues set their own rules. Rules on sideline tablets, in-game video and coach-to-player communication have changed almost every year recently. The product ships with a **compliance mode per level/association** that disables features (e.g. in-game video, sideline tablet video) not permitted for that customer. **Every customer's compliance office or association should confirm the configuration.**
- **No signal stealing, no practice surveillance.** The product refuses to ingest content labeled as opponent practice footage or sideline signal capture, and the terms of service forbid it.
- **Minors' data.** Most high school players are minors. Opponent player data is limited to on-field performance and public roster information, kept private to the subscribing staff, never sold or published, and deleted on request. Own-team data is governed by FERPA (US schools), COPPA where under-13 users exist, and state student-privacy laws.
- **Health information.** Opponent "injury" data is limited to public reports and on-field observations, labeled *unconfirmed*. Own-team medical data is restricted to the trainer role and stays out of the general analytics.
- **Copyright.** Broadcast footage use is the customer's responsibility under their licenses; the product supports, but does not redistribute, it.
- **Human in charge.** The product recommends; coaches decide. Recommendations show confidence and evidence so coaches can overrule them.
- **Respectful language.** "Confidence" and "composure" ratings describe on-field behavior, never character. Ratings are internal coaching tools.

Get a legal review of these policies (sports compliance plus student privacy counsel) before launch.

---

## 12. Roadmap

| Phase | Timeline | Scope | Outcome |
|---|---|---|---|
| **0. Prototype** | Done (this repo) | Browser prototype with sample data | Demo for coach interviews and pilots |
| **1. MVP** | Months 0–4 | Accounts, teams, film upload and play clipping, fast manual tagging, CSV/film-exchange import, tendency engine, tells, predictor, player cards, matchup board, attack plan, report PDF, player packets | 10–20 paid pilot programs |
| **2. AI assist** | Months 4–9 | Scoreboard OCR, auto formation/personnel suggestions, dictation, transcript summarization, LLM report narrative, self-scout, scout cards, calibration reports | Tagging time cut by 50%+ |
| **3. Vision** | Months 9–18 | Tracking, jersey ID, pose-based footwork/technique metrics, speed/effort metrics, coverage recognition | Measurable technique data no competitor at this price offers |
| **4. Live and network** | 18 months+ | Press-box live tracker, halftime reports, league-wide priors (opt-in, anonymized), recruiting add-on | Platform lock-in, data network effects |

---

## 13. Success metrics

- **Staff time saved** per opponent (target: 10+ hours/week at HS, 25+ at college)
- **Tagging speed** (seconds/play) and **AI tag acceptance rate**
- **Predictor calibration** (Brier score) and **top-1 hit rate** vs a naive baseline
- **Report usage**: opens, player-packet completion rate
- **Retention**: season-over-season renewal (target > 85%)
- **Net promoter score** from coaches
- Wins are an outcome, not a metric we claim. Too many factors go into a win to promise them.

---

## 14. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Film quality at HS level is poor (shaky sideline, no end zone) | Manual-first workflow; CV runs only where quality allows; quality score per film |
| Coaches don't trust "black box" predictions | Explainable method, sample sizes, calibration reports, clips behind every number |
| Tagging burden | AI pre-fill, carry-forward, hotkeys, optional outsourced tagging service |
| Incumbent film platforms add similar features | Focus on synthesis and game planning (the "so what"), integrate with them rather than compete on film hosting |
| Rule changes | Compliance mode per level, updated each season |
| Data privacy incident | Least-privilege access, encryption, audits, minimal data on minors |
| Small samples early in season | Bayesian priors from coordinator history and level-wide data |

---

## 15. Appendices

### 15.1 Distance and zone buckets (default, configurable)

- Distance: Short 1–2, Medium 3–6, Long 7–10, Very long 11+
- Field zones by yards to goal: Backed up 90–99, Own territory 51–89, Midfield 40–50, Plus territory 21–39, Red zone 11–20, High red 4–10, Goal line 1–3

### 15.2 Confidence & composure rubric (1–5)

| Score | Observable behaviors |
|---|---|
| 5 | Plays fast, no pre-snap hesitation; responds to a bad play with a good one; communicates and directs teammates |
| 4 | Mostly decisive; occasional hesitation in new looks |
| 3 | Neutral; inconsistent; effort and decisiveness vary with the score |
| 2 | Visible hesitation pre-snap; looks to the sideline often; body language drops after mistakes; mistakes cluster |
| 1 | Repeatedly plays tentatively; avoids contact or competition; mistakes cascade; penalties after frustration |

### 15.3 Footwork rubric (1–5), examples by position

- **OL:** stance balance, first-step length/direction, kick-slide depth, base width under bull rush, recovery footwork
- **DL:** get-off time, first-step gain, hand/foot coordination, rush-plan variety
- **CB/S:** backpedal without false step, hip flip timing, plant and drive, transition speed
- **LB:** first step read (downhill vs false step), shuffle vs crossover, depth in drops
- **QB:** drop timing, base under pressure, resetting feet to throw, climb vs bail
- **WR:** release footwork vs press, route stem tempo, breaking efficiency

### 15.4 Vulnerability score (prototype formula)

```
vulnerability = 100 × weighted average of
   (5 − technique)/4        × 0.20
   (5 − footwork)/4         × 0.15
   (5 − confidence)/4       × 0.15
   inexperience             × 0.15   (FR=1, SO=0.66, JR=0.33, SR=0)
   bust / missed-tackle rate× 0.10
   injury flag              × 0.15   (Out=1, Limited=0.8, Questionable=0.5, Healthy=0)
   out of natural position  × 0.10
```
Weights are configurable per staff; calibrate them against actual matchup results over a season.
