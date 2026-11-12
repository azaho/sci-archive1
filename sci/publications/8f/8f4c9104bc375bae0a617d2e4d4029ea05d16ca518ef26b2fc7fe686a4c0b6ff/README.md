# In one MICrONS mouse, synapses of one connection share a size component only when the axon is from a layer 2/3 or layer 4 excitatory cell, and this component does not follow co-tuning

## Summary

We asked a structure question and a structure-function question about synapse size in the MICrONS cubic millimetre of mouse visual cortex (minnie65, release v1300).

1. When two or more synapses connect the same presynaptic cell to the same postsynaptic cell, are their sizes more similar than cell identity and location predict? This is a known signature of a shared plasticity history (Bartol et al. 2015; Motta et al. 2019; Dorkenwald et al. 2022). Earlier work used small volumes and mostly layer 2/3 pyramidal cells. Campaign tests in the Allen V1 Deep Dive mouse did not resolve it (sci:27b63e3c, sci:ba1aabb2).
2. If the shared component exists, does it follow the functional similarity (signal correlation) of the two cells? A Hebbian account predicts that it should.

We used cleft size (voxel count) of 13.7 million synapses between 71,822 cells with one nucleus and a cell-type label. The main sample used the 2,042 cells with a proofread axon. We built a **double-difference estimator**. For each pair of synapses i, j in one connection, at distance d, we found three distance-matched control synapses:

- k: same axon, other postsynaptic cell of the same type;
- l: same postsynaptic cell, other axon of the same class;
- m: other axon and other postsynaptic cell of the same class pair.

With z the standardised log cleft size, T = z_i z_j - z_i z_k - z_i z_l + z_i z_m. If size is the sum of an axon term, a postsynaptic-cell term, a smooth spatial field, a connection term and noise, then the mean of T is the variance of the connection term (as a fraction of total size variance). Axon, target and location effects cancel. On synthetic data with a true value of 0.30 the estimator gave 0.308 (0.256 to 0.361). With a true value of 0 it gave -0.009 (-0.051 to 0.033) (`files/results/synthetic_test_output.txt`).

## Main results

**1. A connection-specific size component is present for excitatory-to-excitatory connections, but it is near zero for connections that involve an inhibitory cell (Figure 1).** For proofread excitatory axons, the component was 0.158 (0.116 to 0.205) onto 23P targets, 0.224 (0.175 to 0.278) onto 4P, 0.210 (0.166 to 0.257) onto 5P-ET and 0.155 (0.100 to 0.218) onto 5P-IT. Onto basket cells (BC) it was 0.027 (0.002 to 0.052). Onto Martinotti cells (MC) it was 0.016 (-0.011 to 0.042). For BC and MC axons onto excitatory targets with at least 1,000 connections, all estimates were between -0.003 and 0.030. Each interval includes or is close to zero, with tens of thousands of connections (for example BC to 23P: 0.003, -0.010 to 0.016, 41,833 connections). Intervals are 95% percentile intervals from cluster bootstraps. We report the wider of the presynaptic-cell and postsynaptic-cell bootstraps. The raw within-connection product (no controls) was 0.25 to 0.32 for E to E and 0.03 to 0.13 for other pairs. Thus, about one third of the raw E-to-E similarity comes from cell and location terms.

**2. The component depends on the presynaptic cell type, not on the target type (Figure 2A; `files/results/pretype_by_posttype_proofread_EE.csv`).** Pooled over excitatory targets, it was 0.318 (0.271 to 0.364) for 23P axons (463 axons, 4,269 connections) and 0.204 (0.171 to 0.239) for 4P axons (552 axons, 7,014 connections). It was 0.049 (-0.003 to 0.122) for 5P-IT, 0.023 (-0.033 to 0.130) for 5P-ET, 0.065 (0.007 to 0.131) for 6P-IT and 0.044 (-0.024 to 0.108) for 6P-CT axons. The pattern holds within each target type. For example, onto 23P targets: 23P axons 0.26, 4P axons 0.16, 5P-IT axons 0.06. Onto 5P-ET targets: 23P axons 0.36, 4P axons 0.19, 5P-IT axons 0.06. 23P-to-23P and 5P-IT-to-23P synapses both lie mostly on 23P dendrites in the upper layers. Thus, cortical depth of the synapse alone does not explain the difference.

**3. The component does not decrease with distance between the two synapses (Figure 2B).** For E-to-E connections it was 0.177 at 20-40 um, 0.174 at 40-80 um and 0.168 at more than 80 um (straight-line distance). Estimates below 20 um were higher (0.29 to 0.40) but had wide intervals. Most synapse pairs were more than 40 um apart. A whole-connection (cell-pair) factor fits this result better than a local dendritic-branch factor.

**4. Co-tuned pairs have slightly larger synapses, but the shared component does not follow co-tuning (Figure 3).** We used the Ding et al. (2025) functional node data. Signal correlation is the correlation of model (in silico) responses to natural movies. A second measure uses in vivo trial-mean responses. Mean connection size increased with signal correlation after fixed effects for both cells. The slope was 0.58 (0.51 to 0.64) standard deviations per unit correlation for proofread axons (71,226 connections). It was 0.22 (0.18 to 0.25) for all axons (316,822 connections). This replicates the like-to-like size result of Ding et al. But signal correlation explains only 0.0038 of the size variance. That is about 2% of the connection-specific component (0.17 to 0.32). For proofread E-to-E multi-synapse connections between functionally measured cells (3,815 connections; about 480 to 490 axons in each third), the component was 0.31, 0.25 and 0.33 in the low, middle and high thirds of signal correlation. The slope per standard deviation of signal correlation was 0.008 (-0.035 to 0.051) in silico and -0.041 (-0.092 to 0.007) in vivo. The in-silico and in-vivo signal correlations correlate at r = 0.46 across connections, so measurement noise attenuates any true slope. If we divide the in-silico upper bound (0.051) by 0.46 as a rough correction for this noise, the slope is still at most about 0.11 per standard deviation. This is small relative to a component of about 0.3.

