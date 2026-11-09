# Membrane contact explains the higher synapse counts of two-way worm connections; fly two-way connections stay stronger after coarse controls

Job `sci-1107-hp-neural-structure-and-computation-7f19c55d4cbf`, topic `neural-structure-and-computation`, campaign 11_07_2026, machine `hp`, account `claude-olen`. Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an automated research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

In many connectomes, a connection A→B is stronger (it has more synapses) when the reverse connection B→A also exists. Lin et al. 2024 report this for the FlyWire whole fly brain, and cortical slice data show a similar result for amplitudes (Song et al. 2005). Theory reads it as a sign of learning or attractor storage (Brunel 2016). But two simpler causes can also make two-way ("reciprocal") connections look stronger:

1. **Neuron size and completeness.** Large or well-reconstructed neurons have many synapses in both directions.
2. **Geometry.** Two neurons whose neurites touch over a large area have more chances to make synapses in both directions.

We asked: **does the two-way strength excess remain when we remove neuron-level effects and the membrane contact between the two neurons?** We tested this in 8 *C. elegans* nerve rings (Witvliet et al. 2021; 7 have measured contact areas), in 2 adult *Drosophila* connectomes (FlyWire v783 and hemibrain v1.2), and in a small mouse cortex sample (MICrONS, Ding et al. 2025).

## Main results

1. **Worm: contact explains the excess.** With neuron fixed effects only, two-way connections had 1.22 times more synapses than one-way connections (pooled over 7 animals, 95% CI 1.17 to 1.27). Two-way pairs also had 2.08 times more membrane contact (CI 1.95 to 2.21). With contact area added as a control, the ratio fell to 0.95 (CI 0.91 to 0.99). With contact and the ordered neuron-class pair, it was 1.03 (CI 0.97 to 1.09; random-effects CI 0.94 to 1.15). All 7 animals agree, from the L1 stage at birth to the adult (Figure 1). For synapse volume, the ratio after the contact control was 0.87 (CI 0.82 to 0.93): two-way synapses were *smaller* at equal contact.
2. **Worm: almost no excess of two-way pairs after contact.** Among neuron pairs that touch, the number of two-way pairs was 941 against 922 expected if the two directions were independent given neuron effects and contact (2% more). The conditional odds ratio for a reverse edge was 1.20 (CI 1.05 to 1.36).
3. **Fly: the excess remains under all available controls.** At the standard 5-synapse threshold, the ratio was 1.23 (CI 1.22 to 1.24) in FlyWire and 1.33 (1.31 to 1.35) in the hemibrain, with neuron and dominant-neuropil effects. Within the same ordered cell-type pair it was 1.27 (FlyWire) and 1.22 (hemibrain). The two FlyWire hemispheres agree (1.23 and 1.22). A coarse geometry proxy (neuropil overlap of axon and dendrite profiles in both directions) did not lower the ratio (1.24 FlyWire, 1.32 hemibrain) (Figure 2).
4. **A shared pair factor that worm contact removes is present in fly.** In two-way pairs, the residual forward and reverse log synapse counts were correlated. In the worm this correlation was 0.15 (CI 0.08 to 0.21) with neuron effects only and 0.04 (CI −0.03 to 0.10) after the contact control. In the fly, with neuron and neuropil effects, it was 0.13 to 0.14 (FlyWire) and 0.26 (hemibrain). The fly value is similar to the worm value *before* the contact control (Figure 3A). Thus we cannot exclude that fine-scale contact, which the fly tables do not give, also explains the fly excess.
5. **Fly: excitatory pairs have the smallest excess.** In FlyWire (≥5 synapses), cholinergic-to-cholinergic two-way connections were 1.09 times stronger (CI 1.07 to 1.10; 1.03 at ≥10 synapses). Connections between pairs that include a GABA or glutamate neuron were 1.19 to 1.31 times stronger (Figure 3B). This does not agree with the prediction that the excess is largest between excitatory neurons.
6. **Mouse: no conclusion.** In the MICrONS functional-connectomics table, only 14 two-way directed edges (7 pairs) occur among 259 connected edges whose reverse direction could be observed. The synapse-count ratio was 0.93 (CI 0.85 to 1.02) after presynaptic-neuron and co-travel controls. This sample cannot test the question.

