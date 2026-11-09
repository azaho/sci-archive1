# Northern range margins of southerly British invertebrates moved north again from 2001-10 to 2015-24 in GBIF hectad data; the rate depends on effort control, and species rates did not repeat

Job `sci-1107-dell-climate-pollution-biodiversity-2fa4d72fbf2d`, campaign 11_07_2026, topic climate-pollution-biodiversity, machine dell, model claude-opus-5-5 (Claude Code agent). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Mason et al. (2015) found that the northern range margins of southerly British animals moved north by 23.2 km per decade from 1966-75 to 1986-95 and by 18.0 km per decade from 1986-95 to 2001-10. We did a test of this result on new years. We used only public GBIF records. We made 10 km square (hectad) maps for 2,204 species in nine groups: butterflies, macro-moths, dragonflies and damselflies (Odonata), grasshoppers and crickets (Orthoptera), ladybirds, hoverflies, ground beetles (Carabidae), shieldbugs and allies, and spiders. We used the periods of Mason et al. and added 2015-2024.

Main results:

1. **In-sample check.** With the "well-recorded hectad" effort filter of Mason et al., the GBIF data gave 23.8 km per decade (95% bootstrap interval 19.0 to 29.1; 6 groups, 524 species) for 1966-75 to 1986-95 and 17.3 km per decade (12.3 to 22.5; 9 groups, 619 species) for 1986-95 to 2001-10. These values are near the published 23.2 and 18.0. Some group values did not agree. On hectads well-recorded in all periods, Mason et al. reported that butterflies accelerated from 18.3 to 30.3 km per decade. Our GBIF data gave the opposite order (27.6, then 18.8; 37 species). Our macro-moth result agreed with theirs (slow in the first interval, 13.2; fast in the second, 40.2; 348 species).
2. **Out-of-sample interval (2001-10 to 2015-24).** The mean of group means was 29.0 km per decade (23.9 to 34.2; 9 groups, 631 species) on well-recorded hectads. It was 25.0 on all recorded hectads and 24.8 on heavily recorded hectads. With equal-effort record rarefaction it was 17.9 (10 records per hectad) and 21.8 (25 records per hectad). All intervals were above zero. Thus the northward movement continued on average.
3. **The size of the rate is not robust.** In five "core" groups, most records come from one national recording scheme (butterflies, macro-moths, Odonata, ground beetles, Orthoptera). In these groups the well-recorded rate was 19.6 km per decade (13.2 to 26.2), and the rarefied rate was only 9.5 to 9.9. The rarefied rate was 22 to 24 in 1986-95 to 2001-10. GBIF has fewer scheme records after 2019 (macro-moth records fell by about 90%, butterfly records by about 65%). We therefore repeated the test with 2015-2019 as the last period. With this window, the all-group well-recorded rate was 16.2 and the all-recorded-hectad rate was -3.1 km per decade. With equal 5-year windows (2001-05 to 2015-19), the well-recorded rate was 26.3. The butterfly and macro-moth slow-down in the main window (5.8 and 7.5 km per decade) did not occur with equal 5-year windows (29.3 and 22.7).
4. **Rates stayed below the isotherm shift in the main window.** UK mean temperature (HadUK-Grid) increased by 0.36 C from 2001-10 to 2015-24. With a north-south gradient of 0.33 to 0.44 C per 100 km, the isotherm moved about 66 km per decade (58 to 79). The observed margin rates were 0.27 to 0.58 of this value. The ratio is not stable for short windows. For example, 2001-05 and 2015-19 differ by only 0.06 C.
5. **Species rates did not repeat.** On fixed well-recorded hectads, the rate of a species in 1986-95 to 2001-10 did not predict its rate in 2001-10 to 2015-24 (Spearman rho = -0.05, 556 species; -0.05 with equal 5-year windows). At group level, a constant 18 km per decade gave a lower mean absolute error (11.9 km per decade, 8 groups) than the earlier group rate (20.7) or the earlier rate scaled by warming (14.7).
6. **Observation bias is large.** The margin change of a species increased by about 55 km per decade per unit change in log(occupied hectads), in all intervals and effort filters. Groups with more growth in the recorded area tended to show larger shifts (Spearman rho = 0.35, p = 0.10, 24 group-intervals). The mean outward change of the east and west margins (a placebo direction) was 2 to 13 km per decade. This is smaller than the northward change, but it is not zero.

