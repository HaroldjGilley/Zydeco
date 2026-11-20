# Zydeco Scout — Business & Go-to-Market Plan

Companion to `PRODUCT_SPEC.md`. Prices and figures below are **starting
assumptions to test in coach interviews and pilots**, not market research
results.

## 1. Positioning

> **Zydeco Scout turns opponent film, audio and notes into a game plan:
> what they'll do, who to attack, and how, with the evidence to prove it.**

Film platforms store and share video. Stats products count things. Zydeco
Scout answers the question every staff asks on Sunday: **"How do we beat this
team on Saturday?"** It works *with* the film platform a program already
uses and doesn't replace it.

### Differentiators
1. **Prediction with honest confidence**: next-call probabilities with sample sizes and published calibration.
2. **The player layer**: experience, footwork, engagements, confidence, injuries and position fit turned into a vulnerability score and a mismatch board.
3. **Attack plan, not just charts**: concrete "how to attack" recommendations with clips as evidence.
4. **Built for the staff that has no analysts**: AI pre-tagging, fast QC, one-click reports.
5. **Compliance mode by level**, so ADs and compliance offices can say yes.

## 2. Competitive landscape (verify current offerings before pitching)

| Category | Examples | Our angle |
|---|---|---|
| Film exchange / video | Hudl, XOS Digital, DVSport | Integrate via exports; we do synthesis, not hosting |
| Stats / grading services | PFF (college/pro), regional stat services | We serve levels they don't cover, and coach-defined grading |
| Wearables / performance | Catapult, STATSports | Import load data for fatigue context |
| Spreadsheets and paper | Every staff | Our main real competitor: we must be faster than Excel |

## 3. Pricing (hypothesis)

| Plan | For | Price (annual) | Includes |
|---|---|---|---|
| **Sideline** | Youth, small HS | $499 | Manual tagging, tendencies, predictor, report PDF, 1 opponent at a time, 5 staff seats |
| **Varsity** | High school | $1,495 | Everything in Sideline + tells, player cards, matchups, attack plan, player packets (100 players), self-scout, 15 staff seats |
| **Varsity Pro** | Large HS, small college | $3,500 | + AI pre-tagging, dictation, transcript summarization, scout cards, calibration reports, unlimited seats |
| **Collegiate** | NAIA, D-II, D-III, JUCO, FCS | $9,000–$25,000 | + computer-vision metrics, coordinator history import, API/exports, SSO, priority support |
| **Enterprise** | FBS / pro-adjacent | Custom ($40k+) | + custom models, on-site onboarding, data warehouse access, security review |

**Add-ons:** outsourced tagging service ($150–$300/opponent, delivered by
Sunday noon), extra video storage, in-person clinic/onboarding, district or
conference licenses (volume discount 15–30%).

**Free tier:** one opponent per season with limited reports, to seed word of
mouth among assistants who later become head coaches.

## 4. Market sizing (order of magnitude, to refine)

- ~14,000+ US high schools field 11-player football, plus ~750+ college programs across divisions and JUCO.
- Example: 3% HS penetration × $1,495 average ≈ 420 schools ≈ $630k ARR; 10% of college programs at $12k ≈ 75 programs ≈ $900k ARR. Add tagging services and add-ons.
- Expansion: girls' flag football (fast-growing), 7-on-7, international (Europe/Japan/Mexico), and other sports with play-by-play structure (lacrosse, basketball sets).

## 5. Go-to-market

1. **Founder-led pilots (pre-season):** 10–20 programs in one region, free or discounted for a full season in exchange for weekly feedback and a testimonial. Track hours saved and prediction accuracy for case studies.
2. **Coaching clinics and associations:** booth plus a 45-minute session at state coaching association clinics: *"Build a game plan in 60 minutes with your opponent's last three games."* Live demo on real (permitted) film.
3. **Ambassador coaches:** respected coordinators get free seats and referral credit.
4. **Content marketing:** weekly "tendency of the week" breakdowns of public college/pro games, short-form video, and a coaches' newsletter.
5. **Conference/district deals:** once 2–3 teams in a conference adopt, sell the rest.
6. **Booster-funded purchase kit:** a one-page ROI sheet and a donation-ask template, since boosters fund many HS purchases.
7. **Season timing:** sell February–July (budgets set, pre-season planning). Onboard in July/August. Renewals in December/January.

## 6. The demo that sells it (15 minutes)

1. Load an opponent's 3 games (pre-tagged in the demo).
2. Tendencies: "3rd & medium: 74% pass, Mesh is their favorite, #2 gets 41% of targets."
3. Tells: "Pistol with the back offset is 89% run to that side, and it holds in all 3 games."
4. Predictor: pick a live situation and show the probability bars plus similar-play clips.
5. Personnel: "Their left corner is a sophomore, playing out of position, false-steps on stems." Mismatch board puts our best WR on him.
6. Attack plan: auto-generated, with the clips behind it.
7. Print the report. "That took 15 minutes. How long did it take your staff last week?"

## 7. Operations and team

- **Founding team:** product/football lead (coaching network), full-stack engineer, ML/computer-vision engineer, and a part-time tagging lead (former QC/analyst).
- **Tagging service:** trained part-time analysts (former players, sports management students) working on a QA'd workflow; also produces training data for AI tagging.
- **Support:** in-season response within 2 hours Sunday–Thursday; game week matters.

## 8. 12-month milestones

| Month | Milestone |
|---|---|
| 0–1 | 25 coach interviews; validate pricing and top 5 features; finalize tag dictionary with 3 advisor coaches |
| 1–4 | Build MVP; recruit 15 pilot programs |
| 4–7 | Pilot season; weekly feedback; measure hours saved and calibration |
| 7–8 | Case studies; clinic circuit; launch paid plans |
| 8–12 | 100 paying programs target; AI-assist release; first conference deal |

## 9. Key risks

- **Adoption friction:** coaches are busy in season → onboard before the season, offer the tagging service.
- **Data quality:** bad film = bad tags → quality scoring, human QC.
- **Incumbents:** a film platform could add analytics → move fast on the player layer and attack plan, integrate deeply, build coach loyalty through clinics.
- **Compliance changes:** maintain the rules matrix by level each off-season.

## 10. Next steps for you

1. Run a trademark/domain search on the product name.
2. Show the prototype (`scout/index.html`) to 5–10 coaches you know; collect what they would pay and which screens they would actually use.
3. Recruit 2–3 advisor coaches (one offense, one defense, one HS head coach) to lock the tagging dictionary.
4. Decide build vs partner for film hosting (recommend: integrate, don't host).
5. Get a sports-compliance and student-privacy legal review of §11 of the spec.
