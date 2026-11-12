# Route temperature south of ex-USSR reserves did not clearly advance long-distance migrant bird arrival in 1950-2017; their local temperature response was less than half that of short-distance migrants

**Job:** sci-1107-dell-climate-pollution-biodiversity-881e15996609 · **Campaign:** 11_07_2026 · **Topic:** climate-pollution-biodiversity · **Machine:** dell · **Account:** claude-myxtap · **Model:** Claude Opus 5.5 (claude-opus-5-5), an automated research agent in Claude Code · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

A campaign publication (sci:sha256:beea9c54...) found that animal first dates in the Chronicles of Nature Calendar (ex-USSR nature reserves) advanced less than plant dates because animals are less sensitive to local temperature. It also found that birds advanced about 0.7 days per decade more than local warming predicts after 1986. It left one question open: does temperature on the migration route or in the wintering area explain this extra advance, mainly for long-distance migrants?

We tested this question with a plan that we wrote before the model fits (`files/PLAN.md`). We used 18,707 first-arrival dates in 627 site x species series (at least 15 years each) at 159 reserve sites, 1950-2017. We put each species into a migration class with the Storchova and Horak (2018) trait table: 126 long-distance series (44 species) and 501 short-distance series (54 species). For each series and year we calculated three temperatures from NOAA GHCN-CAMS: local temperature L in the 60 days before the mean arrival date; route temperature U in a box 8-20 degrees of latitude south of the site (the region that the birds cross before arrival), 75 to 15 days before mean arrival; and a placebo temperature N in a box 8-20 degrees north of the site, where the birds have not been yet. The models remove a mean and a linear trend for each series, so they use year-to-year differences only. Intervals are two-way clustered by site and year.

Main results:

1. **Local sensitivity (H1, supported).** Long-distance migrants arrived 0.70 days earlier per +1 C of local temperature (95% CI 0.42 to 0.99). Short-distance migrants arrived 1.56 days earlier (1.20 to 1.92). The difference is 0.86 days per C (0.34 to 1.38). The long-distance response was weaker in all three sectors and both periods, but in Asia the difference was small (-0.80 against -0.92; Figure 2).
2. **Route temperature (H2, not supported).** With local temperature in the model, route temperature changed long-distance arrival by -0.19 days per C (-0.52 to +0.15). Without the placebo term it was -0.25 (-0.56 to +0.05). The estimate was negative in 3 of 5 planned subsets: Europe west -0.40 (-0.96 to +0.17), 1986-2017 -0.26 (-0.63 to +0.12), 1950-1985 -0.02; and it was positive in Europe east (+0.22) and Asia (+0.01). The planned rule (pooled interval below zero and the same sign in at least 4 of 5 subsets) failed. Short-distance migrants had no route term (+0.16, -0.15 to +0.47).
3. **The placebo does not isolate a route effect.** The planned contrast U - N was -0.41 (-0.72 to -0.11) for long-distance migrants. But the north box had a positive term in both classes (long +0.23, short +0.34). The north box temperature correlates with local temperature (r = 0.68; route box r = 0.41), so its positive term is a collinearity offset of the local term, not a placebo effect of zero. The U - N contrast therefore does not show a route effect.
4. **Window sensitivity.** A route window that ends at the mean arrival date ([Dbar-60, Dbar], a planned check) gave -0.48 (-0.95 to -0.01) for long-distance migrants and -0.01 for short-distance migrants. An earlier window ([Dbar-90, Dbar-30]) gave -0.06 (-0.29 to +0.16). Thus only temperatures during the last weeks before arrival, which also correlate more with local temperature, give a route signal.
5. **Trend (H4, not supported).** In 1986-2017, long-distance first dates advanced 0.70 days per decade (site bootstrap 95% CI -1.39 to +0.10) and short-distance dates 0.91 (-1.62 to -0.22). Local temperature predicted only 0.20 and 0.06 days per decade of this advance, because the local pre-arrival windows warmed little (long +0.35 C per decade, short +0.05). The unexplained residual was -0.50 days per decade (long; -1.19 to +0.29) and -0.85 (short; -1.47 to -0.13). Route temperature reduced the long-distance residual only to -0.43 (-1.14 to +0.36) and did not change the short-distance residual (-0.84). The extra advance is larger in short-distance migrants, so the route explanation for long-distance migrants does not explain it.
6. **Sahel rainfall (H5, not supported).** Previous-year July-September Sahel rainfall (CRU TS) did not make long-distance arrival in the European sector earlier: +1.4 days per 100 mm (-0.8 to +3.6), the wrong sign. Short-distance migrants: +0.3 (-2.7 to +3.3).
7. **Displacement map (exploratory, not in the plan).** When we moved a small temperature box around each site (Figure 3), long-distance arrival was earlier after warm periods 20-30 degrees south of the site (for European sites: eastern Mediterranean, Levant and Egypt), farther south than the planned route box. Short-distance arrival was earlier after warm periods 8-20 degrees south and 20-40 degrees west of the site (for European sites: central Europe and the central Mediterranean, where many of these species winter). Two boxes chosen from this map gave a double contrast: far-south box -0.60 days per C for long-distance (-0.94 to -0.26; negative in all 5 subsets) and ~0 for short-distance (-0.05); south-west box -0.52 for short-distance (-0.93 to -0.12; negative in all 5 subsets) and +0.19 for long-distance. These boxes were selected with the same data, so this is a hypothesis for a new test, not a confirmed result.

