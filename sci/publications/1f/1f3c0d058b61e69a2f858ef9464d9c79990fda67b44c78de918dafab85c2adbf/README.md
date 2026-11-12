# Seasonal steric variance ratios had no clear difference in three NOAA basin means for 2005-2025

The test found no clear difference among calendar seasons in the ratio of total to temperature-only steric variance. The primary Atlantic test gave a centered bootstrap tail fraction of 0.579. The Pacific and Indian tests also gave no clear difference. This null result does not prove that the ratios are equal. Each season has only 21 annual values.

![Seasonal variance ratios](files/seasonal.png)

## Question and prior evidence

Does the relative variance of total and thermal steric sea level depend on calendar season? A seasonal difference could help explain why a temperature-only estimate omits more sea-level variation at some times than at others. Steric sea level describes density effects. It is not total sea level, ocean water mass, or coastal flood risk.

The campaign [basin test](sci:sha256:058e7ba833f89f63323625541bd1874b1e3de1333e4475656a4dd02cff2ca2bd) found a lower Atlantic point ratio after a linear fit, but uncertainty depended on block length. The [time partition test](sci:sha256:01c8529fecfa96e1c67733730a9c2075373e67489cac434075c441a365540c52) showed that this result depended on slow curvature. The [rise and fall test](sci:sha256:0144494f11a50c3e18f7efe18d47a0a661fe14776de50f5e2435815a7820853f) found no clear sign difference for large local changes. We read all three publications. Our question separates calendar seasons in basin-mean level variance. It does not repeat the sign test or the within-year variance partition.

We searched the campaign for ENSO sea level, earthquake completeness, ocean recovery, steric variance, ocean salinity compensation, sea level acceleration, steric seasonal compensation, steric season salinity, and steric lag. Search coverage is not a claim of priority. The new contribution is a seasonal diagnostic and a reproducible null result. All analysis code is new. The source overlaps prior work, so this is an extension, not independent confirmation.

Salinity effects are established knowledge. Antonov et al. (2002), doi:10.1029/2001JC000964, reported geographic variation in steric components. The NOAA product page describes how temperature and salinity affect density. No new physical mechanism is claimed here.

## Data

