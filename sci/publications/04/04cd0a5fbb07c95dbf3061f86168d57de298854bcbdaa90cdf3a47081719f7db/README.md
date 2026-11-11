# NOAA seasonal hurricane outlook ranges stated as 70% likely contained 58% of outcomes in 2003-2025, mainly because the ranges are narrower than seasonal count noise allows

**Job:** sci-1107-dell-earth-and-ocean-sciences-969b88a28143 · **Topic:** earth-and-ocean-sciences · **Campaign:** 11_07_2026 · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Analysis date:** 2026-11-11.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

NOAA issues seasonal hurricane outlooks for the Atlantic basin (May and August) and the eastern North Pacific (May). Each outlook gives a "likely" range for the counts of named storms (NS), hurricanes (H) and major hurricanes (MH), and for the Accumulated Cyclone Energy (ACE). NOAA states that each range has a 70% probability. Each outlook also gives probabilities for an above-, near- and below-normal season. Earlier campaign work tested many operational hazard products. This seasonal product was not tested before.

We transcribed all 74 archived outlooks from 2002 to 2026 (51 Atlantic, 24 eastern Pacific) from the NOAA Climate Prediction Center (CPC) pages and Internet Archive copies. We verified them against HURDAT2. We wrote an analysis plan before we computed any score (`files/ANALYSIS_PLAN.md`).

Main results (primary sample: 2003-2025, 69 outlooks, 276 range forecasts, 46 basin-seasons):

1. **The ranges contained the outcome in 57.6% of cases** (95% season-block bootstrap interval 47.2-67.6%), not 70%. The Atlantic gave 59.8% (46.2-72.8%) and the eastern Pacific 53.3% (38.0-68.5%). ACE ranges contained only 47.8% (34.7-61.6%) in both basins.
2. **Most of the gap comes from the range widths, not from the range centres.**
   * *Count ranges.* We calculated the highest coverage that each count range can have if NOAA knew the true seasonal mean exactly ("oracle" coverage). We used a Poisson count or a count with the dispersion that we measured about perfect-knowledge sea-surface temperature (SST) predictors. The mean oracle coverage was 0.64 (Poisson) and 0.69 (measured dispersion). The observed count coverage was 0.61. In 78% of Atlantic and 70% of eastern Pacific count ranges, the Poisson oracle coverage was below 0.70. The mean range width was 1.83 Poisson standard deviations. A central 70% Poisson interval needs about 2.07. The probability of a hit increased with the standardised width (logistic slope 1.00 per standard deviation, p = 0.008).
   * *ACE ranges.* NOAA's own ACE errors have a log standard deviation of 0.48 (Atlantic) and 0.41 (eastern Pacific). The mean log half-width of the ranges was 0.29 and 0.33. With these widths, NOAA's own error spread gives an expected coverage of 45% and 58%. The observed coverage was 48% in both basins. A 70% range needs a high-to-low ratio of about 2.7 (Atlantic) and 2.4 (eastern Pacific). The issued ranges had a mean ratio of 1.8 and 2.0.
   * *Centres.* The NOAA ACE midpoints had a log error (RMSE 0.48 Atlantic, 0.41 eastern Pacific) that is equal to the error of a leave-one-out regression on the *observed* peak-season SST predictors (0.49 and 0.43). The centres are thus as good as a simple perfect-knowledge model. Better centres alone cannot remove the coverage gap.
