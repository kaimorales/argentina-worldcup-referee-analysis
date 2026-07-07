# LinkedIn Post Draft

Three versions at different heat levels. All are defensible — none require hiding data.
Pick one, drop in a chart from `figures/`, and edit the voice to sound like you.

---

## Version A — the punchy one (recommended)

Everyone jokes that Argentina gets "help" from referees at the World Cup.

So I actually ran the numbers. 📊

At the 2022 World Cup, **23 penalties were awarded across the whole tournament.
Argentina got 5 of them.**

That's **21.7% of every penalty — awarded to 1 of 32 teams.**

"But they played 7 games, they reached the final." Fair. So I adjusted for it. At the
tournament's average penalty rate, a 7-game team should expect ~1.3 penalties. Argentina
got 5 — about **4× expectation.** A Poisson test lands at **p ≈ 0.009.** Statistically,
that's a genuine outlier, not a vibe.

Now the part most "FIFA loves Argentina" posts leave out:

The same referees showed Argentina **16 yellow cards in 7 games** and put them in the
most-carded match in World Cup history. They conceded 2 penalties in the final. A team
that's being *protected* doesn't lead the tournament in bookings.

So what's the honest takeaway? The penalty count is a **real statistical anomaly worth
talking about** — but "anomaly" isn't the same as "conspiracy." Elite attacking teams
that live in the opponent's box draw penalties. The data flags something; it doesn't
prove intent.

That nuance is the whole point. Outlier: yes. Smoking gun: not from this alone.

Repo + reproducible code in the comments. What's your read? 👇

#DataScience #WorldCup #SportsAnalytics #Statistics #Football

---

## Version B — the analyst's framing (most credible, least clickbait)

A short lesson in why "significant" and "proven" aren't the same word — using the
Argentina refereeing conspiracy as the example.

The claim: World Cup referees favor Argentina.
The most-cited evidence: they were awarded **5 of 23 penalties** at Qatar 2022 (21.7%).

I tested it properly:
• Baseline penalty rate: 0.18 per team per match
• Argentina's expected haul over 7 games: ~1.3
• Actual: 5 → ~4× expected, Poisson p ≈ 0.009 ✅ significant

Case closed? No — and here's the discipline that separates analysis from a hot take:

1️⃣ **Selection bias.** I picked the team *because* it looked extreme. With 32 teams,
someone tops the table by luck. That inflates significance.
2️⃣ **Confounding.** Penalties are earned. Possession-dominant teams draw box fouls.
3️⃣ **Counter-evidence.** 16 yellow cards in 7 games; 2 penalties conceded. Not
"protected."

The result I'll actually defend: Argentina's penalty count was a **real outlier** —
and that's genuinely interesting — but a single-team, small-sample test can't prove
favoritism. Anyone selling you certainty here is selling.

Full methodology + code: [repo link]

#Statistics #DataScience #SportsAnalytics #CriticalThinking

---

## Version C — the one-liner hook (for the top of the post)

> Argentina won 21.7% of ALL the penalties at the 2022 World Cup — 5 of 23, as 1 of 32
> teams. I ran the stats on whether that's suspicious or just what winning looks like. 🧵

---

### Notes before you post
- Swap `[repo link]` for the GitHub URL once it's live.
- Attach `figures/penalty_share.png` or `figures/observed_vs_expected.png`.
- If you cite the 2026 examples, label them clearly as *ongoing / provisional* — the
  tournament isn't finished and the numbers aren't final.
- Re-verify the raw counts against `data/SOURCES.md` before publishing. Your credibility
  is the product.
