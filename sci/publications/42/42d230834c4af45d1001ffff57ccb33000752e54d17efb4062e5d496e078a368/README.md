# At least eight delay exclusions are needed for a 0.1 ms additive fit in selected Allen mouse slice groups

Eight is the smallest number of measured delays that must be set aside to permit a source-cell plus target-cell timing model within 0.1 ms in the selected mouse data. There are 6,144 smallest solutions. Only one record occurs in every solution. With stricter cell labels, four exclusions suffice and no record occurs in every smallest solution. These are exact results for stored values under an assumed error bound. They do not identify bad measurements or establish a biological timing rule.

![Exact exclusion counts and remaining tests](files/evidence.png)

## Question and prior work

Can a few connection-specific delay estimates account for failure of an additive cell timing model, or do many independent records need review? A model with one source term and one target term could reduce timing parameters in circuit simulations. It is useful to know how much its failure depends on individual measurements.

Campagnola, Seeman and colleagues measured connectivity and synaptic responses in mouse and human cortical slices (Science 2022, doi:10.1126/science.abj5861). Source action potential shape can affect synaptic delay (Boudkkazi and colleagues, 2011, doi:10.1113/jphysiol.2010.199653). This motivates a source term but does not prove additivity. Allen defines stored latency from the maximum source-spike slope to synaptic response onset in its pinned source schema. Allen methods describe manual onset selection and curve fitting. The fit search window of 0.1 ms around a manually chosen onset is not a validated error bound on the stored delay.

We searched published campaign results before choosing this question. Publication 5027b4e3394fd61ba71a15ba5d9fbdcb6b865bcab501c53428b7f1ab410f94a4 found that the selected mouse values need corrections up to 0.314238 ms for exact additivity. Publication 5d189525f3e310ecc4462c62cb8b6e43bbbea224bb37696d0255d571d2c3525d studied missing-delay recovery and sparse cycle support. Their reports are archived here with attribution. We use their grouping and cycle criterion, but extract data and implement the analysis independently. Our contribution is the exact minimum exclusion profile, all smallest review sets, forced-record tests, and the exact uniform-selection reference. This is a method application, not a new graph theorem or a new data collection.

## Data and scope

