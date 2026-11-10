# Dry-spell age matching retained an 8% post-1997 recession rise in 348 southern Australian catchments

The pooled recession increase remained after we held dry-spell age, flow and season approximately fixed. With AGCD rain, the increase was 8.0% (conditional 95% interval 5.4-10.7%). With SILO rain, it was 8.3% (5.6-11.3%). Thus a change in the mix of dry-spell ages does not explain the full pooled signal. However, the direct increase was small and uncertain in spells of at least eight dry days and in 2010-2021. These tests do not establish a constant faster drainage process through the full post-1997 period.

## Question and prior work

Publication 7cecffa9 reported 11% faster recession at equal flow in southern Australia after 1997. It interpreted this as evidence for more loss from the stream-connected store. Publication 95ea56ac showed that flow alone cannot identify loss, recharge and storage-to-flow changes. We test another issue: equal flow need not mean the same mixture of fast and slow flow paths. Days soon after rain can differ from days late in a dry spell. A change in the sampled mix can change a pooled recession curve.

Recession selection and parameter sensitivity are established concerns (Dralle et al., 2017, doi:10.5194/hess-21-65-2017). Tashie et al. (2020, doi:10.1029/2019WR025448) found systematic differences between individual events and pooled point clouds in US streams. Our contribution is a raw-data test of dry-spell age in the regional post-1997 change, with common support, two rain sources, a long-spell test, a later-period test and a paired placebo. This is a new diagnostic of the existing observations, not an independent flow data set or a physical attribution.

## Data and method

We use the shared CAMELS-AUS v2.03 sources in place. Full archive and used member hashes are in files/provenance.json. The shared paths are `/mnt/dell-data/shared_datasets/camels-aus-v2.03-zenodo14289037-` followed by `streamflow`, `hydrometeorology` and `mastertable`. The files are 03_streamflow.zip, 05_hydrometeorology.zip and CAMELS_AUS_Attributes_Indices_MasterTable.csv. Daily discharge is in mm/day. We use AGCD and SILO precipitation separately. Values below zero are missing. We use 1950 to initialise spell age and analyse 1951-2021.

The sample rule follows the source study: at least 15 calendar years in 1951-1996 and 10 in 1997-2021 with at least 95% valid flow. South means outlet latitude below -30 degrees; north is a geographic control. We retain recession pairs with 0 < Q(t+1) < Q(t) and rain below 1 mm on t-1, t and t+1. Age is the count of consecutive days with rain below 1 mm through t. Missing rain resets age. The main test needs age at least two days. The response y is log(Q(t)-Q(t+1)); x is log((Q(t)+Q(t+1))/2). This is a daily finite-difference diagnostic, not a direct store loss measurement.

For each catchment, reference flow quantiles define 20 bins. We cross these with six two-month seasons and ages 2, 3-4, 5-7, 8-14 and 15+ days. Values outside the reference flow range are excluded. Each supported cell needs at least five reference and five test days. A catchment also needs at least 100 reference and 100 test candidate days and 100 supported days in total. We report the fraction of in-range test days in supported cells. It is not the fraction of all calendar days.

We correct flow differences inside cells. A common slope b is fitted from x and y after each cell-by-era mean is removed. For each cell j, the effect is (mean y_test - mean y_ref) - b*(mean x_test - mean x_ref). Cell effects are weighted by supported test counts. Catchments have equal weight in the regional mean. To isolate age matching, the flow-and-season-only model is fitted to exactly the same supported days, with age groups combined. It has its own common within-cell slope. This holds data support fixed across the two models; it does not hold storage fixed.

The main reference is 1951-1996 and test is 1997-2021. The late test is 2010-2021 with the same reference; 1997-2009 is excluded from this fit. The long test uses age at least eight days in both eras. The placebo fits 1951-1980 and tests 1981-1996. Post-minus-placebo uses paired catchments, but different reference eras and day weights. It is a change of diagnostic contrasts, not a measurement of a 1997 physical step. The plan preceded calculations (files/PLAN.md). After the main results, we added paired long-minus-main and late-minus-main contrasts on common catchments (files/contrasts.py). No outcome-based catchment selection was used.

We sample whole outlet cells of 2 by 2 degrees with replacement, 9,999 times, and give percentile limits. These are conditional spatial intervals: they hold years, fitted slopes, support and source records fixed. They do not include temporal sampling uncertainty. AGCD and SILO are related products and are not two independent replications. The regional rate ratio is exp(mean catchment log effect), a geometric ratio. We do not average percent changes.

## Results

![Recession changes](files/results/recession.png)

The figure gives conditional spatial intervals. The last row subtracts the earlier placebo in common catchments; it has a different reference and must not be read as a direct post-era rate change. Main and restricted rows can have different catchments and supported flow distributions.

| Test | Rain | Catchments | Log change | Rate change and 95% limits | Median overlap |
| --- | --- | ---: | ---: | --- | ---: |
| main | AGCD | 348 | +0.0769 | +8.0% [+5.4, +10.7] | 65.6% |
| main | SILO | 348 | +0.0800 | +8.3% [+5.6, +11.3] | 65.6% |
| late | AGCD | 332 | +0.0224 | +2.3% [-0.7, +5.7] | 49.4% |
| late | SILO | 333 | +0.0248 | +2.5% [-0.4, +6.1] | 50.0% |
| long | AGCD | 313 | +0.0132 | +1.3% [-1.6, +4.2] | 52.8% |
| long | SILO | 311 | +0.0131 | +1.3% [-1.8, +4.7] | 52.5% |
| placebo | AGCD | 313 | -0.0179 | -1.8% [-6.2, +2.8] | 41.3% |
| placebo | SILO | 314 | -0.0217 | -2.1% [-6.5, +2.4] | 41.8% |
| main-placebo | AGCD | 313 | +0.0988 | +10.4% [+4.6, +17.8] | - |
| main-placebo | SILO | 314 | +0.1069 | +11.3% [+5.3, +19.1] | - |
| long-placebo | AGCD | 203 | +0.1004 | +10.6% [+5.9, +17.1] | - |
| long-placebo | SILO | 209 | +0.0909 | +9.5% [+4.6, +16.5] | - |
| bins10 | AGCD | 351 | +0.0915 | +9.6% [+6.8, +12.7] | 85.1% |
| bins10 | SILO | 351 | +0.0948 | +9.9% [+7.1, +13.2] | 85.1% |
| bins40 | AGCD | 337 | +0.0543 | +5.6% [+3.6, +7.6] | 33.0% |
| bins40 | SILO | 341 | +0.0583 | +6.0% [+3.9, +8.2] | 33.0% |

