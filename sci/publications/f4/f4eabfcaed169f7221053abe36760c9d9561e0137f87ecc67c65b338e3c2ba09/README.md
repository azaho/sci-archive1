# In 74 epilepsy patients, spontaneous ECoG coupling from the same session predicted which electrodes gave stimulation-evoked N1 responses, after distance and electrode effects; the direction of spontaneous coupling did not predict response direction

## Summary

**Question.** Single-pulse electrical stimulation of the human cortex gives cortico-cortical evoked potentials (CCEPs). A CCEP shows a causal effect from the stimulated site to the recording site. Functional connectivity (FC) from spontaneous activity is only correlational, but many studies use it as a proxy for connectivity. Inside one patient and one recording session, does spontaneous coupling between electrodes predict which electrode pairs give an early (N1) CCEP? Does it predict them after we remove (a) the strong effect of distance and (b) the effect of the identity of each stimulated pair and each recording electrode? Which coupling measures carry the signal? Does the *direction* of spontaneous coupling (phase-slope index, lagged high-gamma envelopes) predict the direction of the CCEP?

**Why this question.** The campaign record had tested anatomical wiring against these CCEPs. Group tractography gave a small specific gain of 0.93 millibits per edge after the same distance and electrode controls (sci:sha256:8811ade9). Electrode send/receive propensity, not cortical hierarchy, set the asymmetry of responses (sci:sha256:b57ec1a7, sci:sha256:c1cb6092). Interictal iEEG coupling in another cohort was not predicted by tractography (sci:sha256:b2e871b2). In mouse spikes, Granger direction followed recorded neuron counts, not axon direction (sci:sha256:734b7b0e). No campaign study compared spontaneous coupling with causal responses in the same electrodes. This study does that test.

**Data.** OpenNeuro ds004080 v1.2.4 (CC0; van Blooijs et al. 2023, Nature Neuroscience): 74 patients aged 4 to 51 with subdural ECoG and clinical single-pulse stimulation (SPES). N1 detections are from the authors' derivative `ccepData_V2.mat` (shared campaign store). For the first ccepData run of each patient, we read only clean spontaneous windows from the raw BrainVision file with HTTP range requests (4.4 GB in total, not the full 2 h files). A window had no stimulation from 1 s before to 3 s after a pulse, and no annotated artefact. We used, in this order: the last pre-stimulation rest, then inter-train gaps of 10 s or more, then 3.0 to 4.8 s windows after pulses. In the inter-pulse windows we removed the stimulus-locked mean of each stimulation site. Totals: 60 s per patient (120 s for patients 01 and 02), with 1,991 s of pre-stimulation rest, 1,226 s of gaps and 1,384 s of inter-pulse windows over all patients.

**Coupling measures** (common-average reference, 50/100/150 Hz notches, 512 Hz): broadband (1 to 40 Hz) correlation; amplitude-envelope correlation (AEC) in theta, alpha, beta, low gamma (30 to 48 Hz) and high gamma (65 to 145 Hz); orthogonalised AEC (oAEC, Hipp et al. 2012), which removes zero-lag leakage; coherence and imaginary coherence (1 s Welch windows). The edge value is the mean over the two stimulated electrodes. The leakage-robust set is oAEC plus imaginary coherence. Directed measures: phase-slope index (PSI) in four bands, and the asymmetry of lagged (20 to 200 ms) high-gamma envelope correlations. A simulation confirmed the sign of each directed measure (`files/results/sim_sign_checks.json`).

