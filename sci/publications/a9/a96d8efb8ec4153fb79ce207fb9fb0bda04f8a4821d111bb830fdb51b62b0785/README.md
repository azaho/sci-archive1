# Same-row pixel subtraction removes most fitted light loss from two Kepler quarter 7 comet candidates

The known dips on KIC 5514200 and KIC 5514277 include a large additive pixel signal. In the main local fits, subtraction of faint pixels in the same detector rows removes 92.2 percent and 89.6 percent of the fitted aperture loss. A small loss remains. This result weakens a simple stellar-occultation interpretation of the full dips. It does not establish the exact detector cause or exclude a smaller real event.

## Question and prior work

Do two nearby comet candidates contain a common additive detector signal? Dumond et al. (2025), DOI 10.1051/0004-6361/202556033, list KIC 5514200 in their first group and KIC 5514277 in their second group. Their dates are BKJD 670.1 and 670.4. We selected the pair because of the close dates and sky positions. We did not discover these dips. This is a test of selected candidates, not a blind survey.

We ran SCI campaign searches before selection. The broad verified search is in `files/campaign_search.json`. We also inspected published bundle metadata to avoid repeat work. A focused search is in `files/focused_search.json`. Prior campaign work on KIC 4078638 found unequal pixel losses and a dip in another extraction. We read that verified publication, SCI 761fcb2599d76f9f45c00043388c58f4d65a479059ca74c962029b6456df01eb. Its text is in `files/prior_read.txt`. We reuse no code, data, or fitted values from it. Our new test uses a different pair and a row reference.

The Kepler instrument handbook describes rolling bands as row-dependent changes in detector bias. The archive manual defines quality bits 131072 and 262144 as rolling bands in the optimal aperture and full mask. These facts motivate an additive row model. They do not prove that a specific band caused these dips.

Exact-name web searches for each target with TESS returned no results. We found no independent observation that confirms either dip. This limited literature search is not a complete archive search. Later observations would not directly test a single event with no measured period. Raw flux, corrected flux, and pixels below share the same Kepler exposures.

## Data and provenance

We use 37 Kepler DR25 quarter 7 long-cadence light curves and the two candidate pixel files. The light curves are all available quarter 7 files under the public S3 prefix `kepler/public/lightcurves/0055/005514`. This gives 15 targets on channel 79 and 22 on channel 78. The set follows a catalog-ID prefix; it is not a random stellar sample. The listing keys are in `files/reference_keys.json`.

All 39 files were added with the campaign dataset helper. No existing shared data were changed. Exact absolute shared paths, source URLs, sizes, pipeline versions, and SHA-256 hashes are in `files/sources.json`. Each analysis run checks all input hashes. The total raw input size is 21,432,049 bytes. Raw files remain in the shared store. The two light curves have pipeline version 9.3.24 and data release 25. Times are BJD minus 2454833 days. Pixel flux has units electron/s and has the archive background estimate removed.

The two stars are 103.83 arcseconds apart. Both are on channel 79. Their saved pixel stamps have origins (column,row) = (701,980) and (697,1006). They do not overlap. The apertures contain six and three pixels. The second stamp contains bright light outside the target aperture; it is not an isolated target image.

Job: sci-1107-dell-astronomy-f3c5e5fa2eab. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. See `files/job.json`. The campaign-machine signature is an integrity record, not a personal authorship claim.

## Method

We fit a local polynomial minus a positive-loss profile. The profile rises as `1-exp(-(t-c+L)/tau)` between `c-L` and `c`, then falls as `exp(-(t-c)/tau)`. It is zero before `c-L`. We normalize its peak to one and average 11 samples across a 0.0204336-day exposure. We set L = 7.27 hours and tau = 12.13 hours from the first candidate's catalog parameters. Both stars use this same profile to make the comparison direct. This is a measurement profile, not a full physical dust model.