3. **A natural experiment supports the width explanation.** After 2013, the Atlantic ranges became wider (mean standardised width 1.57 to 2.00; mean oracle coverage 0.59 to 0.71). Atlantic coverage increased from 47.7% (2003-2013) to 70.8% (2014-2025). Across the 16 basin x era x metric groups, observed coverage followed oracle coverage (r = 0.73; mean difference -0.07).
4. **Since 2014, misses have been nearly all on the high side.** In 2014-2025, 31% of all range forecasts were below the outcome (outcome above the range) and only 3.5% were above it. A calibrated central range gives 15% on each side (bootstrap interval of the difference 0.14 to 0.43; 15 seasons with net high misses against 4 with net low misses, sign test p = 0.019). Atlantic named storm counts were above the range midpoint in both eras (mean +0.47 and +0.50 Poisson standard deviations).
5. **The season-type probabilities did not show a clear miscalibration.** The ranked probability skill score against the climatology of the 20 previous seasons was +0.10 (-0.28 to +0.41) for the Atlantic and +0.22 (-0.11 to +0.47) for the eastern Pacific. The most-likely category occurred in 54% (Atlantic) and 61% (eastern Pacific) of outlooks. The mean stated probability of that category was 64% and 57%. Probabilities of 0.675 or more (mean 0.78) verified 58% of the time (39-75%, n = 26). This is a possible small overconfidence, but the interval includes the stated value.
6. **A repair with no new information.** We replaced each count range with a central 70% Poisson interval around NOAA's own midpoint. Count coverage became 76.8% and the interval score (alpha = 0.3) decreased by 6% (10.62 to 9.95). For ACE, a log-normal interval around NOAA's geometric midpoint, with a spread fitted only on earlier outlooks, gave 80% coverage. But the interval score became worse in the Atlantic (154 to 182) and better in the eastern Pacific (192 to 181). Thus wider count ranges are a clear improvement, and the correct ACE width is less certain.
7. **2026 (provisional, operational best tracks).** The Atlantic season had 10 NS, 1 H, 1 MH and ACE 20% of the median by 11 November 2026. The August ranges were 7-13, 2-6, 0-2 and 30-90%. The hurricane count and ACE were below their ranges. The eastern Pacific had 21 NS, 12 H, 10 MH and ACE 338% of the median. The May ranges were 15-22, 9-14, 5-9 and 120-190%. MH and ACE were above their ranges. These seasons are not complete and are not in the primary sample.

## Figures

* `files/figures/fig1_coverage.png`: coverage by metric and basin, with the oracle coverage for the stated widths.
* `files/figures/fig2_atlantic_timeline.png` and `files/figures/fig3_epac_timeline.png`: all ranges and outcomes.
* `files/figures/fig4_width_and_direction.png`: (a) observed coverage against oracle coverage by basin, era and metric; (b) direction of misses by era.
* `files/figures/fig5_season_type_reliability.png`: reliability of the season-type probabilities.

## Data

| Source | Use | Version / identifier |
| --- | --- | --- |
| NOAA CPC Atlantic outlook archive, `https://www.cpc.ncep.noaa.gov/products/outlooks/hurricane-archive.shtml` | 50 Atlantic outlooks 2002-2026 | pages retrieved 2026-11-11; SHA-256 in `files/data/raw_sources_sha256.txt` |
| NOAA CPC eastern Pacific outlook page, Internet Archive snapshots (`web.archive.org`, one per year, 2003-2024), live pages for 2025 and 2026 | 24 eastern Pacific outlooks | snapshot timestamps and SHA-256 in `files/data/raw_sources_sha256.txt` |
| NOAA CPC background pages (current and Internet Archive 2008, 2015) | ACE medians and season-type definitions in each era | same file |
| NHC HURDAT2 Atlantic `hurdat2-1851-2025-092326.txt` | observed 1950-2025 seasons | sha256 `75202780ce56c8458f16fbef5fb8a026b99b00878dbb95c458211b3e6ef125b4`; campaign path `datasets/nhc-hurdat2-atl-1851-2025-092326/` |
| NHC HURDAT2 NE/NC Pacific `hurdat2-nepac-1949-2025-092926.txt` | observed 1971-2025 seasons | sha256 `caece626f7038db64a803a73f5985b563693f0130f3ff16b4b0a0a93c7aa0507`; campaign path `datasets/nhc-hurdat2-nepac-1949-2025-092926/` |
| NHC ATCF operational best tracks `https://ftp.nhc.noaa.gov/atcf/btk/` | provisional 2026 totals | files and SHA-256 in `files/data/raw_sources_sha256.txt` |
| NOAA ERSST v5 `sst.mnmean.nc` (PSL) | perfect-knowledge SST predictors | sha256 `952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386`; campaign path `datasets/ersst-v5-psl-sst-mnmean-20261108-olen/` |

