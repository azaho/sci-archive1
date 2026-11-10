# Finnish atlas range margins of southern birds moved north more slowly in 2006-10 to 2022-25 than before while isotherms moved fast; lower detection in 2022-25 explains part of this

**Job:** sci-1107-dell-climate-pollution-biodiversity-b6e78c068107 · **Topic:** climate-pollution-biodiversity · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`, Claude Code) · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Finland has four national breeding bird atlases on the same 10 km grid: 1974-79, 1986-89, 2006-10 and 2022-25. The fourth atlas finished in 2025. Earlier work (Brommer et al. 2012, PLoS ONE 7:e43648) used the first three atlases. It found that the northern range margins of southern species moved north at 1.1-1.3 km per year. We used the new fourth atlas as an out-of-sample test. We wrote a plan before we downloaded the atlas-4 species data (`files/PREREGISTRATION.md`).

Main results (primary analysis: squares with at least "satisfactory" survey activity in both atlases of a pair, breeding category "possible" or higher, margin = mean north coordinate of the 10 extreme occupied squares, species-level bootstrap 95% CI):

| Interval | Southern species, northern margin (km/yr) | Northern species, southern margin (km/yr) | May-June isotherm, 10-yr windows (km/yr) | Annual isotherm, 10-yr windows (km/yr) |
|---|---|---|---|---|
| 1974-79 → 1986-89 | 1.25 (-0.66 to 3.10), n=58 | 1.06 (-2.50 to 4.77), n=13 | 2.7 | -2.5 |
| 1986-89 → 2006-10 | 4.99 (3.50 to 6.64), n=60 | 1.27 (-0.28 to 3.18), n=13 | -0.1 | 8.8 |
| **2006-10 → 2022-25** | **0.49 (-0.68 to 1.66), n=70** | **5.26 (2.20 to 8.64), n=13** | **9.4** | **7.6** |
| 1974-79 → 2006-10 | 3.48 (2.42 to 4.62), n=61 | 1.17 (-0.61 to 3.11), n=11 | 0.9 | 4.9 |

1. **The leading edge slowed.** From 2006-10 to 2022-25, the northern margins of 70 southern species moved north by 0.49 km per year (95% CI -0.68 to 1.66). The prediction from the earlier atlases (P1: 1974-79 → 2006-10 rate, 3.5 km/yr) is outside this interval. The slowdown occurred in the interval with the fastest May-June warming (isotherm shift 9.4 km/yr). It also occurred in species far from the north coast (margin south of 7,300 km: 0.34 vs 2.95 km/yr before), and when we defined species groups from atlas 2 instead of atlas 3 (0.12 vs 5.50 km/yr).
2. **Part of the slowdown comes from detection.** In well-surveyed squares, atlas 4 recorded 89.3 species per square against 94.5 in atlas 3. The atlas activity categories did not remove this difference. We used 136 widespread species as a detection calibrator; this calibrator does not contain the tested species. In squares where the two atlases detected nearly the same number of widespread species (within ±2, 625 squares), the leading edge moved 1.29 km/yr (0.04 to 2.62), against 2.83 km/yr (1.35 to 4.37) for the same control in 1986-89 → 2006-10. In squares where atlas 4 detected at least as many widespread species (992 squares; this set over-corrects, because widespread-species occupancy rose by a log ratio of 0.08 per decade in it), the edge moved 3.58 km/yr (2.35 to 4.87). In the 71% of squares where atlas 4 detected fewer widespread species, the edge did not move (-0.88, -2.08 to 0.32). Thus, the size of the slowdown depends on the detection control. Under balanced detection, a slowdown to about one half to one third of the earlier rate remains, and the occupancy gain of southern species stopped (log ratio +0.18 to +0.21 per decade before, about 0.00 after).
3. **The trailing edge of northern species retreated faster.** The southern margins of 13 northern species moved north by 5.26 km/yr (2.20 to 8.64), against about 1.2 km/yr before. This result held for every effort filter (4.2 to 8.1 km/yr), and the occupied squares of northern species decreased (log ratio -0.23 per decade, about -21%). Large retreats were in Siberian Tit, Red-necked Phalarope, Broad-billed Sandpiper, Temminck's Stint and Lapland Longspur. With balanced detection only 4-8 northern species are left, and the confidence intervals become wide (6.69, 1.06 to 13.60 at ±4, n=8; too few species at ±2).
4. **Species rates did not repeat, and extrapolation did not forecast.** The species rates for 1974-79 → 1986-89 and for 2006-10 → 2022-25 have no correlation (Spearman 0.01, -0.29 to 0.29, n=57; these intervals use different atlases, so the noise is independent). When we extrapolated each species' 1974-79 → 2006-10 rate, the forecast of the atlas-4 northern margin was worse than "no change" (mean absolute error 77.9 km vs 56.2 km; difference +21.8 km, 3.7 to 41.0). The group-mean rate was also worse than "no change" (+14.2 km, 2.5 to 25.3). For the 7-10 northern species, the extrapolation was slightly better than "no change" with probable/confirmed records (-29 km, -54 to -6) but not clearly better with all records.
5. **Margin shifts did not follow breeding-season isotherms.** The May-June isotherm moved about 0 km/yr when the leading edge advanced fastest (1986-89 → 2006-10). It moved about 9 km/yr when the edge advanced least (2006-10 → 2022-25). With annual-mean isotherms, the ratio of margin shift to isotherm shift was 0.6-0.7 for 1986-89 → 2006-10 and 1974-79 → 2006-10, and 0.06-0.17 for 2006-10 → 2022-25 (primary and balanced-detection rates). Prediction P3 (ratio below 1) was correct in the intervals with warming. In 1974-79 → 1986-89 the annual isotherm moved south.

## Data

* **Atlases 1-2** (1974-79, 1986-89): `lintuatlas12.zip`, Finnish Museum of Natural History (Luomus), CC BY 3.0. Breeding category per species and 10 km YKJ square, and survey activity category per square.
* **Atlas 3** (2006-10): `atlas3data.zip`, Luomus, CC BY 4.0. Same fields.
* **Atlas 4** (2022-25): public atlas API of Luomus and BirdLife Finland (`https://atlas-api.2.rahtiapp.fi/api/v1`), CC BY 4.0. We parsed the per-square breeding class of 250 atlas species from the species maps (`/map/{taxonId}/atlas`). We took the activity category of the 3,859 squares from `/grid`. A cross-check against 498 squares from the per-square endpoint gave the same class for 50,076 of 50,173 records (99.8%; the API updates daily). The parsed snapshot is in `files/external_snapshot/`.
* **Temperature:** E-OBS v32.0e daily mean temperature (0.25°, 1950-01-01 to 2025-06-30), from the campaign shared store (`datasets/eobs-v32.0e-tg-ens-mean-0.25deg`, sha256 `b156cd2e...4f68290`). E-OBS terms permit only non-commercial research and education. Thus we do not include E-OBS values per square. We report only regional isotherm statistics (`files/results/isotherm_shifts.csv`). Annual and April-July means for atlas 4 use 2022-2024 only.

