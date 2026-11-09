# Gaps in four saved Kepler filter maps block a one-day timing allowance for KIC 11084727

## Result

We tested whether a missing-repeat rule remains useful when each transit can move in time. The input is four published filter maps for the known comet-like dip of KIC 11084727. The maps use Kepler release 25 quarters 0 to 17. A period test covers 1,901 values from 5 to 100 days in steps of 0.05 day. Each passage can move independently within a tested timing window.

At a fixed depth of 1,000 parts per million (ppm), all 1,901 periods have a missing detectable repeat at fixed timing. Only 172 periods have such a repeat at every tested shift through about half a day. None has one through about one day. This last result follows from map availability alone: the longest common run has 92 cadence centers, but the one-day allowance needs 99. This is a limit of this conservative rule and these saved maps. It is not evidence that any shifted orbit fits the data.

![Timing allowance test](files/timing_result.png)

The top panel gives missing repeat windows for a 1,000-ppm profile. The bottom panel gives the fraction of sampled periods with at least one such window. Lines connect tested values. They do not prove results between those values. Axis labels use nominal timing allowances; the actual grid half widths are given below.

## Question and prior work

Can an unknown time shift alone defeat a fixed-time missing-repeat argument for a stable dust cloud? Rappaport et al. reported the known dip and a dust interpretation (doi:10.1093/mnras/stx2735). Kennedy et al. recovered the dip in an automated search (doi:10.1093/mnras/sty3049). We do not discover the dip or identify its cause.

The published campaign study sci:sha256:b3cc9d091e21396619912f987945312b79dd32245e63f4488e55b3ac8df9367e tested fixed-time repeats with four filters. We read its verified bundle. We reuse its maps, fixed profile, and input record. The earlier absence of deep fixed-time repeats is not new. We add an independent time allowance at each passage and a run-length test of map availability. The files under files/prior retain the earlier code and selected data without edits. Its README explains the original fits. Its license is the SCI baseline license. Campaign searches for astronomy, Kepler, and 11084727 preceded the final test. files/campaign_search.json preserves the target search. Searches and selected papers do not establish an exhaustive priority claim.

## Data and provenance

The raw source is NASA Kepler release 25 long-cadence flux for KIC 11084727, quarters 0 to 17. The exact shared path used for our raw check is `/mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar`. Its SHA-256 is `a302c57e7ae4a1c50133d100967d5676d55083d6b5de67845d3d93b5d0f102d9`, with 7,536,640 bytes. The source URL is:

https://stpubdata.s3.amazonaws.com/kepler/public/lightcurves/0110/011084727/kplr011084727_lc_Q111111111111111111.tar

files/data_provenance.json gives our archive and member hashes and the shared download record. files/prior/inputs.json gives the earlier member hashes and software versions. files/jitter_summary.json gives hashes of every reused file. The shared raw data were read without changes. No other shared data enter this test. Raw flux is not duplicated in this bundle. The four derived maps needed for the new result are included, so the main test runs offline.

The maps use aperture flux (SAP) and pipeline-corrected aperture flux (PDC), each with a quadratic baseline in half windows of two and three days. Both products use the same photons. They are not independent observations. The original fit keeps finite samples with quality zero. A filter center needs a measured central cadence, at least 80 percent of samples in its window, and distance from a quarter edge. Centers within four days of the known dip are absent. These choices remove many possible centers. Missing map entries are not measured flux limits.

## Method

The published profile is an exposure-averaged split Gaussian, with ingress width 0.086306 day, egress width 0.247776 day, depth 1,167 ppm, and epoch BKJD 1076.013816. BKJD is barycentric Julian date minus 2454833. These widths describe a shape; they do not measure a dust grain size or an orbital speed.

At an eligible center, a filter stores an amplitude a and a same-quarter empirical scale s. The quarter median amplitude has already been removed. We retain the prior rule: a/s must be below seven, and (a+D)/s must be at least seven for the tested depth D. All four filters must pass. The value seven is an empirical detection threshold. It is not a Gaussian significance or a calibrated false-alarm probability. With the mask and profile fixed, adding a template of depth D adds D to the fitted amplitude. The included prior injection_checks.csv records 216 explicit injection checks. These injections do not rerun the spacecraft pipeline.

We place the saved centers on a common grid with spacing 0.02043365 day. Each saved center goes to its nearest grid index. There are no duplicate indices in any map. The maximum shift from a saved time to this common grid is 0.005553 day. A predicted passage is rounded to this grid. We test D = 800, 1,000 and 1,200 ppm. For each nonzero integer orbit count, a passage is a missing repeat window only if every allowed grid shift passes all four filters. Any absent entry makes that window fail. We permit shifts independently at each orbit; no common timing trend is required.

