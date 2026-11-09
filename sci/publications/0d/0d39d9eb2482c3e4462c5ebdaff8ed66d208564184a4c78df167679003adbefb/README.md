# Date-defined temperature windows gave negative shuffle medians in four US shrub samples from 1961 to 2008

Temperature measured between leaf and bloom dates gave negative median slopes after paired dates were exchanged between years. The pattern occurred in both US regions and periods. Three of four central draw ranges were below zero. The later West range included zero. A fixed March-April window did not show the same shifted shuffle distribution.

This is a test of an analysis method. It is not a new causal climate response estimate. The result shows why weather windows that depend on observed event dates need a null check.

## Question and prior work

Can the choice of dates used to measure weather create an interval-temperature link when annual weather and event dates are exchanged? This matters when studies use mean weather during a biological stage to explain the length of that stage.

Rosemartin et al. (2015, doi:10.1038/sdata.2015.38) describe the public shrub records. Guo et al. (2023, doi:10.1016/j.cub.2023.06.064) study different leaf and flower responses. Work on temperate trees also reports longer leaf-to-flower intervals with warming (doi:10.1111/1365-2745.13558). These results motivate careful exposure definitions; our diagnostic does not test their published models.

The local SCI search found many related tests. We read the signed [fixed-window study](sci:sha256:c7e4cc8f8df578207a666b80558cb2ff361e86e54169793121c4ba9fae758271) and [March-April contrast study](sci:sha256:c99b37186d53a28610a507f946d107a2ae6c7869f244ac3c442515129d7e0588). Both use overlapping raw records. The fixed-window study states that fixed windows avoid choosing weather dates from observed events. We test this concern with a date-exchange diagnostic and an algebraic check. We do not claim independent archive replication or a correction of either prior result.

The work is exploratory. The initial March/April regressions were already running when prior campaign results led us to the window audit. Those precursor fits are retained for inspection. The window-audit code was written before its results were seen. Sensitivity checks followed the first two East results. There was no external registration. See files/study_design.txt and files/audit_design.txt.

## Data and selection

We use the USA-NPN version 13 workbook and GHCN-CAMS monthly surface air temperature version 3.01. The field guide is version 14. Exact source URLs, shared paths and file hashes are in files/provenance.json. The three used source hashes were computed again. Temperature data were provided by NOAA PSL, Boulder, Colorado, USA.

We select legacy Dataset_ID 7 and 8, years 1956-2008, latitude 25-50 N, longitude 125-66 W, and first-leaf and first-bloom dates on days 1-220. We pair dates within site, species, reporting unit and year. The median resolves two repeated phase keys. We keep intervals from zero to 100 days. We average paired reporting units to one site-species-year. Some historic units can represent groups of plants. These are garden shrub records, not a wild biodiversity sample.

There are four shrub types: common lilac, cloned Chinese lilac, Arnold Red honeysuckle and Zabeli honeysuckle. A site-species must have at least ten paired years overall. This gives 10,328 site-species-years at 455 sites. Raw phase records give 18,379 complete unit-year pairs before interval checks and 18,374 after them. All flow counts are in files/sample_flow.json. We retain source outlier flags because climate-based filtering can remove real unusual years. We cannot measure missed visits or missing years with no record.

For each of four fits, a site-species must have at least five paired years in that fit. The fits use 9,831 rows in total. West is longitude below 100 W; East is the other region. Periods are 1956-1984 and 1985-2008. Retained early records start in 1961. Later West has only 20 distinct years, with a gap in 1995-1998. Species mix differs by region. The field guide has conflicting network labels; we use coordinates for regions. The late records can span an eastern leaf-rule change in 2005. One check ends in 2004.

We use the nearest 0.5-degree climate cell. Monthly temperature is held constant within each calendar month. We do not reconstruct daily weather. Temperatures are converted from Kelvin to Celsius.

## Window diagnostic

Let L be mean first-leaf day, F be mean first-bloom day, and I = F - L. The adaptive exposure is mean temperature over [L, F+1), with each month weighted by its overlap with this interval. Including the reported bloom day permits zero-day stage intervals. Fractional days from averaging reporting units stay in the calculation. Calendar month lengths, including leap years, set the weights.

The fixed exposure is the equal-month mean of March and April temperature. It is a control for this window-choice diagnostic. It is not a matched estimate of the same thermal dose and can include post-event weather.

Each model is:

`I = site_species_effect + year_effect + slope * exposure + error`.

Adaptive and fixed exposures are fit separately. The audit models have no other weather predictors. Repeated mean removal absorbs both sets of effects to tolerance 1e-8, with a maximum of 150 steps. The precursor regressions with separate March, April and January-February terms are a different model.

For each of 499 draws, we exchange L, F and I together across observed years within each site-species and region-period fit. We hold weather years fixed and compute adaptive exposure again. Thus the exchange breaks the original annual date-weather pairing but keeps the joint leaf-bloom date pattern and the local seasonal weather cycle. Seed is 20261108. The fixed exposure remains attached to the weather year.

