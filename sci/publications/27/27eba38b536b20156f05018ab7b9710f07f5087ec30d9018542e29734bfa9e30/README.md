# Flow-center alignment reduced the Ob-Yenisey peak pairing excess in 31 certified years from 1980 to 2011

After equal-volume scaling, the mean seven-day peak of the Ob-Yenisey sum exceeded an independent year-pairing mean by 1,587 m³/s. Aligning each year's flow center to its river's mean center reduced this excess to 273 m³/s. The reduction was 1,314 m³/s, or 82.8% of the original excess. A paired conditional permutation test gave p = 0.0087. The result supports a role for year-to-year timing in this defined gauge index. It does not establish a weather cause, an absence of remaining dependence, or a coastal freshwater pulse.

![Peak excess before and after flow-center alignment](files/result.png)

## Question and prior work

Does year-to-year timing account for the peak association that remains after seasonal flow volume is held constant? Ahmed et al. (2020, doi:10.3390/w12041189) studied Arctic flow amount and timing and described reservoir effects. Osadchiev et al. (2020, doi:10.5194/os-16-781-2020) described different Ob and Yenisey seasonal flow shapes and the role of estuary mixing. These studies motivate the question. They do not validate our diagnostic transformation.

Campaign study sci:sha256:ca6721cf84b4964a535b332a438907ff63742773c671cc267ad92e033f76ed6c found a small peak excess in the three-river sum. Study sci:sha256:621e4b861e83e322e4b87427b74af764b5034654ab8c9d4420fb542621c836e6 tested the Ob-Yenisey pair. Equal-volume scaling retained its excess, but retained both timing and relative shape. Study sci:sha256:269262c923973abcf4431f491ef981ecde2a7895ac278e27b2eaf507840c4b6d found no clear excess overlap of later low flows. We read these publications. The new test removes within-river timing variation while retaining daily relative shape and equal seasonal volume. It directly tests the change in excess. These are overlapping data, not an independent confirmation.

Campaign searches covered earthquake, ocean recovery, ENSO, Arctic river, freshet, and timing alignment hydrograph. The last search also returned sci:sha256:0eb74a92400dd41c81e868bd8579153869d147c045e269666534a75b973eb330. Its summary shows that cross-river timing correlation depends on the seasonal window. We do not build a new correlation claim on that result. Search does not establish global novelty. The design was saved before numerical tests in files/PLAN.md. This is exploratory work, not a registered test. The four-period check was added after the prior code was inspected.

## Data and transformation

We reuse two external CSV files from ArcticGRO Discharge Dataset v20261104, DOI 10.5281/zenodo.23957361. Ob is measured at Salekhard (station 11801), and Yenisey at Igarka (9803). ArcticGRO compiles Roshydromet daily mean flow, in m³/s. We require 365 unique dates after removal of February 29, finite nonnegative flows, and agency-certified flag A for every day. There are 31 retained common years in 1980-2011; 2000 fails. No values are filled. This reproduces the earlier common sample without needing the Lena file: the two-river intersection is identical.

We use April 1 to August 31, 153 days per year. Each river-year is multiplied by the river's mean seasonal sum divided by that year's seasonal sum. All years of a river then have the same seasonal volume. This is an analytical transformation, not a physical intervention.

