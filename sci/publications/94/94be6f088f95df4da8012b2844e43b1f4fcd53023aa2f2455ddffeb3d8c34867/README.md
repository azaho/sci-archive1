# In the FlyWire fly brain, the transmitter share of neuron input varied less among neurons of one cell type than matched input mixes; eight worm brains gave no clear result

Job: `sci-1107-hp-neural-structure-and-computation-a6faec00cd67`. Topic: neural-structure-and-computation. Machine: hp. Account: claude-olen. Model: Claude Opus 5.5 (`claude-opus-5-5`). Campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Many theories of brain dynamics need a balance between excitatory and inhibitory input to each neuron. Can wiring alone set part of this balance? If it can, the fraction of input that comes from each transmitter must stay more constant among neurons of the same cell type than other fractions of their input.

We tested this hypothesis:

> Among neurons of one cell type, the share of input synapses from GABA, glutamate or acetylcholine (ACh) neurons varies less than the share of an input mix that has the same size and the same single-input variability but no common transmitter.

This is a structure test. It does not use activity data. It asks if the connectome has a "balance template" beyond the general stereotypy of cell-type wiring.

## Data

All data are public. We read them in place from the shared campaign store. `files/provenance/` has the source URLs, the shared paths and the SHA-256 of each file that we used. All hashes agree with the store provenance records.

| Data | Source | SHA-256 (first 16) |
|---|---|---|
| FlyWire v783 proofread connections (per neuropil) | Zenodo 10676866, `proofread_connections_783.feather` | `24f960ae3e7d4f8c` |
| FlyWire neuron annotations (cell type, `top_nt`, side, hemilineage, supertype) | github flyconnectome/flywire_annotations @ `a83b277`, Supplemental file 1 | `b214970b55d2fbe0` |
| Witvliet et al. 2021, 8 worm brains (L1 to adult), synapse lists | github dwitvliet/nature2021 @ `0646af9` | see `used_file_sha256.txt` |
| Wang et al. 2024 worm transmitter atlas, Supplementary File 2 | github openworm/ConnectomeToolbox @ `ffe5702` (eLife 95402) | `0013e4b5f366b82a` |

Shared paths: `datasets/fly-flywire-connections-783-zenodo10676866`, `datasets/flywire-annotations-sf1-a83b277` (we added this one with the campaign dataset helper), `datasets/witvliet2021-primary-synapses-{1..8}-0646af9`, `datasets/worm-wang2024-ntatlas-supp2-ffe5702` (we added this one).

## Method

**Inputs.** Fly: we added the synapse counts of each pre/post neuron pair over neuropils. We kept pairs with 5 or more synapses (the FlyWire convention). A target neuron needed 100 or more input synapses. A target cell type needed 4 to 1,000 such neurons. This gave 2,299 target types, 40,253 target neurons, 1.39 million connections and 15.9 million synapses. Each input neuron got the majority `top_nt` label of its cell type (Eckstein et al. 2024 predictions). The labels were ACh, GABA, glutamate, dopamine, serotonin and octopamine. Worm: each synapse added one count to each of its postsynaptic partners. Members of a class were its left/right and other symmetric neurons in all 8 animals. A member needed 20 or more input synapses. Input units were neuron classes. The label was the first transmitter in Wang et al. 2024. This gave 35 testable nerve-ring classes.

**Statistic.** For target type T, `x[j,t]` is the share of the input of member j that comes from input type t. A partition P (for example, all GABA input types) gives `f_j = sum over t in P of x[j,t]`. The dispersion is `D = var_j(f_j) / (fbar (1 - fbar))`.

**Null.** We kept the input matrix and moved the transmitter labels among input types. Two nulls:

- `size`: we sorted input types by mean share and permuted labels in blocks of 4.
- `size_var` (main, stricter): we cut the sorted list into blocks of 8, sorted each block by the across-member variance of the share of each input type, and permuted labels in pairs. Thus each permutation keeps the number of labelled types. It also keeps, approximately, the labelled share and the sum of the single-type variances. A low real D then means that same-transmitter inputs covary more negatively (they replace each other) than matched inputs.

We used 1,000 permutations per test in the fly and 2,000 in the worm. The per-type result is the mid-rank percentile of the real D in the null. With no effect, percentiles are uniform (mean 0.5). We report the mean percentile with a 95% bootstrap interval over target types. We also give the counts of types below the 5th and above the 95th null percentile, with a sign test on these two counts.

**Calibration and controls.**

- Placebo partition: a fixed pseudo-random 30% of input types, from a hash of the type name.
- Pooled within-hemisphere (fly) or within-animal (worm) variance.
- Input units at three levels: cell type, supertype, and Ito-Lee hemilineage. Hemilineages in the fly mostly use one transmitter (median purity 0.98 in these annotations). The hemilineage level therefore tests if related "sibling" input types that replace each other cause the effect.
- A neuron-level transmitter-confidence cut (`top_nt_conf >= 0.5`).
- A stricter 10-synapse connection threshold.

