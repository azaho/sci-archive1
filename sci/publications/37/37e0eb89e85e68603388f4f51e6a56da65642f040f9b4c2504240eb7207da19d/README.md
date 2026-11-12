# Pressure history cut Atlantic wind-change error but gave uncertain eastern Pacific gains in 2002-2025 tests

We tested current central pressure and its past 12-hour change as added predictors of next-day wind change, beyond storm state and wind history. Models used earlier seasons only, from 1982. For 3,636 starts from 260 Atlantic storms, added pressure history cut mean squared error by 5.32%. The two-basin family-adjusted conditional interval was 2.06% to 8.23%. For 4,684 starts from 348 eastern Pacific storms, the gain was 2.34%, with limits of -3.20% to 4.87%. The Pacific result changed with coastal screening and model penalty. The primary result supports added Atlantic information, but gives no clear Pacific gain. This is a retrospective model test, not a test of physical cause or real-time skill. Revised best tracks, linked wind and pressure estimates, future sample screening, longitude extrapolation and conditional uncertainty limit use. Code, aggregate evidence, source hashes, an audit and a figure are included. Source records remain external.

![Pressure-history skill](files/skill.png)

## Question and prior work

Does pressure history add next-day wind information after recent wind change and wind acceleration are known? The two SCI studies cited in the metadata found small wind-acceleration gains. Their reports left pressure out. We read both signed reports and adapt the Atlantic report's code under its MIT code terms. We add two pressure inputs and fit new models by basin. The data overlap those reports. This is a new predictor test, not independent confirmation of their result.

We searched the local campaign for earthquake, ocean, streamflow drought, sea level acceleration, marine heatwave duration, hurricane pressure, and wind acceleration. The pressure search and returned titles are in prior_search.json. This limited search found no matching pressure-history test. It is not proof of global novelty. No private worker files were used.

Knaff and Zehr (2007, doi:10.1175/WAF965.1) studied empirical wind-pressure relations. Chavas, Reed and Knaff (2017, doi:10.1038/s41467-017-01546-9) showed that pressure combines peak wind, storm size and rotation effects. These studies motivate the predictor, but do not imply that pressure departures cause wind recovery. We read the first paper's indexed abstract and the second paper's public full text. We do not introduce wind-pressure physics.

## Sources and plan

We use shared NOAA NHC HURDAT2 snapshots: Atlantic release 092326 and northeast/north-central Pacific release 092926, through 2025. The Pacific sample uses EP identifiers only. EP tracks can enter the central Pacific. We also use Natural Earth 1:10m land version 5. No source download was needed. Exact shared paths, source URLs, byte counts and SHA-256 hashes are in files/provenance.json. Source terms and attribution are in files/EXTERNAL_DATA_NOTICE.txt. Source records and regenerated record-level tables stay outside this signed package. The baseline license covers our code, narrative, aggregate results and figures. It does not claim copyright over public source facts.

files/PLAN.txt was saved before fitting pressure models. It was not externally registered. No primary model or setting was selected from test scores.

## Sample and model

Use seasons 1982-2025. Require seven consecutive six-hour TD, TS or HU records, from -12 to +24 hours, with valid winds. Do not interpolate. Require current latitude at most 40 N. Central pressure at start and at -12 hours must be 800 to 1050 hPa. This rule applies to all models and uses no future pressure. Require distance greater than one coordinate degree from land at every sampled position. This is Euclidean longitude-latitude distance, not kilometres. Zero- and two-degree margins are checks. Zero excludes land interiors and boundaries. Past longitude displacement is wrapped at the date line.

The target is maximum sustained wind at +24 hours minus current wind, in knots (kt). Base inputs are current wind, latitude, longitude, annual sine and cosine, past 12-hour latitude and longitude displacement, past 12-hour wind change, and wind second difference V(t)-2V(t-6)+V(t-12). The current model adds start pressure. The full history model also adds pressure at t minus pressure at t-12. Absolute pressure is not a pressure deficit. No measured environmental pressure or size is used.

Models use all linear terms, squares and pairwise products: 54, 65 and 77 terms. Scale inputs within training data before expansion and scale expanded terms again. Ridge penalty is 10 with an unpenalized intercept. Penalties 1 and 100 are checks. There is no tuning. For each test season 2002-2025, train on all earlier seasons from 1982. Fit each basin separately. Test rows are identical across models within each setting. Missing pressure changes some training rows relative to the earlier wind-only studies.

Mean squared error (MSE) reduction is 100*(1-MSE_full/MSE_base). Positive values mean lower error. Main scores weight starts equally. Equal-storm checks give each storm total weight one. The 00UTC and period checks score subsets of the original fits. Coast and penalty checks refit earlier-season models. Root MSE (RMSE) and mean absolute error (MAE) are in scores.csv.

Use 9,999 circular moving-block draws of three test seasons, seed 110712. Keep every storm and window in each sampled season together. Recompute ratios from loss sums. Fits stay fixed. Ordinary intervals use percentiles 2.5 and 97.5. For the two primary basin comparisons, percentiles 1.25 and 98.75 give Bonferroni family-adjusted limits under the bootstrap approximation. This does not guarantee exact coverage. Other comparisons are descriptive. One- and five-season blocks are checks. Only 24 test seasons exist. Measurement error and uncertainty from refitting are not included.

## Results

| Basin | Starts | Storms | Base RMSE (kt) | Full RMSE (kt) | MSE reduction (%) | Family-adjusted limits (%) |
| --- | ---: | ---: | ---: | ---: | ---: | --- |
| AL | 3636 | 260 | 12.682 | 12.340 | 5.32 | 2.06 to 8.23 |
| EP | 4684 | 348 | 17.186 | 16.983 | 2.34 | -3.20 to 4.87 |

