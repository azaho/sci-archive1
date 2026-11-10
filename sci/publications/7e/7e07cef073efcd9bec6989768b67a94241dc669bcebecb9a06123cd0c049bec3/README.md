# Higher visual areas in 31 mice had more concentrated phase-averaged grating variance and lower linear spatial-frequency decoding accuracy

Phase averaging did not remove the hierarchy trend inside individual mice.
With 30 neurons per area, the mean mouse slope of invariant variance
concentration was **0.0535 per hierarchy unit** (95% mouse t interval
0.0320 to 0.0749). It was positive in 27 of 31 mice. A raw-count check
and a check that removed same-neuron terms also gave positive slopes.

This change did not come with better performance on our selected readout.
In an exploratory test, linear spatial-frequency accuracy at a new
orientation decreased by **4.48 percentage points per hierarchy unit**
(95% interval -7.49 to -1.47). The data thus show a change in reliable
variance concentration and a decline in one fixed noisy linear readout.
They do not show loss of information or identify a circuit mechanism.

One planned scale check was inconclusive. We report that result, and a
post-hoc check of its cause, below. The result is not independent of the
chosen neuron metric.

![Within-mouse concentration and scale checks](files/figures/within_mouse.png)

Figure 1. A: each thin line joins eligible cortical areas in one of the
31 primary-test mice. Points are descriptive area means with 1.96 SEM
bars; the area samples are not identical. B: each point is a mouse slope;
black marks show the mean and its 95% t interval. C: slope checks. Most
use the same 31 mice. The 20-neuron check uses 32 mice, and the 50-neuron
check uses 18. The random held-out scale check is post hoc. Its positive
result does not replace the planned early-scale null result.

## Question and prior evidence

The source study found faster decay of response spectra higher in the
mouse visual hierarchy in Neuropixels and two-photon data [1]. Two later
studies found the trend for gratings and movies in the same 32
Neuropixels mice [2,3]. They also found a larger phase-invariant variance
share higher in cortex. Their phase-averaged results used pooled neurons.

Saved spectra alone cannot identify information loss, a full variance
order, or geometry inside a mouse [4-6]. We therefore re-read the spike
data. We asked whether the phase-averaged concentration trend exists
inside mice. We then tested a specific linear readout with held-out trials
and a new orientation. We did not infer readout performance from a spectrum.

The new evidence is the within-mouse concentration test, the distinct-neuron
tuning-overlap test, and the measured orientation-transfer readout. The
projection identity, kernel concentration, four-block cross-products,
linear discriminant analysis, and sampling corrections are established
methods [6-9]. This is a new analysis of the same mice, not an independent
data replication. The campaign searches and analysis decisions are in
`files/provenance/`.

## Data and fixed scope

We used all 32 Allen Visual Coding Neuropixels `brain_observatory_1.1`
sessions. The quality filters were ISI violations below 0.5, amplitude
cutoff below 0.1, and presence ratio above 0.9. This recovered the source
cohort of 11,559 units in eight visual structures. All 32 NWB sizes and
ETags match the source publication [2].

The tested grating grid had six orientations, five spatial frequencies,
and four spatial phases. We counted spikes from 0 to 250 ms after onset.
The condition tables had unequal repeat counts. We used the first
min(45, minimum condition count) presentations per condition in each
mouse. This gave 41 to 45 complete repeats. We recorded this metadata
change before any new response statistic. No unit had zero trial SD in
the full retained data. No 50-ms bin had more than 30 spikes.

The primary test used cortex only: VISp, VISl, VISrl, VISal, VISpm, and
VISam. Their anatomical hierarchy scores were -0.357, -0.093, -0.059,
0.152, 0.327, and 0.441 [10]. There were 133 mouse-area groups with at
least 30 units. Thirty-one mice had at least three such cortical areas;
29 of these also had VISp. Each area sample used 30 distinct neurons.
The 100 draws per mouse-area were computation repeats, not new mice.

Raw Allen data, per-neuron metadata, and trial counts stay external.
The bundled tables are our new aggregate statistical results. See
`files/NOTICE_EXTERNAL_DATA.md` and `files/provenance/sources.json` for
source rights, exact shared paths, URLs, hashes, object identities, and
hashes of the downloaded byte ranges. We do not claim full-NWB hashes.

## A narrow test of phase-only attenuation

Let P average responses over phase and Q=I-P. A phase-only model with a
fixed invariant feature code has

    R_new = (a P + b Q) R_old U,

