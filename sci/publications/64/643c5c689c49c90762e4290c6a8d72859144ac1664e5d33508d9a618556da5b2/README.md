# Aftershock decay rate (Omori-Utsu p) did not increase with surface heat flow for 191 shallow Japanese M4.5+ sequences (JMA 1998-2023, GHFDB R2024)

## Summary

Kisslinger and Jones (1991) reported that aftershocks in southern California decay faster
(larger Omori-Utsu exponent p) where the surface heat flow is higher. A later study of
18 Japanese sequences found no such link. Thus it is not clear if crustal temperature controls aftershock decay. We tested the link again with a larger
and more uniform sample from Japan.

We selected isolated shallow (depth 30 km or less) mainshocks of JMA magnitude 4.5 or more
from the JMA unified hypocenter catalog for 1998-2023. For each sequence, we fitted the Omori-Utsu rate
`mu + K (t + c)^-p` by maximum likelihood over 0.02-365 days. The background rate `mu` was fixed
from the year before the mainshock. We assigned to each epicenter the median heat flow of the
IHFC Global Heat Flow Database (GHFDB, release 2024, version 2026.03) within 50 km.

Main result (pre-specified primary test, n = 191 sequences in 76 one-degree cells):

| Quantity | Estimate | 95% interval (1-degree cell block bootstrap) |
| --- | --- | --- |
| Spearman rho, p vs heat flow | 0.005 | -0.163 to 0.188 |
| Random-effects slope of p per decade of heat flow | 0.10 | -0.11 to 0.34 |
| Same slope with controls (magnitude, depth, onshore, Mc) | 0.16 | -0.05 to 0.40 |
| Median p by heat-flow tercile (11-54 / 55-96 / 98-329 mW/m^2) | 1.11 / 1.09 / 1.11 | - |

- p did not change clearly with heat flow. The rank correlation is near zero.
  Correlations above about 0.19 are outside the 95% interval.
- 14 pre-specified sensitivity variants gave the same result: other heat-flow radii, onshore
  heat-flow sites only, onshore or offshore epicenters only, M 5.0 or more, depth 15 km or less,
  100 or more events, fit start 0.1 d or 1 d, fit end 100 d, Mc + 0.3, and the original
  (pre-amendment) selection rules. All 15 Spearman intervals include zero (Figure 3).
- The weighted regression slopes are positive in all 15 analyses (0.01-0.21 p per decade
  without controls, 0.05-0.22 with controls). These analyses share most of their data and are
  not independent. Only one variant (heat flow within 30 km, n = 121) has slope intervals that
  exclude zero (0.01-0.42 without controls, 0.04-0.44 with controls). Thus a weak positive slope
  of at most about 0.4 p per decade is possible. Over the interquartile heat-flow range of
  this sample (48-110 mW/m^2, 0.36 decade), that is a change in p of at most about 0.15. This is
  smaller than the spread of p between sequences (random-effects tau = 0.18). The weighted slope
  gives most weight to large, well-fitted sequences. The rank correlation gives equal weight to
  each sequence. Thus the two measures can differ.
- Secondary outcomes also showed no clear link to heat flow: log10 c (rho -0.01, -0.21 to 0.18),
  and magnitude-normalized productivity N(M >= Mmain - 2, 0.05-30 d) (rho 0.11, -0.06 to 0.26,
  n = 287). The distance to the nearest Holocene volcano, a second temperature proxy, also gave
  no link to p (rho -0.02, -0.14 to 0.10, n = 284).
- Power check: in synthetic catalogs with the same sequences, event counts, background rates
  and between-sequence scatter, an injected slope of 0.25 p per decade gave a mean rho of 0.27.
  The test detected it (interval above zero) in 19 of 20 runs. Slopes of 0.5 and 1.0 were
  detected in 20 of 20 runs. With no slope, 1 of 20 runs gave a false detection (Figure 4).
  The observed rho (0.005) is far below the values that a slope of 0.25 or more gives. The
  synthetic catalogs do not include spatially correlated residuals. Thus the bootstrap intervals
  on the real data are wider than the spread in the simulations.

Conclusion: In this Japanese sample, surface heat flow does not explain the variation of
aftershock decay rate between sequences. A strong heat-flow control of the kind reported for
southern California is not present at the scale that 50 km surface heat-flow medians can
resolve.

## Figures

- `files/fig1_map.png`: GHFDB heat-flow sites and the fitted sequences, colored by p.
- `files/fig2_p_vs_heatflow.png`: p against 50 km median heat flow, for all sequences and for
  onshore epicenters, with sextile medians.