**Summary.** In the only connectomes with measured membrane contact (worm), the strength excess of two-way connections is fully explained by neuron effects plus the larger contact of two-way pairs. In the fly, a 1.2 to 1.3 fold excess remains after neuron, neuropil, cell-type and coarse neuropil-overlap controls. A forward–reverse residual correlation of the same size as in the worm before contact control shows that an unmeasured pair factor is present. A strength excess in raw connectome tables is therefore not sufficient evidence of activity-dependent strengthening or attractor storage. Contact or fine-scale overlap must be controlled first.

## Figures

- `files/figures/fig1_worm_contact_control.png`. Worm synapse-count ratio (two-way / one-way) per animal under four models, and the contact-area ratio.
- `files/figures/fig2_fly_controls.png`. Fly synapse-count ratio under five models for FlyWire and the hemibrain at several thresholds and per FlyWire hemisphere.
- `files/figures/fig3_pair_factor_transmitter.png`. (A) Forward–reverse residual correlation in two-way pairs. (B) FlyWire ratio by transmitter pair.

## Methods

**Edges.** A directed edge i→j has weight w = synapse count. In the worm we count each polyadic synapse once per postsynaptic partner, for neurons only (no muscle or glia), from the Witvliet et al. 2021 nerve-ring annotations. An edge is *two-way* (R = 1) if the reverse edge j→i also exists at the same threshold. Fly thresholds: ≥5 synapses (standard) and ≥10 (FlyWire); ≥1, 3, 5, 10 (hemibrain). Worm threshold: ≥1, with ≥2 as a sensitivity check.

**Strength model.** log w_ij = a_i + b_j + Σ_k g_k(ij) + β R_ij + e_ij, fit on existing edges. Here a_i and b_j are presynaptic and postsynaptic neuron fixed effects, and g_k are optional fixed effects: contact-area bins (20 quantiles of log contact, worm), ordered neuron-class pair (worm) or cell-type pair (fly), the neuropil with most synapses of the pair (fly), and bins of the forward and reverse neuropil opportunity (fly geometry proxy). We remove the fixed effects by alternating projections and report exp(β), the ratio of geometric-mean synapse counts. Standard errors are *dyadic-robust*: they allow correlation between all edges that share a neuron, which includes the two directions of a two-way pair (Fafchamps and Gubert 2007; Aronow et al. 2015). A simulation with a known effect (0.30) recovered 0.32 ± 0.07.

**Contact (worm).** Contact area between two neurons comes from the Witvliet et al. 2021 nerve-ring volume reconstructions (7 datasets; dataset 7 has no contact table). Almost all edges (≥ 99.8%) have contact > 0.

**Occurrence (worm).** Among touching neuron pairs, we fit a logit for edge presence with neuron fixed effects, contact bins and the reverse-edge indicator (dyadic-robust errors). We also compare the observed two-way pair count with Σ p_ij p_ji from the same logit without the reverse term.

**Forward–reverse residual correlation.** Spearman correlation between residuals of i→j and j→i in two-way pairs. Null: residuals paired at random (mean ≈ 0). Worm CIs: pair bootstrap per animal and Fisher-z pooling. Fly CIs: bootstrap over pairs (100 draws; subsample of at most 200,000 pairs).

**Fly geometry proxy.** For each neuron we compute the fraction of its output synapses and of its input synapses in each neuropil (FlyWire) or primary ROI (hemibrain). Forward opportunity is O_f = Σ_r min(out_i(r), in_j(r)). Reverse opportunity O_r uses out_j and in_i. These profiles include the synapses of the edge itself, and they are region-scale, not micron-scale. Thus this proxy is weak, and it is not a contact measurement.

**Transmitter split (FlyWire).** The top predicted transmitter of each neuron is grouped as ACh, GABA/Glu ("inh"), or other. Separate β terms are fit per ordered transmitter pair, with that pair as an extra fixed effect.

**Pooling.** Inverse-variance (fixed) and DerSimonian–Laird (random) pooling of log ratios across worm animals.

## Detailed results

Worm (synapse-count ratio, two-way / one-way, 95% dyadic-robust CI; "neuron" uses the contact subset where contact exists):

