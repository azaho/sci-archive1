# Mean interannual summer-temperature tracking by ring widths at 759 conifer sites north of 55 N did not decrease after 1960, and 152 sites with records to 2010 or later showed no recovery after 1990

## Summary

The "divergence problem" says that tree-ring growth at high northern latitudes became less sensitive to summer temperature after about 1960. One explanation is global dimming: aerosol pollution decreased surface sunlight from about 1960 to 1985, and growth then followed light more than temperature. This explanation makes a forecast: where the sky became brighter again after about 1985 (most strongly in Europe), temperature tracking must recover.

We tested this with raw ring-width measurements from the International Tree-Ring Data Bank (ITRDB). We used 759 conifer sites at or north of 55 N (41,536 measured series). We calculated one site chronology without curve fitting: the mean year-to-year change in log ring width. We correlated it with the year-to-year change in June-August (JJA) mean temperature from Berkeley Earth. We compared three 30-year periods: 1931-1960 (P1), 1961-1990 (P2, dimming), and 1991-2020 (P3, brightening). We used 152 sites with records to 2010 or later for P3.

Main results:

1. **No mean loss of tracking after 1960.** In the 759 sites, the mean Fisher z of the correlation was 0.319 (95% CI 0.264 to 0.368) in P1 and 0.302 (0.254 to 0.347) in P2. The change was -0.017 (-0.070 to +0.040). The sensitivity slope did not change (5.9 and 6.0 percent growth per degree C). A ModNegExp-detrended chronology, CRU TS maximum temperature, a June-July season, a sample-depth limit of 10 or 15 series, latitude 60 N or more, and the genera Picea and Larix gave the same result.
2. **The apparent loss in "temperature-sensitive" sites is a selection effect.** When we selected sites with r >= 0.3 in P1, the mean z decreased by 0.127 in P2. When we selected sites with r >= 0.3 in P2 and went back in time to P1, the mean z decreased by 0.106. The two values are almost equal (Figure 3, left), so the decrease is regression to the mean and not a change in time.
3. **No recovery after 1990.** In the 152 sites to 2010 or later, mean z was 0.318, 0.262 and 0.226 in P1, P2 and P3. The change from P2 to P3 was -0.036 (-0.119 to +0.089). After we removed the expected regression to the mean, the change was -0.05 (-0.12 to +0.05).
4. **The regional pattern is opposite to the dimming forecast.** In Europe (92 sites, mostly Scots pine in Fennoscandia), where brightening was strongest, tracking decreased in each period (z 0.466, 0.350, 0.227). Net of regression to the mean, the P3 value was 0.09 lower than expected (-0.15 to +0.01). In North America (41 sites), tracking increased (z 0.08, 0.21, 0.39), 0.14 above the expected value (+0.04 to +0.23).
5. **A growth-level test was not reliable.** A common test calibrates the detrended index on temperature and examines the mean residual in a later period. This test gave -0.47 SD in 1961-1990, but it also gave +0.39 SD in a pre-1960 placebo (calibration 1901-1930, test 1931-1960). Thus we make no claim about trend (low-frequency) divergence.

Conclusion: in this network, there was no general post-1960 loss of interannual summer-temperature tracking for dimming to explain. Also, tracking did not recover where the sky became brighter. Europe had a continued decrease, centred on Pinus. Warmer sites lost slightly more tracking from P1 to P2 (-0.016 z per degree C of site JJA mean, 95% CI -0.029 to -0.002). This agrees with a small part for warmth or moisture stress, but the effect is small.

## Background and question

Briffa et al. (1998) reported reduced temperature sensitivity of recent tree growth at high northern latitudes. D'Arrigo et al. (2008) reviewed possible causes: drought stress from warming, changes in snow, end effects of detrending, and global dimming. Stine and Huybers (2014) related Arctic tree rings to variations in light. Wild (2009) described dimming from the 1950s to the 1980s and brightening after about 1985 in Europe and North America. Esper and Frank (2009) said that site selection and detrending choices can make divergence. Babst et al. (2019) found a 20th-century decrease in temperature control of growth at high latitudes in the ITRDB.

Our questions:

- Q1. In a fixed panel of high-latitude conifer sites, did interannual tracking of summer temperature decrease from 1931-1960 to 1961-1990?
- Q2. Is part of the reported decrease an observation bias, from site selection (regression to the mean) or from detrending end effects?
- Q3. Did tracking recover after 1990, as the dimming explanation forecasts, and did it recover most in Europe?

