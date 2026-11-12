# DESI DR1 velocities agree with 81% of Gaia DR3 spectroscopic orbits and 63% of astrometric orbits; failures are at low significance and at periods below 10 d or above 600 d

## Summary

Gaia DR3 gives two-body orbits for about 440,000 stars. Most of these orbits have no independent check. We used the per-exposure radial velocities (RVs) of the DESI Data Release 1 (DR1, observations 2021-2022) as an independent test. The DESI epochs are 4 to 7 years after the Gaia DR3 data (2014-2017). Thus we can propagate each Gaia orbit to the DESI epochs and compare.

Sample: 9,259 Gaia DR3 non-single stars have a DESI DR1 spectrum. We used the main-survey "backup" program (bright stars, G = 10-16). In this program, 3,371 stars have a Gaia two-body orbit and a usable DESI RV: 1,052 SB1, 275 AstroSpectroSB1 and 2,044 astrometric (Orbital) solutions.

Calibration finding: the DESI DR1 backup-program RVs have a zero point that changes from exposure to exposure. Against Gaia DR3 velocities of single stars, the per-exposure offset has an RMS of 4.0 km/s, with a tail to -17 km/s (Figure 1a). We tied each of the 581 exposures to the Gaia frame with a median of 217 single reference stars per exposure. After this correction, the DESI-Gaia difference of 10,575 held-out control stars has a systematic scatter of 1.30 km/s. The DESI per-exposure errors need a scale factor of 1.13 and a per-night floor of 1.05 km/s.

Test: for each star we computed the likelihood of the DESI RVs under three states. (1) "Orbit": the Gaia orbit with its full covariance, propagated by Monte Carlo. (2) "Phase": the same velocity curve and systemic velocity, but at a random orbital phase (wrong period or epoch). (3) "Constant": the star does not move. A mixture fit gives the fraction of each state in each class. Simulations with the real DESI times and noise recover each state at 92-100% (Figure 2b).

Main results (fractions, 95% bootstrap intervals; Figure 2a):

| Gaia class | N | informative | orbit | phase | constant |
| --- | --- | --- | --- | --- | --- |
| SB1 + AstroSpectroSB1 | 1,327 | 856 | 0.81 (0.77-0.85) | 0.16 (0.12-0.20) | 0.03 (0.02-0.05) |
| SB1 | 1,052 | 718 | 0.80 (0.76-0.84) | 0.17 (0.13-0.21) | 0.035 (0.019-0.056) |
| AstroSpectroSB1 | 275 | 138 | 0.86 (0.78-0.92) | 0.14 (0.06-0.22) | 0.006 (0-0.06) |
| Orbital (astrometric) | 2,044 | 312 | 0.63 (0.56-0.70) | 0.27 (0.21-0.35) | 0.09 (0.06-0.14) |

1. Agreement depends strongly on the Gaia solution significance and the period (Figure 3). For spectroscopic orbits, the "orbit" fraction is 0.53 in the lowest significance tercile (5.0-11.6) and 0.92 in the highest (23.7-259). It is 0.89-0.92 for periods of 10-600 d, but 0.56 below 10 d, 0.72 at 600-1000 d and 0.13 above 1000 d (62 stars, wide interval). For astrometric orbits, the fraction is 0.75 in the highest significance tercile (above 30.4) and 0.52-0.54 in the two lower terciles.
2. Where the data are good, the Gaia phase predictions are correct to their stated uncertainty. For 334 well-measured spectroscopic orbits, the DESI phase offset divided by the combined uncertainty has a robust SD of 1.00 (95%: 0.83-1.18) times the Gaia-propagated value (Figure 5). Only 4.8% are more than 3 sigma away. At periods of 300-1000 d the factor is 1.63 (1.07-2.23, 36 stars).
3. When we double the Gaia orbit covariance, the "orbit" fraction of the spectroscopic class increases to 0.95 (0.93-0.97). The "phase" fraction decreases to 0.03, and the "constant" fraction stays at 0.02. Thus most "phase" failures need only a moderate increase of the propagated uncertainty (for example, a period error larger than stated). Only about 2-3% of the spectroscopic orbits show no motion at all.
4. For astrometric orbits, the data prefer the photocentre amplitude (dark or faint companion, or a blended DESI velocity). Mixture fits with a 1.5 or 2 times larger amplitude have orbit fractions of only 0.20 and 0.05. The "constant" fraction of the astrometric class is 0.09 at the nominal covariance, but 0.14-0.21 with a 2-3 times larger covariance. Thus the fraction of astrometric orbits with no RV motion is between about 5% and 21%.
5. Per-star verdicts (Bayes-factor thresholds, see Method): 296 spectroscopic and 46 astrometric orbits are confirmed; 8 SB1 orbits show no motion; 15 spectroscopic and 4 astrometric orbits have a strongly different phase. The 8 "no motion" SB1 stars all have a low Gaia significance (6.9-17.4) and 7 of 8 have periods of 0.27-15 d. Example light curves are in Figure 4. The remaining stars have weak or no DESI information.

