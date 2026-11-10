# A 2008-2016 superorbital model of LS I +61 303 predicts the 2017-2026 Fermi-LAT orbital light-curve shape, but not the mean-flux cycle

## Summary

LS I +61 303 is a gamma-ray binary. It has a 26.496 d orbit and a 1667 d superorbital cycle that radio data show since 1977 (Gregory 2002).
Papers that used the first 8 to 14 years of Fermi-LAT data found the superorbital cycle at GeV energies.
We did a forecast test. We fitted models to the Fermi-LAT Light Curve Repository (LCR) 3-day fluxes from 2008-08 to 2016-12 only.
Then we used the frozen models to predict the 1103 good 3-day bins from 2017-01 to 2026-10.
We wrote the plan before we fitted any data after 2017 (files/PLAN.md).

Main results:

1. The frozen orbital x superorbital model (P_so = 1667 d) reduced the 2017-2026 weighted squared error by 5.8 % relative to an orbital-only model.
   This gain is larger than the gain of all 500 models with random superorbital periods (800-4000 d; 99th percentile 1.1 %).
   But the 95 % block-bootstrap interval of the gain is -1.4 % to 16.4 %, because the residuals are red.
2. The gain comes from the superorbital change of the orbital light-curve shape (orbital sidebands at k/P1 +- 1/P_so).
   The sidebands-only model gives 3.8 % (95 % interval 0.8 % to 8.2 %). The mean-flux sinusoid alone gives 1.7 % (-6.9 % to 11.7 %).
3. The orbital phase of the GeV peak moves with superorbital phase in the same pattern in both decades (Figure 1).
   The peak is near orbital phase 0.44-0.50 at superorbital phase 0.06 and near 0.30-0.31 at superorbital phase 0.56, in both halves.
   The orbital amplitude is small near superorbital phase 0.2-0.3 and large near 0.56, in both halves.
4. The orbit-averaged mean-flux cycle became weaker. Its amplitude decreased from 0.92 to 0.47 (1e-7 ph cm-2 s-1). Its phase did not change clearly (shift 0.08 +- 0.07 cycles).
   Inside 2017-2026 alone, the full model prefers a 1417 d period. This is outside the 95 % range of simulations with a 1667 d clock (1525-1841 d with 60-bin blocks, 1525-1874 d with 120-bin blocks).
   The sidebands-only scan of 2017-2026 gives 1583-1654 d, and the full 2008-2026 data give 1671 d.
   Thus the orbital-shape modulation is consistent with a stable 1667 d clock, but the mean-flux part is not a stable periodic signal.
5. The forecast skill did not decrease with lead time. It was -9.4 % in 2017-2019, then +7.2 %, +9.4 % and +11.9 % in the next three half-cycle blocks (to 2026-10).
6. We give a registered forecast for each orbit from 2026-11 to 2029-12 (files/results/forecast_2026_2029.csv).

## Data

- Source: Fermi-LAT Light Curve Repository (Abdollahi et al. 2023), 4FGL J0240.5+6113, photon flux 0.1-100 GeV.
  The main data are 3-day bins with a fixed photon index and TS >= 4. We also used weekly and monthly bins and free-index fits as checks.
  The span is 2008-08-05 to 2026-10-30 (bin centres MJD 54684.5-61344.5).
- Controls: 24 LCR sources (mostly blazars) within 15 deg of LS I +61 303. We used the 6 controls with at least 300 detected bins and at least 100 bins in each period.
- We did not bundle the per-bin LCR fluxes. files/provenance/lcr_download_manifest.json gives the exact URLs, byte counts and SHA-256 hashes.
  files/code/run_all.sh downloads the data again into local scratch. See files/NOTICE-external-data.md.
- Times are bin centres. MJD = 51910 + MET/86400. The 3-day bins start on 2008-08-05 00:00 UTC.

## Quality control (plan amendment 1)

The first run gave absurd fluxes after 2018 (up to 2.4e-2 ph cm-2 s-1). These bins come after the 2018-03-16 Fermi solar-array anomaly.
The same bins also have high fluxes in the control sources. In these fits the isotropic background normalisation is at its 0.01 floor, or the Galactic normalisation is far from 1.
We kept only bins with 0.3 <= EG <= 2.5 and 0.85 <= GAL <= 1.10 (the 0.5-99.5 percentile range before 2018-03-16).
This rule uses only fit-quality fields, not forecast scores. It removed 42 of 2159 converged bins (2 before the anomaly). Figure 4 shows the removed bins.
We wrote this amendment into files/PLAN.md before the second run.

## Method

