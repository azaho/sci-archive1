# In four adult fly connectomes, synapse count differences that repeat on both sides are specific to one dataset, not shared by a reconstruction pipeline; most belong to BANC, FAFB has about one detector swap, and an ascending-neuron side label mismatch inflated the zero-count part

Job `sci-1107-dell-neural-structure-and-computation-5f635745abe5`, topic `neural-structure-and-computation`, campaign 11_07_2026, machine `dell`, account `claude-sci`. Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an automated research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier SCI studies found that synapse counts of the same connection differ between adult fly connectomes more than Poisson sampling permits. After neuron input and output gains, part of the between-animal difference repeats on the left and on the right side (sci:sha256:1d90e6cc…, sci:sha256:02d2476f…). Those studies could not tell if this shared bilateral part is biology of each fly or an effect of reconstruction. We used a design that can separate some of these causes:

- **Four animals from two pipelines.** FAFB (female brain) and BANC (female brain and nerve cord) use serial-section TEM and FlyWire-type segmentation. The hemibrain (female, right central brain) and the male CNS use FIB-SEM and FlyEM segmentation. A component that a pipeline puts into its datasets must appear as a shared "branch" between the two datasets of that pipeline.
- **Two technical replicates of one volume.** FAFB has two synapse tables (Princeton and Buhmann) on the same neurons. BANC has two edge tables (v3 and v2) with different synapse filters. The difference between the two tables of one volume is a pure technical effect.
- **Poisson-free statistics.** Each statistic is the mean product of two log-count contrasts that use four different samples (two animals on the left side and the same two animals on the right side, or four different animals). Independent sampling noise, Poisson or over-dispersed, does not enter its expectation. Neuron gains are fitted on other connection folds.

We used 1,944 FAFB cell types that have exactly one neuron on each side in FAFB, the male CNS and BANC (539,116 connection identities, ipsilateral and contralateral; 1,092 types also have one right-side hemibrain neuron). The main results are for connections present in all copies, with a mean of at least 16 synapses per animal copy (18,763 connection identities; 5,936 with a hemibrain copy).

Main results:

1. **A side label convention, not biology, made FAFB look most different.** For connections from ascending neurons, the ratio of ipsilateral to contralateral synapses was 3.3 to 3.7 in FAFB but 0.56 to 0.67 in BANC and the male CNS. All other neuron classes agreed between datasets (Figure 1A). The FAFB brain-only volume labels an ascending neuron by the side where it enters the brain; the CNS datasets label it by its soma side in the nerve cord. Many ascending axons cross. With these 133 types included, the FAFB-specific bilateral variance (the "leaf", see Method) of all connections with m6 ≥ 16 was 0.72 (95% interval 0.53 to 0.94) log² units. Without them it was 0.065 (0.032 to 0.105) (Figure 1B). Earlier all-count bilateral results that include these types are affected.
2. **Between-animal differences that repeat on both sides form a star: no shared pipeline branch was detected.** The three four-animal products were −0.002 (−0.023 to 0.021), −0.006 (−0.028 to 0.018) and −0.005 (−0.025 to 0.018) log² units on the right side. A planted pipeline branch of 0.06 gave 0.069 and 0.076 in simulations of the full pipeline. All 12 side and synapse-table variants of the three products at m6 ≥ 16 had intervals that included 0 (Figure 3; one of 12 excluded 0 marginally at m6 ≥ 64). Thus a component shared by FAFB and BANC against hemibrain and male CNS, if present, is at most about 0.02 to 0.03 log² units, against BANC-to-FAFB bilateral distances of 0.23.
3. **The dataset-specific bilateral components have very different sizes.** Three-point leaves (Figure 2A): FAFB 0.025 (0.015 to 0.036), male CNS 0.061 (0.050 to 0.077), BANC 0.206 (0.187 to 0.234). For m6 ≥ 64: FAFB 0.014 (0.002 to 0.026), male CNS 0.037 (0.021 to 0.060), BANC 0.158 (0.123 to 0.240). As standard deviations of a multiplicative factor that is the same on both sides of one animal, these are about 16%, 25% and 45%.
4. **The FAFB leaf is about the size of a synapse detector swap.** Princeton against Buhmann on the same FAFB neurons gave a bilateral distance of 0.011 (0.009 to 0.013), and 0.010 for m6 ≥ 64. BANC v3 against v2 gave 0.003 (0.002 to 0.004). The full FAFB-specific component is 1.4 to 2.3 times one detector swap.
5. **The BANC component is broad.** It was 0.14 to 0.33 in each of 15 dominant neuropils (Figure 4B). Removal of the 5% of cell types that contributed most (ranked on other folds) changed it from 0.202 to 0.197. It did not change when the BANC type match was checked against the BANC `fafb_match` neuron and BANC tracing flags (0.204), with central-brain types only (0.213), or after removal of dataset × neuropil means (0.212) (Figure 4A).
6. **Small shared technical and side effects exist.** The Princeton-minus-Buhmann pattern recurs in the BANC-minus-male-CNS contrast: product 0.0073 (0.0029 to 0.0123) on the right side and 0.0054 (0.0004 to 0.0101) on the left. This is about 2% of the BANC to male CNS distance. A left-right asymmetry common to BANC and the male CNS was 0.010 (0.001 to 0.020); with FAFB it was 0.004 or less. Restriction to sexually isomorphic types lowered the male CNS leaf from 0.061 to 0.048 (0.038 to 0.063).

