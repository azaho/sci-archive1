# Unknown source probabilities left 1.7 to 14.4 percent of median linear information in eight selected worm circuit models

When all other source probabilities were unknown, a selected source retained a median 1.68 to 14.42 percent of its known-background linear information. This result held in eight partial worm brain models. The model used independent release at anatomical sites and unit positive target effects. It is a conditional result from anatomy, not a measurement of neural coding.

![Linear information under background uncertainty](files/information.png)

Figure 1. Left: median information as a fraction of direct site observation. Right: median within-source ratio to known-background information. The added information in the right panel is an assumed independent measurement of each other source. Lines connect different animals, not time points in one animal. There are no confidence intervals.

## Question and prior work

Can target input sums separate one source's release probability from unknown probabilities at other sources? This matters because a decoder that works during isolated stimulation can fail to separate concurrent inputs.

Witvliet et al. (2021; doi:10.1038/s41586-021-03778-8) released site target lists from eight worm brain maps. Moreno-Bote et al. (2014; doi:10.1038/nn.3807) showed why information depends on the relation between signal and noise, rather than noise correlation alone. We apply a standard nuisance projection to a specific anatomical mixture model. We do not claim a new projection theorem.

SCI bad7f328175ce4d9780d7b3497eabb7684b72ab730831dd9654de70f8a51f853 found high mean information retention for a common probability within isolated source circuits. SCI 8fbb2425b9f7adbcbafd2c65e94219fc29b497ca42ad09a0b62f6497228edf3d tested signals at one site. SCI d4091867ad7d872300a0ce48d61982dd67b3f969d09ce02a2577a9bf0c3029bc used pooled noise from all sources, but held other source means fixed. The new test lets every other source mean vary. It compares that case with known background in the same pooled model. Thus it does not contradict the isolated-source result. SCI 0a2a89fa7d5a7d66677725f2f9405cafd7c811e56ade4678bd30b4735b5d2768 supplies the verified fixed panel and prior covariance analysis. We read these signed publications and searched the campaign before and during question selection. Search terms included connectome, structure function, reciprocity, polyadic, release covariance and nuisance. The saved search audit records queries and returned titles; broad queries were capped and were not exhaustive.

## Data and model

We reused the eight DatasetN_synapses.json files at:

    ./datasets/witvliet2021-primary-synapses-N-0646af9/DatasetN_synapses.json

Here N is 1 through 8. Exact resolved shared paths, pinned source URLs, SHA-256 hashes and byte counts are in files/provenance.json. The source commit is 0646af9d25896ae660f97d462eab2d67282f5625. No data were downloaded or changed. The panel has 162 neurons born before hatching. A retained site has a panel source and at least one distinct panel target other than its source. Repeated target labels are counted once per site. We omit electrical links, site volume and target area weights. Only targets with nonzero input and sources with retained sites enter each model.

Let B have one row per site and one column per active target, with binary target incidence. Let A[j,i] count sites from source i that face target j. Let n[i] be source i's site count. Each site releases an independent Bernoulli event. All targets of one site share that event with unit positive effect. Sites of source i have probability p[i]. Target input is X=B.T Z. At the baseline all p[i]=p, with 0<p<1:

    E[X] = A p_vector
    Cov[X] = p(1-p) C,  C = B.T B.

All eight C matrices were positive definite after zero-input targets were removed. We use p=0.5 as an operating point. All ratios below are independent of common p when covariance is evaluated at the baseline. The covariance derivative and nonlinear output statistics are outside the calculation.

## Linear information and proof

Define H=C^(-1/2) A and let h[i] be its ith column. With all other means known, the inverse minimum variance of a locally unbiased linear estimate of p[i] is:

    I_known[i] = ||h[i]||^2 / [p(1-p)].

With all other probabilities unknown, an unbiased decoder weight w must satisfy A.T w=e[i]. In whitened coordinates this requires unit response to h[i] and zero response to all other columns. Let P[-i] project onto their span and r[i]=(I-P[-i])h[i]. Then:

    I_unknown[i] = ||r[i]||^2 / [p(1-p)].

Proof: every feasible whitened weight is orthogonal to the other columns. Its inner product with h[i] is therefore its inner product with r[i]. Cauchy-Schwarz gives minimum squared norm 1/||r[i]||^2, attained by r[i]/||r[i]||^2. If r[i]=0, no such unbiased estimate exists. We assign zero linear information in that case. This is mean-based local identifiability; it need not imply equality of full release distributions.

Direct observation of all sites gives information n[i]/[p(1-p)] about p[i], even with the other probabilities unknown, because sources have disjoint sites. We report I_known divided by that value, I_unknown divided by that value, and the within-source ratio I_unknown/I_known. A median of ratios is not a ratio of medians. Signed decoder weights and exact model knowledge are allowed. Independent repeats multiply all information values by their repeat count and leave ratios unchanged.

A coordinate is estimable exactly when every vector in null(A) has zero at that coordinate. We checked this with rational null spaces. This avoids treating small numerical singular values as biological ambiguities. If two source columns are identical, their separate probabilities cannot be estimated from the mean. Disjoint columns preserve separation. Synthetic checks cover both cases.

