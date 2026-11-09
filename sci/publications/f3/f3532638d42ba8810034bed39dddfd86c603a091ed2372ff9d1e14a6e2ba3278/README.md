# Bilateral pooling gave median minimum routing errors of 0.133 and 0.124 in two adult worm count models

## Result

Merging bilateral source neurons loses one-step output detail in two fixed chemical synapse count models. The best common routing row has median worst-source total variation (TV) error 0.133 in adult map D7 and 0.124 in adult map D8. However, the left-minus-right differences have weak direction agreement across the two maps. No pair passes our conditional contact-allocation test in both maps. The study therefore does not establish stable side-specific routing across animals.

![Routing errors and controls](files/figure.png)

## Question and prior work

Can left and right partners share one routing row when destination partners are also merged? This is a useful check before a model treats bilateral partners as one computational unit. A merge can preserve total counts yet lose information about the source that sends a signal.

Witvliet et al. supplied maps across development [doi:10.1038/s41586-021-03778-8]. They showed stable, changing, and variable wiring. Birari and Rabinowitch reported synaptic partner asymmetry and studied redundancy and reachability [doi:10.1016/j.isci.2024.110713]. Thus, bilateral wiring asymmetry is known. Classical Markov chain theory states that exact aggregation requires equal transition sums into every destination group for all sources within a group [Kemeny and Snell, Chapter 6.3]. We apply that condition to an explicit count model. Neither the condition nor the elementary error identity below is a new theorem.

We searched the local campaign for connectome, Witvliet, lump, and coarse graining before calculation. We read the published study [sci:sha256:4758cdea8ce172e3b65fe29fb17050a6f62214c9fbe09f6dee33cd2f0e137a50]. It showed that coarse side totals can recover side assignments. We use its cohort rule and source metadata, but no code or result tables. Our new contribution is a source merge error audit, a conditional count control, and a cross-map direction check. The searches were not an exhaustive review. The internal plan in files/PLAN.md preceded calculation but was not externally registered.

## Data and scope

We reused the completed shared datasets in place. No data were downloaded or changed. The tables are from Worm Neuro Atlas commit b2e13d88b670efcb3438aeacba2ad4bd6c383933 and represent Witvliet adult maps D7 and D8. Both raw tables have positive integer counts and no duplicate pre-post-type rows. Only chemical rows enter the model.

The exact shared paths, resolved paths, file sizes, source URLs, and SHA-256 hashes are in files/provenance.json. The paths relative to this workspace are:

- datasets/worm-witvliet7-b2e13d88/adult7.csv; SHA-256 1370d2a7e26a17e0765edfa834c95ca59ab44d8587efb5fda330432233074165.
- datasets/worm-witvliet8-b2e13d88/adult8.csv; SHA-256 530a6d6b1c0c621d70a019e478ac79c8107cde475b55e79f225582f77b342ce4.

We intersect endpoint names between maps and exclude BWM-, CEPsh, GLR, and excgl names. This leaves 180 neurons, 83 terminal-L/terminal-R pairs, and 97 destination groups. Each name with no bilateral partner stays in a group of one. This name rule keeps dorsal and ventral subgroups separate. Missing edges within this endpoint set are assigned zero listed count. Isolated cells absent from both endpoint lists cannot enter. This is a partial brain sample. The retained chemical counts sum to 6587 in D7 and 7108 in D8.

## Model, error, and proof

For each source neuron i, sum the chemical counts to every destination group g to give C(i,g). Divide this row by its total to give p(i,g). Thus the model selects a listed outgoing contact at random and returns its destination group. It does not model excitation, inhibition, conductance, spike probability, or calcium activity.

For a source pair L,R with positive row totals, define

    TV = 0.5 * sum_g |p(L,g) - p(R,g)|.
    e = min_q max(TV(p(L),q), TV(p(R),q)) = TV / 2.

Here q is any probability row shared by both sources. The triangle inequality gives TV(p(L),p(R)) at most TV(p(L),q)+TV(q,p(R)), so the maximum error is at least TV/2. The midpoint q=(p(L)+p(R))/2 attains that bound for both sources. This proves the identity. The subset of destination groups with p(L,g)>p(R,g) attains the TV discrepancy. Thus e has an event-probability interpretation, not only a vector norm interpretation.

A zero-count source has no defined routing row. We exclude that source pair for the setting and report the denominator. We do not assign an artificial self-loop. The analysis is a local one-step audit on active rows; it is not a complete multi-step Markov model for cells with zero output. A zero error is the local equality needed for exact aggregation. A nonzero error does not imply different neural activity.

We also compute TV over named destinations before merging them. Merging destinations cannot increase TV; the code checks this property. For cross-map direction, d=p(L)-p(R) uses the same group order in both maps. A positive dot product d7.d8 means net agreement in direction. Cosine divides this dot product by both vector norms. It is undefined for a zero vector. We report signs and medians without an independent-pair significance test.

## Conditional contact control

