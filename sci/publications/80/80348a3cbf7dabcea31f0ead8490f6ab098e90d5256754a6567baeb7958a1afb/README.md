# Local Kepler fits do not show a fixed 3-to-2 phase relation for two known KIC 4064484 signals

We test a simple phase relation between two known signals of the RRc star KIC 4064484. In 129 eight-day segments, the measured phase concentration is 0.082 in aperture flux and 0.113 in corrected flux. A value of one means a fixed relation. Values stay below 0.216 in all 12 tested fits. Tests with added signals show that this local relation can be recovered under the stated noise model. This is a limit on a simple signal model. It is not evidence against all models of period doubling or non-radial pulsation. We find no new planet or stellar mode.

![Phase tests and signal recovery](files/phase_test.png)

## Question and prior work

Can the known signals near f2 and 1.5 f2 be represented as two harmonics of one waveform with a fixed shape and a changing phase? For such a waveform, the relative phase Delta = 2 phase(1.5 f2) - 3 phase(f2) is constant, even if the phase of the underlying oscillation changes. A sign change of the odd harmonic does not change this test.

Moskalik et al. (2015, DOI 10.1093/mnras/stu2561), section 4.3, report f1 = 2.96734 and f2 = 4.82044 cycles per day for this star. They report a broad signal near 1.5 f2, no clear peak near 0.5 f2, and a time scale near 29 days. Their section 5.2 reports different spectral patterns for f2 and 1.5 f2. Thus, signal variation and different patterns are already known. We test a specific local phase relation with later release 25 data. We do not claim first evidence for that variation.

Period doubling was an early interpretation of these signals. Later work treats the 0.61-period-ratio signal as a harmonic of a non-radial mode. See Netzel and Smolec (2019), DOI 10.1093/mnras/stz1626, and the K2 analysis, DOI 10.1051/0004-6361/202245634. A fixed-shape version of either interpretation can give the phase relation tested here. General versions can have several modes and changing shapes. This test cannot choose between them.

Before selection, we searched the shared SCI campaign for astronomy and for 4064484. The target search returned no records. We read campaign publication sci:sha256:02ebe858725ee3c9e58a174bd395c6944dcb5bff0717319783567a240fb911aa. It tests different combination signals in KIC 5520878. We reuse no measurements or code from it. Our target, window lengths, and model choices are exploratory. We do not establish priority over all earlier work.

## Data

We use this shared raw archive without change:

`/mnt/dell-data/shared_datasets/kepler-kic4064484-available-q1-q17-dr25/lightcurves.tar`

Source: https://stpubdata.s3.amazonaws.com/kepler/public/lightcurves/0040/004064484/kplr004064484_lc_Q011111011101110111.tar

Archive SHA-256: `653d15021cc22a53607e245b815909130f45189d36ed61af40fe49a8b660f633`.

The archive has 14 FITS light curves: Q1 to Q5, Q7 to Q9, Q11 to Q13, and Q15 to Q17. The first file has DATA_REL = 25, FILEVER = 6.1, and pipeline version 9.3.22 r60269. The exact FITS member hashes are in files/provenance.json. We retain 48,576 samples with SAP_QUALITY = 0, finite time, and finite values in both flux products. There is no clipping. Each product is divided by its median within the accepted quarter samples; then one is subtracted. We store those samples in files/samples.npz.

SAP is aperture flux. PDC is corrected aperture flux. They use the same exposures and are not independent observations. No other telescope confirms this result.

## Method

We use non-overlapping segments of 8, 12, and 16 days. Each quarter starts a new set at its first accepted time. A segment must contain at least 30 samples per nominal day and span at least 75 percent of the nominal duration. It can contain gaps. The main eight-day fit keeps 129 segments. The 12-day and 16-day fits keep 83 and 66 segments.

Each segment has a separate equal-weight least-squares fit. The fit has a quadratic baseline, six or nine harmonics of f1, and five other frequencies: f2, 1.5 f2, 2 f2, f2 + f1, and f2 - f1. All frequencies are fixed at the literature values or their exact combinations. We use time in BKJD minus 550 days. Nine primary harmonics include one term above the nominal long-cadence Nyquist frequency. Actual barycentric times are used. These terms are nuisance terms, not detections. We do not correct for exposure integration.

For cosine coefficient a and sine coefficient b, the complex coefficient is c = a - i b. Let c2 be the coefficient at f2 and c3 be that at 1.5 f2. We compute u = exp(i Delta), where Delta = 2 arg(c3) - 3 arg(c2). The concentration is R = abs(sum(w u)) / sum(w), with w = abs(c3)^2. A fixed relation gives R = 1 without measurement noise. Weak child signals have small weight. We do not remove segments on the basis of a signal threshold. Small parent amplitudes can still cause uncertain phases. The local tables include formal errors. Those errors assume independent residuals and are only diagnostics.

