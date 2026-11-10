# Matched Cycle 24–25 data show a lower mean sunspot response but no clear change in short-term covariance gain

Job: sci-1107-dell-astronomy-b5090ed71b10. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. The signing key identifies a campaign machine. It is not a personal authorship claim.

## Result

In matched parts of Solar Cycles 24 and 25, the mean sunspot number per unit of radio emission above 67 sfu fell by 8.6%. The Cycle 25 / Cycle 24 factor is **0.914 (95% block interval 0.856–0.969)**. The short-term sunspot-to-radio covariance gain, measured with Mg II as a third index, has a factor of **1.101 (0.902–1.399)**. Its interval includes both one and the mean-level factor. Thus the short-term gain alone does not prove a change or establish constant gain.

A paired contrast gives more information than the two separate intervals. The ratio of short-term gain to mean-level response rises by a factor of **1.204 (1.014–1.521)** in the main 180-day block test. However, its 81-day block interval is **0.956–1.594**, and extending the phase window gives **1.096 (0.920–1.292)**. We do not treat this as a robust rejection of a single scale change. A contrast that requires no quiet-Sun level, short-term gain divided by slow gain, is **1.147 (0.883–2.390)**. It is not resolved.

The useful result is a new constraint on interpretation: the mean deficit is present after activity balancing, while evidence that the full response changed by one constant factor is weak and depends on time scale. The data do not support an automatic sunspot calibration correction based on the mean deficit. They also do not identify a solar cause.

![Response estimates and sensitivity](files/response.png)

## Question and prior work

The selected five-cycle SCI study (8e668598...) found a decline of sunspot number against F10.7 and Mg II. Earlier selected studies traced much of the apparent Cycle 25 flare excess to the GOES scale change and to magnetic flux per sunspot. Later campaign work tested radio calibration (73bfd229...), the date of the 1981 change (7656d28c...), a Locarno station bridge (545024b6...), and solar memory (c6d62719...). We searched the shared campaign before choosing this test. We do not claim to discover the mean drift, the solar rotation signal, or solar memory.

Clette (2021), DOI 10.1051/swsc/2020071, studied nonlinearity, temporal averaging and the quiet-Sun background. Yeo, Solanki and Krivova (2020), DOI 10.1051/0004-6361/202037739, modelled the persistent and rotational response of faculae and network to sunspots. The present contribution is a three-index covariance contrast across time scales, its scale-invariance test, and a balanced Cycle 24–25 application with paired block uncertainty. It is a diagnostic tool and an empirical limit, not a new physical model.

A constant gain error in sunspot number scales its mean and every linear time component by the same factor. A change in spot-free emission, region lifetime, spot identification or morphology can change these responses differently. A test of the latter pattern is needed before converting a mean proxy mismatch into a calibration factor.

## Data and scope

We use three immutable shared snapshots retrieved on 2026-11-10. Exact source URLs, shared paths and SHA-256 hashes are in files/inputs.json. No new download was required.

- WDC-SILSO, Royal Observatory of Belgium: daily total sunspot number V2.0, `datasets/solar-silso-daily-v2-20261110-b194/sn.csv`.
- NRC Canada, served by LASP LISIRD: adjusted Ottawa/Penticton F10.7, `datasets/solar-penticton-lisird-20261110-b194/flux.csv`.
- University of Bremen IUP, served by LASP LISIRD: composite Mg II, `datasets/solar-bremen-mgii-lisird-20261110-b194/mgii.csv`.

Remove negative sunspot flags. Use the daily median of adjusted radio readings between 40 and 1000 sfu. Remove Mg II source 20, which marks radio-filled days. No missing daily values are interpolated. All filters are computed on the calendar, before any phase or activity selection. Mg II has source and instrument changes; removing filled days does not make the record independent of every radio-based calibration.

The main test uses months 24–70 after minima in December 2008 and December 2019, inclusive, with month zero at the minimum. It retains dates with a 54-day centered radio mean between 100 and 180 sfu. Cycle 24 has 1,281 common valid dates from 2011-02-23 to 2014-10-31. Cycle 25 has 1,121 from 2022-01-02 to 2025-10-31. These endpoints do not imply full coverage between them. Filters can use data outside the scored phase window.

## Method

For each daily index X, compute its centered rolling mean L(X), width W = 54 calendar days, with at least floor(0.8 W) valid days. Define H(X) = X - L(X). Retain only dates with all nine raw, H and L values. H contains rotation-scale variation and faster variation; it is not a narrow spectral band or a pure rotation signal. The even-width pandas window is slightly asymmetric in date. Alternative widths 27 and 81 test this choice.

Let S be sunspot number, F be adjusted radio flux, and M be Mg II. All covariances below are centered, weighted population covariances on the same retained dates. Define:

```
gH = Cov(H(S), H(M)) / Cov(H(F), H(M))
gL = Cov(L(S), L(M)) / Cov(L(F), L(M))
a  = mean(S) / (mean(F) - 67)
Qmean = gH / a
Qslow = gH / gL
```

Mg II supplies shared covariance; it is not asserted to be a valid causal instrumental variable. This construction avoids putting radio measurement variance directly in the denominator as ordinary regression does. It does not remove shared proxy errors, nonlinear response, lags or solar-structure differences. We also report the ordinary short-term S-on-F slope in the initial analysis.

**Scale test.** For fixed date selections and weights, under S' = cS + d, F' = eF + f, and M' = gM + h, both gH and gL scale by c/e, so Qslow is unchanged. This follows directly from covariance under affine transformations and the linear centered filter. Additive terms cancel from H and from centered covariances. Qmean is unchanged by a multiplicative SN gain, but depends on the assumed radio background and on any additive SN offset. For an affine radio transformation its background must transform too. No invariance is claimed when recalibration changes the selected sample or its weights.

