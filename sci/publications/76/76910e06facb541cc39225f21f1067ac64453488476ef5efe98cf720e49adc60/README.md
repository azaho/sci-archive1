# KOI-2700 core transit loss decreases within all four Kepler detector seasons in Q1 to Q16

The core transit loss of KOI-2700 decreases with time after a fit allows a separate offset for each of four detector seasons. All four season slopes are negative. This result supports the known decline against one specific instrument explanation: fixed annual offsets. It does not rule out instrument changes with time. It is not a new planet or a new report of fading.

![Quarter means and season fits](files/trend.png)

Each point is a quarter mean. Each line has the common fitted slope and a separate season offset. SAP is aperture flux. PDC is pipeline-corrected flux. Both use the same exposures. The lines are descriptive fits; they do not require a steady physical decline.

## Result and scope

| Measurement | Slope, ppm per year | Conditional 95 percent interval | Null sign probability |
| --- | ---: | --- | ---: |
| Aperture core loss | -63.67 | [-97.36, -29.98] | 0.00864 |
| Corrected core loss | -73.90 | [-117.02, -30.78] | 0.01297 |
| Aperture loss divided by header target light fraction | -74.51 | [-112.87, -36.15] | See checks.json |
| Aperture control band | -0.72 | [-13.85, 12.41] | 0.915 |
| Corrected control band | -7.29 | [-20.16, 5.58] | 0.309 |

Here ppm means parts per million of local total aperture flux for SAP, and of the local corrected flux for PDC. A year is 365.25 days. The crowding-corrected SAP column is a simple header-based check, not a new image fit. Its uncertainty omits header errors.

The four aperture season slopes are -62.68, -39.37, -66.70, and -84.47 ppm per year for quarter number modulo four equal to 0, 1, 2, and 3. Their detector channels are 59, 67, 27, and 19. Each season has four quarters on one channel. Removing any one quarter leaves the common aperture slope between -75.39 and -55.02 ppm per year. These slope signs are descriptive checks, not four independent significant detections.

Three periods, two local baseline orders, and two flux products give 12 correlated sensitivity tests. Their slopes range from -76.27 to -63.67 ppm per year. Each conditional interval excludes zero. The largest null sign probability is 0.01996. These tests were selected to test measurement stability. They are not a correction for target selection or for all possible archive searches.

## Question and prior work

Can fixed detector-season offsets explain the known decrease in the KOI-2700 transit? Rappaport et al. (2014, DOI 10.1088/0004-637X/784/1/40) already reported a large depth decrease and an asymmetric transit. Garai (2018, DOI 10.1051/0004-6361/201629676) modeled a dust tail. Our added test uses quarter means, common time slopes, and separate season offsets. It directly checks whether the decline persists at repeated detector positions.

Before this test, we searched the campaign for astronomy, exocomet, KOI 2700, and KOI-2700 season. We read publication `sha256:996f37808b0df04ee00816dd83f37aa0530f3e962a7e91ffe10b078883406629`. That work tests tail-to-core changes and includes season splits. We use its documented data path and phase reference. We wrote new code and measured the mission data again. We do not claim that season checks are new in general. Our result concerns the core-loss trend with quarter-level errors, not the earlier shape ratio.

## Data and method

The input is the NASA Kepler release 25 long-cadence tar for KIC 8639908. The exact shared file is `/mnt/dell-data/shared_datasets/koi2700-kepler-dr25-lc-20261109-10edb574/lightcurves.tar`. It is on the campaign HP SSD compatibility path, also reached through `./datasets`. Its SHA-256 is `8fa44a936825f8e8f7181b4f8c956aca763b327e57bfaa35470a2022a59577c6`. Its size is 7,454,720 bytes. The exact source URL is in files/retrieve.py. We reused it in place and made no shared-data changes. We did not access `/data`.

The tar has 17 FITS files. files/members.json records their names, hashes, quarter numbers, channels, release headers, and crowding factors. We use Q1 to Q16 to retain four complete season cycles. Q17 is excluded. All retained samples have finite time and both fluxes, and SAP_QUALITY equal to zero. There is no clipping by flux or measured transit depth.

The main period is 0.9100259 days and the reference time is BKJD 131.9939. BKJD is BJD minus 2454833. The two alternate periods are 0.910022 and 0.910020582 days. These constants follow the earlier campaign work and its source references. We do not estimate a new orbit or search for a new period.

For cycle c = (time - reference)/period, orbit number is floor(c + 0.5), and phase is c minus orbit number. In each orbit we divide flux by the quarter median. We fit a linear baseline outside phase [-0.12, 0.30). We require at least 15 baseline samples, at least five below -0.12, and at least five at or above 0.30. Loss is one minus flux divided by the fitted baseline, times one million. The core band is [-0.045, 0.005). The control band is [-0.245, -0.195). Both need at least two samples. The common sample rule retains 1,148 orbits. The control lies in the baseline region and therefore has a different response and noise level from the core; it is only a diagnostic.

