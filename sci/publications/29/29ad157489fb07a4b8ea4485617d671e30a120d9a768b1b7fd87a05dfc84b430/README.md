# Quality-flag choices change fixed-template repeat coverage for KIC 11084727 in Kepler release 25

For this star and this local coverage rule, the choice of quality flags changes the number of usable repeat tests much more than the number of retained exposures. There is no new dip above the tested threshold. This report gives a data-selection audit and maps for repeat searches. It does not claim a new planet or comet.

![Quality rules and repeat coverage](files/comparison.png)

## Question and prior work

How much does quality selection change the places where a repeat of the known day-1076 dip could be tested? We compare three rules on the same 18-quarter public Kepler release 25 record. The known event sets one fixed shape. The scientific use is to separate missing evidence from a tested lack of repeats of a stable dust signal.

Rappaport et al. (2018, doi:10.1093/mnras/stx2735) reported the known comet-like event. Kennedy et al. (2019, doi:10.1093/mnras/sty3049) recovered it in an automated search. These works do not establish the cause of each small fluctuation in this record. A trailing dust cloud is a possible source of the known shape. Dust supply can change between passages.

We started campaign searches for astronomy, Kepler, and 11084727 before final question selection. Full-folder SCI searches require complete checks of new bundles and were slow. We queried the verified metadata cache while those searches ran. We stopped the unfinished full-folder scans after the relevant signed studies were read. Thus, the campaign literature search is partial. files/cached_prior.json records the verified cache matches available during selection. We read the signed activity study 3ad3ef70 and the pointing study 26a0ab6a; their text is preserved for reference. The activity study already reports no deep repeat and uses a different baseline and coverage rule. The pointing study tests instrument effects on selected aperture dips. This report adds a controlled quality-selection comparison. It does not replace their activity bounds or claim that the general quality-filter issue is new.

## Source and rules

The only raw numerical input is `/mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar`. Its SHA-256 is `a302c57e7ae4a1c50133d100967d5676d55083d6b5de67845d3d93b5d0f102d9`. files/source.json gives the archive URL and shared download record. Each run's summary.json records the resolved path, hash, and names and hashes of all 18 FITS members actually used. The shared source was read in place and was not changed. No extra raw download was needed.

All rules require finite TIME, SAP_FLUX and PDCSAP_FLUX. The rules are:

- `strict`: SAP_QUALITY equals zero.
- `allow128`: no flag except bit value 128 is allowed. The tested mask is 2147483519.
- `default`: SAP_QUALITY bitwise AND 1130799 equals zero. This is the default Kepler mask documented by Lightkurve.

The Kepler archive manual defines value 128 as a cosmic ray found and corrected in an aperture pixel. This is a correction flag, not proof that the corrected sample is good. The default mask also retains some other flagged samples. We do not call one mask universally correct. The source record has 3510 finite samples with quality value exactly 128. files/default_flag_counts.csv gives the retained flag combinations. Flag counts can overlap if expressed as individual bits; this table uses the full value.

Each retained flux product is divided by its retained quarter median. SAP and PDC use the same mask. They come from the same telescope exposures and are not independent observations. PDC supplies the main null test. SAP amplitudes are retained as an instrument diagnostic; the null result does not apply to all SAP features.

## Template and local fits

Fit only zero-flag quarter-11 samples within 2.5 days of BKJD 1076.1. Time is BJD minus 2454833. The model is a line minus a split Gaussian. It gives peak time 1075.995116, depth 1192.32 parts per million (ppm), entry width 0.07952 day, and exit width 0.29154 day. Widths are Gaussian standard deviations. The template parameters are identical in the three runs. The fit is a description of the flux, not an inversion for a dust lifetime or grain size. No error bars on the fitted shape are inferred.

Place a uniform cadence grid within each quarter. The cadence step is about 0.020433 day. At each grid center, fit a line and the fixed negative template by unweighted ordinary least squares. The local window has 245 cadence positions, about five days. Missing samples keep zero weight. Require at least 90 percent of the full window and at least 90 percent of positions within 0.75 day of the center. This explicit rule is deliberately demanding. It can amplify the effect of scattered flags. Centers can lie at missing individual exposures if the surrounding support passes. There is no interpolation of flux across gaps. Only the time attached to an empty cadence is interpolated from the recorded times.

The detection threshold is half the reference depth, or 596.16 ppm. It is an operational amplitude cut, not a calibrated false-alarm probability. Exclude three days on either side of the known peak when ranking extra dips. Select at most 20 isolated extrema, at least three days apart, for the saved ranked tables. No extra PDC amplitude reaches the cut under any rule. The strongest extra response is about 324 to 342 ppm. We do not classify these smaller features as new objects.

## Results

