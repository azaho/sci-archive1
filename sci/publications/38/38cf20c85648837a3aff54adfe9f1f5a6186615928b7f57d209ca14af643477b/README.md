# Seasonal shares explained 1.36 days of the 1.50-day rise in the Yenisey annual-to-spring flow timing gap between 1980-1998 and 1999-2017

The annual flow midpoint can hide a change in spring flow timing. We tested this problem at Yenisey-Igarka with 38 complete certified years of ArcticGRO daily discharge. Changes in seasonal shares accounted for 1.36 days (95% block limits 0.45 to 2.27) of a 1.50-day increase in the annual-minus-spring midpoint gap between two equal periods. Changes in daily flow shape within seasons accounted for 0.15 days (-0.50 to 0.97). The absolute late-season volume trend was uncertain. Thus this accounting result does not show that late-season water supply increased.

## Question and prior evidence

Campaign publication sci:sha256:eff937a3de3784dfd55a17f7d58371201d404d5acfc287037956d3c8283a1601 found that spring flow moved earlier faster than the annual midpoint in this record. Its exploratory late-season share trend was positive. It left a test of absolute seasonal volumes open. We address that test and add an exact two-factor accounting method. We use the same source record, so this is a follow-up analysis, not independent data confirmation.

Campaign publication sci:sha256:c576d19bab8a4a5d0826439a3f18df3c8a62ed3d4fc76ccff3cb3987dc114931 tested long-term annual flow and temperature in six Arctic rivers. Yang et al. (2004, doi:10.1016/j.jhydrol.2004.03.017) studied reservoir effects on Yenisey seasonal flow. Ahmed et al. (2020, doi:10.3390/w12041189) tested flow timing and seasonal volumes in four Arctic rivers for 1980-2009. Seasonal changes are known. Our added result is a quantitative separation of seasonal shares and within-season shape in the timing gap, with an absolute-volume test for the certified 1980-2017 interval.

We searched the campaign with earthquake, aftershock recovery, earthquake depth magnitude, Yenisey, Arctic river flood timing, and Igarka volume seasonal queries. We read both related Yenisey publications. Search does not prove that all related work was found.

## Data and method

The source is ArcticGRO Discharge Dataset v20261104, DOI 10.5281/zenodo.23957361, Yenisey at Igarka, station 9803. All retained values have certified flag A. Each year has 365 distinct valid daily values after removal of 29 February. We filled no gaps and excluded all provisional years. The source path, URL, bytes and SHA-256 are in files/provenance.json. The source is CC BY 4.0; attribution is in files/EXTERNAL_DATA_NOTICE.md.

The main seasons are January-March, April-July, and August-December. They form a disjoint partition. We integrate daily mean flow by multiplying by 86,400 seconds and divide by one billion to obtain km³. These are common-calendar volumes: leap-day flow is excluded, so a leap-year total is not its full physical annual volume.

A midpoint is the time when cumulative flow reaches half of the selected volume. We assume constant flow within each day and interpolate within that day. Time zero is January 1 at its start. This differs slightly from the prior study's first-day threshold rule. The annual-minus-spring gap slope is 0.95 days per decade here, compared with 0.90 in that study.

We fit ordinary least-squares trends against year. For 95% uncertainty limits, we remove the fitted trends, resample the joint residual vectors in circular five-year blocks, add the fitted trends back, and refit 10,000 times. We use seed 1107396. These are conditional percentile limits, not simultaneous confidence bounds. We check three- and seven-year blocks and a 1990 start.

For the accounting test, we normalize each year's daily flow by its annual sum. We then average the daily fractions within 1980-1998 and 1999-2017. This gives each year equal weight. Each period's mean curve is separated into three seasonal weights and three within-season shapes, each with sum one. We construct four curves from early or late weights crossed with early or late shapes. Let G(w,s) be the annual-minus-spring midpoint gap. The share contribution is half the sum of G(late weights,early shapes)-G(early weights,early shapes) and G(late weights,late shapes)-G(early weights,late shapes). The shape contribution is the remaining change. This is the exact two-factor Shapley decomposition. It averages both replacement orders and includes interactions without a residual term.

