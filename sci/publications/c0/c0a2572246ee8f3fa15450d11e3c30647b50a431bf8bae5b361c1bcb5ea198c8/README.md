# Oklahoma earthquake rates in 2019-2026 fell faster than injection-pressure forecasts made in 2018; lower injection explains little of the error, and rates stay 4-18 times above the 1980-2008 level

Job `sci-1107-dell-earth-and-ocean-sciences-6c4dada337a3` · topic `earth-and-ocean-sciences` · machine `dell` · model `claude-opus-5-5` (Claude Code, Anthropic) · campaign `11_07_2026` · analysis date 2026-11-08.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Wastewater injection into the Arbuckle Group caused thousands of earthquakes in Oklahoma after 2009.
Operators and the state cut injection after 2015, and the earthquake rate fell.
In 2018, Langenbruch, Weingarten and Zoback (LWZ 2018) published a physics-based forecast: about 190, 130 and 100 earthquakes of magnitude 3 or more (M≥3) in 2018, 2019 and 2020 in Oklahoma and southern Kansas, if injection stayed at the early-2018 rate.
We have eight more years of data. We used them to answer three questions:

1. Did the published forecast come true, and if not, did the lower injection after 2018 cause the difference?
2. Do simple injection-driven pressure models forecast the decline better than simple statistical decay of the recent earthquake rate? Does the answer change with the calibration date?
3. Is the 2021-2026 earthquake rate back at the pre-2009 level, and does it follow current injection near each location?

Main results:

- **Published forecast.** Observed ComCat M≥3 counts in a box that reproduces the LWZ 2015 count (947 against their 943) were 181, 57 and 34 in 2018, 2019 and 2020. The forecast was 190, 130 and 100. The 2018 value agrees. The 2019-2020 total is 40% of the forecast (91 against 230). With only Poisson error, the 2019 and 2020 counts are far below the forecast (p < 1e-6). If the forecast mean has a log-normal uncertainty of 0.5, p = 0.13 for 2019 and p = 0.07 for 2020. No M≥5 earthquake occurred in 2018-2020; LWZ gave a 58% probability of at least one, so this result does not test the forecast.
- **Injection scenario.** Reported Arbuckle injection in Oklahoma was 10% (2019) and 30% (2020) below the early-2018 rate that the forecast assumed. In our pressure models calibrated to March 2018, the early-2018 rate gives only 7% (2019) and 14% (2020) more earthquakes than the reported injection. The observed M≥2.5 counts were 28% (2019) and 20% (2020) of the reported-injection forecast. Thus the lower injection explains only a small part of the forecast error.
- **Pressure models against decay baselines.** We calibrated 24 pressure-model variants (memoryless pressure-rate response, response only above the earlier maximum pressure, delayed response, non-linear response, loss of productivity with pressure history) with data to the forecast start and selected one variant on a hold-out period inside the calibration. For forecasts from January 2017, April 2018 and July 2019, the selected pressure model was worse than an exponential decay of the recent rate in every forecast year (M≥2.5, April 2018 start: 0 of 8 years better; it forecast 5,286 events against 1,310 observed). For a forecast from January 2021, the selected pressure model was better than both decay baselines in all 6 years at M≥2.5 and M≥3 (501 forecast against 410 observed; exponential decay 253). But this forecast is almost independent of injection after 2018: with injection held at the early-2018 rate, its 2021-2026 total changes by only 2.6%. Its skill comes from a slow decay shape, not from a demonstrated response to current injection.
- **No return to background.** Oklahoma M≥2.5 counts in 2021-2025 were 125, 82, 57, 72 and 31 per year. The 1980-2008 rate in the same area was 7.1 per year, so the recent rate is 4 to 18 times higher. M≥3 counts in the LWZ box were 6 to 24 per year in 2021-2026 against about 1 per year before 2009 (LWZ 2018). LWZ 2016 expected the rate to "approach historic levels within a few years". This did not occur in 10 years.
- **Location of the residual earthquakes.** Across 0.2-degree cells, the 2021-2026 count increases strongly with the 2014-2016 count of the same cell (log-log slope 0.44-0.57, 95% intervals exclude 0). After the peak count and peak injection are held fixed, the slope on current (2020-2025) Arbuckle injection within 10, 20 or 30 km is uncertain (−0.01 to 0.40; all 95% intervals include 0). All upper 95% bounds (0.44-0.76) are below 1, so the data do not agree with a rate that is proportional to current local injection.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| OCC Form 1012A UIC injection volumes, 2006-2010 (annual) and 2011-2025 (monthly, per well) | Oklahoma Corporation Commission, `https://oklahoma.gov/content/dam/ok/en/occ/documents/og/ogdatafiles/<year>-uic-injection-volumes.xlsx` and `all-2006-2010-uic-1012a.xls`, downloaded 2026-11-08. Byte-identical copies are in the shared campaign datasets `datasets/occ-uic-injection-volumes-<year>-20261108/` and `datasets/occ-uic-1012a-volumes-2006-2010-20261108/` (SHA-256 list: `files/data/raw/occ_SHA256SUMS.txt`, check against the shared `provenance.json`: `files/data/raw/occ_shared_dataset_provenance.txt`). | Arbuckle wells (any year with "ARBUCKLE" in the formation field): 814 wells. |
| OGS earthquake catalog | Oklahoma Geological Survey, `https://ogsweb.ou.edu/eq_catalog/earthquake?start=188201010000&end=202611072359&mag=0&format=csv`, downloaded 2026-11-08 (Walter et al. 2020). Exact bytes: `files/data/raw/ogs_catalog_1882_20261107_m0.csv.gz`. | Oklahoma counts (33.6-37.0°N, 94.4-100.0°W), 1980-2026. |
| USGS ComCat | `https://earthquake.usgs.gov/fdsnws/event/1/query`, one CSV per year 2000-2026, 33.5-37.5°N, 94.4-100.5°W, M≥1.5 (URLs: `files/data/raw/comcat_query_urls.txt`). Exact bytes: `files/data/raw/comcat_ok_ks_2000_2026_M1.5.tar.gz`. | LWZ forecast check (Oklahoma and Kansas), magnitude audit. |

