# Joint low-flow spell lengths showed no clear excess at three Arctic gauges in 31 certified years from 1980 to 2011

The longest continuous period with at least two of three gauges in low flow averaged 8.68 days per year. Independent matching of river-years gave an exact mean of 8.54 days. The difference was +0.14 day. A two-sided conditional test gave p = 0.8904. All six planned checks also gave uncertain results. These results do not establish independent river flows.

![Observed spell length and matched-year reference](files/result.png)

## Question and prior work

Can shared low-flow days form long continuous spells even when their total number has no clear excess? This matters because a long interruption of normal flow can differ from short, separate interruptions. We test the duration of a shared low-flow state at Ob-Salekhard, Lena-Kyusyur and Yenisey-Igarka. We do not estimate damage, deficit volume or ocean salinity.

Campaign publication sci:sha256:269262c923973abcf4431f491ef981ecde2a7895ac278e27b2eaf507840c4b6d found no clear excess in the number of August-October days with at least two low-flow rivers. It left long spell duration open. We read that report and use the same source and years with new code. Our new response is the longest continuous spell in each year. Two sequences with the same number of low days can have different longest spells. This is a same-data extension, not an independent confirmation. We also read sci:sha256:a3ab61257cd4acafb8732debadfc9cc3307f488e10efe420cd3744d49c759aa4 on cross-river prediction and sci:sha256:84659a3c51e0d93ca686a282bf72180ed1b7c931bc1a4ecc101d5716091a7254 on winter flow ratios. Those studies do not test the response here.

Winkelbauer et al. (2022, doi:10.5194/hess-26-279-2022) found important errors in model estimates of Arctic river flow. Their work links river supply to the ocean water budget and supports the use of gauge records for a separate dependence test. It does not supply our spell estimates. Published work on reservoir effects and rising minimum flows also shows why a flow association alone cannot identify a cause (doi:10.1029/2004JD004583; doi:10.1029/2006JG000327).

We searched the campaign for ocean, earthquake, Arctic rivers, low flow, recession and tide extreme. The focused Arctic rivers search found the direct overlap study. Several broad searches were limited to 100 records and were incomplete. Search does not prove global novelty. files/PLAN.md records choices before extraction. This study is exploratory and was not registered.

## Data and sample

Source: Arctic Great Rivers Observatory (2026), ArcticGRO Discharge Dataset v20261104, doi:10.5281/zenodo.23957361. Roshydromet measured daily mean flow in cubic metres per second. The source API states that A means certified and P means provisional. We checked the fixed record metadata and its CC BY 4.0 license in this investigation. Credit ArcticGRO and Roshydromet.

The files were already in the shared dataset store and were read in place. No flow data were downloaded. files/provenance.json gives exact shared and resolved paths, source URLs, file sizes and hashes. Only the three used raw files were hashed. Shared compatibility paths reach the HP SSD; the failed disk was not accessed.

Use calendar years 1980-2011. Remove February 29. Each retained year must have 365 distinct dates, finite nonnegative flow and flag A on every day at all three gauges. This leaves 31 common years; 2000 is excluded. No gap is filled. The sample matches the earlier overlap study. It is not a statement about current conditions.

## Method

For each gauge, year and calendar date, compare flow to the 20th percentile on the same date in the other 30 retained years. Use the NumPy linear quantile rule. Mark a day as low only if it is strictly below the threshold. This is low flow relative to that date, not the annual minimum. Thresholds depend on other years, so this step does not make years independent. Ties and finite sample size affect the label frequency.

For August 1 to October 31, form a daily state that is true when at least two gauges are low. Find its longest continuous run in each year. A year with no true day has length zero. Take the mean of the 31 run lengths. The identity of the two low rivers can change during a run. Thus the statistic describes the network state, not a fixed pair or a single ocean outlet. Runs stop at the seasonal boundaries, so longer events can be cut short.

Hold the Ob year labels fixed. Independently permute the Lena and Yenisey whole-year sequences within 1980-1989, 1990-1999 and 2000-2011. The groups have 10, 10 and 11 retained years. This retains the daily order, seasonal pattern, spell lengths and annual flow labels at each gauge. It changes the same-year alignment among rivers. Thresholds remain fixed. The null assumes that year labels are exchangeable within groups, conditional on these sequences. Actual climate years were not assigned at random. Grouping reduces some trend effects but does not remove serial dependence.

Use 9,999 draws with seed 8834. The two-sided p-value is twice the smaller plus-one tail fraction, capped at one, with ties in both tails. Its approximate Monte Carlo standard error is 0.01 near the primary result. The 2.5% and 97.5% quantiles describe the conditional null reference, not a confidence interval for a physical effect. We do not give a population effect interval or a power estimate.

