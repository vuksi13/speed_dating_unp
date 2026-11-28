# Project progress 3: Speed Dating seminar

Last updated: 24 Nov 2026. Continues from `NAPREDAK_2.md` (20 Nov).
Work is on the git branch **`luka`**.

## How to continue in a new Claude session

Open Claude Code in this project folder and say:

> Read `NAPREDAK_3.md` and continue the way it describes. Next step: review chapter 9.

Since 27 Nov: review **all** chapters first and explain them afterwards. Edit only the chapter under review, and log every change with its reason in `IZMENE.md` (for the professor). If a fix moves numbers in a later chapter, note it in `IZMENE.md` and update it when that chapter is reviewed.

## How we work (keep this process)

1. **Review a chapter**: read the whole chapter and check every claim and number against the raw data. Look at the actual suspicious rows, not just counts and totals.
2. **Fix and shorten**: correct errors, keep the important parts, and prefer short prose over bullet lists.
3. **Verify**: knit the whole seminar on a temporary copy. Confirm the cleaned data and model results did not change unexpectedly, and update every number that moved.
4. **Report**: give a list of **what was checked and what was not**.
5. **Explain**: in the next answer, explain the chapter in segments (key terms, how they connect, why each decision is right, ready-made defence answers), with one question to check understanding.

Rules for explanations: plain English, simple concrete examples (Ana and Marko, strict and lenient professor), one question at a time, and define every term. Methods from outside the course need a one-sentence explanation for the defence.

You push to GitHub yourself, so Claude should only say when something is ready.

## Status

| Chapter | Status |
|---|---|
| 1 Uvod | Ages note added (three participants aged 18–19) |
| 2 Opis i priprema | Rewritten and shortened; column list moved to an appendix |
| 3 Čišćenje | Rewritten, reviewed and explained |
| 4 Nedostajuće vrednosti | Rewritten, reviewed and explained |
| 5 Ekstremne vrednosti | Rewritten, reviewed and explained |
| 6 Eksplorativna analiza | Rewritten and reviewed (27 Nov), including your follow-up fixes; explanation later |
| 7 Statistički testovi | Reviewed and shortened (27 Nov); per-person check added for H2; H5 (hypergamy) removed from the whole seminar; explanation later |
| 8 Nove promenljive | Reviewed and shortened by 40% (27 Nov); descriptive tables without code; explanation later |
| 9–11 | Numbers updated, but **not yet deeply reviewed** |

## Decisions made, with reasons

| Decision | Reason |
|---|---|
| Cramér's V removed | Not in the course; effect size is now the percentage-point gap |
| `car::vif` replaced by `vif_glm()` | The `car` package would not install |
| `met`: 0 means "no" | `met_o` equals the partner's `met` with 0 recoded as 2 in 7,993 of 7,993 rows |
| Values outside 1–10 become NA | Their meaning can't be proven; a 0 has no single meaning |
| Participant 66: `amb1_1` 53 → 5 | The other five traits sum to 95; 53 is by far the highest value (next is 30). Logical imputation, disclosed as strong evidence, not proof |
| `attr_relativno` uses only earlier dates | Otherwise it used dates that had not happened yet (breaks the time rule) |
| H3 race tested per person (paired Wilcoxon) | The row-level test mixes different people and hid the effect |
| `samerace` set to NA in the 136 rows with unknown race | It says 0 there without real information; H3 drops them, models impute the mode ("Ne") |
| Partial preference answers: blanks set to 0 (participants 129, 130, 528) | Filled points already sum to 100; median imputation would push the sum over 100 |
| Blank forms (189 rows) kept | They have a recorded decision; the result doesn't depend on them |
| Extreme ages and IQR-flagged values kept | They are real and carry information; the result doesn't depend on them |

## Numbers for the defence (current)

**H1:** men 47.4% vs women 36.5% yes (11 percentage points), chi-square 101.36, p < 0.001. Per person (Mann-Whitney): 48.1% vs 37.4%, p = 0.000003.

**H3 race, each person compared with themselves:** 44.6% vs 38.4% (6.2 points, p < 0.001). Women 10.9 points (p < 0.001), men 1.8 points (p = 0.30). Row-level chi-square on 8,242 rows: p = 0.033.

**Chapter 4:** 189 blank forms (186 fully blank), only 4 ended in "yes". After removing them, only `shar` keeps a clear link with the decision (−12.5 points per person, p < 0.001).

**Models:**

| Result | Value |
|---|---|
| Lasso, cross-validation AUC | 0.836 |
| Lasso, test AUC | **0.821** (95% range 0.783–0.857) |
| Lasso, test accuracy | **75.1%** (always "no": 60.9%) |
| Columns in the final lasso | 12 |
| Logistic regression / ridge / kNN (k = 151), test AUC | 0.827 / 0.824 / 0.818 |
| With `like` and `prob`, test AUC | 0.854 |
| Test without blank forms | 0.817 |
| Test without rows involving ages over 34 | 0.821 |

## Still to do

- Review chapters 9 → 11, then explain chapters 6 → 11.
- Before submitting: set `koristi_cache <- FALSE` (line 21 of `Seminarski.Rmd`) and knit once from scratch.
- Knit to Word and check formatting; verify volume and page numbers in "Literatura".
- Shorten to about 45–50 pages.

## Technical notes

- The first knit on a new computer takes about 10 minutes, because the model cache (`Seminarski_cache/`) is not in git and has to be rebuilt. Later knits take about a minute.
- On the laptop, R is in `D:\R-4.3.2` and pandoc comes with RStudio. Paths on the desktop PC may differ; Claude can find them.
- `.RData` should not be restored at startup (RStudio: Tools → Global Options → General).
