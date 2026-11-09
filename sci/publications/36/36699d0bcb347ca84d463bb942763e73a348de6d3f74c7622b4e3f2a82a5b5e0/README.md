# The b-value in the 2011 Tohoku-oki high-slip zone stayed above its 1998-2011 level through 2024

## Summary

Tormann et al. (2015) reported that the Gutenberg-Richter b-value in the high-slip zone of the 2011 Mw 9.0 Tohoku-oki earthquake increased at the mainshock and then returned near its pre-mainshock level within about two years. They used this result to say that stress recovers quickly. Bürgmann et al. (2016) replied that the b-value change can come from a change in the event population (different source volumes and faulting types), not from stress. Nanjo et al. (2025) reported that b-values stayed high until June 2025.

We tested three possible artefacts that earlier studies did not separate:

1. A change in the depth mix of events relative to the plate interface (Slab2).
2. Catalogue-wide changes in the JMA catalogue (detection, the April 2016 addition of automatic hypocentres, magnitude types). We use two control regions for this.
3. Changes in completeness. We use fixed thresholds of Mc 3.0 and 3.5 and the b-positive estimator, which tolerates a changing completeness.

Main result. In the high-slip box (HS, 37.5-39.0 N, 142.5-144.2 E), the Aki-Utsu b-value at Mc 3.0 was 0.68 (n = 817) in 1998 to 8 March 2011. It was 0.79 (n = 2,221) in April 2011 to 2013, 0.91 (n = 423) in 2014-2024 and 0.97 (n = 134) in 2019-2024. We found no return to the pre-mainshock level in any post-mainshock window. The 2014-2024 increase was +0.24 (95% bootstrap interval 0.15 to 0.33). The increase stayed when we:

- reweighted each period to the pre-2011 depth mix: +0.28 (0.18 to 0.38)
- used Mc 3.5: +0.42 (0.28 to 0.57)
- used b-positive with a 3.0 floor: +0.24 (0.10 to 0.39)
- subtracted the change in the off-Hokkaido control: +0.18 (0.09 to 0.28)
- subtracted the change in the Izu-Bonin control: +0.23 (0.13 to 0.32)

Thus the result does not agree with a rapid recovery of the b-value. It agrees with the persistent increase that Nanjo et al. (2025) reported. Depth mix and catalogue-wide changes do not explain it.

Main limitation. In GCMT (Mw 5.0 or more), 20 of 24 HS events before 2011 were thrust events. After the mainshock, 2 of 17 HS events in April 2011 to 2013 were thrust events and 10 were normal-faulting events. The JMA catalogue has no focal mechanisms for small events, so we cannot reweight by faulting type. Normal-faulting populations usually have higher b-values. Thus a change in faulting type, which Bürgmann et al. (2016) proposed, can still explain part or all of the increase. This study does not show that differential stress stays low.

## Job and provenance

- Campaign: 11_07_2026. Job: sci-1107-hp-earth-and-ocean-sciences-6cee50e5643b. Topic: earth-and-ocean-sciences. Machine: hp. Account: claude-olen.
- Model: Claude Opus 5.5 (claude-opus-5-5), through Claude Code in T3 Code. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Date of analysis: 2026-11-09.
- Data (all read in place from the shared dataset store `./datasets`, which is `/mnt/dell-data/shared_datasets`). `files/provenance.json` gives the URLs, byte counts and SHA-256 hashes of all input files:
  - JMA unified hypocentre catalogue, yearly files h1998.zip to h2024.zip (`jma-hypocenter-hYYYY-20261109`), 4,932,692 records with type J.
  - USGS Slab2 (Hayes et al. 2018), `Slab2Distribute_Mar2018.tar.gz` (sha256 3f53a835...b1d). We used the kur and izu depth grids. We added this dataset to the shared store with the campaign dataset helper.
  - Global CMT catalogue 1976-2020 (`jan76_dec20.ndk`, sha256 baed5ad2...0eb4). We used it only for the counts of faulting types.

## Methods

