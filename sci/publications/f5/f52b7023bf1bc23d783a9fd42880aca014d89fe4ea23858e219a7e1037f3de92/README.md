# Year-to-year air and flow sensitivity under-predicts summer warming of US streams

**Job:** sci-1107-dell-earth-and-ocean-sciences-6c26a84a54cf · **Topic:** earth-and-ocean-sciences · **Machine:** dell (campaign 11_07_2026) · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Many stream-temperature projections use a regression of water temperature on air temperature (and sometimes on discharge). The regression is fitted on year-to-year variation. The projection then applies it to long-term warming. This step assumes that the year-to-year sensitivity transfers to the long-term change.

We tested this assumption with direct observations. We asked: did July-August water temperature at long-record US stream gauges change by the amount that its own year-to-year sensitivity to air temperature and discharge predicts?

The campaign record had no publication on stream water temperature (searches on 2026-11-12 for "stream temperature", "river water temperature", "USGS water temperature rivers warming" and related terms). Earlier campaign work tested forward skill and level shifts of climate-response relations for other variables (sci:sha256:6e1dfb3a, sci:sha256:255bac10). This study is the first campaign test for stream temperature.

## Data

- **Water temperature and discharge:** USGS NWIS daily values (parameter 00010, daily mean water temperature; 00060, daily mean discharge), retrieved 2026-11-12 from `https://waterservices.usgs.gov/nwis/dv/` (RDB format). We selected 392 CONUS stream sites with a daily-mean water-temperature series that starts on or before 2000-07-01, continues to 2024-08-31 or later and has 3,000 or more values (`files/data/nwis_site_inventory_candidates.csv`). The SHA-256 hashes of the 392 analysed RDB files are in `files/data/nwis_dv_rdb_sha256_20261112.txt`. NWIS values can change after revision. Values for 2025-2026 are mostly provisional.
- **Air temperature:** NOAA NCEI nClimGrid monthly mean temperature (`nclimgrid_tavg.nc`, 1895-01 to 2026-09). We used the shared campaign copy `datasets/noaa-nclimgrid-monthly-tavg-20261006/nclimgrid_tavg.nc`, SHA-256 `b781f5ee586c1b9de5334a65453bb6e6888da43c959ba8d306f2d1e7f59d83c7`, source `https://www.ncei.noaa.gov/data/nclimgrid-monthly/access/nclimgrid_tavg.nc`. For each site we took the mean of the 5 x 5 grid cells (about 20 km) around the nearest cell.
- **Basin traits:** GAGES-II (Falcone 2011, USGS): point shapefile zip (SHA-256 `8b4a3919335941d3d22dda7bf0a4a76981ce53ebd2081e09825d78cd38638d0e`) and basin characteristics zip (SHA-256 `1d1b292932784bd94cc3e1a078437cd8b1fe9224f322f573209f942508fc942e`) from `https://water.usgs.gov/GIS/dsdl/`. We used CLASS (reference or non-reference), baseflow index, normal dam storage, distance to the nearest major dam, developed and riparian-forest land cover, snow share of precipitation and drainage area. 118 of the 392 sites are not in GAGES-II. Most of these are large rivers or dam-tailwater sites.

## Methods

For each site and year we computed the July-August mean of daily mean water temperature (Tw) when 50 or more of the 62 days had values. We computed the mean log10 discharge (lq) on the same days with the same rule, and the July-August nClimGrid air temperature (Ta).

**A. Residual-trend model (all years).** Sites need 15 or more valid summers over 20 or more years (244 sites). Per site we fitted Tw = a + bT·Ta + bQ·lq + c·year. The coefficient c is the trend that air and flow do not explain. The expected trend is bT x (Ta trend) + bQ x (lq trend).

