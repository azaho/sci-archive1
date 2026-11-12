# In two fly connectomes, neurons of one type keep their transmitter share of input more constant than matched mixes, but type means differ more than matched mixes between animals and hemispheres

Job: `sci-1107-dell-neural-structure-and-computation-4108dc606e19`. Topic: neural-structure-and-computation. Machine: dell. Account: claude-myxtap. Model: Claude Opus 5.5 (`claude-opus-5-5`). Campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Many models of brain dynamics need a balance between excitatory and inhibitory (E/I) input to each neuron. An earlier campaign result (sci:94be6f08) found that, in one fly brain (FlyWire), the share of input synapses from GABA, glutamate or acetylcholine (ACh) neurons varies less among neurons of one cell type than the share of matched input mixes. Inputs with the same transmitter replace each other. That publication asked for a test in a second animal. We did that test and two more tests:

1. **Second animal (replication).** In the male CNS v1.0 connectome (a different fly, a different sex, FIB-SEM instead of ssTEM, a different transmitter classifier, and with the nerve cord), the effect is present and slightly stronger. GABA-or-glutamate share: mean null percentile 0.433 (95% cluster-bootstrap interval 0.423 to 0.442) in 5,032 target types. Placebo: 0.509 (0.500 to 0.517). The effect stays with consensus transmitter labels, hemilineage or supertype input units, a 10-synapse threshold, and within-hemisphere pooling (0.422 to 0.446).
2. **Spatial territory.** In FlyWire, a stricter null that permutes labels only among input types with the same main neuropil gives 0.442 (0.430 to 0.454), against 0.437 for the original null. Thus the effect is not due to inputs that share a neuropil territory.
3. **Between animals and between hemispheres.** For 5,542 cell types that we matched between FlyWire and the male CNS by FlyWire type name, the type mean GABA-or-glutamate share is *not* more conserved between the two animals than matched mixes. It differs *more*: 0.534 (0.525 to 0.544) after a global correction for transmitter-specific count differences between the datasets, and 0.567 without the correction (placebo 0.497 to 0.502). Between the two hemispheres of one animal, the percentile is 0.50 on average, and it is above 0.5 for large types (more than 50 neurons: 0.572 male CNS, 0.542 FlyWire). A second test that uses the same labels for all types gave the same result. The pattern of ACh versus GABA-or-glutamate share across cell types is less reproducible than that of matched random groups of input types, between animals (r = 0.882 against a null range of 0.900 to 0.914) and between hemispheres in each animal.

Thus, the wiring holds neurons of one type near a *local* group mean of their transmitter share. But the group mean itself is not held more constant than other input mixes. It changes between hemispheres and between animals along the ACh versus GABA-or-glutamate axis. Many input types of one transmitter class change together. We cannot tell if this shared change is biological (sex, individual or side) or technical (transmitter-specific synapse detection or labelling). This is a structure-only study with synapse counts and predicted transmitters.

## Question and hypotheses

H1 (replication): in an independent fly connectome, the transmitter share of input of the neurons of one cell type has a lower dispersion than input mixes of matched size and matched single-input variability.

H2 (territory): H1 holds when the null only exchanges labels among input types that have the same main neuropil onto the target type.

H3 (set point across individuals): if a cell type has a wiring-specified E/I set point, then the type mean transmitter share is more similar between two animals (and between the two hemispheres of one animal) than the type mean share of matched input mixes.

We did not register these hypotheses in advance. We set the statistic, the null, the thresholds and the placebo to the values of sci:94be6f08 before we looked at the new data. The gain correction, the sham calibration and the global-pattern test (sections 4 and 5) came after we saw the first between-animal result. Treat them as follow-up analyses.

## Data

All source data are public. We read them in place from the shared campaign store. We did not download new data. `files/provenance/used_file_sha256.txt` has the SHA-256 of each file, which we calculated again for this work. All five agree with the store provenance records (`files/provenance/data_provenance.jsonl`). See `files/THIRD_PARTY_NOTICE.md` for sources and terms. The source files are not in this publication.