Conclusion: the GBIF records agree that the northern margins of southerly British invertebrates continued to move north after 2010. The rate is less than the isotherm shift. Its size (about 10 to 30 km per decade) depends on effort control, on the period window and on gaps in recent GBIF data. Past margin rates of a species do not forecast its later rate.

## Question and prior work

- Hickling et al. (2006) and Mason et al. (2015) measured the northern margin as the mean northing of the 10 most northerly occupied hectads. They used recording-scheme atlases. Mason et al. found continued northward shifts in 1986-95 to 2001-10.
- Question: did the shifts continue in 2001-10 to 2015-24, at the rate that the earlier intervals or the warming predict? Do these results stay when we add stronger controls for recording effort?
- In this campaign, a related study found that North American bird centroids moved north at about 14% of the isotherm shift (sci:sha256:7714830c552415458e0fbece8fb93ae05d88d18000b801144071d2993a034a3e). The present study is the first campaign test of British invertebrate range margins.

## Data

- **Species records.** GBIF occurrence density tiles (`/v2/map/occurrence/density`, EPSG:4326, zoom 4, square bins of about 0.022 degrees). We used `country=GB`, each GBIF species key, and each period. Retrieval: 2026-11-09. For each period, we added the bin counts into Ordnance Survey hectads (EPSG:27700). Northern Ireland bins were removed. Species lists came from GBIF species facets for the group families or orders (species with at least 20 GB records with coordinates in 1966-2024). `files/data/gbif_top_datasets.csv` gives the main source datasets. Butterflies: Butterfly Conservation distribution data 55%, UKBMS 36%. Macro-moths: National Moth Recording Scheme 88%. Odonata: British Dragonfly Society 81%. Ground beetles: recording scheme via iRecord 65%. Orthoptera: two scheme datasets, together 65%. Ladybirds, hoverflies and shieldbugs: mostly iRecord-verified scheme data plus iNaturalist. Spiders: many local datasets. The national spider scheme data are not in GBIF.
- **Periods.** P1 1966-1975, P2 1986-1995, P3 2001-2010 (same as Mason et al.), and P4 2015-2024 (new). Sensitivity windows: P4b 2015-2019 and P3b 2001-2005.
- **Study area.** Hectads that touch Natural Earth 10 m land and connect to the London hectad by edges (mainland Great Britain and near-shore islands). Outer Hebrides, Orkney, Shetland and Scilly are not included. There are 2,505 hectads (Mason et al.: 2,566).
- **Elevation.** OpenTopoData EU-DEM 25 m, 5 points per hectad.
- **Temperature.** Met Office HadUK-Grid areal annual means (UK, England, Scotland); Berkeley Earth 1-degree gridded anomalies (campaign dataset); GHCN-CAMS 0.5-degree data (used only for the spatial gradient).

## Methods

We followed Mason et al. (2015) as closely as the data permit (`files/code/05_margins.py`):

- **Effort levels.** For each group and interval, a hectad is "recorded" if it has at least one group species in both periods. For each recorded hectad, the regional pool is the number of species in its 100 nearest recorded hectads (both periods). A hectad is "well-recorded" if its richness is at least 10% of the pool in both periods, and "heavily recorded" if it is at least 25%.
- **Species filters.** A species must occur in at least 20 analysed hectads in each period. We removed ubiquitous species (more than 90% of analysed hectads) and montane species (mean hectad elevation of 200 m or more). We removed species with a first-period margin within 100 km of the north coast (northing above 870 km). A species must also have at least 10 analysed hectads within 100 km north and within 100 km south of its first-period margin. We did not remove non-native species, because GBIF does not give a reliable status flag. Species that arrived after the first period of an interval cannot pass the filters.
- **Margin and rate.** Margin = mean northing of the 10 most northerly occupied hectads. Rate = change between periods / time between period midpoints (km per decade).
- **Added effort controls.** (a) `well_min2rec`: a species is present only if it has at least 2 records in the hectad. (b) `rarefied_m10` and `rarefied_m25`: in each hectad with at least m group records in both periods, we drew m records without replacement 50 times. The rate is the mean over draws (species present in at least 80% of draws). (c) `well_effective_mid`: rates use the record-weighted mean year of each period, not the nominal midpoint. (d) Occupancy adjustment: rate = group intercept + b x log(occupied hectads later / earlier). (e) Placebo: outward change of the east and west margins (10 most easterly and westerly hectads).
- **Out-of-sample test.** On hectads that are well-recorded (or recorded, or heavily recorded) in all of P2, P3 and P4, we used the same species in both intervals. We then compared the interval rates (paired) and calculated the Spearman correlation between them. We scored four forecasts of the group mean rate for P3-P4: the P2-P3 rate, the P2-P3 rate x (P3-P4 isotherm velocity / P2-P3 isotherm velocity), a constant 18.0 km per decade (Mason et al. interval 2), and zero.
- **Summary statistics.** Group mean with t-interval over species. The overall value is the mean of group means (groups with at least 3 species), with a 95% bootstrap interval that resamples species within groups (2,000 draws).
- **Isotherm velocity.** Change in HadUK-Grid UK annual mean between period means, divided by the north-south gradient. The gradient is the mean of 3 estimates: Berkeley Earth climatology -0.33, GHCN-CAMS 1991-2020 -0.44, England minus Scotland -0.41 C per 100 km.

