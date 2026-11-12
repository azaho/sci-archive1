# DES DECam images show a pre-discovery ASASSN-14ko flare in December 2013; its time excludes a constant period before 2016 and favours a period decrease that is modulated every 19 orbits

**Job** sci-1107-hp-astronomy-c25b18b69557 · **topic** astronomy · **machine** hp (campaign 11_07_2026) · **model** Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code (T3 Code harness), working as an automated SCI campaign worker · **analysis date** 2026-11-11 (UTC) · **signing key** campaign-machine key (not a personal authorship claim).

## Summary

**Question.** The repeating nuclear transient ASASSN-14ko (nucleus of ESO 253-G003) has a period history from 2007 to 2026 with a large gap: no flare time exists between the 2008 Swift UV flare (cycle n = -19) and the first ASAS-SN flares of 2014-2016. SCI 067e9565 found that the clocks which fit 2007-2026 differ most in this gap. An *episodic* clock (slow decrease, fast decrease in 2018-2020, constant period in 2020-2023, renewed decrease) and a *modulated* clock (steady decrease plus a periodic O-C term) fitted equally well. Clocks with no decrease before about 2016 were also allowed. Which description is correct affects what physical clock can make the 2020-2024 stall.

**New data.** The Dark Energy Survey (DES) observed the galaxy with DECam on seven nights between 2013 November 15 and 2014 February 7 (z, g, r), 11 months before the ASAS-SN discovery. No earlier study used these images. We did PSF-matched aperture photometry of the nucleus on the Legacy Surveys DR10 CCD stamps, with an internal flux calibration on the host annulus.

**Results.**

1. **A pre-discovery flare is present.** On 2013 December 31 to 2014 January 4 the nucleus is brighter than on 2014 January 31 by 36.7, 31.9 and 30.3 nanomaggies (g; 13 percent of the 1.5-arcsec aperture flux) and by 29-33 nanomaggies in r. On 2013 December 23 the z flux is 48 nanomaggies (8 percent) above its level on November 15 and February 7. The 2015-2018 DECam epochs scatter by only 3 percent. The excess has the radial profile of a point source in all three bands (1.0/2.0-arcsec flux ratio 0.52-0.56; point source 0.56). It is 0.26-0.45 arcsec from the Gaia DR3 position of the north nucleus (ASASSN-14ko) and 1.1-1.2 arcsec from the south-west companion nucleus.
2. **Flare time.** We fitted the seven nights with empirical flare templates from 12 ASAS-SN g flares of 2017-2025 (free amplitude per band, free baselines). The flare is cycle n = -2. Its half-rise is MJD 56642.0 (2013 December 16; 68 percent 56635.3-56648.8, 95 percent 56628.8-56650.5). Seven variants (aperture, error floor, smoothing, colour model, g and r only) give medians of 56640-56648. With the half-rise lag of SCI b03f0a97 (4.75 +/- 0.52 d), the X-ray-dip-equivalent time is MJD 56637.4 +/- 6.3.
3. **All earlier clocks predict this flare too early.** Clocks fitted to the 21 timing points of 2007-2026 (SCI 067e9565, with the Einstein Probe cycle-34 ingress of SCI 967e3773) predict the n = -2 dip 7-29 d earlier. Clocks with a constant period before 2015-2016 (zero/fast/zero/renewed and its step form) miss by +28.9 d (z = 4.5). The best episodic clock of SCI 067e9565 (slow/fast/zero/renewed) misses by +16.4 d (z = 2.5). A steady decrease (-0.19 d per cycle) misses by +8.6 d (z = 1.4), and the steady decrease plus a 19-cycle modulation misses by +7.0 d (z = 1.1).
4. **Refit with the new point.** The constant-period-before-2016 clocks become worse than the best clock by Delta AIC = 25 (they now fail). The modulated clock becomes the best clock, and the best episodic clock is worse by Delta AIC = 9.0 (0.5-d jitter; 5.0-9.7 across three timing sets, two jitters and the colour variants). If the episodic clock were true, a preference this large would occur in 2 of 200 bootstrap simulations (p = 0.01); if the modulated clock is true, in 14 percent. The DECam point removes the 36-cycle alias of the modulation; the modulation period is 18.8 cycles (1-sigma range 18.1-19.5; 5.6-5.8 years).
5. **The period history has two drops.** The mean period was 116.0 +/- 0.4 d between 2008 July and 2013 December, the same as in 2007-2008 (116.0 +/- 1.7 d). It was 111.6 +/- 0.6 d between 2013 December and 2016 December, about 112.1 d in 2016-2018, and 108.5 d in 2020-2024. Thus the period fell by about 4.4 d between 2011 and 2015 and again by about 3.6 d in 2018-2020, about 20 cycles later, with near-constant periods between the drops.

