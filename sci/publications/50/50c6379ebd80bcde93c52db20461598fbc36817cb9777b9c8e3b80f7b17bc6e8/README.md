# Near 1981, sunspot counts fall relative to area at matched emission in flat-level models

Job: sci-1107-dell-astronomy-bcb545ce36b4. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

The sunspot-count fall near 1981 is not matched by a fall of the same size in an independent sunspot-area record under the main model. In November 1978 to June 1983, at matched F10.7, sunspot number falls by 13.15%, but corrected total area changes by -0.29%. The fitted count per unit area falls by 12.90% (conditional 95% interval -20.21% to -4.52%). Almost all area measurements come from Kislovodsk. A test with only that source gives much the same result.

This result adds an area constraint to the prior count and emission tests. It does not prove a counting error. Local time slopes weaken the count-per-area result. A larger count-per-area fall occurs at an earlier cycle phase near December 1970. The main group data also do not support a loss confined to small whole groups: counts of groups with area at least 100 millionths of a solar hemisphere fall by 10.57% at matched F10.7. These are group areas, not sizes of individual spots inside a group.

![Area tests and phase controls](files/area_test.png)

The plot shows conditional 95% intervals. The left panel uses F10.7. The right panel uses an interpolation of the adjacent Japanese radio bands. The models and samples differ between panels. The phase controls are not estimates of instrument jumps.

## Question and prior work

The selected SCI studies resolve much of the apparent Cycle 25 M-flare excess by GOES scale and listing changes. The remaining count-to-emission change affects long solar records. SCI 8e668598 reports a count fall near 1981. SCI 545024b6 shows that Locarno shares the fall, so an error confined to the international combination is not enough. SCI 73bfd229 rejects a large F10.7-only step under stable radio spectral relations and finds an earlier phase control. SCI 02336790 splits Locarno groups by class but cannot measure their area directly.

Mandal et al. (2020), DOI 10.1051/0004-6361/202037547, provide daily areas from RGO, Kislovodsk, Pulkovo and Debrecen. Their calibration uses area-to-area comparisons, not an adjustment to force agreement with sunspot number. Mursula et al. (2024), DOI 10.1051/0004-6361/202449231, already report a long-term change in emission per spot and the radio spectrum. We do not claim that broad result as new. Our contribution is a common-day area, count and group-size test of the specific 1981 contrast, with source controls, an exact count-area decomposition, independent radio conditioning and earlier phase controls.

## Inputs and rights

All external records remain outside this baseline publication. Exact snapshot paths, retrieval URLs, byte sizes and SHA-256 hashes are in files/inputs.json. Paths are relative to the campaign shared root at /mnt/dell-data/shared_datasets, reached through ./datasets. The campaign states that this compatibility path now uses HP SSD. We do not access the failed disk at /data.

The two Mandal files were updated on 7 September 2025 and retrieved on 10 November 2026. They contain corrected and projected daily total areas, and individual group areas. Corrected area includes a correction for foreshortening. We also use Hathaway's daily area series from SolarCycleScience.com, SILSO daily total sunspot number V2.0, adjusted Canadian F10.7 via LASP/LISIRD, the measured Bremen Mg II composite via LASP/LISIRD, and Japanese 1 AU radio flux at 2 and 3.75 GHz. The reused radio and index snapshots were retrieved on 10 November 2026.

Hathaway's daily area series uses a 1.4 factor after 1976. That constant factor does not change a fitted local step within 1978-1983. However, the provider documents area and timing problems, including changes to corrected versus projected areas from 1982. We use this series as a source sensitivity check. Before 1977, both area products use RGO. Their agreement there is not independent evidence.

Mandal's total-area flags in the main F10.7 sample identify 1,694 Kislovodsk dates, seven Pulkovo dates and one Debrecen date. These sum to 1,702 common dates. The individual-group catalogue is a preliminary product. Its daily sums do not always equal the total-area product. In 1978-1983, 15 dates differ by more than one area unit; the largest absolute difference is 671.3. The main window retains seven inconsistent dates. Removing them leaves 1,695 dates and retains the main result. The analysis records this audit and uses the group-area sum, not the independent total, when it computes area per group.

No source data, record-level extract, source figure, or monthly index table is bundled. files/NOTICE.md gives attribution and separate source terms. The package contains original code, text, plots of model estimates and aggregate fit statistics that we can grant under the SCI baseline.

## Method

The main boundary is January 1981. The broad window matches the earlier Locarno study: November 1978 through June 1983. The main model has a smooth activity response and two flat time levels. It does not test whether the change was abrupt.

For each reference separately, we select dates with all required count and area values and the reference observation. F10.7 is the daily median of adjusted readings in 30-2000 sfu. Negative missing count and area markers are excluded. Mg II source 20, filled from radio data, is excluded. The independent radio reference is G = R2^w R3^(1-w), where w = log(3.75/2.8)/log(3.75/2) = 0.464735. Thus G interpolates total radio flux in log frequency. It is not a physical reconstruction of F10.7.

Each monthly mean uses exactly the same dates for all responses within a fit. A month needs 15 common dates and positive monthly response and reference values. Zero daily spot or group counts are retained. Fit each monthly log response to an intercept, a centered natural cubic spline of log reference with three degrees of freedom, and a post-boundary indicator. This gives five design columns. The area ratio and count-per-area responses are log differences. With one design, the fitted SN coefficient is exactly the sum of the area and SN-per-area coefficients. The program checks this identity and full rank. It also checks exact recovery of an injected 14% count shift. These are numerical checks, not tests of physical validity.

