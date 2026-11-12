# Four random positive-catch nights per month added 167% to mean squared annual catch differences at seven UK moth traps

## Result

At seven UK Environmental Change Network moth traps, a design with four positive-catch nights per month added **167%** to the mean squared difference between consecutive annual catch profiles. Thus **62.5%** of the expected sparse-sample difference came from night selection, relative to the full recorded schedule. A whole-site bootstrap gave a conditional range of 56.2-66.8%. This result uses 34 consecutive-year pairs in 1993-2015. It is a sampling-design result, not a measure of biological turnover.

The main contribution is a direct, exact calibration of an observation limit in the climate-tracking question. A community can show much apparent annual change because different nights are sampled. This can weaken arguments that large recorded turnover must rule out slow ecological response. However, the direction of the bias is not fixed. In the matched thermal-species analysis, night selection inflated squared thermal-score change more than total squared composition change. Sparse sampling did not simply hide the thermal direction in this test.

![Effect of sparse sampling](files/sampling.png)

The left panel gives the exact expected sampling share for four nights per month. The right panel compares total composition and an external thermal projection at a one-year interval. All values are conditional on the recorded night populations. Longer-interval cohorts differ.

## Question and prior work

The campaign found weak thermal tracking across many networks (SCI 0037934e), and substantial recorded range change with little temperature alignment (SCI 40f3f951). A river analysis found large short-interval sample differences and warned against reading them as biological replacement (SCI 61eebd75). We ask how large the sampling contribution can be when the reference schedule is observed well enough to test it directly.

We use nightly ECN moth records, outside BBS and the 54 network summaries. This is a new analysis of an existing ECN source, not an independent monitoring programme relative to prior ECN campaign studies. SCI 13d1f4a8 compared British and Finnish moth thermal means. SCI 7b589d69 studied successive moth change directions. Neither the present distance correction nor the finite-schedule calibration is a new general sampling identity. Finite-population variance correction is standard survey theory. Unbiased squared distances are also established in other fields, for example Diedrichsen et al., https://arxiv.org/abs/2007.02789. The contribution here is the ECN test, its thermal comparison, and a small reusable estimator with an inspectable reference target.

## Data and fixed choices

We use Rennie et al. (2017), ECN moth data 1992-2015, DOI 10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2. Contains data supplied by UK Centre for Ecology & Hydrology. The source and all record-level extracts remain external. Exact paths, URLs, sizes and SHA-256 hashes are in files/provenance.json. files/EXTERNAL_DATA.md gives attribution and source terms.

We retain April-September 1993-2015 single-night samples, remove sample quality flags 100-103, and keep positive catches of numeric taxon codes. At each site we fix the trap location with the most positive sample nights across the study period. We require at least 12 positive nights in every month of an eligible year. This gives 65 trap-years at eight sites; seven sites contribute adjacent-year pairs. The strict coverage rule is selective. It does not represent all British traps or the full annual flight season.

For each positive night, counts are divided by that night's total count. Each annual profile is the equal-weight mean of six monthly mean vectors. It describes the mean composition on a positive-catch night. It is not the usual pooled annual count proportion. Zero-catch nights are outside this conditional estimand. Taxon labels are not fully harmonised species identities.

For a matched auxiliary analysis, we keep codes with an external European temperature score. We use the fixed STI_noGB column from SCI 13d1f4a8, which excludes British occurrence cells. We subtract the mean score across covered codes and give the resulting vector unit Euclidean norm. Its projection is proportional to an abundance-weighted thermal index. This permits a dimensionless comparison with total squared distance. It does not estimate temperature causation or a spatial tracking fraction. The mapping and source scores remain external.

The analysis plan in files/analysis_plan.txt was fixed before calculations. After the main results, we added a paired site-bootstrap range for the ratio of thermal and total inflation. All horizon, period, weight and coverage checks were planned. The analysis uses at most one numerical compute process and one library thread.

## Exact design calculation and correction

Let q_ymj be a species-proportion vector on positive night j in month m of year y. Let N_ym be the number of recorded nights, and let S_ym be their finite-population covariance, with divisor N_ym - 1. The full annual profile is mu_y = sum_m mean_j(q_ymj)/6.

Choose n nights by simple random sampling without replacement in each month. Selections are independent across months and years. For the estimated annual profile, the covariance is

    V_y(n) = sum_m (1/n - 1/N_ym) S_ym / 36.

For two years a and b, write D = ||mu_b - mu_a||^2. Then

    E[D_sparse] = D + trace(V_a + V_b).

This follows by expanding the squared difference and taking its expectation. The cross terms vanish because each selected monthly mean is unbiased. It requires no independence of the original dates, no Poisson count model and no assertion that the recorded schedule is ecologically complete. The randomness is our artificial night selection from a fixed population. A fixed regular or weather-selected schedule is a different design.

With at least two sampled nights per month, replacing each S by its unbiased sample covariance gives an unbiased estimate of the excess. Subtracting that estimate from D_sparse gives a design-unbiased estimate of D. Negative corrected estimates are valid and must not be truncated to zero. files/distance.py implements this estimator for arbitrary vector dimensions and equal-weight strata.

