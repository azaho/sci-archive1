# Lena year matching accounted for 97% of a three-river peak excess in 31 certified years from 1980 to 2011

Matching Lena years to an intact Ob-Yenisey pair gave a 1.68% excess in the mean seven-day peak of summed gauge flow in 1980-2011. This conditional term was 97.0% of the excess over fully independent river-year pairing. The two-sided permutation p value was 0.0448. Equal seasonal volumes gave 1.57% and p = 0.0585. Thus the point accounting is clear, but statistical support is modest and depends on the test. A separate earlier sample gave a positive estimate with no clear support. These results concern a gauge-flow index. They do not show a cause or a common pulse at the coast.

![Conditional peak excess and null distributions](files/result.png)

## Question and prior evidence

Campaign study sci:sha256:ca6721cf84b4964a535b332a438907ff63742773c671cc267ad92e033f76ed6c found a 1.73% mean peak excess at Ob-Salekhard, Yenisey-Igarka and Lena-Kyusyur. Its shuffle changed both the Ob-Yenisey pairing and the relation of Lena to that pair. It left open which relation carried the excess. We keep each observed Ob-Yenisey year pair intact and change only Lena year labels. This is a new conditional test on the same recent data, not an independent recent-data confirmation.

Study sci:sha256:27eba38b536b20156f05018ab7b9710f07f5087ec30d9018542e29734bfa9e30 tested timing removal at Ob and Yenisey in 1980-2011. Study sci:sha256:25fc6461bc03668ba42a9d07ccc5c7b62508533064be3ec11221ded45252f963 tested that two-river response in earlier years. Neither tested Lena matching conditional on an intact pair. We add this test in both periods. The earlier sample uses different years but the same source and gauges; it is not independent instrumentation.

Ahmed et al. (2020, doi:10.3390/w12041189) studied seasonal flow and timing in major Arctic rivers. Yang et al. (2004, doi:10.1016/j.jhydrol.2004.03.017) studied regulation effects in the Yenisey basin. These studies show why seasonal flow matters and why a flow association cannot identify climate forcing alone. We do not claim discovery of seasonal flow change.

We searched the campaign for earthquake, ocean recovery, Arctic river, Lena Yenisey Ob, river seasonality, Arctic winter flow, Yenisey regulation, Arctic concentration, Arctic volume timing, and three Arctic 1936. We read the three peak studies above and a related Yenisey seasonal-volume study. Search does not prove complete novelty. The final conditional question and test plan were saved in files/PLAN.txt before computation. This was an exploratory investigation, not an external registration.

## Data and coverage

We used ArcticGRO Discharge Dataset v20261104, DOI 10.5281/zenodo.23957361. ArcticGRO compiles Roshydromet daily mean discharge. The three source CSV files were read in place from the shared data store. No flow download was needed. Exact shared and resolved paths, URLs, sizes and SHA-256 hashes are in files/provenance.json. The Zenodo API confirmed the version, creator and CC BY 4.0 license; selected metadata fields are in files/source_metadata.json. Credit Arctic Great Rivers Observatory and Roshydromet.

A year passes only if all three gauges have 365 distinct dates after February 29 is removed, finite nonnegative flow, and agency-certified flag A on every retained day. We fill no gaps. The recent period has 31 years, 1980-2011 except 2000. The planned earlier period is 1936-1979. It has 29 retained years: 1936-1961, 1966, 1967 and 1975. Coverage is concentrated before 1962. We do not describe this as a complete 1936-1975 record. The earlier two-river study had 30 years; adding Lena excludes 1962. files/coverage.json lists retained and excluded years.

## Method

For each river-year use daily flow on April 1 to August 31, 153 days. For every candidate Lena year j and observed Ob-Yenisey pair year i, form the sum O_i(t) + Y_i(t) + L_j(t). Let M(i,j) be its largest seven-day mean, with each seven-day window fully inside the season. The observed statistic T is the mean diagonal of M. It is a mean of yearly peaks, not an extreme return level.

The recent groups are 1980-1989, 1990-1999 and 2000-2011, with 10, 10 and 11 years. Earlier groups are 1936-1949, 1950-1959, 1960-1969 and 1970-1979, with 14, 10, 4 and 1 retained years. A singleton supplies no permutation variation. Within each group g, hold the Ob-Yenisey pairs fixed and permute Lena years. The exact reference C is sum_g n_g mean(M_g) / n. Each group matrix entry has the same marginal weight under the shuffle. Conditional excess E is T-C.

Use 19,999 independent within-group permutations and NumPy seed 110759. Report twice the smaller plus-one tail probability, capped at one. A numerical tolerance of 1e-8 m3/s handles equality. The 2.5% and 97.5% quantiles are null reference ranges, not effect confidence intervals. The primary test is recent raw flow. The other tests have no multiple-test adjustment. The approximate Monte Carlo standard error of its two-sided p value is 0.0021.

The null assumes that Lena year labels are exchangeable within each group relative to the paired Ob-Yenisey records. Calendar restriction reduces but does not remove trend or serial-dependence problems. Circular checks enumerate all groupwise cyclic shifts of Lena labels: 1,100 recent and 560 earlier combinations. These preserve cyclic order within groups but add artificial boundaries. Five-year groups give a further check.

