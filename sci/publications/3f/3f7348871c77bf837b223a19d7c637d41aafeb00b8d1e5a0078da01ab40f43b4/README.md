# Archived USGS landslide maps for three of six earthquakes had uncertainty moments outside the stated beta distribution bound

Campaign 11_07_2026. Job sci-1107-hp-earth-and-ocean-sciences-6b8f0a64ce8c. Topic: earth-and-ocean-sciences. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Main result

Uncertainty grids in three of six selected USGS landslide cases cannot define the beta distributions that the product method prescribes. The failure affects a small fraction of cells. A broader test shows a tail difference when the beta method is compared with exact nonlinear propagation under an added Gaussian input-error assumption.

The support-bound failure is exact and does not assume Gaussian error. The tail comparison depends on that error law. We did not test observed landslide coverage.

We used released grids for six earthquakes. For each case, we selected the earliest usable archived UPDATE and the latest UPDATE. We kept finite cells with estimated areal coverage C at least 0.002 and positive standard deviation s. The six earliest usable products have 920,485 selected cells.

- **383 cells (0.0416%) fail the documented support bound.** Haiti has 7, Turkey 4 and Hualien 372. A variable on [0,b], where b is about 0.256, must have variance at most C(b-C). Stated variance exceeds this limit by up to a factor of 3.42. All 383 failures remain over the export-rounding ranges.
- **Puerto Rico, Luding and Morocco have no failures.** No selected cell in any case fails the wider physical bound [0,1]. The failure concerns the documented beta representation with its model maximum.
- **The conditional tail difference is wider.** In cells with feasible beta shapes, nominal 95.45% beta intervals contain 85.76-89.92% of the exact Gaussian-input reference mass, by case. The equal-case mean is 88.70%. Nominal 68.27% intervals contain 69.30-72.31%, so one interval level does not describe the tail error.
- **The same calculation changes means.** Exact reference means summed over the selected cells with cell-area weights are 1.42-2.59 times the issued sums. These sums are not the regional alert statistic. We did not apply its additional PGA threshold.
- Latest products retain 4, 2 and 311 invalid cells for Haiti, Turkey and Hualien. Their conditional 95.45% masses range from 85.76% to 90.37%. Puerto Rico has the same single usable UPDATE in both selections. These are overlapping products, not independent samples.

![Case audit](files/figures/case_audit.png)

## Cases and archive scope

| Earthquake | GF / ShakeMap version | Delay (hours) | Selected cells | Invalid cells | Reference mass in 95.45% interval | Exact mean / issued sum |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Puerto Rico 2020 | 1 / 13 | 8797.41 | 3,413 | 0 | 85.76% | 2.586 |
| Haiti 2021 | 9 / 10 | 79.14 | 59,918 | 7 | 89.92% | 1.607 |
| Luding 2022 | 4 / 4 | 261.21 | 104,999 | 0 | 88.44% | 1.572 |
| Turkey 2023 | 9 / 12 | 283.26 | 574,551 | 4 | 89.74% | 1.421 |
| Morocco 2023 | 10 / 10 | 72.40 | 61,415 | 0 | 88.79% | 1.760 |
| Hualien 2024 | 3 / 3 | 1.92 | 116,189 | 372 | 89.57% | 1.490 |


Reference mass uses area weights and only feasible beta cells. The mean ratio uses all selected cells. We make no independence assumption for cells and use no cell-count significance test.

The fixed case set is illustrative, not random. The local plan followed inspection of source methods and one Hualien file header and value range. It was not registered or timestamped independently.

The archive does not support a first-issued test for this set. We required status UPDATE and a listed HDF5 longer than eight bytes, then checked signatures, bytes, hashes and internal labels. Several older entries have no HDF5 or have two-byte placeholders. Several early Hualien entries are now marked DELETE. The earliest usable Hualien UPDATE is version 3, about 1.92 hours after origin. The Puerto Rico file is a later product, about one year after origin. All delays appear above. The amendment in files/ANALYSIS_PLAN.md records this scope change.

## Question and method

Earlier campaign tests found narrow first ShakeMap PGA and PGV intervals. A later audit showed that shared station errors prevent a simple assignment to an earthquake-wide variance term. We extend the research to another product and test a specific algorithm. We do not reuse those studies' station data or assign our result as the cause of their findings.