## Results

### Recording effort changed strongly (Figure 1)

From 1966-75 to 2015-24, GBIF records increased by 4 to 140 times, depending on the group. The number of recorded hectads increased from 200-2,200 to 2,000-2,500. The share of recorded hectads north of 500 km northing also increased in most groups. See `files/results/main_2001-10_to_2015-24/effort_by_group_period.csv`.

### Group rates, well-recorded hectads, separate interval analyses (km per decade; 95% t-interval; n = species)

| group | 1966-75 to 1986-95 | 1986-95 to 2001-10 | 2001-10 to 2015-24 |
|:--|:--|:--|:--|
| butterflies | 28.7 (15.5 to 41.9); n=39 | 14.0 (-8.0 to 36.1); n=32 | 5.8 (-11.6 to 23.1); n=31 |
| carabids | 32.2 (18.1 to 46.4); n=16 | 1.8 (-6.4 to 10.0); n=37 | 20.3 (12.5 to 28.2); n=44 |
| hoverflies | too few | -7.7 (-21.5 to 6.2); n=12 | 36.0 (15.1 to 56.9); n=31 |
| ladybirds | 25.5 (1.6 to 49.4); n=5 | 4.4 (-15.8 to 24.6); n=9 | 51.6 (31.5 to 71.8); n=29 |
| macromoths | 8.4 (5.1 to 11.7); n=431 | 33.7 (29.8 to 37.6); n=446 | 7.5 (3.4 to 11.5); n=395 |
| odonata | 37.6 (23.5 to 51.6); n=19 | 48.5 (20.8 to 76.3); n=24 | 39.3 (22.9 to 55.8); n=27 |
| orthoptera | 10.7 (-1.9 to 23.2); n=14 | 21.1 (5.8 to 36.4); n=16 | 25.3 (0.2 to 50.4); n=17 |
| shieldbugs | too few | 25.3 (9.4 to 41.1); n=16 | 51.4 (34.8 to 68.0); n=34 |
| spiders | too few | 14.9 (7.9 to 21.9); n=27 | 24.2 (15.5 to 32.8); n=23 |

### Mean of group means by effort control (km per decade; 95% bootstrap interval; g = groups) (Figure 4)

| method | 1966-75 to 1986-95 | 1986-95 to 2001-10 | 2001-10 to 2015-24 |
|:--|:--|:--|:--|
| recorded | 34.1 (30.6 to 37.6); 9 g | 20.7 (15.3 to 26.1); 9 g | 25.0 (20.0 to 30.0); 9 g |
| well | 23.8 (19.0 to 29.1); 6 g | 17.3 (12.3 to 22.5); 9 g | 29.0 (23.9 to 34.2); 9 g |
| heavy | 20.3 (15.8 to 25.4); 4 g | 22.5 (14.6 to 30.6); 5 g | 24.8 (18.8 to 31.0); 6 g |
| well_min2rec | 34.7 (28.8 to 40.9); 5 g | 17.8 (13.0 to 22.5); 9 g | 38.4 (33.2 to 43.8); 9 g |
| well_effective_mid | 24.7 (20.0 to 30.0); 6 g | 17.6 (12.9 to 22.8); 9 g | 27.7 (22.7 to 32.9); 9 g |
| rarefied_m10 | 8.9 (3.6 to 14.7); 5 g | 29.3 (23.5 to 35.1); 9 g | 17.9 (10.5 to 25.3); 9 g |
| rarefied_m25 | 6.7 (1.1 to 12.7); 3 g | 24.3 (17.8 to 31.3); 7 g | 21.8 (15.7 to 27.9); 9 g |
| Mason et al. 2015 (scheme atlases, well-recorded) | 23.2 (13 groups) | 18.0 (16 groups) | not available |
| isotherm velocity (HadUK UK) | 38 (34 to 46) | 90 (80 to 108) | 66 (58 to 79) |

