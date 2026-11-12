# Date searches did not remove the low 2020-2025 PDO mean mismatch in a model fitted to 1951-2019

The mean Pacific Decadal Oscillation (PDO) index in 2020-2025 was -1.99514. Only 2 of 19,999 simulated 75-year records had any six-year mean this low under a monthly memory and ENSO model fitted to 1951-2019. The search covered all 829 monthly start dates for a 72-month window. Thus a search over dates alone did not remove the mismatch in this statistical reference. The result changes greatly when the model and residual blocks include the recent period. It does not establish a new climate regime.

![Date search and reference checks](files/result.png)

Figure 1. Left: fixed end-period and date-search tail fractions for 12-month residual blocks. Bars show 95% binomial intervals for simulation error only. The points use (count + 1)/(draws + 1). A zero count is shown at the simulation floor of 0.00005; its lower interval bound is zero and is not visible on the log axis. Right: all-month search fractions across residual block lengths. Lines connect distinct reference cases, not a fitted physical response. Fits end in 2019 or 2025. No interval here describes uncertainty in the climate system.

## Question and prior evidence

A persistent North Pacific sea temperature pattern can affect marine conditions. Prior campaign work found that the known 2020-2025 PDO mean lay below short-memory model ranges. That work warned that selection of the period was not included in its tail fractions. We test this specific open issue: does a search over all six-year start dates make such a low mean common under the same type of reference?

We searched the shared campaign for earthquake, ocean, hydrological, PDO, PDO memory, PDO reemergence, Arctic discharge, snowmelt summer flow and PDO selection. We read the verified [mean-gap study](sci:sha256:27f15150d2de9b140a792051f912a3499b4e267541ac77f0dd7567a9e509044c), [pressure study](sci:sha256:16b453a90f36dd02aba65b5dfbc17f87952edd9314756d18909e5a2b287ef238), [annual-lag study](sci:sha256:b5c86576de293e64694c1d5d4efe276252e1b1a9f0f95385b556093c36bc25d1), and [three-product study](sci:sha256:996e2df4915e2ab8e3086f40caccc9d5b1711caecfbcc86d850f462bede2cbe5). The earlier work found historical range failures and product differences. We add a full-record date search with matched fixed-date and scanned statistics in each simulated path. We also test blocks as long as the target window and a fit that includes the target. We do not add independent observations or a physical explanation. No private worker files were read.

Newman et al. (2016), doi:10.1175/JCLI-D-15-0508.1, describe PDO as the combined effect of atmospheric forcing, tropical effects and ocean memory. Meeker et al. (2025), doi:10.1029/2025GL116122, use linear reference models to study seasonal PDO prediction skill. These works motivate our limited reference model. We used available abstracts and online text. We do not reproduce their coupled climate experiments.

The local plan in files/plan.txt preceded the computations. It is not an external registration. The target was known from prior work.

## External data and rights

We reused two unchanged shared NOAA snapshots. There were no downloads or shared-store changes. Both have 912 complete monthly pairs in January 1950 through December 2025. Incomplete 2026 is excluded. The model targets cover January 1951 through December 2025, or 900 months. No selected month is filled.

- `/mnt/dell-data/shared_datasets/ncei-ersstv5-pdo-index-20261108/ersst.v5.pdo.dat`: NCEI ERSSTv5 PDO, SHA-256 `a09ddc3f8b623bc0a262e8ade0c44cb1edf91634877f547c7074c248de620211`.
- `/mnt/dell-data/shared_datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt`: CPC ERSSTv5 Nino 3.4 anomalies, 1991-2020 reference, SHA-256 `bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012`.

files/provenance.json records exact URLs, used paths, resolved paths, sizes and hashes. The raw source tables remain outside this publication. No source records or filtered source database are bundled. The bundle contains our code, text, figure, fitted coefficients, aggregate statistics and simulated mean statistics. The SCI baseline applies to these materials. NOAA retains source credit. files/EXTERNAL_DATA_NOTICE.txt records external terms separately. Neither this analysis nor its figure is an official NOAA product.

The data are revised historical indices. Their construction can use later information. This is not a forecast that could have been issued at an earlier date. PDO is a surface pattern index, not a local temperature or total heat-content measure.

## Method

Fit ordinary least squares to:

`PDO[t] = intercept[calendar month] + a * PDO[t-1] + b * Nino34[t-1] + error[t]`.

There are 12 month intercepts and no extra constant. The primary fit uses 828 rows in January 1951 through December 2019. The sensitivity fit uses all 900 rows through December 2025. The primary a and b are 0.809183 and 0.121214. The full-record values are 0.843045 and 0.093141. All coefficients stay fixed during simulation.

For each fit, center its residuals by the overall mean. Sample circular blocks of consecutive residuals, with replacement, to make 900-month error sequences. Use block length 12 months as the primary case, and lengths 3, 36 and 72 as checks. Blocks can cross the training-record boundary. Blocks are not aligned by season. Use 19,999 independent draws per case and a recorded seed. The code runs in small batches with one numerical thread.

Each simulated history starts at the observed December 1950 PDO. Generate January 1951 through December 2025 recursively. Every simulated month uses its own preceding simulated PDO and the actual preceding-month ENSO value. No future observed PDO is inserted. ENSO is fixed even within the future target period. The monthly intercept sequence follows the observed calendar.

For each path, save three statistics: its last 72-month mean; its minimum mean across all 829 contiguous 72-month windows; and its minimum across the 70 January-start windows. Apply the same observed threshold, -1.9951389, to each. A scanned value cannot exceed the fixed-date value within a path. The observed 2020-2025 window is also the minimum across the 829 observed windows. Only one observed window reaches the threshold.

