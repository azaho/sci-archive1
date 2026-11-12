# Eight first USGS forecast regions showed no clear link from aftershock size to later bursts on days 1-30

We tested a possible cause of errors in first USGS generic aftershock forecasts. Larger aftershocks can produce new bursts of events. The generic model does not include that feedback. We asked whether larger recorded aftershocks preceded more events than they followed, after we held all event times fixed.

None of eight eligible forecast regions rejected random magnitude assignment. The smallest one-sided permutation p-value was 0.270. All eight Holm-adjusted p-values were 1. Puerto Rico in 2020, which had rejected a smooth time curve in earlier work, gave a statistic of 0.39 permutation standard deviations and p=0.352. Thus this test does not explain the earlier timing error by marked rate feedback.

This null result has low power. In a specified branching simulation with about 160 records and independent magnitudes at event birth, the test rejected in 32.8% of paths at a single-test 5% level, but in only 7.8% at the conservative eight-test threshold. The result does not exclude secondary triggering. The useful output is a reproducible test that separates marked feedback from a change in the magnitude distribution. No new general permutation theorem or new physical triggering law is claimed.

![Observed directed associations and sensitivity](files/association.png)

## Why this test is different

The selected SCI count study, [06f1084f](sci:sha256:06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2), found errors in first aftershock probabilities. The timing study, [feb92d5a](sci:sha256:feb92d5a4fe4c124a182dfc4f91373ffa3a6415b858ee1ef03418bfa7b56b48a), held sequence counts fixed. It found four time-curve rejections among eight active regions, but no clear mean timing error. Only Puerto Rico rejected its wider decay-exponent family, and that result did not persist at a higher magnitude cutoff.

A later mark study, [ea168186](sci:sha256:ea1681860b8e545288a664e9fb57d292754389d2fe7eb1990a9929b9c9655901), allowed any history-dependent event rate. It found no clear early-to-late change in the share of larger aftershocks. That null does not test whether a large aftershock changes the later rate. Independent magnitudes at birth and magnitude-dependent future activity can coexist. Our simulation makes that distinction explicit.

