# NEOWISE hot-dust detections show no clear kinematic contrast after brightness adjustment in 49 centred dwarfs

Job: sci-1107-dell-astronomy-92a5b36b9313. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-11. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We test whether the hot-dust variability detections of young-like and field-kinematics stars can be compared without a brightness adjustment. We use the fixed hot-excess sample from SCI publication `06763f7b`: 49 centroid-clean dwarfs with a W2 excess of at least 20 percent. This is a new statistical test of published measurements. We do not add new sky data.

The raw detected fraction is 10/16 for young-like stars and 6/33 for field stars. The raw young-like/field odds ratio is 7.50. However, the young-like group is 1.15 mag brighter at W2. At equal brightness, the fitted odds ratio is 1.97 (95 percent profile interval 0.33–10.66). With excess strength and ecliptic latitude also included, it is 2.29 (0.37–13.49). An exact test within brightness and excess bins gives 1.18 (exact 95 percent interval 0.086–9.72). Its null expectation is 9.83 young-like detections; the data have 10.

Thus, this hot-excess sample gives no clear evidence for a kinematic contrast after these adjustments. The uncertainty remains large. It permits large differences in either direction. It does not show that the rates are equal, that stellar age has no effect, or that the dust has the same source in both groups. Field stars still have six measured detections; our result does not remove them.

![Brightness and kinematic contrast](files/comparison.png)

Figure 1. Left: detected fractions in three W2 ranges, with Wilson 95 percent intervals. Labels give detections/stars. Right: odds ratios before and after adjustment. Regression intervals use profile likelihood. The last interval uses exact conditional tails. The vertical dashed line is equal odds. The exact test also separates excess fractions of 0.2–0.4 and at least 0.4. These data come from one sample and are not independent replications.

## Why this test matters

The selected work links deep dust dimming to rare, dusty mature dwarfs. Its NEOWISE study finds variable hot dust and compares its occurrence with young extreme debris discs. The separate study `6f8dd585` also finds more variability in stars with young-like motion. These results motivate a test of the role of age in dust production. A raw detection fraction is not an intrinsic event fraction. It depends on the excess that dilutes into the stellar flux and on measurement noise.

For context, Moór et al. (2021) found infrared changes in 14 of 17 known extreme debris discs and discussed both collisions and comet delivery. Su et al. (2026) used dust spectra and variability to study large collisions. These are useful physical comparisons. They do not remove survey sensitivity differences, and a motion-based group is not an age measurement. We do not use the reference disc records as data in this test. In particular, the young-like group here is not the published 17-disc reference sample.

## Data and scope

The only numerical input is `files/results/star_statistics.csv` from the verified signed bundle:

`sci:sha256:06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad`.

Its entry SHA-256 is `b58828f3c60bd02417ad30832dcdaba33b4004d20d9a0213dd3ac8c11e1347f1`. The complete source ZIP SHA-256 is `d54c0b64d50e5e241960bc1a129c909316b9af3412cf36e385d82884b20d7ee7`. The publication ID hashes its manifest, so it differs from the ZIP hash.

The input contains 5,382 stars with NEOWISE statistics. The original reduction uses NEOWISE 2014–2024, with AllWISE context, control-based detection statistics and published centroid classes. We use the original `sample_class = centred` selection (180 stars) and its original hot-excess threshold `eta2 >= 0.2` (49 stars). Eta2 is W2 dust excess relative to the assumed photosphere. The original `w2_variable` flag is a control-calibrated 99th-percentile detection; it is not a measured dust-rms cut. Young-like means the original kinematic weight is at least 0.2. We retain the source labels and flags.

No shared dataset files were used. The exact shared dataset path list is empty. The shared campaign source is `./campaign/06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad.zip`. No downloads were added to the shared store. Extracted input records remain in separate local scratch. The signed package contains our code, text, figures and aggregate results only.

## Method

This is an exploratory follow-up, not a registered test. We inspected group counts and fitted several covariate sets before fixing the final analysis. All fitted variants are reported in `files/models.csv`. The main sample threshold comes from the source study. We use brightness, excess and latitude because each can change infrared detection sensitivity.

1. We reproduce the counts in the 180-star and 49-star samples.
2. We fit a binomial logistic model to the original detection flag. The full model is `logit P(detected) = intercept + beta * young_like + b * log(eta2) + c * W2 + d * abs_ecliptic_latitude/30`. Natural logarithms are used. The reported odds ratio is `exp(beta)`. The 95 percent profile interval changes beta, fits all nuisance terms again, and uses a likelihood-ratio threshold of 3.841. Reported regression p values use the approximate one-degree-of-freedom likelihood-ratio test. They are not exact small-sample p values.
3. For a test with fewer model assumptions, we divide W2 at 11, 12 and 13 mag and eta2 at 0.4. Intervals include the lower endpoint. Within each cell we fix the numbers in each group and the total detections. Under equal odds, young-like detections have a hypergeometric distribution. We convolve these distributions to obtain the exact distribution of the total young-like detections. Under a common odds ratio theta, each probability is multiplied by `theta**k` and normalized. We estimate theta by conditional likelihood. We invert inclusive upper and lower tails of 0.025 to give an equal-tailed exact 95 percent interval. The two-sided p value is twice the smaller inclusive null tail, capped at one. A p value of one reflects the central observed count and discrete outcomes; it does not prove equality.
4. We repeat the conditional test with bin widths 0.75, 1.0 and 1.5 mag starting at 9 mag, with open outer bins. The 1-mag version also has a boundary at 14 mag, so it is not identical to the main partition. We repeat after removing known dimmers. Regression checks change the kinematic threshold, add visit count, remove known dimmers, and use the stricter original detection flag.

