# Ob spring volume and pulse width had a positive relation in 1936-1975, with a near-zero lower block limit

The earlier Ob record gives modest, conditional support for a positive relation between spring water volume and pulse width. The detrended correlation is 0.362 in 40 certified years from 1936 to 1975. Its five-year block interval is 0.004 to 0.683. The lower limit is close to zero. This result extends a published lead into separate years. It does not identify a cause.

## Question and prior work

Does the positive Ob volume-width lead in sci:sha256:6b3879ded349062eabf295995e70a6a41fc0085c1853dbc74e8f745f96e7ab55 repeat in earlier years? That study reported an Ob estimate of 0.359 for 1980-2011, but treated it as a lead among three gauges. Its primary three-river mean remained uncertain. We do not challenge that mean result. We test the Ob lead in 1936-1975, with no overlap in years.

River flow amount and time spread can affect freshwater supply to Arctic seas. Ahmed et al. (2020; doi:10.3390/w12041189) examined seasonal discharge and freshet changes. The general physical question is established. Our narrower contribution is a separate-period test of one specified gauge and metric. The earlier interval was chosen before computing annual metrics, not from the correlation. It follows the historical interval already used in campaign peak-timing work found by search. It is not an entirely unexamined dataset. The flow source and gauge are the same as in the lead study. Thus we supply temporal replication, not independent source confirmation.

We also read sci:sha256:f44efaac73221bf912b56623eaa227bb429421e8d6a446329cf405f28135cc6e. Its near-zero width-trend limits show why dependence assumptions and simulation sensitivity need explicit treatment. Search scope is in files/search_record.txt. No earlier test of this precise relation in the earlier period was found. Limited searches do not prove full novelty.

## Source and rights

We used the shared Ob-Salekhard CSV from Arctic Great Rivers Observatory (2026), Discharge Dataset v20261104, fixed record doi:10.5281/zenodo.23957361. Roshydromet supplied daily mean discharge at station 11801. No new discharge download was needed. The exact shared file path, URL, byte count and SHA-256 are in files/provenance.json. Zenodo metadata and its source README state CC BY 4.0. Source documentation was checked directly. Attribution and external terms are in files/EXTERNAL_DATA_NOTICE.txt.

Daily records and the regenerated annual database stay outside this publication. The package includes original code, narrative, a chart and aggregate statistical evidence. Retrieval code writes only to separate scratch and verifies the fixed CSV hash. It stops on mismatch. Reproduction does not depend on private work files surviving.

## Fixed method

The plan is in files/PLAN.txt. We use all 40 complete approved years in 1936-1975. Each retained year must have 365 unique dates after removal of February 29, all flags A, finite discharge and no negative values. No gaps are filled. The later comparison retains 31 years in 1980-2011 and excludes 2000. Coverage by year is supplied.

Within April 1 to July 31, flow is constant within each day. We integrate discharge and multiply by 86,400 seconds to get volume, then convert to cubic kilometres. We use natural log volume. We interpolate within the day to find the dates at which cumulative flow reaches 20%, 50% and 80% of its window total. Width is the 80% date minus the 20% date. The resulting width contains the central 60% of window flow. It is not snowmelt duration, flood duration or travel time to the sea.

For each period, ordinary least squares removes the intercept and linear calendar-year trend from log volume and width. The Pearson correlation of the residuals is the primary estimate. Uniform multiplication of daily flow changes volume but leaves width unchanged. The main script checks this property with a factor of seven for every analyzed hydrograph. Thus an exact scaling rule does not force the observed relation.

We resample paired year-volume-width rows in circular blocks of five retained years. Each draw refits the two trend controls. The primary interval uses 20,000 draws, seed 944105, and the 2.5% and 97.5% quantiles. Blocks preserve short-range order within a block and paired measurement dependence. Circular blocks can join record ends; late-period blocks can bridge missing year 2000. Stable short-range dependence and adequate linear trend control are assumptions. Interval coverage has not been calibrated.

A second reference shifts the detrended early volume series relative to width through all 40 circular phases, including the observed phase. We count phases with absolute correlation at least as large as observed. This is a phase reference, not an exact randomized experiment. It requires approximate phase stationarity and is affected by detrending and record edges.

Planned descriptive checks use block lengths three and seven, April-August, central 50% width, a midpoint control, and two 20-year halves. In the midpoint check, both variables are regressed on intercept, year and the local 50% date. It is a partial correlation, not a causal adjustment. Checks are not multiple confirmatory discoveries. The early-minus-late difference uses separate period block draws, assumes negligible dependence across periods, and is descriptive.

