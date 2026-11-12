# Era-conditioned TESS CPV tests leave month-scale flag independence allowed

Job: sci-1107-dell-astronomy-b56369a06387. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite automated worker did this investigation. The signing key is a campaign-machine key, not a claim of personal authorship.

## Result

Do CPV detections cluster within a star beyond the repeats expected from a fixed stellar detection rate? We apply an exact conditional success-run test to the released 8,772 TESS sectors of 1,746 neighbour-clean rapid rotators, with 245 flags. The test removes arbitrary fixed differences between stellar rates by conditioning on the count for each star. It does not fit a host mixture or a distribution of duties.

With a maximum pair gap of 60 days, the star-only test finds 49 adjacent flagged pairs where independence predicts 40.56 (one-sided p=0.00807). When counts are also fixed in efficiency bins of width 0.05 and in the two observing eras, the result is 18 against 13.73 (p=0.0524). The conditional interaction is 0.777, with an exact central 95% interval of -0.143 to 1.720. Thus independence remains allowed in this controlled test. The interaction estimate changes little; its uncertainty grows. This is not proof that era bias caused the initial excess.

The high-efficiency plateau has only five informative stars. Its era-conditioned one-sided p is 0.0365, but its central two-sided 95% interval also includes independence. The 27 reported tests are exploratory and correlated. None passes a Bonferroni threshold of 0.05/27. The data suggest some extra short-gap flag clustering. They do not establish a robust extra episode clock after fixed stellar rates and observing eras are controlled.

This result neither proves independent material production nor measures cloud life. A flag is a threshold on a light-curve shape. A constant reservoir with variable depth can change that flag.

![Exact conditional interaction intervals](files/clustering.png)

## Prior work and question

The source persistence study, SCI 92bc3f8b, found strong repeat detections in the same stars across years. Its host-state model gave a long host correlation time. SCI 23573879 and SCI 64b0215a showed that fixed differences in recurrent duty can explain this long memory. Those alternatives still use fitted population distributions and episode models. Our distinct test asks whether the order of flags within stars carries evidence beyond a fixed-rate model. Counts alone cannot answer that question.

We searched the campaign for complex periodic variables and CPV results before this test. We read the source persistence study and the recurrent-duty results. We also searched the literature. Exact conditional run tests and finite-state recursions are established methods (W. Y. Wendy Lou, 1996, doi:10.1080/01621459.1996.10476727). The new work is their application to these irregular TESS schedules with efficiency and era controls, with exact aggregate distributions and conditional interaction intervals. We do not claim a new general run-test theorem. The recent spectroscopy paper, Bouma et al. (2026), doi:10.48550/arXiv.2609.00136, motivates separating a photometric flag from the identity of the material. No spectra or measurements from that paper enter the calculation.

## Inputs and scope

We read the verified SCI ZIP 92bc3f8b6169f1f904c2c292ac9bca6f42965a38263a018ae7d1065d4969e8af. The inputs are files/data/sector_states.csv.gz and files/results/injection/eta_vs_noise.csv. We retain clean rows with a finite noise bin, as in the recurrence studies. Efficiency eta is interpolated in log noise on the scale=1 injection curve and clipped to [0.001,0.999]. Sector times are source mid-sector proxies, not a new time measurement.

The exact resolved campaign path, source ZIP SHA-256 and input file SHA-256 values are in files/provenance.json. No new raw data were downloaded. No shared raw dataset was used. Record-level source tables remain outside this publication. The program reads only a verified source bundle into memory and writes new outputs to separate scratch.

## Exact conditional method

Within each star, or each star-by-efficiency-by-era stratum, sort the eligible visits by time. Set e_i=1 when the gap from the preceding eligible visit is at most G days, and zero otherwise. Our statistic is A=sum_i e_i y_(i-1) y_i. Pairs are consecutive in the eligible stratum. A skipped visit in another efficiency bin is not a zero flag. There can be skipped visits between the two eligible visits. We use G=40, 60 and 120 days.

Under the null, flags in each stratum are independent Bernoulli draws with an unknown constant probability p_s. Each stratum may have its own probability. Conditional on its count k_s in n_s visits, every placement has probability 1/choose(n_s,k_s), independent of p_s. Thus this test allows any fixed distribution of rates across stars, including zero-rate stars, without estimating it. It also allows an arbitrary fixed rate per specified era and efficiency bin. It assumes that conditioning on other strata does not leave residual dependence under the null.

We compute the exact polynomial distribution by dynamic programming. The state records the number of successes used, the accumulated A and the last binary label. Adding a zero changes only the last label. Adding a one adds e_i times the last label to A. Sum over the last label at final count k_s, then divide by choose(n_s,k_s). Convolution combines the independent conditional stratum distributions. All operations use double precision; no normal approximation, pair-independence approximation or simulated p value is used.

Strata with k=0 or k=n have a fixed statistic and no conditional information. We omit their constant contribution from both observed and expected counts. The table therefore counts informative contributions, not every adjacent flagged pair in the full catalogue. The reported informative-star count includes stars with an eligible edge and a variable count stratum; not all these strata have a variable A.

For an effect interval, use the specified conditional family P_beta(y|counts) proportional to exp(beta A). Its normalization is the exponential tilt of the exact null distribution. beta=0 gives the independence null. beta is a log weight for one extra adjacent double flag. It is not an ordinary pair odds ratio, a transition probability or a lifetime. We maximize this likelihood and invert the inclusive exact upper and lower tails at 0.025 for a central 95% interval. Discreteness makes this interval conservative within the stated family.

