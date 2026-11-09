# In mouse V1, distance-matched EM wiring predicted slice connection rates of excitatory inputs to interneurons and of Pvalb-like outputs within 20%, but not of inhibition onto interneurons

## Question

Electron microscopy (EM) connectomes show anatomical synapses. Paired whole-cell recordings in brain slices show connections that give a detectable postsynaptic response. Studies of cortical circuits use both, but the two measures are rarely compared directly. We asked:

1. Does the EM connection rate between two cell classes, at the same soma distance, predict the connection rate that paired recordings detect in slices?
2. Where the two measures disagree, do slicing (cut axons and dendrites), EM axon completeness, or synapse location and size explain the difference?

Scope: mouse primary visual cortex (V1). Adult mice. One EM volume (MICrONS minnie65, one mouse) and the Allen Synaptic Physiology data set (many mice). Soma distance less than 250 um.

## Data

- **EM.** MICrONS minnie65 v1300 static exports (BossDB, CC BY 4.0): `connections_with_nuclei.csv.gz` (synapse counts and summed cleft size per neuron pair with nucleus), `synapses_pni_2_v1_filtered_view.csv.gz` (synapse positions and sizes), `allen_soma_ei_class_model_v1.csv` (excitatory or inhibitory class of 69,957 nuclei), `proofreading_status_public_release.csv` (600 proofread neurons), and the Ding et al. 2025 node table (layer labels of 12,894 neurons, used only to fit layer boundaries).
- **Physiology.** Allen Synaptic Physiology release 2.1, `synphys_r2.1_small.sqlite` (Allen Institute terms of use). We used mouse V1 pairs that were probed (more than 10 presynaptic test spikes at the holding potential for the presynaptic sign), with a connection call, and with 3D soma distance less than 250 um: 21,958 pairs from 2,171 slices.

Exact URLs and SHA-256 hashes are in `files/provenance/data_sources.json`. No raw data or record-level physiology tables are in this publication.

## Methods

**EM presynaptic sample.** We used only neurons with a proofread axon. The proofreading table gives axon status "clean" (false merges removed) or "extended" (also extended). Excitatory axons with status "clean" had a median of 128 output synapses, against 806 for "extended" axons in layer 2/3 (L2/3). Thus, for excitatory sources we used the 75 "extended" axons (27 in L2/3, 20 in L4, 27 in L5, 1 in L6). We made this choice after we saw these counts. For inhibitory sources we used all 98 proofread inhibitory axons (95 "clean", 3 "extended"; median 2,600 output synapses).

**EM inhibitory groups.** EM gives no Cre lines. We put each inhibitory axon in a target-based group, after Schneider-Mizell et al. 2025, with fixed rules from its output synapses: interneuron-targeting (InhTC, Vip-like) if 35 percent or more of its synapses go to inhibitory cells; else perisomatic-targeting (PeriTC, Pvalb-like) if 25 percent or more of its synapses on excitatory cells are within 15 um of the target nucleus centre; else sparse (SparTC) if it has fewer than 800 output synapses; else distal-targeting (DistTC, Sst-like). Result: 37 PeriTC, 27 DistTC, 30 InhTC, 4 SparTC. Both features had two clear modes. Postsynaptic interneuron groups are known only for these 98 typed cells, so EM rates onto interneurons use only them as targets.

**EM pairs.** For each presynaptic axon, every classified neuron with soma within 250 um was a candidate target. A pair was connected if the export gave at least one synapse. Layers came from boundaries fitted to the Ding et al. layer labels (L2/3 to L4 and L4 to L5, 97 percent accuracy). The L5 to L6 boundary is the L4 to L5 boundary plus 211 um. This is an approximation.

**Comparison.** For each physiology pair, the expected connection probability was the EM rate of the same class pair in the same 25 um bin of 3D soma distance. For excitatory to excitatory (E to E) pairs, the class pair also includes the presynaptic and postsynaptic layer. The ratio R = (observed physiology connections) / (sum of EM-expected probabilities). R = 1 means that the two methods agree. The 95 percent intervals come from a two-level bootstrap: we resampled EM presynaptic neurons and physiology slices (2,000 draws).

