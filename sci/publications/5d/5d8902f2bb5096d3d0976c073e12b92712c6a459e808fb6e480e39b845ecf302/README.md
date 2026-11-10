# Satellite input changes step the spatial detail of DOISST v2.1 and ESA CCI v3 daily SST and cause most 1982-2021 trends of SST front fraction and small-scale variance (60S-60N)

## Summary

Three campaign studies (sci:sha256:f50dc28f..., sci:sha256:87b87a67..., sci:sha256:69a00227...) found that the NOAA daily Optimum Interpolation SST (DOISST v2.1) lost fast, day-to-day variance in steps at satellite input changes. Two more studies found that this artifact reaches daily memory, variance and marine heatwave statistics. All of these studies examined the time dimension at single points. None examined the spatial structure of the daily fields.

Many climate statistics use the spatial structure of daily SST: front detection, SST gradients, front intensity in boundary currents and upwelling systems, and the size of anomalies. For example, Xing et al. (2024, Nature Communications) reported a global increase of persistent front occurrence and intensity in 1982-2021 from a daily satellite SST analysis of the ESA CCI / C3S family.

**Question.** Do the satellite input changes also change the spatial detail of daily SST analyses? If so, how much of the reported 1982-2021 change in SST fronts and gradients is a property of the products?

**Approach.** We calculated spatial statistics of every daily DOISST v2.1 field in 1982-2025 on the full 0.25-degree grid (465,873 ice-free pixels, 60S-60N, 16,071 days). The statistics are the SST gradient magnitude at four spatial scales, the front fraction (area with gradient above 2 or 4 K per 100 km), the small-scale variance (variance below a 1.25-degree boxcar mean) and the gradient of the anomaly field. We tested for steps at the dates of the documented DOISST input changes against all other dates. We repeated the calculation on the same pixels for the satellite-only ESA SST CCI Analysis v3.0.1 on 1,020 sampled days (the 1st and 16th of each month, 1982-2024). We then compared both products with in situ SST from 148 pairs of moorings 100-400 km apart.

**Main results.**

1. **DOISST spatial detail changes in steps at its input changes, and the sign depends on the region.** At 1985-01-14 and 2020-07-07, the fields became smoother in most regions (global small-scale variance x0.78 and x0.84). At the two documented input changes (2007-01-01, Pathfinder to Navy AVHRR; 2021-11-01, change to ACSPO L3S), the fronts of the western boundary currents became sharper, but the tropics became smoother. In the Gulf Stream box, the small-scale variance changed by x2.81 at 2007-01-01 and by x2.21 at 2021-11-01. In 20S-20N, it changed by x0.74 and x0.71. In the same days, the temporal day-to-day variance decreased at every date (x0.55 to x0.71). Thus temporal smoothing and spatial sharpening are not the same effect.
2. **The steps are largest at the smallest scales.** In the Gulf Stream box, the 2007 step of the mean gradient was +27% for a 56 km baseline and +10% for a 445 km baseline.
3. **ESA CCI v3 has its own spatial steps, at the dates of its dual-view sensors.** A break search with no prior dates placed the largest breaks of the CCI small-scale variance at 1991-08-16 (x1.29; ATSR-1 data start in August 1991), 2012-04-16 (x0.83; Envisat and AATSR were lost on 2012-04-08) and 2016-06-01 (x1.24; SLSTR-A data start), and at 1985-01-16 (x1.25). CCI has no step at the DOISST dates.
4. **Moorings confirm the steps of both products.** Relative to the buoys, the DOISST variance of the 1-day change of the 100-400 km SST difference decreased by 0.32 ln units at 2007 (113 of 129 pairs; p = 1e-18) and by a further 0.75 at 2022 (59 of 61; p = 1e-11). The buoys did not change (-0.04, -0.03). At 2007, the total DOISST difference variance decreased relative to tropical moorings (-0.33, p = 5e-8) and increased relative to mid-latitude buoys (+0.07, p = 0.005), the same signs as in the gridded fields. At mid-latitude NDBC buoys, the CCI difference variance relative to the buoys increased by +0.22 when ATSR started (p = 0.002), decreased by 0.08 after AATSR ended (p = 0.04) and increased by +0.18 when SLSTR started (p = 2e-4). DOISST did not change at these dates.
5. **The steps cause most 1982-2021 trends of front fraction and small-scale variance.** In CCI, the global front fraction trend was +9.7% per decade (95% interval 5.9 to 13.3). With step terms at the three sensor dates (fixed a priori), it was +3.8% (0.4 to 7.5). Inside 1992-2011 it was +1.3% (-0.7 to 3.2). In DOISST, the raw trends of the boundary-current boxes (for example Gulf Stream small-scale variance +23% per decade, Brazil-Malvinas +25%, Agulhas mean gradient +5.9%) became -7% to -1% with one step term at 2007-01-01. In 1985-2006, these boxes had no trend.
6. **One change remains in both products.** After the step terms, the mean gradient decreased in both products: global -2.3% per decade (DOISST) and -1.3% to -2.2% (CCI), and -4% to -8% per decade in 20S-20N. We could not find out whether this decrease is real.

