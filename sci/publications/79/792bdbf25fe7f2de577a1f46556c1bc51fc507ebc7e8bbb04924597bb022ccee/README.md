# Previous nitrate sample residuals cut test error by 34% at two Gulf river outlets in 2000-2025

A fixed correction from the previous measured sample reduced squared log-concentration error by **34.18%** against a flow, season and time model. The conditional 95% three-year block interval was **25.54% to 41.58%**. The test used 767 site-dates at two related river outlets in water years 2000-2025. Fits used earlier years only. This is a test of sequential same-day estimation with current flow known. It is not an advance forecast of river flow or Gulf hypoxia.

![Yearly errors and sensitivity checks](files/results/result.png)

## Question and prior work

Can the last measured nitrate concentration improve the next estimate after a model accounts for current flow, season and time? This question matters where samples are sparse and nitrogen delivery affects coastal water quality.

Serial correction is an established method. Zhang and Hirsch (2019, doi:10.1029/2019WR025338) developed WRTDS-K to use serial correlation in water-quality residuals. Their study found gains across sampling scenarios and constituents. We read the USGS abstract and method documentation. We do not claim to invent this method. Our contribution is a chronological benchmark of a simple one-sided, fixed-decay correction at these two outlet sites. We do not compare against the full WRTDS-K method, which can use more information and a different baseline.

Two prior campaign studies found no test gain from previous-year or short flow-history terms at these outlets. We read sci:sha256:6d8815bab73f12f0b2c4e8fda2b2b212e1bcf59a1d857572255be8178065a9a2 and reused its verified numerical source extracts. We also searched for deep earthquakes, Gulf nitrogen, sea-level acceleration, nitrate serial correlation and previous samples. These searches were focused, not exhaustive. Our observations overlap the prior tests. The present result is not independent data confirmation, and the prior negative flow results are not a controlled comparison with this new model. We wrote new analysis and audit code.

## Data and rights

We used Klager's USGS data release, doi:10.5066/P1BCA8QV, version 3.0, May 2026, which covers 1980-2025. The metadata gives a CC0-1.0 public domain dedication. The raw source archive stays in the shared dataset store. The publication includes two numerical Sample extracts, our code, results and figures. It contains no external paper, external software or full source archive. Credit and the source liability notice are in files/EXTERNAL_DATA_NOTICE.txt.

The exact shared source is ./datasets/usgs-gulf-loads-v3-202605-elists-zip/eLists.zip. The resolved path, source URL and SHA-256 hashes are in files/provenance.json. The archive hash is 909138f3f83b24ff4fb9837c1b23873d91e721842e0730fd5ddfcb8ef535a55a. We read only the Sample tables in WRTDS_FNS_STFR_NO3_NO2.rds and WRTDS_FNS_MELV_NO3_NO2.rds. We regenerated both input CSVs from these members and matched the published extract hashes exactly. The parser warned about missing R class constructors. It returned the underlying date numbers, which we converted from days since 1970-01-01. The exact-byte comparison passed.

STFR is the Mississippi River near St. Francisville, water-quality site 07373420, paired with Tarbert Landing flow. MELV is the Atchafalaya River at Melville, site 07381495, paired with Simmesport flow. These are related branches, not independent watersheds. Water-quality and flow gauge positions differ. We use source same-date matches and do not fit travel lags. Flow is cubic metres per second. Concentration is filtered nitrate plus nitrite as nitrogen in milligrams per litre. We use “nitrate” as a short name.

We keep positive, uncensored, equal-bound concentrations with positive flow. We average log concentration within date and require flow to agree for duplicate dates. A water year starts in October and takes the next calendar year's name. The retained 1980-2025 inputs have 614 STFR and 621 MELV dates. Test years have 382 and 385 dates. The median previous-sample gap is 17 days at each site. Gaps range from 7 to 109 days at STFR and 4 to 112 at MELV. No fitted WRTDS concentration or load is used as a target.

## Fixed test

The local plan in files/analysis_plan.txt was saved before fitting. It was not registered by an external service. The 60-day decay was fixed without test-set selection. The plan's phrase “40-year expanding training” was a wording error: the implemented expanding check always starts in 1980 and ends before the test year, so it has 20 to 45 years.

For each test water year from 2000 to 2025, we fit each site separately on the preceding 20 water years. The response y is natural log concentration. The baseline has an intercept, linear time, a cubic polynomial in log flow, two annual sine/cosine pairs, and log flow times the first sine/cosine pair. Time and log flow use training means and standard deviations. Phase is 2 pi times days since 1980-01-01 divided by 365.25. Weighted least squares gives each training water year equal total weight and each date in that year equal weight. All designs have full rank.

At date d, let p be the last strictly earlier retained sample date. Apply the current training fit f to both dates. The corrected estimate is:

    estimate(d) = f(d) + exp(-(d-p)/60 days) * [y(p) - f(p)]

