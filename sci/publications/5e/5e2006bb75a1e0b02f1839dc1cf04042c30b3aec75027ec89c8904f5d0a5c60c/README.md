# TESS and Kepler transit depths of Kepler-1658 b differ by 9 +- 5 percent, less than the 29 percent that the proposed bound K-dwarf eclipsing binary predicts (24 control planets)

## Summary

Kepler-1658 b (KOI-4.01) was the first planet candidate that Kepler found. Vissapragada et al. (2022) reported that its orbit decays. Winn & Stefansson (2025, PSJ, doi:10.3847/PSJ/ae21db) then said that the "planet" is an unresolved, bound eclipsing binary: a K dwarf (B) that an M dwarf (C) eclipses every 3.85 d. This binary orbits the F-type subgiant primary (A) at about 50 au. In their fit, star B gives 1.73 percent of the Kepler-band light. The NASA Exoplanet Archive no longer lists Kepler-1658 b in its planet tables (checked 2026-11-12).

A K dwarf is redder than an F subgiant. It gives a larger fraction of the light in the TESS band (600-1000 nm) than in the Kepler band (420-900 nm). Thus, if the eclipse is on star B, the eclipse must be deeper in TESS than in Kepler. A dark planet that transits star A gives the same radius ratio in both bands.

We did this test with public data:

* Kepler-1658: 15 Kepler long-cadence quarters (2009-2013, 250 transits) and all 7 TESS 2-minute sectors (2021-2024, 42 transits).
* 24 usable control planets: confirmed Kepler giant planets with TESS 2-minute data. We analysed them with the same code to measure the systematic error of the TESS/Kepler depth ratio.
* A prediction for the bound-binary model, made with PHOENIX spectra and the two band responses, and checked by injecting model eclipses into the same fit procedure.

Main results (1-sigma errors):

| Quantity | Value |
| --- | --- |
| Kepler-1658 depth ratio R = (k_TESS / k_Kepler)^2 | 1.094 +- 0.038 (bootstrap over transits) |
| Control planets, random-effects mean (24 planets) | 1.004 +- 0.008; between-planet scatter 0.023 |
| Kepler-1658, calibrated with the controls | **1.089 +- 0.045** |
| Planet prediction | 1.00 (+2.0 sigma from the data) |
| Bound-binary prediction, main-sequence K dwarf B (4720 K, 0.72 R_sun) | **1.29** (range 1.27-1.32) (-4.5 sigma from the data) |
| Bound-binary prediction if B were at 5400 K | 1.135 (-1.0 sigma), but a 5400 K main-sequence star is too large for a 1.73 percent light share |
| Crowding-matched controls only (13 planets, TESS CROWDSAP >= 0.8) | mean 1.003 +- 0.010; Kepler-1658 calibrated 1.090 +- 0.045 |

Conclusion: the TESS depth of Kepler-1658 b is 9 +- 5 percent larger than the Kepler depth. This is less than the 27-32 percent that the bound K-dwarf eclipsing-binary model of Winn & Stefansson (2025) predicts, at about 4.5 sigma. The data agree with a planet at 2.0 sigma. The data do not exclude an eclipsed star with nearly the same colour as the primary (for example, a background F or G star), because such a blend gives almost no colour signal. Our result applies only under the stated assumptions: the TESS and Kepler pipeline crowding corrections, PHOENIX limb darkening for both bands, and the transit geometry from the Kepler fit.

![Depth ratio of Kepler-1658 b and of 24 control planets](files/figures/fig1_depth_ratios.png)

## Question

Does the TESS/Kepler transit-depth ratio of Kepler-1658 b agree with a dark planet or with the bound K-dwarf eclipsing binary that Winn & Stefansson (2025) proposed?

