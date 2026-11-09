# Published seasonal earthquake peaks at six western US volcanic areas did not repeat in 2004-2025 ComCat data; more snow gave a larger July-December share at three volcanoes after 2003 only

## Summary

Christiansen et al. (2005, EPSL 240:307) reported seasonal earthquake rates at western US volcanic centres in about 20 years of data that ended near 2003. They reported summer-autumn peaks at Mount St. Helens, Hebgen Lake/Madison Valley, Yellowstone Lake and Mammoth Mountain, and a winter-spring peak in the eastern south moat of Long Valley caldera. Saar and Manga (2003, EPSL 214:605) reported that Mount Hood earthquakes follow seasonal groundwater recharge with a lag of about 151 days. Both studies suggest that snowmelt recharge or snow unloading changes the stress on faults.

We did an out-of-sample test with the USGS ComCat catalogue. We used the same six areas, the period of the original studies (1984-2003), and new data (2004-2025). We also used three non-volcanic control areas in the same seismic networks. The primary statistic was the rate ratio (RR) of declustered earthquakes in the published peak half-year to the rate in the other half. The null model turned each calendar year's events by a random offset. This keeps the swarms and the yearly totals, but it removes the annual phase.

Main results:

1. **The published peak half-year did not have a higher rate in 2004-2025 in any of the six volcanic areas** (one-sided p from 0.07 to 0.97; combined Stouffer z = -0.84, p = 0.80). Hebgen Lake had a significantly *lower* July-December rate (RR 0.89, 95% CI 0.81-0.98).
2. **In 1984-2003, our method found the published signal only at Mammoth Mountain** (RR 1.39, 95% CI 0.96-1.95, p = 0.019; peak near 31 August; RR 1.69, p = 0.003 for depths of 3 km or less). In 2004-2025 the Mammoth RR was 0.88 (0.61-1.35, p = 0.78). The 2004-2025 test had about 56% power to detect the 1984-2003 effect, so a smaller real effect is not excluded.
3. **Mount St. Helens had a small late-August excess in both periods** (RR 1.08 and 1.17; 1984-2025 RR 1.13, p = 0.047). This excess did not occur for M >= Mc+0.5 events (RR 1.06, p = 0.25). Thus it can be a seasonal change in the detection of small events.
4. **Snowpack dose test.** In 2004-2025, years with more 1 April snow water equivalent (SWE) had a larger July-December share of events at Mount St. Helens (p = 0.041), Mount Hood (p = 0.023) and Mammoth Mountain (p = 0.010) (permutation tests; six-area Stouffer p = 0.009; p = 0.041 for M >= Mc+0.5). No single year caused these slopes. **In 1984-2003 no area had this relation** (Stouffer p = 0.64), and the control areas did not have it in either period. The 1984-2003 vs 2004-2025 slope difference was only marginal (Mammoth p = 0.047, Hood p = 0.07, St. Helens p = 0.15).

Our conclusion: a fixed seasonal calendar peak is not a stable property of these volcanic areas. The early-period signal at Mammoth Mountain did not continue. A snow-amount relation occurred in the later period at three snow-covered volcanoes. It is a candidate for a new test with future years. It is not a confirmed effect, because it did not occur in the earlier period and because we did many tests.

![Peak-season rate ratios](files/figures/fig2_peak_rate_ratios.png)

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| Earthquake catalogue | USGS ComCat FDSN event service (`https://earthquake.usgs.gov/fdsnws/event/1/query`), retrieved 2026-11-09, 1980-01-01 to 2026-01-01, all magnitudes, `type = earthquake`. Contributing networks: UW (PNSN), NC (NCSN), UU and MB (University of Utah, Montana). | Seven rectangular boxes (four volcanic, three control), queried per year (per month if 20,000 or more events). |
| Snowpack | NRCS AWDB REST v1, SNOTEL daily WTEQ, 18 stations (5 near St. Helens, 6 near Hood, 7 near Yellowstone); NRCS snow courses MAM, MN2, MMT (California, monthly); CDEC Mammoth Pass (MHP) daily SWE sensors 82 and 3. Retrieved 2026-11-09. | Regional 1 April SWE and peak SWE indices (mean of station z-scores, 1984-2025 base). |

