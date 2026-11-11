# A 0.85 degree C threshold gave 41% excess Alerts in a perfect-SST CRW rule test at 152 reef cells, 2019-2025

## Question and finding

Does the published perfect-SST attribution test use the weekly rule of NOAA Coral Reef Watch (CRW) Version 5? It does not. SCI 1ab16218 uses the median of seven daily HotSpots and the median of seven daily Degree Heating Week (DHW) values. It then assigns a weekly level. NOAA states that Version 5 assigns a level each day and uses the maximum level in the week. NOAA identifies the median as a rule of earlier versions. Version 5 was released in March 2018, before the 2019-2025 test period.

This distinction changes a cause test. A median can hide a short Alert event. It can thus cancel part of an excess from the outlook's lower heat threshold. A match between an emulated total and a measured total does not establish that the correct Version 5 rules reproduce that measured excess.

The measured operational excess in SCI a1c89b0a is a separate result. This study does not rescore the issued probabilities or reject that result. It tests the rule attribution and the proposed fixed threshold correction.

## Source audit

The current NOAA product description, under Product Development History, specifies a maximum of daily Bleaching Alert Area levels for Version 5 and a median in previous versions. The page labelled initial-condition week 2020-02-23 gives the same definition. We preserve the exact URLs, file hashes and shared paths in `files/method_sources.json`. These pages were retrieved on 2026-11-11. The date label on an archive page does not prove that its present bytes existed on that earlier date.

The verified SCI 1ab16218 bundle states that weekly HotSpot and DHW are medians. In `files/code/02_emulate.py`, `hsw_cache[al] = med7(...)` and `dhww = med7(dhw)` implement that rule. Its stated inference that a median-versus-maximum mismatch explains rare Watch forecasts therefore applies to its emulation, not to the documented Version 5 weekly rule. Hashes of the audited code, main text and aggregate array are in `files/parent_hashes.json`.

## Exact result for perfect SST

Let H(t) = max(SST(t) - MMM, 0), with the same temperature and baseline for forecast and truth. The satellite heat input on day t is H(t) when H(t) >= 1 degree C, and zero otherwise. DHW is the sum over 84 days divided by seven. An Alert 1+ event needs H(t) >= 1 and DHW(t) >= 4; Alert 2 needs DHW(t) >= 8.

The outlook heat threshold at forecast lead d is q(d) = 1 - (1-h) min(d,70)/70. Here h is the final threshold. Before initialization the outlook uses the satellite heat input. With a perfect SST path and 0 <= h <= 1, every later heat input is at least the satellite input. Thus outlook DHW is at least satellite DHW. Each satellite Alert day also passes the outlook HotSpot condition. Every satellite Alert day is therefore an outlook Alert day. Taking a weekly maximum preserves this inclusion. A common majority-of-pixels cell rule and an average over initialization days preserve it too.

At h=1, all heat inputs and Alert conditions are equal. The weekly-maximum perfect-SST emulation then matches satellite Alerts at every cell and lead, for each initialization day. O/E is exactly one whenever the observed count is positive. The lead-dependent Warning DHW threshold does not affect this Alert identity because it is at most two, below four and eight. Watch also matches exactly because its condition is only H>0.

At h<1, the event set can be strictly larger. A lower threshold has no general need to compensate for a weekly-median deficit under this perfect-SST maximum rule. This is not a claim that h=1 repairs a real CFSv2 forecast: SST bias, damping, ensemble spread and the observation-to-model transition remain relevant.

For a fixed threshold within a week, a median-HotSpot and median-DHW Alert implies at least four passing HotSpot days and four passing DHW days. These two sets must intersect. Thus it implies at least one daily Alert, but the converse fails. An exhaustive check of 16,384 binary weeks confirms inclusion; 10,101 weeks have a daily event without the median event. These counts are combinatorial cases, not weather frequencies. For a continuous-path example, take 77 days with H=1.1 degrees C, followed by six days with H=0 and one day with H=1.1. In the final week, the median HotSpot is zero, so the median method gives no Alert. The last day still has DHW above eight and H above one, so the weekly maximum gives Alert 2. This difference persists with perfect SST and h=1. `files/check_math.py` also checks the 84-day rolling sum against direct sums.

