# Sudden phase resets fit released TESS CPV sector shifts as well as continuous diffusion

Job: sci-1107-dell-astronomy-322789e35a79. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One worker did this study. The campaign-machine signing key is not a personal authorship claim.

## Result

Loss of phase memory between TESS sectors does not require a continuous random walk. We test the full distribution of released dip-minus-spot phase shifts in complex periodic variables (CPVs). A model in which the pattern holds its phase and sometimes jumps to a new uniform phase fits and predicts the data at least as well in the tested comparisons. The small prediction gain has an interval that includes zero. Thus the evidence does not select sudden resets over diffusion. It also does not select diffusion over resets.

The main sample has 1,289 sector pairs from 65 stars. Each star has equal total weight. Five-fold validation keeps all pairs of a star out of training together. The mean held-out log loss is -0.805 for diffusion, -0.880 for resets and -0.877 for a model with both. Lower loss is better. The reset-minus-diffusion difference is -0.075, with a 95% star bootstrap interval of -0.176 to 0.029. Negative log losses are valid for a continuous density measured per cycle.

The reset fit has a phase width of 0.0179 cycles, a mean reset interval of 401 days and a constant uniform fraction of 0.046. These are descriptive fit values, not clump lifetimes or field evolution times. The diffusion fit has a variance rate of 1.02e-5 cycles squared per day, close to the earlier report, but uses a constant uniform fraction of 0.336. A model can explain many large changes either with diffusion or with resets. This changes the interpretation of a fitted diffusion coefficient without removing the observed phase memory.

![Phase memory and held-out scores](files/comparison.png)

Top: fitted probabilities of a relative shift smaller than 0.05 cycles, with equal-star measured fractions in four gap bins. Curves use one gap at a time; points average stars within each gap bin and need not lie on a fitted curve. Bottom: held-out mean log loss. All models are fitted to the full phase distribution, not just the plotted binary fractions.

![Full phase densities](files/densities.png)

The density figure uses the main sample. Black bars are equal-star phase histograms within each gap bin. Each curve averages the fitted density over those same observed gaps and weights. This shows the difference between a broadening peak and a narrow peak that loses weight. The data are sparse at intermediate gaps. These histograms are descriptive and were not used to choose cuts.

## Question and prior evidence

Bouma et al. (2024, doi:10.3847/1538-3881/ad0c4c) describe transient dips in young rapid rotators. Bouma et al. (2026, arXiv:2609.00136v1) report spectra that support magnetically bound circumstellar plasma in four stars and discuss uncertain optical opacity. These studies motivate tests of pattern persistence. Neither makes a photometric template shift a direct material displacement.

SCI b48ce9da reports a relative phase random walk from months to years. SCI 75404ca3 finds that spot changes dominate much of the within-sector relative residual. SCI cede8f8a finds that short-window harmonic changes do not follow the simple small-diffusion order law. Those are different tests. Here we examine the full between-sector relative phase distribution and test jumps to new phases directly. Campaign searches for CPV, radiative core and phase diffusion preceded this choice. A temperature-matched core test had already been published as SCI 8485da75, so we did not repeat it.

The contribution is a model comparison on long-gap phase measurements, with equal star weights, held-out stars, an edge-disjoint sensitivity and explicit alternatives to the diffusion interpretation. We do not claim to introduce circular diffusion or Poisson jumps as new mathematics.

## Data

The direct input is files/data/anchor_pairs.csv.gz from SCI b48ce9dae32069c8fe40342da4e7bf85c6d4f68c68ed5f7a9fc1d9449dd5fa34. The full ZIP passed SCI verification. Its exact shared path and SHA-256, and the entry hash, are in files/provenance.json. No new raw light curves or shared raw datasets are used. Input records remain outside this publication.

The table contains 1,763 pairs from 70 stars. The source obtained the dip shift and spot shift by separate circular cross-correlations of sector templates on a 2,000-point grid. The relative shift is delta = wrap(dip shift - spot shift), in [-0.5, 0.5) cycles. Its templates derive from 443 TESS sector light curves of 126 selected on-target CPVs, sectors 1-107. The source keeps low-order spot and higher-order dip models separate. We do not refit that decomposition.