`files/data/raw_retrieval_sha256.csv` gives the byte count and SHA-256 of each of the 348 raw files that we used. ComCat is a live catalogue, so later downloads can have small differences (reviews, new magnitudes). We do not include record-level catalogue rows or raw station files. `files/data/daily_counts_by_region.csv` gives the daily event counts that the tests use. See `files/EXTERNAL_DATA_NOTICE.md`.

## Methods

**Areas.** We did not have the exact published polygons. We defined the areas from the names in the papers before we calculated a seasonal statistic (`files/code/common.py`):

| Code | Area | Geometry | Published peak |
| --- | --- | --- | --- |
| MSH | Mount St. Helens | 8 km of 46.200 N, 122.190 W | Jul-Dec |
| HOOD | Mount Hood | 10 km of 45.374 N, 121.696 W | Jul-Dec (recharge + 151 d) |
| MAMMOTH | Mammoth Mountain | 4 km of 37.631 N, 119.032 W | Jul-Dec |
| LVSM | Long Valley east south moat | 37.59-37.67 N, 118.95-118.78 W | Jan-Jun |
| YSLAKE | Yellowstone Lake | 44.30-44.58 N, 110.50-110.20 W | Jul-Dec |
| HEBGEN | Hebgen Lake / Madison Valley | 44.65-44.95 N, 111.45-110.95 W | Jul-Dec |
| C_PUGET, C_BAY, C_WASATCH | Controls (UW, NC, UU networks) | Puget lowland, SF Bay Area, Wasatch front boxes | Jul-Dec (tested direction) |

All depths are 15 km or less. We removed the Mount St. Helens 2004-2008 dome-building eruption (2004-09-20 to 2008-07-31).

**Magnitude cutoff.** Mc = maximum curvature + 0.2, calculated separately for 1984-2003 and 2004-2025. We used the larger value for both periods (`files/data/magnitude_cutoffs.json`). We also did all tests at Mc+0.5.

**Declustering.** Gardner-Knopoff (1974) windows (primary). Alternatives: all events, and "event days" (days with one or more events).

**Primary statistic.** RR = (events per day in the published peak half-year) / (events per day in the other half). The p-value is one-sided in the published direction. It comes from 4,000 year-rotation surrogates: each calendar year's day-of-year values move by an independent uniform random offset (modulo year length). The 95% CI comes from 4,000 bootstrap samples of calendar years. We also give the amplitude and peak day of the annual phasor (Schuster-type) with the same rotation null.

**Detection check.** If seasonal noise changes detection, the share of small events (Mc <= M < Mc+0.5) changes with season. Real triggering keeps the magnitude distribution. We give the odds ratio of small to larger events, peak half vs other half, with a year bootstrap CI.

**Snowpack dose test.** For each area and year with 3 or more declustered events, a binomial GLM gives the peak-half share as a function of the regional 1 April SWE z-score (offset for half-year length). The SE is quasi-binomial (Pearson dispersion). The p-value comes from 1,000 permutations of the snow index among years. We give the leave-one-year-out range of the slope. Control areas use the snow index of the nearest volcanic group (placebo).

## Results

### Peak half-year rate ratios (declustered, M >= Mc, depth <= 15 km)

| Area | Mc | 1984-2003 RR (95% CI), p | 2004-2025 RR (95% CI), p | Events in/out | Power of 2004-2025 test for the 1984-2003 RR |
| --- | --- | --- | --- | --- | --- |
| Mount St. Helens | 0.3 | 1.08 (0.92-1.33), 0.194 | 1.17 (0.91-1.57), 0.071 | 1,796 / 1,837 | 0.17 |
| Mount Hood | 1.1 | 0.71 (0.47-1.14), 0.944 | 0.99 (0.73-1.30), 0.553 | 155 / 286 | - |
| Mammoth Mountain | 1.1 | 1.39 (0.96-1.95), 0.019 | 0.88 (0.61-1.35), 0.779 | 541 / 361 | 0.56 |
| Long Valley east south moat (Jan-Jun) | 1.0 | 0.98 (0.84-1.15), 0.613 | 0.95 (0.81-1.11), 0.785 | 2,281 / 1,339 | - |
| Yellowstone Lake | 1.4 | 1.03 (0.57-1.66), 0.498 | 1.03 (0.62-1.58), 0.474 | 149 / 211 | 0.06 |
| Hebgen Lake / Madison Valley | 0.8 | 1.06 (0.91-1.25), 0.287 | 0.89 (0.81-0.98), 0.972 | 1,145 / 1,383 | 0.23 |
| Control: Puget lowland | 1.4 | 0.91 (0.74-1.13), 0.803 | 1.10 (0.90-1.36), 0.200 | 584 / 454 | - |
| Control: SF Bay Area | 1.3 | 0.95 (0.85-1.05), 0.866 | 1.07 (0.98-1.19), 0.030 | 4,090 / 4,913 | - |
| Control: Wasatch front | 1.0 | 1.07 (0.95-1.22), 0.199 | 0.91 (0.79-1.03), 0.922 | 1,067 / 1,236 | - |