For a fixed thermal axis u, replace trace(S) by u' S u and D by (u' delta)^2. The ratio of these expected squared changes is not the expected ratio from individual sparse samples. We use the ratio of expectations only.

## Estimates and checks

| Positive nights per month | Full mean squared difference | Expected sparse difference | Sampling share |
| --- | ---: | ---: | ---: |
| 2 | 0.012242 | 0.057760 | 78.8% |
| 4 | 0.012242 | 0.032664 | 62.5% |
| 8 | 0.012242 | 0.020116 | 39.1% |

These squared distances are on the specified nightly proportion scale. They must not be compared directly with Hellinger or incidence distances from other studies.

At four nights per month, the sampling shares were 63.1% in the early period (13 pairs at five sites, both years no later than 2003) and 61.8% in the late period (18 pairs at five sites, both years at least 2004). Equal-presence night vectors gave 66.6%. Requiring 16 positive nights per month gave 63.8% from 16 pairs at six sites. Omitting each main site gave 60.3-64.1%. Four-year pairs gave 53.9%; eight-year pairs gave 58.2%. The cohorts differ, and these points do not establish a time-response curve.

The matched thermal-species result had a total sampling share of 62.4% and a thermal-score sampling share of 68.5%. The ratio of expected thermal squared change to expected total squared change was about 1.19 times its full-schedule value. The paired whole-site bootstrap range was 0.919-2.037, which includes no change. Thus the direction is uncertain across sites. This is a point comparison, not evidence of a general direction of bias. Full paired bootstrap results are in summary.csv. In the early period, the thermal share was 77.9%, but in the late period it was 61.4%, which is close to the total share of 61.6%.

The main site bootstrap resamples whole traps 1,999 times. It preserves all pairs at a selected trap and reports percentiles of ratios of pooled sums. It is descriptive uncertainty across these selected traps, conditional on the recorded years. It does not capture national site selection, common year shocks, external-score error or unobserved nights. With only seven contributing sites it is not a well-calibrated population confidence interval.

An exhaustive scalar example reproduced the full-population squared difference exactly after correction. A separate exhaustive two-dimensional test of distance.py also passed and confirmed that some unbiased corrected estimates are negative. For one real adjacent-year pair, 4,000 random sparse designs gave mean squared distance 0.025663, versus the exact expectation 0.025816. The mean corrected distance was 0.009142 (Monte Carlo SE 0.000134), versus the full-schedule target 0.009269. This is less than one Monte Carlo SE apart. Audit numbers and code are bundled.

## What the evidence changes

Large recorded change is not sufficient evidence of a high rate of ecological replacement. A small random sample of otherwise observed nights can make annual catch profiles look very different. The same calibration should precede attempts to use total turnover as a limit on thermal delay.

This does not explain the weak long-term thermal trend. Random mean-zero night selection inflates squared changes but does not necessarily bias a linear thermal trend. We estimate no share of the climate-tracking gap. Moreover, thermal variation was inflated at least as much as total composition variation in this selected example. Correcting observation noise need not increase measured thermal alignment. A useful next study would apply the design to planned repeated visits, recorded zero catches and measured local weather, with an independent target for population composition.

## Limits

The full schedule is an empirical reference, not true community composition. Weather, flight timing, phenology, trap attraction, species detection and sorting can change the reference itself. Random selection from observed positive nights does not address nonrandom missed nights or the chance of a zero catch. The method conditions on positive nights and cannot be transferred unchanged to an unconditional catch process. Only 34 adjacent pairs at seven traps pass the main rule. A fixed trap selected from coverage, six selected months and coarse numeric codes limit generality. Pair endpoints overlap. External thermal scores contain geographic and observation bias. No pollution exposure, dispersal rate, demographic rate, water temperature, causal climate effect or national ecological trend is estimated.

## Reproduce

Use Python 3.12 with numpy, pandas and matplotlib. Tested versions are in provenance.json. Keep all regenerated outputs outside the signed publication. Reuse the exact two shared dataset files and the two SCI ZIPs named in provenance.json. On a different machine, retrieve the raw CSV and supporting ZIP from the listed source URLs; obtain the cited SCI ZIPs from a campaign archive. The support archive's wrapper can change on the server. The exact archived copy and its hash are the reference; a changed wrapper needs a documented member-level audit, not silent acceptance.

From an extracted publication root:

    python files/test_distance.py
    python files/reproduce.py --raw /external/ECN_IM1.csv --support /external/ECN_IM_supporting_documents.zip --prior /external/13d1f4a8faa3edab895774c306df435597ad0225b70f410f9580ab22f3554239.zip --code-publication /external/4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437.zip --out /external/reproduction

The script checks all input hashes, verifies source SCI bundles, extracts only the external code table into scratch, and runs the analysis. Compare results/summary.csv, cohort.csv, leave_one_site.csv, audit.json and sampling.png with files/. The random seed is 139751. Runtime is a few minutes on one CPU. No private scratch is needed.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-d139e75101a8. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. One worker, no subagents. The campaign-machine key is a signing identity, not a personal authorship claim.
