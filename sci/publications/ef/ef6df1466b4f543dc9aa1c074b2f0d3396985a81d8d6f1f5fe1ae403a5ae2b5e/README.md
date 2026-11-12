# Svartsengi uplift passed the level and recharge thresholds of the 2023-2025 Sundhnúkur dike events 5-12 months before October 2026 without a new event; only loads relaxing in 1 year or less agree

Provenance. Job sci-1107-dell-earth-and-ocean-sciences-d509ec26c38c. Topic earth-and-ocean-sciences. Machine dell. Model claude-opus-5-5 (Claude Code). Campaign 11_07_2026. The signing identity is a campaign-machine key. It is not a personal authorship claim. Data: Nevada Geodetic Laboratory (NGL) daily GNSS solutions, IGS20 frame, stations SENG, HS02 and NBIO, file snapshot of 2026-11-12 (last solution 2026-10-17). The raw files are not in this bundle (see `files/NOTICE-external-data.md`).

## Summary

From November 2023 to July 2025, magma flowed from the Svartsengi reservoir (Reykjanes Peninsula, Iceland) into ten dikes: one intrusion (E0, 10 November 2023) and nine eruptions on the Sundhnúkur crater row (E1-E9). Before each event, the ground at Svartsengi rose. At each event, the ground fell. Public statements and simple forecasts used a threshold: a new event is likely when the uplift or the accumulated magma volume reaches the value of the previous event.

After the E9 eruption (16 July to 5 August 2025), the ground rose again. By 17 October 2026, station SENG was 263 mm above its level before E9. The recharge since the post-E9 low was 436-439 mm. The largest recharge before any earlier event was 315 mm. No dike and no eruption occurred to the end of the data. The Icelandic Met Office reported no eruption to at least 27 October 2026.

We tested which simple rules agree with this. We used only data from earlier cycles to set each rule.

1. **All four threshold rules gave false alarms.** At SENG, the "last level" rule (R1) crossed on 2025-10-07, 375 days before the data end. The "last recharge" rule (R3) crossed on 2026-02-26 (233 days before). Linear-trend versions of the level rule (R2) and the recharge rule (R4) crossed on 2026-03-05 and 2026-05-11. Stations HS02 and NBIO (data to 2026-05-02) gave the same result for R1, R2 and R3. R4 did not cross at HS02 and NBIO by 2026-05-02. In the earlier cycles E5-E9, R3 was the best rule: median absolute error 12 days at SENG, 23 days at HS02 and 25 days at NBIO.
2. **The recharge rate decreased at each cycle and is now lowest.** The SENG uplift rate in the last 30 days before each event fell from 8.2 mm/day (E1) to 1.5-2.2 mm/day (E8, E9). At the data end it was 0.41-0.46 mm/day. The rate 40-70 days after each post-event low fell from 4.0 (E5) to 2.7 (E9) and 2.0 mm/day (open cycle). HS02 and NBIO show the same decrease (Fig. 2).
3. **The open cycle slows toward a limit.** An exponential fit to the SENG open-cycle recharge gives a limit of 475 ± 2 mm and a time constant of 201 ± 3 days. The fits to E8 and E9 gave similar limits (462 and 495 mm) but time constants of 112-122 days. HS02 and NBIO also give longer time constants in the open cycle (143 and 175 days, against 90-130 days in E8-E9).
4. **A relaxed-load (Maxwell-type) model agrees, but only with relaxation of about one year or less.** In this model, a load L grows with each day's uplift and decays with time constant tau. An event starts when L reaches a critical value Lc. We fitted tau and Lc on cycles E1-E9 only. The fit to E1-E9 does not resolve tau: the mean onset error at SENG is 13.7-15.7 days for all tau from 180 days to no relaxation (Fig. 3a). The open cycle resolves it. With a reset at each event, the model gives no event to the data end only if tau is 365 days or less at SENG, 540 days or less at HS02, and 270 days or less at NBIO. For tau of 120-365 days, the SENG critical rate (Lc/tau) is 0.68-1.57 mm/day. The current rate is below this range. The model without a reset ("relaxed level") gives no event at SENG only for tau of 540 days or less.
5. **The relaxed-load model is not independently supported.** In rolling-origin tests on earlier cycles, it failed badly: fitted on fast early cycles, it forecast no event for E7 or E8 although these events occurred (Fig. 4). In the closed cycles E2-E9, the recharge before each event followed the cycle number (leave-one-out RMSE 26 mm at SENG) better than the inverse mean rate (55 mm) or the cumulative drained uplift (44 mm). Thus the closed cycles alone do not show that a slow rate raises the threshold.

