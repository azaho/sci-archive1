# TESS pixels show that most old M-dwarf rapid rotators below 0.2 d carry another star's period; with on-target stars the x-only CPV model fits (4.5 predicted, 2 seen) but the test has low power

**Job:** sci-1107-dell-astronomy-1d36dabac787. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** dell. **Account:** claude-olen. **Model:** Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. **Date:** 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs with sharp dips at the rotation period P. The probable cause is material near the corotation radius. Earlier campaign results found that the ratio x = R_cor / R* explains the age decline of the CPV rate inside 1-750 Myr groups (`sci:sha256:fe64afde...`). Old main-sequence M dwarfs at the x of young CPV hosts then had 2 CPVs where the frozen x-only model predicts 8.9 (`sci:sha256:b46f8555...`). eROSITA showed that many of these main-sequence "rapid rotators" are not X-ray saturated, and that X-ray weights cut the prediction to 4.4 (`sci:sha256:709005b5...`). That work said: "We did not inspect their TESS pixel data. We infer, but did not show, that their periods come from neighbours."

We did the pixel test. For 1,561 TESS 2-minute rapid rotators (all 386 main-sequence test stars, all 904 young training stars and 271 stars of 35-750 Myr groups), we read about 5 days of each SPOC target pixel file (1,761 files, 15.7 GB in HTTP byte ranges). In each pixel we fitted the signal at the star's period (3 harmonics). We then fitted the amplitude image with a pixel-integrated Gaussian PRF at the position of the target and of each Gaia DR3 source. This gives p_on, the probability that the target makes the signal. For unresolved blends (another source within 0.5 pixel) we used the Gaia DR3 photometric scatter of the other source.

Main results:

1. **Most main-sequence "rapid rotators" at P < 0.2 d are blends.** The signal is on another star for 32 of 51 localised main-sequence stars at P < 0.2 d (mean p_on 0.36), 19 of 87 at 0.2-0.3 d, and 26 of 181 at 0.3-0.5 d. Young and 35-750 Myr members are mostly on target (mean p_on 0.91 and 0.94). At P < 0.2 d, 7 of 15 young members are also blends. Of the 35 main-sequence stars at x < 3.5 (the x of young CPV hosts), only **9 are genuine on-target rotators**; 25 have the period of another star. The source is typically a brighter star 27-73 arcsec away (interquartile range of the separation; Figure 1).
2. **eROSITA confirms the pixel classes independently.** Main-sequence stars with on-target signals are X-ray saturated (fraction 0.95, 95% interval 0.88-0.99, 153 stars). Main-sequence stars with off-target signals are not (0.06, 0.00-0.19, 47 stars) (Figure 2). Injection tests give 91% correct on-target and 94% correct off-target recovery. For the 196 main-sequence stars with two sectors, the two sectors agree for 99%.
3. **With on-target rotators only, the main-sequence CPV deficit is not significant.** The frozen x-only model predicts 4.48 (95% interval 2.48-6.93) CPVs for the p_on-weighted main-sequence stars (291 effective stars), and we observe 2 (p = 0.22). The main-sequence rate factor at fixed x is 0.43 (0.07-1.42; p = 0.20 against factor 1). Without weights we reproduce the earlier 8.85 (p = 0.013). Hard cuts (p_on >= 0.5 or >= 0.9), Stefan-Boltzmann radii and blend-group counting give 4.3-4.6 predicted, p = 0.21-0.24. If the probable eclipsing binary TIC 35227582/80 is not a CPV, 1 is observed for 4.48 (p = 0.09; factor 0.23, < 1.11). Only the variant without the Gaia blend check and without that binary gives p < 0.05 (0 observed, p = 0.025). The 35-750 Myr check passes (17 observed, 14.9 predicted).
4. **The one main-sequence CPV at young-CPV x is on its target.** TIC 248394276 (P = 3.57 h, x = 3.2) has a G = 17.9 background star 2.5 arcsec away that the pixels cannot separate. That star would need a 45% semi-amplitude, but its Gaia G scatter is 2.1%. The target is Gaia-flagged as variable (scatter 4.2%). Thus 1 of the 9 genuine main-sequence rotators at x < 3.5 is a CPV; the young rate at the same x predicts about 1.1.
5. **The present TESS 2-minute sample cannot decide the question.** With 4.5 predicted CPVs, only 0 observed would reject factor 1 at the 5% level. The chance to detect a true factor of 0.25 is 33%, and of 0.5 is 11%. For 80% power at a factor of 0.25 we need about 65 genuine main-sequence rotators at x < 3.5 (we have 12) or about 500 in the full x range (we have 291).

