# A sea-ice curve for Adélie penguin colony trends is confounded with region in 1984-2017; after 2017 it held on the Antarctic Peninsula, but Ross Sea colonies did not grow as it predicted

Job: sci-1107-dell-climate-pollution-biodiversity-3b00bd2e08c9. Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. Date: 2026-11-09. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Iles et al. (2020, Global Change Biology 26:3788, doi:10.1111/gcb.15085) used counts from the MAPPPD penguin census database at 38 Adélie penguin colonies (1984-2017). They found that the mean March-June sea-ice concentration (SIC) within 500 km of a colony predicts the long-term colony growth rate. The relation is a concave quadratic ("habitat optimum"). Growth is negative below approximately 31% SIC, and the optimum is near 50% SIC. The curve explained more than 80% of the among-colony variance in growth.

We did three tests on this claim:

1. Can the curve be separated from the region of the colony? The 38 colonies are in three regions: the Antarctic Peninsula and Scotia Arc, East Antarctica and the Ross Sea.
2. Does the curve predict colony change after 2017? This period was not used to fit the curve, and Antarctic sea ice decreased after 2016.
3. Does the change in sea ice between periods predict the change in growth (space-for-time transfer)?

We wrote the analysis plan (`files/PLAN.md`) before we calculated growth rates. Section 6 gives the changes that we made after the first results.

## 2. Data

- **Penguin counts:** MAPPPD version 5.0 (Oceanites, release 2026-10-21), complete download from `https://www.penguinmap.com/mapppd/DownloadAll/` on 2026-11-09. SHA-256 `d169c409cf278b137d6df35fbeb9ab3409bdea15f41c39bcaec549a4d4dbca89`, 5,487 records, of which 1,920 are Adélie records. We use counts of nests, chicks and adults with the MAPPPD accuracy class (1-5). We do not include this file or record-level tables made from it (see `files/NOTICE-external-data.md`).
- **Sea ice:** NSIDC Sea Ice Index version 4.0 (G02135, doi:10.7265/a98x-0f50), southern monthly concentration GeoTIFFs (25 km grid, EPSG:3412), March to June, 1979-2026 (192 files). We calculate the March-June mean for each grid cell. Then we average all ocean cells within 500 km (and 100 km as a check) of each MAPPPD site. The table `files/data/site_sic.csv` gives the result for each site and year.
- **Published curve:** we use the Table 1 medians (b0 = 0.023, b1 = 0.024, b2 = -0.029, on standardized SIC). The paper does not give the mean and SD that it used to standardize SIC. Thus we recovered the 38 points of its Fig. 3 from the vector glyph positions in the author PDF (`code/00_digitize_iles_fig3.py`). The published curve fits these points with R2 = 0.99, which shows that the recovery is correct. The authors' SIC values have a mean of 45.0% and an SD of 25.3%. With these values, the published curve is zero at 30.6% and 80.3% SIC, and it has its maximum at 55.4% SIC. Their Peninsula SIC values (4-20%) are lower than ours (19-26%). Their East Antarctic (36-39%, one site 52%) and Ross Sea (71-75%) values are near ours. To apply the published curve to our SIC values, we use a monotone quantile map between the two sets of 38 values.

`files/data/input_checksums.txt` gives the SHA-256 of all input files.

## 3. Methods

- **Growth rate of a colony:** weighted least-squares slope of log(count) on season (season = breeding season that starts in November of year t). Chick counts get a pooled offset to nest counts (median log ratio in seasons with both counts; 0.056). Adult counts have no seasons with both types, so their offset is 0. The weight is 1/(s_acc^2 + 0.2^2), where s_acc = 0.05, 0.10, 0.25, 0.50, 1.0 for accuracy classes 1-5 and 0.2 is a process-noise term. The slope SE uses the residual scale when it is more than 1. We sum Cape Crozier east and west in seasons where the two parts were both counted (Iles et al. used one series).
- **H1 (replication, 1984-2017):** 38 sites with 10 or more survey seasons. Random-effects WLS of growth on z(SIC) and z(SIC)^2. We give the variance share as 1 - tau2(model)/tau2(intercept only), with tau2 from the Paule-Mandel method. We compare this with region-only and region-plus-curve models, and with leave-one-region-out prediction.
- **H1b (within region):** 73 sites with 3 or more seasons over 10 or more years. Slope of growth on SIC within each region.
- **H2 (spatial hold-out):** 35 sites with 3-9 seasons over 10 or more years that are not in the H1 fit.
- **H3 (forward test, 2018-2025):** 45 sites with an in-sample count and at least one count in seasons 2018-2025 (123 counts). Anchor = WLS fit at 2017 from 2008-2017 counts (37 sites), else the last in-sample count (8 sites). Forecast = anchor + g x (years after anchor), with g from: no change; the own 1984-2017 slope; the region mean slope; the refitted curve at 1984-2017 SIC or at 2017-2025 SIC; the published curve at 1984-2017 SIC or 2017-2025 SIC. Metric: mean squared log error per site, then mean over the 34 sites that have all forecasts. The 95% intervals come from a site bootstrap (2,000 samples). We also compare the observed 2017-2025 slope (3 or more seasons over 4 or more years; 20 sites) with the predicted slopes.
- **Regional index:** WLS model of log count with site and season fixed effects. We use sites with 5 or more seasons and seasons with 3 or more sites. The trend SE comes from the scatter of the yearly effects. This SE includes shocks that are common to all colonies in a region in a year.
- **H4 (space-for-time):** for 19 sites, the change in growth (2017-2025 minus 1984-2017) compared with the curve-predicted change from the change in SIC.
- **Checks for observation bias:** we repeated all tests with nest counts only, accuracy class 1-2 only, ground and aerial counts only (no UAV or satellite counts), and a 100 km SIC radius (`files/results/summary_by_variant.csv`).

