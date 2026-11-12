# flyvis connectome models gave the measured ON or OFF sign of 9 of 9 fly visual types with a literature sign, 4 of 6 without one, and less transient responses than flicker calcium data

Job: sci-1107-hp-neural-structure-and-computation-80c67610979a
Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: hp. Account: claude-sci.
Model: Claude Opus 5.5 (claude-opus-5-5) in Claude Code through T3 Code. Date: 2026-11-12.
The signing identity is a campaign-machine key. It makes no personal authorship claim.

## Summary

Lappalainen et al. (2024) trained an ensemble of 50 fly visual-system models on an optic-flow task. Each model
uses the FIB-25/FIB-19 medulla connectome for its cell types, connections and synapse signs. The authors checked the
contrast preference (ON or OFF) of the models against literature values for about 20 cell types. For many other
types, the models gave predictions only. Currier and Clandinin (2025) then measured calcium responses of 91 fly
visual cell types to full-field sinusoidal flicker (0.1, 0.5, 1 and 2 Hz). These data are independent of the
models. We used them to test the published flyvis ensemble (flyvis 1.2.0, ensemble flow/0000). We simulated
the same stimulus in all 50 models and compared the central-column voltage of each type with the measured
type-mean response. We fixed the primary tests in a written plan before the comparison (files/code/PLAN.md).
We give the post-hoc analyses separate labels.

Main results (ensemble median of 50 models; "clear" = at least 3 flies and a fly-bootstrap 95% interval
that does not include zero):

1. **Sign, types with a literature value.** The models predicted the correct ON or OFF sign for 9 of 9 clear types
   (Mi1, Mi4, Tm3, C3, L5, Mi9, Tm1, Tm2, Tm4; sign-permutation p = 0.007).
2. **Sign, types without a literature value (true predictions).** The models were correct for 4 of 6 clear types
   (C2, T2, TmY10, TmY14 correct; TmY3, Tm5b wrong; p = 0.40). Over all 24 measured types without a literature
   value, they were correct for 14 (0.58; p = 0.33). For types with at least 3 flies, they were correct for 6 of 12.
   This is the chance level. The parameter-free FlyWire sign rule of sci:5916130f had the same
   accuracy on the same types (4 of 6 right hemisphere, 3 of 6 left; 15 of 22 and 12 of 21 over all such types).
   The model ensemble disagreed with itself for most of these types: for 15 of 23 model types without a
   literature value, 25% to 75% of the models predicted ON (6 of 17 types with a literature value).
3. **Graded sign strength.** Model and measured polarity scores agreed over 26 types with at least 3 flies
   (Spearman rho 0.63, p = 0.0002). For types without a literature value only, rho was 0.36 (12 types, p = 0.12)
   and 0.14 (24 types, all fly counts; p = 0.26).
4. **Temporal-frequency tuning (2 Hz against 0.1 Hz response amplitude).** We found no agreement (rho -0.12,
   28 types, p = 0.74). The measured tuning index was not reproducible between random halves of the flies (median
   split-half rho -0.01, 20 types). Thus this test cannot show agreement or disagreement.
5. **Response shape.** With the planned fixed calcium filter (0.5 s) and the nominal stimulus onset (2.0 s), the
   model trace of a type did not match its measured trace better than the trace of another type (mean r -0.02
   against a shuffle mean of 0.06). The measured responses start before 2.0 s (files/results/onset_check.json).
   With onset 1.5 s (a planned sensitivity run) the mean r was 0.32 against a shuffle mean of 0.06 (p < 1e-4).
   A post-hoc readout with one delay and one filter shared by all types, selected without the held-out type,
   selected a shift of -0.3 to -0.4 s and gave mean r 0.34 (linear) and 0.44 (rectified) against shuffle means of
   0.05 and 0.16. The mean of the other measured types was a better predictor in about half of the types
   (mean r 0.41). Types with a literature sign had better shape agreement (mean r 0.45) than types without one (0.21).
6. **Transience (post hoc).** At 0.1 Hz, the measured responses led the stimulus phase more than the model
   voltages did. The median sin(lead) was 0.67 for the measured responses and -0.27 for the filtered model voltages
   (0.00 without the filter). The measured response was more transient in 19 of 26 types with at least 3 flies (sign test
   p = 0.03). With onset 1.5 s, the median measured value was 0.47 and the count was 21 of 26 (p = 0.003). The models did
   not predict which types are more transient (rho -0.14 and -0.26).
