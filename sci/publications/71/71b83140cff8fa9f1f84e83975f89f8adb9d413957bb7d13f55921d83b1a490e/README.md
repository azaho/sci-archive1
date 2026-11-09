# The 1995 drought collapse of six British butterfly species did not repeat at similar size after the 2003, 2006, 2018 or 2022 droughts

Job: sci-1107-dell-climate-pollution-biodiversity-87219754f399 (campaign 11_07_2026). Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5), operating as an automated research worker. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Oliver et al. (2015, Nature Climate Change 5:941, doi:10.1038/nclimate2746) used the 1995 drought to identify six "drought-sensitive" British butterflies: Ringlet (*Aphantopus hyperantus*), Speckled Wood (*Pararge aegeria*), Large Skipper (*Ochlodes sylvanus*), Large White (*Pieris brassicae*), Small White (*Pieris rapae*) and Green-veined White (*Pieris napi*). Their projections assume that each future drought has the same effect as the 1995 drought. These projections give widespread local extinction of these species by 2050 under high emissions.

England has had four more summers of similar or higher aridity: 2003, 2006, 2018 and 2022. Two of these (2018, 2022) came after the 2015 publication. Thus they are true out-of-sample tests. We asked:

1. Did the six species again decline more than other species in the year after each later drought?
2. Did the species order of the 1995 response (all species, not only the six) predict the species order after each later drought?
3. Within each drought, did transects with more local aridity have larger declines, and was this slope steeper for the six species?

## Data

* UK Butterfly Monitoring Scheme (UKBMS) site indices 1976-2024 (EIDC, doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9) and site locations 2024 (doi:10.5285/d7256b49-f2e3-4ae7-907d-af729610c768). Open Government Licence.
* Met Office HadUK-Grid areal monthly series for England: mean temperature and rainfall, 1884-2026 (Open Government Licence).
* E-OBS v31.0e daily mean temperature and precipitation, 0.25 degree ensemble mean, 1950-2024 (Cornes et al. 2018). Non-commercial licence; not bundled.

Exact URLs, SHA-256 hashes and licences are in `files/DATA_SOURCES.md`. The raw data are not in this bundle. `files/code/get_data.sh` downloads them to a separate folder.

## Methods

**Drought years.** We used the aridity index of Marsh et al. (2007), as Oliver et al. did: the z-score of April-September mean temperature minus the z-score of April-September rainfall. The reference period is 1884-2005 (Figure 1). Years with index 3.0 or more since 1980 are 1995 (3.76), 2003 (3.76), 2006 (3.06), 2018 (4.06) and 2022 (4.62). For rainfall alone, 1995 was the 4th driest April-September since 1884. 2022 was the 6th, 2003 the 17th, 2018 the 21st and 2006 the 68th. 2025 and 2026 were also very arid, but the UKBMS indices stop at 2024.

**Population response (Oliver et al. criterion 1).** For each site and species, we fitted a straight line to log(index + 1) over the six most recent "clean" years before the event year D. "Clean" years exclude drought years and the year after a drought, so that one drought does not change the baseline of the next drought. The response is the observed log(index + 1) in D+1 minus the fitted value in D+1 (lag 1, the main measure). We also calculated lag 0 (year D). We kept a site-species series only if it had 4 or more valid baseline years, a baseline mean index of 2 or more, and a valid index in the response year. We used only standard UKBMS transects in England, Scotland and Wales. We removed Wider Countryside Butterfly Survey squares (2-3 visits per year), index value -2 (insufficient visits), the Essex/Small Skipper aggregate, and three migrants (Painted Lady, Red Admiral, Clouded Yellow). The number of transects in the lag-1 analysis was 236 (1995), 361 (2003), 343 (2006), 711 (2018) and 734 (2022).

**Species score.** The median response over sites, for species with 10 or more sites.

