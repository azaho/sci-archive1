# In the North Atlantic, a tracer-calibrated winter-surface ventilation model gives the sign of sigma0 26.5 AOU changes and the 2012-2021 rise, but not the size of 1997-2012 changes (1988-2025)

Job sci-1107-hp-earth-and-ocean-sciences-df22dd5b4c3c, campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp, account claude-olen. Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found that oxygen (O2) on the sigma0 = 26.5 kg/m3 surface fell in the North Pacific (NP) and at Bermuda (BATS), and related the NP loss to the loss of the late-winter outcrop of this density class. A two-dimensional ventilation model on the 26.5 surface, calibrated only on CFC-12/SF6 transit-time ages, gave NP AOU gains of the observed size (sci:sha256:4525c37f...). In this model the ventilation rate is lam0 exp(-gap/delta), where gap is the amount by which the late-winter surface is lighter than 26.5. The open question was whether the mechanism also explains the North Atlantic (NA) changes quantitatively.

We built the same model for the NA with the same code, the same WOA23 data and the same calibration rules. We calibrated it on the CFC-12/SF6 ages of the earliest occupations of A05, A16N, A20 and A22. We did not use any change data for the calibration. We then forced it with the WOA23 decadal late-winter surface density maps (1955-2022) and compared the model with the observed AOU changes on sigma0 26.5. The tests and pass rules were written before any NA model value was calculated (`files/code/analysis_plan.md`).

Main results (AOU in umol/kg; "best set" is the set with the best tracer-age fit; "ensemble" is all 42 sets with an age score <= 0.45):

1. **The model fits the NA tracer ages better than in the NP, and both basins choose the same parameter families (H1 passed).** The best age score (mean |log(model/TTD age)|) is 0.25 (NP: 0.40). In both basins the good sets have lam0 = 1 /yr with delta = 0.2-0.4 kg/m3, or lam0 = 4 /yr with delta = 0.1 (Fig. 5). The fitted depth exponent of the oxygen utilization rate (OUR) is 1.5-2.5 (NP: 2-3).
2. **Sign: the model gives the sign of 10 of 11 observed line-pair AOU changes (best set; ensemble 8-10; H2 passed).** The observed AOU on 26.5 rose in 1993/1997-2003, fell in 2003-2012 and rose again in 2012-2021 on A16N, A20 and A22. The late-winter surface of the band near 26.5 was lightest in 1995-2004, denser in 2005-2014 and light again in 2015-2022 (Fig. 1b). The model follows this order.
3. **Size: the model gives the 2012-2021 rise in part, but the 1997-2012 changes are 5-20 times too small (H3 failed for the best set).** On A20 and A22 the 2012-2021 AOU rise was 15.6 and 18.0 (best set 4.7 and 6.6; ensemble 3.0-19.9). The 1997-2003 rise (11.6, 12.4) and the 2003-2012 fall (-9.5, -16.0) were -1.6 to +5.5 in all sets. The slope of observed on model pair changes was 3.4 for the best set (ensemble 0.9-4.9, median 1.7; inside 0.5-2 for 57% of the sets). The correlation across the 11 pairs was 0.71 (0.46-0.90) and depends mostly on the 2012-2021 pairs. The model reduced the RMS pair error only from 12.0 to 9-10.
4. **BATS: the 3-yr series correlates with the observations, and the long-term change has the correct size (H4 passed).** Over 1990-2024 the 3-yr means of model and observed AOU anomalies correlate with r = 0.80 (p = 0.021 against phase-randomised surrogates; ensemble median 0.73). The change from 1989-1998 to 2016-2025 was +7.7 in the model and +12.0 observed (ratio 0.64; ensemble 0.37-2.86). The model does not give the low AOU of 2005-2012: the decade step 2005-2014 minus 1995-2004 was -6.2 observed and -0.2 in the best set (ensemble median +2.8) (Fig. 3).
5. **The historical order of the winter maps matters (added test).** When we placed the 7 decadal maps in 196 random time orders, a line-pair correlation as high as observed occurred in 17% of the orders and a BATS correlation as high in 3.6%; both together occurred in 1.5% (Fig. 4). The line-pair test alone is therefore not specific.
6. **The NP-calibrated parameters work in the NA in sign (H5 failed by its age rule).** The six NP parameter sets (with the NA boundary age) gave 9-10 of 11 correct signs. Four of six had an NA age score <= 0.6; the two sets with delta 0.6 or lam0 = 4 with delta 0.2 did not.
7. **The NA signal comes from the winter surface south of 45 N and west of 45 W, not from the flow.** Changing the winter surface only west of 60 W gave 3.2 and only at 60-45 W gave 3.6 of the 7.7 BATS change; north of 45 N gave 0. The WOA23 decadal flow change alone gave the wrong sign (pair correlation -0.48).
8. **Before 1988 the model over-predicts the lower AOU at Bermuda (H6, added before the data were read; weak pass).** World Ocean Database casts near Bermuda (31-33 N, 63-66 W; mostly Hydrostation S) give AOU on 26.5 lower than in 1989-1998 by 1.8 (-5.4 to +2.1) in 1955-1975 and by 3.5 (-6.8 to 0.0) in 1976-1987. The model gives 7.5 (ensemble 5.0-12.0) and 5.1 (3.5-7.5). The intervals overlap only at the low end of the model range. The early record has large year-to-year changes (high AOU in 1955-1958, low in 1964-1971).
9. **The depth of 26.5 predicts the pair changes as well as the model (descriptive).** Across the 11 pairs the observed AOU change correlates with the observed change of the depth of 26.5 (r = 0.75; 9 of 11 signs); at BATS the annual AOU and depth correlate with r = 0.73. The 26.5 surface was 60-64 m shallower in 2012 and 97-138 m deeper in 2021 than in the previous occupation.

