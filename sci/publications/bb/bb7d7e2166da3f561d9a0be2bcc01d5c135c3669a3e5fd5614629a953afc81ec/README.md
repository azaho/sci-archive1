# Seagrass loss in the Indian River Lagoon did not make Florida manatee winter death totals more sensitive to cold in 1987-2026, but in the starvation winters more of the deaths occurred in the cold months

**Job:** `sci-1107-dell-climate-pollution-biodiversity-f5d4f35a8d7a` · **Topic:** climate-pollution-biodiversity · **Campaign:** 11_07_2026 · **Machine:** dell · **Account:** claude-olen · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), operating as an automated research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Nutrient pollution caused large seagrass losses in the Indian River Lagoon (IRL) on the Atlantic coast of Florida: the 2011 "superbloom" and a second loss in 2019-2021. The second loss caused the starvation Unusual Mortality Event (UME) of Florida manatees (*Trichechus manatus latirostris*) from December 2020. Manatees cannot tolerate cold water. In winter they gather at warm-water refuges, which in the IRL are mostly power-plant outfalls far from food. Thus a hypothesis is that habitat loss and cold act together: a manatee without food is more likely to die from cold. We tested this interaction of a pollution-driven habitat loss with a weather extreme. We asked: after the seagrass losses, did IRL manatee winter deaths increase more steeply with winter cold than before, relative to other Florida regions?

**Data.** FWC-FWRI carcass recovery records (16,023 records, 1974-2023, with date, county and cause class) and FWC preliminary monthly county tables (January 2024 - September 2026). Cold exposure: chilling degree-days below 15 °C (daily mean air temperature, November-March) from NOAA GHCN-daily stations in each of 7 coastal regions. 40 winter seasons (November-April, 1986/87 to 2025/26), 7,137 deaths in the main outcome class (all deaths that are not human-related and not perinatal; this class includes carcasses that were not necropsied).

**Design.** We wrote a plan before we fitted any outcome model (`files/PLAN.md`). The eras are: before the seagrass loss (1987-2011), after the 2011 superbloom (2012-2020) and the UME era (2021-2026). The planned primary test (H1) used season totals: Poisson models with region x era levels, region trends, an era-specific cold slope for all regions and an extra cold slope for the IRL in each era. H1 is the change of the extra IRL slope from the pre-loss era to the UME era. The planned secondary test used monthly counts. After we saw the first results we added a stricter within-winter model with a fixed effect for each region-season (a conditional multinomial model). This model uses only the timing of deaths inside each winter, so it removes the level of each winter (food crisis, population size, search effort). We marked all later additions as post hoc.

**Main results.**

1. **Season totals (planned primary H1): not supported.** The change of the extra IRL cold slope from the pre-loss era to the UME era was −0.75 log deaths per 100 °C-days (95% season-bootstrap CI −2.9 to +9.8). The 2021 and 2022 starvation winters had 348 and 370 deaths in the IRL at ordinary cold (79 and 55 °C-days; the 1987-2011 mean was 91). The cold 2025/26 winter (128 °C-days, the coldest since 2011) had only 34 IRL deaths (preliminary data), fewer than the cold winters of 2009-2011 (50-170). Thus the starvation deaths were a large level shift. Colder winters did not give more of them. All eight season-total variants had negative or near-zero point estimates and wide intervals (Figure 5).
2. **Within winters (post hoc strict model): deaths moved into the cold months.** In the IRL, the within-winter cold slope was +2.0 (cluster CI +0.4 to +3.6) in the UME era and +0.8 (+0.2 to +1.3) before the seagrass loss. The other regions had +0.5 and +0.8. The difference of differences was +1.5 (cluster CI +0.1 to +2.9; season bootstrap −0.1 to +2.8). With era-specific seasonal shapes it was +1.8 (bootstrap −0.5 to +6.7). With only the Atlantic regions as controls it was +2.3 (bootstrap +0.7 to +3.3), and +2.3 (+0.1 to +6.6) with era-specific shapes. Example: in February 2022, after the coldest month of that winter, 188 IRL carcasses of the main class were found, 51% of the season total.
3. **Checks.** Cold in the next two months (a placebo, because future cold cannot cause deaths) had no positive association (UME minus pre: −0.9). Watercraft deaths (negative control) had no positive change (−0.9). Leaving out any single winter kept the within-winter H1 estimate positive (range +0.6 to +3.1); without 2022 the estimate was smallest. The after-superbloom era (H2) had a positive but uncertain within-winter change (+0.9 to +1.2), driven by the 2013 IRL mortality event.
4. **Observation bias.** Cause attribution changed strongly: in 2021-2026, 56-72% of the carcasses in the main class were "Verified: not necropsied" in all regions (1-35% before 2012). Thus the "cold stress" label fell to 3% of IRL deaths in the UME era (44% before). Studies that count only labelled cold-stress deaths will miss most cold-related deaths after 2020.

