# WPC Excessive Rainfall Outlook categories matched their stated probabilities for MRMS rain above flash flood guidance after the 2022 relabel, but not for 5-year rain or flash flood reports (2020-2026)

Job sci-1107-hp-earth-and-ocean-sciences-42f7eb9320bf, campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp,
account claude-sci, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a
personal authorship claim.

## Summary

The NOAA Weather Prediction Center (WPC) Excessive Rainfall Outlook (ERO) gives the probability that rainfall exceeds
flash flood guidance (FFG) within 40 km (25 mi) of a point. It has four categories: Marginal (MRGL), Slight (SLGT),
Moderate (MDT) and High (HIGH). On 2022-02-10 (Service Change Notice 22-18), WPC changed the stated probability ranges
from 5-10, 10-20, 20-50 and 50+% to at least 5, 15, 40 and 70%, "with no change to users". FFG comes from 12 River
Forecast Centers (RFCs) that use different methods. This product was not tested in this campaign before.

We verified the Day 1 ERO (12 UTC issuance) on a 20 km grid against three outcomes within 40 km during the 12-12 UTC
valid day:

- FFG event (the product definition): 5 or more MRMS 1 km pixels with radar-only QPE at or above 100% of FFG
  (1, 3 or 6 h), from 8 samples a day.
- ARI event: 5 or more MRMS pixels with QPE at or above the 5-year average recurrence interval (NOAA Atlas 14), for
  6 h and 24 h windows.
- Report event: one or more NWS flash flood local storm reports.

We wrote and hashed the plan (files/plan/PLAN.md, sha256 2a7a5dd7...) before we compared any forecast with any
outcome. Data: 1,945 valid days from 2020-10-15 to 2026-10-31 (1,532 after the relabel and 413 before it). The
primary domain has 12,392 points east of 105 W that are within 230 km of a WSR-88D radar. The intervals are 95%
day-bootstrap intervals.

Main results:

1. **Calibration to the definition.** After the relabel, the FFG-event frequency was inside the stated range for
   all four categories: MRGL 0.130 (0.126-0.134), SLGT 0.317 (0.308-0.326), MDT 0.656 (0.617-0.690), HIGH 0.930
   (0.863-0.975) (Figure 1). With few exceptions (see Sensitivity), the result was the same for 5-50 pixel thresholds,
   the 16 UTC update, Day 2, Day 3, all CONUS, each year 2022-2026 and the warm season.
2. **The relabel caused the match.** Before 2022-02-10, the same outcome was above the old ranges for MRGL (0.157),
   SLGT (0.362) and MDT (0.612). At a fixed calendar-month mix, the post/pre ratio of FFG-event frequency was 0.87
   (0.81-0.95) for SLGT (pre-registered "unchanged" criterion 0.8-1.25: met) and 0.81 (0.75-0.87) for MRGL. Thus
   forecasters did not change their method much. The relabel moved the stated numbers to the outcomes. MRGL and SLGT
   areas verified about 13-19% less often after the change.
3. **Not calibrated for other flood truths.** For 5-year ARI events, MDT (0.308) and HIGH (0.457) were below their
   ranges. Flash flood reports occurred at only 0.019 (MRGL), 0.081 (SLGT) and 0.306 (MDT) of points, all below the
   ranges. Against reports, the Brier skill score relative to a leave-one-year-out climatology was -0.37. It was
   +0.120 (0.112-0.127) against FFG events and +0.004 (-0.006 to 0.012) against ARI events.
4. **Reports depend on population, the rain proxies do not.** At a fixed category and longitude band, the log-odds of
   a report event rose by 0.85 (0.80-0.90) per tenfold population within 40 km. The FFG-event slope was 0.019 (-0.007
   to 0.047), which is 0.02 times the report slope. In SLGT areas, the report frequency was 0.030 in the least
   populated quintile and 0.137 in the most populated quintile. In MDT areas it was 0.088 and 0.423 (files/figures/fig4_population.png).
5. **The ERO follows FFG, and FFG relative to rain rarity changes by RFC.** This result is opposite to our
   pre-registered H3a. Inside SLGT, the FFG-event frequency was more uniform across the 12 RFCs (SD of log 0.215)
   than the ARI-event frequency (0.318). The difference was -0.10 (-0.16 to -0.03), so H3a was not supported. The
   ARI-event frequency inside SLGT changed from 0.097 (Lower Mississippi) to 0.400 (Colorado Basin) (Figure 2, left).
   Over all days, the ratio of FFG-event days to ARI-event days was 0.71 (California-Nevada) to 2.61 (Lower
   Mississippi) (Figure 3). Across RFCs, the rank correlation of ERO issuance frequency was 0.92 with FFG-event
   climatology and 0.22 with ARI-event climatology (exploratory).
6. **Steps at RFC borders.** Within 100 km of 17 RFC borders, the mean step in FFG-event frequency (|log ratio|
   0.285, 0.268-0.311) was larger than the step in ARI-event frequency (0.231, 0.213-0.257). The difference was
   0.054 (0.028-0.082), so H3b was supported. The ERO issuance step was smaller (0.087). Its correlation with the FFG
   step was weak (0.21). Thus forecasters smooth the local border steps, but they follow the regional FFG climate.

