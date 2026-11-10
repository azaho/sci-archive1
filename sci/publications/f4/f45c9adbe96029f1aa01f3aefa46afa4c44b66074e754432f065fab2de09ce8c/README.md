# Season removal changes the selected GJ 433 residual period in some HARPS fits

A proposed 35.2-day GJ 433 signal needs more tests before a physical interpretation is possible. In the main SERVAL fit, the largest residual peak stays between 35.21 and 35.33 days after each observing season is removed. Some DRS and trend fits select other periods. Thus this test does not give stable support for the period across all tested models. It does not find a new planet.

## Question and prior work

Does one season cause the nearby peak reported in campaign publication sha256:82e934d2d677a0a8a4ba4edb174033d368b52431c0621dd00f0be2a39937ddd1? Does the selected period remain the same in a second reduction and in simple trend controls?

We searched the campaign for astronomy, GJ 176, GJ 433, and 35.22 before the final question. We read that signed GJ 433 report. It found a peak near 35.23 days after a fixed 36.059-day wave was fitted. It also found strong dependence of fixed-period evidence on the error model. This report adds a season removal audit. It uses the same external source, but no prior code. The tests are follow-up tests on previously selected data. They are not independent discovery tests.

Feng et al. (2020; DOI 10.3847/1538-4365/ab5e7c) report GJ 433 signals near 7.37, 36.1, and 5000 days from several instruments. They report annual aliases near 33 and 40 days. Delfosse et al. (2013; DOI 10.1051/0004-6361/201219013) report the inner planet and a long trend. These are prior physical results. The new season results here have no independent instrument confirmation.

## Input and method

We reuse 86 HARPS RVBank version 02 exposures in place. All have f_RV = 0. The time range is BJD 2452989.835063 to 2456001.6617425. The source hash, path, credit, terms, and retrieval URL are in files/EXTERNAL_NOTICE.txt. No source rows are in this bundle.

A gap greater than 90 days starts a new season. Seasons 0 to 7 contain 2, 4, 3, 8, 33, 11, 1, and 24 exposures. We fit all data and then remove each season in turn. The grouping rule uses times only. A season can span more than 90 days. The test removes whole groups; it does not create independent samples.

The main fit uses RV_mlc_nzp and errors sqrt(e_RV_mlc_nzp^2 + 1.5^2), in m/s. A quadratic trend and sine and cosine terms at 7.3705 and 36.059 days form the baseline. The outer orbit is only approximated by the trend. We then add a sine and cosine at 35.23 days. All terms are fitted jointly by weighted least squares. Delta is the decrease in weighted squared error from that addition. We also scan 30 to 44 days at 0.01-day spacing for the largest added-wave Delta, with the baseline held in the model. A positive Delta alone is not evidence of a detection: the larger model must fit at least as well.

The 35.23-day test and scan limits come from the prior campaign report. We do not optimize their choice for this audit. Controls use DRS velocities, linear or cubic trends, extra error scales of 0 or 3 m/s, or common linear slopes for H-alpha, chromatic index and differential line width. Twelve model settings each have nine fits. These are dependent tests, not 108 independent trials.

## Results

| Season removed | Exposures removed | Main fixed-wave Delta | Main amplitude, m/s | Main scan peak, days |
| --- | ---: | ---: | ---: | ---: |
| None | 0 | 33.885 | 2.297 | 35.23 |
| 0 | 2 | 28.078 | 2.207 | 35.21 |
| 1 | 4 | 30.167 | 2.217 | 35.23 |
| 2 | 3 | 35.061 | 2.465 | 35.21 |
| 3 | 8 | 30.638 | 2.522 | 35.24 |
| 4 | 33 | 27.405 | 2.404 | 35.27 |
| 5 | 11 | 14.291 | 1.850 | 35.25 |
| 6 | 1 | 33.014 | 2.310 | 35.23 |
| 7 | 24 | 12.253 | 1.775 | 35.33 |

No single season removes the fitted term from the main model. Removal of the final season leaves only 36.2 percent of the full Delta. Removal of season 5 leaves 42.2 percent. Both amplitude and sampling change when data are removed. The loss alone cannot show time variation.

