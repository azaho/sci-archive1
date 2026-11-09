# Astrometry of 3I/ATLAS before perihelion predicts its 2026 path with an r^-2 force, not a water-ice law; after perihelion small-telescope positions are 900 km tailward; A1 varies 2x

**Campaign:** 11_07_2026. **Job:** sci-1107-dell-astronomy-d937e153634d. **Topic:** astronomy. **Machine:** dell. **Account:** claude-andrii. **Model:** Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We fit the orbit of the interstellar comet 3I/ATLAS (C/2025 N1) to all 8,442 optical positions in the Minor Planet Center (MPC) archive (2025-05-08 to 2026-04-14, 343 stations). We used our own orbit fitter (ASSIST 1.2.3 / REBOUND 4.6.0 with JPL DE440 and 16 massive asteroids) with the Marsden radial (A1), transverse (A2) and normal (A3) non-gravitational acceleration terms. We did three tests.

1. **Forecast test.** We fit only the positions before 2025-10-01 (r of 1.74 au or more, before perihelion on 2025-10-29) and predicted the 4,157 positions after 2025-11-01.
   - Gravity only misses the later positions by up to 12.4 arcsec in RA (monthly median, Feb 2026).
   - A radial term with g(r) = (1 au/r)^2 is already detected before perihelion: A1 = 5.7 +- 1.8 x 10^-8 au/d^2 (delta chi2 = 9 with formal weights). This model reduces the late error to 0.7-1.6 arcsec (Feb-Apr 2026). But it misses by 4-6 arcsec in Nov 2025 - Jan 2026, which is more than its 1-sigma forecast width (3.7 arcsec RA, 0.6 arcsec Dec).
   - The standard water-ice law g(r) misses by 47-62 arcsec. The pre-perihelion acceleration at 2-4.5 au is too large for water-ice sublimation scaling.
2. **Telescope-class offsets.** We compared small telescopes and ATLAS with large telescopes (1.5 m or larger, and HST) in the same 3-day bins. This comparison does not depend on the orbit model.
   - Before perihelion, the apparent motion of 3I was within about 5 degrees of the direction to the Sun. After perihelion, it was within about 5 degrees of the opposite direction. Thus, a timing (along-track) offset and a sunward/tailward photocentre offset are almost the same signal.
   - After perihelion, a 3-D tailward photocentre offset of 907 +- 122 km, projected with the phase angle, fits the small-telescope offsets much better than a timing offset (weighted RSS 2,652 against 2,798). The offset is 0.3-0.55 arcsec in late Nov-Dec 2025 (phase angle 22-31 degrees). It is near zero in January 2026 (phase angle 1-7 degrees), when the apparent rate stayed high.
   - Before perihelion, small telescopes lead the large telescopes by 3.1 +- 0.7 s along the motion (about 0.08 arcsec). We cannot separate this from a sunward offset.
   - There is also a cross-track offset of -0.06 to -0.11 arcsec.
3. **Parameter sensitivity.** For one r^-2 law over the full arc, the fitted A1 is 2.9 to 6.2 x 10^-8 au/d^2. The value depends on the data selection, the weights and the offset model. The formal errors are only 0.07-0.6 x 10^-8 au/d^2. When we fit only the large telescopes, we get A1 = 5.5 +- 0.6, A2 = 2.1 +- 0.5 and A3 = -0.67 +- 0.04 (x 10^-8 au/d^2). These values agree with the full-arc solution of Spada et al. (2026). If all large-telescope positions have a common sunward photocentre offset of K (in 1000 km), A1 changes by -0.87 K. The astrometry alone does not fix K.

**Main limitations:** We do not know the photocentre offset of the large telescopes. Our telescope classes are defined by station name, not by aperture or reduction method. Our weights are simple and our formal chi2/dof is 0.15-0.6. We do not model a time-delayed (DT) or asymmetric g(r), and we have no observations after 2026-04-14.

