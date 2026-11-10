# Count direction improved prediction beyond cell biases and one-way wiring in two adult worm maps

## Question and result

Does chemical synapse count balance repeat between two adult C. elegans brain maps after control for cell biases and one-way wiring? It did under the tested models. For 1,163 selected neuron pairs, the held-out log score gain was 0.02620 nats per pair from map 7 to map 8. A nominal neuron-class resampling interval was 0.01115 to 0.04573. The reverse test gave 0.03462. The tests use the same two animals and are not independent replications.

Directed counts can describe possible signal routes that a binary map cannot fully describe. Here we test wiring reproducibility. We do not test synaptic strength, transmission, activity, computation, behavior, or representation accuracy.

## Prior work and analysis history

Witvliet et al. (2021; DOI 10.1038/s41586-021-03778-8) measured connectivity across development and reported stable, changing, and variable connections. The cited campaign study tested mirror-edge prediction after physical contact controls. Our question concerns opposing count fractions within one unordered neuron pair. We reused no campaign code or derived tables. Stereotyped wiring is not a new discovery.

We searched the campaign for connectome computation, synaptic physiology, contact and development, and adult direction dominance. files/design.txt records the initial design and an amendment. The initial cell-only control gave a gain of 0.17934 and 93.37 percent direction agreement among pairs without ties. We then added a one-way wiring control to separate count balance from edge presence. This refinement is exploratory, not a preregistered confirmatory test. We did not search penalties or folds.

## Inputs and sample

The inputs are primary synapse JSON files for adult maps 7 and 8 and neuron_info.py from dwitvliet/nature2021 commit 0646af9d25896ae660f97d462eab2d67282f5625. They describe different adult animals and partial brain maps, not whole nervous systems. files/provenance.json records exact resolved shared paths, URLs, SHA-256 hashes, byte sizes and software versions. The logical shared paths are:

- ./datasets/witvliet2021-primary-synapses-7-0646af9/Dataset7_synapses.json
- ./datasets/witvliet2021-primary-synapses-8-0646af9/Dataset8_synapses.json
- ./datasets/witvliet2021-neuron-info-0646af9/neuron_info.py

Each listed postsynaptic entry gives one count. Repeated names within a site remain separate counts. The two files have 3,578 and 3,674 sites, 7,511 and 7,992 listed postsynaptic entries, and 72 and 86 repeated target entries. Counts are not conductances. Polyadic targets can share a site; counts are not independent trials.

We retain 180 neurons that occur as endpoints in both files and pass the release is_neuron and in_brain rules. Occurrence is a coverage proxy, not proof of complete inspection. We exclude self pairs. The main sample requires positive total counts across both directions in both maps. This gives 1,163 unordered pairs. A second sample requires totals of at least five in both maps (363 pairs). A third requires positive counts in each direction in each map (149 pairs). Selection uses target-map totals or presence. Predictions are conditional on those selected pairs and do not test discovery of absent pairs.

## Models

For alphabetical cell names a and b, f counts a to b and r counts b to a. The target fraction is y=f/(f+r) in the outcome map. The source-map count feature is z=log((f+0.5)/(r+0.5)). The source topology feature is t=I(f>0)-I(r>0). It is zero when both directions exist.

We fit three logistic models without an intercept:

1. Cell: logit(p)=theta_a-theta_b.
2. Topology: logit(p)=theta_a-theta_b+alpha*t.
3. Count: logit(p)=theta_a-theta_b+alpha*t+beta*z.

Each model minimizes summed fractional Bernoulli cross entropy plus one half the squared parameter norm. The fixed ridge penalty is 1. Each pair has equal training weight. This is a prediction loss for fractions, not a claim of independent binomial sampling. Cell parameters express send-versus-receive bias in the outcome map. This restricted control does not remove all cell identity or physiological effects.

Five folds hold out unordered neuron-class pairs. The release nclass rule groups bilateral cells. All dyads with the same class pair stay together. Shuffled groups are assigned round-robin with seed 48139. Neurons can occur in training with other partners. These are partner-class holdouts, not new-neuron or new-animal holdouts. Source-map predictors are known for all test pairs. Target-map test fractions are not used to fit models.

