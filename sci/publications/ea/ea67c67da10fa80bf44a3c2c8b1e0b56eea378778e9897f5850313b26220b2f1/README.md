# Year-to-year temperature responses explain only 2-29% of Chicago bird size declines and not the Amazon or Tanzania trends; the MAPS share is uncertain

## Summary

Many studies report that bird body size changes through time, and that warming causes the change (the temperature-size rule, a temporal form of Bergmann's rule). Two recent results disagree. Youngflesh et al. (2022) found that temperature predicts smaller adult males in the MAPS banding data. Probst et al. (2026) found that relative mass decreased through time in 24 species, but that temperature did not predict it.

We did a direct test of the warming explanation in four public, independent data sets from three continents:

- MAPS banding stations, North America, 1989-2018: 105 species, 244,250 adult males, 962 stations (Youngflesh et al. 2022).
- Window-collision specimens, Chicago, 1978-2016: 52 migrant species, about 70,000 birds (Weeks et al. 2020).
- BDFFP mist nets, central Amazon, 1979-2019: 43 resident species (Jirinec et al. 2021).
- Mist nets in the Usambara Mountains, Tanzania, 1987-2022: 21 species (Neate-Clegg et al. 2023).

The test is simple. If warming causes the trend, the trait must also respond to year-to-year temperature changes. We removed the local linear temperature trend and measured the trait slope on the remaining temperature anomaly. We then multiplied this slope by the local warming rate. The result is the trend that warming can explain if the long-term response is equal to the year-to-year response. We compared this implied trend with the observed trend. We used two temperature products, CRU TS 4.09 Tmax and Berkeley Earth TAVG.

Main results (Figure 1; pooled across species, random effects, 95% intervals):

| Data set | Trait | Observed trend, %/decade | Implied by warming, %/decade (CRU / Berkeley) | Share implied (CRU / Berkeley) |
| --- | --- | --- | --- | --- |
| MAPS | mass | -0.21 [-0.36, -0.06] | -0.07 / -0.09 | 32% [17, 106] / 43% [23, 154] |
| MAPS | wing | +0.03 [-0.02, +0.08] | -0.01 / -0.00 | no trend to explain |
| Chicago | mass | -0.78 [-0.97, -0.58] | -0.16 / -0.23 | 21% [13, 32] / 29% [19, 48] |
| Chicago | tarsus | -0.66 [-0.72, -0.60] | -0.01 / -0.02 | 2% [0, 4] / 3% [1, 6] |
| Chicago | wing | +0.30 [+0.23, +0.37] | -0.01 / -0.01 | opposite sign |
| Amazon | mass | -0.69 [-0.94, -0.43] | +0.34 / -0.11 | sign depends on product; at most 16% [-6, 53] |
| Amazon | wing | +0.30 [+0.15, +0.44] | +0.07 / +0.08 | 24% / 26%, intervals include 0 |
| Usambara | mass | +1.29 [+0.96, +1.61] | +0.00 / +0.07 | 0% / 6% [-3, 18]; increase, not decrease |

(Share intervals are 2.5-97.5 percentiles of 1000 bootstrap samples of species.)

Conclusions:

1. In Chicago, the warming explanation fails for skeletal size. The tarsus decrease (47 of 49 species) is 30 to 50 times larger than the year-to-year temperature response predicts. Mass has a clear negative temperature slope, but warming explains at most about half of the mass decrease (upper interval 48%). The wing increase has the wrong sign for a temperature response.
2. In MAPS, mass decreases with temperature in time and in space. The implied share of the mass trend is 32-43%, but the interval is wide (17% to more than 100%). Thus the MAPS data do not reject a full warming explanation and do not confirm it.
3. In the Amazon, the observed mass decrease does not follow a consistent temperature response: the anomaly slope is +0.99 %/C with CRU and -0.33 %/C with Berkeley Earth (CRU has only 1-3 stations near the site).
4. In Tanzania, mass increased while the region warmed by about 0.2 C per decade (Berkeley Earth). Warm years had heavier birds, not lighter birds. The increase is present within the records of one bander (1987-2008: +1.03 %/decade [+0.52, +1.54]), so it is not caused by the change of bander in 2008 (Figure 4).
5. In all four data sets the residual trend after the temperature anomaly term is almost the same as the original trend.

Thus a temperature-size response to year-to-year warming does not explain most of the temporal size trends in these data. The trends need another cause, or a long-term response to warming that is much larger than the year-to-year response and that our data cannot measure. One test of the second possibility was not informative: MAPS stations that warmed faster did not have clearly steeper mass decreases, but the interval was very wide (-0.86 %/C [-2.75, +1.03] with CRU; +0.35 %/C [-1.85, +2.55] with Berkeley Earth).

## Prior work and what is new

- External: Weeks et al. 2020 (doi:10.1111/ele.13434) reported the Chicago trends and linked them to summer temperature. Youngflesh et al. 2022 (doi:10.1038/s41559-022-01893-x) reported spatial and temporal temperature effects in MAPS. Jirinec et al. 2021 (doi:10.1126/sciadv.abk1743) reported Amazon mass decreases and wing increases and linked them to climate. Neate-Clegg et al. 2023 (doi:10.1111/ecog.07106) reported Afromontane size increases. Probst et al. 2026 (doi:10.1111/geb.70272) found a relative-mass decrease through time that temperature did not predict.
- Campaign record: searches of the 11_07_2026 campaign ("body size", "Bergmann", "wing length", "bird mass decline", "museum specimens", "MAPS banding") found no prior publication on temporal body-size change. Related campaign results show that community thermal composition follows only a part of its spatial temperature gradient (sci:sha256:0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada) and that bird and butterfly occupancy changes follow temperature only weakly (sci:sha256:40f3f9517b722988160163ef5d821c4d3931726b94b10444932be6d2454b3529). Our result is the morphological equivalent: trait trends are not proportional to the local temperature response.
- New in this work: (a) one common decomposition (trend versus detrended anomaly) applied to four independent data sets; (b) a quantitative "share implied by warming" with bootstrap intervals; (c) two temperature products, which show that the Amazon temperature slope and the Tanzania warming rate depend on the product; (d) observation-bias tests: bander change (Tanzania), capture hour (Amazon), capture date, season, age and sex (Chicago), station turnover (MAPS station fixed effects), and long-running stations only (MAPS).

## Methods

Temperature. For each MAPS station we used the May-August mean of monthly CRU TS 4.09 Tmax at the station's 0.5 degree cell (one station on an ocean cell was dropped). For Chicago we used the June-August Tmax mean over the main breeding region of the migrants (land, 40-60 N, 100-60 W, cos-latitude weights), of the most recent breeding summer (autumn birds: same year; spring birds: previous year). As a check we used the Chicago cell. For the Amazon site (2.41 S, 59.87 W) we used the June-November (dry season) mean of the most recent dry season. For Usambara we used the calendar-year mean at the East and West Usambara cells. We repeated all steps with Berkeley Earth 1 degree TAVG (anomaly plus climatology).

Decomposition. For each station or region we fitted a linear trend to the temperature series over the data years. A = temperature minus this trend line (the detrended anomaly). Warming rate = slope of the line (C per decade).

Species models (log trait; standard errors clustered by station for MAPS and by year for the other data sets):

- M0: log(trait) ~ fixed effects + decade. Observed trend.
- M2: log(trait) ~ fixed effects + decade + A. Anomaly slope and residual trend.
- MAPS only: M1 raw temperature; M3 adds W = station warming slope x decade (dose response); M4 temperature with station and year fixed effects; spatial slope of station means.
- Fixed effects and controls: MAPS station; Chicago season x age, sex, and season-specific day of year (linear and quadratic); Amazon age group, month, and capture hour; Usambara site, and in a check also bander.

Pooling. DerSimonian-Laird random-effects means across species. Implied trend for a species = anomaly slope x warming rate. Share = pooled implied trend / pooled observed trend; the interval comes from 1000 bootstrap samples of species.

Checks. MAPS: prior-year temperature; stations with 10 or more years; a pooled dose-response model across all species (species x station fixed effects, species-specific trends). Chicago: 3- and 5-summer mean anomalies (to allow a delayed or cumulative response) and trends in 1978-2005 and 2006-2016 separately. Amazon: without the capture-hour control. Usambara: bander fixed effects, and each bander separately.

## Further results

- MAPS mass temperature slopes (%/C, CRU): detrended anomaly -0.18 [-0.24, -0.13]; with year fixed effects -0.12 [-0.21, -0.02]; spatial -0.33 [-0.42, -0.24]. With Berkeley Earth: -0.24, -0.17 and -0.24. If we use the spatial slope as the long-term response, warming implies -0.12 %/decade (59% of the trend) with CRU and -0.09 (43%) with Berkeley Earth (Figure 3).
- MAPS prior-year temperature gives a smaller implied share (15% CRU, 22% Berkeley Earth). Stations with 10 or more years give 38% and 50%.
- Chicago 3- and 5-summer mean anomalies do not give larger slopes (mass -0.08 and +0.16 %/C; tarsus -0.08 and -0.12 %/C), so a short delayed response does not close the gap.
- Chicago trends are steeper inside each sub-period (mass -1.18 %/decade in 1978-2005 and -1.35 in 2006-2016) than over the full period (-0.78). Thus mass levels moved up near 2005-2006, when the number of collected birds per year increased about three times. A change in collection or preparation is a possible cause; we did not resolve it. The tarsus decrease is present in both sub-periods (-1.02 and -0.39). The wing increase is present only before 2006.
- Usambara wing trends depend on bander: +0.17 %/decade without and +0.75 with bander fixed effects. The two banders probably measured wings differently, so the Usambara wing result is not reliable.
- With the Chicago cell (instead of the breeding region), local summer Tmax warmed only 0.06 (CRU) or 0.13 (Berkeley Earth) C per decade, and the implied share of the mass trend is 3-10%.

## Limitations

- The year-to-year response can differ from the long-term response. Developmental plasticity, microevolution or slow changes in food can give a long-term response that is larger than the anomaly response. Our test can only say that the year-to-year response is too small; it cannot exclude these slow mechanisms. The MAPS dose-response test, which could identify a long-term response, had no power.
- Regional temperature is a coarse exposure. The Chicago migrants breed over a large area; one box is an approximation. CRU has few stations near the Amazon and Usambara sites, and its Usambara warming rate (about 0 C per decade) differs from Berkeley Earth (0.2 C per decade).
- The MAPS extract has no capture date, time of day, fat score or bander, so these observation effects are not controlled in MAPS. The Usambara data have no capture date.
- Mass changes with season, time of day and condition; we controlled these only where the data permit.
- We did not use phylogenetic models. Species are pooled with random effects only.
- The share implied by warming is a ratio. When the observed trend is small (MAPS, Amazon wing, Usambara wing), the ratio interval is very wide.

## What remains open

- A test with banding data that include date, time and bander (for example, full MAPS or BBL morphometrics) and many decades of station data.
- The cause of the Chicago mass step near 2005-2006 and of the tarsus decrease.
- The cause of the Usambara mass increase in warm years and through time (food, habitat, or body condition).
- A long-term dose-response test with larger contrasts in warming rate (for example, across continents).

## Reproduce

1. `bash files/code/fetch_data.sh SCRATCH` downloads the four CC0 Dryad version ZIPs into SCRATCH (not into this bundle) and decompresses CRU TS 4.09 Tmax (set `DATASETS=` to the campaign dataset store to reuse its copy). Download Berkeley Earth `Complete_TAVG_LatLong1.nc` (URL in files/PROVENANCE.md).
2. `bash files/code/run_all.sh SCRATCH /path/Complete_TAVG_LatLong1.nc OUTDIR` runs all steps (about 10 minutes on 2 CPUs; a full rerun on 2026-11-12 reproduced all result CSV files byte for byte; Python 3.12 with numpy, pandas, xarray, netCDF4, matplotlib).
3. Compare OUTDIR with `files/results/`.

Files:

- `files/results/summary_trend_vs_implied.csv`: pooled trends, anomaly slopes, implied trends, residual trends and shares for all data sets, traits, variants and temperature products.
- `files/results/all_species_coefficients.csv`: species-level coefficients and standard errors.
- `files/results/maps_temperature_slopes.csv`, `maps_pooled_dose_response.csv`, `chicago_robustness_cru.csv`: checks.
- `files/results/fig1-4*.png`: figures.
- `files/code/`: all code. `files/PROVENANCE.md`: sources, versions, hashes. `files/NOTICE-external-data.md`: licences of external data.

## Provenance of this work

Job sci-1107-dell-climate-pollution-biodiversity-7c464739ec3e, topic climate-pollution-biodiversity, campaign 11_07_2026, machine dell, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim. Analysis date 2026-11-12.
