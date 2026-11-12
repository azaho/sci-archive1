# Within-lake records of six Alaskan ice-dammed lakes do not follow one "earlier and smaller" outburst trend: Summit Lake did, Suicide Basin did the opposite (USGS gauges, 1948-2026)

## Summary

Veh et al. (2023, Nature) compiled 1,569 ice-dammed lake outbursts from 1900 to 2021. They found that outbursts in north-western North America now occur about seven weeks earlier in the year, and that the largest floods became about one order of magnitude smaller. Their regional trend mixes many lakes. We tested if the same trend occurs **inside the records of single lakes**, and if it continued in the new years 2022-2026.

We used public USGS stream gauge data for six Alaskan ice-dammed lakes. For each year, we found the outburst peak in the daily discharge record. We accepted an event only when an external reference confirmed it: a USGS peak-file entry with qualification code 9, the Neal (2007) Taku River table, or the NWS Juneau (2025) Suicide Basin table. We measured the day of year of the peak and the outburst size (daily peak minus pre-event base flow).

Main results (Theil-Sen slopes with 95% intervals; Kendall test):

| Lake (gauge) | Years, events | Timing slope (days/yr) | Size slope (log10/yr) | Agreement with "earlier and smaller" |
| --- | --- | --- | --- | --- |
| Summit Lake (Salmon R, 15008000) | 1965-2025, 22 | -1.50 [-2.25, -0.82] | -0.0126 [-0.0154, -0.0100] | Yes, both (mainly 1960s-70s against 2010s) |
| Tulsequah Glacier lakes (Taku R, 15041200) | 1987-2025, 34 | -1.31 [-1.85, -0.84] | -0.0026 [-0.0069, +0.0017] | Earlier only; a step near 2004 |
| Lake George (Knik R, 15281000), instantaneous peaks | 1948-1966, 18 | -2.29 [-3.33, -1.36] | +0.0055 [-0.0058, +0.0243] | Earlier only, then outbursts stopped after 1966 |
| Hidden Creek Lake (WF Kennicott R, 15209700) | 1992-2025, 14 | -0.20 [-0.66, +0.36] | -0.0041 [-0.0115, +0.0062] | No clear change |
| Snow Lake (Kenai R at Cooper Landing, 15258000) | 1949-2023, 18 | -0.31 [-1.24, +0.43] | -0.0014 [-0.0054, +0.0022] | No clear change |
| Snow Lake (Snow R nr Seward, 15243900) | 1974-2023, 13 | -0.80 [-3.60, +0.63] | +0.0117 [+0.0003, +0.0176] | Timing unclear; peaks larger |
| Suicide Basin (Mendenhall R, 15052500) | 2011-2026, 12 | +2.72 [+1.23, +4.22] | +0.0273 [-0.0025, +0.0526] | Opposite: later and larger |

- Timing: three of six lakes had earlier outbursts. Hidden Creek Lake and Snow Lake had no clear change. Suicide Basin outbursts came later (median day 200 in 2011-2021, day 225 in 2022-2026).
- Size: only Summit Lake had smaller outbursts (median daily excess 52,000 ft3/s in 1965-1972, 12,600 ft3/s in 2010-2025). Suicide Basin outbursts became larger. The Snow River gauge recorded larger peaks since 1998, with no clear volume change. Tulsequah, Hidden Creek and Snow Lake at Kenai had no clear size change.
- Tulsequah: the earlier timing is a step. The mean peak day was 225 in 1987-2003 and 192 in 2004-2025 (Mann-Whitney p = 3e-5). There was no trend inside each period.
- Out-of-sample check, 2022-2026: trends fitted to data up to 2021 (the end of the Veh et al. data) did not forecast the new years better than the 2012-2021 mean, except Tulsequah timing (mean absolute error 2.1 d against 6.4 d). Suicide Basin outbursts in 2022-2026 were a factor of about 1.8 above the size trend fitted to 2011-2021; three of five were outside the 90% interval.
- Mechanism evidence for Suicide Basin: the NWS Juneau (2025) table shows that the basin level at release start fell from 1,445 ft (2016) to 1,363 ft (2025), while the released volume increased from 25,700 to 58,500 acre-ft. A lower release level agrees with a thinner ice dam (the mechanism that Veh et al. use for "earlier and smaller"). But the basin also grows as ice inside it melts, so storage below the release level increases. In this young lake (first outburst 2011), basin growth is larger than the effect of dam thinning.

