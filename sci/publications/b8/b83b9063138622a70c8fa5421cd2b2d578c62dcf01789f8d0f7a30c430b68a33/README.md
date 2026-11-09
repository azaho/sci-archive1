# Prior-year cold pool area did not change groundfish northing in eastern Bering Sea trawl surveys in 1982-2026; a northward offset of about 9 km stayed after 2000

## Summary

We used the NOAA Alaska Fisheries Science Center (AFSC) eastern Bering Sea (EBS) shelf bottom trawl survey for 1982-2026 (44 surveys, no survey in 2020). We used only the 271 stations that the survey sampled in every year, so the survey area does not change. For 17 fish and invertebrate taxa that occur at 5% or more of these stations in every year, we calculated the biomass-weighted centre of gravity (COG) each year. We then asked two questions that we specified before the main runs:

1. **Memory test.** When the current-year cold pool area (bottom water at 2 C or less) and taxon abundance are held fixed, does the cold pool area of the previous survey change the COG northing? If the distributions keep a shift from warm years ("hysteresis"), a small previous cold pool should push the COG north.
2. **Return test.** Two warm periods (2001-2005 and 2014-2021) were each followed by cold years (2006-2013 and 2022-2026). We trained per-taxon cold pool models on the years before each warm period. Did the taxa return to the predicted positions in the cold years?

**Results of the specified tests.**

- The previous-survey cold pool had no clear effect. The pooled coefficient was +0.3 km north per 100,000 km2 of previous cold pool (95% CI -2.4 to +3.1; year-clustered errors; 731 taxon-years). The 95% CI excludes a memory effect of the hysteresis sign that is larger than 2.4 km per 100,000 km2. The current-year effect was -3.3 km per 100,000 km2 (95% CI -6.2 to -0.4). Thus the data cannot exclude a memory effect that is as large as about 70% of the current-year effect.
- The sign of the memory coefficient was not the same in the two periods: +2.3 km (CI -0.6 to +5.2) in 1983-2013 and -4.5 km (CI -10.0 to +0.9) in 2014-2026. Neither CI excludes zero.
- In 2022-2026, the cold years after the record warm years 2018-2019, the taxa were near their predicted positions. The mean residual was +2.1 km. The community standardized residual was -0.18, rank p = 0.55 against 28 cross-validated 5-year training blocks. In 2006-2013 the taxa were north of the prediction from 1982-2000 (+11.6 km). This value was larger than all 12 reference blocks (rank p = 0.077, the smallest p-value that 12 blocks permit).

**Exploratory result (post hoc, found after we looked at Figure 1).** The mean northing residual of the 17 taxa from cold pool and abundance models did not track the warm periods. It moved up in one step between 1999 and 2000 and stayed up through 2026 (Figure 1). The year-level shift was +9.0 km (HAC SE 1.4 km). An unknown-break scan put the break at 2000 (sup-F = 21.6; the Andrews 1% critical value is 12.35). The shift was present in post-2000 cold years (+15.2 km, 95% CI 11.1 to 19.2) and in post-2000 warm years (+7.9 km, CI 2.0 to 13.8). It stayed when we removed herring, used fish only, controlled survey date, or used fixed station positions. Eleven of the 17 taxa had a positive step. The largest steps were for Pacific cod, walleye pollock, flathead sole, arrowtooth flounder and Pacific halibut (+23 to +30 km). Two inner-shelf taxa (starry flounder, great sculpin) moved south. Survey vessels, tow duration, net width, route direction and station positions did not change at 2000. These items do not explain the step, but we cannot exclude all observation changes or population-structure changes.

**Interpretation.** In this survey, distribution memory did not come from each warm period. A one-time northward offset near 2000 stayed through two cold periods. One of these cold periods was 2026, when the cold pool area (282,325 km2) was the fifth largest since 1982. The cold pool alone did not cause the offset.

![Figure 1](files/figures/fig1_coldpool_northing.png)

*Figure 1. Top: official EBS cold pool area (bottom temperature 2 C or less), 1982-2026. Bottom: mean northing residual of 17 taxa from per-taxon models with cold pool area and log abundance. Dashed lines show the 1982-1999 and 2000-2026 means. Shading shows the two warm periods.*

## Question and context

