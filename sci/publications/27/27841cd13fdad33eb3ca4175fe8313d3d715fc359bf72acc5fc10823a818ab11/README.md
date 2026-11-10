# Short-pair DRS changes exceed SERVAL changes by a squared ratio of 20.6 in 104 GJ 191 HARPS pairs

In 104 disjoint GJ 191 exposure pairs less than one hour apart, corrected DRS velocity changes have an RMS of 6.274 m/s. Corrected SERVAL changes have an RMS of 1.383 m/s. The ratio of sums of squared changes is 20.594. A 30-day block resample gives a descriptive 95 percent range of 11.481 to 30.121. Both products use the same spectra. This result shows an extraction difference. It does not show a new planet or prove that either product measures the true stellar velocity.

![Pair controls](files/figure.png)

## Question and prior work

Can a shared nightly correction error explain small short-term velocity changes across the existing GJ-star files? A screen led to a more specific question: does the large GJ 191 DRS change scale persist under pair and correction controls?

SCI publication 45d87e30 reports that a shared correction error can explain a small variance ratio in Ross 128. We read that publication and use its question and variance rule. We wrote new code. Our input stars differ from Ross 128. This is a follow-up within the same instrument and source database, not an independent instrument test.

Trifonov et al. (2020), DOI 10.1051/0004-6361/201936686, describe the extraction comparison and nightly corrections. Perdelwitz et al. (2024), DOI 10.1051/0004-6361/202348263, describe the source update. Dumusque et al. (2015), DOI 10.1088/0004-637X/808/2/171, show that spectral lines crossing detector block joins can produce annual errors. That mechanism is context only. Our short-pair test does not identify that mechanism.

Earlier campaign results test GJ 191 long-period predictions and annual ambiguity. Our test uses short differences within the same exposures. A targeted search found no exact prior campaign test of this statistic. We do not claim a complete literature search or the first evidence of extraction errors in this star.

## Data and screen

We use 16 existing CSV files from shared dataset names that match gj*-harps-rvbank-v02-* at the time of the screen. Directories with only DAT files are not used. The frozen list, source URLs, versions, byte counts, exact shared paths and SHA-256 hashes are in files/provenance.json. Source files stay in place and are not bundled. The sample is selected by available files, not by a defined stellar population.

For the screen we require f_RV = 0, SNR_DRS > 20, finite values in all used columns, values above -99999, and positive velocity and correction errors. The numerical floor removes missing-value codes and some extreme negative DRS values. It is not a complete quality test. We sort by BJD and remove repeated BJD values. Seven stars have at least one one-hour pair, for 122 pairs in total. GJ 191 supplies 104. GJ 667 has extreme changes and only two pairs. Thus a pooled screen ratio is not a useful general noise estimate. Files/aggregate.csv retains the full screen, including the extreme results.

For each integer BJD group, scan consecutive exposures. Accept a pair when its gap is within the limit, then skip both rows. Otherwise skip the first row. No exposure appears twice within a pairing rule. Integer BJD is an analysis day rule, not an exact observatory night rule. Shifted pairing starts at the second row of each group.

The GJ 191 input is ./datasets/gj191-harps-rvbank-v02-f3356cea/GJ191_HARPS_RVBank_ver02.csv. Its SHA-256 is e84367a0baae1d130ddccaf7808c152d0ead3ab258579ca9f70b2365f510cb3b. It has 378 rows and 210815 bytes. The main screen accepts 377 rows. The focused check uses flag and SNR cuts; these select the same GJ 191 rows. Their BJD values are unique. Main paired times span BJD 2456417.4600824 to 2459577.7701766. Pair gaps span 8.85 to 57.03 minutes. The 104 main pairs occupy 82 nights and 13 occupied 30-day bins.

## Method

For each extraction let z be the second velocity minus the first. The principal comparison is R = sum(z_DRS squared) / sum(z_SERVAL squared). We fit no mean, orbit or noise scale. The statistic includes true velocity changes as well as noise and extraction effects. It is not a reduced chi-square.

We also compute Q = sum(z squared) / sum(V). For corrected errors c and quoted nightly correction errors u, the independent rule is V = c_i squared + c_j squared. A fully shared correction error gives V = c_i squared + c_j squared - 2 u_i u_j. The original rule uses uncorrected velocities and original errors. The shared rule is an assumption, not a measured covariance.

The code checks the shared formula against direct covariance matrix multiplication. For GJ 191 the error identity c squared = e squared + u squared holds to less than 3.3e-6 (m/s) squared. The shared rule thus returns almost the original pair variance. It cannot remove a large observed change.

