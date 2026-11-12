# SPC watch probabilities for 13,003 US watches in 2006-2025 did not increase enough with watch area and duration; hail-count and 65-kt wind errors followed rule and practice changes

## Summary

The NOAA Storm Prediction Center (SPC) issues seven probabilities with each tornado
and severe thunderstorm watch (WWP product). This study verified these probabilities
for 13,003 watches from 2006 to 2025. It used the SPC final storm report databases.
The analysis plan was written before any report was matched to a watch
(`files/PREREGISTRATION.md`, sha256 d49c2e5e742c2d15fc128fd89956d4eb40416d3150fb3742d2bd22f94411c4a2).

Main results (watch parallelogram, original valid time):

| Event | Mean forecast | Observed | O/F [95% CI] | BSS | Pre-set rule |
|---|---|---|---|---|---|
| >=2 tornadoes | 0.251 | 0.214 | 0.85 [0.82-0.88] | 0.23 | miscalibrated |
| >=1 EF2+ tornado | 0.110 | 0.086 | 0.78 [0.74-0.83] | 0.17 | miscalibrated |
| >=10 severe wind reports | 0.439 | 0.379 | 0.86 [0.84-0.89] | 0.15 | miscalibrated |
| >=1 wind >=65 kt | 0.237 | 0.323 | 1.36 [1.33-1.40] | 0.02 | miscalibrated (too low) |
| >=10 severe hail reports | 0.373 | 0.244 | 0.65 [0.63-0.67] | 0.12 | miscalibrated |
| >=1 hail >=2 in | 0.243 | 0.239 | 0.98 [0.95-1.01] | 0.21 | calibrated |
| >=6 hail+wind reports | 0.749 | 0.704 | 0.94 [0.93-0.95] | 0.12 | within 10% |

O/F = observed event count / sum of issued probabilities. BSS = Brier skill score
against leave-one-year-out climatology. CI = cluster bootstrap over convective days.

1. **Watch size and duration (the largest error).** At a fixed issued probability,
   the chance of the event increases strongly with watch area x duration for all seven
   events (pre-registered test S1: coefficient 0.44-0.81 per unit of ln(area x hours),
   all CIs above 0). The forecasts carry only 26-53% of the observed size dependence.
   For the smallest fifth of watches, O/F is 0.26-0.93 (over-forecast). For the largest
   fifth, O/F is 0.94-1.71. A recalibration with log(area x hours), fitted on 2006-2015,
   reduced the 2016-2025 Brier score by 1.5-5.1% against a plain recalibration fitted
   on the same years, for all seven events (all CIs below 0). Against the raw forecasts
   the reduction is 2.5-19% for five events; for >=2 tornadoes and EF2+ tornadoes the
   CIs include 0.
2. **Hail counting rule.** The severe hail size changed from 0.75 in to 1.00 in on
   5 January 2010. O/F for >=10 severe hail reports fell from 0.77 (2006-2009) to
   0.62 (2010-2025). The mean forecast fell only from 0.40 to 0.37. If 0.75-in reports
   are counted in all years, the 2010-2025 O/F is 0.74, near the 2006-2009 value. Thus
   the forecasts did not follow the change of the counting rule (exploratory).
3. **65-kt wind.** The under-forecast is not constant. In 2006-2012, O/F was 1.06.
   In 2013-2017 the mean issued probability fell from 0.27 to 0.16 while the observed
   frequency did not fall (O/F 2.16). In 2018-2025 the forecasts returned to 0.24 but
   O/F stayed at 1.45. Watches with a measured >=65 kt gust increased from 4-8% of
   watches in 2006-2009 to 16-18% in 2022-2025.
   With estimated reports only, the 2018-2025 O/F is 1.23 (exploratory).
4. **Watch type.** In tornado watches, P(>=2 tornadoes) is calibrated (O/F 0.97
   [0.94-1.01]). In severe thunderstorm watches it is too high (0.66 [0.62-0.71]). PDS
   watches (n = 168) are calibrated for all events within their wide CIs.
5. **Trend (pre-registered S2).** The prediction that the wind-count events (>=10 wind,
   >=6 hail+wind) show an upward O/F trend failed for >=10 wind (slope 0.02 per decade,
   CI -0.02 to 0.07) and was weak for >=6 hail+wind (0.02, CI 0.00-0.05). The tornado
   events increased (TOR2 0.77 to 0.95; EF2 0.71 to 0.87 between the two decades).

## County-based check (operational watch area)

The operational watch is a set of counties. Counties are added, and local offices
clear counties before the end time. With the IEM county-based VTEC archive (13,001 of
13,003 watches matched; county area is on average 21% larger than the polygon), each
report counts if it is in a watch county between that county's issue and expiry times
(`files/results/X5_county_summary.csv`):

| Event | O/F polygon | O/F county [95% CI] | Size coefficient county | Brier change, size model vs plain recalibration, 2016-2025 |
|---|---|---|---|---|
| >=2 tornadoes | 0.85 | 0.87 [0.84-0.89] | 0.57 | -1.4% |
| >=1 EF2+ tornado | 0.78 | 0.79 [0.75-0.84] | 0.61 | -1.6% |
| >=10 wind reports | 0.86 | 0.90 [0.88-0.92] | 0.48 | -1.6% |
| >=1 wind >=65 kt | 1.36 | 1.39 [1.36-1.43] | 0.61 | -3.1% |
| >=10 severe hail | 0.65 | 0.68 [0.65-0.70] | 0.85 | -5.0% |
| >=1 hail >=2 in | 0.98 | 1.01 [0.98-1.04] | 0.55 | -2.3% |
| >=6 hail+wind | 0.94 | 0.95 [0.94-0.96] | 0.67 | -3.3% |