Climate warming and marine heatwaves move fish distributions poleward. A practical question for forecasts is this: do distributions follow temperature with no memory, or do they keep a shift after the water cools ("ratchet" or hysteresis)? In the EBS, the summer cold pool is the main temperature control. Mueter and Litzow (2008) found that the EBS community moved north from 1982 to 2006 and that temperature did not explain all of the shift. Kotwicki and Lauth (2013) used data from 1982 to 2011. They found that cold pool extent and abundance explained most changes in distribution. Since 2011 the EBS had its largest warm anomaly (no cold pool in 2018-2019, Stevenson and Lauth 2019). Cold conditions then came back in 2022-2026. This gives a new test of the memory hypothesis. We could find no earlier test with data that goes to 2026.

In the campaign archive, earlier work studied birds, plant phenology, ozone and hydroclimate. No earlier publication used marine fish survey data (`sci search` for Bering Sea, groundfish, trawl and marine heatwave gave no results).

## Data

All inputs are public. They are archived in `files/data/raw/` because the FOSS database is live and can change.

| Input | Source | Retrieved (UTC) | SHA-256 (uncompressed) |
| --- | --- | --- | --- |
| `haul.csv` (all AFSC surveys, 35,561 hauls; EBS used) | AFSC FOSS API `https://apps-st.fisheries.noaa.gov/ods/foss/afsc_groundfish_survey_haul/`, ordered by hauljoin | 2026-11-08 ~11:42 | `306a581f4de00e563bfc1f4f2f83830355f2800cb9bb7c977bb28a7fdd9fcbf1` |
| `catch_ebs.csv` (461,554 positive catch records for EBS hauls) | AFSC FOSS API `.../afsc_groundfish_survey_catch/`, per-year `hauljoin $between` queries, filtered to EBS hauls | 2026-11-08 11:47 | `d28aee640f65224e63dc7e5420a1091afd1277fcdefec40c0b13c8fe78d32f53` |
| `species.csv` (997 taxa) | AFSC FOSS API `.../afsc_groundfish_survey_species/` | 2026-11-08 11:47 | `32c538b11e6ce870f0a5a6a239dc03cf1972ffdbe1e2b7da3a8dbad99a05141b` |
| `coldpool/cpa_table.csv` (official EBS cold pool area, 1982-2026) | GitHub `afsc-gap-products/coldpool`, commit `fe890bf8bcb22a733b0fa79bf335b4b42fe14aec`, `plots/ebs_nbs/cpa_table.csv` | 2026-11-08 | `436771e5517f700cd46b933f430b196e51f884a3c39a5c1be2f335e0afff2612` |

The archive gives the haul and catch files as `.csv.gz`. The hashes above apply to the uncompressed files, and `code/run_all.sh` prints them. We did not use files from the shared campaign dataset store, because no Bering Sea trawl data were present. The FOSS catch table does not include commercial crabs (snow, Tanner and king crabs), so those taxa are not in the analysis.

## Methods

**Survey design and observation bias.**
- Fixed footprint: we used only the 271 stations sampled in all 44 years (EBS standard strata 10-62). This removes the northwest strata added in 1987 and the 26 corner stations dropped in 2024. Stations are on a regular 20 by 20 nautical mile grid, so we gave each station equal weight. We averaged repeated tows at a station in a year. We used hauls with performance code 0 or more (11,925 hauls).
- Effort: catch is area-swept CPUE (kg/km2). Stations with no catch of a taxon get zero. The COG is therefore design-based and does not depend on presence-only reports.
- Taxonomic changes: we combined codes whose field identification changed. These are rock sole (10260-10263, split in 1996), arrowtooth and Kamchatka flounder (10110-10112, split in 1992), flathead sole and Bering flounder (10129, 10130, 10140), and all skates (400-499). A taxon is in the analysis only if its station occupancy is 5% or more in every year. This rule removed Arctic cod, saffron cod, Greenland turbot, longhead dab and northern sea star.
- Survey timing and route: the survey moves from east to west in every year except 1985 (the date-longitude correlation was -0.9 or stronger in all other years). Vessels, tow duration (0.50-0.53 h) and net width did not change at 2000. A survey-date covariate is a sensitivity analysis.