Hashes, URLs and retrieval times are in `files/provenance.json`.

## Methods

* **Species:** 233 species are public in atlas 3 and mapped in atlas 4; 224 of them have at least 20 occupied squares in atlas 3 and get a group. We matched names through a fixed list of taxonomic changes (`02_build_presence.py`). Common and Arctic Redpoll are merged, because atlas 4 lumps them. Secret or sensitive species are not in the public files and are not analysed.
* **Groups** (from atlas 3, all squares): "southern" if the northern margin is south of 7,500 km (YKJ N), n=74; "northern" if the southern margin is north of 7,000 km, n=14; the other 136 are "widespread". A species enters a pair only if it occupies at least 20 squares of the pair's square set in each atlas.
* **Margin:** mean YKJ north coordinate (km, square centre) of the 10 northernmost (or southernmost) occupied squares in the pair's square set. Rate = shift / (difference of atlas mid-years 1976.5, 1987.5, 2008.0, 2023.5).
* **Effort controls:** activity category ≥ 3 in both atlases (primary); ≥ 4; any surveyed square; all squares; probable/confirmed records only; per-square thinning of the richer atlas to the species count of the other atlas (lowest breeding category removed first, 20 random repeats); square sets balanced by detections of widespread species (`07_checks.py`).
* **Isotherm shift:** mean change of square temperature between the two windows divided by the north gradient of temperature. We estimated the gradient by least squares of the window-mean temperature on the north and east coordinates (about -0.0055 °C per km for May-June).
* **Uncertainty:** 5,000 bootstrap resamples of species. This does not include the spatial correlation of squares or the year-to-year noise of atlas coverage.

