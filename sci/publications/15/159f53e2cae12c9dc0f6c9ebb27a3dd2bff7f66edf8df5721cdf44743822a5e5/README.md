# Five-day Kepler DR25 fits leave 694 of 7241 trial periods without a usable fixed-profile KIC 8027456 repeat at 40 to 402 days

We test exact repeats of the known KIC 8027456 dip in 12 public Kepler release 25 quarters. We fix its published profile and epoch. On a 0.05-day grid from 40 to 402 days, 694 of 7241 trial periods have no usable repeat under a five-day local baseline rule. A 500-parts-per-million profile added at each covered passage passes a fixed empirical screen for at least one passage at 6547 periods. The corresponding count at 300 parts per million is 5843. We test three local windows, halve the period spacing, check raw file hashes, and compare direct linear fits. These are finite window and recovery tests on one corrected data record. They are not orbit exclusions, confidence limits, or evidence for a new planet or comet. Pipeline loss, changing dust output, other profiles, and uncertain repeat times remain possible. No independent telescope confirms an event. Code, selected data, source hashes and offline instructions are included.

## Question and prior work

Can the public Kepler record test fixed-profile repeats of the known KIC 8027456 dip at periods from 40 to 402 days? This question matters when a single dip is used to support a long or eccentric orbit. Gaps can hide events. A random-time recovery fraction does not give a period test when all repeat times depend on one observed time.

Kennedy et al. (2019), DOI 10.1093/mnras/sty3049, reported the known possible comet transit. Their approximate stellar and crossing-time model gave a circular period near 1.1 years. That estimate motivates our 402-day upper test value. We do not derive an orbit from it. The lower bound of 40 days is a chosen test scope. We do not test shorter periods, longer periods, or every real-valued period in the interval.

Campaign publication SCI a374123457a6a62a11980769573864c31484061cf5d29557391091d86855630c searched these 12 quarters with a fixed profile. It found no extra corrected-flux event above a brightening screen. Only 219 of 506 random-time 500-ppm injections passed, mainly because of gaps. We use its selected flux, fitted profile, and fixed screens. We add exact orbital-time fits, period coverage maps, and a finer-grid check. This is an extension of that published search, not an independent event survey.

We ran `sci search "astronomy" --in ./campaign --json` and a Kepler search before choosing the exact question. Both broad searches were stopped after several minutes without output. We inspected published metadata and read relevant published text. A search of a local link to the used bundle completed full checks. files/campaign_search.json and files/prior_verify.json preserve these checks. We did not inspect other workers' private workspaces. The literature search was targeted, not complete.

## Data and fixed model

The shared raw path is `/mnt/dell-data/shared_datasets/kepler-kic8027456-available-quarters-dr25/lightcurves.tar`. Its SHA-256 is `a7d6ad7d5d5662185f25746bb3de4b2acba60de4312a0ecb3de5876f1e77ca0d`. The source is the public MAST mirror on S3. files/prior_provenance.json gives the exact URL, release, all 12 FITS member hashes, and the parent job. files/provenance.json gives this job and the hashes of the used parent files. No shared file was changed or downloaded again.

The data contain quarters 0, 1, 3, 5, 7, 9, 10, 11, 13, 14, 15 and 17, with 35,181 selected rows from BKJD 120.5390 to 1591.0014. BKJD is BJD minus 2454833. Selection uses finite time, corrected flux and corrected-flux error with SAP_QUALITY equal to zero. Each product is divided by its quarter median. Our raw-file check rebuilds all selected time, aperture-flux, corrected-flux and quarter arrays and finds exact agreement. All primary headers state DATA_REL=25. files/raw_validation.json records this test.

We use corrected flux only for the period fits. The parent search found that a large aperture-flux response in quarter 3 set an aperture screen that would miss the known dip. Thus, our recovery statement depends on pipeline correction. Corrected and aperture flux are reductions of the same observations and are not independent observations.

The fixed exposure-averaged split Gaussian has epoch 1448.8633632915487 BKJD, entry width 0.18930128529673612 day and exit width 0.4370976264489895 day. The parent fitted depth is 500.2479 ppm. The widths are Gaussian standard deviations, not contact durations. Nine midpoint samples average each 0.02043365-day exposure. We do not refit these shape values during the period search.

## Exact repeat and recovery rules

For each period P, repeat centers are epoch + n P for all nonzero integers n within the selected time span. The known event is excluded. A local fit uses one quarter, at least 100 rows, and a quadratic time baseline. Both profile wings out to three widths must have at least 70 percent of the nominal cadence count. There must be at least 30 rows before center minus two days and after center plus two days. The profile squared norm after removal of the baseline must exceed one. Half-windows are 4, 5 and 7 days. These are the parent coverage rules. A usable passage can still contain gaps.

Let h be the positive fixed profile and A the polynomial design. We set h_perp = h - A least_squares(A,h). The fitted loss coefficient is -dot(h_perp,flux) / dot(h_perp,h_perp). Positive coefficients mean loss of light. Equal weights match the parent estimator. This estimator is linear. Adding a profile of depth D at its exact fit center increases its coefficient by D. We therefore compute exact individual-injection responses as measured coefficient + D, for D = 300, 500 and 1000 ppm. Each injection is separate; we do not inject all repeats at once. Local windows from distinct passages do not overlap at the tested periods.

