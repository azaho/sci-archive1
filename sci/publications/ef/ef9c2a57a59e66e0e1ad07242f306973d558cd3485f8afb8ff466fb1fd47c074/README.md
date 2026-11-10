# DOISST v2.1 noise steps make 1985-2023 coral heat-stress (DHW) trends 11-16% too low at 1,763 reef pixels; mean-warming differences between products are a larger uncertainty

## Summary

Earlier campaign studies found that NOAA DOISST v2.1 (daily OISST) lost most of its fast (day-to-day) variance in steps at satellite input changes (sci:sha256:f50dc28f..., sci:sha256:87b87a67..., sci:sha256:69a00227...). Other studies showed that these steps bias SST memory, marine heatwave statistics, daily extremes and front statistics (sci:sha256:819eea65..., sci:sha256:cfeb640f..., sci:sha256:4e3a13fa..., sci:sha256:5d8902f2...). No study in the campaign tested coral heat stress.

Degree Heating Weeks (DHW) is the standard coral bleaching heat-stress index (NOAA Coral Reef Watch). DHW adds only the daily SST excess that is 1 C or more above the warmest-month mean (MMM), over 12 weeks. Because of this threshold, DHW is a convex function of daily SST: more fast noise gives more DHW, and less noise gives less DHW. Thus the DOISST noise steps can change DHW trends, and they can change the reported fraction of reefs at bleaching alert levels (DHW 4 and 8 C-weeks).

**Question.** Do the DOISST input steps bias reef DHW statistics in 1985-2025? What is the size and sign of the bias? How does it compare with other differences between SST products?

**Approach.**

1. We selected 1,763 DOISST 0.25-degree reef pixels at the 12,702 survey sites of the global coral-bleaching database (BCO-DMO 773466; van Woesik and Kratochwill 2022).
2. We calculated the Coral Reef Watch statistics (CoralTemp v3.1 method: MMM from 1985-2012 monthly means centred at 1988.2857; HotSpots of 1 C or more; 84-day DHW) for raw DOISST and for three homogenised versions. A homogenised version has the fast spectrum (periods shorter than about 32 days) of one target input segment in all six segments: 2007-2015 (main version), 1985-2006 or 2016-2020. The method removes excess fast power by spectral attenuation and adds missing fast power as random noise. It does not change periods longer than about a month, so it keeps the mean, the seasonal cycle, the warming trend and the long events.
3. We tested the method on 500 synthetic pixels with a known homogeneous truth.
4. We compared DOISST with in situ SST at 149 moorings (97 GTMBA tropical moorings, 52 NDBC buoys; 2,816 buoy-years) on matched days.
5. We compared DOISST with the satellite-only ESA SST CCI Analysis v3.0.1 on every day of 1982-2024 at the 683 reef pixels inside three boxes: Caribbean, Great Barrier Reef (GBR) and Coral Triangle.

## Main results

**R1. The DOISST fast-variance steps are present at reefs.** At the reef pixels, the median power at periods of 4-8 days relative to 2007-2015 was 1.86 in 1985-2006, 0.87 in 2016-2020, 0.59 in mid-2020 to 2021 and 0.29 after November 2021 (Figure 1d). These ratios agree with the global values in sci:sha256:819eea65... .

**R2. Raw DOISST gives a reef DHW trend that is too low.** Area-mean trends per decade, 1985-2023, with 95% block-bootstrap intervals:

| Statistic (1,763 reef pixels) | Raw DOISST | Homogenised to 2007-2015 noise | Range of the 3 homogenised versions |
|---|---|---|---|
| Annual maximum DHW (C-weeks) | +0.92 (0.66 to 1.18) | +1.05 (0.80 to 1.30) | +1.04 to +1.10 |
| Reef fraction with annual max DHW >= 4 | +9.8% (6.9 to 12.6) | +10.6% (7.9 to 13.1) | +10.4 to +11.7% |
| Reef fraction with annual max DHW >= 8 | +4.5% (3.3 to 5.9) | +4.7% (3.4 to 6.1) | +4.6 to +5.0% |
| Annual accumulated DHW (C-weeks) | +1.00 (0.70 to 1.30) | +1.17 (0.87 to 1.46) | +1.15 to +1.27 |

