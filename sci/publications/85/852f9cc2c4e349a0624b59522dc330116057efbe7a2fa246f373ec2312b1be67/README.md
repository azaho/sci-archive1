# Source and target resampling left early mirror-link prediction gains uncertain in 862 worm connections

An early chemical link with a left-right mirror link gave better point predictions of link presence in two adult worm maps. The added value was uncertain when we resampled both source and target families. In 862 selected connections, source-family holdout reduced mean log loss by 0.027745 nats per connection. The nominal 95 percent crossed-family interval was -0.010507 to 0.065414. Target-family holdout gave a reduction of 0.037142, with an interval of -0.003360 to 0.077791. These bounds condition on fitted predictions. They do not measure uncertainty across adult animals.

This result gives a small benchmark for testing structural consistency before linking a connectome to activity from other animals. It does not establish synapse survival, a causal effect of bilateral wiring, or a computation in a living circuit.

![Raw shares and model gains](files/result.png)

Figure 1. A: Adult presence shares by early site count and mirror-link presence. The shares have no uncertainty bars and are descriptive. Mirror-absent bins above count two contain only 5, 1 and 1 connections; no mirror-absent link has count above seven. See strata.csv for all counts. B: Added prediction gains with nominal 95 percent ONE-FACTOR family resampling intervals. Each group uses its own holdout predictions. These intervals omit dependence through the other family factor. The wider crossed-family bounds in the main text and twoway.csv include zero for both primary fits. A figure interval above zero is therefore not evidence of a resolved gain across families.

## Question and prior work

Does early mirror-link presence add information about adult link presence after early strength, cell type, and cell connection totals are known?

Witvliet et al. (2021; doi:10.1038/s41586-021-03778-8) mapped eight different animals across development. They described stable, variable and changing connections. Their connection classes use strength and left-right symmetry. We do not use these classes as outcomes. That would make this test circular. Our outcome comes directly from the two adult maps.

We searched the local campaign before selecting this question. The search terms and returned titles are in campaign_search.json. We read two signed reports. SCI 7f2ce4d0a699d3b9970f466f6936638b25a2c4c1b710e11d6527b2dcf875b1cd tested whether bilateral targets share release sites. SCI 809f8313ac633c42aedeae74c4aa57e73ef6a32c821c03a716f83f02a8ea30e0 tested whether a mirror evoked response adds response prediction value. Those are different tests. Here both predictor and outcome are anatomical. No prior code or result table was reused. Search was not an exhaustive review. This study does not claim to discover bilateral consistency.

## Data and selection

We reused eight primary DatasetN_synapses.json files and two metadata files from repository commit 0646af9d25896ae660f97d462eab2d67282f5625. No raw files were downloaded or changed for this study. The exact shared paths, URLs, byte counts and SHA-256 hashes of all ten used files are in files/provenance.json. The data path pattern is /mnt/dell-data/shared_datasets/witvliet2021-primary-synapses-N-0646af9/DatasetN_synapses.json. Metadata paths use witvliet2021-neuron-info-0646af9 and witvliet2021-dataset-info-0646af9 under the same shared root.

A site is one source JSON row. A target neuron can occur more than once in a row. We count it once per site. All serialized catmaid_id values are distinct within each file. Duplicate-target row counts are 1, 7, 11, 18, 26, 30, 65 and 84 in maps 1 through 8. source_qc.json records these checks. Site volume and target area weights are unused.

We retain neuronal names observed as a source or target in all eight files, with names ending in L or R and with their opposite-side partner also observed in all files. The upstream is_neuron function removes muscles and other cells. This gives 150 cells in 75 bilateral families. The panel is selected for observed coverage; absence outside it is not tested. It excludes unpaired cells and dorsal-ventral pairs. The choice uses coverage in adult files but does not require any particular adult edge.

For each early map pair, sum distinct-site counts on directed edges inside this panel. Keep nonself edges with a positive sum. The primary pair is maps 1 and 2, at 0 and 5 hours after hatching, both L1. There are 862 edges from 66 source families to 73 target families. An outcome is one if the edge has at least one site in EACH adult map, 7 and 8, both at 50 hours. There are 571 positive outcomes. Zero means that at least one map lacks the edge. Zero is not a verified biological absence.

The mirror of source a to target b is opposite-side(a) to opposite-side(b), with direction retained. The tested predictor is one if the mirror edge has a positive early count sum. Adult mirror edges never enter the predictor. The count table includes self edges for cell-total calculations, but they are excluded as prediction cases.

## Fixed prediction model and changes made during analysis