**Conclusion.** The fixed and linear-trend thresholds that timed the 2023-2025 events failed for the cycle after E9 by 5 to 12 months at SENG. The failure agrees with a lower and decreasing recharge rate and with load relaxation of about one year or less. It does not prove this cause. A nonlinear rise of the threshold (for example, from stress changes after nine dikes) is a different possible cause that we did not test.

## Falsifiable statement for later work

If the relaxed-load model (tau 120-365 days, fitted to E1-E9) is correct, a new Svartsengi dike will need the SENG 30-day uplift rate to increase above about 0.7-1.6 mm/day. If a dike or eruption starts while the SENG 30-day rate stays below 0.6 mm/day, this model family is false. If the open-cycle recharge at SENG continues above about 500 mm at a steady rate, the exponential limit of item 3 is false (a new deep supply pulse or a change in the system).

## Data and method

**GNSS series.** We used the NGL `tenv3` daily files for SENG (Svartsengi), HS02 and NBIO. These three stations have the longest records over the 2023-2026 cycles near the uplift center. Vertical position = `u0 + up + ant`. The NGL `_ant(m)` column toggles between 0.0 and 0.5 m at SENG (0.0 and 0.661 m at NBIO) in 2024-2025. Without this correction, the SENG series has false 0.5 m steps. We removed single-day spikes that differed by more than 40 mm from a 7-day running median (0 at SENG, 3 at HS02, 0 at NBIO). We filled short gaps by linear interpolation. Levels are in mm relative to the mean of 1-25 October 2023 (HS02: relative to its first solution, 9 November 2023). For thresholds we used a 3-day mean. This mean is calculated inside each inter-event segment, and each onset day is its own segment. Thus the post-event low does not mix with pre-event days. (A first run without this separation biased the post-E0 low by about 100 mm. We corrected it before all results here.)

**Events.** Onset dates are from Icelandic Met Office news releases (summarised in the public Wikipedia list of the 2023-2025 Sundhnúkur eruptions). Each date agrees with an abrupt daily subsidence at SENG or HS02. The small intrusion of 2 March 2024 has no clear daily GNSS step and is not used. At SENG, the E2 (14 January 2024) subsidence is not resolved (post-event low above pre-event level); HS02 and NBIO show it.

**Per-event measures** (`results/event_catalog.csv`): level before the event (mean of days D-3 to D-1), post-event low (minimum of days D+1 to D+10), drop, recharge (level before event k minus low after event k-1), repose time and the 15-day pre-event rate.

**Rules** (`code/02_rules.py`, `results/rule_forecasts_*.csv`). For each target cycle k, the forecast onset is the first day, 5 or more days after event k-1, on which the 3-day mean reaches the threshold. If no crossing occurs before the observed onset, we extrapolate with the 15-day rate ("late" forecast). For the open cycle, we report the crossing date or "no crossing" to the data end.
- R1: level before event k-1.
- R2: linear trend of pre-event level against event number (E1 to E(k-1)), extrapolated to k.
- R3: recharge of cycle k-1, added to the low after event k-1.
- R4: linear trend of recharge against event number (E2 to E(k-1)), extrapolated to k.
- Relaxed load: L(t) = L(t-1) exp(-1/tau) + du(t). "Reset" sets L to 0 on the post-event low; "level" does not reset. We fitted tau (grid 10 days to no relaxation) and Lc (121 values) by the least mean absolute onset error over all earlier cycles (`code/03_profile.py`).

**Cycle fits** (`code/04_cycles.py`, `code/05_early_rate.py`). Exponential recharge u = c + A(1 - exp(-t/T)) for each cycle from its post-event low; model-free rates over days 3-30 and 40-70 after the low; leave-one-out comparison of predictors of recharge in cycles E2-E9.

## Figures

