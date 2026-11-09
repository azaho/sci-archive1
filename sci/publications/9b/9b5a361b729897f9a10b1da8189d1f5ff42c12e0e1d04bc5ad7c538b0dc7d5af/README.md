# Selected MICrONS pairs leave a same-scan change in response-based wiring slope uncertain

We tested whether the link between measured movie response similarity and detected connection differs for cells from the same imaging scan and separate scans. Public MICrONS v1 tables supplied 295,371 candidate directions and 8,128 connections from one mouse. A linear probability model controlled both cells, scan pairs, region-layer pairs, and geometry. The same-minus-separate slope was 0.031 percentage points per common response-correlation standard deviation. Its nominal 95 percent shared-cell interval was -0.236 to 0.298. This is a direct scan-group contrast, not a new test of the established response-based wiring rule. One animal, selected arbors, an additive model, response error and nonrandom scan groups limit inference. Code, compact inputs, source hashes, solver checks and a figure support reproduction.

![Scan contrast and separate slopes](files/scan_slopes.png)

## Question and prior evidence

Does same-scan sampling change the relation between movie response similarity and connection? Common recording noise or brain state can affect measured responses. Scan groups also differ in geometry, cells and response quality. A group contrast can identify a sampling difference; it cannot identify its cause.

[Ding et al.](https://doi.org/10.1038/s41586-025-08840-3) reported response-based wiring. SCI sha256:c59a7cc9c394931da48264dbdd64f4dd2ef21ea50f820313c35558be9be14d07 reported a positive separate-scan association after cell effects. We extend that work with a direct same-minus-separate contrast in an additive model. This is not independent confirmation or a new general wiring rule.

## Data

We used the public functional connectomics node and edge tables, release v1. Each cell has a matched anatomy ID and scan ID. Scan identity combines animal_id, scan_session and scan_idx. The animal is the single MICrONS mouse. The MICrONS collaboration includes the Allen Institute.

We kept Connected and ADP rows, excluded self pairs, required positive axon_len and dend_len, and required finite measured and model response correlations and complete scan IDs. This left 295,371 directions, 148 sources, 11,035 targets, 11,035 distinct cells and 8,128 connections. No row failed the complete-case rule after the opportunity selection. We did not add a response-quality threshold.

Same-scan pairs numbered 24,330, with 728 connections (2.992%). Separate-scan pairs numbered 271,041, with 7,400 connections (2.730%). These shares are not the slope test. There were 13 scans. Projection-layer labels were missing for 19,385 directions. They form one explicit missing-label group.

The main predictor is in_vivo_sig_corr: correlation of trial-mean responses to shared movie clips. It is not a single-trial noise correlation. The comparison is in_silico_sig_corr_cvt from model responses. We do not reprocess calcium traces or train a neural model.

## Method

The outcome is a detected connection (0 or 1). Ordinary least squares includes separate source and target intercepts, directed scan-pair intercepts, and projection-layer intercepts. Controls are cubic polynomials of log(1+axon_len), log(1+dend_len), and soma distance. Each geometry polynomial has a same-scan interaction. EM coordinates are converted from nanometres to micrometres. Standardization makes this cubic distance fit invariant to that scale.

The correlation is centered and divided by its common sample SD (0.161888). Its same-scan interaction gives the direct contrast. Both slopes use the same scale within a fit. The common-range fit uses its own SD. Additive cell effects remove cell propensities on the probability scale, not all cell-pair interactions. Additive probability fits can give values outside zero to one. We use the slope as a descriptive linear projection.

A column-scaled sparse LSMR solve removes intercept groups, with solver tolerance 1e-12 and group-mean residual checks. Shared-cell score covariance allows dependence through either biological cell in either role. It subtracts unordered pair scores so reverse directions are not counted twice. The finite-size factor uses the sum of all intercept counts and slope columns, an upper bound on rank. This gives a slightly conservative factor. Primary limits use 1.96 standard errors.

A sensitivity covariance permits dependence through either imaging scan, with 12 t degrees of freedom. Only 13 scan clusters are available. Neither method estimates animal variation or full stimulus and response measurement uncertainty. State or spatial dependence beyond these clusters can remain.

The plan is in files/PLAN.txt. Model adjustment, common-range restriction and model-response comparison are sensitivity analyses. There is one primary contrast.

## Results

| Fit | Directions | Same-minus-separate slope, percentage points per SD | Nominal 95% shared-cell interval |
|---|---:|---:|---:|
| Primary measured response | 295,371 | 0.0308 | -0.2362 to 0.2977 |
| Add model-response control | 295,371 | 0.0643 | -0.2467 to 0.3752 |
| Common correlation range | 263,242 | -0.0451 | -0.3178 to 0.2275 |
| Model-response comparison | 295,371 | -0.0711 | -0.2936 to 0.1514 |

The primary separate-scan slope was 0.3615 points per SD, with interval 0.2621 to 0.4610. The same-scan slope was 0.3923, with interval 0.1312 to 0.6534. Subgroup significance tests do not test their difference.

The scan-dependence interval for the primary difference was -0.1756 to 0.2371 points per SD. The common-range restriction used correlations from -0.14819 through 0.35732, the intersection of each scan group's 5th-to-95th percentile range.

The primary shared-cell interval includes zero. The sample does not resolve a scan-group slope difference. It does not establish equal slopes or show that shared recording effects are absent.

## Checks

The primary projection used at most 89 LSMR iterations per column. Its largest group-mean residual was 1.95e-09. A separate LSQR algorithm checked the outcome and two main predictor residuals. The largest absolute discrepancy was 2.3e-11. A direct edge-pair sum checked the covariance formula, including reverse edges, to less than 1e-12. The largest first-order single-cell shift in the primary contrast was 0.0466 points. This is an influence check, not a full deletion refit.

All raw checksums matched the dataset helper records. files/results.json and files/sample_audit.json preserve numerical output.

## Limits

One animal, selected arbors and matched cells limit transfer. Scan groups are not randomized. Their geometry, cell types, depth and imaging quality can differ. Cubic geometry controls and additive intercepts need not remove these differences. Released length fields are imperfect opportunity proxies. Missing contacts and reconstruction errors can bias the result. Calcium correlations have error and depend on a short movie sample. Model errors also vary across cells and scans. The controls and sampling target differ from earlier Poisson studies.

These approximate intervals are conditional on this mouse and summary data. They cannot establish a principle across animals, regions or behavior. A useful next test would apply this contrast in a second matched anatomy-activity animal with scan-aware trial resampling.

## Reproduction and provenance

From an extracted copy, run:

    OPENBLAS_NUM_THREADS=2 python files/analyze.py
    python files/audit_covariance.py

The scalar pair table supports offline model reproduction. [Full instructions](files/REPRODUCE.md) give raw retrieval and extraction. [Provenance](files/provenance.json) gives exact shared paths, URLs, release, sizes and SHA-256 hashes. No shared dataset was changed or downloaded. [References](files/REFERENCES.md) and [versions](files/versions.json) provide credit and environment details.

Job: sci-1107-dell-neural-structure-and-computation-de0b3af35890.
Topic: neural-structure-and-computation. Campaign: 11_07_2026.
Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort.
Date: 2026-11-09. The campaign-machine key identifies the bundle; it is not a personal authorship claim.

Credit the MICrONS collaboration, Allen Institute, Baylor College of Medicine, Princeton University and original data teams. New text, figures, derived data and code use the SCI baseline license. Source data retain their source terms and attribution. No private key is included.
