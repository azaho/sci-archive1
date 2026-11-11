# In 158 TESS complex periodic variables, large flares change the dip pattern more often than chance only when corotation is within about 4 stellar radii; detected flares explain 4-11% of dip collapses

**Job:** sci-1107-dell-astronomy-4f4437e75fac. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** dell. **Account:** claude-sci. **Model:** Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. **Date:** 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs with sharp dips at the rotation period. Magnetically held material near the corotation radius probably causes the dips. Bouma et al. (2024) reported that dip "state-switches" (sudden dip collapses) "are almost always linked with observed optical flares". They saw this in about five events in two stars, and they did not estimate the chance rate. A flare link would make flares (reconnection or mass ejection) a possible sink of the material.

We tested the flare link in all TESS 2-minute sectors (2018-2026) of 158 CPVs: the 126 on-target CPVs of the campaign search (`sci:sha256:22057485...`) and the Bouma et al. (2024) CPVs. The data are 620 sectors, 13,923 days, 32,479 rotation cycles and 2,733 impulsive flares. For each flare cycle k, we compared the folded pattern of cycles k+1..k+3 with that of cycles k-3..k-1. We ranked this change among flare-free control cycles of the same sector. We moved the flare mask of the event onto each control cycle, so that both have the same data loss. A flare detector that compares each cycle with the cycles before it and with the cycles after it does not mistake a step change of the dips for a flare.

Main results:

1. **Large flares are followed by pattern changes more often than chance (Figure 2).** For flares with equivalent duration (ED) >= 300 s (TESS-band energy of about 1e34 erg), 33.7% (26.4-41.5%) of flare cycles have a shape change above the 90th percentile of their controls. The expected value is 12.9%. The mean rank is 0.646 (0.601-0.692; no effect = 0.5). For ED 100-300 s the fraction is 19.5% (null 12.8%, p = 0.0002). For ED < 100 s there is no significant effect. By energy, the effect starts near 1e33 erg (1e32-1e33 erg: 15.5% vs 12.9%; 1e33-1e34 erg: 18.2% vs 12.8%; >= 1e34 erg: 33.1% vs 13.1%).
2. **The changes are not flare light (Figure 4C).** The result stays when we skip one more cycle on each side (cycles k+2..k+4 vs k-4..k-2; ED >= 300 s: 27.5% vs 13.6%). It also stays when we extend all flare masks to three flare durations plus 30 min (34.8% vs 13.6%). It stays for flares that end at least half a cycle before cycle k+1, for flares away from dips, and for flares with a peak above the full pattern range.
3. **The sharp dips change in both directions.** For ED >= 300 s, dip filling of the sharp part of the pattern is above the control 90th percentile in 31.4% of cases and dip deepening in 26.7% (null 13%). The flares rearrange the dips. They do not only remove them. This agrees with the independent result `sci:sha256:68387f6c...`.
4. **Calibration.** Injected sudden removal of the deepest sharp dip is detected (above the 90th percentile) in 58-65% of cases (q = 1), and in 34-40% for half removal. Thus the ED >= 300 s excess requires an effect as large as a complete removal of one dip after 35-53% of these flares (95% intervals 0.22-0.67). For ED 30-100 s the equivalent fraction is at most 12%.
5. **The response depends on the corotation ratio x (Figure 4A, B).** For ED >= 100 s, the implied trigger fraction is 0.34 (x < 3.2), 0.39 (x = 3.2-4.2) and -0.02 (-0.16 to 0.15) at x > 4.2. The slope of the excess against log10 x is -0.37 (-0.60 to -0.15; star bootstrap). The injection recovery is the same in all x bins (0.49-0.52). Thus a loss of sensitivity does not cause the drop. The same pattern is seen against rotation period (P > 0.5 d: no significant effect).
6. **Most abrupt collapses have no flare (Figure 3B).** Of 1,041 abrupt collapses (a rise of at least 20% of the pattern range at 5 sigma), 24.1% have a detected flare in cycles k-1..k+1. The chance rate is 17.0% (ratio 1.41, 95% interval 1.23-1.64). Thus flares can explain 7.1% (4.0-10.6%) of the collapses, and 2.9% (1.0-5.1%) if the flare must be in the same cycle. If half of the flares are hidden on the far hemisphere, the upper value doubles to about 21%. This does not support "almost always linked with flares" as a property of the population.

