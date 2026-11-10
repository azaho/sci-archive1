# Standard ETAS aftershock tails overpredicted Oklahoma M3+ earthquakes in 2019-2026 by about 4 times; an Omori law with a 1.4-2.2 year exponential taper contained the observed counts

Job `sci-1107-dell-earth-and-ocean-sciences-95fd999b6ec5` · topic `earth-and-ocean-sciences` · machine `dell` · account `claude-olen` · model `claude-opus-5-5` (Claude Code, Anthropic) · campaign `11_07_2026` · analysis date 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Two earlier campaign studies (sci:c0a25722, sci:d6c0ec4f) found that Oklahoma earthquake rates fell faster after the 2015-2016 disposal cuts than injection-pressure models predicted. They also found that the rate in 2021-2026 stays 4-18 times above the 1980-2008 rate, and that the residual events occur where the 2014-2016 events occurred. Those studies did not separate earthquakes that injection caused directly from earthquakes that earlier earthquakes triggered (aftershocks and their descendants).

We asked: **is the 2021-2026 residual seismicity an aftershock tail of the 2010-2020 earthquakes, or an independent rate that injection still drives? And which description gives correct forecasts after injection is reduced?**

We fit a space-time ETAS (epidemic-type aftershock sequence) model with a time-varying background to the Oklahoma Geological Survey (OGS) catalog, 2010-01-01 to 2026-11-07, M>=3.0 (3,045 events; main analysis) and M>=2.5 (10,855 events). The background rate (independent events) changes every quarter, and its map changes with time. We then made honest forecasts from 2019-07-01 and 2021-01-01 with models that we fit only to earlier data.

Main results (M>=3.0 unless stated):

1. **Standard ETAS forecasts failed by a factor of about 4.** The standard model (Omori-Utsu decay (t+c)^-p, fitted p = 0.98-1.00) fit to 2010-2020 forecast 391 events (95% simulation range 273-521) in 2021-01 to 2026-11 from the cascade of earlier events alone. Only 102 events occurred. Fit to 2010 to mid-2019, it forecast 704 (536-926) events for 2019-07 to 2026-11; 179 occurred. With any of the three scenarios that add new independent events, the forecasts were 424-1,516 events. These forecasts were worse than a simple exponential decay of the recent rate (cell log-likelihood -490 to -499 against -434 from 2021; -1,045 to -1,610 against -797 from 2019).
2. **The data themselves reject the long Omori tail.** In the standard model fit to all data (2010-2026), the model expects 104 direct aftershocks in 2021-2026 from events before 2021. The same fit assigns only 35 of the 102 observed events to such parents. Synthetic catalogs simulated from this fitted model contain 253-319 events in 2021-2026, against 102 observed.
3. **A tapered Omori law (t+c)^-p exp(-t/tau) is strongly supported.** One extra parameter increased the log-likelihood by 103 at M>=3.0 and by 421 at M>=2.5. The taper time tau was 515 days (fit to 2021), 525 days (fit to mid-2019), 794 days (fit to 2026) at M>=3.0, and 628 days at M>=2.5, thus 1.4-2.2 years. A productivity that changes with the time of the parent event (5 epochs) increased the log-likelihood by only 18, and by 19 more when we added it to the tapered model. With the taper, the 10-year branching ratio still decreased from 0.76 (parents in 2014-2016) to 0.43 (parents in 2021-2026).
4. **The tapered model gave correct out-of-sample forecasts.** With a background rate that decays (exponential fit to the last 8 fitted quarters, floor at the 1980-2008 rate), the tapered model fit to 2010-2020 forecast 59 events (22-137) for 2021-2026 against 102 observed. Fit to 2010 to mid-2019, it forecast 157 (85-257) against 179. Both 95% ranges contain the observed totals. The tapered model had the best cell log-likelihood of all tested models (-321 against -434 for exponential decay from 2021; -627 against -797 from 2019). Its forecasts are low in 2023-2024 (for example 6.9 forecast against 24 observed in 2024, a year with an Mw 5.1 earthquake near Prague).
5. **About half of the 2021-2026 events descend from earlier earthquakes, and the independent rate is still above the 1980-2008 level.** In the tapered model fit to 2010-2026, 53 of the 102 events in 2021-2026 have a root (independent) ancestor before 2021, and 25 events are independent. This gives an independent rate of 4.2 per year, 2.8 times the 1980-2008 rate of all M>=3.0 events in the same box (1.52 per year). Our synthetic test shows that the method gives 1.5-2 times too many independent events and too few old roots in the late period (38 against 19, and 40 against 26, true independent events). The true independent rate can thus be lower, near 1.4-2.8 times the 1980-2008 rate. The 1980-2008 rate includes aftershocks, so the true ratio for independent events can also be higher.
6. **Near three of the four largest 2011-2016 earthquakes, the late activity is less than a pure Omori tail.** Within 10 km of the Fairview 2016 M5.1, Pawnee 2016 M5.8 and Cushing 2016 M5.0 earthquakes, 13, 7 and 2 M>=2.5 events occurred in 2021-2026. An Omori law fit to all post-mainshock events predicts 46, 19 and 7. Near Prague (2011 M5.7), 33 events occurred against 2-5 from the Omori law; 25 of the 33 occurred after the 2024-02-03 M5.1 earthquake. Disposal within 30 km of Prague is still 27-40 million bbl per year (2021-2025), and near Pawnee it fell to 5-10 million bbl per year.
7. **The independent rate follows disposal with short memory.** A fit of the annual independent rate to exponentially weighted disposal volume is best for a memory time of 0.25-0.5 years, with a steep power law (exponent about 4 for Arbuckle-labelled volume, about 8 for all disposal). The fit has a scatter of about a factor of 2 (17 years).

