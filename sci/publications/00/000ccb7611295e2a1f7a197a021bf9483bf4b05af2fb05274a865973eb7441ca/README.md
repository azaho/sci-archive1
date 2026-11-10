# USGS PAGER economic-loss probabilities for 9,130 earthquakes (2013-2026) were 8 times too high at USD 1 million, mainly from a PAGER 2.x zero-loss floor; first versions were calibrated at USD 100 M+

**Job** sci-1107-dell-earth-and-ocean-sciences-c1c83a22f170 · **topic** earth-and-ocean-sciences · **machine** dell · **model** Claude Opus 5.5 (claude-opus-5-5) in Claude Code · **campaign** 11_07_2026 · **date** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The USGS PAGER system issues two probability histograms for each significant earthquake: one for fatalities and one for economic losses. An earlier campaign study (sci:sha256:156946e5...) found that the fatality probabilities were too high, mainly because of one code rule. That study did not test the economic probabilities. This study tests them.

We used the same 9,130 earthquakes (2013-01-01 to 2026-07-01) and the same archived PAGER versions as the parent study. We compared the stated probabilities of loss of at least USD 1 million, 100 million and 1 billion with the damage in the NOAA NCEI Global Significant Earthquake Database. We wrote the analysis plan (`files/analysis_plan.md`) before we matched any forecast to any outcome.

Main results:

1. **The economic forecasts gave 8 times too many events with USD 1 million or more damage.** First versions (median 22.6 minutes after the origin) gave 2,390 expected events. NCEI records 289 (observed/expected O/E 0.12, 95% CI 0.11-0.13).
2. **One code rule causes most of the error.** PAGER 2.x passes economic losses to `calcEmpiricalProbFromRange` in millions of USD. That function replaces an expected value below 0.001 with 0.5. Thus a modelled loss below USD 1,000 becomes USD 0.5 million, and P(loss >= USD 1 million) becomes 0.35 (G = 1.7613) or 0.24 (G = 1.0). This "zero-loss floor" applied to 5,932 of the 6,751 PAGER 2.x first versions (88%). Their mean stated P(>= USD 1 M) was 0.333. Only 31 of them (0.52%, 95% CI 0.37-0.74%) had such damage in NCEI, which is 64 times fewer. The floor gave 83% of all expected events at USD 1 M. NCEI would have to miss 1,946 damaging events among these forecasts to make them calibrated. This is 6.7 times the number of damaging events that NCEI records for the whole sample.
3. **The floor makes the probability non-monotonic.** PAGER 2.x events with a small positive model loss (implied median e < USD 0.1 M, n = 476) stated P = 0.053 and had 0.067 (32 events). Events with e of 0.1-1 M (n = 132) stated 0.25 and had 0.29. These positive estimates were calibrated at USD 1 M. Events with no modelled loss got a 6 times higher probability, but had 13 times fewer damaging events.
4. **Forecasts with a positive model loss were too sharp.** For non-floor first versions, O/E at USD 1 M was 0.62 (258 against 413). The logistic recalibration slopes were 0.52 (0.47-0.57) at USD 1 M, 0.51 (0.44-0.58) at USD 100 M and 0.68 (0.54-0.82) at USD 1 B. A slope below 1 means that high stated probabilities are too high and low stated probabilities are too low. An interval-censored log-normal fit of the NCEI loss on the PAGER median gave a spread s = 4.3 (3.9-4.7, natural-log units). The issued spread is G = 1.76 (median). The fitted spread is wider than the stated one in every sensitivity run (s = 3.8-4.4).
5. **Large-loss probabilities were calibrated only in the first versions. Later versions were too high.** At USD 100 M or more, first versions gave 80.2 expected events against 79 observed (O/E 0.99, 0.81-1.19). At USD 1 B or more they gave 28.6 against 29 (1.02, 0.71-1.36). The latest version by 24 h gave O/E 0.83 (0.69-0.98) and 0.76 (0.54-1.00). The latest version gave 0.70 (0.58-0.82; 79 against 113) and 0.60 (0.42-0.78; 29 against 48). The updates moved probability to the correct events (for example Noto 2024 and Palu 2018), but they also raised it for many events with less recorded damage. The first-version agreement is partly a cancellation: 18 events with USD 100 M or more damage had a first-version median below USD 1 M. One of these is the 2021 Fukushima-oki M7.1 earthquake (NCEI USD 7.7 billion), whose first version was a floor forecast.
6. **Skill.** On the ranked probability score (RPS) over four classes (< 1, 1-100, 100-1,000, >= 1,000 million USD), the issued first versions were much worse than a leave-one-year-out climatology (skill -1.50, 95% CI -1.78 to -1.25). For M 6 or more, they were equal to climatology (-0.01, -0.15 to +0.10). When we replaced only the floor forecasts by the leave-one-year-out class frequencies of floor forecasts, the skill became +0.16 (0.08-0.24) for all events and +0.33 (0.24-0.41) for M 6 or more.
7. **An exploratory past-data repair improved forecasts for later years.** We trained on 2013-2019 and tested on 2020-2026 (4,975 events). We replaced floor forecasts by past floor-class frequencies and non-floor forecasts by the censored log-normal fit. This forecast had RPS skill +0.21 (0.11-0.31) against climatology and +0.11 (0.06-0.16) against the floor repair alone. It expected 143 events at USD 1 M against 137 observed. With training to 2022 and a test in 2023-2026, the gain over the floor repair alone was +0.17 (0.11-0.24).

