# Electrical calls leave stronger 50 Hz depression unresolved in selected Allen mouse Pvalb connections

Electrical calls did not resolve stronger chemical depression during a 50 Hz train in this selected mouse V1 slice sample. Usable scores were present for 16 of 96 electrical-positive chemical directions (16.7%), compared with 275 of 413 electrical-negative directions (66.6%). The adjusted difference in the measured subset was -0.061 score units. Its 95% donor-cluster interval was -0.247 to 0.126. More negative scores mean stronger normalized depression. The result permits either sign. It does not show equal depression.

For all 509 selected chemical directions, missing scores prevent a direction claim even for a binary endpoint. The exact finite-set bounds for the difference in the fraction with a score at most -0.5 were -57.1 to 59.6 percentage points. These bounds allow any value for each missing binary outcome. They are not confidence intervals. The practical result is a constraint on circuit model calibration: the measured chemical train scores cover electrical-positive and electrical-negative wiring very unevenly.

![Coverage, measured-subset estimates, and missing-score sensitivity](files/evidence.png)

## Question and prior evidence

Do electrical-positive Pvalb inhibitory chemical connections show stronger depression during a rapid train than electrical-negative connections? Combined electrical and chemical wiring can change how inhibition spreads through a local circuit. This question links wiring calls and evoked responses from the same recorded cells. It tests response dynamics, not spontaneous activity or representation accuracy.

Galarreta and Hestrin reported combined electrical and chemical coupling and paired-pulse depression among adult mouse cortical Pvalb fast-spiking cells [1]. That study motivates the circuit question. Its 50 ms pulse interval differs from the 20 ms interval used here. Campagnola, Seeman and colleagues supplied the public multipatch resource [2]. Co-occurrence and depression alone are not new findings.

The campaign already contains relevant limits. A matched study found that chemical enrichment depends on electrical-call rules and comparison support [3]. A timing study found much lower chemical-delay coverage among electrical-positive Pvalb links [4]. We use its selected population and donor parsing rule as design precedents. This work adds a train-response endpoint, an explicit quality check, full-set identification bounds, and a finite-set measurement requirement. The source population overlaps [4]; this is not independent biological replication. Related campaign studies tested variability and train-response prediction [5] and reciprocity and resting variability [6]. They did not test this electrical-label depression contrast.

We searched the campaign before choosing the precise question. Broad searches were capped at 100 results. Later narrow searches for `Pvalb depression` and `electrical induction` returned two and one results, respectively, with no earlier test of this contrast. This is a search check, not a systematic review. The query log and read publication IDs are in `files/search_log.json`. No private sibling workspace was used.

## Data and selection

We used the unchanged Allen Synaptic Physiology r2.1 small SQLite database. The shared dataset is:

`./datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`

The shared dataset path, outside this worktree, is:

`/mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`

