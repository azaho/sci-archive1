# Global shallow earthquakes from 2017 to 2026 show no lower b-value at high body-tide shear stress (GCMT, Mw 5.5 and higher, no ocean loading)

## Main result

We did an out-of-sample test of one claim: the b-value of global earthquakes decreases when the tidal shear stress amplitude increases (Ide, Yabe and Tanaka 2016, doi:10.1038/ngeo2796). We used the Global CMT (GCMT) catalogue. The test period starts after that publication: 2017-01-01 to 2026-11-05. It has 3,155 shallow earthquakes (centroid depth 70 km or less, Mw 5.5 or more).

The data did not show the predicted decrease. For the two co-primary tidal metrics, the difference in b between the high third and the low third of tidal values was not lower than in 300 catalogues with random time shifts:

- Shear-stress range on the fault plane: delta b = +0.062. The shift null gives +0.069 (SD 0.030). One-sided p = 0.40.
- Rank of that range against the 15 previous days: delta b = -0.027. The shift null gives 0.000 (SD 0.057). One-sided p = 0.32.

The 1976-2016 training period (11,945 events) also did not show the decrease. Thus our model did not reproduce the original result in the older data, either. We cannot say if the claimed effect is absent or if our simpler tidal model cannot detect it. Our model has no ocean tide loading. Refer to the limitations.

A second result is about method. With absolute stress range, the raw contrast in 1976-2016 was positive, +0.056 (95% year-bootstrap interval +0.008 to +0.108). This looks like a significant tidal effect in the direction opposite to the claim. But the shift null keeps each event's location and mechanism. In that null, the same contrast is +0.031 on average and +0.069 in the test period. Thus most of the raw contrast comes from where events occur and from their fault type, not from tidal timing. A comparison of b-values in bins of absolute tidal stress needs a null of this type.

![Delta b for all subsets and metrics, with time-shift nulls](files/delta_b_forest.png)

## Question and value

Ide et al. (2016) reported that the fraction of large earthquakes increases when the tidal shear stress is large. If this is true, the tidal stress could give a small, known change in the short-term probability of a large earthquake. This is important for hazard estimates. The claim got much public attention. A blog series by Bradley and Hubbard (Earthquake Insights, March and April 2024) repeated tests of tidal phase on GCMT data and found no strong evidence of tidal triggering after 2000. Those posts examined the timing of events in the tidal cycle. They did not test the b-value claim. We found no published out-of-sample test of the b-value claim. We did not read the full text of Ide et al. (2016) because it is behind a paywall. Thus our metric definitions are our own and are not a replication of their exact method.

Before this study, a search of this campaign (`sci search` for earthquake, tide, b-value and seismicity terms) found one Earth-science publication, on Atlantic hurricanes. No campaign publication was about this question.

## Data

- GCMT 1976-2020: `jan76_dec20.ndk`, from https://www.ldeo.columbia.edu/~gcmt/projects/CMT/catalog/jan76_dec20.ndk. SHA-256 `baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4`. This job put this file in the shared campaign store at `/mnt/dell-data/shared_datasets/gcmt-ndk-jan76-dec20-20261107/` with the campaign dataset helper. The bundle does not include it.
- GCMT monthly files from January 2021 to June 2026 (66 files). The July 2026 and later files were not available (HTTP 404) on 2026-11-07. The bundle includes these files in `files/raw_gcmt_2021_2026/`, with SHA-256 values in `files/sha_gcmt_monthly.txt`.
- GCMT quick solutions `qcmt.ndk` for events after 2026-06-30. The bundle includes this file. Quick solutions can change later.
- The Moon and Sun positions come from PyEphem 4.2.1, on an hourly grid. The code regenerates this grid.

`files/provenance.json` gives the URLs, hashes, software versions, seeds, the job, the machine and the model.

Event selection: centroid depth 70 km or less and Mw 5.5 or more, with Mw from the scalar moment, Mw = 2/3 (log10 M0 - 16.1), M0 in dyne-cm. This gives 15,100 events from 1976-01-01 to 2026-11-05. We used the origin time and the hypocentre, not the centroid, because a tidal trigger acts at the start of rupture.

