# Repose and eruption size in the GVP Holocene catalog: most of the long-repose signal comes from old, incomplete records

**Job** sci-1107-hp-earth-and-ocean-sciences-b809cfa0d8d0 · **topic** earth-and-ocean-sciences · **machine** hp · **model** Claude Opus 5.5 (claude-opus-5-5) · **campaign** 11_07_2026 · date 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Many hazard statements say that volcanoes with long repose have larger eruptions. In the full Smithsonian GVP Holocene catalog, 74% of VEI 5 and 93% of VEI 6+ eruptions came more than 100 years after the previous recorded eruption, but only 9% of VEI 2 eruptions did. We tested how much of this pattern is a property of volcanoes and how much is a property of the record.

1. **The record makes most of the naive pattern.** 61% of VEI 4 and 79% of VEI 5+ records start before 1500 and come from geological dating, while small eruptions before 1950 are rarely recorded (VEI 0-1 recorded rate in 1500-1799 is 3% of the 1950-2026 rate). The slope of VEI on log10 gap is 0.29 per tenfold gap in the pooled catalog. It falls to 0.10 when we compare only eruptions of the same volcano in the same era.
2. **Within volcanoes, in the near-complete 1950-2026 record, a weak size-predictable signal remains.** For 691 VEI >= 2 eruptions with a dated preceding repose (152 volcanoes, 60 informative), the odds of VEI >= 3 rose by a factor of 1.77 per tenfold longer repose (95% CI 1.12-2.78; within-volcano permutation p = 0.019). The VEI slope is 0.09 per tenfold repose. The signal is not robust: it is not significant with 1900-2026 or 1980-2026 windows, and it goes to zero when VEI 1 eruptions enter the sequence (1980-2026). It is present at less frequently erupting volcanoes and stratovolcanoes, and absent at the 52 volcanoes with 10 or more eruptions.
3. **Large eruptions did not lengthen the next repose (no time-predictable behaviour).** After VEI >= 3 eruptions the next VEI >= 2 onset came, if anything, sooner than after VEI 2 eruptions at the same volcano (hazard ratio 1.17, 95% CI 0.98-1.39, permutation p = 0.075; 1,317 eruptions, 251 volcanoes). Eruption duration did not change the next repose (HR 1.00 per tenfold duration). Frequently erupting ("open-conduit-like") volcanoes also showed no time-predictable lengthening (HR 1.08, 0.89-1.32).
4. **Repose adds little forecast skill beyond volcano history.** For eruptions in 2000-2026 (508 eruptions, 164 volcanoes), a model trained on 1950-1999 that used the volcano's past share of VEI >= 3 reduced log loss by 0.038 (95% CI 0.006-0.069) against a base rate. Adding the time since the last recorded eruption reduced log loss by a further 0.008 (95% CI -0.004 to 0.021).

## Question and motivation

Two simple recurrence models are often tested for volcanoes, as for earthquakes and tremor:

* **Size-predictable:** a longer repose before an eruption gives a larger eruption (more time to accumulate magma).
* **Time-predictable:** a larger eruption gives a longer repose after it (more time to refill).

Marzocchi and Zaccarelli (2006) reported time-predictable behaviour at open-conduit volcanoes and Poisson behaviour at closed-conduit volcanoes. Passarelli and Brodsky (2012) linked repose to magma viscosity. Colosi and Brodsky (2022) showed that volcano-specific history improves VEI forecasts. Burgos et al. (2022) studied eruptions from long-dormant volcanoes. A global catalog test must separate three effects: (a) differences between volcanoes, (b) changes in record completeness with time and size, and (c) the within-volcano dependence that the two models describe. We designed the tests below to separate these effects.

## Data

* Smithsonian Global Volcanism Program, Volcanoes of the World (VOTW) Holocene eruptions and Holocene volcanoes, WFS CSV layers downloaded 2026-11-09 (UTC). The catalog contains eruptions to March 2026 (latest dated start or end: 2026.25). The layers are live; the version number was not in the WFS output. The current GVP database citation form is: Global Volcanism Program, Volcanoes of the World (v. 5.3.x), Smithsonian Institution, compiled by Venzke, E., https://doi.org/10.5479/si.GVP.VOTW5-2025.5.3.
* Shared campaign copies used (read in place, not changed):
  * `datasets/gvp-votw-holocene-eruptions-wfs-20261109/gvp_holocene_eruptions.csv`, 2,161,706 bytes, SHA-256 `c13b4994579ba1933a885a34f644a45e9c226e5ff94396447f638bf107d16cd4`
  * `datasets/gvp-votw-holocene-volcanoes-wfs-20261109/gvp_holocene_volcanoes.csv`, 1,892,509 bytes, SHA-256 `78ad6949d83de9e3c1ede489279030a8f8e00666abeac6b5d522fe9c67eeb1e1`
