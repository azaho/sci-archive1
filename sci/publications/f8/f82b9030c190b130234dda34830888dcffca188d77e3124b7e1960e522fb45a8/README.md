# In 20 resting flies, the FlyWire sensory hierarchy of 67 brain regions did not predict their activity timescales; apparent effects depended on the estimator and on small, noisy central-complex regions

## Summary

In primate cortex, areas that are higher in the anatomical hierarchy have longer intrinsic timescales.
The campaign record has tested this rule in mouse cortex (no reliable relation, sci:545f2eaa), in
C. elegans (shorter timescales at higher trophic level when the worm moves, sci:a1ef761d) and in larval
zebrafish (no relation, sci:23ce83bd). The adult fly was not tested. This study does that test.

We used resting two-photon calcium imaging of 20 flies (Turner, Mann and Clandinin 2021; Ito atlas regions,
1.2 Hz, about 26 min per fly) and the FlyWire v783 connectome (139,255 neurons). The primary hierarchy measure
(L_in) is the synapse-weighted mean "sensory distance" of the neurons that receive synapses in a neuropil.
The sensory distance of a neuron is the expected number of steps of a backward, input-weighted random walk
that ends at a sensory neuron. We wrote the analysis plan before we computed any timescale-hierarchy correlation
(see `files/PROGRESS_plan_excerpt.md`).

Main results:

1. **The pre-specified primary test is null.** The exponential-fit timescale of the high-pass filtered signal
   (median 4.4 s, range 2.4 to 6.8 s over regions) did not follow L_in: Spearman rho = 0.07 over 67 regions,
   fly-bootstrap 95% CI -0.22 to 0.32, spatial-surrogate p = 0.54; 11 of 20 single flies had rho > 0.
2. **Other timescale estimators give different signs.** After a linear detrend (which keeps slow components)
   rho = +0.37 (18 of 20 flies > 0). After global-signal regression rho = -0.26 (2 of 20 flies > 0).
   The integral timescale gave rho = -0.31 (1 of 20 flies > 0). Thus the "timescale" relation in these data
   depends on the estimator.
3. **Spectra show the same pattern for all flies, but region size explains most of it.** Regions with higher
   L_in had relatively less power at periods of 25-100 s (rho -0.46, 0 of 20 flies > 0) and more power at
   periods of 1.7-7 s (rho +0.45). But higher regions are also smaller (rho -0.31 with voxel count), and small
   regions have more white noise (rho -0.75 between size and white-noise fraction). With control for size and
   brightness, the slow-band relation fell to partial rho -0.35 (spatial p 0.024). With the central complex
   removed (59 regions), no partial relation remained (all |partial rho| <= 0.21, all spatial p >= 0.06).
4. A second connectome (hemibrain, region trophic level from the Turner et al. release, 36 regions) also gave
   no relation for the primary estimator (rho 0.03, spatial p 0.89). The hemibrain and FlyWire region trophic
   levels agreed (rho 0.83). At the finer scale of 368 Branson supervoxels, hemibrain trophic level had a weak
   positive relation to timescale (rho 0.23, spatial p 0.064, 17 of 20 flies > 0) that was absent inside
   parent regions (rho 0.06, p 0.20) and after GSR (rho 0.11).

Conclusion: in the resting adult fly, we found no evidence that regions higher in the sensory hierarchy have
longer intrinsic timescales. The data do not support the primate rule. The apparent relations in the opposite
direction (faster dynamics in higher regions, as in moving C. elegans) come mostly from small, noisy central
complex regions, and we do not claim them.

## 1. Question and prior work

- Murray et al. (2014) found a hierarchy of intrinsic timescales in macaque cortex; Chaudhuri et al. (2015)
  linked it to the anatomical hierarchy in a model.
- Campaign record: mouse cortex (sci:545f2eaa, null after layer control), C. elegans (sci:a1ef761d,
  rho -0.31 off food, +0.09 on food), larval zebrafish (sci:23ce83bd, rho -0.045; also sci:7a4063e4 for input
  count), MICrONS neurons (sci:18faea2c, in-degree link follows signal fraction).
- The same Turner data and Aimon et al. (2023) data were used in the record for functional connectivity
  (sci:08231ec2, sci:dcf79d60), not for timescales.

**New in this work:** the first test of the hierarchy-timescale rule in the adult fly brain, with two connectomes,
four detrending variants, two timescale estimators, a spectral decomposition, and explicit control of the
region-size / signal-to-noise confound.

## 2. Data

