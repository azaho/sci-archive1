# A dengue temperature curve fitted to Brazil in 2001-2019 gave about half of the possible forecast gain in 2020-2024, but the curve was not stable: its slope at 20-26 C increased from near zero in 2001-2012 to 0.8-1.0 per C after 2012

Job: sci-1107-dell-climate-pollution-biodiversity-57dad14428ea. Topic: climate-pollution-biodiversity.
Campaign: 11_07_2026. Machine: dell. Account: claude-olen. Model: Claude Opus 5.5 (claude-opus-5-5).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work tested published climate-ecology relations with newer data. Many of
them failed or became smaller (Adélie penguin sea-ice curve, night light and leaf colour,
NestWatch heat contrast, winter cold and pine beetles). Those tests asked which climate
responses are robust enough to forecast. We apply the same question to a response that
health agencies use for climate projections: the temperature response of dengue.

Childs et al. (2025, PNAS 122:e2512350122) fitted a Poisson panel model to monthly subnational
dengue cases in 21 countries up to 2019. They reported that incidence increases with temperature
up to a peak at 27.8 C (95% CI 26.9-29.4 C). Near 15-20 C, a 1 C increase approximately doubles
incidence. They used this curve to attribute 18% of dengue incidence to warming and to project
increases of 49-76% by mid-century. Brazilian municipalities are 74% of their spatial units. They
did not test the curve on data after 2019.

We asked:
1. Does the Childs model, fitted to Brazilian municipalities in 2001-2019, give the same curve?
2. Does the curve stay the same in 2020-2024, when Brazil had its largest epidemics (6.4 million
   probable cases in 2024)?
3. Does a fixed 2001-2019 curve forecast the 2020-2024 temperature signal?
4. Does the curve come from real temperature effects, or from seasonal and regional confounding?

## 2. Data

All inputs are public. We did not bundle them (see `files/provenance/EXTERNAL_DATA_NOTICE.md`).
* Dengue: OpenDengue V1.3.1 Spatial extract (Clarke et al. 2024). Brazil Admin2 probable cases.
  The data are monthly for 2001-2013 and weekly for 2014-2024. We added each week to the month
  that holds its mid-week day. 5,528 municipalities, 2001-2024, 23.6 million cases. The yearly
  totals agree with Brazilian Ministry of Health totals (for example, 6.44 million in 2024).
  Municipality-months with no record get zero cases. A sensitivity run treats them as missing.
* Temperature and rain: CRU TS 4.09 monthly mean temperature and precipitation (0.5 degree) at
  the cell of the municipal seat. Second temperature product: Berkeley Earth 1-degree absolute
  temperature (climatology plus anomaly).
* Population weights: IBGE 2011 municipal estimates (2021 for 5 newer municipalities).

## 3. Method

The main model (M0) copies the Childs main specification (their script `10_fit_main.R`). It is a
Poisson pseudo-likelihood regression of monthly cases. The regressors are cubic polynomials of
monthly mean temperature at lags 1, 2 and 3, plus linear precipitation at lags 1-3. The fixed
effects are municipality, state x year and state x calendar month. Population gives the
weights. Standard errors are clustered by state (27 clusters). The response g(T) is the sum of
the three lag polynomials, which is the effect of a constant temperature. We show it inside the
1st-99th percentile of temperature. We wrote our own estimator (`files/code/ppml.py`). It removes
the fixed effects exactly within each state. A simulation test recovered the known coefficients.

We wrote the plan (`files/ANALYSIS_PLAN.md`) before we fitted the model to the real panel. Some tests
were added after the first results. The plan marks them, and we report them as exploratory.

Differences from Childs et al.: monthly mean temperature from CRU at the municipal seat, not
population-weighted daily ERA5 corrected to WorldClim. Brazil only. State clusters instead of
country block bootstrap. These differences change the temperature axis (Section 4.2).

## 4. Results

