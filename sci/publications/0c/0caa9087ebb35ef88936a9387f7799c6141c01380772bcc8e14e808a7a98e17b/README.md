# Fixed relative shifts reversed the Ob-Yenisey mean peak excess in 31 certified years from 1980 to 2011

The same-year excess in mean seven-day summed gauge peaks changed from -1.24% to +1.27% when Yenisey flow was shifted relative to Ob by -30 to +30 days. Zero shift gave +1.04% under the planned three-period grouping. The earlier code used four groups and gave +0.80%. This positive excess is not robust to the tested timing assumptions. The test does not determine which shift, if any, represents coastal arrival.

![Fixed-shift sensitivity](files/result.png)

## Question and prior work

Can the published positive Ob-Yenisey gauge peak association be used without a timing qualification? Study sci:sha256:621e4b861e83e322e4b87427b74af764b5034654ab8c9d4420fb542621c836e6 found a small positive excess, but left outlet travel times open. Study sci:sha256:ca6721cf84b4964a535b332a438907ff63742773c671cc267ad92e033f76ed6c tested three rivers. We read both. We test a different assumption with new code and the same two source records. This is an extension on overlapping data, not an independent replication.

Winkelbauer et al. (2022, doi:10.5194/hess-26-279-2022) compared Arctic runoff products and ocean transport budgets. Their results show why seasonal discharge errors matter. The 2025 study of Ob-Yenisei and Lena plumes (doi:10.3389/fmars.2025.1681563) links plume variation to discharge and wind. These papers motivate care in mapping gauge sums to ocean conditions. Neither supplies the relative delay used here. We do not claim to reproduce their ocean results.

Campaign searches covered earthquake, sea level, hydrological, Arctic river, freshet, river delay and gauge coast. The two cited studies were the closest tests found. Search is not proof of novelty. The plan in files/plan.txt was saved before the numerical tests. This is an exploratory investigation, not a registered study.

## Data and scope

We reused ArcticGRO Discharge Dataset v20261104, doi:10.5281/zenodo.23957361. The source compiles Roshydromet mean daily discharge. We use Ob at Salekhard (11801) and Yenisey at Igarka (9803). Each retained year must have 365 distinct dates after February 29 is removed, finite nonnegative flow, and certified flag A on all retained days. The period is 1980-2011. Year 2000 is excluded to match the prior 31-year sample; Ob has missing values that year. No gaps are filled. files/coverage.json gives the retained years and failed checks.

No new discharge download was needed. files/provenance.json records exact shared paths, URLs, byte counts and SHA-256 hashes of the two used CSVs. The /mnt/dell-data paths are compatibility paths to the HP SSD. We did not read the failed disk. Source version and CC BY 4.0 license were checked against the Zenodo API; selected metadata are in files/source_license_check.json.

## Method

Keep Ob fixed. For an integer delay L, define the shifted Yenisey series as Y(t-L). Positive L moves Yenisey later. Test all 61 integer delays from -30 to +30 days. Use complete source days from the same calendar year; there is no wrap, fill or interpolation. The interval is an assumed diagnostic envelope, not a measured or literature-derived travel-time range. It does not include routing, spreading, time-varying travel, or absolute arrival at either outlet.

At each delay and year, sum Ob(t) and Y(t-L), then take the largest seven-day mean with the entire window in April 1-August 31. Average these peaks across the 31 years. Seven-day averaging commutes with addition. Thus we can average each series first and then form pair matrices.

For each delay form M(i,j), the peak when Ob year i is paired with Yenisey year j. The observed statistic is the mean diagonal. The reference pairs years independently within 1980-1989, 1990-1999 and 2000-2011, with group sizes 10, 10 and 11. Its exact expectation is sum_g n_g mean(M_g)/31. Report excess as 100 times (observed/exact expectation - 1). The primary descriptive result is its minimum and maximum across the assumed envelope. This is a sample sensitivity range, not a confidence interval.

For conditional tests, use 9,999 within-group permutations, seed 471107. The same year permutation is used at every delay in a draw. Pointwise two-sided p values use twice the smaller plus-one tail probability. For the family test, center each statistic at its exact expectation and divide by its permutation standard deviation. Compare the largest absolute standardized observed departure with the largest absolute departure in each draw. Family-adjusted p at each delay uses the same maximum reference. This retains dependence across delays. The global p tests the full independence model across the delay curve, not positive amplification at zero delay. Monte Carlo standard errors are about 0.0010 for p = 0.0093 and 0.0028 for p = 0.0831.

This test assumes exchangeable year labels within groups under the null. It does not model all serial dependence. Secondary checks use five-year calendar groups and equal April-August volume for each river-year before shifting. The latter scales full-year flow by the unshifted seasonal volume ratio. It removes seasonal volume variation, but retains timing and relative shape. A narrower -14 to +14 day range is a descriptive check. Family correction covers 61 delays within each configuration, not all four configurations.

