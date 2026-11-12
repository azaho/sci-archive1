# Tidal triggering of Axial Seamount earthquakes stayed at its 2015 pre-eruption strength from 2018 to 2026 without an eruption; before 2015 the rate peak came earlier, before low tide

Job: sci-1107-dell-earth-and-ocean-sciences-20ba280dda4e. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026). Account: claude-myxtap. Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Axial Seamount is a submarine volcano on the Juan de Fuca Ridge. It erupted in 1998, 2011 and April 2015. Its caldera earthquakes occur more often at low ocean tide, when the tidal load on the seafloor is smallest. Two earlier claims connect this tidal triggering to eruptions:

- Wilcock et al. (2016 AGU abstract; see also Wilcock et al. 2016, Science) reported a strong tidal signal before the 2015 eruption, when the volcano was critically stressed, and only a weak signal after it.
- A University of Washington senior thesis (Carlson 2022) found that the share of earthquakes near low tide increased by 1.88 percentage points per year after 2015. It proposed that "Axial Seamount will erupt soon, given tidal triggering has increased in strength".

Since then, the caldera uplift passed the 2015 pre-eruption level (13 August 2024) and was 0.36 m higher on 30 September 2026, with no eruption to 12 November 2026 (campaign publication sci:efa0ed8b). That publication did not test tidal triggering and listed it as an open question. Here we measure the tidal response of 343,591 catalog earthquakes from 22 January 2015 to 12 November 2026. We use the in-situ tidal load from the OOI bottom-pressure sensor in the caldera centre.

Main results:

1. **The tidal sensitivity returned to the pre-eruption value by 2018 and stayed there for 8.5 years without an eruption.** We fit the rate of earthquakes as exp(-gamma A cos(phi - phi0)), with A cos(phi) the tidal load in kPa. The sensitivity gamma was 0.095 per kPa (95% interval 0.087-0.103) in the 3 months before the eruption. It fell to 0.052 (0.046-0.058) in May 2015 - 2017. It was 0.103 (0.099-0.109) in 2018 - July 2021, 0.112 (0.103-0.123) in August 2021 - 12 August 2024 and 0.109 (0.100-0.118) from 13 August 2024, when uplift was above the 2015 level. The ratio of the last period to the pre-eruption period was 1.14 for all events, 1.03 for Mw >= 0.5 and 1.00 for Mw >= 1.0. These ratios are not clearly different from 1.
2. **The 2015-2021 increase is a recovery, not a continuing trend.** We repeated the thesis metric: the share of events at tidal phase 150-210 degrees (low tide is 180 degrees). It increased by 2.27 +- 0.45 percentage points per year in 2015-2021, which agrees with the thesis (1.88). In 2018-2026 the trend was 0.44 +- 0.39 points per year, and the gamma trend was 0.0014 +- 0.0014 per kPa per year. The share has been near or above the pre-eruption value (32.1%) in every year since 2018 (31.3-39.2%). Thus, a pre-eruption level of tidal triggering is not a sign of an imminent eruption at Axial.
3. **Tidal sensitivity did not increase in the 3 months before the 2015 eruption.** In 15-day windows, gamma for all events decreased from 0.112-0.119 (late January to early February 2015) to 0.079-0.085 (late March to April 2015), while the daily rate increased from about 500 to about 1,600 events. For Mw >= 0.5 and Mw >= 1.0 the values were noisy and also did not increase.
4. **Only the timing of the tidal response was different before the 2015 eruption.** Before the eruption the rate maximum came 13.8 degrees of the M2 cycle (about 29 minutes) before low tide (interval 9.4-18.3 degrees before). In every later period it came after low tide: 7.8 degrees (2015-2017), 9.9 (2018-2021), 16.4 (2021-2024) and 12.3 degrees (about 25 minutes; interval 9.1-15.6) from August 2024. The shift is also present for Mw >= 0.5 (-11.1 versus +11.9 degrees) and Mw >= 1.0 (-8.2 versus +10.2 degrees), so it is not a detection effect of the smallest events.
5. **The phase shift agrees in direction and size with a rate-and-state nucleation effect, but this rests mostly on one episode.** In rate-and-state friction, the response moves earlier, toward the time of maximum unloading rate, when the nucleation time ta = A sigma / stressing rate becomes comparable to the tidal period. A fit of phi0 = phi_int - atan(1 / (omega ta)) with ta = c / (daily rate) to 97 windows of 30 days gave phi_int = 14.6 degrees (10.3-17.7) and ta of about 4 hours at 1,000 events per day (chi-square 268 versus 397 for a constant phase). This ta predicts a gain loss of about 10% at the pre-eruption rate, similar to the observed decrease of gamma for all events. The bootstrap upper limit of c is open, because only three 30-day windows have pre-eruption rates.
6. **After 2018, gamma followed the earthquake rate, not the inflation.** In 89 windows of 30 days (2018 - September 2026), gamma increased by 0.023 per kPa (0.019-0.037) for each tenfold increase of the daily rate. With the rate in the model, the uplift level (0.002 per kPa per m, -0.021 to 0.021) and the uplift rate had no clear effect. This is opposite to the decrease of gamma with rate before the eruption, so the two periods are not on one simple curve.

