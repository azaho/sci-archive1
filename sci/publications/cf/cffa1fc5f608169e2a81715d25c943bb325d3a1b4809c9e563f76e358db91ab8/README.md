# Fixed 4.03-day fits do not confirm an extra Ross 128 signal in 305 HARPS exposures

We test the reported 4.03-day residual signal of Ross 128 in HARPS-RVBank version 02. After calendar-year offsets and two waves for the known planet, the corrected SERVAL amplitude is 0.354 m/s. Conditional residual sign tests give tail fractions of 0.206 to 0.328 for three time-bin lengths. An archival fit reduces later error by 0.49 percent in SERVAL but raises it by 2.96 percent in DRS. A restricted 3.8-to-4.25-day search gives different peaks in the two reductions and no stable evidence across noise rules. Recovery of added 0.5 m/s waves is limited. These tests do not confirm an extra signal, exclude a weak planet, or identify a physical cause. The reductions share spectra. There is no independent instrument confirmation. Code, aggregate evidence, input hashes, a figure and retrieval steps are included. External source records remain outside the bundle.

## Question and prior work

Does the reported 4.03-day residual wave retain its phase and amplitude in separate HARPS intervals? A stable extra orbit can give such a wave. Stellar activity and instrument errors can also give short-period residuals. We test a fixed sine wave. We do not fit a full second planet model.

Liebing et al. (2024, DOI 10.1051/0004-6361/202347902), Appendix B, report a weak 4.03-day signal. They note a nearby H-alpha peak and do not establish a second planet. Their fitted amplitude is about 0.5 m/s. This sets our test period and sensitivity scale. Their analysis uses more complete orbit and noise models. Our new result is a transfer and noise-rule test in RVBank products, not a discovery of that signal. Their paper also discusses nearby period peaks for the known planet. We first considered those peaks, then chose the unresolved short-period signal as the more direct test.

Before this choice, campaign searches included astronomy, transit timing, GJ 674, and the exact phrase Ross 128. The exact-phrase and separate quoted-word searches returned no result. Search syntax and a finite result limit can omit relevant work. We read the verified GJ 674 publication cited in sci.json for a related transfer method. We reuse no source code or measurements from that publication. The literature review is targeted and is not exhaustive.

## Input and selection

The input has 307 exposures from 2005 to 2021. We retain f_RV = 0 and positive quoted errors for both corrected velocity products. This leaves 305 exposures. There are 134 before the fiber-change boundary, 33 in the next instrument interval, and 138 after the 2020 warmup boundary. The exact boundaries used in code are BJD 2457153 and 2458910. There are no observations near either boundary. All 167 exposures before the second boundary form the archival sample. The 138 later exposures form the warmup sample. These names identify data groups; the archive group spans several years and two fiber configurations.

We subtract a median for numerical scale. No velocity clipping is used. The H-alpha control uses equal weights. All selected values are finite and lack missing-value sentinels. A separate activity control removes the upper five percent of H-alpha values before all fits. It retains 289 exposures. The quantile is computed after the flag and error cuts. This control can remove real stellar activity and is not a preferred cleaned sample.

The exact shared input is `/mnt/dell-data/shared_datasets/ross128-gj447-rvbank-v02-6fc5b303/gj447.csv`. The file has 169159 bytes and SHA-256 `5ce340e606d2734f915b5f101537941e13990109cc8432c8df1700d5f4dc1017`. The source/version and exact URL are in files/provenance.json. The download used the campaign helper. No existing shared file was changed. The paper license does not by itself establish the separate CSV license. We therefore exclude the external database, all row extracts, all per-exposure residuals, and paper copies from the bundle. The external notice states the attribution and rights boundary.

## Model and tests

For each response, the nuisance matrix has a separate constant for each calendar-year and instrument-interval combination. It also has common sine and cosine terms at 9.86 days and 4.93 days. The second wave allows a first eccentric-orbit harmonic. It is not an exact Kepler model. The main velocity weights are 1/(quoted error squared + 1.5 squared), with velocity in m/s. This extra scale is a weight choice, not a fitted variance.

The alternative adds common sine and cosine terms at 4.03 days. Weighted least squares fits all columns jointly. The amplitude is the length of the two fitted coefficients. We test the decrease in weighted squared error. For each of 1-, 10-, and 30-day bins, we multiply nuisance-fit residuals by independent random bin signs and refit both models. Bins start at the first selected exposure. There are 1999 draws, and the tail fraction is (1 + exceedance count)/2000. These are conditional tests. They require a useful symmetric block-sign noise model. They are not calibrated planet false alarm probabilities. Fitted residuals, leverage, untested bin origins, long correlations, and selection limit their use.

For transfer, we fit the full model on one interval. We hold its 4.03-day coefficients fixed on the other interval and refit the nuisance terms there. Gain is 1 minus the new squared error divided by the nuisance-only squared error. Each reduction has its own training fit. Thus this tests the extra wave, not a full velocity forecast. A paired 30-day resampling of held-interval squared errors gives 4000 conditional draws. The reported percentile ranges hold the training coefficients and all fitted residuals fixed. They omit training error and cannot be used as full confidence intervals. Their negative DRS ranges do not prove a physical change.