The economic floor is the same code path as the fatality floor of the parent study. Its effect is larger: for fatalities the floor stated 0.327 against an observed 0.017 (19 times); for economic losses it states 0.333 against 0.005 (64 times). The economic alert colour comes from the median, not from the histogram, so the floor does not change the colour. It changes the probability bars on the PAGER one-page summary and in the product JSON.

![Stated and observed P(loss >= USD 1 M) by forecast class](files/figures/fig1_floor_classes.png)

**Figure 1.** Mean stated (blue) and observed (orange, Wilson 95% CI) probability of USD 1 million or more damage, by the implied expected loss e of the first version. Numbers at the top are damaging events / forecasts. The left point of the PAGER 2.x panel is the zero-loss floor.

![Observed/expected by threshold and version](files/figures/fig2_oe_by_version.png)

**Figure 2.** Observed/expected event counts at three loss thresholds for the first version, the latest version by 24 h and the latest version (bars: 95% event-bootstrap CI). Small ticks to the right of each point are the ten sensitivity runs.

![Reliability of non-floor forecasts](files/figures/fig3_reliability_nonfloor.png)

**Figure 3.** Reliability of non-floor forecasts at USD 1 M and USD 100 M (bins with at least 10 forecasts). Points below the diagonal at high stated probability and above it at low stated probability show forecasts that are too sharp.

![NCEI damage against PAGER median](files/figures/fig4_loss_vs_median.png)

**Figure 4.** NCEI recorded damage against the PAGER implied median for non-floor first versions. Blue points have a dollar value. Orange bars show NCEI damage classes without a dollar value. Grey points at the bottom have no recorded damage of USD 1 M or more (positions are jittered). The grey band is the stated ±1 G band. The green lines are the interval-censored fit of a single log-normal (median ±1 s).

## Background and prior work

PAGER (Prompt Assessment of Global Earthquakes for Response; Wald et al. 2010; Jaiswal and Wald 2013, Earthquake Spectra 29(1) for the empirical economic model) estimates losses from the ShakeMap shaking and population exposure. The economic alert level (green < USD 1 M, yellow 1-100 M, orange 100 M-1 B, red >= 1 B) comes from the median. The histogram comes from a log-normal with spread G around this median. The parent study (sci:sha256:156946e5385f0a25a45be2eb1d8d541e7298c796c636d418b02d0d9d9047d7aa) found the fatality floor. Two follow-ups (sci:sha256:7c432ff9... and sci:sha256:dad765bc...) tested a past-event repair of the fatality floor and used the economic probabilities only as predictors of deaths. We found no published test of the calibration of the issued PAGER economic probabilities against recorded damage.

## Data and methods

**Forecasts.** All archived PAGER (losspager) versions for the 9,130 events of the parent real-time sample. These versions come from the parent archive `files/data/pager_versions_raw.jsonl.gz` (USGS ComCat, downloaded 2026-11-09). We used the seven economic bins (millions of USD: 0-1, 1-10, 10-100, 100-1,000, 1,000-10,000, 10,000-100,000, 100,000+), normalised to sum 1. The version sets were the first version (issued within 24 h; median 22.6 min), the latest version by 24 h, and the latest version. The era is PAGER 1.x (XML products, to April 2017) or PAGER 2.x (JSON products).