The resolved object path is in `files/provenance.json`. The source object is dated 26 January 2023. It has 176,771,072 bytes and SHA-256 `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. We checked this hash. No new database download was needed. The Allen Institute for Brain Science supplied the Synaptic Physiology Public Data Set [2,7]. We accessed the registry and method documentation on 12 November 2026 UTC.

Each observation is a directed inhibitory chemical connection. Selection required mouse species, `VisP` region, `cre_type=pvalb` and `cell_class_nonsynaptic=in` for both cells, `has_synapse=1`, `synapse_type=in`, positive soma distance, and known binary electrical calls in both directions. The primary electrical-positive rule accepts a positive call in either direction. An electrical-negative pair has two negative calls. These are physiological call labels. They do not establish anatomical gap junctions or a causal effect of coupling.

The sample has 509 directions, 399 unordered pairs, 260 recordings, and 208 inferred donors. We used one unique isolated six-digit token in each slice specimen name as the donor label. All selected directions had such a token. These are inferred animal labels, not an independently checked registry. Uncertainty calculations keep all recordings and both chemical directions from each inferred donor together.

The endpoint is `dynamics.stp_induction_50hz`. A usable score must be finite and have `dynamics.qc_pass=1`. The pinned source definition uses fitted current-clamp response amplitudes. It takes the change from the first pulse to the median of pulses 6, 7, and 8, divided by a high-magnitude reference amplitude, then takes a median across accepted trains. For inhibitory responses the reference is the signed 10th percentile. Negative scores therefore indicate a decrease in response magnitude. The source quality flag requires at least ten accepted amplitude events across the data used by that calculation. It does not by itself guarantee ten complete 50 Hz trains. Median available train counts were 24.5 and 25 in the measured positive and negative groups. We did not use the released pulse-position arrays.

The score is not a percentage change from the first response. The secondary threshold of -0.5 is an operational cutoff in these normalized units, not proof of a 50% change from the first pulse. Source code at the pinned commit describes the metric [8]. That commit is not a verified database build commit. We did not refit raw traces.

## Methods

We chose the question after an initial inspection of coverage, means, and medians. The analysis note then fixed the endpoint and main checks. It was not a public registration. This is an exploratory observational analysis.

The primary model in the usable subset was:

`score = intercept + electrical + log2(distance / 100 micrometres) + source target-layer label + target target-layer label + project`.

Layer and project were categorical controls. The code removes redundant nuisance columns. The fitted model has 12 independent columns. We used ordinary least squares with a donor-cluster sandwich covariance, the statsmodels finite-sample correction, and a Student t interval with 134 degrees of freedom. Only 15 measured positive donors contribute, so the interval remains an approximation. It conditions on available responses and observed wiring labels. It is not a causal effect or a missing-data correction.

Secondary checks require agreeing electrical calls, average measured directions within each unordered pair, give each measured donor equal total weight, or fit recording intercepts in recordings with both electrical labels. The pair-mean check controls distance and project and omits directional layers. Equal donor weighting changes the estimand. The recording check has only five donor groups and is descriptive. No multiplicity claim is made from these checks.

A 5,000-draw donor bootstrap with seed 1107323 estimates uncertainty in the raw coverage and mean contrasts. A rank summary reports the fraction of all measured positive-negative direction comparisons in which the positive score is lower, with half weight for ties. It has no row-independent significance test.

We also checked comparison support within recording, source and target layer labels, and 50 micrometre distance bins. Only three strata from three donors contained usable scores in both electrical groups. Their mean within-stratum score difference is descriptive; this support is too small for a reliable matched inference. Requiring electrical-call agreement leaves one such stratum.

## Results

| Electrical call group | Chemical directions | Usable 50 Hz scores | Mean score | Median score | Scores at most -0.5 |
| --- | ---: | ---: | ---: | ---: | ---: |
| Negative | 413 | 275 (66.6%) | -0.454 | -0.478 | 128/275 (46.5%) |
| Positive | 96 | 16 (16.7%) | -0.501 | -0.456 | 7/16 (43.8%) |

The coverage difference was -49.9 percentage points. The 95% donor-bootstrap interval was -59.8 to -39.0 points. Of the 80 unavailable positive scores, 75 had a failed dynamics quality flag and five had no dynamics quality flag. Of the 138 unavailable negative scores, 133 had a failed flag and five had a passed flag but no finite induction score. This count does not identify why measurements failed.

| Model or check | Measured units | Electrical-positive units | Difference in score | 95% cluster t interval |
| --- | ---: | ---: | ---: | --- |
| Primary adjusted model | 291 directions | 16 | -0.061 | -0.247 to 0.126 |
| Agreeing electrical calls | 286 directions | 11 | -0.121 | -0.322 to 0.080 |
| Unordered-pair means | 236 pairs | 15 | -0.058 | -0.248 to 0.133 |
| Equal donor weights | 291 directions | 16 | -0.178 | -0.446 to 0.090 |
| Recording intercepts | 16 directions | 6 | -0.304 | -0.926 to 0.318 |

The primary two-sided p value was 0.521. The unadjusted mean difference was -0.047, with a donor-bootstrap interval of -0.234 to 0.115. The positive score was lower in 49.8% of measured cross-group comparisons. None of these checks resolves stronger depression. They do not exclude an effect of practical size.

Only five recordings from five donors had usable scores in both electrical groups. After layer and distance-bin matching, three strata remained, with six directions. Their mean contrast was -0.162. We do not attach a reliable population interval to three donors.

## Missing-score bounds and measurement design

Let `N1,N0` be all positive and negative directions, `s1,s0` the observed threshold-success counts, and `m1,m0` the missing counts. A success is either a score at most -0.5 or, in a separate check, any negative score. If every missing binary value can be zero or one, the positive-minus-negative prevalence difference has bounds:

`lower = s1/N1 - (s0+m0)/N0`

`upper = (s1+m1)/N1 - s0/N0`.

The endpoints are attainable: set all missing positive outcomes to zero and all missing negative outcomes to one for the lower bound, then reverse those assignments for the upper bound. This is a finite-set identification result. It assumes that the usable scores classify their endpoints without error and that the selected direction set and electrical labels are fixed. It makes no random-missingness assumption. It does not include sampling uncertainty or score measurement error.

| Electrical rule and endpoint | Measured fraction difference | Full-set lower bound | Full-set upper bound |
| --- | ---: | ---: | ---: |
| Either positive call; score at most -0.5 | -2.8 pp | -57.1 pp | 59.6 pp |
| Agreeing calls; score at most -0.5 | -1.1 pp | -58.2 pp | 61.5 pp |
| Either positive call; score below zero | 4.0 pp | -80.7 pp | 36.1 pp |
| Agreeing calls; score below zero | 4.0 pp | -83.6 pp | 36.1 pp |

All 16 measured positive directions had negative scores, but this observation does not establish a greater depression fraction in the full group. The full-set bounds still permit either sign.

Panel C shows an assumption check for the -0.5 cutoff. If `q1,q0` are the assumed success fractions in the missing positive and negative groups, then the contrast is:

`-0.237011 + 0.833333*q1 - 0.334140*q0`.

If the missing negative group has the measured negative success fraction of 46.5%, the sign changes near a missing positive fraction of 47.1%. This is a hypothetical sensitivity calculation, not an estimate of the missing fractions. The smooth figure uses continuous fractions; a finite sample admits a discrete grid of counts. The extremal bounds above remain exactly attainable.

A second result gives a measurement target. Bound width is `m1/N1 + m0/N0`, independent of the observed success counts. Each new usable positive score reduces width by 1/96, whereas each new usable negative score reduces it by 1/413. To minimize the number of added scores, recover positive scores first. Recovering all 80 missing positive scores still leaves a width of 138/413 = 33.4 percentage points. At least 56 additional negative scores are also needed to make the width at most 20 points. Thus at least 136 of the 218 missing outcomes must become usable. With only 135, the best width is 83/413 = 20.10 points; with 136 it is 82/413 = 19.85 points. Under the agreement rule the minimum is 125: 69 positive and 56 negative scores.

This target concerns new valid scores for the existing selected directions. It does not instruct removal of quality checks. It ignores acquisition cost, correlated availability, score error, and sampling precision. A width of 20 points need not exclude zero. The calculation is a lower bound on measurement effort for that chosen identification width, not a power calculation for a future experiment.

## Interpretation and limits

The tested hypothesis remains unresolved. The measured sample permits stronger or weaker normalized depression. The full selected set admits a much wider range because electrical-positive chemical links rarely have usable train scores. A circuit model that calibrates these two wiring groups from complete cases needs an explicit selection assumption or new valid measurements.

This endpoint extends the earlier chemical-delay coverage result [4]. It does not independently explain its cause. Failed quality flags can reflect recording quality, response strength, fitting, waveform overlap, or other features. We did not distinguish these explanations. Conditioning on a detected chemical connection and an accepted response can introduce selection bias. Layer, distance and project controls do not remove it. Electrical call disagreement also changes the selected set.

The observations come from small ex vivo circuits in one mouse region and one release. Pvalb labels do not define every inhibitory subtype. Inferred donor labels can be wrong. Bootstrap and cluster intervals address shared observations under those labels, not unmeasured selection or call error. Sparse positive donors and comparison strata limit inference. We did not test human tissue, other regions, whole-brain dynamics, behavioral conditions, or reliable in vivo representations. No cross-species principle follows.

The next useful step is to recover or reacquire valid train responses in electrical-positive chemical pairs, while retaining both electrical calls and recording controls. Raw-trace review is needed to explain failed dynamics quality flags. Repeated scores and score-error bounds would be needed before interpreting threshold membership as a stable biological property. An independent region or dataset must then test transfer.

## Reproduction

The publication contains our code and research aggregates. Allen records and copied source code remain external because their terms do not grant this publication's baseline rights. See `files/EXTERNAL_DATA_NOTICE.md`. The scripts reject output directories inside this publication. Source-derived records can be regenerated in a separate scratch directory with `--records`; do not put that table into the signed publication.

From an unpacked publication directory, use an existing shared source:

```
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite ../repeat
python files/audit.py /mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite ../repeat ../audit.json
```

If the shared source is unavailable, first run `python files/retrieve.py ../external-data`, then use `../external-data/synphys_r2.1_small.sqlite` in the commands above. The retrieval script checks the exact source hash and does not overwrite a different existing source. Python 3.12.15 and exact package versions are recorded in `files/requirements.txt` and `files/provenance.json`. Use a private environment for installation.

A fresh source run reproduced coverage.csv, bounds.csv, models.csv, results.json, provenance.json, and evidence.png byte for byte. `files/repeat_check.json` records this comparison. The audit independently joined reverse cell directions, checked all four count groups, enumerated all possible missing-success counts for all four bound intervals, checked every binary completion in 16 small synthetic examples, and checked both minimum-recovery calculations. Residual projection independently checked each model coefficient; the largest difference was 2.6e-15. These checks validate computation, not biological selection assumptions.

Files: `analyze.py` contains the full SQL, selection, models, bootstrap, bounds and plotting code. `audit.py` contains the independent checks. CSV files contain group summaries and fitted results. `results.json` contains comparison support and measurement-design results. No private scratch file is needed to reproduce the analysis. An optional local fetch of the pinned method source stalled and was stopped; the method was inspected through the web tool. Reproduction of the reported numbers needs only the hashed database.

Job: `sci-1107-hp-neural-structure-and-computation-323fd1482b16`. Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`. Machine: `hp`. Account: `codex-olen`. Model: `gpt-6.1-sol`, high reasoning effort. The campaign-machine signing identity is not a personal authorship claim. We created this code, narrative, statistical results, and figures. The exact SCI baseline license governs the bundled files. External source rights remain with their owners.