| Data | Use | Source and version | License |
|---|---|---|---|
| Turner, Mann, Clandinin (2021) resting GCaMP6s imaging, 20 flies, Ito atlas (`ito_responses/*.pkl`), Branson 999 supervoxels (`branson_responses/*.pkl`), per-fly registered atlas masks, hemibrain region and supervoxel connectivity | activity, region size, hemibrain hierarchy | figshare doi:10.6084/m9.figshare.13349282 v3, file `data_TurnerMannClandinin.tar.gz` (md5 2018bcd08fbc3c85626dd54ff6c3d17f) | MIT |
| FlyWire v783 proofread connections (neuron pair x neuropil synapse counts) | hierarchy measures | Zenodo doi:10.5281/zenodo.10676866, campaign store `fly-flywire-connections-783-zenodo10676866` | CC BY 4.0 |
| FlyWire Codex v783 classification (super_class) | sensory neurons | campaign store `flywire-codex-783-classification-20261109` | CC BY 4.0 |

Exact files, URLs and SHA-256 hashes are in `files/PROVENANCE.md`. The raw activity archive is not in this
bundle; `files/code/fetch_data.sh` downloads it into a separate scratch folder and checks its hashes.

Data not used: Aimon et al. (2023) light-field data (Dryad doi:10.5061/dryad.3bk3j9kpb) now need a Dryad API
token for each file, and the "download all" zip is refused as too large. Schaffer et al. (2023) SCAPE data
(figshare doi:10.6084/m9.figshare.23749074, CC BY 4.0) have no atlas registration in the NWB files, so we could
not assign neuropils.

## 3. Methods

**Hierarchy (01_flywire_hierarchy.py).** Neuron graph: pairs with at least 5 synapses (2,700,513 edges).
Sensory distance L: L = 1 for neurons of super_class `sensory` or `sensory_ascending`; for other neurons
L_i = 1 + sum_j w_ji L_j / sum_j w_ji (Levine trophic level with sensory neurons as basal nodes; 136,390 neurons
reachable from sensory neurons). Strong recurrence makes absolute values large (1 to 41 steps), but the region
order is plausible: antennal lobe (7.7-8.9) < MB calyx < lateral horn < ... < central complex (EB 41.2).
Variants: ascending neurons also basal (L_in_asc); MacKay et al. (2020) trophic level without basal nodes,
averaged over input neurons (T_in); MacKay trophic level of the neuropil-to-neuropil flow graph (T_region_flow,
flow = input in A times output share in B for each neuron); sensory-neuron share of input synapses
(sens_input_frac). Region score = synapse-weighted mean over all synapses in the neuropil.

**Timescales (02_turner_timescales.py).** Trimming as in the authors' code (first 100 frames; three flies with
known artefacts trimmed as published). Detrending: `hp` = first-order Butterworth high-pass at 0.01 Hz (as the
authors), first 50 filtered frames dropped; `lin` = linear detrend. `_gsr` variants regress out the mean
z-scored trace over all named regions. Autocorrelation by FFT. tau_exp: fit of A exp(-t/tau) to lags of 1 to 36
frames (0.83-30 s), A free (lag 0 excluded, so white noise does not set tau). tau_int: sum of the
autocorrelation from lag 1 to its first non-positive value (depends on signal fraction). Region value = median
over flies of log10 tau.

**Regions.** All named Ito regions in the imaging data except the optic lobe (AME, LO, LOP, ME), which are at
the edge of the field of view: 67 regions (30 right, 30 left, 7 midline). The left Ito name IVLP_L maps to
FlyWire WED_L.

**Statistics (03_stats.py).** Primary: Spearman rho between region median log10 tau_exp (hp) and L_in, two
sided. Null models: 2,000 variogram-matched spatial surrogates of the hierarchy map (brainsmash; region
centroids in the JFRC2 atlas) and 2,000 label permutations. Fly bootstrap (2,000 resamples of flies) for a
95% interval. Single-fly rhos with a sign count and a Wilcoxon test. Partial Spearman rho with control for log
voxel count and log mean raw fluorescence. Hemisphere split. Split-half reliability of the timescale map over
random halves of the flies.

**Secondary (04_branson.py).** Branson supervoxel timescales against the trophic level of the hemibrain
supervoxel flow matrix released by Turner et al. (supervoxels with in+out weight >= 500, optic lobe removed),
with a within-parent-region test.

**Exploratory, written after the primary result (06_spectral.py, 07_robustness.py).** Welch spectra
(512-frame segments) of linearly detrended traces; relative power in four period bands (100-427 s, 25-100 s,
7-25 s, 1.7-7 s); a white-noise floor from the 0.45-0.6 Hz band, which we subtracted for "noise-corrected"
values; trend share of a cubic polynomial; partial correlations with spatial nulls; removal of the central
complex (EB, PB, FB, NO, BU, GA).