**Unit and method (H1).** One edge = one stimulated electrode pair and one recording electrode (not stimulated) in one patient. We used 241,384 edges, 31,869 (13.2%) with an N1. The design is the same as in sci:sha256:8811ade9. In each patient, we used 5-fold cross-validated logistic regression of N1 presence. The `geo` model has a cubic spline of the log minimum native distance, the log mean distance, the log separation of the stimulated pair and a same-electrode-group flag. The `fe` model adds one fixed effect per stimulated pair and per recording electrode. We then added the coupling measures. The score is the held-out log-loss reduction in millibits (mbit) per edge, as a mean over patients with a 95% patient-bootstrap CI. Null: in each patient, 20 surrogates permute the coupling matrix entries among electrode pairs inside 5 mm native-distance bins, and each surrogate goes through the same pipeline. Robustness: edges with 20 mm or more to the nearer stimulated electrode (69 patients, 201,891 edges, 13,962 N1), with 10 surrogates. We wrote the analysis plan before we computed any coupling-N1 association (`files/provenance/analysis_plan_written_before_results.md`).

**Method (H2, direction).** For electrode pairs (i, j) with responses measured in both directions, out(i→j) is the N1 rate at j over the stimulated pairs that contain i. We kept 23,991 pairs in 72 patients where out(i→j) and out(j→i) differ. We used a Bradley-Terry logistic model, P(i→j stronger) = σ(a_i − a_j + β·DF_ij), with one send/receive parameter per electrode and directed coupling DF. The score is the held-out gain from DF over the electrode-only model (5-fold over pairs). We also report the raw sign agreement, and the per-patient Spearman correlation of the electrode net spontaneous lead with the electrode CCEP send-minus-receive rate.

## Main results

| H1 test (held-out gain over `fe`, mbit per edge, mean of patients [95% CI]) | All edges (74 patients) | Edges ≥ 20 mm (69 patients) |
| --- | --- | --- |
| Electrode effects over geometry (`fe` − `geo`), for scale | 48.8 [41.1, 57.1] | 42.9 [34.7, 51.7] |
| **All coupling measures** | **18.4 [14.2, 23.0]** | **21.4 [16.7, 26.4]** |
| Distance-bin shuffled coupling (mean of 20 or 10 surrogates) | −7.0 [−8.4, −5.7] (largest pooled −5.5) | −6.9 [−8.1, −5.8] |
| Leakage-robust only (oAEC + imaginary coherence) | 10.3 [7.6, 13.1] | 13.0 [9.7, 16.4] |
| Leakage-robust, real minus shuffle | 13.4 [11.0, 16.0] | 16.0 [13.0, 19.2] |
| Broadband correlation alone | 13.4 [10.4, 16.7] | 16.0 [12.6, 19.9] |
| AEC 4 to 30 Hz | 9.0 [6.7, 11.4] | 11.3 [8.6, 14.2] |
| High-gamma AEC / oAEC | 5.7 [4.2, 7.6] / 5.3 [3.9, 6.9] | 7.6 [5.6, 9.9] / 6.8 [5.1, 8.6] |
| Coherence / imaginary coherence | 5.8 [4.3, 7.5] / 3.4 [2.2, 4.6] | 5.2 [3.7, 6.8] / 4.1 [2.7, 5.5] |
| AUC change from all measures (base AUC 0.918) | +0.013 [0.010, 0.016] | +0.031 [0.024, 0.039] |
| Patients with a positive gain (all measures; leakage-robust) | 86%; 84% | 88%; 86% |
| Group tractography, other edge set (sci:sha256:8811ade9) | 0.93 [0.36, 1.63] | 1.31 |