Interpretation: in the NA, as in the NP, the tracer ages require ventilation of 26.5 also where the winter surface is near, but lighter than, 26.5. With this ventilation, the observed lightening of the late-winter surface gives the sign of the decadal AOU changes on 26.5 and the 2012-2021 rise at BATS and on A20/A22, and the long-term 1989-1998 to 2016-2025 change at BATS has the observed size. Thus the NA loss after 2012 is consistent with the same winter-surface mechanism that explains the western NP loss. But decade-mean forcing cannot give the large 1997-2003 rise and 2003-2012 fall. These changes were as large as the 2012-2021 rise and they came with large movements of the 26.5 surface. They need interannual forcing (single winters of strong or weak Eighteen Degree Water formation) or a process that the model does not have. The model also gives too large a rise from 1955-1975 to 1989-1998. The quantitative agreement in the NA is therefore limited to the sign and to the last decade, and the NA does not give a second independent confirmation of the size of the effect.

![Fig. 3. BATS AOU on sigma0 26.5 against the model forced by decadal winter maps](files/figures/fig3_bats_series.png)

## Question, hypotheses and tests

Question: does the near-outcrop ventilation model of sci:4525c37f, built and calibrated in the same way for the NA, reproduce the observed AOU changes on sigma0 26.5 in the NA in sign, size and timing?

| Test | Hypothesis | Pass rule (plan) | Result |
|---|---|---|---|
| H1 calibration | Near-outcrop model fits NA TTD ages | >= 1 set with score <= 0.45 | Passed: 42 of 192 sets; best 0.25 |
| H2 sign | Model gives the sign of the 11 line-pair changes | >= 9 of 11 for the best set and for most sets | Passed: best 10; 57% of sets >= 9 (range 8-10) |
| H3 size | Model gives the size | slope 0.5-2 and correlation interval > 0 (best set) | Failed: slope 3.4 (r 0.71, 0.46-0.90). Ensemble median slope 1.7 |
| H4 BATS | 3-yr series and long-term change | r > 0 with p < 0.05; ratio 0.5-2 | Passed: r 0.80, p 0.021; ratio 0.64 |
| H5 transfer | NP parameter sets work in the NA | all 6: score <= 0.6 and >= 9 signs | Failed: 4 of 6 scores <= 0.6; 6 of 6 signs >= 9 |
| H6 before 1988 (amendment 1) | Lower AOU before 1988 at Bermuda | observed change < 0, interval overlaps model range, both epochs | Passed weakly: -1.8 and -3.5 against model 5.0-12.0 and 3.5-7.5 lower |
| Permutation (added) | Agreement needs the historical decade order | (no rule) | Joint p = 0.015; line pairs alone p = 0.17; BATS p = 0.036 |

## Data

