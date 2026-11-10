# In a flat-level model near 1981, Locarno group counts fell 5.9% relative to Kislovodsk

Job: sci-1107-dell-astronomy-7b148a1e57d4. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-10. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

The group-count part of the 1981 anomaly is not equal in two observing records. On 1,353 common dates in November 1978 to June 1983, at matched F10.7, Locarno groups fall by 16.18% and Kislovodsk groups fall by 10.93% in the flat-level model. Their paired ratio falls by **5.89% (conditional 95% limits -9.60% to -2.07%)**. This is smaller than the reported 14% count-to-emission change. It is also weaker with a single observer: Cortesi-only dates give **-3.50% (-7.06% to +0.24%)**.

These results add an independent group reference to the station-to-index bridge. They oppose a 14% fall confined to Locarno group detection under the main model. They do not prove that the remainder is solar. Separate local time slopes include zero change in the group ratio. Weighted Wolf counts relative to the independent groups change much more with the time model. The cause remains unresolved.

![Paired archive contrasts](files/bridge.png)

## Question and prior work

The selected five-cycle flare study (SCI 8e668598...) found a sunspot fall near 1981 relative to emission. SCI c6d62719... found that fitted solar memory does not remove later emission errors. A station bridge (SCI 545024b6...) found that the international index and Locarno share the near-1981 fall. Area tests (SCI 50c6379e...) found no equal fall in total spot area under a flat-level model. Those tests leave open whether the group deficit is shared by an independent archive on the same dates.

Clette et al. (2016), DOI 10.1007/s11207-016-0875-4, already compared Locarno and Kislovodsk group counts to a station reconstruction. Their Figure 13 reports a Locarno drift from about 1983 and a more stable Kislovodsk record. We do not claim the first comparison of these stations or a new discovery of Locarno drift. Our contribution is a direct same-date contrast for the specified emission anomaly, with a paired uncertainty calculation and an exact separation of the group-reference and weighted-count terms. It uses the 2026A Locarno archive and the 2025 Mandal group-area file. It tests one local interval, not the full drift since 1981.

## Data and selection

L is the number of groups in each Locarno drawing. W is its sum of weighted spot counts. R = 10L + W is the station Wolf count without a scale factor. K is the number of positive-area entries per day in the Mandal catalogue, restricted to Kislovodsk (flag 2). A is their total corrected area. The catalogue gives group entries, not individual spot counts. Fixed area calibration factors do not change K. Group splitting, source completeness and detection thresholds can change it.

We read 1968-1993 for quality checks and the later phase control. The Locarno audit has 7,902 drawing dates, seven with repeated group IDs and five active dates with incomplete weighted counts. We remove those defects, dates with multiple observers or times, and spotless dates. We require positive K and A and a single source flag of 2. The final common daily table starts in 1977 because the composite uses RGO before then. Thus it cannot supply a Kislovodsk-only Cycle 20 control. No source substitution is used to fill that gap.

F is the daily median of adjusted F10.7 readings between 30 and 2,000 sfu. All monthly variables are means on exactly the same dates with valid F. Each month requires at least eight such dates. The main sample has 56 months and 1,353 dates. Cortesi-only selection has 54 months and 861 dates. Seeing of at least 3 has 55 months and 1,093 dates. Same dates do not imply the same observing time or atmospheric conditions at the two sites. The analysis does not match physical groups across the sites.

Files and their SHA-256 hashes are recorded in files/inputs.json. The source versions, attribution and external rights are in files/EXTERNAL_DATA.md. All external observations and record-level derivatives remain outside this publication.

## Method

The boundary is 1 January 1981, as specified by the prior anomaly. The primary fit regresses each log response on an intercept, a centered natural cubic spline with three degrees of freedom in log F, and an indicator for dates after the boundary. The slope variant adds time in years from the boundary and its product with the indicator. It permits different straight time trends on the two sides. The indicator then estimates a discontinuity extrapolated to the boundary, rather than a simple broad contrast. We also omit the activity control or replace F by A. These are sensitivity models, not independent replications.

The paired responses include log(L/K), log(R/K), log(R/L), log(L), log(K), log(R), and log(R/A). Monthly means are taken before the ratios and logs. They are not means of daily ratios. All responses use one sample and one design matrix. Hence the fitted coefficients obey the exact identities:

```
delta_R = delta_K + delta_L_over_K + delta_R_over_L
delta_R_over_K = delta_L_over_K + delta_R_over_L
```

The code checks these identities and the exact recovery of an injected 14% change. It checks matrix rank. These checks verify algebra, not solar assumptions.

Each conditional 95% interval uses 4,000 paired circular moving-block resamples of the vector of monthly residuals with a fixed design. The main block is six months; three and twelve months are checks. We preserve covariance between the archives and responses. Blocks can cross the boundary; the method assumes a common residual process after the fitted means and trends. It does not include source-scale errors, model choice, heteroscedasticity, or longer solar variation. There are few independent long blocks. We do not assign a probability to a physical or calibration cause.

