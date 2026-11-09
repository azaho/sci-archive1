# Mirror edges improved prediction between two adult worm maps after physical contact controls

## Question and result

Does a mirror connection add prediction of a chemical connection in a different animal after control for physical contact? In the tested adult direction, it did. The primary gain was 0.02745 nats per selected edge. The nominal 95 percent interval was 0.00630 to 0.04883. These are held-out prediction results under a specified model. They do not prove a biological cause.

The question matters because circuit models often treat weak connections as unreliable. A mirror connection could give a second measurement of a shared connection tendency. Physical contact could explain part of that marker. This test separates the measured contact variables from the mirror marker within a prediction model. It does not establish reliable representations, neural dynamics, or behavior.

## Prior work and scope

Witvliet et al. (2021, DOI: 10.1038/s41586-021-03778-8) reconstructed eight brains across development. They reported stable, changing, and variable connections, and related physical contact to chemical wiring. The prior campaign publication cited in sci.json found a mirror-edge prediction gain in two adult maps after count and cell controls. Its report identified physical contact as an omitted control. We address that gap with flexible contact terms and an L1 age check. We wrote new code and did not copy its derived tables. We do not claim that bilateral symmetry or wiring variability is a new discovery.

The analysis design in files/design.txt was recorded before inspection of score results. There was no model or penalty search. The tests after the adult source-family test are secondary checks, not independent confirmation.

## Data and selection

We reused the external shared datasets through ./datasets. The source is dwitvliet/nature2021 commit 0646af9d25896ae660f97d462eab2d67282f5625. files/provenance.json lists the exact resolved shared paths, source URLs, byte sizes, and SHA-256 hashes for all nine inputs: four primary chemical synapse JSON files, three physical contact CSV files, and the release neuron and dataset metadata code. The code checks each input hash. No download was needed for this analysis.

Maps 7 and 8 are different adult animals at the reported 50-hour time point. Only map 8 has a physical contact matrix. Thus the adult test uses index map 8 to predict labels in map 7. Maps 1 and 2 are different L1 animals at 0 and 5 hours. L1 results mix animal and age differences. These four maps are not repeated observations of one animal.

Each directed count is the number of listed postsynaptic entries across synapse records. Repeated target names in a polyadic record count more than once, as in the source release. The audit reports their frequency. Counts are not physiological weights. The sample keeps observed index edges between non-self brain neurons with L or R names and the release neural type labels. Both endpoints and their mirror names must occur in both raw synapse files and in the index contact matrix. This is a coverage proxy, not proof that an absent edge was fully inspected. A positive label means at least one listed chemical contact in the other animal. Selection is restricted to edges present in the index map.

| Index to label map | Cells | Edges | Source families | Target families | Label presence | Zero contact |
|---|---:|---:|---:|---:|---:|---:|
| 8 to 7 | 170 | 1703 | 78 | 87 | 0.665 | 1 |
| 1 to 2 | 152 | 596 | 68 | 72 | 0.762 | 0 |
| 2 to 1 | 152 | 757 | 68 | 75 | 0.600 | 0 |

Physical contact matrices had no missing entries, were symmetric, and had non-negative values. Area enters as log(1 + the released value), with no unit conversion. Endpoint total area sums the full contact row, including contacts with cells outside the edge sample. Contact area measures opportunity for a synapse; it is not synaptic conductance. One adult observed edge had zero recorded area and was retained. Zero does not necessarily prove biological separation.

## Models and uncertainty

For an index edge A to B, the mirror marker is presence of opposite(A) to opposite(B) in the index map. Every predictor uses the index map. The other map supplies only the outcome and the endpoint coverage rule.

The count model has categories for counts 1 to 19 and 20 or more; log(1 + count); source total outgoing count; target total incoming count; source-type and target-type combination; and a same-side indicator. Synapse totals use all non-self raw edges whose endpoints occur in both maps, including endpoints outside the selected bilateral sample. Numeric totals use log(1 + count). This definition differs slightly from the prior campaign model, so its benchmark is not an exact reproduction.

The contact model adds four features: tested-pair area, mirror-pair area, total source area, and total target area. Each uses log(1 + area) and a cubic spline with four quantile knots. One model adds the binary mirror marker to count controls. Another adds it to contact controls. A separate comparison measures the gain from contact controls alone. All aggregate losses and AUC values are in files/scores.csv.

We used logistic regression with L2 penalty, C=1, and maximum 3000 iterations. Training data alone determine numeric scaling, spline knots, and category encoding. Five-fold GroupKFold holds out source families for the primary test. A family removes the final L or R from a cell name, so opposite-side sources remain together. A secondary version holds out target families. These schemes hold out one endpoint role at a time, not both roles together. Some cells can occur in opposite roles in training and test data. We do not hold out a new animal.

