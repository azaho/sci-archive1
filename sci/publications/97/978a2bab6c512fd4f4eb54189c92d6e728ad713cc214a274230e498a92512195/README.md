# After 1997, 28 saline Victorian streams became fresher and lost 6 points more salt than less rain explains, but saline baseflow carried only about one tenth of the lost runoff (2010-2021)

Job: sci-1107-dell-earth-and-ocean-sciences-0a462a4c6b68 (campaign 11_07_2026). Topic: earth and ocean sciences.
Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5), working through Claude Code. The signing key is a
campaign-machine key. It is not a personal authorship claim.

## 1. Question

After 1997, runoff in south-east Australia fell about 20-25% below each catchment's 1951-1996
rainfall-runoff relation, and it stayed low (campaign bundles 871b2192, 20955da2 and others).
Earlier campaign work removed many causes. Two Victorian bore studies (795f820e, 47f425a9) found that
shallow water tables fell about 1 m below their rainfall relation, and that larger falls went with larger
runoff losses. Follow-ups made this link weaker (646c1422, 905bbb47, 24e6bb47). An open question is:
did the streams lose their groundwater discharge (for example by disconnection from a falling water table),
or did they lose other water?

Stream salinity can answer this with an independent tracer. In most Victorian catchments, groundwater is
much more saline than event runoff. Thus the electrical conductivity (EC) of stream water tells how much
of the flow comes from groundwater. We asked three questions:

1. At equal flow and season, did stream EC change after 1997? At which flows?
2. Did salt export fall more or less than a simple decrease of rain would cause for the same water loss?
3. Which part of the lost water (in mm) was saline groundwater discharge (baseflow), and which part was
   fresh quickflow?

## 2. Data

- Stream EC grab samples (uS/cm at 25 C), parameter `salinityasec25wq`, from the Victorian Water
  Measurement Information System (WMIS, DEECA), downloaded on 2026-11-10. Most sites have monthly samples
  from 1990-1991 to 2026; some have samples from 1975. We kept WMIS quality codes below 150.
- Daily streamflow (mm/d), daily AGCD and SILO rain, and AGCD maximum temperature from CAMELS-AUS v2.03
  (Zenodo 14289037), 1951-2022.
- Water-table shortfall per catchment (`gw_r_late`, shallow bores within 5 km) from bundle 795f820e.
- Sample: all CAMELS-AUS gauges with WMIS EC that have at least 40 samples up to 1996, at least 40 samples
  in 2010-2021, at least 15 complete calendar years of flow in 1951-1996, and at least 8 in 2010-2021.
  This gives 83 catchments and 34,318 samples (median 83 samples before 1997 and 134 in 2010-2021 per
  catchment; median 30 calibration years).

## 3. Methods

All steps are per catchment unless we say otherwise. `files/code/analysis.py` has the full method.

**EC rating.** We fit log(EC) = a + b log(Q) + c log(Q)^2 + seasonal sine and cosine terms, with Q the
daily flow on the sample day. We fit one rating on samples up to 1996 ("pre") and one on samples in
2010-2022 ("late"). Retransformation uses the Duan smearing factor. Predictions are clipped to the observed
EC range.

**EC change at equal flow.** The mean residual of the late samples from the pre rating, in all samples and
in terciles of the pre-1997 daily flow distribution. Placebo: the difference of the residual between the
second and first half of the pre-1997 samples.

**Salt export and chemical mass balance (CMB).** We used each rating to compute daily EC and the daily
"salt flux" Q x EC (proportional to salt export). We split daily flow into two parts with a two-component
mixing model: baseflow fraction f = (EC - Ce) / (Cb - Ce), clipped to 0-1. Ce (event water) is the 2nd
percentile of pre-1997 EC. Cb (groundwater) is the median EC of pre-1997 samples at flows below the 10th
percentile. We used two forms of Cb: fixed at the pre-1997 value, or with a separate late value from the
late low-flow samples ("era GW EC"). The fixed form gives an upper bound of the baseflow loss (all
freshening counts as less groundwater). The era form gives a lower bound (all low-flow freshening counts
as fresher groundwater).