## 1. Question and prior work

3I/ATLAS is the third known interstellar object. Its orbit needs a non-gravitational acceleration (NGA). Published size estimates use the NGA, the gas production rate and an assumed density. Examples are Forbes & Butler (arXiv:2512.18341), Thoss et al. (arXiv:2603.15735) and the HST nucleus analysis (arXiv:2601.21569). Thus, the NGA magnitude sets the size estimate (R is proportional to A^-1/3).

Spada, Krolikowska & Dones (arXiv:2603.00782) fit the MPC astrometry with symmetric, delayed and asymmetric models. They found that separate pre- and post-perihelion fits give incompatible parameters, and that the systematic errors are larger than the formal errors. They reduced the effect of tailward photocentre bias with weight tiers (they multiplied the uncertainties of 7,489 lower-quality positions by 15), but they did not model the bias. JPL solution #55 (2026-10-21) uses only 117 positions from 2025-10-03 to 2026-10-16, with DT = 28.5 d.

Our questions were:

- Do the positions before perihelion alone predict the later path, and which g(r) law extrapolates correctly?
- Do small-telescope positions differ systematically from large-telescope positions? If so, in which direction, and how does this difference change the NGA parameters?

## 2. Data

- **MPC astrometry.** We used `get-obs` (ADES), retrieved 2026-11-09. There are 8,442 optical positions with no deprecated rows. The dates are 2025-05-08 (TESS precovery) to 2026-04-14. The data include 40 positions from spacecraft other than HST (TESS, NEOSSat, Lucy, Psyche and others) and 11 roving-observer positions (WGS84). The bundle contains a gzip copy and its SHA-256.
- **MPC observatory codes** (`obscodes` API).
- **JPL SBDB orbit #55** and **Horizons barycentric vectors** of #55 (2025-05-01 to 2026-04-20, 6 h step). We used the vectors to compute the residuals of #55. We used the #55 state at 2025-09-01 only as the starting guess.
- **Shared campaign datasets.** These are not duplicated in the bundle. The paths and SHA-256 values are in `files/data/input_manifest.json`:
  - `jpl-de440-linux-p1550p2650-20261109` (DE440)
  - `jpl-sb441-n16-bsp-20261109` (16 perturbing asteroids)
  - `jpl-debias-2018-eggl2020-20261109` (star-catalogue debiasing, Eggl et al. 2020)

## 3. Method

**Orbit model.** We adapted the fitter of campaign publication sci:sha256:e8572651 (dark comets) to this comet. The software is ASSIST/REBOUND with DE440 and sb441-n16, GR, the J2/J4 terms of the Earth and the J2 term of the Sun, and light-time correction. The NGA is A_i g(r) in the radial, transverse and normal directions. We used two g(r) laws:

- `r2`: g = (1 au/r)^2, the same law as JPL #55 and Spada et al.
- `h2o`: the Marsden et al. (1973) water-ice law (alpha = 0.1113, r0 = 2.808 au, m = 2.15, n = 5.093, k = 4.6142).

The **split** model has separate A1-A3 values before and after perihelion. It is a simple form of asymmetric activity.

**Weights.** The uncertainty of each position is sqrt(reported rms^2 + 0.3^2) arcsec. We used 1 arcsec when no rms is reported. We multiplied the uncertainty by sqrt(N/4) when one station has more than 4 positions in one night. We applied the Eggl et al. (2020) debiasing and rejected outliers at chi2 > 8 (Carpino et al. style). As a sensitivity test, we repeated key fits with a floor of 0.15 arcsec (all data) or 0.1 arcsec (large telescopes). The formal chi2/dof is below 1 (0.15-0.6), so our quoted formal errors are conservative within the model. They do not include systematics.

**Telescope classes.** We used these classes:

