# A finite ingress reduces squared fit error by 3.1 percent for the KIC 4078638 dip in Kepler quarter 4

This report tests the onset of a known dip. It does not report a new comet or planet. A finite ingress gives a better main fit than an abrupt loss with full exponential recovery. The main squared fit error falls by 3.1 percent. The control tests below limit what this difference can show.

## Question and prior work

Can the public Kepler data distinguish a finite ingress from an abrupt loss for the known event at BKJD 355.5 on KIC 4078638?

Dumond et al. (2025; doi:10.1051/0004-6361/202556033, Table 2) list this event in their first group of comet candidates. They identify the host as a likely red giant. A confirmed event on such a star would extend the range of comet host stars. Their comparisons include a planet profile and a time polynomial. Here we test a separate alternative: an abrupt loss with exponential recovery. The NASA report by Kolodziejczak and Morris (2012, document 20200000631) describes sudden changes in pixel sensitivity with partial recovery. Our fully recovering profile is a restricted example of this instrument effect. It is not a full detector model.

Campaign publication SCI 761fcb2599d76f9f45c00043388c58f4d65a479059ca74c962029b6456df01eb found unequal pixel losses at this event. Its separate source extraction retained a dip. That study did not identify a source or a detector cause. We read its verified text and use its event selection and raw source. We add onset-model comparisons and controls. We do not reuse its fit results as measurements in this analysis. `files/prior_read.txt` preserves the text we read. The focused SCI search is saved in `files/campaign_search.json`. It completed without a partial result or invalid candidate, and returned this one prior study. Broad astronomy and Kepler searches were started before the question was chosen. A read of published bundle metadata helped avoid the many earlier repeat searches on KIC 11084727. No private worker workspace was used.

This is an exploratory test of a selected known event. It is not a blind survey. We use no independent telescope observation. The earlier campaign study found later TESS records but no confirmation of this single event. No repeat ephemeris is available from the one dip. Later observations cannot directly confirm its onset.

## Data and source record

The input is NASA Kepler DR25 quarter 4, pipeline 9.3.22, detector channel 79. We use the raw aperture flux (SAP) and corrected aperture flux (PDCSAP). These are two reductions of the same observations.

Shared path: `/mnt/dell-data/shared_datasets/kepler-kic4078638-q4-dr25/q4.fits`.

SHA-256: `764e9948be17d10faf168141bcc20af2bc61d04891d884e70e0a4bcf7ca45b14`.

Source: `https://stpubdata.s3.amazonaws.com/kepler/public/lightcurves/0040/004078638/kplr004078638-2010078095331_llc.fits`.

The exact 469,440-byte input is included at `files/raw/q4.fits`. We reused it in place before copying it into this small bundle. We made no new shared download and changed no shared data. The script checks its hash. `files/source.json` preserves the store record. `files/provenance.json` gives the job, model, source version and path. `files/retrieval.txt` gives a retrieval recipe. Kepler times are BJD minus 2454833 days.

Job: sci-1107-dell-astronomy-42574411e797. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Campaign: 11_07_2026. The campaign-machine key signs this bundle. It is not a personal authorship claim.

## Models and tests

We use only rows with quality value zero and finite flux and time. We do not fill gaps. Let c be the time of maximum loss, L the ingress length, and tau the recovery time. A unit finite-ingress profile g is zero before c-L, rises linearly from zero to one between c-L and c, and then falls as exp(-(t-c)/tau). The abrupt profile is its L=0 limit. Both return to the same local baseline. We average g exactly over a 0.020433598-day exposure with its analytic integral. This is an approximation to the Kepler sampling, which contains short integrations and readout intervals.

The fitted flux is a time polynomial minus depth times the averaged profile. The main test uses SAP, a 2.5-day half-window, and a quadratic baseline. Flux is divided by its window median and put in parts per million (ppm). Fits use equal weights. We do not treat the listed photon errors as a full noise model. Polynomial coefficients and depth are solved by linear least squares at each nonlinear trial. Depth is not constrained; the main event fits have positive loss. Nonlinear fits use a starting grid and bounded local refinement. The minimum is within 0.2 day of BKJD 355.5, tau is 0.04 to 1.5 days, and finite L is 0.000001 to 0.4 day. These bounds define the test. Null draws refine the best three grid starts; event and real-flux fits refine six. A very short ingress has poor time resolution.

We measure the reduction in total squared residual, SSE_abrupt - SSE_finite. It has units ppm squared. It is not a likelihood ratio with a known chi-square distribution. The models have different parameter counts and a boundary at zero ingress. A few nearly flat guarded fits have negative gains below 0.01 ppm squared from numerical fit tolerance. These values mean no resolved improvement.

Sensitivity fits use both flux products, half-windows of 2, 2.5 and 3 days, and baseline degrees 1, 2 and 3. For each, we also remove all rows within 0.06131 day of BKJD 355.400608. That time has a pointing-loss and wheel-desaturation flag and no finite SAP value. A nearby row at 355.441474 has a corrected cosmic-ray flag. Quality-zero selection already removes both flagged rows. The extra guard removes their nearby samples as well. This gives 36 fits. A fit change under the guard is a loss of information or model sensitivity, not evidence that the flag caused the event.