**Slicing tests.** (a) R as a function of soma distance. (b) R as a function of the shallower soma depth of the pair below the slice surface, and a binomial model of connection with the EM expectation as an offset, plus distance and depth terms (standard errors clustered by slice). (c) Virtual slicing: we put each EM connection at depth d below a virtual cut and kept a synapse only if it was inside a 350 um slab. A connection was kept if one or more synapses were kept. We used two cut directions (EM x and z axes) and both cut sides. This model ignores axon or dendrite paths that leave the slab, so it gives a lower bound on loss.

**Synapse features.** For each EM connection we measured the synapse count, the summed cleft size, and the distance of each synapse from the target nucleus centre. We compared these with R across the 12 class pairs with an inhibitory source (exploratory Spearman correlations).

## Results

### Connection rates (Figure 1)

| Class pair | Physiology connected/probed (rate) | EM rate at matched distance | EM source axons | R (95% CI) |
| --- | --- | --- | --- | --- |
| E L2/3→L2/3 | 28/407 (0.069) | 0.060 | 27 | 1.15 (0.72 to 1.71) |
| E L2/3→L4 | 4/90 (0.044) | 0.024 | 27 | 1.85 (0.42 to 4.08) |
| E L4→L4 | 78/987 (0.079) | 0.034 | 20 | 2.32 (1.49 to 3.37) |
| E L4→L5 | 25/363 (0.069) | 0.061 | 20 | 1.12 (0.68 to 1.82) |
| E L4→L2/3 | 8/87 (0.092) | 0.027 | 20 | 3.46 (1.23 to 7.30) |
| E L5→L5 | 126/2814 (0.045) | 0.037 | 27 | 1.23 (0.90 to 1.65) |
| E L5→L4 | 13/367 (0.035) | 0.015 | 27 | 2.44 (1.06 to 4.70) |
| E→Pvalb | 263/900 (0.292) | 0.276 | 24 | 1.06 (0.83 to 1.38) |
| E→Sst | 165/824 (0.200) | 0.249 | 24 | 0.80 (0.63 to 1.16) |
| E→Vip | 33/589 (0.056) | 0.053 | 44 | 1.05 (0.63 to 1.84) |
| Pvalb→E | 276/964 (0.286) | 0.356 | 37 | 0.80 (0.69 to 0.95) |
| Sst→E | 135/872 (0.155) | 0.339 | 27 | 0.46 (0.34 to 0.63) |
| Vip→E | 5/614 (0.008) | 0.011 | 30 | 0.76 (0.12 to 1.79) |
| Pvalb→Pvalb | 467/1841 (0.254) | 0.443 | 37 | 0.57 (0.49 to 0.68) |
| Pvalb→Sst | 26/605 (0.043) | 0.315 | 37 | 0.14 (0.08 to 0.21) |
| Pvalb→Vip | 19/488 (0.039) | 0.153 | 37 | 0.25 (0.14 to 0.40) |
| Sst→Pvalb | 77/583 (0.132) | 0.348 | 27 | 0.38 (0.26 to 0.54) |
| Sst→Sst | 90/3180 (0.028) | 0.301 | 27 | 0.09 (0.07 to 0.13) |
| Sst→Vip | 78/517 (0.151) | 0.203 | 27 | 0.74 (0.52 to 1.04) |
| Vip→Pvalb | 12/471 (0.025) | 0.207 | 29 | 0.12 (0.05 to 0.25) |
| Vip→Sst | 43/524 (0.082) | 0.246 | 29 | 0.33 (0.21 to 0.49) |
| Vip→Vip | 15/1070 (0.014) | 0.152 | 29 | 0.09 (0.05 to 0.15) |

In the physiology rows, Pvalb, Sst and Vip are Cre-defined classes. In the EM rows they are the PeriTC, DistTC and InhTC groups.

