# Kepler phase-modulation orbits predict the TESS pulsation-delay changes of delta Scuti binaries, but not their absolute pulsation phases

## Summary

Murphy et al. (2018) found 341 binary orbits from the phase modulation (PM) of delta Scuti pulsations in 4 years of Kepler data (2009-2013). Each orbit is a forecast: the light-travel time delay of the pulsations must continue to follow the orbit after the Kepler mission. We tested this forecast with TESS 2-minute light curves from 2019 to 2024 (Kepler-field sectors 14-82).

We measured the pulsation phases of the same modes in Kepler and TESS for 25 PM binaries, 110 PM "single" stars and 11 PM "possible long-period" stars that have TESS 2-minute data and usable modes. We did not use TESS phases to select stars or modes.

Main results:

1. **Sign convention.** In the Kepler data, our measured delays follow the published orbits with the opposite sign to our convention (delay > 0 = later arrival). The Kepler regression slope is near -1 for 23 of 25 binaries (median -0.90). We fixed this global sign from Kepler data only.
2. **Delay changes inside the TESS era follow the published orbits.** For 24 binaries with two or more TESS sectors (75 sector pairs), the measured change of pulsation delay relative to the first TESS sector agrees with the change that the published orbit predicts: weighted slope 1.04 +- 0.07, weighted skill 0.32 against a no-orbit forecast. A placebo with a random periastron time per star reaches the observed weighted skill in only 0.46% of 5,000 draws (p = 0.005; placebo median -0.24, 95th percentile 0.18). All 12 pairs with a predicted change larger than twice the total error have the predicted sign, and the orbit is closer than "no change" for 10 of 12 (binomial p = 0.019).
3. **The success depends on how well the Kepler data constrain the orbit.** For 13 binaries where our own Kepler delays reproduce the published orbit (slope 0.5-1.5, correlation > 0.3, decided before the TESS comparison), the weighted skill is 0.90 and the slope is 1.07 +- 0.08. For the other 11 (orbits longer than the Kepler baseline, wrong-sign or near-circular cases, and stars whose modes disagree), the weighted skill is 0.03.
4. **Absolute pulsation phases do not carry over from Kepler to TESS for the binaries.** For single stars, the Kepler-extrapolated phase of the first TESS sector (8-13 years later) differs from the observed phase by a median of 0.031 cycles (149 s), and 82% agree within 3 sigma. For the binaries with the published orbit applied, the median difference is 0.125 cycles (658 s), no better than the no-orbit model (0.122 cycles). Small errors in the published orbits (mainly the period) and intrinsic phase drift accumulate over about 10 years.
5. **"Possible long-period" stars change faster than single stars.** Over lags of 60-800 days inside TESS, the median delay change per star is 241 s for 8 class-5 stars and 41 s for 89 single stars (Mann-Whitney p = 0.008). This agrees with long-period binarity, but 28% of single stars also change by more than 150 s, so it does not confirm individual binaries.

The unweighted pooled skill is near zero (-0.05) because a few stars with incoherent multi-mode phases (scatter between modes of 900-3,700 s) dominate a squared-error sum. We chose the error-weighted metric after we saw this. The weights use only the measurement errors, the published orbit errors and the drift of single stars, not the orbit residuals. The placebo uses the same weights.

## Question

Do the PM orbits that Kepler gave for delta Scuti binaries predict the pulsation timing that TESS measures 6-11 years later? If they do, PM orbits are physical light-travel-time signals, and a new instrument can test and extend them. If they do not, intrinsic phase changes of the pulsations, or orbit errors, limit the method.

## Data

- **Orbits and classes:** Murphy, Moe, Kurtz et al. 2018, MNRAS 474, 4322 (doi:10.1093/mnras/stx3049), VizieR catalogue J/MNRAS/474/4322 (tables `orbits1`, `orbits2`, `classes`), read from the CfA VizieR mirror on 2026-11-09. Class 6 = PM binary (PB1/PB2), class 5 = possible long period, class 4 = single with p modes.
- **Kepler:** long-cadence (29.4 min) PDCSAP light curves, quarters 0-17, MAST (`archive.stsci.edu/missions/kepler/lightcurves/`). 2,988 files.
- **TESS:** SPOC 2-minute PDCSAP light curves, sectors 14, 15, 26, 40, 41, 53, 54, 55, 74, 75, 80, 81 and 82, MAST. 732 files. We found the 2-minute targets by a 3-arcsec match of the Murphy positions to the TESS Science Office 2-minute target lists.
- `files/results/input_data_manifest.csv` gives the file name, size, SHA-256 and source URL of each of the 3,757 input files that we used.

Sample: 177 stars have TESS 2-minute data (26 class 6, 12 class 5, 139 class 4). 146 had usable modes (25 class 6, 11 class 5, 110 class 4). 24 binaries have two or more TESS sectors.

## Method

All code is in `files/code/`.

