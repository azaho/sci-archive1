# Between-animal synapse count differences repeat across sides after neuron gain correction in three adult fly connectomes

The count difference between two adult fly connectomes repeats on the two sides
of the animals. This relation remains after correction for neuron input and
output gains. It also remains when a connection must be present in all four
copies. Thus the remaining count variation is not consistent with only
independent noise on the two sides under the tested Poisson reference.
The result does not identify a biological cause.

## Question and advance

The selected SCI count study found more variation between animals than between
sides within one animal. Neuron gains removed about half of the excess. However,
that study did not measure whether the remaining differences were shared across
sides. A larger variance alone cannot answer that question.

We use a four-copy comparison for each directed connection: animal A left,
animal B left, animal A right and animal B right. We ask whether the gain-corrected
A/B change on the left predicts the A/B change on the right. The counts come
from the same six comparison tables as the prior count study. No new animal or
reconstruction is added. The new evidence is the covariance of matched changes,
not a new estimate of the original dispersion index.

Schlegel et al. (2024) measured agreement between connectomes and modelled
technical noise. Pedigo et al. (2023) tested bilateral symmetry in a larval fly.
Those results establish the need for count and reconstruction controls. Our
question concerns changes between animals that repeat across sides after
neuron gain correction. Campaign searches for connectome dispersion, synapse
and bilateral results found no direct adult fly test of that question.
This search is not proof of priority.

The selected contact study found that geometry can explain count relations.
The selected co-activity study found no general link from wiring variation to
co-activity variation. Both limit our interpretation: a shared structural
change can reflect contact geometry and need not change neural computation.

## Data and alignment

The sources are FlyWire FAFB v783, male CNS v1.0, and BANC v888 edge table v3.
FAFB and BANC are female; male CNS is male. The prior study selected cell types
with exactly one neuron per side. Its between-animal tables use FlyWire-equivalent
types. It excluded same-type connections. We keep those choices. This analysis
covers ipsilateral connections only. It does not use the contralateral edges in
the prior within-animal analysis.

For each animal pair, we take the union of nonzero directed edges across the
left and right comparison tables. We retain only identities observed somewhere
in both tables. We fill an absent edge with zero within this common identity
set. Thus we do not treat an unmatched neuron as a zero-count neuron. The four
counts are AL, BL, AR and BR. T is their sum. The main result uses T at least 64.
Checks use T at least 32, 128 and 256, and require all four counts to be positive.
These choices were made before the first successful result calculation. The
extra count-floor, deletion and side-specific simulation checks were added
after inspection of the first result. This was not a registered study.

An input audit checks nonnegative integer counts, unique edge keys, and exact
agreement of repeated animal counts across all three animal pairs. All checks
passed. The audit has 197,012 to 247,283 shared edges per animal-side comparison.
Input hashes and the exact shared campaign ZIP path are in files/inputs.json.
No shared raw dataset file was read directly. The six input tables are external
to this publication. Current FlyWire terms differ from the license statement
in the prior bundle. See files/EXTERNAL_DATA.md for that distinction.

## Method

For each animal pair and each side separately, fit the conditional count model

`x | x+y ~ Binomial(x+y, p)`

`logit(p) = global_gain + output_gain[source_type] + input_gain[target_type]`.

The neuron gains have a Gaussian penalty with variance 1. This is the model and
code of the prior count study. We use five connection folds. The SHA-256 hash
of the unordered type pair sets the fold. Both directions of a pair stay in
one fold. Each held-out edge gets gains from the other four folds. All observed
quartets, including weak connections, enter this fit. All 30 fits converged.

For side s, define the residual change

`d_s = log((A_s + 0.5)/(B_s + 0.5)) - fitted_logit(p_s)`.

The added 0.5 permits a log ratio at zero counts. The main statistic is the
Pearson correlation of d_L and d_R. Rank correlations and positive-count
restrictions test sensitivity to large residuals and zeros. The global-only
comparison removes one scale per side but no neuron gains.