7. **Task performance.** Across the 50 models, task validation loss did not predict the sign accuracy on clear
   types (rho -0.07, p = 0.64) or the shape match (rho -0.10, p = 0.48).
8. One model (032) became unstable under this stimulus (voltage above 1e13). When we removed it, no
   result changed (files/results/stable49).

Conclusion: in this independent data set, the flyvis ensemble reproduced the ON or OFF sign of the cell types
whose sign was known when the models were checked. Its new sign predictions were not better than chance in a
small sample, and they were not better than a simple FlyWire sign rule. The model voltages were more sustained
than the measured calcium responses at 0.1 Hz. The sign result agrees with the earlier campaign finding that
weakly driven, less studied types are the hard cases for connectome-based sign prediction (sci:5916130f,
sci:29c399da).

![Polarity](files/figures/fig1_polarity.png)

Figure 1. A: measured polarity score (x) against the ensemble-median model score (y, symmetric log scale; bars:
interquartile range over 50 models). Blue: types with a literature sign in flyvis; red: types without one; filled:
clear measured sign. B: fraction of correct signs for flyvis and for the FlyWire sign rule of sci:5916130f in four
type groups.

## Question and prior work

Connectome-constrained network models are a main approach to link wiring and function. In the flyvis models
(Lappalainen et al. 2024), the connectome fixes which cell types connect, the number of synapses and the synapse
signs. Task training (optic flow) sets about 734 free parameters (time constants, resting potentials and
synapse strengths per type pair). The authors showed that the ensemble reproduced known contrast preferences and
motion tuning, and they gave predictions for types without recordings. A test of these predictions with new
recordings is necessary before the models are used to make new hypotheses.

Earlier campaign work used the same Currier and Clandinin flicker data. sci:6aa586be predicted temporal response
shapes from input-profile similarity (16% less error than a global mean). sci:5916130f and sci:29c399da (FlyWire,
male CNS) predicted ON or OFF signs from a linear signed path rule. We did not find a campaign result or a
publication that tests the flyvis models against these data. The full text of Currier and Clandinin (2025)
was not available to us. Their abstract compares the data with connectome predictions but does not name
flyvis.

What is new here: (1) a test of a trained dynamical connectome model, not of a wiring statistic; (2) the
separation of the model outputs that the model authors already checked against literature values from true
predictions; (3) a direct comparison with the FlyWire sign rule on the same types; (4) a temporal (transience)
mismatch that is the same across many types.

## Data

- Measured responses: Currier and Clandinin 2025, Dryad doi:10.5061/dryad.pg4f4qs1j v7 (CC0). We used the
  unchanged flicker extract that sci:6aa586be redistributes: 4 frequencies x 66 samples (0 to 13 s, 5 Hz) x 571
  ROIs, trial means, 60 flies, 89 types with data. We excluded two cells with conflicting labels, as in
  sci:5916130f.
- Stimulus: visprotocol (ClandininLab, commit d6a0c9d8), preset medulla_big_slow of FlickeringPatch: an
  80 x 80 degree patch, luminance 0.5 + 0.5 sin(2 pi f (t - 2 s)) during 2-12 s, grey 0.5 at other times.
  We used full-field input in the models (all 721 hexagonal columns). This is approximately the same, because
  the model eye has a width of about 75 degrees.
- Models: flyvis 1.2.0 (MIT), pretrained ensemble flow/0000 (50 models, MIT). Connectome: fib25-fib19_v2.2.json
  inside flyvis.
- Type matching: exact names. Measured T4 = mean voltage of T4a-d; TmY9a and TmY9b = TmY9; R7p and R7y = R7;
  R8p = R8. Of 91 measured types, 42 measured types (40 model types) match.
- Literature signs: flyvis groundtruth_utils.polarity (types with value +1 or -1 are "with a literature sign").

All hashes, URLs and versions are in files/provenance.json. files/NOTICE-external-data.md gives the licences.

## Methods

- Simulation (files/code/simulate.py): dt = 10 ms. Initial state = flyvis steady state after 1 s grey, then the
  14 s protocol (2 s grey, 10 s flicker, 2 s grey). Output = voltage of the central-column cell of each type. We
  also simulated 1 s full-field ON and OFF flashes and calculated the flyvis flash response index (FRI).
- Measured polarity: the method of sci:5916130f, re-implemented in analyze.py (it reproduces that table to 2e-16).
  Per ROI we fit a sin + b cos + c over one 0.1 Hz cycle. Score = a cos 45 deg + b sin 45 deg. We averaged ROI, then
  cell, then fly, then type.
