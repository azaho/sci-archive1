# Gaia DR3 radial-velocity scatter identifies on-target binary false positives among TESS planet candidates

**Job:** sci-1107-dell-astronomy-840a1600b59d (campaign 11_07_2026, topic astronomy, machine dell). **Model:** Claude Opus 5.5 (claude-opus-5-5). **Date:** 2026-11-09. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Many TESS Objects of Interest (TOIs) are eclipsing binaries, not planets. Ground spectroscopy finds them, but it is slow. Gaia DR3 measured the radial velocity (RV) of bright stars 10 to 40 times from 2014 to 2017. A planet moves its host star by less than about 0.3 km/s. A stellar companion moves it by 5 to 100 km/s. Thus:

1. Does the Gaia DR3 RV-variability test separate confirmed planets from on-target stellar binaries among TOIs?
2. Did the test predict the later verdicts on TOIs that had no verdict in November 2020, before Gaia DR3 (June 2022)?
3. Is the size of the RV scatter consistent with the known mass of the companion?
4. Which open candidates does the test flag now?

Earlier work used Gaia DR3 non-single-star (NSS) orbits to reject TOIs (Tarrants and Mendes 2023, arXiv:2310.12380), and a campaign study matched Gaia DR3 eclipsing binaries to TOIs (sci:sha256:987dcc64...). Those methods need a full Gaia orbit solution. Only 263 of about 7,200 matched TOI hosts have one. The RV-variability statistics in `gaia_source` exist for all hosts with G_RVS <= 12. We did not find a published calibration of these statistics against TFOP verdicts.

## Data and method

- **TOIs:** ExoFOP TOI table on 2026-11-09 (8,175 TOIs), and an Internet Archive capture of the same table on 2020-11-20 (2,394 TOIs).
- **Gaia DR3:** We propagated each TOI position to epoch 2016.0 with its proper motion. We selected the nearest Gaia source within 3 arcsec with G within 1.5 mag of T + 0.5. This matched 7,502 TOIs. We used `rv_chisq_pvalue`, `rv_renormalised_gof`, `rv_nb_transits`, `rv_method_used`, `radial_velocity_error`, `rv_template_teff`, `vbroad`, and NSS two-body orbits.
- **Flag:** We used the criterion of Katz et al. (2023): `rv_chisq_pvalue <= 0.01` and `rv_renormalised_gof > 4`, with `rv_nb_transits >= 10` and `rv_method_used = 1` (G_RVS <= 12). We kept hosts with template temperature 3900 to 8000 K. 3,334 TOIs are testable.
- **Epoch scatter:** For `rv_method_used = 1`, DR3 gives `radial_velocity_error = sqrt(pi/(2N) * sigma^2 + 0.11^2)`. We inverted this relation to get the epoch scatter sigma. We subtracted in quadrature a noise model: the median sigma of RV-constant TOI hosts (p > 0.01) in 0.25-mag G_RVS bins. The result is the intrinsic scatter.
- **Companion mass:** We set K = sqrt(2) x intrinsic scatter (circular orbit, random phases), used the TOI period and the TOI stellar mass, and solved the mass function for the minimum companion mass. This mass is correct only if the transiting object causes the RV variation.
- **Classes:** We used the TFOPWG disposition. We divided FP (false positive) TOIs by comment keywords: "spectroscopic binary" (SB1, SB2, SEB1, SEB2), "eclipsing binary on target" (EB without a neighbour keyword), "nearby" (NEB, BEB, NPC, centroid offset, neighbour), and "not parsed". CP and KP are "planet" (this class includes brown dwarfs that TFOP lists as CP). PC and APC are "open candidate". We counted each host once per class and removed 32 hosts with two conflicting classes.
- **Forecast test:** We took the TOIs with TESS disposition PC/APC and no TFOPWG verdict (or PC/APC) on 2020-11-20. We compared the Gaia flag with their TFOPWG verdict on 2026-11-09.

## Results

### 1. The flag separates on-target binaries from planets (Figure 1)

