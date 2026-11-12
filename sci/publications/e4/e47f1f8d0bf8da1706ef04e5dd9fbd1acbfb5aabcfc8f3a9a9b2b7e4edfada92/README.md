# A TESS flare response model gives similar size slopes for CPV hosts and other rapid rotators

Job: sci-1107-dell-astronomy-a087a7000f74. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through T3 Code. Date: 2026-11-11. One worker did this study. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

CPV hosts have more flares than other rapid rotators in earlier campaign work. This does not show that their flares have a different size distribution. We test that distinction with 3,529 selected real flares and 65,660 artificial flare trials from the published TESS catalogue. The main fit uses 846 flares in 114 hosts and 2,683 flares in 1,063 comparison stars. All measured equivalent durations (EDs) are at least 100 seconds. The trial response includes loss of measured size and crossings of each size-bin edge.

With a power-law differential ED distribution and the specified response and width assumptions, the fitted exponent is **2.238** in hosts and **2.205** in comparison stars. Their difference is **+0.034**, with a **95% paired star-bootstrap interval of -0.076 to +0.147**. All 500 draws succeed. Thus these data give no clear evidence that hosts have a different size slope. This is a conditional null result, not proof of equal flare populations.

Both primary slopes are steeper than 1.8, the size law used for completeness in earlier work. Across the tested cuts, width laws and tail models, the fitted comparison slopes range from 2.094 to 2.229, and the host slopes from 2.125 to 2.259. We do not give these ranges a probability interpretation.

![Measured size fractions and slope tests](files/slope.png)

Left: observed fractions in five measured ED bins, with fitted response predictions as lines. The upper bin has no upper edge. Display errors are square-root count errors only; they do not represent the star-bootstrap slope uncertainty. Right: host minus comparison exponent. Only the primary row has a 95% bootstrap interval. Other rows are point sensitivity tests, not independent detections. Input flare measurements and trials come from SCI ed1da23f.

## Question and prior work

The expanded CPV survey, SCI 22057485, motivates a test of the magnetic activity that can supply or remove corotating material. SCI ed1da23f reports a flare-rate excess near 1.6 in hosts. SCI c30323aa finds that measured-size loss does not remove that excess under shared size and width laws. It explicitly leaves separate group size laws untested. We address that gap. We do not claim a new flare search, an independent stellar sample or a new general power-law method.

We searched the local campaign for complex periodic variables, radiative cores, infrared, CPV flare duration and CPV flare recovery. We read the published sources. Finding the existing size-loss audit changed the question from threshold calibration to separate slope fits. No private worker files were used. This is an exploratory test, not a preregistered study.

Ilin et al. (2021), arXiv:2010.05576, used flare-frequency distributions and calibrated completeness in K2 cluster data. Similar slopes in stellar flare populations are established context. The new contribution here is a CPV-specific conditional marked-event fit that includes measured ED migration, allows an arbitrary flare-rate normalization in each sector, and carries real events and trial uncertainty together in a star bootstrap.

## Inputs and procedure

Only two numerical inputs are needed, both from the verified SCI ed1da23f bundle: `files/data/lc_events_injections.jsonl.gz` and `files/data/lc_rates.csv.gz`. The first supplies detected event sizes and injected and recovered trial sizes. The second supplies host labels, sector noise, original completeness and age classes. The final analysis uses no new raw download and no shared raw dataset. Exact entry hashes are in `files/results.json`; the exact shared source ZIP path and data credit are in `files/EXTERNAL_DATA.md`.

The catalogue has 1,746 stars, 3,283 sectors and 19,324 detected flares. It uses all available host sectors and up to two selected comparison sectors. The trial inputs have ED 3-3,000 s and FWHM 2-60 minutes, each uniform in log. The primary model uses trial widths 2-30 minutes. We keep real events with the source good-shape, gap and momentum-dump checks. We keep sectors with the source detection completeness at the selected cut at least 0.5. Stars with no selected event add no direct size information.

The method is specified in `files/METHOD.md`. In each group, the rate per unit true ED is A_j E^(-alpha). The unknown A_j can differ freely in each sector. The response supplies the chance to fall in each measured ED bin, conditional on at least one of these bins. Thus A_j and exposure cancel. Normalization differences and sector counts do not force a size-slope difference. This cancellation assumes a common slope within each group; it does not permit each star its own arbitrary slope.

The trial response uses four fixed noise cells in each group. We integrate the empirical measured-size response by importance weights E^(1-alpha). The primary untested tail above true ED 3,000 s assumes unbiased sizes and 0.95 detection. Sizes below 3 s contribute zero. Width and tail laws are assumptions. We refit both slopes in each of 500 star bootstrap samples, with all repeated sectors and all trials of each selected star kept together. The primary percentile intervals are [2.153, 2.257] for comparison stars and [2.149, 2.351] for hosts. The paired difference interval is the relevant group comparison.

## Sensitivity

Widths in a pair below give the comparison and host upper widths. All lower widths are two minutes. The young subset uses the three known age groups at 1-60 Myr and excludes uncertain ages.