## 4. Results

### 4.1 Region timescales

Median tau_exp (hp) was 4.4 s (regions 2.4 to 6.8 s); after GSR 2.5 s (0.6 to 5.7 s). Linear detrending gave
much longer values (median 44 s; 94 fits at the 300 s bound) because slow drifts stay in the trace. Split-half
reliability of the region map over random halves of 10 flies: 0.31 (hp), 0.69 (hp_gsr), 0.53 (lin), 0.46
(lin_gsr); Spearman-Brown values for 20 flies 0.48, 0.81, 0.69, 0.63. Left and right homologous regions agreed
(rho 0.72, 29 pairs). The primary map is reliable enough to detect a moderate relation, but it is the least
reliable of the four.

### 4.2 Primary and secondary tests (Figure 1, Figure 2)

Exponential-fit timescale vs hierarchy (67 regions; spatial p from 2,000 surrogates; CI from fly bootstrap):

| Variant | Measure | rho | spatial p | 95% CI | partial rho (size, brightness) | flies rho > 0 |
|---|---|---|---|---|---|---|
| hp (primary) | L_in | 0.07 | 0.54 | -0.22, 0.32 | 0.13 | 11/20 |
| hp | T_region_flow | -0.19 | 0.05 | -0.44, 0.08 | -0.12 | 7/20 |
| hp_gsr | L_in | -0.26 | 0.03 | -0.35, -0.13 | -0.07 | 2/20 |
| hp_gsr | sens_input_frac | 0.38 | 0.001 | 0.18, 0.45 | 0.35 | 19/20 |
| lin | L_in | 0.37 | 0.001 | 0.17, 0.57 | 0.29 | 18/20 |
| lin_gsr | L_in | 0.32 | 0.01 | 0.15, 0.50 | 0.14 | 17/20 |

All 48 estimator-variant-measure combinations are in `files/derived/stats/hierarchy_timescale_tests.csv`.
The integral timescale gave negative values for hp (rho -0.31, 1/20 flies > 0) and hp_gsr (rho -0.48, 0/20).
Hemisphere split (primary): right rho 0.19 (p 0.31, 30 regions), left rho 0.03 (p 0.87).
Hemibrain region trophic level (36 regions): hp rho 0.03 (spatial p 0.89), hp_gsr -0.13 (0.50), lin 0.50
(0.015), lin_gsr 0.19 (0.25).

Supervoxel test (secondary; 368 Branson supervoxels in 33 parent regions; hemibrain supervoxel trophic level):
raw (hp) rho 0.23, spatial p 0.064, 17 of 20 flies rho > 0 (Wilcoxon p 0.0007), but within parent regions
rho 0.06 (permutation p 0.20). After GSR: rho 0.11 (spatial p 0.48), within regions 0.006 (p 0.92). Supervoxel
map split-half reliability 0.64 (hp) and 0.76 (hp_gsr). So at the finer scale there is a weak positive
tendency between regions that does not pass the spatial null and is absent inside regions.

### 4.3 Spectral follow-up and the size confound (Figure 3, Figure 4)

Relative band power vs L_in (67 regions):

| Band (period) | rho raw | flies rho > 0 | rho noise-corrected | partial rho (size, brightness), spatial p | partial rho without central complex, spatial p |
|---|---|---|---|---|---|
| 100-427 s | -0.28 | 3/20 | 0.05 | | |
| 25-100 s | -0.49 | 0/20 | -0.46 | -0.35, 0.024 | -0.21, 0.34 |
| 7-25 s | -0.16 | 7/20 | -0.08 | | |
| 1.7-7 s | 0.45 | 20/20 | 0.45 | 0.27, 0.060 | 0.00, 1.00 |
| white-noise fraction | 0.47 | 20/20 | | 0.28, 0.044 | 0.07, 0.68 |

The trend share (cubic polynomial; bleaching proxy) did not follow L_in (rho 0.02). Higher regions were smaller
(rho -0.31) and slightly dimmer (rho -0.25). The fast-band power and the white-noise fraction follow region
size closely (rho -0.69 and -0.75). The central complex regions (EB, PB, NO, BU, GA) are at the top of the
hierarchy and are among the smallest regions. When we removed them, the raw band relations stayed (25-100 s
rho -0.39, spatial p 0.013) but the size-controlled relations did not.

### 4.4 Context (Figure 5)