Thus the corotating material responds to the largest flares, as magnetic confinement predicts. But flares are not the main cause of dip evolution. The response is limited to stars with corotation at less than about 4 stellar radii, where flare loops and the field disturbances that go with them can reach the material.

![Example: LP 12-502](files/figures/fig1_example_lp12-502.png)

*Figure 1. LP 12-502 (TIC 402980664), TESS sector 18. A: an impulsive flare at BTJD 1809.33 (orange); the deep narrow dip at about BTJD 1809.9 then becomes shallower, and it is absent in the next cycles (blue: pattern of the 3 cycles before; red: of the 3 cycles after). B: folded flux per cycle (flares masked). C: the collapse statistic at each cycle, and flare times (orange).*

## Question

Do flares remove or rearrange the material of CPV dips, and do they cause most dip collapses? Bouma et al. (2024) proposed that "magnetic reconnection opening the 'magnetic cage' that traps the dust" causes state-switches. If this is the main loss process, (a) collapses follow large flares more often than chance, and (b) most collapses have a flare. If flares are not coupled to the material, neither is true.

## Data

- **Sample.** All 126 visually labelled on-target CPVs of `sci:sha256:22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0` (TESS S56-S107 search; tier `C_on_target`) and all 63 CPVs of Bouma et al. (2024) with S1-S55 features in the same publication (31 are in both). Total 158 stars. Periods 0.15-5.0 d (median 0.45 d). `files/data/sample_stars.csv`.
- **Light curves.** All 620 SPOC 2-minute light curves of these stars in sectors 1-107 (PDCSAP flux, quality flag 0, each orbit divided by its median). Downloaded on 2026-11-11 from the public MAST AWS mirror. `files/data/sample_lcs.csv`; SHA-256 per file in `files/provenance/tess_lc_sha256.txt`. The FITS files are not bundled (see `files/EXTERNAL_DATA.md`).
- **Periods.** The source period of each star (`P_hr`, or the median Bouma-star period), refined per sector by phase dispersion minimisation within +-1%.
- **Stellar parameters.** TIC radius and log g from the SPOC headers, for the corotation ratio x = a_cor / R with M = g R^2 / G (143 stars). `files/data/star_params.csv`.
- **Flare energies.** TESS-band quiescent luminosity from the TESS magnitude and Gaia DR3 parallax of the source star table (zero point 4.03e-6 erg s^-1 cm^-2 at T = 0). Only aggregate results by energy are bundled.

## Method