**Conclusion.** Daily SST analyses do not have a constant effective spatial resolution. Their spatial detail changes in steps when satellite inputs change. The sign of the change depends on the product, the date and the region. Some steps move the product nearer to the buoys (for example DOISST in the tropics at 2007, CCI at mid-latitudes when ATSR or SLSTR data start). But an improvement in resolution is still a false trend. Trend studies of SST fronts, gradients and small-scale variability must use step terms at the input dates or compare homogeneous segments. Our results do not show that SST fronts did not change. They show that the products can not give the trend without such a control.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| DOISST v2.1 daily mean SST, AVHRR-only, 0.25 degree, 1982-2025 | NOAA PSL `sst.day.mean.YYYY.nc`, 44 files, read in place from the shared campaign store | Main analysis, all days |
| ESA SST CCI Analysis L4 v3.0.1, 0.05 degree (CDR3.0 to 2021, ICDR3.0 from 2022) | CEDA OPeNDAP, stride subset to the DOISST 0.25-degree pixel centres, 1st and 16th of each month, 1982-01-01 to 2024-06-16 (1,020 days, all retrieved) | Independent satellite-only reference |
| Daily buoy SST (52 NDBC, 159 GTMBA) and DOISST at the buoy cells | Archived in sci:sha256:87b87a67... (verified bundle) | In situ test |

Exact URLs, shared paths, SHA-256 hashes and the CCI request hashes are in `files/provenance/`. Terms and attribution of the external data are in `files/NOTICE_external_data.md`.

## Methods

**Grid and mask.** We used the DOISST 0.25-degree pixel centres from 59.875S to 59.875N. The CCI stride-5 points coincide with these centres; they are point samples of the 0.05-degree CCI analysis, not 0.25-degree means. A pixel is in the mask if DOISST has a value on every day of 1982-2025 and the minimum SST is above -1.0 C (465,873 pixels). For the comparison with CCI, a pixel must also have CCI values on all 1,020 sampled days (464,228 pixels).

**Anomalies.** For each pixel and product, we removed a least-squares fit of a constant, a linear trend and three annual harmonics (DOISST: all days 1982-2025; paired comparison: the sampled days of each product).