| Class (hosts) | Flagged | Fraction (95% CI) |
| --- | --- | --- |
| Hosts of known planets with largest K < 0.3 km/s (NASA Exoplanet Archive) | 5 / 447 | 0.011 (0.005-0.026) |
| All CP/KP hosts | 30 / 640 | 0.047 (0.033-0.066) |
| FP, spectroscopic binary | 46 / 50 | 0.92 (0.81-0.97) |
| FP, eclipsing binary on target | 24 / 54 | 0.44 (0.32-0.58) |
| FP, reason not parsed | 83 / 219 | 0.38 (0.32-0.45) |
| FP, nearby eclipsing binary or centroid offset | 52 / 265 | 0.20 (0.15-0.25) |
| False alarm | 6 / 40 | 0.15 (0.07-0.29) |
| Open candidate (PC/APC) | 381 / 1,829 | 0.21 (0.19-0.23) |

- The false-flag rate on hosts of low-K planets is 1.1%. It does not change with magnitude: 1/77, 1/90, 2/129 and 1/151 in G_RVS bins <9, 9-10, 10-11 and 11-12 (Figure 2).
- The area under the ROC curve for spectroscopic binaries against planets is 0.966 (bootstrap 95% CI 0.931-0.989). The Mantel-Haenszel odds ratio, stratified by G_RVS, is 43 for on-target binaries (spectroscopic + eclipsing) against planets.
- Nearby-EB false positives are also flagged more often than planets (odds ratio 4.9). The Gaia flag measures the target star only. Thus some "nearby" FPs have a binary target. For 4 of the 52 flagged nearby FPs, the Gaia NSS orbit period equals the TOI period (or 0.5x or 2x, within 2%). This suggests that the eclipse is on the target for these 4.

### 2. The flag predicted later verdicts (Figure 3)

734 testable TOIs had no TFOPWG verdict on 2020-11-20.

| 2026 verdict | Gaia flagged (119) | Not flagged (615) |
| --- | --- | --- |
| False positive | 41 | 108 |
| CP/KP | 5 | 199 |
| False alarm | 3 | 19 |
| Still PC/APC | 70 | 289 |

- Of the flagged TOIs with a planet/FP verdict, 41/46 (89%, CI 77-95%) became false positives. Of the unflagged ones, 108/307 (35%, CI 30-41%) did (Fisher p = 2.9e-12).
- All 5 flagged TOIs that became CP are brown dwarfs: TOI-148 b, TOI-503 b, TOI-569 b, TOI-1406 b and TOI-2336 b. No flagged TOI in this sample became a planet below 13 Jupiter masses.
- TFOP comments mention Gaia RV information for 57 TOIs (for example "same period as Gaia NSS" or "Gaia DR2 error"). When we remove these TOIs, the result does not change: 39/44 flagged against 107/306 unflagged became false positives.
- The flag is specific but not sensitive: 108 unflagged TOIs also became FPs. Of these, 66 are nearby eclipsing binaries or centroid offsets, which a test of the target star cannot find.

### 3. The scatter gives the correct companion mass

For flagged hosts of companions with a published mass, the mass from the Gaia scatter agrees with the published mass (results/mass_check_nea.csv):

| TOI | Companion | Published mass (M_J) | Gaia-scatter mass / published mass |
| --- | --- | --- | --- |
| 185.01 | WASP-18 b | 10.2 | 1.03 |
| 4603.01 | TOI-4603 b | 12.9 | 1.05 |
| 5882.01 | TOI-5882 b | 22.0 | 0.98 |
| 1476.01 | KELT-1 b | 27.2 | 1.26 (broad lines) |

Brown-dwarf hosts that TFOP lists as CP fall between the 13 M_J and 0.075 M_sun curves (Figure 4). For flagged spectroscopic and on-target eclipsing binaries, 65 of 72 give a stellar minimum mass (> 0.075 M_sun) at the TOI period.

Other flagged planet hosts have more scatter than their planets can cause. The known causes are a stellar companion (WASP-20, Gaia RUWE 33; TOI-1338, a circumbinary planet host), fast rotation with broad lines (Gaia vbroad 28 to 81 km/s: HAT-P-67, XO-6, Kepler-448, EPIC 246851721), and youth with activity (HIP 67522, HIP 94235). We did not find a cause for WASP-163 (TOI-7472.01): its intrinsic scatter is 5.5 km/s, but WASP-163 b (1.87 M_J) has a published K of 0.33 km/s. TOI-7154.01 (CP) has an intrinsic scatter of 156 km/s. These two hosts need RV follow-up. An unseen companion or an RV error can cause the scatter.