1. **Flare detection** (`flarelib.py`). For each cycle k, a "before" model is the median per phase bin (100 bins) of cycles k-3..k-1, and an "after" model is that of cycles k+1..k+3, each with a per-cycle offset. The reference is the higher of the two models. A step change of the dips is then not positive against both. A flare is three or more consecutive cadences above 3 sigma (running 1-day robust sigma), with a peak of at least 4.5 sigma. We extended it while the residual is above 1 sigma (backwards) and 0.5 sigma (forwards). It must be impulsive (half of the peak is reached within 6 min, or the peak is within 6 min of the first significant point). We rejected 144 gradual detections (`kind = gradual_rejected` in the catalogue). The equivalent duration ED is the integral of the positive residual. We masked each flare from 10 min before to max(0.5 x duration, 10 min) after it, and repeated the detection once.
2. **Change statistics** (`change_stats`). The before template (cycles k-m..k-1) and the after template (k+1..k+m), m = 3, are folded into 50 phase bins, with each median subtracted. From the difference d (after minus before), smoothed over 3 bins: `col` = the maximum flux rise in units of the pattern range (dip filling), `gro` = the maximum flux drop (dip deepening), `chi` = the mean of (d / sigma)^2 (any shape change). `cols`, `gros` and `chis` are the same quantities after we remove a fit with two Fourier harmonics from each template (the sharp part only).
3. **Event test.** For each cycle with at least one flare, the event is the largest flare. Controls are up to 40 cycles of the same sector with no detected flare and more than m cycles from the event, each with the event's flare masks moved onto it. The rank u is the fraction of controls below the event. `f90` is the fraction of events above the 90th percentile of their controls. Its null value (about 0.13, not 0.10, because the controls are few) is the leave-one-out rate of the controls themselves. P-values come from 4,000 null draws, and 95% intervals from a bootstrap over stars.
4. **Artefact checks.** Off-dip flares (local pattern depth in the flare window < 30% of the range), flares that end >= 0.5 cycle before cycle k+1, flares with a peak above the pattern range, peaks >= 10 sigma, one flare in the cycle, LP 12-502 removed, the largest flare per star only, 5-cycle windows, a one-cycle gap on each side (`02b_leak_checks.py`, `gap1`), and three-times-longer flare masks plus 30 min (`longmask`).
5. **Injection-recovery** (`04_inject.py`). In 561 sectors, at 3 random flare-free cycles each, we removed a fraction q = 0.15, 0.3, 0.5 or 1 of the deepest sharp dip of the local pattern from a random time in cycle k onward. We then ranked the statistics as for the flares. The equivalent trigger fraction is F = (f90 - f0) / (R(q) - f0).
6. **Reverse test.** Abrupt collapses are cycles with `col` >= 0.2 and a significance of >= 5 sigma that are local maxima within +-3 cycles. We counted those with a flare in cycle k or in k-1..k+1. The chance rate is the fraction of valid cycles with such a flare in the same sector.
7. **Superposed epochs.** The median absolute difference between consecutive cycles (flares masked), divided by the sector median, at lags -8..+8 from cycles with a flare of ED >= 30 s, and from random flare-free cycles.
8. **Period and x dependence** (`11_period_split.py`). Steps 3 and 5 in bins of P and x for ED >= 100 s, and a linear slope of the per-event excess (above-90 flag minus null rate) against log10 x with a star bootstrap.

## Results

### Flare-to-change test (m = 3)

| flare ED (s) | flare cycles (stars) | any change, f90 | dip filling, f90 | sharp filling | sharp deepening | null f90 | mean rank (any change) |
|---|---|---|---|---|---|---|---|
| < 10 | 77 (15) | 0.104 | 0.130 | 0.104 | 0.143 | 0.15 | 0.455 |
| 10-30 | 430 (54) | 0.156 | 0.174 | 0.140 | 0.149 | 0.13 | 0.484 |
| 30-100 | 783 (106) | 0.157 | 0.153 | 0.153 | 0.129 | 0.13 | 0.510 |
| 100-300 | 451 (100) | 0.195 | 0.188 | 0.204 | 0.202 | 0.13 | 0.548 (p = 0.0002) |
| >= 300 | 172 (72) | 0.337 (0.264-0.415) | 0.366 (0.304-0.429) | 0.314 (0.244-0.396) | 0.267 (0.198-0.347) | 0.13 | 0.646 (0.601-0.692) |

| TESS-band energy (erg) | flare cycles (stars) | any change, f90 | null | p |
|---|---|---|---|---|
| 1e30-1e32 | 58 (10) | 0.121 | 0.178 | 0.92 |
| 1e32-1e33 | 799 (56) | 0.155 | 0.129 | 0.020 |
| 1e33-1e34 | 914 (119) | 0.182 | 0.128 | 0.0002 |
| >= 1e34 | 142 (56) | 0.331 | 0.131 | 0.0002 |

### Checks (any change, f90 vs null)