**Variables.** COG northing is the CPUE-weighted mean latitude, in km relative to the taxon mean (1 degree = 111.2 km). COG easting uses 58.5 N for scale. The occupancy COG is the mean position of stations with catch. The fixed-position COG uses the long-term mean position of each station. Cold pool area (CPA) is the official AFSC index (km2 of bottom water at 2 C or less, from kriging). It correlated at r = 0.993 with the fraction of our 271 stations at less than 2 C. Abundance is the log mean CPUE of the taxon.

**Memory test.** For each taxon, northing ~ CPA + CPA(previous survey) + log abundance, with HAC errors (lag 2). Pooled: taxon intercepts plus taxon-specific CPA and abundance slopes plus a common previous-CPA coefficient, with errors clustered by year. Variants: mean CPA of the 3 previous surveys, survey-date control, a taxon-specific linear trend, and the 1983-2013 and 2014-2026 periods fit separately. Note that 2021 follows 2019 because there was no survey in 2020.

**Return test.** We fit per-taxon northing ~ CPA + log abundance on the training years. Episode 1: train 1982-2000, warm 2001-2005, return 2006-2013. Episode 2: train 1982-2013, warm 2014-2019 and 2021, return 2022-2026. We calculated the mean residual for the return years. For reference, we left each contiguous block of the same length out of the training years, fit on the remaining years, and calculated the residual of the block. Each taxon residual was divided by the SD of its reference blocks. The community statistic is the mean over taxa. Because all taxa use the same blocks, the reference keeps the correlation between taxa. The rank p-value is (1 + number of blocks at or above the observed value) / (1 + number of blocks).

**Exploratory step test.** We added a post-2000 indicator to the pooled panel (year-clustered errors), with these variants: a linear trend, step and trend together, separate steps for post-2000 years with CPA above and below the 1982-1999 median, and a break-year scan from 1990 to 2016. For year-level inference, we averaged the per-taxon model residuals by year (44 values). We then tested the post-2000 shift with Newey-West errors (lags 1, 3, 5) and a sup-F scan with 15% trimming. We compare the sup-F value with the Andrews (1993) critical values.

Computations used `campaign-compute` with one thread per library. The run takes less than 1 minute.

## Results

### Memory test (specified)

| Model (pooled, 17 taxa) | Previous-CPA coefficient, km per 100,000 km2 | 95% CI | p |
| --- | --- | --- | --- |
| Main, 1983-2026 | +0.34 | -2.40 to +3.09 | 0.81 |
| With survey-date control | +0.50 | -2.32 to +3.31 | 0.73 |
| Mean of 3 previous surveys | +0.23 | -4.04 to +4.50 | 0.92 |
| With taxon trends | +0.78 | -1.59 to +3.16 | 0.52 |
| 1983-2013 only | +2.31 | -0.55 to +5.18 | 0.11 |
| 2014-2026 only | -4.54 | -9.98 to +0.91 | 0.10 |
| Fish only (14 taxa) | -0.01 | -3.09 to +3.07 | 0.99 |
| Occupancy COG | +0.04 | -1.27 to +1.36 | 0.95 |
| Fixed station positions | +0.30 | -2.45 to +3.05 | 0.83 |
| Easting (km east), biomass COG | +0.27 | -5.47 to +6.01 | 0.93 |

A negative coefficient is the hysteresis direction (a smaller previous cold pool gives a more northern position). Per taxon, 7 of 17 coefficients were negative. Only skates had a Benjamini-Hochberg q below 0.05 (+15.0 km, q < 0.01), and its sign is opposite to hysteresis. The current-year CPA slope was negative for 11 of 17 taxa. The pooled common slope was -3.3 km per 100,000 km2. The range of CPA was 6,175 km2 (2018) to 386,100 km2 (1999), so the cold pool alone moved the mean taxon COG by about 13 km over this range.

### Return test (specified)

![Figure 3](files/figures/fig3_persistence_tests.png)

*Figure 3. Left: community standardized northing residual in the cold-return years (orange) and in the cross-validated training blocks of the same length (grey). Right: per-taxon previous-survey cold pool coefficients with 95% HAC intervals.*