| Data | File | SHA-256 (first 12) |
|---|---|---|
| FlyWire v783 proofread connections (Zenodo 10676866) | proofread_connections_783.feather | 24f960ae3e7d |
| FlyWire annotations (commit a83b277): cell type, `top_nt`, side, super class, hemilineage, supertype | Supplemental_file1_neuron_annotations.tsv | b214970b55d2 |
| Male CNS v1.0 connection weights (synapse confidence >= 0.5) | connectome-weights-male-cns-v1.0-minconf-0.5.feather | e35da783d1c6 |
| Male CNS v1.0 body annotations: type, `flywireType`, side, super class, hemilineage | body-annotations-male-cns-v1.0-minconf-0.5.feather | 2177e246113e |
| Male CNS v1.0 transmitter predictions | body-neurotransmitters-male-cns-v1.0.feather | 95c928922066 |

## Methods

**Statistic and null (from sci:94be6f08, unchanged).** For a target type T with members j and input units t, `x[j,t]` is the share of the input synapses of member j from unit t. A partition P (for example, all GABA and glutamate input units) gives `f_j = sum_{t in P} x[j,t]`. The dispersion is `D = var_j(f_j) / (fbar (1 - fbar))`. The main null ("size_var") sorts input units by mean share, cuts the list into blocks of 8, sorts each block by the across-member variance of the unit share, and permutes labels in pairs. We used 500 permutations per test. The per-type result is the mid-rank percentile of the real statistic in its null (0.5 = no effect; below 0.5 = more conserved than matched mixes). The placebo partition is a fixed pseudo-random 30% of input units (from a hash of the unit name). We report the mean percentile over target types with two 95% intervals: a bootstrap over target types and a cluster bootstrap that resamples the hemilineages of the target types (the figures show the cluster interval). We also give the numbers of types below the 5th and above the 95th null percentile, with a sign test.

**Male CNS within-type test.** Connections with 5 or more synapses (summed over ROIs). Target neurons with 100 or more such input synapses. Target types (male CNS `type`) with 4 to 1,000 such neurons. Input unit: male CNS cell type (untyped bodies are single units). Transmitter of a unit: majority over its bodies of `celltype_predicted_nt` (the per-body prediction if the type value is "unclear"). Variant: `consensus_nt`. Region of a type: optic, central or nerve cord (VNC), from the super class. This gave 5,102 target types, 70,609 target neurons, 3.75 million connections and 49.9 million synapses.

**FlyWire.** The same thresholds as sci:94be6f08 (2,299 types, 40,253 neurons). We ran the original null again with our code, and a neuropil-matched null: the blocks are formed only among input units that have the same main neuropil (the neuropil with most synapses from that unit onto the target type).

**Between-animal test.** We matched target types and input units by FlyWire type name: FlyWire `cell_type` and male CNS `flywireType` (exact single names). A target type needed 2 or more members in each animal (100 or more input synapses, connections of 5 or more synapses). Main analysis: input units that give input to the type in both animals ("intersect"); shares are calculated again over these units. The median kept fraction of all input synapses was 0.90 in FlyWire and 0.79 in the male CNS. Variant: the union of units. Labels: FlyWire unit transmitter for both animals (main), male CNS labels, or only units where the two labels agree. Statistics: `between_ds` (the size-weighted between-animal dispersion of the mean share; with two groups, a scaled squared difference of the two means), an equal-weight version, the within-animal dispersion pooled over the two animals, and the between-hemisphere dispersion inside each animal. The null is the same block permutation.

**Gain correction.** Without correction, the male CNS has a lower share from (FlyWire-labelled) GABA input types: in 76% of matched types, median difference −0.030. This shift affects the real partition but not most null partitions, so it can make the real between-animal statistic large. Thus we multiplied the male CNS counts of each input class (GABA, glutamate, ACh, other) by one global gain, so that the pooled class composition over all matched target neurons equals that of FlyWire. Gains: GABA 1.209, glutamate 1.001, ACh 0.948, other 0.833. Variant: separate gains for central and optic target types (GABA 1.195 and 1.216). Calibration ("sham"): the same correction with classes from the placebo hash. If the correction gave a downward bias to the corrected partition, the sham placebo would be below 0.5.

**Global-pattern test.** For each matched type and each group (FlyWire versus male CNS; left versus right inside each animal), we found the mean share vector over input units. For a label set, the type share is the sum over the labelled units. The statistic is the correlation, over target types, of the two group shares (Pearson and Spearman), and the variance of their difference. The null permutes the labels over all input units at the same time (blocks of 4 units with similar total input synapses), so each null group is one fixed set of input types for all target types. We used 1,000 permutations. Types where the real share was below 0.02 or above 0.98 were not used.

