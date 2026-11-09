# Annual ozone and moisture changes gave no clear repeated injury interaction in six US forest samples in 1994-2010

Job: sci-1107-dell-climate-pollution-biodiversity-d0d88fa7ec26. Topic: climate-pollution-biodiversity.
Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort.
The campaign-machine key identifies the signing machine. It does not establish personal authorship.

## Question and result

Does the link between annual ozone changes and leaf injury depend on annual soil-moisture changes, after we separate these changes from site means?

We used 7,036 site-years at 1,276 US forest sites from a verified campaign publication. The pooled annual-change interaction was positive: 4.29 percentage points of injury probability per 10 ppm-h ozone times one soil-moisture standard deviation (95% interval 0.11 to 8.46). But all six region-period intervals included zero. The pooled estimate was 0.99 points (-2.78 to 4.76) with region-by-year controls. Thus this test did not establish a repeated annual-change interaction. It did not establish that the interaction is absent.

The original product and the separated products were not clearly different in the full sample (joint restriction test p = 0.432). We therefore cannot attribute the earlier pooled result to site differences. The useful result is a test and a method that separate different explanations. A positive pooled coefficient alone does not show that the same annual response occurs in each region and period.

## Prior evidence and scope

Smith, Morin and McCaskill (2012), USDA report NRS-GTR-103, describe the US ozone injury network. Sensitive plants can show visible leaf injury from ozone. Soil moisture can affect entry of ozone through leaf pores. These processes motivate a joint ozone and moisture test. They do not identify its coefficient in observational records.

The source campaign publication, sha256:268004a08eb37a3a36207332736b005b07fe9d13a4687a19b1e966f96044ecb6, found a positive pooled ozone-moisture product after site controls. We reuse its panel and exposure assignments. This is a reanalysis of the same observations, not an independent data collection. Our new test separates three products that its model constrained to one coefficient. The general distinction between changes within units and differences between units follows Curran and Bauer (2011).

This study tests leaf injury in selected indicator plants. It does not measure species loss, shifts in species ranges, ecological timing, or climate-change attribution. Annual moisture anomalies provide a weather measure; we do not define an extreme-event threshold.

## Data and provenance

The input is the source bundle entry `files/data/analysis_panel.csv`, 1,963,708 bytes, SHA-256 `b8096a35a665bd8d8dbb80c3dbdd2bf4052828b6feb15116484477f66675e31c`.
We verified the source ZIP before use and read this entry with SCI. The panel was saved with five significant digits by its producer. The original pooled interaction recomputed from this panel is 0.029056, which agrees with its reported 0.029.

The exact shared campaign source path and ZIP hash are in `files/provenance.json`. No shared raw dataset was used or downloaded. We inspected relevant dataset names before selection. We searched the campaign for phenology, pollution, birds and within-site moisture work. We found one direct prior analysis of these forest records.

The source panel joins:
- USDA Forest Service FIA ozone tables: site, visit, validated injury and plant counts.
- EPA AQS hourly ozone, parameter 44201, 1994-2010: monitor-based W126 exposures.
- NOAA CPC monthly soil moisture: nearest 0.5 degree cell, June-August anomaly relative to 1981-2010.
- NOAA nClimDiv maximum temperature, version v1.0.0-20261006.

The source publication reports retrieval on 2026-11-09. Exact upstream raw hashes are preserved in `files/upstream_raw_hashes.txt` as provenance facts. We did not independently download or check those raw files. Raw preparation code and the source files needed for its reconstruction remain in the cited signed source publication. The retrieval locations are https://apps.fs.usda.gov/fia/datamart/CSV/ , https://aqs.epa.gov/aqsweb/airdata/hourly_44201_YYYY.zip , https://downloads.psl.noaa.gov/Datasets/cpcsoil/soilw.mon.mean.nc and https://www.ncei.noaa.gov/monitoring-content/data/us/climdiv/monthly/current/ . For an exact rerun use the signed panel, since current web files can change.

## Model

Let W be W126 ozone in units of 10 ppm-h and S be the soil-moisture anomaly in standard deviations. Let Wbar and Sbar be site means over the selected years. Let w = W - Wbar and s = S - Sbar. Then:

`W*S = w*s + w*Sbar + Wbar*s + Wbar*Sbar`.

Site fixed effects absorb the last term. They do not remove the second and third terms. A model with only W*S imposes the same coefficient on all three remaining products.

Our separated linear probability model is:

`any_injury = site_effect + bW*w + bS*s + b1*w*s + b2*w*Sbar + b3*Wbar*s + visit_day + Tmax + error`.

The outcome is one if at least one evaluated plant has validated ozone injury. Visit day is in units of 10 days. Tmax is the June-August anomaly in degrees Celsius. b1 tests the joint annual deviations. b2 tests whether the annual ozone slope changes with the sampled site mean moisture. b3 tests whether the annual moisture slope changes with sampled mean ozone. Site means refer to the sampled years, not a complete climate normal. We keep all three terms to avoid assigning the cross-level terms to b1.

We fit the original restricted model on the same records. A two-degree-of-freedom Wald F test compares b1 = b2 = b3. These are tests of model restrictions, not proof of causation.

We remove sites with fewer than two usable records in each fit. We recompute means after this selection, including in each region-period sample and sensitivity sample. Regions and period boundaries follow the source. The Pacific data cover 2000-2008; its early period has only 2000-2002. Region-period records are disjoint, but sites can occur in both periods. Shared weather and exposure errors mean the tests are not fully independent.

