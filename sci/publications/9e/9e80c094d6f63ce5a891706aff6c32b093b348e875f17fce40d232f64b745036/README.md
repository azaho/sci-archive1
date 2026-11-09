# Wood Thrush counts did not increase where acid wet deposition decreased most on eastern US Breeding Bird Survey routes, 1987-2025

## Summary

Hames et al. (2002, PNAS, doi:10.1073/pnas.172700199) found a lower probability of Wood Thrush
(*Hylocichla mustelina*) breeding in areas with high acid wet deposition. The effect was stronger at
high elevation and on low-pH soils. The proposed mechanism is soil calcium loss. After 1990, US
sulfate emissions decreased because of the Clean Air Act. At the eastern US Breeding Bird Survey
(BBS) routes in this study, the median wet sulfate (SO4) deposition decreased from 19 to 5 kg/ha/yr
between 1985-1994 and 2016-2025.

We did a test of one prediction of the acid-deposition hypothesis. If acid deposition limits Wood
Thrush abundance, Wood Thrush counts must increase most on the routes where deposition decreased
most. The increase must also be larger than that of other forest birds.

The data did not agree with this prediction:

- **Main model (1987-2025, 1,850 routes, 39,856 route-years).** Wood Thrush counts changed by
  **+10.7% per +10 kg/ha/yr wet SO4** (95% CI +2.2% to +20.0%). This is the opposite sign to the
  prediction. A within-BCR permutation of the route deposition histories gave a two-sided p = 0.028
  (210 permutations). The permutation null had mean -0.001 and SD 0.042. The clustered SE was 0.041.
- **Comparison with other forest birds.** The Wood Thrush estimate was at the 77th percentile of
  64 other AVONET "Forest" species (the median species was -2.8%). Thus the Wood Thrush result is
  not unusual. It does not show a Wood-Thrush-specific benefit from cleaner air.
- **Robustness.** The sign stayed positive or near zero in all model variants. With route-specific
  linear trends removed, the estimate was +2.2% (-4.7% to +9.7%). This most conservative model
  permits a recovery of at most about 5% per 10 kg/ha/yr decrease in SO4.
- **Long-term trends.** In 1966-1998, Wood Thrush route trends were *more positive* where 1985-1994
  SO4 deposition was higher. This is opposite to the trend link that Hames et al. described. In
  1999-2025, this trend contrast was slightly negative and uncertain. The recovery prediction was
  that the 1999-2025 contrast is higher than the 1966-1998 contrast. The data showed the opposite.
- **Elevation.** The SO4 effect on Wood Thrush did not change with route elevation (interaction
  +0.016, SE 0.030).
- **Other focal species.** Veery, Hermit Thrush and Ovenbird (forest-floor invertebrate foragers
  that other studies propose as calcium-sensitive) showed no consistent recovery. Ovenbird had a
  more negative SO4 effect at higher elevation (interaction -0.103, SE 0.028). But 15 of 68 species
  had an elevation interaction with |z| > 1.96, so this result is not specific to Ovenbird.

**Conclusion.** In BBS route counts, we found no sign that Wood Thrush numbers recovered where acid
deposition decreased most. This does not show that acid deposition had no effect on Wood Thrush.
Soil calcium can stay low for decades after deposition decreases, and the BBS cannot measure
breeding attempts at forest sites (the Hames et al. response variable). The result shows that the
spatial pattern of Wood Thrush population change since 1987 does not follow the spatial pattern of
the acid-deposition decrease.

## Question and scope

- Tested scope: 2,496 BBS routes in the contiguous US east of 100 W, 1966-2025 (BBS 2026 release);
  NADP NTN annual gradient grids, 1985-2025. Canadian routes are not included because the NADP
  grids cover the contiguous US only.
- Main assumption: within one Bird Conservation Region (BCR) and year, routes with a larger
  deposition decrease are otherwise comparable after route-observer fixed effects. Regional changes
  that are common to a BCR (weather, regional habitat change, regional detection change) are
  removed by BCR x year fixed effects.

## Data