- **L:** large professional telescopes, about 1.5 m or larger, plus HST and ZTF. The station codes are 309, W84, 250, G37, 290, F51, F52, X05, I33, V00, 807, J13, F65, E10, T15, G96, 705, W74, 697 and I41. There are 590 positions (208 before and 382 after perihelion).
- **A:** ATLAS units (0.5 m, 1.86 arcsec pixels).
- **S:** all other ground stations (7,171 positions).
- **X:** other spacecraft.

**Offset models.** We used three forms of the photocentre or measurement offset of a class:

- a 3-D offset of K km along the Sun-comet line. Its sky projection is K sin(phase)/Delta.
- a timing offset tau (s) along the apparent motion, plus a cross-track offset c (arcsec).
- a sky-plane offset along the projected Sun direction.

We fit the offsets together with the orbit (`run2.py`). We also fit them with an orbit-independent regression. In that regression, we subtract the median residual vector of the L class in the same 3-day bin and use cluster-robust (station-night) errors (`joint_offset.py`).

**Forecast test.** We fit the positions before 2025-10-01 TDB and evaluated the positions after 2025-11-01. There are only 26 positions in October 2025, and these are near solar conjunction. We report the monthly medians of the residuals and the linear forecast width from the orbit covariance.

## 4. Results

### 4.1 Forecast of the post-perihelion path from data before 2025-10-01 (Figure 1)

Monthly median O-C (RA cos Dec / Dec, arcsec) of all post-perihelion positions for the orbits fit before 2025-10-01. The parameters are in units of 10^-8 au/d^2.

| Model fit to data before 2025-10-01 | A1 | Nov 2025 | Dec | Jan 2026 | Feb | Mar | Apr |
| --- | --- | --- | --- | --- | --- | --- | --- |
| gravity only | 0 | -0.7/+1.6 | +2.6/+1.2 | +10.9/+0.5 | +12.4/+1.1 | +11.8/+1.5 | +10.9/+1.0 |
| r2, A1 only | 5.7 +- 1.8 | -4.5/+2.7 | -6.2/+3.8 | -4.0/+2.9 | -1.6/+2.1 | -0.8/+1.8 | -0.7/+1.2 |
| r2, A1 only, A/S Sun-line offsets | 6.4 +- 1.8 | -5.1/+2.9 | -7.3/+4.1 | -5.4/+3.2 | -2.9/+2.1 | -2.0/+1.9 | -1.8/+1.2 |
| r2, A1 only, A/S timing offsets | 7.2 | -5.2/+2.9 | -8.4/+4.3 | -7.5/+3.4 | -5.0/+2.2 | -4.0/+1.9 | -3.6/+1.2 |
| r2, A1, A2, A3 | 8.4 +- 4.6 | -3.9/+0.9 | -8.6/+1.6 | -14.0/+1.5 | -13.5/+0.3 | -12.1/-0.1 | -10.9/-0.7 |
| water-ice g(r), A1 only | 41.6 +- 14.5 | -14.0/+5.1 | -37.3/+12.3 | -62.1/+12.3 | -57.9/+5.3 | -51.9/+3.2 | -47.2/+1.8 |

- **Detection before perihelion.** The 4,089 pre-perihelion positions prefer the r2 A1 model to gravity only by delta chi2 = 9.0 (formal weights). After we rescale the weights to chi2/dof = 1, delta chi2 is about 28. With the alternative offsets and weights, A1 is 6.4 to 7.4. The positions of the large telescopes alone before perihelion (382 positions) cannot constrain the NGA (A1 = 8.8 +- 16.9).
- **Extrapolation.** The r2 law extrapolates much better than gravity only, and much better than the water-ice law. The water-ice law gives a negligible force at 3-4.5 au. Thus, to fit the pre-perihelion displacement, it needs an A1 that predicts too much acceleration near perihelion (median miss 49 arcsec).
- **Forecast width.** The r2 A1 forecast is not statistically exact. In Dec 2025, the Dec residual (+3.8 arcsec) is 6 times the forecast width (0.6 arcsec). The free-A2/A3 model, with more parameters, extrapolates worse (-14 arcsec in Jan 2026).
- **Interpretation.** One constant r^-2 law fits the activity before perihelion approximately but not exactly. This agrees with the incompatibility of separate fits before and after perihelion found by Spada et al. (2026).