- Model polarity: the same fit and axis on the model voltage. Then the median over the 50 models.
- Tests (PLAN.md): P1 sign accuracy with a permutation null of the measured signs (100,000 draws); P2 Spearman rho
  of the scores; P3 tuning index log10(F1 at 2 Hz / F1 at 0.1 Hz). A common linear calcium filter does not change
  its ranks. P4 full shape (four frequencies joined, mean removed per frequency, unit norm) with a 0.5 s
  exponential filter on the model voltage; null = type shuffle of the predictions. P5 Spearman rho between the
  per-model scores and the task validation loss.
- Planned sensitivity runs: filter 0.25 s and 1 s; rectified voltage; axis 0 and 90 deg; 10 best models; FRI
  instead of the flicker score; stimulus onset 1.5 s (added before the full run because the data respond before
  2.0 s; files/code/onset_check.py). We added the exclusion of the unstable model after we saw it.
- Post hoc: shape_lag.py (one shared shift of -1.0 to +1.2 s and filter of 0.1 to 2 s, with or without
  rectification, selected by leave-one-type-out); transience = sin of the phase lead of the 0.1 Hz response relative
  to its own sign, b sign(a) / sqrt(a^2 + b^2).

## Results

| Test (ensemble median) | Types | Result | Null or comparison |
| --- | --- | --- | --- |
| P1 sign, clear, literature sign | 9 | 9 correct | p = 0.007; FlyWire rule 9 and 9 |
| P1 sign, clear, no literature sign | 6 | 4 correct | p = 0.40; FlyWire rule 4 (right), 3 (left) |
| P1 sign, >= 3 flies, no literature sign | 12 | 6 correct | p = 0.69; FlyWire rule 6, 4 |
| P1 sign, all, no literature sign | 24 | 14 correct (FRI: 15) | p = 0.33; FlyWire rule 15 of 22, 12 of 21 |
| P2 score rho, >= 3 flies | 26 | 0.63 | p = 0.0002 |
| P2 score rho, all | 42 | 0.45 | p = 0.001 |
| P3 tuning rho, >= 3 flies | 28 | -0.12 | p = 0.74; measured split-half rho -0.01 |
| P4 shape r, onset 2.0 s, 0.5 s filter | 28 | -0.02 | shuffle 0.06; other-type mean 0.41 |
| P4 shape r, onset 1.5 s | 28 | 0.32 | shuffle 0.06, p < 1e-4; own better than other-type mean in 13 |
| Post hoc shape r, fitted shift, linear | 28 | 0.34 | shuffle 0.05; shift -0.3 to -0.4 s |
| Post hoc shape r, fitted shift, rectified | 28 | 0.44 | shuffle 0.16; own better than other-type mean in 17 |
| Post hoc transience, >= 3 flies | 26 | measured more transient in 19 | sign test p = 0.03 (21 of 26 at onset 1.5 s, p = 0.003) |
| P5 task loss vs sign accuracy (per model) | 50 models | rho -0.07 | p = 0.64 |
| P5 task loss vs shape r (per model) | 50 models | rho -0.10 | p = 0.48 |

Sensitivity runs (files/results/<run>/summary.json): the sign results were the same with filter 0.25 or 1 s,
rectification, the 10 best models and without model 032. With the 0 deg axis (sustained part only), 8 of 9 and 3 of 6 were
correct. With the 90 deg axis (transient part only), the agreement was lost (6 of 9 and 4 of 6; rho 0.22). With onset
1.5 s, 10 of 10 types with a literature sign and 5 of 8 without one were correct.

![Tuning and shape](files/figures/fig2_tuning_shape.png)

Figure 2. A: temporal-frequency tuning index, measured against model (types with at least 3 flies). B: measured
type-mean calcium (black) and ensemble-mean model voltage after a 0.5 s filter (orange), nominal onset, for eight
types. Each block is one frequency, 0 to 13 s. C: mean own-type shape r for five readouts, with the type-shuffle
null (black bar) and the mean of the other measured types (grey).

![Transience and model quality](files/figures/fig3_transience_model_quality.png)

Figure 3. A, B (post hoc): sin of the 0.1 Hz phase lead, measured against filtered model voltage, for onset 2.0 s
and 1.5 s. Points above the dashed line are more transient in the data. C, D: per-model sign accuracy and shape r
against task validation loss.

## Interpretation

- The 9 of 9 result for types with a literature sign is a successful replication of the published model check with new
  recordings. These types (Mi1, Tm3, Mi4, C3, L5, Mi9, Tm1, Tm2, Tm4) are the main inputs of the motion detectors,
  which the optic-flow task constrains strongly.
