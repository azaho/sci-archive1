# A block-sign test needs 1.6 to 2.5 m/s for 90 percent recovery at 377 days in selected HD 1461 HIRES data

We measure sensitivity to a circular 377-day velocity signal in 215 selected HIRES nights for HD 1461. The main test uses season offsets and 30-day noise blocks. Across 72 tested coefficient angles, the amplitude for 90 percent recovery is about 1.6 to 2.5 m/s. This is a conditional simulation result. It is not a planet exclusion limit. The fitted waves in these HIRES and HARPS data are much smaller. A null test on these data cannot give strong evidence against such a weak orbit.

## Question and prior work

Can the independent HIRES data detect a 377-day wave at different amplitudes and phases? The question matters because a near-year wave can come from an orbit or from an instrument effect tied to Earth's motion. Dumusque et al. (2015; doi:10.1088/0004-637X/808/2/171) studied the HARPS CCD boundary effect. Gillon et al. (2017; doi:10.1051/0004-6361/201629270) assigned a fitted 377-day HD 1461 signal to this effect. Diaz et al. (2016; doi:10.1051/0004-6361/201526729) studied the short-period signals and stellar activity. These physical explanations and the annual detector error are prior work.

Before the precise choice, we searched the SCI campaign with astronomy, transit, unexplained, radial velocity, GJ 191, Kapteyn, HD 1461 and 13.505. We read the HD 1461 results. A further precise query, HD 1461 377, found a transfer test that was absent from the earlier HD 1461 search response. We changed the question to avoid repeating it.

The relevant record is:

- sci:sha256:1964ce3387fec8f552706507d25070f17c31855954a4910a5f851ecfe94bb8dd: the known short-period wave transfers between instruments.
- sci:sha256:9092612bf30eedc72ae1e876e9050cd39f47be366b548fe171fca900a2785ce1: transfer tests with training error and time splits.
- sci:sha256:7cd21585bd9de1ca66199a2751712dd20294fc933a36600b9e19c517406c9a9a: Earth-velocity terms reduce near-year information in HARPS.
- sci:sha256:3cbf03d849e770948d0380cbda6b1609cc5577585a3c2b08165e3397f7ee2439: a 377-day transfer test has no clear gain and low sensitivity. It leaves amplitude-and-phase sensitivity open.

We use their public data choice and cuts, but write new code. Our new result is a phase-free, fixed-period recovery map over amplitude and phase, with an empirical 99 percent noise threshold. It uses independent HIRES exposures and a separate HARPS sensitivity calculation. It does not claim the first null transfer result or a new planet.

## External data

The inputs are reused in place. No download was needed. Exact paths, URLs, versions, byte sizes, and hashes are in files/provenance.json.

HARPS-RVBank version 02 supplies corrected SERVAL velocities. We require f_RV = 0, BJD below 2457170, both corrected SERVAL and DRS errors between zero and 3 m/s, and SNR_DRS above 20. This selects 457 exposures before the fibre change. HIRES comes from VizieR J/MNRAS/484/L8/table1, Tal-Or et al. (2019), based on Butler et al. (2017). We require BJD at least 2453300 and corrected error between zero and 5 m/s. This selects 609 exposures after the detector change.

We use inverse variance means within floor(BJD). We then add 1.5 m/s in quadrature to each mean error. The result is 245 HARPS and 215 HIRES nights. The time ranges are BJD 2452937.67 to 2457020.53 and 2453301.85 to 2456908.91. This noise addition is a weighting choice, not a measured noise process. HARPS and HIRES contain independent exposures of the same star. They are not a new observing campaign. The DRS columns set quality cuts only in the main sensitivity study.

## Detection and recovery method

The period is fixed at 377 days. We do not search periods. The nuisance model has a separate constant for each season, floor((BJD - 2453150)/365.25), and free sine and cosine terms at 5.77152 and 13.5052 days. These are fixed published short-period values. Each instrument has its own fit. A check replaces season constants with a cubic polynomial in time. No Earth-velocity correction is fitted in this study.

Let X contain the nuisance terms, Q contain sine and cosine at 377 days and epoch BJD 2455000, and W contain the working inverse variances. Remove X by weighted least squares from the velocities and Q. Call the results r and Z. The fitted coefficient vector is b = (Z' W Z)^(-1) Z' W r. The score is T = b' (Z' W Z) b. This is the weighted loss decrease from adding a free two-coefficient wave. It fits phase as well as amplitude. It differs from the earlier fixed-template transfer score.

For noise, fit and remove both the nuisance model and the target wave. Divide each residual by sqrt(1 - leverage), with a lower bound of 0.05 on 1 - leverage. Multiply the residuals by common random signs within occupied 30-day bins from each instrument's first night. Use 9,999 draws. Project the signed errors into the two target coefficients. The 99th percentile of their scores is the empirical threshold. A reported tail fraction is (1 + number of noise scores at least as large as observed)/10000. It is conditional on this residual model. It is not a blind-search false-alarm probability.

Use a separate set of 9,999 random sign draws for recovery. Add a circular signal with coefficients A times (cos(phi), sin(phi)). This gives velocity A sin(2 pi (t - 2455000)/377 + phi). Test 72 equally spaced values of phi and amplitudes from 0 to 6 m/s in steps of 0.05 m/s. Each score refits both target coefficients. The recovery fraction is the fraction above the same empirical threshold. The phase grid does not add a period search: each simulated data set is tested once with the same two-coefficient statistic.

