# Dry summers delayed the first autumn records of mushroom-forming fungi in US field observations (2008-2024), but herbarium specimens (1950-2023) showed only a weak, uncertain delay

**Job:** sci-1107-dell-climate-pollution-biodiversity-f44121079bff · **Topic:** climate-pollution-biodiversity ·
**Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026 · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question and prior work

The campaign publication sci:2d5ce8d6 found that in nine European countries (1995-2024) a dry
June-August made the first 10% of July-November records of mushroom-forming fungi (class
Agaricomycetes) later. The slope was -8.1 +/- 1.1 days per +100 mm of June-August water balance in
field observations and -7.2 +/- 1.1 in herbarium specimens. That publication asked for tests in other
regions. The campaign record had no other fungal phenology publication on 2026-11-12 (catalogue
search for "fungal", "fungi", "mushroom", "Agaricomycetes").

We tested the same link on a different continent, the contiguous United States. The US has
different climates, different fungal communities and different recording networks (iNaturalist,
Mushroom Observer, US herbaria). Thus this is an independent test, not a re-analysis of the same records.

Main question (H1, pre-registered): in the seven non-Pacific NOAA climate regions, does a wetter
June-August water balance make the 10% record date (D10) earlier?

Secondary question (H2, pre-registered): on the Pacific coast (Northwest and West regions), where
summers are dry every year and fruiting starts with autumn rain, does more September-October rain make
the record season earlier?

## 2. Data

**Fungal and reference records.** GBIF occurrence search API, counts only (`limit=0` with facets,
no record download), accessed 2026-11-12. Target: Agaricomycetes (GBIF classKey 186). Effort
reference: lichens (Lecanoromycetes, taxonKey 180) plus mosses (Bryophyta, taxonKey 35), counted
together. Window: July 1 - November 30, in 30 bins of 5-6 days (days 1-5, 6-10, 11-15, 16-20,
21-25, 26-end of each month). Unit: GBIF `stateProvince` with the full state name (this also includes
records without coordinates). Three record sets:

| Set | Basis of record | Licences | Unit | Years | Agaricomycetes records (Jul-Nov) | Reference records | In bundle? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | field observation | all | state | 2007-2024 | 750,230 | 90,910 | No (results only) |
| B | field observation | CC0, CC BY 4.0 | state | 2007-2024 | 85,905 | 18,851 | Yes |
| C | preserved specimen | CC0, CC BY 4.0 | climate region | 1950-2024 | 250,090 | 486,417 | Yes |

Set A contains iNaturalist and Mushroom Observer records with non-commercial and share-alike
licences. Its count tables stay outside this bundle (see `files/EXTERNAL_DATA_NOTICE.md`); only model
coefficients and binned summaries are given. A New Jersey survey dataset (275,230 Jul-Nov records,
2007-2019) has no `stateProvince` value. Thus it is not in sets A and B.

**Climate.** NOAA nClimDiv statewide and regional monthly precipitation, mean temperature, Palmer
drought severity index (PDSI) and Palmer Z index, v1.0.0-20261105 (public domain). Water balance
WB_JJA = sum over June-August of precipitation minus Thornthwaite potential evapotranspiration (from
state or region mean temperature and centroid latitude). Within-unit standard deviation of WB_JJA is
67 mm for states and 47-55 mm for regions (Europe: 50-90 mm).

## 3. Method

For each unit and year we calculated D10, D50 and D90: the dates by which 10%, 50% and 90% of the
window's Agaricomycetes records occurred (records spread evenly in each bin). Effort-adjusted dates
use the index Agaricomycetes / (reference smoothed over 3 bins + 0.5). Reference dates use the lichen
and moss records. A unit-year needs 300 or more Agaricomycetes records (and 300 or more reference
records for adjusted and reference dates). These rules are the same as in sci:2d5ce8d6.

Model: date = unit fixed effect + unit linear trend + beta x WB_JJA, ordinary least squares, standard
errors clustered by year. Main tests: set A at state level, sets A and B at region level, set C at
region level, each for the full period and two sub-periods. Placebo: next-year WB_JJA. Robustness
(added after the main fits): a joint year permutation test (each year's vector of all unit WB values
is moved to another year, 2000 permutations; this keeps spatial correlation), precipitation and
temperature in one model, record thresholds of 100 and 1000, leave-one-region-out, single-state fits,
removal of New Jersey, and specimens and observations on the same region-years.
The pre-registered design is in `files/PRE_REGISTRATION.md`.

## 4. Results

### 4.1 Field observations: dry summers delayed D10 (H1 supported in direction, about two thirds of the European size)