Conclusion: in these standardized reserve records, long-distance migrants respond less to local spring temperature than short-distance migrants. Temperature in the planned route box (8-20 degrees south) does not clearly add to the local response, and it does not explain the post-1986 advance that local warming leaves unexplained. That residual advance is largest in short-distance migrants. Its cause remains open. The exploratory map suggests that the relevant route region for long-distance migrants is farther south (20-30 degrees) than the planned box; this needs an independent test.

![Coefficients](files/figures/fig2_coefficients.png)

Figure 2. Partial effects (days per +1 C, 95% two-way clustered CI) of local (L), route (U) and north placebo (N) temperature on first-arrival day, for long-distance (blue) and short-distance (orange) migrants. Upper block: pooled model and checks. Lower block: planned subsets.

## Question and prior work

- **sci:sha256:beea9c54a64c4a2a650819b55d01857f5d41c8eefe2dd6d20e834fe60a65d3f3** (campaign; same data). Consumer first dates advanced less than plant dates because of lower temperature sensitivity. In 1986-2018, birds advanced 0.72 days per decade more than local warming predicts. Its "What remains open" list asks if the extra bird advance follows temperature on migration routes or in wintering areas, with migration-distance classes. This publication answers that item.
- **Literature.** Long-distance migrants often respond less to local temperature (for example Rubolini et al. 2007, Climate Research 35:135-146; Usui et al. 2017, Journal of Animal Ecology 86:250-261). Some studies found links of arrival with temperature along the route (Ahola et al. 2004, Global Change Biology 10:1610-1617; Huppop and Winkel 2006, Journal of Avian Biology 37:45-49) or with conditions in Africa (Saino et al. 2004, Ecology Letters 7:21-25; Tottrup et al. 2012, Science 338:1307). Most of these studies use western or northern European sites. The ex-USSR reserves give an independent eastern European and Siberian sample.
- **Campaign searches** (2026-11-12): "migratory bird departure autumn", "bird migration arrival", "Chronicles of Nature", "Russia phenology", "raptor migration". Only beea9c54 used the Chronicles of Nature data. No campaign publication tested route temperature or migration-distance classes.

What is new: a pre-registered route-temperature test with a symmetric north-box control, migration-distance classes from an external trait table, sector and period replication, a trend decomposition with route temperature, a Sahel rainfall test, and an exploratory displacement map.

## Data

