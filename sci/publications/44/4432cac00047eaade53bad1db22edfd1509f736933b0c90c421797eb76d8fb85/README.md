# Svartsengi magma recharge, Iceland, 2023-2026: the trigger rules that timed ten earlier events best predicted an event by early 2026 that did not occur, while steady recharge continued

Job: `sci-1107-hp-earth-and-ocean-sciences-2a9c4e1df4df` · topic: earth-and-ocean-sciences · machine: hp · model: Claude Opus 5.5 (`claude-opus-5-5`) · campaign 11_07_2026 · analysis date 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

From November 2023 to July 2025, magma from the Svartsengi reservoir (Reykjanes Peninsula, Iceland) went into dikes along the Sundhnúkur crater row ten times: two intrusions without an eruption (2023-11-10, 2024-03-02) and nine eruptions (last onset 2025-07-16, end 2025-08-05).
After each event, the ground above Svartsengi subsided and then rose again.
After the July 2025 eruption, the ground continued to rise for more than 15 months, but no new intrusion or eruption occurred to the end of our data (2026-10-17).
The Icelandic Meteorological Office (IMO) estimated 29.1 million m3 of new magma by 2026-08-18, more than before any earlier event (17-23 million m3).

We asked:

1. Does the GNSS uplift confirm that the current re-inflation is larger than before every earlier event, at more than one station?
2. Which simple trigger rule times the ten earlier onsets, and does that rule permit the current long pause ("stall")?
3. Is the current recharge an exponential approach to a stable level (a two-reservoir model with fixed deep pressure), or does a steady supply continue?

We found no prior campaign publication on Svartsengi or the Sundhnúkur events (searches on 2026-11-12: "Svartsengi uplift", "Sundhnukur eruption", "Grindavik", "Reykjanes peninsula", "Iceland", "magma recharge inflation GNSS").

## Data

* Daily GNSS positions from the Nevada Geodetic Laboratory (NGL), IGS20 frame, `tenv3` files (Blewitt et al. 2018), retrieved 2026-11-12 from `https://geodesy.unr.edu/gps_timeseries/IGS20/tenv3/IGS20/<STA>.tenv3`.
  Seventeen stations were retrieved; the analysis uses SENG (Svartsengi, data to 2026-10-17), HS02 (to 2026-05-02), GEVK (Grindavík, to 2026-10-17) and AUSV (to 2026-10-17).
  The raw files are not in this bundle. On the campaign host they are in `/mnt/dell-data/shared_datasets/ngl-igs20-tenv3-<sta>-20261112/` (one dataset per station, with provenance). SHA-256 hashes are in `files/SHA256SUMS_raw.txt`. `files/code/fetch_data.sh` downloads them again to a scratch folder. NGL updates these files, so later downloads can differ.
* Event onset dates: the published IMO chronology, as summarised in the Wikipedia article "2023-2025 Sundhnúkur eruptions" (read 2026-11-12). Status to October 2026: IMO news releases as reported in the cited web pages. We used the onset dates only; all levels, re-inflations and rates come from the GNSS data.

### GNSS corrections

* SENG: from December 2023 to August 2025 the NGL daily heights toggle between two levels 50.7 cm apart (336 of 3,308 days). The toggles do not occur in the SENG horizontal components or at HS02, so they are an antenna-height or processing artefact. `seng_fixed()` in `files/code/load.py` removes them. After the correction, SENG = 1.10 x HS02 + constant (residual SD 2.8 cm, which is mainly the different subsidence at the two sites during events).
* Single-day outliers (more than 3 robust SD and at least 1 cm from a 7-day running median, not part of a step) were removed, except in a window from 2 days before to 10 days after each onset (11-14 days per station).
* We did not subtract a reference station. The far station REYK (Reykjavík) rose by less than 1 cm per year, which is small relative to the 25-45 cm signals.

## Method

For each event k: level on the last day before onset (U_trig), post-event floor (minimum within 12 days after onset, U_start), and re-inflation before the next event (dU = U_trig(k+1) - U_start(k)).

Trigger rules, each tested by leave-one-out on the ten events from December 2023 to July 2025 (each event predicted from the other nine, with the observed uplift path):

* H0, fixed re-inflation: an event occurs when dU reaches a constant (IMO uses a similar volume rule).
* H1a, level rises per event: an event occurs when the absolute level reaches a + b·k.
* H1b, level rises with time: threshold a + b·t.
* H1c, re-inflation threshold grows with the floor (for example, a reservoir that becomes larger).
* H3, fading-memory stress (a Maxwell-like relaxation of the host rock): sigma(t) = sum of past daily height changes, each multiplied by exp(-age / tau_r), with tau_r from 7 to 365 days; an event occurs when sigma reaches a constant.