A pass means a coefficient strictly above the parent empirical screen: about 261.9, 292.7 and 304.2 ppm for 4, 5 and 7 days. Code reads the exact values in files/prior_summary.json. Those screens are the largest brightening response in a previous time-grid scan. They are not confidence thresholds or false-alarm probabilities. In particular, an exact-center coefficient can exceed a time-grid screen without being a new independent detection. We preserve actual pass counts and all coarse-grid event coefficients.

The main output grid is 40 to 402 days inclusive at 0.1-day spacing. We repeat the calculation at 0.05 day. Fractions give each sampled period equal weight. They do not apply an orbital population prior. Counts are exact for these grids; they are not claims about all continuous periods. files/blind_runs.csv gives consecutive blind samples on the 0.1-day grid. Their endpoints are sampled periods, not solved boundaries.

## Results

| Half-window, days | Grid step, days | Period count | No usable repeat | Any actual pass | Any 300-ppm injection pass | Any 500-ppm injection pass | Any 1000-ppm injection pass |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 4 | 0.1 | 3621 | 356 | 0 | 3195 | 3265 | 3265 |
| 5 | 0.1 | 3621 | 347 | 0 | 2928 | 3274 | 3274 |
| 7 | 0.1 | 3621 | 336 | 0 | 2547 | 3285 | 3285 |
| 4 | 0.05 | 7241 | 713 | 0 | 6390 | 6528 | 6528 |
| 5 | 0.05 | 7241 | 694 | 0 | 5843 | 6547 | 6547 |
| 7 | 0.05 | 7241 | 674 | 0 | 5091 | 6567 | 6567 |

For the five-day rule on the finer grid, 9.584 percent of periods have no usable repeat. The range of usable passage counts is 0 to 20. The coarse-grid blind fraction is 9.583 percent. Grid refinement tests the aggregate count, not exact interval edges. A period with a recovered injection has at least one tested local window that can recover that specific added profile in the fixed recorded flux. This does not imply a statistically excluded orbit when no real event passes.

![Exact-repeat coverage and individual-injection recovery](files/period_window.png)

The 500-ppm and 1000-ppm curves coincide. The upper plot gives the number of usable passages at each coarse-grid period. The lower plot gives the fraction with at least one individual-injection pass in 20-day bins for the five-day window. This is a summary of a deterministic record. It has no binomial error bars because the periods and their windows are dependent. The last two days of the scope are retained in the complete table, though the lower plot stops at the final full 20-day bin.

As a concrete comparison, the 350-day grid period predicts three other passages in the selected time span, but none is usable under the five-day rule. Its passages near BKJD 398.86 and 748.86 have no selected rows in the local window. The passage near 1098.86 has only 42 rows and no sampled exit wing. The 372-day period has three usable passages. files/coverage_examples.csv gives the times and coverage counts from a separate check script. The longest consecutive blind run on the coarse grid is 334.1 to 357.9 days (239 samples). These are statements about sampled periods under the stated cuts. We do not infer exact continuous interval boundaries. This contrast shows why a random-time recovery fraction cannot replace an orbit-conditioned window map.

## Checks and physical limits

A direct four-column design-matrix solution agrees with the projected coefficient in 136 accepted test windows. The largest absolute difference is 9.95e-14 ppm. Direct 500-ppm injections agree with the linear response to 5.68e-13 ppm. Files validation.json and raw_validation.json give the full check results. The 0.05-day calculation repeats all local fits and coverage rules; it does not interpolate a coarser scan.

The result is a map of where this record can test one repeat model. It does not establish a new planet, a comet, an orbital period, eccentricity, or a physical cause. A fixed object may change its dust output or transit profile. Timing can depart from epoch + n P. Epoch and profile uncertainty are held fixed. Real signals may be changed or removed by the pipeline before these post-processing injections. Quality cuts, finite cadence, stellar changes, detector artifacts and a blended source remain possible. The parent pixel and instrument work does not replace independent observations. We obtain no independent telescope confirmation.

The presence of blind grid periods prevents a blanket repeat exclusion in this tested range when the blind count is positive. Conversely, usable coverage alone cannot reject an orbit. Statistical exclusion would require a calibrated noise and signal model, a treatment of fit and epoch uncertainty, and a specified activity model. We make none of those exclusions here.

## Reproduction and job record

Job: sci-1107-syam2-astronomy-80f5dc7650e3. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. The signer is a campaign-machine key, not a personal authorship claim. The bundle is saved locally only. It contains no private key.

In a writable extracted copy, use Python 3.12 and the package versions in files/provenance.json (also files/prior_requirements.txt), then run `bash files/reproduce.sh`. This uses the preserved selected arrays and needs no network. It rebuilds both grids, coarse-grid event and blind-run tables, validation results and the figure. It can take several minutes. Derived files in that extracted copy are replaced.

For an optional independent raw-data check, run `python files/check_raw.py /absolute/path/to/lightcurves.tar`. Reuse the shared path above. If it is not available, `python files/prior_retrieve.py /new/local/path/lightcurves.tar` retrieves the exact source and checks the hash. It refuses an existing output path. The check script reconstructs and compares arrays in memory; it never changes the shared archive. The bundle preserves the arrays, retrieval code, raw and member hashes, fixed profile, fixed screens, all coarse-grid local fits and both-grid summaries. The baseline license covers our text, code, figures and derived data; NASA source provenance is retained.