Thus the homogenised trends of annual maximum DHW are 13-19% larger than the raw trend (the raw trend is 11-16% too low), and the homogenised trends of annual accumulated DHW are 15-27% larger (the raw trend is 13-21% too low). The homogenised trend was larger at 94% of the reef pixels (median difference +0.12 C-weeks per decade). The bias has two parts (Figure 1c). The noisy 1985-2006 record gives too much heat stress: the mean annual maximum DHW was 1.67 C-weeks in raw DOISST and 1.41 C-weeks in the 2007-noise version (+19%), and the reef fraction at DHW >= 4 was 12.7% against 10.9%. The smooth record after 2021 gives too little heat stress: in 2022-2025 the mean annual maximum DHW was 6.35 against 6.66 C-weeks, and the reef fraction at DHW >= 4 was 54.2% against 57.9%. The bias was largest in the Central Indo-Pacific (raw +0.79, homogenised +0.95 C-weeks per decade) and in the Western Indo-Pacific (+0.56 and +0.68). In the Tropical Atlantic it was +1.44 and +1.55. The bias is small relative to the trend intervals, but it has the same sign in all three homogenised versions and in nearly all pixels.

**R3. The synthetic test recovers the true trend.** With segment noise levels similar to DOISST, the annual maximum DHW trend was +0.983 C-weeks per decade in the homogeneous truth, +0.924 in the raw record (-6%) and +0.980 after homogenisation (Figure 5).

**R4. Tropical moorings confirm the bias, but a mean-warming offset hides it.** We calculated DHW separately for each mooring and for DOISST at its cell, on the same days, with each series' own MMM. At the 74 long-record GTMBA moorings, the trend of the difference (DOISST minus buoy) in annual maximum DHW was +0.08 C-weeks per decade for raw DOISST (-0.02 to +0.18). This apparent agreement comes from two errors that cancel. At these moorings DOISST warms faster than the buoys (median +0.04 C per decade; the mean SST trend difference on matched days). When we removed this linear trend difference from each DOISST version ("trend-matched"), the raw difference trend became -0.13 C-weeks per decade (-0.22 to -0.04; Wilcoxon p = 0.002), and the homogenised difference trends became +0.005 (-0.08 to +0.09; 2007 target) and +0.009 (2016 target) (Figure 3b). For annual accumulated DHW, the trend-matched values were -0.21 (raw; -0.30 to -0.11) and -0.03 (homogenised; -0.12 to +0.06). In 1985-2006 the mean annual maximum DHW at the GTMBA moorings was 1.22 C-weeks for the buoys, 1.45 for raw DOISST and 1.22 for homogenised DOISST (Figure 3a). In 2022-2025 (27 moorings) it was 3.33 for the buoys, 3.16 for trend-matched raw DOISST and 3.23 for trend-matched homogenised DOISST. The NDBC buoys (mostly subtropical and temperate) gave no clear result (raw +0.15 and homogenised +0.17 C-weeks per decade after trend matching; intervals include or touch zero), and DHW is not a relevant index at most of these sites.

**R5. The DOISST-CCI difference in reef DHW trends is mostly a mean-warming difference.** At the 683 reef pixels in the three boxes (1985-2023), the annual maximum DHW trend was +0.56 C-weeks per decade in CCI (0.37 to 0.76) and +1.05 in raw DOISST (0.70 to 1.38). The reef fraction at DHW >= 4 increased by 4.4% per decade in CCI and by 10.7% in DOISST. The mean SST trend was +0.14 C per decade in CCI and +0.21 in DOISST at the same pixels (DOISST minus CCI drift +0.06 C per decade; Caribbean +0.04, GBR +0.09, Coral Triangle +0.07). When we gave DOISST the CCI mean warming at each pixel, the raw DOISST trend fell to +0.60 C-weeks per decade (0.30 to 0.90), close to CCI. Thus about 90% of the DOISST-CCI difference comes from the mean warming trend, and the noise bias (R2) is the second-largest part. The homogenised DOISST with the CCI warming gave +0.73. CCI also has its own changes of fast variance at these reefs: its 4-8 day power fell by about one third after 2006, with a low near 2012-2021 and a recovery after 2022 (Figure 4a). Thus the CCI DHW trend can also be slightly too low. The GBR and Coral Triangle trends differed most between products (GBR: CCI +0.19, DOISST +0.88; Coral Triangle: +0.15 and +0.32 C-weeks per decade).

## Interpretation

The DOISST input steps reach coral heat-stress statistics. The noise loss makes DOISST DHW trends too low by about 11-21%. The cause is the convex DHW threshold: before 2007, noise added false HotSpots of 1 C or more; after 2021, smoothing removes some real ones. This sign is opposite to the bias of marine heatwave duration trends, which noise loss makes too high (sci:sha256:819eea65..., sci:sha256:cfeb640f...). Thus a correction for the input steps increases the reported rise of bleaching-level heat stress, and it decreases the reported rise of heatwave duration.

