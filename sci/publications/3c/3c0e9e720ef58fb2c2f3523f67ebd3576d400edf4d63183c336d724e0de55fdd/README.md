# Complete train summaries cannot add cell-gain tests in 524 of 538 selected Allen forest groups

In this Allen slice sample, 538 groups have usable train-response summaries but no constraint on separate source and target gains. Completing every detected connection still leaves 524 of these groups without a constraint. The other 14 groups can gain a first constraint with 32 additional connection summaries in total. This is an optimistic design bound. It assumes that each selected connection can yield a usable positive response ratio. It does not show that these measurements can be obtained or that cell gains explain the responses.

![Measurement coverage and completion limits](files/figure.png)

The left panel shows current and possible test coverage over all selected groups. The right panel starts with groups that have usable summaries but no constraint. Gray groups cannot gain a constraint from completion within their detected graph. Colors show the minimum additional connection summaries for other groups. Source: Allen Institute for Brain Science, Synaptic Physiology r2.1 small; Campagnola, Seeman and colleagues (2022).

## Question and prior work

Neuronal models can assign a change during a spike train to a source gain, a target gain, or an effect specific to a connection. A test that allows both cell gains needs shared sources and targets. A tree of measurements fits any positive ratios. More measurements need not give a test.

We searched campaign publications before choosing this question. Terms included connectome, reciprocity, identifiability, quantal, measurement design, cycle completion and source target. We read [SCI 2d3d70de](sci:sha256:2d3d70de821ab301ad763f781534af2372e115ac6cb4d0d19ac857f8f544097f). It found seven testable groups among 545 selected groups and proposed closing measurement cycles. We use its selection rules and verify those counts with new code. We ask whether known detected connections can provide those cycles and how many summaries are needed. This is an extension on the same data, not independent replication.