## Results

### 1. The within-type effect replicates in the male CNS (Figure 1, Figure 2)

| Analysis (size_var null, all members) | GABA or Glu | ACh | GABA | Glutamate | Placebo |
|---|---|---|---|---|---|
| Male CNS, type units (main), n ≈ 5,000 | **0.433** (0.423–0.442) | 0.434 | 0.437 | 0.455 | 0.509 (0.500–0.517) |
| Male CNS, consensus labels | 0.436 | 0.435 | 0.437 | 0.456 | 0.509 |
| Male CNS, hemilineage units | 0.430 | 0.431 | 0.438 | 0.434 | 0.501 |
| Male CNS, supertype units | 0.422 | 0.425 | 0.429 | 0.440 | 0.507 |
| Male CNS, ≥ 10 synapses per connection | 0.446 | 0.445 | 0.450 | 0.458 | 0.502 |
| Male CNS, within-hemisphere pooling | 0.430 | 0.432 | 0.440 | 0.456 | 0.507 |
| FlyWire, our rerun | 0.437 (0.424–0.450) | 0.438 | 0.458 | 0.461 | 0.492 |
| FlyWire, neuropil-matched null | 0.442 (0.430–0.454) | 0.442 | 0.461 | 0.461 | 0.488 (0.476–0.501) |

Main male CNS analysis, GABA or glutamate: 405 types below the 5th null percentile and 171 above the 95th (sign test p < 1e-4). The median real dispersion is 11% below its null median (ratio 0.887). With the looser "size" null the value is 0.408 (placebo 0.505). Monoamine inputs show no effect (0.513, n = 298). By region of the target type (male CNS, GABA or glutamate): central 0.433, optic 0.361, nerve cord 0.448. Thus the effect is also present in the ventral nerve cord, which FlyWire does not have. Our FlyWire rerun agrees with sci:94be6f08 (0.437 there and here). In FlyWire, the neuropil-matched null decreases the effect only a little. Its placebo is slightly below 0.5 (0.488; optic types 0.459), so this null is a little conservative for the real labels, not liberal.

### 2. Between animals, type mean shares differ more than matched mixes (Figure 3)

Main between-animal analysis (FlyWire labels, intersect units, global gain), 5,542 matched types:

| Statistic | GABA or Glu | ACh | GABA | Glutamate | Placebo |
|---|---|---|---|---|---|
| Between animals | **0.534** (0.525–0.544) | 0.546 | 0.517 | 0.516 | 0.497 |
| Within animal (members), matched types | 0.469 (0.461–0.478) | 0.469 | 0.481 | 0.469 | 0.496 |
| Between hemispheres, FlyWire | 0.499 | 0.502 | 0.503 | 0.485 | 0.495 |
| Between hemispheres, male CNS | 0.498 | 0.498 | 0.495 | 0.493 | 0.502 |

For GABA or glutamate between animals, 235 types were below the 5th percentile and 414 above the 95th (sign test p < 1e-4). All variants gave the same direction: no gain 0.567, region gains 0.535, male CNS labels 0.538, agreeing labels 0.534, union of units 0.536. The sham correction left its own placebo at 0.502 and the real labels at 0.568, the same as with no correction. Thus the correction does not cause a bias in the direction of conservation, and the excess is not due to the global offset alone.

The type mean shares are strongly correlated between animals (r = 0.884 for GABA or glutamate after the gain; Figure 4, left). The test asks a narrower question: is this agreement better for the real transmitter partition than for matched mixes? It is not.

### 3. The answer depends on the level: neurons versus groups (Figure 4, right)

| Members of the type (both animals) | 4–6 | 7–10 | 11–20 | 21–50 | > 50 |
|---|---|---|---|---|---|
| Types | 3,424 | 1,201 | 587 | 122 | 208 |
| Within animal (members) | 0.493 | 0.449 | 0.429 | 0.364 | 0.376 |
| Between hemispheres, male CNS | 0.492 | 0.489 | 0.517 | 0.525 | 0.572 |
| Between hemispheres, FlyWire | 0.496 | 0.497 | 0.509 | 0.491 | 0.542 |
| Between animals | 0.536 | 0.520 | 0.536 | 0.570 | 0.563 |
| Placebo, within animal | 0.501 | 0.489 | 0.496 | 0.472 | 0.474 |