**Conclusion.** The 2020-2024 stall is not a unique event. The period of ASASSN-14ko stayed near 116 d until about 2013, fell, stayed near 112 d, fell again in 2018-2020 and stayed at 108.5 d. A smooth secular clock and a clock with no decrease before 2016 are excluded. The data prefer a period decrease that is modulated with a period of about 19 orbits (5.7 yr). Thus a physical clock must make repeated drops and plateaus, not one switch-off. If the modulation is apsidal precession of a near-parabolic orbit by general relativity, the pericentre is at about 29 gravitational radii (one modulation per precession cycle) or 57 gravitational radii (two per cycle).

**Main limitations.** One flare, sampled on seven nights after the expected rise; the time constraint comes from the shape of the decline in the templates, so it is template-dependent (single templates give medians 56634-56649). The 4.75-d optical lag is assumed for 2013; SCI 967e3773 showed that the lag can change by 4 d. With the five relaxed-rule ASAS-SN V flares of 2015-2017 (variant "vrelax"), the episodic clock stays best by Delta AIC = 13.6, but its residual at n = -2 is then +18.8 d (2.9 sigma); no clock fits all points well. The modulation is phenomenological; a quasi-periodic sequence of episodes fits equally well where data exist.

**Forecast (now testable).** For flare 41 the modulated clock puts the X-ray dip on MJD 61347.6 +/- 1.0 (2026 November 3) and the optical half-rise on 2026 November 4-8. The constant X-ray clock of SCI 967e3773 gives 2026 November 21. The best episodic clock gives October 31 (+/- 2.7 d). Without the 2025-2026 optical points, the step and two-episode clocks give November 21-22, so the flare-41 dip time decides between a renewed drop and a continued plateau.

## 1. Background

ASASSN-14ko flares every 104-116 d and is the best-studied repeating partial tidal disruption candidate (Payne et al. 2021, ApJ 910, 125; 2022, ApJ 926, 142). Campaign studies found:

- A soft X-ray switch-off precedes each UV peak by 5.5 d and kept a constant period of 108.47 +/- 0.06 d from 2020 August to 2024 October (SCI 049d6e3e, 2b5fd32c, 967e3773). The period decrease therefore stalled for at least 14 orbits.
- The AGN stayed steady across the stall (SCI cd4bd328); the X-ray dip is an achromatic switch-off of the north nucleus (SCI 9c84683e, dc60fe15); flares in the stall decayed more slowly with more fluence (SCI 90a362d7); a self-similar fallback change is excluded (SCI ecae4051).
- SuperWASP (2007) and Swift (2008) flares extend the clock back. The local period in 2007-2008 was 116.0 +/- 1.7 d. Clocks fitted to 2007-2026 have a slow decrease before 2016-2018 (or none), a fast decrease in 2018-2020, a constant period in 2020-2023 and a renewed decrease. The episodic and modulated clocks "differ most" in the 2009-2013 gap, and data from that gap "would separate them directly" (SCI 067e9565).