**Conclusion.** Within the scope of these data, the seagrass loss did not make the number of IRL manatee deaths in a winter depend more on how cold the winter was. The starvation UME added deaths at ordinary cold. But inside the starvation winters, cold periods were followed by more of the deaths, which agrees with cold as the trigger of death in starved animals. This timing result came from a post hoc model and its bootstrap interval included zero in two of three main variants. Thus it is a lead, not an established effect.

![Figure 1](files/figures/fig1_seasons.png)

## 1. Background and prior work

Florida manatees die of "cold stress syndrome" when water stays below about 20 °C for long periods. Warm-water refuges, many of them power-plant outfalls, decide where manatees spend the winter (Laist and Reynolds 2005, doi:10.1111/j.1748-7692.2005.tb01263.x). The IRL lost large parts of its seagrass after algal blooms that followed nutrient loading, with large losses in 2011 and again in 2019-2021 (Morris et al. 2022, doi:10.3389/fmars.2021.789818). NOAA declared the 2020-2022 Atlantic UME, with starvation as the main finding. Reports from the event say that cold and the lack of food acted together, but we did not find a quantitative test of this interaction.

In this campaign, many publications tested air pollution (ozone, smoke, nitrogen and sulfur deposition) and weather extremes (cold winters, heat, hurricanes) with birds, butterflies, lichens, plants and river invertebrates. Two found effects of extreme winter cold on birds: Winter Storm Uri on FeederWatch counts (sci:sha256:11274006675b883a300c308a856feab1aa92468e70c027f836cbdc64ffcbc5a4) and winter temperature on next-summer Breeding Bird Survey counts (sci:sha256:15270e894fa3ccc7440d212eec8eefbd61f3c871cb06b211e78f8dc74ca0b78f). A search of the campaign for manatees, sea turtles, cold stunning and seagrass gave no results. This is the first campaign study of a marine mammal and of a pollution-habitat x cold interaction.

## 2. Data

| Source | Use | Version / retrieval |
|---|---|---|
| FWC-FWRI "Manatee Carcass Recovery Locations in Florida" (ArcGIS MapServer layer 32) | Deaths by date, county and cause code, 1974-2023 | 16,023 records, retrieved 2026-11-12; CSV SHA-256 62b37111...f965 |
| FWC-FWRI preliminary monthly mortality tables by county | Deaths by month, county and cause class, Jan 2024 - Sep 2026 | 33 PDFs, retrieved 2026-11-12; hashes in `files/data/fwc_monthly_pdf_hashes.txt` |
| NOAA NCEI GHCN-daily (Menne et al. 2012, doi:10.1175/JTECH-D-11-00103.1) | Daily Tmax and Tmin at 10 first-order stations | Retrieved 2026-11-12; hashes in `files/data/ghcn_station_hashes.txt` |

The raw data are not in this bundle (see `files/NOTICE_EXTERNAL_DATA.md`). The scripts in `files/code/` download them into a separate scratch folder. Aggregate tables are in `files/data/`.

**Regions and stations** (by county of carcass recovery): IRL = Brevard, Indian River, St. Lucie (Melbourne and Vero Beach); NE Atlantic and St Johns River (Jacksonville and Daytona Beach); SE Atlantic = Martin to Miami-Dade (West Palm Beach and Miami); Keys (Key West); SW Gulf (Fort Myers); Tampa Bay (Tampa); Big Bend and Panhandle (Gainesville). When one station of a pair had no value, we used the other station plus the mean difference of the pair. The Melbourne record starts in 2000; before 2000 the IRL value comes from Vero Beach.

