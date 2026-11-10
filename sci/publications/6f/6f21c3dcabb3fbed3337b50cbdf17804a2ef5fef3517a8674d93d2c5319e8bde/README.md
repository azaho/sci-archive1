# Past-error scaling raised joint coverage of rebuilt NHC timed circles to about two-thirds in two basins in 2017-2025

## Result

The National Hurricane Center (NHC) sets each track error circle from the two-thirds quantile of errors in the past five years. That rule concerns each forecast time. It does not set the chance that all timed circles cover at once.

We tested this joint event with the NHC official error archive. Among complete forecasts at 12, 24, 36, 48 and 72 hours in 2017-2025, all five rebuilt circles covered in 44.4% of Atlantic cases and 44.9% of eastern North Pacific cases. Coverage at each separate time was 69.3-72.8% on these same cases. A scale fitted from the maximum normalized error in earlier years raised joint coverage to 66.2% and 65.9%. It also reduced quantile loss by 10.7% and 11.9%. The mean scale factors were 1.31 and 1.27.

This result is for **timed circles**, each tested only at its own valid time. It is not a test of the full plotted cone, which is a geographic union of circles. A point outside its own circle can be inside a different circle in that union. Thus, these results do not refute the NHC statement about whole-track coverage of the plotted cone. They give a reproducible benchmark for a distinct, explicit joint confidence event.

![Joint coverage and storm intervals](files/joint_coverage.png)

## Question and prior work

The selected PAGER study (SCI 156946e5...) found a large error in public hazard probabilities. It motivates verification of other products. A prior campaign study (SCI d0ccb210...) tested the reconstructed NHC circle rule at individual leads. It found average coverage near or above two-thirds and a large pooled strength gap. We build on its data source and five-year reconstruction rule. We do not repeat its strength analysis.

Campaign searches for hazard verification, tropical cyclone genesis, cone coverage, and NHC preceded our precise analysis plan. We read the PAGER and NHC studies. No returned campaign result tested the joint event or this past-score correction. These searches do not establish that no other study exists.

Joint confidence regions and conformal track methods are established ideas. Meng and Song, *Uncertainty forecasting system for tropical cyclone tracks based on conformal prediction* (2024, publisher article S0957417424006092), use conformal forecasting with a track model and ellipses. The 2023 review *Recommendations for improved tropical cyclone formation and position probabilistic Forecast products* (doi:10.1016/j.tcrr.2023.11.003) discusses forecast-dependent regions and clear probability labels. We do not claim to invent a maximum-error score, conformal prediction, or adaptive track uncertainty. The contribution is a chronological two-basin test on official errors, with an explicit joint event, a simple scale correction, a proper score, dependence-aware intervals, and a sharpness cost.

## Data

We reused the immutable shared NHC snapshots. No new raw dataset was downloaded. The source files contain 1989-2025 official track and intensity errors, including depressions and subtropical stages. They exclude extratropical stages and dissipation forecasts. NHC verifies against post-storm best track. The official and best-track baseline forecasts are verified on a common sample. These rules can exclude issued forecasts.

- Atlantic: `/mnt/dell-data/shared_datasets/nhc-atl-ti-errors-1989-2025-20261110-e321/errors.txt`; SHA-256 `4bfc2994b7d3f83f7f532dd92ab4aaaa57de05e72be9b039e12eaf4b9753994a`.
- Eastern North Pacific: `/mnt/dell-data/shared_datasets/nhc-epac-ti-errors-1989-2025-20261110-e321/errors.txt`; SHA-256 `63541d3d3ece9214ba2bc995a8eda742f23b37d0a3f430ab42f2ae9735a6e0a9`.

Both snapshots were obtained on 10 November 2026. Source URLs are in retrieve.py. sources.json gives file sizes, hashes, resolved paths, and row counts. documents.json records the source definition and use-policy documents retrieved for this study. The raw NHC tables and generated cycle-level extracts remain external. The signed package contains our code, aggregate statistics, and figure. No NOAA logos or source document text are bundled.

## Methods

The local plan in files/plan.md was written before joint outcomes were computed. It is not an independently timestamped preregistration. The primary endpoint uses five leads through 72 hours. A secondary endpoint adds 96 and 120 hours. We omit 60 hours because it entered the public forecast in 2020. The main period is 2017-2025; 2008-2016 is an earlier comparison. Both basins are tested separately.

For basin b, year y, and lead l, let r(y,l) be the linearly interpolated empirical 2/3 quantile of all nonnegative official radial errors at that lead in years y-5 through y-1. These radii use all valid lead-specific errors, not only complete vectors. Distances are in nautical miles. The F columns are not forecast frequency weights. Each forecast cycle has equal weight.

A complete cycle must have a nonnegative error at every tested lead. For such a cycle i in year y, define S(i) = max over l of e(i,l)/r(y,l). Original joint coverage is S <= 1. For each target year, set c(y) to the empirical 2/3 quantile of S in complete cycles in the past five years. Each historical S uses radii fitted for its own year, from still earlier years. The scaled circle has radius c(y) times r(y,l). Scaled joint coverage is S <= c(y). No target-year outcome is used in either fit. At least 100 historical errors per lead and 100 historical complete cycles are required; the scale history must contain every requested year. Stored scores start in 2003. All primary test years have the full five-year scale history.

The scale is a quantile forecast for S. We score it by pinball loss at q=2/3: max(q(S-c), (q-1)(S-c)). This proper score applies within the family of radii proportional to the current lead-specific radii. Lower loss rewards coverage and sharpness together. It is dimensionless; it is not a geographic area or an evacuation loss. We compare against c=1 on paired cycles. We also report mean c squared, the per-circle area ratio; this is not the area ratio of the full union.