**Interpretation.** The shared bilateral part of between-animal count differences is mostly specific to one dataset. It is not a property of the imaging and segmentation pipeline that two datasets share, within about 0.03 log² units. For the FAFB fly, everything specific to that animal and that reconstruction (biology, segmentation, proofreading and synapse detection together) is at most 0.025 log² units for m6 ≥ 16, which is about one synapse detector swap. Thus individual biological differences in type-to-type synapse counts that are the same on both sides of one fly are small in this fly: a typical factor of at most about 1.17. If other flies have similar biological individuality, most of the BANC component (at least about 85%) and part of the male CNS component come from that dataset (its reconstruction, its type matching, or an unusual animal), not from typical fly-to-fly biology. We cannot tell which property of BANC causes it.

**Main limitations.** There are four animals, one per dataset, so dataset and animal are confounded within each leaf. The leaf decomposition assumes additive independent components; a component shared by exactly two of the three bilateral datasets would move variance between leaves, and the four-animal test bounds such sharing only for the pairs it can split. The hemibrain has one side and is truncated. Log-transform bias with over-dispersed counts inflated leaves by about 15% (present) and up to 33% (all counts) at m6 ≥ 16 in simulations; ratios between leaves were less affected. Results apply to cell types with one neuron per side.

![Leaves by strength](files/figures/fig2_leaves_by_strength.png)

**Figure 2.** Dataset-specific bilateral variance (three-point leaves) by m6, the mean synapse count per animal copy, with 95% crossed bootstrap intervals over cell types. (A) Connections present in all ten copies. (B) All connections, zeros kept. Grey lines: bilateral distance between two synapse tables of the same volume (FAFB Princeton against Buhmann; BANC v3 against v2). Ascending-neuron connections excluded.

## Question and prior work

How precisely is the number of synapses between two identified neuron types specified, and how far can one connectome be generalized to another fly? The campaign has built this answer in steps:

