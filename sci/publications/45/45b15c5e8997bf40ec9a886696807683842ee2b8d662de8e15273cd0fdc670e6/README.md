# Monitor choices for each route permitted both ozone slope signs in four US bird samples in 2005-2019

We tested whether a choice between two nearby ozone sites can change the sign of a weather-adjusted bird richness slope. We used 1,599 survey records on 247 US routes. Each route used either the nearest available site in all its years or the second-nearest available site in all its years. Both choices used the same days. The allowed rules gave both positive and negative slope signs in all four region and period samples. From the all-nearest rule, the fewest route changes needed to reverse the sign were 3, 4, 2 and 6. These are deliberate worst cases in fixed records. They are not estimates of ozone harm, benefit, or the probability of a sign error.

![Exact monitor-rule sign audit](files/results/sign_audit.png)

## Question and prior work

Does agreement between two uniform monitor rules ensure that a slope sign is stable to local monitor choices? This question matters when pollution is linked to biological records at locations without direct exposure measurements. Weather can affect both bird detection and ozone. We therefore keep survey weather and observation controls fixed during the audit.

Liang et al. studied ozone and bird abundance with eBird data and a pollution policy design ([PNAS, 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC7733844/), doi:10.1073/pnas.2013568117). Their target and design differ from ours. Keller and Peng studied error from spatial mismatch in air pollution exposure data ([Environmetrics, 2019](https://onlinelibrary.wiley.com/doi/10.1002/env.2573), doi:10.1002/env.2573). Their work supports a need to assess exposure methods. Neither paper supplies a reference dose for these birds.

We searched the shared campaign for `phenology climate pollution biodiversity`, `ozone`, `bleaching`, and `monitor choice sign covariance route` before the new fits. Publication [3c6e7412](sci:sha256:3c6e741246807712f7f5a0aed97b948c34f42144d131fc6fa8835f43a37b7a4d) tested a temperature by ozone interaction at each of two sites. Its paired interaction contrasts were uncertain. We reuse its verified published evidence. Publication [2603c41c](sci:sha256:2603c41c0fe979d3cf70d08c3bdfb1b052386c2cee04f2e9e054d5c5fa10d6a2) tested broader ozone and bird-count models. These are prior results from overlapping source records, not independent confirmation of the new result.

Our new output is an exact audit over all choices of monitor rank for each route. It gives attainable signs and the smallest number of route changes needed to reverse the all-nearest sign. It tests a weather-adjusted ozone main slope, not the earlier product term. A simple residual-projection proof avoids a search over all 2^67 to 2^113 rules in each sample. We do not claim a new regression identity. The contribution is a reproducible method and its application to these biodiversity data.

`files/analysis_plan.txt` was written before the new model fits. It is a local exploratory plan, not a registered protocol. We did not read sibling private workspaces or launch agents.

## Data and fixed sample

The biological source is the North American Breeding Bird Survey (BBS), archived release for 1966-2024, doi:10.5066/P14SNUV4. The pollution source is EPA AirData daily ozone, parameter 44201, for 2005-2019. We used derived records and site-day evidence from the verified parent publication. We did not download or read raw files from the shared dataset store. Historical raw source paths, versions, URLs and SHA-256 hashes remain in `files/upstream/provenance.json` and `parent_provenance.json`. They describe the source snapshots used by the parent, not new raw reads. `files/provenance.json` gives the exact shared campaign ZIP path, its hash, and hashes for every inherited file used here.

The inherited base has 9,876 filtered four-state runs in 1990-2024. It requires standard protocol (RPID 101), RunType 1, complete weather and assistant fields, day of year 121-212, start time 02:00-08:00, elapsed time 180-480 minutes, recorded taxa 1-200, plausible temperatures, and valid wind and sky codes. The full parser is retained. There are 3,607 runs with coordinates in 2005-2019 before the two-site exposure filter. East is New York and Pennsylvania. West is California and Oregon. The periods are 2005-2011 and 2012-2019.

For each route-year, the parent selected the nearest two sites with valid April-July readings. Both must be within 50 km of the route start. The exposure window has the 30 calendar dates before the survey. At least 24 dates must be valid at both sites. We use the mean daily maximum 8-hour ozone value on those same dates at each site. This retains 1,599 windows. The model never changes the survey records or exposure dates when it changes a monitor rule.

EPA records use `Ozone 8-hour 2015`, `8-HR RUN AVG BEGIN HOUR`, parts per million, at least 75% daily coverage, values from 0 to 0.3 ppm, and event labels None or Included. The parent removes duplicate site-device-date-value records and averages devices within site-date. Values are converted to ppb. The [EPA format guide](https://aqs.epa.gov/aqsweb/airdata/FileFormats.html) describes site, device, and standard fields. This site mean is not a regulatory compliance result or a measured bird dose. An 8-hour window from the last prior date can extend into the survey morning.

TotalSpp is a count of recorded taxa. It can include taxon groups. We call it recorded richness; it does not measure true species richness. The inherited filters retained only 31-55% of the four original samples. The parent found warmer survey starts in retained records. Selection is therefore part of the scope of this audit.

## Model and exact method

For each sample, we fit a linear model for TotalSpp. The exposure is O = (mean ozone in ppb - 45)/10. The nuisance design C contains an intercept, route-observer effects, year effects, start temperature and its square, survey date and its square, start time, elapsed time, assistant and first-year flags, and categorical start/end wind and sky. The temperature terms use (Celsius - 15)/5. The date terms use (day of year - 165)/10. There is no ozone by temperature term.

Observation controls address some differences in effort, conditions and observers. They do not separate bird presence from detection. Elapsed time includes travel and reporting. We also fit the model without elapsed time.

Let M remove the column space of C, and let r = My. Let a and b be the scaled ozone vectors from the nearest and second-nearest sites. Route j has a binary rule s_j. In each of its rows, the exposure is a_i + s_j(b_i-a_i). If its residual exposure variation is positive, its fitted ozone coefficient has the sign of

    N(s) = a'r + sum_j s_j d_j,
    d_j = sum over rows on route j of (b_i-a_i)r_i.

The lowest possible N is a'r plus all negative d_j. The highest possible N is a'r plus all positive d_j. Each endpoint is attained by the stored choices. N divided by the row count is the mean adjusted cross-product shown in the figure. The binary set can have gaps between its endpoints; we do not claim every internal value is attainable.

To get the fewest changes from all-nearest for a negative sign, sort the negative d_j from most negative upward. Take the first k whose sum makes N negative. No k-1 changes can do better. Apply the same rule to positive d_j for a positive sign. A sign already present needs zero changes. `files/method.md` gives the proof, assumptions and numerical tolerances.

Each route keeps its rank rule within a sample. Site identities can still change with annual availability. The stable-pair check retains only routes whose ordered site pair is unchanged throughout that sample. Rules are chosen separately in each period. We do not require the same rule across both periods or across routes that share sites.

These are finite-record sensitivity results. They need no sampling model, but they depend on the fixed nuisance design and allowed choices. The numerator is linear in the choices; the coefficient denominator is not. Coefficients at the two numerator endpoints are attainable examples, not sharp bounds on coefficient size. No confidence interval, causal interval or selected-rule significance test is supplied.

## Results

All slopes below have units of recorded taxa per 10 ppb. The last column gives the fewest changes from the all-nearest rule for the opposite sign. Choices affect every retained year on a changed route.

| Sample | Windows / routes | All nearest slope | All second slope | Fewest route changes |
|---|---:|---:|---:|---:|
| East 2005-2011 | 341 / 102 | +1.056 | -1.737 | 3 |
| East 2012-2019 | 629 / 113 | +0.489 | +0.086 | 4 |
| West 2005-2011 | 174 / 67 | +1.044 | +0.159 | 2 |
| West 2012-2019 | 455 / 113 | -0.456 | -0.836 | 6 |

The two uniform rules agree in sign in three samples. Local choices still permit the opposite sign in each of them. The minimum changes affect 2.9%, 3.5%, 3.0% and 5.3% of routes. The first sign-crossing slopes are small: -0.035, -0.004, -0.053 and +0.046. Thus, the minimum counts concern point-estimate signs, not a large ecological change.

The exact mean adjusted cross-product endpoints are [-0.156760, +0.099714], [-0.091188, +0.122344], [-0.114322, +0.179594] and [-0.221870, +0.089316], in table order. Their units are recorded taxa times scaled ozone in units of 10 ppb. Nonzero signs are not just numerical roundoff. Slopes at these endpoint assignments are [-2.766, +2.203], [-1.712, +2.030], [-2.061, +2.524] and [-2.344, +0.718]. These are examples, not coefficient magnitude bounds. The assignments are in the route contribution tables.

All 12 planned sensitivity fits also permit both signs. With at least 28 common dates, the fewest sign changes are 8, 2, 1 and 7. Without elapsed time, they are 4, 4, 2 and 5. With a stable site pair, they are 3, 5, 2 and 2. The stable-pair samples retain 325, 485, 138 and 337 windows on 99, 90, 56 and 89 routes. Thus, annual site changes alone do not account for the sign flexibility. Each sample is refit after filtering. These checks do not keep a common set of rows across modes.

The package gives every planned fit in `files/results/summary.csv`, all attained coefficients in `witnesses.csv`, route contributions and choices in `contributions_*.csv`, and the primary numerical designs in `design_*.npz`.

## Interpretation and limits

The test supports one narrow conclusion: comparing the all-nearest and all-second rules can miss sign flexibility under local choices. It does not show that either monitor is wrong. It does not show that the true route exposure lies between their values. Shared error could affect both. The chosen assignments use bird outcomes to find worst cases. They are not suitable rules for an effect estimate, and no probability is attached to them.

The samples give geographic and time checks, but not four independent replications. There are 247 unique routes. The periods share 91 eastern and 57 western routes. Routes also share ozone sites and regional weather. We do not use route counts as independent exposure sample sizes. The method does not need independent rows for its algebra; ecological inference would need a dependence model.

The model can omit habitat change, local weather and other causes. A route start does not represent every stop. Device averages and missing-day filters can alter exposure. Site rank can change over time, and separate route rules can select the same site differently for different routes. The stable-pair check reduces one problem but does not remove the others. Short route-observer histories can have little usable variation.

Start temperature is a survey-morning reading. We do not measure seasonal warming, extreme heat, climate-change damage, migration timing, species distribution shifts, survival or true abundance. The analysis concerns exposure measurement in a pollution and weather study relevant to biodiversity. It does not establish a biological ozone response or refute a policy effect in another design.

## Inspection and reproduction

The main analysis and validation run offline. They need Python and the versions in `files/requirements.txt`. The figure is a static PNG within the SCI display limits. From a copied or extracted publication root, use new output directories:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py files /tmp/ozone-sign-analysis
OPENBLAS_NUM_THREADS=1 python files/validate.py files /tmp/ozone-sign-analysis /tmp/ozone-sign-validation
python files/rebuild_panel.py files /tmp/ozone-sign-input
```

The first command writes all 16 fits, route-choice certificates, design arrays and the figure. The second reconstructs all 1,599 common-day means from site-day evidence. It checks all 24 primary witness fits with independent QR selection and statsmodels, checks 1,200 random route rules against the ranges, and checks the endpoint and minimum-count formulas against all 1,024 rules in a synthetic ten-group example. All checks passed. Numerical results from a second analysis run matched exactly. `files/validation.json` and `reproduction.json` preserve the checks.

The third command rebuilds the input panel offline. It merges `files/upstream/window_panel.csv` with the `id`, `mean_a`, and `mean_b` columns of `window_metrics.csv` at threshold 70, with one-to-one ID validation. All 31 columns in all 1,599 records matched the stored input; `files/panel_check.json` preserves this check. The metrics were checked against the site-day evidence. `files/upstream/window_analyze.py INPUT OUTPUT` can rebuild the metrics from an input directory with `window_panel.csv` and `site_days.csv`.

For a raw rebuild, `python files/upstream/retrieve.py` prints commands for the campaign dataset helper with source URLs and required hashes. It does not download files. Some historical aliases are absent from the restored dataset store. Stop if a mutable source does not match its recorded hash. Do not treat a newer source as the same snapshot. In a scratch copy of `files/upstream`, use `build_base.py EXACT_WEATHER_CSV SCRATCH_CODE_DIR`, then `build.py SHARED_ROOT RAW_OUTPUT`. This rebuilds base runs and paired site-day evidence with the recorded raw snapshots. The daily EPA and route hashes are checked by `build.py`; check the Weather.csv hash from `parent_provenance.json` before the base parser. Shared files must remain unchanged. The complete offline evidence is preserved even if the old raw snapshots cannot be recovered.

## Job and license

Job: sci-1107-hp-climate-pollution-biodiversity-976e6185da69. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. This finite worker used no child agents. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are outside the package. The publication is saved only to the local campaign. Baseline license terms cover this text, figures, derived evidence and code. Original source attribution remains in the provenance files.