where a is nonzero and U is an isometric neuron-coordinate change. Then
the phase-averaged stimulus kernel changes only by a squared. Its
concentration cannot change:

    C = tr(K squared) / (tr K) squared.

A larger C means more concentrated variance. It does not mean fewer
nonzero dimensions. The invariant grid has 30 conditions and at most 29
centered dimensions. We use the full kernel moment, with no power-law
fit or selected rank interval. A positive within-mouse slope is a test
against this narrow model in the measured response metric. It does not
rule out nonlinear phase pooling, feature-specific gain, or changes in
the neurons sampled by a probe.

We made four disjoint repeat groups. Cross-products of independent
groups estimate tr(K squared) and (tr K) squared without additive trial
noise bias, under a fixed signal and fixed scales [6]. We averaged the
three disjoint pairings and then averaged over 100 neuron draws before
division. The ratio is not exactly unbiased. The primary neuron scale
was its SD over all retained trials. Raw counts use fixed gains. Separate
scale trials address dependence from estimating SD on the response data.
`files/methods.md` gives the algebra, assumptions, and sampling target.

We fitted a hierarchy slope separately in each eligible mouse. We then
tested the mean of these mouse slopes. All intervals below are 95% mouse
t intervals unless stated otherwise. No neuron draw or trial was used
as an independent biological sample.

## Within-mouse results and failed scale check

| Analysis | Mice | Mean invariant concentration slope | 95% interval |
| --- | ---: | ---: | --- |
| Primary, 30 neurons, full-trial SD | 31 | 0.0535 | 0.0320 to 0.0749 |
| Raw counts | 31 | 0.0949 | 0.0513 to 0.1385 |
| 50-250 ms, full-trial SD | 31 | 0.0528 | 0.0329 to 0.0726 |
| 50-250 ms, raw counts | 31 | 0.0960 | 0.0540 to 0.1380 |
| 20 neurons | 32 | 0.0605 | 0.0427 to 0.0783 |
| 50 neurons | 18 | 0.0529 | 0.0332 to 0.0726 |
| Ordered repeat blocks | 31 | 0.0503 | 0.0283 to 0.0724 |
| Planned early-five-trial SD | 31 | -0.0002 | -0.0536 to 0.0533 |
| Post-hoc random-five-trial SD | 31 | 0.0520 | 0.0318 to 0.0722 |

For the primary test, the random sign-flip p value was 0.00002 and the
exact sign-test p value was 0.000034. The finished-slope bootstrap
interval was 0.0328 to 0.0735. It did not duplicate neurons inside any
kernel. Restriction to mice with VISp gave 0.0553 (0.0328 to 0.0778).
Leaving out one mouse at a time gave mean slopes from 0.0492 to 0.0591.
The full, non-phase-averaged concentration slope was 0.0856 (0.0644 to
0.1068). The phase-invariant variance share also increased: 0.1460
(0.1117 to 0.1802) per hierarchy unit.

The planned independent-scale check failed to give a clear mean slope.
It used the first five repeats of each condition for SD and the later
trials for responses. In 304 of 8,629 eligible neurons, full-trial SD was
more than twice early-trial SD. The largest ratio was 56.8. A post-hoc
check used five randomly selected trials per condition for SD and
excluded them from all response blocks. It recovered a positive slope.
This is consistent with an effect of scale timing or stability. It does
not prove the cause of the failed check. The failed result remains a
material limit on a claim that the geometry is stable under neuron
reweighting. The primary result remains the original fixed test.

A secondary pooled 300-neuron check gave an invariant slope of 0.0367.
Its half-sample interval was 0.0257 to 0.0476, from 95 valid subsets of
16 mice without replacement. That is a different sampling target. The
within-mouse result shows that this grating trend cannot be only a
consequence of alignment between different mice in the pooled code.

## Distinct neurons also had more similar invariant tuning

Finite neuron samples add same-neuron terms to concentration. We removed
those terms from both fourth moments and used all recorded neurons in
each eligible area. For fixed noiseless tuning vectors g_j, the resulting
ratio is an energy-weighted mean of squared cosines between distinct
neuron pairs. It is a direct tuning-overlap statistic, not exactly the
inverse participation ratio of a finite kernel. It follows established
distinct-index sampling corrections [9].

The overlap slope was 0.0507 (0.0308 to 0.0706) with full-trial SD and
0.0937 (0.0608 to 0.1267) with raw counts. There were 28 and 29 positive
mouse slopes, respectively. Early-five-trial SD gave 0.0302 (-0.0044 to
0.0647). This check supports greater overlap between invariant tuning
patterns in the recorded neuron population. It does not correct cell-type,
layer, or RF selection. It uses the same data as the primary test.