**Deficits.** For each annual series X (flow, salt flux, baseflow, quickflow) we fit
sqrt(X) = a + b P + c P(t-1) + d Tmax on 1951-1996 (as in bundle 795f820e). The deficit is the mean
observed X in 2010-2021 divided by the mean predicted X, minus 1. Years 1951-1989 use the pre rating on
the observed daily flows.

**Effective-rain analogue.** This is our null hypothesis: the catchment behaves as if it received less
rain. We find the factor k on 2010-2021 rain for which the pre-1997 flow model gives the observed mean
flow. Then we predict the salt flux, baseflow and quickflow at k x rain with their own pre-1997 models.
The "excess" of a flux is the observed change minus the analogue change (percentage points).
We split the salt excess into a flow-regime part (pre rating applied to the observed late daily flows,
minus the analogue) and a chemistry part (late rating minus pre rating on the same flows).

**Groups.** EC is a useful tracer only where groundwater is much more saline than event water. We call a
catchment "saline" if Cb / Ce >= 3 (28 catchments, median Cb 2,000 uS/cm). The other 55 catchments are
"fresh" (median Cb 110 uS/cm, Cb / Ce 1.7). We chose this threshold after a first look at the data. The
saline catchments are drier (median aridity PET/P 1.5 vs 1.0) and mostly cleared (31% vs 96% forest).

**Uncertainty.** Inside each catchment we bootstrapped the samples (inside each era) and the years
(calibration and test years), 200 times. Group medians have 95% intervals from a hierarchical bootstrap
(resample catchments, then one within-catchment draw per catchment, 2,000 times). P values are Wilcoxon
signed-rank tests on the catchment point values. Pooled mm shares sum deficits over catchments.

**Validation and sensitivity.** (a) Synthetic test: calibrate on 1951-1980, then multiply 1981-1996 rain
by 1.15. This makes real flows look like a deficit that a pure rain decrease causes. A correct method
must then give zero excess. (b) Placebo with a 1981-1996 test window and no chemistry change.
(c) SILO rain; a rating with a fixed pre-1997 shape and only an offset after 2010; a rating with a
30-day antecedent-flow term; at least 20 calibration years; the 1997-2009 window.

The first version of the analogue used the interannual elasticity of salt to flow. The synthetic test
showed a bias of -2.7 points for this version, so we changed to the effective-rain analogue before we
made the final runs. We report the elasticity version as a sensitivity (`x_salt_eps`, `x_bf_eps`).

## 4. Results

Numbers are group medians with 95% hierarchical bootstrap intervals, for 2010-2021 against the 1951-1996
relation, AGCD rain, unless we say otherwise. "pts" are percentage points.

**4.1 Streams became fresher at equal flow, mostly at low flow (Figure 1).** In all 83 catchments, EC at
equal flow and season was 5.8% lower than the 1990-1996 rating (log change -0.058, -0.087 to -0.021;
p = 0.0008). The change was largest in the low-flow tercile (-10.7%, p < 0.001), smaller at mid flow
(-4.3%) and absent at high flow (-0.8%, p = 0.88). The pre-1997 split-half placebo gave -2.8%.
In the 28 saline catchments, the change was -13.1% (all flows), -19.5% (low flow; -27.6 to -11.3),
-9.6% (mid) and -4.6% (high); placebo -2.9% (p = 0.27). In the 55 fresh catchments, only low-flow EC
fell (-7.7%, p < 0.001).