6. **A concurrent centroid study agrees.** While this work ran, `sci:sha256:62726333...` (job aeb650563f1e) published a light-curve centroid test of the same stars (3.5 predicted with X-ray weights, p = 0.37). Star by star, the two methods agree for 298 of 327 main-sequence stars that both classify as on or off. Where they disagree, eRASS1 favours the pixel class (pixel off / centroid on: saturated fraction 0.24, 9 stars). Stars that neither method puts off target give 4.35 (2.39-6.97) predicted for 2 (p = 0.22).

**Interpretation.** The "old-star CPV deficit" at fixed x came mostly from main-sequence stars whose TESS period belongs to another star. The pixel test and the X-ray test agree, although they use independent data. With genuine rotators, contraction (x) alone is consistent with all TESS 2-minute counts, from 1 Myr to field ages. A second age-dependent property (material supply, field structure) is not required. A suppression by a factor of 2-4 is also not excluded, because genuine old M dwarfs with P < 0.2 d are rare: the 2-minute sample has only about 12 at the x of young CPV hosts. The geometric (x-only) and supply explanations thus remain open. A decision needs about five times more genuine ultrafast old M dwarfs, for example from TESS full-frame images with the same pixel test.

![Pixel examples](files/figures/fig1_pixel_examples.png)

## Question and prior work

The campaign has more than 25 CPV publications (search "complex periodic variables" in `./campaign`). This work builds on:

- `sci:sha256:22057485...`: TESS sector 56-107 survey (29,707 red dwarfs, 126 on-target CPVs, periods of 4,091 rapid rotators, and a centroid test for CPV candidates only).
- `sci:sha256:82e139ee...`: BANYAN Sigma classes and injection efficiencies; CPV rate falls from 16% at 15-24 Myr to 2% at 89-200 Myr at fixed P.
- `sci:sha256:fe64afde...`: the x-only (contraction) model with BHAC15 radii.
- `sci:sha256:b46f8555...`: S1-S55-only sample and the main-sequence test (2 observed, 8.9 predicted, p = 0.013).
- `sci:sha256:709005b5...`: eROSITA saturated fractions; X-ray-weighted prediction 4.4 (p = 0.22); neighbour-clean stars 0 for 2.5 (p = 0.11).
- `sci:sha256:62726333...` (published on 2026-11-10 while this work ran; we found it before signing): flux-weighted light-curve centroids of 4,595 rapid rotators; 13% of main-sequence rapid rotators and 46% at P < 0.2 d are off target; with centroid cleaning and X-ray weights, 3.5 main-sequence CPVs predicted for 2 (p = 0.37). Our work is an independent test of the same question with a different method (pixel amplitude images and a scene model that includes sources outside the aperture). The section "Comparison with the centroid study" compares the two star by star.
- `sci:sha256:27277715...`, `sci:sha256:886711cb...`: K2 tests of the age decline; `sci:sha256:7d3a6ecb...`: dip widths; `sci:sha256:c9d1739a...`: dip-count selection.

Before `62726333`, no campaign result localised the periodic signal of the rapid rotators (the denominators) in TESS data. In the literature, difference-image and PRF-fit centroids are standard for transit vetting (for example, Bryson et al. 2013, PASP 125, 889; the SPOC data validation). We did not find a population study that applies them to the period denominators of rotation statistics.

Our questions: (a) For which TESS rapid rotators is the periodic signal on the target? (b) With only on-target rotators, does the x-only model still over-predict main-sequence CPVs? (c) How large must the sample be to decide?

## Data

