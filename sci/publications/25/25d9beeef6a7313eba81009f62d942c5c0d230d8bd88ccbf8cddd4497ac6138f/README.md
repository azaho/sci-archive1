# Published superoutburst ephemerides of SU UMa dwarf novae do not predict the 2021-2025 superoutbursts

Job sci-1107-dell-astronomy-48d7b27cf838 · topic astronomy · machine dell · campaign 11_07_2026 · account claude-andrii · model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

SU UMa dwarf novae have long, bright "superoutbursts" that repeat at a supercycle C_so. Vogt et al. (2021, MNRAS, doi:10.1093/mnras/staa3711, arXiv:2101.02756) gave linear ephemerides T_max = T0 + E x C_so for 206 SU UMa stars. They found that the superoutburst times stay within about 7 percent (median 9.1 percent) of the cycle from a straight line, and they called this a "pronounced quasi-periodic repeatability". They gave the table so that other workers can extend it.

We ask two questions:

1. Do these ephemerides predict the superoutbursts that occurred after the paper (2020-12-18 to 2025-10)?
2. If not, is the cause a wrong period, or a supercycle that does not keep its phase (a "renewal" process, in which each superoutburst resets the disk and the next interval does not depend on older events)?

The second question has physical importance. In the thermal-tidal instability model, a superoutburst removes mass from the disk and makes the disk smaller. The next superoutburst starts when the disk again grows to the 3:1 resonance radius. This model gives a renewal process, not a fixed clock.

## 2. Data

All data are public. We did not put raw light curves in this package (see `files/provenance/EXTERNAL_DATA_NOTICE.md`).

| Source | Use | Version / access |
| --- | --- | --- |
| ZTF public data release light curves, IRSA API (`nph_light_curves`, 3 arcsec cone, g and r) | quiescent level, outburst detection 2018-03 to 2025-10 (last epoch MJD 60969) | release served by IRSA on 2026-11-09 |
| ASAS-SN Sky Patrol v2 (`pyasassn` 0.6.21, `master_list` catalogue, V 2012-2018 and g 2017-2025) | outburst detection, mostly before ZTF | queried 2026-11-09 |
| Vogt et al. 2021, Table 1 (T0, C_so, errors, O-C, N, Delta T) | ephemerides under test | parsed from the arXiv v1 LaTeX source (`src.tgz` SHA-256 `dec266c3...4995`) |
| Otulakowska-Hypka, Olech & Patterson 2016 (VizieR J/MNRAS/460/2526/table2) | target list of SU UMa stars with positions and amplitudes | CfA VizieR mirror, `table2.tsv` SHA-256 `9613a483...2a17` |

Targets: 392 SU UMa-class stars (types SU, ER, WZ) north of declination -31 deg from the 2016 catalogue, plus 50 Vogt stars not in that catalogue (442 in total). We matched 156 Vogt stars to the catalogue by position (< 15 arcsec). We fixed one typo in the Vogt LaTeX table (HO Del declination "+14 0310" -> "+14 03 10"). SHA-256 values of every raw input file that we used are in `files/provenance/raw_input_sha256.txt`.

## 3. Method

### 3.1 Outburst detection (code/03_outbursts.py)

1. ZTF: we keep object IDs within 1.2 arcsec of the mean position of the IDs that show outbursts (at least 3 points 1.5 mag brighter than their median). The quiescent reference of each ID is its 75th-percentile magnitude.
2. Threshold: a first pass at 1 mag above quiescence gives the typical peak amplitude A (median of the 3 brightest ZTF episodes). The final outburst threshold is max(1, A - 2) mag above quiescence. Thus a night is "bright" only when the star is within about 2 mag of its typical superoutburst peak.
3. ASAS-SN: we use forced-aperture fluxes. A point is bright when the flux above the 25th-percentile baseline (per camera and filter) is more than the threshold flux and more than 5 sigma. A point is "faint" only when the 5-sigma limit is within 0.5 mag of the threshold. We reject ASAS-SN data when the baseline flux is brighter than the threshold (blend with a neighbour star).
4. Nights with data from both surveys are combined. An episode is a run of bright nights with gaps of 4 d or less. A "superoutburst" has an observed bright span of 6 d or more. A "normal" outburst has a span with its bracketing gaps of 6 d or less. All other episodes are "ambiguous". Superoutburst episodes less than 30 d apart are one event (a dip or a rebrightening). The event time is the first bright night + 1 d (the approximate time of maximum).
5. ZTF data are necessary for each star. 285 of 442 targets have usable ZTF data.

### 3.2 Quality cut (code/03b_quality.py)

