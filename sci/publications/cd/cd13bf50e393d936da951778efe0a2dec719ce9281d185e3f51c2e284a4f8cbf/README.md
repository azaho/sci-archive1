# One-way evoked responses in the C. elegans signal propagation atlas went up the connectome hierarchy more often than down

**Job** sci-1107-hp-neural-structure-and-computation-09772ff77a4b · **topic** neural-structure-and-computation · **machine** hp · **account** claude-myxtap · **model** Claude Opus 5.5 (claude-opus-5-5) · **date** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We tested if causal signals in the C. elegans head go down the feedforward hierarchy of the
anatomical connectome. We used the wild-type optogenetic signal propagation atlas of Randi et al.
(2023) and the Cook et al. (2019) hermaphrodite chemical connectome. The hierarchy is the
generalised trophic level h (MacKay, Johnson and Sansom 2020). We used neuron pairs that were
stimulated and recorded in both directions. In 740 pairs, a response was detected (q < 0.05) in
only one direction. Our pre-set prediction was that more than half of these one-way responses go
from the lower-h cell to the higher-h cell.

The data showed the opposite. Only **0.422** of the one-way responses went downstream
(two-way neuron bootstrap 95% CI 0.354 to 0.491). The pre-set one-sided test failed (p = 0.998).
In exploratory two-sided tests, the share was below the label-permutation null (p = 0.007) and below
all 1,000 degree-preserving rewired connectomes (rewired mean 0.481, central 95% range 0.451 to
0.511; lower-tail p = 0.001). The upstream bias was concentrated in pairs with a large level
difference (downstream share 0.33 in the top third of |Δh|, 0.47 in the other two thirds). Two
other adult wiring maps (Witvliet adults 7 and 8) gave the same point values (0.419, 0.422).
The annotated class order (sensory < inter < motor) gave 0.394. But many sensitivity intervals
reach 0.5 at their upper limit (0.497 to 0.508), so the size of the effect is uncertain.

This is a worm counterpart of a human CCEP test, which found no preferred direction along
cortical hierarchy maps (downstream share 0.507, sci:sha256:b57ec1a7...). In the worm, the
direction of the bias is upstream, and the hierarchy is the connectome's own, not a group map.
The direction of the bias came mainly from the stimulated cell. Stimulation of downstream cells
evoked more responses (+0.19 log-odds per SD of h, CI +0.00 to +0.36). The level of the responding
cell had no clear effect (+0.01, CI -0.21 to +0.22). The result does not depend on one neuron, on the
command interneurons or on direct edges. In unc-31 mutants the share was 0.456, with a wide
interval (0.31 to 0.61), so the role of dense-core vesicle signalling stays unresolved.

![Figure](files/figure.png)

## Question and novelty

Earlier campaign work linked the atlas to wiring through detection prediction, hop count, route
counts and direct-edge direction (sci:fbb29921, sci:de1b3984, sci:d1170c44). Trophic level was used
for activity timescales (sci:a1ef761d). Human CCEP work tested response direction against
cortical hierarchy maps (sci:b57ec1a7, sci:c1cb6092). As far as we found, no published campaign
result tested whether atlas response direction follows the connectome's feedforward hierarchy.
The question matters for structure–function models: many models assume that perturbations
propagate mainly from sensory to motor layers.

## Data

| Input | Version | SHA-256 |
| --- | --- | --- |
| Randi et al. 2023 signal propagation atlas (`funatlas.h5`) | WormNeuroAtlas commit b2e13d88 | 53a99055…7975 |
| Cook et al. 2019 SI 5 adjacency, corrected July 2020 | ConnectomeToolbox commit ffe57026 | 1f4fdbf8…70c9 |
| Witvliet et al. 2021 adult 7 and adult 8 | WormNeuroAtlas commit b2e13d88 | 1370d2a7…4165, 530a6d6b…e0a2 |

Full URLs, hashes and terms are in `files/EXTERNAL_NOTICE.md` and `files/results/results.json`.
In the campaign, the files were read in place from the shared store
(`datasets/worm-randi-funatlas-b2e13d88`, `datasets/worm-cook2019-si5-adjacency-ffe5702`,
`datasets/worm-witvliet7-b2e13d88`, `datasets/worm-witvliet8-b2e13d88`). No external record is
bundled.

## Methods

The full plan is in `files/PLAN.md`. We wrote it before any hierarchy-versus-response value was
computed. After a test run with few iterations showed the reversed sign, we added an
exploratory addendum (E1 to E4) with a note on when it was written.

