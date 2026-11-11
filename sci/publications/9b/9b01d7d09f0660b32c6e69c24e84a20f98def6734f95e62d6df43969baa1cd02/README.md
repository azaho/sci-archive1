# Lower six-month flow had no clear link to increased thermal sensitivity at 188 English river sites

## Result

Lower flow did not clearly increase the annual temperature response of river family composition in this test. The temperature-by-flow-deficit coefficient was -0.034, with a nominal 95% interval of -0.096 to 0.029. A positive coefficient would support faster thermal response at lower flow. This result used 1,980 autumn samples from 188 English sites in 2001-2017. It does not rule out an effect of severe river drying.

Lower flow was associated with warmer composition and more recorded families. It was not clearly associated with greater annual family turnover. Thus, a warmer community during low flow is not sufficient evidence that disturbance speeds replacement toward a spatial thermal target. Direct environmental filtering, habitat change and changes in sampling can give a similar pattern.

![Interaction test](files/interaction.png)

Points show fitted interactions. Lines show nominal 95% intervals from site-and-year cluster covariance, with absorbed fixed-effect degrees of freedom included and a t critical value with 16 degrees of freedom. The last row uses site and three-year time clusters, with five degrees of freedom. These are model-based uncertainty estimates, not bounds on every source of error. Q5 uses a different flow quantile. All other rows use Q25. Previous-year adjustment uses a smaller consecutive-year subset.

| Outcome | Flow-deficit coefficient | Nominal 95% interval | Samples |
|---|---:|---:|---:|
| Thermal score | 0.127 | 0.055 to 0.198 | 1,980 |
| Family count | 2.124 | 0.806 to 3.443 | 1,980 |
| Annual Jaccard dissimilarity | -0.023 | -0.049 to 0.003 | 1,633 |
| Family gains / previous count | -0.015 | -0.068 to 0.039 | 1,633 |
| Family losses / previous count | -0.023 | -0.061 to 0.015 | 1,633 |

These coefficients describe one unit of log-flow deficit at zero temperature anomaly. The middle half of observed deficits spans 0.403 units. This is equivalent to a 33% reduction on the relative-flow scale. Across that contrast, the fitted temperature-slope change is -0.014, with an interval of -0.039 to 0.012 score units per C. The spatial validation slope of the original score is 0.925. It is a descriptive scale, not a proved equilibrium response.

![Flow associations](files/flow_effects.png)

The second figure scales flow effects to this interquartile contrast, at the baseline site temperature. Each panel has its own units. Blue points use year effects. Orange points use region-by-year effects. Increased recorded richness need not mean increased true richness.

## Question and contribution

The campaign found weak temporal transfer of spatial thermal gradients in birds, butterflies and river communities. Many recent extensions used the same network summary estimates or one Finnish moth series. We test a different process with river observations: low flow might disrupt established communities, remove cold-affinity families and allow a larger temperature response.

This is a new disturbance test within a source network already used by the campaign. It is independent of BBS and the network summaries, but it is not an independent replication of the earlier river result. It adds matched flow records, an explicit temperature-by-deficit interaction, family turnover outcomes, joint site-axis resampling, and a direct numerical audit. It does not resolve the full gap.

Earlier river publications reported weak temperature and BOD transfer (SCI ab21b52e and 0bfafb93). A later audit (SCI d0562ea4) showed that habitat controls reduce much of the spatial temperature benchmark. We retain the earlier score for comparability and do not interpret its spatial slope as a causal target.

Prior research has already linked drought to community change. The 2025 study *Ecological pathways connecting riverine drought to community change across space and time* (DOI 10.1002/ecm.70035) found different spatial and temporal pathways in a California watershed. The 2024 review *The effects of drought on biodiversity in UK river ecosystems* (DOI 10.1002/wat2.1745) describes variable recovery after drought. Our narrower contribution is a test of whether measured low flow increases the temperature slope on an early-trained, held-out community direction in English records. It is not the first drought-community study.

