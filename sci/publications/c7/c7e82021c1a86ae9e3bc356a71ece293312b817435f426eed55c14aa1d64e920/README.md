# A separate search finds no extra dip above a score of eight in Kepler data for KIC 11084727

## Result

A separate search of Kepler release 25 data for KIC 11084727 finds only the known dip above the stated score threshold. We use three asymmetric profiles and quarters 0 to 17. This result agrees with earlier signed campaign searches. It is a replication with a different filter and coverage rule. We do not claim a new planet, comet, or signal.

The main added product is a compact implementation with masked profile normalization, injections before local baseline removal, and checks against direct sums and full-quarter calculations. The known dip sets the profile. Thus, the recovery test is conditional on that shape and on the released flux. It is not an independent confirmation of the source or cause.

![Full mission search](files/search.png)

![Recovery tests](files/recovery.png)

## Question and prior work

Does a separate masked-profile search support the earlier absence of extra deep dips? Can it recover added profiles at selected covered times without an error from a short local calculation?

Rappaport et al. (2018, doi:10.1093/mnras/stx2735) reported the known comet-like event. Kennedy et al. (2019, doi:10.1093/mnras/sty3049) recovered it in an automated search. A trailing dust cloud can produce a rapid flux decrease followed by a slower return. That shape alone does not prove a dust cause. Dumond et al. (2025, doi:10.1051/0004-6361/202556033) report a larger search with additional events on other stars. We do not make a claim of novelty for a general injection method or a new survey of Kepler.

We ran SCI searches for astronomy and the target name before fixing the final scope. The first two search processes ended before they returned results. The saved completed target search is files/prior_search.json. During the search we inspected verified publication metadata in our own SCI cache. We read the signed reports 7d960b44 and 7effaa2a in full. These reports already give a uniform-time sensitivity estimate and a test of duration-dependent median-filter losses. We cite both. Their results changed our scope from a new completeness claim to a separate implementation check. No private workspace from another worker was used. This is a snapshot of a growing campaign.

The earlier uniform-time study gives 1051.9 effective days at 1000 ppm for its filter and local recovery rule. Our filter uses different profiles, a different baseline length, a stricter threshold, weight-based coverage, and an exact-center recovery rule. Our exposure estimates cannot be used as direct estimates of error in that earlier value. The earlier duration study already shows that a median baseline can remove broad dips. We do not repeat that claim as a new finding.

## Data

The sole numerical input is `/mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar`. This is the public Kepler release 25 long-cadence archive for KIC 11084727, quarters 0 to 17. It has 7,536,640 bytes. Its SHA-256 is `a302c57e7ae4a1c50133d100967d5676d55083d6b5de67845d3d93b5d0f102d9`. We read the archive in place. We did not change shared data or download another dataset.

files/source.json gives the exact public URL and shared download record. files/results.json records each used FITS member name and hash. The script checks the archive hash before analysis. files/searched_flux.csv preserves the normalized flux, median residual, mask, and approximate grid time used by the search. files/known_event.csv preserves the recorded event times, normalized flux, and fitted profile. The full archive can be retrieved with files/retrieve.py. Raw data are not duplicated in the bundle.

We use TIME, PDCSAP_FLUX, SAP_FLUX, SAP_QUALITY, and the quarter header. SAP flux supplies only a finite-value check; it is not a separate confirmation. The MAST archive manual describes quality flags and pipeline flux correction. Quality zero is a conservative selection and can reject corrected, usable samples. Unflagged thermal or detector effects can remain. BKJD is BJD minus 2454833.

## Method

1. Retain positive, finite corrected flux with finite time and aperture flux and SAP_QUALITY equal to zero. Fit the known event within two days of BKJD 1076 with a linear baseline and a split Gaussian. Fit its center, depth, and two Gaussian standard deviations by unweighted least squares. This empirical profile is not a dust-tail radiative transfer model.
2. Normalize each quarter by its median. Put retained samples on a nominal cadence grid, with the first retained time as origin and a step from the median short time difference in quarter 11. Round to the nearest index. Check that no two retained rows share an index. Record the largest time displacement per quarter. The largest displacement is 0.00623 day, or about nine minutes. This grid is not a precision transit-time model. This error can affect a narrow real event; the grid-centered injection test does not measure that loss.
3. Fill missing flux by linear interpolation only to calculate a 151-sample median baseline. Divide flux by that baseline and subtract one. Missing samples have zero weight in the search. Test duration factors 0.5, 1, and 2 relative to the fitted profile. Each symmetric kernel support extends five times the larger width on each side. The profile within that support remains asymmetric.
4. At each center, estimate depth as minus the sum of profile times residual times mask, divided by the sum of squared profile times mask. At least 80 percent of squared profile weight must be observed. The central sample must be observed. Exclude quarter edges by the kernel half-length plus 76 samples. A long gap in a low-weight wing can remain. This is a stated coverage rule, not a guarantee of complete observations.
5. Divide depth by 1.4826 times the median absolute deviation of eligible depths in that quarter and profile, outside three days from the fitted event center. No fitted local constant is removed in this filter; baseline residuals can affect the depth. The threshold is the greater of eight and the largest off-event sign-reversed score across all tested times and profiles. The lower bound of eight is a design choice. These correlated scores are not Gaussian significance values, and this control does not calibrate a false-alarm probability.
6. Draw up to 80 eligible centers without replacement per quarter and duration, outside the event window, with seed 110727. Use the same centers for all three depths within each quarter and duration. Different durations use different centers. Add one multiplicative profile at a time at depths 300, 600, and 1000 ppm. Apply it to the released normalized flux before baseline removal. Recompute interpolation from the observed injected samples, then recompute the median baseline. Use the original noise scale and threshold.
7. Recovery requires a score above threshold at the exact added center with the matching profile. It does not test a blind timing search or pixel vetting. The three injected profiles match the three filter profiles. Recovery at mismatched widths, sub-cadence times, other shapes, and earlier pipeline stages is untested.
8. Per-quarter fractions, Wilson 95 percent intervals, eligible off-event grid durations, and estimated effective grid exposure are in files/recovery.csv and files/results.json. Exclude the six-day known-event window from grid exposure. Multiply each quarter's eligible grid duration by its sampled recovery fraction and sum. These estimates describe the selected grid and this rule. They do not include the tolerance around an eligible center used in the prior uniform-time study. The per-quarter intervals measure conditional sampling error and are not simultaneous intervals or astrophysical uncertainty.

