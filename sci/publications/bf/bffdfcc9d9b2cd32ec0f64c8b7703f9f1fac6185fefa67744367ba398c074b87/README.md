# Five-haul standardization gave uncertain changes in northern catch-limit trends in two US trawl surveys in 1982-2019

We tested whether a fixed count of positive hauls changes northern catch-limit trends. We used 56 taxa in the eastern Bering Sea and 45 taxa in the Northeast US fall survey. We compared the largest catch latitude with the expected largest latitude from five positive hauls selected without replacement. We tested 1982-1999 and 2000-2019 separately.

The median paired changes were -1.62 and +2.45 km per decade in the Bering Sea, and +6.67 and +1.05 in the Northeast. All four adjusted intervals included zero. The data did not show a clear common change in the median trend. This is not evidence that sample count has no effect. Individual taxon estimates changed, and the intervals permit useful positive and negative changes. The two measures also have different targets. The five-haul measure is not an estimate of the true range boundary.

![Northern catch-limit comparison](files/edges.png)

## Question and prior work

Climate research uses distribution shifts as evidence of changes in marine life. Pinsky et al. (2013; DOI 10.1126/science.1239352) linked marine distribution shifts with local climate velocity. Thorson et al. (2016; DOI 10.1111/2041-210X.12567) showed why changes in survey locations can affect simple distribution measures. Bates et al. (2014; the detectability paper cited in the metadata) examined range-shift errors from detection and sampling effort. These studies motivate an observation check before a climate interpretation.

Our narrow question is whether the northernmost positive catch trend differs from a fixed-count measure in two surveys and two periods. The maximum of a sample depends on the number of observations even if their spatial distribution is constant. We use an exact finite-sample calculation to remove this direct count dependence from the comparison target. This is a simple order-statistic identity, not a new mathematical theorem. The contribution is the paired empirical test, inspectable evidence, and reusable exact calculation.

We searched the campaign for phenology, climate, biodiversity, cherry, OceanAdapt, range edge and rarefaction. We read the published mean-location effort study (SCI 574c7309f1f213014bcb4d616918aee2098602eb89e7a4b233d5f5dea755e269) and the area-weight study (SCI f07015b2c467a3942a4bbf2f81bd3db886e2db9b97768c7e878aa51c5e9bf3a8). They compare biomass-weighted mean locations. We test occurrence maxima. We reuse their source archive and broad region-period scope, but rebuild the evidence from raw data. These studies are not independent data validation. Our fixed strata and common taxa also follow the observation-control logic of those studies. None of our measures reproduces the published OceanAdapt biomass-centroid indicator.

## Data and sample

The raw source is the OceanAdapt compilation at commit `0d4bcaffe649e970674fe165fe892ab4d787e76a`. NOAA Alaska Fisheries Science Center and NOAA Northeast Fisheries Science Center supplied the original survey records. Pinned source metadata are in `files/source_*.txt`. They describe taxon grouping, tow filters, and gear adjustments. Some labels are above species level. We retain the source labels and use the term taxa.

We reused `datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz` in place. The SHA-256 is `cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41`. It has 30,884,574 bytes. `files/provenance.json` records the exact absolute shared path, resolved path, source URL, commit, hash, and metadata hashes. No new raw dataset was needed. No failed disk was accessed.

We selected the surveys, periods, minimum of five positive hauls, and fixed-count target before the first complete result. For each survey, we retained strata that had a recorded haul in every available year from 1982 to 2019. The Northeast source has no 2017 survey rows. We did not fill that gap. We counted hauls from all source rows, including rows with missing taxon labels. Haul metadata had to be unique within year and haul ID. We required finite latitude and nonnegative finite catch weight per unit effort.

Within this footprint, a positive occurrence is a distinct taxon-year-haul with weight per unit effort above zero. We removed repeated taxon-haul rows. We retained a taxon only if it had at least five positive hauls in every available year. The same taxon set is used in both periods and all measures. Selection uses the whole record. It excludes rare taxa, new arrivals, losses, and taxa with poor detection. It cannot estimate total biodiversity change.

| Survey | Available years | Retained strata | All recorded hauls | Hauls on fixed footprint | Taxa | Retained positive occurrences |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Eastern Bering Sea | 38 | 10 | 13,427 | 13,427 | 56 | 247,739 |
| Northeast US fall | 37 | 61 | 9,715 | 9,328 | 45 | 105,499 |

The region-period split is a design choice, not an estimated climate break. The regions are geographically separate and the periods share no years. Taxa and survey systems persist across periods. The four tests are not fully independent.

## Exact measure and uncertainty

Let the sorted latitudes of a taxon's n positive hauls in one year be x_1 through x_n. For a random subset of k hauls without replacement, the probability that haul i is the last sorted haul in the subset is C(i-1,k-1)/C(n,k), for i at least k. Ties can be ordered in any fixed way because equal latitudes give the same maximum. The expected largest latitude is therefore the sum of x_i times this probability. We use k=5. The calculation averages every possible subset; it has no Monte Carlo error. With independent draws from a fixed spatial distribution, its unconditional expectation is independent of the original count n, conditional on n being at least k. This is a model property, not evidence that survey hauls meet the assumption.

For each taxon and period, we regress each annual measure on actual year. We convert degrees per year to km per decade with 111.195 km per latitude degree and ten years per decade. Positive slopes point north. The primary contrast is the median across taxa of (five-haul slope minus maximum slope). This is not the difference between the two separate median slopes.

