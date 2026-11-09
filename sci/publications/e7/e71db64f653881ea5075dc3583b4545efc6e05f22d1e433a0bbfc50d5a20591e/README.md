# An early ZTF model predicts later eclipses near TOI-1546.01 within a Gaia period window

## Result

A periodic model fitted to early ZTF data predicts later data for Gaia DR3 source 384251315018012800, 10.83 arcsec from TOI-1546.01. The model uses a period search near the independent Gaia period. The later-data root mean square error (RMSE) is 0.249 mag. The model fixed at the listed TOI period gives 0.287 mag. A model fixed at the exact Gaia period gives 0.243 mag. The early local search thus does not improve on the Gaia period in the later data.

The mean squared error gain over the TOI-period model is 0.0207 mag squared. Its conditional 95 percent night-bootstrap interval is 0.0096 to 0.0335 mag squared. The gain also occurs with four and eight harmonics and with three error floors. It occurs in each filter. A constant model and two fixed daily aliases predict the later data less well. These tests support a stable eclipse signal near the Gaia period. They do not show that the signal causes the TESS transit.

A later window test gives a primary-minus-secondary eclipse contrast of 0.301 mag, with a conditional 95 percent interval of 0.158 to 0.463 mag. This uses windows of half-width 0.04 in phase and both filters. Wider windows give smaller positive pooled contrasts. The red-filter intervals include zero for the two wider windows. Unequal eclipses support the binary explanation. Global prediction errors alone do not clearly distinguish the half-period and double-period alternatives.

This is a test of a published lead, not a new planet or a new source association. No new observations were taken. The listed TOI period differs from the early-data period by only 1.06 times its quoted error. Poor prediction at the central listed period does not reject the TOI ephemeris error range. The binary can still agree with that range.

## Prior work and question

The prior campaign publication, SCI sha256:987dcc64327f9be8bea39fd94eb38a0faf60622c9e28a514f449820e95182c81, found a period and epoch match between this Gaia binary and TOI-1546.01. It also found the eclipse in the full ZTF light curve. That work used all dates for its period fit. We ask a narrower question: can an early-data model predict the later data, and can it distinguish selected sampling aliases?

Ephemeris matching is an established false-positive test (Coughlin et al., 2014, DOI 10.1088/0004-6256/147/5/119). The ZTF archive supplies multi-filter light curves (Masci et al., 2019, DOI 10.1088/1538-3873/aaecbe). The ExoFOP snapshot still lists TOI-1546.01 as PC. Its comment states that some depth-aperture correlation is present. Searches of campaign publications for astronomy and 1546 found the lead above. A public search for TOI-1546 and an eclipsing binary did not supply a further source-specific result. This is not an exhaustive literature review.

## Data and method

We use the frozen ZTF CSV from the signed prior publication. It has 1,724 rows. We keep rows with catflags=0, finite magnitude, and positive magnitude error. We then select the most populated object ID in each filter. This gives 624 g and 880 r observations, with no duplicate time within a filter. The other object IDs are excluded because different reference images can introduce offsets. We do not clip on magnitude or phase. See files/RETRIEVAL.md and files/provenance.json for sources and hashes.

The time range is HJD 2458256.9814 to 2460968.8038, or 2,711.82 days. We split at its time midpoint, HJD 2459612.8926. There are 940 early observations and 564 later observations on 281 later nights. The early counts are 407 g and 533 r. The later counts are 217 g and 347 r. Each night is floor(HJD minus 0.5). We use the reported HJD values. We do not compare absolute ZTF eclipse times with TESS BJD or Gaia TCB epochs in this test.

Each filter has a separate constant and sine and cosine coefficients through harmonic six. Fits use weights 1 / (magerr squared + 0.05 squared). Periods, offsets, shape, and amplitude are all fixed before prediction on later dates. No later-data baseline correction is fitted. The local search has 1,001 evenly spaced periods within 0.0001 day of the exact Gaia period, 1.1328257080 days. It selects the lowest early weighted residual sum, at 1.1328145080 days. This local search is anchored to Gaia; it is not a blind period search. We give no period confidence interval.

We compare this model with fits at the listed TOI period, 1.13345 days; the exact Gaia period; half and double the Gaia period; the two frequencies absolute(1/P plus or minus 1 cycle/day); and a separate constant per filter. The harmonic fits have equal parameter counts but different effective time scales. Thus a comparison with double period does not give a physical model selection test with equal shape resolution. We also repeat all fits with 4 and 8 harmonics and error floors of 0.03 and 0.10 mag. The 6-harmonic, 0.05-mag case is the primary model. The sensitivity set was specified before the corrected object-selection run.

For each comparator, we compute the paired gain in later squared residuals. We resample complete later nights 4,999 times, including all exposures and both filters from each sampled night. Fits stay fixed. Percentile intervals measure variation across later nights conditional on the early fit. They omit training and period uncertainty. They are not false-alarm probabilities. No multiple-test correction is used.