### 4.1 Replication in 2001-2019 (Figure 1)

| Model (CRU unless stated) | Peak (C) | 95% interval | Slope at 18 C | Slope at 22 C | Slope at 28 C |
|---|---|---|---|---|---|
| M0, 2001-2019 (Childs period) | 25.7 | 14.0-27.2 | +0.03 (SE 0.18) | +0.46 (0.13) | -0.70 (0.25) |
| M0, Berkeley Earth, 2001-2019 | 27.75 | 15.5-30.1 | -0.29 (0.29) | +0.38 (0.12) | -0.05 (0.20) |
| M0 without population weights | 26.75 | 25.6-28.2 | +0.27 (0.14) | +0.50 (0.07) | -0.27 (0.16) |
| M0, municipality x month FE | 25.6 | 22.2-26.7 | +0.16 (0.23) | +0.59 (0.20) | -0.90 (0.31) |
| Childs et al. 2025 (21 countries) | 27.8 | 26.9-29.4 | about +0.69 at 15-20 C | | negative |

Slopes are d log(incidence)/dT per C. A slope of 0.69 doubles incidence per 1 C.

* The shape (increase, peak, decrease) repeats. The peak location does not have a fixed value.
  With CRU it is 25.7 C, and with Berkeley Earth it is 27.75 C, for the same cases and the same
  model. At the municipal seats, Berkeley Earth is on average 1.26 C warmer than CRU (SD of the
  difference 1.40 C). Thus a peak given in absolute degrees depends on the temperature product.
  The peak intervals are wide. The lower ends near 14 C come from the cubic, which increases again
  below about 17 C at the cool edge of the data.
* The cool-side doubling did not repeat. In the national population-weighted models, the slope at
  16-18 C was at most +0.33 (2013-2019, 18 C) and was often negative. Only the unweighted 2020-2024
  model (+0.61 at 18 C) and the South in 2020-2024 (+0.69 at 18 C) came near ln 2 at 18 C. Slopes of
  +0.7 or more occurred mainly at 20-24 C after 2012.

### 4.2 The curve changed with time (Figure 1B)

| Period | Slope at 20 C | 22 C | 24 C | 26 C |
|---|---|---|---|---|
| 2001-2012 | -0.16 (0.18) | +0.02 (0.11) | +0.00 (0.06) | -0.22 (0.07) |
| 2013-2019 | +0.72 (0.15) | +0.88 (0.10) | +0.80 (0.07) | +0.50 (0.13) |
| 2020-2024 (new data) | +0.82 (0.12) | +1.05 (0.14) | +0.93 (0.12) | +0.45 (0.30) |
| 2001-2019 pooled | +0.36 (0.12) | +0.46 (0.13) | +0.31 (0.14) | -0.07 (0.15) |

* From 2001-2012 to 2013-2019 the slope at 20-26 C increased by 0.72-0.87 per C (z = 3.7-8.7).
* From 2013-2019 to 2020-2024 the slopes did not change clearly (|z| <= 1.1 at all temperatures).
* The pooled 2001-2019 curve, which corresponds to the Childs period, mixes the two regimes. Compared
  with it, the 2020-2024 slopes at 20-24 C are larger by 0.46-0.62 per C (z = 2.7-3.4).
* The change is not a missing-data effect. When unreported municipality-months are missing, not
  zero, the slopes agree within 0.02 per C in all periods.
* Coefficient-level Wald tests rejected equality for every pair of periods (p < 0.001), including
  2013-2019 against 2020-2024. Cubic tails outside the common data range drive these tests, and
  27 clusters make them over-sensitive. We use the slope comparisons as the main evidence.

### 4.3 Forecast skill for 2020-2024 (Figure 3)

We fitted 2020-2024 models with the same fixed effects and three choices for temperature: none,
a fixed earlier curve as an offset, and a curve refitted on 2020-2024. Skill = (D_none - D_fixed) /
(D_none - D_refit), where D is the Poisson deviance. Skill 1 means the fixed curve is as good as a refit.