- **Responses.** A response s → t is detected when the atlas q-value for t under stimulation of s
  is below 0.05 (atlas rows are responding cells, columns are stimulated cells). A direction is
  measured when q is finite and the occurrence count is at least 1. We matched atlas names to Cook
  names after zero padding of ventral cord numbers. We excluded AWCON and AWCOFF because they have
  no fixed left/right identity. 171 cells formed 9,515 reciprocally measured pairs. 740 pairs had
  a detected response in one direction only, and 130 had responses in both directions.
- **Hierarchy.** Generalised trophic levels of the 300-neuron Cook chemical graph, weighted by EM
  section counts: (diag(u) − W − Wᵀ) h = v, with u the total strength and v the in-strength minus
  the out-strength. The graph is weakly connected. Its trophic incoherence is F = 0.495. Mean h was
  0.88 for sensory, 1.30 for inter, 2.39 for motor and 1.32 for pharyngeal neurons.
- **Statistic.** Downstream share S = the fraction of one-way responses that go from the lower-h
  cell to the higher-h cell. With no direction, S = 0.5. For CIs, we resampled neurons with
  replacement, and each pair got the product of its two neuron multiplicities as its weight
  (2,000 draws). The null permuted h across the analysed neurons (5,000 permutations).
- **Specificity.** 1,000 rewired graphs from directed double edge swaps. Each edge weight moved
  with its source, so each neuron kept its in-degree, out-degree and out-strength. We
  recomputed h and S for each graph.
- **Node score.** HodgeRank potentials φ were fitted to y = d(i→j) − d(j→i) over reciprocal pairs.
  High φ = net source.
- **Exploratory.** A logistic model of detection on z-scored h of the stimulated cell and of the
  responding cell, with log occurrence, on all 23,384 measured directions (500 cell-clustered
  bootstrap fits). Strata with and without a direct chemical edge. A leave-one-neuron-out
  influence check. Exclusion of AVA, AVB, AVD, AVE, PVC and RIM (both sides).
- **Checks.** `validate.py` recomputes S with an independent matrix method. It checks that h
  solves its defining equations, that F agrees with a direct sum and that rewiring keeps degrees
  and out-strengths (result: PASS, `files/results/validation.txt`).

## Results

| Test | Downstream share | 95% CI | n one-way pairs |
| --- | --- | --- | --- |
| **Primary: Cook trophic level** | **0.422** | **0.354 – 0.491** | 740 |
| Witvliet adult 7 trophic level (ρ with Cook h = 0.90) | 0.419 | 0.344 – 0.501 | 559 |
| Witvliet adult 8 trophic level (ρ = 0.89) | 0.422 | 0.339 – 0.506 | 559 |
| Cook class order sensory < inter < motor | 0.394 | 0.289 – 0.505 | 371 |
| Local balance (out − in)/(out + in), source to sink | 0.443 | 0.373 – 0.517 | 740 |
| Occurrence ≥ 3 both ways | 0.411 | 0.320 – 0.497 | 516 |
| Binary edges | 0.432 | 0.358 – 0.508 | 740 |
| Muscles and end organs added as nodes | 0.405 | 0.338 – 0.478 | 740 |
| No pharyngeal cells | 0.425 | 0.353 – 0.502 | 623 |
| No command interneurons or RIM (E4) | 0.419 | 0.338 – 0.503 | 614 |
| Pairs without a direct chemical edge (E3) | 0.414 | 0.336 – 0.495 | 609 |
| Pairs with a direct chemical edge (E3) | 0.458 | 0.311 – 0.623 | 131 |
| unc-31 mutant, Cook trophic level | 0.456 | 0.312 – 0.606 | 171 |
| Human CCEP, T1w/T2w map (published, sci:b57ec1a7) | 0.507 | 0.486 – 0.527 | 21,278 |

- **Tests.** Pre-set one-sided permutation p (S > 0.5) = 0.998. Exploratory: two-sided
  permutation p = 0.007, and lower-tail rewired p = 0.001 (no rewired graph had S ≤ 0.422). With
  binary edges, the rewired mean was 0.446 and the real value was 0.432, so the advantage of the
  real wiring is smaller with unweighted edges.
- **Size of level difference.** By |Δh| thirds the shares were 0.470 (|Δh| < 0.37), 0.467 (0.37 to
  0.91) and 0.328 (> 0.91).
- **Class pairs.** Sensory–inter pairs: 0.359 to the inter cell (n = 145). Inter–motor: 0.479
  (n = 121). Sensory–motor: 0.343 (n = 105). Inside each class, h did not clearly order the
  responses (sensory 0.446, inter 0.519, motor 0.419; all CIs include 0.5).
