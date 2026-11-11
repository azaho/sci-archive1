# Runoff per unit rain fell in a 1997-1998 step in Victoria but declined from the 1950s in New South Wales; the Victorian step came before most water-table fall (CAMELS-AUS, 1952-2021)

Job sci-1107-dell-earth-and-ocean-sciences-e2b208db9249 · topic earth-and-ocean-sciences · machine dell ·
model claude-opus-5-5 (Claude Opus 5.5) · campaign 11_07_2026. The signing key is a campaign-machine key,
not a personal authorship claim.

## Summary

**Question.** After 1997, south-east Australian (SE-AU) runoff stayed 20-25% below the
1951-1996 rainfall-runoff relation. Earlier campaign work excluded rain-gauge noise, stored water,
evaporative demand, greening, bushfire and one-parameter Budyko changes. Victorian water tables fell
about 1 m from 1997, but the groundwater link weakened under controls. A drought-triggered mechanism,
for example stream-aquifer disconnection, must give a change that starts with the Millennium Drought.
A slow driver (farm dams, land use, forest change, data drift) gives a decline that starts earlier.
We asked: **what is the time shape of the loss of runoff per unit rain over 1952-2021, and when did it
start?**

**Method.** We used 120 SE-AU CAMELS-AUS v2.03 catchments with long annual flow records, and three
rain sources: AGCD, SILO and a fixed network of long-record GHCN-Daily rain gauges (no network change
in 1951-2021). A two-way panel model, sqrt(Q_it) = a_i + b_i P_it + c_i P_i,t-1 + s_i g_t + e_it,
gives a common annual runoff-efficiency profile g_t without a calibration window. We compared step,
trend, hinge and ramp shapes of g_t with AR(1) errors and BIC. Intervals are 95% cluster bootstraps over
2 x 2 degree cells (the whole panel fit is repeated in each draw). The plan (`files/ANALYSIS_PLAN.md`)
was written and hashed before any timing result. The split by state and all mechanism checks are
post hoc.

**Results.**

1. **Pooled SE-AU (planned endpoint).** A gradual decline fitted better than a step
   (BIC difference -15.0, 95% interval -20.0 to -2.9, AGCD; -11.5 with SILO). In 1985-1996, 46% (31-66%)
   of the 2010-2021 loss was already present (38 of 78 mm/yr). **This planned result is not robust.**
   With the fixed gauges (37 catchments) the difference was -3.7 (-10.7 to +10.1). With an early
   calibration window, or a start in 1960 or 1965, a step fitted equally well or better.
2. **The pooled region mixes two time shapes (post hoc).**
   - **Victoria (71 catchments): a step in 1997-1998.** Runoff efficiency was flat from about 1957 to
     1996 and then fell by 0.6-0.9 SD in one step. Step fitted better than gradual with all three rain
     sources: BIC difference +6.1 (AGCD), +10.3 (SILO), +10.0 (gauges, 24 catchments, interval +3.9
     to +14.1). The step at 1997 beyond any trend was -0.62 SD (-1.08 to -0.25), -0.73 (-1.13 to
     -0.43) and -0.94 (-1.40 to -0.56). The best step year was 1997 or 1998 (bootstrap 1997-1998). The
     1985-1996 deficit was small or zero (AGCD -0.22 SD; SILO -0.05; gauges +0.17).
   - **New South Wales and ACT (39 catchments): a gradual decline from the 1950s to about 1992, and
     no extra step in 1997.** Gradual fitted better: -13.8 (-15.9 to -4.7) AGCD, -9.4 (-13.6 to -2.9)
     SILO, -10.1 (-10.6 to +0.7) gauges (12 catchments). The 1997 step beyond the trend was +0.13
     (-0.14 to +0.43), +0.38 and +0.12 SD, that is, not a loss. In 1985-1996 runoff was already 20-22%
     (42-65 mm/yr) below the 1952-1970 relation, 65-81% of the 2010-2021 loss.
3. **Per-catchment fits agree.** The gradual-trend term was more negative in the east (Spearman rho
   with outlet longitude -0.55, -0.68 to -0.39). The 1997 step was more negative in the west (rho
   +0.60, +0.38 to +0.73). Land-use and water-body proxies (CAMELS-AUS water-body fraction,
   impoundment, land-use and pasture factors) did not go with a larger gradual decline (rho +0.10 to
   +0.16, all intervals include zero or are positive).