| D | stage | edges | two-way edges | no control | neuron | + contact | + class pair | contact ratio | reverse-edge OR | two-way pairs obs/exp |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | L1 0h | 675 | 116 | 1.12 [1.00, 1.26] | 1.05 [0.93, 1.20] | 0.84 [0.73, 0.98] | 0.84 [0.74, 0.95] | 2.15 [1.80, 2.58] | 1.19 [0.68, 2.09] | 58/57 |
| 2 | L1 5h | 865 | 166 | 1.24 [1.07, 1.43] | 1.15 [1.06, 1.25] | 0.92 [0.85, 1.01] | 0.99 [0.83, 1.19] | 2.28 [1.88, 2.77] | 1.17 [0.80, 1.71] | 83/81 |
| 3 | L1 8h | 887 | 198 | 1.21 [1.06, 1.38] | 1.19 [1.04, 1.36] | 0.99 [0.85, 1.14] | 0.94 [0.75, 1.18] | 1.90 [1.51, 2.39] | 1.53 [0.99, 2.34] | 99/89 |
| 4 | L1 16h | 1012 | 208 | 1.36 [1.14, 1.62] | 1.20 [1.08, 1.33] | 0.97 [0.87, 1.08] | 1.20 [0.99, 1.45] | 1.91 [1.60, 2.27] | 1.13 [0.79, 1.62] | 104/104 |
| 5 | L2 23h | 1325 | 316 | 1.19 [1.02, 1.38] | 1.27 [1.15, 1.40] | 0.97 [0.89, 1.06] | 1.10 [0.93, 1.31] | 2.01 [1.73, 2.35] | 1.25 [0.96, 1.62] | 158/157 |
| 6 | L3 27h | 1314 | 278 | 1.19 [1.00, 1.42] | 1.21 [1.07, 1.37] | 0.96 [0.86, 1.08] | 1.14 [0.96, 1.34] | 1.78 [1.53, 2.07] | 0.87 [0.64, 1.19] | 139/149 |
| 7 | adult 50h | 1933 | 528 | 1.15 [1.01, 1.32] | 1.34 [1.20, 1.50] | – | – | – | – | – |
| 8 | adult 50h | 1933 | 600 | 1.20 [1.07, 1.35] | 1.45 [1.30, 1.61] | 0.97 [0.86, 1.08] | 1.12 [0.99, 1.25] | 2.44 [2.13, 2.80] | 1.44 [1.07, 1.93] | 300/285 |

(Datasets 7 and 8 have the same edge count by chance: they share 1,279 edges and have 6,560 and 7,061 synapse–partner counts.)

Worm sensitivity (`files/results/worm_sensitivity.json`): after the contact control, the ratios were 0.87 to 0.98 with 40 bins, 0.86 to 1.02 with 5 bins, 0.87 to 0.98 with a linear and quadratic log-contact term, and 0.83 to 1.02 with edges and reciprocity defined at ≥2 synapses. All 7 animals give values at or below about 1 in all four checks.

Fly (synapse-count ratio; full CIs in `files/results/summary_ratios.csv`):

| data | threshold | edges | two-way edges | none | neuron | + neuropil | + type pair | + opportunity (both dir.) |
|---|---|---|---|---|---|---|---|---|
| FlyWire whole brain | ≥5 | 2,700,513 | 377,448 | 1.34 | 1.23 | 1.23 | 1.27 | 1.24 |
| FlyWire whole brain | ≥10 | 1,066,822 | 123,018 | 1.28 | 1.23 | 1.23 | 1.24 | 1.23 |
| FlyWire left hemisphere | ≥5 | 1,077,560 | 145,062 | 1.37 | 1.23 | 1.23 | 1.28 | – |
| FlyWire right hemisphere | ≥5 | 1,230,213 | 172,548 | 1.35 | 1.23 | 1.22 | 1.30 | – |
| hemibrain | ≥1 | 3,550,403 | 1,304,956 | 1.40 | 1.45 | 1.44 | 1.27 | 1.45 |
| hemibrain | ≥3 | 1,144,112 | 305,640 | 1.37 | 1.36 | 1.37 | 1.24 | 1.37 |
| hemibrain | ≥5 | 662,578 | 155,662 | 1.40 | 1.32 | 1.33 | 1.22 | 1.32 |
| hemibrain | ≥10 | 305,058 | 63,778 | 1.44 | 1.30 | 1.31 | 1.23 | 1.30 |

Dyadic-robust CIs for the fly models with neuron effects have half-widths of 0.01 to 0.03. With these sample sizes, the statistical error is much smaller than the uncertainty from missing controls.

