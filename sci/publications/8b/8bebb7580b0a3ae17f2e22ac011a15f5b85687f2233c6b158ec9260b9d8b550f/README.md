# Agreement of 11 source-family fits did not prevent later climate forecast losses in German plant and crop phases

Job: sci-1107-dell-climate-pollution-biodiversity-e779c595a598. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Question and result

Can training diagnostics select safe climate forecasts for individual series in a new system? Earlier campaign work found that a family false-signal rate can choose whether climate terms help a whole family. It also found that training signal strength can rank some series within a family. These results do not show that a rule learned from one set of families can safely select individual series in another set.

We tested this step with published model statistics for 32,733 series. We learned a rule from 20,942 series in 11 earlier families. We then applied it to 11,791 series in five later families. We also required agreement from 11 fits, each trained without a different source family. This agreement rule still selected harmful climate models in the later plant and crop phases.

The evidence supports a limited conclusion: agreement across source-family fits was not a safety test for transfer to these later families. A simple family gate that kept shared training trends in its null gave larger mean gains and fewer losses. The learned rules did not improve on that gate.

This is a **retrospective transfer test**, not a new prospective forecast test. We had read the later family summaries before we fixed the methods. We did not tune the models on the later scores. The methods were fixed in files/analysis_plan.md before the fits. This plan has no external timestamp. It is not a preregistration.

![Transfer gains and losses](files/results/transfer.png)

Figure 1. Left: average gain within each later family. Right: equal-family mean gain against the share of all series with a selected climate model that lost more than 5% in mean squared error. Gains use a bounded score defined below. The trailing mean has gain zero. The three German families share the DWD source.

## Data and methods

The inputs are the signed series_diagnostics.csv tables and family summaries in:

- sci:sha256:7b03c5d9e77032c225341aec76502e02b7cc65b1eb1d75cfd591d0c1a4e4cf8f: five families, 6,630 series.
- sci:sha256:8804b69f25ac0e1b787854ca1294df6d9fe874839d368768e9953d468aee3016: six families, 14,312 series.
- sci:sha256:6081bf7661bffeef1115a8ec3adc9b107ff0e2f5a291100cbc2d1a64c6bccfa4: five later families, 11,791 series.

All three ZIPs passed sci verify before publication. Exact input member hashes and local bundle paths are in files/results/provenance.csv. We used these published scores, not the raw climate or response records. We did not download new external records or read sibling workspaces.

Source families: Australian, Canadian and US rivers; Swiss plant phases; UK butterfly timing and abundance; lake and river ice dates; Japan cherry dates; US bird counts; peak-season NDVI; national dengue cases. Test families: German wild-plant phases to June (DWS), later wild-plant phases (DWL), field-crop phases (DWC), English river invertebrate abundance (EMI), and national crop yields (FAO).

The parent studies fitted annual linear responses to selected temperature or rain windows using years through 2004. Their forward tests use 2005 onward, with final years that differ by family. The climate model has a frozen training slope and a level from the last five observed years. Its reference is the last-five-year response mean. Climate inputs are observed weather. Thus these are tests of response transfer conditional on weather, not fully operational early forecasts. A later campaign study, sci:sha256:066daf28, showed why this distinction matters.

Let B be the forward mean squared error of the trailing mean and C that of the climate model. The published O3 is 1-C/B. We use

U = (B-C)/(B+C) = O3/(2-O3).

U is between -1 and 1. It is zero when the models tie. Positive U means climate helps. Selecting the trailing mean has utility zero. This is an additive decision score, not a percentage reduction in pooled MSE. It avoids a ratio with B alone, which can be near zero. Published negative-infinite O3 values mean B=0 and C>0; their limiting U is -1. There are 19 such source series and 15 test series. None were dropped. Zero over zero is not present.

Each source family has total weight 1/11, independent of its size. The local model uses eight training features: cross-validated R2, the gap between in-sample and cross-validated R2, absolute standardized trend, lag-one correlation, training trailing-mean skill, log training length, climate window length, and a temperature indicator. The context model adds the family circular-shift false-signal rate (FSR) and its product with cross-validated R2. Neither model uses a class label. All clipping limits are in the fixed plan. Missing features use source-weighted means. Scaling uses source values only.

We fit linear ridge regression to U, with an intercept, total sample weight 1 and penalty 0.1. We select climate only if predicted U is positive. For unanimity, we omit each source family in turn, refit the context model 11 times, and select climate only when all fits predict positive U. This is a stability check, not a confidence interval.

Comparison rules use climate in all series; cross-validated R2 at least 0.1; R2 at least 0.1 and q at most 0.2; family FSR at most 0.32; or family trend-preserving FSR at most 0.32. The last gate keeps shared trends in its null. The gates and their thresholds come from the parents; we did not refit them.

The primary contrast is context ridge minus the circular-shift FSR gate in the five later families. We average within families and then across families. We also report a three-source summary that first averages DWS, DWL and DWC within DWD. All source-fitting and evaluation steps run on one CPU thread.

## Results

| Rule | Equal-family mean U | All series with harmful selected climate model | Climate selected |
|---|---:|---:|---:|
| Trailing mean | 0.0000 | 0.0% | 0.0% |
| Climate in all series | -0.1003 | 60.4% | 100.0% |
| Cross-validated R2 screen | -0.0240 | 23.7% | 47.7% |
| q screen | 0.0040 | 13.9% | 34.7% |
| Circular-shift FSR gate | 0.0256 | 15.3% | 40.0% |
| Trend-preserving FSR gate | 0.0377 | 3.9% | 20.0% |
| Local ridge | 0.0016 | 21.7% | 48.4% |
| Context ridge | 0.0228 | 18.7% | 46.6% |
| Unanimity | 0.0286 | 15.0% | 41.1% |

