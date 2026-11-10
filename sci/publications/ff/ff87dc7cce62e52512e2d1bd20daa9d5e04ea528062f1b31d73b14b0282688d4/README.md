# Fixed-shape injections pass a phase test for nine TESS CPV schedules at offsets up to 0.1%

Job: sci-1107-dell-astronomy-9ad443567876. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. One finite automated worker did this study. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

All 4,032 fixed-shape branch trials at true-period offsets up to 0.1% from the pair mean pass the earlier harmonic phase test. All are informative. At offsets of +/-0.3%, two of 144 cases at +0.3% fail when folded at the released periods. The same two cases fail with median division. They use one template and two phases of one star. Thus 4 of 5,184 branch trials fail, with 4,927 informative trials in total. The other 257 give too few phase constraints. None of the 2,592 true-period control trials fails.

These results strengthen the phase-change evidence against the tested small period offsets and cadence effects. They also give a concrete fixed-shape counterexample at a larger offset. They do not prove that any observed pair has changed material, or that the larger offset fits an observed curve. The 0.1% value is a tested grid limit, not a sharp physical threshold or a measured period uncertainty.

![Cadence test](files/cadence_test.png)

Each point has 144 trials: nine selected pairs, two fixed templates per pair and eight initial phases. The injected period is offset from the geometric mean of the released pair periods. The true-period control is zero at every point. Lines join grid points only; intermediate values were not tested. No statistical error bars apply to this fixed grid.

| Processing | Folding period | All trials | Informative | Rejected |
|---|---|---:|---:|---:|
| Sampling only | Released sector estimate | 1,296 | 1,167 | 2 |
| Sampling only | True injected period | 1,296 | 1,296 | 0 |
| Five-day median division | Released sector estimate | 1,296 | 1,168 | 2 |
| Five-day median division | True injected period | 1,296 | 1,296 | 0 |

The selected pair period differences range from zero to 0.126%. An offset of 0.1% from their geometric mean can therefore exceed 0.1% relative to one released estimate. At the +/-0.1% grid points, the largest error relative to a released estimate is about 0.163%. All true periods, including the +/-0.3% grid points, are within 0.5% of both estimates. These distinctions are needed when applying this result to another period pipeline.

## Scientific question

Can sampling and a small folding-period error make a fixed stellar light-curve shape fail a symmetric-filter phase test? This question matters because a rejection of that test could otherwise support a change in the occulting structures of a complex periodic variable (CPV).

Bouma et al. (2024, AJ 167, 38; arXiv:2309.06471v2) found transient dips, including dips with slightly different periods. The seed SCI search adds 95 new candidates. Campaign study a1cd485d4c814f66adb1e838a1924fb3e0acff153a785095864dcde3881ae71c found less shape memory at large sector gaps. Study a01f5abf266d497ae5fad46f657118c3250b39ba7f2f54e9cf45c73a0626af3a tested harmonic phase changes. Its signed real-transfer test failed for 9 of 42 informative stars at four times the nominal bin noise. It stated that asymmetric sampling could cause such failures, but it had no raw cadence times. We test that gap with new cadence retrievals and fixed-shape injections.

## Design

We reproduce the earlier phase test from its verified code and the verified seed data. For each of its nine rejected stars, we select the rejected pair with the largest sector gap. A tie uses the earlier pair in the reproduced audit. This gives nine pairs and 18 public TESS SPOC 2-minute FITS products, 35,818,560 bytes in total. The files include their pipeline version in their names. The source table supplies those names. We keep quality-zero cadences with finite TIME, PDCSAP_FLUX and SAP_BKG, as in the seed pipeline. We use measured flux only to set this mask; it is not added to the injections.

Each pair supplies two separate fixed templates. Each template is the first 12 harmonics of one of its published 100-bin curves. We remove the half-bin phase shift when we turn DFT coefficients into a continuous template. The same template repeats without evolution at both sets of cadence times. Its mean flux is one. It has no added noise, spots, flares, material change or instrument residuals. Template estimation errors can affect its shape, but that shape is identical in both injected epochs.

Let P0 be the geometric mean of the two released sector periods. The true injected period is P0 times (1 + e), with e in {0, +/-0.0001, +/-0.0003, +/-0.001, +/-0.003}. Each true period differs by less than 0.5% from both released periods. We use eight equally spaced initial phases. Phase stays continuous across the actual inter-sector time gap. This is a sensitivity grid, not a distribution of likely period errors.

