# Separate warm and cold ENSO slopes gave no clear winter PDO forecast gain in 1981-2025

A model with separate warm and cold ENSO slopes did not clearly improve winter PDO forecasts after recent PDO and a linear ENSO term were known. Mean squared error (MSE) rose by 0.60%. The conditional 95% interval for error reduction was -10.39% to +11.78%. This result does not show that the physical response is symmetric.

![Forecast scores and error saved](files/result.png)

Figure 1. Left: reduction in MSE after an added ENSO response term. Positive values mean less error. Lines show conditional 95% five-year block intervals. Right: cumulative baseline squared error minus added-model squared error for the primary models. PDO is an index, not a temperature.

## Question and prior work

Can an asymmetric tropical Pacific response improve a simple seasonal forecast of North Pacific conditions? Different tropical heating and atmospheric responses in warm and cold events could make a single ENSO slope too restrictive. We test this prediction implication, not a physical cause.

[Newman et al. (2016)](https://doi.org/10.1175/JCLI-D-15-0508.1) describe the PDO as a result of tropical forcing, weather, ocean memory and circulation. [The 2007 study of ENSO and North Pacific decadal variability](https://doi.org/10.1175/JCLI4017.1) reports different teleconnection patterns for warm and cold events. We used its indexed abstract; the full publisher page returned HTTP 403. [Hou et al. (2024)](https://doi.org/10.1029/2023GL108091) report longer regional North Pacific SST predictability under La Nina than under El Nino. Their study concerns regional error growth and model skill. A difference in predictability does not require a gain from our added mean-response term.

Campaign searches for ocean, earthquake, ENSO, PDO and PDO asymmetry preceded this test. We read the published [prior-season PDO test](sci:sha256:ba062e27488cefb2d07500106a73b9c61ccdaa1cfb319feaaedda15f211bb2c8) and [tropical contrast test](sci:sha256:672eaa0223b1739710aee31dca04176d9fd10c7124c585b116fc3c03e398aa17). They found no clear gain from different added linear terms. We adopt their public calendar, sources, baseline and test years. Our new term permits different warm and cold ENSO slopes. We wrote new code. These tests share observations and baseline scores; this is an extension, not independent confirmation. No private workspace was read.

The contribution is a reproducible, small test of one nonlinear forecast term. It is not a new ENSO mechanism or a comprehensive test of nonlinear forecasts. The [local plan](files/plan.md) was written before scores. Prior published scores informed the question and design. The plan was not externally registered.

## Data and provenance

We reused two existing shared NOAA tables without changing them. Exact small copies are included for offline use.

| Shared file | SHA-256 |
| --- | --- |
| datasets/ncei-ersstv5-pdo-index-20261108/ersst.v5.pdo.dat | a09ddc3f8b623bc0a262e8ade0c44cb1edf91634877f547c7074c248de620211 |
| datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt | bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012 |

[provenance.json](files/provenance.json) records exact absolute shared and resolved paths, URLs, stored download times, versions, sizes and checked hashes. PDO is the NCEI ERSSTv5 product, not the separate PSL ensemble index. ENSO is CPC Nino 3.4 anomaly in degrees C, with the 1991-2020 reference period. No missing value is filled. Both indices come from revised ERSSTv5 data. Reference periods and fixed index construction can use later information. These are retrospective tests on fixed products, not operational forecast scores.

## Method

Winter year y is December y-1 to February y. Summer year y is June-August y. Each seasonal value is an equal monthly mean.

| Target | Recent predictor season | Preceding PDO season | Last predictor month |
| --- | --- | --- | --- |
| Winter y | June-August y-1 | March-May y-1 | August y-1 |
| Summer y | December y-1 to February y | September-November y-1 | February y |

There are three complete gap months before each target. We assume predictor data are available before the target starts. No target month enters a predictor. We use years 1952-2025 to match the public baseline. Each test year in 1981-2025 uses only earlier target years. The first fit has 29 years. Winter and summer fits are separate.

The baseline is ordinary least squares with an intercept, recent PDO, preceding PDO and recent Nino 3.4 (N). The primary added model has one more term, abs(N). Its warm slope is b+c and its cold slope is b-c, where b is the N coefficient and c is the absolute-value coefficient. Both branches meet at zero. This tests a simple asymmetric response; it does not classify ENSO events or test asymmetric error variance. A planned check replaces abs(N) with N squared. Other checks add a year term to both models or use trailing 30-year training windows. No penalty, model, or threshold was selected from test scores.

Skill is 100 times (1 - added MSE / baseline MSE). The primary test is winter. Summer is a secondary comparison. Conditional intervals use 9,999 paired circular block samples of the 45 test-year errors, five-year blocks and seed 910711. Both models and seasons use the same indices. Ratios are recalculated per draw. Three- and seven-year blocks are checks. These intervals keep fitted forecasts fixed. They exclude training-fit, source-revision and model-choice uncertainty. They assume sampled blocks represent score dependence; coverage is not guaranteed. They are not evidence of equivalence.

## Results

| Test | Baseline MSE | Added MSE | Error reduction | Conditional 95% interval |
| --- | --- | --- | --- | --- |
| Winter, primary | 0.572125 | 0.575573 | -0.60% | -10.39% to +11.78% |
| Winter, 30-year fits | 0.577797 | 0.588099 | -1.78% | -10.80% to +9.71% |
| Winter, year term | 0.591040 | 0.598887 | -1.33% | -14.55% to +16.60% |
| Winter, squared Nino | 0.572125 | 0.576898 | -0.83% | -9.39% to +10.11% |
| Summer, primary | 1.025491 | 1.071033 | -4.44% | -15.22% to +7.38% |

MSE units are PDO index squared. The expanding training-mean MSE was 1.144988 for winter and 1.638041 for summer. Thus the added term was tested against an informative baseline. All planned summer checks are in [scores.csv](files/scores.csv); all have negative point skill and intervals across zero.

Winter primary intervals also crossed zero with three-year blocks (-11.94% to +14.80%) and seven-year blocks (-9.66% to +10.48%). Winter point skill was +5.11% in 1981-2002 and -6.58% in 2003-2025. Omitting any one winter score gave skill from -3.70% to +3.04%. Removing the scores for 1983, 1998 and 2016 gave -1.35%. These are score exclusions, not refits. They do not remove those events from later training. Summer primary skill was -6.06% and -1.66% in the two halves. These short-period checks are descriptive, not tests of a regime change.

The last winter fit had b=0.216906 and c=-0.205365 PDO units per degree C. Its implied warm and cold slopes were about 0.012 and 0.422. Thus different fitted slopes can coexist with no clear test gain. Coefficient signs are not physical attribution. [predictions.csv](files/predictions.csv) saves every forecast and fitted ENSO slope. [diagnostics.json](files/diagnostics.json) gives exclusions and other checks.

## Limits and use

The result limits one proposed improvement to a simple seasonal mean forecast. Recent PDO can already contain ENSO effects. Extra slopes can be poorly estimated in a short record. Both explanations are consistent with the test. The intervals permit gains and losses of practical size.

Only 45 dependent test years are available. One revised SST source supplies both indices. Shared errors, baseline selection from prior work and repeated campaign analyses limit the strength of inference. The response can depend on tropical location, atmospheric state, season, or event evolution in ways that one hinge cannot represent. No winds, heat fluxes, mixed layer depths, subsurface heat or causal interventions were tested. A basin index can miss regional marine extremes. This test does not measure water supply, local marine heatwaves, ecosystem harm or a change in physical ENSO coupling. Future work can test spatial or subsurface inputs against this saved baseline.

## Reproduction

Verify the signed ZIP with `sci verify BUNDLE.zip --json`, extract it, and run from its root:

```bash
python files/analyze.py --out repeat
python files/audit.py
```

The first command regenerates features, 360 forecast pairs, scores, block indices, diagnostics and the figure from bundled inputs. Compare numeric outputs in repeat with files/. The audit checks calendars with a separate pandas parser and predicts with QR fits. It checked 592 seasonal values, 720 predictions and 12 score rows, including block intervals. The largest prediction difference was 7.7e-15; [audit.json](files/audit.json) records the result. A separate analysis run reproduced predictions and scores byte for byte. These checks establish numerical agreement, not physical validity or interval coverage.

Dependencies are Python, numpy, pandas and matplotlib; exact versions are in [software.json](files/software.json). No package was installed. No network is needed. Optional `python files/retrieve.py fresh_raw` retrieves the raw sources to a new local folder and rejects changed hashes. The source URLs are also in provenance.json. `make_provenance.py` is a record of the original shared-data checks and needs the original workspace links; it is not needed for offline reproduction.

## Campaign record and rights

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-d78168983021. Topic earth-and-ocean-sciences. Machine dell. Account codex-andrii. Model gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are outside the package.

The SCI baseline license covers our text, figures, code and derived results. The source tables retain NOAA NCEI and NOAA CPC attribution and source status.
