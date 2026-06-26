# 🇰🇷 Korea's Road to R32 — World Cup 2026

An interactive, in-browser **Monte Carlo simulation** of the **FIFA World Cup 2026**
group stage and Round-of-32 bracket. The headline view is **South Korea's live odds to
reach the Round of 32**; two more tabs cover any team's likely R32 opponent and the
**Boston** Round-of-32 match (Gillette Stadium — Match 74). Updated with live results.

> **The Boston match has two tickets.** One always goes to the **winner of Group E**
> (Germany, Ecuador, Ivory Coast or Curaçao). The other goes to one of the **best
> third‑placed teams**, which the official bracket draws from **Groups A, B, C, D or F**.
> The app simulates the whole 48‑team group stage thousands of times and counts how
> often each country lands in that match — then ranks them by probability.

### Two modes (tabs)

1. **🏟️ Boston Round of 32** — the A‑vs‑B matchup for Match 74: the two seat races
   (Group E winner vs wildcard 3rd) and the most likely exact ties.
2. **🧭 Any team's R32 opponent** — pick *any* of the 48 teams and see how it finishes
   its group, whether it reaches the Round of 32, and **who it would most likely play**
   (by scenario: win the group / runner‑up / sneak through 3rd), with the venue for each
   path. (Defaults to **South Korea**. Fun fact it surfaces: if Korea finishes 3rd it can
   actually end up *in the Boston match vs Germany*.)

## ▶️ View it

The page is a single, self‑contained `index.html` (no build step, no dependencies).

- **GitHub Pages:** https://songyh1996.github.io/r32-boston/ *(published by the
  [Deploy to GitHub Pages](.github/workflows/deploy-pages.yml) workflow)*
- **Instant preview (public repos):**
  https://raw.githack.com/songyh1996/r32-boston/claude/cool-johnson-yk9hf4/index.html
- **Locally:** clone the repo and open `index.html` in any browser, or run
  `python3 -m http.server` and visit `http://localhost:8000`.

## ✨ What you can do

- It's **one game = two seats**, shown as **A vs B**: a matchup card, then two
  separate ranked races — **Seat A** (who wins Group E) and **Seat B** (the wildcard
  3rd‑place team) — each summing to ~100%, plus the most likely **exact A‑vs‑B ties**.
- **Real group‑stage results are baked in.** Completed matches are locked to their
  actual scores (only remaining fixtures are simulated). Toggle them off to compare with
  the pre‑tournament forecast, or hit **↻ Refresh from live data** to pull the latest.
- Adjust the **number of simulations** (2k–60k), **edit any team's rating** (Seat A
  inline or the full 48‑team editor), and re‑run to watch the picture shift.
- See **which group** Boston's wildcard third‑placed team comes from most often.

## 🧮 Methodology

It is a forward Monte Carlo simulation, run entirely in your browser:

1. **Match model.** Each team has a strength rating (default ≈ FIFA World Ranking points,
   June 2026). A match's rating gap sets an expected goal supremacy, and each side's goals
   are drawn from a **Poisson** distribution — so scorelines and goal difference are realistic.
2. **Real results, then simulate the rest.** Completed group‑stage matches are **locked**
   to their actual scorelines (fetched from
   [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json)); only the
   not‑yet‑played fixtures are simulated.
   **Live, in‑play scores** are layered on top from ESPN's public scoreboard (no API key,
   fetched client‑side, auto‑refreshed every minute): a match in progress keeps its current
   score and only the *remaining* minutes are simulated, so every probability moves with the
   live action.
3. **Group stage.** All 12 groups are completed; teams are ranked by
   points → goal difference → goals scored (head‑to‑head/fair‑play tiebreakers are simplified).
4. **Round of 32.** 32 teams advance: 12 winners + 12 runners‑up + the **8 best third‑placed**
   teams. Thirds are matched to winner slots respecting FIFA's official eligibility sets
   (Boston's *Winner Group E* slot can only meet a third from **A/B/C/D/F**). When more than
   one valid assignment exists the choice is randomised, so no group is artificially favoured.
5. **Tally.** Over all runs, track each **seat** separately — who fills Seat A (Group E
   winner) and Seat B (wildcard 3rd) — plus how often each exact **A‑vs‑B** tie occurs.

### The real bracket (Round of 32, winner‑vs‑third slots)

| Match | Slot | Venue |
|------:|------|-------|
| **74** | **Winner Group E vs best 3rd (A/B/C/D/F)** | **Boston / Gillette Stadium** |
| 77 | Winner Group I vs best 3rd (C/D/F/G/H) | — |
| 79 | Winner Group A vs best 3rd (C/E/F/H/I) | — |
| 80 | Winner Group L vs best 3rd (E/H/I/J/K) | — |
| 81 | Winner Group D vs best 3rd (B/E/F/I/J) | — |
| 82 | Winner Group G vs best 3rd (A/E/H/I/J) | — |
| 85 | Winner Group B vs best 3rd (E/F/G/I/J) | — |
| 87 | Winner Group K vs best 3rd (D/E/I/J/L) | — |

### Group E (the only group whose teams can take Boston's "home" slot)

🇩🇪 Germany · 🇪🇨 Ecuador · 🇨🇮 Ivory Coast · 🇨🇼 Curaçao

## ⚠️ Caveats

This is an explainer for fun and insight — **not** a betting tool. Ratings are approximate,
and the exact 495‑row FIFA third‑place combination table is approximated by a valid,
randomised matching. Completed matches are locked to real scores; matches still to be
played use the pre‑tournament strength ratings (which you can nudge and re‑run).

## 📚 Data sources

- FIFA World Cup 2026 group draw & Round‑of‑32 format (FIFA / ESPN / NBC Sports / Sky Sports).
- Boston (Gillette Stadium) hosts **Match 74** of the Round of 32 on June 29, 2026 (Gillette Stadium / CBS Boston / NESN).
- Finished group‑stage results: [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json) (public‑domain).
- Live, in‑play scores: ESPN public soccer scoreboard API (`site.api.espn.com`, no key, fetched client‑side).
- Team strengths ≈ FIFA World Ranking points, June 2026 (FIFA / ESPN).

*Built as an interactive World Cup explainer. The simulation runs client‑side; no data leaves your browser.*