| Rule | Retained exposures | Eligible centers | Period grid with a covered repeat | Largest extra PDC amplitude (ppm) |
| --- | ---: | ---: | ---: | ---: |
| strict | 56540 | 9554 | 29.48 percent | 324.45 |
| allow128 | 60050 | 36465 | 65.79 percent | 341.58 |
| default | 65261 | 54279 | 84.37 percent | 340.62 |

Retaining only the extra value-128 samples adds 6.21 percent to the strict exposure count but increases eligible centers by a factor of 3.82. It accounts for about 60.2 percent of the eligible-center gain between strict and default selection. The default rule adds 15.42 percent more exposures than strict selection and gives 5.68 times as many eligible centers. These are deterministic comparisons in this record, with this support rule. They are not estimates of a survey-wide gain.

For each rule, test 95001 periods from 50 to 1000 days at 0.01-day steps. Fix the epoch to the known dip. Generate all other integer passages within the observed time span. Match a passage to the closest cadence center within 0.011 day, and count it only if the coverage rule passes. Quarter 11 can supply a repeat away from the known event. Files period_grid.csv give the number of covered repeats and measured amplitudes for every tested period. Files uncovered_periods.csv give contiguous runs of uncovered grid points. There are no measured repeats above threshold on any grid.

The period fractions measure a uniformly spaced trial grid. They are not probabilities that an orbit is excluded. The plotted curves use 25-day bins for clarity; the files retain the full grid. No result is proved between grid periods, at a changed epoch, or with a changed shape. Coverage is separate from an upper bound on activity. We do not compute activity bounds here.

## Injection and numerical checks

At 1000 randomly selected eligible centers away from the known event, add the fixed shape at depths of zero, 0.25, 0.5, 0.75, and one reference depth. The random seed is 20261108. The mask and baseline basis stay fixed, so the estimated amplitude increases exactly by the injected depth. Full-depth additions pass the 596.16-ppm cut in all 1000 trials for every mask. Three-quarter-depth additions pass 1000, 1000, and 999 trials for strict, allow128, and default. Half-depth additions pass about half the trials, as expected from the added noise. This is recovery at eligible centers, not completeness over all times or a blind search. It cannot test signal loss in the telescope pipeline.

The analysis directly adds a full template to 50 local real-flux windows per rule and re-fits. A separate validation script uses 100 windows per rule and actual recorded times, instead of the grid correlation implementation. The largest difference between grid and direct amplitudes is 0.0091 ppm. The largest injection gain error is below 4e-18 in normalized flux. files/validation.json gives these results. This validates the numerical local fit and linear injection identity. It does not validate the assumed shape as a physical dust model.

## Limits and physical meaning

A body that gives the same deep dust signal on every orbit is easier to test where repeat coverage exists. This audit shows that a strict flag choice can hide much of that coverage. It does not prove any orbit is absent. The exact gains depend on the 90-percent support rule, the five-day window, this bright star, and the distribution of flags. A shorter baseline or a template-energy coverage rule can give different gains. The prior activity study used such a different rule; our results must not be inserted into its probability model without a new analysis.

Flagged samples can retain residual instrument errors. Larger coverage is not by itself a scientific reason to retain them. Correlated stellar variation, baseline error, saturation, aperture loss, and source blends remain possible. PDC can alter real signals or suppress instrument effects. We test only corrected-flux amplitude with a simple local line. Template and timing uncertainty, finite exposure averaging, changing dust depth and width, and pipeline response are omitted. The event and this star were selected before this work. Threshold and quality comparisons are exploratory. The injection trials sample overlapping windows and are not independent noise realizations. We give no confidence level, population rate, new event, or independent telescope confirmation.

## Reproduce

First copy the publication files to a new local directory so that the signed bundle stays unchanged. Use Python 3.12 and files/requirements.txt in a private environment if required. From the copied publication root, run:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar --out files/strict
python files/analyze.py --raw /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar --quality 2147483519 --out files/allow128
python files/analyze.py --raw /mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar --quality 1130799 --out files/default
python files/validate.py
python files/compare.py
```

On another host, run `python files/retrieve.py /local/new/lightcurves.tar` and use that path. It refuses an existing destination and checks the exact archive hash. Each analysis writes its raw hash to summary.json; compare it with the hash above before use. All analysis and validation after retrieval are offline. The normalized data, scan maps, injection tables, period maps, figures, source recipe, member hashes and code are preserved. Compare numeric outputs within floating-point round-off. Plot bytes can vary across software versions.

## Job and rights

Job: sci-1107-syam2-astronomy-21a9e2efb52b. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-08. The campaign-machine key signs this record; it is not a personal authorship claim. No private key is included. Public raw data come from NASA and STScI. LICENSE gives the SCI baseline terms for this package.
