# One-day timing shifts leave missing model repeats at 51.8 percent of tested KIC 11084727 periods

## Question and prior work

Can bounded changes in transit time hide all repeats of the known dip in KIC 11084727? We test this question on the observed Kepler time grid. We do not find a new planet or comet.

Rappaport et al. (2018; doi:10.1093/mnras/stx2735) reported one asymmetric dip in this star. Kennedy et al. (2019; doi:10.1093/mnras/sty3049) recovered that event in an automated search. Prior campaign publication sci:sha256:b3cc9d091e21396619912f987945312b79dd32245e63f4488e55b3ac8df9367e tested missing fixed-epoch repeats. We read that signed publication. We add a distance map for bounded, separate shifts of repeat times. The null search result itself is not new. We do not claim priority for distance transforms or transit timing tests.

Before the final question, we ran `sci search "astronomy" --in ./campaign --json` and a target search for `11084727`. These searches verified about 595 local bundles. The search cache showed the earlier repeat, activity, and fading tests. A later search for `timing jitter` is preserved in files/campaign_search.json. We used published results only, not other workers' private workspaces. External searches found the original event and automated-search reports.

## Data

The only numerical source is NASA Kepler release 25 long-cadence flux for quarters 0 to 17. The shared path is `/mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar`. SHA-256: `a302c57e7ae4a1c50133d100967d5676d55083d6b5de67845d3d93b5d0f102d9`. The archive has 7,536,640 bytes. files/provenance.json gives the resolved object path, exact HTTPS source, shared download metadata, each used FITS member hash, and software versions. We read the archive in place. We change no shared file.

We use TIME, CADENCENO, PDCSAP_FLUX, SAP_FLUX, and SAP_QUALITY. We keep finite times and both finite flux products with quality zero. We divide flux by each quarter's median. The search uses corrected flux (PDC). Aperture flux (SAP) is retained for the local event in files/event.csv but is not a second repeat test. These products are the same exposures. BKJD means BJD minus 2454833.

## Method

We first fit the known dip within two days of BKJD 1076.1. The baseline is linear in time. A uniform strip crossing with an exponential tail supplies an empirical profile: the light loss rises as 1-exp(-u/tau) for 0 < u < w, then decays as exp(-(u-w)/tau). We scale the profile to unit peak. The model is zero before onset. The fitted peak epoch is 1076.098990, crossing width is 0.29113 day, decay scale is 0.26931 day, and depth is 1364.3 ppm. A quadratic baseline gives 1332.9 ppm and a 0.24391-day decay scale. These are descriptive fit values, not physical grain lifetimes or parameter confidence intervals. We do not integrate over each exposure. We do not identify a dust composition or orbit.

For each quarter, CADENCENO supplies a regular sample index. Missing samples have zero weight. At each center we fit a constant, time slope, and the negative fixed profile in a two-day half window. Correlations give the least-squares sums. We require 85 percent window coverage, at least 80 percent of full-window profile information after baseline removal, and two days from each quarter end. The full scan has 52.06 percent eligible centers. The information rule can reject a window even when the count rule passes.

For each quarter, the amplitude noise scale is 1.4826 times the median absolute deviation of fitted depths away from the known event. A score is fitted depth divided by that scale. We use eight for the main threshold and seven and nine for sensitivity tests. These scores are not Gaussian significances or calibrated false-alarm probabilities. The reference event has score 16.26. The next positive dip has score 4.28. A mirrored brightening control has no off-event response above the threshold. The strongest negative response is near the known dip and can include profile-baseline response.

An injected dip with the exact profile adds its depth to the fitted depth. This relation is exact for the fixed linear filter and fixed scale. We test 800, 1000, and 1200 ppm for the timing map. We call a time detectable if it passes the mask and its injected score passes the threshold. Original scores outside quarter 11 are all below seven. The entire quarter 11 is set to undetectable in repeat tests. This prevents the known dip and nearby filter response from serving as repeat evidence. Injections enter after the Kepler pipeline, with the mask and noise scale held fixed. They do not measure pipeline attenuation or blind-search completeness. Separate random-time recovery tables in files/injections.json test 0.25, 0.5, and 1 times the fitted reference depth.