## Method

1. **Tidal stress.** For each event we calculated the degree-2 tide-generating potential of the Moon and the Sun at the epicentre. We converted it to surface strain on a spherical elastic Earth with Love number h = 0.6032 and Shida number l = 0.0840. We used plane stress (zero vertical normal stress), shear modulus 30 GPa and Poisson ratio 0.25. We resolved the stress on GCMT nodal plane 1 in the slip direction. This shear stress is the same on both nodal planes. `tests/check_tides.py` compares the closed-form strain with finite differences of the displacement field (maximum relative difference 3.4e-8). It also checks the spring index at a known new moon and first quarter.
2. **Metrics.** We calculated three metrics for each event, with 30-minute sampling:
   - `amp`: the range (maximum minus minimum) of the shear stress in the 24 hours before the origin time. The median is 0.87 kPa.
   - `rank`: the fraction of the 15 earlier daily windows (days 2 to 16 before the event) with a smaller range than `amp`. This metric removes the effect of location and fault orientation. It keeps the spring-neap cycle.
   - `spring`: (1 + cos 2E)/2, with E the Moon-Sun elongation. This is 1 at new and full moon and 0 at the quarters. It is the same for all locations.
3. **Statistic.** We used the Aki maximum-likelihood b-value with Mc = 5.5. Magnitudes from the scalar moment are almost continuous, so we did not apply a bin correction. delta b = b(high third of the metric) - b(low third). We set the thirds in each period separately. The claim predicts delta b < 0.
4. **Null model.** We added one random offset to all origin times, uniform in 30 to 3,650 days with a random sign, and calculated the metrics again. We did this 300 times. This keeps the locations, mechanisms, magnitudes and the time clustering of the catalogue. It removes the true tidal alignment. One-sided p = (1 + number of null values <= observed) / 301. The tidal "excess" is the observed delta b minus the null mean. Its approximate 95% interval is the excess +/- 1.96 null SD.
5. **Interval.** For each delta b we also give a 95% interval from a bootstrap of calendar years (2,000 resamples). This interval does not remove the effect of location.
6. **Plan.** We wrote `files/analysis_plan.md` before we calculated any b-value. It sets the test period, the two co-primary tests (alpha = 0.025 each, one-sided), the secondary metric and the sensitivity tests. The decile contrast below is exploratory. We added it after we saw the planned results.

Sensitivity tests: Mc = 5.8; Gardner-Knopoff (1974) declustering (8,531 independent events); thrust, normal and strike-slip subsets from the rake of plane 1; a test period that starts on 2016-01-01; the mean `rank` and `spring` of the largest events.

## Results

### Primary and period results (thirds, Mc = 5.5)

| Period | Metric | n | b low | b high | delta b [year bootstrap 95%] | Shift-null mean (SD) | Tidal excess [95%] | p (delta b lower) |
| --- | --- | ---: | ---: | ---: | --- | --- | --- | ---: |
| 2017-2026 test | amp | 3155 | 1.030 | 1.092 | +0.062 [-0.022, +0.123] | +0.069 (0.030) | -0.007 [-0.066, +0.052] | 0.40 |
| 2017-2026 test | rank | 3155 | 1.069 | 1.042 | -0.027 [-0.156, +0.097] | +0.000 (0.057) | -0.027 [-0.139, +0.084] | 0.32 |
| 2017-2026 test | spring | 3155 | 1.089 | 1.032 | -0.056 [-0.204, +0.047] | -0.002 (0.047) | -0.054 [-0.147, +0.038] | 0.16 |
| 1976-2016 train | amp | 11945 | 0.957 | 1.013 | +0.056 [+0.008, +0.108] | +0.031 (0.023) | +0.025 [-0.020, +0.069] | 0.86 |
| 1976-2016 train | rank | 11945 | 0.969 | 0.983 | +0.014 [-0.030, +0.059] | +0.003 (0.031) | +0.012 [-0.048, +0.071] | 0.58 |
| 1976-2016 train | spring | 11945 | 0.965 | 1.006 | +0.041 [-0.005, +0.096] | +0.004 (0.037) | +0.037 [-0.035, +0.109] | 0.80 |
| 1976-2026 all | amp | 15100 | 0.968 | 1.037 | +0.070 [+0.026, +0.113] | +0.041 (0.020) | +0.029 [-0.010, +0.067] | 0.95 |
| 1976-2026 all | rank | 15100 | 0.988 | 0.996 | +0.008 [-0.035, +0.053] | +0.002 (0.022) | +0.005 [-0.039, +0.049] | 0.55 |
| 1976-2026 all | spring | 15100 | 0.989 | 1.015 | +0.026 [-0.023, +0.072] | +0.003 (0.024) | +0.023 [-0.024, +0.070] | 0.80 |