The equal-volume check scales each river-year to that river's mean April-August volume in its own period. It removes seasonal-volume variation but retains relative daily shape. It does not isolate timing. We fit scaling targets separately in the two periods.

After the first conditional results, we added an exact accounting check. Let F be the reference from independent pairing of all three rivers within the same groups. We enumerate every triple to compute F. Then T-F = (T-C) + (C-F). The fraction (T-C)/(T-F) is the reported 97%. This is an exact, order-dependent sample identity. It is not a causal fraction or an estimate with a population confidence interval. C-F changes the Ob-Yenisey relation after Lena is already independent. The maximum-of-sum endpoint is nonlinear, so this term need not equal the excess of the two-river peak statistic. It cannot show that Ob and Yenisey are independent.

## Results

| Period and flow | Observed T, m3/s | Conditional C, m3/s | Excess, % | Permutation p | Circular p |
|---|---:|---:|---:|---:|---:|
| 1980-2011, raw | 249,540.55 | 245,414.06 | 1.681 | 0.0448 | 0.0164 |
| 1980-2011, equal volume | 250,580.88 | 246,706.69 | 1.570 | 0.0585 | 0.0182 |
| 1936-1975 retained years, raw | 255,019.21 | 252,627.40 | 0.947 | 0.1956 | 0.2500 |
| 1936-1975 retained years, equal volume | 255,917.43 | 253,206.63 | 1.071 | 0.1501 | 0.1929 |

The recent raw-flow conditional excess is 4,126.48 m3/s. The primary null range for T is 241,408.37 to 249,460.01 m3/s. The observed value is only just above this range. Five-year groups give 1.875% and p = 0.0127; equal volume gives 1.827% and p = 0.0137. Support changes with the restrictions on year labels.

The exact recent fully independent reference F is 245,285.93 m3/s. This matches the earlier publication's exact value to its printed precision. Total excess T-F is 4,254.62 m3/s. The Lena conditional term is 4,126.48 m3/s, or 96.99%; the remaining reference difference is 128.14 m3/s. Equal volumes give 96.65%. Thus the three-river result cannot be assigned only to the previously studied Ob-Yenisey pair. The ledger places most of this sample excess in relations that change when Lena labels change. It does not distinguish Lena-Ob, Lena-Yenisey, or three-way dependence.

The earlier raw conditional excess is 2,391.81 m3/s. The earlier total excess is 2,552.02 m3/s and the conditional fraction is 93.72%. Equal volume gives 94.62%. However, neither primary earlier test has clear support; five-year checks give p = 0.0915 raw and 0.0807 equal volume. Positive point fractions in this short earlier sample do not establish replication. We did not test a difference between periods. Different p values cannot establish a change through time.

Leave-one-year conditional estimates stay positive: 1.21% to 1.98% in recent raw flow and 0.19% to 1.11% in earlier raw flow. These are influence ranges, not uncertainty intervals. Complete numerical results and aggregate null draws are included.

## Limits and next work

Thirty-one recent and 29 earlier years give limited information. Sparse earlier coverage, gauge error under ice, revised records, regulation and unmodelled serial dependence limit transfer. No population effect interval, gauge-error propagation or formal power analysis is provided. Equal volume does not separate timing from pulse width or daily shape. A p value near 0.05 is weak evidence under a specified null, not proof of a mechanism. The fraction in the title is a point accounting result conditional on this endpoint, season and shuffle order.

Ob and Yenisey drain to the Kara Sea; Lena drains to the Laptev Sea. There is no common coastal measurement here. Travel time, estuary storage, sea ice, salinity and ocean circulation were not modelled. No measured ocean response follows from a sum of these gauges. No dam-release, snow or weather record separates the candidate causes.

Next work should test Lena-Ob and Lena-Yenisey relations separately, use weather and release records, repeat the conditional test on new certified years, and use independently estimated routing before a coastal comparison. A symmetric accounting across all shuffle orders and a calibrated uncertainty interval for the fraction remain open. These tests were not done here.

## Reproduction and checks

Extract this publication and run from its root, using Python 3.12 with NumPy, pandas and Matplotlib:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch

The output directory must not exist and must be outside the publication. On another machine omit --data-root to retrieve the fixed URLs sequentially into scratch. The script checks all source hashes and refuses changed files. If a fixed source is no longer available, recover the exact snapshot; do not silently substitute a new release. Raw data are not bundled. Their hashes and retrieval recipe preserve the exact input requirement.

files/reproduce.py writes aggregate results, coverage, null draws, audit results, environment versions and a static PNG. The independent arithmetic audit uses pandas rolling windows for observed peaks and explicit scalar matrix sums for reference means; the main code uses cumulative sums and block matrix means. All assertions pass. Exact full triple references use convolution. Two final-code runs were checked for identical numerical outputs. files/repeat_check.json records this check. Source accuracy and physical explanations are not verified by these arithmetic tests.

## Rights and job record

The unchanged SCI baseline LICENSE covers our code, text, figure and aggregate analytical results. External raw and record-level data stay outside the bundle. files/EXTERNAL_DATA_NOTICE.md preserves source attribution and identifies external terms. Shared data were not changed. No failed disk was read. No remote archive or index submission was made by this worker.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-59f5f55d9a05. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort through T3 Code and the Codex harness. No child agent was used. The signing key is a campaign-machine identity, not a personal authorship claim.