- Ephemerides (fixed before the test): P1 = 26.4960 d, P_so = 1667 d, zero phase MJD 43366.275 (JD 2443366.775, Gregory 2002); P2 = 26.935 d (second period of the beat model; Massi & Jaron 2013 and later papers give values near 26.92-26.94 d, and Chernyakova et al. 2023 give 26.932 d above 1 GeV).
- Models (weighted least squares on flux, weights 1/sigma^2, fitted on 2008-2016 only):
  - M0: constant.
  - M1: orbital Fourier series, 3 harmonics of P1 (7 parameters).
  - M2: M1 plus one sinusoid at P_so (mean-flux cycle).
  - M3: orbital harmonics whose coefficients change sinusoidally with superorbital phase. The frequencies are 1/P_so and k/P1 + j/P_so for k = 1..3 and j = -1, 0, +1 (21 parameters).
  - M4: beat model with 3 harmonics of P1 and 3 harmonics of P2 (13 parameters).
  - M5: analog model; the mean training flux in 10 x 10 cells of orbital phase x superorbital phase.
- Score: 2017-2026 skill = 1 - (weighted MSE of model) / (weighted MSE of M1).
- Null: M3 with 500 random superorbital periods (uniform in frequency, 800-4000 d, without 1450-1900 d).
- Uncertainty: moving-block bootstrap of the 2017-2026 bins (blocks of 60 bins = 180 d, 4000 draws).
- Coherence: period scans of the M3 gain for each half and for all data. We simulated each half as the 1667 d M3 fit of that half plus block-resampled residuals (300 draws; 60-bin and 120-bin blocks) and scanned again.
- Superorbital-phase-resolved profiles: in 8 superorbital-phase bins we fitted a mean and the first orbital harmonic. We give the mean flux, the amplitude and the orbital phase of the peak. Bin bootstrap gives the errors.

## Results

Test-period (2017-2026, 1103 bins) weighted MSE (units (1e-7 ph cm-2 s-1)^2, relative to the bin errors):

| Model | Parameters | 2008-2016 fit wMSE | 2017-2026 wMSE | Skill vs M1 |
| --- | --- | --- | --- | --- |
| M0 constant | 1 | 5.359 | 5.079 | -18.6 % |
| M1 orbital | 7 | 4.425 | 4.284 | 0 |
| M2 orbital + mean sinusoid | 9 | 4.026 | 4.210 | +1.7 % |
| M3 orbital x superorbital | 21 | 3.782 | 4.035 | +5.8 % (95 %: -1.4 to 16.4) |
| M3 sidebands only (no mean sinusoid) | 19 | - | - | +3.8 % (95 %: 0.8 to 8.2) |
| M4 two-period beat (P1, P2) | 13 | 4.204 | 4.173 | +2.6 % |
| M5 analog cells | 100 | 3.365 | 4.646 | -8.5 % |

- The in-sample gain of M3 over M1 is 14.5 % in 2008-2016. The gain of M3 refitted inside 2017-2026 at 1667 d is 8.7 %. The frozen model kept 5.8 %, about two thirds of the gain that was available in 2017-2026.
- The unweighted skill of M3 is +2.8 %.
- Data variants (M3 skill): weekly fixed index 5.2 %, 3-day free index 5.9 %, weekly free index 4.7 %, monthly 6.4 %, 3-day with upper limits as half values 5.8 %, extra removal of 6 bins above 2e-6 ph cm-2 s-1 5.9 %, without 2018-2019 8.8 %.
- Random-period null: 0 of 500 periods reached 5.8 %. The null median is -3.5 %, the 95th percentile is 0.8 %.
- Controls: with the same frozen ephemerides, M3 was worse than M1 for 5 of 6 control sources (skill -28 % to +2.5 %). The orbital model M1 had no skill for any control (-4.3 % to -0.4 % vs constant).
- Period scans (Figure 3): best period 1759 d for 2008-2016 (simulation 95 % range for a 1667 d clock: 1508-1796 d with 60-bin blocks), 1417 d for 2017-2026 (range 1525-1841 d; 0 to 0.7 % of simulations at or below 1417 d), 1671 d for 2008-2026.
  With a linear trend term the 2017-2026 best period stays at 1419-1423 d. Without the mean-flux sinusoid (sidebands only) it is 1583 d (3-day) or 1654 d (weekly).
- Residual periodograms after removal of the orbital model show the strongest peak at 26.93-26.95 d in both halves and a second peak at 26.06 d. These are the two superorbital sidebands of P1 (26.92 d and 26.08 d).
  The power near 26.3 d, which a 2024 paper reported as a new signal (arXiv:2406.02042), is weak in both halves (0.002 and 0.008, compared with 0.039 at 26.93 d). We did not test that claim in a formal way.
- Yearly mean flux was 8.1 +- 0.6 (1e-7) in 2009-2016 and 7.5 +- 0.5 in 2017-2025 (standard deviation of the yearly means).

