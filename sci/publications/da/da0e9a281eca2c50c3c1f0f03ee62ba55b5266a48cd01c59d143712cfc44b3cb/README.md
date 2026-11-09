# Among 505 earthquakes in 1995-2026, only Denali 2002 (119 kPa) changed Yellowstone geyser intervals; ten events at 16-38 kPa long-period stress gave no detectable change

Job: sci-1107-hp-earth-and-ocean-sciences-7e459825952c · Topic: earth-and-ocean-sciences ·
Machine: hp · Account: claude-myxtap · Model: Claude Opus 5.5 (claude-opus-5-5) ·
Campaign 11_07_2026 · Date: 2026-11-09. The signing key is a campaign-machine key. It is not a
personal authorship claim.

## 1. Summary

Geysers are sensitive hydrothermal systems. The 2002 M7.9 Denali earthquake changed the eruption
intervals of several Yellowstone geysers at a distance of 3,100 km (Husen et al. 2004). Hurwitz et
al. (2014) analysed Daisy and Old Faithful for 2001-2011. They concluded that a dynamic stress of
more than about 0.1 MPa is necessary, and that no geyser responded to less than 0.02 MPa. Since
2011, more large earthquakes have occurred, with stresses in the gap between these two values
(for example, Ridgecrest 2019, Stanley 2020 and Michoacan 2022). Thus we can do an
out-of-sample test of the threshold.

We tested all declustered earthquakes of 1995-2026 that could shake the geyser basins. For each
earthquake, we measured the observed long-period (0.01-0.4 Hz) peak ground velocity (PGV) at
broadband stations near Yellowstone. We converted it to a peak dynamic stress (PDS). We used 14
regular geysers from the GeyserTimes archive (128,000 Old Faithful eruptions and 83,000 Daisy
eruptions, plus 12 other geysers). We compared the 7-day median interval after each earthquake
with the 7-day median interval before it. A placebo distribution at 700 dates within +/-1 year
calibrates each change.

Results:

1. **Denali 2002 is the only clear response.** The event score has a placebo p = 0.005
   (rank-based score p = 0.021). Daisy intervals became 38% shorter (z = -11.6). Castle intervals
   became 12% longer (z = +9.2). The other seven geysers with data did not change. These signs
   agree with Husen et al. (2004).
2. **No event from 16 to 38 kPa gave a change.** The ten next-largest stresses (Michoacan 2022,
   38 kPa; Ridgecrest 2019, 33 kPa; Stanley 2020, 29 kPa; Tehuantepec 2017, 26 kPa; and six more)
   had placebo p from 0.31 to 0.93. Their mean placebo percentile was 0.37 (test p = 0.91).
3. **No dose-response.** Over 317 events with a long-period PGV of at least 0.01 mm/s, the
   Spearman correlation of -log10 p with PDS was -0.04 (p = 0.46). The correlation was also near
   zero for broadband PGV (local events) and for the Wang (2007) energy density estimate. Only 16
   of 505 events had p < 0.05, against 25 expected by chance.
4. **Local high-frequency shaking did not change the geysers.** Local earthquakes gave broadband
   PGV up to 2.9 mm/s at Old Faithful and the largest Wang energy densities, but small long-period
   stress. None gave a consistent change. An example is the 2014 M4.8 Norris earthquake (2.3 mm/s
   broadband, 8.6 kPa long-period, p = 0.036, which is within the chance count).
5. **Daisy recovery took about two months.** Daisy intervals were at 0.65 of the pre-event value
   in week 0. The band for the same weeks in 29 other years is 0.92-1.11. Daisy returned to the
   band in week 9. Castle returned in week 3. This agrees with the recovery "over subsequent
   weeks" that Husen et al. (2004) reported, and gives a number for it.

Main limitation: only one event (Denali) is above 40 kPa. Thus the data give an upper bound on the
response at 16-38 kPa (for changes larger than about 13% at Daisy, Grand and Great Fountain, and
7% at Old Faithful). They do not locate the threshold between 38 and 119 kPa.

## 2. Question and prior work

Question: Do Yellowstone geyser intervals change after earthquakes more than at placebo times?
Which shaking measure predicts a change: observed long-period PGV, observed broadband PGV, or the
Wang (2007) energy density estimate?

Prior work:

- Husen, Taylor, Smith and Healser (2004), Geology 32, 537-540, doi:10.1130/G20381.1. After Denali
  2002, eight of 22 monitored geysers changed (author name as printed in the paper). Daisy, Depression, Plume, Riverside and Pink erupted
  more frequently. Castle, Plate and Lone Pine erupted less frequently.
- Hurwitz, Sohn, Luttrell and Manga (2014), J. Geophys. Res. Solid Earth 119, 1718-1737,
  doi:10.1002/2013JB010803. They used Daisy and Old Faithful intervals for 2001-2011. Denali
  (0.14 MPa at LKWY) shortened Daisy intervals. Other global earthquakes gave at least ten times
  less stress and no response. They used PDS = v mu / beta with v measured at LKWY.
- Campaign publications on earthquake hydrology found no well-level step excess at any energy
  density (sci:sha256:f4f72761...), a stream-gauge rise excess only at high energy density
  (sci:sha256:960bb4a1...), and no faster baseflow recession (sci:sha256:7537d3ad...). Other campaign
  publications studied Old Faithful intervals and river flow (sci:sha256:715b324b...,
  sci:sha256:e11e40da..., sci:sha256:b5d05a1e...). No campaign publication tested geysers against
  earthquakes.

This study adds: 15 more years (2012-2026), 14 geysers, all declustered events with a measured
exposure, a placebo calibration per geyser, and a cross-station check of the exposure.

## 3. Data

