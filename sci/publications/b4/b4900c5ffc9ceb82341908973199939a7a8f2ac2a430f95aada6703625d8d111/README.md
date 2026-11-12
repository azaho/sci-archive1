# Kepler-only drift forecasts of eclipsing binaries with changing eclipse depths fit only about half of the TESS visits ten years later

Job `sci-1107-dell-astronomy-62e06f7bc0b3`, campaign 11_07_2026, topic astronomy, machine Dell, model Claude Opus 5.5 (`claude-opus-5-5`).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

This study tests a forecast method that the campaign uses. Earlier campaign work extrapolated eclipse-depth drift to forecast when the eclipses of HD 93683 and HD 303514 stop. Here we do a hindcast test of the same idea on a large, well-measured sample.

- **Sample.** We used the 22 detached Kepler eclipsing binaries (EBs) with a "depth variation" (DV) flag in the Kepler EB catalogue (Kirk et al. 2016), with morphology < 0.5 and period 1-100 d. We also used 40 matched non-DV detached EBs as controls. TESS data are complete for 21 DV systems and 16 controls (see Limitations).
- **Kepler stage (2009-2013).** We fitted 4,532 single Kepler eclipses in 64 eclipse channels (primary or secondary) with one eclipse shape per channel and a free impact parameter |b| per eclipse. Then we fitted four forecasts: linear |b| drift, quadratic |b| drift, persistence (last Kepler |b|) and a linear trend of eclipse depth.
- **TESS stage (2019-2024).** We made our own forced-PSF photometry of TESS full-frame-image cutouts at Gaia DR3 positions (crowded field, 21 arcsec pixels). We measured |b| in each TESS visit with the Kepler shape. We tested each forecast with a |b| tolerance that we calibrated on stable controls (delta = 0.10, which accepts 91% of stable-control visits; 95% range 0.78-0.97).
- **Main result.** For the DV binaries, the forecasts agree with only 33-64% of 121 informative TESS visits (20 systems): linear |b| drift 0.45 (95% system-bootstrap range 0.27-0.63), quadratic 0.33 (0.17-0.51), persistence 0.55 (0.36-0.73) and linear depth trend 0.64 (0.44-0.82). The linear |b| forecast becomes worse with time: 0.66 at 5-8 yr, 0.39 at 8-10 yr and 0.36 at 10-12 yr after Kepler.
- **Direction of the error.** The linear |b| forecast predicts eclipse loss too early. In 92% of the DV visits with a detected eclipse, TESS gives a smaller |b| than the forecast (median difference -1.25; stable controls: -0.21). At the last TESS visit, the linear forecast says "no eclipses" for 24 channels, but 10 of them still have eclipses. Of 11 channels for which it says "eclipses", 10 have eclipses.
- **Two causes.** (1) Kepler saw only partial eclipses in many systems, so the Kepler light curve does not fix where b = 0 is. In 13 channels, TESS eclipses are deeper than the central eclipse of the Kepler model. Examples are KIC 8023317 and KIC 9715925: the linear forecast said "eclipses stop before 2020", but TESS shows deep eclipses in 2019-2024. This agrees with the photodynamical model of Borkovits et al. (2022) for KIC 8023317 (central eclipse near 2023.7). (2) The precession is not linear over 10 years. KIC 7289157 was forecast to stop eclipsing in about 2017. TESS shows grazing eclipses again in 2022 and 2024.
- **Precession fits.** A joint Kepler+TESS model of uniform nodal precession (one node period for both eclipses) gives a constrained node period for 5 of 21 DV systems. For KIC 7955301 it gives P_node = 19.0 yr (2-sigma 16.5-21.8), eclipse loss in about 2016 and eclipse return in 2027.8. The published spectro-photodynamical model (Gaulme et al. 2022) gives 19.2 yr, loss at the start of 2016 and return in 2028. For KIC 8023317 and 5653126, our simple model is not constrained, and its ranges do not include the published 650 yr and 225 yr.
- **Consequence for the campaign.** A depth or inclination trend that is measured over a few years is not a reliable forecast of eclipse loss 10 years ahead. Forecasts such as "HD 303514 loses its eclipses near 2030" need a dynamical model with a known b zero point (full eclipse shape) and a known node period, and a wide uncertainty.

## 1. Question

Campaign publications found real orbital-plane changes from long-baseline photometry. Some forecasts were made from depth or inclination drift: HD 93683 (drift -0.33 deg/yr, sci:sha256:d86cdb9d...) and HD 303514 (eclipses can stop near 2030, sci:sha256:575e53bd..., 2f7e9f37...). A sibling job later found the HD 303514 tertiary from TESS timing (sci:sha256:90287c11...).