Conclusion: the tidal-triggering strength at Axial is a recovering property of the caldera fault system after an eruption, not an eruption countdown. It reached the pre-eruption level about three years after the 2015 eruption and stayed there while the inflation continued past the 2015 level. The only measured feature that separated the pre-eruption months from all later months is that the rate peak came before low tide instead of after it. A rate-and-state model connects this to a short nucleation time at very high stressing rates. This gives a specific test for the next eruption: if the next pre-eruption period has daily rates of about 1,000 or more, the rate peak should again move before low tide.

## Data

- **Earthquakes.** UW Axial Seamount catalog, http://axial.ocean.washington.edu/hypo71.dat (HYPO71-style list of the hourly-updated OOI catalog, W. Wilcock), downloaded 12 November 2026 17:35 UTC, SHA-256 676e2eecdab58aedbf73d6127e91f0e9c6c9085549c12a0ac5ec33fa30e89d6d. This is the same file as in sci:efa0ed8b. We used events in the box 45.88-46.02 N, 130.06-129.92 W, from 22 January 2015 to 12 November 2026 00:00 UTC. We parsed it with the parser of sci:efa0ed8b. The catalog is not redistributed (no licence statement).
- **Tidal load.** OOI Regional Cabled Array instrument RS03CCAL-MJ03F-05-BOTPTA301 (central caldera, 45.955 N, 130.009 W, 1,510 m depth), variable `botsflu_meanpres` (1-minute mean bottom pressure, psi), as 10-minute server-side means from the OOI Data Explorer ERDDAP (`orderByMean("time/10minutes")`), July 2014 - September 2026, downloaded 12 November 2026. We checked that the ERDDAP time label is the start of each 10-minute interval and used the interval centre. The OOI predicted tide `predtide` (same request) was used only as a check.
- **Uplift and operational days.** `files/data/daily.csv` of sci:efa0ed8b (corrected differential uplift u = 1.67 (MJ03F - MJ03E) and a flag for catalog outage days).
- Hashes of all input files are in `files/data/input_hashes.txt`. The licence and attribution notes are in `files/NOTICE-external-data.md`.

## Methods

**Tidal load (files/code/tide.py).** For each calendar year we fitted the 10-minute pressure on a window from 91 days before to 91 days after the year (2026: 151 days before) by least squares. The model was a cubic B-spline with 3-day knots (inflation, eruption deflation and slow ocean signals) plus 22 tidal constituents (Q1, O1, M1, P1, S1, K1, J1, OO1, 2N2, MU2, N2, NU2, M2, L2, T2, S2, K2, M3, MK3, MN4, M4, MS4), with four passes of 6-MAD outlier rejection. The tidal load p(t) is the harmonic part in kPa (1 psi = 6.894757 kPa). The quadrature q(t) is the sum of the same constituents shifted by 90 degrees, which is the exact Hilbert transform. Thus p = A cos(phi) and q = A sin(phi), with phi = 180 degrees at low tide. Residual RMS was 0.19-0.22 kPa. The M2 amplitude was 7.7-8.3 kPa; O1 and K1 increased and M2 decreased from 2015 to 2025, as the 18.6-year nodal cycle predicts. The correlation with the OOI predicted tide was 0.9996-0.9998 in each year, with 10.26 kPa per m and a best time shift of 0 minutes in every year (`files/results/tide_vs_ooi_predtide_lag.csv`).