**Pair analysis.** For the 566 target types with 8 or more members, we took up to 40 fast-transmitter input types with 1% or more mean share. We correlated their shares (and, separately, log-count residuals after removal of log total input) across members. We then compared pairs with the same transmitter against pairs with different transmitters in the same target type.

## Results

**1. In the fly, transmitter shares were more conserved than matched input mixes (Figure 1, Figure 2).** Main analysis (type units, `size_var` null, all members):

| Partition | Types | Mean percentile (95% CI) | Below 5% / above 95% | Sign test p | Median D ratio, real/null |
|---|---|---|---|---|---|
| GABA or glutamate | 2,252 | 0.437 (0.425–0.449) | 172 / 79 | <1e-4 | 0.91 |
| ACh | 2,251 | 0.438 (0.425–0.450) | 167 / 79 | <1e-4 | 0.91 |
| GABA | 2,020 | 0.457 (0.445–0.469) | 126 / 80 | 0.002 | 0.95 |
| Glutamate | 1,947 | 0.462 (0.449–0.474) | 105 / 58 | 3e-4 | 0.96 |
| Monoamine | 140 | 0.507 (0.461–0.556) | 4 / 5 | 1.0 | 1.00 |
| Placebo | 2,194 | 0.493 (0.481–0.505) | 121 / 117 | 0.85 | 1.00 |

The placebo is near 0.5 in all fly analyses (0.49–0.52). Thus the test is calibrated. The effect is small: the median type has a real dispersion about 9% below its null median. But the effect is consistent. For GABA or glutamate, the mean percentile stayed below 0.5 in all fly variants:

| Fly variant (`size_var` unless noted) | GABA or Glu | GABA | Glutamate | Placebo |
|---|---|---|---|---|
| Type units, within-hemisphere variance | 0.436 | 0.456 | 0.470 | 0.498 |
| Type units, `size` null | 0.421 | 0.441 | 0.451 | 0.489 |
| Supertype units | 0.425 | 0.446 | 0.439 | 0.501 |
| Type units, targets with ≥50% hemilineage-labelled input (n≈1,380) | 0.434 | 0.462 | 0.465 | 0.498 |
| Hemilineage units, same targets (n≈1,320) | 0.437 | 0.451 | 0.447 | 0.517 |
| Transmitter confidence ≥ 0.5 | 0.454 | 0.459 | 0.475 | 0.493 |
| ≥ 10 synapses per connection (1,694 types) | 0.457 | 0.469 | 0.457 | 0.491 |

All 95% intervals for GABA or glutamate exclude 0.5. Two results are weaker. In the 10-synapse variant, GABA alone gives 0.469 (0.453–0.484), and the sign test on its tails gives p = 0.14. With the confidence cut, glutamate alone gives 0.475 (0.462–0.489), and the tail test gives p = 0.08. When all input types of a hemilineage get one label and move as one unit, the effect does not decrease. Thus sibling types from one lineage that replace each other do not cause it. By target super-class (main analysis, GABA or glutamate): central 0.440 (0.427–0.453, n = 1,834), optic 0.414 (0.370–0.458, n = 183), visual projection 0.439 (0.388–0.491, n = 132), descending 0.416 (0.325–0.507, n = 48). See `results/summary_fly_by_superclass.csv`.

**2. Same-transmitter inputs from different lineages replaced each other (Figure 3).** Per target type, we found the mean correlation of same-transmitter pairs minus that of different-transmitter pairs:

- Same transmitter, different hemilineage (340 types): −0.034 (95% CI −0.054 to −0.015) for log-count residuals; −0.028 (−0.047 to −0.008) for shares.
- Same transmitter, at least one input without a lineage label (517 types): −0.019 (−0.029 to −0.008).
- Same transmitter, same hemilineage (360 types): +0.029 (0.001 to 0.058). Sibling inputs co-vary. They do not replace each other.

Thus the conserved transmitter share comes from negative covariance between inputs that have the same transmitter but come from different lineages. The pair correlations are small. The effect is a weak tendency, not a strict rule.

**3. Worm: no clear result.** For the 35 nerve-ring classes in 8 Witvliet brains, the mean percentiles were: GABA or glutamate 0.480 (0.389–0.570), glutamate 0.504 (0.412–0.597), ACh 0.488 (0.390–0.586), GABA 0.369 (0.201–0.555, only 6 classes). The placebo was 0.548 (0.436–0.653) for all members and 0.649 (0.545–0.746) for within-animal pooling. Thus the worm test is small and not well calibrated. It neither supports nor rejects the fly result. Worm classes have few input classes. Thus few label permutations are possible, and many null values are equal to the real value.