**Daily spatial statistics.** For each day:
- Gradient magnitude |grad SST| from central differences over +-1, 2, 4 and 8 pixels (baselines 56, 111, 222 and 445 km at the equator), in K per 100 km.
- Front fraction: the area fraction with |grad SST| above 2 K per 100 km (`front2`) or 4 K per 100 km (`front4`), on the +-1 pixel gradient.
- Small-scale variance `res2`: mean of (SST minus its 5 x 5 pixel boxcar mean)^2.
- Anomaly gradient `ga2` and the Taylor length scale of the anomaly field, L = sqrt(2 var(a) / mean |grad a|^2).
- Temporal reference `dd2`: mean of (a_t - a_t-1)^2.
We calculated cos(latitude)-weighted means over 13 regions: 60S-60N, 20S-20N, 20N-60N, 60S-20S, four western boundary current boxes (Gulf Stream, Kuroshio, Agulhas, Brazil-Malvinas), four eastern boundary upwelling boxes and the equatorial Pacific (box limits in `code/common.py`). We also saved annual 1-degree maps.

**Step tests at known dates.** For each statistic (ln, day-of-year median removed), the step is the mean of the 120 days after a date minus the mean of the 120 days before it. The null distribution is the same step at all other dates (every 7 days, more than 200 days from the five test dates; 1,977 dates). We give the ratio exp(step), z = step / SD(null) and a two-sided empirical p-value. For the sampled CCI days we used 24 samples (about one year) on each side. The test dates are the documented DOISST input changes (2007-01-01, 2021-11-01), the dates of earlier DOISST day-to-day variance steps (1985-01-14, 2017-03-02, 2020-07-07; from sci:sha256:87b87a67...) and approximate CCI sensor dates (1991-08-01 ATSR-1, 1995-06-01 ATSR-2, 2002-06-01 AATSR and AMSR-E, 2006-12-01 MetOp-A, 2011-10-04 end of AMSR-E, 2012-04-08 end of Envisat, 2016-05-01 SLSTR-A, 2022-01-01 ICDR). We did not check the CCI dates against the CCI input counts. We also used binary segmentation (mean shifts, 8 splits, minimum 180 days; for sampled days 6 splits, minimum 12 samples) with no prior dates.

**Trends.** OLS slopes of annual means of the ln statistic, in % per decade, with 95% moving-block bootstrap intervals (3-year blocks, 2,000 draws). Step terms are the fraction of each year after the step date. We fixed the step models before the fit: DOISST 2007-01-01 (for 1982-2021); CCI 1991-08-01, 2012-04-08 and 2016-05-01 (and a variant that adds 1985-01-14). We also fitted trends inside segments with no documented change (DOISST 1985-2006 and 2007-2020; CCI 1992-2011).

**Mooring pairs.** We used all pairs of moorings of the same network that are 100-400 km apart and have 3 or more years of common data (148 pairs: 74 GTMBA, 74 NDBC). The daily SST difference D = SST_i - SST_j comes from the buoys and from DOISST at the two buoy cells, on the same days. We removed the anomaly model from D for each source. For each pair-year (250 or more days) we calculated the variance of D (`var_all`), of D minus its 31-day running mean (`var_hp`) and half the variance of its 1-day change (`var_dd`). We compared ln(DOISST / buoy) between 1985-2006, 2007-2020 and 2022-2025 inside each pair (paired Wilcoxon test, bootstrap interval of the median). For the three-way test with CCI, we used the 1,020 sampled days and the same DOISST pixel as the prior bundle (we found the pixel by value matching on three days), and calculated `var_all` per pair and period.

## Results

### R1. DOISST spatial statistics step at the input-change dates

Global (60S-60N) steps, ratio after / before (120-day windows; z against 1,977 other dates):

| Statistic | 1985-01-14 | 2007-01-01 | 2017-03-02 | 2020-07-07 | 2021-11-01 |
| --- | --- | --- | --- | --- | --- |
| Temporal day-to-day change `dd2` | 0.70 (z -4.6) | 0.68 (-5.0) | 0.71 (-4.4) | 0.64 (-5.8) | 0.55 (-7.7) |
| Mean gradient, 56 km | 0.91 (-7.7) | 0.98 (-1.7) | 0.99 (-1.2) | 0.94 (-5.3) | 0.99 (-0.7) |
| Front fraction > 2 K/100 km | 0.77 (-6.2) | 1.08 (1.8) | 0.98 (-0.5) | 0.94 (-1.5) | 1.05 (1.1) |
| Front fraction > 4 K/100 km | 0.65 (-4.7) | 1.69 (5.7) | 1.01 (0.1) | 0.95 (-0.6) | 1.19 (1.9) |
| Small-scale variance | 0.78 (-6.1) | 1.13 (3.0) | 1.01 (0.1) | 0.84 (-4.3) | 1.13 (3.1) |

