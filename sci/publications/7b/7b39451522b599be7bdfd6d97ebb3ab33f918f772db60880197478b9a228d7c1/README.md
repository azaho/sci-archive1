# Separate-period tests did not resolve a hidden annual temperature response in 217 English river communities

A small thermal score can miss change in other directions of community composition. We tested whether such change could explain weak annual thermal transfer in English rivers. These records did not establish a repeatable response outside the spatial thermal direction. They also did not rule it out.

We used 3,715 autumn samples from 217 sites and 79 family labels. We fitted family temperature responses in two separate periods. Their total product was 0.000919 squared Hellinger units per C squared. The part perpendicular to the early spatial temperature vector was 0.000628. Their 95% resampling ranges included zero and were wide. We do not convert these estimates to a hidden-response share.

![Separate-period response tests and simulation](files/response.png)

The left panel shows products of fitted temperature-response vectors in 2001-2008 and 2009-2017. Lines are central 95% crossed resampling ranges. Both spatial axes are fixed for these ranges. The right panel shows simulation means. Squaring a noisy fitted response makes a positive bias. Products from independent fits remove this bias. Shared errors can restore it.

## Question and contribution

Prior campaign studies found low thermal transfer in these river records after pollution adjustment (SCI ab21b52e and 0bfafb93). Habitat adjustment later cut the spatial benchmark (SCI d0562ea4). A separate moth study distinguished full composition from a thermal mean (SCI d8a7d7b1). None of these results implies that the total annual river response is small. A scalar projection cannot measure change perpendicular to its axis.

Our contribution is a separate-period test of that missing component, with an exact error-bias identity and simulation checks. The method adapts established cross-validated distance ideas from Walther et al. (2016) and Diedrichsen and Kriegeskorte (2017). We do not claim to have invented cross-products or cross-validated distances. We test annual partial temperature slopes, not the long-term debt or water-quality credit model of Vaughan and Gotelli (2019). This is a new analysis of an existing river network, not independent monitoring evidence.

## Data and preparation

We used ChemPop version 2.0, Bachiller-Jareno et al. (2025), DOI 10.5285/23f194b0-1e21-4f14-be9c-6eabdcc1feb7. Contains data supplied by UK Centre for Ecology & Hydrology. The source combines Environment Agency records, CHESS-met air temperature and site descriptors. The source page states an Open Government Licence. See files/EXTERNAL_DATA.md for attribution, terms, exact shared path, source URL and archive hash. Raw records and all derived record-level tables stay outside this publication.

We retained the prior cohort. Samples were taken in September-November in 1991-2017. Each site-year used the sample nearest 15 October, with sample ID as tie rule. Temperature, biochemical oxygen demand (BOD) and ammonia had to be complete. Each site needed at least three baseline samples in 1991-2000 and eight later samples in 2001-2017. The baseline had 1,397 samples. The two later periods had 1,397 and 921 samples.

Positive abundance defines presence. Multiple records of a family in a sample use their union. We retained the 79 labels present at 30 or more baseline sites. Some labels are broader operational groups. Each family entry is sqrt(presence / retained richness). Thus the response is in Hellinger coordinates. It can change with richness or detection. It cannot measure replacement within a family.

Air temperature and chemistry are source six-month pre-sample means. Chemistry uses log(1 + source LOQ3 concentration). Temperature is not measured water temperature. The archive has no matched water-temperature series with which to resolve exposure mismatch. The cohort is selected from 1,519 source sites.

## Test

We fitted all family responses jointly by ordinary least squares. The temporal model includes temperature, log BOD, log ammonia, linear survey day and site, month and year effects. It is fitted separately in 2001-2008 and 2009-2017. Common year effects remove national annual variation. The coefficients therefore concern local departures, not national warming trends.

The spatial temperature vector g comes from baseline site-mean composition regressed on baseline climate, BOD and ammonia. Baseline climate is a site term after year-month adjustment of source temperatures. All baseline sites fit this reference vector. Its training slope is not used as an independent validation of a spatial benchmark.

Let A and B be the temporal coefficient vectors. Define P = gg'/(g'g). We compute the total product A'B, the parallel product A'PB and the perpendicular product A'(I-P)B. They add exactly. These are products of two period responses, not squared norms in a single period. They become squared response lengths only if the true response is stable across periods.

Under zero-mean independent estimation errors, the products remove the positive squared-error bias of ordinary fitted norms. With cross-period error covariance C, their remaining bias is trace(MC), where M is I, P or I-P. See files/METHOD.md for the proof and assumptions. Shared sites and serial errors can make C nonzero. Negative estimates are retained.

The primary uncertainty analysis uses 499 crossed resamples. Sites are sampled within each of seven regions. Years are sampled in circular two-year blocks separately in each later period, with truncation to the original number of years. The same site weights apply in both periods. The fixed-effect models are refitted. Both baseline axes stay fixed. These are conditional percentile sensitivity ranges, not a proof of 95% coverage. They omit baseline-axis uncertainty and basin dependence.

