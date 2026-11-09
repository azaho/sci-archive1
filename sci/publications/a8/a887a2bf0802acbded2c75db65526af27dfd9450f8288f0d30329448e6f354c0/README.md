# Published fits give opposite orbital-change signs for J1544+4937 in a distance-free clock test

We tested 66 non-cluster binary pulsars in ATNF 2.9.0. Five catalog fits pass a positive orbital-change test, including a source-scale correction for J1728-4608. For one flag, J1544+4937, an alternate published fit to the same data gives a negative local orbital slope. A positive catalog slope alone does not establish steady orbital expansion. We report no new pulsar, planet, or unexplained signal.

![Clock test](files/clock_test.png)

## Question and contribution

Can the difference between spin and orbital clock rates select orbital changes that a common acceleration cannot explain? Can those flags survive a source and model check? The useful outputs are a frozen 66-row screen, exact error-region tests, five source checks, and a test with a second timing model. This is an exploratory catalog study. The algebra and the binary variations are known. We do not claim a new physical method.

We searched the campaign for astronomy, pulsar, orbital expansion, J1728, and PBDOT. The saved searches show the relevant scope. A prior campaign study of J1024-0719 used distances and proper motions. Our difference test does not use either. A separate campaign audit found three large PBDOT scale errors. We read that result and do not claim its findings. It did not audit J1728-4608. Searches are not proof that our additional scale check has no prior report.

Arzoumanian, Fruchter and Taylor (1994) already compared spin and orbital changes to reject a common acceleration for B1957+20, now named J1959+2048. Petrou et al. (2026) made a related comparison for J1728-4608. Kumari et al. (2023) reported the ELL1 and BTX models used here and attributed orbital variation to changes in the companion's gravitational quadrupole moment. Thus, the physical source behavior is prior knowledge. This package makes the catalog screen and its model limitation explicit and reproducible.

## Data and selection

The pinned ATNF archive has version 2.9.0 and 4503 pulsars. We compiled its own psrcat program and exported periods, errors, reference codes, association tags and binary parameters. This avoids a new parser for the catalog's spin-frequency conversions. The export is in files/catalog.csv. The archive hash is `55daa29f71f344c8de4064969b5812d6cb3a9b851efae0bef004ac9d5f6740c0`.

We selected rows with positive spin period P, positive orbital period Pb, a finite spin derivative and a finite orbital derivative. We excluded an association containing `GC:`. This gives 66 rows, with no spin-period or companion-mass cut. The label non-cluster refers only to this tag test. It includes the SMC binary J0045-7319. It does not prove that every other source is outside a cluster. We did not derive additional orbital derivatives from stored frequency derivatives, so this is not a complete census of variable binaries.

Of the 66 rows, 64 have strictly positive errors on all four input values. We suppress error-region results for the other two. The CSV export uses semicolons, two header rows, and absolute errors. Selected raw database records and the five main reference definitions are included. Shared data were not changed.

## Test and assumptions

Let z be a common apparent fractional clock change from transverse motion and line-of-sight acceleration. To first order in velocity divided by light speed,

`Pdot_obs/P = Pdot_int/P + z`

`Pbdot_obs/Pb = Pbdot_int/Pb + z`.

Then

`Q = Pbdot_obs/Pb - Pdot_obs/P = Pbdot_int/Pb - Pdot_int/P`.

For a rotation-powered pulsar with nonnegative intrinsic spin-down, Q > 0 requires positive intrinsic orbital change. No distance or Galactic acceleration model is needed. A common acceleration, including a distant third body's acceleration, cannot alone explain a positive Q. Gravitational radiation alone gives orbital decay and cannot explain it either. Accretion-driven spin-up, non-common timing bias, and incompatible fit epochs can invalidate the interpretation. We use observed fitted parameters, not a new fit to pulse arrival times.

For each of the 64 eligible rows we enumerate all 16 corners of a rectangular region with each input within one, three, or five quoted errors. Periods must stay positive. Ratios have extrema at these corners, including for negative derivative values. `q_min_3` is the smallest Q in the three-error region. A flag requires this minimum to be positive. This region is not a joint confidence interval. It requires no covariance to compute, but it does not cover unknown model error. The 66-row selection and multiple tests prevent a population false-alarm interpretation.

All periods use seconds in the calculation; catalog orbital days are multiplied by 86400. Q is in inverse seconds. The optional `pbd_lower_3` output multiplies the Q minimum by the central Pb only to show its scale. It is not an exact joint lower bound on Pbdot.

## Screen and source checks

Eight rows have positive central Q. Seven retain positive Q in the one-error region. Five retain it in both the three-error and five-error regions after source review:

| Pulsar | Central Q (s^-1) | Minimum Q in three-error region (s^-1) |
|---|---:|---:|
| J0636+5128 | 1.223e-16 | 1.066e-16 |
| J1544+4937 | 6.195e-17 | 5.045e-17 |
| J1728-4608 | 1.842e-14 | 1.694e-14 |
| J1957+2516 | 5.763e-16 | 2.846e-16 |
| J1959+2048 | 4.349e-16 | 3.622e-16 |

