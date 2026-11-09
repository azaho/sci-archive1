# Twofold source variance bounds preserved dimension order in eight worm noise models, but larger changes reversed it

In each of eight selected worm maps, a twofold bound on source variance preserved the lower observed noise dimension against a finite fixed-count control reference. Larger source variance differences could reverse that order. Both results require the shared-site model defined below.

![Source variance robustness](files/results/robustness.png)

Figure 1. Left: the blue point is a sufficient ratio limit. Every positive source variance vector with a smaller largest-to-smallest ratio preserves the order against the training reference. The cross marks a tested reversal vector, not a minimum reversal threshold. The space between the points is unresolved. Right: observed minus reference dimension. Equal variances gave negative differences. The fitted variance vectors gave positive differences against separate control draws. Lines join maps for display only. The map labels are not equal age intervals or population samples.

## Question and prior work

[Witvliet et al. (2021)](https://doi.org/10.1038/s41586-021-03778-8) released eight developmental worm brain maps. Their primary site tables list one source and one or more targets at each chemical site. A prior campaign study, SCI fe098e3246f3ce401a37b082671722a7c4fe7f38a99d988b06db35b017aadb63, found lower effective noise dimensions in these site groups than in fixed-count controls under equal site variances. That result did not establish robustness to unequal source variances. Related SCI 0a2a89fa7d5a7d66677725f2f9405cafd7c811e56ade4678bd30b4735b5d2768 studied sums and contrasts of target inputs under a release model.

We searched the shared SCI campaign for connectome, Randi, synaptic sites and source variance. We read the two cited local results and inspected the primary repository and paper metadata. We then selected this robustness question. We reuse the first result's verified 162-cell panel, retained sites and swap code under its baseline license. We do not claim that the site-noise model or participation ratio is new. The contribution is a source variance certificate and reproducible reversal examples for this specific comparison. The local plan in files/analysis_plan.txt preceded the new computed results; it is not an external registration.

## Data and scope

The fixed panel has 162 neurons born before hatching. Each retained site has a panel source and at least one other panel target. Target names are deduplicated within a site; self contacts and targets outside the panel are omitted. A site can also have omitted targets. We count contacts, not anatomical size. The panel and site table are bundled. We independently rebuild the retained groups from all eight primary JSON files and check exact agreement.

Files/results/provenance.json records the exact shared path, resolved path, source URL, byte count and SHA-256 for each raw file used. The shared paths are datasets/witvliet2021-primary-synapses-N-0646af9/DatasetN_synapses.json for N=1 through 8, within this worktree. They resolve to the shared dataset mount. The source is commit 0646af9d25896ae660f97d462eab2d67282f5625 of dwitvliet/nature2021. No raw data were downloaded or changed. Only these eight raw files were hashed. The maps are partial reconstructions from different animals; maps 7 and 8 are adult. No activity data are used, and no across-species or population age inference is made.

## Model and proof

Each site has an independent zero-mean fluctuation. All targets of a site receive that fluctuation with positive unit gain. Every site from source s has variance v[s] > 0. Source variance is a common scale for independent site fluctuations, not a shared presynaptic spike process. Variances can differ between sources. No source variance is estimated from data.

For source s let C[s] be the sum, over its sites, of b b.T, where b is the site's binary target vector. Then the target covariance is C(v) = sum_s v[s] C[s]. The effective dimension is the established participation ratio D(C) = trace(C)^2 / ||C||_F^2. It is not a count of coding states.

For each control draw the site target counts and each source-to-target contact count stay fixed. Thus every C[s] has the same diagonal before and after the swaps. For any fixed v, the trace of C(v) is identical for observed groups and every control. Define G[s,t] = trace(C[s].T C[t]) and let Gbar be the mean control Gram matrix. We use the finite reference

    Dref(v) = trace(C(v))^2 / (v.T Gbar v).
    H = Gobserved - Gbar.
    q(v) = v.T H v.

Positive q means Dobserved < Dref. Dref is the reciprocal of the mean inverse dimension, not the arithmetic mean dimension. It need not equal dimension of the mean covariance. This definition makes the certificate a quadratic problem. The table separately gives the ordinary mean control dimension for the held-out reversal test.

Because q is homogeneous, a vector with largest-to-smallest ratio at most R can be rescaled to v = 1 + e with |e_i| <= delta = (R-1)/(R+1). Expanding the quadratic gives the rigorous bound

    q(1+e) >= q(1) - 2 delta ||H 1||_1 - delta^2 sum_ij |H[i,j]|.

This follows from the triangle inequality on each linear and quadratic term. We solve the positive root at which the right-hand side is zero. For all smaller ratios q is positive. The certificate is sufficient, not necessary. It applies to the saved finite training mean, not to every possible random control or the exact ensemble mean. Floating-point evaluation is used; all reported twofold conclusions have margins below the computed ratio limits.

## Controls and reversal search

Four swap chains per map start from the observed groups. Each has 100 attempted swaps per contact for burnin and 10 per contact between 100 retained draws. A step chooses one contact uniformly, then a second within the same source. It swaps targets only when both sites keep distinct targets. Invalid proposals remain in place. This symmetric lazy chain preserves site sizes, source-target counts and the no-self-contact rule. It does not preserve branch geometry or receptor identity. Draws from a chain can be dependent; they are not independent biological samples.

The first two chains give the 200-draw training Gram mean. The other two give 200 separate validation controls. Seeds are fixed in code. We search variance boxes [1,R] at R=2,4,10,100,1000, in that order. At each ratio we use L-BFGS-B from four starts: all ones, a gradient-based corner, and two seeded random vectors. We stop at the first ratio with a negative quadratic value. No global minimum or minimum reversal ratio is claimed. The variance vector is the same in the observed and control models. The witness does not change contact counts or site groups. No biological plausibility claim is made for these fitted variance vectors.

## Results

| Map | Sufficient ratio limit | Reversal ratio used | Equal-variance observed D | Equal-variance reference D | Reversal observed D | Separate control mean D | Separate draws with reversal |
|---|---:|---:|---:|---:|---:|---:|---:|
| 1 | 2.169 | 10 | 54.18 | 57.06 | 46.58 | 46.17 | 187/200 |
| 2 | 2.189 | 10 | 57.16 | 60.20 | 47.17 | 46.77 | 184/200 |
| 3 | 2.188 | 10 | 57.16 | 59.76 | 46.39 | 45.92 | 195/200 |
| 4 | 2.255 | 10 | 58.14 | 61.04 | 47.67 | 47.52 | 149/200 |
| 5 | 2.253 | 10 | 60.72 | 63.45 | 50.55 | 50.33 | 157/200 |
| 6 | 2.331 | 100 | 57.87 | 61.47 | 42.21 | 41.89 | 182/200 |
| 7 | 2.319 | 100 | 62.85 | 66.07 | 32.15 | 31.94 | 182/200 |
| 8 | 2.341 | 100 | 61.74 | 65.07 | 39.50 | 38.92 | 193/200 |

All eight sufficient ratio limits exceeded two. Explicit reversal vectors had variance ratios of 10 in maps 1-5 and 100 in maps 6-8. Their negative q values also held against the separate validation Gram means. The ordinary mean validation dimension was below the observed dimension in every map. Individual validation draws reversed in 149 to 195 of 200 draws, so the witnesses do not reverse every possible control. These counts describe a conditional simulation and are not population p-values.

Swap acceptance fractions ranged from 0.405 to 0.578. The largest measured lag-one correlation of witness q across the validation chains was 0.108. These diagnostics do not prove mixing of all site configurations. Training and validation results are from the same swap model. Validation reduces control-draw fitting effects; it does not supply independent animals or measured source variances.

## Independent checks and meaning

Files/verify.py separately rebuilds dense source covariance matrices from the retained site table, exactly matches their observed Gram matrices, checks weighted covariance norms, checks training and validation means, and tests the certificate identity and sampled variance vectors. All checks passed for all eight maps. The analysis also checks fixed source-target margins through each source covariance diagonal and checks site sizes after swaps. Code, all source variance vectors, per-chain mean Gram matrices, per-draw q scores and numeric summaries are supplied.

The equal-variance result is stable to a bounded amount of source heterogeneity under this finite reference. It is not an invariant of the pair-count wiring graph or site grouping alone. Strong enough changes of source weights can change the result while all pair counts and site sizes stay fixed. This specifies one uncertainty that physiological measurements must resolve before these structural noise dimensions can be used to explain reliable representations.

The model omits correlated source spikes, recurrent propagation, target filtering, electrical coupling, receptor signs, unequal target gains and unequal variances among sites of the same source. Site variances can reflect release statistics or amplitude scales, but these data identify neither. Low dimension can help or harm a decoder depending on signal alignment. We do not infer coding loss, adaptation, real noise covariance or conservation across animals and brain regions. Unknown geometry and annotation error can affect the control comparison. The gap between the sufficient limits and found reversals remains unresolved.

## Reproduction and identity

Use files/REPRODUCE.txt. A small independent check needs only the bundled site groups and numeric matrices. The full rerun reads immutable shared raw files and checks their hashes. files/requirements.txt pins the private environment. files/IDENTITY.txt records job, topic, machine, account and model. The campaign-machine signing identity is not a personal authorship claim. All publication output is saved locally.