| Source | Version | Use |
| --- | --- | --- |
| BBS States.zip 10-stop summaries | 2026 release, 1966-2025, doi:10.5066/P144YU3S | Route totals per species |
| BBS Weather.csv, Routes.csv, SpeciesList.csv | same release | Run quality (RunType), observer, route location and BCR |
| NADP NTN gradient grids `SO4_dep_YYYY`, `NO3_dep_YYYY` | 1985-2025, downloaded 2026-11-08 | Annual wet deposition (kg/ha/yr) |
| OpenTopoData SRTM 90 m | public API, 2026-11-08 | Route-start elevation |
| AVONET (Tobias et al. 2022) via campaign bundle 15270e89 | `species_traits_avonet.csv` | Habitat = Forest species set |

Shared campaign dataset paths (staged with `campaign-dataset`, sha256 of the files used):

- `datasets/bbs-2026-release-states-6a0b0b0a/States.zip` sha256 `568053a412e42f2974642d1961956174e8eaad6bc85c278ef50d6191cc56adcf`
- `datasets/bbs-2026-release-weather-6a0b0b0a/Weather.csv` sha256 `4bcdb3346dcc44839690702f76c10306a19329260e99e16576b1a92f4465f67d`
- `datasets/bbs-2026-release-routes-6a0b0b0a/Routes.csv` sha256 `8ac35620930b0bc758ed3fcb33c689ebe08840edd04f840050b13dd1a56e8362`
- `datasets/bbs-2026-release-specieslist-6a0b0b0a/SpeciesList.csv` sha256 `e54e4b5b1eb6fc5fc5941a8e31876ecc17675f229265f60c4dbfed742fb35274`
- `datasets/bbs-2026-release-50stopdata-6a0b0b0a/50-StopData.zip` sha256 `eed5fc264a1af6074783685de96b433b1d5ce4a1f8e09528449dbd4f9ba03204` (downloaded, then not used; see Deviations)

Source URLs are in `files/data/shared_dataset_provenance.jsonl`. The NADP grid ZIP hashes are in
`files/data/nadp_grid_sha256.txt`; the URL pattern is
`https://nadp.slh.wisc.edu/filelib/maps/NTN/grids/<YEAR>/<VAR>_<YEAR>.zip`. The NADP server
closed connections under parallel requests; a browser User-Agent and sequential retries worked.

## Methods

1. **Counts** (`01_bbs_totals.py`, `04_panel.py`). Route totals (`SpeciesTotal`) from the 10-stop
   summaries. Runs: US, RPID 101, RunType 1, east of 100 W (74,239 runs, 2,496 routes, 5,808
   observers). A species' range is the set of routes where it was found in 2 or more years. Inside
   its range, a run without a record is a zero count. Species: all AVONET habitat "Forest" species
   with 150 or more range routes (68 species; `files/data/species_set.csv`).
2. **Exposure** (`02_nadp_routes.py`). Mean grid value within 15 km of the route start point (only
   start coordinates are public; a route is about 39 km long). Exposure = 3-year trailing mean
   (t-2 to t), in units of 10 kg/ha/yr.
3. **Models** (`05_models.py`, pyfixest 0.70 `fepois`, LSMR demeaner, SE clustered by route). The
   main model (P1) is
   `count ~ SO4_3yr + first_year_of_observer_on_route | route-observer + BCR x year`, 1987-2025.
   Variants: P1_early (1987-2005), P1_late (2006-2025), P1_regA (Appalachian-Northeast BCRs 12, 13,
   14, 28, 30), P1_regB (other eastern BCRs), P1_trend (exposure residualized on route-specific
   linear time trends), P1_nstops (response = number of 10-stop segments with a record, 0-5),
   P1_NO3 (wet NO3 in place of SO4), P4_elev (adds SO4 x elevation). P3_pre and P3_post use
   `(year - centre)/10 x baseline SO4 (1985-1994 mean)` for 1966-1998 and 1999-2025.
   P0_base and P0_late (added after the main results) are cross-sectional:
   counts in 1985-1994 or 2016-2025 on baseline SO4 + elevation + elevation^2 | BCR x year.