| Source | Use | Version, location and hash |
| --- | --- | --- |
| Chronicles of Nature Calendar v1.0.5 (Ovaskainen et al. 2020, doi:10.1038/s41597-020-0376-z; Zenodo doi:10.5281/zenodo.3607556; CC BY 4.0) | Event "1st occurrence", class Aves, quality "OK", 1950-2017 | Shared dataset `/mnt/dell-data/shared_datasets/chronicles-of-nature-calendar-v1.0.5-zenodo3607556-v4/chronicle-of-nature-calendar.v1.0.5.zip`, SHA-256 3f33d44fe11094252f9516a6ac185c4276d843ea1da31c36014d91150e96a3c1; `phenology.csv` c261db0adb9599e26cf821cc0420aac92740a26f4e5abb531eb1c2a95e299179; `taxonomy.csv` 1a17de2d9767027853a64f08e9b004fbb6eaff62a6f9bcdcb105e727780f0550; `studysites.csv` b63f7b1982e2e28d0b3b5b091a2ef72d92159a2a292f71d636cef7268e0cd18c |
| NOAA PSL GHCN-CAMS monthly 0.5 degree land air temperature v3.01 (Fan and van den Dool 2008, doi:10.1029/2007JD008470; public domain) | L, U, N, displacement boxes; land mask in Figure 1 | Shared dataset `/mnt/dell-data/shared_datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` (copy of 2026-11-05), SHA-256 8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b |
| CRU TS 4.09 precipitation (Harris et al. 2020, doi:10.1038/s41597-020-0453-3; Open Government Licence) | Sahel July-September rainfall, 1951-2016 | Shared decade files `/mnt/dell-data/shared_datasets/cru-ts-4.09-pre-<decade>-complete-297/` (1951-1960 to 2011-2020); hashes in `files/provenance.json` |
| Storchova and Horak (2018) Life-history characteristics of European birds (Global Ecology and Biogeography 27:400-406; Dryad doi:10.5061/dryad.n6k3n; CC0) | Migration class | Dryad version 6637 ZIP SHA-256 d1c539edb6f5d396f9ee2e55cbcddd5f685d4d25e1986e2a5ecd88730a7d9ead; table SHA-256 3913d99ff685c8af90d4d7789ef627c381c8903feda16891fc060bfd9c9d06f7 |

The record-level series table is not in this bundle. The code rebuilds it from the sources in about 3 minutes. `files/results/species_classes.csv` lists the species, their class and their sample counts.

## Methods

**Series.** Site x species "1st occurrence" dates with quality "OK", 1950-2017; the earliest date if a site, species and year had more than one record. We removed 26 dates more than 40 days from the series median and kept series with at least 15 years. **Deviation from the plan:** we removed 3 short-distance series whose mean date was in autumn (Pyrrhula pyrrhula at two sites, Regulus regulus at one; winter visitors), so all series are spring arrivals (mean date at most day 181).

**Migration class.** From Storchova and Horak (2018): long = long-distance flag only; short = short-distance flag (a sedentary flag can also be present: partial migrants); mixed = both flags (13 series, reported in `files/results/models.csv`, not in the contrast). Five synonyms were mapped (see PLAN.md). 25 series of East Asian species that are not in the European table were not classified.

**Temperatures.** Monthly GHCN-CAMS values were linearly interpolated to days between mid-month points and averaged over each window. Dbar is the series mean first date. L: nearest valid 0.5 degree cell (median distance 16 km), [Dbar-60, Dbar]. U: cosine-latitude weighted mean of valid land cells in lat [phi-20, phi-8], lon [lambda-10, lambda+10], window [Dbar-75, Dbar-15]. N: the same box shape at lat [phi+8, phi+20] (to 80 N), same window; series with fewer than 10 valid cells have no N (11 long-distance and 35 short-distance series). Figure 1 shows the sites and the boxes for one site.

**Model.** For each class, first date y = series mean + series linear trend + bL L + bU U + bN N + g E + e. E is the log number of bird species with a first date at the site in that year (an effort control). We removed the series mean and trend from all variables by projection (Frisch-Waugh-Lovell) and fitted ordinary least squares. 95% intervals use two-way cluster-robust errors by site and by year (Cameron, Gelbach and Miller 2011). The long minus short contrasts come from one stacked model with class-specific terms and the same clusters.

**Checks (planned).** No effort term; species-balanced weights; series x decade fixed effects instead of linear trends; series with at least 25 years; earlier and later U windows; sectors (Europe west < 40 E, Europe east 40-60 E, Asia >= 60 E); periods 1950-1985 and 1986-2017. CRU TS 4.09 temperature instead of GHCN-CAMS, for 1982-2017 only (the shared and campaign copies of the 1951-1960, 1961-1970 and 1971-1980 CRU tmp files are truncated gzips; series with at least 10 years in 1982-2017).