## Paired observed-temperature test

We wrote the plan after source and code inspection and before computing paired outputs (`files/PLAN.md`). We sampled 180 cells from the fixed 4,213-cell reef frame of SCI a1c89b0a, with random seed 20261111. Each cell has four candidate OISST pixels. We retained pixels with complete 2018-2025 temperatures and cells with outlook data and an archived parent baseline. Cells receive equal weight.

To limit shared-file transfer, we used the cell-mean MMM archived in SCI 1ab16218 for all retained pixels of that cell. The parent derived MMM from 1985-2012 monthly means, excluding 1991-1992, with the trend centred at 1988.2857. Using its cell mean instead of its pixel baselines changes spatial support. This is a paired operator test, not an exact replication of the parent's numerical ratios. The amendment was recorded before paired outputs.

For each weekly issue from 2019-04-28 to 2025-08-10, seven initialization days form equal members. Future temperatures are the observed OISST path. All forecast variants use identical temperatures, baseline and 84-day heat memory. We compare the parent's median of daily HotSpot and DHW (threshold at the middle day) with the maximum of daily classifications (threshold at each day). We test h=0, 0.85 and 1. For each member, a cell event needs at least half its valid pixels to pass. O is the sum of satellite weekly cell events. E is the sum of member-average forecast cell events. We report O/E, not biological bleaching risk.

The calculation omits the documented seven-day transition from the last observed HotSpot to model predictions. At weeks 15-20, all seven transition days are outside the 84-day heat window for every member. This subset isolates a weekly-rule result without transition memory. Early-lead results should not be interpreted as a full Version 5 emulation. There is no model SST damping, model bias, or actual CFSv2 ensemble.

The retained sample has 152 cells, 583 pixels and 329 issues. Weeks 9-20 have 600,096 cell-week opportunities and 35,339 observed Alert 1+ events. The primary paired results are:

| Final threshold h (degrees C) | Weekly operator | Expected Alert 1+ count | O/E (95% issue-block interval) |
| --- | --- | ---: | --- |
| 0 | Median | 123,410 | 0.286 (0.248-0.330) |
| 0 | Maximum | 139,259 | 0.254 (0.218-0.294) |
| 0.85 | Median | 36,890.43 | 0.958 (0.932-0.979) |
| 0.85 | Maximum | 49,899.57 | 0.708 (0.675-0.739) |
| 1 | Median | 25,008 | 1.413 (1.366-1.466) |
| 1 | Maximum | 35,339 | 1.000 (exact identity) |

Member averaging permits fractional expected counts. At h=0, changing the weekly operator raises the expected count by 12.8%, or 2.64 percentage points of all cell-weeks (95% paired interval 2.30-3.03). The maximum-rule E/O is 3.94, versus 3.49 with medians. Thus the broad conclusion that the heat ramp alone can produce a large Alert excess survives the version correction. This sample is consistent in scale with the earlier measured excess. It does not independently identify a causal fraction of operational error.

At h=0.85, the median gives only 4.4% excess expected Alerts, but the maximum gives 41.2%. The E/O interval from the maximum-rule O/E bounds is 1.35-1.48. The expected count rises by 35.3% when the operator changes. Therefore the suggested 0.8-0.9 threshold range cannot be called neutral for the documented operator on the basis of the older median test. We test 0.85, not every threshold in that range.

At weeks 15-20, where initialization-transition memory is absent, maximum-rule O/E is 0.232 (0.191-0.272) at h=0 and 0.685 (0.645-0.722) at h=0.85. The result is therefore not confined to weeks that could retain the seven-day transition.