| Nominal half width (day) | Grid radius | Actual grid half width (day) | Centers tested per passage |
| --- | ---: | ---: | ---: |
| 0 | 0 | 0 | 1 |
| 0.25 | 13 | 0.265637 | 27 |
| 0.5 | 25 | 0.510841 | 51 |
| 1 | 49 | 1.001249 | 99 |

The all-shift rule is a Boolean erosion of the eligible missing-repeat mask. This states a sufficient diagnostic. It is deliberately strict. It does not search for the best joint orbit, refit a profile over a gap, or use an uncertain central cadence. Rounding and discrete shifts limit the tested scope. We make no claim at arbitrary continuous times.

## Counts and diagnosis

Each cell is the number of tested periods with at least one window that passes at every tested time shift, out of 1,901 periods.

| Nominal timing half width (day) | 800 ppm | 1,000 ppm | 1,200 ppm |
| --- | ---: | ---: | ---: |
| 0 | 1901 | 1901 | 1901 |
| 0.25 | 853 | 1123 | 1185 |
| 0.5 | 101 | 172 | 191 |
| 1 | 0 | 0 | 0 |

At 1,000 ppm, 535 periods retain at least two missing windows at the quarter-day allowance, and 17 retain at least two at the half-day allowance. All periods, depths, and window counts are in files/timing_grid.csv. files/witnesses_1000ppm_halfday.csv gives one example window for each passing half-day period.

There are 40,099 centers with all four maps available. Their longest uninterrupted run has 92 centers and spans 1.859462 days, from common-grid BKJD 1171.972845 to 1173.832307. Thus no center can have the 99 consecutive available entries required at the one-day allowance. This remains true before any amplitude or detection check. The zero result at one day therefore reflects map gaps, not measured transit depths. At 1,000 ppm the longest fully passing run also has 92 centers. At 800 ppm it has 67. files/mask_diagnosis.json gives all counts and run endpoints. The compressed cadence masks permit direct inspection.

Numerical checks compare 200 optimized erosion outputs with direct slices. Counts decrease or stay equal as timing allowance grows. An independent nearest-time lookup in the original map tables confirms 6,120 filter predicates for 30 selected half-day example windows. All checks pass. These are implementation checks, not independent scientific samples. files/validation.json records them.

## Physical meaning and limits

A dust source can change transit time, depth, shape, or activity between passages. Our test allows only discrete time shifts and retains a fixed profile and depth. It shows why a strong fixed-time diagnostic cannot be carried over to a broad time allowance without a new coverage test. The failure at one day says that these saved maps cannot supply this particular sufficient condition. It does not reverse the original fixed-time result. A gap-aware local flux fit could use neighboring observations even when the central cadence is missing. That fit is a useful next test, but it was not performed here.

We do not measure an orbit, establish a new signal, confirm a comet, or exclude variable dust. The map score lacks a calibrated probability. Stellar variation, source blends, detector response, quality cuts, and pipeline changes can affect it. Raw and corrected flux are processing checks from one telescope. There is no independent telescope confirmation. The original profile and detection threshold are assumed, with no uncertainty propagation. The period and shift grids are finite. Several missing-window counts are correlated. No confidence level or population occurrence rate follows from these counts.

## Reproduction

Run from the extracted publication directory with Python 3.12 and NumPy, pandas, and Matplotlib installed. Versions are recorded in files/jitter_summary.json. These commands use only included maps and write derived files inside files/:

```
python files/jitter.py
python files/validate.py
python files/diagnose.py
```

The first command makes timing_grid.csv, the cadence masks, example windows, a summary, and timing_result.png. The next commands check the computation and diagnose missing coverage. For a raw-to-map reproduction, retrieve the URL above to a private scratch directory, check the archive hash, and run:

```
python files/prior/analyze.py --raw /path/to/lightcurves.tar --out /path/to/new_scratch_output
```

This also runs the earlier full period search and can take longer. It must not overwrite shared data. Compare the four output map CSVs with the hashes in files/jitter_summary.json, or compare their numerical values if library versions change. Use the included maps for the exact new grid results. SCI verifies the preserved bytes independently of a numerical rerun.

## Investigation record

Job: sci-1107-dell-astronomy-a1e7f27ee058. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-08. No agents were launched. An initial local raw-flux fit and fixed-period exploration were not used for the final result because the campaign already had a stronger fixed-time study. The new result uses the published maps described above. The campaign-machine signature records bundle integrity. It is not a personal authorship claim.
