# Kepler phase tracking of 154 hump-and-spike A and F stars gives spike coherence times near 1,000 days, not the 1.5-day or 30-day spot lifetimes from autocorrelation fits

## Summary

Many A and F stars in Kepler data show a "hump and spike" pattern in the frequency spectrum. The hump is a group of Rossby (r) modes. The spike is a sharp peak at the rotation frequency. The cause of the spike is not known. One explanation is a star spot that a weak, dynamo-generated magnetic field makes. A second explanation is an overstable convective (OsC) mode of the core. Published lifetimes of the spike disagree by a factor of 20. Trust et al. (2020) fitted autocorrelation functions (ACFs) of the light curves and found mean spot decay times of 1.5 d (normal A stars) and 3.6 d (Am/Fm stars). Henriksen et al. (2023) fitted ACFs of band-passed light curves and found a mean spike lifetime of about 30 d. Trust et al. interpreted their values as spot decay times. Henriksen et al. used their short lifetimes as evidence for dynamo-generated spots and against OsC modes.

We did a direct test. A signal with a lifetime of tau loses its phase within a few tau. Thus we measured the phase of the spike in 30-day segments of the 4-year Kepler light curves at one fixed frequency, and we calculated the correlation of the segment amplitudes as a function of the time lag. For each star we injected strictly periodic signals and signals with known lifetimes (1.5 to 3,000 d) into the star's own light curve, and we ran the same analysis on them.

Main results for 154 stars with a spike signal-to-noise ratio (S/N) of 8 or more:

1. **The spike keeps its phase for much longer than 30 d.** At lags of 500 to 1,500 d, 133 of 154 spikes (86%) keep more phase correlation than all injected signals with a 30-d lifetime can give (3-sigma test). 146 of 154 (95%) reject a 1.5-d lifetime.
2. **Typical coherence times are hundreds to thousands of days.** The fitted coherence time has a median of 959 d (quartiles 420 and 2,285 d). Injections show that this estimator recovers true lifetimes of 300 d and 1,000 d as 294 d and 1,069 d.
3. **Some spikes are strict clocks over the Kepler mission.** 22 of 154 spikes (14%) agree with a strictly periodic signal over 4 years. 21 (14%) lose phase faster than a 300-d lifetime allows.
4. **The phase loss is mostly not a smooth change of the spin frequency.** A linear frequency drift does not restore the phase of most stars. The phase residuals wander.
5. **The two ACF methods do not measure the spike.** The whole-light-curve ACF gives almost the same decay time when we remove the spike and its harmonics (median 5.6 d with the spike, 5.7 d without it; Spearman rho = 0.69 between the two). The band-passed ACF lifetime changes by a factor of 4.4 when the band half-width changes from 0.005 to 0.05 per day, and it falls towards the value of the data without the spike when the band includes the r-mode hump. A strictly periodic spike with white noise gives band-passed lifetimes of about 1,400 to 1,550 d.
6. **The spike is not light from a contaminating star.** No star shows a Kepler-season pattern in the quarter amplitudes of the spike (0 of 154 at p < 0.01).

Conclusion: in the tested sample, the spike is a long-lived signal. Its coherence time is near 1,000 d, which is 30 to 600 times the published ACF lifetimes. A model for the spike must give a surface or mode feature that keeps its phase for years, and in 14% of the stars for more than the full 4 years. Short-lived dynamo spots that live for days or weeks do not agree with these data. Long-lived magnetic features or coherent (self-excited) modes are possible. The ACF decay times in the earlier studies come mostly from other variability (r modes, other pulsations and noise), not from the spike.

## Question

The published lifetimes of the spike in hump-and-spike stars (1.5 d, 3.6 d, about 30 d) come from fits of the ACF envelope. Does the spike really lose its phase on these time scales, when we measure its phase directly?

## Prior work and what is new