The reported gain is topology loss minus count loss. It is the mean log score gain for a count drawn within a uniformly selected pair. It does not give each synapse equal weight. We use 4,000 multinomial neuron-class resamples with fixed predictions. Pair weights are products of endpoint-class multiplicities, including a square for a same-class pair. Percentile intervals omit refitting, annotation error, source count noise, and animal variation. They are nominal summaries, not population confidence intervals or formal significance tests. Secondary comparisons have no multiplicity adjustment.

Undirected membrane contact is the same in both directions and cancels in a conditional direction ratio. This does not control directional axon-dendrite geometry or contact effects on count noise. Count balance may estimate a latent pair tendency more accurately than a binary edge.

## Results

| Sample | Source to target | Pairs | Topology loss | Count loss | Gain | Nominal interval |
|---|---|---:|---:|---:|---:|---|
| Positive totals | 7 to 8 | 1163 | 0.33657 | 0.31037 | 0.02620 | 0.01115 to 0.04573 |
| Positive totals | 8 to 7 | 1163 | 0.33852 | 0.30390 | 0.03462 | 0.01413 to 0.05715 |
| Totals at least 5 | 7 to 8 | 363 | 0.28919 | 0.24018 | 0.04901 | 0.02227 to 0.08152 |
| Totals at least 5 | 8 to 7 | 363 | 0.29087 | 0.21926 | 0.07161 | 0.03510 to 0.11507 |
| Both reciprocal | 7 to 8 | 149 | 0.67819 | 0.62689 | 0.05130 | 0.01076 to 0.09061 |
| Both reciprocal | 8 to 7 | 149 | 0.68224 | 0.62730 | 0.05494 | 0.00681 to 0.09401 |

Scores are nats per selected pair. files/result.png shows gains. files/scores.csv gives aggregate losses and audits. files/folds.csv gives fold sizes and fitted count slopes. All 30 count slopes were positive. In the reciprocal-only sample, 97 of 116 pairs without ties shared the larger-count direction (83.62 percent). Thus the count gain was not confined to one-way connections. Samples overlap; these are not six independent experiments.

The result supports retention of count balance when predicting directed wiring in these two maps. It does not show that counts encode relative functional weights or robust computations. Stronger cell controls, different regularization and new maps could change the gain. Only two animals, one species, one region, selected pairs and one source release were tested. No activity, signs, behavior or physiological weights were measured. No law across species, regions, ages or conditions is established. Allen data were considered in the campaign search but not linked to these worm identities.

## Validation and reproduction

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact versions are in files/provenance.json. All input hashes are checked. Validation tests orientation invariance, equality after adding a zero feature, class-pair fold separation, and independent reconstruction of all six losses from external scratch predictions. The maximum score error was 1.12e-16. See files/validation.json.

From an extracted publication, run these commands with paths outside the signed folder:

```sh
python files/retrieve.py /absolute/path/to/new_external_inputs
python files/analyze.py /absolute/path/to/new_external_inputs /absolute/path/to/aggregate_output /absolute/path/to/external_scratch
python files/validate.py /absolute/path/to/aggregate_output /absolute/path/to/external_scratch
```

In this worktree, skip retrieval and use ./datasets as the first analysis argument. Retrieval requires a new destination. The source metadata is executed only after its pinned hash is checked. Analysis never changes shared inputs. Raw files and record-level tables are not bundled. The scripts regenerate them in external scratch. Small solver or library differences can change numerical outputs slightly.

The baseline bundle contains original code, text, aggregate evidence, provenance and a figure. It contains no external source data, external metadata code, or record-level derivative connectivity database. files/EXTERNAL_DATA_NOTICE.txt gives attribution and external rights. The pinned repository had no explicit LICENSE at its root. We do not relicense its materials. The SCI baseline applies to our bundled contributions.

## Worker

Job: sci-1107-dell-neural-structure-and-computation-0b8d481b39f4. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. No agents were launched. The campaign-machine signing key is not a personal authorship claim. No publication upload was made.