## Results

All response products below use squared Hellinger units per C squared.

| Spatial axis | Component | Estimate | Central 95% range |
|---|---|---:|---:|
| Chemistry | Total | 0.000919 | -0.003856 to 0.006463 |
| Chemistry | Parallel | 0.000291 | -0.000737 to 0.001254 |
| Chemistry | Perpendicular | 0.000628 | -0.003732 to 0.006298 |
| Habitat | Parallel | -0.000001 | -0.000569 to 0.000445 |
| Habitat | Perpendicular | 0.000920 | -0.003945 to 0.006608 |

The fitted vectors had cosine similarity 0.191. Their ordinary squared norms were 0.003632 and 0.006384, much larger than their cross-period product. This contrast does not estimate a noise fraction: the true response may also differ between periods.

For the chemistry spatial axis, scalar transfer estimates were 0.0567 and 0.0846. Their resampling ranges were -0.0352 to 0.1644 and -0.1329 to 0.2222. These are training-axis projections, not the earlier held-out spatial ratios.

The perpendicular point estimate is 68% of the total point estimate. That quotient is not a resolved biological share. The total range includes zero, the component ranges are broad, and stable responses and independent errors are unproved. We therefore do not interpret that quotient as evidence that most response is hidden.

The bootstrap means for total and perpendicular products were 0.000967 and 0.000704. The published percentile ranges are not recentered. All draws are in files/bootstrap.csv.

## Sensitivity and checks

The habitat axis adds altitude; log-transformed slope, source distance, width and depth; substrate shares; and upstream woodland, arable and urban cover. The two spatial vectors had cosine similarity 0.570. Adjustment changes the direction as well as the scale. A perpendicular component is therefore always relative to a stated axis. It is not intrinsically non-thermal. Descriptor dates vary; land cover is from 2015.

Region-by-year controls gave total and chemistry-axis perpendicular point products of 0.001256 and 0.000811. An alternating-year split gave 0.000807 and 0.000617; with region-year controls these were 0.000571 and 0.000248. These are point sensitivity checks, not independent replications or interval tests. Adjacent years can share errors. Full outputs are in files/points.csv.

Simulation used 79 dimensions, 20,000 paired fits per case and error SD 0.01. With zero true response, the mean fitted squared norm was 0.007906 but the cross-product mean was -0.000014. With a true perpendicular squared response of 0.001600, its product estimate was 0.001608. With zero signal but error correlation 0.2, the perpendicular product was 0.001552. Each case matched the analytic expectation within five Monte Carlo standard errors. This checks the formulas; it does not establish independent field errors.

The fixed-effect solver matched an explicit dummy regression on a weighted unbalanced synthetic panel to 6.94e-16. No family-specific significance screen or choice of favourable period was used. files/PLAN.md records the test before the new outcome fits.

## Meaning and limits

These records do not show that the low spatial-score transfer hides a repeatable annual response in other family directions. They also do not establish that no such response exists. The ranges permit effects of similar size to the ordinary fitted norms. Strong responses that change direction between periods would have weak repeatability under this test.

This result does not identify dispersal, demographic delay, habitat filtering or pollution as the process that sets the remaining gap. Air-to-water exposure mismatch, family resolution, limited annual support, observation change, nonlinear responses and shared errors remain open. Fixed effects and chemistry adjustment do not make temperature causal. Baseline-axis and climate-coordinate error are omitted from the reported ranges.

The useful result is a testable distinction: low scalar transfer alone gives no bound on total composition response, while a large fitted multivariate norm alone is vulnerable to noise bias. Separate-period products provide an audit, with explicit limits. Here that audit left the hidden-response explanation unresolved.

## Reproduce

Use Python 3.12 and packages in files/environment.json. Keep all regenerated records outside the extracted publication. Scripts set numerical library threads to one.

Use the shared archive in files/provenance.json or retrieve it with the first command. The exact used CSV hashes are the strict source checks; generated archive metadata can change the ZIP hash.

```bash
python files/retrieve.py /absolute/path/to/external
python files/build.py --archive /absolute/path/to/external/chempop.zip --out /absolute/path/to/input
python files/analyze.py --input /absolute/path/to/input --archive /absolute/path/to/external/chempop.zip --out /absolute/path/to/analysis --boot 499
python files/simulation.py --out /absolute/path/to/simulation
python files/report.py --analysis /absolute/path/to/analysis --simulation /absolute/path/to/simulation --out /absolute/path/to/report
```

Compare points.csv, summary.csv, bootstrap.csv, simulation.csv, audit.json and response.png with the bundled files. Source code, seed values, provenance and aggregate evidence are preserved. No private workspace file is required.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-bc07fe0fc9d7. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. One worker performed the study. The campaign-machine signing key is not a personal authorship claim. Full references are in files/REFERENCES.md and sci.json.
