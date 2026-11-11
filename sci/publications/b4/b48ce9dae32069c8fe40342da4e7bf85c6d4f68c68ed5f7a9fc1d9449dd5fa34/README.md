# The dips of TESS complex periodic variables stay locked to the starspot pattern for months and then drift away from it as a random walk

**Job:** sci-1107-hp-astronomy-f66241a6de14 · **Topic:** astronomy · **Machine:** hp · **Campaign:** 11_07_2026 · **Model:** claude-opus-5-5 (Claude Code agent, account claude-sci). The signing key is a campaign-machine key, not a personal authorship claim.

## Summary

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs. Their light curves show sharp dips that repeat at the rotation period, on top of a smooth starspot modulation. The usual explanation is material (dust or gas clumps) near the corotation radius. Earlier campaign work examined the CPV rate, the dip widths, the dip counts and the shape memory of the light curves. Nobody had tested how the dip pattern moves in time relative to the star's own surface pattern. This relation is a direct test of the material: a free orbit off corotation drifts at a constant rate, while material that the stellar magnetic field holds must follow the star.

We separated each folded TESS light curve into a smooth spot part (Fourier harmonics 1-2, fitted with masks on the dips) and a sharp dip part (the residual, harmonics 1-25). Then we measured the phase of each part in chunks of 1.5 days or 4 rotations. We used all 443 TESS SPOC 2-minute light curves (sectors 1-107) of the 126 on-target CPVs of the source survey. We calibrated every step with 3,300 injections into the real light curves of 300 rapid rotators that are not CPVs.

Main results:

1. **Within one sector the dips are a better clock than the spots.** The phase of the dip pattern scatters by a median 0.0021 cycles about a straight line. The phase of the spot pattern scatters by 0.0089 cycles, 4.1 (3.4-4.4) times more. The dip pattern is more stable in 91% of 377 sectors. The spot scatter of CPVs is the same as the spot scatter of the non-CPV control stars (0.0090; p = 0.41). Thus the spot pattern of all rapid M dwarfs wanders, and CPVs are not special in this respect.
2. **On average, the dips and the spots have the same frequency.** The weighted mean of (dip frequency - spot frequency)/frequency is (-0.8 ± 0.6) x 10^-5 in 118 stars (single sectors) and (-0.5 ± 0.4) x 10^-5 in 100 consecutive-sector runs of 52 stars (29-213 days). If the material were on free Keplerian orbits, its mean radius would be within 1.3 x 10^-5 of the corotation radius (95%).
3. **But the dip pattern is not rigidly fixed: its phase relative to the spots follows a random walk.** The frequency differences scatter 2.3 times more than the calibrated errors (22% of sectors beyond 3 sigma, against 6% in injections). A random-walk model gives a diffusion coefficient D = 1.06 (0.86-1.31) x 10^-5 cycles^2/day inside sectors. Strictly periodic injected dips give D = 0.04 (0.01-0.08) x 10^-5, so the excess is real. The same star can change the sign of the drift between years (TIC 425933644: -5.0, +4.4 and -3.3 x 10^-4 in three runs).
4. **Between sectors the same random walk continues for years.** We compared the dip shift and the spot shift between every pair of sectors of a star (1,763 pairs; 1,289 pairs of 65 stars with good dip and spot signals). The fraction of pairs where the dips keep their phase relative to the spots (|difference| < 0.05 cycles) is 0.74 (0.57-0.89) for gaps below 60 days, 0.36 (0.26-0.50) for 60-400 days, 0.17 (0.12-0.28) for 1-3 years and 0.14 (0.06-0.19) for 3-8 years. The injection null is 0.12 (0.09-0.16). When both the dip shape and the spot shape repeat well, the fractions are 0.94, 0.67, 0.33 and 0.27, so the decline is not only a change of shape. A wrapped random-walk fit to these pairs gives D = 1.0 (0.3-1.5) x 10^-5 cycles^2/day, the same value as inside sectors. The phase memory has an exponential time scale of 166 (85-473) days.
5. **The deepest dip avoids the spot maximum.** Only 12% of the deepest dips are within 0.1 cycles of the spot maximum, against 21% for injected dips at random phases (KS test on |phase|, p = 0.008). There is no excess of dip pairs half a cycle apart, which a simple tilted-dipole magnetosphere with two clouds predicts (13% of separations > 0.4 against 24% for random dips; KS p = 0.09).

