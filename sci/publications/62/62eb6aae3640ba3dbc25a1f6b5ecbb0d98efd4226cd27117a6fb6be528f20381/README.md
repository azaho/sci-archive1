# SPHEREx 2025-2026 spectra of 598 main-belt asteroids agree with AKARI 2.7 um band depths and show that a Gaia DR3 0.7 um band raises the 3 um band rate from 37% to 62% at all sizes from 16 to 400 km

Job `sci-1107-dell-astronomy-7f5aca2585fd`, topic astronomy, machine dell (campaign 11_07_2026), model `claude-opus-5-5` (Claude Code). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Hydrated (water- or OH-bearing) minerals on asteroids give an absorption band near 2.7-3 um. Ground telescopes cannot see most of this band because water in the air of the Earth absorbs it. A weaker band near 0.7 um (Fe2+-Fe3+ charge transfer in phyllosilicates) is easy to see in visible spectra. Rivkin (2012) and earlier work used the rule "a 0.7 um band means a 3 um band" to count hydrated asteroids from visible survey data. Vilchez et al. (2026, MNRAS 546, staf2171) found, in 20 asteroids, that many objects with a 0.7 um band have no 3 um band, "especially among bodies smaller than 100 km". We asked: (1) Can the SPHEREx all-sky survey measure the 3 um band of main-belt asteroids? (2) In a large sample, how often does a Gaia DR3 0.7 um band come with a 3 um band, and does this change with size?

**Method.** We matched 4,114 numbered asteroids (H < 12.5, with a Gaia DR3 reflectance spectrum) to 270,830 SPHEREx exposures (2025-04-24 to 2026-10-28). We used two-body orbits for the first match and JPL Horizons positions seen from the SPHEREx spacecraft for the final positions. We selected 1,034 asteroids (816 with albedo pv <= 0.10, 160 random controls with pv > 0.15, 63 objects of the AKARI survey of Usui et al. 2019) and 15,160 exposures. In each exposure, detector D4 (2.42-3.82 um) and detector D1 (0.75-1.1 um) see the same sky at the same time. We did PSF photometry of the moving asteroid in small pixel boxes of both files (25,857 Level-2 files, read by HTTP byte ranges). The ratio D4/D1 removes the rotation light curve and the observing geometry. We divided by the solar spectrum, removed thermal emission with a NEATM model (eta = 1.0; SBDB diameter and albedo), and multiplied by the Gaia DR3 reflectance at the D1 wavelength. This gives the reflectance at 2.4-3.45 um relative to 0.55 um. The band depth D2 is 1 minus the mean reflectance at 2.70-2.88 um divided by a straight continuum through 2.42-2.62 um and 3.15-3.45 um. We wrote the cuts, windows and the detection rules before the full photometry (`files/provenance/analysis_plan.md`).

**Results.**
1. *Validation.* For the 44 AKARI asteroids that passed the cuts, SPHEREx D2 agrees with the AKARI 2.7 um band depth: Pearson r = 0.93, Spearman rho = 0.74, slope 1.06, offset -0.026, rms difference 0.051 (Figure 2). The detection decision agrees for 39 of 44 objects. For example, (13) Egeria gives 37% (AKARI 40.5%), (51) Nemausa 51% (46.6%), (49) Pales 30% (29.9%) and (10) Hygiea 15% (17.8%).
2. *False bands.* High-albedo controls have median D2 = -0.021 and a robust scatter of 0.052. Only 2 of 83 controls (2.4%, 95% CI 0.7-8.4%) pass the band rule (D2 >= 0.05 and 3 sigma). The bootstrap errors are 2.2 times too small when we compare them with the scatter of the controls. Tables give both errors.
3. *Main test.* Among 501 low-albedo asteroids (16-407 km, median 70 km), 62% (164/266; 95% CI 56-67%) with a Gaia 0.7 um band have a SPHEREx 3 um band, against 37% (87/235; 31-43%) without a 0.7 um band (Fisher p = 4e-8, odds ratio 2.7). D2 and the 0.7 um depth have Spearman rho = 0.46 (Figure 3).
4. *Size.* The rate does not depend on size. Below 100 km it is 61% (111/183) with a 0.7 um band and 36% (67/186) without. At 100 km or more it is 64% (53/83) and 41% (20/49). In a logistic model, the size term (p = 0.25) and the size-by-band interaction (p = 0.82) are not significant. Below 30 km, 8 of 13 objects with a 0.7 um band have a 3 um band. The data do not support a size-dependent loss of the 3 um band below 100 km.
5. *0.7 um band without a 3 um band.* Of the 102 objects with a Gaia 0.7 um band and no detected 3 um band, only 6 have a D2 upper limit below 5% (2 sigma, inflated errors). Four of these 6 are in the outer belt or beyond (a > 3.2 au): (65) Cybele, (153) Hilda, (361) Bononia, (911) Agamemnon. The other two are (792) Metcalfia and (1042) Amazone. The other 96 cases are limited by noise.
6. *Exploratory (not planned).* The 3 um rate increases with the Gaia 0.7 um depth: 39% below 1%, 40% at 1-2%, 64% at 2-3% and 83% at 3% or more (Figure 4). Thus weak Gaia 0.7 um detections (1-2%) do not predict the 3 um band better than no detection. Bus Ch types have the band in 95% (53/56). The rate decreases outward in the belt. Beyond 3.3 au (Cybele and Hilda zones) only 23% of the objects with a 0.7 um band have a band in our 2.70-2.88 um window.

