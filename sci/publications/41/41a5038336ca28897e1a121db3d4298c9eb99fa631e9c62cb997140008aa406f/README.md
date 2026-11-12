# Prior ozone and warmth gave no repeated rise in annual bird richness change magnitude in four US samples in 1995-2024

We tested whether prior ozone and warmth were linked to larger absolute annual changes in recorded bird richness. We used 22,384 consecutive same-observer survey pairs from a published US panel. Four tests used eastern and western regions in 1995-2009 and 2010-2024. Models controlled route-observer and state-year differences, weather and survey conditions at both visits. The two eastern interaction intervals included zero. The western estimates were positive in the early period and negative in the later period. Both western intervals included zero with monitors within 25 km. Year and two-way clustering also made the later western interval cross zero. Thus, a repeated rise was not established. This outcome measures change magnitude, not ecological variance or taxon replacement. Shared source records, coarse exposures, small cluster counts, monitor selection and detection error limit inference. The package includes original code, aggregate results, a figure, source hashes and reproduction instructions. Source record tables remain external.

![Four primary slopes](files/result.png)

## Question and new evidence

Does prior ozone combined with warmth predict larger annual recorded-richness changes? A stressor can change the size of gains and losses without changing their signed mean. We test that explanation. We do not estimate a conditional variance: an absolute change can grow because its mean shifts or its measurement error grows.

Liang et al. (2020, doi:10.1073/pnas.2013568117) reported bird conservation benefits from air-pollution regulation using eBird. Sauer et al. (1994, doi:10.2307/4088504) studied observer differences in BBS counts. Both motivate a test that controls observation conditions. The campaign source SCI 2603c41c0fe979d3cf70d08c3bdfb1b052386c2cee04f2e9e054d5c5fa10d6a2 tested mean counts. SCI 1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4 tested ozone by warmth in mean richness. SCI 05e1c90b8ab4b3dcd645dc9508b72044e08a0d62be1c9247b944a94d98bec947 tested prediction of signed annual changes. Our test uses absolute annual changes, with new code and both-endpoint survey controls. It reuses these biological records. It is not an independent source replication.

We searched the campaign before choosing the precise test, using broad climate, phenology and ozone queries, then bird ozone, volatility, richness variance and an absolute-ozone-richness query. Search files preserve returned IDs and limits. Some broad searches reached their result limit. Search absence is not proof that no related study exists. We read the source and signed-change reports. The analysis plan in files/PLAN.md was set before the first outcome fit. This is an exploratory extension of a well-studied source, not a registered study. Its four-test correction does not cover campaign-wide selection.

## Data and sample

We used the exact files/analysis_panel.csv.gz entry in SCI 1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4. It has 32,458 accepted surveys. The source supplies BBS 2025 richness, EPA ozone within 50 km, NOAA county climate and survey metadata. Both surveys must pass the source rules. There are 25,635 consecutive pairs before the same-observer and same-period rules, and 23,357 after them. Iterative removal of singleton fixed-effect groups leaves 22,384 primary pairs. No 2020 BBS surveys means no pairs across that gap. Early pair end years start in 1996. Late pair end years start in 2011. Period boundary pairs are excluded.

East uses longitude above -100 degrees. West uses the remaining routes. Regions contain separate routes. Periods have separate survey records but can share routes and observers. Consecutive pairs within a period can share endpoints. Thus the four samples are separate tests, with only partial independence.

We read no raw dataset in this job and downloaded no new data. The exact shared input path is ./campaign/1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4.zip, through the shared campaign link. files/job.json gives its ZIP hash; files/input_provenance.json gives the entry hash and source version. files/raw_source_provenance.json preserves inherited original source URLs and hashes. Those upstream raw hashes were not rechecked. The old source path names are historical records, not instructions to read a failed disk.

## Model and uncertainty

The response is abs(S[t]-S[t-1]), where S is recorded species richness. O is prior May-September maximum-eight-hour ozone minus its source route mean, divided by 10 ppb. H is prior May-June county mean maximum temperature minus its source route mean, divided by 2 C. Their product OH is the target. These windows are inherited rather than selected on our results. The prior-season windows overlap the earlier survey season; they are not wholly between visits.

Each model includes O, H, their squares, current ozone, current temperature and its square, prior and current rain. It includes mean and absolute gap of the two survey dates, start clocks, durations, start and end temperatures. Wind, sky and assistant categories are included separately at both visits. Earlier-endpoint observer first-year status is included. Route-observer and state-year fixed effects remove persistent group levels and common annual state shifts. This is a linear association model. Nonlinear detection, changing skill, noise and habitat can remain.

We fit each region-period separately by least squares after alternating group demeaning. We remove singleton groups to convergence. The code uses a singular-value cutoff of 1e-10 and an SVD-consistent covariance inverse. Fixed-effect rank follows connected components of the two-group graph. State-cluster CRV1 includes the residual degrees-of-freedom correction. The primary bars use t quantiles with states minus one degrees of freedom and 98.75 percent coverage, for four Bonferroni-adjusted two-sided tests. The repetition rule requires a positive lower bound in all four cells. This rule failed.