1. **Excitatory sources.** For excitatory sources onto interneurons, the two methods agreed: R was 1.06, 0.80 and 1.05 for Pvalb, Sst and Vip targets. EM also reproduced the 5-fold lower rate onto Vip cells than onto Pvalb cells. For E to E pairs, physiology found more connections than EM. The pooled layer-matched R was 1.47 (1.24 to 1.79; 284 observed against 193 expected in 5,147 pairs). Three of seven layer pairs had intervals above 1. No E-source class pair had an interval wholly below 1.
2. **Inhibitory sources onto excitatory cells.** Pvalb to E agreed within about 20 percent (R = 0.80, 0.69 to 0.95). Sst to E was about half of the EM expectation (R = 0.46).
3. **Inhibitory sources onto interneurons.** In all nine class pairs, the physiology rate was lower than the EM rate, with R from 0.09 to 0.74. Eight of the nine intervals were wholly below 1 and seven were wholly below 0.6 (Sst to Vip: 0.52 to 1.04). The largest differences were Sst to Sst (0.09) and Vip to Vip (0.09). EM gave rates of 15 to 44 percent for these class pairs.

### Robustness

- E to E: R decreased to 1.23 (0.99 to 1.60) with the half of EM axons that had the most output synapses, and increased to 1.76 with the other half. EM E to E rates increased with the axon output count (Spearman rho 0.44 to 0.62 by layer; Figure 3A). About 26 percent of the output synapses of extended excitatory axons went to segments with no nucleus, against about 10 percent for inhibitory axons. These two facts are consistent with an EM undercount of E to E connections. Removal of EM targets within 75 um of the volume edges did not change R (1.44).
- Physiology subsets gave E to E R from 1.08 (coarse-matrix project) to 1.75 (more than 200 test spikes). The 2 mM calcium subset gave R = 1.74 and the 1.3 mM subset gave 1.21. For Pvalb to E and E to Pvalb, the calcium difference had the opposite sign. Calcium is confounded with project and recording period, so we do not interpret it as a detection effect.
- Inhibitory results did not change materially with other typing thresholds (interneuron-target fraction 0.25 or 0.5; perisomatic fraction 0.15 or 0.30), without the sparse group, with only axons with 1,000 or more output synapses, or with sources only in L2/3 to L5 (`files/results/robustness_inhib.json`). Over all these variants, Sst to Sst R was 0.09 to 0.11 and Pvalb to Sst R was 0.12 to 0.16.

### Slicing (Figure 2)

- R did not decrease with soma distance for E to E, Pvalb to E, or Pvalb to Pvalb. For E to E and Pvalb to Pvalb it increased (Pvalb to Pvalb distance term +0.62 log-odds per 100 um, 95% CI 0.34 to 0.90). Only E to Pvalb decreased with distance (-0.74 per 100 um, CI -1.20 to -0.27). Thus, slicing loss that increases with distance is not the main cause of the differences.
- The soma depth term was small in all four models (E to E +0.15 log-odds per 100 um, CI -0.25 to 0.55; 4,164 pairs, 531 slices). The E to E ratio was lowest (1.13) for pairs with a soma less than 50 um deep. This agrees in shape with the virtual-slicing prediction (Figure 2C), but the intervals are wide.
- Virtual slicing kept 87 percent (60 um depth) to 93 percent (80 um depth) of EM E to E connections and 90 to 98 percent of connections with an inhibitory source or target. The median physiology soma depth was 71 um (interquartile range 53 to 95 um). Synapses beyond the cut can thus explain a loss of about 10 percent, not the 3- to 10-fold deficits for inhibitory connections onto interneurons. Path loss is not in this estimate.

### Synapse location and size (Figure 3B)

Across the 12 class pairs with an inhibitory source, R had no clear relation to the EM median synapse distance from the target nucleus (rho = -0.20, p = 0.53), summed cleft size (rho = 0.02), or synapses per connection (rho = -0.04). The target class gave the clearest separation (target interneuron against excitatory: rho = -0.64, p = 0.025, n = 12). For example, Pvalb to Sst synapses were as close to the target soma (median 31 um) as Pvalb to Pvalb synapses, but R was 0.14 against 0.57.

For E to E connections, the spread of log10 PSP amplitude (SD 0.41 to 0.54) was similar to the spread of log10 EM summed cleft size (SD 0.47 to 0.53). However, the order of median amplitudes across layer pairs did not follow the order of median EM sizes (`files/results/ee_amplitude_vs_size.csv`; 11 to 91 physiology connections per layer pair).