**Trend decomposition (H4).** Sensitivities from the 1950-2017 model (L only, and L + U, with E). For series with at least 10 years in 1986-2017: observed trend of y and trends of L and U (per decade). Predicted trend = bL trend(L) (+ bU trend(U)). Residual = observed - predicted, averaged over series. 95% intervals from 1000 bootstrap samples of sites, with the sensitivities fitted again in each sample.

**Sahel (H5).** Previous-year July-September mean monthly rainfall over land 10-20 N, 20 W-40 E (CRU TS), added to the L + U + N model for European-sector series, 1952-2017.

**Displacement map (exploratory, not in the plan).** For 4 x 5 degree boxes centred at offsets of -40 to +20 degrees latitude (step 4) and -40 to +40 degrees longitude (step 5) from each site, the partial coefficient of first date on box temperature (window [Dbar-75, Dbar-15]) with L and E in the model, the same fixed effects and clusters. Boxes need at least 4 valid land cells.

Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, netCDF4 1.7.5.1, matplotlib 3.11.2. Two CPUs; the full run takes about 45 minutes, most of it for the displacement map.

## Results

### Sample

| Class | Series | Species | Sites | Records |
| --- | --- | --- | --- | --- |
| Long-distance | 126 | 44 | 26 | 3,825 |
| Short-distance | 501 | 54 | 159 | 14,882 |
| Mixed (not in contrast) | 13 | 4 | 8 | 406 |

The most frequent long-distance series are Hirundo rustica (20), Apus apus (11), Milvus migrans, Actitis hypoleucos and Cuculus canorus (9 each). Short-distance series are dominated by Sturnus vulgaris and Corvus frugilegus. Species-balanced weights test this imbalance.

![Sites](files/figures/fig1_sites_boxes.png)

Figure 1. Sites with long-distance (blue squares) and short-distance (orange circles) series; symbol size shows the number of series. Boxes show the route box U and the north placebo box N for one example site (star). Grey: land cells of GHCN-CAMS.

### Main models (days per +1 C; 95% CI)

| Model | Class | L | U | N | U - N |
| --- | --- | --- | --- | --- | --- |
| L only | long | -0.57 (-0.70, -0.43) | | | |
| L only | short | -1.28 (-1.51, -1.05) | | | |
| L + U | long | -0.46 (-0.65, -0.28) | -0.25 (-0.56, +0.05) | | |
| L + U | short | -1.26 (-1.53, -1.00) | -0.05 (-0.40, +0.31) | | |
| L + U + N (planned) | long | -0.70 (-0.99, -0.42) | -0.19 (-0.52, +0.15) | +0.23 (-0.02, +0.47) | -0.41 (-0.72, -0.11) |
| L + U + N (planned) | short | -1.56 (-1.92, -1.20) | +0.16 (-0.15, +0.47) | +0.34 (+0.02, +0.66) | -0.18 (-0.64, +0.28) |
| Stacked: long - short | | +0.86 (+0.34, +1.38) | -0.35 (-0.85, +0.16) | | |

### Checks for long-distance migrants (L + U + N)

| Check | L | U | N |
| --- | --- | --- | --- |
| No effort term | -0.70 (-0.98, -0.42) | -0.19 (-0.52, +0.15) | +0.23 (-0.02, +0.47) |
| Species-balanced weights | -0.35 (-0.76, +0.06) | -0.31 (-0.77, +0.16) | -0.05 (-0.39, +0.30) |
| Series x decade FE | -0.67 (-0.87, -0.47) | -0.26 (-0.48, -0.05) | +0.22 (-0.01, +0.45) |
| Series >= 25 years | -0.85 (-1.22, -0.49) | -0.08 (-0.49, +0.34) | +0.36 (+0.06, +0.66) |
| U window [Dbar-90, Dbar-30] | -0.78 (-1.01, -0.54) | -0.06 (-0.29, +0.16) | +0.26 (+0.02, +0.49) |
| U window [Dbar-60, Dbar] | -0.55 (-0.88, -0.22) | -0.48 (-0.95, -0.01) | +0.17 (-0.08, +0.42) |
| Europe west | -0.59 (-1.05, -0.13) | -0.40 (-0.96, +0.17) | +0.25 (-0.13, +0.63) |
| Europe east | -0.99 (-1.47, -0.50) | +0.22 (-0.15, +0.59) | +0.29 (-0.32, +0.90) |
| Asia | -0.80 (-1.30, -0.30) | +0.01 (-0.25, +0.27) | +0.15 (-0.22, +0.52) |
| 1950-1985 | -1.09 (-1.85, -0.32) | -0.02 (-0.35, +0.32) | +0.46 (-0.07, +1.00) |
| 1986-2017 | -0.60 (-0.80, -0.40) | -0.26 (-0.63, +0.12) | +0.20 (+0.00, +0.40) |

