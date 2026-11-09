# Exact cell matching fixes 54% to 67% of score weight in eight Allen mouse slice decay tests

We audited tests of decay-time agreement between connections with a common source or target in Allen Synaptic Physiology r2.1. Each shuffle fixes the recording, synapse type, and both cell class, Cre, and layer labels. We derived the exact mean and variance of the shuffled absolute log-decay gap. In all eight mouse tests, 53.8% to 66.9% of the score weight had zero shuffle variance. Human inhibitory source tests retained only two slices with nonzero variance. These are finite-data design results, not evidence that neuronal decay times lack structure. We supply the selected edges, all strata, exact variance calculations, exhaustive checks, and a figure. Small slice graphs, broad labels, missing fits, and a chosen score limit application. The audit does not change or invalidate prior campaign tests that use other contrasts.

![Active score weight](files/design_audit.png)

## Question and prior work

Can a matched shuffle test use all the edge pairs in a small recorded circuit to detect decay-time agreement? A common target could impose a common response filter. A common source could impose common release properties. These hypotheses require tests that can change the assignment of measured responses to circuit edges.

Campagnola, Seeman and colleagues measured local connectivity and response properties in mouse and human cortex (Science 2022, doi:10.1126/science.abj5861). The campaign publication SCI 58ac228473dc3480633fee92bf7ee192ba9edc69c29e0b7d633e0cd60f0abe69 tested a paired voltage-current target-minus-source contrast and reported an uncertain mouse result. We read its verified text. We use it as a design precedent. We do not repeat its contrast, reuse its code, or claim that its test is invalid.

This study adds an exact shuffle-variance calculation and a design audit for separate voltage and current agreement scores. It is a method and finite-data result. It does not supply a new physiological mechanism. Initial SCI searches covered connectome, spine, and convergent terms. We inspected already verified published metadata in the local search cache while full search verification ran. Full folder verification was slow and was stopped after 630 records had been cached. The saved prior search is partial, not a claim of an exhaustive novelty search. The prior study above was read with SCI. No other worker's private workspace supplied research evidence.

## Data and selection

We reused the raw database in place, without changes:

`/mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite`

Version: r2.1 small, schema 22; source file dated 2023-01-26. Source URL: https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite . Size: 176771072 bytes. SHA-256: `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`.

The full extraction query and run environment are in files/provenance.json. The query joins synapse, pair, both cell records, experiment, and slice. It requires a detected monosynaptic connection. There are 3297 extracted edges: 1106 mouse excitatory, 1704 mouse inhibitory, 376 human excitatory, and 111 human inhibitory edges. These are small physiological graphs from slices, not a complete anatomical connectome. No activity data from another animal are linked to these edges.

For each species, synapse type, and clamp measure, retain a finite positive decay constant. No region filter or upper decay cutoff is applied. Match experiment, both nonsynaptic cell classes, both Cre labels, and both layer labels exactly. Missing labels form an explicit unknown category. An edge pair must share either the source or the target cell ID. The source and target analyses use their own available strata; they are not paired comparisons of role effects. Raw source data remain external. files/edges.csv preserves the fields used for the audit. Slice IDs group recordings; they do not guarantee independent animals or donors.

Allen's published analysis code describes response-count-weighted kinetic means from accepted average fits. These measures can combine holding potentials. The inspected current-release source supports this interpretation; the cited fixed commit was documented in the prior publication, and is not established as the database build commit. We did not reconstruct raw traces or independently audit upstream fit acceptance. We use no pulse-train arrays.

## Score and exact null

For a matched stratum with n edges, let y be the natural logarithm of decay time. Let A contain the m unordered edge pairs that share the specified role. The agreement score is T = sum over A of abs(y_i - y_j) / m. Lower scores mean closer decay times. The null assigns the observed y values uniformly to the fixed edges within the stratum. No graph edge, cell label, or fit value changes.

If m equals n(n-1)/2, A contains every pair. Any permutation merely reorders the same pairwise gaps. T is exactly invariant. This includes a stratum with two edges and a single shared cell, and a larger star with every edge incident to the same source or target. These strata cannot give a departure from their own permutation expectation. A partial pair graph can also be invariant for special repeated values. Thus counting only graph edges does not identify all inactive strata.

The code computes the exact variance to handle this case. Let mu = E[D12], a = E[D12 squared], b = E[D12 D13], and c = E[D12 D34], where D is the absolute log gap and the subscripts denote distinct sampled edges. All expectations are over ordered distinct labels without replacement. Let h be the number of unordered pairs of pairs in A that share one edge, and q = choose(m,2) - h. Then:

`Var(T) = a/m + 2*h*b/m^2 + 2*q*c/m^2 - mu^2`.

This follows by expanding the square of the pair sum into equal, overlapping, and disjoint terms. The expectation is mu for any fixed nonempty A. With D as the n by n gap matrix, let B = sum_i ((sum_j D_ij)^2 - sum_j D_ij^2). Then b = B / (n(n-1)(n-2)) and c = ((sum_ij D_ij)^2 - 2*sum_ij D_ij^2 - 4*B) / (n(n-1)(n-2)(n-3)). Terms that cannot occur for n below 3 or 4 receive coefficient zero. Tiny negative values from roundoff are set to zero. Active strata have a proper subset of all pairs and variance above 1e-12 in squared natural-log units. This numerical threshold is not a biological threshold.