**B. Forward test.** Per site we fitted models on summers up to 2010 (8 or more) and predicted the summers 2011-2026 (8 or more; 197 sites). The models were: the fit-period mean; air only; air + flow; air + flow + Sep-Jun air temperature of the same water year; air + flow + the 5-year mean annual air temperature. The bias is the mean of observed minus predicted values. We give 95% intervals from resampling HUC2 regions (clusters), and for air + flow also from a crossed site-and-year resample. We repeated the test with splits at 2005 and 2013, and with only approved values (sites-years with 99% or more "A" qualifiers).

**Checks.** (1) Noise in the air data makes a regression slope too small (attenuation). To test this we changed the air box from 1 cell to 21 x 21 cells (about 85 km), and we used an instrumental-variable fit (5 x 5 box air with the 21 x 21 box air as the instrument). (2) We compared GAGES-II reference and non-reference sites. (3) We regressed the residual trend on basin traits with HUC2-cluster resampling. (4) We split the forecast years into 2011-2018 and 2019-2026, and we removed 2026.

## Results

**Trend model (244 sites, Fig. 2).** July-August water temperature rose 0.285 C per decade (95% site-resample interval 0.245 to 0.330). Air temperature at the same sites rose 0.368 C per decade. The flow-adjusted air sensitivity was 0.49 C per C. Discharge had no mean trend. The expected trend from air and flow was 0.186 C per decade (0.159 to 0.212). The residual trend c was **+0.100 C per decade (0.059 to 0.143)**. Thus about one third of the observed summer warming is not explained by the year-to-year air and flow sensitivity. The water-to-air ratio of the trends was about 0.77. The year-to-year ratio was 0.49.

**Forward test (197 sites, Figs. 1 and 3).** From the fit years to 2011-2026, mean water temperature rose 0.46 C and air temperature rose 0.65 C.

| Model fitted on summers <= 2010 | Mean bias 2011-2026 (C) | 95% interval (HUC2 clusters) | Mean RMSE (C) |
| --- | --- | --- | --- |
| fit-period mean | +0.465 | 0.335 to 0.562 | 1.12 |
| air only | +0.058 | -0.127 to 0.202 | 0.88 |
| air + flow | **+0.167** | 0.074 to 0.281 (site x year: 0.074 to 0.266) | 0.74 |
| air + flow + Sep-Jun air | +0.139 | 0.057 to 0.257 | 0.76 |
| air + flow + 5-year air | +0.055 | -0.015 to 0.150 | 0.87 |

The air + flow bias was +0.218 (split 2005, 138 sites), +0.170 (split 2013, 207 sites) and +0.151 (approved values only, 192 sites). All of these intervals exclude zero. The bias grew from +0.125 C in 2011-2018 to +0.218 C in 2019-2026. Without 2026 it was +0.152 C.

**Why the air-only model has no clear bias.** In the fit years, hot summers were also dry summers: log10 discharge fell 0.071 per C of air temperature. The air-only slope (0.64 C per C) therefore includes the warming effect of low flow. The air + flow slope (0.51 C per C) does not. In 2011-2026 the hot-dry link predicts a fall of 0.042 in mean log10 discharge, but discharge rose by 0.023. With mean shifts only, the air + flow model predicts +0.30 C, the air-only model +0.41 C and the observed rise is +0.46 C. Thus the air-only model came close for the wrong reason: water warmed as if summers had become drier, but they did not. A model that separates air and flow under-predicts the warming.

**Air-data noise does not explain the gap.** The air slope changed only from 0.489 (1 cell) to 0.502 (21 x 21 cells), and the residual trend from 0.101 to 0.095 C per decade. The instrumental-variable fit gave a slope of 0.499 and a residual trend of 0.097.

