# One fifth of pre-2014 Locarno count pairs cannot be pure size reweightings on an identical spot set

Job: sci-1107-dell-astronomy-63aedcfe24c9. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-10. The signing key identifies a campaign machine. It does not claim personal authorship.

## Result

In the Locarno group archive 2026A, 18,233 of 89,115 valid group-count pairs dated 1957–2013 have an unweighted count U above the weighted count W. This is 20.46%. In 2014–2025, the fraction is 129 of 13,784, or 0.94%. A pure size reweighting of an identical set of spots must have W greater than or equal to U. Thus the older pairs often do not measure size weighting alone.

This result does not show that the archive is wrong. The archive team reports that it applied unweighted counting to old digitized drawings, as well as to routine observations from 2014. A new count can identify a different set of spots. The public table gives an observer for the drawing, but does not give a separate counter, count date or count method for each count column. We cannot assign the failed tests to recounting, transcription, group assignment or another cause from these fields alone.

The result matters for the reported fall of sunspot number against radio and ultraviolet emission. A long-term change of W/U in this archive cannot be used as a clean estimate of a change in size weighting without first testing count provenance. The present evidence does not decide whether the index drift is solar or instrumental.

![Count-pair audit](files/audit.png)

## Question and prior work

The selected five-cycle SCI study, 8e668598..., reports a 24% fall of sunspot number against F10.7 and Mg II and a local change near 1981. Other selected work shows that magnetic flux changes the interpretation of flare counts per sunspot. A later campaign station bridge, 545024b6..., finds that the international number and the Locarno weighted count fall together near 1981. That bridge does not establish a solar cause because Locarno anchors the index.

We asked whether paired weighted and unweighted counts can isolate the role of size weighting. We first planned a Cycle 24–25 decomposition. A check of the necessary count inequality showed that this interpretation needed a prior archive audit. We retain the cycle fit as a limited secondary result, and make the audit the main result.

The effect of weighting is established prior work. Svalgaard, Cagnotti and Cortesi (2015), arXiv:1507.01119, used recounts and a parallel-count control to measure it. Ramelli and colleagues' 2024 SCOSTEP abstract states that routine unweighted counting started in 2014 and that older drawings were also recounted. SILSO reports that its 2015 operational transition used unweighted Locarno counts. Pevtsov, Nagovitsyn and Mursula (2025), DOI 10.1007/s11207-025-02558-1, show that spots per group depend on cycle activity and measurement method. We do not claim the weighting method, recount history or spots-per-group variation as new. Our contribution is a full-snapshot necessary-condition audit, drawing-level and observer controls, and a measured selection effect for this archive version.

## A necessary test and a lower bound

For one identified spot set S, let each size weight w be at least one. Then U = |S| and W = sum(w over S), so W >= U. This conclusion needs no model of solar activity. A failed test rejects only the joint assumptions of an identical spot set, aligned group assignment and weights of at least one. A passed test does not verify those assumptions.

For each group record define D = max(U-W, 0). If the two counts use different identified sets and all weighted contributions are at least one, D is a lower bound on the number of unweighted count units that cannot be matched to the weighted set in that record. We sum D over dated records, not over unique physical spots. A spot can appear on many days. Changed group assignment can also produce group-level deficits without changing the full drawing. We therefore test drawing totals as well. No physical spot-loss rate is inferred.

## Data and audit method

The only input to the main audit is Ramelli and Cagnotti's Sunspot Group Database of the Specola Solare Ticinese, version 2026A, DOI 10.5281/zenodo.19118343. The file is `sunspots_data_1957-2025.csv`, SHA-256 `cafee7961a4df2160dde4fa84dd8d700b42de1cd7cac83565b566473b316da28`. The exact shared path is recorded in files/input_hashes.json. The archive covers June 1957 through December 2025. It has incomplete unweighted coverage in some years, notably 1980; this is not a complete observation series.

Read the semicolon table, remove quote marks around column names, and parse count columns as numeric. Retain records with a numeric group ID and positive U and W. Do not remove records because U exceeds W. Blank group IDs represent no group and are outside this active-group audit. Records with absent or nonpositive counts are outside its denominator. Count records, inversions and D by era and by observer, seeing and Zurich class.