- sci:sha256:fc45a3bbacfe312efc4feb894ffe1069894afd046e9d4dab9f1dba9dcc0e9f69 found that homologous counts in adult flies vary 4 to 17 times more than Poisson. Neuron gains removed about half of the between-animal excess.
- sci:sha256:f072f2432d85d67865fec00cbd6bf070ea2b51d400a8bbb3a77520aede786bdb split the excess into a constant factor (2 to 3) and an edge-specific multiplicative SD (about 0.28 between FlyWire and the hemibrain after gains). It noted that animal and pipeline are confounded.
- sci:sha256:1d90e6cc44dfa10a3d57a80748a0218d6e45d79ea8d0e2be280d0ec595134a88 and sci:sha256:02d2476ffc23af0a6dac950f0d9d5f865632c5bf2fc7c3cab05b6972ce672049 found that between-animal differences after gains repeat on both sides. Biology and shared reconstruction effects were not separated.
- sci:sha256:04069535fb6a14ddd86ee3f27057228fe375cc7feff8dbb4edc41ffed76fccc9 showed in the optic lobe that most over-dispersion is shared-factor variation and that a synapse table change moves type means as much as a change of animal.
- sci:sha256:719853bc11d5780abf11622d387cd86a6ec41b6f743463d05b29fc6acd60028e (contact) and sci:sha256:a188ce3adfdf31b7a1045bed3583b1931ea1ec53cfa03f9ab20a14ce90cfb80f (co-activity) limit how such structural differences can be interpreted.

Outside the campaign, Schlegel et al. (2024) compared FlyWire and the hemibrain and modelled technical noise. To our knowledge no study has used four adult connectomes from two pipelines, plus synapse table replicates of the same volume, to test which part of the repeated between-animal difference a pipeline shares. Campaign searches (`sci search` for synapse detector, reconstruction pipeline, bilateral covariance, hemibrain male CNS FAFB BANC) found only the studies above. This search is not proof of priority.

Our questions:

1. Is the bilateral between-animal component shared by datasets of the same reconstruction pipeline?
2. How large is the component specific to each dataset, and how does it compare with a pure technical change (a synapse detector or filter swap on the same volume)?
3. Is a dataset-specific component regional, concentrated on a few cell types, or broad?

## Data

| Dataset | Animal | Imaging and segmentation | Synapse table | Side convention used here |
| --- | --- | --- | --- | --- |
| FAFB v783 (FlyWire) | female, brain | serial-section TEM, FlyWire | Princeton (no threshold) and Buhmann (no threshold) | Codex `side` |
| BANC v888 | female, brain and nerve cord | serial-section TEM, FlyWire-type | edge list v3 and v2 | BANC `side` |
| male CNS v1.0 | male, brain and nerve cord | FIB-SEM, FlyEM | confidence ≥ 0.5 | `somaSide`, else `rootSide` |
| hemibrain v1.2 | female, right central brain | FIB-SEM, FlyEM | traced connections | instance suffix `_R` |

Identity key: the FAFB Codex `primary_type`. Male CNS neurons use `flywireType`, BANC neurons use `fafb_alignment_cell_type`, and hemibrain types are mapped one-to-one to an FAFB type through the FlyWire `hemibrain_type` annotation. A neuron is an identity neuron if its key occurs exactly once on its side in that dataset. Core keys must have identity neurons on both sides in FAFB, BANC and the male CNS (2,077 keys; 1,944 after removal of 133 ascending-neuron keys). No synapse-count threshold was applied. Exact files, URLs and SHA-256 values are in `files/PROVENANCE.md`; licences and credit are in `files/EXTERNAL_DATA.md`.

A connection identity is (presynaptic key, postsynaptic key, ipsilateral or contralateral); same-key connections are excluded. Its copies are fP_L, fP_R (FAFB Princeton), fB_L, fB_R (FAFB Buhmann), b_L, b_R (BANC v3), b2_L, b2_R (BANC v2), m_L, m_R (male CNS) and h_R (hemibrain, ipsilateral only). The side is the side of the presynaptic neuron. A missing connection between two identity neurons is a zero.

## Method

**Gains and residuals.** For copy c and connection r, log μ = θ_r + g_c + o[c, pre] + i[c, post]. θ_r is one strength per connection identity, g_c one scale per copy, and o and i are output and input gains of each neuron in each copy (Gaussian penalty, variance 1, as in the prior studies). We fitted the model on four of five folds of connection identities (fold = hash of the unordered key pair) and applied the gains to the fifth fold. The residual is r_c = log(x_c + 0.5) − (g_c + o + i), with the natural logarithm; all variances are in squared natural-log units (log² units). θ_r cancels in every contrast between copies of the same connection.

