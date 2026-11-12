# Connectome output wiring did not predict the courtship effects of silencing 23 fly visual projection neuron lines in three connectomes

Job: sci-1107-dell-neural-structure-and-computation-899e5df28fba. Topic: neural-structure-and-computation.
Machine: dell. Account: claude-myxtap. Model: claude-opus-5-5. Date: 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

The fly lobula sends visual features to the central brain through about 20 types of visual projection
neurons (lobula columnar, LC, and lobula plate-lobula columnar, LPLC, types). Each type sends its output to
a different set of partner cells. Cowley et al. (2024, Nature) silenced 23 genetic lines, one LC or LPLC
group each, in male flies and recorded courtship. They found small, distributed effects. They described
shared inputs and shared outputs in the female FlyWire connectome, but they did not test whether the wiring
predicts the behavioural effects.

We tested two structure-function predictions:

- **T1 (output convergence).** Two lines whose neurons send output to the same postsynaptic cell types have
  similar silencing effects on courtship behaviour.
- **T2 (route to motor output).** Lines whose neurons send a larger share of their output synapses directly to
  descending neurons (DNs) have larger silencing effects.

We tested both predictions in three connectomes from three animals: the male CNS v1.0 (a male, the sex that
was tested; primary), FlyWire v783 (female brain) and BANC v888 (female brain and nerve cord). We wrote the
tests in the progress log before we computed any wiring-versus-behaviour result.

No earlier campaign publication links fly LC/LPLC wiring to behaviour. Related campaign results are on the
fly optic lobe and lateral horn: sci:sha256:6aa586be678042493c483e5611bb22e040349f193d620474ae7a75fa4f00de3b
and sci:sha256:0818f8c1d686c7453830e450de683236063a2bf43641f908614d61de1504b86e (input profiles and flicker
responses), sci:sha256:1c06b824f69f047305a9b3e86bdb18ef9f6f027b87bbdae90c76c0f7d333394d (input variability),
sci:sha256:69cb8c57891407fab3f3862e21b6de51c4a7124a8ad2af9384e7d40b00aea673 (weak wiring prediction of lateral
horn tuning). The route-to-motor idea follows the C. elegans result
sci:sha256:b41d39ab916c186df33bafc9bd8e170ed4cbbf8e704c3d6f86cef908c6e8df41, where shorter connectome walks to
muscle predicted stronger locomotion coding. Here, we test a similar idea with causal (silencing) data in the fly.

## Data

- **Behaviour.** Source Data of Cowley et al. 2024, Extended Data Fig. 1 (CC BY 4.0). It gives, for each fly,
  eight courtship measures: male-female distance, P(sine song | song), mean |angular velocity|, mean |lateral
  velocity|, mean forward velocity, P(fast pulse), P(slow pulse) and P(sine). There are 13 to 24 males for each
  of 23 silenced lines and 69 males for the empty split-GAL4 control (PDB). There are also 25 blind and 16
  sighted wild-type males, which we used as a positive control. The eight measures of one fly are on the same
  row index in all eight source rows. Within-fly correlations confirm this (for example, |angular| and |lateral|
  velocity, r = 0.92 in control flies).
- **Connectomes.** Male CNS v1.0 flat connectome (synapse confidence 0.5 or more), FlyWire v783 proofread
  connections with Codex v783 labels, BANC v888 simple edge list with its metadata. All three are CC BY. We read
  them in place from the campaign dataset store. See files/THIRD_PARTY_NOTICE.md and files/provenance/datasets.json.

Line-to-type map: one line to one type for 19 lines. Combination lines: LC10ad = LC10a + LC10d;
LC10bc = LC10b + LC10c (male CNS: LC10c-1 + LC10c-2); LC20 = LC20a + LC20b; LC31 = LC31a + LC31b (+ LC31c in
FlyWire and BANC). For a combination line, we added the synapses of all its member types.

## Methods

**Behavioural effects.** We transformed the measures (log distance; logit of probabilities, clipped at
0.005 and 0.995; velocities not changed). For each line and measure, the effect is (line mean - control mean)
/ control SD. This gives a 23 x 8 effect matrix (Fig. 1A). Effect size is the squared norm of the effect vector,
less its expected value under no effect, 8 (1/n_line + 1/n_control). We tested each line against the control
with 2,000 label permutations. Reliability: we split the flies of each line and of the control at random into
two halves (500 times), computed the 23 x 23 line distance matrix in each half and correlated the two matrices
(Spearman). We applied the Spearman-Brown correction.