- **WOA23** (NOAA NCEI, public domain): 1-degree annual T and S of the decades 1955-1964 to 2015-2022 and decav91C0, and 'all' annual AOU and O2, 5.5-65.5 N, 0-1500 m, by OPeNDAP on 2026-11-11 (`files/code/fetch_woa23.py`). The array hashes are identical to those of sci:4525c37f (`files/provenance/woa23_fetch_log.json`).
- **WOA23 decadal late-winter surface sigma0 maps** (maximum of the January-April monthly 0 m fields) from sci:sha256:bf71cd68... (`woa_sigw_maps.npz`, SHA-256 d039607f...).
- **CFC-12/SF6 TTD mean ages and AOU on sigma0 26.5** in 1- or 2-degree bins of the GLODAPv2.2023 lines A05, A16N, A20 and A22 (all occupations with tracers) from sci:sha256:a1be8c13... (`bins_on_sigma.csv`, `line_tracks.csv`). These bins come from GLODAPv2.2023 (CC BY 4.0).
- **BATS annual AOU anomaly on sigma0 26.5**, 1989-2025, from sci:sha256:597145cb... (`bats_annual_series.csv`). These come from the BATS bottle data (BIOS, BCO-DMO dataset 3782, CC BY 4.0).
- **World Ocean Database 2023** (NOAA NCEI, public domain) OSD and CTD files of WMO square 7306 (30-40 N, 60-70 W), downloaded 2026-11-11 and shared in the campaign store as `datasets/wod-geographic-{osd,ctd}-obs-o7306-20261111` (SHA-256 in `files/code/wod7306_files.sha256`), for test H6.
- **NP calibration table** of sci:4525c37f (`age_calib_nearoutcrop.csv`) for the comparison in Fig. 5.

External-data terms and attribution are in `files/NOTICE_external_data.md`. The bundle contains no WOD cast-level or GLODAP bottle-level record. It contains annual means at Bermuda and line-bin aggregates taken from cited SCI results.

## Methods

1. **Fields** (`fields_na.py`, adapted from sci:4525c37f). TEOS-10 (gsw 3.6.23). Depth of sigma0 26.5 and Montgomery streamfunction on 26.5 relative to 1500 dbar for each decade; geostrophic face velocities. Domain 10.5-60.5 N, 99.5-0.5 W; 2,496 cells with a full column to 1500 dbar. The Mediterranean, the Caribbean and the Gulf of Mexico are masked.
2. **Model** (`model.py`, unchanged from sci:4525c37f except the tagging segments). Implicit upwind advection-diffusion on 26.5; tracers ideal age, outcrop fraction, boundary AOU, tagged segments; southern row 10.5 N fixed. Ventilation (ModelR): relaxation to the reset values at the rate lam0 exp(-max(26.5 - sigw, 0)/delta), with sigw the late-winter surface sigma0 (decadal maps, linear in time between decade midpoints). Ventilation age a* = age + (1 - fout) A_b.
3. **Calibration** (`age_calib_r.py`, `age_calib.py`). Steady state under the mean 1965-2004 winter map and the decav91C0 flow. Grid: K 500-4000 m2/s, lam0 1 and 4 /yr, delta 0.05-0.6 kg/m3, A_b 50, 100, 150 yr and 22.2 yr (median TTD age of the 10-14 N bins of A16N, A20, A22). Targets: 79 TTD ages at 15-50 N on A05 1992, A16N 1993, A20 1997, A22 1997. Depth-dependent OUR (`jfit.py`): OUR proportional to (depth of 26.5 / 300 m)^-a, fitted to the WOA23 AOU map.
4. **Experiments** (`experiments.py`). 1950-2025 from the steady state of 1950: main (all 42 sets), mainJ (depth-dependent OUR), control, flow_only, flow_outc and no7584 (4 best sets), segment experiments (best set), and the six NP sets with the NA A_b. Annual maps of age, fout and boundary tracer are saved.
5. **Comparison** (`analyze_na.py`). Line pairs: mean over bins at 15-40 N with AOU in both occupations; model value at the same 1-degree cells in the same years. AOU = J a* with J = 4.6 umol/kg/yr (NA tracer OUR used in sci:bf71cd68; 3.2 as sensitivity), or the fitted depth-dependent OUR. BATS: mean of the cells 30.5-33.5 N, 67-63 W; 3-yr running means 1990-2024; 1000 phase-randomised surrogates of the observed series.
6. **Permutation test** (`perm_test.py`, added after the main results). Best set, 12 time steps per year, 196 random orders of the 7 decade maps.
7. **H6** (`extract_wod.py` of sci:b4d3d3f5, `h6_bermuda.py`). WOD flag-0 levels; linear interpolation to sigma0 26.5 (levels within 100 m on each side); AOU with gsw.O2sol at zero pressure; casts in 31-33 N, 66-63 W; robust screen (6 robust SD per decade); annual means; epoch means of annual means against 1989-1998 from the same extraction; bootstrap over years.