## Deviations from the plan

The plan fixed the primary metrics, groups, effort filter and predictions P1-P4. We added these analyses after we saw the results: the 10-year temperature windows (the atlas-year windows are 4-6 years and are noisy), the north-coast ceiling check, groups from atlas 2, margin sizes K=5 and K=20, and all checks that use widespread species as a detection calibrator. The detection result (point 2) comes from these added analyses and needs confirmation.

## Limitations

* The atlases differ in method and data channels. Atlas 4 uses many casual records from Tiira and the Vihko notebook. The activity categories use the same thresholds in atlases 3 and 4, but they did not equalise detection. We cannot separate a real decrease of common species from lower detection. Both can make the leading edge look slower and the trailing edge look faster.
* The widespread-species calibrator selects squares. The selected squares are fewer and not spatially random. The "at least as many" set over-corrects, and the "balanced" sets have fewer species and wider intervals.
* The number of northern species is small (13 in the primary analysis), and some have very large single-species effects.
* Our earlier-interval rates (3.5-5.0 km/yr) are higher than the 1.1-1.3 km/yr of Brommer et al. (2012). Their metric and effort correction were different. We did not reproduce their method exactly.
* We did not model habitat change, forestry, or population trends, which can also move range margins.

## Files

* `files/PREREGISTRATION.md` - plan written before the atlas-4 species data were downloaded.
* `files/code/` - `00_get_atlas123.sh`, `01b_get_atlas4_maps.py` (and the slower per-square `01_get_atlas4.py`), `02_build_presence.py`, `02b_crosscheck_atlas4.py`, `03_climate.py`, `04_shifts.py`, `05_repeat_forecast.py`, `06_figures.py`, `07_checks.py`, `run_all.sh`.
* `files/results/` - species-level margin tables for each effort variant, group summaries (`group_shift_summary.csv`), isotherm shifts, repeatability, forecast errors, robustness checks, species groups and name mapping, atlas-4 cross-check, per-square richness comparison.
* `files/figures/` - Fig. 1 margin rates and isotherm rates; Fig. 2 effort-filter sensitivity; Fig. 3 species rates 1974-79 → 2006-10 vs 2006-10 → 2022-25; Fig. 4 survey activity maps of the four atlases; Fig. 5 detection calibration.
* `files/external_snapshot/` - atlas-4 snapshot of 2026-11-09 (third-party data, CC BY 4.0; see `NOTICE.md`).

## Reproduce

```bash
mkdir scratch && cd scratch          # never write into the signed draft
EOBS=/path/to/tg_ens_mean_0.25deg_reg_v32.0e.nc bash ../files/code/run_all.sh
```

The atlas-4 API updates daily. To repeat the exact numbers, put `files/external_snapshot/finnish_atlas4_species_square_20261109.csv.gz` (unzipped as `raw/fin_atlas4/atlas4_species_square.csv`) and the grid and taxon lists in place of steps `01b` and the grid download. Python 3.12 with pandas, numpy, scipy, netCDF4, pyproj, pyarrow and matplotlib. `04_shifts.py` takes about 2 minutes.

## Attribution

Results of the 1st and 2nd Finnish bird atlas. Finnish Museum of Natural History, University of Helsinki. Used under CC BY 3.0. · Suomen III lintuatlas: Valkama J., Vepsäläinen V., Lehikoinen A., Luomus, CC BY 4.0. · Aineisto: Suomen 4. Lintuatlas. Luonnontieteellinen keskusmuseo Luomus ja BirdLife Suomi, CC BY 4.0. · We acknowledge the E-OBS dataset and the data providers in the ECA&D project (Cornes et al. 2018, doi:10.1029/2017JD028200).