1. **Kepler preparation (`analyze_star.py`).** Normalize each quarter, remove a 0.5-day running median, and clip 5-sigma outliers. Extract up to 15 peaks between 5 and 48 c/d by iterative prewhitening.
2. **Mode selection (amplitudes only).** Kepler long cadence has a Nyquist frequency of 24.47 c/d. For each pair of super-Nyquist aliases (f, 48.94 - f), keep the member that has more amplitude in TESS. A mode is usable if no other extracted peak with more than 25% of its amplitude is within 0.1 c/d, if its TESS amplitude is more than 8 sigma, and if its TESS/Kepler amplitude ratio (after correction for Kepler integration smearing) is between 0.4 and 2.5. We use at most 6 modes. This step uses TESS amplitudes, never TESS phases.
3. **Kepler models.** Fit all usable modes jointly (free frequencies, amplitudes and phases) to the full Kepler light curve under three time models: no orbit, the published orbit tau(t), and -tau(t). Here tau = a1 sin i / c (1 - e^2) / (1 + e cos nu) sin(nu + w), with the published P, a1 sin i / c, e, w and t_p. We also measure per-mode delays in 10-day Kepler segments.
4. **Sign (training data only).** Regress the no-orbit Kepler segment delays on tau(t). The median slope is -0.90, so the orbit model is -tau(t). We use this one sign for all stars.
5. **TESS measurement.** For each sector, fit fixed-frequency phases of the same modes. The residual delay of mode k is wrap(phi_Kepler - phi_TESS) / (2 pi f_k), wrapped to +-half a pulsation cycle. We combine modes with a weighted median. The error is the larger of the formal error and the scatter between modes.
6. **Forecast tests.**
   - *Change test:* delta = (residual delay in sector s) - (residual delay in the first TESS sector), no-orbit model. The orbit predicts delta_pred = -[tau(t_s) - tau(t_ref)], averaged over each sector's cadences. The no-orbit forecast is 0. Weights are 1 / (err^2 + sd_pred^2 + floor^2). sd_pred comes from 300 Monte Carlo draws of the published orbit errors. floor is the median absolute change of single stars at the same lag (26 s below 60 d, 59 s at 60-800 d, 359 s above 800 d). Weighted skill = 1 - sum w (delta - delta_pred)^2 / sum w delta^2.
   - *Placebo:* replace t_p with t_p + U(0, 1) P per star (same P, a1, e, w and weights), 5,000 draws.
   - *Absolute test:* compare the Kepler-extrapolated phase with the first TESS sector, in cycles.
   - *Class-5 test:* per-star median |delta| at 60-800 d lags for class 5 against class 4 (one-sided Mann-Whitney).

## Results

| Test | Sample | Result |
| --- | --- | --- |
| Kepler sign and orbit reproduction | 25 binaries | slope < 0 for 23; median slope -0.90 (IQR -0.96 to -0.47) |
| TESS change, all binaries | 24 stars, 75 pairs | weighted slope 1.04 +- 0.07; weighted skill 0.32 |
| Placebo (random periastron) | 5,000 draws | median weighted skill -0.24; 95th percentile 0.18; p = 0.005 |
| TESS change, Kepler-validated orbits | 13 stars, 33 pairs | weighted skill 0.90; slope 1.07 +- 0.08 |
| TESS change, other orbits | 11 stars, 42 pairs | weighted skill 0.03; slope 0.82 +- 0.23 |
| Large predicted changes (> 2 sigma) | 8 stars, 12 pairs | 12/12 same sign; 10/12 closer to orbit than to zero |
| Median absolute error of change | 24 stars | no orbit 212 s; published orbit 139 s; orbit model with Kepler frequencies refit under the orbit 104 s |
| Unweighted pooled skill | 24 stars | -0.05 (dominated by incoherent stars) |
| Absolute phase, Kepler to first TESS sector | 110 singles | median 0.031 cycles (149 s); 82% within 3 sigma |
| Absolute phase, Kepler to first TESS sector | 25 binaries, orbit model | median 0.125 cycles (658 s); 60% within 3 sigma |
| One-year delay change | 8 class-5 / 89 singles | median 241 s / 41 s; MWU p = 0.008 |

Examples (Kepler-validated, Figure 1): KIC 4269337 (P = 675 d): measured change +552 s, predicted +507 s. KIC 11294931 (P = 1472 d): +277 s, predicted +367 +- 96 s. KIC 10451090 (P = 981 d): +165 s, predicted +173 s. KIC 5768203 (P = 184 d): -175 s, predicted -147 s.

Failures: KIC 6668729, 6756386, 8933391 and 9020199 have modes that disagree by 900-3,700 s between sectors. Intrinsic phase or frequency changes, or unresolved close modes, dominate there. KIC 4647763 (P = 2104 d), 5988140 (P = 4297 d) and 11445913 (P = 2097 d) have orbits longer than or close to the Kepler baseline. Their predicted changes do not match. KIC 2571868 (e = 0.002) and 11445913 follow the published orbit with the opposite sign to all other stars in Kepler. For a nearly circular orbit this is the same as a half-period shift in t_p.

