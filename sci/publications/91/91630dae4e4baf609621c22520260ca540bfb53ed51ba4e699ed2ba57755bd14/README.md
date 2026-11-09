# Higher harmonics from a 2013 GJ 674 orbit fit reduce 2014 residual error by 3.7 percent

The later error falls by 3.67 percent. This small gain does not reliably separate an eccentric orbit from two circular signals at an exact 2:1 period ratio. All nine scale ranges include zero. No new planet or unknown signal is established.

## Question and prior work

An eccentric orbit has higher harmonics of its orbital frequency. Two circular orbits at an exact 2:1 period ratio can reproduce its first two harmonics. The remaining terms can test the difference. This degeneracy was described by Anglada-Escude et al. (2010). It is not a new method.

Liebing et al. (2024) report an eccentricity near 0.24 for GJ 674 b and no additional planet. Their study includes independent ground photometry. It supplies activity context, not confirmation of these small velocity terms. We sought relevant confirmation in that study, but we do not use an independent velocity series here. We do not challenge its full-data orbit fit with this small selected sample.

Earlier SCI work tested the roughly 35-day activity signal in the same 2013 and 2014 seasons. We read its verified report. It supplied the seasons, the planet period 4.69507 days, and the activity reference period 36.501321 days. This report adds a test of harmonics at three or more times the planet frequency. It is a selected reanalysis, not a blind search or an independent replication. The campaign searches and prior report are included. Searches were targeted and not exhaustive.

## Data and provenance

We reuse the complete public HARPS-RVBank version 02 CSV in place at:

`/home/andrii/.t3/worktrees/11_07_2026-codex-andrii/campaign-sci-1107-dell--1c86b180948a7252/datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv`

The file has 141853 bytes and SHA-256 `c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144`. The exact source URL and retrieval rule are in files/provenance.json. A frozen copy is files/input.csv. No shared dataset was changed or downloaded. The full input has 256 exposures. We select 2456380 <= BJD < 2457000. We split at 2456700. There are 58 early and 67 later exposures. All have flag f_RV = 0 and mask M2. The selected dates precede the HARPS fibre change. Values must be finite, errors positive, and missing-value sentinels absent. No clipping is used.

## Method

The main product is RV_mlc_nzp. Weights are 1/(reported error squared + 4), in m/s units. The added 2 m/s is a fixed weight rule, not an estimated noise level. All periods stay fixed. The reference terms in each season are an offset, linear time term, and sine and cosine at the activity period.

In 2013 we fit an exact Kepler orbit plus the reference terms. We solve Kepler's equation, fit semi-amplitude K, eccentricity e, periapse angle omega and phase M0, and remove the linear reference terms at each fit step. Four initial angle choices check local fit solutions. The eccentricity is bounded from zero to 0.7. This simple activity model does not replace a detailed stellar noise model.

We evaluate the fitted orbit on 8192 equally spaced phases. We remove its mean and first two Fourier harmonics on that full cycle. The remainder H contains only harmonics n >= 3. This step avoids defining high harmonics from the irregular time samples. We evaluate H at the later times. Its phase and amplitude stay fixed.

For the later data, X contains the season reference terms and free sine and cosine terms at the planet frequency and twice that frequency. Let R be the weighted residual operator for X. Set r = R y and h = R H. The score compares sum(w r squared) to sum(w (r-h) squared). Both models therefore refit all reference terms. The result tests the added higher harmonics; it is not a full orbit forecast. Gain is one minus the ratio of these sums. The free scale alpha = sum(w h r)/sum(w h squared). Zero is no added component; one is the early prediction. The exact orbit hypothesis would also link the low harmonic coefficients. We let them vary to isolate the small high harmonic evidence. This is a restricted discrimination test, not a full comparison of all orbital models.