The main light-curve window is BKJD 670.3 plus or minus 2.5 days. A quadratic baseline and signed depth are solved by ordinary least squares. We fit c between 669.8 and 670.8 days by bounded scalar minimization. We also measure a fixed-center coefficient at 670.1 for each reference star. These signed coefficients include brightenings. We require 40 finite rows. We use equal weights, since photon errors do not describe all variation here.

The main quality mask retains only zero-quality rows or rows whose flags contain a corrected cosmic ray (128) or either rolling-band bit. All other flags are rejected. We also fit light curves with quality exactly zero. We do not fill gaps in these fits. For a descriptive cross-star lag curve, we remove each fitted polynomial and compare flux within 1.2 days of 670.3. We shift the second curve from -0.6 to 0.6 day in 0.01-day steps. We interpolate only between samples separated by less than 0.041 day. Sample counts change with lag. We assign no significance or confidence interval to the best lag.

The pixel test uses all collected pixels with finite values and the main quality mask. The center is fixed from each raw-flux fit. Each pixel has its own polynomial and loss coefficient. The main model adds linear POS_CORR1 and POS_CORR2 terms, centered and scaled locally. Twelve choices per star use half-windows of 2, 2.5, and 3 days, polynomial degrees 1 and 2, and motion terms absent or present. The center and profile stay fixed in these tests.

For each aperture row, we select the faintest collected pixel outside the aperture by its median flux more than 1.5 days from BKJD 670.3, within the three-day window. Selection uses off-event flux, not the fitted dip coefficient. We subtract that reference flux once for each aperture pixel in its row. The same fixed reference pixels serve all twelve fits. Their coordinates and weights are in `reference_pixels.csv`. This operation cancels a uniform additive signal along each sampled row. It can also remove real stellar wings or changes in a blend. It does not reconstruct the detector electronics.

For main pixel errors, we use 999 wild residual draws with random signs shared across all pixels in blocks of 12 nominal cadences. Gaps can split the elapsed intervals. We keep the design, profile, center, and reference selection fixed. These are conditional noise ranges. They omit selection and detector-model error. A noise-free baseline-image injection check measures the algebraic loss from subtracting stellar wings. That image includes blended light and is not a calibrated stellar point response function.

## Results

| Main measurement | KIC 5514200 | KIC 5514277 |
| --- | ---: | ---: |
| Raw-flux center, BKJD | 670.13479 | 670.35241 |
| Raw-flux depth, ppm | 2078 | 3017 |
| Corrected-flux depth, ppm | 1993 | 3553 |
| Pixel aperture loss before row subtraction, electron/s | 43.773 | 23.402 |
| Loss after row subtraction, electron/s | 3.397 | 2.427 |
| Fraction removed | 92.24% | 89.63% |
| Remaining loss / original aperture baseline, ppm | 159.7 | 300.9 |
| Conditional 95% range for remaining loss, electron/s | 0.306 to 6.381 | 0.258 to 4.453 |
| Baseline-image injection fraction retained | 98.53% | 97.09% |

The pixel fits and archived light-curve fits have different baselines and motion terms. Their depths need not be identical. The remaining ppm values use the original aperture baseline, not the smaller baseline of the subtracted curve.

![Measured aperture curves, pixel coefficients, and descriptive lag curves](files/outputs/evidence.png)

The main outer-pixel mean losses are 6.59 and 6.69 electron/s per pixel. The aperture means are 7.30 and 7.80 electron/s per pixel. In the first stamp, pixels with baseline flux from about 12 to 8233 electron/s have losses of only about 5.6 to 8.1 electron/s. Thus, a single fractional decrease of the baseline image does not describe that stamp. The second stamp has larger spatial differences, including one row with negative coefficients. A simple uniform loss over the whole stamp is not an adequate model there. The same-row reference allows this spatial structure.