Question: **if we have only a few years of excellent photometry of an EB with changing eclipses, how well can a simple drift model forecast the eclipses 5-12 years later?**
The Kepler field gives a direct test. Kepler measured depth changes from 2009 to 2013. TESS observed the same field in 2019, 2020-2021, 2022 and 2024. Borkovits et al. (2025) already listed (without a depth model) Kepler EBs whose eclipses were gone in TESS. Our new parts are: a forecast made only from Kepler data, a quantitative score against TESS, a calibration with control binaries, a comparison of four forecast rules, and joint precession fits.

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| Kepler EB catalogue, 3rd revision (Kirk et al. 2016) | VizieR J/AJ/151/68/catalog (CfA mirror) | Sample (DV flag, period, epoch, morphology) |
| Kepler long-cadence PDCSAP light curves, Q0-Q17 | MAST `archive.stsci.edu/missions/kepler/lightcurves` | Kepler stage, 1,613 files |
| TESS FFI cutouts 9x9 px, sectors 14-82 | MAST TESScut API | TESS stage (forced PSF photometry) |
| Gaia DR3 positions and G, BP, RP | GAVO TAP `gaia.dr3lite` | PSF scene model and merged-light fraction |

`files/provenance/input_hashes.csv` gives the SHA-256 hash, size and exact URL of each input file (Kepler, TESScut, Gaia, catalogue). We do not redistribute the external data. The external terms are in `files/EXTERNAL_DATA_NOTICE.md`.

## 3. Method

### 3.1 Eclipse model
For each eclipse channel, the model is a limb-darkened disc (radius 1, linear limb darkening u) that a disc of radius k hides along a straight chord:
`F(t) = 1 - A occ(sqrt(b^2 + ((t - tc)/tau)^2); k, u)`.
A is the light fraction of the eclipsed star (third light included), tau is the time to cross one stellar radius and b is the impact parameter. Orbital-plane precession changes only b. We used u = 0.6 (Kepler) and 0.45 (TESS). We integrated the model over each exposure.

### 3.2 Kepler stage (`code/kepler_fit.py`)
1. Detrend each quarter with a running median (eclipses masked).
2. Find the primary and secondary eclipses in the folded light curve.
3. Fit one shape (k, tau, A) per channel. Each eclipse gets its own |b| and a small timing offset (alternating fit, three starts in k).
4. Keep, for each eclipse, the full chi-square profile against |b|. The profile is scaled by the reduced chi-square.
5. Fit the drift models to the profiles: |b(t)| = |b0 + b1 x| and |b0 + b1 x + b2 x^2| (x in years from 2011.4). A Laplace approximation, scaled for extra scatter, gives the forecast uncertainty. Eclipses that are not seen are handled correctly, because their profile is flat above b = 1 + k.
6. Two more forecasts: persistence (median |b| of the last 5 Kepler eclipses) and a linear depth trend (weighted fit of eclipse depth against time, clipped to [0, central depth], changed to |b| with the same shape). We added the depth-trend forecast after we saw the b zero-point problem (Section 5). Thus it is not a pre-set test.

### 3.3 TESS stage (`code/tess_phot.py`, `code/tess_fit.py`)
1. Forced PSF photometry per cadence: Gaussian PRF (width and shift fitted on the median image), at Gaia DR3 positions, plus a plane background. Sources closer than 1 px to a fitted source are merged with Gaia flux ratios. We corrected the depth by the merged-light fraction f_t (median over targets 0.96; lowest sector value 0.10; 0.34 for KIC 7289157).
2. For each channel and each TESS visit (sectors less than 200 d apart), we made a chi-square profile against |b| with the Kepler shape. One timing offset per visit is free in a search window that we set from the Kepler timing scatter. We used only eclipses with at least 80% data cover in the window. We clipped bad in-window cadences.
3. Detection: delta chi-square against "no eclipse" > max(25, largest value of the same search at up to 10 phases with no eclipse in the same visit).
4. A visit is "informative" if its profile separates a central eclipse from "no eclipse" by delta chi-square >= 9.

### 3.4 Scores (`code/summary.py`)
A forecast passes in a visit if the TESS profile minimum within |b_forecast| +- delta is <= 9. We calibrated delta on stable controls (Kepler drift < 3 sigma and shape chi2r <= 20; 16 channels, 43 informative visits) with the rule "smallest delta at which >= 90% of the persistence forecasts pass". This gave delta = 0.10 (pass rate 0.91). We set the rules before we looked at all TESS results. Two exceptions are the null-phase detection rule (added after a marginal case, KIC 4769799) and the depth-trend forecast. Section 6 explains both. The 95% ranges come from a bootstrap over systems (4,000 resamples), because visits of one system are correlated.