The global means hide opposite regional changes (Figures 1-3). At 2007-01-01, the small-scale variance changed by x2.81 in the Gulf Stream box (p = 0.001), x1.97 in Brazil-Malvinas (p = 0.008), x1.68 in Kuroshio (p = 0.011), x1.63 in Agulhas (p = 0.001) and x0.74 in 20S-20N (p = 0.005). The mean gradient changed by x1.27, x1.23, x1.15, x1.19 and x0.89. At 2021-11-01, the Gulf Stream small-scale variance changed by x2.21 (p = 0.013) and the 20S-20N value by x0.71 (p = 0.002). With annual means (2007-2010 against 2003-2006), the small-scale variance step was +103% (Gulf Stream), +115% (Brazil-Malvinas), +76% (Agulhas), +38% (Kuroshio) and -27% (20S-20N). The break search with no prior dates placed breaks of the global mean gradient at 1985-01-13, 2007-01-01 and 2020-07-07, and of the global small-scale variance at 1985-01-13, 2007-01-01 and 2020-05-30.

### R2. The steps decrease with spatial scale

For all dates and regions, the size of the gradient step decreases from the 56 km baseline to the 445 km baseline (Figure 2). Examples: Gulf Stream 2007, +27% to +10%; Kuroshio 2007, +15% to +5%; 20S-20N 2007, -11% to 0%; 60S-60N 1985, -9% to -5%. Thus the steps are a change of the effective resolution of the analysis, not a change of the large-scale SST pattern.

### R3. ESA CCI v3 has spatial steps at its own sensor dates

On the same pixels and days, the CCI small-scale variance had breaks (no prior dates) at 1985-01-16 (x1.25), 1991-08-16 (x1.29), 2012-04-16 (x0.83), 2016-06-01 (x1.24), 2017-10-01 (x1.08) and 2018-12-01 (x1.11). The known-date tests (about one year on each side) gave, for the front fraction and the small-scale variance: ATSR-1 start 1991-08-01, x1.14 (p = 0.017) and x1.15 (p = 0.017); end of Envisat 2012-04-08, x0.91 (p = 0.044) and x0.88 (p = 0.019); SLSTR-A start 2016-05-01, x1.16 (p = 0.015) and x1.23 (p = 0.006). At the DOISST date 2007-01-01, CCI changed by x1.02 (p = 0.55) and x0.97 (p = 0.42). The ln ratio DOISST / CCI shows the steps of both products (Figure 4). The CCI steps at the start of ATSR-2 (1995) and AATSR/AMSR-E (2002) were small and not significant.

### R4. Moorings confirm the steps in both products

All days, 148 pairs (129 with data before and after 2007; 61 before and after 2022). Change of the median ln(DOISST / buoy) variance of the 100-400 km SST difference:

| Part of the difference | 1985-2006 to 2007-2020 | 2007-2020 to 2022-2025 | Buoys alone (same changes) |
| --- | --- | --- | --- |
| 1-day change `var_dd` | -0.32 (113 of 129 negative, p = 1e-18) | -0.75 (59 of 61, p = 1e-11) | -0.04, -0.03 |
| Sub-monthly `var_hp` | -0.10 (p = 3e-6) | -0.36 (p = 5e-11) | 0.00, -0.03 |
| Total `var_all` | -0.04 (p = 0.006) | -0.08 (p = 2.5e-4) | +0.02, +0.03 |