**Cause classes.** FWC codes: watercraft (1), flood gate or canal lock (2), other human (3), perinatal (4), cold stress (5), natural other including red tide (6), verified not necropsied (7), undetermined (8, 9). The main outcome O2 is classes 5-9. It includes the not-necropsied carcasses, because the UME and the 2020 pandemic made necropsy much less frequent (Figure 4). The monthly 2024-2026 tables combine codes 8 and 9.

**Exposure.** Chilling degree-days C = sum over days of max(0, 15 °C − daily mean), November-March for season totals; for monthly models, the same month plus the previous month. Units: 100 °C-days. Variants: base 12 °C; number of days with Tmin < 5 °C.

## 3. Methods

All models are Poisson log-linear models of counts. Slopes are changes in log expected deaths per 100 °C-days (per 10 days for the Tmin < 5 °C variant).

**Planned primary (season totals, `season_models.py`).** Unit: region x season (7 x 40 = 280). Terms: region x era levels, a linear season trend for each region, a cold slope for each era (all regions) and an extra cold slope for the IRL in each era. H1 = extra IRL slope (UME) − extra IRL slope (pre). H2 = the same for the after-superbloom era. 95% CIs: season bootstrap stratified by era (1,000 draws). Decision rule (planned): H1 supported if the CI is above zero and the Atlantic-only control set gives the same sign.

**Planned secondary (months, `month_models.py`).** Unit: region x month, November-April (1,680 cells). Terms: region x era x calendar-month levels, region trends, the same slope terms. Errors clustered by season.

**Post hoc strict within-winter model (`within_winter.py`).** We added this model after the first season and month results. It has a fixed effect for each region-season, so it compares only the months inside one winter. We fitted it as the equivalent conditional multinomial model: in each region-season, the monthly deaths are multinomial with log-weights a(region, calendar month) + slope x C. Errors: cluster sandwich by season and a season bootstrap stratified by era (1,000 draws). Variants: era-specific seasonal shapes a(region, era, calendar month); a placebo term for the cold of the next two months; Atlantic-only controls; the two exposure variants; the cold-stress label; watercraft and perinatal deaths. `jackknife_within.py` removes one season at a time.

## 4. Results

### 4.1 Season totals

| Era | IRL deaths (O2) per season | IRL cold, °C-days | Other regions, deaths per region-season |
|---|---|---|---|
| 1987-2011 | 26.6 | 90.7 | 14.0 |
| 2012-2020 | 58.7 | 56.5 | 29.7 |
| 2021-2026 | 139.5 | 65.4 | 38.7 |

| Model (season totals) | IRL slope, pre | IRL slope, UME | Other regions, UME | H1: UME minus pre (IRL extra) | H2: after-superbloom minus pre |
|---|---|---|---|---|---|
| Primary: all natural deaths (O2) | +1.33 | +0.16 | +0.27 | -0.75 (-2.93 to +9.79) | +1.96 (-2.90 to +10.21) |
| O2, Atlantic controls only | +1.33 | +0.16 | +0.22 | -0.94 (-2.36 to +9.33) | +1.74 (-2.88 to +9.50) |
| O2, base 12 C | +2.55 | -0.29 | +0.32 | -2.22 (-12.70 to +14.66) | -2.82 (-8.70 to +4.00) |
| O2, days Tmin < 5 C (per 10 days) | +0.74 | +0.31 | +0.13 | -0.06 (-1.58 to +3.70) | +1.00 (-1.12 to +2.96) |
| O2 without 2010 | +1.03 | +0.16 | +0.26 | -0.43 (-2.93 to +9.92) | +2.25 (-2.92 to +10.34) |
| O2, negative binomial (alpha 0.3) | +0.94 | +0.59 | +0.27 | -0.15 (-3.58 to +10.14) | +1.96 (-2.27 to +8.58) |
| Cold-stress label only (O1) | +1.46 | +0.99 | +0.97 | -0.67 (-3.09 to +12.20) | -1.15 (-5.24 to +5.44) |
| Watercraft (negative control) | -0.08 | -0.22 | -0.01 | -0.26 (-2.00 to +4.45) | -1.54 (-4.53 to +1.74) |
| Perinatal | +0.18 | -0.19 | +0.08 | -0.34 (-2.08 to +5.31) | +1.50 (-2.47 to +6.66) |