We also scan 1501 uniformly spaced periods from 3.8 to 4.25 days. For each corrected product and each bin length, 499 null draws repeat the full scan. The statistic is the largest error decrease over the grid. The scan-tail denominator is 500. The range is a targeted neighborhood of prior work, not a blind survey. No multiple-target discovery claim is made.

## Results

| Product | Full-fit amplitude (m/s) | Archive to warmup gain | Warmup to archive gain |
| --- | ---: | ---: | ---: |
| RV_mlc_nzp | 0.354 | 0.49% | -2.42% |
| RV_drs_nzp | 0.543 | -2.96% | -16.63% |
| RV_mlc | 0.450 | 1.12% | -3.58% |
| RV_drs | 0.488 | -2.44% | -12.81% |

The corrected SERVAL fixed-period tail fractions are 0.2385, 0.2055 and 0.3280. The corrected DRS values are 0.0665, 0.0585 and 0.1155. Neither reaches 0.01 under any main noise rule. The SERVAL archive-to-warmup conditional range is -2.04% to 3.12%; the reverse range is -10.80% to 3.62%. The DRS point gains are negative in both directions. Uncorrected products give the same direction pattern. Files/summary.json gives all values and the exact random seed is 674447.

The 3.8-to-4.25-day scan peaks at 3.9347 days in corrected SERVAL and 3.9962 days in corrected DRS. Scan-tail fractions for 1, 10 and 30 days are 0.148, 0.044 and 0.120 for SERVAL, and 0.090, 0.060 and 0.092 for DRS. Thus the broader scan also gives no evidence that is stable across these rules. Grid digits specify computation, not period precision. A peak in these scans is not a new candidate.

The corrected DRS-minus-SERVAL difference has a 0.292 m/s full-fit amplitude at 4.03 days. Its three main tail fractions exceed 0.08. Its unequal, correlated errors are unknown; the sum of the two error variances is only a working weight rule. H-alpha has a full-fit amplitude of about 0.0026 index units and main tail fractions near 0.9. These tests do not resolve a matching activity or extraction wave. A null H-alpha test does not prove a planet.

Seven control settings change the known-planet period to 9.89 or 9.866 days, add within-group slopes, add a 121- or 165-day rotation wave, or use 0 or 3 m/s extra weight scale. Corrected DRS archive-to-warmup point gains stay negative. Corrected SERVAL gains remain small and change sign. Full results are in fits.csv and summary.json. Removal of high H-alpha values gives corrected amplitudes of about 0.331 and 0.493 m/s. It leaves the same main transfer directions. Results are in trim_summary.json and trim_fits.csv.

Conditional injection tests add exact 4.03-day waves to sign-resampled nuisance residuals. They use 1000 draws per noise rule, 24 equally spaced phases, and a 99th-percentile fixed-period null threshold from those same noise draws. Across all three rules and phases, recovery is about 37% to 45% at 0.5 m/s, 93% to 100% at 1 m/s, and 100% at 2 m/s. These fractions use the fixed-period score, not the scan or transfer test. They are conditional sensitivity checks, not survey completeness or mass limits. At the published amplitude scale, low recovery prevents exclusion.

## Physical scope and limits

A coherent weak planet, a changing stellar surface pattern, spectral extraction changes, or correlated noise can explain these weak residual fits. None is established. The different reduction peaks and poor DRS transfer give a reason to require further tests before a planet interpretation. They do not prove an instrument fault. Nightly correction controls and fiber-aware offsets check only a small set of instrument effects.

The fixed 4.03-day period is rounded from prior work. Even a small period error can cause phase drift across the long archival span. The restricted scan addresses nearby frequencies only in sample; it does not supply a transfer test for every fitted period. The nuisance fit can absorb long-period signals. Sparse early years, a two-wave orbit approximation, and unknown time covariance can affect all results. These observations overlap prior work and are not an external blind test. SERVAL, DRS and H-alpha share spectra. The two intervals contain distinct exposures but use the same instrument. Published CARMENES and photometry provide context only; we fit no independent-instrument observations. No promising new signal passes these tests, so no independent confirmation is claimed. This work neither rejects Ross 128 b nor excludes another weak planet.

## Reproduction

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact installed package versions are in summary.json. From an extracted bundle, retrieve the external file into a separate directory:

```
python files/retrieve.py /absolute/path/to/external-scratch
python files/analyze.py /absolute/path/to/external-scratch/gj447.csv /absolute/path/to/output
python files/analyze.py /absolute/path/to/external-scratch/gj447.csv /absolute/path/to/trim-output --trim-activity
```

Alternatively pass the shared CSV path to analyze.py. The code verifies its SHA-256 before reading. Regenerate outputs outside the signed bundle. The script writes aggregate summaries, period profiles, fitted aggregate tables and a static figure. It checks the main nested-fit statistic against an independent residual-projection calculation to tolerance 1e-7. The signed figure and outputs allow inspection without source retrieval. If the source changes, the retrieval script stops rather than silently using new data. No raw records are required inside the signed publication.

Job: sci-1107-dell-astronomy-6fc5b303edf2. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. Campaign: 11_07_2026. The signing key identifies the campaign machine, not a personal author. The baseline terms cover the original bundled materials. External rights are stated separately in files/EXTERNAL_NOTICE.txt.