By network, at 2007 the total difference variance of DOISST decreased relative to the tropical GTMBA moorings (-0.33, 56 pairs, p = 5e-8) and increased relative to the mid-latitude NDBC buoys (+0.07, 73 pairs, p = 0.005), as in the gridded fields. In the same pairs, the buoys' own variance changed by +0.09 (GTMBA, p = 0.02) and +0.01 (NDBC, p = 0.66). Before 2007, DOISST had more 100-400 km variance than the tropical moorings (median ln ratio +0.39) and less than the NDBC buoys (-0.47). After 2007 the values were +0.07 and -0.41. Thus the 2007 change moved DOISST nearer to the buoys in both regions.

Three-way test on the sampled days (Figure 5, right column). At the NDBC buoys, ln(CCI / buoy) changed by +0.22 from 1985-1991 to 1992-2001 (41 pairs, p = 0.002), by -0.08 from 2007-2011 to 2012-2016 (65 pairs, p = 0.04) and by +0.18 from 2012-2016 to 2017-2021 (63 pairs, p = 2e-4). In the same periods, ln(DOISST / buoy) changed by +0.08 (p = 0.12), -0.02 (p = 0.74) and +0.03 (p = 0.32). At the NDBC buoys, CCI is nearest to the buoys when dual-view sensor data are present (median ln ratio -0.04 in 2017-2021, -0.26 in 2012-2016).

### R5. Trends of front statistics and the effect of step terms

1982-2021 trends (% per decade, 95% interval), on the sampled days for CCI and on all days for DOISST (Figure 6; all regions in `results/`):

| Statistic, region | DOISST raw | DOISST with 2007 step | CCI raw | CCI with 3 sensor steps | CCI 1992-2011 only |
| --- | --- | --- | --- | --- | --- |
| Front fraction, 60S-60N | +3.3 (-0.4, 6.8) | -4.0 (-9.3, 1.3) | +9.7 (5.9, 13.3) | +3.8 (0.4, 7.5) | +1.3 (-0.7, 3.2) |
| Small-scale variance, 60S-60N | +2.4 (-1.0, 5.9) | -5.6 (-9.8, -1.3) | +10.3 (4.9, 15.6) | +2.8 (-2.8, 8.6) | -1.0 (-4.4, 2.0) |
| Mean gradient, 60S-60N | -2.0 (-2.8, -1.1) | -2.3 (-3.9, -0.8) | +1.6 (0.0, 3.2) | -1.3 (-3.2, 0.6) | -2.6 (-3.7, -1.5) |
| Mean gradient, Gulf Stream | +4.2 (2.1, 6.3) | -1.8 (-4.2, 0.5) | +2.9 (0.8, 5.1) | +1.1 (-2.2, 4.5) | -0.3 (-3.2, 2.5) |
| Small-scale variance, Gulf Stream | +23.1 (14.4, 32.1) | -3.7 (-9.3, 2.2) | +12.5 (6.2, 18.9) | +10.6 (1.9, 19.9) | +6.8 (-2.1, 15.5) |
| Mean gradient, Agulhas | +5.9 (3.4, 8.4) | -0.9 (-3.2, 1.4) | +4.2 (2.3, 5.9) | +3.0 (0.5, 5.6) | +2.2 (-0.6, 5.0) |
| Mean gradient, Brazil-Malvinas | +7.8 (4.5, 11.4) | -1.8 (-4.5, 0.9) | +3.8 (2.3, 5.3) | +0.6 (-2.2, 3.8) | -0.7 (-3.5, 2.2) |
| Mean gradient, 20S-20N | -8.0 (-9.8, -6.3) | -4.2 (-6.3, -1.9) | -3.6 (-5.3, -1.9) | -6.8 (-9.5, -4.0) | -8.5 (-10.4, -6.6) |

