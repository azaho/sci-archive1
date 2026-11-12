# At least 308 of 1,289 released TESS CPV sector shifts need corrections above 1/60 cycle to define a phase per star

Job: **sci-1107-hp-astronomy-d7eb2ff0e2f5**. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite automated worker did this study. No agents were launched. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We tested whether the released changes in dip phase relative to spot phase can be treated as the motion of one clock per star. They cannot all have this meaning with small corrections. In the source-quality sample of 65 TESS complex periodic variable (CPV) stars, **at least 308 of 1,289 sector-pair shifts (23.9%) require a correction larger than 1/60 rotation cycle** to agree with any scalar phase history for each star. This result is a lower bound on the released measurements. It has an integer-checked certificate and needs no probability model for material motion or measurement noise. It is not a bound on the fraction of material that moves.

We also compared continuous longitude diffusion with occasional phase resets. Neither model gives a clear prediction advantage when an entire star is left out of fitting. The reset-minus-diffusion log score is **0.072 nats per star, with a conditional 95% star-bootstrap interval of -0.033 to 0.173**. A stricter sample in which both shapes repeat passes the main closure check, but it also does not distinguish these two processes. The evidence supports loss of pattern memory. It does not select a unique continuous random walk of material.

![Phase closure and prediction tests](files/phase_tests.png)

Figure 1. Left: a scalar phase must give zero closure around three epochs. The bars show the fraction of triples with closure above 0.05 cycles, first averaged within each star. Intervals resample stars. The strict subset has zero such triples among 43 triples from 15 stars. This zero count is not an upper confidence limit. Right: prediction scores when each tested star is absent from fitting. Intervals resample the resulting star scores and condition on the fitted folds. Diffusion and resets are not clearly separated. A fixed random frequency performs worse than diffusion in the strict subset.

## Question and prior work

CPVs are young, rapidly rotating low-mass stars with sharp optical dips. Bouma et al. (2024, doi:10.3847/1538-3881/ad0c4c) reported dip evolution over about 100 rotations. Spectroscopy in Bouma et al. (2026, arXiv:2609.00136v1) supports circumstellar plasma in corotation and leaves the cause of the optical opacity open. These results make the distinction between a moving structure and a changing pattern useful.

The direct source, SCI b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34, compared dip and spot shifts between sectors. It reported a relative-phase diffusion coefficient near 1e-5 cycles squared per day. Its pair fits allow a constant uniform outlier fraction. Its short-sector fits and long-sector comparisons were separate tests. We test only the released **between-sector** shifts here. We do not remeasure the short-sector phases or the mean dip-minus-spot frequency.

We searched the shared campaign for CPV, phase and random-walk results before choosing this study. Related campaign work, SCI cede8f8ad02163f7a6f3426457fd4b1f43da2faf8cc4081cd06beaff8b701a2c, found that short-window Fourier changes do not follow the simple small-diffusion order law. It also showed that replacement and large phase resets can share second-order statistics. Our contribution uses different published measurements. It adds a necessary phase-closure test, a certified count bound on incompatible shifts, and prediction for stars left out of fitting. Angular consistency is an established mathematical problem (Singer 2011, doi:10.1016/j.acha.2010.02.001). Stochastic resetting is an established process class (Evans, Majumdar and Schehr 2020, doi:10.1088/1751-8121/ab7cfe). We do not claim either method in general as new.

This study is an exploratory reanalysis, not a registered test. The 0.05-cycle main threshold is the source's definition of phase anchoring. We also report thresholds of 0.02 and 0.10 cycles.

## Data

The direct source contains 1,763 sector pairs from 70 stars. Each pair has the time gap, the best circular cross-correlation shift of the dip template, the corresponding spot shift, their peak correlations, and the wrapped difference of the shifts. The underlying TESS observations cover sectors 1-107 in 2018-2026. Pair gaps range from 21.75 to 2,908.42 days. We keep the source selection and use no new labels.