Timing error: the difference between the first threshold crossing and the true onset; if the threshold was not reached before onset, the remaining gap divided by the 14-day slope (maximum 365 days).
Stall test: the maximum value of the rule's variable in the current cycle, minus the threshold fitted on all ten events, divided by the SD of the onset values (z > 0 means that the rule predicted an event that did not occur).

Current-cycle shape: fits of U = Ua - A·exp(-t/tau) and U = Ua - A·exp(-t/tau) + q·t, compared by AIC. Uncertainty: moving-block bootstrap (30-day blocks, 300 replicates) of the residuals, both from the exponential-only fit (null distribution) and from the exponential+linear fit (confidence interval).

## Results

### 1. The current re-inflation is the largest of the series (Figures 1 and 2)

| Station | dU before the 5 eruptions May 2024 - Jul 2025 (cm) | dU now (cm) | date dU passed the earlier maximum |
|---|---|---|---|
| SENG | 24.8, 29.1, 28.5, 29.9, 31.7 | 43.6 (2026-10-17) | 2026-03-01 |
| HS02 | 25.0, 37.0, 31.5, 33.5, 35.5 | 38.6 (2026-05-02) | 2026-04-02 |
| GEVK | 10.8, 8.9, 10.9, 8.3 | 14.6 (2026-10-17) | 2026-03-13 |
| AUSV | 7.7 (one complete cycle) | 15.7 (2026-10-17) | 2025-10-07 |

At SENG the current dU is 1.37 times the largest earlier value and 1.76 times the smallest. This agrees with the IMO volume ratio (29.1 / 17-23 = 1.3-1.7). The absolute level at SENG (106 cm above October 2023) is 25 cm above the highest earlier pre-onset level (81 cm, July 2025).

### 2. The rules that best timed the earlier onsets failed for the current cycle (Figure 4)

Leave-one-out results for the ten events (median and maximum absolute timing error), and the stall test:

| Rule | SENG median / max error (days) | SENG stall z | SENG date the threshold was passed | HS02 median / max error (days) | HS02 stall z |
|---|---|---|---|---|---|
| H1a level rises per event (b = 8.2 cm/event at SENG, 7.3 at HS02) | 10 / 30 | +3.5 | 2026-02-15 | 6 / 20 | +1.1 |
| H0 fixed re-inflation | 22 / 47 | +2.2 | 2025-11-24 | 23 / 51 | +1.2 |
| H1c threshold grows with floor | 23 / 50 | +2.0 | 2025-11-29 | 25 / 55 | +1.1 |
| H1b level rises with time | 41 / 365 | -1.8 | not passed | 28 / 150 | -2.2 |
| H3 fading memory, tau_r = 30 d | 22 / 365 | -1.5 | not passed | 19 / 365 | -1.0 |
| H3 fading memory, tau_r = 90 d | 24 / 126 | -1.2 | not passed | 24 / 40 | -0.3 |
| H3 fading memory, tau_r = 180 d | 31 / 61 | -0.8 | not passed | 34 / 68 | +0.2 |

* The best rule for the past (H1a) timed all ten onsets within 30 days (SENG) and 20 days (HS02). It predicted the next event at about 93 cm at SENG; this level was passed on 2026-02-15. At 2026-10-17 the SENG level was 14 cm (3.5 SD) above the H1a threshold. H0 (the IMO-like volume rule) and H1c were passed in November 2025.
* The H0 errors change sign with time: early events came later than the rule predicted, and the 2025 events came 43-51 days earlier. Thus the needed re-inflation increased during the series, but the increase did not continue to the 44 cm of the current cycle.
* The rules that permit the stall have thresholds that increase with time (H1b) or that are harder to reach when loading is slow (H3). With short memory (tau_r = 30 d), H3 says that the April 2025 and July 2025 eruptions should have come 311-365 days later than they did, at both stations; H1b says the same for July 2025 (150-365 days). These rules are rejected by the 2025 eruptions.
* Fading memory with tau_r = 90-180 days is the only family that is not clearly rejected: median errors are 24-34 days (2-5 times the H1a errors), maximum errors 40-126 days, and the current cycle is 0.3-1.2 SD below its threshold at three of four station-tau combinations (HS02 with tau_r = 180 d passed its threshold on 2025-11-20). The margins are small, so continued uplift can reject this family soon.
* Figure 3 shows the post hoc view: the earlier onsets (cycles with at least 31 days) came at 31-day uplift rates of 57-219 cm/yr (the 2025 eruptions at 57-93 cm/yr), and the current cycle passed the earlier re-inflation levels at 15-30 cm/yr. A rule that needs both a re-inflation threshold and a minimum rate is consistent with all data, but we made it after we saw the stall, and it is not tested.

The k >= 5 subsets (only the six events from March 2024) give the same order (`files/results/rules_*_k5.csv`).

### 3. The current recharge has not stopped: a steady term continues (Figure 1)