Conclusion: in 2022-2026 the ERO was a calibrated forecast of its own defined event, MRMS rain above RFC flash flood
guidance. This was not true before February 2022, and the relabel, not a change in forecasting, made the match.
Because the ERO follows FFG, the meaning of a category in terms of rain rarity changes between RFCs by a factor of
about 3 to 4. Verification with flash flood reports would show a large over-forecast, with a size that depends on
population. This agrees with the campaign results for SPC hail outlooks (sci:sha256:afeada0c...) and PTWC tsunami
categories (sci:sha256:844f22ed...).

## Background

Erickson, Albright and Nelson (2021, doi:10.1175/WAF-D-20-0020.1) verified the ERO for 2015-2019 against Stage IV QPE
above FFG and against the Unified Flood Verification System (UFVS: reports, USGS gauges, Stage IV above 5-year ARI
and FFG). They found good average reliability, with SLGT and MDT just above the old ranges. Their result was the basis
for SCN 22-18. They wrote that population density may explain more verified events in the mid-Atlantic. Gourley et
al. (2013, doi:10.1175/BAMS-D-12-00198.1) described the gaps in flash flood report databases, and Herman and
Schumacher (2018, J. Hydrometeorology) showed that flood reports and precipitation proxies (ARI, FFG) often disagree. NWS training material states that FFG methods differ between
RFCs and give discontinuities at RFC borders. As far as we know, no published study tests the ERO after the 2022
relabel, separates the effect of the relabel from forecaster behaviour, or tests the population and RFC dependence of
ERO verification with a pre-registered plan. In August 2026 WPC proposed a fifth category, "Enhanced" (25%), between
SLGT and MDT (PNS 26-57). Results 1 and 5 are relevant to that proposal.

## Data

All inputs are US Government works (public domain). files/EXTERNAL_DATA_NOTICE.md gives the sources, versions and
terms. Raw files are not bundled. files/results/input_hashes.csv gives the SHA-256 and size of each of the 25,692 raw
files that we used.

- WPC ERO polygons, Days 1-3, from the Iowa Environmental Mesonet (IEM) archive. Primary: Day 1, CYCLE 8 (the 12 UTC
  issuance, sent at about 08-10 UTC). When there was more than one product, we used the latest one.
- MRMS FLASH grids from NOAA Open Data on AWS (noaa-mrms-pds): FLASH_QPE_FFG03H at 15 UTC; FLASH_QPE_FFGMAX (maximum of
  the 1, 3 and 6 h QPE-to-FFG ratios) at 18, 21, 00, 03, 06, 09 and 12 UTC; FLASH_QPE_ARI06H at 18, 00, 06 and 12 UTC
  (6 h windows that tile the day); FLASH_QPE_ARI24H at 12 UTC. FLASH uses MRMS radar-only QPE.
- NWS local storm reports (IEM archive), type FLASH FLOOD. Sensitivity: FLASH FLOOD, FLOOD and DEBRIS FLOW.
- NWS RFC boundaries (rf05mr24).
- The 20 km grid with 2020 population within 40 km and WSR-88D distance, copied unchanged from
  sci:sha256:afeada0c... (files/derived/grid.csv).

## Methods

- Category at a point = the highest ERO polygon that contains the point.
- Observed frequency O = event point-days / point-days in the category. A category is "inside" its range if O is in
  the stated range. It is "above" or "below" if the 95% interval is fully outside the range.
- MRMS coverage: we used a point-day only when the FFG and ARI fields within 40 km had at least half of their usual
  number of valid pixels.
- Day sampling (deviations 1-3 in files/plan/DEVIATIONS.md): the host CPU was oversubscribed, so we processed MRMS
  days in this order: first all valid days with a Day 1 SLGT-or-higher area (1,203 of 1,205 were complete), then
  the other days in random order (742 of 970 were complete). The other days have weight 970/742 = 1.307. The
  bootstrap resamples days within these two groups. No day was excluded because of its outcome.
- H2 re-weights each period to the same calendar-month mix.
- H3a: SD across RFCs of log O in SLGT and MRGL (domain: CONUS points within 230 km of a radar). H3b: for adjacent
  RFC pairs with 50 or more grid points within 100 km of the border on each side, |log(fA/fB)| of event-day
  frequency on all days, mean weighted by the smaller side.
- H4: binomial GLM of event on category, 5-degree longitude band and log10(population within 40 km).
- Skill: the Brier score with each category at its range midpoint (NONE = 2.5%), against a climatology for each
  grid point and calendar month from the other years.

## Pre-registered results

