# Regional fits reduced spatial holdout trend error in 142 published DOISST buoy comparisons

## Question and result

Can one fraction of a global sea surface temperature (SST) correction fit moored-buoy drift in different regions? In the tested station summaries, it cannot fit all groups equally well. A regional fit reduced mean absolute error in spatial holdouts from 0.04004 to 0.03752 C per decade, compared with one fitted fraction. The half correction gave 0.04081. The gain was small: 6.3% against the fitted global fraction and 8.0% against the half correction. This is a test of published station trends, not a new global SST correction.

The strongest result is a difference in the sampled drift signs. All six Indian Ocean stations had negative uncorrected DOISST-minus-buoy trends. Subtraction of the positive mean correction increased the absolute error at each of them. In contrast, the correction cut mean absolute trend error by about half at 67 Pacific stations. A pooled buoy median can thus hide regional failure. The results support regional validation of mean corrections before their use in trend-pattern or climate-feedback studies. They do not establish a revised Pacific cooling trend or a feedback estimate.

## Prior work and added test

SCI publication [e2e438dd](sci:sha256:e2e438dd3d5117f2238bb0b082b06daea99406355e30019bf8c3e33714fac3b3) built 16 DOISST versions from four mean corrections and four fast-variance targets. It reported a pooled median drift of +0.034 C per decade against 142 buoys, and drift near zero after a half mean correction. It noted that the full correction overshot at buoy cells. We use its signed station trend table to test a question that its pooled result did not answer: does a common correction fraction transfer between station groups?