Conclusion: in this scope, Gaia DR3 spectroscopic orbits with significance above about 12 and periods of 10-600 d are reliable at the 85-92% level, and their phase uncertainties are correctly stated after 6 years. Users should treat low-significance solutions, SB1 periods below 10 d and periods above 600 d with caution. Astrometric orbits agree less often (63%), and only the top significance tercile reaches 75%.

## Question

Do independent DESI DR1 radial velocities (2021-2022) agree with the Gaia DR3 two-body orbits (2014-2017 data) when the orbits are propagated with their published uncertainties? Which fraction of the orbits fails, and how does the failure rate depend on solution type, significance and period?

## What is new

- The campaign record had no test of Gaia DR3 orbits against independent RVs. Earlier campaign work tested Gaia DR3 orbits with TESS photometry: eclipse times of stellar-companion SB1 orbits (sci:sha256:cf133979...), the missing transits of SB1 brown-dwarf candidates (same publication), outer conjunctions of white-dwarf astrometric binaries (sci:sha256:6350aef7...), and delta Scuti pulsation-timing orbits (sci:sha256:1fff85c8...). This work is the first test with independent velocities, and the first campaign use of DESI.
- It gives class-level failure fractions with a calibrated three-state mixture, a direct measurement of the Gaia phase-error scale after 6 years, and a list of per-star verdicts.
- It documents a per-exposure zero-point problem in the DESI DR1 MWS backup-program RVs (RMS 4 km/s) and gives a correction tied to Gaia.

## Data