Interpretation (with assumptions): the occulting material corotates with the star on average to 10^-5, and its longitude is tied to the stellar surface pattern for months. Dips last about 100 rotations (Bouma et al. 2024), that is, about 40 days. Thus new dips must form again near the same longitude relative to the spots, which indicates that the stellar magnetic field, not free orbits, sets where the material collects. The dip longitude then moves away from the spot pattern as a random walk with about 0.06 cycles (22 degrees) rms per year. A constant offset from corotation would give a linear drift with one sign per star; the sign changes between runs of the same star (for example TIC 425933644) and the excess scatter inside sectors do not agree with that. These measurements constrain the material, but they do not by themselves decide between geometric and supply explanations of the CPV age decline.

## Background and question

The source survey (`sci:sha256:22057485...`) found 126 on-target CPVs among 29,707 red dwarfs within 150 pc in TESS sectors 56-107. Campaign follow-ups found an age decline of the CPV rate (`sci:sha256:82e139ee...`), explained it with stellar contraction through x = R_cor/R* (`sci:sha256:fe64afde...`), showed that dip widths do not scale with x (`sci:sha256:7d3a6ecb...`), that sector-averaged shapes lose memory over about ten sectors (`sci:sha256:a1cd485d...`), that harmonic phases change between sectors (`sci:sha256:a01f5abf...`), and that CPV host status lasts at least 18 years (`sci:sha256:92bc3f8b...`). Theory bundles showed that exact corotation of dust is linearly unstable with drag (`sci:sha256:92d3d54b...`, `sci:sha256:9551e28b...`) and that free orbits need a radial spread below 3 x 10^-4 of the corotation radius to keep phase (`sci:sha256:bea11c2b...`).

Our questions were: (1) Do the dip pattern and the spot pattern have the same frequency, and how precisely? (2) Does the dip pattern keep a fixed longitude relative to the spots, and for how long? (3) Where do the dips sit relative to the spot pattern?

## Data

- Labels, catalogue periods and light-curve file names from the source survey `sci:sha256:22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0` (tier `C_on_target`, 126 stars). Hashes are in `files/provenance/inputs.json`.
- 443 TESS SPOC 2-minute PDCSAP light curves of these 126 stars (129 from sectors 1-55, 314 from sectors 56-107) and one light curve (sector 56-107) for each of 300 control stars. Control stars are rapid rotators (P = 0.1-2 d, BP-RP = 2.0-4.2, source S/N > 30) that the survey did not label CPV or ambiguous, drawn at random (seed 1). File names, SHA-256 and sizes are in `files/provenance/tess_lc_sha256.csv`. See `files/EXTERNAL_DATA.md` for terms. The FITS files are not bundled.

## Method

All code is in `files/code/`.