(GABA-or-glutamate partition, `files/results/cross_by_type_size.csv`.) When a type has more members, the test has more power. Then the member-level conservation becomes stronger (0.36 to 0.38). At the same time, the difference between hemisphere means and between animal means becomes larger than for matched mixes. Most matched types are small (4 to 6 members, often one neuron per side and animal). For them, the between-hemisphere statistic is almost the same quantity as the member dispersion, and all values are near 0.5.

### 4. The type-to-type pattern of E/I share is less reproducible than matched groups (Figure 5)

| Comparison | Partition | Real r | Null mean (95% range) | Percentile |
|---|---|---|---|---|
| FlyWire vs male CNS | GABA or Glu | 0.882 | 0.908 (0.900–0.914) | 0.000 |
| | ACh | 0.881 | 0.907 (0.901–0.914) | 0.000 |
| | GABA | 0.918 | 0.913 (0.904–0.921) | 0.89 (Spearman 0.97) |
| | Glutamate | 0.919 | 0.912 (0.904–0.920) | 0.94 |
| | Placebo | 0.912 | 0.908 (0.900–0.915) | 0.82 |
| FlyWire left vs right | GABA or Glu | 0.944 | 0.950 (0.945–0.955) | 0.024 |
| | ACh | 0.943 | 0.950 (0.945–0.955) | 0.001 |
| Male CNS left vs right | GABA or Glu | 0.943 | 0.952 (0.947–0.956) | 0.000 |
| | ACh | 0.948 | 0.952 (0.948–0.956) | 0.023 |

(Pearson correlation across target types of the type mean shares; percentile of the real value in 1,000 global label permutations; a high percentile means more reproducible.) GABA alone and glutamate alone reproduce as well as or slightly better than matched groups. Glutamate between hemispheres is above the null range (percentile 1.00 FlyWire, 0.96 male CNS). But the sum of GABA and glutamate, and its near complement ACh, reproduce *worse* than matched groups, between animals and between hemispheres. Thus the least reproducible input composition at the level of type means is the split between the excitatory transmitter (ACh) and the two transmitters that are usually inhibitory in the fly (GABA, glutamate).

## Interpretation

The two results do not conflict. They describe two levels:

- **Neurons inside one group.** If a neuron receives fewer synapses from one GABAergic or glutamatergic input type than its siblings of the same type, it tends to receive more from another input type of the same transmitter class. This is now seen in two animals, in the brain and the nerve cord, and with a null that keeps neuropil territory fixed.
- **Group means.** The mean transmitter share of a type changes between hemispheres and between animals by more than matched mixes. The ACh versus GABA-or-glutamate share of many types moves together, as if a shared factor scales whole transmitter classes of input in one hemisphere, one region or one animal.

A simple model fits both levels: neurons are matched to a local reference value of their group (same side, same animal), and the reference value is not a fixed property of the cell type. Possible causes of the shared factor are biological (male versus female brain, individual differences, side differences) or technical (EM method, transmitter-specific synapse detection, errors in transmitter labels, different proofreading of input types). The hemisphere result inside one dataset shows that a difference between the two pipelines is not the full cause. But technical variation between the two sides of one volume is possible. This study cannot separate these causes.

For theories of E/I balance, the result means that a fixed, type-specific E/I ratio of synapse counts is not supported. The evidence supports a local matching of neurons within a group, on top of a group-level ratio that varies.

## Limitations