4. **The Victorian step came before most of the water-table fall.** Victorian shallow water tables
   (published regional median, sci:sha256:47f425a9) were flat in 1978-1996 and then fell gradually,
   with a best single-step year of 2002. In 1998-2000, the water table was 0.58 m down, half of its
   2001-2009 level (1.16 m). Runoff efficiency was already at 80-95% of its 2001-2009 deficit
   (AGCD -1.01 against -1.06 SD; SILO -0.90 against -1.01; gauges -0.62 against -0.77). The two
   series correlate over 1978-2021 (r = 0.73) because both are low after 1997.
5. **Checks that did not change the shapes (post hoc).** Heavy-rain amount and wet-day count
   (AGCD and SILO daily rain); the Interdecadal Pacific Oscillation phase (IPO TPI, r with g between
   -0.15 and +0.19; BIC 23-35 worse than the best shape); rain squared; three years of rain memory;
   Morton PET; a stricter, near-balanced catchment set; a 70% gauge-completeness network (59
   catchments: Victoria +10.3, NSW+ACT -10.7 with gauge rain). Adding temperature weakened the NSW+ACT
   shape preference (-8.0 AGCD, -2.5 SILO, -2.2 gauges), but the 1985-1996 deficit stayed (-0.46 to
   -0.84 SD). With a start in 1960 or 1965 the NSW+ACT preference fell to -0.6 to -5.1, but the
   1985-1996 deficit relative to 1960-1975 stayed at -0.39 to -0.60 SD (54-76% of the late loss).
6. **The method can tell the shapes apart.** In synthetic data with the real rain, catchments and
   noise, a true 1997 step gave a gradual preference in only 1-3% of 150 sets per region. A true trend
   gave a 95th percentile of +2.1 to +2.7. The observed Victorian value (+6.0) is above every
   pure-trend 95th percentile. The NSW+ACT value (-13.8) is below the 5th percentile of the pure-trend
   sets (-9.4).
7. **Controls.** South-west Western Australia (12 catchments) had a strong post-1997 step (-1.1 SD) and
   no 1985-1996 deficit. Northern Australia (31) had no loss.

**Conclusion.** The "post-1997 SE-AU runoff loss" is two different changes. In Victoria the loss is
an abrupt 1997-1998 step at the start of the Millennium Drought. A drought-triggered mechanism is
therefore possible there. But the step came before most of the water-table fall, so a gradual
groundwater decline did not lead the loss. A threshold crossed by the first part of the fall, or a
common driver of both, remains possible. In New South Wales the loss of runoff per unit rain had
mostly occurred before 1997, during the wet-to-dry decades 1955-1995. No drought, groundwater or
post-1997 mechanism can explain that part. Explanations of the SE-AU shift must treat the two regions
separately, and studies that calibrate on 1951-1996 underestimate the NSW loss.

**Main limitations.** The state split, all mechanism checks and the bore comparison are post hoc.
The pooled planned endpoint is not robust to the start year or the calibration method. Before 1960
fewer catchments have flow (39 in 1952 against about 118 after 1967), and the very wet 1950s
influence the NSW trend. The fixed-gauge sets are small (24 Victorian, 12 NSW+ACT catchments). The
annual model has catchment-specific rain slopes but no land-use, farm-dam or extraction time series,
so we did not identify the cause of the NSW decline. Temperature and a trend are hard to separate in
NSW. The bore series is regional, not stream-side. Flow ends in 2020-2022, depending on the source.

## Figures

- `files/figures/fig1_profiles_vic_nsw.png`: regional runoff-efficiency profiles, Victoria and NSW+ACT,
  three rain sources, with the AGCD bootstrap band and the best shape.
- `files/figures/fig2_map_trend_step.png`: per-catchment gradual trend and extra 1997 step.
- `files/figures/fig3_victoria_runoff_vs_bores.png`: Victorian runoff efficiency against the regional
  shallow water-table median.
- `files/figures/fig4_shape_robustness.png`: BIC difference for every configuration with bootstrap
  intervals.
