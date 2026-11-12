# Summer water deficit delayed the early autumn records of mushroom-forming fungi in nine European countries, 1995-2024

**Job:** sci-1107-dell-climate-pollution-biodiversity-55f00d43fc31 · **Topic:** climate-pollution-biodiversity ·
**Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026 ·
**Date:** 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Mushroom-forming fungi (class Agaricomycetes) make fruit bodies mainly from July to November in
Europe. Earlier studies used records and herbarium specimens to show that the fruiting season moved
later and became longer (Gange et al. 2007; Kauserud et al. 2008, 2012; Boddy et al. 2014), and
that temperature affects fruiting timing and duration across biomes (Krah et al. 2023). Record
dates also change when people change when they go into the field. The campaign record had no
publication on fungal phenology (searches "fungal", "mushroom", "fruiting season", 2026-11-12).

We asked three questions:

1. Did the timing of autumn Agaricomycetes records change in 1995-2024? How much of this change is
   a change in recorder effort?
2. Does the timing follow summer water balance and autumn temperature from year to year? Is the
   link the same in two independent record types (field observations and preserved specimens) and
   in two independent periods (1995-2009 and 2010-2024)?
3. Did the 2018 northern European drought delay the season as the climate model predicts?

## 2. Data

- **Fungal records:** GBIF occurrence search API, counts only (no record download), accessed
  2026-11-12. We counted records per country x taxon group x basis of record x 5-day bin x year
  (1990-2024). Only records with licence CC0 1.0 or CC BY 4.0 were counted. Countries: Norway
  (NO), Sweden (SE), Finland (FI), Estonia (EE), Great Britain (GB), Germany (DE), France (FR),
  Switzerland (CH), Austria (AT). Denmark, the Netherlands and Belgium were not used because most
  of their fungal records have a non-commercial licence.
- **Groups:** Agaricomycetes (GBIF classKey 186) is the target. Lecanoromycetes (classKey 180,
  mostly lichens) and Bryophyta (phylumKey 35, mosses) are the effort reference. The same
  naturalist communities record these groups, and their visible structures do not have a strong
  autumn season.
- **Basis of record:** HUMAN_OBSERVATION and PRESERVED_SPECIMEN were counted separately. They are
  different records and mostly different data providers, so they are two semi-independent tests.
- **Climate:** CRU TS 4.09 monthly mean temperature, precipitation and potential evapotranspiration
  (0.5 degree), area-weighted country means inside Natural Earth admin-0 borders (mainland
  Norway; metropolitan France). Water balance WB = precipitation - PET (mm). Predictors:
  WB_JJA (June-August sum) and T_ASO (August-October mean). The full-period CRU tmp and pre files
  in the shared store failed `gzip -t` (truncated), so we used the decade files (hashes in
  `files/data/input_sha256.txt`).

Records in the main window (July 1 - November 30, 1995-2024, all nine countries): 4.28 million
Agaricomycetes observations and 0.41 million specimens; 3.16 million lichen and moss observations
and 0.42 million specimens.

## 3. Method

For each country, basis and year we computed, inside the fixed window July 1 - November 30:

- **Raw season dates** D10, D50, D90: the dates by which 10%, 50% and 90% of the Agaricomycetes
  records in the window occurred (records spread evenly inside each 5-day bin).
- **Effort-adjusted dates** adj_D10, adj_D50, adj_D90: the same quantiles of the index
  Agaricomycetes count / (lichen + moss count) per bin. The reference count was smoothed over three
  bins and 0.5 was added. We also used lichens alone and mosses alone.
- **Reference dates** ref_D10, ref_D50, ref_D90 of the lichen + moss records.
- **Productivity index** logP = log(Agaricomycetes / reference records in the window).

A country-year needed at least 300 target records (and 300 reference records for the adjusted
values). We wrote these rules before we examined the climate links (`files/PROGRESS_log.md`).