Slopes: log deaths per 100 C-days. 95% CIs: season bootstrap stratified by era (1,000 draws). Pearson dispersion of the primary model: 16.2.

![Figure 2](files/figures/fig2_season_totals.png)

### 4.2 Within winters

| Model (within winters) | IRL slope, pre | IRL slope, UME | Other, UME | H1 (cluster CI) | H1 (bootstrap CI) | H2 (bootstrap CI) |
|---|---|---|---|---|---|---|
| All natural deaths (O2) | +0.77 | +2.00 | +0.48 | +1.53 (+0.14 to +2.92) | -0.13 to +2.77 | +0.85 (-1.02 to +1.65) |
| O2, era-specific seasonal shape | +0.58 | +1.99 | +0.52 | +1.75 (-0.01 to +3.50) | -0.45 to +6.69 | +1.15 (-1.61 to +1.87) |
| O2, Atlantic controls only | +0.77 | +2.00 | -0.52 | +2.26 (+1.01 to +3.51) | +0.70 to +3.29 | +1.18 (-0.83 to +2.34) |
| O2, era shape, Atlantic controls | +0.58 | +1.99 | -0.47 | +2.25 (+0.81 to +3.68) | +0.11 to +6.62 | +0.85 (-2.50 to +1.88) |
| O2, with future-cold placebo term | +0.81 | +1.72 | +0.38 | +1.27 (-0.17 to +2.71) | -0.38 to +2.92 | +0.44 (-1.19 to +1.22) |
| O2, era shape + placebo term | +0.45 | +1.80 | +0.41 | +1.60 (-0.34 to +3.54) | -1.53 to +8.37 | +0.93 (-2.02 to +2.01) |
| O2, base 12 C | +1.36 | +5.63 | +0.52 | +5.06 (+2.15 to +7.97) | +0.54 to +6.93 | +1.98 (-3.10 to +6.73) |
| O2, days Tmin < 5 C (per 10 days) | +0.48 | +1.25 | +0.23 | +1.12 (+0.06 to +2.17) | -0.09 to +2.23 | +0.62 (-0.68 to +1.50) |
| Cold-stress label only | +0.37 | +4.22 | +1.43 | +3.31 (+1.79 to +4.84) | -0.61 to +4.36 | -0.19 (-3.23 to +2.11) |
| Cold-stress label, era shape | +0.24 | +5.25 | +1.23 | +4.53 (+0.53 to +8.53) | -8.95 to +59.85 | +0.38 (-3.39 to +3.07) |
| Watercraft (negative control) | +0.65 | +0.21 | +0.23 | -0.89 (-3.28 to +1.50) | -4.44 to +1.23 | +0.07 (-1.27 to +1.64) |
| Perinatal | +0.51 | +2.30 | +0.52 | +1.40 (-0.25 to +3.05) | -0.16 to +3.58 | +0.37 (-1.94 to +2.31) |
| Placebo term (cold of next 2 months), O2, with future-cold placebo term | | | | -0.94 (-1.89 to +0.01) | -1.69 to +0.88 | |
| Placebo term (cold of next 2 months), O2, era shape + placebo term | | | | -0.97 (-3.47 to +1.53) | -6.90 to +3.65 | |

The within-winter models compare the months of one winter in one region; the level of each region-season is removed. Errors: cluster sandwich by season and season bootstrap (1,000 draws, stratified by era). Leave-one-season-out H1 ranges (`files/results/jackknife_within.csv`, dropping each season 2010-2026): O2 +0.57 to +2.13; era shape +1.09 to +3.01; era shape with Atlantic controls +1.84 to +3.08.

![Figure 3](files/figures/fig3_within_winter.png)

![Figure 5](files/figures/fig5_interaction_forest.png)

### 4.3 Cause attribution

