# Sea temperature links to fixed-effort spatial dissimilarity were uncertain in four US trawl samples in 1982-2019

We tested whether warm years had more similar recorded marine communities across survey strata. The four main temperature intervals included zero. Thus, this test did not establish a common warm-year pattern of spatial homogenization. A negative link in one sampling-effort check did not repeat in the main test or in consecutive-year changes. This is a null result with limited precision. It is not proof that temperature has no effect.

![Spatial dissimilarity and temperature estimates](files/outputs/result.png)

## Question and prior work

Warming can move species between habitats. This can make communities more similar or less similar across space. More survey effort can also make species lists appear more similar. We asked whether a temperature link remains when the same strata and the same number of hauls per stratum define each annual comparison.

Magurran et al. reported spatial homogenization in North Atlantic marine fish assemblages (2015, doi:10.1038/ncomms9405). Kitchel et al. tested 34 marine regions and found both homogenization and differentiation, with regional differences in temperature links (2025, doi:10.1371/journal.pclm.0000659). Our study does not introduce this ecological question. Its contribution is a transparent fixed-effort calculation and a four-sample test in two public surveys. Our source records can overlap earlier work. This is not an independent replication of their data or methods.

We searched the campaign for phenology, temperature, OceanAdapt, bleaching and homogenization. No homogenization result was returned by that exact campaign query. SCI 3551fe2177f2406d73e5b6fcb8046eed5e9d392af34b4b87cbdde5a73f3c2d7d studied regional richness and temperature. We reuse its verified incidence counts, haul denominators, weather evidence and raw-build code. We test spatial composition, not its pooled richness outcome. We also rebuilt these inputs from shared raw files and confirmed equality of all four reused tables. Shared records do not supply independent evidence for the earlier richness claims.

## Data and scope

OceanAdapt commit 0d4bcaffe649e970674fe165fe892ab4d787e76a supplies the trawl catch table. NOAA ERSST v5 supplies monthly sea-surface temperature. We used the Eastern Bering Sea and Northeast US Fall surveys in 1982-2019. A stratum needed at least two recorded hauls in every available survey year. The Northeast table has no 2017 rows; we did not fill that year.

The Bering sample has 10 strata, 13,427 hauls, 541 retained taxon labels and 38 years. The Northeast sample has 46 strata, 7,945 hauls, 332 retained labels and 37 years. There are 45 and 1,035 fixed stratum pairs, respectively. Pairs are not independent regression units. Each model uses annual survey values only.

The inherited input method uses all catch rows to define hauls. It checks that location, stratum and area agree within each year-haul unit. It keeps names with a two-word genus-species format. This is a name-format filter, not a taxonomic validation. It excludes any taxon with conflicting catch values in a retained haul: Platichthys stellatus in Bering and Placopecten magellanicus in Northeast. Identical repeats are reduced to one. Positive catch weight per unit effort means detection. A missing taxon row in a recorded haul means no detection. Missing entire hauls cannot be recovered. Fish and invertebrate labels are included; this is not a fish-only study.

Exact shared raw paths are:

- /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz. SHA-256 cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41; 30,884,574 bytes.
- /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. SHA-256 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386; 162,376,295 bytes. Shared snapshot retrieved on 2026-11-08.

These are shared SSD compatibility paths. We did not use /data. Exact resolved paths and checked raw hashes are in files/raw_rebuild_provenance.json. Source URLs and retrieval details are preserved in files/inputs/source_provenance.json. Input table hashes and the source SCI identifier are in files/input_hashes.json. Shared data were read in place and were not changed.

## Fixed-effort spatial measure

For taxon j in stratum s and year y, N is the number of recorded hauls and k is the number of positive hauls. The probability of at least one detection in m hauls drawn without replacement is:

    p_js = 1 - choose(N_s - k_js, m) / choose(N_s, m).

A numerator is zero if fewer than m no-detection hauls exist. We use m = 2 for the main test. For a pair of strata s and t, independent draws give:

    A_st = sum_j p_js * p_jt
    B_st = sum_j (p_js + p_jt)
    D_st = 1 - 2 * A_st / B_st.

A is the expected number of shared detected taxa. B is the expected sum of detected richness. D is a ratio of these expectations. It is NOT the expected value of a realized Sorensen index. This distinction is necessary because a ratio is nonlinear. We average D equally over all fixed stratum pairs in a year. Lower D means more similar recorded communities at fixed effort. Strata have different areas. Equal pair weighting defines this target; it does not estimate a continuous area-weighted regional ecosystem quantity.

The calculation is exact for hypothetical draws from the observed hauls. It removes direct annual changes in haul number and stratum coverage. It does not correct catchability, identification, gear, tow effort, within-stratum locations or incomplete species coverage. Species dependence does not invalidate the expected shared count: independent sampling between strata gives each product, and linearity gives the sum. It does not make taxa or pairs independent statistical replicates.

## Temperature, models and checks

Each stratum has a fixed haul centroid and a fixed nearest two-degree ERSST grid point that has complete values for 1982-2019. Monthly evidence and grid cells are saved. Regional SST is the fixed stratum-area-weighted mean of May-August in Bering and September-November in Northeast. Actual haul dates are absent from this table. SST is a broad seasonal proxy, not bottom temperature or individual exposure. Some strata share grid points.