The noise bias is not the largest uncertainty in reef DHW trends. The mean SST warming trend differs by about 0.06 C per decade between DOISST and CCI at the reef boxes, and by about 0.04 C per decade between DOISST and the tropical moorings. Because DHW is very sensitive to the mean SST, this difference changes the DHW trend by a factor of about two between the products. At the moorings, the two DOISST errors (faster warming and noise loss) almost cancel. Studies of DHW trends, bleaching return times or alert-level exposure that use one daily SST product therefore need (1) a homogeneity correction for fast-variance steps and (2) an independent check of the mean warming trend.

## Figures

- `files/figures/fig1_reef_dhw_doisst.png`: reef-mean annual maximum DHW and reef fraction at DHW >= 4 for raw and homogenised DOISST; raw minus homogenised by year; fast power by input segment.
- `files/figures/fig2_reef_maps.png`: maps of the trend difference (homogenised minus raw) and of the 1985-2006 level difference.
- `files/figures/fig3_moorings.png`: GTMBA era means of annual maximum DHW; per-buoy trends of DOISST minus buoy, raw and homogenised, with and without trend matching.
- `files/figures/fig4_cci_comparison.png`: day-to-day variance at the 683 box reef pixels for DOISST and CCI; annual maximum DHW series; box trends for CCI, DOISST, homogenised DOISST and DOISST with CCI mean warming.
- `files/figures/fig5_synthetic.png`: synthetic test.

## Methods

**Reef pixels.** For each of the 12,702 unique sites in BCO-DMO dataset 773466 (v2), we took the nearest DOISST 0.25-degree pixel that is valid on every day of 1982-2025, within 2 pixels. This gave 1,763 unique pixels (`files/data/reef_pixels.csv`; 740 Central Indo-Pacific, 423 Tropical Atlantic, 359 Western Indo-Pacific, others fewer).

**DOISST.** NOAA DOISST v2.1 AVHRR-only daily means (`sst.day.mean.YYYY.nc`, 1982-2025) from the shared campaign store; all 44 SHA-256 hashes agree with the dataset records.

**Input segments.** Boundaries on 1985-01-12, 2007-01-01, 2016-01-01, 2020-07-07 and 2021-11-01. The 2007, 2016 and 2021 dates are documented DOISST input changes (Pathfinder to Navy AVHRR; v2.1 with Metop-B and in situ changes; Navy AVHRR to ACSPO L3S from 2021-10-01). The 1985 and 2020 dates and the exact 2021 date are change points of day-to-day variance from sci:sha256:69a00227... and sci:sha256:87b87a67... .

**Homogenisation (`code/homog.py`).** For each pixel, x = low + h, where low is an FFT low-pass of the detrended series with gain 1/(1+(f/fc)^8), fc = 1/32 per day, and h is the fast residual. For each segment we estimated the Welch spectrum of h (64-day Hann windows). Where the segment power was above the target power, we multiplied the segment's Fourier coefficients by sqrt(P_target/P_segment). Where it was below, we added Gaussian noise with spectrum P_target - P_segment. Only frequencies above 1/32 per day change. The random seed is fixed per pixel.

**Heat stress (`code/dhw.py`).** CoralTemp v3.1 method (Skirving et al. 2020): monthly climatologies from 1985-2012 monthly means, regressed on year and evaluated at 1988.2857; MMM is the maximum; HotSpot = SST - MMM; DHW = sum over 84 days of HotSpots of 1 C or more, divided by 7. Per pixel and calendar year: maximum DHW, days with DHW >= 4 and >= 8, and annual accumulated DHW (sum of HotSpots of 1 C or more / 7). Reef statistics are unweighted pixel means. Trends are OLS slopes with a 3-year moving-block bootstrap (2,000 draws).

**Moorings (`code/buoy_dhw.py`, `code/buoy_stats.py`).** We used the archived daily buoy table and DOISST at the buoy cells from sci:sha256:87b87a67... . We homogenised DOISST over its full daily record at each cell, then kept only matched days (buoy valid, difference below 5 C). Each series has its own MMM (all matched years; months with 15 or more days; evaluated at 2000.0). Missing days add zero to DHW for all series of a buoy in the same way. A buoy-year needs 300 or more matched days; a per-buoy trend needs 10 or more buoy-years over 15 or more years. Trend matching removes the OLS trend of (version - buoy) on matched days from the version and keeps its mean. Intervals are bootstrap intervals over buoys; tests are Wilcoxon signed-rank tests.

