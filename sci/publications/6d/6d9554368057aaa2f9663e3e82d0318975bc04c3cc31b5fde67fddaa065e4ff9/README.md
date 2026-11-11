# Finnish moth community change was near its spatial warming benchmark in 1993-2022

Job: sci-1107-dell-climate-pollution-biodiversity-7f27be560d40. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Main result

Finnish moth community change was close to the expectation from its spatial temperature gradient. Its direct community temperature index (CTI) to air temperature trend ratio was only 0.22. However, the spatial CTI-temperature slope was only 0.214 C/C. After division by that slope, the ratio was **1.02 (95% spatial-block interval 0.86 to 1.24)**. A small direct ratio can thus occur without a large gap relative to spatial sorting. This is an independent limit on the scope of the earlier weak-transfer result. It is not proof that warming caused the observed CTI trend.

![Spatial benchmark and survey weather audit](files/result.png)

## Question and prior evidence

The campaign found weak spatial-to-temporal transfer across 75 networks. The butterfly correction also showed that thermal indices from the monitoring network itself can encode non-climatic decline. We asked whether a clear deficit remains in an independent Finnish release whose thermal indices come from European ranges. We also asked whether temperature in survey years gives the same warming benchmark as the full annual record.

Mäkinen et al. (2025, PNAS) studied thermal composition in five Finnish groups. Their public release has community means and warm- and cold-group abundances. It has no full species-by-survey table. A prior campaign audit found a species richness term in the printed thermal diversity equation. We therefore do not use the diversity index. Our mean-index analysis neither resolves that equation issue nor needs it.

Ellis et al. (2025, Nature Communications) already studied Finnish moth colonisation and extinction. Their results give a regional process context: cold-species loss in the north and warm-species entry in the south. Our new test concerns the size of the trend relative to spatial sorting, not discovery of those processes. Their moth records are not an independent replication of this release. We do not treat the studies as independent samples.

This investigation is exploratory. The first source-data fits showed a moth ratio near 0.90 and a large plant survey-temperature slope before the continuous-climate analysis was chosen. See files/PLAN.md for the decision record. We did not preregister the question.

## Data and estimands

We use version 1 of the Dryad data, dated 8 April 2025 (doi:10.5061/dryad.4j0zpc8np), and the recorded GHCN-CAMS v3.01 monthly snapshot. Exact shared paths, source URLs, byte counts and hashes are in files/provenance.json. The source release uses European thermal scores. We retain its CTI values without recalculation. We drop rows missing CTI, temperature, year, site or coordinates, and retain sites with at least two records. The retained moth data end in 2022, despite wider dates in the source description. The plant data have only three calendar years: 1985, 1995 and 2006.

We interpret the projected coordinates as ETRS-TM35FIN (EPSG:3067), based on their scale and Finnish extent. This is an explicit coordinate-system assumption. Source and GHCN survey temperatures have correlations from 0.954 to 0.984 (files/climate_alignment.csv), which supports the alignment. We convert them to longitude and latitude and select the nearest 0.5-degree GHCN-CAMS cell. Annual temperature is the day-weighted mean of the 12 monthly means. We use every year between each group's first and last survey year to estimate the cell climate mean and linear trend. Native GHCN temperatures remain in kelvin in external scratch. All centred slopes and changes are identical in degrees C.

For site i and year t, write the full temperature record as T_it = m_i + h_i t + e_it, with t centred at the middle of the group period. Fit CTI_it = site_i + c t + error by least squares. This fit weights sites by their within-site year sum of squares, not equally. Let w_it be year minus its site mean. The matching full-record temperature trend is H = sum(w_it squared times h_i) / sum(w_it squared).

For the spatial slope B, regress the site mean of CTI minus c times the site mean of t on m_i, with one equal-weight row per retained site and an intercept. This removes a common calendar trend from site means before spatial comparison. The direct ratio is c/H; the spatial benchmark ratio is R = c/(H B). It compares two descriptive gradients. B is not a causal temperature coefficient.

The survey-weather identity is exact under this decomposition: the within-site temperature slope on survey years equals H + sum(w_it times e_it)/sum(w_it squared). The second term measures how survey timing samples annual weather departures. It does not require species data. files/weather_identity.csv verifies this identity to less than 1e-15 in each group.

## Estimates

| Group | Years | Rows / sites | CTI trend, C/year | Spatial slope, C/C | Direct ratio | Spatial benchmark ratio (95% interval) |
|---|---|---:|---:|---:|---:|---:|
| moth | 1993-2022 | 2029 / 246 | 0.01256 | 0.214 | 0.218 | 1.02 (0.86 to 1.24) |
| butterfly | 1999-2020 | 1007 / 101 | 0.00324 | 0.159 | 0.060 | 0.38 (0.06 to 0.83) |
| bird | 1978-2020 | 3386 / 933 | 0.00755 | 0.402 | 0.116 | 0.29 (0.16 to 0.40) |
| plant | 1985-2006 | 3460 / 1538 | -0.00155 | 0.102 | -0.018 | -0.17 (-0.42 to 0.10) |
| plankton | 1978-2017 | 4048 / 946 | -0.00302 | 0.174 | -0.052 | -0.30 (-0.86 to 0.24) |

