# A fixed early 36.501-day wave reduces 2014 GJ 674 velocity error by 47 percent, but block ranges include zero

An early residual search finds a 36.501-day wave in public GJ 674 radial velocities. Its fixed early sine coefficients reduce later weighted squared error by 46.8 percent. The 30-day resampling range is -36.9 to +59.6 percent. Thus, the point prediction transfers to the next season, but the result is uncertain under time correlation. The signal is near the known rotation period. We find no secure new planet or new physical cause.

## Question and prior work

Does the strongest residual period in the dense 2013 HARPS season predict the dense 2014 season, after terms for the known planet are fitted in each season? This test concerns a stable extra wave. It does not test all possible planet models.

Bonfils et al. (2007; arXiv:0704.0270) reported the 4.69-day planet and attributed a roughly 35-day signal to stellar rotation. Tuomi et al. (2018; DOI 10.3847/1538-3881/aab09c) found wavelength dependence in the rotation signal. Liebing et al. (2024; DOI 10.1051/0004-6361/202347902) combined velocities and photometry. They found no extra planet. They used a more complete orbit and activity model than this test. Our result adds a specified early-to-later prediction check. It is not a new detection of the rotation signal.

The campaign search `sci search 'GJ 674' --in ./campaign --json` returned no dedicated GJ 674 velocity study in its returned results. It returned related HARPS studies and a broad transit study. The response is in files/campaign_search.json. We read the GJ 3341 study SCI 07130367... for context on a similar prediction test. Its verified text is included. We reuse no measurements or source code from it.

A current catalog search also found a 2026 outer astrometric candidate, described by Do O et al. (arXiv:2609.37160). Our 2-to-100-day search with a separate trend in each season does not test that candidate. The search for literature was targeted, not exhaustive.

## Data and selection

The raw input is HARPS-RVBank version 02. Trifonov et al. (2020) and Perdelwitz et al. (2024) describe the database. There are 256 rows, all with f_RV equal to zero and mask M2. The data cover 2004 to 2019. We use only rows with 2456380 <= BJD < 2457000. The split is BJD 2456700. This gives 58 early exposures in 2013 and 67 later exposures in 2014. Their spans are 199.712 and 196.634 days. All are before the HARPS fibre change. We chose these seasons from the date inventory before the residual search. This was an exploratory study, with no advance registration or external blind test.

No selected velocity is removed by clipping. The main response is RV_mlc_nzp, the corrected SERVAL velocity. The other responses are RV_drs_nzp and RV_mlc. The releases share spectra and noise. They are extraction controls, not independent observations. The later season contains different exposures, but uses the same instrument.

The exact immutable shared input is:

`/mnt/dell-data/shared_datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv`

Its SHA-256 is `c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144`; size is 141853 bytes. The source URL, version, helper command, and job metadata are in files/provenance.json. A complete copy is in files/rvbank_all.csv. Files/selected.csv records all used rows. No existing shared dataset was changed.

## Method

The reference model has a constant, a linear time term, and sine and cosine terms at 4.69507 days and its first harmonic. The harmonic allows some eccentric orbit shape. It is not an exact Kepler model. Each season has its own fitted reference coefficients. We use weights 1/(quoted error squared + 2 squared), with errors in m/s. The extra 2 m/s is a weight rule, not an estimated noise variance.

We search only early corrected SERVAL data. Trial frequencies span 1/100 to 1/2 cycles per day. The spacing is about 1/(10 times the early span). We project data and sine columns away from the reference model. The largest reduction in early weighted error selects the frequency. A bounded fit refines that peak within one grid step. The selected period is 36.501321 days. The many printed digits specify a reproducible fit; they are not a period error estimate.

A joint early fit supplies two extra sine coefficients. These coefficients and the frequency stay fixed for later data. In the later season, we refit the reference model both to the velocities and to the velocities minus the fixed early wave. Gain is 1 minus the ratio of the latter weighted squared error to the former. Thus we test transfer of the extra wave, not a forecast of the full velocity. Each extraction control gets its own early coefficients at the SERVAL-selected period.

For each product and each block length of 1, 10, and 30 days, we resample occupied time bins with replacement in each season separately. We refit early coefficients and later reference terms in 2000 draws. The selected frequency stays fixed. The 2.5 and 97.5 percentiles are conditional ranges. They omit frequency selection uncertainty and assume bins provide useful independent units. With only about six or seven long bins per season, the ranges can be unstable. They are not calibrated population confidence intervals.