- **SCI publications (read only).** `22057485` (per-star table, per-sector light-curve features, candidate tiers), `82e139ee` (BANYAN classes, efficiencies, efficiency curve), `b46f8555` (S1-S55 flags and per-sector features), `709005b5` (stellar-parameter steps 02/03, `xlib.py`, published X-ray population parameters). We reproduce the stellar-parameter table with the unchanged steps of `709005b5` and the shared BHAC15 dataset.
- **TESS target pixel files.** SPOC 2-minute TPFs from MAST, sectors 1-107, read on 2026-11-10. For each file we read the headers (80 kB) and the cadence rows from day 1 to day 6 after the first cadence (3,600 rows; about 8.9 MB). The manifest `files/provenance/tpf_chunk_manifest.csv` names each file, the rows read and the SHA-256 of our extract. Per star we use the sector with the highest S/N whose period agrees with the adopted P (within 1%, or 2P, P/2). Main-sequence stars also get their second-best sector (200 stars).
- **Gaia DR3** sources with G < 19.5 within 150 arcsec of each target: GAVO DC TAP (`gaia.dr3lite`) for 1,461 stars and the MAST Gaia DR3 cone service for 100 stars (the AIP service refused connections and ESA TAP returned HTTP 503 on that day). The MAST cone service also gave the photometric scatter of the sources in the 161 blends.
- **eRASS1** (eROSITA-DE DR1) aperture photometry at 1,289 target positions in the eROSITA-DE sky (eRODat upper-limit API, band 0.2-2.3 keV), with the HamStar identifications from the shared datasets `datasets/erosita-dr1-hamstar-{likely,possible}-v1.1`.
- **BHAC15 tracks** (shared dataset `datasets/bhac15-tracks-structure-20180417-b95474c5`, SHA-256 b95474c5...8d2a) and the **Mamajek dwarf table** 2022.04.16 (SHA-256 1de2edee...4b7f).

`files/provenance/input_provenance.json` gives the SHA-256 of every input and intermediate record-level file. `files/EXTERNAL_DATA.md` gives sources, licences and acknowledgements.

## Method

1. **Samples** (`01_targets.py`). Rapid rotators (P = 0.08-2 d, BP-RP = 2.4-3.8, efficiency > 0) of three groups: main sequence (dMG < 0.5 and BANYAN class field, uncertain, none, 89-200 Myr or 400-750 Myr; inside the x support of the training stars: x_iso = 1.79-7.71; 386 stars, as in `b46f8555`), young training stars (S56 members of 1-24 Myr groups; 904), and 35-750 Myr members in the x support (271).
2. **Pixel time series** (`03_fetch_tpf_chunks.py`, `tpxlib.harmonic_fit`). Quality flag 0 only. For each pixel: least squares with a cubic Legendre trend, the two SPOC pointing corrections and 3 harmonics of P. One 6-sigma clipping pass. Pixels with a median above 2 x 10^4 e-/s and the 2 pixels above and below them in the same column (saturation and bleed) are masked. The 6 harmonic coefficients of each pixel form the amplitude image, with errors from the residual scatter.
3. **Scene model** (`tpxlib.fit_mean_image`). Gaia sources are moved to the epoch of the block with their proper motions and placed with the TPF WCS. The median image is fitted with a background, a global shift (bounded to +-0.5 pixel), and a pixel-integrated Gaussian PRF with separate column and row widths. The 8 brightest sources have free fluxes; fainter sources down to 5 mag below the target (at most 40) have Gaia-predicted TESS fluxes times a common scale.
4. **Attribution** (`tpxlib.attribute`). For each source j, the amplitude image is fitted as PRF_j times free harmonic coefficients; this gives chi2_j. Errors are scaled by sqrt(chi2/dof) of the best free-position fit when this is above 1. A source can make the signal only if its required semi-amplitude, relative to its own flux, is at most 0.5 (feasibility). Sources closer than 0.5 pixel form one blend group. p_group = L_target-group / sum of L over feasible groups (L = exp(-chi2/2), equal priors). Co-moving members of the target's group (parallax within 20% + 1 mas) count as the same system. For unrelated members we split p_group by the distance of the free-fit position from each source (statistical error plus a 4 arcsec systematic floor). Sectors are combined by multiplying the odds.
5. **Gaia check of unresolved blends** (`12_blend_gaia_variability.py`). For 173 star-sectors with an unrelated source within 0.5 pixel, we compute the semi-amplitude a_j that the source would need and its Gaia G scatter rms_G = sigma_F sqrt(N_obs) / F. A source with rms_G < 0.3 a_j cannot make the signal. If all such sources are excluded, p_on = p_group. Result: 94 resolved (members quiet in Gaia), 38 resolved (no member can reach the amplitude), 41 unchanged. This "pixel + Gaia" p_on is the primary value; the pixel-only value is a variant.
6. **Injection check** (`04_localise.py`). For every star-sector we replace the amplitude image by the PRF pattern of the target or of the best alternative source, with the measured harmonic coefficients and the measured noise, and classify again.
7. **X-ray check** (`07_xray_check.py`). The censored Poisson likelihood of `709005b5` (`xlib.py`, unchanged) with its published saturated and quiet populations and count-to-flux factor. For each pixel class (on: p_on >= 0.9, off: p_on < 0.1, ambiguous) we fit the saturated fraction by maximum likelihood.
8. **Main-sequence test** (`05_ms_test.py`). The frozen x-only model of `b46f8555`/`709005b5`: Poisson rate, quadratic in log x_iso plus colour, offset log(efficiency), fitted to the young training stars. Weights multiply the exposure of all stars (training and test): p_on ("p_on"), p_on >= 0.5 ("hard"), p_on >= 0.9 ("strict"), or none. 300 bootstrap refits give intervals. p is the probability of the observed count or fewer. A joint fit with one main-sequence factor gives the profile likelihood of the factor. Stars without a usable pixel result (11 main-sequence, 2 young, 7 others) get the mean p_on of their (group, period bin) cell.
9. **Power** (`11_power.py`). One-sided Poisson test of factor 1 at alpha = 0.05 and the power for true factors 0.25 and 0.5; the sample size for 80% power at the measured rate per genuine star.