4. **Reference distribution** (`07_summary.py`). Each focal estimate is ranked among the 64
   non-focal forest species fitted with the same model.
5. **Permutation** (`08_perm.py`). For Wood Thrush P1, each route received the complete SO4 history
   of a random route in the same BCR (210 draws, 6 seeds).
6. **Descriptive time bins** (`06_event_bins.py`). Routes were put in tertiles of the
   1985-1994 to 2016-2025 SO4 decrease, measured relative to their BCR mean. The model gives the
   log count ratio of high- to low-decrease routes in 5-year bins (reference 1986-1990), with
   route-observer and BCR x year fixed effects.

The analysis plan (`files/PLAN.md`) was written before the outcome models were fitted. It records
the decision rule and the later additions.

## Results

Wood Thrush estimates (log count change per +10 kg/ha/yr of wet SO4; positive = more birds where
deposition is higher = no recovery where deposition fell):

| Model | Estimate | 95% CI | Route-years / routes | Percentile among 64 forest species |
| --- | --- | --- | --- | --- |
| P1 main 1987-2025 | +0.102 | +0.022, +0.182 | 39,856 / 1,850 | 77 |
| P1 1987-2005 | +0.104 | +0.028, +0.181 | 19,011 / 1,688 | 75 |
| P1 2006-2025 | +0.125 | -0.016, +0.265 | 20,138 / 1,660 | 83 |
| P1 Appalachian-NE BCRs | +0.032 | -0.057, +0.122 | 17,724 / 784 | 65 |
| P1 other eastern BCRs | +0.230 | +0.077, +0.384 | 22,132 / 1,066 | 77 |
| P1 route trends removed | +0.022 | -0.048, +0.092 | 39,856 / 1,850 | 67 |
| P1 segments with a record | +0.077 | +0.024, +0.129 | 39,856 / 1,850 | 75 |
| P1 wet NO3 in place of SO4 | +0.220 | +0.102, +0.339 | 39,856 / 1,850 | 80 |
| P3 trend x baseline SO4, 1966-1998 | +0.157 | +0.088, +0.227 | 27,301 / 1,648 | 75 |
| P3 trend x baseline SO4, 1999-2025 | -0.044 | -0.107, +0.019 | 27,701 / 1,716 | 31 |

The P3 units are log change per decade per 10 kg/ha/yr of baseline SO4.
For all focal species and models, see `files/results/focal_summary.csv`. For all species, see
`files/results/all_species_estimates.csv`.

The time bins (Figure 3) show the timing. Before 1986-1990, Wood Thrush counts increased on the
high-decrease routes relative to the low-decrease routes. After 2005, when deposition decreased
fastest, the Wood Thrush counts on the high-decrease routes decreased relative to the
low-decrease routes (2021-2025 log ratio -0.28, SE 0.10). Veery and Hermit Thrush increased
relative to the low-decrease routes after 1990, but the intervals are wide. In the models, Veery
and Hermit Thrush had no clear SO4 effect for 1987-2025. Only Hermit Thrush in 2006-2025 had a
clear negative estimate, which is the sign that a recovery predicts (-0.79, CI -1.23 to -0.36,
8th percentile of the reference species). This result did not repeat in 1987-2005 (+0.07).

The cross-sectional P0 models gave higher Wood Thrush counts at routes with higher baseline
SO4 (+0.47 in 1985-1994 and +0.45 in 2016-2025). This shows that the core Wood Thrush range
(Appalachians) is also the high-deposition area. The BBS cannot remove this range effect as the
site-level design of Hames et al. did. Thus P0 is not a valid replication of the Hames et al.
cross-sectional result, and we do not use it as evidence for or against that result.

## Figures

- `files/figures/fig1_deposition.png`: wet SO4 at routes in 1985-1994 and 2016-2025, the
  within-BCR decrease used for tertiles, and the route median series.
- `files/figures/fig2_species_estimates.png`: focal species estimates (95% CI) against 64 other
  forest species for 8 model variants (gray points clipped at +-1.5).
- `files/figures/fig3_high_vs_low_decline_bins.png`: high- versus low-decrease route count ratios
  by 5-year bin.
