# Flow-center alignment reduced the Ob-Yenisey peak excess by 72% in 30 certified years from 1936 to 1975, with mixed test support

We tested whether a flow-timing result from 1980-2011 transferred to a separate earlier record. We used ArcticGRO v20261104 daily flow at Ob-Salekhard and Yenisey-Igarka. Thirty complete certified years passed in a planned 1936-1979 window; the last retained year was 1975. Each April-August hydrograph had the same volume within its river. Aligning each flow center to its river mean reduced the mean seven-day peak excess over independent year pairing from 1,486 to 414 cubic metres per second. The reduction was 1,073, or 72.2%, with primary conditional permutation p = 0.0527. A refitted paired-year bootstrap range was 60 to 2,020; a three-position block range was 112 to 2,079. Five-year groups gave p = 0.1198; median-date alignment and circular shifts gave 0.0383 and 0.0061. Thus the point reduction transferred, but test support was mixed. This is a separate-period test on the same gauges and source, not proof of a cause or a coastal pulse. Sparse later coverage, source error, regulation, exchangeability and short blocks limit the result. Original code, aggregate evidence and fixed source hashes support reproduction.

![Peak excess in separate periods](files/result.png)

## Question and prior work

Does removal of year-to-year flow timing variation reduce the Ob-Yenisey peak association in an earlier record that was not in the prior test? The two rivers supply freshwater to the Kara Sea. Shared timing can affect a sum of gauge flows. This sum does not measure flow arrival at the coast.

Campaign study sci:sha256:27eba38b536b20156f05018ab7b9710f07f5087ec30d9018542e29734bfa9e30 found a reduction of 1,314 m³/s in 31 certified years from 1980 to 2011. We read that publication and took its equal-volume, integer flow-center alignment method as our test. Its original timing excess was 1,587 m³/s and its aligned excess was 273 m³/s. Campaign study sci:sha256:ca6721cf84b4964a535b332a438907ff63742773c671cc267ad92e033f76ed6c first tested the three-river peak index. Study sci:sha256:269262c923973abcf4431f491ef981ecde2a7895ac278e27b2eaf507840c4b6d found no clear excess overlap of later low flows. We read both for context. Those results do not determine the outcome in this earlier sample.

Ahmed et al. (2020, doi:10.3390/w12041189) studied seasonal flow amount and timing and described reservoir effects. Osadchiev et al. (2020, doi:10.5194/os-16-781-2020) showed that estuary mixing affects river plumes. These studies motivate our scope and its coastal limits. We do not claim a new finding about seasonal river flow or estuary mixing.

We searched the campaign for earthquake, ocean recovery, streamflow drought, Arctic discharge, freshet, and Ob Yenisey 1936. We found no direct test of this earlier-period timing-removal response. Search is not proof of global novelty. The new contribution is a separate-period test, with all volume and timing targets fitted only on that period. It uses the same gauges and source version. Non-overlap of years does not prove statistical independence across periods. The saved design is files/PLAN.txt. This is exploratory work, not a registered test.

## Data and coverage

ArcticGRO Discharge Dataset v20261104, DOI 10.5281/zenodo.23957361, compiles daily mean flow from Roshydromet. We use Ob at Salekhard (11801) and Yenisey at Igarka (9803). Units are m³/s. We require a complete calendar year with 365 distinct dates after February 29 is removed, finite nonnegative flow, and flag A on each retained day. No value is filled. Both files were reused in the shared store without changes or downloads. Exact paths, resolved shared paths, fixed source URLs, sizes and SHA-256 hashes are in files/provenance.json. Compatibility paths refer to HP SSD; no failed disk was read.

The planned early window was 1936-1979. Only 30 common years pass: 1936-1962 inclusive, 1966, 1967 and 1975. Fourteen other years fail the flow or certification checks. files/coverage.json lists all years; files/independent_audit.json gives per-file exclusion reasons. Coverage is concentrated before 1963. This result must not be described as full coverage of the 44-year window. The late method check uses the prior 31 common years in 1980-2011, with 2000 excluded.

## Method

For each year, keep the 153 days from April 1 to August 31. Multiply each river-year by the mean seasonal sum for its river divided by its own seasonal sum. Thus all years of one river have the same seasonal volume. Each period has separate targets. For q(t), with t = 0,...,152, the flow center is sum(t q(t))/sum(q(t)). Translate by round(mean center minus center), using nearest-even rounding. Add 80 zero days on each side before translation. No flow wraps, is lost or is interpolated. Shifts in the early sample range from -12 to +14 days. Each river retains its own mean center; we do not force the rivers to peak together.

For each original and aligned condition, form a matrix M(i,j). Its entry is the largest consecutive seven-day mean of the sum of Ob year i and Yenisey year j, on the full padded support. The observed statistic is the mean diagonal. For a group with n years, the exact independent year-pairing mean is the mean of its n by n submatrix. Weight group means by n/30. Define excess E as observed minus reference. Our primary response is E(original) minus E(aligned). This directly tests the change; separate tests before and after alignment cannot replace it.

The planned groups are 1936-1949, 1950-1959, 1960-1969 and 1970-1979. Retained sizes are 14, 10, 5 and 1. The singleton 1975 contributes zero excess and no permutation variation. Hold Ob fixed and permute Yenisey labels within groups. Use the same permutation in both conditions. We use 19,999 draws with seed 11072086; the sequence also covers the later checks. Two-sided p is twice the smaller plus-one tail fraction, capped at one, with numerical tolerance 1e-9 m³/s. Reference ranges in results.json are null ranges, not confidence intervals. Monte Carlo standard error of the main two-sided p is about 0.0023.