The fitted step sizes of the CCI front fraction were +26% (ATSR-1), -14% (end of Envisat) and +23% (SLSTR-A); the fitted DOISST 2007 step was +23%. In DOISST, the trends inside 1985-2006 were near zero in all boundary-current boxes (for example Gulf Stream mean gradient -1.4% per decade, -3.4 to 0.4). Inside 2007-2020, some boxes had positive trends (Kuroshio mean gradient +4.0%, 0.1 to 8.1; 20N-60N front fraction +5.2%, 1.1 to 9.1). The break search also found smaller DOISST breaks in 2013 and 2016-2017, so these segment trends can also contain input effects.

### R6. What remains

- After the step terms, both products show a decrease of the mean gradient, mainly in 20S-20N (DOISST -4.2, CCI -6.8 to -8.0% per decade). The two products agree in sign, but both have strong steps in this region. The moorings cannot test it, because GTMBA pairs show product-to-buoy changes of the same size. We do not know whether it is real.
- The DOISST anomaly length scale did not show a clear step or trend (2007 step x0.90, p = 0.07; 1982-2021 trend -2.7% per decade raw, -1.1% with the step term).

## Interpretation

The effective spatial resolution of an optimal interpolation analysis depends on the density, the noise and the resolution of its inputs. When the inputs change, the analysis changes. In DOISST, the 2007 change to Navy AVHRR (two satellites) and the 2021 change to ACSPO L3S (several satellites) put more data into each day. In the tropics, where real small-scale gradients are weak, the noise decreased and the fields became smoother. Near strong fronts, real small-scale structure was resolved better and the fronts became sharper. In CCI, the dual-view ATSR, AATSR and SLSTR radiometers add high-quality data, and the fields become sharper when these sensors are present. The moorings show that several of these steps move the product nearer to the in situ truth. But in a time series, each step is a false trend.

The front and gradient trends of a daily SST analysis can thus come from the observing system. The size of the sensor steps in CCI v3 (+23% to +26% in the front fraction) is larger than the global trends that Xing et al. (2024) reported for a product of the same family (+2.4% per decade in occurrence, +5.6% in intensity). We did not repeat their method or use their product version, so we can not give the artifact share of their result. Our results show that such a trend needs a test for steps at the sensor dates.

## Limitations

- We used one front definition (a fixed gradient threshold on a 0.25-degree grid), not the histogram front algorithm of Xing et al. or other algorithms. CCI values are point samples of the 0.05-degree analysis, and DOISST values are 0.25-degree analysis values. Thus the levels of the two products are not comparable; only their changes are.
- CCI is sampled on 2 days per month. Its step dates have a resolution of about 2 weeks, and the known-date tests use about one year on each side.
- The CCI sensor dates are approximate mission dates. We did not check them against the CCI input counts. The cause of the 1985 step in both products is not known (in DOISST it is also a step of the temporal variance; in CCI it can be the start of NOAA-9 data).
- The empirical p-values come from overlapping windows and do not correct for multiple testing over statistics and regions. The block bootstrap intervals use 40 annual values and are approximate.
- Step terms at fixed dates can absorb part of a real trend. The segment trends do not have this problem, but they are short and can contain smaller input changes (DOISST 2013, 2016-2017; CCI 1985, 2017-2018).
- Buoy SST data are DOISST inputs, and buoys measure at one point near 1 m depth. The mooring pairs sample only the tropical moorings and US coastal waters. No pair is in a western boundary current front. The three-way CCI test uses few pairs before 1992.
- The analysis covers 60S-60N with a fixed ice-free mask. Polar fronts and sea-ice edges, where Xing et al. found the largest trends, are not in this study.

## Reproduction

`files/code/run_all.sh` lists all steps. Run it from a work directory whose parent contains the campaign links `datasets/` (shared DOISST files) and `campaign/` (prior SCI bundles). Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib is necessary. The CCI download takes about 3 hours (24 parallel OPeNDAP requests to CEDA). The DOISST statistics take about 4.5 CPU-hours. The raw CCI subset and the DOISST files are not in this bundle; `fetch_cci_grid.py` writes the CCI subset into `scratch/`, outside the publication folder. To check the statistics without the raw data, start from `files/data/` and the statistics scripts.