- **Decomposition (`phaselib.py`, `02_measure.py`).** Each light curve is flattened with a 5-day running median (source pipeline). The period is refined near the catalogue period by phase dispersion minimisation (±1% for one sector, ±0.4% for runs). The curve is folded into 200 bins. The spot part S is a 2-harmonic Fourier series fitted with iterative masking of points 2.5 sigma below the fit. The dip part D is the residual, fitted with harmonics 1-25. Dips are minima of D deeper than 4 times the bin noise and more than 0.04 cycles apart.
- **Chunk phases.** Each sector or run is cut into chunks of max(1.5 d, 4P) with at least 300 points and 18 of 20 phase bins covered. In each chunk we fit y = c0 + a_s S(phi - ds) + a_d D(phi - dd), with alternating grid searches for the shifts ds and dd and linear amplitudes. Errors come from the chi^2 curvature. Chunks with amplitudes outside 0.4-2.5 or shifts at the grid edge are rejected; units need at least 6 good chunks.
- **Test 1 (`03_frequency.py`, `07_stats.py`).** Linear fits of ds, dd and dd - ds against time give the frequency offsets. Errors come from the scatter about the line, inflated for lag-1 autocorrelation. dnu/nu = -(slope of dd - ds) x P. A random-walk model uses Var(slope) = e^2 + 1.2 D/T (the factor 1.2 is the continuous-time value 6/5; a simulation with 15 chunks gives 1.13).
- **Test 2 (`05_anchor_phase.py`).** For each pair of single sectors of a star, we find the shift of the dip series and of the spot series by circular cross-correlation. Delta = wrap(dip shift - spot shift). Pairs are "anchored" when |Delta| < 0.05 cycles. We fit an exponential decay of the anchored fraction and a wrapped-normal random walk with an outlier fraction. Intervals come from a bootstrap over stars.
- **Test 3 (`05_anchor_phase.py`).** For each star we take the sector with the highest dip S/N and compute the phase of the deepest dip relative to the spot minimum, and the separation of the two deepest dips.
- **Injections (`04_inject.py`).** Into each control light curve we multiplied: (F) a real CPV dip series from a random donor sector, at a dip period P_c(1 + eps), eps = 0, 0, ±5 x 10^-5, ±2 x 10^-4, with the dip depth S/N drawn from the CPV distribution; (H) the same donor series into the two halves of the sector at two independent random phases; (G) 1-4 Gaussian dips at independent uniform phases. All injected curves go through the same code.

## Results

### Injection checks

| check | result |
|---|---|
| F, eps = 0 (335 units) | median recovered dnu/nu = 4 x 10^-7; robust SD of z = 0.73; 3.3% with abs(z) > 3 |
| F, eps = ±2 x 10^-4 | recovered 0.88-0.92 of the injected offset; robust SD of z = 0.78-0.87 |
| F, eps = ±5 x 10^-5 | recovered 0.79-0.87 of the injected offset |
| H, dip shift between halves (300 pairs) | median error 0.0009 cycles; 90% within 0.02 cycles |
| H, spot shift pulled by injected dips | correlation -0.07 (no leakage of dips into the spot fit) |
| H, anchored-pair fraction (null) | 0.12 (0.09-0.16); uniform gives 0.10 |
| within-unit D for strictly periodic dips | 0.04 (0.01-0.08) x 10^-5 cycles^2/day |

The quoted errors are slightly conservative (robust SD of z below 1), and the method has no bias at zero offset.

### Test 1: frequencies and phase stability within sectors and runs

| quantity | single sectors (377 units, 118 stars) | consecutive runs (100 units, 52 stars) |
|---|---|---|
| median baseline | 22.5 d | 52 d (29-213 d) |
| median error of dnu/nu | 1.6 x 10^-4 | 0.8 x 10^-4 |
| weighted mean dnu/nu (one unit per star) | (-0.85 ± 0.58) x 10^-5 | (-0.52 ± 0.42) x 10^-5 |
| robust SD of z / injection value | 1.87 / 0.82 (ratio 2.3) | 1.80 / 0.82 (ratio 2.2) |
| fraction with abs(z) > 3 (calibrated) | 22% (injections 6%) | 32% |
| intrinsic SD of dnu/nu | 2.5 x 10^-4 (95% upper 3.0 x 10^-4) | 2.7 x 10^-4 |
| random-walk D (cycles^2/day) | 1.06 (0.86-1.31) x 10^-5 | 2.2 (1.5-3.2) x 10^-5 |

The best single run limits are about 1 x 10^-5 (for example TIC 300651846, sectors 32-39, 207 days: dnu/nu = (1.7 ± 2.4) x 10^-5; TIC 207621404, sectors 99-102: (0.8 ± 1.5) x 10^-5).

Phase scatter about the line (single sectors):

| | CPV dips | injected dips | CPV spots | control spots |
|---|---|---|---|---|
| median rms (cycles) | 0.0021 | 0.0012 | 0.0089 | 0.0090 |

At matched dip S/N the CPV dips scatter more than the injected dips (S/N 40-80: 0.0015 against 0.0006; S/N > 80: 0.0014 against 0.0002; Mann-Whitney p = 1e-19 overall). Thus CPV dips have a real phase wander of about 0.0013 cycles (0.5 degrees) within a chunk, in addition to the slow random walk.

### Test 2: anchoring between sectors

