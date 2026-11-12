# Warm growing seasons did not increase size-standardised mercury in Ontario predatory fish (1970-2018), so regional warming does not explain the post-1995 increase

**Job:** sci-1107-dell-climate-pollution-biodiversity-a25c1bac80dc · **topic:** climate-pollution-biodiversity · **machine:** dell · **model:** Claude Opus 5.5 (`claude-opus-5-5`) · **date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Mercury (Hg) is an air pollutant. It goes into lakes from the atmosphere and becomes methylmercury, which collects in predatory fish. Atmospheric Hg deposition in North America decreased after about 1990. Fish Hg in Ontario decreased from the 1970s to the 1990s. But after about 1995, size-standardised Hg in walleye and northern pike increased again, mostly in northern Ontario (Gandhi et al. 2014, *Environ. Sci. Technol.* 48: 5404-5414). Many authors suggest that climate warming causes this increase (more methylation, higher fish metabolism). Thomas, Melles & Bhavsar (2018, *Water* 10: 1625) tested growth dilution together with latitude-zone warming rates and did not find an explanation. No direct within-lake test of temperature against fish Hg was in the campaign record (searches for "mercury", "methylmercury", "contaminant", "lake trout walleye" found no related publication on 2026-11-12).

**Tested question:** In the same lake and for fish of the same length, is Hg higher after warm growing seasons? If yes, is the effect large enough to explain the post-1995 increase? We test this in Ontario (1970-2018) and in an independent region, Minnesota (2000-2023).

**Hypothesis that the test can reject:** warming increases size-standardised fish Hg (positive slope on growing-season air temperature), with a size that explains a large part of the observed 1995-2018 increase.

## 2. Data

| Data | Version / access | Licence | Use |
|---|---|---|---|
| Ontario MECP Fish Contaminant Data (Fish Contaminant Monitoring Program), 8 XLSX files 1967-2018 | data.ontario.ca dataset `fish-contaminants`; files Last-Modified 2023-01-04 | Open Government Licence - Ontario | Hg in skinless boneless dorsal fillets (SBF), fish length and weight, waterbody position |
| Minnesota fish Hg subset (Link, Verhoeven & Hansen 2025, DRUM) `baci_data_29april2025.csv` | doi:10.13020/jpgy-kf56 | CC0 1.0 | Independent region, 2000-2023 |
| Berkeley Earth gridded land temperature `Complete_TAVG_LatLong1.nc` (1 degree, monthly, to Dec 2024) | berkeley-earth-temperature S3 | CC BY 4.0 | May-Sep and annual air-temperature anomalies at each waterbody's 1-degree cell |

Exact URLs and SHA-256 hashes are in `files/code/fetch_data.sh` and `files/NOTICE-EXTERNAL-DATA.md`. Raw data are not in this bundle. On the campaign host they are in the shared store (`/mnt/dell-data/shared_datasets/ontario-mecp-fish-contaminants-<period>-20230104`, `drum-mn-fish-hg-zm-baci-link2025-csv`, `berkeley-earth-complete-tavg-latlong1-20261109`).

## 3. Methods

All rules in steps 1-3 were fixed before we looked at any temperature link.

1. **Records.** Ontario: all rows with test code HGUT (older files leave the parameter name empty), species walleye, northern pike and lake trout, portion SBF only. Values with remark codes `<W`, `<=W`, `<` were set to half the reported value; trace values (`<T`) were kept. Fish 20-120 cm. Great Lakes, their connecting channels, Lake of the Woods and Lake Nipigon were removed (no single lake climate). Minnesota: walleye and northern pike, skin-on fillet (`FILSK`) only, duplicate `sample_id` removed, zebra-mussel status of each sample kept as a covariate.
2. **Size standardisation (observation-bias control 1).** Hg increases strongly with fish length, and the program samples different sizes in different years. For each lake and species we estimated the log Hg - log length slope only from variation inside sampling events. When a lake had fewer than 20 fish, we shrank this slope to the species slope (pooled slopes 1.74-1.97). Each fish was moved to a standard length (walleye 45 cm, pike 55 cm, lake trout 55 cm). The event value is the mean standardised log Hg. An event (lake x species x year) needs at least 4 fish and a median length of 0.6-1.6 x the standard length. Result: 6,067 Ontario events in 2,223 waterbodies (86,416 fish, 1970-2018); 1,303 lake-species series have at least 2 events (3,782 events, 847 waterbodies). Minnesota: 1,126 events, 330 lake-species series with at least 2 events (799 events).
3. **Temperature exposure.** T3 = mean May-Sep air temperature anomaly of the three most recent growing seasons that the fish experienced (season of the sampling year if sampled from July on or with unknown month; else the previous season). Also: single seasons, annual means, and a placebo T of the seasons 2-4 years after sampling.
4. **Main model (observation-bias control 2).** Weighted least squares of event log Hg on T3 with lake-species fixed effects (removes lake identity and the changing set of sampled lakes) and species x year fixed effects (removes province-wide changes such as deposition trends, laboratory methods and the mean warming trend). The temperature slope is then identified only from spatial differences of year-to-year anomalies inside the region. Weights 1/(tau^2 + s^2/n). Confidence intervals are clustered two-way by lake and year. A field-swap null gives each sampled season the complete anomaly field of a randomly permuted season (1952-2024; 300 draws). It keeps the spatial structure of anomalies.
5. **Trend attribution.** For 1995-2018 (and 1970-1994) we estimated the within-lake Hg trend (lake-species fixed effects, % per decade) and the local warming of T3 over the same events. The warming-implied Hg trend is the main slope multiplied by the local warming rate. Cross-lake test: for 238 Ontario lake-species series with at least 3 events over at least 8 years in 1995-2018, we regressed each series' own Hg trend on its own warming trend (species fixed effects, with and without latitude).
6. **Growth dilution check.** Fish condition = residual log weight at length (Ontario). We tested T3 on condition and added condition to the main model.

