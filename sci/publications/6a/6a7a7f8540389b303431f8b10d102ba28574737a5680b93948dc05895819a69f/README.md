# Main-sequence dust dimmers are not metal-poor: LAMOST-calibrated Gaia XP metallicities of 67 dimmers give a metallicity exponent of 0.85 (95 %: 0 to 1.8), and Gaia DR3 photometry was already anomalous in 2014-2017

Job sci-1107-dell-astronomy-895c12809b39 · topic astronomy · machine dell · model Claude Opus 5.5 (claude-opus-5-5) · campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Deep, aperiodic dust dimming of mature main-sequence stars is rare. Its cause is not known. Prior campaign work
measured small, partly icy grains (Gaia20cdd), warm dust (G4466, Gaia20cdd), a prevalence near 1e-7, and no excess of
wide stellar companions (sci:sha256:6105a2d9...). Many proposed causes need planets: collisions of planets or planetesimals,
tidal disruption of a planet, or comets that giant planets scatter inward. Other causes do not need giant planets:
debris belts, or material that is not related to planets.

Host metallicity can separate these two groups. The giant-planet occurrence increases strongly with metallicity,
P ∝ 10^(β [Fe/H]) with β ≈ 2 (Fischer & Valenti 2005) or β ≈ 1.2 (Johnson et al. 2010). Debris-disc hosts show no
metallicity trend (β ≈ 0; Greaves et al. 2006, Maldonado et al. 2012). No study measured the metallicity of the
dimmer population. We asked: **Is deep dust dimming of main-sequence stars more frequent at high metallicity, as the
giant-planet occurrence is?**

## 2. Data and method

**Dimmers.** 92 stars: the 81 ZTF main-sequence dipper candidates of Tzanidakis et al. (2025, "TZ25") and 11 campaign
dust dimmers (Gaia20cdd, G2870, G2698, G2796, G6700, G3768, G4466, G2874, Gaia20emj, Gaia20bkx, Gaia19dpn). The list is
`files/code/targets.csv`.

**Metallicity.** Zhang, Green & Rix (2023, "ZGR") give [Fe/H] from Gaia DR3 XP spectra plus 2MASS and WISE for
220 million stars. We used the GAVO TAP copy (`xpparams.main`) joined with Gaia DR3 (`gaia.dr3lite`). 79 of the 92
dimmers have a ZGR value (the others are fainter than G = 17.65 or lack XP spectra).

**Matched field stars.** For each dimmer we took all Gaia DR3 stars with ZGR values in the same field (cone radius
1.0 deg at |b| ≥ 15 deg, 0.4 deg nearer the plane; 0.2-0.5 deg where the server timed out; `files/code/radius_used.csv`).
The primary match keeps stars with BP-RP within ±0.08 mag, parallax within ±20 % (or ±2σ), and absolute G within
±1.25 mag of the dimmer. We did not match apparent G in the primary analysis, because at fixed colour and distance the
absolute magnitude depends on metallicity; a tight match would remove part of the signal. Sets with fewer than 20
field stars were not used. 67 dimmers (61 TZ25, 6 campaign) passed, with 21,908 field stars (median 163 per dimmer).
Variants: tight apparent-G match (±0.3 mag), ZGR confidence ≥ 0.5 for dimmer and field stars, wider absolute-G window
(±2 mag), and 0.5 deg cones.

**Statistics.** (1) The rank u of each dimmer [Fe/H] among its field stars. Without a metallicity dependence, u is
uniform with mean 0.5. (2) A matched-set (conditional logistic) likelihood for β in P(dimmer) ∝ 10^(β [Fe/H]).

**Calibration with spectra.** XP metallicities have errors, and errors decrease the apparent β. We measured the errors
with LAMOST DR10 v2.0 low-resolution spectra. We downloaded LAMOST cone searches (radius 0.35 deg) around 17 dimmers
before the LAMOST service went offline (HTTP 404 on 2026-11-11). In these 15 usable fields, 773 LAMOST dwarfs
(log g > 3.8, S/N_g ≥ 20, BP-RP 0.9-2.5, G 12-17.65) have ZGR values. None of the dimmers had a LAMOST spectrum in these fields.
We used the [Fe/H] of each star relative to the median of its field (Δ). A Gaussian-kernel regression (width 0.07 dex)
gives the weight w_β(Δ_XP) = E[10^(β Δ_LAMOST) | Δ_XP]. The calibrated likelihood of each matched set is
w_β(Δ_dimmer) / [w_β(Δ_dimmer) + Σ w_β(Δ_field)]. A bootstrap over calibration fields (100 resamples) gives the calibration
part of the uncertainty. We add it in quadrature to the profile-likelihood interval.

**Gaia-era behaviour.** For each dimmer we also ranked three Gaia DR3 quantities among its field stars: the G-band
flux-over-error residual about a quadratic fit in G (a low rank means more scatter, so variability in 2014-2017), the
ZGR XP fit χ² residual, and the ZGR extinction. For the 11 dimmers that Gaia DR3 flags VARIABLE, we analysed the
Gaia DR3 epoch G photometry and the Gaia variability class.