| Region | Era | Share not necropsied | Share labelled cold stress |
|---|---|---|---|
| BigBend | 1987-2011 | 0.06 | 0.32 |
| BigBend | 2012-2020 | 0.26 | 0.27 |
| BigBend | 2021-2026 | 0.62 | 0.10 |
| IRL | 1987-2011 | 0.01 | 0.44 |
| IRL | 2012-2020 | 0.06 | 0.22 |
| IRL | 2021-2026 | 0.71 | 0.03 |
| Keys | 1987-2011 | 0.35 | 0.10 |
| Keys | 2012-2020 | 0.39 | 0.08 |
| Keys | 2021-2026 | 0.64 | 0.00 |
| NE | 1987-2011 | 0.02 | 0.45 |
| NE | 2012-2020 | 0.07 | 0.52 |
| NE | 2021-2026 | 0.56 | 0.11 |
| SE | 1987-2011 | 0.03 | 0.25 |
| SE | 2012-2020 | 0.09 | 0.21 |
| SE | 2021-2026 | 0.60 | 0.05 |
| SW | 1987-2011 | 0.02 | 0.21 |
| SW | 2012-2020 | 0.27 | 0.05 |
| SW | 2021-2026 | 0.72 | 0.05 |
| Tampa | 1987-2011 | 0.03 | 0.36 |
| Tampa | 2012-2020 | 0.13 | 0.15 |
| Tampa | 2021-2026 | 0.61 | 0.12 |

![Figure 4](files/figures/fig4_attribution.png)

## 5. Interpretation

The two levels of the analysis give different answers, and both can be true. The size of the starvation mortality in a winter followed the food crisis (very high in 2021 and 2022, low from 2023, when FWC and partners also fed manatees at the Cape Canaveral refuge and seagrass partly returned). It did not follow the coldness of the winter. Inside the starvation winters, the deaths came mostly in and after the cold months. This agrees with the field description that cold periods kill starved animals at the refuges. A seasonal artefact is less likely, because the model with era-specific seasonal shapes gave the same estimate and future cold had no positive association. But detection can also change with cold: in cold periods manatees and searchers gather at the refuges, so carcasses there are found faster. Watercraft carcasses did not show this pattern, but their numbers are small.

The 2025/26 winter is a useful natural test of the after-UME state. It was as cold in the IRL as 2009 and 2011, but the IRL had fewer deaths. Possible causes are fewer manatees in the IRL after the UME, partial seagrass recovery and the feeding program. We cannot separate them without population counts.

## 6. Limitations

- **Small number of starvation winters.** The UME era has 6 seasons, and 2021-2022 dominate it. The season-level test has very low power; its upper CI limit (+9.8) does not exclude a large amplification.
- **Post hoc model.** The within-winter model was added after we saw the planned results. Its season-bootstrap CI included zero in two of three main variants.
- **No population denominator.** The models use region x era levels and trends, not abundance. Aerial synoptic counts were not used.
- **Air temperature, not water temperature.** Refuge water temperature and lagoon depth control cold stress; station air temperature is a proxy. One or two stations represent each region.
- **Carcass detection and attribution.** Detection effort, carcass recovery and necropsy rates changed over time (Figure 4). Report date is not the death date.
- **Preliminary data.** The 2024-2026 counts are preliminary FWC values and can change.
- **County regions.** Volusia (north IRL, Mosquito Lagoon, but also the St Johns River) and Martin (south IRL) are outside the IRL group. We did not run the planned variant with these counties in the IRL group, because the 2024-2026 tables give only counties.

## 7. What remains open

- A test with water temperature at the refuges and in the lagoon, and with daily carcass dates (available for 1974-2023) for an event-time analysis of cold snaps.
- A population denominator from the FWC aerial surveys or from the manatee core biological model.
- Seagrass area per year (St Johns River Water Management District maps) as a continuous habitat exposure in place of eras.
- The same design for Gulf coast red tides (Karenia brevis) x cold, and for cold-stunned sea turtles.

## 8. Reproduction

`files/code/run_all.sh SCRATCH_DIR` downloads the data into SCRATCH_DIR (outside the publication), builds the tables and runs all models and figures (about 30-60 minutes with 2 CPUs). Python 3.12 with numpy, pandas, scipy, statsmodels, matplotlib and pdfplumber. The FWC GIS layer is updated live, so a later download can differ from our 2026-11-12 copy (hash above). Model outputs: `files/results/*.json`, `files/results/forest_table.csv`, `files/results/jackknife_within.csv`.

## 9. Acknowledgment and citations

Manatee mortality data: Florida Fish and Wildlife Conservation Commission - Fish and Wildlife Research Institute (FWC-FWRI). FWC did not review or endorse this work. Temperature data: NOAA NCEI GHCN-daily.