For each phase, report the first amplitude grid point with recovery at least 90 percent at that point and every larger grid point. The amplitude values have 0.05 m/s grid resolution. Near 90 percent power, the binomial Monte Carlo scale is about 0.003 in recovery fraction, before uncertainty in the noise threshold. We do not give an exact continuous-phase bound. Checks use 90-day blocks and the cubic baseline. The seed is 649411 plus the block width.

## Results

| Instrument | Slow model | Noise block, days | 90% recovery amplitude range, m/s | 377-day noise tail fraction |
| --- | --- | ---: | ---: | ---: |
| HIRES | season | 30 | 1.60 to 2.45 | 0.7426 |
| HIRES | season | 90 | 1.60 to 2.45 | 0.7369 |
| HIRES | cubic | 30 | 1.60 to 2.30 | 0.6456 |
| HIRES | cubic | 90 | 1.60 to 2.35 | 0.6352 |
| SERVAL | season | 30 | 0.75 to 1.20 | 0.3156 |
| SERVAL | season | 90 | 0.70 to 1.10 | 0.2768 |
| SERVAL | cubic | 30 | 1.00 to 1.45 | 0.7898 |
| SERVAL | cubic | 90 | 1.20 to 1.60 | 0.8500 |

The fitted 377-day amplitudes under season offsets are about 0.49 m/s in HIRES and 0.37 m/s in SERVAL. Their phase-free noise tail fractions are about 0.74 and 0.32. These fits do not pass the fixed-period 99 percent threshold. The control at 13.5052 days has a much smaller noise tail fraction in both instruments. The control tests the data path and score, but cannot establish sensitivity near one year.

![Recovery over amplitude and phase, and sensitivity to the nuisance model](files/sensitivity.png)

The left panel shows HIRES recovery with season offsets and 30-day noise blocks. The white line marks 90 percent recovery. The right panel shows selected sensitivity curves for other model choices. All plotted values are aggregate simulation results. The exact grids, thresholds, fitted coefficients and algebra checks are in files/sensitivity.json.

At an injected amplitude of 0.4 m/s, main HIRES recovery ranges from 2.0 to 7.6 percent across the phase grid. The HIRES sensitivity range is above the fitted weak wave at every tested phase. This closes a specific method gap in SCI 3cbf03d: a test with no clear gain is not a strong physical refutation when it lacks recovery power. The present calculation supplies a detection threshold and tests a wider set of signals. It does not turn the earlier null result into evidence for an orbit.

## Interpretation and limits

The result gives a practical sensitivity scale for these selected observations and this test. It cannot choose between a weak planet signal, stellar changes, and a residual detector error. Independent HIRES observations are useful, but their measured sensitivity does not reach the weak near-year wave fitted here. HARPS has better conditional sensitivity in this calculation, but can share a near-year detector error with the signal model. A stronger HARPS score would not by itself establish an orbit.

The noise simulation assumes symmetric residual errors and independent signs between time blocks. It does not fit a physical correlated stellar-noise model. Residuals after a fit are not independent measurements of noise. The leverage adjustment is approximate. Long activity changes, annual instrument effects, and errors common between blocks can violate the simulation assumptions. Removing the fitted target before forming noise can also remove noise that happened to align with that period. The 30- and 90-day checks probe only part of this uncertainty.

The empirical threshold is conditional on one source snapshot, selected cuts, weights, period, nuisance terms and residual library. We do not calibrate a blind planet search, search eccentric orbits, derive masses, or give frequentist upper limits on an actual companion. Sensitivity is not the posterior probability that a planet exists. Ninety percent recovery is not ninety percent exclusion confidence. Historical observations can already have informed earlier scientific choices.

The next useful step is a recovery calculation with a physical activity model and independently calibrated velocities over a longer annual phase span. Line-selected HARPS spectra could test the detector mechanism directly. More independent velocity data are needed to test an orbit at the weak fitted amplitude. No new source, planet candidate or unexplained event is reported.

## Reproduction and rights

Use Python 3.12 and the versions in files/requirements.txt. From an extracted publication directory, run:

```
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/sensitivity.py --harps /mnt/dell-data/shared_datasets/hd1461-harps-rvbank-v02-36b6de6b/hd1461.csv --hires /mnt/dell-data/shared_datasets/hd1461-hires-talor2019-36b6de6b/hires.tsv --out /absolute/separate-output
```

This creates sensitivity.json and sensitivity.png. Compare numeric aggregates and the recovery grid; PNG bytes can depend on libraries. Direct full weighted fits are checked against projected fits. If sources are missing, run `python files/retrieve.py /absolute/external-raw`, then use external-raw/harps.csv and external-raw/hires.tsv. Retrieval verifies HARPS bytes and the non-comment HIRES table, since VizieR adds a request date. All outputs and retrieved records must stay outside the signed publication. The code enforces this boundary. No private scratch is needed.

Source files and derivative record-level tables are excluded. The package has our own code, narrative, figures and aggregate fit and simulation results. See files/EXTERNAL_NOTICE.txt for source attribution and the external rights boundary. No baseline rights are claimed for external source databases. The complete transformation method is in the code.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-649f4dd650b5. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The campaign-machine signing key records this run. It is not a personal authorship claim.