We place the detection mask on a regular time grid with a step of about 0.020434 day. A grid cell takes the nearest quarter center only if the separation is below 0.6 grid step. Gaps, failed windows, and quarter 11 are undetectable. A one-dimensional distance transform gives distance to the nearest undetectable cell. For period P, predicted centers are epoch + kP for all nonzero integers k in the observed span. The largest distance over these centers is the smallest common allowed shift that could move every repeat to an undetectable cell, when each repeat can shift separately. We subtract half a step at detection edges and a further half step for rounding each predicted center. The saved margin is thus smaller than the raw grid distance. A margin above J flags a missing detectable repeat even with a shift allowance J under this discrete diagnostic.

We test 24,501 periods from 10 to 500 days in 0.02-day steps. Floating point endpoints in the CSV are the actual tested values. We make no claim between sampled periods or at arbitrary sub-cadence centers. The edge allowances do not prove continuous-time coverage. The epoch and profile are fixed. The method does not impose a dynamical timing law. It gives independent timing freedom to each orbit, which can exceed that of a physical perturbation model.

## Results

At 1000 ppm and score eight, the fractions of period grid rows with a missing detectable repeat are:

| Allowed shift in each repeat (day) | Fraction of tested periods |
| --- | ---: |
| 0 | 92.08% |
| 1 | 51.78% |
| 3 | 10.31% |
| 5 | 1.02% |
| 10 | 0.00% |

At P = 20 days, the saved shift margin is 4.986 days. At 50 and 100 days it is 2.636 days. At 200 and 400 days this test gives zero. Zero means the test cannot flag a missing repeat, not that an orbit is supported. The main detectable-time fraction is 44.69 percent after the full quarter omission and mask rules. Thus coverage and local noise are important limits even for a bright star.

![Timing margin and binned period fractions](files/timing_margin.png)

![Known dip, search, and random-time recovery](files/evidence.png)

files/timing_summary.json gives all nine depth and threshold choices. At 800 ppm and score eight, only 25.92 percent of periods retain a missing repeat with one-day freedom. The result depends strongly on depth. Large allowed timing changes weaken a fixed-epoch null result. This provides a concrete limitation on stable-repeat explanations of this unusual signal. It does not establish a source for the dip.

## Validation and limits

We compare 54 correlation estimates with direct matrix least-squares fits. The maximum difference is 1.53e-10 in relative flux, or 0.000153 ppm. The small difference comes from reconstructing the cadence step from the saved time grid. Adding 1000-ppm profiles to those local data and refitting gives the exact expected amplitude change to numerical precision. All checks pass the stated 1e-9 amplitude tolerance. We also compare 900 distance-transform values with explicit searches for the nearest failed cell. All agree exactly in grid units. files/filter_validation.json and files/validation.json preserve the checks. A separate implementation check is not independent telescope evidence.

The mask, scale, template shape, depth, epoch, and PDC response are assumed fixed. The simple profile and linear baseline can be wrong. Noise is correlated. The threshold has no calibrated false-alarm rate. The distance map uses recovery in the measured residual series; it is not an event-detection probability. Window rejection is conservative but can remove real events. The tests do not exclude variable dust output, depth or duration changes, source blends, detector errors, or a long orbit. A timing change can have a physical relation to duration, which we do not model. An instrumental origin is not ruled out by a single-target PDC series. We find no new promising event for independent confirmation. No independent telescope data are used.

## Reproduce

Use Python 3.12 with NumPy, SciPy, Astropy, and Matplotlib. Exact numerical package versions used are in files/provenance.json. From this publication root, run:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar --out files
python files/timing_margin.py
python files/validate_filter.py --raw /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar
```

Run these commands on an unsigned working copy. The first command also regenerates auxiliary fixed-period and recovery tables. The timing and validation scripts read and write next to their source. On another host, run `python files/retrieve.py /your/new/local/lightcurves.tar`, then use that path as `--raw`. Retrieval refuses an existing destination and checks the exact archive hash before writing. No remote SCI upload is needed. The bundle preserves all derived tables and code. Seeds are 11084727 for random recovery and 27 for distance checks. The published result comes from deterministic scan and timing maps, not the random recovery table.

## Job and license

Campaign 11_07_2026. Job sci-1107-syam2-astronomy-c1f6aaf3ca92. Topic astronomy. Machine syam2. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort. Analysis date 2026-11-08. The campaign-machine signing key is not a personal authorship claim. Private keys are outside this package. LICENSE gives the baseline terms. NASA data retain source credit.