Interpretation. In Oklahoma, earthquake triggering after the disposal cuts did not continue with the stationary Omori-Utsu decay that the 2010-2020 sequences suggested. Aftershock tails stopped after about 1.4-2.2 years, and the triggering productivity decreased. This agrees with the observation by Goebel et al. (2019) that some Oklahoma sequences had few aftershocks when injection was reduced, and with the expectation from rate-and-state friction that a stress decrease (here a pore-pressure decrease) shortens the response. A standard ETAS model therefore overestimates the hazard after injection stops, and it misattributes the slow late decline to a long aftershock tail. The residual rate in 2021-2026 is a combination of (a) tapered aftershocks of the 2014-2020 activity and of new events, and (b) an independent rate that is still above the 1980-2008 level and that follows the remaining disposal with a short delay.

## Question and scope

- Region: OGS events inside the box 33.6-37.0 N, 100.0-94.4 W (the box of sci:c0a25722). Events before 2010 (from 2006) act only as triggers.
- Time: 2010-01-01 to 2026-11-07, in days.
- Magnitudes: OGS magnitude rounded to 0.1. Main threshold M>=3.0 (lower bin edge 2.95); secondary M>=2.5.
- Replication catalog: USGS ComCat (M>=3.0), same box and period.

## Data

| Input | Source and version | How we got it | Use |
| --- | --- | --- | --- |
| OGS earthquake catalog (Walter et al. 2020) | `https://ogsweb.ou.edu/eq_catalog/earthquake?start=188201010000&end=202611072359&mag=0&format=csv`, downloaded 2026-11-08 by sci:c0a25722 | byte-exact copy `files/data/raw/ogs_catalog_1882_20261107_m0.csv.gz` in sci:c0a25722 (SHA-256 `8051c55a66d49fe1b49b2d2e06a9cceb2ba2e56a4645d56cf8dd5d81f70d7711`) | main catalog |
| USGS ComCat | `https://earthquake.usgs.gov/fdsnws/event/1/query`, one CSV per year 2000-2026, 33.5-37.5 N, 103.2-94.2 W, M>=2.0, retrieved 2026-11-08 by sci:d6c0ec4f | `files/data/comcat_ok_region_m2_2000_2026_raw.tar.gz` in sci:d6c0ec4f (SHA-256 `047371829d44c722184030bc8eabb09acbe00a0be4e41d7a6154b5af5f53f410`) | replication |
| OCC Form 1012A disposal volumes (Oklahoma Corporation Commission) | `https://oklahoma.gov/occ/divisions/oil-gas/oil-gas-data.html`, files of 2026-11-08 | parsed tables `files/data/occ_disposal_wells_monthly_2011_2025.parquet` (SHA-256 `076cc91d031509907fc402aa14a48bafdbef95981cc75b8682b0785160aaf863`) and `occ_disposal_wells_annual_2006_2010.parquet` (`d9bd8933aa740cd9c60aeb72f5e7e85134b476f27f12a281579ffdc2ab8cc442`) in sci:d6c0ec4f; raw OCC files: `https://oklahoma.gov/content/dam/ok/en/occ/documents/og/ogdatafiles/<year>-uic-injection-volumes.xlsx` and `all-2006-2010-uic-1012a.xls` (SHA-256 list in sci:c0a25722, `files/data/raw/occ_SHA256SUMS.txt`) | disposal volumes |

