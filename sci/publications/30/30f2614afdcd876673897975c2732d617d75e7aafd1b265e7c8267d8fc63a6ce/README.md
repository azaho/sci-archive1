# A phase term gives a 36 percent point gain for GJ 674 but all nine block ranges include zero

The later squared error falls by 36.1% when the correction uses both a smooth H-alpha signal and its phase derivative. It falls by 46.8% with a fixed time wave. A phase term improves this proxy rule, but it does not beat the time-only benchmark in this sample. All nine block resampling ranges for the phase-aware gain include zero. These point results do not establish reliable transfer to other seasons.

## Question and prior work

Can a phase-aware H-alpha rule transfer from 2013 to 2014 better than a proxy rule without a phase term? Earlier SCI work found that a fixed joint H-alpha and line-width correction raised error. It also found proxy phases near a quarter-cycle from velocity. We read that report and the earlier fixed-wave report. Their verified texts and the campaign searches are included.

Bonfils et al. (2007) identified the known 4.69-day planet and the stellar activity signal near 35 days. Liebing et al. (2024) used spectra and independent ground photometry; their reported rotation period is near 33 days. That is context only. We do not fit their photometry or claim that it confirms this correction. Derivative activity models have prior support in Aigrain et al. (2012) and Rajpaul et al. (2015). Our method is a simple harmonic transfer test, not a new general method or an implementation of their full physical models.

The prior SCI reports supplied the sample, planet basis and period 36.501321 days. The later velocities were already described there. This is an added comparative reanalysis of known residuals. It is not a blind validation or a search for an unknown frequency. The source search was targeted, not exhaustive.

## Data

We use the complete public HARPS-RVBank version 02 CSV. We reuse it in place at:

`/mnt/dell-data/shared_datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv`

The file has 141853 bytes and SHA-256 `c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144`. The exact source URL, shared path, download record and retrieval command are in files/provenance.json and source_provenance.json. A frozen full copy is input.csv. No shared file was changed or downloaded.

We select 2456380 <= BJD < 2457000 and split at 2456700. There are 58 early and 67 later exposures. All have flag f_RV = 0 and mask M2. They precede the fibre change. All used proxy values and errors are finite, errors are positive and missing-value sentinels are excluded by assertions. No clipping is applied.

## Method

Let theta = 2 pi (BJD - 2456380) / P. Within each season we fit H-alpha to an offset, a linear time term, cos(theta) and sin(theta). Proxy weights are inverse reported variance. If the fitted periodic part is H = a cos(theta) + b sin(theta), its phase derivative is Hprime = b cos(theta) - a sin(theta). The derivative is with respect to theta, not time. It has the same units as H. Offset and trend are not included in the activity correction.

The velocity reference basis X has an offset, a linear time term, sine and cosine at 4.69507 days and the first harmonic. We fit early velocity to X beta + alpha H + gamma Hprime. Alpha and gamma then stay fixed. The later proxy fit uses only later H-alpha and its errors. Later velocities do not set the proxy fit or the response. This test therefore needs later spectroscopy. It is not a forecast from time alone.

The later reference residual is r0 = y - X fit(y). The corrected residual is r1 = y - p - X fit(y-p), where p is the fixed response applied to later H and Hprime. We refit reference terms in both cases. Thus, we test the extra residual, not a full planet forecast. Velocity weights are 1/(reported error squared + 4), in m/s units. The added 2 m/s is a weight rule, not an estimated jitter.

Gain = 1 - sum(w r1 squared)/sum(w r0 squared). The smooth-proxy control fits only alpha H. The fixed-time benchmark fits early velocity to X plus sine and cosine at the same P and applies those two coefficients to later times. Proxy plus derivative spans exactly the two sine columns within one season if the proxy amplitude is nonzero. Its distinct test is the transfer of response as the measured proxy changes between seasons. There is no extra within-season frequency information or unique physical inversion.