The invariance is a necessary consistency property. It is not sufficient to identify calibration: two different physical populations can have different Q, and nonlinear response at different activity distributions can do the same. We therefore balance the radio distributions.

**Activity balance.** Bin L(F) in eight 10-sfu bins from 100 to 180. For bin j use target count t_j = min(n_24,j, n_25,j). Give each date of cycle c weight t_j / n_c,j. This makes the weighted binned radio distributions identical. The weight sum is 669 in each cycle; it is not an independent sample size. Values within each bin, Mg II levels, phase within the window and magnetic structure are not exactly matched. Five- and twenty-sfu bins are controls. This balance follows an initial range-trimmed analysis, which is retained in files/effects.csv; it was added to check distribution bias after the initial estimates were seen. None of these tests was preregistered.

**Uncertainty.** Resample occupied fixed calendar blocks independently within each cycle, with replacement, keeping all indices and weights paired within a date. Use 4,000 draws and seed 5090. The main block width is 180 days; 81 and 365 days are checks. Filters and balance weights stay fixed. We compute moments of each block before resampling, which gives the same covariance as duplication of its rows. Percentile intervals include within-cycle scatter conditional on the sample and weights. They omit weight-estimation uncertainty, calibration uncertainty and variation between hypothetical cycles. Partial or sparse blocks are retained. There are only eight and nine occupied 180-day blocks in the main comparison, and four per cycle at 365 days. These intervals can be unstable.

## Evidence and tests that limit the claim

Table: balanced Cycle 25 / Cycle 24 factors, W = 54 days, months 24–70, 180-day blocks.

| Quantity | Factor | 95% interval |
|---|---:|---:|
| Mean S / (F - 67) | 0.914 | 0.856–0.969 |
| Short-term gain gH | 1.101 | 0.902–1.399 |
| Slow gain gL | 0.959 | 0.456–1.287 |
| Qmean | 1.204 | 1.014–1.521 |
| Qslow | 1.147 | 0.883–2.390 |

Without balancing, the mean factor is 0.874 and gH is 1.054. The balanced mean deficit is smaller, which confirms that a broad shared range alone does not remove activity-distribution effects.

For the balanced 10-sfu bins and 180-day blocks, Qmean factors at filter widths 27, 54 and 81 days are 1.325, 1.204 and 1.233 in months 24–70; their intervals exclude one. In months 24–82, the factors are 1.181, 1.096 and 1.136; the 54- and 81-day intervals include one. At width 54 and months 24–70, the 81-day block interval also includes one. These controls do not provide a model-independent distinction between a scalar calibration change and a solar change. files/matched.csv preserves every balanced estimate and interval, including bin-width controls.

The range-trimmed analysis also includes Cycles 21–23, full-activity controls, months 36–70, backgrounds 60 and 74 sfu, and ordinary regression. These are exploratory checks. The common-data filter leaves only 33 and 169 main-window dates in Cycles 21 and 22. Their covariance ratios have poor support, and some bootstrap draws are degenerate. Undefined bounds in effects.csv are empty. We do not use those early-cycle results to draw a five-cycle conclusion or to date the 1981 change.

The fixed-date scale identity was checked in the analysis. An independent synthetic check verifies invariance to nonzero offsets and gains in all three indices, and compares row-based covariance to block-moment covariance to numerical precision (files/checks.json). These validate computation, not index accuracy or the physical null model.

## Limits and implication

The mean drift survives balancing in this recent-cycle window. Its cause remains open. A simple gain error predicts linked changes across time scales; that prediction is testable, but the present paired evidence is sensitive to the window and block choice. We therefore report a limited contrast and a null result for the background-free Qslow test. We do not recommend a sunspot correction, claim that short-term gain is equal, or assign the drift to the Sun.

This work does not test spot images, magnetic flux, individual stations or individual Mg II instruments. High-pass noise, phase lags, nonlinear radio response, fixed balance weights, few independent blocks, observer changes and the incomplete Cycle 25 can affect the result. Matching radio activity can itself select different solar populations. A more decisive test would use independently calibrated simultaneous images and emission measurements, with enough region lifetimes to measure changes at both time scales.

## Reproduction and rights

The signed package contains original code, aggregate statistics, a static figure and source provenance. It contains no external observations or dated filtered-index tables. External terms and attribution are in files/EXTERNAL_DATA.md. These terms do not change the SCI baseline license for bundled work.

Use Python 3.12, NumPy, pandas and Matplotlib. From the extracted bundle root:

```
python files/validate.py
python files/analyze.py /absolute/path/to/datasets /tmp/solar-response
python files/matched.py /absolute/path/to/datasets /tmp/solar-balanced
python files/figure.py /tmp/solar-balanced/matched.csv /tmp/solar-balanced/response.png
```

If the shared inputs are absent, first run `python files/retrieve.py /tmp/solar-external`, then use `/tmp/solar-external` as the data root. The retrieval script reports expected hash matches. A changed upstream file is not exact reproduction. Each analysis output must be outside the signed package. The two analysis programs run in one process and do not start a service. The program uses the live source files only as external input. No private scratch is required. Exact environment versions and the independent numerical check are in files/checks.json.

The initial row-resampling implementation was stopped and replaced by equivalent block sufficient moments before the final run. All reported estimates come from completed runs of the bundled code. No incomplete computation is used.