- `files/fig3_sensitivity.png`: Spearman rho and adjusted slope with 95% block-bootstrap intervals
  for the primary test and the 14 variants.
- `files/fig4_power.png`: recovered rho for synthetic catalogs with an injected p-heat-flow slope.

## Data

All inputs were read in place from the campaign shared dataset store. Exact paths, source URLs and
SHA-256 hashes of every file used are in `files/data/provenance_inputs.json`. All recorded hashes
matched the files on 2026-11-09.

| Data | Source | Use |
| --- | --- | --- |
| JMA unified hypocenter catalog, yearly files h1998-h2024 | https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip | Mainshocks, aftershocks, background |
| IHFC Global Heat Flow Database R2024 v2026.03 | doi:10.5880/fidgeo.2024.014 | Heat flow (0 < q <= 1000 mW/m^2) |
| Smithsonian GVP Holocene volcanoes (WFS, 2026-11-09) | https://volcano.si.edu | Distance to volcano |
| Natural Earth 10 m land v5 | https://naciscdn.org/naturalearth/10m/physical/ne_10m_land.zip | Onshore flag, maps |

We do not include the JMA catalog (82 MB as parquet) in this package. Step 1 of the code
rebuilds it from the yearly zip files. The package includes the derived per-sequence tables, the
GHFDB points used near Japan, and all statistics.

## Methods

The pre-specified plan, with one dated amendment, is in `files/analysis_plan.md`.

1. Catalog. We parsed all `J` hypocenter records. We removed low-frequency events (subsidiary flag 5). 4,932,692
   records, 1998-01-01 to 2024-12-31.
2. Mainshocks. Magnitude 4.5 or more, depth 30 km or less, 24-46 N, 122-150 E, origin before 2024-01-01.
   Window radius R = min(100 km, max(10 km, 2 L)), with L the Wells and Coppersmith (1994)
   subsurface rupture length. Isolation: we removed a candidate if an event of equal or larger magnitude
   occurred within max(2R, 30 km) in the previous 365 days, or within R in the next 365 days.
   4,567 candidates gave 450 isolated mainshocks.
3. Aftershocks: events within R (epicentral), depth 50 km or less, 0-365 days. Mc = maximum-curvature
   magnitude of aftershocks on days 1-365, plus 0.2. Sequences with fewer than 20 events
   on days 1-365 have no Mc and we did not use them.
4. Fit. Maximum likelihood with analytic gradients (L-BFGS-B, nine starting points) over
   [0.02, 365] d. mu = rate of M >= Mc events within R in the prior 365 days. Standard error of p
   from the numerical Hessian. Quality control: at least 30 events, converged, 0.2 < p < 3, c < 5 d,
   s.e.(p) < 1. 346 fitted, 284 passed, and 191 had at least 3 heat-flow values within 50 km.
   A synthetic test recovered p = 0.83, 1.07 and 1.51 for true p = 0.8, 1.1 and 1.5 (500 events).
5. Statistics. Spearman rho of p and heat flow. Random-effects weighted least squares of p on
   log10 heat flow (weights 1/(se^2 + tau^2)), with and without controls. Every interval
   comes from a block bootstrap that resamples one-degree cells (5,000 draws for the primary test, 2,000 for the
   variants). Nearby sequences share heat-flow values, so a sequence-level bootstrap would give
   intervals that are too narrow.
6. Power. We simulated Omori-Utsu plus background catalogs for each of the 191 sequences with its own
   fitted c, background rate and event count. We set p_true = median p + beta (log10 HF - mean) +
   N(0, tau^2), with tau = 0.18 from the primary fit. Then we refitted the catalogs and repeated the
   Spearman test with a 500-draw block bootstrap, 20 times for each beta = 0, 0.25, 0.5, 1.0.

## Limitations

- Surface heat flow is a coarse proxy for the temperature at hypocentral depth. The GHFDB coverage
  in Japan is uneven. Many offshore values come from marine probes, and 93 of the 284 good fits had
  fewer than 3 values within 50 km. A link between p and temperature at depth that the
  surface data cannot resolve is still possible.
- Isolation and window rules are simple (no ETAS declustering). Secondary sequences inside
  the windows can bias single-sequence Omori fits, especially over 365 days. The fit-end-100-d
  and fit-start variants partly address this.
- The maximum-curvature Mc can be too low early in a sequence. The fitted c absorbs part of this,
  and the start-time and Mc + 0.3 variants gave the same result.