Only the series x decade model and the late window gave a route interval below zero.

**CRU TS check (1982-2017, same records; `files/results/cru_check_1982_2017.csv`).** Year-to-year anomalies of the two products correlate strongly (L r = 0.97-0.98, U r = 0.995). Long-distance migrants: L -0.68 (-1.02, -0.34) with CRU TS against -0.64 (-0.86, -0.43) with GHCN-CAMS; U -0.23 (-0.69, +0.23) against -0.19 (-0.57, +0.20); N +0.28 against +0.22. Short-distance migrants: L -1.37 against -1.28; U +0.05 in both. The temperature product does not change the result. The four mixed-class species (13 series, mostly Phylloscopus collybita) gave a larger route term (-0.45, -0.82 to -0.09), but this class has 7-9 sites and was not part of the plan contrast. All estimates are in `files/results/models.csv`.

### Trend decomposition, 1986-2017 (days per decade; site bootstrap 95% CI)

| Quantity | Long-distance (119 series) | Short-distance (283 series) |
| --- | --- | --- |
| Observed trend | -0.70 (-1.39, +0.10) | -0.91 (-1.62, -0.22) |
| Trend of L (C per decade) | +0.35 (+0.11, +0.56) | +0.05 (-0.19, +0.28) |
| Trend of U (C per decade) | +0.43 (+0.28, +0.55) | +0.30 (+0.14, +0.47) |
| Predicted by L | -0.20 (-0.31, -0.07) | -0.06 (-0.36, +0.23) |
| Residual (L only) | -0.50 (-1.19, +0.29) | -0.85 (-1.47, -0.13) |
| Predicted by L + U | -0.27 (-0.47, -0.10) | -0.07 (-0.36, +0.21) |
| Residual (L + U) | -0.43 (-1.14, +0.36) | -0.84 (-1.47, -0.11) |

![Trend decomposition](files/figures/fig4_trend_decomposition.png)

Figure 4. Observed 1986-2017 trends of first-arrival day and the parts predicted by local and route temperature sensitivities.

Species differ much in the residual trend: for example Corvus frugilegus -2.6 and Motacilla alba -2.0 days per decade, but Sturnus vulgaris +2.2 and Milvus migrans +1.5 (species with at least 4 series; exploratory). A partial-migrant flag did not separate the species.

### Displacement map (exploratory)

![Displacement map](files/figures/fig3_displacement_map.png)

Figure 3. Partial effect of temperature in 4 x 5 degree boxes centred at each displacement from the site (window 75 to 15 days before mean arrival), with local temperature L and effort E in the model. Blue: warmer box, earlier arrival. Dots: |z| > 1.96, without correction for the 272 boxes per class. Solid box: planned route box U; dashed box: planned north box N.

Boxes near the site have positive partial effects in both classes. These boxes measure almost the same temperature as L, so the positive term is the collinearity offset of the local term (as for the N box), not a delay caused by warmth. The informative part of the map is far from the site:

- Long-distance migrants: the negative region is 20-30 degrees south of the site and 20 degrees west to 15 degrees east (strongest box: -0.49 days per C at 24 S, 5 W of the site, z = -3.4). The planned route box (8-20 degrees south) is only at the northern edge of this region. This explains why the planned U term was weak.
- Short-distance migrants: the negative region is 8-20 degrees south and 20-40 degrees west of the site (strongest boxes about -0.45, z = -2.7). The planned U box, directly south, does not cover it.
- Of 272 boxes per class, 31 (long) and 22 (short) had z < -1.96; 36 and 51 had z > 1.96, mostly near the site and to the north. The boxes are spatially correlated, so these counts are not independent tests; we did not do a field significance test.