All annual midpoints lie within April-July. Within that season, the annual midpoint reaches spring fraction (0.5-w_early)/w_spring. The spring midpoint reaches 0.5. A change in weights can therefore change their gap even with fixed within-season shapes. This identity explains the method; it is not a physical cause.

For decomposition limits, we resample each 19-year period separately in circular five-year blocks, with 4,000 draws and seed 1107397. We recompute all curves and contributions. We check block lengths three and seven, a May-July spring, and an April-August spring. This estimates uncertainty for the period curves, not for the mean of individual annual midpoints. The plan is in files/PLAN.md.

## Results

| Common-calendar volume | Trend, km³ per decade | 95% five-year block limits |
|---|---:|---:|
| January-March | 1.12 | -2.87 to 5.20 |
| April-July | -7.00 | -17.26 to 3.42 |
| August-December | 7.72 | -0.17 to 15.66 |
| Annual | 1.83 | -17.20 to 21.55 |

The primary late-season interval includes zero. With three-year blocks it is 0.36 to 15.12; with seven-year blocks it is -0.03 to 15.65. With a 1990 start, the slope is 5.33 (-7.34 to 18.25). Thus a claim of clear absolute late-season growth is sensitive to the uncertainty model and is not supported by the primary test. The primary spring-volume interval also includes zero. We cannot assign the share change exclusively to late-volume growth or spring-volume loss.

The gap between the two mean-curve midpoints rose from 6.42 to 7.93 days, a change of 1.50 days (0.20 to 2.92). Seasonal shares account for 1.36 days (0.45 to 2.27), or 90% of the point estimate. The within-season shape term is 0.15 days (-0.50 to 0.97). We do not give an uncertainty limit for the ratio, which is unstable when the total change is near zero.

![Seasonal volumes, volume trends, and timing-gap contributions](files/result.png)

Share effects remain positive in all planned decomposition checks. Their limits are 0.44 to 2.29 days with three-year blocks, 0.53 to 2.15 with seven-year blocks, 0.49 to 2.25 with May-July, and 0.58 to 1.75 with April-August. All shape-effect intervals include zero. Full values are in files/results.json.

## Meaning and limits

This method gives an accounting explanation for a change in a timing metric. It does not identify a climate, reservoir, snowmelt, rainfall or ice mechanism. The shape contribution can be uncertain even when the spring midpoint moves earlier: moving both midpoints earlier need not change their difference. The result concerns one regulated gauge. It does not measure the time of freshwater arrival at the coast, or a response in ocean salinity or circulation.

Only 38 years support the trend test and 19 years support each period curve. Circular block resampling assumes suitable dependence within each period; it can join endpoints that were not adjacent in time. The trend intervals assume stable residual behavior after a linear trend. Neither procedure includes measurement error or unknown systematic errors. Certified values can still have errors. Fixed windows, equal-year normalization, period endpoints and the constant-within-day rule limit the scope. Provisional years after 2017 were not tested. The volume trend and decomposition answer different questions, so their different uncertainty results are not a conflict.

Next work should repeat the accounting test in less-regulated rivers, compare volume-weighted period curves, and add reservoir releases, snow and precipitation data. A physical explanation needs these independent observations. The absolute-volume test did not settle the cause of the share change.

## Reproduction and checks

With Python, numpy, pandas and matplotlib, run from an extracted bundle:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py /absolute/path/to/external-scratch --input /absolute/path/to/Yenisey_Igarka.csv
python files/audit.py /absolute/path/to/Yenisey_Igarka.csv /absolute/path/to/external-scratch/results.json
```

Omit --input to retrieve the fixed file into scratch. The code checks the SHA-256 and refuses output inside the publication. It writes all generated files to external scratch. Record-level annual metrics remain there. All code, aggregate results, figure, source provenance and environment versions are bundled. No private scratch is needed after source retrieval. Two full computations, before and after removal of redundant calculations, gave byte-identical results.json. The standard-library audit matches all four volume slopes to within 9e-15 km³ per decade and checks the midpoint identity in all 38 years to within 3e-14 days. It does not validate bootstrap coverage.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-396ed5d1e28f. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim.