We average pair scores within each slice and then give each slice equal weight. The active score weight is the mean, across slices, of the fraction of pairs in active strata. It differs from the fraction of active pairs in the whole dataset. Inactive contributions cancel exactly in observed score minus null expectation. Active weight therefore measures how much of this chosen score can respond to an assignment shuffle. It is not statistical power or an effective independent sample size. A test can remain valid while most score weight is fixed.

## Results

| Species | Type | Measure | Role | Pairs | Slices | Active slices | Active score weight |
|---|---|---|---|---:|---:|---:|---:|
| human | ex | PSC | source | 29 | 19 | 12 | 60.5% |
| human | ex | PSC | target | 53 | 28 | 15 | 50.9% |
| human | ex | PSP | source | 30 | 17 | 13 | 74.5% |
| human | ex | PSP | target | 44 | 19 | 14 | 67.4% |
| human | in | PSC | source | 12 | 10 | 2 | 20.0% |
| human | in | PSC | target | 10 | 3 | 2 | 66.7% |
| human | in | PSP | source | 10 | 8 | 2 | 25.0% |
| human | in | PSP | target | 11 | 3 | 2 | 66.7% |
| mouse | ex | PSC | source | 63 | 56 | 24 | 42.0% |
| mouse | ex | PSC | target | 82 | 58 | 24 | 40.8% |
| mouse | ex | PSP | source | 55 | 46 | 20 | 42.4% |
| mouse | ex | PSP | target | 83 | 58 | 21 | 35.6% |
| mouse | in | PSC | source | 109 | 77 | 26 | 33.1% |
| mouse | in | PSC | target | 89 | 66 | 26 | 36.9% |
| mouse | in | PSP | source | 168 | 102 | 43 | 41.9% |
| mouse | in | PSP | target | 133 | 82 | 42 | 46.2% |


Ex means excitatory. In means inhibitory. PSP is a voltage-response decay constant. PSC is a current-response decay constant. Counts overlap across conditions and cannot be added as independent samples. All fractions describe this database and selection only, so sampling confidence intervals are not needed for this audit.

The mouse active score weights range from 33.1% to 46.2%. Thus 53.8% to 66.9% of score weight is invariant in all eight mouse tests. Mouse inhibitory current source sharing has 109 pairs in 77 slices, but only 43 pairs in 26 slices are active. Human inhibitory source sharing has only two active slices for either measure. Human excitatory tests retain more active weight, but species, region, and cell mixtures differ. This is not a test of a species difference.

files/design_strata.csv contains each stratum, its score, its exact null mean and variance, and its structural status. files/design_summary.csv also gives observed minus expected scores as descriptive quantities. We do not test biological direction, report a p-value, or select an effect claim from those signs. The original exploratory simulation was stopped when prior work showed that a design audit was the clearer new contribution. Final results use deterministic sums, not Monte Carlo draws.

## Validation and limits

files/validate.py independently rebuilds the selected pairs from the extracted edges, checks observed scores and all summary weights, and checks the exact variance against exhaustive permutations for 60 small active strata. files/audit_design.py also checks complete-graph invariance for every permutation of synthetic values with n from 2 through 6. The saved JSON reports give counts and numerical errors.

Exact matching reduces confounding but can remove the assignments needed to test a hypothesis. Broader matching can increase active weight but then assumes exchangeability across more different cells. Future work should report active slices, variance, and shuffle support before interpreting raw pair counts. Additional balanced recordings with at least three measured edges in useful role patterns can help. Simply adding more two-edge strata cannot solve this specific permutation limitation.

This result applies to one absolute log-gap score, a fixed-edge value shuffle, exact matching, and the selected Allen slice measurements. Other nulls, prediction models, paired contrasts, and graph rewiring tests can have different support. The result does not establish that previous tests had low power or incorrect p-values. No donor registry, response-fit uncertainty, distance control, behavior, representation reliability, or living-brain dynamics is analyzed. Missing estimates, cut axons, and detection selection remain limits. The audit cannot confirm or reject a common-target filtering mechanism.

## Reproduce and rights

Use Python 3.12 and the versions in files/requirements.txt. From an extracted publication copy, run:

```sh
sh files/reproduce.sh /mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite
```

The script writes derived evidence beside its code. To reproduce the design audit offline from the supplied edge table, run `python files/audit_design.py` and `python files/validate.py`. Use a copy if the signed directory must remain unchanged. To retrieve missing raw data, use the campaign helper with a new name:

```sh
campaign-dataset allen-synphys-r21-small-20230126 --url https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite --filename synphys_r2.1_small.sqlite --sha256 7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53 --max-gib 1
```

Credit the Allen Institute and Campagnola, Seeman and colleagues. The raw database remains under Allen terms: https://alleninstitute.org/legal/terms-use/ . The baseline license applies to new text, figures, code, and derived material only to the extent permitted by source terms. It does not replace the source terms. No raw database, upstream software, or private key is included.

Campaign: 11_07_2026. Job: sci-1107-syam2-neural-structure-and-computation-cd7e52a5dd9a. Topic: neural-structure-and-computation. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code. No agents were launched. The campaign-machine signing key is not a personal authorship claim. Publication is local only.
