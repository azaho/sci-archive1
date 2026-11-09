# An automatic b-value foreshock traffic light did not identify shallow Japanese M5+ earthquakes followed by larger events in 2002-2024; most larger events came before a decision

## Summary

Gulia and Wiemer (2019, Nature) proposed a "foreshock traffic light system" (FTLS). After an M>=6 earthquake, it compares the b-value of the early aftershocks with the local background b-value. A drop of 10% or more gives a red light: a larger earthquake is probably still to come. A rise of 10% or more gives a green light: the main shock has occurred. They reported 95% success in 29 scored sequences. Later work showed that the result for one sequence depends on expert choices (Dascher-Cousineau et al. 2020).

We applied one fixed, automatic version of the FTLS to every eligible shallow (depth <= 40 km) Mj>=6 and Mj>=5 trigger earthquake in the JMA hypocentre catalogue for 2002-2024. We wrote the rule down before the first run (`files/PLAN.md`). The outcome was an equal-or-larger event within 50 km in the 30 days after the decision time.

Main results:

1. **The rule can be applied to few sequences.** Of 221 M>=6 triggers, 24 (11%) had enough background and early aftershock data. Of 910 M>=5 triggers, 43 (4.7%) had enough data. Most triggers are offshore, where the catalogue has few small events.
2. **Most larger events came too early for a warning.** 118 of the 910 M>=5 triggers (13%) had an equal-or-larger event within 50 km and 30 days. 46% of these came within 0.5 days (the blind time) and 55% within 1.5 days (the primary decision time). For M>=6 the values are 39% and 57% (Figure 1).
3. **In the real-time test, the red light had no hits.** In the primary rule, 0 of 23 (M>=6) and 0 of 38 (M>=5) scored sequences had an equal-or-larger event after the decision time. All 4 (M>=6) and 8 (M>=5) red lights were false alarms. The Gulia-Wiemer style success rate was 0.69 (M>=6) and 0.67 (M>=5). A rule that always gives green scores 1.00 on the same sequences. Summed over 46 robustness variants (the same sequences appear in many variants), only 9 of 413 red lights were followed (2.2%). No variant had a significant red-light excess (smallest one-sided Fisher p = 0.16).
4. **The retrospective test also gave no clear signal.** We let the b-value window stop just before the larger event (not possible in real time). In 16 variants with 37-122 scored sequences and 2-12 followed sequences, the AUC of -Delta b was 0.29 to 0.73. Every 95% bootstrap interval included 0.5. The best one-sided Fisher p for "red lights are followed more often" was 0.06, with no correction for 16 tests. Two simple features had point-estimate AUCs of 0.52-0.74 (magnitude gap to the largest early aftershock) and 0.62-0.72 (number of early M>=3 events). These features need no b-value.
5. **The two well-known Japanese foreshock cases are sensitive to settings.** Kumamoto 2016 (M6.5, then M7.3 after 28 h): Delta b was -50% (red) with the primary 12 h blind time, but the decision time (36 h) was after the M7.3. With a 0.5 d decision window it was orange (-4%). With a 0.1 d blind time it was red (-18%) before the M7.3. For the 2011-03-09 M7.3 Tohoku foreshock, the primary 2 d blind time for M>=7 ended after the M9.0 (2.1 d later), so no warning was possible. With a 0.1 d blind time it was red (-27%) before the M9.0.

Conclusion: in the JMA catalogue for 2002-2024, an automatic FTLS gave no measurable skill. It could not be applied to most triggers, and it could not warn before most equal-or-larger events. The number of followed sequences in the testable subset is small (0-12). Thus the test cannot exclude a moderate real effect. It does exclude the claimed high success rate for an automatic version of the rule with these settings.

## Data

- JMA hypocentre catalogue (Seismological Bulletin of Japan), annual files h1983-h2024. Source: `https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip`. We used the shared campaign copies `/mnt/dell-data/shared_datasets/jma-hypocenter-h*-20261108/` (43 zip files). `files/data/jma_input_provenance.json` gives the path, source URL and SHA-256 for each file. We checked every hash before the analysis. The analysis uses records from 1996-09-01 (prior-event check) and 1997-10-01 (b-values, start of the unified JMA catalogue) to 2024-12-31.
- We kept only 'J' (JMA-determined) records and used magnitude 1 (the preferred JMA magnitude, Mj; mostly velocity or displacement types).

