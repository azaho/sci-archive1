# Long secondary periods of LMC red giants lose phase between OGLE (1997-2009) and Gaia DR3 (2014-2017); ellipsoidal binaries keep phase

## Summary

About one third of pulsating red giants show a long secondary period (LSP) of 200 to 1500 days. The cause of the LSP is not known. A leading explanation is a low-mass companion in orbit, with a dusty cloud that blocks part of the giant once per orbit (Soszyński et al. 2021). An orbit is a strict clock. Thus, if the LSP light change is locked to an orbit, an ephemeris from one decade must predict the phase of the LSP in a later decade.

We did this test on 2,877 LSP stars in the Large Magellanic Cloud (LMC). We fitted the OGLE-II/III I-band light curves (1997-2009) and predicted the LSP phase at the middle of the Gaia DR3 epoch photometry (2014-2017). Then we measured the phase in the Gaia G light curve at the same period. For each star we injected a strictly periodic signal into the same data and refitted it, so that the measurement noise is known star by star.

Results:

1. The LSP phases do not stay on the predicted clock. The median absolute phase offset is 0.121 cycles, but a strictly periodic signal gives a median noise SD of 0.053 cycles. 52% of the LSP stars have offsets that are larger than the strictly periodic null at p <= 0.05. 19% have offsets larger than a quarter cycle.
2. Red-giant ellipsoidal binaries with short photometric periods (< 200 d) in the same catalogue, with the same pipeline, keep their phase over a median of 19 cycles (diffusion D = 3e-5 cycles^2 per cycle, 95% upper limit 7e-5). At Gaia S/N >= 10, all ellipsoidal stars give D <= 1e-4. At Gaia S/N >= 10, the LSP stars give D = 0.0045 (0.0041-0.0050).
3. A random-walk phase model fits the LSP offsets. The fitted effective diffusion is D = 0.0045 cycles^2 per cycle (95% CI 0.0043-0.0048). Light-curve-level injections show that this value corresponds to an intrinsic random walk of about D = 0.003 cycles^2 per cycle (0.055 cycles per square root of a cycle). In units of time, the effective diffusion is 0.0077 cycles^2 per 1000 days, and it is almost the same in the three period terciles.
4. An independent test inside the OGLE data only (same I band, no Gaia data) gives the same result: LSP D = 0.0043 (0.0039-0.0045) for 4,953 stars, ellipsoidal D = 0 (upper limit 6e-5) for 444 stars.
5. The phase change does not continue in one direction. The OGLE-internal phase drift does not predict the sign of the later Gaia drift (Spearman rho = -0.016, p = 0.38, n = 2,816). Thus the data agree with a stochastic phase wander, not with a smooth, constant period change.
6. The pulsation periods of the same stars (median 90 d, 46 cycles of extrapolation) keep no phase memory (resultant length R = 0.09). The LSP has a partial memory. It is between a strict clock and the stochastic pulsations.

Conclusion: inside the tested scope, the photometric LSP is not a strictly periodic clock. The LSP phase wanders by about 0.13 to 0.17 cycles (SD) over a decade (intrinsic and effective diffusion). This result does not agree with a light change that is locked to a fixed orbital phase. A binary model is possible only if the obscuring structure moves in orbital longitude by about 0.1 to 0.3 cycles within some years. The result agrees with the recent Gaia astrometric result against a binary origin (Shariat et al. 2026), but it uses different data and a different method.

## Question

Does the LSP light change of LMC red giants keep a constant phase over two decades, as a Keplerian orbit must do?

## Data