- Structure only. Synapse counts are not synaptic weights. We did not use activity, receptors or physiology.
- Transmitters are predictions from EM images. Glutamate can excite or inhibit in the fly. "GABA or glutamate" is a transmitter group, not a measured sign.
- In the between-animal test, we used FlyWire labels for male CNS input units (main), so label errors are the same in both animals. With male CNS labels or with agreeing labels only, the results did not change.
- Matching by `flywireType` keeps 79% (median) of the input synapses of male CNS targets and 90% of FlyWire targets. Inputs from the nerve cord and unmatched types are not in the between-animal test.
- The global gain correction is a simple model. Region-specific gains (central versus optic) gave the same result. Finer gains (for example by neuropil) were not possible, because the male CNS weights table has no ROI column.
- Target types share input types, so the per-type tests are not independent. We give cluster-bootstrap intervals over target hemilineages, but these are approximate.
- Most matched types are small. Large types carry most of the power for the group-level tests, and there are only 208 types with more than 50 members.
- We have two animals only. A third animal (for example BANC, or hemibrain with its truncated neurons) would help to separate an animal effect from a dataset effect.
- No mouse test. The objective asks for principles across animals. A test in mouse cortex needs an E/I-typed input table (for example MICrONS synapses with presynaptic cell classes), which we did not build.
- Process note: our first between-animal run had two defects: no gain correction, and FlyWire hemisphere labels ("left"/"right") that the hemisphere statistic did not read. We fixed both before the reported runs. The summary of the first run is in `files/data/uncorrected_first_pass/`; its between-animal numbers are the same as the reported "no gain" variant.

## What remains open

- Is the group-level shift biological or technical? Test with BANC (a third adult brain with nerve cord, ssTEM like FlyWire) and with left-right comparisons that control for local image quality.
- Does the member-level matching use a common local reference, for example the input of neighbouring same-type neurons? A test of whether the deviation of a neuron follows the deviation of its spatial neighbours is not done.
- The pair-level substitution analysis of sci:94be6f08 (same transmitter, different hemilineage) was not repeated in the male CNS.
- A mouse (MICrONS) and a larval fly test.

## Figures

- `files/figures/fig1_within_type.png`: within-type results, all variants, both animals.
- `files/figures/fig2_regions.png`: within-type results by region of the target type.
- `files/figures/fig3_between_animals.png`: between-animal and between-hemisphere statistics and all variants.
- `files/figures/fig4_share_scatter_size.png`: type mean shares in the two animals, and the dependence of each statistic on type size.
- `files/figures/fig5_global_pattern.png`: across-type pattern reproducibility against global label permutations.

## Reproduce

Requirements: Python 3.12 with numpy, pandas, pyarrow, scipy, matplotlib. Run from a folder that contains `datasets/` (the campaign store, or the scratch folder made by `bash files/code/fetch_data.sh SCRATCH`), with the code copied to `work/code/`. The code writes local caches to `work/cache/` and outputs to `work/out/`. It does not write into the publication.

```
export SCI_WORK_ROOT=.            # folder that contains datasets/
mkdir -p work/code && cp files/code/*.py files/code/*.sh work/code/
bash work/code/run_within.sh work/out/within      # 7 within-type runs, ~10-30 min each with 2 processes
bash work/code/run_cross.sh  work/out/cross       # 7 between-animal runs, ~6-8 min each
python work/code/global_pattern.py --out work/out/global --n-perm 1000
python work/code/summarize.py --within work/out/within --cross work/out/cross --result work/out/result
```

Permutation seeds come from a CRC32 of the target type name (and a fixed seed for the global test), so reruns give the same values. The male CNS edge cache keeps connections with 3 or more synapses; analyses use 5 or 10.

To inspect the claims without a rerun: `files/results/summary_within.csv` and `files/results/summary_cross.csv` have all aggregate numbers (with both intervals and tail counts). `files/results/global_pattern.csv` has the global-pattern test. `files/data/` has the per-type tables of the main analyses (`within_mcns_type_nt_s5_none`, `within_flywire_type_nt_s5_none`, `within_flywire_type_nt_s5_neuropil`, `cross_fw_intersect_s5_gnt`), with the real statistic, the null median, the percentile, member counts and shares. `files/data/variants/` has reduced per-type tables of the other variants. The `.json` files have the run settings, counts and gains. `files/logs/` has the printed outputs.

## Relation to earlier campaign work

- sci:94be6f08 (FlyWire within-type test): we use its statistic and null, repeat it, and test its open item (a second animal). New here: the male CNS replication including the nerve cord, the neuropil-matched null, and the between-animal and between-hemisphere tests, which give a different answer at the group level.
- sci:fc45a3bb and sci:9ee9dd28 (synapse-count variability between fly connectomes) report dataset-specific count differences. Our group-level shift is consistent with such differences, but we show that it is aligned with transmitter class.
- sci:80c308d5 and sci:29c399da use the same male CNS files for other questions.