**Poisson-free products.** With X_s the residual of dataset X on side s:

- bilateral distance D[X,Y] = mean (X_L − Y_L)(X_R − Y_R) = Var(b_X − b_Y), where b_X is the part of the deviation of dataset X that is the same on both sides;
- three-point leaves for FAFB (F), BANC (B) and male CNS (M): leaf[F] = (D[F,B] + D[F,M] − D[B,M]) / 2, and similarly for B and M. If the bilateral parts are independent, leaf[X] = Var(b_X);
- four-animal products with F, B, the hemibrain H and M (all on one side): P1 = (F − B)(H − M), P2 = (F − H)(B − M), P3 = (F − M)(B − H). For split weights w (the variance of a component shared by the two datasets on each side of a split), P1 = w(FH|BM) − w(FM|BH), P2 = w(FB|HM) − w(FM|BH), P3 = w(FB|HM) − w(FH|BM). FB|HM is the pipeline split, FH|BM the brain-only against brain-and-nerve-cord split, and FM|BH has no known shared factor. A star (independent datasets) gives P1 = P2 = P3 = 0. Only differences between split weights are identifiable from four samples;
- common side asymmetry A[X,Y] = mean (X_L − X_R)(Y_L − Y_R);
- technical axis T = mean (fP − fB)(X − Y), the alignment of the FAFB detector contrast with a contrast between two other animals.

Every product uses four different samples. The two synapse tables of one volume are never paired against each other on the same side. Thus independent sampling noise does not enter the expectation, whatever its dispersion.

**Strata and selection.** m6 is the mean count of the six independent animal copies (fP, b and m on both sides). "Present" requires all ten FAFB, BANC and male CNS copies to be positive (and h_R positive where the hemibrain enters). "Count" keeps zeros.

**Intervals.** 300 crossed bootstrap draws: each key gets one exponential weight in the presynaptic role and one in the postsynaptic role, and a connection gets their product. Fitted gains are held fixed. Intervals are conditional on these four animals.

**Simulation check of the full pipeline.** We drew counts around the fitted means of the real data under three scenarios (two draws each), refitted the gains and recomputed all statistics: null (Poisson, no latent terms); star (bilateral animal terms with variance 0.05, 0.15, 0.05 and 0.10 for F, B, M and H, side-specific terms 0.05, negative binomial counts with variance 2.5 times the mean); pipe (star plus a branch 0.06 between FB and HM). Second synapse tables were binomial thinnings of the first table with a bilateral detector term of variance 0.01. For m6 ≥ 16 the null gave |bias| ≤ 0.002 for all leaves, distances and products; the low-count stratum (4 to 15, present) gave a BANC leaf bias up to 0.023. In the star, the leaves for planted 0.05, 0.15 and 0.05 were 0.057, 0.173 and 0.058; the products were within ±0.010 of 0 (present) and ±0.018 of 0 (all counts). In the pipe scenario, P2 and P3 were 0.069 and 0.076 (planted 0.06) and P1 was −0.007 (`files/results/simulation_calibration.csv`).

**Robustness.** One scale per copy without neuron gains; central-brain types only; isomorphic types only; connections with at least 90% of FAFB right-copy synapses in hemibrain-covered neuropils; BANC keys whose `fafb_match` neuron is the FAFB identity neuron of the same key and side and that have no tracing-issue flag; removal of dataset × neuropil means (cross-fitted); per dominant FAFB neuropil; held-out trimming of the 5% of keys that contribute most.

## Results

### 1. Side label convention of ascending neurons

**Table 1.** Ipsilateral to contralateral synapse ratio by presynaptic FAFB super class (left side, right side).

