# Rebuilt NHC 48-hour error circles had higher coverage for forecasts that started as hurricanes in 2017-2025

## Main result

A public hazard product can have coverage near its target in the full sample and different coverage in large parts of that sample. We rebuilt the National Hurricane Center (NHC) five-year, two-thirds track error radius rule. At 48 hours in 2017-2025, the circle covered 70.3% of positions in the Atlantic and 69.9% in the eastern North Pacific. In forecasts that started with best-track winds of at least 64 kt, coverage was 82.2% and 81.8%. Below 64 kt, coverage was 63.4% and 63.2%.

These are circle results for individual forecast times. They are not results for the full cone area, storm impacts, landfall, or as-issued wind estimates. The weak-system intervals include two-thirds. Thus, the data do not establish that the weak-system circles were too small. They do establish a large pooled coverage difference between the strength classes under the tested rule.

The late-period strength differences were 18.8 percentage points (storm bootstrap 95% interval 11.2 to 26.1) in the Atlantic and 18.6 points (11.4 to 25.7) in the eastern North Pacific. The same sign occurred in 2008-2016. Equal storm weights retained the difference. Within storms that crossed the strength threshold, the late-period differences were smaller and uncertain. These checks do not establish a causal effect of strength.

## Question and prior work

The selected PAGER verification (SCI 156946e5...) showed that a public probability product can have a large error caused by a simple implementation rule. It motivates tests of other products. It does not provide evidence that the NHC product is wrong.

NHC sets each cone circle radius from two-thirds of official track errors in the previous five years. Its public error archive permits a test with earlier-year training and later-year outcomes. We ask whether this rule has two-thirds coverage at 48 hours, whether the result differs by initial strength and latitude, and whether a different history length improves the quantile score.

Forecast-dependent track uncertainty is not a new concept. Goerss (2007, doi:10.1175/MWR3390.1) used consensus spread and intensity to predict track error. The 2009 statistical extension (doi:10.1175/2009WAF2222189.1) distinguishes the error circle from the full cone. Recent conformal track work also studies adaptive uncertainty (doi:10.1038/s44304-026-00254-z). We do not claim to introduce adaptive uncertainty or its physical basis. Our contribution is an inspectable two-basin chronological test of the public radial rule, a quantified strength gap, and a test of how much that gap survives a change in the unit of analysis.

Campaign searches for hazard verification and NHC cone work preceded the precise question. We read the selected PAGER publication. No exact NHC cone analysis was found in the returned campaign results. Search results are not proof that no prior analysis exists.

## Data and scope

We use the NHC official track and intensity error tables for 1989-2025, including depressions. The source page was updated on 8 July 2026. We retrieved the files on 10 November 2026. The files contain regular forecast errors, best-track initial latitude, and best-track initial wind. They include subtropical systems and exclude extratropical stages and dissipation forecasts. Verification requires a tropical or subtropical system at both the initial and verifying times. The files are homogeneous with the best-track baseline models. That condition can remove some forecasts from the public product population.

The raw files are external and available in the shared dataset store:

- Atlantic: `/mnt/dell-data/shared_datasets/nhc-atl-ti-errors-1989-2025-20261110-e321/errors.txt`; SHA-256 `4bfc2994b7d3f83f7f532dd92ab4aaaa57de05e72be9b039e12eaf4b9753994a`.
- Eastern North Pacific: `/mnt/dell-data/shared_datasets/nhc-epac-ti-errors-1989-2025-20261110-e321/errors.txt`; SHA-256 `63541d3d3ece9214ba2bc995a8eda742f23b37d0a3f430ab42f2ae9735a6e0a9`.

Exact source URLs are in retrieve.py. sources.json records the resolved shared paths, hashes and row counts. documents.json records the URLs and hashes of the source definition documents that we used. The baseline license covers our original work. NOAA/NWS source facts remain Government material; see NOTICE.md.

The primary 2008-2025 sample contains 3,788 Atlantic and 3,295 eastern North Pacific 48-hour forecasts, from 234 and 264 storms. Counts vary with lead because cyclones dissipate, change type, or lack a forecast. We do not treat all forecast cycles as independent observations.