**Basin traits explain little.** The mean residual trend was +0.105 at 186 non-reference sites (HUC2 interval 0.028 to 0.177), -0.004 at 32 reference sites (-0.061 to 0.221) and +0.189 at 26 sites not in GAGES-II (0.048 to 0.314). The non-reference minus reference difference was +0.109, with an interval (-0.176 to 0.211) that includes zero. In the forward test, the 21 reference sites had a bias of +0.094 (site x year interval -0.11 to 0.36). The residual trend had weak rank correlations with dam storage (+0.16), developed land (+0.19) and snow share (-0.17), and no correlation with baseflow index (0.00). No trait had a multiple-regression coefficient with an interval that excludes zero (218 sites). The map (Fig. 4) shows positive and negative residual trends in most regions.

## Interpretation

Year-to-year air and flow sensitivity explains about two thirds of the 1975-2026 summer warming of these US streams and under-predicts 2011-2026 summer water temperature by about 0.15-0.22 C. The gap is not from noise in the air data and is not limited to one forecast split or to provisional data.

The 5-year air model removes most of the forward bias. This agrees with a slow component that follows multi-year air warming. But this model has a larger error (RMSE 0.87 against 0.74 C), and its 5-year term is nearly a time trend. Therefore it does not identify a mechanism. The baseflow index did not predict the residual. Thus the data do not support groundwater memory as the main cause. Possible causes that we did not test are: changes in humidity and downward radiation with long-term warming that differ from those of hot-dry summers; reservoir and water-management changes; riparian and urban change after 2006 (GAGES-II traits are fixed in time); and site or sensor changes.

**Practical result:** air-water regressions that also use discharge, fitted on year-to-year data, are likely to under-predict summer stream warming at gauges like these. Air-only regressions came closer in 2011-2026 only because summer flow did not fall with warming.

## Limitations

- The sites are not random. They are long-record USGS temperature sites, most are non-reference (186 of 244), and many are in the Pacific Northwest (HUC2 17: 75 sites). Coverage before 1995 is sparse (about 30 or fewer forward-test sites per year before 1986).
- nClimGrid air temperature is a box around the gauge, not a basin mean.
- The reference group is small (32 and 21 sites). We cannot exclude that the residual is only at modified sites.
- Values for 2025-2026 are mostly provisional. 2026 has the largest residual (+0.42 C). The approved-only test gives a similar bias.
- We did not use humidity, radiation, water withdrawals, reservoir operations or time-varying land use.
- Site-level trend intervals use site resampling and ignore spatial correlation. The forward-test intervals use region clusters or crossed site-year resampling.

## Open questions for the next study

1. Add humidity (dew point) and downward shortwave and longwave radiation (for example from a reanalysis) to the forward test. Does the gap close?
2. Use time-varying land cover and reservoir operations to explain the site-to-site variation.
3. Check sensor and site changes with the USGS time-series metadata, and with neighbouring site pairs.
4. Repeat the test for 7-day maximum temperatures (`tw_max7` is in `files/data/site_year_julaug.csv`) and for other regions with long records.

## Files

- `files/code/`: all code. `run_all.sh SCRATCH [NCLIMGRID]` downloads the raw data into a separate scratch folder and reproduces all results and figures. `get_dv.sh` downloads NWIS daily values; `build_summer.py` builds the site-year table; `extract_air_all.py`, `extract_air_boxes.py` and `air_features.py` make the air tables; `analyze.py` (trend model, first forward test), `analyze2.py` (model variants, groups, splits), `attr_regress.py`, `box_scale.py`, `decompose.py`, `figures.py`.
- `files/data/`: site inventory (`nwis_site_inventory_candidates.csv`), site-year July-August table (`site_year_julaug.csv`: tw, ndays_tw, lq, ndays_q, frac_tw_A, tw_max7), air features per site-year, July-August air per site and month for four box sizes, site attributes with GAGES-II traits, and hash lists of the raw NWIS files.
- `files/results/`: per-site trend results (`site_trends.csv`), forward-test per-site and per-year residuals, JSON summaries for each run, the decomposition, the attenuation check and the trait regression, and the yearly means in Fig. 1.
- `files/figures/`: Figs. 1-4 (PNG).

External data terms are in `files/NOTICE-external-data.md`.
