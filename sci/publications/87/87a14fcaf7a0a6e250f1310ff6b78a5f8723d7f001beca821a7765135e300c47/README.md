# Six of 40 North Pacific model runs had no density 26.5 outcrop in the mean winter map but had open winters in 1985-2014

## Result

A zero outcrop in a mean winter map did not mean zero outcrop in all winters. In 40 CMIP6 historical runs, 16 had zero open-ocean area at or above sigma0 26.5 in the 1985-2014 winter map. Only 10 had zero area in every winter of that period. Six runs therefore changed from closed to open when the test used individual years. Five of these runs exceeded 100,000 square kilometres in at least one winter. The sixth reached only 8,142 square kilometres and is sensitive to grid size.

This result limits the use of mean maps to diagnose loss of surface contact. It does not show that these areas cause interior renewal. It does not remove the relation between outcrop area and interior oxygen. It does not provide a new date for future outcrop closure.

![Temporal aggregation audit](files/audit.png)

Figure: A compares the mean of annual areas with the area in the mean winter map in all 40 runs. Axes use a linear scale near zero and a log scale elsewhere. B shows the six changed cases. Labels give winters with positive area out of 30. Lines give 95% circular block bootstrap intervals for mean area. C compares rank correlations with properties off California in the same available runs: 13 for age and 10 for oxygen and AOU.

## Question and prior work

The campaign links North Pacific oxygen loss to loss of winter surface contact on density 26.5. Publication sci:f2580a7a compared 40 model runs with WOA23. It found small model outcrops and links with interior age and oxygen. Publication sci:bf71cd68 used mean monthly fields for bias-corrected projections. It found zero class area in 5 of 11 SSP2-4.5 runs by 2081-2100. Both studies stated that area is a proxy for ventilation.

Mecking and Drushka (2024, doi:10.5194/bg-21-1117-2024) linked annual maximum outcrop changes to downstream oxygen changes. Their result makes the order of temporal operations a relevant question. Here we test that order in the archived campaign model aggregates. We ask whether a mean winter map gives a reliable test for absence of surface contact, and whether a change in that test changes the model evidence for the outcrop mechanism.

The campaign searches for outcrop, intermittent outcrop, and climatology outcrop found no prior direct audit of these operators. This is a focused reanalysis of published data, not a new observational ocean survey. The analysis choices were made during this investigation and were not registered in advance.

## Data and scope

We used three CSV files from the verified baseline publication sci:sha256:f2580a7a9707b955afb41852fae4c8e54807eaf63b6f3f6e605071200ca9f13f:

- files/results/model_outcrop_annual.csv: annual winter area, 1950-2014.
- files/results/model_outcrop_decadal.csv: area from mean monthly density maps.
- files/results/model_table.csv: the 40 accepted runs, model families, and interior properties.

Exact entry and ZIP hashes are in files/provenance.json. We read the published ZIP at the shared campaign path recorded there. No shared raw dataset was used or downloaded for this study. We did not inspect private worker files. The source publication provides model stores, chunk hashes, versions, and code for regeneration from monthly tos and sos. Its exclusion of NESM3 and MCM-UA-1-0, due to area failures, is retained.

The source uses maximum January-April sigma0, TEOS-10, and an open North Pacific mask at 25-55 N, 120 E-125 W. It excludes marginal seas. We retain its native grid cell areas. Two metrics are tested: area with sigma0 >= 26.5, and area in the band 26.4 <= sigma0 < 26.7. All areas below are in trillion square metres (10^12 m2).

## Methods

Let D(y,m,i) be surface density in year y, month m, and cell i. Let w(i) be cell area and I be an indicator. For the cumulative threshold c=26.5:

A_annual = mean_y sum_i w(i) I[max_m D(y,m,i) >= c].

A_clim = sum_i w(i) I[max_m mean_y D(y,m,i) >= c].

The source computes its mean winter map by averaging monthly density before taking the monthly maximum. For the band metric we replace the indicator with 26.4 <= density < 26.7. This audit uses the published areas; it does not recompute density.

Neither the maximum nor the threshold commutes with averaging. At each cell, mean_y max_m D is at least max_m mean_y D, but the threshold is not convex. Thus there is no general rule that A_annual must exceed A_clim. In particular, a zero A_clim cannot prove that A_annual is zero. The two metrics answer different questions.

We compare 1985-2014 using identical models and years. We count opening years at thresholds of 0, 0.01, 0.05 and 0.1 trillion m2. The last threshold is 100,000 km2. We estimate intervals for mean annual area with 2,000 circular bootstrap draws of six blocks, each five years long, using seed 110711. These intervals describe temporal sampling under this choice of block length. They do not include model error, forced trends or uncertainty in the mask.

For interior comparisons, we retain the source's combined age, oxygen and AOU values off California. These combine April 2005 snapshots and 1985-2014 series, as documented by the source. We compare Spearman correlations in identical complete subsets for both operators. Family tests average available runs within the source's model families. P values are two-sided asymptotic tests with no correction for multiple tests. We do not use a significance threshold to choose the result.

We also compare area ratios for 2005-2014 versus 1965-1984. The primary change check uses the same seven runs that had large baseline band area in the source. This avoids changing membership when small denominators vanish.