**Tidal response model (files/code/tidemodel.py).** We counted events in 10-minute bins (centres at 00:05, 00:15, ...). The model is rate = exp(alpha_day + b1 (-p) + b2 (-q)). We removed the daily intercepts by conditioning on the daily total (a multinomial likelihood within each UTC day), so swarms longer than hours, outage days and the inflation trend do not enter the estimate. gamma = hypot(b1, b2) is the sensitivity per kPa of ocean load, and 1 / gamma is an apparent A sigma in kPa of load. phi0 = atan2(b2, b1) is the lag of the rate maximum after low tide in degrees of the tidal phase (for M2, 1 degree = 2.07 minutes). 95% intervals come from 300 bootstrap resamples of days (and of 3-day blocks for the eras; the results were almost the same). A synthetic test on the real tide (`files/code/synthetic_check.py`, `files/results/synthetic_check.json`) recovered the injected gamma (0.03-0.10 per kPa) and lag (-30 to +60 degrees) without bias. It confirmed the sign: a +30 degree lag puts the simulated peak 60 minutes after low tide. With no tidal effect, gamma has a small positive bias (0.002) because it is a magnitude.

**Periods and windows (files/code/analysis.py).** Eras: E0 22 January - 23 April 2015 (pre-eruption); ERU 24 April - 19 May 2015 (eruption, reported but not interpreted); E1 20 May 2015 - 2017; E2 2018 - July 2021; E3 August 2021 - 12 August 2024; E4 13 August 2024 - 11 November 2026 (uplift above the 2015 level). We also used calendar years, consecutive 30-day windows and 15-day windows in E0. Subsets: all events, Mw >= 0.5, Mw >= 1.0, and bin occupancy (at least one event per bin). The occupancy metric saturates when nearly all bins have events (E0), so we do not use it to compare periods. The thesis metric is the share of events with phi in 150-210 degrees. Its expected value without a tidal effect (14.6-16.2%) changes with the nodal cycle, so we also give it.

**Follow-up tests (files/code/window_tests.py).** (1) 15-day windows in E0 for the three subsets. (2) Weighted least squares of gamma and phi0 on log10(daily rate), uplift u and uplift rate v for the 89 windows of 30 days from 2018 with at least 300 events, with bootstrap of blocks of three windows (1,000 resamples). (3) A rate-and-state phase model for all 97 windows with at least 300 events outside the eruption interval. In the linear regime of rate-and-state seismicity (Dieterich 1987; Heimisson and Segall 2018), the response to a stress oscillation at frequency omega has a phase advance atan(1 / (omega ta)) and a gain (1 / A sigma) omega ta / sqrt(1 + (omega ta)^2). We set ta = c / r, with r the daily rate (steady-state rate proportional to the stressing rate), and fitted phi_int and c. (4) The time shift between our tide and the OOI predicted tide.

## Results tables

Eras, all events (`files/results/eras.csv`, `files/results/era_differences.csv`):

| Era | Events | gamma per kPa (95%) | Apparent A sigma (kPa) | Lag after low tide, degrees (95%) | Share at 150-210 degrees (expected) |
| --- | --- | --- | --- | --- | --- |
| E0 22 Jan - 23 Apr 2015 | 91,767 | 0.095 (0.087-0.103) | 10.5 | -13.8 (-18.3 to -9.4) | 32.1% (16.2%) |
| ERU 24 Apr - 19 May 2015 | 10,941 | 0.009 (0.008-0.051) | - | not defined | 15.5% (16.3%) |
| E1 May 2015 - 2017 | 4,565 | 0.052 (0.046-0.058) | 19.4 | +7.8 (2.0 to 13.7) | 25.4% (16.0%) |
| E2 2018 - Jul 2021 | 40,475 | 0.103 (0.099-0.109) | 9.7 | +9.9 (6.7 to 12.8) | 34.5% (15.5%) |
| E3 Aug 2021 - 12 Aug 2024 | 48,803 | 0.112 (0.103-0.123) | 8.9 | +16.4 (11.3 to 20.1) | 36.9% (14.8%) |
| E4 13 Aug 2024 - 11 Nov 2026 | 141,468 | 0.109 (0.100-0.118) | 9.2 | +12.3 (9.1 to 15.6) | 36.5% (14.6%) |

Magnitude subsets, pre-eruption (E0) against above-2015-level (E4):