## Data

- **Ring widths:** ITRDB total ring-width files (Tucson .rwl format) from the NOAA NCEI World Data Service for Paleoclimatology. We found the sites with the NOAA paleo-search API (tree-ring studies at latitude 50 N or more). We downloaded the 1,321 .rwl files of sites with a last year of 1990 or later, on 2026-11-09. `files/provenance/itrdb_sites_used.csv` gives each site, its NOAA study ID, investigators, DOI and file URL. `files/provenance/rwl_file_sha256.csv` gives the SHA-256 of each file that we used.
- **Temperature (primary):** Berkeley Earth Complete_TAVG_LatLong1.nc (1 degree, monthly, 1750-2024). Shared campaign path `datasets/berkeley-earth-complete-tavg-latlong1-20261109/Complete_TAVG_LatLong1.nc`, SHA-256 `4b78118b5552cc4987a7c575b042a0ea92de55d7c01f47783edb81d082c40664`, from `https://berkeley-earth-temperature.s3.us-west-1.amazonaws.com/Global/Gridded/Complete_TAVG_LatLong1.nc`. Absolute temperature = anomaly + monthly climatology. We used the nearest valid land grid cell (search radius 3 cells).
- **Temperature (robustness):** CRU TS 4.09 monthly mean daily maximum temperature (tmx), 0.5 degree, 1901-2024. Shared path `datasets/cru-ts-4.09-tmx-1901-2024/cru_ts4.09.1901.2024.tmx.dat.nc.gz`, SHA-256 `78df1a40cc0b522664a6874a014bc42982e6b9632194ddc249a62ce27b049e78`.
- **Map land polygons:** Natural Earth 10m land v5 (`datasets/naturalearth-10m-land-v5/ne_10m_land.zip`), for Figure 1 only.

We do not include raw ITRDB measurements, chronologies, or climate grids in this bundle. See `files/NOTICE-external-data.md`.

## Methods

**Parsing.** We read the Tucson decadal format with fixed widths (columns 1-8 series ID, 9-12 year, ten 6-character values). The stop marker 999 means 0.01 mm units and -9999 means 0.001 mm units. We set values of 0 or less (missing or locally absent rings) to missing. We used series with 30 or more rings and years 1850 or later.

**Chronologies.** (1) DLOG: for each series, the first difference of log ring width; the site value is the mean across series. This chronology has no fitted growth curve and thus no end-of-record detrending effect. (2) STD: each series divided by a ModNegExp curve (a exp(-b t) + k with b > 0 and k >= 0; if this fit failed, a line with slope <= 0; otherwise the series mean), and the site value is the Tukey biweight mean. (3) STD-TRUNC: the same as STD, but we cut each series at 1960 before curve fitting.

**Correlations.** For each site and period, we calculated r(DLOG, first difference of JJA T) and r(STD, JJA T). A year was used only when 5 or more series were present. A period was valid with 25 or more usable years (P1, P2) or 20 or more (P3, 1991 to min(last year, 2020)). We used the Fisher z transform. The sensitivity slope is the OLS slope of DLOG on the change of JJA T (times 100 = percent growth per degree C).

**Samples.** Main sample: conifers (Picea, Pinus, Larix, Abies, Tsuga, Pseudotsuga, Chamaecyparis, Juniperus, Thuja) at 55 N or more. Panel A: valid P1 and P2 (759 sites, 65 spatial blocks). Panel B: Panel A sites with a valid P3 (152 sites, 22 blocks; last years 2010-2024, median 2014). Secondary band: 50-55 N.

**Uncertainty.** Sites in the same region share climate and investigators. Thus we used a cluster bootstrap over 5 degree latitude by 10 degree longitude blocks (2,000 resamples) for all 95% intervals.

**Selection placebo.** We selected sites with r >= threshold in P1 and calculated the mean change to P2. Then we did the reverse: we selected with r >= threshold in P2 and calculated the change to P1. If the forward and reverse decreases are equal, the decrease comes from selection on noise, not from time.

**Regression-to-the-mean expectation for P3.** We fitted z(P2) = a + b z(P1) over Panel A (persistence b = 0.465) and applied it to z(P2) of Panel B sites to get an expected z(P3) for a stable process. We give observed minus expected z(P3) with a block bootstrap that refits a and b.

**End-effect placebo.** We compared r(STD, T) in 1931-1960 for STD and STD-TRUNC. In STD-TRUNC, 1931-1960 is at the end of each curve fit.