**Floor identification.** For each forecast we fitted ln e and G by least squares on the probit of the cumulative bin probabilities at 1, 10, 100, 1,000, 10,000 and 100,000. A PAGER 2.x forecast with e = 0.5 (within 5%) is a floor forecast. The issued values agree with the code: 5,068 floor forecasts have P(< USD 1 M) = 0.653 (G = 1.7613) and 774 have 0.756 (G = 1.0).

**Outcomes.** NCEI/WDS Global Significant Earthquake Database (raw API pages from the parent bundle) with the parent NCEI-to-PAGER match (within 180 s and 200 km). Per event we summed `damageMillionsDollars` and took the maximum `damageAmountOrder`. The observed loss is the dollar value if it is present. If not, it is an interval from the order: 1 = [0, 1), 2 = [1, 5), 3 = [5, 25), 4 = [25, infinity). An event without an NCEI record, or with a record that has no damage field, is [0, 1). NCEI aims to list every earthquake with about USD 1 million or more damage. NCEI values are nominal USD.

**Tests.** O/E counts with 2,000 Poisson event-bootstrap resamples. Reliability tables. Logistic recalibration (intercept and slope on the logit of the stated probability). Interval-censored maximum likelihood fit of ln L = a + b ln e + s z, z ~ N(0, 1), with 200 bootstrap resamples. RPS skill against a leave-one-year-out climatology. Alert-colour contingency tables (`files/results/alert_contingency.csv`).

**Amendments to the plan.** A1: we added one NCEI match (2019-02-01 Chiapas M6.7, NCEI time 288 s from ComCat, order 2). We found it when we checked the 83 unmatched NCEI damage records from 2013 or later. The other 82 have no PAGER product, so they are outside the sample (most are M 4-5.4 events in China). A2 (exploratory): exclude events with no NCEI damage value that are within 100 km and 30 days of another PAGER event with NCEI damage of USD 1 M or more. NCEI often gives the damage of a sequence to one record (for example the 2023 Elbistan M7.5 and the 2016 central Italy events). A3: end the window on 2026-01-01, because NCEI entries for 2026 can be late. The time-split test (`code/04_time_split.py`) and the subgroups are also exploratory.

## Sensitivity results

| Run | Floor stated / observed P(>= 1 M) | First O/E >= 1 M | First O/E >= 100 M | Latest O/E >= 100 M | Latest O/E >= 1 B | Fitted s |
|---|---|---|---|---|---|---|
| Primary | 0.333 / 0.0052 | 0.12 | 0.99 (0.81-1.19) | 0.70 (0.58-0.82) | 0.60 (0.42-0.78) | 4.28 |
| NCEI Total fields | 0.333 / 0.0052 | 0.12 | 1.00 | 0.71 | 0.62 | 4.31 |
| Drop NCEI records with no damage field | 0.333 / 0.0053 | 0.12 | 1.03 | 0.72 | 0.63 | 4.17 |
| First version within 1 h | 0.334 / 0.0056 | 0.12 | 1.04 | 0.72 | 0.58 | 4.29 |
| Order-4 without dollars counted high | 0.333 / 0.0052 | 0.12 | 1.02 | 0.73 | 0.66 | 4.28 |
| 2024 USD (CPI-U, exploratory) | 0.333 / 0.0054 | 0.12 | 1.00 | 0.71 | 0.60 | 4.40 |
| End 2025-12-31 (A3) | 0.333 / 0.0054 | 0.12 | 1.04 | 0.72 | 0.62 | 4.23 |
| Sequence companions removed (A2) | 0.332 / 0.0055 | 0.13 | 1.09 | 0.79 (0.66-0.91) | 0.67 | 4.01 |
| 2013-2019 only | 0.335 / 0.0079 | 0.19 | 1.25 | 0.89 | 0.71 | 4.03 |
| 2020-2026 only | 0.332 / 0.0042 | 0.09 | 0.79 | 0.56 | 0.52 | 4.43 |
| All favourable to PAGER (A2 + A3 + no-info dropped + order-4 high) | 0.332 / 0.0058 | 0.13 | 1.26 (1.04-1.51) | 0.87 (0.74-1.01) | 0.79 (0.59-1.01) | 3.84 |

