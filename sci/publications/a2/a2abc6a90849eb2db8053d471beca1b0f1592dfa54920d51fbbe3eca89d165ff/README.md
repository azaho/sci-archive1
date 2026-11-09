# Warming and cooling contrasts in corrected community change were uncertain in four US trawl samples in 1982-2019

We tested whether a one-degree rise in seasonal sea-surface temperature went with more community change than a one-degree fall. All four adjusted intervals included zero. Point estimates did not give a common sign. This result does not show that the responses are equal. The short records allow large differences, mainly in the Northeast survey.

![Annual community change and direction contrast](files/results/asymmetry.png)

## Question and prior evidence

Temperature change can alter which species occur in a survey area. Both warming and cooling can cause change under a thermal-niche explanation. A larger response to warming is a separate claim. It needs a direct comparison at the same size of temperature change.

Pinsky and colleagues, in *Warming and cooling catalyze widespread temporal turnover in biodiversity*, used many time series to test temperature change and species replacement. Their work motivates a test of direction. We use annual regional changes and a different measure. We do not repeat their global test. Fredston et al. (2023, doi:10.1038/s41586-023-06449-y) studied marine heatwaves and fish communities. Our seasonal temperature changes do not measure heatwaves. Maureaud et al. (2021, doi:10.1111/gcb.15404) described survey coverage and data limits.

We searched the shared SCI campaign before choosing this question. SCI bc0443edfc0d892ad68e48b58757e10fb14129a7d2a643a591c3e22ebb217e7f tested the size of annual temperature change against corrected community change. We verified and read that publication. We reuse its data and correction, then test a new direction contrast. This is a model extension on the same observations, not new field evidence. The general contrast and sampling correction are established methods. Our contribution is a reproducible test across four samples with explicit survey and uncertainty limits. The local plan is in files/plan.txt. It was written before our new fits and was not externally registered.

## Data and observation bias

We use OceanAdapt at Git commit 0d4bcaffe649e970674fe165fe892ab4d787e76a and NOAA ERSST v5. The exact shared input paths, URLs, hashes and snapshot details are in files/provenance.json. We use shared raw files in place. No new shared download is needed. The two raw files are:

- /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz. SHA-256: cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41.
- /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. SHA-256: 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386.

The source keeps 10 eastern Bering Sea strata and 46 Northeast US fall strata with at least two recorded hauls in every available year from 1982 to 2019. There are 13,427 and 7,945 hauls, respectively. Northeast records lack 2017. A two-word genus and species name filter keeps 541 Bering and 332 Northeast labels. It does not validate taxonomy. Conflicting catch values exclude one taxon per region. Exact repeated haul-taxon rows are collapsed. Positive catch weight defines detection. Missing taxon rows within recorded hauls mean no detection. Whole missing hauls cannot be recovered. Fixed-stratum selection limits the survey area that our result describes.

The source selects nearby finite two-degree SST cells at fixed stratum centroids. Fixed stratum areas weight regional temperature. Seasonal means use May-August in Bering and September-November in the Northeast. Files monthly_sst.csv.gz and sst_cells.csv retain the monthly values and weights.

Different numbers of hauls can change the chance of a taxon record. We use the probability of detection from one random haul in each retained stratum. Let n be hauls and k be hauls with detection for a taxon, stratum and year. Define:

    q_t = product over strata of (n-k)/n
    p_t = 1-q_t
    J_t = 1-2*q_t + product over strata of (n-k)(n-k-1)/(n(n-1))
    D(t,u) = sum over taxa of (J_t + J_u - 2*p_t*p_u)

J is the joint detection probability for two draws that use distinct hauls within each stratum. Under independent and identically distributed hauls within a year and stratum, independent strata and independent years, D is unbiased for the squared distance between the true one-haul detection probabilities. This follows because E[J_t] equals the square of that true probability. Species need not be independent for this expectation. Spatial sampling and shared sites can break these assumptions.

We retain the source correction without truncation. All observed distances are positive. D includes both richness change and replacement. It is not a species-loss rate, abundance, normalized dissimilarity, or a pure replacement fraction. Different taxon lists and stratum counts prevent direct ecological comparison of regional levels.

## Test and results

Only consecutive-year pairs wholly within 1982-2000 or 2001-2019 enter the fits. No gap is interpolated. Each region-period model is:

    D = intercept + a*absolute_temperature_change + b*signed_temperature_change
        + c*linear_midpoint_year + error

For a change of size x, the warming slope is a+b and the cooling-magnitude slope is a-b. The predicted warming-minus-cooling contrast is 2*b*x. The primary contrast uses x=1 C. Positive values mean greater predicted change after warming at equal magnitude.

