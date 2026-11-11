# A shared step in four of seven SST products causes the tested blind search to correct the clean products

## Result

A synthetic test of the published seven-product SST correction shows a limit that product agreement does not measure. The blind search removes a +0.06 K step when it is present in one, two or three products. When it is present in four, five or six products, the search instead applies cold-step corrections to the clean products. The corrected products agree but retain the warm step. With fitted SST noise, the remaining common step is 0.0583 to 0.0614 K in all 24 majority-step tests. This is a method test. It does not show that this error occurred in the observed record.

![Family-step tests](files/results/family_benchmark.png)

The source study (SCI d9bdf1f8) fits a free monthly common signal and product steps to seven SST products. It finds 23 steps. After correction the products give about 0.149 K per decade for 1985-2024. Its code states that sparse selection assigns steps to minority products. A later study (SCI 25e4afb2) bounds errors shared by all products. Here we test partial input families in the blind search and give a conditional family-weighted estimator.

Relative correction and contaminated references are established problems. Menne and Williams (2009) describe pairwise correction; WMO (2020) discusses shared network changes. Our contribution is the numerical test of this SST detector with its own noise parameters, an absolute remaining-error metric, and tests of correct and incorrect family weights. The weighted median is an established estimator. We do not claim a new general estimator or discovery of the common-error information limit.

Shared inputs make this test relevant but do not prove the scenario. For example, Copernicus documents that ERA5 prescribes HadISST2.1.0.0 SST before September 2007 and OSTIA afterwards. That history does not establish that four of these seven products share a step. We do not infer a real family map.

## Blind test

We use the original `Joint`, `ar1_noise` and `fit_given` code without edits. The source ZIP passes complete SCI verification. The test has 528 months (1982-2025), seven products, four detection regions and the source availability pattern. HadISST1 is complete; the other six availability patterns come from the published table. No SST values enter our test. Regions are 20-60N, 20S-20N, 20-40S and 40-60S.

Each affected product receives a +0.06 K step in January 2005 in each region. There is no other step, drift or common climate signal. A common climate signal would cancel in the within-month transform. We run the full unknown-date greedy search and its backward check. We fix its final pass-B weights and threshold (88.9291) at the source values. We do not recalibrate them for each injection. This tests the fitted pass-B detector, not the full two-pass calibration pipeline.

There is one noiseless test for each affected-product count and eight noise draws with the source final residual standard deviations, AR(1) coefficients and cross-region correlation. Noise is independent across products; the artifact is shared exactly. For each draw, a random product ordering defines nested affected subsets of sizes one to seven. The noise is paired across subset sizes. There are 63 searches. The cap of 20 steps is never reached. Eight draws are diagnostic tests, not enough to estimate rare failure rates.

Let B be the injected bias and Bhat the estimated correction. We calculate the change in B-Bhat between months 60 to 13 before the step and months 12 to 59 after it. The mean across products and four equally weighted regions is the remaining common jump. It is not an area-weighted global SST estimate. Spread is the standard deviation across products of their region-mean remaining jumps. We do not remove the common part before scoring. The source simulation removes that part for its relative-error score; that score does not measure this failure.

| Affected products | Noiseless corrections | Median common jump with noise (K) | Median spread with noise (K) |
|---|---|---|---|
| 1 | 1 affected product | 0.00009 | 0.00072 |
| 2 | 2 affected products | 0.00024 | 0.00178 |
| 3 | 3 affected products | 0.00001 | 0.00200 |
| 4 | 3 clean products | 0.05993 | 0.00197 |
| 5 | 2 clean products | 0.06010 | 0.00156 |
| 6 | 1 clean product | 0.06021 | 0.00101 |
| 7 | None | 0.06000 | 0.00000 |

For one to three affected products, all 48 injected product events across the eight draws are found within three months, with no such hits on clean products. For four to six affected products there are no affected-product hits within three months and 45 clean-product hits. Exact dates and additional events are in `traces.json`. Close agreement does not distinguish successful correction from error transfer here.

If the retained 0.06 K step were uniform over the study mask, it would add 0.02278 K per decade to a linear trend from January 1985 to June 2024. This is a leverage calculation, not an estimate of a hidden contribution to the reported trend.

## Identical relative explanations

Write X_p=T+c_p+B_p+e_p. For a subset F of k products, a step delta H in F and zero elsewhere has the same fitted observations as a common signal T_new=T+delta H, zero bias in F, and bias -delta H in its complement. The first explanation needs k product-step parameters; the second needs 7-k. Product sparsity favours the second when k is at least four, in this noiseless sufficient-signal case.