**Tests.** (1) The six-species contrast: the mean score of the six species minus the mean score of the other species. (2) The Spearman rank correlation of species scores between 1995 and each later drought. Uncertainty for both: 400 bootstrap resamples of whole transects. Calibration for both: the same statistic in 28 non-drought "placebo" years (aridity index below 2.4, not the year after a drought, 1982-2021). For the rank correlation, we removed placebo years 1987-1997 because they share data with the 1995 window (21 placebo years remain). (3) Within each drought year: OLS of the site response on local E-OBS aridity (cell z-scores against 1961-2005), with species fixed effects, a local-aridity by six-species interaction, and standard errors clustered by site. Sites farther than 20 km from a valid E-OBS cell were removed.

## Results

**1995 is reproduced in-sample.** In 1996 the six species were 0.83 log units below the other species (95% bootstrap CI -0.94 to -0.65). This is about 56% lower. It is lower than in all 28 placebo years (Figure 2a). Four of the six species had a significant majority of sites below trajectory. This is expected, because the six species were chosen from the 1995 response.

**The six-species contrast did not repeat at similar size (Figure 2a).**

| Drought year | Aridity index | Six minus others, lag 1 (95% CI) | Placebo percentile |
|---|---|---|---|
| 1995 | 3.76 | -0.83 (-0.94, -0.65) | 0 |
| 2003 | 3.76 | -0.32 (-0.41, -0.18) | 14 |
| 2006 | 3.06 | +0.16 (+0.06, +0.30) | 64 |
| 2018 | 4.06 | -0.25 (-0.37, -0.16) | 14 |
| 2022 | 4.62 | +0.02 (-0.08, +0.16) | 32 |

After 2003 and 2018, the six species were lower than the other species, but by less than half of the 1995 contrast. Four of the 28 placebo years had a lower contrast. After 2022, the most arid year in the record before 2025, there was no contrast. The mean contrast of the two post-publication droughts (2018 and 2022) was -0.12. This is at the 15th percentile of all 378 pairs of placebo years. The bootstrap intervals show only transect sampling noise. They are much narrower than the year-to-year spread of the placebo contrasts (5-95%: -0.40 to +0.86), so the placebo percentile is the correct test.

Per species (lag 1, `files/results/species_event_table.csv`): Ringlet was below trajectory after all five droughts (median -0.84, -0.37, -0.10, -0.22, -0.13). Speckled Wood was below after 1995, 2003, 2006 and 2018 (-0.68, -0.27, -0.41, -0.20) but above after 2022 (+0.29). Large White, Small White and Green-veined White had no consistent sign after the later droughts. In our measure, Small White and Green-veined White were not clearly below trajectory in 1996 either (-0.04 and -0.06). Oliver et al. also used two other criteria to select them.

**The 1995 species order partly transferred to 2003 and 2018, but not to 2006 or 2022 (Figures 2b and 3).** Spearman rho with the 1995 scores was 0.54 for 2003 (CI 0.35 to 0.67; above all 21 placebo years), -0.03 for 2006, 0.38 for 2018 (CI 0.15 to 0.46; above 20 of 21 placebo years) and -0.04 for 2022 (CI -0.12 to 0.20; placebo percentile 52). The 2003 and 2018 agreement was also present at lag 0 (rho 0.48 and 0.43), so it is partly a same-summer effect and not only a next-year collapse. With the "change from the year before the drought" measure (Oliver et al. criterion 2), the lag-1 rank agreement was weaker (0.18, 0.11, 0.09, 0.09).

**Local aridity did not predict larger local declines (Figure 4).** For the other species, the lag-1 slope on local aridity was -0.09 (SE 0.10) in 1995, +0.27 (0.07) in 2003, +0.02 (0.08) in 2006, +0.01 (0.04) in 2018 and +0.01 (0.04) in 2022. The six-species slope difference was +0.25 (0.12) in 1995 and +0.03 (0.05) in 2022. Thus in 1995 the six species declined *less* at more arid transects. No drought year had a negative slope that was outside the placebo range. Within-year spread of local aridity was small (SD about 0.5 index units), and the spatial pattern of aridity can correlate with other regional differences. Per-species slopes from 1995 did not predict per-species slopes after the later droughts (rho -0.15 to 0.40, 29-30 species).