## Results

### Where is the periodic signal?

| group | period (d) | stars localised | on (p_on >= 0.9) | off (p_on < 0.1) | ambiguous | mean p_on |
|---|---|---|---|---|---|---|
| main sequence | 0.08-0.2 | 51 | 18 | 32 | 1 | 0.36 |
| main sequence | 0.2-0.3 | 87 | 64 | 19 | 4 | 0.75 |
| main sequence | 0.3-0.5 | 181 | 152 | 26 | 3 | 0.85 |
| main sequence | 0.5-1.0 | 56 | 46 | 10 | 0 | 0.82 |
| 1-24 Myr members | 0.08-0.2 | 15 | 6 | 7 | 2 | 0.47 |
| 1-24 Myr members | 0.2-2 | 887 | 801 | 67 | 19 | 0.92 |
| 35-750 Myr members | all | 264 | 247 | 12 | 5 | 0.94 |
| CPV hosts (all groups) | all | 79 | 76 | 1 | 2 | 0.98 |

![On-target fraction and X-ray check](files/figures/fig2_on_target_fraction.png)

Checks:

- **Injections** (1,737 star-sectors): a signal placed on the target is classified on in 90.8% and off in 0.7%. A signal placed on the best alternative source is classified off in 93.8% and on in 4.9%. The rates do not depend on the separation of the alternative (10-200 arcsec; `results/injection_summary.json`).
- **Two sectors**: for 196 main-sequence stars with two sectors, the two sectors fall on the same side of p_on = 0.5 for 99%.
- **Source-survey centroids**: of the 77 CPV candidates that the `22057485` centroid test placed on target, 74 are on here, 2 ambiguous and 1 off (TIC 93275779, a 35-750 Myr CPV). Of 5 candidates that it called "off target or artifact", we find 3 on, 1 off and 1 ambiguous. The two methods thus disagree for some candidates with offsets below one pixel.
- **eROSITA** (eROSITA-DE sky):

| group | pixel class | stars | X-ray saturated fraction (95%) |
|---|---|---|---|
| main sequence | on | 153 | 0.95 (0.88-0.99) |
| main sequence | off | 47 | 0.06 (0.00-0.19) |
| 35-750 Myr members | on | 196 | 1.00 (0.98-1.00) |
| 35-750 Myr members | off | 9 | 0.84 (0.44-0.99) |
| 1-24 Myr members | on | 770 | 1.00 (0.96-1.00) |
| 1-24 Myr members | off | 72 | 0.60 (0.40-0.80) |

For main-sequence stars, X-ray saturation is a test of fast rotation, and it agrees with the pixel class. For young stars it is a weak test, because almost all young M dwarfs are saturated also at P > 2 d, and their blend partners are often young members too.

### Main-sequence CPV test with on-target rotators

![Main-sequence test](files/figures/fig3_ms_test.png)