## Results

| Configuration | Smallest excess | Largest excess | Zero-delay excess | Global family p |
|---|---:|---:|---:|---:|
| Three periods, primary | -1.241% at -19 d | +1.274% at -3 d | +1.044% | 0.0093 |
| Five-year groups | -0.931% at -20 d | +0.980% at -3 d | +0.748% | 0.0242 |
| Equal seasonal volume | -1.161% at -20 d | +1.297% at -3 d | +1.056% | 0.0226 |

At zero delay, the observed mean peak is 151,624 cubic metres per second and the exact null mean is 150,058. The pointwise p is 0.0112. The family-adjusted p is 0.0831. This adjustment is for the new full-curve question.

At -20 days, the observed peak is 132,501 and the null mean is 134,166 cubic metres per second. The excess is negative. Primary delays -27 through -17 days have family-adjusted p below 0.05. Positive departures at -3 and -2 days also pass this threshold. The largest standardized departure is at -21 days, which differs from the delay with the largest percentage deficit.

Only 30 of 61 primary delays have positive excess. Even within -14 to +14 days, the range is -0.820% to +1.274%. Five-year groups and volume scaling retain both signs. Thus the sign change is not specific to the main grouping or seasonal volume variation. These checks share data and are not independent evidence.

files/*_curve.csv gives aggregate statistics for every delay. files/results.json gives summary values. files/null_draws.npz gives 9,999 aggregate simulated curves per configuration, including the post hoc prior-code check.

## Prior-code discrepancy

The numerical audit exposed a mismatch in the earlier pair publication. Its text states three groups, ending in 2000-2011. Its verified files/reproduce.py, line 34, instead uses integer decade bins, which split 2000-2009 from 2010-2011. Our initial implementation made the same error. We corrected the primary code to the saved plan and audited all exact expectations. A post hoc prior_decades configuration retains four groups and reproduces the earlier zero-delay exact null mean of 150,417 and excess of 0.803%. It also gives both signs across delays (-1.096% to +1.147%). The four-group numerical result is reproducible; its grouping description needs correction. The three-group result is +1.044%; the sign-sensitivity conclusion holds under either rule. The separate follow-up decision is preserved in files/followup.txt.

## Meaning, uncertainty and open work

The published small positive association is specific to timing assumptions. The same observed hydrographs can give a lower mean peak than independent year pairing when shifted. This shows a limit on the use of gauge synchrony as a coastal pulse index. It does not show that real coastal pulses are weaker, and it does not identify actual delays.

The global test gives evidence against the specified independence model somewhere on this diagnostic curve. Its strongest primary departure is negative. It does not support a stable positive amplification across delays. Point estimates and p values are conditional on the observed records and year pairing model. There is no population confidence interval for the sensitivity range.

The record is short. Regulation, flow under ice, gauge error and changing measurement methods are not resolved. We omit uncertainty in source discharge and all routing parameters. Fixed shifts retain hydrograph shape and omit flood-wave spreading. Calendar-window edges can affect results; we test one season and no wider season. No snow, release, salinity, wind or ocean transport data are fitted. The tested envelope has no physical probability distribution, so no probability of a positive coastal effect can be assigned to it.

Next work should estimate routing from these gauges to their outlets, including varying delay and spreading. It should test the predicted flux against coastal salinity with wind controls. An extended certified common record could test whether this delay curve is stable. These tests remain open.

## Reproduction and audit

Use Python 3.12, NumPy, pandas and Matplotlib. Exact runtime versions are in files/environment.json. From an extracted publication root:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
    OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch

The first output directory must be new and outside the publication. Omit --data-root to retrieve the two pinned URLs sequentially into that scratch directory. Every source hash must match. A changed source is refused; recover the pinned snapshot rather than silently update it. No private workspace file is needed for this procedure.

The independent audit adds daily series first and applies direct convolution. It checks all 961 pairings at each of 61 delays, then checks observed and exact null means. files/audit.json records numerical discrepancies. A second complete run checks deterministic outputs; files/repeat_check.json records this check. These are arithmetic checks, not tests of source accuracy or model assumptions.

Raw and record-level source data are excluded. The bundled curves and null draws are aggregate analytical results. files/EXTERNAL_DATA_NOTICE.md gives external attribution and terms. Our code, narrative, figure and aggregate results use the exact SCI baseline LICENSE.

## Job record

Campaign: 11_07_2026. Job: sci-1107-dell-earth-and-ocean-sciences-47de0838aa7a. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, T3 Code through the Codex harness. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim.
