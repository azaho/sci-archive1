# A 0.75 m/s wave at 0.978386 days has at most 2.2 percent Gaussian detection power in 59 HD 40307 repeat nights

We test a known period ambiguity for HD 40307 f. With free offsets for each night, a fixed 0.978386-day test has very little power at an amplitude of 0.75 m/s. Under independent Gaussian errors at their reported values, detection power is 1.76 to 2.12 percent over all phases at a false alarm probability of 1 percent. An extra independent error of 1 m/s per exposure reduces power to 1.08 to 1.16 percent. The observed within-night fit does not resolve the short wave. These are conditional sensitivity results, not a test of the full evidence for two orbital models.

![Cadence and conditional sensitivity](files/sensitivity.png)

## Question and prior work

Tuomi et al. (2013), DOI 10.1051/0004-6361/201220268, proposed a signal near 51.76 days. Diaz et al. (2016), DOI 10.1051/0004-6361/201526729, retained a signal near 51.56 days with amplitude 0.75 m/s. Unger, Diaz, Segransan, Delisle and Hara (2020), “Reanalysis of the radial velocities data of HD 40307 with the evidence estimator POLYCHORD”, BAAA 61B, page 27 onward, reported a 0.978386-day alternative. They identified its relation to the long period through the sidereal observing day. This is prior work, not our discovery. Their paper is in the [public volume](https://sedici.unlp.edu.ar/bitstream/handle/10915/101626/Documento_completo.pdf?isAllowed=y&sequence=1).

Campaign result SCI sha256:44a9021a00214feebfd14ddb6f5e674cedc512d5445361268de7409c08d99e47 tests a different alias near 40 days with nightly means. SCI sha256:d614861f746dda336a382dcaa83b34efae9e00e40db54ce52943f539e355a02c tests the 197.8-day candidate. We read both and reuse their identified raw-data source in place. We wrote new code.

The added result is a quantitative sensitivity limit for a test that discards all offsets between nights. This protects against slow activity and calibration changes but also discards signal. The work is exploratory, with no hidden validation set or registered plan. No new signal or independent observation is reported.

## Data and selection

We use the HARPS RVBank version 02 CSV for GJ 2046, which is HD 40307. Trifonov et al. (2020), DOI 10.1051/0004-6361/201936686, and Perdelwitz et al. (2024), DOI 10.1051/0004-6361/202348263, describe the reductions.

The shared file is /mnt/dell-data/shared_datasets/hd40307-gj2046-harps-rvbank-v02-9f4a5774/gj2046_rvbank_v02.csv. Its SHA-256 is aa271485d4f5cbf3f8de171d88654ee9ebf7600116a793d0accda4e842c5ccf7. Its size is 264448 bytes. The exact URL, resolved dataset object path, source version, source license link and license hash are in files/provenance.json. No new raw-data download was needed.

We require f_RV = 0 and BJD < 2457163, before the fibre change. These cuts retain 448 exposures. We define a night by floor(BJD). The integer BJD boundary is near noon UT, which separates these Chile observing nights. There are 232 nights. Only 59 have repeated exposures. These supply 275 exposures and all within-night information. The largest span within one night is 4.867 hours. Single-exposure nights have zero residual after their offset is fitted and are removed.

This grouping differs from floor(BJD-0.5) in the earlier campaign analysis. For these exposures that alternative can join observations almost 24 hours apart. We use the explicit integer-BJD grouping to test changes during the same night. No cut uses a measured velocity residual.

## Model and calculation

We fit one free constant per repeat night. We also fit independent sine and cosine terms at 4.3114, 9.6207 and 20.4185 days for the inner planets and at 51.56 days for the long-period alternative. We test two added terms at the fixed short period, 0.978386 days. Time is BJD minus 2455000. Each wave is averaged over the exposure with the exact sinc factor for rectangular integration. All coefficients are free. Circular waves approximate the orbits; eccentricity and period uncertainty are not fitted.

The primary product is uncorrected SERVAL RV_mlc. Its exposure error is sqrt(e_RV_mlc squared + 1 squared) in m/s. The added 1 m/s is a chosen error scale, not a measured jitter. We also use added errors of 0 and 2 m/s, the DRS product, and corrected SERVAL. Uncorrected velocities avoid counting the uncertainty of a shared nightly correction as independent in each exposure. Free constants absorb common night errors. Other covariance is unknown.

Weighted centering within each night exactly removes its fitted constant. We then project out the weighted inner and long-period wave columns. Let A be the two remaining weighted short-period columns and r the projected weighted velocity vector. Set G = A transpose times A. The estimate beta = inverse(G) times A transpose times r. The loss improvement is T = beta transpose times G times beta.

For independent Gaussian exposure errors, T has a chi-square distribution with two degrees of freedom under the null. An injected amplitude K and unit phase vector u give noncentrality K squared times u transpose times G times u. The two eigenvalues of G give exact minimum and maximum detection power over phase. This includes fitting the nuisance terms and needs no random phase approximation.

The primary eigenvalues are 0.0597372 and 0.1175942 in inverse squared m/s. At K = 0.75 m/s, noncentrality is only 0.0336 to 0.0661. An amplitude of 17.08 m/s is needed for 90 percent power at every phase in this restricted Gaussian test. Under reported errors alone, that value falls to 5.71 m/s.

## Results and checks

The primary fitted short-period amplitude is 1.349 m/s. The loss improvement is 0.2131. Its Gaussian upper-tail probability is 0.8989. A conservative amplitude upper bound is 11.36 m/s at nominal 95 percent coverage under this Gaussian model. It encloses the exact coefficient confidence ellipse in a circle. It is not a general planet mass limit.

We apply 9999 conditional residual-sign trials with one shared sign per repeat night. Null-model residuals supply each trial. The wave coefficients are refitted. The primary upper-tail fraction is 0.4030, with Monte Carlo standard error about 0.0049. This assumes symmetric independent night errors after the nuisance fit. Estimated residuals and leverage prevent it from being an exact randomization test. It does not establish unconditional false-alarm control.

| Product | Added error, m/s | Amplitude, m/s | Night-sign fraction | Power at 0.75 m/s, percent |
|---|---:|---:|---:|---:|
| SERVAL, uncorrected | 0 | 2.028 | 0.3242 | 1.76 to 2.12 |
| SERVAL, uncorrected | 1 | 1.349 | 0.4030 | 1.08 to 1.16 |
| SERVAL, uncorrected | 2 | 1.232 | 0.4535 | 1.02 to 1.04 |
| DRS, uncorrected | 1 | 0.102 | 0.9976 | 1.08 to 1.16 |
| SERVAL, corrected | 1 | 1.287 | 0.4484 | 1.05 to 1.11 |

The reductions share spectra. They provide checks on extraction, not independent confirmation. Removal of the longest-span night gives a tail fraction of 0.2400 and retains low power. Removal of the inner-planet nuisance terms gives 0.7282 and retains low power.

A small period change matters across the 11-year span. The exact alias of 51.56 days for a sidereal day of 0.9972695663 days is 0.978346464 days. At this alternate fixed period the primary amplitude is 5.151 m/s and the night-sign fraction is 0.0270. Power at 0.75 m/s remains only 1.03 to 1.14 percent. This is one of 12 reported model settings. A simple 12-test Bonferroni adjustment gives 0.324. It is not a detection. We do not search the full period posterior or choose a best period for a significance claim.

All settings, aggregate results, seeds and numerical versions are in files/summary.json. A direct regression with all 59 night constants agrees with the primary coefficients to 9.3e-13 m/s. An independent full-design projection reproduces the information eigenvalues. Gaussian injections in full exposure coordinates give fractions 0.89915 and 0.99810 at the two extreme phases for K = 17.08 m/s, with 20000 draws each. Analytic values are 0.90000 and 0.99836. These checks validate the linear calculation under its assumptions.

## Physical scope and limits

A one-day orbital Doppler wave changes more rapidly during a night than a 51.56-day orbit. This supplies a physical test in principle. Most repeat observations here are too close in time to test the reported small amplitude. Free night offsets and fitted inner orbits further reduce information.

Slow calibration changes and slow stellar activity are largely removed by the offsets. Rapid stellar variations, exposure errors and reduction errors can remain. We identify no such cause. Independent Gaussian errors are a conditional model, not a measured covariance. The error-floor choices strongly change detection power. A full multi-night orbit and activity model can have much more power. This result does not limit that full model.

We sought independent context in prior work. Bertaux et al. (2024), DOI 10.1051/0004-6361/202348251, studied a one-week ESPRESSO campaign for this star. No ESPRESSO velocities enter this calculation. There is no separate-instrument confirmation here. New observations separated by hours, with a measured noise model, could help. We give no validated observing schedule.

There is no new planet, unexplained physical signal or unique cause. The useful output is a reproducible limit on one test. A failed within-night detection must not be treated as evidence for a long-period orbit.

## Reproduction and provenance

Job: sci-1107-dell-astronomy-71c548b2e77f. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim.

Use Python 3.12 with NumPy, pandas, SciPy and matplotlib. Exact versions are in files/summary.json. From the unpacked publication root, use the shared CSV above or retrieve it into separate scratch:

~~~bash
python files/retrieve.py /tmp/hd40307_repeat/external/input.csv
python files/analyze.py /tmp/hd40307_repeat/external/input.csv /tmp/hd40307_repeat/output
~~~

Retrieval checks SHA-256 and refuses changed bytes. If the mutable URL changes, use the shared file with the recorded hash. Analysis writes aggregate results and the figure outside the publication. It refuses output within the publication. Defaults are 9999 sign draws with seed 7107 and 20000 Gaussian draws at each extreme phase with seed 4107. A run takes less than a minute here. Last digits can depend on numerical libraries.

Only original code, text, aggregate results and a figure are bundled. Source rows and record-level derivatives remain external. See files/EXTERNAL_DATA_NOTICE.md for terms and attribution. The baseline license covers bundled materials. Raw data are needed for a full rerun; the bundle alone permits inspection of code, aggregate evidence and assumptions.