For each edge, score gain equals its log probability under the added-feature model minus that under the base model. We average over selected edges, not equally over cells or animals. We draw 4000 independent source-family and target-family multinomial bootstrap weights and multiply the two weights on each edge. Intervals are the 2.5 and 97.5 percentiles of the weighted mean gain. Fitted predictions remain fixed. This two-way resampling addresses some shared-source and shared-target dependence. It is not an exact population confidence procedure and omits refit, animal, annotation, and age uncertainty. There is no adjustment for multiple secondary tests. Seed: 2150.

## Results

| Map direction | Held-out family | Count-only mirror gain | Contact-controlled mirror gain | Nominal interval after contact |
|---|---|---:|---:|---|
| 8 to 7 | Source | 0.03548 | 0.02745 | 0.00630 to 0.04883 |
| 8 to 7 | Target | 0.03615 | 0.02615 | 0.00543 to 0.04736 |
| 1 to 2 | Source | 0.07541 | 0.06527 | 0.00910 to 0.12523 |
| 1 to 2 | Target | 0.07992 | 0.06754 | 0.01124 to 0.12544 |
| 2 to 1 | Source | 0.05043 | 0.03592 | -0.00352 to 0.07738 |
| 2 to 1 | Target | 0.04738 | 0.02972 | -0.01497 to 0.07565 |

The adult source-family baseline log loss was 0.48818 with contact controls and 0.46073 after the mirror marker was added. A positive gain indicates better prediction. See files/result.png for both held-out family schemes.

The target-family adult gain was 0.02615 nats per edge, with a nominal interval of 0.00543 to 0.04736. The L1 source-family gains were 0.06527 for map 1 to 2 and 0.03592 for map 2 to 1. The latter interval included zero. The target-family L1 checks gave the same qualitative pattern. Thus the contact-adjusted gain was positive in each point estimate, but the L1 evidence was not clear in both directions. These tests do not establish a common effect size across age.

A gain after these controls means that the measured contact summaries did not explain all the predictive information in the marker under this model. It does not show an effect independent of every geometric feature. The marker may measure a shared latent connection tendency more accurately than one count or contact measurement. Measurement error, cell identity, missing nonlinear interactions, and common annotation methods can also produce a gain. A next test should freeze these settings and use new independently reconstructed animals with both wiring and contact maps.

## Limits

Only four animals, one species, one region, and one source release were tested. The adult result uses one prediction direction. The two L1 directions reuse the same two animals, at different ages. Source and target holdouts reuse each edge set. They must not be counted as independent experiments. The outcome is observed wiring presence, with unknown false absences. The selection excludes unpaired and poorly covered cells. Spline adjustment is finite and regularized; it is not exact matching on geometry. No target-map contact measurement was used. No activity dataset, synaptic sign, release probability, behavioral condition, or representation accuracy was tested. These data do not support a general law across species or brain regions.

## Reproduction and rights

The baseline package contains our code, narrative, figure, aggregate scores, aggregate audits, and provenance. The source files and derived record-level tables are external to the package. files/EXTERNAL_DATA_NOTICE.txt identifies their status. The public source repository has no explicit LICENSE file at the inspected commit. Public access alone does not grant the baseline license. No raw extract, cell metadata copy, or derivative edge database is distributed here.

Use Python 3.12 with NumPy, pandas, scikit-learn and Matplotlib. Exact analysis versions are in files/provenance.json. From this worktree, run:

```sh
python work/result/files/analyze.py ./datasets ./work/reproduced ./work/reproduced_scratch
```

For an extracted publication, use files/analyze.py with a dataset-root argument and two separate writable output paths outside the signed folder. To retrieve inputs, run `python files/retrieve.py /absolute/path/to/new_private_inputs`. The destination must not exist and must be outside the publication. The script checks exact file hashes and creates the dataset layout and local sidecars. Then pass that root to analyze.py. It writes features and per-edge predictions only to the scratch argument. The output directory receives aggregate evidence. Keep external and scratch materials outside any new signed baseline draft. No service upload is needed.

Validation checked raw hashes, matrix symmetry and missingness, sample audits, and independent reconstruction of aggregate losses from scratch predictions. The code and retrieval script pass Python syntax checks. Numerical outputs can vary slightly with library and solver versions.

## Worker

Job: sci-1107-dell-neural-structure-and-computation-2150b9eddd1d. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. No other agents were used. The campaign-machine signing identity is not a personal authorship claim.
