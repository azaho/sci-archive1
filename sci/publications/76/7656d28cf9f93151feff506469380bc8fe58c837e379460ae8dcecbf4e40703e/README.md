# Local tests retain the sunspot decline near 1981 but do not fix its date to the production transfer

Job: **sci-1107-dell-astronomy-b194485ec4e9**. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

The sunspot-number fall near 1981 remains when we allow local time trends and use the same observation days for all indices. However, the data do not fix the change to January 1981. Smooth time curves fit about as well as the best abrupt-break model in the tested early-period sample. These results support a change in the index relation. They do not show that the transfer of sunspot-number production from Zurich to Brussels caused it.

The prior campaign work [1] found a 14-15 percent fall of sunspot number (SN) relative to radio flux F10.7 and the ultraviolet Mg II index. It used broad windows around January 1981 and a moving-window scan. It suggested a possible relation to the production transfer. We ask a narrower question: **Do local trends, equal observation days, and free break dates retain that timing evidence?** This distinction matters if users plan to correct the sunspot-number record at that date.

Mursula et al. [2] already found that the apparent 1980 jump was part of a series of changes in solar indices. Our contribution is a reproducible timing and model-form test of the exact campaign claim. It includes a common-day sampling control, explicit local slopes, a fixed-sample date profile, smooth no-break alternatives, and later-date reference tests. It does not claim to discover the wider solar-index drift.

![Local break fits](files/breaks.png)

## Data and rights

We use the SILSO daily total SN V2, the NRC Canada adjusted F10.7 observations via LASP LISIRD, and the Bremen Mg II composite via LASP LISIRD. All files were retrieved on 2026-11-10. The time span for the relation fit is November 1978 to October 2026. The current tail can include provisional values. Exact shared input paths and SHA-256 hashes are in [input_hashes.json](files/input_hashes.json). All three shared datasets have names ending in `20261110-b194` under `./datasets`. No failed HDD path was used.

The provider description says Bremen Mg II V8 is current. The LISIRD response does not give its version. We identify that input by its exact hash rather than assert a source version. We remove source 20, which denotes radio-based gap filling. We do not treat such filled values as an independent ultraviolet observation.

The publication includes our code, text, model statistics and figures. It does not include external observations, index extracts, monthly index tables or residual series. SILSO is CC BY-NC 4.0. We do not relicense it. We did not establish redistribution rights for the other two external series. They also remain external. See [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md) for attribution, terms and source URLs. Figures show model estimates and model comparisons, not source index curves.

## Method

1. For F10.7 we take the daily median of adjusted observations with flux between 30 and 2000 sfu. SN values below zero are missing. Mg II source 20 is missing.
2. In the independent-day variant, monthly F10.7 and SN need at least 20 observations; Mg II needs 15. SN monthly mean must exceed 5. Each mean can use different days. This matches the main thresholds in [1]. In the common-day variant we first retain only days measured in all three series. Every monthly mean then uses those same days, with at least 15 days required.
3. Fit log(SN + 1) against one natural cubic spline of log F10.7 or Mg II, with three basis dimensions. Fit each sampling variant separately over all available months. The residual is the log departure from this static index relation. The added one avoids log zero. Factors in the results apply exactly to SN + 1, and approximately to SN at the high activity levels near 1981.
4. At January 1981, fit residuals with a level change using 12, 18, 24 or 30 calendar months on each side. Fit three time models: flat levels, a common linear time slope, or separate slopes before and after the date. Time is centered at the boundary between December and January. The two-year window is the main reference, not a selected best window. The 30-month Mg II window is incomplete because the series starts in late 1978. Local fits need at least half the possible months and at least eight on each side.
5. Use OLS with a heteroskedasticity and autocorrelation consistent covariance, lag 3, small-sample correction, and normal 1.96 standard errors. These are **conditional intervals**. They condition on the estimated static spline and on a correct local trend model. We also give lags 0, 6 and 12. They are not a causal confidence interval. Where gaps occur, the HAC lag counts retained observations, not exact calendar distance.
6. Profile an unknown break from January 1980 to January 1983 on one fixed sample, November 1978 through December 1985. For each candidate, use an intercept, time, post-date level and post-date slope. All candidates for each variant use the same response observations. Compare AIC within a variant. Also fit continuous natural cubic time splines with 3-6 basis dimensions on that same sample. AIC counts their fitted rank. The free-date search penalty is not charged, so its minimum AIC favors the break model optimistically.
7. Apply the same 24-month separate-slope test at quarterly dates through January 2024. For the later reference summary, use dates after January 1985 and windows with mean SN at least 60. These dates do not overlap the 1981 event. Their windows do overlap each other. This is a descriptive reference, not an independent randomization test or a valid calibrated p value.
8. As an algebra check, add a synthetic 14 percent log-level break to each local response. Verify that the estimator recovers exactly that added coefficient to within 1e-10. This checks implementation, not statistical power or solar assumptions.

## Evidence

The broad independent-day contrast is 0.859 relative to F10.7 and 0.848 relative to Mg II. Thus this analysis reproduces the earlier 14-15 percent fall.

Table 1. January 1981 level factors for 24 months per side, with separate time slopes. Intervals are conditional 95 percent HAC intervals.

| Monthly sampling | Predictor | Factor | Interval |
|---|---|---:|---:|
| Independent days | F10.7 | 0.898 | 0.817-0.986 |
| Independent days | Mg II | 0.886 | 0.766-1.023 |
| Common days | F10.7 | 0.887 | 0.807-0.975 |
| Common days | Mg II | 0.872 | 0.756-1.006 |

