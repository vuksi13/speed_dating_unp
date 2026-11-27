# Change log: what we changed and why

A running list of every correction to the seminar, so you can explain to the professor what was done and why. Newest chapter at the bottom. Each entry says what was wrong or missing, what we changed, and the reason.

## Whole seminar

| What | Why |
|---|---|
| Cramér's V removed; effect size is now the gap in percentage points | Not part of the course; a percentage gap is easier to interpret |
| `car::vif` replaced with our own `vif_glm()` | The `car` package would not install; the result is the same for numeric predictors |
| Caching for the slow model chunks | A full knit took about 10 minutes; now it takes about 1 minute after the first knit |

## Chapter 1: Uvod

| What | Why |
|---|---|
| Added a note on three participants aged 18–19 | The text said "postdiplomci", but some are too young to be graduate students |

## Chapter 2: Opis i priprema podataka

| What | Why |
|---|---|
| Rewritten and shortened; column descriptions moved to an appendix | Easier to read; the full list stays available |
| Added a check of same home area via zip code (74 dates, p = 0.34) | The `from` column is free text and can't be compared; the result isn't significant, so it isn't added to models |
| Noted that the zip-code test is only a rough row-level check | Rows of the same person aren't independent |
| Noted that H5 uses the partner's `career_c` as the status measure | `income` is the median income of the home area, not personal income, and `income`/`mn_sat` are missing for about half the participants |

## Chapter 3: Čišćenje podataka

| What | Why |
|---|---|
| `met`: 0 treated as "no" | In 7,993 of 7,993 rows the partner's `met_o` matches `met` with 0 recoded to 2; wave list shows 0 was used instead of 2 |
| All values outside the 1–10 scale set to NA (515 fields) | A 0 has no single meaning: its "yes" rate looks like a 1 for `prob`, but like nothing else for `shar` |
| Participant 66: `amb1_1` 53 changed to 5 | The other five traits sum to 95, so 5 makes exactly 100; 53 is the largest value in the column (next is 30). Logical imputation: strong evidence, not proof |
| `samerace` set to NA in 136 rows where one person's race is unknown | It said 0 ("different race") without real information. H3 now drops these rows automatically. Models fill NA with the most common value ("Ne"), so model input is the same |
| Partial preference answers: blank fields set to 0 (participants 129, 130, 528) | The filled fields already sum to 100, so the blanks mean 0 points. Left as NA, median imputation would add about 10 points per blank and push the sum over 100 |

## Chapter 4: Nedostajuće vrednosti

| What | Why |
|---|---|
| Missingness test excludes invalid values (zeros) | They weren't skipped ratings, so counting them as missing mixed two different things |
| Added a per-person test (paired Wilcoxon) next to the chi-square | Rows of the same person aren't independent; the per-person test showed that only `shar` keeps a real link with the decision (−12.5 points) |
| "189 fully blank forms" corrected to 186 fully blank + 3 with only invalid values | The original count was wrong |
| Added a bar chart of the "yes" share by number of blank ratings | Shows the drop from 43.5% to 2.1% at a glance |
| Counts updated after the chapter 3 fixes: 58 columns with NA, 6,270 complete rows (74.8%) | `samerace` now has NA values; the preference zeros made 30 more rows complete |

## Chapter 5: Ekstremne vrednosti

| What | Why |
|---|---|
| Intro compares three methods (boxplot, z-score, IQR) and explains why IQR is the main one | Quartiles don't depend on the extreme values and don't assume a normal distribution |
| `exphappy` added to the check (29 flagged columns) | It was missing from the list |
| Rewrote the IQR examples with actual numbers (reading: fence 4, 26 people; `attr1_1`: fence 40, 39 people) | The old "middle 50%" wording and "about 20 points" were confusing |
| Model sensitivity check without extreme ages (chapter 10: AUC 0.821) | Shows the result doesn't depend on these participants |

## Chapter 6: Eksplorativna analiza

| What | Why |
|---|---|
| New section "Izbor promenljivih": correlation of all 51 numeric columns with `dec` | Answers "why these variables?": only the 8 date ratings have correlation ≥ 0.1; 35 columns are below 0.05 |
| Ratings boxplot now ordered by mean, with the mean as a red dot; table shows mean, median and SD | The text talked about means while the graph showed medians, so they seemed to disagree |
| Explained what standard deviation means (e.g. `shar` SD 2.11 = about two points from its mean) | The number was given without explanation |
| Explained how the attractiveness graph is built (e.g. men gave a 7 on 855 dates and said yes on 510 → 59.6%) | It wasn't clear what each point means |
| Corrected: at low attractiveness ratings women say yes slightly more often, not "identically"; men are higher only at ratings 6–9; women at 9 are 74.9%, not "over 75%" | The old text didn't match the data |
| "Even for women, attractiveness pulls hardest" changed to point to H4 | Chapter 6 never showed women separately |
| Small vs large events: noted that size is the same for everyone at one event | The difference can come from other differences between events |
| "Druga tabela" fixed; tables printed as real tables | The first output was a chart, not a table |
| Clarified the preference scale is 100 points for everyone | Waves 6–9 answered on 1–10 but the data were already converted to 100 |
| Conclusion as prose instead of bullets; filler words removed | Shorter and easier to read |

## Later chapters affected by earlier fixes

Numbers already updated in chapters 7–10 after the chapter 3 fixes: H4 now has 124 people (participant 528 was dropped before because of a blank field), attractiveness 24.0 → 32.4 points; small model changes (logistic regression CV accuracy 74.9%, test 75.8%; recall at threshold 0.35: 84.8%). Main results unchanged: lasso test AUC 0.821, accuracy 75.1%.