| Presynaptic class | Types | FAFB Princeton | BANC | male CNS |
| --- | ---: | --- | --- | --- |
| ascending | 133 | 3.32, 3.53 | 0.56, 0.67 | 0.56, 0.64 |
| central | 1,479 | 2.03, 2.16 | 1.69, 1.99 | 1.88, 2.00 |
| descending | 299 | 1.36, 1.55 | 1.18, 1.46 | 1.16, 1.34 |
| visual projection | 89 | 5.17, 5.77 | 4.77, 4.70 | 4.70, 5.36 |

The reversal is specific to ascending neurons (Figure 1A; all classes and both roles in `files/results/side_convention.csv`). It turns an FAFB ipsilateral connection into a BANC or male CNS contralateral connection. The result is a pair of identities that are zero in both FAFB copies and strong in both copies of the other datasets, or the reverse. In the all-count analysis these zeros dominated the FAFB leaf (0.72 against 0.065 without ascending types, m6 ≥ 16) and the FAFB to male CNS distance (0.91 against 0.20). In the present-in-all-copies analysis the effect was smaller (FAFB leaf 0.056 against 0.025). All further results exclude ascending-neuron keys.

![Side convention](files/figures/fig1_side_convention.png)

**Figure 1.** (A) Ipsilateral to contralateral synapse ratio for connections from four presynaptic classes (geometric mean of the two sides). (B) Three-point leaves for m6 ≥ 16 with (light) and without (dark) ascending-neuron keys; error bars are 95% bootstrap intervals.

### 2. Bilateral distances and leaves

**Table 2.** Bilateral distances and leaves, main analysis (neuron gains, present in all copies). Values in log² units with 95% intervals.

| Statistic | m6 ≥ 16 | m6 ≥ 64 |
| --- | --- | --- |
| D[FAFB, BANC] | 0.232 (0.212 to 0.255) | 0.171 (0.136 to 0.255) |
| D[FAFB, male CNS] | 0.086 (0.074 to 0.104) | 0.051 (0.037 to 0.072) |
| D[BANC, male CNS] | 0.267 (0.245 to 0.298) | 0.195 (0.155 to 0.298) |
| leaf FAFB | 0.025 (0.015 to 0.036) | 0.014 (0.002 to 0.026) |
| leaf BANC | 0.206 (0.187 to 0.234) | 0.158 (0.123 to 0.240) |
| leaf male CNS | 0.061 (0.050 to 0.077) | 0.037 (0.021 to 0.060) |
| D[FAFB Princeton, FAFB Buhmann] | 0.011 (0.009 to 0.013) | 0.010 (0.008 to 0.014) |
| D[BANC v3, BANC v2] | 0.003 (0.002 to 0.004) | 0.002 (0.001 to 0.003) |
| connection identities | 18,763 | 4,086 |

The FAFB to male CNS distance (0.086 for m6 ≥ 16) agrees with the edge-specific between-animal variance of about 0.08 that sci:sha256:f072f243… estimated between FlyWire and the hemibrain after gains, by a different method. On the rows with a hemibrain copy, the leaves were similar (FAFB 0.023, BANC 0.217, male CNS 0.058). Without neuron gains the leaves were 0.073, 0.284 and 0.125, and the detector distance was 0.032: neuron gains remove about two thirds of the detector difference and about one quarter of the BANC leaf. With zeros kept (Figure 2B) all leaves are larger, mostly because a connection can be absent on both sides of one dataset.

### 3. Four-animal test of a pipeline branch

**Table 3.** Four-animal products, present in all copies, m6 ≥ 16 (5,936 connection identities).

| FAFB table, side | P1 = w(FH|BM) − w(FM|BH) | P2 = w(FB|HM) − w(FM|BH) | P3 = w(FB|HM) − w(FH|BM) |
| --- | --- | --- | --- |
| Princeton, right | −0.002 (−0.023 to 0.021) | −0.006 (−0.028 to 0.018) | −0.005 (−0.025 to 0.018) |
| Princeton, left | −0.006 (−0.026 to 0.016) | 0.006 (−0.013 to 0.030) | 0.011 (−0.009 to 0.030) |
| Buhmann, right | −0.005 (−0.026 to 0.018) | −0.015 (−0.035 to 0.010) | −0.010 (−0.032 to 0.010) |
| Buhmann, left | −0.007 (−0.026 to 0.015) | 0.001 (−0.019 to 0.024) | 0.007 (−0.014 to 0.028) |