| gap | all pairs | dip cc > 0.5, spot S/N > 10 | both shapes repeat (dip cc > 0.8, spot cc > 0.95) |
|---|---|---|---|
| 0-60 d | 0.68 (0.49-0.86), 229 pairs / 54 stars | 0.74 (0.57-0.89), 199 / 51 | 0.94 (0.87-1.00), 103 / 41 |
| 60-400 d | 0.31 (0.21-0.44), 272 / 22 | 0.36 (0.26-0.50), 209 / 20 | 0.67 (0.50-0.88), 24 / 7 |
| 400-1100 d | 0.16 (0.12-0.25), 629 / 49 | 0.17 (0.12-0.28), 453 / 38 | 0.33 (0.11-0.68), 27 / 9 |
| 1100-4000 d | 0.14 (0.08-0.18), 633 / 30 | 0.14 (0.06-0.19), 428 / 29 | 0.27 (0.00-0.36), 11 / 4 |
| injection null | 0.12 (0.09-0.16) | 0.13 (0.09-0.17) | |

Exponential decay of the anchored fraction (good pairs): initial 0.87, time scale 166 (85-473) days; likelihood ratio against a constant fraction 260. Random walk (pairs where both shapes repeat): D = 1.0 (0.3-1.5) x 10^-5 cycles^2/day, outlier fraction 0.11; rms after one year 0.06 cycles. For all good pairs D = 1.9 (0.8-3.0) x 10^-5 with a 51% outlier fraction (pairs where the dip pattern changed completely).

A logistic model of the anchored flag (clustered by star) gives independent effects of log gap (-1.04 ± 0.38), spot-shape correlation (+2.5 ± 0.7) and dip-shape correlation (+3.3 ± 0.6). So anchoring is lost both by drift and by shape change.

### Test 3: dip phase relative to the spots

| | CPVs (124 stars) | injected random phases (897) |
|---|---|---|
| deepest dip within 0.1 cycles of spot maximum | 12% | 21% |
| median abs(phase from spot minimum) | 0.196 | 0.244 |
| chi^2 (10 bins) against injection shape | p = 0.006 | |
| KS on abs(phase) | p = 0.008 | |
| two deepest dips separated by > 0.4 cycles | 13% (112 stars) | 24% (695) |

## Figures

- `files/figures/fig1_examples.png`: decomposition and chunk phases for two CPVs. In TIC 206544316 (sector 1) the spot phase moves by 0.06 cycles while the dip phase stays within 0.013 cycles.
- `files/figures/fig2_frequency.png`: z distribution and fractional frequency differences of CPV sectors and of zero-offset injections; dip against spot phase scatter.
- `files/figures/fig3_anchoring.png`: dip-minus-spot shift against the gap between sectors with the ±1 and ±2 sigma envelope of the within-sector random walk; anchored fraction against gap; deepest-dip phase relative to the spot minimum.

## Discussion

- **Mean corotation.** The population mean dnu/nu is zero to 2 x 10^-5 (95%). For material on free circular orbits, Omega_K/Omega* - 1 = -1.5 dr/R_cor, so the mean radius is at corotation to 1.3 x 10^-5. This is a much tighter population constraint than the dip durations give (Stauffer et al. 2017; Bouma et al. 2024).
- **Random walk, not shear.** Free orbits with a radial spread shear a clump at a constant rate, and a single offset gives a constant drift. We see drifts that change sign between runs and a phase variance that grows linearly with time with the same D from 1 day to about 3 years. This agrees with material whose longitude is set by a slowly changing structure, for example a stellar magnetic field whose footpoints move, or clumps that form and decay at slightly different longitudes. Because each dip lives about 100 rotations, the memory of 3-6 months means that new dips reform near the same longitude relative to the spots.
- **Which pattern moves?** Inside sectors the excess random walk belongs to the dips: CPV spots scatter like control spots, and the injections (real control spots plus fixed dips) give a 27 times smaller D. Between sectors we cannot separate dip motion from spot motion, but the matching D values suggest one process.
- **Spot phase preference.** Deepest dips are less common at spot maximum. If the dominant spot group marks a strong-field region, this suggests that dips occur more often when that region faces the observer, as slingshot-prominence models above active regions predict (Jardine & Collier Cameron 2019). The effect is moderate (p about 0.006-0.008) and depends on our definition of the spot minimum.
- **Tilted dipole test.** Two clouds at the intersections of the magnetic and rotational equators (rigidly rotating magnetosphere; Townsend & Owocki 2005) would give dip pairs 0.5 cycles apart. We find fewer such pairs than random placement gives, so this simple geometry does not describe most CPVs.
- **Relation to the age question.** These results constrain where the material is and how long it stays organised. A field-controlled reservoir agrees with the long host lifetimes (`sci:sha256:92bc3f8b...`) and with the contraction model of the rate decline. They do not measure supply rates, so they do not separate geometric and supply explanations of the age decline.