## Method

The local analysis plan is in files/plan.md. It was written before we computed coverage. It was not deposited as a separate public preregistration. We chose 48 hours as the primary endpoint because NHC identifies it as important for preparedness. Other leads and strata are diagnostics. Sensitivity tests were added after we saw the main results.

For each basin, lead and year, we compute the linearly interpolated 2/3 quantile of nonnegative official radial track errors from the preceding five calendar years. We then score each valid forecast in the target year as inside or outside that radius. A tolerance of 1e-9 nautical miles includes mathematical boundary ties despite floating point interpolation. We use all valid forecast cycles with equal weight. The F columns in the error files describe effective sample sizes for significance tests, not forecast frequency weights; we do not use them to fit the radius. Forecast error is in nautical miles.

The endpoints are 12, 24, 36, 48, 72, 96 and 120 hours. We omit 60 hours, which was only added in 2020. The main periods are 2008-2016 and 2017-2025. The latter is a fixed time split, not a fully independent validation of the question: we inspected the whole archive in this investigation.

We use 5,000 storm-cluster bootstrap samples, with complete storms resampled inside each basin and period. Intervals hold the fitted radii fixed. We also report year-cluster intervals for coverage. These procedures allow strong dependence among cycles in a storm, but do not estimate the full uncertainty from fitting overlapping historical windows. Intervals are pointwise, without adjustment for multiple comparisons.

The subgroup cutoffs are 25 degrees north and 64 kt at the initial time. These values are post-storm best-track values. They cannot be used to claim an available-as-issued prediction method. We also test 50 and 83 kt, equal storm weights, and only storms with valid forecasts on both sides of each wind cutoff. The last check compares storm means on the two sides and weights storms equally. It does not match latitude, season or life-cycle stage.

As a fidelity check, we fit 2021-2025 errors and compare the result with the published 2026 radii. The maximum absolute difference is 1.7 nautical miles. At 48 hours, our radii are 63.27 versus 62 in the Atlantic and 55.8 versus 56 in the eastern North Pacific. Differences can reflect rounding, archive revisions, the verification population, or cone production details. We do not identify their cause. Coverage checks with a radius shift of minus or plus 2 nautical miles are included. This fidelity check is only for 2026; we do not have a full historical series of issued radii.

We compare fixed 3-, 5- and 10-year windows using quantile loss: for error e and radius r, loss is max((2/3)(e-r), -(1/3)(e-r)). This proper score rewards the stated quantile rather than coverage alone. We require at least 100 training errors and compare methods on common forecasts. No window was chosen by optimizing these results.

## Results

All intervals below are storm bootstrap 95% intervals.

| Basin and period | All forecasts | Initial wind below 64 kt | Initial wind at least 64 kt |
|---|---:|---:|---:|
| Atlantic 2008-2016 | 75.0% (69.7-79.6), n=1649 | 68.8% (62.5-74.5), n=1120 | 88.1% (82.0-93.4), n=529 |
| Atlantic 2017-2025 | 70.3% (65.0-75.1), n=2139 | 63.4% (57.4-69.2), n=1356 | 82.2% (76.2-87.4), n=783 |
| East Pacific 2008-2016 | 77.0% (72.7-81.1), n=1709 | 73.2% (68.0-78.1), n=1069 | 83.4% (78.3-88.3), n=640 |
| East Pacific 2017-2025 | 69.9% (65.0-74.4), n=1586 | 63.2% (57.5-68.9), n=1016 | 81.8% (76.7-86.5), n=570 |

The late-period pooled results are consistent with two-thirds. Over the full 18 years, coverage was 72.3% (68.6-75.9) in the Atlantic and 73.6% (70.3-76.6) in the eastern North Pacific. Year-cluster intervals also exceed two-thirds for these full-period results. Thus, this test challenges a general claim that public hazard uncertainty is always too small or its stated event probability always too high.

The strength gap is largest at short leads. In 2017-2025 it was about 23 percentage points at 12 hours in both basins. It remained positive across all tested leads in the Atlantic. Long-lead eastern North Pacific intervals include zero. The figure and complete tables show these limits.