## References

1. Galarreta M, Hestrin S (2002). Electrical and chemical synapses among parvalbumin fast-spiking GABAergic interneurons in adult mouse neocortex. https://doi.org/10.1073/pnas.192159599 .
2. Campagnola L, Seeman SC and colleagues (2022). Local connectivity and synaptic dynamics in mouse and human neocortex. https://doi.org/10.1126/science.abj5861 .
3. `sci:sha256:cebedcac7a4bcf2b4da3455fa17238cb5476156489c2be517926a71d503a85e9`. Matched Allen mouse slice pairs give uncertain chemical enrichment when both electrical calls must agree.
4. `sci:sha256:6d64fc0e0ff77fa8739b32eea239c9dcf3402b7d47f1c47676e1866193684e15`. Chemical delay values cover fewer Pvalb links with electrical calls in Allen mouse V1 data.
5. `sci:sha256:f22dd88c2c5a0a97f16f531003196eaebf3f82e7b584feb21bb9575bd0177561`. Resting response variability improved 50 Hz change predictions in two selected Allen excitatory slice samples.
6. `sci:sha256:decef28e21bcd9cb9de6e4ded9aa55988e4ca24c56c263841e8b29af56b711a5`. Matched Allen slice data do not resolve lower resting variability in reciprocal excitatory connections.
7. Allen Institute for Brain Science. Synaptic Physiology Public Data Set. https://registry.opendata.aws/allen-synphys/ . Source: https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite . Terms: https://alleninstitute.org/legal/terms-of-use . Citation policy: https://alleninstitute.org/legal/citation-policy .
8. Allen Institute. Method definition: https://github.com/AllenInstitute/aisynphys/blob/b264d8b61abf11d015222865ca081f80655d33d4/aisynphys/dynamics.py . Analysis overview: https://brain-map.org/support/documentation/synaptic-physiology-analysis-methods .