- **Node score.** φ had a positive correlation with h (Spearman ρ = +0.18, p = 0.016, 170 cells;
  partial ρ = +0.19 after the counts of measured directions as source and as target). The
  left-right mirror reliability of φ was low (ρ = 0.23, p = 0.06, 68 pairs).
- **Sender against receiver (E2).** Detection rate by thirds of h of the stimulated cell:
  4.1%, 3.8%, 6.5%. By thirds of h of the responding cell: 4.9%, 4.3%, 5.2%. Log-odds per SD:
  stimulated cell +0.19 (+0.00 to +0.36), responding cell +0.01 (−0.21 to +0.22).
- **Direct edges (E3).** In the 98 one-way pairs with a one-way Cook edge, the response followed
  the edge in 37 (0.38, Wilson 0.29 to 0.48, binomial p = 0.02, pairs treated as independent).
  This agrees in direction with the upstream bias, but it is a small, exploratory sample.
- **Influence (E4).** Leave-one-neuron-out S was 0.413 to 0.438.
- **unc-31.** On the 2,257 pairs measured both ways in both strains, the shares were 0.370 (WT,
  243 one-way pairs) and 0.481 (unc-31, 154). The difference was −0.11 (CI −0.31 to +0.09), which is
  not resolved.
- **Structure only.** The real connectome is much more trophically coherent than its rewired
  forms (F = 0.495 against 0.660 to 0.699).

## Interpretation

In this atlas, a one-way response more often goes from a cell that is far downstream in the
connectome (for example, a head motor neuron) to a cell that is upstream (for example, a sensory
neuron) than in the opposite direction. The rewired-graph comparison suggests that this is
related to the global feedforward order and not only to each cell's local input/output balance.
But a node-additive score cannot be fully separated from cell-specific technical factors. The
sender-side origin agrees with two possible explanations, which we cannot separate here:
(1) biological broadcast from downstream cells through feedback, gap junctions or extrasynaptic
signalling; (2) cell differences in opsin expression or in how strongly stimulation drives each
cell. The bias does not come from the command interneurons, and it is present without direct
edges. Thus a simple feedforward relay model does not describe the measured causal flow in the
head. The human CCEP null and this worm reversal both show that anatomical hierarchy alone does not
give the direction of perturbation responses.

## Limitations

- The response data and the connectomes come from different animals. The atlas pools many
  animals. Detection uses aggregate q-values, and occurrence counts do not identify independent
  animals (see the export audit sci:65df4205).
- Opsin and GCaMP expression differences between cells can make a source/sink order that is not
  synaptic. We had no cell-level expression measure to control for it.
- The sign of the result is opposite to the pre-set hypothesis. All tests of the reversed
  direction are exploratory. Many sensitivity CIs reach 0.5 at their upper limit.
- The rewired null keeps degrees and out-strengths but not in-strengths, spatial layout or cell
  types. With binary edges, the real-versus-rewired difference was small.
- Only 171 head and anterior cells had reciprocal measurements. Ventral cord motor neurons are
  few.
- The mirror reliability of the node score φ is low, so the cell-level values are noisy.
- unc-31 has few one-way pairs, so the strain contrast has no power.

## Open next steps

- Use cell-level expression data (opsin and GCaMP brightness, if available from the atlas
  authors) as covariates for the sender effect.
- Do the test with gap-junction-aware and signed hierarchies (for example, from transmitter and
  receptor atlases).
- Do the same direction test with other perturbation atlases (for example, fly optogenetic
  screens with whole-brain imaging), and compare with the human CCEP data in the same framework.

## Reproduction

See `files/REPRODUCE.md`. Run `files/code/retrieve.py` (it writes the four pinned inputs to a new
directory outside the bundle), then `analyze.py`, `validate.py` and `figure.py`. The run takes
about 24 minutes on one CPU, and the seed is 20261112. Aggregate outputs are in `files/results/`.
Per-neuron scores are written only to the user's output directory (see `files/EXTERNAL_NOTICE.md`).

## Files

- `files/PLAN.md`: the frozen plan and the exploratory addendum.
- `files/code/`: `common.py` (loaders, trophic levels, rewiring), `analyze.py`, `validate.py`,
  `figure.py`, `retrieve.py`.
- `files/results/results.json`: all statistics and input hashes. `rewired_shares.npy`: the
  downstream share and F of each rewired graph. `share_by_dh.csv`. `validation.txt`.
  `environment.json`.
- `files/figure.png`: the summary figure.
- `files/EXTERNAL_NOTICE.md`: external sources, terms and what is not bundled.