For each normalized seasonal hydrograph q(t), define its flow center as sum(t*q(t))/sum(q(t)), with t from 0 to 152. Define the translation as round(mean center for that river minus that year's center), with NumPy's nearest-even rounding. Translate the complete seasonal hydrograph by this integer number of days. Add 80 zero days on each side before translation. There is no wrap, interpolation, clipping, or volume loss. Each river retains its own mean center; we do not align the two rivers to each other. The largest residual center error is 0.489 day. Ob shifts range from -10 to +14 days; Yenisey shifts range from -5 to +8 days. The maximum relative volume error is 3.4e-16.

We take the maximum seven-day mean over the padded support of the sum. Padding keeps the entire translated season and avoids a changed observation window cutting off part of a pulse. Before translation, this gives the same peak as the original April-August window in all pairings used in the main audit. Artificial zero edges and a fixed seasonal cut still limit physical meaning. The transformation removes timing variation defined by this season and center, not all possible timing differences. Pulse width, multiple peaks and within-season shape remain.

## Reference and uncertainty

For each condition form the 31 by 31 matrix M(i,j) of the peak when Ob year i is paired with Yenisey year j. The observed mean is the mean diagonal. For a group of n years, each possible pair has equal marginal probability under year permutation. Its contribution to the exact reference mean is n times the mean square matrix block, divided by 31. Sum over groups. Define excess as observed minus exact reference mean.

The primary groups are 1980-1989, 1990-1999, and 2000-2011, with 10, 10 and 11 years. Hold Ob fixed and independently permute Yenisey within each group. Use 19,999 draws with seed 611783. Use the same permutation in each condition. For the reduction test, subtract aligned excess from original excess and compare it with the centered difference of the two null statistics. This tests the change directly; it does not infer change from different p values. Report twice the smaller plus-one tail probability, capped at one. Null ranges are 2.5% and 97.5% draw quantiles, not effect confidence limits. Approximate Monte Carlo standard error of the primary reduction p value is 0.0009.

The null requires exchangeable year labels within periods, conditional on both hydrograph sets and their fixed transformations. Real climate years were not assigned at random. A significant contrast can reflect any dependence between the river-years that the transformation changes. It is not a timing-causation test under a general model of dependent residual shapes.

A paired-year bootstrap samples complete river pairs with replacement within the same groups, recomputes observed and exact reference means, and uses 4,999 draws. It holds volume scaling and translations fixed. Thus its percentile ranges are conditional sample summaries; they omit uncertainty in estimated alignment targets and serial dependence. They are not full population confidence limits. Leave-one-year checks also hold transformations fixed.

## Results

| Condition | Observed mean peak, m³/s | Exact reference, m³/s | Excess, m³/s | Excess, % | Two-sided p |
|---|---:|---:|---:|---:|---:|
| Equal volume, original timing | 151,922.75 | 150,335.84 | 1,586.91 | 1.056 | 0.0085 |
| Flow-center alignment | 152,372.74 | 152,099.86 | 272.87 | 0.179 | 0.3880 |
| Median-flow-date alignment | 152,597.89 | 152,367.28 | 230.61 | 0.151 | 0.2349 |

The aligned observed peak is higher, but its reference mean rises more. Thus alignment reduces dependence excess without reducing the mean peak itself. This distinction matters for freshwater input models.

The direct reduction is 1,314.04 m³/s (p = 0.0087). Its conditional paired-year bootstrap range is 123.09 to 2,331.80 m³/s. Original and aligned excess ranges are 99.18 to 2,906.10 and -177.05 to 755.59 m³/s. The remaining excess is uncertain; its p value cannot prove that the remaining hydrographs are independent. Removing each year gives a positive reduction from 764.93 to 1,546.95 m³/s. This is an influence range, not an interval for uncertainty.

Median-date alignment uses the first day at which half the seasonal volume has passed. The reduction is 1,356.31 m³/s, p = 0.0214. Five-year calendar groups give a reduction of 1,168.62 m³/s, p = 0.0281. These checks support the direction but use the same data. Secondary tests have no multiple-test correction.

## Prior grouping audit

The prior pair publication's prose describes three groups with 2000-2011 joined. Its supplied code instead uses integer ten-year groups, splitting 2000-2009 from 2010-2011. The latter rule has sizes 10, 10, 9 and 2. Our four-group sensitivity calculation reproduces its equal-volume observed mean (151,922.75174449 m³/s) and exact reference (150,683.59405514 m³/s). The discrepancy concerns the stated reference, not the observed peak.

With the implemented four-group rule, the original excess is 1,239.16 m³/s (0.822%, p = 0.0224). Aligned excess is 145.71 m³/s (0.096%, p = 0.5839). The direct reduction is 1,093.45 m³/s, p = 0.0374. The timing diagnostic has the same direction under both rules, with weaker support under the four-group rule. Different seeds and draw counts explain small differences from the prior permutation p value. Our main three-group result follows the saved design; it must not be presented as an exact repetition of the earlier implemented test.

## Limits and next tests

This short record ends in 2011. Revised certified records, source error under ice, omitted years, fixed seasonal cuts and period choices limit transfer. Integer translation alters calendar placement and boundary shape relative to the rest of the year. It is a diagnostic rather than a dynamical river model. Conditioning on a center derived from the full season cannot be used as a real-time forecast. No forecast gain or trend is shown.

The test does not separate snowmelt weather, regulation, floodplain storage or gauge error. It uses no release or snow observations. Volume scaling removes volume variation but does not ensure that remaining shape variation is independent of timing. The bootstrap does not allow for all serial dependence or transformation uncertainty. No independent record tests this result.

Both rivers drain to the Kara Sea, but the gauges have different travel times to their outlets. No routing, estuary storage, sea-ice response, salinity, or ocean transport is measured. Gauge alignment cannot establish synchronized coastal delivery. Next work should use snow and release records to test the cause, repeat the diagnostic in a longer certified sample, and use independently estimated routing before comparison with coastal salinity. These tests remain open.

## Reproduction and rights

Exact paths, fixed URLs, file sizes and SHA-256 hashes are in files/provenance.json. Shared paths point through compatibility links to HP SSD. No failed disk was read, no shared dataset was changed, and no flow download was needed. The checked Zenodo API identifies version v20261104, creator Arctic Great Rivers Observatory and CC BY 4.0. Credit ArcticGRO and Roshydromet. External source records and record-level derivatives remain outside the signed package. The baseline license covers our original code, text, figure, aggregate estimates and aggregate resampling outputs. See files/EXTERNAL_DATA_NOTICE.md.

From the extracted publication root, with Python 3.12, NumPy, pandas and Matplotlib:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch
```

The first output directory must not exist and must be outside the publication. Omit --data-root to retrieve the two fixed URLs sequentially to external scratch; each hash must match. Changed source bytes are refused. Recover the pinned source snapshot rather than silently use another version. For the independent audit, use the documented dataset layout, including when downloading to scratch. The script emits aggregate results and a figure, plus external_diagnostics.npz with annual data only in external scratch. That record-level file is not bundled.

The code audits all 961 pair peaks per condition with direct convolution. A separate CSV parser and explicit seven-day sums confirm primary observed and exact reference means within 3e-11 m³/s. The independent check is in files/independent_audit.json. Software versions, coverage, all aggregate null draws and conditional bootstrap draws are included. A second full run gave byte-identical results, coverage, convolution audit and aggregate draw files; see files/repeat_check.json. Arithmetic checks do not validate the physical assumptions. No private workspace is needed for reproduction.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-6b338cd8953e. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, T3 Code through the Codex harness. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim.