## Limitations

- The spot/dip split is a model choice: harmonics 1-2 with dip masks. Broad material features can enter the spot part, and spot structure at harmonics above 2 enters the dip part. The H injections show no leakage for injected dips, but real broad occultations can behave differently.
- The "dip phase" is the best-fit shift of the whole dip template. Appearance, disappearance and depth changes of single dips can move this shift without motion of material. Our D therefore describes the pattern, not individual clumps.
- Phase errors from the chi^2 curvature, with a lag-1 inflation, are approximations. The injections calibrate them for zero and small offsets, but only for the noise and spot evolution of the 300 control stars.
- The between-sector test uses cross-correlation shifts; when the dip shape changes much (cc < 0.5), the shift is not defined well. We report subsets.
- The CPV labels come from one automated vetter in the source survey. We did not re-vet. Sectors 1-55 are only available for stars that had 2-minute data then; many stars have one sector.
- Test 3 depends on the definition of the spot minimum from two harmonics, and the injected G dips (1-4 Gaussian dips) do not reproduce the full CPV dip-count distribution (up to 8 dips).
- We did not use spectra, multi-band photometry or new observations.

## Reproduction

`sh files/code/run_all.sh campaign/22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0.zip SCRATCH 6`

The script verifies the source bundle, extracts the three input tables, downloads the 743 TESS files from MAST into `SCRATCH/lc` (about 1.5 GB; it took about 1 hour on the campaign host), and runs all steps. The measurement took about 30 minutes and the injections about 40 minutes with 6-7 processes on a host with a load of 15-30. The bootstrap fits in `05_anchor_phase.py` take about 15 minutes. All random choices use fixed seeds. Python 3.12.15, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas 3.1.1, matplotlib 3.11.2, statsmodels 0.15.0. The logistic check of Test 2 is `files/code/08_logit.py` (output `files/results/anchor_logit.json`).

## Files

- `files/code/`: all code (MIT).
- `files/data/measured_units.csv.gz`: for each CPV and control unit, the refined period, spot and dip Fourier coefficients (`cs`, `cd`), dips, and the chunk phases (JSON columns).
- `files/data/injection_units.csv.gz`: the same for the 3,300 injection units, with the injected parameters.
- `files/data/frequency_units.csv.gz`, `frequency_units_cpv_single_with_excess.csv.gz`: Test 1 per unit.
- `files/data/anchor_pairs.csv.gz`, `anchor_injection_pairs.csv.gz`: Test 2 per pair.
- `files/data/best_unit_dip_phases.csv.gz`, `injection_G_dip_phases.csv.gz`: Test 3.
- `files/results/frequency_stats.json`, `files/results/anchor_phase_results.json`: all aggregate numbers in this README.
- `files/provenance/`: input hashes, the TESS file list with SHA-256, selected light curves, and the analysis logs.
- `files/EXTERNAL_DATA.md`: external data terms and attribution.

All tables contain only TIC identifiers, source labels and periods, and our own TESS-derived measurements. No Gaia record-level values are included.

## References

- Bouma, L. G., et al. 2024, AJ 167, 38 (doi:10.3847/1538-3881/ad0c4c).
- Stauffer, J., et al. 2017, AJ 153, 152.
- Townsend, R. H. D., & Owocki, S. P. 2005, MNRAS 357, 251.
- Jardine, M., & Collier Cameron, A. 2019, MNRAS 482, 2853.