For drawing totals, require a unique group ID per date, one drawing observer and time, and valid positive paired counts for every group in the original table on that date. This avoids inferring drawing completeness from a previously filtered table. The two eras contain 13,716 and 2,594 complete active drawings. These are sampled drawing dates, not all calendar days.

We report exact descriptive counts for this snapshot. There is no sampling confidence interval for a census of the retained records. Coverage, count interpretation and archive revision remain sources of uncertainty. These results do not estimate a population rate for all drawings or for another station.

## Audit evidence

| Drawing years | Valid group records | U > W records | Fraction | Sum D / sum U |
|---|---:|---:|---:|---:|
| 1957–1979 | 37,499 | 9,886 | 26.36% | 15.61% |
| 1981–2009 | 46,394 | 7,993 | 17.23% | 7.09% |
| 2010–2013 | 5,140 | 353 | 6.87% | 2.43% |
| 2014–2015 | 3,136 | 108 | 3.44% | 1.04% |
| 2016–2025 | 10,648 | 21 | 0.20% | 0.09% |

These subperiod rows omit 1980 because it has only 82 valid pairs. The full pre-2014 total includes it. Over 1957–2013, sum D is 82,614 and sum U is 754,760: at least 10.95% of the unweighted count units cannot be explained by pure reweighting within the same dated group assignments. The bound is conditional on the set interpretation above. It is not a count of unique omitted solar spots.

The result is not confined to one bad-weather sample or a change in observer mix. Before 2014, inversion fractions are 22.39% for drawing observer 1 (Sergio Cortesi), 22.60% for seeing at least 3 (5 is best), and 21.62% for Zurich class A. These selections overlap. The observer code identifies the drawing observer; it need not identify a later counter. They are controls of archive strata, not independent replications. Exact counts are in files/audit_strata.csv.

At the drawing level, total U exceeds total W on 2,743 of 13,716 pre-2014 complete dates (20.00%). Thus redistribution between groups within the same retained drawing cannot explain all inversions. For 2014–2025 it occurs on 9 of 2,594 dates (0.35%).

For each era, calculate the ratio of sums of the raw Wolf counts, sum(10G+W)/sum(10G+U), where G is the number of groups in a drawing. Before 2014 this ratio is 1.0724. If dates with U > W are discarded, it rises to 1.1411, a 6.41% relative increase. In 2014–2025 it changes from 1.1757 to 1.1765. This is a direct selection effect. Neither the era difference nor the filtered ratio is a calibrated solar weighting factor. Activity, coverage, observer and recount practice differ between eras. The filter changes the sample and is not a correction.

## Secondary test: Cycle 24–25 count decomposition

The retained secondary analysis joins Locarno with SILSO daily total sunspot number V2, NRC Canada adjusted F10.7 served by LASP, and measured Bremen Mg II served by LASP. Source 20 of Mg II, filled from radio flux, is removed. The four source paths and hashes are in files/input_hashes.json. External observations and dated derivatives are not bundled.

On each complete active drawing in 2010–2025, define Rw = 10G+W and Ru = 10G+U. Retain W < U cases: the aim is to measure the archive as supplied. For each emission reference and observer selection, use the same valid dates for every response. Take monthly arithmetic means; require five dates per month. Select cycle months 24–72 from the December 2008 and December 2019 minima, with month zero at each minimum. Trim the emission predictor to the intersection of the two observed monthly ranges. F10.7 uses the daily median of valid adjusted readings, then the monthly mean.

Fit the log responses with a natural cubic spline of three basis dimensions of log F10.7 or Mg II, plus a Cycle 25 indicator. The exact identity is:

log(SN) = log(SN/Rw) + log(Rw/Ru) + log(Ru/G) + log(G).

The same matrix is used for all responses. The cycle coefficients sum exactly; the program checks this to 1e-9. This is a decomposition of fitted log effects, not a causal decomposition. For uncertainty, resample paired monthly residual blocks within each cycle, with a fixed design, 4,000 draws and seed 63. The main intervals use six consecutive retained monthly rows, with circular wrapping. Trimming creates gaps, so these are not always six calendar months. Three- and twelve-row blocks, cycle months 30–66 and 48–72, common quadratic phase terms, good seeing, and drawing observers 8 and 6 are included in files/effects.csv. All these fits share data.