- Saio et al. (2018) explained the hump as r modes and the spike as rotational modulation (spots) or OsC modes.
- Balona (2013) listed Kepler A stars with this characteristic periodogram. Trust et al. (2020) measured spot sizes and ACF decay times for 170 hump-and-spike stars. Henriksen et al. (2023) measured ACF spike lifetimes for 162 stars. Antoci et al. (2025) studied HR 7495 in detail and favoured spots.
- The SCI campaign record has no earlier work on hump-and-spike stars. Two campaign studies use related phase-coherence logic: magnetic Ap/Bp rotation signals keep their phase over 30 years (sci:sha256:825c1a9d...), and long secondary periods of red giants lose phase (sci:sha256:719b8a6d...).
- New in this work: (1) a direct phase-coherence measurement of the spike for 154 stars, (2) per-star injection calibration with strictly periodic and finite-lifetime signals, (3) a test of the two published ACF methods on the same data with the spike removed and with a synthetic strictly periodic spike, (4) a season test for contamination.

## Data

- Sample: 174 Kepler stars. 131 normal A stars and 39 Am/Fm stars from Trust et al. (2020, tables A1 and A2; this list includes most of the Balona 2013 hump-and-spike stars), and 4 more stars from the first 10 rows of Henriksen et al. (2023, Table A1; the full table is only in the online supplement). The catalogue tables come from the CfA VizieR mirror and arXiv (see `files/provenance/DATA_NOTICE.md`).
- Light curves: Kepler DR25 long-cadence PDCSAP flux, quarters 1 to 17 (Q0 is not used), from the public STScI bucket. 2,992 FITS files (1.25 GB). Each file's name, URL, size and SHA-256 hash is in `files/provenance/kepler_file_manifest.csv`.
- We did not put the light curves or the catalogue tables in this bundle. `files/code/00_fetch_tables.sh` and `files/code/02_download.py` retrieve them into a scratch folder.

## Method

All code is in `files/code/`. The shared functions are in `lib.py`.

1. **Light curve.** We keep quality-0 PDCSAP points, convert each quarter to ppm, remove a cubic trend per quarter and clip 5-sigma outliers.
2. **Spike frequency.** The spike is the highest peak within +-0.005 per day of the published spike frequency (Trust et al.; else Henriksen et al.), refined on a fine grid. S/N is the peak amplitude divided by the median amplitude 0.08-0.40 per day above the spike.
3. **Segment amplitudes.** We cut each light curve into 30-day segments (at least 60% coverage). In each segment we fit a constant, a linear trend and sinusoids at f and 2f, with f fixed. The complex amplitude z = a + ib of the fundamental gives the phase.
4. **Lag correlation.** For all pairs of segments, C(lag) = Re sum(z_j conj(z_k)) / sqrt(sum|z_j|^2 sum|z_k|^2), in lag bins from 20 to 1,500 d.
5. **Null and calibration.** We add to the star's own light curve (a) a strictly periodic sinusoid with the spike amplitude, 8 times, at 0.25 and 0.32 per day above the spike (outside the hump), and (b) signals whose complex amplitude follows an Ornstein-Uhlenbeck process with e-folding time tau = 1.5, 10, 30, 100, 300, 1,000 and 3,000 d, 6 times each, with the rms segment amplitude of the spike. We run steps 3-4 on each injected signal.
6. **Statistics.** R_long is the pair-weighted C at lags of 500-1,500 d divided by the same quantity for the strictly periodic injections. A star rejects a lifetime tau if R_long is more than the mean plus 3 standard deviations (minimum 0.05) of the injections with that tau. A star agrees with a strictly periodic signal if R_long is more than the coherent mean minus 3 standard deviations (minimum 0.05). The coherence time tau_fit is a weighted least-squares fit of C/C_coherent = exp(-lag/tau) over all lag bins.
7. **Lorentzian width.** We fit a Lorentzian to the power spectrum within +-0.02 per day of the spike.
8. **ACF replication** (`04_acf.py`). (a) Whole light curve: ACF on a uniform grid with zero-filled gaps, fit of the Giles et al. (2017) model exp(-t/tau)(A cos(2 pi t/P) + B cos(4 pi t/P)) + y0 for lags up to 20 d and 60 d. (b) Band-passed light curve: we keep Fourier components within n f +- df (n = 1-4; df = 0.005, 0.01, 0.02, 0.05 per day), compute the ACF up to 150 d, fit the same model and report 2 tau as in Henriksen et al. We apply both methods to the real data, to the data with a 4-harmonic strictly periodic spike model removed, and to that model plus white noise with the star's residual scatter.
9. **Drift or wander** (`08_phase_drift.py`). We unwrap the segment phases and fit a line and a quadratic (a linear change of frequency). We give the von Neumann ratio of the residuals (2 for uncorrelated noise; less than 2 for a smooth wander) and R_long after we remove the quadratic phase.
10. **Season test** (`05_season.py`). One amplitude per quarter; one-way ANOVA of the amplitudes by Kepler season (quarter mod 4). Light from a contaminating star changes with the aperture, and the aperture changes with the season.
11. **Sensitivity.** We repeated the coherence analysis with the highest peak within +-0.04 per day of the catalogue frequency (`files/results/wide/`).

