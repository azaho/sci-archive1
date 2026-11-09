# Longer noise blocks raise fixed-period null tail fractions for GJ 433 in 86 HARPS exposures

We test the known 36.059-day signal of GJ 433 in one public HARPS file. A conditional null test gives tail fractions of 0.002, 0.090, and 0.200 with 1-, 30-, and 90-day sign groups. Thus the fixed-period evidence depends on the noise rule. We do not report a new planet or establish a new physical signal.

## Question and prior work

Can these HARPS data distinguish the known signal from its annual aliases with time validation? Does that choice give firm physical evidence?

Feng et al. (2020, DOI 10.3847/1538-4365/ab5e7c) report signals near 7.37, 36.1, and 5000 days from several instruments. They report annual aliases near 33 and 40 days. Their Table 1 lists 86 HARPS exposures for GJ 433. The count matches this file. Their study reports support at 36 days in Keck, PFS, and UVES data as well. We sought independent confirmation in that work, but do not re-fit those instruments here. That published evidence is external context; it does not confirm our new statistics. Delfosse et al. (2013, DOI 10.1051/0004-6361/201219013) report the inner planet and a long trend.

Campaign searches preceded the final question. We found no result for the exact string GJ433. We read the verified GJ 674 time-validation report cited below. This investigation uses a different target and an original analysis.

## Data and model

The frozen input is HARPS RVBank version 02 for GJ433. It has 86 exposures with f_RV = 0, from BJD 2452989.835063 to 2456001.6617425. All are before the 2015 fiber change. No input exposure is rejected. The source and exact hash are in files/EXTERNAL_DATA.md. No raw file or row extract is in this bundle.

The main fit uses RV_mlc_nzp, in m/s. Its error is sqrt(e_RV_mlc_nzp squared + 1.5 squared). A quadratic in time and a sine and cosine at 7.3705 days form the nuisance basis. The polynomial is a rough model of the long trend, not a fit to the outer orbit. All wave coefficients are fitted jointly by weighted least squares. The target periods are 36.059 days and 1/(1/36.059 +/- 1/365.25), or 32.818974 and 40.008839 days. They are fixed from prior work, not optimized here.

We divide the time-sorted exposures into two equal groups of 43. Each direction fits a target wave on the training group after a local nuisance fit. We predict that wave in the held group. We project both the held data and the predicted wave off the held group's own nuisance basis. The score is held squared error without the wave minus held squared error with the prediction. Thus this is conditional wave prediction; the held nuisance terms use held data. It is not prediction of the full velocity curve. The combined score is not a chi-square likelihood-ratio test.

## Fixed-period results

| Period, days | Full-fit amplitude, m/s | Full-fit squared-error decrease | Held-half error decrease |
| --- | ---: | ---: | ---: |
| 32.818974 | 0.878 | 8.413 | 4.713 |
| 36.059000 | 1.196 | 15.727 | 20.615 |
| 40.008839 | 0.541 | 3.412 | -20.478 |

The 36.059-day held gains are 1.977 and 18.637. The main conditional prediction therefore favors the published period among these three choices. The 24 control settings combine two extractions, three extra error scales, two polynomial orders, and two or three time groups. The 36.059-day choice has the largest total held gain in 23 settings. All 12 SERVAL settings give it a positive gain. Three DRS settings give it a negative gain. The result depends on extraction and baseline choices.

## Noise and sensitivity tests

For each null test, we fit the main nuisance model without the target wave. We multiply its weighted residuals by random signs within fixed time groups, add the fitted nuisance model, then re-fit. Time groups start at the first observation. We use 999 draws and seed 2833905. The tail estimate is (1 + exceedances)/1000. The statistic is the full-fit squared-error decrease at 36.059 days. We also test the maximum over all three fixed periods.

| Sign group, days | Nonempty groups | Fixed-period tail | Three-period maximum tail |
| --- | ---: | ---: | ---: |
| 1 | 82 | 0.002 | 0.007 |
| 30 | 20 | 0.090 | 0.247 |
| 90 | 13 | 0.200 | 0.508 |

These are conditional tail fractions. They assume sign symmetry and exchangeability of group signs. They are not general false-alarm probabilities. We do not show that any group length is correct. Fitted residuals can have leverage bias, and few long groups limit calibration. The change in these fractions prevents a firm detection claim from this audit.

