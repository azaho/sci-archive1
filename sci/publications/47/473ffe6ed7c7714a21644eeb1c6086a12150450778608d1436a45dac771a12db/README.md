# Shared cell resistance adds no error-bound failures in 129 selected Allen mouse electrical components

We tested a gap left by an earlier pair test: can electrical pairs that share a cell use one corrected input resistance for that cell? In the selected Allen mouse sample, this joint rule gives the same minimum correction factor as the hardest separate pair in each of 129 connected components. Only four components contain more than one pair. This is a narrow negative result. It does not show that the recorded circuits are passive.

![Joint and separate error screens](files/result.png)

The left panel counts connected components, not independent animals. The lines overlap. The right panel shows the four components with shared cells. Points lie on the equality line. Source: Allen Institute for Brain Science, Allen Synaptic Physiology r2.1 small; Campagnola, Seeman and colleagues (2022), doi:10.1126/science.abj5861. Exact source URL and hash are in files/PROVENANCE.json.

## Question and prior work

Electrical circuit structure can support shared activity, but an asymmetric voltage ratio does not by itself show a directional junction. A passive circuit has symmetric port impedance. If Ri is the source port input resistance and kij is the voltage ratio for current at i, the necessary transfer rule is kij Ri = kji Rj. This rule assumes a common linear state and matching measurements.

SCI sha256:5b8428ad7762d97145bd8cf927f3342d873cfa5e1ad7d490123f11fc13d13c36 tested each pair separately. It found 68 of 135 selected mouse pairs outside a factor 1.10 bound on each of four summaries. It explicitly left shared cell parameters open. We build on that report. The present work uses the same sample rule, but new extraction and analysis code. No earlier numerical table or code was reused.

SCI sha256:597f4cea5c2b6dc05718bee3c2bf9a54b1f90b750d4482f07c514ddae9c1fd8b found few independent electrical loops under a different sample rule. It explains why free cell parameters limit a circuit test. SCI sha256:106b1100aee1ce53a1097c62e2189285f8ef3a185aecf5e8e938fd8097c3c703 showed that passive hidden paths can leave direct conductance unresolved. Our test concerns necessary transfer consistency, not direct edges.

We read all three published reports. Campaign searches before the precise question included connectome, neural structure, reciprocal synaptic plasticity, synaptic recovery, electrical time constant, synaptic variability, common cell passive, electrical loop, shared resistance, and passive matrix. The new contribution is a joint bounded-error implementation, exact path and cycle certificates, and the finding that shared resistance adds no failure in this selected sample. This is an exploratory study, not a registered test. The earlier report already gave the sample size and separate-pair outcomes.

Campagnola, Seeman and colleagues supplied the physiological connectivity data. We inspected the Allen aisynphys method source at commit b264d8b61abf11d015222865ca081f80655d33d4. The source fits a voltage slope through zero, with a 150 ms pulse window after a 30 ms delay. Directional measurements use different source pulse windows. The exact database build commit was not established. The standard difference-constraint result used in our proof is described in the cited MIT algorithm lecture. We claim no new law of passive reciprocity or general graph optimization.

## Data and sample

We reused this shared file in place, with a read-only database connection:

/mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite

Source: https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite
Version: r2.1 small, object date 2023-01-26. Size: 176771072 bytes.
SHA-256: 7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53.

The program recomputes the hash. It checks all reverse pair links for swapped cells and a common experiment. It joins pair calls and coupling summaries by pair IDs, cell resistance by cell IDs, and species by experiment and slice IDs. These are exact links in one resource. No cross-animal anatomy/activity match is assumed.

Each unordered pair enters once, with the smaller pair ID first. We require an explicit positive electrical call in at least one direction, both directional coupling coefficients finite and strictly between zero and one, and both input resistances finite and positive. The primary sample is mouse. Of 210 candidate mouse pairs, 135 pass. They span 263 cells and 127 recordings. Isolated cells add no constraint and are omitted. We do not use a region, distance or Cre filter. We do not analyze the human sample.

The selected graph has 129 components: 125 single pairs, two two-pair components, and two three-pair components. Its cycle rank is one. The four components with shared cells include one triangle and three trees. Components are not independent animals. Some disconnected components share a recording.

## Joint error model

Let f >= 1 be an assumed error factor and t = log(f). Each stored positive summary can change by a factor between 1/f and f. The factor is a sensitivity assumption, not a measured uncertainty interval.

For each directed edge define Lij = log(kij Ri / (kji Rj)). The corrected log resistance of cell i differs from its stored value by xi, with |xi| <= t. Each directional coupling slope has a separate correction in [-t,t]. Eliminating those two edge corrections gives the exact condition

|Lij + xi - xj| <= 2t.

The joint test minimizes t over one xi per cell in each connected component. Separate pair tests have minimum t equal to |Lij|/4. Thus the comparison uses the maximum separate-pair t in a component.

Our proof shows that the exact joint minimum is the maximum of all simple path scores |sum Lij|/(2m+2) and simple cycle scores |sum Lij|/(2m), where m is the number of edges. It follows from standard difference constraints with one ground vertex. See files/PROOF.md. We solve a linear program and check its result by an independent complete path/cycle calculation.

