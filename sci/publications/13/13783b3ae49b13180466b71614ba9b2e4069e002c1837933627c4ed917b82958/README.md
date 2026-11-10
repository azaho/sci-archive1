# Group-count and area-concentration controls retain the Cycle 25 radio excess in matched area models

Job: sci-1107-dell-astronomy-45fafc704503. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 10 November 2026. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result and question

Does a change in the number and area distribution of whole spot groups explain the Cycle 25 emission excess at fixed dark area? In the tested models, it does not. With HMI area as reference, adding group count and effective group number changes the fitted F10.7 rise from about 9.9% to 10.4%. With ground area as reference, the rise changes from about 13.3% to 12.6%. Mg II also retains a positive offset. This is evidence against a specific group-composition explanation under stable measurement scales and the fitted response. It is not evidence that all possible changes in group structure have been excluded.

![Group controls](files/group_controls.png)

## Why this test adds evidence

The selected flare work removes GOES scale and event-list artefacts. The remaining activity-index change needs a separate explanation. Campaign SCI 24162623 finds higher emission at fixed HMI area. SCI 3f959cc2 finds higher 2 GHz emission at fixed sunspot number. These tests do not condition on group-area concentration. SCI c6d62719 tests solar memory; the Locarno studies test a different historical interval. We searched campaign sunspot results before choosing this question. None of the returned publications tests the added group-composition controls used here.

Mandal et al. (2020), DOI 10.1051/0004-6361/202037547, supply group and total areas. Meadows (2025), DOI 10.1093/rasti/rzaf024, measures HMI area and discusses differences in grouping by observers. Yeo et al. (2020), DOI 10.1051/0004-6361/202037739, study the different evolution of spots and bright magnetic structures. Mursula et al. (2024), DOI 10.1051/0004-6361/202449231, study long-term radio-to-spot changes. Those broad findings are prior work. Our addition is a conditional test of whole-group number and area concentration as an explanation of the recent area-to-emission difference, with shared-support and source checks. We do not claim a new emission mechanism.

## Data and rights

We reuse six immutable shared files in place. Their exact paths, URLs, byte counts and SHA-256 hashes are in files/inputs.json. The shared data root is /mnt/dell-data/shared_datasets on HP SSD, also reached through ./datasets in the assigned worktree. No new shared download was needed. Mandal group and total areas are the 7 September 2025 update. HMI area, SILSO V2 daily number, adjusted F10.7 through LASP/LISIRD and Bremen Mg II through LASP/LISIRD are campaign snapshots retrieved on 10 November 2026.

External observations and derived daily or monthly databases stay outside this publication. We include only our code, statistical estimates, figures and report. Source attribution and separate source terms are in files/NOTICE.md. The parsing and input-retrieval code is adapted from SCI 24162623, whose baseline license provides MIT terms for code. New model code is included here under the same baseline terms. No third-party data license is replaced.

We remove exact ten-field duplicate group rows, as required by the defect found in SCI 24162623. We require daily group sums to agree with the separate total-area file to within one microhemisphere. files/duplicate_audit.csv and files/area_audit.json give aggregate input checks. These checks are repeated by our code. They are not a new discovery about this catalogue.

## Preparation and estimands

For each day let a_i be a positive corrected group area. Define K as the number of groups and

```
E = (sum a_i)^2 / sum(a_i^2)
T = sum sqrt(a_i)
```

E is the effective number of equal-area groups. It is one when one group holds all area and equals K when all groups have equal area. T is a size-distribution proxy. It would be proportional to perimeter only for separate circular regions with equal shape; it is not measured spot perimeter. None of these measures gives individual-spot size or plage area. The monthly E is the mean of daily E, not a ratio of monthly area moments.

Use January 2011 to November 2013 and January 2022 to November 2024, the same nominal cycle months 25 through 59 after December 2008 and December 2019. HMI readings are averaged per day. F10.7 is the median valid adjusted reading per day in 30 to 2000 sfu. Bremen source 20, which is filled from radio data, is omitted. Negative sunspot markers are missing. Require positive HMI area, ground area, F10.7, Mg II, sunspot number, K, E and T on the same day. Thus spotless days are outside the target population. Require at least 15 common dates per month. Means use exactly the same dates for all variables. Japan, ground area, HMI and Canadian data need not observe the same hour.

For each area reference separately, keep monthly areas within the intersection of the two cycle ranges. The main HMI sample has 26 early and 22 late months. The ground sample has 27 early and 25 late months. This differs slightly from the prior area study because positive group days and consistent daily sums are required here. Responses are monthly total F10.7, Mg II, sunspot number, K, E and T. Mg II percentages refer to the full index and cannot be compared in physical size with radio percentages above a quiet background.

## Models and uncertainty

Fit each monthly log response to an intercept, a centered natural cubic spline of log area with three degrees of freedom, and a Cycle 25 indicator. The indicator is a constant conditional log offset. Add log K, log E, both, or log T in separate models. Report 100*(exp(offset)-1). The primary comparison uses both K and E. These are regressions at fixed predictors, not paired observations or causal mediation estimates.

Controls use a common phase slope, separate cycle phase slopes centered at month 42, a four-degree area spline, three-degree splines for each morphology control, and only Kislovodsk source dates. The last test recomputes monthly means and area overlap, so it can change the sample. Three- and twelve-observation block checks test sensitivity to dependence. All controls were selected during this investigation, without a preregistration.