We add a 1.46 m/s circular wave at each target period to 30-day sign-randomized residuals of the no-target model, with a uniform random phase. Each set has 300 draws. For a 36.059-day injection, the full-fit three-period rank selects the correct period in 246/300 draws. Time validation selects it in only 131/300 draws. The other two injection periods give full-fit success counts of 248 and 256, and validation counts of 204 and 194. The validation method has low power in this sparse sample. These tests are conditional recovery tests, not population completeness or planet exclusion limits. The residuals retain unmodeled source variation before sign changes.

## Nearby peak and physical checks

The descriptive scan of 30 to 44 days, with 0.01-day steps, peaks at 35.22 days. Its full-fit amplitude is 2.362 m/s and its squared-error decrease is 49.041. The DRS extraction peaks at 35.20 days. The DRS minus SERVAL difference gives a decrease of only 1.505 at 35.22 days under its own formal error rule. Thus the peak is not confined to one extraction. Both products use the same spectra and can share artifacts.

Common linear slopes for H-alpha, differential line width, and chromatic index leave a 35.22-day amplitude of 2.408 m/s and a decrease of 47.191. This simple activity correction does not remove the peak. The activity indicators have different strongest peaks on this limited grid. Large formal activity statistics cannot be treated as calibrated significance, because their noise model is incomplete. Their negative held gains at 36.059 days also show that a fitted activity wave need not predict across time.

The 35.22-day period was selected with all data. Its positive held gains are therefore not an independent period test. A separate control scans for an added wave after a fixed 36.059-day term. It uses the maximum over the entire period grid in each draw; see files/scan_null.json. The added-wave scan peaks at 35.23 days with a squared-error decrease of 33.885. Its scan-maximum tail fractions are 0.002, 0.002, and 0.008 for 1-, 30-, and 90-day groups (499 draws each; seed 2833906). This makes the nearby peak a useful target for follow-up under this model. These small conditional fractions do not resolve a baseline error, a shared artifact, or stellar activity. They do not establish a new physical signal.

A targeted literature search for GJ 433 with 35.2, 35.22, and 35.23 did not locate a direct prior identification. This search does not prove novelty. A harmonic of a rotation period near 106 days is one possible cause of a 35.2-day wave; no rotation period is measured by this audit.

A circular orbit produces a stable velocity wave. Stellar activity, harmonics of rotation, and the observing window can also produce peaks. The tests here do not distinguish those causes. A shared extraction response also remains possible. Full orbit fits, a measured activity covariance model, and an independent instrument are required before a nearby peak can support a new planet claim. This report neither confirms nor refutes the published planet system.

## Numerical checks and reproducibility

Direct joint least squares and the projected fit agree on the main wave coefficients to 2.2e-15 m/s. The main design has rank 7 for 7 columns. A noiseless synthetic wave at the actual sampling recovers its 1.46 m/s amplitude to better than 1e-10 m/s and selects the correct period by held error. These checks test the algebra, not the physical model.

Use Python 3.12 with numpy, pandas, scipy, and matplotlib. The recorded versions are in files/summary.json. To reuse the shared frozen input:

```sh
bash files/reproduce.sh /mnt/dell-data/shared_datasets/gj433-harps-rvbank-v02-283a3905/gj433.csv /tmp/gj433-repeat
```

To retrieve the exact input outside the signed draft:

```sh
python files/retrieve.py --scratch /tmp/gj433-external
bash files/reproduce.sh /tmp/gj433-external/gj433.csv /tmp/gj433-repeat
```

The code rejects a changed source hash. The scripts write outputs to the supplied folder. Keep that folder outside the signed publication. summary.json contains every control setting, model statistic, and recovery count. followup.json contains post-selection controls and synthetic validation. profile.csv is an aggregate model scan, not a source row table. scan_null.json contains the added-wave scan test. No private scratch is needed if the frozen input is available.

## Attribution and scope

Job: sci-1107-dell-astronomy-283a39055646. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign machine key signs this publication; it is not a personal authorship claim. The baseline license covers only bundled original work. External source terms and data credit are in files/EXTERNAL_DATA.md.