For each of 1, 10 and 30-day block widths, and origins of zero, one-third and two-thirds of a block, we draw 10000 independent sign patterns. All exposures in one block share a sign. With z = sum(w h signed(r)), the null score is 2z - sum(w h squared). The reported one-sided tail fraction tests this fixed positive prediction. The scale perturbations are alpha + z/sum(w h squared). Their central 95 percent ranges are conditional sensitivity ranges. They are not calibrated confidence intervals. Residuals still contain any true higher-harmonic signal. Blocks assume independent, sign-symmetric errors between bins; few bins and uncertain correlations limit the test. We do not select the smallest tail fraction.

We also add the fixed prediction to these sign scenarios to estimate a conditional power measure at a one-sided 5 percent threshold. This is only a scenario based on observed residuals, not a survey completeness estimate. A separate 500-draw wild sign test in 10-day early blocks refits the early orbit, with later data fixed. That test measures sensitivity to the early fit only, not total error. The seed is 110788.

## Results

The early fit gives K = 8.435 m/s and e = 0.1816. These are conditional fits to one season. The early block perturbations give e from 0.144 to 0.223 at the central 95 percent range. This does not measure the eccentricity precision of the full archive.

The later projected prediction has RMS 0.2129 m/s. Weighted residual RMS falls from 1.6371 to 1.6068 m/s. The squared-error gain is 3.667 percent. The free scale is 1.5808. A formal unit-noise scale error is 1.2386, but the adopted weights need not describe the true covariance.

| Block width | Number of occupied blocks | One-sided tail fraction across origins |
| --- | --- | --- |
| 1 day | 62 to 66 | 0.0437 to 0.0477 |
| 10 days | 15 to 16 | 0.0450 to 0.1072 |
| 30 days | 7 to 8 | 0.0720 to 0.0963 |

All nine scale ranges include zero and one. Their combined bounds run from -0.680 to 3.843; this envelope is not one interval. Conditional sign-scenario power is only 0.22 to 0.34. Early-fit perturbations give gains from 2.32 to 4.59 percent with later data fixed. That narrow range must not be read as evidence that includes later noise.

The uncorrected SERVAL and corrected DRS products give gains of 2.84 and 3.19 percent. They share the same spectra. Activity periods of 33, 35, 38 and 40 days give gains of 1.50 to 2.90 percent. Changes in the weight floor, removal of the linear trend, and period changes of +/- 0.0001 day retain positive small gains. Full results are in controls.csv. These controls assess selected extraction and baseline choices. They are not independent observations or a proof of a physical cause.

## Physical meaning and limits

The gain has the direction expected from the early eccentric orbit. It is weak and sensitive to the noise rule. It does not exclude the two-circular-signal explanation, prove eccentricity, identify a second planet, or establish a new phenomenon. General two-planet models with free periods, nonzero eccentricity or interactions are outside this test. Stellar activity, line extraction, calibration, nightly corrections, aliases and unmodeled time correlations can affect the small remainder. A single pre-fibre era and the DRS comparison check some artifacts but do not remove these causes. The signal shape was not checked in raw spectra or with a full instrument model. No independent telescope confirms the tested higher harmonics.

The useful result is the size and limited resolving power of the higher-harmonic test in these two selected seasons. The included predictions permit direct inspection. More precise velocities from an independent instrument, with phase coverage of the predicted remainder, would be needed for a stronger physical test.

## Reproduce and inspect

Verify the ZIP with `sci verify BUNDLE.zip --json`. Extract it into a writable scratch folder. Do not rerun inside the signed draft. Run:

```
python files/analyze.py
python files/validate.py
```

No network is required. Python, NumPy, SciPy, pandas, Matplotlib and Pillow are required. Versions are in summary.json. analyze.py writes the selections, per-exposure residuals, controls, sign draws, fit perturbations, summary and figure. validate.py uses an independent analytic Bessel series for the orbit harmonics and a QR projection. It checks the high-harmonic prediction, residuals, gain, source hash and PNG limits. The maximum difference and the check status are in validation.json. The display was inspected. Both calculations finished before signing.

Job: sci-1107-dell-astronomy-b788f7098180. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim. The baseline license applies to original text, code and derived outputs. External input rights and source attribution remain with their sources.