## Method (primary rule)

- Triggers: Mj>=6.0 (extension: Mj>=5.0), depth <= 40 km, 2002-01-01 to 2024-11-30. No event with M >= Mtrig within 50 km in the previous 365 days.
- Source volume: epicentral distance <= L/2 + 3 km, with L = 10^(-2.44 + 0.59 M) km (Wells and Coppersmith 1994), and |depth - trigger depth| <= 20 km. Gulia and Wiemer used a 3 km box around a fault plane. We used a circle because an automatic fault-plane choice was not available for all events. Radii L + 3 km, 10 km and 20 km are robustness variants.
- Background b: source-volume events from 1997-10-01 to 30 days before the trigger. Mc = maximum curvature + 0.2. Aki-Utsu maximum likelihood with the 0.05 bin correction. At least 100 events >= Mc.
- Blind time: 0.5 d for M<7 and 2 d for M>=7 (the Ridgecrest choices of Gulia et al. 2020). Decision window: from the end of the blind time for 1 day. Mc_post = max(Mc_bg, MAXC + 0.2). At least 50 events >= Mc_post.
- Delta b = 100 (b_post - b_bg)/b_bg. Red <= -10%, green >= +10%, orange otherwise.
- Outcome: an event with M >= Mtrig within 50 km in (decision time, decision time + 30 d]. If an equal-or-larger event occurred before the decision time, we report the trigger as "too early" and do not score it.
- Robustness (real time, 23 variants each for M>=6 and M>=5): source radius; decision window 0.5 or 3 d; blind time 0.1 or 1 d; Mc correction 0.0 or 0.4; b-positive (van der Elst 2021, delta 0.2) with and without the blind time; minimum post-trigger events 30 or 100; minimum background events 50; outcome 20 or 100 km, 5 or 365 d; strictly larger; a "permissive" set (20 km, 3 d, 30/50 events) with Aki-Utsu, b-positive and 365 d.
- Retrospective test (16 variants, declared before the run in PLAN.md addendum 2): blind time 0.05 d; the b window stops at the first equal-or-larger event if it comes earlier; outcome window 30 d from the trigger.

## Results

### Real-time test, selected variants (all 46 in `files/results/grid_summary_realtime.csv`)

Columns: testable sequences; testable with an equal-or-larger event before the decision ("too early"); scored; followed after the decision; followed/total for red, orange and green; Gulia-Wiemer style success rate (correct red + correct green)/(red + green); AUC of -Delta b.

| variant | testable | too early | scored | followed | red | orange | green | GW success | AUC |
|---|---|---|---|---|---|---|---|---|---|
| m6_primary | 24 | 1 | 23 | 0 | 0/4 | 0/10 | 0/9 | 0.69 | n/a |
| m6_blind_0.1 | 37 | 0 | 37 | 3 | 2/11 | 1/19 | 0/7 | 0.50 | 0.78 |
| m6_window_0.5 | 24 | 0 | 24 | 1 | 0/4 | 1/10 | 0/10 | 0.71 | 0.65 |
| m6_bplus | 21 | 1 | 20 | 0 | 0/9 | 0/8 | 0/3 | 0.25 | n/a |
| m6_permissive | 49 | 5 | 44 | 1 | 0/11 | 1/16 | 0/17 | 0.61 | 0.40 |
| m6_permissive_365d | 49 | 5 | 44 | 5 | 1/11 | 2/16 | 2/17 | 0.57 | 0.45 |
| m5_primary | 43 | 5 | 38 | 0 | 0/8 | 0/14 | 0/16 | 0.67 | n/a |
| m5_blind_0.1 | 66 | 7 | 59 | 3 | 2/15 | 1/28 | 0/16 | 0.58 | 0.81 |
| m5_window_3.0 | 61 | 9 | 52 | 1 | 0/13 | 1/16 | 0/23 | 0.64 | 0.65 |
| m5_bplus_from0 | 60 | 8 | 52 | 1 | 0/19 | 1/26 | 0/7 | 0.27 | 0.14 |
| m5_permissive | 108 | 23 | 85 | 1 | 0/22 | 1/28 | 0/35 | 0.61 | 0.43 |
| m5_permissive_365d | 108 | 23 | 85 | 11 | 2/22 | 5/28 | 4/35 | 0.58 | 0.44 |

