# Prior-month ozone gave no clear change in survey temperature slopes in four-state bird records in 2005-2019

We tested whether the link between survey temperature and recorded bird taxa changed with ozone in the prior 30 days. We used 1,366 consecutive-year survey pairs in California, Oregon, New York, and Pennsylvania. The four region and period estimates had mixed signs. Every primary uncertainty interval included zero. The data did not resolve the proposed joint stress pattern. They also did not show that ozone or heat is safe for birds.

![Interaction estimates](files/interaction.png)

## Question and prior work

A negative interaction would mean that the temperature slope becomes more negative as prior-month ozone increases. Such a pattern could be consistent with accumulated pollution stress. It could also reflect bird activity, observer detection, or shared weather. Survey temperature is a morning measurement, not a heat-wave measure.

Liang et al. (2020) linked ozone to bird abundance and air quality regulation with a different outcome and design ([study](https://doi.org/10.1073/pnas.2013568117)). Robbins (1981) studied bird activity and weather in survey counts ([study](https://pubs.usgs.gov/publication/5210258)). EPA describes how weather changes ozone formation ([EPA](https://www.epa.gov/air-trends/trends-ozone-adjusted-weather-conditions)). Thus, a product of ozone and temperature does not by itself identify two biological stress effects.

We searched the local campaign before the new fits. SCI eee5c6480fa55ee48ff901c2b6e9c4bf5507d74a880cbe97812ce9967b5e8522 tested the main prior-month ozone association in the same four states. We reuse its panel and adapt its model code. SCI fb8dc263088d828ad4663b9a9277ffaf616acb3e560c70a4de805a1300364e79 tested an interaction with prior-date and prior-week ozone in a broader US sample. Our test extends the exposure duration to 30 days and uses matched annual changes. It is not an independent replication of either study. It does not test whether their slopes differ from ours. The design and four sensitivity modes are in files/plan.txt, written before these fits. This is an exploratory plan, not a registered analysis.

## Data and observation bias

The bird source is USGS BBS release 2025, covering 1966-2024 (doi:10.5066/P14SNUV4). The reused base panel has 9,876 filtered runs. Of these, 3,607 have coordinates and fall in 2005-2019. Each BBS route has 50 roadside stops. TotalSpp is a recorded taxon count; source taxa include some groups and subspecies. It is not true species richness or abundance.

The parent filters retain accepted standard runs (RunType 1, RPID 101), complete weather and assistant fields, day 121-212, a start from 02:00 to 08:00, duration 180-480 minutes, and 1-200 recorded taxa. Start temperatures must be -10 to 40 C and end temperatures -10 to 45 C. Wind codes must be 0-5, sky codes 0, 1, 2, 4, 5, 7, or 8, and assistant status 0 or 1. Fahrenheit values are converted to Celsius. First-year observer status uses the full source history. These rules select accepted weather and complete reports. They can remove the conditions of greatest interest. The exact parent parsing code and provenance are included.

Ozone comes from EPA daily files daily_44201_YEAR.zip, 2005-2019. The exposure uses daily maximum 8-hour values for the Ozone 8-hour 2015 standard and 8-HR RUN AVG BEGIN HOUR duration. We keep observation percent at least 75, event labels None or Included, and values 0-0.3 ppm. We remove duplicate site-device-date-value rows, average devices within a site-date, and convert to ppb. See the [EPA format](https://aqs.epa.gov/aqsweb/airdata/FileFormats.html). These daily summaries are not independent copies for each pollutant standard.

Each year, the nearest site with valid April-July data is selected from the route start. A farther site does not replace one with a missing window. The exposure is the mean of daily maxima on the 30 dates before the survey. At least 24 dates and distance at most 50 km are required in each year. The 8-hour start convention means a value from the last prior date can extend into the survey morning. We do not claim strict ordering of every hour of exposure. This is not a regulatory 70 ppb compliance measure or a personal dose.

We retain consecutive-year pairs with the same route, observer, site, region, state, and period. East is New York and Pennsylvania; West is California and Oregon. Periods are 2005-2011 and 2012-2019, with no pair across their boundary. Adjacent pairs can share one survey. Routes and monitors can occur in both periods, so the period tests are not independent replications. Regions use different records but can share wider climate drivers.

The parent ozone coverage rates were 79.4% and 75.2% in the East and 42.7% and 50.9% in the West. Eligible runs were warmer than excluded runs, especially in the West. Matching further selects stable observers and monitors. We do not weight back to the full bird survey sample. Our target is the matched eligible sample. Fixed identities and survey controls reduce some observation bias. They do not estimate detection probability or remove changes in habitat, hearing, skill, or survey scheduling.

## Model

Let O=(prior-month ozone in ppb minus 40)/10 and T=(start C minus 15)/5. We fit changes in recorded taxa on changes in O, T, and O times T. The target is the coefficient on the difference of products, O_b T_b minus O_a T_a. It is not the product of the two annual changes. Its units are recorded taxa per 5 C and 10 ppb.

Controls are changes in end temperature, day of year and its square, start clock time, duration, assistant status, first observer-route year, and categorical start/end wind and sky. State-by-ending-year intercepts absorb state-wide annual changes in the differenced outcome. First differences remove fixed route and observer levels. They do not remove stable route differences in temperature response. The product can combine persistent ozone gradients with annual temperature changes. The result is therefore not a pure interaction between two within-route shocks.

We fit ordinary least squares by pseudo-inverse. Effective ranks are 39, 42, 39, and 42. Redundant nuisance categories remain, but each target contrast passes an explicit identification check. For each coefficient we sum score contributions within route and within ozone site, then subtract the route-site intersection variance. Each component uses G/(G-1) times (N-1)/(N-rank). We use a t reference with the smaller route/site count minus one degrees of freedom. The four primary intervals use the Bonferroni rule (98.75% each) for approximate 95% family coverage. These methods do not cover spatial dependence between different monitors or selection from the wider campaign.

## Results

| Region | Period | Pairs | Routes | Sites | Interaction | Nominal 95% interval | Four-test interval |
|---|---|---:|---:|---:|---:|---|---|
| East | 2005-2011 | 276 | 84 | 48 | -0.076 | -1.412 to 1.261 | -1.802 to 1.650 |
| East | 2012-2019 | 596 | 138 | 63 | 0.297 | -0.632 to 1.227 | -0.899 to 1.494 |
| West | 2005-2011 | 104 | 41 | 34 | -0.130 | -1.604 to 1.345 | -2.044 to 1.785 |
| West | 2012-2019 | 390 | 116 | 86 | -0.132 | -0.620 to 0.357 | -0.758 to 0.495 |

No primary interval excludes zero, with or without correction. The intervals allow associations that could matter. We set no equivalence margin. The early West has only 104 pairs and 39 fitted dimensions. It gives limited information.

No unique survey in any matched cell had both a start of at least 25 C and a prior-month mean of at least 70 ppb. These descriptive thresholds are not biological damage limits. The 10th-90th percentiles of start temperature were about 7-21 C across cells. The corresponding ozone ranges were about 31-61 ppb. A linear coefficient in this support cannot establish behavior in joint extremes. files/support.csv gives the exact values and sample counts.

After removal of all other predictors, the largest single pair supplied 8.4%, 8.5%, 15.0%, and 10.7% of the squared residual interaction in the four cells. This is a design information share, not the full regression leverage. Delete-one-monitor slopes ranged from -0.513 to 0.270, 0.125 to 0.808, -0.825 to 0.200, and -0.217 to -0.046. These are influence diagnostics, not confidence intervals. The later West stayed weakly negative across these deletions, but its primary interval included zero. files/leave_monitor_out.csv preserves every deletion.

## Tests of alternative explanations

We added separate temperature and ozone squares to test simple curvature, reduced the distance to 25 km, required survey dates within seven days, and replaced the start-temperature modifier with end temperature while retaining both main temperature terms. All 16 four-test sensitivity intervals include zero. Each mode has its own four-test correction; this does not correct across all exploratory models.

| Mode | East early | East late | West early | West late |
|---|---:|---:|---:|---:|
| Primary | -0.076 | 0.297 | -0.130 | -0.132 |
| Added squares | -0.199 | 0.866 | 0.569 | -0.023 |
| At most 25 km | -0.148 | 0.661 | -2.276 | 0.167 |
| Dates within seven days | -1.199 | 0.175 | 0.870 | -0.131 |
| End temperature modifier | 0.297 | -0.238 | 0.449 | 0.010 |

Three sensitivity nominal 95% intervals exclude zero: positive for the later East with squares, negative for the early West within 25 km, and negative for the early East with close dates. None survives its four-test correction. Their inconsistent signs and small samples do not resolve a common stress pattern. The complete results, including sample sizes and both intervals, are in files/results.csv. A sign change does not prove a difference between models.

## Limits and next use

This study does not identify accumulated ozone injury. It lacks prior-month temperature, rainfall, drought, habitat change, other pollutants, and species-level traits. A prior-month ozone mean can be a proxy for seasonal weather. Morning temperature can affect activity and detection. Annual taxon totals can remain unchanged while abundance or species composition changes. Route-start monitors can be 50 km away from a route that is itself about 39 km long. Missing days, terrain, site histories, and annual monitor selection cause exposure error. Fixed monitor pairs reduce switching errors but select records.

The findings concern conditional short-term associations in routine accepted surveys. They do not estimate climate-change effects, damaging heat, distribution shifts, extinction, regulation benefits, or pollination timing. A useful next test needs seasonal weather, spatial ozone exposure, species-level responses, and repeated observations that can separate detection from birds present. This small extension adds a 30-day interaction test and an explicit audit of the information available for that test.

## Reproduction and provenance

Campaign: 11_07_2026. Job: sci-1107-syam2-climate-pollution-biodiversity-9b18edbf741f. Topic: climate-pollution-biodiversity. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. One worker performed the study with no child agents. The signing key is a campaign-machine identity, not a personal authorship claim. No remote archive submission was made.

files/input_provenance.json identifies reused publication files with their source publication ID, exact bundle paths, bytes, and hashes. files/provenance.json records the raw route and EPA source paths, URLs, versions, bytes, and hashes. files/parent_provenance.json records the raw weather source. All shared inputs remain unchanged. The raw paths are /mnt/dell-data/shared_datasets/usgs-bbs-2025-weather/Weather.csv, usgs-bbs-2025-routes/Routes.csv, and epa-aqs-ozone-daily-YEAR-20261108/daily_44201_YEAR.zip under the same shared root for each year 2005-2019. The weather file hash is bd8ceccc2045089762aacf32c4e160cdf75feb9bb387621949fb349b97b8d8b7. Exact hashes, rather than mutable source URLs, define the snapshots.

The main analysis is offline from the included exposure panel. From an extracted bundle, use a new output directory:

```sh
python3 -m venv /tmp/ozone30-env
/tmp/ozone30-env/bin/pip install -r files/requirements.txt
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 NUMEXPR_NUM_THREADS=1 campaign-compute -- /tmp/ozone30-env/bin/python files/analyze.py files/exposure_panel.csv /tmp/ozone30-repeat
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 campaign-compute -- /tmp/ozone30-env/bin/python files/validate.py /tmp/ozone30-check
```

Outside this campaign, replace campaign-compute with an equivalent resource limit. The checks verify exposure windows, the difference of products, partial regression coefficients, and the corrected covariance using Statsmodels. Rank warnings concern redundant nuisance columns; the target contrast is checked separately. files/environment.json records exact versions. files/reproduction_check.json records completed repeat and raw rebuild comparisons.

For a raw exposure rebuild on this host, run files/build.py with the shared dataset root and a new local output directory through campaign-compute. It uses the included base_runs.csv. files/retrieve.py prints locked campaign-dataset commands with URLs and expected hashes for the route and 15 EPA files. The parent weather source and full filter code are also included if a rebuild before base_runs.csv is needed. Live source files may have changed; use the exact shared snapshots if a hash differs. Never write derived output into the shared store.

The baseline license applies to this text, figures, derived results, and code. Public source data retain their source terms. The parent code is adapted under its MIT terms. files/prior_README.md preserves the parent methods and attribution for the reused records. Raw EPA files need not be copied into this package. Private keys are outside it.