The reverse test (fit after 2025-11-01, predict before 2025-10-01) gives similar results:

| Model fit after 2025-11-01 | Backcast error (RA, Jun-Aug 2025) |
| --- | --- |
| gravity only | -8.6 to -11.3 arcsec |
| r2 A1 | about -3 arcsec |
| water-ice A1 | about +1 arcsec |
| water-ice A1-A3 | +24 to +33 arcsec |

The tables are `files/tables/forecast_test.csv` and `files/tables/all_fits.csv`.

### 4.2 Small telescopes compared with large telescopes (Figure 2)

**Per-station test.** We used three different reference orbits. Each orbit fit gives the same pattern. For 83 small-telescope stations (S class) before perihelion, the median along-Sun offset is +235 to +273 km (sky plane), and 69-73% of the stations have a positive offset. For 84 stations after perihelion, the median offset is -189 to -350 km, and 74-77% of the stations have a negative offset. The 36 stations with data before and after perihelion moved tailward in 86% of cases (Wilcoxon p = 2e-5 to 7e-5). See `station_offset_tests.csv`.

**Orbit-independent bin test.** In this test, S minus L is +0.069 +- 0.049 arcsec toward the Sun before perihelion (14 bins) and -0.193 +- 0.063 arcsec after perihelion (16 bins).

**Apparent motion.** The sign change is not alone evidence for a coma that changes direction. The apparent motion of 3I was 5 degrees (median) from the Sun direction before perihelion and -175 degrees after perihelion. In the frame of the apparent motion, the small telescopes are ahead of the large telescopes in both periods (+0.055 and +0.20 arcsec) and offset across the motion in both periods (-0.06 and -0.11 arcsec).

**Joint regression.** For the S class, we compared the models with cluster-robust errors (`joint_offset_regression_c_L_split.csv`):

| Period | timing + cross (wRSS) | sky-plane Sun-line + cross | 3-D Sun-line x sin(phase) + cross | all three |
| --- | --- | --- | --- | --- |
| before perihelion (2,285 positions) | tau = +3.1 +- 0.7 s (2,600) | K = +179 +- 41 km (2,595) | K3d = +457 +- 208 km (2,625) | not separable |
| after perihelion (1,921 positions) | tau = +3.9 +- 0.6 s (2,798) | K = -234 +- 39 km (2,805) | **K3d = -907 +- 122 km (2,652)** | tau = -0.9 +- 0.7 s, K3d = -1,033 +- 164 km (2,648) |
| full arc (4,206 positions) | tau = +3.7 +- 0.5 s (5,407) | K = -107 +- 29 km (5,557) | K3d = -718 +- 108 km (5,379) | tau = +2.4 +- 0.5 s, K3d = -519 +- 107 km (5,313) |

After perihelion, the data clearly prefer a tailward 3-D photocentre offset of about 0.9-1.0 x 10^3 km. The timing term then becomes zero. The offset follows the phase angle and not the apparent rate. In January 2026, the phase angle was 1-7 degrees and the rate was 2.0-2.7 arcsec/min, and the offset is near zero. In December 2025, the phase angle was 22-31 degrees and the rate was 2.2-3.1 arcsec/min, and the offset is 0.25-0.55 arcsec.

Before perihelion, the phase angle was small and the motion was parallel to the Sun line. Thus, a 3.1 s timing lead and a sunward offset of about 180 km (sky plane) cannot be separated.

The cross-track offset of -0.06 to -0.11 arcsec has no explanation in our models. Possible causes are differential colour refraction in unfiltered small-telescope images, or asymmetric coma and dust structure.