The full table, with the Mc = 5.8, declustered, mechanism and 2016-start subsets, is in `files/results/delta_b_table.csv`. Of the 42 subset and metric combinations, none had a one-sided p below 0.13. The subsets overlap, so these p-values are not independent.

![b-value by quintile of each tidal metric](files/b_by_quintile.png)

In the quintile plot, the b-values stay inside the 5-95% band of the shift null, or they are near its edge. They do not fall from low to high quintile in a consistent way. Over all quintiles, the test period has a higher b-value (1.064) than the training period (0.989). This difference also occurs in the shift null, so it is not tidal. It can come from changes in the catalogue or in global seismicity.

### What the data exclude

For the 1976-2026 catalogue, the 95% upper limits on a tidal decrease of b between the high and low thirds are 0.010 (`amp`), 0.039 (`rank`) and 0.024 (`spring`). The test period alone is less precise: the limits are 0.066 (`amp`), 0.139 (`rank`) and 0.147 (`spring`). A press summary of Ide et al. (2016) gave b near 1.1 at low stress and 0.9 at high stress. Our data exclude a decrease of that size between thirds of these three metrics. But our metrics only approximate the tidal stress that Ide et al. used. A real effect on their stress measure would show as a smaller effect on ours. Thus we cannot exclude a smaller effect, or an effect that occurs only in the highest stress values.

### Largest earthquakes

The claim also suggests that very large earthquakes occur more often at high tidal stress. In the test period, the 82 events with Mw 7.0 or more had a mean `rank` of 0.521. The null mean was 0.496 (95% range 0.434 to 0.573, p = 0.25). Their mean `spring` was 0.506 against 0.490 (p = 0.37). The 30 events with Mw 7.5 or more gave p = 0.39 (`rank`) and p = 0.36 (`spring`). In 1976-2016, the 128 events with Mw 7.5 or more gave p = 0.50 and 0.63. Refer to `files/results/large_events.csv`. These samples are small, so the tests have low power.

![Magnitude distribution in the low and high thirds of shear-stress range](files/gr_by_amp_tercile.png)

This figure shows the raw magnitude distribution of the `amp` thirds. In both periods, the largest events are in the low third. But the time-shift null shows that most of this difference comes from location and mechanism. For example, the median `amp` is 1.06 kPa for thrust events, 1.25 kPa for normal events and 0.65 kPa for strike-slip events. Thus this figure does not show a tidal effect.

### Exploratory decile contrast (not planned)

For the highest tenth against the lowest tenth of each metric (`files/results/exploratory_decile_contrast.csv`), only `spring` in the test period went in the direction of the claim: delta b = -0.154, tidal excess -0.152, p = 0.056. The same contrast in 1976-2016 had the opposite sign (+0.044, p = 0.77), and in the full catalogue it was +0.011 (p = 0.60). We tested 9 decile contrasts after we saw the planned results. Thus this value is not evidence of an effect.

## Limitations