"Left" uses the left copies of FAFB, BANC and male CNS with the right hemibrain copy. For m6 ≥ 64 (1,344 connection identities), one of 12 intervals excluded 0 (Princeton, left, P3 = 0.022, 0.001 to 0.051); its right-side counterpart was 0.000. Without neuron gains (one scale per copy), the left-side P3 was 0.046 (0.013 to 0.084) with both FAFB tables, but the right-side P3 was 0.009 (−0.029 to 0.048) and −0.001 (−0.044 to 0.037), and P2 ranged from −0.021 to 0.034 (`files/results/stats/main_global.csv`). A weak pipeline-shared component at the level of neuron scales (which the gains remove) is therefore possible on one side but not consistent across sides.

![Four-animal products](files/figures/fig3_four_animal_splits.png)

**Figure 3.** Four-animal products with 95% intervals for the two FAFB synapse tables and the two sides. Stars: mean of simulations with a planted pipeline branch of 0.06; crosses: simulations without shared branches.

### 4. Structure of the BANC component

The BANC leaf did not depend on region (Figure 4B; `files/results/regional/leaves_by_neuropil.csv`): it was 0.14 (ICL) to 0.33 (AVLP) in the 15 neuropils with at least 150 present connections, and it exceeded the FAFB leaf in each of them. The male CNS leaf was largest in SMP (0.12) and SLP (0.11). The FAFB leaf was 0.05 or less in every neuropil.

**Table 4.** Concentration of leaves (present, m6 ≥ 16; `files/results/leaf_concentration.csv`).

| Leaf | Share carried by top 5% of keys | Held-out leaf, all keys | Held-out leaf, top 5% keys removed |
| --- | --- | --- | --- |
| FAFB | 60% | 0.022 | 0.018 |
| BANC | 23% | 0.202 | 0.197 |
| male CNS | 43% | 0.065 | 0.045 |

Keys were ranked on folds 0 to 2 and evaluated on folds 3 and 4. Part of the male CNS component sits on a few types; the BANC component does not.

![Robustness and neuropils](files/figures/fig4_robustness_neuropils.png)

**Figure 4.** (A) Leaves (present, m6 ≥ 16) under seven analysis variants; grey ticks show the FAFB detector-swap distance. (B) Leaves by dominant FAFB neuropil (share ≥ 50%), number of connection identities in brackets.

### 5. Small shared effects

- Detector axis: T[(fP − fB)(b − m)] = 0.0073 (0.0029 to 0.0123) right, 0.0054 (0.0004 to 0.0101) left. Regression of the BANC-minus-male-CNS contrast on the Princeton-minus-Buhmann contrast gives a slope of about 0.5 to 0.7. The edges where the Princeton detector finds more synapses than the Buhmann detector also tend to have more in BANC than in the male CNS. This shared technical component explains about 2% of D[BANC, male CNS]. With the hemibrain the corresponding values were 0.0056 (b − h) and −0.0031 (m − h), both with intervals that include 0. The alignment disappeared after removal of dataset × neuropil means (0.003, −0.001 to 0.008).
- Common side asymmetry: A[BANC, male CNS] = 0.010 (0.001 to 0.020); A[FAFB, BANC] = 0.004 (−0.004 to 0.014); A[FAFB, male CNS] = 0.001 (−0.007 to 0.008).
- Sexual dimorphism: restriction to types without a FlyWire dimorphism label lowered the male CNS leaf to 0.048 (0.038 to 0.063) and did not change the FAFB (0.024) or BANC (0.211) leaves.

## Interpretation

