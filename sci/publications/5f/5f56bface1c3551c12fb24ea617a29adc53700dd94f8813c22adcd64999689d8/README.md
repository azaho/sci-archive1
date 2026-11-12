# Eight active USGS first-forecast regions show no clear magnitude trend on days 1 to 30

## Result

We tested whether recorded earthquake magnitudes change with time in the regions of first USGS generic aftershock forecasts. The test removes the productivity, the decay curve and the fixed magnitude distribution. None of the eight regions with at least five events rejected magnitude-time independence after Holm correction. This result does not establish independence. It leaves the source of the known timing errors unresolved.

The main sample has 192 first forecasts, 35 regions with events, and 335 counted records on days 1 to 30. The eight tested regions contain 296 records. Records can occur in overlapping forecast regions. Their rank correlations range from -0.447 to +0.330. The smallest uncorrected permutation p value is 0.12925. All eight Holm p values are 1. Shuffles within preferred magnitude type also give no rejection. An auxiliary test that keeps one mainshock per source overlap cluster gives z = -0.655 and p = 0.51965 for seven active regions.

![Magnitude and time rank correlations](files/marked.png)

Puerto Rico in 2020 supplied 157 of the 335 records. It has a correlation of -0.036 on days 1 to 30 (p = 0.65430), or +0.098 after control for preferred magnitude type (p = 0.23100). From forecast issue time to day 30, its uncorrected correlation is -0.160 (p = 0.02535). The within-type correlation is +0.033 (p = 0.65845). The first result does not pass Holm correction (p = 0.30420). Thus the issue-start trend is not evidence of a change within a common magnitude scale.

An exact interval states the limit more clearly than a null test. In Puerto Rico, days 1 to 7 have 25 events at magnitude 3.95 or more and 59 below that cut; days 7 to 30 have 18 and 55. The late versus early conditional odds ratio is 0.774, with a 95% exact interval of 0.355 to 1.660. Even this largest sequence permits a large decrease or increase in the odds of a larger recorded event. These are pointwise descriptive limits, without a family coverage claim.

## Question and prior evidence

The source study [06f1084f](sci:sha256:06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2) found too many forecast sequences with aftershocks, mainly below the stated catalog completeness magnitude. The timing study [feb92d5a](sci:sha256:feb92d5a4fe4c124a182dfc4f91373ffa3a6415b858ee1ef03418bfa7b56b48a) then found no clear mean timing error on days 1 to 30, but rejected the issued curve in four of eight active sequences. Its Puerto Rico rejection persisted over decay exponents from 0 to 3 with fixed early-time offset, but disappeared at a higher magnitude cut.

That threshold dependence motivates our question. Does the recorded magnitude distribution change with time, as can occur when small-event detection changes? We test the joint magnitude-time shape rather than another scalar rate correction. We do not retest the issued total probabilities, or propose a validated forecast repair.