**Robustness (`files/results/robustness.csv`).** With species means instead of medians, with a 25-site minimum, or with the migrants included, the lag-1 six-species contrasts were -0.21 to -0.36 for 2003 and 2018 and -0.07 to +0.04 for 2022. The 1995 contrast stayed below all placebo years (-0.83 to -0.97).

## Interpretation

The 1995 collapse of the six species was unusual. Later droughts of equal or higher aridity, including the 2022 drought with a similar rainfall deficit, gave smaller or no group-specific declines. Thus the assumption that every future drought has the 1995 effect was not supported by the four later events. The species ranking of 1995 recurred in two of four events (2003, 2018), so some species-specific drought response may exist, but it was not constant. Possible reasons, which we did not test: differences in drought timing within the season, the following year's weather (for example the wet summer of 2007 after the 2006 drought), changes in habitat and host plants since 1995, and changes in the transect network.

## Limitations

* Only five drought events. The placebo distributions have 21-28 years. Percentiles are coarse.
* The aridity index uses a fixed 1884-2005 reference. Recent warming increases the temperature part, so recent years reach high index values with smaller rain deficits (Figure 1).
* We did not repeat the habitat area and fragmentation analysis of Oliver et al. We did not use land-cover data.
* The UKBMS site index is a GAM-based index that fills gaps in the season. Hot weather can change butterfly activity and detection in the drought year itself; the lag-1 measure reduces but does not remove this effect.
* The transect network grew from about 240 to about 730 sites between 1995 and 2022. New sites are not a random sample. We used only within-site changes, but the species and site mix still differs between events.
* The six-year trajectory baseline can be unstable at sites with few years or low counts. We used thresholds (4 years, mean index 2 or more) that we fixed before we saw the results for later droughts. Other thresholds were tested only as listed above.
* The species criteria of Oliver et al. included a growth-rate versus aridity regression over all years. We did not re-select species with that criterion. We tested their published group of six.

## Files

* `files/figures/` - Figure 1 (aridity), Figure 2 (six-species contrast and rank agreement by year), Figure 3 (species scatter), Figure 4 (spatial slopes).
* `files/results/species_scores.csv` - species median response for each event year and lag (all years 1980-2023).
* `files/results/species_event_table.csv` - per species and drought: sites, median response, fraction below trajectory, Wilcoxon p.
* `files/results/species_transfer.json`, `bootstrap.csv` - main test statistics, CIs and placebo values.
* `files/results/spatial_models.csv`, `spatial_species_slopes.csv` - within-year spatial models (coefficients only).
* `files/results/robustness.csv` - variants.
* `files/code/` - all analysis code; `run_all.sh` and `get_data.sh`.
* `files/DATA_SOURCES.md` - URLs, versions, hashes, licences. `files/NOTICE-external-data.md` - attribution.

## Reproduce

```
bash files/code/get_data.sh /tmp/scratch_datasets      # or use the shared campaign datasets folder
bash files/code/run_all.sh /tmp/scratch_run /tmp/scratch_datasets
```

Python 3.12 with pandas, numpy, scipy, statsmodels, xarray, netCDF4, pyproj, pyarrow and matplotlib. The full run takes about 10 minutes on one machine. The bootstrap uses a fixed seed (1995).

## Attribution

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee. Contains Met Office data licensed under the Open Government Licence v3.0. We acknowledge the E-OBS dataset and the data providers in the ECA&D project (Cornes et al. 2018, J. Geophys. Res. Atmos. 123:9391). See `files/NOTICE-external-data.md`.