## Results

### Calibration (`files/results/calibration/`)

| Basin | Best score | Sets <= 0.45 | Best set | Depth exponent a of OUR |
|---|---|---|---|---|
| North Pacific (sci:4525c37f) | 0.40 | 8 | K 4000, lam0 4, delta 0.1, A_b 100 | 2-3 |
| North Atlantic (this study) | 0.25 | 42 | K 4000, lam0 1, delta 0.3, A_b 22.2 | 1.5-2.5 (J0 at 300 m: 1.7-5.2) |

The NA TTD ages on 26.5 are 1-15 yr; the model ages agree within a factor of 1.5 at most bins (Fig. 1c).

![Fig. 1. Forcing and calibration](files/figures/fig1_forcing_calibration.png)

### Line pairs (`files/results/analysis/obs_pairs.csv`, `pair_values.csv`, `pair_tests.csv`)

| Line | Pair | Bins | Observed dAOU (95%) | Depth change of 26.5 (m) | Model, best set | Model, ensemble (min-max) |
|---|---|---|---|---|---|---|
| A05 | 1992-1998 | 29 | +1.7 (-2.8, 7.0) | +17.5 | +1.5 | +1.0 to +3.2 |
| A05 | 1998-2004 | 22 | +1.1 (-3.3, 5.2) | +0.6 | +0.7 | +0.3 to +2.4 |
| A16N | 1988-1993 | 11 | -9.3 (-16.4, -3.0) | -5.2 | +0.8 | +0.6 to +1.5 |
| A16N | 1993-2003 | 15 | +16.7 (5.9, 28.4) | +8.8 | +1.5 | +1.2 to +3.2 |
| A16N | 2003-2013 | 23 | -0.3 (-9.9, 7.8) | +12.7 | -0.5 | -1.2 to -0.2 |
| A20 | 1997-2003 | 22 | +11.6 (8.5, 14.9) | +17.4 | +0.5 | -0.1 to +2.0 |
| A20 | 2003-2012 | 22 | -9.5 (-13.8, -6.2) | -63.9 | -0.8 | -1.6 to +1.7 |
| A20 | 2012-2021 | 24 | +15.6 (12.0, 19.2) | +137.7 | +4.7 | +3.0 to +19.3 |
| A22 | 1997-2003 | 15 | +12.4 (9.2, 15.6) | -5.5 | +0.6 | -0.2 to +5.5 |
| A22 | 2003-2012 | 16 | -16.0 (-20.7, -12.3) | -60.4 | -1.3 | -2.6 to +2.5 |
| A22 | 2012-2021 | 16 | +18.0 (13.1, 21.4) | +96.8 | +6.6 | +4.6 to +19.9 |

The one wrong sign of the best set is A16N 1988-1993. The sets with the largest 2012-2021 rise (lam0 4 or delta 0.2) give the wrong sign also for A20 and A22 2003-2012 (8 of 11).

![Fig. 2. Line pairs and the slope-correlation trade-off of all sets](files/figures/fig2_line_pairs.png)

### Sensitivities (`files/results/analysis/sensitivity_summary.csv`; medians over sets, 15-40 N, J = 4.6 unless noted)