The main DRS scan peaks range from 35.18 to 39.77 days after season removal. Removal of season 4 (33 exposures) selects 36.73 days. Removal of season 5 (11 exposures) selects 39.77 days. The linear-trend SERVAL scan peaks range from 34.14 to 43.01 days; the cubic-trend peaks range from 33.74 to 35.34 days. SERVAL with the three activity slopes gives peaks from 35.24 to 35.31 days. All settings retain a nonzero fitted 35.23-day term, but the preferred period is not stable across controls. files/summary.json gives each fit. files/season_audit.png compares the two main reductions.

## Conditional stability test

We test whether the loss after season removal is unusual for a coherent 35.23-day wave under three limited noise rules. We fit the full two-wave-plus-trend model. We divide its velocity residuals by sqrt(1-h), where h is the diagonal of the weighted fit projection. This reduces residual shrinkage from fit leverage. We multiply these residuals by shared random signs in 1-, 30-, or 90-day groups. Groups start at the first exposure. We add them to the full fitted model and refit all nine masks. Each rule uses 2000 draws, with seed 8690415 and a single sequential random stream.

The statistic is the smallest season-removal Delta divided by full-data Delta, at fixed 35.23 days. Its observed value is 0.3616. Lower values mean a larger relative loss in one removal. The lower-tail fractions, with a one-count correction, are 0.0640, 0.0310, and 0.0210 for 1-, 30-, and 90-day groups. Their simulation standard errors are about 0.0055, 0.0039, and 0.0032. These fractions depend on the group rule. They do not establish time variation. The fitted period and mean were selected from these data, and the residual signs need not satisfy this noise model. Only 13 groups remain for the 90-day rule. No family-wise physical significance claim is made. The result flags uneven seasonal support under conditional models.

## Physical interpretation and limits

A second circular orbit would give a coherent velocity wave. Its 35.23-day frequency differs from 36.059 days by a beat time of about 1532 days. The periods therefore cannot be treated as independent in this sparse 3012-day span. A changed outer-orbit model, stellar activity, and a shared instrumental effect can change the nearby peaks. This audit does not fit a full outer orbit or a stellar noise covariance. It does not measure rotation. The trend sensitivity prevents a unique physical explanation.

SERVAL and DRS use the same spectra. Their agreement on a fitted term cannot exclude shared artifacts. Linear activity slopes do not model changing spots or magnetic cycles. No new raw spectra or independent instrument velocities are fitted. The several-instrument result in Feng et al. concerns the published system; it does not confirm this 35.23-day residual. These results neither confirm nor refute that system. They show that the main peak is not confined to one season, while its preferred period depends on reduction and baseline. Independent spectra, a full orbit model, and a measured activity model are needed for a new physical claim.

## Reproduction and checks

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Exact versions are in files/summary.json. From the extracted publication directory, run:

```sh
python files/analyze.py /mnt/dell-data/shared_datasets/gj433-harps-rvbank-v02-283a3905/gj433.csv /tmp/gj433-audit
```

If the shared input is absent, retrieve it to a new external directory:

```sh
python files/retrieve.py /tmp/gj433-external
python files/analyze.py /tmp/gj433-external/gj433.csv /tmp/gj433-audit
```

The input hash must match. The scripts reject output inside the publication. No private scratch is needed. The retrieval script refuses to overwrite a file. A changed upstream source is a reproducibility limit unless a copy with the recorded hash is available. The analysis creates an aggregate summary and a static figure. Direct joint fits and projected fits agree in amplitude to 4.5e-16 m/s. A noiseless coherent model retains its amplitude after all deletions to 9e-16 m/s. These checks test the algebra, not the physical assumptions.

## Job record

Job: sci-1107-dell-astronomy-8d8690d41538. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. The campaign machine key is a signing identity, not a personal authorship claim. The exact SCI baseline license applies to original bundled materials. External terms and attribution are separate. This investigation stops after local signing and verification. No remote submission is requested or performed.