Before the forecast comparison we set a light-curve quality cut: bright-night fraction < 0.25 (stars with very frequent normal outbursts can merge normal outbursts into a false superoutburst), threshold >= 2 mag (high contrast), and quiescent scatter < 0.15 of the threshold (no strong blend). 166 stars pass. These stars give the primary results. The results without the cut are also in `results.json` (keys ending in `_all`). They agree.

### 3.3 Checks of the detections

- Cross-survey check (code/05_crossval.py): for episodes that one survey calls a superoutburst, and where the other survey has at least 3 nights in the same interval, the other survey calls it a superoutburst 208 times (ZTF reference) and 200 times (ASAS-SN reference). It calls it ambiguous (because of gaps) 135 and 106 times. It calls it a normal outburst 0 times. It finds no episode 6 and 1 times.
- Visual check: code/13_vet_sheets.py makes 8 contact sheets of the 2018-2025 light curves of the 78 quality-cut Vogt stars that have post-2020 events. We inspected 4 sheets (40 stars). In these stars the detected superoutbursts are long, bright outbursts. We did not inspect the other 38 stars. Some real superoutbursts are missed in seasonal gaps. Missed events do not bias the phase test.
- In-sample control: for superoutbursts inside the time span that Vogt et al. used, their ephemerides fit our event times (see 4.1). A placebo that uses the ephemeris of a different star with similar C_so (+-20 percent) gives mean cos = 0.00 (95th percentile of 200 placebos 0.20).

### 3.4 Forecast test (code/06_vogt_forecast.py, code/11_stats_figures.py)

For each event after 2020-12-18 (after the paper appeared) we calculate the phase error phi = (t - T0 - E C_so)/C_so with E the nearest integer, so phi is in [-0.5, 0.5). The statistic is the mean of cos(2 pi phi). A uniform phase gives 0. A perfect forecast gives 1. We give 95 percent ranges from a bootstrap over stars. For comparison, we calculate the value that the Vogt error model expects, exp(-2 pi^2 sigma^2), with sigma^2 = sigma(T0)^2 + (E sigma(C_so))^2 + (O-C)^2, in cycle units.

### 3.5 Self-forecast control (code/08_self_forecast.py)

We fit our own linear ephemeris to our superoutbursts before 2020-12-18 (at least 4 events, cycle counts from a coverage-aware rule that takes the longest period that every interval allows; an implied missed event must fall in a data gap of 10 d or more, or on an ambiguous episode). Then we predict the events after that date.

### 3.6 Renewal simulation (code/10_renewal_sim.py)

For each Vogt star (its N, Delta T and C_so) we simulate intervals from Normal(C, sC) (memoryless), observe N events that include the first and last cycle, and fit a line with the TRUE cycle counts (best case for the observer). We record the in-sample rms(O-C)/C and the phase error of the next 1 to 12 events. A "clock" model (fixed period, 3 percent timing jitter, s = 0) is the comparison. 20 repeats per star and per s.

## 4. Results

### 4.1 Main result: no forecast skill after 2020

| Set (quality cut) | Events | Stars | mean cos(2 pi phi) | 95% range | Expected from Vogt error model |
| --- | --- | --- | --- | --- | --- |
| Inside the Vogt data span (control) | 31 | 18 | 0.64 | 0.41 to 0.86 | 0.62 |
| After their data, before 2020-12-18 | 175 | 80 | -0.02 | -0.14 to 0.09 | 0.52 |
| After 2020-12-18 (forecast test) | 197 | 78 | 0.02 | -0.08 to 0.14 | 0.43 |
| After 2020-12-18, no quality cut | 343 | 119 | 0.03 | -0.05 to 0.12 | 0.41 |

The ephemerides fit the events inside their own data span as well as their error model expects. After their data end, the phase errors are uniform (Fig. 2). The fraction of events within 0.15 cycle of the forecast is 0.31; a uniform phase gives 0.30. The median forecast distance is 7.7 cycles after the last Vogt event. No subgroup keeps skill: N <= 5 (0.03), N >= 6 (0.02), N >= 9 (-0.08), C_so < 200 d (-0.10), 200-500 d (0.02), >= 500 d (0.08), O-C/C_so < 0.05 (0.08), events with span >= 10 d (-0.02). All 95 percent ranges include 0.

Fig. 1 shows examples. VW CrB has clear superoutbursts about every 350-410 d in 2021-2025, but the ephemeris has C_so = 724 d. BG Ari repeats at about 390-400 d, not 236 d. HO Del repeats at about 230-450 d, not 823 d. Thus some published periods are wrong by a factor near 2 or more.

### 4.2 Our own ephemerides also fail

Ephemerides that we fit to our 2013-2020 data (29 quality-cut stars, 112 later events) also give no skill: mean cos 0.00 (-0.15 to 0.18). For events less than 2 cycles after the last fitted event the value is 0.11 (-0.22 to 0.43, 23 events). Thus wrong published periods are not the only cause. Our training data before 2018 are sparse (ASAS-SN only), so our cycle counts can also be wrong.

