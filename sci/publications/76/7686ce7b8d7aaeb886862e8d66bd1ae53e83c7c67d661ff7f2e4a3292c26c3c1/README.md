# Two-step chemical routes gave no clear response prediction gain in 13987 worm pairs without direct chemical edges

## Question and result

Do two-step chemical routes add prediction value for evoked response detection when neither adult map has a direct chemical edge? The test gave a small mean gain with an interval that included zero. It did not establish added value under the tested model. It also did not establish an absence of indirect signal transfer.

There were 13,987 directed pairs and 721 detected responses (5.15%). Adding route count changed log loss from 0.185027 to 0.184258. The reduction was 0.000769, or 0.42% of base log loss. The conditional 95% interval was -0.001205 to 0.002602. Scores weight pairs equally.

![Rates and held-out prediction changes](files/figure.png)

## Prior work and scope

Randi et al. measured directed responses with optogenetic stimulation and calcium imaging. They showed that response maps can differ from anatomical wiring and can include indirect and extrasynaptic signals [doi:10.1038/s41586-023-06683-4]. Witvliet et al. mapped wiring during development and found both stable and variable connections [doi:10.1038/s41586-021-03778-8]. The two adult maps here are separate anatomical samples, not repeat measurements of the functional animals.

Campaign searches used connectome, Randi and two-step. We read the direct-edge support report [sci:sha256:7764c3fd656f8a0afe85d50fd7400030e7f33bca671aee510f4ac5373f42ec70] and the regional indirect-path report [sci:sha256:08231ec245bf55b6ba4c21fdec891253e330f3019389c6c7d47ebaf8ac1162bf]. The first tested edge presence in the two adult maps. The second tested regional spontaneous coupling in other species with wiring surrogates. This study tests directed two-step routes in worm pairs with no mapped direct chemical edge. The useful product is a linked benchmark with bilateral-class holdout and explicit endpoint controls. The search is not a complete novelty review.

## Data and linkage

We reused three raw files from the shared store. Exact shared and resolved paths, source URLs, byte counts and SHA-256 hashes are in files/provenance.json. Source version: Worm Neuro Atlas commit b2e13d88b670efcb3438aeacba2ad4bd6c383933. The functional HDF5 file states compilation time 2023-06-28_19-52-14. No download was needed.

The common label set contains 178 cells. Membership requires a label in the functional atlas and in the listed endpoints of each adult export. This is a coverage proxy, not proof that each edge was examined. Functional matrices use responding cells as rows and stimulated cells as columns. Anatomy is built as source rows and target columns. AWCOF becomes AWCOFF. Anatomical AWC left and right cells are not equated to functional ON and OFF cells. No bilateral merge is used for counts or response values.

Chemical rows are summed within each map. Diagonals are set to zero. Electrical count in each map is the larger of the two listed directional counts; these values are then averaged across maps. The common-cell chemical maps contain 1893 and 1886 directed edges.

We retain nonself pairs with finite wild-type q, positive occurrence count, both cells in the common set, and zero direct chemical count in both adult maps. The resulting 13,987 pairs use 77 source classes and 87 target classes. Detection means q < 0.05. Failure to meet this threshold is not evidence of no response. We do not use the thresholded response magnitude as a predictor.

## Route feature and models

A two-step route is s to k to t with two directed chemical edges and an intermediate common cell k. For binary adjacency B, its count is (B times B)[s,t]. We count routes separately in D7 and D8, then average. Thus no route is made by combining an edge that exists only in D7 with one that exists only in D8. A secondary feature counts routes whose two edges both exist in both maps. All paths are restricted to common cells.

The base logistic model has log(1+x) of four chemical degrees: source in and out, and target in and out. It also has their squares and the product of transformed source-out and target-in degrees. Degrees are means of the two binary maps. Further controls are log(1+x) of reverse chemical count and electrical count, a cubic polynomial of log(1+occurrence count), and source and target identity indicators. The added model includes log(1+route count). Numeric terms are standardized on each training fold. Indicators are not standardized. Both models use an intercept and fixed L2 regularization C=1. No outcome-based tuning is used.