* The WFS output has a session-specific `FID` column, so a new download has a different raw hash. FID-free content hashes (table without `FID`, sorted by `Eruption_Number` or `Volcano_Number`, written by pandas `to_csv(index=False)`): eruptions `fd94d092f221cd0edf8bd7222be8603e02a603942ef13ad5731c76fc20810a96`, volcanoes `26e1dc526966d4fbf53f5fe919683a75fc34756379a838e9d78f2a9a7258c6fa`. A fresh download on 2026-11-09 had the same content hashes.
* Source URLs: `https://webservices.volcano.si.edu/geoserver/GVP-VOTW/ows?service=WFS&version=2.0.0&request=GetFeature&outputFormat=csv&typeName=GVP-VOTW:Smithsonian_VOTW_Holocene_Eruptions` and the same with `typeName=GVP-VOTW:Smithsonian_VOTW_Holocene_Volcanoes`.
* The GVP data are under the Smithsonian Terms of Use (personal, educational and non-commercial use). **This bundle does not contain GVP records or record-level derived tables.** It contains only our code, figures and aggregate statistics. See `files/EXTERNAL_DATA_NOTICE.md`. `files/code/retrieve_gvp.py` downloads the layers into a separate local folder.

We used only confirmed eruptions (9,916). Dates use the start and end year, month and day; an unknown month is set to mid-year and an unknown day to mid-month.

## Methods

**Event sequences.** For a minimum VEI and a start year, we keep confirmed eruptions with VEI at or above the minimum and onset at or after the start year. For each eruption we compute, inside that set and the same volcano:

* preceding repose = onset minus the latest end of all earlier eruptions (missing if one of those ends is unknown; eruptions with repose <= 0 are not used in the size test);
* following repose = next onset minus own end (event), or catalog end (2026.25) minus own end (censored);
* onset-to-onset gaps as a sensitivity check.

The primary sequence is VEI >= 2, 1950-2026: 1,461 eruptions at 265 volcanoes. The recorded rate of VEI >= 2 eruptions is near constant across decades after 1950 (Figure 1C, `results/record_rate_by_vei_era.csv`), while VEI 0-1 recording increases after 1980. An eruption enters the size test only if its predecessor is also in the window. This selection depends on the repose (the predictor) and on the onset time, not on the VEI (the outcome).

**Naive pattern and design ladder.** For all VEI-dated confirmed eruptions, the naive gap is the onset gap to the previous recorded eruption of any size, in any era (7,255 eruptions with a gap). We fit the slope of VEI on log10 gap (A) pooled, (B) with volcano fixed effects, (C) with volcano x era fixed effects (eras <1500, 1500-1799, 1800-1899, 1900-1949, 1950-1979, 1980-2026), (D) with volcano fixed effects in 1950-2026 records, and, for the primary sequence, (E) between volcanoes (VEI on volcano mean log repose) and (F) within volcanoes. The 95% intervals come from 300-1,000 resamples of whole volcanoes.

**Size-predictable test.** Conditional logistic regression of VEI >= 3 (against VEI 2) on log10 preceding repose with volcano strata and decade indicators. We also give the within-volcano linear slope of VEI on log10 repose (1,000 volcano bootstrap samples) and two-sided permutation p values (2,000 permutations of VEI inside each volcano, and inside each volcano x era block, era split at 1980).

**Time-predictable test.** Stratified Cox model (volcano strata, Breslow ties) for the following repose, with VEI >= 3, numeric VEI, or log10 duration as the covariate. We wrote a fast one-covariate fit (`files/code/cox1.py`); it gives the same coefficients and standard errors as statsmodels PHReg to all printed digits. Intervals: Wald and 1,000 volcano bootstrap samples; p: 2,000 within-volcano permutations of the size label.

**Subgroups.** Major rock type (mafic, intermediate, silicic), number of VEI >= 2 eruptions in 1950-2026 (>= 10 as a proxy for persistently active, open-conduit-like volcanoes), volcano type and tectonic setting (GVP volcano table).