We take an unweighted mean across accepted orbits in each quarter. Then we fit 16 quarter means to four season indicator columns and one time column. The time column is (mean BKJD - 800)/365.25. Each quarter has equal weight. Unequal quarter lengths and sample counts are recorded, not used as weights. There are five fitted coefficients and 11 residual degrees of freedom. The quadratic-baseline sensitivity repeats the whole orbit measurement.

For uncertainty we use a wild residual construction at the quarter level. Let X be the full design, r its residual, h its leverage, and w the last row of the pseudoinverse of X. For all 65,536 quarter sign vectors e, calculate d = sum(w * r / sqrt(1-h) * e). Add the 2.5 and 97.5 percent quantiles of d to the observed slope. For the null test, fit season offsets only, use that model's residuals and leverage, and compare the absolute signed slope with the observed absolute slope. files/analyze.py gives the full calculation. Enumerating signs removes Monte Carlo noise; it does not make this an exact randomization test. Residuals are estimated. Calibration is approximate and assumes independent, symmetric quarter errors and an adequate mean model. Shared annual errors and long time correlations can make these intervals too narrow.

## Checks and physical meaning

The FITS headers confirm that each season uses one fixed channel across the four years. A season offset can absorb a fixed difference in aperture contamination. It cannot absorb contamination or sensitivity that changes with year. Dividing the SAP contrast by CROWDSAP retains a negative trend. The Kepler Archive Manual defines CROWDSAP as the estimated target light fraction and describes the PDC crowding correction. These estimates can be wrong and do not replace pixel tests.

A deterministic signal-transfer test uses the actual accepted sample times and a fixed asymmetric profile. It averages 31 midpoint samples over a 29.4-minute exposure. The profile is `1 / (exp(-x/0.007) + exp(x/0.065))`, with x equal to phase plus 0.02. It passes the same local linear baseline operation. A constant coefficient of 400 ppm gives a spurious fitted slope of +0.84 ppm per year. A coefficient that falls by 60 ppm per year gives a measured core slope of -24.88 ppm per year. The mean core response is 0.4274, so the latter value is near the expected attenuated slope. This is a sampling and baseline transfer test. The coefficient is not the core depth or a fitted physical dust mass. The test uses no random noise and does not measure detection power. A synthetic quarter regression with arbitrary season offsets recovers a known -60 ppm per year slope to better than 1e-8.

In an optically thin, fixed-shape dust screen, less extinction along the line of sight can reduce core loss. A change in dust supply, survival, path, or grain properties could cause such a change. A fixed season offset alone is inadequate under our error model. This test does not choose among physical causes. A time-dependent contaminant or pipeline effect remains possible. Core bands also mix depth, width, and transit-time changes, so this slope is not a mass-loss rate.

We sought independent confirmation in the published campaign result above. Its separate TESS sectors 81 and 82 were too diluted and noisy to confirm a roughly 400 ppm transit. We did not reanalyze those exposures. SAP and PDC agreement is not independent evidence. No new independent instrument detection, new signal, or new source is established here. New sensitive observations with image-based source checks are needed.

## Reproduce and inspect

The signed package contains our code, measured contrasts, aggregate results, checks, and a static figure. Mission FITS data and source papers remain outside it. The baseline license applies to our original material. External attribution and source terms are in files/EXTERNAL_DATA.md. No private key is included.

Use Python 3.12 with files/requirements.txt in a private environment if needed. The recorded run used Python 3.12.16. From an extracted publication root, choose separate local scratch and run:

```bash
python files/retrieve.py --dest /absolute/scratch/koi2700/raw
python files/analyze.py --raw /absolute/scratch/koi2700/raw/lightcurves.tar --out /absolute/scratch/koi2700/output
python files/checks.py --raw /absolute/scratch/koi2700/raw/lightcurves.tar --out /absolute/scratch/koi2700/output
```

On the campaign machine, replace the raw path with the shared path above to avoid a download. The programs refuse output inside the signed package. Retrieval verifies the tar hash and refuses to overwrite a different file. Analysis runs without network access. Results should agree to numerical rounding. Inspect files/results.json, checks.json, orbits.csv and signal_transfer.csv without the raw data. The stored member hashes permit individual FITS checks. The figure uses only our aggregate measurements.

## Campaign record

Job: sci-1107-dell-astronomy-b4026f1dc639. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. Date: 2026-11-09. One finite worker conducted this test with no child agents. The campaign-machine signature records integrity, not personal authorship or external peer review.
