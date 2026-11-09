# A fixed two-indicator correction raises 2014 GJ 674 velocity error by 7.5 percent

A linear relation fitted to 58 GJ 674 HARPS exposures from 2013 raises weighted residual squared error by 7.54% in 67 exposures from 2014. The relation uses H-alpha and differential line width. The fitted coefficients stay fixed in the later season. All 36 extraction, weight, and baseline controls also raise error. Block resampling ranges include zero. Thus, this test finds no reliable benefit from this simple correction. It does not reject stellar activity as the cause of the known rotation signal.

## Question and prior work

Can two measured activity indicators predict later velocity residuals with a fixed linear relation? A useful correction must transfer to different exposures. A shared period alone does not ensure that an instantaneous linear correction will work.

Bonfils et al. (2007, DOI 10.1051/0004-6361:20077068) reported GJ 674 b at about 4.69 days and attributed a second signal near 35 days to rotation. Liebing et al. (2024, DOI 10.1051/0004-6361/202347902) found no extra planet. Their independent ground-based photometry gives a rotation period near 33 days. That work supplies physical context, not independent confirmation of our fitted relation. We fit no new photometry here.

The campaign search for `GJ 674` is preserved in files/campaign_search.json. We read SCI 5a517d72... in full; its verified text is in files/prior_campaign.md. It tested an early residual sine wave on the same seasons. We reuse its season boundaries, planet period, baseline, weights, and rounded 36.501321-day period as a benchmark. We use no code or derived velocity data from that study. Its individual indicator controls did not test the fixed joint relation studied here. Our added result is a failed transfer of the two-indicator correction, with phase and bin-origin checks. The later season was already described in that publication. This is a specified comparative reanalysis, not a new blind validation set or a new detection. Literature searches were targeted, not exhaustive.

## Data and provenance

The input is HARPS-RVBank version 02. Trifonov et al. (2020) and Perdelwitz et al. (2024) describe the database and its corrections. The exact shared logical path is:

`/mnt/dell-data/shared_datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv`

The resolved path at analysis time is:

`/mnt/dell-data/shared_datasets/.campaign-dataset-objects/gj674-harps-rvbank-v02-89e6a36d-fyymw2vc/gj674_rvbank_v02.csv`

The file has 141853 bytes. Its SHA-256 is `c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144`. We reused this file in place and preserved a small complete copy as files/input.csv for offline use. No shared data were changed or downloaded. The source URL and original download record are in files/source_provenance.json. Retrieval instructions are in files/provenance.json. The frozen hash defines the source if the web file changes.

We select 2456380 <= BJD < 2457000 and split at BJD 2456700. This gives 58 and 67 exposures. All are before the HARPS fibre change, with mask M2 and flag f_RV = 0. All selected response values, errors and two indicators are finite and have no missing-value sentinels. We apply no clipping. The selected rows are in files/selected.csv. The main response is RV_mlc_nzp, the corrected SERVAL velocity. DRS and SERVAL without nightly correction are extraction controls. They share spectra, so they are not independent instrument tests.

## Method

In each season the reference design X contains an offset, a linear time term, and sine and cosine terms at 4.69507 days and its first harmonic. The harmonic permits some orbit shape but is not an exact eccentric orbit. We use weights w = 1/(e_RV squared + 2 squared), with velocity in m/s. The added 2 m/s is a weight rule, not an inferred noise variance.

We center and scale each indicator with its early mean and population standard deviation. We fit the early data to X beta + Z gamma by weighted least squares. Z contains H-alpha alone, line width alone, or both. The later prediction uses the later measured indicators multiplied by the fixed early gamma. It therefore requires contemporaneous spectroscopy; it is not a forecast from time alone. No later velocities set gamma.

For later data, we fit X to y for the reference residual r0. We fit X to y - Z gamma for corrected residual r1. Thus, local offsets, trends and planet terms are refitted in both cases. We test correction of the extra residual, not prediction of the whole velocity. Gain is 1 - sum(w r1 squared)/sum(w r0 squared). A negative gain means higher error. The sine benchmark replaces Z by sine and cosine columns at the fixed prior period. The frequency is never searched in this study.

We resample occupied time bins with replacement, separately in each season. Each draw refits early gamma and later reference terms. Shared draws allow paired comparisons. We make 3000 draws each at 1, 10 and 30 days with bins anchored to each season's first exposure. We then make 2000 draws each with 10-day and 30-day bins anchored to BJD 2456380 plus 0, one-third, or two-thirds of the bin length. Random seeds are 951107 and 951108. Percentile ranges are conditional sensitivity measures. Few independent long bins, unknown correlations, and prior use of these data prevent a claim of calibrated population coverage. We do not report a planet false alarm probability.