Event selection. We used JMA records with subsidiary flag 1 (natural earthquakes), a valid magnitude and a valid depth. Magnitudes are rounded to 0.1. We left out 9 March to 10 April 2011, which contains the M7.3 foreshock, the mainshock and the first 30 days of aftershocks, when completeness changes fastest.

Regions (latitude and longitude boxes):

| Code | Box | Role |
|---|---|---|
| HS | 37.5-39.0 N, 142.5-144.2 E | Tohoku-oki high-slip zone (main target) |
| HScore | 37.8-38.6 N, 142.8-143.9 E | smaller core of HS |
| RZ | 35.5-40.5 N, 141.5-145.0 E | wider rupture zone (contains HS) |
| HOK | 41.5-43.5 N, 143.0-147.0 E | control, southern Kuril trench off Hokkaido |
| IZU | 30.0-34.0 N, 139.0-143.0 E | control, Izu-Bonin |

Position relative to the plate interface. For each event, dz = JMA depth - Slab2 interface depth. The classes are upper plate (dz < -10 km), interface (|dz| <= 10 km) and slab (dz > 10 km). A variant uses 15 km.

Estimators.
- Aki-Utsu maximum likelihood with bin correction, b = log10(e) / (mean(M) - (Mc - 0.05)), at fixed Mc = 3.0 and Mc = 3.5.
- Fixed-composition b. Each event gets the weight p_pre(class) / p_period(class), so that every period has the 1998-2011 class shares. Then we calculate the weighted Aki-Utsu b.
- b-positive (van der Elst 2021). We use the positive magnitude differences of 0.2 or more between consecutive events in time, with magnitude floors 2.0, 2.5 and 3.0.
- Uncertainty. We used 1,000 bootstrap resamples for the period tables and 2,000 for the pooled contrasts. For the Aki-Utsu contrasts we also give the Utsu (1992) test probability.
- Control comparison. We calculated (HS change) - (control change) from independent bootstrap draws.

Windows. PRE = 1998-01-01 to 2011-03-08. EARLY = 2011-04-11 to 2013-12-31. LATE = 2014-2024. LATE2019 = 2019-2024. We also used eight shorter periods (Table 1).

## Results

### Table 1. HS, Aki-Utsu b at Mc 3.0, by period

| Period | n | b (95% CI) | b with pre-2011 depth mix | Slab share | b interface class | b slab class |
|---|---|---|---|---|---|---|
| 1998-2003 | 412 | 0.74 (0.67-0.82) | 0.74 | 0.43 | 0.77 | 0.70 |
| 2004-2011.03 | 405 | 0.62 (0.57-0.68) | 0.61 | 0.29 | 0.64 | 0.60 |
| 2011.04-2011 | 1133 | 0.80 (0.76-0.84) | 0.84 | 0.54 | 0.95 | 0.71 |
| 2012-2013 | 1088 | 0.78 (0.74-0.83) | 0.85 | 0.82 | 0.89 | 0.76 |
| 2014-2015 | 162 | 0.92 (0.82-1.06) | 0.92 | 0.60 | 0.92 | 0.93 |
| 2016-2018 | 127 | 0.85 (0.73-0.99) | 0.90 | 0.64 | 1.00 | 0.80 |
| 2019-2021 | 88 | 0.97 (0.81-1.19) | 1.04 | 0.55 | 1.20 | 0.89 |
| 2022-2024 | 46 | 0.95 (0.75-1.24) | 1.01 | 0.52 | (n = 15) | (n = 24) |

The share of slab events (more than 10 km below Slab2) at M 3.0 or more increased from 0.29-0.43 before 2011 to 0.82 in 2012-2013 (Figure 2). But the b-value increased in the interface class and in the slab class separately. Reweighting to the pre-2011 mix made the increase slightly larger, not smaller.

### Table 2. Change from PRE to LATE (2014-2024), with 95% bootstrap intervals