All intervals above resample 100 km spatial blocks, retain full site records, and repeat the CTI trend, spatial slope and ratio calculation (999 draws; seed 20261111). There are 44 moth, 22 butterfly, 52 bird, 49 plant and 44 phytoplankton blocks. Intervals condition on the observed years, fixed thermal indices and climate product. They are nominal intervals, not a multiple-test correction. We do not pool groups.

For moths, H is 0.05759 C/year. B times H is 0.01233 CTI C/year, close to the observed 0.01256. Thus the direct 22% ratio is largely the scale of the spatial thermal gradient. The original source-temperature and unadjusted spatial-mean calculation gives 0.90, also much larger than 0.12. That earlier pooled value is a reference, not a matched control or a universal null hypothesis.

Birds retain a clear point deficit after the same normalization (0.29). Butterfly uncertainty is wide. Plant and phytoplankton point trends are negative and their spatial-block intervals include zero. These data do not show that every group attains its spatial benchmark. They also do not support a single common tracking fraction.

## Robustness and uncertainty

The moth ratio is 1.019 for sites with at least a ten-year span (66 sites) and 1.023 for sites with at least five visits (160 sites). A model that includes the annual temperature residual e_it gives 1.017. The fast anomaly coefficient divided by B is 0.058, with spatial-block interval -0.004 to 0.132. A large secular ratio can coexist with a small interannual slope. These do not identify a lag time.

Excluding Epirrita autumnata in the separate source release gives c = 0.01299, B = 0.22099 and R = 1.021. This is a point check, without a new bootstrap interval. Hence that dominant cyclic species does not explain the main benchmark result.

Omitting successive five-year blocks of ecological observations gives moth ratios from 0.993 to 1.077. This sensitivity retains the original full-record climate definition. It is not an interval for all possible temporal shocks. The point estimates for north and south bioclimatic zones are 1.62 and 1.02. Those estimates have different spatial gradients and coverage, so we do not interpret their difference as a process effect. The within-zone benchmark variant is also in files/results.csv.

A separate two-way cluster calculation allows common year shocks as well as 100 km spatial dependence in the CTI trend. It gives a moth trend interval of 0.00961 to 0.01551 C/year, using a t reference with 29 degrees of freedom. It does not include uncertainty in H or B and therefore is not a ratio interval. The butterfly trend interval then includes zero. Plants have only three years; their cluster interval has two degrees of freedom and is very imprecise. Full values are in files/year_uncertainty.csv.

## Survey-year weather changes the plant denominator

In GHCN-CAMS, the plant survey-year slope is 0.2151 C/year. The matching full-record slope is 0.08776. The exact survey-weather term is +0.12737 C/year. Thus the survey-year slope is **2.45 times** the full-record slope, within the same climate product. The source temperature slope, 0.2107, is close to the GHCN survey-year slope. Product choice alone cannot explain this difference. The source mean plant-survey temperature is much colder in 1985 than in 1995. Sampling these few years overstates the continuous climate trend.

This effect does not restore plant community warming: its CTI point trend stays negative. It changes the size and meaning of the exposure benchmark. The corresponding survey/full climate ratios are 1.04 for moths, 0.98 for butterflies, 0.93 for birds and 0.95 for phytoplankton. It is a large issue here mainly for sparse plant surveys.

## What follows, and what remains open

The release adds a counterexample to uniformly weak transfer: Finnish moth CTI change is near the spatial expectation even with external European thermal scores. A universal low-response constraint is therefore not enough to explain all these observations. The method also gives an exact check for survey-weather error in sparse ecological comparisons.

We do not establish which process caused the remaining deficit in birds, plants or phytoplankton. The CTI means cannot separate colonisation, loss and abundance change. Regional moth process results from prior work are consistent with more than one route to similar community change. Faster life cycles alone are not identified as the reason for the moth contrast. Butterflies have different sites, periods and observation methods.

Spatial gradients contain habitat and geography. Annual air temperature is an imperfect exposure for insects, understorey plants and lake plankton. We did not adjust habitat, pollution, management, effort or detection. The source indices have no propagated estimation error. Light-trap activity can change abundance weights. The linear benchmark can miss nonlinear climate response. The climate trend is estimated rather than known, and the main bootstrap does not resample common years or climate reconstruction errors. A large descriptive ratio must not be read as a causal warming fraction, proof of equilibrium, or a forecast of future tracking. A small temporal slope on annual anomalies does not rule out a response to sustained warming.

## Reproduction and rights

The package has our source code, aggregate results and figure. External records and site-level derivatives remain outside it. Read files/EXTERNAL_NOTICE.md for source attribution and terms. No source licenses are replaced by the SCI baseline.

From the publication root, set SCI_REBUILD to an absolute path outside the publication and run `sh files/reproduce.sh`. The script creates an isolated environment, retrieves and verifies the two exact external inputs, extracts tables and climate into scratch, fits all models, and writes results to scratch/out. The NOAA URL is mutable. If its hash has changed, use the recorded campaign snapshot; do not accept a new file silently. For existing shared inputs, files/retrieve.py accepts --archive and --climate paths. The individual analysis commands in reproduce.sh can then use those paths. Exact hashes allow a reader to identify the required snapshots.

Compare scratch/out/results.csv, sensitivity.csv, omit_year_blocks.csv, noepi.json and weather_identity.csv with files/. The dummy-variable check in checks.json independently verifies the moth within-site trend estimator. Source retrieval with hash checks, table extraction, the weather identity and the species-exclusion fit were run locally. The main analysis ran with one numerical thread. The saved figure is static and below SCI display limits.
