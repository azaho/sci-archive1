# Temperature relations fitted before 2005 forecast 2005-2024 Swiss spring plant dates well, British butterfly flight dates weakly, and British butterfly population growth no better than shuffled climate

Job `sci-1107-dell-climate-pollution-biodiversity-c9ac9894281a`, topic climate-pollution-biodiversity,
campaign 11_07_2026, machine dell, account claude-olen, model Claude Opus 5.5 (`claude-opus-5-5`).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign studies found that four published climate- and pollution-ecology relations
failed or became smaller in newer data: the Adélie penguin sea-ice curve, the delay of autumn
leaf colour by night light, a NestWatch heat contrast, and winter cold against mountain pine
beetle growth (cited below). These were single tests. They do not tell which *kinds* of
ecological climate response are robust enough to forecast.

We asked: **if we fit a climate-response relation on old years only, freeze it, and forecast
later years, which response types give real forecast skill?** We used one protocol for all
response types. The same protocol was applied to the same butterfly species at the same sites
for two response types (flight timing and population growth). This removes most differences of
taxon, observer, site and climate data between the compared response types.

## 2. Data

| System | Response | Units | Records used (train / test) | Years |
|---|---|---|---|---|
| MeteoSwiss phenology network | day of year of 50% event, spring (median before day 182) | 19 phases | 72,770 / 37,384 station-years | 1951-2024 |
| MeteoSwiss | summer-autumn events (leaf colour, leaf fall, fruit, vintage, late flowering) | 8 phases | 24,843 / 12,666 | 1951-2024 |
| MeteoSwiss | start of hay harvest (managed) | 1 | 4,446 / 2,045 | 1951-2024 |
| UK Butterfly Monitoring Scheme 2024 | mean flight date per site and year | 43 species | 109,718 / 127,402 site-years | 1976-2024 |
| UKBMS 2024 | population growth r = ln N(t) - ln N(t-1) from site indices | 37 species | 88,218 / 54,616 site-year pairs | 1976-2024 |

Climate: E-OBS v32.0e daily mean temperature and v31.0e daily precipitation (0.25 degree), as
monthly means of the grid cell of each site. Great Britain only (Northern Ireland sites use a
different grid and were removed). Units need at least 200 records in each period; sites need at
least 3 (timing) or 5 (growth) training records.

## 3. Method (one protocol for all units)

1. **Split.** Main split: training years up to 2004, test years 2005-2024 (20 years).
   Second split: training up to 1994, test 1995-2024.
2. **Select one climate window in training years only.** Candidates are mean temperatures of
   1-3 consecutive months. For timing, the window starts in the previous November or later and
   ends no later than the training median month of the event (33 or fewer candidates). For
   growth, the window can be in the previous year (January-December) or the current year
   (January-September), for temperature or rain (120 candidates). We keep the window with the
   largest within-site R² in training. This copies common practice ("sliding window" climate
   searches).
3. **Fit within-site relations in training years.** Timing: y = a_site + b·X. Growth: r = a_site +
   d·ln N(t-1) + β·X (Gompertz density dependence). We also fitted pre-set models without window
   search: timing with the 3 months before the median event month; growth with five fixed terms
   (previous June-August temperature and rain, December-February, March-May and June-July
   temperature), similar to Roy et al. (2001).
4. **Freeze and forecast.** In test years, the forecast uses training site means, training
   coefficients and the observed test-year climate. Growth forecasts are one year ahead and use the
   observed N(t-1).
5. **Baselines with no climate.** Timing: the training site mean (climatology), and also the
   training within-site linear trend. Growth: the same Gompertz model without the climate term.
6. **Score.** For each test year we take the mean over sites of the observed anomaly o (observed
   minus no-climate baseline) and of the forecast anomaly p. The year-level skill score is
   SS = 1 - Σ(o - p)² / Σo². SS > 0 means that the climate term made the forecast better. 95%
   intervals come from a bootstrap of test years (2,000 draws). We also report site-level skill,
   skill against the trend baseline, the correlation of detrended o and p (interannual tracking),
   the ratio of test-period slope to training slope with the same window, and a decomposition of
   the error into a mean shift part and an interannual part.