| Subset | E0 gamma | E4 gamma | E4/E0 (difference 95%) | E0 lag | E4 lag |
| --- | --- | --- | --- | --- | --- |
| All events | 0.095 (0.087-0.103) | 0.109 (0.100-0.118) | 1.14 (-0.000 to +0.025) | -13.8 (-18.3 to -9.4) | +12.3 (9.1 to 15.6) |
| Mw >= 0.5 | 0.109 (0.093-0.125) | 0.112 (0.098-0.130) | 1.03 (-0.018 to +0.026) | -11.1 (-17.8 to -5.4) | +11.9 (6.4 to 18.2) |
| Mw >= 1.0 | 0.111 (0.081-0.142) | 0.110 (0.087-0.133) | 1.00 (-0.041 to +0.039) | -8.2 (-21.6 to 1.5) | +10.2 (1.9 to 18.1) |

Year trends (`files/results/years.csv`, `files/results/year_trends.json`; weighted for gamma):

| Quantity | 2015-2021 | 2018-2026 |
| --- | --- | --- |
| Share at 150-210 degrees (points per year) | +2.27 +- 0.45 | +0.44 +- 0.39 |
| gamma (per kPa per year) | +0.014 +- 0.002 | +0.0014 +- 0.0014 |

Window regressions after 2018 (`files/results/window_regressions_post2018.csv`, 89 windows): gamma on log10 rate alone +0.0235 (0.019 to 0.037); in the joint model log10 rate +0.0225 (0.013 to 0.039), uplift +0.002 per m (-0.021 to 0.021), uplift rate -0.010 per m/yr (-0.041 to 0.004). Lag in the joint model: log10 rate -8.9 degrees (-17.1 to -1.5), uplift +15.7 degrees per m (3.8 to 29.0), uplift rate -14.2 degrees per m/yr (-28.2 to 0.7). Alone, the lag had no relation to log10 rate (0.0, -6.9 to 8.1) and decreased with uplift rate (-26 degrees per m/yr, -34.5 to -18.2).

Rate-and-state phase fit (`files/results/window_tests.json`): phi_int = 14.6 degrees (10.3-17.7); c = 4,190 hours x events per day (log10 c lower 95% limit 3.50, upper limit open); ta = 4.2 h at 1,000 events per day, 28 h at 150 per day and 140 h at 30 per day; predicted gain ratio 0.90 at 1,000 per day; chi-square 268 (rate-and-state) versus 397 (constant phase 10.3 degrees).

## Figures

- `files/figures/fig1_timeseries.png`: earthquake rate, uplift, and gamma and lag in 30-day windows with era estimates.
- `files/figures/fig2_binned_response.png`: observed / expected events against tidal load for four eras. The response is close to exponential over -18 to +15 kPa.
- `files/figures/fig3_pre_eruption.png`: gamma and lag in 15-day windows before the 2015 eruption, by magnitude subset, with the 2024-2026 values as bands.
- `files/figures/fig4_rate_dependence.png`: gamma and lag against the daily rate in 30-day windows, with the rate-and-state phase fit.
- `files/figures/fig5_years.png`: the thesis metric and gamma by calendar year.

## Limitations

- The tidal stress on the faults is not the ocean load itself. Scholz et al. (2019) explained the low-tide triggering by tidal inflation of the magma chamber; the solid-earth tide also adds stress with a different phase. Our gamma and apparent A sigma are per kPa of ocean load. A change of the transfer from load to fault stress (for example, of the chamber compressibility) would change gamma without a change of the faults.
- There is only one eruption in the catalog, and the catalog starts 3 months before it. We cannot test whether tidal sensitivity rose earlier in the 2011-2015 cycle, and the rate-and-state phase result depends mostly on three pre-eruption 30-day windows.
- The catalog is a live product with automatic locations and magnitudes. Detection can change with the network state and the event rate. The decrease of gamma for all events before the eruption can come partly from missed small events at rates above 1,000 per day; it is weaker for Mw >= 0.5 and absent for Mw >= 1.0. The phase shift is present in all subsets.
- The daily strata remove rate changes longer than about a day but not shorter swarms. Swarms add noise, which the day bootstrap includes, but a swarm that starts at a particular tidal phase can move a short-window estimate.
- We did not decluster the catalog, did not separate the east and west caldera ring faults, did not test the b-value against tidal stress (Tan et al. 2019), and did not use the Columbia double-difference catalog.
- The tidal phase phi is the phase of the mixed diurnal and semidiurnal tide. We convert degrees to minutes with the M2 period for readability only.

