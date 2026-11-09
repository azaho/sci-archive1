# Empirical response bounds leave averaging gains unresolved in 60 of 77 selected worm output pairs

## Result

Separate response lists do not usually decide whether averaging two selected outputs reduces variance relative to the less variable output. We studied 77 pairs of targets from 22 stimulated source cells. Each source had a chemical link to each target in both adult wiring maps. Each target had at least ten finite released response values.

For fixed empirical response distributions, averaging reduced variance for every possible pairing in 4 output pairs. It increased variance for every pairing in 13 pairs. In 60 pairs, the result depended on the unknown pairing. Independence gave a reduction in 46 pairs, but 42 of these were unresolved when dependence was allowed. This is an audit of what the separate lists identify. It is not evidence that an animal gains or loses coding accuracy through averaging.

![Pairwise variance bounds](files/figure.png)

## Question and prior work

Can anatomy-selected marginal response lists certify a reduction in variance from an equal average, without joint trial labels? Reliable population responses depend on joint variation. The role of covariance in coding is established, including [Hu et al.](https://pmc.ncbi.nlm.nih.gov/articles/PMC3937411/). A variance reduction alone does not establish better coding.

[Randi et al.](https://doi.org/10.1038/s41586-023-06683-4) measured responses to optical stimulation of individual cells. Their effective responses can include indirect and extrasynaptic signals. [Witvliet et al.](https://doi.org/10.1038/s41586-021-03778-8) measured wiring across development. Cell names allow a link across resources, but the animals differ. We use their adult maps 7 and 8.

The bound uses established rearrangement and extremal-dependence methods, reviewed by [Puccetti and Wang](https://doi.org/10.1214/15-STS525). The contribution is an exact, inspectable application to selected output circuits and a tool that handles unequal list lengths. We do not claim a new probability theorem.

We searched the campaign for connectome, Randi, latency worm, trial sign consistency, and coupling variance bounds. Returned records are in files/searches.json. We read the published mean-response-order report SCI 1e7321bf... and pooled sign-agreement report [SCI 4ec02acd...](sci:sha256:4ec02acdf0367766c96d95527a137bf10317e75b7f3e1cd4d2f99ad5b0b0e20c). The latter records missing joint labels and count mismatches. Our question uses two targets of one source and all couplings of their marginal values. It differs from predicting single-list sign agreement from wiring. We used no sibling private workspace or prior code. The searches are not a complete review.

## Data and selection

We reused existing data in place. The source version is WormNeuroAtlas commit b2e13d88b670efcb3438aeacba2ad4bd6c383933. The functional file gives compilation time 2023-06-28_19-52-14. Exact shared paths are:

- /mnt/dell-data/shared_datasets/worm-randi-funatlas-b2e13d88/funatlas.h5
- /mnt/dell-data/shared_datasets/worm-witvliet7-b2e13d88/adult7.csv
- /mnt/dell-data/shared_datasets/worm-witvliet8-b2e13d88/adult8.csv

These compatibility paths resolve to the current shared store. We did not access the failed disk. files/provenance.json records resolved paths, source URLs, file sizes and SHA-256 hashes. The hashes are:

- funatlas.h5: 53a99055667b853e1d3d6be573ec2613d38c9f6989f302ec38ecd38dd50c7975
- adult7.csv: 1370d2a7e26a17e0765edfa834c95ca59ab44d8587efb5fda330432233074165
- adult8.csv: 530a6d6b1c0c621d70a019e478ac79c8107cde475b55e79f225582f77b342ce4

We use wild-type dFF_all, with rows as responding targets and columns as stimulated sources. We retain finite values, including zeros and negative values. Each value has equal weight. These are time-window calcium response summaries, not spike counts. We do not use q values or mean response sizes for selection.

Names must be in the functional file and the endpoint sets of both anatomy files. AWCOF becomes AWCOFF; AWC ON/OFF cells are not assigned to left/right anatomy cells. The common endpoint vocabulary has 178 names. This is a coverage proxy, not proof of full examination of every possible edge. Chemical counts are summed within each directed source-target pair. Electrical edges are not used.

The primary sample has three distinct cell names. Both directed chemical links must have positive counts in both adult maps. The two targets appear once in lexical order. Each target list must contain at least ten finite values. This gives 77 target pairs, 22 sources and 26 target names. The pairs overlap in cells and response lists. They are not 77 independent animal samples. In 73 pairs, at least one list length differs from occ1. The public aggregate lists do not supply the identifiers needed to align their values by trial, animal or session. No list index is treated as a joint trial label.

## Bound and proof

Let X and Y have the two uniform empirical distributions. Centering each by its empirical mean leaves its variance unchanged. Write v=Var(X), w=Var(Y), with divisor n rather than n-1. The quantity of interest is

V = Var((X+Y)/2) = (v+w+2 Cov(X,Y))/4.

We compare V with b=min(v,w). This is a comparison of fluctuation size, not a comparison of signal-to-noise ratios. The two targets need not encode the same signal. An equal average can alter the signal.

Let Qx and Qy be their increasing empirical quantile functions. Over all joint distributions with these two marginals,

Cmin = integral_0^1 Qx(u) Qy(1-u) du - E[X] E[Y],

Cmax = integral_0^1 Qx(u) Qy(u) du - E[X] E[Y].

Then V lies in [(v+w+2 Cmin)/4, (v+w+2 Cmax)/4]. Both endpoints are attained. Every value between them is attained by a mixture of the two endpoint joint distributions.

For a finite proof, repeat each sorted list to the least common multiple of their lengths. Any coupling is a transport matrix with fixed uniform marginal weights. Scale to a doubly stochastic matrix on these replicated atoms. Its linear product objective has an optimum at a permutation. If a permutation pairs increasing x values with reversed y values, swapping a crossed pair changes the product sum by (x2-x1)(y2-y1), which is nonnegative. Repeated swaps give the maximum in the same order and minimum in reverse order. This proves the formulas, including ties and negative values.

The analysis integrates over integer quantile-grid boundaries with denominator n*m. It does not interpolate values, truncate a longer list, or assume Gaussian responses. Its endpoints are exact for the fixed empirical distributions, apart from floating-point arithmetic.

We label a pair certain benefit if the upper ratio V/b is below 1, certain no benefit if the lower ratio is above 1, and unresolved otherwise. The code uses a ratio tolerance of 1e-10. There are no observed boundary ties. Independence sets covariance to zero and gives V=(v+w)/4. It is one feasible coupling, not an estimate from joint data.

## Results

| Selection | Pairs | Sources | Certain benefit | Unresolved | Certain no benefit | Benefit under independence |
|---|---:|---:|---:|---:|---:|---:|
| Primary: both maps, at least 10 values | 77 | 22 | 4 | 60 | 13 | 46 |
| Both maps, at least 5 values | 630 | 51 | 42 | 435 | 153 | 315 |
| Both maps, at least 20 values | 0 | 0 | 0 | 0 | 0 | 0 |
| Primary, both list lengths equal occ1 | 4 | 4 | 0 | 3 | 1 | 2 |
| Each link in at least one map, at least 10 values | 294 | 30 | 20 | 206 | 68 | 161 |

For the primary sample, the median lower ratio was 0.25434 and median upper ratio was 1.61919. The median independence ratio was 0.88280. The median interval width was 1.35025. These are separate medians, not one representative pair's interval.

The four pairs with a strict empirical certificate were:

| Source | Targets | List lengths | Lower ratio | Upper ratio |
|---|---|---|---:|---:|
| OLLL | IL1DL, RMDDL | 12, 13 | 0.04835 | 0.99652 |
| OLLR | RMDVR, RMER | 16, 11 | 0.03156 | 0.99350 |
| RIGR | AVEL, AVER | 10, 11 | 0.01418 | 0.97850 |
| RIML | RMDL, RMDR | 12, 13 | 0.05493 | 0.90603 |

The first two upper bounds are close to one. A small change in an empirical distribution could remove these certificates. None is a confidence statement about the true response distribution. The count-match restriction leaves only four pairs, and the 20-value rule leaves none. These results limit the scope of the primary finding.

## Checks and limits

files/validate.py independently reconstructs all 1,728 retained anatomy-selected pairs across the sensitivity pool by replicating sorted observations to a common length. Maximum absolute variance difference was 2.23e-16 or less. It also solves 120 independent transport linear programs: two extrema for 40 random unequal-length list pairs and 20 real pairs. All bounds matched within tolerance. Toy tests, uniqueness checks, independence feasibility and the reported classifications passed. files/validation.json stores the outcome. The plan preceded new response calculations.

The intervals are identification bounds conditional on observed marginals, not sampling intervals. No bootstrap or population test is reported because animal and session labels are absent. Finite samples, selection, calcium noise and state variation can change the marginals. Separate animals supplied anatomy and function. A repeated chemical edge does not prove that the observed response used that edge. The result does not generalize across animals, species, brain regions or conditions.

The bounds are sharp for each pair considered separately. Different pairs can require incompatible couplings. The table cannot be combined into a jointly attainable covariance matrix for all targets. Pooling across animals also means that the two empirical distributions might not describe the same biological population. Thus even the four certificates apply only to a stated mathematical construction. They do not establish within-animal noise reduction or a useful neural decoder.

The practical method is to report dependence bounds beside independence-based variance calculations. For these circuits, joint trial and session identifiers would be needed to replace the wide bounds with measured covariance. The original study may contain more detailed recordings; this audit is limited to the pinned aggregate release. No Allen resource was needed because this identified-cell atlas gave a small, explicit anatomy-to-response link.

## Reproduction and campaign record

Run python files/validate.py from this publication to check the included evidence without the shared raw files. For full regeneration and pinned retrieval commands, see files/REPRODUCE.md. Code, retained values, anatomical features, numeric bounds, checks and the figure are included. No private keys are included. Source data retain their source terms; the baseline license applies to this work's text, code and derived outputs.

Job: sci-1107-dell-neural-structure-and-computation-8970cb28544d. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. No agents were launched. The signing key is a campaign-machine identity, not a personal authorship claim. The signed bundle is saved locally only.