The ATLAS (A) class has only 3-8 usable bins. Its offsets are not significant before perihelion. After perihelion, the cross-track offset is +0.30 arcsec (sky-plane test).

### 4.3 Effect on the non-gravitational parameters (Figures 3 and 4)

All values are in units of 10^-8 au/d^2 and use g = (1 au/r)^2. The errors are formal (not rescaled).

| Fit | A1 | A2 | A3 |
| --- | --- | --- | --- |
| all data, no offset | 2.85 +- 0.14 | 3.75 +- 0.12 | -0.73 +- 0.01 |
| all data, A/S 3-D Sun-line offsets (fitted -1.3 and -1.4 x 10^3 km) | 4.21 +- 0.07 | 3.45 +- 0.10 | -0.71 +- 0.01 |
| all data, A/S timing + cross offsets | 2.90 | 3.56 | -0.67 |
| all data, one global Sun-line offset (degenerate) | 6.21 +- 0.27 | 3.69 +- 0.12 | -0.69 +- 0.01 |
| large telescopes only | 5.49 +- 0.61 | 2.08 +- 0.47 | -0.67 +- 0.04 |
| large telescopes only, floor 0.1 arcsec | 5.89 +- 0.31 | 1.92 | -0.68 |
| Spada et al. 2026, ng1 (full arc) | 4.94 +- 0.07 | 1.80 +- 0.09 | -0.76 +- 0.01 |
| JPL #55 (after 2025-10-03, DT = 28.5 d) | 4.62 +- 0.48 | -0.96 +- 0.20 | -0.83 +- 0.17 |

**Split model.** Fit only to the large telescopes, the split model gives a post-perihelion A1 = 6.4 +- 1.1, A2 = -1.3 +- 2.0, A3 = -1.12 +- 0.17. The pre-perihelion A1 = 0.3 +- 4.1 is not determined. With all data and timing offsets, the split model gives a post-perihelion A1 = 2.8, A2 = -0.63, A3 = -0.73, and a pre-perihelion A2 = +5.6.

**Consistent values.** A3 is consistent (-0.5 to -1.1) in all fits.

**Inconsistent values.** A1 and A2 depend on the data selection. This dependence is larger than the formal errors by a factor of 5-30. The large-telescope fit gives the highest A1. The fits of all data that do not model the class offsets give the lowest A1.

**Absolute offset.** We shifted all large-telescope positions by an assumed common 3-D Sun-line offset K (`run3.py`). Then A1 changes linearly:

- -0.87 x 10^-8 au/d^2 per 1000 km for the r2 A1-A3 model
- -0.77 for the post-perihelion part of the split model
- -2.2 for the water-ice law

The formal chi2 changes by at most 6 over K = -5 to +1 x 10^3 km (about 40 after rescaling the weights to chi2/dof = 1). The minimum is near K = -3 x 10^3 km, but the curve is irregular because the outlier set changes. For the split model, the chi2 changes by less than 1 over K = -2 to +2 x 10^3 km. Thus, the astrometry constrains the common offset only weakly (Figure 3, right). If the large telescopes have a tailward bias of a fraction of the 0.9 x 10^3 km bias that we measure for the small telescopes, the large-telescope A1 increases by up to about 0.8 x 10^-8 au/d^2 (15%).

**Size estimate.** The size scales as A^-1/3. The total A1 range of 2.9-6.4 x 10^-8 au/d^2 thus gives a radius range of a factor of 1.3 for the same outgassing assumptions.

### 4.4 Residuals of JPL #55 before its data arc (Figure 5)

JPL orbit #55 does not use positions before 2025-10-03. Its large-telescope residuals in May-Aug 2025 are -1.3 to -1.7 arcsec in RA (monthly medians). After October 2025, they are near zero (|median| 0.08 arcsec or less), except March 2026 (-0.5 arcsec, few positions). JPL describes this solution as temporary, so this is not a failure of the JPL work. It shows that a DT = 28 d r^-2 model fit only after perihelion does not reproduce the early arc to better than about 1.5 arcsec.

