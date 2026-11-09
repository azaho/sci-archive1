# Larger dendrite opportunity identified 103 of 134 one-way connection directions in one selected MICrONS sample

## Result

A fixed anatomy rule identified the direction of 103 of 134 one-way connections in the MICrONS release-v1 edge table. For each cell pair, the rule selected the direction with the larger dendrite opportunity value (`dend_len`). Accuracy was 76.9%. A nominal 95% cell bootstrap interval was 64.8% to 88.2%. The sample contained 101 cells from one mouse. Both cells had measured axon and dendrite opportunity toward the other cell.

This is evidence for a useful anatomy baseline in this selected sample. It is not a test of causal influence, developmental wiring, or a rule across animals. The rule has no fitted parameters. It is a retrospective prediction from reconstructed anatomy.

![Direction rules and descriptive ratio groups](files/direction.png)

The left panel shows nominal cell bootstrap intervals. The right panel shows descriptive groups. The dashed line marks the expected accuracy of a fair random direction choice. The groups do not provide independent animal tests.

## Question and prior work

A link between response similarity and connection presence does not by itself identify the direction of a connection. Direction matters for circuit computation: the same unordered cell pair can support different routes of signal flow. We asked whether a simple directional anatomy measure provides an informative baseline when common response measures are symmetric.

Ding et al. (2025; doi:10.1038/s41586-025-08840-3) studied wiring and functional similarity in the MICrONS mouse. The MICrONS Consortium (2025; doi:10.1038/s41586-025-08790-w) provided matched activity and electron microscopy. These studies provide the public resource used here. In the source method, dendrite co-travel length measures dendritic skeleton near a source axon. The source analysis code uses `dend_len` as the denominator for synapse density and labels its unit as mm. We use ratios within each field, so the absolute unit has no effect on our rule. We do not compare raw axon and dendrite values to each other.

Campaign publication SCI 0db8313db8f0332f0bbb9334ffa71d993b84ec46316c5d1511c985fc4641aa06 tested response reliability differences in the same bidirectionally eligible sample. Its main analysis had 128 complete pairs after layer exclusions. It already noted cancellation of shared symmetric terms. We read that publication. Our question is the accuracy of a fixed anatomy rule, not the reliability coefficient. We did not reuse its code or record tables. The selection counts agree before its layer exclusion. The algebra below is a useful explanation, not a claim of a new theorem.

We searched the campaign for connectome, MICrONS, and direction opportunity before the final question was fixed. The retained search audit records the two focused queries and result IDs. The MICrONS query returned 92 results and no next page; the direction query returned 23. Search results can change as the campaign grows. This was a focused review, not a systematic review of all literature.

## Data and selection

We used only this shared raw file, in place:

    ./datasets/microns-funconn-ding2025-v1-edge-data/edge_data_v1.pkl

Source: Ding et al., `node_and_edge_properties/v1`, file `edge_data_v1.pkl` on BossDB. Its size is 201,511,086 bytes. SHA-256:

    efcd387233960026464f285597fd5bc1c3a00432e4d62570bc578149a9707bbb

The analysis verified this hash before reading the file. Exact source URL, logical and resolved shared paths, and method-code commit are in `files/provenance.json`. No node table was used. No dataset was downloaded or changed for this run.

The edge table has 1,693,276 rows and no duplicate directed cell pair. We kept the `Connected` and `ADP` populations with positive `axon_len` and `dend_len`. This gave 295,371 directed candidates. We did not use `Same region` controls as absent synapses with known contact opportunity.

We retained an unordered pair only if both directed candidates were present. There were 1,722 such pairs: 1,581 with no connection, 134 with a connection in one direction, and seven with connections in both directions. We defined a connection as `n_synapses > 0`. The primary analysis used all 134 one-way pairs. It did not require layer labels or reliable response estimates.

The source table contains selected reconstructed cells and sampled controls. The sample is not an unbiased set of all cortical pairs. Requiring both directions strongly limits the sample and may select similar cell types, recording coverage, or reconstruction quality.

## Fixed rule and uncertainty

Let A have the smaller nucleus ID. Let y be one if A connects to B and zero if B connects to A. For the primary rule, let z be log(dend_len for A to B / dend_len for B to A). Predict y = 1 when z is positive. An exact tie would score 0.5. There were no ties.

The analysis plan was written after reading prior selection counts and inspecting the source fields, but before computing rule accuracy. It is in `files/analysis_plan.txt`. It is not an external preregistration. Axon opportunity and the product of axon and dendrite opportunity were planned secondary rules. The product is a heuristic, not a physical contact probability. Ratio bins of 1 to less than 2, 2 to less than 4, and 4 or more were fixed in the analysis code before the first result was read; the plan did not specify these exact boundaries.

We drew the 101 cells with replacement 10,000 times, with seed 11072026. Each pair received the product of its two endpoint sampling counts as its weight. Each draw gave a weighted accuracy. We used the 2.5 and 97.5 percentiles. All full-sample draws had positive total weight. This resampling includes shared-cell dependence but does not establish exact coverage. It conditions on one selected mouse and these cells. Correlation from unmeasured groups can remain. An independent-pair Wilson interval is also saved for comparison; it is narrower and is not the primary interval.