- Our selection (M 4.5+, 1998-2023, depth 30 km or less) is not the same as Kisslinger and Jones (1991) or the
  earlier 18-sequence Japanese study. We did not repeat the California analysis.
- After the first run, and before we computed any heat-flow statistic, we changed the minimum
  magnitude, the Mc rule and the radius cap (amendment in `files/analysis_plan.md`). The original-rule
  result (n = 47) is in Figure 3 and is also null.
- We did 14 variants and 3 effect measures. We did not correct for multiple tests. The single
  variant with slope intervals that exclude zero (30 km radius) does not agree with the 50 km and
  100 km radii.

## Reproduce

```
# from a directory where ./datasets is the campaign shared dataset store
OUT=out bash files/code/run_all.sh
```
`run_all.sh` runs: `01_parse_jma.py` (catalog), `02_sequences.py` (selection and fits; arguments:
fit start, fit end, Mc offset, minimum magnitude), `02_sequences_v0_original_rules.py` (selection
rules before the amendment), `03_covariates.py` (heat flow, volcano distance, onshore flag),
`06_summary.py` (all tests, writes `sensitivity.csv` and `results.json`), `07_power.py` (power
simulation) and `05_figures.py`. Use Python 3.12 with numpy, pandas, scipy, geopandas, shapely, matplotlib and pyarrow.
Set `OMP_NUM_THREADS=1` (the script does this). The fits use many small array operations, and
threaded BLAS made them about 100 times slower on our busy shared host. Our main fit runs used
threaded BLAS and took about 2 h of wall time each. The results do not depend on the thread count.
The `seq_v0` table in this package came from the first run (numerical gradients). The v0 script
uses the analytic-gradient fitter, which agreed to 1e-4 in p on the amended sample.

## Files

- `files/code/`: all analysis code.
- `files/analysis_plan.md`: pre-specified plan and amendment.
- `files/data/seq_main_cov.csv`: the primary table, one row per isolated mainshock. Columns: time, location,
  magnitude, R, Mc, event counts, background rate, K, c, p, s.e., heat-flow values (30/50/100 km,
  onshore-only, inverse-distance), volcano distance, onshore flag, cell.
- `files/data/seq_{ts0.1,ts1,T100,mc0.3,v0}_cov.csv`: sensitivity fit tables.
- `files/data/ghfdb_japan_points.csv`: GHFDB values used (20-50 N, 118-154 E), with IDs.
- `files/data/sensitivity.csv`, `files/data/results.json`: all test results.
- `files/data/power.csv`: power simulation results.
- `files/data/provenance_inputs.json`: input paths, URLs and hashes.

## Provenance of this work

Job sci-1107-hp-earth-and-ocean-sciences-f6767f903db4, campaign 11_07_2026, topic
earth-and-ocean-sciences, machine hp, account claude-andrii. Analysis and text by the model
Claude Opus 5.5 (claude-opus-5-5) acting as an automated research worker. The signing key is a
campaign-machine key. It is not a personal authorship claim. Date: 2026-11-09.

## References

- Kisslinger, C., and L. M. Jones (1991), Properties of aftershock sequences in southern California,
  J. Geophys. Res., 96(B7), 11947-11958. doi:10.1029/91JB01200
- Utsu, T., Y. Ogata, and R. S. Matsu'ura (1995), The centenary of the Omori formula for a decay law of
  aftershock activity, J. Phys. Earth, 43, 1-33. doi:10.4294/jpe1952.43.1
- Ogata, Y. (1983), Estimation of the parameters in the modified Omori formula for aftershock
  frequencies by the maximum likelihood procedure, J. Phys. Earth, 31, 115-124. doi:10.4294/jpe1952.31.115
- Wells, D. L., and K. J. Coppersmith (1994), New empirical relationships among magnitude, rupture
  length, rupture width, rupture area, and surface displacement, Bull. Seismol. Soc. Am., 84, 974-1002.
- Global Heat Flow Data Assessment Group et al. (2024), The Global Heat Flow Database: Release 2024,
  GFZ Data Services. doi:10.5880/fidgeo.2024.014
- Dascher-Cousineau, K., E. E. Brodsky, T. Lay, and T. H. W. Goebel (2020), What controls variations in
  aftershock productivity?, J. Geophys. Res. Solid Earth, 125, e2019JB018111. doi:10.1029/2019JB018111
- The earlier 18-sequence Japanese study (JMA catalog, M 5.5+, no heat-flow link) is known to us only
  through its abstract, as found in a web search; we could not retrieve the full text.