- `files/figures/fig5_synthetic_recovery.png`: synthetic recovery test.

## Methods in detail

**Data.** CAMELS-AUS v2.03 daily flow (mm/d), AGCD and SILO daily rain, AGCD Tmax/Tmin, SILO Morton
wet-environment ET. Calendar years; a flow year needs 90% or more valid days. Groups: SE-AU = outlets in
VIC, NSW, ACT, SA, TAS; SW-WA = WA south of 30 S; North-AU = other. Primary set: 40 or more valid
years in 1951-2021, 15 or more in 1951-1980, and 8 or more in each of 1997-2009 and 2010-2021 (120 SE-AU:
71 VIC, 36 NSW, 3 ACT, 10 TAS). Balanced set: 80% of years in every decade block from 1955 (36).

**Fixed gauge rain.** We used the 732 GHCN-Daily candidate stations of sci:sha256:20955da2 (inside or
within 25 km of a catchment). A station-year is valid if all months have 90% or more daily coverage.
A station joins the network only if it has valid years in 80% or more of the years of every block
1951-60, ..., 2011-21. The index is an inverse-distance mean of P_k(y)/mean_k(1951-1996), scaled
by the AGCD 1951-1996 catchment mean. Relative to these gauges, AGCD rose by about 1.5-2% and SILO fell
by about 3% from the 1950s to the 2010s.

**Profile.** Alternating least squares for a_i, b_i, c_i and g_t; s_i is the residual SD of the
stationary fit; g_t is relative to its 1952-1970 mean. Effects in mm/yr are mean[(F + s g)^2 - F^2]
with F the fitted sqrt flow without g.

**Shapes.** S0 constant; S1 step at 1997; S2 step at a free year 1965-2012; S3 linear trend; S4
hinge from a free year 1955-2010; S5 step 1997 + trend; S6 ramp between two free years; S7 free hinge
+ step 1997. Exact Gaussian AR(1) likelihood profiled over phi; each free break year counts as one
parameter. "Gradual minus step" = min BIC(S3, S4, S6) - min BIC(S1, S2). Bootstrap draws use S0-S5
and a coarser phi grid.

**Deviations from the plan.** The early-calibration variant used 1952-1980 (the plan wrote
1952-1975), to match the selection rule. S6 is not refitted in the bootstrap draws. In the first
run, one SW-WA bootstrap draw contained no 1952-1970 data and stopped the run. We added a rule that
marks a draw as degenerate when fewer than 10 of its 1952-1970 years or fewer than 40 years have a value, and reran with the same seeds. Degenerate draws are excluded from intervals: none in the pooled SE-AU runs, 1-6 of 1,000 in NSW+ACT and TAS runs, 3-24 in the small Victorian gauge-subset runs, and 31-51 of 500 in SW-WA (column `boot_degenerate` in the summaries).

**Post hoc checks.** (P1) synthetic recovery (`code/posthoc.py p1`); (P2) start years 1960 and
1965; (P3) state split, with the full bootstrap pipeline (`code/posthoc_states.py`); (P4/P5)
per-catchment OLS fits sqrt(Q) = X b + theta (t - 1952)/10 + delta [t >= 1997] in SD units and
their Spearman links with attributes; (P6) Victorian bore timing; heavy rain (`code/posthoc_heavy.py`),
IPO (`code/posthoc_ipo.py`), 70% gauge network (`code/posthoc_fixed70.py`).

## Key numbers (files/results)