SHA-256 values of the OGS and ComCat files are in `files/data/raw/ogs_comcat_SHA256SUMS.txt`. The OCC 2024 file has fewer rows than the adjacent years (27 of 387 Arbuckle wells that report in 2023 and 2025 have no 2024 volume). We used the file as published.

## Methods

**Counts.** We count OGS events with magnitude (rounded to 0.1) at or above 2.0, 2.5 or 3.0 in 476 cells of 0.2° × 0.2° and in calendar months from January 2006 to October 2026. The main threshold is M≥2.5. The background rate μ is the 1980-2008 OGS rate in the study box, spread evenly over the cells (7.07 M≥2.5 events per year in total).

**Pressure.** `04_pressure.py` solves 2-D linear diffusion of pressure on a 4 km grid (explicit finite differences, zero pressure at the edges of a padded domain) with the monthly Arbuckle volume of each well as a point source. 2006-2010 annual volumes are spread evenly over the months. The hydraulic diffusivity D is 0.1, 0.3, 1, 3, 10 or 30 m²/s. Pressure is in linear arbitrary units; all models below do not change when the pressure scale changes. We average pressure over each cell. A second scenario holds each well at its mean January-March 2018 rate after March 2018 (the LWZ assumption).

**Rate models.** λ_c(t) = μ + s_c F_c(t). F is (a) the positive part of the monthly pressure change ("SI", seismogenic-index type), or (b) the increase of the running maximum of pressure ("KAISER": no events while pressure is below its earlier maximum). Options: an Omori delay kernel (τ + 1 month)^(−p) with p = 1 or 1.5; a power n = 1.5, 2 or 3 on F; a depletion factor exp(−p_max/(d·p95)) with d = 0.1, 0.3 or 1. The cell productivity s_c is a gamma-Poisson (empirical Bayes) estimate from the calibration counts. The prior shape is selected by marginal likelihood.