| Sample | Rule | Pairs | Stars | Complete triples | Stars with triples |
|---|---|---:|---:|---:|---:|
| All | All released pairs | 1,763 | 70 | 11,895 | 49 |
| Source-quality | Dip correlation >0.5 and spot signal-to-noise >10 | 1,289 | 65 | 5,111 | 41 |
| Both shapes repeat | Dip correlation >0.8 and spot correlation >0.95 | 165 | 44 | 43 | 15 |

The strict rule is exactly the source rule. It does not additionally require the source-quality cuts. Thus it is a separate sensitivity selection. A complete triple has all three pair measurements in the stated sample. Triples overlap. We do not treat them as independent.

The input files are `files/data/anchor_pairs.csv.gz` and `files/data/anchor_injection_pairs.csv.gz` in the verified source publication. Exact entry hashes, source ZIP hash, source path and software versions are in `files/provenance.json`. The shared source path is `/mnt/dell-data/campaigns/11_07_2026/b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34.zip`. This is the supplied HP SSD compatibility path. No file from the shared datasets store is used. No new raw data are downloaded. Source records and per-star derived records remain outside this publication.

## Phase closure and the count bound

Let `d_ij` be the released dip-minus-spot shift from epoch i to epoch j, in cycles. Let `wrap` return a value in [-0.5, 0.5). If there is one relative phase `theta_i` at each epoch, exact shifts must obey

    d_ij = wrap(theta_j - theta_i)
    C_ijk = wrap(d_ij + d_jk - d_ik) = 0.

This identity holds for diffusion, constant drift, abrupt resets and any other scalar phase history. It also holds if each epoch has an arbitrary phase-origin offset, since that offset cancels around the triangle. It need not hold for maxima of pairwise cross-correlations when shapes change or a different peak is selected. A high peak correlation alone does not prove closure.

All source shifts are on a 2,000-point phase grid. We convert them to integer bins and do the triangle sums modulo 2,000. This avoids numerical decisions for values exactly at a threshold. The maximum input deviation from that grid is stored in the results.

In the source-quality sample, the fraction of relative-shift triples with `|C| > 0.05` is 48.6% when all triples have equal weight. It is **31.7% (22.1-41.4%)** when each of the 41 stars with triples has equal weight. The latter interval resamples stars 4,000 times. For dip shifts alone the equal-star fraction is 22.9%; for spot shifts alone it is 9.5%. Both template components contribute to the inconsistency. The strict sample has no relative closure above 0.05 cycles, but has one incompatible pair required at the smaller 0.02 closure threshold.

To convert closure to a count bound, let `e_ij` be the circular correction from a released shift to the shift of any proposed scalar phase history. The triangle inequality on the circle gives

    |C_ijk| <= |e_ij| + |e_jk| + |e_ik|.

If `|C_ijk| > h`, at least one of its three corrections is larger than `h/3`. Put a nonnegative weight on each such triangle. Require the sum of triangle weights on every edge to be at most one. The sum of all triangle weights is then a lower bound on the number of edges with corrections larger than `h/3`: every bad triangle needs an affected edge, and no edge pays more than one unit of weight. This is the dual of a fractional covering problem.

We solve the linear program separately within each star. We round its dual weights down to integer millionths and check every edge load with integer arithmetic. If needed, we scale down again before checking. The ceiling of each feasible rational dual sum is a valid integer lower bound for that star. We then sum those bounds. The result is certified by feasibility of the stored rational weights, not by a solver tolerance or by assumed optimality. The code regenerates all certificates in separate scratch.

| Required correction above | Source-quality: minimum affected pairs | All pairs: minimum affected pairs |
|---|---:|---:|
| 1/150 cycle (0.00667) | 352 / 1,289 (27.3%) | 535 / 1,763 (30.3%) |
| 1/60 cycle (0.01667) | **308 / 1,289 (23.9%)** | 505 / 1,763 (28.6%) |
| 1/30 cycle (0.03333) | 275 / 1,289 (21.3%) | 483 / 1,763 (27.4%) |