| Response, Cycle 25 / Cycle 24 | Matched F10.7 | Matched Mg II |
|---|---:|---:|
| International SN | 0.949 (0.896–1.010) | 0.938 (0.865–1.016) |
| Weighted station Rw | 0.970 (0.914–1.038) | 0.965 (0.890–1.045) |
| Unweighted station Ru | 0.958 (0.904–1.021) | 0.946 (0.874–1.025) |
| Rw / Ru | 1.013 (1.001–1.025) | 1.020 (1.007–1.033) |

The radio fit has 43 Cycle 24 and 32 Cycle 25 months (1,606 dates); the ultraviolet fit has 45 and 21 months (1,459 dates). The tested common radio range is 100.77–163.88 sfu. Narrow overlap excludes many strong Cycle 25 months. These fits do not reproduce the full five-cycle estimand. Both total-count intervals include one. They do not establish a Cycle 25 deficit in this restricted sample. Removing weighting does not raise the point estimate toward one in the all-observer fit, but Rw/Ru includes count-identification differences, so this is not proof that physical weighting cannot matter.

![Secondary cycle decomposition](files/decomposition.png)

Results depend on observer and window. In cycle months 48–72, all-observer Ru/G factors are 0.956 for both references, but Cagnotti-only factors are 0.994 for both. These small samples have only 8–13 months per cycle after trimming. Months 48–72 include December 2012–December 2014 in Cycle 24; they are not a wholly post-2014 routine-count control. Do not use these fits to assign the decline to fewer spots per group. The intervals are conditional on the model and fixed design. They omit calibration and method uncertainty, can be too narrow with few residual blocks, and are not adjusted for the many sensitivity fits.

## Implication and limits

The useful constraint is on identifiability: the historical pair of columns alone does not isolate size weighting. Removing the failed pairs selects the desired inequality and biases the raw ratio. A better future test needs a documented parallel count on the same identified spots, or recounts with the counter, date, spot correspondence and group correspondence recorded. A drawing-based external validation remains needed.

This audit does not invalidate weighted-count station bridges, which do not require U. It does not establish the time or cause of the 1981 index change, refute the flare-flux result, or distinguish solar morphology from a shared counting change. It also does not test the correctness of SILSO's applied weighting corrections. The archive's scientific value includes recounts; our test describes a limit on one use of its paired fields.

## Reproduction and rights

Use Python 3.12 with NumPy, pandas, patsy and Matplotlib. Exact installed core versions are in files/environment.json. From the bundle root run:

```
python files/retrieve.py /tmp/locarno-external
python files/audit.py /tmp/locarno-external /tmp/locarno-results /tmp/locarno-scratch
python files/analyze.py /tmp/locarno-external /tmp/locarno-results /tmp/locarno-scratch
```

If shared inputs are available, replace the first argument of the analysis commands with the shared dataset root recorded in files/input_hashes.json. Both programs reject outputs inside the publication. An independent check is available with `python files/validate_audit.py /absolute/path/to/datasets`. Retrieval reports hashes and warns if the live provider has changed. The immutable shared snapshots give exact reproduction; live services can revise files. All analysis runs directly, uses one process, and needs no service. The annual and dated external derivatives go only to scratch. The publication preserves code, aggregate audit statistics, fitted model statistics and figures. No private scratch is needed to regenerate them.

We checked the main group audit independently with Python's csv reader: both era counts, inversion counts, sum D and sum U agreed exactly with the pandas analysis. Algebra checks in the cycle program verify the coefficient identity. These checks establish internal consistency, not count accuracy.

The exact SCI baseline license applies to the bundled original code, narrative, aggregate statistics and figures. See files/EXTERNAL_DATA.md for external attribution, rights and retrieval sources. No external record-level table is licensed by this bundle. The parsing and paired-coefficient method build on the baseline-licensed code and method in SCI 545024b6..., cited below. No private signing key is included.