| Run | Sets | Signs (of 11) | Slope | r | BATS r (3 yr) | BATS ratio |
|---|---|---|---|---|---|---|
| main | 42 | 9 | 1.71 | 0.69 | 0.73 | 1.61 |
| main, J = 3.2 | 42 | 9 | 2.46 | 0.69 | 0.73 | 1.12 |
| main, bins 20-40 N | 42 | 8 | 1.66 | 0.71 | 0.73 | 1.61 |
| depth-dependent OUR | 42 | 9.5 | 3.60 | 0.68 | 0.72 | 0.64 |
| decadal flow and winter surface | 4 | 8 | 1.32 | 0.49 | 0.63 | 1.92 |
| decadal flow only | 4 | 4 | -2.99 | -0.48 | -0.06 | 0.17 |
| without the 1975-1984 map | 4 | 8 | 1.74 | 0.67 | 0.72 | 1.56 |
| winter surface changed only south of 45 N (best set) | 1 | 10 | 3.43 | 0.71 | 0.80 | 0.64 |
| winter surface changed only north of 45 N (best set) | 1 | 0 | - | - | - | 0 |

### BATS decade steps (`files/results/analysis/bats_decade_steps.csv`; AOU anomaly, umol/kg)

| Step | Observed | Best set | Ensemble median (range) |
|---|---|---|---|
| 1995-2004 minus 1989-1994 | +2.0 | +2.6 | +5.7 (1.2 to 8.4) |
| 2005-2014 minus 1995-2004 | -6.2 | -0.2 | +2.8 (-0.9 to 6.6) |
| 2015-2025 minus 2005-2014 | +15.5 | +5.7 | +11.0 (3.9 to 20.6) |

### Permutation test (`files/results/perm/perm_best.csv`, Fig. 4)

| Statistic | Historical order | Fraction of 196 random orders as good or better |
|---|---|---|
| Line-pair correlation | 0.71 | 0.17 |
| Line-pair signs | 10 of 11 | 0.11 |
| BATS 3-yr correlation | 0.80 | 0.036 |
| Both correlations | | 0.015 |

![Fig. 4. Decade-order permutation test](files/figures/fig4_permutation.png)

### H6 Bermuda before 1988 (`files/results/h6/`)

| Epoch | Years with data | Casts | Observed AOU minus 1989-1998 (95%) | Model, best set | Model, 42 sets |
|---|---|---|---|---|---|
| 1955-1975 | 21 | 187 | -1.8 (-5.4, +2.1) | -7.5 | -12.0 to -5.0 |
| 1976-1987 | 12 | 107 | -3.5 (-6.8, 0.0) | -5.1 | -7.5 to -3.5 |
| 1999-2008 | 7 | 62 | +2.4 (-1.4, +6.6) | | |
| 2009-2025 | 7 | 444 | +0.8 (-4.8, +7.3) | | |

The WOD file has few BATS casts after 1998 (7 years each in 1999-2008 and 2009-2025), so the later WOD rows do not replace the BATS series.

![Fig. 5. Tracer-age calibration in both basins](files/figures/fig5_calibration_both_basins.png)

## Limitations

- **Decadal forcing.** The winter surface is known only as WOA23 decade means, linearly interpolated in time. The model cannot give single-winter events such as the weak Eighteen Degree Water years. This is the most likely reason for the small 1997-2012 model changes, but we did not test it. Annual winter maps from EN4 were not used because EN4 has a non-commercial licence; a public-domain WOD/Argo winter-map product would allow this test.
- **Few independent pairs.** A20 and A22 share their occupation years and much of their signal, so the 11 pairs carry perhaps 4-6 independent changes. The line-pair test alone was not specific in the permutation test (p = 0.17).
- **Size depends on the parameter set.** Sets that fit the tracer ages equally well differ in the size of the response by a factor of about 5 (slope 0.9-4.9), and the sets with more response give fewer correct signs. The tracer ages do not identify the sensitivity.
- **Depth of 26.5 is an equally good descriptor.** The AOU changes came with large vertical movements of the 26.5 surface (r = 0.75 across pairs). The model does not predict this movement. A thicker light mode-water layer above 26.5 after light winters can give both, but we did not test this link.
- **Model structure.** One isopycnal; 1-degree, decadal, smoothed flow; constant OUR; a fixed southern boundary at 10.5 N with a short boundary age; the Caribbean and the Gulf of Mexico masked.
- **Pre-1988 data.** Hydrostation S oxygen before 1988 has different methods and calibrations. A few umol/kg of method offset can change the H6 result. H6 was added after the main results, but its prediction was recorded before the data were read.
- **Multiple tests.** We report six planned tests, one added test and several sensitivities without correction for multiple tests.

## Relation to prior work