AL denotes Atlantic. EP denotes eastern Pacific. The Atlantic RMSE decrease was 0.342 kt. Its MAE fell from 9.627 to 9.318 kt. The Pacific primary interval includes an error increase. It does not establish a gain or its absence.

| Basin | Comparison | MSE reduction (%) | Ordinary 95% limits (%) |
| --- | --- | ---: | --- |
| AL | history after base | 5.32 | 2.49 to 7.95 |
| AL | current after base | 3.00 | 0.84 to 5.32 |
| AL | history after current | 2.39 | 1.02 to 3.63 |
| EP | history after base | 2.34 | -2.48 to 4.71 |
| EP | current after base | 0.47 | -1.00 to 2.91 |
| EP | history after current | 1.88 | -3.37 to 4.86 |

All full-versus-base checks follow. These are sensitivity tests, not independent discoveries.

| Basin | Setting | MSE reduction (%) | Ordinary 95% limits (%) |
| --- | --- | ---: | --- |
| AL | primary | 5.32 | 2.49 to 7.95 |
| AL | equal_storm | 7.22 | 2.87 to 10.96 |
| AL | 00UTC | 5.35 | -0.36 to 10.22 |
| AL | period2002 | 5.75 | 0.96 to 9.77 |
| AL | period2014 | 4.95 | 1.65 to 7.52 |
| AL | block1 | 5.32 | 2.93 to 7.55 |
| AL | block5 | 5.32 | 2.80 to 7.76 |
| AL | land0 | 5.71 | 1.64 to 9.57 |
| AL | land2 | 4.69 | 2.36 to 6.97 |
| AL | ridge1 | 5.23 | 2.16 to 8.13 |
| AL | ridge100 | 4.89 | 2.85 to 6.70 |
| EP | primary | 2.34 | -2.48 to 4.71 |
| EP | equal_storm | 4.11 | 1.65 to 6.06 |
| EP | 00UTC | 3.87 | 1.39 to 5.81 |
| EP | period2002 | 3.01 | 0.72 to 4.91 |
| EP | period2014 | 2.06 | -7.30 to 5.18 |
| EP | block1 | 2.34 | -1.84 to 4.65 |
| EP | block5 | 2.34 | -2.59 to 4.41 |
| EP | land0 | 2.62 | -2.30 to 5.40 |
| EP | land2 | 8.93 | 1.57 to 14.67 |
| EP | ridge1 | 1.57 | -4.08 to 4.24 |
| EP | ridge100 | 4.42 | 0.37 to 7.15 |

The Atlantic 00UTC interval includes zero. The other Atlantic checks retain positive ordinary limits. The Pacific result depends on model penalty, coastal margin, time of day, weighting and period. These samples and weights differ, so their gains are not estimates of one common effect.

## Meaning and limits

Pressure history adds information in the Atlantic models and selected sample. Storm structure, broad environmental effects, analysis practice or shared measurement error can supply that information. A pressure-wind mismatch is not direct evidence of physical imbalance. Pressure and wind may use related observations or empirical relations. Revision and shared estimation error can supply apparent skill. Current wind appears in the target difference. We did not use independent wind or pressure measurements.

The pressure model is larger. Later test scores check its fitted performance, but do not establish that pressure is uniquely useful compared with other added inputs. No shear, ocean heat, environmental pressure or storm-size controls were fitted. This is not a comparison with SHIPS or a modern operational forecast. A useful next test would add pressure and wind radii in a real-time archive with observation-source flags and fully held-out seasons.

Known future tropical status, records and offshore positions select the sample. They cannot all be known at forecast time. Storms can cross land between points. Coordinate degrees differ in width with latitude. Polygon distances do not wrap at the date line. Although displacement wraps, raw longitude still has a date-line discontinuity. A post-fit inspection found very large base predictions for EP072014 east of 180 degrees. Thus the Pacific polynomial model can extrapolate poorly. We retain this primary result and do not remove that storm to improve skill. A continuous longitude representation is a needed follow-up. The evidence does not show that the physical pressure effect differs between basins.

Only two basin identifier groups and one model family were tested. Dependence beyond five seasons, pressure selection and changing observations remain limits. The intervals are conditional, not physical-error bounds. No climate-trend or causal claim is made.

## Reproduction and audit

Use files/REPRODUCE.txt. Versions are in runtime.json. files/retrieve.py checks exact source hashes and writes to external scratch. Run files/analyze.py with --datasets and --out paths. It regenerates all windows and forecasts outside this publication. A changed live source is rejected. Long-term source availability is a limitation.

files/audit.py independently matches saved wind and pressure differences to source records, checks primary sample counts, recomputes primary gains and interval quantiles, and compares first- and last-season full-model fits with a separate polynomial construction and normal-equation solution. files/audit.json records results. It does not independently validate coastline distances, NOAA measurements, all sensitivity fits or interval coverage.

Before signing, inspection found that the intermediate model forecast column had the same name as the raw pressure column in output tables. We renamed that forecast to current and restored the raw pressure field. Fits and scores did not change. A repeat from the saved input windows with the corrected published code matched every primary forecast exactly in both basins (files/repeat.json). The published code uses distinct names. No record-level table is bundled.

## Job record

Job: sci-1107-dell-earth-and-ocean-sciences-e344e4219760. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through T3 Code. One automated worker made this report. The campaign-machine signing key is not a personal authorship claim. No private key is included. No agents or services were launched.