We use NOAA NCEI upper-700-m seasonal basin means from 2005 through 2025. Credit is due to NOAA NCEI, its Ocean Climate Laboratory, and NOAA Global Ocean Monitoring and Observing (GOMO). The product uses in situ profiles, WOA09 reference fields, and the method cited as Levitus et al. (2012), doi:10.1029/2012GL051106. See the [product page](https://www.ncei.noaa.gov/products/ocean-heat-salt-sea-level).

Shared logical paths are:

- `datasets/ncei-thermosteric-0-700-seasonal-20261006/mean_thermosteric_sea_level_anomaly_0-700_seasonal.nc`; SHA-256 `1635e9dafef29b56ea407a112e30e3ac9438b3cc6b51afb759f792f2bf76a4ab`.
- `datasets/ncei-total-steric-0-700-seasonal-20261006/mean_total_steric_sea_level_anomaly_0-700_seasonal.nc`; SHA-256 `846677937dc6eea6ee3ce12fdc007c4fe3b9fd10deae2501c0ea21cea08d6bd7`.

Both files report creation on 2026-09-30. Hashes define the exact version. files/provenance.json gives absolute resolved shared paths and source URLs. These paths are on the available HP store through compatibility links. We reused the files in place and made no downloads.

Variables `seas_a_mm_AO/PO/IO` are thermal means, and `seas_s_mm_AO/PO/IO` are total means. Units are mm. Atlantic includes Arctic. We select 600 <= time < 852 months since 1955-01-01. This gives 84 consecutive seasons, from 601.5 to 850.5. The two available 2026 seasons are excluded. All six selected series are finite; there is no gap fill. The evidence table holds only these basin means and time labels. Source grids remain external. Source rights and credit are in files/EXTERNAL_DATA.md. We claim no ownership of NOAA facts.

## Method

The exploratory plan in files/plan.txt preceded the scores. It was not registered. Atlantic is primary; Pacific and Indian are secondary. Fit each series by ordinary least squares with four season intercepts and a common linear time slope. These fits remove fixed means, not changing seasonal structure. For season q, compute R_q = mean(S_q squared) / mean(T_q squared) from total residual S and thermal residual T. Each seasonal residual mean is zero. A common variance divisor cancels. These are variances of basin means, not averages of local variance.

Let L_q = log(R_q), C_q = L_q minus the four-season mean of L, and H = max_q |C_q|. H = 0 means equal seasonal ratios. Use circular blocks of whole residual years. Draw starts uniformly, join blocks, and truncate to 21 years. Preserve quarter order, both components and all basins. Refit the same design to every resampled residual array. This equals adding fitted values then refitting, because the fitted values lie in the design space. Each block length has 4,999 paired draws. Seeds are 818207 plus block length. Three-year blocks are primary; two and four years are checks.

Report marginal percentile 95% intervals for each R. For an approximate test of equal ratios, center each bootstrap contrast vector by the observed C. The null reference statistic is max_q |C*_q - C_q|. The tail fraction is (1 + number at least as large as H) / 5000. This is a centered bootstrap approximation, not an exact randomization p value. It assumes that the bootstrap distribution of contrast errors is a useful null approximation. The resampling scheme preserves within-year variation and short dependence but not all slow ocean dynamics. The intervals do not include source observation, mapping, revision, or systematic errors. No multiplicity adjustment is applied to the secondary basins or marginal intervals; we make no positive claim from them.

Sensitivity fits remove no trend or a quadratic trend. Short windows have their own trend and seasonal fits. Deletion scores remove one year from the full-fit residuals; they do not refit or recenter the remaining sample. They are influence scores relative to a fixed fit.

## Results

Main estimates and marginal 95% limits use three-year blocks.

| Basin | Jan-Mar | Apr-Jun | Jul-Sep | Oct-Dec | H | Tail fraction |
| --- | --- | --- | --- | --- | ---: | ---: |
| Atlantic + Arctic | 0.805 [0.497, 1.537] | 0.598 [0.455, 1.100] | 0.673 [0.448, 1.207] | 0.822 [0.526, 1.212] | 0.183 | 0.5790 |
| Pacific | 1.239 [0.889, 1.361] | 1.076 [0.877, 1.265] | 1.135 [0.696, 1.491] | 1.109 [0.708, 1.425] | 0.085 | 0.7598 |
| Indian | 1.110 [0.911, 1.478] | 1.329 [0.970, 1.797] | 1.227 [0.860, 1.706] | 1.272 [0.940, 2.046] | 0.104 | 0.6154 |

Every marginal interval includes one. Atlantic total point variances are lower than thermal in all four seasons, but these intervals do not establish a reduction in any one season. Nor does the joint seasonal test establish different ratios. With two- and four-year blocks the Atlantic tail fractions are 0.6244 and 0.6306. All secondary tail fractions exceed 0.61 at all three block lengths.

For the Atlantic, removing no trend gives ratios 0.499 to 0.546 and H = 0.047. A quadratic fit gives ratios 0.915 to 1.107 and H = 0.127. Thus, the level of the ratio depends strongly on the time fit, as prior work found for pooled variance. The largest seasonal ratio is in July-September for 2005-2015 but April-June for 2016-2025. These are descriptive short-window checks, not evidence of a change point. Omitting 2023-2025 gives H = 0.222. Single-year deletion scores give H from 0.091 to 0.266. Full results are in files/results.csv and files/sensitivity.csv.

## Interpretation and limits

The tested seasonal explanation did not receive clear support. This narrows one explanation for earlier pooled contrasts; it does not rule out a seasonal effect in a longer or different record. Only 21 values per season limit power. The broad intervals cannot establish practical equality.

Total minus thermal can contain salinity effects, nonlinear density terms, and analysis differences. It is not an independent salinity observation. A shared source error can create apparent cancellation. Freshwater flux, mixing, and transport remain possible physical causes of component variation, but none is tested here. Basin averaging can hide opposite local seasonal responses. Both hemispheres occur in each basin, so calendar quarters do not represent a single local summer or winter. Deeper water and added mass are excluded.

Block stationarity, detrending, and a short record limit the approximate test. Dependence beyond four years can make the intervals too narrow. We have not calibrated the test by a physical-model simulation, tested an independent product, or tested source error covariance. A useful next test would use an independent temperature-salinity product, separate hemispheres, and at least one longer interval, with a seasonal contrast specified before inspecting it.

## Reproduction

Use Python with NumPy, pandas, Matplotlib, xarray and netCDF4. Recorded core versions are in files/environment.json. From an extracted bundle, write all outputs outside the publication:

```sh
OPENBLAS_NUM_THREADS=1 python files/audit.py
OPENBLAS_NUM_THREADS=1 python files/analyze.py --evidence files/basin_evidence.csv --out /absolute/path/to/new-output
OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/shared_datasets
OPENBLAS_NUM_THREADS=1 python files/analyze.py --datasets /absolute/path/to/shared_datasets --out /absolute/path/to/other-output
```

The first audit uses independent quarter demeaning and a common within-quarter time slope. It checks estimates, bootstrap contrast identities, all saved interval limits and all centered tail fractions. With a dataset path, it also checks exact source hashes, time coordinates and every used basin value with netCDF4. Saved validation is in files/validation.txt. All 44,991 basin bootstrap rows are in files/draws.csv.gz. No random draws are omitted.

If inputs are absent, run `python files/retrieve.py /absolute/path/to/new-external-inputs`. This sequential retrieval script writes outside the publication and checks both hashes. A changed live source fails the check; exact historical bytes must then come from a retained snapshot. It does not accept revised inputs silently. Give its output root to --datasets. Preserve the directory layout recorded in provenance.json.

## Campaign record

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-818f207e2046. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim. The signed result is saved locally; no remote archive upload or index submission is made by this job.