| Method | HS | HOK | IZU | HS - HOK | HS - IZU |
|---|---|---|---|---|---|
| Aki Mc 3.0 | +0.24 (0.15, 0.33) | +0.05 (0.02, 0.09) | +0.01 (-0.01, 0.04) | +0.18 (0.09, 0.28) | +0.23 (0.13, 0.32) |
| Aki Mc 3.5 | +0.42 (0.28, 0.57) | +0.10 (0.05, 0.16) | -0.04 (-0.09, 0.01) | +0.32 (0.16, 0.48) | +0.46 (0.31, 0.62) |
| Aki Mc 3.0, pre-2011 depth mix | +0.28 (0.18, 0.38) | +0.06 (0.02, 0.10) | +0.01 (-0.02, 0.04) | +0.22 (0.11, 0.33) | +0.26 (0.17, 0.37) |
| Aki Mc 3.0, depth mix with 15 km class limit | +0.27 (0.17, 0.37) | +0.05 (0.02, 0.09) | +0.01 (-0.01, 0.04) | +0.21 (0.11, 0.33) | +0.25 (0.15, 0.36) |
| b-positive, floor 3.0 | +0.24 (0.10, 0.39) | +0.09 (0.02, 0.15) | -0.03 (-0.10, 0.03) | +0.15 (-0.00, 0.32) | +0.27 (0.12, 0.44) |
| b-positive, floor 2.5 | +0.24 (0.15, 0.34) | +0.04 (-0.00, 0.08) | -0.01 (-0.05, 0.03) | +0.20 (0.10, 0.31) | +0.25 (0.16, 0.36) |
| b-positive, floor 2.0 | +0.18 (0.11, 0.24) | +0.04 (0.01, 0.06) | -0.00 (-0.03, 0.02) | +0.14 (0.07, 0.21) | +0.18 (0.11, 0.25) |
| b-positive, floor 2.0, flag K only (biased, see below) | +0.07 (0.00, 0.13) | +0.03 (0.00, 0.06) | -0.03 (-0.06, 0.01) | +0.04 (-0.03, 0.11) | +0.09 (0.02, 0.17) |

`files/results/pooled_contrasts.csv` and `did_contrasts.csv` give all windows (EARLY, LATE, LATE2019) and the HScore and RZ regions.

### Direct test of the rapid-recovery claim

If the b-value had returned to its pre-mainshock level by about 2013, the change in the later windows would be near zero. For HS at Mc 3.0, the change was +0.11 (0.06 to 0.17) in EARLY, +0.24 (0.15 to 0.33) in LATE and +0.29 (0.15 to 0.46) in LATE2019. The b-value moved further away from the pre-mainshock level, not back to it. The EARLY increase relative to HOK was not clear at Mc 3.0 (+0.02, -0.07 to 0.11), but it was clear at Mc 3.5 (+0.15, 0.00 to 0.28). Thus the evidence that the b-value stayed high is strongest after 2014.

### Other observations

- The control off Hokkaido also increased: +0.05 at Mc 3.0 and +0.10 at Mc 3.5. The Izu-Bonin control did not change clearly. Thus a part of the raw HS increase can be regional or catalogue-wide. The control differences in Table 2 remove that part.
- The wider rupture zone (RZ) increased less, +0.06 (0.03 to 0.08) at Mc 3.0. The increase is concentrated in the high-slip zone.
- Before 2011, the HS Aki-Utsu b at Mc 3.0 decreased from 0.74 (1998-2003) to 0.62 (2004 to March 2011). This agrees with the decrease before the mainshock that other studies reported. b-positive at floor 2.0 did not show this decrease (0.71 and then 0.70). Thus this decrease before the mainshock is not robust to the estimator.
- Catalogue flags. From April 2016, 57-70% of HS events at M 2.0 or more have flags other than K (automatic or low-precision hypocentres) (Figure 2). These events are small: their mean magnitude is 2.27, and the mean of the flag-K events is 2.84. Only 4% of the HS events at M 3.0 or more after April 2016 have flags other than K. Thus the Mc 3.0 and Mc 3.5 results do not depend on this change. When we keep only flag-K events at M 2.0, we remove small events selectively, and the result is a b-value that is too low. When we keep all flags at M 2.0, the result depends on the automatic magnitudes. For this reason we do not use the M 2.0 b-positive values as evidence.
- Magnitude types. JMA gives D-type (displacement) magnitudes mostly to the larger events (median Mj 4.7 in HS) and V-type (velocity) magnitudes to the smaller events. A V-only subset therefore removes large events and gives b-values that are too high. We report this subset in `bvalues_by_period.csv` (variant `V_only`) but do not use it as a check.