7. **Shuffled-climate null.** For each unit we repeated steps 2-6 ten times with the climate years
   shuffled (the same shuffle for all sites; 1976-2024 or 1951-2024). This gives the training |t|
   and the forward skill that the window search gives with no real climate signal.

The training |t| is from a regression of year means of within-site anomalies. It counts years,
not site-years, so it is not inflated by shared year effects.

## 4. Results

### 4.1 A clear order of forecast skill (main split, Fig. 1)

| Response class | n | Median SS (year) | Mean SS (95% CI over units) | SS > 0 | SS CI above 0 | SS vs trend baseline > 0 | Median detrended r | Median test/train slope |
|---|---|---|---|---|---|---|---|---|
| Plant spring timing | 19 | 0.82 | 0.80 (0.76 to 0.84) | 19/19 | 19/19 | 19/19 | 0.90 | 0.92 |
| Plant summer-autumn timing | 8 | 0.59 | 0.57 (0.41 to 0.73) | 8/8 | 6/8 | 7/8 | 0.67 | 0.80 |
| Hay harvest start | 1 | 0.92 | - | 1/1 | 1/1 | 1/1 | 0.93 | 1.03 |
| Butterfly flight timing | 43 | 0.21 | 0.16 (0.09 to 0.22) | 36/43 | 8/43 | 26/43 | 0.51 | 0.75 |
| Butterfly growth, selected window | 37 | -0.15 | -0.15 (-0.25 to -0.04) | 15/37 | 2/37 | - | 0.23 | 0.40 |
| Butterfly growth, fixed 5 terms | 37 | -0.18 | -0.22 (-0.33 to -0.11) | 7/37 | 0/37 | - | 0.31 | 0.20 |

![Forward skill by response class](files/figures/fig1_forward_skill_by_class.png)

The second split (training up to 1994, test 1995-2024) gave the same order: plant spring mean SS
0.80 (0.75 to 0.84), plant summer-autumn 0.41, butterfly timing 0.19 (0.05 to 0.30), butterfly
growth -0.51 (-0.81 to -0.24) with the selected window and -0.46 with the fixed five terms
(`files/results/class_summary_train1994.csv`).

### 4.2 Butterfly growth forecasts were not better than shuffled-climate forecasts

| Response class | Training median abs(t): observed / null | Units with abs(t) above null 95th pct | Mean forward SS: observed / null | One-sided Mann-Whitney p (observed > null) |
|---|---|---|---|---|
| Plant spring timing | 12.1 / 1.6 | 19/19 | 0.80 / -0.05 | < 0.001 |
| Plant summer-autumn timing | 7.0 / 1.8 | 8/8 | 0.57 / -0.12 | < 0.001 |
| Butterfly flight timing | 2.7 / 1.4 | 21/43 | 0.16 / -0.14 | < 0.001 |
| Butterfly growth | 3.1 / 2.2 | 13/37 | -0.15 / -0.20 | 0.085 |

The window search alone gave butterfly growth a median training |t| of 2.2 with shuffled
climate. This is mainly an effect of the search over 120 candidate windows. Most "significant" weather windows for
growth were within the range that the search gives by chance. Growth units that passed the null
threshold in training were not more often skilful in test years (5/13 against 10/24 that did not
pass). The test slope kept the training sign in 84% of growth units, but its median size was 0.40
of the training slope, and only 24% had a test |t| above 2 with the same sign.

![Training evidence against forward skill](files/figures/fig3_training_evidence_vs_skill.png)