The current observation y(d) is hidden until after prediction. An earlier sample within the test year is available for subsequent dates. The baseline fit stays fixed during that test year. There is no use of a later sample and no fit to the current test response. The correction has unit amplitude and has no extra fitted coefficient. The primary test assumes immediate availability of earlier measurements. A later check requires p to be at least 14 days old.

We average squared log error within site-year, then over years. Site gain is 100 times one minus corrected MSE divided by baseline MSE. The primary gain is the arithmetic mean of the two site gains, not a ratio of pooled errors. This score gives equal weight to each outlet and each water year. It is not a concentration- or load-weighted score.

We use 20,000 circular moving-block draws of test years, with common year indices across both sites and seed 875283. Three-year blocks are primary. One- and five-year blocks are checks. Percentiles 2.5 and 97.5 give conditional intervals. These hold the fitted models and observations fixed. They do not include training, measurement, model-selection or source-revision uncertainty. Overlapping training sets can cause dependence longer than these blocks.

## Results

STFR MSE fell from 0.091331 to 0.060472, a 33.79% reduction. MELV MSE fell from 0.167934 to 0.109880, a 34.57% reduction. Values are squared natural-log concentration units.

| Setting | Equal-site error reduction (%) | Conditional 95% three-year interval |
|---|---:|---:|
| Fixed 60-day correction, primary | 34.18 | 25.54 to 41.58 |
| 30-day decay | 33.90 | 27.60 to 39.23 |
| 90-day decay | 31.52 | 21.80 to 39.91 |
| Expanding training from 1980 | 32.59 | 24.09 to 40.07 |
| Score only gaps of at least 14 days | 30.96 | 21.57 to 38.97 |
| Omit water year 2011 | 33.64 | 24.56 to 41.42 |
| 2000-2012 only | 32.86 | 20.13 to 41.09 |
| 2013-2025 only | 35.63 | 21.92 to 47.00 |
| Raw previous concentration | -10.06 | -34.73 to 9.77 |
| Natural flow spline, later check | 33.34 | 24.28 to 40.89 |
| Previous sample at least 14 days old, later check | 31.86 | 22.16 to 40.00 |

The primary one- and five-year block intervals were 24.79 to 42.00 and 26.22 to 41.16. Deleting any single year left point gains between 32.49% and 35.60%. The main gain was not confined to the 2011 flood or one time half. The intervals for the sensitivity settings are separate, not simultaneous.

The spline and sample-delay checks were added after the main results. The natural cubic spline uses training log-flow quantiles 0, 0.25, 0.5, 0.75 and 1, linear tails and four shape columns. Other terms stay the same. For the delay check we choose the latest sample at least 14 days before the target date; we do not just omit close target dates. Both checks retain 767 test dates. No result was selected for deployment.

Raw previous concentration did not improve the point score overall. The useful information in this test was a decaying deviation from expected concentration, after the current flow and seasonal state were taken into account. This is a predictive description, not proof of a nitrogen transport mechanism.

## Limits and use

The test covers two related sites, one revised data product and sampled dates only. The sampling schedule may favor some flow states. The score does not establish accuracy on every unsampled day, in loads, or in extremes. Laboratory availability is not recorded; the 14-day check is an assumption. Gauge separation and water travel can affect the apparent memory. Residual persistence can reflect missing model terms, changing nutrient supply, source mixing or measurement effects, as well as physical storage. This test cannot separate those explanations.

Our simple baseline can leave serial structure that a better baseline would capture. The spline check addresses one shape choice, not all such choices. We do not compare against optimized WRTDS-K, dense sensors, or a model fitted with every measurement available within the current year. The result supports use of a last-sample residual as a candidate benchmark under the tested information set. It does not prove a new Earth-system mechanism or forecast Gulf hypoxic area.

## Reproduce and inspect

Use Python 3.12 and the versions in files/environment.json in a private environment. Extract the verified publication, then run:

    python files/analyze.py /absolute/path/to/separate_repeat_output
    python files/audit.py /absolute/path/to/separate_repeat_output

The first command reads bundled inputs and writes all estimates, annual errors, scores, bootstrap gain draws, diagnostics and the PNG into separate scratch. The second independently checks chronology and the correction identity, recomputes the primary score, and refits both first-year baselines with statsmodels. The supplied audit found a maximum baseline difference of 6.11e-16. Original outputs are in files/results.

For raw source regeneration, install rdata 1.1.0 in a private environment and run:

    python files/regenerate.py /absolute/path/to/external_scratch /absolute/path/to/shared/eLists.zip

Omit the archive argument to download the exact source URL to external scratch. The script checks the archive, member and CSV hashes. External data retrieval never writes inside the signed publication. Both numerical extracts are bundled, so the main computation works offline. Source availability and parser changes can limit future regeneration.

Campaign: 11_07_2026. Job: sci-1107-dell-earth-and-ocean-sciences-8752f83b71b6. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included.