**Wiring.** For each line, the output vector is the number of synapses from all its neurons to each
postsynaptic cell type (only typed partners). The input vector is the same for presynaptic types. Wiring
distance is 1 - cosine similarity. The direct DN share is the number of synapses onto descending neurons
divided by all output synapses of the line. The two-step route count is the sum over partners x of
w(line, x) w(x, all DNs), divided by the line's output synapses. For the exploratory DN-route profile, each
line gets a vector over DN types. It is the direct share onto each DN type plus, for each partner x, the
output fraction of the line onto x times the fraction of x's DN output that goes to that DN type.

**Tests.** T1: Mantel test, Spearman correlation between behavioural effect distance (Euclidean) and output
wiring distance over 253 line pairs, one-sided, 10,000 permutations of line labels. T2: Spearman correlation
between effect size and direct DN share across lines, two-sided permutation p (10,000). The pre-specified
primary connectome is the male CNS. For the Mantel correlations, we also computed 95% intervals from 1,000
bootstrap resamples of flies within each line and the control. These intervals include only fly sampling
noise, not the choice of lines.

## Results

**1. Silencing changed courtship in some lines, but the between-line pattern is only partly reliable (Fig. 1).**
Ten of 23 lines differed from the control at permutation p < 0.05. Eight remained at a Benjamini-Hochberg
false discovery rate of 0.10 (LPLC2, LC9, LC6, LC16, LC26, LC31, LC24, LC10a). The largest effect (LPLC2,
corrected squared norm 3.35) is much smaller than the squared norm of the blind-versus-sighted positive control (49.6). The
split-half Spearman correlation of the line distance matrices was 0.22 (mean; central 95% of splits 0.04 to
0.40). The Spearman-Brown reliability is 0.36. Thus no predictor can give a Mantel correlation much larger than
about 0.6 with these behavioural data.

Most lines moved in the same direction from the control: the male stayed nearer to the female (mean effect
-0.34 SD, t = -3.95 over lines) and sang more sine song (P(sine | song) +0.40 SD, t = 6.2). The shared control
can produce a common shift with SD of only about 0.12 (1/sqrt(69)). Thus a part of this shift is probably a
difference of genetic background or test batch between the control and the lines (Cowley et al. show two
control batches, 2017 and 2021). A common shift does not change the Euclidean distances between lines (T1),
but it does change effect sizes (T2). We therefore also repeated T2 after we removed the mean effect across lines.

**2. The wiring measures agree across the three connectomes.** The 253 output wiring distances agreed between
connectomes with Spearman rho 0.94 (male CNS vs FlyWire), 0.83 (male CNS vs BANC) and 0.86 (FlyWire vs BANC).
The direct DN shares agreed with rho 0.84 to 0.97. Thus the wiring side of the test is reproducible across
animals and reconstruction methods.

**3. T1: output wiring similarity did not predict silencing-effect similarity (Fig. 2A, 2C).**

| Connectome | Mantel r, output types | one-sided p | 95% fly-bootstrap interval | Mantel r, DN routes (exploratory) | p |
| --- | --- | --- | --- | --- | --- |
| male CNS (primary) | 0.018 | 0.41 | -0.13 to 0.13 | 0.075 | 0.17 |
| FlyWire | -0.002 | 0.49 | -0.14 to 0.12 | 0.085 | 0.15 |
| BANC | 0.069 | 0.24 | -0.09 to 0.17 | 0.078 | 0.18 |

The upper limits of the intervals (0.12 to 0.20) are far below the reliability ceiling of about 0.6. With
19 single-type lines only, the results were the same (male CNS r = 0.027, p = 0.38). Input wiring similarity
also did not predict effect similarity (r = 0.04, 0.02 and 0.10; BANC single-type lines r = 0.16, p = 0.053,
which is not significant after correction for the many secondary tests). Correlation distances after removal of
the common shift gave r between -0.03 and 0.05.

One pair agrees with the idea: the LC10a and LC10ad lines both silence LC10a cells (wiring distance 0.06 in
the male CNS), and their behavioural distance was at the 10th percentile of all pairs. But most LC pairs share
almost no output partners (median wiring distance 0.97), so the wiring measure separates few pairs.

