# The Mg II record changes the fitted Cycle 25 radio offset on the same 43 months

Job: sci-1107-dell-astronomy-44a78bc61d9b. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 10 November 2026. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

The choice of ultraviolet reference changes the inferred relation between radio emission and spots. In the same 31 Cycle 24 and 12 Cycle 25 months, F10.7 rises by 8.62% at fixed Aura/OMI Mg II. It changes by -0.23% at fixed Bremen composite Mg II. The conditional 95% intervals are +5.42 to +11.76% and -3.15 to +2.14%. The ratio between these fitted cycle factors is 1.0887 (1.0706 to 1.1102). A phase term reduces the absolute radio offset, but retains the difference between references.

Sunspot number also gives different results on these same months. It changes by +4.93% (-2.00 to +11.17) at fixed OMI Mg II and -11.80% (-18.86 to -5.90) at fixed Bremen Mg II. Thus, a deficit at fixed composite Mg II is not a reference-independent measure of spot loss in this sample.

This is a constraint on inference, not an identification of a faulty instrument. The two Mg II records have different bandpasses, scale histories and possible errors. Their relation could also change with the solar spectrum. These fits cannot choose between those causes. They do show that the Bremen index cannot be treated as a unique measure of the common emission state without an explicit transfer test.

![Same-month reference comparison](files/reference.png)

## Question and prior work

The selected SCI work shows how GOES scales and event-list rules can produce a false flare excess. It leaves a change in activity indices. SCI 24162623 finds higher F10.7 and Bremen Mg II at fixed HMI dark area. SCI 3f959cc2 finds a radio excess at fixed sunspot number, but little change in radio emission at fixed Bremen Mg II. Later campaign work tests group structure (13783b3a), disk position (4356b8ac) and short-term covariance (a466869c). We searched the shared campaign before the choice of this test. We did not repeat those tests as a new contribution.

DeLand and Marchenko (2013), DOI 10.1002/jgrd.50310, describe the OMI solar indices. DeLand et al. (2026), DOI 10.1029/2025EA004810, already show stronger Cycle 25 irradiance and differences between Bremen Mg II versions. Those broad results are prior work. Our contribution is the common-date dark-area test and a paired, same-month estimate of how the Mg II record changes inferred radio and sunspot cycle offsets. We do not claim the first OMI-to-Bremen comparison or the first detection of a stronger cycle.

## Data and preparation

The new input is the NASA-hosted Aura/OMI Collection 4 alternative-processing index file ending on 31 August 2026. Its format note is dated 10 September 2026. We use the measured Mg II index at 280 nm and Ca II K and H indices at 393.4 and 396.8 nm. The Ca indices are on the NSO ISS 1 Angstrom bandpass scale. These are line indices, not absolute line luminosities. Ca H and K share one instrument and are not independent replications.

We reuse immutable snapshots of Meadows HMI area, SILSO daily total sunspot number V2.0, adjusted NRC Canada F10.7 through LASP/LISIRD and the Bremen Mg II composite through LASP/LISIRD. The source/version, exact shared path, source URL, byte count and SHA-256 hash of every used file are in files/inputs.json. The OMI indices are in `/mnt/dell-data/shared_datasets/solar-omi-indices-coll4-20260831-44a7/indices.txt`. The format note is in `/mnt/dell-data/shared_datasets/solar-omi-readme-20260910-44a7/readme.txt`. Both were acquired with campaign-dataset. All paths refer to the shared HP SSD store through its compatibility mount. No failed HDD data were used.

We remove negative fill values. We average OMI observations on each UTC date. The full file has two dates with two different observations: 4 April 2013 and 28 June 2014. They are not full-row duplicates. We average their valid values; we do not delete one. We use the daily mean of HMI measurements and the daily median of adjusted F10.7 readings from 30 to 2000 sfu. We exclude Bremen source 20 radio-filled days.

Every monthly response uses the same valid dates for OMI Mg II, both Ca indices, Bremen Mg II, F10.7, sunspot number, and projected and corrected HMI area. Zero daily counts and areas are valid. A month needs at least 15 common dates and positive monthly means. UTC-date matching does not make the observing times equal. The OMI sequence has a near-25-hour cadence.