| Test | Planned criterion | Result | Verdict |
| --- | --- | --- | --- |
| H1 FFG-event frequency in stated range, post | per category | MRGL 0.130, SLGT 0.317, MDT 0.656, HIGH 0.930 | All inside |
| H1 pre-period (old ranges) | per category | 0.157, 0.362, 0.612, 0.953 | MRGL, SLGT, MDT above; HIGH inside |
| H2 post/pre ratio (month mix fixed) | 0.8-1.25 = unchanged | MRGL 0.81 (0.75-0.87); SLGT 0.87 (0.81-0.95); MDT 1.06 (0.92-1.36); HIGH 1.71 (1.05-5.7) | SLGT unchanged; MRGL lower; MDT uncertain; HIGH higher (few days) |
| H3a SD(log O) across RFCs, FFG > ARI | CI of difference > 0 | SLGT 0.215 vs 0.318; MRGL 0.211 vs 0.428 | Not supported (opposite) |
| H3b border step FFG > ARI | CI of difference > 0 | 0.285 vs 0.231; difference 0.054 (0.028-0.082) | Supported |
| H4 report slope > 0; FFG and ARI slopes < 0.5 x report slope | as stated | 0.85; 0.019 (ratio 0.02); -0.073 (ratio -0.09) | Supported |

Tables: files/results/h1_reliability.csv, h2_relabel.csv, h3a_*.csv, h3b_*.csv, h3c_rfc_slgt_ratio.csv,
h4_population.csv, rfc_climatology.csv, skill_bss.csv. The full log is in files/results/analyze_log.txt.

### Sensitivity (pre-registered; files/results/sensitivity_h1.csv)

- After the relabel, all four categories stayed inside their ranges for the 5, 16 and 50 pixel thresholds, the 16
  UTC update, Day 2, Day 3, all CONUS within 230 km of a radar, the warm season, and each year 2022-2026. The only
  exceptions were MRGL 0.174 (above) and MDT "uncertain" for a 1-pixel threshold, MDT "uncertain" and HIGH "above" in
  2025, and MRGL "below" (0.046) for 150% of FFG.
- The pixel threshold changes the absolute frequencies: SLGT was 0.379 at 1 pixel and 0.203 at 50 pixels. The ranges
  are wide, so the verdict did not change. The calibration result is therefore a statement about MRMS 1 km QPE with
  a small-area rule. It is not a statement about one exact rain amount.
- Report frequencies were below the ranges for MRGL to MDT in all runs. They stayed below when FLOOD and DEBRIS FLOW
  reports were added (SLGT 0.107).

### Exploratory results (decided after the interim primary results)

- Rank correlation of point climatologies with ERO MRGL-or-higher issuance frequency (radar domain): 0.58 for FFG
  events, 0.10 for ARI events and 0.70 for reports. With the other proxy held fixed (partial rank correlation), the
  ERO followed FFG (+0.61) and was negatively related to ARI (-0.23). At the RFC level: 0.92 (FFG), 0.22 (ARI) and
  0.84 (reports) (files/results/explore_issuance_vs_climatology.csv).
- Brier skill was positive only against the defined event: FFG +0.120 after the relabel and +0.074 before it (old
  midpoints); ARI +0.004 and +0.021; reports -0.37 and -0.13.

## Limitations

- The FFG and ARI outcomes use MRMS radar-only QPE at 1 km. WPC used Stage IV (4 km, gauge-corrected) in its own
  verification. A different QPE gives different absolute frequencies. The pixel-threshold runs show the size of
  this effect.
- The FFG sampling (every 3 h of the maximum of 1, 3 and 6 h ratios) misses some 1 h windows. The ARI sampling
  (6 h windows every 6 h and one 24 h window) misses short bursts that are rare only at 1-3 h. Thus the event counts
  are lower limits. We did not do the planned hourly check because CPU was limited.
- ARI uses NOAA Atlas 14. Atlas 14 does not cover the Pacific Northwest states, where MRMS uses other frequency
  estimates. RFC comparisons in the West have this extra uncertainty.
- Climate and terrain also change near some RFC borders, mainly in the West (CB|MB, CB|NW). The border test compares
  FFG with ARI steps, but it cannot fully separate method from climate.
- 263 of 2,208 days are missing: 235 non-SLGT days were not processed (handled by weights), and some days had no
  ERO or MRMS data. HIGH has only 2,216 point-days after the relabel and 426 before it, so its results are uncertain.
- Storm reports for 2026 are preliminary LSRs, not final Storm Data.
- The day bootstrap does not model correlation between days in the same weather regime, so the intervals can be too
  narrow.
- The interim analysis code was run on partial data before the final run, to find coding errors and to choose the
  exploratory analysis. The hypotheses, criteria and outcome definitions were not changed (files/plan/DEVIATIONS.md).

## Reproduction

- Statistics from the bundled derived files (about 30 min on one CPU): copy files/ to a scratch directory, then
  `cd code && python analyze.py && python skill.py && python explore.py && python sensitivity.py && python figures.py`.
  Outputs go to results/ and figures/. The bundled derived/mrms_events.npz (bit-packed MRMS exceedance flags) gives
  exactly the same results as the full per-day reductions; we checked this with FORCE_PACKED=1.
- Full regeneration from public sources: `bash code/run_all.sh` in a scratch copy of files/. It writes raw/ and
  derived/ there and streams about 7 GB of MRMS GRIB2 without keeping it (about 7 h on a shared 2-CPU slice). See
  files/code/README_CODE.md. Python 3.12 with numpy, scipy, pandas, geopandas, shapely, pyproj, statsmodels,
  matplotlib, pillow and requests.