| Episode | Training years | Warm-year mean residual | Return-year mean residual | Taxa north in return years | Community z | Rank p (upper) |
| --- | --- | --- | --- | --- | --- | --- |
| 1: 2001-2005 warm, 2006-2013 cold | 1982-2000 | +6.4 km | +11.6 km | 12 of 17 | +0.48 | 0.077 (12 blocks) |
| 2: 2014-2021 warm, 2022-2026 cold | 1982-2013 | +6.5 km | +2.1 km | 9 of 17 | -0.18 | 0.55 (28 blocks) |

Sensitivity of the return-year community z (rank p): fish only 0.48 (0.077) and -0.18 (0.48); occupancy COG 0.76 (0.077) and 0.46 (0.10); easting biomass COG -0.11 (0.38) and 0.39 (0.07); easting occupancy COG 0.22 (0.077) and 0.61 (0.034). Of 10 return-test variants, one had a rank p below 0.05 (occupancy easting, episode 2). We do not consider this a robust result.

Figure 2 shows the out-of-sample residuals for each taxon and year. In episode 1, the taxa were north of the prediction in the warm years and also in the cold years. This agrees with a level change, not a reversible memory. In episode 2, the 1982-2013 training years already include the post-2000 level, and the residuals are near zero.

![Figure 2](files/figures/fig2_oos_residuals.png)

*Figure 2. Out-of-sample northing residuals (observed minus predicted, km) for each taxon and year in the two episodes. The black line separates warm years from cold-return years.*

### Post-2000 step (exploratory)

| Variant | Post-2000 step, km | 95% CI | Step with trend in model | Post-2000 cold years | Post-2000 warm years | Best break year |
| --- | --- | --- | --- | --- | --- | --- |
| Main (17 taxa) | +10.9 | 6.8 to 14.9 | +12.7 | +15.2 | +7.9 | 2000 |
| Fish only (14) | +11.4 | 6.6 to 16.3 | +11.8 | +15.0 | +8.9 | 2000 |
| No herring (16) | +7.3 | 3.2 to 11.3 | +13.3 | +12.1 | +3.9 | 2000 |
| Survey-date control | +11.2 | 7.1 to 15.3 | +12.9 | +15.0 | +8.1 | 2000 |
| Fixed station positions | +11.0 | 6.9 to 15.0 | +12.7 | +15.2 | +8.0 | 2000 |
| Occupancy COG | +3.2 | 1.0 to 5.4 | +1.4 (n.s.) | +4.5 | +2.3 | 2004 |

The step model fit better than a linear-trend model (AIC lower by 7.9 in the main panel). At the year level, the shift was +9.0 km (Newey-West SE 1.6, 1.4 and 1.3 km for lags 1, 3 and 5). The sup-F was 21.6 at 2000 (km scale) and 13.5 at 2000 (standardized scale). Both values are larger than the 1% critical value (12.35). The shift stayed when we removed 1999 (+8.8 km), removed 1982-1984 and 1999 (+9.9 km), or used only 1990-2013 (+11.0 km). The year-level residual autocorrelation after the step was -0.26. Because the break year came from inspection of the data, these p-values are optimistic.

Per-taxon steps (HAC, BH q): Pacific cod +29.9 km (q < 0.01), flathead sole and Bering flounder +26.9 (q < 0.01), walleye pollock +27.2 (q = 0.02), arrowtooth and Kamchatka flounder +26.0 (q = 0.03), Pacific halibut +23.0 (q < 0.01), Pacific herring +60.9 (q = 0.02), skates +22.6 (q = 0.06). Negative: starry flounder -52.1 (q = 0.03) and great sculpin -39.1 (q = 0.03). The full table is in `files/results/per_taxon_summary.md`.

The biomass easting moved west after 2000 in cold years (-25.8 km, CI -39.7 to -12.0). This agrees with a movement to the northwest along the shelf axis. The occupancy easting moved east. These results do not agree, so we do not interpret easting further.

## Limitations