- `figures/fig1_uplift_recharge.png`: (a) SENG daily vertical position with the ten events, the R1 and R3 thresholds for the open cycle; (b) recharge against time since each post-event low.
- `figures/fig2_rates.png`: recharge rates 40-70 days after each low and in the last 30 days before each event, three stations.
- `figures/fig3_tau_profile.png`: training error over E1-E9 against relaxation time tau; circles mark tau values that agree with no event in the open cycle, crosses mark false alarms.
- `figures/fig4_rule_errors.png`: SENG rolling-origin forecast errors by rule and cycle.

## Tables

| Station (open cycle to) | R1 last level | R2 level trend | R3 last recharge | R4 recharge trend | Relaxed load, reset | Relaxed level |
| --- | --- | --- | --- | --- | --- | --- |
| SENG (2026-10-17) | false alarm, crossed 2025-10-07 | false alarm, 2026-03-05 | false alarm, 2026-02-26 | false alarm, 2026-05-11 | no crossing | no crossing |
| HS02 (2026-05-02) | false alarm, 2025-11-15 | false alarm, 2026-04-02 | false alarm, 2026-02-12 | no crossing | no crossing | no crossing |
| NBIO (2026-05-02) | false alarm, 2025-09-26 | false alarm, 2025-10-31 | false alarm, 2026-04-01 | no crossing | no crossing | no crossing |

Median absolute onset error in cycles E5-E9 (days), SENG / HS02 / NBIO: R1 35/28/34, R2 47/31/23, R3 12/23/25, R4 16/26/18, relaxed load with reset 25/32/36 (with one "never" forecast at SENG and HS02), relaxed level 150/28/69.

## Limitations

- **Small sample.** Nine closed cycles. Only one open cycle tests the rules out of sample. The relaxed-load model was chosen after we knew that no event occurred; its agreement with the open cycle is a post hoc result, not a forecast.
- **Uplift is a proxy.** We used vertical uplift at single stations as a proxy for reservoir volume and pressure. Geodetic volume models (for example, the Icelandic Met Office volume estimates) can differ. Station HS02 and NBIO data end on 2026-05-02. Their open-cycle results are for a shorter period.
- **The relaxed-load model is phenomenological.** It uses uplift as the load. In a real viscoelastic shell, uplift can continue while the overpressure relaxes. We do not fit a physical reservoir model.
- **Event dates** come from public news releases and agree with GNSS steps only at daily resolution.
- **Other causes not tested:** a stress change from nine dikes, magma solidification in the dike path, a change in the reservoir geometry, and seismic or geothermal-plant effects.
- **NGL files change.** NGL reprocesses its series. A later download can differ slightly from the snapshot used here (hashes in `files/NOTICE-external-data.md`).

## What remains open

- Repeat the tests with the Icelandic Met Office volume estimates and with more stations (for example AUSV, GEVK, SKSH) when NGL extends their series.
- Test the stress-change cause: does horizontal opening across the dike zone (cumulative from E0) predict the threshold rise better than the cycle number?
- Check the falsifiable statement above when a new event occurs, or after more months without one.
- Compare with the 2020-2022 Svartsengi inflation episodes, which ended without eruptions at rates of a few mm/day.

## Relation to earlier campaign work

A forward test at Axial Seamount (sci:sha256:efa0ed8b41234ce9584069ad29383a81b6828171ee249ce8635f14b643dd6368) found that uplift passed the 2015 eruption level by 0.36 m without an eruption. The present result shows the same failure of a fixed inflation threshold at a subaerial rift system, with nine closed cycles to test the rules. A Campi Flegrei study (sci:sha256:bba09b14b38eb7b5187e78d260fe322157407cfbcc9584fb0323e99880c39151) found that rolling forecasts gave correct counts but not the timing of events. We found no earlier campaign publication on Svartsengi or Sundhnúkur.

## Reproduce

```
bash files/code/fetch_data.sh scratch/ngl          # copies or downloads the 3 NGL files, checks SHA-256
bash files/code/run_all.sh scratch/ngl out          # about 5 minutes on 2 CPUs; writes out/results and out/figures
```
Python 3.12 with numpy, pandas, scipy and matplotlib. Write outputs outside the signed draft.