## Results

### Surface access changes in six runs

| Run | Mean annual area >=26.5 | Maximum annual area | Open winters | Winters above 0.1 |
|---|---:|---:|---:|---:|
| ACCESS-CM2 | 0.0119 | 0.1294 | 4/30 | 3/30 |
| ACCESS-ESM1-5 | 0.1195 | 0.5906 | 24/30 | 13/30 |
| CMCC-CM2-SR5 | 0.0021 | 0.0081 | 8/30 | 0/30 |
| CMCC-ESM2 | 0.0380 | 0.3242 | 9/30 | 5/30 |
| EC-Earth3 | 0.0845 | 0.4912 | 14/30 | 7/30 |
| MIROC-ES2L | 0.0735 | 0.4561 | 19/30 | 6/30 |

Each row has zero area in the mean map. Five remain changed cases if an opening must exceed 0.01, 0.05, or 0.1 trillion m2 at least once. Their five largest winters account for 53-100% of total area-years. Thus large events carry much of the surface-contact signal.

Across all 40 runs, mean annual cumulative area exceeds mean-map area in 30 runs and equals it in 10. The median absolute difference is 0.0815 trillion m2. Among the 24 runs with positive mean-map area, the median ratio of annual to mean-map area is 1.81. These ratios exclude zero denominators.

For the 26.4-26.7 band, zero-area runs fall from 14 with mean maps to 8 with annual tests. The six changed cases differ from those for the cumulative metric. Annual mean band area is larger in 29 runs; its median ratio to positive mean-map area is 1.45. This distinction is expected: a cell can leave a band through either edge.

### The oxygen link remains

| Property off California | Runs | Mean-map rho | Annual-mean rho |
|---|---:|---:|---:|
| Ideal age | 13 | -0.50 | -0.64 |
| Oxygen | 10 | +0.74 | +0.70 |
| AOU | 10 | -0.62 | -0.68 |

These values use the area at or above 26.5. Annual-mean oxygen and AOU links also remain in nine family means (rho +0.75 and -0.75). The age relation is weak in eight family means (rho -0.21). Family structure therefore limits the age inference. All band-metric and cumulative-metric tests are in files/correlations.csv.

The changed classification does not establish that the young ages in ACCESS-CM2 or MIROC-ES2L come from these openings. The source suggested other pathways. Our results add a possible surface-contact route that a zero mean map alone could not exclude.

### The large-outcrop historical loss remains small

In the seven runs with large baseline outcrops, the annual-mean band ratio is 0.77-0.94, compared with 0.73-0.97 from mean maps. Thus the change of temporal operator does not create losses near the WOA23 mean-map ratio of about 0.39 in those runs. However, WOA23 provides mean maps, so these two ranges are not equivalent observational comparisons.

Across smaller-outcrop runs, change ratios depend strongly on the operator and on zero denominators. For matched subsets with both ratios defined, the median band ratio changes from 0.45 to 0.52 (30 runs). The median cumulative ratio changes from 0.61 to 0.46 (27 runs). Annual processing therefore does not always weaken an estimated historical loss.

## Meaning and limits

A model test should report the mean-map area, mean annual area, opening frequency, and event size separately. A claim of persistent surface closure needs annual fields. A zero mean map tests the mean state only. This diagnostic rule applies to future projections, but the counts here apply only to historical runs. We did not process bias-corrected annual future maps. In particular, we cannot revise the earlier 5-of-11 projection count.

The strongest inference is an exact property of the archived model aggregates: six zero mean maps hide annual openings. This is not a measurement of renewed water volume. Surface access may be short, shallow, spatially isolated or reversed by later mixing. Monthly data omit storms and other short events. The mask omits marginal-sea ventilation. Finite grid size matters, especially for CMCC-CM2-SR5. One member per model does not sample each model's internal variability.

The result also does not correct WOA23 smoothing, observing gaps or density bias. It retains source processing and is not an independent raw-field validation. Interior samples are sparse, mixed in time, and not proof of a causal response. The correlations and bootstrap intervals are descriptive. The audit refines a claim of no contact while retaining the broader evidence that a small outcrop is linked with low model oxygen.

## Reproduction and provenance

Run with Python 3.12, numpy, pandas, scipy and matplotlib, and the configured SCI CLI:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 \
      python files/analyze.py /path/to/campaign /tmp/outcrop-audit

The script verifies the source ZIP, checks all period counts, computes every table, checks annual sums against a separate arithmetic path, and checks mean-map values against the period table. It writes only to the specified output folder. Use an external scratch folder to keep a signed package unchanged. Source ID, input hashes, licenses and software versions are recorded in files/provenance.json and files/environment.json. The verified source publication is required; raw regeneration instructions are in that source.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-0f1012efca79. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, T3 Code Codex harness. Analysis date 2026-11-11. The campaign-machine signature is not a personal authorship claim.

## Attribution

We acknowledge WCRP, the CMIP6 modelling groups, ESGF, Pangeo and the authors of the cited campaign publication. This work transforms their published aggregate areas and interior values into temporal comparisons, counts and correlations. Their source data remain external. The baseline license applies to the new code, text, figures and derived aggregates. See files/NOTICE.md for source attribution and terms.
