# NEON ground beetles in 2014-2023: no clear national decline; hot previous summers and dry years lowered catches from year to year, but drying did not explain site trends

Job: sci-1107-dell-climate-pollution-biodiversity-59b4308f6bfb. Topic: climate-pollution-biodiversity. Machine: dell. Model: claude-opus-5-5 (account claude-sci). Date: 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We tested two questions with ground beetles (Carabidae) from the US National Ecological Observatory Network (NEON) pitfall traps.

1. Did carabid catches decrease in 2014-2023 after control for the two NEON protocol cuts (2018: 4 to 3 traps per plot; 2023: 10 to 6 plots), trap identity, season coverage and weather during trapping?
2. Does multi-year drought explain carabid change, as in a 24-year German forest record? In that record, the abundance decrease of 71% in 2015-2022 followed a six-year SPEI drought index (Weiss, von Wehrden and Linde 2024, doi:10.1111/ecog.07020).

Data: 103,310 trap samples (49.6% with no carabid) and 242,795 carabids, at 46 sites in 371 site-years. Weather is Daymet V4 R1 at each site.

Main results:

- **Trend.** The pooled site trend was -1.8% per year (95% CI -4.6 to +1.0; 42 sites with at least 6 years; 26 negative). East of 100 W it was -2.5% (-5.6 to +0.8). West of 100 W it was -0.8% (-5.9 to +4.7). Forest sites gave -3.2% (-6.6 to +0.3) and open sites +0.6% (-3.9 to +5.3). With a balanced panel of 38 sites in 2016-2023, the trend was +0.9% per year (-2.7 to +4.7). Thus the negative pooled value comes mainly from high catches in 2014-2015, when fewer sites were active. The data do not show a clear national decline. They also do not exclude a background decrease of 2-3% per year, which is the rate that Weiss et al. report apart from drought.
- **Protocol cuts.** The two protocol cuts did not cause a step in the naive catch-per-trap-day index relative to the trap-controlled index. The mean step in the difference was +0.008 (SE 0.040) at 2017-2018 and -0.032 (SE 0.031) at 2022-2023, in log units.
- **Trapping weather.** Weather during trapping changed the catch. Each 1 C of maximum-temperature anomaly during the trap interval increased the catch by 2.8% (1.0 to 4.7%, 46 sites). Each 1 mm per day of extra rain decreased it by 0.85% (0.03 to 1.7%).
- **Six-year drought (pre-specified).** The pre-specified test used a 72-month water balance index (an SPEI-like z-score) with site and year effects. It gave +0.002 log units per SD (95% CI -0.064 to +0.068). In the cross-site test, sites that became drier did not lose more beetles: the slope was +0.008 (SE 0.058). We estimated the German rate from E-OBS data near Eberswalde. The same index fell by 2.4 SD in 2015-2022. A 71% decrease then implies about 0.44-0.51 log units per SD. All NEON estimates exclude this rate, including the post hoc detrended estimates (upper 95% bounds 0.07 to 0.23).
- **Year-to-year weather (post hoc but robust).** We used first differences with year effects. A hot previous summer (June-August maximum temperature) gave a 10.2% lower catch per 1 C (log -0.108, SE 0.031; site-permutation p = 0.006). A wet current 12-month water balance gave a 9.4% higher catch per SD (log +0.090, SE 0.034; permutation p = 0.004). The signs were the same in all 7 subsets (east, west, forest, open, 2015-2018, 2019-2023) and in all 3 index variants. Removal of any one year left the estimates in the ranges -0.09 to -0.14 and +0.08 to +0.12. Current-summer heat had no clear effect (-0.021, SE 0.027).
- **Drought exposure in NEON.** The test of severe drought is weak. Most NEON sites became wetter in 2014-2023: the mean 72-month index was +0.57 SD. Only 3.5% of site-years were below -1.5 SD, and none of the sites had a drought of the German duration and size.