The conditional null requires exchangeable year labels within groups. Transformations are fixed for permutation tests. Each river retains its marginal hydrographs and seasonal cycle. This test is not a randomized experiment. It can respond to any dependence changed by translation, not only to a causal timing effect.

The paired-year bootstrap samples pairs within the same groups. For each of 1,999 draws, it refits volume scaling and alignment targets and recomputes both exact references. The three-position circular block bootstrap resamples consecutive positions within each group and also refits. Its blocks follow retained-year order: gaps mean that positions are not always adjacent calendar years. Circular edges are artificial, groups are small, and the singleton remains fixed. These percentile ranges are conditional sample uncertainty summaries. They do not cover every form of serial dependence, source error or nonstationarity. A bootstrap range and a permutation p test different assumptions; their disagreement is not a computational contradiction.

Planned checks use five-year calendar groups, median-flow-date alignment, and circular label shifts within the primary groups. Median alignment uses the first date on which half the seasonal volume has passed. Secondary tests have no multiple-test correction. Leave-one-year checks refit targets and references. We do not test a difference between periods.

## Results

| Early-period test | Original excess, m³/s | Aligned excess, m³/s | Reduction, m³/s | Two-sided reduction p |
|---|---:|---:|---:|---:|
| Flow center, primary | 1486.28 | 413.73 | 1072.55 | 0.0527 |
| Five-year groups | 1130.14 | 295.34 | 834.80 | 0.1198 |
| Median date | 1486.28 | 194.40 | 1291.88 | 0.0383 |
| Circular shifts | 1486.28 | 413.73 | 1072.55 | 0.0061 |

Original and aligned observed mean peaks are 155262.20 and 155631.08 m³/s. Their exact reference means are 153775.91 and 155217.35 m³/s. Alignment raises the reference more than it raises the observed mean. It reduces dependence excess without reducing the observed peak. The primary reduction is 72.16% of original excess. Original excess is 0.967% of its reference; aligned excess is 0.267%. The original excess test gives p = 0.0057; aligned excess gives p = 0.0864. A large aligned p cannot prove independence.

The refitted paired-year bootstrap 95% percentile range for reduction is 60.47 to 2019.92 m³/s. The three-position block range is 112.13 to 2078.61. Both are positive, but the primary permutation result and five-year check give weaker support. The early point reduction transfers in direction and rough size; statistical support is mixed. Leaving out each year retains a positive reduction from 877.25 to 1497.11 m³/s. That is an influence range, not an uncertainty interval.

The late method check reproduces the prior excesses to rounding: 1586.91 before alignment, 272.87 after, reduction 1314.04 m³/s. Its new Monte Carlo p is 0.0099 versus 0.0087 in the prior study; random draws differ. This check validates method transfer, not a new late-period finding. Comparing significance across periods is not evidence of a period change.

## Limits and next tests

The evidence supports a repeatable descriptive timing diagnostic, with mixed early-period inference. It does not identify snowmelt weather, regulation, storage, or gauge error as the cause. Translation also changes calendar placement relative to the fixed seasonal cut and uses zero edges. Equal-volume scaling removes amplitude variation but retains width and shape, which may depend on timing. Gauge error, especially near ice conditions, is not propagated. Certification does not remove error.

Only 30 early years pass; just six retained years follow 1959. Historical measurement and reservoir regimes differ from the late sample. We have no weather or release records and no untreated control. Period groups can reduce slow change but do not ensure exchangeability. We report all planned checks, including weaker ones. No return level, trend, forecast skill, salinity response or ocean circulation effect is shown. Gauge-to-coast routing and estuary storage are absent.

Next work should explain the missing certified early years, test other stations or source versions, and add snow and release observations. An independent routing model is needed before testing coastal salinity. This study does none of those tests. The mixed permutation support makes a causal timing claim premature.

## Reproduction and checks

From an extracted bundle, with Python 3.12, NumPy, pandas and Matplotlib, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch
```

The output directory must be new and outside the publication. Omit --data-root to fetch the two fixed files sequentially into new_scratch/external_data. Then use that directory as data_root in the audit. Each source hash must match; changed bytes are refused. Use the pinned source snapshot rather than silently accepting a revision. Exact software versions are in files/environment.json. No source record or per-year discharge table is bundled. The script makes only aggregate outputs and metadata. Its matrices stay in memory.

An independent standard-library CSV parser and explicit rolling sums reproduce the main excesses. The production cumulative-sum matrices were also checked against direct convolution for every pair in both periods. Maximum peak differences were below 2.1e-10 m³/s. A second full run checks deterministic results; see files/repeat_check.json. These checks test arithmetic, not the physical assumptions.

## Rights and job record

Credit Arctic Great Rivers Observatory and Roshydromet. Source v20261104 is identified by its fixed DOI and hashes. The Zenodo API was checked and states CC BY 4.0. Raw records stay in the external shared store or retrieval scratch. The signed bundle contains our code, narrative, figure and aggregate analytical results. files/EXTERNAL_DATA_NOTICE.txt identifies the external source and its terms. The unchanged SCI baseline LICENSE covers the bundled original materials and does not replace source terms.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-a2086d7f5f9e. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, T3 Code through the Codex harness. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim.