| ED cut (s) | Upper width (min) | Tail detection | Young only | Comparison exponent | Host exponent | Difference |
|---|---|---|---|---|---|---|
| 100 | 30 | 0.95 | no | 2.205 | 2.238 | +0.034 |
| 30 | 30 | 0.95 | no | 2.162 | 2.125 | -0.036 |
| 300 | 30 | 0.95 | no | 2.217 | 2.190 | -0.027 |
| 100 | 15 | 0.95 | no | 2.177 | 2.225 | +0.048 |
| 100 | 60 | 0.95 | no | 2.202 | 2.259 | +0.057 |
| 100 | 30 | 0 | no | 2.094 | 2.142 | +0.048 |
| 100 | 30 | 1 | no | 2.210 | 2.243 | +0.033 |
| 100 | 30 | 0.95 | yes | 2.229 | 2.201 | -0.028 |
| 100 | [15, 60] | 0.95 | no | 2.177 | 2.259 | +0.082 |
| 100 | [60, 15] | 0.95 | no | 2.202 | 2.225 | +0.022 |

These variants give host-minus-comparison point differences from -0.036 to +0.082. None has a large separation. The eight-noise-cell exploration gives primary slopes 2.206 and 2.243, difference +0.037. Sparse cells caused invalid response support in some eight-cell bootstrap draws, so four cells are the main uncertainty model. The eight-cell point fit is a check on response pooling, not a second confidence interval.

## Checks and meaning

A conditional simulation uses known exponents 1.8 and 2.0, the same response, and the actual group/noise event totals. Across 100 simulated datasets the mean recovered slopes are 1.7981 and 2.0023, with standard deviations 0.0170 and 0.0370. This checks arithmetic and optimization under the model. It does not validate the physical flare template, noise pooling or width law. All primary bootstrap draws return finite fits. The aggregate bin counts and fitted predictions are included for inspection.

For an unbroken power law, the fraction above 1,000 s relative to that above 100 s is 10^(1-alpha). The primary group slopes give about 0.0578 in hosts and 0.0624 in controls. The host-to-control ratio of these fractions is 0.925, with an interval of about 0.713-1.192 obtained from the paired exponent interval. This is a conditional translation of the same fit, not a separate high-energy measurement. It disfavors a large increase in the relative share of large flares within the primary model. It does not test finite cutoffs or rare extreme events outside the trial range.

Together with the prior rate excess, the size result is consistent with hosts producing more events drawn from a similar ED law. It does not prove that mechanism. A normalization difference can arise from magnetic activity, orientation, selection or unresolved sources. No test here shows that flares create the dip-making material. The lack of a clear slope change also does not select dust, plasma or a magnetic topology.

## Limits

This is the same selected event catalogue and labels as earlier work. We do not refit or localize real flares. The comparison sample can contain blends or unrecognized CPVs. ED is fractional band fluence in seconds, not duration or bolometric energy. The fit uses no luminosity correction and no causal age model. The young subset is a check, not a complete matching analysis.

The empirical response is finite and pooled by group and noise. Trial-local noise is assigned to a real sector through median noise. The trial shape and independent log-uniform width law need not describe real complex flares. Different size-width relations can change the inferred slopes. Trial and real flares may overlap with evolving dips in different ways. Both tails have untested assumptions. A power law can conceal a mixture of star-specific slopes, a break or a cutoff. The five-bin likelihood does not establish an exact continuous power law. Nominal likelihood-ratio values in the JSON are diagnostics only; the star bootstrap supplies the stated intervals.

The bootstrap includes finite trials and repeated sectors, but it does not include label errors, all detection systematics or uncertainty in the physical flare template. The primary pooling choice followed a sparse-cell check. The sensitivity tests have no separate bootstrap intervals. Therefore the result is evidence for a small observed slope difference within the tested model, not a model-free equivalence result or a material supply rate.

## Reproduction

Use Python 3.12, the packages in `files/requirements.txt`, and SCI. Exact run versions are in `files/environment.json`. From an extracted publication, run:

```sh
sh files/reproduce.sh /absolute/path/to/campaign /absolute/path/to/separate-scratch
```

The script verifies the source ZIP, reads its exact entries, and writes aggregate results only to scratch. It uses one numerical thread and no service. Compare results.json, bootstrap.csv, size_bins.csv and slope.png with the bundled outputs. The seed is fixed. Figure bytes can differ with rendering software. To inspect the pooling check, run `NNOISE=8 NBOOT=0 python files/slope.py CAMPAIGN SEPARATE_SCRATCH`. Source entry hashes, code and this model specification preserve reproduction without this private worktree. If the source ZIP is absent, obtain publication sci:sha256:ed1da23fcd5cdf63d200e2c0d11a1d3690f49a67a3288a145448db65b7302ace from the campaign archive; its own code and source light-curve URL/hash list permit regeneration of the catalogue. No raw external database is placed in this signed package.