Across all 107 main units, the median forward skill was 0.11, 0.06, 0.21 and 0.78 for training
|t| bins of 0-2, 2-4, 4-6 and above 6 (`skill_by_training_t_bin_train2004.csv`). All 33 units
with a year-level training |t| of 5 or more had positive forward skill (19 plant spring phases, 6
plant summer-autumn phases, 7 butterfly timing species and 1 growth species, Polyommatus icarus,
SS 0.07). Below |t| = 5, 45 of 74 units had positive skill, and for growth only 14 of 36. Skill
above 0.5 occurred only in plant phases, all with |t| above 6.

![Slope stability](files/figures/fig2_slope_stability.png)

### 4.3 Butterfly timing: interannual tracking is real, but the 2005-2024 advance is mostly not forecast

In test years, butterfly mean flight dates were a median 4.3 days earlier than the training site
means. The frozen temperature relations forecast only 0.5 days of this (pooled 16% of the shift).
The trend baseline forecast 4.4 days. The forecast error was negative (observed earlier than
forecast) for 42 of 43 species (sign test p < 0.001). The year-to-year variation was tracked
(median detrended r 0.51). For Swiss spring plants, the frozen relations forecast 76% of the
observed shift (median observed -7.1 days, forecast -4.9 days). But the plant residual also grew
more negative with time (median -1.4 days per decade, 18 of 19 phases). Thus both systems
advanced more than their interannual temperature sensitivity predicted; the shortfall was much
larger for butterflies.

![Level and interannual parts](files/figures/fig5_level_vs_interannual.png)

The unexplained butterfly advance differed by life-cycle class (Kruskal-Wallis p = 0.006). It was
largest in species with hibernating adults or immigrants (median -6.9 days: small tortoiseshell
-13.7, peacock -7.6, painted lady -7.3, red admiral -6.5, clouded yellow -6.4). For these species
the mean flight date mixes post-hibernation, immigrant and summer generations. A change in the
mix (for example more red admirals that overwinter in Britain) can move the mean date without a
temperature-sensitivity change. The unexplained advance was not related to the species' change in
abundance (Spearman 0.07, p = 0.65). Univoltine species had a median error of -3.2 days.

![Example series](files/figures/fig4_example_series.png)

### 4.4 Window search helped timing but did not help growth

Pre-set windows gave lower timing skill than the selected windows (plant spring 0.65 against 0.80;
butterfly timing 0.07 against 0.16; `figS1`). Thus the timing signal is real and the search found
better windows. For growth, the fixed five-term model was also worse than the no-climate
baseline (mean SS -0.22, 0 of 37 units with an interval above 0).

![Selected against fixed windows](files/figures/figS1_selected_vs_fixed_window.png)

## 5. Interpretation

* Direct temperature control of development (plant spring phases, and to a smaller degree
  butterfly emergence) is a forecastable climate response. Its slope was stable across periods
  (test/train 0.92 for plant spring phases), and it beat both climatology and a trend
  extrapolation in every spring phase.
* Year-to-year butterfly population growth is not forecastable from monthly weather with this
  kind of model, even though the training fits look "significant". The training evidence was
  mostly the result of the window search. This agrees with the earlier campaign forecast
  failures for demographic responses (penguin colony growth, nest success, beetle outbreak
  growth) and with a campaign ridge-model test of British butterfly indices (cited).
* Even a robust timing relation does not forecast the full later shift. Butterflies advanced
  about 4 days more than their temperature sensitivity predicts. Forecasts of phenology change
  that use only interannual temperature sensitivity will be too small for these species.
* A practical rule from these data: a training-period climate slope needs a year-level |t| well
  above the shuffled-climate null of its own window search (here 5 or more) before it is
  likely to forecast. This threshold is empirical, from 107 units in two schemes; it is not a
  general constant.

## 6. Limitations

* The comparison of response types is also a comparison of data quality. Swiss phenology
  observers record one fixed event at one station. UKBMS mean flight date and site indices come
  from weekly transect counts and depend on abundance and weather on visit days. Part of the
  difference between plants and butterflies can come from measurement noise, not biology. The
  within-UKBMS contrast (same species, sites and climate) does not have this problem.
* Linear window models only. We did not test thermal-time, state-space or mechanistic population
  models. Such models can do better; our result applies to the common linear-window practice.