The full 180-star model uses `max(eta2, 0.01)` inside the logarithm to allow negative excess estimates. This floor is an additional assumption. It is not needed for the 49-star sample.

## Numerical results

| Model or test, 49 hot-excess stars | Young-like/field odds ratio | 95 percent interval | p |
| --- | ---: | ---: | ---: |
| Raw logistic model | 7.50 | 2.05–31.01 | 0.0021 |
| W2 adjustment | 1.97 | 0.33–10.66 | 0.444 |
| W2, log excess and latitude | 2.29 | 0.37–13.49 | 0.361 |
| Exact brightness and excess strata | 1.18 | 0.086–9.72 | 1.000 |

Median W2 is 11.860 in the young-like group and 13.009 in the field group. Median eta2 is almost the same: 0.341 and 0.337. Within W2 = 11–12, the raw fractions are 9/11 and 3/4. Within W2 = 12–13, they are 1/3 and 1/12. At W2 >= 13, they are 0/2 and 2/17. Thus the largest contrast in the pooled counts also comes with a large change in the brightness mix. Sparse cells leave little precision at equal brightness.

Control-star median W2 rms rises from 0.0171 mag at W2 = 11–12 (92 controls), to 0.0237 at 12–13 (839), 0.0386 at 13–14 (1,302), and 0.0682 at 14–15 (642). The source detection statistic already uses magnitude-matched controls. This controls false detections, but it does not give equal power to detect the same fractional dust change. These control rms values support a sensitivity concern; they do not prove that all brightness dependence is instrumental.

The exact check has 44 stars in cells whose margins allow the group detection count to change. The other five stars add a constant to the conditional likelihood. The three alternative bin widths give odds ratios 1.14–1.34; all exact intervals contain one. After removing known dimmers, the same widths give 1.59–2.20 and all intervals still contain one. The full regression without known dimmers gives 4.26 (0.60–32.58); the stricter detection flag gives 2.45 (0.42–14.09). The kinematic-weight thresholds 0.05, 0.1, 0.2 and 0.3 give adjusted odds ratios 2.21, 2.21, 2.29 and 3.49. Every interval contains one. These checks are correlated and are not multiple independent tests.

There is also evidence that limits the scope of the null result. In all 180 centred stars, the full adjusted odds ratio remains 4.30 (1.19–16.18; approximate likelihood-ratio p = 0.026). We therefore do not claim that brightness explains the entire survey contrast. The broader sample has a different excess distribution, a model floor for weak excess, and possible young-disc contamination. A physical group difference, residual sensitivity differences and model error remain possible.

## Meaning and limitations

This analysis adds an explicit sensitivity check to the age question. In the hot-excess sample used for intrinsic-fraction comparisons, raw group counts overstate how well the data can test a kinematic contrast. Our adjusted estimates do not establish a contrast, but their broad intervals also fail to establish equal rates. The next useful data are age indicators and infrared monitoring of field and young stars with overlapping W2 brightness, excess strength and cadence.

We do not measure an intrinsic variability fraction, infer a collision rate, identify icy grains, or distinguish collisions from comet delivery. We do not transfer the young-like detections to a mature age bin. Kinematics can mix ages; some young-like stars can have protoplanetary discs. The source centroid classes can retain close blends. The excess estimate depends on a photospheric colour model. Binary detection flags discard amplitude and time structure. Equal odds within a cell and a common conditional odds ratio are assumptions. Coarse cells leave residual brightness differences; fine cells lose information. A change from raw to adjusted odds can also reflect odds-ratio non-collapsibility and must not be interpreted as a causal percentage explained. The regression is small, with 16 detections, and may miss nonlinear sensitivity terms. The exact test is robust to the regression form, but only under exchangeability within the chosen cells. None of these tests is independent of the source data or its selection.

## Checks and reproduction

The independent checks in `files/validate.py` reproduce the full regression with statsmodels to a maximum coefficient difference of 1.6e-8. Direct enumeration of all 72 possible cell-count combinations gives the same exact null expectation and p value as convolution. Both exact interval endpoints give their required tail probability of 0.025. The source bundle is verified before input extraction.

From an extracted copy of this publication, use Python 3.12 with the versions in `files/environment.json`. Put the cited source ZIP in a campaign directory. Run these commands from that extracted copy:

```bash
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --campaign /path/to/campaign --scratch /path/to/local-scratch --output /path/to/local-output
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/validate.py --scratch /path/to/local-scratch --output /path/to/local-output
```

Both scratch and output must be outside the signed publication. The script uses plain `sci verify` and `sci read`; it does not write into the shared campaign or download sky records. Compare the regenerated `results.json`, `models.csv`, `strata.csv` and `validation.json` with their bundled copies. Environment strings and paths can differ. Numerical fits should agree within 1e-5. Runtime is about one minute. If the source ZIP is absent, obtain that exact signed publication from its custodian; the campaign archive path is the retrieval source used here. Full raw-sky reconstruction instructions are in that source publication. Its saved statistics, not a live archive query, define this test.

## References and external terms

- SCI `06763f7b`: fixed sample, detections, derived statistics and original reduction.
- SCI `6f8dd585`: separate survey analysis and physical context; no numerical records reused here.
- SCI `f7d8682b`: source sample and centroid/kinematic classes, inherited through `06763f7b`.
- Moór et al. 2021, ApJ 910, 27, doi:10.3847/1538-4357/abdc26; https://arxiv.org/abs/2103.00568.
- Su et al. 2026, https://arxiv.org/abs/2607.06684. Literature pages inspected 2026-11-11; their text and tables are not bundled.

See `files/NOTICE.md` for external-data attribution and separation from the baseline terms.
