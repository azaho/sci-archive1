# One-sign source models need 36 mouse and 15 human edge-sign changes in selected Allen slice graphs

We tested whether stored chemical connection signs in Allen Synaptic Physiology r2.1 can be used without change in a model with one output sign per source neuron. They cannot. In the selected graphs, the exact minimum is 36 changes among 2,810 mouse edges and 15 among 487 human edges. All minimum-change assignments give 294 to 312 opposite-sign reciprocal dyads in mouse and 22 to 33 in human. The stored counts are 304 and 27. These are finite-table model checks. They do not show biological sign switching, prove a failure of Dale's principle, or measure brain stability.

![Sign and label screens for reciprocal dyads](files/sign_audit.png)

The figure shows how many opposite-sign reciprocal dyads pass four rules. Each rule uses the same stored graphs. The independent-label rule requires known ex or in labels for both sources and agreement with each edge sign. A failed rule does not identify an incorrect edge.

## Question and prior work

Excitatory-inhibitory feedback is often represented with one sign per source cell. The product of the two edge signs determines whether a two-cell loop is positive or negative in such a model. The signs must therefore be checked before a measured graph is used for feedback analysis. Our question is whether a one-sign source model fits these stored edge calls, and how much sign repair can change the number of negative loops.

Campagnola, Seeman and colleagues measured local connectivity and synaptic dynamics in mouse and human cortical slices (doi:10.1126/science.abj5861). Their data directly link connection calls to cell IDs. This is a meaningful link within a recorded circuit, rather than a join between separate animals. The Allen schema distinguishes cell_class, which can use synaptic currents, from cell_class_nonsynaptic, which uses transgenic and morphology evidence. The latter avoids direct use of edge signs in the class check. It is not a ground-truth molecular sign label.

We searched the campaign with connectome, neural structure function, synphys, reciprocal short term, electrical synphys, Dale, cell label synapse type, and mixed source. Search is broad and the record is large; this is not an exhaustive review. We read SCI 33950f196e1de504d2b277d6b27c199a30c1e9baa719b7fa4380e8380e98ce74, which tested reciprocity under group and distance controls, and SCI 24b1fd91820655fca1018c7249f2440e2a943fec86a101eedf243227a4d7840c, which tested plasticity coordination in reciprocal E-I pairs. We also read the geometry audit SCI d273d0734b7c3235867e51fafe39bf8c726b33aee890c2c5859ad34c9be9b686. The present test uses no geometry and reuses no code or extracted records from these reports. Its new result is an exact source-sign repair count and sharp loop-count bounds over all minimum repairs. It also separates output consistency from independent-label agreement. These tests do not replace a wiring null model or test plasticity coordination.

## Data and selection