**4.2 The freshening developed during the drought and did not recover (Figure 5).** In saline catchments,
the per-catchment trend of the low-flow EC residual in 1997-2022 was -4.5% per decade (p = 0.008, n = 28).
After 2010 there was no further trend (+0.5% per decade, p = 0.92), and EC did not return to the
pre-1997 rating when runoff partly recovered in 2010-2012. Fresh catchments became saltier after about
2019 (low-flow trend after 2010 +6.1% per decade, p = 0.03).

**4.3 Saline streams lost more salt than less rain explains (Figure 2).** In the saline group, runoff was
30.4% below the rain relation (-43.1 to -17.7%). The same water loss from less rain (rain factor
k = 0.90) would reduce salt export by 27.3%. The observed salt export fell by 35.1%. The excess was
-6.1 pts (-14.2 to -3.5; p = 0.0009; negative in 79% of catchments). About half came from fresher water
at equal flow (chemistry part -5.2 pts, -7.4 to -0.8) and less from the changed daily flow regime
(-2.6 pts, -7.7 to 0.0; p = 0.002). Catchments with larger water deficits had larger excess salt loss
(Spearman rho 0.42, p = 0.03), and drier catchments had larger excess (rho with aridity -0.70). In the
fresh group, salt export followed the analogue (+2.4 pts, -2.2 to +5.7; p = 0.20).

**4.4 The saline baseflow component fell more than the analogue, but carried little of the lost water
(Figure 3).** With a fixed groundwater EC, the CMB baseflow of the saline group fell by 33.4%, against
14.9% for the analogue (excess -19.2 pts, -31.3 to -7.8; p = 0.001). Quickflow fell by 34.1%, against
33.1% for the analogue (+3.0 pts). With an era-specific groundwater EC (fresher groundwater after 2010),
the baseflow excess was -3.4 pts (-27.3 to +18.2; p = 0.99). Saline baseflow was only 14.9% of
predicted flow in these catchments (CMB baseflow index 0.13 per catchment). Thus, of the summed water
deficit (mean 25 mm/yr per catchment), saline baseflow carried 10.9% (-4.2 to 30.6%), of which only
4.8% (-9.3 to 21.2%) was beyond the analogue. With era-specific groundwater EC, this excess was -12.5%
(-47.8 to +9.8%). At least about 70% of the lost water was fresh quickflow, and quickflow fell by the
amount that a 10% rain decrease predicts.

**4.5 Validation and sensitivity (Figure 4).** The synthetic rain-decrease test (calibration 1951-1980,
1981-1996 rain x 1.15, 35% synthetic deficit) gave a salt excess of -0.8 pts (-1.6 to +0.5) and a
baseflow excess of -1.6 pts (-4.6 to +2.1). The 1981-1996 placebo gave -1.2 and -1.9 pts. All other
variants kept a salt excess (-5.8 to -11.1 pts) and a fixed-EC baseflow excess (-16.1 to -24.2 pts),
with intervals below zero. The excess baseflow share of the mm deficit stayed small (+2.7 to +13.7%;
upper bounds 19-40%). The earlier elasticity analogue gave the same signs (salt -6.9 pts, baseflow
-22.7 pts).