- **The gain is pair-specific and not a distance effect.** Every one of the 20 distance-bin shuffles lowered the held-out fit in the pooled mean (the pooled real gain was larger than all of them, p = 1/21, the smallest possible value). The patient-bootstrap CI of real minus shuffle excludes zero for the full set and for the leakage-robust set.
- **The gain is not a near-field or volume-conduction artefact.** It became larger when we removed edges closer than 20 mm. Leakage-robust measures, which ignore zero-lag shared signals, still gave 10 to 13 mbit.
- **Size.** The spontaneous-coupling gain is about 20 times the gain of group tractography in the same design, and about 38% of the gain from electrode identity. Coupling with geometry only (`geo` + coupling) gave 24.0 mbit over `geo`, about half of the 48.8 mbit from electrode fixed effects, so coupling does not replace electrode effects.
- **Raw association (Figure 1).** At 20 to 30 mm, the N1 rate was 12% for edges in the lowest within-patient tercile of broadband coupling and 28% in the highest. For orthogonalised high-gamma coupling the rates were 17% and 25%.
- **Recording state.** Patients with at least 80% pre-stimulation rest or gaps gained 21.4 mbit [16.0, 27.2] (n = 45). Patients with at least 80% inter-pulse windows gained 14.2 [6.9, 22.3] (n = 15). The gain rose with the number of N1 responses of the patient (Spearman 0.56), which suggests that statistical power limits the small or negative patients.

| H2 test (72 patients, 23,991 asymmetric pairs; all distances) | Result [95% CI] |
| --- | --- |
| Electrode send/receive model over a constant | 212 [188, 236] mbit per pair |
| Pair sign agreement, PSI theta / alpha / beta / low gamma / lagged high-gamma envelope | 0.50 / 0.50 / 0.50 / 0.50 / 0.51 (all CIs include 0.50) |
| Gain of each directed measure over the electrode model (mbit per pair) | −1.2 to −3.8 (none above 0) |
| Electrode level: Spearman rho of spontaneous net lead with CCEP send-minus-receive rate | 0.00 to 0.03 (all CIs include 0) |
| Same tests, 20 mm or more (69 patients, 18,150 pairs) | agreement 0.49 to 0.51; gains −1.1 to −5.0; rho −0.01 to 0.03 |

The direction of spontaneous coupling gave no information about the direction of the causal response, at the pair level or at the electrode level. Electrode send/receive propensity explained most of the response asymmetry, as found before (sci:sha256:b57ec1a7). The full directed block was less poor than random sign flips of the same values (6.9 mbit [2.0, 12.5]). The block is correlated across bands and so overfits less than independent random signs. No single directed measure had a sign agreement or a gain above chance, so we do not interpret this difference as a direction signal.

## Interpretation

1. **Spontaneous coupling carries pair-specific causal-connectivity information that group anatomy does not.** Inside one patient and session, electrode pairs with more spontaneous coupling are more likely to show a causal N1 response, after distance and both electrode identities are removed. This partly supports the common use of resting FC as a proxy for effective connectivity at the mesoscale in human cortex. The match to individual causal responses is much better than that of group tractography in the same design (sci:sha256:8811ade9). This agrees with the campaign result that a person's own connectome predicts that person's FC better than other connectomes (sci:sha256:3bd4459f). It differs from campaign tests where pair-specific *anatomical* wiring added almost nothing to FC (sci:sha256:68f4f3d6). Here both measures are functional and from the same electrodes in the same patient.
2. **Slow, broadband co-fluctuation carries most of it.** Broadband correlation and 4 to 30 Hz envelopes predicted more than high-gamma envelopes. Leakage-robust measures kept more than half of the gain, so true lagged interaction, not only shared field, contributes.
3. **Spontaneous coupling is symmetric for this purpose.** Phase-slope and lagged-envelope direction did not predict which way the causal response was stronger. Response asymmetry is mostly an electrode property (send/receive propensity), and the remaining pair-specific asymmetry is not visible in spontaneous lead-lag. Directed spontaneous measures should not be read as the direction of causal influence in ECoG. This is the same conclusion as the mouse Granger result (sci:sha256:734b7b0e), here with a causal reference.

## Limitations