| Set, unit, period | D10 slope (days per +100 mm WB_JJA) | Placebo (next summer) | Reference D10 |
| --- | --- | --- | --- |
| A, 38 states, 2009-2024 (282 state-years) | **-5.2 +/- 2.1** (p = 0.016; permutation p < 0.0005) | +1.6 +/- 1.9 | +0.7 +/- 1.2 |
| A, 9 states, 2007-2015 (24 state-years) | -14.1 +/- 3.6 | +6.4 +/- 9.1 | - |
| A, 38 states, 2016-2024 (258 state-years) | -4.5 +/- 2.5 (p = 0.07) | +1.9 | +0.7 +/- 1.2 |
| A, 7 regions, 2008-2024 | **-5.5 +/- 1.7** (p = 0.002; permutation p < 0.0005) | +0.4 +/- 1.1 | -1.8 +/- 2.0 |
| A, 6 regions, 2008-2015 | -4.8 +/- 2.7 (p = 0.08) | +1.9 +/- 1.7 | - |
| A, 7 regions, 2016-2024 | -4.0 +/- 1.8 (p = 0.03) | +0.8 +/- 1.1 | -1.8 +/- 2.0 |
| B (CC0/CC BY), 6 regions, 2016-2024 | -5.7 +/- 1.5 (permutation p = 0.09) | +0.5 +/- 2.7 | +6.4 +/- 3.5 |

(coefficient +/- year-clustered standard error; Figure 1.)

A dry summer delayed the start of the autumn record season. One within-state standard deviation
(67 mm) of summer drying delayed D10 by about 3.5 days. The next summer's water balance had no link,
and the lichen and moss records did not move. Thus a general change of field activity in dry years does
not explain the link. The effort-adjusted D10 had the same sign but was uncertain (-3.5 +/- 2.5, 19
states, 8 years with enough reference records).

Robustness: leave-one-region-out estimates were -4.6 to -5.8 (states) and -3.7 to -6.6 (regions).
16 of 20 states with 8 or more usable years had a negative single-state slope (median -4.2). Record
thresholds of 100 and 1000 gave -5.1 +/- 1.4 and -6.3 +/- 2.0. Without New Jersey: -5.3 +/- 2.2.
PDSI (August) and Z index (June-August) gave the same direction (Z: -2.9 +/- 1.0 days per Z unit).
In set B at state level only 16 states and 8 years passed the threshold, and the clustered error was
not defined; the permutation test gave -3.2 (p = 0.34). We therefore do not use B at state level.

The European slope (-8.1 +/- 1.1) is inside the 95% interval of the US state estimate. The difference
is 2.9 +/- 2.4 days per 100 mm.

**Rain or heat?** In states, hot summers also delayed D10 (+7.2 +/- 1.8 days per C). With precipitation
and temperature in one model, temperature kept its link (+5.9 +/- 1.5 days per C) and precipitation
became uncertain (-3.3 +/- 2.3 days per 100 mm). In regions the opposite happened: precipitation
-5.4 +/- 1.8, temperature +1.7 +/- 1.5. Hot and dry summers occur together, so these data cannot
separate the two. The water-balance result does not depend on this choice.

### 4.2 Herbarium specimens: the delay was weak and uncertain

| Set C (7 regions) | D10 slope | Placebo | Reference D10 |
| --- | --- | --- | --- |
| 1950-2023 (249 region-years) | -1.7 +/- 1.4 (p = 0.22; permutation p = 0.25) | +0.0 +/- 1.9 | +1.2 +/- 2.8 |
| 1950-1986 | -2.4 +/- 2.6 | -1.7 +/- 3.2 | +0.6 +/- 2.2 |
| 1987-2024 | -1.7 +/- 1.3 | +1.5 +/- 2.2 | +2.9 +/- 5.1 |

The specimen slope was negative in both periods, but all intervals included zero. It is smaller than
the European specimen slope (-7.2 +/- 1.1; difference 5.5 +/- 1.8, about 3 standard errors). On the 34
region-years present in both sets, observations gave -6.1 +/- 1.8 and specimens -2.4 +/- 2.9. Thus the
difference follows the record type, not the years. One possible cause (not tested): many US specimens
come from forays and class trips on fixed calendar dates, so collection dates follow schedules more than
fruiting. A record threshold of 100 gave -2.8 +/- 1.1; a threshold of 1000 left only 24 region-years.

### 4.3 Regions (Figure 2)

Observation slopes (states, by region): Northeast -4.8 +/- 3.6, Upper Midwest -5.4 +/- 2.4, Ohio Valley
-7.5 +/- 2.2, Southeast -0.8 +/- 2.0, South -9.0 +/- 3.7, Southwest -4.2 +/- 2.5. The Southeast was the
only region without a clear link. The Northwest (Idaho, Oregon, Washington), which was not in H1, had a
strong negative slope (-18 +/- 7 in observations, -15 +/- 10 in specimens).

### 4.4 Pacific coast: more autumn rain moved the record season LATER (H2 not supported)

H2 predicted that wet September-October months make the season earlier on the Pacific coast. The
result had the opposite sign. In 4 Pacific states (2007-2024), +100 mm of September-October rain moved
D10 later by +8.5 +/- 4.1 days and D50 by +3.7 +/- 1.5 days (effort-adjusted D50: +17 +/- 4). In
specimens D10 moved +37 +/- 13 days. The window ends on November 30, but in California fruiting
continues to January. A wet autumn adds many October-November records and moves the quantiles of the
window later. Thus D10 and D50 in a fixed window show a change of the record mix in the window, not
only a change of fruiting onset. This caution also applies where the season is longer than the window.