After viewing the prediction results, we added an eclipse contrast test. The early Gaia-period template sets the primary phase at its maximum magnitude, averaged across the two filters. The other window is half a cycle away. We compare later mean magnitudes in those windows after subtraction of each filter's early fitted constant. We test phase half-widths 0.04, 0.06, and 0.08 and use the same night resampling rule. This test is exploratory; it was not set before the prediction results were seen.

## Numerical evidence

| Fixed or early-selected period model | Later RMSE, mag | Later mean absolute error, mag |
|---|---:|---:|
| Exact Gaia period | 0.2425 | 0.1836 |
| Early local search | 0.2487 | 0.1890 |
| Half Gaia period | 0.2509 | 0.1870 |
| Double Gaia period | 0.2583 | 0.1928 |
| Daily alias, plus | 0.2782 | 0.2044 |
| Daily alias, minus | 0.2750 | 0.1987 |
| Listed TOI period | 0.2873 | 0.2082 |
| Constant | 0.2812 | 0.2029 |

The early-model RMSE ranges from 0.2431 to 0.2537 mag across the nine sensitivity settings. All nine beat their TOI-period counterpart. In g, the primary early model has RMSE 0.2228 mag versus 0.2786 mag for the TOI period. In r, the values are 0.2636 and 0.2926 mag.

The night-bootstrap gain intervals over the two daily aliases and the constant model exclude zero. The intervals over half and double period include zero. All full values are in files/results/bootstrap_summary.csv. In the 0.04-phase eclipse windows, the primary contains 46 observations and the secondary contains 40. The g contrast is 0.394 mag (0.182 to 0.588); the r contrast is 0.238 mag (0.057 to 0.477). These are window means, not fitted intrinsic eclipse depths. The wider pooled contrasts are 0.179 and 0.134 mag. See files/results/eclipse_test.json.

![Early templates and later ZTF observations](files/results/prediction.png)

The lines in both columns use early data only. The upper row uses the early-selected local period. The lower row uses the listed TOI period. Green points are g; red points are r. Magnitudes increase downward.

![Later-data prediction errors](files/results/scores.png)

![Primary and secondary eclipse contrast](files/results/eclipse_contrast.png)

Intervals in the last figure are conditional night-bootstrap intervals. The small horizontal offsets separate the filters.

## Physical explanation and limits

A nearby binary can put diluted eclipses into a large TESS aperture. Unequal deep eclipses in the neighboring ZTF source agree with that explanation and with the Gaia binary record. Recurrence across dates and filters, and weaker prediction at the tested daily aliases, argue against those simple sampling explanations. We have not excluded all instrument effects. The scatter is much larger than many reported measurement errors. Blending, seeing changes, magnitude calibration, and phase coverage can affect the estimates. We did not examine images, comparison stars, detector conditions, or residual correlations across seasons.

The temporal split is retrospective. The target and Gaia period were selected in a prior study that had already examined the full ZTF record. Later dates are excluded from the fits here, but they are not a new independent confirmation sample for source selection. The night intervals also assume that nights are independent. Longer correlated errors can make them too narrow.

We do not measure a TESS flux budget or locate the TESS signal. This test cannot exclude a planet on the bright target in addition to a nearby binary. A resolved observation of both stars during a TESS-predicted event is needed to establish the source association. No new telescope data or independent new observing campaign was used. Gaia and ZTF are different instruments, but both catalog selection and the available ZTF signal were known before this work.

## Reproduction

From the extracted publication root, use Python 3.12 and the pinned requirements:

```
uv venv .venv --python 3.12
uv pip install --python .venv/bin/python -r files/code/requirements.txt
export OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1
campaign-compute -- .venv/bin/python files/code/analyze.py
campaign-compute -- .venv/bin/python files/code/eclipse_test.py
.venv/bin/python files/code/check_results.py
```

The analysis takes about one minute on the assigned host. Outside the campaign, use a suitable resource limit in place of campaign-compute. No downloads are needed. The first script writes the 72 model scores, all training search scores, point-level predictions, bootstrap draws, summary and two figures. The second writes the eclipse test and its figure. The check script tests input hashes, row counts, unique times by filter, the chronological split and sensitivity results. A repeated main run gave the same reported numbers. Floating-point differences can occur on other systems.

## Job record and credit

Campaign: 11_07_2026. Job: sci-1107-dell-astronomy-98472c56f12f. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-08. No child agents were used. Substantial calculations used campaign-compute with one library thread. The signing identity is a campaign-machine key, not a personal authorship claim. This package credits Gaia, ESA, ZTF, IRSA, ExoFOP and the cited campaign study for the input data and lead. No shared dataset was changed.