| Station | q, steady term (cm/yr), 95% block-bootstrap interval | transient tau (days) | AIC gain of exp+linear over exp | bootstrap p (exp-only null) |
|---|---|---|---|---|
| SENG | 16.9 (15.8-17.9) | 91 | 370 | < 0.003 |
| HS02 | 18.1 (13.0-22.2) | 86 | 62 | 0.007 |
| GEVK | 8.2 (6.8-9.0) | 63 | 57 | < 0.003 |
| AUSV | 8.3 (6.7-9.2) | 75 | 53 | < 0.003 |

A pure exponential approach to a fixed level (constant deep pressure) is rejected at all four stations. After a transient of about 90 days, the uplift continued at a steady rate. If the rate does not change, SENG will rise by about 17 cm more in the 12 months after October 2026 (the pure exponential fit gives 4 cm). Thus the pause is not caused by a recharge that has stopped. The pause is caused by a trigger level that has become higher than the level that the 2023-2025 series showed, or by a different trigger process.

The earlier cycles were too short to separate a steady term from the transient. In the three cycles from August 2024 to July 2025, the exponential-only fits had tau 109-177 days, and the events occurred at 34-68% of the way to the fitted level; the current cycle is now at 88-92% of its exponential-only level. This is a description only, because the exponential-only model does not fit the current cycle well.

## Interpretation

The 2023-2025 series had a regular pattern: each new event needed approximately 8 cm more absolute uplift at SENG than the last event, and the trend predicted the onsets within 30 days.
After July 2025 the pattern stopped. Magma supply continued at a steady rate, and the uplift passed all thresholds that the earlier series defined, by November 2025 to February 2026.
Possible causes, which we did not test: (a) the large April 2025 dike (about 30 million m3, mostly not erupted) or the July 2025 eruption increased the compressive stress on the dike path, so that the threshold increased more than the trend; (b) the reservoir became larger or changed shape, so that the same uplift now means a smaller pressure; (c) magma now goes into storage outside the measured source.
A parallel case is Axial Seamount, where uplift passed the 2015 pre-eruption level by 0.36 m without an eruption (sci:sha256:efa0ed8b...).

For forecasts, this result shows that rules calibrated on the 2023-2025 series (fixed volume, or a threshold that rises per event) are not reliable for the current cycle: their thresholds were passed 8-11 months before the end of our data. A slow-loading (fading-memory) explanation with a long memory (90-180 days) remains possible but is weakly supported.

## Limitations

* Ten events and one stall. The stall is a single outcome, and we selected the rule families after we knew that the stall had occurred (the parameters were fitted only on the ten earlier events).
* Daily positions: onsets that are less than one day apart from the subsidence are resolved only to one day. HS02 data end on 2026-05-02 because of NGL processing latency.
* Uplift at one station is a proxy for reservoir volume and pressure. We did not model the source (for example, Mogi or a sill), and we did not use InSAR or seismicity.
* The SENG correction assumes that the 50.7 cm toggles are an artefact. HS02, which does not have toggles, gives the same conclusions.
* Event dates come from secondary summaries of IMO releases, not from IMO data files.
* The steady term q can be a part of a slower transient. Two more years of data are necessary to separate these.

## What remains open

* Test the rule "threshold and minimum rate" on the next event: it predicts that a new intrusion will start only after an uplift acceleration.
* Invert the GNSS (and InSAR) for source volume and depth per cycle, to test causes (a)-(c).
* Use the IMO seismicity catalogue to test whether earthquake rates in the dike path changed after April 2025.
* The 2020-2022 Svartsengi uplift episodes (visible at SENG and SKSH) ended without an eruption. They give a second sample of "uplift without a trigger".

## Reproduce

```
bash files/code/fetch_data.sh /tmp/svg_raw        # or use the shared store copies
cd files && SVG_RAW=/tmp/svg_raw bash code/run_all.sh   # writes ./out; about 2 minutes on 1 CPU
```
Python 3.12 with numpy, pandas, scipy and matplotlib. Results in this bundle: `files/results/` (`cycles_<STA>.csv` per-event levels, `expfits_<STA>.csv` per-cycle fits, `rules_<STA>_k1.csv` and `loo_*.csv` rule tests, `stallfit.json` current-cycle fits), figures in `files/figures/`.

## Data rights

`NOTICE-external-data.md` (in `files/`) identifies the external data and their terms. The bundle contains only our code, text, figures and derived aggregate values (event levels and fit parameters).

## References

* Blewitt, G., Hammond, W. C., Kreemer, C. (2018). Harnessing the GPS data explosion for interdisciplinary science. Eos 99. doi:10.1029/2018EO104623.
* Wikipedia, "2023-2025 Sundhnúkur eruptions", read 2026-11-12 (IMO chronology summary).
* IMO news releases on Svartsengi magma accumulation (2026), via the cited web pages.