### 4.3 A renewal process explains the published residuals and the forecast failure

| Interval scatter s | Simulated median in-sample rms(O-C)/C | mean cos, 1 cycle ahead | 4 cycles | 8 cycles |
| --- | --- | --- | --- | --- |
| 0 (clock, 3% jitter) | 0.022 | 0.97 | 0.94 | 0.89 |
| 0.05 | 0.033 | 0.90 | 0.69 | 0.43 |
| 0.10 | 0.069 | 0.67 | 0.23 | 0.05 |
| 0.125 | 0.084 | 0.53 | 0.11 | 0.00 |
| 0.15 | 0.101 | 0.42 | 0.03 | -0.01 |

The published median rms(O-C)/C_so is 0.091. A memoryless process with interval scatter s of about 0.12-0.14 gives this value, even when the observer knows the true cycle counts (Fig. 4). The same process predicts mean cos near 0.1 at 4 cycles and near 0 at 8 cycles. This agrees with the observed values (Fig. 3). A fixed clock with the published residuals predicts 0.4-0.9, and the data reject it. Thus the small in-sample residuals do not show that the superoutburst times keep a long-term phase.

Fully covered consecutive intervals (no data gap >= 10 d, no ambiguous episode between two superoutbursts) exist mostly for short-cycle, active stars. In 11 such stars the interval coefficient of variation has a median of 0.075 (range 0.055-0.17). For 17 adjacent interval pairs in 6 stars, the lag-1 correlation is 0.12 (95 percent range -0.25 to 0.66). A clock with timing jitter predicts -0.5. This sample is small, and the short-cycle stars mostly fail the quality cut, so this test is weak. It agrees with a renewal process.

## 5. Interpretation

1. The Vogt et al. (2021) linear ephemerides do not predict superoutbursts after 2020. Users should not use them to schedule observations more than about one cycle ahead.
2. Two causes contribute: (a) some periods are aliases (examples above); (b) even with correct periods, a memoryless supercycle with 10-15 percent interval scatter removes the phase memory within about 4-8 cycles. A typical forecast distance of 8 cycles is enough to remove all skill.
3. The result agrees with the thermal-tidal instability model, in which each superoutburst resets the disk. "Quasi-periodic" is correct for the interval lengths. It is not correct for long-term phase.

## 6. Limitations

- Superoutburst detection uses survey cadence (ZTF 2-3 d, ASAS-SN about 1-3 d). Some superoutbursts are missed in gaps. The event time (first bright night + 1 d) has an error of a few days, which is small relative to C_so (median 430 d).
- The quality cut removes stars with very frequent outbursts (ER UMa-like stars). We do not test their ephemerides in the primary set. The full set gives the same result.
- The interval-scatter value s comes from a simulation that matches only the median residual. It does not use the individual Vogt epochs (most are only in the online journal table, which we did not use). The lag-1 test has low power.
- The supercycle values in `files/derived/supercycles.csv` come from an automatic rule ("longest allowed period"). Many have alias flags (`alias=True`). Do not use them as a catalogue without a visual check.
- ZTF covers only declination > -31 deg. The 24 southern targets are not analysed.
- ZTF and ASAS-SN light curves change with new releases. The SHA-256 list records the exact files we used. A new download can differ.

## 7. Reproduction

```
bash files/code/00_get_data.sh /path/to/scratch     # downloads into scratch, never into this package
bash /path/to/scratch/code/run_analysis.sh /path/to/scratch
```

Python 3.12.16 with numpy 2.5.4, pandas 3.1.1, matplotlib 3.11.2, astropy 8.0.2; `pyasassn` from github.com/asas-sn/skypatrol (0.6.21). Run time: downloads about 3 h (IRSA is slow), analysis about 8 min. The simulation uses a fixed random seed.

## 8. Files

- `files/results/results.json`: all statistics in this text.
- `files/results/vogt_phase_all_events.csv`: each detected superoutburst of a Vogt star, its phase error, cycles since the last Vogt event, and group (in / between / post).
- `files/results/renewal_sim_summary.csv`: simulation summary.
- `files/results/fig1-fig4*.png`: figures.
- `files/derived/episodes*.csv`: our outburst catalogue (combined, ZTF only, ASAS-SN only): start, end, span, peak (ZTF, mag relative to quiescence), class.
- `files/derived/objects.csv`, `quality.csv`: per-star status, threshold, quality metrics.
- `files/derived/supercycles.csv`: automatic supercycle estimates (see limitations).
- `files/derived/cv.csv`, `iv.csv`, `sf_*.csv`: cross-survey check, intervals, self-forecast.
- `files/code/`: all code. `files/provenance/`: input hashes and external-data notice.
