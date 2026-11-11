# Climate-set root-zone storage growth predicts 16% of the lost south-east Australian runoff after 2009 and false losses in northern Australia (174 + 62 catchments, GR4J)

Job sci-1107-dell-earth-and-ocean-sciences-291f20d761c4, campaign 11_07_2026, topic earth-and-ocean-sciences,
machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key. It is not a
personal authorship claim.

## Question

After 1997, runoff in south-east Australia (SE-AU) fell about 20-25% below the 1951-1996 rainfall-runoff
relation and stayed low, also in the wet years 2010-2011 and 2020-2022. Earlier campaign work excluded
rain-gauge artefacts, stored water (GRACE), evaporative demand, greening, fire, channel losses and land use
in protected catchments (for example sci:sha256:871b2192..., ccf7e5d4..., 58715cfe..., c651f046...,
a3f0e3af..., 1ace58a8..., 5eddb9c5...). Most of the lost water was fresh quickflow (978a2bab...). If storage
did not change, the water balance needs more evaporation at equal rain.

One mechanism that can make more evaporation persist is ecosystem adaptation of the root zone. Vegetation
sizes its accessible storage capacity Sr to the largest climatic storage deficit of the past decades (the
mass-curve method of Gao et al. 2014 and Wang-Erlandsson et al. 2016). If the Millennium Drought made record
deficits, Sr grew and stayed large (a "ratchet"). A larger store holds more rain for transpiration, so less
quickflow and baseflow form. Tian et al. (2022, HESS 26:4853) found that the GR4J production-store capacity
calibrated to flow increased during the drought. Trotter et al. (2023, MODSIM) let storage capacity follow
recent climate. Neither study predicted the change from climate alone and then tested it against the flow
record.

We asked: **if Sr is set only by the climate record (with no flow data after 1996), does the ratchet predict the
size, the persistence and the spatial pattern of the post-1997 loss? Does it correctly predict no loss in
northern Australia?**

## Approach (fixed in files/ANALYSIS_PLAN.md before any deficit was computed)

- Data: CAMELS-AUS v2.03 daily streamflow, AGCD rain (primary), SILO rain (secondary) and SILO Morton
  wet-environment areal potential evaporation Ep, 1950 to the end of record (at most 2022-02).
  Catchments: 175 SE-AU, 64 North-AU (control without the Millennium Drought) and 25 south-west Western
  Australia (SW-WA) catchments from bundle 871b2192. 261 catchments passed the rules (calibration KGE >= 0.5):
  174 SE-AU, 62 North-AU, 25 SW-WA. Median calibration KGE was 0.84 (SE-AU) and 0.85 (North-AU).
- Model: daily GR4J. All models were calibrated on 1956-1996 only (warm-up 1950-1955), with the mean of
  KGE(Q) and KGE(sqrt Q) as the objective and differential evolution with a fixed seed.
- Climatic capacity: f = (P - Q) / Ep over the calibration days (fixed evaporation fraction), the daily
  deficit D(t) = max(0, D(t-1) + f Ep - P), and the annual maximum of D.
  - Ratchet (M1): Sr(y) = maximum annual deficit in the previous 20 years.
  - Reversible (M2): Sr(y) = maximum annual deficit in the previous 3 years.
  - The GR4J capacity is X1(y) = X1_0 Sr(y) / mean Sr(1956-1996). This adds no free parameter. M0 is static GR4J.
- Outcomes per catchment for P2 = 2010-end and P1 = 1997-2009 (observed-flow days only):
  - observed change dObs = Qobs / Qsim(M0) - 1;
  - predicted change dPred = Qsim(M1 or M2) / Qsim(M0) - 1.
  - The primary statistic is FE = mean dPred / mean dObs, with a bootstrap over catchments.
  - We also report the same quantities in mm/yr (volume-weighted). We added this measure after we saw
    the pooled annual series. It was not in the plan.

## Results

### Primary outcomes (SE-AU, AGCD rain, 2010-end)

| Quantity | Ratchet M1 | Reversible M2 |
| --- | --- | --- |
| Mean observed change dObs (174 catchments) | -24.0% (95% CI -26.6 to -21.4) | same |
| Mean predicted change dPred | -11.6% (-14.7 to -8.7) | -13.1% (-16.5 to -9.9) |
| FE (mean of catchment ratios) | 0.48 (0.38-0.60) | 0.55 (0.43-0.67) |
| Spearman rho(dPred, dObs) | 0.25 (0.09-0.40) | 0.39 (0.24-0.53) |
| North-AU control: observed / predicted | +11.1% / -8.1% (-15.6 to +1.9) | +11.1% / -10.7% |
| Volume: observed / predicted (mm/yr) | -55.7 / -8.8 | -55.7 / -10.1 |
| FE by volume | 0.16 (0.10-0.23) | 0.18 (0.13-0.24) |