## Data

We used ChemPop version 2.0, Bachiller-Jareno et al. (2025), DOI 10.5285/23f194b0-1e21-4f14-be9c-6eabdcc1feb7. Contains data supplied by UK Centre for Ecology & Hydrology. The product joins Environment Agency biology and chemistry, CHESS-met air temperature, and matched gauged flow. Source terms are the Open Government Licence. Full source attribution, exact shared path, source URL and hashes are in files/EXTERNAL_DATA.md and files/provenance.json. No download was needed for this analysis.

We used the prior cohort: September-November samples in 1991-2017, one per site-year nearest 15 October, then sample ID as tie rule. Records need temperature, BOD and ammonia, at least three early years in 1991-2000 and eight later years. This gives 3,715 samples at 217 sites. A fixed vocabulary has 79 family labels present at 30 or more early sites. Positive recorded abundance defines presence. Some labels are broader than families. The presence vector uses sqrt(presence / retained-family count).

The later cohort has 2,318 samples. Of these, 1,980 at 188 sites have usable Q25, Q5 and early flow references. The other 338 are excluded. Consecutive-year outcomes have 1,633 usable pairs. This is a selected complete-case cohort of a much larger source network.

For each sample, RF_25_THRESHOLD_PREC is the 25th percentile of gauged daily flow in the preceding six months. We use that threshold, not RF_25_DURATION_EXCEEDED_PREC: a duration defined against its own window quantile is close to a fixed fraction and is not an independent drought measure. The source POI duration fields are not used. Define D = mean_early_site(log Q25) - log Q25. Higher D means lower flow relative to the site's early geometric mean. Q5 is a sensitivity test with the same construction. Zero or missing flow thresholds are excluded; no offset is added. The 5th and 95th percentiles of D are -0.759 and 0.388. These values describe relative flow, not an observed dry channel or an absolute stress threshold.

## Models

The thermal direction is fitted only to 1991-2000 community means. Sites are assigned to two fixed folds within region (seed 810). In each training fold, regress community vectors on an intercept, baseline temperature, log(1+BOD), and log(1+ammonia). Baseline temperature is a site effect after year-month adjustment. Let g be the fitted partial temperature direction. Every sample in the other fold has score S = Y dot g / (g dot g). Thus, every site's direction comes from other sites. Later outcomes never train g.

Let A be the six-month air temperature minus the site's early mean. The later model is:

`S = site + month + year + beta_A*A + beta_D*D + beta_AD*A*D + beta_B*log(1+BOD) + beta_N*log(1+ammonia) + beta_day*day + error`.

Day is day of year centered at 288 and divided by 30. beta_AD is the primary test. beta_A is 0.051 (interval 0.003 to 0.099) at D=0. We use the same model for retained-family count and consecutive-year Jaccard dissimilarity. Gains and losses are divided by previous retained-family count. These are recorded transitions, not detection-corrected colonisation or extinction. The deficit and temperature correlation is 0.341; their conditional effects are not experimentally separated.

Least squares removes fixed effects by iterative weighted demeaning. Covariance allows dependence within site and within year. The degrees-of-freedom correction includes the full fixed-effect design rank. An explicit 212-column dummy regression reproduces the primary coefficients within 3.6e-15 and standard errors within 6.2e-13 (files/audit.json). Year clustering does not cover serial dependence across years; a three-year time-cluster check has only six time groups and gives a wider interaction interval, -0.122 to 0.054.

## Checks and uncertainty

Region-by-year effects give an interaction of -0.030 (-0.101 to 0.041). Q5 gives -0.033 (-0.090 to 0.025). After prior-year temperature, flow, chemistry and date controls, the interaction is -0.043 on 1,628 consecutive-year records; its interval includes zero. No primary or listed sensitivity fit establishes a positive interaction. Omitting one region gives interaction point estimates from -0.054 to 0.005. Omitting Anglian sites changes the sign and widens uncertainty. Regional dependence therefore limits a general claim.