The main bound is positive in 25 of the 65 source-quality stars. If the minimum fraction within each star is averaged equally over all 65 stars, its lower bound is 8.2%. The 23.9% result refers to **pair measurements**, not a typical star or an occurrence rate. A zero bound for the strict sample at 1/60 cycle does not prove all its shifts are correct: triangles need not detect every inconsistency, and 29 of its 44 stars have no complete triple. The bounds are necessary and can be conservative.

![Correction bounds and a fixed-center control](files/closure_bound.png)

Figure 2. Left: necessary pair-correction bounds with exact rational dual certificates. Labels give the minimum counts. Lines only join the tested tolerances. Right: one declared synthetic example has four fixed Gaussian centers and changing depths. Pairwise cross-correlations select shifts of 0, 0 and 0.41 cycles, despite zero motion of every center. The three pair correlations are 0.965, 0.549 and 0.662. This is an existence example, not a fit to a real star.

## Circular process comparison

We fit the full released wrapped shift, rather than only the flag `|d| < 0.05`. Let `W(d; v)` be the wrapped normal density with zero mean and variance v before wrapping. The uniform density on a unit circle is one. The general density used here is

    p(d | t) = 1 - A(t) + A(t) W(d; v(t))
    A(t) = (1-f) exp(-lambda t).

The five models are:

| Model | Variance v(t) | Reset rate |
|---|---|---|
| Static | sigma0^2 | lambda = 0 |
| Diffusion | sigma0^2 + D t | lambda = 0 |
| Reset | sigma0^2 | lambda fitted |
| Diffusion plus reset | sigma0^2 + D t | lambda fitted |
| Random fixed frequency | sigma0^2 + q t^2 | lambda = 0 |

In the reset model the phase is constant between Poisson events. At an event it takes a new independent uniform longitude. The displayed density is its pair-increment law, convolved with a wrapped normal measurement width. It is not resetting to a fixed physical location. Here f is a constant uniform contamination fraction. Neither f nor sigma0 is a measured instrument error. The diffusion convention is `Var(increment) = D t`, without an extra factor of two.

For nonzero integer m, the expected circular moment is

    E cos(2 pi m d) = (1-f) exp[-lambda t - 2 pi^2 m^2 v(t)].

Diffusion broadens the coherent peak with time and gives an m-squared decay rate. Resets remove mass from a peak of fixed width and give an order-independent reset rate. Both can lower the fraction of aligned pairs. Aggregate moments for orders 1-5 and four gap bins are retained in the results; they are supporting descriptions, not independent tests.

The main fit gives each star total weight one, divided equally among its pairs. A separate fit gives every pair weight one to recover the source convention. These are composite pair scores, not a full joint likelihood for each star's trajectory. All models have zero systematic drift and share their parameters across stars within a selected sample. Closure failures are one reason not to interpret all pairs as exact increments. We do not assign a chi-squared p value to differences of these scores.

We refit 300 bootstrap samples of stars for parameter intervals. We also leave one whole star out in turn, fit the other stars with equal-star weights, and average the test log densities over that star's pairs. Positive score contrasts favor the first model. Intervals below resample the held-out star scores 10,000 times. They are conditional on the fitted folds; they do not refit every fold in each score bootstrap or cover all processing errors.

| Prediction contrast | Source-quality: mean (95% interval), nats/star | Both shapes repeat: mean (95% interval), nats/star |
|---|---:|---:|
| Reset minus diffusion | 0.072 (-0.033, 0.173) | 0.036 (-0.136, 0.241) |
| Diffusion plus reset minus diffusion | 0.074 (-0.016, 0.158) | 0.071 (-0.072, 0.236) |
| Diffusion plus reset minus reset | 0.002 (-0.040, 0.039) | 0.035 (-0.040, 0.108) |
| Random fixed frequency minus diffusion | 0.029 (-0.073, 0.125) | -0.126 (-0.243, -0.031) |
| Diffusion minus static | 0.199 (0.095, 0.300) | 0.101 (-0.045, 0.239) |
| Reset minus static | 0.271 (0.144, 0.386) | 0.138 (0.003, 0.295) |