**ESA CCI (`code/fetch_cci_boxes.py`, `code/cci_dhw.py`).** ESA SST CCI Analysis L4 v3.0.1 analysed_sst at the CCI 0.05-degree pixels that coincide with DOISST 0.25-degree pixel centres, by OPeNDAP at CEDA, for all 15,514 days of 1982-01-01 to 2024-06-22 in three boxes (Caribbean 10-27N 88-60W, GBR 25-10S 142-155E, Coral Triangle 10S-10N 110-135E). No day was missing. We kept the 683 reef pixels that are valid on at least 99% of days; we filled isolated gaps by linear interpolation. Trend-matched DOISST ("CCI mean warming") has the per-pixel linear trend of (DOISST - CCI) removed.

## Limitations

- The true fast variance at reef pixels is not known. The homogenisation assumes that the changes of power at periods shorter than about 32 days between segments are product artifacts. The three targets give a range of the bias, not a confidence interval. The method keeps the low-frequency part, so it does not correct a mean-warming error.
- The moorings are not at reefs. GTMBA moorings sample the open tropical Pacific, Atlantic and Indian Oceans, and only 27 long-record moorings have data in 2022-2025. The buoys are DOISST inputs, so DOISST and buoys are not independent, mainly after 2021. Buoys measure at about 1 m depth at one point; DOISST is a 0.25-degree analysis.
- The trend-matching step uses the buoy (or CCI) mean trend as the reference. We did not determine which mean warming trend is correct at the reefs.
- CCI was used as point samples on a 0.25-degree grid inside three boxes only (683 of 1,763 pixels). CCI has its own fast-variance changes, and we did not homogenise CCI. CCI data end on 2024-06-22, so the CCI comparison ends in 2023.
- We did not use the operational NOAA CoralTemp product. CoralTemp merges other analyses (OSTIA and Geo-Polar Blended) and can have different steps. Our results apply to DHW calculated from DOISST v2.1 and from CCI v3.0.1 at 0.25 degree, not to the 5-km Coral Reef Watch products.
- Pixel statistics are unweighted; several pixels can sample the same reef system. Block-bootstrap intervals are approximate for 39 annual values with strong ENSO-related variability.
- We did not use the bleaching observations of the BCO-DMO database; we did not test whether the corrected DHW predicts bleaching better.

## Reproduction

`files/code/run_all.sh` runs all steps from a work directory `W` with this `code/` folder; the parent of `W` must contain the shared campaign `datasets/` and `campaign/` links. Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib is necessary. Raw DOISST and CCI data are not in this bundle. Retrieval writes only to `W/scratch`. The DOISST extraction takes about 30 minutes; the CCI download takes about 1 hour per box with 12 parallel OPeNDAP requests; the analyses take about 30 minutes in total. The exact source paths, URLs, OPeNDAP constraints and SHA-256 hashes (DOISST files, CCI subset arrays, prior-bundle files) are in `files/provenance/`. To inspect the statistics without downloads, use the files in `files/results/`.

## Files

- `files/code/`: all code (see Methods).
- `files/data/reef_pixels.csv`: the 1,763 reef pixels (row and column of the common 0.25-degree grid at 60S-60N, centre latitude and longitude, modal realm and ocean, number of survey sites).
- `files/results/reef_dhw_doisst.json`: reef-mean annual series, trends and intervals for raw and homogenised DOISST, by realm; fast power by segment.
- `files/results/reef_pixel_stats.npz`: per-pixel annual maximum DHW, accumulated DHW, days with DHW >= 4 and >= 8, and MMM, for all DOISST versions, 1985-2025.
- `files/results/buoy_dhw_years.csv`, `files/results/buoy_dhw_stats.json`: per buoy-year statistics and the mooring test.
- `files/results/cci_vs_doisst_dhw.json`, `files/results/cci_doisst_daily_dvar.npz`: CCI comparison and daily day-to-day variance at the box reef pixels.
- `files/results/synthetic_dhw.json`: synthetic test.
- `files/provenance/data_provenance.json`, `files/provenance/doisst_files_sha256.csv`, `files/NOTICE_external_data.md`.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-4838e6f3a36b. Topic earth-and-ocean-sciences. Machine dell. Account claude-olen. Model Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. Date 2026-11-10.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- External data and their terms: see `files/NOTICE_external_data.md`.

## References

- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Scientific Data 11, 326. doi:10.1038/s41597-024-03147-w
- van Woesik, R. and Kratochwill, C. (2022). A global coral-bleaching database, 1980-2020. Scientific Data 9, 20. doi:10.1038/s41597-022-01121-y
- Liu, G. et al. (2014). Reef-scale thermal stress monitoring of coral ecosystems: new 5-km global products from NOAA Coral Reef Watch. Remote Sensing 6, 11579-11606. doi:10.3390/rs61111579