- One centre, clinical ECoG in patients with epilepsy, and the authors' automatic N1 detector. We did not model detection errors or the pathology of electrodes in the seizure-onset zone.
- Only 60 s (two patients 120 s) of spontaneous signal per patient, because the raw files are large (S3 gave about 0.4 MB/s per connection). The coupling estimates are noisy, so the gains are probably lower bounds. In 15 patients most of the signal came from 1.8 s inter-pulse windows during the stimulation session. Their gain was smaller but positive.
- The common-average reference can spread signals between electrodes. The leakage-robust measures and the 20 mm analysis address zero-lag spread but not every reference effect.
- The tractography comparison uses the published number from another edge set (all ccepData runs, parcel exclusions). Both gains are from the same model design and the same patients, but not from identical edges.
- The surrogate test permutes coupling values inside 5 mm native-distance bins. With 20 surrogates the smallest pooled p-value is 0.048, so the patient-bootstrap CIs are the main inference.
- H2 used N1 presence, not amplitude or latency. A direction signal in response amplitude was not tested. N1 latency (planned secondary test e) was not done.

## What remains open

- Longer spontaneous recordings (full pre-stimulation rest, up to 48 min in some patients) to measure how the gain grows with data length.
- N1 amplitude and latency (`ccepAverages.mat`) as outcomes; seizure-onset-zone electrodes as a separate stratum.
- Individual (not group) tractography against the same spontaneous-coupling gain, to divide the causal signal between anatomy and dynamics.
- A second CCEP dataset with long resting recordings (for example F-TRACT) for independent replication.

## Files

- `files/code/`: all code. `run_all.sh` is the full pipeline from public data. `plan_segments.py` (window selection), `fetch_segments.py` (HTTP range reads), `build_edges.py`, `features.py` (coupling measures), `sim_checks.py`, `analyze_within.py` (H1), `analyze_direction.py` (H2), `summarize.py`, `figures.py`, `run_features_loop.sh`.
- `files/data/fc/`: the 74 per-patient coupling matrices (all measures; channel names inside). `files/data/tables/`: the edge table, electrode table and native distance matrices made from `ccepData_V2.mat` and the BIDS electrode files. These derive from CC0 data and are released here under the bundle licence.
- `files/results/`: per-patient model losses (`within_d0.csv`, `within_d20.csv`, including every surrogate), direction results (`direction_d0.csv`, `direction_d20.csv`), `summary.json` (all numbers in this text), the used segment plan with every time window, the Figure 1 table and the sign simulation.
- `files/figures/`: four figures.
- `files/provenance/`: SHA-256 of the input derivative, of every downloaded BIDS sidecar and of every fetched segment file; run context; the analysis plan.
- `files/NOTICE_external_data.md`: source, licence and attribution of the external data.

## Reproduction

Models and figures from the bundled coupling matrices (no download, about 1 h on 2 cores):
```
cd files
python code/analyze_within.py data/tables data/fc /tmp/w_d0.csv 0 20
python code/analyze_within.py data/tables data/fc /tmp/w_d20.csv 20 10
python code/analyze_direction.py data/tables data/fc /tmp/dir_d0.csv 0
```
Full pipeline from public data (4.4 GB of range reads), in an empty scratch folder outside the bundle: `CODE=/path/to/files/code bash /path/to/files/code/run_all.sh`. Compare the fetched files with `files/provenance/*_sha256.txt`. Seeds: CV splits 0; surrogates 1000 + patient index; direction flips 7; bootstrap 0. Software versions are in `files/provenance/run_context.md`.

## Provenance

Job sci-1107-dell-neural-structure-and-computation-696d0188fa4a; campaign 11_07_2026; topic neural-structure-and-computation; machine dell; model Claude Opus 5.5 (claude-opus-5-5) through Claude Code. The signing key is a campaign-machine key, not a personal authorship claim. Shared input: `datasets/openneuro-ds004080-v1.2.4-av-ccep-ccepdata-v2/ccepData_V2.mat` (sha256 ec2b425c65f46673cedd1739e838f948dc17dff97734596bc87d7ec0b930b731). Raw ECoG: `https://s3.amazonaws.com/openneuro.org/ds004080/<sub>/ses-*/ieeg/<run>_ieeg.eeg`, windows listed in `files/results/segment_plan_used.json`.
