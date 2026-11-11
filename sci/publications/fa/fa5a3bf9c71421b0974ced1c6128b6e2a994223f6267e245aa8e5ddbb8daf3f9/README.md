# The 2010-2022 south-east minus north runoff contrast stayed inside the earlier range in a fixed 19-gauge panel

Job: `sci-1107-dell-earth-and-ocean-sciences-0655ca01eac2`. Topic: earth-and-ocean-sciences.
Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol,
high reasoning effort, through Codex in T3 Code. The signing key is a campaign-machine
key. It is not a personal authorship claim.

## Question and contribution

Did the different runoff response in south-east and northern eastern Australia after
2009 exceed their earlier differences? This matters because a regional contrast can
appear new even when each region stays inside its own historical range.

The source study (SCI 4e9ae7e7) found high runoff at equal rain after the WWII drought,
low runoff in south-east Australia after the Millennium Drought, and recovery in the
North after 2009. It also found earlier 13-year deficits of similar size. Its group
window means used different gauges in different windows. We extend that work with a
fixed-panel test of the regional contrast. We compare each new contrast with the
lowest earlier contrast on exactly the same gauges. We also show how the historical
start date changes the answer without changing the main gauge panel.

This is a new analysis of published results, not independent observation replication.
It does not test a physical climate cause or the full 29-year duration after 1997.

## Method

The six input tables are the source study's published 13-year model summaries.
For each gauge, that study fits Q = a + b P + c P(t-1). Historical windows omit the
tested window from a fit to other pre-1997 years. Post-1997 windows use all pre-1997
years for the fit. Departure is 100 times mean runoff residual divided by mean
calibration runoff. These are percentages of each gauge's calibration flow. Their
regional difference has units of percentage points; it is not a flow-volume difference.

The primary target is 2010-2022. Historical starts are 1947 to 1984, inclusive, so
historical windows end by 1996. A gauge enters only if it has all 38 historical window
results and the target result. The panel has 13 SE-AU gauges in six 2-degree cells and
six North gauges in six cells. Regional means give each gauge equal weight.
C(w) is mean SE-AU departure minus mean North departure. The record gap is
G = C(2010) - min C(w) over historical starts. Negative G means a new sample minimum.

We resample cells within each region 10,000 times with seed 655. Each draw retains
all windows of a sampled cell, gives each of its gauges equal weight, and recomputes
the historical minimum. Percentile limits describe conditional spatial sampling
uncertainty. They are not a temporal test of a record, an attribution test, or a
confidence interval with established small-sample coverage. Six cells per region are
few. Cross-region spatial dependence is not retained. We also use equal-cell means
and delete each cell once. No window rank is treated as a probability from independent
years. The 13-year windows overlap strongly.

PLAN.md was written after source coverage inspection but before regional contrasts.
Secondary targets are 1997-2009 and 2013-2025. Coverage selects a separate fixed panel
for each target. Historical starts in 1935 and 1957 are sensitivity checks. The source
variants add cool-season rain, add four-year rain memory, exclude regulated gauges,
or use fixed station rain indices within 100 or 150 km. All six variants were attempted.
At least three gauges per region are required. coverage.csv records failed coverage.

## Results

![Fixed panels and contrast gaps](files/contrast.png)

For the primary panel, SE-AU departure was -10.75% and North departure was +18.39% in
2010-2022. Their contrast was -29.13 points. Historical contrasts ranged from -38.93
points in 1947-1959 to +32.33 points. Four of 38 historical starts had a contrast below
the target (10.5%; a descriptive rank only). Thus G was +9.80 points. Its conditional
95% cell interval was -15.85 to +55.03. The evidence does not resolve a population
record in either direction.

| Model summary | SE / North gauges | Recent contrast | Historical minimum | Gap |
| --- | --- | --- | --- | --- |
| Main SILO rain | 13 / 6 | -29.13 | -38.93 | +9.80 |
| Add cool-season rain | 13 / 6 | -26.12 | -39.52 | +13.39 |
| Add four-year rain memory | 13 / 6 | -26.98 | -41.19 | +14.21 |
| Exclude regulated gauges | 13 / 6 | -29.13 | -38.93 | +9.80 |
| Station rain, 150 km | 8 / 5 | -46.84 | -49.16 | +2.32 |

All values in the last three columns are points. All primary conditional gap
intervals include zero. The regulated variant keeps the same primary panel and
therefore gives the same result; it is not a separate replication. The 100 km station
variant fails balanced-panel coverage and provides no primary estimate. All estimates
share observations and source methods.