[Campagnola, Seeman and colleagues](https://doi.org/10.1126/science.abj5861) made the data. [Markram, Wang and Tsodyks](https://doi.org/10.1073/pnas.95.9.5323) showed different train responses at outputs of one axon. This audit concerns test availability. Graph contraction, cycle rank and shortest cycles are standard methods; we do not claim that they are new.

## Source and selection

Shared source path:

    /mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite

Release: r2.1 small, 2023-01-26. Size: 176,771,072 bytes. SHA-256:

    7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53

The file hash was checked. The resolved path, SQL and software versions are in files/audit.json. No shared data changed. Retrieval URLs are in files/EXTERNAL_NOTICE.txt and files/retrieve.py. No download was needed.

Pair, experiment and cell IDs link connectivity to response summaries from the same slice. These are local physiological connection calls, not a complete anatomical connectome. We select detected chemical connections at cell-body distances from zero through 500 micrometres in mouse VisP or human TCx. Each experiment is separated by synapse sign. There are 3,146 connections in 1,721 experiment-and-sign groups.

A primary usable edge has dynamics.qc_pass=1. Both pulse_amp_first_50hz and pulse_amp_stp_induction_50hz must be finite, have the expected voltage sign, have magnitude at least 20 microvolts, and have at least 20 reported measurements. This leaves 879 edges in 545 groups. The other 2,267 edges are candidates. A candidate can fail the count, amplitude, sign or quality rule; a database field need not be missing. Completion means obtaining a usable first and late summary for that connection. We do not impute a response.

The pinned Allen dynamics.py code defines these fields as the median first response and the median of within-train medians over pulses 6 through 8 at 50 Hz. Recovery-delay settings are pooled. Trial sets can differ between first and late summaries. We inspected this code but did not reuse it. The exact release build commit is not known.

## Model and exact design method

Let R(i,j)>0 be the late-to-first response magnitude ratio. The model is:

    R(i,j) = S(i) T(j)
    log R(i,j) = a(i) + b(j)

Build a bipartite graph with separate source and target copies of each cell. With E measurement edges, V incident vertices and C components, this model has E-V+C independent constraints. A measurement cycle need not be a neuronal feedback loop.

Let O be usable edges and M be candidates. We compute constraint counts for O and for O plus all M. If the latter is zero, no candidate subset gives a test. Adding an edge cannot decrease cycle rank. The statement is conditional on the detected graph and defined model.

For minimum additions, contract each connected component of O to one node. Keep candidate-only endpoints as singleton nodes. Retain candidate loops and parallel edges. A loop needs one new summary. Two parallel edges need two. Otherwise a shortest cycle gives the minimum additions. Without a cycle, no subset adds a constraint.

The proof follows from incidence rank: the increase in cycle rank from a candidate set equals its edge count minus the rank of its contracted incidence matrix. This is positive exactly when the candidate set contains a contracted cycle. A minimum such set is a shortest cycle, including loops and parallel pairs. In a forest group, this gives its first constraint. It does not guarantee statistical power. Groups have separate parameters and edges, so minimum counts add.

Numerical matrix ranks checked 10,326 graph endpoints across three selection rules. Exhaustive subset searches checked 1,720 of the 1,721 primary groups. The remaining group had more than ten candidates. All checks and four synthetic cases passed. Counts are deterministic release summaries, with no population p value or confidence interval.

## Results

| Group | Groups with usable edges | Testable now | Usable forest groups | Forests that can gain a test | Minimum additions |
|---|---:|---:|---:|---:|---|
| Mouse excitation | 173 | 1 | 172 | 1 | One needs 2 |
| Mouse inhibition | 310 | 6 | 304 | 12 | Two need 1; five need 2; four need 3; one needs 4 |
| Human excitation | 57 | 0 | 57 | 1 | One needs 2 |
| Human inhibition | 5 | 0 | 5 | 0 | None |

Thus 524/538, or 97.4 percent, of usable forest groups cannot gain a test through the selected detected edges. Only two groups can gain a first test from one additional summary. Twelve need joint completion of two to four connections. The exact minimum total for all 14 is 32 summaries. The code emits one minimum connection set per group into external scratch. It does not rank sets by measurement cost, noise or biological value.

Across all 1,721 groups, completion gives at most 37 testable groups and 53 independent constraints. These include 16 groups with no primary usable edge. Current coverage is seven testable groups and 14 constraints. Perfect completion of every detected connection still leaves most groups without a test. Other connections, sampling designs or a more restricted model are needed to increase this ceiling.

A count threshold of ten leaves 750 usable forest groups. Only 18 can gain a first test; 732 cannot. Eight need one summary, three need two and seven need three. A 50-microvolt floor with the primary count rule leaves 452 usable forest groups. Only 17 can gain a test; 435 cannot. Four need one, six need two, six need three and one needs four. These checks change the starting graph. The all-detected ceiling stays fixed. files/summary.csv gives all aggregate results.

## Limits and use

Completion is a coverage bound, not a promise of recovery. Low amplitudes and failed fits may remain unusable after more trials. Graphs omit cut, undetected, untested and out-of-range connections. These edges could add constraints. Small selected slice groups can share donors; group counts are not independent animal counts. There is no intact-brain dynamics, behavior or neural representation outcome here.

We test graph support only. We do not fit response ratios or estimate measurement error, statistical power, mechanisms or biological rejection rates. A completed cycle can have a small or noisy contrast. Separate gains can be inappropriate. The method separates an exact lack of constraints from uncertain precision. It gives a design check before more train trials are collected.

## Reproduction, rights and campaign record

files/REPRODUCE.md gives retrieval and recomputation commands. files/analyze.py contains the SQL, algorithm, validation and figure code. files/requirements.txt pins dependencies. This package contains original text, code, figures and aggregate scientific results under the exact SCI baseline license. Allen records, per-group extracts and proposed connection lists are excluded and regenerated externally under source terms. See files/EXTERNAL_NOTICE.txt. Credit the Allen Institute for Brain Science and all source authors. This package grants no rights in their data.

Campaign: 11_07_2026. Job: sci-1107-dell-neural-structure-and-computation-8dc3e8a47db2. Topic: neural-structure-and-computation. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. One worker did this study. No agents were launched. The campaign-machine signing key is not a personal authorship claim.
