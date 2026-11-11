# Temperature-matched TESS counts do not separate a radiative-core CPV effect from the hot-star boundary

Job: sci-1107-dell-astronomy-8e2d600199e8. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite worker did this analysis. The campaign-machine signing key is not a personal authorship claim.

## Result

The released TESS sample has 77 complex periodic variables (CPVs) among 855 young rapid rotators. The 125 stars assigned a radiative core by BHAC15 have no CPVs. We reproduce these counts. But this zero count does not give strong evidence for a core effect separate from the temperature boundary. Most core stars have no useful comparison stars at the same temperature and corotation ratio.

In strata 100 K wide in temperature and 0.25 wide in ln(x), only 10 core stars occur with both no-core stars and at least one CPV. Under equal observed CPV odds within each stratum, the expected core count is 0.837. The exact probability of zero is 0.398. The one-sided 95% upper bound on the core/no-core odds ratio is 4.08. The data in these strata permit equal odds. They do not require a core penalty. With age-class strata as well, no stratum has both core states and a CPV at either 50 K or 100 K resolution, for either radius method and either tested bin origin.

This result limits an interpretation of the earlier core claim. It does not remove the observed hot-star deficit, prove that temperature is its physical cause, or rule out a role for magnetic topology. A model trained across different temperatures can predict 16 CPVs in core stars. That is a transfer-model prediction. It is not a count expected from temperature-matched comparisons.

![Exact conditional bounds](files/conditional.png)

The figure shows the core/no-core observed CPV odds bound from every temperature-plus-x bin scheme without age bins. A value above one permits equal odds. Twenty-three of 24 bounds include one. Labels give temperature width, ln(x) width, and bin shift. A shift of 0.5 moves each bin grid by half its width. The one bound below one uses photometric radii, 200 K bins and a shifted grid. Its unadjusted probability is 0.0467. This isolated result is not robust to the other grids or to age matching.

## Question and prior work

CPVs are rapidly rotating young M dwarfs with sharp dips in their light curves. Material close to corotation is a possible cause. The campaign survey SCI 22057485 supplies labels and periods. SCI 82e139ee assigns young-group age classes and detection efficiencies. SCI fe64afde links the age trend to x = R_cor/R_star. SCI 1edfe4ec corrects the exponent units in that rate law. We use x but make no magnetic-pressure claim from a rate exponent.

SCI b31ef8c8 reports no CPVs in 125 stars with a radiative core and 15.9 detections expected from an x-only fit to no-core stars. It also reports that a temperature cut at 3450 K fits at least as well and states that the physical boundary is not identified. We extend that distinction with exact conditional tests, explicit overlap counts, bounded probabilities, and prediction across withheld age classes.

Gregory et al. (2012, doi:10.1088/0004-637X/755/2/97) relate large-scale magnetic topology to stellar internal structure. That supplies a physical reason to test a core effect, but does not identify its effect on CPV rates. Our test asks whether the released photometric sample separates a core penalty from a temperature boundary. No new observations enter this analysis.

## Data and sample

We use the survey star table and the age-class table from the two signed SCI sources. Input entry hashes are in `files/input_hashes.json`. The source ZIPs are verified before reading. We reuse the unchanged parameter code `01_params.py` from SCI b31ef8c8 as `files/stellar_params.py`. It extends the method of SCI fe64afde. The code uses Baraffe et al. (2015) BHAC15 tracks and the Mamajek dwarf colour table, version 2022.04.16, to compute temperature, model mass, radius and radiative-core mass fraction qrad. Core means qrad > 0.01. It is a model assignment, not a measured core.

The selection follows the core study: rapid flag true, period from 0.15 to less than 1 day, BP-RP from 1.5 to less than 4.2, positive injection efficiency, and age class 1–12, 15–24, 35–60 or 89–200 Myr. Both radius choices retain all 855 stars. x_iso uses the group-age model radius and mass. x_sb uses the luminosity-based Stefan-Boltzmann radius and track mass. The corotation radius is (G M P^2 / (4 pi^2))^(1/3).

No new download was needed. Exact shared table paths used:

- `datasets/bhac15-tracks-structure-20180417-b95474c5/BHAC15_tracks_structure.txt`, SHA-256 b95474c5d4284373a2fed3f06d969a44bcd925ac0e5b226cc0235acb7e068d2a. BHAC15 source file, server version 2018-04-17.
- `datasets/mamajek-dwarf-sequence-20220416-1de2edee/EEM_dwarf_UBVIJHK_colors_Teff.txt`, SHA-256 1de2edeec17bb3346e0e4e70b999de5ee29947df38474e64cddb7cfacc164b7f. Version 2022.04.16.

These paths are relative to the worktree shared link, which resolves to `/mnt/dell-data/shared_datasets`. Original URLs and terms are in `files/EXTERNAL_DATA.md`. Source star tables and derived star records stay outside this publication.

## Method

### Conditional comparison

We partition temperature into widths 50, 100 and 200 K, and ln(x) into widths 0.25 and 0.5. Bin indices are floor(T/width + shift) and floor(ln(x)/width + shift). The shift is 0 or 0.5. We repeat with and without age-class bins, and for both x methods. These are 48 specified sensitivity settings. They were chosen during this analysis, not registered in advance. We report all settings, not a selected small probability.

In a stratum, n1 stars have a core, n0 have no core and k stars have CPV labels. An informative stratum has n1 > 0, n0 > 0 and k > 0. Under equal observed odds, conditional on k, the core CPV count A has a hypergeometric distribution. Its expectation is k n1/(n0+n1). The probability of the observed zero core count is the product over informative strata of choose(n0,k)/choose(n0+n1,k).

For an observed-odds ratio R, each probability is proportional to choose(n1,a) choose(n0,k-a) R^a. We solve P_R(all core counts zero) = 0.05 for the exact one-sided upper confidence bound. No informative stratum means no finite bound. Conditioning removes the arbitrary baseline odds in each bin. It does not remove gradients within a bin, uncertain core labels or different detection efficiencies. The equal-odds null concerns detected CPVs. It is not a test of intrinsic material incidence. Stars and strata are treated as independent.

### Bounded rate fits and prediction

We fit Bernoulli labels with p_i = e_i sigmoid(eta_i), where e_i is the released injection efficiency and eta is an intercept plus linear and squared ln(x/3). Extra terms are: none; linear temperature (T-3300)/300; a core indicator; a T > 3450 K indicator; or core plus linear temperature. We use the published efficiency directly, with no new normalization. Thus this likelihood differs from the source Poisson model. Coefficients have numerical bounds from -25 to 25 to handle separation. These are fit safeguards, not physical priors. Zero-event categories drive the penalty towards those bounds.

Each of the four age classes is then withheld in full. The same models train on the remaining classes. We score the held-out binary labels by negative log likelihood. The 3450 K threshold was selected in the prior study using these same labels. Its withheld scores therefore are descriptive, not an independent validation of that cut. A separate nested scan selects the temperature cut only in training, from 3250 to 3750 K in 25 K steps. This scan checks sensitivity to threshold selection.

## Evidence

The core and temperature definitions agree for 794 of 855 stars (92.9%). All 61 stars where the definitions disagree have no CPVs.

| Model core status | Temperature | Stars | CPVs |
|---|---|---:|---:|
| No core | At most 3450 K | 704 | 77 |
| No core | Above 3450 K | 26 | 0 |
| Core | At most 3450 K | 35 | 0 |
| Core | Above 3450 K | 90 | 0 |

The 26 hot no-core stars are important: a core-only explanation does not explain their zero count automatically. The fitted core model predicts 4.26 CPVs there with x_iso, whereas the temperature model predicts 1.70 among the 35 cool core stars. These are full-sample fit diagnostics, not independent probabilities for rejecting either model.

| Strata, x_iso | Informative stars | Core stars | CPVs | Expected core count under equal odds | P(zero) | Upper odds bound |
|---|---:|---:|---:|---:|---:|---:|
| 50 K, ln(x) width 0.25, shift 0 | 40 | 4 | 5 | 0.500 | 0.579 | 8.23 |
| 100 K, ln(x) width 0.25, shift 0 | 95 | 10 | 8 | 0.837 | 0.398 | 4.08 |
| 200 K, ln(x) width 0.5, shift 0 | 269 | 31 | 24 | 1.292 | 0.226 | 2.33 |
| 100 K, ln(x) width 0.25, shift 0, plus age class | 0 | 0 | 0 | 0 | 1 | No finite bound |