**Level test and its placebo.** We calibrated STD on JJA T in 1931-1960 and calculated the mean residual (in calibration SD) in P2 and P3. For the placebo, we calibrated in 1901-1930 and tested in 1931-1960.

## Results

| Test (main sample, DLOG vs change of JJA T, Berkeley Earth) | n sites | Estimate (95% block-bootstrap CI) |
| --- | --- | --- |
| Mean z, P1 1931-1960 | 759 | 0.319 (0.264 to 0.368) |
| Mean z, P2 1961-1990 | 759 | 0.302 (0.254 to 0.347) |
| Change P2 - P1 | 759 | -0.017 (-0.070 to +0.040) |
| Change P2 - P1, STD index vs T | 759 | -0.022 (-0.059 to +0.018) |
| Change P2 - P1, CRU tmx | 759 | +0.020 (-0.035 to +0.083) |
| Change P2 - P1, depth >= 10 | 738 | -0.016 (-0.070 to +0.045) |
| Change P2 - P1, lat >= 60 | 552 | -0.005 (-0.074 to +0.081) |
| Change P2 - P1, Picea | 288 | +0.011 (-0.085 to +0.124) |
| Change P2 - P1, Larix | 141 | +0.046 (-0.052 to +0.157) |
| Change P2 - P1, Pinus | 232 | -0.116 (-0.165 to -0.032) |
| Change P2 - P1, 50-55 N band | 335 | +0.001 (-0.070 to +0.079) |
| Slope change P2 - P1 (percent per degree C) | 759 | +0.13 (-1.23 to +1.46) |
| Panel B mean z P1 / P2 / P3 | 152 | 0.318 / 0.262 / 0.226 |
| Panel B change P3 - P2 | 152 | -0.036 (-0.119 to +0.089) |
| Panel B P3 observed minus RTM-expected | 152 | -0.05 (-0.12 to +0.05) |
| Europe P3 observed minus RTM-expected | 92 | -0.09 (-0.15 to +0.01) |
| North America P3 observed minus RTM-expected | 41 | +0.14 (+0.04 to +0.23) |
| Warmth moderator of P2 - P1 (z per degree C) | 759 | -0.016 (-0.029 to -0.002), p = 0.024 |
| Warmth moderator of P3 - P2 (z per degree C) | 157 | +0.014 (-0.014 to +0.043) |

Selection placebo (DLOG):

| Threshold | Select in P1, change to P2 | Select in P2, change to P1 |
| --- | --- | --- |
| r >= 0.2 | -0.095 (-0.136 to -0.043), n = 522 | -0.069 (-0.133 to -0.014), n = 492 |
| r >= 0.3 | -0.127 (-0.166 to -0.077), n = 408 | -0.106 (-0.184 to -0.049), n = 383 |
| r >= 0.4 | -0.155 (-0.204 to -0.094), n = 289 | -0.165 (-0.246 to -0.099), n = 263 |

The STD chronology gave the same symmetry (for example r >= 0.3: -0.174 forward, -0.166 reverse).

End-effect placebo: STD-TRUNC minus STD in 1931-1960 was -0.003 z (-0.005 to 0.000). Thus ModNegExp end effects did not change interannual correlations.

Level test: the mean residual was +0.39 SD in the placebo (mean JJA warming +0.28 C), -0.47 SD in 1961-1990 (mean change 0.00 C) and -0.39 SD in 1991-2020 (mean warming +0.56 C, 152 sites). Offsets of the same size and opposite sign occur before 1960. Thus this test cannot separate a true trend divergence from detrending artefacts.

Selection in the updated sites: in Europe, the 92 sites with records to 2010 or later had a higher P1 z (0.466) than the 105 European sites without them (0.289). Investigators possibly updated the most temperature-sensitive sites. This is the reason we report P3 values net of regression to the mean.

Europe sensitivity slopes (Panel B) were 6.3, 3.9 and 3.2 percent per degree C in P1, P2 and P3. The SD of the year-to-year JJA temperature change was 1.28, 1.55 and 1.11 degree C. Thus the European decrease is in both correlation and slope.

Full numbers are in `files/results/results.json`, `files/results/results_rtm_levels.json` and `files/results/results_robustness.json`. Per-site statistics are in `files/results/site_metrics.csv`.

## Interpretation