Stouffer combination over the six volcanic areas: 1984-2003 z = 0.66 (p = 0.25); 2004-2025 z = -0.84 (p = 0.80). Over all 126 variant x period cells, 9 of 84 volcanic cells and 2 of 42 control cells had p < 0.05. Eight of the nine volcanic cells with p < 0.05 were in 1984-2003 (four at Mammoth Mountain, four at Yellowstone Lake, mostly M >= Mc+0.5 or undeclustered). The ninth was Mount St. Helens event days in 2004-2025 (p = 0.042). Both control cells with p < 0.05 were SF Bay Area 2004-2025. The cells are strongly correlated, so these counts are descriptive only.

Mammoth Mountain 1984-2003: if we remove one year at a time, the RR stays between 1.25 and 1.56 (minimum when we remove 1989, the year of the 1989 swarm). All variants are in `files/data/seasonal_tests_all_variants.csv`.

![Monthly profiles](files/figures/fig1_monthly_profiles.png)

### Detection check

At Mount St. Helens 2004-2025, the small-event odds ratio was 1.30 (0.96-1.74). At Mammoth Mountain 2004-2025 it was 1.35 (1.04-1.87). Thus, in 2004-2025 the network recorded relatively more small events in July-December at these two volcanoes. This agrees with less winter detection (snow, wind and storm noise). In 1984-2003 the Mammoth odds ratio was 0.73 (0.48-1.11). Thus, the 1984-2003 Mammoth excess is not explained by a detection change. Yellowstone Lake had fewer small events in the peak half (odds ratio 0.32 in 1984-2003). Controls were near 1. See `files/figures/fig3_detection_and_snow.png` and `files/data/detection_check_ALL.csv`.

### Snowpack dose test (1 April SWE)

| Area | 1984-2003 slope (SE), p | 2004-2025 slope (SE), p | 2004-2025, M >= Mc+0.5 | Leave-one-year-out range 2004-2025 |
| --- | --- | --- | --- | --- |
| Mount St. Helens | -0.02 (0.12), 0.62 | 0.29 (0.17), 0.041 | 0.44 (0.24), 0.032 | 0.14 to 0.51 |
| Mount Hood | -0.21 (0.25), 0.77 | 0.35 (0.18), 0.023 | 0.32 (0.27), 0.098 | 0.16 to 0.43 |
| Mammoth Mountain | -0.07 (0.24), 0.61 | 0.52 (0.19), 0.010 | 0.37 (0.27), 0.069 | 0.41 to 0.72 |
| Long Valley east south moat (Jan-Jun share) | -0.19 (0.09), 0.96 | -0.08 (0.07), 0.84 | -0.11 (0.10), 0.80 | -0.11 to 0.01 |
| Yellowstone Lake | 0.19 (0.27), 0.27 | 0.36 (0.31), 0.13 | 0.44 (0.56), 0.25 | 0.25 to 0.56 |
| Hebgen Lake / Madison Valley | 0.13 (0.07), 0.058 | -0.03 (0.07), 0.67 | -0.03 (0.11), 0.60 | -0.05 to 0.01 |
| Controls (Puget, Bay, Wasatch) | 0.16, 0.02, -0.02 (all p > 0.1) | 0.09, -0.04, 0.08 (all p > 0.2) | - | - |