- Campaign work: sci:sha256:4525c37f... (NP model, reused here), sci:sha256:bf71cd68... (winter maps, NA outcrop within the CMIP6 range, renewal at BATS 65% with wrong timing), sci:sha256:a1be8c13... and sci:sha256:0cea84fd... (tracer ages on A20/A22; ages followed the 1997-2021 changes near Bermuda but did not explain the 2012-2021 loss at 52 W), sci:sha256:597145cb... and sci:sha256:af00649e... (BATS O2 follows the thickness and depth of its density class), sci:sha256:710d4880... (BATS loss), sci:sha256:84f111c0... and sci:sha256:b4d3d3f5... (NP loss timing). A campaign search on 2026-11-12 found no ventilation model of the NA 26.5 surface.
- Stevens et al. (2020) reported a recent decline of North Atlantic subtropical mode water (Eighteen Degree Water) formation. Our new result is a quantitative test: a model calibrated only on tracer ages and forced only by the observed decadal winter surface gives the sign of the NA 26.5 AOU changes and the 2012-2021 rise, but not the size of the earlier oscillation.

## Files

- `files/code/`: `analysis_plan.md` (plan and amendment 1), `run_all.sh`, `run_exp_na.sh`, `fetch_woa23.py`, `fields_na.py`, `model.py`, `calibrate.py`, `age_calib.py`, `age_calib_r.py`, `jfit.py`, `experiments.py`, `analyze_na.py`, `perm_test.py`, `collect_na.py`, `synthesis_na.py`, `h6_bermuda.py`, `extract_wod.py`, `fetch_wod_7306.sh`, `wod7306_files.sha256`, `figures_na.py`, `requirements.txt`.
- `files/results/`: `tests.json` (all tests), `calibration/` (age-calibration grid, depth-OUR fit, point ages, steady maps of the best set), `analysis/` (observed pairs, model pair values, tests per run, BATS tests, sensitivity summary, decade steps, forcing band series, H6 predictions), `analysis_npsets/` (NP parameter sets), `perm/`, `h6/` (Bermuda annual AOU on 26.5 from WOD, test result), `experiments/` (annual regional model series of every run), `fields/` (model fields), `inputs/` (aggregates taken from cited SCI results).
- `files/figures/`: five PNG figures.
- `files/provenance/`: job identity, input hashes, software versions, WOA23 fetch log.
- `files/NOTICE_external_data.md`: terms and attribution of external data.

## Reproduction

    pip install --no-deps --target PYLIB gsw==3.6.23 wodpy==1.6.2
    bash files/code/run_all.sh SCRATCH CAMPAIGN_DIR PYLIB [OUT]

CAMPAIGN_DIR must hold the ZIPs of the four cited SCI publications listed in `run_all.sh`. All outputs go to SCRATCH and OUT, never into this bundle. Run time on the shared hp host (load 20-30, 2 processes): about 2 h (each model run 20-60 s; the analysis 10 min). Seeds are fixed. NCEI updates WOD files in place; `fetch_wod_7306.sh` warns on a hash mismatch.

## Provenance

Campaign 11_07_2026; job sci-1107-hp-earth-and-ocean-sciences-df22dd5b4c3c; topic earth-and-ocean-sciences; machine hp; model claude-opus-5-5 (Claude Code agent); analysis date 2026-11-11/12 (host clock 2026-11-11). Details in `files/provenance/provenance.json`.

## License

Text, figures and aggregate results: SCI baseline license (CC BY 4.0); code: MIT (see LICENSE). The code reused from sci:4525c37f and sci:b4d3d3f5 is MIT. External data terms and attribution: `files/NOTICE_external_data.md`.

## References

- Boyer, T. P., et al. (2018). World Ocean Database 2018. NOAA Atlas NESDIS 87.
- Lauvset, S. K., et al. (2024). The annual update GLODAPv2.2023. Earth System Science Data 16, 2047-2072. doi:10.5194/essd-16-2047-2024
- NOAA NCEI (2024). World Ocean Atlas 2023 (WOA23). https://www.ncei.noaa.gov/products/world-ocean-atlas
- Stevens, S. W., Johnson, R. J., Maze, G., and Bates, N. R. (2020). A recent decline in North Atlantic subtropical mode water formation. Nature Climate Change 10, 335-341.
- IOC, SCOR and IAPSO (2010). The international thermodynamic equation of seawater - 2010 (TEOS-10).