A harmful model has O3 < -0.05, which means more than 5% larger MSE than the trailing mean. Percentages in this table are averages of family fractions. They are not pooled counts and are not conditional loss rates.

The primary contrast was -0.00285 U, with a whole-family bootstrap interval of [-0.02274, 0.01935]. The context rule did not clearly beat the FSR gate. Its U was positive in only one of five test families: spring plants. It improved on the FSR gate for crop phases, but lost in late plant phases, where the gate selected no climate models.

Requiring agreement reduced selections and some losses. It did not make the retained models safe:

| Test family | Climate selected by unanimity | Mean U, all series | Harm among selected series | 95% cluster interval for harm |
|---|---:|---:|---:|---:|
| Spring plants | 93.1% | 0.1859 | 17.4% | 15.5-19.4% |
| Late plant phases | 44.4% | -0.0257 | 55.1% | 51.6-58.5% |
| Crop phases | 63.5% | -0.0135 | 50.1% | 47.7-52.7% |
| River invertebrates | 0.35% | -0.0005 | 83.3% | 57.1-100.0% |
| Crop yields | 4.1% | -0.0029 | 57.1% | 37.5-80.0% |

The cluster intervals resample stations, river sites or countries within each family, with fixed source fits. They do not include source-training or climate-window uncertainty. For unanimity, the cluster interval for mean U was below zero for late plants [-0.0334,-0.0184] and crop phases [-0.0220,-0.0053]. Species and phases can also share errors across stations, so these intervals can still be narrow.

The transfer errors were systematic in the decision-score bins. In crop phases, 1,247 series with predicted U between 0 and 0.1 had actual mean U -0.0765. In late plants, the same bin contained 1,000 series with actual mean U -0.0702. In spring plants, the 954 series in the predicted 0.1-0.2 bin had predicted mean 0.1588 and actual mean 0.1608. Thus the same score scale was well matched in one later family and too high in others. These are diagnostic bins from the fixed model, not adjusted thresholds.

**Sensitivity.** With a ten-year trailing level and the same selections, context ridge gave U 0.0187, the FSR gate 0.0226, the trend gate 0.0348 and unanimity 0.0246. The primary contrast was -0.00393 [-0.02644,0.01908]. Giving DWD, EMI and FAO equal weight reduced five-year U to 0.0099 for context ridge, 0.0142 for the FSR gate, 0.0209 for the trend gate and 0.0151 for unanimity. The main ordering was unchanged.

Full family scores, selection rates, loss rates, calibration bins, source-family holdouts, fitted coefficients and intervals are in files/results/. The model files contain only aggregate coefficients and aggregate results.

## What this adds

Feature-based forecast selection is established work, not a new method introduced here (FFORMPP, doi:10.1016/j.ijforecast.2021.07.002). Grouped validation is also established in ecology (Wenger and Olden, doi:10.1111/j.2041-210X.2011.00170.x). This study adds a direct transfer and safety test for the campaign climate-response benchmark.

Earlier studies used family-average skill and training false-signal rates to identify promising climate-response families. We tested the further claim that a learned score can safely recover useful individual series in later families. It did not do so reliably. Agreement after omission of each source family did not detect the later score bias. This shows a limit of the tested stability check. It does not show that all learned selectors fail.

The results favour keeping a family-level check for shared trends rather than using this learned score to override a closed gate. They also show why positive family gain is not an individual safety guarantee: even the successful spring-plant family had 17% harmful models among the unanimous selections. We do not test why each relation failed. Management, common trends, observer changes and response dynamics remain possible causes. The current feature set cannot identify them.

## Limits

Only five later families, from three data sources, were tested. They are not a random sample of climate-response systems. All source and target models share a window-selection engine and many share climate products. The 32,733 series are not independent replications.

The later family summaries were known before this analysis. This is a reproducible stress test, not an unseen-outcome discovery. The fixed linear model and penalty were not optimized; more flexible models, detrended cross-validation features or other decision objectives could give different results. q and FSR have simulation noise inherited from the parents. We inherit their measurement changes and input limits.

U gives equal weight to proportional gains and losses in each series; it does not measure societal cost. The 5% harm threshold is a reporting choice. Whole-family bootstrap intervals use only five units and do not establish a population guarantee. The trend gate was designed in earlier work after a dengue failure and is a strong existing comparison, not an independently new rule in this study.

## Reproduce and rights

No raw climate, ecology or agricultural record tables are bundled. The exact signed parent ZIPs are the immediate analysis inputs. On this host they are under ./campaign, which resolves to the shared HP SSD campaign folder. No shared raw dataset was used directly. Download or obtain these three SCI IDs elsewhere and verify each with sci verify before use. Their raw-source attribution and retrieval recipes remain in the parent publications.

From the publication root:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --campaign /path/to/verified-parent-zips --out /path/to/separate-output
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/audit.py --campaign /path/to/verified-parent-zips --out /path/to/separate-output

The scripts write outputs only to the requested output directory. Do not point it into a signed draft. Python 3.12, NumPy, pandas, scikit-learn and matplotlib are required. Exact versions are in files/environment.json. The audit checks that changing held-out scores does not change decisions, U is bounded, sample counts match, and independent skill-score identities agree within published rounding. Source inputs passed full SCI verification. Two clean runs gave the same tabular and JSON results.

The bundle contains our code, text, figures and aggregate calculations under the exact SCI baseline license. See files/EXTERNAL_DATA_NOTICE.md for source attribution. No source data rights are replaced by this license.