| Run (saline group) | n | water deficit % | salt excess, pts | baseflow excess, fixed GW EC, pts | baseflow excess, era GW EC, pts | low-flow log(EC) change x100 | baseflow excess as % of mm deficit, fixed GW EC |
|---|---|---|---|---|---|---|---|
| primary | 28 | -30.4 | -6.1 (-14.2 to -3.5) | -19.2 (-31.3 to -7.8) | -3.4 (-27.3 to +18.2) | -19.5 | +4.8 (-9.3 to +21.2) |
| silo | 28 | -27.3 | -6.8 (-15.1 to -3.8) | -21.0 (-33.1 to -8.7) | -3.6 (-28.1 to +17.0) | -19.5 | +7.3 (-14.7 to +40.0) |
| rating_offset | 28 | -30.4 | -11.1 (-15.5 to -6.8) | -24.2 (-37.4 to -15.6) | -14.8 (-30.7 to +0.5) | -19.5 | +13.7 (+2.7 to +30.8) |
| rating_antecedent | 28 | -30.4 | -7.0 (-12.8 to -2.5) | -16.3 (-29.7 to -4.4) | +9.9 (-23.3 to +21.7) | -20.2 | +2.7 (-10.4 to +19.0) |
| mincal20 | 26 | -30.4 | -5.8 (-14.1 to -2.5) | -18.2 (-32.4 to -6.3) | -3.4 (-29.2 to +21.0) | -19.5 | +4.7 (-10.2 to +24.3) |
| window_1997_2009 | 28 | -53.5 | -6.8 (-11.7 to -1.8) | -16.1 (-27.5 to -5.1) | -7.6 (-23.0 to +5.4) | -11.9 | +4.1 (-13.6 to +26.7) |
| placebo_1981_1996 | 14 | +2.1 | -1.2 (-2.4 to +0.9) | -1.9 (-6.0 to +2.8) | -1.9 (-6.0 to +2.8) | n/a | -3.8 (-74.0 to +63.4) |
| synthetic_rain15 | 14 | -34.6 | -0.8 (-1.6 to +0.5) | -1.6 (-4.6 to +2.1) | -1.6 (-4.6 to +2.1) | n/a | +0.4 (-1.3 to +2.1) |

(Placebo and synthetic runs use 14 saline catchments with 15 or more calibration years in 1951-1980; in
these runs EC changes are not defined because no late samples are used.)

**4.6 Link to water tables (post hoc).** In 23 catchments with bore data from bundle 795f820e, larger
water-table shortfalls went with a larger chemistry part of the salt loss (rho 0.51, p = 0.013; partial
rho given the water deficit 0.51) and with a larger baseflow excess (rho 0.53, p = 0.01; partial 0.46).
The link with low-flow EC alone was weak (rho 0.23, p = 0.29).


## 5. Interpretation

1. **The tracer confirms a groundwater signal.** In saline Victorian catchments, less saline groundwater
   reached the streams after 1997 than the rain predicts. The signal is largest at low flow, it grew
   during the drought, it did not recover after 2010, and it was largest where water tables fell most.
   This agrees with Westfall et al. (2025), who found fresher streams after the drought in 23 Victorian
   catchments, and with the baseflow and recession results of bundles 5b8df990 and 7cecffa9.
2. **But the groundwater signal is small in volume.** Saline groundwater discharge is a small part of
   flow in these catchments. Even with the upper-bound assumption (no change of groundwater EC), the loss
   of groundwater discharge beyond the rain analogue is about 5% (upper bound about 20%) of the lost
   water. Most of the lost water was fresh quickflow, and quickflow fell as if the catchments received
   about 10% less rain. Thus a loss of groundwater discharge to streams (for example stream-aquifer
   disconnection) cannot by itself explain the persistent runoff deficit.
3. **What remains.** The main loss is in the event-water response to rain. A falling water table can
   still cause this indirectly, for example through smaller saturated source areas or more infiltration
   into a thicker unsaturated zone. EC cannot separate this from other causes of a smaller event
   response. A test needs event-scale tracer or source-area data.
4. **Fresh catchments.** In the forested, wetter eastern catchments, EC cannot resolve the split, because
   groundwater is not saltier than event water. There, salt export followed the rain analogue, and only
   low-flow EC fell.
5. **Practical note.** Salt export from saline Victorian catchments in 2010-2021 was about one third
   below the pre-1997 rain relation, 6 points more than the water loss alone predicts. Salt-load models
   that scale salt with flow under a pre-1997 relation will over-predict salt export.


## 6. Limitations

- EC is a good tracer only in the 28 saline catchments. In the 55 fresh (mostly forested, eastern)
  catchments, groundwater and event water have similar EC, and the mass balance cannot resolve the split.
- Two-component mixing is a simplification. Soil water, bank storage and evaporative concentration also
  change EC. The "baseflow" of the CMB is saline water from the groundwater end-member, not all slow flow.