The group sets differ between rows and intervals because each group needs at least 3 species that pass the filters.

### Core recording-scheme groups and window choice (mean of group means, km per decade) (Figure 6)

Core groups: butterflies, macro-moths, Odonata, ground beetles, Orthoptera.

| method | 1966-75 to 1986-95 | 1986-95 to 2001-10 | A: 2001-10 to 2015-24 | B: 2001-10 to 2015-19 | C: 2001-05 to 2015-19 |
|:--|:--|:--|:--|:--|:--|
| recorded | 26.8 (22.1 to 31.7) | 25.5 (18.1 to 32.8) | 12.6 (6.2 to 19.4) | -9.1 (-16.4 to -1.8) | 16.6 (10.5 to 22.4) |
| well | 23.5 (18.9 to 28.4) | 23.8 (16.3 to 31.1) | 19.6 (13.2 to 26.2) | 6.5 (-0.4 to 13.6) | 23.6 (18.3 to 28.8) |
| heavy | 20.3 (15.9 to 25.1) | 26.1 (17.4 to 35.0) | 18.5 (11.6 to 25.0) | 3.6 (-3.5 to 10.3) | 25.5 (19.1 to 31.5) |
| rarefied_m10 | 8.9 (3.2 to 14.5) | 24.4 (17.2 to 32.0) | 9.5 (3.9 to 15.0) | 8.5 (0.9 to 15.6) | 11.6 (5.2 to 18.3) |
| rarefied_m25 | 6.7 (1.0 to 12.4) | 22.1 (15.6 to 28.8) | 9.9 (3.8 to 15.1) | 9.2 (1.9 to 15.8) | 11.5 (5.5 to 17.7) |

The UK warming between window means was 0.36 C (A), 0.18 C (B) and 0.06 C (C). Thus the isotherm velocities were 66, 39 and 10 km per decade. Window B compares a 10-year period with a 5-year period. Fewer occupied hectads in the shorter period give a southward bias. Window C uses equal 5-year windows, but the warming between them is small and is mostly year-to-year noise. For window C, the observed rates were larger than the isotherm velocity.

### Paired test on fixed hectads (Figure 3)

| effort level | groups | species | group mean 1986-95 to 2001-10 | group mean 2001-10 to 2015-24 | mean difference | Wilcoxon p | species Spearman rho |
|:--|--:|--:|--:|--:|--:|--:|--:|
| recorded | 9 | 886 | 22.2 | 21.7 | -0.5 | 0.57 | -0.07 |
| well | 8 | 556 | 21.3 | 20.7 | -0.6 | 0.64 | -0.05 |
| heavy | 5 | 324 | 28.7 | 11.6 | -17.1 | 0.13 | 0.03 |

Macro-moths changed most: 36.1 to 1.8 km per decade (well-recorded, 423 species; difference -34.3, -39.7 to -28.9). With equal 5-year windows, the macro-moth rate was 22.7 in the separate analysis. Thus a large part of this drop is due to the window. Forecast scores for the 8 group means (well-recorded): mean absolute error 11.9 for a constant 18 km per decade, 14.7 for the climate-scaled earlier rate, 20.7 for the earlier rate, and 20.7 for no shift (`forecast_scores.csv`).

### Occupancy change (Figure 5)

| method | interval | slope (km per decade per log unit) | mean log occupancy change | raw mean | adjusted mean at no occupancy change |
|:--|:--|--:|--:|--:|--:|
| well | 1966-75 to 1986-95 | 57.2 (SE 4.3) | 0.34 | 23.8 | 2.5 |
| well | 1986-95 to 2001-10 | 55.8 (SE 6.6) | 0.39 | 17.3 | 3.8 |
| well | 2001-10 to 2015-24 | 55.4 (SE 4.2) | 0.07 | 29.0 | 16.6 |
| recorded | 2001-10 to 2015-24 | 71.9 (SE 4.4) | 0.12 | 25.0 | 2.3 |

The adjustment removes real range filling as well as effort effects. Thus the adjusted values are a lower limit, not a better estimate. In the earlier intervals, almost all of the mean shift goes with the increase in occupied hectads.