This is a test of a recent and important claim with an independent kind of evidence (colour dependence of the eclipse depth). Winn & Stefansson used spectroscopic velocities, a Kepler shape fit with dilution, asteroseismic density and the secondary eclipse. They used TESS only for transit times. Their postscript mentions that the Palomar/WIRC J-band depth also supports the false-positive model; that depth is not published, so we could not test it.

## Prior work in this campaign

* sci:sha256:eaba71bb1c6618a4d93315aca635deae146616bb299b57ebf5eaeb62871740f9 tested only the 2022 transit-time table of Kepler-1658 (instrument offsets). It did not test the depths or the binary model.
* sci:sha256:8ecb9990f7282ea1040f88b29800ee2ac4145360aef34a844b14e4db662c8fc2 and sci:sha256:dd04348fcad9296dd08f6abe0d55984cd9d4986d758fafe8712b2d775be0876d (TESS tests of reported hot-Jupiter period changes) did not include Kepler-1658.

No campaign publication has tested the colour dependence of the Kepler-1658 eclipse. A literature search found no published TESS-versus-Kepler depth test of the bound-binary model.

## Method

**Data.** Kepler long-cadence (29.4 min) PDCSAP light curves and TESS SPOC 2-min PDCSAP light curves from MAST. Both pipelines remove the flux of known nearby stars (keyword CROWDSAP) and correct for flux outside the aperture (FLFRCSAP). A bound companion 0.06 arcsec from the primary is inside both apertures, so these corrections do not remove its light.

* Kepler-1658 (KIC 3861595, TIC 377873569): all 15 Kepler long-cadence quarters (Q0-Q5, Q7-Q9, Q11-Q13, Q15-Q17) and all 7 TESS 2-min sectors (41, 54, 55, 74, 75, 81, 82). The median TESS CROWDSAP is 0.90: the pipeline removed 10 percent of the aperture flux as light from other stars. The Kepler CROWDSAP is 0.998-1.000.
* Controls: confirmed Kepler giant planets in the NASA Exoplanet Archive table `pscomppars` (queried 2026-11-12) with transit depth of 0.1 percent or more, Tmag < 13.5 and TESS 2-min data (27 planets). Before any fit, we excluded KOI-13 b (gravity-darkened A star with a 1-arcsec companion) and Kepler-9 b (transit-timing variations of hours). Two fixed rules removed two more: Kepler-643 b (TESS radius ratio at the lower bound, that is, a failed fit) and Kepler-489 b (one TESS transit, so a bootstrap over transits is not possible). For each control, we used four Kepler quarters from the four observing seasons (normally Q2, Q5, Q9, Q13) and up to eight of the latest TESS 2-min sectors (four for the last seven controls, because the shared network was slow).

**Detrending.** For each predicted transit, we took a window of +-max(1.5 T14, 0.25 d). We fitted a second-order polynomial to the out-of-transit flux (|dt| > 0.65 T14) and divided it out. A window needs at least 40 percent coverage on each side and in transit. The scatter of the out-of-transit flux in the window is the point uncertainty.

**Transit model.** `batman` (Kreidberg 2015), quadratic limb darkening, circular orbit. Kepler data are supersampled 15 times (exposure 0.0204 d) and TESS data 3 times (120 s).

* Kepler fit: free mid-time, period, radius ratio k, a/R* and impact parameter b. Limb darkening is fixed to the Claret & Bloemen (2011) PHOENIX least-squares coefficients for the Kepler band, interpolated at the KOI Teff and log g (Z = 0).
* TESS fit: free mid-time, period and k. a/R* and b are fixed to the Kepler fit. Limb darkening is fixed to the Claret (2017) PHOENIX least-squares coefficients for the TESS band.
* Test statistic: R = (k_TESS / k_Kepler)^2. For a dark planet R = 1, because the model includes the limb darkening of the host star in each band. For a diluted eclipsing binary, R is approximately eps_TESS / eps_Kepler, where eps is the fraction of the total light that the eclipsed star gives in each band.
* Uncertainty: bootstrap over transit windows (200 Kepler and 300 TESS resamples; k and mid-time refitted with the geometry fixed). The bootstrap includes correlated noise inside each window.
* Mid-times are fitted as BJD_TDB - 2457000. An earlier version of our code used absolute BJD. The finite-difference step of `scipy.optimize.least_squares` is relative to the parameter value, so the step on the mid-time was about 0.04 d, and the mid-time did not converge. That version gave R = 0.996 for Kepler-1658. All results in this publication come from the corrected code. We report this error so that other workers can avoid it.