Thus time-dependent memory is useful for prediction in the main sample. No tested comparison selects diffusion over resets. The strict sample disfavors a homogeneous random fixed-frequency model relative to diffusion; this does not rule out all shear or differential-rotation models.

The equal-star source-quality diffusion fit gives D = 1.03e-5 cycles squared/day, with a conditional parameter-bootstrap interval of 0.35e-5 to 2.12e-5. It is compatible with the source's scale. The reset fit instead gives a 401-day time (208-608 days) and sigma0 = 0.0179 cycles. In the combined model, D = 0.54e-5 and the reset time is 786 days. Its D interval reaches the lower search bound of 1e-11, which acts as negligible diffusion on these time gaps. The data do not provide a lower bound on continuous diffusion once resets are allowed in this model. These are pattern-model parameters, not material lifetimes.

Weighting matters. In the source-quality sample, reset minus diffusion gives an in-sample score of -0.0015 nats per pair with pair weights, but +0.0803 nats per star with equal-star weights. In the strict sample the corresponding contrasts are -0.0779 and +0.0489. A few well-observed stars therefore change the preferred average. Neither average is an independent replication. In 300 selections of one random pair per star, reset has a higher fitted score in 92% of main-sample selections and 84% of strict selections. These are pair-selection sensitivities, not confidence probabilities.

## Checks and synthetic controls

The wrapped densities integrate to one to the reported numerical precision. Their first four circular moments agree with the analytic formula to less than 5e-16. Analytic gradients agree with finite differences to less than 2e-9 on the declared test points. All reported main fits, parameter bootstrap fits and held-out fits report optimizer success. A separate check enumerates every binary covering choice in 40 small systems; no certified count exceeds the exact minimum.

One thousand arbitrary scalar phase triples close to floating precision. Independent rounding of their shifts onto the source grid gives closure at most 0.0005 cycles. Two thousand rigid translations of fixed synthetic profiles also close to floating precision. Thus the 0.05-cycle test is much larger than grid-rounding closure.

The fixed-center control in Figure 2 uses centers at 0, 0.16, 0.41 and 0.67 cycles, Gaussian width 0.018 cycles, and independent lognormal depths with log standard deviation 0.8 at each of three epochs. Of 2,000 trials, 1,954 have all three correlations above 0.5; 40.2% of those have closure above 0.05 cycles. Of 223 trials with all correlations above 0.8, 4.9% fail. This control has no raw-cadence noise, period fitting or fitted stellar physics. It shows that shape change is sufficient to break closure, not that this exact process caused the real failures.

We also draw one actual gap per star and simulate one independent shift at each of the 65 gaps. With homogeneous parameters fixed at the main diffusion fit, diffusion has a better fitted score in 98.3% of 300 trials. With parameters fixed at the reset fit, reset wins in 99.0%. These are ideal pair-level recovery tests. They show that the code can separate these particular homogeneous truths. They do not calibrate a rejection probability for correlated real trajectories, selection, model heterogeneity or the source measurement procedure.

The source's two-half injection table is used only to reproduce its null control description. It does not contain multi-sector triples and cannot calibrate their closure errors. We do not use it to set a statistical threshold for the count proof.

## Implications and limits

The new firm result is a limitation on using pairwise template shifts as physical longitude increments. At least 308 released source-quality offsets cannot all be close to a scalar relative phase. The cause can include changing dip depths, new features, spot evolution, ambiguous correlation peaks, or measurement errors. The proof does not identify the cause or show that the source's flux measurements are wrong.

The process comparison gives an explicit alternative to continuous diffusion. It preserves evidence for loss of phase memory but does not measure the motion, supply or life of material. The low contamination fraction of the fitted reset model should not be read as a physically verified error rate: that model fits marginal pair densities and does not enforce their joint closure. The strict sample removes the large observed triangle failures and still leaves the model distinction unresolved.