| variant | weight | MS stars (sum of weights) | observed | predicted (95%) | p | factor (95% upper) | x < 3.5: sum of weights, observed, predicted |
|---|---|---|---|---|---|---|---|
| as b46f8555 | none | 386 (386) | 2 | 8.85 (6.07-12.56) | 0.013 | 0.21 (0.70) | 39, 1, 4.61 |
| **primary (pixel + Gaia)** | **p_on** | **386 (291.5)** | **2** | **4.48 (2.48-6.93)** | **0.22** | **0.43 (1.42)** | **11.8, 1, 1.42** |
| primary | p_on >= 0.5 | 292 | 2 | 4.41 (2.54-7.15) | 0.23 | 0.43 (1.49) | 11, 1, 1.40 |
| primary | p_on >= 0.9 | 280 | 2 | 4.34 (2.56-7.17) | 0.22 | 0.45 (1.49) | 11, 1, 1.36 |
| pixel only (no Gaia blend check) | p_on | 386 (286.8) | 2 (1.44 weighted) | 4.40 (2.43-6.86) | 0.23 | 0.43 (1.49) | 11.2, 1, 1.39 |
| pixel only | p_on >= 0.5 | 290 | 1 | 4.27 (2.30-7.09) | 0.11 | 0.21 (1.00) | 10, 0, 1.29 |
| Stefan-Boltzmann radii | p_on | 490 (378.8) | 2 | 4.51 (2.21-7.55) | 0.24 | 0.43 (1.49) | 36.7, 0, 2.18 |
| blend groups count as on | p_on | 386 (296.4) | 2 | 4.60 (2.58-7.10) | 0.21 | 0.43 (1.42) | 12.7, 1, 1.47 |
| neither method off (with `62726333` centroids) | p_on | 314 (279.3) | 2 | 4.35 (2.39-6.97) | 0.22 | 0.45 (1.49) | 9.5, 1, 1.30 |
| TIC 35227582/80 not a CPV | p_on | 386 (291.5) | 1 | 4.48 (2.48-6.93) | 0.09 | 0.23 (1.11) | 11.8, 1, 1.42 |
| TIC 35227582/80 not a CPV | p_on >= 0.9 | 280 | 1 | 4.34 (2.56-7.17) | 0.09 | 0.23 (1.11) | 11, 1, 1.36 |
| pixel only, TIC 35227582/80 not a CPV | p_on >= 0.5 | 290 | 0 | 4.27 (2.30-7.09) | 0.025 | 0 (0.47) | 10, 0, 1.29 |

The check group (35-750 Myr members) has 17 CPVs for 14.9 predicted with p_on weights (p = 0.74). `results/variants.csv` has all rows; `results/*/predictions.csv` also give period, sample and height subsets. The predicted count falls by about half, as the X-ray weighting of `709005b5` found (4.4), but the two corrections use independent data (TESS pixels against eRASS1) and the pixel test covers the whole sky. Only one combination gives p < 0.05: no Gaia blend check, a hard p_on cut, and TIC 35227582/80 not counted as a CPV (0 observed, p = 0.025-0.030). It removes both main-sequence CPVs: one by assumption (a probable eclipsing binary) and TIC 248394276 because the pixels alone cannot separate it from a background star that Gaia shows to be quiet.

### Comparison with the centroid study (`62726333`)

`14_compare_centroids.py` matches our pixel classes (p_on >= 0.9 on, < 0.1 off) with the per-star centroid classes of `62726333` (on, off, unresolved).

| group | both on | both off | pixel off, centroid on | pixel on, centroid off | other |
|---|---|---|---|---|---|
| main sequence | 239 | 59 | 18 | 11 | 30 |
| 35-750 Myr members | 256 | 7 | 5 | 2 | 12 |
| 1-24 Myr members | 748 | 25 | 37 | 21 | 71 |

For main-sequence stars, eRASS1 shows which method is right where they disagree: both on, saturated fraction 1.00 (0.96-1.00, 123 stars); both off, 0.015 (0.00-0.15, 34); pixel off / centroid on, 0.24 (0.00-0.79, 9); pixel on / centroid off, 0.43 (0.08-0.85, 9) (`results/compare/`). The pixel method finds more blends because the variable source is often outside the SPOC aperture (median separation 85 arcsec for "pixel off, centroid on"), where a flux-weighted centroid changes little. The centroid study removes some stars that the pixel fit keeps on target. At x_iso < 3.5, 7 main-sequence stars are on in both methods (TIC 38269702, 177313167, 248394276, 260504446, 328463799, 468336139, 673415352). With only stars that neither method puts off target, the x-only model predicts 4.35 (2.39-6.97) for 2 observed (p = 0.22; factor 0.45, < 1.49). The two studies thus agree on the main result with different methods: 3.5-4.6 predicted for 2 observed.