### 4. Flagged open candidates (results/flagged_open_candidates.csv)

386 PC/APC TOIs on 384 hosts have the flag. With a 1.1% false-flag rate (upper limit 2.6%), we expect about 20 (at most about 48) false flags among the 1,829 testable open-candidate hosts. We put each flagged TOI in a priority class:

| Priority | Rule | TOIs | of which TFOPWG PC with no binary note in the TOI comments |
| --- | --- | --- | --- |
| A | Gaia NSS orbit period = TOI period (x0.5, x1, x2, within 2%) | 73 | 29 |
| B | Stellar minimum mass at the TOI period, vbroad <= 40 km/s or unknown | 167 | 104 |
| C | Brown-dwarf or planetary minimum mass | 96 | 70 |
| D | Broad lines (vbroad > 40 km/s); spectra necessary | 50 | 34 |

The 133 PC TOIs in classes A and B with no binary note are the main new prediction: we expect most of them to be stellar binaries (on-target eclipsing binaries, or planets in binaries). The 2020 forecast gives a guide: 89% of flagged TOIs with a verdict became false positives.

## Limitations

- The test applies only to hosts with G_RVS <= 12 and template temperature 3900-8000 K (41% of TOIs).
- The flag shows that the target star moves. It does not show that the transit signal comes from the companion. A planet in a wide binary is also flagged. Class C includes possible brown dwarfs and real planets in binaries.
- Broad lines and stellar activity cause false flags. The flag rate of CP/KP hosts is 11/301 for vbroad < 15 km/s, 9/37 for 15-40 km/s and 3/12 above 40 km/s.
- We parsed FP reasons from free-text comments. The parse is approximate. 219 FPs have no parsed reason.
- The noise model and the sqrt(2) factor are approximations. The minimum mass assumes a circular orbit at the TOI period.
- The forecast test is not fully blind: TFOP observers can see Gaia DR2 and DR3 data. The 57 TOIs whose comments mention Gaia RV data do not change the result, but other unrecorded use is possible.
- The ExoFOP and NASA Exoplanet Archive tables change daily. A re-run on a later date gives a slightly different sample.

## Reproduction

`bash files/code/run_all.sh /path/to/scratch` downloads the inputs into the scratch directory and runs scripts 01-06 (Python 3.12 with numpy, pandas, scipy, astropy, pyvo, matplotlib). The Gaia queries use the AIP TAP mirror and take about 30 min. files/PROVENANCE.md gives the SHA-256 of each input that we used. files/NOTICE-external-data.md gives the external data terms. The bundle does not contain Gaia, ExoFOP or NASA Exoplanet Archive catalogue columns. It contains identifiers, our class labels, and the quantities that we computed.

## Files

- `files/results/derived_toi_gaia_rv_flags.csv`: one row per TOI: TOI, TIC, Gaia DR3 source_id, class, flags, epoch scatter, noise model, intrinsic scatter, minimum companion mass, NSS period match, comment-note flags.
- `files/results/flagged_open_candidates.csv`: the 386 flagged open candidates with priority class.
- `files/results/flagged_planet_tois.csv`, `forecast_2020_sample.csv`, `table1_flag_rate_by_class.csv`, `table2_flag_rate_by_grvs_bin.csv`, `noise_model_grvs.csv`, `mass_check_nea.csv`, `summary.json`.
- `files/figures/`: Figures 1-4. `files/code/`: all code.

## Figures

- Figure 1 (`fig1_flag_rate_by_class.png`): flag rate by class.
- Figure 2 (`fig2_scatter_vs_grvs.png`): epoch RV scatter against G_RVS with the noise model.
- Figure 3 (`fig3_forecast_2020.png`): 2026 verdicts of TOIs that were open on 2020-11-20, by flag.
- Figure 4 (`fig4_scatter_vs_period.png`): intrinsic scatter against TOI period for flagged TOIs, with curves for companion masses.

## References

- Katz D. et al. 2023, A&A 674, A5, Gaia DR3 radial velocities, doi:10.1051/0004-6361/202244220.
- Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1, doi:10.1051/0004-6361/202243940.
- Guerrero N. et al. 2021, ApJS 254, 39, the TESS Objects of Interest catalog, doi:10.3847/1538-4365/abefe1.
- Tarrants T. and Mendes E. 2023, arXiv:2310.12380.