## Results

### Coherence of the spike

| Quantity (S/N >= 8, n = 154) | Value |
| --- | --- |
| Reject lifetime 1.5 d | 146 (95%) |
| Reject lifetime 30 d | 133 (86%) |
| Reject lifetime 100 d | 79 (51%) |
| Reject lifetime 300 d | 21 (14%) |
| Agree with strictly periodic signal over 4 yr | 22 (14%) |
| R_long median (quartiles) | 0.54 (0.34, 0.72) |
| tau_fit median (quartiles) | 959 d (420, 2,285 d) |
| tau_fit 10th and 90th percentiles | 160 d, 4,751 d |
| Lorentzian FWHM below 1/T (unresolved in 4 yr) | 70% |
| Lorentzian FWHM below 1/(pi x 100 d) | 96% |

Injection calibration (median over stars of the median recovered tau_fit): 1.5 d -> 6 d; 10 d -> 21 d; 30 d -> 43 d; 100 d -> 106 d; 300 d -> 294 d; 1,000 d -> 1,069 d; 3,000 d -> 4,429 d. Values below about 30 d are not resolved with 30-day segments. The estimator is reliable from 100 to 1,000 d.

Figure 1 (`files/figures/fig1_examples.png`) shows three stars. Figure 2 (`fig2_long_lag_coherence.png`) shows R_long against S/N with the injection references. Figure 3 (`fig3_lag_correlation.png`) shows the median lag curve. It falls from 0.83 at 40 d to about 0.55 at 400 d and then stays near 0.55-0.63 to 1,300 d. A single exponential lifetime does not give this shape. The data agree better with a long-lived coherent part of the spike plus a part that loses phase in some hundred days. Part of the early drop can also come from r-mode power that leaks into the 30-day fits (see Limitations).

Other results:

- Normal A and Am/Fm stars do not differ (median R_long 0.54 and 0.60; Mann-Whitney p = 0.98). Trust et al. found different ACF decay times for these two groups (1.5 and 3.6 d).
- R_long does not correlate with the Trust et al. ACF decay time (Spearman rho = 0.15, p = 0.06, n = 150) or with Teff (rho = -0.15, p = 0.06).
- R_long decreases with spike frequency (rho = -0.35, p = 7e-6): median 0.66, 0.55 and 0.41 in the frequency terciles 0.51-1.07, 1.07-1.49 and 1.49-2.75 per day. R_long also increases with S/N (rho = 0.29), as expected from noise.
- For the 10 stars with published Henriksen et al. lifetimes (15-38 d), 7 reject a 30-d lifetime; their tau_fit values are 28 to 14,800 d.
- Drift or wander: for the 97 stars with phase scatter below 0.15 cycles, a quadratic phase (linear frequency change) gives R_long > 0.8 for 23%, against 20% without it. The median von Neumann ratio of the residuals is 1.25. Thus the remaining phase changes are correlated in time (a wander), not white noise around a smooth spin-down or spin-up.
- Sensitivity: with the wider +-0.04 per day peak search, 162 stars pass S/N >= 8; 81% reject a 30-d lifetime, 94% reject 1.5 d and 14% agree with a strictly periodic signal. In 28 stars the wide search picks a different peak, mostly a peak in the hump 0.02-0.04 per day below the published spike; these hump peaks are less coherent.
- Spike amplitudes change from quarter to quarter (median coefficient of variation 0.41), but not with the Kepler season (0 of 154 stars at p < 0.01).