**Main limitation.** Our band window measures the sharp 2.7-2.9 um (phyllosilicate OH) band. It does not measure rounded 3.1 um (Ceres- or Themis-like, ice) bands well, because these bands also lower the long continuum (3.15-3.45 um). Thus our "no band" class includes objects with a different band shape, mainly in the outer belt. Other limitations are below.

## What is new

- This is, as far as we know, the first large-sample measurement of the 2.7-3 um hydration band of asteroids from SPHEREx data, and the first in this campaign record on asteroid composition (the record had only NEA Yarkovsky drifts, sci:sha256:67a369ea..., 3I/ATLAS and comet 29P).
- The method uses the simultaneous D1 exposure as the normaliser. This removes rotation, distance and phase effects without a light-curve model. The method needs no spectral template: Gaia DR3 gives the D1 reflectance.
- A large-sample test (501 objects, 16-407 km) of the 0.7 um to 3 um rule. It gives a quantitative conditional rate and its dependence on the 0.7 um depth. It contradicts the size dependence suggested from 20 objects by Vilchez et al. (2026).
- A catalogue of D2 for 598 asteroids (`files/results/spherex_band_depth_catalogue.csv`).

## Methods (details)

**Sample.** JPL SBDB query (2026-11-12) of numbered asteroids with H < 12.5 (5,737 objects). Gaia DR3 `sso_reflectance_spectrum` exists for 4,114 of them. Gaia 0.7 um depth `d07` = 1 - mean(R682, R726) / continuum at 704 nm, where the continuum is a line through mean(R550, R594) and mean(R814, R858). We used only bands with flag 0. "0.7 um band present" means d07 >= 0.01 and d07 >= 3 sigma (`code/03_sample.py`).

**Exposure match.** We downloaded the D1 footprint table of all SPHEREx exposures (IRSA TAP `spherex.plane`, 270,830 rows; `code/01_planes.py`). Two-body ephemerides (`code/twobody.py`) on a 6-hour grid gave 214,763 candidate (asteroid, exposure) pairs inside the frame (`code/04_coarse_match.py`). The two-body error for (512) was 97 arcsec after 300 days; the final positions come from Horizons.

**Selection** (`code/06_select.py`). We kept asteroids with predicted V < 17 and at least 4 pairs at predicted lambda4 2.68-2.92 um, 3 at 2.42-2.62 um and 2 at 3.15-3.45 um. Groups: all with pv <= 0.10, the AKARI objects, and 160 random controls with pv > 0.15 (seed 1). Per asteroid we kept the brightest 6, 5 and 4 pairs in these windows.

**Positions.** Horizons, observer centre 500@-163182 (SPHEREx), at the mid-time of each exposure, interpolated to MJD-AVG of the file header (`code/05_horizons.py`). On test files, the Horizons position and the image centroid agree within 0.25 px (6.2 arcsec pixels); a free-position grid fit found no better position.