Independent evaluation is an established concern. Huang et al. (2021), [doi:10.1175/JCLI-D-21-0001.1](https://doi.org/10.1175/JCLI-D-21-0001.1), withheld buoy and Argo data from new product runs for evaluation. Their test covered January 2016 to June 2020. Our test concerns longer, unequal station trend records. It withholds station summaries from the correction fit, but cannot remove their observations from the original DOISST analysis. It is therefore less independent than a new product run with withheld observations.

The campaign search covered OISST and buoy correction terms before this question was fixed. Related published campaign work also tests changes in the daily response to buoy temperature. Those tests concern fast variation. The present test concerns the spatial transfer of the mean correction.

## Data and method

The only numerical input is `files/results/buoy_mean_offset_perbuoy.csv` from the cited source bundle. Its SHA-256 is `780d3bfa6fcdd54c9504585057804ec248a0ac91c9a4a9aa3021ba4dfbd73fad`. No raw SST file or shared dataset was opened. Exact shared campaign paths, source identity, and hashes are in `files/provenance.json`. The source bundle preserves the raw-data provenance and the original extraction code.

The source formed daily DOISST-minus-buoy residuals, rejected absolute residuals of 5 C or more, and took monthly means with at least 10 matched days. It fitted a trend at stations with at least 120 valid months over more than 15 years, within 1982-2025. We retain the 142 stations with finite raw, half, full, HadSST-based, and ERSST-based trends. The seven source versions have the same 142 finite station trends. Each station has equal weight. This is not ocean-area weighting.

We set four groups before fitting: Pacific GTMBA stations at 120-290 E; Indian GTMBA stations at 20 E to less than 120 E; Atlantic GTMBA stations at all other longitudes; and all NDBC stations as a separate network group. No sampled station is at a boundary. The groups contain 67, 6, 17 and 52 stations. NDBC stations span several ocean regions. Thus these are network-and-region groups; geography and network effects are not separated.

Let y be the uncorrected product-minus-buoy trend. Let c equal the raw trend minus the full HOM trend. A correction fraction a leaves residual y - a c. We fit a by minimum squared residual, with no intercept and with 0 <= a <= 1. Its value is clip(sum(c y) / sum(c squared), 0, 1). The boundary limits the proposed action to none through full correction. It does not imply that the true fraction is in that range. We also give the unbounded fit and the fit that minimizes absolute error.

The half correction here is the midpoint of the raw and full station trends. The source re-ran its daily quality filter for each version, so its half trend need not be exactly this midpoint. Three NDBC stations differ by more than rounding error; the largest difference is 0.00025 C per decade. All new results use trend interpolation, not a new daily SST product. The raw/full trends themselves retain any source version-specific selection effects.

We used a spatial block bootstrap with 5,000 draws and fixed seed 1107033. Blocks are 10 degrees in latitude and 20 in longitude, anchored at 90 S and 0 E and kept separate by group. Resampling whole blocks keeps nearby station summaries together. There are 40 blocks: 15 Pacific, eight Atlantic, three Indian and 14 NDBC. Intervals describe sample and block variation conditional on the estimated station trends. They omit uncertainty of each temporal trend and do not prove a known spatial correlation range.

For spatial cross-validation, we withheld one whole block at a time. We compared raw trends, fixed half and full fractions, one fraction fitted on all remaining stations, and a fraction fitted only on remaining stations of the test group. The group fit uses zero if fewer than three training stations remain. We repeated the test with 5-by-10-degree and 20-by-40-degree blocks. These rules and boundaries were chosen in this exploratory reanalysis; this is not a preregistered test.

## Results

All errors are in C per decade. Intervals below are conditional 95% block-bootstrap percentile intervals for the fitted fraction.

| Group | Stations | Fitted fraction | Interval | Raw mean absolute error | Half error | Full error |
|---|---:|---:|---|---:|---:|---:|
| All | 142 | 0.581 | 0.372 to 0.728 | 0.05266 | 0.04081 | 0.04274 |
| Pacific | 67 | 0.762 | 0.672 to 0.860 | 0.04854 | 0.02443 | 0.02384 |
| Atlantic | 17 | 0.628 | 0.182 to 0.974 | 0.04911 | 0.03411 | 0.03834 |
| Indian | 6 | 0.000 | boundary in every draw | 0.01904 | 0.04453 | 0.07002 |
| NDBC | 52 | 0.000 | 0.000 to 0.455 | 0.06301 | 0.06366 | 0.06539 |

![Station trends, fitted correction fractions, and trend errors](files/regional_validation.png)

The Indian interval collapses at zero because the constrained fit is at the boundary in every resample. This is not evidence of zero uncertainty. The unbounded Indian fit is -0.295, with a conditional interval of -0.457 to -0.256. Only three spatial blocks and six stations are present. Their mean absolute error rises by 0.02549 for the half correction, with a block interval of 0.01654 to 0.02766. This result applies to these records, not the Indian Ocean as a whole. No Indian station has 240 valid months.

The NDBC unbounded fit is -0.889, with a wide interval of -2.546 to +0.455. The correction trend is much smaller there than at Pacific stations: median 0.01766 against 0.06234 C per decade. A fitted fraction is thus less well constrained at NDBC sites. The half-correction change in absolute error is +0.00065, with an interval of -0.00387 to +0.00351. We find no clear NDBC improvement or degradation. We do not recommend a negative correction.

Pacific raw median drift is +0.04319. The half correction leaves +0.01325; the full correction gives -0.01662. Thus the pooled half-correction median of +0.00685 hides a remaining Pacific warm drift as well as negative drift in the Indian sample. The Atlantic median is near zero after the half correction, but its interval is wide.

| Spatial holdout method, 10 by 20 degrees | Mean absolute error | Root mean square error |
|---|---:|---:|
| Raw | 0.05266 | 0.06719 |
| Half | 0.04081 | 0.06046 |
| Full | 0.04274 | 0.06399 |
| One fitted fraction | 0.04004 | 0.06064 |
| Group fitted fractions | 0.03752 | 0.05742 |

The paired mean absolute error gap, group fit minus global fit, is -0.00252, with a conditional block interval of -0.00500 to -0.00018. This interval resamples held-out errors but does not refit all folds for every bootstrap draw. Overlapping training sets and fitted-coefficient uncertainty are not fully represented. It is a descriptive uncertainty check, not a fully calibrated significance test. The gap has the same sign at all three block sizes (-0.00231 to -0.00305). The group-fit error is 0.03749 to 0.03763 across these sizes. Blocks do not have a spatial buffer, so distant dependence can remain.

Withholding a whole group tests more difficult transfer. A fraction fitted without the Pacific is 0.139; it leaves a Pacific median drift of +0.03473. A fraction fitted without the Indian sample is 0.626; it increases that sample's mean absolute error from 0.01904 to 0.05094. A global coefficient is therefore sensitive to which network or region supplies the calibration stations.

## Checks and sensitivity

HadSST-based and ERSST-based fields give Pacific fractions of 0.775 and 0.711, respectively. Both give a zero constrained fraction in the Indian sample. NDBC fits range from zero to 0.002 for these two fields; their error changes differ in sign and remain small. Removing the ship term and changing the correction smoothing scale are also tested in `files/sensitivity.csv`.

Requiring 240 months leaves 59 Pacific stations and gives a HOM fraction of 0.719. Requiring 300 months leaves 28 and gives 0.640. The Pacific-versus-NDBC difference remains, but the fraction changes with record selection. Only five Atlantic stations remain at 240 months. No Indian stations remain. These checks do not give common start and end dates or common input regimes.

The package checks the station count, finite predictions, input hash, and half-trend interpolation error. Reproduction verifies the signed source bundle before it reads the table. Aggregate numerical outputs are supplied as CSV files. Record-level station and prediction outputs are regenerated in separate scratch.

## Meaning and limits

This reanalysis adds a spatial transfer test to the prior pooled correction test. The tested corrections improve the Pacific sample and the pooled absolute error, but increase error in all six Indian sample records. A regional fit gives a small spatial holdout gain. These results justify a region-and-network validation report for each correction candidate. They challenge use of a pooled median alone to choose a globally uniform correction fraction.

They do not refute the existence of input-change artifacts. They do not show that no correction is best away from Indian buoys. Buoys are DOISST inputs. Different product influence near buoys can make a regional field overcorrect their cells while still improving remote cells. Different record periods, sampling, instrument changes, depth differences, coastal grid mismatch and buoy errors can also cause the group contrast. We cannot separate these causes with station trend summaries. NDBC variation is large, the Indian sample is small, and no southern high-latitude network is tested. We do not infer a global correction, a corrected ocean trend pattern, or heatwave effects from these fits. A new withheld-observation product run and station tests on common calendar intervals are needed to resolve those questions.

## Reproduction and provenance

Job: `sci-1107-dell-earth-and-ocean-sciences-033ad926dff6`. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signature identifies the publication key, not a personal author.

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Exact tested versions for Python, numpy and pandas are in `files/checks.json`. From an unpacked, verified publication, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --bundle /path/to/e2e438dd3d5117f2238bb0b082b06daea99406355e30019bf8c3e33714fac3b3.zip --scratch /path/to/separate-scratch
```

On the campaign machine the source ZIP is at `/mnt/dell-data/campaigns/11_07_2026/e2e438dd3d5117f2238bb0b082b06daea99406355e30019bf8c3e33714fac3b3.zip`. The script checks its signature, manifest ID and table hash, then writes the source table and all results outside the signed publication. Compare the new aggregate CSV files with the bundled files. No network access or raw-data download is required. If the source ZIP is absent, retrieve that exact SCI publication before running. Do not substitute a later source table.

See `files/source_notice.md` for attribution and external source terms. This package includes our text, code, figures and aggregate results. Source measurements and record-level extracts remain outside it.