## Files

- `files/code/`: all code. `common.py` (grid, regions, metrics), `doisst_spatial.py` (DOISST passes), `fetch_cci_grid.py`, `paired_spatial.py`, `stats_tools.py` (step tests, break search, bootstrap), `analysis_doisst.py`, `segment_trends.py`, `analysis_paired.py`, `adjusted_trends.py`, `buoy_pairs.py`, `buoy_pairs_cci.py`, `buoy_pairs_networks.py`, `figures.py`, `provenance.py`, `pack_derived.py`, `run_years.sh`, `run_all.sh`.
- `files/data/doisst_daily_spatial_metrics_1982_2025.csv.gz`: all daily statistics for all 13 regions (columns `metric|region`).
- `files/data/doisst_annual_maps_1deg.npz`: annual 1-degree maps of the mean gradient, front fraction, small-scale variance and day-to-day change.
- `files/data/paired_doisst_cci_sampled_days_metrics.csv.gz` and `paired_annual_grad_maps_1deg.npz`: both products on the 1,020 sampled days (columns `metric|region|product`).
- `files/data/masks_0p25deg.npz`: the ice-free and paired masks.
- `files/results/`: step tests (`doisst_known_date_tests.csv`, `doisst_steps.json`, `paired_steps.csv`, `cci_breaks.json`), trends (`doisst_trends.csv`, `doisst_segment_trends.csv`, `paired_trends.csv`, `adjusted_trends.csv`), annual means, and mooring-pair results (`buoy_pairs_*.csv`, `buoy_pairs_*.json`).
- `files/figures/`: Figures 1-6.
- `files/provenance/`: `data_provenance.json` (DOISST shared paths, URLs and SHA-256; CCI request description; reused prior-bundle files) and `cci_requests.csv.gz` (date, CDR/ICDR and SHA-256 of each OPeNDAP response).
- `files/NOTICE_external_data.md`: terms and attribution of the external data.

## Figures

- `fig1_doisst_daily_series.png`: daily DOISST statistics for 60S-60N, the Gulf Stream box and 20S-20N.
- `fig2_scale_dependence.png`: DOISST gradient steps against the gradient baseline.
- `fig3_step_maps.png`: maps of the change of the 1-degree mean gradient across 2007 and 2021-2022, DOISST and CCI.
- `fig4_doisst_vs_cci.png`: annual means of both products and the ln ratio DOISST / CCI on the same days.
- `fig5_mooring_pairs.png`: product / buoy variance of the SST difference between moorings, by network.
- `fig6_trends.png`: 1982-2021 trends with and without step terms, by region.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-a8ccb2df20cf. Topic earth-and-ocean-sciences. Machine dell. Account claude-sci. Model Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. Date 2026-11-10.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- DOISST files: shared campaign datasets `noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109`, read in place; hashes re-computed and compared with the dataset records (`provenance/data_provenance.json`). CCI: retrieved from CEDA on 2026-11-10. Buoy data: reused from sci:sha256:87b87a67... .

## References

- Lee, C., Song, H., Choi, Y., Cho, A., Marshall, J. (2025). Observed multi-decadal increase in the surface ocean's thermal inertia. Nature Climate Change 15, 308-314. doi:10.1038/s41558-025-02245-w
- Xing, Q., Yu, H., Wang, H. (2024). Global mapping and evolution of persistent fronts in Large Marine Ecosystems over the past 40 years. Nature Communications 15, 4090. doi:10.1038/s41467-024-48566-w
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007). Daily high-resolution-blended analyses for sea surface temperature. Journal of Climate 20, 5473-5496. doi:10.1175/2007JCLI1824.1
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Scientific Data 11, 326. doi:10.1038/s41597-024-03147-w
- ESA SST CCI Analysis L4 v3.0 dataset. doi:10.5285/4a9654136a7148e39b7feb56f8bb02d2