**Honest forecast protocol.** For each forecast start (January 2017, April 2018, July 2019, January 2021), calibration uses data from January 2010 to the month before the start. We select D, kernel, power, depletion and family on the last 24 calibration months (fit on the earlier months). Then we refit s_c on the full calibration period and forecast every month to October 2026. The reported "selected pressure model" is the variant with the best hold-out score, chosen before the forecast period was scored.

**Baselines.** PERSIST: the last 12 calibration months per cell, constant. DECAY: PERSIST times exp(−t/τ), with τ fit to the statewide counts in the 24-month hold-out window. POWERDECAY: statewide (t − t_peak + c)^(−p) from June 2015, fit on the same window, spread over cells by their last-12-month share. Score: Poisson log-likelihood of monthly cell counts in the forecast period.

**Cross-section of the residual rate.** `07_scenario_tail.py` fits a negative binomial GLM of the 2021-2026 cell count on log(2014-2016 count + 0.5), log(mean 2013-2015 injection) and log(mean 2020-2025 injection + 10⁴ bbl) for Arbuckle wells within R = 10, 20 or 30 km of the cell centre, in cells with any 2013-2015 injection. Intervals come from 2,000 bootstrap resamples of 1° spatial blocks.

**Magnitude audit.** `02_catalogs.py` matches OGS and ComCat events (20 s, 20 km). `09_mag_audit.py` reports yearly OGS-minus-Mw differences and yearly b-values.

## Results

### Published 2018 forecast (Figure 1)

| Year | Observed M≥3 (ComCat box 34-37.5°N, 96-99.5°W) | LWZ 2018 forecast | Ratio | Poisson P(N ≤ obs) | P with log-normal σ = 0.5 |
| --- | --- | --- | --- | --- | --- |
| 2018 | 181 | 190 | 0.95 | 0.27 | 0.54 |
| 2019 | 57 | 130 | 0.44 | < 1e-6 | 0.13 |
| 2020 | 34 | 100 | 0.34 | < 1e-6 | 0.07 |

Two other boxes give 2015 counts of 947 and 927 (`results/lwz_check.json`). Arbuckle injection (Oklahoma only, Figure 1a) was 450, 408 and 314 million barrels in 2018-2020 against 452 million barrels per year in the forecast assumption.

### Out-of-sample forecasts (Figures 2 and 3)

M≥2.5, annual counts (2026: January-October):

| Year | Observed | Selected pressure model, start 2018-04 (SI, D = 10 m²/s, n = 1.5) | Same, early-2018 injection | Exponential decay (τ = 20 months) | Power-law decay | Selected pressure model, start 2021-01 (KAISER, D = 10 m²/s, n = 3, depletion) | Exponential decay, start 2021-01 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2019 | 241 | 851 | 912 | 343 | 491 | – | – |
| 2020 | 145 | 740 | 844 | 189 | 372 | – | – |
| 2021 | 125 | 614 | 799 | 103 | 294 | 121 | 98 |
| 2022 | 82 | 565 | 765 | 57 | 241 | 102 | 63 |
| 2023 | 57 | 539 | 738 | 31 | 202 | 88 | 40 |
| 2024 | 72 | 481 | 714 | 17 | 173 | 76 | 26 |
| 2025 | 31 | 430 | 693 | 9 | 150 | 68 | 17 |
| 2026 | 43 | 309 | 562 | 4 | 111 | 47 | 9 |

Log-likelihood difference per forecast month, selected pressure model minus baseline (`results/score_differences.csv`):