- Q1: No. The network mean of interannual tracking did not decrease from 1931-1960 to 1961-1990. Some regions (Europe, eastern Canada) and the genus Pinus decreased; Alaska increased.
- Q2: Yes, selection is important. If a study selects sites because they track temperature well in one period, it will find a decrease in another period, forward or backward in time. Detrending end effects were negligible for interannual correlation.
- Q3: No recovery occurred after 1990. The region with the strongest brightening (Europe) continued to decrease, and North America increased. This order is opposite to the forecast of the dimming explanation for interannual tracking.

These results do not test the effect of light on low-frequency growth level, which was the main subject of Stine and Huybers (2014). Our level test failed its placebo. A test of that subject needs detrending that keeps low-frequency variance (for example regional curve standardization with pith offsets) and station or satellite radiation data.

## Limitations

- Interannual correlation only. We do not make claims about centennial trends or reconstruction offsets.
- P3 has only 152 sites, and 92 are in Europe (81 in Fennoscandia and the Baltic, in 6 blocks). The North American P3 sample has 41 sites in few blocks. Siberia has only 19 P3 sites.
- We did not measure dimming at each site. The regional dimming and brightening timing comes from the literature (Wild 2009).
- Gridded temperature at high latitudes before about 1950 uses few stations. The CRU tmx check gave the same P1 to P2 result, but both products can share station limits.
- First-difference correlations emphasize the highest frequencies and include effects of prior-year growth.
- ITRDB sites are not a random sample of forests. Collection targeted old trees and climate-sensitive sites. Updates to 2010 or later are also not random (see above).
- We used one season (JJA, with June-July as a check). Some sites respond to other months or to moisture.
- Some ITRDB files have wrong units or headers. Our metrics use log changes and ratios, so a constant scale error has no effect.

## Reproduction

The code is in `files/code/`. It needs Python 3.12 with numpy, pandas, scipy, statsmodels, netCDF4, pyarrow, matplotlib and geopandas.

```
bash files/code/run_all.sh /path/to/scratch \
  /path/to/Complete_TAVG_LatLong1.nc \
  /path/to/cru_ts4.09.1901.2024.tmx.dat.nc.gz \
  /path/to/ne_10m_land.zip
```

`00_fetch.sh` downloads the ITRDB metadata and .rwl files into the scratch directory, never into this bundle. The ITRDB archive and the paleo-search API can change. Compare downloaded files with `files/provenance/rwl_file_sha256.csv`. The step order is 01 site table, 02 parse, 03 climate extraction, 04 chronologies (about 15 minutes with 20 processes), 05 site metrics, 06 aggregate tests, 07 regression-to-the-mean and level tests, 08 subset checks, 09 figures. The bootstrap seeds are fixed.

## Provenance

- Job: sci-1107-dell-climate-pollution-biodiversity-5727852e8cd2; campaign 11_07_2026; topic climate-pollution-biodiversity; machine dell; account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data access: 2026-11-09. Computation on the dell host.

## References

- Briffa K.R. et al. (1998) Reduced sensitivity of recent tree-growth to temperature at high northern latitudes. Nature 391, 678-682. doi:10.1038/35596
- D'Arrigo R. et al. (2008) On the 'Divergence Problem' in northern forests. Global and Planetary Change 60, 289-305. doi:10.1016/j.gloplacha.2007.03.004
- Stine A.R., Huybers P. (2014) Arctic tree rings as recorders of variations in light availability. Nature Communications 5, 3836. doi:10.1038/ncomms4836
- Wild M. (2009) Global dimming and brightening: a review. JGR 114, D00D16. doi:10.1029/2008JD011470
- Esper J., Frank D. (2009) Divergence pitfalls in tree-ring research. Climatic Change 94, 261-266. doi:10.1007/s10584-009-9594-2
- Babst F. et al. (2019) Twentieth century redistribution in climatic drivers of global tree growth. Science Advances 5, eaat4313. doi:10.1126/sciadv.aat4313
- Zhao S. et al. (2019) The International Tree-Ring Data Bank (ITRDB) revisited. Journal of Biogeography 46, 355-368. doi:10.1111/jbi.13488
- Rohde R.A., Hausfather Z. (2020) The Berkeley Earth Land/Ocean Temperature Record. ESSD 12, 3469-3479. doi:10.5194/essd-12-3469-2020
- Harris I. et al. (2020) Version 4 of the CRU TS monthly high-resolution gridded multivariate climate dataset. Scientific Data 7, 109. doi:10.1038/s41597-020-0453-3