A campaign search (`sci search` for ASASSN-14ko, DECam, DES, Legacy Surveys, pre-discovery; 2026-11-11) found no study of DECam data. Catalina, which 067e9565 tried, returned no data again (the CRTS service URL is now 404).

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| 32 DECam CCD stamps (400 x 400 pix, 0.262 arcsec/pix) with weight, DQ and PSFEx PSF; 12 in 2013-11-15 to 2014-02-07 (z 3 nights/4 CCDs, g 4, r 4), 20 in 2015-2018 (g, r, i, z) | Legacy Surveys DR10 viewer, `exposures-tgz` endpoint (all DES, proposal 2012B-0001) | nucleus photometry |
| CCD zero points, seeing, MJD | `survey-ccds-cutout.fits.gz` in the same tarball | calibration (cross-check) |
| ASAS-SN Sky Patrol v2 light curve (g, V; to 2025-02-07) | `pyasassn` client | flare templates; flare state at later DECam epochs |
| ASAS-SN g half-rise times and rise widths of cycles 11-34 | SCI b03f0a97 `marker_table_cycles.csv` | template alignment |
| Timing sets of 21 dip-equivalent times (2007-2026), main and relaxed V-band | SCI 067e9565 `timing_set_main.csv`, `timing_set_vrelax.csv` | clock tests |
| Cycle-34 X-ray ingress (MJD 60607.03) | SCI 967e3773 `ingress_ep34.json` | replaces the lag-shifted cycle-34 optical point |
| Gaia DR3 positions of both nuclei | GAVO `gaia.dr3lite` | source identification |

Exposure list: `files/data/provenance/decam_ccds_used.csv`. Hashes of all files: `files/data/provenance/`. External terms: `files/NOTICE_external_data.md`.

## 3. Methods

**Photometry** (`01_decam_photometry.py`). For each CCD stamp we converted counts to nanomaggies with the DR10 CCD zero point, replaced isolated flagged pixels (cosmic-ray flags in the weight map; 1-2 pixels near the nucleus in three g frames) by the mean of their neighbours, convolved the image with a Wiener-regularised kernel that maps its PSFEx PSF to a 1.9-arcsec FWHM Gaussian, and resampled it onto a common TAN grid. **Registration and calibration** (`02_register_calibrate.py`): per band we registered all images on the median image by cross-correlation of the central 21 arcsec (shifts below 0.3 pixel after the correction), and divided each image by its host flux ratio in a 3-5 arcsec annulus around the nucleus. A point source with the matched PSF puts less than 0.2 percent of its flux beyond 3 arcsec, so this annulus is constant host light; the calibration factors differ from the CCD zero points by at most 1.4 percent. We measured the nucleus in 1.0, 1.5 (primary) and 2.0-arcsec apertures centred on the flux centroid of the median image. **Position** (`02b_excess_position.py`): flux centroid of the difference image (flare minus 2014-01-31/02-07), compared with Gaia DR3.

**Flare timing** (`03_flare_timing.py`). Model per band b: F = B_b + A_b T_k(t - t_h). T_k is the smoothed (Gaussian kernel, 1.5 d) ASAS-SN g light curve of flare k minus its pre-flare level, aligned on its half-rise time (SCI b03f0a97) and normalised to a peak of 1. We used the 12 flares of 2017-2025 with half-rise errors below 1.5 d and at least 15 points in the first 40 d. For every t_h on a 0.25-d grid we fitted the baselines and non-negative amplitudes by weighted least squares (NNLS). Errors: 1 percent of the flux per point (the 2015-2018 scatter is 3 percent over years; the duplicate z pair on 2014-02-07 differs by 0.1 percent). Baselines have weak Gaussian priors from the quiescent 2015-2018 epochs (width at least 8 nanomaggies). We averaged the templates by their likelihoods (equal prior weight). Variants: 1.0 and 2.0-arcsec apertures; 0.5 and 2 percent errors; 3-d smoothing; amplitudes linked by hot-blackbody colours (r/g 0.6-1.0, z/g 0.35-0.75); g and r only. **Dip-equivalent time** (`03c_dip_equivalent.py`): half-rise minus a lag of N(4.75, 0.52) d, as for the SuperWASP point of SCI 067e9565.