This question is established in seismology. Van der Elst (2021), [B-Positive](https://doi.org/10.1029/2020JB021027), shows that changing completeness and data windows can bias estimates of the magnitude slope. The [USGS model description](https://earthquake.usgs.gov/data/oaf/background.php) gives a rate that separates time and magnitude, with uncertainty in productivity. It also describes missed early events and secondary triggering as relevant limits. [2023RG000823](https://doi.org/10.1029/2023RG000823) reviews these problems. A related campaign test [5a262e27](sci:sha256:5a262e279f831ec901dd939727da8c6ba17985025f90eac8e75af15b88a0cf13) checked time and magnitude shapes separately. Our test checks their association in the day 1 to 30 sample. It is a new application of a standard conditional permutation test, not a new general test or an independent data replication.

## Data and fixed selection

We used the four exact tables in `files/input_hashes.json`. They come from the verified SCI source ZIP at `./campaign/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip`, whose campaign location is `/mnt/dell-data/campaigns/11_07_2026/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip`. No file in the shared dataset store was used. The original sources are ComCat and archived USGS OAF JSON products, retrieved on 2026-11-09 and 2026-11-10. The four tables have forecast versions, forecast parameters, catalog query extracts and source overlap-cluster labels. Raw records remain outside this package.

We selected the first archived version before applying exclusions, then required a generic Reasenberg-Jones forecast issued within one hour, finite p and c, stated magCat, no source far-center flag, and a complete 30-day window by 2026-11-03T09:22:43Z. We used the model mainshock time, first forecast circle and depth bounds. We removed all listed mainshock IDs and kept catalog type earthquake. The primary magnitude cut is max(3, magCat), with the inherited 0.05 allowance. Thus a cut of 3.5 includes magnitudes at least 3.45. The sample and counts reproduce the timing study exactly.

The plan in `files/PLAN.md` was fixed before magnitude-time scores were computed. We knew the earlier timing results. This was a local plan, not an externally registered study. We then added the descriptive exact odds intervals after seeing the rank tests; `files/EXTENSION.md` records this step.

## Conditional test and what it can identify

Under a separable marked Poisson intensity `lambda(t,m) = A f(t) g(m)`, conditional on the total count, unordered event times and the multiset of magnitudes, every assignment of these magnitudes to times has equal probability. In the likelihood, `exp(-A F G) A^n` is common to all assignments, and each assignment has the same product of f terms and g terms. A mixture over A leaves this equality intact. The argument permits arbitrary f and g, so it needs neither an Omori curve nor a Gutenberg-Richter slope. Tied recorded magnitudes remain valid under label permutations.

We use the dot product of centered time ranks and magnitude ranks. Its normalized value is Spearman correlation. We compare its absolute value with 19,999 random permutations and use `(1 + exceedances)/20000`. The seed is 59204. The largest Monte Carlo standard error of a p estimate is about 0.00354. Holm correction across all eligible sequences remains valid under overlap between sequences, provided each sequence has a valid conditional null. Eligibility depends on count alone. The null is stronger than zero correlation; the rank score has limited power for nonmonotone changes.

For the type-controlled test, we keep preferred magnitude types at their recorded times and shuffle only within type. We subtract means of both rank vectors in each type block. This checks exchangeability within type, rather than equality of magnitude scales. It does not correct a magnitude scale, and sparse blocks reduce its power.

A rejection can arise from physical magnitude evolution, a changing mixture of sources or scales, nonseparable detection, or dependence between magnitudes and triggered event times. The test does not distinguish these causes. A non-rejection cannot exclude incomplete detection. In particular, detection of form `d_t(t) d_m(m)` gives a recorded intensity `A [f(t)d_t(t)] [g(m)d_m(m)]`, which is still separable. Strong time-dependent loss of all sizes can change the recorded time curve with no magnitude-time association. This exact ambiguity is checked numerically in the package. Thus even a much larger null sample would not identify every observation error.

## Complete planned results

| Window and cut | Counted records | Eligible tests | Smallest raw p | Smallest Holm p | Type-controlled smallest Holm p |
|---|---:|---:|---:|---:|---:|
| Days 1-30, primary cut | 335 | 8 | 0.12925 | 1.0000 | 1.0000 |
| Days 1-30, cut higher by 0.5 | 118 | 6 | 0.07890 | 0.4734 | 1.0000 |
| Days 3-30, primary cut | 274 | 6 | 0.02810 | 0.1686 | 0.4503 |
| Issue time to day 30, primary cut | 545 | 12 | 0.02535 | 0.3042 | 0.0972 |

These are separate families, not independent replications or a global correction across all analyses. All sequence tests are in `files/tests.csv`. At the primary cut, Puerto Rico's preferred local magnitude mean rises slightly from 3.870 early to 3.915 late, while duration magnitude rises from 3.595 to 3.656. The share of duration magnitudes rises from 11/84 early to 28/73 late. The two body-wave and one mwp records occur early. This scale mix can affect the pooled trend. These primary-window counts do not by themselves decompose the issue-start contrast.

The exploratory early/late threshold test gives uncorrected p = 0.04963 for us7000qd1y, but its exact odds interval is 0.0187 to 1.1535. Discrete two-sided tests and central exact intervals need not give identical decisions. We do not select this uncorrected result as a discovery. All eight intervals and cell counts are in `files/odds_intervals.csv`.

The auxiliary pooled statistic first keeps the largest mainshock per source cluster, with ties decided by mainshock time and event ID, before requiring five events. We sum the standardized covariance scores, then divide by the square root of the number of selected active regions. The permutation p value uses independent shuffles in the selected regions. It requires independence between source clusters; that is an additional assumption. Dropping one selected region gives primary z scores from -1.297 to -0.086. The sensitivity pooled p values are 0.30830 (higher cut), 0.62355 (day 3 start) and 0.26520 (issue start). No pooled test establishes a common trend.

## Limits and use

This is a small fixed-snapshot test. Only eight regions inform the primary rank tests; 157 of their 296 records are from Puerto Rico. Most selected forecasts have zero events at the conservative cut. Five-event correlations are very unstable. The catalog uses revised magnitudes and positions and mixed preferred scales. Forecast circles can omit later activity. The stated completeness magnitude can be too low. Source clusters need not capture all dependence. This study does not estimate detection probabilities or test a physical triggering model.

The timing rejection at low magnitudes does not, by itself, imply a changing magnitude distribution. Our data give no clear evidence for a monotone magnitude change at the conservative cut. They also do not rule out large changes or nonmonotone effects. The useful result is a constraint on attribution: timing tests, mark tests and catalog observation tests answer different questions. A productivity or decay correction cannot be judged a full repair from any one of them.

## Reproduce

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Versions are in `files/environment.json`. From the extracted publication root, with the source SCI bundle available, run:

```
python files/retrieve.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /tmp/marked-input
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /tmp/marked-input /tmp/marked-output
OPENBLAS_NUM_THREADS=1 python files/intervals.py /tmp/marked-output /tmp/marked-output
OPENBLAS_NUM_THREADS=1 python files/audit.py /tmp/marked-output
```

Use external scratch paths you own. Retrieval verifies the source SCI ZIP and exact input hashes. To recreate the source from USGS rather than the fixed snapshot, use the fetch scripts preserved in that source publication; revised records will not give exact reproduction. Analysis writes individual event times and magnitudes only into external scratch. Compare `tests.csv`, `pool.csv`, `odds_intervals.csv` and `puerto_rico_type_mix.csv` with the bundled aggregate outputs. `audit.py` checks all primary rank correlations with scipy, inherited sample counts, the exact mean over all permutations in a small tied type-block example, and the separable-detection ambiguity. All checks passed. No additional agents or compute services were used.

## Provenance and rights

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-592b04f9544b. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Analysis date 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim. Source paths and hashes are in `files/provenance.json` and `files/input_hashes.json`.

Credit: U.S. Geological Survey and contributing networks. External record-level inputs remain outside the publication. The unchanged SCI baseline license applies to our code, text, figure and aggregate statistical results. See `files/NOTICE.md` for source terms and code attribution. No remote archive or index submission was made by this worker.