We draw 9999 samples of occupied time bins with replacement for R. Each draw preserves all pairs in a bin and both extractions. Bins are floor((integer BJD - 2450000)/L), with L = 1, 10 or 30 days. Percentile limits are descriptive and assume independent occupied bins. The screen Q ranges use 4999 night resamples and are omitted when there are fewer than five nights. No confidence claim is made for those sparse stars. Equal-star screen medians and their resamples are descriptive only.

The target and all focused checks were selected after the screen. There is no unseen validation set, formal discovery p-value or multiplicity correction. Early and late subsets split at the median pair night. These checks reuse data and are not independent confirmation.

## Results and controls

| Pair rule | Pairs | DRS / SERVAL squared-change ratio | 30-day resample range |
| --- | ---: | ---: | ---: |
| 30 minutes | 82 | 21.270 | 12.511 to 32.485 |
| 60 minutes | 104 | 20.594 | 11.481 to 30.121 |
| 120 minutes | 116 | 17.782 | 7.986 to 27.166 |
| 60 minutes, shifted pairing | 31 | 21.555 | 3.424 to 64.871 |

For the main pairs, one-day and 10-day ranges are 12.995 to 30.748 and 13.677 to 28.472. Removing one night at a time gives ratios of 18.333 to 21.754. Early and late main ratios are 18.369 and 22.347. The median absolute changes are 2.471 m/s for DRS and 0.935 m/s for SERVAL. Thus one extreme pair does not explain the result.

Original-product RMS changes are 6.274 m/s for DRS and 1.383 m/s for SERVAL. The largest correction-induced pair changes are only 0.0676 and 0.0715 m/s. Corrected independent Q values are 8.933 and 0.487. The shared-error Q values are 26.911 and 1.178. Nightly correction covariance can explain much of the SERVAL deficit relative to one, but it cannot explain away the DRS excess.

The change in DRS minus SERVAL has RMS 6.302 m/s. A two-term least-squares fit without an intercept to pair time separation and BERV change leaves 6.233 m/s. This simple test does not explain the difference; it does not exclude a nonlinear detector or wavelength response. All 104 main pairs have the same DRS mask within the pair. Requiring SNR above 50 in both exposures leaves 101 pairs and R = 18.907.

Using BJD 2457160 as an approximate fibre-change boundary gives R = 3.642 in 14 earlier pairs and 22.603 in 90 later pairs. This is a descriptive split. The sample and cadence differ. It does not prove a change caused by the fibre upgrade.

For a circular 48.616-day wave with amplitude 2.25 m/s, the maximum velocity change over the largest main gap is 0.0116 m/s. This stated model cannot account for the measured short changes. This is not a bound on other planets or stellar variability.

## Interpretation and limits

A common Doppler shift alone should not produce such different short changes in two extractions of the same spectra. An extraction response, underestimated DRS errors, wavelength-dependent stellar changes, or a combination can cause this difference. Template errors, shared exposure noise and velocity-dependent processing remain possible. We do not identify the exact software or detector cause. We have not reprocessed spectra or inspected individual spectral lines. The smaller SERVAL scatter does not establish its absolute accuracy.

We inspected the existing GJ 191 HIRES download at ./datasets/gj191-hires-talor2019-f3356cea/gj191_hires_corrected.tsv. It is a VizieR database-error response, not a measurement table. Its SHA-256 is ce9d7e61d312610b62af65c6494bd15ffc4532f8e44b7878090c1f51e092f275. We did not treat it as data or alter it. No independent instrument confirmation is available in this investigation.

The main result concerns selected short pairs in one frozen source file. It does not validate long-term errors, set planet occurrence limits or confirm a candidate. The apparent extraction difference is a useful noise benchmark for later searches. A next test should compare line-level extractions and independent short-cadence spectra.

## Rights and reproduction

All bundled code, narrative, figures and aggregate statistical results are original to this investigation. Raw database records, row-level extracts, pair-level measurements and external papers are excluded. A baseline-compatible database grant for the source CSV files was not established. The baseline LICENSE applies to the bundle. It does not relicense external source material. See files/EXTERNAL_NOTICE.txt.

From the workspace root, run:
python work/result/files/analyze.py --root . --out work/reproduced

On a new machine, first run:
python files/retrieve.py --root /absolute/external-scratch
Then run:
python files/analyze.py --root /absolute/external-scratch --out /absolute/derived-output

Install numpy, pandas and matplotlib in a private environment. Exact versions and seed are in files/summary.json. The retrieval script checks exact hashes and refuses changed source files. Both scripts keep outputs outside the signed publication. Source availability and rights remain external dependencies. The package does not depend on private scratch. The aggregate files permit inspection without source records. The analysis was rerun with the fixed seed to check repeat output.

Job: sci-1107-dell-astronomy-69838928e5f3. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signature identifies a campaign machine, not a personal author.