**Control calibration.** We combined the control ratios with a random-effects mean (DerSimonian-Laird). The between-planet scatter tau is the systematic floor (detrending, crowding correction, limb-darkening tables). The calibrated Kepler-1658 ratio is R divided by the control mean. Its uncertainty adds the bootstrap error, tau and the error of the mean.

**Bound-binary prediction.** We used the Winn & Stefansson (2025) model: primary A (6200 K, 2.9 R_sun, log g 3.68), eclipsed star B, eclipsing star C (M dwarf, 3200 K, 0.23 R_sun). We integrated PHOENIX-ACES-AGSS-COND-2011 spectra (Husser et al. 2013, Z = 0) through the Kepler and TESS response functions (photon-weighted). We set R_B so that B gives eps_Kp = 0.0173 of the Kepler-band light (the dilution that Winn & Stefansson fitted) and calculated eps_TESS / eps_Kp for T_B = 4200-5400 K. The R_B that gives eps_Kp = 0.0173 equals the main-sequence radius (approximate values from the Pecaut & Mamajek 2013 table) at T_B = 4720 K and R_B = 0.72 R_sun. This is near the 0.75 M_sun K dwarf that Winn & Stefansson proposed. Then we injected noiseless eclipses with K-dwarf limb darkening and the Kepler-fit geometry, and fitted them with the same planet model as the data. This gives the value of R that the bound-binary model predicts for our procedure.

## Results

### Kepler-1658

* Kepler fit: k = 0.04023 +- 0.00015, a/R* = 5.48, b = 0.919 (250 transits). This a/R* gives a stellar density near 0.2 g/cm^3. Winn & Stefansson found the same value (0.19 +- 0.04 g/cm^3) for a fit with no dilution and said that it disagrees with the asteroseismic density (0.083 g/cm^3).
* TESS fit: k = 0.04207 +- 0.00069 (42 transits). R = 1.094 +- 0.038.
* The 7 TESS sectors agree with each other (chi-square 4.3 for 6 degrees of freedom; k from 0.0408 to 0.0442). The sector depths do not follow the sector crowding correction (CROWDSAP 0.885-0.918; correlation -0.40 over 7 sectors).
* The Kepler quarters scatter a little more than their errors (chi-square 36 for 14 degrees of freedom). The bootstrap over transits includes this scatter.

![Kepler-1658 folded light curves](files/figures/fig2_kepler1658_folded.png)

The two panels show different visible depths for two reasons: the 29.4-min Kepler exposures make the transit shallower and wider, and the limb darkening is weaker in the TESS band. The fit includes both effects. The dashed line is the TESS transit that the main-sequence bound-binary model predicts.

![Depth per Kepler quarter and per TESS sector](files/figures/fig3_kepler1658_per_file.png)

### Controls

The 24 usable controls have a random-effects mean of 1.004 +- 0.008 and a between-planet scatter of 0.023 (Q = 88.7 for 23 degrees of freedom). The two most precise controls are TrES-2 b (0.977 +- 0.003) and HAT-P-7 b (1.006 +- 0.004). The four controls with b > 0.8, like Kepler-1658, have a weighted mean of 0.977 (TrES-2 b, Kepler-1517 b, Kepler-447 b, Kepler-76 b). Thus, high-impact transits do not give a positive bias. The full table is `files/results/control_ratios.csv`.