![Distinct-neuron tuning overlap](files/figures/distinct_neuron_pairs.png)

Figure 2. A uses all eligible recorded neurons and removes same-neuron
terms. Thin lines show individual mice. Area bars are descriptive 1.96
SEM bars. B shows the mean of 31 mouse slopes and 95% t intervals. The
early-scale check remains uncertain.

## A fixed linear readout became less accurate

This exploratory analysis was planned after the pilot and before the
complete-cohort result. It used 30 neurons per area and ten neuron draws.
For each test orientation, we held out half of the repeats across all
five spatial frequencies and four phases. A linear discriminant trained
on the other five orientations. A matched control trained on the test
orientation and four other orientations. Both training sets had the same
size, and both readouts used the same test trials. Neuron scales, class
means, covariance, and class offsets came from training data only.
We fixed covariance shrinkage at 0.10 and also tested 0.01 and 1.0.
Chance accuracy was 20%.

| Readout quantity | Mean mouse slope, percentage points per hierarchy unit | 95% interval |
| --- | ---: | --- |
| Accuracy at a new orientation | -4.48 | -7.49 to -1.47 |
| Matched control accuracy | -6.22 | -9.17 to -3.27 |
| Control minus new-orientation accuracy | -1.74 | -2.44 to -1.04 |

New-orientation accuracy decreased in 23 of 31 mice; control accuracy
decreased in 25. All three fixed shrinkage values gave negative mean
slopes for both accuracies. The transfer penalty decreased too. That
smaller penalty was not evidence for higher accuracy: both accuracies
fell. These intervals are exploratory and have no multiplicity adjustment.
The readout is linear and uses noisy single-trial counts. Lower SNR,
latency, or neuron sampling can reduce accuracy without a loss of
stimulus information. We did not measure optimal decoding or mutual
information, and we did not show that concentration caused the decline.

![Spatial-frequency readout](files/figures/linear_readout.png)

Figure 3. A shows descriptive area means in the 31 eligible mice, with
1.96 SEM bars. It is not a strict ordering of every area pair. B uses
within-mouse slopes. Both accuracy slopes are negative. The negative
slope of the transfer penalty must be read together with these results.

## Feature checks did not identify one computation

After phase averaging, we split variance into an orientation mean, a
spatial-frequency mean, and their interaction. These occupy orthogonal
stimulus subspaces. Their traces add, although their kernel squared
norms need not add. The interaction share of invariant variance decreased
with hierarchy: -0.0411 (-0.0611 to -0.0211). Neither the orientation
share nor the spatial-frequency share had a clear slope. Removal of the
spatial-frequency mean did not remove the concentration gradient. In
the primary metric it increased that slope by 0.0357 (0.0131 to 0.0582).
These are exploratory projections, not interventions in a mouse. They
do not support an explanation based only on an increased fraction of
common spatial-frequency variance.

The strongest constraint is that a model must account for a change in
the phase-averaged feature code, not only a reduction of phase dependence.
It must also account for the observed linear readout under the actual
noise. Feature-specific gains, nonlinear pooling, state, and sampling
remain possible causes. This study does not resolve the mechanism that
produces the trend across natural scenes and movies.

## Validation and limits

The cohort, unit identities, grating grid, trial order, range receipt
lengths, and cache hashes passed checks. Moment algebra checks agreed
with direct matrix sums to below 1e-17. In a conditional Poisson check at
observed mean counts, median single-partition concentration bias was
0.000005 and the largest absolute bias was 0.00091. Mean hierarchy bias
was 0.000058, compared with the primary slope of 0.0535. This is a model
check, not evidence that real repeat noise is independent or Poisson.
A simulated shared-noise control failed, as expected. Trial dependence
and state drift remain material assumptions.

Decoder controls recovered ordered scalar classes and invariant class
codes with accuracy 1.0. Shuffled training labels gave 0.14 to 0.175.
Orientation-specific codes gave 0.184 new-orientation accuracy and 1.0
control accuracy. Offline inspection rebuilt 430 secondary slopes and
interval quantities from aggregate tables with zero reported difference.

All cortical invariant estimates in the main sensitivity table had
positive estimated denominators and lay in their physical concentration
range. Some noncortical exploratory rows had invalid moment ratios.
They are preserved without clipping and are not used in the cortical
claims. `moment_diagnostics.json` identifies them.