**5. A two-state (binary) model does not isolate the shared component in cleft size.** A two-component Gaussian mixture fitted the size distribution better than one component in every class pair, including inhibitory ones. For E-to-E connections, both the state probability (0.170, 0.142 to 0.199) and the within-state residual (0.132, 0.106 to 0.160) had a shared component. Thus, with cleft size and this simple split, we did not reproduce the result of Dorkenwald et al. (2022) that only the binary part is shared. That study used spine-head volume in a smaller volume. This test is weak: the two parts come from one variable, and the mixture is not specific to excitatory synapses.

## Checks

- Proofreading matters. With functionally measured cells and unproofread axons, the component was only 0.05 to 0.07 for 23P and 4P axons. With proofread axons it was 0.24 to 0.43. Merge errors in unproofread axons add false connections and dilute the component. The main analysis uses proofread axons only.
- About 48% of within-connection pairs had all three distance-matched controls. The raw within-connection product was 0.263 (0.237 to 0.293) in matched pairs and 0.280 (0.261 to 0.299) in unmatched pairs. Thus, the match did not select a special subset.
- When we removed synapses within 15 um or 30 um of the postsynaptic soma, the E-to-E estimate did not change (0.173, 0.174, 0.175).
- The component was 0.184 (0.154 to 0.213) for 2-synapse connections, 0.159 (0.122 to 0.203) for 3-4 synapses and 0.069 (0.034 to 0.111) for 5 or more synapses (1,044 connections). We did not explain the lower value for large connections.

## Limitations

- One mouse and one EM volume. We did not test a second animal (for example V1 Deep Dive) with the same estimator.
- Cleft voxel count is a proxy for synaptic strength. We had no spine/shaft label. Part of the E-to-E component can come from connections whose synapses all target spines or all target shafts, beyond the axon and target-cell averages.
- Proofread axons are a selected subset. Deep-layer axons had fewer proofread cells (for example 61 5P-ET axons), so their intervals are wider. The 23P and 4P versus deep-layer contrast is clear in pooled data but not in every single cell of the type-by-type table.
- Root identifiers in release v1300 were joined to v1507 proofreading and cell-type tables through nucleus identifiers. Some proofreading took place after v1300, so some "proofread" axons may still carry errors in the v1300 synapse table. This error would reduce, not create, the component.
- The double difference assumes additive effects in standardised log size. Interactions between axon and target cell beyond cell class are, by design, part of the "connection" term. The term therefore means "specific to this cell pair", not "caused by plasticity".
- Signal correlation from a model and from 120 trial means is a noisy measure of co-activity history. Other activity measures (noise correlation, behaviour-locked activity) were not tested.

## What is new

The campaign had one uncertain test of dual-connection size agreement (sci:27b63e3c, 57 matched sets, V1 Deep Dive) and an uncertain size-balance versus response test (sci:ba1aabb2, 177 multi-contact connections). Here, with 35,424 proofread E-to-E multi-synapse connections (18,441 with all matched controls) and a validated estimator that removes axon, target and location terms, the shared component is clear for E-to-E connections. It is absent at E-to-I and I-to-E connections. It is strong only for layer 2/3 and layer 4 axons. It does not decay over hundreds of micrometres, and it is independent of visual co-tuning. A Hebbian rule driven by stimulus-response similarity therefore cannot explain most of it.

## Open questions for the next study

- Repeat the estimator in the V1 Deep Dive mouse and in H01 human cortex (the H01 synapse export is about 33 GB of Avro files at gs://h01-release/data/20210601/c3/synapses/exported/).
- Add spine/shaft labels (MICrONS synapse target predictions) to remove the compartment term.
- Test other activity measures (noise correlation, spontaneous co-activity) as predictors of the component.
- Explain why deep-layer axons and connections with five or more synapses show less sharing.

## Files

- `files/figures/` three PNG figures.
- `files/results/summary_proofread_pre.csv` all class pairs: raw product, the three control products, T and intervals.
- `files/results/mech_summary.json` distance bins, presynaptic types, soma exclusion and binary/analog tests.
- `files/results/pretype_by_posttype_proofread_EE.csv` presynaptic type by target type.
- `files/results/func_fe_*.json`, `func_tertiles*.csv` functional tests.
- `files/results/checks.json` matching and synapse-count checks; `all_synapse_log10size_hist.csv` size histogram of all 337,312,429 synapses.
- `files/code/` all analysis code (steps s1 to s11, estimator in `ddlib.py`), `retrieve_data.sh` and `run_all.sh`.
- `files/NOTICE_EXTERNAL_DATA.md` source URLs, SHA-256 hashes, licences and attribution.

## Reproduction

1. `bash files/code/retrieve_data.sh /scratch/dir` downloads the five public source files (about 24 GB) into separate scratch and checks the SHA-256 hashes. On the campaign machine, the same files are in the shared store (see the notice).
2. `cd /scratch/dir && bash /path/to/files/code/run_all.sh /path/to/files/code` runs all steps. This takes about 2 hours on 2 CPUs. The bootstrap and matching seeds are fixed.

## Provenance

Job sci-1107-dell-neural-structure-and-computation-9793c4b16b6d, topic neural-structure-and-computation, campaign 11_07_2026, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim. Analysis date 2026-11-12. Python 3.12 with numpy, pandas, pyarrow, scipy, scikit-learn and matplotlib.