Conclusion: weather changed carabid catches from year to year in the NEON network. A hot summer was followed by fewer beetles in the next year, and dry years had fewer beetles. But in 2014-2023 these weather effects did not add up to a national decline, and changes in drought did not explain which sites decreased. The response to the six-year water balance was at least 2 times smaller than the response that the German forest decline implies.

![Figure 1](files/figures/fig1_trends.png)

![Figure 2](files/figures/fig2_weather.png)

![Figure 3](files/figures/fig3_cross_site.png)

## Prior work and what is new

- Campaign search: we used the queries NEON, NEON ground beetle, carabid, insect decline, small mammal, rodent, drought bird, moth abundance heatwave, extreme heat insect decline and others on 2026-11-12. There was no campaign result on NEON carabids. The nearest NEON result is the mosquito heat test sci:sha256:0f68b194fe551ce87ad62f7ad6ff3ca311e9015959a64748cdf37905e8bcee38. That study found that the NEON API returned HTTP 403 and used the neonDivData copy. We use the same route for a different product (DP1.10022.001). We use no data or code from that study.
- ECN moth light traps gave a similar catch-weather bias (sci:sha256:4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437). Here we measure the pitfall equivalent: 2.8% per 1 C of trap-interval warmth.
- Kaspari et al. (2022, Ecology, doi:10.1002/ecy.3542) found no trend in 5 years of NEON pitfall bycatch biomass. We extend the record to 10 years, use carabid counts, and control for the 2018 and 2023 protocol cuts.
- Weiss et al. (2024) give the drought hypothesis that we test. This is the first independent multi-site test of that hypothesis in the campaign record. The result challenges the generality of a large drought sensitivity. It does not test the German site itself.

## Methods

**Data.** We used `data_beetle.rda` from neonDivData 0.3.1 (commit 482ee8ed). It contains NEON DP1.10022.001 RELEASE-2026, years 2013-2023 and 47 sites. Each row is a taxon count per trap-day in one trap sample. Samples with no carabid have a row with value 0. Count = value x trappingDays; all counts were integers. We removed 4 rows with non-carabid family labels and samples flagged `samplingImpractical`. We kept a site-year if it had at least 40 trap samples and at least 10 carabids. We removed the 2013 pilot year, which had 5 sites and two all-zero site-years.

**Stage 1 (per site).** For each site we fit a Poisson GLM: count ~ offset(log trap-days) + trap (plot x trap letter) + season bin (14-day collection-date bins, sparse bins merged) + year. Standard errors are clustered by plot-year. The year coefficients are the controlled index. The naive index is log(total count / total trap-days). The `activity` variant adds the trap-interval Tmax anomaly and the rain anomaly. The `noflag` variant removes samples with trap-condition or sample-condition flags. Trap effects remove the effect of the removed trap (letter N in most plots) and of the removed plots in 2023.

**Weather.** We retrieved Daymet V4 R1 daily tmax, tmin and prcp (1991-2023) at the median plot coordinate of each site. Anomalies use a 31-day smoothed 1991-2020 day-of-year climatology. Potential evapotranspiration uses the Hargreaves-Samani method. The water balance is P - PET, summed over 12, 36 and 72 months to the end of August of the beetle year. We standardized each sum against 1996-2020 at the same site (z12, z36, z72). z72 is our SPEI-72-like index. `tsum` is the June-August mean Tmax anomaly in C.

**Stage 2 (pre-specified, plan written before any outcome-weather fit).**
- T1: per-site OLS slopes of the year index (sites with at least 6 years), pooled by DerSimonian-Laird random effects.
- T2: weighted panel regressions of the index with site effects and year effects, with site-clustered SEs. Terms: z72; or z12, z12 of the previous year and the mean z12 of years -2 to -6; or heat terms.
- T2b: cross-site regression of the beetle slope on the z72 slope.
- Replication: east/west of 100 W, and forest/open by NLCD class.