**Forecast test.** For each VEI >= 2 eruption since 1950 we predict P(VEI >= 3) from information dated before its onset: the volcano's past share of VEI >= 3 among VEI >= 2 eruptions in the whole Holocene record (shrunk to the training base rate with weight 2), an indicator of no earlier record, and log10 time since the last recorded eruption (any VEI or VEI >= 2). Logistic models are trained on 1950-1999 onsets (953 eruptions) and scored on 2000-2026 onsets (508). Log-loss differences have 95% intervals from 2,000 resamples of test volcanoes.

Random seed 20261109 in all scripts.

## Results

### 1. The naive pattern and the record (Figure 1)

| VEI | records with a gap | median gap (yr) | gap > 100 yr | share with onset < 1500 |
|---|---|---|---|---|
| 0-1 | 1,950 | 3.7 | 15% | 15% |
| 2 | 3,611 | 3.8 | 9% | 8% |
| 3 | 1,060 | 20 | 29% | 31% |
| 4 | 457 | 100 | 49% | 61% |
| 5+ | 177 | 380 | 77% | 79% |

(VEI 5 alone: 74% with gap > 100 yr; VEI 6+: 93%.) Large eruptions are mostly dated geologically, from tephra and radiocarbon records that do not keep small eruptions. Their "previous recorded eruption" is therefore usually another large eruption. Relative to 1950-2026, the recorded rate in 1500-1799 was 3% for VEI 0-1, 15% for VEI 3, 30% for VEI 4 and 64% for VEI 5+ (`results/record_rate_by_vei_era.csv`). VEI 2 has a high recorded rate in 1800-1979 (up to 1.19 times the 1950-2026 rate). This agrees with the GVP practice of assigning VEI 2 to explosive eruptions with little other information.

### 2. Design ladder (Figure 2, `results/design_ladder.csv`)

| design | n | VEI per tenfold gap (95% CI) |
|---|---|---|
| A pooled, all Holocene records | 7,255 | 0.29 (0.22-0.36) |
| B within volcano, all records | 7,255 | 0.27 (0.21-0.33) |
| C within volcano and era, all records | 7,255 | 0.10 (0.06-0.14) |
| D within volcano, 1950-2026 records, any-VEI gap | 2,513 | 0.16 (0.08-0.24) |
| E between volcanoes, 1950-2026 VEI >= 2 repose | 691 | 0.20 (0.03-0.35) |
| F within volcano, 1950-2026 VEI >= 2 repose (primary) | 691 | 0.09 (0.00-0.18) |

Comparison of eruptions within the same era removes about two thirds of the pooled slope. Volcano identity alone (B) removes little, because the main bias is within volcanoes: their old records hold only large eruptions.

### 3. Size-predictable test (Figure 3A, `results/size_predictable_tests.csv`)

| sequence | n | informative volcanoes | OR for VEI >= 3 per tenfold repose (95% CI) | permutation p |
|---|---|---|---|---|
| **VEI >= 2, 1950-2026 (primary)** | 691 | 60 | **1.77 (1.12-2.78)** | 0.019 (0.025 in era blocks) |
| VEI >= 2, 1900-2026 | 554 | 53 | 1.39 (0.85-2.29) | 0.12 |
| VEI >= 2, 1980-2026 | 556 | 55 | 1.51 (0.89-2.57) | 0.072 |
| VEI >= 1, 1980-2026 | 861 | 59 | 1.26 (0.76-2.11) | 0.66 |
| VEI >= 2, 1950-2026, onset-to-onset gap | 1,196 | 86 | 1.35 (0.95-1.93) | 0.010 |
| VEI >= 2, 1950-2026, VEI without "?" | 633 | 55 | 1.89 (1.16-3.05) | 0.011 |
| VEI >= 2, 1950-2026, previous eruption VEI 2 only | 492 | 45 | 2.49 (1.32-4.70) | 0.017 |
| VEI >= 2, 1950-2026, previous eruption VEI >= 3 only | 199 | 32 | 1.92 (0.82-4.51) | 0.18 |

Control for the size of the previous eruption did not change the repose term (OR 1.74, 1.10-2.76). Thus the signal does not come only from small follow-up eruptions soon after large ones. The 1900-2026 sequence has fewer usable eruptions than the 1950-2026 one because more pre-1950 end dates are unknown. The VEI >= 1 sequence result (no signal) can mean that VEI 1 eruptions break long VEI >= 2 reposes into short ones, or that the VEI >= 2 result is partly chance. We cannot separate these two explanations.

### 4. Time-predictable test (Figure 3B, `results/time_predictable_tests.csv`)