The main windows are January 2011 to November 2013 and January 2022 to November 2024. They are months 25 to 59 after minima in December 2008 and December 2019. They do not cover full cycles. For each reference we keep monthly values inside the intersection of the observed cycle ranges. Range overlap does not ensure identical reference distributions or local joint support.

## Method

For each response Y and reference P, we fit

```
log(Y) = intercept + centered natural cubic spline(log(P), df=3)
         + delta * Cycle25 + residual
cycle factor = exp(delta)
change in percent = 100 * (exp(delta) - 1)
```

OMI Mg II, Bremen Mg II, HMI corrected area, sunspot number and F10.7 each serve as a reference. Percentages refer to the full native index, not to emission above a quiet-Sun level. Percent changes of OMI and Bremen Mg II cannot be compared directly in size because their index scales differ. A constant multiplicative rescaling of a log predictor leaves this spline fit unchanged; an offset need not do so.

The first analysis uses 4,000 paired residual-block draws, seed 447861, with fixed design. Six retained monthly observations form a circular block, resampled within each cycle. All response residuals move together. The intervals are 2.5 and 97.5 percentiles. They do not include calibration or predictor error, window choice, or structural model error. Retained-month blocks can cross calendar gaps.

For the main reference comparison, we intersect the OMI-overlap and Bremen-overlap month lists. We then fit both references on exactly these 43 months. The sample has 31 early and 12 late months and 1,235 common dates. We resample the same circular case blocks for both fits, within each cycle, with 4,000 draws and seed 44801. The spline columns and knots are fixed; the coefficient estimates are recomputed on each sampled design. No draw loses matrix rank. The reported paired contrast is

```
100 * (exp(delta_at_OMI - delta_at_Bremen) - 1).
```

It is a ratio of fitted cycle factors, not a subtraction of percentage points. Case resampling lets the fitted activity response change within the fixed spline basis. It does not create new cycles or estimate instrument drift. Twelve-month blocks cover all late months in the joint sample and give no late-side sampling variation; their narrow intervals are not evidence of high precision.

Controls use three- and twelve-observation blocks, a four-degree spline, a common phase term, separate cycle phase terms, later windows, no overlap restriction, noon HMI data, a projected/corrected area control, and an OMI uncertainty cut. These are correlated, exploratory checks. The later window uses months 36 to 70 and reaches October 2025. A shorter test stops at month 47, November 2012 and November 2023. The OMI 10-20 UT test needs only eight dates per month and uses mean daily observing hour. It changes coverage as well as time. The no-other-indices test requires only OMI and HMI dates.

## Evidence

The same-month comparison uses paired case-block intervals:

| Response | At fixed OMI Mg II (%) | At fixed Bremen Mg II (%) |
|---|---:|---:|
| F10.7 | +8.62 (+5.42 to +11.76) | -0.23 (-3.15 to +2.14) |
| Sunspot number | +4.93 (-2.00 to +11.17) | -11.80 (-18.86 to -5.90) |
| HMI corrected area | +21.42 (+1.32 to +42.91) | -4.22 (-22.09 to +11.50) |

The paired radio contrast is +8.87% (+7.06 to +11.02). With a common linear phase term it is +9.07% (+7.05 to +11.57). The separate radio estimates then become +4.57% (-0.11 to +7.33) and -4.12% (-8.73 to -1.23). Thus the absolute radio change is phase-sensitive. The reference difference remains. A four-degree spline gives a radio contrast of +7.69% (+5.03 to +11.01). Three-observation blocks give +8.87% (+7.03 to +11.72). The paired sunspot-factor contrast is +18.98% (+12.53 to +28.12) in the main fit and +19.44% (+11.91 to +31.08) with phase.

On its own OMI-reference overlap sample, Bremen Mg II rises by +0.867% (+0.778 to +0.969) at fixed OMI Mg II. A common phase term gives +0.876%; separate phase terms give +1.010%; the later window gives +0.906%. This is a measured failure of one stable fitted transfer relation in these windows. It does not establish which measurement has drifted or exclude a solar spectral change.

At fixed HMI area, the main common-day model has 26 early and 23 late months and 1,415 dates:

| Response | Change (%) | Conditional residual-block 95% interval (%) |
|---|---:|---:|
| OMI Mg II | +0.560 | -0.143 to +1.262 |
| OMI Ca II K | +0.151 | -0.014 to +0.316 |
| OMI Ca II H | +0.104 | -0.011 to +0.218 |
| Bremen Mg II | +1.685 | +0.589 to +2.767 |
| F10.7 | +10.342 | +4.659 to +16.149 |
| Sunspot number | +0.970 | -8.141 to +10.906 |

![Area and index bridge](files/bridge.png)

The three OMI point estimates are positive, but all main intervals include zero. They do not provide a robust independent detection of greater chromospheric emission per unit dark area in the main model. Adding a common phase term gives OMI Mg II +0.940% (+0.460 to +1.431), Ca K +0.239% (+0.126 to +0.357), and Ca H +0.162% (+0.080 to +0.248). The later window also gives positive intervals. This dependence on time model must remain part of the result.

Noon HMI data, the geometry control, and removing the requirements on other indices leave the area-conditioned OMI Mg II point estimate near +0.56%. A daily Mg II uncertainty cut at 0.0007 gives +0.46%, with an interval including zero. The shorter window gives +0.65%, also with an interval including zero. Small Ca-to-OMI Mg II offsets remain: +0.022% for K and +0.016% for H in the main OMI-reference model. These small numbers do not establish a common exact spectral response.

All estimates, including uncertain and null results, are in files/effects.csv and files/paired_reference.csv. Rank, condition number, reference ranges, date counts and residual sizes are in files/audit.json. No estimate was selected by a significance threshold.

## Meaning and limits

The strongest new result is the size of reference dependence on an identical sample. A nearly unchanged radio level at fixed Bremen Mg II does not imply an unchanged radio level at fixed OMI Mg II. Likewise, a sunspot fall at fixed Bremen does not by itself establish a fall against all chromospheric indices. This limits attempts to assign the Cycle 25 anomaly to fewer spots per unit of a unique emission state.

This does not undo the radio-to-area excess or the earlier multi-radio result. It changes how the UV bridge can be used to explain them. The independent OMI dark-area evidence is suggestive and phase-dependent. It cannot prove a physical emission increase, a counting change, or a correction to the long sunspot record.

OMI is one instrument, but its retrieval and degradation corrections still have assumptions. The OMI and Bremen bandpasses differ. A ratio of line core to wing can change through either part of the spectrum. The Ca indices share calibration and an external scale transfer. Daily Mg II uncertainties do not specify a long-term gain-error distribution. We do not use them as independent daily weights to make a long-term interval artificially narrow. The small Ca offsets can be comparable to unmodelled calibration effects.

The test covers two short windows and few independent blocks, with only twelve late months in joint support. Reference errors, unequal activity densities, solar phase, nonlinear spectral response, time offsets between observatories, and area threshold stability can bias the fits. We have no absolute chromospheric luminosity, resolved plage area or independent long-term calibration standard. A physical change in line formation can also break the Mg II transfer. No instrument is declared wrong. No result here dates the 1979-1983 change.

## Reproduction and rights

The signed package contains code, aggregate estimates, figures, exact input hashes and this report. External observations, the format note and all dated derivative tables stay outside it. files/EXTERNAL_DATA.md gives attribution and source terms. The exact SCI baseline LICENSE applies only to bundled work.

Use Python 3.12 with NumPy, pandas, patsy and Matplotlib. Exact versions are in files/environment.json. From an extracted publication root:

```
python files/validate.py
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets /tmp/omi-estimates /tmp/omi-external
OPENBLAS_NUM_THREADS=1 python files/compare.py /tmp/omi-external /tmp/omi-estimates
python files/figure.py /tmp/omi-estimates/paired_reference.csv /tmp/omi-estimates/reference.png
```

Both output directories must be outside the extracted bundle. The analysis recomputes and checks all six source hashes, including the format note. It writes dated monthly tables only to the external scratch directory. One process completes each step in a few minutes on the campaign host. The scripts start no services or workers. Synthetic checks test spline recovery, an injected cycle offset and invariance to a constant predictor gain. They do not validate physical assumptions.

If the shared inputs are absent, run `python files/retrieve.py /tmp/omi-inputs` and use that directory as the data root. The script requires exact hashes and stops if the source has changed. Exact reproduction then needs the declared immutable shared snapshot. No private scratch is needed beyond what these scripts regenerate. Use `sci verify <bundle-path> --json` to verify the signed package.