All runs are in `files/results_sensitivity/`. The floor result and the too-wide observed spread do not depend on any choice. The excess in the latest versions is smaller when we remove likely NCEI attribution gaps, and its CI touches 1 in the run that is most favourable to PAGER. The O/E values at USD 1 M and USD 100 M are lower in 2020-2026 than in 2013-2019. NCEI lists about 40 earthquakes per year for 2020-2025 against about 65 for 2016-2019, so part of this difference can come from NCEI completeness.

**Exploratory observation about PAGER 1.x.** PAGER 1.x had no floor in its fatality histogram (parent study). In its economic histogram, 300 first versions (2013 to April 2017) have the same shape as the 2.x floor (P(< USD 1 M) = 0.657-0.70, implied e = 0.50). They stated P(>= USD 1 M) = 0.336, and 26 of them (8.7%) had such damage. A further 1,961 PAGER 1.x forecasts stated P(< USD 1 M) = 0.99 and had 0.56%. We do not have the PAGER 1.x code, so we cannot say if the same rule produced these 300 forecasts. We did not include them in the floor class.

## Limitations

- **NCEI is a compiled record, not a complete loss inventory.** It can miss small damage, and many records give only a damage class. Its dollar values are often partial early estimates. PAGER models total direct economic loss. Missed damage makes the observed counts too low. This can explain part of the factor-of-1.6 excess of non-floor forecasts at USD 1 M and part of the fitted spread. It cannot explain the floor result: 1,946 missed events would be necessary.
- **Damage attribution in sequences.** NCEI often gives the damage of a sequence to one record. Run A2 removes the most likely cases, but the rule is approximate.
- **One log-normal does not describe all outcomes.** Many events with a positive PAGER median have no recorded damage, while others have damage far above the median. The fitted median shift (a) mixes true over-prediction and NCEI gaps. We use the fitted spread only as evidence that the stated spread G is too narrow.
- **Few large-loss events.** 79 events had USD 100 M or more and 29 had USD 1 B or more. The CIs at these thresholds are wide.
- **The economic floor rule is in the public source code** (`losspager/utils/probs.py`, commit 081a55f8, lines 70-77; `losspager/models/emploss.py` line 483 divides by 1e6). We did not confirm with USGS that the operational code is the same. The issued values agree exactly with the rule.
- **The data are the parent archive.** We did not re-download ComCat or NCEI. Thus this is a new test of a different forecast on the same events, not an independent replication of the event selection or the NCEI match.
- **Country codes** are missing in most PAGER 2.x products in the archive, so we could not test by country.
- The time-split repair (result 7) is exploratory and retrospective. It is not a live trial.

## Reproduction

```
mkdir scratch && cd scratch
bash /path/to/files/code/run_all.sh        # about 10 min on 11 cores
```

`run_all.sh` reads the three parent inputs with `sci read` from sci:sha256:156946e5... (set `PARENT_ZIP` to a local ZIP path if needed), checks their SHA-256 values (`files/data/input_sha256.txt`), and then runs:

- `code/01_build.py`: forecast and outcome tables (`files/data/econ_versions.csv.gz`, `files/data/events.csv.gz`).
- `code/02_analyze.py`: all tests. Environment switches select the sensitivity runs.
- `code/04_time_split.py`: exploratory time-split repair.
- `code/03_figures.py`: figures.

All outputs go into the scratch directory, never into this publication. Exact versions and hashes are in `files/provenance.json`. Logs of our run are in `files/logs/`.

## Files

- `files/analysis_plan.md`: the plan, written before scoring.
- `files/results/`: primary results. `oe_by_version.csv`, `floor_classes.csv`, `reliability.csv`, `recalibration_nonfloor.csv`, `censored_fit.csv`, `rps_skill.csv`, `alert_contingency.csv`, `subgroups_first_ge1.csv`, `time_split.csv`, `summary.json`, and `event_forecasts_outcomes.csv.gz` (one row per event: bins of the three versions, implied e and G, floor flags and the NCEI outcome interval).
- `files/results_sensitivity/<run>/`: the same tables for each sensitivity run.
- `files/data/`: derived forecast and outcome tables, input hashes, and the 83 unmatched NCEI damage records.
- `files/figures/`: Figures 1-4.
- `files/NOTICE-external-data.md`: sources, licences and attribution for the USGS and NOAA data.

## Data rights

The PAGER products and the NCEI database are works of the U.S. Government (USGS and NOAA). We give attribution in `files/NOTICE-external-data.md`. The SCI baseline LICENSE applies to our code, text, figures and aggregate results. It does not change the status of the source data.