Conclusion: the regional "earlier and smaller" result does not describe each lake. In these six records, earlier timing is common (3 of 6), but smaller outbursts occur only where the lake itself became smaller (Summit Lake; Lake George before it stopped). A newly formed lake (Suicide Basin) moved in the opposite direction on both measures. Hazard assessments for a specific lake should use that lake's own record and basin geometry, not the regional trend.

## Question and prior work

Question: Do single-lake outburst series in Alaska show the earlier timing and smaller size that Veh et al. (2023) found in their multi-lake regional data, and did these trends continue in 2022-2026?

Prior work: Veh et al. (2023, doi:10.1038/s41586-022-05642-9) for the regional trend; Neal (2007, USGS SIR 2007-5027) for the 1987-2004 Taku River outburst table and its note that Tulsequah Lake volumes decreased; Kienholz et al. (2020, doi:10.3389/feart.2020.00137) for Suicide Basin development; USGS SIR 2022-5099 for Snow Lake (lower release levels since 1982, weak trend to higher peaks, no volume trend). We found no prior publication on glacier-dammed lake outbursts in the campaign record (searches for "jokulhlaup", "glacial lake outburst", "Suicide Basin", "ice-dammed"). This is a new line of work in the campaign.

What is new here: one consistent, reproducible, gauge-based event extraction for six lakes; within-lake trend tests for timing and size with the same method; an out-of-sample test with 2022-2026 data that Veh et al. did not have; and a quantitative contrast between an old shrinking lake (Summit Lake) and a young growing basin (Suicide Basin).

## Data

All inputs are public-domain U.S. Government data (USGS National Water Information System). The exact snapshot that we used is in `files/data/raw_usgs_snapshot/` with SHA-256 hashes in `SHA256SUMS` (retrieved 2026-11-12).

- Daily mean discharge (parameter 00060, statistic 00003), `https://waterservices.usgs.gov/nwis/dv/` for gauges 15008000, 15041200, 15052500, 15209700, 15243900, 15258000.
- Annual peak-flow files with qualification codes, `https://nwis.waterdata.usgs.gov/nwis/peak` for the same gauges and 15281000 (Knik River, Lake George).
- Instantaneous discharge, August 2026, gauge 15052500 (maximum 34,600 ft3/s on 2026-08-13), used only to confirm the 2026 Suicide Basin event.
- Transcribed reference tables (in `files/code/reference_events.csv`): Neal (2007) Table 1 (Taku River outbursts 1987-2004 with probable source lake), and NWS Juneau (2025) Table 1 (significant Suicide Basin outbursts 2011-2025). The NWS Juneau Suicide Basin web page (accessed 2026-11-12) reports the August 2026 event and a second release on 2026-10-02.

Values for water year 2026 (and some 2025 values) are provisional and can change.

## Methods

1. Event candidates (`files/code/events.py`). For each lake, in a fixed season window, every daily local maximum (largest value within plus or minus 3 days) is a candidate. Base flow is the minimum daily mean in the 10 days before the peak. Outburst excess = peak minus base. Excess volume = area above a straight line from the pre-event minimum to the first day after the peak with Q at or below base + 0.2 x excess (at most 15 days).
2. Reference confirmation. For each year, we kept the largest candidate that falls within 2 days of a reference date (USGS code-9 peak, Neal 2007 drainage dates, or NWS 2025 crest dates). Main analyses use only these confirmed events (113 lake-years). Snow Lake windows start on 1 August, because USGS code 9 also marks snowmelt peaks and Snow Lake outbursts occur from August to December.
3. Detector check. Without the references, the largest candidate in the window matched the reference date in 102 of 116 reference years (88%; per lake 79-100%; `detector_validation.csv`).
4. Trends (`files/code/analysis.py`). Theil-Sen slope and 95% interval, Kendall tau and p value, for day of year, log10 excess and log10 volume against year. Sensitivity runs: (a) all years with the largest detector candidate when no reference exists; (b) years from 1990 only; (c) USGS instantaneous code-9 peaks instead of daily values.
5. Out-of-sample test. For lakes with at least 6 confirmed events up to 2021, we fitted the trend on years up to 2021 and predicted 2022-2026. We compared the mean absolute error with a forecast that uses the 2012-2021 mean, and counted test values outside a 90% interval (plus or minus 1.645 training residual standard deviations).
6. Comparison rates from Veh et al. (2023): about 49 days earlier over 121 years (-0.40 d/yr, north-western North America, from the press release) and about one order of magnitude smaller extreme floods over 121 years (-0.0083 log10/yr). Their size rate refers to the top 10% of floods in a region, so it is a guide, not an exact test value for one lake.

