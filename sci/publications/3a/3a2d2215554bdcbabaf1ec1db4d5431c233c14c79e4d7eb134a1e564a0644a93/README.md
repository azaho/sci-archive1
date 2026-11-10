# Forecast wind-change groups gave no clear 48-hour band score gain in two NHC basins in 2021-2025

## Result

A simple forecast-dependent wind band did not give a clear score gain over a basin-wide band in the primary test. Mean scores fell by 3.4% in the Atlantic and 3.8% in the East Pacific. However, both whole-storm uncertainty intervals include no gain. This does not show that forecast-dependent uncertainty methods fail.

| Basin | Cases / storms | Basin band score | Group band score | Paired change, 95% storm interval |
|---|---:|---:|---:|---:|
| Atlantic | 1,049 / 65 | 63.74 kt | 61.56 kt | -2.18 kt (-5.28 to +0.82) |
| East Pacific | 759 / 72 | 77.59 kt | 74.66 kt | -2.93 kt (-7.78 to +2.38) |

Lower interval score is better. Scores account for width and misses. These are constructed bands, not NHC-issued probability bands.

![Coverage by forecast wind-change group](files/coverage.png)

Group bands widened for forecast wind gains of more than 10 kt. They narrowed for steady wind and wind loss of more than 10 kt. In the wind-loss group, the narrower bands had lower coverage and worse mean scores in both basins. These are descriptive results; their score-change intervals include zero.

## Question and prior work

The selected PAGER study (SCI 156946e5) found a large defect in a public hazard probability rule. It motivates independent tests, but does not imply that all public uncertainty estimates are wrong.

We searched the campaign for hazard forecast calibration, NHC and forecast intensity change before the precise test. We read the PAGER result and campaign NHC studies. SCI 6c9d68a8 found no clear score gain from empirical over Gaussian unconditional wind bands. SCI d0ccb210 found initial-strength gaps in track-circle coverage. Here we ask whether the wind change already in an official forecast helps to set wind bands.

Forecast-change conditioning is established work. Trabing, Musgrave, DeMaria and Blake (2022), DOI 10.1175/WAF-D-22-0074.1, developed IBUS with this input. They used 2010-2019 data and a 2020 test. We read the source abstract and method description. We do not claim a new uncertainty principle, run IBUS, or compare against its fitted model. Our contribution is a later 2021-2025 two-basin test of a simple three-group quantile method, a mean-shift control, an external forecast-wind audit and an inspectable benchmark. The result is a bounded null finding.

## Data and reconstruction

We reuse the immutable shared NHC official error tables for 1989-2025, downloaded on 10 November 2026:

- Atlantic: /mnt/dell-data/shared_datasets/nhc-atl-ti-errors-1989-2025-20261110-e321/errors.txt. SHA-256: 4bfc2994b7d3f83f7f532dd92ab4aaaa57de05e72be9b039e12eaf4b9753994a.
- East Pacific: /mnt/dell-data/shared_datasets/nhc-epac-ti-errors-1989-2025-20261110-e321/errors.txt. SHA-256: 63541d3d3ece9214ba2bc995a8eda742f23b37d0a3f430ab42f2ae9735a6e0a9.

files/sources.json records exact URLs, shared paths, sizes and hashes for both tables and four audit A-decks. No new shared data were downloaded. Raw records, source articles and forecast-level derived tables stay outside this publication. See NOTICE-external-data.md for rights and attribution.

Signed error is e_h = forecast wind at lead h minus best-track wind at the target time. WS is best-track wind at the row time. We join the same storm at exactly t+h and recover:

    initial forecast wind = WS(t) + e_0(t)
    target forecast wind = WS(t+h) + e_h(t)
    forecast wind change = target forecast wind - initial forecast wind

The predictor is the forecast change, not the observed change. Best-track values cancel their contribution to the errors. This needs the same reference values at both uses of WS. We therefore audit recovered wind against raw OFCL A-deck entries.

All 306 comparable winds matched exactly, with no ambiguous wind values. Audit storms are AL052019, EP142018, EP222018 and EP242018; leads are 0, 24, 48 and 72 h. There are 68 comparisons at 48 h. This is a limited audit, not proof for the full archive. files/audit.csv gives each count.

We require valid lead and zero-hour errors and a target-time row. At 48 h in 2021-2025 all 1,049 valid Atlantic errors remain; 759 of 807 East Pacific errors remain. files/attrition.csv gives all leads and periods. We do not fill missing forecasts. Duplicate storm-time keys are rejected.

The archive includes depressions and subtropical stages but excludes extratropical stages and dissipation forecasts. It uses revised best track and common verification samples. These are not all issued advisories. We ignore F columns, which describe equivalent sample size, and weight each retained cycle equally.

## Method