- We cannot separate "less groundwater discharge" from "fresher groundwater discharge" with EC alone.
  We give both bounds (fixed and era groundwater EC). Chloride or isotopes could separate them.
- Grab samples are monthly and rarely sample floods. The rating extrapolates to the highest flows.
- Pre-1997 EC samples cover mostly 1990-1996 (seven years). Salt fluxes before 1990 come from the
  1990-1996 rating applied to the observed flows.
- The saline group was chosen after a first look at the data; the group differs in aridity, land cover
  and location from the fresh group. Thus group contrasts are not causal.
- Possible changes in EC methods, salinity management (for example salt interception or tree planting)
  and irrigation return flows are not known per catchment. A step change of methods would affect all
  flows; the observed change is largest at low flows and small at high flows, and it developed
  gradually after 1997.
- The bore link uses only 23 catchments and is one of several post hoc correlations.

## 7. References

- Westfall, Peterson, Lintern, Western (2025). Fresher streams after a prolonged drought in Victoria,
  Australia. Water Resources Research. doi:10.1029/2025WR041614.
- Fowler et al. (2022). Explaining changes in rainfall-runoff relationships during and after Australia's
  Millennium Drought: a community perspective. HESS 26, 6073-6120. doi:10.5194/hess-26-6073-2022.
- Cartwright, Gilfedder, Hofmann (2014). Comparison and uncertainties of baseflow estimates from a
  chemical mass balance and digital filters. HESS 18, 15-30. doi:10.5194/hess-18-15-2014.
- Duan (1983). Smearing estimate: a nonparametric retransformation method. JASA 78, 605-610.
- Fowler et al. CAMELS-AUS v2. doi:10.5194/essd-17-4079-2025; data doi:10.5281/zenodo.14289037.
- Campaign bundles: 871b2192, 20955da2, 5b8df990, 7cecffa9, 795f820e, 47f425a9, 646c1422, 905bbb47,
  24e6bb47 (full IDs in sci.json).

## 8. Reproduction

See `files/code/reproduce.sh`. It extracts CAMELS-AUS members, downloads the WMIS EC records into a
scratch folder, and runs `prep.py`, `run_all.sh` (all variants), `summarize.py`, `timeline.py` and
`figures.py`. Python 3.12 with numpy, pandas, pyarrow, scipy and matplotlib. Runtime: about 2 h with
14 processes on a loaded 24-thread host. The WMIS service is live, so a new download can differ; the
SHA-256 of every file we used is in `files/provenance/wmis_files_sha256.csv`.

Files:
- `files/results/primary/`: per-catchment results (`gauge_results_with_attributes.csv`), within-catchment
  bootstrap draws (`gauge_boot.csv.gz`), annual flow and component series (`annual_components.csv.gz`),
  group summaries (`summary.json`).
- `files/results/<variant>/summary.json` and `gauge_results_with_attributes.csv` for each sensitivity run;
  `files/results/summary_variants.csv` compares them.
- `files/results/timeline.csv`, `timeline_trends.csv`: yearly EC and runoff residuals.
- `files/figures/`: figures 1-5. `files/DATA_NOTICE.md`: external data terms.

Column guide (gauge_results): `rq` water deficit (fraction); `rs` salt-flux deficit; `rs_ana` analogue;
`rsfix` salt deficit with the pre-1997 rating; `rqb`/`rqq` baseflow/quickflow deficits with fixed Cb;
`rqbv`/`rqqv` with era Cb; `*_ana` effective-rain analogues; `*_exp` elasticity analogues; `k_rain` rain
factor; `dlogec_*` mean log(EC) residual of late samples against the pre rating; `cb_pre`, `cb_late`, `ce`
end-members (uS/cm); `contrast` = cb_pre / ce; `bfi_pre` CMB baseflow index 1951-1996.