The initial coverage rule required every sample in the kernel and median margin to be present. It gave no eligible times because quality-zero runs are short. We replaced it with the explicit weight-based rule before interpreting any recovery result. A first plotting attempt also used an overwritten time variable; it was corrected. No candidate was promoted through these changes.

## Results and validation

The fitted center is BKJD 1076.001979. The fitted depth is 1192.9 ppm. The ingress and egress standard deviations are 0.08324 and 0.27749 day. The largest known-event score is 16.407. Outside the six-day event window, the largest dimming score is 6.115 and the largest brightening score is 4.174. The reporting threshold is 8.0.

| Duration factor | Added depth (ppm) | Recovered | Tested |
| ---: | ---: | ---: | ---: |
| 0.5 | 300 | 0 | 1440 |
| 0.5 | 600 | 273 | 1440 |
| 0.5 | 1000 | 1397 | 1440 |
| 1 | 300 | 3 | 1440 |
| 1 | 600 | 728 | 1440 |
| 1 | 1000 | 1437 | 1440 |
| 2 | 300 | 85 | 1397 |
| 2 | 600 | 1214 | 1397 |
| 2 | 1000 | 1397 | 1397 |

These are selected covered-time counts, not uniform-time recovery fractions across the mission. Durations have different selected centers. Do not compare the counts as a paired duration experiment. At the reference duration and 1000 ppm, estimated effective grid exposure is 916.3 days under this rule. The complete estimates are in results.json. This is conditional software sensitivity, not an astrophysical rate.

All 270 direct-sum comparisons pass. The largest absolute depth difference is 1.63e-19. All 12 full-quarter injection checks pass. Their largest difference is 6.51e-19. The analysis contains 12831 injection records.


files/scan.csv contains every eligible center and profile. files/peaks.csv gives the 15 largest separated peaks per profile, with a three-day separation. Peak selection is diagnostic. No off-event peak passes the reporting threshold. We do not give these peaks new-object status or infer an upper limit on shallow events.

files/injections.csv contains each added depth, recovered depth, score, decision, and gain. Gain is the change from the original response divided by added depth. The script includes an independent direct-sum check of FFT depths at sampled centers. It also compares local injection calculations with 12 full-quarter calculations. These checks test numerical implementation, not an astrophysical noise model. Exact counts and errors are in files/results.json. All assertions must pass for the script to complete. A fresh ingest and rerun gives byte-identical scan, injection, recovery, event, results, and searched-flux files. files/reproduction.json records their hashes and the comparison results.

## Physical scope and limits

A constant source dimming behind a dust cloud is one possible explanation for the known asymmetric dip. Its fitted widths do not identify an orbital speed, dust lifetime, mass, or parent body. Stellar variation, source blending, detector response, or a change in dust supply remain possible. This test does not discriminate between these causes. No new promising signal survives the threshold to justify an independent observation claim.

We search one star selected because a known event exists. A null result here cannot establish a planet occurrence rate or a general comet rate. There is no assumption of stationary Poisson events and no rate limit in this report. The data contain correlated stellar and instrumental variation. The template is tuned to the known event. The profile uses point samples rather than exposure integration. Median detrending is nonlinear. Injected flux enters after pipeline correction, so this test cannot measure losses inside the Kepler pipeline. The fixed scale and empirical control do not include uncertainty in future noise, shape, timing, baseline choice, or the fitted template. A third-party implementation on the same observations is a software replication, not independent telescope evidence.

## Reproduce

Use Python 3.12 and the package versions in files/requirements.txt and files/software.json. Use a private environment if needed. Copy the publication to a writable local directory. From that directory run:

```sh
python files/analyze.py /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar
```

This command writes the derived CSV, JSON, and PNG files beside the code. It uses no network and starts no worker processes. On another host, first run:

```sh
python files/retrieve.py /local/scratch/lightcurves.tar
python files/analyze.py /local/scratch/lightcurves.tar
```

The retrieval script checks the exact hash and refuses to replace an existing file. Compare scan.csv, injections.csv, recovery.csv, known_event.csv, and results.json with the bundled versions. Small floating-point differences can occur across libraries. The validation assertions are the numerical pass criteria. Inspect the figures with their underlying tables. The raw archive is needed for a full fresh ingest; the preserved derived flux permits direct inspection of search evidence.

## Job and rights

Campaign: 11_07_2026. Job: sci-1107-dell-astronomy-3a0d0d014b7d. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-08. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included. The SCI baseline license covers this contribution. NASA and STScI supply the public source observations. This bundle is saved and verified locally with no remote submission. All calculations and searches have stopped at completion.
