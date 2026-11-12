# In 459 IBL mouse sessions, 5-11 Hz rhythmic spiking formed a lick-locked orofacial system and a septo-hippocampal system; mesoscale septal input did not predict the regional map

Job `sci-1107-dell-neural-structure-and-computation-697beb9f1a94`, topic `neural-structure-and-computation`,
campaign 11_07_2026, machine `dell`, account `claude-sci`, model `claude-opus-5-5` (Claude Code in T3 Code).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** The medial septum (MS) paces the hippocampal theta rhythm (about 6-10 Hz). Many neurons outside the
hippocampus also fire rhythmically near this frequency. Does anatomical input from the septal pacemaker tell
which mouse brain regions contain rhythmic neurons? If not, what other system makes the rhythm?

**Data.** International Brain Laboratory (IBL) Brain-Wide Map 2026 Q2 aggregates: log-binned spike
autocorrelograms (ACGs, 1 ms to 1.94 s) of 75,129 good units from 459 sessions and 698 probes. Structure:
the Knox et al. (2019) mesoscale connectome model, and (post hoc) 14 Allen Mouse Brain Connectivity tracer
experiments with injections in MS or the diagonal band nucleus (NDB). Behaviour: lick times and spike
windows of 16 IBL probes.

**Method.** For each unit we fitted the ACG (40-600 ms, normalised to its asymptote) with a cubic polynomial
in log lag plus a damped cosine. The cosine amplitude A (fraction of baseline) and its z value, at the best
frequency in 5-11 Hz, measure rhythmicity. A unit is rhythmic if z >= 5. A 12-20 Hz control band used the
same rule. We computed the share of rhythmic units in 200 summary structures (>= 20 units, >= 2 sessions).
We wrote and hashed the analysis plan (`files/code/PLAN.md`) before any structure-to-rhythm statistic.
Inference used 1,000 Gaussian-process spatial surrogate maps (method of sci:f4e4c521).

**Results.**

1. The rhythm map is reliable and has two clusters. 16.1% of units were rhythmic at 5-11 Hz; 0.6% passed the
   same rule at 12-20 Hz. The split-half (session) Spearman correlation of the regional share was 0.52
   (95% range 0.43-0.61). The highest shares were in septo-hippocampal regions (TRS 0.63, MS 0.58, LSc 0.51,
   SF 0.48, DG 0.43, CA1 0.40) and in orofacial brainstem and mouth sensory regions (SPVC 0.51, SSp-m 0.49,
   IRN 0.42, V 0.41, SUT 0.35, VII 0.32, PARN 0.32). Both clusters had a median best frequency of 6.75 Hz.
2. Planned test H1 failed. Knox MS+NDB input did not predict the regional share (Spearman 0.05, spatial p 0.36;
   64th percentile of 291 single sources). No Knox source passed the spatial null (best rho 0.16; null 95%
   point 0.22). The orofacial-source test H2 also failed (best source VII rho 0.10, p 0.36). In the joint
   model H3, the orofacial (VII) input had a partial rho of 0.20 (p 0.011) and the septal input had -0.08
   (p 0.78). No structure model predicted held-out brain divisions (all leave-one-division-out R2 < 0).
3. The failure is not only a Knox model error. Allen tracer experiments put MS output where expected
   (septum, CA1-CA3, DG, subiculum, entorhinal cortex). The 20 strongest MS targets had twice the rhythmic share
   of other regions (0.28 against 0.135; spatial p 0.001, exploratory). But across all 198 regions the
   tracer predictor also failed (rho 0.06, p 0.33; Gad2-Cre MS only: 0.10, p 0.22), because many rhythmic
   regions get no septal input.
4. Behaviour separates the two systems. In 16 probes (8 chosen for orofacial and 8 for septo-hippocampal
   rhythmic units), 94% of rhythmic orofacial units (probe mean; 236 units) were phase locked to the lick cycle
   (Rayleigh p < 1e-6 and vector strength >= 0.1); only 2% of septo-hippocampal rhythmic units (312 units)
   were. Lick rates were 6.3-8.2 Hz. In other regions on the same probes, 42% of rhythmic units were lick
   locked (95% probe range 0.23-0.62), for example in MV, NTS, CP and cerebellar SIM, but not in VISp.
5. The planned amplitude contrast of V1 failed. Rhythm amplitude was larger inside lick bouts than outside them
   in both systems (orofacial 1.20 against 0.39; septo-hippocampal 0.34 against 0.18). The difference between
   systems was 0.30 (95% probe bootstrap -0.14 to 0.77). Phase locking, not amplitude change, separates them.