## Interpretation

The GeV orbital light-curve shape of LS I +61 303 follows the radio superorbital clock: a model frozen in 2016 predicts the shape for about two more superorbital cycles.
This agrees with models in which a structure with the superorbital period changes where along the orbit the GeV emission peaks. Examples are a precessing jet (Massi & Jaron 2013) or a rotating non-axisymmetric Be disk (Xing et al. 2017).
Our test cannot separate these models. The sideband frequencies of M3 and the P2 of the beat model differ by only 0.1 cycle over 18 years.
The two-period beat model with only P1 and P2 terms (M4) predicted less well than M3. This is because M3 also contains the k/P1 + 1/P_so sideband (26.08 d), which is present in both halves.
The orbit-averaged GeV flux cycle is less stable. Its amplitude decreased by half, and inside 2017-2026 it prefers a shorter period. Changes in the Be-star disk can cause such non-periodic slow changes, but we did not test this.

## Limitations

- The bootstrap interval of the main 5.8 % gain includes zero (P(skill <= 0) = 0.056). Only the sidebands-only gain has an interval above zero. We added the sidebands-only decomposition after the main test; it was not in the plan.
- The quality-control rule was added after the first run. It uses only fit-quality fields, but other undetected exposure artefacts after 2018 can remain. Removal of 2018-2019 increased the skill.
- The LCR uses one fixed analysis (0.1-100 GeV, 12 deg region, fixed nearby sources). We did not do our own likelihood analysis, and we did not test energy dependence. Chernyakova et al. (2023) report that P1 dominates below 0.3 GeV and the 26.93 d period above 1 GeV.
- 3-day bins smooth the orbital profile (bin width 0.11 in orbital phase). Bin centres can be wrong by up to 1.5 d for partly empty bins.
- The test period covers only about 2.2 superorbital cycles. Period values from one half have a resolution of a few hundred days.
- The simulations for the period test use block-resampled residuals. They can underestimate long-timescale red noise.
- We used weighted least squares on flux. The LCR errors are asymmetric; we used the mean half-width.

## Reproduction

1. Run `bash files/code/run_all.sh /path/to/scratch` with Python 3.12, numpy 2.5.4, astropy 8.0.2 and matplotlib 3.11.2.
2. The script downloads the LCR light curves and the pyLCR source list into scratch, runs all analysis steps and writes JSON results and figures into scratch.
3. Compare the new manifest hashes with files/provenance/lcr_download_manifest.json. The LCR adds new bins and can reprocess old bins, so a later download can give slightly different numbers.
4. The results that we used are in files/results/. The figures are in files/figures/.

Files:
- files/PLAN.md: the plan written before the test, with amendment 1.
- files/code/: lcr.py (helpers, ephemerides, QC rule), 00_get_lcr.py (download), 01_forecast.py (main test), 02_null_scan.py (null, bootstrap, scans, controls), 03_phase.py (phase-resolved profiles, sub-periods, data variants), 04_extra.py (yearly means, residual periodograms), 05_forecast_next.py (2026-2029 forecast), 06_figures.py, 07_period_sim.py, 08_scan_variants.py, 09_sideband_skill.py, 10_outlier_sens.py, run_all.sh.
- files/results/: JSON outputs of each step; forecast_2026_2029.csv (per orbit: predicted orbital phase and amplitude of the first harmonic, peak date and flux, mean flux).
- files/figures/: Figures 1-5.

## Provenance

- Job sci-1107-dell-astronomy-406dd7656f94, campaign 11_07_2026, topic astronomy, machine dell, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), running as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data retrieved 2026-11-10 UTC from the Fermi LCR. Analysis run on 2026-11-10 UTC.

## References

- Gregory P. C. 2002, ApJ 575, 427 (radio 1667 d period and ephemeris), doi:10.1086/341257.
- Massi M., Jaron F. 2013, A&A, doi:10.1051/0004-6361/201219685, arXiv:1303.2007 (beat model, P2).
- Ackermann M. et al. 2013, ApJL 773, L35, arXiv:1307.6384 (GeV superorbital variability).
- Xing Y., Wang Z., Takata J. 2017, ApJ, doi:10.3847/1538-4357/aa9b36, arXiv:1704.02091 (GeV superorbital modulation, rotating disk).
- Simultaneous long-term monitoring of LS I +61 303 by OVRO and Fermi-LAT, 2018, MNRAS, doi:10.1093/mnras/sty1037, arXiv:1804.07692.
- Chernyakova M. et al. 2023, arXiv:2306.05954 (energy-dependent periods).
- arXiv:2406.02042 (2024; new 26.3 d GeV signal).
- Abdollahi S. et al. 2023, ApJS 265, 31, arXiv:2301.01607 (Fermi LAT Light Curve Repository).