### Replication of the ACF methods

| ACF method (median over 154 stars) | real data | spike removed | strictly periodic spike + white noise |
| --- | --- | --- | --- |
| Whole light curve, tau (fit to 20 d) | 5.6 d | 5.7 d | 21 d |
| Whole light curve, tau (fit to 60 d) | 6.1 d | 5.9 d | 157 d |
| Band-pass 2 tau, df = 0.005 per day | 488 d | 209 d | 1,547 d |
| Band-pass 2 tau, df = 0.01 per day | 455 d | 161 d | 1,457 d |
| Band-pass 2 tau, df = 0.02 per day | 411 d | 158 d | 1,357 d |
| Band-pass 2 tau, df = 0.05 per day | 110 d | 40 d | 1,371 d |

Figure 4 (`fig4_acf_replication.png`) shows these results. Our implementations do not give the published numbers exactly (for example, our whole-light-curve tau values do not correlate positively with those of Trust et al.: rho = -0.16). The published papers do not give all fit settings (lag range, band widths per star, prewhitening stop criterion). The pattern is clear in our implementation: the whole-light-curve ACF decay does not depend on the spike, and the band-passed lifetime depends on the band width and on the r-mode power inside the band. A strictly periodic spike gives long ACF lifetimes in both methods; the light-curve length limits them.

## Interpretation

A spot or a mode with a lifetime of 1.5 d or 30 d cannot keep phase correlation over 500 to 1,500 d. Most spikes do. Thus the short published lifetimes are not lifetimes of the spike. They are decay times of the total variability within the analysed band or light curve.

What can make a signal that keeps its phase for about 3 years, and in some stars for more than 4 years? (a) A long-lived surface magnetic feature. Fossil-field spots of Ap stars keep their phase for decades (sci:sha256:825c1a9d...); the spikes are much less stable than that, but much more stable than solar-type spots. Long-lived active longitudes are another possibility. (b) A self-excited, saturated mode. An overstable mode can be coherent; the OsC test of Henriksen et al. that used the ACF lifetimes and the convective turnover time therefore does not apply. Our data cannot separate these two possibilities. They do show that a spike model needs a coherence time near 1,000 d, a slow random phase wander and amplitude changes of about 40% between quarters.

## Limitations

- **Hump leakage.** The r-mode hump is often less than 0.03 per day below the spike. A 30-day segment cannot resolve it, so hump power adds incoherent power to the segment amplitudes. This decreases C and R_long. Thus R_long is a lower limit of the coherence of the spike itself, and the true coherence times can be longer. It cannot make a short-lived spike look coherent.
- **Injection model.** The finite-lifetime injections are Ornstein-Uhlenbeck amplitudes at a fixed frequency. Real spots can also change frequency (differential rotation) and shape. The strictly periodic injections are at 0.25-0.32 per day above the spike, where there is no hump; thus the coherent null is optimistic for stars with a strong hump next to the spike.
- **Small number of injections.** Six injections per lifetime per star give approximate thresholds. We used a minimum standard deviation of 0.05 to make the test conservative.
- **ACF replication.** We could not reproduce the published ACF values exactly. Our conclusions about the ACF methods are about these methods as we implemented them from the published descriptions.
- **Sample.** The sample is the published hump-and-spike lists; it selects stars with clear spikes. 20 of 174 stars have S/N < 8 and are not in the statistics. The Henriksen et al. sample is represented by only 10 stars (the public rows).
- **One mission.** All data are Kepler (2009-2013). Coherence over more than 4 years is not tested. TESS data can extend the test for the brightest, most coherent stars; we did not do this.
- **Mechanism.** The test does not identify the cause of the spike.