For each pair and map, hold fixed both source totals and every pooled destination count C(L,g)+C(R,g). Randomly allocate contacts to L without replacement until its observed total is reached; R receives the rest. This is the multivariate hypergeometric allocation. It represents exchangeable, independent contacts conditional on those margins. For 9,999 draws and seed 11072026, the upper-tail p value is (1 + number of draw TVs at least the observed TV)/(10,000). Ties count in the tail. We apply Benjamini-Hochberg adjustment separately to all active pairs in each map.

This is an artificial reference model. Contacts at one release site can share a source and targets. The model does not preserve sites, spatial constraints, or developmental history. Its p and q values are conditional diagnostics, not calibrated probabilities for biological symmetry or annotation error. We supply all p values and null means and central 95% ranges. The ranges describe reallocation draws, not animal uncertainty. There are only two animals; no population interval is justified here.

## Results

| Count model outcome | D7 | D8 |
| --- | ---: | ---: |
| Active source pairs | 74 | 73 |
| Median TV after destination merge | 0.2664 | 0.2489 |
| Median minimum worst-source error e | 0.1332 | 0.1244 |
| Pairs with e greater than 0.10 | 57 | 49 |
| Pairs with TV equal to zero | 0 | 0 |
| Pairs with conditional q below 0.05 | 0 | 2 |
| Median of pair-specific null mean TVs | 0.2914 | 0.2805 |

Across the 73 pairs active in both maps, 37 have positive direction dot products. The median cosine is 0.00356. The two D8 calls are AWC (q=0.04015) and SDQ (q=0.00730). No pair has q below 0.05 in both maps. The p-value resolution is 0.0001; the smallest value does not mean zero probability. Large within-map merge errors therefore do not, by themselves, show a repeated side-specific routing pattern. The null means in the table are medians across pairs, not paired effect estimates. Lack of rejection does not prove equivalence or biological randomness.

## Planned sensitivity checks

We set small raw edges to zero before group sums for each count threshold. Binary weights set every listed edge to one. The own-group check removes the query pair's destination group and then renormalizes. These are changes to the model, not independent data replications. Conditional p values were planned only for the primary count model.

| Setting | Active D7 / D8 | Median e D7 / D8 | Positive direction dots / pairs active in both |
| --- | ---: | ---: | ---: |
| counts | 74 / 73 | 0.1332 / 0.1244 | 37 / 73 |
| binary | 74 / 73 | 0.1917 / 0.1786 | 38 / 73 |
| min2 | 73 / 73 | 0.1293 / 0.1157 | 36 / 73 |
| min3 | 71 / 72 | 0.1114 / 0.1023 | 35 / 70 |
| min5 | 60 / 61 | 0.1310 / 0.0571 | 24 / 57 |
| exclude_own | 73 / 73 | 0.1331 / 0.1170 | 37 / 73 |

The count thresholds change both weights and coverage. At threshold 5, many rows have few partners or become zero. The lower D8 median in that setting should not be read as proof that weak edges alone cause the primary error. Removing the own destination group leaves the main median errors similar.

## Checks and limits

The code checks raw hashes, positive integer counts, unique raw edges, and TV contraction under destination merging. Independent linear programs check every primary pair-map minimax error. files/validate.py computes TV again from saved integer matrices with a positive-event formula, checks midpoint errors, tests identical and disjoint synthetic profiles, and checks the q values with a separate SciPy implementation. Validation records are supplied.

Only two fixed partial adult maps from one study enter this test. No Allen data or neural activity enter. The use of public structure alone was chosen to permit an exact, auditable model test. The same neuron labels and reconstruction methods can share errors across maps. Counts are not conductances. Grouping by terminal names is an anatomical rule, not a validated functional equivalence. The artificial contact control can miss site dependence. Absence of a repeated conditional rejection is not an equivalence result. Weak direction agreement can reflect biological variation, count variation, or measurement limits. No generalization across species, brain regions, ages, or behavioral conditions is established.

The practical result is a reusable check: before interpreting a bilateral count model as one common routing process, report its minimum source-specific error and check whether the lost direction repeats across animals. A next study should link this audit to activity from identified cells, with more independent maps and a release-site control.

## Reproduction

See files/REPRODUCE.md. The package retains original analysis code, the derived integer matrices, labels, every pair score, null summaries, direction vectors, cross-map scores, software versions, source hashes, and the figure. Shared raw tables are not copied. files/retrieve.py gives a hash-checked private retrieval route. The signed bundle can be checked offline without running any code.

## Campaign record and license

Job: sci-1107-dell-neural-structure-and-computation-8a23e47d0929. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort through Codex in T3 Code. Date: 2026-11-09. No agents were launched. The campaign-machine signing key is not a personal authorship claim. No private keys are included.

The SCI baseline license covers new text, figures, original code, and derived evidence. Raw source data retain their upstream terms. No upstream software was copied. This publication does not claim to relicense the upstream repository.