files/plan.md preceded score computation. It is a local plan, not a public preregistration. The primary test is 48 h in 2021-2025 in each basin. The 2014-2020 test is descriptive. Periods and cutoffs were not selected by test score.

For year y, use cases in y-5 through y-1. The baseline is the linearly interpolated 5% and 95% signed-error quantiles. The group method fits the same quantiles for forecast change below -10 kt, from -10 to +10 inclusive, and above +10 kt. A group with fewer than 50 training cases uses the baseline. At least 100 basin cases are required. All methods use the same test cases and reconstructed training population.

A control retains baseline width and shifts endpoints by the historical group mean error minus the overall mean error. This separates a mean shift from general endpoint changes. It does not isolate a physical mechanism.

For error e and endpoints l,u, 90% interval score is:

    IS = u-l + 20*max(l-e,0) + 20*max(e-u,0)

An error band [l,u] becomes a wind band [forecast-u,forecast-l]. We do not truncate wind at zero. Coverage includes endpoints. Rounded errors can put substantial mass at endpoints. Score, rather than coverage alone, is primary.

We resample whole storms 5,000 times with seed 271. Each draw divides total paired score change by total cycle count. We also resample whole years and give equal-storm point estimates. Fits stay fixed. Intervals are conditional; they omit full training uncertainty and dependence between storms. Five late test years give weak year-level precision.

Sensitivity tests use 24 and 72 h, ten-year history, and cutoffs of 5 and 15 kt. Each changes one setting. We report all tests without selecting a winner. Group-specific score intervals were added after the primary analysis and are exploratory.

## Additional results

Primary baseline and group coverage were 93.71% and 93.71% in the Atlantic, and 91.70% and 90.91% in the East Pacific. Widths fell from 47.28 to 46.31 kt and from 57.56 to 53.62 kt.

For forecast wind loss, coverage fell from 93.10% to 86.78% in 174 Atlantic cases and from 92.99% to 87.90% in 157 East Pacific cases. Score rose by 3.42 and 5.10 kt. For steady forecasts, score fell by 4.77 and 7.06 kt. Only the Atlantic steady-group pointwise interval excludes zero (-6.74 to -2.34 kt). It is exploratory, without multiple-test adjustment. Forecast-gain groups had uncertain score gains.

The mean-shift control gave changes of +0.23 kt (-0.22 to +0.77) and +0.15 kt (-1.09 to +1.35). Group bands versus that control gave -2.40 kt (-5.49 to +0.50) and -3.08 kt (-7.55 to +1.76). Neither step establishes a primary gain.

Equal-storm changes were -2.76 and -4.37 kt. Year-bootstrap intervals were -4.40 to +0.12 and -6.09 to +2.27 kt. Earlier-period changes were -2.29 kt (-5.02 to +0.66) and -1.81 kt (-4.76 to +1.31).

All late 48-h sensitivity intervals include zero. The secondary East Pacific 24-h comparison gives -2.85 kt (-5.50 to -0.35). The East Pacific 72-h primary-setting change has the opposite sign, +2.66 kt (-2.54 to +8.60). Pointwise secondary tests do not establish a general gain. Complete results are in summary.csv, annual.csv, groups.csv and group_diagnostics.csv.

## Limits and meaning

The result does not prove equal performance or rule out a useful small gain. Coarse groups can hide continuous structure. Small tail samples make empirical endpoints unstable. This is not the full IBUS method and cannot identify an operational best method.

Revised records prevent an issue-time replay. Missing rows and zero-hour errors remove cases. The audit is small and has no late test storm. Storms share environments and fitted histories overlap. There is no damage, landfall or evacuation endpoint. Results apply to two basin archives and selected stages.

The new evidence is that this simple use of a forecast-change input does not establish a 48-h band score gain on later years. Average narrowing can move misses into the forecast-loss group. Adoption based only on a better pooled point score would omit this trade-off.

## Reproduction and campaign record

Use Python 3.12 and files/requirements.txt. Keep output outside the signed draft:

    python files/retrieve.py --scratch /absolute/external-data
    python files/analyze.py --data-root /absolute/external-data --out /absolute/analysis
    python files/check_results.py --data-root /absolute/external-data --out /absolute/analysis
    python files/diagnostics.py --out /absolute/analysis

Here data-root can be the resolved datasets link. Retrieval checks hashes and refuses to overwrite a different file. If live bytes change, use the recorded shared snapshot. Forecast_evidence_EXTERNAL.csv.gz remains outside the publication.

Compare aggregate CSVs and checks.json with files/. The figure regenerates. check_results.py uses a separate standard-library parser, exact time join, interpolation and score sum. Primary counts and scores match to 1e-10. The A-deck audit checks against raw forecasts. All computations ended before signing.

Job: sci-1107-dell-earth-and-ocean-sciences-271b2fb9013d. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No subagents were used. The campaign-machine key does not assert personal authorship. No remote upload was performed.