| covariate / sequence | n (events) | HR for next VEI >= 2 onset (95% CI) | permutation p |
|---|---|---|---|
| **VEI >= 3, true repose, 1950-2026 (primary)** | 1,317 (1,069) | **1.17 (0.98-1.39)** | 0.075 |
| numeric VEI, true repose | 1,317 (1,069) | 1.13 per VEI unit (0.98-1.31) | 0.086 |
| VEI >= 3, onset-to-onset gap | 1,461 (1,196) | 0.85 (0.72-1.01) | 0.063 |
| VEI >= 3, 1900-2026 | 1,925 (1,639) | 1.16 (1.00-1.34) | 0.040 |
| VEI >= 3, 1980-2026 | 807 (607) | 1.19 (0.94-1.50) | 0.15 |
| VEI >= 3, VEI >= 1 sequence 1980-2026 | 1,349 (1,106) | 1.10 (0.90-1.35) | 0.35 |
| log10 duration, true repose | 1,317 (1,069) | 1.00 (0.93-1.09) | 0.92 |

The time-predictable model requires HR < 1 (a longer wait after larger eruptions). All true-repose estimates are at or above 1. The onset-to-onset HR below 1 is expected without any physics, because onset-to-onset gaps include the eruption duration and larger eruptions last longer. The pooled survival curves in Figure 3B mix volcanoes; the hazard ratio compares eruptions of the same volcano.

### 5. Subgroups (`results/subgroups.csv`; light permutation counts)

| group | size OR per tenfold repose (95% CI) | time HR after VEI >= 3 (95% CI) |
|---|---|---|
| less frequent (< 10 eruptions, 213 volcanoes) | 3.45 (1.60-7.45) | 1.46 (1.04-2.06) |
| frequent (>= 10 eruptions, 52 volcanoes) | 1.11 (0.58-2.13) | 1.08 (0.89-1.32) |
| stratovolcanoes | 2.22 (1.29-3.82) | 1.08 (0.89-1.32) |
| mafic rock | 2.70 (1.23-5.93) | 1.08 (0.83-1.39) |
| intermediate rock | 1.54 (0.86-2.74) | 1.29 (1.02-1.64) |
| subduction zones | 1.88 (1.17-3.04) | 1.17 (0.98-1.40) |

Silicic, caldera, shield, rift and intraplate groups had too few informative volcanoes for the conditional model. We did these subgroup tests after the main tests. They are exploratory and are not corrected for multiple comparisons.

### 6. Forecast test (`files/figures/fig4_forecast_skill.png`, `results/forecast_scores.json`)

| model (trained 1950-1999, tested 2000-2026) | log loss | Brier |
|---|---|---|
| base rate | 0.629 | 0.218 |
| volcano history | 0.592 | 0.202 |
| history + log gap since any recorded eruption | 0.583 | 0.198 |
| history + log gap since VEI >= 2 eruption | 0.587 | 0.200 |
| log gap only | 0.617 | 0.212 |

Gain of history over base rate: 0.038 (0.006-0.069). Gain of gap over history: 0.008 (-0.004 to 0.021); 90% of bootstrap samples were positive. The gap feature is the value that a forecaster has in practice, including the record bias.

## Interpretation

The well-known association between long repose and large eruptions is mostly a property of the catalog. Old records keep only large eruptions, so large eruptions appear to follow long gaps. Inside the modern record, at the same volcano, a longer repose gives a modestly higher chance of VEI >= 3 (about 1.8 times the odds per tenfold repose). This effect is fragile to window and threshold choices, and it is absent at persistently active volcanoes. We found no support for time-predictable behaviour, also not at frequently erupting volcanoes. This disagrees with the open-conduit result of Marzocchi and Zaccarelli (2006) in this test design. After large eruptions, the next eruption tends to come slightly sooner. This agrees with short-term clustering of activity after large eruptions. It is the opposite of the pattern that a campaign study found for Cascadia tremor episodes (larger episodes were followed by longer quiet times but were not preceded by them; see citations). For forecasting, volcano history carries most of the available skill. Repose adds a small and uncertain gain.

## Limitations