## Interpretation

At matched soma distance, EM wiring of proofread axons predicted the slice connection rates of excitatory sources onto all three interneuron classes and of Pvalb cells onto excitatory cells within about 20 percent. For E to E connections, the remaining excess in physiology is consistent with incomplete EM excitatory axons and synapses on segments with no nucleus. Thus, EM E to E rates in this sample are probably lower bounds. The largest differences were inhibitory connections onto interneurons: slice recordings detected 9 to 74 percent of the EM expectation. Distance, slice depth, virtual slicing, synapse location and synapse size did not explain this. Possible causes that we did not test are: small or shunting inhibitory responses in interneurons at the recording potential, mismatch between Cre classes and EM target groups (for example, DistTC cells that are not Sst cells), differences in Cre-line sampling, and differences between animals and ages. Studies that use slice data to set interneuron-to-interneuron connection probability in circuit models, or that use EM to predict functional inhibition between interneurons, should allow for this difference of up to 10-fold.

## Limitations

- One EM animal and a small number of proofread source axons per class (20 to 37). The EM axon-status criterion for excitatory cells was chosen after we saw output counts. The 76 "clean" excitatory axons gave both very low rates (many truncated L2/3 axons) and some very high rates (a few L5 axons with 10 to 28 percent E to E rates). We did not resolve this.
- EM inhibitory groups are inferred from target choice. They are not Cre classes. Postsynaptic interneuron groups are known only for 98 column cells.
- EM and physiology come from different mice, ages (physiology median age 46 days) and preparation conditions. Physiology used several protocols over years.
- Layers in EM are approximate. E to Vip rates mix all layers.
- The physiology detection threshold per pair is not in the small SQLite release, so we could not model detection directly.
- Virtual slicing uses synapse positions only. Cut paths are not modelled.
- The synapse-feature analysis has only 12 class pairs and is exploratory.

## Reproduce

1. `bash files/provenance/retrieve_data.sh /path/outside/publication` downloads the six inputs (about 23 GB) and checks their SHA-256 hashes.
2. Make a work folder `W` with `W/code` (copy of `files/code`), and a folder `W/../datasets/<dataset_name>/` for each input (the names in `retrieve_data.sh`). Copy `proofreading_status_public_release.csv` into `W`.
3. In `W`, run `bash files/provenance/run_all.sh` (about 40 minutes; most time is the stream of the 20 GB synapse file). It writes `scratch/`, `results_tables/` and `figures/`.

Software: Python 3.12, pandas, numpy, scipy, scikit-learn, statsmodels, matplotlib, pyarrow. Bootstrap seeds are fixed in the scripts.

## Files

- `files/code/` analysis scripts 01 to 15, `ratio_lib.py`, `common_load.py`.
- `files/results/` aggregate tables: ratios (`all_ratios.csv`, `rate_ratios.*`, `inhib_ratios.*`), sensitivity (`sensitivity_EE.json`, `robustness_inhib.json`), slicing (`distance_depth.json`, `virtual_slicing.json`), synapse features (`em_classpair_features.csv`, `crossclass_*`), EM rates and physiology counts by class, layer and distance bin, per-axon EM tables (`pre_output_counts.csv`, `em_inhibitory_types.csv`), and `ee_amplitude_vs_size.csv`.
- `files/figures/` three figures.
- `files/provenance/` data sources and hashes, retrieval and run scripts, external data notice.

## Provenance of this work

SCI campaign 11_07_2026. Job sci-1107-hp-neural-structure-and-computation-a55782e65912. Topic neural-structure-and-computation. Machine hp. Model claude-opus-5-5 (Claude Code), account claude-andrii. The signing key is a campaign-machine key, not a personal authorship claim. Analysis date 2026-11-09.

## External data and attribution

See `files/provenance/NOTICE-external-data.md`. MICrONS data: MICrONS Consortium, CC BY 4.0. Allen Synaptic Physiology data: Allen Institute for Brain Science, used under the Allen Institute terms of use. This publication contains no copy of either source data set. It contains our aggregate statistics and, for MICrONS, per-neuron derived features under CC BY 4.0 with attribution.