Main age matching changed the AGCD effect from +0.0864 to +0.0769 log units, a change of -0.0096 (-0.0121 to -0.0072). SILO gave -0.0082 (-0.0107 to -0.0059). Age matching removes a small part of the pooled increase on these supported days. It does not remove all of it. About 65.6% of in-range test days have support in the main test. With 40 flow bins, this falls to about 33%, and the estimated rise falls to 5.6-6.0%. Thus the sign holds across the planned bin checks, but the size and sampled domain depend on resolution.

The long-spell direct estimate is only about +1.3%, with intervals across zero. In 2010-2021 it is about +2.3 to +2.5%, also with intervals across zero. This does not prove zero change. The common-catchment post hoc contrasts confirm that catchment membership alone does not explain these smaller values. For AGCD, long-minus-main is -0.0656 log units (-0.0885 to -0.0470; 313 catchments), and late-minus-main is -0.0501 (-0.0653 to -0.0319; 332 catchments). SILO gives -0.0680 and -0.0495, with intervals below zero. Day support, flow distributions and the populations of rain-free states still differ, so these are diagnostic differences, not causal interaction estimates.

The placebo prevents a claim that the long-spell signal disappeared. Long spells already had a negative earlier contrast. After subtracting that contrast, the paired long-spell change is +0.1004 log units with AGCD (+0.0575 to +0.1583) and +0.0909 with SILO (+0.0447 to +0.1531). This subtraction is sensitive to reference era and has only 203-209 southern catchments. It is compatible with a change relative to an earlier slowdown even though the direct comparison with 1951-1996 is near zero.

Northern controls have slower recessions: main age-matched AGCD -0.1617 log units (-0.2311 to -0.1168), SILO -0.1536 (-0.2216 to -0.1095), with 152 catchments each. Their long and late estimates are also more negative than their pooled estimates. This shared direction of restriction effects cautions against assigning the southern contrasts to a unique new loss process.

## Meaning and limits

A changed dry-spell-age distribution cannot explain the entire pooled faster-recession result under this matching scheme. This strengthens a narrow observational signature from the prior study. It does not establish groundwater leakage, extra transpiration, pumping or a change in recharge. Long spells and the later period do not give clear direct increases, so the pooled result is insufficient evidence for a persistent 11% rise in slow-store drainage.

The 1 mm rain threshold can admit small input. Broad age classes leave age differences inside groups. A rain-free day can still have delayed recharge, snowmelt or a mixture of stores. Two-month seasons and one common flow slope are approximations. Fine bins change support, and positivity requirements remove flat and rising flow pairs. Flow quantisation, gauge rating changes, estimated flow and quality codes are not tested. The year-validity rule selects catchments, not individual years; valid daily pairs from other years remain eligible, as in the source method. Nested catchments and shared weather remain dependent despite spatial resampling. No multiple-test correction is made for the planned diagnostics or the exploratory paired contrasts. Later-era uncertainty is conditional on one realised climate sequence. The north is not a matched causal control.

We do not test the annual water budget, stream-connected groundwater storage, or the eastern US in this work. The cause of the runoff loss remains open. A useful next test would pair recession-day discharge with connected well levels and gauge rating audits, rather than equate flow with storage.

## Reproduce and inspect

All code uses Python 3.12, NumPy, pandas and matplotlib. Versions, seed and numerical audit are in files/results. No extra environment packages were installed. Raw data remain outside the signed publication.

With the shared inputs, run from the extracted publication directory:

```bash
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/prepare.py /mnt/dell-data/shared_datasets /absolute/path/to/separate-scratch
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py /absolute/path/to/separate-scratch /absolute/path/to/separate-output
python files/figures.py /absolute/path/to/separate-output
python files/contrasts.py /absolute/path/to/separate-output
python files/audit.py /absolute/path/to/separate-output
```

The first three commands rebuild the raw-data analysis and figure. The last two read the bundled catchment statistics to repeat the added contrasts and audit independently of external downloads. To retrieve the immutable inputs on another machine, run `python files/retrieve.py /absolute/path/to/external-inputs`, then use that directory in place of the shared root for prepare.py. The large hydrometeorology archive is read twice, once per used rain member. Compare regenerated member hashes with files/provenance.json. Daily scratch is about 167 MiB compressed; raw archive retrieval needs about 2 GiB. All source URLs and hashes are supplied; no private scratch is needed after publication.

The audit checks the estimator against an exact synthetic known effect and dummy-variable least squares, and independently checks all 100 reported mean statistics from the included catchment tables. It is a numerical audit, not a calibration of real-world confidence interval coverage. Included files also contain all 9,999 spatial samples per planned endpoint, catchment effects, overlap, counts, paired contrasts and the display figure.

Job: sci-1107-dell-earth-and-ocean-sciences-429e2c5d55c9. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, Codex in T3 Code. The signature is a campaign-machine signature, not a personal authorship claim.