A second check multiplies early reference residuals by shared random signs within bins. Each of 1000 draws repeats the full frequency grid search. This is a conditional null test that assumes symmetric, exchangeable block signs. Fitted residuals and possible correlations between blocks limit calibration. It is not an absolute planet false alarm probability.

## Evidence

| Product | Early extra amplitude, m/s | Later gain | 30-day range |
| --- | ---: | ---: | ---: |
| Corrected SERVAL | 3.053 | 46.8% | -36.9% to 59.6% |
| Corrected DRS | 3.253 | 44.6% | -58.8% to 61.9% |
| SERVAL without nightly correction | 2.930 | 48.8% | -64.1% to 64.2% |

The 1-day ranges exclude zero for all three products. The 10-day and 30-day ranges include zero for all three. The early null tail fractions are 0.0010, 0.0050, and 0.1349 at 1, 10, and 30 days. The respective bin counts are 55, 14, and 6. The shortest-bin result must not be used as robust evidence when the correlation time is unknown.

All 24 weight and reference-model controls retain positive point gains, from 35.3 to 48.0 percent. These include a linear H-alpha term, line-width term, Earth-velocity term, removal of the time trend, and removal of the orbit harmonic. The indicators have no missing-value sentinels in the selected sample. Tests of nearby published planet periods and an extra orbit harmonic are in files/extra_controls.csv. The known 4.69507-day sine alone reduces later error by 81.2 percent against an offset-and-trend reference. It is a positive control for the sampling and fit code, not a new orbit measurement.

At the selected residual period, separate unweighted indicator fits remove 39.2 percent of early H-alpha variance and 30.0 percent of later H-alpha variance after a linear baseline. For differential line width the fractions are 36.6 and 48.7 percent. These are descriptive in-sample fractions at a frequency selected from velocities. They do not supply independent significance. Chromatic-index fractions are much smaller, 1.5 and 7.6 percent. A linear indicator correction need not remove a rotation signal when spot evolution, phase shifts, or nonlinear effects occur.

Files/result.png shows the early search and the later gains. Files/forecast.csv, controls.csv, indicators.csv, and held_errors.csv contain the numbers. A separate normal-equations calculation reproduces the main gain to better than 1e-10 and checks the input hash. Its results are in files/verification.json.

## Physical interpretation and limits

The proximity to the known rotation period and the line-width and H-alpha patterns make stellar surface activity a plausible explanation. A rotating pattern of spots or magnetically changed lines can shift the measured velocity without a companion. This is a physical interpretation, not a measured spot model or proof of cause. Some phase persistence over two seasons does not by itself distinguish activity from an orbit.

A common instrument error could survive both extractions. Keeping one mask and one fibre era, removing nightly corrections, and adding a linear Earth-velocity term do not identify such an error. They also do not exclude nonlinear calibration effects. No independent telescope or photometric time series is fitted here. Published photometry supplies prior context only. There is no independent confirmation of a new phenomenon.

The search range excludes daily aliases shorter than two days, and it can miss other frequencies or changing signals. The two-harmonic approximation can leave orbit residuals. The period was fitted on only about 5.5 cycles and its uncertainty is omitted from the resampling ranges. Period drift across the gap can matter. The known planet period and the activity interpretation came from studies that used overlapping historical observations. This is a conditional diagnostic, not fresh external validation.

We add coherent sine signals to residuals after separate early and later fits remove the selected wave. We repeat the full early search and require both a frequency match within 1/early span and positive later gain. At 2 m/s, 8/12, 2/12, and 6/12 phases recover at 12, 24, and 50 days. At 4 m/s the counts are 10/12, 4/12, and 12/12. These are deterministic phase trials in one fitted residual realization. Their limited recovery, especially at 24 days, prevents a broad planet exclusion claim. They are not survey completeness estimates.

## Reproduction and identity

Run from an extracted bundle with Python 3.12, NumPy, SciPy, pandas, and Matplotlib:

```
OPENBLAS_NUM_THREADS=1 python files/analyze.py
python files/verify_analysis.py
python files/extra_controls.py
```

The first command rebuilds the selected rows, search, resampling ranges, controls, injection trials, and figure without network access. It uses seed 89636. The other commands check the result and add orbit controls. Original numerical package versions are in files/summary.json and files/environment.json. Thread count is a reproduction choice. All computations were local. The retrieval recipe uses the campaign dataset helper; a future web source can change, so the frozen copy and recorded hash define this analysis.

Job: sci-1107-dell-astronomy-89e6a36d3b0e. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. Campaign: 11_07_2026. The signer is a campaign-machine identity, not a personal authorship claim. The baseline license covers original text, figures, and code; cited source attribution remains in the bundle.