| Forecast start | M | vs exponential decay | vs power-law decay |
| --- | --- | --- | --- |
| 2017-01 | 2.5 | −44.4 | −20.8 |
| 2018-04 | 2.0 / 2.5 / 3.0 | −41.8 / −16.0 / −3.8 | −31.8 / −15.1 / −1.8 |
| 2019-07 | 2.5 | −6.0 | −12.0 |
| 2021-01 | 2.0 / 2.5 / 3.0 | +9.0 / +7.6 / +2.6 | −1.3 / +4.6 / +2.0 |

The sign change between the 2019 and 2021 starts is the same at M≥2.5 and M≥3.0. At M≥2.0 (where the 2019 network change can affect completeness), the 2021 result is mixed. The selected pressure models become more non-linear for later calibration dates (n = 1.5 to 2 before 2019, n = 3 with depletion for 2021). No variant with a linear response was selected at any date. Even the best fits do not reproduce the 2015 peak (in-sample 2015 values of the selected M≥2.5 models are 1,200-2,300 against 3,316 observed), so a 2-D linear diffusion model with fixed cell productivities does not describe the full cycle.

### Residual rate (2021-2026)

Negative binomial slopes, 95% block-bootstrap intervals (`results/tail_regression.csv`):

| R (km) | M | Slope on current injection | Slope on 2014-2016 count | Cells / blocks |
| --- | --- | --- | --- | --- |
| 10 | 2.5 | 0.14 [−0.19, 0.60] | 0.44 [0.27, 0.87] | 121 / 13 |
| 20 | 2.5 | 0.22 [−0.33, 0.74] | 0.49 [0.39, 0.81] | 202 / 17 |
| 30 | 2.5 | 0.40 [−0.05, 0.76] | 0.53 [0.44, 0.87] | 258 / 19 |
| 10 | 3.0 | −0.01 [−0.26, 0.62] | 0.57 [0.49, 0.93] | 121 / 13 |
| 20 | 3.0 | −0.01 [−0.47, 0.60] | 0.47 [0.31, 0.82] | 202 / 17 |
| 30 | 3.0 | 0.27 [−0.07, 0.44] | 0.54 [0.40, 0.85] | 258 / 19 |

### Magnitude audit

ComCat M≥3 values in Oklahoma are OGS values in most cases (median difference 0.0 for `ml` events in every year). For M≳3.3, the OGS catalog sometimes copies the USGS Mw (most events in 2010-2014) and sometimes keeps its own ML. When OGS keeps its own ML, it is 0.2-0.3 units above Mw in 2015-2017 (`results/mag_audit_offsets.csv`). This mix affects few events at M≥2.5. The OGS b-value for M≥2.5 is 1.1-1.25 in 2014-2021 and the M≥3 fraction is 0.27-0.29 in 2014-2020, with no step at the 2019 change of the ComCat contributing network (`results/mag_audit_bvalue.csv`). A magnitude shift of 0.2 changes counts by a factor of about 1.6 (b ≈ 1.1); this is smaller than the factor 3.5-5 forecast errors in 2019-2020.

## Interpretation

The 2018-2020 decline was faster than an injection-driven pressure-rate response can give with the reported volumes, in our models and in the published LWZ 2018 model. The lower injection after 2018 was too small to explain this. Thus a process that the models do not include reduced the earthquake rate. Possible processes are a reduced hydraulic connection between the injection interval and the basement (plug-backs of the lower Arbuckle; Skoumal et al. 2024), a threshold or strongly non-linear fault response, and depletion of critically stressed faults. Our data cannot separate these: the OCC depth fields change by more than 100 ft for only 9 of 765 Arbuckle wells in 2011-2025 (`code/10_depth_check.py`, `results/depth_check.log`), so we could not test plug-backs.

After 2021 the rate decays more slowly than an exponential fit to the preceding two years. A pressure model with a non-linear, depleting response follows this slow tail, but its forecast does not depend on post-2018 injection, and the cross-section shows no clear link to current local injection. The residual earthquakes occur where the 2014-2016 earthquakes occurred. This agrees with a long-lived after-effect of the earlier pressurization, but it does not exclude a small effect of current injection (slope up to about 0.7).