### 3.5 Precession fits (`code/precession_fit.py`)
The model is b_j(t) = C_j + B_j cos(2 pi (t - t1)/P_node) for channel j, with one P_node and t1 for the system. It uses the Kepler eclipse profiles and the TESS visit profiles (TESS terms capped at 25). P_node goes from 3 to 400 yr. We scaled delta chi-square by chi2_min/dof. We call P_node "constrained" only if this scale < 10, the best value is not at the grid edge and the 2-sigma range is narrower than a factor of 3.

## 4. Results

### 4.1 Forecast scores (DV binaries, informative TESS visits)

| Forecast | All DV (121 visits, 20 systems) | 5-8 yr (32) | 8-10 yr (56) | 10-12 yr (33) | Drifting, good shape (67 visits) |
| --- | --- | --- | --- | --- | --- |
| Linear |b| drift | 0.45 (0.27-0.63) | 0.66 | 0.39 | 0.36 | 0.54 |
| Quadratic |b| drift | 0.33 (0.17-0.51) | - | - | - | 0.42 |
| Persistence | 0.55 (0.36-0.73) | 0.63 | 0.55 | 0.45 | 0.55 |
| Linear depth trend | 0.64 (0.44-0.82) | 0.69 | 0.64 | 0.58 | 0.78 |
| Stable controls, persistence | 0.91 (0.78-0.97) | | | | |

"Drifting, good shape" means Kepler drift > 3 sigma, |b1| > 0.05 per yr and Kepler shape chi2r <= 20 (19 channels, 14 systems). In that group, the depth trend is better than the linear |b| drift by 0.25 (95% range 0.02-0.53). The other differences between forecast rules are not significant (`files/results/scores.json`). All four rules are below the control level. For the depth trend, the 95% ranges overlap slightly.

![Forecast skill](files/figures/fig2_forecast_skill.png)

### 4.2 Per-system behaviour (Figure 1)

![DV primaries](files/figures/fig1_dv_primary_gallery.png)

Last informative TESS visit of each DV primary or secondary eclipse (selected cases; all are in `files/results/tess_visits.csv`):

| KIC | Kepler trend | Kepler-only linear forecast at last visit | TESS 2022-2024 |
| --- | --- | --- | --- |
| 10319590 | eclipses stop 2010 | no eclipses | no eclipses (agrees) |
| 8938628 | |b| rises 0.3 -> 1.1 | no eclipses | no eclipses (agrees) |
| 7670617, 10223616 | |b| rises | no eclipses | no eclipses (agrees) |
| 10268809 | |b| rises | primary: none; secondary: none | primary none; secondary still seen (partly wrong) |
| 8023317 | depth grows, |b| -> 0 | no eclipses after 2018 | deep, flat-bottomed eclipses every visit (wrong; central eclipse near 2023.7 in Borkovits et al. 2022) |
| 9715925 | |b| -> 0 by 2013 | no eclipses after 2020 | deep eclipses every visit (wrong) |
| 5653126 | depth grows | no eclipses | eclipses near b = 0-0.45 (wrong; edge-on passage in Borkovits et al. 2022/2025) |
| 7289157 | |b| rises 0 -> 0.9 | no eclipses after 2017 | grazing eclipses in 2022 and 2024, not in 2019-2021 (wrong; precession turns) |
| 7955301 | |b| -> 0, then rises | no eclipses | no eclipses (agrees; eclipse return expected 2028) |
| 4769799 | |b| rises 0.1 -> 0.7 | no eclipses | a shallow 0.15% dip in 2024 (delta chi2 90, null max 22): candidate eclipse return, needs confirmation |

### 4.3 Precession (Figure 3)

![Precession](files/figures/fig3_precession.png)

| KIC | P_node best (yr) | 2-sigma range (yr) | Note |
| --- | --- | --- | --- |
| 7955301 | 19.0 | 16.5-21.8 | Gaulme et al. 2022: 19.2 yr; model: loss 2016.2, return 2027.8, next loss 2035.2 |
| 7289157 | 36 | 36-97 | eclipses continue in model; grazing now |
| 5771589 | 10.8 | 10.8-11.5 | |
| 9715925 | 4.9 | narrow | short value; needs an outer orbit of about 100 d; treat as tentative |
| 3867593 | 3.7 | 3.0-4.6 | few eclipses per visit; tentative |
| 8023317 | 23 | 18-159 (not constrained, scale 14) | published 650 yr is outside |
| 5653126 | 120 | 25-211 (not constrained, scale 95) | published 225 yr is just outside |

`files/results/precession.csv` has all 21 systems and their eclipse windows for 2026-2040.

## 5. Interpretation