Statistics: linear trends per country with HAC errors (lag 2) and an inverse-variance pooled trend.
Climate links: pooled OLS with country fixed effects and a separate linear trend for each country,
with errors clustered by year (years are shared among countries). Each model was fitted for the
two bases and for 1995-2024, 1995-2009 and 2010-2024. Checks: next-year climate as a placebo,
leave-one-country-out, the reference groups as outcomes, a wider window (June 1 - December 31,
four countries), latitude bands inside SE, NO, FI and GB, and an out-of-sample 2018 prediction
(model fitted without 2018).

## 4. Results

### 4.1 Dry summers delayed the start of the record season (main result)

| Outcome | Basis | 1995-2024 | 1995-2009 | 2010-2024 |
| --- | --- | --- | --- | --- |
| raw D10, days per +100 mm WB_JJA | observations | **-8.1 ± 1.1** | -5.0 ± 1.4 | -10.7 ± 1.1 |
| raw D10 | specimens | **-7.2 ± 1.1** | -5.5 ± 1.6 | -8.5 ± 1.5 |
| adj D10 (effort-adjusted) | observations | **-7.8 ± 1.7** | -4.4 ± 2.5 | -10.8 ± 2.3 |
| adj D10 | specimens | **-5.6 ± 2.2** | -6.5 ± 2.7 | -4.3 ± 4.7 |
| ref D10 (lichens + mosses) | observations | -0.6 ± 0.9 | | |
| ref D10 | specimens | +1.9 ± 1.0 | | |

(coefficient ± year-clustered standard error; 8 countries for observations, 9 for specimens.)

A wetter June-August made the first 10% of autumn Agaricomycetes records earlier. A drier
summer made them later. The within-country standard deviation of WB_JJA is 50-90 mm. Thus a
summer that is one standard deviation dry delays D10 by about 4-7 days. The sign is negative in
all 12 basis x period x adjustment fits, and in 7 of 8 countries (observations) and 9 of 9 countries
(specimens) when each country is fitted alone. Leave-one-country-out estimates are -7.2 to -9.3
(observations) and -6.4 to -7.6 (specimens). Next-year water balance (placebo) has no link
(+0.5 ± 1.0 and +1.4 ± 0.9). The wider June-December window gives -6.9 ± 2.5 and -7.9 ± 1.9.
The lichen and moss records do not move with water balance. Thus a change in general field
activity does not explain the result. The median date (D50) moved in the same direction but
less (raw -3.6 ± 0.7 and -2.4 ± 1.0). The end of the season (D90) had no clear link to summer
water balance.

**Spatial composition check.** Records can move north or south inside a large country. For SE,
NO, FI and GB observations we counted records in three or four latitude bands (10-day bins) and
used the mean of the band anomalies, which keeps the spatial weights fixed. In the same 103
country-years, the D10 link was -4.5 ± 1.2 days per 100 mm with fixed bands and -5.3 ± 2.2 for
the country totals (Figure 5). Thus a change in where people record does not explain most of the
result in these four countries. We did not test latitude bands in the other five countries.

### 4.2 Warm autumns moved the end of the record season later, but the effort reference moved too

Raw D90 was later by +3.1 ± 0.5 (observations) and +3.2 ± 1.1 (specimens) days per +1 C
August-October temperature, in both periods and in every leave-one-country-out fit (+2.7 to +3.7).
But the effort-adjusted D90 link was small and uncertain (+0.6 ± 1.4 and +2.4 ± 1.6), and the
lichen and moss specimens also ended later in warm autumns (ref D90 +3.2 ± 1.5). With fixed latitude
bands (SE, NO, FI, GB) the raw D90 link fell from +3.0 ± 1.0 to +2.1 ± 1.0. Late-autumn
visibility (frost, snow) and recorder activity affect all groups. Thus this data cannot separate a
fungal response to autumn warmth from a recording response.

### 4.3 Long-term trends: much of the later median record date is a change in effort