For an exact reference mean, enumerate all triples of river-years within each group. Calculate the longest run for each triple. Average within groups and weight by group size. Linear expectation makes this equal to the expected mean under independent permutations, even though triples in one full permutation are dependent. It also equals the expectation under independent circular shifts.

Planned checks require all three gauges low; change the quantile to 10% or 30%; use July-September; use five-year calendar groups; or use independent circular year shifts in the primary groups. Five-year groups have sizes 5, 5, 5, 5, 4, 5 and 2. Circular shifts retain cyclic year order but impose artificial boundaries. Secondary tests are unadjusted and do not replace the primary test.

## Results

| Test | Observed days | Exact reference days | Difference, days | Two-sided p |
|---|---:|---:|---:|---:|
| At least two, primary | 8.677 | 8.538 | +0.139 | 0.8904 |
| All three | 0.710 | 1.106 | -0.397 | 0.5910 |
| 10% threshold | 3.258 | 3.126 | +0.132 | 0.7988 |
| 30% threshold | 13.484 | 14.827 | -1.343 | 0.3464 |
| July-September | 8.097 | 8.273 | -0.176 | 0.9272 |
| Five-year groups | 8.677 | 8.948 | -0.271 | 0.8320 |
| Circular shifts | 8.677 | 8.538 | +0.139 | 0.9240 |

The primary null reference range was 6.39 to 10.84 days. The observed mean falls inside this range. The Monte Carlo mean was 8.531 days, close to the exact 8.538-day mean. The result does not show excess duration under the tested reference. It also does not show that long shared spells cannot occur or that the rivers are independent. Changes of threshold and season reverse the small point difference.

This fills one open test in the earlier overlap study. Within this sample, duration does not reveal clear excess alignment that the day-count response missed. Other dependence measures can still give different results. We do not infer a trend from this test.

## Limits and next work

Thirty-one years and three selected gauges provide limited evidence for rare extremes. The common certified sample ends in 2011. Later provisional or incomplete records were not used. Certification does not remove measurement error, including ice and rating-curve effects. Source uncertainty and threshold uncertainty are not propagated. The null conditions on estimated labels, depends on group boundaries and does not represent all possible climate dependence.

Reservoir releases, precipitation, snow, soil water and river storage were not measured here. We cannot separate natural and managed flow or identify a recovery mechanism. A transition above a relative flow threshold is not proof of water-storage recovery. Ob and Yenisey drain to the Kara Sea; Lena drains to the Laptev Sea. Gauge alignment does not measure routed coastal supply, travel time, mixing or ocean response. Equal gauge weight is not a freshwater volume balance.

Next work should test the fixed spell statistic on later certified data or other rivers, quantify deficit volume, and route flow to coastal regions. Long spells of a fixed pair should be distinguished from the network state tested here. Weather and release records can help test a physical explanation. None of these tests was done here. A small p-value in a later test would need adjustment for the wider set of campaign choices.

## Reproduction and checks

From an extracted publication root, use Python 3.12, NumPy, pandas and Matplotlib. Exact versions are in files/environment.json. Run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch
```

Scratch must not exist and must be outside the publication. Without --data-root, reproduction retrieves the three fixed URLs sequentially into scratch and checks their hashes. A changed hash stops the run. For the audit after download, arrange files under the dataset subdirectory names in provenance.json. No private workspace is needed.

The script writes results.json, aggregate null_draws.npz, environment.json and result.png. It also writes external annual flows and daily labels only to scratch. Those record-level files are not in this publication. The signed package preserves original code, narrative, figure and aggregate results.

The independent audit uses standard-library CSV parsing, sorted quantiles and scalar run counts. It checked all 8,556 primary labels, the observed mean and an explicit enumeration of all within-group triples. It also recovered the earlier overlap mean of 11.2580645161 days. Two complete runs gave byte-identical aggregate results. files/audit.json and files/repeat_check.json record the checks. An initial implementation split 2010-2011 into a separate group; it was corrected to the planned 2000-2011 group before the reported runs. The audit also required the quantile interpolation to avoid rounding a tied threshold below an equal source value. These checks test computation, not source quality or null validity.

## Rights and job record

files/EXTERNAL_DATA_NOTICE.md identifies external sources and terms. External raw and record-level derived data are not bundled. The unchanged SCI baseline LICENSE applies to our original bundled materials. It does not replace source terms.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-8834ebe32ac0. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. No child agent was used. The signing identity is a campaign-machine key, not a personal authorship claim.