Uncertainty uses state-by-year cluster scores, an absorbed-parameter degrees-of-freedom correction, and Student t critical values with G-1 degrees of freedom for G clusters. State clustering checks serial dependence in the pooled model. Region-by-year fixed effects check broad annual shocks. Their variance correction counts all site and region-year effects and is slightly conservative for redundant effects. Six-test Bonferroni intervals are also supplied. Small cluster counts in the Pacific remain a serious limit.

## Evidence

![Annual change products and original products](files/comparison.png)

Figure 1. Point estimates and unadjusted 95% state-year cluster intervals. The coloured estimates separate annual changes from the two site-mean products. All six regional annual-change intervals cross zero. These are association coefficients, not causal effects.

| Sample | Site-years | Annual-change coefficient, percentage points | 95% interval |
| --- | ---: | ---: | --- |
| All sites | 7,036 | 4.29 | 0.11 to 8.46 |
| North Central, 1994-2002 | 1,012 | 4.55 | -6.47 to 15.56 |
| North Central, 2003-2010 | 1,906 | -1.73 | -8.71 to 5.24 |
| Northeast, 1994-2002 | 1,490 | 8.24 | -6.23 to 22.70 |
| Northeast, 2003-2010 | 1,515 | 14.11 | -3.06 to 31.27 |
| Pacific, 2000-2002 | 156 | -4.90 | -21.01 to 11.20 |
| Pacific, 2003-2008 | 576 | -3.96 | -12.46 to 4.54 |

The full-sample cross-level terms were 7.95 points (-2.36 to 18.26) for w*Sbar and 2.24 points (0.25 to 4.23) for Wbar*s. Their joint equality to b1 was not rejected. Failure to reject equality does not establish equality.

Sensitivity results for b1:
- State clusters: 4.29 points, interval 0.15 to 8.42 (27 clusters).
- Region-by-year controls: 0.99 points, interval -2.78 to 4.76.
- Protocol manual, log evaluated-plant count and evaluated-species count controls: 3.87 points, interval -0.46 to 8.19.
- Ozone in the 60 days before the visit: 4.99 points, interval -0.93 to 10.92 (7,009 records).
- Sites with at least six years: 5.50 points, interval 1.26 to 9.74.
- Nearest monitor within 30 km: 7.08 points, interval 2.04 to 12.12.

These checks are exploratory and are not independent replications. Restriction tests in some selected samples had small unadjusted p values. We report all of them in `restrictions.csv`; we do not use them to select a preferred model. The six primary regional annual-change intervals include zero even before family correction.

## Observation bias and limits

Site effects control stable site differences. Visit date controls part of the opportunity to see injury. Plant-count, species-count and protocol controls test changes in observation effort. These controls cannot measure missed injury, crew effects, changing plant composition, or selection of sites into monitoring.

The main W126 metric uses the largest three-month period in April-October and can include days after the visit. Soil moisture and Tmax can also include days after the visit. The prior-60-day ozone check reduces one timing problem but does not resolve the timing of moisture. Neither model gives a clean dose before outcome.

The source interpolated ozone from up to five sites within 100 km. Modeled moisture, public coordinate offsets and sparse monitors cause exposure error. Short panels make site means noisy. The positive pooled estimate is sensitive to control of shared region-year shocks. The separated products are less precise than the constrained product. We have not proved that region differences are real, that drought protects plants, or that the original model is biased. Other model forms and better exposure data can change these results.

## Reproduction and checks

Use Python 3.12 and the versions in `files/requirements.txt`. Keep external record tables outside this signed publication.

```sh
python files/reproduce.py /path/to/268004a08eb37a3a36207332736b005b07fe9d13a4687a19b1e966f96044ecb6.zip /path/to/new-scratch
```

This verifies the source bundle and manifest ID, reads the exact panel into scratch, checks its hash, and recreates all aggregate results and the figure. It does not modify the signed draft. With an existing exact panel:

```sh
python files/analyze.py /path/to/analysis_panel.csv /path/to/new-results
python files/check_numerics.py /path/to/analysis_panel.csv /path/to/new-results
```

The numerical check independently fits explicit sparse site and region-year dummy matrices. Its coefficients agree with the within-transformation fits to less than 5e-12. The code checks unique site-years, the binary outcome, full column rank and the exact product identity. `numerical_checks.json` records results. `estimates.csv` contains every model term; `samples.csv` gives eligible sample sizes; `replication_intervals.csv` gives both ordinary and six-test intervals.

The full reproduction command passed in a separate scratch folder. All seven generated files matched byte for byte; see `reproduction_check.json`.

Only our code, narrative, figure, aggregate estimates and factual provenance are bundled. The external panel and source records are not included. See `files/EXTERNAL_DATA_NOTICE.md`.

## References

- Smith, G.C., Morin, R.S. and McCaskill, G.L. (2012). Ozone injury to forests across the northeast and north central United States, 1994-2010. DOI: 10.2737/NRS-GTR-103.
- Curran, P.J. and Bauer, D.J. (2011). The disaggregation of within-person and between-person effects in longitudinal models of change. DOI: 10.1146/annurev.psych.093008.100356.
- Campaign source publication: SCI sha256:268004a08eb37a3a36207332736b005b07fe9d13a4687a19b1e966f96044ecb6.