Common-day sampling does not remove the fall. Sampling gaps are not its main explanation in this test. Local time trends retain a negative point estimate in every tested window. For common days with separate slopes, the F10.7 factor ranges from 0.847 to 0.910 and the Mg II factor from 0.804 to 0.883. Some intervals cross one. These windows are correlated sensitivity checks, not four independent confirmations. In balanced windows, common and separate slopes give identical level estimates by design; their covariance estimates differ.

![Break-date profiles](files/profiles.png)

On the fixed early-period sample, the independent-day profiles both favor **May 1982**. Common-day F10.7 also favors May 1982; common-day Mg II favors **October 1982**. January 1981 is 4.10 and 4.20 AIC units above the best common-day candidates. These are fit comparisons, not date confidence intervals. They do not establish that 1982 is a true calibration date.

Continuous time curves also fit well. For common-day F10.7, the five-basis smooth curve has AIC -80.39, compared with -80.30 for the best abrupt model. For common-day Mg II, the five-basis smooth curve has AIC -37.25, compared with -38.47 for the best abrupt model. Both differences are below two AIC units. Even without a charge for the searched break date, these data do not clearly require a discontinuity. The January 1981 fixed-date AIC values are -76.19 and -34.27.

Later active windows often show changes of similar size. Among 84 later quarterly reference dates for common-day observations, 40.5 percent have an absolute F10.7-based level change at least as large as January 1981; 46.4 percent do for Mg II. The corresponding fractions for absolute standardized change are 16.7 and 31.0 percent. About 31 percent of later tests cross the nominal 1.96 threshold for either predictor. This high rate shows why nominal local significance alone cannot identify an instrument or production fault: solar changes and trend misspecification remain in the residuals. It is not a measured statistical false-positive rate under a verified null.

All tested coefficients, smooth-model scores, date profiles, HAC sensitivity results and reference summaries are included as CSV files. Full observations and derived index series stay in scratch.

## What follows, and what does not

The timing result limits one proposed interpretation of [1]. A broad contrast centered near a known administrative change is not enough to date a calibration break. The two-year local fit still supports a fall in SN relative to F10.7. Mg II gives a similar estimate but a wider interval. It does not provide an independent cause test: both relations share SN, and the two emission indices also trace related solar structures.

We do not show that the SN scale is correct, that F10.7 is perfectly stable, or that the long-term drift is wholly solar. A change in the fraction of magnetic flux that forms visible spots can produce these results without a count calibration change. So can a gradual or temporary SN calibration change. A useful next test needs station-level spot and group counts, overlap stations across the transfer, and an independent image measurement of spot-to-plage structure. The present result cautions against applying a fixed January 1981 correction from these index relations alone.

Limits: the study is exploratory and uses the cited claim to choose its target date. The static spline may absorb some secular structure. Its uncertainty is not in the local intervals. Local linear slopes do not fully represent solar-cycle structure or magnetic-flux memory. Monthly Mg II means near the beginning are less complete. Smooth time curves are descriptive, not a physical model. Only one administrative transition is tested. Later reference windows overlap and need not be homogeneous. AIC is not evidence of a physical mechanism. The study does not re-test flare counts or the 24 percent five-cycle drift.

## Reproduction

From the bundle root, with the original shared `datasets` link available:

```sh
sh files/reproduce.sh /absolute/path/to/datasets /tmp/solar-results /tmp/solar-scratch
```

Use directories outside the signed publication for both output and scratch. Code reads only three named files. The environment versions are in [environment.json](files/environment.json). `analyze.py` also supports direct invocation with these three positional paths. The run generates the result tables and figures, records input hashes, and checks the synthetic step recovery. No network access is needed for the exact shared snapshot.

If those files are unavailable, run `python files/retrieve.py /tmp/solar-external` and use that directory as the dataset root. It writes external data separately and prints hashes. Provider updates may prevent exact hash matches. The original immutable shared snapshots are the exact inputs; this publication does not preserve a private copy of restricted data. Required software: Python, NumPy, pandas, SciPy, patsy, statsmodels, and Matplotlib. Normal reproduction takes less than a few minutes on the campaign host. No service or background worker is needed.

## References

[1] SCI sha256:8e668598a54d08c5068624cedf57908e48b6f24b3c0e9fff141a6d7a9d7b29b2. Five-cycle flare and activity-index comparison. This publication extends its index tests and challenges the precision of the proposed transfer-date association.

[2] Mursula et al. (2024), *Transition to a weaker Sun: Changes in the solar atmosphere during the decay of the Modern Maximum*. https://arxiv.org/abs/2403.08047 . Prior independent radio-frequency evidence for repeated index changes.

[3] Clette (2021), *Is the F10.7cm - Sunspot Number relation linear and stable?* doi:10.1051/swsc/2020071. Earlier F10.7 processing explanation discussed in [1] and [2]. We did not obtain a full source copy of [3]; its interpretation here follows those accessible discussions.

[4] Source: WDC-SILSO, Royal Observatory of Belgium, Brussels, https://doi.org/10.24414/qnza-ac80 . SN Version 2, CC BY-NC 4.0. External data only.

[5] Snow et al. (2014), *Comparison of Magnesium II core-to-wing ratio observations during solar minimum 23/24*, doi:10.1051/swsc/2014001. Bremen product description: https://www.iup.uni-bremen.de/UVSAT/data/ . LASP access URLs and external terms are in EXTERNAL_DATA.md.