## Results

| Correction | Later error reduction | Later weighted RMS, m/s |
| --- | ---: | ---: |
| Reference only | 0% | 2.295 |
| H-alpha | +0.58% | 2.288 |
| Line width | -5.26% | 2.355 |
| Both indicators | -7.54% | 2.380 |
| Fixed sine wave | +46.84% | 1.673 |

The early joint coefficients are +0.1923 and -0.5533 m/s per early standard deviation of H-alpha and line width. These are descriptive coefficients, not physical response constants.

With 30-day bins anchored to each season's first exposure, the joint gain range is -31.45% to +3.02%. The sine gain range is +5.62% to +56.84%. However, with bins anchored at BJD 2456380, the joint range is -39.04% to +3.99% and the sine range is -46.99% to +59.96%. Moving this common origin by 10 days gives a sine range of -101.47% to +62.69%. The paired joint-minus-sine ranges also change from excluding to including zero. Selection of one favorable bin origin would give excessive confidence. Files/intervals.csv and bin_origin.csv report every tested range.

All 36 combinations of three velocity products, three jitter weight rules (0, 2 and 4 m/s), and four baseline designs give negative joint gains, from -12.10% to -2.95%. The designs use the main basis, omit its trend, omit its harmonic, or add a linear Earth-velocity term. Sine gains remain positive, from +33.81% to +48.86%. These are related sensitivity tests, not 36 independent confirmations. Omitting each occupied later 30-day bin in turn gives joint gains from -8.30% to -6.41%; a single later bin does not set the sign. Earlier-season leverage and nonlinearity remain possible.

At the fixed period, separate fits of X plus sine and cosine columns give indicator phases relative to velocity of -88.6 and -105.5 degrees in 2013, and -112.2 and -76.9 degrees in 2014, for H-alpha and line width respectively. These phases are descriptive fits at a prior selected frequency; they have no supplied confidence interval. Both indicators lie near the same quadrature of velocity. Two such indicators need not span both phases of the velocity wave. Measurement noise and other variability also limit a linear correction.

Files/result.png shows residuals and one bin choice. Files/bin_sensitivity.png shows why this choice cannot alone support a confidence claim. Full outputs include exposure predictions, all resampling gains, controls, omitted-bin results and phase coefficients.

## Physical meaning and limits

Rotating spots and magnetic changes can alter line shape, emission and apparent velocity with different phases. The phase offsets permit this explanation for weak simultaneous linear correction. They do not identify a unique surface model. A relation with time delay, nonlinear terms or evolving coefficients can behave differently. No such model is validated here. Failure of this correction is not evidence for a companion.

The same spectra supply velocities and indicators. Shared measurement errors, spectral extraction errors and instrument drift can survive the tests. Alternative extraction, no nightly correction, one fibre era and an Earth-velocity term reduce some concerns but do not establish an astrophysical cause. The published independent photometry supports the general rotation context only. There is no independent observation of this exact failed transfer. This work establishes no new planet, unknown signal, or broad exclusion limit. It provides a reproducible limit on a simple activity correction in two selected seasons.

The two-harmonic orbit approximation can leave residuals. Indicator errors are not modeled. Weight errors, bin dependence, sample selection and activity evolution limit the result. A more complete joint orbit and activity analysis may improve prediction. The data are public and historically reused; no absolute novelty claim is made for the signal or its activity origin.

## Reproduce and inspect

Extract a verified bundle to a writable scratch directory. From that copy, run:

```
OPENBLAS_NUM_THREADS=1 python files/analyze.py
OPENBLAS_NUM_THREADS=1 python files/robustness.py
python files/verify_analysis.py
```

These commands require Python, NumPy, pandas, SciPy, Matplotlib and Pillow. They use only bundled input and write outputs beside the scripts. Versions are in files/summary.json. Do not rerun inside the signed draft because outputs are signed files. Verification checks the raw hash, a separate normal-equation coefficient solution, independent gain calculations, weighted residual means and display limits. Normal-equation and SVD coefficients agree within 2e-15 in the main fits. The plotted image was inspected. All computations ran locally and finished before signing.

Job: sci-1107-dell-astronomy-95daa83b9bf8. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim. The baseline license applies to original text, code, figures and derived outputs. External source attribution and rights remain with their sources.