This bundle contains no record-level catalog or well data. It contains only our code, aggregate results (annual and quarterly counts, model parameters, cell-year forecast totals, regional annual volumes) and figures. See `files/EXTERNAL_DATA_NOTICE.md` for the terms and attribution of the external data. `files/code/00_get_data.sh` retrieves the inputs into a separate scratch folder.

## Methods

**ETAS model** (`files/code/etas.py`). For a target event at time t and position x:

lambda(t, x) = nu(t) u(x, t) + sum over earlier events i of K_i exp(alpha (m_i - Mc)) (t - t_i + c)^-p exp(-(t - t_i)/tau) f(|x - x_i|; m_i)

- f is a power-law spatial kernel (q - 1)/(pi s^2) (1 + r^2/s^2)^-q with s^2 = D^2 exp(gamma (m - Mc)), truncated at 50 km.
- nu(t) is constant in each quarter (91.3 days). u(x, t) is a leave-one-out kernel density of the background probabilities of the other events. It is Gaussian in space, with an adaptive bandwidth (distance to the 5th neighbour, at least 2 km), and has Gaussian time weights (sigma 180 days).
- Standard model: tau = infinity and one K. Tapered model: tau is a free parameter. Epoch model: K_i depends on the year of the parent event (edges 2014, 2017, 2019, 2021).
- The Omori kernel is not normalised, so p < 1 is allowed.

**Estimation.** EM (stochastic declustering, Zhuang et al. 2002; Veen and Schoenberg 2008). The E-step computes the probability P_ij that event j was triggered by event i, and the background probability phi_j. The M-step updates nu in closed form, recomputes u, and maximises the expected log-likelihood for (alpha, c, p, tau) with K profiled, and for (D, gamma, q). Pair sums use fine logarithmic bins of time and distance. Pairs with P_ij < 1e-7 are dropped after iterations 4 and 12 (dropped probability mass: 0.01 events at M>=3.0, 0.12 at M>=2.5). We stop when no parameter changes by more than 0.02% between iterations (about 15-40 iterations).

**Ancestry.** For each event, the probability that its root (independent) ancestor falls in a period follows from A_j = phi_j e(t_j) + sum_i P_ij A_i (`ancestry` in `etas.py`).

**Forecasts** (`03_forecast.py`). We fit the model to data before the start F only. Then we simulated 500 catalogs from F to 2026-11-07 with all earlier events as parents, with magnitudes from a Gutenberg-Richter law (fitted b, maximum 6.0). Background scenarios after F:
- *inherited*: no new independent events;
- *floor*: the 1980-2008 OGS rate of the box;
- *persist*: the mean rate of the last 4 fitted quarters;
- *decay*: an exponential fit to the last 8 fitted quarters, with the floor as lower limit.

The comparison model *DECAY_CELL* is the last-12-month count per 0.2-degree cell times exp(-t/T), with T fit to the monthly counts of the 24 months before F, plus the 1980-2008 rate spread evenly over the cells. We score Poisson log-likelihoods of the observed counts in 476 cells x calendar years. Mean simulated counts are the cell rates (floor 1e-4).

**Model-light check** (`04_sequences.py`). M>=2.5 events within 10 km and 20 km of the four largest 2011-2016 events. Omori-Utsu plus constant rate, fit to year 1 or to all years after the mainshock (p in 0.3-3, c in 1e-4 to 30 days).

**Disposal** (`05_injection.py`). Quarterly volumes of wells with a 2D* well type (all disposal) and of wells with ARBUCKLE in the formation field in any year. Monthly rows with zero volume, volume above 5 million bbl, or invalid year are removed. The annual independent rate is fit as mu0 + A V_L^n, where V_L is the exponentially weighted past volume with memory time L, in log space.

**Synthetic test** (`06_synthetic.py`). We simulated two catalogs from the standard M>=3.0 model with its fitted background, then refit them with the standard and the tapered model.

## Results tables

M>=3.0 model fits, 2010-2026 (`files/results/summary_fits.csv`):