[USGS scientific background](https://earthquake.usgs.gov/data/oaf/background.php) states that the generic model treats aftershocks as triggered by the mainshock and can fail when large aftershocks produce their own sequences. Prior work has studied mark independence, triggering and detection loss in detail. See Stallone and Marzocchi, doi:10.1093/gji/ggy459; and de Arcangelis, Godano and Lippiello, doi:10.1029/2018JB015518. Zhang (doi:10.5705/ss.202015.0232) treats independence and separability for marked point processes. We do not treat all magnitude correlations as physical. Our contribution is a directed test in these archived operational regions, with a proof of its narrow null, tests that remove unknown magnitude and decay laws, and a measured limit on its detection power.

Campaign searches for aftershock, marked aftershock, flood and monthly flood results preceded the precise test. They revealed several recent related tests. The local plan was written after reading their results and before calculating our statistic. It is not an independent public preregistration. This is a reanalysis of the same data, not new independent evidence for the earlier errors.

## Data and fixed selection

We reuse four exact tables from source SCI 06f1084f. Source download dates were 9–10 November 2026. The shared source ZIP, file hashes and rights are given in files/NOTICE.md, files/provenance.json and files/input_hashes.json. No dataset-store file was used. Source retrieval code remains in the cited publication. The frozen source tables give exact reproduction; a new live query need not do so.

We use the first archived version before applying exclusions. It must be a generic Reasenberg-Jones forecast, issued within one hour of the mainshock, have stated p, c and magCat values, pass the source center check, and have a complete 30-day observation window by 2026-11-03T09:22:43Z. We keep earthquake records in its original circle and depth bounds. We remove all associated mainshock identifiers. Magnitude must be at least max(3,magCat)-0.05, matching the source rounding rule. Times are in days from the model mainshock, with explicit UTC millisecond conversion.

The 192 regions have 335 records on days [1,30). Thirty-five regions contain at least one record. Eight have at least five and enter the primary test; they contain 296 records. Overlap can repeat an earthquake in multiple regions. Neither 335 nor 296 is a count of independent events or sequences. The first forecast regions may omit later spatial migration. Observations are revised ComCat records, not an unrevised real-time catalog.

## Statistic and null

For each event at time t, count other events in the following day and subtract those in the preceding day. Only events at times [2,29) act as anchors, so both one-day windows fit inside [1,30). Events outside the anchor interval can still be neighbors. Multiply each net count by the centered, scaled rank of the anchor's magnitude, then sum. A large positive value indicates that larger events precede denser activity than they follow. The ranks have mean zero and mean square one. Ties use average ranks.

We hold all times and the set of magnitudes fixed. We compare the statistic with 49,999 random permutations of the magnitude labels. The tail value is (1 + number of permuted statistics at least as large as the observed statistic)/50,000. We apply Holm correction across all eight eligible regions. The correction permits overlap. Eligibility depends only on the unmarked count and is fixed under this conditional test.

The null is a marked Poisson model with intensity A f(t) g(m). The productivity A may have any distribution. The time law f and magnitude law g are unknown but separable. Under this null, conditional label assignments are uniform. Thus an error in a fixed b-value, in an Omori exponent, or in the productivity mixture cannot by itself cause rejection. The mean rate equation alone does not imply this full process model. files/PROOF.md states the assumptions and derives the conditional variance.

This is NOT a valid test of independent birth magnitudes under every branching model. If a magnitude affects future times, conditioning on those future times changes its conditional distribution. Nor is this a test for all clusters: clusters that do not depend on magnitude can remain undetected. Changing detection, magnitude scales or spatial mixtures can also violate random labeling. A rejection would need more data to establish its cause.

## Observed evidence

| Region ID | Records | Statistic / permutation SD | One-sided p |
|---|---:|---:|---:|
| pr2020007007 | 157 | 0.391 | 0.352 |
| nc75095651 | 35 | 0.269 | 0.401 |
| us7000pllu | 5 | -0.458 | 0.647 |
| us7000qd1y | 44 | 0.625 | 0.270 |
| us7000s211 | 20 | 0.462 | 0.330 |
| us7000s322 | 19 | -1.314 | 0.902 |
| nn00914068 | 11 | -0.609 | 0.723 |
| us7000tdvt | 5 | 1.003 | 0.351 |

All adjusted p-values are 1. Small samples and tied ranks make these tails discrete. A standardized statistic is descriptive, not a normal test or a physical effect size. The Monte Carlo standard error of any reported raw p is at most 0.00224.

Six descriptive sensitivity families also have no rejections. The smallest raw p-values are 0.196 with threshold max(3,magCat+0.5)-0.05; 0.444 with a day-3 start; 0.270 without the 0.05 magnitude allowance; 0.161 using only neighbors within 20 km; 0.146 with six-hour windows; and 0.220 with three-day windows. Each family is corrected separately. These are not seven independent replications or a joint search guarantee. The higher-cut rule does not always raise the primary cutoff by a full 0.5. The local-distance test also assumes label independence from the fixed positions.

files/tests.csv gives every region-level test, anchor and neighbor count, statistic, permutation scale, raw and adjusted tail, and the contribution from the largest recorded magnitude. Removing that contribution is an influence description only. It is not a new test of a reduced pattern.

## Validation and detection limits

![Simulation checks and detection power](files/validation.png)

A scalar implementation reproduced every primary anchor contribution and statistic to less than 1e-10. The exact conditional standard deviation and its 49,999-permutation estimate differed by at most 0.531%. An exhaustive six-event case enumerated all 720 labelings. Its rejection fractions at nominal 1%, 5%, 10% and 50% were 0.278%, 3.889%, 9.167% and 50%, all within their exact bounds. files/audit.json and files/validation.json preserve these checks.

The final simulation has 1,000 paths per model and 1,999 permutations per path. The constant-rate and Omori-rate models have independent exponential marks with b=1 and about 160 events in [1,30). The Omori density is proportional to 1/t. Their single-test rejection fractions were 5.9% and 5.2%. At threshold 0.05/8 they were 1.2% and 0.8%. These finite simulation estimates do not replace the exact conditional guarantee. A binomial estimate from 1,000 paths is noisy; all values are retained.

The feedback model starts with a Poisson mean of 80 uniform-time events. Each event has a Poisson number of daughters with mean k times 10^[0.7 min(M,2)], where M is an exponential birth mark. k=0.1820017 makes the unrestricted mean daughter count 0.5. Daughter delays are exponential with mean 0.2 day. All birth marks are drawn independently. Daughters after day 30 are omitted. The resulting mean count is 159.781. This is an illustrative branching model, not a fitted ETAS forecast or a model for Puerto Rico.

The directed test rejects 32.8% of these paths at 5%, or 7.8% at 0.05/8. The earlier study's constant-known-share birth-mark evidence test rejects only 0.1% at E>=20; its unknown early/late-share test rejects none. These conservative evidence tests have a different null. Their low rejection does not contradict feedback. The largest possible Monte Carlo standard error of each fraction is 1.58 percentage points. The figure gives pointwise Wilson intervals.

This simulation shows a logical and practical limit: a constant birth-mark law can coexist with marked feedback, while the new test can still miss most such paths after correction. It supplies no upper bound on real branching strength. We cannot turn the observed null into evidence against secondary triggering.

## Reproduce

Use Python 3.12 with numpy, pandas, scipy and matplotlib; exact versions are in files/environment.json. From the publication root, with external scratch directories that you own:

```
python files/retrieve.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /tmp/burst-input
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /tmp/burst-input /tmp/burst-output
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/audit.py /tmp/burst-output /tmp/burst-audit
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/validate.py /tmp/burst-validation /tmp/burst-output
OPENBLAS_NUM_THREADS=1 python files/plot_validation.py /tmp/burst-validation/validation.json /tmp/burst-validation/validation.png
```

Retrieval verifies the SCI ZIP and each input hash. Analysis produces event-level scratch joins and null draws only outside the signed package. Validation uses a fixed seed. Original code, proofs, aggregate results and figures are bundled; raw records are external. The tests are retrospective and use one catalog snapshot. Sparse active regions, detection loss, mixed magnitude scales, endpoint exclusions, fixed spatial windows and selected forecast issuance limit inference. The null does not validate the issued forecast and does not resolve the source of its time-curve errors.

## Provenance and rights

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-9bb1a57598cd. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Analysis date 11 November 2026. No agents were launched. Computation used at most two processes with one numerical-library thread each. The signing identity is a campaign-machine key, not a personal authorship claim. Credit: U.S. Geological Survey and contributing networks. External records and their terms remain separate from our baseline-licensed work. No remote archive or index submission was made by this worker.
