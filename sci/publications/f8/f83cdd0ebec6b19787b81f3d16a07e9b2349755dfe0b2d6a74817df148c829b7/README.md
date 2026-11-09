# A seismicity-rate alarm from the public JMA catalog came before 6 of 61 Japanese eruption onsets in 1999-2024 with an uncertain gain, and about 99% of its alarms had no eruption

## Summary

We tested a simple question for eruption forecasting in Japan. Does the rate of shallow earthquakes in the public JMA
unified hypocenter catalog increase in the 30 days before eruption onsets? How often does the same increase occur without an eruption?

We used the JMA hypocenter files for 1998-2024 and the Smithsonian Global Volcanism Program (GVP) Volcanoes of the World
eruption list (WFS snapshot of 2026-11-09). We examined 89 Japanese Holocene volcanoes from 29.5 N to 46 N and 61 confirmed
eruption onsets with a known day at 16 of these volcanoes (February 1999 to September 2024).

The primary alarm rule was fixed before we computed results (files/analysis_plan.md). An alarm is on for a day when the
previous 30 days had at least 5 earthquakes at 10 km depth or less within 10 km of the volcano, and at least 3 times the count
expected from the year before.

Main results:

* The alarm was on before 6 of 61 onsets (hit rate 9.8%, 95% volcano-bootstrap interval 2.9% to 21.1%).
* At the same 16 volcanoes, the alarm was on for 3.9% of all days (2.3% to 5.7%). The probability gain was 2.5 (0.8 to 5.1). The interval includes 1, which is no skill.
* Over all 89 volcanoes, the rule made 1,407 alarm episodes. Only 11 (0.8%, 0.3% to 1.4%) had an onset at the same volcano during the episode or within 30 days after it. When we joined episodes with gaps shorter than 30 days, 11 of 1,061 episodes (1.0%) were followed by onsets. 76 of the 89 volcanoes had at least one alarm.
* A threshold-free score, log((N30+1)/(E+1)), gave a mean onset-day percentile rank of 0.59 (0.49 to 0.71) against all other days at the same volcano. A value of 0.5 is no skill.
* Low-frequency events (JMA flag 5) within 15 km gave no skill: 1 of 61 hits, gain 0.45 (0 to 1.34), rank 0.52 (0.45 to 0.58).
* For 22 of the 61 onsets, the catalog had no shallow event within 10 km in the 30 days before onset and an expected count below 1. Most of these onsets were at island volcanoes (for example Kikai, Suwanosejima and Miyakejima after 2001). The public catalog cannot see a precursor there.
* The hits were Usu (GVP name Toya) 2000, Miyakejima 2000, Akan 2006, Kirishima 2008, Kuchinoerabujima 2015 and Kirishima (Shinmoedake) 2017. Ontake 2014 (35 events against 13.3 expected, ratio 2.6) and Hakone 2015 (493 against 183, ratio 2.7) were below the 3 times limit. Aso 2016 occurred during the Kumamoto aftershock sequence and did not show an increase above that high baseline.
* Lead times were short. Four of the six hits had the alarm on for only 1, 2, 3 and 6 days before onset (Miyakejima 2000, Kirishima 2017, Usu 2000, Kuchinoerabujima 2015). Only Akan 2006 (31 days) and Kirishima 2008 (29 days) had a month of alarm before onset.

Thus the public catalog contains a weak and uncertain precursory signal. It is clearest for a few large magmatic eruptions (Usu 2000, Miyakejima 2000), where the swarm started only days before onset. It does not give
a useful stand-alone alarm in this form: it misses about 90% of onsets and nearly all alarms are false.

## Data

| Input | Source and version | Use |
| --- | --- | --- |
| JMA unified hypocenter catalog, annual files h1998-h2024 | https://www.data.jma.go.jp/eqev/data/bulletin/hypo_e.html (files at https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip), retrieved 2026-11-09 | Event time, location, depth, magnitude, subsidiary flag (1 natural earthquake, 5 low-frequency event) |
| GVP Volcanoes of the World, Holocene volcanoes | GVP WFS layer Smithsonian_VOTW_Holocene_Volcanoes, retrieved 2026-11-09 | Volcano number, name, coordinates, country |
| GVP Volcanoes of the World, Holocene eruptions | GVP WFS layer Smithsonian_VOTW_Holocene_Eruptions, retrieved 2026-11-09 | Confirmed eruption onsets, VEI |

We read the campaign shared copies in place. files/provenance_inputs.json lists the exact shared path, source URL,
byte count and SHA-256 of each of the 29 input files. All hashes agree with the shared dataset provenance records.
The raw files and record-level extracts are not in this bundle. See files/NOTICE-EXTERNAL-DATA.md.

## Methods