* VEI is an ordinal, coarse size scale. VEI 2 is partly a default value for poorly described explosive eruptions, and GVP VEI is the maximum over an eruption episode. GVP defines eruption episodes by its own rules (for example, a gap of at least 3 months), so repose lengths depend on these rules.
* Completeness after 1950 is near constant for VEI >= 2 in global counts, but it is not proven at each volcano. Remote volcanoes can still miss VEI 2 eruptions, which makes reposes too long. The direction of the bias on the within-volcano slope is not known.
* Only 60 volcanoes have both VEI 2 and VEI >= 3 eruptions with dated reposes in the primary window. Large eruptions (VEI >= 4) are few after 1950 (65), so the tests mainly compare VEI 3 with VEI 2. We cannot say whether repose predicts VEI >= 4 or larger eruptions.
* Unknown end dates remove many 1950-1979 eruptions from repose calculations. One unknown end date removes all later preceding reposes at that volcano (a conservative rule). Imprecise start dates use mid-year or mid-month values. No next onset came before the end of the previous eruption in the time-test set, so the overlap rule did not change the results.
* The size test uses within-volcano comparisons. With few eruptions per volcano, conditional models use only volcanoes with both outcomes; results are not representative of rarely erupting volcanoes, which are the volcanoes with the largest hazard from long repose.
* We did not pre-register the tests. The primary window (1950-2026), threshold (VEI >= 2) and outcome (VEI >= 3) were set before the model fits, but the previous-size control and subgroups came after the first results.
* The WFS layers change with each GVP update. A new download can give slightly different numbers.

## Reproduction

Requirements: Python 3.12 with numpy, pandas, scipy, statsmodels and matplotlib (tested with statsmodels 0.15.0).

```
cd files/code
python retrieve_gvp.py /path/to/scratch/gvp          # writes outside the draft; reports hash match
./run_all.sh /path/to/scratch/gvp                     # analysis.py, forecast.py, figures.py
```

In the campaign workspace, `./run_all.sh` without arguments reads the shared dataset copies listed above. The full run took about 7 minutes on the loaded hp machine. Outputs: `files/results/*.csv|json` (aggregate) and `files/figures/*.png`. `build_events.py` can also write a record-level pickle to a scratch folder for inspection; that file must not be redistributed.

## Files

* `files/code/build_events.py`: cleaning, dating and event sequences.
* `files/code/analysis.py`: naive pattern, design ladder, size and time tests, subgroups.
* `files/code/cox1.py`: one-covariate stratified Cox fit.
* `files/code/forecast.py`: out-of-sample forecast test.
* `files/code/figures.py`, `files/code/run_all.sh`, `files/code/retrieve_gvp.py`.
* `files/results/`: aggregate tables (`naive_gap_by_vei.csv`, `record_rate_by_vei_era.csv`, `design_ladder.csv`, `size_predictable_tests.csv`, `time_predictable_tests.csv`, `subgroups.csv`, `within_volcano_repose_bins.csv`, `km_post_repose_by_size.csv`, `forecast_scores.json`, `summary.json`).
* `files/figures/`: four PNG figures.
* `files/EXTERNAL_DATA_NOTICE.md`: terms and attribution for the GVP data.

## References

* Global Volcanism Program. Volcanoes of the World (v. 5.3.x). Smithsonian Institution, compiled by Venzke, E. https://doi.org/10.5479/si.GVP.VOTW5-2025.5.3
* Marzocchi, W., Zaccarelli, L. (2006). A quantitative model for the time-size distribution of eruptions. JGR Solid Earth. https://doi.org/10.1029/2005JB003709
* Passarelli, L., Brodsky, E. E. (2012). The correlation between run-up and repose times of volcanic eruptions. Geophys. J. Int. https://doi.org/10.1111/j.1365-246X.2011.05298.x
* Colosi, E., Brodsky, E. E. (2022). How big will the next eruption be? J. Appl. Volcanol. https://doi.org/10.1186/s13617-022-00115-0
* Burgos, V., Jenkins, S. F., Bebbington, M., Newhall, C., et al. (2022). What is the probability of unexpected eruptions from potentially active volcanoes or regions? Bull. Volcanol. https://doi.org/10.1007/s00445-022-01605-0
* Papale, P. (2018). Global time-size distribution of volcanic eruptions on Earth. Sci. Rep. https://doi.org/10.1038/s41598-018-25286-y
* National Academies of Sciences, Engineering, and Medicine (2017). Volcanic Eruptions and Their Repose, Unrest, Precursors, and Timing. https://doi.org/10.17226/24650
* Campaign results: GVP eruption-onset seasonality (sci:sha256:17680dc4...), earthquake-eruption triggering (sci:sha256:cbe6f23c...), Cascadia tremor episode size and quiet time (sci:sha256:38bdf3cb...). Full identifiers are in `sci.json`.