Both models are logistic regression with L2 regularization, C=1, maximum 3000 iterations. Standard scaling is fitted on training rows only. There is no penalty tuning. Baseline columns are log(1+x) counts from each early map; log total count; an indicator of presence in both early maps; count categories 1, 2, 3, 4, 5-7, and 8 or more; source-target broad cell-type categories; same-side indicator; and log(1+x) source output site total, target input site total, source output degree, and target input degree. The corresponding four totals for the mirror cells are also included. All cell totals use early edges inside the panel. The added model has exactly one extra column: early mirror-edge presence.

This is an exploratory analysis, not a registered test. The first baseline omitted degrees and mirror-cell totals. Its primary source-holdout gain was 0.036605. After viewing that result, we added those controls to test a cell-connection-total explanation. The final gain fell to 0.027745. We also added crossed-family uncertainty after inspecting one-factor uncertainty. These changes and all final sensitivity rows are disclosed. They do not create an independent confirmation.

We use five-fold StratifiedGroupKFold, shuffle enabled, seed 1107. The primary split holds out source families. Both mirror sources are in the same family and thus remain together. A second split holds out target families. No family of the held-out grouping can cross its split. This tests prediction for unseen source families or unseen target families, separately. It does not hold out both at once. Unsupervised dummy category vocabularies use all selected rows; training outcomes do not cross folds.

Mean log loss weights each selected directed edge equally. Positive loss reduction means the added predictor improved point prediction. The primary source-holdout baseline loss is 0.505667 and the added loss is 0.477923. AUC rose from 0.809390 to 0.837832. In target holdout, loss changed from 0.530192 to 0.493050 and AUC from 0.790017 to 0.827559. AUC is descriptive; we do not compute a separate AUC test.

## Uncertainty and sensitivity

We first resampled held-out families 5000 times, retaining all their edges and using edge-weighted mean loss gain. These source-only bounds were 0.008497 to 0.047950. Target-only bounds were 0.009618 to 0.062595. Connections share both source and target circuits, so either one-factor result can miss dependence.

For the primary two fits, we then independently resampled source families and target families, each with replacement at its original family count. Each edge gets the product of its two family multiplicities. The resulting 5000 crossed-family draws gave the bounds in the first paragraph, which include zero. All draws are saved. These are nominal conditional ranges, not calibrated population confidence intervals. They do not refit the model, vary folds, or resample animals. No population p-value is claimed.

With the stronger outcome of at least two adult sites in each map, source holdout gave gain 0.016351 and one-factor bounds -0.000429 to 0.033617; target holdout gave 0.015634 and -0.003125 to 0.033975. Thus this stricter test is also unresolved under its one-factor ranges.

Maps 3+4 (L1 at 8 and 16 hours) and maps 5+6 (L2/L3 at 23 and 27 hours) are sensitivity predictors with the same adult outcomes. They give positive point gains in both split schemes. All twelve final combinations of early pair, adult threshold and split are in results.csv. These are dependent analyses of the same adults, not six independent replications. No multiple-testing significance claim is made.

## Limits and scientific use

Only two adult animals enter every outcome. Early and adult animals differ. A link present in all these maps need not be the same physical synapse through time. Same-site counts are structural observations, not conductance, release probability or response reliability. Some early links may be transient or missed by annotation. Spatial neurite overlap and annotation confidence are not controlled. Both can support mirror consistency without a special circuit function.

Mirror-absent edges are mostly weak. Count categories and continuous counts reduce this imbalance but do not give matched causal comparisons. We did not test penalty sensitivity or other classifiers. The panel depends on observed coverage in all eight maps. Shared target dependence makes a source-only interval too narrow for this question, and even the crossed scheme is an approximate description of this fixed graph.

The result supports a testable candidate cue for linking structural maps: an early mirrored edge. It leaves its added value uncertain under crossed-family resampling. It cannot justify matching activity records on mirror structure alone. There are no neural activity data, Allen data, other species, other brain regions or behavioral conditions in this package. Transfer to neuronal computation or reliable representations needs an independent structure-activity study.

## Inspection and reproduction

files/REPRODUCE.md gives exact commands for a derived-table rebuild and a raw rebuild with verified retrieval. counts.csv, cells.csv and predictions.csv preserve the evidence for inspection. analyze.py reproduces the fits. validate.py independently reconstructs all eight count tables from raw rows, checks outcomes and loss arithmetic, checks saved intervals, and computes crossed-family draws. All checks passed for eight maps and 150 cells. versions.json records the environment. The figure is a static PNG below SCI display limits.

The SCI baseline license applies to new text, figures, derived evidence and original code. Raw data and upstream software retain their source terms. The GPL-3.0 upstream metadata software is not copied into this package. No private key or credential is included.

## Campaign record

Job: sci-1107-dell-neural-structure-and-computation-3c11d59b0769. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code. Date: 2026-11-09. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim.
