# SPC Day 3 to Day 8 severe-weather contours were drawn about 80 km too tight at every lead day in 2015-2025, when reports are the truth

## Summary

The NOAA Storm Prediction Center (SPC) issues Day 3 and Day 4-8 convective outlooks for the contiguous United States (CONUS). Each contour gives the probability of a severe thunderstorm report (tornado, hail of 1 inch or more, or damaging wind of 50 kt or more) within 25 statute miles (40.2 km) of a point during the 12Z-12Z day. The Day 4-8 product has used 15% and 30% contours since December 2014 (NWS Service Change Notice 14-54). We found no published verification of the Day 4-8 probabilities. No earlier campaign result tests them.

We compared all as-issued Day 3 (about 08Z issuance) and Day 4-8 (about 09Z issuance) outlooks for 2008-2025 with the final SPC severe report database (1950-2025 files). We used a 20 km equal-area grid of 19,598 CONUS points. A point has an event when a report occurs within 40.2 km of the point during the valid day. This is the SPC verification definition. We wrote the pre-registration (`files/PREREGISTRATION.md`) before we joined the forecasts to the reports.

Main results for 2015-2025. The 95% intervals come from a bootstrap that resamples whole weeks.

1. **The area between the 15% and 30% contours verified inside its stated range at all lead days, but near the top.** The pooled Day 4-8 frequency was 0.274 (0.253-0.294) over 1,062 lead-days. The values by lead were D4 0.272, D5 0.260, D6 0.299, D7 0.304 and D8 0.253 (5 days only). The area inside the Day 4-8 30% contour verified at 0.521 (0.455-0.583). Pre-registered tests P1 and P2 passed.
2. **The frequency did not decrease with lead.** The D6-D8 frequency minus the D4 frequency was +0.028 (-0.009 to +0.064). The Day 3 15-30% band verified at 0.287, only 0.015 (0.002-0.028) above Day 4. As the lead increases, the forecasters draw fewer and smaller-coverage areas. They do not draw less reliable areas.
3. **Frequency stayed above the stated value outside the drawn contours.** Just outside (0-40 km) the Day 4-8 15% contour, the frequency was 0.191 (0.179-0.206). Thus a point that the forecast put below 15% had a frequency above 15%. The frequency fell to 15% only at 79 km (64-97 km) outside the contour. The result was the same at each lead: D4 70 km, D5 81 km, D6 114 km, D7 95 km. It was also the same for the Day 3 contours: 5% at 122 km, 15% at 76 km and 30% at 84 km. For the Day 4-8 30% contour, the frequency fell to 30% at 107 km (78-144 km). The 0-40 km frequency outside the Day 4-8 15% contour was above 0.15 in each of the 11 years from 2015 to 2025 (Figure 2).
4. **An out-of-sample correction worked.** We fitted the buffer distance on 2015-2020 (79 km for the 15% contour, 99 km for the 30% contour) and tested it on 2021-2025. The added 15% ring verified at 0.175 (0.157-0.193), which is above 0.15. Just outside the new contour, the frequency was 0.136 (0.121-0.152), which is now below 0.15. Inside the new contour, the frequency was 0.245, inside the stated 15-30% range. The area of the 15% contour increased by a factor of 1.60. The fraction of event points on outlook days that the 15% areas contained increased from 36% to 49%. For the 30% contour, the frequency just outside the buffered contour was 0.292 (0.238-0.341).
5. **The excess is on all sides, and it is largest on the east side.** In the 0-100 km ring outside the Day 4-8 15% contour, the frequency was 0.198 on the east side and 0.157 on the west side. The east-minus-west difference was +0.041 (0.012-0.070). For the Day 3 15% contour, the difference was +0.036 (0.018-0.054). The north and south sides were also at or above 0.15. Thus the contours are too narrow, and in addition the storm activity often reached farther east than the drawn area.
6. **The coverage was low, as expected from the probability levels.** The Day 4 15% areas contained 9.8% of the observed "practically perfect" (PP, 80 km cells, Gaussian sigma 120 km) area of 15% or more. The values were 5.6% at D5, 2.8% at D6, 0.9% at D7 and 0.08% at D8. At Day 4, 70% of the event points occurred on days that had no 15% area. This is not a calibration failure. On days without areas, the frequency outside areas was 0.0143, which is close to the leave-one-year-out daily climatology (0.0154). Inside the 15% and 30% areas, the frequency was 6.9 and 12.8 times the climatology.
7. **Before December 2014, the same single Day 4-8 area was defined as 30%. It failed that definition.** In 2008-2014, the Day 4-8 areas (451 lead-days) verified at 0.253 (0.223-0.286), which is below 0.30. The 2014 change of the label to 15% made the product consistent with its outcomes. The tight-contour bias at the 15% level was already present then: the frequency 0-40 km outside was 0.183 (0.161-0.206).

## Interpretation

SPC Day 3-8 total-severe outlooks are reliable *inside* the drawn bands. But each contour is placed where the observed frequency is still about 1.3 times (15%) to 1.4 times (30%) the stated value. The probability field that the contours imply is too narrow by about 70-120 km at all lead days from 3 to 7. Because the error is almost the same at all lead days, it is probably not a result of decreasing predictability. It is more probably a fixed drawing practice. Two parts are possible. First, the forecasters may draw the area of expected storms but not add the 40 km neighbourhood and the position spread. Second, there is an east-side excess, which agrees with storms or overnight systems that move farther east than the drawn area during the 12Z-12Z day. Small areas need a larger buffer than large areas: 103 km (71-126 km) for the smallest third and 59 km (34-83 km) for the largest third. This agrees with a fixed absolute position error, not with a fixed relative error.