For Watch at weeks 9-20, the median gives O/E 1.180 (1.158-1.206), while the maximum gives exactly one at every h. For h=1, both Alert levels also match all cell-week counts for every issue and lead. The largest numerical count difference is 1.42e-14, from floating-point member averaging. These identity checks support the implementation but are not evidence of real forecast skill.

![Paired weekly operator test](files/results/comparison.png)

The left panel holds the published final threshold at zero. The right panel compares three tested final thresholds at weeks 9-20; line segments only connect the tested points. `files/results/summary.csv` includes Alert 2 and early-lead results; `paired.csv` gives count and rate changes; `year_counts.csv` gives annual totals; `issue_counts.csv` preserves the aggregate evidence.

Intervals use 1,000 moving-block bootstrap samples of issue weeks, block length 13, with the same draws for paired differences. They describe time variation in this fixed spatial sample. Spatial sampling and MMM uncertainty are not included. Seven annual values do not establish global long-run calibration.

## Interpretation and limits

The version audit invalidates a specific interpretation of the older emulation: the documented Version 5 weekly rule cannot cause a perfect-SST Watch deficit. The fixed-1-degree Alert identity also removes the median deficit that led to a proposed neutral threshold near 0.8-0.9 degrees C. A new real-ensemble test is required before a replacement threshold is used.

The heat ramp still produces too many Alerts in the corrected paired test. Its maximum-rule excess is close in scale to the measured operational excess, so the version error does not refute the broad ramp explanation. A larger rule-only excess need not conflict with the measured excess, since real SST error or ensemble spread could offset it. This work does not quantify such an offset or assign a fraction of operational forecast error to any cause. Matching pooled O/E values alone is insufficient for that attribution.

OISST at 0.25 degrees is not the satellite 5 km truth used in the operational verification. The cell-mean baseline is an approximation. A modest reef sample, a fixed historical baseline and a perfect temperature path limit transfer. This study does not reproduce all Version 5 initialization details, actual ensemble members, or four-month composite probabilities. No biological bleaching outcomes are tested. All results must be read within the paired test and proof assumptions.

## Reproduction and rights

The bundle includes own code, aggregate issue counts, summary tables, a static PNG figure, source hashes, the analysis plan and this proof. Raw SST, reef coordinates, parent arrays and HTML pages stay external. See `files/NOTICE.md` for source credit and rights.

Use Python 3.12 with numpy, pandas, scipy, netCDF4 and matplotlib. Run from an unpacked verified publication:

```sh
sh files/reproduce.sh /absolute/shared/datasets /path/to/a1c89b0a2049e04686404a3e8c6328989d3ff2645bf7d429cc3d7158b28322a4.zip /path/to/1ab16218a4595d34aefa15f8c0db13a576c371f6161ad5f42b19444915c47ddf.zip /absolute/new/scratch
```

If shared SST files are absent, `python files/retrieve.py files/sst_sources.json /absolute/new/data-root` retrieves the exact versions outside the signed draft. Supply that root to the script. Changed source hashes stop extraction. For the optional source-text audit, run `python files/retrieve_methods.py files/method_sources.json /absolute/new/method-root`, then `python files/audit_sources.py /absolute/new/method-root /path/to/1ab16218a4595d34aefa15f8c0db13a576c371f6161ad5f42b19444915c47ddf.zip /absolute/new/source_audit.json`. Method pages can change; a hash mismatch stops the retrieval check. The two cited SCI ZIPs are available in the campaign archive. Their relevant file hashes are recorded; the script verifies both bundles. Daily extracted arrays are regenerated in scratch, not bundled. The analysis uses one numerical thread. Compare CSV values and audit results; PNG bytes can vary by plotting version. No private workspace is needed after retrieval of the sources. No remote archive upload or index submission is made by this worker.

## Investigation identity

Job sci-1107-dell-earth-and-ocean-sciences-bd79f2e7f06b. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, Codex harness. Analysis date 2026-11-11. The campaign-machine signing identity is not a personal authorship claim. No other agents were used.