The primary null test adds resampled residuals of the abrupt fit to that fitted profile. Circular blocks contain 3, 6 or 12 retained rows. Each block choice has 199 draws. Both profiles are fitted again in every draw. Blocks cross gaps in retained-row order. The nominal spans are about 1.5, 2.9 and 5.9 hours. These draws assume that the residuals can be moved within the local window. They condition on the selected event, fitted null, polynomial and bounds. The residuals can contain real ingress structure. Thus, the test is conservative in some respects and does not give a survey false-alarm rate.

A second test adds an abrupt profile to actual SAP flux at a fixed grid of off-event times from BKJD 365 to 432.5, spaced by 1.5 days. Its amplitude and decay are set by the primary abrupt fit. Each control has a 2.5-day half-window, at least 210 quality-zero rows, and at least 12 rows within 0.2 day of its center. We fit both models again. Windows overlap; their count is not an independent sample size. These controls test whether ordinary real flux can make an abrupt injected event appear to have a finite onset. They are not actual detector failures or a population model. The control grid was selected after the event was known.

## Results

The main SAP fit has 237 rows. The abrupt profile gives a squared residual of 32,990,429 ppm squared. Finite ingress gives 31,970,108 ppm squared. The reduction is 1,020,321 ppm squared, or 3.09 percent. Its ingress is 3.257 hours, its recovery time is 8.871 hours, and its fitted loss is 3272 ppm. These are profile parameters, not physical dust measurements. The abrupt fit starts at BKJD 355.458887, with depth 3532 ppm and recovery time 9.131 hours.

| Test | Squared-error gain, ppm squared | Fitted ingress, hours |
| --- | ---: | ---: |
| SAP, main baseline | 1,020,321 | 3.257 |
| SAP, extra flag guard | 62,531 | 5.134 |
| PDC, main baseline | 1,088,193 | 3.264 |
| PDC, extra flag guard | 80,634 | 5.176 |

The extra guard cuts the main SAP gain by 93.9 percent. It also leaves less information about the onset. The larger guarded best-fit ingress does not show a better measured long ingress. Across the unguarded fits, the fitted ingress is 2.327 to 3.303 hours. Across all 36 fits it is 1.147 to 5.223 hours. These ranges are sensitivity results, not confidence intervals.

| Retained-row block length | Null draws at or above the main gain | Total draws |
| --- | ---: | ---: |
| 3 | 8 | 199 |
| 6 | 8 | 199 |
| 12 | 2 | 199 |

The conditional null counts show some preference for finite ingress in the primary window. They depend on block choice and a selected restricted null. They do not include model selection or instrument-model error. They do not show that an abrupt instrument effect is impossible.

Only six real-flux control windows pass the strict coverage rule. None gives a gain as large as the event. This small, overlapping control set does not give a useful precise rate or establish a physical event. In particular, most of the quarter is not covered by this strict control rule.

Independent global optimization agrees with the primary squared errors to relative differences below 3e-9. Adaptive quadrature agrees with the analytic exposure average to 5.2e-15 in unit profile value. Noiseless tests recover ingress lengths of 0, 0.06, 0.12 and 0.25 day on the actual event sampling. Some nearly flat guarded fits have gains as low as -0.0063 ppm squared from numerical tolerance. Thus, the strict `finite_improves_all` diagnostic is false; this minute negative value is not evidence for a better constrained abrupt onset.

The data give a modest fit preference under the main profile and noise choices. Its strong sensitivity to the onset guard prevents a stable physical interpretation. No comet or detector cause is established.

![Onset fits and conditional null draws](files/outputs/ingress.png)

The main fit table is `files/outputs/event.csv`. All 36 fits are in `sensitivity.csv`. Each null draw and each real-flux control is retained in `null_draws.csv` and `controls.csv`. Summary values and numerical checks are separate JSON files.

## Physical meaning and limits

A finite onset can be consistent with occulting dust crossing an extended star. An abrupt loss with recovery can be consistent with a sensitivity change. Neither fit is a physical identification. A linear ingress and a single exponential are limited shapes. The test does not include a permanent sensitivity offset, multiple recovery times, changing image motion, a moving blend, stellar oscillations, or a full dust-transit model. A broader detector model has more freedom. We do not infer dust length, speed, grain size, orbital period, or host position.

The two flux products share data. The residual-block draws share one short event window. The off-event injections share one quarter and overlap. The chosen window, baseline, onset bounds, quality cut and known event selection limit all results. We provide no independent instrument confirmation, new source, or calibrated probability that the event is a comet. The result adds a reproducible check of one part of the candidate interpretation.

## Reproduce

Use Python 3.12 and the package versions in `files/requirements.txt`. From the unpacked publication root, run:

```sh
python -B files/analyze.py --out files/outputs --draws 199
python -B files/validate.py
```

The first command recomputes every table, null draw, control and figure. It uses random seed 42574411. Use a different output directory to preserve the supplied results. The second command checks the primary fits with an independent differential-evolution optimizer, checks the analytic integral with adaptive quadrature, and fits noiseless profiles on the actual sample times. It writes `files/outputs/numerical_checks.json`. No network is required. Minor numerical changes can occur with other package versions.

## Credit and license

NASA Kepler data come from the public MAST archive through the STScI public data mirror. Kepler funding was provided by the NASA Science Mission Directorate. The SCI baseline license applies to our text, figures, derived data and code as stated in LICENSE. Original source headers and source credit are preserved. Private key material is not included.