* Growth forecasts use the Gompertz model with site intercepts. This model is biased in short
  series, but the climate and no-climate models share the bias.
* E-OBS grid-cell means are not site temperatures. Station density in E-OBS changes in time. This
  can add trends to the temperature, and it can explain part of the drift in the residuals.
* The shuffled null has 10 draws per unit, which is enough for class-level comparisons but not
  for exact per-unit p-values.
* Test years 2005-2024 contain only 20 year-level points per unit; per-unit intervals are wide.
* MeteoSwiss files are updated in place by the provider. A later download can give slightly
  different numbers.
* Life-cycle classes were coded by hand.

## 7. Relation to earlier work in this campaign

| Earlier result (cited) | Response type | Outcome in newer data |
|---|---|---|
| Adélie penguin sea-ice optimum curve | colony growth (demographic) | no forecast better than no change after 2017 |
| Night light and autumn leaf colour | timing, non-climate driver | delay removed by site and observer controls |
| NestWatch farmland-forest heat contrast | nest success (demographic) | contrast reversed in 2021-2025 |
| Winter cold and mountain pine beetle | outbreak growth (demographic) | no effect |
| Leaf-out sensitivity, Fu et al. 2015 test | timing | constant thermal time explains change; held to 2023 |
| Butterfly indices, ridge model | growth (demographic) | weather raised forecast error in 2010-2024 |
| Cold winters and resident birds | count change (demographic) | replicated; a direct-mortality counterexample |

Our test adds a controlled comparison inside one scheme and a selection-aware null. The order
"plant timing > butterfly timing > butterfly growth" holds with the same species, sites, climate
data and model-search effort.

## 8. Reproduction

* `files/code/run_all.sh <scratch>` runs everything. `00_retrieve.sh` downloads the source files into
  `<scratch>/raw` and checks SHA-256 values. Python 3.12 with numpy, pandas, pyarrow, netCDF4,
  pyproj, scipy and matplotlib.
* Steps: `01_extract_eobs_monthly.py` (monthly E-OBS fields for UK and Swiss boxes),
  `02_prepare.py` (site tables, grid-cell mapping), `02b_voltinism.py` (life-cycle classes),
  `03_forecast.py` (selection, fit, frozen forecast, bootstrap, shuffled null),
  `04_summarise.py`, `05_diagnostics.py`, `06_null_comparison.py` (tables and figures).
* In this campaign the source files came from the shared store (`datasets/<name>`); the exact
  names, source URLs and hashes are in `files/provenance/provenance_used.txt`.
* Random seed 20261110 (forecast and null), 7 (class bootstrap).
* Run time on the campaign machine (heavily shared): about 1 hour for extraction and 1 hour for
  the null.

## 9. Files

* `files/results/units_train2004.csv`, `units_train1994.csv`: one row per unit and model, with window,
  slopes, t values, skill scores and intervals.
* `files/results/year_series_*.csv`: year means of observed and forecast anomalies per unit (test years).
* `files/results/perm_null_train2004.csv`: shuffled-climate null fits.
* `files/results/class_summary_*.csv`, `null_summary_*.csv`, `null_comparison_*.csv`,
  `level_decomposition_*.csv`, `level_summary_*.csv`, `butterfly_bias_tests_*.csv`,
  `skill_by_training_t_bin_*.csv`, `life_cycle_classes.csv`.
* `files/figures/*.png`, `files/code/*`, `files/provenance/provenance_used.txt`.
* `files/EXTERNAL_DATA_NOTICE.md`: source data, licences and required attributions. The source data
  are not in this publication.

## 10. Data attribution

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly
Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint
Nature Conservation Committee (Open Government Licence v3). Source: MeteoSwiss. We acknowledge the
E-OBS dataset from the EU-FP6 project UERRA and the Copernicus Climate Change Service, and the data
providers in the ECA&D project (https://www.ecad.eu). See `files/EXTERNAL_DATA_NOTICE.md`.