The b-positive variants give many more red lights (the b-positive background b is often higher than the post-trigger b-positive value). Thus the class balance depends strongly on the b estimator.

### Retrospective test (all 16 variants)

Columns: scored; followed; followed/total for red, orange and green; AUC of -Delta b (95% bootstrap interval); one-sided Fisher p for red vs not red; AUC of the magnitude gap (smaller gap = higher score); AUC of the early M>=3 count.

| variant | scored | followed | red | orange | green | AUC -Delta b | Fisher p | AUC gap | AUC count |
|---|---|---|---|---|---|---|---|---|---|
| m6_rhalf_L_w1_aki | 48 | 3 | 2/19 | 1/21 | 0/8 | 0.60 (0.28-0.84) | 0.34 | 0.69 | 0.70 |
| m6_rhalf_L_w1_plus | 39 | 3 | 2/12 | 1/23 | 0/4 | 0.64 (0.18-0.95) | 0.22 | 0.70 | 0.66 |
| m6_rhalf_L_w3_aki | 53 | 3 | 2/23 | 1/19 | 0/11 | 0.67 (0.46-0.90) | 0.40 | 0.70 | 0.72 |
| m6_rhalf_L_w3_plus | 45 | 3 | 2/18 | 1/21 | 0/6 | 0.69 (0.34-0.95) | 0.35 | 0.71 | 0.69 |
| m6_r20.0_w1_aki | 52 | 3 | 1/22 | 1/21 | 1/9 | 0.34 (0.10-0.71) | 0.82 | 0.52 | 0.63 |
| m6_r20.0_w1_plus | 37 | 2 | 1/15 | 0/19 | 1/3 | 0.36 (0.00-0.81) | 0.65 | 0.59 | 0.71 |
| m6_r20.0_w3_aki | 61 | 4 | 2/26 | 2/22 | 0/13 | 0.46 (0.25-0.69) | 0.57 | 0.57 | 0.67 |
| m6_r20.0_w3_plus | 51 | 4 | 1/18 | 1/25 | 2/8 | 0.29 (0.04-0.76) | 0.84 | 0.60 | 0.65 |
| m5_rhalf_L_w1_aki | 83 | 4 | 2/27 | 1/35 | 1/21 | 0.50 (0.07-0.82) | 0.39 | 0.70 | 0.71 |
| m5_rhalf_L_w1_plus | 66 | 4 | 3/24 | 1/31 | 0/11 | 0.73 (0.32-0.94) | 0.13 | 0.70 | 0.68 |
| m5_rhalf_L_w3_aki | 94 | 5 | 2/31 | 2/39 | 1/24 | 0.58 (0.26-0.82) | 0.54 | 0.74 | 0.66 |
| m5_rhalf_L_w3_plus | 77 | 5 | 3/31 | 2/35 | 0/11 | 0.65 (0.32-0.91) | 0.32 | 0.74 | 0.63 |
| m5_r20.0_w1_aki | 105 | 10 | 4/35 | 3/45 | 3/25 | 0.50 (0.30-0.70) | 0.44 | 0.68 | 0.62 |
| m5_r20.0_w1_plus | 76 | 7 | 5/28 | 1/37 | 1/11 | 0.63 (0.36-0.86) | 0.06 | 0.74 | 0.67 |
| m5_r20.0_w3_aki | 122 | 12 | 5/36 | 3/46 | 4/40 | 0.52 (0.33-0.70) | 0.25 | 0.66 | 0.62 |
| m5_r20.0_w3_plus | 100 | 11 | 5/35 | 4/49 | 2/16 | 0.53 (0.33-0.72) | 0.32 | 0.69 | 0.67 |