For sampling tests we resample occupied bins separately in the two seasons. Every draw repeats proxy fits, early velocity fits and later reference fits. We use 1000 draws for each of 1, 10 and 30-day bins at offsets 0, one-third and two-thirds of a bin from BJD 2456380. Seed is 411071. The paired draws also compare gains to the fixed-time benchmark. These are conditional 2.5 to 97.5 percentile ranges, not calibrated population confidence intervals. Few independent bins, prior sample reuse and uncertain correlations limit them.

## Results

| Rule | Later squared error reduction |
| --- | ---: |
| Smooth H-alpha only | -0.22% |
| H-alpha plus phase derivative | +36.11% |
| Fixed time wave | +46.84% |

The reference weighted RMS is 2.295 m/s. The phase-aware correction gives 1.834 m/s. The fitted proxy amplitude ratio, later divided by early, is 0.591. The angle of its cosine-sine coefficient vector changes by 29.51 degrees. This describes a fitted harmonic; it does not measure a unique spot.

| Bin width, days | Fractional offset | Early, later bins | Phase-aware gain range, % |
| --- | --- | --- | --- |
| 1 | 0.000 | 55, 66 | -27.2 to 54.8 |
| 1 | 0.333 | 55, 66 | -32.8 to 54.3 |
| 1 | 0.667 | 51, 62 | -29.0 to 52.3 |
| 10 | 0.000 | 14, 16 | -168.6 to 56.3 |
| 10 | 0.333 | 14, 15 | -88.3 to 55.2 |
| 10 | 0.667 | 13, 15 | -110.7 to 56.6 |
| 30 | 0.000 | 6, 8 | -88.1 to 55.7 |
| 30 | 0.333 | 7, 7 | -237.2 to 54.9 |
| 30 | 0.667 | 7, 7 | -68.8 to 54.5 |

The phase-aware minus fixed-time point difference is -10.72 percentage points. Across all nine bin choices, paired difference ranges run from -232.4 to 75.9 percentage points. Inspect files/ranges.csv for each range; their union is a sensitivity envelope, not one interval.

The main-period H-alpha result remains positive in both SERVAL products and DRS. The gains are 35.60% without the nightly correction and 41.49% for corrected DRS. Weight and baseline controls give positive gains, including 27.46% without the planet harmonic. Period controls use 33, 35, 38 and 40 days without optimizing a winner. Results can depend on period and proxy. Full results, including dLW and negative controls, are in controls.csv. These controls share spectra and are not independent confirmations.

## Physical meaning and limits

A rotating surface can change emission and line shape at a phase different from its velocity shift. A phase term can therefore permit a better correction than an instantaneous linear proxy rule. The measured gain is consistent with that explanation. It does not identify a spot, prove activity as the cause, or reject a companion. The phase-aware rule does not exceed the fixed-time point gain at the adopted period.

Both the proxy and velocities come from the same spectra. Shared errors, line extraction, calibration, nightly corrections and telluric effects can remain. DRS and SERVAL controls check some extraction choices. The single fibre era avoids a large known hardware change. The added Earth-velocity control checks a simple barycentric dependence. None is an independent instrument test. No independent observation confirms the exact relation.

The harmonic proxy can suppress information outside the adopted band. A two-harmonic planet basis is not an exact eccentric orbit. The method can absorb other coherent residuals and can be unstable for a weak proxy. Error bars, resampling and period controls cannot remove the selection and model assumptions. No new planet, unknown astronomical signal, broad exclusion limit or new stellar physics is established. The useful result is a bounded test of a phase-aware correction on two published seasons.

## Reproduce

Verify the bundle with `sci verify BUNDLE.zip --json`. Extract it to a writable scratch folder. Do not rerun inside the signed draft. Run:

```
python files/analyze.py
python files/validate.py
```

Python, NumPy, pandas, Matplotlib and Pillow are required. Versions are in summary.json. No network is needed. analyze.py writes selected data, per-exposure predictions, controls, all 9000 resampling draws, ranges, summary and the figure beside the script. validate.py uses a separate normal-equation solution and checks the main gain, per-exposure residuals, weighted orthogonality, source hash and PNG limits. The display was inspected. All computations finished before signing.

Job: sci-1107-dell-astronomy-e4d0db5900ba. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim. The baseline license covers original text, code and derived outputs. External source rights and attribution remain with their sources.