| Model | log-likelihood | p | c (days) | tau (days) | alpha | 10-year branching ratio | independent fraction |
| --- | --- | --- | --- | --- | --- | --- | --- |
| standard | -22,824.9 | 1.039 | 0.018 | none | 1.34 | 0.69 | 0.33 |
| p fixed 0.95 | -22,875.8 | 0.95 | 0.005 | none | 1.33 | 0.70 | 0.32 |
| p fixed 1.2 | -22,907.9 | 1.20 | 0.106 | none | 1.36 | 0.67 | 0.35 |
| monthly background, 90-day kernel | -22,831.6 | 1.028 | 0.016 | none | 1.31 | 0.70 | 0.31 |
| productivity by epoch | -22,806.9 | 1.040 | 0.018 | none | 1.37 | 0.62, 0.74, 0.62, 0.50, 0.40 | 0.33 |
| tapered | -22,722.1 | 0.898 | 0.004 | 794 | 1.32 | 0.71 | 0.31 |
| tapered + epoch | -22,703.0 | 0.897 | 0.004 | 790 | 1.35 | 0.63, 0.76, 0.63, 0.52, 0.43 | 0.31 |
| ComCat, standard | -22,838.0 (other data) | 1.046 | 0.021 | none | 1.27 | 0.68 | 0.33 |

At M>=2.5: standard -66,686.5 (p = 1.081); tapered -66,265.1 (p = 0.917, tau = 628 days).

The monthly-background variant has a lower log-likelihood than the quarterly one, although it has more parameters. The kernel background estimate is not a maximum-likelihood estimate, so log-likelihoods of different background settings are only approximately comparable. The triggering-model comparisons use the same background settings.

In-sample consistency for 2021-01 to 2026-11 (`files/results/tail_consistency.csv`):

| Fit | Expected direct aftershocks of pre-2021 events | EM-attributed | Observed events |
| --- | --- | --- | --- |
| standard, M>=3.0 | 103.6 | 35.2 | 102 |
| tapered, M>=3.0 | 20.3 | 28.7 | 102 |
| standard, M>=2.5 | 325.4 | 113.7 | 413 |
| tapered, M>=2.5 | 47.3 | 81.3 | 413 |

Out-of-sample forecasts, M>=3.0 (`files/results/summary_forecasts.csv`; 95% ranges from 500 simulations):

| Start | Model | Background scenario | Forecast | 95% range | Observed | Cell log-likelihood |
| --- | --- | --- | --- | --- | --- | --- |
| 2019-07-01 | standard | inherited only | 704 | 536-926 | 179 | -1,090.5 |
| 2019-07-01 | standard | decay | 773 | 572-997 | 179 | -1,045.2 |
| 2019-07-01 | tapered | inherited only | 83 | 30-170 | 179 | -862.8 |
| 2019-07-01 | tapered | decay | 157 | 85-257 | 179 | **-626.6** |
| 2019-07-01 | tapered | floor | 119 | 55-227 | 179 | -745.8 |
| 2019-07-01 | exponential decay (no ETAS) | - | 178 | - | 179 | -797.2 |
| 2021-01-01 | standard | inherited only | 391 | 273-521 | 102 | -499.1 |
| 2021-01-01 | standard | decay | 424 | 310-588 | 102 | -493.9 |
| 2021-01-01 | productivity by epoch | decay | 265 | 207-335 | 102 | -399.0 |
| 2021-01-01 | tapered | inherited only | 33 | 8-94 | 102 | -397.6 |
| 2021-01-01 | tapered | decay | 59 | 22-137 | 102 | **-320.9** |
| 2021-01-01 | tapered | floor | 57 | 21-128 | 102 | -331.4 |
| 2021-01-01 | tapered | persist | 184 | 103-302 | 102 | -353.2 |
| 2021-01-01 | exponential decay (no ETAS) | - | 84 | - | 102 | -433.9 |

The exponential-decay comparison model gave a nearly correct statewide total from 2019 (178 against 179). It has a worse cell log-likelihood because it puts the events in the cells that were active in the last 12 months.

Synthetic recovery (`files/results/synthetic/`), true values from the standard M>=3.0 fit:

| Seed | Fit | p (true 1.039) | K (true 0.0338) | tau | independent fraction (true) | old-root events in 2021-2026 (true) | independent events in 2021-2026 (true) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | standard | 1.058 | 0.0334 | - | 0.372 (0.346) | 161 (227) | 38 (19) |
| 11 | tapered | 1.056 | 0.0333 | 100,000 (upper bound; no taper) | 0.371 (0.346) | 162 (227) | 38 (19) |
| 12 | tapered | 1.055 | 0.0342 | 100,000 (upper bound; no taper) | 0.344 (0.313) | 217 (270) | 40 (26) |

The estimator did not find a false taper. It recovered the triggering parameters within 2% (p) and 3% (K and alpha). It gave too many independent events and too few old-root events in the late period.

Mainshock neighbourhoods, M>=2.5 within 10 km, 2021-01 to 2026-11 (`files/results/sequences/`):

| Mainshock | Observed | Omori term, fit to year 1 | Omori term, fit to all years | Disposal within 30 km, 2021-2025 (million bbl/yr) |
| --- | --- | --- | --- | --- |
| Prague 2011 M5.7 | 33 (8 before the 2024 M5.1) | 2.1 | 5.3 | 27-40 (2011: 115) |
| Fairview 2016 M5.1 | 13 | 39.8 | 46.2 | 20-22 (2016: 55) |
| Pawnee 2016 M5.8 | 7 | 23.3 | 18.6 | 5-10 (2014: 55) |
| Cushing 2016 M5.0 | 2 | 0.0 | 7.0 | 33-52 (2015: 109) |

In the tapered model, the 2024-02-03 Prague M5.1 earthquake has a background probability below 0.01. It is a triggered event, and its root ancestor is from 2021 or later with probability 0.93 (standard model: 0.71; root before 2016: 0.29).

## Figures

- `files/figures/fig1_decomposition.png`: annual M>=3.0 counts, separated into independent events and triggered events by the period of their root ancestor (tapered and standard models).
- `files/figures/fig2_background_vs_injection.png`: Oklahoma disposal volume and the annual independent and total M>=3.0 rate.
- `files/figures/fig3_mainshock_tails.png`: observed 2021-2026 events near the four largest 2011-2016 earthquakes against Omori-law extrapolations.
- `files/figures/fig4_forecasts.png`: out-of-sample annual forecasts from 2019-07 and 2021-01.
- `files/figures/fig5_model_likelihoods.png`: log-likelihood of model variants relative to the standard ETAS model.

## Limitations

- **The taper is a post-hoc model.** We added it after the standard forecasts failed. Its forecasts are honest (we fit it only to data before each start), but we chose the model form after we saw the 2021-2026 data. Only two forecast starts are tested, and they overlap in time.
- **The taper is a description, not a mechanism.** An exponential taper with tau = 1.4-2.2 years and a decreasing productivity are two possible forms. Other forms (a pressure-dependent productivity, a rate-and-state response to the pressure decrease) can fit equally well. We did not test them.
- **The background is flexible.** It changes every quarter, and its map changes on a 180-day scale. The split between independent and triggered events depends on this choice. In the synthetic test the method gave 1.5-2 times too many independent events in 2021-2026.
- **Forecast background scenarios are simple.** The best forecasts used a background that decays, with a floor at the 1980-2008 rate. Such a background cannot predict a local increase, for example the 2024 Prague sequence.
- **Magnitudes.** OGS magnitudes mix ML and copied Mw for larger events (sci:c0a25722). The b-value at M>=3.0 is 1.32 and at M>=2.5 is 1.15. This difference can come from the magnitude mix. We fit alpha and b separately for each threshold.
- **Region edges.** The model ignores triggering across the box edges (Kansas, Texas) and the loss of aftershocks outside the box. Events in Kansas are not in the OGS box.
- **Spatial cutoff and pruning.** Triggering beyond 50 km is not allowed.
- **Disposal fit.** The fit uses 17 annual values and statewide volumes. The steep exponents can also come from changes in the location and depth of injection, which we did not model.
- **Compute.** The host was heavily shared during this work. We used M>=3.0 for most variants because M>=2.5 fits took several hours each. We did not run M>=2.5 forecasts. We stopped three M>=2.5 fits (forecast windows and a flexible background) before convergence and do not report them. A first run of the M>=3.0 forecasts used the M>=2.5 1980-2008 rate as the floor by mistake; we corrected the floor and reran all forecasts. Only the corrected results are in this bundle.

## Reproduce