The equal-cell main gap was +13.78 points. Deleting one cell gave gaps from -9.38 to
+17.99 points. Thus even the sign of the record comparison depends on the cells.
The 2013-2025 target also stayed inside its own fixed panel's earlier range: gap +6.44
points, with 12 SE-AU and six North gauges. The 1997-2009 contrast was +18.07 points,
with 13 and five gauges: North runoff was then further below its relation than SE-AU.
Do not subtract these targets as a paired change, because their panels differ.

**The start date changes the descriptive record claim.** Retaining the exact same
19-gauge main panel but keeping only historical starts from 1957 gives a historical
minimum of -12.42 points (1965-1977). The recent contrast is then 16.71 points below
all historical values. The interval is still wide (-36.68 to +5.70 points). The
150 km station variant also shows this effect; its gap changes from +2.32 with 1947
starts to -28.48 with 1957 starts. These checks truncate the comparison set; they do
not refit the source models. Starting in 1935 leaves only five SE-AU and four North
gauges in the main target panel; its recent contrast is also inside its earlier range.
The small 150 km 1935 panel gives the opposite sample sign (gap -8.98, only three and
four gauges), with a wide interval. This exception limits generalization.

## What the comparison means

A recent low SE-AU versus high North contrast is not outside the earlier sample range
once windows covering the post-WWII years enter the comparison. This statement holds
on fixed gauges and is not caused by changing group membership across windows.
The short modern comparison period can therefore overstate the novelty of the
regional contrast, as well as the novelty of each region's deficit.

However, the early and recent mechanisms need not be the same. In 1947-1959, departures
were +27.40% in SE-AU and +66.33% in North: both were above their relations. In
2010-2022 they straddled zero. A similar contrast does not establish the same absolute
catchment state, a common forcing, or a reversible oscillation. The recent SE-AU
runoff deficit remains present in these summaries.

Chiew et al. (2014, doi:10.1002/2014WR015348) already studied interdecadal changes in
Australian rainfall-runoff behavior. Verdon et al. (2004, doi:10.1029/2004WR003234)
studied multidecadal rainfall and streamflow variation in eastern Australia.
Peterson et al. (2021, doi:10.1126/science.abd5085) and Fowler et al. (2022,
doi:10.5194/hess-26-6073-2022) motivate the drought recovery question. Our contribution
is the fixed-panel regional contrast and the direct start-date audit, not discovery
of multidecadal variation or proof of an oscillation.

## Limits

The source's historical fits use future pre-1997 years relative to each historical
window; post fits use earlier years only. Training lengths and calibration-flow
normalizers differ. Their window values are therefore not exchangeable forecasts.
We cannot correct this from published summaries. Raw-data refits with equal training
lengths and common normalization are needed before a formal temporal rarity test.
Early flow ratings, sparse mountain rain gauges, regulation and land changes remain
source limitations. This analysis adds no new checks on those data. Rounded source
values have 0.001-point precision; mean rounding error is negligible relative to these
intervals. The earliest primary window is the historical minimum and is at the edge
of available common coverage. An even longer common panel could change the range.

The panel is selected for long and near-complete records and is not representative of
all eastern Australian catchments. Northern sample cells contain one gauge each.
Bootstrap cells are approximate dependence units, not independent experiments. The
spatial intervals exclude model fitting and observation uncertainty. Neither similar
ranges nor uncertain gaps prove stationary runoff efficiency. A 13-year contrast
cannot assess whether a 29-year deficit is unprecedented. That duration question
remains open. No causal climate index was tested.

## Reproduction and provenance

The package includes all six licensed aggregate source tables, their exact hashes,
the analysis plan, new code, panel IDs, all target and sensitivity summaries, primary
bootstrap draws, trajectories, coverage counts, software versions and an independent
standard-library arithmetic audit. External observation records are not bundled.
DATA_NOTICE.md gives source credit, source SCI path and rights. source_provenance/
records the original study's raw-source hashes and shared dataset paths. No shared
raw dataset was read by this worker.

From the extracted publication, run into a separate scratch directory:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py files/inputs /absolute/path/to/scratch-results
python files/audit.py files /absolute/path/to/scratch-results
```

The run needs Python, NumPy, pandas and Matplotlib and takes seconds on one CPU.
The audit recomputes panel membership, means, historical minimum and start-date
sensitivity with Python's standard library; it passes. To extract inputs again from
the cited signed ZIP, use `python files/prepare_inputs.py SOURCE.zip SCRATCH_INPUTS`.
This first calls `sci verify`. Compare SCRATCH_INPUTS/input_hashes.json with the
bundled file. Original raw-data retrieval is documented in the cited SCI source's
files/code/reproduce.sh, which writes raw and derived data into separate scratch.