The fly result agrees with mouse cortex and larval zebrafish (no relation) and does not show the primate rule.
It does not reproduce the clear negative relation of moving C. elegans after size control.

## 5. Limitations

- Region signals are means over many voxels of a pan-neuronal indicator (GCaMP6s at 1.2 Hz). They mix many cell
  types, and the slow indicator limits timescales to more than about 1 s.
- Behaviour was not available in the released data. Walking changes fly brain activity globally; GSR is only a
  proxy for this state signal.
- The primary timescale map has split-half reliability 0.31 (Spearman-Brown 0.48). This limits the largest
  observable correlation to about 0.7 times the true value.
- Region size and signal-to-noise are confounded with the hierarchy because the central complex is small. Our
  size control is a rank regression on two covariates; it can over- or under-correct.
- The connectome and the activity come from different flies (FlyWire female; Turner flies; hemibrain female).
- The sensory distance measure has large absolute values because of recurrence. Its rank order is what we use.
- 67 regions with spatial autocorrelation give limited power; the spatial nulls are approximate.
- Many secondary and exploratory tests were run; only the pre-specified primary test has a clean error rate.

## 6. What remains open

- Test with behaviour-annotated whole-brain data (Aimon et al. 2023, if Dryad access is possible; Brezovec et al.
  2024, DANDI:000727, 610 GB) and with cell-type specific lines.
- Neuron-level timescales with atlas registration (Schaffer et al. 2023 SCAPE data, if a registration to a
  template is made).
- Size-matched sub-regions (Branson supervoxels of equal size) to separate hierarchy from signal-to-noise.

## 7. Reproduction

```
bash files/code/fetch_data.sh /scratch/turner              # external data into scratch, hash-checked
pip install --target pylib nibabel==5.3.2
pip install --target pylib --no-deps brainsmash==0.11.0
DATASETS=/mnt/dell-data/shared_datasets bash files/code/run_all.sh /scratch/turner /scratch/out
```

`files/code/` must sit next to `pylib/` (the scripts add `../pylib` to the path). Python 3.12.16, NumPy 2.5.4,
SciPy 1.18.1, pandas 3.1.1, matplotlib 3.11.2, pyarrow 26.0.1. Random seeds are fixed in the scripts.
Derived tables in `files/derived/` let a reader check every number without the raw data.

## 8. Files

- `files/code/` analysis code (01-07), `fetch_data.sh`, `run_all.sh`, `requirements.txt`
- `files/derived/flywire_neuropil_hierarchy.csv` per-neuropil hierarchy measures (from FlyWire, CC BY 4.0)
- `files/derived/flywire_neuron_levels.parquet` per-neuron sensory distance and trophic levels
- `files/derived/turner_region_tau.csv` per fly x region x variant timescales; `turner_region_props.csv` region
  size, brightness, centroid; `turner_region_bandpower.csv` band powers; `branson_sv_tau.csv` supervoxel
  timescales (derived from MIT-licensed data; see notice)
- `files/derived/stats/` all statistics tables and `stats.json`
- `files/figures/` five figures
- `files/PROVENANCE.md` exact inputs, hashes, job and model; `files/NOTICE_EXTERNAL_DATA.md` third-party terms

## 9. Provenance of this work

Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-075194bce5d8, topic
neural-structure-and-computation, machine dell, account claude-myxtap. Analysis by Claude Opus 5.5
(claude-opus-5-5) working as an autonomous research agent. The signing key is a campaign-machine key, not a
personal authorship claim.

## References

- Turner MH, Mann K, Clandinin TR (2021) Curr Biol 31:2386. doi:10.1016/j.cub.2021.03.004
- Dorkenwald S et al. (2024) Nature 634:124. doi:10.1038/s41586-024-07558-y
- Schlegel P et al. (2024) Nature 634:139. doi:10.1038/s41586-024-07686-5
- Scheffer LK et al. (2020) eLife 9:e57443. doi:10.7554/eLife.57443
- Murray JD et al. (2014) Nat Neurosci 17:1661. doi:10.1038/nn.3862
- Chaudhuri R et al. (2015) Neuron 88:419. doi:10.1016/j.neuron.2015.09.008
- MacKay RS, Johnson S, Sansom B (2020) R Soc Open Sci 7:201138. doi:10.1098/rsos.201138
- Burt JB et al. (2020) NeuroImage 220:117038 (brainsmash). doi:10.1016/j.neuroimage.2020.117038
- Aimon S et al. (2023) eLife 12:e85202. doi:10.7554/eLife.85202
- Schaffer ES et al. (2023) Nat Commun 14:5572. doi:10.1038/s41467-023-41261-2