Requirements: Python 3.12 with numpy, scipy, pandas, matplotlib, pyarrow (versions in `files/code/environment.txt`) and the `sci` command (to extract the inputs from the parent publications).

1. `sh files/code/00_get_data.sh SCRATCH CAMPAIGN_DIR` extracts the byte-exact inputs from sci:c0a25722 and sci:d6c0ec4f into SCRATCH and prints their SHA-256 values. Compare them with `files/data_provenance/input_sha256.txt`. If the parent bundles are not available, the script downloads from OGS and ComCat; these files can differ from the archived bytes.
2. `sh files/code/run_all.sh SCRATCH RESULT CAMPAIGN_DIR` runs every step: catalogs (`01`), ETAS fits (`02`), forecasts (`03`), mainshock tails (`04`), disposal (`05`), synthetic tests (`06`), collection (`08`), tail check (`10`), summaries (`09`) and figures (`07`). Run it from a folder that contains `code/` (a copy of `files/code/`). Each M>=3.0 fit takes about 20 CPU-minutes, and each M>=2.5 fit takes 1-3 CPU-hours. Forecasts use fixed random seeds.
3. Record-level outputs (event tables, per-event probabilities `events.npz`) go to SCRATCH only.

## Files

- `files/code/`: all code (`etas.py` model, `00`-`10` steps, `run_all.sh`, `environment.txt`).
- `files/results/fits/<name>/`: `params.json` (parameters, likelihood, branching ratios), `nu.csv` (quarterly background rate), `annual.csv` (annual counts, independent and triggered sums, ancestry sums).
- `files/results/forecasts/<name>/`: annual forecast means and 95% ranges, scores, settings.
- `files/results/summary_fits.csv`, `summary_forecasts.csv`, `tail_consistency.csv`, `pre2009_rates.json`.
- `files/results/sequences/`, `files/results/injection/`, `files/results/synthetic/`, `files/results/logs/`.
- `files/data_provenance/input_sha256.txt`: SHA-256 values of the inputs.
- `files/EXTERNAL_DATA_NOTICE.md`: terms and attribution of external data.

## References

- Goebel, T. H. W., Rosson, Z., Brodsky, E. E., Walter, J. I. (2019). Aftershock deficiency of induced earthquake sequences during rapid mitigation efforts in Oklahoma. Earth and Planetary Science Letters 522, 135-143. (author copy: https://www.jakewalter.net/papers/Goebeletal2019.pdf)
- Langenbruch, C., Weingarten, M., Zoback, M. D. (2018). Physics-based forecasting of man-made earthquake hazards in Oklahoma and Kansas. Nature Communications 9, 3946. doi:10.1038/s41467-018-06167-4
- Langenbruch, C., Zoback, M. D. (2016). How will induced seismicity in Oklahoma respond to decreased saltwater injection rates? Science Advances 2, e1601542. doi:10.1126/sciadv.1601542
- Llenos, A. L., Michael, A. J. (2013). Modeling earthquake rate changes in Oklahoma and Arkansas: possible signatures of induced seismicity. Bulletin of the Seismological Society of America. https://pubs.usgs.gov/publication/70048493
- Ogata, Y. (1998). Space-time point-process models for earthquake occurrences. Annals of the Institute of Statistical Mathematics 50, 379-402. doi:10.1023/A:1003403601725
- Zhuang, J., Ogata, Y., Vere-Jones, D. (2002). Stochastic declustering of space-time earthquake occurrences. Journal of the American Statistical Association 97, 369-380. doi:10.1198/016214502760046925
- Veen, A., Schoenberg, F. P. (2008). Estimation of space-time branching process models in seismology using an EM-type algorithm. Journal of the American Statistical Association 103, 614-624. doi:10.1198/016214508000000148
- Dieterich, J. (1994). A constitutive law for rate of earthquake production and its application to earthquake clustering. Journal of Geophysical Research 99, 2601-2618. doi:10.1029/93JB02581
- Walter, J. I., et al. (2020). The Oklahoma Geological Survey Statewide Seismic Network. Seismological Research Letters 91, 611-621. doi:10.1785/0220190211
- Campaign publications: sci:sha256:c0a2572246ee8f3fa15450d11e3c30647b50a431bf8bae5b361c1bcb5ea198c8 and sci:sha256:d6c0ec4f174b1330bc04ff13b32b6747e594058c722d3ada3a7a4f9069c8d5e6.