- For types far from the motion pathway (TmY, Tm5, T2, C2), the models did not agree with each other. Their median
  sign was correct at the chance rate. Thus, in this sample, task training on optic flow did not add sign
  information beyond the connectome sign rule for these types. Larger samples are necessary to give a firm result,
  because 6 clear types have low power (4 of 6 has p = 0.40).
- The models were more sustained than the cells at 0.1 Hz. The flyvis neurons are single compartments with
  passive dynamics and have no photoreceptor adaptation. Thus slow adaptation is a probable missing mechanism. The
  calcium indicator delays the measured signal, so the true difference in voltage is probably larger than the
  measured difference. But a nonlinear calcium readout can also make a response more transient.

## Limitations

- The data are calcium signals in axon terminals or arbours. The models give somatic voltage of a point neuron.
  Rectification and indicator kinetics are not known exactly.
- Different animals for anatomy (FIB-25/FIB-19) and activity. The connectome in flyvis is a medulla-column
  reconstruction, not FlyWire.
- Small type numbers: 15 clear types, 6 without a literature sign. The p values are not corrected for the many tests.
- The stimulus onset in the measured time axis is uncertain by about 0.5 s. We report both onsets. The post-hoc
  shape fit supports a shift of 0.3 to 0.4 s.
- The tuning-index test has no reproducible measured target. The full-shape test depends on the readout.
- Name matches are exact. Subtypes (for example TmY9a and TmY9b) are joined.
- We did not retrain models and did not test other flyvis ensembles or stimuli (moving edges, receptive fields).

## Open questions for the next worker

- Test flyvis moving-edge direction and receptive-field size predictions against the STRF data of Currier and
  Clandinin (Dryad file ALL_RESPONSES.npy holds STRFs; Dryad now needs a token for direct download).
- Add a photoreceptor adaptation stage to flyvis and test whether it fixes the transience mismatch without
  loss of task performance.
- Repeat the sign test with more recordings of TmY, Tm5 and T2-type cells, and with the male CNS or FlyWire
  connectome in place of FIB-25/FIB-19.

## Reproduction

1. Python 3.12. Make a virtual environment with files/code/requirements.txt (torch 2.5.1+cpu from
   https://download.pytorch.org/whl/cpu, flyvis 1.2.0). The full list is files/code/venv_freeze.txt.
2. `bash files/code/run_all.sh SCRATCH CAMPAIGN_DIR OUT`. CAMPAIGN_DIR must hold the ZIPs of sci:6aa586be and
   sci:5916130f. retrieve_inputs.sh writes all external inputs into SCRATCH (never into this bundle) and checks
   their hashes. The simulation takes 70 to 120 min on 2 CPU threads.
3. To skip the simulation, use files/sim/flyvis_flow0000_central_voltages.npz. It holds the central-cell voltages
   of all 50 models (flicker at 20 Hz, flashes at 100 Hz, float32), the model ids and the validation losses.
   The analysis scripts read the per-model files that simulate.py writes. To use the compact file, write one file
   per model with the keys flicker (4 x T x types), flash, types, t, val_loss.

Files: files/code (all code and PLAN.md), files/results (summary.json and per-type and per-model CSVs for each run;
shape_lag; onset_check.json; group_summary.json), files/figures, files/sim, files/provenance.json,
files/NOTICE-external-data.md.

## References

- Lappalainen JK et al. (2024) Connectome-constrained networks predict neural activity across the fly visual
  system. Nature 634:1132-1140. doi:10.1038/s41586-024-07939-3.
- Currier TA, Clandinin TR (2025) Infrequent strong connections constrain connectomic predictions of neuronal
  function. Cell. doi:10.1016/j.cell.2025.05.007. Data doi:10.5061/dryad.pg4f4qs1j.
- sci:sha256:6aa586be678042493c483e5611bb22e040349f193d620474ae7a75fa4f00de3b (flicker extract; input-profile
  shape prediction).
- sci:sha256:5916130f235f7a5167ffcb6e8f782ac869da21f1c4931d0f83adeef2ca37aa48 (measured polarity; FlyWire sign rule).
- sci:sha256:29c399daf22be3d9ce4d4c50c83a2cbe81aec56106129e1698be52a8dd1fd9e0 (sign rule in the male CNS).
- Takemura S et al. (2013) Nature 500:175-181; (2015) PNAS 112:13711-13716; (2017) eLife 6:e24394 (medulla connectomes that flyvis combines in fib25-fib19_v2.2).