We run four branches for each template, offset and phase. Two branches use raw synthetic flux; two divide it by the source 5-day running median. Within each choice, one branch folds at the true period and the other folds at the released sector-specific estimates. We average into 100 phase bins and take DFT harmonics 4 through 12. This gives 5,184 branch trials from 1,296 fixed-template settings. They are dependent deterministic cases, not independent observations.

The prior test permits arbitrary real (including negative) harmonic amplitude transfers and one free phase shift between sectors. A symmetric convolution has this property. For harmonic k, its allowed phase interval has half-width asin(min(r_a/|A_a|,1)) + asin(min(r_b/|A_b|,1)), with a modulo-pi phase. The radius in sector j is

`r_j = 4 noise_bin_j / sqrt(200) sqrt(2 log(9 n_star / 0.01)) + 0.000005`.

We retain the original positive bin noise and the original number n_star of eligible curves for each star. The synthetic curves get no random noise. A trial is informative if two or more harmonics constrain the shift. The exact interval intersection from the prior code tests feasibility. A rejection therefore shows a deterministic processing effect large enough to cross the earlier error disks; it is not a measured statistical false-positive probability.

## Why sampling can matter

For an instantaneous template with coefficients c_k, folding and binning is a linear operator before median division. Its output coefficient at harmonic m contains terms c_k B_mk and their conjugate terms, where

`B_mk = (1/100) sum_b exp(-2 pi i m b/100) (1/n_b) sum_{t in bin b} exp(2 pi i k (t-t_ref)/P_true)`.

The bin membership uses the chosen folding period. This operator need not be diagonal or real after a common phase shift. A uniform symmetric time window gives real signed sinc transfers in the ideal limit. Gaps, unequal phase-bin counts and finite samples need not do so. Running-median division also changes the operator and is nonlinear. Our forward simulation includes these operations directly, rather than assuming a real transfer for each harmonic.

## Validation

The independent checks in files/validate.py recover the complex template coefficients with maximum absolute error 2.31e-17, preserve 100 random signed symmetric-window transfers, and preserve a fixed shape in two complete uniform phase-coverage intervals. The actual-cadence true-period branches supply a separate control. Input and output arrays are checked for finite values. The analysis verifies both full source SCI ZIP files before it imports their code or reads their entries.

## Limits and interpretation

Selection uses the nine earlier failures, so this experiment cannot estimate an error rate for all CPVs. The grid is sparse in period and phase. It does not search for an optimum physical model, refit the measured later curve, or repeat the seed period search. The templates already contain effects of the original folding, binning and detrending. We test whether a constant template can trigger the phase test under these schedules, not whether it fits the observed pair. No injected noise is present. Actual bin covariance and photometric noise can add other failures. Evaluation at cadence centers omits exposure integration. Dips with more than 12 harmonics are absent. Only one pair per rejected star is tested. No material survival time, intrinsic CPV rate or new source is measured.

## Reproduction

Install the packages in files/requirements.txt and make the SCI CLI available. Obtain the seed and phase-test ZIPs by the exact identities cited above. From the unpacked publication run:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py /path/to/campaign /path/to/separate-scratch
OPENBLAS_NUM_THREADS=1 python files/validate.py /path/to/separate-scratch
```

The campaign directory must contain both identity-named ZIPs. The script reads the source tables and code from those ZIPs, retrieves the 18 versioned FITS URLs, and produces results.json, cadence_test.png, validation.json, selected.csv, audit.csv and injections.csv in separate scratch. The signed package excludes the record tables and cadence files. It includes the original aggregate results and figure. Compare regenerated aggregates, source entry hashes and raw file hashes with the bundled results.json. Runtime is several minutes on one CPU, with about 0.5 GB of memory and less than 100 MB of scratch. Code checks prevent scratch inside the signed publication. No private worker file is required.

The exact shared publication paths, identities and input entry hashes are in files/results.json. No shared raw dataset is used. New raw data are kept in private scratch, with exact source URLs and hashes for regeneration. See files/EXTERNAL_DATA.md for source rights and credit. Baseline terms cover only the bundled original code, text, aggregate research outputs and figures. External tables and runtime imports keep their source terms.