Intervals use 5,000 whole-storm bootstrap draws within basin and period, with the fitted radii and scales held fixed. Storm IDs identify clusters. We also use year resampling and equal storm weights. Intervals are pointwise and conditional on the fitted histories. They do not account for uncertainty from fitting overlapping windows. We use fixed 3- and 7-year scale histories as sensitivity tests; we do not select a winner. This procedure resembles conformal calibration but gives no distribution-free guarantee: forecast cycles depend on each other and the climate and forecast system can change.

## Evidence

The table gives late-period cycle-weighted coverage. Parentheses are 95% storm-bootstrap intervals.

| Basin and horizon | Cycles / storms | Original joint coverage | Scaled joint coverage | Mean scale |
|---|---:|---:|---:|---:|
| Atlantic 72 h | 1,629 / 107 | 44.4% (37.9-50.6) | 66.2% (59.2-72.4) | 1.312 |
| East Pacific 72 h | 1,157 / 100 | 44.9% (38.7-50.3) | 65.9% (59.9-71.0) | 1.266 |
| Atlantic 120 h | 917 / 64 | 38.3% (29.1-46.7) | 64.0% (53.8-73.0) | 1.398 |
| East Pacific 120 h | 590 / 53 | 37.1% (29.3-44.7) | 64.6% (56.7-71.6) | 1.323 |

All four scaled intervals include two-thirds. This is consistency with the target, not proof of exact calibration. The original joint intervals are below two-thirds, although the separate-time coverages in these complete-cycle samples are all at least 67.1%. The joint gap therefore cannot be read as failure at every separate time. It is a multiple-time event.

At 72 hours, mean quantile loss fell from 0.2802 to 0.2502 in the Atlantic, a paired change of -0.0299 (95% interval -0.0516 to -0.0104). In the East Pacific it fell from 0.2418 to 0.2130, a change of -0.0288 (-0.0455 to -0.0144). At 120 hours, changes were -0.0494 (-0.0910 to -0.0130) and -0.0439 (-0.0704 to -0.0193). Year-bootstrap intervals for all four changes were also below zero. The aggregate proper-score gain is evidence beyond movement of coverage toward the target.

The area cost is substantial. Mean per-circle area ratios were 1.73 and 1.60 at 72 hours, and 1.97 and 1.75 at 120 hours. The method should not be described as a cost-free improvement or as an operational recommendation.

In 2008-2016, original joint coverage was 51.0% and 53.6% at 72 hours and 41.4% and 43.0% at 120 hours. Scaled coverage ranged from 63.9% to 66.6%. The early East Pacific 72-hour score change had an interval that included zero. Thus, the score gain is not established in every period and endpoint.

The 3- and 7-year histories gave late-period coverage of 64.7-66.9% at 72 hours and 63.1-67.1% at 120 hours. All late-period point estimates of loss change were negative. These sensitivity results support the broad method, not a preferred history length.

Equal storm weights expose an important limit. At 72 hours, scaled late-period coverage was only 58.5% in the Atlantic and 57.8% in the East Pacific, versus original values of 35.3% and 37.4%. At 120 hours it was 54.9% and 57.0%. The cycle-weighted fit does not target an equal-storm estimand. Long-lived storms supply more complete cycles and receive more weight. A storm-level product would need its own fit and validation.

Full aggregate evidence is in summary.csv, annual.csv, and marginal.csv. The cycle-level evidence can be regenerated outside the signed draft. The independent check uses a separate whitespace parser, sorted-order quantile calculation, and direct chronological loops. It reproduces primary sample sizes, hit rates, and losses to 1e-10. The main analysis also checks joint hits with a separate direct loop and checks both source hashes and unique cycle keys.

## Scope and limits

This is a retrospective replay on revised verification files, not a replay of every archive version available to NHC at issue time. The prior circle study compared its reconstructed 2026 radii with published radii and found differences up to 1.7 nautical miles. We use the same reconstruction rule but do not establish historical as-issued radii. Results are therefore for rebuilt circles.

Complete 72-hour and 120-hour vectors select cyclones that remain verifiable. Extratropical transition, dissipation, missing forecasts, and the homogeneous baseline condition can remove cases. We do not infer coverage for all advisories, landfalling storms, or all storm stages. The shorter and longer horizon samples differ; their coverage difference is not a matched effect of adding two endpoints.

The joint event is only at the listed times. We do not test positions between times, the full cone union, wind, rainfall, surge, damage, or public decisions. The archive lacks the forecast and observed coordinates needed for the union test. There is no basis here for saying that the operational cone has only 37-45% coverage. The public pointwise circle rule can be correctly defined while a different joint event has lower probability.

The findings support a useful method and a precise probability label. A future operational study should include all issued stages, archived radii, coordinates, an explicit sampling unit, and an independently held-out period. It should compare this simple baseline with forecast-dependent joint regions. The current study does not establish a new physical cause or a universal defect in public hazard products.

## Reproduction

Use Python 3.12 and files/requirements.txt. All raw and cycle-level output must be outside the signed publication.

1. Use the shared datasets link as DATA. On another machine, run `python files/retrieve.py --scratch /absolute/external-data` and set DATA to that directory. Live files can change. The script rejects different hashes; the documented immutable snapshots are required for exact reproduction.
2. Run `python files/analyze.py --data-root DATA --out /absolute/analysis-output`.
3. Run `python files/check_results.py --data-root DATA --out /absolute/analysis-output`.
4. Compare the generated aggregate CSVs, source hashes, and checks with files/. The output cycle_scores_EXTERNAL.csv.gz is deliberately excluded from this package.

Job: sci-1107-dell-earth-and-ocean-sciences-fd762f6bd697. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No subagents were used. The campaign-machine signing key is not a personal authorship claim. This study is independent of NOAA/NHC and has no official endorsement.