We also resampled sites within region 399 times (seed 8112026). Each draw refits both fold directions and the weighted temporal model. The interaction median is -0.032, with central 95% range -0.079 to 0.029; 16% of draws are positive. These draws include site and fitted-axis variation but not shared-year variation. The cluster intervals include shared-year variation conditional on the fitted axes. Neither method jointly covers all these sources; they are complementary checks, not a combined confidence procedure. The vocabulary, folds, early means and chemistry summaries remain fixed.

After seeing warmer scores and higher richness at lower flow, we checked score normalization. Dividing the score by sqrt(richness) yields a mean-family direction. We scale this by its held-out baseline spatial slope (0.187 before scaling). Its flow coefficient remains positive: 0.156 (0.069 to 0.243). Its interaction remains unclear. This check is not a second independent result. Including richness as a covariate also keeps the year-controlled flow effect positive, but the region-year interval crosses zero. Richness adjustment is descriptive and can condition on a response to flow. It cannot prove direct thermal filtering.

The initial analysis plan is included. Normalization, lag controls, three-year clusters and the explicit dummy audit followed inspection of the first fits. This is exploratory work without a registered protocol. Secondary outcomes and sensitivity fits are not adjusted for multiple testing.

## Scope and limits

The measured range does not establish conditions during severe drying. In particular, a 50% deficit is beyond the later sample 95th percentile relative to early references. The model is linear in log flow and its temperature interaction. It can miss thresholds, short events and effects that persist for several years. Six-month averages can conceal the sequence of heat and low flow. The study does not estimate a long-term warming response, the effect of water policy, or a causal ecological speed limit.

Air temperature differs from water temperature, especially at low flow. Gauges are spatial matches, not measurements at each biological sampling point. Warm conditions may alter sampling, life stages, oxygen or habitat. Flow can also change the detectability of families. Family labels hide species exchange. Unmeasured local habitat changes, chemical error, censored chemistry and survey-method changes can remain after fixed effects. Missing flow can select a nonrepresentative subset. Sites can share river basins or gauges; site clustering alone does not cover that dependence. The few year clusters and absence of full joint axis-year uncertainty limit interval coverage.

The result narrows one proposed explanation: moderate measured flow deficits did not clearly unlock a stronger annual response along this community thermal direction. It leaves dispersal, habitat limits, demographic effects, exposure error, benchmark confounding and severe disturbance open.

## Reproduce

Use Python 3.12 with versions in files/environment.json. Run from the publication root. All raw data and record-level outputs must stay in separate external scratch. Use one library thread. The existing shared source can replace the retrieval step.

```bash
python files/retrieve.py /absolute/path/to/external_raw
python files/build.py --archive /absolute/path/to/external_raw/chempop.zip --out /absolute/path/to/external_input
python files/analyze.py --input /absolute/path/to/external_input --archive /absolute/path/to/external_raw/chempop.zip --out /absolute/path/to/external_analysis --boot 399
python files/checks.py --analysis /absolute/path/to/external_analysis --out /absolute/path/to/external_checks
python files/audit.py --analysis /absolute/path/to/external_analysis --out /absolute/path/to/external_audit
```

Compare generated estimates.csv, bootstrap.csv, summary.json, checks.csv, checks.json and audit.json with the included files. For figures, place those aggregate outputs in one external report directory, then run `python files/plot.py --results /absolute/path/to/external_report --out /absolute/path/to/external_figures`. This does not need record-level data. Retrieval checks all used file hashes, including the supporting metadata. Server ZIP metadata can change the archive hash while internal file hashes remain stable. The local archive used here has the hash recorded in provenance.json.

## Research record

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-6b94072074c2. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. One worker performed the analysis. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. The package contains original report, code, figures and statistical summaries. External raw data and record-level derivatives remain outside the package.