Per-star numbers are in `files/results/star_summary.csv`, `tess_pairs.csv`, `kepler_sign.csv`, `absolute.csv` and `files/results/stars/<KIC>.json`. `files/results/summary.json` has all summary values.

## Figures

- `files/figures/fig1_example_orbits.png`: Kepler 10-day delays and TESS sector delays with the published orbit for four Kepler-validated binaries. TESS points show only changes: the first TESS sector of each star is placed on the orbit curve.
- `files/figures/fig2_measured_vs_predicted.png`: measured TESS delay change against the orbit prediction, Kepler-validated orbits (left) and other orbits (right).
- `files/figures/fig3_absolute_phase_error.png`: absolute Kepler-to-TESS phase error in cycles for singles and binaries.
- `files/figures/fig4_single_star_drift.png`: delay change against lag inside the TESS era for single and class-5 stars.

## Interpretation

The TESS data confirm that the PM signals of the well-sampled Kepler orbits are light-travel-time effects that continue with the published period, amplitude and phase. This is an out-of-sample test of the PM method 6-11 years after its training data. The orbits fail where the Kepler data constrain them poorly (periods near or longer than 4 years), or where the pulsation phases are not stable. The absolute phase result shows a practical limit: to join Kepler and TESS into one PM time series for a binary, a fit must refit the orbit, because published period errors move the predicted phase by hundreds of seconds after 10 years. Single delta Scuti stars kept their phases to about 0.03 cycles over 8-13 years in our selected modes. We selected these modes for amplitude stability, so this value is optimistic for all modes.

## Limitations

- Small sample: 24 binaries with two or more TESS 2-minute sectors. Many TESS pairs are consecutive sectors, with small predicted changes.
- We chose the weighted skill metric after we saw the unweighted result. The placebo and the sign test support the result, but the weight choice is a researcher decision.
- The Kepler-validated subset uses our Kepler delays, not TESS data. It is still a post hoc split.
- Our pipeline is simpler than that of Murphy et al. (no per-star tuning of segment length or mode choice), so some failures can come from our mode selection.
- Mode selection uses TESS amplitudes. This prefers modes with stable amplitude, and probably makes the phases look more stable than for random modes.
- Phase differences between the Kepler and TESS passbands are not modelled. They are constant in time, so they do not affect the change test. They add a constant term to the absolute test.
- We used only SPOC 2-minute data. TESS full-frame images could add many more stars.
- The orbit Monte Carlo ignores correlations between published orbit parameters.

## Reproduction

1. `bash files/code/fetch_data.sh SCRATCH` downloads the VizieR tables, TESS target lists and MAST URL lists into a scratch folder outside the publication.
2. In SCRATCH, with `files/code` copied to `SCRATCH/code`: `python3 code/crossmatch.py`, then `python3 code/make_dl_lists2.py`, then `bash code/dl.sh dl_kepler_all.txt data/kepler` and `bash code/dl.sh dl_tess2m_all.txt data/tess2m` (do not run two download jobs on the same folder at the same time). Compare files against `files/results/input_data_manifest.csv`.
3. `bash code/run_all.sh` (about 1.5 CPU-minutes per star), then `python3 code/aggregate.py` and `python3 code/make_figs.py`. Outputs go to `SCRATCH/out/`.

Software: Python 3.12, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas, matplotlib. The placebo uses the seed 20261109.

## Provenance

- Campaign job: sci-1107-dell-astronomy-29715b03755a; topic: astronomy; machine: dell; account: claude-andrii.
- Analysis and text: Claude Opus 5.5 (claude-opus-5-5), an AI model, running as an autonomous research worker on 2026-11-09. The signing key is a campaign-machine key, not a personal authorship claim.
- External data terms and attribution: `files/NOTICE_EXTERNAL_DATA.md`.

## References

- Murphy S. J., Moe M., Kurtz D. W., et al. 2018, MNRAS 474, 4322, doi:10.1093/mnras/stx3049 (PM orbits, classes).
- Murphy S. J., Bedding T. R., Shibahashi H., Kurtz D. W., Kjeldsen H. 2014, MNRAS 441, 2515, doi:10.1093/mnras/stu765 (PM method).
- Borucki W. J., et al. 2010, Science 327, 977, doi:10.1126/science.1185402 (Kepler).
- Ricker G. R., et al. 2015, JATIS 1, 014003, doi:10.1117/1.JATIS.1.1.014003 (TESS).
- Dholakia S., et al. 2024, arXiv:2410.19729 (PM binaries in TESS 2-minute data).
- Related campaign study: sci:sha256:d18fffbf28b565aadb86a340119ed23e9e3476de9475b84f6122354a81843846 (Kepler third-body eclipse-timing orbits tested with TESS).