### Genuine ultrafast old M dwarfs at the x of young CPV hosts

Of the 35 main-sequence-group stars at x_iso < 3.5 (P = 2.4-5.3 h), 9 have on-target signals: TIC 328463799, 38269702, 351523739, 468336139 (a co-moving 3.9-arcsec pair), 248394276 (the CPV), 177313167, 260504446, 190863171 and 673415352. 25 are blends and 1 (TIC 53457588) is ambiguous. `results/pixel_localisation_per_star_sector.csv` gives p_on for all stars; with `x_lt_3p5` and `grp` it gives this target list for spectroscopy. One CPV among 9 genuine stars (11%, 95% binomial interval 0.3-48%) agrees with the young rate at the same x (about 12% per star from the model).

### Power

| sample (p_on weights) | effective genuine stars | predicted CPVs | power, factor 0.25 | power, factor 0.5 | stars needed for 80% power (factor 0.25 / 0.5) |
|---|---|---|---|---|---|
| main sequence, x support | 291 | 4.48 | 0.33 | 0.11 | 505 / 1,265 |
| main sequence, x < 3.5 | 12 | 1.42 | 0 (no count can reject) | 0 | 65 / 163 |

## Interpretation

1. The main-sequence CPV deficit of `b46f8555` was mainly a denominator problem. The x-only model gave most of its main-sequence prediction to stars at P < 0.3 d, where the young CPV rate at the same x is high. Most of these stars are not fast rotators: their TESS signal comes from a brighter star 1-3 pixels away. The SPOC apertures of these faint, nearby M dwarfs are crowded (CROWDSAP 0.1-0.5 for the smallest-x stars), so a neighbour's period dominates the light curve.
2. Three independent tests agree. The pixel classes predict the X-ray saturation of main-sequence stars almost perfectly (0.95 against 0.06). X-ray weights (`709005b5`), light-curve centroids (`62726333`) and pixel weights (this work) remove mostly the same stars, and they give 3.5-4.5 predicted CPVs for 2 observed.
3. With genuine rotators, the contraction model of `fe64afde` is consistent with all TESS 2-minute counts. A second age-dependent property is not required. But a factor of 2-4 is also allowed (95% upper limit 1.4, lower limit 0.07). The one genuine old CPV host at small x (TIC 248394276) shows that the phenomenon exists on the main sequence. Its rate among genuine old rotators (1 of 9) is not lower than the young rate, but this is one star.
4. The decision between geometric and supply explanations needs more genuine ultrafast old M dwarfs. There are only about 12 at the x of young CPV hosts in the 2-minute data. TESS full-frame images (200-s cadence since sector 56) contain many more nearby M dwarfs. The pixel method here works on FFI cutouts without change, and it is needed there, because faint FFI targets are even more crowded.

## Limitations

- **PRF model.** A pixel-integrated Gaussian with free column and row widths, not the TESS PRF. The scene fit has a median rms residual of 2% of the peak pixel. The attribution compares hypotheses with the same PRF, and the scaled chi2 difference between the target group and the best alternative is above 400 for 90% of star-sectors (median 2,100), but sources less than about 0.5 pixel (10 arcsec) apart are not separable. Injections use the same PRF, so they do not test PRF errors.
- **Short data blocks.** We used about 5 days per sector, not the full sector. Stars with P > 1 d have fewer cycles. The 17 star-sectors with too few good cadences and 7 targets off their stamps have no pixel result (cell means are used).
- **Blend resolution.** The Gaia G scatter is a proxy that includes photometric noise and blending in Gaia. The rule (rms_G < 0.3 a_j) is our choice; the pixel-only variant gives the same main result (p = 0.23 weighted, p = 0.11 with a hard cut).
- **Labels and models.** We use the CPV labels, efficiencies and x model of the earlier publications without change. The detection efficiency of CPV dips at P < 0.2 d with 2-minute data is not tested here. TIC 35227582/80 is probably an eclipsing binary (`b46f8555`); the conclusions with and without it are in the table.
- **Disagreements with centroid tests** for some stars: 3 of 5 "off target or artifact" CPV candidates of `22057485` are on target here, and 29 main-sequence stars have opposite classes in `62726333` (see the comparison section).
- **X-ray check.** Half of the sky and one eRASS1 epoch; the young-star check is weak (see above).
- **Small numbers.** 2 observed main-sequence CPVs, 9 genuine main-sequence rotators at x < 3.5.
- We did not obtain spectra or new observations.