## 5. Interpretation

- **Real non-gravitational acceleration.** The comet had an NGA before perihelion. A1 at r = 2-4.5 au was already of the same size as the full-arc value when we scale it by r^-2. This agrees with activity driven by a volatile more volatile than water. JWST measured a CO2-dominated coma at 3.32 au before perihelion (Cordiner et al. 2025, arXiv:2508.18209). Pure water-ice scaling cannot connect the pre-perihelion and post-perihelion orbits.
- **Small-telescope photocentre bias.** After perihelion, the small-telescope astrometry has a tailward photocentre bias of about 900 km along the Sun line. This bias grows with the phase angle. It is the expected sign for a comet with a dust tail measured with larger seeing disks and apertures.
- **Effect on the NGA.** Models that do not include such offsets, or that include them in a different form (timing compared with Sun-line), give A1 values that differ by a factor of 2. The formal errors do not show this difference. NGA-based size estimates of 3I must use an A1 uncertainty of about +-35%, not the formal +-2%.

## 6. Limitations

- **Unknown absolute offset.** We do not know the absolute photocentre offset of the large telescopes. All of our A values are conditional on a zero offset for the L class.
- **Telescope classes.** We assign the classes by station name. Some L stations (ZTF, 1.2 m Schmidt) and some S stations (LCO 1 m) are borderline. The aperture, exposure time and reduction method (centroid, PSF fit, zero-aperture extrapolation) are mostly unknown. The ADES `exp` field is not consistent between stations.
- **Weights.** Our weights are simple, and the formal chi2/dof is 0.15-0.6. We did not inflate tiers as Spada et al. did. The quoted errors are formal.
- **g(r) models.** We did not model a time-delayed g(r) (DT) or a smooth asymmetric g(r). The split model is a step approximation of asymmetric activity.
- **Data gaps.** There are only 26 positions in October 2025 (solar conjunction). There are no MPC positions after 2026-04-14 in our download, although JPL #55 lists data to 2026-10-16. The spacecraft positions (Mars orbiters and others) that are not in the MPC download are not used.
- **Linear forecast width.** The forecast width is the linear propagation of the formal covariance, so it is too narrow.
- **No size estimate.** We do not compute a nucleus size or a mass. We only quantify how the A1 uncertainty propagates.

## 7. Reproduction

1. Put `files/data/*.gz` (gunzipped) in `raw/` with the names in `files/data/input_manifest.json`.
2. Link `../datasets` to the shared campaign datasets (DE440, sb441-n16, debias_2018).
3. Install `rebound==4.6.0 assist==1.2.3 healpy==1.20.1` with `pip install --target pylib --no-deps`.
4. Run `files/code/run_all.sh`.

The full run takes about 1-2 h on one core per job. Each full-arc fit takes 30-340 s.

These files contain the results:

- `files/results/fit_results.tar.gz`: every fit as JSON, with parameters, covariance, active mask and residuals.
- `resid_*`, `track_*`: per-position residual geometry.
- `files/tables/`: all summary tables.

**Software:** Python 3.12, numpy, pandas, scipy, astropy, matplotlib, healpy 1.20.1, REBOUND 4.6.0, ASSIST 1.2.3.

## Files

- `files/code/ofit.py`: orbit fitter (propagation, debiasing, weights, class offsets, outlier rejection).
- `files/code/run_fits.py`, `run2.py`, `run3.py`: model fits, telescope-class fits and offset profile.
- `files/code/stations.py`, `track.py`, `local_diff.py`, `joint_offset.py`, `tail_angle.py`: residual geometry and offset tests.
- `files/code/summarize.py`: tables and figures.
- `files/figures/fig1..fig5`: figures.
- `files/tables/*.csv`: results tables.
- `files/data/`: raw inputs and the input manifest with SHA-256 values.