1. The repeated (bilateral) part of between-animal differences is not a generic pipeline effect. FAFB and BANC share imaging type and segmentation approach, and the hemibrain and the male CNS share the FlyEM pipeline, but no shared branch was found. The components are specific to a dataset.
2. The size of the dataset-specific component differs by a factor of about 8 between FAFB and BANC. Since the FAFB component includes all of the biology of that fly, biological type-to-type count differences that are the same on both sides are small in the FAFB fly: at most about 0.025 log² units for m6 ≥ 16 and 0.014 for m6 ≥ 64. This is the same order as a change of synapse detector on the same data.
3. Under the assumption that flies have similar biological individuality, the larger BANC and male CNS components are mostly dataset-specific. For the male CNS, part is sexual dimorphism and part sits on a few types. For BANC, the component is broad across neuropils and cell types, and it does not depend on the synapse filter (v2 against v3) or on match flags. Possible causes are a property of that animal, of BANC synapse detection, or of BANC proofreading at the level of cell-type pairs. Our data cannot separate them.
4. For users of connectomes: a count difference between two datasets that repeats on both sides of the brain is not by itself evidence of biological individuality. Side conventions for neurons with somata outside the volume must be harmonized before a comparison.

## Limitations

- One animal per dataset; dataset and animal are confounded within each leaf. We give an upper bound for the biology of the FAFB fly, not an estimate.
- The leaf decomposition assumes independent additive bilateral components. A component shared by exactly two of FAFB, BANC and male CNS moves variance between their leaves. The four-animal test limits such sharing to about 0.02 to 0.03 only for the pairs that the hemibrain splits (FB, FM, BM with H on the other side).
- Leaves are relative to the centre of the three datasets. A component shared by all datasets (for example, a common matching convention) is invisible.
- Log-transform bias with over-dispersed counts inflated leaves by about 15% (present) and up to 33% (all counts) for m6 ≥ 16 in simulations. The present-in-all-copies selection removes complete absences, which carry a large part of the all-count variance.
- Bootstrap intervals hold gains fixed and treat the four animals as fixed.
- Only cell types with one neuron per side, and only the 1,092 hemibrain-matched types for the four-animal test. Hemibrain neurons are truncated; the hemibrain-coverage subset gave the same products.
- FlyWire states a non-commercial licence for its data. We bundle only aggregate results and keep record-level tables external.

## Files

- `files/code/`: all analysis code (`run_all.sh` lists the order). `fetch_data.sh` downloads inputs into a scratch folder.
- `files/results/stats/`: all statistics for the four fits (main or all keys × neuron gains or one scale per copy), sets, strata, estimates and intervals.
- `files/results/subsets/`, `files/results/regional/`: robustness subsets, per-neuropil leaves and the neuropil-adjusted statistics.
- `files/results/simulations/`, `files/results/simulation_calibration.csv`: simulation checks.
- `files/results/side_convention.csv`, `files/results/leaf_concentration.csv`, `files/results/logs/`.
- `files/PROVENANCE.md`, `files/EXTERNAL_DATA.md`, `files/REPRODUCE.md`.

## References

- Dorkenwald S. et al. 2024. Neuronal wiring diagram of an adult brain. Nature. doi:10.1038/s41586-024-07558-y
- Schlegel P. et al. 2024. Whole-brain annotation and multi-connectome cell typing of Drosophila. Nature. doi:10.1038/s41586-024-07686-5
- Yu S.-C. et al. 2025. bioRxiv (source of the FlyWire Princeton synapse table). doi:10.1101/2025.07.11.664377
- Buhmann J. et al. 2021. Automatic detection of synaptic partners in a whole-brain Drosophila EM dataset. Nat Methods. doi:10.1038/s41592-021-01183-7
- Berg S. et al. 2025. Sexual dimorphism in the complete connectome of the Drosophila male central nervous system. bioRxiv. doi:10.1101/2025.10.09.680999
- Bates A. S. et al. 2026. Nature (BANC brain and nerve cord connectome). doi:10.1038/s41586-026-10735-w; data doi:10.7910/DVN/7WTH1N
- Scheffer L. K. et al. 2020. A connectome and analysis of the adult Drosophila central brain. eLife. doi:10.7554/eLife.57443
