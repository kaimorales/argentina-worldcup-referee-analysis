# Does Argentina Get Favorable Treatment From World Cup Referees?

A small, reproducible data project testing a popular claim: that Argentina is favored
by referees — especially on penalty kicks — at the FIFA World Cup. Focus: **2022 (Qatar,
complete)** and **2026 (ongoing, provisional data)**.

## TL;DR

- In 2022, Argentina were awarded **5 of the 23 open-play penalties in the entire
  tournament — 21.7%, to one of 32 teams.**
- Adjusting for the fact that they played 7 games (reached the final), that's about
  **4× the penalties expected** at the tournament-average rate.
- A Poisson test puts this at **p ≈ 0.009** — a genuine statistical outlier, not a vibe.
- **But** the same refs booked them **16 times in 7 games** and put them in the most-carded
  match in World Cup history. They were *not* protected across the board. The honest
  story is "penalty outlier," not "teacher's pet."

This repo is built to be **credible under scrutiny**, not to win an argument. The
counter-evidence is reported alongside the headline, because on LinkedIn the comment
section will find it anyway.

## Reproduce

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python src/analyze.py
```

Outputs regenerate `reports/FINDINGS.md` and three charts in `figures/`.

## Repo layout

| Path | What it is |
|------|-----------|
| `data/argentina_2022_matches.csv` | Argentina's 7 matches: penalties for/against, results |
| `data/tournament_baseline_2022.csv` | Tournament totals used as the statistical baseline |
| `data/argentina_2026_incidents_provisional.csv` | Best-effort 2026 refereeing incidents (provisional) |
| `data/SOURCES.md` | Every figure's provenance and confidence level |
| `src/analyze.py` | Loads data, runs the Poisson test, writes findings + figures |
| `reports/FINDINGS.md` | Auto-generated results |
| `reports/METHODOLOGY.md` | How the test works and its limits |
| `reports/linkedin_post.md` | Drafted post, ready to adapt |

## A note on honesty

The point of the project was to test a claim, not to launder a conclusion. The 2022
penalty finding is real and holds up. The framing throughout is deliberately careful:
an outlier is evidence worth discussing, not proof of intent. See
[`reports/METHODOLOGY.md`](reports/METHODOLOGY.md) for the caveats.

**2026 data is provisional** — collected from live reporting while the tournament is
ongoing and should be re-verified before publication.