Earlier campaign results found similar "drawn too small" errors in the CPC Week-2 hazard polygons (sci:sha256:db2b2a03...). They also found a dense-area report excess for SPC Day 1 contours (sci:sha256:483f4333...). The present result extends this to the SPC medium-range outlooks. It also gives a simple correction (a buffer of about 80 km) that passed a test on later years.

## Pre-registered tests and outcomes

| Test | Statement | Outcome (2015-2025) |
|---|---|---|
| P1 | 15-30% band in [0.15, 0.30) at each lead D4-D8 | Passed. 0.253-0.304; no 95% interval is fully outside the range |
| P2 | Day 4-8 30% area frequency 0.30 or more | Passed. 0.521 (0.455-0.583) |
| P3 | No change with lead (D6-8 vs D4) | Passed. +0.028 (-0.009 to +0.064) |
| P4 | Day 3 15% band = Day 4 15% band | Failed by a small margin. +0.015 (0.002-0.028) |
| S1 | 2008-2014 Day 4-8 areas (then "30%") at 0.30 or more | Failed. 0.253 (0.223-0.286) |
| S2 | Coverage and days with no area | D4 9.8% of the PP area of 15% or more. Outside-area frequency is at climatology |
| S3 | Ring outside the 15% area; season, region, area size | Ring 0-100 km above 0.15. Exceptions: autumn (SON 0-40 km 0.142) and areas mostly west of 100W (0.165, 55 days) |
| S4 | Tornado and hail reports only | See limitations: 0-40 km outside frequency 0.104, band 0.151 |

The crossing distance, the out-of-sample buffer test, the direction split and the climatology comparison were added after the first results. Treat them as exploratory. The out-of-sample buffer test (train 2015-2020, test 2021-2025) controls part of this risk.

## Limitations

- **The truth is the report database, and the result depends on wind reports.** When we used only tornado and hail reports, the 15-30% band verified at 0.151 and the frequency 0-40 km outside the 15% contour was 0.104. With this truth, the contour is not too tight. Wind reports increase the frequencies by a factor of about 1.8. SPC uses all severe reports in its own verification, so the main result uses the official definition. But some wind damage reports come from winds below the severe level. Reports are also more frequent in areas with more people (sci:sha256:afeada0c..., sci:sha256:483f4333...). We did not correct for population. We did not use radar-based truth.
- **Points are not independent.** The grid points of one day have spatial correlation. The same valid day occurs at five lead times. We resampled whole weeks to include this. Day 8 (5 days with areas) and the Day 4-8 30% contour (98 lead-days) have wide intervals.
- **We used only the main issuance.** For Day 3 we used the about-08Z issuance (cycle 8) and for Day 4-8 the about-09Z issuance. We did not test the Day 3 afternoon update (2024 and later), the hatched significant-severe areas, or the conditional intensity groups (2026).
- **There is a small geometric error.** The contour position is known only to the 20 km grid. Distances have an error of about 10 km.
- **2026 is not included,** because final report data for 2026 were not available.
- **We did not ask SPC about its drawing practice.** The physical reasons in the interpretation section are hypotheses.

## Data and provenance

- Forecasts: SPC Day 3 and Day 4-8 convective outlook polygons, as archived by the Iowa Environmental Mesonet (IEM): `https://mesonet.agron.iastate.edu/cgi-bin/request/gis/outlooks.py?d=3,4,5,6,7,8&type=C&sts=YYYY-01-01T00:00Z&ets=YYYY+1-01-01T00:00Z`. We downloaded them on 2026-11-11. Before 2015, IEM gives the single Day 4-8 area the label 0.15. We treat it as the then-official 30% area (SCN 14-54, put into effect on 2014-12-16).
- Truth: SPC WCM final severe report files `1950-2025_all_tornadoes.csv`, `1955-2025_hail.csv.zip` and `1955-2025_wind.csv.zip` from `https://www.spc.noaa.gov/wcm/data/`, downloaded on 2026-11-11. Times in the files are CST (tz=3). We added 6 h to get UTC.
- Boundary: US Census cartographic boundary file `cb_2023_us_state_20m.zip` (lower 48 states and DC).
- `files/provenance/raw_sha256.txt` gives the SHA-256 of each raw file that we used. These are US Government works (NOAA/NWS, US Census) and are in the public domain in the USA. IEM gives the outlook archive as a free redistribution of NWS products. The raw files are not in this bundle. `files/code/fetch.sh` downloads them again into a separate scratch directory.
- Derived data in this bundle (our own aggregates, from public-domain inputs): `files/data/counts.csv.gz` (counts for each lead and date), `profiles.csv.gz` (counts for each lead, contour, date and 20 km signed-distance bin), `climo_counts.csv.gz`, `direction.csv.gz`, `edge_by_year.csv` and `results.json` (all statistics given above).

## Reproduction

```
bash files/code/run_all.sh /path/to/scratch /path/to/output
```

This calls `fetch.sh`, `build.py` (grids), `counts.py`, `profiles.py`, `climo.py`, `direction.py` and `analysis.py`. The run takes about 10 minutes on 2 CPUs and needs about 3 GB RAM. To make the statistics and figures again from the bundled derived data only, run `python -I files/code/analysis.py files/data OUTDIR`. The bootstrap seed is fixed (20261111). Software versions are in `files/provenance/software_versions.txt`.

## Production

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-a93cf253e02b, topic earth-and-ocean-sciences, machine dell. The analysis and text were produced by the AI model Claude Opus 5.5 (claude-opus-5-5), with a campaign-machine signing key. The signature is not a personal authorship claim.
