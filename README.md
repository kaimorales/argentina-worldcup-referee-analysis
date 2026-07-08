# Does Argentina Get Favorable Treatment From World Cup Referees?

A small, reproducible data project testing a popular claim: that Argentina is favored
by referees — especially on penalty kicks — at the FIFA World Cup. Focus: **2022 (Qatar,
complete)** and **2026 (ongoing, provisional data)**.

## Design

**Subject:** Argentina in 2022 + 2026. **Control:** the rest of World Cup history.
The question is how extreme Argentina's penalty haul is against that historical baseline.

## TL;DR

- **⭐ The headline — a structural break in 2022 (this is the novel finding):** under the
  *same VAR rules*, Argentina went from the **19th-most-penalized team in 2018** (1 penalty in
  4 games, dead-average, p = 0.60) to **1st in 2022** (5 in 7 games, 4× the field, p = 0.009).
  Measuring them *relative to the field* cancels the VAR era-effect — so this isn't "everyone
  got more penalties," it's Argentina-specific, and it *switched on in 2022.* They reached the
  2014 final (7 games) with ~0 open-play penalties. "They always got these calls" is false.
- **⭐ The anomaly is World-Cup-specific (the key nuance):** widening to *all* competitive
  matches 2022→present, Argentina drew **4.0× the field at the 2022 World Cup (#1 of 32)** but
  a **dead-average 1.1× at Copa América 2024** (1 penalty in 6 games — and they *won* it), then
  ~2× again at the 2026 World Cup. "Rigged in every match" is false; "outlier specifically at
  the FIFA World Cup" is real. Including the Copa result is what makes the claim credible.
- **All-time record:** Argentina's **5 penalties in 2022 is the most ever awarded to a
  single team in one World Cup** — no team in ~90 years had exceeded 4 (Netherlands 1978,
  Portugal 1966). That's the 100th percentile of the whole historical distribution.
- **Within 2022:** those 5 were **21.7% of the 23 penalties in the entire tournament** —
  to one of 32 teams.
- **Rate test vs the VAR-era baseline (0.20 penalties/team/match):**
  - 2022 → 3.5× expected, **p = 0.015** (significant)
  - 2026 (provisional) → 2.0× expected, p = 0.27 (not significant; only 5 games)
  - **2022 + 2026 pooled → 2.9× expected, p = 0.013** (significant)
- **Full 32-team model (real StatsBomb event data):** modelling penalties as proportional to
  attacking volume across all 32 teams, **Argentina is the single biggest outlier** — largest
  shots-adjusted residual (+2.78 SD), rank 1/32, **5.2 penalties per 100 shots vs a 1.6 field
  average**, and the *only* team significant at raw p = 0.021.
- **It's not just "they attack more":** France — the other finalist, same 7 games — took
  **more shots (100 vs 96)** for **higher xG (10.25 vs 10.02)** yet got **2.5× fewer penalties.**
  Chance quality was identical (xG/shot 0.10 both), so volume can't explain the gap.
- **Honest statistics:** after correcting for testing 32 teams (Bonferroni/BH), Argentina's
  p rises to 0.66 — *not* significant. Five penalty events can't carry a harsh correction alone.
  The case rests on **convergence**: biggest residual + France control + all-time record.
- **The 2026 twist:** Argentina were awarded ≥2 penalties again — but **Messi missed both**,
  the first player ever to miss two in a single World Cup. "Gets the calls" ≠ "always benefits."
- **Counter-evidence / nuance (2022):** the same refs booked them **16 times in 7 games**,
  put them in the most-carded match in World Cup history, and they were *not* even the most
  shot-happy team. Favored on **penalties specifically** — not "teacher's pet" across the board.

This repo is built to be **credible under scrutiny**, not to win an argument. The
counter-evidence is reported alongside the headline, because on LinkedIn the comment
section will find it anyway. **Significance is not intent** — an outlier this size can also
come from a possession-heavy side that lives in the opponent's box.

## Reproduce

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python src/analyze.py                # 2022 single-tournament deep-dive
python src/baseline_comparison.py    # Argentina (2022+2026) vs World Cup history
python src/exposure_and_scorecard.py # France exposure comparison + scorecard + placebo
python src/fullfield_regression.py   # all 32 teams, StatsBomb data, exposure regression
python src/structural_break.py       # 2018 vs 2022 structural break (proves it started in 2022)
python src/conspiracy_window.py      # ⭐ 2022→present competitive record (WC vs Copa América)
```

The StatsBomb dataset (`data/statsbomb_team_stats_2022.csv`) is already built and committed.
To rebuild it from source, see the downloader note in `data/SOURCES.md`.

Outputs regenerate the `reports/*.md` findings files and charts in `figures/`.

## Repo layout

| Path | What it is |
|------|-----------|
| `data/argentina_2022_matches.csv` | Argentina's 7 matches: penalties for/against, results |
| `data/tournament_baseline_2022.csv` | 2022 tournament totals used as the single-tournament baseline |
| `data/tournament_penalty_totals.csv` | Per-tournament penalty totals (VAR-era control group) |
| `data/team_tournament_penalty_records.csv` | All-time "most penalties to one team" record holders |
| `data/argentina_subject.csv` | Argentina 2022 + 2026 penalty counts (the subject) |
| `data/argentina_2026_incidents_provisional.csv` | Best-effort 2026 refereeing incidents (provisional) |
| `data/team_exposure_2022.csv` | Argentina vs France: shots, xG, penalties (exposure control) |
| `data/argentina_scorecard_2022.csv` | Multi-metric refereeing scorecard inputs |
| `data/statsbomb_team_stats_2022.csv` | **All 32 teams** from StatsBomb events (shots, xG, pens, fouls, cards) |
| `data/statsbomb_team_stats_2018.csv` | All 32 teams, 2018 World Cup (for the structural-break test) |
| `data/argentina_penalty_history.csv` | Argentina's per-tournament penalty timeline (2010–2026) |
| `data/statsbomb_team_stats_copa2024.csv` | Copa América 2024, all teams (competitive control for 2022+) |
| `data/argentina_competitive_2022plus.csv` | Argentina's competitive record since 2022 (WC + Copa) |
| `data/SOURCES.md` | Every figure's provenance and confidence level |
| `src/analyze.py` | 2022 single-tournament Poisson test → `FINDINGS.md` + figures |
| `src/baseline_comparison.py` | Argentina (2022+2026) vs World Cup history → `BASELINE_FINDINGS.md` + figures |
| `src/exposure_and_scorecard.py` | France exposure comparison + scorecard + placebo → `EXPOSURE_FINDINGS.md` + figures |
| `src/fullfield_regression.py` | 32-team StatsBomb exposure regression + multiple-comparison correction → `FULLFIELD_FINDINGS.md` + figures |
| `src/structural_break.py` | 2018-vs-2022 field-relative structural break → `STRUCTURAL_BREAK_FINDINGS.md` + figure |
| `src/conspiracy_window.py` | ⭐ 2022→present competitive record, WC vs Copa América → `CONSPIRACY_WINDOW_FINDINGS.md` + figure |
| `reports/*_FINDINGS.md` | Auto-generated results |
| `reports/METHODOLOGY.md` | How the tests work and their limits |
| `reports/linkedin_post.md` | Drafted posts, ready to adapt |

## A note on honesty

The point of the project was to test a claim, not to launder a conclusion. The 2022
penalty finding is real and holds up. The framing throughout is deliberately careful:
an outlier is evidence worth discussing, not proof of intent. See
[`reports/METHODOLOGY.md`](reports/METHODOLOGY.md) for the caveats.

**2026 data is provisional** — collected from live reporting while the tournament is
ongoing and should be re-verified before publication.