1. **Catalog parse** (files/code/parse_jma.py). We read every J-type record (4,932,674 events in 1998-2024). Depth
   uses the fixed-depth form when the decimal digits are blank. Negative magnitudes use the JMA encoding (-n, A, B, C).
2. **Volcanoes and onsets** (files/code/analysis.py). Volcanoes: GVP country "Japan", latitude 29.5-46, longitude 128-146 (89 volcanoes;
   Ogasawara, Mariana and Russian-administered Kuril volcanoes are outside). Onsets: GVP "Confirmed Eruption" with start
   year 1999-2024 and a known month and day. One onset in January 1999 did not have a complete 395-day history and was
   removed, which gave 61 onsets. We use 00:00 of the GVP onset date in JST catalog time and do not use the onset day.
3. **Counts.** Daily counts of flag-1 events at depth 10 km or less within 10 km (great-circle) of the GVP coordinate,
   all magnitudes. Secondary: flag-5 events at any depth within 15 km.
4. **Alarm.** For day t: N30 = count on days t-30 to t-1; E = (count on days t-395 to t-31) x 30/365. Alarm if N30 >= 5 and N30 >= 3E.
5. **Scores.** Hit rate H = fraction of onsets with alarm on at the onset day. Alarm-time fraction = fraction of valid
   volcano-days with alarm on. Valid days start at day 395 and exclude 60 days from each onset. Gain G = H divided by the
   alarm-time fraction of the volcanoes that erupted. Precision P = fraction of alarm episodes (runs of alarm days) with an onset from the episode start to 30 days after its end.
6. **Uncertainty.** Cluster bootstrap over volcanoes, 2,000 draws. Volcanoes that erupted and volcanoes that did not erupt
   are resampled separately. We give 95% percentile intervals.
7. **Sensitivity** (planned): windows 7 and 90 days, ratio 2 and 5, radius 5 and 20 km, magnitude 1.0 or more, depth 20 km or less, repose and VEI splits.
8. **Post-hoc checks** (added after we saw the primary counts; files/code/analysis2.py, analysis3.py): threshold-free rank score,
   onsets with at least 12 baseline events, merged episodes, alarm fraction against lag, and the largest magnitude in the window that started each episode.

## Results

### Primary and sensitivity rules (shallow events unless stated)

| Rule | Hits / 61 | H (95% interval) | Alarm-time fraction | Gain G (95% interval) | True / all episodes |
| --- | --- | --- | --- | --- | --- |
| Primary: 10 km, 30 d, 3x | 6 | 0.098 (0.029-0.211) | 0.039 | 2.55 (0.81-5.09) | 11 / 1407 |
| Window 7 d | 5 | 0.082 (0.020-0.150) | 0.022 | 3.68 (0.95-7.57) | 18 / 2444 |
| Window 90 d | 10 | 0.164 (0.074-0.318) | 0.059 | 2.77 (1.25-5.66) | 11 / 900 |
| Ratio 2x | 11 | 0.180 (0.077-0.326) | 0.061 | 2.96 (1.63-4.90) | 20 / 2170 |
| Ratio 5x | 4 | 0.066 (0.016-0.143) | 0.025 | 2.67 (0.62-6.72) | 6 / 799 |
| Radius 5 km | 6 | 0.098 (0.040-0.184) | 0.030 | 3.31 (1.47-6.81) | 13 / 924 |
| Radius 20 km | 6 | 0.098 (0.033-0.176) | 0.043 | 2.30 (0.73-4.44) | 11 / 1672 |
| Magnitude 1.0 or more | 5 | 0.082 (0.022-0.161) | 0.027 | 3.04 (0.88-7.22) | 8 / 862 |
| Depth 20 km or less | 5 | 0.082 (0.028-0.167) | 0.042 | 1.96 (0.71-4.03) | 10 / 1598 |
| Low-frequency events, 15 km | 1 | 0.016 (0.000-0.058) | 0.036 | 0.45 (0.00-1.34) | 6 / 939 |
| Shallow or low-frequency | 6 | 0.098 (0.030-0.209) | 0.073 | 1.35 (0.43-2.66) | 14 / 2259 |

All shallow-event rules gave point gains of 2.0 to 3.7. Three of the eight sensitivity rules had intervals above 1.
We did not correct for multiple tests, so these three intervals are not independent confirmation. In all rules, at most
1.4% of alarm episodes came before an onset.

### Splits (primary rule)

| Subset | Hits / onsets | Gain G (95% interval) |
| --- | --- | --- |
| Time since previous GVP onset at the volcano 1 year or more | 5 / 41 | 3.16 (0.70-6.62) |
| Time since previous onset less than 1 year | 1 / 20 | 1.40 (0.00-9.85) |
| VEI 2 or more | 4 / 27 | 4.72 (1.14-13.10) |
| VEI 1 or less | 2 / 34 | 1.43 (0.00-3.39) |