## Open questions for later work

- Extend the phase test to TESS (2019-2026) for the 22 strictly periodic spikes. For the highest-S/N stars the 4-year Kepler frequency can possibly predict the phase across the 2013-2019 gap; this needs a check of the frequency errors and of the TESS noise at 10-50 ppm.
- Model the r-mode hump together with the spike (for example, with a Lorentzian sum for the hump) to remove the leakage and get the true spike coherence times.
- Look for a relation between spike coherence and the hump-spike frequency spacing, which measures the rotation and possibly differential rotation.
- Spectropolarimetry of the strictly periodic spike stars (list in `files/results/main/coherence_per_star.csv`, column `consistent_coherent`).

## Files

- `files/results/main/coherence_per_star.csv`: per-star measurements (spike frequency, amplitudes, S/N, C ratios, injection references, tau_fit, test results). Only our measurements, the KIC number and the source table group are included.
- `files/results/main/per_star_json/<KIC>.json`: complete per-star output, with segment times, complex amplitudes, lag curves and all injection results.
- `files/results/main/summary.json`: all statistics in this README.
- `files/results/main/acf_replication_per_star.csv`, `season_check_per_star.csv`, `phase_drift_per_star.csv`: per-star results of the ACF replication, the season test and the drift test.
- `files/results/wide/`: the sensitivity analysis with the +-0.04 per day peak search (same code with SPIKE_HALF=0.04; run before the final main run, so a rerun can differ in the last digits).
- `files/results/sample_kic_group.csv`: the 174 KIC numbers and their source group.
- `files/figures/`: figures 1-5 (figure 5: Lorentzian widths).
- `files/provenance/`: data notice and the Kepler file manifest with SHA-256 hashes.

## Reproduction

`sh files/code/run_all.sh SCRATCH_DIR` downloads the catalogue tables and 2,992 Kepler files (about 1.2 GB) into SCRATCH_DIR, and runs all steps with 2 processes. It takes about 1.5 hours on 2 CPUs plus the download time. Keep SCRATCH_DIR outside this publication folder. The random seeds depend on the KIC number, so the reruns give the same numbers. Software: Python 3.12, numpy, scipy, pandas, astropy and matplotlib.

## Provenance

- Job sci-1107-dell-astronomy-8fb8c67df5a9, campaign 11_07_2026, topic astronomy, machine dell, account claude-myxtap. Analysis date 2026-11-12.
- Model: Claude Opus 5.5 (claude-opus-5-5), an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data: Kepler DR25 (NASA/MAST, public); catalogue tables from VizieR (CfA mirror) and arXiv, cited below and not redistributed.

## References

- Antoci, V. et al. 2025, A&A, HR 7495 hump-and-spike study, arXiv:2502.11879.
- Balona, L. A. 2013, MNRAS 431, 2240 (Activity in A-type stars).
- Cantiello, M. & Braithwaite, J. 2019, ApJ 883, 106.
- Giles, H. A. C. et al. 2017, MNRAS 472, 1618.
- Henriksen, A. I. et al. 2023, MNRAS 520, 216, doi:10.1093/mnras/stad153, arXiv:2301.04974.
- Lee, U. & Saio, H. 2020, MNRAS 497, 4117.
- McQuillan, A. et al. 2013, MNRAS 432, 1203.
- Saio, H. et al. 2018, MNRAS 474, 2774.
- Santos, A. R. G. et al. 2021, MNRAS 508, 267.
- Trust, O. et al. 2020, MNRAS 492, 3143, doi:10.1093/mnras/stz3623.