For hazard: the 2021-2026 M≥2.5 rate is still 4-18 times the 1980-2008 rate, and an Mww 5.06 earthquake occurred near Prague on 3 February 2024 (ComCat ok2024cish). A forecast that extrapolates the 2016-2020 decline would give a rate that is too low after 2022.

## Limitations

- The LWZ study-area polygon is not available to us. We use a box that reproduces their 2015 count. The forecast uncertainty of LWZ 2018 is not published as a number; we show two assumed values.
- Our pressure model is 2-D, homogeneous and Oklahoma-only. It omits Kansas wells, the basement, faults, the Nemaha flow barrier, poroelastic stress and injection before 2006. It is a simple, reproducible benchmark, not a replication of the LWZ 3-D model or of Marty et al. (2025).
- Hyperparameter grids are coarse. Selection on a 24-month hold-out can favour models that fit only the last two calibration years (for example the January 2021 model under-predicts 2018 by a factor of 3 in-sample).
- Monthly cell counts are correlated in space and time. We report forecast-year counts of better scores and block-bootstrap intervals, but we did not compute formal significance for the log-likelihood differences.
- OGS magnitudes mix ML and copied Mw for larger events (see audit). ComCat changed its contributing network for Oklahoma in 2019.
- The OCC 2024 file is incomplete for some wells.

## Reproduce

`files/code/run_all.sh` lists every step. Put the 16 OCC files in `raw/occ/` (copy from the shared datasets or download; check `occ_SHA256SUMS.txt`), unpack the OGS and ComCat files from `files/data/raw/` into `raw/ogs/` and `raw/comcat/`, and run the script with Python 3.12 (pandas 2.x/3.x, numpy, scipy, statsmodels, matplotlib, python-calamine, xlrd). The full run takes about 15 minutes on one core. `files/data/derived/` holds the parsed injection table (`inj_monthly.csv.gz`, `wells.csv`), the cleaned OGS events and the cell panels; `files/results/` holds every model table, selection table and log.

## Files

- `files/code/01_parse_injection.py` … `09_mag_audit.py`, `run_all.sh`
- `files/data/raw/` – exact OGS and ComCat bytes, OCC hashes and shared-dataset provenance
- `files/data/derived/` – parsed injection, wells, OGS events, cell panels, OGS-ComCat matches
- `files/results/` – forecasts, scores, selected parameters, LWZ check, tail regression, magnitude audit, logs
- `files/figures/` – Figures 1-3

## References

- Langenbruch, C., Weingarten, M., Zoback, M. D. (2018). Physics-based forecasting of man-made earthquake hazards in Oklahoma and Kansas. Nature Communications 9, 3946. doi:10.1038/s41467-018-06167-4
- Langenbruch, C., Zoback, M. D. (2016). How will induced seismicity in Oklahoma respond to decreased saltwater injection rates? Science Advances 2, e1601542. doi:10.1126/sciadv.1601542
- Marty, S., Avouac, J.-P., Langenbruch, C., Curry, W. (2025). Coulomb stress-based forecasting of injection-induced seismicity in Oklahoma and Kansas. Earth and Planetary Science Letters 671, 119677. doi:10.1016/j.epsl.2025.119677
- Dempsey, D., Riffault, J. (2019). Response of induced seismicity to injection rate reduction. Water Resources Research. doi:10.1029/2018WR023587
- Skoumal, R. J., et al. (2024). Plug-backs and reduced injection lowered induced earthquake rates in Oklahoma. The Seismic Record (summary: https://www.seismosoc.org/news/plugged-wells-and-reduced-injection-lower-induced-earthquake-rates-in-oklahoma/)
- Walter, J. I., et al. (2020). The Oklahoma Geological Survey Statewide Seismic Network. Seismological Research Letters 91, 611-621. doi:10.1785/0220190211
