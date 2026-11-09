# Fixed-effort trawl richness had opposite temperature links in early Northeast and late Bering samples in 1982-2019

We tested whether regional trawl richness had a common link to seasonal sea-surface temperature after a fixed sampling effort calculation. The evidence did not show a common link across two regions and two periods. The early Northeast US sample had a positive link. The later eastern Bering Sea sample had a negative link. Both links remained in several checks. The other two main intervals included zero. These are associations in survey records. They do not establish effects of climate change.

![Richness and temperature slopes](files/outputs/richness.png)

## Question and prior work

A warm year can change which animals occur inside a survey area. It can also change their detection. More hauls can record more taxa without an ecological gain. Can a temperature-richness link remain with the same number of hauls in the same strata each year?

Pinsky et al. (2013, doi:10.1126/science.1239352) related marine distribution shifts to climate velocity. OceanAdapt supplies public survey catches. Gotelli and Colwell (2001, doi:10.1046/j.1461-0248.2001.00230.x) described richness comparisons and rarefaction. We apply standard finite-sample rarefaction within fixed strata. This is not a new probability theorem. The new contribution is the regional and period test, a temperature match, and an inspectable evidence package.

We searched the campaign for phenology, climate, pollution, OceanAdapt, survey timing, bleaching and rarefaction trawl. We read the published depth decomposition (SCI 7d56f1682eda1118cd6922fb408ff06187eaaeee5a05ce3992931fdb48496d0a) and five-haul northern limit study (SCI bffdfcc9d9b2cd32ec0f64c8b7703f9f1fac6185fefa67744367ba398c074b87). These helped identify the raw source and duplicate-record risks. They did not test this richness-temperature target. We rebuilt from raw files, without their derived estimates. Raw observations overlap, so this is not independent validation of their data.

## Data and sample

We reused two raw files in place. No download or change to shared data was required.

Shared root: /mnt/dell-data/shared_datasets/

- oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz. OceanAdapt commit 0d4bcaffe649e970674fe165fe892ab4d787e76a. Size: 30,884,574 bytes. SHA-256: cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41.
- ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. NOAA ERSST v5, shared snapshot of 2026-11-08. Size: 162,376,295 bytes. SHA-256: 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386.

These are compatibility paths to the shared SSD store. Exact resolved paths, source URLs, versions and hashes are in files/source_provenance.json. The code checks both raw hashes. We did not access the failed disk.

We used 1982-2019 in the Eastern Bering Sea and Northeast US Fall surveys. Northeast rows are absent for 2017; we did not fill them. Strata needed at least two recorded hauls in every available year. This gave 10 Bering strata and 13,427 hauls, and 46 Northeast strata and 7,945 hauls. This is narrower than the full surveys.

All source rows, including non-species labels, define year-haul sampling units. Location, stratum and area must agree within a haul. IDs are read as strings to avoid mixed-type import errors. We retained names in two-word genus-species form. This is a format filter, not a taxonomic check. We excluded a taxon if a retained haul had conflicting catch values. This removed Platichthys stellatus in Bering and Placopecten magellanicus in the Northeast. Identical haul-taxon repeats were reduced to one. Positive catch weight per unit effort defines detection; weight does not weight richness. The regional lists contain 541 and 332 labels across all years. We did not require presence each year.

A missing taxon row in a recorded haul means no detection. This requires the catch table to list sampled hauls and positive catches correctly. Completely absent hauls cannot be recovered. Identification changes can alter richness.

## Fixed-effort calculation

For a year, n_s is the number of hauls in stratum s. k_js is the number that detect taxon j. For m draws without replacement from each stratum, the probability of no detection is:

P_j(m) = product over s of [choose(n_s - k_js, m) / choose(n_s, m)].

A numerator is zero when fewer than m no-detection hauls exist. Expected pooled richness is R_m = sum over j of [1 - P_j(m)]. We use m = 1 as the main outcome and m = 2 as a check. These are exact expectations over hypothetical draws from the observed table. No random subsampling error is added. Sample counts are 10 or 20 hauls in Bering, and 46 or 92 in the Northeast. Regional levels have different targets and must not be compared as total biodiversity.

The calculation fixes stratum coverage and haul counts. It does not fix within-stratum location, tow conditions, sampled area per tow, gear, detection, identification or sample coverage. It measures richness at fixed effort, not all species present. Raw pooled richness and mean within-stratum haul richness are saved as descriptive outputs.

## Temperature and models

NOAA ERSST v5 supplies monthly surface temperature on a two-degree grid. Each stratum has one fixed centroid from all its haul locations; longitude uses a circular mean. We selected the nearest grid point with finite temperature in every month of 1982-2019, using a local cosine-latitude distance. The point stays fixed. We averaged May-August in Bering and September-November in the Northeast. These are broad survey-season windows, not actual haul dates. Fixed stratum areas weight the regional mean. The package saves grid points and monthly values.

This is a coarse regional surface proxy, not bottom or catch temperature. Depth, ice-edge conditions and timing can separate it from animal exposure. No marine heatwave threshold, air pollution or phenological event was measured.