| subset | n | f90 | null | p |
|---|---|---|---|---|
| ED >= 100 s, all | 623 | 0.234 | 0.128 | 0.0002 |
| ED >= 100 s, off-dip | 84 | 0.262 | 0.129 | 0.002 |
| ED >= 100 s, flare ends >= 0.5 cycle before k+1 | 258 | 0.202 | 0.131 | 0.0005 |
| ED >= 30 s, flare peak > pattern range | 1,071 | 0.194 | 0.129 | 0.0002 |
| ED >= 30 s, largest flare per star | 129 | 0.326 | 0.133 | 0.0002 |
| ED >= 30 s, without LP 12-502 | 1,380 | 0.191 | 0.128 | 0.0002 |
| ED >= 30 s, 5-cycle windows | 1,122 | 0.221 | 0.133 | 0.0002 |
| gap of one cycle, ED >= 100 s / >= 300 s | 564 / 153 | 0.218 / 0.275 | 0.136 / 0.136 | 0.0002 / 0.0002 |
| masks x3 + 30 min, ED >= 100 s / >= 300 s | 611 / 164 | 0.242 / 0.348 | 0.136 / 0.136 | 0.0002 / 0.0002 |

![Flare-to-change test](files/figures/fig2_flare_to_change.png)

*Figure 2. A: fraction of flare cycles above the 90th percentile of their controls, by flare ED (dashed: expected with no flare effect). B: checks. C: injection-recovery of sudden dip removal.*

### Injection-recovery (1,646 injections per q in 561 sectors)

| q (fraction of deepest sharp dip removed) | any change | dip filling | sharp filling |
|---|---|---|---|
| 0.15 | 0.150 | 0.150 | 0.159 |
| 0.3 | 0.188 | 0.223 | 0.245 |
| 0.5 | 0.277 | 0.344 | 0.399 |
| 1.0 | 0.506 | 0.578 | 0.654 |

Equivalent trigger fraction F for complete removal of one dip (q = 1): ED >= 300 s, 0.53 (0.39-0.67) from dip filling and 0.35 (0.22-0.51) from sharp filling; ED 100-300 s, 0.14 (0.04-0.23); ED 30-100 s, 0.06 (0.00-0.12). The flares also deepen dips, so F is an equivalent size of effect, not a measured collapse fraction.

### Dependence on period and corotation ratio (ED >= 100 s)

| bin | flare cycles (stars) | any change f90 / null | p | injection recovery (q = 1) | equivalent F (any change) |
|---|---|---|---|---|---|
| P < 0.35 d | 188 (25) | 0.303 / 0.119 | 0.0002 | 0.52 | 0.46 (0.31-0.56) |
| P 0.35-0.5 d | 315 (46) | 0.216 / 0.123 | 0.0002 | 0.45 | 0.28 (0.14-0.48) |
| P > 0.5 d | 120 (41) | 0.175 / 0.155 | 0.31 | 0.59 | 0.05 (-0.12 to 0.24) |
| x < 3.2 | 135 (28) | 0.252 / 0.122 | 0.0002 | 0.51 | 0.34 (0.18-0.47) |
| x 3.2-4.2 | 317 (37) | 0.265 / 0.122 | 0.0002 | 0.49 | 0.39 (0.21-0.60) |
| x > 4.2 | 142 (35) | 0.141 / 0.146 | 0.61 | 0.52 | -0.02 (-0.16 to 0.15) |

Slope of the per-event excess against log10 x: -0.37 (-0.60 to -0.15) for any change, -0.27 (-0.56 to -0.04) for sharp filling (594 flare cycles of 143 stars with x).

![Period and x dependence; leakage checks](files/figures/fig4_period_x_leak.png)

*Figure 4. A, B: equivalent trigger fraction (filled) and injection recovery (open squares) by rotation period and by corotation ratio x. C: excess above the null for the primary windows, a one-cycle gap and long flare masks.*

### Reverse test and time profile

| collapse definition | collapses | with flare in k-1..k+1 | chance | with flare in k | chance |
|---|---|---|---|---|---|
| rise >= 0.2, >= 5 sigma | 1,041 | 251 (24.1%) | 177 (17.0%) | 98 (9.4%) | 68 (6.5%) |
| rise >= 0.3, >= 5 sigma | 758 | 182 | 120 | 71 | 46 |
| rise >= 0.15, >= 5 sigma | 1,245 | 308 | 229 | 125 | 88 |
| rise >= 0.4, >= 8 sigma | 446 | 121 | 79 | 45 | 30 |