By the pre-set rule:

- The ratchet result is "partial / inconclusive": FE is 0.48, below the 0.5 that "explains most" requires,
  but its lower bound is above 0.25.
- The false-positive control **failed**. The ratchet predicts an 8-point loss in North-AU, where flow
  increased by 11%. The rule allowed at most 5 points.
- The ratchet is **not** favoured over the reversible model: FE(M1) - FE(M2) = -0.06 (-0.11 to -0.02).

### Where the predicted loss comes from (Figures 1, 2 and 5)

The FE of 0.48 comes almost completely from dry catchments. In terciles of 1956-1996 runoff:

| SE-AU tercile (1956-96 runoff, mm/yr) | Observed | Ratchet predicted | Observed mm/yr | Predicted mm/yr |
| --- | --- | --- | --- | --- |
| dry (21-164, n=58) | -34% | -30% | -26 | -18 |
| mid (164-344, n=58) | -21% | -4% | -53 | -8 |
| wet (349-2032, n=58) | -16% | -0.3% | -88 | -0.9 |

In dry catchments the climatic capacity ratio Sr(2010-end) / Sr(1956-96) is about 1.8. The same ratio
occurs in the dry North-AU catchments (median 1.88). There the ratchet predicts a median change of -31%,
but flow rose (median +11%, mean +17%). The prediction follows the climatic capacity ratio almost exactly (Spearman -0.93 within SE-AU,
-0.96 within North-AU). The water-limited GR4J responds strongly to X1 in dry catchments, so it responds to
any multi-year deficit, with or without a real loss. The model explains only 10% (95% CI -15 to +35%) of
the SE-AU minus North-AU contrast in observed change.

In the wet third of SE-AU, which lost most of the water (88 mm/yr), the Millennium Drought did not exceed
the earlier deficits much (capacity ratio about 1.06). Across all SE-AU catchments, the median ratio of the
Millennium Drought maximum deficit to the 1956-1996 maximum is only 1.07. So the climatic ratchet does not
produce a capacity change where most of the water was lost.

### The capacity change that the flow needs is not the climatic one (Figure 3)

As a diagnostic only, we refitted X1 alone on 2010-end flow with the other M0 parameters held. To reproduce
the post-2009 flow, SE-AU needs a median X1 increase of x1.56 (SILO x1.37), SW-WA needs x1.62, and North-AU
needs x0.82. This agrees with Tian et al. (2022): a larger effective store reproduces the SE-AU loss. But
across SE-AU catchments the required ratio does not follow the climatic Sr ratio (Spearman -0.13, 95% CI
-0.28 to +0.04; the sign is opposite to the hypothesis). The required increase is similar in dry, mid and
wet terciles (x1.69, x1.46, x1.49). The SE-AU flow behaves as if the store became about 1.5 times larger
everywhere, but the size of the past drought deficit does not set that change.

### Other secondary results

- Elasticity: with X1 = X1_0 (Sr/Sr_ref)^beta and beta free in 1956-1996, the median beta is 0 (quartiles
  0 to 0.61). The pre-1997 record gives no support for a capacity that follows past deficits, and this model
  predicts FE 0.14 (0.07-0.22).
- Annual-reset deficit (D set to zero each 1 July): FE 0.03 (0.005-0.06). The ratchet prediction needs
  deficits that accumulate over many years under a fixed evaporation fraction. That assumption is itself
  doubtful in a drought, because real vegetation reduces transpiration.
- SILO rain: the SE-AU observed deficit is smaller (-17.1% mean, -33 mm/yr). Ratchet FE is 0.81 by ratio
  (0.64-1.02) and 0.32 by volume (0.21-0.53). The dry-catchment pattern is the same.
- 1997-2009: ratchet FE 0.22 (0.18-0.27), by volume 0.07.
- SW-WA (25 catchments, drying since 1975 and 2000): ratchet FE 0.83 (0.54-1.31), by volume 0.39
  (0.27-0.66). It is the region where the ratchet comes nearest. But SW-WA catchments are mostly dry, which
  is the class with false North-AU predictions.
- Flow components (Lyne-Hollick filter, Figure 4): in 2010-end the observed SE-AU change is -5.7% of static
  flow in baseflow and -18.3% in quickflow. The ratchet predicts -1.0% and -10.6% (mean of catchment ratios).

## Interpretation

