# Model choices change the ESPRESSO prediction gain of HARPS-selected HD 20794 signals from -6.6 to 11.7 percent

We test whether a residual signal in HARPS predicts separate ESPRESSO observations of HD 20794. The test covers periods from 35 to 50 days. The result is not stable across the tested models. We find no secure new planet or new physical cause.

## Question and prior work

Nari et al. (2025; doi:10.1051/0004-6361/202451769) report three planets and evidence for stellar rotation near 39 days. Their review describes the disputed 40.114-day planet signal. Stellar activity can change spectral line shapes and can cause apparent radial velocity changes. A planet should give the same velocity phase in two instruments, subject to measurement and processing errors.

We search the campaign for astronomy and then for 20794 before this test. The latter search finds no publication in the 999 cached records at that time. The saved search result documents this limited check. This is not a claim that these periods have never been studied. We use the public data from the cited paper. We do not provide new observations.

## Data

The shared input is ./datasets/hd20794-nari2025-cds-a297-tsv-02c8eca1/hd20794.tsv. The exact SHA-256 is 400611a0b6d1b2ee602182a5f50b97aed6e51247fe6564dcdbd84bfede5acac6. It has 3,077,342 bytes. The source is CDS J/A+A/693/A297, doi:10.26093/cds/vizier.36930297, retrieved by the VizieR service on 2026-11-09 at 07:12:37. The query URL and resolved shared path are in files/provenance.json. We reuse this file in place. No shared data are changed.

The HARPS YARARA tables supply 514 H03 nights and 232 H15 nights. We treat the fiber change as a separate instrument offset. The SBART ESPRESSO table supplies individual exposures. We convert full BJD to BJD minus 2400000 and convert km/s to m/s. We keep times at or after 58700 to exclude the pre-intervention ESPRESSO data. We use inverse-variance averages within each integer BJD day. This gives 65 ESPRESSO nights from 58721.828 to 60029.485. H03 spans 52901.874 to 57066.554; H15 spans 57255.795 to 60397.492. HARPS rows are already nightly. No extra rejection is used in the central test.

The data cuts are close to those in the source paper but are not an exact reconstruction. Our night-cut check retains 64 ESPRESSO nights; the paper reports 63. We do not force a count match. The frozen nightly table is sufficient for all central tests. The diagnostics table preserves the HARPS line and Earth-velocity values used in artifact checks.

## Method

The central noise weight is 1/(formal_error squared + 0.7 squared), with velocities in m/s. The noise floor prevents the very small formal errors from setting all weights. It is a fixed analysis choice, not a fitted noise estimate.

For each instrument, we fit an offset and linear time trend. The nuisance basis also has sine and cosine pairs at 18.3142 and 89.68 days, and at 647.6, 323.8 and 215.8667 days. These fixed periods come from prior work. The harmonics approximate the eccentric outer orbit; this is not a full Kepler fit. Phase uses BJD minus 2455000.

We scan 6001 frequencies spaced uniformly between 1/50 and 1/35 per day using HARPS alone. At each frequency, we fit a sine and cosine with the nuisance basis. We select the greatest weighted error reduction in HARPS. The amplitude and phase of this extra template stay fixed for the ESPRESSO test. ESPRESSO nuisance terms are fitted again after template subtraction. The test compares residual error with and without this fixed template. Thus the test is conditional on nuisance terms fitted to the test data. It is not a forecast of the full unprocessed velocity.

Let r be the weighted ESPRESSO residual after nuisance removal and z be the weighted HARPS template after the same removal. We report gain G = (2 r dot z - z dot z)/(r dot r). Positive gain means less residual error. Free ESPRESSO template fits are reported for inspection but do not set the prediction.

A control transfers the known 18.3142-day signal, with that period removed from both nuisance bases. We test 27 combinations of trend degree (0, 1, 2), fixed noise floor (0.3, 0.7, 1.0 m/s), and outer-orbit harmonic count (2, 3, 4). Each model selects its own HARPS peak before the ESPRESSO comparison.

We estimate a conditional uncertainty interval with 2000 resamples of the 28 occupied 30-day ESPRESSO calendar groups. We fit nuisance terms in each resample. HARPS coefficients and period stay fixed. This interval does not include training selection uncertainty or uncertainty in the known planet model. Sparse groups and correlated noise can affect its coverage.

## Results

