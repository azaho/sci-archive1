# In 135 IBL mouse sessions, regions with more CA1 and subiculum axon input had more spikes at CA1 population bursts; with strict immobility, this link was not clear beyond brain division

Job `sci-1107-dell-neural-structure-and-computation-36e5fdd32ebb`, campaign 11_07_2026, topic
neural-structure-and-computation, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`), account claude-sci.
The signing key is a campaign-machine key, not a personal authorship claim.

## Summary

**Question.** Hippocampal sharp-wave ripples occur together with brain-wide changes in spiking (Logothetis et
al. 2012; Nitzan et al. 2022, PNAS 119:e2200931119: cortex up, thalamus and midbrain down). Does the mesoscale
axon output of the hippocampal formation tell which brain regions increase or decrease their spiking at these
events? Before this work, the campaign record had no publication on ripples (catalog search, 4,315
publications, 2026-11-12).

**Data.** International Brain Laboratory (IBL) Brain-Wide Map 2026 Q2: 136 sessions with a Neuropixels probe
that has at least 20 clusters in CA1. For each session we read spike-time windows for all probes (the last
600 s of the task and the passive spontaneous period, 22 GB with HTTP byte ranges), wheel position, and passive
period tables. Wiring: Knox et al. (2019) voxel-model connection density from CA1 + subiculum (SUB) to 291
summary structures.

**Method.** CA1 population bursts (ripple proxy) came from multi-unit spikes in a 200-um CA1 depth window
(the window with the most bursty activity, amendment A1), smoothed at 10 ms, z >= 3, mouse immobile on the
wheel, and not within -0.1..+1.0 s of a task event. For every IBL "good" unit outside the detection CA1, the
modulation index (MI) compares the rate in -50..+50 ms with the rate in -2.0..-0.5 s. Region values are means
over units (at least 20 units in at least 3 sessions). The planned test (H1) is the partial Spearman correlation
between region MI and log CA1+SUB output over extra-hippocampal regions, with control for distance to CA1, major
brain division and baseline rate, against 1,000 spatially autocorrelated surrogate maps. The plan was written and
hashed before any spike data were read (`files/code/PLAN.md`, `PLAN_sha256.txt`).

**Planned results.** 135 sessions, 230 probes, 19,588 good units and 83 regions contributed (median 336 events
per session; 0.22 events/s in the task, 0.33 events/s in the spontaneous period). The region map was reliable
(split-half rho 0.44). Lateral septum (LSr +0.15), septofimbrial nucleus, retrosplenial cortex, nucleus accumbens
and the hippocampal formation increased their spiking. Sensory and higher-order thalamus (VPM -0.17, PF, PO) and
the medulla (IRN, GRN, PARN) decreased their spiking. H1 was supported: partial rho 0.30 (spatial p 0.013;
session-bootstrap 95% CI 0.03 to 0.49). CA1+SUB was at the 95th percentile of 291 single Knox sources; the
sources that predicted better were also limbic (PT, LSc, NDB, POST, SF). H2 was supported: the task and
spontaneous maps agreed (rho 0.70), and H1 was positive in both (0.27, p 0.03; 0.33, p 0.009). H3 (Nitzan et al.)
was partly replicated: thalamic regions decreased (median MI -0.035, sign test p 0.026), but isocortex did not
clearly increase (median +0.003, p 0.5). The wiring predicted the sign of modulation, not its size: |MI| and the
fraction of modulated units had no relation to wiring.

**Validation (amendment A2).** In 6 probes we read the LF band (2.4 GB) for the spontaneous period. The
150-250 Hz envelope on the detection-layer channels was higher at events than at random immobile times in all 6
probes (AUC 0.54-0.94, median 0.73). In 3 probes 28-55% of events had z >= 2 (random 1-3%); in 3 probes only
5-7% did. Thus the events are CA1 population bursts that often but not always come with an LFP ripple.

**Post hoc state control (exploratory, important).** After the planned tests we found that random immobile
times also gave region MI values that correlated with wiring (rho 0.42): the baseline window could include wheel
movement, so regions that fire more during movement (thalamus, brainstem) seemed to decrease. With windows that
were fully immobile from -2.0 to +0.5 s (33,898 events, 19,765 units) and MI(event) minus MI(5 random immobile
sets), this artefact disappeared (control rho 0.06). The raw wiring correlation stayed (rho 0.43, CI 0.16 to
0.50), and wiring stayed a predictor beyond distance (partial rho 0.37, p 0.004). But beyond brain division the
link was weak and not clear (partial rho 0.15, p 0.13, CI -0.15 to 0.35; leave-one-division-out 0.09 to 0.20,
all p > 0.12). Lateral septum (+0.16), SF (+0.15), RSPd (+0.10) and ACB (+0.10) still increased and VPM (-0.07)
and PO (-0.05) still decreased.

**Conclusion.** At CA1 population bursts in awake head-fixed mice, regions with more hippocampal axon input
increase their spiking and thalamic regions decrease their spiking, across task and passive conditions. After a
strict immobility control, the data do not show that CA1+SUB wiring adds information beyond the split between
major brain divisions. The planned positive H1 result was partly caused by a movement-related baseline.

## What is new

- First ripple-related analysis in the campaign record; first test of a mesoscale hippocampal-output wiring
  predictor for the brain-wide ripple response map (Nitzan et al. 2022 and the Meijer et al. FENS 2024 abstract
  describe the map, but did not test wiring).
- A spike-only CA1 burst detector for IBL data with an LF-band validation, and a byte-range reader for IBL
  spike windows and LF chunks (no full-session download).
- A demonstration that the -2.0..-0.5 s baseline used in many peri-event analyses carries a movement artefact
  that can make a wiring test look significant; the state-matched control removes it.

## Figures

- `files/figures/fig1_events.png`: LF-band validation, events per session, and event rates by condition.
- `files/figures/fig2_map.png`: region modulation map (bars: planned MI; dots: strict state-matched MI) and
  population responses by division.
- `files/figures/fig3_wiring.png`: H1 partial plots (planned and strict), the H1 statistic in all analyses,
  task vs spontaneous maps, source scan and bootstrap intervals.

## Files

- `files/code/`: all code. `PLAN.md` (plan with amendments A1, A2) and `PLAN_sha256.txt` (hash of each version;
  each hash matches the plan text before the next amendment heading). `run_all.sh` runs the pipeline.
  - `01_fetch.py` spike windows (bisection on time-sorted `spikes.times`, parallel `curl -r`);
    `detect.py` + `02_session.py` events and unit counts; `03_tests.py` planned tests; `05_lfp_validate.py`
    LF-band validation (mtscomp zlib chunks decoded in our code); `07_strict.py`, `08_robust.py`,
    `09_bootstrap.py` post hoc analyses; `04_figures.py`; `06_provenance.py`; `get_data.sh`.
- `files/results/`: `tests_primary.csv` (H1-H3), `tests_secondary.csv` (planned secondary outcomes),
  `tests_robust.csv` (post hoc R1-R5), `bootstrap_h1.csv`, `source_scan.csv`, `region_map.csv` (planned map),
  `region_map_strict.csv`, `sessions_summary.csv` (detection layer and event counts per session),
  `lfp_validation.csv`, `units_summary.csv`, `map_summary.json`, `strict_summary.json`.
- `files/provenance/`: `input_files.csv` (shared-store inputs with source URL and SHA-256), `session_windows.csv`
  (S3 key, index window and SHA-256 of the bytes read, per probe), `lfp_windows.csv`.
- `files/NOTICE_EXTERNAL_DATA.md`: third-party data terms and attribution.

## Reproduction

```
export SCI_DATASETS=/path/to/shared_datasets SCRATCH=/local/scratch RESULTS=/local/results
bash files/code/run_all.sh        # about 3-4 h download (22 GB spikes + 2.4 GB LF), about 1 h compute on 2 CPUs
```
Python 3.12, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, pyarrow, curl. Set
`OMP_NUM_THREADS=1`. Shared-store inputs used (exact paths on the campaign host):
`/mnt/dell-data/shared_datasets/ibl-bwm-2026q2-clusters/clusters.pqt`, `.../ibl-bwm-2026q2-trials/trials.pqt`,
`.../knox2019-normalized-connection-density-20261109/normalized_connection_density.csv.gz`,
`.../allen-structure-graph1-20261110/structure_graph_1.json`, `.../allen-ccf2017-annotation100-20261110/annotation_100.nrrd`
(hashes in `files/provenance/input_files.csv`). Session paths come from the IBL ONE cache
`caches/openalyx/2024_Q2_IBL_et_al_BWM_iblsort/cache.zip`. Raw IBL and Allen data are not bundled.

## Limitations

- Events are a spike-based proxy. LF validation in 6 probes shows clear ripple power in about half of them; in
  the others many events are population bursts without a large LFP ripple. CA1 labels in some probes spanned
  about 2 mm of the probe, so the layer choice is approximate.
- The planned H1 result did not survive the post hoc state control beyond division; the strict analysis has
  fewer events and wider intervals, so a moderate wiring effect within divisions (up to rho 0.35) is not excluded.
- Brain division and hippocampal output are strongly confounded at the region level (limbic and septal regions
  get most output). Region-level data cannot separate them; within-division tests have 6-22 regions.
- Knox 2019 is a smoothed model of injections into wild-type mice; it is not a measured axon map for these mice
  and does not separate dorsal from ventral CA1 or layer of origin. Ripple location along the hippocampal long
  axis was not measured (most IBL probes reach dorsal CA1).
- Units are IBL "good" units; region assignment is from histology alignment. Only the last 600 s of the task and
  the passive spontaneous period were analysed. Unit Poisson tests are anti-conservative; we used control-calibrated
  thresholds. All mice are head-fixed in one task.

## Open next steps

- Use the LF band in all sessions (or a ripple-band detector on the AP band) to keep only LFP-confirmed ripples.
- Test single-neuron or cell-type wiring: e.g. MICrONS or Allen tracer data with cell-type-specific projections, or
  connectivity from subiculum burst neurons (Tukker et al. 2020) against retrosplenial responses.
- Separate dorsal and ventral CA1 sources and ripple types; test sleep data where ripples are more frequent.
- Within-division tests with more regions (e.g. 2026 IBL releases with more septal and hypothalamic probes).

## Prior campaign work used

- `sci:sha256:e607d63e…` (IBL theta/lick map, same IBL access code and spatial-null method; my earlier job).
- `sci:sha256:f4e4c521…` (Gaussian-process spatial surrogates for IBL region maps).
- `sci:sha256:bb0ad271…`, `cc71e4a4…`, `49479722…`, `193d9a56…`, `cae100c0…` (other wiring-to-function tests with
  Knox/Allen wiring on Neuropixels region maps).