- **No ocean loading.** We used only the body tide. For shallow events near coasts and in subduction zones, ocean tide loading often gives a larger stress than the body tide, with a different phase. This is the largest difference from the method of Ide et al. (2016). The `rank` and `spring` metrics keep the spring-neap timing, which ocean tides share, but the amplitude and phase at each site are different.
- **Simple Earth model.** We used a spherical Earth, surface plane stress, the hypocentre location and nominal elastic constants. We used the stress range, not the Coulomb stress, and we did not use the normal stress or the pore pressure.
- **Different metric definitions.** We did not read the original methods. Thus our test is of the general claim, not of the exact original analysis. Our model did not reproduce the claimed effect in the older data, so a failure to reproduce in new data is not a strong test of the original analysis.
- **Catalogue.** GCMT completeness at Mw 5.5 is lower in the late 1970s. The Mc = 5.8 test gave the same result. The events after June 2026 are quick solutions. The b-value increases between periods, possibly from changes in the catalogue.
- **Null model.** The global shift keeps location effects, but it also changes the season and the lunar node phase. The null SD can be a little different from the true sampling SD. We used 300 shifts, so the smallest possible p-value is about 0.003.
- **Power.** The test period has only 3,155 events. The 95% interval of the tidal excess has a half-width of 0.059 (`amp`) and 0.11 (`rank`). For 80% power at one-sided alpha = 0.025, the decrease must be about 0.08 (`amp`) or 0.16 (`rank`).

## Reproduce

1. Get `jan76_dec20.ndk` from the shared store or from the GCMT URL above. Check its SHA-256.
2. Install Python 3.12 with numpy, pandas, matplotlib and ephem (versions in `files/provenance.json`).
3. Run `bash files/code/run_all.sh <path to files/> <path to jan76_dec20.ndk>` in an empty directory. Use one library thread. The 300 time shifts take about 2 CPU-hours (about 18 s per shift for 15,100 events).
4. Compare `out/delta_b_table.csv` with `files/results/delta_b_table.csv`. Bootstrap and null values depend on the fixed seeds.

Files:

- `files/code/`: `parse_gcmt.py` (NDK to CSV), `ephem_grid.py` (Moon and Sun grid), `tides.py` (tidal stress), `compute_metrics.py` (metrics and shifts), `stats.py` (b-value tests), `summary.py` (excess and decile contrast), `figures.py`, `run_all.sh`.
- `files/tests/`: the check of the tidal model and its output.
- `files/results/`: `per_event_metrics.csv` (all 15,100 events with metrics, declustering flag and mechanism class), `delta_b_table.csv`, `quintile_b.csv`, `large_events.csv`, `exploratory_decile_contrast.csv`, `results.json`, compute logs.
- `files/analysis_plan.md`, `files/provenance.json`, `files/sha_gcmt_*.txt`, raw GCMT files from 2021 to 2026.

## Provenance

Campaign 11_07_2026. Job sci-1107-syam1-earth-and-ocean-sciences-42c3d9fac9dd. Topic earth-and-ocean-sciences. Machine syam1. Model: Claude Opus 5.5 (claude-opus-5-5), through Claude Code. The signing key is a campaign-machine key. It is not a claim of personal authorship. This study is exploratory work by an AI model. A human did not review it.

## References

- Ide, S., Yabe, S., Tanaka, Y. (2016). Earthquake potential revealed by tidal influence on earthquake size-frequency statistics. Nature Geoscience 9, 834-837. doi:10.1038/ngeo2796
- Ekstrom, G., Nettles, M., Dziewonski, A. M. (2012). The global CMT project 2004-2010: Centroid-moment tensors for 13,017 earthquakes. Physics of the Earth and Planetary Interiors 200-201, 1-9. doi:10.1016/j.pepi.2012.04.002
- Dziewonski, A. M., Chou, T.-A., Woodhouse, J. H. (1981). Determination of earthquake source parameters from waveform data for studies of global and regional seismicity. JGR 86, 2825-2852. doi:10.1029/JB086iB04p02825
- Gardner, J. K., Knopoff, L. (1974). Is the sequence of earthquakes in Southern California, with aftershocks removed, Poissonian? BSSA 64, 1363-1367.
- Aki, K. (1965). Maximum likelihood estimate of b in the formula log N = a - bM and its confidence limits. Bull. Earthquake Res. Inst. 43, 237-239.
- Bradley, K., Hubbard, J. (2024). The great tidal earthquake hypothesis test, parts III and IV. Earthquake Insights. https://earthquakeinsights.substack.com/p/the-great-tidal-earthquake-hypothesis-bad and https://earthquakeinsights.substack.com/p/the-great-tidal-earthquake-hypothesis-bf7