- `files/figures/fig4_permutation_null.png`: within-BCR permutation null for Wood Thrush.

## Observation bias and limitations

- **Observer and detection effects.** Route-observer fixed effects and a first-year term control
  for observer differences and for the first-year effect. BCR x year fixed effects remove regional
  year effects (such as weather and regional changes in detection). The comparison with other forest
  species tests for survey artefacts that are common to all species. But detection changes that
  are specific to Wood Thrush and that correlate with deposition within a BCR are not controlled.
- **Exposure error.** The grids are interpolated from about 250 NTN sites. We sample them near the
  route start point only. Only wet deposition is used; dry deposition and soil calcium are not
  measured. Soil base-cation recovery can be slow, so a delayed bird recovery is possible beyond 2025.
- **Confounding.** The deposition decrease correlates with the baseline level (r = 0.97), with
  latitude and with the Ohio Valley-Appalachian region. Other changes in these areas (forest
  maturation, deer browsing, warming, land use) can cause a positive or negative bias. The
  route-trend model removes linear differences, and its result (+0.022, CI -0.048 to +0.092) is
  close to zero.
- **Response variable.** BBS counts measure relative abundance of singing birds along roads. They
  do not measure breeding attempts or productivity. Hames et al. used playback at forest sites.
- **Multiple tests.** We fitted 13 model variants for 4 focal species and 64 reference species.
  We report all estimates. The secondary focal-species results (Hermit Thrush in 2006-2025, the
  Ovenbird elevation interaction) come from one sub-period or one interaction among many tests and
  did not repeat in the other period or across model variants. We treat them as exploratory.
- **Model fit.** The 1987-2025 models use the 3-year exposure mean, so 1987 is the first year.
  The P1_trend model uses residualized exposure (Frisch-Waugh step on the linear predictor). This is
  an approximation for a Poisson model.

## Deviations from the plan

- The first panel used the 50-stop file. This file has data mainly from 1997 onward, so earlier
  runs became false zeros. We found this in a sanity check. We discarded those fits (a few estimates
  were seen, including Wood Thrush P1 +0.04, SE 0.05) and rebuilt the panel from the 10-stop
  summaries before any of the reported fits.
- The P0 cross-sectional models were added after the main results were seen.
- Route elevation came from OpenTopoData SRTM 90 m because the USGS EPQS service was too slow
  (about 6-10 s per point). For 107 routes, both sources were available and agreed (r = 0.9994,
  median absolute difference 3.8 m).

## Reproduction

```
# Python 3.12 with pandas, numpy, rasterio, pyproj, matplotlib; pyfixest 0.70 in a private venv
python3 files/code/01_bbs_totals.py        # needs datasets/bbs-2026-release-states-6a0b0b0a
python3 files/code/04_panel.py             # also uses species_traits_avonet.csv (in files/data)
python3 files/code/02_nadp_routes.py       # needs NADP grid ZIPs in work/raw/nadp (URL pattern above)
python3 files/code/03_route_elevation.py   # OpenTopoData API
python  files/code/05_models.py P1         # and the other model names listed in the script
python  files/code/06_event_bins.py
python  files/code/08_perm.py 7550 <seed> 35   # seeds 1-6
python3 files/code/07_summary.py
python3 files/code/09_figures.py
```

The scripts use paths relative to the worktree (`work/...`, `datasets/...`). The bundle includes the
derived inputs needed to refit the models without new downloads: `files/data/panel_forest_east.parquet`
(zero-filled route-year counts for the 68 species), `files/data/runs_east.csv.gz`,
`files/data/nadp_route_year.csv.gz` (route x year SO4, NO3 and Ca wet deposition) and
`files/data/route_elevation.csv`.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-climate-pollution-biodiversity-6c499294d78f, topic
  climate-pollution-biodiversity, machine dell, account claude-andrii, model Claude Opus 5.5
  (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Related campaign work: BBS ozone studies (for example 2603c41c) and the BBS wildfire smoke
  study (64f2d048) tested other air-pollution links; the AVONET table is reused from 15270e89.