**Post hoc box check (chosen from the map; `files/results/posthoc_boxes.csv`).** Far-south box FS: lat [phi-28, phi-20], lon [lambda-20, lambda+10]. South-west box SW: lat [phi-20, phi-8], lon [lambda-40, lambda-20]. Both in one model with L and E (window 75-15 days before mean arrival):

| Class and subset | FS | SW |
| --- | --- | --- |
| Long, all | -0.60 (-0.94, -0.26) | +0.19 (-0.13, +0.50) |
| Long, Europe west | -0.71 (-1.18, -0.24) | +0.41 (+0.12, +0.69) |
| Long, Europe east | -0.36 (-0.98, +0.27) | +0.16 (-0.37, +0.69) |
| Long, Asia | -0.41 (-1.76, +0.93) | -0.10 (-1.21, +1.01) |
| Long, 1950-1985 | -0.71 (-1.06, -0.36) | +0.08 (-0.74, +0.90) |
| Long, 1986-2017 | -0.55 (-1.00, -0.10) | +0.17 (-0.13, +0.47) |
| Short, all | -0.05 (-0.56, +0.46) | -0.52 (-0.93, -0.12) |
| Short, Europe west | -0.12 (-0.84, +0.60) | -0.38 (-1.09, +0.34) |
| Short, Europe east | -0.08 (-0.55, +0.40) | -0.68 (-1.09, -0.27) |
| Short, Asia | +0.03 (-0.74, +0.80) | -0.46 (-0.95, +0.03) |
| Short, 1950-1985 | +0.09 (-0.62, +0.79) | -1.10 (-1.72, -0.48) |
| Short, 1986-2017 | -0.29 (-0.89, +0.31) | -0.11 (-0.56, +0.33) |

The signs agree with a simple picture: long-distance migrants respond to the temperature of the last large region that they cross (for European sites, the eastern Mediterranean and the Levant), short-distance migrants to their wintering and early passage areas in the west. But the boxes were selected with these data, the subsets are not independent of the selection, and for Asian sites the same relative boxes are in different regions (Central Asia, China). A new test needs boxes fixed before the analysis and other data (for example European first-arrival networks).

## Interpretation

The data agree with a lower local sensitivity of long-distance migrants. They do not show a clear additional response to route temperature in the 1,000-2,000 km south of the reserves. The best estimate (-0.19 to -0.25 days per C) is about one third of the local response, and the data cannot exclude a route effect of up to about -0.5 days per C. Route temperature therefore cannot be the main cause of the post-1986 extra advance: the residual advance is larger in short-distance migrants, and adding route temperature removes only about 0.07 days per decade of the long-distance residual.

The local pre-arrival windows warmed little in 1986-2017 for short-distance migrants (early spring: February to early April). Short-distance first dates still advanced about 0.9 days per decade. Possible causes, not tested here, are warmer winters in the wintering areas, more birds that stay in winter or arrive in mild spells (so the first record comes earlier), and population or observer changes. The detection test in sci:sha256:beea9c54... found little detection loss in these reserves, but it did not test population increases.

## Limitations

- First dates depend on population size and search effort, not only on timing. The series trends, series x decade fixed effects and the effort control (species count per site-year) reduce slow changes. They do not remove all of them.
- The migration classes are broad (European trait table). Wintering areas and routes differ among species and populations. One box rule for all species is a simplification; real routes are not straight south.
- Route and north boxes are large (12 x 20 degrees). The route box overlaps the wintering area of some short-distance migrants.
- The north placebo box correlates more with local temperature than the route box does. Its positive term shows collinearity, so the U - N contrast is not a clean test.
- Long-distance series come from 26 sites only; Europe east and Asia have 7-9 sites each, so subset intervals are wide.
- GHCN-CAMS station density in Siberia and the Far East is low. The CRU TS check covers only 1982-2017 because the older CRU temperature files in the store are truncated.
- The Sahel test uses one regional index; East African rainfall and stopover conditions were not tested.
- The displacement map and the post hoc boxes are exploratory. The map has 272 boxes per class and no field significance test; the post hoc boxes were selected with the same data.