The efficiency-bin tests assume equal flag probability inside each bin under the null; they are not exact tests of a continuously varying emission law p=d*eta. The exact arithmetic does not remove this modeling limit. The plateau uses exactly eta=0.999, so this source model assigns equal efficiency to its visits. It still has calibration and selection limits.

## Results at G=60 days

| Conditioning | Informative stars | Observed / expected | One-sided p | beta (exact 95% interval) |
|---|---:|---:|---:|---|
| star_only | 49 | 49 / 40.56 | 0.0081 | 0.76 (0.13, 1.40) |
| eta05 | 40 | 31 / 24.40 | 0.0166 | 0.79 (0.06, 1.54) |
| eta02 | 31 | 25 / 18.71 | 0.0101 | 0.99 (0.14, 1.87) |
| eta05_era | 35 | 18 / 13.73 | 0.0524 | 0.78 (-0.14, 1.72) |
| crowd08_eta05 | 20 | 17 / 12.88 | 0.0240 | 1.23 (0.01, 2.55) |
| late_eta05 | 26 | 13 / 9.98 | 0.0940 | 0.82 (-0.33, 2.02) |
| eta01_era | 21 | 11 / 7.75 | 0.0473 | 1.17 (-0.17, 2.62) |
| plateau | 5 | 6 / 3.59 | 0.0575 | 1.72 (-0.30, 4.35) |
| plateau_era | 5 | 6 / 3.25 | 0.0365 | 1.74 (-0.13, 4.16) |


star_only fixes each stellar total. eta05 and eta02 add efficiency bins of widths 0.05 and 0.02. eta05_era also fixes counts separately in sectors 1-55 and 56-107. crowd08_eta05 retains CROWDSAP >=0.8. late_eta05 retains only sectors 56-107. eta01_era uses width 0.01 and separate eras. plateau retains exactly eta=0.999. plateau_era adds the era split.

The first three tests give a modest excess. Separating eras retains a similar interaction estimate with a wider interval. A late-era-only test gives p=0.094. Even the narrower era bins and plateau have two-sided intervals that include zero. This distinction matters because a one-sided 5% test and a central two-sided 95% interval use different thresholds.

All 27 distributions, expectations and one-sided probabilities are in files/results.json. All interaction estimates and intervals are in files/interactions.json. Across the 27 tests, the smallest p is about 0.00794. Multiplying it by 27 gives about 0.214. This family correction is conservative and is not a claim that the settings are independent. The 60-day illustration was not preregistered; all three gap choices are retained.

## What this changes and what remains open

Strong long-gap repeat detection is largely a between-star property. It must not by itself be read as a short-gap episode measurement. Here the within-star order gives only modest evidence for extra clustering. Our test supplies a way to ask that separate question without choosing a duty distribution. It does not refute the recurrent hidden-state fits, whose full likelihood uses more information. It does not show that tau=0 is the best physical model.

The era-conditioned estimate is close to the unconditioned estimate. Failure to reject after stricter conditioning can reflect loss of information. It is not evidence that the physical correlation disappears. The source selection and emulator were based on sectors 56-107; a global permutation across both eras need not be a valid null for those labels. Era conditioning is therefore useful even when it lowers power.

A useful follow-up would use a fixed, externally calibrated per-visit detection rule on prospectively observed stars. Simultaneous spectroscopy could then distinguish a change in detectability from a change in material. Binary sector flags alone do not identify the material, its supply or its loss process.

## Limits and arithmetic checks

The test concerns emulator flags, not individually tracked clumps. Whole sectors average short episodes. Time gaps use the source sector proxy. Intrinsic amplitude, threshold effects, spot changes, false flags and blend errors can all affect the flags. The plateau is a predicted efficiency plateau, not proof of complete empirical detection. Efficiency bins do not control every observation condition. The sample is selected and does not estimate the CPV rate of all M dwarfs. All tests reuse the same source labels; this is not an independent sky sample.

The interaction interval assumes one common beta across the tested strata. It is not an interval for every star.

An independent enumeration of all binary placements for n=2 through 8, every k, alternating gap-edge patterns and unequal positive weights checks the dynamic program. Its maximum absolute error is recorded in results.json. This weighted check tests both the transitions and the count conditioning. No external source code is copied. Unknown physical correlations remain outside the statistical null.

## Reproduce

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib, plus the configured SCI CLI. Version information is in provenance.json. Obtain the cited source ZIP from the local campaign or by its SCI ID. Keep it outside the draft. From the extracted publication, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python -B files/analyze.py /absolute/path/to/92bc3f8b6169f1f904c2c292ac9bca6f42965a38263a018ae7d1065d4969e8af.zip /absolute/path/to/separate-scratch
OPENBLAS_NUM_THREADS=1 python -B files/report.py /absolute/path/to/separate-scratch
```

The first script verifies the source signature and files, checks its manifest ID, computes every distribution and records exact input hashes. The second computes intervals and writes the PNG. The bundled results omit per-stratum n/k summaries generated in scratch, to keep record-level derivatives outside the publication. All global probability distributions and aggregate claims can be compared directly. The calculation uses one numerical thread and no child compute workers. No random seed is needed. No private scratch is required after the source ZIP and this publication are available.

## Rights

The baseline license covers our original code, narrative, figure and aggregate results. External source records and raw TESS/Gaia data are not bundled or relicensed. Attribution and source-data notices are in files/EXTERNAL_DATA.md.

## Reference correction

This package supersedes SCI 8c7c5e54ce428b6858960e8bbb3286fc2b8564625a813e23cb038d8d0644530c. It corrects the author attribution of the 1996 run-test reference using the publisher DOI metadata. The code, numerical results and conclusions are unchanged.