A climate-set root-zone ratchet is not a sufficient explanation of the persistent SE-AU runoff loss:

1. It predicts only about one sixth of the lost water volume.
2. It predicts nothing where most water was lost (the wet third).
3. It predicts equal losses in dry northern catchments that did not lose flow.
4. Its predicted spatial pattern does not match the capacity change that the flow needs.

A uniform increase of the effective GR4J store of about x1.5 fits the SE-AU loss. Thus a change in how the
catchment partitions water (more held for evaporation) stays the best description, but the size of the past
drought deficit does not predict it. This leaves open causes that act at a similar fraction in wet and dry
SE-AU catchments, for example a regional change in vegetation water use or in rain properties that the
gauge products and daily models do not resolve.

## Limitations

- GR4J is one model structure. X1 in GR4J is not exactly the root-zone capacity, and the proportional link
  X1 ~ Sr is an assumption (we also tested a free elasticity). Other structures (for example with a separate
  root-zone store) can respond differently.
- The mass-curve Sr uses a fixed evaporation fraction from 1956-1996. Results depend on the 20-year or 3-year
  memory and on multi-year accumulation (the annual-reset version predicts almost nothing).
- Differential evolution with a limited budget (popsize 8, 50 generations, then polish) leaves some
  optimiser noise in M1 - M0 differences, probably a few percent per catchment.
- Record ends differ (2014-12, 2020-02 or 2022-02 by source). Quality codes were not used to filter days.
- The North-AU control has a different climate (monsoon) and a positive observed residual after 2009.
  Part of that residual can be a model error, not a real gain.
- Deviations from the plan, made to save compute: the SILO refits, the annual-reset and the free-elasticity
  models were run for SE-AU only, and the calibration budget was smaller than first written.
- The FE statistic as defined in the plan (mean of catchment ratios) gives most weight to low-flow
  catchments. The volume-weighted view was added after we saw the data. We report both.

## Files

- `files/ANALYSIS_PLAN.md`: plan written before the analysis.
- `files/code/`: `build_daily.py` (data extraction), `gr4j.py` (numba GR4J, deficit, KGE),
  `fit_catchments.py` (calibrations), `analyze.py` (outcomes), `figures.py`, `reproduce.sh`.
- `files/results/summary.csv`: FE and rho per group, rain product, period and model, with bootstrap CIs.
- `files/results/extra.json`: volume-weighted results, terciles, contrasts, diagnostics and fit statistics.
- `files/results/catchment_results.csv`: per-catchment period changes, parameters and capacity ratios.
- `files/results/annual_series.csv.gz`: annual observed and simulated flow per catchment (AGCD), and the
  annual deficits.
- `files/figures/`: Figures 1-5.
- `files/provenance/`: hashes of the CAMELS-AUS members and the shared dataset records.
- `files/DATA_NOTICE.md`: external data sources, terms and required credit.

## Reproduction

Run `bash files/code/reproduce.sh <dataset root> <bundle 871b2192 zip> <scratch dir> <out dir>`. The dataset
root holds `camels-aus-v2.03-zenodo14289037-hydrometeorology/05_hydrometeorology.zip` (SHA-256
458e611f8df42ac56a8651e169ffdc9bf7084c363a336d5c648be44971648ecb) and
`camels-aus-v2.03-zenodo14289037-streamflow/03_streamflow.zip` (SHA-256
863443419ca37c81b6a76061115698c34fa92475cbb4bffceb72380e06bc4cf3), from Zenodo record 14289037.
The script needs Python 3.12 with numpy, scipy, pandas, matplotlib and numba 0.68.1 (see
`files/environment.txt`). It writes only to the given scratch and output directories. The calibrations took
about 2.5 h with 2 processes on a loaded host. The intermediate daily array had SHA-256
36792614c8cdc379b9ae5dbc53864eea5e26aecd8411dd5f805af7fc0683a3dc in this run.

## References

- Fowler, Zhang and Hou (2025), CAMELS-AUS v2, ESSD 17:4079, doi:10.5194/essd-17-4079-2025.
- Perrin, Michel and Andreassian (2003), GR4J, J. Hydrol. 279:275, doi:10.1016/S0022-1694(03)00225-7.
- Gao et al. (2014), GRL 41:7916, doi:10.1002/2014GL061668.
- Wang-Erlandsson et al. (2016), HESS 20:1459, doi:10.5194/hess-20-1459-2016.
- Tian et al. (2022), HESS 26:4853, doi:10.5194/hess-26-4853-2022.
- Trotter, Saft, Peel and Fowler (2023), MODSIM2023, https://mssanz.org.au/modsim2023/files/trotter.pdf.