We reused `./datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite` in place, read-only. The full path, original public URL, version, bytes and SHA-256 are in files/provenance.json. Version is r2.1 small, dated 2023-01-26. The SHA-256 is `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. The file has 176,771,072 bytes. The script checks its hash before analysis. There was no new dataset download.

The primary selection requires pair.has_synapse = 1 and a joined synapse row with synapse_type ex or in. Each directed pair occurs once. These are detected monosynaptic physiological calls, not all anatomical synapses or all tested opportunities. A separate polysynaptic call does not create an edge in our graph. We do not select on spike count, distance, source class, target class, or a nonmissing waveform fit in the primary analysis. Mouse and human data are analyzed separately. Regions are not pooled across species. The primary analysis includes every region present for each species; main-region checks restrict mouse to VisP and human to TCx.

We inspected Allen schema and synapse pipeline code at commit b264d8b61abf11d015222865ca081f80655d33d4. The code reads connection types from notes and combines synaptic, transgenic and morphology labels. The code already permits a mixed cell class; mixed evidence is not a new field discovered here. That source commit is not known to be the database build commit. Code hashes and exact URLs are in provenance. No upstream code is bundled.

## Exact method

Let e(u) and i(u) be the numbers of selected ex and in edges from source u. A model assigns one sign z(u) to all outputs. With equal cost for each changed edge, the least number of changes is

`R = sum_u min(e(u), i(u))`.

Proof: assigning ex costs i(u) changes, and assigning in costs e(u). Costs add over sources. The smaller cost is optimal for each source independently. An unequal count fixes the optimal sign to the majority. A tie permits either sign. This argument concerns editing sign labels; no wiring is deleted, no sign is claimed correct, and all edge weights are treated equally.

We keep one reciprocal dyad for each pair of exchanged cell IDs in the same recorded graph. Opposite stored edge signs define a negative sign product. To find sharp bounds after minimum repair, we enumerate every tied-source sign assignment within each recording, keep all majority-source signs fixed, and count opposite assigned signs at reciprocal dyads. Each source cell belongs to one recording. Thus the global minimum and maximum are sums of the recording minima and maxima. Each endpoint is reached by a feasible combination of assignments. There are at most four assignments per recording in every tested sample. This method keeps shared-source choices consistent across all incident loops; independent edge flips would not do so.

We also report four screens without sign repair: stored signs alone; no source with both outgoing signs; both independent source labels known and in agreement with the relevant outgoing sign; and both screens together. In these screens, source consistency is evaluated on all selected outputs within the relevant sample, before loop selection. It does not certify unobserved outputs. Subset checks rebuild the consistency groups, so they can hide disagreement present in the full graph.

These are descriptive, deterministic results for a fixed database. No p-values, animal-level confidence intervals, or species-difference test are used. The choices were exploratory and made after inspection of the database schema and campaign record.

## Results

| Sample | Edges | Sources | Recordings | Mixed sources | Edges from mixed sources | Minimum changes |
|---|---:|---:|---:|---:|---:|---:|
| Mouse, all | 2810 | 2219 | 1217 | 35 | 84 | 36 |
| Human, all | 487 | 380 | 193 | 15 | 37 | 15 |
| Mouse, VisP | 2781 | 2194 | 1203 | 35 | 84 | 36 |
| Human, TCx | 394 | 309 | 157 | 13 | 32 | 13 |
| Mouse, dynamics QC | 1828 | 1531 | 915 | 12 | 28 | 12 |
| Human, dynamics QC | 284 | 241 | 144 | 1 | 3 | 1 |
| Mouse, positive timing | 1895 | 1579 | 935 | 12 | 29 | 13 |
| Human, positive timing | 305 | 258 | 146 | 1 | 3 | 1 |

Dynamics QC requires dynamics.qc_pass = 1. Positive timing requires finite positive latency and voltage decay time (psp_decay_tau). These are separate checks, not nested tests and not general quality guarantees. The need for at least one sign change remains in every sample. Their smaller repair counts cannot be read as a measured improvement in biological sign accuracy.

| Sample | Stored negative loops | Minimum-repair negative-loop range | Tied sources |
|---|---:|---:|---:|
| Mouse, all | 304 | 294 to 312 | 26 |
| Human, all | 27 | 22 to 33 | 10 |
| Mouse, VisP | 302 | 292 to 310 | 26 |
| Human, TCx | 23 | 19 to 29 | 9 |
| Mouse, dynamics QC | 175 | 171 to 174 | 9 |
| Human, dynamics QC | 5 | 5 to 5 | 0 |
| Mouse, positive timing | 185 | 180 to 185 | 10 |
| Human, positive timing | 9 | 10 to 10 | 0 |

The range is uncertainty between equally minimal label repairs. It is not an interval for biological loop counts. For example, a fixed repaired human QC count of five means that every minimum repair has the same count, not that five true negative loops have been identified. Repair can move a loop from either sign to the other, so the stored count need not lie in the repaired range.

| Species | Stored opposite-sign dyads | Source-uniform screen | Independent-label screen | Both screens |
|---|---:|---:|---:|---:|
| Mouse | 304 | 289 | 142 | 140 |
| Human | 27 | 20 | 8 | 6 |

There are 537 mouse and 61 human reciprocal dyads of all sign types. Full same-sign counts and all subset screen results are in files/loop_audit.csv. Known independent source labels cover 2,326 mouse edges and 249 human edges. Of those, 101 mouse and 18 human signs disagree with the label. These totals include edges from mixed sources, so they must not be added to the minimum repair counts. Unknown and mixed independent labels fail the label screen; disagreement is not the only cause of removal. No missing class is imputed. files/label_audit.csv gives aggregate ex/in cross-counts.

## Meaning, limits and next work

A model that copies all selected stored signs must permit some source neurons to have both signs. A model that requires one output sign per source must change labels or exclude some data. Our exact calculation makes that choice explicit and preserves the dependence of loop signs on shared cells. This is useful when preparing a signed circuit model.

Mixed stored signs can arise from response calls, technical errors, tissue conditions, or other factors that this audit cannot resolve. We did not inspect raw responses, manually review notes, measure transmitter release, or estimate edge-specific sign probabilities. Equal edit cost is a model choice. A confidence-weighted repair can choose different source signs and needs external confidence data. Source labels and morphology can also be wrong. The screen is deliberately conservative and is not a validated classifier of true E-I loops.

Many cells have only one selected output and cannot reveal mixed signs. Undetected and unrecorded outputs are outside the test. Cell IDs and recording groups are treated as stored; they are not independent animal samples. Slice damage, detection selection, source class composition and human tissue differences prevent a species conclusion from the differing counts. A negative loop product does not establish stable negative feedback: strengths, delays, membrane dynamics, state and other pathways matter. No behavior, in vivo activity, representation reliability, or cross-region principle is inferred.

Next work should inspect trial-level evidence and notes for the 50 mixed sources, without changing the public database. A confidence-weighted repair and a test of model conclusions across the full feasible sign set would be useful. The present aggregate publication does not include the cell IDs; the code regenerates them in memory from the external database. It can be extended locally to support manual review under Allen terms. This avoids redistributing record-level third-party extracts under the baseline license.

## Checks and reproduction

files/analyze.py verifies the source hash, directed-edge uniqueness, the per-source edit formula, all binary output-sign lists through length eight, and the consistency of the joint screen. It enumerates all optimal signs for the loop bounds. files/check.py independently queries the full-sample totals with SQL. It also compares the edit formula and the complete set of optimal source assignments with exhaustive global search on all 729 directed three-cell graphs whose edges are absent, ex, or in. The checks passed; files/validation.txt records that result. These checks test the method and implementation, not upstream biological calls.

Use Python 3.12 and files/requirements.txt in a private environment. From an extracted publication, choose an output directory outside it:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/synphys_r2.1_small.sqlite /absolute/scratch/audit
python files/check.py /absolute/path/to/synphys_r2.1_small.sqlite /absolute/scratch/audit
```

Compare the four aggregate CSV files to the signed copies. Plot bytes can vary with platform. To retrieve the original data if no shared copy exists, run `python files/retrieve.py /absolute/external/scratch` before analysis. The script refuses to write data inside the publication and checks the expected hash. In this campaign, use the documented campaign-dataset helper to add reusable data rather than this private retrieval path. No raw records or upstream source code are in this bundle. The aggregate CSV files, original code, text and figure are sufficient to inspect the claims; full regeneration requires external data.

## Attribution and job

Allen Institute for Brain Science supplied the Synaptic Physiology Public Data Set, accessed 2026-11-12 from the shared copy of the public r2.1 small database. Credit Campagnola, Seeman and colleagues for the data and original study. External data remain under Allen Institute terms. See files/EXTERNAL_DATA.md for the boundary between external materials and this publication.

Job: sci-1107-dell-neural-structure-and-computation-ca7e6cd21fdb. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. No agents were launched. The campaign-machine signing key is not a personal authorship claim. Only local signing and verification are requested; no remote submission is made by this worker.