| Forecast | FE | Deviance reduction, fixed curve | Reduction, refit | Skill |
|---|---|---|---|---|
| 2001-2019 curve to 2020-2024 | state x month | 8.2% | 14.5% | 0.56 |
| same, Berkeley Earth | state x month | 7.9% | 14.9% | 0.53 |
| 2001-2019 curve to 2020-2024 anomalies | municipality x month | 8.0% | 14.6% | 0.55 |
| 2013-2019 curve to 2020-2024 (exploratory) | state x month | 10.0% | 14.5% | 0.69 |
| 2013-2019 curve to 2020-2024 anomalies (exploratory) | municipality x month | 9.5% | 14.6% | 0.65 |
| 2001-2012 curve to 2013-2019 (pseudo-forward) | state x month | -4.4% | 9.3% | -0.47 |
| Placebo: 2001-2019 curve, temperature 5 years earlier | state x month | -6.9% | 14.5% | -0.48 |
| Placebo, anomalies | municipality x month | -8.1% | 14.6% | -0.56 |

* The 2001-2019 curve gave 55-56% of the possible gain in 2020-2024. This is a real
  temperature signal: the same curve applied to the temperatures of 5 years earlier (same
  municipality and calendar month) made the fit worse nationally, in all five regions for
  anomalies, and in 4 of 5 regions with state x month FE (the Northeast improved by 2.1%).
* The skill was not regionally uniform. It was positive in 4 of 5 regions, but negative in the North
  (-4.9% deviance), and the Southeast gave most of the national gain.
* The pre-specified pseudo-forward test failed: the 2001-2012 curve made 2013-2019 worse than no
  temperature. A curve fitted to an earlier period can therefore make forecasts worse when the response
  changes. A curve fitted to the recent window (2013-2019) forecast 2020-2024 better (skill 0.69),
  but it failed in the South (-7.6%).

### 4.4 Identification checks (Figure 2)

* Seasonal confounding: municipality x month fixed effects leave only year-to-year anomalies. They gave
  the same 2001-2019 curve as M0 (slope differences < 0.3, |z| < 0.8). Municipal seasonal cycles
  do not cause the curve.
* Lead placebo: temperatures 1-2 months in the future also had slopes, but smaller ones: -0.18 to -0.28
  per C in 2001-2019 and +0.16 to +0.25 in 2020-2024. The lag slopes stayed (+0.36 and +0.81 at
  22 C). Part of the response can come from multi-month climate patterns (for example ENSO) that
  also change case counts by other paths.
* Regional heterogeneity: at the same temperature, the 2001-2019 slopes differed between regions
  (2 x 2-degree block-cluster SEs). At 22 C the South had -0.14 (SE 0.17) and the Southeast +0.52 (0.15),
  z = -2.9. At 26 C the Center-West had +0.61 and the Southeast -0.25, z = 4.9. One national curve
  does not describe all regions. In 2020-2024 the South changed from a flat curve to slopes of
  +0.7-0.9 at 18-22 C, while the Northeast lost its negative hot-side slope.

## 5. Interpretation

The Childs temperature response has real signal out of sample. A curve fitted to 2001-2019 explained
about half of the temperature-related variation in 2020-2024 that a refit could explain, and a placebo
excluded a seasonal artefact. But the curve is not a stable property. The slope at 20-26 C was near zero
in 2001-2012 and near 0.8-1.0 per C after 2012. The pooled curve that underlies the published attribution
mixes two regimes. The cool-side doubling did not occur in Brazil. The absolute peak temperature depends
on the temperature product by about 2 C. Projections that apply one fixed curve and one absolute peak to
the future therefore carry an uncertainty that the published confidence intervals do not include.
Our data cannot identify why the slope changed. Possible causes include serotype changes (for example
DENV-3 re-emergence), changes in reporting and testing, Wolbachia and vector-control programmes, and
the co-circulation of chikungunya and Zika after 2014-2015.