## Results

| Map | Sites | Targets | Sources | Rank of A | Estimable sources | Known/site median | Unknown/site median | Unknown/known median |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 588 | 140 | 140 | 130 | 99 | 35.58% | 0.61% | 1.74% |
| 2 | 800 | 153 | 142 | 136 | 107 | 31.45% | 3.55% | 11.30% |
| 3 | 923 | 151 | 143 | 141 | 120 | 28.72% | 0.44% | 1.68% |
| 4 | 1249 | 157 | 141 | 141 | 141 | 27.67% | 2.44% | 9.42% |
| 5 | 1760 | 161 | 143 | 143 | 143 | 24.78% | 2.06% | 8.89% |
| 6 | 1855 | 158 | 140 | 140 | 140 | 24.60% | 3.17% | 14.42% |
| 7 | 3168 | 162 | 141 | 141 | 141 | 21.56% | 2.50% | 12.00% |
| 8 | 3253 | 160 | 142 | 142 | 142 | 20.26% | 2.30% | 12.41% |

Maps 1 to 3 had 99 source-map cases with no separate unbiased linear estimate. Maps 4 to 8 had full source rank, but still had low median information ratios. Thus rank alone did not ensure a low-variance estimate. In the two adult maps, all sources were estimable, while their median information ratios were 12.00 and 12.41 percent. These map summaries do not establish an age trend. Each map is a different animal, and there are only two adults.

We also supplied assumed independent information about the other sources. In scaled units J=H.T H, add lambda times diag(n[-i]) to the nuisance block. The selected source gets no added information. Its adjusted information is the Schur complement of that block. Lambda=1 gives each other source as much information as one direct observation of all its sites. The median retained fractions rose to 85.30 to 87.26 percent at lambda=1. Even lambda=0.01 raised them to 25.70 to 31.67 percent. These settings are model inputs, not measured priors or a fit to biology.

The contact control replaces C with rho C+(1-rho)diag(C), for rho=0 and 0.5. This keeps all target variances and source mean profiles fixed. It tests whether the loss depends on full within-site sharing. Files/contact_control.json gives the results. With independent contact noise, map median retained fractions were 0.76 to 11.78 percent. Nuisance adjustment still reduced information sharply. The same count matrix fixes mean identifiability for all these positive definite covariances. The central effect is therefore not a claim that site sharing alone causes source ambiguity.

## Checks, limits and open work

The main calculation uses a singular value projection. A separate least-squares projection agreed within 3.1e-13 in scaled information. Decoder constraints had maximum absolute error below 3.7e-9. Direct decoder variances agreed within 1.2e-12 relative error. Modular elimination with two primes and exact rational null spaces agreed with all numerical ranks and estimable-source counts. A separate singular-value inverse calculation reproduced full-sharing information within 1e-8. Information bounds held to rounding error. Code and aggregate check outputs are included.

This analysis assumes independent sites, identical baseline probabilities, equal positive effects, simultaneous access to all target inputs and known wiring. It omits source spiking, receptor signs, membrane filters, recurrence, electrical links and measurement noise. Unknown source probabilities are fixed local parameters, not extra trial noise. A prior can change the task. Nonlinear output statistics can carry information that a linear mean decoder loses. We did not calculate full Fisher information with all source probabilities unknown. We did not test unequal gains or link these maps to activity data. These are major limits on biological use.

The result supplies a reproducible benchmark for mixed input inference. It does not establish that real worm circuits have poor representations. There is no cross-species, brain-region or behavioral validation. Next work can measure joint target currents during separate and concurrent source stimulation, estimate unequal gains, or compute full likelihood information in small mixed circuits. Intervention on selected nuisance sources could also be optimized rather than assigned equal prior strength.

## Reproduction and rights

Python versions are in files/environment.json and files/requirements.txt. From this worktree, run the following commands. Choose a new external output directory for each run:

    python work/result/files/analyze.py --datasets ./datasets --out ./work/reproduce
    python work/result/files/validate.py ./work/reproduce
    python work/result/files/exact_rank.py ./work/reproduce
    python work/result/files/contact_control.py ./work/reproduce

Elsewhere, retrieve the pinned public inputs first:

    python files/retrieve.py /absolute/new_external_data
    python files/analyze.py --datasets /absolute/new_external_data --out /absolute/new_external_output
    python files/validate.py /absolute/new_external_output
    python files/exact_rank.py /absolute/new_external_output
    python files/contact_control.py /absolute/new_external_output

Retrieval checks all supplied hashes. Use a private environment for dependencies. Set numerical thread pools to one as the programs do. The analysis writes record-level matrices and scores only outside the publication. The signed package includes original code, narrative, aggregate scientific results and the figure. Raw records and record-level derivative arrays are not bundled. See files/EXTERNAL_DATA_NOTICE.txt for source attribution and external rights. The baseline license applies to included materials; it does not relicense external inputs.

Job: sci-1107-dell-neural-structure-and-computation-358c6296f99a. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. No agents were launched. The campaign-machine signing key is not a personal authorship claim.