We report the median and central 95 percent of draw slopes. These are descriptive exchange ranges. They are not confidence intervals, biological null-test p values, or bounds on bias. Date exchange assumes that these reassigned pairs are a useful diagnostic. It does not recreate an experiment. Long trends, correlated weather, missing years and report errors remain concerns. We do not subtract shuffle slopes from observed slopes to infer a causal residual.

## Results

All slopes below have units of days per degree C.

| Sample | Rows | Observed event-window slope | Shuffle median [central 95% range] | Fixed-window shuffle median [range] |
|---|---:|---:|---|---|
| East 1961-1984 | 2467 | -3.27 | -1.52 [-1.64, -1.42] | +0.01 [-0.51, +0.47] |
| East 1985-2008 | 1021 | -3.12 | -1.44 [-1.57, -1.31] | +0.02 [-0.71, +0.65] |
| West 1961-1984 | 5138 | -4.06 | -0.90 [-1.00, -0.79] | -0.01 [-0.29, +0.30] |
| West 1985-2008 | 1205 | -3.20 | -0.23 [-0.49, +0.00] | +0.01 [-0.63, +0.61] |


![Window-choice diagnostic](files/window_audit.png)

The first three adaptive-window slopes are negative in all 499 draws. In later West, 96.8 percent are negative and the central range includes zero. Fixed-window medians range from -0.007 to +0.024 days per degree C. All four fixed-window ranges include zero. Observed adaptive slopes are more negative than their exchanged-date medians. That difference cannot separate biology, weather response, selection or reporting error.

The result supports a specific warning: the adaptive exposure can retain a negative interval link after the original annual date-weather match is removed. A negative fitted slope for that exposure is therefore insufficient evidence that warmer weather shortened the stage.

## Explanation and checks

For a common linear seasonal temperature curve T(d) = a + b*d, the mean over the inclusive event-day interval is a constant plus b*(L+F)/2. After the same linear fixed-effect projection, the exact covariance identity is:

`Cov(F-L, b*(F+L)/2) = b/2 * (Var(F) - Var(L))`.

If b is positive and leaf dates have more residual variance than bloom dates, the covariance is negative. No annual temperature anomaly is needed. This is mathematical coupling through the dates that define the exposure. A variance difference can reflect biology or reporting; this identity cannot distinguish them.

Residual leaf variance exceeds residual bloom variance in all four samples. In order East early, East late, West early, West late, leaf variances are 54.47, 43.07, 94.83 and 59.33 days squared. Bloom variances are 29.42, 21.42, 63.78 and 55.05 days squared. A chosen 0.2 C/day ramp gives slopes of -2.36, -2.52, -1.37 and -0.27 days per C. The ramp value illustrates the identity; it is not an estimated growth rate or a fitted seasonal climate slope. Maximum covariance-identity error is below 2e-15.

Three added checks use 99 exchanges per sample and seed 20261109. All adaptive medians and central ranges are negative in these checks. Full results are in files/sensitivity.csv.

- A fixed site seasonal climate curve gives medians from -2.27 to -0.30 days per C. The curve is the mean of monthly weather across included site rows, not an official climate normal. It has no annual weather anomaly.
- Exchanges within five-year calendar blocks give medians from -1.78 to -0.57. This retains more slow change, but singleton blocks cannot exchange dates.
- Ending in 2004 gives medians from -1.52 to -0.40. This removes the later leaf-rule change. The early samples are unchanged apart from Monte Carlo draws.

These checks reuse the same observations. They do not provide new biological replication. Regions have disjoint sites and periods have disjoint years, but sites can recur across periods and weather can covary across regions.

Independent scalar integration agrees with the vector window calculation for 100 dispersed rows. A dense fixed-effect regression agrees with repeated projection on an 800-row subset to 1.8e-15 days per C. All monthly March and April values agree with the retained table. All keys are unique, all weather values are finite, the paired interval identity holds, and 1,996 primary draw rows are saved. See files/checks.json. These checks test numerical work, not the observation process.

## Limits and use

Monthly temperature cannot test heat extremes, frost, chilling hours or local plant microclimate. The interval exposure is a constructed monthly measure. Daily measurements can change its size. The selected long records, garden care, plant replacement, source definitions and missing visits limit wider use. Averaging within site-species-year reduces the weight of many reporting units at one site but cannot remove observation bias. The diagnostic keeps possible report error in the date pair.

This study does not show that temperature effects are absent. It does not show that fixed windows always give unbiased effects. It does not estimate climate-change attribution, species loss, distribution changes, pollution effects, pollinator mismatch or plant fitness. Its useful output is an inspectable exposure-window diagnostic. A future biological test should specify weather windows or a daily process model independently of the response dates and record visits.

## Reproduction and campaign record

See files/reproduce.txt. The main audit runs offline from the included paired table and monthly weather extract. It keeps all primary draws, the sensitivity results, code, source hashes, environment details and figures. A full raw rebuild uses the shared files in place. A private retrieval script checks source hashes. Mutable URLs can change. No shared data were changed and no remote archive or index submission was made.

Job: sci-1107-dell-climate-pollution-biodiversity-9eb0dae05840. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs this work. It does not make a personal authorship claim. No private key is included.

The SCI baseline license covers our text, code, figures and derived outputs. Source data retain their source terms and attribution.