We use three selections, fixed before fitting these models: the source good-pair cut (dip correlation > 0.5 and spot signal-to-noise > 10), the source strict shape cut (dip correlation > 0.8 and spot correlation > 0.95), and all pairs. We call the good-pair cut the main selection. The strict cut does not also impose the good-pair cut; it follows the source definition.

## Model and estimation

Let W(delta; v) be a wrapped normal density on a circle of circumference one, with zero mean and unwrapped variance v. Let s be a pair-level phase width, q a constant uniform fraction, D a phase variance rate in cycles squared per day, and lambda a reset rate per day. A uniform density on this circle is one. We compare:

    diffusion: f = q + (1-q) W(delta; s^2 + D t)
    reset:     f = 1 - (1-q) exp(-lambda t)
                   + (1-q) exp(-lambda t) W(delta; s^2)
    hybrid:    f = 1 - (1-q) exp(-lambda t)
                   + (1-q) exp(-lambda t) W(delta; s^2 + D t)

The reset process means a jump to an independent uniform longitude, not a return to a fixed longitude. The hybrid follows Brownian phase changes between these jumps. Both leave the difference uniform if any reset occurs. The coefficient D is Var(change)/time, not half that value.

For circular order k > 0, the hybrid has the exact moment

    E cos(2 pi k delta) = (1-q) exp(-2 pi^2 k^2 s^2)
                         exp[-(2 pi^2 k^2 D + lambda)t].

At k = 1, reset decay and diffusion decay can be identical when lambda = 2 pi^2 D, at the same s and q. Higher moments or the full distribution are needed to separate them. A loss of one measure of phase coherence alone cannot establish continuous diffusion. A narrow reset peak and a spreading diffusion peak are different testable predictions.

We minimize minus the weighted log density. A star with n retained pairs contributes weight 1/n per pair. This is a composite score, not the likelihood of independent sector pairs. Shared epochs make pairs dependent. We report no likelihood-ratio p value or ordinary independent-pair AIC. Four optimizer starts use L-BFGS-B. All full-sample fits converge. Bounds are s = 0.001 to 0.3 cycles, q = 0 to 0.98, D = 1e-10 to 0.01 cycles squared per day and lambda = 1e-7 to 1 per day. A fitted value at a bound is disclosed below.

Five folds are assigned by shuffled star identifiers with a fixed seed. Each held-out star contributes its average negative log density. Resampling these 65 held-out star scores 10,000 times gives the interval on the paired score difference. This interval describes star variation conditional on the trained fold models. It does not include the full variation from training-set refits. Four further fold partitions test split sensitivity. The main seed is 322789; the checks use RNG seed 7003. Their integer labels identify successive partitions, not separate RNG seeds.

## Evidence and controls

| Selection | Pairs | Stars | Diffusion log loss | Reset log loss | Hybrid log loss | Reset minus diffusion, 95% interval |
|---|---:|---:|---:|---:|---:|---|
| Main | 1289 | 65 | -0.805 | -0.880 | -0.877 | -0.075 [-0.176, 0.029] |
| Strict shapes | 165 | 44 | -1.952 | -2.009 | -2.030 | -0.058 [-0.253, 0.105] |
| All | 1763 | 70 | -0.689 | -0.756 | -0.772 | -0.067 [-0.148, 0.016] |

Scores should be compared between models within a row. Different selections have different phase distributions. Each interval includes zero. The hybrid has no clear predictive gain in the main sample. The four other main-sample fold partitions give reset-minus-diffusion differences from -0.091 to -0.077. These are sensitivity checks, not four independent replications.

The main diffusion fit reaches the lower bound s = 0.001 cycles. The fitted D is therefore a conditional description with little independent zero-gap width information. It is not a measured physical diffusivity. The main hybrid gives s = 0.0112 cycles, D = 5.39e-6 and a reset interval of 786 days. This trade-off shows that forcing all time evolution into D can change its estimate.

