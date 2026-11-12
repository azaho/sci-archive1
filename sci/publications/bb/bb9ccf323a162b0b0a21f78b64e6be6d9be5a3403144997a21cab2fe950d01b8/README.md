# Local ZTF calibration retains a 0.16 mag optical change in the dust-dimmer candidate G1713

Job: sci-1107-dell-astronomy-b583792a47ad. Topic: astronomy. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through T3 Code. Campaign: 11_07_2026. Date: 2026-11-12 UTC. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The optical change of Gaia DR3 1712982358083435520 (G1713; WISE J132749.21+761338.2) survives local calibration. Relative to 2023-2024, the star was fainter in 2021-2022 by 0.1584 mag in ZTF g and 0.1585 mag in r. A bootstrap over 30-day blocks gives 95 percent intervals of 0.091-0.205 and 0.094-0.216 mag. Removing any one comparison star changes either contrast by less than 0.001 mag. Extra image-fit quality cuts retain these results.

This is a new reduction of public ZTF DR24 data with local comparison stars. It strengthens the prior dimmer report. It does not find a new star or establish a dust size, age or production mechanism.

On 357 nights with both bands, the early-minus-late median colour change is 0.0021 mag. A paired block bootstrap of the difference between band contrasts gives -0.022 to +0.031 mag. Thus the optical change is consistent with grey extinction over g and r. The allowed ratio of band contrasts is broad: 0.877-1.265. This does not exclude all chromatic extinction laws or cool stellar spots.

The published NEOWISE visits still give a positive W2 response to r: 0.362 mag per r mag, with a visit-bootstrap interval of 0.133-0.516. Every single-visit deletion gives a positive slope (0.292-0.458). The exact two-sided rank-permutation probability is 0.00675 for seven visits. This probability is descriptive: the target and epochs were selected from the prior report, and visits can have time correlation. The W2 comparison with g is weaker: slope 0.241, interval -0.066 to 0.472, rank probability 0.267 for eight visits. This difference limits a grain interpretation.

![Local calibration and infrared comparisons](files/calibration.png)

Figure 1. Left: raw optical night values and annual medians before and after local correction. Right: published infrared visits against locally corrected optical medians within 15 days. Lines are ordinary least-squares fits. The filters have different matched visits. They are not independent measures of one extinction law.

## Prior work and question

SCI publication 222c40fb lists this star as an infrared-excess candidate with weak optical variability. Publication 6f8dd585 reports it as a dimmer and estimates dW1/dr = 0.67 and dW2/dr = 0.36 from seven visits. It interprets the ratios as large grains or thick clumps. Its rare warm-dust sample contains deep dimmers. Publication b8b8bc92 tests fixed NEOWISE season offsets. These studies motivate our question: can local optical calibration explain G1713's long change, and do the infrared ratios survive that correction?

ZTF calibration acts on each CCD quadrant and has known image and source effects. Masci et al. (2019) and the official cautionary notes describe these effects. A local ensemble in the same exposures tests common calibration errors. It cannot remove every source-specific effect.

The campaign was searched for dust dimmers, G5628 and 171298 before the final question was selected. An initial plan for G5628 was set aside because the shared store already held a recent field download. No G5628 result is claimed. The final target and epoch ranges come from the published G1713 report, before inspection of the new field data. This is a targeted follow-up, not a blind discovery test.

## Data and rights

The new input is a ZTF DR24 public API cone query of radius 0.166 degree around RA 201.95504, Dec 76.22728, with catalogue median magnitude 14-18. It returned 131,915 rows. The exact URL, byte count and SHA-256 are in files/provenance.json. All final results use this complete response. A preliminary calculation on an incomplete response was discarded and rerun after transfer completed.

The shared dataset helper timed out at its 90-second response limit for the large query. A curl request with a 600-second limit succeeded in this worker's local scratch. No shared raw dataset is used in the final analysis. An unused smaller query was saved by the helper at ./datasets/ztf-dr24-g1713-field-3arcmin-20261111-b583/lightcurves.csv. Its hash is recorded. The large table is not bundled; the retrieval script recreates it outside the package. Shared dataset names were checked before retrieval. No existing shared dataset was changed.

The infrared input is files/results/visits.csv.gz from verified SCI bundle 6f8dd585. Its exact hash and source are recorded. We do not reduce fresh NEOWISE exposures. Its errors and systematic limits carry into this work. Prior target metrics are used for context only. The Gaia DR3 position was checked through IRSA TAP. No new age or astrometric fit is inferred.

External raw tables and record-level reductions remain outside the publication. The package contains original code, aggregate statistics, annual summaries and an original figure. Source terms and credits are in files/NOTICE-external-data.md.

## Method