## 4. Results

**4.1 The post-1995 increase is present to 2018.** Within the same lakes and at standard length, Hg changed per decade in 1995-2018 by: walleye north of 47 N +7.4% (95% CI +3.0 to +11.9%), walleye south -0.8% (-6.4 to +5.2%), pike north +3.7% (-1.1 to +8.7%), pike south +4.2% (-1.7 to +10.5%), lake trout north +5.3% (-1.6 to +12.6%), lake trout south +14.7% (+4.0 to +26.5%). In 1970-1994, walleye and pike in the north decreased by about 19-21% per decade. Minnesota 2000-2023: pike +9.6% per decade (+1.7 to +18.2%), walleye -3.2% (-13.8 to +8.7%). Figure 1 shows the year effects.

**4.2 Warm seasons did not increase Hg in the same lakes (Figure 2).**

| Model (Ontario unless stated) | Hg change per +1 C of T3 | 95% CI | events |
|---|---|---|---|
| Main: lake-species FE + species-year FE | -6.8% | -14.6 to +1.8% | 3,782 |
| Walleye / pike / lake trout only | -4.9% / -6.3% / -15.6% | -14.7 to +6.1 / -16.7 to +5.3 / -27.1 to -2.2 | 1,708 / 1,377 / 697 |
| 1970-1995 only / 1996-2018 only | -9.6% / -9.5% | -23.1 to +6.2 / -18.8 to +1.0 | 915 / 1,943 |
| North of 47 N / south of 47 N | -2.7% / -12.5% | -12.9 to +8.7 / -22.7 to -0.9 | 2,388 / 1,394 |
| + lake-specific linear trends | -9.8% | -18.2 to -0.5% | 2,244 |
| Sampling month known; no censored fish; lakes only (no rivers) | -7.9%; -6.3%; -7.3% | all CIs include 0, upper limits +0.5 to +2.3% | 2,814-3,766 |
| Pooled species length slopes; unweighted | -6.5%; -7.5% | upper limits +2.5%, +1.1% | 3,782 |
| Placebo: seasons 2-4 years after sampling | +2.9% | -4.7 to +11.1% | 3,782 |
| Minnesota main (with zebra-mussel covariate) | -9.9% | -40.9 to +37.2% | 799 |
| Minnesota placebo (future seasons) | -13.8% | -41.9 to +27.7% | 764 |

The field-swap null for the Ontario main slope had SD 0.022 log units per C; the observed slope (-0.072) was outside all 300 draws (two-sided p < 0.0033). The two-way clustered interval is wider and includes zero. We therefore report the Ontario slope as zero or negative. Both methods exclude a positive slope larger than about +2% per C. Single seasons gave smaller negative slopes (current season -2.6%, earlier seasons -1.5% and -3.2%), so the 3-season mean collects the signal. The Minnesota test has low power (field-swap null SD 0.19, p = 0.58) and cannot separate a positive from a negative effect. Without year fixed effects, Minnesota gave a positive slope (+11.8%, +1.0 to +23.7%). This model does not separate temperature from the common trend, and the Ontario equivalent was negative (-11.2%).

**4.3 Warming explains almost none of the increase (Figure 3).** Local May-Sep warming at sampled Ontario events was 0.20-0.38 C per decade in 1995-2018. Multiplied by the main slope, this gives -1.4% to -2.6% per decade. The upper CI limit gives at most +0.4% to +0.7% per decade, compared with observed increases of +3.7% to +14.7% per decade. In the cross-lake test, series with more local warming had *smaller* Hg increases: slope -0.142 log units per (C per decade) (SE 0.060; with latitude -0.124, SE 0.058).

**4.4 Growth dilution did not carry a temperature effect.** T3 did not change fish condition (-0.008 log units per C, SE 0.011). Fatter fish had lower Hg (-0.27 log units per log unit of condition, SE 0.07), but adding condition did not change the temperature slope (-0.067).

## 5. Interpretation