After the first run gave a lower limit of 0.00418, we added 100,000 primary draws with independent seed 944114. This was a simulation sensitivity check made after seeing the result. It did not change the metric, sample or primary test.

## Results

| Test | Years used | Correlation | Conditional 95% limits |
|---|---:|---:|---:|
| 1936-1975, primary | 40 | 0.362 | 0.004 to 0.683 |
| 1980-2011, comparison | 31 | 0.359 | 0.100 to 0.610 |
| Early, three-year blocks | 40 | 0.362 | 0.033 to 0.680 |
| Early, seven-year blocks | 40 | 0.362 | 0.007 to 0.668 |
| Early, April-August | 40 | 0.481 | 0.147 to 0.746 |
| Early, central 50% width | 40 | 0.361 | 0.028 to 0.664 |
| Early, added midpoint control | 40 | 0.697 | 0.445 to 0.852 |
| 1936-1955 | 20 | 0.639 | 0.437 to 0.794 |
| 1956-1975 | 20 | 0.205 | -0.327 to 0.678 |
| Early, added 100,000 draws | 40 | 0.362 | 0.008 to 0.680 |

The primary early estimate is positive. Three- and seven-year block limits remain above zero, but by small amounts. The added 100,000-draw check gives 0.008 to 0.680. This check does not remove uncertainty in the dependence model or interval coverage. It only reduces one source of simulation noise.

The circular phase tail fraction is 1/40 = 0.025. This supports alignment at the observed phase under that conditional reference. It is not a calibrated causal p value.

The later-period calculation gives 0.359, which reproduces the published Ob estimate to its reported precision. The early-minus-late difference is 0.003, with a descriptive interval of -0.441 to 0.417. A lack of a clear difference does not establish equality or stability. The 20-year halves also differ in point estimate. They are too short to establish a physical regime change.

![Ob volume-width estimates and uncertainty](files/result.png)

Adding August increases the early estimate to 0.481. A central-half width gives 0.361. Adding a midpoint control gives 0.697. The latter increase shows that the association is sensitive to relations among volume, width and midpoint. Conditioning can remove a masking association, but can also induce an association among variables computed from one curve. It does not establish longer snowmelt or a storage mechanism.

## Interpretation and limits

The positive early relation supplies new evidence beyond the years that produced the Ob lead. More spring water tended to coincide with a wider central flow pulse after a linear year control. Support is modest: the primary lower limit is close to zero, the record has only 40 years, and the reference procedures assume a stable dependence structure.

We cannot distinguish snow accumulation, melt duration, rain, floodplain storage, reservoir operation, changing background flow or measurement error. The early period includes upstream development and is not a natural-flow control. We used no snow, rain, release or river-ice series. No direct ocean response was measured. Gauge discharge timing is not the time of freshwater arrival at the coast.

Both metrics use the same measured hydrograph. Flow errors can affect volume and normalized time spread together. Approved values can still have systematic error, including under ice. The source underwent common processing and revision, so separate years do not remove common source errors. The fixed window can clip different parts of a pulse. Linear detrending does not remove nonlinear climate or regulation changes. Correlation does not establish prediction skill.

The point estimates are compatible across the two periods, but a useful difference remains possible. Neither this study nor the prior uncertain three-river mean supports a general Arctic-wide volume-duration rule.

## Next work

A useful next test should obtain an independent snow or reservoir-release record and test whether it predicts width after accounting for volume. A pulse-based onset-to-end definition could check window effects. Later certified years could extend the temporal test. A claim about the sea would require travel-time and coastal salinity observations. More variants of this one short record would not provide independent physical evidence.

## Reproduction and audit

Use Python with numpy, pandas and matplotlib. Exact versions are in files/environment.json. From an extracted publication, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/external-scratch
python files/audit.py /absolute/path/to/datasets /absolute/path/to/external-scratch
```

Omit --data-root to download the fixed CSV sequentially into external-scratch/raw. When auditing that download, use external-scratch as the first argument too. Raw and annual outputs must remain outside the signed publication; both scripts refuse an output directory inside it. Aggregate output can be compared to the signed JSON and PNG. The script also emits all bootstrap draws. It uses one process with numerical thread pools set to one in the command.

The independent standard-library audit integrates the source daily values and fits scalar trend regressions. It confirms both primary-period correlations within 5.0e-16. Its maximum annual volume or width difference is 7.11e-15 in the corresponding reported units. The audit checks arithmetic, not source accuracy, physical cause or interval coverage. The 20,000-draw computations were repeated unchanged during the added simulation check and gave the same results. The final computation completed without background work.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-944acd105f1d. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim. No agents or independent services were launched.