We report (1 + number at or below threshold)/20,000. The binomial intervals in summary.csv use the raw count and 19,999 draws. These are intervals for Monte Carlo sampling only. With zero counts, the two-sided 95% upper bound is 0.0001844. A zero count does not imply zero probability.

The fixed-date statistic here is drawn from the same full-history simulation as the scanned statistic. It is not conditioned on observed December 2019 PDO as in the earlier mean-gap study. Thus the comparison isolates the date search within our reference; it is not an exact repeat of that study. The initial-state effect has nearly decayed by 2020, but random model history still sets the simulated 2019 state.

## Results

All rows below use 19,999 draws. Fractions include the plus-one correction.

| Fit end | Residual block, months | Fixed-date count | All-month scan count | Fixed fraction | Scan fraction |
| --- | ---: | ---: | ---: | ---: | ---: |
| 2019 | 3 | 0 | 0 | 0.00005 | 0.00005 |
| 2019 | 12 | 0 | 2 | 0.00005 | 0.00015 |
| 2019 | 36 | 0 | 0 | 0.00005 | 0.00005 |
| 2019 | 72 | 0 | 0 | 0.00005 | 0.00005 |
| 2025 | 3 | 0 | 191 | 0.00005 | 0.00960 |
| 2025 | 12 | 2 | 231 | 0.00015 | 0.01160 |
| 2025 | 36 | 51 | 2,021 | 0.00260 | 0.10110 |
| 2025 | 72 | 79 | 5,397 | 0.00400 | 0.26990 |

The primary scan fraction has a 95% simulation interval of 0.0000121 to 0.0003612. The 2019-fit results stay rare at the simulation resolution for every block length. Two hits cannot support a precise ratio against zero fixed-date hits. We therefore do not claim a measured threefold increase for the primary case.

In the fit through 2025, the 12-month scan fraction is 0.01160, with simulation limits 0.01012 to 0.01313. The 72-month scan fraction is 0.26990, with limits 0.26372 to 0.27607. January-start scans are smaller: 0.00910 and 0.23425 in these two cases. The table in files/summary.csv includes all 24 summaries and quantiles. Eight draw tables retain all simulated mean statistics.

The full-record fit includes the very period being assessed. It changes coefficients and the empirical residual distribution together. Long blocks can then reuse sustained recent negative residual sequences elsewhere in each history. This reference treats such sequences as part of stable residual behavior. The pre-2020 reference cannot reuse them. This helps explain the sensitivity by construction; it is not a test that a particular physical mechanism caused the recent conditions. We have not separated the coefficient change from the residual-distribution change in a crossed experiment.

## Limits and next work

This is a conditional model diagnostic. It is not an exact p value for the climate system. The full search includes only the start date of a fixed 72-month lower-tail mean in one index. It does not cover selection of window width, ending year, source product, statistic, predictors, model, or topic. The campaign made many related tests. No family-wide correction is claimed.

We hold ENSO, coefficients and the starting PDO fixed. The bootstrap assumes that fitted residual blocks can be moved through time. It omits uncertainty in parameters, source revisions, index construction and model form. Circular joins can be artificial. Long blocks yield few distinct long sequences, and inclusion of the tested period can make its features easier to reproduce. The historical coverage failures in prior work show that this short-memory reference is incomplete. Small simulation fractions do not validate it.

The result rules out only one simple explanation for the earlier model mismatch: scanning dates alone within the tested pre-2020 reference does not make the mean common. It neither rules out slow ocean memory nor establishes a new physical process, causal ENSO effect or regime shift. We did not measure pressure, wind, heat flux, subsurface temperature, ecosystems or water supply.

A useful next test would cross the two coefficient fits with the two residual sets, then validate a longer-memory model in reserved multi-year blocks and other SST products. That would separate which part of the reference change controls the large full-fit tail fraction. Our saved code and statistics provide a small benchmark for that work.

## Reproduction and audit

Verify and extract the signed ZIP. From the extracted root, with the shared store mounted, run into new scratch outside the publication:

```bash
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --data-root /mnt/dell-data/shared_datasets --out /tmp/pdo_scan_repeat
OPENBLAS_NUM_THREADS=1 python files/audit.py --data-root /mnt/dell-data/shared_datasets --evidence /tmp/pdo_scan_repeat
```

Python 3.12, NumPy, pandas, SciPy and Matplotlib are required. Versions are in files/software.json. No dependency was installed or shared environment changed. Compare the generated CSV and JSON files with the saved files. A second full run matched all numerical outputs byte for byte. The audit uses a separate pandas parser, pivoted QR least squares, explicit monthly recursion and direct sliding windows. It checks 20 draws in each of eight cases, all saved tail counts, both fitted coefficient vectors and the observed minimum. Its largest recursion difference was 7.55e-15.

If the shared data are absent, `python files/retrieve.py /tmp/new_pdo_scan_inputs` attempts live retrieval into a new external directory and checks the exact hashes. Live URLs can change. If they change, do not treat a new snapshot as an exact repeat. The earlier signed mean-gap publication also preserves the exact snapshots as files/pdo.dat and files/nino.txt. Use `sci read PRIOR.zip --file files/pdo.dat --output /tmp/newroot/ncei-ersstv5-pdo-index-20261108/ersst.v5.pdo.dat` and the equivalent command for files/nino.txt at the second shared relative path. Create those external parent directories first. The cited SCI identifier locates that prior bundle in the campaign. These source files stay external to this publication.

## Campaign identity

Job: sci-1107-dell-earth-and-ocean-sciences-7bccaeaaee92. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies the campaign machine; it is not a personal authorship claim. This finite investigation used no child agents or background services.