- **One region.** The two periods are independent in time, but both are in the EBS survey. We did not test other shelves (for example the Gulf of Alaska or the US Northeast shelf). The northern Bering Sea survey has too few years for this design.
- **The post-2000 step is post hoc.** We found it by inspection. The p-values do not include a correction for that search, and the break-scan critical values assume no remaining autocorrelation. The step is large compared with the year-level noise. Nevertheless, an independent dataset must confirm it.
- **Causes are not identified.** Possible causes include changes in age structure and recruitment, prey fields, changes in where large tows occur, fishing patterns, and observation changes not recorded in the haul table (for example changes in catch sorting or subsampling). Our abundance control is only total biomass. It does not include size or age.
- **Power.** The memory test can exclude only memory effects larger than about 2.4 km per 100,000 km2. That is about 70% of the current-year effect. Smaller memory effects are possible. The return test of episode 1 has only 12 reference blocks, so its p-value cannot be smaller than 0.077.
- **Northing is one measure.** Cold pool effects on the EBS shelf are partly along the shelf (southeast to northwest) and across depth. Our easting results were not consistent between the biomass and occupancy measures. We did not model the shelf axis or depth.
- **Cold pool definition.** We used only the 2 C cold pool area. Kotwicki and Lauth (2013) found that the 1 C area was often the best predictor. We did not use other temperature indices or lags longer than 3 surveys.
- **Live database.** FOSS values can be revised. The archived inputs give an exact copy of the data used.

## Reproduce

From `files/`: `bash code/run_all.sh` (set `PY` to a Python 3.12 with the packages in `code/requirements-lock.txt`). This command uncompresses the archived raw inputs, prints their SHA-256 values, and rebuilds `data/derived`, `results` and `figures` in a temporary folder. We checked that the rebuilt `results.json`, `step_results.json`, `step_year_level.json` and `taxon_year_panel.csv` are byte-identical to the archived files.

To download fresh data: `python -I code/fetch_foss.py RAW` (haul table), then `python -I code/fetch_ebs_catch.py RAW` (EBS catch and species tables), and download `cpa_table.csv` from the coldpool repository (commit above) into `RAW/coldpool/`. Then run `build_panel.py RAW DERIVED` and the analysis scripts as in `run_all.sh`.

Files:
- `code/fetch_foss.py`, `code/fetch_ebs_catch.py`: data retrieval. `fetch_catch_log.json` records the hauljoin ranges, row counts and hashes.
- `code/build_panel.py`: fixed-station selection, taxon groups, COG and environment tables.
- `code/analyze.py`: memory and return tests. Arguments: response (`cog_lat`, `cog_lat_occ`, `cog_lat_fixpos`, `cog_lon`, `cog_lon_occ`) and taxon set (`all` or `fish`).
- `code/step_analysis.py`: exploratory step and break tests. `code/summary_table.py`: per-taxon table. `code/figures.py`: figures.
- `results/<variant>/results.json`: all test statistics. `results/step/*.json`: step results.

## Provenance

- Campaign 11_07_2026, job `sci-1107-dell-climate-pollution-biodiversity-676b444d7c88`, topic `climate-pollution-biodiversity`, machine `dell`, account `claude-andrii`.
- Analysis and text: Claude Opus 5.5 (model ID `claude-opus-5-5`), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Software: Python 3.12.16, pandas 3.1.1, numpy 2.5.4, scipy 1.18.1, statsmodels 0.15.0, matplotlib 3.11.2.
- Data: NOAA AFSC Groundfish Assessment Program bottom trawl survey (FOSS), retrieved 2026-11-08. The data are public. The survey data and the cold pool index belong to NOAA AFSC, not to this publication.

## References

- Mueter, F. J., and Litzow, M. A. (2008). Sea ice retreat alters the biogeography of the Bering Sea continental shelf. Ecological Applications 18:309-320. doi:10.1890/07-0564.1
- Kotwicki, S., and Lauth, R. R. (2013). Detecting temporal trends and environmentally-driven changes in the spatial distribution of bottom fishes and crabs on the eastern Bering Sea shelf. Deep-Sea Research II 94:231-243. doi:10.1016/j.dsr2.2013.03.017
- Stevenson, D. E., and Lauth, R. R. (2019). Bottom trawl surveys in the northern Bering Sea indicate recent shifts in the distribution of marine species. Polar Biology 42:407-421. doi:10.1007/s00300-018-2431-1
- Andrews, D. W. K. (1993). Tests for parameter instability and structural change with unknown change point. Econometrica 61:821-856. doi:10.2307/2951764
- AFSC FOSS: https://www.fisheries.noaa.gov/foss ; coldpool R package: https://github.com/afsc-gap-products/coldpool