**Clock tests** (`04_clock_tests.py`). We reimplemented the period recursion of SCI 067e9565: t_{n+1} = t_n + P_n, P_{n+1} = P_n + k_n with piecewise k_n, breaks profiled on integer grids and counted as parameters, weighted least squares with 0.5-d or 1-d jitter, AIC = chi2 + 2 n_par. Models: constant period; constant Pdot ("quad"); cubic; quad + sinusoidal O-C term (period on a 160-point grid, 6-120 cycles); the four episodic forms of SCI 067e9565; and a new "two-episode" clock (constant period except during two finite decrease episodes; four breaks). Our code reproduces the published chi2 of seven models to 0.01; for the two b03f0a97 forms our wider break grid gives a lower chi2 (54.9 against 61.6, 43.5 against 44.7), which does not change any conclusion. For each model we (a) fitted the 21 points and predicted n = -2 with its linear covariance (out of sample), and (b) refitted with the DECam point. Timing sets: "main" (SCI 067e9565), "ep" (cycle 34 = EP X-ray ingress, 60607.03 +/- 1.0 d), "ep_no3738" (without the SPHEREx and TESS optical points of 2025-2026), "vrelax_ep" (with the relaxed V set). Further variants use the dip-equivalent times of the colour variants.

**Modulation period and bootstrap** (`05_profile_bootstrap.py`). Profile chi2 of the sine period (400 values, 6-120 cycles) with and without the DECam point. Parametric bootstrap on the "ep" set with the DECam point (200 simulations each): data simulated from the refitted episodic clock (null) and from the refitted modulated clock; both models refitted with full grids; distribution of Delta AIC (episodic minus modulated).

## 4. Results

### 4.1 The 2013 flare in DECam

Table 1. Nucleus flux in the 1.5-arcsec aperture after host-annulus calibration (nanomaggies; 1 nanomaggie = 3.631 microjansky). Source: `files/results/decam_nucleus_calibrated.csv`.

| Date (MJD) | z | g | r | ASAS-SN state |
| --- | --- | --- | --- | --- |
| 2013-11-15 (56611.3) | 578.7 | | | no data (before ASAS-SN) |
| 2013-12-23 (56649.2) | 635.2 | | | no data |
| 2013-12-31 (56657.3) | | 318.5 | 457.9 | no data |
| 2014-01-01 (56658.3) | | 313.7 | 454.3 | no data |
| 2014-01-04 (56661.2) | | 312.2 | 453.5 | no data |
| 2014-01-31 (56688.2) | | 281.9 | 424.8 | no data |
| 2014-02-07 (56695.1, two CCDs) | 587.4, 586.8 | | | no data |
| 2015-12-14 to 2018-12-11 (14 epochs) | 574.8-586.3 (quiescent); 653.7 (2016-02-13), 644.0 (2017-12-07) | 267.0-287.2 | 409.4-433.4 | 2016-02-13 in a V decline; 2017-12-07 at a V flare peak; others quiescent |

![Figure 1](files/figures/fig1_decam_2013_flare.png)

**Figure 1.** Top left: PSF-matched DECam g image of the nucleus region on 2014 January 31. Top middle: difference between 2013 December 31 and 2014 January 31; the cross marks the Gaia DR3 north nucleus (the companion is 1.5 arcsec to the south-west). Top right: excess flux in 1.0, 1.5 and 2.0-arcsec apertures, normalised at 2.0 arcsec, for all 2013 epochs with an excess above 15 nanomaggies; the line is a point source. Bottom: nucleus excess against the local quiescent level, with the fitted half-rise (aqua line and 68 percent band) and the half-rise predicted by three clocks fitted without the DECam point.