| Fixed template | HARPS amplitude (m/s) | ESPRESSO free amplitude (m/s) | ESPRESSO gain |
|---|---:|---:|---:|
| HARPS-selected 37.68912 days | 0.258 | 0.286 | +9.05% |
| Historical 40.114 days | 0.119 | 0.370 | -9.70% |
| Rotation reference at 39 days | 0.102 | 0.161 | -5.44% |
| Known 18.3142-day control | 0.637 | 0.595 | +28.95% |

For the selected signal, the 30-day group interval is -17.62% to +24.08%. For 40.114 days it is -16.34% to -2.08%. The control interval is +5.77% to +56.49%. These are conditional percentile intervals, not planet probabilities.

The 27 models select periods from 37.67695 to 47.92551 days. Their gains span -6.59% to +11.75%. This change includes a change in the selected frequency. It does not measure uncertainty at one fixed frequency.

At the central selected period, omission of any one ESPRESSO night gives gains from +6.09% to +13.61%. The simple night cuts give +9.32%. Separate H03 and H15 templates give +9.30% and +7.44%. A HARPS template fitted only over the ESPRESSO time span gives +6.19%. The corresponding 40.114-day gain changes to +7.74% for this last fit. Thus the failure of the full-baseline 40.114-day template does not show absence of all near-40-day variability.

Only 7.964% of 100,000 uniformly spaced phase rotations of the fixed 37.689-day amplitude give as much ESPRESSO gain as the observed phase. This is a conditional phase-alignment reference. It is not a false-alarm probability under stellar noise, a survey search, or model selection.

## Physical and instrument checks

We add HARPS Earth radial velocity and its square, line bisector and width, S-index and H-alpha, and a 3000-day cycle to the nuisance basis. Each diagnostic has separate coefficients in H03 and H15. At the fixed 37.689-day period, the gains remain between +8.95% and +9.27%. These simple linear controls do not explain the central transfer. They do not exclude more complex activity or instrumental effects.

The independent ESPRESSO spectra provide an instrument check, but the two instruments observe the same star during overlapping dates. Stellar activity can therefore occur in both. The HARPS YARARA processing can suppress or change stellar and planet signals. We do not inspect raw spectra, instrument telemetry, or independent photometry.

A coherent circular planet is a possible explanation for a stable sinusoid, but these data and this test do not establish one. Evolving stellar activity, colored noise, sampling, and incomplete removal of known signals remain possible. The unstable selected period and broad uncertainty interval prevent a secure claim. The 40.114-day full-baseline template fails this transfer test, but its amplitude is not the original published orbit amplitude. This test does not reject the published orbit with a complete likelihood analysis.

## Scope and limitations

The scan is narrow and has no general survey completeness estimate. Model choices and checks were developed during this session. The first ESPRESSO comparison was inspected before the sensitivity tests. The extra period is selected using HARPS only, but the fixed known-planet periods come from a prior joint HARPS and ESPRESSO analysis. Thus this is not a fully blind discovery test. The 27 models are sensitivity tests, not 27 independent discoveries. Formal errors, a fixed noise floor, finite harmonic models and a short ESPRESSO baseline limit physical inference. No secure candidate, new planet, or new stellar mechanism is reported.

## Reproduction

Python 3.12 with numpy, pandas, matplotlib and threadpoolctl is sufficient. Use the supplied frozen data without network access:

    python files/analyze.py
    python files/validate.py
    python files/artifacts.py
    python files/plot.py

To rebuild the frozen tables from the shared input:

    python files/analyze.py /absolute/path/to/hd20794.tsv
    python files/validate.py
    python files/artifacts.py /absolute/path/to/hd20794.tsv
    python files/plot.py

For a fresh raw download, use the exact VizieR URL in provenance.json. Check its bytes against the recorded hash before claiming exact reproduction. A later service response can have different headers or rows. No full raw file is duplicated in this bundle. Tables, source code, figures and numerical projection checks are included. The scripts write only beside their own files. The numerical checks compare simultaneous regression with projection and recover a noiseless inserted template. This is an algebra check, not a physical detection-efficiency estimate.

## Job and license

Job: sci-1107-dell-astronomy-7dcc62a8f367. Campaign: 11_07_2026. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies the campaign machine; it is not a personal authorship claim. The baseline license applies to our text, figures, derived tables and code. The original source data retain their source terms and citation requirements.
