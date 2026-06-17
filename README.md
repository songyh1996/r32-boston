# 🏟️ Road to Boston — World Cup 2026 Round of 32

An interactive, in-browser **Monte Carlo simulation** that ranks which national teams are
most likely to play in the **FIFA World Cup 2026 Round-of-32 match in Boston**
(Gillette Stadium, Foxborough — **Match 74, Mon June 29, 2026, 4:30 PM ET**).

> **The Boston match has two tickets.** One always goes to the **winner of Group E**
> (Germany, Ecuador, Ivory Coast or Curaçao). The other goes to one of the **best
> third‑placed teams**, which the official bracket draws from **Groups A, B, C, D or F**.
> The app simulates the whole 48‑team group stage thousands of times and counts how
> often each country lands in that match — then ranks them by probability.

## ▶️ View it

The page is a single, self‑contained `index.html` (no build step, no dependencies).

- **GitHub Pages:** https://songyh1996.github.io/r32-boston/ *(published by the
  [Deploy to GitHub Pages](.github/workflows/deploy-pages.yml) workflow)*
- **Instant preview (public repos):**
  https://raw.githack.com/songyh1996/r32-boston/claude/cool-johnson-yk9hf4/index.html
- **Locally:** clone the repo and open `index.html` in any browser, or run
  `python3 -m http.server` and visit `http://localhost:8000`.

## ✨ What you can do

- See a **live leaderboard** ranking every contender by its chance to appear in Boston,
  split by route: **win Group E** (teal) vs **wildcard 3rd place** (purple).
- Adjust the **number of simulations** (2k–60k) and re‑run.
- **Edit any team's rating** (Group E race panel, or the full 48‑team editor) to reflect
  results as the tournament unfolds, then re‑run to watch the ranking shift.
- See **which group** Boston's wildcard third‑placed team comes from most often.

## 🧮 Methodology

It is a forward Monte Carlo simulation, run entirely in your browser:

1. **Match model.** Each team has a strength rating (default ≈ FIFA World Ranking points,
   June 2026). A match's rating gap sets an expected goal supremacy, and each side's goals
   are drawn from a **Poisson** distribution — so scorelines and goal difference are realistic.
2. **Group stage.** All 12 groups are played out; teams are ranked by
   points → goal difference → goals scored (head‑to‑head/fair‑play tiebreakers are simplified).
3. **Round of 32.** 32 teams advance: 12 winners + 12 runners‑up + the **8 best third‑placed**
   teams. Thirds are matched to winner slots respecting FIFA's official eligibility sets
   (Boston's *Winner Group E* slot can only meet a third from **A/B/C/D/F**). When more than
   one valid assignment exists the choice is randomised, so no group is artificially favoured.
4. **Tally.** Over all runs, count how often each country is one of the two teams in
   **Match 74**, and report the probability.

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
randomised matching. The defaults are pre‑tournament strength; nudge ratings to reflect
real results and re‑run.

## 📚 Data sources

- FIFA World Cup 2026 group draw & Round‑of‑32 format (FIFA / ESPN / NBC Sports / Sky Sports).
- Boston (Gillette Stadium) hosts **Match 74** of the Round of 32 on June 29, 2026 (Gillette Stadium / CBS Boston / NESN).
- Team strengths ≈ FIFA World Ranking points, June 2026 (FIFA / ESPN).

*Built as an interactive World Cup explainer. The simulation runs client‑side; no data leaves your browser.*