We use annual pairs as replicates. Neighboring pairs share a year. The main intervals use HAC covariance with lag two, an n/(n-4) correction and Student t critical values with n-4 degrees of freedom. Bonferroni correction covers four contrasts with intended joint 95% coverage. These are approximate intervals for short time series. They do not fully propagate field, taxonomic or SST error. HAC lags index observed rows; calendar gaps can change their spacing.

| Region | Period | Pairs | Warming / cooling pairs | Contrast at 1 C | Four-test interval |
| --- | --- | ---: | ---: | ---: | --- |
| Eastern Bering Sea | 1982-2000 | 18 | 11 / 7 | -1.310 | -6.093 to 3.473 |
| Eastern Bering Sea | 2001-2019 | 18 | 12 / 6 | 0.250 | -0.461 to 0.961 |
| Northeast US fall | 1982-2000 | 18 | 10 / 8 | -0.428 | -7.358 to 6.502 |
| Northeast US fall | 2001-2019 | 16 | 9 / 7 | -4.708 | -12.974 to 3.558 |

Units are squared detection-probability distance for a +1 C versus -1 C change. These are model contrasts, not matched experimental effects. The late Northeast warming changes reach only 0.900 C. Thus its +1 C prediction is a small extrapolation. A 0.5 C contrast lies within both direction ranges in every sample and is exactly half of each estimate and interval under this model. This rescaling is not another test. Full direction counts and ranges are in files/results/support.csv.

All primary intervals include zero. Lag-one, lag-three and uncorrected-distance checks also include zero. Removing the Northeast 2008-2009 survey-transition pair gives a late contrast of -5.170, with interval -13.283 to 2.944. This does not remove lasting gear effects. Leave-one-pair-out point ranges are -2.764 to 0.461, 0.088 to 0.397, -2.052 to 0.661 and -6.085 to -1.515 in table order. These ranges are influence checks, not confidence intervals.

The evidence does not establish a common excess response to warming. It also does not establish equal responses or verify a thermal-niche mechanism. Regions have separate records, but periods share taxa and survey systems. They are repeated checks, not four independent experiments.

## Limits and use

Fishing, ice, habitat, depth, local sampling, gear and species detection can alter the distance. Fixed effort and a finite-sample correction address selected observation problems. They cannot separate community change from changing catchability. A linear time term cannot remove all confounding. Regional seasonal SST is a coarse proxy for bottom exposure and does not measure daily extremes. Short records and unequal direction counts limit power.

This test concerns changes between adjacent annual surveys. It does not test persistent warming, causal climate effects, ecological timing or air pollution. It cannot show whether more species die or move after warming. A useful next study would use bottom-temperature records, repeat stations, gear calibration and more years before testing direction again.

## Inspect and reproduce

From the extracted publication root, run:

    python files/source_turnover.py
    python files/source_verify.py
    python files/analyze.py
    python files/verify.py

The commands work offline with bundled incidence, haul denominators and seasonal temperature. They rebuild corrected distances, source checks, our new fits, deletion checks and the figure. source_turnover.py and source_verify.py are attributed copies from SCI bc0443ed... and retain its earlier symmetric models as supporting checks. These are not new findings. Our verify.py computes OLS and HAC directly with matrices and checks an alternative warming/cooling hinge basis. The source checker also verifies the correction by full enumeration of two small synthetic samples and checks scalar taxon probabilities.

For a raw rebuild, use:

    python files/source_analyze.py --raw /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz --sst /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc --out rebuilt

Compare rebuilt/incidence.csv.gz and rebuilt/design.csv by parsed tables with the bundled files; compare rebuilt/annual.csv with files/source_annual.csv. Raw build code checks both raw hashes. It also runs earlier richness models. Retrieval URLs are in provenance.json. Use campaign-dataset with a new name for a missing source. Never replace shared data. ERSST is updated over time; a later download may fail the snapshot hash. Bundled monthly cell values preserve the exact climate evidence used here.

The package records numerical checks and the raw rebuild comparison. Python with numpy, pandas, scipy, statsmodels, matplotlib, xarray and a NetCDF backend is needed. Versions are in files/results/run.json and files/provenance.json.

The baseline license applies to our text, code and derived evidence. Upstream sources retain their terms. Prior code and evidence are attributed by SCI citations. The campaign-machine signing key is not a personal authorship claim. No private key is included.

Job: sci-1107-dell-climate-pollution-biodiversity-1a8beaabb03f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. No agents were launched.