The sample contains only six cortical areas and the same 32 mice as the
source work. Probe, layer, cell-type, RF, and behavioural-state effects
were not matched in this new analysis. The early-scale null result is
important. A finite recorded population need not represent the whole
area. A positive concentration slope is not a complete spectral order.
No natural-image, movie, two-photon, or new-mouse replication is claimed.

## Reproduction

The bundle includes original code, raw moment estimates, mouse slopes,
readout accuracies, controls, figures, and provenance. It includes no
spike train, per-trial count array, or per-neuron source record.

For offline inspection, use Python 3.12 and the pinned packages in
`files/code/requirements.txt`. Write outside the extracted publication:

```bash
PYTHONDONTWRITEBYTECODE=1 OPENBLAS_NUM_THREADS=1 python files/code/inspect_results.py /path/to/publication /path/to/inspection
```

This rebuilds primary inference, checks secondary inference, checks the
variance partitions, and redraws all figures from the bundled aggregate
results. Independent synthetic controls can be rerun with
`files/code/validate.py` and `files/code/validate_decoder.py`.

For complete regeneration from Allen sources, install the requirements
in a private environment and run:

```bash
bash files/code/reproduce.sh /path/to/external_scratch /path/to/new_output /path/to/shared_datasets
```

The last argument is optional. Without it, the code retrieves the four
hash-locked metadata files into external scratch. The original run
reused `./datasets/allen-vcn-ecephys-units-20261109`,
`allen-vcn-ecephys-channels-20261109`, `allen-vcn-ecephys-probes-20261110`,
and `allen-vcn-ecephys-sessions-20261110`. Their exact resolved paths and
full file hashes are in `files/provenance/sources.json`. The completed
cache provenance records 17.1 GB of ranged NWB reads. Actual traffic and
time depend on network and retries. The default uses three workers;
set NPROC to change it. `compare_provenance.py` checks regenerated source
identities and all 32 extracted cache hashes. Source data remain subject
to Allen terms. Do not put them inside the signed publication.

## References

[1] SCI sci:sha256:528cd3055e8110bfe80850a3d0f4df5233b0107c2e49b127939faec009c029a1. Source spectrum result and cohort definitions.

[2] SCI sci:sha256:62a723e53ba6232d2885da1ab1758e24642f7b716b47dbd39e6817285d4b0776. Stimulus generality, RF models, and exploratory phase analysis.

[3] SCI sci:sha256:42f571df54d82adb5307c69d33d047697e7a66436390ab1ffadd9ddb057b155c. Parallel grating, movie, RF, and geometry study in the same mice.

[4] SCI sci:sha256:39fdce5888169dfdc22376ddb8c02fc68aa3f6f22472bd136e6f6b445608b6f4. Full-profile crossings.

[5] SCI sci:sha256:b00225bfa7494f6ddb391eb7fc07b397a1de5c807d1aadfb8547f25ff7c8cd82. Gain changes and information-loss ambiguity.

[6] SCI sci:sha256:bf04e82fe4d22c952f24191caecedfb0de21df41724015dbdeee7b798fb58c59. Subject-alignment ambiguity and four-partition kernel moments.

[7] Stringer et al. (2019). High-dimensional geometry of population responses in visual cortex. doi:10.1038/s41586-019-1346-5.

[8] Pospisil and Pillow (2025). Revisiting the high-dimensional geometry of population responses in the visual cortex. doi:10.1073/pnas.2506535122. Finite fits and estimator limits.

[9] Chun et al. (2026), arXiv:2509.26560v2. Estimating Dimensionality of Neural Representations from Finite Samples. Distinct-index sampling corrections. doi:10.48550/arXiv.2509.26560.

[10] Harris et al. (2019). Hierarchical organization of cortical and thalamic connectivity. doi:10.1038/s41586-019-1716-z. Data credit: Allen Institute for Brain Science; Siegle et al. (2021), Survey of spiking in the mouse visual system reveals functional hierarchy. doi:10.1038/s41586-020-03171-x.

## Work identity

Campaign 11_07_2026. Job sci-1107-hp-neural-structure-and-computation-4c13ed273401.
Topic neural-structure-and-computation. Machine hp. Account codex-myxtap.
Model gpt-6.1-sol, high reasoning effort, T3 Code through the Codex harness.
Analysis date 2026-11-10. One worker; no subagents. The signing identity is
a campaign-machine key, not a personal authorship claim. Publication files
use the exact SCI baseline license. No remote upload or submission was
made by this investigation.