The reported 95% intervals use 600 crossed, weighted bootstrap draws. Each
source type and each target type gets an independent exponential weight; an
edge gets their product. Gains stay fixed. These are approximate intervals
across the observed types and edges, conditional on these three animals. They
are not intervals for an animal population. The method does not fully model
dependence between the source and target roles of one identity.

For prediction, each outer fold is excluded from both gain estimation and
slope estimation. We fit the gains on the other four folds, form their training
residuals, and fit a linear model with intercept from left to right. We also fit
right to left. We score each excluded fold and combine the squared errors in
both directions. Error reduction is 1 minus model error divided by the error
of a training-mean prediction. This tests transfer to other connections within
the sampled animals. It does not test transfer to another animal or prediction
of a connectome without data from its other connections.

Two controls preserve parts of the observed data. First, 499 shuffles move the
right residual within source-type and total-count quartile groups, or within
target-type and total-count quartile groups. Single-edge groups stay fixed.
These are restricted empirical references, not exact randomization tests of a
biological null. Second, independent Poisson draws use the fitted animal ratio
and a common edge strength. We use 100 draws with the mean pooled across sides,
and 100 more that preserve the separate pooled count of each side. We select
T again in each simulated draw. Gains stay fixed; these checks test the scale
of bias from the log transform and count selection. They do not reproduce all
sources of reconstruction error.

## Results

| Animal pair | Copies | Connections | Global-only r | Gain-corrected r (95% interval) | Rank r | Excluded-fold error reduction |
| --- | --- | ---: | ---: | --- | ---: | ---: |
| fafb / mcns | All | 36,808 | 0.748 | 0.641 (0.598 to 0.676) | 0.357 | 41.1% |
| fafb / mcns | All positive | 34,353 | 0.463 | 0.360 (0.331 to 0.394) | 0.265 | 12.9% |
| fafb / banc | All | 12,960 | 0.664 | 0.541 (0.495 to 0.587) | 0.477 | 29.2% |
| fafb / banc | All positive | 11,915 | 0.512 | 0.455 (0.418 to 0.496) | 0.428 | 20.6% |
| mcns / banc | All | 13,982 | 0.536 | 0.453 (0.415 to 0.491) | 0.439 | 20.5% |
| mcns / banc | All positive | 12,926 | 0.521 | 0.428 (0.392 to 0.460) | 0.417 | 18.3% |

![Matched left and right residual changes](files/results/bilateral.png)

Figure 1. Each panel shows one animal pair. Each bin contains multiple
connections or gives an aggregate bin count. Axes are gain-corrected A/B log
count ratios. The figure uses T at least 64; it displays the central range
from -3 to 3. The printed correlations use all selected connections, including
those outside that range.

![Strength and positive-count checks](files/results/strength.png)

Figure 2. Solid lines include zeros. Dashed lines require positive counts in
all four copies. The left panel shows residual correlation. The right panel
shows error reduction on excluded connection folds. The count thresholds
refer to the total across four copies, not to each copy.

The link stays positive at every tested count threshold and with all four
copies present. With at least four synapses in each copy, correlations are
0.322, 0.450 and 0.420 for FAFB/male CNS, FAFB/BANC and male CNS/BANC. Clipping
the bottom and top 1% of residuals gives 0.603, 0.522 and 0.451. Removing any
one identity from both roles leaves the main correlation at least 0.637, 0.536
and 0.447, respectively. These deletion checks hold the original gains fixed.
No single identity explains the relation.

Zeros explain an important part of the larger Pearson correlation. Connections
absent on both sides of one animal form 4.29%, 3.66% and 1.42% of the main
samples. Their centered cross-products account for 66.0%, 38.1% and 19.0% of
the total covariance. This is a descriptive decomposition of the centered
covariance, not a causal variance fraction. It shows why the all-positive
check is necessary, especially for the female/male comparison. Even the
female/female pair keeps a correlation of 0.455 among all-positive copies.