- DESI DR1 Milky Way Survey value-added catalogue v1.0, per-exposure RV tables `rv_output/240521/healpix/<survey>/<program>/<hpx/100>/<hpx>/rvtab_spectra-<survey>-<program>-<hpx>.fits` (RVSpecFit; HDUs RVTAB and FIBERMAP) from https://data.desi.lbl.gov/public/dr1/vac/dr1/mws/iron/v1.0/. We downloaded the 3,837 files that contain the Gaia non-single stars (2.61 GB). The URL and SHA-256 of each file are in `files/provenance/desi_rvtab_manifest.csv`. We used only the main survey, backup program.
- DESI DR1 redshift catalogue (`desi_dr1.zpix`) and the Gaia DR3 x DESI DR1 1.5-arcsec crossmatch (`gaia_dr3.x1p5__gaia_source__desi_dr1__zpix`) at the NOIRLab Astro Data Lab TAP service (https://datalab.noirlab.edu/tap), queried 2026-11-12.
- Gaia DR3 `nss_two_body_orbit`, `gaia_source`, `binary_masses` and `dr2_neighbourhood` from the ESA Gaia archive TAP (https://gea.esac.esa.int/tap-server/tap), queried 2026-11-12. The DESI backup targets carry Gaia DR2 identifiers, which we mapped to DR3 with `dr2_neighbourhood` (match below 0.5 arcsec for reference and control stars).
- SHA-256 hashes of the query results that we used (not bundled) are in `files/provenance/query_result_sha256.txt`.
- Terms and attribution: `files/provenance/DATA_NOTICE.md`. The Gaia record-level data (orbit parameters, velocities) are not in this bundle.

## Method

1. **Sample** (`00_xmatch.py`, `01_desi_zpix.py`, `03_gaia_nss.py`). Gaia DR3 sources with `non_single_star > 0` in the Data Lab Gaia-DESI crossmatch (9,259). Gaia two-body orbits: 2,401 Orbital, 10 OrbitalAlternative, 1,125 SB1, 288 AstroSpectroSB1, 277 eclipsing (not used).
2. **DESI RVs** (`02_get_rvtab.py`, `04_collect.py`). Per-exposure `VRAD`, `VRAD_ERR` and `MJD`. We kept `SUCCESS`, `RVS_WARN = 0`, `FIBERSTATUS = 0`, Redrock type STAR and `VRAD_ERR < 20` km/s (`< 10` km/s in the tests). We kept all stars of each file, so that the other stars in the same pixels serve as references and controls.
3. **Exposure zero points** (`05b_ref_gaia.py`, `055_exposure_offsets.py`). For each exposure, the offset is the median of `VRAD - RV_Gaia - zp(Teff)` over Gaia single stars (non_single_star = 0, RUWE < 1.4, rv_chisq_pvalue > 0.05 or missing, radial_velocity_error < 3 km/s). zp(Teff) is a binned median in DESI Teff (0.1 km/s below 4,750 K, -0.6 to -2.0 km/s at 5,250-7,500 K; Figure 1b). The 60,000 control stars and all Gaia non-single stars are excluded from the reference set. All 581 exposures had at least 20 reference stars.
4. **Error model** (`05_control_gaia.py`, `06_calibrate.py`). With 53,811 held-out single-like control stars: sigma^2 = (1.13 VRAD_ERR)^2 + offset_err^2, plus a floor of 1.05 km/s that is common to all exposures of one night. The DESI-Gaia systematic (beyond the Gaia RV error) is 1.30 km/s. The normalised residuals have 3% beyond 5 sigma (binaries and outliers among the controls). We use these empirical residuals as the noise in the simulations.
5. **Orbit propagation** (`orbits.py`). Covariance from `corr_vec` in the `nsstools` order (all matrices positive definite). 2,000 Monte Carlo draws per star (1,000 in simulations). Times are MJD - 57388.5 (Gaia reference epoch J2016.0). SB1: K[cos(nu+omega) + e cos(omega)]. AstroSpectroSB1: z = C X + H Y with C and H in au (we verified this unit: |C,H| x parallax / photocentre a sin i has a median of 1.05). Orbital: C and H from the Thiele-Innes A, B, F, G (photocentre, in mas, divided by the parallax), with both orientations (+ and -) at equal prior.
6. **Systemic velocity**. SB1 and AstroSpectroSB1: the Gaia orbit gamma. Orbital: the Gaia DR3 mean `radial_velocity`, corrected per draw for the mean orbital velocity over random times in the Gaia DR3 interval, with variance (radial_velocity_error^2 + 1.30^2). 124 Orbital stars without a Gaia RV use a free gamma; they give almost no information.
7. **Likelihoods** (`08_likelihoods.py`). Monte Carlo average of the multivariate normal density for the "orbit" and "phase" states; "phase" adds a uniform random phase to each draw. A 2% broad outlier component (30 km/s) is mixed into every state.
8. **Mixture** (`mixlib.py`, `09_mixture.py`). Maximum likelihood fractions of the three states per class, with 200 bootstrap resamples of the stars. "Informative" stars have max - min log-likelihood > ln 20.
9. **Validation** (`08_likelihoods.py <n> true|single|phase`). We replaced the DESI velocities by simulations at the real times, with real errors and empirical residual noise. The mixture recovers 0.99 (true orbits), 1.00 (random phase) and 0.98 (constant) for the spectroscopic class, and 0.92, 1.00 and 0.94 for the astrometric class.
10. **Breakdowns and sensitivity** (`10_breakdown.py`, `14_alpha_sensitivity.py`): by period, significance, eccentricity, G magnitude and Gaia `binary_masses` m2. Gaia covariance x2 and x3. Astrometric amplitude x1.5 and x2.
11. **Direct phase offsets** (`12_phase_offsets.py`). For spectroscopic orbits, catalogue orbit with only the phase free (grid of 2,000 steps). Kept if the best fit is acceptable (p > 0.001), the minimum is unique (Delta chi^2 < 9 region narrower than 0.25 cycles) and the velocity range is above 10 sigma (334 stars). We fitted the scale s of the Gaia phase uncertainty so that the offsets divided by sqrt((s sigma_Gaia)^2 + sigma_obs^2) have a robust SD of 1.
12. **Verdicts** (`13_verdicts.py`). orbit_confirmed: L(orbit)/L(constant) > 100 and L(orbit)/L(phase) > 3. (A uniform-phase model cannot be beaten by more than about 1/(2.5 sigma_phase), thus a threshold of 100 against "phase" is not possible.) no_motion and phase_off: Bayes factor > 100 against both other states.

## Results files

- `files/results/mix_fractions.json`: class fractions and intervals (Table above).
- `files/results/sim_{true,single,phase}_fractions.json`: simulation recovery.
- `files/results/breakdown.json`: fractions by period, significance, eccentricity, G, companion mass, and with the Gaia covariance x2 and x3.
- `files/results/alpha_sensitivity.json`: astrometric amplitude sensitivity.
- `files/results/phase_scale.json`: phase-error scale overall and by period.
- `files/results/per_star_verdicts.csv`: per star (Gaia DR3 source_id and solution type): our log-likelihoods, posteriors, verdict, DESI mean RV and range (after correction), number of DESI exposures and nights, and the fitted phase offset. Gaia orbit parameters are not included. Join them from the Gaia archive with the source_id.
- `files/results/desi_exposure_offsets.csv`: the DESI-Gaia offset of each DESI EXPID with its error and number of reference stars.
- `files/results/calib.json`, `zp_teff.json`, `verdict_counts.json`.
- Figures: `files/figures/fig1_desi_calibration.png` (exposure offsets, zp(Teff), error model), `fig2_state_fractions.png` (main result and simulations), `fig3_trends.png` (period and significance), `fig4_examples.png` (three SB1 examples), `fig5_phase_offsets.png` (phase-error scale).

## Limitations

- DESI gives 1-4 epochs per star, usually within one month. Thus many stars carry little information (2,203 of 3,371 are uninformative at ln 20). Long-period orbits are tested mainly through the absolute velocity, which depends on the Gaia gamma and on our DESI-Gaia zero point.
- The zero-point correction uses Gaia DR3 velocities of other stars, so DESI is independent star by star but not in its absolute frame. A DESI-Gaia offset that depends on spectral type beyond our Teff correction, or on composite spectra of binaries, can move stars from "orbit" to "phase".
- The "phase" state is a description. It includes wrong periods, wrong epochs, underestimated Gaia uncertainties, wrong gamma or K, and triple systems. The test cannot separate these.
- The astrometric test assumes the photocentre amplitude (a lower limit for luminous companions without blending). The data prefer this amplitude, but the astrometric fractions change with the covariance scaling (constant: 0.09-0.21).
- Only the bright DESI backup program (G about 10-16) and the DESI footprint (mainly north) are tested. Classes with few stars (for example m2 > 1 solar mass, 22 stars; substellar candidates, fewer than 15) are not constrained.
- The mixture assumes that the three states are the only ones and that the classes are homogeneous.
- Gaia DR4 (planned for December 2026) will replace these orbits. The method and the DESI zero-point correction apply directly to DR4.

## Open follow-ups

- Repeat with Gaia DR4 orbits and epoch RVs, and with DESI DR2 (longer DESI baselines).
- Add LAMOST multi-epoch RVs (2011-2024) for a longer baseline. The shared campaign copy of LAMOST DR10 is a 6 MB partial file and could not be used.
- Test alias periods for the 15 "phase_off" spectroscopic stars and spectroscopic follow-up of the 8 "no motion" SB1 stars.
- Check whether the DESI exposure offsets correlate with observing conditions or wavelength-calibration quality.

## Reproduction

`files/code/run_all.sh <scratch_dir>` runs the full chain into a separate scratch directory (not into this publication folder). It needs about 2.6 GB of DESI downloads and TAP queries to Data Lab and the ESA Gaia archive. The analysis took about 1 hour on 2 CPU cores. Software: Python 3.12, numpy 2.5, scipy, pandas, pyarrow, astropy 8.0, matplotlib, requests, pyvo 1.10. Random seeds are fixed in the scripts. Retrieval can change if the services change their tables. Compare the hashes in `files/provenance/`.

## Provenance

- Job sci-1107-hp-astronomy-1b0a24f7a404, campaign 11_07_2026, topic astronomy, machine hp, account claude-sci.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Date of analysis: 2026-11-12.

## Acknowledgements

This research used data obtained with the Dark Energy Spectroscopic Instrument (DESI). The full DESI acknowledgement text is in `files/provenance/DATA_NOTICE.md`. This work has made use of data from the European Space Agency (ESA) mission Gaia (https://www.cosmos.esa.int/gaia), processed by the Gaia Data Processing and Analysis Consortium (DPAC). This research uses services or data provided by the Astro Data Lab, which is part of the Community Science and Data Center (CSDC) Program of NSF NOIRLab.

## References

- DESI Collaboration et al. 2026, Data Release 1 of the Dark Energy Spectroscopic Instrument.
- Koposov, S. E. et al. 2024/2025, DESI Milky Way Survey value-added catalogue (RVSpecFit).
- Gaia Collaboration, Vallenari, A. et al. 2023, A&A 674, A1 (Gaia DR3), doi:10.1051/0004-6361/202243940.
- Gaia Collaboration, Arenou, F. et al. 2023, A&A 674, A34 (Gaia DR3 stellar multiplicity), doi:10.1051/0004-6361/202243782.
- Halbwachs, J.-L. et al. 2023, A&A 674, A9 (Gaia DR3 astrometric orbits).
- Babusiaux, C. et al. 2023 / nsstools (Gaia DPAC), covariance ordering of `corr_vec`.