## Interpretation

In one adult fly brain, the wiring holds the transmitter composition of the input of a neuron closer to its cell-type value than other input compositions of equal size and variability. If a neuron of a type gets less input from one GABAergic or glutamatergic input type, it tends to get more from another input type with the same transmitter but a different lineage. The same is true for ACh. This is a structural candidate for the regulation of excitation and inhibition at the level of synapse counts. But it is weak (about 9% lower dispersion at the median). Most of the input variability among neurons of a type has no relation to transmitter.

## Limitations

- Structure only. We did not test activity, synaptic strength, receptor type or dynamics. Synapse counts are not synaptic weights.
- Fly transmitter labels are EM-based predictions with errors. Glutamate in the fly can excite or inhibit. Thus "GABA or glutamate" is a transmitter group, not a measured sign. Results for ACh and for GABA or glutamate are nearly complementary tests, because these groups contain almost all fast input.
- One fly brain. The variation is among neurons of a type in one animal (both hemispheres). We did not do a replication across animals (for example, hemibrain or male CNS).
- Target types share input types. Thus the per-type tests are not independent, and the bootstrap intervals and sign tests are approximate.
- The block-permutation nulls match share and single-type variance only approximately. They do not match other properties, for example neuropil location or input neuron size.
- Types with more than 1,000 members (for example, the largest Kenyon cell and optic columnar types) and neurons with fewer than 100 input synapses are not in the test.
- The worm analysis has low power and a placebo that is not well calibrated. We did not test mouse data, because a public E/I-typed input table at the needed scale was not available in the shared store.
- First pass of the pair analysis: a NaN-handling defect put pairs without a lineage label into the "different hemilineage" group. We corrected the defect before we made the reported numbers. The worm labels with a leading "*" in Wang et al. 2024 were also corrected before the reported run.

## Reproduce

Requirements: Python 3.12 with numpy, pandas, pyarrow, scipy, matplotlib, openpyxl. The campaign shared datasets must be at `./datasets`. The run time was about 15–45 minutes per fly run with 8 processes on a loaded machine. Peak memory was about 2.3 GB.

```
export SCI_WORK_ROOT=.            # folder that contains datasets/
python3 files/code/fly_composition.py --out work/out/fly --unit type        --n-perm 1000 --max-members 1000
python3 files/code/fly_composition.py --out work/out/fly --unit hemilineage --n-perm 1000 --max-members 1000
python3 files/code/fly_composition.py --out work/out/fly --unit supertype   --n-perm 1000 --max-members 1000
python3 files/code/fly_composition.py --out work/out/fly_ntconf05 --unit type --nt-conf 0.5 --n-perm 1000 --max-members 1000
python3 files/code/fly_composition.py --out work/out/fly_minsyn10 --unit type --min-syn 10 --n-perm 1000 --max-members 1000
python3 files/code/fly_pair_substitution.py --out work/out/fly_pairs
python3 files/code/worm_composition.py --out work/out/worm --n-perm 2000
python3 files/code/summarize.py --out-dir work/out --result-dir files
```

Permutation seeds come from a CRC32 of the target type name. Thus reruns give the same values. To inspect the claims without a rerun, use the per-type tables in `files/data/` (gzip CSV, one row per target type × partition × null × pooling). They have the real D, the null median and mean, the percentile, the share, the number of members and input types, and the super-class. `files/results/summary_by_analysis.csv` has all aggregate numbers. `files/logs/` has the printed outputs.

Files:

- `files/code/common.py`: dispersion statistic and block-permutation nulls.
- `files/code/fly_composition.py`, `files/code/worm_composition.py`: per-type tests.
- `files/code/fly_pair_substitution.py`: pair correlations.
- `files/code/summarize.py`: tables and figures.
- `files/code/run_fly*.sh`: the batch scripts that we used.
- `files/figures/`: three PNG figures.

## References

- Dorkenwald et al. 2024, Nature, doi:10.1038/s41586-024-07558-y (FlyWire connectome).
- Schlegel et al. 2024, Nature, doi:10.1038/s41586-024-07686-5 (FlyWire annotations, hemilineages).
- Eckstein et al. 2024, Cell, doi:10.1016/j.cell.2024.03.016 (transmitter prediction).
- Witvliet et al. 2021, Nature, doi:10.1038/s41586-021-03778-8 (8 worm brains).
- Wang et al. 2024, eLife, doi:10.7554/eLife.95402 (worm transmitter atlas).
- Related campaign results: homologous synapse counts versus Poisson in worm and fly (sci:sha256:fc45a3bb…), inhibitory input fraction and response reliability in MICrONS (sci:sha256:a4bfe03d…).