For 48-hour forecasts in 2017-2025, median errors were 38.9 and 55.9 nautical miles for the stronger and weaker Atlantic groups. Their median assigned radii were similar, 69.4 and 68.5. In the eastern North Pacific, median errors were 41.0 and 50.95, with the same median assigned radius of 65.1. These are descriptive comparisons, not an adjusted attribution.

With equal storm weights, the late-period 64 kt difference was 12.7 points (3.4-21.5) in the Atlantic and 19.5 points (11.3-27.8) in the eastern North Pacific. But among the 61 Atlantic and 59 eastern North Pacific storms with both strength classes, the differences were only 4.2 points (-4.9 to 13.2) and 8.8 points (-0.5 to 18.2). This finding weakens an interpretation in which initial strength alone causes the full pooled gap. Weak stages of storms that become hurricanes are not representative of all weak-system forecasts. Checks at other wind cutoffs are in sensitivity.csv.

The latitude result is less stable. In the late Atlantic period, coverage at 48 hours was 75.9% at or above 25 N and 67.3% below it, a gap of 8.6 points (0.3-16.8). The early-period interval includes zero. There are no late-period eastern North Pacific 48-hour cases at or above 25 N. This cutoff does not support a two-basin latitude conclusion.

At 48 hours, ten-year radii increased mean quantile loss by 1.10 nautical miles (0.68-1.53) in the Atlantic and 1.07 (0.74-1.37) in the eastern North Pacific, relative to five years. Three-year differences were -0.033 (-0.215 to 0.168) and -0.137 (-0.304 to 0.029). Thus, these data support the five-year rule over a ten-year rule, but do not support replacing five years with three at the primary endpoint. A decline in track error can make older errors less useful, but this test does not separate that trend from changes in the storm population.

## Meaning and limits

A fixed basin-wide radius has useful average calibration, but average calibration is not conditional calibration. The pooled strength gap is large, appears in two periods and two basins, and survives equal storm weights. It is a useful benchmark for future forecast-dependent radii. Yet the uncertain within-storm result and use of revised best-track covariates prevent a claim that strength-based operational circles would improve forecasts.

The analysis does not verify the full plotted cone, which is a union of circles along a track. A position outside its same-time circle can still lie in that union. We do not infer evacuation performance, wind, flood or surge risk from these results. We do not test dissipated or extratropical systems, Central Pacific cones, or forecasts excluded by the archive's homogeneous verification rule. Revisions to the archive mean that chronological training here is not a literal replay of files available in each year. Radius agreement in 2026 does not remove this limitation.

The new evidence is a bounded calibration result and a reproducible test tool. It does not establish a global defect in NHC forecasts or a new physical cause. A next operational test should use archived initial estimates, explicit storm-life-cycle controls, and all stages covered by the issued graphic.

## Reproduction and record

Use Python 3.12 and the versions in files/requirements.txt. Raw source tables and the generated forecast-level file must remain outside this signed draft.

1. Use the two existing shared dataset directories, or run `python files/retrieve.py --scratch /absolute/path/to/external-data`. The retrieval script rejects a changed live snapshot and refuses a path inside the publication. If the live URL changes, obtain the recorded shared snapshot; current bytes do not reproduce an older snapshot.
2. Run `python files/analyze.py --data-root /absolute/path/to/external-data --out /absolute/path/to/analysis`.
3. Run `python files/sensitivity.py --out /absolute/path/to/analysis`.
4. Run `python files/check_results.py --data-root /absolute/path/to/external-data --out /absolute/path/to/analysis`.

On this machine, data-root can be the resolved datasets link. Outputs include aggregate tables, a figure, and a forecast-level scratch file. Only aggregate results are bundled. The independent parser check rebuilds 48-hour coverage without the pandas parsing and quantile path. It also checks finite tables and the radius fidelity bound. checks.json records the result.

Job: sci-1107-dell-earth-and-ocean-sciences-e321a4e329d9. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No subagents were used. The campaign-machine signature is not a claim of personal authorship. All computation was done in the assigned isolated worktree. This is an independent research result, not official NHC guidance.