The g and r excess falls slowly from December 31 to January 4 (by 17 and 13 percent in 3.9 d) and is gone on January 31. The z excess on December 23 (+48 nanomaggies) is about 80 percent of the z excess at the flare peak of 2017 December 7 (+62 nanomaggies), so December 23 was near the peak. The z flux on November 15 is at the quiescent level (-9 +/- 6 nanomaggies against February 7). The excess is not an artefact of PSF matching: its aperture ratios agree with a point source within 0.04 in all bands, the result does not depend on the seeing (0.96-1.33 arcsec on these nights; all images are matched to 1.9 arcsec), and the host-annulus and CCD zero-point calibrations agree to 1.4 percent.

### 4.2 Time of the flare

Table 2. Half-rise time t_h of flare n = -2 (MJD). Source: `files/results/flare_m2_timing_*.json`.

| Variant | 2.5 % | 16 % | median | 84 % | 97.5 % |
| --- | --- | --- | --- | --- | --- |
| main (1.5", 1 %, free amplitudes) | 56628.8 | 56635.3 | 56642.0 | 56648.8 | 56650.5 |
| hot-blackbody colours | 56628.3 | 56633.0 | 56639.8 | 56642.5 | 56646.0 |
| g and r only | 56621.8 | 56634.0 | 56648.3 | 56652.5 | 56656.3 |
| aperture 1.0" / 2.0" | 56630.8 / 56628.5 | 56633.8 / 56636.5 | 56641.0 / 56642.3 | 56648.8 / 56648.8 | 56650.5 / 56650.8 |
| errors 0.5 % / 2 % | 56631.8 / 56625.3 | 56634.3 / 56634.8 | 56640.5 / 56643.0 | 56649.0 / 56649.0 | 56650.0 / 56652.3 |
| template smoothing 3 d | 56632.0 | 56636.8 | 56643.3 | 56649.0 | 56652.0 |

The single templates fit with chi2 = 1.0-6.0 for 12 points (best 1.0) (template 22, a flare with a data gap, fails with chi2 = 177 and has zero weight). The upper limit comes from the elevated z flux on December 23; the lower limit comes from the slow g and r decline on December 31 to January 4 and the quiescent z flux on November 15. Dip-equivalent time: MJD 56637.4 +/- 6.3 (68 percent 56630.5-56644.0; `dip_equivalent_m2.json`). The colour variants give 56633.7 +/- 4.9 (blackbody) and 56639.6 +/- 9.8 (g and r only).

![Figure 2](files/figures/fig2_timing_and_prediction.png)

**Figure 2.** Left: likelihood of the half-rise time for each template (grey), the template average (blue) and two variants. Right: observed minus predicted n = -2 dip time for clocks fitted to the 21 points of 2007-2026 ("ep" set) without the DECam point; error bars combine the prediction and measurement errors.

### 4.3 Clock tests

Table 3. Clock tests on the "ep" timing set (jitter 0.5 d). "Predicted" uses the 21 points without DECam. Source: `files/results/clock_tests_ep.csv` (other sets in `clock_tests_*.csv`).

| Clock | n_par | Delta AIC, 21 points | predicted dip n = -2 (MJD) | observed - predicted (d) | z | Delta AIC, 22 points | residual after refit (d) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| quad + sine (modulated) | 6 | 0.0 | 56630.4 +/- 0.9 | +7.0 | 1.1 | 0.0 | +7.0 |
| slow/fast/zero/renewed (k0-on-off-on) | 8 | 3.7 | 56621.0 +/- 1.6 | +16.4 | 2.5 | 9.0 | +15.8 |
| zero/fast/zero/step | 7 | 7.0 | 56608.5 | +28.9 | 4.5 | 25.1 | +26.6 |
| zero/fast/zero/renewed | 7 | 7.3 | 56608.5 | +28.9 | 4.5 | 25.4 | +26.5 |
| two-episode (new) | 8 | 9.0 | 56608.5 | +28.9 | 4.5 | 27.1 | +26.6 |
| constant Pdot (quad) | 3 | 60.7 | 56628.8 | +8.6 | 1.4 | 61.3 | +8.6 |
| cubic | 4 | 62.5 | 56629.2 | +8.2 | 1.3 | 62.9 | +8.0 |
| on-off-on / on-off-step (b03f0a97 forms) | 6 | 52 / 49 | 56629.6 / 56623.2 | +7.8 / +14.2 | 1.2 / 2.2 | 52 / 52 | +7.7 / +7.4 |

Out of sample, the DECam point lies +7.0 to +7.2 d after the modulated clock in three timing sets (+22.4 d in the relaxed-V set, where the 21-point fit picks another phase), +8.3 to +9.6 d after the constant-Pdot clock, +16.4 to +20.1 d after the best episodic clock and +26 to +29 d after the clocks with a constant period before 2016.

Table 5. Delta AIC after the refit with the DECam point (22 points; 0.5-d jitter; best model = 0).

| Set | modulated | best episodic (k0-on-off-on) | zero/fast/zero/renewed | two-episode | constant Pdot |
| --- | --- | --- | --- | --- | --- |
| main (SCI 067e9565) | 0.0 | 5.0 | 21.1 | 22.3 | 50.6 |
| ep | 0.0 | 9.0 | 25.4 | 27.1 | 61.3 |
| ep without 37, 38 | 0.0 | 8.4 | 24.5 | 2.6 (breaks -6, -2, 13, 20) | 57.4 |
| vrelax + ep | 13.6 | 0.0 (residual +18.8 d) | 11.9 | 13.6 | 107.6 |

Without the 2025-2026 optical points, a two-episode clock with decrease episodes at cycles -6 to -2 (2012-2013) and 13 to 20 (2018-2020), and a constant period at all other times, fits nearly as well as the modulated clock (Delta AIC = 2.6). This is the staircase of Section 4.4. In this set the step forms of SCI b03f0a97 and 067e9565 also fit (Delta AIC = 2.6-9.3; with 1-d jitter the zero/fast/zero/step clock has breaks -18, 17, 18 and a residual of +2.9 d), and these clocks predict the flare-41 dip on MJD 61365.5-61366.5.

![Figure 3](files/figures/fig3_oc_and_periods.png)

**Figure 3.** Top: O-C of the dip-equivalent timing points ("ep" set plus DECam) against the refitted constant-Pdot clock, with three refitted clocks. Bottom: mean period between successive timing points (errors below 7 d; aqua: intervals that use the DECam point; horizontal bars show the interval) and the clock periods. Cycle n = -21 is 2007 December, n = -2 is 2013 December, n = 14 is 2018 November, n = 21 is 2020 December, n = 34 is 2024 October.

### 4.4 Period history

Mean periods between timing points (`summary.json`, key `local_periods`):

| Interval | Years | Mean period (d) |
| --- | --- | --- |
| n = -21 to -19 | 2007.9-2008.6 | 116.0 +/- 1.7 |
| n = -19 to -2 | 2008.6-2013.9 | 116.03 +/- 0.43 |
| n = -2 to 8 | 2013.9-2016.9 | 111.6 +/- 0.6 |
| n = 8 to 12 | 2016.9-2018.2 | 112.0 +/- 0.4 |
| n = 12 to 14 | 2018.2-2018.8 | 112.4 +/- 0.6 |
| n = 21 to 34 | 2020.9-2024.8 | 108.49 +/- 0.10 |

The period did not decrease measurably from 2007-2008 to 2008-2013. It fell by 4.4 +/- 0.8 d across 2011-2015 (centre of the -19..-2 interval to centre of the -2..8 interval; mean rate -0.33 d per cycle, 2.5 times the slow rate of the best episodic clock) and stayed near 112 d in 2016-2018. The 2018-2020 decrease (-0.55 d per cycle) and the 2020-2024 stall follow.

### 4.5 Modulation period and bootstrap

![Figure 4](files/figures/fig4_sine_period_profile.png)

**Figure 4.** Profile chi2 of the modulation period of the quad + sine clock, with (solid) and without (dashed) the DECam point, for the SCI 067e9565 set and for the set with the EP cycle-34 ingress.

With the DECam point the second minimum of SCI 067e9565 at 36.4 cycles rises from Delta chi2 = 9.2 to 16.5 (main set) and from 25.0 to 32.0 (ep set). The best period is 19.65 cycles (main; 1-sigma 18.9-20.6) or 18.8 cycles (ep; 18.1-19.5), that is 5.6-6.1 years.

Table 4. Parametric bootstrap, "ep" set with DECam, 200 simulations each (`files/results/bootstrap_main_ep1_*.csv`). Observed Delta AIC (episodic minus modulated) = 9.0.

| Simulated truth | P(Delta AIC >= 9.0) | Delta AIC quantiles 2.5 / 16 / 50 / 84 / 97.5 percent |
| --- | --- | --- |
| episodic clock (k0-on-off-on, refitted with DECam) | 0.010 (2 of 200) | -8.7 / -4.1 / -0.3 / +2.6 / +6.5 |
| modulated clock (quad + sine, refitted with DECam) | 0.14 | -1.9 / +1.4 / +5.2 / +8.5 / +13.2 |

The observed preference is unlikely if the episodic clock is true (p = 0.01, one-sided; 95 percent binomial range 0.001-0.036) and typical if the modulated clock is true. The bootstrap assumes Gaussian timing errors with 0.5-d jitter and fixed cycle numbers.

## 5. Interpretation

**What the 2013 flare adds.** Before this study, the 2009-2013 gap allowed a period that was constant until about 2016, a slow steady decrease, or a modulation. The December 2013 flare fixes the mean period over 2008-2013 at 116.03 +/- 0.43 d. A constant period until 2015-2016 then cannot reach the 2016-2018 timing: those clocks miss the flare by 27-29 d. A slow steady decrease from 2007 (the first segment of the best episodic clock) also arrives too early, because the period must stay near 116 d until about 2013 and then drop by about 4 d within a few years. This is a fast-decrease episode similar in size to the 2018-2020 episode, about 20 cycles earlier.

**What kind of clock.** The record now shows two drops of about 4 d, each followed by a plateau (about 112 d in 2016-2018; 108.5 d in 2020-2024). A steady decrease with a modulation of 18.8-19.7 cycles describes this, and so does a staircase of discrete episodes. A smooth secular clock (gravitational waves, constant drag, constant Pdot, cubic) is excluded by Delta AIC > 50. The precessing star-disc drag clock of SCI cd4bd328 has a 70-77 cycle modulation period and already failed on the 2007-2008 points (SCI 067e9565). The 2020-2024 stall is then the second plateau, not a unique switch-off of the decay. If the modulation repeats, the next drop is due in about 2024-2027. The SPHEREx and TESS flares of 2025-2026 (cycles 37-38), which are 7-8 d early on the constant X-ray clock, agree with this, but SCI 967e3773 showed that the optical lag can change by 4 d, so they do not prove it.

**A physical scale.** A periodic modulation of the orbital decay requires a periodic change of the encounter geometry. General-relativistic apsidal precession of a near-parabolic orbit advances the pericentre by 3 pi R_g / r_p per orbit. One modulation per precession cycle (18.8-19.7 orbits) gives r_p = 28-30 R_g; two per cycle (for example a drag or impact geometry that repeats every pi) give r_p = 56-59 R_g. For the partial disruption of a Sun-like star (r_p = 1-2 tidal radii; tidal radius 47 (M/1e6 Msun)^(-2/3) R_g), this points to a black hole mass of about 1e6-6e6 Msun. This is an order-of-magnitude scale with stated assumptions (orbit near parabolic, Schwarzschild precession, solar-type star), not a measurement; Lense-Thirring or third-body precession would give other scales.

**What this does not show.** We do not measure the flare peak or the rise; the time rests on the decline shape and on the z/g relation. We do not know the 2013 optical lag.

## 6. Limitations

- One flare. Seven DECam nights sample the end of the rise (z), the decline (g, r) and the quiescent level. Single-template medians range from 56634.3 to 56648.5; the template average and all variants give 56640-56648 (g and r only: 95 percent range 56621.8-56656.3).
- The half-rise lag of 4.75 d is assumed for 2013. SCI 967e3773 found a lag of 1.0 d in cycle 34; a shorter lag in 2013 would move the dip later and make all clocks miss by more. Broad flares with precursors (2022-2023) have longer lags; the 2013 decline is not broad, but the rise is not observed.
- The relaxed-rule ASAS-SN V flares of 2015-2017 (n = 2, 4, 5, 10) scatter by about 4 d around any clock. With them the episodic clock is preferred by AIC, but it misses the DECam flare by 2.9 sigma; the set is not described well by any clock.
- The flux calibration uses the host annulus; residual PSF-matching errors are below the 1-percent error floor (duplicate CCDs differ by 0.1 percent; quiescent epochs of 2015-2018 differ by 3 percent, which includes AGN variability over years).
- The modulated clock is phenomenological. The modulation period rests on two drops; a modulation and a random sequence of episodes are not separated by present data.
- No flux cross-calibration between DECam and ASAS-SN apertures was needed (amplitudes are free), but the colour variants show that a hot-blackbody prior moves the time by about 2 d.

## 7. Reproduction

```
bash files/code/run_all.sh ./campaign ./scratch            # needs curl, sci, Python 3.12, files/code/requirements.txt
```

`00_retrieve.sh` downloads the DECam stamp tarball (34 MB) and the ASAS-SN light curve into scratch and unpacks the three SCI input bundles; `01`-`07` do the photometry, timing, clock tests, bootstrap and figures. Run time on one CPU: photometry 15 s, timing variants 1 min, clock tests 4 min, bootstrap about 20 min per hypothesis. Hashes of all inputs: `files/data/provenance/`. The ASAS-SN Sky Patrol service is live and is being rebuilt (notice of 2026-11-03), so a new download can differ from the snapshot (its hash is recorded).

## 8. Files

- `files/code/` (MIT): `00_retrieve.sh`, `00_get_asassn.py`, `01_decam_photometry.py`, `02_register_calibrate.py`, `02b_excess_position.py`, `03_flare_timing.py`, `03b_timing_variants.sh`, `03c_dip_equivalent.py`, `04_clock_tests.py`, `04b_clock_variants.sh`, `05_profile_bootstrap.py`, `06_figures.py`, `07_summary.py`, `run_all.sh`, `requirements.txt`.
- `files/results/`: DECam nucleus photometry (`decam_nucleus_phot.csv`, `decam_nucleus_calibrated.csv`), excess position (`excess_position.json`), timing fits and likelihood grids (`flare_m2_timing_*.json`, `flare_m2_timing_grid_*.csv`), dip-equivalent times (`dip_equivalent_m2*.json`), timing sets used (`timing_set_*.csv`), clock tests and curves (`clock_tests_*.csv`, `clock_curves_*.csv`), sine profiles (`sine_profile_*.csv`), bootstrap (`bootstrap_*.csv`), `summary.json`, logs.
- `files/figures/`: Figures 1-4.
- `files/data/provenance/`: exposure list, SHA-256 of the DECam stamps, ASAS-SN snapshot and SCI inputs.
- `files/NOTICE_external_data.md`: external data and acknowledgements.

## References

- Payne A. V. et al. 2021, ApJ 910, 125; 2022, ApJ 926, 142.
- Dey A. et al. 2019, AJ 157, 168 (Legacy Surveys); DES Collaboration 2018, ApJS 239, 18; 2021, ApJS 255, 20.
- Shappee B. J. et al. 2014, ApJ 788, 48; Kochanek C. S. et al. 2017, PASP 129, 104; Hart K. et al. 2023, arXiv:2304.03791 (ASAS-SN).
- Gaia Collaboration 2023, A&A 674, A1.
- SCI campaign publications cited in `sci.json`.