## Figures

- `files/figures/fig1_rolling_bvalues.png`: rolling b-values for HS and the two controls.
- `files/figures/fig2_composition_flags_mc.png`: HS depth mix relative to Slab2, share of non-K flags, and yearly completeness proxy.
- `files/figures/fig3_pooled_contrasts.png`: PRE to LATE changes and control differences for all estimators.

## Limitations

1. Faulting type is not controlled. GCMT faulting types in HS changed from mostly thrust events to mostly normal-faulting events (`files/results/gcmt_mechanism_counts.csv`; only 3 HS events of Mw 5.0 or more in 2014-2020). This change can cause part or all of the b-value increase.
2. Offshore JMA depths before the S-net network (installed 2016-2017) have errors of many kilometres. Thus the interface, slab and upper-plate classes are approximate.
3. Box regions are simple. We did not repeat the distance-weighted sampling along the interface that Tormann et al. (2015) used. Thus this is a test of their conclusion, not an exact repeat of their method.
4. The late windows have few events in HS (n = 134 for 2019-2024 at Mc 3.0, n = 48 at Mc 3.5). Thus the late intervals are wide.
5. The fixed thresholds of Mc 3.0 and 3.5 can be below the true completeness in the months soon after the mainshock (the yearly MAXC proxy was 2.8 in 2011-2013). b-positive with a 3.0 floor gave the same result, which reduces this concern.
6. We did not decluster the catalogue. The post-mainshock windows are mostly aftershocks.
7. We did not correct for multiple tests. We give many variants to show robustness, not to select the best one.
8. The JMA magnitude (Mj) is not Mw. A change in the magnitude calculation over time that affects only HS is not excluded, but the control regions show no such change.

## Reproduction

From the worktree root, with `./datasets` mounted:

```
bash work/result/files/code/run_all.sh
```

The steps are: parse JMA (`parse_jma.py`), extract two Slab2 grids, calculate the period b-values (`bvalue_analysis.py`), calculate the pooled contrasts (`pooled_tests.py`), count GCMT faulting types (`gcmt_mechanisms.py`) and make the figures (`figures.py`). The random seeds are fixed (20261109 and 7). The total run time was about 30 minutes on 8 cores. `files/results/selected_events_M2_HS_HOK_IZU.csv.gz` contains the selected events (M 2.0 or more, HS, HScore, HOK, IZU) with their Slab2 classes, so you can examine the results without the raw catalogue.

## References

- Tormann, T., Enescu, B., Woessner, J., Wiemer, S. (2015). Randomness of megathrust earthquakes implied by rapid stress recovery after the Japan earthquake. Nature Geoscience 8, 152-158. doi:10.1038/ngeo2343
- Bürgmann, R., Uchida, N., Hu, Y., Matsuzawa, T. (2016). Tohoku rupture reloaded? Nature Geoscience (correspondence). doi:10.1038/ngeo2649
- Nanjo, K. Z. et al. (2025). Non-randomness of Japan megaquakes implied by stress recovery and accumulation. Communications Earth & Environment. doi:10.1038/s43247-025-03075-6
- van der Elst, N. J. (2021). B-positive: a robust estimator of aftershock magnitude distribution in transiently incomplete catalogs. JGR Solid Earth 126, e2020JB021027. doi:10.1029/2020JB021027
- Hayes, G. P. et al. (2018). Slab2, a comprehensive subduction zone geometry model. Science 362, 58-61. doi:10.1126/science.aat4723
- Utsu, T. (1992). On seismicity. Report of the Joint Research Institute for Statistical Mathematics.
- Aki, K. (1965). Maximum likelihood estimate of b in the formula log N = a - bM and its confidence limits. Bull. Earthquake Res. Inst. 43, 237-239.