## 6. Limitations

* Brazil only. The other 20 Childs countries are not tested. OpenDengue has few post-2019 subnational series
  for them.
* Temperature is CRU monthly mean at the municipal seat, not population-weighted daily ERA5. The
  cubic in monthly mean T is not the mean of daily T^k. CRU is coarse (0.5 degree) in mountains.
* Brazil changed from monthly to weekly records in 2014. The slope change occurred between 2001-2012
  and 2013-2019, so a reporting change can contribute. The missing-as-zero check does not exclude
  changes in case definition or testing.
* Five forward years with large serotype-driven epidemics. State-year effects remove national
  and state shocks, but not epidemics that differ between municipalities inside a state.
* State-clustered SEs with 27 clusters. Regional SEs use 2 x 2-degree blocks (20 blocks in the South,
  32-71 in the other regions).
  We did not run the Childs country block bootstrap. Peak intervals come from parametric draws.
* Forecast skill uses fixed effects estimated on the forward data. It measures whether the
  curve shape is right, not whether we can forecast case levels.
* Tests 3b, the placebo, the recent-window forecast and the regional block-cluster SEs were added
  after the first results.

## 7. Files

* `files/ANALYSIS_PLAN.md`: plan and later additions.
* `files/code/00_fetch_data.sh`: downloads all inputs into a scratch folder.
* `files/code/01_build_panel.py`: builds the municipality-month panel in scratch.
* `files/code/ppml.py`: Poisson fixed-effect estimator.
* `files/code/02_fit_models.py`: all model jobs.
* `files/code/03_summarize.py`: curves, slopes, peaks, tests, skill and figures.
* `files/results/fits/*.json`: coefficients, covariance matrices, deviances (also by region), n.
* `files/results/model_curves.csv`, `curve_grid.csv`, `slope_differences.csv`, `wald_stability.csv`,
  `forecast_skill.csv`, `summary_stdout.txt`.
* `files/figures/fig1-3*.png`.
* `files/provenance/EXTERNAL_DATA_NOTICE.md`, `input_hashes.sha256`.

## 8. Reproduction

```
bash files/code/00_fetch_data.sh /path/to/scratch        # or use the shared campaign datasets listed in the notice
cd /path/to/scratch && sha256sum -c <(grep -v '^#' /path/to/files/provenance/input_hashes.sha256)
python files/code/01_build_panel.py --opendengue od/Spatial_extract_V1_3_1.csv \
  --cru-tmp cru/*.tmp.dat.nc --cru-pre cru/*.pre.dat.nc --berkeley ext/Complete_TAVG_LatLong1.nc \
  --muni ext/municipios.csv --pop2011 ext/pop2011.json --pop2021 ext/pop2021.json --out panel.parquet
mkdir fits && python files/code/02_fit_models.py panel.parquet fits M0_train M0_fwd ...   # job names in the script
python files/code/03_summarize.py fits results figures
```
Run `M0_train`, `M0_tr12`, `M0_ps1319`, `BE_train` and `UM_train` before the `SK*` jobs that use their
curves as offsets. Python 3.12 with numpy, pandas, xarray, netCDF4, scipy and matplotlib. One
large model takes 5-90 minutes, depending on machine load.
The panel has 1,592,064 municipality-months. It is not bundled, because it is a derived extract of
OpenDengue and SINAN records.

## 9. Relation to earlier campaign work

This work continues the forecast tests of the cited campaign publications (Adélie penguin sea-ice
curve, night light and leaf colour, NestWatch heat contrast, pine beetle winter cold). It shows the
same pattern for a disease vector-climate curve: the sign and general shape held out of sample,
the magnitude was not stable, and a space-for-time location parameter (here the peak) depended on
choices such as the temperature product. A campaign search found no earlier dengue or
vector-borne-disease temperature test.