To remove reused sectors, we sort each star's pairs by increasing gap and greedily keep a pair only if neither sector has been used. This cut uses no phase values. It leaves 151 pairs in 65 stars. The equal-star weighted negative composite score is -89.92 for diffusion, -93.77 for resets and -93.88 for the hybrid. Lower is better. Reset s is 0.0180 cycles and its interval is 686 days. This is a full-sample fit sensitivity, not a new held-out test. The reset interval changes under selection, so no universal host or material lifetime follows.

We also fit equal-pair weights as a sensitivity. Exact results are in files/results.json. These fits favour diffusion: its negative composite score is lower than the reset score by 1.94 in the main sample, 12.85 with strict shapes and 21.39 with all pairs. These fits let stars with many sectors dominate and are not the main estimator. The reversal limits any claim that one transition law applies to all stars. Our main question concerns a typical selected star, not a typical available sector pair.

Numerical tests integrate each model density over the circle at four lags and check three analytic circular moments. Errors pass the stated 1e-8 and 1e-9 tolerances. Synthetic recovery tests draw 1,000 independent pairs at empirical gap values from each fitted main model, ten times per model. All 20 fits favour the generating model. Thus the two density families are numerically distinct and the optimizer can separate them in that ideal test. This is not a raw-light-curve injection, an estimate of actual power, or a calibrated significance test for these dependent stars. It does not reproduce template errors or heterogeneous stars.

## Meaning and limits

The released sector shifts support phase memory that weakens with time. They do not require continuous diffusion. A pattern with occasional phase resets is a viable alternative within these tested model families. A reset could arise from a new occulting structure, a new spot group, or a change in which feature dominates cross-correlation. The measurement cannot choose among these causes. The reset rate is not a mass supply rate or a clump destruction rate.

The models assume a common symmetric transition density. Star-to-star diffusion differences, persistent frequency offsets, nonuniform preferred longitudes and phase-dependent selection can give other distributions. We do not exclude them. Strict shape selection acts on the same templates as the measured shift and can preferentially keep coherent patterns. A cross-correlation peak can change between dip groups even without physical motion. There is no independent stellar longitude clock. The fitted width absorbs phase error and small physical changes; no pair-level error covariance is available. The q component can absorb both bad matches and real large shifts. These effects prevent a physical identification of D, q or the reset interval.

The preference changes with pair versus star weights. The sample is selected, has only 65 main stars, and has uneven gap coverage. Many pairs share sectors. Equal star weights and held-out stars reduce, but do not remove, this limitation. The score interval is conditional on five fitted training sets. No new spectra, multi-band data, age measurements or light-curve injections enter the study. These results do not identify dust versus gas, magnetic topology, host duration or a core effect.

A useful next observation is repeated photometry at intermediate lags with stable independent spot or spectroscopic phase markers. Measuring whether the central phase peak broadens or retains its width while losing weight directly tests these alternatives. Sparse long-baseline detections alone can miss the distinction.

## Reproduction and rights

Use Python 3.12 with numpy, scipy, pandas, matplotlib and the SCI CLI. The exact software versions are in files/results.json. Run from any location:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
    python /path/to/files/reproduce.py /path/to/campaign /path/to/separate-scratch

The campaign directory must contain the source ZIP named above. The script verifies that ZIP, extracts the exact input into separate scratch, checks its hash, runs the analysis and all controls, creates two PNGs, and compares the aggregate JSON outputs exactly. It never writes records into the publication. Exact numeric repeat comparison assumes the recorded software versions. Code is serial and uses at most one CPU. No remote archive or index submission is made.

files/results.json holds fit values, prediction scores, intervals, gap-bin counts and validation. files/checks.json holds alternate folds, edge-disjoint fits and synthetic recovery. files/aggregate_histogram.csv holds only gap-bin phase counts. files/provenance.json holds exact input hashes. files/EXTERNAL_DATA.md credits the phase extraction source, the TESS mission and MAST, and identifies external terms. Only our code, text, figures and aggregate results are bundled under the SCI baseline. Source records and raw data stay external.