## 4. Results

### 4.1 In 1984-2017, the sea-ice curve does not separate from region (Fig. 1)

- The three regions have SIC ranges that do not overlap: Peninsula 19-26%, East Antarctica 39-53%, Ross Sea 71-74% (core sites, our SIC values).
- Refitted curve: b = 0.050 (SE 0.013), 0.008 (0.007), -0.052 (0.012). It is zero at 31.5% and 74.7% SIC, and it has its maximum at 53.1% SIC. The value of 31.5% agrees with the published value of 31%. The curve explains 49% of the among-site variance (our data and method), not more than 80%.
- A model with only region effects explains 53%. Region plus curve explains 50%. Thus, SIC adds no information after region. The results of all four observation-bias checks are the same (curve 0.49-0.62, region only 0.53-0.67).
- Leave-one-region-out predictions fail. For example, without the Peninsula sites, the fit predicts +0.30 per year for the Peninsula, but the observed mean is -0.074 per year. In each region, the prediction error is larger than the error of a zero-growth prediction.
- The published curve explains only 9% (0.09-0.42 in the checks) of the variance of our site slopes. Its Fig. 3 values are posterior medians that the model pulls toward the curve. Our East Antarctic slopes (mean +0.040 per year, up to +0.11) and some Peninsula slopes (to -0.18 per year) are much farther from the curve.

### 4.2 Within regions, there is evidence only for the low-ice part of the curve

- **Peninsula:** 27 sites, 19-45% SIC. Growth increases by 0.037 per year per 10 SIC points (SE 0.009; Spearman 0.54, p = 0.004). The value stays between 0.032 and 0.038 in the checks, except 0.016 (SE 0.004) with the 100 km radius. This agrees with the rising part of the curve.
- **Ross Sea:** 31 sites, 51-74% SIC. Slope -0.002 (SE 0.006). The data do not show the predicted decrease at high ice.
- **East Antarctica:** 15 sites, 39-53% SIC. Slope -0.037 (SE 0.044). This result is uncertain.
- **Spatial hold-out:** in 35 sites that were not in the fit, the curve predictions have a rank correlation of 0.68 with the observed growth. The mean squared error of the curve is lower than that of the region mean (bootstrap interval of the difference below zero), because the Peninsula hold-out sites cover a wider SIC range.

### 4.3 After 2017: the Peninsula agreed with the curve, the Ross Sea did not (Fig. 2, Fig. 3)

- **Mean SIC change:** at the index sites, SIC decreased from 72.3% (1984-2017) to 69.0% (2017-2025) in the Ross Sea, and from 25.0% to 21.5% on the Peninsula.
- **Peninsula regional index (21 sites):** the 2017-2025 trend is -4.1 ± 2.3% per year (SE). The published curve predicts -4.1% per year (1984-2017 ice) or -5.7% per year (2017-2025 ice). These values agree.
- **Ross Sea regional index (26 sites):** the trend was +1.3 ± 0.4% per year in 1985-2017 and -1.4 ± 1.6% per year in 2017-2024. The published curve predicts +1.5% per year (1984-2017 ice) or +1.5% per year (2017-2025 ice). The refitted curve predicts +1.1% per year (1984-2017 ice) or +2.4% per year (2017-2025 ice), because less ice moves the Ross Sea colonies toward the optimum. The observed trend is 2.9 percentage points per year below the published prediction (z ≈ 1.8). Thus, the shortfall is probable, but it is not certain at the 95% level. The index decreased to -0.21 in 2023 and increased to +0.05 in 2024 (only 5 sites were counted in 2024).
- **Site slopes, 2017-2025:** All 15 Ross Sea sites had a negative slope (mean -0.035 per year). The published prediction is +0.015 per year (Fig. 3a). Many Victoria Land sites were counted only in 2017, 2018 and 2023. Thus, the low year 2023 has a large effect on these slopes, and the regional index gives the better estimate. The 5 Peninsula sites had a mean of -0.058 per year (predicted -0.045 per year).
- **Count forecasts:** no forecast was clearly better than the no-change forecast. The mean squared log errors are: no change 0.824, own trend 0.794, refitted curve 0.806, published curve 0.874, region mean 0.899. All bootstrap intervals of the difference from no change include zero (Fig. 3b). The results of the four checks are the same. The error variance between counts at a colony is much larger than the trend signal over 1-8 years.
- **Space-for-time (H4, 19 sites):** the curve-predicted change in growth from the change in SIC does not predict the observed change. Spearman rho = -0.01 for the refitted curve and -0.18 for the published curve. In the checks, rho is between -0.18 and +0.12. Both regions had a lower growth rate after 2017 (Peninsula -0.034, Ross Sea -0.040 per year). The curve predicted a lower rate only for the Peninsula.