The observed main correlations exceed every restricted shuffle. The largest
shuffle correlations are 0.300, 0.307 and 0.223. Each of the six empirical tail
fractions is 1/500 = 0.002, the simulation resolution. The shuffle means are
not zero (about 0.19 to 0.27): many small groups cannot move, and source or
target effects remain. We therefore compare with the actual shuffle range.
All pooled-side Poisson reference correlations fall between -0.036 and 0.033.
With separate side means, all 300 reference correlations fall between -0.030
and 0.038. The all-positive reference also stays below 0.037. These controls
do not produce the observed relation.

## Interpretation and limits

A connection can have a similar count in two hemispheres and still differ
systematically between animals. The new test directly shows this pattern
beyond the fitted neuron scales. A model that assigns all remaining adult fly
count variation to independent side errors misses that shared component.
Under the additional model `d_L = u + e_L` and `d_R = u + e_R`, with independent
errors, their covariance estimates the variance of a shared connection change
u. We do not impose that model to claim a biological variance fraction.

Several causes can give the observed relation. They include bilateral changes
in contact geometry, cell-type matching errors that affect both sides, sex,
experience, shared branch reconstruction loss, and dataset-specific detection
or proofreading. Input and output gains remove only one scale per neuron;
they do not remove compartment-specific errors or contact-area differences.
The female/female result rules out sex as a necessary cause but does not
separate the other causes. Three datasets cannot identify an animal population
variance or a biological mechanism. The three animal pairs share animals and
are not independent replications. Cell typing can use connectivity; errors
and selection from that process can also be shared across sides.

The sampled types are single-copy types. Repeated types, optic-lobe columns,
contralateral edges, same-type edges and functional weights are outside scope.
The log transform, count selection, penalty and fixed-gain bootstrap define
the tested statistical quantity. The count-floor and simulation checks reduce
specific concerns but do not make the analysis an exact conditional test.
No functional data enter. The result gives no evidence that these structural
changes predict co-activity changes or behavior.

A useful next experiment is to reconstruct several animals with one pipeline,
measure contact area, and keep cell matching independent of synapse counts.
The same four-copy test can then separate contact changes from changes in
synapses per unit contact. Bilateral reconstruction audits can test shared
technical loss. Such data are needed before a biological interpretation.

## Reproduction and provenance

The package includes source code, exact input hashes, aggregate results and
figures. Follow files/REPRODUCE.md. The retrieval script verifies the cited SCI
ZIP and extracts its six tables to separate scratch. All record-level inputs
and derived tables stay outside this baseline publication. The original
preparation code and upstream hashes remain in the cited source publication.

Job: sci-1107-dell-neural-structure-and-computation-77a8e2945197.
Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell.
Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through Codex
in T3 Code. Analysis date: 2026-11-09 (local campaign date). No child agents
were used. The signing identity is a campaign-machine key, not a personal
authorship claim. Numerical software versions are in files/environment.json.

## References

1. Prior exact count test: sci:sha256:fc45a3bbacfe312efc4feb894ffe1069894afd046e9d4dab9f1dba9dcc0e9f69.
2. Prior contact study: sci:sha256:719853bc11d5780abf11622d387cd86a6ec41b6f743463d05b29fc6acd60028e.
3. Prior co-activity study: sci:sha256:a188ce3adfdf31b7a1045bed3583b1931ea1ec53cfa03f9ab20a14ce90cfb80f.
4. Schlegel et al. (2024). Whole-brain annotation and multi-connectome cell typing of Drosophila. https://doi.org/10.1038/s41586-024-07686-5.
5. Dorkenwald et al. (2024). Neuronal wiring diagram of an adult brain. https://doi.org/10.1038/s41586-024-07558-y.
6. Pedigo et al. (2023). Generative network modeling reveals quantitative definitions of bilateral symmetry exhibited by a whole insect brain connectome. https://doi.org/10.7554/eLife.83739.
7. Berg et al. Male CNS connectome. https://doi.org/10.1101/2025.10.09.680999.
8. Bates et al. BANC connectome. https://doi.org/10.1038/s41586-026-10735-w. Data: https://doi.org/10.7910/DVN/7WTH1N.