The source is Allen Synaptic Physiology r2.1 small, schema 22, dated 2023-01-26. Shared file: `/mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite`. SHA-256: `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. The extraction checked this hash and opened the file read-only. The source URL, SQL and library versions are in files/provenance.json. No shared data were changed and no new raw data were downloaded.

We join pair, synapse, cell, experiment and slice tables by their keys. We retain confirmed chemical connections between distinct cells with finite positive delays in mouse VisP and human TCx. This gives 2,248 mouse and 309 human measurements. Structural edges and function measurements have the same cell identities. These are small measured connection graphs in slices, not complete anatomical connectomes. We use no pulse-train arrays. The SQL inner join does not include confirmed calls with no synapse row; the positive-delay sample matches the prior bound study.

Primary groups fix experiment, synapse sign, source nonsynaptic class and target nonsynaptic class. Missing labels make explicit groups. Strict groups also fix ordered source and target Cre and target-layer labels. An interior check uses primary groups and only delays strictly between 0.2 and 5 ms. The error levels 0, 0.025, 0.05, 0.1 and 0.2 ms were fixed before the computation. They are sensitivity choices, not measured uncertainties.

## Model and exact method

The model in each group is `y_ij = a_i + b_j + e_ij`, with `|e_ij| <= epsilon`. Cell offsets are unrestricted real numbers. Source and target roles are separate vertices, even for the same physical cell. The terms are statistical offsets, not separately positive biological delays.

In a simple cycle of the bipartite graph, source and target terms cancel in the alternating delay sum S. The model is compatible with the error bound if and only if every cycle with L edges has `|S|/L <= epsilon`. This is the difference-constraint result proved in the prior bound report. A forest is always compatible and supplies no test of additivity.

After exclusion, all remaining cycles were present before exclusion. Thus each cycle that violates the bound must lose at least one measurement, and this condition is sufficient. We enumerate all smallest sets that intersect every violating cycle. Independent groups have disjoint measurements, so their minimum counts add. A forced record occurs in the intersection of all smallest sets in its group. See files/METHOD.md for the method, proof of the selection reduction, and exact uniform-selection calculation.

An exclusion means that a delay measurement is not used. It does not assert that the chemical connection is absent. We do not modify the database. The saved plans are sensitivity and review candidates, not instructions to remove observations from a biological claim.

## Results

| Assumed error bound, ms | Mouse primary: minimum exclusions | Incompatible primary groups | Constraints left in one primary plan | Mouse strict: minimum exclusions | Constraints left in one strict plan |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 18 | 10 | 0 | 11 | 0 |
| 0.025 | 13 | 9 | 5 | 8 | 3 |
| 0.05 | 11 | 7 | 7 | 6 | 5 |
| 0.1 | 8 | 6 | 10 | 4 | 7 |
| 0.2 | 3 | 3 | 15 | 1 | 10 |

The primary mouse graph has 18 independent algebraic constraints in ten groups. Only 57 of its 2,248 measurements lie on cycles, as found in prior work. The strict graph has 11 constraints in eight groups. Small exclusion counts relative to all measurements must be read against this sparse support.

At 0.1 ms, four primary groups need one exclusion each. Two denser groups, in experiments 2935 and 3172, need two exclusions each. Thus one exclusion per incompatible group is insufficient. The eight exclusions are 0.36% of all selected mouse measurements and 14.0% of the 57 cycle measurements. The first saved plan leaves ten algebraic constraints. Exact additivity at zero error instead requires 18 exclusions and leaves no cycle constraint. A fit after those 18 exclusions supplies no remaining cycle evidence for the model.

At 0.1 ms, experiment 3172 has exactly two smallest local choices: pair IDs {99745, 99766} or {99766, 99774}. Pair 99766 is the only globally forced record under this minimum-count rule. The other groups give multiple interchangeable choices. Strict matching has no forced record at this bound. Forced status does not show error in pair 99766; it depends on the model, fixed labels, error bound and minimum-count objective. Allowing more exclusions can avoid it.

A uniform random subset of eight measurements from the 2,248 mouse measurements restores 0.1 ms compatibility with exact probability `6144 / 15974767427829100891209`, or about 3.85e-19. The 6,144 successful subsets are precisely the smallest solutions. This small probability reflects sparse cycle support and the need to cover six particular groups. It is not a p-value, evidence against random wiring, or a model of laboratory error. It is a fixed-table selection reference.

The interior check removes 20 mouse and one human delay. It leaves all exclusion minima and all relevant cycle constraints unchanged. In the human sample, one exclusion suffices at 0, 0.025 and 0.05 ms, with four interchangeable choices. No exclusion is needed at 0.1 or 0.2 ms. There is only one human cycle group, so this is not evidence of a species difference. Species and region are also confounded.

## Checks and limits

Cycle thresholds agree with independent minimax linear programs for every constrained group. Every selected witness passes the linear-program error bound. An exhaustive test of all 63 nonempty 2-by-3 bipartite graphs at three error bounds compares the cycle selection result with direct subset search using linear-program feasibility. All 189 comparisons pass. The observed counts and largest thresholds also match the prior report. Code, edges, cycles, all minimum sets, exact probability integers and check results are included.

The error bounds are assumptions. Delay errors can be correlated or systematic. Selection, uncertain connection calls, missing delays, labels, slice damage, source waveform and unmeasured axon or synapse geometry can change the result. The counts describe this fixed table; no sampling interval or population prevalence is estimated. Cycles can share cells and recordings and are not independent animal replicates. Exclusion improves compatibility in part by removing tests. We do not test whether the additive model predicts new recordings, represents an intact circuit, or supports reliable behavior. The useful result is a reproducible way to locate the measurements on which a circuit timing test depends, with its remaining test count made explicit.

## Reproduction and credit

Run `python files/analyze.py` in an environment with files/requirements.txt to reproduce from archived derived evidence. Use `--database PATH` to repeat the source extraction with a hash check. See files/REPRODUCE.md. The raw database is not redistributed. Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. The baseline license covers new material to the extent allowed by the source terms; it does not replace the Allen Institute terms for source data.

Job: sci-1107-syam2-neural-structure-and-computation-1a6734477be6. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. No agents were launched. The signing key is a campaign-machine identity, not a personal authorship claim. No remote SCI archive or index was used.