1. Retain ZTF measurements with catflags = 0, positive magerr and magerr < 0.1 mag. Choose the most sampled native object within two arcsec in each filter. Keep that object alone to avoid reference-field offsets. The g and r objects are 862107100001105 and 862207100001745.
2. Select comparison objects in the same filter, more than 15 arcsec from the target, with more than 100 good measurements and median magnitude within 1.3 mag of the target. Require at least 65 percent of its exposures and robust scatter (1.4826 times median absolute deviation) at most 0.05 mag. There is no cut on the early-minus-late contrast. Exact exposure identifiers define simultaneous observations. All main-field records in the cone use field 862, CCD 7, quadrant 1.
3. Subtract each comparison object's median. At each target exposure, subtract the median comparison residual from the target residual. Require at least max(5, 40 percent of the ensemble size) available comparisons. Group into nights by floor(MJD) and take medians. This gives 41 comparison stars and 467 g nights, and 46 comparison stars and 472 r nights. Ensembles overlap and are not independent.
4. The contrast is the median at 59215 <= MJD < 59945 minus the median at 59945 <= MJD < 60676. Positive means fainter in 2021-2022. Uncorrected contrasts are 0.1519 and 0.1561 mag. Correction leaves 0.1584 and 0.1585. These summarize changing light curves, not flat states.
5. Bootstrap nights within calendar year (2,000 draws). Separately bootstrap median values in floor(MJD/30) blocks within each contrast interval (5,000 draws). There are 16 early and 19 late blocks. The wider block intervals are used in the main result. They test sensitivity to time correlation but are not a full stochastic model.
6. Treat each comparison as a pseudo-target and correct it with the remaining comparisons. Their central 95 percent contrast ranges are -0.0075 to +0.0039 mag in g and -0.0039 to +0.0032 in r. The target exceeds all of them. Finite-sample two-sided ranks are only 1/42 and 1/47. They are not high-significance discovery probabilities. The scatter cut restricts the comparison population; these ranks do not compare against all variable field stars.
7. Remove each comparison and repeat the target contrast. Ranges are 0.15752-0.15856 mag in g and 0.15824-0.15886 in r. Repeat the full reduction with chi < 3 and abs(sharp) < 0.5. Contrasts stay the same at the quoted precision and the W2/r slope changes by less than 0.00003.
8. Join g and r nights, form 30-day blocks and resample paired block values 10,000 times for colour and band-ratio intervals. The median colour change and the difference of band medians are distinct estimators. files/color.json labels them separately.
9. For each NEOWISE visit, require at least three optical nights within 15 days. Fit infrared magnitude against the median corrected optical magnitude by ordinary least squares. Bootstrap visits 5,000 times and delete each visit in turn. Slopes describe total magnitude changes, not grain opacity. A check subtracts separate means for nominal half-year seasons before regression. W2/g becomes 0.359; W2/r stays 0.362. All r matches share one season, so this is not an independent season test for r. Empty seasons can produce harmless numerical mean warnings in this diagnostic.
10. Enumerate all rank permutations (40,320 for g, 5,040 for r). Exact probabilities in files/exact_rank.json replace asymptotic probabilities in the interpretation. All four comparisons are reported; none is selected as a new blind discovery.

## Interpretation and limits

A common local ZTF calibration change cannot explain the optical variation under the stated ensemble model. Similar g and r contrasts, the warm excess and the positive r-to-W2 response support the prior dimmer interpretation. The local calibration is the new evidence. The g-based comparison and block intervals show where the evidence is less precise.

A grain-opacity ratio is not a total-flux magnitude slope when dust adds infrared emission. Covering fraction, constant or changing thermal emission, time evolution and saturation can change these slopes. Seven to eight visits cannot separate these effects. This study does not infer a minimum grain radius or prove grey occultation from W1 alone. It does not resolve the ice supply of Gaia20cdd. No ice is measured in G1713 here.

Field kinematics from prior work are not an age. Comparison stars need not match the target's colour or crowding. Source-specific seeing, colour terms and close blends remain possible. Strict fit-quality cuts test only part of this risk. Infrared visits are not locally recalibrated here. Their errors can be correlated. Bootstrap intervals do not include all systematics, temporal correlation or target selection. The optical changes extend beyond the contrast windows; 2025 enters annual plots but not the contrast. No event rate, recurrence period, population frequency or causal collision claim is measured.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy and matplotlib, plus curl and SCI. Installed versions are in files/environment.json. Obtain the cited SCI ZIP from the campaign. From an extracted copy of this verified publication, run:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py /path/to/campaign /path/to/scratch /path/to/output
```

The script verifies the prior ZIP, retrieves its visit file with sci read, downloads ZTF DR24 to separate scratch, prints its hash and runs analysis, colour and exact-rank scripts. Put a previously downloaded raw file at scratch/lightcurves.csv to skip the network. Check its hash against provenance.json. IRSA can change row order or processing; report any changed hash. Keep scratch and output outside the signed publication. For the strict check, rerun analyze.py with STRICT=1 and a separate output directory. Seeds are fixed. Compare aggregate JSON and annual CSV files. Text rounds full-precision outputs.

files/results.json holds main aggregate results and comparison identifiers with new contrast statistics. files/strict_results.json holds the quality-cut check. files/color.json and files/exact_rank.json hold paired colour and exact tests. The annual CSV files and static PNG are aggregate evidence. Analysis writes record-level nightly intermediates only to the separate output directory. No private worker files are needed.