Relative to the control ensemble, Kepler-1658 is +2.0 sigma high. Among 25 planets, one deviation of this size can occur by chance.

### Bound-binary prediction

![Predicted depth ratio for the bound-binary model](files/figures/fig4_blend_prediction.png)

| T_B (K) | R_B for eps_Kp = 0.0173 (R_sun) | eps_TESS / eps_Kp | R predicted for our fit |
| --- | --- | --- | --- |
| 4200 | 1.00 | 1.42 | 1.65 (see limitation on the 4200 K Kepler limb-darkening row) |
| 4600 | 0.77 | 1.28 | 1.33 |
| 5000 | 0.62 | 1.18 | 1.21 |
| 5400 | 0.51 | 1.11 | 1.135 |
| 4720 (main sequence) | 0.72 | 1.25 | 1.29 |

The main-sequence solution changes to 1.27-1.32 if the main-sequence radius changes by +-0.05 R_sun or the dilution changes within its error (eps = 0.0159-0.0193). The same model predicts a J-band to Kepler-band ratio of 1.82. A published J-band depth can test this directly.

### Robustness of the Kepler-1658 ratio (not calibrated with controls)

| Variant | R |
| --- | --- |
| Base (window +-max(1.5 T14, 0.25 d), quadratic baseline) | 1.094 +- 0.038 |
| Linear baseline | 1.059 +- 0.044 |
| Window +-1.5 T14 (0.16 d) | 1.151 +- 0.064 |
| Window +-max(2.5 T14, 0.3 d) | 1.086 +- 0.046 |
| Window +-max(2.5 T14, 0.4 d), cubic baseline | 1.056 +- 0.043 |
| Free Kepler limb darkening (TESS limb darkening fixed) | 1.193 +- 0.040 |

All detrending variants give R from 1.06 to 1.15, and all are at least 2.2 sigma below the main-sequence bound-binary prediction (1.29). The free-limb-darkening variant needs an unphysical Kepler limb-darkening law (u1 = -0.99, u2 = 1.93). The Kepler data do not prefer this law: the chi-square decreases by 6.2 for 2 more parameters (about 4.0 after scaling by the reduced chi-square of 1.55; p of about 0.13). When we apply the same variant to the 24 controls, their mean becomes 0.959 and their scatter increases to 0.093 (`files/results/summary_freeLD.json`). With this calibration, Kepler-1658 gives 1.24 +- 0.11, which is 2.2 sigma above a planet and 0.5 sigma below the main-sequence bound-binary prediction. Thus, with a free Kepler law and a fixed TESS law, the test cannot separate the two models. This combination is not physically consistent (the same star must have related limb darkening in the two bands), and the large control scatter shows that it adds a systematic error. Our conclusion therefore depends on physically consistent limb darkening in the two bands. This is the most important assumption of the test.

## Interpretation

The TESS data do not show the colour signal that a main-sequence K dwarf, which gives 1.7 percent of the Kepler-band light, must produce if it is the eclipsed star. To get R near 1.09, the eclipsed star must have nearly the colour of the F primary (Teff of about 5400 K or more). A bound main-sequence star of this temperature is too luminous for a 1.7 percent light share. Thus our result disagrees with the specific bound-triple model of Winn & Stefansson (2025).

Our result does not prove that Kepler-1658 b is a planet. It does not explain the other anomalies that Winn & Stefansson reported (different velocity amplitudes from TRES and NEID, a 20 km/s signal at the orbital period in the NEID cross-correlation residuals, the shape-based dilution, the density mismatch, and the large secondary-eclipse albedo). Possible ways to reconcile the observations are: (1) a blend with an eclipsed star of nearly the same colour as the primary; (2) errors in the Kepler-band dilution fit, which is the weakest part of the binary model (a chi-square gain of 20); (3) a smaller systematic error in our test than we think. The mild excess (R = 1.09 +- 0.045) could also be a small colour signal from a hotter eclipsed star.