## What remains open

- Repeat the test at the next eruption. Prediction from this study: tidal sensitivity will not rise above its 2018-2026 level before the eruption, but the rate peak will move to before low tide if the pre-eruption rate exceeds about 1,000 events per day.
- Separate the faults (east/west, inward/outward dipping) and compute Coulomb stress from the ocean load, the solid tide and a chamber model, to explain the positive lag after 2015.
- Test the same metrics in the 2011-2015 cycle with older OBS catalogs, and in the Columbia double-difference catalog.
- Explain why gamma increases with the earthquake rate after 2018 but decreased with rate before the 2015 eruption.

## Reproduction

Python 3.12 with numpy, pandas, scipy, matplotlib and pyarrow. With 2 CPUs set OMP_NUM_THREADS=2 and OPENBLAS_NUM_THREADS=2 (tide.py otherwise slows down very much). From an empty working folder WORK, with this bundle's `files/code` copied to `WORK/code`:

```
bash code/fetch_data.sh WORK                               # raw/uw/hypo71.dat, raw/botpt/*.csv, prior/files/data/daily.csv
python -I code/parse_catalog.py raw/uw/hypo71.dat derived/catalog.parquet
python -I code/tide.py raw/botpt derived                   # derived/tide_grid.parquet, tide_fit_summary.csv (about 3 min)
python -I code/synthetic_check.py .                        # results/synthetic_check.json
python -I code/analysis.py .                               # results/eras.csv, era_differences.csv, years.csv, windows_30d.csv, binned_response.csv (about 10 min)
python -I code/window_tests.py .                           # results/pre_eruption_15d.csv, window_regressions_post2018.csv, window_tests.json, ...
python -I code/figures.py .                                # figures/*.png
```

The year-trend numbers (`files/results/year_trends.json`) are weighted least-squares fits to `years.csv` (gamma weighted by 1 / gamma_se^2; the share metrics unweighted) with x = year - 2020. The live catalog and the OOI data can change; compare the hashes with `files/data/input_hashes.txt`. Bootstrap seeds are fixed in the code.

## Citations

- Wilcock, W. S. D., et al. (2016). Seismic constraints on caldera dynamics from the 2015 Axial Seamount eruption. Science, 354, 1395-1399. doi:10.1126/science.aah5563.
- Wilcock, W. S. D., et al. (2016). Earthquake tidal triggering associated with the 2015 eruption of Axial Seamount. AGU Fall Meeting abstract OS44B-03 (bibcode 2016AGUFMOS44B..03W).
- Carlson, A. (2022). Is the tidal triggering of earthquakes at Axial Seamount predictive of eruptions? UW School of Oceanography senior thesis. https://digital.lib.washington.edu/researchworks/items/cdf781d2-c09c-40e0-bb34-84ceae101c4c.
- Scholz, C. H., Tan, Y. J., and Albino, F. (2019). The mechanism of tidal triggering of earthquakes at mid-ocean ridges. Nature Communications (2019).
- Tan, Y. J., et al. (2019). Tidal triggering and the stress dependence of the b value at Axial Seamount. Earth and Planetary Science Letters (cited for context; not tested here).
- Dieterich, J. H. (1987). Nucleation and triggering of earthquake slip: effect of periodic stresses. Tectonophysics, 144, 127-139. doi:10.1016/0040-1951(87)90012-6.
- Heimisson, E. R., and Segall, P. (2018). Constitutive law for earthquake production based on rate-and-state friction: Dieterich 1994 revisited. Journal of Geophysical Research: Solid Earth, 123, 4141-4156. doi:10.1029/2018JB015656.
- Chadwick, W. W., et al. (2022). Geodetic monitoring at Axial Seamount since its 2015 eruption. G-cubed, 23, e2021GC010153. doi:10.1029/2021GC010153.
- Campaign publication sci:sha256:efa0ed8b41234ce9584069ad29383a81b6828171ee249ce8635f14b643dd6368 (Axial Seamount forward test of the count-uplift model): uplift table, catalog parser, and the open question that this study answers.
- OOI Regional Cabled Array, NSF; UW Axial Seamount catalog. See `files/NOTICE-external-data.md`.