All sources are products of the US federal government (NOAA). See `files/NOTICE_EXTERNAL_DATA.md`. The raw pages and data files are not in this bundle. `files/code/fetch_sources.sh` downloads them into a separate scratch folder.

The transcribed outlook tables are `files/data/outlooks_atlantic.csv` and `files/data/outlooks_epac.csv`. Each row gives the issue date, the three season-type probabilities, the four ranges, the ACE median basis and value, the stated probability wording, and notes.

## Methods

**Verification quantities.** We used calendar-year totals (NOAA outlooks include off-season storms in their ranges). A named storm is a system with tropical storm, subtropical storm or hurricane status at 34 kt or more. A hurricane has hurricane status at 64 kt or more, and a major hurricane at 96 kt or more. ACE is the sum of squared 6-hourly maximum winds (00, 06, 12, 18 UTC) while the system has TS, SS or HU status at 34 kt or more, in units of 10^4 kt^2. For the eastern Pacific, we counted EP-designated systems and used all their fixes (sensitivity: fixes east of 140W only). We expressed ACE as a percent of the median that each outlook states: Atlantic 87.5 (1951-2000, used to 2010), 92.4 (1981-2010, 2011-2020), 96.7 (1951-2020, from 2021); eastern Pacific 110 (2003-2006), 109 (1971-2005, 2007-2010), 100.4 (1981-2010, 2011-2020), 97.2 (1991-2020, from 2021). The 2003-2004 eastern Pacific medians are not stated; we used the 2005 value.

**Coverage.** A range forecast is a hit when the outcome is in the closed range. We pooled metrics and outlooks and used a season-block bootstrap (10,000 resamples of years; both outlooks of an Atlantic year stay together).

**Oracle coverage.** For August outlooks we subtracted the storms that formed before the issue date from the range (NOAA ranges include them). For each remaining range [a, b] we maximised P(a <= Y <= b) over the mean of Y. Y is Poisson, or negative binomial / binomial with the variance-to-mean ratio phi from a Poisson regression of 1971-2025 counts on observed peak-season SST predictors (Atlantic: relative MDR SST and relative Nino-3.4 SST in August-October; eastern Pacific: relative Nino-3.4 SST and relative eastern Pacific SST in July-September; plus a linear trend). The measured phi was 0.95, 0.62, 0.68 (Atlantic NS, H, MH) and 0.83, 0.91, 1.21 (eastern Pacific). For ACE we used a log-normal spread equal to the leave-one-out residual of the same regression (0.47 Atlantic, 0.50 eastern Pacific).

**Season types.** We classified each observed season with the NOAA definition in force in the outlook year (ACE thresholds and count conditions from the CPC background pages; see `season_type()` in `files/code/analysis.py`). The reference forecast was the frequency of each type in the 20 previous seasons (with 0.5 added to each count). Sensitivity: the current definition for all years.

**Repair.** For counts: a central 70% Poisson interval (15% and 85% quantiles) with mean equal to the NOAA midpoint, after removal of storms already observed. For ACE: a log-normal interval around the NOAA geometric midpoint, with the root-mean-square log error of earlier outlooks of the same basin and issue month (at least 5 earlier outlooks). We compared the interval score with alpha = 0.3.

## Sensitivity checks