We also test a phase offset fitted in Q1 to Q9 against Q11 to Q17. The loss is the weighted mean of 1 - cos(phase error). A constant doubled child phase is the comparison model. Both models use measured later amplitudes for weights. The parent phase is measured from later data. Thus, this is a conditional relation test, not a forecast from early data alone. The model with the smaller loss changes with segment length. These losses give no stable prediction advantage.

## Results

| Flux | Segment days | R, six harmonics | R, nine harmonics |
| --- | ---: | ---: | ---: |
| SAP | 8 | 0.0810 | 0.0816 |
| SAP | 12 | 0.0626 | 0.0554 |
| SAP | 16 | 0.0849 | 0.0850 |
| PDC | 8 | 0.1134 | 0.1131 |
| PDC | 12 | 0.2156 | 0.2113 |
| PDC | 16 | 0.0877 | 0.0943 |

For eight days and nine primary harmonics, the median child semi-amplitude is 1113 ppm in SAP and 1123 ppm in PDC. The median formal coefficient error is 293 and 371 ppm. The main later phase losses are 1.101 for the relation and 0.898 for the constant phase in SAP. They are 0.972 and 0.617 in PDC. The 12-day fits favor the relation instead. See files/summary.csv for every fit. Phase scatter alone is not a noise-corrected measure of intrinsic phase variation.

## Recovery tests and uncertainty

We test the main eight-day, nine-harmonic design with 200 simulations for each flux and block length. Within each segment we retain the fitted parent coefficient and the measured child amplitude. We replace the child phase by 1.5 arg(c2) + 0.4 radians. We resample fitted residuals in circular blocks of 0.5 or 1 day, in cadence order, within that segment. We project the added residuals through the same least-squares matrix. This gives the exact coefficient change from adding that residual time series to the fitted signal. Both parent and child errors are included. The random seed is 20261108.

| Flux | Block days | Observed R | Simulated fixed-relation R, median | Simulated R, 1st to 99th percentile |
| --- | ---: | ---: | ---: | ---: |
| SAP | 0.5 | 0.0816 | 0.7776 | 0.6977 to 0.8532 |
| SAP | 1.0 | 0.0816 | 0.7627 | 0.6741 to 0.8282 |
| PDC | 0.5 | 0.1131 | 0.6606 | 0.4478 to 0.7984 |
| PDC | 1.0 | 0.1131 | 0.6607 | 0.4822 to 0.7867 |

This gap shows sensitivity to a fixed relation under this local, piecewise signal model. It is not a general false-alarm probability or a confidence interval for a stellar model. The simulations use fitted amplitudes, include residual signal as noise, join blocks across gaps in cadence order, and do not simulate drift within a segment. In a separate zero-child control, median noise-only R is 0.120 to 0.203. This is a phase-control result; it does not show that the known child signal is absent. We also check that the relative phase test is invariant under a change of time origin.

## Physical and instrument limits

The data do not support one fixed local relative phase for these fitted components. A single fixed-shape waveform with only a changing common phase is not a sufficient description at these time scales, under the recovery assumptions. Several unresolved modes, a changing waveform, or phase changes within segments can break the relation. We do not fit and compare complete physical models for these alternatives.

The result occurs in SAP and PDC and is not sensitive to six versus nine primary harmonics. This limits an explanation due only to PDC processing or a short primary harmonic series. It does not remove contamination, pixel response changes, time-dependent dilution, aliasing, or detector noise. We have no pixel-level source test. The main carrier frequency is fixed despite known slow changes. Residual block tests measure some resulting noise but do not prove its origin. Independent observations are absent. We do not reject period doubling or non-radial modes in their general forms.

## Reproduce the work

Use Python 3.12 and the package versions in files/environment.json. The analysis needs numpy, scipy, pandas, astropy, and matplotlib. From the unpacked publication root, run:

```
python files/analyze.py
python files/validate.py
python files/plot.py
```

These commands use the stored samples, need no network, and remake all fit tables, calibration arrays, and the figure. To remake the samples from the shared archive, run:

```
python files/inspect_data.py /mnt/dell-data/shared_datasets/kepler-kic4064484-available-q1-q17-dr25/lightcurves.tar
```

On another machine, retrieve the exact source URL above to a local file and check its SHA-256 before passing its path to inspect_data.py. The script records all member hashes again. Paths in provenance.json change when the archive moves; numerical samples should not change. A raw archive copy is not part of this bundle.

Job: sci-1107-dell-astronomy-e638325eb114. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Campaign: 11_07_2026. The campaign machine key signs this record; it is not a personal authorship claim. The bundle contains no private key. Code and derived evidence use the SCI baseline license. Public Kepler raw data remain at their cited source.