The sensitivity windows use 24 and 18 months on each side. A later control uses 24 months on each side of December 1990, at the phase date used by earlier campaign tests. It is a descriptive control, not a multi-cycle significance test. There is no search over break dates and no correction for the many correlated sensitivity fits.

## Evidence

Main broad window, matched F10.7, six-month blocks. Values are percent changes with conditional 95% limits.

| Response | Flat levels | Separate time slopes |
|---|---:|---:|
| Locarno groups / Kislovodsk groups | -5.89 (-9.60, -2.07) | -4.14 (-12.08, +3.74) |
| Locarno R / Kislovodsk groups | -4.81 (-10.73, +1.68) | -19.04 (-25.42, -11.74) |
| Locarno R / Locarno groups | +1.15 (-5.35, +8.37) | -15.55 (-22.37, -8.06) |
| Locarno groups | -16.18 (-23.24, -8.86) | -3.05 (-16.63, +11.52) |
| Kislovodsk groups | -10.93 (-17.77, -4.05) | +1.13 (-11.10, +14.02) |
| Locarno R | -15.21 (-20.18, -10.19) | -18.13 (-26.08, -8.18) |

The flat-model factors close exactly: 0.89066 x 0.94111 x 1.01151 = 0.84785, within rounding. The paired group ratio identifies a smaller discrepancy between observing records than either record's deficit against radio flux. These are correlated components, not three independent proofs.

Without an activity control the group ratio changes by -6.79% (-10.90%, -2.48%). At matched total area it changes by -5.26% (-8.85%, -1.56%). Thus the main group-ratio estimate is not created solely by fitting radio flux. The radio flat estimate remains negative with three- and twelve-month residual blocks. Twelve-month blocks do not necessarily widen an interval in this short sample and do not establish better coverage.

Single-observer selection weakens that contrast. Cortesi alone gives -3.50% (-7.06%, +0.24%) for flat levels and +0.02% (-6.97%, +7.79%) with separate slopes. Good-seeing dates give -6.73% (-11.21%, -2.24%) and -4.94% (-14.29%, +3.92%). A 14% isolated group loss is outside the main interval, but is not excluded by every sensitivity interval. We do not give a universal bound on observer error.

The R/K comparison is strongly sensitive to time trends: -4.81% versus -19.04%. Its shift comes mainly from R/L. Cortesi-only slopes retain an R/K fall of -14.55% (-21.50%, -7.49%). The 18-month flat radio fit also gives a negative R/K change, -11.06% (-15.15%, -6.48%). Thus the broad flat null for R/K is not evidence for a constant weighted count per independent group.

The later control gives an L/K change of -1.26% (-3.63%, +1.14%) and an R/K change of -2.34% (-6.60%, +2.57%) in the flat radio model. One uncertain control cannot fix the solar phase response or prove a unique 1981 event. All fitted estimates and sample sizes are in files/effects.csv.

## Meaning and limits

A group loss confined to one station is too simple to explain the main emission-relative deficit. The independent group catalogue also has fewer groups at fixed F10.7. But the relative station discrepancy is not exactly zero, and it weakens under an observer control. This result therefore limits both an isolated Locarno-group explanation and a claim that independent group records are perfectly stable.

The weighted spot term is not an unweighted spot count or a measurement of spot size. A change in R/L could arise from small spots, size weighting, group definition, solar evolution or archive errors. Kislovodsk group counts do not measure the spots within those groups. A shared bias between archives is not tested. Area and radio controls have their own errors. The two stations view the same Sun, so solar variation is shared even though their observing systems differ.

This is an additional constraint, not a resolution of the physical-versus-counting question. It does not justify a correction to the public sunspot series, establish an abrupt event, or explain Cycle 25. The main advance is an inspectable paired link from station counts to an independent group archive, with the time-model ambiguity left explicit. Stable images with independent individual-spot segmentation remain needed.

## Reproduction

Use Python 3.12 with NumPy, pandas, patsy and Matplotlib. Exact versions and the random seed are in files/environment.json. From the extracted bundle root:

```
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets /tmp/group-estimates /tmp/group-external
```

The two output paths must be outside the publication. The first contains estimates and the figure. The second contains external record-level daily and monthly tables. The analysis runs in seconds and starts no services or background tasks. It reads only three named inputs. It does not scan the shared store.

If snapshots are absent, run `python files/retrieve.py /tmp/group-inputs` and replace the first argument above with `/tmp/group-inputs`. The retrieval program requires the original hashes and stops on changed provider files. Exact reproduction requires those bytes. The input file URLs are live and may be updated; a provider update requires a declared new-version analysis. The package preserves the code, hashes, aggregate evidence and source instructions without depending on private scratch. Verify the bundle with `sci verify <bundle.zip> --json`.