* Including 2002 (prototype wording): Atlantic coverage 59.7%.
* Only outlooks that state an explicit 70% (2009-2025): Atlantic 68.4%, eastern Pacific 55.9%. The Atlantic result is near nominal in this subset, because it is mostly the post-2013 period (item 3).
* Eastern Pacific ACE east of 140W only: coverage 56.5% instead of 47.8%.
* Current season-type definition for all years: RPSS against climatology +0.21 (Atlantic) and +0.15 (eastern Pacific).
* The Poisson premise: the Atlantic H and MH counts were under-dispersed about the SST predictors (phi 0.62 and 0.68). With these values the oracle coverage for H and MH is higher (0.72 and 0.75 instead of 0.61 and 0.66), and the width explanation is weaker for these two metrics. The phi estimates have a standard error of about 0.2. The predictor model is simple, so a better model could have a smaller residual. The ACE and named storm results do not depend on this premise.

## Limitations

* The sample is small: 46 basin-seasons, and the four metrics of one season are correlated. The bootstrap intervals are wide.
* We transcribed the outlooks by hand from web pages. Each value is in the CSV files with the source page hash. For 2003-2007 the ranges are called "likely" without a number; for 2008 NOAA gave 60-70% or 67%. We treated all of them as 70% ranges.
* HURDAT2 is a reanalysed record. NOAA may have verified against operational values. Small differences in ACE can change hits near range limits.
* The season-type definitions before 2011 contain words such as "well above" and "slightly above". Our coded rule is one reading of them.
* The EP perfect-knowledge model explains little ACE variance (R^2 = 0.09). The EP "centre" comparison is therefore weak.
* The 2026 results come from operational best tracks of incomplete seasons.
* Changes after the plan: the era comparison (2003-2013 against 2014-2025), the miss-direction test and the oracle with measured dispersion were added after we saw the first results. They are exploratory. In the first run, a coding error (addition of numpy booleans) stopped the "two of three counts" part of the season-type rule. We corrected the code; the rule did not change.
* We do not know the internal method that NOAA uses to set the ranges. Our attribution is statistical: it shows that the stated widths cannot give 70% under count noise at the measured level, and that coverage changed when the widths changed.

## Relation to earlier campaign work

Earlier campaign publications found specific miscalibration in public hazard products (for example NHC formation probabilities, wind speed probabilities and the Coral Reef Watch outlook). Like the Coral Reef Watch attribution, this study separates the error that the product rules cause from the error of the physical forecast. Here, the range widths alone explain most of the coverage gap.

## Reproduction

```
bash files/code/fetch_sources.sh /tmp/noaa_scratch      # downloads into scratch, never into the bundle
bash files/code/run_all.sh files /tmp/noaa_scratch      # rewrites files/results and files/figures
```

Python 3.12 with numpy, pandas, scipy, statsmodels, xarray (netCDF4) and matplotlib. Random seed 20261111. Run time is a few minutes on 2 CPUs. Live CPC pages and ATCF files can change after 2026-11-11; compare with `files/data/raw_sources_sha256.txt`.

Files:
* `files/code/`: `observed.py` (HURDAT2 totals), `btk2026.py` (2026 totals), `predictors.py` (ERSST predictors), `analysis.py` (all tests), `figures.py`, `fetch_sources.sh`, `run_all.sh`.
* `files/data/`: transcribed outlooks, raw source hashes.
* `files/results/`: `range_verification.csv` (one row per range forecast), `coverage_summary.csv`, `era_comparison.csv`, `ace_error_decomposition.csv`, `season_type_verification.csv`, `season_type_scores.csv`, `season_type_reliability.csv`, `observed_*.csv`, `predictors_ersst.csv`, `summary.json`, `analysis_stdout.txt`.
* `files/ANALYSIS_PLAN.md`: the plan written before scoring.

Related prior work outside the campaign: arXiv:2410.05503 (2024) argues that Poisson models of North Atlantic counts are near a lower bound of forecast error; Klotzbach et al. (2019, Tropical Cyclone Research and Review) review seasonal forecast skill but do not test range coverage.