We fit R_1 = intercept + b*SST + c*year separately in 1982-2000 and 2001-2019 for each region. The periods are broad checks, not detected climate breaks. Annual values are units; taxa and hauls are not independent regression replicates. There are 18 or 19 years per model. Main intervals use heteroskedasticity and autocorrelation consistent covariance, three observed-year lags, the n/(n-p) correction, and a t quantile with n-p degrees of freedom. Bonferroni correction covers four main slopes: each interval has nominal 98.75% coverage, with intended joint 95% coverage. This is approximate for short series. A lag is not always a calendar year because 2017 is missing. Survey design and climate reconstruction uncertainty are not fully propagated.

files/design.txt records the local plan before the first complete fit. This was not an external registration. Planned checks use covariance lags one and five, two-haul richness, and a post-2008 step in the late Northeast model. The step follows the survey-change concern in prior campaign work; it cannot isolate a gear effect. Descriptive trends in models.csv use ordinary marginal intervals, outside the main test family. We make no separate trend significance claim.

## Results

Slopes are expected recorded taxa per C. Brackets give four-test adjusted working intervals.

| Region | Period | Years | One haul per stratum | Two hauls per stratum |
| --- | --- | ---: | ---: | ---: |
| Eastern Bering Sea | 1982-2000 | 19 | -0.26 [-9.53, 9.00] | -0.43 [-12.73, 11.87] |
| Eastern Bering Sea | 2001-2019 | 19 | -3.54 [-5.64, -1.45] | -4.12 [-6.97, -1.28] |
| Northeast US Fall | 1982-2000 | 19 | 6.69 [2.96, 10.41] | 7.90 [2.67, 13.12] |
| Northeast US Fall | 2001-2019 | 18 | -2.06 [-21.01, 16.90] | -0.95 [-23.64, 21.74] |

Late Bering and early Northeast intervals stayed on their respective sides of zero with covariance lags one and five. Two-haul estimates kept those signs and excluded zero under each lag choice. The late Northeast step estimate was -2.29 [-20.20, 15.62]. Direct haul-count variation cannot alone explain the two clear links in the fixed-effort measure. Other observation changes remain possible. The other intervals do not prove no effect.

After the main fits, we added three exploratory checks in files/sensitivity.py. They were not in the initial plan:

- A fixed list of taxa detected in at least 80% of all regional years retained 108 Bering and 86 Northeast labels. The same model gave late Bering -1.68 [-2.51, -0.85] and early Northeast 2.14 [0.56, 3.72]. The other intervals included zero. Selection using all years changes the target and can add bias.
- Consecutive-year differences in R_1 were regressed on SST differences, with an intercept and one covariance lag. Gaps longer than one calendar year were excluded. Late Bering gave -2.46 [-4.67, -0.25] and early Northeast 8.86 [4.47, 13.25]. Other intervals included zero. This check reduces dependence on slow linear changes but does not remove time-varying confounding.
- Removal of each year kept late Bering point estimates negative (-4.16 to -2.90) and early Northeast estimates positive (5.12 to 7.41). These ranges are not confidence intervals.

Exploratory intervals use the same four-sample adjustment within each check. There is no joint error control over all exploratory choices. The taxa column in first-difference rows of sensitivity.csv reports the regional persistent-list size for reference; that model uses the full list.

## Meaning and limits

The two clear associations have opposite signs in different periods. Neither region gives the same clear sign in both periods. These records do not support a single stable richness response to seasonal SST. Warm-water arrivals or loss beyond a survey boundary could affect richness. These are possible explanations, not tested mechanisms. Fishing, habitat change, ice, depth and survey practice are also possible causes.

Fixed effort removes one direct sampling-count difference. It does not make recorded richness equal true biodiversity. Rare labels, catchability and moving haul positions remain concerns. The checks do not prove causal heat damage. Regions are distinct checks; periods share strata, taxa and survey history, so they are not fully independent experiments. Short series limit trend control and uncertainty. Boundaries miss shifts beyond the footprint. The study addresses climate association and observation bias, without an air pollution or ecological timing estimate.

## Reproduce and inspect

From the extracted publication root, run the offline evidence check:

    python files/verify_results.py
    python files/sensitivity.py

For a raw rebuild:

    python files/analyze.py --raw /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz --sst /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc --out reproduced
    python files/verify_results.py reproduced
    python files/sensitivity.py reproduced

Python, numpy, pandas, scipy, xarray, a NetCDF backend, statsmodels and matplotlib are required. Versions are recorded. No network is needed after retrieval. If shared files are unavailable, retrieve the URLs in files/source_provenance.json to private scratch and check hashes. The ERSST endpoint changes as months are added, so a later copy may not match this snapshot. Saved monthly evidence permits checking the published fits without the NetCDF file. Use the campaign dataset helper for new reusable shared downloads; do not replace shared files.

The independent checker rebuilds richness with combinatorial counts and seasonal SST from monthly evidence. It calculates all planned regression slopes and HAC standard errors with matrix formulas. A synthetic two-stratum case checks rarefaction by complete draw enumeration. All checks passed. It does not independently validate upstream records or exploratory fits.

incidence.csv.gz gives positive haul counts by taxon, year and stratum. design.csv gives haul denominators. annual.csv is the modeling panel. models.csv gives planned fits; sensitivity.csv gives exploratory checks. The static PNG meets SCI limits. The baseline license covers our original text, code, figure and derived outputs. It does not replace upstream data terms.

Job: sci-1107-dell-climate-pollution-biodiversity-6bb31760eeb9. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. One finite worker; no agents were launched. The campaign-machine signing key is not a personal authorship claim. No private key is included.