Red lights were followed somewhat more often than other classes in most retrospective variants (for example 5/36 = 14% vs 7/86 = 8% in m5_r20.0_w3_aki). The difference is small and not significant, and the AUC is near 0.5. In the retrospective mode, followed sequences have shorter windows that start earlier. This favours lower Aki-Utsu b-values because of incompleteness, so the retrospective test is biased toward the FTLS claim. It did not show a clear signal.

### Figures

- `files/results/fig1_delay_ecdf.png`: delay from the trigger to the first equal-or-larger event within 50 km (all triggers, not only testable ones).
- `files/results/fig2_db_by_outcome.png`: Delta b split by outcome for the primary real-time rule and three retrospective variants.
- `files/results/fig3_trigger_map.png`: M>=5 triggers, testability and traffic-light class, and triggers that had an equal-or-larger event.

## Limitations

- Power is low. The testable subset is small, and few testable sequences had a later equal-or-larger event (0-12 per variant). A moderate real effect is possible.
- This is not the exact Gulia-Wiemer procedure. We used circular source volumes instead of fault-plane boxes, one global background b per volume instead of a moving-window median, and fixed blind times instead of expert-chosen times. Those authors state that expert choices matter. Our purpose was to test a rule that can run without them.
- The background period (1997-2024) has completeness changes, for example more small events from 2016. One MAXC Mc for the whole period can be too low for early years. The b-positive variants reduce this effect and gave no better result.
- JMA Mj mixes velocity and displacement magnitude types. We did not convert to Mw.
- The prior-event exclusion uses a fixed 50 km radius. 67 of 910 M>=5 triggers (5 testable) are within the rupture length of an earlier larger event further than 50 km away (for example an M5.7 at 65 km from the 2024 Noto M7.6, 2 minutes later). None of these 5 testable sequences was followed, so the result does not change.
- Most triggers are offshore. There the JMA catalogue has a high completeness magnitude, so the test applies mainly to inland and near-coast sequences.
- One region (Japan) and one catalogue. The result may not transfer to California or Italy, where the original FTLS cases were found.

## Reproduction

```
bash files/code/run_all.sh /mnt/dell-data/shared_datasets ./repro
```

This runs `parse_jma.py` (catalogue to parquet, about 2 min), `timing.py` (delays), `run_grid.py` (46 real-time variants), `RETRO=1 run_grid.py` (16 retrospective variants), and `summarize.py` (tables and figures). On a loaded 24-core host, the grids took about 25 and 15 minutes with 12-16 processes. The software was Python 3.12.16, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1 and matplotlib 3.11.2. The per-trigger output for every variant is in `files/results/grid_realtime/` and `files/results/grid_retrospective/` (`variants.json` gives the settings). `files/results/delay_to_larger_event.csv` has the delays for all triggers.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-d6f74a103807, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-08. Pre-analysis plan with two dated addenda: `files/PLAN.md`.

## References

- Gulia, L., Wiemer, S. (2019). Real-time discrimination of earthquake foreshocks and aftershocks. Nature 574, 193-199. doi:10.1038/s41586-019-1606-4
- Gulia, L., Wiemer, S., Vannucci, G. (2020). Pseudoprospective evaluation of the foreshock traffic-light system in Ridgecrest and implications for aftershock hazard assessment. Seismol. Res. Lett. 91(5). Author text: https://www.earth-prints.org/handle/2122/13679
- Dascher-Cousineau, K., Lay, T., Brodsky, E. E. (2020). Two foreshock sequences post Gulia and Wiemer (2019). Seismol. Res. Lett. 91, 2843-2850. doi:10.1785/0220200082
- van der Elst, N. J. (2021). B-positive: a robust estimator of aftershock magnitude distribution in transiently incomplete catalogs. J. Geophys. Res. Solid Earth 126, e2020JB021027. doi:10.1029/2020JB021027
- Wells, D. L., Coppersmith, K. J. (1994). New empirical relationships among magnitude, rupture length, rupture width, rupture area, and surface displacement. Bull. Seismol. Soc. Am. 84, 974-1002.
- Tamaribuchi, K., Yagi, Y., Enescu, B., Hirano, S. (2018). Characteristics of foreshock activity inferred from the JMA earthquake catalog. Earth Planets Space 70, 90. doi:10.1186/s40623-018-0866-9