**Photometry** (`code/08_phot.py`, based on sci:sha256:1252e08c). 11 x 11 pixel stamp, PSF from the file, plane background, VARIANCE weights. Gaia DR3 stars with G < 19.5 inside the stamp are fitted at the same time at fixed positions. Important flag facts: FLAGS bit 19 (OUTLIER) and bit 21 (SOURCE) are set on the asteroid itself (the pipeline flags moving and known solar-system objects). Therefore we do not mask them. We mask bit 1 (OVERFLOW) and the other bad-pixel bits. 30,070 file boxes were read; 29,064 fits are valid; 30 files failed in the WCS inversion.

**Reflectance** (`code/09_reflectance.py`). q = [(F4 - F_thermal) / F1] / [S(lambda4) / S(lambda1)] x R_Gaia(lambda1). S is the CALSPEC Kurucz solar model averaged over the channel width. R_Gaia is interpolated between 0.726 and 0.946 um and kept flat beyond 0.946 um (the Gaia 0.99 and 1.03 um points are not reliable). NEATM: eta = 1.0, emissivity 0.9, G from SBDB or 0.15.

**Band depth** (`code/10_banddepth.py`). Pair cuts: no OVERFLOW pixel in the 3 x 3 core, no Gaia star within 2.5 px that is brighter than V + 2.5, chi2_red < 50 in both detectors, thermal fraction < 0.3. Then 3-sigma (MAD) clipping in each window. D2 uses the two-sided continuum; D1s = 1 - q_band / q_short uses only the short side. Errors come from 1000 bootstrap samples over pairs. 11,344 of 14,181 pairs passed; 598 asteroids have enough pairs. The cut on the SOURCE flag in the first plan was dropped after a 47-object pipeline test showed that this flag marks the asteroid itself (89% of pairs). This change came before any test result.

**Tests** (`code/11_tests.py`, `code/13_robust.py`, `code/15_extra.py`). Wilson intervals, Fisher exact test, logistic regression with log10 diameter.

## Robustness (files/results/robustness.json)

| Variant (pv <= 0.10) | P(3 um given 0.7 um) | P(3 um given no 0.7 um) | Fisher p |
|---|---|---|---|
| Baseline | 0.617 (n 266) | 0.370 (n 235) | 4e-8 |
| D2 >= 0.03 | 0.643 | 0.379 | 5e-9 |
| D2 >= 0.08 | 0.583 | 0.311 | 1e-9 |
| d07 >= 0.005 | 0.605 | 0.333 | 3e-9 |
| d07 >= 0.02 | 0.747 | 0.392 | 2e-13 |
| One-sided depth D1s | 0.541 | 0.251 | 4e-11 |
| Control offset (+0.021) removed | 0.699 | 0.426 | 7e-10 |
| NEATM eta = 0.8 | 0.511 | 0.265 | 3e-7 |
| NEATM eta = 1.3 | 0.686 | 0.421 | 3e-9 |

For asteroids below 40 km the two rates are 0.50-0.67 and 0.17-0.35 in all variants. The split-half test (band-window pairs before and after the median time, median 119 days apart) gives r = 0.77 and a robust scatter of 0.05 per half.

## Limitations and open problems

- The 2.70-2.88 um window and a straight continuum to 3.15-3.45 um favour sharp (phyllosilicate) bands. Rounded 3.1 um bands are under-measured. A shape-aware fit (for example Usui-type local continua, or band-centre fits with SPHEREx D5 at 3.8-4.4 um for the thermal tail) is the next step.
- Thermal emission: the NEATM eta changes the rates by up to 0.1, and D2 has a weak correlation with the modelled thermal fraction (rho = 0.34). The one-sided depth D1s, which does not use the long continuum, also decreases with heliocentric distance (rho = -0.23). Thus the outward decrease is probably mostly real, but part of it can come from thermal residuals.
- Errors: bootstrap errors are about 2.2 times too small (compared with the control scatter). The 3-sigma rule with bootstrap errors is therefore weaker than it looks; the D2 >= 0.05 condition and the control false-band rate (2.4%) set the real threshold.
- SPHEREx calibration: S-type controls have D2 = -0.02 (AKARI offset -0.026). We did not apply a channel-level calibration with solar-analog stars.
- The Gaia DR3 0.7 um depth is noisy at 1-2%. Weak detections can be false or can come from other minerals. The large-sample rate (62%) therefore mixes real and false 0.7 um bands; the rate for 0.7 um depths >= 3% (83%) is the better estimate of the physical link.
- Rotation: D4/D1 removes brightness changes but not real colour changes across the surface.
- Selection: H < 12.5, V < 17 at the SPHEREx epochs, and enough pairs. Only 13 + 39 objects are below 30 km. Saturated (OVERFLOW) cores remove the brightest objects: (1) Ceres and (4) Vesta gave no valid fit, and all pairs of (2) Pallas had OVERFLOW pixels.
- SPHEREx QR products are preliminary. Later releases can change the calibration.