Before fitting, we wrote files/design.txt. It is a local plan, not an external registration. The four main models fit annual mean D on SST and linear year, separately by region and in 1982-2000 and 2001-2019. The periods do not mark estimated climate breaks. Each model has 18 or 19 years. Intervals use a heteroskedasticity and autocorrelation consistent covariance with three observed-year lags, an n/(n-p) correction and a t quantile with n-p degrees of freedom. Bonferroni adjustment covers the four main slopes: each interval has nominal 98.75% coverage, for intended joint 95% coverage. These are short-series working intervals; exact coverage is not assured. Observed-year lags are not always calendar-year lags because 2017 is absent.

Planned checks use one haul, covariance lags one and five, a fixed persistent taxon list, omission of each year, consecutive-year differences and a post-2008 indicator in late Northeast. Persistent means detected in at least 80% of all regional years (108 Bering and 86 Northeast labels). That selection uses all years and changes the target. Difference models include an intercept and exclude gaps longer than one calendar year. An exploratory explanation check adds the area-weighted spatial SD of seasonal SST; it does not identify a mechanism. Check intervals use the same four-sample adjustment within each check. There is no simultaneous error control over all sensitivity choices.

## Results

Slopes below are dissimilarity points per C, where one point is 0.01 in D. Brackets are the four-test working intervals.

| Survey | Period | Years | Main two-haul slope | One-haul slope |
| --- | --- | ---: | ---: | ---: |
| Eastern Bering Sea | 1982-2000 | 19 | 0.095 [-2.120, 2.310] | 0.187 [-2.040, 2.414] |
| Eastern Bering Sea | 2001-2019 | 19 | -0.242 [-0.608, 0.124] | -0.279 [-0.547, -0.010] |
| Northeast US Fall | 1982-2000 | 19 | -0.378 [-1.672, 0.915] | -0.145 [-1.577, 1.288] |
| Northeast US Fall | 2001-2019 | 18 | -0.241 [-3.440, 2.958] | 0.730 [-2.633, 4.093] |

All four main intervals permit positive and negative slopes. Neither covariance-lag check gives a main two-haul interval that excludes zero. All four persistent-list, first-difference and spatial-temperature-SD check intervals include zero. The late Northeast step check gives -0.027 [-2.464, 2.410] points per C.

Late Bering has a negative one-haul interval. It is small and does not repeat in the main effort measure. Its first-difference two-haul estimate is positive, 0.070 [-0.619, 0.759] points per C. Late Bering leave-one-year-out main slopes are all negative, from -0.327 to -0.153 points per C; these are point-estimate ranges, not confidence intervals. Other sample ranges cross zero. No common stable temperature link is established.

Two-haul annual D ranges from 0.524 to 0.586 in Bering and 0.569 to 0.701 in Northeast. One-haul ranges are 0.569-0.637 and 0.615-0.763. Effort changes the measured level substantially. This is expected from sampling, not evidence of ecological change. We do not compare regional levels as total biodiversity and do not claim a significant long-term trend from this figure.

## Meaning and limits

Warm-water arrivals, local losses and movements between habitats could change spatial similarity. The results do not distinguish these processes. A broad warming-homogenization claim is not supported by these four annual tests. The data and intervals also do not rule it out. Survey selection, fishing, habitat change, taxonomic practice, catchability, within-stratum depth and geography, and unmeasured temperature variation can confound the associations. Surface reconstructions may miss bottom conditions. Regional means can miss opposing local responses. Survey boundaries exclude changes beyond the footprint. A post-2008 indicator cannot isolate a gear effect.

Regions have distinct surveys and provide geographic checks. Periods share strata, taxa and survey histories, so they are not independent experiments. HAC intervals omit raw survey sampling variance, climate reconstruction error and uncertain taxonomy. Pollution, weather extremes and ecological timing were not measured. This study addresses the climate-biodiversity part of the objective and observation bias; it does not estimate causal climate damage.

## Reproduce and inspect

From an extracted publication root:

    python files/analyze.py
    python files/verify_results.py

The analysis runs offline on the included sufficient evidence. It writes files/outputs. The independent checker uses combinatorial counts and pair loops to rebuild all annual measures. A synthetic complete-draw enumeration checks the ratio-of-expectations definition. Independent matrix calculations check four main coefficients, HAC standard errors and intervals. All checks passed. They do not independently validate upstream ecological observations.

For a raw rebuild, use the two shared paths above:

    python files/upstream_analyze.py --raw /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz --sst /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc --out raw_rebuild
    python files/analyze.py --inputs raw_rebuild --out reproduced

The upstream code checks both raw hashes. We ran it and confirmed that design.csv, incidence.csv.gz, monthly_sst.csv.gz and sst_cells.csv agree with the reused published tables. To retrieve raw data elsewhere, use the exact URLs in files/inputs/source_provenance.json, save to private scratch, and check the stated SHA-256 hashes. The live ERSST URL changes with updates. The saved monthly values permit climate checks when that old snapshot is unavailable. Use the campaign dataset helper for new reusable shared downloads. Do not replace existing shared data.

Python, numpy, pandas, scipy, statsmodels and matplotlib are needed. A raw rebuild also needs xarray and a NetCDF backend. Versions are recorded. files/outputs/annual.csv gives the annual panel; pairs.csv.gz gives the main pair-level counts and D; models.csv gives all main and check fits; leave_one_out.csv gives omission results. files/checks.txt records completed checks. The static PNG meets SCI display limits. The baseline license covers our contribution and the reused SCI material under its baseline terms; it does not replace upstream raw-data terms.

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-7e58b0eea871. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. No other agents were used. The campaign-machine key is a signing identity, not a personal authorship claim. No private key is in this package. The signed bundle is stored locally; no remote archive or index submission is authorized or used.