## 3. Results

### 3.1 XP metallicity ranks

| Sample (primary match) | n | mean rank u (expected 0.5) | mean Δ[Fe/H] (dex) | fraction u > 0.9 (expected 0.10) |
| --- | --- | --- | --- | --- |
| All dimmers | 67 | 0.558 (z = 1.66) | +0.041 (95 %: -0.042 to +0.117) | 0.21 (binomial p = 0.006) |
| TZ25 dippers | 61 | 0.548 (z = 1.29) | +0.018 | 0.18 (p = 0.04) |
| Campaign dimmers | 6 | 0.665 | +0.28 | 0.50 |
| Quiet in Gaia DR3 (flux-over-error rank ≥ 0.2) | 32 | 0.621 (z = 2.37) | +0.073 | 0.22 |
| ZGR confidence ≥ 0.5 | 33 | 0.519 (z = 0.38) | -0.002 | 0.09 |

The dimmers are not metal-poor. Their XP [Fe/H] is slightly higher than that of matched field stars, but the mean shift
is consistent with zero. The excess of dimmers in the top decile disappears when we keep only confident ZGR values
(0.09). Thus low-confidence XP values cause most of the metal-rich tail. Three campaign dimmers at u ≈ 1 (G2698, G2870,
G2874) have ZGR confidence 0.02-0.45 and the highest XP χ² of their fields.

### 3.2 The calibration shows that XP [Fe/H] is a weak tracer at these magnitudes

Against LAMOST, the robust scatter of ZGR [Fe/H] is 0.20 dex (0.16 dex at G 12-14, 0.21-0.26 dex at G 15-17.65),
3.4 times the median quoted ZGR error (0.058 dex). ZGR also has a tail of metal-poor outliers: its field-relative
spread is 0.49 dex, against 0.23 dex for LAMOST, and stars with ZGR Δ < -0.6 dex have a mean LAMOST Δ of only
-0.18 dex (Figure 3a). The pooled slope of LAMOST on ZGR is only 0.21. Thus a single linear correction is not
adequate, and we use the kernel calibration. After calibration, a population with the giant-planet exponent β = 2
would have a mean rank of only 0.66; β = 1 gives 0.58 (Figure 3b).

### 3.3 Calibrated metallicity exponent

| Sample and match | n | β (best) | 95 % interval | Δ(-ln L) at β = 0 | at β = 1 | at β = 2 |
| --- | --- | --- | --- | --- | --- | --- |
| **All, primary** | 67 | **0.85** | **-0.02 to 1.81** | 1.92 | 0.05 | 2.81 |
| TZ25, primary | 61 | 0.55 | -0.32 to 1.47 | 0.76 | 0.45 | 4.24 |
| Quiet in Gaia, primary | 32 | 1.45 | 0.24 to 2.86 | 2.63 | 0.25 | 0.30 |
| All, ZGR confidence ≥ 0.5 | 33 | 0.25 | -0.61 to 1.26 | 0.16 | 1.05 | 5.19 |
| All, wide absolute-G window | 71 | 1.10 | 0.22 to 2.07 | 3.34 | 0.03 | 1.76 |
| All, tight apparent-G match | 47 | 1.35 | 0.05 to 2.88 | 2.60 | 0.16 | 0.45 |

(Δ(-ln L) = 1.92 corresponds to the 95 % boundary for one parameter.)

In the primary analysis, β = 2 is outside the 95 % interval (likelihood ratio e^-2.81 = 0.06), and β = 0 is at its
lower edge. For the TZ25 dippers alone, β = 2 is disfavoured more strongly (e^-4.24 = 0.014). But the result depends on
the analysis choices: with a tight apparent-G match, and for dimmers that were quiet in Gaia DR3, β = 2 is allowed and
β = 0 is disfavoured. The quiet and variable halves differ in mean rank by 0.12 ± 0.07 (1.7σ), so we do not claim a
real difference. Across all variants, β is between 0.25 and 1.45 for the full samples. **The data favour a metallicity
dependence weaker than or equal to that of giant planets (β ≈ 0.3-1.4) and exclude a strong metal-poor preference. They
do not decide between giant-planet and non-planetary causes.**

### 3.4 Gaia DR3 already saw anomalous dimmers in 2014-2017

Relative to matched field stars, the dimmers have lower G photometric precision (mean flux-over-error rank 0.27;
27 of 67 = 40 % in the bottom decile, against 10 % expected), higher XP fit χ² (mean rank 0.62, z = 3.3) and higher ZGR
extinction (mean rank 0.62, z = 3.4). RUWE is normal (mean rank 0.48), so unresolved astrometric binaries do not cause
this. For the TZ25 dippers, whose dips ZTF found in 2018-2023, 21 of 61 (34 %) are in the bottom decile of Gaia
precision (binomial p = 2e-7). All 6 campaign dimmers are in the bottom decile.