The joint-support check retains a month only if its vector (log area, log K, log E) lies inside the opposite cycle's convex hull before this check. This is a one-pass support restriction, not equal-density matching. The final retained hulls can differ. The HMI test leaves only 16 early and six late months; the ground test leaves 17 and eight. Its narrow intervals cannot be treated as strong independent evidence because very few blocks remain.

Use 3,000 paired residual bootstrap draws with design fixed, circular blocks of six retained monthly observations, drawn separately within cycles. All responses use the same residual row draw. Intervals are conditional 2.5 and 97.5 percentiles. The paired full-model minus area-only log-offset contrast is also saved in files/audit.json. The reduced model uses the exact same dates and phase controls. Its intervals use outcomes generated from the full fitted model. This contrast is a model-based sensitivity estimate, not an identified physical share.

Code asserts full matrix rank and exact recovery of an injected 14% response gain in every fit. Output records condition numbers, sample sizes and the dates used in external scratch. These algebra checks do not validate the solar model. Reference error, measurement drift, systematic source error, window selection and response-model error are not in the intervals. Blocks in retained-month order can span calendar gaps. Twelve-observation blocks can be large relative to a cycle sample.

## Numerical evidence

| Reference and model | F10.7 change (%) | Conditional 95% limits | Mg II change (%) | Early / late months |
|---|---:|---:|---:|---:|
| HMI: Area only | +9.92 | +4.17 to +15.90 | +1.60 | 26 / 22 |
| HMI: Area + K + E | +10.42 | +7.26 to +13.70 | +1.69 | 26 / 22 |
| HMI: Nonlinear K and E | +11.35 | +8.11 to +14.43 | +1.82 | 26 / 22 |
| HMI: Both + separate phase slopes | +13.08 | +10.61 to +15.16 | +2.18 | 26 / 22 |
| HMI: Both, Kislovodsk dates | +9.54 | +6.47 to +12.86 | +1.55 | 26 / 22 |
| HMI: Both, joint support | +8.87 | +7.10 to +10.48 | +1.62 | 16 / 6 |
| Ground: Area only | +13.32 | +8.29 to +18.72 | +1.92 | 27 / 25 |
| Ground: Area + K + E | +12.55 | +9.58 to +15.66 | +1.78 | 27 / 25 |
| Ground: Nonlinear K and E | +12.12 | +9.09 to +15.24 | +1.71 | 27 / 25 |
| Ground: Both + separate phase slopes | +15.89 | +13.81 to +17.99 | +2.39 | 27 / 25 |
| Ground: Both, Kislovodsk dates | +12.22 | +9.09 to +15.83 | +1.74 | 27 / 27 |
| Ground: Both, joint support | +10.88 | +8.51 to +13.23 | +1.60 | 17 / 8 |

At fixed HMI area in the area-only model, K changes by -1.71% (conditional 95% limits -10.78 to +8.35) and E by -0.46% (-12.43 to +12.12). These null results do not prove equal group structure. At fixed ground area, the changes are +1.75% for K and +2.95% for E, also with intervals that include zero. Responses used as controls have an algebraic zero offset; those rows in the complete output are not scientific evidence.
For H_both, the added-control minus area-only log offset for F10.7 is +0.00452, with conditional limits +0.00231 to +0.00699. The design condition number is 55.4. The main sample contains 1432 common dates.
For A_both, the added-control minus area-only log offset for F10.7 is -0.00678, with conditional limits -0.00884 to -0.00472. The design condition number is 57.1. The main sample contains 1548 common dates.

The added controls do not bring the fitted F10.7 offset close to zero. This result constrains a model in which the number of whole groups and their area concentration account for the observed excess. It does not establish a change in emission from an individual spot. The sum-square and square-root summaries can miss other parts of the area distribution, and monthly averaging can hide nonlinear daily relations.

## Interpretation and limits

The new test narrows the class of simple structural explanations. Redistribution of a fixed total dark area among more groups, as represented by K and E in these models, does not remove the excess. The evidence still allows more plage or network per dark area, different magnetic field geometry, longer persistence of bright structures, changes inside groups, scale drift, and nonlinear responses absent from the model. Stable area and emission scales are assumptions. No physical cause is proved, and no correction to the public sunspot record is derived.

Group assignment itself depends on observers. The positive-day cut and cross-source agreement cut can select a nonrepresentative sample. Group area and HMI total area have different measurement methods, but HMI threshold calibration uses Debrecen, which also enters the ground composite. Ground source changes and the duplicate repair limit independence. The residual-block estimates have only a few independent blocks. The study covers two selected windows, not full cycles and not the 1979-1983 transition. It uses no facular map, group magnetic flux, spot temperature or individual-spot mask. A stable independently measured plage-to-area relation would provide a more direct physical test.

## Reproduction

From an extracted bundle root, use Python 3.12 with NumPy, pandas, SciPy, patsy and Matplotlib. Exact environment versions and seed are in files/environment.json.

```
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets /tmp/group-results /tmp/group-external
```

Both output paths must be outside the signed publication. One process runs all fits, checks only the six named hashes and writes aggregate results and the figure to the first output directory. Record-level daily or monthly derivatives go only to external scratch. No private workspace is required for reproduction. If snapshots are absent, run `python files/retrieve.py /tmp/group-inputs` and use that directory as the data root. Retrieval stops if a provider has changed the declared bytes; exact reproduction then needs the named immutable snapshot. Verify the signed bundle with `sci verify <bundle.zip> --json`.