The ground-failure model estimates the fraction of a cell affected by landslides. It converts logistic-model output through a nonlinear rule. Its uncertainty code uses a first-order derivative. The beta recipe takes the resulting C and s as mean and standard deviation on a bounded interval. The method is in [Allstadt et al. (2022)](https://doi.org/10.1177/87552930211032685); the model is from [Nowicki Jessee et al. (2018)](https://doi.org/10.1029/2017JF004494).

The source transform is

    P = 1 / (1 + exp(-x))
    C = g(x) = exp(-7.592 + 5.237 P - 3.042 P^2 + 4.035 P^3)

Its upper limit is b=0.25614796837915954. For a variable on [0,b], nonnegative Y(b-Y) gives Var(Y) <= E[Y](b-E[Y]). This is a known result; see [Bhatia and Davis (2000)](https://doi.org/10.1080/00029890.2000.12005203). A proper beta needs strict inequality. We test this condition, the rounded upper bound 0.256, and the wider physical bound 1.

For a conditional alternative, the published derivative formula permits recovery of x=g^-1(C) and a combined error scale t=s/g'(x). We then **add the assumption** X=x+tZ, where Z is standard normal. Exact propagation through g gives quantile g(x+t Phi^-1(q)) at probability q. No simulation or beta approximation is needed. The median stays C; the mean generally changes.

In some low-coverage cells, the beta recipe puts reference probability below the model's positive lower limit. Its upper tail is also too short under the Gaussian reference. This explains why the 68% and 95% comparisons differ. It is an algorithm comparison under stated assumptions, not proof about true landslide probabilities.

Prior work includes forward uncertainty propagation for logistic geospatial models; see [Zhan et al. (2023)](https://doi.org/10.1016/j.enggeo.2023.107271). Our contribution is the released-grid audit and recovery of a combined scale from two output grids. The variance inequality and the general principle of nonlinear propagation are not new.

Full equations, proof, assumptions and spatial limits are in files/METHOD_AND_PROOF.md.

![Nonlinear mechanism](files/figures/nonlinear_mechanism.png)

## Evidence checks

All 12 selections passed checks against the frozen catalogue, listed byte lengths, HDF5 event and ShakeMap labels, and info.json labels. The checks also caught an early pairing error between Hualien versions; it was fixed before the reported six-case results.

For the five cases with uncertainty TIFFs, complete finite-value comparisons give a maximum HDF5-to-TIFF SD difference below 3.8e-9. NoData masks are decoded first. Puerto Rico has no paired TIFF. Thus the support failures occur in released uncertainty fields.

All 383 earliest-product failures persist under worst-case rounding. A separate corner sensitivity changes C by 0.00005 and s by 0.0000005. Conditional 95.45% masses remain between 85.51% and 90.03% over the six cases and corners. These are sensitivities, not global optimisation bounds.

Independent numerical integration checks 20 theoretical cases, with logit locations -3 to 4 and error scales 0.5 to 3. The maximum mean difference from 128-node Gauss-Hermite integration is 3.2e-9; the maximum SD difference is 2.5e-8. Inverse and analytic interval checks pass. Running only the public source beta-interval function gives exactly the same endpoints as our implementation. Across all audited cells, 64 to 128 quadrature nodes change each area-summed mean by less than 6.7e-8 in relative terms. Every exact-reference moment pair obeys the support bound.

## Use and limitations

The method supplies a cheap output check and an exact conditional quantile tool. A production method can reject infeasible beta shapes. Under Gaussian latent error, it can propagate quantiles through the monotone transform. Keeping C as a mean while changing only an SD defines a different model and needs separate validation.

1. Six selected earthquakes do not identify a failure rate across USGS products. Most files are later versions. This is not a first-response performance test.
2. The exact moment failure affects only 0.0416% of selected cells. It does not establish a large error in regional hazard or population alerts.
3. Gaussian combined error is an added reference assumption. A stated SD and independent inputs do not prove that law. The exact alternative is not a calibrated correction.
4. We hold masks, clipping and other predictors fixed. We recover one combined scale, not separate shaking, model and source-error components.
5. Cellwise quantiles do not give an interval for total area. Spatial covariance and uncertain masks remain open. Means can be summed without independence; variances and quantiles need a joint model.
6. We do not verify an exact production executable. The pinned public source implements the documented equations and rounding. Released grids and matched TIFFs are the direct evidence.
7. No observed landslide calibration is claimed. A candidate Hualien inventory had no explicit mapping boundary file and used images from several weeks. We did not label unlisted land as known absence.

The result identifies one exact inconsistency in a documented operational uncertainty representation and provides a reproducible conditional alternative. It does not show that the beta approximation causes earlier ShakeMap undercoverage, or that the alternative improves observed landslide forecasts.

## Reproduction and rights

From an extracted bundle, run:

    bash files/code/run_all.sh /absolute/local/scratch/gf-audit

Python 3.12 and packages in files/provenance/environment.json are required. The script uses one numerical thread. It reuses exact shared files where available, otherwise retrieves about 310 MB into separate scratch. It checks hashes and fails if a source changed. See files/REPRODUCE.md.

The 43-entry manifest records exact URLs, hashes, sizes, versions and shared paths. It includes 11 distinct product releases, six catalogue snapshots and five public source files. Original code, aggregate tables, proofs and static figures are bundled. Raw rasters, source code and polygons stay external. See files/EXTERNAL_DATA_NOTICE.md for attribution and external terms. The unchanged SCI baseline LICENSE covers the bundled work.