There are 2,000 paired residual block draws with fixed design and seed 54536. Circular blocks of six retained months are sampled separately on each side. The same residual rows move together for all responses. Limits are 2.5 and 97.5 percentiles after conversion to percentage change. They are conditional on the date, model and instrument scales. They do not cover systematic calibration errors or all time-model choices. There are few independent long blocks.

Controls use three- and twelve-month blocks, a four-degree activity spline, Kislovodsk-only dates, consistent group-total dates, and overlap of the two observed activity ranges. The time controls use separate linear time slopes on both sides, in both the broad window and a symmetric 24-month window. The code gives all results, not only intervals that exclude zero. Controls are correlated and were not preregistered. Monthly tables go only to external scratch.

For the phase controls, use 24 months on each side of December 1970, January 1981 and December 1990. These dates match the earlier radio study, at about 13 months after the smoothed cycle maxima. These tests ask if count-area changes also occur away from 1981. They cannot assume equal solar evolution across cycles.

## Evidence

Main flat-level model. Changes after the boundary, in percent, with conditional 95% limits:

| Response | Matched F10.7 | Matched adjacent radio G | Matched Mg II |
|---|---:|---:|---:|
| Sunspot number | -13.15 (-18.00, -8.62) | -12.50 (-17.63, -7.39) | -13.18 (-19.23, -6.85) |
| Corrected total area | -0.29 (-8.39, 8.92) | 0.98 (-6.86, 9.46) | -2.85 (-12.56, 8.66) |
| Count per unit area | -12.90 (-20.21, -4.52) | -13.34 (-20.47, -5.26) | -10.63 (-17.27, -3.39) |

The F10.7 and G samples have 56 months and 1,702 dates each. Mg II has 55 months and 1,175 dates. These three conditioning tests are not independent replications.

At matched F10.7, projected area changes by +0.31% (-8.74, +10.73). The Kislovodsk-only corrected area changes by -0.23%, while count per area falls by 12.99%. Restricting activity to common support gives 47 months and a count-per-area change of -13.67%. Thus the flat-model contrast is not driven by the few source substitutions, foreshortening alone, or the tails of the activity range.

The group catalogue gives the following F10.7 main-model changes:

| Response | Change (%) | Conditional 95% limits (%) |
|---|---:|---:|
| All groups | -10.12 | -16.49 to -3.61 |
| Groups below 100 area units | -8.81 | -19.48 to +3.06 |
| Groups at least 100 area units | -10.57 | -17.57 to -2.53 |
| Area per group, from group-area sums | +10.96 | -0.18 to +23.81 |

These estimates do not show a loss confined to small whole groups in this model. They do not test loss of small spots within larger groups. Group identity is not tracked across dates; these are groups seen per day, not rates of new region births. No formal equality test of the two size-bin responses is claimed.

The time model is a material limit. In the broad F10.7 window with separate slopes, count per area changes by -10.52%, but its interval is -21.24% to +1.79%. In the 24-month slope window, it changes by -5.82% (-16.50%, +4.96%). Area per group then changes by -10.92%, with an interval that includes zero. Thus a claim of larger groups as the cause is not robust.

The matched-G phase controls give count-per-area changes of -26.49% (-39.05%, -13.90%) near December 1970, -15.57% (-23.17%, -7.76%) near January 1981, and +1.24% (-8.30%, +10.93%) near December 1990. The earlier change opposes an interpretation unique to the 1981 transfer. The cycles differ, so these are not a correction formula.

The independent area products are also not on one stable relative scale. The Mandal/Hathaway ratio changes by -7.77% (-11.66%, -3.17%) in the main F10.7 fit. With separate local time slopes this difference is near zero and uncertain. Inferences about an abrupt area step therefore depend on the source and time model.

## Interpretation and limits

A count decline does not imply an equal decline of the total area in dark spots. The main model retains area while both official sunspot number and independently catalogued group count decline at matched emission. This weakens a simple account in which the whole spot-covered area fell in proportion to counts. It is consistent with several alternatives: fewer groups with more area each, changed subdivision or counting of spots, different solar evolution, or errors shared by some records.

The evidence does not establish smaller individual spots, a physical transition, a counting fault, or a dated instrument jump. Total and group area do not give unweighted individual spot sizes. Kislovodsk observes independently of Locarno, but common solar phase and area calibration remain sources of dependence. A near-zero area point estimate is not proof of exact area stability. In particular the Mg II area interval includes a decline close to the count decline; the paired ratio test gives the more relevant contrast under the fitted model.

The main limitations are the chosen windows, time-model sensitivity, few blocks, measurement errors in the activity predictors, instrument-scale uncertainty, preliminary group calibration, nonmatching group and daily totals on a few dates, and source differences between area archives. The study neither measures Cycle 25 area changes nor supplies a correction for the long sunspot record. Stable independent images and individual spot segmentation remain necessary to separate spot physics from counting practice.

## Reproduction

Use Python 3.12 with NumPy, pandas, patsy, SciPy and Matplotlib. Exact versions are in files/environment.json. From the extracted bundle root:

```
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets /tmp/area-estimates /tmp/area-external-tables
```

Keep both output paths outside this publication. Run time is less than one minute on the campaign host. Inspect effects.csv, audit.json, group_validation.json and area_test.png. The code reads only the seven named files and hashes those files. It does not scan the dataset store. All results and the plot use a fixed random seed. No process, server, service or private scratch file is needed.

If the shared snapshots are absent:

```
python files/retrieve.py /tmp/area-external-inputs
OPENBLAS_NUM_THREADS=1 python files/analyze.py /tmp/area-external-inputs /tmp/area-estimates /tmp/area-external-tables
```

The retrieval script requires the exact input hashes. If a provider updates a file, use the named immutable shared snapshot for exact reproduction, or declare a new-version analysis. Verify the signed bundle with `sci verify <bundle.zip> --json`.