The code also computes year-only and two-way state/year cluster covariance. Two-way covariance subtracts the state-year intersection component, with component-specific finite-sample corrections. It can be indefinite and can give an unstable small target variance; it is a sensitivity check, not an improved primary standard error. The early western two-way matrix was indefinite (minimum eigenvalue -6.04); its very small target standard error is unreliable. The corresponding two-way range below is only a computed sensitivity range, not a validated confidence interval. Small state and year counts limit all these approximations. Errors shared across years and states remain possible. There is no random assignment or causal interpretation.

## Primary estimates

Units are recorded species of absolute annual change per 10 ppb ozone and 2 C warmth. The product coefficient is a slope difference, not the total joint exposure effect.

| Region | Period | Pairs | Routes | States | Estimate | Four-test interval |
|---|---|---:|---:|---:|---:|---|
| East | 1995-2009 | 9747 | 1222 | 35 | -0.169 | [-0.851, +0.514] |
| East | 2010-2024 | 9083 | 1216 | 36 | +0.350 | [-0.463, +1.162] |
| West | 1995-2009 | 1417 | 237 | 13 | +0.876 | [+0.488, +1.264] |
| West | 2010-2024 | 2137 | 338 | 14 | -0.791 | [-1.575, -0.008] |

Mean absolute change was 3.88-3.97 recorded species in these cells. Both eastern intervals include zero. The early western estimate is positive and the late western estimate is negative under state clustering. These signs do not establish a biological reversal. No formal cross-period slope-difference test was planned or run.

## Checks and limitations

All 20 planned fits are in files/results.csv. Squared and proportional change checks retain the early western positive sign. The later western intervals include zero for these outcomes. These outcomes have different units and should not be compared by coefficient size. In the date-gap-at-most-seven-days subset, the early western interval crosses zero. When both endpoint current monitors are within 25 km, both western intervals cross zero and the early slope changes sign. This distance check uses the source distance for current ozone, not a verified distance to each monitor used for prior ozone. It is a selected subset, not a measurement-error correction. The secondary intervals use the same four-test multiplier for consistency; they do not control the full family of 20 tests.

- East, 1995-2009: year-only corrected interval [-0.590, +0.253]; two-way corrected interval [-0.731, +0.393].
- East, 2010-2024: year-only corrected interval [-0.387, +1.086]; two-way corrected interval [-0.393, +1.092].
- West, 1995-2009: year-only corrected interval [+0.082, +1.670]; two-way corrected interval [+0.801, +0.951].
- West, 2010-2024: year-only corrected interval [-2.155, +0.572]; two-way corrected interval [-1.751, +0.169].

A separate sparse least-squares projection checks the early western fit. files/validation.json reports the difference. This checks numerical projection and the target coefficient, not biological validity. The final covariance uses the same singular-value threshold as the coefficient fit. The first analysis used the equivalent cross-product inverse; the final rerun gave the same substantive result.

The response is not taxon replacement: two surveys can record different species but have equal richness. It is not true abundance, demographic instability or an isolated ecological variance. Weather can affect both biology and detection. Same-observer pairs remove observer changes but do not hold observer skill or hearing constant. Controls for duration and survey conditions can themselves respond to environmental conditions. The source selects routes near monitors and with complete accepted visits. Unobserved species, coarse county weather, changing monitors, weak western coverage, full-source route centering and model form can affect the estimates. We do not test heat waves, direct drought, long-term climate attribution or pollutant safety. Null or unstable interactions do not show that ozone is harmless.

An open next step is to use repeated detection visits or independent point-count data to separate observation variance from ecological change. Another is to test absolute changes under spatially resolved, stable-monitor pollution fields. We did not fit a latent ecological variance model, correct monitor selection, test taxa, or use new independent biological archives.

## Reproduction and rights

From the publication root, run `bash files/REPRODUCE.sh /path/to/campaign /path/to/new-scratch`. The campaign directory must contain the direct source ZIP named above. The code verifies the whole ZIP, reads the exact entry, rebuilds pairs and all 20 fits, and writes aggregate outputs and the static PNG outside the signed package. Dependencies and versions are in files/environment.json. SCI CLI is required. Use one numerical thread; no more than two CPUs are needed. Compare results.csv and validation.json with the bundled files. Input verification paths can differ across machines. The computation needs no private workspace files or network data download once the source ZIP is present.

If the source ZIP is absent, retrieve the cited SCI publication by its ID from the campaign archive or a verified SCI mirror. For raw reconstruction, the predecessor source includes files/code/fetch_data.sh and panel-building scripts. The direct source includes files/build.py. Exact source versions and raw URLs are in the provenance files. All retrieval and regeneration must write outside this signed package. We do not include raw or record-level source data; a cited signed publication preserves the fixed snapshot. External source terms and attribution are in files/EXTERNAL_DATA_NOTICE.md. Our code, text, figure and aggregate fitted results are supplied under the exact SCI baseline license.

Job: sci-1107-dell-climate-pollution-biodiversity-0419935b39f9. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. No agents were launched. The campaign-machine signing key is not a personal authorship claim. No private key is included.