This count comparison holds for all 127 nonempty subsets, listed in `sparse_truth_table.csv`. It compares two exact explanations, not every possible greedy-search outcome. The source within-month transform maps both explanations to the same array even with unequal weights and gaps; our maximum numerical difference is 6.7e-16. A covariance model alone cannot distinguish them. A penalty or external anchor must select one. The seven unknown-date noiseless searches confirm the count result for the tested nested subsets.

## Conditional family weights

For an externally specified date, let d_p be the observed product jump and g the unknown common jump. Minimise sum_p a_p abs(d_p-g). The solution is a weighted median. Set a_p=1/n_f for the n_f products in family f. Each family has total weight one. The estimated product correction is d_p-g. Interpretation requires that more than half of the total family weight has no artifact at this date, and that all products observe the same true common jump.

If within-family jumps are identical, the estimate depends on family counts rather than product copy counts. Replicating an identical family preserves its empirical mass and the solution. All 4,000 numerical replication checks pass. This property does not imply invariance when one unequal member of a family is copied.

We test this restricted estimator separately, with a known date. It does not replace blind detection. We use the tropical source noise parameters. Adjacent 60-month means give Gaussian product jumps with contrast variances calculated exactly from stationary AR(1) covariance. There are 10,000 draws (seed 516041). The first k products share the artifact; the other products are separate clean families. Tested k values are one to five. Controls use equal product weights or an incorrect map that groups the clean products and leaves affected products separate.

For four affected products:

| Gauge weights | Common-jump RMSE (K) | Product-error RMSE (K) |
|---|---|---|
| Equal products | 0.04950 | 0.05030 |
| Correct families | 0.00471 | 0.01011 |
| Incorrect families | 0.05728 | 0.05797 |

Correct weights reduce common-jump RMSE by 90.5%. Incorrect weights make it worse. Correct-family RMSE across k=1..5 is 0.0034 to 0.0075 K. These are simulation summaries, not observational confidence limits. Family membership must come from input history or external evidence. Using agreement at the tested step to infer it would be circular. Two families with opposite histories give no clean-majority guarantee.

## Limits and implication

This supports recovery of isolated steps in the tested noise and shows error transfer under a product-majority artifact. It does not challenge documented DOISST changes, measured product differences, or published model-forcing effects. It does challenge using product count or small corrected spread alone to establish absolute stability.

The synthetic errors have one date and size, and the same sign in all regions. Real errors can have different dates, patterns and responses. We do not test cross-product random-noise covariance, recalibration, a radiative kernel or an independent thermometer. Fitted source parameters are not independent observational validation. Correct family weights require known lineage and a clean family majority. No revised ocean warming rate follows. A next observational task is a date-specific input-lineage map tested against observations that do not share the input changes.

## Reproduce

Use Python 3.12, numpy 2.5.4, pandas 3.1.1 and matplotlib. No raw SST download is required. From the extracted publication:

    bash files/code/run_all.sh /absolute/path/to/external_output

This takes about two minutes on one numerical thread and writes only to external output. It uses bundled fitted-noise parameters and availability flags in `files/results/benchmark_inputs.json`. To rebuild inputs from the prior ZIP, use `benchmark.py --campaign /path/to/campaign --out /external/output --replicates 8` without `--inputs`. That mode verifies the source ZIP before reading the three recorded entries. Entry hashes and the exact shared campaign ZIP path are in `provenance.json`. No shared raw dataset files were used.

`family_gauge.py` contains the reusable estimator and copy checks. `injections.csv`, `traces.json`, `family_method.csv`, `family_draws.csv.gz`, `checks.json`, and `blind_summary.csv` preserve the evidence. An independent rerun of all seven noiseless cases from frozen inputs matches the original run. The bundled source algorithm is unchanged and credited in `files/NOTICE.md`.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-516c040335db. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Analysis date 2026-11-11. The campaign-machine signature is not a personal authorship claim. One numerical thread and no agents were used.

## References

- SCI d9bdf1f8fd55b950ba2f985c2d9e934d034ca6eee444716ace775b1e3b229d26: seven-product correction, source algorithm and fitted calibration.
- SCI 25e4afb2b92ff314218571cb2ed551960f44cbfbf401d42334657f47f1dbbe7b: fully shared-error bounds; this study tests partial families.
- Menne and Williams (2009), doi:10.1175/2008JCLI2263.1.
- WMO (2020), Guidelines on Homogenization, WMO-No. 1245. https://dgm-meteo.github.io/wmo-clino/Docs/WMO2020_1245_en_Guidelines%20on%20Homogenization.pdf
- Copernicus, Climate Bulletin: About the data and analysis. https://climate.copernicus.eu/climate-bulletin-about-data-and-analysis (accessed 2026-11-11).