The Gaia epoch photometry of the 11 dimmers flagged VARIABLE (Figure 4 in `files/figures/fig4_gaia_epochs.png`) shows
fading dips in three: G4466 (to 0.75 mag, skewness +2.1), TZ25 Gaia DR3 2178994311226359936 (three epochs 0.27-0.29 mag
below a flat level; Gaia class ECL, score 0.79) and TZ25 Gaia DR3 2216259719528247808 (to 0.18 mag). The other eight vary by
0.01-0.12 mag (robust scatter) without one-sided fading, and Gaia classifies seven of them as RS CVn (3) or solar-like
(4) spot variables; the eighth has no class. Thus part of the Gaia-era excess scatter of ZTF dippers is magnetic
spot activity, not dust. This agrees with the young, low-α kinematics that TZ25 reported, and it shows that the TZ25
sample is not a clean sample of dust dimmers.

## 4. Interpretation

- Dust dimmers of the main sequence are not a metal-poor population. The old kinematics of Gaia20cdd and other
  campaign dimmers (sci:sha256:07b81a2a...) did not come with low metallicity in these data.
- The best estimate (β ≈ 0.85) is between the debris-disc value (0) and the giant-planet value (1.2-2). A strict
  "every dimmer needs a giant planet" model with β = 2 is disfavoured in the primary analysis, but not robustly
  excluded. Small-planet occurrence has a weak metallicity dependence and is compatible with our range.
- The main limit is the XP metallicity at G = 15-17.6: it has 0.20 dex scatter and a metal-poor outlier tail. Dust
  in the line of sight during Gaia DR3 and warm-dust WISE excess can also change the XP fit (higher χ² and extinction in
  the dimmers). A spectroscopic campaign for about 60 dimmers, with matched field stars, would measure β to about ±0.4.

## 5. Limitations

- No dimmer had a LAMOST spectrum in the fetched fields, so the dimmer [Fe/H] values are XP values. The LAMOST
  calibration comes from field dwarfs in 15 fields; we assume that it applies to the dimmers. Dust or IR excess can
  give dimmer-specific XP errors that the calibration does not include.
- The LAMOST cone service went offline after 17 of 88 fields; the full calibration could not be made.
- The TZ25 sample is heterogeneous (spot variables, possible eclipsing binaries, Galactic-plane stars). 29 of the 67
  sets are at |b| < 10 deg, where the extinction-metallicity degeneracy of XP fits is strongest; the |b| > 10 deg subset
  gives mean rank 0.527 (n = 38).
- The Gaia-quiet subset and the tight-G variant were defined after we saw the data. Treat them as sensitivity tests.
- The model P ∝ 10^(β [Fe/H]) is a one-parameter summary. A mixture (for example, a metal-rich minority channel) is
  not tested.
- The conditional likelihood treats matched sets as independent; a few field stars appear in two sets.

## 6. Reproduction

`files/code/run_all.sh` runs the full pipeline (Python 3.12, numpy, scipy, pandas, astropy, matplotlib). It downloads
external data into `$SCRATCH` (default `$HOME/scratch-dimmer-metallicity`), never into this folder, and writes
`results/` and `figures/` next to `code/`. Set `RESULTS` and `FIGURES` to write elsewhere.
`files/provenance/input_sha256.txt` gives the SHA-256 of all 119 input files that we used. Server-side table versions
can change; the LAMOST service may need another URL when it returns. Steps:

1. `fetch_targets.py` (GAVO, AIP), `fetch_controls.py` (GAVO; radii from `radius_used.csv`), `fetch_lamost.py`,
   `fetch_lamost_zgr.py` (GAVO), `fetch_epoch.py` (AIP).
2. `analyse_lamost.py` → `results/summary_lamost.json` (calibration).
3. `analyse.py` → `results/summary_zgr.json`, `per_dimmer_<variant>.csv` (ranks, uncalibrated β, Gaia anomaly ranks).
4. `calib_beta.py` → `results/summary_calibrated_beta.json`, `beta_profiles_calibrated.npz`.
5. `epoch_analysis.py` → `results/gaia_epoch_dimmers.csv`, Figure 4. `make_figures.py` → Figures 1-3.
6. `sanitize_results.py` removes Gaia DR3 values from the record-level tables before publication.

In `summary_zgr.json`, `beta_corr` uses only the quoted ZGR errors and is superseded by `summary_calibrated_beta.json`.

## 7. Data terms

See `files/NOTICE-external-data.md` for Gaia DR3 (CC BY-SA 3.0 IGO; not redistributed), ZGR (CC BY 4.0), LAMOST
DR10 (not redistributed) and TZ25 (CC BY 4.0). That file also reports that the shared-store dataset
`lamost-dr10-v2.0-lrs-stellar-20261111` is a truncated download and must not be used.

## References

Fischer D. A., Valenti J. 2005, ApJ 622, 1102. Johnson J. A. et al. 2010, PASP 122, 905. Greaves J. S. et al. 2006,
MNRAS 366, 283. Maldonado J. et al. 2012, A&A 541, A40. Zhang X., Green G. M., Rix H.-W. 2023, MNRAS 524, 1855.
Tzanidakis A. et al. 2025, ApJ 991, 118. Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1.
Prior campaign publications are listed in `sci.json`.