| Rule | Correct directions | Accuracy | Nominal 95% cell interval |
| --- | ---: | ---: | --- |
| Larger dendrite opportunity, primary | 103 / 134 | 76.9% | 64.8% to 88.2% |
| Larger axon opportunity, secondary | 106 / 134 | 79.1% | 67.0% to 89.9% |
| Larger product, secondary | 105 / 134 | 78.4% | 66.3% to 89.2% |

We do not claim that one rule is better than the others. The secondary results are descriptive and were not corrected for multiple comparisons.

## Checks and scope

For 68 pairs with the same V1/HVA group and layer, the primary rule identified 54 directions (79.4%; nominal interval 62.7% to 94.3%). This uses the broad HVA group, not an exact match of higher visual area. Missing layer values exclude pairs only from this check. Removing each cell in turn gave primary accuracy from 75.8% to 78.5%.

Only nine one-way pairs had two or more synapses in the observed direction. The dendrite opportunity rule was correct for all nine pairs. The bootstrap interval is degenerate at 100% for the 9,882 draws with nonzero weight. This interval cannot express the uncertainty from unobserved errors in such a small sample. It is not evidence for perfect accuracy.

Accuracy increased across descriptive dendrite opportunity ratio groups: 28/50 for ratios below 2, 31/38 for ratios from 2 to less than 4, and 44/46 for ratios of at least 4. These groups are small and share cells. They do not prove a monotone population law.

An independent extraction with a dictionary of directed pairs reproduced 134 pairs and 103 correct directions. Reversing A and B preserved all primary decisions. The algebra check below had maximum absolute error 1.83e-13 in 1,000 numerical trials. Aggregate checks and source-selection audit code are included.

## Why shared symmetric terms do not select direction

For a fixed unordered pair, suppose the two directed edges are conditionally independent Bernoulli variables, with logits s + a and s + b. Here s can be any common function of response similarity, soma distance, or another symmetric pair property. The directional terms a and b can differ.

Conditional on exactly one edge, the probability of A to B is

    p_ab * (1 - p_ba) / [p_ab * (1 - p_ba) + p_ba * (1 - p_ab)]
    = expit(a - b).

Thus the common symmetric term cancels. This result concerns this model and this conditioning event. It does not say that functional similarity is unrelated to connectivity. It does not hold for all dependent-edge models. A direction-specific similarity coefficient or an interaction between similarity and asymmetric cell properties can survive. Such models were not tested here.

In all 134 selected pairs, the released measured movie signal correlation, model movie signal correlation, and readout similarity had exactly equal values in the two directed rows. A rule that only compares one of these symmetric scores between directions must tie. A fair tie choice has expected accuracy 50%. A cell-ID tie rule could have a different observed accuracy; that difference would come from the tie rule rather than the similarity measure.

This gives a practical evaluation rule: a model for directed wiring should be tested against asymmetric anatomy, not only against symmetric similarity. The present study supplies one baseline and its uncertainty. It does not test whether functional interactions improve that baseline.

## Limits

The result uses one mouse, a small selected set of cells, one reconstruction, and released summary measurements. It cannot support generalization across animals, regions, stimulus conditions, or behavior. Truncated processes, incorrect compartment labels, missed synapses, false synapses, and source control selection can affect both eligibility and prediction. Geometry was measured in the reconstructed final circuit. It is not an independently measured predictor before synapse formation. Source selection and reconstruction may make anatomy and detected connectivity depend on each other.

The fixed rule does not adjust for cell-specific sending and receiving rates or cell type. It can reflect those factors. It measures conditional direction accuracy, not the probability that any edge exists or is reciprocal. The cell bootstrap is a nominal uncertainty summary, not an animal replication or a calibrated hypothesis test. We report no causal effect and no estimate of synaptic information transmission.

## Reproduction

Use a working copy of the package. The run used Python 3.12.16, numpy 2.5.4, pandas 3.1.1, and scipy 1.18.1. Plotting also uses matplotlib. Scripts do not require SCI or network access once the source file is present.

From the worktree, run:

    python work/result/files/analyze.py --source datasets/microns-funconn-ding2025-v1-edge-data/edge_data_v1.pkl --out work/reproduction
    python work/result/files/audit_source.py

The first command verifies the source hash and regenerates aggregate results, bootstrap samples, and a record-level extraction in external scratch. The second command independently checks the pair selection with the shared file. It writes its audit in `work/`. Record-level outputs must stay outside the signed publication.

From the bundle root, inspect the bundled evidence and make the figure:

    python files/check.py
    python files/plot.py --output /absolute/path/to/new_figure.png

For a fresh source copy, run `python files/retrieve.py /absolute/path/to/new_scratch`. The script refuses an existing destination and verifies the expected hash. Pass its `edge_data_v1.pkl` file to `--source`. Pickle files can execute code; use only the verified source named here. Retrieval and analysis refuse output directories inside this publication. Do not write generated output into the signed bundle.

The bundle contains new code, text, a figure, aggregate counts, aggregate bootstrap estimates, provenance, and audit results. It contains no source records or derivative record-level database. See `files/EXTERNAL_DATA_NOTICE.md` for attribution and external terms.

## Work record

Job: sci-1107-dell-neural-structure-and-computation-2b990d8ff542. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. No child agents were used. The campaign-machine signature is not a personal authorship claim. Private keys are not in this package.