The repose difference is not clear (Fisher exact p = 0.65). The VEI split suggests that larger eruptions had more
precursors in the catalog, but the sample is small and the split was one of several.

### Post-hoc checks

* Threshold-free rank (fig4): shallow events, all onsets 0.59 (0.49-0.71); onsets with at least 12 baseline events 0.60 (0.39-0.73, 27 onsets); low-frequency events 0.52 (0.45-0.58).
* Alarm fraction against lag (fig2): the fraction of onsets with the alarm on rose from about 0.03-0.05 one year before
  to 0.07-0.10 in the last 30 days, and to 0.13 in the first week after onset. A similar peak (0.10) also occurred about 300 days before onset, so the pre-onset rise is near the noise level.
* False alarms are mostly small swarms: the median largest magnitude in the 30-day window that started a false episode was 1.8. Only 4.2% of false episodes had an M 4 or larger event in that window. If we remove episodes with M 3 or larger, precision rises only from 1.0% to 1.2%.

## Figures

* files/figures/fig1_onset_counts.png: observed 30-day count against expected count for each onset, with the alarm limit.
* files/figures/fig3_rule_sensitivity.png: hit rate and alarm-time fraction for each rule.
* files/figures/fig2_alarm_by_lag.png: fraction of onsets with the alarm on against days from onset.
* files/figures/fig4_rank_auc.png: threshold-free rank scores.

## Limitations

* Catalog detection. The JMA unified catalog does not contain all volcanic earthquakes that JMA volcano observatories
  record. Many island volcanoes have almost no catalog events. The test is about the public unified catalog, not about the
  full monitoring data that JMA uses for its volcanic alert levels.
* Network changes. Station additions and automatic processing (flag A events from about 2016) change detection over time.
  The 30-day against prior-year ratio reduces slow changes but does not remove steps.
* Onset dates. GVP onset dates can differ from the start of the eruptive phase, and we treat them as JST dates. Small phreatic events at frequently active volcanoes (Aso, Kikai, Suwanosejima) dominate the onset list.
* Small sample. 61 onsets at 16 volcanoes, with 10 onsets at Aso, 10 at Kikai and 10 at Miyakejima. Volcano bootstrap intervals are wide.
* Single simple rule. We did not test magnitude-dependent, b-value, migration or deformation precursors. A better rule may exist; this result is a reference for such rules.
* Precision depends on the number of volcanoes. With 89 volcanoes and few eruptions, base rates are low, so precision is low for any weak signal.

## Relation to prior campaign work

Prior campaign publications used the same JMA and GVP inputs for other questions: foreshocks near volcanoes
(sci:sha256:8fbf6ee8...), seasonality of eruption onsets (sci:sha256:17680dc4...), and eruption onsets after large earthquakes
(sci:sha256:cbe6f23c...). None of them tested a pre-eruption seismicity alarm. Our result agrees with the general observation that seismic unrest often does not lead to eruption, and that some eruptions (for example Ontake 2014) have weak precursors.

## Reproduce

Requirements: Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, pyarrow 26.0.1 (versions used).

```
# 1. Get the inputs (or use the campaign shared copies at /mnt/dell-data/shared_datasets)
bash files/code/fetch_data.sh /tmp/volc_data        # writes outside the publication
sha256sum /tmp/volc_data/*/*                         # compare with files/provenance_inputs.json
# 2. Run everything (parse about 3 min, analysis about 5-10 min on a loaded host)
bash files/code/run_all.sh /tmp/volc_data /tmp/volc_scratch /tmp/volc_out
```

The run writes the record-level onset table (onset_records.csv, onset_records_ranked.csv) and daily count arrays into the scratch
folder. These are derived from GVP records and are not part of this bundle. Random seeds are fixed (20261110 and 7).
GVP updates its live WFS layers, so a new download can change onsets. The recorded hashes identify the 2026-11-09 snapshot.

## Files

* files/analysis_plan.md: plan written before outcome counts.
* files/code/: parse_jma.py, analysis.py, analysis2.py, analysis3.py, figures.py, run_all.sh, fetch_data.sh.
* files/results/results.json: primary, secondary, sensitivity and split results with bootstrap intervals.
* files/results/posthoc_results.json, posthoc_false_alarm_mmax.json, posthoc_hit_lead_days.json: post-hoc checks.
* files/results/*_alarm_fraction_by_lag.csv, *_merged_episodes_per_year.csv, superposed_epoch_daily_sums.csv: aggregate series.
* files/provenance_inputs.json: input paths, URLs and hashes.
* files/NOTICE-EXTERNAL-DATA.md: attribution and terms for external data.

## Provenance of this work

Job sci-1107-hp-earth-and-ocean-sciences-258fa3f7bd6d, campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp,
account claude-olen. Analysis by the AI model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key, not a personal authorship claim.