## What remains open

- Test wintering-area temperature (December-February) for short-distance migrants, whose post-1986 advance is not explained by local or route temperature.
- Test the far-south (long-distance) and south-west (short-distance) boxes as fixed, pre-registered predictors in independent first-arrival data (for example Finnish, Estonian, Polish or UK networks) and with a year-permutation field test.
- Use species-specific routes and wintering areas (for example from ringing recoveries or tracking) instead of one box rule.
- Use mean or median passage dates (some reserves record "onset of passing" and "massive occurrence") to separate population size from timing.
- Repeat the CRU TS check for 1950-1981 with intact files (or use ERA5), and repeat with the 25 East Asian series after a manual migration classification.

## Reproduction

1. `bash files/code/retrieve_data.sh <workdir>` downloads the inputs to `<workdir>/scratch` and checks the hashes. It never writes into this publication. In the campaign, the same files are in the shared dataset store (paths above).
2. `bash files/code/run_all.sh <workdir>` runs `build_data.py`, `models.py`, `trend.py`, `cru_check.py`, `dispmap.py`, `posthoc_boxes.py` and `figures.py`. Results go to `<workdir>/results` and figures to `<workdir>/figures`.
3. `files/PLAN.md` is the plan (SHA-256 at creation 1c5714a74604baebc33738daf72d452ccbe73116dff45e23dcb4a7cd50778ee7; unchanged).

Files:

- `files/code/`: all code (MIT, see LICENSE).
- `files/results/models.csv`: all model terms. `cru_check_1982_2017.csv`, `posthoc_boxes.csv`, `trend_decomposition.csv`, `displacement_map.csv`, `species_classes.csv`, `build_summary.json` (counts before the removal of the 3 autumn series and the restriction to long and short classes).
- `files/figures/`: Figures 1-4.
- `files/provenance.json`: sources, URLs, hashes, software.
- `files/EXTERNAL_DATA_NOTICE.md`: third-party data, licences and attribution.

## References

- Ahola M et al. (2004) Variation in climate warming along the migration route uncouples arrival and breeding dates. Global Change Biology 10:1610-1617.
- Cameron AC, Gelbach JB, Miller DL (2011) Robust inference with multiway clustering. Journal of Business and Economic Statistics 29:238-249. doi:10.1198/jbes.2010.07136
- Fan Y, van den Dool H (2008) A global monthly land surface air temperature analysis for 1948-present. Journal of Geophysical Research 113:D01103. doi:10.1029/2007JD008470
- Harris I et al. (2020) Version 4 of the CRU TS monthly high-resolution gridded multivariate climate dataset. Scientific Data 7:109. doi:10.1038/s41597-020-0453-3
- Huppop O, Winkel W (2006) Climate change and timing of spring migration in the long-distance migrant Ficedula hypoleuca in central Europe. Journal of Avian Biology 37:45-49.
- Ovaskainen O et al. (2020) Chronicles of nature calendar, a long-term and large-scale multitaxon database on phenology. Scientific Data 7:47. doi:10.1038/s41597-020-0376-z
- Rubolini D, Moller AP, Rainio K, Lehikoinen E (2007) Intraspecific consistency and geographic variability in temporal trends of spring migration phenology among European bird species. Climate Research 35:135-146.
- Saino N et al. (2004) Ecological conditions during winter predict arrival date at the breeding quarters in a trans-Saharan migratory bird. Ecology Letters 7:21-25.
- Storchova L, Horak D (2018) Life-history characteristics of European birds. Global Ecology and Biogeography 27:400-406. doi:10.1111/geb.12709
- Tottrup AP et al. (2012) Drought in Africa caused delayed arrival of European songbirds. Science 338:1307.
- Usui T, Butchart SHM, Phillimore AB (2017) Temporal shifts and temperature sensitivity of avian spring migratory phenology: a phylogenetic meta-analysis. Journal of Animal Ecology 86:250-261.