The probability that a reverse edge exists increases with forward weight in all fly tables. For example, in FlyWire at ≥5 synapses it rises from 0.09 for 5-synapse edges to 0.36 for edges with ≥69 synapses (`p_reverse_by_weight` in the result JSON files).

## Limitations

- **Contact is measured only in the worm.** The fly result cannot separate a wiring rule from fine-scale geometry. The neuropil proxy is coarse and partly circular. A micron-scale contact or arbor-overlap measure for FlyWire or the hemibrain would resolve this.
- **Contact can be both a cause and a result.** If synapse formation enlarges contact, the contact control removes part of a true effect. Synapses are a small part of total contact area in the nerve ring, but we did not measure this fraction.
- **Worm samples are small** (116 to 600 two-way edges per animal). Single-animal CIs are wide. The pooled estimates and the agreement of 7 animals carry the result.
- **Neuron fixed effects absorb any reciprocity effect that is constant for a neuron.** The estimate is a within-neuron comparison.
- **Transmitter labels in the fly are predictions.** Glutamate is treated as inhibitory, which is not true at all fly synapses.
- **Mouse data are too sparse** (7 two-way pairs) for any conclusion.
- **Synapse count is a proxy for strength.** We did not use physiology.

## Reproduction

1. Get the inputs. On the campaign host they are in the shared store (`datasets/`, paths in `files/data/input_sha256.txt`). Elsewhere, run `bash files/code/fetch_data.sh /some/scratch/folder`. The script downloads into that folder (never into this bundle) and checks the SHA-256 hashes.
2. Run `SCI_DATASETS=/some/scratch/folder SCI_SCRATCH=/some/tmp bash files/code/run_all.sh` from a working folder. It writes `files/results/*.json`, `summary_ratios.csv` and the figures. Python 3.12 with numpy, scipy, pandas, pyarrow and matplotlib. Set one BLAS thread per process (the script does this). Peak memory is about 2 GB for FlyWire.
3. The analysis is deterministic except for bootstrap draws, which use fixed seeds.

Files:
- `files/code/fe.py`: fixed-effect regression with dyadic-robust errors.
- `files/code/worm.py`, `worm_sens.py`, `worm_rho.py`: worm analyses.
- `files/code/fly.py`, `flyload.py`, `fly_geom.py`: fly analyses.
- `files/code/mouse.py`: MICrONS check.
- `files/code/summarize.py`: pooling, tables, figures.
- `files/results/`: aggregate results only (model coefficients, counts, correlations). They contain no neuron-level or edge-level records.

## Data provenance and licences

The bundle contains no third-party raw data and no record-level derived tables. See `files/NOTICE-external-data.md` for the sources, versions, URLs, hashes and licence terms of the external inputs.

## References

- Witvliet D. et al. (2021) Connectomes across development reveal principles of brain maturation. Nature 596. doi:10.1038/s41586-021-03778-8
- Dorkenwald S. et al. (2024) Neuronal wiring diagram of an adult brain. Nature 634. doi:10.1038/s41586-024-07558-y
- Schlegel P. et al. (2024) Whole-brain annotation and multi-connectome cell typing of Drosophila. Nature 634. doi:10.1038/s41586-024-07686-5
- Lin A. et al. (2024) Network statistics of the whole-brain connectome of Drosophila. Nature 634. doi:10.1038/s41586-024-07968-y
- Scheffer L.K. et al. (2020) A connectome and analysis of the adult Drosophila central brain. eLife 9:e57443. doi:10.7554/eLife.57443
- Ding Z. et al. (2025) Functional connectomics reveals general wiring rule in mouse visual cortex. Nature 640. doi:10.1038/s41586-025-08840-3
- Song S. et al. (2005) Highly nonrandom features of synaptic connectivity in local cortical circuits. PLoS Biol 3:e68. doi:10.1371/journal.pbio.0030068
- Brunel N. (2016) Is cortical connectivity optimized for storing information? Nat Neurosci 19. doi:10.1038/nn.4286
- Fafchamps M., Gubert F. (2007) The formation of risk sharing networks. J Dev Econ 83. doi:10.1016/j.jdeveco.2006.05.005
- Aronow P.M., Samii C., Assenova V.A. (2015) Cluster-robust variance estimation for dyadic data. Political Analysis 23. doi:10.1093/pan/mpv018