## Files

- `files/results/spherex_band_depth_catalogue.csv`: 598 asteroids, D2, bootstrap and inflated errors, D1s, pair counts, thermal fraction, Gaia d07, flags `b3` (3 um band) and `g07` (0.7 um band). `band_depths.csv` is the full analysis table; `band_depths_eta0.8.csv` and `band_depths_eta1.3.csv` are the thermal variants.
- `files/results/tests.json` (H1, H2, controls), `h2_by_diameter.csv`, `robustness.json`, `extra.json` (exploratory, including the 6 confident "0.7 um without 3 um" objects), `split_half.csv`.
- `files/data/spherex_asteroid_photometry.csv.gz`: our PSF fluxes (uJy) in D1 and D4 for 29,064 file boxes. `pair_reflectance.csv.gz`: 14,181 D1/D4 pairs with q, thermal model, geometry and quality columns. `asteroid_properties.csv`: SBDB values and our Gaia-derived indices for the 1,034 selected asteroids.
- `files/provenance/`: `pairs.csv.gz` (the exact selection), `photometry_jobs.csv.gz` (file URIs and predicted pixels), `spherex_files_irsa_md5.csv.gz`, `input_sha256.txt`, `analysis_plan.md`, `predmodel_1252e08c.json`, `environment.txt`.
- `files/figures/`: four PNG figures (Figures 1-3 are display items; Figure 4, `fig4_exploratory_depth_region.png`, is the exploratory figure).
- `files/NOTICE-external-data.md`: sources, licences and credits of external data.

## Reproduce

- Offline, from the bundle tables (about 1 min): `bash files/code/reproduce_from_bundle.sh files [usui2019_band_depth.csv]` in an empty folder. It recomputes band depths, tests, robustness and figures and prints the H2 rates for comparison. To get the AKARI table: `python files/code/00_get_usui2019.py scratch/usui` (needs network).
- Full run (about 3 h on 2 CPUs, network): `bash files/code/run_all.sh files` in an empty folder. It downloads all external inputs into `./scratch`. With `EXACT=1` (default) it uses the published selection `pairs.csv`; with `EXACT=0` it rebuilds the exposure table and the selection (SBDB elements and SPHEREx releases can change).
- Use `OMP_NUM_THREADS=1`. The IRSA IBE server limits request rates; the photometry uses the AWS Open Data mirror.

## Citations

- sci:sha256:1252e08c45d107a4fd2bd9a2c003550368d58c7131571e5af4bf364c2d03d591 - SPHEREx range-read and PSF-photometry code, position and wavelength model (reused).
- Usui F., Hasegawa S., Ootsubo T., Onaka T. 2019, PASJ 71, 1, doi:10.1093/pasj/psy125 (arXiv:1810.03828) - AKARI 2.7 um band depths (validation).
- Vilchez A., Duffard R., Spagnuolo M. G., Pinilla-Alonso N. 2026, MNRAS 546, staf2171, doi:10.1093/mnras/staf2171 - claim tested.
- Rivkin A. S. 2012, Icarus 221, 744, doi:10.1016/j.icarus.2012.08.042 - 0.7 um to 3 um link.
- Gaia Collaboration, Galluccio L. et al. 2023, A&A 674, A35, doi:10.1051/0004-6361/202243791 - Gaia DR3 asteroid reflectance spectra.
- Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1, doi:10.1051/0004-6361/202243940 - Gaia DR3.
- NASA SPHEREx mission, Level-2 quick-release images, NASA/IPAC Infrared Science Archive (https://irsa.ipac.caltech.edu/Missions/spherex.html).
- Harris A. W. 1998, Icarus 131, 291 - NEATM.