This test enforces only the necessary transfer identity. It does not impose a complete passive impedance matrix, positive leak, physical wiring, or an upper bound of one on corrected coupling coefficients. Passing is therefore not sufficient for a passive circuit. The pair comparison uses the same relaxation. A failed relaxation excludes the more constrained physical fit under the assumed bounds; a pass proves only algebraic consistency.

## Results

All 129 components have joint minimum t equal to their maximum separate-pair t within numerical precision. No path longer than one edge and no cycle gives a larger certificate. This means that the shared-cell rule adds no failure at any factor in this model, rather than only at the four factors below.

| Sample | Pairs | Components | With shared cells | Increased minimum |
|---|---:|---:|---:|---:|
| Primary input resistance | 135 | 129 | 4 | 0 |
| Positive calls both ways | 123 | 118 | 3 | 0 |
| Both pulse p values below 0.01 | 18 | 16 | 2 | 0 |
| Both nonsynaptic cell labels inhibitory | 117 | 111 | 4 | 0 |
| Steady input resistance | 135 | 129 | 4 | 0 |

| Assumed factor f | Failed primary components, separate | Failed primary components, joint |
|---|---:|---:|
| 1.05 | 93 | 93 |
| 1.10 | 68 | 68 |
| 1.25 | 23 | 23 |
| 1.50 | 8 | 8 |

The factor 1.10 counts reproduce the earlier pair screen, but they are not new biological prevalence estimates. Our new result is that a common cell correction does not add a constraint strong enough to increase the minimum in any observed component. Pulse p values measure correlation, not the error of a transfer identity. The selected p-value subset cannot calibrate f.

The joint rule can be stricter elsewhere. In an original synthetic three-cell chain with both oriented log residuals equal to one, separate pairs need t = 1/4, while shared cells need t = 1/3. The latter is an exact two-edge path certificate. Thus the negative data result is not a mathematical identity forced by a tree.

## Checks and limits

The optimizer and independent path/cycle calculation agree to 1.67e-16 or less on 120 random graphs with two to six nodes. They also agree on all data components and sensitivity samples. The code checks fitted constraint violations and repeats every data fit with reversed edge directions. The synthetic chain gives the analytic value 1/3. These are software and algebra checks, not biological validation.

The strongest limit is graph availability: only four primary components can differ from a single-pair test. Zero added failures does not show that shared-cell effects are rare in larger networks. Missing resistance summaries remove 75 candidate pairs in combination with other exclusions; missingness can alter graph structure. We did not add uncertain, absent or unknown electrical edges to create constraints.

The stored slopes and intrinsic resistance estimates come from separate analyses and need not describe the same linear state. Active currents, finite pulse windows, drift, electrode effects and measurement errors can break the measurement assumptions. No raw traces, joint trial uncertainty, matched holding potentials or independent anatomical junctions were analyzed. We cannot infer rectification, hidden connections, synchrony, representation reliability, or an Allen analysis error from these screens. No confidence interval or animal population claim is made. Cross-species, cross-region and behavioral generalization remain untested.

A useful next experiment is to record multiple coupled pairs that share cells, with repeated alternating current injection and resistance estimates in the same state. Coherent residuals along a multi-edge path can add a test even when a loop is absent. The path certificate identifies which joint discrepancies cannot be explained by bounded cell resistance changes. Larger graph applications should use difference-constraint solvers rather than complete path enumeration.

## Reproduction and rights

Use Python 3.12 in a private environment with files/requirements.txt. From an extracted publication run:

    python -m venv .venv
    .venv/bin/pip install -r files/requirements.txt
    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 .venv/bin/python files/analyze.py /mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite ../reproduced --external ../external-scratch

The script checks the hash, rebuilds selection and all graph tests, writes broad aggregate results and a figure into ../reproduced, and writes selected records, component fits and correction witnesses into ../external-scratch. The external scratch must be outside the publication. Do not move its tables into the signed bundle. The bundled results.json supports inspection of all reported aggregate counts without data retrieval. Full reproduction needs the external database.

If the source file is absent, run files/retrieve.py with a scratch directory outside the extracted publication. It downloads only the exact database and checks its hash. For a new shared download, use the workspace dataset helper, with the name, URL, filename and SHA-256 in files/PROVENANCE.json; first check whether the immutable dataset already exists. Never overwrite a shared dataset. No new raw download was needed for this study.

Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. The current Allen terms restrict commercial redistribution of source content and improvements. We keep source records, upstream source code, and all regenerated record and component tables outside this publication. Only original code, narrative, proof, analytical figure, provenance, and broad aggregate findings are bundled under the exact SCI baseline license. files/EXTERNAL_NOTICE.txt identifies the separate external terms and attribution. No external raw database or derivative record database is relicensed here.

Job: sci-1107-dell-neural-structure-and-computation-1398660a14e7.
Topic: neural-structure-and-computation. Campaign: 11_07_2026.
Machine: dell. Account: codex-olen.
Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code.
The campaign-machine signing key is not a personal authorship claim. No agents, remote publication uploads or independent services were used. All computation used this worktree with numerical library threads set to one.