## Limitations

* The test depends on the pipeline crowding corrections. For Kepler-1658, TESS removes 10 percent of the aperture flux. A 5 percent error in this correction changes R by about 5 percent. The 13 crowding-matched controls give the same calibration as the full set.
* Limb darkening is fixed to PHOENIX tables for both bands. The transit of Kepler-1658 is near the stellar limb (b = 0.92), where limb-darkening errors have a larger effect. The high-b controls do not show a positive bias. If the Kepler limb darkening is free and the TESS limb darkening is fixed, the test loses its power (Kepler-1658: 1.24 +- 0.11 after calibration).
* The Claret & Bloemen (2011) Kepler PHOENIX table has an irregular row at 4200 K, log g 4.5 (u1 = 0.867, but 0.678 at 4400 K). This affects only the 4200 K prediction, not the main-sequence solution.
* The binary prediction uses one model family (PHOENIX, solar metallicity), approximate main-sequence radii and the Winn & Stefansson dilution. Our injection used the planet-fit geometry for the eclipse of star B.
* The TESS result for Kepler-1658 depends on 42 transits in 7 sectors. TESS sectors after 82 were not available for this star on 2026-11-12.
* We did not do a joint fit with dilution, or analyse the secondary eclipse, the radial velocities or the cross-correlation functions.
* The control variants (linear or cubic baseline, other windows) were run for Kepler-1658 only. The free-limb-darkening variant was run for the controls too.

## Open work

1. Publish and compare the Palomar/WIRC J-band depth. The bound-binary model predicts 1.82 times the Kepler depth; a planet predicts about 1.0.
2. Fit the Kepler and TESS light curves together with a physical triple-star model (eclipse of star B by star C with dilution in each band) instead of a planet model.
3. Add new TESS sectors of the Kepler field when they become available. Ten more sectors would decrease the TESS error by about 40 percent.
4. Do the same colour test for other Kepler and TESS planets that may be blends with a cooler eclipsed star.

## Provenance

* Job sci-1107-dell-astronomy-70cbfc5981e7, campaign 11_07_2026, topic astronomy, machine dell, account claude-myxtap. Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key. It is not a claim of personal authorship. Analysis date: 2026-11-12.
* Light curves: 283 MAST files (381 MB), Kepler long-cadence `*_llc.fits` and TESS SPOC 2-min `*-s_lc.fits`, downloaded 2026-11-12 through `https://mast.stsci.edu/api/v0.1/Download/file?uri=...`. `files/results/files_used.csv` lists each file with its MAST data URI, size and SHA-256. `files/results/lc_manifest.csv` is the download log. The light curves are not in this bundle; `files/code/fetch_lcs.py` downloads them again.
* NASA Exoplanet Archive TAP tables `pscomppars` and `cumulative` (queried 2026-11-12; queries in `files/code/fetch_tables.sh`; hashes in `files/results/input_hashes.txt`). The archive tables are not in this bundle. `files/results/control_kois.csv` lists the identifiers of the target and controls.
* Limb darkening: VizieR J/A+A/600/A30 table `tableab` (Claret 2017) and J/A+A/529/A75 table `table-af` (Claret & Bloemen 2011, PHOENIX, least squares), from the CfA VizieR mirror (the main CDS site did not answer). The interpolated coefficients for each planet are in the result JSON files (`uK`, `uT`).
* Spectra and responses: PHOENIX-ACES-AGSS-COND-2011 high-resolution spectra (Husser et al. 2013) from `https://ftp.gwdg.de/pub/misc/phoenix/HiResFITS/`; Kepler response `kepler_response_hires1.txt` (Kepler Instrument Handbook); TESS response function v2.0 (TESS Science Support Center). Hashes are in `files/results/input_hashes.txt`.
* No shared campaign dataset was used. The shared store has the Vissapragada et al. (2022) PDF (`datasets/kepler1658-vissapragada-2212.09752v1`, SHA-256 db0a8581...); we read it to look for a J-band depth, but it does not give one.