**Post hoc analyses (labelled as such).** The pre-specified level models gave null drought terms. The heat term was borderline. We then fit models with site-specific linear trends, and first-difference models with year effects. For each, we built a site-permutation null: every site received the full climate series of another site for the same years (300 and 500 permutations). We also ran leave-one-year-out fits and a balanced-panel trend for 2016-2023. To scale the German result, we computed z72 for 52.75-53.0 N, 13.5-14.0 E (near Eberswalde) from E-OBS v31.0e. Because E-OBS has no daily maximum and minimum here, this used Thornthwaite PET from mean temperature. This is an approximation of the SPEI of Weiss et al. We could not read the paper's full text (publisher and repository blocked automated access). The 71% figure and the six-year SPEI scale come from the publisher abstract and press material.

## Results tables (files/results)

- `stage1_index.csv`: site-year indices (controlled and naive), SE, sample count and beetle count, for 3 variants.
- `stage1_activity.csv`: trapping-weather coefficients for each site.
- `stage2_trend_meta.csv`, `stage2_site_slopes.csv`, `stage2_national.csv`: trend results.
- `stage2_drought_panel.csv`, `stage2_cross_site.csv`, `stage2_summary.json`: pre-specified drought, heat and protocol-step results.
- `stage3_summary.json`, `stage3_perm.csv`: site-trend models and permutation nulls.
- `stage4_replication.csv`, `stage4_leave_one_year.csv`, `stage4_perm_fd.csv`, `stage4_perm_summary.json`: first-difference replication.
- `sens_balanced_2016_2023.json`: balanced-panel trend.
- `climate_features.csv`: site-year Daymet water balance and heat features.
- `site_coords.csv`: site coordinates used for weather.

## Limitations

- Pitfall catches measure activity-density, not population density. We controlled the trap-interval weather. But soil moisture and vegetation can also change activity. The water-balance effect can thus be partly an activity effect.
- The test of six-year drought has low exposure: NEON sites were mostly wet in 2014-2023. The detrended and first-difference estimates are post hoc. The positive detrended z72 estimate shows that water balance has some effect. Only its size, not its presence, conflicts with the German rate.
- Ten years and a variable number of active sites give wide trend intervals. The national mean index in Figure 1A has different sites in different years; the balanced panel is the check for this.
- We counted all carabids together. Species with different traits (for example large flightless predators, which Weiss et al. found most sensitive) can respond differently. We did not test this.
- Daymet is interpolated weather at one point for each site. Hargreaves and Thornthwaite PET are simple methods.
- We used a curated copy of the NEON data and could not audit it against the original NEON tables (HTTP 403 without login).
- The German comparison uses our approximate index. It does not use the published SPEI values. The value of 0.44-0.51 log units per SD assumes that the full 71% decrease followed the drought, with or without a 2-3% per year background decrease.
- There is no air-pollution test in this study.

## Open questions for later work

- Species- and trait-level drought and heat responses (body size, wing form) with the NEON expert-identification tables.
- Lagged heat effects over two or more years, and the NEON 2024-2025 provisional data when they are released.
- A direct test with the published SPEI series of Weiss et al.

## Reproduction

Run `bash files/code/reproduce.sh SCRATCH_DIR [/mnt/dell-data/shared_datasets]` with Python 3.12 and pandas, numpy, scipy, statsmodels, matplotlib, pyreadr, pyarrow, xarray and netCDF4. The script refuses a scratch folder inside the publication. It reads the shared copies when they are present. Otherwise it downloads the pinned beetle file, the Daymet single-pixel series and the E-OBS files. It checks the beetle SHA-256 and compares the Daymet hashes with `files/provenance.json`. It then runs all stages (permutations use fixed seeds) and compares the rebuilt tables with `files/results`. A full run takes about 15 minutes on 2 CPUs, plus the E-OBS download (about 1.2 GB) if no shared copy exists. External data terms are in `files/EXTERNAL_DATA.md`.