## 5. Interpretation

In MAPPPD, the strong among-colony relation between mean sea ice and Adélie trend is mostly a contrast between three regions. These regions are different in many properties that are not sea ice (for example krill, fast ice, polynyas, human disturbance history and survey programmes). The data support one part of the curve: within the Peninsula, colonies at higher ice levels decreased less. This part also held after 2017. The data do not support the high-ice part of the curve. Ross Sea colonies did not grow faster when ice decreased after 2016. Instead, their growth stopped. The 1984-2017 sea-ice curve is therefore not a reliable tool to forecast Adélie colony change in the heavy-ice part of the range. Iles et al. said that annual forecasts have little skill. Our count forecasts also show this for 1-8 year horizons.

## 6. Limitations and changes from the plan

- **Not a full replication:** we used weighted least-squares slopes, not the Bayesian state-space model. MAPPPD v5.0 does not have all of the original 38 series. For example, the Pointe Géologie supplement was not public, and some site codes changed. Our 38 core sites are mostly the same as the original sites, but not all.
- **Sea-ice product:** we used the Sea Ice Index (NASA Team), not NSIDC-0051 directly. Our Peninsula SIC values are higher than those of the authors. The quantile map that we used to apply the published curve is an approximation.
- **Few independent units:** after 2017, there are data only from the Peninsula and the Ross Sea. East Antarctica has no post-2017 counts in MAPPPD. Colonies in a region share year effects, so the 15 Ross Sea sites are not 15 independent tests. The regional-index SE uses only 7-8 seasons.
- **Counts after 2017:** some recent Peninsula counts are from UAV surveys. Nest-only, accuracy class 1-2 and ground/aerial-only checks gave the same conclusions. Many sites have 1-3 post-2017 counts.
- **Changes after the first results:** (a) we replaced the two planned guesses of the published standardization with the values that we recovered from Fig. 3; (b) we added the regional index, the within-region slopes (H1b) and the region-only and leave-one-region-out models; (c) the planned rule "the curve transfers if it is better than no change and the region mean" was tested; the curve failed this rule in all variants.

## 7. Files and reproduction

- `files/code/get_data.sh SCRATCH` downloads all inputs into a local scratch folder. It does not write into this publication. The MAPPPD endpoint is live. Use `files/data/input_checksums.txt` to compare the bytes.
- `files/code/run_all.sh SCRATCH` runs the steps 01 (site SIC), 00 (Fig. 3 points; needs `pypdf`), 02 (tests H1-H4 for five variants), 03 (regional index), 04 (figures) and 05 (summary). We ran the pipeline again in a clean folder, and the JSON results were identical. Python 3.12 with numpy, pandas, scipy, rasterio, pyproj, matplotlib and pypdf.
- `files/results/results_<variant>.json`: all aggregate test results. `regional_index.json` and `regional_index_and_sic.csv`: regional index and regional SIC. `summary_by_variant.csv`: main numbers for each check.
- `files/data/site_sic.csv`: March-June SIC within 500 km and 100 km for each MAPPPD site, 1979-2026.
- `files/figures/`: Figures 1-3.
- The script writes site-level growth tables and the recovered Fig. 3 points into the scratch folder only.

## 8. References

- Iles D.T., Lynch H., Ji R., Barbraud C., Delord K., Jenouvrier S. (2020) Sea ice predicts long-term trends in Adélie penguin population growth, but not annual fluctuations. Global Change Biology 26:3788-3798. doi:10.1111/gcb.15085
- Che-Castaldo C. et al. (2017) Pan-Antarctic analysis aggregating spatial estimates of Adélie penguin abundance reveals robust dynamics despite stochastic noise. Nature Communications 8:832. doi:10.1038/s41467-017-00890-0
- Oceanites, Inc. (2026) MAPPPD: census counts of Antarctic and sub-Antarctic breeding penguins. MAPPPD version 5.0. https://www.penguinmap.com
- Fetterer F. et al. Sea Ice Index, Version 4 (G02135). NSIDC. doi:10.7265/a98x-0f50