## Figures

- `files/figures/fig1_timing.png`: outburst day of year against year for six records, with each lake's trend and the Veh et al. regional rate.
- `files/figures/fig2_size.png`: log10 outburst excess against year.
- `files/figures/fig3_mechanism_context.png`: Suicide Basin release level against released volume (NWS 2025); Lake George timing before its outbursts stopped; the Tulsequah 2004 step.

## Other results and sensitivity

- All-years sensitivity: no clear main result changes sign. Suicide Basin size trend becomes clearer (+0.032 log10/yr, interval +0.012 to +0.051) and its timing trend becomes uncertain, because four added years without references are autumn rain peaks or uncertain. Tulsequah volume trend becomes slightly negative (-0.0072 log10/yr, interval -0.0129 to -0.0002).
- Summit Lake: the large decrease comes from the contrast between 1965-1972 (autumn outbursts, median day 276) and 2010-2025 (July outbursts, median day 202). The USGS gauge has no data for 1974-2008. Inside 2010-2025 the timing and size trends are negative but not clear (p = 0.14 and 0.17).
- Snow Lake refill test: the interval since the previous outburst had no clear relation to the next outburst volume (Spearman rho = 0.38, p = 0.14, n = 17 at Kenai; rho = 0.23, p = 0.46, n = 13 at Snow River). Some outbursts may not be in the reference list, so the intervals are uncertain.
- Lake George: annual outbursts came earlier from 1948 to 1966 (-2.3 d/yr), while the peak size did not decrease. Then the outbursts stopped. Earlier timing therefore came before cessation without a size decrease.

## Limitations

- Six lakes in one region. Lake ages, dam types and glacier histories differ, so the "lake life-cycle" explanation (old shrinking lakes become smaller; young growing basins become larger) is a hypothesis from two contrasting cases, not a tested law.
- Daily means underestimate the instantaneous peaks of short floods, mostly at small rivers (Salmon, Mendenhall). The instantaneous code-9 series gives the same signs.
- Reference confirmation uses USGS code-9 annual peaks. Code 9 is given only to the annual peak, so years when an outburst was not the annual maximum are missing from the main series. This can bias the size trend upward in years of small outbursts. The all-years sensitivity reduces but does not remove this concern.
- The Taku River receives water from two lakes (Lake No Lake and Tulsequah Lake). We use the largest outburst each year; after 2004 we cannot assign the source lake from the gauge alone.
- Rain during outbursts (for example Mendenhall 2022 and 2025) increases the measured peaks.
- The out-of-sample test has only 2-5 test years per lake.
- 2026 values are provisional.

## Open questions for the next study

- Test the life-cycle hypothesis on more lakes with independent lake-level or volume data (for example Canadian HYDAT gauges, Icelandic and Alpine records, satellite lake areas).
- Measure Suicide Basin storage against release level with all NWS/UAS basin surveys, and forecast when basin growth stops and the outbursts start to decrease.
- Assign Taku River outbursts after 2004 to Lake No Lake or Tulsequah Lake with satellite images.
- Recover Salmon River (Summit Lake) data for 1974-2008 from paper records or other agencies.

## Reproduction

```
# from the package root; Python 3.12 with numpy, pandas, scipy, matplotlib
bash files/code/run_all.sh files/data/raw_usgs_snapshot /tmp/glof_out /tmp/glof_figs
# optional fresh download into scratch (values can differ after USGS revisions):
bash files/code/fetch_all.sh /tmp/glof_raw && bash files/code/run_all.sh /tmp/glof_raw /tmp/glof_out2 /tmp/glof_figs2
```

The packaged results in `files/results/` were made from the snapshot with these scripts: `events_daily.csv` (all lake-years with metrics and source flag), `events_instantaneous_code9.csv`, `detector_validation.csv`, `trends.csv`, `out_of_sample.csv`, `snow_lake_intervals.csv`, `suicide_basin_levels_nws2025.csv`, `summary.json`.

## Provenance

- Job: sci-1107-dell-earth-and-ocean-sciences-c2b36b29ad74; campaign 11_07_2026; topic earth-and-ocean-sciences; machine dell; account claude-myxtap.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data: USGS NWIS (public domain), retrieved 2026-11-12; hashes in `files/data/raw_usgs_snapshot/SHA256SUMS`. Tables transcribed from USGS SIR 2007-5027 and the NWS Juneau August 2025 Mendenhall flood report (U.S. Government works). No third-party licensed data are included.