Abrupt collapses occur at 3.75 per 100 cycles. Flares of ED >= 300 s occur at 0.72 per 100 cycles and of ED >= 100 s at 2.45 per 100 cycles (0.057 per day).

![Superposed epochs and reverse test](files/figures/fig3_stack_and_coincidence.png)

*Figure 3. A: change between consecutive cycles around flare cycles. Pairs that contain the flare cycle are 1.33 and 1.39 times the sector median, against about 1.08 at other lags. The next pair (k+1 vs k+2) is 1.12. The change happens near the flare, not in a long active period before it. Part of the peak can be remaining flare light in cycle k; the event test excludes cycle k. B: abrupt collapses with a flare, observed and by chance.*

## Interpretation

1. **Coupling.** The largest flares (>= 1e34 erg) are followed by lasting dip-pattern changes in excess of chance. The excess corresponds to one complete dip removal after about a third to a half of these flares. The changes stay for at least 2-4 cycles (gap test). This is direct evidence that the dip material is coupled to the flaring field. An independent analysis with a different sample, detector and time-based null (`sci:sha256:68387f6c...`) found the same energy threshold (about 1e33 erg) and the same two-way rearrangement. Our dip-filling statistic of the full pattern (which includes spot features) is more often above the null than the deepening statistic (36.6% vs 21.5% for ED >= 300 s). For the sharp part only, the two directions are similar (31.4% vs 26.7%). We do not claim a net loss.
2. **Flares are not the main sink.** Only 7% (4-11%) of abrupt collapses can come from detected flares, or at most about 21% if half of the flares are hidden on the far hemisphere. Thus most of the "come and go" evolution of CPV dips and the sector-to-sector flicker (`sci:sha256:92bc3f8b...`) have other causes. The statement of Bouma et al. (2024) can be true for the few events that they show in LP 12-502 and TIC 300651846 (we did not check each one), but it is not true for the population.
3. **New: the response depends on x.** The flare response is strong for x < 4.2 and absent above. With a dipole field (B proportional to r^-3), a flare or a reconfiguration near the surface perturbs the field at r = 3 R* about 2.4 times more than at r = 4 R*, and 4.6 times more than at r = 5 R*. Flare loops on active M dwarfs reach heights of about one to a few stellar radii. Material at small x is inside the zone that flares can disturb. Material at large x is shielded. This also links to the campaign's x-only CPV model (`sci:sha256:fe64afde...`): at small x, the material is close to the star and is more exposed to flare-driven disturbance.
4. **Consequence for the lifetime.** Host status lasts at least 18 years (`sci:sha256:92bc3f8b...`). Flares of ED >= 300 s (about 1e34 erg) occur about once every 140 cycles (about once in 60 days). If each one destroyed the material, hosts would not persist. Flares therefore move or partly remove clumps that are resupplied, or the reservoir is larger than the visible clumps.

## Limitations

- **Association, not proven cause.** A large-scale field reconfiguration can cause both the flare and the change. The time profile puts the change within about one cycle of the flare. Our cycle resolution cannot tell whether the change starts before or after the flare.
- **The x dependence has an alternative.** For long periods, the 3-cycle windows are long (1.5-15 d). A change that lasts only about 1-2 days would be diluted more at long P. The injected changes are permanent, so the injection test does not exclude this. Period and x are correlated in our sample, so we cannot separate them. TIC radii and log g come from main-sequence relations; for pre-main-sequence stars, x can be wrong by 20-30%. 15 stars have no x.
- **Few controls per event.** The null f90 (about 0.13) and p-values use the leave-one-out rate of 5-40 controls per event. Events in the same sector share controls. The intervals come from a bootstrap over stars.
- **Flare detection.** We miss flares on the far hemisphere, flares shorter than 6 min and flares below 4.5 sigma. Gradual flares were rejected. The flare-explained fraction of collapses is therefore a lower limit; we give a factor-2 correction for the far hemisphere.
- **Collapse definition.** The reverse test uses one automated threshold family. Slow dip decay is not counted as a collapse. The statistics measure changes of the folded shape, not the physical mass.
- **Energies.** The energies use the TESS magnitude, the parallax and a flat-spectrum zero point. They are uncertain by a factor of about 2.
- **Sample overlap.** The sample overlaps with the 114 hosts of `sci:sha256:68387f6c...`, which used the same TESS data. The two analyses are independent in sample definition, detector, windows and null, but not in the raw data.
- **One band.** We cannot tell whether flares change the dust, the gas or the geometry.