**Conclusion.** In head-fixed mice that lick for reward, brain-wide 5-11 Hz rhythmic spiking comes from at least
two systems with the same frequency: a septo-hippocampal system that does not follow the lick cycle, and an
orofacial system that does. Strong septal projection targets are rhythmic, but septal input is not a general
predictor of where rhythmic neurons are. A study that reads "theta" from spike rhythms in task data must
separate lick-locked rhythm first.

## Limitations

- The ACG is aggregated over the whole session (task, licking, wheel movement and rest). The unit index cannot
  separate theta from lick rhythm without lick times. We checked behaviour only in 16 probes and in a 40%
  window of each spike file.
- The orofacial and septo-hippocampal region lists were defined after we saw the ranked map. H2 and H3 are
  therefore not independent confirmations. H1 was specified before structure statistics.
- Knox (2019) is a voxel model; its brainstem estimates rest on few injections. The tracer check uses 14
  experiments with different Cre lines and is post hoc.
- Region shares mix cell types; we did not separate putative interneurons. The spatial null controls smooth
  spatial structure only.
- Out-of-bout periods include running and other movements. Whisking, breathing and undetected licks can also
  give 5-11 Hz rhythm. We did not have whisking or breathing signals.
- One species, one task, head-fixed animals. The result does not tell how the two systems interact.

## What is new and what remains open

New: a brain-wide map of 5-11 Hz rhythmic spiking from IBL ACGs, a pre-registered negative test of septal
mesoscale input, a tracer-based check, and a lick-phase test that separates an orofacial system from the
septo-hippocampal one. Earlier campaign work used the same ACGs for timescales (sci:3845db66) and Knox inputs
for task coding and latency (sci:cc71e4a4, sci:49479722, sci:bb0ad271); none studied rhythmicity.

Open: (1) classify every IBL unit with full-session lick, wheel and video data (about 100 GB of spike files);
(2) test whether hippocampal theta-rhythmic units outside HPF follow monosynaptic HPF input at the cell level
(for example with single-neuron projectomes); (3) test passive datasets without licking (Allen Visual Coding)
to see whether the orofacial cluster disappears; (4) whisking and breathing as further 5-11 Hz sources.

## Files

- `files/code/` - all code. `PLAN.md` and `PLAN_sha256.txt` hold the frozen plan. `run_all.sh` runs everything;
  `get_data.sh` and `04_fetch_sessions.py` retrieve external inputs into a scratch folder.
- `files/results/region_rhythm.csv` - per region: units, sessions, rhythmic share (several thresholds),
  shrunken logit share, median best frequency (IBL-derived; Allen coordinates removed).
- `files/results/tests_primary.csv`, `sensitivity.csv`, `lodo_prediction.csv`, `source_scan.csv` (rho per Knox
  source), `exploratory.csv`, `tracer_check.csv`, `tracer_topdecile.csv`, `tracer_experiments.csv`.
- `files/results/validation_*.csv` - probes, sessions, unit-level condition fits and lick locking, region
  breakdown, summary.
- `files/provenance/input_files.csv` - URL, bytes and SHA-256 of every input (shared-store files, Allen API
  JSON, IBL caches, IBL spike windows and licks).
- `files/NOTICE_EXTERNAL_DATA.md` - sources, licences and attribution.

## Reproduce

```
export SCI_DATASETS=/mnt/dell-data/shared_datasets SCRATCH=/abs/scratch \
       RESULTS=/abs/out/results FIGURES=/abs/out/figures
bash files/code/run_all.sh
```

Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, pyarrow 26.0.1, matplotlib 3.11.2, curl. Compute
is about 10 minutes on 2 CPUs; downloads are about 2.5 GB of IBL byte ranges. The 08 figure step must run
before 09 (09 removes Allen-derived columns from the bundled tables).

Shared-store inputs used (paths on the campaign host): `ibl-bwm-2026q2-clusters-acgs-log/clusters.acgs_log.npy`,
`ibl-bwm-2026q2-acgs-log-times/acgs_log.times.npy`, `ibl-bwm-2026q2-clusters/clusters.pqt`,
`knox2019-normalized-connection-density-20261109/normalized_connection_density.csv.gz`,
`allen-structure-graph1-20261110/structure_graph_1.json`, `allen-ccf2017-annotation100-20261110/annotation_100.nrrd`
(hashes in `files/provenance/input_files.csv`; all equal the store records).