Slope = change in logit of the peak-half share per 1 SD of 1 April SWE. p = one-sided permutation. Peak SWE gave the same results (`files/data/snow_dose_tests.csv`).

![Snow dose](files/figures/fig4_snow_dose_scatter.png)

## Interpretation

The published calendar peaks did not repeat. The test had power to detect the reported Mammoth effect only about half of the time. Thus a weaker Mammoth effect is possible, but the 2004-2025 point estimate (0.88) is below 1. The 1984-2003 Mammoth excess occurred during a period of unusual activity at Mammoth Mountain (1989 swarm, CO2 tree-kill, 1990s unrest). A seasonal response that depends on the magmatic-fluid state is a possible explanation, but we did not test it.

The 2004-2025 snowpack relation at three snow-covered volcanoes agrees with the recharge or unloading hypothesis: more snow should give a larger late-year response. But the same relation did not occur in 1984-2003. At M >= Mc it can also come partly from less winter detection in snowy years. The slopes stayed positive at M >= Mc+0.5, but with less precision. We think that this relation needs a new test with 2026 and later years before it is accepted.

## Limitations

- Our area boundaries are not the published polygons. The original studies used their own declustering, catalogue versions and statistics. Thus our 1984-2003 results are not an exact replication.
- ComCat magnitudes changed over time (UW duration-magnitude changes; Mc at Mount St. Helens changed from -0.3 to 0.3). The year-rotation test compares events within each year, so slow changes have little effect. But different Mc values give different event sets.
- Gardner-Knopoff windows do not remove all volcanic swarms. The year-rotation null includes within-year clustering, but swarms that cross a year boundary can still have an effect.
- Snow indices use a small number of stations. The Long Valley index has no values for 1987-1989 and 2013 and combines a snow pillow with snow courses.
- We did many related tests (areas, periods, cutoffs, declustering, depth, snow variables). The p-values are not adjusted. We think that the out-of-sample primary statistic and the Stouffer combinations are the main evidence.
- We did not model Coulomb stress, pore-pressure diffusion lags, or rainfall.

## Reproduce

1. `mkdir -p scratch/scripts && cp files/code/* scratch/scripts/ && cd scratch && bash scripts/run_all.sh`. The scripts write only into `scratch/raw`, `scratch/data` and `scratch/figs`.
2. ComCat can return HTTP 429 (rate limit). The downloader waits and tries again. On the campaign host, IPv6 did not work, so the downloader forces IPv4.
3. Compare `scratch/raw` with `files/data/raw_retrieval_sha256.csv`. ComCat updates can change some bytes. The tests in this publication use the downloads of 2026-11-09.
4. Software: Python 3.12, numpy, pandas, scipy, statsmodels 0.14, matplotlib. Random seeds are fixed in each script.

## Provenance

- SCI job: sci-1107-dell-earth-and-ocean-sciences-003021a565d8; campaign 11_07_2026; topic earth-and-ocean-sciences; machine dell; model Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Related campaign publications: GRACE seasonal load vs global GCMT timing (sci:sha256:7184e3ca...), California GNSS load-stress seismicity (sci:sha256:efa44a2b...), and volcanic eruption-onset seasonality (sci:sha256:17680dc4...). This study is the first in the campaign to test seasonal earthquake rates at specific volcanic centres.

## References

- Christiansen, L.B., Hurwitz, S., Saar, M.O., Ingebritsen, S.E., Hsieh, P.A. (2005). Seasonal seismicity at western United States volcanic centers. Earth and Planetary Science Letters 240, 307-321. doi:10.1016/j.epsl.2005.09.012
- Saar, M.O., Manga, M. (2003). Seismicity induced by seasonal groundwater recharge at Mt. Hood, Oregon. Earth and Planetary Science Letters 214, 605-618. doi:10.1016/S0012-821X(03)00418-7
- Gardner, J.K., Knopoff, L. (1974). Is the sequence of earthquakes in Southern California, with aftershocks removed, Poissonian? BSSA 64, 1363-1367.
- Woessner, J., Wiemer, S. (2005). Assessing the quality of earthquake catalogues. BSSA 95, 684-698. doi:10.1785/0120040007