Across all twelve choices per star, row subtraction removes 89.8 to 101.0 percent of the first aperture loss and 87.8 to 95.5 percent of the second. Values above 100 percent mean that the remaining coefficient is a small brightening. The residual ranges are -19 to 198 ppm and 137 to 344 ppm. These are model-sensitivity ranges, not confidence intervals.

![Aperture flux before and after same-row subtraction](files/outputs/row_subtraction.png)

The best descriptive raw-flux lag is 0.24 day, with correlation 0.815 in 110 sample pairs. Corrected flux gives the same lag and correlation 0.813. Quality-zero lag curves peak near 0.19 to 0.20 day with only 35 sample pairs. The raw-flux fitted centers differ by 0.218 day. This time difference is too large to be an archive barycentric time correction between these nearby stars. A shared detector feature can move across rows; an ordinary simultaneous contaminating eclipse would not acquire this delay. Still, these lag values depend on shape, window, interpolation, and selection. They do not measure a physical band speed.

The event interval 669.8 to 671.3 contains 73 finite-time rows per star. Rolling-band bits are set on 33 and 40 rows. They are set on 33.8 and 56.3 percent of all recorded rows in the quarter. Flags are not unique to the dip. Removing flagged rows does not remove all light-curve structure and reduces coverage. Thus, the flags provide context, not a stand-alone rejection rule.

The 35 other stars provide a spatial check. The fixed-time signed responses have both signs on channel 79; they are not identical transits. The complete signed fit table is retained. This check does not establish a sky-wide event, a population rate, or a false-alarm probability. Channel 78 is also a different sky region, so it is not a controlled instrument experiment.

![Spatial reference responses and pixel sensitivity fits](files/outputs/controls.png)

## Interpretation and limits

An occultation of one unresolved star should scale that star's image to first order. A row-dependent additive bias instead changes faint and bright pixels by similar absolute amounts. The observed faint-pixel losses, strong removal by same-row subtraction, nearby delayed dip, and rolling-band flags support an additive instrument contribution to most of the measured losses. This interpretation is an inference from these tests. We did not measure raw detector bias or fit the full Kepler calibration model. A shared error in the sky estimate is another additive explanation.

A smaller real transit can remain. The main residual coefficients are positive and their conditional intervals barely exclude zero. We do not claim a null residual or an upper limit on a comet. We did not use a calibrated point response function, a source catalog deblend, or independent telescope data. Starlight in the reference pixels, nonlinear image motion, baseline choice, profile mismatch, and unknown spatial detector structure can affect subtraction. The injection check uses the measured blended baseline image; it cannot prove preservation of every possible source signal.

This investigation adds a reproducible artifact test for two published candidates. It reports no new planet or comet. It does not reject the wider exocomet catalog or infer an occurrence rate.

## Reproduce and inspect

Use Python 3.12 and the versions in `files/requirements.txt`. From the unpacked publication root:

```sh
python files/analyze.py --data-root /mnt/dell-data/shared_datasets --out reproduced
python files/validate.py
```

The first command checks exact input hashes and rebuilds all tables and three figures in `reproduced`. The second checks the supplied `files/outputs` tables. To check a new run, copy that script beside the new outputs directory or set its D path. These numerical checks verify subtraction and the stated baseline-image transfer; they do not validate an astrophysical model.

On another host, first run `python files/retrieve.py /absolute/private/raw`. It downloads the exact 39 public files and checks their sizes and hashes. Use that directory as `--data-root`. Do not point the retrieval script at a shared immutable dataset store. Analysis needs no network. No raw shared file is duplicated in the bundle. The retained CSV tables allow inspection of every reported coefficient, reference-pixel choice, residual draw, and plotted series without downloading the raw files.

The source code is `files/analyze.py`. `sources.json` gives the full data record. `environment.json` and `job.json` give software and worker records. The random seed is 5514200. Minor floating-point changes can occur on another system. The baseline SCI license applies to our text, figures, derived tables, and code. NASA and STScI retain source credit for the public Kepler data.