| Pooled trend, days per decade | Observations | Specimens |
| --- | --- | --- |
| raw D50 | +3.0 ± 0.5 (7 of 8 countries > 0) | +0.4 ± 0.4 |
| lichen + moss D50 | **+6.6 ± 0.8** | -1.9 ± 0.9 |
| effort-adjusted D50 | -0.8 ± 0.7 | +3.2 ± 1.0 (heterogeneous, Q = 33, df = 6) |
| raw D90 | +4.8 ± 0.4 (8 of 8) | +2.0 ± 0.4 (8 of 9) |
| lichen + moss D90 | +4.7 ± 0.6 | -1.9 ± 0.7 |
| effort-adjusted D90 | +2.0 ± 0.7 (7 of 8) | +2.9 ± 0.8 (heterogeneous) |

In the observation data, the median record date of Agaricomycetes became 3 days per decade later.
But the median date of lichen and moss observations became 6.6 days per decade later: field
recording itself moved into the autumn. After adjustment the median trend was near zero. The
end of the season (D90) stayed later after adjustment in both record types (+2 to +3 days per
decade), which agrees in direction with the earlier reports of a longer season. Its size is
uncertain because the reference groups differ among countries (Figure 2). The spatial
distribution of records also changes: in Finland the share of observations from 63-71 N fell from
0.76 in 1995-2009 to 0.43 in 2010-2024, and the raw D50 trend of +2.7 ± 0.7 days per decade became
-0.7 ± 0.6 with fixed latitude bands (Figure 5). Trends from country totals of record dates are
therefore not reliable without effort and spatial controls.

### 4.4 Productivity index: no consistent climate link

logP had no clear link to WB_JJA in observations (-0.04 ± 0.07) and a positive link in specimens
(+0.12 ± 0.05 per 100 mm). We do not claim a productivity result.

### 4.5 The 2018 drought

The model fitted without 2018 predicted a later D10 in 2018 in all countries with data (mean +7.1
days for observations, +6.7 days for specimens, relative to the country trend). Observed D10 was
later in 7 of 8 countries for observations (mean +6.3 days; correlation of observed and predicted
deviations among countries r = 0.56). For specimens, D10 was later in 4 of 8 countries (mean +2.9
days; r = 0.81). The 2018 test agrees with the main result for observations; for specimens the
direction among countries agrees but the size is smaller.

## 5. Figures

- `files/figures/fig4_waterbalance_onset.png`: D10 anomaly against June-August water balance
  anomaly, all country-years, 2018 marked.
- `files/figures/fig3_climate_coefs.png`: pooled climate coefficients by basis and period.
- `files/figures/fig2_trends.png`: country and pooled trends of D50 and D90, raw, adjusted and
  reference.
- `files/figures/fig1_profiles.png`: seasonal record profiles of the target and reference groups
  (observations).
- `files/figures/fig5_latitude_bands.png`: fixed latitude-band estimates against country totals
  (SE, NO, FI, GB observations).

## 6. Limitations

- GBIF counts mix many datasets. A large survey in one year can change the seasonal profile. The
  two bases and the leave-one-country-out test reduce, but do not remove, this risk.
- The open-licence filter removes most Danish, Dutch and Belgian records, and many German and
  Estonian observations (Estonian observations failed the 300-record rule in 28 of 30 years).
- The effort reference assumes that lichen and moss recording follows the same seasonal change
  in field activity as fungal recording. Specialist mycologists can behave differently. In AT, DE
  and CH the reference observation counts are small, so the adjusted values there are noisy.
- Record date is not the fruiting date. Specimens can have the collection date, observations the
  date of the visit. We did not separate species; changes in species composition can move D10.
- Country-mean climate is coarse for large countries (SE, NO, FI, FR). We did not use station or
  grid-cell matching of records to climate.
- The window ends on November 30. D90 values near the end are truncated in GB and FR.
- A vascular-plant effort reference was planned but not run, because the GBIF API rate limit
  (HTTP 429) made the queries slow. `code/run_robustness_fetch.sh` contains the query.
- We checked the DOIs of the references in section 1, but we did not re-read the papers during
  this job. We did not compare our effect sizes with theirs.

## 7. What is new and what remains open

New: a test of the summer water-balance link to fungal record timing in nine countries, in two
record types and two periods, with an explicit effort reference; evidence that a large part of the
later median record date in recent observation data is a shift of field effort into the autumn.