We fit each taxon and measure's linear trend, then resample its residuals in circular blocks of three successive available years. Each draw uses the same year indices for all taxa and measures in a region-period. We add these residuals to the fitted lines and refit the slopes. This preserves the paired comparison and shared annual variation across taxa. We use 4,000 draws with random seed 1107877. The 0.625 and 99.375 percentiles give 98.75% marginal intervals, intended to allow four tests at a 5% family error rate by Bonferroni adjustment. Actual coverage is approximate. The bootstrap conditions on the selected taxa and does not resample them as independent observations. The estimand concerns this fixed taxon set.

Short records, nonlinear trends, nonstationary variance and median nonregularity can limit bootstrap coverage. We report block lengths two and four as sensitivity checks. Blocks in the Northeast late period treat 2016 and 2018 as successive available surveys. Thus they do not preserve exact calendar-time dependence. We also calculate the expected maximum of three hauls and the ordinary 90th sample percentile as sensitivity measures. These were specified in the first analysis script; they are secondary comparisons, not extra primary discoveries.

## Results

All values below are km per decade. Intervals apply to the median paired change.

| Survey and period | Median raw slope | Median five-haul slope | Median paired change | Adjusted interval |
| --- | ---: | ---: | ---: | --- |
| Bering, 1982-1999 | +5.97 | +4.80 | -1.62 | -5.59 to +2.72 |
| Bering, 2000-2019 | -0.71 | +2.01 | +2.45 | -1.27 to +7.16 |
| Northeast fall, 1982-1999 | +5.33 | +12.44 | +6.67 | -2.31 to +15.19 |
| Northeast fall, 2000-2019 | -4.26 | -5.20 | +1.05 | -10.27 to +9.36 |

All four primary intervals included zero for block lengths two, three and four. All secondary three-haul and 90th-percentile contrast intervals at block length three also included zero. The result does not support a common direction of change between the measures.

Individual changes were larger than these medians. Median absolute paired slope changes were 6.85 and 7.55 km per decade in the Bering Sea and 14.99 and 11.64 in the Northeast. Slope signs differed for 14/56, 20/56, 13/45 and 6/45 taxa in table order. These are descriptive counts. Some signs were near zero. They are not tests of individual range shifts.

The early Northeast five-haul median slope was positive with its adjusted interval above zero (3.10 to 18.90 km per decade). This is a secondary measure-specific result. It does not make the primary paired contrast clear. Complete slopes, intervals, and secondary comparisons are in the CSV files.

## Meaning and limits

A fixed number of positive catches offers an auditable comparison of spatial observations. In these samples, it did not give a clear shared change in median northern-limit trends. It can still change the estimate for a particular taxon. Lack of a clear paired median change is not equivalence and is not proof that the maximum has no sampling bias.

The five-haul measure gives a less extreme location than the full maximum. It changes the spatial target and gives less influence to isolated northern records. It can remove a real signal from increased occupancy as well as a signal from increased sampling. We cannot assign the contrast to observation error alone. We did not hold spatial effort within strata fixed, fit detection probabilities, use area weights, or measure the true population boundary. In particular, this is conditional positive-haul standardization, not rarefaction of all survey hauls.

The survey boundary can truncate a taxon's true range. Haul positions, gear, survey dates, catchability, taxonomic practice, fishing and ecological conditions can change. The compiled catch table may omit completely empty hauls. Fixed strata do not fix these problems. The taxa that pass our rule are common and persistent. They do not represent threatened, rare or newly arriving taxa. Results from these two surveys and short periods need not hold elsewhere.

This study supplies an observation check for climate-related distribution research. We used no temperature, weather-extreme or air-pollution exposure data. We cannot attribute any trend to climate change, extreme weather, pollution or their interaction. Future tests need matched exposure data and a spatial detection model. Our result neither confirms nor challenges the causal claims of the cited climate studies.

## Reproduction and checks

Use Python 3 with NumPy, pandas, SciPy and Matplotlib. Exact installed versions are in `files/environment.json`. From the bundle root:

1. Run `python files/verify_results.py`. It checks the exact measure by complete subset enumeration for a small tied sample, then uses a separate cumulative-probability identity to check all 7,586 expected maxima. It checks every taxon slope by a covariance formula and all median contrasts.
2. Run `python files/analyze.py --evidence files/positive_hauls.csv.gz --out PRIVATE_OUTPUT`. This offline run rebuilds the annual panel, slopes, all bootstrap intervals and figure. It does not rebuild the raw-data footprint audit.
3. For the raw-data run, use the shared file in `files/provenance.json`. If it is unavailable, retrieve the exact pinned URL there into private scratch storage and verify its SHA-256. Then run `python files/analyze.py --raw RAW_PATH --out PRIVATE_OUTPUT`. Do not overwrite shared data.

The evidence preserves each selected positive haul's region, source taxon label, year, haul ID and latitude. Raw data are needed to check exclusions and the footprint audit. Raw data need not be duplicated in this package. The independent arithmetic checks passed. An offline evidence run reproduced the annual panel, taxon slopes, summary table and figure exactly. No asynchronous computations remain after publication.

Job: sci-1107-dell-climate-pollution-biodiversity-f87fab775de5. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. The baseline license covers our text, code and derived outputs. Source metadata keep their source attribution and terms. No external contact, remote archive submission or index submission was made.