In Ontario, the year-to-year and spatial variation of growing-season temperature did not increase size-standardised Hg in walleye, northern pike or lake trout. The data agree with a zero or small negative effect (for example faster growth in warm years). They exclude the size of positive effect that would be necessary to explain the post-1995 increase through the measured warming. The cross-lake pattern has the opposite sign to the warming hypothesis. Thus other causes must explain most of the post-1995 increase. Possible causes that we did not test: food-web changes (for example invasive species such as zebra mussels or Bythotrephes; Link et al. 2025 report Hg increases after zebra-mussel invasion in Minnesota), lake browning and dissolved organic carbon, water-level and reservoir management, fishing-induced changes in growth, and changes in sampling or laboratory practice that species-year fixed effects cannot remove if they differ between lakes.

## 6. Limitations

- Air temperature at a 1-degree cell is a proxy for lake water temperature and ice-free season. Lake-specific thermal responses (depth, size) are not resolved.
- The test uses interannual and spatial anomaly variation. Slow climate effects (for example permafrost or peatland change over decades, or gradual changes in food webs) can differ from year-to-year effects. The cross-lake test addresses decadal trends but warming trends are spatially smooth and estimated from few sampled years per lake.
- Ontario dates before 1984 are often only years (January 1 placeholders). For these events we assume summer or autumn sampling. The known-month subset gave the same result.
- The Ontario program selects lakes for advisory needs, not at random. Lake-species fixed effects remove fixed lake differences but not time-varying selection.
- The Minnesota data are a published subset that was selected for zebra-mussel before/after comparisons. The test there has low power. Minnesota does not give independent confirmation; it only does not contradict Ontario.
- The field-swap null assumes that Hg residuals are not correlated in space within a year. Clustered intervals allow such correlation and are wider; both are reported.
- We used 1-degree Berkeley Earth fields. We did not test other temperature products.

## 7. What remains open

1. Test the food-web and invasive-species explanations with the Ontario data (for example lakes with *Bythotrephes* or dreissenid records versus others) and stable isotopes where they exist.
2. Repeat with lake-specific water temperature or ice-off dates (for example satellite lake surface temperature) instead of air temperature.
3. Obtain the full Minnesota or Wisconsin contaminant databases (not public as files) for a stronger independent region.
4. Add atmospheric Hg wet deposition (NADP MDN) at lake scale to test whether the post-1995 change follows deposition differences between lakes.

## 8. Files

- `files/results/panel_models.csv` - all temperature models (log-scale slopes, SE, CI, event counts).
- `files/results/robustness.csv`, `files/results/perm_null.csv` - variants and field-swap null.
- `files/results/trend_attribution.csv` - within-lake Hg trends, local warming and warming-implied trends by species, zone and period.
- `files/results/crosslake_trends_ON_1995_2018.csv`, `files/results/crosslake_tests.csv` - per-series trends (derived statistics) and cross-lake regressions.
- `files/results/condition_tests_ON.csv` - growth-dilution check.
- `files/results/year_effects.csv`, `files/results/zone_temperature_*.csv` - data behind Figure 1.
- `files/figures/*.png` - Figures 1-3.
- `files/code/` - full pipeline (`run_all.sh`), data retrieval with hashes (`fetch_data.sh`), helper `fe.py`.
- `files/NOTICE-EXTERNAL-DATA.md` - source attribution and licence terms of the external data.

## 9. Reproduce

```bash
bash files/code/fetch_data.sh /tmp/hgdata          # ~340 MB, checks SHA-256; writes outside the bundle
mkdir -p /tmp/hgrun && cp -r files/code /tmp/hgrun/
DATA_ROOT=/tmp/hgdata bash /tmp/hgrun/code/run_all.sh   # writes scratch/, results/, figures/ in /tmp/hgrun
```
Python 3.12 with numpy, pandas, scipy, statsmodels, xarray/netCDF4, openpyxl, pyarrow, matplotlib. Runtime about 20 minutes on 1 CPU. Random seed 20261112 (field-swap null). On the campaign host, `DATA_ROOT` defaults to the shared store.

## References

- Gandhi N., Tang R.W.K., Bhavsar S.P., Arhonditsis G.B. (2014) Fish mercury levels appear to be increasing lately: a report from 40 years of monitoring in the province of Ontario, Canada. *Environ. Sci. Technol.* 48: 5404-5414.
- Thomas S.M., Melles S.J., Bhavsar S.P. (2018) Exploring the role of growth dilution and climate warming in walleye and northern pike mercury trends. *Water* 10: 1625. doi:10.3390/w10111625.
- Link D.J., Verhoeven M.R., Hansen G.J.A. (2025) Data and R code in support of: Fish tissue mercury concentrations increase following the invasion of zebra mussels. DRUM, doi:10.13020/jpgy-kf56.
- Ontario Ministry of the Environment, Conservation and Parks. Fish Contaminant Data. Open Government Licence - Ontario. https://data.ontario.ca/dataset/fish-contaminants
- Rohde R.A., Hausfather Z. (2020) The Berkeley Earth Land/Ocean Temperature Record. *Earth Syst. Sci. Data* 12: 3469-3479.