- **OGLE-III Catalog of Variable Stars, LMC long-period variables** (Soszyński et al. 2009, Acta Astron. 59, 239). Catalogue files `ident.dat`, `OSARGs.dat`, `SRVs.dat`, `Miras.dat`, `remarks.txt`, and the I-band photometry in `phot.tar.gz` from https://www.astrouw.edu.pl/ogle/ogle3/OIII-CVS/lmc/lpv/ (retrieved 2026-11-09). The catalogue remarks flag 6,951 stars as `LSP` and 1,814 as `ECL/ELL` (sequence E). Time stamps are HJD-2450000. 34% of the stars also have OGLE-II data (1997-2000); the others start in 2001. Median OGLE baseline: 2,788 days.
- **Gaia DR3** (Gaia Collaboration, Vallenari et al. 2023): `gaiadr3.gaia_source` for the cross-match and `gaiadr3.epoch_photometry` (G and RP transits) for the later epoch. Both were read from the AIP Gaia TAP mirror (https://gaia.aip.de/tap). Gaia times are BJD-2455197.5. We added 5197.5 days to put them on the OGLE time scale (the BJD-HJD difference is less than 4 s and was ignored).
- The SHA-256 hashes of the OGLE files are in `files/provenance/ogle_sha256.txt`. The shared campaign copy of `phot.tar.gz` is at `datasets/ogle3-lmc-lpv-phot-soszynski2009/phot.tar.gz` (SHA-256 43f455c7...166448). The Gaia epoch photometry was fetched for 5,963 sources in 120 queries. A content hash of the retrieved time and flux arrays is b67705103e2bcd3f947594dab4425e22f888d9e5e32894c01c3afce87c95b990 (computed by the snippet in `files/provenance/DATA_NOTICE.md`).

The raw OGLE and Gaia data are not in this bundle. See `files/provenance/DATA_NOTICE.md` for sources, terms and the retrieval recipe.

## Method

1. **Sample.** We cross-matched the LSP and ECL/ELL stars to Gaia DR3 within 1 arcsec and kept the brightest match with -0.2 < G - I < 2.5 (8,760 matches; median separation 0.09 arcsec). Gaia DR3 gives epoch photometry only for sources with `phot_variable_flag = VARIABLE` (5,373 LSP, 590 ECL/ELL). The target period is the catalogue primary period P1 (100-1600 d). For LSP-flagged stars P1 is on sequence D. For ECL/ELL stars P1 is the photometric period (half of the orbital period). After the fits, 5,364 LSP and 588 ECL/ELL stars remained.
2. **OGLE fit** (`04_phase.py`). Model: cubic Legendre trend, first and second harmonics of the target period, and one sinusoid at each other catalogue period (nuisance terms; periods near the target period or its 2:1, 1:2 and 3:1 ratios were removed). We clipped 5-sigma outliers and weighted points by the quadrature sum of the formal error and the robust residual scatter. We refined the target frequency on a two-stage grid (+-0.6/T, then +-0.06/T, with a parabolic peak). For LSP stars we also refined the strongest shorter period (pulsation control).
3. **Prediction.** We extrapolated the phase of the fundamental harmonic to the middle of the Gaia span. Median extrapolation: 7.7 LSP cycles from the OGLE mid-epoch and 4.6 cycles past the last OGLE point.
4. **Gaia measurement.** We used G magnitudes (and RP as a check). Transits with `variability_flag_g_reject = 1` were removed. Model: linear trend plus one sinusoid at the fixed OGLE target frequency, plus the pulsation sinusoid when there were at least 25 epochs. The phase offset is dphi = phi_Gaia - phi_predicted, wrapped to [-0.5, 0.5) cycles.
5. **Strictly periodic null.** For each star we made 40 synthetic data sets. Each set contains the fitted OGLE model (a strictly periodic LSP) plus the star's own OGLE residuals, rotated by a random number of points, and the fitted Gaia model with the OGLE-shaped fundamental scaled to the Gaia amplitude plus rotated Gaia residuals, at the real time stamps. We repeated the full fit (with period refinement) and got a null SD and a p-value for each star.
6. **Phase diffusion.** We fitted dphi with a wrapped normal of mean mu and variance null_SD^2 + D x N, where N is the number of cycles from the OGLE mid-epoch to the Gaia mid-epoch. A 95% interval for D comes from the profile likelihood.
7. **Injection calibration** (`06_rw_injection.py`). For 400 LSP stars we replaced the LSP with a signal whose phase follows a random walk with D_true = 0, 0.002, 0.0068 or 0.02 cycles^2 per cycle, and ran the same pipeline.
8. **OGLE-internal split test.** Ephemeris from the first 45% of the OGLE baseline, phase in the last 35% at the fixed early frequency, with its own strictly periodic null (20 injections per star). Same band, no Gaia data.
9. **Quality cuts for the main test:** at least 25 Gaia G epochs, Gaia span at least 0.8 of the target period, and Gaia S/N >= 5 for the LSP term. Sensitivity runs use S/N >= 3 and >= 10.

## Results

| Group (Gaia S/N >= 5 unless noted) | n | median abs(dphi) (cycles) | median null SD | fraction p <= 0.05 | D (cycles^2/cycle), 95% CI |
| --- | --- | --- | --- | --- | --- |
| LSP | 2,877 | 0.121 | 0.053 | 0.52 | 0.0045 (0.0043-0.0048) |
| LSP, S/N >= 10 | 590 | | | 0.53 | 0.0045 (0.0041-0.0050) |
| LSP, S/N >= 3 | 4,148 | | | 0.51 | 0.0052 (0.0050-0.0053) |
| ECL/ELL, all periods | 173 | 0.050 | 0.044 | 0.31 | 0.0010 (0.0008-0.0014) |
| ECL/ELL, P < 200 d | 70 | | | 0.21 | 3e-5 (1e-5 to 7e-5) |
| ECL/ELL, P 200-300 d | 66 | | | 0.33 | 0.0016 (0.0011-0.0025) |
| ECL/ELL, P > 300 d | 37 | | | 0.43 | 0.0045 (0.0024-0.0117) |
| ECL/ELL, S/N >= 10 | 63 | | | 0.13 | 6e-5 (3e-5 to 1e-4) |
| OGLE split, LSP (I band only) | 4,953 | | 0.167 | 0.12 | 0.0043 (0.0039-0.0045) |
| OGLE split, ECL/ELL | 444 | | 0.178 | 0.09 | 0 (upper 6e-5) |
| Pulsation period of LSP stars | 236 | | | | R = 0.09 (no phase memory) |

Injection calibration (400 real LSP light curves, recovered effective D): injected 0 -> 5e-5; 0.002 -> 0.0028; 0.0068 -> 0.012; 0.02 -> 0.030. The observed 0.0045 thus corresponds to an intrinsic D of about 0.003 (between the 0.002 and 0.0068 points).

LSP diffusion by star property (S/N >= 5, terciles):

| Property tercile | D per cycle | D per 1000 days |
| --- | --- | --- |
| P 136-430 d (median 353 d) | 0.0023 | 0.0071 |
| P 430-674 d (median 527 d) | 0.0036 | 0.0067 |
| P 674-1250 d (median 810 d) | 0.0078 | 0.0091 |
| I-band LSP amplitude low / mid / high | 0.0038 / 0.0042 / 0.0054 | 0.0092 / 0.0068 / 0.0072 |
| Gaia S/N low / mid / high | 0.0052 / 0.0043 / 0.0041 | 0.0093 / 0.0075 / 0.0063 |

O-rich LSP stars: D = 0.0038 (n = 2,493); C-rich: D = 0.010 (n = 384). RGB: 0.0025 (n = 1,186); AGB: 0.0060 (n = 1,691). These groups differ in period, and the diffusion per unit time is almost constant with period. Thus the group differences are mostly a period effect.

Other checks:

- G and RP phases (same Gaia transits, different band) agree: median abs difference 0.012 cycles. The mean LSP offset is -0.015 cycles. Thus a band-dependent phase lag cannot cause the scatter.
- The Gaia/OGLE amplitude ratio is 1.62 for LSP stars and 1.38 for ECL/ELL stars.
- The LSP diffusion does not decrease when the Gaia S/N increases. Thus measurement noise does not cause the excess.

Figures:

- `files/figures/fig1_phase_offsets.png`: phase-offset distributions for LSP, ECL/ELL and pulsation, with the strictly periodic null.
- `files/figures/fig2_drift_vs_cycles.png`: absolute offset and binned circular SD against the number of cycles elapsed.
- `files/figures/fig3_injection_calibration.png`: recovered against injected diffusion, with the observed values.
- `files/figures/fig4_examples.png`: an ellipsoidal star, an LSP star that keeps its phase and an LSP star that loses it (OGLE data, extrapolated ephemeris, and scaled Gaia data).

## Interpretation

A companion orbit is a strict clock at these time scales. Thus a binary model must keep the LSP minimum at a fixed orbital phase, or the obscuring material must move in orbital longitude. The short-period ellipsoidal binaries show that the pipeline keeps the phase of a real orbit over about 19 cycles. The LSP signal loses phase much faster: the effective SD reaches 0.19 cycles after a median of 7.7 cycles. Thus the photometric LSP is not locked to a fixed orbital phase. This agrees with mechanisms that have a finite coherence time, for example oscillatory convective modes, non-radial modes or episodic dust formation. Our test cannot identify the mechanism.

The ECL/ELL stars with photometric periods > 300 d (orbital periods > 600 d, in the sequence-D period range) lose phase like the LSP stars. Some of these stars possibly have an LSP that the catalogue classified as ellipsoidal. Soszyński (2007) noted ellipsoidal-like light curves in some LSP stars. We did not resolve this.

## Limitations

- The strictly periodic null is somewhat optimistic for faint signals: for the coherent short-period ellipsoidal stars, 21% have p <= 0.05 where 5% is expected. Thus individual p-values are approximate. The diffusion fit for the same stars gives D close to zero, and the LSP result does not change at S/N >= 10. The main conclusion therefore does not depend on this calibration.
- The OGLE and Gaia bands differ (I against G). A shape change with band can move the fitted phase. The G/RP agreement and the small mean offset show that this effect is small compared with the scatter. It is not zero.
- Gaia DR3 gives a median of 36 G epochs per star over 2.8 years. Only sources with the Gaia VARIABLE flag have epoch photometry. Gaia S/N cuts select larger-amplitude LSPs.
- The random-walk model is a description. Other forms of phase change (for example, cycle-to-cycle changes in light-curve shape, amplitude changes, or two close periods) can give a similar offset distribution. The absence of a split/Gaia drift correlation argues against a constant period change only.
- The OGLE ephemeris uses the catalogue period P1 and a two-harmonic shape. Stars with complex or multi-periodic LSPs can give a less accurate prediction. The null includes the ephemeris error for a constant signal only.
- The test is photometric. We did not test radial-velocity phase coherence. An orbit with a dust cloud that changes its longitude is not excluded.
- Only LMC stars with OGLE-III LSP flags are included.

## Reproduction

`files/code/run_all.sh <scratch_dir>` downloads the OGLE files, checks their hashes, cross-matches to Gaia DR3, downloads the Gaia epoch photometry from the AIP mirror, and runs the analysis, statistics and figures. Keep the scratch directory outside the publication folder. The full run took about 1.5 hours on 20 processes on a loaded 24-core host. Python 3.12 with numpy 2.5, scipy 1.18, pandas, astropy 8.0, matplotlib and requests.

Script order: `01_catalog.py` (catalogue parse), `02_gaia_xmatch.py` and `02b_best.py` (Gaia cross-match), `03_gaia_epoch.py` (Gaia epochs), `04_phase.py` (per-star fits, null injections, OGLE split test), `06_rw_injection.py` (random-walk calibration), `05_stats.py` (summary statistics), `07_figures.py`, `08_ell_period_split.py`.

Results in this bundle:

- `files/results/phase_results_per_star.csv`: our per-star fit results (5,952 stars): OGLE ID, Gaia DR3 source_id, fitted period, amplitudes, phases, phase offsets, null SDs and p-values, 20 null samples per star, cycles elapsed, split-test values and pulsation-control values. This table holds our measurements, not catalogue values.
- `files/results/summary.json`: all statistics in this README.
- `files/results/rw_injection_calibration.csv`: phase offsets of the random-walk injections.
- `files/results/ell_period_split.json`: ECL/ELL diffusion by period.
- `files/provenance/ogle_gaia_crossmatch_ids.csv`: OGLE ID to Gaia DR3 source_id map with separation and variability flag.

## Provenance

- Job: sci-1107-dell-astronomy-af0b3a1e1b57, campaign 11_07_2026, topic astronomy, machine dell, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Date of analysis: 2026-11-09.
- Related campaign work: the Mira period studies (sci:sha256:daf0fd31..., sci:sha256:ac75c219...) found that phase-persistence tests need light-curve-level nulls. We used such nulls here.

## References

- Soszyński, I. et al. 2009, Acta Astron. 59, 239 (OGLE-III LMC LPVs), arXiv:0910.1354.
- Soszyński, I. et al. 2021, ApJL 911, L22, Binarity as the origin of long secondary periods in red giant stars.
- Soszyński, I. 2007, ApJ 660, 1486, Long secondary periods and binarity in red giant stars, arXiv:astro-ph/0701463.
- Shariat, C., El-Badry, K., MacLeod, M., Leiner, E. 2026, arXiv:2604.09767, Gaia astrometry disfavors a binary origin for long secondary periods.
- Wood, P. R., Olivier, E. A., Kawaler, S. D. 2004, ApJ 604, 800.
- Pawlak, M. et al. 2024, A&A, arXiv:2311.04314.
- Gaia Collaboration, Vallenari, A. et al. 2023, A&A 674, A1.