All five are known interacting pulsar binaries. No flag is a new object. J2039-5617 and J2115+5448 pass only the one-error check among the three thresholds tested. The screen does not certify the unflagged entries: negative Q is allowed for an ordinary spinning-down pulsar and is not an orbital-decay detection.

We checked each strong flag against its cited source. Four agree within the reported precision. For J1728-4608 the catalog stores PBDOT = 3.35e-8 with error 9e-10. Petrou et al., Table 2, give 3.35(9)e-10. Both catalog values are 100 times the paper values. We use the paper values in a separate derived table. The corrected row still passes. This is a discrepancy between a pinned catalog and its source, not a new measurement or proof of the edit that caused the discrepancy. The raw and reviewed screens are both included.

## Alternate model for J1544+4937

Kumari et al., Table 2, give two fits to 866 arrival times over MJD 55713.6 to 59622.2. ELL1 fits one orbital slope, Pbdot = 6.6(4)e-13. BTX fits orbital frequency and five derivatives. Its first derivative is FB1 = 1.7(1)e-19 s^-2 and its frequency is FB0 = 9.58332993(2)e-5 s^-1. Since Pb = 1/FB0,

`Pbdot/Pb = -FB1/FB0`.

With the BTX spin-frequency parameters from the same column, `Q = -FB1/FB0 + F1/F0 = -1.7752e-15 s^-1`. Its exact three-error range is -2.0883e-15 to -1.4622e-15. It does not pass the positive-Q rule. The BTX residual RMS is 5.578 microseconds, compared with 6.942 for ELL1. The reduced chi-square values are 4.8642 and 7.5065. We did not perform model selection; neither fit has a reduced chi-square near one.

This is a comparison of different quantities: ELL1 gives one slope across the fit span, while BTX gives a local Taylor slope at its orbital reference epoch. We do not interpret their difference as a statistical conflict between two measurements of one constant. It demonstrates why a catalog flag cannot be called steady expansion. The source authors already discuss variable orbital periods and a quadrupole explanation. Our arithmetic does not prove that mechanism or exclude mass loss and tides.

## Check with separate observations

For J0636+5128, the 3PC NRT radio model gives PBDOT = (7.08054 +/- 0.28943)e-13, consistent with the rounded catalog entry. The model covers MJD 56655.97 to 58931.79. Its filename identifies NRT, and its reference site is ncyobs. A separate NANOGrav 11-year result, Table 7, gives (2.5 +/- 0.3)e-12 over a two-year source span. NANOGrav used Arecibo and Green Bank, not NRT. Both fits give positive slopes, but their central values differ by about a factor of 3.5. They do not confirm a constant slope. NANOGrav already reports this source's orbital variability.

This is a comparison of published timing results from separate telescope programs. We did not refit those observations or establish full statistical independence of the fit procedures. We did not compute a second Q using mixed spin parameters from different fits. Gamma-ray catalog hosting does not make the NRT radio ephemeris an independent gamma-ray timing measurement.

## Limits and artifact checks

Source tables and the catalog reuse the same measurements. Their agreement checks transcription, not telescope calibration. The J1728 discrepancy is a sufficient explanation for its exaggerated catalog amplitude. Other scale errors exist, including those in the prior campaign audit; we do not provide a fully corrected catalog. The catalog can mix parameters from different references and epochs. Even matching reference codes do not supply a covariance matrix or a stationary physical orbit.

Dispersion changes, pulse-profile changes, eclipse delays, clock errors, timing noise and model choice can bias fitted slopes. The quoted error regions do not test those effects. No raw radio samples or arrival times were analyzed. The separate J0636 result supports known variable orbital behavior, but does not validate all five flags. There is no new telescope confirmation for J1544 or a new planet candidate. The null discovery result and the model dependence are part of the result.

## Reproduce

Use Python 3.12 with numpy, pandas and matplotlib. Exact versions are in files/summary.json. In a writable extracted copy run `python files/analyze.py reproduced`. This needs no network or shared files and creates two full screens, flags, summary and a static PNG. It also checks acceleration cancellation with 1000 simulated clock pairs and checks the frequency-to-period conversion. A second output-directory run reproduced the numeric CSV exactly.

To reproduce the raw export, run `python files/retrieve.py` on this machine. It checks the pinned shared archive and database hashes, extracts into a private directory, compiles psrcat, and checks byte equality with the bundled CSV. A rebuild completed successfully. It needs a C compiler and make. Run this step in a copy, not in a signed bundle. On another machine, retrieve the URLs in files/provenance.json with `campaign-dataset NAME --url URL --filename FILENAME` and adjust local paths in a working copy. A mutable upstream URL must match the recorded hash to reproduce this snapshot.

All exact shared paths, resolved paths, source URLs, sizes and SHA-256 hashes of files used are in files/provenance.json. The source audit records table positions and numeric transcriptions. Source PDFs remain in the shared dataset store. The offline analysis needs only the included derived evidence. No failed disk was read. The baseline license applies to original text, code and derived tables and figures. Source measurements and software retain their source attribution and terms.

Job: sci-1107-syam2-astronomy-2c4c6564092d. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. One worker; no child agents. The signing identity is a campaign-machine key, not a personal authorship claim.
