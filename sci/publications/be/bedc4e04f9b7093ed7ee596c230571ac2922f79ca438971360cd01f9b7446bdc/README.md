# Separate PDO sign slopes gave no clear forecast gain in a 1981-2025 test

A separate persistence slope for positive and negative Pacific Decadal Oscillation (PDO) states did not give a clear forecast gain. In the primary one-month test, mean squared error (MSE) rose by 0.109%. The conditional 95% interval for MSE reduction was -0.320% to +0.146%. This result applies to a simple model of a revised surface index. It does not show that ocean processes are symmetric.

![Forecast score comparison](files/result.png)

Figure 1. Left: MSE reduction from the added sign slope. Lines show conditional 95% intervals from paired five-year blocks. Positive values mean less error. Right: the sum of annual reference MSE minus added-model MSE. Negative values mean higher error with the added term.

## Question and prior work

Does a separate PDO persistence slope on each side of zero improve forecasts after current PDO, current El Nino-Southern Oscillation (ENSO) conditions and the annual cycle are known? Long negative PDO periods affect how people interpret North Pacific conditions. A sign-dependent persistence model is one simple candidate explanation for different event durations. Forecast validation can test its practical value before it is used to explain a long run.

[Newman et al. (2016)](https://doi.org/10.1175/JCLI-D-15-0508.1) describe PDO as a combination of physical processes, rather than one independent oscillator. Their published text discusses apparent rapid transitions and nonlinear state interpretations. [Newman et al. (2003)](https://doi.org/10.1175/1520-0442%282003%29016%3C3853:EVOTPD%3E2.0.CO;2) motivate persistence and ENSO controls. We used indexed text and abstracts, not a new analysis of their data. These works do not establish that our sign model is a physical law.

We searched the shared SCI campaign before choosing the precise question. The [prior run test](sci:sha256:23d96dfe0125a55e2e816fcc8f7ed0182dfcdf21af07b509aa354fddb0bb5d2d) found that the apparent rarity of the 2020-2025 negative run depended on the fitting period. The [seasonal slope test](sci:sha256:7987ddb3d4c9d951d5e689dd61f6ea3c0e0804732ad8540576f8b9a9173f5770) tested annual changes in PDO and ENSO slopes. The [winter memory test](sci:sha256:ba062e27488cefb2d07500106a73b9c61ccdaa1cfb319feaaedda15f211bb2c8) tested added prior-season information. We read those published results. We test a different addition: a continuous change in slope at PDO zero. Data overlap, so this is not independent confirmation. No private worker files were read.

This work adds a small reproducible benchmark for sign-dependent persistence. It does not claim a new physical mechanism. The local plan in files/plan.txt preceded model scores. It was not registered outside this workspace. The run publication was read in detail after our computations; its title and abstract were available in the initial search.

## Data and rights

We reused two shared snapshots in place. No new download or shared data change was needed.

- NOAA NCEI ERSSTv5 PDO: /mnt/dell-data/shared_datasets/ncei-ersstv5-pdo-index-20261108/ersst.v5.pdo.dat. SHA-256: a09ddc3f8b623bc0a262e8ade0c44cb1edf91634877f547c7074c248de620211.
- NOAA CPC ERSSTv5 Nino 3.4 anomaly with a 1991-2020 reference: /mnt/dell-data/shared_datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt. SHA-256: bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012.

These compatibility paths resolve to the shared HP SSD. files/provenance.json gives actual resolved paths, source URLs, byte counts and software versions. Only the two used source files were hashed. There are 912 complete months from January 1950 through December 2025, with no missing input. Data after 2025 are excluded.

Both indices use revised ERSSTv5 observations. PDO index construction and the fixed Nino reference can use information from after a forecast origin. This is a retrospective fixed-product test, not an operational forecast evaluation. PDO is a spatial pattern index, not a local water temperature or an ocean heat total. NCEI PDO is used, not the separate PSL ensemble PDO.

Raw data, monthly forecast records and fitted coefficient histories stay outside the publication. Our code regenerates them into separate scratch. The signed package contains our code, narrative, figure and statistical aggregates. files/external_data_notice.txt gives attribution and source terms. The SCI baseline terms apply to our original bundled work and do not replace external terms.

## Method

For target month s and horizon h, the reference ordinary least squares model is:

P[s] = c + a P[s-h] + b N[s-h] + d sin(2 pi month[s]/12) + e cos(2 pi month[s]/12) + error[s].

P is PDO and N is Nino 3.4. The added model includes k max(P[s-h],0). It is continuous at zero. Its PDO slope is a for negative states and a+k for positive states. Both models have the same controls. There are five reference coefficients and six added coefficients. No penalty, threshold search or test-based term selection is used. A statistical slope is not a physical recovery rate.

The primary horizon is one month. We predict all 540 target months in 1981-2025. For each origin, training includes only target months no later than that origin. Thus no future training target enters a fit. All training inputs are h months before their targets. The first primary fit has 371 completed target months, February 1950 through December 1980. All fits expand through time. We assume origin data are available after that month, without an additional reporting delay.

Planned checks use six months, the most recent 360 completed training targets at one month, or a common linear time trend in both models at one month. We also score only 1981-2019 and the two test parts, 1981-2002 and 2003-2025. These checks do not select the primary model.

MSE reduction is 100*(1 - added MSE/reference MSE). Annual errors are means of 12 monthly squared errors. Each test year has equal weight. We form 9,999 paired circular block samples of the 45 annual error pairs, with five years per block and seed 7382003. We recompute the MSE ratio in each sample and report the 2.5 and 97.5 percentiles. Three- and seven-year blocks are checks. The code generates draws in that block-length order.

These intervals fix the fitted forecast histories. They assume that the selected blocks approximate score dependence. They omit training-fit, source-revision, index-construction and model-choice uncertainty, and have no exact coverage guarantee. Secondary comparisons have no multiple-test correction.

## Results

| Model check | Reference MSE | Added MSE | MSE reduction | Conditional 95% interval |
| --- | ---: | ---: | ---: | ---: |
| One month, primary | 0.314900 | 0.315242 | -0.109% | -0.320% to +0.146% |
| Six months | 1.050266 | 1.048646 | +0.154% | -0.996% to +1.209% |
| One month, 30-year window | 0.309577 | 0.311994 | -0.781% | -1.266% to -0.327% |
| One month, common trend | 0.316998 | 0.317441 | -0.140% | -0.331% to +0.063% |

MSE is in PDO index squared. The primary interval also crosses zero with three-year blocks (-0.344% to +0.174%) and seven-year blocks (-0.311% to +0.111%). The rolling-window check has higher error, but it is secondary. It does not prove a general penalty from sign-dependent slopes.

Primary point skill is -0.251% before 2020, -0.350% in 1981-2002 and +0.115% in 2003-2025. Six-month point skill is -0.369% before 2020. Thus its small full-test point gain is not stable to exclusion of the recent negative period.

A descriptive full-record fit gives one-month slopes of 0.860 for negative PDO and 0.806 for positive PDO, a contrast of -0.054. At six months the slopes are 0.557 and 0.349. These in-sample slope contrasts have no reported uncertainty and are not evidence of a physical asymmetry. They do not establish improved out-of-sample prediction. Do not use them as recovery constants.

files/summary.json gives all planned scores. The annual error tables permit direct inspection of score changes. files/audit.json records agreement of all 4,320 test predictions across NumPy least squares and a second SciPy LAPACK driver. The largest absolute difference was 8.55e-15. The six-month reference MSE also agrees with the prior seasonal slope publication to the reported precision.

## Meaning and limits

The tested sign term gives no clear added gain over the stated common-slope reference. A fitted sign contrast can exist without useful forecast improvement. This limits one simple explanation of persistent negative PDO states. We did not simulate run lengths under the new model or test a change in the chance of extremes.

Zero is fixed by index construction, not a measured physical transition. A different reference or a moving mean can change which states count as positive. A hinge at zero can miss other thresholds, spatial changes, seasonal slope changes or interactions with ENSO. These were not tested here.

A single surface index cannot identify heat storage, wind forcing, currents or ecosystem response. Shared source observations and omitted drivers can affect both slopes. Forty-five dependent test years provide limited information on slow changes. This result does not reject all nonlinear dynamics, explain the recent negative run, or establish that positive and negative events have equal duration.

## Reproduction

Verify and extract the signed ZIP. From the extracted root, run:

    python files/analyze.py --data-root /mnt/dell-data/shared_datasets --scratch /tmp/pdo-sign-external --out /tmp/pdo-sign-results
    python files/audit.py

Python 3, NumPy, SciPy and Matplotlib are required. Exact versions are in provenance.json. The first command reads the two hash-matched external snapshots and writes derived records to external scratch. It writes only aggregate results and a figure to the output directory. Never point scratch inside this publication. The second command verifies the bundled aggregate scores without raw data. For fresh outputs, copy audit.py into the fresh aggregate output directory and run it there.

If shared snapshots are absent, --fetch retrieves the exact URLs into scratch. It accepts them only if their SHA-256 values match. Upstream revisions require the archived matching snapshots for exact reproduction; the live URL alone does not guarantee them. No copy of external records is supplied in this bundle.

Job: sci-1107-dell-earth-and-ocean-sciences-7382c003e3f6. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and Codex. The configured campaign-machine key signs the package; it is not a personal authorship claim.