1. **The b zero point is not known from partial eclipses.** If Kepler sees only partial eclipses, then k, A and b are degenerate. The fit can put b = 0 at the deepest Kepler eclipse, even if the true central eclipse is later and deeper. A linear |b| model then "passes through b = 0" and forecasts a return to shallow eclipses and eclipse loss. In 13 DV channels, the TESS eclipses are deeper than the central eclipse of the Kepler model. A depth-trend forecast does not need the b zero point, and it did best.
2. **Precession is periodic.** Linear extrapolation is good only for a small part of the node period. The pass rate of the linear forecast falls from 0.66 (5-8 yr) to 0.36 (10-12 yr). The DV flag selects systems with fast change, and thus short node periods (KIC 7955301: 19 yr).
3. **Thus eclipse-loss dates from drift alone are biased early.** 10 of 24 "eclipses stopped" forecasts were wrong. Only 1 of 11 "eclipses continue" forecasts was wrong.

For HD 303514 and HD 93683, this means: a date of eclipse loss from a depth or inclination trend is not reliable without a dynamical model. The sibling timing result (90287c11) and the photodynamical HD 93683 model (17a4acfc) are the better tools.

## 6. Limitations

- **Incomplete controls.** The TESScut service gave many 504 errors. TESS cutouts are complete for 21 of 22 DV systems (KIC 11558882 missing) and 16 of 40 controls. We stopped the downloads to finish the job. The control calibration uses 16 stable channels and 43 visits. We did not analyse the 8 semidetached DV systems (a secondary group in the plan).
- **Simple eclipse model.** Straight chord, linear limb darkening, the same light fraction in Kepler and TESS bands. Stable controls show a small offset (TESS |b| 0.11 lower than persistence, median). The tolerance delta = 0.10 absorbs most of it. Some Kepler shapes fit poorly (chi2r > 20: spots, red-giant oscillations, third-body eclipses, e.g. KIC 7668648). We report these separately.
- **Rules added after a first look.** We added the null-phase detection test, the in-window clip and the depth-trend forecast after the first TESS results. We say this in Section 3.
- **Detection errors.** For the red giant KIC 7955301, one 2021 visit passes the detection test (delta chi2 32, null max 13), but the published model has no eclipses then. Red-noise false detections are possible.
- **Forced photometry.** Gaussian PRF; the merged-light correction depends on Gaia flux ratios. Light from unresolved companions within about 4 arcsec is the same in Kepler and TESS.
- **Precession model.** Uniform precession with constant mutual inclination. It does not include apsidal motion, eccentricity changes or the b-scale degeneracy. Short node periods (3.7 and 4.9 yr) are tentative.
- **Sample.** The Kirk et al. (2016) DV flag is not a complete or uniform selection. Two non-DV controls also drift (KIC 9032900, 4055092).

## 7. Files

- `files/code/`: all code; `files/code/README_reproduce.md` gives the full recipe.
- `files/results/kepler_events.csv`: per Kepler eclipse: time, |b| (68% range), depth, delta chi2 against flat, timing offset.
- `files/results/kepler_shapes.csv`: shape and drift parameters (with covariances) per channel.
- `files/results/tess_visits.csv`: per TESS visit: measured |b|, detection, null level, forecasts, pass/fail for each tolerance.
- `files/results/systems.csv`, `scores.json`, `precession.csv`, `tess_photometry_sectors.csv` (PSF width, merged-light fraction per sector).
- `files/results/profiles.npz`: chi-square profiles against |b| (Kepler eclipses on a 100-point grid, float16; TESS visits), so that the scores and precession fits can be done again without the raw data.
- `files/figures/`: Figures 1-3 and supplementary galleries (DV secondaries, control primaries).
- `files/provenance/input_hashes.csv`: hashes and URLs of all external inputs.

## 8. Reproduce

Follow `files/code/README_reproduce.md`. The scripts download about 5 GB into a separate `scratch/` folder (not into this bundle). Python 3.12, numpy, scipy, pandas, astropy, matplotlib. Run time on 2 CPUs: about 3 h plus the downloads (TESScut took about 7 min per target). The sample selection uses a fixed random seed.

## 9. References

- Kirk B. et al. 2016, AJ 151, 68 (Kepler EB catalogue III), doi:10.3847/0004-6256/151/3/68
- Borkovits T. et al. 2022, MNRAS 515, 3773 (KICs 6964043, 5653126, 5731312, 8023317), doi:10.1093/mnras/stac1983
- Borkovits T. et al. 2025, arXiv:2502.09480 (Kepler triples revisited by TESS)
- Gaulme P. et al. 2022, A&A 668, A173 (KIC 7955301), doi:10.1051/0004-6361/202244373
- Campaign: sci:sha256:0f548fc8..., 96d47af4..., d86cdb9d..., 575e53bd..., 2f7e9f37..., 17a4acfc..., 90287c11..., d18fffbf... (full IDs in sci.json)