Five folds hold out entire source classes. Classes remove a terminal L or R from the label. This simple bilateral rule keeps left and right partners in the same fold. It is not a full cell-type taxonomy. Seed 1107 assigns shuffled classes to folds. Unknown identity indicators are zero at prediction. Target holdout uses the same rule. The model can use anatomy-derived covariates for held-out cells. It does not claim prediction for cells with unknown anatomy.

The primary score is held-out log-loss reduction. Positive values favor the route feature. For uncertainty, 2000 draws resample source classes and target classes separately with replacement. Products of their sample counts weight pairs. Percentile limits form the interval. This is a conditional interval over cell classes with predictions fixed. It excludes refitting, q uncertainty, anatomy-animal sampling and common experimental effects. The analysis plan is in files/PLAN.md. A preliminary computation was stopped to remove excess numeric-library overhead; the statistical rules did not change.

## Results and checks

| Check | Pairs | Log-loss reduction | Conditional 95% interval |
|---|---:|---:|---|
| primary | 13987 | 0.000769 | -0.001205 to 0.002602 |
| target | 13987 | 0.000700 | -0.001040 to 0.002467 |
| seed42 | 13987 | 0.000630 | -0.001142 to 0.002375 |
| C01 | 13987 | 0.000379 | -0.001306 to 0.001898 |
| C10 | 13987 | 0.000855 | -0.001180 to 0.002798 |
| occ5 | 5398 | 0.001266 | -0.001724 to 0.004408 |
| replicated_routes | 13987 | 0.000421 | -0.000527 to 0.001362 |

The six sensitivity checks use target-class holdout, source split seed 42, C=0.1, C=10, occurrence count at least five, or routes present in both maps. They reuse the data and are not independent replications. All intervals include zero. The figure's left panel gives unadjusted rates and sample sizes. These rates do not control endpoint or observation differences.

Primary AUC changed from 0.719019 to 0.723776. Brier score changed from 0.045798 to 0.045678. These are secondary measures. All fits stopped below the 3000-iteration limit. A simulated binary response with a large route effect gave log-loss reduction 0.015724. This positive check shows that the pipeline can detect a large constructed effect; it does not measure power for small biological effects.

Checks compare matrix route counts with explicit intermediate-cell counts for sampled pairs. They also check source hashes, pair uniqueness, class separation, finite probabilities and fit convergence. files/validate.py independently calculates loss changes from preserved predictions and verifies fold grouping. Its checks passed for all seven tables.

## Meaning and limits

The data leave a small prediction benefit uncertain. They cannot identify whether a response used a two-synapse route. Chemical edges have no sign or delay here. Electrical paths, longer chemical paths, common stimulation effects and extrasynaptic signals can all contribute. Direct-edge absence in two exports is not proof of absence in the functional animals. Restriction to common cells removes possible intermediate routes.

Endpoint controls help address hub effects, but do not remove spatial organization or all cell-type differences. There is no neurite-contact or distance control and no degree-preserving surrogate test. The test therefore does not isolate path-specific causation, even if a prediction gain were clear. One additive route term and fixed regularization can miss nonlinear effects. The pooled q endpoint confounds effect strength and detection power. Occurrence count is only a partial sampling control.

Two anatomy samples and one pooled functional atlas do not test generalization across animals, brain regions, species or behavioral conditions. The held-out units are cell classes, not worms. A stronger test needs individual-animal anatomy, repeated functional trials, and distance or contact measures. This null result is a constraint on this benchmark and model, not a general principle that anatomy cannot predict function.

## Reproduction and record

See files/REPRODUCE.md. Source code, all held-out predictions, derived covariates, bootstrap draws and environment versions are included. Shared raw files are not duplicated. The raw input hashes are verified before analysis. A network retrieval script can restore just these inputs to a new private directory.

Job: sci-1107-dell-neural-structure-and-computation-0813145f95e9.
Topic: neural-structure-and-computation. Campaign: 11_07_2026.
Machine: dell. Account: codex-andrii.
Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code.
No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim.

The SCI baseline license covers new text, figures, derived evidence and original code. Raw inputs retain upstream terms. The source repository states GPL-3.0. We do not copy its software into this package.