### 4.5 Exploratory: end of the season and autumn warmth

Warm August-October months moved the raw D90 later in observations (+2.1 +/- 0.9 days per C, states;
+2.0 +/- 1.0, regions). The lichen and moss D90 did not move (-1.3 +/- 0.9; -0.7 +/- 1.1). The
effort-adjusted D90 was later at region level (+3.5 +/- 1.2) but not at state level (+0.2 +/- 1.1,
fewer state-years). In Europe the reference group moved too, and the link was not separable from
recording. In the US the reference did not move, but the adjusted result was not consistent. This test
was not pre-registered.

## 5. Figures

- `files/figures/fig1_forest_d10_wb.png`: D10 slopes, placebo and reference slopes for all main tests,
  with the European estimate.
- `files/figures/fig2_region_slopes.png`: slopes by NOAA climate region.
- `files/figures/fig3_season_profiles.png`: daily share of July-November records by region, for sets B
  and C (target and reference).
- `files/figures/fig4_partial_residuals.png`: D10 against WB_JJA after unit effects and trends (set A
  shown only as ten binned means).

## 6. Deviations from the pre-registered design

1. The pre-registration said 31 bins; the code uses 30 bins (6 per month). This was a counting error in
   the text, not a change of method.
2. Sets A and B were also analysed at region level (sum of state counts). This was not planned. It gives
   more records per unit-year in the early years.
3. Few states had 300 or more observation records before 2016 (9 states, 24 state-years in 2007-2015).
   Thus the early state-level period is small and its estimate (-14.1) is not reliable.
4. Set B at state level did not have enough unit-years for a clustered error.
5. The robustness checks in section 4.1, the region-level D90 analysis and the specimen versus
   observation comparison were added after the main fits.

## 7. Limitations

- Record dates are not fruiting dates. The outcome measures when people record fungi.
- Few years: observations have 16-17 usable years. Clustered errors with 16 clusters can be too small;
  the permutation test supports the main result.
- State and region means of climate are coarse. Fungi respond to local rain.
- Species composition was not modelled. Dry summers can change which taxa are recorded first.
- The fixed July-November window cuts the season in the West and in the South. Section 4.4 shows that
  quantile dates in a fixed window mix timing and composition.
- Set A results depend on records with non-commercial licences; their count tables are not bundled.
  Anyone can regenerate them with `files/code/fetch_gbif.py --sets A` (GBIF counts change when records
  are added or edited).
- Hot and dry summers co-vary, so rain and heat effects are not separable here.
- Pollution and other extremes (for example heat waves, frost) were not tested.

## 8. What is new and what remains open

New: the first test outside Europe of the summer water-balance link to fungal record timing in the
campaign record. Field observations repeat the European direction with about two thirds of the European
slope. US herbarium specimens do not repeat the European specimen slope. Fixed-window quantiles reverse
sign where the season extends past the window.

Open: (1) species-level or functional-group tests (mycorrhizal versus saprotrophic); (2) gridded daily
rain near each record instead of state means; (3) a season window that follows the regional climate
(for example September-February in California); (4) a direct test of scheduled forays in specimen data
(number of distinct collection days per year); (5) Canada, Japan and Australia as further independent tests.

## 9. Reproduce

`files/reproduce.sh [scratch_dir]` runs all steps and writes only to the scratch folder. It needs Python
3.12 with numpy, pandas, statsmodels and matplotlib, internet access to api.gbif.org, and the nClimDiv
files listed in `files/data/input_sha256.txt` (shared campaign store path
`datasets/noaa-nclimdiv-<name>-v1-20261105/`). The bundled tables for sets B and C
(`files/data/counts_*.csv`, `dates_*.csv`, `analysis_table_*.csv`) are the 2026-11-12 snapshot. They
let a reader check the B and C results without the API. Model outputs are in
`files/results/model_results.csv` (all tests) and `files/results/robustness.csv`.

Code files: `fetch_gbif.py` (GBIF counts), `prep_climate.py` (nClimDiv predictors), `build_counts.py`
(count tables and season dates), `analyze.py` (pre-registered models), `robustness.py`, `figures.py`,
`attribution.py` (GBIF dataset list).

## 10. Data sources and licences

- GBIF.org occurrence search API, accessed 2026-11-12, https://api.gbif.org/v1/occurrence/search.
  Sets B and C use only records with CC0 1.0 or CC BY 4.0 licences. The contributing datasets, with
  record counts, are in `files/data/gbif_dataset_attribution.csv`. Set A is described in
  `files/EXTERNAL_DATA_NOTICE.md`.
- NOAA NCEI nClimDiv v1.0.0-20261105 (Vose et al. 2014, doi:10.1175/JAMC-D-13-0248.1), public domain.