| Region, rain | n | BIC gradual - step (95% CI) | g 1985-96 | g 2010-21 | share of late loss present 1985-96 | step 1997 beyond trend |
|---|---|---|---|---|---|---|
| SE-AU AGCD (planned) | 120 | -15.0 (-20.0, -2.9) | -0.54 | -1.17 | 0.46 (0.31, 0.66) | -0.20 (-0.47, 0.09) |
| SE-AU SILO (planned) | 120 | -11.5 (-15.8, -0.1) | -0.54 | -0.98 | 0.55 (0.32, 0.76) | -0.08 |
| SE-AU gauges (planned) | 37 | -3.7 (-10.7, 10.1) | -0.30 | -0.83 | 0.36 (-0.03, 0.77) | -0.32 (-0.83, 0.14) |
| VIC AGCD | 71 | +6.1 (-9.4, 15.0) | -0.22 | -1.12 | 0.20 (0.02, 0.39) | -0.62 (-1.08, -0.25) |
| VIC SILO | 71 | +10.3 (-0.3, 19.3) | -0.05 | -0.79 | 0.07 (-0.08, 0.26) | -0.73 (-1.13, -0.43) |
| VIC gauges | 24 | +10.0 (3.9, 14.1) | +0.17 | -0.63 | -0.27 (-0.51, 0.25) | -0.94 (-1.40, -0.56) |
| NSW+ACT AGCD | 39 | -13.8 (-15.9, -4.7) | -0.79 | -1.18 | 0.67 (0.47, 0.99) | +0.13 (-0.14, 0.43) |
| NSW+ACT SILO | 39 | -9.4 (-13.6, -2.9) | -0.88 | -1.08 | 0.81 (0.69, 1.07) | +0.38 (0.16, 0.57) |
| NSW+ACT gauges | 12 | -10.1 (-10.6, 0.7) | -0.61 | -0.94 | 0.65 (0.21, 1.17) | +0.12 (-0.46, 0.58) |
| SW-WA AGCD | 12 | -4.1 (-9.3, 1.4) | +0.06 | -1.54 | -0.04 | -1.11 (-1.45, -0.78) |
| North-AU AGCD | 31 | +3.7 (-3.0, 4.4) | -0.10 | +0.37 | n/a | +0.02 |

g in catchment SD units relative to 1952-1970. Full tables: `files/results/out/summary.csv`
(planned) and `files/results/out/summary_states.csv` (post hoc state split).

## Files

- `files/ANALYSIS_PLAN.md`, `files/code/ANALYSIS_PLAN.sha256`: plan and its hash with time.
- `files/code/`: `build_annual.py`, `build_heavy.py`, `fetch_ghcnd.py`, `station_index_fixed.py`,
  `twoway.py` (model), `run_all.py` (planned runs), `posthoc*.py`, `figures.py`, `reproduce.sh`.
- `files/data/`: annual CAMELS-AUS-derived tables, gauge network membership, published bore series,
  IPO series (see `files/DATA_NOTICE.md`).
- `files/results/out/`: per configuration `profile_*` (g_t and catchment count), `shapes_*` (all
  shape fits), `boot_*` (all bootstrap draws; the first 200 include g_t), `summary*.csv/json`.
- `files/results/posthoc/`: post hoc tables, synthetic draws, per-catchment fits.
- `files/provenance/`: hashes of shared datasets, extracted members, GHCN-Daily files and other inputs;
  software versions.

## Reproduction

`bash files/code/reproduce.sh SCRATCH_DIR` downloads CAMELS-AUS v2.03, GHCN-Daily station files and
the IPO index into SCRATCH_DIR, reads the bore series from the cited SCI publication, and repeats every
step (about 2-3 hours on 12 cores). Bootstrap seeds are fixed. To check the figures and tables
only, run `python files/code/figures.py WORK RAW FIG` against the included results and the CAMELS-AUS
boundary shapefile. The GHCN-Daily rain index is not included; it is regenerated in scratch.

## Relation to earlier work

This study builds on the SCI campaign results on the SE-AU post-1997 runoff loss: sci:sha256:871b2192
(rain-slope loss), sci:sha256:448ef5cf (monthly model; a post hoc gradual-drift result on 67
catchments), sci:sha256:20955da2 (fixed gauge networks), sci:sha256:47f425a9 and sci:sha256:795f820e
(Victorian bores), sci:sha256:646c1422 and sci:sha256:905bbb47 (weaker groundwater link) and
sci:sha256:36d145c1 (Victorian hidden low-runoff states). Our result supports the abrupt Victorian state
change of Peterson et al. (2021, Science 372:745) and sci:sha256:36d145c1. It also shows that the
gradual drift reported in sci:sha256:448ef5cf comes mostly from NSW catchments. External literature:
Saft et al. (2015, WRR 51:2444), Fowler et al. (2022, HESS 26:6073), Henley et al. (2015).