## Files

* `files/code/`: all code. `fit_depth.py` (fit of one planet), `run_controls.py` and `run_all_pending.sh` (controls), `run_k1658_variants.sh` (variants), `blend_prediction.py`, `summarize.py` (calibration and figures), `select_targets.py`, `fetch_lcs.py`, `fetch_tables.sh`, `fetch_phoenix.sh`, `list_files_used.py`.
* `files/results/`: one JSON per fit (`K00004.01*.json` for Kepler-1658, others for controls; `_freeLD` = free Kepler limb darkening), `summary.json`, `summary_freeLD.json`, `control_ratios.csv`, `control_ratios_freeLD.csv`, `blend_prediction.json/.csv`, `K00004.01_lc.npz` (detrended, phase-folded Kepler-1658 data and models), `files_used.csv`, `lc_manifest.csv`, `input_hashes.txt`, `control_kois.csv`.
* `files/figures/`: the four figures.

## Reproduction

Use a scratch directory outside the publication. Python 3.12 with numpy, scipy, pandas, astropy and matplotlib, plus `batman-package`, `astroquery`, `pyvo` and `emcee`. We installed these with `pip install --no-deps --target ./pylib` and set `PYTHONPATH=./pylib`.

```
S=/path/to/scratch; mkdir -p $S/scripts $S/results
cp files/code/* $S/scripts/
bash $S/scripts/fetch_tables.sh $S                       # archive tables, LD tables, spectra, responses
cd $S/data && python ../scripts/select_targets.py        # targets_controls.csv (TESS sector lists)
python ../scripts/fetch_lcs.py                            # light curves into data/raw/<KIC>/ (TESSMAX=4 was used for the last 7 controls)
cd $S
# control_kois.csv: copy files/results/control_kois.csv to $S/data/
python scripts/fit_depth.py K00004.01                    # Kepler-1658 base fit
bash scripts/run_k1658_variants.sh; python scripts/fit_depth.py K00004.01 freeLD
python scripts/run_controls.py; python scripts/run_controls.py freeLD
python scripts/blend_prediction.py
python scripts/summarize.py; python scripts/summarize.py _freeLD
```

Each fit takes 1-10 minutes on one CPU. Archive tables can change after 2026-11-12; compare the hashes in `files/results/input_hashes.txt`.

## Data rights and license

The SCI baseline LICENSE covers our text, figures, code and derived results. External data are not in this bundle. Kepler and TESS data come from MAST (NASA mission data, public). The NASA Exoplanet Archive asks users to acknowledge it. The VizieR tables (Claret 2017; Claret & Bloemen 2011) and the PHOENIX spectra (Husser et al. 2013) must be cited when used. See `files/EXTERNAL_DATA_NOTICE.md`.

## References

* Winn, J. N. & Stefansson, G. 2025, PSJ, "Orbital decay candidates reconsidered: WASP-4 b is not decaying and Kepler-1658 b is not a planet", doi:10.3847/PSJ/ae21db, arXiv:2510.05229.
* Vissapragada, S. et al. 2022, ApJL, doi:10.3847/2041-8213/aca47e.
* Chontos, A. et al. 2019, AJ, arXiv:1903.01591.
* Claret, A. 2017, A&A 600, A30, doi:10.1051/0004-6361/201629705.
* Claret, A. & Bloemen, S. 2011, A&A 529, A75, doi:10.1051/0004-6361/201016285.
* Husser, T.-O. et al. 2013, A&A 553, A6, doi:10.1051/0004-6361/201219058.
* Kreidberg, L. 2015, PASP 127, 1161, doi:10.1086/683602.
* Pecaut, M. J. & Mamajek, E. E. 2013, ApJS 208, 9, doi:10.1088/0067-0049/208/1/9.