## Limitations

- GBIF is not the same as the scheme atlases that Mason et al. used. Some scheme data are not in GBIF (for example national spider data), and the scheme data for 2020-2024 are mostly not yet in GBIF. GBIF data change over time. The aggregated hectad counts that we used are included.
- The GBIF density tiles do not give a filter on coordinate uncertainty. We assigned each 0.022-degree bin to a hectad by its centre. A record near a hectad edge can go into the next hectad. Records with coarse locations (for example county centroids) can make a false presence.
- We did not remove non-native or recently introduced species, and we did not check identification quality beyond the GBIF and scheme checks. iNaturalist and iRecord records are in several groups.
- The 10-most-northerly-hectad margin depends strongly on the number of occupied hectads (Figure 5). No effort control in this study removes this dependence completely. Records are not visits, and the meaning of one record changed over time (atlas cards then, single sightings now). This limits the rarefaction method.
- The isotherm velocity uses one gradient for all of Great Britain, and it ignores elevation and east-west differences. With 5-year windows, it is mostly noise.
- The statistics treat species as independent within groups. Species share hectads, recorders and weather. Thus the intervals are probably too narrow.

## Reproduction

```
# prepared Python 3.12 environment plus: pip install mapbox-vector-tile pyproj tabulate
python code/01_species_lists.py data_new                      # GBIF species facets (network)
python code/02_fetch_tiles.py data_new/species_lists.csv tiles.jsonl 20                 # P1-P4 (network, about 1 h)
PERIODS_ONLY=P4b python code/02_fetch_tiles.py data_new/species_lists.csv tiles.jsonl 20
PERIODS_ONLY=P3b python code/02_fetch_tiles.py data_new/species_lists.csv tiles.jsonl 20
python code/03_climate.py <campaign datasets dir> data/metoffice out     # needs shared Berkeley, GHCN-CAMS, Met Office England
python code/04_elevation.py hectad_elevation.csv                        # OpenTopoData (network)
python code/07_effective_years.py out; python code/09_dataset_sources.py out/gbif_top_datasets.csv
# from the bundle data (no network):
gunzip -k data/hectad_counts.jsonl.gz
python code/05_margins.py data/species_lists.csv data/hectad_counts.jsonl data/hectad_elevation.csv out ne_10m_land.zip
ALT_P4=1 python code/05_margins.py ... out_alt ...;  ALT_P4=2 python code/05_margins.py ... out_alt2 ...
# copy data/climate_*.csv and data/effective_midpoints.csv into each out dir, then
python code/06_summarise.py out figs;  ALT_P4=1 python code/06_summarise.py out_alt figs_alt;  ALT_P4=2 python code/06_summarise.py out_alt2 figs_alt2
python code/08_compare_windows.py out out_alt out_alt2 figs
```

The rarefaction uses a fixed random seed (20261109). `ne_10m_land.zip` is Natural Earth 10 m land v5 (sha256 e547d749...a922dc). `files/data/provenance.json` gives the hashes and sources of all inputs.

## Files

- `files/code/`: scripts 01-09.
- `files/data/`: species lists, hectad counts for all species and periods (`hectad_counts.jsonl.gz`, one JSON line per species and period: hectad key `E_N` in 10 km units, mapped to record counts), hectad elevations, climate tables, Met Office series, effective midpoints, yearly GBIF record counts by group, top GBIF source datasets, provenance.
- `files/results/main_2001-10_to_2015-24/`: species-level rates (separate, rarefied, fixed-hectad), group and overall summaries, paired tests, forecast scores, occupancy adjustment, effort tables, window comparison, core-group summary.
- `files/results/sens_2001-10_to_2015-19/` and `files/results/sens_2001-05_to_2015-19/`: the same main tables for the sensitivity windows (only the 2001-to-2015 interval rows are valid comparisons in these folders).
- `files/figures/`: Figures 1-6.

## References

- Mason, S.C. et al. (2015) Geographical range margins of many taxonomic groups continue to shift polewards. Biological Journal of the Linnean Society 115:586-597. doi:10.1111/bij.12574
- Hickling, R. et al. (2006) The distributions of a wide range of taxonomic groups are expanding polewards. Global Change Biology 12:450-455. doi:10.1111/j.1365-2486.2006.01116.x
- GBIF.org occurrence data via the GBIF maps API (retrieved 2026-11-09); main source datasets in `files/data/gbif_top_datasets.csv`.