Without age bins, x_iso probabilities range from 0.186 to 0.612. With x_sb they range from 0.0467 to 0.287. At 50 or 100 K, adding age class gives no informative strata in all settings. At 200 K, only four of eight age-matched settings have informative strata. They each contain just one or two core stars and give probabilities from 0.847 to 0.882. The result is lack of overlap, not proof of equal physical rates.

| Model | Full-sample AIC, x_iso | Total withheld log loss, x_iso | Total withheld log loss, x_sb |
|---|---:|---:|---:|
| x only | 485.53 | 246.68 | 250.80 |
| x + linear temperature | 459.22 | 234.19 | 240.52 |
| x + core | 456.35 | 230.81 | 235.98 |
| x + published temperature cut | 450.24 | 227.92 | 235.22 |
| x + core + linear temperature | 453.72 | 229.77 | 235.58 |
| x + nested temperature cut | Not applicable | 274.38 | 271.01 |

Both core and temperature information improve on x alone. The published temperature cut has a small descriptive score advantage over core. The nested scan performs poorly: when the youngest class is withheld it chooses 3375 K and assigns very small probabilities to some young CPVs. Its large loss depends on numerical treatment of separation. It warns against treating a fitted hard boundary as a reliable prediction. It does not prove that the core model is the correct physics. The four folds share training stars, and no independent significance claim is made from these score differences.

![Counts and prediction checks](files/evidence.png)

## Meaning and next test

The strong result is a lack of CPVs in a region of temperature and age, not a unique detection of an internal-structure cause. The conditional method makes that distinction explicit. Core status is computed from temperature and age, so narrow matching can remove almost all core variation. An analysis that holds those inputs fixed cannot create information about a core that was never measured independently.

The useful next observations are in the discordant categories: young hot fully convective stars, and cool stars with securely established cores. Independent temperatures, ages, radii and magnetic maps are needed. More stars far from this boundary can improve the overall x law but provide little direct leverage between core and temperature explanations. K2 evidence of hot very young CPVs, discussed in the source core study, remains relevant and was not retested here.

## Limits

This is an exploratory reanalysis of one selected TESS sample. It does not add new photometry, spectroscopy, manual labels or independent age measurements. The source labels come from one automated vetter. The temperature scale uses dwarf colours for young stars. Age errors, extinction, binaries and magnetic effects on stellar models can move core assignments. Finite bins leave residual differences; fine bins lose overlap. Detection efficiencies are held fixed in the bounded fits and are not removed by the conditional odds test. Multiple bin settings are sensitivity checks, not repeated discovery tests. Failure to distinguish core and temperature does not exclude magnetic support, dust, or gas. We do not estimate material supply or lifetime.

## Reproduction

From any directory, with Python 3.12, numpy, scipy, pandas, pyarrow, matplotlib and sci available, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python /path/to/unpacked/files/reproduce.py /path/to/campaign /path/to/shared_datasets /path/to/separate-scratch
```

The campaign must contain the survey and age source ZIPs named in the script. The two shared tables must have the exact paths and hashes above. The script verifies source ZIPs, checks input hashes, regenerates the stellar table in separate scratch, runs all fits and all conditional settings, and compares aggregate CSV results with this bundle. It never writes external records into the publication. No download is needed with these shared inputs. If the tables are absent, obtain the exact bytes from the URLs in the external notice into separate scratch or with the campaign dataset helper; do not replace a shared dataset.

`margins.csv` gives anonymous aggregate (n0, n1, k) margin counts for each conditional setting, with no star identifiers or bin locations. These counts suffice to inspect the exact probabilities without external records. `validation.json` tests the exact conditional calculation against SciPy's noncentral hypergeometric mass function and checks the likelihood gradient by finite differences. `repeat_check.json` records a fresh full repeat. The package includes code, model coefficients, aggregate counts, scores, all bin tests, source hashes and figures. It contains no raw or derived stellar database. The exact SCI baseline license applies to the bundled files. No remote archive submission was made.