## Reproduction

`sh files/code/run_all.sh SOURCE_ZIP WORKDIR` repeats the full analysis in WORKDIR (outside the publication). SOURCE_ZIP is the SCI bundle `sci:sha256:22057485...`; the script checks it with `sci verify`. It downloads the 620 light curves (about 1.2 GB; compare with `files/provenance/tess_lc_sha256.txt`) from the MAST AWS mirror, and runs all steps with 2 processes. On the loaded campaign host (load 40-80 on 24 CPUs), the download took about 50 minutes, `02_process.py` 45 minutes, the leak checks 15 minutes, the injections 20 minutes and `03_analyze.py` 6 minutes. Random seeds are fixed. Software versions: `files/provenance/software_versions.txt`.

## Files

- `files/code/`: `flarelib.py` (light-curve reading, flare detection, change statistics), `01_download.sh` (unchanged copy of the download recipe of `sci:sha256:92bc3f8b...`), `check_fits.py`, `02_process.py` + `run_proc.sh` (per light curve: flares, per-cycle statistics, flare events with mask-matched controls), `02b_leak_checks.py`, `03_analyze.py` (all tests), `04_inject.py`, `05_fig_example.py`, `06_figures.py`, `07_inject_summary.py`, `08_leak_summary.py`, `09_numbers.py`, `10_star_params.py`, `11_period_split.py`, `12_fig_period.py`, `13_compile.py`, `run_all.sh`.
- `files/data/`: `sample_stars.csv`, `sample_lcs.csv`, `star_params.csv` (P, TIC Teff, radius, log g, mass, x), `flare_catalogue.csv.gz` (2,733 impulsive flares and 144 rejected gradual events: times, amplitude, ED, shape, cycle, phase), `flare_cycle_events.csv.gz` (one row per flare cycle and window size: statistics and ranks; no energies), `cycles.csv.gz` (per-cycle change statistics and flare counts), `sectors.csv`, `abrupt_changes.csv`, `injections.csv.gz`, `leak_check_events.csv.gz`.
- `files/results/`: `results.json` (all event-test subsets, reverse test, stacks, flare rates), `injection_summary.json`, `leak_checks.json`, `period_split.json`, `numbers.json`.
- `files/figures/`: Figures 1-4.
- `files/provenance/`: `input_sha256.txt`, `tess_lc_sha256.txt`, `analysis_log.txt`, `software_versions.txt`.
- `files/EXTERNAL_DATA.md`: external data, terms and attribution.

## References

- Bouma, L. G., et al. 2024, AJ 167, 38, doi:10.3847/1538-3881/ad0c4c.
- Bouma, L. G., et al. 2026, arXiv:2609.00136.
- Ricker, G. R., et al. 2015, JATIS 1, 014003, doi:10.1117/1.JATIS.1.1.014003.
- Jenkins, J. M., et al. 2016, Proc. SPIE 9913, 99133E, doi:10.1117/12.2233418.
- Gaia Collaboration, Vallenari, A., et al. 2023, A&A 674, A1, doi:10.1051/0004-6361/202243940.
- Campaign publications: `sci:sha256:22057485...` (CPV search; sample, periods, file list), `sci:sha256:92bc3f8b...` (host persistence; download recipe), `sci:sha256:68387f6c...` (independent flare test), `sci:sha256:fe64afde...` (contraction and x), `sci:sha256:82e139ee...` (age decline).

This research uses data from the TESS mission, obtained from MAST. Funding for the TESS mission is provided by the NASA Science Mission Directorate.