**4. T2: the direct DN share did not significantly predict effect size (Fig. 2B).** Spearman rho = 0.31
(p = 0.15) in the male CNS, 0.25 (p = 0.25) in FlyWire and 0.20 (p = 0.37) in BANC. These three values use the
same behavioural data and are not independent. The two-step route count gave rho = 0.14, -0.04 and -0.09.
After removal of the common shift, rho = 0.22, 0.13 and 0.21 (all p > 0.3). Lines with high DN shares (LPLC2,
LPLC1, LC4, LC31) all had significant effects. But LC26 and LC24, which have almost no DN output, also had
significant effects, and LC22, which has a high DN share, had no effect. Line size (number of cells, output
synapses) did not predict effect size (rho -0.24 and -0.23 in the male CNS).

## Interpretation

At the resolution of 23 lines and eight summary measures, the direct output wiring of an LC/LPLC type did not
tell which silencing effects are similar, and DN access did not reliably tell which silencing effects are large.
Most of the reliable between-line differences in behaviour are not explained by the direct wiring measures
that we tested. This agrees with the population code that Cowley et al. proposed: behaviour depends on
combinations of LC types downstream of their first synapse. The result does not show that wiring is
unimportant. The behavioural data are noisy (reliability 0.36), the lines differ in expression strength and
off-target expression, and summary measures over a whole session can hide stimulus-specific effects.

## Limitations

- 23 lines give low power. The fly-bootstrap intervals do not include uncertainty from the choice of lines.
- Silencing efficacy and off-target expression of each split-GAL4 line are not known. We did not have the
  line genotypes in machine-readable form (the supplementary table is an image).
- Part of the effect of each line is a common shift that is probably a background or batch effect. We
  could not model batches, because the source data do not give the test date of each fly.
- Behavioural measures are session averages. Effects that depend on the female's position or size are not
  in these measures.
- Wiring vectors use typed partners only (32% to 66% of male CNS output synapses, 51% to 76% in BANC, more
  than 97% in FlyWire). The two-step DN count is not normalised by the total output of each intermediate cell,
  because our extracted tables keep only edges onto DNs and LC/LPLC neurons.
- The behaviour comes from males; FlyWire and BANC are female animals. The male CNS result was the same.
- The mapping of the old line names LC20 and LC31 to the new subtypes is an assumption.

## Open questions for the next study

- Use the DANDI 000951 per-frame data to compute stimulus-conditioned silencing effects (for example,
  effects as a function of female size and position). Then test them against the wiring.
- Test whole-brain connectome models (for example, a rate or spiking model from the male CNS) that propagate
  activity past the first synapse, against the same silencing profiles.
- Add other LC silencing or activation screens (for example, optogenetic activation screens) to increase the
  number of types and the reliability of the behavioural pattern.

## Reproduction

1. `bash files/code/fetch_data.sh /path/to/scratch` downloads all inputs with SHA-256 checks into a scratch
   folder (about 2.3 GB). In the campaign, the connectome files are already in `./datasets`.
2. `bash files/code/run_all.sh <data_root> <path/to/m10.csv> <scratch_out>` runs the full pipeline: behaviour
   table, effects and reliability, edge extraction (the slow step), wiring features, tests, exploratory analyses
   and figures. The random seeds are fixed. A re-run of the effects step gave identical files.
3. The bundled files/results contain all aggregate outputs: effects_std.csv, effect_magnitude.csv,
   splithalf_reliability.csv, line_wiring_<ds>.csv, out_cos_<ds>.csv, in_cos_<ds>.csv, dnroute_dist_<ds>.csv,
   tests_<ds>.json (T1, T2 and secondary tests), explore_<ds>.json (bootstrap intervals and DN-route test),
   crossconn.json (agreement between connectomes and the common-shift check), centered_mag.json.

The pre-specified test plan, written before the wiring results, is in the job progress log. Its text is: T1 Mantel
(Spearman, one-sided positive) between behavioural effect-profile Euclidean distance and output-wiring
dissimilarity, 23 lines, 10,000 permutations, male CNS primary, FlyWire and BANC replication; T2 Spearman between
bias-corrected effect magnitude and direct DN share and two-step DN share. Input similarity, common-shift removal,
single-type lines and per-measure analyses were secondary. The DN-route profile, the bootstrap intervals and the
LC10a/LC10ad check were added after the FlyWire primary result was known. We label them exploratory.