All observations, labels and reductions are inherited from one source. We did not inspect raw pixels, refit cadence data, estimate the covariance of the cross-correlation shifts, or independently classify stars. The masks select repeatable shapes and can favor memory. There is no phase-error estimate for each pair in the released table. Differences between stars and between observing seasons can mimic a single diffusion coefficient or reset rate. A constant uniform contamination term is only one error model. Phase evolution in the spot reference cannot be separated from dip evolution by these relative shifts alone.

The count bound is exact for the released grid-valued shifts and stated tolerances. It has no sampling interval because it is a deterministic statement about those records. Its interpretation for the stellar population is limited by selection and repeated observations. Bootstrap intervals elsewhere are not proof of a universal physical process. We have not refuted magnetic confinement or excluded a component of true diffusion. We have not reanalysed the source's within-sector frequency agreement.

A stronger physical measurement now needs a phase definition that passes multi-epoch closure, with raw-cadence controls for evolving shapes. A joint fit with separate centers and depths, validated on epochs absent from fitting, or a repeated velocity-resolved line tracer could supply such a label. Closure and the provided correction-bound code are useful checks before converting an empirical shift into a material transport coefficient.

## Reproduction and package

Use Python 3.12, NumPy, SciPy, pandas and matplotlib, plus SCI 0.3.0. Exact installed versions are in `files/provenance.json`. From an unpacked publication, run:

```sh
python files/reproduce.py /path/to/b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34.zip /path/to/separate-scratch /path/to/new-output --bootstrap 300
```

The script verifies the complete source bundle, checks its exact identity and entry hashes, and extracts only the two required tables into separate scratch. It runs the analysis, rational certificates, controls and figures in sequence with one library thread. It rejects scratch or output paths inside this signed bundle. Regeneration takes several minutes on the campaign host and uses no more than one compute process at a time. No private workspace, downloaded raw data or local service is needed.

To inspect only the main deterministic bound, use `python -B files/inspect_bound.py SOURCE_ZIP SEPARATE_SCRATCH NEW_OUTPUT`. This short path verifies and extracts the inputs, forms the triples and checks the rational dual certificates. It does not run the process fits or resampling.

The source can be located by its exact SCI identifier. If it is not already local, use `sci pull sci:sha256:b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34` with a configured source archive, or retrieve the named ZIP from the campaign archive. The identity and hashes, rather than the current path, define the data version. The command above does not need network access once the ZIP is present.

The bundle contains original code, this text, two static PNG figures, aggregate results, fitted parameters, input provenance and numerical validation. Source records, per-star scores, triple tables and rational per-triangle certificate weights are regenerated only in scratch. The exact dual weights and their constraints can be checked there with integer arithmetic. `files/EXTERNAL_DATA.md` gives attribution and external terms. The exact SCI baseline license is installed without change.

## References

- Source phase study: SCI b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34.
- Source survey: SCI 22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0.
- Short-window harmonic diagnostic: SCI cede8f8ad02163f7a6f3426457fd4b1f43da2faf8cc4081cd06beaff8b701a2c.
- Bouma et al. 2024, AJ 167, 38, [doi:10.3847/1538-3881/ad0c4c](https://doi.org/10.3847/1538-3881/ad0c4c).
- Bouma et al. 2026, [arXiv:2609.00136v1](https://arxiv.org/abs/2609.00136v1).
- Singer 2011, Applied and Computational Harmonic Analysis 30, 20-36, [doi:10.1016/j.acha.2010.02.001](https://doi.org/10.1016/j.acha.2010.02.001).
- Evans, Majumdar and Schehr 2020, J. Phys. A 53, 193001, [doi:10.1088/1751-8121/ab7cfe](https://doi.org/10.1088/1751-8121/ab7cfe).
- Angus et al. 2018, MNRAS 474, 2094, [doi:10.1093/mnras/stx2109](https://doi.org/10.1093/mnras/stx2109), for the general ambiguity from evolving stellar surface patterns.