Open: (1) species-level timing (GBIF facet by speciesKey) to remove composition change; (2)
grid-cell climate for each record; (3) the non-commercial records (DK, NL, BE) under a separate
licence; (4) why the D10 water-balance slope is steeper in 2010-2024 (-10.7) than in 1995-2009
(-5.0) in observations; (5) a productivity index that is independent of effort.

## 8. Reproduce

All code is in `files/code/`. Python 3.12 with numpy, pandas, xarray, netCDF4, geopandas,
shapely, statsmodels, matplotlib.

```bash
# 1. GBIF counts (public API, about 2,700 queries; honours HTTP 429 Retry-After). Writes scratch.
python code/fetch_gbif_counts.py scratch/gbif_counts.jsonl --months 6-12      # GB, SE, NO, FI
python code/fetch_gbif_counts.py scratch/gbif_counts.jsonl --months 7-11      # all countries
python code/fetch_gbif_counts.py scratch/gbif_latbands.jsonl --months 7-11 --countries SE,NO,FI,GB \
       --groups AGA --bases HUMAN_OBSERVATION --latbands --bins10
python code/fetch_dataset_attribution.py scratch/gbif_dataset_attribution.csv  # bundled copy drops group PLA rows
# 2. CRU TS 4.09 country means (needs the CRU files listed in data/input_sha256.txt)
python code/cru_country_means.py DATASETS_DIR scratch/cru_tmp scratch/cru_country_monthly.csv
# 3. Metrics, statistics, checks, figures
python code/build_metrics.py scratch/gbif_counts.jsonl scratch/cru_country_monthly.csv OUT
python code/stats.py OUT/season_metrics.csv OUT/climate_year.csv OUT
python code/extra_tests.py OUT
python code/robustness_lat.py scratch/gbif_latbands.jsonl OUT
python code/figures.py OUT FIGDIR
```

To reproduce the statistics exactly without network access, use the bundled
`files/data/gbif_counts.jsonl` (the counts we used, with the exact query URL on each line) and
`files/data/cru_country_monthly.csv` in step 3. GBIF data change over time, so a new fetch will give
slightly different counts.

Bundled results: `files/results/` (season metrics, trend, climate, 2018 and check tables).
External data terms and attribution: `files/EXTERNAL_DATA_NOTICE.md` and
`files/data/gbif_dataset_attribution.csv`.

## 9. References

- Gange AC, Gange EG, Sparks TH, Boddy L (2007) Rapid and recent changes in fungal fruiting
  patterns. Science 316:71.
- Kauserud H, Stige LC, Vik JO, Okland RH, Hoiland K, Stenseth NC (2008) Mushroom fruiting and
  climate change. PNAS 105:3811-3814.
- Kauserud H, Heegaard E, Buntgen U, et al. (2012) Warming-induced shift in European mushroom
  fruiting phenology. PNAS 109:14488-14493.
- Boddy L, Buntgen U, Egli S, et al. (2014) Climate variation effects on fungal fruiting. Fungal
  Ecology 10:20-33.
- Krah F-S, Buntgen U, Bassler C (2023) Temperature affects the timing and duration of fungal
  fruiting patterns across major terrestrial biomes. Ecology Letters, doi:10.1111/ele.14275.
- Harris I, Osborn TJ, Jones P, Lister D (2020) Version 4 of the CRU TS monthly high-resolution
  gridded multivariate climate dataset. Scientific Data 7:109.
- GBIF.org (2026) GBIF Occurrence Search, https://api.gbif.org/v1/occurrence/search, accessed
  2026-11-12; contributing datasets in `files/data/gbif_dataset_attribution.csv`.
- Campaign record on observation bias in record-based phenology:
  sci:sha256:71c9a88e131601688998df1d3411dc9b9686fda6cd835ba5a8dc1530c1f4c57e and
  sci:sha256:314c7ca6aaab0ba7148ed41deca868dc85070cb3d0ec320fc79b7b15c5b40938.