| Data | Source and version | Use |
| --- | --- | --- |
| Geyser eruptions | GeyserTimes complete archive, shared dataset `datasets/geysertimes-eruptions-complete-20261108/geysertimes_eruptions_complete.tsv.gz` (source https://geysertimes.org/archive/complete/geysertimes_eruptions_complete.tsv.gz, downloaded 2026-11-08, 27,374,654 bytes, SHA-256 7756725b1b55317665c0aacdf21e254c476c135ab89fb5f281451a371cd7bb82) | Eruption times 1995-2026 |
| Earthquakes | USGS ComCat FDSN event service, retrieved 2026-11-09 08:26 UTC: global M >= 6.5; M >= 4.5 within 1,500 km of Old Faithful; M >= 2.5 within 100 km; 1995-01-01 to 2026-11-09 | 3,392 events (`files/data/*.csv`) |
| Waveforms | EarthScope FDSN (obspy 1.5.1): US.LKWY (broadband, 37 km from Old Faithful), WY.YFT (at Old Faithful), US.BOZ, US.AHID, US.DUG; retrieved 2026-11-09 | Peak velocities (`files/data/pgv_measurements.csv`) |

We did not store the waveforms. The bundle holds the derived peak velocities, so the geyser
analysis can run without a new download (see section 7). `files/provenance.json` gives hashes.

## 4. Methods

The plan (`files/PLAN.md`) was written before we calculated a geyser response. It has three
dated amendments and one addition. Section 6 tells which changes we made after we saw results.

**Geysers.** A clean eruption is a primary record (not a duplicate entry) with `ie = 0` (not "in
eruption"), `A = 0` (not approximate), `q = 0` (not questionable) and `min = 0` (not a minor
eruption). We merged times within 3 minutes. We selected geysers with at least 15,000 clean
eruptions since 1995 and a quartile ratio q75/q25 of intervals of 1.7 or less. This gave 14
geysers: Old Faithful, Plume, Daisy, Little Cub, Grand, Spouter, Turban, Oblong, Fountain,
Logbridge, Riverside, Great Fountain, Castle and Baby Daisy (`files/data/geyser_table.csv`).

**Interval change.** At time t0, a valid interval is 0.4 to 1.6 times the median raw interval in
t0 +/- 30 days. This removes most missed eruptions. The pre window has the intervals that end in
the 7 days before t0. The post window has the intervals that start in the 7 days after t0. Each
window needs at least 5 valid intervals. The change is
Delta = ln(median post) - ln(median pre).

**Placebo.** For each event and geyser, we calculated Delta at t0 + k days, with |k| from 15 to
365 days. We removed placebo dates within 14 days of an "exposed" event (pgv_lp or pgv_bb of at
least 0.1 mm/s, or log10 e >= -4). Then z = (Delta - placebo median) / (1.4826 x placebo MAD).

**Event scores.** S = root mean square of z over the geysers with data (primary). M = max |z|.
F = mean of -ln(1 - u), with u the placebo percentile of |z| (rank-based; robust to Riverside's
heavy tails). We compared the event with each placebo date on the geysers that both have (at
least 3). The p-value is (1 + number of placebo dates with a score at least as large) / (1 +
number of placebo dates).

**Exposure.** We removed the instrument response and band-passed the horizontal components:
0.01-0.4 Hz (long period) and 0.05-15 Hz (broadband, LKWY) or 0.5-20 Hz (YFT). The peak is the
largest absolute horizontal value. For events beyond 300 km with a value of at least 0.3 mm/s, we
also measured BOZ, AHID and DUG, and we used the median of the stations. For events within 300 km,
pgv_lp is the YFT value at the geyser basin (else LKWY), and pgv_bb is the YFT value (else LKWY).
PDS = pgv_lp x mu / beta, with mu = 33 GPa and beta = 3.5 km/s (Hurwitz et al. 2014). The Wang
(2007) estimate is log10 e = (0.48 M - 1.4 - log10 r) / 0.33, with r the hypocentral distance in km.

**Declustering.** We kept an event only if no event with a larger max(pgv_lp, pgv_bb) occurred
within 7 days. This gave 567 events, and 505 had a score.

**Tests.** P1: mean placebo percentile of the 10 events with the largest pgv_lp, against a
uniform null (20,000 simulations on each event's placebo grid). P2: Spearman correlation of
-log10 p with log10 pgv_lp, log10 pgv_bb and log10 e. Sensitivity runs: 2-day and 30-day windows,
and a run without Old Faithful. Recovery: weekly median ratio after 3 November 22:12 UTC in 2002,
compared with the same calendar window in other years.

## 5. Results

### 5.1 Observed long-period stress does not follow the energy density estimate

![Observed long-period stress against the Wang energy-density estimate](files/figures/fig1_exposure.png)

Denali gave 119 kPa (four stations: LKWY 10.6, BOZ 14.7, AHID 6.9, DUG 16.9 mm/s). Hurwitz et
al. (2014) reported 140 kPa from the LKWY peak vector velocity. Our LKWY value for Tohoku 2011
(11 kPa) agrees with their 10 kPa. Only Denali is above 40 kPa in 1995-2026. Six events are at
20-40 kPa and 13 events are at 10-20 kPa. The Wang estimate ranks local events very differently.
For example, the 2014 M4.8 Norris earthquake has the largest e (10^-2.0 J/m3), but only 8.6 kPa of
long-period stress. The Spearman correlation of log e with log pgv_lp is 0.67 for distant events
and 0.59 for local events.

### 5.2 Only Denali changed the geysers

![Placebo -log10 p against long-period stress and local broadband PGV](files/figures/fig2_dose_response.png)

| Event | PDS (kPa) | Geysers | p (RMS) | p (rank) |
| --- | --- | --- | --- | --- |
| Denali 2002, M7.9 | 119.2 | 9 | 0.005 | 0.021 |
| Michoacan 2022, M7.6 | 38.4 | 9 | 0.42 | 0.41 |
| Ridgecrest 2019, M7.1 | 32.8 | 7 | 0.57 | 0.83 |
| Stanley 2020, M6.5 | 28.9 | 4 | 0.65 | 0.85 |
| Tehuantepec 2017, M8.2 | 26.3 | 9 | 0.93 | 0.95 |
| Ometepec 2012, M7.4 | 22.5 | 8 | 0.42 | 0.40 |
| El Mayor-Cucapah 2010, M7.2 | 19.7 | 9 | 0.51 | 0.47 |
| Mendocino 2024, M7.0 | 18.4 | 3 | 0.31 | 0.31 |
| Tecoman 2003, M7.6 | 17.1 | 9 | 0.71 | 0.52 |
| Gorda 2005, M7.2 | 16.5 | 8 | 0.84 | 0.89 |
| Sumatra 2004, M9.1 | 16.1 | 8 | 0.92 | 0.92 |

P1 (top 10, with Denali): mean percentile 0.47, p = 0.64. P1 without Denali (next 10 events,
16-38 kPa): mean percentile 0.37, p = 0.91. P2: rho = -0.04 (p = 0.46) for pgv_lp, rho = -0.05
without Denali, rho = -0.10 (p = 0.60, n = 31) for pgv_bb, and rho = 0.04 (p = 0.49) for log10 e.

Counts of p < 0.05 by PDS bin: 10/327 (below 1 kPa), 3/93 (1-3 kPa), 2/44 (3-10 kPa), 0/16
(10-30 kPa), 0/2 (30-100 kPa), 1/1 (above 100 kPa).

| Window | Events scored | p < 0.05 (RMS / max / rank) | Expected | Denali p (RMS / rank) | P1 p without Denali |
| --- | --- | --- | --- | --- | --- |
| 7 days (primary) | 505 | 16 / 11 / 23 | 25.2 | 0.005 / 0.021 | 0.91 |
| 2 days | 410 | 10 / 11 / 12 | 20.5 | 0.019 / 0.051 | 0.86 |
| 30 days | 535 | 26 / 26 / 49 | 26.8 | 0.060 / 0.010 | 0.39 |
| 7 days, no Old Faithful | 467 | 16 / 12 / 18 | 23.4 | 0.005 / 0.047 | 0.91 |

The rank score with 30-day windows gave more small p-values than expected (49 against 27). Thus
its placebo calibration is not exact for long windows. We do not use it for a claim.

### 5.3 Per-geyser changes

![Per-geyser z for the 12 largest long-period stresses](files/figures/fig4_geyser_z.png)

At Denali, Daisy (z = -11.6, per-geyser p = 0.003) and Castle (z = +9.2, p = 0.003) changed. Old
Faithful (+2.2%, z = 1.4), Grand, Plume, Oblong, Spouter, Fountain and Great Fountain did not. At the
other events, the largest |z| values were Little Cub (+5.1, Michoacan 2022) and Castle (+3.9,
Ridgecrest 2019). Values of this size are common at placebo dates for these geysers.

Large single-geyser values also occur after weak shaking. Daisy had z = +14.5 after the 1998 M7.1
Antofagasta earthquake (0.17 kPa) and z = -10.2 after the 2011 M7.1 Miyagi aftershock (0.4 kPa).
Thus one large single-geyser z is not sufficient evidence of a seismic response. Denali is
different for three reasons: it has the largest exposure, it is the planned positive control,
and two geysers changed in the directions that Husen et al. (2004) reported.

Detection limits (95th percentile of |Delta| over all scored events, 7-day windows): Old Faithful
6.9%, Turban 10.5%, Great Fountain 12.3%, Daisy 12.9%, Grand 14.6%, Castle 16.6%, Spouter 17.5%,
Plume 18.3%, Fountain 31%, Oblong 42%, Little Cub 43%, Riverside 83%
(`files/results/detection_limits_w7.csv`). Denali's Daisy change (38%) is three times the Daisy limit.

### 5.4 Recovery after Denali

![Daisy and Castle weekly intervals after 3 November in 2002 and in other years](files/figures/fig5_denali_recovery.png)

![Daily intervals for four geysers around the three largest stresses](files/figures/fig3_timecourse.png)

| Geyser | Week 0 ratio, 2002 | Weeks 0-3 mean, 2002 | Other-year 5-95% band, weeks 0-3 | Back in band | Weeks outside band (0-29) |
| --- | --- | --- | --- | --- | --- |
| Daisy | 0.65 | 0.73 | 0.92-1.11 | week 9 | 10 of 30 |
| Castle | 1.13 | 1.08 | 0.96-1.04 | week 3 | 8 of 30 |
| Grand | 0.98 | 0.97 | 0.90-1.09 | week 0 | 3 of 30 |
| Old Faithful | 1.02 | 1.01 | 0.96-1.02 | week 1 | 1 of 30 |

Daisy shortened at once and then recovered at a steady rate over about 9 weeks. Husen et al.
(2004) wrote that Daisy recovered "over subsequent weeks", and that Castle had "short-term
irregularities ... lasting for a few days". Our weekly medians put the Daisy recovery at 9 weeks
against the seasonal band of other years. They show a Castle change for about 3 weeks. After
week 3, Castle intervals stayed 3-5% above the other-year median for most of the 30 weeks. This
persistent part is small and we do not claim it.

## 6. Changes to the plan and their effect

1. Exposure QC (amendments 1 and 2). The first single-station values had errors (South Sandwich
   2021 at LKWY was 55 times the YFT value; El Salvador 2023 gave 2,485 kPa from YFT). We changed
   to a median of up to five stations before we calculated the full set of geyser responses.
2. Placebo comparison (amendment 3). The planned rule needed all event geysers at each placebo
   date. Seasonal coverage made it fail (Denali had 43 valid dates; Michoacan 2022 had 0). We had
   seen the per-geyser z values of the top six events (Denali: Daisy -11.6, Castle +9.2) and the
   Denali p (0.0066) from a partial test run before this change. The new rule compares on the shared
   geysers.
3. Rank score (addition). We added F after we saw that Riverside dominates RMS and max |z|. It
   is a robustness check. All conclusions are the same with RMS, max |z| and F at 7 days.

## 7. Reproduce

Python 3.12 with numpy, pandas, scipy, matplotlib and pyarrow, plus obspy 1.5.1 and decorator
(only for waveform steps). The code expects this layout: `work/code/` (the files in
`files/code/`), `work/scratch/`, `work/results/`, `work/figures/`, and the shared dataset link
at `work/../datasets/`. On this host, IPv6 routes hang. `code/ipv4.py` forces IPv4 for the
waveform client.

```bash
# 1. Earthquake catalog (or copy files/data/*.csv into work/scratch/)
#    see files/provenance.json for the exact ComCat queries
python code/catalog.py                     # -> scratch/events_all.csv
# 2a. Exposure from waveforms (about 1.5 h at 12 processes):
python code/pgv.py -6                      # LKWY and YFT, cached per event
python code/pgv_verify.py                  # BOZ, AHID, DUG for large distant events
# 2b. Or reuse the derived values in this bundle:
python code/unpack_pgv.py files/data/pgv_measurements.csv
# 3. Geyser responses and tests
python code/geysers.py                     # clean eruptions, geyser selection
python code/respond.py 7 w7
python code/respond.py 2 w2
python code/respond.py 30 w30
python code/respond.py 7 w7_noOF "Old Faithful"
python code/tests.py                       # -> results/tests.json
python code/timecourse.py ak002e435qpj,us7000i9bw,ci38457511
python code/recovery.py
python code/figures.py
```

`code/pgv_reverse.py` is a helper that we used to run `pgv.measure` in reverse time order in
parallel. It writes to the same cache.

Outputs in this bundle: `files/results/event_scores_*.csv` (one row per declustered event with
exposure and scores), `files/results/geyser_z_*.csv` (per-geyser Delta, z and p),
`files/results/tests.json` (P1, P2, bins, lists), `files/results/denali_recovery_*`,
`files/results/timecourse.csv`, `files/results/denali_placebo_w7.npz` (Denali event and placebo
matrices).

## 8. Limitations

- One event above 40 kPa. The study cannot locate the threshold between 38 and 119 kPa. It also
  cannot tell if the Denali response came from the stress amplitude or from the long duration and
  directivity of the Denali surface waves.
- Observation coverage changes with season and year. Winter events have fewer geysers (Stanley
  2020, 4 geysers; Mendocino 2024, 3). Geysers that responded to Denali (Plate, Depression, Pink,
  Lone Pine) are not in the set, because they fail the regularity or count rule.
- The interval filter (0.4-1.6 times the local median) removes missed eruptions. It also removes
  real changes larger than 60%, and it can hide a change in the eruption mode.
- PDS uses one shear modulus and wave speed, horizontal peaks, and stations 37-200 km from the
  basins. Site effects at the geyser basins can differ.
- Weather affects Daisy (Hurwitz et al. 2014). We did not add weather covariates. The placebo
  dates include all seasons, so the calibration is a mean over seasons.
- The p-values of single events are not corrected for 505 tests. Denali's status depends on it
  being the planned positive control with the largest exposure.

## 9. References

- Husen, S., Taylor, R., Smith, R. B., Healser, H. (2004). Changes in geyser eruption behavior and
  remotely triggered seismicity in Yellowstone National Park produced by the 2002 M 7.9 Denali
  fault earthquake, Alaska. Geology 32, 537-540. doi:10.1130/G20381.1
- Hurwitz, S., Sohn, R. A., Luttrell, K., Manga, M. (2014). Triggering and modulation of geyser
  eruptions in Yellowstone National Park by earthquakes, earth tides, and weather. J. Geophys.
  Res. Solid Earth 119, 1718-1737. doi:10.1002/2013JB010803
- Wang, C.-Y. (2007). Liquefaction beyond the near field. Seismol. Res. Lett. 78, 512-517.
  doi:10.1785/gssrl.78.5.512
- Hill, D. P., et al. (1993). Seismicity remotely triggered by the magnitude 7.3 Landers,
  California, earthquake. Science 260, 1617-1623.
- GeyserTimes archive: https://geysertimes.org/archive/
- USGS ComCat: https://earthquake.usgs.gov/fdsnws/event/1/
- EarthScope FDSN web services: https://service.earthscope.org/