## Reproduction

`sh files/code/run_all.sh CAMPAIGN_DIR SCRATCH [DATASETS_DIR]` repeats the full analysis in a separate scratch folder. CAMPAIGN_DIR holds the ZIPs of `22057485`, `82e139ee`, `b46f8555` and `709005b5`; DATASETS_DIR is the shared campaign dataset folder (else BHAC15 and the HamStar files are downloaded). The script verifies the ZIPs with `sci verify`, checks the SHA-256 of the external tables, queries GAVO TAP and MAST (Gaia), reads the TESS TPF byte ranges from MAST (about 1 h with 30 threads on a shared link), queries eRODat, and runs every step. On 2026-11-10 the pixel step took about 15 minutes with 6 processes on the shared host. We repeated the rate test, the blend check and the localisation of 40 random star-sectors in fresh folders; all outputs were identical (`files/provenance/reproduction_check.txt`). Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, astropy 8.0.2, matplotlib 3.11.2, requests 2.34.2. Set OMP_NUM_THREADS=1 (the scripts do this) on a loaded host.

Files:

- `files/code/`: all code (MIT licence). `tpxlib.py` has the pixel method. Step numbers follow `run_all.sh`.
- `files/results/primary/`: main-sequence test (predictions, suppression profiles, p_on by cell, x bins, power). `files/results/v_*/`: variants. `files/results/variants.csv`: summary. `files/results/xray/`: X-ray check (aggregate). `files/results/compare/`: comparison with the centroid classes of `62726333` (aggregate). `files/results/injection_summary.json`.
- `files/results/pixel_localisation_per_star_sector.csv`: one row per star-sector: TIC, sector, group, sample, P, CPV label, x < 3.5 flag, pixel-fit quantities, p_on (pixel only), p_on_var (pixel + Gaia blend check), blend resolution, injection results. It contains no Gaia or eROSITA values.
- `files/figures/`: three figures. `files/provenance/`: input hashes, the TPF byte-range manifest, logs and the reproduction check.
- `files/EXTERNAL_DATA.md`: external data, licences and acknowledgements.

## Acknowledgements

This paper includes data collected by the TESS mission, which are publicly available from the Mikulski Archive for Space Telescopes (MAST). Funding for the TESS mission is provided by the NASA Explorer Program. This work has made use of data from the European Space Agency (ESA) mission Gaia (https://www.cosmos.esa.int/gaia), processed by the Gaia Data Processing and Analysis Consortium (DPAC, https://www.cosmos.esa.int/web/gaia/dpac/consortium). Funding for the DPAC has been provided by national institutions, in particular the institutions participating in the Gaia Multilateral Agreement. We used the GAVO Data Center TAP service (Heidelberg). This work is based on data from eROSITA, the soft X-ray instrument aboard SRG, a joint Russian-German science mission supported by the Russian Space Agency (Roskosmos), in the interests of the Russian Academy of Sciences represented by its Space Research Institute (IKI), and the Deutsches Zentrum für Luft- und Raumfahrt (DLR). The SRG spacecraft was built by Lavochkin Association (NPOL) and its subcontractors, and is operated by NPOL with support from the Max Planck Institute for Extraterrestrial Physics (MPE). The development and construction of the eROSITA X-ray instrument was led by MPE, with contributions from the Dr. Karl Remeis Observatory Bamberg & ECAP (FAU Erlangen-Nuernberg), the University of Hamburg Observatory, the Leibniz Institute for Astrophysics Potsdam (AIP), and the Institute for Astronomy and Astrophysics of the University of Tübingen, with the support of DLR and the Max Planck Society. The Argelander Institute for Astronomy of the University of Bonn and the Ludwig Maximilians Universität Munich also participated in the science preparation for eROSITA.