All Brier changes have 95% CIs below 0. The county results agree with the polygon
results. With county areas, >=10 wind reports (O/F 0.901) is just inside the
pre-set 10% margin; the other four miscalibrated events stay outside it.

## Figures

* `files/figures/fig1_reliability.png` - reliability diagrams for the seven events.
* `files/figures/fig2_by_year.png` - O/F by year.
* `files/figures/fig3_size.png` - O/F by fifth of watch area x duration, with polygon
  +-25 km buffers and county-based areas.
* `files/figures/fig4_hail_wind_sources.png` - hail counting rule and 65-kt wind periods.

## Method

* Watches: IEM archive of SPC watches (parallelogram polygon, ISSUE, EXPIRE, seven
  probabilities, PDS flag), 2006-2025, 0 < duration <= 18 h, duplicates removed:
  13,003 watches (4,211 tornado, 8,792 severe thunderstorm).
* Reports: SPC final databases (tornado 1950-2025, hail and wind 1955-2025), CST
  converted to UTC. A tornado counts at its touchdown point and start time. Severe
  hail: >= 0.75 in before 2010-01-05 12 UTC, >= 1.00 in after. Wind: all records of
  the severe wind database; >= 65 kt uses the magnitude field (measured or estimated).
* A report counts for a watch if it is inside the polygon between ISSUE and EXPIRE.
* "<2%" is scored as 0.02 (sensitivity 0.01: EF2 O/F 0.80).
* Bootstrap: 2000 resamples of convective days (12-12 UTC).

## Sensitivity

| Variant | Effect |
|---|---|
| tornado start or end point inside | TOR2 O/F 0.86 |
| wind reports >= 50 kt only | WIND10 O/F 0.85, HW6 0.94 |
| polygon +25 km (`files/results/X4_buffer_summary.csv`) | O/F up by 0.07-0.18; size coefficient 0.35-0.76; forecast carries 29-58% of the size effect |
| polygon -25 km | O/F down by 0.13-0.25; size coefficient 0.63-1.05 |

The size result does not depend on the area definition. The overall O/F levels change
with the area: the fixed buffers move them by 0.07-0.25. The +25 km buffer is larger
than the real county extension: the county-based O/F values are only 0.01-0.04 above
the polygon values (table above). Over all area variants, >=10 severe hail (0.49-0.76),
EF2+ tornadoes (0.63-0.89) and >=1 wind >=65 kt (1.12-1.55) keep the same sign of error.

## Limitations

* Storm reports are not a complete record of events. Report density depends on
  population, spotter networks and practice; the 65-kt and hail results can contain
  reporting changes, not only forecast changes.
* The verification area of the WWP probabilities is not stated in the product. The
  polygon and the county-based area give O/F values within 0.04 of each other; fixed
  buffers of +-25 km change them more.
* Overlapping and replacement watches can share reports. Each watch is scored alone.
* The hail-criterion, 65-kt and county analyses are exploratory (after the
  pre-registration). The reason for the 2013-2017 change in 65-kt forecasts is not
  known; this study did not find an SPC statement about it.
* Watch area x duration is a property known at issue time. The size effect can also
  come from forecaster practice that makes large watches on days with widespread
  storms; the recalibration test shows that the information is usable, not why it is
  missing.
* 2026 watches were not scored (no final reports).

## Prior work

Vescio and Thompson verified experimental watch probabilities for 166 watches in
1997-1998 (SPC, https://www.spc.noaa.gov/publications/vescio/wwprobs.pdf). Dean and
others gave conditional tornado probabilities in watches (SPC publications) and a
multi-tier verification of tornado watches (25th AMS SLS). This study found no
published verification of all seven operational WWP probabilities over 2006-2025.
Related campaign result: SPC Day 1 hail outlook population dependence
(sci:sha256:afeada0c22c6a333d1e706bf55bb3375a80d377de5f95672f963e77d61230d8d).

## Reproduce

```
cd files
bash code/fetch_raw.sh /scratch/raw            # external data to scratch only
python -I code/build_counts.py /scratch/raw data/watch_counts.csv
python -I code/build_counts.py /scratch/raw /scratch/counts_p25.csv 25
python -I code/build_counts.py /scratch/raw /scratch/counts_m25.csv -25
python -I code/build_counts_county.py /scratch/raw data/watch_counts.csv data/watch_counts_county.csv
python -I code/analyze.py data/watch_counts.csv results          # pre-registered
python -I code/explore.py data/watch_counts.csv results          # exploratory X1-X3
python -I code/buffer_check.py data/watch_counts.csv /scratch/counts_p25.csv /scratch/counts_m25.csv results
python -I code/county_check.py data/watch_counts.csv data/watch_counts_county.csv results
python -I code/figures.py results figures
```

Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, geopandas 1.2.0, shapely 2.2.0,
statsmodels 0.15.0, scikit-learn 1.9.1, matplotlib 3.11.2. Runtime about 5 min per
count build, 25 min for the county build, on 1 CPU.

## Files

* `files/data/watch_counts.csv` - one row per watch: probabilities, times, area, centroid,
  report counts (polygon). `files/data/watch_counts_county.csv` - county-based counts.
* `files/results/*.csv` - all tables (primary, reliability_by_category, sensitivity,
  S1_size, S2_trend, S2_by_year, S3_type, X1-X5).
* `files/PROVENANCE.md`, `files/NOTICE.md` - sources, hashes, terms.

## Job record

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-5f5b6d034ec4, topic
earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code). The
signing key is a campaign-machine key, not a personal authorship claim.
